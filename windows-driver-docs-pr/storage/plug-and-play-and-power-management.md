---
title: プラグ アンド プレイと電源管理
description: プラグ アンド プレイと電源管理
ms.assetid: 9e5d545d-ec24-42ac-a9e5-290502548fc0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1d125b52fbc84b1ae367616c40873e220b9b2225
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63389396"
---
# <a name="plug-and-play-and-power-management"></a>プラグ アンド プレイと電源管理


LsiU3AdapterControl ルーチンでは、そのハードウェアを変更することがなく実装する特別なアダプターの制御ルーチン\_初期化\_データ構造体。 電源管理を通過するアダプターの HwFindAdapter と HwInitialize ルーチンを置換する StopAdapter と ScsiRestartAdapter ControlTypes、サポートが含まれています。 LsiU3StartIo ルーチンがさらに、関数コード SRB される Srb の処理を追加\_関数\_POWER HBA のシャット ダウンします。

 

 




