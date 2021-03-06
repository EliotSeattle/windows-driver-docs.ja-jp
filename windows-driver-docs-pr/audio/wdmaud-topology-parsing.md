---
title: WDMAud トポロジ解析
description: WDMAud トポロジ解析
ms.assetid: 8aa3e2e8-c9a2-4c3e-94b1-44a0dc218bf3
keywords:
- WDMAud トポロジ解析 WDK オーディオ
- トポロジ解析 WDK オーディオ
- ソース ミキサー行 WDK オーディオ
- 移行先ミキサー行 WDK オーディオ
- 出力先ミキサーの行を解析
- 仮想 sum WDK オーディオ
- 変換ノード WDK オーディオ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 90442e6e4e21a17a920228ff47a32c97cb49ebf5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354095"
---
# <a name="wdmaud-topology-parsing"></a>WDMAud トポロジ解析


## <span id="wdmaud_topology_parsing"></span><span id="WDMAUD_TOPOLOGY_PARSING"></span>


[WDMAud システム ドライバー](user-mode-wdm-audio-components.md#wdmaud_system_driver)ソース ミキサーの行を解析前に、まず移行先ミキサーの行を解析します。 WDMAud が出力先の行を解析して順序は、逆 SysAudio が行を検出したのです。 たとえば、上位の番号付きのピンが最初に解析されます。 解析、直接の親、暗証番号 (pin) を開始し、アップ ストリームの方向に移動します。 各ノードは、パーサーは、次の終了条件のいずれかが検出するまで、これらの規則に従って変換されます。

-   解析中の現在のノードは、合計ノードです。

-   現在のノードは、MUX ノードです。

-   現在のノードには、複数の親があります。

MUX と合計のノードが、*クラシック ターミネータ*変換先の行のできます。 合計ノードは、すべてのコントロールを生成しません。 MUX ノードは、MUX によって制御されるソース行のそれぞれへの参照を含んでいる宛先行に MUX コントロールを生成します。

複数の親が検出された場合、解析はすぐに終了します。 ミキサー行ドライバーは、複数の入力を結合して形成されたは"仮想 sum"として、この条件を解釈します。

返される名前に由来変換先の行の名前、 [ **KSPROPERTY\_PIN\_名前**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-pin-name)その pin のプロパティ。

変換先の行のすべてのコントロールを翻訳すると後のソース行を変換する WDMAud を開始します。 ここでも、WDMAud がこれらの行を解析し、順序は SysAudio がそれらにクエリの順序の逆です。 また、ソース行が解析されます方向は、逆に、出力先の行が解析されます。 WDMAud、暗証番号 (pin) から開始し、次の終了条件のいずれかが検出されない限り、ダウン ストリームの方向に続行して各行を解析します。

-   パーサーは、出力先の行を検索します。

-   出力先の行に変換されている現在のノードが属しています。

-   現在のノードは、合計ノードです。

-   現在のノードは、MUX ノードです。

出力先の行が属するソース行の解析中に、MUX が発生したときに、コントロールに変換されます。 ただし、後で、移行先の行に格納されている MUX 内の行番号を更新するプレース ホルダーとしてのみ使用がされます。 最後の行番号はまだ使用可能なこの時点では、ため、プレース ホルダーが必要です。

MUX と合計のノードの両方の終了ソース行。そのため、すべてのノード、合計または MUX と別の合計または間 MUX は翻訳されません。

## <a name="span-idnotesspanspan-idnotesspanspan-idnotesspannotes"></a><span id="Notes"></span><span id="notes"></span><span id="NOTES"></span>ノート


1.  MUX の線名は、合計または MUX ノードから、MUX に行の供給する場合を除く、行の暗証番号 (pin) の名前から派生されます。 その場合は、行の名前は、MUX または合計のノードの名前です。 ミキサーのドライバーを検出されると、これが、合計または MUX ノードの名前を持つ仮想ミキサーの行を構築および合計または MUX と MUX の間のすべてのコントロールに変換されます。

2.  A*分割*トポロジでは、ノードが複数の 1 つの子がある場合。 これは、ピンが 1 つは 2 つの独立した宛先にルーティングしますが、ボリュームや、ミュートなどのいくつかの一般的なコントロールを共有するときに便利です。 分割が発生すると、いつでも WDMAud ドライバーは、新しい行と分割までのすべてのコントロールが解析された重複部分を作成します。 ソース行を終了する合計ノードが発生した後でも、分割が見つかるたびに無条件で発生します。

 

 




