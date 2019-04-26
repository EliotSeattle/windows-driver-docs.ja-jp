---
title: HS_NETWORK_IDENTITY 構造体
description: HS_NETWORK_IDENTITY 構造体には、Wi-fi ネットワークを一意に識別する情報が含まれています。
ms.assetid: 40d9720b-c122-4d19-8907-cfa2a05014e7
keywords:
- Windows Vista 以降のドライバーをネットワーク HS_NETWORK_IDENTITY 構造体
- Windows Vista 以降のドライバーをネットワーク PHS_NETWORK_IDENTITY 構造体ポインター
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: d9bbffa2b2b153be41a8443eb8cf74d1f0c1136b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63351039"
---
# <a name="hsnetworkidentity-structure"></a>HS\_ネットワーク\_IDENTITY 構造体

[!include[Wi-Fi Hotspot Offloading deprecation](wi-fi-hotspot-offloading-deprecation.md)]


**HS\_ネットワーク\_IDENTITY**構造体には、Wi-fi ネットワークを一意に識別する情報が含まれています。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
typedef struct _HS_NETWORK_IDENTITY {
  HS_SSID             Ssid;
  HS_AUTH_ALGORITHM   hsAuthAlgo;
  HS_CIPHER_ALGORITHM hsCipherAlgo;
} HS_NETWORK_IDENTITY, *PHS_NETWORK_IDENTITY;
```

<a name="members"></a>メンバー
-------

**ssid**  
ネットワークが SSID。

**hsAuthAlgo**  
ワイヤレス ネットワークで使用される認証アルゴリズム。

**hsCipherAlgo**  
ワイヤレス ネットワークで使用される暗号アルゴリズム。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Hotspotoffloadplugin.h (Hotspotoffloadplugin.h を含む)</td>
</tr>
</tbody>
</table>

 

 




