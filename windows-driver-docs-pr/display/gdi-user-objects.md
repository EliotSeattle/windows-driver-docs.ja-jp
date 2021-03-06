---
title: GDI ユーザー オブジェクト
description: GDI ユーザー オブジェクト
ms.assetid: 25048f14-a46e-49bb-8890-699bf1324007
keywords:
- GDI WDK Windows 2000 の表示、ユーザー オブジェクト
- グラフィックス ドライバー WDK Windows 2000 の表示、ユーザー オブジェクト
- WDK の GDI やユーザー オブジェクトの描画
- WDK GDI のユーザー オブジェクト
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0ec5927ca3ceba3cbeca85ee4ffb39c6b657c924
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382348"
---
# <a name="gdi-user-objects"></a>GDI ユーザー オブジェクト


## <span id="ddk_gdi_user_objects_gg"></span><span id="DDK_GDI_USER_OBJECTS_GG"></span>


GDI は重要なは、内部データを構造化、いますと渡すことによってこれらの構造体のパブリック フィールドにドライバー アクセスは保持*ユーザー オブジェクト*します。 ユーザー オブジェクトは、GDI データ構造体とこれらの構造内の情報へのアクセスが必要なドライバーの間のインターフェイスを提供する中間のデータ構造です。 ドライバーは、クエリについては、またはさまざまなサービスを要求するには GDI にユーザー オブジェクトに、ポインターを渡すことができます。 パブリック フィールドを持つユーザーのオブジェクトには次の利点があります。

-   内部の GDI データ構造体への直接アクセスに関連する問題がなくなります。

-   ドライバーの GDI データを保持する場所を提供します。 たとえば、PATHOBJ 構造体には、パスのような複雑なオブジェクトを列挙するために必要なすべての余分なデータを保持できます。

次のユーザー オブジェクトを使用できます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">オブジェクト</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-_brushobj" data-raw-source="[&lt;strong&gt;BRUSHOBJ&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-_brushobj)"><strong>BRUSHOBJ</strong></a></p></td>
<td align="left"><p>線、テキスト、または塗りつぶしを出力する関数のグラフィック ブラシ オブジェクトを定義します。 ドライバーを呼び出すことができます<a href="https://docs.microsoft.com/windows-hardware/drivers/#wdkgloss-brushobj" data-raw-source="&lt;em&gt;BRUSHOBJ&lt;/em&gt;"> <em>BRUSHOBJ</em> </a> services ブラシを実現する、または実現 GDI によって以前にキャッシュを検索します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-_clipobj" data-raw-source="[&lt;strong&gt;CLIPOBJ&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-_clipobj)"><strong>CLIPOBJ</strong></a></p></td>
<td align="left"><p>アクセスに、ドライバーを提供します、 <a href="https://docs.microsoft.com/windows-hardware/drivers/#wdkgloss-clip-region" data-raw-source="&lt;em&gt;clip region&lt;/em&gt;"><em>クリップ領域</em></a>の描画や情報を入力します。 このリージョンは、一連の四角形として列挙できます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-_floatobj" data-raw-source="[&lt;strong&gt;FLOATOBJ&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-_floatobj)"><strong>FLOATOBJ</strong></a></p></td>
<td align="left"><p>グラフィックスの浮動小数点演算をエミュレートするためにドライバーを許可します。 その他のすべてのカーネル モード ドライバーは、浮動小数点演算が無効になります。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-_fontobj" data-raw-source="[&lt;strong&gt;FONTOBJ&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-_fontobj)"><strong>FONTOBJ</strong></a></p></td>
<td align="left"><p>については、特定のインスタンス (または実現) フォントへのドライバーへのアクセスを提供します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-_palobj" data-raw-source="[&lt;strong&gt;PALOBJ&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-_palobj)"><strong>PALOBJ</strong></a></p></td>
<td align="left"><p>パレットの色の RGB; を含む構造体使用してアクセスできる、 <a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-palobj_cgetcolors" data-raw-source="&lt;strong&gt;PALOBJ_cGetColors&lt;/strong&gt;"> <em>PALOBJ</em> </a>構造にパブリック メンバーが含まれていません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-_pathobj" data-raw-source="[&lt;strong&gt;PATHOBJ&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-_pathobj)"><strong>PATHOBJ</strong></a></p></td>
<td align="left"><p>指定するパスを定義します (行やベジエ曲線) を描画します。 A <a href="https://docs.microsoft.com/windows-hardware/drivers/#wdkgloss-pathobj" data-raw-source="&lt;em&gt;PATHOBJ&lt;/em&gt;"> <em>PATHOBJ</em> </a>構造が一連の行と線を付けるか、入力をベジエ曲線を記述するドライバーに渡されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-_strobj" data-raw-source="[&lt;strong&gt;STROBJ&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-_strobj)"><strong>STROBJ</strong></a></p></td>
<td align="left"><p>ドライバーのグリフのハンドルとテキスト文字列の描画方法を説明する位置の一覧を列挙します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-_surfobj" data-raw-source="[&lt;strong&gt;SURFOBJ&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-_surfobj)"><strong>SURFOBJ</strong></a></p></td>
<td align="left"><p>GDI ビットマップ、デバイス依存ビットマップ、またはデバイス管理の画面が画面を識別します。 参照してください<a href="surface-types.md" data-raw-source="[Surface Types](surface-types.md)">画面型</a>詳細についてはします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff570618(v=vs.85)" data-raw-source="[&lt;strong&gt;XFORMOBJ&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff570618(v=vs.85))"><strong>XFORMOBJ</strong></a></p></td>
<td align="left"><p>ジオメトリのワイド線など、任意線形 2 次元変換をについて説明します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-_xlateobj" data-raw-source="[&lt;strong&gt;XLATEOBJ&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-_xlateobj)"><strong>XLATEOBJ</strong></a></p></td>
<td align="left"><p>ソースのサーフェス形式からピクセルを宛先表面形式に変換するために必要な翻訳を定義します。</p></td>
</tr>
</tbody>
</table>

 

 

 





