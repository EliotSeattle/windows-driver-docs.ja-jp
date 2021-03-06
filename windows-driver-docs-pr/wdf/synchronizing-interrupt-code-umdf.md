---
title: 割り込みコードの同期
description: 割り込みコードの同期
ms.assetid: 5E2D0063-2251-40B3-8982-46001E67EB55
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: da2931c7e1e4756c71adb79e5686980386bd1561
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75210830"
---
# <a name="synchronizing-interrupt-code"></a>割り込みコードの同期


[!include[UMDF 1 Deprecation](../includes/umdf-1-deprecation.md)]

割り込みデータバッファーにアクセスするすべてのドライバーコードは、一度に1つのルーチンのみがデータにアクセスするように同期する必要があります。

割り込みコードを同期するには、手動割り込みロックまたは自動コールバックシリアル化を使用します。

## <a name="manual-interrupt-locking"></a>手動による割り込みロック


UMDF は、 [*OnInterruptIsr*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfinterrupt/nc-wudfinterrupt-wudf_interrupt_isr)、 [*OnInterruptDisable*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfinterrupt/nc-wudfinterrupt-wudf_interrupt_disable)、または[*OnInterruptEnable*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfinterrupt/nc-wudfinterrupt-wudf_interrupt_enable)コールバックを呼び出す前に、割り込みロックを取得します。

ドライバーが割り込みロックを使用してコードを同期する必要がある場合は、 [**Iwdfinterrupt:: AcquireInterruptLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfinterrupt-acquireinterruptlock)と[**Iwdfinterrupt:: ReleaseInterruptLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfinterrupt-releaseinterruptlock)を呼び出します。 たとえば、ドライバーは、これらのメソッドを使用して、 [*OnInterruptWorkItem*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfinterrupt/nc-wudfinterrupt-wudf_interrupt_workitem)コールバックルーチンの割り込みロックを取得し、解放します。 ただし、i/o ディスパッチコールバック ( [**Onread**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iqueuecallbackread-onread)や[**onread**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iqueuecallbackwrite-onwrite)など) では、ドライバーはまず[**Iwdfinterrupt:: TryToAcquireInterruptLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfinterrupt-trytoacquireinterruptlock)を呼び出して、作業項目をキューに含めるか、またはデッドロックの可能性を回避するために同じスレッドで作業するかを決定します。 任意のスレッドコンテキストから**Iwdfinterrupt:: AcquireInterruptLock**を呼び出すことによって発生する可能性のあるデッドロックシナリオの例については、 [**Iwdfinterrupt:: AcquireInterruptLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfinterrupt-acquireinterruptlock)の「解説」を参照してください。

[**Iwdfinterrupt:: TryToAcquireInterruptLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfinterrupt-trytoacquireinterruptlock)が**TRUE**を返した場合、ドライバーは同じスレッドで割り込みロックを取得しました。 この場合、ドライバーは、そのロックを必要とする作業を実行し、 [**ReleaseInterruptLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfinterrupt-releaseinterruptlock)を呼び出します。 **Iwdfinterrupt:: TryToAcquireInterruptLock**が**FALSE**を返す場合、ドライバーは作業項目をキューに置いて、その[*onworkitem*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfworkitem/nc-wudfworkitem-wudf_workitem_function)コールバックで作業を実行します。 この場合、作業項目で自動シリアル化を使用することはできません。

## <a name="using-automatic-serialization"></a>自動シリアル化の使用


UMDF ドライバーは、 *LockType*パラメーターを**WdfDeviceLevel**に設定して[**Iwdfdeviceinitialize:: setlocktype constraint**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdeviceinitialize-setlockingconstraint)を呼び出して、自動コールバック同期を要求できます。

次に、 [**Createinterrupt**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice3-createinterrupt)を呼び出す前に、ドライバーは wudf の自動**シリアル化**メンバー [**\_割り込み\_CONFIG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfinterrupt/ns-wudfinterrupt-_wudf_interrupt_config)構造体を**TRUE**に設定します。

その結果、UMDF は、i/o キュー、要求の取り消し、およびファイルオブジェクトのコールバックルーチンを使用して、ドライバーの[*OnInterruptWorkItem*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfinterrupt/nc-wudfinterrupt-wudf_interrupt_workitem)コールバックをシリアル化します。 このシナリオでは、UMDF は、割り込みごとのオブジェクトロックではなく、コールバックロックを使用します。

 

 





