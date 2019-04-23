---
title: KSPROPERTY\_DIRECTSOUND3DBUFFER\_位置
description: KSPROPERTY\_DIRECTSOUND3DBUFFER\_位置プロパティを 3D サウンド バッファーの位置を指定します。
ms.assetid: 727ffb54-f020-473f-8631-1300da0f312c
keywords:
- KSPROPERTY_DIRECTSOUND3DBUFFER_POSITION オーディオ デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_DIRECTSOUND3DBUFFER_POSITION
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c00382b77930d640cfba27899ab3700c949970f5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56581751"
---
# <a name="kspropertydirectsound3dbufferposition"></a>KSPROPERTY\_DIRECTSOUND3DBUFFER\_位置


KSPROPERTY\_DIRECTSOUND3DBUFFER\_位置プロパティを 3D サウンド バッファーの位置を指定します。

## <span id="ddk_ksproperty_directsound3dbuffer_position_ks"></span><span id="DDK_KSPROPERTY_DIRECTSOUND3DBUFFER_POSITION_KS"></span>


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
<th align="left">Set</th>
<th align="left">移行先</th>
<th align="left">プロパティ記述子の型</th>
<th align="left">プロパティ値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>はい</p></td>
<td align="left"><p>はい</p></td>
<td align="left"><p>Pin</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff537143" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff537143)"><strong>KSNODEPROPERTY</strong></a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff536367" data-raw-source="[&lt;strong&gt;DS3DVECTOR&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff536367)"><strong>DS3DVECTOR</strong></a></p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (データの操作) は、バッファーの位置を示す DS3DVECTOR 型の構造です。 位置ユニットについては、[ **KSPROPERTY\_DIRECTSOUND3DLISTENER\_DISTANCEFACTOR**](ksproperty-directsound3dlistener-distancefactor.md)を参照してください。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSPROPERTY\_DIRECTSOUND3DBUFFER\_位置プロパティ要求がステータスを返します\_を正常に完了したことを示すために成功します。 それ以外の場合、要求は、適切なエラー状態コードを返します。

<a name="remarks"></a>コメント
-------

DirectSound 3D バッファーの位置についての詳細については、Microsoft Windows SDK のドキュメントでは、次を参照してください。

-   **VPosition** DS3DBUFFER 構造体のメンバー。

-   **IDirectSound3DBuffer::GetPosition**と**IDirectSound3DBuffer::SetPosition**メソッド。

<a name="requirements"></a>必要条件
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

[**DS3DVECTOR**](https://msdn.microsoft.com/library/windows/hardware/ff536367)

[**KSPROPERTY\_DIRECTSOUND3DLISTENER\_DISTANCEFACTOR**](ksproperty-directsound3dlistener-distancefactor.md)

 

 





