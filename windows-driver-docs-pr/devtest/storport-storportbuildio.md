---
title: StorPortBuildIo ルール (storport)
description: このルールは、StorPort ミニポートの StorPortBuildIo ルーチンから FALSE が返された場合に、該当する SRB が StartIo に渡されないことを確認します。
ms.assetid: C35954F9-9C59-408B-BF80-2B8DCD328F9C
ms.date: 05/21/2018
keywords:
- StorPortBuildIo ルール (storport)
topic_type:
- apiref
api_name:
- StorPortBuildIo
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 1be7a86ba7c6020e0a4a19322abf66e9cd450ed3
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840024"
---
# <a name="storportbuildio-rule-storport"></a>StorPortBuildIo ルール (storport)


このルールは、StorPort ミニポートの**StorPortBuildIo**ルーチンから**FALSE**が返された場合に、該当する SRB が**StartIo**に渡されないことを確認します。 (このような場合、ミニポートドライバーは、 **StorPortBuildIo**または他の場所からの**requestcomplete**の通知の種類で[**storportnotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportnotification)を呼び出すことによって、SRB を完了する必要があります)。

> [!NOTE]
> このルールは、ポートミニポートではなく、StorPort の正しい操作をテストしています。

 

|              |          |
|--------------|----------|
| ドライバーモデル | Storport |

<a name="how-to-test"></a>テストする方法
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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静的ドライバー検証ツール</a>を実行し、 <strong>StorPortBuildIo</strong>規則を指定します。</p>
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

 

 





