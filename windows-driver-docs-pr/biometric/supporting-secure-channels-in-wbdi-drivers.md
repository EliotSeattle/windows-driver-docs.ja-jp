---
title: WBDI ドライバーでのセキュリティで保護されたチャネルのサポート
description: WBDI ドライバーでのセキュリティで保護されたチャネルのサポート
ms.assetid: 1b4532f4-18ee-4c65-9373-2ca635d2f40d
keywords:
- 生体認証ドライバー WDK、セキュリティで保護されたチャネル
- セキュリティで保護されたチャネル WDK 生体認証
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 86d094897584be04bf2efe022930ed743b94b0e9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63328362"
---
# <a name="supporting-secure-channels-in-wbdi-drivers"></a>WBDI ドライバーでのセキュリティで保護されたチャネルのサポート


WBDI ドライバーでは、ホストとデバイス間のセキュリティで保護されたチャネルをサポートするために、ドライバーでのセキュリティ関連の機能をカプセル化する必要があります。 ドライバーは、セキュリティで保護されたチャネルを管理します。 ドライバーは、Windows 生体認証サービス (WBS) にサンプル データを渡す、データを暗号化されたあります。 WBS でプラグイン ベンダーから提供されたエンジンは、必要に応じて、web サービスをセキュリティで保護されたチャネルを設定できます。

セキュリティに関する考慮事項は、WBF アプリケーションにとって透過的な必要があります。

 

 





