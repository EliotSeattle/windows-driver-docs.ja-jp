---
title: TCP/IP タスクオフロードの概要
description: TCP/IP タスクオフロードの概要
ms.assetid: e73cc4e8-574b-438b-acd2-f0aaf5c20589
keywords:
- TCP/IP オフロード WDK ネットワーク、タスクオフロード
- WDK TCP/IP トランスポートのオフロード、タスクオフロード
- タスクオフロード WDK TCP/IP トランスポート
- タスクオフロード WDK TCP/IP トランスポート、タスクオフロードについて
- 機能 WDK TCP/IP オフロード
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2757c34d2b720fc5173d47229c9c1aff6b8c6083
ms.sourcegitcommit: fec48fa5342d9cd4cd5ccc16aaa06e7c3d730112
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2019
ms.locfileid: "69565696"
---
# <a name="tcpip-task-offload-overview"></a>TCP/IP タスクオフロードの概要





Microsoft TCP/IP トランスポートでは、パフォーマンスを向上させるために、適切なタスクオフロード機能を備えたネットワークインターフェイスカード (NIC) にタスクをオフロードすることができます。

Windows Vista 以降の Windows オペレーティングシステムでは、次のタスクオフロードサービスがサポートされています。

### <a name="checksum-tasks"></a>チェックサムタスク

TCP/IP トランスポートは、IP および TCP チェックサムの計算と検証をオフロードできます。

### <a name="internet-protocol-security-ipsec-offload-version-1-ipsecov1"></a>インターネットプロトコルセキュリティ (IPsec) オフロードバージョン 1 (IPsecOV1)

\[IPsec タスクオフロード機能は非推奨とされており、使用しないでください。\]

TCP/IP トランスポートでは、認証ヘッダー (AH)、カプセル化セキュリティペイロード (ESP)、またはその両方の暗号化されたチェックサムの計算と検証をオフロードできます。 TCP/IP トランスポートでは、ESP ペイロードの暗号化と復号化、およびユーザーデータグラムプロトコル (UDP) でカプセル化された ESP データパケットの暗号化と復号化をオフロードすることもできます。

IPsecOV1 の詳細については、「 [IPsec オフロードバージョン 1](ipsec-offload-version-1.md)」を参照してください。

### <a name="internet-protocol-security-ipsec-offload-version-2-ipsecov2"></a>インターネットプロトコルセキュリティ (IPsec) のオフロードバージョン 2 (IPsecOV2)

\[IPsec タスクオフロード機能は非推奨とされており、使用しないでください。\]

TCP/IP トランスポートでは、認証ヘッダー (AH)、カプセル化セキュリティペイロード (ESP)、またはその両方の暗号化されたチェックサムの計算と検証をオフロードできます。 TCP/IP トランスポートでは、ESP ペイロードの暗号化と復号化、およびユーザーデータグラムプロトコル (UDP) でカプセル化された ESP データパケットの暗号化と復号化をオフロードすることもできます。 IPsecOV2 は、NDIS 6.1 以降のバージョンでサポートされています。

IPsecOV2 の詳細については、「 [IPsec Offload Version 2](ipsec-offload-version-2.md)」を参照してください。

### <a name="large-send-offload-version-1-lsov1"></a>Large send offload バージョン 1 (LSOV1)

TCP/IP トランスポートでは、large send offload version 1 (LSOV1) がサポートされています。 LSOV1 を使用すると、TCP/IP トランスポートは IPv4 の TCP パケットを含む大容量 (IP ヘッダーを含む最大 64 KB) のセグメント化をオフロードできます。

### <a name="large-send-offload-version-2-lsov2"></a>Large send offload version 2 (LSOV2)

Large send offload version 2 (LSOV2) インターフェイスは、LSOV1 の拡張バージョンです。 LSOV2 では、64K を超える大きな TCP パケットの IPv6、IPv4、およびセグメンテーションがサポートされています。 大きいパケットのセグメント化のオフロードの詳細については、「[大きな TCP パケットのセグメント化のオフロード](offloading-the-segmentation-of-large-tcp-packets.md)」を参照してください。

Windows 8 と windows Server 2012 以降では、Windows オペレーティングシステムは、次の追加のタスクオーバーロードサービスをサポートしています。

### <a name="receive-segment-coalescing-rsc"></a>Receive Segment Coalescing (RSC)

受信セグメント合体 (RSC) を使用すると、ネットワークカードミニポートドライバーは複数の TCP セグメントを結合し、オペレーティングシステムのネットワークサブシステムに対して1つの結合された単位 (SCU) として示すことができます。

### <a name="network-virtualization-using-generic-routing-encapsulation-nvgre-task-offload"></a>汎用ルーティング カプセル化 (NVGRE) タスク オフロードを使用したネットワークの仮想化

[汎用ルーティングカプセル化 (NVGRE) タスクオフロードを使用したネットワーク仮想化](network-virtualization-using-generic-routing-encapsulation--nvgre--task-offload.md)により、汎用ルーティングカプセル化 (GRE) でカプセル化されたパケットを使用できるようになります。

-   Large Send Offload (LSO)
-   Receive Side Scaling (RSS)
-   仮想マシン キュー (VMQ)

このセクションの内容:

-   [タスクオフロード機能の決定](determining-task-offload-capabilities.md)
-   [タスクオフロードサービスの有効化と無効化](enabling-and-disabling-task-offload-services.md)
-   [現在のタスクのオフロード設定を確認しています](determining-the-current-task-offload-settings.md)
-   [タスクのオフロードの種類の組み合わせ](combining-types-of-task-offloads.md)
-   [レジストリ値を使用してタスクオフロードを有効または無効にする](using-registry-values-to-enable-and-disable-task-offloading.md)
-   [チェックサムタスクのオフロード](offloading-checksum-tasks.md)
-   [IPsec タスクのオフロード](offloading-ipsec-tasks.md)
    - \[IPsec タスクオフロード機能は非推奨とされており、使用しないでください。\]
-   [大きな TCP パケットのセグメント化のオフロード](offloading-the-segmentation-of-large-tcp-packets.md)

 

 





