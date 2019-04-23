---
title: バグ チェック 0x165 CLUSTER_CSV_STATUS_IO_TIMEOUT_LIVEDUMP
description: CLUSTER_CSV_STATUS_IO_TIMEOUT_LIVEDUMP のバグ チェックでは、0x00000165 の値を持ちます。 これは、SMB クライアントでタイムアウト状況が発生していることを示します。
keywords:
- バグ チェック 0x165 CLUSTER_CSV_STATUS_IO_TIMEOUT_LIVEDUMP
- CLUSTER_CSV_STATUS_IO_TIMEOUT_LIVEDUMP
ms.date: 01/03/2019
topic_type:
- apiref
api_name:
- CLUSTER_CSV_STATUS_IO_TIMEOUT_LIVEDUMP
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ea0567ae1faa6321fdec5f3e72e5d7771a61223f
ms.sourcegitcommit: fb8b1d2e18dd727e8a479b04c9e6051e7e9fa484
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/18/2019
ms.locfileid: "59239795"
---
# <a name="bug-check-0x165-clustercsvstatusiotimeoutlivedump"></a>バグ チェック 0x165:クラスター\_CSV\_状態\_IO\_タイムアウト\_LIVEDUMP

クラスター\_CSV\_状態\_IO\_タイムアウト\_LIVEDUMP バグ チェックが 0x00000165 の値を持ちます。 これは、非調整ノード上の SMB クライアントがという苦情調整のノードで IO が時間がかかりすぎると、STATUS_IO_TIMEOUT ですべての IOs が失敗したことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。


## <a name="clustercsvstatusiotimeoutlivedump-parameters"></a>クラスター\_CSV\_状態\_IO\_タイムアウト\_LIVEDUMP パラメーター

|パラメーター|説明|
|--- |--- |
|1|省略可能なクラスター サービスの PID です。|
|2|STATUS_IO_TIMEOUT を監視するノードのクラスター ノードの Id。|
|3|予約済み。|
|4|予約済み。|

## <a name="cause"></a>原因
-----

非調整ノード上の SMB クライアントは、調整のノードで IO が時間がかかりすぎると、STATUS_IO_TIMEOUT ですべての IOs が失敗したという苦情います。

追加情報は、ダンプのセカンダリのデータ ストリームで使用できます。

(このコードは、実際のバグチェックには使用されません。 クラスターの共有ボリュームのテレメトリなどを含むライブ ダンプの識別に使用されます)。


## <a name="resolution"></a>解決方法
----------
 

## <a name="see-also"></a>関連項目
----------

[使用してライブ ダンプ (ブログ) のトラブルシューティングがハングします。](https://blogs.msdn.microsoft.com/clustering/2016/03/02/troubleshooting-hangs-using-live-dump/)

[バグチェック コード リファレンス](bug-check-code-reference2.md)



