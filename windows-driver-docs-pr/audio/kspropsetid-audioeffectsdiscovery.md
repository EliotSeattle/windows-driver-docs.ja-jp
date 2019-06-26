---
title: KSPROPSETID\_AudioEffectsDiscovery
description: KSPROPSETID\_AudioEffectsDiscovery プロパティ セットは、マイクロソフトの汎用プロキシ オーディオ処理オブジェクト (APO) を使用するオーディオ デバイス ドライバによって実装されます。
ms.assetid: 68229885-1446-4BF0-B4E1-96A777006567
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 752ef27db4769a13239a2f9d782a46ed515833de
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358722"
---
# <a name="kspropsetidaudioeffectsdiscovery"></a>KSPROPSETID\_AudioEffectsDiscovery


**KSPROPSETID\_AudioEffectsDiscovery**プロパティ セットは、マイクロソフトの汎用プロキシ オーディオ処理オブジェクト (APO) を使用するオーディオ デバイス ドライバによって実装されます。

**KSPROPSETID\_AudioEffectsDiscovery**は Windows 8.1 と Windows オペレーティング システムの以降のバージョンで使用できます。

*MsApoFxProxy.h*ヘッダー ファイルの定義、 **KSPROPSETID\_AudioEffectsDiscovery**プロパティを次のように設定します。

``` syntax
#define STATIC_KSPROPSETID_AudioEffectsDiscovery\  
    0xb217a72, 0x16b8, 0x4a4d, 0xbd, 0xed, 0xf9, 0xd6, 0xbb, 0xed, 0xcd, 0x8f  
DEFINE_GUIDSTRUCT("0B217A72-16B8-4A4D-BDED-F9D6BBEDCD8F", KSPROPSETID_AudioEffectsDiscovery);  
#define KSPROPSETID_AudioEffectsDiscovery DEFINE_GUIDNAMED(KSPROPSETID_AudioEffectsDiscovery)
```

**KSPROPSETID\_AudioEffectsDiscovery**プロパティ セットには、次の KS プロパティが含まれています。

[**KSPROPERTY\_AUDIOEFFECTSDISCOVERY\_EFFECTSLIST**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/dn457706(v=vs.85))

このプロパティ名が定義されている、 [ **KSPROPERTY\_AUDIOEFFECTSDISCOVERY** ](https://docs.microsoft.com/windows/desktop/api/msapofxproxy/ne-msapofxproxy-ksproperty_audioeffectsdiscovery)列挙型。

 

 





