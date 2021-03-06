---
title: 中間ドライバー通知オブジェクト
description: 中間ドライバー通知オブジェクト
ms.assetid: 756e02ff-5e30-4511-af4c-b7be9830898c
keywords:
- WDK のネットワーク処理、中間のドライバーをオブジェクトに通知します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2f5f5142e46837c35b8a00f956fcf0d8947ba31a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385083"
---
# <a name="intermediate-driver-notify-object"></a>中間ドライバー通知オブジェクト





*中間ドライバー オブジェクトに通知*ネットワーク クラスのインストーラーの拡張機能です。 ネットワーク クラスのインストーラーは、読み込みを通知オブジェクトを初期化しますと、ドライバーに関連するイベント (仮想ミニポート削除通知) などの通知を送信します。 通知オブジェクトの概要が一般に必要なかどうか、またはオブジェクトに通知を参照してください詳細については[ネットワーク コンポーネントの通知オブジェクト](notify-objects-for-network-components.md)します。

通知オブジェクトをインストールに含めるには、中間ドライバー プロトコル INF に参照する必要があります。 中間のフィルター ドライバーでは、通知オブジェクトは必要ありません。 柔軟な構成オプションをユーザーに提供したい場合は、フィルター、中間ドライバーに通知オブジェクトを含めることができます。

Windows vista では、ミニポート INF ファイルをシステム INF ディレクトリにコピーするのにには、通知オブジェクトまたはカスタム セットアップ アプリケーションを使用できます。 これらのいずれかを使用する**SetupCopyOEMInf** (Microsoft Windows SDK のドキュメントで説明)、INF をコピーします。 Windows Vista およびそれ以降のオペレーティング システム バージョンでは、使用する必要があります、 [ **INF CopyINF ディレクティブ**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-copyinf-directive)プロトコル ミニポート INF をコピーする INF でします。 INF ファイルをコピーする方法の詳細については、次を参照してください。[コピー Inf](https://docs.microsoft.com/windows-hardware/drivers/install/copying-inf-files)します。

MUX 中間ドライバーに通知オブジェクトがインストールおよび仮想 miniports を削除するサービスを提供する必要があります。 これは、自動またはユーザー インターフェイスを提供することで実行できます。 仮想ミニポートのレジストリにデバイス名の一覧が管理する必要があります。 デバイス名の一覧は、仮想ミニポートと物理デバイス間のバインドを定義します。 たとえば、n 対一 MUX 中間ドライバーのサンプルは通知オブジェクト内の各物理デバイスにバインドされている仮想ミニポートのリストを保持する、 **UpperBindings**レジストリ エントリ。 MUX サンプル ドライバーの読み込み、 **UpperBindings**を一覧表示し、各エントリに対して仮想ミニポートを初期化します。

MUX は、中間ドライバーを使用する必要があります、 **UpperRange**/**LowerRange**エントリを外部のバインディングを制御します。 ただし、必要な場合は、通知オブジェクトから外部のバインドを制御できます。 中間ドライバー内のバインディングの詳細については、次を参照してください[中間ドライバー UpperRange と LowerRange INF ファイルのエントリ。](intermediate-driver-upperrange-and-lowerrange-inf-file-entries.md)

通知オブジェクトは、ユーザーが変更またはドライバーの構成を表示できるユーザー インターフェイスを必要に応じて指定できます。 MUX 中間ドライバーのサンプルには、通知オブジェクトのユーザー インターフェイス例にはが含まれています。

 

 





