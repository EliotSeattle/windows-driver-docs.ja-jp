---
title: ISCSI\_PortalInfo WMI クラス
description: ISCSI\_PortalInfo WMI クラス
ms.assetid: b38aa87c-00a5-483e-aa44-23f359783829
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: d8bb4958295d5afb89b2119f8db4a490df28f679
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63359682"
---
# <a name="iscsiportalinfo-wmi-class"></a>ISCSI\_PortalInfo WMI クラス


## <span id="ddk_iscsi_portalinfo_wmi_class_kr"></span><span id="DDK_ISCSI_PORTALINFO_WMI_CLASS_KR"></span>


ISCSI\_PortalInfo WMI クラスには、iSCSI ポータルに関連する情報が含まれています。 このクラスが次のように定義されている*Mgmt.mof*します。

```cpp
class ISCSI_PortalInfo
{
    [read,
     WmiDataId(1),
     description("An integer used to uniquely identify a paticular port"),
     WmiVersion(1)] uint32 Index;

    [read,
     WmiDataId(2),
     ISCSI_PORTAL_TYPE_QUALIFIERS,
     description("**typedef** The type of portal (Initiator or Target) \n"),
     WmiVersion(1)] ISCSI_PORTAL_TYPE PortalType;

    [read,
     WmiDataId(3),
     ISCSI_CONNECTION_PROTOCOL_TYPE_QUALIFIERS,
     //Description("The portal's transport protocol"): amended,
     description("The portal's transport protocol"),
     WmiVersion(1)] ISCSI_CONNECTION_PROTOCOL_TYPE Protocol;

    [read,
     WmiDataId(4),
     WmiVersion(1)] uint8 Reserved1;

    [read,
     WmiDataId(5),
     WmiVersion(1)] uint8 Reserved2;
 
    [read,
     WmiDataId(6),
     description("The portal's network address"),
     WmiVersion(1)] ISCSI_IP_Address IPAddr;

    [read,
     WmiDataId(7),
     description("The portal's socket number"),
     WmiVersion(1)] uint32 Port;

    [read,
     WmiDataId(8),
     description("The portal's aggregation tag"),
     WmiVersion(1)] uint16 PortalTag;
};
```

WMI ツールのスイートでは、上記のクラス定義をコンパイルするときに生成、 [ **ISCSI\_PortalInfo** ](https://msdn.microsoft.com/library/windows/hardware/ff561557)データ構造体。

 

 





