---
title: MPIO\_タイマー\_カウンター WMI クラス
description: MPIO\_タイマー\_カウンター WMI クラス
ms.assetid: 386110f8-504c-4617-b8ae-557ea504d41d
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: eb8e798fe5a56e1d1e13ea0c4e2890bb1d211239
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843565"
---
# <a name="mpio_timers_counters-wmi-class"></a>MPIO\_タイマー\_カウンター WMI クラス


WMI クライアントは、MPIO\_タイマー\_カウンター WMI クラスを使用して、すべてのグローバルタイマー値の MPIO を照会します。

```cpp
class MPIO_TIMERS_COUNTERS
{

    [key, read]
     string InstanceName;
    [read] boolean Active;

    //
    // Flag indicating if automatic path verification must be performed every
    // N seconds (where N depends on the value set in PathVerificationPeriod).
    // Type is boolean and must be filled with either 0 (disbale) or 1 (enable).
    //
    [WmiDataId(1),
     read, write,
     Description("Enable/Disable Auto Path-Verification.") : amended
    ] uint32 PathVerifyEnabled;

    //
    // This timer is specified in seconds. The default is 30 seconds
    // and its max allowed is MAXULONG. It controls the periodicity
    // for path verification.
    //
    [WmiDataId(2),
     read, write,
     Description("Path Verification Timer.") : amended
    ] uint32 PathVerificationPeriod;

    //
    // This timer is specified in seconds. The default is 20 seconds
    // and its max allowed is MAXULONG. It controls the amount of time
    // that the pseudo-LUN will continue to be in memory, even after
    // loosing all its paths.
    //
    [WmiDataId(3),
     read, write,
     Description("PDO Remove Timer.") : amended
    ] uint32 PDORemovePeriod;

    //
    // The number of times a failed I/O will be retried if DsmInterpretError
    // requests a retry. The default is set to 3.
    //
    [WmiDataId(4),
     read, write,
     Description("Request Retry Count (Max 500)") : amended
    ] uint32 RetryCount;

    //
    // This value is specified in seconds. The default is 1 second. It
    // controls the interval of time after which a failed request is
    // retried (after the DSM has decided so).
    //
    [WmiDataId(5),
     read, write,
     Description("Retry Interval (seconds) (Max MAXULONG)") : amended
    ] uint32 RetryInterval;

};
```

このクラス定義が WMI ツールスイートによってコンパイルされると、 [**MPIO\_タイマー\_カウンター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mpiowmi/ns-mpiowmi-_mpio_timers_counters)データ構造が生成されます。 この WMI クラスに関連付けられているメソッドはありません。

 

 





