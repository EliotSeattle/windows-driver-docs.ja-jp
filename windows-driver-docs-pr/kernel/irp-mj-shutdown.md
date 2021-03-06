---
title: IRP_MJ_SHUTDOWN
description: データの内部キャッシュがある大容量記憶装置のドライバーは、DispatchShutdown ルーチンでこの要求を処理する必要があります。
ms.date: 08/12/2017
ms.assetid: af0b01b5-5f81-42da-aa4b-433bd422a51f
keywords:
- IRP_MJ_SHUTDOWN カーネルモードドライバーのアーキテクチャ
ms.localizationpriority: medium
ms.openlocfilehash: 865ea1d3d8190311018c5f576241362cd626f9f6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838596"
---
# <a name="irp_mj_shutdown"></a>IRP\_MJ\_シャットダウン


データの内部キャッシュがある大容量記憶装置のドライバーは、 [*DispatchShutdown*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)ルーチンでこの要求を処理する必要があります。 基になるドライバーがデータの内部バッファーを保持している場合は、大容量記憶装置と中間ドライバーのドライバーもこの要求を処理する必要があります。

<a name="when-sent"></a>送信時
---------

シャットダウン要求を受信すると、システムがシャットダウンされていることを示すメッセージがファイルシステムドライバーによって送信されていることを示します。

1つまたは複数のファイルシステムドライバーは、ユーザーがログオフしたとき、または他の何らかの理由でシステムがシャットダウンされたときに、このような低レベルのドライバーを1つ以上のシャットダウン要求を送信できます。

PnP マネージャーは、任意のスレッドコンテキストで、IRQL < = APC_LEVEL にこの IRP を送信します。

## <a name="input-parameters"></a>入力パラメーター


なし

## <a name="output-parameters"></a>出力パラメーター


なし

<a name="operation"></a>操作
---------

ドライバーは、シャットダウン要求を完了する前に、デバイスに現在キャッシュされているデータ、またはドライバーの内部バッファーに保持されているデータの転送を完了する必要があります。

ドライバーは、 [**IoRegisterShutdownNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioregistershutdownnotification)または[**IoRegisterLastChanceShutdownNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioregisterlastchanceshutdownnotification)のいずれかを使用して登録する場合を除き、デバイスオブジェクトに対して**IRP\_MJ\_のシャットダウン**要求を受信しません。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Wdm (Wdm .h、Ntddk、または Ntifs を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[*DispatchShutdown*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)

[**IoRegisterLastChanceShutdownNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioregisterlastchanceshutdownnotification)

[**IoRegisterShutdownNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioregistershutdownnotification)

 

 




