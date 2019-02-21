---
title: ISCSI\_TargetPortalGroup WMI クラス
description: ISCSI\_TargetPortalGroup WMI クラス
ms.assetid: dff17d52-b308-49cc-97ec-d54eddb4e747
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: a45569f06103c00a554358a4b331b45d50c22026
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550290"
---
# <a name="iscsitargetportalgroup-wmi-class"></a>ISCSI\_TargetPortalGroup WMI クラス


## <span id="ddk_iscsi_targetportalgroup_wmi_class_kr"></span><span id="DDK_ISCSI_TARGETPORTALGROUP_WMI_CLASS_KR"></span>


ISCSI\_TargetPortalGroup クラスは、ターゲット ポータルのグループを定義します。

このクラスが次のように定義されている*Common.mof*します。

```cpp
class ISCSI_TargetPortalGroup {
  [WmiDataId(1), description("Number of portals in group") :
    amended]
    uint32  PortalCount;
  [WmiDataId(2), WmiSizeIs("PortalCount"),
    description("Target portals in group") : amended]
    ISCSI_TargetPortal  Portals[];
};
```

WMI ツールのスイートでは、上記のクラス定義をコンパイルするときに生成、 [ **ISCSI\_TargetPortalGroup** ](https://msdn.microsoft.com/library/windows/hardware/ff561575)データ構造体。

 

 





