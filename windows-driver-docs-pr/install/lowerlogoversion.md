---
title: LowerLogoVersion
description: LowerLogoVersion
ms.assetid: b11b9190-9e3f-473d-b78f-b472601c60e2
keywords:
- LowerLogoVersion
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5537c7a7d02fc02c9ec7dec3f7f24286b6bceb60
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377668"
---
# <a name="lowerlogoversion"></a>LowerLogoVersion


**LowerLogoVersion**は、[デバイス セットアップ クラス プロパティ](https://docs.microsoft.com/previous-versions/ff542239(v=vs.85))次のように、ドライバーの署名のスコアに影響します。

-   Windows が同じである Windows バージョンについては、WHQL 署名が含まれるドライバーに署名のハイスコアを割り当てますかそれより遅い、 **LowerLogoVersion**値。

-   Windows では、[次へ] の最適な署名のスコアを割り当てます、サード パーティによって署名されたドライバーを Authenticode テクノロジの使用の Windows バージョン WHQL シグネチャを持つドライバーによりも前、 **LowerLogoVersion**値。

A **LowerLogoVersion**値では、次の表に記載されている Windows のバージョンを指定する NULL で終わる文字列。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Windows のバージョン</th>
<th align="left">LowerLogoVersion 値</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>Windows 7</p></td>
<td align="left"><p>6.1</p></td>
</tr>
<tr class="even">
<td align="left"><p>Windows Server 2008</p></td>
<td align="left"><p>6.1</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Windows Vista</p></td>
<td align="left"><p>6.0</p></td>
</tr>
<tr class="even">
<td align="left"><p>Windows Server 2003</p></td>
<td align="left"><p>5.2</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Windows XP</p></td>
<td align="left"><p>5.1</p></td>
</tr>
<tr class="even">
<td align="left"><p>Windows 2000</p></td>
<td align="left"><p>5.0</p></td>
</tr>
</tbody>
</table>

 

システムの既定**LowerLogoVersion**システム定義の値[デバイス セットアップ クラス](device-setup-classes.md)「5.1」。 これは、ドライバーを Windows Server 2003 および Windows XP、WHQL 署名を持つのマイクロソフトの Windows Vista と Windows の以降のバージョンで署名されたドライバーとして同じシグネチャ スコアであることを意味します。

ドライバーのランク付けの詳細については、次を参照してください。[どの Windows ランクのドライバー (Windows Vista 以降)](how-setup-ranks-drivers--windows-vista-and-later-.md)します。

 

 





