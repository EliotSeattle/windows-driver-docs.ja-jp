---
title: ネットワーク INF ファイル内の Remove セクション
description: ネットワーク INF ファイル内の Remove セクション
ms.assetid: c9be4e98-fa35-4966-895a-aebe29f16289
keywords:
- INF ファイル WDK ネットワークの削除
- ネットワーク INF ファイル WDK を削除
- セクションの WDK ネットワークを削除します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 38359509414853158d6d987e99b0856cb9ac1e96
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385833"
---
# <a name="remove-section-in-a-network-inf-file"></a>ネットワーク INF ファイル内の Remove セクション





**削除**のセクションではサポートされて**NetClient**、 **NetTrans**、および**NetService**コンポーネントではなく**Net**コンポーネント (アダプター)。

**注**  **NetClient**コンポーネントは Windows 8.1、Windows Server 2012 R2 で非推奨以降。

 

ネットワーク クラスのインストーラーを追跡するありませんアダプター インスタンス。 A**削除**を他のアダプターかアダプターの複数のインスタンスを共有するファイルを削除するセクションを表示できるこれらのアダプターまたはアダプター インスタンス動作していません。
かどうかによって使用されるドライバー ファイルを削除する必要が、 **Net**コンポーネント、ファイルを使用しているすべてのドライバーを追跡する共同インストーラーを使用します。 このような共同インストーラーには、同じデバイスに複数のデバイス ドライバーの複数のインスタンスも追跡する必要があります。 共同インストーラーの詳細については、次を参照してください。 [INF ファイルを作成する](https://docs.microsoft.com/windows-hardware/drivers/install/overview-of-inf-files)します。

 

 





