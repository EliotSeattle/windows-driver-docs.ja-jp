---
title: バグ チェック コールバック データの読み取り
description: バグ チェック コールバック データの読み取り
ms.assetid: 638074bb-5133-4edc-86c5-33aafa837a0c
keywords:
- バグチェックのコールバックデータ
- バグチェックのコールバックデータ、コールバックデータの表示
- バグチェックのコールバックデータ、セカンダリデータの表示
- セカンダリバグチェックコールバックデータ
- バグチェック、コールバックルーチン
- dbgeng .h ヘッダーファイル、IDebugDataSpaces3
- dbgeng .h ヘッダーファイル、ReadTagged 付き
- dbgeng .h ヘッダーファイル、StartEnumTagged
- dbgeng .h ヘッダーファイル、GetNextTagged
ms.date: 10/25/2018
ms.localizationpriority: medium
ms.openlocfilehash: f9f9bf09a845b859500307671f202c085214a545
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838813"
---
# <a name="reading-bug-check-callback-data"></a>バグ チェック コールバック データの読み取り


多くのドライバーは、*バグチェックコールバックルーチン*を提供します。 Windows がバグチェックを発行すると、システムをシャットダウンする前に、これらのルーチンが呼び出されます。 これらのルーチンは、*コールバックデータ*および*セカンダリコールバックデータ*と呼ばれるメモリの領域を指定して書き込むことができます。

