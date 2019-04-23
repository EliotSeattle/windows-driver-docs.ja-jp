---
title: 拡張可能な Wave 形式の記述子
description: 拡張可能な Wave 形式の記述子
ms.assetid: b80e651b-fb97-4502-8526-e844425805dc
keywords:
- wave 形式の記述子の WDK オーディオ
- PCM の形式の WDK オーディオ
- wave 形式のタグの WDK オーディオ
- wave ストリーム WDK オーディオ
- オーディオ データ形式 WDK
- データ形式の WDK オーディオ、wave 形式の記述子
- WDK のオーディオ、wave 形式の記述子を書式設定します。
- KSDATAFORMAT 構造体
- KMixer システム ドライバー WDK オーディオ、wave 形式記述子
- WAVEFORMATEXTENSIBLE
- WAVEFORMATEX 構造体
- オーディオ データ形式の WDM WDK
ms.date: 10/27/2017
ms.localizationpriority: medium
ms.openlocfilehash: ec15f1f408f9b09e32e3b1bd14bb44a4404529e6
ms.sourcegitcommit: d334150abe0b189faf33049908af7aab1458c13d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2019
ms.locfileid: "57464318"
---
# <a name="extensible-wave-format-descriptors"></a>拡張可能な Wave 形式の記述子


## <span id="extensible_wave_format_descriptors"></span><span id="EXTENSIBLE_WAVE_FORMAT_DESCRIPTORS"></span>


Wave オーディオ ストリームのデータ形式の記述子の図は、次のとおりです。

![wave 形式の記述子を示す図](images/wavefmt.png)

