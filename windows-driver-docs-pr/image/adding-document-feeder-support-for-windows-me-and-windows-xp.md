---
title: Windows XP と Windows ドキュメント フィーダー サポートを追加します。
description: Windows XP と Windows ドキュメント フィーダー サポートを追加します。
ms.assetid: f3be94fa-6fb7-45de-a3ce-f3d173e802cf
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6dc97e835bb9b0b7a0d461c44a43769c3bc2da41
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56527293"
---
# <a name="adding-document-feeder-support"></a>ドキュメント フィーダーのサポートを追加します。

ドキュメント フィーダー付きは、ユニットに接続されている、またはスキャナーをスキャンする位置に紙のドキュメントを自動的にフィードに組み込まれています。 ドキュメント フィーダーの付いたスキャナーなどの機能が公開され、次の一覧に含まれるプロパティの追加により制御されます。 Windows Me と Windows XP は、ルート項目は次のプロパティがあります。

- [**WIA\_DPS\_水平\_シート\_フィード\_サイズ**](https://msdn.microsoft.com/library/windows/hardware/ff551401)
- [**WIA\_DPS\_垂直\_シート\_フィード\_サイズ**](https://msdn.microsoft.com/library/windows/hardware/ff551446)
- [**WIA\_DPS\_MIN\_水平\_シート\_フィード\_サイズ**](https://msdn.microsoft.com/library/windows/hardware/ff551405)
- [**WIA\_DPS\_MIN\_垂直\_シート\_フィード\_サイズ**](https://msdn.microsoft.com/library/windows/hardware/ff551407)
- [**WIA\_DPS\_シート\_フィーダー\_登録**](https://msdn.microsoft.com/library/windows/hardware/ff551430)
- [**WIA\_DPS\_ドキュメント\_処理\_機能**](https://msdn.microsoft.com/library/windows/hardware/ff551379)
- [**WIA\_DPS\_ドキュメント\_処理\_状態**](https://msdn.microsoft.com/library/windows/hardware/ff551386)
- [**WIA\_DPS\_ドキュメント\_処理\_を選択します**](https://msdn.microsoft.com/library/windows/hardware/ff551384)
- [**WIA\_DPS\_ページ**](https://msdn.microsoft.com/library/windows/hardware/ff551414)

Windows Me と Windows XP は、子項目では、次の省略可能なドキュメント フィーダー プロパティにあります。

- [**WIA\_DPS\_ページ\_サイズ**](https://msdn.microsoft.com/library/windows/hardware/ff551417)
- [**WIA\_DPS\_ページ\_幅**](https://msdn.microsoft.com/library/windows/hardware/ff551419)
- [**WIA\_DPS\_ページ\_高さ**](https://msdn.microsoft.com/library/windows/hardware/ff551416)
- [**WIA\_IP\_向き**](https://msdn.microsoft.com/library/windows/hardware/ff552625)

ドライバーが、WIA を報告するデバイスに、フラット ベッドやドキュメント フィーダー付き、両面印刷ユニットがある場合は、\_DPS\_ドキュメント\_処理\_としての機能のプロパティ (フィード |フラット |DUP)。 確認します WIA の有効な値\_DPS\_ドキュメント\_処理\_選択が正しく設定されています。

たとえば、アプリケーションがドキュメント フィーダーの 3 つのページの双方向のスキャンを実行しようとします。 これを実現するアプリケーションは、設定、WIA\_DPS\_ドキュメント\_処理\_にプロパティを選択します (フィーダー |双方向)、WIA を設定および\_DPS\_3 ページのプロパティ。 WIA を設定する必要があります、アプリケーションが最初に、ページの先頭をスキャンしようとすると場合、\_DPS\_ドキュメント\_処理\_にプロパティを選択します (フィーダー |双方向 |前部\_最初)。 これが完了したらアプリケーションがデータ転送元となる要求すべき子項目に移動します。 3 ページ目としてフィーダーに 2 番目のページの一番前と、ミニドライバーは、1、2 つのページとしてそのページのページとしてフィーダーに最初のページの先頭を報告します。

デバイスがドキュメント フィーダー付きの場合、ドキュメント フィーダー付きのプロパティをサポートする必要があることに注意してください。

## <a name="acquiring-data-from-a-document-feeder"></a>ドキュメント フィーダー付きのデータの取得

実装で行う必要があるいくつかの変更がある、 [ **IWiaMiniDrv::drvAcquireItemData** ](https://msdn.microsoft.com/library/windows/hardware/ff543956)メソッド、スキャナーがドキュメント フィーダー付きのイメージを取得するとします。

1. アプリケーションの読み取り、WIA\_DPS\_ドキュメント\_処理\_スキャナーがドキュメント フィーダーを使用してスキャンをサポートしているかどうかを判断する機能のプロパティ。
1. アプリケーションの読み取り、WIA\_DPS\_ドキュメント\_処理\_ドキュメント フィーダーを使用してスキャンするスキャナーが構成されているかどうかを決定するプロパティを選択します。
1. アプリケーションは、WIA を読み取ることによってドキュメント フィーダーに用紙が表示がかどうかを判断します。\_DPS\_ドキュメント\_処理\_状態。 フィーダーに用紙がない場合は、設定の WIA\_DPS\_ドキュメント\_処理\_状態を適切な状態コードおよび戻り値の WIA\_エラー\_用紙\_から空**IWiaMiniDrv::drvAcquireItemData**取得が行われた後すぐにします。
1. チェック、WIA\_DPS\_スキャンの動作を決定するページのプロパティ。 このプロパティが 0 の場合は、フィーダーが空になるまでのすべてのページをスキャンします。 正の場合は、WIA に含まれている値で示されるページの数のみをスキャン\_DPS\_ページのプロパティ。
1. ループを制御する、継続的にスキャン、およびデータ (一度に 1 つのページ) を呼び出すことによって、WIA アプリケーションを送信して、要求されたページ数をスキャン、 [ **IWiaMiniDrvCallBack::MiniDrvCallback** ](https://msdn.microsoft.com/library/windows/hardware/ff543946)メソッド。 次のコード例では、これが機能する方法を示します。

    ```cpp
    for(int x=1; x=Pagecount; x++)
    {
        \\ Tell scanner to scan an image.
        \\ Receive image data from scanner.
        \\ Send the just-scanned image to the registered application.
    }
    ```

1. 場合[ **WIA\_IPA\_TYMED** ](https://msdn.microsoft.com/library/windows/hardware/ff551656) TYMED に設定されている\_コールバックまたは TYMED\_マルチページ\_コールバックし、余分なメッセージ (IT\_MSG\_新規\_ページ) 1 つのページがスキャンされた後、次の 1 つは、スキャンする前に送信する必要があります。 これは、呼び出すことで、 [ **wiasSendEndOfPage** ](https://msdn.microsoft.com/library/windows/hardware/ff549351) WIA サービス ユーティリティ関数。

ドキュメント フィーダー付きのドライバーが返すページ数は、WIA の設定によって異なります。\_DPS\_ページのプロパティ。

## <a name="if-wiadpspages-is-zero"></a>場合 WIA\_DPS\_ページには 0 です

1. スキャナーは、最初のページをスキャンできない場合は、すぐに、エラー コードを返します。 これには、紙詰まりと用紙、スキャナーを実行するとが含まれます。
1. スキャナーが正常に最初のページをスキャンし、かつはスキャンを続行できますが紙不足しています、WIA 成功コードを返す\_状態\_エンド\_の\_メディア。 アプリケーションは、スキャナーの用紙が不足していますが、転送が成功すると、この通知します。 WIA に一部のアプリケーションが応答\_エラー\_用紙\_よう WIA には、同じ方法で空\_状態\_エンド\_の\_メディア。
1. スキャナーが正常に最初のページをスキャンし、かつはスキャンを続行できますがデータの損失にならないエラーが発生した、WIA を返す\_状態\_エンド\_の\_メディア。 これにより、アプリケーションを回復して、エラーが発生する前にスキャンした任意のページを保存できます。 スキャナーが障害から回復した正しくまでにすぐに、後続のスキャンは、エラー コードを返す必要があります。
1. スキャナーが正常に最初のページをスキャンし、かつはスキャンを続行できますがデータの損失が発生するエラーが発生した、エラー コードをすぐに返します。

## <a name="if-wiadpspages-is-positive"></a>場合 WIA\_DPS\_ページが正の値

1. どの WIA のすべての規則\_DPS\_ページは、0 個適用します。
1. 要求されたページ数をスキャンする前に、スキャナーに紙が不足している場合は、WIA を返す\_状態\_エンド\_の\_メディア。 これにより、アプリケーション ページが既に正常にスキャンの数を保つため、スキャンのセッションを閉じることができます。 WIA に一部のアプリケーションが応答\_エラー\_用紙\_よう WIA には空のと同じ方法\_状態\_エンド\_の\_メディア。