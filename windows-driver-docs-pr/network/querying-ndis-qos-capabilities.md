---
title: NDIS QoS 機能のクエリ
description: NDIS QoS 機能のクエリ
ms.assetid: 00A2EFCD-CD90-446C-B588-EC66E3E730B2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e3af0c60c0937146a40d78f165d8c1be11648a77
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385423"
---
# <a name="querying-ndis-qos-capabilities"></a>NDIS QoS 機能のクエリ


プロトコルとフィルター ドライバーに関連は次のように、ネットワーク アダプターの NDIS サービスの品質 (QoS) 機能を照会できます。

-   上にあるドライバーは、オブジェクト識別子 (OID) のクエリ要求のを通じてネットワーク アダプターでサポートされているハードウェアの NDIS QoS 機能を照会できます[OID\_QOS\_ハードウェア\_機能](https://docs.microsoft.com/windows-hardware/drivers/network/oid-qos-hardware-capabilities)します。

-   上にあるドライバーは現在の OID クエリ要求を使ってネットワーク アダプターで有効になっているハードウェアの NDIS QoS 機能を照会できます[OID\_QOS\_現在\_機能](https://docs.microsoft.com/windows-hardware/drivers/network/oid-qos-current-capabilities)します。

NDIS は、ミニポート ドライバーのこれらの OID 要求を処理します。 登録すると、ミニポート ドライバー ハードウェアおよびネットワーク アダプターの NDIS QoS 機能が現在有効なネットワーク アダプターの初期化中に、NDIS は、この情報をキャッシュします。 NDIS は、上にある、ドライバーから OID の要求を処理する場合、このデータを返します。

ミニポート ドライバーが NDIS QoS 機能を登録する方法の詳細については、次を参照してください。 [NDIS QoS 機能の登録](registering-ndis-qos-capabilities.md)します。

 

 





