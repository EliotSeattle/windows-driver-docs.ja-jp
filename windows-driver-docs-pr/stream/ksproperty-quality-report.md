---
title: KSPROPERTY\_品質\_レポート
description: KSPROPERTY\_品質\_レポート プロパティが省略可能なプロパティ、暗証番号 (pin) は、品質管理をサポートしている場合に実装する必要があります。
ms.assetid: 9879a28d-aa92-4583-be63-03fed67c8416
keywords:
- KSPROPERTY_QUALITY_REPORT ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_QUALITY_REPORT
api_location:
- ks.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6567bf3b9bc5a737f68f64dca0f348b73204f40f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538144"
---
# <a name="kspropertyqualityreport"></a>KSPROPERTY\_品質\_レポート


KSPROPERTY\_品質\_レポート プロパティが省略可能なプロパティ、暗証番号 (pin) は、品質管理をサポートしている場合に実装する必要があります。

## <span id="ddk_ksproperty_quality_report_ks"></span><span id="DDK_KSPROPERTY_QUALITY_REPORT_KS"></span>


### <a name="usage-summary-table"></a>使用状況の概要テーブル

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th>取得</th>
<th>設定</th>
<th>対象</th>
<th>プロパティ記述子の型</th>
<th>プロパティ値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>〇</p></td>
<td><p>〇</p></td>
<td><p>Pin</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566728" data-raw-source="[&lt;strong&gt;KSQUALITY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566728)"><strong>KSQUALITY</strong></a></p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

KSPROPERTY\_品質\_レポートは、型のプロパティの値を持つ[ **KSQUALITY** ](https://msdn.microsoft.com/library/windows/hardware/ff566728)構造体。 取得または現在使用されているフレームの割合と最適なフレームの受信時刻からデルタを設定するには、この構造体を使用します。

クラス ドライバーは、このプロパティを処理しませんストリームのミニドライバーは、独自の処理を提供する必要があります。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Ks.h (Ks.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)

[**KSQUALITY**](https://msdn.microsoft.com/library/windows/hardware/ff566728)

 

 





