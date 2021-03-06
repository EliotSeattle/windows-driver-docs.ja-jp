---
title: バグチェック 0x14B SOC_SUBSYSTEM_FAILURE
description: SOC_SUBSYSTEM_FAILURE のバグチェックには、0x0000014B という値が指定されています。 これは、チップ (SoC) サブシステム上のシステムで回復不能なエラーが発生したことを示します。
ms.assetid: CC42D634-90CE-43F1-8552-E5DE711D2117
keywords:
- バグチェック 0x14B SOC_SUBSYSTEM_FAILURE
- バグチェック 0x14B SOC_SUBSYSTEM_FAILURE
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- Bug Check 0x14B SOC_SUBSYSTEM_FAILURE
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 50b51c398a54d1f2ca19ebe0c22c9d3d4735c9cc
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72827239"
---
# <a name="bug-check-0x14b-soc_subsystem_failure"></a>バグチェック 0x14B: SOC\_サブシステム\_エラー


SOC\_サブシステム\_エラーのバグチェックには、0x0000014B という値があります。 これは、チップ (SoC) サブシステム上のシステムで回復不能なエラーが発生したことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターの使用中にブルースクリーンのエラーコードが表示された顧客の場合は、「[ブルースクリーンエラーのトラブルシューティング](https://www.windows.com/stopcode)」を参照してください。


## <a name="bug-check-0x14b-soc_subsystem_failure-parameters"></a>バグチェック 0x14B SOC\_サブシステム\_エラーパラメーター


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
<td align="left"><p><strong><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_soc_subsystem_failure_details" data-raw-source="[SOC_SUBSYSTEM_FAILURE_DETAILS](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_soc_subsystem_failure_details)">SOC_SUBSYSTEM_FAILURE_DETAILS</a></strong>構造体のアドレス。</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>予約済み。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>予約済み。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ホーム フォルダーが置かれているコンピューターにアクセスできない</p></td>
<td align="left"><p>(省略可能)。 ベンダーから提供されたデータブロックのアドレス。</p></td>
</tr>
</tbody>
</table>

 

<a name="resolution"></a>解像度
----------

! [デバッグ拡張機能の[**分析**](-analyze.md)] には、バグチェックに関する情報が表示され、根本原因を特定するのに役立ちます。

```dbgcmd
2: kd> !analyze -v
*******************************************************************************
*                                                                             *
*                        Bugcheck Analysis                                    *
*                                                                             *
*******************************************************************************

SOC_SUBSYSTEM_FAILURE (14b)
A SOC subsystem has experienced an unrecoverable critical fault.
Arguments:
Arg1: 9aa8d630, nt!SOC_SUBSYSTEM_FAILURE_DETAILS
Arg2: 00000000, Reserved
Arg3: 00000000, Reserved
Arg4: a126c000, (Optional) address to vendor supplied general purpose data block.
```

指定された nt を使用します。SOC\_サブシステム\_エラー\_詳細構造を使用して、エラーデータをダンプします。これには、dt コマンドと、Arg1 によって指定されたアドレスを使用します。

```dbgcmd
2: kd> dt nt!SOC_SUBSYSTEM_FAILURE_DETAILS 9aa8d630
   +0x000 SubsysType       : 1 ( SOC_SUBSYS_AUDIO_DSP )
   +0x008 FirmwareVersion  : 0
   +0x010 HardwareVersion  : 0
   +0x018 UnifiedFailureRegionSize : 0x24
   +0x01c UnifiedFailureRegion : [1]  "F"
```

SoC ベンダと連携して、オプションのベンダーが提供している汎用データブロックなど、データをさらに解析します。

[**K、kb、kc、kd、kp、kp、kv (スタックバックトレースの表示)** ](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)コマンドを使用して、スタックトレースを調べることができます。 プロセッサ番号を指定して、すべてのプロセッサのスタックを調べることができます。

また、コード内でこの停止コードまでのブレークポイントを設定し、エラーが発生したコードへのシングルステップフォワードを試行することもできます。

詳細については、以下のトピックを参照してください。

[Windows デバッガー (WinDbg) を使用したクラッシュダンプ分析](crash-dump-files.md)

Windows デバッガーを使用してこの問題に対処することができない場合は、いくつかの基本的なトラブルシューティング手法を使用できます。

-   このバグチェックの原因となっているデバイスまたはドライバーの特定に役立つ可能性のある追加のエラーメッセージについては、イベントビューアーのシステムログを確認してください。

-   バグ チェックのメッセージでドライバーが特定された場合は、そのドライバーを無効にするか、ドライバーの更新状況を製造元に確認します。

-   システムの製造元から提供されているハードウェア診断を実行できます。

-   一般的なトラブルシューティング情報については、「 [**Blue Screen Data**](blue-screen-data.md)」を参照してください。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>サポートされている最小のクライアント</p></td>
<td align="left"><p>Windows 8</p></td>
</tr>
<tr class="even">
<td align="left"><p>サポートされている最小のサーバー</p></td>
<td align="left"><p>Windows Server 2012</p></td>
</tr>
</tbody>
</table>

 

 




