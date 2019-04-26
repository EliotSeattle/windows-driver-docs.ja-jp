---
title: wudfext.wudfdevice
description: Wudfext.wudfdevice 拡張機能には、プラグ アンド プレイ (PnP) とデバイスの電源管理の状態のシステムが表示されます。
ms.assetid: d070f5ba-97c0-47f8-869f-54a3d3395476
keywords:
- デバッグ wudfext.wudfdevice Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wudfext.wudfdevice
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 169d998f46d00cb2b31e36d3c05aacc43d9ff88f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63348004"
---
# <a name="wudfextwudfdevice"></a>!wudfext.wudfdevice


**! Wudfext.wudfdevice**拡張機能は、プラグ アンド プレイ (PnP) とデバイスの電源管理の状態のシステムが表示されます。

```dbgcmd
!wudfext.wudfdevice pWDFDevice
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______pWDFDevice______"></span><span id="_______pwdfdevice______"></span><span id="_______PWDFDEVICE______"></span> *pWDFDevice*   
アドレスを指定します、 **IWDFDevice**について PnP または電源管理の状態を表示するインターフェイス。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>利用不可</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 以降</strong></p></td>
<td align="left"><p>Wudfext.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

詳細については、次を参照してください。[ユーザー モード ドライバー フレームワークのデバッグ](user-mode-driver-framework-debugging.md)します。

<a name="remarks"></a>注釈
-------

使用することができます、 **! wudfext.wudfdevice**デバイスの現在の PnP または電源管理の状態を確認する拡張機能を*pWDFDevice*パラメーターを指定します。

例を次に、 **! wudfext.wudfdevice**表示。

```dbgcmd
kd> !wudfdevice 0xf2f80 
Pnp Driver Callbacks:
  IPnpCallback: 0x0
  IPnpCallbackHardware: 0x0
  IPnpSelfManagedIo: 0x0
Pnp State Machine:
  CurrentState:  WdfDevStatePnpStarted
  Pending UMIrp: 0x00000000
    Could not read event queue depth, assuming 8
  Event queue:
    Processed/in-process events:
      PnpEventAddDevice
      PnpEventStartDevice
      PnpEventPwrPolStarted
    Pending events:
    State History:
      WdfDevStatePnpInit
      WdfDevStatePnpInitStarting
      WdfDevStatePnpHardwareAvailable
      WdfDevStatePnpEnableInterfaces
      WdfDevStatePnpStarted
Power State Machine:
  CurrentState:      WdfDevStatePowerD0
  Pending UMIrp:     0x00000000
  IoCallbackFailure: false
    Could not read event queue depth, assuming 8
  Event queue:
    Processed/in-process events:
      PowerImplicitD0
    Pending events:
    State History:
      WdfDevStatePowerStartingCheckDeviceType
      WdfDevStatePowerD0Starting
      WdfDevStatePowerD0StartingConnectInterrupt
      WdfDevStatePowerD0StartingDmaEnable
      WdfDevStatePowerD0StartingStartSelfManagedIo
      WdfDevStatePowerDecideD0State
      WdfDevStatePowerD0
Power Policy State Machine:
  CurrentState             : WdfDevStatePwrPolStartingSucceeded
  PowerPolicyOwner         : false
  PendingSystemPower UMIrp : 0x00000000
  PowerFailed              : false
    Could not read event queue depth, assuming 8
  Event queue:
    Processed/in-process events:
      PwrPolStart
      PwrPolPowerUp
    Pending events:
    State History:
      WdfDevStatePwrPolStarting
      WdfDevStatePwrPolStarted
      WdfDevStatePwrPolStartingSucceeded
```

 

 





