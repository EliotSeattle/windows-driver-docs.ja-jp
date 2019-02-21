---
title: GUIDType (ServiceInfo)
description: GUIDType (ServiceInfo)
ms.assetid: a08d4c7c-c282-4870-b836-6788ffa2d088
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b979649c213b7d7b515c34755477c041c2ae49bc
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56527237"
---
# <a name="guidtype-serviceinfo"></a>GUIDType (ServiceInfo)

[!include[MBAE deprecation warning](mbae-deprecation-warning.md)]

GUIDType XML 単純型では、GUID を指定します。

``` syntax
<xs:simpleType name="GUIDType">
  <xs:restriction base="xs:string">
    <xs:pattern value="[0-9a-fA-F]{8}-[0-9a-fA-F]{4}-[0-9a-fA-F]{4}-[0-9a-fA-F]{4}-[0-9a-fA-F]{12}" />
  </xs:restriction>
</xs:simpleType>
```

## <a name="span-idpatternsspanspan-idpatternsspanspan-idpatternsspanpatterns"></a><span id="Patterns"></span><span id="patterns"></span><span id="PATTERNS"></span>パターン


GUIDType 単純型は、 **xs:string**は、次のパターンによって制限されています。

-   \[0 9a-fA F\]{8}-\[0 9a-fA F\]{4}-\[0 9a-fA F\]{4}-\[0 9a-fA F\]{4}-\[0 9a-fA F\]{12}

 

 





