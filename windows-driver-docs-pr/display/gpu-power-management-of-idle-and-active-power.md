---
title: アイドル状態とアクティブな電源の GPU 電源管理
description: Windows Display Driver Model (WDDM) 1.2 以降のドライバーが個々のデバイスまたは一連のデバイスの電力を管理できるようにする GPU 電源管理インフラストラクチャ。
ms.assetid: F8096F7E-39EA-45CB-8A1C-60A7A298AFEC
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 30a3a9b3a2e47c8b9581998b4ad51c40609e90a4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838932"
---
# <a name="gpu-power-management-of-idle-states-and-active-power"></a>アイドル状態とアクティブな電源の GPU 電源管理


Windows 8 以降では、Windows Display Driver Model (WDDM) 1.2 以降のドライバーが個々のデバイスまたは一連のデバイスの電力を管理できるようにする、オプションの GPU 電源管理インフラストラクチャを使用できます。 このインフラストラクチャは、Windows とのコラボレーションにおける、F 状態と P 状態の電源管理をサポートするための標準化されたメカニズムを提供します。

|                                                                                   |                                        |
|-----------------------------------------------------------------------------------|----------------------------------------|
| 最小 WDDM バージョン                                                              | 1.2                                    |
| Windows の最小バージョン                                                           | 8                                      |
| ドライバーの実装                                                             | 省略可能                               |
| [必要条件](https://docs.microsoft.com/windows-hardware/test/hlk/windows-hardware-lab-kit)とテスト | **デバイス...RuntimePowerMgmt** |

 

## <a name="span-idgpu_power_management_device_driver_interface__ddi_spanspan-idgpu_power_management_device_driver_interface__ddi_spanspan-idgpu_power_management_device_driver_interface__ddi_spangpu-power-management-device-driver-interface-ddi"></a><span id="GPU_power_management_device_driver_interface__DDI_"></span><span id="gpu_power_management_device_driver_interface__ddi_"></span><span id="GPU_POWER_MANAGEMENT_DEVICE_DRIVER_INTERFACE__DDI_"></span>GPU 電源管理デバイスドライバーインターフェイス (DDI)


これらの新しい関数および更新された関数と構造体は、Windows 8 以降で使用できます。ディスプレイミニポートドライバーでは、電源コンポーネントの状態を遷移させると共に、Microsoft DirectX グラフィックスカーネルサブシステムで power イベントを伝達します。

-   [*DxgkCbCompleteFStateTransition*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkcb_completefstatetransition)
-   [*DxgkCbPowerRuntimeControlRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkcb_powerruntimecontrolrequest)
-   [*DxgkCbSetPowerComponentActive*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkcb_setpowercomponentactive)
-   [*DxgkCbSetPowerComponentIdle*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkcb_setpowercomponentidle)
-   [*DxgkCbSetPowerComponentLatency*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkcb_setpowercomponentlatency)
-   [*DxgkCbSetPowerComponentResidency*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkcb_setpowercomponentresidency)
-   [*DxgkDdiPowerRuntimeControlRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddipowerruntimecontrolrequest)
-   [*DxgkDdiSetPowerComponentFState*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddisetpowercomponentfstate)
-   [**DXGK\_DRIVERCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_drivercaps)
-   [**DXGK\_POWER\_コンポーネント\_フラグ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_power_component_flags)
-   [**DXGK\_POWER\_コンポーネント\_マッピング**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_power_component_mapping)
-   [**DXGK\_POWER\_コンポーネント\_の種類**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ne-d3dkmddi-_dxgk_power_component_type)
-   [**DXGK\_POWER\_RUNTIME\_コンポーネント**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_power_runtime_component)
-   [**DXGK\_QUERYADAPTERINFOTYPE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ne-d3dkmddi-_dxgk_queryadapterinfotype)
-   [**DXGKARG\_QUERYADAPTERINFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgkarg_queryadapterinfo)
-   [**DXGK\_QUERYSEGMENTOUT3**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_querysegmentout3)

## <a name="span-idgpu_power_management_scenariosspanspan-idgpu_power_management_scenariosspanspan-idgpu_power_management_scenariosspangpu-power-management-scenarios"></a><span id="GPU_power_management_scenarios"></span><span id="gpu_power_management_scenarios"></span><span id="GPU_POWER_MANAGEMENT_SCENARIOS"></span>GPU の電源管理のシナリオ


Gpu とディスプレイ画面は、ラップトップ、モバイルデバイス、デスクトップ Pc における最大の電力消費者の2つです。

電力消費を減らし、バッテリ寿命を延ばすための主要な電源管理シナリオを次に示します。

-   個々のシステムコンポーネントが使用されていない場合はシャットダウンされるため、モバイルフォームファクターデバイスはアイドル状態になり、電力を節約できます。
-   チップベースの Windows システム (SoC) ベースのデバイスは、コンシューマーデバイスや携帯電話と同様に動作します。これは、必要なときに直ちに電源を入れ、電力を節約するためです。

## <a name="span-idhardware_certification_requirementsspanspan-idhardware_certification_requirementsspanspan-idhardware_certification_requirementsspanhardware-certification-requirements"></a><span id="Hardware_certification_requirements"></span><span id="hardware_certification_requirements"></span><span id="HARDWARE_CERTIFICATION_REQUIREMENTS"></span>ハードウェア認定の要件


ハードウェアデバイスがこの機能を実装するときに満たす必要がある要件の詳細[について](https://docs.microsoft.com/windows-hardware/test/hlk/windows-hardware-lab-kit)は、**デバイス...RuntimePowerMgmt**。

Windows 8 で追加された機能の確認については、「 [WDDM 1.2 の機能](wddm-v1-2-features.md)」を参照してください。

 

 





