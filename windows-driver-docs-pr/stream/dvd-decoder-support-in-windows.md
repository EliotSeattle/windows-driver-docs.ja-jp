---
title: Windows での DVD デコーダーのサポート
description: Windows での DVD デコーダーのサポート
ms.assetid: 3a77b6d1-6095-4cf8-8cd4-2e6d80d171c8
keywords:
- DVD デコーダー ミニドライバー WDK では、Windows をサポートします。
- デコーダー ミニドライバー WDK DVD では、Windows をサポートします。
- DVD デコーダー ミニドライバー WDK、書き込み
- デコーダー ミニドライバー WDK DVD を書き込む
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b25e03803d53e607152bc98987ca81ceef156b18
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574870"
---
# <a name="dvd-decoder-support-in-windows"></a>Windows での DVD デコーダーのサポート





**注**  このトピックでは、開発者向けです。 DVD デコーダーは、Windows の詳細についてはのソフトウェア デコーダーの一覧を含む記事を参照して、Q306331"[と Windows Vista の Windows XP の Windows Media Player でのソフトウェアの DVD の mpeg-2 デコーダーのサポート](https://go.microsoft.com/fwlink/p/?linkid=3100&ID=306331)、"microsoftナレッジ ベース。

 

DVD デコーダーが Windows 98 ではサポートされている/Me、Windows 2000 以降と以降。

DVD デコーダーのミニドライバーを書き込むようにミニドライバーを含める必要があります、 *ksmedia.h*と*ntddcdvd.h* WDK に用意されているヘッダー ファイル。 ようにミニドライバーにリンクする必要がありますも、 *stream.lib*、 *ks.lib*、 *ksguid.lib*、および*dxapi.lib*ライブラリ。

Windows XP では、下では、次のコンポーネントは、DVD のデコードおよび再生をサポートします。

-   **WDM Stream クラス ドライバー**

    WDM ストリーム クラス ドライバーは、ストリーミング データ型と mpeg-2 と ac-3 のハードウェア デコーダーをサポートします。 詳細については、[ストリーミング ミニドライバー](https://msdn.microsoft.com/library/windows/hardware/ff568275)を参照してください。

**注**  は提供されません mpeg-2 または ac-3 ソフトウェア/ハードウェア Windows XP を備えたデコーダー フィルター。 ベンダーは、必要な各 DVD データ ストリームのいずれか、DirectShow と互換性のあるソフトウェア デコーダーを指定または、その DVD のハードウェア デコーダーをサポートするために WDM ストリーミングと互換性のある DVD デコーダー ミニドライバーを提供する必要があります。

 

-   **DVD ROM クラス ドライバー**

    著作権保護と集中、用のコマンドを含む、DVD-ROM コマンド セットのサポートは、Windows XP では、更新された CD-ROM クラス ドライバーによって提供されます。 このクラス ドライバーは、DVD-ROM ドライブからデータのセクターを読み取る機能を提供します。

-   **UDF ファイル システム**

    NT ベースのオペレーティング システムでは、FAT と NTFS のような UDF インストール可能なファイル システムを提供します。 このインストール可能なファイル システムには、DVD の UDF でフォーマットされたディスクがサポートしています。

-   Microsoft **DirectShow**

    DirectShow フィルターおよび関連するサポート含める DVD ナビゲーター/スプリッター、ビデオ、サブピクチャとオーディオ ストリーム、line21 デコーダー (クローズド キャプション)、ビデオ ミキサー、ビデオの表示機能、およびオーディオのハードウェア デコーダー ミニドライバー インターフェイスのプロキシ フィルターレンダラーです。

    -   DirectShow DVD ナビゲーター/スプリッター フィルター

        DVD/スプリッター ナビゲーター フィルターは、DVD ムービー、保護者、複数の言語に埋め込まれているプログラミング言語を解釈し、ほとんどの DVD に固有のデータ構造を処理します。 このフィルターは、dvd から直接、DVD のストリームを読み取るし、オーディオ、ビデオ、およびサブピクチャなどの個々 のメディアの種類の出力を生成します。 フィルターは、ストリーム内のコマンドに応答し、すべてのユーザー入力を処理します。

    -   プロキシの DirectShow フィルター

        このフィルターでは、WDM 接続とアーキテクチャのプロパティをストリーミングする DirectShow インターフェイスに変換します。 作成されます (つまり、インスタンス化します)、オーディオとビデオのデータ型などのハードウェアでデコードするデータの種類ごとのデバイス オブジェクト。 このフィルターには、新しいインターフェイスの展開を許可するプラグインがサポートされています。

    -   DirectShow のクローズド キャプションのデコード フィルター

        このフィルターは、DVD のビデオ ストリームのクローズド キャプション データをテキスト イメージに変換します。

    -   DirectShow のビデオ ポート マネージャーと表示フィルター

        これらのフィルターは、ハードウェアのビデオ ポートを使用してビデオの再生を有効にして、低帯域幅のビデオ ストリーム、クローズド キャプション デコーダーの出力ストリームをブレンドするためのサポートを提供します。

-   Microsoft **VPE で DirectDraw HAL**

専用のバスでは、ビデオ ストリームのデコードを mpeg-2 デコーダーからディスプレイ カードに転送します。 マイクロソフトは、(VPE) を渡す、ビデオ グラフィックス配列 (VGA) をハードウェアでデコードされたビデオのビデオ ポート拡張子を持つ DirectDraw ハードウェア アブストラクション レイヤー (HAL) を使用してこれらのインターフェイスのソフトウェアのサポートを提供します。 ソフトウェア デコーダーの場合は、VGA にデコードされたビデオを転送する高速のグラフィックスのポート (AGP) バスを使用できます。

-   **著作権保護**

    ディスク上のセクターを暗号化し、それらをデコードする前にそれらのセクターの暗号化を解除して、DVD の著作権保護が提供されます。 コンピューターに存在する、DVD-ROM ドライブを Microsoft が DVD ナビゲーター/スプリッター、監督、デコーダーの間で、認証シーケンスを使用してソフトウェアとハードウェアの両方の decrypters をサポートします。 キーの交換シーケンスは DVD デコーダー ミニドライバーの入力ピンに送信されるプロパティを介して実装されます。

2 つのプライマリ DVD の再生の形式があります。

[ハードウェア ベースの DVD のデコード](hardware-based-dvd-decoding.md)

[DVD のソフトウェア ベースのデコード](software-based-dvd-decoding.md)

次のトピックの要約、DVD デコーダー関連のカーネル プロパティおよびイベントをストリーミングします。

[DVD デコーダーに関連する KS プロパティ](dvd-decoder-related-ks-properties.md)

[DVD デコーダー関連 KS イベント](dvd-decoder-related-ks-events.md)

 

 