その他の量が次の情報を書式設定の図に示されるように、 [ **KSDATAFORMAT** ](https://msdn.microsoft.com/library/windows/hardware/ff561656)構造体は、データ形式によって異なります。

オーディオのシステムでは、いくつかの方法でこの種類の形式の記述子を使用します。

-   上記の図に示すように 1 つは、ミニポート ドライバーに、呼び出しのパラメーターとして渡されるような形式の記述子**NewStream**メソッド (たとえばを参照してください[ **IMiniportWaveCyclic::NewStream**](https://msdn.microsoft.com/library/windows/hardware/ff536723)).

-   *ResultantFormat*のパラメーター、 [ **IMiniport::DataRangeIntersection** ](https://msdn.microsoft.com/library/windows/hardware/ff536764)など、1 つのメソッドが書式記述子を書き込む先バッファーへのポインターをメソッド上記の図に示します。

-   [ **KSPROPERTY\_PIN\_DATAINTERSECTION** ](https://msdn.microsoft.com/library/windows/hardware/ff565198)プロパティの get 要求を上記の図に示すような形式の記述子を取得します。

-   [ **KSPROPERTY\_PIN\_PROPOSEDATAFORMAT** ](https://msdn.microsoft.com/library/windows/hardware/ff565206)プロパティの設定要求は、上記の図に示すような形式の記述子を受け入れます。

-   ような形式を使用、 [ **KsCreatePin** ](https://msdn.microsoft.com/library/windows/hardware/ff561652)関数の*Connect*パラメーターを呼び出します。 このパラメーターが指す、 [ **KSPIN\_CONNECT** ](https://msdn.microsoft.com/library/windows/hardware/ff563531)書式記述子が含まれているバッファーの先頭に構造体。 形式の記述子の直後に、KSPIN\_構造体を接続し、前の図に示すような KSDATAFORMAT 構造から始まります。

KSDATAFORMAT 構造を次の形式の情報はいずれかになります、 [ **WAVEFORMATEXTENSIBLE** ](https://msdn.microsoft.com/library/windows/hardware/ff538802)構造または[ **WAVEFORMATEX** ](https://msdn.microsoft.com/library/windows/hardware/ff538799)構造体。 WAVEFORMATEXTENSIBLE は、WAVEFORMATEX よりも広い範囲の形式を記述できます WAVEFORMATEX の拡張バージョンです。 WAVEFORMATEX は、事前 WDM WAVEFORMAT 構造体の拡張バージョンです。 WAVEFORMAT は廃止され、Microsoft Windows の任意のバージョンで WDM オーディオ サブシステムでサポートされていません。

同様に、PCMWAVEFORMAT 構造体は、廃止、ですが、制限付きサポートを提供する WDM オーディオ サブシステム WAVEFORMAT の拡張バージョンです。

WAVEFORMAT と PCMWAVEFORMAT については、Microsoft Windows SDK のドキュメントを参照してください。

次の 4 つ wave 形式の構造体--以降では、同じ 5 つメンバーで始まるすべて WAVEFORMAT、PCMWAVEFORMAT、WAVEFORMATEX、および WAVEFORMATEXTENSIBLE-- **wFormatTag**します。 上記の図は、これらが同一である構造体の一部を強調表示を互いに重なって表示される 4 つの構造を示します。 PCMWAVEFORMAT と WAVEFORMATEX WAVEFORMAT の拡張を追加して、 **wBitsPerSample** 、メンバーが WAVEFORMATEX も追加、 **cbSize**メンバー。 WAVEFORMATEXTENSIBLE 以降では、3 つのメンバーを追加することにより、WAVEFORMATEX を拡張**サンプル**.wValidBitsPerSample します。 (**サンプル**その他のメンバーを共用体には**wValidSamplesPerBlock**の代わりに使用が**wValidBitsPerSample**いくつかの形式と圧縮します)。**WFormatTag**バッファーに KSDATAFORMAT 構造の末尾の直後に、メンバーは、どのような形式の情報に依存して KSDATAFORMAT を指定します。 [KMixer システム ドライバー](kernel-mode-wdm-audio-components.md#kmixer_system_driver)の次の表に示す 3 つの形式のタグのいずれかを使用している PCM 形式のみをサポートしています。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">wFormatTag 値</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>WAVE_FORMAT_PCM</p></td>
<td align="left"><p>WAVEFORMATEX または PCMWAVEFORMAT で指定された整数 PCM のデータ形式。</p></td>
</tr>
<tr class="even">
<td align="left"><p>WAVE_FORMAT_IEEE_FLOAT</p></td>
<td align="left"><p>WAVEFORMATEX で指定された浮動小数点の PCM のデータ形式。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>WAVE_FORMAT_EXTENSIBLE</p></td>
<td align="left"><p>WAVEFORMATEXTENSIBLE で指定された拡張データ形式。</p></td>
</tr>
</tbody>
</table>

 

実際には、KMixer は、これらのタグ値で記述できる PCM 形式のサブセットのみをサポートしています (と PCM 以外の形式をサポートしていません)。 USB オーディオ デバイス (を参照してください[USBAudio クラスのシステム ドライバー](kernel-mode-wdm-audio-components.md#usbaudio_class_system_driver)) すべての PCM 形式の USB オーディオ ストリームを通過 KMixer のために、このサブセットに制限されます。 (一部の PCM USB オーディオ ストリームが KMixer; をバイパスできる詳細については、次を参照してください[形式の非 PCM の USB オーディオ サポート](usb-audio-support-for-non-pcm-formats.md)。)。ただし、この Windows XP 以降では、DirectSound のアプリケーションは KMixer でサポートされていない形式をサポートする WaveCyclic および WavePci のデバイスのハードウェアのピンに直接接続して KMixer の制限を克服できます。 詳細については、[WDM オーディオでハードウェア アクセラレータを DirectSound](directsound-hardware-acceleration-in-wdm-audio.md)を参照してください。

波の意味ではあいまい\_形式\_PCM タグ値 WAVEFORMATEX または PCMWAVEFORMAT のいずれかの構造上の表で指定できます。 ただし、これら 2 つの構造はほぼ同じです。 唯一の違いは、WAVEFORMATEX が含まれている、 **cbSize**メンバーと PCMWAVEFORMAT しません。 WAVEFORMATEX の仕様に従って**cbSize**場合は無視されます**wFormatTag** = WAVE\_形式\_PCM (ため**cbSize**は暗黙的にゼロ)。**cbSize**はその他の形式を使用します。 したがって、PCM 形式の場合 PCMWAVEFORMAT WAVEFORMATEX 同じ情報が含まれます、同じように扱うことができます。

WAVEFORMATEX WAVEFORMATEXTENSIBLE が指定できる形式のサブセットのみを指定できます。 WAVEFORMATEX とは異なり WAVEFORMATEXTENSIBLE は、次の操作を行うことができます。

1.  サンプル コンテナーのサイズから個別にサンプルあたりのビット数を指定します。 たとえば、20 ビット サンプルは、左揃えの 3 バイトのコンテナー内で格納できます。 WAVEFORMATEX、サンプル コンテナーのサイズからサンプル データ ビット数を区別するために失敗した場合、これは、このような形式を明確に記述することができません。

2.  マルチ チャネル ストリームにオーディオ チャンネルには、特定の speaker の場所を割り当てます。 WAVEFORMATEX では、この機能がないし、ステレオのみ mono と (2 つのチャネル) のストリームを適切にサポートすることができます。

WAVEFORMATEXTENSIBLE によって WAVEFORMATEX によって定義された任意の形式を記述できます。 WAVEFORMATEXTENSIBLE WAVEFORMATEX 構造体に変換する方法の詳細については、[形式のタグの間で変換およびサブフォーマット Guid](converting-between-format-tags-and-subformat-guids.md)を参照してください。

WAVEFORMATEX はサンプル サイズが 8 または 16 ビットの形式を記述するためだけで十分ですが、WAVEFORMATEXTENSIBLE サンプル有効桁数の 16 ビットを超える形式を適切に記述する必要があります。 2 つの例を次に示します。

-   24 ビットのサンプルの有効桁数を持つストリームは、効率的に処理、32 ビットのコンテナー サイズを使用できますが、24 ビット コンテナーを使用してデータを失うことがなく、ストレージ効率の向上に変換できます。

-   24 ビットのサンプル データのストリームを処理するときに精度の 20 ビットのみを提供するレンダリング デバイスはディザリングその出力信号の忠実性を向上させるために使用することができます。 ディザリング、ただし、追加の処理時間を必要として、元のストリームが 20 ビットのみに正確な場合は、追加の処理が必要ではありません。

これらの例の両方では、処理、および記憶域の効率の適切なトレードオフを行うときに、信号の品質を維持しサンプル有効桁数とコンテナーのサイズがわかっている場合にのみ可能性があります。

単純な形式は、WAVEFORMATEX または WAVEFORMATEXTENSIBLE 構造体のいずれかを明確に説明されていることができます、オーディオ ドライバーは形式を記述するいずれかの構造を選択するオプションが。 ただし、オーディオ ドライバーが 8 ビットまたは 16 ビットのサンプルのステレオの PCM 形式の mono と (2 つのチャネル) を指定 WAVEFORMATEX を通常使用される、一部の古いアプリケーションが期待 WAVEFORMATEX を使用して、これらの形式を指定するすべてのオーディオ ドライバー。

ドライバーは、2 つの構造のうちのどのクライアント アプリケーションまたはコンポーネントで使用する形式を指定するを認識する必要があります、ドライバー、WAVEFORMATEX または WAVEFORMATEXTENSIBLE 構造体のいずれかとして明確に指定できるオーディオ形式をサポートする場合構造体。 たとえば、オーディオ デバイスは、44.1 kHz 16 ビット、ステレオの PCM 形式をサポートする場合に、ミニポート ドライバーの KSPROPERTY\_PIN\_PROPOSEDATAFORMAT プロパティ ハンドラーとその実装の**NewStream**メソッドは、WAVEFORMATEX または WAVEFORMATEXTENSIBLE 構造と形式を指定するかどうかに関係なく、その形式を受け入れる必要があります。

形式のデータの処理を簡素化するには、ドライバーは通常を内部的に形式を表す WAVEFORMATEXTENSIBLE 構造体を使用します。 このアプローチには、入力の WAVEFORMATEX 構造体の内部の WAVEFORMATEXTENSIBLE 表現への変換または内部 WAVEFORMATEXTENSIBLE 表現出力 WAVEFORMATEX 構造体への変換を必要があります。

場合に WAVEFORMATEXTENSIBLE、WAVEFORMATEX から書式記述子を変換するときに、 **wFormatTag** WAVEFORMATEX 構造体のメンバーは、WAVE\_形式\_PCM または WAVE\_形式\_IEEE\_FLOAT、設定、 **dwChannelMask**どちらのスピーカーに WAVEFORMATEXTENSIBLE 構造体のメンバー\_フロント\_講演者、または (mono ストリーム) センター\_フロント\_左 |スピーカー\_フロント\_権利 (ステレオ ストリーム) をします。 スピーカー\_フロント\_*XXX*定数 Ksmedia.h のヘッダー ファイルで定義されています。

Windows 98"Gold"を除くすべての Windows リリースでは、KMixer は、複数のチャネルがあるし、サンプルあたり最大 32 ビットを持つ WAVEFORMATEXTENSIBLE PCM の範囲の形式をサポートします。

WAVEFORMATEX PCM のサブセットでは、ある KMixer サポートの間で異なれば Windows リリースでは、次の表に示すように書式設定します。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Windows のリリース</th>
<th align="left">パックされたサンプルのサイズ</th>
<th align="left">チャネルの数</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>Windows 98"Gold"</p></td>
<td align="left"><p>8、16、24、および 32 ビット</p></td>
<td align="left"><p>マルチチャネル</p></td>
</tr>
<tr class="even">
<td align="left"><p>Windows 98 SE</p></td>
<td align="left"><p>8 および 16 ビットのみ</p></td>
<td align="left"><p>Mono とステレオのみ</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Windows 98 SE + 修正プログラム</p></td>
<td align="left"><p>8、16、24、および 32 ビット</p></td>
<td align="left"><p>Mono とステレオのみ</p></td>
</tr>
<tr class="even">
<td align="left"><p>Windows 2000</p></td>
<td align="left"><p>8 および 16 ビットのみ</p></td>
<td align="left"><p>Mono とステレオのみ</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Windows Me</p></td>
<td align="left"><p>8、16、24、および 32 ビット</p></td>
<td align="left"><p>Mono とステレオのみ</p></td>
</tr>
<tr class="even">
<td align="left"><p>Windows XP 以降</p></td>
<td align="left"><p>8 および 16 ビットのみ</p></td>
<td align="left"><p>Mono とステレオのみ</p></td>
</tr>
</tbody>
</table>

 
WAVEFORMATEXTENSIBLE で**dwBitsPerSample**はコンテナーのサイズと**wValidBitsPerSample**は有効なデータ サンプルごとのビット数です。 コンテナーが、メモリ内のバイト境界で常に、コンテナーのサイズは 8 ビットの倍数として指定する必要があります。

WAVEFORMATEXTENSIBLE 構造が定義されている場合、前に、ベンダーは、公式の 16 ビットの形式のタグは、書式に割り当てることができるように、マイクロソフトの各新規 wave 形式を登録する必要があります。 (形式のタグ、 **wFormatTag** WAVEFORMATEX 構造体のメンバーです)。パブリック ヘッダー ファイル Mmreg.h で登録されている形式のタグの一覧が表示されます (たとえば、WAVE\_形式\_MPEG)。

WAVEFORMATEXTENSIBLE の形式を登録する必要はなくなりました。 ベンダーできる個別に Guid に割り当て、新しい形式に応じて。 (に GUID が含まれている形式、**サブフォーマット**WAVEFORMATEXTENSIBLE のメンバーです)。Microsoft では、最も一般的な形式でパブリック ヘッダー ファイル Ksmedia.h Guid の一覧表示 (たとえば、KSDATAFORMAT\_サブタイプ\_MPEG)。 新しい形式の GUID を定義する前に、ベンダーが KSDATAFORMAT の一覧を確認する必要があります\_サブタイプ\_*XXX*で特定の適切な GUID は既に定義されているかどうかを判断する Ksmedia.h 定数形式です。

WAVEFORMATEXTENSIBLE を使用する場合は、設定**wFormatTag** WAVE に\_形式\_拡張と**サブフォーマット**を適切な形式の GUID。 PCM の整数形式設定**サブフォーマット**KSDATAFORMAT に\_サブタイプ\_PCM。 浮動小数点数としてサンプルの値をエンコードする PCM 形式の場合、次のように設定します。**サブフォーマット**KSDATAFORMAT に\_サブタイプ\_IEEE\_FLOAT です。 これらの形式のいずれか、次のように設定します。 **cbSize**に**sizeof**(WAVEFORMATEXTENSIBLE)**- sizeof**(WAVEFORMATEX)。 PCM 以外のデータ形式を記述する WAVEFORMATEXTENSIBLE の使用方法の詳細については、[非 PCM Wave 形式のサポート](supporting-non-pcm-wave-formats.md)を参照してください。

 

 



