---
title: SerCx2 用のシリアル コントローラー ドライバーの設計
description: シリアル、コント ローラーを管理するには、ハードウェアに固有のタスクを実行し、SerCx2 と通信するシリアル コント ローラー ドライバーを作成します。
ms.assetid: 67045E19-4EE1-4C31-A842-858E9A90233E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: eef691b3537da00079017dc9d5a5db8ab1bbc0e9
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67394136"
---
# <a name="serial-controller-driver-design-for-sercx2"></a>SerCx2 用のシリアル コントローラー ドライバーの設計

シリアル、コント ローラーを管理するには、ハードウェアに固有のタスクを実行し、SerCx2 と通信するシリアル コント ローラー ドライバーを作成します。 Windows 8.1 以降、SerCx2 は、シリアル コント ローラーに共通する処理タスクの多くを処理するシステム提供のコンポーネントです。 これらのタスクでは、タイムアウトを管理して、読み取りの処理を含めるし、シリアル コント ローラーのクライアントから送信された要求を記述します。

## <a name="in-this-section"></a>このセクションの内容

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>トピック</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="features-of-sercx2-based-serial-controller-drivers.md" data-raw-source="[Features of SerCx2-Based Serial Controller Drivers](features-of-sercx2-based-serial-controller-drivers.md)">シリアル コント ローラーの SerCx2 ベースのドライバーの機能</a></p></td>
<td><p>シリアル コント ローラーの SerCx2 ベースのドライバーは、KMDF に汎用ドライバー操作を実行するメソッドとコールバックを使用して、コント ローラーのシリアル ドライバーに固有の操作を実行する SerCx2 と通信する KMDF ドライバーです。</p></td>
</tr>
<tr class="even">
<td><p><a href="sercx2-i-o-transactions.md" data-raw-source="[SerCx2 I/O Transactions](sercx2-i-o-transactions.md)">SerCx2 I/O トランザクション</a></p></td>
<td><p>SerCx2 読み取りの処理を簡略化 (<a href="https://docs.microsoft.com/previous-versions/ff546883(v=vs.85)" data-raw-source="[&lt;strong&gt;IRP_MJ_READ&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff546883(v=vs.85))"><strong>IRP_MJ_READ</strong></a>) と書き込み (<a href="https://docs.microsoft.com/previous-versions/ff546904(v=vs.85)" data-raw-source="[&lt;strong&gt;IRP_MJ_WRITE&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff546904(v=vs.85))"><strong>IRP_MJ_WRITE</strong></a>) シリアル コント ローラーの要求ドライバー。 読み取りまたは書き込み要求に応答して、SerCx2 シリアル コント ローラーのドライバーを 1 つまたは複数の I/O トランザクションを発行します。 ドライバーの観点からは、各トランザクションは、単純、完全な I/O 操作です。</p></td>
</tr>
</tbody>
</table>
