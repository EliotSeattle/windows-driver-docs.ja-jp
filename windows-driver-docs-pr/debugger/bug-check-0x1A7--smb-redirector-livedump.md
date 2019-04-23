---
title: バグ チェック 0x1A7 SMB_REDIRECTOR_LIVEDUMP
description: SMB_REDIRECTOR_LIVEDUMP のバグ チェックでは、0x000001A7 の値を持ちます。 SMB リダイレクターが問題を検出し、デバッグ情報を収集するカーネル ダンプをキャプチャしたことを示します。
keywords:
- バグ チェック 0x1A7 SMB_REDIRECTOR_LIVEDUMP
- SMB_REDIRECTOR_LIVEDUMP
ms.date: 01/10/2019
topic_type:
- apiref
api_name:
- SMB_REDIRECTOR_LIVEDUMP
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 9a8cff66082327b239de1d1159b405dfc4281deb
ms.sourcegitcommit: fb8b1d2e18dd727e8a479b04c9e6051e7e9fa484
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/18/2019
ms.locfileid: "59239401"
---
# <a name="bug-check-0x1a7-smbredirectorlivedump"></a>バグ チェック 0x1A7:SMB\_リダイレクター\_LIVEDUMP

SMB\_リダイレクター\_LIVEDUMP バグ チェックが 0x000001A7 の値を持ちます。 SMB リダイレクターが問題を検出し、デバッグ情報を収集するカーネル ダンプをキャプチャしたことを示します。


> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。

 

## <a name="smbredirectorlivedump-parameters"></a>SMB\_リダイレクター\_LIVEDUMP パラメーター

|パラメーター|説明|
|--- |--- |
|1| 理由コード - 次の値を参照してください。|
|2| 次の値を参照してください。|
|3| 予約済み。|
|4| 予約済み。|

SMB リダイレクターは、問題が検出されましたし、デバッグ情報を収集するカーネル ダンプをキャプチャします。

**理由コード**

```text
0x1 : An I/O failed to complete in a reasonable amount of time.
    2 - Pointer to the connection object.
    3 - Reserved.
    4 - Reserved.
```

## <a name="cause"></a>原因
-----

SMB リダイレクターは、問題が検出されましたし、デバッグ情報を収集するカーネル ダンプをキャプチャします。

次のレジストリ値が設定されている場合にのみ、このバグチェック コードのライブのダンプが生成されます。

```
HKLM\System\CurrentControlSet\Services\Lanmanworkstation\Parameters [DWORD] LiveDumpFilter = 1
```

このレジストリ キーが設定されている場合、IO で RDR のタイムアウトを livedump が発生します。

(このコードは、実際のバグチェックには使用されません。 ライブ ダンプの識別に使用されます)。

## <a name="see-also"></a>関連項目
----------

[バグチェック コード リファレンス](bug-check-code-reference2.md)