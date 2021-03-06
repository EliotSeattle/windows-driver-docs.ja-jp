---
title: WDM ドライバー レイヤーの例
description: WDM ドライバー レイヤーの例
ms.assetid: 64eaa850-6394-4832-b11f-ce4db7f7c37d
keywords:
- WDM ドライバー WDK カーネル、複数層のドライバー
- 階層型ドライバー WDK カーネル
- ドライバーは、WDK WDM をレイヤーします。
- ジョイスティック WDK WDM
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: b96e7151fda11e11b001f074eb3792b9b2f4639d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537459"
---
# <a name="wdm-driver-layers-an-example"></a>WDM ドライバー レイヤー:例





このセクションでは、WDM ドライバーのレイヤーを説明するために USB ハードウェア WDM ドライバーの可能なセットについて説明します。

次の図は、USB ジョイスティックのプラグ アンド プレイ ハードウェア構成の例を示します。

![usb ジョイスティックのサンプル プラグ アンド プレイ ハードウェアを示す図します。](images/usbjoyhw.png)

この図では、USB ジョイスティックは、USB ハブ上のポートに接続されます。 この例では、USB ハブは、USB ホスト コント ローラー ボード上に存在し、USB ホスト コント ローラー ボード上の単一のポートに接続します。 USB ホスト コント ローラーは、PCI バスに接続されます。 PnP パースペクティブ、USB ハブ、USB ホスト コント ローラー、および PCI バスからポートをそれぞれ提供するためは、すべてのバス デバイス。 ジョイスティックはバスのデバイスではありません。

次の図は、前の図の USB ジョイスティック ハードウェア用に読み込まれることがドライバーのサンプル セットを示します。

![usb ジョイスティックの「プラグ アンド プレイ ドライバー レイヤーを示す図](images/usbjoydr.png)

前の図の下部にある以降は、サンプル履歴内のドライバーが含まれます。

-   PCI バスを駆動する PCI ドライバ。 これは、PnP バス ドライバーです。 PCI バス ドライバーは、Microsoft によって、システムで提供されます。

-   USB ホスト コント ローラーのバス ドライバーは、クラス/miniclass ドライバーのペアとして実装されます。 USB ホスト コント ローラー クラスと miniclass ドライバーは、Microsoft によって、システムで提供されます。

-   ドライブを USB ハブを USB ハブ バス ドライバー。 USB ハブのドライバーは、Microsoft によって、システムで提供されます。

-   ジョイスティック; 用の 3 つのドライバーうち 1 つは、クラス/miniclass ペアです。

    関数のドライバー、ジョイスティック、デバイスのメイン ドライバーは、HID クラス ドライバー/HID USB miniclass ドライバーのペアです。 (HID は「ヒューマン インターフェイス デバイス」を表します)。HID USB miniclass ドライバーでは、一般的なの HID サポート用 HID クラス ドライバー DLL に依存、HID デバイスの USB 固有のセマンティクスをサポートします。

    関数のドライバーは、特定のデバイスに固有または、HID のように、関数のドライバーがデバイスのグループをサービスできます。 この例では、HID クラス ドライバー/HID USB miniclass ドライバーのペアは、HID 準拠の任意のデバイスを USB バス上のシステム サービスします。 HID クラス ドライバー/HID 1394 miniclass ドライバー ペアは、1394 バス上の任意の HID 準拠デバイスをサービスが。

    デバイスの製造元、または Microsoft によって、関数のドライバーを記述できます。 この例では、関数のドライバーでは (、HID クラス/HID USB miniclass ドライバーのペア) は、Microsoft によって書き込まれます。

    この例ではジョイスティック デバイスのドライバーを 2 つのフィルター処理がある: マクロ ボタンの機能と低レベル デバイス フィルターを追加する上位レベルのクラス フィルターにより、ジョイスティック、マウス デバイスをエミュレートします。

    上位レベルのフィルターがフィルター ジョイスティック I/O に必要のある人物によって書き込まれ、下位レベルのフィルター ドライバーは、ジョイスティック仕入先によって書き込まれます。

-   カーネル モードとユーザー モードの HID クライアントとアプリケーションは、ドライバーではありませんが、完全を期すのために表示されます。

 

 




