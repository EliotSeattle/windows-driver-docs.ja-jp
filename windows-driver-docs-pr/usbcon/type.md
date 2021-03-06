---
Description: このトピックでは、USB タイプ C 対応システムと Windows の相互運用性をテストする方法について説明します。
title: USB Type-C 手動相互運用性テスト手順
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bdbbe69fb2defd000933a0842b6a2cfcf07cb392
ms.sourcegitcommit: b316c97bafade8b76d5d3c30d48496915709a9df
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/13/2020
ms.locfileid: "79242891"
---
# <a name="usb-type-c-manual-interoperability-test-procedures"></a>USB Type-C 手動相互運用性テスト手順


**要約**

-   Windows 10 の USB タイプ-C 手動の相互運用性テスト手順: 機能テスト (FT) とストレステスト (ST)。
-   さまざまなテスト計画は、割り当てられた時間に対して特定の目的を解決することを意図しています。
-   デバイスの追加や削除などのシナリオを確認するための診断手順とヒント。

\* * に適用されます * *

-   Windows 10

**公式の仕様と手順**

-   [USB 3.1 および USB タイプ-C 仕様]( https://go.microsoft.com/fwlink/p/?LinkId=620208)
-   [xHCI の相互運用性テスト手順](https://go.microsoft.com/fwlink/p/?LinkId=623257)

**最終更新日時**

-   2015 年 8 月

このトピックでは、USB タイプ C 対応システムと Windows の相互運用性をテストする方法について説明します。 デバイスおよびシステムの製造元が、USB タイプ C コネクタを公開するシステムやデバイスでさまざまな機能とストレスのテストを実行するためのガイドラインを提供します。 このリーダーは、USB.ORG からダウンロードできる公式の USB 仕様および xHCI 相互運用性テスト手順に精通していることを前提としています。

USB タイプの C ConnEx ボードを使用してこれらのテストを実行する方法については、「usb の種類-c[を使用した c システムのテスト](test-usb-type-c-systems-with-mutt-connex-c.md)」を参照してください。

テスト製品は、次の1つまたは複数のカテゴリに属することができます。

-   **システム**: 種類 C の USB ポートが公開されているデスクトップ、ラップトップ、タブレット、サーバー、または電話。 Windows 10 のデスクトップエディション (Home、Pro、Enterprise、および教育)、Windows 10 Mobile などのバージョンを実行している必要があります。
-   **Dock**: 複数のポートを公開する任意の USB タイプ C デバイス。
-   **デバイス**: タイプ C ポートを持つ任意の USB デバイスで、システムまたはドッキングに接続できます。 このカテゴリには、従来の USB デバイスだけでなく、USB タイプ C 仕様で定義されているアクセサリモードと代替モードをサポートするデバイスが含まれます。

USB タイプ C の相互運用性テスト手順は、「機能テスト (FT)」と「ストレステスト (ST)」の2つのセクションに分かれています。 各テストセクションでは、テストケースについて説明し、テストに適用されるカテゴリを識別します。 製品は、該当するカテゴリ全体に対してテストする必要があります。 特定のテストケースには、関連するヒントへのリンクと、追加情報のヒントが含まれています。 このドキュメントでは、USB タイプ C の機能とエクスペリエンスに焦点を絞っています。 Usb タイプ C のソリューションには、USB ハブや USB コントローラーなどの他の USB コンポーネントが含まれている場合があります。 USB ハブとコントローラーの詳細なテストについては、「USB IF の[xHCI の相互運用性テスト手順](https://go.microsoft.com/fwlink/p/?LinkId=623257)」と「Windows ハードウェア認定キット」に記載されています。

<a href="" id="device-enumeration"></a>[デバイス列挙型](#ft1)  
デバイス列挙の主要な側面が機能していることを確認します。

<a href="" id="system-boot"></a>[システムブート](#ft2)  
製品が通常のシステムブートを妨げることがないことを確認します。

<a href="" id="system-power-transitions"></a>[システムの電源切り替え](#ft3)  
システムの電源遷移と、低い電力状態からのウェイクアップ機能が製品の影響を受けないかどうかをテストします。

<a href="" id="selective-suspend"></a>[選択的中断](#ft4)  
選択的中断遷移を確認します。

<a href="" id="dock-identification"></a>[識別のドック](#ft5)  
Dock のデバイス記述子が正しく実装されていることを確認してください。

<a href="" id="alternate-mode-negotiation"></a>[代替モードネゴシエーション](#ft6)  
サポートされている代替モードを確認します。

<a href="" id="charging-and-power-delivery--pd-"></a>[課金と電力配信 (PD)](#ft7)  
USB タイプ-C での充電を確認します。

<a href="" id="role-swap"></a>[ロールのスワップ](#ft8)  
ロールのスワップを確認します。

「ストレステスト」セクションでは、一定期間にわたってデバイスの安定性をテストする、ストレスおよびエッジケースシナリオの手順について説明します。 ストレステストには、レガシ USB 検証 (非 USB タイプ C) 用のカスタムデバイス、 [MICROSOFT USB テストツール (MUTT) デバイス](microsoft-usb-test-tool--mutt--devices.md)が必要です。 その他のテストと自動化は、今後の USB タイプ C テストデバイスで実現できます。

<a href="" id="system-power-transitions"></a>[システムの電源切り替え](#st1)  
システムの電源イベントが繰り返し発生した後で、製品の信頼性をテストします。

<a href="" id="transfer-events"></a>[イベントの転送](#st2)  
複数の転送および接続イベントを生成します

<a href="" id="plug-and-play--pnp-"></a>[プラグアンドプレイ (PnP)](#st3)  
さまざまな PnP シーケンスを生成します。

<a href="" id="device-topology"></a>[デバイストポロジ](#st4)  
製品を使用して、さまざまなデバイスとトポロジをテストします。

## <a href="" id="ft1"></a>FT Case 1: デバイス列挙型


適用対象: システム、ドッキング、デバイス

**デバイスの列挙が機能していることを確認するには**

1.  テストシステムを再起動し、Windows にログオンします。
2.  テストシステムで**デバイスマネージャー**を開きます。 **[スタート]** の **[検索]** テキストボックスに「 **devmgmt.msc** 」と入力します。
3.  デバイスを USB タイプ C 対応システムに接続します。 必要に応じて、デバイスの電源が入っているか、外部電源に接続されていることを確認します。
    -   システム: USB タイプ C デバイスをシステムに接続します。
    -   デバイス: デバイスを USB タイプ C 対応システムに接続します。
    -   Dock: 任意の USB 3.0 デバイスと、代替モードをサポートする USB タイプ C デバイス、または USB タイプ C アクセサリ (ドック) に接続します。 Dock をシステムに接続します。

4.  デバイスノードが**デバイスマネージャー**に追加されていることを確認します。 詳細については、「[デバイスの追加を確認する方法](#add)」を参照してください。
5.  接続されているデバイスがエラーなしで機能していることを確認します。
6.  デバイスを切断し (該当する場合は dock)、**デバイスマネージャー**の変更を観察します。 ドッキングとデバイスは**デバイスマネージャー**に表示されません。 詳細については、「[デバイスの削除を確認する方法](#remove)」を参照してください。
7.  USB タイプ C ケーブルの向きを[反転または反転](#flip)し、手順 3. ~ 6. を繰り返します。

## <a href="" id="ft2"></a>FT ケース 2: システムブート


適用対象: システム、ハブ、デバイス

**テスト対象の製品が通常のシステムブートプロセスを妨げていないことを確認するには**

1.  テストシステムを再起動し、Windows にログオンします。
2.  USB タイプ C ポートが公開されているシステムに、次の USB デバイスを接続します。
    -   システム: 次の図に示すように、USB タイプ-C から USB タイプのアダプターを使用して、これらのデバイスをシステムの公開された USB タイプ C ポートに接続します。

        ![usb タイプ-c 構成](images/typec4.png)

        -   USB ハブ
        -   USB キーボード
        -   USB 3.0 フラッシュドライブ
    -   Dock: テスト対象の dock で公開されているポートにこれらのデバイスを接続します。
        -   USB ハブ
        -   USB キーボード
        -   USB 3.0 フラッシュドライブ
    -   デバイス: システムの公開されている USB タイプ C ポートにデバイスを接続します。

3.  テストシステムで**デバイスマネージャー**を開きます。 **[スタート]** の **[検索]** テキストボックスに「 **devmgmt.msc** 」と入力します。
4.  デバイスノードが**デバイスマネージャー**に追加されていることを確認します。 詳細については、「[デバイスの追加を確認する方法](#add)」を参照してください。
5.  システムを再起動します。システムがシャットダウンして正常に起動することを確認します。 システムエラーがある場合は調査します。
6.  システムまたはドッキングテストの場合は、次のことを確認します。
    -   USB フラッシュドライブは、起動可能なメディアとして UEFI/BIOS によって認識され、システムを起動することができます。
    -   USB キーボードは UEFI/BIOS によって認識され、UEFI/BIOS に入るために使用できます。

7.  システムが起動したら、デバイスが**デバイスマネージャー**に表示されていることを確認し、適切に列挙されたことを示します。
8.  接続されているすべてのデバイスのデバイス機能を検証します。
9.  システムの場合、手順 3. ~ 8. を繰り返します。そのためには、これらのデバイスを dock に接続して、USB タイプ C ドックをシステムに接続します。
    -   USB ハブ
    -   USB キーボード
    -   USB 3.0 フラッシュドライブ

## <a href="" id="ft3"></a>FT ケース 3: システムの電源切り替え


適用対象: システム、ドッキング、デバイス

**システムの電源切り替えと、低い電力状態からのウェイクアップ機能が製品の影響を受けないことを確認するには**

1.  テストシステムを再起動し、Windows にログオンします。
2.  USB 3.0 ハブを、システムの公開されている USB タイプ C ポートに接続します。 詳細については、「[デバイスをシステムに接続する方法](#connect)」を参照してください。
3.  USB デバイスをハブに接続します。
4.  テストシステムで**デバイスマネージャー**を開きます。
5.  **デバイスマネージャー**にデバイスが追加されていることを確認します。 詳細については、「[デバイスの追加を確認する方法](#add)」を参照してください。
6.  次に説明する [スタート] メニューまたはオートメーションを使用して、システムをスリープや休止などの低い電力状態に送信します。
7.  システムを低電力状態からウェイクアップします。 デバイスでリモートウェイクがサポートされている場合は、デバイスを使用してシステムを復帰させることができます。 詳細については、「[システムウェイクのトラブルシューティング](#wake)」を参照してください。 それ以外の場合は、(電源ボタンまたはキーボードを使用して) システムを通常どおりスリープ解除します。
8.  デバイスがまだ機能していることを確認します。 詳細については、「[デバイスの機能を確認する方法](#function)」を参照してください。

使用可能な他のシステム電源の状態 (スリープ (S3)、休止状態 (S4)、およびハイブリッドスリープ) に対して、このテストを繰り返します。

Windows Driver Kit (WDK) に含まれている pwrtest .exe を使用  **こと**で、電源の状態への移行を簡略化できます。 詳細については、「 [Pwrtest](https://docs.microsoft.com/windows-hardware/drivers/devtest/pwrtest)」を参照してください。

 

## <a href="" id="ft4"></a>FT ケース 4: セレクティブサスペンド


適用対象: Dock、デバイス

**デバイスが選択的中断に移行することを確認するには**

1.  テストデバイスとシステムの間で USB バスアナライザーを接続します。 詳細については、「[アナライザーを使用した選択的中断の確認](#analyzer)」を参照してください。
2.  キャプチャセッションを開始します。
3.  デバイスが選択的中断に入ることを許可します。 15秒間待機して、デバイス上で転送がアクティブになっていないことを確認します。 たとえば、テストデバイスがフラッシュドライブの場合は、ファイルが開いていないことを確認します。キーボードまたはマウスの場合は、デバイスをアイドル状態のままにします。
4.  アクションを実行して、デバイスをセレクティブサスペンド状態からウェイクアップします。 たとえば、フラッシュドライブでファイルを開きます。キーボードの場合は、キーを押すか、マウスを動かします。
5.  アナライザーで、デバイスがセレクティブサスペンド状態になったことを確認します。

選択的中断の追加情報については、次のソースを参照してください。

-   [HID のセレクティブサスペンドを有効にする](https://go.microsoft.com/fwlink/p/?LinkId=623307)
-   [USB デバイスを使用した HID のセレクティブサスペンド](https://docs.microsoft.com/windows-hardware/drivers/hid/selective-suspend-for-hid-over-usb-devices)
-   [Demystifying の選択的な中断]( https://go.microsoft.com/fwlink/p/?LinkId=623308)

## <a href="" id="ft5"></a>FT Case 5: ドック識別


適用対象: Dock

1.  テストシステムを再起動し、Windows にログオンします。
2.  USB タイプ C ドックをシステムに接続します。
3.  Dock の状態が正しく識別されていることを確認します。

**注**  ドック識別に関する追加情報は、2015の[WinHEC スライドプレゼンテーション](https://go.microsoft.com/fwlink/p/?LinkId=623309)に記載されています (「デバイスを Dock として識別する」セクションの「約スライド26」を参照してください)。

 

## <a href="" id="ft6"></a>FT Case 6: 代替モードネゴシエーション


適用対象: システム、ドッキング、デバイス

**サポートされているモードの代替モードネゴシエーションの確認**

1.  テストシステムを再起動し、Windows にログオンします。
2.  テストシステムで**デバイスマネージャー**を開きます。 **[スタート]** の **[検索]** テキストボックスに「 **devmgmt.msc** 」と入力します。
3.  代替モードが有効な USB タイプ C デバイスを、システムの代替モードが有効な USB タイプ C ポートに接続します。デバイスとシステムの両方が少なくとも1つの代替モードを共有し、必要に応じてデバイスの電源が入っているか、外部電源に接続されていることを確認します。
    **注**  タイプ C ドングル/アダプターの場合は、適切な周辺機器の電源が入っていて、ドングル/アダプターのタイプ c 以外の端に接続されていることを確認してください。

     

4.  **デバイスマネージャー**に代替モードデバイスが追加されていることを確認します。 場合によっては、代替モードのデバイスがモニターデバイスまたは別のバスデバイスとして表示されることがあります。 詳細については、「[デバイスの追加を確認する方法](#add)」を参照してください。
5.  デバイスを切断し、**デバイスマネージャー**の変更を監視します。 ハブとデバイスは**デバイスマネージャー**に表示されなくなります。 詳細については、「[デバイスの削除を確認する方法](#remove)」を参照してください。
6.  USB タイプ C ケーブルの向きを[反転または反転](#flip)し、手順2-5 を繰り返します。

## <a href="" id="ft7"></a>FT ケース 7: 課金と電力配信 (PD)


適用対象: システム、dock、USB 電力配信プロトコルをサポートするデバイス

**USB タイプを使用した充電の確認-C**

1.  USB.org による定義に従って、 [USB 電源配布テスト]( https://go.microsoft.com/fwlink/p/?LinkId=623310)を実行します。
2.  テストシステムを再起動し、Windows にログオンします。
3.  システムの場合は、次の手順を実行します。
    1.  USB タイプ C ケーブルを使用して、2つのシステムを接続します。 現在のシステムを受信しているシステムが1つだけであることを確認します。
    2.  システムに複数の USB タイプ C ポートが含まれている場合は、USB タイプ C ケーブルで同じシステム上の2つの USB タイプ C ポートを接続します。 システムが充電されていないことを確認します (それ自体は)。
    3.  バンドルされている USB タイプ-C チャージャー (バンドルされている場合) をシステムの USB タイプ C ポートに接続します。 システムが充電されていることを確認します。
    4.  他のソースからの USB タイプ-C 充電器を使用して、上記の手順 3c. を繰り返します。
    5.  USB タイプ C デバイスを、USB タイプ C ポートを公開したシステムに接続します。 デバイスが現在受信していることを確認します。

4.  Dock の場合は、次の手順を実行します。
    1.  Usb タイプの c が有効なシステムに dock を接続します。
    2.  Dock がシステムの接続を充電していることを確認します。

5.  デバイスの場合は、次の手順を実行します。
    1.  デバイスを USB タイプ C 対応システムに接続します。 デバイスがシステムから電力を受け取ることを確認します。
    2.  optionalデバイスを USB タイプ C 対応システムに接続します。 デバイスがシステムに課金されることを確認します。

## <a href="" id="ft8"></a>FT ケース 8: ロールのスワップ


適用対象: システム

**ロールのスワップの確認**

1.  テストシステムを再起動し、Windows にログオンします。
2.  USB タイプ C ケーブルを使用して、2つのシステムを接続します。
3.  各システムの現在のロールを確認します。
4.  役割をスワップするために必要な手順を実行します。
5.  各システムの現在のロールが変更されたことを確認します。

## <a href="" id="st1"></a>ST Case 1: システムの電源切り替え


適用対象: システム、ドッキング、デバイス

1.  テストシステムを再起動します。
2.  USB SuperMUTT デバイスを、公開されている USB タイプ C ポートに接続します。
3.  [(認定) テスト中に、IO を使用して DF-スリープ]( https://go.microsoft.com/fwlink/p/?LinkId=623311)を実行します。
4.  USB タイプ C テストデバイスで手順 3. を繰り返します。

## <a href="" id="st2"></a>ST Case 2: 転送イベント


適用対象: システム、ドッキング、デバイス

1.  テストシステムを再起動します。
2.  USB SuperMUTT デバイスを、公開されている USB タイプ C ポートに接続します。
3.  テストの[前後に、i/o を使用した DF 再](https://go.microsoft.com/fwlink/p/?LinkId=623312)起動の再起動を実行します。
4.  USB タイプ C テストデバイスで手順 3. を繰り返します。

## <a href="" id="st3"></a>ST Case 3: プラグアンドプレイ


適用対象: システム、ドッキング、デバイス

1.  テストシステムを再起動します。
2.  USB SuperMUTT デバイスを、公開されている USB タイプ C ポートに接続します。
3.  テストの[前後に、i/o で DF-スリープと PnP]( https://go.microsoft.com/fwlink/p/?LinkId=623313)を実行します。
4.  USB タイプ C テストデバイスで手順 3. を繰り返します。

## <a href="" id="st4"></a>ST ケース 4: デバイストポロジ


適用対象: システム、ドッキング、デバイス

1.  テストシステムを再起動します。
2.  USB タイプ C A/V アダプタを使用すると、A/V アダプタのすべてのポートを接続し、次の図に示すようにすべての機能を使用できるようになります。

    ![usb タイプ-c a/v アダプター構成](images/typec5.png)

3.  テスト対象のシステムに追加の USB タイプ C ポートがある場合は、手順 2. を繰り返します。
4.  テスト[中に i/o を使用して DF-Sleep]( https://go.microsoft.com/fwlink/p/?LinkId=623314)を実行します。

**注**  テスト中に、オーディオタイプ-C A/V ドングルを介して接続されているデバイスからの glitching がないことを検証します (ビデオのひずみや audio のドロップダウンなど)。

 

## <a href="" id="ft-plan"></a>機能システム相互運用性テスト計画


予想される期間:20 分

この計画の目的は、システムがさまざまな種類の周辺機器と充電器を使用できるかどうかを判断することです。 このテスト計画は、システムの OEM 以外のソースからのテストに重点を置いています。

-   システム: USB タイプ C ポートが公開された Windows 10Windows 10 システム (PC、タブレット、スマートフォン)。
-   周辺機器
    -   USB タイプ-A から USB タイプ-C アダプター
        -   USB 3.0 ハブ
        -   USB マウス
        -   USB 3.0 フラッシュドライブ
    -   USB タイプ-C ストレージドライブ
    -   USB タイプ-C ビデオ (ドングルは使用可能)
-   電源: USB タイプ-C 充電装置

<!-- -->

-   「 [FT Case 1:](#ft1) USB タイプのデバイス列挙-C ドングル」を実行します。 各デバイスが予期したとおりに機能していることを確認します。 このイメージは、USB タイプをドングルとしてテストするために推奨されるトポロジを示しています。

    ![usb タイプをテストするためのトポロジ (ドングル)](images/typec1.png)

-   [FT ケース 6:](#ft6)リスト内の残りの周辺機器の代替モードネゴシエーションを実行します。 各デバイスが予期したとおりに機能していることを確認します。
-   FT ケース7の縮小版を実行します。 USB タイプ-C チャージャーを使用して、[課金と電力配信 (PD)](#ft7)を行います。 2台のコンピューターを必要とするセクションをスキップし、サードパーティ製の電源アダプターでシステムが充電 (受け入れ) できることのみを検証します。

## <a name="usability-system-interoperability-test-plan"></a>ユーザビリティシステム相互運用性テスト計画


予想される期間:60 分

この計画の目的は、このシステムで USB タイプ C 周辺機器を使用する最も一般的なユーザーシナリオを実行できるかどうかを判断することです。 このテスト計画は、[機能システムの相互運用性テスト計画](#ft-plan)に記載されているテストが正常に完了したことを前提としています。 ユーザビリティテスト計画では、一般的なユーザー、システム、およびデバイスのシナリオに焦点を当てています。

-   システム: USB タイプ C ポートが公開された Windows 10Windows 10 システム (PC、タブレット、スマートフォン)。
-   周辺機器
    -   USB タイプ-A から USB タイプ-C アダプター
        -   USB 3.0 ハブ
        -   USB マウス
        -   USB 3.0 フラッシュドライブ
    -   USB タイプ-C ストレージドライブ
    -   USB タイプ-C ビデオ (ドングルは使用可能)
    -   USB タイプ-C A/V ドングル (1 つのアダプターとしてビデオ、USB、および場合によってはオーディオの両方を含む)
-   電源: さまざまなサプライヤーからの2つの USB タイプ C 充電器。

<!-- -->

-   「 [FT](#ft3) (USB)」と入力して、リスト内の各周辺機器のシステムの電源の移行を実行します。 各デバイスで、システムの電源状態が変更される前と処理後に、予期したとおりに機能していることを確認します。
    -   次の図に示すように、usb タイプ-A から USB タイプ C アダプターを構成します。

        ![usb タイプをテストするためのトポロジ (ドングル)](images/typec1.png)

    -   このイメージに示されているように、USB タイプ-C A/V ドングルを構成します。

        ![usb タイプ-c a/v ドングルの構成](images/typec2.png)

<!-- -->

-   [FT ケース 2:](#ft2)前の図に示されているように USB タイプ-C A/V ドングルのみを使用してシステムを起動し、次のシナリオを検証します。
    -   システムは接続されているすべてのデバイスで起動し、ビデオは USB タイプ-C A/V ドングルを介して接続されたモニターに表示されます。
    -   システムは、USB タイプ-C A/V ドングルを使用して接続された USB ディスクから起動します。

## <a name="full-interoperability-test-plan"></a>完全な相互運用性のテスト計画


予想される期間: 180 + 分

完全な相互運用性のテスト計画では、より多くのユーザーシナリオに対応しています。 これらのテストは、デバイスのシステムで USB 対応の準備ができている場合に実行します。

-   Systems
    -   USB タイプ C ポートが公開されている windows 10Windows 10 システム (PC、タブレット、または電話)。
    -   USB タイプ C ポートが公開された追加の Windows 10 システム (PC、タブレット、スマートフォン)。 USB タイプの C ポートを公開したシステム (PC、タブレット、または電話)。 別の製品ラインまたは OEM のシステムをお勧めします。
-   周辺機器
    -   USB タイプ-A to Type-C adapterUSB Type-A to USB Type-C アダプター
        -   USB 3.0 ハブ
        -   USB マウス
        -   USB 3.0 フラッシュドライブ
    -   USB タイプ-C ストレージドライブ
    -   USB タイプ-C ビデオ (ドングルは使用可能)
    -   USB タイプ-C A/V ドングル (1 つのユニットとしてビデオ、オーディオ、USB を含む)
-   電源: さまざまなサプライヤーからの2つの USB タイプ C 充電器。

<!-- -->

-   すべての関数ストレステストケースを実行します。 次の図に、USB の種類-C A/V について推奨される構成を示します。

    ![usb タイプ-c a/v アダプター構成](images/typec3.png)

## <a href="" id="add"></a>デバイスの追加を確認する方法


-   デバイスが接続されている USB ホストコントローラーを特定します。
-   新しいデバイスが**デバイスマネージャー**の適切なノードの下に表示されていることを確認します。
-   Usb 3.0 ポートに接続されている USB 3.0 ハブの場合、2つのデバイスが表示されることを想定しています。1つは USB 3.0 の下流で、もう1つは全速度ハブの下流です。

## <a href="" id="remove"></a>デバイスの削除を確認する方法


-   **デバイスマネージャー**でデバイスを識別します。
-   テストステップを実行して、システムからデバイスを削除します。
-   **デバイスマネージャー**にデバイスが存在しないことを確認します。
-   USB 3.0 ハブの場合は、両方のデバイス (SuperSpeed とコンパニオンハブ) が削除されていることを確認します。 この場合、デバイスの削除に失敗すると、デバイスエラーになる可能性があります。また、適切な根本原因のトリアージに関係するすべてのコンポーネントによって調査する必要があります。

## <a href="" id="function"></a>デバイスの機能を確認する方法


-   デバイスが USB ハブの場合は、ハブの下流にあるデバイスが機能していることを確認します。 他のデバイスがハブの使用可能なポートに接続できることを確認します。
-   デバイスが HID デバイスの場合は、その機能をテストします。 USB キーボードの種類、USB マウスがカーソルを動かし、ゲームコントローラーのコントロールパネルでゲームデバイスが機能していることを確認します。
-   USB オーディオデバイスは、サウンドを再生または録音する必要があります。
-   記憶装置にアクセスできる必要があり、200 MB 以上のサイズのファイルをコピーできる必要があります。
-   デバイスにスキャン & 印刷などの複数の機能がある場合は、必ずスキャン機能と印刷機能の両方をテストしてください。
-   デバイスが USB タイプ C の場合は、該当する USB および代替モードが機能していることを確認します。

## <a href="" id="connect"></a>デバイスをシステムに接続する方法


-   USB 2.x デバイスで、テストデバイスに適した USB 2.x ケーブルが使用されていることを確認します。
-   デバイスがシステムによって認識されない場合は、デバイスを同じ種類の別のケーブルで接続して、正しくないケーブルまたはコネクタがないかどうかを確認します。

## <a href="" id="wake"></a>システムウェイクのトラブルシューティング


システムをウェイクアップできないデバイスのトラブルシューティングを行うには、次のようにします。

-   デバイスがウェイクアップに対応していることを確認します。
-   デバイスが接続されているホストコントローラーがシステムをウェイクアップするように設定されていることを確認します。

## <a name="troubleshooting-missing-power-states"></a>不足している電源状態のトラブルシューティング


テストシステムがスリープ状態または休止状態にならない場合は、システム内のすべてのデバイスに最新のデバイスドライバーがインストールされていることを確認してください。 最も一般的な原因の1つは、システムでサポートされていないビデオカードです。 システムの電源状態の問題を解決する方法の詳細については、「[スリープを使用できない理由]( https://go.microsoft.com/fwlink/p/?LinkId=623315)」を参照してください。

## <a name="using-etw-to-log-issues"></a>ETW を使用した問題のログ記録


USB 2.0 ポートの ETW を有効にするには、「 [Windows 7 の usb コアスタックの etw](https://go.microsoft.com/fwlink/p/?LinkId=623316)」を参照してください。

USB 3.0 ログ記録を有効にするには、代わりに次のコマンドを実行します (または、「Logman を使用して[usb イベントトレースをキャプチャする方法](how-to-capture-a-usb-event-trace.md)」を参照してください)。

``` syntax
logman start usbtrace -ets -o usbtrace.etl -nb 128 640 -bs 128
logman update usbtrace -ets -p Microsoft-Windows-USB-UCX Default
logman update usbtrace -ets -p Microsoft-Windows-USB-USBHUB3 Default
```

これらのログがキャプチャされたら、テストシナリオを実行します。

次のコマンドを使用してトレースを停止します。

``` syntax
logman stop usbtrace -ets
```

## <a href="" id="analyzer"></a>アナライザーを使用して選択的中断を確認する


USB 2.0 と3.0 のトラフィックを分析するには、LeCroy Voyager M3i、Advisor T3、TotalPhase Beagle 5000 などの USB アナライザーデバイスが必要です。 これらのアナライザーは、選択的中断機能を確認するために必要なリンク状態情報をキャプチャして表示することができます。

たとえば、TotalPhase analyzer を使用してトラフィックをキャプチャした後、出力には次のようなイベントが表示されます。

![usb タイプ-c アナライザー](images/typec-analyzer.png)

デバイスが中断状態になることをテストで要求している場合は、上記の &lt;Suspend&gt; イベントと、デバイスが中断状態になることが予想される時刻を関連付けることができます。

## <a name="using-an-analyzer-to-confirm-lpm-u1-and-u2-transitions"></a>アナライザーを使用して、LPM U1 と U2 遷移を確認する


Analyzer トレースは、すべてのリンク状態遷移を明示的に表示する必要があります。ステートメントは、イベントに "Rx U0-&gt; U2" として表示されます。 たとえば、LeCroy ソフトウェアを使用して、 **[レポート]** タブの [ **USB3] リンク状態のタイミングビュー**を選択します。 このオプションは、タイム軸のリンク状態を示します。 Analyzer によって、U2 が正しく移行されない場合があることに注意してください。 リンクの状態は U1 になりますが、U2 から回復している可能性があります。

## <a name="disabling-selective-suspend-in-device-manager"></a>デバイスマネージャーでのセレクティブサスペンドの無効化


デバイスマネージャーで USB デバイスのセレクティブサスペンドを無効にするには、まずデバイスツリーでデバイスノードを見つけます。 この例では、次に示すハブのセレクティブサスペンドを無効にします。

![デバイス マネージャー](images/typec-device-mgr.png)

デバイスを右クリックし、 **[プロパティ]** を選択します。 次に、 **[電源管理]** タブを選択します。

![デバイス マネージャー](images/typec-device-mgr1.png)

セレクティブサスペンドを無効にするには、[**コンピューターがこのデバイスの**電源をオフにして電源を入れることを許可する] チェックボックスがオフになっていることを確認します。

## <a href="" id="flip"></a>USB タイプ C ケーブルを反転または反転する


USB タイプ C ケーブルは、ケーブルの向きに関係なくユーザーの機能を維持することを目的としています。 ケーブルを交換するには、ケーブルを取り外し、180度回転して、ケーブルを再度取り付けます。

## <a name="reporting-test-results"></a>テスト結果のレポート


次の詳細を指定します。

-   失敗したテストの前に実行されたテストの一覧 (順)。
-   一覧には、失敗または成功したテストを指定する必要があります。
-   テストに使用されたシステム、デバイス、ドッキング、またはハブ。 必要に応じて追加情報を取得できるように、make、model、および Web サイトを含めます。

 

 




