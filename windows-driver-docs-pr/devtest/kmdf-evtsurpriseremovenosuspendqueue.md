---
title: EvtSurpriseRemoveNoSuspendQueue ルール (kmdf)
description: EvtSurpriseRemoveNoSuspendQueue ルールでは、代わりに、自己管理型の I/O のコールバック関数を使用すること、ドレイン、停止、または EvtDeviceSurpriseRemoval コールバック関数から、キューを削除しないでください WDF のドライバーを指定します。
ms.assetid: A22CC69F-AC48-4E2A-BE7E-9272810CB171
ms.date: 05/21/2018
keywords:
- EvtSurpriseRemoveNoSuspendQueue ルール (kmdf)
topic_type:
- apiref
api_name:
- EvtSurpriseRemoveNoSuspendQueue
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 66bccf10b5f5e923d7e90f6952ee1001c7ad8a61
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573799"
---
# <a name="evtsurpriseremovenosuspendqueue-rule-kmdf"></a>EvtSurpriseRemoveNoSuspendQueue ルール (kmdf)


**EvtSurpriseRemoveNoSuspendQueue**ルールは、WDF ドライバーの電源べきではないドレインいること、停止、または、キューから削除するを指定します[ *EvtDeviceSurpriseRemoval* ](https://msdn.microsoft.com/library/windows/hardware/ff540913)コールバック。関数を代わりに、自己管理型の I/O のコールバック関数を使用する必要があります。 *EvtDeviceSurpriseRemoval*コールバック関数は、電源のパスと同期されていません。

|              |      |
|--------------|------|
| ドライバー モデル | KMDF |

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>EvtSurpriseRemoveNoSuspendQueue</strong>ルール。</p>
コードの分析を実行するには、次の手順に従います。
<ol>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh454281#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](https://msdn.microsoft.com/library/windows/hardware/hh454281#preparing-your-source-code)">(ロールの型宣言の使用)、コードを準備します。</a></li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh454281#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](https://msdn.microsoft.com/library/windows/hardware/hh454281#running-static-driver-verifier)">Static Driver Verifier を実行します。</a></li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh454281#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](https://msdn.microsoft.com/library/windows/hardware/hh454281#viewing-and-analyzing-the-results)">表示し、結果を分析します。</a></li>
</ol>
<p>詳細については、<a href="https://msdn.microsoft.com/library/windows/hardware/hh454281" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](https://msdn.microsoft.com/library/windows/hardware/hh454281)">ドライバーで障害を検出する Static Driver Verifier を使用して</a>を参照してください。</p></td>
</tr>
</tbody>
</table>

<a name="applies-to"></a>対象
----------

[**WdfIoQueueDrain**](https://msdn.microsoft.com/library/windows/hardware/ff547406)
[**WdfIoQueueDrainSynchronously**](https://msdn.microsoft.com/library/windows/hardware/ff547412)
[**WdfIoQueuePurge** ](https://msdn.microsoft.com/library/windows/hardware/ff548442) 
 [ **WdfIoQueuePurgeSynchronously**](https://msdn.microsoft.com/library/windows/hardware/ff548449)
[**WdfIoQueueStop** ](https://msdn.microsoft.com/library/windows/hardware/ff548482)
 [ **WdfIoQueueStopAndPurge**](https://msdn.microsoft.com/library/windows/hardware/hh439289)
[**WdfIoQueueStopAndPurgeSynchronously** ](https://msdn.microsoft.com/library/windows/hardware/hh439293) 
 [ **WdfIoQueueStopSynchronously**](https://msdn.microsoft.com/library/windows/hardware/ff548489)
 

 




