---
title: MOUNTDEV_MOUNTED_DEVICE_GUID
description: MOUNTDEV_MOUNTED_DEVICE_GUID
ms.assetid: 48d127ed-414b-40bb-8a35-6472c8783b81
keywords:
- MOUNTDEV_MOUNTED_DEVICE_GUID デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- MOUNTDEV_MOUNTED_DEVICE_GUID
api_location:
- Mountmgr.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 3da28329f4f87fbc77df61ee812183d64ffd7cee
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371924"
---
# <a name="mountdevmounteddeviceguid"></a>MOUNTDEV_MOUNTED_DEVICE_GUID


MOUNTDEV_MOUNTED_DEVICE_GUID[デバイス インターフェイス クラス](https://docs.microsoft.com/windows-hardware/drivers/install/device-interface-classes)ボリューム デバイス用に定義されます。

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
<td align="left"><p>MOUNTDEV_MOUNTED_DEVICE_GUID</p></td>
</tr>
<tr class="even">
<td align="left"><p>クラス GUID</p></td>
<td align="left"><p>{53F5630D-B6BF-11D0-94F2-00A0C91EFB8B}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

このデバイスのインターフェイス クラスの MOUNTDEV_MOUNTED_DEVICE_GUID 識別子はエイリアス、 [ **GUID_DEVINTERFACE_VOLUME** ](guid-devinterface-volume.md)デバイス インターフェイスのクラス。

記憶域[サンプル](https://go.microsoft.com/fwlink/p/?LinkId=618052)WDK に含まれています、 [ClassPnP ストレージ クラス ドライバー ライブラリ](https://go.microsoft.com/fwlink/p/?linkid=256095)MOUNTDEV_MOUNTED_DEVICE_GUID を使用して、GUID_DEVINTERFACE_VOLUME デバイス インターフェイスのインスタンスを登録するにはクラス。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">Mountmgr.h (include Mountmgr.h)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**GUID_DEVINTERFACE_VOLUME**](guid-devinterface-volume.md)

 

 






