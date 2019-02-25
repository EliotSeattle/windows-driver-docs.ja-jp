---
title: バグ チェック 0x102 DPC_WATCHDOG_TIMEOUT
description: DPC_WATCHDOG_TIMEOUT のバグ チェックでは、0x00000102 の値を持ちます。 これは、割り当てられた時間間隔内で実行されませんでした、DPC ウォッチドッグ ルーチンことを示します。
ms.assetid: 1BEC2701-3127-4FB9-AD0F-DD54A9F2C2C3
keywords:
- バグ チェック 0x102 DPC_WATCHDOG_TIMEOUT
- DPC_WATCHDOG_TIMEOUT
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- DPC_WATCHDOG_TIMEOUT
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 54b544c7a9a8d53175daf56e4e60386f976a9642
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550697"
---
# <a name="bug-check-0x102-dpcwatchdogtimeout"></a>バグ チェック 0x102 の。DPC\_ウォッチドッグ\_タイムアウト


DPC\_ウォッチドッグ\_バグ チェックのタイムアウトが 0x00000102 の値を持ちます。 これは、割り当てられた時間間隔内で実行されませんでした、DPC ウォッチドッグ ルーチンことを示します。

**重要な**プログラマ向けのトピックです。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。

## <a name="dpcwatchdogtimeout-parameters"></a>DPC\_ウォッチドッグ\_タイムアウト パラメーター


| パラメーター | 説明                                            |
|-----------|--------------------------------------------------------|
| 1         | 標準のクロック ティックで DPC ウォッチドッグ タイムアウト間隔。 |
| 2         | ハングしたプロセッサの PRCB アドレス。                |
| 3         | 予約済み                                               |
| 4         | 予約済み                                               |

 

<a name="cause"></a>原因
-----

通常、このバグ チェックは、クロック レベルとディスパッチのレベル以上である IRQL で ISR がハングしているかまたは指定されたプロセッサの DPC ルーチンがハングしていることを意味します。

たとえば、StorPort ミニポート ドライバーの StorPort.sys 処理、ディスパッチに実行されるルーチンでの I/O 完了\_レベルとを逐次的に完了したすべての Irp の I/O 完了ルーチンの呼び出し。 I/O 完了ルーチン単独または組み合わせてを受け取らない場合は時間がかかりすぎる、キーボードやマウスが応答を停止します。 StorPort ルーチンが完了までに時間が過剰なを実行する Windows DPC ウォッチドッグ タイマーのルーチンを決定することもできます。

<a name="resolution"></a>解決方法
----------

記憶域スタックでのカーネル ドライバーでは、ドライバーの I/O 完了ルーチンの効率的なコーディングによって問題の可能性を減らすことができます。 まだ十分な時間で完了ルーチンで必要なすべての処理を実行できない場合は、ルーチンできます I/O 作業の作業の要素を作成する作業キューに要素をキューや状態を返す\_詳細\_処理\_必ず指定します。ドライバーのワーカー スレッドを作業要素を検索する必要がありますは、作業を実行し、IoCallerDriver IRP IRP のさらに I/O 処理を保証するための操作を行いますは。

 

 



