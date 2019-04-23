---
title: StartIoRecursion ルール (wdm)
description: StartIoRecursion ルールでは、ドライバーの StartIo ルーチンには、いますへの呼び出しが含まれている場合、ドライバーは DeferredStartIo 属性が TRUE に設定された IoSetStartIoAttributes を最初に呼び出す必要がありますを指定します。 それ以外の場合、無限再帰が発生することができます。
ms.assetid: 997df0a3-1222-435d-9c61-e97a2b6185cf
ms.date: 05/21/2018
keywords:
- StartIoRecursion ルール (wdm)
topic_type:
- apiref
api_name:
- StartIoRecursion
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: d00706359c261c277cf26c4326bd45d7d2e19df5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578813"
---
# <a name="startiorecursion-rule-wdm"></a>StartIoRecursion ルール (wdm)


**StartIoRecursion**規則で指定された場合、ドライバーの[ **StartIo** ](https://msdn.microsoft.com/library/windows/hardware/ff563858)ルーチンにはへの呼び出しが含まれています[**います** ](https://msdn.microsoft.com/library/windows/hardware/ff550358)、ドライバーは呼び出す必要がありますまず[ **IoSetStartIoAttributes** ](https://msdn.microsoft.com/library/windows/hardware/ff550330)で、 *DeferredStartIo*属性に設定**TRUE**します。 それ以外の場合、無限再帰が発生することができます。

|              |     |
|--------------|-----|
| ドライバー モデル | WDM |

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>StartIoRecursion</strong>ルール。</p>
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

[**IoSetStartIoAttributes**](https://msdn.microsoft.com/library/windows/hardware/ff550330)
[**います**](https://msdn.microsoft.com/library/windows/hardware/ff550358)
 

 




