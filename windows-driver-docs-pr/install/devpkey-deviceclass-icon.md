---
title: DEVPKEY_DeviceClass_Icon
description: DEVPKEY_DeviceClass_Icon
ms.assetid: 036b6daf-b5de-4aa0-b7e3-ba0430107938
keywords:
- DEVPKEY_DeviceClass_Icon デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- DEVPKEY_DeviceClass_Icon
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: cc038b8f0ac64f9d89c0e692f3d950bae33ab6bf
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378076"
---
# <a name="devpkeydeviceclassicon"></a>DEVPKEY_DeviceClass_Icon


DEVPKEY_DeviceClass_Icon デバイス プロパティがのアイコンを表す、[デバイス セットアップ クラス](https://docs.microsoft.com/windows-hardware/drivers/install/device-setup-classes)します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>プロパティのキー</strong></p></td>
<td align="left"><p>DEVPKEY_DeviceClass_Icon</p></td>
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
<td align="left"><p><strong>ローカライズか。</strong></p></td>
<td align="left"><p>X</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

DEVPKEY_DeviceClass_Icon の値によって設定されます、 [ **INF AddReg ディレクティブ**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addreg-directive)に含まれている、 [ **INF ClassInstall32 セクション**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-classinstall32-section)クラスをインストールするとします。 DEVPKEY_DeviceClass_Icon の値を設定するには、使用、 **AddReg**を設定するディレクティブ、**アイコン**クラスのレジストリ エントリの値。

**アイコン**エントリの値が文字列の形式で整数値。 数が負の場合、数値の絶対値、setupapi.dll にあるアイコンのリソース識別子です。 数が正の場合がある場合、クラスのインストーラーまたはクラスのプロパティ ページのプロバイダー、クラスのインストーラーがなく、プロパティ ページのプロバイダーがある場合、数、クラスのインストーラー、DLL のアイコンのリソース識別子です。 ゼロの値が無効です。

呼び出すことができます[ **SetupDiGetClassProperty** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclasspropertyw)または[ **SetupDiGetClassPropertyEx** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclasspropertyexw) DEVPKEY_DeviceClass_Icon の値を取得するには.

Windows Server 2003、Windows XP、および Windows 2000 は、このプロパティをサポートは DEVPKEY_DeviceClass_Icon プロパティのキーをサポートしていません。 Windows Server 2003、Windows XP、および Windows 2000 でのデバイス セットアップ クラスに対する小さいアイコンへのアクセス方法については、次を参照してください。[デバイス セットアップ クラスのアイコンのプロパティにアクセスする](https://docs.microsoft.com/windows-hardware/drivers/install/accessing-icon-properties-of-a-device-setup-class)します。

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


[**INF AddReg ディレクティブ**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addreg-directive)

[**INF ClassInstall32 セクション**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-classinstall32-section)

[**SetupDiGetClassProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclasspropertyw)

[**SetupDiGetClassPropertyEx**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclasspropertyexw)

[**SetupDiDrawMiniIcon**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdidrawminiicon)

[**SetupDiLoadClassIcon**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiloadclassicon)

 

 






