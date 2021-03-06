---
title: USB ビデオ クラス ドライバーの概要
description: USB ビデオ クラス ドライバーの概要
ms.assetid: 890d448e-bfee-462d-8cce-a2cca42f2f6d
keywords:
- USB ビデオ クラス ドライバー WDK AVStream、USB ビデオ クラス ドライバーについて
- USB ビデオ クラス ドライバーに関するクラス ドライバー WDK USB、ビデオ
- USB ビデオ クラス ドライバーに関する UVC ドライバー WDK AVStream、
- ユーザー モードのクライアント WDK USB ビデオ クラス
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6a4595ae0a06228deb9872bbf14bb37d9cc068f0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63382547"
---
# <a name="usb-video-class-driver-overview"></a>USB ビデオ クラス ドライバーの概要


Web カメラまたはデジタル ビデオ_カメラのドライバーを提供する場合は、システムが指定したユニバーサル シリアル バス (USB) ビデオ クラス ドライバー、Usbvideo.sys の使用を検討します。 USB ビデオ クラス (UVC) ドライバーでは、USB ビデオ クラス デバイス ドライバーのサポートを提供する Microsoft 提供の AVStream ミニドライバーです。 デバイスは、UVC を使用する場合は、独自のドライバーを提供する必要はありません。 代わりに、デバイスは、システム指定のドライバーを使用した自動的に動作します。

USB ビデオ クラス モデルでベンダーを書き込みませんドライバー。代わりに、ベンダーは実装のガイドラインに従ってストリーミング ビデオのハードウェア、[ユニバーサル シリアル バス デバイス クラス定義のビデオ デバイス仕様](https://go.microsoft.com/fwlink/p/?linkid=516989)します。 UVC ドライバーでは、その機能を取得するには、直接ハードウェアを照会し、必要な独自のドライバーで、デバイスをドライブします。

必要に応じて、ベンダー固有の処理を追加する UVC ドライバーの機能を拡張できます。

次の表は、異なるバージョンの Windows で UVC のサポートを示します。

| UVC バージョン                             | Windows Vista/XP | Windows 7     | Windows 8 |
|-----------------------------------------|------------------|---------------|-----------|
| USB ビデオ クラス 1.5 (H.264 ビデオ コーデック) | サポートされない    | サポートされない | サポート対象 |
| USB ビデオ クラス 1.1                     | サポートされない    | サポート対象     | サポート対象 |
| USB ビデオ クラス 1.0                     | サポート対象        | サポート対象     | サポート対象 |

 

Windows 8 以降、H.264 ビデオ コーデック (エンコーダー/デコーダー) はサポートされています。 H.264 は、ネットワーク帯域幅とストレージ領域の使用を減らすのビデオの効率的な圧縮技法を許可するオープン規格です。 これは、指定されたビット レートのビデオ品質の向上につながります。 詳細については、次を参照してください。 [USB H.264 ビデオをカメラ サポート](usb-h-264-video-cameras-support.md)します。 参照することも、 [H.264 の USB ビデオ クラスに提案された拡張機能の Microsoft](https://go.microsoft.com/fwlink/p/?LinkId=233063)します。

Usbvideo.sys ドライバーを使用するいくつかの利点を次に示します。

-   インストールに必要な CD はありません。
-   コストを記述しないドライバー
-   メンテナンス コストが不要
-   機能を追加するベンダー向け機会
-   パブリック シンボルを使用したデバッグの簡略化
-   Driver Verifier の連携
-   チェックされている OS のビルドとの連携
-   電源管理で ACPI 準拠
-   電源管理のセレクティブ サスペンドに準拠
-   メディア ファンデーション、DirectShow のマルチ メディア Api をサポートしています

システム提供の Usbvideo.sys ドライバーは、異なるバージョンの Windows で、次の UVC 機能をサポートします。

| UVC 機能                                                                        | Windows Vista/XP | Windows 7     | Windows 8     |
|------------------------------------------------------------------------------------|------------------|---------------|---------------|
| 1 つのビデオ コントロールのインターフェイスと 1 つまたは複数のビデオ ストリーミング インターフェイス          | サポート対象        | サポート対象     | サポート対象     |
| Standard ユニットと端末、拡張機能のユニットを含む                            | サポート対象        | サポート対象     | サポート対象     |
| UVC 仕様で定義されているすべての 3 つのメソッドをまだイメージ キャプチャのサポート | サポート対象        | サポート対象     | サポート対象     |
| 一括と isochronous デバイス                                                       | サポート対象        | サポート対象     | サポート対象     |
| プローブのコミットのコントロールを使用してパラメーターのネゴシエーションのストリーミング                        | サポート対象        | サポート対象     | サポート対象     |
| 圧縮された形式:MJPEG、DV                                                      | サポート対象        | サポート対象     | サポート対象     |
| 非圧縮形式。YUY2、NV12                                                   | サポート対象        | サポート対象     | サポート対象     |
| サポートはキャプチャし、デバイスの表示                                           | サポート対象        | サポート対象     | サポート対象     |
| 圧縮された形式:MPEG2TS                                                         | サポートされない    | サポートされない | サポートされない |
| Stream およびフレーム ベースの形式                                               | サポートされない    | サポート対象     | サポート対象     |
| H.264 ビデオ コーデック                                                                  | サポートされない    | サポートされない | サポート対象     |

 

## <a name="customizing-the-uvc-driver"></a>UVC ドライバーをカスタマイズします。


UVC については、サポートをカスタマイズするには指定することによって、[拡張ユニット プラグイン](introduction-to-usb-video-class-extension-units.md)します。 拡張機能のユニットは、デバイスとアプリケーションのベンダーから提供された秘密のコントロール チャネルを提供します。

## <a name="additional-resources"></a>その他のリソース


UVC 実装をテストするには、次のツールを使用できます。

-   GraphEdit
-   KsStudio
-   USBView

これらのツールの詳細については、次を参照してください。 [AVStream テストおよびデバッグ](avstream-testing-and-debugging.md)します。

USB ビデオ クラス 1.1 の仕様の圧縮設定をダウンロードすることができます、[デバイス クラスのページ](https://go.microsoft.com/fwlink/p/?linkid=517016)USB Implementers Forum web サイト。

 

 




