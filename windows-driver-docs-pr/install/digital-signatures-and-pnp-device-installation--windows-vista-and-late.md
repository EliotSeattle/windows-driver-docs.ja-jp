---
title: デジタル署名と PnP デバイスのインストール (Vista 以降)
description: デジタル署名と PnP デバイスのインストール (Windows Vista 以降)
ms.assetid: 38d3e8c9-0be1-4fea-9128-15834c0c4e2e
keywords:
- ドライバーの署名の WDK、PnP デバイスのインストール
- ドライバー WDK、PnP デバイスのインストールへの署名
- デジタル署名 WDK、PnP デバイスのインストール
- 署名 WDK、PnP デバイスのインストール
- PnP WDK ドライバーの署名
- プラグ アンド プレイ WDK ドライバーの署名
- ドライバー パッケージのデジタル署名 WDK
- パッケージのデジタル署名 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9ec2391559d7849351f58c43b594208956c0b18f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571509"
---
# <a name="digital-signatures-and-pnp-device-installation-windows-vista-and-later"></a>デジタル署名と PnP デバイスのインストール (Windows Vista 以降)


プラグ アンド プレイ (PnP) デバイスのインストールを使用して Windows Vista と Windows の以降のバージョンで、[デジタル署名](digital-signatures.md)の[ドライバー パッケージの](driver-packages.md) [カタログ ファイル](catalog-files.md)を行うには次の。

-   ドライバー パッケージの発行元の id を確認します。 Windows では、ドライバーの発行元を信頼するかどうかを選択できるようにする、id が使用されます。

-   パブリッシュ後にドライバー パッケージが変更されたかどうかを決定します。

Windows Vista 以降のバージョンの Windows での PnP デバイスのインストールをサポートして、次の種類のデジタル署名の[ドライバー パッケージ](driver-packages.md):

-   一般公開リリースされているドライバーを使用できる署名の種類:
    -   署名機関 Windows によって生成された署名:
        1.  インボックス ドライバー
        2.  ドライバーの認定および Windows Hardware Quality Labs (WHQL) からの署名
        3.  Windows 継続的なエンジニア リング (SE) の更新プログラム。
    -   署名機関を Windows では生成されませんが、次に準拠している署名:

        1.  [カーネル モード コードの署名ポリシー](kernel-mode-code-signing-policy--windows-vista-and-later-.md)の 64 ビット バージョンの Windows Vista および以降のバージョンの Windows。
        2.  [PnP デバイスのインストール要件を署名](pnp-device-installation-signing-requirements--windows-vista-and-later-.md)の 32 ビットおよび 64 ビット バージョンの Windows Vista と Windows の以降のバージョン。

        この種類の署名の生成を使用して、[ソフトウェア発行元証明書 (SPC)](software-publisher-certificate.md)マイクロソフトがこのような証明書を発行する権限を持つサード パーティ証明機関 (CA) から取得しました。

    -   署名の署名機関の Windows では生成されませんし、準拠していない、[カーネル モード コードの署名ポリシー](kernel-mode-code-signing-policy--windows-vista-and-later-.md)に準拠しているが、 [PnP デバイスのインストール要件を署名](pnp-device-installation-signing-requirements--windows-vista-and-later-.md)します。 この種類の署名は、Windows Vista の 32 ビット バージョン、以降のバージョンの Windows カーネル モード ドライバーの署名に使用できます。 この種類の署名の生成を使用して、[コマーシャル リリースの証明書](commercial-release-certificate.md)Microsoft ルート証明書プログラムのメンバーである CA から取得しました。

