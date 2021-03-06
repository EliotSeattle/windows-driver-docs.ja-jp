---
title: メモリ リークの検出
description: メモリ リークの検出
ms.assetid: 1227c5e8-d83b-4f27-aa69-6e54aebc3ad8
keywords:
- メモリ リーク
- メモリ リークのデバッグ
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5730b74408fa4c8c7c25b06f3f5deaf62ddc3641
ms.sourcegitcommit: a39a3f4c9f26968e00317574c0d8530ee8ab6f8b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67894234"
---
# <a name="finding-a-memory-leak"></a>メモリ リークの検出

メモリ リークが発生、プロセスは、ページまたは非ページ プールからメモリを割り当てますが、メモリを解放しません。 その結果、これらの制限付きプールのメモリが不足している Windows 速度が低下する原因と、時間の経過と共にします。 メモリが完全になくなると、エラーが表示される場合があります。

このセクションで、次のとおりです。

- [リークが存在するかを決定する](determining-whether-a-leak-exists.md)かわからない場合に使用できる手法について説明します、システムでメモリ リークがあるかどうか。

- [カーネル モード メモリ リークを検出](finding-a-kernel-mode-memory-leak.md)カーネル モード ドライバーまたはコンポーネントによってリークを検出する方法について説明します。

- [ユーザー モード メモリ リークを検出](finding-a-user-mode-memory-leak.md)ユーザー モード ドライバーまたはアプリケーションによって引き起こされるリークを検出する方法について説明します。

