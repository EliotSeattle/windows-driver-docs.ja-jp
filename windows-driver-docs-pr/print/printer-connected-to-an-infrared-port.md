---
title: 赤外線ポートに接続されているプリンター
description: 赤外線ポートに接続されているプリンター
ms.assetid: 8545cf66-9b5c-41e8-82e0-e0edd75ad41b
keywords:
- 赤外線ポート WDK プリンター
- 赤外線ポート WDK プリンター
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6c8fa5091cdaafcf25f28b685ce69ead29318a0e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380666"
---
# <a name="printer-connected-to-an-infrared-port"></a>赤外線ポートに接続されているプリンター





赤外線 (IR) ポート経由で接続されているプリンターでは、1284 デバイスの文字列を使用して、プラグ アンド プレイをサポートしていません。 赤外線ポートを使用しているコンピューターでのサービスは、常にデバイスをポーリングします。 列挙型では、PDO は作成、IR のプラグ アンド プレイ プリンターが範囲内になる\\ルート\\で、*デバイス ID*フォーム HWP の*nnnn*します。 *ハードウェア ID*の*devnode* HWP フォームの 1 つのエントリが*nnnn*します。

[ **INF 製造元セクション**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-manufacturer-section) lpt ポートと赤外線ポート経由でプラグ アンド プレイをサポートしているプリンターのエントリは、次のような表示する必要があります。

```cpp
 
"Model Name XYZ" = Install_Section_XYZ, LPTENUM\Company_NameModelNam1234, Company_NameModelNam1234, Model_Name_XYZ
"Model Name XYZ" = Install_Section_XYZ, HWP9876, Model_Name_XYZ
```

 

 




