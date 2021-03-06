---
title: 非同期レンダリング
description: 非同期レンダリング
ms.assetid: f291e416-aaee-4639-9410-6d01b3b02097
keywords:
- ディスプレイ ドライバー WDK Windows 2000、非同期のレンダリング
- 非同期表示 WDK Windows 2000 を表示します。
- レンダリングを非同期 WDK Windows 2000 の表示
- 同期の WDK Windows 2000 の表示
- Windows 2000 の WDK の描画呼び出しの表示の DirectDraw をバッチ処理
- DirectDraw WDK Windows 2000 の表示、バッチを呼び出す
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: eb6d164593f7e2e4bb2fa109f16b17c25c2a0bf1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384632"
---
# <a name="asynchronous-rendering"></a>非同期レンダリング


## <span id="ddk_asynchronous_rendering_gg"></span><span id="DDK_ASYNCHRONOUS_RENDERING_GG"></span>


1 つまたは複数のグラフィックス DDI 描画操作を非同期的に処理し、GDI へのアクセスを使用すると、そのビットマップを提供するためのディスプレイ ドライバー **EngModifySurface**します。 ドライバーは、グラフィックス DDI 描画操作をバッチ処理する場合は、描画のエラーを回避するためにも同期ルーチンを提供する必要があります。

このようなドライバーのいずれかを実装するが[ **DrvSynchronizeSurface** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvsynchronizesurface)または[ **DrvSynchronize** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvsynchronize)同期とルーチンです。 ドライバーがフックされている場合にのみこれらのルーチンのいずれかの GDI 呼び出す[ **EngAssociateSurface**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engassociatesurface)します。 GDI はのみ呼び出す**DrvSynchronizeSurface**でこれらのルーチンの同期の両方をフックするドライバー。

[**DrvSynchronizeSurface** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvsynchronizesurface)ドライバーの同期イベントが発生する理由に関する追加情報を提供します。 これにより、同期のためのパフォーマンスの遅延を削減するドライバーができます。 たとえば、ドライバーどのデバイス ビットマップがアクセラレータのキューでは、その追跡できる可能性がありますからすぐに返す**DrvSynchronizeSurface**指定した画面が現在キューにない場合。

ドライバーはアクティブ化も、同期ルーチンを提供するだけでなく、*時間に基づく*または*プログラム * * メカニズムをフラッシュ*で、次のフラグを設定して、 **flGraphicsCaps2**のフィールド、 [ **DEVINFO** ](https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-tagdevinfo)構造体。

-   GCAPS2\_SYNCTIMER--は定期的に呼び出されるドライバーの同期ルーチンと、このフラグを設定します。 グラフィックス DDI 呼び出しのバッチのドライバーでは、このフラグを指定する必要があります。 これにより、これらのドライバーは、lag ソフトウェア カーソルの移動または描画するには、急激な増加で実行などの問題を回避します。

    GDI は、DSS を渡します\_タイマー\_イベント フラグを[ **DrvSynchronizeSurface** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvsynchronizesurface)定期的なイベントのため、この同期ルーチンが呼び出されたとき。

-   GCAPS2\_SYNCFLUSH--呼び出されるたびに、ドライバーの同期化ルーチンを設定するには、このフラグと、Microsoft Win32 **GdiFlush** API が呼び出されます。 非同期のレンダリングを実行するドライバーは、このフラグを指定および同期化ルーチンを提供する必要があります。

    GDI は、DSS を渡します\_フラッシュ\_イベント フラグを[ **DrvSynchronizeSurface** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvsynchronizesurface)フラッシュ ベースのイベントのため、この同期ルーチンが呼び出されたとき。 に関する詳細については、Microsoft Windows SDK ドキュメントを参照してください**GdiFlush**します。

### <a name="span-idlimitationsonbatchingdirectdrawdrawingcallsspanspan-idlimitationsonbatchingdirectdrawdrawingcallsspanspan-idlimitationsonbatchingdirectdrawdrawingcallsspanlimitations-on-batching-directdraw-drawing-calls"></a><span id="Limitations_on_Batching_DirectDraw_Drawing_Calls"></span><span id="limitations_on_batching_directdraw_drawing_calls"></span><span id="LIMITATIONS_ON_BATCHING_DIRECTDRAW_DRAWING_CALLS"></span>DirectDraw 描画呼び出しをバッチ処理に関する制限事項

ドライバーは、DirectDraw 宛先表面が表示される画面の描画呼び出しをバッチことはありません必要があります。 使用して画面を完了したフレームの更新のウィンドウの DirectX アプリケーションでこのような状況が発生した[ *DdBlt* ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_blt)され、したがってすぐに表示されます。 この制限は、非同期的に反転する可能性がありますの DirectDraw のビデオ ポート画面にも適用されます。

 

 





