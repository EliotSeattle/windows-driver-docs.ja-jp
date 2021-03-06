---
title: 既定の規則セット (Storport)
description: 既定の規則セット (Default.sdv) では、推奨される一連のドライバーを分析するときに使用する規則を指定します。
ms.assetid: 8310E393-4CA7-4701-8BBC-6E758C927FBE
ms.date: 05/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: 51cbd04167729d8a25935d95632b6b14410aeef7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371412"
---
# <a name="default-rule-set-storport"></a>既定の規則セット (Storport)


既定の規則セット (Default.sdv) では、推奨される一連のドライバーを分析するときに使用する規則を指定します。

[DDI 使用量のルール設定 (Storport)](ddi-usage-rule-set--storport-.md)
[Irql ルール設定 (Storport)](irql-rule-set--storport-.md)
[ロック ルール設定 (Storport)](locking-rule-set--storport-.md)
[SrbProcessing ルール設定 (Storport)](srbprocessing-rule-set--storport-.md)
[VirtualStorport ルール設定 (Storport)](virtualstorport-rule-set--storport-.md)
**既定の規則を選択するには**

1.  Microsoft Visual Studio で、ドライバーのプロジェクト (.vcxProj) を選択します。 **ドライバー**  メニューのをクリックして**Static Driver Verifier を起動しています**.

2.  をクリックして、**ルール**タブ。**規則セット**、**既定**。

    Visual Studio の開発者コマンド プロンプト ウィンドウから既定のルールを選択するには、次のように指定します。 **Default.sdv**で、 **/check**オプション。 次に、例を示します。

    ```
    msbuild /t:sdv /p:Inputs="/check:Default.sdv" mydriver.VcxProj /p:Configuration="Win8 Release" /p:Platform=Win32
    ```

    詳細については、次を参照してください。[ドライバーで障害を検出する Static Driver Verifier を使用して](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers)と[Static Driver Verifier のコマンド (MSBuild)](https://docs.microsoft.com/windows-hardware/drivers/devtest/-static-driver-verifier-commands--msbuild-)します。

 

 





