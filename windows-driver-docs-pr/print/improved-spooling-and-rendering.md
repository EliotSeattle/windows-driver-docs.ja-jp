---
title: 強化されたスプールとレンダリング
description: 強化されたスプールとレンダリング
ms.assetid: 0e385282-fbc8-4c4b-9070-19ee8290ddd6
keywords:
- XPSDrv プリンター ドライバー WDK、スプール
- XPSDrv プリンター ドライバー WDK、レンダリング
- XPS スプール ファイル WDK XPSDrv
- WDK のスプール ファイルを印刷します。
- プラグインの WDK の印刷、XPSDrv のレンダリング
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1fd249ee27c4d226fe45d0f45c1b61af2c6176a7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390579"
---
# <a name="improved-spooling-and-rendering"></a>強化されたスプールとレンダリング


XPS 印刷パスでは、エンドユーザーが XPSDrv プリンター ドライバーに印刷と XPS のスプール ファイル形式で XPS ドキュメントをスプールしてスプーラの効率性が向上します。 XPS ドキュメントのファイル形式は、XPS のスプール ファイル形式と同じであるため、スプール処理が効率化され、ドキュメントをスプールする前に、拡張メタファイル (EMF) データ ファイルなど、中間スプール ファイルを生成する必要があります。 スプール ファイルのサイズより小さい、XPS 印刷パス アプリケーション ネットワーク トラフィックの削減や印刷のパフォーマンスを向上させることができます。

EMF は、一連のサービスを表示するため、GDI への呼び出しを必要とする GDI 呼び出しとしてアプリケーションの出力を表すクローズ形式です。 EMF とは異なり XPS スプール形式に XPSDrv ドライバーが対象とする場合は、さらに解釈を必要とせず、ビジュアルの実際の出力を表します。 GDI ベースの印刷ドライバーがデータを必要とし、色空間の変換中、XPSDrv プリンター ドライバーはスプール ファイル内のデータを直接操作し、これらの変換を回避します。

XPS ドキュメントを使用するか、ターゲットに XPSDrv ドライバーときに通常、スプール ファイルのサイズが削減されます。 スプール ファイルが大きく、大規模なベクトル コンテンツにおけるデバイス フォントに依存するファイルとファイルがありますが、スプール ファイルは大幅に小さくなりますが一般にします。

スプール ファイルのサイズは、変換プロセスでいくつかの最適化により低減されます。

-   すべてのフォントのサブセットのフォント。 出力が処理された後、ファイル内のフォントに使用される文字のみが含まれています。 この最適化は、ドキュメント、特に東アジア フォントのセットを使用するドキュメントのスプール ファイルのサイズを大幅に減ります。

-   ロゴとイメージ ファイルを含む、共通のリソースの id です。 変換プロセスでは、イメージは、ドキュメント内で複数回使用し、そうである場合は、XPS のスプール ファイルの共有リソースを作成するかどうかを識別します。 この最適化では、同じロゴや背景を使用して、各スライドを PowerPoint ファイルなどのグラフィックを多用するドキュメントのスプール ファイルのサイズを大幅に短縮できます。

-   ZIP 圧縮します。 ZIP 圧縮は、XPS スプール ファイル形式 (XPS ドキュメント形式) の一部として実装されます。 この最適化では、スプール ファイルのサイズを減らします。

これらの最適化 XPS ドキュメントをいつでも実行または XPS スプール ファイルが作成されます。

 

 




