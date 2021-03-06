---
title: バグ チェック 0xAC HAL_MEMORY_ALLOCATION
description: HAL_MEMORY_ALLOCATION のバグ チェックでは、0x000000AC の値を持ちます。 このバグ チェックでは、ハードウェア アブストラクション レイヤー (HAL) が十分なメモリを取得できませんでした。 ことを示します。
ms.assetid: 816e6ab5-ccec-47fb-8618-865cb5bb6cb2
keywords:
- バグ チェック 0xAC HAL_MEMORY_ALLOCATION
- HAL_MEMORY_ALLOCATION
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- HAL_MEMORY_ALLOCATION
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 666c0ea32607dcf7ab6d4576212bb2f828ae9782
ms.sourcegitcommit: d03b44343cd32b3653d0471afcdd3d35cb800c0d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2019
ms.locfileid: "67519036"
---
# <a name="bug-check-0xac-halmemoryallocation"></a>バグ チェック 0xAC:HAL\_メモリ\_割り当て


HAL\_メモリ\_割り当てのバグ チェックが 0x000000AC の値を持ちます。 このバグ チェックでは、ハードウェア アブストラクション レイヤー (HAL) が十分なメモリを取得できませんでした。 ことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://www.windows.com/stopcode)します。


## <a name="halmemoryallocation-parameters"></a>HAL\_メモリ\_割り当てパラメーター


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">パラメーター</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>1</p></td>
<td align="left"><p>アロケーション サイズ</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>ファイル名を含む文字列へのポインター</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>予約済み</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

HAL は、システムの重要な要件を非ページ メモリ プールを取得できませんでした。

これらの重大なメモリ割り当てがシステムの初期化、および、HAL の早い段階で行われた\_メモリ\_割り当てのバグ チェックが予期されていません。 このバグ チェックでは、プールの破損または大規模な消費量などの他のいくつかの重大なエラー可能性を示します。

 

 




