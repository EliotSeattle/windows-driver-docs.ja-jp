---
title: IPsec 関数
description: このセクションでは、Windows Filtering Platform コールアウト ドライバーの IPsec の機能について説明します。
ms.assetid: c457f036-84be-47fd-8cfe-9ac867111ca5
keywords:
- IPsec の機能はネットワーク ドライバー
ms.date: 11/07/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5ec18b25dfa268ac1762e95856ccc611fabc0961
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327694"
---
# <a name="ipsec-functions"></a>IPsec 関数

次の関数のセマンティクスは、正確に同じ戻り値の型は、Win32 エラー コードではなく、NTSTATUS コードがユーザー モード アプリケーションから呼び出されたときに、コールアウト ドライバーとしてから呼び出された場合です。 これらの各関数については、次を参照してください。、 [Windows フィルタ リング プラットフォーム](https://go.microsoft.com/fwlink/p/?linkid=210226)、Microsoft Windows SDK のドキュメント セクション。

これらの関数の呼び出し元は、IRQL で実行する必要があります PASSIVE_LEVEL を = です。

- FwpmIPsecTunnelAdd0
- FwpmIPsecTunnelDeleteByKey0
- IPsecGetStatistics0
- IPsecSaContextAddInbound0
- IPsecSaContextAddOutbound0
- IPsecSaContextCreate0
- IPsecSaContextCreateEnumHandle0
- IPsecSaContextDeleteById0
- IPsecSaContextDestroyEnumHandle0
- IPsecSaContextEnum0
- IPsecSaContextExpire0
- IPsecSaContextGetById0
- IPsecSaContextGetSpi0
- IPsecSaCreateEnumHandle0
- IPsecSaDbGetSecurityInfo0
- IPsecSaDbSetSecurityInfo0
- IPsecSaDestroyEnumHandle0
- IPsecSaEnum0

