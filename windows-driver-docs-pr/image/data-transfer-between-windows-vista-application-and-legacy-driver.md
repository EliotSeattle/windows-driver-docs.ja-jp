---
title: Windows Vista アプリケーションとレガシ ドライバー間のデータ転送
description: Windows Vista アプリケーションとレガシ ドライバー間のデータ転送
ms.assetid: 0acb2ca3-6ac6-441d-a12d-446ae5b70295
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 57e16fa6d760462f47e8e4dbdadeb83b8f6352ac
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360860"
---
# <a name="data-transfer-between-windows-vista-application-and-legacy-driver"></a>Windows Vista アプリケーションとレガシ ドライバー間のデータ転送


互換性層では、Windows Vista アプリケーションを呼び出す**IWiaTransfer::Download** (Microsoft Windows SDK のドキュメントで説明) レガシ ドライバー。 互換性レイヤーは、形式変換するほかフォルダー転送コードを実装する必要があります。 互換レイヤーは、従来、ドライバーから複数のページを転送することが常にフィーダー転送用の特別なコードを実装します。 Windows Vista のアプリケーションが、フラグを使用しても、フィーダー項目から、スキャン中に複数のページを要求することは常に\_ファイル転送。 次の図は、Windows Vista のアプリケーションと従来のドライバーを示します。

![windows vista のアプリケーションとレガシ ドライバー間データ転送を示す図](images/vistaapp-legacydrv.png)

WIA サービス内で従来のコールバック オブジェクトは、従来の転送メッセージおよびデータ転送の Windows Vista のメッセージに変換し、指定されたストリームにデータを書き込みます。

Windows Vista のアプリケーションは、TYMED のみが必要です\_ファイルと TYMED\_マルチページ\_互換性レイヤが責任を担うファイルその TYMED\_コールバックと TYMED\_マルチページ。\_従来、ドライバーからは、Windows Vista アプリケーションにコールバックは公開されません。

互換レイヤーのこの部分を実装する最も簡単な方法は、常にレガシ TYMED ドライバーへの呼び出しをされている\_ファイルと TYMED\_マルチページ\_ファイル セットです。 これの欠点は、こと、ドライバーは常にしなければデータは、アプリケーションのストリームにライトバックでした前に、イメージ全体をスキャンします。 互換レイヤーは TYMED を使用してそのため、\_Windows Vista アプリケーションの形式のスキャンを要求する場合にコールバック**WiaImgFmt\_BMP** (、 [ **WIA\_IPA\_形式**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-format)プロパティに設定**WiaImgFmt\_BMP)** します。 これにより、データ バックアップ バンドでバンドを記述する互換性レイヤーです。

ただし、従来のドライバーをサポートしません**WiaImgFmt\_BMP**が**WiaImgFmt\_MEMORYBMP**ため TYMED\_コールバック。 したがって、BMP ファイル ヘッダーを作成しても、アプリケーションにこのファイルのヘッダーを書き戻す変換のコールバック オブジェクトがあります。 これは、ときに、BMP ファイル ヘッダー直接から構築できる BMP 情報のヘッダーなどの簡単な場合があります。 あります。 ただし、BMP 情報ヘッダーの高さが 0 に設定します。 この場合、WIA 互換性レイヤーは、BMP ファイルのヘッダーを記述して、BMP 情報ヘッダーを更新する前にすべてのデータが転送されるまで待つ必要があります。

TYMED だけ以外ため TYMED 転送、\_コールバック、従来、ドライバーから実行されますは、複数ページの形式は通常のみでサポートされる TYMED\_マルチページ\_ファイル、およびドライバー サポート通常詳細ため TYMED 形式\_ため TYMED よりファイル\_コールバック.

中、TYMED\_ファイル転送互換性レイヤーをアプリケーションのストリームにデータを戻す書き込みます前に、転送が終了するまでの待機します。 これは、ファイルをメモリにマッピングしてメモリを 1 つ 1 つのすべてのデータ書き込み要求を記述します。

TYMED、中に\_コールバック転送では、互換性レイヤー書き戻します、アプリケーションのストリームに、IT を受信するたびに\_MSG\_従来、ドライバーからのデータの転送メッセージ。

互換レイヤーには、フィーダー転送の特別なコードも含まれています。 このコードによりこと互換性レイヤーから転送できる複数のページ、ADF TYMED TYMED でない場合でも\_マルチページ\_ファイル。 これは、方法は、互換性レイヤーを複数回、1 ページのみを要求するたびに、ドライバーを呼び出すことによってです。 このソリューションにより、すべてのレガシ ドライバーが Windows Vista のアプリケーションによって呼び出されたときに、トレイから複数のページの転送を処理できること。

従来、ドライバーは、たとえば (プレビュー) 用の転送時に「アウト オブ バンド」メッセージを送信できます。 転送のストリーム ベースのモデルに収まらないために、これらのメッセージは無視されます。

TYMED 定数の詳細についてを参照してください[理解 TYMED](understanding-tymed.md)します。

 

 




