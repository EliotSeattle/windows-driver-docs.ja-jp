---
title: Web サイトを設定します。
description: Web サイトを設定します。
ms.assetid: 9c719557-bca0-4c9c-9208-70e106d976f9
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5b31665742900d479fcd90231c7d4056a6ff9cd2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560535"
---
# <a name="setting-up-the-web-site"></a>Web サイトを設定します。


元のソース ファイルを共有し、サイトのルート ディレクトリに注意してください、Web サイトを設定します。 ソースは、使用可能なサイトからなどです。

```text
https://SrcMachineName/source
```

ソース ファイルをインターネット経由でアクセスできるようにするためには、ソース ファイルを含んでいるディレクトリを構成する必要があります。

インデックス付きソースが存在するディレクトリを選択して開始します。 この例でこのディレクトリの c: を呼び出して\\ソースと、ネットワーク上でサーバーの名前\\SrcMachineName します。 ユーザーは、サイトにアクセスできるし、ネットワーク経由でソース コンテンツにアクセスする必要があるセキュリティ グループを追加する必要がありますように、アクセス許可を設定する必要があります。 有効にするセキュリティのレベルでは、環境からは異なります。 いくつかのインストールでは、このグループは**Everyone**します。

**ディレクトリのアクセス許可を設定します。**

1.  開いている**Windows エクスプ ローラー**します。

2.  展開**コンピューター**します。

3.  C: ドライブを展開します。

4.  右クリックして**c:\\ソース**選択**共有とセキュリティ**します。

5.  チェック、**このフォルダーを共有**ボタンをクリックします。

6.  をクリックして、**権限**ボタンをクリックします。

7.  必要なセキュリティ グループが読み取りアクセス権を下に追加することであることを確認**グループまたはユーザー名**と適切なボックスをチェックします。

8.  クリックして**OK**アクセス許可を終了します。

9.  をクリックして**OK**ソースのプロパティを終了します。

ソース ディレクトリ srv のソース パスを持つ別のコンピューターでのデバッグに使用できます\*\\\\SrcMachineName\\ソース。

 

 




