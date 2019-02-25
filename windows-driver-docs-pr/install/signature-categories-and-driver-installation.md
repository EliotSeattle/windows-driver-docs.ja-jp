---
title: 署名のカテゴリとドライバーのインストール
description: 署名のカテゴリとドライバーのインストール
ms.assetid: d5b0e3a3-51c3-40d8-a2dc-c9392feff2cb
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 553a0c6855a958259a303d471c9d8ff6a9457dee
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56556660"
---
# <a name="signature-categories-and-driver-installation"></a>署名のカテゴリとドライバーのインストール


Windows Vista および Windows の以降のバージョンのドライバーをインストールして、前に、オペレーティング システムは、ドライバーの署名を分析します。 署名が存在する場合、Windows は、その署名に対するすべてのドライバーのファイルを検証します。 この分析の結果に基づいて、Windows によって、ドライバーが、次のカテゴリのいずれかで。

<a href="" id="signed-by-a-microsoft-windows-signing-authority--"></a>**Microsoft Windows が署名機関によって署名されます。**   
これらのドライバーは、いずれか受信トレイ、によって、WHQL 署名または Windows Sustained Engineering によって署名です。

<a href="" id="signed-by-a-trusted-publisher--"></a>**信頼された発行元によって署名されます。**   
これらのドライバーがサード パーティによって署名されたし、ユーザーが常にこのパブリッシャーからの署名されたドライバーを信頼するを明示的に選択します。

<a href="" id="signed-by-an-untrusted-publisher--"></a>**信頼されていない、発行元によって署名されます。**   
これらのドライバーがサード パーティによって署名され、ユーザーは、このパブリッシャーからドライバーを信頼しないでくださいに明示的に選択します。

<a href="" id="signed-by-publisher-of-unknown-trust--"></a>**不明な信頼の発行元によって署名されます。**   
これらのドライバーがサード パーティによって署名された、ユーザーがこの発行元を信頼するかどうかを指定できません。

<a href="" id="altered--"></a>**変更されます。**   
これらのドライバー署名されますが、Windows がでその少なくとも 1 つのファイルを検出、[ドライバー パッケージ](driver-packages.md)パッケージの署名後に変更されました。

<a href="" id="unsigned--"></a>**符号なし整数。**   
これらのドライバーは署名されていないまたは署名が無効です。 有効な署名は、信頼された証明機関 (CA) によって発行された証明書を使用して作成する必要があります。

ドライバーを分類すると、Windows をインストールするかどうか判断します。 プロセスは、ユーザーの種類によって異なります。 管理者と標準ユーザーでは、Windows では、ユーザーを表示しません。 Windows の署名機関または信頼された発行元によって署名されたドライバーが自動的にインストールし、サイレント モードでインストールし、他のすべてを拒否します。

管理ユーザーには、柔軟性があります。

-   ドライバーは、Windows の署名機関または信頼された発行元によって署名済み、Windows はユーザーに確認しないで、ドライバーをインストールします。

-   ドライバーは、信頼されていない発行元によって署名済み、Windows では、ドライバーはインストールされません。 Windows は、ユーザーがこの場合、プロンプト表示されませんが、エラーをログに記録*Setupapi.dev.log*します。

-   場合は、ドライバーは、不明な信頼の発行元によって署名された、Windows には、次の Windows セキュリティ ダイアログ ボックスで、ユーザーが求められます。

    ![不明な信頼関係があるドライバーを windows セキュリティ ダイアログ ボックスのスクリーン ショット](images/install1.png)

    ユーザーがこのドライバーをインストールするかどうかを明示的に選択する必要があります。 ユーザーは、ユーザーのシステム上の信頼された発行元の一覧に、パブリッシャーを追加することもできます。 このオプションでは、このパブリッシャーから今後すべてのドライバーは、として扱われます。 ユーザーが選択には、ユーザーのシステムにインストールされているときに信頼されている場合。 ユーザーがこのオプションを選択していない場合、不明な信頼のカテゴリと管理者のユーザーに、パブリッシャーはこのパブリッシャーの追加のドライバーをインストールしようとする場合、このメッセージを受信する続行します。

-   ドライバーは、有効な署名がないか、変更された場合、Windows には、次の Windows セキュリティ ダイアログ ボックスを持つ管理者が要求されます。 ここでも、ユーザーでは、ドライバーをインストールするかどうかを選択明示的にする必要があります。

    ![有効な署名がないドライバーを windows セキュリティ ダイアログ ボックスのスクリーン ショット](images/install2.png)

**注**  Windows Vista のおよびユーザー HD DVD および下でライセンス供与されている他の形式など、次世代のプレミアム コンテンツを再生するために、Windows の以降のバージョン、 *Advanced Access Content System (AACS)仕様*、そのシステム上のすべてのカーネル モード コンポーネントに署名する必要があります。 つまり、符号なしまたは変更されたドライバーをインストールする管理ユーザーを選択した場合、システムはプレミアム コンテンツを再生は許可されていません。 Windows Vista のメディア コンポーネントを保護する方法の詳細については、次を参照してください。[コードは、Windows Vista のメディアの保護されているコンポーネントの署名](https://go.microsoft.com/fwlink/p/?linkid=74262)します。

 

 

 




