---
title: 使用できないシンボル ストアを処理します。
description: 使用できないシンボル ストアを処理します。
ms.assetid: 42e3518b-b139-49cd-96cc-ea31f6df7964
keywords:
- SymProxy、ストアが利用不可
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 838b9e52c1bb27d61bb4a250201fe58face94809
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56535973"
---
# <a name="dealing-with-unavailable-symbol-stores"></a>使用できないシンボル ストアを処理します。


取得する SymSrv が構成されているシンボルの 1 つ格納されている場合は、ファイルからが停止しているか利用できない状態には、結果ファイルの要求ごとに、クライアントから待機時間が長い場合があります。 SymSrv は SymProxy から呼び出されると、問題のストアにアクセスしようとして停止する SymSrv を設定してこれらの待機のほとんどを回避できます。 この機能が関与している場合は、一定の時間間隔を設定中に指定された数の同じストアからのタイムアウトが発生した後のストアを使用しようとしています。 SymSrv が停止します。 .Ini ファイルまたはレジストリから、これらの変数の値を制御できます。

**.Ini ファイルを使用してシンボル ストアのアクセスを制御するには**

1.  %Windir%\\system32\\inetsrv\\Symsrv.ini、という名前のセクションを作成する**タイムアウト**します。

2.  値を追加**トリガー**、**カウント**、および**ブラック アウト**このセクションにします。

**トリガー**時間のタイムアウトを監視する (分) の量を示します。 **カウント**中に検索するタイムアウトの数を示す、**トリガー**期間。 **ブラック アウト**しきい値に達した後に、ストアを無効にする分単位の時間の長さを示します。

たとえば、次の設定お勧めします。

```ini
[timeouts]
trigger=10
count=5
blackout=15
```

この例で、ストアへのアクセスは 10 分間に 5 つのタイムアウトが発生する場合をオフになります。 15 分のブラック アウトが完成したら、ストアが再アクティブ化します。

**レジストリを使用してシンボル ストアのアクセスを制御するには**

1.  という名前のキーを作成します。

    ```text
    HKLM\ Software\Microsoft\Symbol Server\Timeouts
    ```

2.  次の 3 つの REG 追加\_DWORD 値**トリガー**、**カウント**と**ブラック アウト**このキーにします。 .Ini ファイルで行うように、これらの値を設定します。

トリガー、count、またはブラック アウト値のいずれかが 0 に設定されている場合は、レジストリまたは .ini ファイルを使用するかどうか、またはキーまたは値のいずれかが存在しない場合は、この機能は無効です。

サービスとして実行されている場合にのみ、SymSrv のこの機能は現在使用可能なは。 つまり、この機能の唯一の現実的なアプリケーションではの SymProxy から呼び出された場合。

 

 




