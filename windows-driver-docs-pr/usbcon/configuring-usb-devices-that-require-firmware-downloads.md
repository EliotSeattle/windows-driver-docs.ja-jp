---
Description: Firmware is internal to a device, and is independent of the operating system. However, firmware downloads can cause operating system errors.
title: ファームウェアの更新の USB デバイスを構成します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d4c1d98ac24d0381046fbed203ab3550707ea4ff
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575123"
---
# <a name="configuring-a-usb-device-for-firmware-update"></a>ファームウェアの更新の USB デバイスを構成します。


ファームウェアでは、デバイスの内部し、は、オペレーティング システムに依存しません。 ただし、ファームウェアのダウンロードには、オペレーティング システムのエラーを生じることができます。

-   Windows xp の場合、デバイスをシステムに接続する可能性があります複数プラグが発生する切り、サウンド、エンド ユーザー エクスペリエンスの低下につながります。

-   ファームウェアがデバイスを起動するたびにダウンロードされるため、これが機能しない直後に、取り込まれています後、またはオペレーティング システムは、S3 または S4 の電力状態から再開した後に。

-   S3 または S4 からの復帰には、S4 モードで自己供給型のデバイスに、ほとんどのコンピューターが電源オフ切り取りため、ポップアップの突然の削除 ダイアログ ボックスが、デバイスにあります。

システム エラーを回避するには。

-   デバイスが製造元とデバイスの Id の 2 つのセットであることを確認します。

    ファームウェアの更新プログラムの対応するデバイスは、2 回、システムによって列挙されます。 システムによって、デバイスが検出されると、ベンダーとデバイスの ID を使用して予備のドライバーを読み込む このドライバーには、ファームウェアのダウンロードが容易になります。

    ファームウェアが読み込まれた後、予備のドライバーが原因でもう一度デバイスを列挙するシステム バスをリセットします。 新しいファームウェアは、さまざまなベンダーとデバイス id。 2 つ目の列挙中にシステムは新しい一連の Id を使用して、メインのデバイス ドライバーを読み込みます。

-   ベンダーとデバイスの Id は、製品に固有のことを確認します。

    デバイスには、サード パーティによってプログラミング可能な USB チップが含まれている場合、チップが自身を識別 Id の標準セットを使用しています。 同じシステム上の別のデバイスと同じチップを使用する場合、2 つのデバイス Id、オペレーティング システムが正しく機能しない原因の同じセットの間の競合である可能性があります。

## <a name="related-topics"></a>関連トピック
[Windows 用の USB デバイスの構築](building-usb-devices-for-windows.md)  