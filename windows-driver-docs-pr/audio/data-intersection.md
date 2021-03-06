---
title: データ交差
description: データ交差
ms.assetid: a1588ce0-a091-4bfd-98a9-4d78e2fc847f
keywords:
- データ交差ハンドラー WDK オーディオ、データ共通部分
- WDK オーディオのデータ交差
- WDK オーディオの共通部分
- データ範囲の WDK オーディオ
- シンクが WDK オーディオをピン留めする
- ソースピン WDK オーディオ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e5477abf43f8dd27c14ce1e531b1ec30d7c38194
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72833577"
---
# <a name="data-intersection"></a>データ交差


## <span id="data_intersection"></span><span id="DATA_INTERSECTION"></span>


オーディオフィルターグラフでは、2つのピンがストリームに共通の形式をサポートしている場合にのみ、1つのフィルターのソースピンから別のフィルターのシンクピンにオーディオストリームをフローできます。 同様に、クライアントは、フィルターのシンクピンにオーディオストリームを送信したり、クライアントと pin が共通のストリーム形式をサポートしている場合にのみ、フィルターのソースピンからオーディオストリームを受信したりすることができます。 オーディオフィルターでは、データ積集合 (データ範囲の積集合) と呼ばれる手法を使用して、2つのピンまたはクライアントと pin に共通するストリーム形式を識別します。

たとえば、Windows Server 2003、Windows XP、Windows 2000、および Windows Me/98 では、 [sysaudio システムドライバー](kernel-mode-wdm-audio-components.md#sysaudio_system_driver)は、互換性のあるオーディオデータをサポートするフィルターピンのペアを接続することで、データ共通の手法を使用してオーディオフィルターグラフを作成します。83'7d.

[Pin ファクトリ](pin-factories.md)は、各ピンがデータ範囲の配列としてサポートする一連の形式を指定します。各データ範囲は、型[**ksdatarange よって\_AUDIO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksdatarange_audio)型の構造体です。 データ範囲では、一般的な形式の種類を指定します。これは、 [**KSDATAFORMAT\_WAVEFORMATEX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksdataformat_waveformatex)または[**KSDATAFORMAT\_DSOUND**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksdataformat_dsound)にすることができます。 さらに、データ範囲では、次のパラメーターのそれぞれに対して値の範囲を指定します。

-   サンプルあたりのビット数

-   サンプルの頻度

-   チャンネル数

KSK DATARの\_オーディオ構造体は、サンプル単位とサンプル頻度の範囲の最小値と最大値の両方を指定しますが、チャネル数の範囲の最大値のみを指定します。 チャネルの最小数は、暗黙的に1です。

2つの pin の共通データ形式をネゴシエートするジョブは、それぞれが互いに交差する2つのデータ範囲 (各ピンから1つ) を見つけることで構成されます。 次の場合、データ範囲のペアが交差します。

-   同じ一般的な wave 形式 (KSDATAFORMAT\_WAVEFORMATEX または KSDATAFORMAT\_DSOUND) をサポートしています。

-   サンプルごとのビット数の範囲が重複しています。

-   サンプルの頻度の範囲が重複しています。

前述のように、KSDATAFORMAT\_AUDIO 構造は、pin でサポートされるチャネルの最小数が常に1であるハードウェアモデルを意味します。 このモデルによれば、2つのピンのチャネル数の範囲は常に重複しています。両方のピンが少なくとも1つのチャネルをサポートしているためです。 明らかに、少なくとも1つ以上のチャネルがあるハードウェアアダプターは、このモデルに準拠していませんが、アダプタードライバーには、この種の問題に対処するための独自のデータ共通ハンドラーを含めることができます (「独自の例」を参照してください)。 [データの交差ハンドラー](proprietary-data-intersection-handlers.md))。

2つのピンの交差するデータ範囲のペアを見つけると、次のように、ハンドラーは交差領域から共通のデータ形式を選択します。

-   サンプルあたりのビット数は、2ビット/サンプルの範囲が重複する領域から選択されます。

-   サンプル頻度は、2つのサンプル頻度の範囲が重複する領域から選択されます。

-   チャネルの数は、2つのチャネルの範囲が重複する領域から選択されます。

たとえば、オーディオポートドライバーのシンク pin と、別のフィルターのソースピン (通常は[KMixer システムドライバー](kernel-mode-wdm-audio-components.md#kmixer_system_driver)) の共通形式をネゴシエートする場合、sysaudio は最初にソース pin のデータ範囲配列を取得します。 次に、SysAudio は、Ksk プロパティを送信して[ **\_\_DATAINTERSECTION**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-pin-dataintersection)リンクをシンク pin に送信します。この要求には、ソース PIN のデータ範囲配列が含まれます。 カーネルストリーミングレイヤーは、要求をインターセプトし、最初の要素で始まるソースピンのデータ範囲配列内の連続する要素ごとに、ポートドライバーのデータの交差ハンドラーを1回呼び出します。データの積集合。

SysAudio がポートドライバーのデータの交差ハンドラーに対して行う各呼び出しでは、ハンドラーはまず、ミニポートドライバーからシンク pin のデータ範囲配列を取得します。 次に、シンクピンデータ範囲と現在のソースピンデータ範囲の交差部分を見つけるために成功するまで、最初の要素で始まる配列を反復処理します。 ハンドラーは、共通の形式を選択して共通し、この形式を呼び出し元に出力します。

反復処理の各ステップで、ポートドライバーは、2つのピンのそれぞれに1つずつ、2つのデータ範囲を持つミニポートドライバーの独自のデータ交差ハンドラーを呼び出します。 任意の手順で、独自のハンドラーが2つのデータ範囲の間のデータの交差チェックを処理するのを拒否する場合、ポートドライバーのデータ積集合ハンドラーは代わりにチェックを実行します。

要約すると、ソースピンデータ範囲とシンクピンデータ範囲の交差部分の検索は、反復的なプロセスです。

-   外側のループでは、カーネルストリーミングレイヤーは、最初の配列要素から開始して、ソースピンのデータ範囲配列内の連続する要素を反復処理します。

-   内側のループでは、ポートドライバーは、最初の配列要素から開始して、シンク pin のデータ範囲配列内の連続する要素を反復処理します。

検索は、最初のデータの交差部分の検索時に停止します。 このプロセスでは、各 pin のデータ範囲配列の先頭に向かって要素を優先する傾向があります。 ピンのデータ範囲の配列を指定する場合、アダプタードライバーは、優先する形式のデータ範囲を配列の先頭に配置することによって、配列要素を並べ替える必要があります。

 

 




