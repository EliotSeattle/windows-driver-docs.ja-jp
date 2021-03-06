---
title: NdisAllocateNetBuffer rule (ndis)
description: NdisAllocateNetBuffer 規則は、NdisAllocateNetBuffer と NdisFreeNetBuffer が別の順序で呼び出されることを指定します。 最終的な目標は、MiniportHaltEx が終了したときに、NET\_バッファーのすべてのインスタンスが解放されるようにすることです。
ms.assetid: 218708DA-ADDF-4E59-900A-4F8B5CBF00B7
ms.date: 05/21/2018
keywords:
- NdisAllocateNetBuffer rule (ndis)
topic_type:
- apiref
api_name:
- NdisAllocateNetBuffer
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 25e8fae30125a9771652dd0aae1a339e50681f38
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840095"
---
# <a name="ndisallocatenetbuffer-rule-ndis"></a>NdisAllocateNetBuffer rule (ndis)


**NdisAllocateNetBuffer**規則は、 [**NdisAllocateNetBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocatenetbuffer)と[**NdisFreeNetBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreenetbuffer)が別の順序で呼び出されることを指定します。 最終的な目標は、 [*Miniporthaltex*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt)が終了したときに、 [**NET\_バッファー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)のすべてのインスタンスが解放されるようにすることです。

このルールでは、3つの異なる状態を使用します。 この状態は、 [**NET\_バッファー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)が割り当てられるか解放されると変化します。 [*ミニポート*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt)が終了したときに、 **NET\_バッファー**がまだ割り当てられている場合は、ルールによって問題が報告されます。

|              |      |
|--------------|------|
| ドライバー モデル | NDIS |

<a name="how-to-test"></a>テスト方法
-----------

<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">コンパイル時</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静的ドライバー検証ツール</a>を実行し、 <strong>NdisAllocateNetBuffer</strong>規則を指定します。</p>
コードの分析を実行するには、次の手順に従います。
<ol>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code)">コードを準備します (ロールの種類の宣言を使用します)。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier)">静的ドライバー検証ツールを実行します。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results)">結果を表示して分析します。</a></li>
</ol>
<p>詳細については、「 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers)">Static Driver Verifier を使用したドライバーの欠陥の検出</a>」を参照してください。</p></td>
</tr>
</tbody>
</table>

<a name="applies-to"></a>適用対象
----------

[**NdisAllocateNetBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocatenetbuffer)
[ **NdisFreeNetBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreenetbuffer)
 

 





