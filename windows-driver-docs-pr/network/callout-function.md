---
title: 吹き出し関数
description: 吹き出し関数
ms.assetid: cf7b8e69-e6b2-41ac-9906-f0e3c090eb7a
keywords:
- 吹き出し関数 WDK Windows フィルタ リング プラットフォーム
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 596e4e19fafe9952299a6cce5f4d6273d5afb3a6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536777"
---
# <a name="callout-function"></a>吹き出し関数


A*コールアウト関数*によって実装されている関数には、[コールアウト ドライバー](callout-driver.md)を定義する関数の 1 つは、[コールアウト](callout.md)。 コールアウトは、引き出し関数の次の一覧で構成されます。

-   A [ *notifyFn* ](https://msdn.microsoft.com/library/windows/hardware/ff568803)通知を処理する関数。

-   A [ *classifyFn* ](https://msdn.microsoft.com/library/windows/hardware/ff544890)プロセス分類する関数。

-   A [ *flowDeleteFn* ](https://msdn.microsoft.com/library/windows/hardware/ff550025)関数をプロセス フローの削除 (省略可能)。

[フィルター エンジン](filter-engine.md)コールアウトは、ネットワークのデータを処理できるように吹き出しのコールアウトが関数の呼び出し。

 

 




