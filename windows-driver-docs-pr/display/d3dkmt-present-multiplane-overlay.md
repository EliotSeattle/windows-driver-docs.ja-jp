---
title: D3DKMT\_存在\_MULTIPLANE\_オーバーレイ構造体
description: システムの使用に予約されています。 ドライバーでは使用しないでください。
ms.assetid: 2526ccce-826a-4e8f-ab15-639510b1d5cf
keywords:
- D3DKMT_PRESENT_MULTIPLANE_OVERLAY 構造体のディスプレイ デバイス
topic_type:
- apiref
api_name:
- D3DKMT_PRESENT_MULTIPLANE_OVERLAY
api_location:
- D3dkmthk.h
api_type:
- HeaderDef
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: bc406f672581819e08752986980c086187797e89
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63331300"
---
# <a name="d3dkmtpresentmultiplaneoverlay-structure"></a>D3DKMT\_存在\_MULTIPLANE\_オーバーレイ構造体


システムの使用に予約されています。 ドライバーでは使用しないでください。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
typedef struct D3DKMT_PRESENT_MULTIPLANE_OVERLAY {
  union {
    D3DKMT_HANDLE hDevice;
    D3DKMT_HANDLE hContext;
  };
  ULONG                          BroadcastContextCount;
  D3DKMT_HANDLE                  BroadcastContext[D3DDDI_MAX_BROADCAST_CONTEXT];
  D3DDDI_VIDEO_PRESENT_SOURCE_ID VidPnSourceId;
  UINT                           PresentCount;
  D3DDDI_FLIPINTERVAL_TYPE       FlipInterval;
  D3DKMT_PRESENTFLAGS            Flags;
  UINT                           PresentPlaneCount;
  D3DKMT_MULTIPLANE_OVERLAY      *pPresentPlanes;
  UINT                           Duration;
} D3DKMT_PRESENT_MULTIPLANE_OVERLAY;
```

<a name="members"></a>メンバー
-------

**hDevice**

**hContext**

**BroadcastContextCount**

**BroadcastContext**

**VidPnSourceId**

**PresentCount**

**FlipInterval**

**フラグ**

**PresentPlaneCount**

**pPresentPlanes**

**Duration**

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>サポートされている最小のクライアント</p></td>
<td align="left"><p>Windows 8</p></td>
</tr>
<tr class="even">
<td align="left"><p>サポートされている最小のサーバー</p></td>
<td align="left"><p>Windows Server 2012</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">D3dkmthk.h</td>
</tr>
</tbody>
</table>

 

 





