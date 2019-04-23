---
Description: Guidelines for hardware vendors and device manufacturers to prepare USB devices and host controllers for Windows Hardware Certification Program submission.
title: USB-IF 認定テスト
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 51b5169c89d717d031dc5e43f0b7e548ba717cf6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571932"
---
# <a name="usb-if-certification-tests"></a>USB-IF 認定テスト


Windows ハードウェア認定プログラムの提出の USB デバイスとホスト コント ローラーを準備するには、ハードウェア ベンダーとデバイスの製造元に関するガイドラインです。

## <a name="usb-if-certification-tests"></a>USB-IF 認定テスト


USB のハードウェアを製造する場合は、具体的には USB デバイスまたはホスト コント ローラー、ハードウェアは USB の電気で機械的な要件を満たす必要があります-Windows 証明書を受信するには場合。 USB の認定の USB デバイスとホスト コント ローラーのさらに詳細なテストについて説明し、高品質な実装によりかどうか。

以前のバージョン、Windows ハードウェア認定キットに必要なハードウェアの製造元がデバイスを USB を送信する-テストの場合。 ただし、その要件が変更されました。 自分のデバイス、usb を送信する必要はなくなり-テストの場合。

HLK、USB の新しいバージョンの要件をテストする場合により、ベンダーをダウンロードして、USB からテストを実行する-場合の web サイト、HLK でこれらのテストが成功することをアサートします。 かどうか、デバイスが USB によって認定されて既に-USB を提供する必要がある場合は、-、HLK にデバイスの場合にテスト ID (TID)。

場合でも、USB デバイスは、現在の Microsoft Windows 認定プログラム要件を満たす、それらのデバイスの多くを完全に準拠していない USB 仕様に準拠します。 最も一般的な例は次のとおりです。

-   **ハブ**:外部であることをレポートするためによく発生ときに電源が実際に唯一バスの電源が入っています。 False のレポートは、バス上、電圧の無効な状態につながります。
-   **ハード ディスク ドライブ**:USB バスからの電力の過剰描画のため正しく、列挙しないため、よく発生します。 多くの状況では、外付けハード ディスク ドライブには、正常に動作する非標準のケーブルが必要があります。
-   **フラッシュ ドライブ**:記述子の要求を正しく処理しないために、一般的な失敗します。これにより、デバイスにハングを Microsoft オペレーティング システムの記述子は失敗します。
-   **カード リーダー**:セレクティブ サスペンド状態に入るされません一般的失敗します。
-   **プリンター**:スタンバイから再開しないでためによく発生します。
-   **オーディオ**:スタンバイから再開しないでためによく発生します。

非準拠の USB デバイスには、ユーザー エクスペリエンスの低下、困難な広報、製品および収益、高い製品のサポートの問い合わせ件数、および出荷された製品のバグをサービスに関連付けられているコストの増加が失われる可能性があります。
## <a name="windows-hlk-requirements-for-usb-if-tests"></a>USB の Windows HLK 要件-IF テスト


-   デバイス (**Device.Connectivity.UsbDevices.UsbifCertification)**

    USB を強くお勧めの場合に証明します。ただし、Windows HLK 要件**Device.Connectivity.UsbDevices.UsbifCertification** USB は不要の USB デバイスの場合に証明します。 要件は、デバイスは USB のいずれかであることを示す-認定を受けている場合や、USB のサブセットのデバイスの場合の認定テストを実行することができます。

-   ホスト コント ローラー (**Device.BusController.UsbController.UsbifCertification**)

    USB ホスト コント ローラー製造元は、完全な USB を取得する必要があります-IF 証明、それぞれ Windows HLK 要件を満たすためにします。

-   ハブ (**Device.Connectivity.UsbDevices.UsbifCertification**)

    USB ハブの製造元は、完全な USB を取得する必要があります-IF 証明、それぞれ Windows HLK 要件を満たすためにします。

そのシステムに統合 USB ホスト コント ローラーを選択したときに、システム製造元は、それらの要件に注意してくださいにあります。 これらの要件は、USB デバイスで、カスタマー エクスペリエンスを大幅に改善できます。 クラッシュやハングの主な理由を回避し、トラブルシューティングを行うし、非対応の問題をデバッグするために費やされた時間を短縮できます。

## <a name="windows-hardware-certification-submission-options"></a>Windows ハードウェア認定の送信オプション


このイメージは、Windows 証明書を取得する方法のプロセス フローを示しています。

![usb のテストの場合](images/usbif-testing.png)

Windows 認定資格を満たす新しい USB の USB デバイスを送信することができます、次のメソッドのいずれかを使用して要件をテストする場合。

