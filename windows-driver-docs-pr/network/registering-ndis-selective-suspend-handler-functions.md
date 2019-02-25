---
title: 選択的登録 NDIS 中断ハンドラー関数
description: 選択的登録 NDIS 中断ハンドラー関数
ms.assetid: D4125F14-8356-4D9E-A287-D35D3BF69182
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0db84c30f6f1aec53c62529dde5040a10b46c7ed
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553950"
---
# <a name="registering-ndis-selective-suspend-handler-functions"></a>選択的登録 NDIS 中断ハンドラー関数


ミニポート ドライバーには、選択的 NDIS がサポートしている場合は、中断、NDIS は、基になるネットワーク アダプターがアイドル状態になることをドライバーに通知します。 ミニポート ドライバーでは、これらのアイドル状態の通知を処理するために、次の関数を提供する必要があります。

<a href="" id="miniportidlenotification"></a>[*MiniportIdleNotification*](https://msdn.microsoft.com/library/windows/hardware/hh464092)  
NDIS 呼び出し、 [ *MiniportIdleNotification* ](https://msdn.microsoft.com/library/windows/hardware/hh464092)ミニポート ドライバー、ネットワーク アダプターがアイドル状態になることを通知するハンドラー関数。 ミニポート ドライバーは、ネットワーク アダプターが、低電力状態に移行できるかどうかを決定することにより、アイドル状態の通知を処理します。 ミニポート ドライバーでは、バスに固有の方法でこの決定を実行します。

USB のミニポート ドライバーが USB アイドル状態の要求の I/O 要求パケット (IRP) を発行して、ネットワーク アダプターが低電力状態に移行できるかどうかを決定するなど、([**IOCTL\_内部\_USB\_送信\_IDLE\_通知**](https://msdn.microsoft.com/library/windows/hardware/ff537270)) を基になる USB バス ドライバー。 アダプターがアイドル状態し、低電力状態に移行することができます、この IRP の処理、ミニポート ドライバーに通知されます。

<a href="" id="miniportcancelidlenotification"></a>[*MiniportCancelIdleNotification*](https://msdn.microsoft.com/library/windows/hardware/hh464088)  
NDIS 呼び出し、 [ *MiniportCancelIdleNotification* ](https://msdn.microsoft.com/library/windows/hardware/hh464088)未処理のアイドル状態の通知をキャンセル ハンドラー関数。 この関数が呼び出されると、ミニポート ドライバーは、アイドル状態の通知で以前発行がある可能性があります bus 固有 Irp をキャンセルします。

たとえば、 [ *MiniportCancelIdleNotification* ](https://msdn.microsoft.com/library/windows/hardware/hh464088)を呼び出すと、USB ミニポートが以前に発行された USB アイドル要求 IRP を取り消す必要があります。 IRP が取り消されたときに、アダプターが電力状態に遷移しますようになりましたことができます、ミニポート ドライバーに通知されます。

ときに、ミニポート ドライバーの[ **DriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff548818)関数が呼び出されると、選択的 NDIS は、次の手順に従ってハンドラー関数を中断するドライバー レジスタ。

1.  ミニポート ドライバーを設定する必要があります、 **SetOptionsHandler**のメンバー、 [ **NDIS\_ミニポート\_ドライバー\_特性**](https://msdn.microsoft.com/library/windows/hardware/ff565958)構造体のドライバーのエントリ ポイントを[ *MiniportSetOptions* ](https://msdn.microsoft.com/library/windows/hardware/ff559443)関数。 ドライバー呼び出し[ **NdisMRegisterMiniportDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff563654)を登録するその**NDIS\_ミニポート\_ドライバー\_特性**NDIS と構造体。

2.  NDIS 呼び出し、 [ *MiniportSetOptions* ](https://msdn.microsoft.com/library/windows/hardware/ff559443)関数への呼び出しのコンテキストで[ **NdisMRegisterMiniportDriver**](https://msdn.microsoft.com/library/windows/hardware/ff563654)します。

    ときに[ *MiniportSetOptions* ](https://msdn.microsoft.com/library/windows/hardware/ff559443)が呼び出され、ミニポート ドライバーの初期化、 [ **NDIS\_ミニポート\_SS\_特性**](https://msdn.microsoft.com/library/windows/hardware/hh451559)ハンドラー関数へのポインターを含む構造体。 ミニポート ドライバーを呼び出して[ **NdisSetOptionalHandlers** ](https://msdn.microsoft.com/library/windows/hardware/ff564550)設定と、 *OptionalHandlers*パラメーターへのポインターを**NDIS\_ミニポート\_SS\_特性**構造体。

選択的 NDIS のアイドル状態の通知を処理する方法の詳細については、中断を参照してください[NDIS セレクティブ サスペンド アイドル通知](ndis-selective-suspend-idle-notifications.md)します。

 

 




