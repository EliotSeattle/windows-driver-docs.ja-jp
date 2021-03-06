---
title: OID_WDI_SET_REMOVE_WOL_PATTERN
description: OID_WDI_SET_REMOVE_WOL_PATTERN では、ファームウェアから wake on LAN (WOL) パターンを削除します。
ms.assetid: 9fb03747-b585-4c73-b004-1bdc2a995e9d
ms.date: 07/18/2017
keywords:
- OID_WDI_SET_REMOVE_WOL_PATTERN ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 3ef9b5e0483e081553508bb388f1d664ee8a6eb4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386535"
---
# <a name="oidwdisetremovewolpattern"></a>OID\_WDI\_設定\_削除\_WOL\_パターン


OID\_WDI\_設定\_削除\_WOL\_パターン、ファームウェアから、wake on LAN (WOL) パターンを削除します。

| Scope | タスクでシリアル化された設定します。 | 通常の実行時間 (秒) |
|-------|--------------------------|---------------------------------|
| ポート  | 〇                      | 1                               |

 

## <a name="set-property-parameters"></a>プロパティ パラメーターの設定


| TLV                                                                                        | 許可されている複数の TLV インスタンス | 省略可能 | 説明     |
|--------------------------------------------------------------------------------------------|--------------------------------|----------|-----------------|
| [**WDI\_TLV\_WAKE\_パケット\_パターン\_削除**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-wake-packet-pattern-remove) |                                |          | WOL パターンの id。 |

 

## <a name="set-property-results"></a>セットのプロパティの結果


追加のパラメーターはありません。 ヘッダー内のデータで十分です。

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>サポートされている最小のクライアント</p></td>
<td><p>Windows 10</p></td>
</tr>
<tr class="even">
<td><p>サポートされている最小のサーバー</p></td>
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>Header</p></td>
<td>Dot11wdi.h</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[OID\_WDI\_設定\_追加\_WOL\_パターン](oid-wdi-set-add-wol-pattern.md)

 

 




