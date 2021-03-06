---
title: リークが存在するかどうかの判別
description: リークが存在するかどうかの判別
ms.assetid: a29db56e-6507-48f4-ad30-eb0a849f8673
keywords:
- メモリ リークの検出
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3a685b39143c5acf5773c90c7a70fe50285e3c8e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63346292"
---
# <a name="determining-whether-a-leak-exists"></a>リークが存在するかどうかの判別


Windows のパフォーマンスが時間の経過と共に低下させること、メモリ リークが含まれている疑いがある場合は、このセクションで説明した手法は、メモリ リークがあるかどうかを指定できます。 わかりません、リークの原因とは何もユーザー モードとカーネル モードであるか。

パフォーマンス モニターを起動することで開始します。 次のカウンターを追加します。

-   **メモリ**--&gt;**Pool Nonpaged Bytes**

-   **メモリ**--&gt;**プール (ページ バイト)**

-   **ページング ファイル**--&gt;**% 使用率**

更新時間を時間の経過と共に、リークのグラフをキャプチャする 600 秒に変更します。 データを後で調査用にファイルに記録する場合があります。

アプリケーションまたはメモリ リークの原因と考えられるテストを開始します。 しばらくの間が自動で実行するには、アプリケーションまたはテストを許可します。この期間中には、対象のコンピュータを使用しません。 リークは、通常は時間がかかるし、検出するために時間がかかる場合があります。 メモリ リークが発生したかどうかを決定する前に、数時間待機します。

パフォーマンス モニター カウンターを監視します。 テストの開始後は、カウンターの値が迅速に変更され、プール値は定常状態に到達するメモリの時間がかかる場合があります。

ユーザー モードのメモリ リークは、常にページング可能なプールに配置され、両方が発生する、**ページ プールのサイズ**カウンターとページファイル**使用状況**徐々 に増加するカウンター。 カーネル モードのメモリ リークが非ページ プールは、通常は少なくなり、原因、 **Pool Nonpaged Bytes**カウンターを増やすには、ページング可能なメモリがも影響を受けることができますが。 場合によってはこれらのカウンターは、アプリケーションがデータをキャッシュために、偽陽性を表示することがあります。

 

 





