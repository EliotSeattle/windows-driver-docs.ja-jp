---
title: バグ チェック 0xC000021A STATUS_SYSTEM_PROCESS_TERMINATED
description: STATUS_SYSTEM_PROCESS_TERMINATED のバグ チェックでは、0xC000021A の値を持ちます。 これは、ユーザー モードの重要なサブシステムでエラーが発生したことを意味します。
ms.assetid: d46e2948-ff18-49e0-a738-7b90ab54d333
keywords:
- バグ チェック 0xC000021A STATUS_SYSTEM_PROCESS_TERMINATED
- STATUS_SYSTEM_PROCESS_TERMINATED
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- STATUS_SYSTEM_PROCESS_TERMINATED
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: d9d3aab36b1e048949db804d5ae807f18bbd414e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529416"
---
# <a name="bug-check-0xc000021a-statussystemprocessterminated"></a>バグ チェック 0xC000021A の。ステータス\_システム\_プロセス\_終了


ステータス\_システム\_プロセス\_TERMINATED バグ チェックが 0xC000021A の値を持ちます。 これは、ユーザー モードの重要なサブシステムでエラーが発生したことを意味します。

**重要な**プログラマ向けのトピックです。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。

## <a name="statussystemprocessterminated-parameters"></a>ステータス\_システム\_プロセス\_終了パラメーター


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
<td align="left"><p>この問題を識別する文字列</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>エラー コード</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>予約済み</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>予約済み</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

このエラーは、WinLogon またはクライアント サーバー ランタイム サブシステム (CSRSS) などのユーザー モード サブシステムが致命的に侵害され、セキュリティが保証されることが不要になったときに発生します。 応答では、オペレーティング システムは、カーネル モードに切り替わります。 Microsoft Windows は、WinLogon または CSRSS も実行できません。 そのため、これはユーザー モード サービスの障害は、システムを停止するいくつかのケースの 1 つです。

一致しないシステム ファイルもこのエラーがあります。 これは、ハード ディスクをバックアップから復元した場合に発生します。 一部のバックアップ プログラムでは、使用されているかを決定するシステム ファイルの復元をスキップ可能性があります。

<a name="resolution"></a>解決方法
----------

ユーザー モード プロセスで、実際のエラーが発生したため、カーネル デバッガーを実行しているこのような状況で役に立ちますはありません。

**ユーザー モード デバイス ドライバー、システム サービス、またはサード パーティ製アプリケーションでエラーを解決するには。** ユーザー モード プロセスで 0xC000021A のバグ チェックが発生したため、最も一般的な問題の原因は、サード パーティ製アプリケーションです。 新しいまたは更新されたデバイス ドライバー、システム サービス、またはサード パーティ製アプリケーションのインストール後に、エラーが発生した場合、新しいソフトウェアを削除または原因を特定するため無効にする必要があります。 有効な更新についてソフトウェアの製造元に問い合わせてください。

**一致しないシステム ファイルの問題を解決するには。** バックアップから最近、ハード ディスクを復元した場合は、バックアップ/復元プログラムの更新バージョンは、製造元から入手できることを確認します。

次の手順は、追加情報の収集に役立つ可能性があります。

-   最後にインストールされたアプリケーションを参照してください。 実行するこの移動を「アンインストールまたは変更するプログラム」がインストールされているアプリケーションをコントロール パネルと並べ替えには、インストールの日付。

-   デバイスまたはエラーの原因となっているドライバーの特定に役立つ可能性がある追加のエラー メッセージをイベント ビューアーのシステム ログを確認します。 詳細については、次を参照してください。[イベント ビューアーを開く](https://windows.microsoft.com/windows/what-information-event-logs-event-viewer#1TC=windows-7)します。 ブルー スクリーンに同じ期間に発生したシステム ログの重大なエラーを探します。

次の手順は、この問題の解決に役立つ可能性があります。

-   システム ファイル チェッカー ツールを使用して、欠落または破損システム ファイルを修復します。 システム ファイル チェッカーは、ユーティリティは Windows ユーザーを Windows システム ファイルで破損をスキャンし、復元できるようにするには、ファイルが破損しています。 システム ファイル チェッカー (SFC.exe) ツールを実行するのにには、次のコマンドを使用します。

    ```console
    SFC /scannow
    ```

    詳細については、次を参照してください。[システム ファイル チェッカー ツールを使用してシステム ファイルの欠落または破損の修復](https://support.microsoft.com/kb/929833)します。

-   ウイルス検出プログラムを実行します。 ウイルスに感染する可能性、Windows 用にフォーマットされたハード_ディスクのすべての種類と、結果として得られるディスクの破損は、システムのバグ チェックのコードを生成できます。 ウイルス検出プログラムへの感染マスター ブート レコードのチェックを確認します。

-   システムにインストールされている最新の Service Pack があることを確認します。 どのサービス パックを検出する場合は、いずれかがシステムにインストールされている、 をクリックして**開始**、 をクリックして**実行**、型**winver**、し、ENTER キーを押します。 **について Windows**いずれかがインストールされている場合、Windows のバージョン番号と、サービス パックのバージョン番号をダイアログ ボックスが表示されます。

**セーフ モードを使用します。**

トラブルシューティングのための要素を分離するためのセーフ モードの使用を検討し、Windows を使用するために必要な場合。 セーフ モードを使用して、Windows の起動中に、最低限必要なドライバーとシステム サービスのみを読み込みます。 セーフ モードを入力するを使用して**更新とセキュリティ**で設定します。 選択**Recovery**-&gt;**スタートアップを高度な**メンテナンス モードで起動します。 結果として得られるメニューでは、次のように選択します**トラブルシューティング**- &gt; **オプションの高度な** - &gt; **スタートアップ設定**。 - &gt; **再起動**します。 Windows を再起動した後、**スタートアップ設定**画面で、セーフ モードで起動するには、4、5 または 6 のオプションを選択します。

ブート、f8 キーなどのファンクション キーを押して、セーフ モードを利用できます。 特定のスタートアップ オプションの製造元から情報を参照してください。

 

 



