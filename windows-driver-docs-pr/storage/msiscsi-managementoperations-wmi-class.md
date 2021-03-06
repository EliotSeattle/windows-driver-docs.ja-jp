---
title: MSiSCSI\_ManagementOperations WMI クラス
description: MSiSCSI\_ManagementOperations WMI クラス
ms.assetid: 1037be46-6cae-458d-8549-927c7a053195
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 25e853881189b03e4526a88a1ab18289f12222cc
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845344"
---
# <a name="msiscsi_managementoperations-wmi-class"></a>MSiSCSI\_ManagementOperations WMI クラス


MSiSCSI\_MangementOperations WMI クラスには、送信先アドレスに対して ICMP ping 要求を実行するための ping メソッドが含まれています。 このクラスは、管理 .mof で次のように定義されています。

```cpp
class MSiSCSI_ManagementOperations
{
    //
    // This class must be registered using PDO instance names
    //
    [key]
    string InstanceName;
 
    boolean Active;

    [WmiMethodId(10),
     Implemented,
     Description("Perform an ICMP ping") : amended,
     cpp_quote(
"//\n"
"// This method is recommended.\n"
"//\n"             
"// Ping will perform ICMP ping requests to the destination address \n"
"// and return the number of ping responses received. This is only supported\n"
"// by some HBA, use the ping command for the software initiator.\n"
"//\n"
              )            
    ]
    void PingIPAddress(
                     [in,
                      Description("Number of requests to send") : amended
                     ] uint32 RequestCount,

                     [in,
                      Description("Number of bytes in each request") : amended
                     ] uint32 RequestSize,

                     [in,
                      Description("Number of ms to wait for response") : amended
                     ] uint32 Timeout,

                     [in,
                      description("IP address to ping") : amended
                     ] ISCSI_IP_Address Address,
 
                     [out,
                      ISCSI_STATUS_QUALIFIERS
                     ] ISCSI_STATUS Status,
 
                     [out,
                      Description("Number of responses received") : amended
                     ] uint32 ResponsesReceived

                    );

 
};
```

WMI ツールスイートは、前のクラス定義をコンパイルするときに、 [Msiscsi\_ManagementOperations](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)データ構造体の1つを生成します。

 

 





