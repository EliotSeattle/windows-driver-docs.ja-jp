---
title: DEVPKEY_Device_ProblemStatus
description: DEVPKEY_Device_ProblemStatus
ms.assetid: 477f835c-6094-4fba-80af-f6032bca7f85
keywords:
- デバイスとドライバーのインストールの DEVPKEY_Device_ProblemStatus
topic_type:
- apiref
api_name:
- DEVPKEY_Device_ProblemStatus
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 02/28/2020
ms.openlocfilehash: c5b6247f02b042cc29d590b4ca7a22f79f62b4db
ms.sourcegitcommit: 6f165a03303b7e4950b37d4b992f0f481b14f3ca
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/04/2020
ms.locfileid: "78279453"
---
# <a name="devpkey_device_problemstatus"></a>DEVPKEY_Device_ProblemStatus


DEVPKEY_Device_ProblemStatus デバイスプロパティは、問題コードが生成されたときに設定される NTSTATUS 値です。 問題コードが設定された理由について、より多くのコンテキストを提供します。 追加のコンテキストが使用できない場合は、STATUS_SUCCESS (0x00000000) として表示されます。


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>プロパティキー</strong></p></td>
<td align="left"><p>DEVPKEY_Device_ProblemStatus</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>プロパティ-データ型識別子</strong></p></td>
<td align="left"><p><a href="devprop-type-int32.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_NTSTATUS&lt;/strong&gt;](devprop-type-ntstatus.md)"><strong>DEVPROP_TYPE_NTSTATUS</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>プロパティアクセス</strong></p></td>
<td align="left"><p>インストールアプリケーションおよびインストーラーによる読み取り専用アクセス</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>た?</strong></p></td>
<td align="left"><p>いいえ</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>コメント
-------

デバイスマネージャーまたはカーネルデバッガーで問題の状態を検出する方法の詳細については、「[デバイスインスタンスの状態と問題のコードを取得](retrieving-the-status-and-problem-code-for-a-device-instance.md)する」を参照してください。

NTSTATUS 値の詳細については、「 [Ntstatus 値の使用](../kernel/using-ntstatus-values.md)」を参照してください。

[**Setupdigetdeviceproperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)を呼び出して、DEVPKEY_Device_ProblemStatus の値を取得できます。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>バージョン</p></td>
<td align="left"><p>Windows 8 以降のバージョンの Windows で使用できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ヘッダー</p></td>
<td align="left">Devpkey (Devpkey を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>参照


[**CM_Get_DevNode_Status**](https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_get_devnode_status)

[**SetupDiGetDeviceProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)

 

 






