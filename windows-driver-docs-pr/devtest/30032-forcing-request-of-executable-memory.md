---
title: C30032
description: C30032 を呼び出す関数の割り当てと POOL_NX_OPTOUT ディレクティブを使用して実行可能なメモリの要求を強制的にメモリを警告します。
ms.assetid: 7C6F9ACE-DD02-45A7-A601-C5C7A5C89256
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C30032
ms.openlocfilehash: ae5a20bc4344e7d6c45d9cbd437cd03de83d5cac
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371696"
---
# <a name="c30032"></a>C30032


C30032 を警告します。メモリ割り当て関数と、強制的に実行可能なメモリを使用しての要求を呼び出し、[プール\_NX\_OPTOUT](https://docs.microsoft.com/windows-hardware/drivers/kernel/selective-opt-out-pool-nx-optout)ディレクティブ

禁止\_MEM\_割り当て\_FORCE\_UNSAFE

プリプロセッサ ディレクティブ[プール\_NX\_OPTOUT](https://docs.microsoft.com/windows-hardware/drivers/kernel/selective-opt-out-pool-nx-optout)非セーフな型の自動昇格を防ぎます (**MM\_ページ\_優先度**と**プール\_型**) に安全な型 (たとえば、NonPagedPoolNx に NonPagedPool)。 プールの使用\_NX\_OPTOUT ソース内は仕様による可能性があります。 かどうかは、これは仕様、および実行可能なメモリが必要で警告を抑制することができます[警告メッセージを抑制するプラグマ Prefast](https://docs.microsoft.com/previous-versions/windows/embedded/gg155764(v=winembedded.70))します。 追加のメモリの保護にオプトインしている Windows 10 システムでは、この種類の割り当てが許可されていません。

## <a name="span-idexamplespanspan-idexamplespanspan-idexamplespanexample"></a><span id="Example"></span><span id="example"></span><span id="EXAMPLE"></span>例


次のコードでは、この警告が生成されます。

ソース ファイル。

```
C_DEFINES=$(C_DEFINES) –DUNICODE -DPOOL_NX_OPTOUT=1
```

コード ファイル。

```
pPtr = MmGetSystemAddressForMdlSafe( pMdl, NormalPagePriority);
```

次のコードは、この警告を回避できます。

ソース ファイルで次のように追加します。

```
C_DEFINES=$(C_DEFINES) -DUNICODE -DPOOL_NX_OPTIN_AUTO=1
```

コード ファイル。

```
pPtr = MmGetSystemAddressForMdlSafe( pMdl, NormalPagePriority);
```

 

 





