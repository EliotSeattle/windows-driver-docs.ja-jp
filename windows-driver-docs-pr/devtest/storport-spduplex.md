---
title: SpDuplex ルール (storport)
description: このルールは、このミニポートが全二重モードであるかを確認します。 すべてのドライバー、StorPort ミニポート モデルに基づいて構築されていますが、全二重モードでなければなりません。 半二重モードは、StorPort を既存の SCSI ドライバーを移植するときにのみ使用する必要があります。
ms.assetid: 07B331B4-F0D6-48C4-BEEC-166D43F60E41
ms.date: 05/21/2018
keywords:
- SpDuplex ルール (storport)
topic_type:
- apiref
api_name:
- SpDuplex
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 28151d886ce1d325560bc55b15bf253bc6048233
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574243"
---
# <a name="spduplex-rule-storport"></a>SpDuplex ルール (storport)


このルールは、このミニポートことを確認します。**全二重**モード。 すべてのドライバー、StorPort ミニポート モデルに基づいて構築されていますがである必要があります**全二重**モード。 **半二重**StorPort を既存の SCSI ドライバーを移植するときにのみ使用する必要があります。

|              |          |
|--------------|----------|
| ドライバー モデル | Storport |

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>SpDuplex</strong>ルール。</p>
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

 

 




