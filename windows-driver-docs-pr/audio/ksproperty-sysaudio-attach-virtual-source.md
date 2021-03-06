---
title: KSK プロパティ\_SYSAUDIO\_接続\_仮想\_ソース
description: KSK プロパティ\_SYSAUDIO\_ATTACH\_VIRTUAL\_SOURCE プロパティは、仮想ソースを仮想オーディオデバイス上のピンインスタンスにアタッチします。
ms.assetid: cb677eb2-b58d-4f36-b729-d0bfc06db07f
keywords:
- KSPROPERTY_SYSAUDIO_ATTACH_VIRTUAL_SOURCE オーディオデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_SYSAUDIO_ATTACH_VIRTUAL_SOURCE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 62b31f27cf0f103d7d126a64542731618e99afb4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72830531"
---
# <a name="ksproperty_sysaudio_attach_virtual_source"></a>KSK プロパティ\_SYSAUDIO\_接続\_仮想\_ソース


KSK プロパティ\_SYSAUDIO\_ATTACH\_VIRTUAL\_SOURCE プロパティは、仮想ソースを仮想オーディオデバイス上のピンインスタンスにアタッチします。

## <span id="ddk_ksproperty_sysaudio_attach_virtual_source_ks"></span><span id="DDK_KSPROPERTY_SYSAUDIO_ATTACH_VIRTUAL_SOURCE_KS"></span>


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
<td align="left"><p>[はい]</p></td>
<td align="left"><p>[はい]</p></td>
<td align="left"><p>Pin</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-sysaudio_attach_virtual_source" data-raw-source="[&lt;strong&gt;SYSAUDIO_ATTACH_VIRTUAL_SOURCE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-sysaudio_attach_virtual_source)"><strong>SYSAUDIO_ATTACH_VIRTUAL_SOURCE</strong></a></p></td>
<td align="left"><p>なし</p></td>
</tr>
</tbody>
</table>

 

プロパティ記述子 (インスタンスデータ) は、SYSAUDIO\_型の構造であり、プロパティと仮想ソースインデックスを指定する\_仮想\_ソースをアタッチします。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSK プロパティ\_SYSAUDIO\_アタッチ\_仮想\_ソースプロパティ要求は、正常に完了したことを示すステータス\_成功を返します。 それ以外の場合、要求は適切なエラー状態コードを返します。

<a name="remarks"></a>注釈
-------

このプロパティは、仮想ソースを仮想オーディオデバイス上の pin インスタンスに接続します。 詳細については、「 [**Ksk プロパティ\_SYSAUDIO\_作成し\_仮想\_ソースを作成する**](ksproperty-sysaudio-create-virtual-source.md)」を参照してください。

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


[**SYSAUDIO\_\_仮想\_ソースにアタッチする**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-sysaudio_attach_virtual_source)

[**KSK プロパティ\_SYSAUDIO\_作成\_仮想\_ソース**](ksproperty-sysaudio-create-virtual-source.md)

 

 






