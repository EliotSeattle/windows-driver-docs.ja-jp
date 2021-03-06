---
title: COM インターフェイス設計スキル
description: COM インターフェイス設計スキル
ms.assetid: 3a3adbc2-af6f-4495-8993-fd25d56ffad6
keywords:
- Windows デバイスのテスト フレームワーク WDK、アクションのインターフェイス
- WDTF WDK、アクションのインターフェイス
- アクションは、WDK WDTF をインターフェイスします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 292a179291806c21ccb89f863202ebce6779e6d0
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386249"
---
# <a name="com-interface-design-skills"></a>COM インターフェイス設計スキル


アクションの新しいインターフェイスを作成するときに注意してください、次の機能を使用したオブジェクト モデルを設計する必要があります。

1.  **直感的な**します。 Express の言葉で手動テストします。

2.  **簡単に理解して使用します。** ように簡単に、使用すると、手動テスト担当者は、最上位レベルのシナリオのスクリプトを記述できます。 これらのテスト担当者は、アプリケーションが中断されるので、これを自動的にその知識を深めるにする方法に多くの洞察をある[シナリオ スクリプト](creating-wdtf-scenarios.md)します。

3.  **オブジェクト指向**します。 生産性を向上させるのオブジェクト指向のインターフェイスを確認します。 さいわい、 [WDTF シナリオ モデル](extending-the-framework.md)このルールを中断するが困難です。

4.  **堅牢な**します。 アクションのインターフェイスは再利用性のためのもの、単純なユース ケースだけを準備するので、試してください。

5.  **関連**します。 診断を設計に含めることを確認します。 ユーザーをデバッグ方法の問題、インターフェイスを使用するときに考慮するを再試行してください。 使用してコードをインストルメント化することが役立ちます[WPP ソフトウェア トレース](https://docs.microsoft.com/windows-hardware/drivers/devtest/wpp-software-tracing)します。

 

 