- **USB の場合は認定資格**

  USB の取得-から場合証明、 [USB-独立したテスト ラボを承認されている場合](http://www.usb.org/developers/compliance/labs/)し、Windows の認定資格については、デバイスに送信します。 USB を取得するには、次のオプションのいずれかを選択することができます-デバイスまたはホスト コント ローラーの場合は証明書。

  -   USB デバイスの送信-テスト用の独立したテスト ラボを承認されている場合。 ラボを検索する方法については、USB を参照してください。-独立したテスト ラボを承認されている場合。
      **注**通常は、承認された独立したテスト ラボ 1 ~ 2 週間かかります USB 仕様に準拠する目的の 1 つの USB デバイスをテストします。

         

  -   USB のため、承認された独立したテスト ラボに USB デバイスに送信する-認定資格の場合は、製造元が、ラボで登録し、有効な仕入先 ID (VID) をする必要があります。

  デバイスが USB を正常に通過した後、デバイスの次の特権がある場合は、認定テスト。

  -   パンフレット、パッケージ化、および製品情報、デバイスの USB ロゴを使用できます。
  -   USB 掲載することができます-IF インテグレーターのリスト。
  -   デバイスを持ち込み、[コンプライアンス ワーク ショップの USB 場合スポンサー](http://www.usb.org/developers/events/compshop/)します。 それぞれの年は 4 つのワーク ショップが、米国内で保持されているし、アジアに 1 つのワーク ショップが保持されています。

  デバイスが USB を経過した後のテスト ラボやワーク ショップからテスト ID 番号 (TID) が表示される場合は、認定テスト、します。 デバイスの Windows HLK テストの残りの部分を実行すると、この TID 数を Windows HLK に提供します。

  テストと、承認された独立したテスト ラボでの USB デバイスを認定のコストには、ラボの演習には異なります。 一部承認済みの独立したテスト ラボでは、ボリューム ディスカウントやいくつかの関連企業向けの割引を提供します。 テストおよび任意の USB 場合スポンサー コンプライアンス ワーク ショップでの USB デバイスを認定するためのコストはありません。 USB のメンバーがあります-USB に参加する場合、コンプライアンス ワーク ショップを勧める場合。

- **USB の自己テストがある場合**

  USB コマンド Verifier テスト ツールをダウンロードして、USB の相互運用性のテスト ドキュメントおよびから必要なテストを実行、 [USB-IF](http://www.usb.org/home)します。 Windows 認定資格については、デバイスを次に送信します。

  **注**USB ホスト コント ローラーとハブの USB 資格がありません-場合にセルフ テスト オプションし、完全な USB を取得する必要があります-場合証明。

  USB を使用する場合、Windows の証明書を取得する場合は自己テスト オプション行う必要がありますには少なくとも次の USB-IF テスト。

  -   USB コマンド検証機能をテストします。USB コマンドの検証テストでは、理解し、一般的な USB コマンドも受け入れるようにデバイスの機能を確認します。
  -   USB の相互運用性をテストします。USB の相互運用性のテストでは、機能と他の USB 周辺機器と共存するデバイスの機能を対象します。

  これらのテストでは、ダウンロードされ、Windows HLK の外部で実行することができます。 Windows の最新バージョンのみにこれらのテストを実行する必要がありますに注意してください (USB で指定されたとおりの場合) Windows の複数のバージョンの Windows 証明の認定の USB デバイスを送信している場合でも。 テスト結果は、すべてのバージョンの Windows のすべての Windows 認定提出に適用されます。

  次の手順が必要な USB を実行する方法について説明します-Windows の認定デバイスを修飾する場合にテストします。

  1. USB 3.0 コマンド検証テスト ツール (USB30CV) との相互運用性のテストからドキュメントのダウンロード[SuperSpeed USB ソフトウェアおよびハードウェア ツール](https://go.microsoft.com/fwlink/p/?LinkId=623333)します。
  2. USB の実行-次の表で指定されている USB ハードウェアのテストの場合。

     <table>
     <colgroup>
     <col width="50%" />
     <col width="50%" />
     </colgroup>
     <thead>
     <tr class="header">
     <th>USB のバージョン</th>
     <th>USB-IF テスト</th>
     </tr>
     </thead>
     <tbody>
     <tr class="odd">
     <td>USB 2.0</td>
     <td><p>XHCI ホスト コント ローラーの背後にあるデバイスを接続し、USB 3.0 コマンド Verifier テスト ツール (USB30CV) で [USB 2.0 デバイス] の章 9 テストを実行します。</p>
     <p>EHCI 部分の相互運用性のセクションで説明したように、相互運用性のテストを実行、 <a href="http://compliance.usb.org/resources/GoldSuite%20Test%20Procedure.pdf">GoldSuite テスト手順ドキュメント</a>します。 これらのテストの実行を 2 回: EHCI ホスト コント ローラーの背後にある接続されたデバイスと xHCI ホスト コント ローラーの背後にある接続されたデバイスから 1 つ。</p></td>
     </tr>
     <tr class="even">
     <td>USB 3.0</td>
     <td><p>XHCI ホスト コント ローラーの背後にあるデバイスを接続し、USB 3.0 コマンド Verifier テスト ツール (USB30CV) で [USB 3.0 デバイス] の章 9 テストを実行します。</p>
     <p>」の説明に従って、相互運用性のテストを実行、 <a href="https://go.microsoft.com/fwlink/p/?LinkId=623335" data-raw-source="[XHCI Interoperability Testing](https://go.microsoft.com/fwlink/p/?LinkId=623335)">XHCI の相互運用性のテスト</a>ドキュメント。 これらのテストを 2 回実行: EHCI ホスト コント ローラーの背後にある接続されたデバイスの 1 つの時間と xHCI ホスト コント ローラーの背後にある接続されたデバイスの 1 つの時刻。</p></td>
     </tr>
     </tbody>
     </table>
    
  3. テストが成功すると、文字列"SELFTEST"テスト ID (TID) として、USB への入力を入力します。-、HLK で IF 証明検証テスト。

## <a name="related-topics"></a>関連トピック
[USB の Windows ハードウェア ラボ キット テスト](windows-hardware-certification-kit-tests-for-usb.md)  


