---
title: DirectSound Stream データの形式
description: DirectSound Stream データの形式
ms.assetid: 41d3d5ad-7336-4ecf-b6e2-a24ee4ec731f
keywords:
- DirectSound WDK のオーディオ ストリームのデータを形式します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f6fc290a9e065315764558f4982a724d91f8db4e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557250"
---
# <a name="directsound-stream-data-format"></a>DirectSound Stream データの形式


## <span id="directsound_stream_data_format"></span><span id="DIRECTSOUND_STREAM_DATA_FORMAT"></span>


この例では、 [ **KSDATAFORMAT\_DSOUND** ](https://msdn.microsoft.com/library/windows/hardware/ff537094) DirectSound ストリームのデータ形式を記述する構造体。

```cpp
  DataFormat.FormatSize  = sizeof(KSDATAFORMAT_DSOUND);
 DataFormat.Flags       = 0;
  DataFormat.SampleSize  = 0;
  DataFormat.Reserved    = 0;
  DataFormat.MajorFormat = STATICGUIDOF(KSDATAFORMAT_TYPE_AUDIO);
  DataFormat.SubFormat   = STATICGUIDOF(KSDATAFORMAT_SUBTYPE_PCM);
 DataFormat.Specifier   = STATICGUIDOF(KSDATAFORMAT_SPECIFIER_DSOUND);
  BufferDesc.Flags       = KSDSOUND_BUFFER_LOCHARDWARE;
  BufferDesc.Control     = KSDSOUND_BUFFER_CTRL_3D;
  BufferDesc.WaveFormatEx.wFormatTag      = WAVE_FORMAT_PCM;
  BufferDesc.WaveFormatEx.nChannels       = 2;
  BufferDesc.WaveFormatEx.nSamplesPerSec  = 22050;
  BufferDesc.WaveFormatEx.nAvgBytesPerSec = 88200;
  BufferDesc.WaveFormatEx.nBlockAlign     = 4;
  BufferDesc.WaveFormatEx.wBitsPerSample  = 16;
  BufferDesc.WaveFormatEx.cbSize          = 0;
```

 

 




