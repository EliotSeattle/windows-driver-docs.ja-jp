---
title: オーディオのエンドポイント、プロパティ、およびイベント
description: オーディオのエンドポイント、プロパティ、およびイベント
ms.assetid: ffc5834f-30c8-40b5-b57b-fe784331690c
keywords:
- オーディオ イベント WDK
- WDK のオーディオのプロパティ
- ポート ドライバー WDK のオーディオ、プロパティ
- ポート ドライバー WDK のオーディオ、イベント
- アダプターのドライバー WDK のオーディオ、イベント
- アダプターのドライバー WDK のオーディオ、プロパティ
- オーディオのプロパティに関するプロパティ、WDK オーディオ
- オーディオのイベントについてイベント WDK、オーディオ
- WDM WDK オーディオのプロパティ
- WDM オーディオ イベント WDK
- WDM オーディオ プロパティ WDK、オーディオのプロパティについて
- KS プロパティ WDK オーディオ
- KS イベント WDK オーディオ
- WDK オーディオのプロパティ
- ピンの WDK オーディオ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c43919ff22e8025b3aeb3feba6a21a4315be8298
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355697"
---
# <a name="audio-endpoints-properties-and-events"></a>オーディオのエンドポイント、プロパティ、およびイベント


## <span id="audio_properties_and_events"></span><span id="AUDIO_PROPERTIES_AND_EVENTS"></span>


PortCls システム ドライバーが記載されている組み込みの操作のサブセットをサポート[KS プロパティ、イベント、およびメソッド](https://docs.microsoft.com/windows-hardware/drivers/stream/ks-properties--events--and-methods)します。

Portcls.sys でポート ドライバーがサポートのいくつかのプロパティとイベントの要求ハンドラーを提供することで、ミニポート ドライバーのハンドラーには、他の要求を転送することによってプロパティおよびイベント。

WaveCyclic、WavePci、MIDI、および Dmu ポート ドライバーの現在の実装は、以下を説明します。

-   フィルター、pin、およびノードのプロパティのサポート

-   Pin とノード上のイベントのイベントをフィルターではなくサポート

クライアントは、プロパティまたはイベントの要求のターゲットとしてフィルターまたは暗証番号 (pin) のインスタンスへのハンドルを指定できます。 ノードのプロパティまたはイベントの要求では、フィルターまたは暗証番号 (pin) のハンドルだけでなく、ノード ID を指定します。 詳細については、次を参照してください。[フィルター、Pin、およびノードのプロパティ](filter--pin--and-node-properties.md)します。

トポロジのポート ドライバーは次のよう

-   フィルターとそのノードのプロパティのサポート

-   ノード上のイベントのサポート

トポロジのフィルターのピンは、完全に存在し、したがってことはできませんをインスタンス化したり削除する有線接続を表します。

ポート ドライバーは、か、フィルターまたはそのピンとノード上のメソッドをサポートを提供します。 ポートのドライバーは、メソッドの要求を処理しないでくださいと、これらの要求を処理するためのミニポート ドライバーを転送しません。

オーディオのアダプターのドライバーでは、次の標準的なプロパティ セットの一部またはすべてをサポートします。

[KSPROPSETID\_AC3](https://docs.microsoft.com/windows-hardware/drivers/audio/kspropsetid-ac3)

[KSPROPSETID\_音響\_エコー\_キャンセル](https://docs.microsoft.com/windows-hardware/drivers/audio/kspropsetid-acoustic-echo-cancel)

[KSPROPSETID\_オーディオ](https://docs.microsoft.com/windows-hardware/drivers/audio/kspropsetid-audio)

[KSPROPSETID\_DirectSound3DBuffer](https://docs.microsoft.com/windows-hardware/drivers/audio/kspropsetid-directsound3dbuffer)

[KSPROPSETID\_DirectSound3DListener](https://docs.microsoft.com/windows-hardware/drivers/audio/kspropsetid-directsound3dlistener)

[KSPROPSETID\_DrmAudioStream](https://docs.microsoft.com/windows-hardware/drivers/audio/kspropsetid-drmaudiostream)

[KSPROPSETID\_全般](https://docs.microsoft.com/windows-hardware/drivers/stream/kspropsetid-general)

[KSPROPSETID\_Hrtf3d](https://docs.microsoft.com/windows-hardware/drivers/audio/kspropsetid-hrtf3d)

[KSPROPSETID\_ジャック](https://docs.microsoft.com/windows-hardware/drivers/audio/kspropsetid-jack)

[KSPROPSETID\_暗証番号 (pin)](https://docs.microsoft.com/windows-hardware/drivers/stream/kspropsetid-pin)

[KSPROPSETID\_シンセサイザー](https://docs.microsoft.com/windows-hardware/drivers/audio/kspropsetid-synth)

[KSPROPSETID\_シンセサイザー\_Dls](https://docs.microsoft.com/windows-hardware/drivers/audio/kspropsetid-synth-dls)

[KSPROPSETID\_TopologyNode](https://docs.microsoft.com/windows-hardware/drivers/audio/kspropsetid-topologynode)

すべてのオーディオ ドライバーのサポート、 **KSPROPSETID\_オーディオ**プロパティ セット。

オーディオのアダプターのドライバーによっては、次のイベント セットをサポートします。

[KSEVENTSETID\_AudioControlChange](https://docs.microsoft.com/windows-hardware/drivers/audio/kseventsetid-audiocontrolchange)

さらに、オーディオのアダプターのドライバーは Ksmedia.h のヘッダー ファイルで定義されているその他のプロパティ セットのプロパティのハンドラーを提供する無料です。 ドライバーがまたを定義して独自のカスタム プロパティとイベントのセットをサポートしますが、カスタム プロパティまたはイベントについて認識しているアプリケーションのみが使用できます。

このセクションでは、オーディオ固有のプロパティとイベントについて説明します。 このガイドには、次のトピックがあります。

[オーディオのプロパティの要求](audio-property-requests.md)

[フィルター、Pin、およびノードのプロパティ](filter--pin--and-node-properties.md)

[オーディオのプロパティのハンドラー](audio-property-handlers.md)

[オーディオのプロパティに対する基本的なサポート クエリ](basic-support-queries-for-audio-properties.md)

[オーディオ エンドポイント ビルダー アルゴリズム](audio-endpoint-builder-algorithm.md)

[動的サブデバイス登録および登録解除](dynamic-subdeviceregistration-and-unregistration.md)

[マルチ チャネルのノードを公開します。](exposing-multichannel-nodes.md)

[暗証番号 (pin) カテゴリのプロパティ](pin-category-property.md)

[エンドポイントのオーディオ デバイスのフレンドリ名](friendly-names-for-audio-endpoint-devices.md)

[オーディオの位置プロパティ](audio-position-property.md)

[データ範囲は、プロパティの積集合をピン留め](pin-data-range-and-intersection-properties.md)

[Jack の Description プロパティ](jack-description-property.md)

[マイク配列 Geometry プロパティ](microphone-array-geometry-property.md)

[ハードウェア イベント](hardware-events.md)

 

 




