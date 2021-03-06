---
ms.assetid: AB35CE97-0C66-47B3-9C64-81BA01D65104
title: 新しいソフトウェア ドライバーの作成
description: このトピックでは、Visual Studio を使って新しいソフトウェア ドライバーの作成を始める方法について説明します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: bcaf5c2e7e27eb5d4791f6825f9a7412768123e3
ms.sourcegitcommit: 5598b4c767ab56461b976b49fd75e4e5fb6018d2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2020
ms.locfileid: "67370773"
---
# <a name="creating-a-new-software-driver"></a>新しいソフトウェア ドライバーの作成

このトピックでは、Visual Studio を使って新しいソフトウェア ドライバーの作成を始める方法について説明します。 ソフトウェア ドライバーは、デバイス ファンクション ドライバー、フィルター ドライバー、ファイル システム ドライバーとは異なります。それらのドライバーについては、別のトピックで説明しています。 ソフトウェア ドライバーと、他の種類のドライバーとの違いについて詳しくは、「[ドライバーとは](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/what-is-a-driver-)」と「[ドライバー モデルの選択](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/choosing-a-driver-model)」をご覧ください。

まず、どのドライバー モデルがソフトウェア ドライバーに適しているかを判断します。 選択肢は、カーネル モード ドライバー フレームワーク (KMDF)、従来の NT ドライバー モデル、Windows Driver Model (WDM) の 3 つです。 どのモデルが最適かの判断については、「[ドライバー モデルの選択](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/choosing-a-driver-model)」をご覧ください。

## <a name="case-1-you-want-to-use-kmdf"></a>ケース 1:KMDF を使用する

1. Visual Studio の **[ファイル]** メニューで、 **[新規作成]、[プロジェクト]** の順にクリックします。
2. [新しいプロジェクト] ダイアログ ボックスの左側のウィンドウで、 **[WDF]** を探してクリックします。
3. 中央のウィンドウで、 **[Kernel Mode Driver (KMDF)] (カーネル モード ドライバー (KMDF))** をクリックします。
4. **[名前]** ボックスと **[場所]** ボックスに入力し、 **[OK]** をクリックします。 詳しくは、「[テンプレートを使った KMDF ドライバーの作成](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/writing-a-kmdf-driver-based-on-a-template)」をご覧ください。
    > [!NOTE]
    > 新しい KMDF ドライバーを作成する場合、32 文字以下のドライバー名を選ぶ必要があります。 この長さの制限は、wdfglobals.h で定義されています。
5. この時点で、ほとんどの KMDF ドライバーに必要な一般的なコードを実装したドライバー プロジェクトができています。 これで、ソフトウェア ドライバー固有のコードを追加できるようになりました。

## <a name="case-2-you-want-to-use-the-legacy-nt-model"></a>ケース 2:従来の NT モデルを使用する

1. Visual Studio の **[ファイル]** メニューで、 **[新規作成]、[プロジェクト]** の順にクリックします。
2. Visual Studio の [新しいプロジェクト] ダイアログ ボックスで、 **[Windows Driver (Windows ドライバー)]** の **[WDM]、[Empty WDM Driver (空の WDM ドライバー)]** をクリックします。

    > [!NOTE]
    > 作成するのは WDM ドライバーではありませんが、 **[Empty WDM Driver]\(空の WDM ドライバー\)** テンプレートが必要です。
3. **[名前]** ボックスと **[場所]** ボックスに入力し、 **[OK]** をクリックします。
4. この時点で、空の WDM ドライバー プロジェクトができます。 ソリューション エクスプローラー ウィンドウでドライバー プロジェクトを右クリックし、 **[追加]、[新しい項目]** の順にクリックします。
5. [新しい項目の追加] ダイアログ ボックスで **[C++ ファイル (.cpp)]** を選び、ファイルの名前を入力して **[OK]** をクリックします。

    > [!NOTE]
    > .cpp ファイルでなく .c ファイルを作成する場合は、拡張子が **.c** の名前を入力します。
6. ntddk.h をインクルードします。
7. ソフトウェア ドライバーに必要な関数を実装します。 関数の実装と整理が進むにつれて、ヘッダー ファイル、.cpp または .c ファイルの追加が必要になる場合があります。

## <a name="case-3-you-want-to-use-wdm"></a>ケース 3:WDM を使用する

ソフトウェア ドライバーに WDM を使うことはほとんどありません。 しかし、使う場合は、次の手順に従います。

1. Visual Studio の **[ファイル]** メニューで、 **[新規作成]、[プロジェクト]** の順にクリックします。
2. Visual Studio の [新しいプロジェクト] ダイアログ ボックスで、 **[Windows Driver]** (Windows ドライバー) の **[WDM]** をクリックします。
3. **[名前]** ボックスと **[場所]** ボックスに入力し、 **[OK]** をクリックします。
4. この時点で、空の WDM ドライバー プロジェクトができます。 ソリューション エクスプローラー ウィンドウでドライバー プロジェクトを右クリックし、 **[追加]、[新しい項目]** の順にクリックします。
5. [新しい項目の追加] ダイアログ ボックスで **[C++ ファイル (.cpp)]** を選び、ファイルの名前を入力して **[OK]** をクリックします。

    > [!NOTE]
    > .cpp ファイルでなく .c ファイルを作成する場合は、拡張子が **.c** の名前を入力します。
6. wdm.h をインクルードします。
7. ソフトウェア ドライバーに必要な関数を実装します。 関数の実装と整理が進むにつれて、ヘッダー ファイル、.cpp または .c ファイルの追加が必要になる場合があります。
