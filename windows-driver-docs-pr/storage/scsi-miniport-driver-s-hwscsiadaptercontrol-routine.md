---
title: SCSI ミニポート ドライバーの HwScsiAdapterControl ルーチン
description: SCSI ミニポート ドライバーの HwScsiAdapterControl ルーチン
ms.assetid: ccc5aa02-415d-40d1-a1ed-c7d4d881f4ca
keywords:
- SCSI ミニポート ドライバー WDK ストレージ、HwScsiAdapterControl
- HwScsiAdapterControl
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2034a3919e09ecbfb462c801a25ade9aa47220cc
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529055"
---
# <a name="scsi-miniport-drivers-hwscsiadaptercontrol-routine"></a>SCSI ミニポート ドライバーの HwScsiAdapterControl ルーチン


## <span id="ddk_scsi_miniport_drivers_hwscsiadaptercontrol_routine_kg"></span><span id="DDK_SCSI_MINIPORT_DRIVERS_HWSCSIADAPTERCONTROL_ROUTINE_KG"></span>


NT ベースのオペレーティング システムのミニポート ドライバーにこのエントリ ポイントを設定する必要があります**NULL**で、 [ **HW\_初期化\_データ (SCSI)** ](https://msdn.microsoft.com/library/windows/hardware/ff557456) (参照してください[必須およびオプションの SCSI ミニポート ドライバー ルーチン](required-and-optional-scsi-miniport-driver-routines.md)) ミニポート ドライバーがプラグ アンド プレイをサポートしていない場合。 それ以外の場合、ミニポート ドライバーが必要、 [ **HwScsiAdapterControl**](https://msdn.microsoft.com/library/windows/hardware/ff557274)ルーチンの HBA の PnP や電源管理操作をサポートします。

ミニポート ドライバーの*HwScsiAdapterControl*ルーチンは、まずポート ドライバーによって呼び出されます**ScsiQuerySupportedControlTypes** HBA が初期化された後、最初の I/O、決定する前に。その他の操作、ミニポート ドライバーでサポートされています。 ミニポート ドライバーではサポートされているがサポートする操作を設定する\_コントロール\_型\_ポート ドライバーによって割り当てられているリスト。 後*HwScsiAdapterControl*ポート ドライバーのみ、ミニポート ドライバーによって示された操作をもう一度ルーチンを呼び出すと、この最初の呼び出しから返します。

ミニポート ドライバーの*HwScsiAdapterControl*ルーチンは、次の操作の一部またはすべてをサポートできます。

-   **ScsiStopAdapter**電源オフ、システムから削除またはそれ以外の場合を再構成またはした無効になっているときに、HBA をシャット ダウンします。

    SCSI ポート ドライバーの呼び出し時に*HwScsiAdapterControl* HBA を停止するは完了していない要求が存在しないことをようにします。 ミニポート ドライバーでは、HBA の割り込みを無効にする、バック グラウンド、割り込みの対象とならない処理を含むすべての処理を停止、および初期化されていない状態に HBA を配置する必要があります。 ミニポート ドライバーがそのリソースを解放する必要があります。必要に応じて、ポート、ドライバーは、ミニポート ドライバーに代わってリソースを解放します。 この呼び出しを*HwScsiAdapterControl*前に、SRB が\_関数\_フラッシュの要求、ので、フラッシュの要求が完了したので、そのデータが変更された場合を除き、キャッシュをフラッシュする必要はありません。

    ミニポート ドライバーは呼び出されませんもう一度この HBA の PnP マネージャーは、HBA を再起動することを要求するか、電源管理のシャット ダウンされた HBA の電源が入ってまで。

    なお*HwScsiAdapterControl*、ミニポート ドライバー任意のルーチンのように、HBA は既にシステムから削除された後に、HBA を停止するという可能性があります。

-   **ScsiSetBootConfig** BIOS は、システムを起動する必要がある HBA の設定を復元します。

    ミニポート ドライバーをサポートする必要があります**ScsiSetBootConfig**を呼び出す必要がある場合[ **ScsiPortGetBusData** ](https://msdn.microsoft.com/library/windows/hardware/ff564624)または[ **ScsiPortSetBusDataByOffset** ](https://msdn.microsoft.com/library/windows/hardware/ff564751)このような設定を復元します。 ポート ドライバー呼び出しミニポート ドライバーの*HwScsiAdapterControl*で**ScsiSetBootConfig** HBA を停止するルーチンを呼び出した後。

-   **ScsiSetRunningConfig**ミニポート ドライバーは、システムの実行中に、HBA を制御する必要がある HBA の設定を復元します。

    ミニポート ドライバーをサポートする必要があります**ScsiSetRunningConfig**を呼び出す必要がある場合**ScsiPortGetBusData**または[ **ScsiPortSetBusDataByOffset** ](https://msdn.microsoft.com/library/windows/hardware/ff564751)このような設定を復元します。 ポート ドライバー呼び出しミニポート ドライバーの*HwScsiAdapterControl*で**ScsiSetRunningConfig** HBA を再起動するルーチンを呼び出す前にします。

-   **ScsiRestartAdapter**を電源管理のシャット ダウンされた HBA を再起動します。

    ポートのドライバーの呼び出し時に*HwScsiAdapterControl* HBA を再起動して、ミニポート ドライバーに割り当てられていたすべてのリソースを引き続き使用し、そのデバイスの拡張機能と、論理ユニットの拡張機能はそのまま残ります。 ミニポート ドライバーがからのみ呼び出すことのルーチンを呼び出す必要がありますいないその HBA を再起動すると*HwScsiFindAdapter*します。

    ミニポート ドライバーがサポートされていない場合**ScsiRestartAdapter**、ポート ドライバー呼び出し、ミニポート ドライバーの*HwScsiFindAdapter*と*HwScsiInitialize*ルーチンHBA を再起動します。 ただし、このようなルーチンが必要な領域を再起動するとため、このようなミニポート ドライバーに電源が入らないの HBA をサポートするミニポート ドライバーだけ早く検出作業を行うことがあります**ScsiRestartAdapter**します。

参照してください[ **HwScsiAdapterControl** ](https://msdn.microsoft.com/library/windows/hardware/ff557274)詳細についてはします。

 

 



