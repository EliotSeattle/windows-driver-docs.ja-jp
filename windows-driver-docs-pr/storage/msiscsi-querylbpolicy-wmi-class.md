---
title: MSiSCSI\_QueryLBPolicy WMI クラス
description: MSiSCSI\_QueryLBPolicy WMI クラス
ms.assetid: 1d80f525-491a-4c81-8827-7c5c13107a54
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: f8d3c7f9dc6d5ba7769cb01a1ac9b31f24569d5c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845333"
---
# <a name="msiscsi_querylbpolicy-wmi-class"></a>MSiSCSI\_QueryLBPolicy WMI クラス


MSiSCSI\_QueryLBPolicy WMI クラスには、負荷分散ポリシーに関する情報が含まれています。 このクラスは、管理 .mof で次のように定義されてい*ます。*

```cpp
class MSiSCSI_QueryLBPolicy 
{
    [key]
    string InstanceName;

    boolean Active;

    [WmiDataId(1),
     DisplayName("Adapter Id") : amended,
     DisplayInHex,
     Description("Id that is globally unique to each instance of each adapter. Using the address of the Adapter Extension is a good idea.") : amended
    ]
    uint64 UniqueAdapterId;

    [WmiDataId(2),
     read,
     DisplayName("Reserved field") : amended
    ] uint32 Reserved;

    [WmiDataId(3),
     read,
     DisplayName("Count of Elements in LoadBalancePolicies array") : amended,
     cpp_quote("\n    // Number of elements in LoadBalancePolicies array\n"),
     Description("Number of elements in LoadBalancePolicies array") : amended
    ] uint32 SessionCount;

    [WmiDataId(4),
     DisplayName("Load Balance Policy for each session") : amended,
     description("Load Balance Policy that is currently being used by iSCSI Initiator - one element for each session on the adapter") : amended,
     WmiSizeIs("SessionCount")
    ]
    ISCSI_Supported_LB_Policies LoadBalancePolicies[];
};
```

WMI ツールスイートは、前のクラス定義をコンパイルするときに、 [**Msiscsi\_QueryLBPolicy**](https://docs.microsoft.com/windows-hardware/drivers/ddi/iscsimgt/ns-iscsimgt-_msiscsi_querylbpolicy)データ構造体を生成します。

 

 





