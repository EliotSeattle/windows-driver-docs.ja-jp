---
title: ベジェ曲線
description: ベジェ曲線
ms.assetid: 322ff79b-e5b8-4247-99eb-1aa3779216ef
keywords:
- GDI WDK Windows 2000 の表示、曲線、ベジエ
- グラフィック ドライバー WDK Windows 2000 を表示、曲線、ベジエ
- WDK の GDI やベジエ曲線の描画
- 3 次スプライン WDK GDI
- ベジエ曲線 WDK GDI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 02a59523a38e61f4110dff43e7ff98581654a04f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384623"
---
# <a name="bezier-curves"></a>ベジェ曲線


## <span id="ddk_bezier_curves_gg"></span><span id="DDK_BEZIER_CURVES_GG"></span>


曲線の汎用的なプリミティブであるベジエ曲線 (3 次スプライン) を含むパスをハードウェア デバイスに描画できるいくつか高度な。 そのため、ドライバーが内のこれらの曲線のサポートを含めることができる場合、 [ **DrvStrokePath** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvstrokepath)関数。

GDI は、デバイス管理の画面で、ベジエ曲線のパスを描画する必要があります、ときに、GCAPS がテストされます\_ベジエ曲線のフラグ (で、 [ **DEVINFO** ](https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-tagdevinfo)構造体) を呼び出してかどうかを判断する[ **DrvStrokePath**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvstrokepath)します。 呼び出された場合、この関数は、要求された操作を実行します。 いずれかまたは幾何学的線のと同じようにそれを処理していませんが決定します。 後者の場合、GDI 要求に分かれますより単純な操作は、たとえば、行の概数を曲線に変換しています。

 

 





