---
title: WMI と電源管理タブ
description: WMI と電源管理タブ
ms.assetid: ff270fc0-806b-4014-ba9c-9c321a10c893
keywords:
- WMI の WDK カーネルでは、プロパティ シート
- プロパティ シートの WDK WMI
- デバイスのプロパティ シートの WDK WMI
- WDK の WMI の電源管理
- プロパティ ページの WDK WMI
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: e12509b6ddec12d9524c2f1801810e5511a281ca
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386867"
---
# <a name="wmi-and-the-power-management-tab"></a>WMI と電源管理タブ





電源管理をサポートするドライバーが自動的に有効にできる、**電源管理**デバイス マネージャー内デバイスのプロパティ シートのタブ。 ドライバーが、GUID を処理する場合\_POWER\_デバイス\_有効化または GUID\_POWER\_デバイス\_WAKE\_を有効にする WMI クラスの Guid、デバイス マネージャーが表示されます、 **電源管理**デバイスのプロパティ シートのタブ。 どの WMI クラスの Guid、ドライバーのサポートによっては、プロパティ ページで、特定のコントロールが有効になります。

GUID\_POWER\_デバイス\_*XXX*クラスの Guid が次のようにプロパティ ページのコントロールを有効にします。

-   GUID\_POWER\_デバイス\_を有効にします。

    デバイスの電源管理のアクティブ化またはチェック ボックスを有効にします。 WMI クラスのデータ ブロックは、電源管理が有効になっているかどうかを示す単一のブール値で構成されます。 値の意味では、デバイスによって異なります。

-   GUID\_POWER\_デバイス\_WAKE\_を有効にします。

    送信待機/ウェイク Irp をアクティブ化またはチェック ボックスを有効にします。 選択した場合、ドライバーを送信する必要があります、 [ **IRP\_MN\_待機\_WAKE** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-wait-wake)物理デバイス、そのオブジェクトを要求します。 これにより、外部のイベントに応答システムをスリープ解除するデバイスです。 たとえば、キーボード クラス ドライバーを有効にすると、キーボード デバイスがシステムをスリープ解除キーが押されたときにします。 チェック ボックスを選択していない場合、ドライバーを取り消すか、 **IRP\_MN\_待機\_WAKE**要求。 WMI クラスのデータ ブロックは、チェック ボックスの現在の状態を示す単一のブール値で構成されます。

WMI クエリの要求が送信され、GUID\_POWER\_デバイス\_*XXX* WMI クラスの Guid、ドライバーのプロパティ シートがデバイス マネージャーを開くたびにします。 WMI の変更要求のたびに、チェック ボックスのいずれかの値が送信される、**電源管理** タブの変更。 ユーザーがそれらのドライバーが、レジストリのいずれかのプロパティの現在の値を格納する必要がありますので、ドライバーの読み込みとアンロードされるの間で維持する設定の値を期待します。

マウスやキーボード クラス サンプル ドライバー両方処理 GUID\_POWER\_デバイス\_WAKE\_を有効にする WMI クラスの GUID。 参照してください\\src\\入力\\kbdclass と\\src\\入力\\mouclass Windows Driver Kit (WDK) にします。

 

 




