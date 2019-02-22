---
title: KSPROPERTY\_オーディオ\_サンプリング\_率
description: KSPROPERTY\_オーディオ\_サンプリング\_レート プロパティは、位置のノードは、出力ストリームを生成するために、入力ストリームをサンプル レートを指定します。
ms.assetid: c5e48678-3b9a-4e5b-ae7b-16f9dcae7492
keywords:
- KSPROPERTY_AUDIO_SAMPLING_RATE オーディオ デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIO_SAMPLING_RATE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: e7e2412d10b8782d9eabc1c550e95b62b5e24f16
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558603"
---
# <a name="kspropertyaudiosamplingrate"></a>KSPROPERTY\_オーディオ\_サンプリング\_率


KSPROPERTY\_オーディオ\_サンプリング\_レート プロパティは、位置のノードは、出力ストリームを生成するために、入力ストリームをサンプル レートを指定します。

## <span id="ddk_ksproperty_audio_sampling_rate_ks"></span><span id="DDK_KSPROPERTY_AUDIO_SAMPLING_RATE_KS"></span>


### <a name="span-idusagesummarytablespanspan-idusagesummarytablespanspan-idusagesummarytablespanusage-summary-table"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用状況の概要テーブル

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
<th align="left">取得</th>
<th align="left">設定</th>
<th align="left">対象</th>
<th align="left">プロパティ記述子の型</th>
<th align="left">プロパティ値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>〇</p></td>
<td align="left"><p>〇</p></td>
<td align="left"><p>Pin</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff537143" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff537143)"><strong>KSNODEPROPERTY</strong></a></p></td>
<td align="left"><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (データの操作) は ULONG 型で、サンプリング レートを指定します。 このレートは 1 秒あたりのサンプルの数として表されます (Hz のサンプリング頻度)。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSPROPERTY\_オーディオ\_サンプリング\_レート プロパティ要求がステータスを返します\_を正常に完了したことを示すために成功します。 それ以外の場合、要求は、適切なエラー状態コードを返します。

<a name="remarks"></a>注釈
-------

ミニポート ドライバーは、ノードが指定したサンプリング レートをサポートしていない場合、プロパティの設定要求のエラーを返す必要があります。

このプロパティは、次のノード タイプのサンプリング レートを制御するために使用されます。

-   ADC ノード ([**KSNODETYPE\_ADC**](ksnodetype-adc.md))

-   DAC のノード ([**KSNODETYPE\_DAC**](ksnodetype-dac.md))

-   SRC ノード ([**KSNODETYPE\_SRC**](ksnodetype-src.md))

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
<td align="left">Ksmedia.h (Ksmedia.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[**KSNODEPROPERTY**](https://msdn.microsoft.com/library/windows/hardware/ff537143)

[**KSNODETYPE\_ADC**](ksnodetype-adc.md)

[**KSNODETYPE\_DAC**](ksnodetype-dac.md)

[**KSNODETYPE\_SRC**](ksnodetype-src.md)

 

 






