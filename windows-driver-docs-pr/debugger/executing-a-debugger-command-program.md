---
title: デバッガー コマンド プログラムの実行
description: デバッガー コマンド プログラムの実行
ms.assetid: ad28a5d6-0d6a-42c0-82f3-6760a8c773ab
keywords:
- デバッガー コマンド プログラムの実行
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 412bb20e950615b2247f31a52ba16ba2ea990b2d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379744"
---
# <a name="executing-a-debugger-command-program"></a>デバッガー コマンド プログラムの実行


## <span id="ddk_debugger_command_program_execution_dbg"></span><span id="DDK_DEBUGGER_COMMAND_PROGRAM_EXECUTION_DBG"></span>


デバッガー コマンド プログラムは、次の方法のいずれかで実行できます。

-   すべてのステートメントの入力、[デバッガー コマンド ウィンドウ](debugger-command-window.md)個々 のステートメントをセミコロンで区切られたコマンドの 1 つの文字列として。

-   個々 のステートメントをセミコロンで区切られたコマンドの 1 行上のスクリプト ファイルには、すべてのステートメントを追加します。 このスクリプト ファイルを実行しで説明する方法のいずれかを使用して[スクリプト ファイルを使用する](using-script-files.md)します。

-   別の行に各ステートメントでのスクリプト ファイル内のすべてのステートメントを追加します。 (または、キャリッジ リターンとセミコロンの任意の組み合わせでステートメントを分離する。)使用してこのスクリプト ファイルを実行し、 [  **$ &gt; &lt; (スクリプト ファイルを実行)** ](-----------------------a---run-script-file-.md)または **$$ &gt; &lt; (実行スクリプト ファイル)** コマンド。 これらのコマンドは、指定したスクリプト ファイルを開きをセミコロンで区切って、すべての改行を置き換え、1 つのコマンド ブロックとして生成されるテキストを実行します。

 

 





