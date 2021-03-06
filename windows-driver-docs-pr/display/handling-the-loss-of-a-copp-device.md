---
title: COPP デバイスの喪失の処理
description: COPP デバイスの喪失の処理
ms.assetid: 7e74b249-34be-44cc-a022-ba6574f2f841
keywords:
- 保護 WDK COPP、デバイスの紛失をコピーします。
- ビデオのコピー防止 WDK COPP、デバイスの紛失
- COPP WDK DirectX va なので、デバイスの紛失
- デバイスの紛失、ビデオの WDK COPP の保護
- 失われた COPP デバイス WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: eccd54f38b813751c2438c4a25a97ba94ab172de
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369840"
---
# <a name="handling-the-loss-of-a-copp-device"></a>COPP デバイスの喪失の処理


## <span id="ddk_handling_the_loss_of_a_copp_device_gg"></span><span id="DDK_HANDLING_THE_LOSS_OF_A_COPP_DEVICE_GG"></span>


**このセクションには、Windows Server 2003 SP1 にのみ以降が適用されますおよび Windows XP SP2 以降。**

保護モードに設定されているビデオ セッションでは、ビデオのセッションに関連付けられている DirectX VA COPP デバイスの破棄を引き起こすシナリオを処理する必要があります。 次のシナリオは、ディスプレイ ドライバーの呼び出しを開始する[ *DdMoCompDestroy* ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_destroy)ビデオ セッションの認定出力コネクタでのコンテンツの保護が可能性がありますが、コールバック関数有効になります。

-   表示モードの変更

-   アタッチまたはデタッチ Windows デスクトップからの監視

-   全画面表示のコマンド プロンプト ウィンドウを入力します。

-   任意の DirectDraw または Direct3D 排他モード アプリケーションの開始

-   ユーザーの簡易切り替えを実行します。

-   ワークステーションをロックまたは CTRL + ALT + DEL キーを押します

-   リモート デスクトップ接続を使用して、ワークステーションへのアタッチ

-   たとえば、中断または休止状態に省電力モードの場合--

-   アプリケーション予期せずに終了 - たとえば、ページ フォールトを

ビデオのセッションが有効になっていると、出力コンテンツの保護中に前に示したシナリオのいずれかが発生した場合、ディスプレイ ドライバーの*DdMoCompDestroy*関数は、ビデオのミニポート ドライバーへの呼び出しを開始する必要があります[ *COPPCloseVideoSession* ](https://docs.microsoft.com/windows-hardware/drivers/display/coppclosevideosession) COPP デバイスの現在のローカルの保護のレベル数によって、グローバルな保護レベル数をデクリメントする関数。 ビデオのミニポート ドライバーはする必要がありますし、変更されたグローバルな保護レベルを確認し、それに応じて出力コネクタに適用される保護レベルを調整します。

 

 





