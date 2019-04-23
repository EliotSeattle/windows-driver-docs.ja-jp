---
title: V4 プリンター ドライバー
description: V4 プリンター ドライバー モデルは、アドレスが既知の問題、バージョン 3 のドライバー モデルがデザインされたときとため自社のプリンターにユーザーが持つエクスペリエンスの質を向上します。
ms.assetid: CB333340-FBA0-4CB4-BAD6-4673B4AC0DF2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ce43f9ca4b8d3ae71c9ef56bc8ae8513186dc50a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56577704"
---
# <a name="v4-printer-driver"></a>V4 プリンター ドライバー


V4 プリンター ドライバー モデルは、アドレスが既知の問題、バージョン 3 のドライバー モデルがデザインされたときとため自社のプリンターにユーザーが持つエクスペリエンスの質を向上します。

**注**  良いいくつかのこのセクションの概念を説明するために、Fabrikam という架空の企業が使用されます。

 

**はじめに**

V4 プリンター ドライバー モデルは、既存の v3 プリンター ドライバー モデルの改良と、ドライバーの開発を向上させる、IT 管理のコストの削減、および新しいシナリオをサポートすることがあります。 V4 印刷ドライバー モデルがなど使い慣れたテクノロジの多くをサポートするために引き続き[XPSDrv](xpsdrv-printer-driver.md)、 [GPD](introduction-to-gpd-files.md)、 [PPD](pscript-minidrivers.md)、[自動構成](printer-autoconfiguration.md)と[Bidi](bidirectional-communication.md)します。 V4 印刷ドライバー モデルには、いくつかの新しい機能拡張ポイントもサポートしています。

V4 印刷ドライバー モデルは、次を含むいくつかの新しいシナリオの最適化も。

-   Windows 8 のシナリオ

    UWP アプリでは、UI の動作とセキュリティ コンテキストに関する新しい設計の考慮事項を提示します。 プリンター ドライバー モデルが必要なこの新しい環境では密接に統合されたサポートを提供するとします。 V4 印刷ドライバー モデルでは、印刷設定をカスタマイズを提供するプリンタの製造元の唯一の方法で発生または UWP アプリでプリンターの通知のエクスペリエンスを提供します。

-   プリンターの共有

    プリンターの共有は、Windows サーバーのキー値提案アイテムです。 簡単に行う共有より効率的なプロセッサ アーキテクチャのドライバーを管理する必要がなくなれば、v4 プリンター ドライバー モデルが設計されました。

-   ドライバーの開発の容易さ

    V4 ドライバーは、XPSDrv アーキテクチャと、バージョン 3 のプリンター ドライバー モデルから既存の開発作業をサポートする必要があります。 および v4 ドライバーを簡単に開発してテストする必要がありますも、します。

**アーキテクチャの概要**

以下は、v4 印刷ドライバーの概要を示したものです。 を除き、レンダリングのフィルターとユーザー インターフェイス アプリケーションでの図は、他のすべての機能ブロックは、Microsoft によって実装されます。 V4 印刷ドライバーが機能拡張のデータ ファイルと JavaScript と大きく依存します。 青い四角形は、v3 ドライバー モデルで使用されていた既存のファイルを表し、緑色のボックス接続する新しい場所を表します。

![v4 印刷ドライバーの高レベルの表現](images/v4driverarch.png)

このセクションでは、v4 プリンター ドライバーの次の側面について説明します。

[V4 プリンター ドライバーの表示](v4-driver-rendering.md)

[V4 プリンター ドライバーの構成](v4-driver-configuration.md)

[V4 プリンター ドライバーのセットアップ](v4-driver-setup.md)

[V4 プリンター ドライバーのユーザー インターフェイス](v4-printer-driver-user-interfaces.md)

[V4 プリンター ドライバーの接続](v4-printer-driver-connectivity.md)

[Visual Studio で v4 プリンター ドライバーをビルドします。](build-a-v4-print-driver-in-visual-studio.md)

 

 



