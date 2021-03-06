---
title: finishTitle XML 要素
description: finishTitle XML 要素
ms.assetid: d8730b49-9cc0-46f4-88a1-fd5543063277
keywords:
- finishTitle XML 要素のデバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- finishTitle XML Element
api_type:
- NA
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 3d8580cc4ac00744c39de0c1f24d2493b7fd9a3d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360304"
---
# <a name="finishtitle-xml-element"></a>finishTitle XML 要素


\[DIFx は非推奨、詳細については、「 [DIFx ガイドライン](https://docs.microsoft.com/windows-hardware/drivers/install/difx-guidelines)します。\]

**FinishTitle** XML 要素が DPInst の完了 ページの上部に表示される 完了 のタイトルのテキストをカスタマイズします。

### <a name="element-tag"></a>**要素タグ**

```cpp
<finishTitle>
```

### <a name="xml-attributes"></a>**XML 属性**

なし

### <a name="element-information"></a>**要素情報**

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>親要素</strong></p></td>
<td align="left"><p><a href="language-xml-element.md" data-raw-source="[&lt;strong&gt;language&lt;/strong&gt;](language-xml-element.md)"><strong>言語</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>子要素</strong></p></td>
<td align="left"><p>許可なし</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>データの内容</strong></p></td>
<td align="left"><p>[完了] ページの上部でタイトルのテキストをカスタマイズする文字列。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>子要素が重複しています</strong></p></td>
<td align="left"><p>許可なし</p></td>
</tr>
</tbody>
</table>

 

### <a href="" id="comments"></a>「解説」

次のコード例に示します、 **finishTitle** [完了] ページの上部でタイトルのテキストをカスタマイズする要素。 カスタム タイトル テキストを指定するテキストが太字のフォント スタイルで表示されます。

```cpp
dpinst>
  ...
  <language code="0x0409">
    ...
    <finishTitle>Congratulations! You are finished installing your Toaster device.</finishTitle>
    ...
  </language>
  ...
</dpinst>
```

場合、 **finishTitle**要素が指定されていない、DPInst は既定の [完了] ページに表示される既定のタイトル テキストを表示します。

## <a name="see-also"></a>関連項目


[**finishText**](finishtext-xml-element.md)

[**言語**](language-xml-element.md)

 

 






