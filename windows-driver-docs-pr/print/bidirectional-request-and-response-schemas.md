---
title: 双方向の要求と応答のスキーマ
description: 双方向の要求と応答スキーマは、クエリやアプリケーションとプリンターの間の双方向通信のために使用する応答の XML 形式のセットを提供します。
ms.assetid: C005D90D-DCDB-410C-BD6F-83111849547E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0f3579ceb8517082c1bf90c9271f143e1054f45e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571709"
---
# <a name="bidirectional-request-and-response-schemas"></a>双方向の要求と応答のスキーマ


双方向の要求と応答スキーマは、クエリやアプリケーションとプリンターの間の双方向通信のために使用する応答の XML 形式のセットを提供します。 これらのクエリを使用して、アプリケーションはに従って格納されているプリンターの構成および状態データを取得できます、[双方向通信スキーマ](bidirectional-communication-schema.md)します。 任意の書き込み可能なプリンターのプロパティを設定することもできます。 いずれかを使用することができます、 [ **IBidiSpl2::SendRecvXMLStream** ](https://msdn.microsoft.com/library/windows/hardware/dd144983)または[ **IBidiSpl2::SendRecvXMLString** ](https://msdn.microsoft.com/library/windows/hardware/dd144984)との通信に関数プリンターです。

いくつかの要求スキーマと対応する応答のスキーマがあります。 次のトピックでは、それぞれの正式な定義と、それぞれの例があります。

[Get 要求および応答スキーマ](get-request-and-response-schemas.md)

[EnumSchema 要求および応答スキーマ](enumschema-request-and-response-schemas.md)

[セットの要求および応答スキーマ](set-request-and-response-schemas.md)

[GetWithArgument 要求および応答スキーマ](getwithargument-request-and-response-schemas.md)

任意の要求または応答のルート要素は、その型を識別します。 &lt;EnumSchema&gt;要求と応答を使用してアクセス可能なプリンターのプロパティの一覧を取得します。 &lt;取得&gt;と&lt;設定&gt;要求が複数のクエリを許可します。 A&lt;設定&gt;"query"が設定とそれに書き込む値プロパティの id だけです。

各&lt;クエリ&gt;スキーマがあるプロパティや読み書きされるプロパティの値を示す属性を = です。 これらのスキーマの値 = 属性は、双方向通信のスキーマのツリー内のパス。

たとえば、各&lt;取得&gt;応答が元のクエリのセットを繰り返し、それぞれに、結果を追加します。 各&lt;設定&gt;応答は、「クエリ」の元のセットを繰り返しますが、何も提供しますが成功するクエリの詳細。 いずれかのクエリが失敗した場合、&lt;取得&gt;または&lt;設定&gt;結果は、エラー メッセージを要求します。

要求の作成方法の詳細については、[双方向通信のスキーマのクエリを構築する](constructing-a-bidi-communication-schema-query.md)を参照してください。

双方向通信のスキーマの詳細については、次を参照してください。、[双方向通信スキーマ階層](bidirectional-communication-schema-hierarchy.md)と[双方向通信のスキーマ リファレンス](https://msdn.microsoft.com/library/windows/hardware/ff545175)トピック。

 

 



