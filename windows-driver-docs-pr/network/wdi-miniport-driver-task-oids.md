---
title: WDI タスク OID
description: このセクションには、WDI タスク Oid が含まれています。
ms.assetid: CAA92CA5-5CD6-4705-AA4C-54C1AA83ACA3
ms.date: 07/18/2017
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 696b2b320977be6341f37afc3354751ee6c6a5b5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842912"
---
# <a name="wdi-task-oids"></a>WDI タスク OID


このセクションには、WDI タスク Oid が含まれています。

Wi-fi Driver Interface (WDI) オブジェクト識別子 (Oid) は、WDI を実装するミニポートドライバーにのみ適用されます。

次の表では、WDI OID query (Q)、set (S)、および NDIS 6.0 method (M) 要求を実装するかどうかを指定します。

<a href="" id="r"></a> **\R\n\r\n**  
オブジェクトのサポートが必要であることを示します。 ミニポートドライバーは、 [*Miniportoidrequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_oid_request)関数からサポートされて\_いない状態コード NDIS\_status\_返すことによって、オブジェクトの設定またはクエリ要求に失敗しないようにする必要があります。

<a href="" id="o"></a>**I/o**  
オブジェクトのサポートが省略可能であることを示します。 ミニポートドライバーは、オブジェクトのクエリまたは設定要求をサポートすることができます。または、ドライバーが、[*ミニ Portoidrequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_oid_request)関数からサポートされて\_いない NDIS\_ステータス\_を返すことによって要求を失敗させることができます。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th>名前</th>
<th>Q</th>
<th>S</th>
<th>[M]</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="oid-wdi-task-change-operation-mode.md" data-raw-source="[OID_WDI_TASK_CHANGE_OPERATION_MODE](oid-wdi-task-change-operation-mode.md)">OID_WDI_TASK_CHANGE_OPERATION_MODE</a></p></td>
<td><p></p></td>
<td><p></p></td>
<td><p>R</p></td>
</tr>
<tr class="even">
<td><p><a href="oid-wdi-task-close.md" data-raw-source="[OID_WDI_TASK_CLOSE](oid-wdi-task-close.md)">OID_WDI_TASK_CLOSE</a></p></td>
<td><p></p></td>
<td><p></p></td>
<td><p>R</p></td>
</tr>
<tr class="odd">
<td><p><a href="oid-wdi-task-connect.md" data-raw-source="[OID_WDI_TASK_CONNECT](oid-wdi-task-connect.md)">OID_WDI_TASK_CONNECT</a></p></td>
<td><p></p></td>
<td><p></p></td>
<td><p>R</p></td>
</tr>
<tr class="even">
<td><p><a href="oid-wdi-task-create-port.md" data-raw-source="[OID_WDI_TASK_CREATE_PORT](oid-wdi-task-create-port.md)">OID_WDI_TASK_CREATE_PORT</a></p></td>
<td><p></p></td>
<td><p></p></td>
<td><p>R</p></td>
</tr>
<tr class="odd">
<td><p><a href="oid-wdi-task-delete-port.md" data-raw-source="[OID_WDI_TASK_DELETE_PORT](oid-wdi-task-delete-port.md)">OID_WDI_TASK_DELETE_PORT</a></p></td>
<td><p></p></td>
<td><p></p></td>
<td><p>R</p></td>
</tr>
<tr class="even">
<td><p><a href="oid-wdi-task-disconnect.md" data-raw-source="[OID_WDI_TASK_DISCONNECT](oid-wdi-task-disconnect.md)">OID_WDI_TASK_DISCONNECT</a></p></td>
<td><p></p></td>
<td><p></p></td>
<td><p>R</p></td>
</tr>
<tr class="odd">
<td><p><a href="oid-wdi-task-dot11-reset.md" data-raw-source="[OID_WDI_TASK_DOT11_RESET](oid-wdi-task-dot11-reset.md)">OID_WDI_TASK_DOT11_RESET</a></p></td>
<td><p></p></td>
<td><p></p></td>
<td><p>R</p></td>
</tr>
<tr class="even">
<td><p><a href="oid-wdi-task-ihv.md" data-raw-source="[OID_WDI_TASK_IHV](oid-wdi-task-ihv.md)">OID_WDI_TASK_IHV</a></p></td>
<td><p></p></td>
<td><p></p></td>
<td><p>O</p></td>
</tr>
<tr class="odd">
<td><p><a href="oid-wdi-task-open.md" data-raw-source="[OID_WDI_TASK_OPEN](oid-wdi-task-open.md)">OID_WDI_TASK_OPEN</a></p></td>
<td><p></p></td>
<td><p></p></td>
<td><p>O</p></td>
</tr>
<tr class="even">
<td><p><a href="oid-wdi-task-p2p-discover.md" data-raw-source="[OID_WDI_TASK_P2P_DISCOVER](oid-wdi-task-p2p-discover.md)">OID_WDI_TASK_P2P_DISCOVER</a></p></td>
<td><p></p></td>
<td><p></p></td>
<td><p>O</p></td>
</tr>
<tr class="odd">
<td><p><a href="oid-wdi-task-p2p-send-request-action-frame.md" data-raw-source="[OID_WDI_TASK_P2P_SEND_REQUEST_ACTION_FRAME](oid-wdi-task-p2p-send-request-action-frame.md)">OID_WDI_TASK_P2P_SEND_REQUEST_ACTION_FRAME</a></p></td>
<td><p></p></td>
<td><p></p></td>
<td><p>O</p></td>
</tr>
<tr class="even">
<td><p><a href="oid-wdi-task-p2p-send-response-action-frame.md" data-raw-source="[OID_WDI_TASK_P2P_SEND_RESPONSE_ACTION_FRAME](oid-wdi-task-p2p-send-response-action-frame.md)">OID_WDI_TASK_P2P_SEND_RESPONSE_ACTION_FRAME</a></p></td>
<td><p></p></td>
<td><p></p></td>
<td><p>O</p></td>
</tr>
<tr class="odd">
<td><p><a href="oid-wdi-task-request-ftm.md" data-raw-source="[OID_WDI_TASK_REQUEST_FTM](oid-wdi-task-request-ftm.md)">OID_WDI_TASK_REQUEST_FTM</a></p></td>
<td><p></p></td>
<td><p></p></td>
<td><p>O</p></td>
</tr>
<tr class="even">
<td><p><a href="oid-wdi-task-roam.md" data-raw-source="[OID_WDI_TASK_ROAM](oid-wdi-task-roam.md)">OID_WDI_TASK_ROAM</a></p></td>
<td><p></p></td>
<td><p></p></td>
<td><p>R</p></td>
</tr>
<tr class="odd">
<td><p><a href="oid-wdi-task-scan.md" data-raw-source="[OID_WDI_TASK_SCAN](oid-wdi-task-scan.md)">OID_WDI_TASK_SCAN</a></p></td>
<td><p></p></td>
<td><p></p></td>
<td><p>R</p></td>
</tr>
<tr class="even">
<td><p><a href="oid-wdi-task-send-ap-association-response.md" data-raw-source="[OID_WDI_TASK_SEND_AP_ASSOCIATION_RESPONSE](oid-wdi-task-send-ap-association-response.md)">OID_WDI_TASK_SEND_AP_ASSOCIATION_RESPONSE</a></p></td>
<td><p></p></td>
<td><p></p></td>
<td><p>O</p></td>
</tr>
<tr class="odd">
<td><p><a href="oid-wdi-task-send-request-action-frame.md" data-raw-source="[OID_WDI_TASK_SEND_REQUEST_ACTION_FRAME](oid-wdi-task-send-request-action-frame.md)">OID_WDI_TASK_SEND_REQUEST_ACTION_FRAME</a></p></td>
<td><p></p></td>
<td><p></p></td>
<td><p>O</p></td>
</tr>
<tr class="even">
<td><p><a href="oid-wdi-task-send-response-action-frame.md" data-raw-source="[OID_WDI_TASK_SEND_RESPONSE_ACTION_FRAME](oid-wdi-task-send-response-action-frame.md)">OID_WDI_TASK_SEND_RESPONSE_ACTION_FRAME</a></p></td>
<td><p></p></td>
<td><p></p></td>
<td><p>O</p></td>
</tr>
<tr class="odd">
<td><p><a href="oid-wdi-task-set-radio-state.md" data-raw-source="[OID_WDI_TASK_SET_RADIO_STATE](oid-wdi-task-set-radio-state.md)">OID_WDI_TASK_SET_RADIO_STATE</a></p></td>
<td><p></p></td>
<td><p></p></td>
<td><p>R</p></td>
</tr>
<tr class="even">
<td><p><a href="oid-wdi-task-start-ap.md" data-raw-source="[OID_WDI_TASK_START_AP](oid-wdi-task-start-ap.md)">OID_WDI_TASK_START_AP</a></p></td>
<td><p></p></td>
<td><p></p></td>
<td><p>O</p></td>
</tr>
<tr class="odd">
<td><p><a href="oid-wdi-task-stop-ap.md" data-raw-source="[OID_WDI_TASK_STOP_AP](oid-wdi-task-stop-ap.md)">OID_WDI_TASK_STOP_AP</a></p></td>
<td><p></p></td>
<td><p></p></td>
<td><p>O</p></td>
</tr>
</tbody>
</table>

 

 

 




