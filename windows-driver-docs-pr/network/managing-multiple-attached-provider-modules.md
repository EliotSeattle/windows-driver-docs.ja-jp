---
title: 複数のアタッチされているプロバイダー モジュールの管理
description: 複数のアタッチされているプロバイダー モジュールの管理
ms.assetid: 307cfbf8-e5a3-4c01-abf5-5b2eea250d77
keywords:
- WDK ネットワーク モジュールの登録、アタッチされている複数のプロバイダー モジュール
- WDK ネットワーク モジュールの登録、アタッチされている複数のクライアント モジュール
- 複数の接続されているネットワーク モジュール WDK ネットワーク モジュールのレジストラー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: afb75baf40f971a90067f58a770793490d840c52
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63343582"
---
# <a name="managing-multiple-attached-provider-modules"></a>複数のアタッチされているプロバイダー モジュールの管理


1 つのクライアント モジュールは、プロバイダーの 1 つ以上のモジュールにアタッチできます。 接続されているプロバイダーに複数のモジュールを管理するためにクライアント モジュールする必要があります個別に保存しないバインド ハンドル、プロバイダー モジュールのバインディング コンテキスト、およびがアタッチされているプロバイダー モジュールごとに、プロバイダー モジュールのディスパッチ テーブル。 通常、このデータは、添付ファイルごとにクライアント モジュールのバインド コンテキストに保存されます。 ただし、クライアント モジュールは、選択した任意の方法で接続されているプロバイダー モジュールごとにデータを管理できます。

A[ネットワーク プログラミング インターフェイス (NPI)](network-programming-interface.md)クライアント モジュールのバインド コンテキストへのポインターまたは他の NPI 固有識別子としてのいずれかのいずれかが含まれているように、通常、クライアントのモジュールのコールバック関数を定義します関数パラメーター。 その結果、クライアント モジュールは、NPI コールバック関数のいずれかが呼び出されると、どのプロバイダー モジュールは、呼び出し元を判断できます。

 

 





