---
title: GDL テンプレート資格
description: GDL テンプレート資格
ms.assetid: 6a0fef55-4097-4d5b-b192-ce8a03b9c41f
keywords:
- テンプレートのテンプレートに関連付けるキーワードの WDK GDL
- キーワード WDK GDL、テンプレートに関連付けるキーワード
- WDK GDL、アソシエーションのテンプレートの検索条件
- アソシエーションの検索条件 WDK GDL
- GDL WDK、エントリを検索
- GDL WDK、エントリ
- テンプレートを GDL エントリを表す該当の WDK GDL
- WDK GDL、派生テンプレートのテンプレート
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ff92b14bc2dea64ae09253ba86dd670cb4bf322f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390599"
---
# <a name="gdl-template-qualification"></a>GDL テンプレート資格


テンプレートとそのテンプレート フォームから直接または間接的に派生したすべてのテンプレート、*継承ツリー*または*サブツリー*します。 ただし、再定義されているテンプレートを派生\*名の構成要素は、このツリーから除外されます。

テンプレートを指定するときに、\*のメンバーの一覧 GDL パーサーは、名前付きのテンプレートとの関連付けの候補として名前付きのテンプレートから派生したすべてのテンプレートを考慮します。 この継承ツリーを修飾するには、複数のテンプレートがある場合、パーサーは最も近いデータ エントリに関連付ける条件に一致するテンプレートを選択します。 指定されたデータのエントリを表すテンプレートとしての要件を満たすテンプレートは、次の条件を満たす必要があります。

-   として宣言されているテンプレート\*仮想が自動的にそれに適合しません。 ただし、派生テンプレートと見なされます。

-   テンプレートの\*名前コンストラクトは、データ エントリのキーワードに一致する必要があります。 なお、\*名前を継承することができます。

-   データ エントリのコンス トラクターをテンプレートの 1 つの要素である\*インスタンスの一覧は、データ構造のインスタンス名と一致する必要があります。 また、条件を満たすテンプレートが継承するすべての基本テンプレートは、この要件を満たすもする必要があります。 継承チェーンのすべてのテンプレートが必要です、\*エントリをインスタンスこのエントリがないものは既定でこの要件が満たされてに使用されます。

-   継承ツリーには、複数のテンプレートが適用されると、次の追加条件と見なされます。
    -   既定では、または、ワイルドカードを使用して、継承チェーン内のすべてのテンプレートがインスタンス名要件を満たすことで、テンプレートが適用される場合&lt;ANY&gt;し、もう 1 つの条件を満たすテンプレートに 1 つまたは複数のテンプレートがある場合は、その継承内チェーンは、明示的な一致では、インスタンス名の要件を満たすため、明示的な一致を使用するテンプレートを使用します。
    -   残りの条件を満たすテンプレートの最も派生テンプレートが使用されます。
    -   残りの条件を満たすテンプレートでは、最近に定義されたテンプレートが使用されます。

 

 




