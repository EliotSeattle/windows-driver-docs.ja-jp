---
title: GuardedRegions ルール (wdm)
description: GuardedRegions ルールは、KeEnterGuardedRegion と KeLeaveGuardedRegion の呼び出しが厳密な代替で使用されることを確認します。
ms.assetid: CF98BF68-905C-48D2-AE72-08DD5559AA0D
ms.date: 05/21/2018
keywords:
- GuardedRegions ルール (wdm)
topic_type:
- apiref
api_name:
- GuardedRegions
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: eca5f9312452564fab1066ef0684a94eddcfe2d1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839231"
---
# <a name="guardedregions-rule-wdm"></a>GuardedRegions ルール (wdm)


**GuardedRegions**ルールは、 [**KeEnterGuardedRegion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-keenterguardedregion)と[**KeLeaveGuardedRegion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-keleaveguardedregion)の呼び出しが厳密な代替で使用されることを確認します。

[**KeEnterGuardedRegion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-keenterguardedregion)を呼び出すたびに、 [**KeLeaveGuardedRegion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-keleaveguardedregion)への呼び出しが一致している必要があります。

|              |     |
|--------------|-----|
| ドライバー モデル | WDM |

|                                   |                                                                                                                                       |
|-----------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|
| この規則で見つかったバグ チェック | [**バグチェック 0xC4: ドライバー\_VERIFIER\_検出された\_違反**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation)(0x0004000e) |

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静的ドライバー検証ツール</a>を実行し、 <strong>GuardedRegions</strong>規則を指定します。</p>
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

<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">実行時</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier" data-raw-source="[Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)">ドライバーの検証ツール</a>を実行し、[ <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/ddi-compliance-checking" data-raw-source="[DDI compliance checking](https://docs.microsoft.com/windows-hardware/drivers/devtest/ddi-compliance-checking)">DDI 準拠チェック</a>] オプションを選択します。</p></td>
</tr>
</tbody>
</table>

 

<a name="applies-to"></a>適用対象
----------

[**KeEnterGuardedRegion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-keenterguardedregion)
[**KeLeaveGuardedRegion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-keleaveguardedregion)関連項目
--------

[重要なリージョンと保護されたリージョン](https://docs.microsoft.com/windows-hardware/drivers/kernel/critical-regions-and-guarded-regions)
 

 





