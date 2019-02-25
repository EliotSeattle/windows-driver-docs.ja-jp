---
title: 表示と WinDbg のローカル変数の編集
description: コマンドを入力して、[ローカル] ウィンドウを使用して、または [ウォッチ] ウィンドウを使用して、WinDbg でローカル変数を表示できます。
ms.assetid: 9d816df7-2b20-4be3-90d7-7a11b0f30238
keywords:
- デバッグ情報のウィンドウで [ローカル] ウィンドウ
- '[ローカル] ウィンドウ'
- メモリ、[ローカル] ウィンドウ
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: b4a637edb0b15d7246758585ac172feb6d221def
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56527668"
---
# <a name="viewing-and-editing-local-variables-in-windbg"></a>表示と WinDbg のローカル変数の編集


コマンドを入力して、[ローカル] ウィンドウを使用して、または [ウォッチ] ウィンドウを使用して、WinDbg でローカル変数を表示できます。

## <a name="span-iddebuggercommandwindowspanspan-iddebuggercommandwindowspanspan-iddebuggercommandwindowspandebugger-command-window"></a><span id="Debugger_Command_Window"></span><span id="debugger_command_window"></span><span id="DEBUGGER_COMMAND_WINDOW"></span>デバッガー コマンド ウィンドウ


入力して、ローカル変数とパラメーターを表示することができます、 [ **dv** ](dv--display-local-variables-.md)コマンドまたは[ **dt** ](dt--display-type-.md)デバッガー コマンド] ウィンドウでコマンド。

## <a name="span-idddklocalswindowdbgspanspan-idddklocalswindowdbgspanopening-the-locals-window"></a><span id="ddk_locals_window_dbg"></span><span id="DDK_LOCALS_WINDOW_DBG"></span>[ローカル] ウィンドウを開く


[ローカル] ウィンドウには、現在のスコープ内のすべてのローカル変数に関する情報が表示されます。

開くかで WinDbg ウィンドウで、ローカル ウィンドウに切り替え、**ビュー**  メニューのをクリックして**ローカル**します。 (ALT + 3 キーを押すこともできます をクリックしてまたは、**ローカル**ボタン (![[ローカル] ボタンのスクリーン ショット](images/tblocal.png)) ツールバー。 ALT + SHIFT + 3 を閉じる [ローカル] ウィンドウ。)

次のスクリーン ショットでは、[ローカル] ウィンドウの例を示します。

![[ローカル] ウィンドウのスクリーン ショット ](images/window-locals.png)

[ローカル] ウィンドウには、4 つの列を含めることができます。 **名前**と**値**列は常に表示される、および**型**と**場所**列は省略可能です。 表示する、**型**と**場所**列、をクリックして、 **Typecast**と**場所**ボタン、それぞれ、ツールバーの。

## <a name="span-idusingthelocalswindowspanspan-idusingthelocalswindowspanspan-idusingthelocalswindowspanusing-the-locals-window"></a><span id="Using_the_Locals_Window"></span><span id="using_the_locals_window"></span><span id="USING_THE_LOCALS_WINDOW"></span>[ローカル] ウィンドウを使用します。


[ローカル] ウィンドウでは、次の操作を行うことができます。

-   **名前**列には、それぞれのローカル変数の名前が表示されます。 変数が、データ構造の場合は、その名前の横にあるチェック ボックスが表示されます。 構造体メンバーの表示を閉じたりするには、選択するか、チェック ボックスをオフにします。

-   **値**列には、各変数の現在の値が表示されます。

    -   変数の新しい値を入力するには、現在の値をダブルクリックしますと、新しい値を入力または古い値を編集します。 (切り取り、コピー、および貼り付けコマンドは、編集するために使用できる)。いずれかを入力できます[C++ 式](c---numbers-and-operators.md)します。
    -   新しい値を保存するには、ENTER キーを押します。
    -   新しい値を破棄するには、esc キーを押します。
    -   無効な値を入力すると、ENTER キーを押したときに、古い値が再び表示されます。

    型の整数**int**は 10 進数の値として表示される型の整数**UINT**が現在の基数に表示されます。 現在の基数を変更するには、使用、 [ **n (設定数の基本)** ](n--set-number-base-.md)デバッガー コマンド] ウィンドウでコマンド。

