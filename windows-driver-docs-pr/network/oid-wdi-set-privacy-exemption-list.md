---
title: OID_WDI_SET_PRIVACY_EXEMPTION_LIST
description: OID_WDI_SET_PRIVACY_EXEMPTION_LIST は、パケットの説明の除外対象の一覧を提供する、ホストによって使用されます。 アダプターでは、除外対象に指定された IEEE EtherType 値に一致するパケットを受信するこれらの例外が適用されます。
ms.assetid: 409ac8c5-0bf7-4ae9-b709-5c2cfa1f8b7f
ms.date: 07/18/2017
keywords:
- OID_WDI_SET_PRIVACY_EXEMPTION_LIST ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 468406bddf74869d68464b2993e7479a9ca4626f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67359167"
---
# <a name="oidwdisetprivacyexemptionlist"></a>OID\_WDI\_設定\_プライバシー\_除外\_一覧


OID\_WDI\_設定\_プライバシー\_除外\_一覧は、パケットの説明の除外対象の一覧を提供する、ホストによって使用されます。 アダプターでは、除外対象に指定された IEEE EtherType 値に一致するパケットを受信するこれらの例外が適用されます。

| Scope | タスクでシリアル化された設定します。 | 通常の実行時間 (秒) |
|-------|--------------------------|---------------------------------|
| ポート  | 〇                      | 1                               |

 

## <a name="set-property-parameters"></a>プロパティ パラメーターの設定


| TLV                                                                                 | 許可されている複数の TLV インスタンス | 省略可能 | 説明                        |
|-------------------------------------------------------------------------------------|--------------------------------|----------|------------------------------------|
| [**WDI\_TLV\_プライバシー\_除外\_エントリ**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-privacy-exemption-entry) | x                              | x        | プライバシーの除外対象エントリの一覧です。 |

 

## <a name="set-property-results"></a>セットのプロパティの結果


追加データがありません。 ヘッダー内のデータで十分です。

<a name="requirements"></a>要件
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

 

 