-   企業のネットワーク環境が作成され、エンタープライズ CA によって管理されるデジタル証明書が作成するだけでドライバーを展開するための署名。 エンタープライズ CA を構成する方法の詳細については、このドキュメントの範囲外です。

    エンタープライズ CA を作成する方法についてで「コード署名のベスト プラクティス」のホワイト ペーパーを参照してください。、[署名要件の Windows ドライバー](https://go.microsoft.com/fwlink/p/?linkid=14507) web サイト。

-   社内で開発およびドライバーのテスト中に使用できる署名の種類:
    -   によって生成された署名、 [WHQL テスト署名プログラム](whql-test-signature-program.md)
    -   によって生成された署名を[MakeCert テスト証明書](makecert-test-certificate.md)
    -   署名によって作成された、[市販のテスト証明書](commercial-test-certificate.md)Microsoft ルート証明書プログラムのメンバーである CA から取得しました。
    -   によって生成された署名を[テスト証明書をエンタープライズ CA](enterprise-ca-test-certificate.md)

Windows Vista と以降のバージョンの Windows は、サード パーティによって生成された署名のサポートを提供する次の機能を示します。

-   ドライバーをパブリッシャーには、信頼された管理者が制御できます。 Windows Vista および Windows の以降のバージョンは、メッセージを表示せず信頼された発行元からドライバーをインストールします。 決してを信頼しないように、管理者が選択した発行元からドライバーをインストールします。

-   ドライバーの署名ポリシーは、常に設定*警告*します。 これにより、*無視*と*ブロック*が Windows Server 2003、Windows XP、および Windows 2000 で使用可能なオプションです。 管理者は、未署名のドライバーや、まだ信頼されない発行元からドライバーのインストールを常に承認する必要があります。

-   すべて[デバイス セットアップ クラス](device-setup-classes.md)は均等に扱われます。 Windows Server 2003、Windows XP、および Windows 2000、WHQL によって署名されたドライバー パッケージが必要、INF ファイルで定義されているデバイス セットアップ クラスを指定する *%SystemRoot%/inf/Certclas.inf*します。 それ以外の場合、Windows は未署名としてドライバー パッケージを扱います。

-   以降、Windows Vista ではいくつかの互換性のあるドライバーから選択するときに、ランク付け、オペレーティング システムを使用して最適なドライバーを選択するには、サード パーティの署名を持つドライバーが含まれています。

    このアルゴリズムでは、次のようにドライバーを順位付けされます。

    -   場合、 [AllSignersEqual グループ ポリシー](allsignersequal-group-policy--windows-vista-and-later-.md)はランク付けサード パーティの署名で署名されているドライバーよりも高いマイクロソフトの署名で署名されたドライバーをオペレーティング システムを無効にします。 この順位付けは、サード パーティの署名で署名されたドライバーは、他のすべての方法でデバイスに適している場合でも発生します。
    -   場合、 [AllSignersEqual グループ ポリシー](allsignersequal-group-policy--windows-vista-and-later-.md)が有効になっている、オペレーティング システムをランク付けデジタル署名されたドライバーをすべて均等にします。

    **注**  以降、Windows 7 で、 [AllSignersEqual グループ ポリシー](allsignersequal-group-policy--windows-vista-and-later-.md)既定で有効です。 Windows Vista および Windows Server 2008、 **AllSignersEqual**グループ ポリシーが既定で無効になっています。 IT 部門は、既定の動作を有効または無効に順位付けをオーバーライドできます、 **AllSignersEqual**グループ ポリシー。

     

Windows を分析し、ドライバーをインストールする前に、[ドライバー パッケージの](driver-packages.md)デジタル署名します。 署名が存在する場合は、Windows で、署名を使用して、ドライバー パッケージ内のファイルを検証します。 この分析の結果に基づいて、Windows を分類してデジタル署名には、次のように。

-   **署名機関に Windows によって署名されます。** これらのドライバーが Windows の既定のインストールに含まれるか (*インボックス ドライバー*) によって、WHQL リリース署名、または、Windows SE によって署名されます。

-   **信頼された発行元によって署名されます。** これらのドライバーは、サード パーティによって署名されているし、ユーザーがこのパブリッシャーからの署名されたドライバーを常に信頼を明示的に選択しました。

-   **信頼されていない、発行元によって署名されます。** サード パーティによってこれらのドライバーが署名されているし、決してこのパブリッシャーからドライバーを信頼するユーザーが明示的に選択します。

-   **不明な信頼の発行元によって署名されます。** サード パーティによってこれらのドライバーが署名されているし、ユーザーがこの発行元を信頼するかどうかを指定できません。

-   **変更されます。** これらのドライバー署名されますが、Windows がでその少なくとも 1 つのファイルを検出、[ドライバー パッケージ](driver-packages.md)が、パッケージが署名された後に変更されました。

-   **符号なし整数。** これらのドライバーは署名されていないまたは署名が無効です。 有効な署名は、信頼された CA によって発行された証明書を使用して作成する必要があります。

以降、Windows Vista では、オペレーティング システムをコンピューターに最初にドライバーをインストールするときに、プレインストール、またはステージで、ドライバー、[ドライバー ストア](driver-store.md)します。 ドライバーをプレインストールするには、は、Windows は、ドライバー ストアにドライバー パッケージをコピーし、システム INF ディレクトリで、ドライバー パッケージの INF ファイルのコピーを保存します。 Windows、その後はサイレント モードでインストールの一致するデバイス ドライバーをドライバー ストアにドライバー パッケージのコピーを使用しています。 Windows デバイス用のプレインストールされているドライバーのインストール時に、ユーザーの介入は必要ありません。

Windows のプレインストールかどうかを[ドライバー パッケージ](driver-packages.md)次のように、署名のカテゴリ、ユーザーの資格情報と、ユーザーの操作に依存します。

-   **署名機関または信頼された発行元の Windows によって署名されます。** Windows は、システム管理者と標準ユーザー (管理者の資格情報のないユーザー) のドライバー パッケージをサイレント モードでプレインストールします。 Windows では、任意のユーザー ダイアログ ボックスは表示されません。

-   **信頼されていない、発行元によって署名されます。** Windows は、ドライバー パッケージをプレインストールしていません。

-   **不明な信頼の発行元によって署名されます。** Windows では、ダイアログ ボックスを表示するドライバー パッケージの発行元がまだ信頼されていない管理者に通知するシステム管理者にします。 ドライバー パッケージをインストールするオプションと、常に、発行元を信頼するオプション、ダイアログ ボックスは、管理者を提供します。 Windows では、標準ユーザーにダイアログ ボックスを表示しないと、標準ユーザー用のドライバー パッケージをプレインストールすることはできません。

-   **変更または符号なし。** Windows では、署名が検証されないことには、システム管理者を適切に警告するダイアログ ボックスが表示されます。 ダイアログ ボックスは、管理者は、インストールしたり、ドライバー パッケージをインストールしないようにオプションを提供します。 Windows では、標準ユーザーにダイアログ ボックスを表示しないと、標準ユーザー用のドライバー パッケージをプレインストールすることはできません。

ドライバーの署名とインストールの詳細については、[署名カテゴリとドライバーのインストール](signature-categories-and-driver-installation.md)を参照してください。

 

 