-   **型**列 ([ローカル] ウィンドウに表示されます) 場合は、各変数の現在のデータ型を示しています。 各変数が独自のデータ型の適切な形式で表示されます。 データ構造にその型の名前がある、**型**列。 その他の変数の型は、この列に「新しい型の入力」を表示します。

    「新しい種類の入力」をダブルクリックする場合は、新しいデータ型を入力して、型をキャストできます。 このキャストは、[ローカル] ウィンドウにのみ、この変数の現在の表示を変更します。これは変更されません何もデバッガーで、または、ターゲット コンピューター上。 さらで新しい値を入力する場合、**値**列、入力したテキストは解析に入力したすべての新しい型ではなく、シンボルの実際の型に基づいて、**型**列。 [ローカル] ウィンドウを閉じてするデータ型の変更が失われます。

    拡張機能のコマンドを入力することも、**型**列。 デバッガーでは、シンボルのアドレスをこの拡張機能に渡すし、一連の現在の行の下にある折りたたみ可能な行の結果の出力が表示されます。 たとえば、スレッド環境ブロックの有効なアドレスの場合は、この行でシンボルを入力できます **! teb**で、**型**を実行する列、 [ **! teb** ](-teb.md)このシンボルのアドレスで拡張機能。

-   **場所**列 ([ローカル] ウィンドウに表示されます) 場合は、データ構造の各メンバーのオフセットを示します。

-   ローカル変数が、Vtable を含むクラスのインスタンスの場合、**名前**列が、Vtable を表示し、関数ポインターを表示する v テーブルを展開することができます。 派生実装、表記法を示す基本クラスの Vtable が含まれている場合 **\_vtcast\_クラス**を示すため、派生クラスが追加されているメンバーが表示されます。 これらのメンバーは、派生クラス型のように展開します。

