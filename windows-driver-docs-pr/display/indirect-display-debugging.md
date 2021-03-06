---
title: デバッグ (間接ディスプレイドライバーを)
description: 間接的な表示のデバッグ手法について説明します
ms.assetid: a343812d-03d0-4a95-9c36-7e6b5a404088
ms.date: 04/22/2020
ms.localizationpriority: medium
ms.openlocfilehash: 59c3acb5f719859e8f219cbc90adfafd53d94331
ms.sourcegitcommit: 49d7f27a24360559456063092ac35b2ba1aba7b1
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/04/2020
ms.locfileid: "82742618"
---
# <a name="debugging-indirect-displays"></a>デバッグ (間接表示を)

間接的に表示されるドライバーは、umdf ドライバーであるため、UMDF デバッグドキュメントが適切な開始点となります。このセクションのページの例を[次](https://docs.microsoft.com/windows-hardware/drivers/wdf/determining-why-the-umdf-driver-fails-to-load-or-the-umdf-device-fails)に示します。  このページには、間接的に表示される特定のデバッグ情報が表示されます。

## <a name="span-idregistry_controlspanspan-idregistry_controlspanspan-idregistry_controlspanregistry-control"></a><span id="Registry_Control"></span><span id="registry_control"></span><span id="Registry_Control"></span>レジストリコントロール

IddCx には、間接ディスプレイドライバーのデバッグを支援するために使用できるレジストリ設定がいくつかあります。  すべてのレジストリ値は、 **HKLM\System\CurrentControlSet\Control\GraphicsDrivers**レジストリキーの下にあります。


| 値の名前               | 詳細 |
|--------------------------|---------|
| TerminateIndirectOnStall | 0を指定すると、フレームが使用可能になってから10秒以内にフレームが処理されない場合に、ドライバーを終了するウォッチドッグが無効になります。  それ以外の値を指定すると、ウォッチドッグは有効のままになります。 |
| IddCxDebugCtrl           | IddCx のさまざまなデバッグ側面を有効にしたビットフィールド、次の表を参照してください。 |

**メモ**TerminateIndirectOnStall レジストリ値を使用してウォッチドッグ HLK を無効にすると、テストは失敗します。

### <a name="iddcxdebugctrl-values"></a>IddCxDebugCtrl の値

| IddCxDebugCtrl のビット | 意味  |
|:---------------------:|----------|
| 0x0001 | IddCx がエラーを検出したときにデバッガーを中断する |
| 0x0002 | IddCx が読み込まれたときにデバッガーを中断する |
| 0x0004 | IddCx がアンロードされたときにデバッガーを中断する |
| 0x0008 | IddCx DriverEntry が呼び出されたときにデバッガーを中断する |
| 0x0010 | ドライバーのバインドが呼び出されたときにデバッガーを中断する |
| 0x0020 | ドライバーの開始が呼び出されたときにデバッガーを中断する |
| 0x0040 | ドライバーのバインド解除が呼び出されたときにデバッガーを中断する |
| 0x0080 | Ddi コールでドライバーを終了するときに時間がかかりすぎる DDI ウォッチドッグを無効にします |
| 0x0100 | 未使用 |
| 0x0200 | デバッグオーバーレイを有効にします。以下を参照してください |
| 0x0400 | フレーム内のダーティ rect に色の付いたアルファボックスを重ねて、0x0200 を設定する必要があります |
| 0x0800 | Pref stats を frame にオーバーレイし、0x0200 を設定する必要があります |

**メモ**どのオーバーレイ関数も、ドライバーによって作成され、IddCxSwapChainSetDevice () に渡された Direct3D デバイスを動作させるために、D3D11_CREATE_DEVICE_BGRA_SUPPORT フラグを使用して作成する必要があります。

## <a name="span-ididdcx_wpp_tracesspanspan-ididdcx_wpp_tracesspanspan-ididdcx_wpp_tracesspaniddcx-wpp-traces"></a><span id="IddCx_WPP_traces"></span><span id="iddcx_wpp_traces"></span><span id="IddCx_WPP_traces"></span>IddCx WPP トレース

Iddcx は、WPP インフラストラクチャを使用してデバッグ情報を記録します。  WPP 情報はファイルにキャプチャできますが、キャプチャの進行中はカーネルデバッガーに表示できます。

### <a name="capturing-iddcx-wpp-tracing"></a>IddCx WPP トレースのキャプチャ

WPP のトレースを有効にする方法はいくつかあります。 logman プログラムでビルドを使用すると便利です。  次の行をバッチファイルにコピーし、管理者特権でのコマンドプロンプトから実行すると、IddCx WPP トレースが IddCx ファイルに収集されます。

```
@echo off  
echo Starting WPP tracing....
logman create trace IddCx -o IddCx.etl -ets -ow -mode sequential -p  {D92BCB52-FA78-406F-A9A5-2037509FADEA} 0x4f4 0xFF
echo Tracing enabled
pause
echo Stopping WPP tracing....
logman -stop IddCx -ets
```

#### <a name="controlling-what-is-captured"></a>キャプチャ対象の制御
Logman の Flags パラメーター (この場合は 0x4f4) は、どの WPP メッセージ IddCx ログを記録するかを制御します。  この値の意味は、Windows ビルド19041以降で変更されています。

##### <a name="flags-meaning-prior-to-windows-build-19041"></a>Windows ビルド19041より前のフラグの意味
フラグがレベルとして扱われ、上位レベルごとに新しい種類のメッセージと、前のレベルのすべてのメッセージが追加されました。

| フラグレベルの値  | キャプチャされたメッセージの種類 |
|:------------------:|-----------------------|
| 1                  | 使用されていない              |
| 2                  | エラー                |
| 3                  | 警告              |
| 4                  | Information           |
| 5                  | "詳細"               |

##### <a name="flags-meaning-for-windows-build-19041-and-above"></a>Windows ビルド19041以降のフラグの意味
フラグはビットフィールドで、メッセージの種類がキャプチャされた場合、各ビットが制御します。

| フラグビット | キャプチャされたメッセージの種類  |
|:---------:|------------------------|
| 0x001     | 未使用  |
| 0x002     | 未使用  |
| 0x004     | エラー  |
| 0x008     | 問題のないエラー。たとえば、D3D11_CREATE_DEVICE_BGRA_SUPPORT が設定されていない状態でデバッグオーバーレイが有効になっている場合 |
| 0x010     | IddCx オブジェクト  |
| 0x020     | IddCx への UMDF framework 呼び出し |
| 0x040,     | IddCx からドライバーへの DDI 呼び出し |
| 0x080     | ドライバーから IddCx への低頻度呼び出し |
| 0x100     | ドライバーから IddCx への高頻度フレーム関連の呼び出し |
| 0x200     | ドライバーから IddCx への高頻度カーソル関連の呼び出し |
| 0x400     | カーネルから IddCx への呼び出し |
| 0x800     | IddCx からカーネルへの呼び出し |

通常のログ記録シナリオでは、0x0f4 を使用することをお勧めします。フレームごとの情報を表示する場合は、0x1f4 を使用することをお勧めします。

### <a name="decoding-iddcx-wpp-tracing"></a>IddCx WPP トレースをデコードしています
すべての WPP トレースと同様に、WPP 情報は pdb ファイルに格納されます。そのため、pdb にアクセスして、その情報をデコードする必要があります。  Windows ビルド19560より前の場合、パブリックシンボルサーバーの IddCx には、WPP デコードを有効にするために必要な WPP 情報が含ま**れていません**。 Windows ビルド19560以降の場合、パブリックシンボルサーバーの IddCx には、WPP メッセージをデコードするために必要な WPP 情報が含まれています。

標準の WPP デコードツールのいずれかを使用して、メッセージのデコードと表示を行うことができます。

## <a name="span-iddebugging_iddcx_errorsspanspan-iddebugging_iddcx_errorsspanspan-iddebugging_iddcx_errorsspandebugging-iddcx-errors"></a><span id="Debugging_IddCx_errors"></span><span id="debugging_iddcx_errors"></span><span id="Debugging_IddCx_errors"></span>IddCx エラーのデバッグ
間接的な表示ドライバーを開発するときに、IddCx がエラーを検出したときに追加情報を取得すると便利な場合がよくあります。  上記のセクションを使用すると、IddCx がエラーを検出したときにデバッガーを中断するように IddCx を構成できますが、エラーのコンテキストを理解するために、最後のいくつかのトレースメッセージに IddCx エラーメッセージを表示すると便利です。
上記のセクションを使用すると、logman を使用して WPP のトレースを有効にすることができます。次の情報を参考にして、障害発生時のカーネルデバッガーでインメモリの WPP バッファーを表示します。
**メモ**これを機能させるには、デバッガーが WPP デコード情報を含む IddCx を取得するために、(ユーザーモードのデバッガーではなく) カーネルデバッガーと Windows ビルド19560以降を使用する必要があります。

次の例では、間接ディスプレイドライバーが IddCxMonitorArrival () を呼び出し、IddCx 処理の一部としてドライバーの EvtIddCxMonitorQueryTargetModes () DDI を呼び出します。この例では、ドライバーは DISPLAYCONFIG_VIDEO_SIGNAL_INFO のモードを返しました。AdditionalSignalInfo。 vSyncFreqDivider が0に設定されていますが、これは無効であり、エラーが発生します。

使用されるデバッガーコマンドの一覧を次に示します。

| command                             | 意味  |
|-------------------------------------|----------|
| !wmitrace.bufdump                   | すべてのログバッファーと名前を一覧表示します。 IddCx は自分の名前であり、logman コマンドラインから取得されます。 |
| ! wmitrace<Log buffer name> | IddCx の例で、指定したログバッファーの内容をデコードして表示します。 |

この例のデバッガー出力を次に示します。

```
0: kd> !wmitrace.bufdump
(WmiTrace) BufDump
    LoggerContext Array @ 0xFFFFE6055EB0AC40 [64 Elements]

 Logger Context  Number Available   Size    NPP Usage   PP Usage
================ ====== ========= ======== =========== ==========
ffffe6055ee6c800      4         2     4096       16384             Circular Kernel Context Logger
ffffe6055eaa8640      2         2    65536      131072             Eventlog-Security
ffffe6055eb83a00      2         1    65536      131072             DefenderApiLogger
ffffe6055ebb6a00      2         2    65536      131072             DefenderAuditLogger
ffffe6055eb74040      2         1    16384       32768             DiagLog
ffffe6055eb74640      4         2    65536      262144             Diagtrack-Listener
ffffe6055eaa8040      2         2    65536                 131072  EventLog-Application
ffffe6055eb7c040      2         1    65536      131072             EventLog-System
ffffe6055eb7c640      5         3    65536      327680             LwtNetLog
ffffe6055eb85040      4         2    65536      262144             Microsoft-Windows-Rdp-Graphics-RdpIdd-Trace
ffffe6055eb85680      8         6   131072     1048576             NetCore
ffffe6055eb89040      4         4     4096       16384             NtfsLog
ffffe6055eb89640      8         6   131072     1048576             RadioMgr
ffffe605683ef040      3         2     4096                  12288  WindowsUpdate_trace_log
ffffe6055eb8f640      2         2     2048        4096             UBPM
ffffe6055eb108c0      4         2    16384       65536             WdiContextLog
ffffe6055eb968c0      4         2    81920      327680             WiFiSession
ffffe60567e8a6c0      5         3     8192       40960             IddCx
ffffe605658379c0     10         9     3072       30720             umstartup
ffffe605659d4840     10         9   131072     1310720             SCM
ffffe605655af9c0      2         1    65536      131072             UserNotPresentTraceSession
ffffe605659d6840      2         1     4096        8192             COM
ffffe60565925080     10         8    20480      204800             Terminal-Services-LSM
ffffe60565956080     10         9    20480      204800             Terminal-Services-RCM
ffffe6055eba39c0     50        49     3072      153600             UserMgr
ffffe60567388280      2         2    32768       65536             WFP-IPsec Diagnostics
ffffe605678a3040      5         3     4096       20480             MpWppTracing-20200424-092923-00000003-ffffffff
ffffe60567e35080      2         1    65536      131072             ScreenOnPowerStudyTraceSession
ffffe605655e0a00      5         3     4096       20480             SHS-04242020-092951-7-7f
ffffe605692054c0      4         4     8192       32768             RdpIdd
ffffe60567f597c0      4         3    65536      262144             SgrmEtwSession
ffffe605678a9a00      4         4     8192       32768             DispBrok-DeskSrv
ffffe60569286680      4         4     8192       32768             DispBrok-Desk
ffffe605668026c0      4         4     8192       32768             DispBrok
================ ====== ========= ======== =========== ==========
                    195       159             6651904     143360

0: kd> !wmitrace.logdump IddCx
(WmiTrace) LogDump for Logger Id 0x13
Found Buffers: 5 Messages: 537, sorting entries
[1]0EF8.0CF0::04/24/2020-09:43:36.894 [cx][IddCx]DriverEntry: Enter
[1]0EF8.0CF0::04/24/2020-09:43:36.897 [cx][IddCx]?IddCxLibraryInitialize@@YAJXZ: Enter
[1]0EF8.0CF0::04/24/2020-09:43:36.897 [cx][IddCx]?IddCxLibraryInitialize@@YAJXZ: Exit
[1]0EF8.0CF0::04/24/2020-09:43:36.897 [cx][IddCx]DriverEntry: Exit, status=STATUS_SUCCESS
[0]0EF8.0CF0::04/24/2020-09:43:36.904 [cx][IddCx]?IddCxLibraryBindClient@@YAJPEAU_WDF_CLASS_BIND_INFO@@PEAPEAX@Z: Enter
[0]0EF8.0CF0::04/24/2020-09:43:36.904 [cx][IddCx]?IddCxLibraryBindClient@@YAJPEAU_WDF_CLASS_BIND_INFO@@PEAPEAX@Z: Exit, status=STATUS_SUCCESS
[0]0EF8.0CF0::04/24/2020-09:43:36.910 [cx][IddCx]IddCxImplDeviceInitConfig: Enter
[0]0EF8.0CF0::04/24/2020-09:43:36.910 [cx][IddCx]IddCxImplDeviceInitConfig: Exit, status=STATUS_SUCCESS
[0]0EF8.0CF0::04/24/2020-09:43:36.910 [cx][IddCx]IddCxImplGetVersion: Enter
[0]0EF8.0CF0::04/24/2020-09:43:36.910 [cx][IddCx]IddCxImplGetVersion: Exit, status=STATUS_SUCCESS
[0]0EF8.0CF0::04/24/2020-09:43:36.911 [cx][IddCx]IddCxImplDeviceInitialize: Enter
[0]0EF8.0CF0::04/24/2020-09:43:36.912 [cx][IddCx]IddCxImplDeviceInitialize: New IddDevice 0x000001642F5E0770 created
[0]0EF8.0CF0::04/24/2020-09:43:36.912 [cx][IddCx]IddCxImplDeviceInitialize: Exit, status=STATUS_SUCCESS
[0]0EF8.0CF0::04/24/2020-09:43:36.917 [cx][IddCx]IddCxImplAdapterInitAsync: Enter
[0]0EF8.0CF0::04/24/2020-09:43:36.917 [cx][IddCx]?Init@IddAdapter@@QEAAXPEAUIDDCX_ADAPTER__@@PEAVIddDevice@@PEAUIDDCX_ADAPTER_CAPS@@@Z: New IddAdapter 0x000001642F5E77D0 created, API object 0xFFFFFE9BD0A18978, IddDevice 0x000001642F5E0770
[0]0EF8.0CF0::04/24/2020-09:43:36.917 [cx][IddCx]?SendUserModeMessage@IddAdapter@@QEAAJIPEAXI0W4DXGK_IDD_ESCAPE_CODE@@PEAI@Z: Sending escape 0x0 to kernel
Unknown( 76): GUID=ac5ec775-ccdb-3c2c-6150-28b4eacacbc4 (No Format Information found).
[0]0EF8.0CF0::04/24/2020-09:43:36.917 [cx][IddCx]IddCxImplAdapterInitAsync: Exit, status=STATUS_SUCCESS
[0]0EF8.0558::04/24/2020-09:43:36.935 [cx][IddCx]?HandleKernelModeMessage@IddAdapter@@QEAAXIPEAXI0PEAI@Z: IddAdapter 0x000001642F5E77D0, processing command START_ADAPTER_COMPLETE from KMD
[0]0EF8.0558::04/24/2020-09:43:36.935 [cx][IddCx]?HandleKernelModeMessage@IddAdapter@@QEAAXIPEAXI0PEAI@Z: IddAdapter 0x000001642F5E77D0, Successful adapter start, Wddm Luid = 0xe6e90, Adapter caps 0x0, Session Id 0, Terminal Luid 0x0
[0]0EF8.0558::04/24/2020-09:43:36.935 [cx][IddCx]?HandleKernelModeMessage@IddAdapter@@QEAAXIPEAXI0PEAI@Z: Exit
[0]0EF8.1588::04/24/2020-09:43:36.936 [cx][IddCx]<lambda_e42696d61f3ea0fd0d39fdb90d856b7b>::operator(): DDI: Calling EvtIddCxAdapterInitFinished DDI, IddAdapter 0xFFFFFE9BD0A18978
[0]0EF8.1588::04/24/2020-09:43:36.936 [cx][IddCx]IddCxImplMonitorCreate: Enter
[0]0EF8.1588::04/24/2020-09:43:36.936 [cx][IddCx]IddCxImplMonitorCreate: New IddMonitor 0x000001642F5EF720 created, API object 0xFFFFFE9BD0A11A38, IddAdapter 0x000001642F5E77D0
[0]0EF8.1588::04/24/2020-09:43:36.936 [cx][IddCx]IddCxImplMonitorCreate: Exit, status=STATUS_SUCCESS
[0]0EF8.1588::04/24/2020-09:43:36.936 [cx][IddCx]IddCxImplMonitorArrival: Enter
[0]0EF8.1588::04/24/2020-09:43:36.936 [cx][IddCx]?StartWatchInternal@IddWatchdog@@AEAAXK@Z: IddWatchdog 0x000001642F5E77F0, still has pending watch not started by watchdog thread.
[0]0EF8.1588::04/24/2020-09:43:36.936 [cx][IddCx]?ParseMonitorDescription@IddDevice@@QEAAXUIDDCX_MONITOR_DESCRIPTION@@AEAV?$vector@UIDDCX_MONITOR_MODE@@V?$allocator@UIDDCX_MONITOR_MODE@@@std@@@std@@AEAI@Z: DDI: Calling EvtIddCxParseMonitorDescriptio DDI to get mode count, Device 0x000001642F5E0770
[0]0EF8.1588::04/24/2020-09:43:36.936 [cx][IddCx]?ParseMonitorDescription@IddDevice@@QEAAXUIDDCX_MONITOR_DESCRIPTION@@AEAV?$vector@UIDDCX_MONITOR_MODE@@V?$allocator@UIDDCX_MONITOR_MODE@@@std@@@std@@AEAI@Z: DDI: Return successfully from EvtIddCxParseMonitorDescriptio DDI to get mode count, mode count 23
[0]0EF8.1588::04/24/2020-09:43:36.936 [cx][IddCx]?StartWatchInternal@IddWatchdog@@AEAAXK@Z: IddWatchdog 0x000001642F5E77F0, still has pending watch not started by watchdog thread.
[0]0EF8.1588::04/24/2020-09:43:36.936 [cx][IddCx]?StartWatchInternal@IddWatchdog@@AEAAXK@Z: IddWatchdog 0x000001642F5E77F0, still has pending watch not started by watchdog thread.
[0]0EF8.1588::04/24/2020-09:43:36.936 [cx][IddCx]?ParseMonitorDescription@IddDevice@@QEAAXUIDDCX_MONITOR_DESCRIPTION@@AEAV?$vector@UIDDCX_MONITOR_MODE@@V?$allocator@UIDDCX_MONITOR_MODE@@@std@@@std@@AEAI@Z: DDI: Calling EvtIddCxParseMonitorDescriptio DDI to get modes, Device 0x000001642F5E0770
[0]0EF8.1588::04/24/2020-09:43:36.936 [cx][IddCx]?ParseMonitorDescription@IddDevice@@QEAAXUIDDCX_MONITOR_DESCRIPTION@@AEAV?$vector@UIDDCX_MONITOR_MODE@@V?$allocator@UIDDCX_MONITOR_MODE@@@std@@@std@@AEAI@Z: DDI: Return successfully from EvtIddCxParseMonitorDescriptio DDI to get modes
[0]0EF8.1588::04/24/2020-09:43:36.936 [cx][IddCx]?StartWatchInternal@IddWatchdog@@AEAAXK@Z: IddWatchdog 0x000001642F5E77F0, still has pending watch not started by watchdog thread.
[0]0EF8.1588::04/24/2020-09:43:36.936 [cx][IddCx]?AddMonitorModes@IddMonitor@@AEAAXAEAV?$vector@UTARGET_MONITOR_MODE@@V?$allocator@UTARGET_MONITOR_MODE@@@std@@@std@@@Z: IddMonitor 0x000001642F5EF720, parseMonitorDescription returned 23 modes.
[0]0EF8.1588::04/24/2020-09:43:36.936 [cx][IddCx]?StartWatchInternal@IddWatchdog@@AEAAXK@Z: IddWatchdog 0x000001642F5E77F0, still has pending watch not started by watchdog thread.
[0]0EF8.1588::04/24/2020-09:43:36.936 [cx][IddCx]?QueryModes@IddMonitor@@AEAAXAEAV?$vector@UIDDCX_TARGET_MODE@@V?$allocator@UIDDCX_TARGET_MODE@@@std@@@std@@@Z: DDI: Calling EvtIddCxMonitorQueryTargetModes DDI for mode count, IddMonitor 0x000001642F5EF720
[0]0EF8.1588::04/24/2020-09:43:36.936 [cx][IddCx]?QueryModes@IddMonitor@@AEAAXAEAV?$vector@UIDDCX_TARGET_MODE@@V?$allocator@UIDDCX_TARGET_MODE@@@std@@@std@@@Z: DDI: Return successfully from EvtIddCxMonitorQueryTargetModes DDI, mode count = 0x23
[0]0EF8.1588::04/24/2020-09:43:36.936 [cx][IddCx]?StartWatchInternal@IddWatchdog@@AEAAXK@Z: IddWatchdog 0x000001642F5E77F0, still has pending watch not started by watchdog thread.
[0]0EF8.1588::04/24/2020-09:43:36.936 [cx][IddCx]?StartWatchInternal@IddWatchdog@@AEAAXK@Z: IddWatchdog 0x000001642F5E77F0, still has pending watch not started by watchdog thread.
[0]0EF8.1588::04/24/2020-09:43:36.936 [cx][IddCx]?QueryModes@IddMonitor@@AEAAXAEAV?$vector@UIDDCX_TARGET_MODE@@V?$allocator@UIDDCX_TARGET_MODE@@@std@@@std@@@Z: DDI: Calling EvtIddCxMonitorQueryTargetModes DDI to get modes, IddMonitor 0x000001642F5EF720
[0]0EF8.1588::04/24/2020-09:43:36.936 [cx][IddCx]?QueryModes@IddMonitor@@AEAAXAEAV?$vector@UIDDCX_TARGET_MODE@@V?$allocator@UIDDCX_TARGET_MODE@@@std@@@std@@@Z: DDI: Return successfully from EvtIddCxMonitorQueryTargetModes DDI
[0]0EF8.1588::04/24/2020-09:43:36.936 [cx][IddCx]?StartWatchInternal@IddWatchdog@@AEAAXK@Z: IddWatchdog 0x000001642F5E77F0, still has pending watch not started by watchdog thread.
[0]0EF8.1588::04/24/2020-09:43:36.936 [cx][IddCx]?AddTargetModes@IddMonitor@@AEAAXAEAV?$vector@UTARGET_MONITOR_MODE@@V?$allocator@UTARGET_MONITOR_MODE@@@std@@@std@@@Z: IddMonitor 0x000001642F5EF720, queryTargetModes returned 23 modes.
[0]0EF8.1588::04/24/2020-09:43:55.341 [cx][IddCx] Throwing error (Status 0xc000000d(STATUS_INVALID_PARAMETER)) from function Validate in onecoreuap\windows\core\dxkernel\indirectdisplays\classext\cx\ddivalidation.cpp:412, Msg DISPLAYCONFIG_VIDEO_SIGNAL_INFO.AdditionalSignalInfo.vSyncFreqDivider cannot be zero for target mode
Total of 537 Messages from 5 Buffers

```

最後の行は、エラーの理由を示しています。