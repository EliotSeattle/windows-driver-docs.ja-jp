---
title: ドライバーのフライティング
description: パートナー センターでドライバーをフライティングすると、定義した Windows Insider リング内でドライバーを配布して、自動的に監視および評価することができます。
ms.date: 07/27/2018
ms.topic: article
ms.localizationpriority: medium
ms.openlocfilehash: a6cf66d1d57bc66da2f732db121470f17240709b
ms.sourcegitcommit: 5598b4c767ab56461b976b49fd75e4e5fb6018d2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2020
ms.locfileid: "63335119"
---
# <a name="driver-flighting"></a>ドライバーのフライティング

パートナー センターでドライバーをフライティングすると、定義した Windows Insider リング内でドライバーを配布して、自動的に監視および評価することができます。 フライトの完了後、ドライバーのパフォーマンス レポートが生成され、それに基づいてドライバーの重要な機能を評価し、シナリオを改善できます。 フライトが成功し、マイクロソフトの承認が得られると、ドライバーが Windows Update を通じて一般ユーザーに配布されます。 

次のビデオでは、ドライバーのフライティング プログラムの概要をさらに詳しく説明します。 
<iframe src="https://channel9.msdn.com/Events/WinHEC/WinHEC-Online/Start-Your-Driver-Flighting-The-benefit-of-Driver-Promotion/player" width="960" height="540" allowFullScreen frameBorder="0"></iframe>

## <a name="signing-up-for-driver-flighting"></a>ドライバーのフライティングへのサインアップ

ドライバーのフライティングにサインアップするには、パートナー センターにサポート チケットを送信します。 パートナー センターのサポートには、以下に示すようにブラウザーのウィンドウの右上隅でアクセスできます。

![パートナー センターのサポートにアクセスするためのボタン](images/support.jpg)

> [!NOTE]
> ドライバーのフライティングにサインアップするときに、パートナー センター内にいることを確認します。 パートナー センターの別の領域からのサポート ボタンをクリックすると、非ダッシュ ボード サポート グループに接続します。

チケットには、以下の各項目を明記します。

- ドライバーのターゲットとなる既存の推定デバイス数
- 1 か月あたりのプロモーション要求の推定ボリューム
- 販売者 ID または発行元 ID (あるいはその両方)

サポート チケットがマイクロソフトに届いてから、結果が通知されるまで最大 5 営業日かかる場合があります。

アカウントが承認されると、組織の管理者は **[設定]** ページの **[ユーザーの管理]** にアクセスしてフライティング用にユーザーを構成できるようになります。 対象のユーザーが、以下のいずれかの役割を持っていることを確認してください。

- 配送先住所ラベルの所有者
- 配送先住所ラベルのプロモーター

## <a name="how-to-promote-a-driver-for-driver-flighting"></a>ドライバーのフライティング用にドライバーをプロモーションする方法

パートナー センターに提出されたドライバーは、次の手順に従ってフライティング用にプロモーションできます。

1. ドライバーが提出され、プロセスの**検証**段階に入ったら、新しい配送先住所ラベルを作成し、 **[詳細]** と **[プロパティ]** のセクションに必要事項を記入します。 詳しくは、「[Windows Update にドライバーを公開する](https://docs.microsoft.com/windows-hardware/drivers/dashboard/publish-a-driver-to-windows-update)」をご覧ください。

2. 次の説明に従って、1 つまたは複数のドライバーのプロモーション オプションを選択して、ドライバーをフライティング用にプロモーションします。

|                            プロモーションのオプション                             |                                                               説明                                                                |
|-------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------|
|   Windows のアップグレード時にドライバーを自動的に配信してインストールする   | ドライバーが動的更新によって配信されるプログラムとしてマークされ、オペレーティング システムのアップグレード時に、適用可能なコンピューターに配信できるようになります。 |
| 適応可能なすべてのシステムに、ドライバーを自動配信してインストールする |                ドライバーが重要な更新プログラム (CU) としてマークされ、Windows Update 経由で自動的にインストールできるようになります。                 |

3. フライティング用のプロモーションに必要なその他の詳細情報を指定します。
    1. プロモーションについて協力しているマイクロソフト スポンサーのメール アドレス
    2. 公開要求をプロモーションするビジネス上の妥当性
    3. ドライバーの品質検証プロセス
    4. ドライバーの公開によって影響を受ける OEM (存在する場合)

4. 次のうち、ドライバーに当てはまる項目を選択します。 この情報は、評価プロセスの迅速化に役立ちます。![フライティング対象のドライバーを説明する選択肢の画像: 選択肢は、"共同エンジニアリング ドライバーである"、"再起動が必要"、"UI やソフトウェアを展開する"、"新しいまたは未リリースのデバイスをサポートする" です](images/driver-flighting-statements.png)

    > [!IMPORTANT] 
    > 以下の点に注意してください。
    > * ドライバーのインストール後の再起動は、可能な限り避けてください。 
    > * インストール時に UI やソフトウェアを展開するドライバーは S モードの Windows 10 に準拠しないため、このオペレーティング システムに対するフライティングは実施できません。
    > * 共同エンジニア リング ドライバーは、リリース前のバージョンの Windows 用に開発されているドライバーです。 共同エンジニア リング ドライバー: 
    >    * フライティング プロセス中に、Microsoft Insider Program に参加しているデバイスにのみ配布されます。
    >    * フライトの成功後、Microsoft Insider Program に参加していないデバイスには配布されません。
    >    * 60 日後に、フライティングが終了となります。 フライティング プロセスの完了後、フライト バグ レポートが提供されます。 

5. 通常どおり配送先住所ラベルの処理を完了します。

ドライバーを配送用にプロモーションすると、マイクロソフトはドライバーを承認するかどうかを評価し、評価完了時 (通常、配送先住所ラベルの発行から 2 週間以内) にドライバーのフライティング レポートを提供します。 以前作成された出荷ラベルを再利用した場合、発行日が更新されないことに注意してください。

## <a name="reasons-a-driver-may-be-rejected"></a>ドライバーが却下される場合がある理由

ドライバーの却下には、いくつかの理由が考えられます。 ほとんどの場合、却下の原因はドライバーのターゲットの問題です。 具体的な内容は次のとおりです。

- Windows 10 だけでなく、以前のバージョンの Windows を併せてターゲットとしている。
- ターゲットとするデバイス クラスに、適切に従わなかった特定の CHID ターゲット要件がある可能性がある。  一部のデバイス クラスで Firmware のような CHID を必要とし、その他のクラスでは、Display のような CHID の使用が禁止されている。  情報を正しく入力したことを確認してください。
- 他の OEM をターゲットとするハードウェア ID を誤って使用している。

## <a name="related-topics"></a>関連トピック

- [新しいハードウェア申請を作成する](create-a-new-hardware-submission.md)
- [パートナー センターでハードウェア申請を管理する](manage-your-hardware-submissions.md)
- [複数の Windows バージョンで Microsoft によって署名されたドライバーを取得する](get-drivers-signed-by-microsoft-for-multiple-windows-versions.md)
