---
title: Debugger Data Model - オペランド オブジェクト
description: マシン命令の各オペランドはオペランドのオブジェクトによってについて説明します。
ms.date: 12/12/2018
ms.localizationpriority: medium
ms.openlocfilehash: b94c971aea0cfaaa29db818112118b4574a61624
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63376067"
---
# <a name="operand-objects"></a>オペランドのオブジェクト 
## <a name="summary"></a>概要
マシン命令の各オペランドはオペランドのオブジェクトによってについて説明します。 オペランドの文字列の変換は、全体の命令の文字列の変換の一部になります。 
## <a name="object-properties"></a>オブジェクトのプロパティ
|名前|説明|
|--- |--- |
|属性|[オペランド属性](dbgmodel-object-operand-attributes.md)オペランドの特定の側面を記述するオブジェクト。|
|レジスタ|A[コレクション](dbgmodel-namespace-collections.md)の[登録](dbgmodel-object-register.md)オペランドを使用するすべてのレジスタを記述するオブジェクト。|