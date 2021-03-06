---
title: OID_CO_DELETE_PVC
description: このトピックでは、OID_CO_DELETE_PVC オブジェクト識別子 (OID) について説明します。
ms.assetid: 02da08d0-9d08-4a91-b851-50e3c3b065d6
keywords:
- OID_CO_DELETE_PVC
ms.date: 11/03/2017
ms.localizationpriority: medium
ms.openlocfilehash: 01098387d069bf42f92fb8e5c028f18e8c9689ef
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843265"
---
# <a name="oid_co_delete_pvc"></a>OID_CO_DELETE_PVC

OID_CO_DELETE_PVC OID は、構成された Pvc の呼び出しマネージャーの一覧から永続的な仮想接続 (PVC) を削除するために、クライアントから呼び出しマネージャーに送信されます。 PVC は、次のように定義された CO_PVC 構造体として書式設定されます。

```c++
typedef struct _CO_PVC {
    NDIS_HANDLE             NdisAfHandle;
    CO_SPECIFIC_PARAMETERS  PvcParameters;
} CO_PVC, *PCO_PVC;
``` 

この構造体のメンバーには、次の情報が含まれています。

**NdisAfHandle**  
[NdisClOpenAddressFamilyEx](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisclopenaddressfamilyex)によって返される NDIS 提供のハンドルを指定します。

**PvcParameters**  
書式設定された[CO_SPECIFIC_PARAMETERS](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisclopenaddressfamilyex)構造体。 この構造体には、PVC を説明するプロトコル固有のパラメーターが含まれています。

PVC は、管理者によって手動で削除されます。 このようなアクティビティを監視するクライアントは、この OID を呼び出しマネージャーに送信することによって削除された PVC の呼び出しマネージャーに通知します。

## <a name="requirements"></a>要件

| | |
| --- | --- |
| バージョン | Windows Vista 以降 |
| Header | Ntddndis (Ndis .h を含む) |

