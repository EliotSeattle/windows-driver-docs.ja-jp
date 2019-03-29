---
title: プログラミングに関する考慮事項
description: プログラミングに関する考慮事項
ms.assetid: 5f51352a-cfbb-4fa0-98af-953b151a4563
keywords:
- ネットワーク モジュールのレジストラー WDK、プログラミングの考慮事項
- NMR WDK、プログラミングの考慮事項
- 参照カウントの WDK ネットワーク モジュールのレジストラー
- 進行中は、WDK ネットワーク モジュールのレジストラーを呼び出す
- WDK ネットワーク モジュールのレジストラーの参照をカウント
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 32430060bb81ec3526dbd0f3568abd828a1005da
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2019
ms.locfileid: "57349607"
---
# <a name="programming-considerations"></a>プログラミングに関する考慮事項


ネットワーク モジュールは、何らかの形式の参照カウントに接続されているネットワーク モジュールの実行中の呼び出しの数を追跡するを使用する必要があります[ネットワーク プログラミング インターフェイス (NPI)](network-programming-interface.md)関数。 これには、NMR で 2 つのネットワーク モジュールのいずれかの登録を解除するとき、接続されているネットワーク モジュールからのデタッチが容易になります。 ネットワーク モジュールは、接続されているネットワーク モジュールの NPI 関数の実行中の呼び出しがなくなるまで、デタッチを完了できません。 ネットワーク モジュールは、ネットワーク モジュールをデタッチ後に、以前に接続されているネットワーク モジュールに電話を開始することを確認する必要がありますもします。

たとえば、クライアント モジュールでは、プロバイダーが接続されているモジュールの NPI 関数の実行中の呼び出しの数を追跡するため、次のような実装を使用する可能性があります。

