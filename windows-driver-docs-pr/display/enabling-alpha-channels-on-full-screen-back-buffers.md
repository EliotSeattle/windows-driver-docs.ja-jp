---
title: 全画面バック バッファーでのアルファ チャネルの有効化
description: 全画面バック バッファーでのアルファ チャネルの有効化
ms.assetid: 9d922464-fb1b-459b-9363-61afff7c51e3
keywords:
- DirectX 8.0 リリース ノート WDK Windows 2000 の表示、全画面表示のアルファ チャネルのバック バッファー
- チェーン WDK DirectX 8.0 の反転
- プライマリ フリッピング チェーン WDK DirectX 8.0
- 全画面表示のフリッピング チェーン WDK DirectX 8.0
- アルファ チャネル WDK DirectX 8.0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bd06402e11b1e90d78297882c220ae407da938c4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385611"
---
# <a name="enabling-alpha-channels-on-full-screen-back-buffers"></a>全画面バック バッファーでのアルファ チャネルの有効化


## <span id="ddk_enabling_alpha_channels_on_full_screen_back_buffers_gg"></span><span id="DDK_ENABLING_ALPHA_CHANNELS_ON_FULL_SCREEN_BACK_BUFFERS_GG"></span>


DirectDraw DDI では、プライマリのフリッピング チェーンの作成には組み込みのピクセル形式がありません。 そのため、このチェーン内のサーフェスになる表示モードのピクセル形式です。 たとえば、32 bpp のモードで作成されたプライマリ フリッピング チェーンは、D3DFMT\_X8R8G8B8 形式。

全画面表示の多くのアプリケーションでは、このようなチェーンが作成されます。 チェーンのバック バッファーは、D3DRS のアルファ チャネルがあるないため\_ALPHABLENDENABLE 状態を表示して、宛先表面に関連付けられている blend レンダリング状態が定義されて適切です。 DirectX 8.1 では、Direct3D ランタイムがこれらのサーフェスのピクセル形式でアルファ チャネルを持つサーフェスの全画面表示のフリッピング チェーンを作成するアプリケーションの要求のドライバーを通知するために使用する新しい機能について説明します。

この機能のサポートを示すために、ドライバーは、D3DCAPS3 を設定する必要があります\_アルファ\_全画面表示\_反転\_または\_破棄ビット (で定義されている、 *d3d8caps.h*ファイル) で**Caps3** D3DCAPS8 構造体のメンバー。 ドライバーがへの応答で D3DCAPS8 構造体を返します、 **GetDriverInfo2** 」の説明に従ってクエリ[DirectX 8.0 スタイル Direct3D の機能を Reporting](reporting-directx-8-0-style-direct3d-capabilities.md)します。 このクエリのサポートについては、「[サポート GetDriverInfo2](supporting-getdriverinfo2.md)します。

この機能のサポートが確認された後、ドライバーを受信できます[ *DdCreateSurface* ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff549263(v=vs.85)) 、DDSCAPS2 で呼び出しを\_ENABLEALPHACHANNEL (で定義されている、 *ddraw.h*ファイル) でビットを設定、 **dwCaps2**のメンバー、 [ **DDSCAPS2** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff550292(v=vs.85))構造体。 このビットがプライマリ フリッピング チェーンの一部であるか、スタンドアロンのバック バッファー上にあるサーフェスを作成する設定のみです。

ドライバーは、このビットが検出される場合、表示モードの形式が、表示モードの形式とアルファいないサーフェスが取るドライバーを決定します。 たとえば、32 bpp のモードでこのようなサーフェイス与える必要があります、D3DFMT\_A8R8G8B8 形式。

この機能は、DirectX 8.1 ランタイムをインストールして Windows 2000 オペレーティング システムのバージョンと Windows XP およびそれ以降のバージョンで使用できます。

 

 





