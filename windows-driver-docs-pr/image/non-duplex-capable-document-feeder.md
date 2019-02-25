---
title: 二重モード対応のドキュメント フィーダー付き
description: 二重モード対応のドキュメント フィーダー付き
ms.assetid: e22ec1bb-623e-45c6-88f4-d3b6a45fa175
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8b19996c226a8fd2a5b8b08f40410ad9e9fce8a1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553865"
---
# <a name="non-duplex-capable-document-feeder"></a>二重モード対応のドキュメント フィーダー付き





次の図は、単純な (非双方向) ドキュメント フィーダーのスキャンをサポートしているフラット ベッド スキャナーの WIA 項目のツリーを示しています。

![非双方向ドキュメント フィーダー付きのスキャンをサポートするフラット ベッド スキャナーの wia 項目のツリーを示す図](images/wia-feeder-tree4.png)

フラット ベッド スキャナー フィーダー (または自動ドキュメント フィーダー付き) がありませんでした。 次の図は、フラット ベッドや両面印刷ユニット フィーダー スキャナーの項目のツリーを示しています。

![フラット ベッドや両面印刷ユニット フィーダー スキャナーの項目のツリーを示す図](images/wia-feeder-tree2.png)

フラット ベッド項目は、フラット ベッド スキャナーの上に存在するがない場合にのみ省略できます。 同様に、フィーダー項目フィーダーをしているスキャナーの項目のツリーに存在する必要があります。 フィーダー項目は、基本的なスキャン (二重化またはシンプレックス)、単純な双方向 (同じフロントとバック項目)、および高度な双方向スキャン (フロント エンドとバック項目) などの設定の制御に使用されます。

### <a name="scanning"></a>スキャン

アプリケーションは、ドキュメント フィーダー付きのスキャンを実行するフィーダー項目に移動します。 この項目は、アプリケーションが数をスキャンするページと各ページの設定を構成します。 3 つのドキュメントが 3 つのページに結果をスキャンすることを確認します。

### <a name="image-acquisition"></a>Image Acquisition

標準の取得とフォルダーの取得、WIA フィーダー項目プロパティの設定はすべてのフロント ページ使用されます。 標準の取得とフォルダーの取得の詳細については、次を参照してください。[二重モード対応ドキュメント フィーダー付きの高度な](advanced-duplex-capable-document-feeder.md)します。

 

 



