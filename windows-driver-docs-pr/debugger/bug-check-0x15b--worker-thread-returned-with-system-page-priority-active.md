---
title: バグ チェック 0x15B WORKER_THREAD_RETURNED_WITH_SYSTEM_PAGE_PRIORITY_ACTIVE
description: WORKER_THREAD_RETURNED_WITH_SYSTEM_PAGE_PRIORITY_ACTIVE のバグ チェックでは、ワーカー スレッドのシステム ページの優先度のリークを示す 0x0000015B の値を持ちます。
ms.assetid: F618AA35-54BC-4923-99C8-311DB1D20C71
keywords:
- バグ チェック 0x15B WORKER_THREAD_RETURNED_WITH_SYSTEM_PAGE_PRIORITY_ACTIVE
- WORKER_THREAD_RETURNED_WITH_SYSTEM_PAGE_PRIORITY_ACTIVE
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- WORKER_THREAD_RETURNED_WITH_SYSTEM_PAGE_PRIORITY_ACTIVE
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: e33613c3f97e82f041f0c4698129288fdfb241fa
ms.sourcegitcommit: d03b44343cd32b3653d0471afcdd3d35cb800c0d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2019
ms.locfileid: "67520021"
---
# <a name="bug-check-0x15b-workerthreadreturnedwithsystempagepriorityactive"></a>バグ チェック 0x15B:ワーカー\_スレッド\_から返された\_WITH\_システム\_ページ\_優先度\_ACTIVE


ワーカー\_スレッド\_から返された\_WITH\_システム\_ページ\_優先度\_アクティブなバグ チェックが 0x0000015B の値を持ちます。 これは、ワーカーが呼び出されたルーチンによってワーカー スレッドのシステム ページの優先順位がリークされたことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://www.windows.com/stopcode)します。


## <a name="workerthreadreturnedwithsystempagepriorityactive-parameters"></a>ワーカー\_スレッド\_から返された\_WITH\_システム\_ページ\_優先度\_ACTIVE パラメーター


| パラメーター | 説明                                                                    |
|-----------|--------------------------------------------------------------------------------|
| 1         | ワーカー ルーチン (問題のあるドライバーを検索するには、このアドレスでは ln) のアドレス |
| 2         | 現在のシステム ページ優先順位の値                                             |
| 3         | 作業項目のパラメーター                                                             |
| 4         | 作業項目のアドレス                                                               |

 

 

 




