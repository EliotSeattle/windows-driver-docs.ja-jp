---
title: バグ チェック 0x151 UNSUPPORTED_INSTRUCTION_MODE
description: UNSUPPORTED_INSTRUCTION_MODE のバグ チェックでは、0x00000151 の値を持ちます。
ms.assetid: 2FB679D8-9FA3-423D-BCA1-5EDE88C78FBF
keywords:
- バグ チェック 0x151 UNSUPPORTED_INSTRUCTION_MODE
- UNSUPPORTED_INSTRUCTION_MODE
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- UNSUPPORTED_INSTRUCTION_MODE
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ef8bba4b8b865274e08d6bdff53ad972503ccfe7
ms.sourcegitcommit: d03b44343cd32b3653d0471afcdd3d35cb800c0d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2019
ms.locfileid: "67520061"
---
# <a name="bug-check-0x151-unsupportedinstructionmode"></a>バグ チェック 0x151:サポートされていない\_命令\_モード


サポートされていない\_命令\_モードのバグ チェックが 0x00000151 の値を持ちます。 これは、サポートされていないプロセッサ命令モード (たとえば、実行されているクラシック ARM 命令 ThumbV2 命令ではなく) を使用してコードを実行しようとすることを示します。 これは許可されていません。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://www.windows.com/stopcode)します。


## <a name="unsupportedinstructionmode-parameters"></a>サポートされていない\_命令\_モード パラメーター


| パラメーター | 説明                                    |
|-----------|------------------------------------------------|
| 1         | 問題が検出された場合に、プログラム カウンターです。 |
| 2         | トラップ フレーム                                     |
| 3         | 予約済み                                       |
| 4         | 予約済み                                       |

 

 

 