<span id="BugCheckCallback"></span><span id="bugcheckcallback"></span><span id="BUGCHECKCALLBACK"></span>[バグチェックコールバック](https://go.microsoft.com/fwlink/p/?LinkID=254479)  
このルーチンによって書き込まれたデータは、コールバックデータの一部になります。 データは、クラッシュダンプファイルに含まれていません。 

<span id="BugCheckSecondaryDumpDataCallback"></span><span id="bugchecksecondarydumpdatacallback"></span><span id="BUGCHECKSECONDARYDUMPDATACALLBACK"></span>[BugCheckSecondaryDumpDataCallback](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-kbugcheck_reason_callback_routine)  
このルーチンによって書き込まれたデータは、セカンダリコールバックデータの一部になります。 データは、クラッシュダンプファイルに含まれています。

<span id="BugCheckAddPagesCallback"></span><span id="bugcheckaddpagescallback"></span><span id="BUGCHECKADDPAGESCALLBACK"></span>[バグチェッカーのコールバック](https://go.microsoft.com/fwlink/p/?LinkID=254480)  
このルーチンによって指定されたページは、コールバックデータの一部になります。 これらのページのデータは、クラッシュダンプファイルに含まれています。

デバッガーで使用できるコールバックとセカンダリコールバックデータの量は、次のいくつかの要因によって異なります。

-   クラッシュしたシステムのライブデバッグを実行している場合は、[バグチェックコールバック](https://go.microsoft.com/fwlink/p/?LinkID=254479)によって既に記述されているか、またはバグチェックコール[バック](https://go.microsoft.com/fwlink/p/?LinkID=254480)によって指定されたコールバックデータを使用できます。 セカンダリコールバックデータは、固定メモリの場所に格納されていないため、使用できません。

-   完全なメモリダンプまたはカーネルメモリダンプをデバッグしている場合は、 [BugCheckSecondaryDumpDataCallback](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-kbugcheck_reason_callback_routine)によって書き込まれた、[バグチェッカーのコールバック](https://go.microsoft.com/fwlink/p/?LinkID=254480)とセカンダリコールバックのデータによって指定されたコールバックデータが使用できるようになります。 [バグチェックコールバック](https://go.microsoft.com/fwlink/p/?LinkID=254479)によって書き込まれたコールバックデータは使用できません。 

-   小さいメモリダンプをデバッグする場合、コールバックデータは使用できません。 セカンダリコールバックデータが使用できるようになります。

これらのさまざまなダンプファイルサイズの詳細については、「[カーネルモードのダンプファイルの種類](varieties-of-kernel-mode-dump-files.md)」を参照してください。


## <span id="ddk_reading_bug_check_callback_data_dbg"></span><span id="DDK_READING_BUG_CHECK_CALLBACK_DATA_DBG"></span>


### <a name="span-iddisplaying-callback-dataspanspan-iddisplaying-callback-dataspandisplaying-callback-data"></a><span id="displaying-callback-data"></span><span id="DISPLAYING-CALLBACK-DATA"></span>コールバックデータの表示

バグチェックコールバックデータを表示するには、 [ **!** ](-bugdump.md)を使用します。

パラメーターを指定しない場合、 [ **!** ](-bugdump.md)を使用すると、すべてのコールバックのデータが表示されます。

1つの特定のコールバックルーチンのデータを表示するには、 [ **!** ](-bugdump.md)の KeRegisterBugCheckCallback*コンポーネント*を使用します。ここで、 *component*は、そのルーチンが登録されたときにに渡されたパラメーターと同じです。

### <a name="span-iddisplaying-secondary-callback-dataspanspan-iddisplaying-secondary-callback-dataspandisplaying-secondary-callback-data"></a><span id="displaying-secondary-callback-data"></span><span id="DISPLAYING-SECONDARY-CALLBACK-DATA"></span>セカンダリコールバックデータの表示

セカンダリコールバックデータを表示するには、2つの方法があります。 **Enumtag**コマンドを使用することも、独自のデバッガー拡張機能を記述することもできます。

セカンダリコールバックデータの各ブロックは、GUID タグによって識別されます。 このタグは、の**Guid**フィールド **(KBUGCHECK\_セカンダリ\_DUMP\_DATA)** によって指定され、 [BugCheckSecondaryDumpDataCallback](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-kbugcheck_reason_callback_routine)に渡されます。

[**Enumtag (2 番目のコールバックデータの列挙)** ](-enumtag--enumerate-secondary-callback-data-.md)コマンドは、正確なインストルメントではありません。 すべてのセカンダリデータブロックが表示され、タグが表示された後、16進形式と ASCII 形式でデータが表示されます。 通常は、セカンダリデータブロックに実際に使用されているタグを特定するだけで役立ちます。

このデータをより実用的な方法で使用するには、独自のデバッガー拡張機能を作成することをお勧めします。 この拡張機能は、dbgeng .h ヘッダーファイル内のメソッドを呼び出す必要があります。 詳細については、「[新しいデバッガー拡張機能の作成](writing-new-debugger-extensions.md)」を参照してください。

セカンダリデータブロックの GUID タグがわかっている場合は、拡張機能で**IDebugDataSpaces3:: readtagged**メソッドを使用してデータにアクセスする必要があります。 プロトタイプは次のとおりです。

```cpp
STDMETHOD(ReadTagged)(
    THIS_
    IN LPGUID Tag,
    IN ULONG Offset,
    OUT OPTIONAL PVOID Buffer,
    IN ULONG BufferSize,
    OUT OPTIONAL PULONG TotalSize
    ) PURE; 
```

このメソッドの使用例を次に示します。

```cpp
UCHAR RawData[MY_DATA_SIZE];
GUID MyGuid = .... ;

Success = DataSpaces->ReadTagged(  &MyGuid,  0,  RawData,
                                   sizeof(RawData),  NULL); 
```

小さすぎる*BufferSize*を指定すると、 **readtagged**は成功しますが、*バッファー*には要求されたバイト数だけが書き込まれます。 大きすぎる*BufferSize*を指定すると、 **readtagged**は成功しますが、*バッファー*には実際のブロックサイズのみが書き込まれます。 *TotalSize*のポインターを指定すると、 **readtagged**はそれを使用して実際のブロックのサイズを返します。 ブロックにアクセスできない場合、 **Readtagged**はエラー状態コードを返します。

2つのブロックが同じ GUID タグを持つ場合、最初に一致するブロックが返され、2つ目のブロックはアクセスできなくなります。

ブロックの GUID タグがわからない場合は、 **IDebugDataSpaces3:: startenumtagged**、 **IDebugDataSpaces3:: GetNextTagged**、 **IDebugDataSpaces3:: endenumtagged**の各メソッドを使用して、タグ付けされたブロックを列挙できます。 プロトタイプは次のとおりです。

```cpp
STDMETHOD(StartEnumTagged)(
    THIS_
    OUT PULONG64 Handle
    ) PURE;

STDMETHOD(GetNextTagged)(
    THIS_
    IN ULONG64 Handle,
    OUT LPGUID Tag,
    OUT PULONG Size
    ) PURE;

STDMETHOD(EndEnumTagged)(
    THIS_
    IN ULONG64 Handle
    ) PURE; 
```

### <a name="span-iddebugging-callback-routinesspanspan-iddebugging-callback-routinesspandebugging-callback-routines"></a><span id="debugging-callback-routines"></span><span id="DEBUGGING-CALLBACK-ROUTINES"></span>デバッグ (コールバックルーチンを)

コールバックルーチン自体をデバッグすることもできます。 コールバックルーチン内のブレークポイントは、他のブレークポイントと同じように動作します。

コールバックルーチンによって2番目のバグチェックが発生した場合、この新しいバグチェックは最初に処理されます。 ただし、Windows は Stop プロセスの特定の部分を繰り返しません。たとえば、2番目のクラッシュダンプファイルは書き込まれません。 ブルースクリーンに表示されるストップコードは、2番目のバグチェックコードになります。 カーネルデバッガーがアタッチされている場合は、通常、両方のバグチェックに関するメッセージが表示されます。

 

 





