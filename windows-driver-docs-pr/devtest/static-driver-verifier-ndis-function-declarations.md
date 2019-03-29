---
title: 静的ドライバー検証ツールでの NDIS 関数の宣言
description: 静的ドライバー検証ツールでの NDIS 関数の宣言
ms.assetid: f8d11a99-0fd0-45cf-b583-8f8833b21f79
keywords:
- SDV の WDK、NDIS
- SDV NDIS 規則
- SDV の WDK、NDIS ルール
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2ad8b288019c549b109bdcf08bb366421e6a11f7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570480"
---
# <a name="static-driver-verifier-ndis-function-declarations"></a>静的ドライバー検証ツールでの NDIS 関数の宣言


SDV NDIS ドライバーの確認を有効にするには、ロールの種類をコールバック関数を使用して各コールバック関数を宣言する必要があります。 コールバック関数のロールの種類は、Ndis.h のヘッダー ファイルで定義されてし、そのヘッダー ファイルでは、ドライバーをビルドするとが含まれています。

コールバック関数の定義を宣言する前に、ドライバーのコールバック関数を宣言する必要があります。 次のコード例の関数の役割の型宣言を示しています、 [ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389)コールバック関数。 ミニポートを使用して、このコールバック関数を宣言する必要があります\_ロールの種類を初期化します。 この例では、コールバック関数が呼び出されます*myMiniportInitializeEx*します。

```
#include <ndis.h>  
MINIPORT_INITIALIZE myMiniportInitializeEx
```

コールバック関数に関数のプロトタイプ宣言がある場合とロールの種類の関数の宣言、関数プロトタイプを置き換える必要があります。 関数の役割の種類の宣言に関する詳細については、次を参照してください。、[を使用して関数の役割の型の宣言](using-function-role-type-declarations.md)トピック。

次の表は、コールバック関数のロールの種類と関連付けられている NDIS コールバック関数を示します。

