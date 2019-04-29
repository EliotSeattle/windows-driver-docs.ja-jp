---
title: 最初の画像デコード構成
description: 最初の画像デコード構成
ms.assetid: 5888b2d3-42e8-4145-90f7-025b66a4d6e9
keywords:
- 圧縮の画像セット WDK DirectX VA のデコード
- WDK DirectX VA を設定する画像のデコード
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 66af0e802bfa3ec9248506bd8676692aec3e883a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327919"
---
# <a name="first-picture-decoding-configuration"></a>最初の画像デコード構成


## <span id="ddk_first_picture_decoding_configuration_gg"></span><span id="DDK_FIRST_PICTURE_DECODING_CONFIGURATION_GG"></span>


このセット (このセット内の 2 番目と 3 番目の構成よりも優先構成) の最初の構成の定義は次のとおりです。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Member</th>
<th align="left">値</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>guidConfigBitstreamEncryption</strong></p></td>
<td align="left"><p>DXVA_NoEncrypt</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>guidConfigMBcontrolEncryption</strong></p></td>
<td align="left"><p>DXVA_NoEncrypt</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>guidConfigResidDiffEncryption</strong></p></td>
<td align="left"><p>DXVA_NoEncrypt</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>bConfigBitstreamRaw</strong></p></td>
<td align="left"><p>Zero</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>bConfigMBcontrolRasterOrder</strong></p></td>
<td align="left"><p>1</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>bConfigResidDiffHost</strong></p></td>
<td align="left"><p>1</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>bConfigSpatialResid8</strong></p></td>
<td align="left"><p>Zero</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>bConfigResid8Subtraction</strong></p></td>
<td align="left"><p>Zero</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>bConfigSpatialHost8or9Clipping</strong></p></td>
<td align="left"><p>Zero</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>bConfigSpatialResidInterleaved</strong></p></td>
<td align="left"><p>Zero</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>bConfigIntraResidUnsigned</strong></p></td>
<td align="left"><p>Zero</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>bConfigResidDiffAccelerator</strong></p></td>
<td align="left"><p>Zero</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>bConfigHostInverseScan</strong></p></td>
<td align="left"><p>Zero</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>bConfigSpecificIDCT</strong></p></td>
<td align="left"><p>Zero</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>bConfig4GroupedCoefs</strong></p></td>
<td align="left"><p>Zero</p></td>
</tr>
</tbody>
</table>

 

 

 





