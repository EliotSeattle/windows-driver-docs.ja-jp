---
title: DirectX VA デバイスの取得
description: DirectX VA デバイスの取得
ms.assetid: 7af82243-7cb3-4e66-a6ee-3f4220baa459
keywords:
- DirectX ビデオ アクセラレータ WDK Windows 2000 の表示、デバイスの取得
- DirectX VA デバイスの取得
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d72f5c8004c6ce12349110ddf1922b71dbca18f6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67365661"
---
# <a name="retrieving-directx-va-devices"></a>DirectX VA デバイスの取得


## <span id="ddk_retrieving_directx_va_devices_gg"></span><span id="DDK_RETRIEVING_DIRECTX_VA_DEVICES_GG"></span>


次のコード例を使用すると、VA の DirectX デバイスを取得できます。 このコードは、の実装、 [ *DdMoCompGetGuids* ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_getguids)コールバック関数。 **GetMoCompGuids**のメンバー、 [ **DD\_MOTIONCOMPCALLBACKS** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-dd_motioncompcallbacks)コールバック関数へのポインターを構造体します。

```cpp
DWORD g_dwDXVANumSupportedGUIDs = 4;
const GUID* g_DXVASupportedGUIDs[4] = {
 &DXVA_DeinterlaceContainerDevice,
    &DXVA_ProcAmpControlDevice
    &DXVA_DeinterlaceBobDevice
 &DXVA_COPPDevice
};

DWORD APIENTRY
  MOCOMPCB_GETGUIDS(
    PDD_GETMOCOMPGUIDSDATA  lpData
    )
{
    DWORD dwNumToCopy;

    // If lpGuids == NULL, the driver must return the number of 
    // supported GUIDS in the dwNumGuids parameter. If non-NULL, 
    // the supported GUIDS must be copied into the buffer at lpGuids.
    if (lpData->lpGuids) {
        dwNumToCopy = min(g_dwDXVANumSupportedGUIDs, lpData->dwNumGuids);
        for (DWORD i = 0; i < dwNumToCopy; i++) {
            lpData->lpGuids[i] = *g_DXVASupportedGUIDs[i];
        }
    }
    else {
        dwNumToCopy = g_dwDXVANumSupportedGUIDs;
    }

    lpData->dwNumGuids = dwNumToCopy;
    lpData->ddRVal = DD_OK;

    return DDHAL_DRIVER_HANDLED;
}
```

 

 





