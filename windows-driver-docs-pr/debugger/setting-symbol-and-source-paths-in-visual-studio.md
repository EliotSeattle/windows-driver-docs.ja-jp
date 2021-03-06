---
title: Visual Studio でのシンボルと実行可能イメージ パスの設定
description: プロシージャは、シンボルの設定と Visual Studio での実行可能ファイル イメージのパスについて説明します。
ms.assetid: BFFF9BBC-C926-4974-A43E-C3A2DDA74AA4
ms.date: 05/11/2018
ms.localizationpriority: medium
ms.openlocfilehash: 8c299b26ce55ddc964c3b26c22e7263b39cca9d3
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67366386"
---
# <a name="setting-symbol-and-executable-image-paths-in-visual-studio"></a>Visual Studio でのシンボルと実行可能イメージ パスの設定

> [!IMPORTANT]
> この機能は、Windows 10 バージョン 1507、以降のバージョンの WDK でご利用いただけません。
>


このトピックで示す手順では、Visual Studio に統合された Windows Driver Kit が必要です。 統合環境を取得するには、最初に、Microsoft Visual Studio をインストールし、Windows Driver Kit (WDK) をインストールします。 詳細については、次を参照してください。 [Windows ドライバー開発](https://docs.microsoft.com/windows-hardware/drivers/)します。

## <a name="span-idsettingthesymbolpathbyusingapropertypagespanspan-idsettingthesymbolpathbyusingapropertypagespanspan-idsettingthesymbolpathbyusingapropertypagespansetting-the-symbol-path-by-using-a-property-page"></a><span id="Setting_the_Symbol_Path_by_Using_a_Property_Page"></span><span id="setting_the_symbol_path_by_using_a_property_page"></span><span id="SETTING_THE_SYMBOL_PATH_BY_USING_A_PROPERTY_PAGE"></span>プロパティ ページを使用してシンボル パスの設定


1.  Visual Studio で、ホスト コンピューターで次のように選択します。**オプション**から、**ツール**メニュー。
2.  **オプション**プロパティ ボックスに移動**デバッグ&gt;シンボル**します。
3.  Microsoft シンボル サーバーからシンボルを取得する場合は、チェック**Microsoft シンボル サーバー**します。
4.  ホスト コンピューター上のフォルダーからシンボルを取得する場合は、チェック**環境変数。\_NT\_シンボル\_パス**します。 設定し、 \_NT\_シンボル\_パス[環境変数](general-environment-variables.md)します。

## <a name="span-idsettingthesymbolpathbyenteringacommandspanspan-idsettingthesymbolpathbyenteringacommandspanspan-idsettingthesymbolpathbyenteringacommandspansetting-the-symbol-path-by-entering-a-command"></a><span id="Setting_the_Symbol_Path_by_Entering_a_Command"></span><span id="setting_the_symbol_path_by_entering_a_command"></span><span id="SETTING_THE_SYMBOL_PATH_BY_ENTERING_A_COMMAND"></span>コマンドを入力して、シンボル パスの設定


デバッガーのイミディ エイト ウィンドウで、Visual Studio では、入力、 [ **.sympath (シンボル パスの設定)** ](-sympath--set-symbol-path-.md)コマンド。

## <a name="span-idsettingtheexecutableimagepathbyenteringacommandspanspan-idsettingtheexecutableimagepathbyenteringacommandspanspan-idsettingtheexecutableimagepathbyenteringacommandspansetting-the-executable-image-path-by-entering-a-command"></a><span id="Setting_the_Executable_Image_Path_by_Entering_a_Command"></span><span id="setting_the_executable_image_path_by_entering_a_command"></span><span id="SETTING_THE_EXECUTABLE_IMAGE_PATH_BY_ENTERING_A_COMMAND"></span>コマンドを入力して、実行可能イメージのパスを設定します。


デバッガーのイミディ エイト ウィンドウで、Visual Studio では、入力、 [ **.exepath (実行可能ファイル パスの設定)** ](-exepath--set-executable-path-.md)コマンド。

 

 





