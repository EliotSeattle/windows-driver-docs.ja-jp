---
title: パッケージ対応印刷ドライバー
description: パッケージ対応印刷ドライバー
ms.assetid: f2ab38b9-410c-4dd8-bb81-4a8e0e48317a
keywords:
- パッケージに対応した印刷ドライバー WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 54292a6c1d83ab6e21d95a82adcfe60a23863088
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63353701"
---
# <a name="package-aware-print-drivers"></a>パッケージ対応印刷ドライバー


パッケージに対応した印刷ドライバーでは、ポイントをサポートし、パッケージを使用した印刷、INF ファイルにエントリがあります。 これらのエントリ ポイントを行えるようにし、他のファイルに印刷ドライバーの依存関係の対応するために印刷をでは、わずかなものにでき、ドライバー パッケージの性質に依存することができます。

-   ドライバー パッケージ内のファイルが一意で、その他のプリンター ドライバー パッケージに記載されていない場合を使用して、 **PackageAware** INF キーワード。

-   ドライバー パッケージ内のファイルは他の印刷ドライバー パッケージ内のファイル共有されている場合。
    -   共有のファイルを個別に移動[コア ドライバー](writing-core-drivers.md)します。
    -   使用して、 **PackageAware**キーワードと**CoreDriverDependencies**キーワードをこのコアの個別のドライバーを参照してください。 これは、リモート インストール シナリオではさまざまなファイル バージョンの競合を回避する必要があります。

このセクションの内容:

[ファイルを共有しない印刷ドライバーをパッケージに注意してください。](package-aware-print-drivers-that-do-not-share-files.md)

[ファイルを共有するプリンター ドライバーをパッケージに注意してください。](package-aware-print-drivers-that-share-files.md)

 

 




