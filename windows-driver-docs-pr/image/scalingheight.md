---
title: ScalingHeight 要素
description: 必要な ScalingHeight 要素には、ドキュメントの低速スキャン方向にスケーリングを指定します。
ms.assetid: 29dcaab0-d32b-4aa0-ba27-3da0c9c39f97
keywords:
- ScalingHeight 要素イメージング デバイス
topic_type:
- apiref
api_name:
- wscn ScalingHeight wscn Override "" wscn UsedDefault ""
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: e33ea0dcd0bbbc74635ecec5d54575d3c2355336
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63364399"
---
# <a name="scalingheight-element"></a>ScalingHeight 要素


必要な**ScalingHeight**要素が低速スキャン方向にスケーリングするドキュメントを指定します。

<a name="usage"></a>使用方法
-----

```xml
<wscn:ScalingHeight wscn:Override=""                    wscn:UsedDefault=""
  Override = "xs:string"
  UsedDefault = "xs:string">
  text
</wscn:ScalingHeight wscn:Override=""                    wscn:UsedDefault="">
```

<a name="attributes"></a>属性
----------

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th>属性</th>
<th>種類</th>
<th>必須</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong><strong>上書き</strong></strong></p></td>
<td><p>xs:string</p></td>
<td><p>X</p></td>
<td><p></p>
<p>(省略可能)。 ブール値 false、0 にする必要がある、1 または true です。<strong>falsetrue</strong></p></td>
</tr>
<tr class="even">
<td><p><strong><strong>UsedDefault</strong></strong></p></td>
<td><p>xs:string</p></td>
<td><p>X</p></td>
<td><p></p>
<p>(省略可能)。 ブール値 false、0 にする必要がある、1 または true です。<strong>falsetrue</strong></p></td>
</tr>
</tbody>
</table>

<a name="text-value"></a>テキスト値
----------

必須。 1 ~ 1000、包括的な範囲の整数。

## <a name="child-elements"></a>子要素


子要素はありません。

## <a name="parent-elements"></a>親要素


<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th>要素</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="scaling.md" data-raw-source="[&lt;strong&gt;Scaling&lt;/strong&gt;](scaling.md)"><strong>スケーリング</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>注釈
-------

**ScalingHeight**要素が低速スキャン方向で適用するスケール ファクターを指定します。 スケーリングは、値が 100 の幅を 100% スケール (ドキュメントの高さに調整なし) と示されている 1% 単位で表されます。

すべての WSD スキャン サービスは、少なくとも値 100 をサポートする必要があります。

WSD スキャン サービスを指定できます、省略可能な**オーバーライド**と**UsedDefault**属性の場合にのみ、 **ScalingHeight**要素に含まれる、 **DocumentFinalParameters**階層。 詳細については**オーバーライド**と**UsedDefault**とその用途を参照してください[ **DocumentFinalParameters**](documentfinalparameters.md)します。

この要素に使用できる値をサブセットすることができます。

## <a name="see-also"></a>関連項目


[**DocumentFinalParameters**](documentfinalparameters.md)

[**スケーリング**](scaling.md)

[**ScalingWidth**](scalingwidth.md)

 

 






