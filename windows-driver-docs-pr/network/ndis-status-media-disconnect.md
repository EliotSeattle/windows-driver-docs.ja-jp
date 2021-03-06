---
title: NDIS_STATUS_MEDIA_DISCONNECT
description: NDIS_STATUS_MEDIA_DISCONNECT 状態では、接続から切断されたにネットワーク接続の状態が変更されたことを示します。
ms.assetid: 490853ca-c849-4b2b-9639-4be670616101
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_MEDIA_DISCONNECT ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 39889b36bcb6fdd91b61095979f6c6b7cb87c94a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368580"
---
# <a name="ndisstatusmediadisconnect"></a>NDIS\_状態\_メディア\_切断


NDIS\_状態\_メディア\_切断状態では、ネットワーク接続の状態が変更されたことから接続を切断されたことを示します。 たとえば、ネットワーク デバイスでは、(ワイヤレス デバイスの場合) の範囲外であるか、ユーザーがデバイスのネットワーク ケーブルから切り離しために、接続が失われます。

<a name="remarks"></a>注釈
-------

NDIS 変換 NDIS\_状態\_メディア\_切断状態のインジケーターを[ **NDIS\_状態\_リンク\_状態**](ndis-status-link-state.md) NDIS 6.0 のドライバーを後続の状態のインジケーター。

NDIS 5。*x*以前のミニポート ドライバーを示し、 [ **NDIS\_状態\_メディア\_CONNECT** ](ndis-status-media-connect.md)の接続時の状態復元します。

NDIS の詳細については\_状態\_メディア\_切断を参照してください[を示す接続の状態 (NDIS 5.1)](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff546856(v=vs.85))と[802.11 ネットワークのメディアの状態インジケーター](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff549301(v=vs.85)).

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>バージョン</p></td>
<td><p>NDIS 6.0 以降はサポートされていません (を使用して、 <a href="ndis-status-link-state.md" data-raw-source="[&lt;strong&gt;NDIS_STATUS_LINK_STATE&lt;/strong&gt;](ndis-status-link-state.md)"> <strong>NDIS_STATUS_LINK_STATE</strong> </a>代わりに)。 Windows Vista および Windows XP で 5.1 の NDIS ドライバーのみサポートされています。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ndis.h (Ndis.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_状態\_リンク\_状態**](ndis-status-link-state.md)

[**NDIS\_状態\_メディア\_接続**](ndis-status-media-connect.md)

 

 




