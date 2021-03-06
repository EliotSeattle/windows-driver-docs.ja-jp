---
title: デバッグ メッセージの読み取りとフィルター処理
description: デバッグ メッセージの読み取りとフィルター処理
ms.assetid: 2ad320f6-596d-4b4c-bfad-d570c856bcc7
keywords:
- コードのデバッグ、メッセージの読み取り
- コードのデバッグ、メッセージのフィルター処理
- デバッグメッセージの読み取り
- デバッグメッセージのフィルター処理 (WDK)
- ルーチン WDK デバッグ、メッセージフィルター処理
- フィルターマスク WDK デバッグ
- コンポーネント名 WDK デバッグ
- 重要度ビットフィールド WDK デバッグ
- レベル WDK デバッグ
- Level パラメーター
- デバッグメッセージの表示
- デバッグメッセージの優先順位 WDK
- DbgPrint バッファー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: edc663586bbf145207c60dec2eac431afb1c9ca4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839330"
---
# <a name="reading-and-filtering-debugging-messages"></a>デバッグ メッセージの読み取りとフィルター処理


## <span id="ddk_reading_and_filtering_debugging_messages_tools"></span><span id="DDK_READING_AND_FILTERING_DEBUGGING_MESSAGES_TOOLS"></span>


[**Dbgprintex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-dbgprintex)、 [**vdbgprintex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-vdbgprintex)、 [**vdbgprintexwithprefix**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-vdbgprintexwithprefix)、および[**KdPrintEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kdprintex)ルーチンは、指定された条件下でカーネルデバッガーにメッセージを送信します。 この手順では、優先度の低いメッセージを除外できます。

**注**   Microsoft windows Server 2003 以前のバージョンの windows では、 [**Dbgprint**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-dbgprint)ルーチンと[**KdPrint**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kdprint)ルーチンは、メッセージを無条件にカーネルデバッガーに送信します。 Windows Vista 以降のバージョンの Windows では、これらのルーチンは、 **Dbgprintex**や**KdPrintEx**などの条件に応じてメッセージを送信します。 どちらのバージョンの Windows を使用している場合でも、 **Dbgprintex**、 **vdbgprintex**、 **vdbgprintexwithprefix**、および**KdPrintEx**を使用する必要があります。これらのルーチンを使用すると、メッセージが送信される条件を制御できます。

 

**デバッグメッセージをフィルター処理するには**

1.  デバッガーに送信するメッセージごとに、ドライバーのコードで**Dbgprintex**、 **vdbgprintex**、 **vdbgprintexwithprefix**、または**KdPrintEx**を使用します。 適切なコンポーネント名を*ComponentId*パラメーターに渡し、このメッセージの重大度または性質を反映する*レベル*パラメーターに値を渡します。 メッセージ自体は、 **printf**と同じ構文を使用して、 *Format*パラメーターと*arguments*パラメーターに渡されます。

2.  適切な*コンポーネントフィルターマスク*の値を設定します。 各コンポーネントには異なるマスクがあります。 マスクの値は、そのコンポーネントのメッセージのうち、どれが表示されるかを示します。 レジストリエディターを使用して、またはメモリ内でカーネルデバッガーを使用して、コンポーネントフィルターマスクを設定できます。

3.  コンピューターにカーネルデバッガーをアタッチします。 ドライバーが**Dbgprintex**、 **vdbgprintex**、 **vdbgprintexwithprefix**、または**KdPrintEx**にメッセージを渡すたびに、 *ComponentId*と*Level*に渡される値は、の値と比較されます。対応するコンポーネントフィルターマスク。 これらの値が特定の条件を満たしている場合、メッセージはカーネルデバッガーに送信されて表示されます。 それ以外の場合、メッセージは送信されません。

詳細については、次のセクションを参照してください。

このページでは、 **Dbgprintex**へのすべての参照が、 **KdPrintEx**、 **Vdbgprintex**、および**vdbgprintexwithprefix**にも同様に適用されることに  **注意**してください。

 

