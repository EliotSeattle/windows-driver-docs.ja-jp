---
title: MSFC\_FibrePortHBAAttributes WMI クラス
description: MSFC\_FibrePortHBAAttributes WMI クラス
ms.assetid: 028afadf-1a2d-4792-8b6c-d53359af64c1
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 218502ab9dc518f9c817ed75240c7f9bded2c0d0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842860"
---
# <a name="msfc_fibreporthbaattributes-wmi-class"></a>MSFC\_FibrePortHBAAttributes WMI クラス


## <span id="ddk_msfc_fibreporthbaattributes_wmi_class_kr"></span><span id="DDK_MSFC_FIBREPORTHBAATTRIBUTES_WMI_CLASS_KR"></span>


FCbre チャネル HBA API をサポートする HBA ミニポートドライバーは、MSFC\_FibrePortHBAAttributes WMI クラスを使用して、ファイバーチャネルポートに関連付けられている属性情報を公開します。 各ポートには、このクラスのインスタンスが1つ存在する必要があります。

MSFC\_FibrePortHBAAttributes クラスは、次のように*Hbaapi .mof*で定義されます。

```cpp
class MSFC_FibrePortHBAAttributes {
  [key] 
  string InstanceName;
  boolean Active;
  [Description ("Unique identifier for the port. "
    "This identifier must be unique among all "
    "ports on all adapters. The same value for "
    "in other classes that expose port information"
    "the identifier must be used for the same port") : amended,
    WmiRefClass("MSFC_FibrePort"),
    WmiRefProperty("UniquePortId"),
    WmiDataId(1)
    ] uint64 UniquePortId;
  [HBA_STATUS_QUALIFIERS, WmiDataId(2)] HBA_STATUS  HBAStatus;
  [HBAType("HBA_PORTATTRIBUTES"),WmiDataId(3)]
    MSFC_HBAPortAttributesResults Attributes;
};
```

WMI ツールスイートによってコンパイルされた場合、このクラス定義では次のデータ構造が生成されます。

[**MSFC\_FibrePortHBAAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_msfc_fibreporthbaattributes)

この WMI クラスに関連付けられているメソッドはありません。

 

 





