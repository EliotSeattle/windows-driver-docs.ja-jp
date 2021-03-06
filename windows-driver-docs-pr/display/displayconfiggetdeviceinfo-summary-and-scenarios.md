---
title: DisplayConfigGetDeviceInfo の概要とシナリオ
description: DisplayConfigGetDeviceInfo の概要とシナリオ
ms.assetid: 19d9a77c-252e-4623-b4bc-f0b990ed31e2
keywords:
- Windows 7 の WDK の表示、CCD Api、DisplayConfigGetDeviceInfo 接続が表示されます。
- WDK の Windows Server 2008 R2 の表示、CCD Api、DisplayConfigGetDeviceInfo 接続が表示されます。
- Windows 7 の WDK の表示、CCD Api、DisplayConfigGetDeviceInfo 構成が表示されます。
- 構成するには、WDK Windows Server 2008 R2 の表示、CCD Api、DisplayConfigGetDeviceInfo が表示されます。
- CCD WDK Windows 7 の概念の表示、DisplayConfigGetDeviceInfo
- CCD 概念 WDK Windows Server 2008 R2 の表示、DisplayConfigGetDeviceInfo
- DisplayConfigGetDeviceInfo WDK Windows 7 の表示
- DisplayConfigGetDeviceInfo WDK Windows Server 2008 R2 の表示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 76e7ad0bd73f4d7c1948a84651c03a07315a4b63
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67365737"
---
# <a name="displayconfiggetdeviceinfo-summary-and-scenarios"></a>DisplayConfigGetDeviceInfo の概要とシナリオ


このセクションでは、Windows 7 以降および Windows Server 2008 R2 以降のバージョンの Windows オペレーティング システムにのみ適用されます。

次のセクションでは、呼び出し元が使用する方法をまとめると、 [ **DisplayConfigGetDeviceInfo** ](https://docs.microsoft.com/windows/desktop/api/winuser/nf-winuser-displayconfiggetdeviceinfo) CCD 関数を使用するためのシナリオを提供**DisplayConfigGetDeviceInfo**します。

### <a name="span-iddisplayconfiggetdeviceinfosummaryspanspan-iddisplayconfiggetdeviceinfosummaryspandisplayconfiggetdeviceinfo-summary"></a><span id="displayconfiggetdeviceinfo_summary"></span><span id="DISPLAYCONFIGGETDEVICEINFO_SUMMARY"></span>DisplayConfigGetDeviceInfo の概要

呼び出し元が使用できる[ **DisplayConfigGetDeviceInfo** ](https://docs.microsoft.com/windows/desktop/api/winuser/nf-winuser-displayconfiggetdeviceinfo)ユーザー インターフェイスに表示するに分かりやすい名前を取得します。 呼び出し元は、アダプター、ソースおよびターゲットの名前を取得できます。 呼び出し元が使用できるも**DisplayConfigGetDeviceInfo**接続されているディスプレイ デバイスのネイティブの解像度を取得します。

### <a name="span-iddisplayconfiggetdeviceinfoscenariosspanspan-iddisplayconfiggetdeviceinfoscenariosspandisplayconfiggetdeviceinfo-scenarios"></a><span id="displayconfiggetdeviceinfo_scenarios"></span><span id="DISPLAYCONFIGGETDEVICEINFO_SCENARIOS"></span>DisplayConfigGetDeviceInfo シナリオ

[**DisplayConfigGetDeviceInfo** ](https://docs.microsoft.com/windows/desktop/api/winuser/nf-winuser-displayconfiggetdeviceinfo)は、次のシナリオで呼び出されます。

-   表示のコントロール パネル アプレット呼び出し[ **DisplayConfigGetDeviceInfo** ](https://docs.microsoft.com/windows/desktop/api/winuser/nf-winuser-displayconfiggetdeviceinfo)接続されているすべてのモニターを一覧表示するドロップダウン メニューに表示するモニター名を取得します。

-   表示のコントロール パネル アプレット呼び出し[ **DisplayConfigGetDeviceInfo** ](https://docs.microsoft.com/windows/desktop/api/winuser/nf-winuser-displayconfiggetdeviceinfo)システムに接続されているアダプターの名前を取得します。

-   表示のコントロール パネル アプレット呼び出し[ **DisplayConfigGetDeviceInfo** ](https://docs.microsoft.com/windows/desktop/api/winuser/nf-winuser-displayconfiggetdeviceinfo)解像度は、ユーザー インターフェイスで強調表示するために接続されている各モニターのネイティブの解像度を取得します。

 

 