### <a name="span-idrequiredfunctiondeclarationsspanspan-idrequiredfunctiondeclarationsspanrequired-function-declarations"></a><span id="required_function_declarations"></span><span id="REQUIRED_FUNCTION_DECLARATIONS"></span>必要な関数の宣言

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">NDIS ミニポート ドライバーのコールバック関数</th>
<th align="left">ロールの種類名</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff559332" data-raw-source="[&lt;em&gt;MiniportAddDevice&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559332)"><em>MiniportAddDevice</em></a></p></td>
<td align="left"><p>MINIPORT_ADD_DEVICE</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff559335" data-raw-source="[&lt;em&gt;MiniportCancelDirectOidRequest&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559335)"><em>MiniportCancelDirectOidRequest</em></a></p></td>
<td align="left"><p>MINIPORT_CANCEL_DIRECT_OID_REQUEST</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff559339" data-raw-source="[&lt;em&gt;MiniportCancelOidRequest&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559339)"><em>MiniportCancelOidRequest</em></a></p></td>
<td align="left"><p>MINIPORT_CANCEL_OID_REQUEST</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff559342" data-raw-source="[&lt;em&gt;MiniportCancelSend&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559342)"><em>MiniportCancelSend</em></a></p></td>
<td align="left"><p>MINIPORT_CANCEL_SEND</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff559346" data-raw-source="[&lt;em&gt;MiniportCheckForHangEx&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559346)"><em>MiniportCheckForHangEx</em></a></p></td>
<td align="left"><p>MINIPORT_CHECK_FOR_HANG</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff559369" data-raw-source="[&lt;em&gt;MiniportDevicePnPEventNotify&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559369)"><em>MiniportDevicePnPEventNotify</em></a></p></td>
<td align="left"><p>MINIPORT_DEVICE_PNP_EVENT_NOTIFY</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff559371" data-raw-source="[&lt;em&gt;MiniportDirectOidRequest&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559371)"><em>MiniportDirectOidRequest</em></a></p></td>
<td align="left"><p>MINIPORT_DIRECT_OID_REQUEST</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff559375" data-raw-source="[&lt;em&gt;MiniportDisableInterruptEx&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559375)"><em>MiniportDisableInterruptEx</em></a></p></td>
<td align="left"><p>MINIPORT_DISABLE_INTERRUPT</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff559376" data-raw-source="[&lt;em&gt;MiniportDisableMessageInterrupt&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559376)"><em>MiniportDisableMessageInterrupt</em></a></p></td>
<td align="left"><p>MINIPORT_DISABLE_MESSAGE_INTERRUPT</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff559378" data-raw-source="[&lt;em&gt;MiniportDriverUnload&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559378)"><em>MiniportDriverUnload</em></a></p></td>
<td align="left"><p>MINIPORT_UNLOAD</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff559380" data-raw-source="[&lt;em&gt;MiniportEnableInterruptEx&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559380)"><em>MiniportEnableInterruptEx</em></a></p></td>
<td align="left"><p>MINIPORT_ENABLE_INTERRUPT</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff559383" data-raw-source="[&lt;em&gt;MiniportEnableMessageInterrupt&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559383)"><em>MiniportEnableMessageInterrupt</em></a></p></td>
<td align="left"><p>MINIPORT_ENABLE_MESSAGE_INTERRUPT</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff559384" data-raw-source="[&lt;em&gt;MiniportFilterResourceRequirements&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559384)"><em>MiniportFilterResourceRequirements</em></a></p></td>
<td align="left"><p>MINIPORT_FILTER_RESOURCE_REQUIREMENTS</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff559388" data-raw-source="[&lt;em&gt;MiniportHaltEx&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559388)"><em>MiniportHaltEx</em></a></p></td>
<td align="left"><p>MINIPORT_HALT</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff559389" data-raw-source="[&lt;em&gt;MiniportInitializeEx&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559389)"><em>MiniportInitializeEx</em></a></p></td>
<td align="left"><p>MINIPORT_INITIALIZE</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff559395" data-raw-source="[&lt;em&gt;MiniportInterrupt&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559395)"><em>MiniportInterrupt</em></a></p></td>
<td align="left"><p>MINIPORT_ISR</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff559398" data-raw-source="[&lt;em&gt;MiniportInterruptDPC&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559398)"><em>MiniportInterruptDPC</em></a></p></td>
<td align="left"><p>MINIPORT_INTERRUPT_DPC</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff559407" data-raw-source="[&lt;em&gt;MiniportMessageInterrupt&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559407)"><em>MiniportMessageInterrupt</em></a></p></td>
<td align="left"><p>MINIPORT_MESSAGE_INTERRUPT</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff559411" data-raw-source="[&lt;em&gt;MiniportMessageInterruptDPC&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559411)"><em>MiniportMessageInterruptDPC</em></a></p></td>
<td align="left"><p>MINIPORT_MESSAGE_INTERRUPT_DPC</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff559416" data-raw-source="[&lt;em&gt;MiniportOidRequest&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559416)"><em>MiniportOidRequest</em></a></p></td>
<td align="left"><p>MINIPORT_OID_REQUEST</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff559418" data-raw-source="[&lt;em&gt;MiniportPause&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559418)"><em>MiniportPause</em></a></p></td>
<td align="left"><p>MINIPORT_PAUSE</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff559420" data-raw-source="[&lt;em&gt;MiniportProcessSGList&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559420)"><em>MiniportProcessSGList</em></a></p></td>
<td align="left"><p>MINIPORT_PROCESS_SG_LIST</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff559427" data-raw-source="[&lt;em&gt;MiniportRemoveDevice&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559427)"><em>MiniportRemoveDevice</em></a></p></td>
<td align="left"><p>MINIPORT_REMOVE_DEVICE</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff559432" data-raw-source="[&lt;em&gt;MiniportResetEx&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559432)"><em>MiniportResetEx</em></a></p></td>
<td align="left"><p>MINIPORT_RESET</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff559435" data-raw-source="[&lt;em&gt;MiniportRestart&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559435)"><em>MiniportRestart</em></a></p></td>
<td align="left"><p>MINIPORT_RESTART</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff559437" data-raw-source="[&lt;em&gt;MiniportReturnNetBufferLists&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559437)"><em>MiniportReturnNetBufferLists</em></a></p></td>
<td align="left"><p>MINIPORT_RETURN_NET_BUFFER_LISTS</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff559440" data-raw-source="[&lt;em&gt;MiniportSendNetBufferLists&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559440)"><em>MiniportSendNetBufferLists</em></a></p></td>
<td align="left"><p>MINIPORT_SEND_NET_BUFFER_LISTS</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff559443" data-raw-source="[&lt;em&gt;MiniportSetOptions&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559443)"><em>MiniportSetOptions</em></a></p></td>
<td align="left"><p>MINIPORT_SET_OPTIONS</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff559446" data-raw-source="[&lt;em&gt;MiniportSharedMemoryAllocateComplete&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559446)"><em>MiniportSharedMemoryAllocateComplete</em></a></p></td>
<td align="left"><p>MINIPORT_ALLOCATE_SHARED_MEM_COMPLETE</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff559449" data-raw-source="[&lt;em&gt;MiniportShutdownEx&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559449)"><em>MiniportShutdownEx</em></a></p></td>
<td align="left"><p>MINIPORT_SHUTDOWN</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff559452" data-raw-source="[&lt;em&gt;MiniportStartDevice&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559452)"><em>MiniportStartDevice</em></a></p></td>
<td align="left"><p>MINIPORT_START_DEVICE</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff559454" data-raw-source="[&lt;em&gt;MiniportSynchronizeInterrupt&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559454)"><em>MiniportSynchronizeInterrupt</em></a></p></td>
<td align="left"><p>MINIPORT_SYNCHRONIZE_INTERRUPT</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff559455" data-raw-source="[&lt;em&gt;MiniportSynchronizeMessageInterrupt&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559455)"><em>MiniportSynchronizeMessageInterrupt</em></a></p></td>
<td align="left"><p>MINIPORT_SYNCHRONIZE_MESSAGE_INTERRUPT</p></td>
</tr>
</tbody>
</table>

 

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">NDIS 他のコールバック関数</th>
<th align="left">ロールの種類名</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>NDIS_IO_WORKITEM_ROUTINE</p>
<p><em>ルーチン</em></p>
<p><em>ルーチン</em>が 2 番目のパラメーターで指定されているコールバック ルーチン、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff563775" data-raw-source="[&lt;strong&gt;NdisQueueIoWorkItem&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff563775)"> <strong>NdisQueueIoWorkItem</strong> </a>関数。</p></td>
<td align="left"><p>NDIS_IO_WORKITEM_FUNCTION</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff568351" data-raw-source="[&lt;em&gt;NetTimerCallback&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff568351)"><em>NetTimerCallback</em></a></p></td>
<td align="left"><p>NDIS_TIMER_FUNCTION</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idrecommendedfunctiondeclarationsspanspan-idrecommendedfunctiondeclarationsspanrecommended-function-declarations"></a><span id="recommended_function_declarations"></span><span id="RECOMMENDED_FUNCTION_DECLARATIONS"></span>関数の宣言をお勧めします。

