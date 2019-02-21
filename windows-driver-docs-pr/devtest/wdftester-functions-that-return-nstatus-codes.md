---
title: リターン コードの送ら KMDF 関数
description: リターン コードの送ら KMDF 関数
ms.assetid: 0edd35c0-2357-4502-8c59-36b16cf7f294
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: df14fede11fdf33d609439c4479f42dd0eef8b26
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529656"
---
# <a name="kmdf-functions-that-return-nstatus-codes"></a>リターン コードの送ら KMDF 関数


リターン コードの NTSTATUS KMDF Ddi の一覧を次に示します。 次の 2 つを除くこれら Ddi のいずれかが失敗しましたでした。**WdfRequestReuse**と**WdfWaitLockAcquire**します。

**WdfChildListAddOrUpdateChildDescriptionAsPresent**

**WdfChildListCreate**

**WdfChildListRetrieveAddressDescription**

**WdfChildListRetrieveNextDevice**

**WdfChildListUpdateChildDescriptionAsMissing**

**WdfCmResourceListAppendDescriptor**

**WdfCmResourceListInsertDescriptor**

**WdfCollectionAdd**

**WdfCollectionCreate**

**WdfCommonBufferCreate**

**WdfCommonBufferCreateWithConfig**

**WdfDeviceAddDependentUsageDeviceObject**

**WdfDeviceAddQueryInterface**

**WdfDeviceAddRemovalRelationsPhysicalDevice**

**WdfDeviceAllocAndQueryProperty**

**WdfDeviceAssignMofResourceName**

**WdfDeviceAssignS0IdleSettings**

**WdfDeviceAssignSxWakeSettings**

**WdfDeviceConfigureRequestDispatching**

**WdfDeviceCreate**

**WdfDeviceCreateDeviceInterface**

**WdfDeviceCreateSymbolicLink**

**WdfDeviceEnqueueRequest**

**WdfDeviceIndicateWakeStatus**

**WdfDeviceInitAssignName**

**WdfDeviceInitAssignSDDLString**

**WdfDeviceInitAssignWdmIrpPreprocessCallback**

**WdfDeviceInitRegisterPnpStateChangeCallback**

**WdfDeviceInitRegisterPowerPolicyStateChangeCallback**

**WdfDeviceInitRegisterPowerStateChangeCallback**

**WdfDeviceMiniportCreate**

**WdfDeviceOpenRegistryKey**

**WdfDeviceQueryProperty**

**WdfDeviceRetrieveDeviceInterfaceString**

**WdfDeviceRetrieveDeviceName**

**WdfDeviceStopIdle**

**WdfDeviceWdmDispatchPreprocessedIrp**

**WdfDmaEnablerCreate**

**WdfDmaTransactionCreate**

**WdfDmaTransactionExecute**

**WdfDmaTransactionInitialize**

**WdfDmaTransactionInitializeUsingRequest**

**WdfDmaTransactionRelease**

**WdfDpcCreate**

**WdfDriverCreate**

**WdfDriverOpenParametersRegistryKey**

**WdfDriverRegisterTraceInfo**

**WdfDriverRetrieveVersionString**

**WdfFdoAddStaticChild**

**WdfFdoInitAllocAndQueryProperty**

**WdfFdoInitOpenRegistryKey**

**WdfFdoInitQueryProperty**

**WdfFdoQueryForInterface**

**WdfInterruptCreate**

**WdfIoQueueCreate**

**WdfIoQueueFindRequest**

**WdfIoQueueReadyNotify**

**WdfIoQueueRetrieveFoundRequest**

**WdfIoQueueRetrieveNextRequest**

**WdfIoQueueRetrieveRequestByFileObject**

**WdfIoResourceListAppendDescriptor**

**WdfIoResourceListCreate**

**WdfIoResourceListInsertDescriptor**

**WdfIoResourceRequirementsListAppendIoResList**

**WdfIoResourceRequirementsListInsertIoResList**

**WdfIoTargetAllocAndQueryTargetProperty**

**WdfIoTargetCreate**

**WdfIoTargetFormatRequestForInternalIoctl**

**WdfIoTargetFormatRequestForInternalIoctlOthers**

**WdfIoTargetFormatRequestForIoctl**

**WdfIoTargetFormatRequestForRead**

**WdfIoTargetFormatRequestForWrite**

**WdfIoTargetOpen**

**WdfIoTargetQueryForInterface**

**WdfIoTargetQueryTargetProperty**

**WdfIoTargetSendInternalIoctlOthersSynchronously**

**WdfIoTargetSendInternalIoctlSynchronously**

**WdfIoTargetSendIoctlSynchronously**

**WdfIoTargetSendReadSynchronously**

