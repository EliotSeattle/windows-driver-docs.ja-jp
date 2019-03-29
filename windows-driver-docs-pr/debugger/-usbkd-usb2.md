---
title: usbkd.usb2
description: Usbkd.usb2 コマンドは、USB 2.0 のスケジュール情報を持つことが USB エンドポイントの一覧を表示します。
ms.assetid: 48DC685A-3624-4DAD-8077-FB7C4BE4BE93
keywords:
- デバッグ usbkd.usb2 Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usbkd.usb2
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 18db66eb1364197d36930e5cb7a4675882b15dcd
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56581745"
---
# <a name="usbkdusb2"></a>!usbkd.usb2


**! Usbkd.usb2**コマンドは、USB 2.0 のスケジュール情報を持っている USB エンドポイントの一覧を表示します。

```dbgcmd
!usbkd.usb2 DeviceExtension
```

## <a name="span-idddkdevobjdbgspanspan-idddkdevobjdbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>パラメーター


<span id="_______DeviceExtension______"></span><span id="_______deviceextension______"></span><span id="_______DEVICEEXTENSION______"></span> *DeviceExtension*   
USB ホスト コント ローラーの機能のデバイス オブジェクト (FDO) のデバイスの拡張機能のアドレス。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Usbkd.dll

<a name="examples"></a>使用例
--------

USB ホスト コント ローラーの FDO のデバイスの拡張機能のアドレスを検索する 1 つの方法を次に示します。 最初に入力[ **! usbkd.usb2tree**](-usbkd-usb2tree.md)します。

```dbgcmd
0: kd> !usbkd.usb2tree

EHCI MINIPORT(s) dt usbport!_USBPORT_MINIPORT_DRIVER ffffe00001f48bd0
...
2)!ehci_info ffffe00001ca11a0 !devobj ffffe00001ca1050 PCI: VendorId 8086 DeviceId 293c RevisionId 0002 
...
```

上記の出力の引数として、FDO のデバイスの拡張機能のアドレスを表示、 [DML](debugger-markup-language-commands.md)コマンド **! ehci\_情報 ffffe00001ca11a0**します。 デバイスの拡張機能のアドレスを渡す、 **! usb2**コマンド。

```dbgcmd
0: kd> !usbkd.usb2 ffffe00001ca11a0

Sig: HFDO
Hcd FDO Extension:
----------
----------
dt usbport!_HCD_ENDPOINT ffffe0000212d970  !usbep ffffe0000212d970
    Tt 0000000000000000 Device Address: 0x00, ep 0x81 Interrupt In
    dt _USB2LIB_ENDPOINT_CONTEXT ffffe000023b60f0    dt _USB2_EP ffffe000023b6100
    Period,offset,Ordinal(32,0,0)   smask,cmask(00,00  ........ , ........) maxpkt 1
```

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[USB 2.0 デバッガー拡張機能](usb-2-0-extensions.md)

[ユニバーサル シリアル バス (USB) ドライバー](https://go.microsoft.com/fwlink/p?LinkID=227351)

 

 






