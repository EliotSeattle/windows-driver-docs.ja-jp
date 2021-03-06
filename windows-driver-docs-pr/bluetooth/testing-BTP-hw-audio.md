---
title: Microsoft Bluetooth テストプラットフォーム
description: Bluetooth テストプラットフォーム (BTP) でサポートされているハードウェア (オーディオ)。
ms.assetid: a6beeecb-5967-4e08-bfe2-b8aae26861ad
ms.date: 2/14/2020
ms.localizationpriority: medium
ms.openlocfilehash: 9d7a525e57dcee8187c3c98194a023e10ea85379
ms.sourcegitcommit: d03c24342b9852013301a37e2ec95592804204f1
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/21/2020
ms.locfileid: "77528912"
---
# <a name="audio-capable-peripheral-radios"></a>オーディオ対応周辺機器無線 #

Bluetooth テストプラットフォーム (BTP) Traduci ボードには、任意のラジオモジュールと通信するための12ピンコネクタが必要です。 ここに一覧表示されているオーディオラジオとテクニカルは、ラジオモジュールを受け取り、必要な pin を必要な12ピンレイアウトに分解します。

| ラジオ | 機能 | パラメーター |
| --- | --- | --- |
| RN52 | 基本料金 (BR) オプション | rn52 (例 RunPairingTests rn52) |

## <a name="audio-sled-rn52-radio"></a>オーディオスレッド (RN52 radio) ##

RN52 は、スピーカーやヘッドセットなどのオーディオ周辺機器として動作することができる、ロービングネットワークからの基本料金 (BR) ラジオです。 現在、今後の BTP オーディオテストのサポートが予定されています。 詳細については、「RN52」 ([**マイクロチップ**](https://www.microchip.com/wwwproducts/en/RN52)) のページを参照してください。 このスレッドでは、無線からのオーディオ出力データを分割し、検証を支援するために Traduci 上のオーディオコーデックとオーディオ処理 FPGA にルーティングします。

### <a name="rn52-radio"></a>RN52 Radio ###

![RN52 ラジオの写真](images/RN52.png)

### <a name="rn52-radio-on-btp-compatible-sled"></a>BTP 互換スレッドでの RN52 Radio ###

![スレッドの RN52 ラジオの写真](images/Traduci_and_RN52.jpg)

> [!NOTE]
> RN52 radio は、"JA" というラベルが付いた Traduci board 12 ピンのポートに**のみ**接続できます。

- ソフトウェアを構成する AT コマンドを使用した UART データ接続
- SPP、A2DP、HFP、および AVRCP プロファイルをサポートします。
- バージョン3.0 オーディオモジュール
- 完全に認定されたクラス 2 BR Bluetooth 2.1 + EDR
- 小さなフォームファクター、低電力、surface マウントモジュール
