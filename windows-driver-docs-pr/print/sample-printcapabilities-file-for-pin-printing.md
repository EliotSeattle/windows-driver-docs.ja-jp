---
title: PIN 印刷のサンプル PrintCapabilities ファイル
description: 次のサンプル PrintCapabilities ファイルは、暗証番号 (PIN) で保護された印刷を指定する方法を示しています。
ms.assetid: 4C3BBEF1-C0DB-48F7-B4EC-BBB5D3699692
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5fcf0ee3b823fbdbf5f960683f3c03adde3ef56d
ms.sourcegitcommit: ab64169b631da4db3f0b895600f1c38a22cb7e2e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/03/2020
ms.locfileid: "75652966"
---
# <a name="sample-printcapabilities-file-for-pin-printing"></a>PIN 印刷のサンプル PrintCapabilities ファイル


次のサンプル PrintCapabilities ファイルは、暗証番号 (PIN) で保護された印刷を指定する方法を示しています。

```xml
<?xml version="1.0"?>
<psf:PrintCapabilities
   xmlns:psf="https://schemas.microsoft.com/windows/2003/08/printing/printschemaframework" 
   xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance" 
   xmlns:xsd="https://www.w3.org/2001/XMLSchema" version="1"
   xmlns:psk="https://schemas.microsoft.com/windows/2003/08/printing/printschemakeywords"
   xmlns:pskv11=" https://schemas.microsoft.com/windows/2013/05/printing/printschemakeywordsv11">
   <psf:ParameterDef name="pskv11:JobPasscodeString">
      <psf:Property name="psf:DataType">
           <psf:Value xsi:type="xsd:QName">xsd:string</psf:Value>
      </psf:Property>
      <psf:Property name="psf:DefaultValue">
           <psf:Value xsi:type="xsd:string"/>
      </psf:Property>
      <psf:Property name="psf:MaxLength">
           <psf:Value xsi:type="xsd:integer">9</psf:Value>
      </psf:Property>
      <psf:Property name="psf:MinLength">
           <psf:Value xsi:type="xsd:integer">4</psf:Value>
      </psf:Property>
      <psf:Property name="psf:Mandatory">
              <psf:Value xsi:type="xsd:QName">psk:Optional</psf:Value>
      </psf:Property>
      <psf:Property name="psf:UnitType">
              <psf:Value xsi:type="xsd:string">numeric</psf:Value>
      </psf:Property>
      <psf:Property name="psk:DisplayName">
           <psf:Value xsi:type="xsd:string">Job PassCode</psf:Value>
      </psf:Property>
   </psf:ParameterDef>
   <psf:Feature name="pskv11:JobPasscode">
      <psf:Property name="psf:SelectionType">
           <psf:Value xsi:type="xsd:string">psk:PickOne</psf:Value>
      </psf:Property>
      <psf:Property name="psk:DisplayName">
           <psf:Value xsi:type="xsd:string">Enable Job PassCode</psf:Value>
      </psf:Property>
      <psf:Option name="psk:On" />
      <psf:Option name="psk:Off" />
   </psf:Feature>
</psf:PrintCapabilities>
```

保護された印刷の詳細については、「[保護された印刷のドライバーサポート](driver-support-for-protected-printing.md)」を参照してください。

 

 




