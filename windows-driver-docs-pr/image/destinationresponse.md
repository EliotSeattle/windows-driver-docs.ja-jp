---
title: DestinationResponse 要素
description: 必要な DestinationResponse 要素には、1 つ ScanDestination 登録応答情報が含まれています。
ms.assetid: 388304ca-4d62-40cf-ad68-13607a836caf
keywords:
- DestinationResponse 要素イメージング デバイス
topic_type:
- apiref
api_name:
- wscn DestinationResponse
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 43cf9feb3851452b48e97db1cefb9ec492eb649b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63373199"
---
# <a name="destinationresponse-element"></a>DestinationResponse 要素


必要な**DestinationResponse**要素には、1 つの応答の情報が含まれています。 [ **ScanDestination** ](scandestination.md)登録します。

<a name="usage"></a>使用方法
-----

```xml
<wscn:DestinationResponse>
  child elements
</wscn:DestinationResponse>
```

<a name="attributes"></a>属性
----------

属性はありません。

## <a name="child-elements"></a>子要素


<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th>要素</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>&lt;ベンダー定義要素&gt;</p></td>
</tr>
<tr class="even">
<td><p><a href="clientcontext.md" data-raw-source="[&lt;strong&gt;ClientContext&lt;/strong&gt;](clientcontext.md)"><strong>ClientContext</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><a href="destinationtoken.md" data-raw-source="[&lt;strong&gt;DestinationToken&lt;/strong&gt;](destinationtoken.md)"><strong>DestinationToken</strong></a></p></td>
</tr>
</tbody>
</table>

## <a name="parent-elements"></a>親要素


<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th>要素</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="destinationresponses.md" data-raw-source="[&lt;strong&gt;DestinationResponses&lt;/strong&gt;](destinationresponses.md)"><strong>DestinationResponses</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>注釈
-------

**DestinationResponse**要素が含まれています、 [ **ClientContext** ](clientcontext.md)要素からその照合[ **ScanDestination**](scandestination.md)要素、クライアントが応答を識別できるようにします。 **DestinationResponse**も含まれています、 [ **DestinationToken** ](destinationtoken.md)すべてで使用するための要素[ **CreateScanJobRequest** ](createscanjobrequest.md)このターゲットからの要素を操作します。

## <a name="see-also"></a>関連項目


[**ClientContext**](clientcontext.md)

[**CreateScanJobRequest**](createscanjobrequest.md)

[**DestinationResponses**](destinationresponses.md)

[**DestinationToken**](destinationtoken.md)

[**ScanDestination**](scandestination.md)

 

 






