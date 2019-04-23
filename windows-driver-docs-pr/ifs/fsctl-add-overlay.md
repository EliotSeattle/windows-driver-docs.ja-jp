---
title: FSCTL_ADD_OVERLAY 制御コード
description: FSCTL\_追加\_オーバーレイ コントロールのコードは、ボリュームの名前空間に新しいバックアップを外部ソースを追加します。 このバックアップ ソースでは、Windows Image Format (WIM) ファイルを指定できます。
ms.assetid: 0507ECDE-49C6-4EC4-87D6-76D6475620F4
keywords:
- FSCTL_ADD_OVERLAY 制御コード インストール可能なファイル システム ドライバー
topic_type:
- apiref
api_name:
- FSCTL_ADD_OVERLAY
api_location:
- ntifs.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 53b4ceecfa7e9a541a53d8fd28febc1bd1bcb114
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571742"
---
# <a name="fsctladdoverlay-control-code"></a>FSCTL\_追加\_オーバーレイ コントロール コード


**FSCTL\_追加\_オーバーレイ**制御コードは、ボリュームの名前空間に新しいバックアップを外部ソースを追加します。 このバックアップ ソースでは、Windows Image Format (WIM) ファイルを指定できます。

この操作を実行するには、呼び出す[ **FltFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff542988)または[ **ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)次のパラメーターを使用します。

**Parameters**

<a href="" id="instance--in-"></a>*インスタンス\[で\]*  
[**FltFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff542988)のみです。 呼び出し元の非透過インスタンス ポインター。 このパラメーターは、必要なは、NULL にすることはできません。

<a href="" id="fileobject--in-"></a>*FileObject\[で\]*  
[**FltFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff542988)のみです。 オーバーレイを追加するボリュームのファイル ポインター オブジェクト。 このパラメーターは、必要なは、NULL にすることはできません。

<a href="" id="filehandle--in-"></a>*FileHandle\[で\]*  
[**ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)のみです。 オーバーレイが追加されます、ボリュームのハンドル。 このパラメーターは、必要なは、NULL にすることはできません。

<a href="" id="fscontrolcode--in-"></a>*FsControlCode\[で\]*  
操作の制御コード。 使用**FSCTL\_追加\_オーバーレイ**この操作にします。

<a href="" id="inputbuffer"></a>*InputBuffer*  
含める必要がありますが、入力バッファーへのポインターを[ **WOF\_外部\_情報**](https://msdn.microsoft.com/library/windows/hardware/dn632452)構造体。 追加のプロバイダー固有のデータは後すぐに、必要な場合に**WOF\_外部\_情報**します。

<a href="" id="inputbufferlength--in-"></a>*InputBufferLength\[で\]*  
設定**sizeof**([**WOF\_外部\_情報**](https://msdn.microsoft.com/library/windows/hardware/dn632452)) さらに、追加のプロバイダーの入力データのサイズ。

<a href="" id="outputbuffer--out-"></a>*OutputBuffer\[アウト\]*  
追加操作の結果情報を含む出力バッファーへのポインター。

<a href="" id="outputbufferlength--out-"></a>*OutputBufferLength\[アウト\]*  
バッファーのサイズが指す*OutputBuffer*します。

<a name="status-block"></a>ステータス ブロック
------------

[**FltFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff542988)または[ **ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)ステータスを返します\_操作が成功した場合は成功します。 それ以外の場合、適切な関数では NTSTATUS 値は次のいずれかを返す可能性があります。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">項目</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>STATUS_ACCESS_DENIED</strong></p></td>
<td align="left"><p>リクエスターでは、管理者特権はありません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_BUFFER_TOO_SMALL</strong></p></td>
<td align="left"><p>によって示される出力バッファーの長さ<em>OutputBuffer</em>とで指定した<em>OutputBufferLength</em>、小さすぎます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>STATUS_INTERNAL_ERROR</strong></p></td>
<td align="left"><p>要求されたボリュームにアクセスできません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_INVALID_DEVICE_REQUEST</strong></p></td>
<td align="left"><p>バックアップ サービスが存在しないか開始されていません。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>コメント
-------

追加のバックアップ ソースは、Windows Imaging Format (WIM) ファイルが、入力バッファーに格納されます、 [ **WOF\_外部\_情報**](https://msdn.microsoft.com/library/windows/hardware/dn632452)構造が続く、 [**WIM\_プロバイダー\_追加\_オーバーレイ\_入力**](https://msdn.microsoft.com/library/windows/hardware/dn632447)構造体。 *InputBufferLength*ここでは、 **sizeof**(**WOF\_外部\_情報**) + **sizeof**(**WIM\_プロバイダー\_追加\_オーバーレイ\_入力**)。 要求の完了時に、データによって示される*OutputBuffer*含む 1 つの大きな\_WIM ファイルの新しいデータ ソース識別子を指定する整数値。

その他のバックアップ プロバイダーでは、独自の特定の入力パラメーターの構造を定義し、データ型を出力します。

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>バージョン</p></td>
<td align="left"><p>Windows 8.1 Update 以降を利用できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Ntifs.h (Ntifs.h または Fltkernel.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**FSCTL\_削除\_オーバーレイ**](fsctl-remove-overlay.md)

[**FSCTL\_SUSPEND\_オーバーレイ**](fsctl-suspend-overlay.md)

[**FSCTL\_UPDATE\_オーバーレイ**](fsctl-update-overlay.md)

[**FSCTL\_取得\_外部\_バックアップ**](fsctl-get-external-backing.md)

[**FSCTL\_設定\_外部\_バックアップ**](fsctl-set-external-backing.md)

 

 





