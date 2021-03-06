---
title: PwrTest のデバイス シナリオ
description: PwrTest デバイスのシナリオでは、デバイスのアイドル状態の統計を監視します。
ms.assetid: 75C53B6E-3D1F-4E9D-A99E-3060A9CC37BC
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0ba13206cebbddda0cf7dcc8109685988e622796
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67393506"
---
# <a name="pwrtest-device-scenario"></a>PwrTest のデバイス シナリオ


PwrTest デバイスのシナリオでは、デバイスのアイドル状態の統計を監視します。

このシナリオは、主に Windows 7 デバイスの電源の動作の使用、Windows の今後のバージョンが Pwrtest で現在サポートされていないデバイスをアイドル状態を追跡するため、別のメカニズムを使用します。 Windows 7 よりも新しい Windows のバージョン、使用、 [Windows パフォーマンス ツールキット (WPT)](https://go.microsoft.com/fwlink/p/?linkid=294280)します。 WPT には、カーネル モードの電源プロバイダーをトレースするために使用できる Windows Performance Recorder (WPR) と Windows パフォーマンス アナライザー (WPA) フレームワーク (PoFx) デバイスの電源の統計を表示することができますし、その後、遷移グラフ化できますが含まれています。

## <a name="span-idsyntaxspanspan-idsyntaxspanspan-idsyntaxspansyntax"></a><span id="Syntax"></span><span id="syntax"></span><span id="SYNTAX"></span>構文


```
pwrtest /device  [/t:n] [/?] 
```

<span id="_t_n"></span><span id="_T_N"></span>**t:** <em>n</em>  
シナリオの実行を合計時間 (分) を指定します (既定値の*n*は 30 分です)。

**使用例**

```
pwrtest /device /t:60
```

```
pwrtest /device
```

### <a name="span-idxmllogfileoutputspanspan-idxmllogfileoutputspanspan-idxmllogfileoutputspanxml-log-file-output"></a><span id="XML_log_file_output"></span><span id="xml_log_file_output"></span><span id="XML_LOG_FILE_OUTPUT"></span>XML ログ ファイルの出力

```XML
<PwrTestLog>
  <SystemInformation>
  </SystemInformation>
  <DeviceIdleEvents> 
    <DeviceIdleChangeEvent>
        <Timestamp></TimeStamp>
        <InstancePath></InstancePath>
        <Description></Description>
    </DeviceIdleChangeEvent>
    <DeviceIdleEvent>
        <Timestamp></TimeStamp>
        <InstancePath></InstancePath>
        <Device></Device>
        <Pdo></Pdo>
        <ConservationTimeout></ConservationTimeout>
        <PerformanceTimeout></PerformanceTimeout>
        <AccruedIdleTime></AccruedIdleTime>
        <BusyCount></BusyCount>
        <AccruedBusyCount></AccruedBusyCount>
        <IdlePowerState></IdlePowerState>
        <CurrentPowerState></CurrentPowerState>
        <Analysis></Analysis>
    </DeviceIdleEvent>
  </DeviceIdleEvents>
</PwrTestLog> 
```

次の表では、ログ ファイルに表示される XML 要素について説明します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">要素</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><strong>&lt;DeviceIdleEvents&gt;</strong></td>
<td align="left"><p>すべてのデバイスのさまざまなアイドル イベントが含まれています。 1 つだけ <strong>&lt;DeviceIdleEvents</strong> PwrTest ログ ファイルごとの要素。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;タイムスタンプ&gt;</strong></td>
<td align="left"><p>ある特定のイベントのタイムスタンプ。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;InstancePath&gt;</strong></td>
<td align="left"><p>デバイス インスタンスのパス。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;DeviceIdleChangeEvent&gt;</strong></td>
<td align="left"><p>デバイスでは、追加またはイベントを削除します。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;説明&gt;</strong></td>
<td align="left"><p>DeviceRemoved または DeviceDetected します。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;DeviceIdleEvent&gt;</strong></td>
<td align="left"><p>デバイスのアイドル状態の統計情報イベントです。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;デバイス&gt;</strong></td>
<td align="left"><p>機能のデバイス オブジェクト。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;Pdo&gt;</strong></td>
<td align="left"><p>物理デバイス オブジェクト</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;ConservationTimeout&gt;</strong></td>
<td align="left"><p>控えめなタイムアウトが (通常は DC 電源で使用される)。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;PerformanceTimeout&gt;</strong></td>
<td align="left"><p>パフォーマンス (通常は AC 電源で使用される) がタイムアウトしました。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;AccruedIdleTime&gt;</strong></td>
<td align="left"><p>アイドル時間は、期間中に計上されます。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;BusyCount&gt;</strong></td>
<td align="left"><p>デバイス ドライバーが呼び出された回数<a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer" data-raw-source="[&lt;strong&gt;PoSetDeviceBusy&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)"> <strong>PoSetDeviceBusy</strong> </a>期間中にします。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;AccruedBusyCount&gt;</strong></td>
<td align="left"><p>デバイス ドライバーと呼ばれる時間の合計数<a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer" data-raw-source="[&lt;strong&gt;PoSetDeviceBusy&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)"> <strong>PoSetDeviceBusy</strong></a>します。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;IdlePowerState&gt;</strong></td>
<td align="left"><p>アイドル状態になっている数値の状態が表示されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;CurrentPowerState&gt;</strong></td>
<td align="left"><p>現在の数値の電源の状態。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;分析&gt;</strong></td>
<td align="left"><p>期間中の変更点を説明する文字列。</p></td>
</tr>
</tbody>
</table>



## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[PwrTest 構文](pwrtest-syntax.md)










