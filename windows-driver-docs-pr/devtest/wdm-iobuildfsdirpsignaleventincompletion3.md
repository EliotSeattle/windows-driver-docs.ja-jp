---
title: IoBuildFsdIrpSignalEventInCompletion3 ルール (wdm)
description: IoBuildFsdIrpSignalEventInCompletion3 規則は、Irp-PendingReturned れたフラグが設定され、完了ルーチンがローカルに作成された非同期 IRP を処理するときに、完了ルーチンで KeSetEvent を呼び出す必要があることを指定します。
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
ms.openlocfilehash: 4cc1d67b1f4434ae70f2d7b4c5142175837f797a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839952"
---
# <a name="iobuildfsdirpsignaleventincompletion3-rule-wdm"></a>IoBuildFsdIrpSignalEventInCompletion3 ルール (wdm)


**IoBuildFsdIrpSignalEventInCompletion3**ルールでは、 **Irp&gt;pendingreturned**フラグが設定され、完了ルーチンがローカルに作成されたを処理するときに、完了ルーチンで[**KeSetEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesetevent)を呼び出す必要があることを指定します。非同期の IRP。

この場合、完了ルーチンは呼び出されません。

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静的ドライバー検証ツール</a>を実行し、 <strong>IoBuildFsdIrpSignalEventInCompletion3</strong>規則を指定します。</p>
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

[**IosetIoSetCompletionRoutineEx ルーチン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcompletionroutine)
[](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcompletionroutineex)
[**keinitializeevent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keinitializeevent)
 

 





