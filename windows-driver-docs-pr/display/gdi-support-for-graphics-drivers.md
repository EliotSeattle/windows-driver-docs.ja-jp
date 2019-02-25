---
title: GDI グラフィックス ドライバーのサポート
description: GDI グラフィックス ドライバーのサポート
ms.assetid: ef42cda0-106f-4c1b-babc-29a1070e2a2f
keywords:
- GDI WDK Windows 2000 の表示、参照
- グラフィックス ドライバー WDK Windows 2000 の表示、参照
- WDK GDI を描画するを参照します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f91bc718ff8504486ead47cbaf2dba0206537531
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536559"
---
# <a name="gdi-support-for-graphics-drivers"></a>GDI グラフィックス ドライバーのサポート


## <span id="ddk_gdi_support_for_graphics_drivers_gg"></span><span id="DDK_GDI_SUPPORT_FOR_GRAPHICS_DRIVERS_GG"></span>


このセクションでは、Microsoft Windows NT ベースのオペレーティング システムのグラフィックス デバイス インターフェイス (GDI) について説明します。 GDI はグラフィック ドライバーを提供するサポートし、詳しく説明します。

このセクションでは GDI への参照はカーネル モードの GDI; への暗黙の参照Microsoft Win32 GDI は明示的に識別されます。 カーネル モードの GDI は、グラフィックス エンジンとも呼ばれます。

GDI 関数と構造の参照が記載されて、[デバイスの表示のリファレンス](https://msdn.microsoft.com/library/windows/hardware/ff554046)セクション。 ほとんどの GDI 関数宣言と構造体の定義が記載*Winddi.h*します。 ディスプレイ ドライバーでは、Microsoft DirectDraw ヒープ マネージャーの機能が宣言されている*Dmemmgr.h*します。 両方のファイルは、Windows Driver Kit (WDK) に付属しています。

 

 




