---
title: MIDI ストリームのデータ形式
description: MIDI ストリームのデータ形式
ms.assetid: c179cf74-7493-4c27-97bd-5eb4d0dffbe6
keywords:
- MIDI ストリームデータ形式 WDK オーディオ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: efa099d63939f97a382df9dbc4b392bf6e5a19d0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72830355"
---
# <a name="midi-stream-data-format"></a>MIDI ストリームのデータ形式


## <span id="midi_stream_data_format"></span><span id="MIDI_STREAM_DATA_FORMAT"></span>


この例では、 [**KSDATAFORMAT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksdataformat)構造体を使用して、MIDI ストリームのデータ形式を記述します。

```cpp
  DataFormat.FormatSize  = sizeof(KSDATAFORMAT);
  DataFormat.Flags       = 0;
  DataFormat.SampleSize  = 0;
 DataFormat.Reserved    = 0;
  DataFormat.MajorFormat = STATICGUIDOF(KSDATAFORMAT_TYPE_MUSIC);
  DataFormat.SubFormat   = STATICGUIDOF(KSDATAFORMAT_SUBTYPE_MIDI);
  DataFormat.Specifier   = STATICGUIDOF(KSDATAFORMAT_SPECIFIER_NONE);
```

 

 