```C++
// Context structure for the client's binding to a provider module
typedef struct CLIENT_BINDING_CONTEXT_ {
  LIST_ENTRY Link;
  HANDLE NmrBindingHandle;
  PVOID ProviderBindingContext;
  PEXNPI_PROVIDER_DISPATCH ProviderDispatch;
  KSPIN_LOCK DetachLock;
  LONG InProgressCallCount;
  LONG Detaching;
  .
  . // Other client-specific members
  .
} CLIENT_BINDING_CONTEXT, *PCLIENT_BINDING_CONTEXT;

// Pool tag used for allocating the binding context
#define BINDING_CONTEXT_POOL_TAG 'tpcb'

// Structure for the client's dispatch table
const EXNPI_CLIENT_DISPATCH Dispatch = {
  .
  . // Function pointers to the client module's
  . // NPI callback functions
  .
};

// Head of linked list of binding context structures
LIST_ENTRY BindingContextList;

// Spin lock for binding context list
KSPIN_LOCK BindingContextListLock;

// Prototype for the client module's unload function
VOID
  Unload(
    PDRIVER_OBJECT DriverObject
    );

// Variable to contain the handle for the registration
HANDLE ClientHandle;

// DriverEntry function
NTSTATUS
  DriverEntry(
    PDRIVER_OBJECT DriverObject,
    PUNICODE_STRING RegistryPath
    )
{
  NTSTATUS Status;

  // Specify the unload function
  DriverObject->DriverUnload = Unload;

  // Initialize the binding context list spin lock
  KeInitializeSpinLock(
    &BindingContextListLock
    );

  // Initialize the binding context list head
  InitializeListHead(
    &BindingContextList
    );

  .
  . // Other initialization tasks
  .

  // Register the client module with the NMR
  Status = NmrRegisterClient(
    &ClientCharacteristics,
    &ClientRegistrationContext,
    &ClientHandle,
    );

  // Return the result of the registration
  return Status;
}

// ClientAttachProvider callback function
NTSTATUS
  ClientAttachProvider(
    IN HANDLE NmrBindingHandle,
    IN PVOID ClientContext,
    IN PNPI_REGISTRATION_INSTANCE ProviderRegistrationInstance
    )
{
  PNPI_MODULEID ProviderModuleId;
  PEXNPI_PROVIDER_CHARACTERISTICS ProviderNpiSpecificCharacteristics;
  PCLIENT_BINDING_CONTEXT BindingContext;
  PVOID ProviderBindingContext;
  PEXNPI_PROVIDER_DISPATCH ProviderDispatch;
  KLOCK_QUEUE_HANDLE BindingContextListLockHandle;
  NTSTATUS Status;

  // Get pointers to the provider module's identification structure
  // and the provider module's NPI-specific characteristics structure
  ProviderModuleId = ProviderRegistrationInstance->ModuleId;
  ProviderNpiSpecificCharacteristics =
    (PEXNPI_PROVIDER_CHARACTERISTICS)
      ProviderRegistrationInstance->NpiSpecificCharacteristics;

  //
  // Use the data in the structures pointed to by
  // ProviderRegistrationInstance, ProviderModuleId,
  // and ProviderNpiSpecificCharacteristics to determine
  // whether to attach to the provider module.
  //

  // If the client module determines that it will not attach
  // to the provider module
  if (...)
  {
    // Return status code indicating the modules did not
    // attach to each other
    return STATUS_NOINTERFACE;
  }

  // Allocate memory for the client's binding context structure
  BindingContext =
    (PCLIENT_BINDING_CONTEXT)
      ExAllocatePoolWithTag(
        NonPagedPool,
        sizeof(CLIENT_BINDING_CONTEXT),
        BINDING_CONTEXT_POOL_TAG
        );

  // Check result of allocation
  if (BindingContext == NULL)
  {
    // Return error status code
    return STATUS_INSUFFICIENT_RESOURCES;
  }

  // Initialize the client binding context structure
  KeInitializeSpinLock(
    &BindingContext->DetachLock
   );
  BindingContext->InProgressCallCount = 0;
  BindingContext->Detaching = 0;
  ...

  // Continue with the attachment to the provider module
  Status = NmrClientAttachProvider(
    NmrBindingHandle,
    BindingContext,
    &Dispatch,
    &ProviderBindingContext,
    &ProviderDispatch
    );

  // Check result of attachment
  if (Status == STATUS_SUCCESS)
  {
    // Save NmrBindingHandle, ProviderBindingContext,
    // and ProviderDispatch for future reference
    BindingContext->NmrBindingHandle =
      NmrBindingHandle;
    BindingContext->ProviderBindingContext =
      ProviderBindingContext;
    BindingContext->ProviderDispatch =
      ProviderDispatch;

    // Acquire the binding context list spin lock
    KeAcquireInStackQueuedSpinLock(
      &BindingContextListLock,
      &BindingContextListLockHandle
      );

    // Add this binding context to the list of valid
    // binding contexts
    InsertTailList(
      &BindingContextList,
      &BindingContext->Link
      );
 
    // Release the binding context list spin lock
    KeReleaseInStackQueuedSpinLock(
      &BindingContextListLockHandle
      );
  }

  // Attachment did not succeed
  else
  {
    // Free memory for client's binding context structure
    ExFreePoolWithTag(
      BindingContext,
      BINDING_CONTEXT_POOL_TAG
      );
  }

  // Return result of attachment
  return Status;
}

// Wrapper function around a provider NPI function
//
// Each of the provider NPI functions should be wrapped
// in this manner.
NTSTATUS
  ProviderNpiFunctionXxx(
    ClientBindingContext,
    .
    . // Parameters to the provider NPI function
    .
    )
{
  KLOCK_QUEUE_HANDLE BindingContextListLockHandle;
  KLOCK_QUEUE_HANDLE DetachLockHandle;
  PCLIENT_BINDING_CONTEXT BindingContextListElement;
  PLIST_ENTRY Entry;
  NTSTATUS Status;

  // Acquire the binding context list spin lock
  KeAcquireInStackQueuedSpinLock(
    &BindingContextListLock,
    &BindingContextListLockHandle
    );

  // Search for the binding context in the list of valid
  // binding contexts
  for (Entry = BindingContextList.Flink;
       Entry != &BindingContextList;
       Entry = Entry->Flink)
  {
    // Get the next binding context from the list
    BindingContextListElement =
      CONTAINING_RECORD(
        Entry,
        CLIENT_BINDING_CONTEXT,
        Link
        );

    // Check if this binding context is a match
    if (BindingContextListElement == ClientBindingContext)
    {
      // Break out of the search loop
      break;
    }
  }

  // Check if the binding context was not found
  if (Entry == &BindingContextList)
  {
    // Release the binding context list spin lock
    KeReleaseInStackQueuedSpinLock(
      &BindingContextListLockHandle
      );

    // Return status indicating that the interface is not available
    return STATUS_NOINTERFACE;
  }

  // Acquire the detach spin lock at DPC level
  KeAcquireInStackQueuedSpinLockAtDpcLevel(
    &ClientBindingContext->DetachLock,
    &DetachLockHandle
    );

  // The modules should not be detaching
  ASSERT(ClientBindingContext->Detaching != 1);

  // Increment the in-progress call count
  ClientBindingContext->InProgressCallCount++;

  // Release the detach spin lock from DPC level
  KeReleaseInStackQueuedSpinLockFromDpcLevel(
    &DetachLockHandle
    );

  // Release the binding context list spin lock
  KeReleaseInStackQueuedSpinLock(
    &BindingContextListLockHandle
    );

  // Call the provider NPI function
  Status =
    ClientBindingContext->ProviderDispatch->ProviderNpiFunctionXxx(
      ClientBindingContext->ProviderBindingContext,
      .
      . // Parameters to the provider NPI function
      .
      );

  // Check if pending
  if (Status == STATUS_PENDING)
  {
    // If completion of the call is pending, then when the call
    // completes, the completion routine (or other callback function
    // that is called upon completion of the call) must include the
    // the same code as below for the non-pending case.

    // Return pending status
    return STATUS_PENDING;
  }

  // Acquire the detach spin lock
  KeAcquireInStackQueuedSpinLock(
    &ClientBindingContext->DetachLock,
    &DetachLockHandle
    );

  // Decrement the in-progress call count
  ClientBindingContext->InProgressCallCount--;

  // Check if the modules are now detaching
  if (ClientBindingContext->Detaching == 1)
  {
    // Check if this call was the last of the in-progress
    // calls to the provider module to be completed
    if (ClientBindingContext->InProgressCallCount == 0)
    {
      // Release the detach spin lock
      KeReleaseInStackQueuedSpinLock(
        &DetachLockHandle
        );

      // Inform the NMR that detachment is complete
      NmrClientDetachProviderComplete(
        ClientBindingContext->NmrBindingHandle
        );
    }
    else
    {
      // Release the detach spin lock
      KeReleaseInStackQueuedSpinLock(
        &DetachLockHandle
        );
    }
  }
  else
  {
    // Release the detach spin lock
    KeReleaseInStackQueuedSpinLock(
      &DetachLockHandle
      );
  }

  // Return status of the call to the provider NPI function
  return Status;
}

// ClientDetachProvider callback function
NTSTATUS
  ClientDetachProvider(
    IN PVOID ClientBindingContext
    )
{
  PCLIENT_BINDING_CONTEXT BindingContext;
  KLOCK_QUEUE_HANDLE BindingContextListLockHandle;
  KLOCK_QUEUE_HANDLE DetachLockHandle;
  NTSTATUS Status;

  // Get a pointer to the binding context
  BindingContext = (PCLIENT_BINDING_CONTEXT)ClientBindingContext;

  // Acquire the binding context list spin lock
  KeAcquireInStackQueuedSpinLock(
    &BindingContextListLock,
    &BindingContextListLockHandle
    );

  // Remove the binding context from the binding context list
  RemoveEntryList(&BindingContext->Link);

  // Acquire the detach spin lock at DPC level
  KeAcquireInStackQueuedSpinLockAtDpcLevel(
    &BindingContext->DetachLock,
    &DetachLockHandle
    );

  // Set the flag indicating that the client module is detaching
  // from the provider module so that the completion of the final
  // call will complete the detachment
  BindingContext->Detaching = 1;

  // Check if there are no in-progress NPI function calls to the
  // provider module
  if (BindingContext->InProgressCallCount == 0)
  {
    // Set the status to success to indicate detachment is complete
    Status = STATUS_SUCCESS;
  }

  // There are one or more in-progress NPI function calls
  // to the provider module
  else
  {
    // Set the status to pending to indicate that detachment is
    // pending completion of the in-progress NPI function calls
    Status = STATUS_PENDING;
  }

  // Release the detach spin lock from DPC level
  KeReleaseInStackQueuedSpinLockFromDpcLevel(
    &DetachLockHandle
    );

  // Release the binding context list spin lock
  KeReleaseInStackQueuedSpinLock(
    &BindingContextListLockHandle
    );

  // Return the status of the detachment
  return Status;
}
```

同様に、プロバイダー モジュールは、クライアントが接続されているモジュールの NPI コールバック関数の実行中の呼び出しの数を追跡するため、上記の例でクライアント モジュールとして同じ考え方実装を使用可能性があります。

**注**  上のコード例は、接続されているネットワーク モジュールの NPI 関数の実行中の呼び出しの数を追跡可能な方法の 1 つを示しています。 ネットワーク モジュールは、ネットワークのモジュールがサポートする特定の NPI の実装の詳細によって、別の方法を使用して可能性があります。

 

 

 





