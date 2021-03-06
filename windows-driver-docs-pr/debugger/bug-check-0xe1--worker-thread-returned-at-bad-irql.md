---
title: バグ チェック 0xE1 WORKER_THREAD_RETURNED_AT_BAD_IRQL
description: WORKER_THREAD_RETURNED_AT_BAD_IRQL のバグ チェックでは、0x000000E1 の値を持ちます。 これは、ワーカー スレッドが完了し、IRQL DISPATCH_LEVEL と共に返されることを示します。
ms.assetid: c02b98e9-e3a4-473a-bd9f-3130b7e58c1d
keywords:
- バグ チェック 0xE1 WORKER_THREAD_RETURNED_AT_BAD_IRQL
- WORKER_THREAD_RETURNED_AT_BAD_IRQL
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- WORKER_THREAD_RETURNED_AT_BAD_IRQL
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 4387f2f6b83f8af8c97330e0860a0e1b6a3b067b
ms.sourcegitcommit: d03b44343cd32b3653d0471afcdd3d35cb800c0d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2019
ms.locfileid: "67518822"
---
# <a name="bug-check-0xe1-workerthreadreturnedatbadirql"></a>バグ チェック 0xE1:ワーカー\_スレッド\_から返された\_で\_不良\_IRQL


ワーカー\_スレッド\_から返された\_で\_不良\_IRQL のバグ チェックが 0x000000E1 の値を持ちます。 これは、ワーカー スレッドが完了し、IRQL と共に返されることを示します&gt;= ディスパッチ\_レベル。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://www.windows.com/stopcode)します。


## <a name="workerthreadreturnedatbadirql-parameters"></a>ワーカー\_スレッド\_から返された\_で\_不良\_IRQL パラメーター


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">パラメーター</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>1</p></td>
<td align="left"><p>ワーカーのルーチンのアドレス</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>IRQL でワーカー スレッドが返される</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>作業項目のパラメーター</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>作業項目のアドレス</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

ワーカー スレッドが完了し、IRQL と共に返される&gt;= ディスパッチ\_レベル。

<a name="resolution"></a>解決方法
----------

エラーが発生したドライバーを検索するには、使用、 [ **ln (最も近いシンボルの一覧)** ](ln--list-nearest-symbols-.md)デバッガー コマンド。

```dbgcmd
kd> ln address
```

場所*アドレス*パラメーター 1 で指定されたワーカーの日常的なアドレスです。

 

 




