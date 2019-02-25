---
title: 形式の画面を使用して 2D 操作のためのレポートのサポート
description: 形式の画面を使用して 2D 操作のためのレポートのサポート
ms.assetid: c7737daf-3342-48dc-a365-f789b7203013
keywords:
- 2 次元操作 WDK DirectX 9.0、画面の書式設定します。
- WDK DirectX 9.0 2D 操作は、画面の書式設定します。
- 画面は、WDK DirectX 9.0 をフォーマットします。
- 画面形式 WDK DirectX 9.0、レポートの 2D 操作のサポート
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e330d894a99852d7feead255a795c2a04596155c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528680"
---
# <a name="reporting-support-for-2d-operations-using-surface-formats"></a>形式の画面を使用して 2D 操作のためのレポートのサポート


## <span id="ddk_reporting_support_for_2d_operations_using_surface_formats_gg"></span><span id="DDK_REPORTING_SUPPORT_FOR_2D_OPERATIONS_USING_SURFACE_FORMATS_GG"></span>


ドライバーでフラグを指定する、 **dwOperations**のメンバー、 [ **DDPIXELFORMAT** ](https://msdn.microsoft.com/library/windows/hardware/ff550274)サーフェスの形式を使用して 2D 操作を実行できることを示すための構造その形式。

ドライバーことまたはからにコピーし、D3DFORMAT を設定して、画面に塗りつぶしの色を指定するたとえば、\_OP\_OFFSCREENPLAIN フラグ。

ドライバーはベンダーから提供されたコードや、D3DFORMAT からのコードを使用する場合の列挙型を設定する、 **dwFourCC** DDPIXELFORMAT と割り当て画面、ドライバーの形式のメンバーでは、D3DFORMAT を使用できますも\_OP\_変換\_TO\_ARGB と D3DFORMAT\_MEMBEROFGROUP\_ARGB 色変換をソースとターゲットのサーフェスの間で実行できないかどうかを示すフラグ。 D3DFORMAT を持つターゲット サーフェスは、\_MEMBEROFGROUP\_ARGB フラグが設定を示す D3DFORMAT を持つ任意のソース画面から色の書式を変換できることを示します\_OP\_変換\_TO\_ARGB フラグを設定します。

ドライバーでは、D3DFORMAT を指定できますのみ\_MEMBEROFGROUP\_ターゲット画面形式の場合、少なくとも 5 ビットのカラー チャネルあたりの ARGB フラグ。 D3DFMT つまり\_設定されている A1R5G5B5 形式、 **dwFourCC** DDPIXELFORMAT のメンバーは有効です。 ただし、D3DFMT\_A4R4G4B4 形式が無効です。 D3DFORMAT を指定するときに、ドライバーは特定のソース画面形式に制限も\_OP\_変換\_TO\_ARGB フラグ。 ソースの形式は、D3DFORMAT に対して有効な任意の形式を指定できます\_MEMBEROFGROUP\_ARGB フラグまたは*FOURCC*サーフェスの形式。

反 D3DFORMAT\_OP\_変換\_TO\_ARGB と D3DFORMAT\_MEMBEROFGROUP\_ARGB ARGB 形式を示すため、ランタイムは、サーフェスを指定するドライバーもことができます。XRGB 形式 (たとえば、D3DFMT\_X1R5G5B5)。 ドライバーが D3DFORMAT を指定する場合\_MEMBEROFGROUP\_ARGB または D3DFORMAT\_OP\_変換\_TO\_ARGB 形式が無効です、ランタイムでは、読み込みを Direct3D HAL を禁止します。

 

 




