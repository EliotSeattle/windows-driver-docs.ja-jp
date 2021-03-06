---
title: FSCTL_OFFLOAD_WRITE 制御コード
description: FSCTL\_OFFLOAD\_書き込み制御コードは、オフロード書き込みプリミティブをサポートするストレージシステム内のデータブロックに対してオフロード書き込みを開始します。
ms.assetid: A40C6D4C-D31D-423E-B7B0-51151EEDD30F
keywords:
- FSCTL_OFFLOAD_WRITE 制御コードのインストール可能なファイルシステムドライバー
topic_type:
- apiref
api_name:
- FSCTL_OFFLOAD_WRITE
api_location:
- ntifs.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6d95cc553f0fad68da7224c047b5e296fcb91c86
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841279"
---
# <a name="fsctl_offload_write-control-code"></a>FSCTL\_オフロード\_書き込み制御コード


**FSCTL\_offload\_書き込み**制御コードは、オフロード書き込みプリミティブをサポートするストレージシステム内のデータブロックに対してオフロード書き込みを開始します。

この操作を実行するには、ミニフィルタードライバーは、次のパラメーターを使用して[**Fltfscontrolfile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)を呼び出します。ファイルシステム、リダイレクター、およびレガシファイルシステムフィルタードライバーは、次のパラメーターを使用して[**zwfscontrolfile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)を呼び出します。

**Parameters**

