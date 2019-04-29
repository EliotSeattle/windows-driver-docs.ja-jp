---
title: MPIO\_EventEntry WMI クラス
description: MPIO\_EventEntry WMI クラス
ms.assetid: 37160002-fe65-4d02-80f5-375f169b7d11
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 961006ce44568ff76e40bb2eb9940030a5c4d753
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63331102"
---
# <a name="mpioevententry-wmi-class"></a>MPIO\_EventEntry WMI クラス


MPIO ドライバーは、MPIO を使用して\_EventEntry WMI クラスは、MPIO 関連するイベントです。 このクラスは現在実装されていません。

```cpp
class MPIO_EventEntry : WMIEvent
{
        [key, read]
        string InstanceName;

        [read]
        boolean Active;

        //
        // Current system time at time of logging.
        //
        [WmiDataId(1),
         read,
         Description("Time Stamp") : amended,
         WmiTimeStamp
        ] uint64 TimeStamp;

        //
        // Indicates severity of event being logged.
        //
        [WmiDataId(2),
        read,
        Values{"Fatal Error",
               "Error",
               "Warning",
               "Information"} : amended,

        DefineValues{"MPIO_FATAL_ERROR",
                     "MPIO_ERROR",
                     "MPIO_WARNING",
                     "MPIO_INFORMATION"},

        ValueMap{"1", "2", "3", "4"}
        ] uint32 Severity;

        //
        // Multi-path disk's name that this event is being logged for.
        //
        [WmiDataId(3),
        read,
        MaxLen(63),
        Description("Component") : amended
        ] string Component;

        //
        // Description of event.
        //
        [WmiDataId(4),
        read,
        MaxLen(63),
        Description("Event Description") : amended
        ] string EventDescription;
};
```

この WMI クラスに関連付けられているメソッドはありません。

 

 





