---
title: weave メソッド
description: weave メソッド
ms.assetid: d35a08b6-7221-4e1c-895f-446f23096519
keywords:
- DirectX VPE サポート WDK DirectDraw、インターリーブのビデオを表示します。
- VPEs WDK DirectDraw を描画、ビデオがインターリーブを表示します。
- DirectDraw VPEs WDK Windows 2000 の表示、インターリーブのビデオを表示します。
- 拡張機能のビデオ ポート WDK DirectDraw、インターリーブのビデオを表示します。
- VPEs WDK DirectDraw、インターリーブのビデオを表示します。
- インターリーブのビデオを表示します。
- インタリーブされたビデオは、WDK のビデオ ポートの拡張機能を表示します。
- WDK DirectDraw を一元管理します。
- デインター レース WDK ビデオ ポートの拡張機能
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 803c33ccecd4a3be5db9938237c82d29cb1d23e4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391176"
---
# <a name="weave-method"></a>weave メソッド


## <span id="ddk_weave_method_gg"></span><span id="DDK_WEAVE_METHOD_GG"></span>


Weave メソッドは、オーバーレイの画面にインター レースのフィールドをインターリーブするハードウェアのビデオ ポートを使用してデータを表示し、同時に両方のフィールドを示します。 ただし、weave アルゴリズムは、でした。 プロセスがモーションの成果物が表示されます。 Weave アルゴリズムも 3:2 パターンを認識する MPEG ドライバーに依存し、カーネル モードのビデオ トランスポートで関数を使用してを元に戻します。 カーネル モードのビデオ トランスポートは、同じフレームから来るようにすべてのフィールドのペアの原因と、繰り返しフィールドを破棄するビデオ ポートに、ハードウェアにあります。 フィルムを使用してサンプリングされた最初のと同様、1 秒あたり 24 のフレームに表示される完全なフレームのビデオになります。

各ソース フィルム フレームは、2 つまたは 3 つのフィールドで、NTSC 信号で表現されます。 これは、A フレームを構成する 2 つの A フィールドように見えることができます。 各シーケンスのフィルムの 4 つのフレームは、5 つのテレビ フレームに変換されます。 A、B、C および D のフィルムのフレームが AA、BB、BC、CD、および DD. フィールド パターンを持つ 5 つのテレビ フレームになります ときに、繰り返し\_MPEG ストリームでは、このパターンのエンコードが使用されるフィールドのフラグ、MPEG データ ペイロードには 4 つだけのフレームが含まれていますが、5 つのテレビのすべてのフレームのフィールドの順序が保持されます。

Weave メソッドは、1 秒あたり 24 プログレッシブ フレームを生成し、インター レースされたソースから完全に垂直方向の解像度を保持します。 ビデオは、3:2 プルダウンを使用してフィルムから作成した場合、またはモーションが含まれていない場合は、weave、プログレッシブのモニターの手頃な表示を最適なプロセスです。

 

 





