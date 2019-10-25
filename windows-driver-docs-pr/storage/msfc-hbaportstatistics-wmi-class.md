---
title: MSFC\_HBAPortStatistics WMI クラス
description: MSFC\_HBAPortStatistics WMI クラス
ms.assetid: 275e4a50-6500-4a23-a0ae-ddd232da42f0
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 830684bd5adb8d77f3fd4bfd760454477f3b1414
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845536"
---
# <a name="msfc_hbaportstatistics-wmi-class"></a>MSFC\_HBAPortStatistics WMI クラス


## <span id="ddk_msfc_hbaportstatistics_wmi_class_kr"></span><span id="DDK_MSFC_HBAPORTSTATISTICS_WMI_CLASS_KR"></span>


WMI クライアントは、MSFC\_HBAPortStatistics クラスを使用して、hba のポートに関連する統計を HBA ミニポートドライバーに照会します。

MSFC\_HBAPPortStatistics クラスは、 *Hbaapi .mof*で次のように定義されています。

```cpp
class MSFC_HBAPortStatistics
{
  [ WmiDataId(1) ]
  sint64 SecondsSinceLastReset;
  [ WmiDataId(2) ]
  sint64 TxFrames;
  [ WmiDataId(3) ]
  sint64 TxWords;
  [ WmiDataId(4) ]
  sint64 RxFrames;
  [ WmiDataId(5) ]
  sint64 RxWords;
  [ WmiDataId(6) ]
  sint64 LIPCount;
  [ WmiDataId(7) ]
  sint64 NOSCount;
  [ WmiDataId(8) ]
  sint64 ErrorFrames;
  [ WmiDataId(9) ]
  sint64 DumpedFrames;
  [ WmiDataId(10) ]
  sint64 LinkFailureCount;
  [ WmiDataId(11) ]
  sint64 LossOfSyncCount;
  [ WmiDataId(12) ]
  sint64 LossOfSignalCount;
  [ WmiDataId(13) ]
  sint64 PrimitiveSeqProtocolErrCount;
  [ WmiDataId(14) ]
  sint64 InvalidTxWordCount;
  [WmiDataId(15) ]
  sint64 InvalidCRCCount;
};
```

WMI ツールスイートによってコンパイルされた場合、このクラス定義では次のデータ構造が生成されます。

[**MSFC\_HBAPortStatistics**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_msfc_hbaportstatistics)

この WMI クラスに関連付けられているメソッドはありません。

 

 





