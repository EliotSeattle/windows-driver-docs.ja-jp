---
title: MSFC\_VirtualFibrePortAttributes WMI クラス
description: MSFC\_VirtualFibrePortAttributes WMI クラス
ms.assetid: D605D63F-0EBF-44C0-8ADE-729F2DE48487
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 288613b89e600cce387432ebec7656a054fedb1f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63386547"
---
# <a name="msfcvirtualfibreportattributes-wmi-class"></a>MSFC\_VirtualFibrePortAttributes WMI クラス


WMI クライアントが使用、MSFC\_VirtualFibrePortAttributes クラスの仮想ポートのプロパティを取得します。

MSFC\_VirtualFibrePortAttributes クラスが次のように定義されている*Npivwmi.mof*:

```mof
class MSFC_VirtualFibrePortAttributes  
{  
    [WmiDataId(1), Description("Status of the virtual port"):Amended,  
    uint32 Status;  
  
    [WmiDataId(2), Description("FC Id"):Amended]  
    uint32 FCId;  
      
    [WmiDataId(3), Description("Port symbolic name"):Amended]  
    uint16 VirtualName[64];  
  
    [WmiDataId(4), Description("An opaque tag passed in by the app. 128 bit so that a guid can be stored in it."):Amended]  
    uint8 Tag[16];  
  
    [WmiDataId(5), Description("The world wide port name of the virtual port"):Amended]  
    uint8 WWPN[8];   
  
    [WmiDataId(6), Description("The world wide node name of the virtual port"):Amended]  
    uint8 WWNN[8];   
  
    [WmiDataId(7), Description("The world wide node name of fabric"):Amended]  
    uint8 FabricWWN[8];  
};  
```

WMI ツール スイートによってコンパイルされると、このクラスの定義には、次のデータ構造が生成されます。

[**MSFC\_VirtualFibrePortAttributes**](https://msdn.microsoft.com/library/windows/hardware/hh127628)

この WMI クラスに関連付けられているメソッドはありません。

 

 





