---
title: KSK プロパティ\_BDA\_ノード\_プロパティ
description: クライアントは、KSK プロパティ\_BDA\_NODE\_プロパティを使用して、ノードでサポートされるプロパティの一覧を取得します。
ms.assetid: 36d37844-a69b-4f67-bb8f-e5445ba9a2cb
keywords:
- KSPROPERTY_BDA_NODE_PROPERTIES ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_BDA_NODE_PROPERTIES
api_location:
- Bdamedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: bf66aff787a4952b0704a8fa999a687da3c0e2d0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844345"
---
# <a name="ksproperty_bda_node_properties"></a>KSK プロパティ\_BDA\_ノード\_プロパティ


クライアントは、KSK プロパティ\_BDA\_NODE\_プロパティを使用して、ノードでサポートされるプロパティの一覧を取得します。

## <span id="ddk_ksproperty_bda_node_properties_ks"></span><span id="DDK_KSPROPERTY_BDA_NODE_PROPERTIES_KS"></span>


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
<th>[購入]</th>
<th>設定</th>
<th>対象</th>
<th>プロパティ記述子の型</th>
<th>プロパティ値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>[はい]</p></td>
<td><p>必須ではない</p></td>
<td><p>フィルター</p></td>
<td><p>KSPROPERTY</p></td>
<td><p>Guid の一覧</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

ノードでサポートされるプロパティの一覧は、Guid の一覧です。

ネットワークプロバイダーは、このプロパティを使用して、BDA テンプレート接続リスト内の各ノードの機能を照会します。

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
<td>Bdamedia (Bdamedia を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**BdaPropertyNodeProperties**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bdasup/nf-bdasup-bdapropertynodeproperties)

[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)

 

 






