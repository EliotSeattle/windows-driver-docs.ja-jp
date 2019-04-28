---
title: Hello World' のインストール ファイル
description: Hello World' のインストール ファイル
ms.assetid: 826f4f99-16bd-4586-9cc1-0afde2fcee65
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 17e3dd3c02647d4c9f762ccb83611f968c346655
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63377633"
---
# <a name="hello-world-installation-file"></a>'Hello World' のインストール ファイル

ミニドライバーは、インストールするセットアップ情報 (INF) ファイルが必要です。 INF ファイルでは、すべてのデバイスのインストールに必要な情報を含むテキスト ファイルです。 INF ファイルについては、次を参照してください。、 [WIA デバイスの INF ファイル](inf-files-for-wia-devices.md)と[INF ファイルを作成する](https://msdn.microsoft.com/library/windows/hardware/ff549520)セクション。

*Hellowld.inf*ファイルは、次を含める必要があります。

```INF
; HELLOWLD.INF  -- Hello World WIA Minidriver setup file
; Copyright (c) 2002-2003 Hello World Company
; Manufacturer:  Hello World Company

[Version]
Signature=$WINDOWS NT$
Class=Image
ClassGUID={6bdd1fc6-810f-11d0-bec7-08002be2092f}
Provider=%Mfg%
DriverVer=06/26/2001,1.0
CatalogFile=wia.cat

[DestinationDirs]
DefaultDestDir=11

[Manufacturer]
%Mfg%=Models

[Models]
%WIADevice.DeviceDesc% = WIADevice.Scanner, HELLOWORLD_PNP_ID

[WIADevice.Scanner]
Include=sti.inf
Needs=STI.SerialSection
SubClass=StillImage
DeviceType=2
DeviceSubType=0x0
Capabilities=0x30
DeviceData=WIADevice.DeviceData
AddReg=WIADevice.AddReg
CopyFiles=WIADevice.CopyFiles
ICMProfiles="sRGB Color Space Profile.icm"

[WIADevice.Scanner.Services]
Include=sti.inf
Needs=STI.SerialSection.Services

[WIADevice.DeviceData]
Server=local
UI DLL=sti.dll
UI Class ID={4DB1AD10-3391-11D2-9A33-00C04FA36145}

[WIADevice.AddReg]
HKR,,HardwareConfig,1,1
HKR,,USDClass,,"{7C1E2309-A535-45b1-94B3-9A020EE600C6}"
HKCR,CLSID\{7C1E2309-A535-45b1-94B3-9A020EE600C6},,,"Hello World WIA Minidriver"
HKCR,CLSID\{7C1E2309-A535-45b1-94B3-9A020EE600C6}\InProcServer32,,,%11%\hellowld.dll
HKCR,CLSID\{7C1E2309-A535-45b1-94B3-9A020EE600C6}\InProcServer32,ThreadingModel,,Both

[WIADevice.CopyFiles]
hellowld.dll

[SourceDisksFiles.x86]
hellowld.dll=1
[SourceDisksNames.x86]
1=%Location%,,,

[SourceDisksFiles.IA64]
hellowld.dll=1
[SourceDisksNames.IA64]
1=%Location%,,,

[Strings]
Mfg="Hello World Company"
WIADevice.DeviceDesc="Hello World WIA Minidriver"
Location="Hello World WIA Minidriver Installation Source"
```

 

 




