---
title: RemoveLockQueryMnRemove ルール (wdm)
description: IRP の処理時に IoAcquireRemoveLock および IoReleaseRemoveLock への呼び出しが正しく使用 RemoveLockQueryMnRemove ルールを確認します\_MJ\_MinorFunction IRP の PNP\_MN\_クエリ\_削除\_デバイス。
ms.assetid: 593B8305-EA61-4857-9304-A8319A8E0017
ms.date: 05/21/2018
keywords:
- RemoveLockQueryMnRemove ルール (wdm)
topic_type:
- apiref
api_name:
- RemoveLockQueryMnRemove
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f0e9c507402b1933c29edb8f8909f2c7e96bdb17
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573181"
---
# <a name="removelockquerymnremove-rule-wdm"></a>RemoveLockQueryMnRemove ルール (wdm)


**RemoveLockQueryMnRemove**への呼び出し規則を確認します[ **IoAcquireRemoveLock** ](https://msdn.microsoft.com/library/windows/hardware/ff548204)と[ **IoReleaseRemoveLock**](https://msdn.microsoft.com/library/windows/hardware/ff549560)が IRP の処理時に正しく使用\_MJ\_MinorFunction IRP の PNP\_MN\_クエリ\_削除\_デバイス。 ドライバーは IRP が下位のスタックを転送する前に削除ロックを取得する必要があります。

このルールは、FDO および FIDO ドライバーのみに適用されます。

たとえば、フィルター ドライバーの FDO と PDO で構成される PnP ドライバー スタックがあるとします。

PnP マネージャーでは、クエリの削除がスタックを送信します。 アイドル状態のシステムの実行中に、FDO になっています。 FDO 決定電源ダウン削除クエリの状態で d0 IRP を要求します。 D0 IRP が到着すると、前に、PnP マネージャーは、PnP IRP を削除して、フィルター ドライバーが IRP が処理されたことを送信します。 フィルター ドライバーでは、スタックからデタッチされ、その状態をクリーンアップします。 スタックの上部にある、d0 が到着しますが、フィルター ドライバーは送信しません下位のスタックが存在しないコンテキストまたはデータがもはや送信先を判断します。 FDO は d0 IRP IRP がないことが到着するを待つハング状態にします。

**このエラーを回避する**

1.  デバイスは、デバイス スタックからデタッチされる前に[ **IoAcquireRemoveLock** ](https://msdn.microsoft.com/library/windows/hardware/ff548204) IRP の次の種類のスタックを IRP が転送される前に、成功する必要があります。

    -   IRP\_MN\_クエリ\_削除
    -   IRP\_MN\_SUPRISE\_REMOVAL
    -   IRP\_MN\_削除\_デバイス

2.  [**IoReleaseRemoveLockAndWait** ](https://msdn.microsoft.com/library/windows/hardware/ff549567)呼び出す前に呼び出す必要がある[ **IoDetachDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff549087)または[ **IoDeleteDevice**](https://msdn.microsoft.com/library/windows/hardware/ff549083). (これにより、デバイス ドライバーのすべての削除ロックが解放される)。

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>RemoveLockQueryMnRemove</strong>ルール。</p>
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

[**IoAcquireRemoveLock**](https://msdn.microsoft.com/library/windows/hardware/ff548204)
[**保留**](https://msdn.microsoft.com/library/windows/hardware/ff548336)
[**IoReleaseRemoveLock**](https://msdn.microsoft.com/library/windows/hardware/ff549560) 
 [ **PoCallDriver**](https://msdn.microsoft.com/library/windows/hardware/ff559654)
 

 




