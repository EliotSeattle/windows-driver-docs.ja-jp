---
title: OID_WDI_SET_REMOVE_PM_PROTOCOL_OFFLOAD
description: プロトコルで指定されたプロトコル、オフロード OID_WDI_SET_REMOVE_PM_PROTOCOL_OFFLOAD 削除オフロード id。
ms.assetid: 47850c43-4d10-48f5-b2e9-1f94f23eabf2
ms.date: 07/18/2017
keywords:
- OID_WDI_SET_REMOVE_PM_PROTOCOL_OFFLOAD ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: e9460fcc63c3928d7dea6cf6cb0ee32c59d65162
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56581549"
---
# <a name="oidwdisetremovepmprotocoloffload"></a>OID\_WDI\_設定\_削除\_PM\_プロトコル\_オフロード


OID\_WDI\_設定\_削除\_PM\_プロトコル\_プロトコルによって指定されたプロトコル、オフロード オフロード削除オフロード id。

| Scope | タスクでシリアル化された設定します。 | 通常の実行時間 (秒) |
|-------|--------------------------|---------------------------------|
| ポート  | はい                      | 1                               |

 

## <a name="set-property-parameters"></a>プロパティ パラメーターの設定


| TLV                                                                                        | 許可されている複数の TLV インスタンス | 省略可能 | 説明          |
|--------------------------------------------------------------------------------------------|--------------------------------|----------|----------------------|
| [**WDI\_TLV\_PM\_プロトコル\_オフロード\_削除**](https://msdn.microsoft.com/library/windows/hardware/dn898037) |                                |          | プロトコルのオフロードの id。 |

 

## <a name="set-property-results"></a>セットのプロパティの結果


追加のパラメーターはありません。 ヘッダー内のデータで十分です。
必要条件
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


[OID\_WDI\_取得\_PM\_プロトコル\_オフロード](oid-wdi-get-pm-protocol-offload.md)

[OID\_WDI\_設定\_追加\_PM\_プロトコル\_オフロード](oid-wdi-set-add-pm-protocol-offload.md)

 

 



