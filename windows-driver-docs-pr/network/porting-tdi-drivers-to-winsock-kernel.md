---
title: Winsock カーネルへの TDI ドライバーの移植
description: TDI ドライバーを Winsock カーネル (WSK) に移植するには、次の表に示すように、TDI タスクを同等の WSK に変換する必要があります。
ms.assetid: 23662BF1-92EC-4C07-9A8D-F8F1D7D51692
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 684af6ea6ad39663ccd12f481ffe1ea180f03a40
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843686"
---
# <a name="porting-tdi-drivers-to-winsock-kernel"></a>Winsock カーネルへの TDI ドライバーの移植


TDI ドライバーを Winsock カーネル (WSK) に移植するには、次の表に示すように、TDI タスクを同等の WSK に変換する必要があります。

| タスク                            | TDI                                                                                       | Winsock カーネル (WSK)                                                                                                          |
|----------------------------------|-------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------|
| 登録と登録解除          | 該当なし                                                                                       | [**Wskregister**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nf-wsk-wskregister)と[ **wskregister**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nf-wsk-wskderegister)                                       |
| キャプチャとリリースプロバイダー NPI | 該当なし                                                                                       | [**WskCaptureProviderNPI**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nf-wsk-wskcaptureprovidernpi)と[ **WskReleaseProviderNPI**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nf-wsk-wskreleaseprovidernpi)   |
| アドレスファイルオブジェクトの作成       | *EaBuffer*を作成し、 [**zwcreatefile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntcreatefile)を呼び出します。                      | 不要になりました。 「 [**Wsksocket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_socket)」を参照してください。                                                                 |
| 接続ファイルオブジェクトの作成    | 接続*EaBuffer*を作成し、 [**zwcreatefile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntcreatefile)を呼び出します。           | 不要になりました。 「 [**Wsksocket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_socket) 」と「 [*Wskacceptevent*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_accept_event)」を参照してください。                 |
| アドレスの関連付け                | [**TDI\_\_アドレスの関連付け**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff565080(v=vs.85))                                | [**WskBind**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_bind)                                                                                               |
| イベントハンドラーの設定               | [**TDI\_\_イベント\_ハンドラーの設定**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff565576(v=vs.85))                               | Wskcontrolsocket を使用した[**Wskcontrolsocket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_control_socket)または静的なバリエーション[](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_control_client) |
| イベントハンドラーの消去             | [**TDI\_\_イベント\_ハンドラーの設定**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff565576(v=vs.85))                               | [**WskControlSocket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_control_socket)                                                                             |
| 接続                          | [**TDI\_接続**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff565083(v=vs.85))                                                     | [**WskConnect**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_connect)                                                                                         |
| 切断                       | [**TDI\_切断**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff565090(v=vs.85))                                               | [**WskDisconnect**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_disconnect)                                                                                   |
| Send                             | [**TDI\_送信**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff565549(v=vs.85))                                                           | [**WskSend**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_send)                                                                                               |
| 受信                          | [**TDI\_受信**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff565131(v=vs.85))                                                     | [**WskReceive**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_receive)                                                                                         |
| アドレスの関連付け解除             | [**TDI\_\_アドレスの関連付けを解除します**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff565089(v=vs.85))                          | 該当なし                                                                                                                           |
| 受信ハンドラー                  | [**Clienteventreceive**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff545260(v=vs.85))、 [ **TDI\_受信**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff565131(v=vs.85)) | [*WskReceiveEvent*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_receive_event)                                                                                 |
| 接続ハンドラー                  | [**Clienteventconnect**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff544257(v=vs.85))、 [ **TDI\_CONNECT**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff565083(v=vs.85)) | [**WskAccept**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_accept)                                                                                           |
| ソケットまたは接続を閉じる       | [**ObDereferenceObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obdereferenceobject)または[ **zwclose**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntclose)    | [**WskCloseSocket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_close_socket)                                                                                 |

 

 

 





