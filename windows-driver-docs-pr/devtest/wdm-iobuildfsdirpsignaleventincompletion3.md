---
title: IoBuildFsdIrpSignalEventInCompletion3 ルール (wdm)
description: IoBuildFsdIrpSignalEventInCompletion3 ルールでは、KeSetEvent が Irp-PendingReturned フラグが設定され、完了ルーチンは、ローカルで作成された非同期 IRP の処理時に、完了のルーチンで呼び出される必要があることを指定します。
ms.assetid: 9A9A8169-AEDC-4B13-B407-22F549678526
ms.date: 05/21/2018
keywords:
- IoBuildFsdIrpSignalEventInCompletion3 ルール (wdm)
topic_type:
- apiref
api_name:
- IoBuildFsdIrpSignalEventInCompletion3
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: c7d84cc43d401c6b4d453d0bd3204d780209f141
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571611"
---
# <a name="iobuildfsdirpsignaleventincompletion3-rule-wdm"></a>IoBuildFsdIrpSignalEventInCompletion3 ルール (wdm)


**IoBuildFsdIrpSignalEventInCompletion3**ルールを指定する[ **KeSetEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff553253)完了ルーチンで呼び出される必要があるときに、 **Irp&gt;PendingReturned**フラグが設定され、ローカルで作成された非同期 IRP の処理が完了ルーチン。

ここで完了ルーチンは呼び出されません。

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>IoBuildFsdIrpSignalEventInCompletion3</strong>ルール。</p>
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

[**IoSetCompletionRoutine**](https://msdn.microsoft.com/library/windows/hardware/ff549679)
[**IoSetCompletionRoutineEx**](https://msdn.microsoft.com/library/windows/hardware/ff549686)
[**KeInitializeEvent**](https://msdn.microsoft.com/library/windows/hardware/ff552137)
 

 




