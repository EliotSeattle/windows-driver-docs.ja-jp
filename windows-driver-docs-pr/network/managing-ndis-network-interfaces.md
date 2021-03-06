---
title: NDIS ネットワーク インターフェイスの管理
description: NDIS ネットワーク インターフェイスの管理
ms.assetid: b4c61b8a-a3ef-449d-9bce-853d91911dc4
keywords:
- NDIS ネットワーク インターフェイス、WDK を管理します。
- ネットワーク インターフェイス、WDK を管理します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 410a7003ce97ffb2f9f8cf15ff61c51f8d8d80ab
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67356150"
---
# <a name="managing-ndis-network-interfaces"></a>NDIS ネットワーク インターフェイスの管理





NDIS ネットワーク インターフェイスのプロバイダーは、NDIS をネットワーク インターフェイスを登録します。 インターフェイスを登録する前に、インターフェイス プロバイダーを取得、 [ **NET\_LUID** ](https://docs.microsoft.com/windows/desktop/api/ifdef/ns-ifdef-net_luid_lh)値インターフェイスに対応します。 NDIS インターフェイス インデックスを割り当てます ( *IfIndex*で RFC 2863) が登録されている場合にインターフェイスにします。

NDIS は、ドライバーは、インターフェイスの履歴テーブル内のエントリの管理に使用できるサービスも用意されています。 (*ifStackTable*で RFC 2863)。

このセクションの内容:

[NET\_LUID 値](net-luid-value.md)

[NET を使用して\_LUID インデックス](using-a-net-luid-index.md)

[ネットワーク インターフェイスを登録します。](registering-a-network-interface.md)

[ネットワーク インターフェイスを登録解除](deregistering-a-network-interface.md)

[マッピング、NET\_インターフェイス インデックスに LUID 値](mapping-a-net-luid-value-to-an-interface-index.md)

[NET\_ミニポート アダプターとフィルター モジュールの LUID 値](net-luid-values-for-miniport-adapters-and-filter-modules.md)

[ネットワーク インターフェイスのスタックを維持](maintaining-a-network-interface-stack.md)

 

 