<a href="" id="instance--in-"></a> *\]のインスタンス \[*  
[**Fltfscontrolfile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)のみ。 呼び出し元の非透過インスタンスポインター。 このパラメーターは必須であり、NULL にすることはできません。

<a href="" id="fileobject--in-"></a> *\]の FileObject \[*  
[**Fltfscontrolfile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)のみ。 書き込み先のファイルを指定するファイルポインターオブジェクト。 このパラメーターは必須であり、NULL にすることはできません。

<a href="" id="filehandle--in-"></a> *\]の FileHandle \[*  
[**Zwfscontrolfile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)のみ。 書き込み先のファイルのファイルハンドル。 このパラメーターは必須であり、NULL にすることはできません。

<a href="" id="fscontrolcode--in-"></a> *\]の FsControlCode \[*  
操作の制御コード。 この操作には、 **FSCTL\_オフロード\_書き込み**を使用します。

<a href="" id="inputbuffer"></a>*InputBuffer*  
読み取り対象のデータブロックのサイズとオフセットを格納している、 [**FSCTL\_オフロード\_書き込み\_入力**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_fsctl_offload_write_input)構造体へのポインター。

<a href="" id="inputbufferlength--in-"></a> *\]内の InputBufferLength \[*  
*InputBuffer*が指すバッファーのサイズ (バイト単位)。 この値は**sizeof**(FSCTL\_OFFLOAD\_WRITE\_INPUT) です。

<a href="" id="outputbuffer--out-"></a>*OutputBuffer \[out\]*  
読み取り対象のデータブロックのサイズとオフセットを格納している、 [**FSCTL\_オフロード\_書き込み\_入力**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_fsctl_offload_write_input)構造体へのポインター。

<a href="" id="outputbufferlength--out-"></a>*OutputBufferLength \[out\]*  
*Outputbuffer*パラメーターが指すバッファーのサイズ (バイト単位)。 この値は、少なくとも**sizeof**(FSCTL\_OFFLOAD\_読み取り\_出力) である必要があります。

<a name="status-block"></a>ステータス ブロック
------------

[**Fltfscontrolfile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)または[**zwfscontrolfile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)は、操作が成功した場合に STATUS\_SUCCESS を返します。 それ以外の場合、適切な関数は、次のいずれかの NTSTATUS 値を返す可能性があります。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">用語</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>STATUS_INVALID_DEVICE_REQUEST</strong></p></td>
<td align="left"><p>指定されたハンドルは、有効なファイルハンドルではありません。</p></td>
</tr>
<tr class="even">
<td align="left"><p> <strong>STATUS_INVALID_PARAMETER</strong></p></td>
<td align="left"><p>ファイルサイズが PAGE_SIZE 未満です。</p>
<p>\- または -</p>
<p><em>Inputbufferlength</em> &lt; <strong>sizeof</strong>(FSCTL_OFFLOAD_WRITE_INPUT)。</p>
<p>\- または -</p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_fsctl_offload_write_input" data-raw-source="[&lt;strong&gt;FSCTL_OFFLOAD_WRITE_INPUT&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_fsctl_offload_write_input)"><strong>FSCTL_OFFLOAD_WRITE_INPUT</strong></a>の1つ以上のメンバーが正しくありません。</p>
<strong>Fileoffset</strong>は、ボリュームの論理セクターサイズの倍数ではありません。
<strong>Copylength</strong>は、ボリュームの論理セクターサイズの倍数ではありません。
<strong>Transferoffset</strong>は、ボリュームの論理セクターサイズの倍数ではありません。
<strong>Size</strong>は、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_fsctl_offload_write_input" data-raw-source="[&lt;strong&gt;FSCTL_OFFLOAD_WRITE_INPUT&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_fsctl_offload_write_input)"><strong>FSCTL_OFFLOAD_WRITE_INPUT</strong></a>構造体のサイズではありません。
<strong>Fileoffset</strong> &gt; ファイルの有効なデータ長 (VDL) です。
<strong>Fileoffset</strong> + <strong>Copylength</strong> &gt; <strong>MAXULONGLONG</strong>。</td>
</tr>
<tr class="odd">
<td align="left"><p><strong>STATUS_NOT_SUPPORTED</strong></p></td>
<td align="left"><p>オフロード読み取り操作は、このボリュームではサポートされていません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_OFFLOAD_WRITE_FILE_NOT_SUPPORTED</strong></p></td>
<td align="left"><p>要求されたファイルの種類はサポートされていません。 次のファイルの種類では、オフロード操作はサポートされていません。</p>
<ul>
<li>トランザクションファイル (TxF)</li>
<li>非ユーザーファイル</li>
<li>圧縮されたファイル</li>
<li>スパース ファイル</li>
<li>暗号化されたファイル</li>
<li>NTFS Metatdata ファイル</li>
</ul></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>STATUS_TOO_LATE</strong></p></td>
<td align="left"><p>マウント解除後にボリュームに書き込み操作を実行しようとしました。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_FILE_DELETED</strong></p></td>
<td align="left"><p>このファイルのデータストリームは無効です。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>STATUS_FILE_CLOSED</strong></p></td>
<td align="left"><p>ファイルハンドルは閉じられています。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_INVALID_HANDLE</strong></p></td>
<td align="left"><p>指定されたファイルハンドルは無効です。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>STATUS_FILE_LOCK_CONFLICT</strong></p></td>
<td align="left"><p>現在のファイルロック状態のため、読み取りまたは書き込みアクセス権を付与できません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_END_OF_FILE</strong></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_fsctl_offload_write_input" data-raw-source="[&lt;strong&gt;FSCTL_OFFLOAD_WRITE_INPUT&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_fsctl_offload_write_input)"><strong>FSCTL_OFFLOAD_WRITE_INPUT</strong></a>の<strong>fileoffset</strong>メンバーは、ファイルの終わり (EOF) の後に始まります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>STATUS_DISMOUNTED_VOLUME</strong></p></td>
<td align="left"><p>マウント解除されたボリュームでオフロード書き込みを行うことはできません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_MEDIA_WRITE_PROTECTED</strong></p></td>
<td align="left"><p>ボリュームは読み取り専用です。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>STATUS_INSUFFICIENT_RESOUCES</strong></p></td>
<td align="left"><p>要求を完了するために使用できるリソースが不足しています。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_BUFFER_TOO_SMALL</strong></p></td>
<td align="left"><p><em>InputBuffer</em>が<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_fsctl_offload_write_input" data-raw-source="[&lt;strong&gt;FSCTL_OFFLOAD_WRITE_INPUT&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_fsctl_offload_write_input)"><strong>FSCTL_OFFLOAD_WRITE_INPUT</strong></a>構造体を含むようにするには、 <em>inputbufferlength</em>が小さすぎます。</p>
<p>\- または -</p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_fsctl_offload_write_output" data-raw-source="[&lt;strong&gt;FSCTL_OFFLOAD_WRITE_OUTPUT&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_fsctl_offload_write_output)"><strong>FSCTL_OFFLOAD_WRITE_OUTPUT</strong></a>構造体を受け取る<em>Outputbuffer</em>の<em>outputbufferlength</em>が小さすぎます。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

オフロード読み取りは、通常のファイルに対してのみ使用できます。 サポートされてい\_ないファイルの種類の一覧については、[**ステータス\_オフロード\_書き込み\_\_ファイルを書き込む**] の説明を参照してください。

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
<td align="left"><p>Windows 8 以降で使用できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Ntifs (Ntifs または Fltkernel .h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**FltFsControlFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)

[**ZwFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)

[**FSCTL\_オフロード\_書き込み\_入力**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_fsctl_offload_write_input)

[**FSCTL\_オフロード\_書き込み\_出力**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_fsctl_offload_write_output)

 

 






