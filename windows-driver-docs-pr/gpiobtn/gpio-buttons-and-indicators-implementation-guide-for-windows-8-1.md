---
title: GPIO のボタンおよびインジケーター実装ガイド
description: Windows 8 では、HID ミニポート クラス ドライバーを使用して、汎用 I/O (GPIO) のボタンとインジケーターのサポートが導入されていました。
ms.assetid: E073E15A-7068-43D0-9DBA-7DD2E7FE2993
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: cce7dd181f2a90555f273e104a7855c6f0ec57bd
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385165"
---
# <a name="gpio-buttons-and-indicators-implementation-guide"></a>GPIO のボタンおよびインジケーター実装ガイド


Windows 8 では、HID ミニポート クラス ドライバーを使用して、汎用 I/O (GPIO) のボタンとインジケーターのサポートが導入されていました。 その目的は、主要なボタン (電源、Windows、ボリューム、回転ロック) の標準化された方法でのサポート、および関連する Windows Engineering Guidance (WEG) を提供することでした。 Windows 8.1 では、エンド ツー エンドのユーザー エクスペリエンスの品質の向上および革新的なさまざまなフォーム ファクター間での動作の統一に重点を置いています。

## <a name="span-idinthissectionspanin-this-section"></a><span id="in_this_section"></span>このセクションの内容


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">トピック</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="state-indicators.md" data-raw-source="[State indicators](state-indicators.md)">状態インジケーター</a></p></td>
<td align="left"><p>このセクションでは、モードとドッキングのインジケーターの状態について説明します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="physical-buttons.md" data-raw-source="[Physical buttons](physical-buttons.md)">物理ボタン</a></p></td>
<td align="left"><p>ハードウェア ボタンを使用して、便利なユーザー インターフェイスの代替手段がない多くの一般的なタスクを実行できます。 このセクションでは対応するシナリオ、ハードウェア ボタンは通常、物理キーボードがコンバーチブルやスレートなどのフォーム ファクターで、ユーザーが利用できるときに発生したタスクの使用します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="interface-implementation-guidance.md" data-raw-source="[Interface implementation guidance](interface-implementation-guidance.md)">インターフェイスの実装のガイダンス</a></p></td>
<td align="left"><p>このセクションでは、インターフェイスの実装のガイダンスを提供します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="code-samples.md" data-raw-source="[Code samples](code-samples.md)">コード サンプル</a></p></td>
<td align="left"><p>このセクションには、コード サンプルとインターフェイスの実装のサンプルの記述子が含まれています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="implement-the-unattended-windows-setup-setting.md" data-raw-source="[Implement the unattended Windows Setup setting](implement-the-unattended-windows-setup-setting.md)">無人 Windows セットアップの設定を実装します。</a></p></td>
<td align="left"><p>このトピックでは、無人 Windows セットアップ コンポーネントの設定を設定する方法について説明します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="logging-and-investigations.md" data-raw-source="[Logging and investigations](logging-and-investigations.md)">ログ記録と調査</a></p></td>
<td align="left"><p>このトピックでは、ログ記録と調査の GPIO 実装について説明します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="running-test-passes.md" data-raw-source="[Running test passes](running-test-passes.md)">実行中のテスト成功</a></p></td>
<td align="left"><p>ミット プラットフォームでは、テストの自動化と調査の対象となる送信される GPIO パターンをカスタマイズするオプションの両方を提供することにより、GPIO ボタンをテストできます。</p></td>
</tr>
</tbody>
</table>

 

Windows 8.1 への投資の一部として、 **msgpio**ボタン ドライバーは、重要な機能強化。

-   調査を高速化ログ記録を拡張します。
-   同期と堅牢性を強化するために、エラー処理が向上します。
-   新しい ConvertibleSlateMode[無人 Windows セットアップ](https://go.microsoft.com/fwlink/p/?linkid=276788)GPIO 以外のラップトップで OEM のイメージのカスタマイズの一部として、モードをラップトップに静的に設定に使用します。

GPIO ボタンとインジケーターの実装に関する質問がある場合に、Microsoft サポート グループに電子メールを送信dockingsupport@microsoft.comします。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック
[電源ボタンの動作と実装](https://aka.ms/connect-redirect?DownloadID=47452)  
[接続されたスタンバイ ウェイク ソース](https://aka.ms/connect-redirect?DownloadID=49891)  
[ACPI 設計ガイド](https://aka.ms/connect-redirect?DownloadID=48755)  
[GetSystemMetrics 関数](https://go.microsoft.com/fwlink/p/?linkid=324686)  
[Windows 8 におけるキーボードの機能拡張](https://go.microsoft.com/fwlink/p/?linkid=324536)  
[Windows ハードウェア互換性プログラム](https://docs.microsoft.com/windows-hardware/design/compatibility/index)  
[Windows デスクトップ アプリ認定要件](https://go.microsoft.com/fwlink/p/?linkid=306131)  
[HID I²C 経由で](https://go.microsoft.com/fwlink/p/?linkid=324690)  
[ミットで GPIO テスト](https://docs.microsoft.com/windows-hardware/drivers/spb/gpio-tests-in-mitt)  
[Windows システム イメージ マネージャー テクニカル リファレンス](https://go.microsoft.com/fwlink/p/?linkid=324691)  
[Windows の無人セットアップに関するリファレンス](https://go.microsoft.com/fwlink/p/?linkid=276788)  
[Windows Driver Kit (WDK) 8.1](https://go.microsoft.com/fwlink/p/?linkid=310164)  



