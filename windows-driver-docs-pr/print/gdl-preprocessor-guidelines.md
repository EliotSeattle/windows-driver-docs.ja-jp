---
title: GDL プリプロセッサ ガイドライン
description: GDL プリプロセッサ ガイドライン
ms.assetid: dc8450ca-cacc-458c-a05b-8566d04d8bae
keywords:
- プリプロセッサ ディレクティブ WDK GDL、ガイドライン
- WDK GDL、ソース ファイルのプリプロセッサ ディレクティブのディレクティブ
- ソース ファイル WDK GDL、プリプロセッサ ディレクティブ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ec04844e5ff0377c384b21363e3e5101723a19f6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537254"
---
# <a name="gdl-preprocessor-guidelines"></a>GDL プリプロセッサ ガイドライン


GDL プリプロセッサ ディレクティブを記述するときは、次のガイドラインを使用します。

予期しない結果を防ぐためには、GDL ファイルの作成者はプリプロセッサ シンボルおよびプレフィックスを定義するときに、次のガイドラインを確認する必要があります。

決して未定義状態になシンボルを明示的に定義しなかった、ファイルには、ファイルが終了する前に常に、ファイルで定義されている任意のシンボルを未定義です。 つまり、常にそれらを検出すると、シンボルおよびプレフィックスのスタックのままにします。 このガイドラインに準拠している場合ことがあります、プリプロセッサに関連する名前空間の競合。

GDL パーサーのインターフェイスは、ルート GDL ファイル事前処理される GDL テキストの任意のサイズのフラグメントを挿入するクライアントを有効になります。 この機会には、パーサー GDL ファイルの該当セクションを処理するために必要なすべてのプリプロセッサ シンボルを定義するクライアントが有効になります。 このフラグメントには、他 GDL 標準テンプレートが含まれる場合がありますも、標準マクロを定義することもできます。

**注**  ファイルが含まれる行で、すべてのプリプロセッサ シンボルと、インクルード ファイルの前処理中に定義されているホストで定義されているプレフィックスのままです。 ファイルが処理されると、プリコンパイル済み、まったく新しい解析と環境を作成します。 したがって、すべてのシンボルとプレフィックスが既定値に返されます。 処理されるファイルとしてプリコンパイル済みしたりしないでください外部依存関係を持つプリプロセッサ シンボルの定義されているファイルをホストします。

 

**注**  プリプロセッサ ディレクティブとマクロは影響を受けませんスイッチ/case 構成体によってスイッチ/ケース構造の前に、ディレクティブは個別に評価されるためです。

 

論理演算子は GDL プリプロセッサ ディレクティブではサポートされていません。 このような状況を解決する方法については、次を参照してください。 [GDL プリプロセスでの論理演算子を含む問題](problems-with-logical-operators-in-gdl-preprocessing.md)します。

 

 



