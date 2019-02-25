---
title: 一般的なコントロールのノードとフィルター
description: 一般的なコントロールのノードとフィルター
ms.assetid: 33e0605b-0fd1-4506-a48b-427976e94dfc
keywords:
- WDK BDA のノードを制御します。
- WDK BDA ノード
- ネットワーク プロバイダーは、WDK BDA をフィルター処理します。
- チューナー制御ノード WDK BDA
- 制御ノード WDK BDA 復調器します。
- キャプチャ フィルター WDK BDA
- PID フィルター コントロール ノード WDK BDA
- IPSink WDK BDA
- NDISIP WDK BDA
- ブロードキャスト ドライバー アーキテクチャ WDK AVStream、制御ノード
- BDA WDK AVStream、制御ノード
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5548cbfb31875ed0c5cdad67b1895ce00a87124e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530626"
---
# <a name="common-control-nodes-and-filters"></a>一般的なコントロールのノードとフィルター





制御ノードとの図に示すようなフィルターの種類、[制御ノード、フィルター、およびハードウェア](control-nodes--filters-and-hardware.md)セクションに共通のデジタル衛星、地上波を受信して、ブロードキャストのケーブルを接続します。 ただし、他のノードの種類とはブロードキャストのメディアとデバイスも、さまざまなフィルターを作成できます。 各制御ノード必要がある 1 つの BDA デバイス フィルターに対応していないことに注意してください。 場合によっては、1 つの BDA デバイス フィルターが 1 つ以上のコントロールのノードをカプセル化できます。

次の一覧には、制御ノードおよびブロードキャストのアーキテクチャで一般的に見られるフィルターについて説明します。

<a href="" id="network-provider"></a>**ネットワーク プロバイダー**  
A*ネットワーク プロバイダー フィルター* (または*ネットワーク プロバイダー*) デジタル テレビ信号を BDA デバイス経由にルーティングします。 さまざまな放送のプロバイダーは、--サテライト、ケーブル、アンテナの 3 つの基本的なネットワーク型に対するデジタル テレビ信号を送信するようにします。 ATSC、DVB-S、DVB-C、DVB-T などの複数の標準により定義された形式でこれらのデジタル信号が送信されます。 BDA デバイスは、受信し、これらのデジタル信号を管理します。

ネットワーク プロバイダー:

-   実際に通過したデータのないことですが、フィルターのグラフでソース フィルターです。

-   ネットワークの種類ごとに存在するか、新しいネットワークの種類に対して作成できます。

-   グラフの作成プロセスに参加します。

-   このようなフィルターを初期化する BDA ミニドライバーのプロパティとメソッドのセットによって、グラフ内の他のフィルターと通信します。

各ネットワーク プロバイダーには、その関連付けられているネットワークの種類の構成を別のグラフを構築できます。 アプリケーションでは、情報を BDA ミニドライバーに渡されますネットワーク プロバイダーに要求を調整するを渡します。 詳細については、Microsoft Windows SDK ドキュメントのブロードキャストのアーキテクチャのセクションを参照してください。

<a href="" id="tuner"></a>**チューナー**  
この制御ノードは、トランスポート ストリームを実行する特定の頻度をフィルター処理します。 単独、またはその他の制御ノードと共に、フィルター内で表示されることができます。

<a href="" id="demodulator"></a>**復調器**  
アナログ信号をデジタル ビット ストリームに変換するコントロールのノードです。 単独、またはその他の制御ノードと共に、フィルター内で表示されることができます。

<a href="" id="capture"></a>**キャプチャ**  
ホストのメモリにデータを移動するフィルター。

<a href="" id="pid-filter"></a>**PID フィルター**  
コントロールのノードで、トランスポート ストリームから 1 つまたは複数の基本データ ストリームを選択します。 これは、デマルチプレクサーの主な機能です。 単独、またはその他の制御ノードと共に、フィルター内で表示されることができます。

<a href="" id="mpe-parser"></a>**MPE パーサー**  
IP データは、mpeg-2 プライベート セクションを含むストリームを解析するフィルター。

<a href="" id="ipsink"></a>**IPSink**  
IP パケットを受け入れるようにデータをサンプリングし、NDIS TCP/IP スタックにデータを転送するフィルター。

<a href="" id="ndisip"></a>**NDISIP**  
NDIS ミニポート ドライバーの IPSink フィルターが渡されるデータ用のネットワーク アダプターの受信側として機能します。

**注**  以降 Windows Vista では、IPSink フィルターはサポートされていません。

 

 

 



