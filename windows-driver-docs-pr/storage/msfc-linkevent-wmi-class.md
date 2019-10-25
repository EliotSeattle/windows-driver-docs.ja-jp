---
title: MSFC\_LinkEvent WMI クラス
description: MSFC\_LinkEvent WMI クラス
ms.assetid: 9507fb1a-ce2a-4ce9-8272-77c8c9d0a92c
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 15e9ed5bc6539c3d98f17908007def2690e90a5f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845533"
---
# <a name="msfc_linkevent-wmi-class"></a>MSFC\_LinkEvent WMI クラス


## <span id="ddk_msfc_linkevent_wmi_class_kr"></span><span id="DDK_MSFC_LINKEVENT_WMI_CLASS_KR"></span>


WMI プロバイダーは、MSFC\_LinkEvent WMI クラスを使用してリンクイベントを報告します。

MSFC\_LinkEvent クラスは、次のように*Hbaapi .mof*で定義されます。

```cpp
class MSFC_LinkEvent : WMIEvent {
  [key] 
  string InstanceName;
  boolean Active;
  [WmiDataId(1), Description("Type of event") : amended,
    EVENT_TYPES_QUALIFIERS] uint32  EventType;
  [WmiDataId(2), Description("Discovered Port WWN") : amended,    HBAType("HBA_WWN")]uint8  AdapterWWN[8];
  [WmiDataId(3), Description("Size of RLIR buffer") : amended]
    uint32 RLIRBufferSize;
  [WmiDataId(4), Description("Size of RLIR buffer") : amended,
     WmiSizeIs("RLIRBufferSize")]uint8 RLIRBuffer[];
};
```

WMI ツールスイートによってコンパイルされた場合、このクラス定義では次のデータ構造が生成されます。

[**MSFC\_LinkEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_msfc_linkevent)

この WMI クラスに関連付けられているメソッドはありません。

 

 





