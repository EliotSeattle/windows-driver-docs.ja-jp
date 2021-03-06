---
title: ブレークポイントを編集します。
description: ブレークポイントを編集します。
ms.assetid: ca55ee25-aef3-42b1-b628-0a0e849103eb
keywords:
- ブレークポイントを編集します。
- ブレークポイント、ブレークポイントの編集
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 97f5f14b9e3c202527160cd1534ee29011f131a2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63354799"
---
# <a name="edit--breakpoints"></a>Edit | Breakpoints (編集 | ブレークポイント)


## <span id="ddk_edit_breakpoints_dbg"></span><span id="DDK_EDIT_BREAKPOINTS_DBG"></span>


クリックして**ブレークポイント**上、**編集**メニューを表示またはブレークポイントを制御します。

このコマンドは、ALT + F9 キーを押すと同じです。 場合、[ソース ウィンドウ](source-window.md)または[逆アセンブル ウィンドウ](disassembly-window.md)がアクティブでない、f9 キーを押してしたりできます をクリックして、**ブレークポイント (f9) を挿入または**ボタン (![スクリーン ショット挿入または削除するブレークポイントのボタンの](images/tbbp.png)) ツールバー。

ただし、ソース ウィンドウまたは [逆アセンブル] ウィンドウがある場合は開きます、**挿入ブレークポイント (F9) を削除または**ボタンをクリックし、F9 キーは、現在の行にブレークポイントを設定します。 (既にある場合、現在の行にブレークポイントを設定、キーまたはボタンはブレークポイントを削除します。)

ステートメントや呼び出しを複数の行にまたがっている場合、WinDbg は、ステートメントまたは呼び出しの最後の行のブレークポイントを設定します。 またはステートメント全体に対してブレークポイントを設定するステートメントの前に、キャレット (^) を挿入する必要があります。 デバッガーは、現在のカレット位置にブレークポイントを設定することはできませんが許可されている次の位置を下方向に検索され、あるブレークポイントを挿入します。

### <a name="span-iddialogboxspanspan-iddialogboxspandialog-box"></a><span id="dialog_box"></span><span id="DIALOG_BOX"></span>ダイアログ ボックス

クリックすると**ブレークポイント**、**ブレークポイント** ダイアログ ボックスが表示されます。 このダイアログ ボックスでは、現在のすべてのブレークポイント情報を表示しは、次の列に表示されます。

-   ブレークポイントの数。 以降のコマンドのブレークポイントを指すために使用できる 10 進の番号です。

-   ブレークポイントの状態です。 この状態は、 **e** (有効) または**d** (無効)。

-   (未解決のブレークポイントのみ)文字**u**します。 ブレークポイントが解決しない場合、この文字が表示されます (つまり、任意のモジュールの現在読み込まれているアドレスを一致いません)。 詳細については、次を参照してください。[未解決ブレークポイント (bu ブレークポイント)](unresolved-breakpoints---bu-breakpoints-.md)します。

-   ブレークポイントの仮想アドレス。 ソース行番号の読み込みを有効にした場合、表示には、アドレスのオフセットではなく、ファイルと行番号情報が含まれます。 ブレークポイントが解決されない場合は、ここではなく、一覧の最後に、アドレスが表示されます。

-   (プロセッサのブレークポイントのみ)情報の種類とサイズ。 この情報は、 **e** (execute)、 **r** (読み取り/書き込み) **w** (書き込み)、または**は**(入力/出力)。 これらの型は、(バイト単位)、ブロックのサイズに従います。 詳細については、次を参照してください。[プロセッサ ブレークポイント (ba ブレークポイント)](processor-breakpoints---ba-breakpoints-.md)します。

-   かっこで囲まれたパスの初期数後に、ブレークポイントがアクティブになるまでの残りはパスの数。 1 つのプログラム カウンターは、互換性に影響することがなく、ブレークポイントを通過する回数ですこの数値の値より小さくします。 したがって、この数は 1 より小さいことはありません。 この数がこのポイントを介してアプリケーションの実行時間のみをカウントすることにも注意してください。 つまり、このポイントの上にステップ インはカウントされません。 フル カウントに達した後にクリアし、ブレークポイントをリセットすることによってのみ、カウントをリセットできます。

