---
title: MSiSCSI\_DiscoveryConfig WMI クラス
description: MSiSCSI\_DiscoveryConfig WMI クラス
ms.assetid: dbf170ba-92ab-47bd-a076-5f54129305a5
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 316a16ebb552cc1d8e4f30ffd0a46907b65a14d1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845033"
---
# <a name="msiscsi_discoveryconfig-wmi-class"></a>MSiSCSI\_DiscoveryConfig WMI クラス


## <span id="ddk_msiscsi_discoveryconfig_wmi_class_kr"></span><span id="DDK_MSISCSI_DISCOVERYCONFIG_WMI_CLASS_KR"></span>


MSiSCSI\_DiscoveryConfig WMI クラスは、イニシエーターが探索を実行するために使用する方法を報告します。

このクラスは、 *config.xml*で次のように定義されています。

```cpp
class MSiSCSI_DiscoveryConfig {
  [key] string  InstanceName;
  boolean  Active;
  [WmiDataId(1), read, write, description("HBA should
    perform target discovery via iSNS") : amended] 
    boolean  PerformiSNSDiscovery;
  [WmiDataId(2), read, write, description("HBA should 
    perform target discovery via SLP") : amended] 
    boolean  PerformSLPDiscovery;
  [WmiDataId(3), read, write, description("Automatic 
    discovery of iSNS server") : amended] 
    boolean  AutomaticiSNSDiscovery;
  [WmiDataId(4), read, write, MaxLen(256), 
    description("Default initiator name for registering with 
    iSNS") : amended] 
    string  InitiatorName;
  [WmiDataId(5), read, write, description("Fixed Addresses 
    of iSNS servers") : amended] 
    ISCSI_IP_Address  iSNSServer;
};
```

WMI ツールスイートは、前のクラス定義をコンパイルするときに、 [**Msiscsi\_DiscoveryConfig**](https://docs.microsoft.com/windows-hardware/drivers/ddi/iscsicfg/ns-iscsicfg-_msiscsi_discoveryconfig)データ構造を生成します。

 

 





