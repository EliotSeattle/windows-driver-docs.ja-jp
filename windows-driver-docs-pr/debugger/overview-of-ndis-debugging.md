---
title: NDIS のデバッグの概要
description: NDIS のデバッグの概要
ms.assetid: d15e8a0c-e553-4e0d-84ed-5fdc2026a2d3
keywords:
- NDIS デバッグの概要
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: ace66602dde1efba95cf1841158a74087deae4ed
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63359538"
---
# <a name="overview-of-ndis-debugging"></a>NDIS のデバッグの概要


ネットワーク ドライバーをデバッグするための 2 つの主要ツールとは、デバッグ トレースと Network Driver Interface Specification (NDIS) 拡張機能です。 デバッグ トレースの詳細については、次を参照してください。 [NDIS デバッグ トレースを有効にする](enabling-ndis-debug-tracing.md)します。 NDIS の拡張機能のデバッグの詳細については、次を参照してください。 [NDIS 拡張](ndis-extensions--ndiskd-dll-.md)、Ndiskd.dll 拡張モジュールの拡張機能コマンドの完全な一覧を提供します。 Winxp ディレクトリで拡張モジュールが表示されます。

ネットワークのドライバーをデバッグするための別のツールは、デバッグ情報を取得するために便利ですが通常のデバッグの拡張のコレクションです。 たとえば、入力[**スタックの 2 つの ndis!。**](-stacks.md) スタックの以降のすべてのスレッドを表示します**ndis!** します。 この情報は、ハング、失速のデバッグに役立ちます。

また NDIS 固有バグの確認コードがあるバグ チェック 0x7C (BUGCODE\_NDIS\_ドライバー)。 そのパラメーターの完全な一覧を参照してください。 [**バグ チェック 0x7C**](bug-check-0x7c--bugcode-ndis-driver.md)します。

NDIS ドライバーをテストするためのもう 1 つの便利なツールでは、NDIS Verifier です。 詳細については、Windows Driver Kit (WDK) ドキュメントの NDIS Verifier のトピックを参照してください。

 

 





