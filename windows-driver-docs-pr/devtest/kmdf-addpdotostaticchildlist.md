---
title: AddPdotoStaticChildlist ルール (kmdf)
description: AddPdotoStaticChildlist ルール PDO デバイスの場合、framework 関数 WdfFdoAddStaticChild する必要があります呼び出すように指定 WdfPdoInitAllocate と WdfDeviceCreate を正常に呼び出して、ドライバーから。
ms.assetid: 31ECB3D2-1EAC-484A-8C3A-DF94AC473334
ms.date: 05/21/2018
keywords:
- AddPdotoStaticChildlist ルール (kmdf)
topic_type:
- apiref
api_name:
- AddPdotoStaticChildlist
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f233826984e174d3b7222d2ff1c6d8ef921a5e64
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56579566"
---
# <a name="addpdotostaticchildlist-rule-kmdf"></a>AddPdotoStaticChildlist ルール (kmdf)


PDO デバイスの場合、framework 関数 AddPdotoStaticChildlist ルールを指定する[ **WdfFdoAddStaticChild** ](https://msdn.microsoft.com/library/windows/hardware/ff547225)ドライバー呼び出しの後に呼び出す必要がある[ **WdfPdoInitAllocate** ](https://msdn.microsoft.com/library/windows/hardware/ff548786)と[ **WdfDeviceCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff545926)正常にします。

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>AddPdotoStaticChildlist</strong>ルール。</p>
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

[**WdfDeviceCreate**](https://msdn.microsoft.com/library/windows/hardware/ff545926)
[**WdfFdoAddStaticChild**](https://msdn.microsoft.com/library/windows/hardware/ff547225)
[**WdfObjectDelete**](https://msdn.microsoft.com/library/windows/hardware/ff548734)
[**WdfPdoInitAllocate**](https://msdn.microsoft.com/library/windows/hardware/ff548786)
 

 




