---
title: MarkQueryRelations ルール (wdm)
description: MarkQueryRelations ルールは、ドライバーが IRP\_\_クエリ\_デバイス\_RELATIONS IRP を保留する必要があることを指定します。
ms.assetid: A40EA428-D715-46E6-B11E-2F316647184E
ms.date: 05/21/2018
keywords:
- MarkQueryRelations ルール (wdm)
topic_type:
- apiref
api_name:
- MarkQueryRelations
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: da99cb2c2c629696a8a77914f831c2190c83327b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839897"
---
# <a name="markqueryrelations-rule-wdm"></a>MarkQueryRelations ルール (wdm)


**Markqueryrelations**ルールは、ドライバーが irp\_\_クエリ\_デバイス\_RELATIONS irp を保留する必要があることを指定します。

このルールは、 **RemovalRelations**要求を処理するときに、バスドライバーの FDO および FIDO device オブジェクトにのみ適用されます。

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静的ドライバー検証ツール</a>を実行し、 <strong>markqueryrelations</strong>ルールを指定します。</p>
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

[**IoAcquireRemoveLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioacquireremovelock)
[**Ioallocateirp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocateirp)
[**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)
[**Iogetdeviceインターフェイス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdeviceinterfaces)
[**Ioallocateirp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iomarkirppending)
[**IoRegisterPlugPlayNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioregisterplugplaynotification)
[**ioset補完ルーチン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcompletionroutine)
[**IoSetCompletionRoutineEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcompletionroutineex)
[**pocalldriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-pocalldriver)
 

 





