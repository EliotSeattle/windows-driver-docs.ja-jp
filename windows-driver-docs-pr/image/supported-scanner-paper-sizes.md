---
title: サポートされているスキャナーの用紙サイズ
description: サポートされているスキャナーの用紙サイズ
ms.assetid: c4437c38-b43a-433c-913a-d3de9bf74284
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 026bd09af83f5f147128dd7e68cce0def86571c0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56548732"
---
# <a name="supported-scanner-paper-sizes"></a>サポートされているスキャナーの用紙サイズ





WIA ユーザー インターフェイスの 2 つのコンポーネントは、ユーザーに対してページ サイズの一覧を表示することが、スキャナーをサポートするページ サイズを把握する WIA ドライバーの簡単な方法はありません。

### <a name="page-size-in-wia-applications"></a>WIA アプリケーションでのページ サイズ

WIA のプロパティがサポートされているレポート ページ サイズに WIA ドライバーが存在しないか、アプリケーションがページ サイズを直接指定できるようにします。 ドライバーにページ サイズの設定を通信するためには、アプリケーションはドット/インチ (dpi) で必要なサイズの計算し、デバイスの登録の要件に準拠するスキャンの原点を調整する必要があります。

### <a href="" id="page-size-in-the-common-scanner-dialog-and-in-the-scanner-and-camera-w"></a>一般的なスキャナーのダイアログ ボックスで、スキャナーとカメラ ウィザードで、ページ サイズ

一般的なスキャナーのダイアログ ボックスとスキャナーとカメラ ウィザードのサポートされているページ サイズを水平方向の幅と高さ、0.001 インチ単位で両方で各ページのサイズが説明されている静的テーブルがあります。 スキャナーがドキュメント フィーダー モードの場合にのみ、これらのページ サイズが表示されています。

フィードのモードでは、ページで、ドライバーをサポートする、(領域) でのページの最大サイズ、ベッドの最大サイズによって決定されると見なされます既定のページ サイズ。 フィーダーまたはデバイスのベッドに収まらない用紙サイズは、ユーザーに提供されていません。

 

 



