---
title: MS\_SM\_AdapterInformationQuery WMI クラス
description: MS\_SM\_AdapterInformationQuery WMI クラス
ms.assetid: 3a396a73-6ade-455a-ac3f-fd0175cc704e
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 7c8b53293aeb4921431e742a25e4752efe00eafb
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386144"
---
# <a name="mssmadapterinformationquery-wmi-class"></a>MS\_SM\_AdapterInformationQuery WMI クラス


記憶域管理 API をサポートする HBA ミニポート ドライバーは、MS を使用して\_SM\_AdapterInformationQuery クラスは、SAS アダプターに関連付けられている属性の情報を公開します。

MS\_SM\_AdapterInformationQuery クラスが次のように定義されている*Hbaapi.mof*:

```cpp
class MS_SM_AdapterInformationQuery
{
    [key] 
    string  InstanceName;
    boolean Active;

    [Description ("Unique identifier for the adapter. This idenitifer must "
                  "be unique among all adapters. The same "
                  "value for the identifier must be used for the same adapter "
                  "in other classes that expose adapter information"),

  // WmiRefClass("MS_SM_ChannelAdapter"),  // ?? need a new ref class
     WmiRefProperty("UniqueAdapterId"),
     WmiDataId(1)
    ]
    uint64 UniqueAdapterId;             // CIM_FibreChannelAdapter REF
                                        // ?? need a new REF 

    [HBA_STATUS_QUALIFIERS, 
     WmiDataId(2)
    ]
    HBA_STATUS HBAStatus;

    [WmiDataId(3)]
    uint32 NumberOfPorts;   

    [WmiDataId(4)]
    uint32 VendorSpecificID;

    [
     cpp_quote("\n"
     "   //******************************************************************\n"
     "   //\n"
     "   //  The string type is variable length (up to MaxLen).              \n"
     "   //  Each string starts with a ushort that holds the strings length  \n"
     "   //  (in bytes) followed by the WCHARs that make up the string.      \n"
     "   //\n"
     "   //******************************************************************\n"
     "\n"),

     MaxLen(64), 
     WmiDataId(5)
    ]
    string Manufacturer;

    [MaxLen(64), WmiDataId(6)]
    string SerialNumber;

    [MaxLen(256), WmiDataId(7)]
    string Model;

    [MaxLen(256), WmiDataId(8)]
    string ModelDescription;

    [MaxLen(256), WmiDataId(9)]
    string HardwareVersion;

    [MaxLen(256), WmiDataId(10)]
    string DriverVersion;

    [MaxLen(256), WmiDataId(11)]
    string OptionROMVersion;

    [MaxLen(256), WmiDataId(12)]
    string FirmwareVersion;

    [MaxLen(256), WmiDataId(13)]
    string DriverName;

    [MaxLen(256), WmiDataId(14)]
    string HBASymbolicName;

    [MaxLen(256), WmiDataId(15)]
    string RedundantOptionROMVersion;

    [MaxLen(256), WmiDataId(16)]
    string RedundantFirmwareVersion;

    [MaxLen(256), WmiDataId(17)]
    string MfgDomain;
};
```

このクラスの定義が WMI ツール スイートによってコンパイルされると、次のデータ構造が生成されます。

[**MS\_SM\_AdapterInformationQuery**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_ms_sm_adapterinformationquery)

この WMI クラスに関連付けられているメソッドはありません。

 

 





