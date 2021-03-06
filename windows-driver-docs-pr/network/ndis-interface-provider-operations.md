---
title: NDIS インターフェイス プロバイダー操作
description: NDIS インターフェイス プロバイダー操作
ms.assetid: cd5c76b0-6b38-44ea-ac1b-02be5d073203
keywords:
- NDIS ネットワーク インターフェイス、WDK インターフェイス プロバイダー
- ネットワーク インターフェイス、WDK インターフェイス プロバイダー
- インターフェイス プロバイダー WDk のネットワーク インターフェイス
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0b00e6d204951aebb8471c11e49b396ac5e7cf5d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385512"
---
# <a name="ndis-interface-provider-operations"></a>NDIS インターフェイス プロバイダー操作





すべての NDIS ドライバーは、インターフェイスのプロバイダーとして登録できます。 ドライバー (または、NDIS プロキシ インターフェイス プロバイダー) がコンピューターに導入される新しいインターフェイスを検出すると、それを割り当てます、 [ **NET\_LUID** ](https://docs.microsoft.com/windows/desktop/api/ifdef/ns-ifdef-net_luid_lh)インデックス、インターフェイスを登録し、関連付けられている NET を保持\_(レジストリ) などの永続的ストレージ LUID 値。 次の一覧には、コンピューターに新しいインターフェイスを導入する方法の例をいくつかについて説明します。

-   中間のドライバー用の仮想アダプターまたは物理アダプターか、ネットワーク アダプターをインストールします。 この場合は、NDIS プロキシ インターフェイス プロバイダーは、インターフェイスを管理します。

-   フィルター モジュールをアタッチします。 この場合は、NDIS プロキシ インターフェイス プロバイダーは、インターフェイスを管理します。

-   MUX 中間ドライバー内部バインドします。 MUX 中間ドライバーには、内部のインターフェイスが NDIS に表示されないために、このケースを処理する NDIS プロバイダー サービスを実装する必要があります。

コンピューターが再起動後、インターフェイス プロバイダー割り当てることはできません、新しい[ **NET\_LUID** ](https://docs.microsoft.com/windows/desktop/api/ifdef/ns-ifdef-net_luid_lh)インターフェイスが永続的ですある場合は、同じインターフェイスの代わりに、インターフェイス。プロバイダーは、以前に保存された NET を使用する必要があります\_LUID 値と同じインターフェイスを登録します。 また、インターフェイスが永続的でない場合でもインターフェイス プロバイダー解放する必要があります、NET\_LUID インデックス コンピューターの電源障害がある場合。 したがって、インターフェイス プロバイダーは、NET を格納する必要があります\_LUID 永続的ストレージ (レジストリなど)。

インターフェイスをプロバイダーでは、インターフェイスがシャット ダウンされることを検出する場合は、インターフェイス登録解除する必要があります。

**注**  がアンインストールされ、デタッチされたときに、モジュールをフィルター処理するときに、NDIS プロキシ プロバイダー登録ミニポート アダプター用のインターフェイスを解除します。

 

インターフェイスが完全に削除されることをインターフェイスをプロバイダーが検出されたかどうか (たとえば、NDIS プロキシ プロバイダーは通知ミニポート アダプターがアンインストールされていること)、インターフェイス プロバイダーは、インターフェイスの登録を解除し、NET を解放\_LUID のインデックス。 NDIS プロキシ プロバイダーは、NET も解放\_LUID インデックスのフィルター モジュールがデタッチされるとします。

実行時に、インターフェイス プロバイダーは、登録されているインターフェイスの OID 要求を処理します。 NDIS プロキシ インターフェイス プロバイダーは、基になるドライバー インターフェイスの情報を取得する OID 要求を発行する可能性があります。

 

 





