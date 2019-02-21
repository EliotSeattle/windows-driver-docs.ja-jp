---
title: NDIS 6.20 で古いインターフェイス
description: NDIS 6.20 で古いインターフェイス
ms.assetid: 11c3abd5-651e-4f9c-9f0b-ced6c00947f1
keywords:
- NDIS 6.20 WDK、旧式の NDIS 6.1 インターフェイスします。
- NDIS 6.1 インターフェイス WDK NDIS 6.20 が動作を廃止します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 05ea07ff327bf81f2d8e57bac380008cb680fa6c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551106"
---
# <a name="obsolete-interfaces-in-ndis-620"></a>NDIS 6.20 で古いインターフェイス





NDIS 6.1 アプリケーション インターフェイス要素の一部では、NDIS 6.20 ドライバーを廃止します。

次の表には、NDIS 6.1 インターフェイスの要素とその NDIS 6.20 代替が一覧表示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">古いインターフェイス</th>
<th align="left">代わりに使用します。</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff557067" data-raw-source="[&lt;strong&gt;LOCK_STATE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff557067)"><strong>LOCK_STATE</strong></a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff557070" data-raw-source="[&lt;strong&gt;LOCK_STATE_EX&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff557070)"><strong>LOCK_STATE_EX</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564915" data-raw-source="[&lt;strong&gt;NDIS_CURRENT_PROCESSOR_NUMBER&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564915)"><strong>NDIS_CURRENT_PROCESSOR_NUMBER</strong></a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff561737" data-raw-source="[&lt;strong&gt;NdisCurrentProcessorIndex&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff561737)"><strong>NdisCurrentProcessorIndex</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>NDIS_MAX_PROCESSOR_COUNT</strong>(定数)</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff562689" data-raw-source="[&lt;strong&gt;NdisGroupMaxProcessorCount&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff562689)"><strong>NdisGroupMaxProcessorCount</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567277" data-raw-source="[&lt;strong&gt;NDIS_RW_LOCK&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567277)"><strong>NDIS_RW_LOCK</strong></a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567279" data-raw-source="[&lt;strong&gt;NDIS_RW_LOCK_EX&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567279)"><strong>NDIS_RW_LOCK_EX</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>MAXIMUM_PROCESSORS</strong>(定数)</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff562689" data-raw-source="[&lt;strong&gt;NdisGroupMaxProcessorCount&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff562689)"><strong>NdisGroupMaxProcessorCount</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564579" data-raw-source="[&lt;strong&gt;NdisSystemProcessorCount&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564579)"><strong>NdisSystemProcessorCount</strong></a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff562689" data-raw-source="[&lt;strong&gt;NdisGroupMaxProcessorCount&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff562689)"><strong>NdisGroupMaxProcessorCount</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564577" data-raw-source="[&lt;strong&gt;NdisSystemActiveProcessorCount&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564577)"><strong>NdisSystemActiveProcessorCount</strong></a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff562685" data-raw-source="[&lt;strong&gt;NdisGroupActiveProcessorCount&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff562685)"><strong>NdisGroupActiveProcessorCount</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff562661" data-raw-source="[&lt;strong&gt;NdisGetProcessorInformation&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff562661)"><strong>NdisGetProcessorInformation</strong></a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff562662" data-raw-source="[&lt;strong&gt;NdisGetProcessorInformationEx&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff562662)"><strong>NdisGetProcessorInformationEx</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff563637" data-raw-source="[&lt;strong&gt;NdisMQueueDpc&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff563637)"><strong>NdisMQueueDpc</strong></a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff563640" data-raw-source="[&lt;strong&gt;NdisMQueueDpcEx&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff563640)"><strong>NdisMQueueDpcEx</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>使用しないでください、 <em>TargetProcessors</em> MINIPORT_ISR_HANDLER のパラメーター ( <a href="https://msdn.microsoft.com/library/windows/hardware/ff559395" data-raw-source="[&lt;em&gt;MiniportInterrupt&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559395)"> <em>MiniportInterrupt</em></a>)</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff563640" data-raw-source="[&lt;strong&gt;NdisMQueueDpcEx&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff563640)"><strong>NdisMQueueDpcEx</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>使用しないでください、 <em>TargetProcessors</em> MINIPORT_MSI_ISR_HANDLER のパラメーター ( <a href="https://msdn.microsoft.com/library/windows/hardware/ff559407" data-raw-source="[&lt;em&gt;MiniportMessageInterrupt&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559407)"> <em>MiniportMessageInterrupt</em></a>)</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff563640" data-raw-source="[&lt;strong&gt;NdisMQueueDpcEx&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff563640)"><strong>NdisMQueueDpcEx</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566515" data-raw-source="[&lt;strong&gt;NDIS_NBL_MEDIA_SPECIFIC_INFORMATION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566515)"><strong>NDIS_NBL_MEDIA_SPECIFIC_INFORMATION</strong></a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566518" data-raw-source="[&lt;strong&gt;NDIS_NBL_MEDIA_SPECIFIC_INFORMATION_EX&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566518)"><strong>NDIS_NBL_MEDIA_SPECIFIC_INFORMATION_EX</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569621" data-raw-source="[OID_GEN_PHYSICAL_MEDIUM](https://msdn.microsoft.com/library/windows/hardware/ff569621)">OID_GEN_PHYSICAL_MEDIUM</a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569622" data-raw-source="[OID_GEN_PHYSICAL_MEDIUM_EX](https://msdn.microsoft.com/library/windows/hardware/ff569622)">OID_GEN_PHYSICAL_MEDIUM_EX</a></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569773" data-raw-source="[OID_PNP_ADD_WAKE_UP_PATTERN](https://msdn.microsoft.com/library/windows/hardware/ff569773)">OID_PNP_ADD_WAKE_UP_PATTERN</a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569764" data-raw-source="[OID_PM_ADD_WOL_PATTERN](https://msdn.microsoft.com/library/windows/hardware/ff569764)">OID_PM_ADD_WOL_PATTERN</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569774" data-raw-source="[OID_PNP_CAPABILITIES](https://msdn.microsoft.com/library/windows/hardware/ff569774)">OID_PNP_CAPABILITIES</a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569765" data-raw-source="[OID_PM_CURRENT_CAPABILITIES](https://msdn.microsoft.com/library/windows/hardware/ff569765)">OID_PM_CURRENT_CAPABILITIES</a></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569775" data-raw-source="[OID_PNP_ENABLE_WAKE_UP](https://msdn.microsoft.com/library/windows/hardware/ff569775)">OID_PNP_ENABLE_WAKE_UP</a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569768" data-raw-source="[OID_PM_PARAMETERS](https://msdn.microsoft.com/library/windows/hardware/ff569768)">OID_PM_PARAMETERS</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569779" data-raw-source="[OID_PNP_REMOVE_WAKE_UP_PATTERN](https://msdn.microsoft.com/library/windows/hardware/ff569779)">OID_PNP_REMOVE_WAKE_UP_PATTERN</a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569771" data-raw-source="[OID_PM_REMOVE_WOL_PATTERN](https://msdn.microsoft.com/library/windows/hardware/ff569771)">OID_PM_REMOVE_WOL_PATTERN</a></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569783" data-raw-source="[OID_PNP_WAKE_UP_PATTERN_LIST](https://msdn.microsoft.com/library/windows/hardware/ff569783)">OID_PNP_WAKE_UP_PATTERN_LIST</a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569772" data-raw-source="[OID_PM_WOL_PATTERN_LIST](https://msdn.microsoft.com/library/windows/hardware/ff569772)">OID_PM_WOL_PATTERN_LIST</a></p></td>
</tr>
</tbody>
</table>

 

 

 





