---
title: バグ チェック 0x192 KERNEL_AUTO_BOOST_LOCK_ACQUISITION_WITH_RAISED_IRQL
description: KERNEL_AUTO_BOOST_LOCK_ACQUISITION_WITH_RAISED_IRQL のバグ チェックでは、DISPATCH_LEVEL 以上を実行中に AutoBoost によって追跡されるロックが取得されたことを示します。
ms.assetid: D88EF2CC-26DC-44D8-80CB-18D058C6A413
keywords:
- バグ チェック 0x192 KERNEL_AUTO_BOOST_LOCK_ACQUISITION_WITH_RAISED_IRQL
- KERNEL_AUTO_BOOST_LOCK_ACQUISITION_WITH_RAISED_IRQL
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- KERNEL_AUTO_BOOST_LOCK_ACQUISITION_WITH_RAISED_IRQL
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 85e492a9344cc7427d9eba3ee2b459b80807a2ce
ms.sourcegitcommit: 55d7f63bb9e7668d65aa0999e65d18fabd44758e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2019
ms.locfileid: "59238749"
---
# <a name="bug-check-0x192-kernelautoboostlockacquisitionwithraisedirql"></a>バグ チェック 0x192:カーネル\_自動\_BOOST\_ロック\_買収\_WITH\_発生\_IRQL


カーネル\_自動\_BOOST\_ロック\_買収\_WITH\_発生\_IRQL のバグ チェックが 0x00000192 の値を持ちます。 これは、ディスパッチで実行中に AutoBoost によって追跡されるロックが取得されたことを示します\_レベルまたはそれ以降。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。


## <a name="kernelautoboostlockacquisitionwithraisedirql-parameters"></a>カーネル\_自動\_BOOST\_ロック\_買収\_WITH\_発生\_IRQL パラメーター


| パラメーター | 説明                             |
|-----------|-----------------------------------------|
| 1         | スレッドのアドレス               |
| 2         | ロックのアドレス                        |
| 3         | ロックが取得された IRQL |
| 4         | 予約済み                                |

 

<a name="cause"></a>原因
-----

APC の上のロックを呼び出し元をブロックすることはできません\_レベルため、デッドロックの原因となる割り込まれたスレッドによって排他的ロックが保持されることもできます。

 

 



