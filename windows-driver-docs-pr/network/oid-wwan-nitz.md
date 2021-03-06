---
title: OID_WWAN_NITZ
description: ネットワーク Id とタイムゾーン (NITZ) を使用して現在のネットワーク時刻を照会するには、OID_WWAN_NITZ を使用します。
ms.assetid: 5AC5842E-CBD1-47E0-88D2-D3F58CC6F142
ms.date: 04/11/2019
keywords:
- Windows Vista 以降のネットワークドライバーの OID_WWAN_NITZ
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: b048475b19bdd02951b4c506ceae6a56a60adeab
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843826"
---
# <a name="oid_wwan_nitz"></a>OID_WWAN_NITZ

ネットワーク Id とタイムゾーン (NITZ) を使用して現在のネットワーク時刻を照会するには、OID_WWAN_NITZ を使用します。

ミニポートドライバーは、クエリ要求を非同期的に処理し、その後、現在のネットワーク時刻とタイムゾーンを記述する[**NDIS_WWAN_NITZ_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_nitz_info)構造を含む[NDIS_STATUS_WWAN_NITZ_INFO](ndis-status-wwan-nitz-info.md)状態通知を送信する前に、最初に元の要求に NDIS_STATUS_INDICATION_REQUIRED を返す必要があります。

Set 要求は適用できません。

## <a name="remarks"></a>注釈

この OID の使用方法の詳細については、「 [MB NITZ サポート](mb-nitz-support.md)」を参照してください。

## <a name="requirements"></a>要件

|   |   |
| --- | --- |
| バージョン | Windows 10 バージョン 1903 |
| Header | Ntddndis (Ndis .h を含む) |

## <a name="see-also"></a>関連項目

[MB NITZ のサポート](mb-nitz-support.md)

[NDIS_STATUS_WWAN_NITZ_INFO](ndis-status-wwan-nitz-info.md)

[**NDIS_WWAN_NITZ_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_nitz_info)
