---
title: ELAM の前提条件
description: 早期起動マルウェア対策 (ELAM) ドライバーは、検証と文書化されている要件に準拠していることを確認に記載されている手順を使用して送信できます。
ms.assetid: ''
ms.date: 04/27/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5c19c473123fab03d9077931a47a7a4c03b66594
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550364"
---
# <a name="elam-driver-submission-process"></a>ELAM ドライバーの送信プロセス

次の手順は、送信、早期起動マルウェア対策 (ELAM) ドライバーを使用できます。

1. ELAM ドライバーの文書化されている要件に準拠するには、ドライバーを確認します。  参照してください[ELAM ドライバーの要件](elam-driver-requirements.md)と[INF SignatureAttributes セクション](inf-signatureattributes-section.md)詳細についてはします。

2. ハードウェア ロゴ キット (HLK) とハードウェア認定キット (HCK) を使用して、ドライバーを検証します。 Windows 8 と Windows 10 では、ドライバーを使用する場合は、キットの両方のバージョンを実行する必要があります。 送信時に結果が含まれます。 参照してください[HLK ツールのテクニカル リファレンス](https://msdn.microsoft.com/library/windows/hardware/dn939924)詳細についてはします。 必須の HCK テストについては、以下を参照してください。

3. カーネル モード ドライバーで説明したように、署名ポリシーに従って、[ドライバーの署名ポリシー](https://docs.microsoft.com/windows-hardware/drivers/install/kernel-mode-code-signing-policy--windows-vista-and-later-)トピック。

4. 評価にドライバー パッケージの送信、 [Windows ハードウェア デベロッパー センター](https://developer.microsoft.com/windows)

各ドライバーの .sys ファイルは、初期起動 AM ドライバーであることを示す特別な証明書を使用して、Microsoft によって署名されたコードである必要があります。

AM ドライバーが 1 つのバイナリにする必要があります (その他の任意の Dll をインポートできません)。

## <a name="hardware-certification-kit-tests"></a>ハードウェア認定キット テスト


各ドライバーの以前の Windows 10 オペレーティング システムを対象とするには、ISV によって管理されます。 次の HCK テストを渡す必要があります。

パフォーマンス テスト
-   コールバックの待機時間、各起動時 AM ドライバーは、.5ms 内でのカーネル ドライバーの検証コールバックを返す必要があります。 この時間は、カーネルがドライバーをドライバーが、コールバックが応答するまでに、コールバックを発行するから測定されます。
-   メモリの割り当て - 各起動時 AM ドライバーは、128 KB で、ドライバーのイメージとその構成 (署名) データの両方のメモリのフット プリントを制限する必要があります。
-   アンロード ブロック - 各起動時 AM ドライバーは、最後のブート ドライバーが初期化された後、午前ドライバーが読み込まれたなることを示しますが、同期コールバックを受け取ります。 AM ドライバーは、「クリーンアップ」を行いランタイム AM ドライバーで使用できる任意の状態情報を保存する必要があることを示していますとしてこれを使用できます。 ただし、起動時 AM、ドライバーがロードするドライバーをブートを続行するコールバックを返す必要があります。
-   署名データ テスト - 各起動時 AM ドライバーは、よく知られている単一の場所としないその他のマルウェアの署名データを取得する必要があります。 これにより、測定し、Windows によってそのデータを保護できます。 このテストによりこと各 AM ドライバーのみその構成からデータを読み取るレジストリ ハイブが作成されるをドライバーのようになります。
-   バックアップのドライバーのテスト - 早期起動 AM ドライバーのインストール時は、バックアップのドライバー ストアにドライバーのバックアップ コピーをインストールする必要がありますもします。 この要件は、プライマリのドライバーが壊れた場合に、修復方法に関するヘルプです。 このテストにより、インストールされているコンピューターの起動時の AM のドライバーがありますが、対応するドライバー、バックアップ ストアに。