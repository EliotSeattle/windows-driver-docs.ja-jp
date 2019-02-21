---
title: 構成記述子
description: 構成記述子
ms.assetid: 256edfa8-de02-438d-b4ce-0a2df0d0f46e
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6768651c9c16aff0bbd80941b66938132672ccd7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56556550"
---
# <a name="configuration-descriptor"></a>構成記述子





<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Offset</th>
<th align="left">フィールド</th>
<th align="left">サイズ</th>
<th align="left">Value</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0</p></td>
<td align="left"><p>bLength</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>0x09</p></td>
<td align="left"><p>この記述子は、バイト単位のサイズ</p></td>
</tr>
<tr class="even">
<td align="left"><p>1</p></td>
<td align="left"><p>bDescriptorType</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>0x02</p></td>
<td align="left"><p>構成記述子</p></td>
</tr>
<tr class="odd">
<td align="left"><p>2</p></td>
<td align="left"><p>wTotalLength</p></td>
<td align="left"><p>2</p></td>
<td align="left"><p>0x003E</p></td>
<td align="left"><p>この記述子と次のすべての記述子を含む (バイト単位)、全体の構成ブロックの長さ</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>bNumInterfaces</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>0x02</p></td>
<td align="left"><p>2 つのインターフェイス</p></td>
</tr>
<tr class="odd">
<td align="left"><p>5</p></td>
<td align="left"><p>bConfigurationValue</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>0x01</p></td>
<td align="left"><p>この構成の ID</p></td>
</tr>
<tr class="even">
<td align="left"><p>6</p></td>
<td align="left"><p>iConfiguration</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>0x00</p></td>
<td align="left"><p>未使用</p></td>
</tr>
<tr class="odd">
<td align="left"><p>7</p></td>
<td align="left"><p>bmAttributes</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>0x80</p></td>
<td align="left"><p>バスの電源</p></td>
</tr>
<tr class="even">
<td align="left"><p>8</p></td>
<td align="left"><p>MaxPower</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>0x64</p></td>
<td align="left"><p>200 mA</p></td>
</tr>
</tbody>
</table>

 

 

 