次の関数の役割種類現在使用されていない SDV ルールで NDIS ドライバー。ただし、これらは可能性があります、将来を使用します。 Windows 7 でこれらの関数の役割の種類がサポートされてし、その特定の機能ロールの種類を使用して、これらのコールバックを宣言することをお勧めします。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">NDIS フィルター ドライバーのコールバック関数</th>
<th align="left">ロールの種類名</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549905" data-raw-source="[&lt;em&gt;FilterAttach&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549905)"><em>FilterAttach</em></a></p></td>
<td align="left"><p>FILTER_ATTACH</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549908" data-raw-source="[&lt;em&gt;FilterCancelDirectOidRequest&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549908)"><em>FilterCancelDirectOidRequest</em></a></p></td>
<td align="left"><p>FILTER_CANCEL_DIRECT_OID_REQUEST</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549915" data-raw-source="[&lt;em&gt;FilterCancelSendNetBufferLists&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549915)"><em>FilterCancelSendNetBufferLists</em></a></p></td>
<td align="left"><p>FILTER_CANCEL_SEND_NET_BUFFER_LISTS</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549911" data-raw-source="[&lt;em&gt;FilterCancelOidRequest&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549911)"><em>FilterCancelOidRequest</em></a></p></td>
<td align="left"><p>FILTER_CANCEL_OID_REQUEST</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549918" data-raw-source="[&lt;em&gt;FilterDetach&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549918)"><em>FilterDetach</em></a></p></td>
<td align="left"><p>FILTER_DETACH</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549926" data-raw-source="[&lt;em&gt;FilterDevicePnPEventNotify&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549926)"><em>FilterDevicePnPEventNotify</em></a></p></td>
<td align="left"><p>FILTER_DEVICE_PNP_EVENT_NOTIFY</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549931" data-raw-source="[&lt;em&gt;FilterDirectOidRequest&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549931)"><em>FilterDirectOidRequest</em></a></p></td>
<td align="left"><p>FILTER_DIRECT_OID_REQUEST</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549933" data-raw-source="[&lt;em&gt;FilterDirectOidRequestComplete&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549933)"><em>FilterDirectOidRequestComplete</em></a></p></td>
<td align="left"><p>FILTER_DIRECT_OID_REQUEST_COMPLETE</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549936" data-raw-source="[&lt;em&gt;FilterDriverUnload&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549936)"><em>FilterDriverUnload</em></a></p></td>
<td align="left"><p>DRIVER_UNLOAD</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549952" data-raw-source="[&lt;em&gt;FilterNetPnPEvent&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549952)"><em>FilterNetPnPEvent</em></a></p></td>
<td align="left"><p>FILTER_NET_PNP_EVENT</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549954" data-raw-source="[&lt;em&gt;FilterOidRequest&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549954)"><em>FilterOidRequest</em></a></p></td>
<td align="left"><p>FILTER_OID_REQUEST</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549956" data-raw-source="[&lt;em&gt;FilterOidRequestComplete&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549956)"><em>FilterOidRequestComplete</em></a></p></td>
<td align="left"><p>FILTER_OID_REQUEST_COMPLETE</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549957" data-raw-source="[&lt;em&gt;FilterPause&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549957)"><em>FilterPause</em></a></p></td>
<td align="left"><p>FILTER_PAUSE</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549960" data-raw-source="[&lt;em&gt;FilterReceiveNetBufferLists&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549960)"><em>FilterReceiveNetBufferLists</em></a></p></td>
<td align="left"><p>FILTER_RECEIVE_NET_BUFFER_LISTS</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549962" data-raw-source="[&lt;em&gt;FilterRestart&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549962)"><em>FilterRestart</em></a></p></td>
<td align="left"><p>FILTER_RESTART</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549964" data-raw-source="[&lt;em&gt;FilterReturnNetBufferLists&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549964)"><em>FilterReturnNetBufferLists</em></a></p></td>
<td align="left"><p>FILTER_RETURN_NET_BUFFER_LISTS</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549966" data-raw-source="[&lt;em&gt;FilterSendNetBufferLists&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549966)"><em>FilterSendNetBufferLists</em></a></p></td>
<td align="left"><p>FILTER_SEND_NET_BUFFER_LISTS</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549967" data-raw-source="[&lt;em&gt;FilterSendNetBufferListsComplete&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549967)"><em>FilterSendNetBufferListsComplete</em></a></p></td>
<td align="left"><p>FILTER_SEND_NET_BUFFER_LISTS_COMPLETE</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549970" data-raw-source="[&lt;em&gt;FilterSetModuleOptions&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549970)"><em>FilterSetModuleOptions</em></a></p></td>
<td align="left"><p>FILTER_SET_MODULE_OPTIONS</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549972" data-raw-source="[&lt;em&gt;FilterSetOptions&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549972)"><em>FilterSetOptions</em></a></p></td>
<td align="left"><p>FILTER_SET_OPTIONS</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549973" data-raw-source="[&lt;em&gt;FilterStatus&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549973)"><em>FilterStatus</em></a></p></td>
<td align="left"><p>FILTER_STATUS</p></td>
</tr>
</tbody>
</table>

 

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">いる CoNDIS ミニポート ドライバーのコールバック関数</th>
<th align="left">ロールの種類名</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff559351" data-raw-source="[&lt;em&gt;MiniportCoActivateVc&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559351)"><em>MiniportCoActivateVc</em></a></p></td>
<td align="left"><p>MINIPORT_CO_ACTIVATE_VC</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff559354" data-raw-source="[&lt;em&gt;MiniportCoCreateVc&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559354)"><em>MiniportCoCreateVc</em></a></p></td>
<td align="left"><p>MINIPORT_CO_CREATE_VC</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff559356" data-raw-source="[&lt;em&gt;MiniportCoDeactivateVc&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559356)"><em>MiniportCoDeactivateVc</em></a></p></td>
<td align="left"><p>MINIPORT_CO_DEACTIVATE_VC</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff559358" data-raw-source="[&lt;em&gt;MiniportCoDeleteVc&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559358)"><em>MiniportCoDeleteVc</em></a></p></td>
<td align="left"><p>MINIPORT_CO_DELETE_VC</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff559362" data-raw-source="[&lt;em&gt;MiniportCoOidRequest&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559362)"><em>MiniportCoOidRequest</em></a></p></td>
<td align="left"><p>MINIPORT_CO_OID_REQUEST</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff559365" data-raw-source="[&lt;em&gt;MiniportCoSendNetBufferLists&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559365)"><em>MiniportCoSendNetBufferLists</em></a></p></td>
<td align="left"><p>MINIPORT_CO_SEND_NET_BUFFER_LISTS</p></td>
</tr>
</tbody>
</table>

 

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">NDIS プロトコル ドライバーのコールバック関数</th>
<th align="left">ロールの種類名</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff570220" data-raw-source="[&lt;em&gt;ProtocolBindAdapterEx&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff570220)"><em>ProtocolBindAdapterEx</em></a></p></td>
<td align="left"><p>PROTOCOL_BIND_ADAPTER_EX</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff570236" data-raw-source="[&lt;em&gt;ProtocolCloseAdapterCompleteEx&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff570236)"><em>ProtocolCloseAdapterCompleteEx</em></a></p></td>
<td align="left"><p>PROTOCOL_CLOSE_ADAPTER_COMPLETE_EX</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff570259" data-raw-source="[&lt;em&gt;ProtocolDirectOidRequestComplete&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff570259)"><em>ProtocolDirectOidRequestComplete</em></a></p></td>
<td align="left"><p>PROTOCOL_DIRECT_OID_REQUEST_COMPLETE</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff570263" data-raw-source="[&lt;em&gt;ProtocolNetPnPEvent&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff570263)"><em>ProtocolNetPnPEvent</em></a></p></td>
<td align="left"><p>PROTOCOL_NET_PNP_EVENT</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff570264" data-raw-source="[&lt;em&gt;ProtocolOidRequestComplete&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff570264)"><em>ProtocolOidRequestComplete</em></a></p></td>
<td align="left"><p>PROTOCOL_OID_REQUEST_COMPLETE</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff570265" data-raw-source="[&lt;em&gt;ProtocolOpenAdapterCompleteEx&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff570265)"><em>ProtocolOpenAdapterCompleteEx</em></a></p></td>
<td align="left"><p>PROTOCOL_OPEN_ADAPTER_COMPLETE_EX</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff570267" data-raw-source="[&lt;em&gt;ProtocolReceiveNetBufferLists&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff570267)"><em>ProtocolReceiveNetBufferLists</em></a></p></td>
<td align="left"><p>PROTOCOL_RECEIVE_NET_BUFFER_LISTS</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff570268" data-raw-source="[&lt;em&gt;ProtocolSendNetBufferListsComplete&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff570268)"><em>ProtocolSendNetBufferListsComplete</em></a></p></td>
<td align="left"><p>PROTOCOL_SEND_NET_BUFFER_LISTS_COMPLETE</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff570269" data-raw-source="[&lt;em&gt;ProtocolSetOptions&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff570269)"><em>ProtocolSetOptions</em></a></p></td>
<td align="left"><p>PROTOCOL_SET_OPTIONS</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff570270" data-raw-source="[&lt;em&gt;ProtocolStatusEx&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff570270)"><em>ProtocolStatusEx</em></a></p></td>
<td align="left"><p>PROTOCOL_STATUS_EX</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff570278" data-raw-source="[&lt;em&gt;ProtocolUnbindAdapterEx&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff570278)"><em>ProtocolUnbindAdapterEx</em></a></p></td>
<td align="left"><p>PROTOCOL_UNBIND_ADAPTER_EX</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff570279" data-raw-source="[&lt;em&gt;ProtocolUninstall&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff570279)"><em>ProtocolUninstall</em></a></p></td>
<td align="left"><p>PROTOCOL_UNINSTALL</p></td>
</tr>
</tbody>
</table>

 

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">NDIS プロトコル CL コールバック関数</th>
<th align="left">ロールの種類名</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff570221" data-raw-source="[&lt;em&gt;ProtocolClAddPartyComplete&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff570221)"><em>ProtocolClAddPartyComplete</em></a></p></td>
<td align="left"><p>PROTOCOL_CL_ADD_PARTY_COMPLETE</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff570223" data-raw-source="[&lt;em&gt;ProtocolClCallConnected&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff570223)"><em>ProtocolClCallConnected</em></a></p></td>
<td align="left"><p>PROTOCOL_CL_CALL_CONNECTED</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff570224" data-raw-source="[&lt;em&gt;ProtocolClCloseAfComplete&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff570224)"><em>ProtocolClCloseAfComplete</em></a></p></td>
<td align="left"><p>PROTOCOL_CL_CLOSE_AF_COMPLETE</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff570225" data-raw-source="[&lt;em&gt;ProtocolClCloseCallComplete&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff570225)"><em>ProtocolClCloseCallComplete</em></a></p></td>
<td align="left"><p>PROTOCOL_CL_CLOSE_CALL_COMPLETE</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff570226" data-raw-source="[&lt;em&gt;ProtocolClDeregisterSapComplete&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff570226)"><em>ProtocolClDeregisterSapComplete</em></a></p></td>
<td align="left"><p>PROTOCOL_CL_DEREGISTER_SAP_COMPLETE</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff570227" data-raw-source="[&lt;em&gt;ProtocolClDropPartyComplete&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff570227)"><em>ProtocolClDropPartyComplete</em></a></p></td>
<td align="left"><p>PROTOCOL_CL_DROP_PARTY_COMPLETE</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff570228" data-raw-source="[&lt;em&gt;ProtocolClIncomingCall&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff570228)"><em>ProtocolClIncomingCall</em></a></p></td>
<td align="left"><p>PROTOCOL_CL_INCOMING_CALL</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff570229" data-raw-source="[&lt;em&gt;ProtocolClIncomingCallQoSChange&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff570229)"><em>ProtocolClIncomingCallQoSChange</em></a></p></td>
<td align="left"><p>PROTOCOL_CL_INCOMING_CALL_QOS_CHANGE</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff570230" data-raw-source="[&lt;em&gt;ProtocolClIncomingCloseCall&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff570230)"><em>ProtocolClIncomingCloseCall</em></a></p></td>
<td align="left"><p>PROTOCOL_CL_INCOMING_CLOSE_CALL</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff570231" data-raw-source="[&lt;em&gt;ProtocolClIncomingDropParty&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff570231)"><em>ProtocolClIncomingDropParty</em></a></p></td>
<td align="left"><p>PROTOCOL_CL_INCOMING_DROP_PARTY</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff570232" data-raw-source="[&lt;em&gt;ProtocolClMakeCallComplete&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff570232)"><em>ProtocolClMakeCallComplete</em></a></p></td>
<td align="left"><p>PROTOCOL_CL_MAKE_CALL_COMPLETE</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff570233" data-raw-source="[&lt;em&gt;ProtocolClModifyCallQoSComplete&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff570233)"><em>ProtocolClModifyCallQoSComplete</em></a></p></td>
<td align="left"><p>PROTOCOL_CL_MODIFY_CALL_QOS_COMPLETE</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff570234" data-raw-source="[&lt;em&gt;ProtocolClNotifyCloseAf&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff570234)"><em>ProtocolClNotifyCloseAf</em></a></p></td>
<td align="left"><p>PROTOCOL_CL_NOTIFY_CLOSE_AF</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff570235" data-raw-source="[&lt;em&gt;ProtocolClOpenAfComplete&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff570235)"><em>ProtocolClOpenAfComplete</em></a></p></td>
<td align="left"><p>PROTOCOL_CL_OPEN_AF_COMPLETE</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff570235" data-raw-source="[&lt;em&gt;ProtocolClOpenAfCompleteEx&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff570235)"><em>ProtocolClOpenAfCompleteEx</em></a></p></td>
<td align="left"><p>PROTOCOL_CL_OPEN_AF_COMPLETE_EX</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff570237" data-raw-source="[&lt;em&gt;ProtocolClRegisterSapComplete&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff570237)"><em>ProtocolClRegisterSapComplete</em></a></p></td>
<td align="left"><p>PROTOCOL_CL_REGISTER_SAP_COMPLETE</p></td>
</tr>
</tbody>
</table>

 

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">いる CoNDIS CM コールバック関数</th>
<th align="left">ロールの種類名</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff570238" data-raw-source="[&lt;em&gt;ProtocolCmActivateVcComplete&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff570238)"><em>ProtocolCmActivateVcComplete</em></a></p></td>
<td align="left"><p>PROTOCOL_CM_ACTIVATE_VC_COMPLETE</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff570239" data-raw-source="[&lt;em&gt;ProtocolCmAddParty&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff570239)"><em>ProtocolCmAddParty</em></a></p></td>
<td align="left"><p>PROTOCOL_CM_ADD_PARTY</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff570240" data-raw-source="[&lt;em&gt;ProtocolCmCloseAf&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff570240)"><em>ProtocolCmCloseAf</em></a></p></td>
<td align="left"><p>PROTOCOL_CM_CLOSE_AF</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff570241" data-raw-source="[&lt;em&gt;ProtocolCmCloseCall&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff570241)"><em>ProtocolCmCloseCall</em></a></p></td>
<td align="left"><p>PROTOCOL_CM_CLOSE_CALL</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff570242" data-raw-source="[&lt;em&gt;ProtocolCmDeactivateVcComplete&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff570242)"><em>ProtocolCmDeactivateVcComplete</em></a></p></td>
<td align="left"><p>PROTOCOL_CM_DEACTIVATE_VC_COMPLETE</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff570243" data-raw-source="[&lt;em&gt;ProtocolCmDeregisterSap&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff570243)"><em>ProtocolCmDeregisterSap</em></a></p></td>
<td align="left"><p>PROTOCOL_CM_DEREGISTER_SAP</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff570244" data-raw-source="[&lt;em&gt;ProtocolCmDropParty&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff570244)"><em>ProtocolCmDropParty</em></a></p></td>
<td align="left"><p>PROTOCOL_CM_DROP_PARTY</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff570245" data-raw-source="[&lt;em&gt;ProtocolCmIncomingCallComplete&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff570245)"><em>ProtocolCmIncomingCallComplete</em></a></p></td>
<td align="left"><p>PROTOCOL_CM_INCOMING_CALL_COMPLETE</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff570246" data-raw-source="[&lt;em&gt;ProtocolCmMakeCall&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff570246)"><em>ProtocolCmMakeCall</em></a></p></td>
<td align="left"><p>PROTOCOL_CM_MAKE_CALL</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff570247" data-raw-source="[&lt;em&gt;ProtocolCmModifyCallQoS&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff570247)"><em>ProtocolCmModifyCallQoS</em></a></p></td>
<td align="left"><p>PROTOCOL_CM_MODIFY_QOS_CALL</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff570248" data-raw-source="[&lt;em&gt;ProtocolCmNotifyCloseAfComplete&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff570248)"><em>ProtocolCmNotifyCloseAfComplete</em></a></p></td>
<td align="left"><p>PROTOCOL_CM_NOTIFY_CLOSE_AF_COMPLETE</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff570249" data-raw-source="[&lt;em&gt;ProtocolCmOpenAf&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff570249)"><em>ProtocolCmOpenAf</em></a></p></td>
<td align="left"><p>PROTOCOL_CM_OPEN_AF</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff570250" data-raw-source="[&lt;em&gt;ProtocolCmRegisterSap&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff570250)"><em>ProtocolCmRegisterSap</em></a></p></td>
<td align="left"><p>PROTOCOL_CM_REG_SAP</p></td>
</tr>
</tbody>
</table>

 

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">いる CoNDIS CO コールバック関数</th>
<th align="left">ロールの種類名</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff570251" data-raw-source="[&lt;em&gt;ProtocolCoAfRegisterNotify&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff570251)"><em>ProtocolCoAfRegisterNotify</em></a></p></td>
<td align="left"><p>PROTCOL_CO_AF_REGISTER_NOTIFY</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff570252" data-raw-source="[&lt;em&gt;ProtocolCoCreateVc&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff570252)"><em>ProtocolCoCreateVc</em></a></p></td>
<td align="left"><p>PROTOCOL_CO_CREATE_VC</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff570253" data-raw-source="[&lt;em&gt;ProtocolCoDeleteVc&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff570253)"><em>ProtocolCoDeleteVc</em></a></p></td>
<td align="left"><p>PROTOCOL_CO_DELETE_VC</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff570255" data-raw-source="[&lt;em&gt;ProtocolCoOidRequest&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff570255)"><em>ProtocolCoOidRequest</em></a></p></td>
<td align="left"><p>PROTOCOL_CO_OID_REQUEST</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff570255" data-raw-source="[&lt;em&gt;ProtocolCoOidRequestComplete&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff570255)"><em>ProtocolCoOidRequestComplete</em></a></p></td>
<td align="left"><p>PROTOCOL_CO_OID_REQUEST_COMPLETE</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff570256" data-raw-source="[&lt;em&gt;ProtocolCoReceiveNetBufferLists&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff570256)"><em>ProtocolCoReceiveNetBufferLists</em></a></p></td>
<td align="left"><p>PROTOCOL_CO_RECEIVE_NET_BUFFER_LISTS</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff570257" data-raw-source="[&lt;em&gt;ProtocolCoSendNetBufferListsComplete&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff570257)"><em>ProtocolCoSendNetBufferListsComplete</em></a></p></td>
<td align="left"><p>PROTOCOL_CO_SEND_NET_BUFFER_LISTS_COMPLETE</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff570258" data-raw-source="[&lt;em&gt;ProtocolCoStatusEx&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff570258)"><em>ProtocolCoStatusEx</em></a></p></td>
<td align="left"><p>PROTOCOL_CO_STATUS_EX</p></td>
</tr>
</tbody>
</table>

 

 

 





