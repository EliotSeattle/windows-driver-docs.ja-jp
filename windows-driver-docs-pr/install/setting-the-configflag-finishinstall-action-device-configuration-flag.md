---
title: 実行完了-インストール アクションを持つものとして、デバイスをマークします。
description: 実行完了-インストール アクションを持つものとして、デバイスをマークします。
ms.assetid: 7f2560e6-94a7-4dd0-aa2a-e6cdd96c6d9b
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 727242d84f2fd70c60762be66be314351fc0efa5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386878"
---
# <a name="marking-a-device-as-having-a-finish-install-action-to-perform"></a>実行完了-インストール アクションを持つものとして、デバイスをマークします。


*インストーラー* (クラスのインストーラー、クラスの共同インストーラーまたはデバイスの共同インストーラー)、DI_FLAGSEX_FINISHINSTALL_ACTION フラグを設定して、インストーラーを処理するときに実行する終了インストール アクションを使用している Windows を示します、。[ **DIF_NEWDEVICEWIZARD_FINISHINSTALL** ](https://docs.microsoft.com/windows-hardware/drivers/install/dif-newdevicewizard-finishinstall)要求。 この操作により、Windows インストールの完了操作を実行する必要があること、デバイスのフラグを設定します。 手順は次のとおりです。

1.  インストーラーを受信すると、 [ **DIF_NEWDEVICEWIZARD_FINISHINSTALL** ](https://docs.microsoft.com/windows-hardware/drivers/install/dif-newdevicewizard-finishinstall)要求、完了インストール アクションを実行する場合、インストーラーが DI_FLAGSEX_FINISHINSTALL_ACTION フラグを設定します。

    インストーラーは、次のエラー コードの 1 つを返します。

    -   ERROR_DI_DO_DEFAULT インストーラーが完了-インストール ウィザードのページを持たないクラスのインストーラーの場合。
    -   NO_ERROR 場合は、インストーラーは、クラスのインストーラーを終了インストール ウィザードのページまたはが 完了-インストール ウィザードのページはありませんか共同インストーラーを持ちます。

2.  DI_FLAGSEX_FINISHINSTALL_ACTION フラグ設定されている場合、デバイスのすべてのインストーラーが処理後、 [ **DIF_NEWDEVICEWIZARD_FINISHINSTALL** ](https://docs.microsoft.com/windows-hardware/drivers/install/dif-newdevicewizard-finishinstall)フラグとしてデバイスのデバイス、Windows の要求[完了] のインストール操作を実行する必要があります。

 

 





