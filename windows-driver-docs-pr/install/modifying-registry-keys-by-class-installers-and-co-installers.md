---
title: クラス インストーラーと共同インストーラーでのレジストリ キーの変更
description: クラス インストーラーと共同インストーラーでのレジストリ キーの変更
ms.assetid: A7F41F97-5E06-41d8-B80F-DDBC41A62BB3
keywords:
- レジストリ WDK デバイスのインストール、レジストリ キーの変更
- レジストリ WDK デバイスのインストール、レジストリ キーを変更するクラスのインストーラー
- レジストリ WDK デバイスのインストール、レジストリ キー、共同インストーラーを変更します。
- クラスのインストーラー WDK デバイスのインストール、レジストリ キーの変更
- 共同インストーラー WDK デバイスのインストール、レジストリ キーの変更
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: af2e82c214157888f735c1df6e3c819f82116742
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377658"
---
# <a name="modifying-registry-keys-by-class-installers-and-co-installers"></a>クラス インストーラーと共同インストーラーでのレジストリ キーの変更


**注**  ユニバーサルまたはモバイルのドライバー パッケージでは、このセクションで説明する機能はサポートされていません。 参照してください[ユニバーサル INF ファイルを使用して](using-a-universal-inf-file.md)します。

 

特定の状況では、except*クラス インストーラー*と*co-installer*作成、変更、またはレジストリ キーを削除する、標準レジストリ関数を使用しないでください。 ほとんどの場合、レジストリ キー変更がのみに格納されるディレクティブを使用して[INF ファイル](overview-of-inf-files.md)します。 これらのディレクティブの詳細については、次を参照してください。 [INF ディレクティブの概要](summary-of-inf-directives.md)します。

次に、この規則の例外を示します。

-   必要があるときにクラスのインストーラーと共同インストーラー関数を使用できます、標準レジストリにレジストリ キーを変更する、 **HKLM\\ソフトウェア**サブツリーです。

    **注**  クラスのインストーラーと共同インストーラーが、デバイスの内のエントリとしてカスタムのデバイスのプロパティを保存ことを強くお勧め*ソフトウェア キー*します。

     

-   クラスのインストーラーと共同インストーラーは許可されている場合にサブキーを変更する、 **HKLM\\システム\\CurrentControlSet\\コントロール\\CoDeviceInstallers**レジストリ キー。

次のガイドラインは、クラスのインストーラーや共同インストーラーによってレジストリ キーを安全に変更する後にする必要があります。

-   クラスのインストーラーと共同インストーラーを使用する必要がありますまず[ **SetupDiCreateDevRegKey** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdicreatedevregkeya)または[ **SetupDiOpenDevRegKey** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiopendevregkey)へのハンドルを開く変更するレジストリ キーです。 ハンドルが開かれた後は、レジストリ キーを変更するのにクラスのインストーラーと共同インストーラーが標準レジストリ関数を使用できます。

-   クラスのインストーラーと共同インストーラーを使用する必要がありますいない**SetupDiDeleteDevRegKey**または*ハードウェア キー*デバイス。 詳細については、次を参照してください。[デバイスのレジストリ キーを削除する](deleting-the-registry-keys-of-a-device.md)します。

詳細については、標準レジストリ関数は、次を参照してください。[レジストリ関数](https://go.microsoft.com/fwlink/p/?linkid=194529)します。

 

 





