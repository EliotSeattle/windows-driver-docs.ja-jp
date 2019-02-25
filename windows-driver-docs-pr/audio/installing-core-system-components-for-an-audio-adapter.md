---
title: オーディオのアダプターの主要なシステム コンポーネントをインストールします。
description: オーディオのアダプターの主要なシステム コンポーネントをインストールします。
ms.assetid: fc14867e-cae8-4381-bcd3-ec2230050cf6
keywords:
- オーディオ アダプター WDK、システム コンポーネント
- アダプターのドライバー WDK オーディオ、システム コンポーネント
- ポート クラス オーディオ アダプター WDK、システム コンポーネント
ms.date: 10/27/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2cd1926add0c99bbf1a248997910a75f7ee10440
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530320"
---
# <a name="installing-core-system-components-for-an-audio-adapter"></a>オーディオのアダプターの主要なシステム コンポーネントをインストールします。


## <span id="installing_core_system_components_for_an_audio_adapter"></span><span id="INSTALLING_CORE_SYSTEM_COMPONENTS_FOR_AN_AUDIO_ADAPTER"></span>


このセクションには、ポート クラス オーディオ アダプターのコアのシステム コンポーネントのインストールの詳細については、次のトピックが含まれています。

[Windows でのインストール](installing-in-windows.md)

[ **INF DDInstall セクション**](https://msdn.microsoft.com/library/windows/hardware/ff547344)製造元ので、各ハードウェア ID が指定されて**モデル**セクションを含めることを指定する必要があります、 **KS します。登録**Ks.inf」セクションおよび**WDMAUDIO します。登録**Wdmaudio.inf」セクション。 Ks.inf ファイルは、ストリーミング コンポーネント core カーネルをインストールします。 Wdmaudio.inf ファイルには、コア WDM オーディオ コンポーネントがインストールされます。 ベンダーは、変更またはこれらのシステム INF ファイルを置換する必要がありますできません。

 

 



