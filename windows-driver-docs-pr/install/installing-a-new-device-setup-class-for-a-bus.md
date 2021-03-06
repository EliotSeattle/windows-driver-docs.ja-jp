---
title: バス用の新しいデバイス セットアップ クラスのインストール
description: バス用の新しいデバイス セットアップ クラスのインストール
ms.assetid: a94899b6-02e0-4181-bb14-5552806a8c9e
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 663fb8f1155aaa98c567d3d98673192d1927aee9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63364974"
---
# <a name="installing-a-new-device-setup-class-for-a-bus"></a>バス用の新しいデバイス セットアップ クラスのインストール


新しいバスは、その機能は既存に属しているデバイスによって提供される機能と大幅に異なるデバイスをサポートしている場合[デバイス セットアップ クラス](device-setup-classes.md)バスの新しいデバイス セットアップ クラスをインストールする必要があります。 新しいデバイス セットアップ クラスをインストールするかどうかを判断するのに役立つ詳細については、次を参照してください。[新しいデバイス セットアップ クラスを作成する](creating-a-new-device-setup-class.md)します。

バスの新しいデバイス セットアップ クラスをインストールする関連するディレクティブを設定、 [ **INF バージョン セクション**](inf-version-section.md)、含める、 [ **INF ClassInstall32 セクション**](inf-classinstall32-section.md)、INF Class32 セクションで参照されている、ために必要な追加のセクションが含まれます。

次の注釈付きの例は、インストールに含める必要がある基本的な INF ファイルのエントリを示しています、[デバイス セットアップ クラス](device-setup-classes.md)します。 デバイス セットアップ クラスの構成設定については、次を参照してください。 [ **INF ClassInstall32 セクション**](inf-classinstall32-section.md)します。

```cpp
[Version]
signature="$CHICAGO$"
; Specify a unique class name that identifies the manufacturer and the bus type
Class=%AbcSuperBus%

; Specify a unique GUID that identifies the device setup class
ClassGUID={17ed6609-9bc8-44ca-8548-abb79b13781b}

; Identify the provider of the INF file
Provider=%AbcCorp%

; Specify the version of the device driver
DriverVer=01/01/2007,1.0.0.0 

[ClassInstall32]
; Reference an AddReg directive that specifies class properties
Addreg=AbcSuperBusClassReg 

[AbcSuperBusClassReg]
; Specify the properties of the device setup class
HKR,,,,%AbcSuperBus%
HKR,,Icon,,-19
HKR,,NoInstallClass,,1
. . .
. . .
[Strings] 
AbcCorp="Abc Corporation"
AbcSuperBus="Abc Corporation Super Bus Controller"
```

 

 





