---
title: 汎用ドライバー ペア モデルとしての KMDF
description: このトピックでは、汎用的なドライバー ペアのモデルと見なすことのできるカーネル モード ドライバー フレームワーク (KMDF) の概念について説明します。
ms.assetid: C05E3017-0F1A-49D7-8EAD-0DC44351A39A
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3fb7c4c0d0c87db0ae03d092239b6ed0182098eb
ms.sourcegitcommit: 5598b4c767ab56461b976b49fd75e4e5fb6018d2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2020
ms.locfileid: "63371286"
---
# <a name="kmdf-as-a-generic-driver-pair-model"></a>汎用ドライバー ペア モデルとしての KMDF


このトピックでは、汎用的なドライバー ペアのモデルと見なすことのできるカーネル モード ドライバー フレームワーク (KMDF) の概念について説明します。 このトピックを読む前にまず、「[ミニドライバーとドライバーのペア](minidrivers-and-driver-pairs.md)」で説明する概念について理解しておく必要があります。

Microsoft では長年にわたり、このパラダイムに基づくテクノロジ固有のドライバー モデルを作ってきました。

-   ドライバーは、汎用的な処理を行う部分と特定のデバイスに固有の処理を行う部分の 2 つに分けられます。
-   汎用部分 (フレームワーク) は、Microsoft によって作成されています。
-   固有部分 (KMDF ドライバー) は、Microsoft または独立したハードウェア ベンダーによって作成される場合があります。

![汎用ドライバー ペアとしての KMDF の図](images/kmdfdriverpair.png)

ドライバー ペアのうちフレームワークの部分は、多様なドライバーに共通する一般的なタスクの処理を担当します。 たとえば、フレームワークは、I/O 要求キュー、スレッド同期と電源管理などのタスクを処理することができます。

フレームワークには、KMDF ドライバーのディスパッチ テーブルが存在するため、ユーザーが (KMDF ドライバー、フレームワーク) のペアに I/O 要求パケット (IRP) を送信すると、IRP はフレームワークに送信されます。 フレームワークが単独で IRP を処理できる場合は、KMDF ドライバーは関与しません。 またフレームワークが単独で IRP を処理できない場合は、KMDF ドライバーによって実装されたイベント ハンドラーを呼び出すことにより、支援を利用します。 以下に、KMDF ドライバーで実装できるイベント ハンドラーの例をいくつか示します。

-   EvtDevicePrepareHardware
-   EvtIoRead
-   EvtIoDeviceControl
-   EvtInterruptIsr
-   EvtInterruptDpc
-   EvtDevicePnpStateChange

たとえば、USB 2.0 ホスト コントローラー ドライバーには、usbehci.sys という固有の部分と usbport.sys という汎用部分が含まれます。 USB 2.0 ミニポート ドライバーと呼ばれる usbehci.sys には、USB 2.0 ホスト コントローラーに固有のコードが含まれています。 USB ポート ドライバーと呼ばれる usbport.sys には、USB 2.0 と USB 1.0 に適応する汎用コードが含まれています。 ドライバーのペア (usbehci.sys と usbport.sys) の組み合わせにより、USB 2.0 ホスト コントローラーに対する単一の WDM ドライバーが形成されます。

ドライバーのペア (固有ドライバーと汎用ドライバー) には、各種のデバイス テクノロジに対応した多様な名前が付けられています。 デバイス固有のドライバーにはほとんどの場合、*ミニ*というプレフィックスが付けられています。 汎用ドライバーはポート ドライバーまたはクラス ドライバーと呼ばれることもあります。 以下に、ペア (固有ドライバー、汎用ドライバー) の例をいくつか示します。

-   (ディスプレイ ミニポート ドライバー、ディスプレイ ポート ドライバー)
-   (USB ミニポート ドライバー、USB ポート ドライバー)
-   (バッテリ ミニクラス ドライバー、バッテリ クラス ドライバー)
-   (HID ミニドライバー、HID クラス ドライバー)
-   (ストレージ ミニポート ドライバー、ストレージ ポート ドライバー)

開発されるドライバー ペア モデルが増えるに従って、ドライバーの作成方法をすべて把握するのは難しくなりました。 個々のモデルに、デバイス固有ドライバーと汎用ドライバーの間で行うやり取りのために、独自のインターフェイスが用意されています。 したがって、あるデバイス テクノロジ (たとえばオーディオ) に対応したドライバーを開発する際に必要となる一連の知識と、別のデバイス テクノロジ (たとえばストレージ) に対応したドライバーの開発に伴う知識はまったく異なることがあります。

開発者はしだいに、カーネル モード ドライバーのペアに統一されたモデルがあれば、便利であると考えました。 Windows Vista で初めて提供されたカーネル モード ドライバー フレームワーク (KMDF) はこうしたニーズに対応したものです。 KMDF に基づくドライバーは、テクノロジ固有のドライバー ペア モデルの多くに共通するパラダイムを利用しています。

-   ドライバーは、汎用的な処理を行う部分と特定のデバイスに固有の処理を行う部分の 2 つに分けられます。
-   Microsoft が作る汎用部分は、フレームワークと呼ばれます。
-   Microsoft または個々のハードウェア ベンダーが作る固有部分は KMDF ドライバーと呼ばれます。

USB 3.0 ホスト コントローラー ドライバーは、KMDF に基づくドライバーの一例です。 この例では、ペアの両方のドライバーが Microsoft によって作られています。 汎用ドライバーはフレームワーク、デバイス固有のドライバーは USB 3.0 ホスト コントローラー ドライバーにそれぞれ対応します。 次の図は、USB 3.0 ホスト コントローラーのデバイス ノードとデバイス スタックを示したものです。

![USB 3 ホスト コントローラーのデバイス スタックの図](images/kmdfaspair01.png)

図で usbxhci.sys は、USB 3.0 ホスト コントローラー ドライバーを表します。 usbxhci.sys は、フレームワーク部分に相当する wdf01000.sys でペアを構成します。 usbxhci.sys と wdf01000.sys のペアにより、単一の WDM ドライバーが形成され、これが USB 3.0 ホスト コントローラーのファンクション ドライバーの役割を果たします。 ドライバー ペアがデバイス スタックで占有するのは、単一のデバイス オブジェクトに対応した 1 レベルだけです。 usbxhci.sys と wdf01000.sys のペアで表す単一のデバイス オブジェクトは、USB 3.0 ホスト コントローラーのファンクショナル デバイス オブジェクト (FDO) 部分に対応します。

KMDF ドライバーとフレームワークのペアでは、フレームワークが、多様なカーネル モード ドライバーに共通するタスクの処理を担当します。 たとえば、フレームワークでは、I/O 要求のキュー、スレッド同期、大部分のプラグ アンド プレイ タスク、および電源管理に関するほとんどのタスクを処理することができます。 KMDF ドライバーは、特定のデバイスとのやり取りを必要とするタスクを処理します。 KMDF ドライバーは、フレームワークが必要に応じて呼び出すイベント ハンドラーを登録することにより、要求の処理に関与します。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[ミニドライバーとドライバーのペア](minidrivers-and-driver-pairs.md)

[カーネル モード ドライバー フレームワーク](https://docs.microsoft.com/windows-hardware/drivers/wdf/)

 

 






