---
title: DEVPKEY_Device_SessionId
description: DEVPKEY_Device_SessionId
ms.assetid: 0e5815b3-0427-4f07-9ec1-a21976d5d933
keywords:
- DEVPKEY_Device_SessionId デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- DEVPKEY_Device_SessionId
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 951628a50589c0a3111c71378212e64eb1c5148a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363009"
---
# <a name="devpkeydevicesessionid"></a>DEVPKEY_Device_SessionId


DEVPKEY_Device_SessionId デバイス プロパティは、ターミナル サービス セッションでアクセスできるデバイスのインスタンスを示す値を表します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>プロパティのキー</strong></p></td>
<td align="left"><p>DEVPKEY_Device_SessionId</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>データ型のプロパティの識別子</strong></p></td>
<td align="left"><p><a href="devprop-type-uint32.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_UINT32&lt;/strong&gt;](devprop-type-uint32.md)"><strong>DEVPROP_TYPE_UINT32</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>プロパティへのアクセス</strong></p></td>
<td align="left"><p>読み取りおよび書き込みアプリケーションやサービスでのアクセス。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ローカライズか。</strong></p></td>
<td align="left"><p>X</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

ターミナル サーバーの機能は、プラグ アンド プレイ (PnP) デバイス リダイレクトをサポートします。 デバイスのリダイレクトは、すべてのターミナル サービス セッションのアプリケーションとサービスによってデバイスにアクセスするかどうか、またはデバイスが特定のターミナル サービス セッション内でのみアクセスできるかどうかを判断します。 ターミナル サービス セッション内で、デバイスのユーザー補助機能については、次のように、デバイスの DEVPKEY_Device_SessionId の設定によって決まります。

-   DEVPKEY_Device_SessionId プロパティが存在しないか、プロパティが存在する場合、プロパティの値が設定されていない、すべてのアクティブなターミナル サービス セッションで、デバイスにアクセスできます。

-   DEVPKEY_Device_SessionId プロパティが存在し、プロパティの値が 0 以外の場合、ターミナル サービス l セッション識別子を設定、デバイスがターミナル サービス セッションの識別子で示される、ターミナル サービス セッションでのみアクセスできます。

-   DEVPKEY_Device_SessionId プロパティが存在し、プロパティの値が 0 に設定されて、デバイスがサービスによってのみアクセスできます。 セッション 0 では、サービスのみが実行できる特殊なセッションです。

DEVPKEY_Device_SessionId プロパティを呼び出すことによってアクセスできる[ **SetupDiGetDeviceProperty** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)と[ **SetupDiSetDeviceProperty** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdisetdevicepropertyw).

Windows Server 2003、Windows XP、および Windows 2000 では、このプロパティはサポートされません。

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>バージョン</p></td>
<td align="left"><p>Windows Vista および Windows の以降のバージョンで使用できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Devpkey.h (Devpkey.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**SetupDiGetDeviceProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)

[**SetupDiSetDeviceProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdisetdevicepropertyw)

 

 






