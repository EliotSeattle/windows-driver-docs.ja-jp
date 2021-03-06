---
title: コンポーネントのインストール、アップグレード、および削除
description: コンポーネントのインストール、アップグレード、および削除
ms.assetid: 7069e7a0-0c7e-4f7c-a764-a83e758df1bf
keywords:
- オブジェクトの WDK ネットワーク、ネットワーク コンポーネントの削除の通知します。
- ネットワーク通知オブジェクト WDK、ネットワーク コンポーネントを削除します。
- オブジェクトの WDK ネットワーク、ネットワーク コンポーネントのアップグレードの通知します。
- ネットワークがネットワーク コンポーネントのアップグレード、WDK をオブジェクトに通知します。
- オブジェクトの WDK ネットワーク、ネットワーク コンポーネントのインストールを通知します。
- ネットワークがネットワーク コンポーネントのインストール、WDK をオブジェクトに通知します。
- ネットワーク コンポーネントを削除します。
- WDK のネットワーク コンポーネントをアップグレードするには、オブジェクトに通知します。
- WDK のネットワーク コンポーネントをインストールするには、オブジェクトに通知します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9445db497145a433edece7795ab5cbc22d2383f7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381218"
---
# <a name="installing-upgrading-and-removing-the-component"></a>コンポーネントのインストール、アップグレード、および削除





ネットワーク構成のサブシステムをインストールするときは、アップグレード、またはもコンポーネントのインストール、アップグレードを完了して削除の通知呼び出しのネットワーク コンポーネント、サブシステムを削除します。 コンポーネントのでは、コンポーネントを必要とする操作を実行するオブジェクトを実装することを通知します。 次に、例を示します。

-   通知オブジェクトが、マルチプレクサーのプロトコルがバインドされる仮想アダプターをインストール、サブシステムをインストール、マルチプレクサーようには、仮想 LAN のマルチプレクサーの通知オブジェクトを実装することができます。

    仮想アダプターをインストールする通知オブジェクトがネットワークの構成を呼び出す[ **INetCfgClassSetup::Install** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff547711(v=vs.85))メソッド。 この呼び出しでは、通知オブジェクトは、インストールする仮想アダプターの識別子を渡します。 通知オブジェクトが呼び出すことができます**INetCfgClassSetup::Install**、たとえばからその[ **INetCfgComponentNotifyBinding::NotifyBindingPath** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff547731(v=vs.85))または[**INetCfgComponentPropertyUi::ApplyProperties** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff547741(v=vs.85))メソッド。

    仮想アダプターのインストールを完了するには、オペレーティング システム、仮想アダプターの INF ファイルする必要があります。 この INF ファイルを配置できることを確認するにする必要がありますにコピー、オペレーティング システム、multipexer がインストールされている場合。 詳細については、次を参照してください。[コピー Inf](https://docs.microsoft.com/windows-hardware/drivers/install/copying-inf-files)します。 このトピックでは、ことを示します、 **CopyINF**ディレクティブまたはへの呼び出し、 **SetupCopyOEMInf** INF ファイルをターゲット システムの INF ディレクトリにコピーする、共同インストーラーまたはセットアップ アプリケーションによって関数を使用できます。 ただし場合は、INF ファイルをマルチプレクサー (元の INF) は、コピーを使用して**SetupCopyOEMInf**、しを使用して仮想アダプターの INF ファイルをコピーする必要がありますも**SetupCopyOEMInf**のため、オペレーティング システムシステムのみを処理する**CopyINF**ディレクティブ元 INF がまだ INF ディレクトリ内でない場合。

-   通知オブジェクトがすべての仮想アダプターを削除、サブシステム、マルチプレクサーを削除するときにできるように、マルチプレクサーの通知オブジェクトを実装できます。 仮想アダプターを削除するには、通知オブジェクトはネットワークの構成を呼び出します。 [ **INetCfgClassSetup::DeInstall** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff547710(v=vs.85))メソッド。 この呼び出しでは、通知オブジェクトはへのポインターを渡します。、 **INetCfgComponent**仮想アダプターのインターフェイス。 通知オブジェクトが呼び出すことができます**INetCfgClassSetup::DeInstall**、たとえばからその**INetCfgComponentNotifyBinding::NotifyBindingPath**または**INetCfgComponentPropertyUi:。ApplyProperties**メソッド。

-   通知オブジェクトが、コンポーネントのバインド パスの順序を変更するコンポーネントをアップグレードすると、サブシステムようには、コンポーネントの通知オブジェクトを実装することができます。 順序を変更するこの通知オブジェクトの[ **INetCfgComponentSetup::Upgrade** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff547783(v=vs.85))メソッドを呼び出すか、 [ **INetCfgComponentBindings::MoveBefore**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff547722(v=vs.85))または[ **INetCfgComponentBindings::MoveAfter** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff547721(v=vs.85))メソッド。

 

 