-   関連付けられたプロセスとスレッド。 スレッドが 3 つのアスタリスクで指定した場合 (\*\*\*)、このブレークポイントは、スレッド固有のブレークポイントではありません。

-   モジュールとのオフセットでの関数は、ブレークポイントのアドレスに対応します。 ブレークポイントが解決されない場合、ブレークポイントのアドレスはかっこで囲まれたここでは、表示されます。 ブレークポイントが有効なアドレスの設定、シンボル情報が不足している場合、この列は空白になります。

-   このブレークポイントにヒットしたときに自動的に実行されるコマンド文字列。 このコマンド文字列は引用符で表示されます。 ブレークポイントにヒットした場合、このコマンド文字列内のコマンドは、アプリケーションの実行が再開されるまでに実行されます。 いずれかのプログラムの実行を再開コマンド (など**g**または**t**) コマンドの一覧の実行を停止します。

クリックできますしのすべてのブレークポイントを選択した場合、**削除**、**を無効にする**、または**を有効にする**ボタンをクリックします。 **削除**ボタンは、ブレークポイントを完全に削除します。 **を無効にする**ボタンは、ブレークポイントを一時的に無効にします。 **を有効にする** ボタンを無効になっているブレークポイントを再度有効にします。

**すべて削除**ボタンは、すべてのブレークポイントを完全に削除します。

内のコマンドを入力することも、**コマンド**ボックスに、次の方法。

-   入力した場合、 [ **bp (ブレークポイントの設定)**](bp--bu--bm--set-breakpoint-.md)、 **bu (未解決のブレークポイントの設定)**、 **bm (シンボルのブレークポイントの設定)**、 [ **ba (アクセスの切断)**](ba--break-on-access-.md)、 [ **bc (ブレークポイント クリア)**](bc--breakpoint-clear-.md)、 [ **(ブレークポイントを無効にする) bd**](bd--breakpoint-disable-.md)、または[ **(ブレークポイントを有効にする) をする**](be--breakpoint-enable-.md)コマンド、**コマンド**でコマンドを入力した場合、ボックスの動作、 [デバッガー コマンド ウィンドウ](debugger-command-window.md)します。 ただし、コマンド自体は、小文字である必要があります。 コマンドは、スレッドの指定子で始まることはできません。 スレッドの指定子を使用する場合を入力します。、**スレッド**初期ティルダ (~) なしのボックスです。

-   その他の任意のテキストを入力すると、テキストは、の引数文字列として扱われます、 [ **bu (未解決のブレークポイントの設定)** ](bp--bu--bm--set-breakpoint-.md)コマンド。 プレフィックスのエントリでは、デバッガー **bu**とスペースしてコマンドとして実行します。

新しいブレークポイントを入力するときにも、行うことができます。

-   ブレークポイントを作成するスレッドに固有のスレッドの指定子を入力して、**スレッド**ボックス。 通常、スレッドの指定子を先頭にティルダ (~) 文字を含めないでください。

-   条件を入力して、条件付きブレークポイントを作成、**条件**ボックス。 条件は、任意の評価可能な式を指定でき、現在の式の構文に従って評価されます (を参照してください[を評価する式](evaluating-expressions.md))。 これらの種類のブレークポイントの詳細については、次を参照してください。 [、条件付きブレークポイント](setting-a-conditional-breakpoint.md)します。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

ブレークポイント、他のコマンドのブレークポイントとブレークポイント、およびカーネル デバッガーからのユーザー領域でブレークポイントの設定を制御する方法を使用する方法の詳細については、次を参照してください。[を使用してブレークポイント](using-breakpoints.md)します。 条件付きブレークポイントの詳細については、次を参照してください。 [、条件付きブレークポイント](setting-a-conditional-breakpoint.md)します。

 

 





