---
title: バージョン
description: バージョン
ms.assetid: 1a476586-bef9-41ec-8e8a-f4343361dc92
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0c6fa8c49eda306a900d5f509e60bda375190b91
ms.sourcegitcommit: f017184b00f59b088df87a5bd85fec51b7aed8b2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/15/2019
ms.locfileid: "72323651"
---
# <a name="version"></a>バージョン

[!include[MBAE deprecation warning](mbae-deprecation-warning.md)]

Version 要素は、サービスメタデータパッケージを作成したアプリケーションソフトウェアのバージョンを指定します。

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>ユーセジリンク


``` syntax
<Version>
  text
</Version>
```

## <a name="span-idattributesspanspan-idattributesspanspan-idattributesspanattributes"></a><span id="Attributes"></span><span id="attributes"></span><span id="ATTRIBUTES"></span>アトリビュート


属性はありません。

## <a name="span-idchild_elementsspanspan-idchild_elementsspanspan-idchild_elementsspanchild-elements"></a><span id="Child_elements"></span><span id="child_elements"></span><span id="CHILD_ELEMENTS"></span>子要素


子要素はありません。

## <a name="span-idparent_elementsspanspan-idparent_elementsspanspan-idparent_elementsspanparent-elements"></a><span id="Parent_elements"></span><span id="parent_elements"></span><span id="PARENT_ELEMENTS"></span>親要素


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
<td><p><a href="metadatabuilderinformation.md" data-raw-source="[MetadataBuilderInformation](metadatabuilderinformation.md)">MetadataBuilderInformation</a></p></td>
<td><p><a href="metadatabuilderinformation.md" data-raw-source="[MetadataBuilderInformation](metadatabuilderinformation.md)">MetadataBuilderInformation</a>要素は、サービスメタデータパッケージを作成したアプリケーションを指定します。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idxsdspanspan-idxsdspanxsd"></a><span id="XSD"></span><span id="xsd"></span>XSD.EXE


``` syntax
<xs:element name="Version" type="tns:VersionType" />

<xs:simpleType name="VersionType">
  <xs:restriction base="xs:string">
    <xs:minLength value="1" />
    <xs:maxLength value="256" />
  </xs:restriction>
</xs:simpleType>
```

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>注釈


Version 要素は、Windows 7 オペレーティングシステムでは使用されません。 OEM および開発者が使用するために予約されています。

 

 





