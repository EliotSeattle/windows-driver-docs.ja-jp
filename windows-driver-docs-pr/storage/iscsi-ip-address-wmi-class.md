---
title: ISCSI\_IP\_アドレスの WMI クラス
description: ISCSI\_IP\_アドレスの WMI クラス
ms.assetid: 3ceeb54f-ecc5-40c5-b0a8-8c6f86203f1c
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: c0738f9bc137a4adaf8e753a1631f7088c0a9265
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528523"
---
# <a name="iscsiipaddress-wmi-class"></a>ISCSI\_IP\_アドレスの WMI クラス


## <span id="ddk_iscsi_ip_address_wmi_class_kr"></span><span id="DDK_ISCSI_IP_ADDRESS_WMI_CLASS_KR"></span>


ISCSI\_IP\_Address クラスが使用されている IP プロトコルのバージョンから独立している IP アドレスの定義を提供します。 このクラスで定義されます*Common.mof*します。

```cpp
class ISCSI_IP_Address {
  [WmiDataId(1), read, write, DisplayName("Address Format")
    : amended, description("Type of address specified. 
    It can be text: a DNS or dotted address or it can be
    a binary ipv4 or ipv6 address") : amended,
    Values{ "Text Address", "IpV4 Address",
            "IpV6 Address", "Empty Address"},
    ValueMap{"0", "1", "2", "3"}]
#define ISCSIIPADDRESSTYPE  uint32
  ISCSIIPADDRESSTYPE  Type;
  [WmiDataId(2), read, write, DisplayInHex,
    DisplayName("IPV4 Address"): amended,
    description("If IPV4 Address is specified as the 
    Address Format then this contains the binary IPv4 
    ip address") : amended]
    uint32  IpV4Address;
  [WmiDataId(3), DisplayName("IPV6 Address"): amended,
    read, write, description("If IPV6 Address is 
    specified as the Address Format then this contains 
    the binary IPv6 ip address") : amended]
    uint8  IpV6Address[16];
  [WmiDataId(4), read, write,
    DisplayName("IPV6 Flow Information") : amended,
    description("IPV6 flow information") : amended]
    uint32  IpV6FlowInfo;
  [WmiDataId(5), read, write,
    DisplayName("IPV6 Scope Id") : amended,
    description("IPV6 scope id") : amended]
    uint32  IpV6ScopeId;
  [WmiDataId(6), read, write,
    DisplayName("Text Address") : amended,
    description("Text address, either a DNS address or
    dotted address") : amended, 
    MaxLen(MAX_ISCSI_TEXT_ADDRESS_LEN)]
    string  TextAddress;
};
```

WMI ツールのスイートでは、上記のクラス定義をコンパイルするときに生成、 [ **ISCSI\_IP\_アドレス**](https://msdn.microsoft.com/library/windows/hardware/ff561536)データ構造体。

 

 





