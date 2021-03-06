---
title: スピーカー構成の設定を適用
description: スピーカー構成の設定を適用
ms.assetid: 98fe96cc-8436-4400-9b39-86d188e085c9
keywords:
- 失敗したスピーカー構成要求の WDK オーディオ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4d784b07b048aeb3e56329831de24d9922f1ceaf
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355758"
---
# <a name="applying-speaker-configuration-settings"></a>スピーカー構成の設定を適用


## <span id="applying_speaker_configuration_settings"></span><span id="APPLYING_SPEAKER_CONFIGURATION_SETTINGS"></span>


**注**  この情報は、Windows XP およびそれ以前のオペレーティング システムに適用されます。 以降、Windows Vista で**IDirectSound::GetSpeakerConfig**と**IDirectSound::SetSpeakerConfig**非推奨とされました。

 

DirectSound は、レジストリの現在のスピーカーの構成設定を追跡し、その設定のオーディオ ハードウェアに毎回デバイスが作成される新しい DirectSound を適用します。

アプリケーション プログラムは呼び出すことでシステム全体のスピーカーの構成を変更することができます、 **IDirectSound::SetSpeakerConfig**メソッドで、レジストリのスピーカーの構成設定を更新します。 メソッドは、またオーディオ デバイスは、一般に、DirectSound オブジェクトが存在する場合は、スピーカーの設定を変更することはありませんが、新しい設定は直ちに、ハードウェアを適用しようとします。 DirectSound は、このメソッドを定義するスピーカー構成の一覧は、次を参照してください。[スピーカー構成要求の変換](translating-speaker-configuration-requests.md)します。

ユーザーは、スピーカーの構成 ダイアログを使用して、構成を変更できる、**マルチ メディアのプロパティ**コントロール パネルの ページ (mmsys.cpl)。 Windows XP で、DirectSound のスピーカー構成ダイアログ ボックスを見つけるには、これらの手順をなどに従います。

1.  コントロール パネルで、ダブルクリック、**サウンドとオーディオ デバイス**アイコン。

2.  **オーディオ** タブからデバイスを選択、**音の再生**一覧。

3.  **[詳細設定]** ボタンをクリックします。

4.  をクリックして、**スピーカー**タブ。

この時点では、ラベルを表示する必要があります**スピーカーのセットアップ**から選択できるスピーカー構成の一覧の横にあります。

DirectSound を使用して、 [ **KSPROPERTY\_オーディオ\_チャネル\_CONFIG** ](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-audio-channel-config) 3D ノードまたは DAC にスピーカー構成情報を送信する要求をプロパティの設定ノード ([**KSNODETYPE\_3D\_効果**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-3d-effects)または[ **KSNODETYPE\_DAC** ](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-dac)) オーディオ フィルター グラフ。 3D のノードのプロパティの要求の対象を実際には pin です (3 D ストリーム オブジェクト) フィードをノード。 DAC のノードでは、ターゲットは、DAC のノードを含むフィルター オブジェクトです。 いずれの場合も、スピーカーの構成設定はグローバルであり、オーディオ デバイス全体に影響を与えます。 以降を実行しているすべてのオーディオ アプリケーションは、DirectSound の設定が変更されるまで、新しい設定の対象がもう一度です。

Windows Me に付属し、Windows XP 以降、スピーカー構成プロパティに要求を送信 DAC ノード--DirectSound の以前のバージョン、DirectSound の唯一のバージョンは、この機能をサポートしないことに注意してください。 ただし、DirectSound のすべてのバージョンでは、3 D のノードにこれらの要求を送信します。

アプリケーション プログラムには、3 D の 1 つ以上のノードが作成、DirectSound は作成する最初の 3D ノードにのみスピーカー構成要求を送信します。

DirectSound は、3 D をスピーカー構成要求を送信し、DAC のノードごとにアプリケーションを作成、DirectSound オブジェクトまたは呼び出し、 **IDirectSound::SetSpeakerConfig**メソッド。 オーディオ デバイスは、一般に、作業中のストリームを管理しているし、DirectSound 可能であれば、この制限を回避しようとするときに、スピーカーの構成を変更することではありません。 たとえば、DirectSound オブジェクトを作成するときに、フィルターをインスタンス化した後は、ストリームを作成する前に、- フィルターのピンをインスタンス化する前に DirectSound にはスピーカー構成要求が送信します。

この制限はへの呼び出しの場合を回避することが難しく、 **SetSpeakerConfig**します。 アプリケーションを呼び出すと**SetSpeakerConfig**アダプターのドライバーは、DirectSound のスピーカー構成要求を通常が失敗します。 DirectSound オブジェクトが既に存在するデバイスが既にアクティブなストリームを管理することを意味するためです。

アダプター ドライバーではこのような状況で障害が発生したスピーカー構成要求を処理するための 2 つのオプションがあります。

-   ドライバーでは、要求された構成を保存でき、そのすべてのストリームが破棄されるとすぐ、それを適用することができます。

-   ドライバーは、要求を無視し、次回 DirectSound オブジェクトが作成された別のスピーカー構成要求を送信する DirectSound に依存します。

最初のオプションは、ユーザーは、スピーカーの構成 ダイアログで新しい設定を選択する場合、変更はすぐに有効 DirectSound アプリケーションだけでなく--すべてのアプリケーションであるために、優れたユーザー エクスペリエンスを示します。 (もちろん、すべてのオーディオ アプリケーションを新しい設定が選択されている時に実行している場合、変更は延期されますオーディオのすべてのアプリケーションを終了するまで。)2 番目のオプションでは、ただし、変更は反映されません DirectSound アプリケーションが実行されるまで。 たとえば、Windows のマルチ メディア waveOut API を使用するアプリケーションがコントロール パネルの設定を変更した後に実行する最初のアプリケーションの場合は、ユーザー疑問に思う理由、新しい設定には影響を及ぼさずがありません。

3D または DAC のノードに送信されるスピーカー構成要求に応答してでは、通常のアダプターのドライバーは、オーディオのアプリケーションで現在インスタンス化される pin はない場合にのみに、スピーカーのオーディオ ハードウェアの構成を更新します。 つまり、waveOut アプリケーションがなどが 1 つまたは 2 つ目のアプリケーションの呼び出し時に複数の pin を開く場合**DirectSoundCreate**ドライバーは、スピーカーのオーディオ デバイスの保留中の変更を遅延する必要があります後で構成します。

ドライバーは、デバイスのスピーカーの構成を変更する要求を満たすためにできない場合、要求が失敗だけです。 DirectSound オブジェクトの作成時にスピーカー構成要求を失敗または**SetSpeakerConfig**呼び出しでは、DirectSound オブジェクトの作成は発生しませんまたは**SetSpeakerConfig**呼び出しを失敗します。

ブート時に、オーディオ ドライバーにはハードウェアのスピーカーの構成を通常のステレオである、既定の設定を初期化します。 任意のアプリケーションでは、DirectSound オブジェクトを作成するとすぐに、DirectSound には、ハードウェアをレジストリに格納されている設定が適用されます。 呼び出すことが前に、アプリケーション プログラムは DirectSound デバイスを作成する必要があります**SetSpeakerConfig**レジストリがこのレジストリのスピーカーの構成設定を変更する通常の設定を反映のハードウェアにした場合のみDirectSound デバイスが解放され、2 番目の DirectSound デバイスが作成されます。

オーディオ デバイスまたはスピーカー構成エラーの発生をインストールした後は、すぐには、ステレオ DirectSound スピーカーの構成が既定値です。

 

 