-   [ローカル コンテキスト](changing-contexts.md#local-context)決定 [ローカル] ウィンドウでローカル変数のセットが表示されます。 何らかの理由で、ローカル コンテキストが変更されると、[ローカル] ウィンドウが自動的に更新します。 既定では、ローカル コンテキストは、プログラムのカウンターの現在の位置と一致します。 ローカル コンテキストを変更する方法の詳細については、ローカル コンテキストを参照してください。

[ローカル] ウィンドウが 2 つのボタンを含むツールバー (**Typecast**と**場所**) とその他のコマンドのショートカット メニュー。 メニューにアクセスする、ウィンドウのタイトル バーを右クリックするか、ウィンドウの右上隅の近くのアイコンをクリックします (![は同じですが、このトピックのアイコンをボタン、2 つが、さまざまな機能を提供しているよう](images/window-locals-menu-icon.png))。 ツールバーとメニューは、次のボタンおよびコマンドが含まれます。

-   (ツールバーとメニュー)**Typecast**の表示、**型**オンとオフの列。

-   (ツールバーとメニュー)**場所**の表示、**場所**オンとオフの列。

-   (メニューのみ)**表示の 16 ビット値は Unicode として**Unicode 文字列をこのウィンドウに表示します。 このコマンドは、オンとオフは、[ローカル] ウィンドウでは、ウォッチ ウィンドウ、およびデバッガー コマンドの出力に影響するグローバルな設定をオンにします。 このコマンドを使用すると、 [**リストア\_(Unicode 表示を有効にする) を unicode** ](-enable-unicode--enable-unicode-display-.md)コマンド。

-   (メニューのみ)**常に表示番号の既定の基数**と 10 進数形式で表示することではなく既定の基数に表示される整数。 このコマンドは、オンとオフは、[ローカル] ウィンドウでは、ウォッチ ウィンドウ、およびデバッガー コマンドの出力に影響するグローバルな設定をオンにします。 このコマンドを使用すると、 [ **.force\_基数\_出力 (整数の基数を使用して)** ](-force-radix-output--use-radix-for-integers-.md)コマンド。

    **注**   、**常に表示番号の既定の基数**コマンドでは長整数には影響しません。 しない限り、長整数が 10 進数形式で表示されます、 [**リストア\_長い\_状態 (Long 整数の表示を有効にする)** ](-enable-long-status--enable-long-integer-display-.md)コマンドを設定します。 **リストア\_長い\_状態**コマンド [ウォッチ] ウィンドウで、[ローカル] ウィンドウで、デバッガー コマンドの出力の表示に影響は、[ローカル] ウィンドウで、メニューで、このコマンドに相当するものはありません。

     

-   (メニューのみ)**選択した値を開いて [メモリ] ウィンドウ**新しいドッキング メモリ ウィンドウが開き、選択した式のアドレスで始まるメモリを表示します。

-   (メニューのみ)**Dt が選択されているメモリの値を呼び出す**実行、 [ **dt (表示の種類)** ](dt--display-type-.md)コマンドのパラメーターとして選択したシンボルにします。 デバッガー コマンド ウィンドウで、結果が表示されます。 **-N**オプションが自動的に 16 進数のアドレスからシンボルを区別するために使用します。 その他のオプションは使用されません。 このメニュー項目を使用して生成されるコンテンツを実行しているときに生成されたコンテンツと同じことに注意してください、 **dt**形式、コマンドラインからコマンドが若干異なります。

-   (メニューのみ)**ツールバー**オンとオフは、ツールバーをオンにします。

-   (メニューのみ)**ドッキング**または**ドッキング解除**によって、ウィンドウに入力するか、ドッキング状態のままにします。

-   (メニューのみ)**新しいドッキングするのには移動**[ローカル] ウィンドウを閉じ、新しいドッキング ステーションで開かれます。

-   (メニューのみ)**ウィンドウの種類のタブのドッキング先として設定**[ローカル] ウィンドウでは使用できません。 このオプションでは、windows のソースまたはメモリの使用のみです。

-   (メニューのみ)**常に浮動**によって、ウィンドウをドッキング場所にドラッグされる場合でも、ドッキングされていないままにします。

-   (メニューのみ)**フレームを使用して移動**によって、ウィンドウに、ウィンドウがドッキングされていない場合でも、WinDbg フレームが移動したときに移動します。 Windows のドッキング、タブ、および浮動小数点の詳細については、次を参照してください。 [、Windows の位置づけ](positioning-the-windows.md)します。

-   (メニューのみ)**ヘルプ**ツールを Windows のデバッグ ドキュメントのこのトピックを開きます。

-   (メニューのみ)**閉じる**このウィンドウを閉じます。

## <a name="span-idddkdebuggingbioscodedbgspanspan-idddkdebuggingbioscodedbgspanthe-watch-window"></a><span id="ddk_debugging_bios_code_dbg"></span><span id="DDK_DEBUGGING_BIOS_CODE_DBG"></span>[ウォッチ] ウィンドウ


、WinDbg で表示し、ローカル変数を変更する [ウォッチ] ウィンドウを使用することができます。 [ウォッチ] ウィンドウには、使用する変数の一覧を表示できます。 これらの変数には、グローバル変数と任意の関数からのローカル変数を含めることができます。 [ウォッチ] ウィンドウでは、いつでも、現在の関数のスコープに一致する変数の値を表示します。 [ウォッチ] ウィンドウでこれらの変数の値を変更することもできます。

[ウォッチ] ウィンドウは、[ローカル] ウィンドウとは異なり、ローカル コンテキストの変更により影響はありません。 現在のプログラム カウンターのスコープで定義されている変数のみには、表示または変更は、その値を持つことができます。

[ウォッチ] ウィンドウを開くには、次のように選択します。**ウォッチ**から、**ビュー**メニュー。 ALT + 2 キーを押すこともできますかをクリックして、**ウォッチ**ツールバーのボタン:![ウォッチ式のボタンのスクリーン ショット](images/tbwatch.png)します。 ALT + SHIFT + 2 は、[ウォッチ] ウィンドウを閉じます。

次のスクリーン ショットでは、ウォッチ ウィンドウの例を示します。

![[ウォッチ] ウィンドウのスクリーン ショット ](images/window-watch.png)

[ウォッチ] ウィンドウには、4 つの列を含めることができます。 **名前**と**値**列は常に表示される、および**型**と**場所**列は省略可能です。 表示する、**型**と**場所**列、をクリックして、 **Typecast**と**場所**ボタン、それぞれ、ツールバーの。

## <a name="span-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報


ローカル変数を制御する方法の詳細については、変数を使用して、スコープとその他のメモリに関連するコマンドの説明の変更の概要を参照してください[読み取りと書き込みメモリ](reading-and-writing-memory.md)します。

 

 




