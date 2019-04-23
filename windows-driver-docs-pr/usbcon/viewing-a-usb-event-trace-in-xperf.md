---
Description: This topic describes how to view a USB event trace in Xperf.
title: Xperf での USB イベント トレースの表示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ce0ea8ac02a35e7684a820d36c838c792f9b4638
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574353"
---
# <a name="viewing-a-usb-event-trace-in-xperf"></a>Xperf での USB イベント トレースの表示


このトピックでは、Xperf で USB イベントのトレースを表示する方法について説明します。

パフォーマンスとタイミングの問題を分析するには、USB イベント トレースを表示するのに Xperf を使用できます。 たとえば、usb.etl の名前は、イベント トレース ログ ファイルがあり、Xperf ツールをダウンロードした場合、トレースを分析するには、次のコマンドを発行します。

```cpp
xperf usb.etl
```

Xperf は、グラフィカルな形式で、イベントのビューを表示します。 初期ビューは、各ダイヤモンドがこのイメージに 1 つまたは複数のイベントを表しますタイムライン ビューです。 このひし形は、イベント プロバイダーに応じて色分けです。

![windows パフォーマンス アナライザー - xperf](images/xperf.png)

タイムライン ビューは、クラスターのイベント アクティビティをグラフィカルに表示します。 グラフィカル ビューで 1 秒間隔で USB 大容量記憶装置デバイスのデバイスの概要イベントをこの例のトレースの後に発生した USB 転送要求としてイベント アクティビティの定期的な性質をわかりやすくなります。

セクションでは、タイムラインの間でマウス ポインターを移動し、ズーム インできます。 この図は、トレースの最初に発生するデバイスの概要イベントへのズームインします。

![windows パフォーマンス アナライザー - xperf](images/xperf1.png)

この図のように、トレース全体または選択した期間だけ、スプレッドシート形式で、イベントの概要テーブルを表示できます。

![windows パフォーマンス アナライザー - xperf](images/xperf2.png)

概要テーブルを表示するで右クリックし、**汎用イベント**画面し、選択**概要テーブル**します。

イベントの概要テーブルは、それらとビューのピボット新しい列の順序に基づいたイベントの順序を変更する列をドラッグできるので、非常に強力なビューです。 目的の項目に注目することを有効にするのには展開したり折りたたんだり同一の並べ替え順序を持つ項目。

Xperf より読みやすい形式で、Netmon が USB イベント データを表示することもありますが、ネットワーク モニター、Xperf タイムラインおよびテーブル ビューが不足しています。 一定期間には、トレースのイベントを分析するには、Xperf、ネットワーク モニター間で切り替えることができます。

## <a name="related-topics"></a>関連トピック
[Windows のイベント トレースは USB](usb-event-tracing-for-windows.md)  
[Xperf を使用して USB ETW を使用しました。](using-xperf-with-usb-etw.md)  


