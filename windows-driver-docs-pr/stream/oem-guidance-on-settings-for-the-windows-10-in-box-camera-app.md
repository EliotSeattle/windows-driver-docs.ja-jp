---
title: Windows 10 組み込みカメラ アプリの設定に関する OEM ガイダンス
description: Windows 10 用の新しい組み込みのカメラ アプリは、さまざまな OEM によって必要な構成を行わなくても、Windows プラットフォームでサポートされるハードウェアで機能する設計されています。
ms.assetid: 567D2083-9837-44A6-97FB-AD0C9B9EB067
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 88056937684d00ff2a0fa5c66c32c86a06d9b67d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63372380"
---
# <a name="oem-guidance-on-settings-for-the-windows-10-in-box-camera-app"></a>Windows 10 組み込みカメラ アプリの設定に関する OEM ガイダンス


Windows 10 用の新しい組み込みのカメラ アプリは、さまざまな OEM によって必要な構成を行わなくても、Windows プラットフォームでサポートされるハードウェアで機能する設計されています。 カメラ アプリについては、によって通知デバイスのハードウェアと、適切な既定値と、ユーザーのオプションを選択する設定を確認しています。

次のセクションでは、Oem は、アプリが、それ自体を構成する方法を理解して、必要に応じて、そのドライバーを調整できるように、組み込みのカメラ アプリを使用してロジックをそれに応じてについて説明します。

Oem は、デバイスの機能を正しくアドバタイズ、自分のアプリケーションをテストおよび必要な場合、変更を検討してドライバーを最初に構成することをお勧めします。

## <a name="background-and-legacy-behavior"></a>背景と従来の動作


Windows Phone 7.5 (Mango) では、Oem がサポートされているカメラの構成を指定し、カメラ アプリケーションをカスタマイズするための手段を提供する、カメラのマニフェスト ファイル (CameraSettings.xml) が登場しました。 Windows 10 では、このメカニズムは、現在サポートされていませんし、カメラ アプリを選択し、適切な設定をユーザーに表示する組み込みのロジックを使用して置き換えられました。

## <a name="logic-for-choosing-resolutions-to-display"></a>表示解像度を選択するためのロジック


-   **ロジックを静止画像します。**

    まだ画像解像度については、インボックス カメラ アプリは、ドライバーでサポートされている解像度から導き出されますの縦横比の一覧をユーザーに表示します。 アプリは、常に、各縦横比のサポートされている最高の解像度でキャプチャします。 1% 以内の縦横比が同じであると見なされます。

    **Oem メーカーに対する推奨事項:** Oem は、そのドライバーは、デバイスの画面の縦横比と一致する解像度の設定をサポートを確認してください。 既定として選択するように、解像度が高品質なキャプチャ エクスペリエンスを提供する必要があります (を参照してください、*既定の解像度を選択するためのロジック*以下のセクション)。

-   **ビデオのロジック**

    ビデオのキャプチャのカメラ アプリが利用できるように、ユーザー、3 つ最高の解像度、ドライバーで指定されたフレームをサポートする評価 (fps) を 1 秒あたりのフレーム数 15 を超えています。 カメラ アプリが表示されます、ユーザーにすべての使用可能なフレーム レートが高いその 15 fps (したがってハイ フレーム レートのキャプチャをサポートする) これら 3 つの解決策の。

    **Oem メーカーに対する推奨事項:** Oem が、ドライバーが 15 fps を超える割合で、目的のビデオ キャプチャ解像度をサポートしていることを確認してください (25 を超える fps が最善のカスタマー エクスペリエンスをお勧めします)、および提供する、3 つ最高の解像度が、OEM が提示された解決策であることを確認ユーザー。 ドライバーのハイ フレーム レートの機能を指定も確認します。

## <a name="logic-for-choosing-default-resolution"></a>既定の解像度を選択するためのロジック


-   **ロジックを静止画像します。**

    カメラ アプリは、その解像度が最も高い解決オプションの 60% 未満でない限り、デバイスの画面の縦横比が最も一致するドライバーによってアドバタイズされた解像度を選択してもキャプチャするための既定の解像度を選択します。 これは、ユーザー エクスペリエンスの低下が発生する非常に低い解像度を除外します。

-   **ビデオのロジック**

    カメラ アプリは、30 fps のキャプチャをサポートする最高の解像度を選択して、既定の解像度ビデオのキャプチャを選択します。

    場合よりも高い解像度1080p@30fps を使用して、アプリが既定でします。 代わりに、アプリは選択1080p@30fps バッテリ、ストレージ、および温度の問題の上の懸念事項を制限します。 4 K 解像度は、ユーザーが選択できます。

## <a name="logic-for-choosing-default-camera"></a>既定のカメラを選択するためのロジック


既定のセンサーが指定されている場合、カメラ アプリは既定でそのセンサーを使用します。 既定のセンサーが指定されていない場合、カメラ アプリはバック センサーを使用します。 バック センサーがない場合は、アプリは、前面のセンサーを使用します。

## <a name="legacy-oem-settings-and-settings-not-supported-in-windows10-camera"></a>従来の OEM 設定と設定を Windows 10 のカメラでサポートされていません


カメラのマニフェスト ファイルを使用して Windows Phone 8 および Windows Phone 8.1 デバイス用に指定する従来の OEM 設定がサポートされていません。

これには、次の設定が含まれます。

| 設定                  | 説明                                                                                                                                                                                                    |
|--------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| クイックバー アクション         | Windows 10 で、クイックバーが存在しません。 代わりにダッシュ ボードは、画面の上部でご利用いただけます。 ダッシュ ボードの設定は、ハードウェアの機能によって決定されは、OEM がカスタマイズできません。 |
| シーン モード              | 新しいカメラ アプリには、シーン モードまたはモードのシーンをカスタマイズする OEM の機能が用意されていません。                                                                                                          |
| カスタム プロパティの設定 | カメラの Windows 10 アプリは、GUID のプロパティと値のカスタム プロパティの設定をサポートしていません。                                                                                                      |
| カスタム メニュー項目        | カメラの Windows 10 アプリは、カスタム メニュー項目の追加をサポートしていません。                                                                                                                                |

 

 

 




