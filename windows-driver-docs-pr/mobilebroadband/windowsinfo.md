---
title: WindowsInfo
description: WindowsInfo
ms.assetid: 62b3a7d3-503e-4815-aadb-8c67318c54e0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: aede0b8e34ad1f23d0b2258bcf5e38e82bfee0f2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63323662"
---
# <a name="windowsinfo"></a>WindowsInfo

[!include[MBAE deprecation warning](mbae-deprecation-warning.md)]

WindowsInfo 要素は、の親要素、 [WindowsInfo XML スキーマ](windowsinfo-xml-schema.md)します。

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>使用状況


``` syntax
<WindowsInfo>
  child elements
</WindowsInfo>
```

## <a name="span-idattributesspanspan-idattributesspanspan-idattributesspanattributes"></a><span id="Attributes"></span><span id="attributes"></span><span id="ATTRIBUTES"></span>属性


属性はありません。

## <a name="span-idchildelementsspanspan-idchildelementsspanspan-idchildelementsspanchild-elements"></a><span id="Child_elements"></span><span id="child_elements"></span><span id="CHILD_ELEMENTS"></span>子要素


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>要素</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="showdeviceindisconnectedstate.md" data-raw-source="[ShowDeviceInDisconnectedState](showdeviceindisconnectedstate.md)">ShowDeviceInDisconnectedState</a></p></td>
<td><p>この値に設定する必要があります<strong>false</strong>のため、Windows 8、Windows 8.1、および Windows 10 でのサービス メタデータ パッケージには適用されません。</p></td>
</tr>
<tr class="even">
<td><p><a href="launchdevicestageondeviceconnect.md" data-raw-source="[LaunchDeviceStageOnDeviceConnect](launchdevicestageondeviceconnect.md)">LaunchDeviceStageOnDeviceConnect</a></p></td>
<td><p>この値に設定する必要があります<strong>false</strong>のため、Windows 8、Windows 8.1、および Windows 10 でのサービス メタデータ パッケージには適用されません。</p></td>
</tr>
<tr class="odd">
<td><p><a href="launchdevicestagefromexplorer.md" data-raw-source="[LaunchDeviceStageFromExplorer](launchdevicestagefromexplorer.md)">LaunchDeviceStageFromExplorer</a></p></td>
<td><p>この値に設定する必要があります<strong>false</strong>のため、Windows 8、Windows 8.1、および Windows 10 でのサービス メタデータ パッケージには適用されません。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idparentelementsspanspan-idparentelementsspanspan-idparentelementsspanparent-elements"></a><span id="Parent_elements"></span><span id="parent_elements"></span><span id="PARENT_ELEMENTS"></span>親要素


親要素はありません。

## <a name="span-idxsdspanspan-idxsdspanxsd"></a><span id="XSD"></span><span id="xsd"></span>XSD


``` syntax
<xs:element name="WindowsInfo" type="tns:WindowsInfoType" />

<xs:complexType name="WindowsInfoType">
  <xs:sequence>
    <xs:element name="ShowDeviceInDisconnectedState" type="xs:boolean" default="false" />
    <xs:element name="LaunchDeviceStageOnDeviceConnect" type="xs:boolean" default="false" minOccurs="0" />
    <xs:element name="LaunchDeviceStageFromExplorer" type="xs:boolean" default="false" minOccurs="0" />
    <xs:element ref="v2:LaunchApplicationOnDeviceConnect" minOccurs="0" />
    <xs:element ref="v2:WindowsHardwareLogoCertified" minOccurs="0" />
  </xs:sequence>
</xs:complexType>
```

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>注釈


WindowsInfo 要素が必要です。

 

 





