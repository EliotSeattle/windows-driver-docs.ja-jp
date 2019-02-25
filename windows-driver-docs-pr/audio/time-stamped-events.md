---
title: イベントのタイムスタンプ
description: イベントのタイムスタンプ
ms.assetid: 8db89e31-bfd7-48cf-9eb2-12ac7784cc31
keywords:
- シンセサイザー WDK のオーディオ、タイムスタンプ
- タイム スタンプ WDK オーディオ
- イベントのタイムスタンプ付きの WDK オーディオ
- イベントの WDK オーディオ
- PCM バッファー WDK オーディオ
- WDK オーディオ、時計の待機時間
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f68ed0b65b1cae533c3ee4b4e5bca676a3bbd123
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537247"
---
# <a name="time-stamped-events"></a>イベントのタイムスタンプ


## <span id="time_stamped_events"></span><span id="TIME_STAMPED_EVENTS"></span>


シンセサイザーのタイミングの全体像は、再生する必要があるタイミングを正確にメモを送信するのではなく各メモ時刻スタンプされ、バッファーに配置です。 このバッファーが処理され、タイムスタンプで指定されている時間 (ミリ秒) の 2 つ内で再生します。 (タイミング解像度は 100 ナノ秒では、これは説明このディスカッションの時間単位をより便利なは、ミリ秒単位の観点から。)

待機時間の時計をシステムに、待機時間がわかっているため、イベントのタイムスタンプ、適切な時に再生するバッファーで待機しているではなくだけをキューにイベントを削除でき、待ち時間が短いことを期待しています。

マスターのクロックの実装を COM [ **IReferenceClock** ](https://msdn.microsoft.com/library/windows/desktop/dd743269)インターフェイス (Microsoft Windows SDK のドキュメントで説明)。 すべてのシステム上のデバイスは、この参照の時刻を使用します。

Microsoft の波のシンクの実装では、20 ミリ秒ごとのスリープ状態のスレッドを作成します。 スレッドのジョブの方法では、別のバッファーを作成し、DirectSound をします。 そのバッファーを作成するには、シンセサイザーを呼び出すし、指定された量の音楽データを表示するために尋ねます。 入力を求められたら量は、正確に 20 ミリ秒にする可能性があるスレッドが起動すると、実際の時間によって決まります。

シンセサイザーに渡される内容が実際には、単に、PCM バッファーに書き込むデータの量を指定する長さのパラメーター データの書き込みを開始する位置のメモリ内の場所にポインターです。 シンセサイザーはこのバッファーに PCM のデータを記述し、指定された時間まで入力します。 つまり、レンダリング開始アドレスから指定された長さに到達するまで。 メモリ ブロックは (つまり、既定のケース) DirectSoundBuffer を指定できますが、DirectShow グラフまたは wave シンクによって定義されたその他のいくつかのターゲット可能性があります。

PCM バッファーは概念的には重要です (つまり、絶えずループしている)。 シンセサイザーには、バッファーの連続するスライスにサウンドを記述する 16 ビットの数値が表示されます。 スライスのサイズは若干異なります、スレッドが起動するたびに、シンクは 20 ミリ秒ごとに正確を起こすことはできませんのでです。 スレッドのウェイク アップは、たびに再生されるように catch スリープ状態に戻る前にバッファーを進行がどの程度を判断します。

シンセサイザー ポート ドライバー自体には、アプリケーションの観点から、 [ **IDirectMusicSynth::GetLatencyClock** ](https://msdn.microsoft.com/library/windows/hardware/ff536536) wave シンクからクロックを取得する関数。 これは、2 つのクロックがあります。

-   Wave シンクを含むすべてのユーザーがリッスンするマスター クロック。

-   待機時間の時計を提供する DirectMusic ポートとして、アプリケーションによって認識されるように wave シンクによって実装される待機時間のクロック。

つまり、アプリケーションは、待機時間の時計を求めるプロンプトが wave シンクではなく、DirectMusic ポートの抽象化から予定されていると、クロックが表示されます。

この待機時間のクロックによって返される時間は、バッファーは、表示できる最も早い時刻をバッファー内の時点までのシンセサイザーのレンダリングが既にためです。 シンセサイザーは、その最後の書き込みに小さなバッファーをレンダリングするが場合、待機時間を小さくするとも。

そのため、呼び出しのシンク、wave [ **IDirectMusicSynth::Render** ](https://msdn.microsoft.com/library/windows/hardware/ff536541)シンセサイザーでバッファーを表示してが入力されることを要求するレンダリング データ。 次の図に示すように、シンセサイザーの実行時間すべてタイムスタンプ付きのイベントの結果としてに付属している[ **IDirectMusicSynth::PlayBuffer** ](https://msdn.microsoft.com/library/windows/hardware/ff536540)関数呼び出し。

![タイムスタンプ付きのメッセージのキューを示す図](images/dmevents.png)

各入力バッファーには、メッセージ タイムスタンプにはが含まれています。 これらのメッセージの各は、そのタイムスタンプで指定した時間にバッファーに表示されるキューに置かれます。

このモデルの重要な点の 1 つは、タイムスタンプ以外の特定の順序がないことです。 レンダリングの前に、いつでも、キューに追加できるように、これらのイベントをストリーミングします。 すべては、イベント ベース時間に関してです。 たとえば、400 時間単位での参照時刻がいる場合は、し、タイムスタンプ 400 の時間に発生するすべてが発生しているようになりました。 タイムスタンプ今から 10 個のユニットが発生するイベントについては 410 では発生します。

 

 



