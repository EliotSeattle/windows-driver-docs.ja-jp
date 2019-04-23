---
title: バグ チェック 0xC0000221 STATUS_IMAGE_CHECKSUM_MISMATCH
description: STATUS_IMAGE_CHECKSUM_MISMATCH のバグ チェックでは、0xC0000221 の値を持ちます。 これは、ドライバーまたはシステム DLL が破損していることを示します。
ms.assetid: d0baccb0-51a2-45c7-ae08-507217d0ac96
keywords:
- バグ チェック 0xC0000221 STATUS_IMAGE_CHECKSUM_MISMATCH
- STATUS_IMAGE_CHECKSUM_MISMATCH
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- STATUS_IMAGE_CHECKSUM_MISMATCH
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 102497f4aa46f83c3658e4d4c99fd530ea2a61c4
ms.sourcegitcommit: fb8b1d2e18dd727e8a479b04c9e6051e7e9fa484
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/18/2019
ms.locfileid: "59238973"
---
# <a name="bug-check-0xc0000221-statusimagechecksummismatch"></a>バグ チェック 0xC0000221:ステータス\_イメージ\_チェックサム\_が一致しません


ステータス\_イメージ\_チェックサム\_の不一致のバグ チェックが 0xC0000221 の値を持ちます。 これは、ドライバーまたはシステム DLL が破損していることを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。


## <a name="statusimagechecksummismatch-parameters"></a>ステータス\_イメージ\_チェックサム\_不一致パラメーター


<a name="cause"></a>原因
-----

このバグは、ドライバーまたはその他のシステム ファイルに重大なエラーからの結果を確認します。 ファイル ヘッダーのチェックサムが予想されるチェックサムと一致しません。

(ディスク エラー、RAM、または破損しているページ ファイル) ファイルの I/O パスにハードウェアの障害が原因の可能性もあります。

<a name="resolution"></a>解決方法
----------

このエラーを解決するには、システム リカバリ ディスク (ERD) を実行し、システムを修復またはシステム パーティションに存在しないか破損しているドライバー ファイルを交換します。

Windows の既存のコピーをインプレース アップグレードを実行することもできます。 これにより、すべてのレジストリ設定と構成については、維持されますが、すべてのシステム ファイルが置き換えられます。 任意のサービス パックや修正プログラムが適用されていたが場合、は、(最新のサービス パックし、後のサービス パックの修正プログラムを最初に、インストールした該当する場合の順序で) 適切な順序で後で再インストールする必要があります。

特定のファイルが破損するいるとバグの確認メッセージで確認された場合は、その個々 のファイルを手動で置き換えることを試行できます。 システム パーティションが FAT でフォーマットされている場合は、MS-DOS 起動ディスクからを起動し、ハード ディスク上に元のソースからファイルをコピーします。 デュアル ブート コンピューターを使っている場合、その他のオペレーティング システムを起動し、ファイルを置換できます。

NTFS パーティションを持つ単一ブート システム上のファイルを置換する場合は、オペレーティング システムに f8 キーを押して、システムを再起動する必要があります**ローダー** ] メニューの [選択**セーフ モードとコマンド プロンプト**します。 そこから、ファイルのハード ディスク上に元のソースからの新しいバージョンをコピーします。 セーフ モードでシステムのスタートアップ プロセスの一環として、ファイルを使用する場合は、ファイルにアクセスするには、回復コンソールを使用してコンピューターを起動する必要があります。 これらのメソッドが失敗した場合は、Windows を再インストールして、バックアップからシステムを復元してください。

**注**  製品 CD から、元のファイルは、ファイル名拡張子で終わる、 \_ (アンダー スコア)、ファイルを圧縮しないことを可能にする前に必要があります。 回復コンソールの**コピー**コマンドは、自動的に圧縮されたファイルを検出し、ターゲットの場所にコピーする際に展開します。 ドライブにアクセスするをセーフ モードを使用している場合は、使用、**展開**コマンドを解凍し、ターゲット フォルダーにファイルをコピーします。 使用することができます、**展開**セーフ モードのコマンドライン環境でコマンド。

 

**ディスク エラーの問題を解決するには。** ディスクのエラーは、ファイルの破損のソースを指定できます。 実行**Chkdsk/f/r**を検出し、ファイル システム構造的な破損を解決します。 システム パーティションにディスクのスキャンが開始する前に、システムを再起動する必要があります。

**RAM の問題を解決するには。** RAM がシステムに追加した直後に、エラーが発生した場合は、ページング ファイルが壊れている可能性があります。 または新しい RAM そのものは、障害があるか、互換性のない可能性があります。

**バグ チェックが原因となっている RAM を新しく追加されたかを判断するには**

1.  RAM の元の構成に、システムを返します。

2.  回復コンソールを使用して、ページング ファイルが含まれるパーティションへのアクセスをファイル pagefile.sys を削除します。

3.  回復コンソールで引き続き実行**Chkdsk/r**ページング ファイルに含まれるパーティションにします。

4.  システムを再起動します。

5.  ページング ファイルを追加の RAM の量に対して最適なレベルに設定します。

6.  システムをシャット ダウンし、RAM を追加します。

    新しい RAM は、速度、parity、および型 (つまり、高速ページ モード (FPM) と同期の動的なランダム アクセス メモリ (SDRAM) と (エド語) を拡張データ) のシステムの製造元の仕様を満たす必要があります。 可能な限り既存のインストールされている ram の容量を新しい RAM を照合しようとしてください。 RAM は、さまざまな形式 (1 つのインライン メモリ モジュール--SIMM--またはデュアル インライン メモリ モジュール--DIMM) で、多くのさまざまな容量と、さらに重要なを取得できます。 これらの種類の連絡先を混在させることは避けて、電気の連絡先は gold または要素のいずれかにできます。

新しいメモリを再インストール後に、同じエラー メッセージが発生した場合は、メモリのスキャナーでは特に、システムの製造元によって提供されるハードウェア診断を実行します。 詳細については、これらの手順は、コンピューターの製造元のマニュアルを参照してください。

ログオンするとは、システムにもう一度、デバイスや、エラーの原因となっているドライバーの特定に役立つ可能性がある追加のエラー メッセージをイベント ビューアーのシステム ログを確認します。

BIOS のメモリ キャッシュを無効にすると、このエラーも解決可能性があります。

 

 



