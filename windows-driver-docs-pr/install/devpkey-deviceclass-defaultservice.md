---
title: DEVPKEY_DeviceClass_DefaultService
description: DEVPKEY_DeviceClass_DefaultService
ms.assetid: 19d1a9ea-3bde-4230-af1a-b67b5a29e6f4
keywords:
- DEVPKEY_DeviceClass_DefaultService デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- DEVPKEY_DeviceClass_DefaultService
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: d5fd1be85ac24b22d45115bdaac40579c2b7a1cb
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378086"
---
# <a name="devpkeydeviceclassdefaultservice"></a>DEVPKEY_DeviceClass_DefaultService


DEVPKEY_DeviceClass_DefaultService のデバイス プロパティの既定のサービスの名前を表します、[デバイス セットアップ クラス](https://docs.microsoft.com/windows-hardware/drivers/install/device-setup-classes)します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>プロパティのキー</strong></p></td>
<td align="left"><p>DEVPKEY_DeviceClass_DefaultService</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>データ型のプロパティの識別子</strong></p></td>
<td align="left"><p><a href="devprop-type-string.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_STRING&lt;/strong&gt;](devprop-type-string.md)"><strong>DEVPROP_TYPE_STRING</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>プロパティへのアクセス</strong></p></td>
<td align="left"><p>アプリケーションをインストールし、インストーラーによって、読み取り専用アクセス</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>対応するレジストリ値の名前</strong></p></td>
<td align="left"><p><strong>既定のサービス</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>ローカライズか。</strong></p></td>
<td align="left"><p>X</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

デバイス セットアップ クラスに対する既定のサービスがインストールされているし、デバイスがデバイスに固有のサービスをインストールしていない場合、 [ **INF ClassInstall32.Services セクション**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-classinstall32-services-section)のクラスをインストールする INF ファイルデバイスのクラスの既定のサービスをインストールします。

DEVPKEY_DeviceClass_DefaultService の値は、の値、**既定 Service**クラスのレジストリ キーの下のレジストリ値。

呼び出すことができます[ **SetupDiGetClassProperty** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclasspropertyw)または[ **SetupDiGetClassPropertyEx** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclasspropertyexw) DEVPKEY_DeviceClass_ の値を取得するにはDefaultService します。

Windows Server 2003、Windows XP、および Windows 2000 は、このプロパティをサポートは DEVPKEY_DeviceClass_DefaultService プロパティのキーをサポートしていません。 対応するこのプロパティの値にアクセスすることができます**既定 Service**クラスのレジストリ キーの下のレジストリ値。 クラスのレジストリ キー値のエントリをアクセスする方法については、次を参照してください。[にアクセスするレジストリ エントリの値で、クラス レジストリ キー](https://docs.microsoft.com/windows-hardware/drivers/install/accessing-registry-entry-values-under-the-class-registry-key)します。

<a name="requirements"></a>要件
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


[**INF ClassInstall32.Services セクション**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-classinstall32-services-section)

[**SetupDiGetClassProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclasspropertyw)

[**SetupDiGetClassPropertyEx**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclasspropertyexw)

 

 






