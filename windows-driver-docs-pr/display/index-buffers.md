---
title: インデックス バッファー
description: インデックス バッファー
ms.assetid: 5bf7dc12-d988-4194-a81f-52c9c5356610
keywords:
- DirectX 8.0 リリース ノートには、Windows 2000 の WDK 表示インデックス バッファー
- インデックス バッファー WDK Directx 8.0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 710a4b8edba32a42db2ee92997f64a1435c58993
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371360"
---
# <a name="index-buffers"></a>インデックス バッファー


## <span id="ddk_index_buffers_gg"></span><span id="DDK_INDEX_BUFFERS_GG"></span>


DirectX 8.0 では、インデックス バッファーの概念を紹介します。 これらのバッファーを頂点バッファーとよく似ていますが、頂点データ自体ではなく、頂点データに単純な 16 ビットまたは 32 ビットのインデックスを格納します。 インデックス バッファーは、最適なダウンロードとインデックスのデータをキャッシュします。 たとえば、頂点バッファーのすべての特典を拡張します。

インデックス バッファーは、作成、ロック、ロック解除、および頂点バッファーに使用されるものと同じドライバー エントリ ポイントが破壊されます。 ドライバーは、これらのバッファーの種類を区別できるビット DDSCAPS2 が新しいセキュリティ機能を使用して\_INDEXBUFFER します。 インデックス バッファーの場合、このフラグを設定、 **ddsCapsEx.dwCaps2** 、画面のフィールド[ **DD\_画面\_詳細**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_surface_more)構造体。 頂点バッファーを明確になります。

その他の多数のサーフェス型とは異なりは、ドライバーは DDSCAPS2 機能を設定する必要ありません\_ドライバーを受信する INDEXBUFFER ランタイムにその機能をレポートするときにインデックス バッファーの作成、破棄、およびロックを呼び出します。 頂点バッファーをサポートする DirectX 8.0 ドライバーは、インデックス バッファーをサポートするもと見なされます。 基になるハードウェアにインデックス バッファーを直接サポートがあるない場合、ドライバーはサーフェイスでのシステム メモリを割り当てることによってインデックス バッファーの作成を処理する必要があります。

 

 





