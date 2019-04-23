---
title: SetupAPI を使用したデバイスとドライバー パッケージのアンインストール
description: SetupAPI を使用したデバイスとドライバー パッケージのアンインストール
ms.assetid: e170961b-5d12-43d5-b502-3b37e6421f6e
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3f460b6b4ff6229bfc8a55e127388669f6a84f16
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580065"
---
# <a name="using-setupapi-to-uninstall-devices-and-driver-packages"></a>SetupAPI を使用したデバイスとドライバー パッケージのアンインストール


[SetupAPI](setupapi.md)は関数の 2 つのセットを提供するシステム コンポーネントです。

-   [一般的なセットアップ関数](https://msdn.microsoft.com/library/windows/hardware/ff544985)

-   [デバイス インストールの機能](https://msdn.microsoft.com/library/windows/hardware/ff541299)

*デバイスのインストール アプリケーション*、*共同インストーラー*、および*クラス インストーラー*これらの関数を使用してデバイスのインストールのカスタム操作を実行することができます。 SetupAPI も、デバイスのアンインストールをサポートし、[ドライバー パッケージ](driver-packages.md)にインストールします。

このトピックでは、SetupAPI 関数を使用してデバイスとドライバー パッケージをアンインストールする手順について説明します。

ドライバーとドライバー パッケージのアンインストールの詳細については、[と、どのデバイスとドライバー パッケージがアンインストール](how-devices-and-driver-packages-are-uninstalled.md)を参照してください。

### <a href="" id="uninstalling-the-device"></a> デバイスのアンインストール

SetupAPI)、次のメソッドを使用して、システムから。

-   デバイスのインストール アプリケーションが呼び出すことによって、デバイスをアンインストールすることを要求することができます、 [ **SetupDiCallClassInstaller** ](https://msdn.microsoft.com/library/windows/hardware/ff550922)関数。 アプリケーションがデバイスをアンインストールするには、この関数を呼び出すときに設定する必要があります、 *InstallFunction*パラメーターを[ **DIF_REMOVE** ](https://msdn.microsoft.com/library/windows/hardware/ff543717)コード。  差分のすべてのコードの一覧は、[デバイスのインストール機能](https://msdn.microsoft.com/library/windows/hardware/ff541307)を参照してください。

    場合[ **SetupDiRemoveDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff552097)呼びます DIF_REMOVE 要求の処理中に、関数は、システムから、デバイスの devnode を削除します。 また、デバイスのハードウェアとソフトウェアのレジストリ キー、すべてのハードウェア プロファイル固有のレジストリ キー (構成固有のレジストリ キー) とも削除されます。

    **注**  **SetupDiRemoveDevice**クラスのインストーラーとデバイスのインストール アプリケーションではなくにのみ呼び出す必要があります。

    差分のコードの詳細については、[DIF コードの処理](handling-dif-codes.md)を参照してください。

-   Windows 7 以降のデバイスのインストール アプリケーション デバイスをアンインストールできますを呼び出して、 [ **DiUninstallDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff544754)関数。 この関数は呼び出しと同様、 [ **SetupDiCallClassInstaller** ](https://msdn.microsoft.com/library/windows/hardware/ff550922)で、 *InstallFunction*パラメーターに設定[ **DIF_REMOVE**](https://msdn.microsoft.com/library/windows/hardware/ff543717). ただし、だけでなく、指定されたデバイスの devnode を削除するには、この関数と呼び出し時に、システムに存在するデバイスのすべての子 devnode を削除します。

### <a href="" id="deleting-a-driver-package-from-the-driver-store"></a> ドライバー ストアからドライバー パッケージを削除します。

Windows XP 以降では、デバイスのインストール アプリケーションが呼び出すことができます、 [SetupUninstallOEMInf](https://go.microsoft.com/fwlink/p/?linkid=169503)関数を指定された削除する[INF ファイル](inf-files.md)システム INF ファイルのディレクトリから。

Windows Vista 以降、この関数はそのも削除、[ドライバー パッケージ](driver-packages.md)から、指定した INF ファイルを含む、[ドライバー ストア](driver-store.md)します。

### <a href="" id="deleting-the-binary-files-of-the-installed-driver"></a> インストールされているドライバーのバイナリ ファイルを削除します。

この操作を実行する SetupAPI を使用できません。

 

 




