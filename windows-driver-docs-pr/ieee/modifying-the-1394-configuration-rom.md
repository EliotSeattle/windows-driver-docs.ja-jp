---
title: 1394 構成 ROM の修正
description: 1394 構成 ROM の修正
ms.assetid: 3dc4fe53-a26b-44c7-96ef-e7bb6181c958
keywords:
- IEEE 1394 WDK バス、Rom の構成を変更します。
- 1394 WDK バス、Rom の構成を変更します。
- Rom WDK の IEEE 1394 バスの構成
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f59e2be9a3316b94461e3ef0a3291824da14d8f5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385755"
---
# <a name="modifying-the-1394-configuration-rom"></a>1394 構成 ROM の修正





1394 バスに接続されている Microsoft Windows システムでは、ノードでサポートされている機能のユニットを説明する構成 ROM を公開します。 1394 構成 Rom の詳細については、IEEE 1394 1995 と IEEE-1212 2000 仕様を参照してください。 Windows XP およびそれ以降のオペレーティング システムでは、2 つの方法で構成 ROM の内容が動的に定義することができます。

1.  ドライバーでは、1394 バス上の非 1394 バス用に設計されたハードウェアを公開する構成 ROM を動的に変更できます。

    たとえば、汎用システム、システムの IDE バスに接続されている内部の DVD ドライブを検討してください。 DVD ドライブで使用されるプロトコルに 1394 要求をマップするドライバーは、1394 の他のノードに 1394 バス上の DVD ドライブにさらされる可能性が。 これを行うことには、システムの 1394 構成 ROM に単位の新しいディレクトリを追加する必要があります。 1394 バスに接続されているその他のシステムは、1394 DVD デバイスの場合と同様に、汎用システムを列挙することになります。

2.  ドライバーは、仮想の物理デバイス オブジェクト (Pdo) を使用して、デバイス ドライバーのテストを容易にするための方法でハードウェアをエミュレートします。

    デバイスのエミュレーションでは、まだ受信がいないデバイスのドライバーをテストできます。 ハードウェア エミュレーション ドライバーは、1394 バス上の仮想 1394 デバイスに公開できます。 開発者は、別のシステムで新しいハードウェアのドライバーをデバッグできます。 詳細については、デバイスのエミュレーションは、次を参照してください。[ハードウェア エミュレーション ドライバーの IEEE 1394](https://docs.microsoft.com/windows-hardware/drivers/ieee/ieee-1394-hardware-emulation-drivers)します。

## <a name="related-topics"></a>関連トピック
[IEEE 1394 ノードの構成 ROM の内容を取得します。](https://docs.microsoft.com/windows-hardware/drivers/ieee/retrieving-the-contents-of-a-ieee-1394-node-s-configuration-rom)  