**WdfIoTargetSendWriteSynchronously**

**WdfIoTargetStart**

**WdfLookasideListCreate**

**WdfMemoryAssignBuffer**

**WdfMemoryCopyFromBuffer**

**WdfMemoryCopyToBuffer**

**WdfMemoryCreate**

**WdfMemoryCreateFromLookaside**

**WdfMemoryCreatePreallocated**

**WdfObjectAllocateContext**

**WdfObjectCreate**

**WdfObjectQuery**

**WdfPdoAddEjectionRelationsPhysicalDevice**

**WdfPdoInitAddCompatibleID**

**WdfPdoInitAddDeviceText**

**WdfPdoInitAddHardwareID**

**WdfPdoInitAssignDeviceID**

**WdfPdoInitAssignInstanceID**

**WdfPdoInitAssignRawDevice**

**WdfPdoMarkMissing**

**WdfPdoRetrieveAddressDescription**

**WdfPdoRetrieveIdentificationDescription**

**WdfPdoUpdateAddressDescription**

**WdfRegistryAssignMemory**

**WdfRegistryAssignMultiString**

**WdfRegistryAssignString**

**WdfRegistryAssignULong**

**WdfRegistryAssignUnicodeString**

**WdfRegistryAssignValue**

**WdfRegistryCreateKey**

**WdfRegistryOpenKey**

**WdfRegistryQueryMemory**

**WdfRegistryQueryMultiString**

**WdfRegistryQueryString**

**WdfRegistryQueryULong**

**WdfRegistryQueryUnicodeString**

**WdfRegistryQueryValue**

**WdfRegistryRemoveKey**

**WdfRegistryRemoveValue**

**WdfRequestAllocateTimer**

**WdfRequestChangeTarget**

**WdfRequestCreate**

**WdfRequestCreateFromIrp**

**WdfRequestForwardToIoQueue**

**WdfRequestGetStatus**

**WdfRequestProbeAndLockUserBufferForRead**

**WdfRequestProbeAndLockUserBufferForWrite**

**WdfRequestRequeue**

**WdfRequestRetrieveInputBuffer**

**WdfRequestRetrieveInputMemory**

**WdfRequestRetrieveInputWdmMdl**

**WdfRequestRetrieveOutputBuffer**

**WdfRequestRetrieveOutputMemory**

**WdfRequestRetrieveOutputWdmMdl**

**WdfRequestRetrieveUnsafeUserInputBuffer**

**WdfRequestRetrieveUnsafeUserOutputBuffer**

**WdfRequestReuse**

**WdfRequestUnmarkCancelable**

**WdfSpinLockCreate**

**WdfStringCreate**

**WdfTimerCreate**

**WdfUsbInterfaceSelectSetting**

**WdfUsbTargetDeviceAllocAndQueryString**

**WdfUsbTargetDeviceCreate**

**WdfUsbTargetDeviceCyclePortSynchronously**

**WdfUsbTargetDeviceFormatRequestForControlTransfer**

**WdfUsbTargetDeviceFormatRequestForCyclePort**

**WdfUsbTargetDeviceFormatRequestForString**

**WdfUsbTargetDeviceFormatRequestForUrb**

**WdfUsbTargetDeviceIsConnectedSynchronous**

**WdfUsbTargetDeviceQueryString**

**WdfUsbTargetDeviceResetPortSynchronously**

**WdfUsbTargetDeviceRetrieveConfigDescriptor**

**WdfUsbTargetDeviceRetrieveCurrentFrameNumber**

**WdfUsbTargetDeviceRetrieveInformation**

**WdfUsbTargetDeviceSelectConfig**

**WdfUsbTargetDeviceSendControlTransferSynchronously**

**WdfUsbTargetDeviceSendUrbSynchronously**

**WdfUsbTargetPipeAbortSynchronously**

**WdfUsbTargetPipeConfigContinuousReader**

**WdfUsbTargetPipeFormatRequestForAbort**

**WdfUsbTargetPipeFormatRequestForRead**

**WdfUsbTargetPipeFormatRequestForReset**

**WdfUsbTargetPipeFormatRequestForUrb**

**WdfUsbTargetPipeFormatRequestForWrite**

**WdfUsbTargetPipeReadSynchronously**

**WdfUsbTargetPipeResetSynchronously**

**WdfUsbTargetPipeSendUrbSynchronously**

**WdfUsbTargetPipeWriteSynchronously**

**WdfWaitLockAcquire**

**WdfWaitLockCreate**

**WdfWmiInstanceCreate**

**WdfWmiInstanceFireEvent**

**WdfWmiInstanceRegister**

**WdfWmiProviderCreate**

**WdfWorkItemCreate**

 

 