-   [コンポーネント名の識別](#identifying-the-component-name)
-   [適切なレベルの選択](#choosing-the-correct-level)
-   [コンポーネントフィルターマスクの設定](#setting-the-component-filter-mask)
-   [メッセージを表示するための条件](#criteria-for-displaying-the-message)
-   [例](#example)
-   [DbgPrint バッファーとデバッガー](#dbgprint-buffer-and-the-debugger)

### <a name="identifying-the-component-name"></a>コンポーネント名の識別

各コンポーネントには、個別のフィルターマスクがあります。 このマスクを使用すると、デバッガーは各コンポーネントのフィルターを個別に構成できます。

各コンポーネントは、コンテキストに応じてさまざまな方法で参照されます。 **Dbgprintex**の*ComponentId*パラメーターでは、コンポーネント名の先頭に "DPFLTR\_" と "\_ID" が付加されます。 レジストリのコンポーネントフィルターマスクは、コンポーネント自体と同じ名前になります。 デバッガーでは、コンポーネントフィルターマスクの先頭に "Kd\_" と "\_Mask" というプレフィックスが付いています。

Windows Driver Kit (WDK) の DPFLTR ヘッダーファイルには、(\_*XXXX*\_ID 形式の) コンポーネント名の完全な一覧があります。 これらのコンポーネント名のほとんどは、Windows 用に予約されており、Microsoft によって作成されるドライバー用に予約されています。

独立系ハードウェアベンダー用に予約されているコンポーネント名は6つあります。 ドライバーの出力と Windows コンポーネントの出力が混在しないようにするには、次のコンポーネント名のいずれかを使用する必要があります。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">コンポーネント名</th>
<th align="left">ドライバーの種類</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>IHVVIDEO</p></td>
<td align="left"><p>ビデオドライバー</p></td>
</tr>
<tr class="even">
<td align="left"><p>IHVAUDIO</p></td>
<td align="left"><p>オーディオドライバー</p></td>
</tr>
<tr class="odd">
<td align="left"><p>IHVNETWORK</p></td>
<td align="left"><p>ネットワークドライバー</p></td>
</tr>
<tr class="even">
<td align="left"><p>IHVSTREAMING</p></td>
<td align="left"><p>カーネルストリーミングドライバー</p></td>
</tr>
<tr class="odd">
<td align="left"><p>IHVBUS</p></td>
<td align="left"><p>バスドライバー</p></td>
</tr>
<tr class="even">
<td align="left"><p>IHVDRIVER</p></td>
<td align="left"><p>その他の種類のドライバー</p></td>
</tr>
</tbody>
</table>

 

たとえば、ビデオドライバーを作成する場合は、DPFLTR\_IHVVIDEO\_ID を**Dbgprintex**の*ComponentId*パラメーターとして使用し、レジストリで値 name IHVVIDEO を使用して、 **Kd\_IHVVIDEO\_Mask を参照します。** デバッガーで。

Windows Vista 以降のバージョンの Windows では、 **Dbgprint**および**KdPrint** send のすべてのメッセージが既定のコンポーネント (DPFLTR\_default\_ID) に関連付けられています。

### <a name="choosing-the-correct-level"></a>適切なレベルの選択

**Dbgprintex**ルーチンの*Level*パラメーターの型は DWORD です。 これは、*重要度のビットフィールド*を判断するために使用されます。 *Level*パラメーターとこのビットフィールドの間の接続は、*レベル*のサイズによって異なります。

-   *Level*が0から31までの数値と等しい場合、重要度ビットフィールドはビットシフトとして解釈されます。 重要度ビットフィールドは、値 1 &lt;&lt;*レベル*に設定されます。 このため、 *Level*に0から31までの値を選択した場合、ビットフィールドのビットセットは1つだけになります。 *Level*が0の場合、ビットフィールドは0x00000001 に相当します。 *Level*が31の場合、ビットフィールドは0x80000000 に相当します。

-   *Level*が32から0xffffffff の範囲の数値の場合、重要度ビットフィールドは*レベル*自体の値に設定されます。

したがって、ビットフィールドを0x00004000 に設定する場合は、 *Level*を0x00004000 として、または単に14として指定できます。 このシステムの結果、一部のビットフィールド値 (完全にゼロのビットフィールドを含む) を生成することはできません。

次の定数は、 *Level*の値を設定するのに役立ちます。 これらのファイルは、次のように定義されています。

```ManagedCPlusPlus
#define DPFLTR_ERROR_LEVEL 0
#define DPFLTR_WARNING_LEVEL 1
#define DPFLTR_TRACE_LEVEL 2
#define DPFLTR_INFO_LEVEL 3
#define DPFLTR_MASK 0x80000000
```

*Level*パラメーターを使用する簡単な方法の1つは、0 ~ 31 の値を常に使用することです。これは、ビット0、1、2、および3を DPFLTR\_*XXXX*\_レベルで指定された意味で使用し、他のビットを使用して任意のものを意味します。

*Level*パラメーターを使用するもう1つの簡単な方法は、常に明示的なビットフィールドを使用することです。 このメソッドを選択する場合は、ビットフィールドで DPFLTR\_マスク値のビットごとの OR を使用できます。 この値により、32未満の値が誤って使用されることはありません。

Windows がメッセージレベルを使用する方法とドライバーの互換性を確保するには、重大なエラーが発生した場合に、重要度ビットフィールドの最低ビット (0x1) のみを設定する必要があります。 32未満の*レベル*値を使用している場合、この値は DPFLTR\_ERROR\_level に相当します。 重要度ビットフィールドが設定されている場合は、ドライバーが実行されているコンピューターに他のユーザーがカーネルデバッガーをアタッチするたびに、メッセージが表示されます。

適切な状況では、警告、トレース、および情報の各レベルを使用します。 他のビットは、役に立つ任意の目的に使用できます。 この機能により、さまざまな種類のメッセージを選択して表示または非表示にすることができます。

Windows Vista 以降のバージョンの Windows では、 **Dbgprint**および**KdPrint**によって送信されたすべてのメッセージは、DPFLTR\_INFO\_レベルと同じ*レベル*の**dbgprintex**および**KdPrintEx**メッセージのように動作します。 つまり、これらのメッセージには、重要度ビットフィールドの3番目のビットが設定されています。

### <a name="setting-the-component-filter-mask"></a>コンポーネントフィルターマスクの設定

コンポーネントフィルターマスクを設定するには、次の2つの方法があります。

- ターゲットコンピューターでは、レジストリキー **HKEY\_ローカル\_コンピューター\\システム\\CurrentControlSet\\コントロール\\セッションマネージャー\\デバッグ印刷フィルター**に、コンポーネントフィルターマスクを使用してアクセスできます。 レジストリエディターを使用して、このキーを作成または開きます。 このキーの下で、必要なコンポーネントの名前を使用して、大文字での値を作成します (たとえば、 **DEFAULT**または**IHVDRIVER**)。 この値には、コンポーネントのフィルターマスクとして使用する DWORD 値を設定します (たとえば、DPFLTR\_INFO\_LEVEL メッセージを表示するには、DPFLTR\_エラー\_レベルに加え、すべてのメッセージを表示するにはマスクを0Xf ですに設定します)。

- カーネルデバッガーがアクティブになっている場合は、の **\_** **\_** シンボルに格納されているアドレスを逆参照することにより、コンポーネントフィルターマスクの値にアクセスできます。<em>ここで、</em> *xxxx*は目的のコンポーネント名です。 このマスクの値を WinDbg または KD で表示するには、 **dd (表示 dword)** コマンドを使用するか、 **ED (enter dword)** コマンドで新しいコンポーネントフィルターマスクを入力します。 シンボルがあいまいになる危険性がある場合は、このシンボルを nt! として指定します **。Kd\_** <em>XXXX</em> **\_Mask**です。

レジストリに格納されているフィルターマスクは、ブート中に有効になります。 デバッガーによって作成されたフィルターマスクはすぐに有効になり、対象のコンピューターが再起動されるまで保持されます。 デバッガーはレジストリに設定されている値を上書きできますが、コンポーネントフィルターマスクは、対象のコンピューターが再起動された場合にレジストリで指定された値に戻ります。

また、WIN2000 というシステム全体のマスクもあります。 既定では、このマスクは0x1 と同じですが、他のすべてのコンポーネントと同様に、レジストリまたはデバッガーを使用して変更できます。 フィルター処理を実行すると、各コンポーネントフィルターマスクは、最初にビットごとの OR を使用して、WIN2000 マスクと結合されます。 特に、この組み合わせは、マスクが指定されていないコンポーネントが既定で0x1 に設定されていることを意味します。

### <a name="criteria-for-displaying-the-message"></a>メッセージを表示するための条件

**Dbgprintex**がカーネルモードコードで呼び出されると、Windows は*Level*によって指定されたメッセージの重要度ビットフィールドと、 *ComponentId*によって指定されたコンポーネントのフィルターマスクを比較します。

**注**   *level*パラメーターが 0 ~ 31 の場合、重要度ビットフィールドは 1 &lt;&lt;*レベル*と同じであることに注意してください。 しかし、 *level*パラメーターが32以上の場合、重要度ビットフィールドは単に*level*と等しくなります。

 

Windows は、重要度ビットフィールドとコンポーネントフィルターマスクに対して AND 演算を実行します。 結果が0以外の場合は、メッセージがデバッガーに送信されます。

### <a name="example"></a>例

最後に起動する前に、**デバッグ印刷フィルター**キーに次の値を作成したとします。

-   DWORD 0x2 と等しい値を持つ IHVVIDEO。

-   IHVBUS。これは DWORD 0x7FF に相当します。

ここで、カーネルデバッガーで次のコマンドを発行します。

```
kd> ed Kd_IHVVIDEO_Mask 0x8 
kd> ed Kd_IHVAUDIO_Mask 0x7 
```

この時点で、IHVVIDEO コンポーネントのフィルターマスクは0x8 で、IHVAUDIO コンポーネントのフィルターマスクは0x7 で、IHVBUS コンポーネントのフィルターマスクは0x7FF です。

ただし、これらのマスクは、ビットごとの OR を使用して、WIN2000 システム全体のマスク (通常は0x1 に等しい) と自動的に結合されるため、IHVVIDEO mask は実質的に0x9 と同じになります。 フィルターマスクがまったく設定されていないコンポーネント (たとえば、IHVSTREAMING または DEFAULT) には、フィルターマスクとして0x1 が割り当てられています。

ここで、次の関数呼び出しがさまざまなドライバーで発生するとします。

```
DbgPrintEx( DPFLTR_IHVVIDEO_ID,  DPFLTR_INFO_LEVEL,   "First message.\n");
DbgPrintEx( DPFLTR_IHVAUDIO_ID,  7,                   "Second message.\n");
DbgPrintEx( DPFLTR_IHVBUS_ID,    DPFLTR_MASK | 0x10,  "Third message.\n");
DbgPrint( "Fourth message.\n");
```

最初のメッセージの*レベル*パラメーターは、DPFLTR\_INFO\_level に等しいレベルです (3)。 この値は32未満であるため、ビットシフトとして扱われるので、ビットフィールドの重要度が低くなります。 この値は、AND 演算を使用して0x9 の有効な IHVVIDEO コンポーネントフィルターマスクと結合され、0以外の結果が得られます。 そのため、最初のメッセージがデバッガーに送信されます。

2番目のメッセージの*レベル*パラメーターは7です。 この場合も、この値はビットシフトとして扱われるので、ビットフィールドの重要性があります。 この値は AND 演算を使用して0x7 の IHVAUDIO コンポーネントフィルターマスクと結合され、結果は0になります。 そのため、2番目のメッセージは転送されません。

3番目のメッセージには、DPFLTR\_MASK | と等しい*レベル*パラメーターがあります。0x10. この値は31を超えているため、重要度ビットフィールドは、0x80000010 に設定されている*Level*の値と同じになります。 この値は、AND 演算を使用して、IHVBUS コンポーネントフィルターマスクである0x7FF と結合され、0以外の結果が得られます。 そのため、3番目のメッセージがデバッガーに送信されます。

4番目のメッセージは、 **Dbgprintex**ルーチンではなく、 **dbgprint**ルーチンに渡されました。 Windows Server 2003 以前のバージョンの Windows では、 **Dbgprint**に渡されるメッセージは常に転送されます。 Windows Vista 以降のバージョンの Windows では、 **Dbgprint**に渡されたメッセージには常に既定のフィルターが適用されます。 重要度ビットフィールドは、1 &lt;&lt; DPFLTR\_INFO\_レベル (0x00000008) に相当します。 このルーチンのコンポーネントは、既定値です。 既定のコンポーネントのフィルターマスクを設定していないので、値は0x1 です。 AND 演算を使用してこのマスクと重要度ビットフィールドを組み合わせると、結果は0になります。 4番目のメッセージは転送されません。

### <a name="dbgprint-buffer-and-the-debugger"></a>DbgPrint バッファーとデバッガー

**Dbgprint**、 **dbgprintex**、 **vdbgprintex**、 **vdbgprintexwithprefix**、 **KdPrint**、または**KdPrintEx**ルーチンがメッセージをデバッガーに送信すると、書式設定された文字列が**dbgprint**バッファーに送信されます。 このバッファーの内容は、GFlags の**バッファー DbgPrint 出力**オプションを使用してこの表示を無効にしていない限り、デバッガーコマンドウィンドウに直ちに表示されます。

このディスプレイを無効にした場合は、 **! dbgprint**拡張コマンドを使用することによってのみ、dbgprint バッファーの内容を表示できます。 デバッガー拡張機能の詳細については、「 [Windows デバッグ](https://docs.microsoft.com/windows-hardware/drivers/debugger/index)」を参照してください。

**Dbgprint**、 **dbgprintex**、 **vdbgprintex**、 **vdbgprintexwithprefix**、 **KdPrint**、または**KdPrintEx**を1回呼び出すと、512バイトの情報のみが転送されます。 512バイトより長い出力は失われます。 DbgPrint バッファー自体は、Windows の無料ビルドで最大 4 KB のデータを保持でき、Windows のチェックされたビルドで最大 32 KB のデータを保持できます。 Windows Server 2003 以降のバージョンの Windows では、KDbgCtrl ツールを使用して、DbgPrint バッファーのサイズを変更できます。 このツールは、Windows 用デバッグツールの一部です。

*ComponentId*と*Level*の値によってメッセージがフィルターで除外される場合、そのメッセージはデバッグ接続を介して送信されません。 このため、このメッセージをデバッガーで表示する方法はありません。

 

 





