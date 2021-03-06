---
title: バグ チェック 0x166 CLUSTER_RESOURCE_CALL_TIMEOUT_LIVEDUMP
description: CLUSTER_RESOURCE_CALL_TIMEOUT_LIVEDUMP のバグ チェックでは、0x00000166 の値を持ちます。 これは、クラスター リソースの呼び出しが構成されたタイムアウトより長くかかったことを示します。
keywords:
- バグ チェック 0x166 CLUSTER_RESOURCE_CALL_TIMEOUT_LIVEDUMP
- CLUSTER_RESOURCE_CALL_TIMEOUT_LIVEDUMP
ms.date: 12/27/2018
topic_type:
- apiref
api_name:
- CLUSTER_RESOURCE_CALL_TIMEOUT_LIVEDUMP
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 1985bfffcbc58acc2247a6713f257ffa8e69cbc0
ms.sourcegitcommit: d03b44343cd32b3653d0471afcdd3d35cb800c0d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2019
ms.locfileid: "67519965"
---
# <a name="bug-check-0x166-clusterresourcecalltimeoutlivedump"></a>バグ チェック 0x166:クラスター\_リソース\_呼び出す\_タイムアウト\_LIVEDUMP

クラスター\_リソース\_呼び出す\_タイムアウト\_LIVEDUMP バグ チェックが 0x00000166 の値を持ちます。 これは、クラスター リソースの呼び出しが構成されたタイムアウトより長くかかったことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://www.windows.com/stopcode)します。



## <a name="clusterresourcecalltimeoutlivedump-parameters"></a>クラスター\_リソース\_呼び出す\_タイムアウト\_LIVEDUMP パラメーター

|パラメーター|説明|
|--- |--- |
|1|リソースのホスト モニターの PID です。|
|2|リソース呼び出しを処理するスレッド TID します。|
|3|リソースの呼び出しの種類 - 以下に示します。|
|4|サブコード。 3 番目のパラメーターが 8 し、このパラメーターの場合に、クラスター リソースの制御コードが含まれています。 3 番目のパラメーターが 9 し、このパラメーターの場合は、クラスター リソースの種類の制御コードが含まれています。|

**リソースの呼び出しの種類**

1 つのオープン

2 を閉じる

オンライン 3

オフライン 4

5 を終了します。

6 を判別します。

7 のリリース

8 リソース コントロール

9 のリソースの種類のコントロール

10 がアライブが探す

11 が有効

12 のエラー通知

13 のシャット ダウン プロセス

14 のキャンセル


## <a name="cause"></a>原因
-----

クラスター リソースの呼び出しは、構成されたタイムアウトよりも長くかかります。 システムでは、遅延の分析のためのライブのダンプを生成します。

(このコード決してできますの実際のバグチェック。)

## <a name="resolution"></a>解決方法
----------
 

## <a name="see-also"></a>関連項目
----------

[使用してライブ ダンプ (ブログ) のトラブルシューティングがハングします。](https://techcommunity.microsoft.com/t5/Failover-Clustering/bg-p/FailoverClustering)

[バグチェック コード リファレンス](bug-check-code-reference2.md)




