---
title: ndiskd dbgsystems
description: Ndiskd dbgsystems 拡張機能によって、デバッグトレースが有効になっている NDIS サブシステムが表示され、必要に応じて変更されます。  ndiskd dbgsystems は、WPP とドライバーの検証ツールによって置き換えられました。
ms.assetid: f36a26b6-18a8-4a01-96c7-99826e6b662f
keywords:
- ndiskd dbgsystems Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ndiskd.dbgsystems
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b47b5cf4b4296706d90c6f8ca5b3f291f2cc59ca
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72826671"
---
# <a name="ndiskddbgsystems"></a>!ndiskd.dbgsystems


**! Ndiskd dbgsystems**拡張機能によって、デバッグトレースが有効になっている NDIS サブシステムが表示され、必要に応じて変更されます。

**警告**  
 **! ndiskd DBGSYSTEMS**は、WPP (Windows software trace プリプロセッサ) とドライバーの検証ツールによって置き換えられました。 ! ndiskd は、ターゲットシステムが **! ndiskd dbgsystems**をサポートしていない場合に、次の警告を出します。

```console
0: kd> !ndiskd.dbgsystems
    This target does not support tracing through !ndiskd.dbglevel or
    !ndiskd.dbgsystems.
    Learn how to collect traces with WPP
```

警告の下部にあるリンクをクリックすると、詳細情報が表示されます。

```console
0: kd> !ndiskd.help wpptracing
    WPP traces are fast, flexible, and detailed.  Plus, starting with Windows 8
    and Windows Server 2012, you can automatically decode NDIS traces using the
    symbol file.  Just point TraceView (or tracepdb.exe) at NDIS.PDB, and it
    will be able to get all the TMFs it needs to trace NDIS activity.
    
    If you would like traces to be printed in the debugger window, you use the
    !wmitrace extension.  For example, you might enable traces with this:

    !wmitrace.searchpath c:\path\to\TMF\files
    !wmitrace.start ndis -kd
    !wmitrace.enable ndis {DD7A21E6-A651-46D4-B7C2-66543067B869} -level 4 -flag 0x31f3
```

 

WPP の詳細については、「 [Wpp ソフトウェアのトレース](https://docs.microsoft.com/windows-hardware/drivers/devtest/wpp-software-tracing)」を参照してください。

ドライバーの検証機能の詳細については、「 [Driver verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)」を参照してください。

WMI トレースの詳細については、「 [Wmi トレース拡張機能 (Wmitrace)](https://docs.microsoft.com/windows-hardware/drivers/debugger/wmi-tracing-extensions--wmitrace-dll-)」を参照してください。

```console
!ndiskd.dbgsystems [-subsystem <any>] 
```

## <a name="span-idddk__ndiskd_dbgsystems_dbgspanspan-idddk__ndiskd_dbgsystems_dbgspanparameters"></a><span id="ddk__ndiskd_dbgsystems_dbg"></span><span id="DDK__NDISKD_DBGSYSTEMS_DBG"></span>パラメータ


<span id="_______-subsystem______"></span><span id="_______-SUBSYSTEM______"></span> *-サブシステム*   
切り替えるサブシステム。

複数のコンポーネントが選択されている場合は、スペースで区切ります。 以前に選択したコンポーネントが繰り返された場合、そのデバッグの監視はオフになります。 可能な値は次のとおりです。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>値</strong></p></td>
<td align="left"><p><strong>通用</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p>初期化</p></td>
<td align="left"><p>アダプターの初期化をトレースします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>.CONFIG</p></td>
<td align="left"><p>アダプター構成をトレースします。</p></td>
</tr>
<tr class="even">
<td align="left"><p>SEND</p></td>
<td align="left"><p>ネットワーク経由でデータを送信するトレース。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>RECV</p></td>
<td align="left"><p>ネットワークからデータを受信するトレース。</p></td>
</tr>
<tr class="even">
<td align="left"><p>プロトコル</p></td>
<td align="left"><p>プロトコル操作をトレースします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>束縛</p></td>
<td align="left"><p>バインディング操作をトレースします。</p></td>
</tr>
<tr class="even">
<td align="left"><p>BUS_QUERY</p></td>
<td align="left"><p>バスクエリをトレースします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>登録</p></td>
<td align="left"><p>レジストリ操作をトレースします。</p></td>
</tr>
<tr class="even">
<td align="left"><p>量</p></td>
<td align="left"><p>メモリ管理をトレースします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FILTER</p></td>
<td align="left"><p>フィルター操作をトレースします。</p></td>
</tr>
<tr class="even">
<td align="left"><p>要求</p></td>
<td align="left"><p>要求をトレースします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>WORK_ITEM</p></td>
<td align="left"><p>作業項目の操作をトレースします。</p></td>
</tr>
<tr class="even">
<td align="left"><p>PNP</p></td>
<td align="left"><p>プラグアンドプレイ操作をトレースします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>PM</p></td>
<td align="left"><p>電源管理操作をトレースします。</p></td>
</tr>
<tr class="even">
<td align="left"><p>OPEN</p></td>
<td align="left"><p>参照オブジェクトを開く操作をトレースします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>固定</p></td>
<td align="left"><p>ロック操作をトレースします。</p></td>
</tr>
<tr class="even">
<td align="left"><p>RESET</p></td>
<td align="left"><p>リセット操作をトレースします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>WMI に関するページ</p></td>
<td align="left"><p>Windows Management Instrumentation 操作をトレースします。</p></td>
</tr>
<tr class="even">
<td align="left"><p>NDIS_CO</p></td>
<td align="left"><p>接続指向の NDIS をトレースします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>「</p></td>
<td align="left"><p>参照操作をトレースします。</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Ndiskd .dll

<a name="remarks"></a>注釈
-------

この拡張機能は、チェックを行う NDIS にのみ適用されます。 NDIS のビルド情報を確認するには、 [ **! ndiskd ndis**](-ndiskd-ndis.md)拡張機能を実行します。

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[ネットワークドライバーの設計ガイド](https://docs.microsoft.com/windows-hardware/drivers/network/index)

[Windows Vista 以降のネットワークリファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)

[ネットワークスタックのデバッグ](https://go.microsoft.com/fwlink/p/?linkid=845311)

[**NDIS 拡張機能 (Ndiskd .dll)** ](ndis-extensions--ndiskd-dll-.md)

[ **!ndiskd.help**](-ndiskd-help.md)

[ **!ndiskd.ndis**](-ndiskd-ndis.md)

[WPP ソフトウェア トレース](https://docs.microsoft.com/windows-hardware/drivers/devtest/wpp-software-tracing)

[ドライバーの検証ツール](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)

[WMI トレース拡張機能 (Wmitrace)](https://docs.microsoft.com/windows-hardware/drivers/debugger/wmi-tracing-extensions--wmitrace-dll-)

 

 






