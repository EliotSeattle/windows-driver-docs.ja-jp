---
title: NDIS-WDF 関数に対応する関数
description: NDIS-WDF 関数に対応する関数
ms.assetid: 28C8DFA3-5602-422D-89AA-6EA05F501E15
keywords:
- NetAdapterCx の NDIS WDF 関数、対応する NetCx の NDIS WDF 関数と同等
ms.date: 06/05/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2647f9c0a06a7637189c4e431b726d9ba75b7633
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63384539"
---
# <a name="ndis-wdf-function-equivalents"></a>NDIS-WDF 関数に対応する関数

[!include[NetAdapterCx Beta Prerelease](../netcx-beta-prerelease.md)]

次の表は、NDIS 関数と同等の WDF を示します。

|NDIS API ファミリ|WDF のと同じ|
|-|-|
|[**NdisAllocateIoWorkItem**](https://msdn.microsoft.com/library/windows/hardware/ff561604)|[**WdfWorkItemCreate**](https://msdn.microsoft.com/library/windows/hardware/ff551201)|
|[**NdisAllocateTimerObject**](https://msdn.microsoft.com/library/windows/hardware/ff561618)|[**WdfTimerCreate**](https://msdn.microsoft.com/library/windows/hardware/ff550050)|
|[**NdisAcquireSpinLock**](https://msdn.microsoft.com/library/windows/hardware/ff560699)|[**WdfSpinLockAcquire**](https://msdn.microsoft.com/library/windows/hardware/ff550040)|
|[**NdisInterlockedIncrement**](https://msdn.microsoft.com/library/windows/hardware/ff562752)|[**InterlockedIncrement**](https://msdn.microsoft.com/library/windows/hardware/ff547910)|
|[**NdisInitializeEvent**](https://msdn.microsoft.com/library/windows/hardware/ff562732)|[**KeInitializeEvent**](https://msdn.microsoft.com/library/windows/hardware/ff552137)|
|[**NdisMInitializeScatterGatherDma**](https://msdn.microsoft.com/library/windows/hardware/ff553543)|[**WdfDmaEnablerCreate**](https://msdn.microsoft.com/library/windows/hardware/ff546983)|
|[**NdisInitializeString**](https://msdn.microsoft.com/library/windows/hardware/ff562741)|[**WdfStringCreate**](https://msdn.microsoft.com/library/windows/hardware/ff550046)|
|[**NdisSystemActiveProcessorCount**](https://msdn.microsoft.com/library/windows/hardware/ff564577)|[**KeGetCurrentProcessorNumberEx** ](https://msdn.microsoft.com/library/windows/hardware/ff552076) (カーネル)|
|[**NdisWriteRegisterUchar**](https://msdn.microsoft.com/library/windows/hardware/ff564678)|[**WDF_WRITE_REGISTER_UCHAR**](https://msdn.microsoft.com/library/windows/hardware/dn265684)|
