---
title: 受信トレイのドライバーのプライベート ビルドを作成します。
description: 受信トレイのドライバーのプライベート ビルドを作成します。
ms.assetid: aed3c175-3e95-4bfb-a514-a663dd9e3f57
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 953d8cdb3de7f61ad2ee3dab648ccc0c0258a1bc
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67356316"
---
# <a name="creating-a-private-build-of-an-inbox-driver"></a>受信トレイのドライバーのプライベート ビルドを作成します。


受信トレイのドライバーのプライベート バージョンをビルドするときに、 [Windows がランクのドライバーの署名に同じように構成されている](configuring-windows-to-rank-driver-signatures-equally.md)、プライベート ビルド outranks Microsoft によって署名されたバージョンであることを確認する必要があります。 これを実現する最も簡単な方法がの値を更新するには、 [ **INF DriverVer ディレクティブ**](inf-driverver-directive.md)で、[ドライバー パッケージの](driver-packages.md)INF ファイル。 日時の値よりも新しいバージョンの新しい値を指定する必要があります、 **DriverVer**ターゲット システムにインストールされているパッケージの INF ファイルでディレクティブ。

次の手順に従って、Microsoft によって署名されたバージョンを outranks するインボックス ドライバーのプライベート バージョンを構築するプロセスを自動化できます。

1. 新しい INF ファイルを生成するメイクファイルの変更、[ドライバー パッケージ](driver-packages.md)します。 たとえば、次の行を追加、*メイクファイル*:

   ```cpp
   $(O)\sample.inf
   ```

2. ディレクティブを追加、*メイクファイル*新しい INF ファイルを生成し、実行するが、 [Stampinf](https://docs.microsoft.com/windows-hardware/drivers/devtest/stampinf) INF ファイルのタイムスタンプをツールします。 次のコード例が方法を作成し、タイムスタンプという INF ファイルを表示するなど、 *Sample.inf*:

   ```cpp
   $(O)\ sample.inf: $(_INX)\ sample.inx $(_LNG)\ sample.txt
       $(C_PREPROCESSOR_NAME) $(PREFLAGS) $(_LNG)\$(@B).txt > $(O)\$(@B).txt1
       copy /b $(_INX)\$(@B).inx+$(O)\$(@B).txt1 $@
       @del $(O)\$(@B).txt1
       stampinf -f sample.inf -d * -v * -c MyCatalogFile.cat
       $(TSBINPLACE_CMD)
   ```

   次[Stampinf](https://docs.microsoft.com/windows-hardware/drivers/devtest/stampinf)コマンド ライン パラメーターは、この例で使用されます。

   - -D\*パラメーターは、INF ファイルで、DriverVer ディレクティブの一部として、現在の日付を使用します。
   - **-V \\** * パラメーターは、バージョン番号の現在の時刻を使用します。 STAMPINF_VERSION 環境変数が設定されていると、Stampinf はこの環境変数で指定されているバージョン番号値を使います。
   - -**C**パラメーターの名前を指定する、[カタログ ファイル](catalog-files.md)の[ドライバー パッケージ](driver-packages.md)します。 この値が書き込まれる、 **CatalogFile**のディレクティブ、 [ **INF バージョン セクション**](inf-version-section.md)生成される場合はファイル。

   **注**Stampinf が現在の日付とバージョンを使用して、INF の PRIVATE_DRIVER_PACKAGE 環境変数を設定した場合**DriverVer**ディレクティブ。 この環境変数を設定では使用する必要はありません、 **-d**または **-v**内のパラメーター、*メイクファイル*します。

     

サインインする必要があります、ドライバーがビルドされたら、[ドライバー パッケージ](driver-packages.md)は同じと[カタログ ファイル](catalog-files.md)に指定されている、 **-c**のパラメーター [Stampinf](https://docs.microsoft.com/windows-hardware/drivers/devtest/stampinf)内、*メイクファイル*します。 ドライバー パッケージに署名するに記載されている手順に従います[開発中にドライバーの署名、およびテスト](signing-drivers-during-development-and-test.md)します。

 

 





