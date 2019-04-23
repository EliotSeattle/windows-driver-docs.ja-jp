---
title: Microsoft パブリック シンボル サーバー
description: Microsoft シンボル サーバーは、Windows デバッガーのシンボルを公開します。
ms.assetid: b0d38104-c386-4d20-8d9c-7701347c1643
keywords:
- SymSrv、パブリックの Microsoft シンボル
- シンボル サーバー、Microsoft のパブリック シンボル
- パブリック シンボル ストア
- Microsoft シンボル ストア
ms.date: 04/26/2018
ms.localizationpriority: medium
ms.openlocfilehash: f53f44ee1628fddd1bdd00c05b5ca05642af32a0
ms.sourcegitcommit: fb8b1d2e18dd727e8a479b04c9e6051e7e9fa484
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/18/2019
ms.locfileid: "59362915"
---
# <a name="microsoft-public-symbol-server"></a>Microsoft パブリック シンボル サーバー


**サーバーの状態:** 既知の問題はありません: white_check_mark: <br> Microsoft パブリック シンボル サーバーが完全に動作します。 <br>
既知の問題を報告してください[ windbgfb@microsoft.com](mailto:windbgfb@microsoft.com)します。 

---

Microsoft シンボル サーバーは、Windows デバッガーのシンボルを公開します。

次のようにシンボル パスで、パブリック シンボル サーバーを直接参照できます。

```console
set _NT_SYMBOL_PATH=srv*DownstreamStore*https://msdl.microsoft.com/download/symbols
```

*DownstreamStore*ローカル コンピューターまたはシンボルをキャッシュに使用されるネットワーク上のディレクトリを指定する必要があります。 このダウン ストリームのストアには、デバッガーへのアクセスが; シンボルが保持されます。アクセスしないシンボルの大半は、Microsoft のシンボル ストアに残ります。 これは、ダウン ストリームのストアを比較的小さく維持され、作業にすぐに、シンボル サーバーは、各ファイルを 1 回だけダウンロードします。

この長いシンボル パスを入力しなくて済むようにするには、使用、 [ **.symfix (シンボル ストア パスの設定)** ](-symfix--set-symbol-store-path-.md)コマンド。 次のコマンドは、既存のシンボル パスに、パブリック シンボル ストアを追加します。

```dbgcmd
.symfix+ C:\MySymbols
```

ローカル シンボル キャッシュの場所を省略すると、デバッガーのインストール ディレクトリの sym サブディレクトリが使用されます。

使用して、 [ **.sympath (シンボル ストア パスの設定)** ](-symfix--set-symbol-store-path-.md)完全なシンボル パスを表示するコマンド。 この例では、symfix を使用して、ローカル シンボル キャッシュを作成し、http の Microsoft シンボル サーバーを使用する方法を示します。

```dbgcmd
0: kd> .symfix c:\MyCache
0: kd> .sympath
Symbol search path is: srv*
Expanded Symbol search path is: cache*c:\MyCache;SRV*https://msdl.microsoft.com/download/symbols
```

シンボルの使用方法の詳細については、次を参照してください。、 [Windows デバッガーのシンボル パス](https://docs.microsoft.com/windows-hardware/drivers/debugger/symbol-path)します。

**シンボル ファイルの圧縮**

Microsoft シンボル サーバーは、シンボル ファイルの圧縮バージョンを提供します。 ファイルが圧縮されることを示すために、ファイル名の拡張子の末尾にアンダー スコアがあります。 たとえば、ntdll.dll の PDB は ntdll.pd として利用可能な\_します。 SymProxy 圧縮ファイルをダウンロードするときは、ローカル ファイル システムで圧縮解除されたファイルを格納します。 DontUncompress のレジストリ キーは、SymProxy でこの動作を無効に設定できます。

デバッガーのトピックを参照して[SymStore](symstore.md) SymStore.exe/compress を使用して、独自のシンボルをシンボル サーバーで圧縮を格納する方法について。

 

 




