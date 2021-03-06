---
title: GUID_61883_CLASS
description: GUID_61883_CLASS
ms.assetid: 3380c42c-3ac4-4d71-9a1b-581ef8c7b57a
keywords:
- GUID_61883_CLASS デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- GUID_61883_CLASS
api_location:
- 61883.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 75e97f886dda6cd11308761d7353834926b82640
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67387333"
---
# <a name="guid61883class"></a>GUID_61883_CLASS


GUID_61883_CLASS[デバイス インターフェイス クラス](https://docs.microsoft.com/windows-hardware/drivers/install/device-interface-classes)、61883 デバイスに対して定義されているが[デバイス セットアップ クラス](https://docs.microsoft.com/windows-hardware/drivers/install/device-setup-classes)します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">属性</th>
<th align="left">設定</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>識別子</p></td>
<td align="left"><p>GUID_61883_CLASS</p></td>
</tr>
<tr class="even">
<td align="left"><p>クラス GUID</p></td>
<td align="left"><p>{7EBEFBC0-3200-11d2-B4C2-00A0C9697D07}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>コメント
-------

61883 デバイス セットアップ クラスのデバイス用のドライバーでは、オペレーティング システムと 61883 デバイスの存在をアプリケーションに通知するこのデバイスのインターフェイス クラスのインスタンスを登録します。 61883 デバイス インターフェイスのクラスには、IEC 61883 プロトコルをサポートする IEEE 1394 デバイスが含まれています。 61883 のデバイスとドライバーについては、次を参照してください。 [IEC 61883 クライアント ドライバー](https://docs.microsoft.com/windows-hardware/drivers/ieee/iec-61883-client-drivers)します。

1394 bus デバイスに対するデバイス セットアップ クラスについては、次を参照してください。 [ **BUS1394_CLASS_GUID**](bus1394-class-guid.md)します。

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
<td align="left"><p>Windows XP および Windows の以降のバージョンで使用できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">61883.h (61883.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**BUS1394_CLASS_GUID**](bus1394-class-guid.md)

 

 






