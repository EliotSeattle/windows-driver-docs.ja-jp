---
title: 一般的な x64 のディレクティブ
description: このトピックでは、64 ビット Windows で使用するための INF を適切に修飾するために必要な変更について説明します。
ms.assetid: FC372524-0422-4022-AF54-4C6116C89F30
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2531f37de4e26fe355f575660ed2e085b0da45c7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379073"
---
# <a name="general-x64-directives"></a>一般的な x64 のディレクティブ


このトピックでは、64 ビット Windows で使用するための INF を適切に修飾するために必要な変更について説明します。

例:

``` syntax
[DestinationDirs]
DefaultDestDir  = 11
R200.Miniport   = 12  ; drivers
R200.Display    = 11  ; system32
R200.DispWow  = 10, SysWow64

[Manufacturer]
%ATI% = ATI.Mfg, NTamd64

[ATI.Mfg.NTamd64]

[R200_RV200]
FeatureScore=F8
CopyFiles=R200.Miniport, R200.Display, R200.DispWow
AddReg = R200_SoftwareDeviceSettings
AddReg = R200_RV200_SoftwareDeviceSettings
DelReg = R200_RemoveDeviceSettings

; File sections
;

[r200.Miniport]
r200.sys

[r200.Display]
r200umd.dll,,,0x00004000             ; COPYFLG_IN_USE_TRY_RENAME

[R200.DispWow]
r2umd32.dll,,,0x00004000             ; COPYFLG_IN_USE_TRY_RENAME
```

 

 





