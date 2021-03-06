---
title: KSK プロパティ\_HRTF3D\_INITIALIZE
description: KSK プロパティ\_HRTF3D\_INITIALIZE プロパティは、HRTF アルゴリズムの初期化に使用するパラメーター値を指定します。
ms.assetid: 45c6c80a-caea-4fb2-a8c8-f64130c0f837
keywords:
- KSPROPERTY_HRTF3D_INITIALIZE オーディオデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_HRTF3D_INITIALIZE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3d6f102f66975145ace1d728a3ab3e1c730a424d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72832752"
---
# <a name="ksproperty_hrtf3d_initialize"></a>KSK プロパティ\_HRTF3D\_INITIALIZE


KSK プロパティ\_HRTF3D\_INITIALIZE プロパティは、HRTF アルゴリズムの初期化に使用するパラメーター値を指定します。

## <span id="ddk_ksproperty_hrtf3d_initialize_ks"></span><span id="DDK_KSPROPERTY_HRTF3D_INITIALIZE_KS"></span>


### <a name="span-idusage_summary_tablespanspan-idusage_summary_tablespanspan-idusage_summary_tablespanusage-summary-table"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用状況の概要テーブル

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
<th align="left">[購入]</th>
<th align="left">設定</th>
<th align="left">対象</th>
<th align="left">プロパティ記述子の型</th>
<th align="left">プロパティ値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>必須ではない</p></td>
<td align="left"><p>[はい]</p></td>
<td align="left"><p>Pin</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty)"><strong>KSNODEPROPERTY</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksds3d_hrtf_init_msg" data-raw-source="[&lt;strong&gt;KSDS3D_HRTF_INIT_MSG&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksds3d_hrtf_init_msg)"><strong>KSDS3D_HRTF_INIT_MSG</strong></a></p></td>
</tr>
</tbody>
</table>

 

プロパティ値 (操作データ) は、初期化値を指定する KSDS3D\_HRTF\_INIT\_MSG 型の構造体です。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSK プロパティ\_HRTF3D\_INITIALIZE プロパティ要求は正常に完了したことを示すステータス\_成功を返します。 それ以外の場合、要求は適切なエラー状態コードを返します。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">Ksmedia .h (Ksk を含む)</td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[**KSNODEPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty)

[**KSDS3D\_HRTF\_INIT\_MSG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksds3d_hrtf_init_msg)

 

 






