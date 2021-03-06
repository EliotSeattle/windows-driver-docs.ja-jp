---
title: 3D 製造のキーワードの概要
description: 印刷スキーマ3D 製造のキーワードは、デバイスの機能やデバイス構成の選択した設定に対して可能な設定を指定します。
ms.assetid: D78EB9E6-584A-419C-B320-8962CDCC966E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e8ba8df870c36290f2aa8db00c3afe869c746cbb
ms.sourcegitcommit: ab64169b631da4db3f0b895600f1c38a22cb7e2e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/03/2020
ms.locfileid: "75652790"
---
# <a name="3d-manufacturing-keywords-overview"></a>3D 製造のキーワードの概要


印刷スキーマ3D 製造のキーワードは、3D 製造デバイスの機能の設定、または特定のデバイス構成の選択した設定を識別します。 これらのキーワードはそれぞれ、明確に定義された方法で特定の概念を記述し、3D 製造用の印刷スキーマドキュメントのプロデューサーとコンシューマーの間の設定の通信を明確にします。

プロデューサーとコンシューマーは、private キーワード拡張機能の同様の機能にキーワードを定義することを優先するために、Print Schema 3D 製造キーワードを使用する必要があります。 キーワードは、 **name**属性を使用して個々の印刷スキーマフレームワーク要素を識別します。 特定のキーワードに指定された名前は、キーワードが表す設定または特性を代表するものである必要があります。

PrintCapabilities または PrintTicket ドキュメント内に出現するキーワードインスタンスは、この記事のセクション1.6 で定義されているスコーププレフィックス規則に準拠している必要があります。 スコーププレフィックスの詳細については、「印刷スキーマの仕様」の5.4 「スコーププレフィックス」を参照してください。

## <a name="11-xml-namespaces"></a>1.1. XML 名前空間


3D 製造用の印刷スキーマキーワードの名前空間 URI は次のとおりです。

```xml
https://schemas.microsoft.com/3dmanufacturing/2013/01/pskeywords3d
```

この仕様では、名前空間プレフィックス**psk3d:** は、3d 製造名前空間の印刷スキーマキーワードから描画された要素、属性、および属性値を示すために使用されます。 プロデューサーは、関連する印刷スキーマ名前空間の名前空間宣言に関連付けられている名前空間プレフィックスを使用して、プレフィックスの付いた要素、属性、または属性値を生成する必要があります。 コンシューマーは名前空間の宣言に対して名前空間プレフィックスを解決して、修飾名が正しい名前空間から描画されるようにする必要があります。 コンシューマーは、名前空間プレフィックス**psk3d:** が正しく宣言され、3d 製造名前空間の Print スキーマキーワードに関連付けられている必要があります。 個々のプロデューサーは、3D 製造名前空間プレフィックスに異なる印刷スキーマキーワードを使用するか、この名前空間を既定の名前空間として宣言し、この名前空間から描画された要素、属性、および属性値の名前空間プレフィックスを省略します。 ただし、このキーワードの名前空間を既定の名前空間に割り当てることはお勧めしません。

この仕様では、名前空間プレフィックス**vnd:** は、ベンダー定義の名前空間から抽出されたプライベートキーワード拡張属性値を示すためにのみ使用されます。 ベンダーは、定義する名前空間ごとに独自の一意の名前空間プレフィックスを定義する必要があります。 ベンダーは、名前空間の**vnd:** 名前空間プレフィックスを定義しないでください。 プロデューサーは、 **vnd:** 名前空間を使用する印刷スキーマドキュメントを生成することはできません。

さらに、この仕様では、名前空間プレフィックス xsd: を使用して、XML スキーマ名前空間から描画された要素と属性を示します。また、XML スキーマインスタンス名前空間から取得した要素と属性を示すために、名前空間プレフィックス**xsi:** が使用されます。 この仕様または印刷スキーマ仕様の XSD スキーマまたはその他の要件によって明示的に許可されている場合を除き、XML コンテンツには、"xml" または "xsi" 名前空間から抽出された要素または属性を含めることはできません。

印刷スキーマフレームワークのコンテキストで使用するために定義されている追加の XML 要件と名前空間については、「1.2」の「印刷スキーマでの XML Usage」を参照してください。

## <a name="12-3d-manufacturing-keywords-versioning"></a>1.2. 3D 製造キーワードのバージョン管理


この仕様は、新しいキーワードで定期的に更新される場合があります。 前方互換性と下位互換性を確保するために、新しい一連のキーワードにはそれぞれ一意の名前空間が割り当てられます。 特定の名前空間で定義されているキーワードは、そのキーワードセットが実稼働用にリリースされた後に変更または拡張されることはありません。 詳細については、「印刷スキーマの仕様」の「1.3.2」を参照してください。

## <a name="13-common-keyword-terminology"></a>1.3. 一般的なキーワードに関する用語


このセクションの用語では、この仕様の残りの部分で特定の3D 製造キーワードを記述するための基本的なフレームワークとボキャブラリについて説明します。

### <a name="131-model"></a>1.3.1. モデル

この仕様では、*モデル*は、単一のジョブとして3d 製造プロセスによって作成される1つまたは複数のオブジェクトを参照します。 これには、単一のオブジェクト、複数の同種オブジェクト、複数の異種オブジェクト、別のオブジェクトで完全に囲まれたオブジェクト、またはインタロックされた分離不可能な*アセンブリ*内の複数のオブジェクトが含まれる場合があります。

### <a name="132-coordinate-space"></a>1.3.2. 座標空間

3D 製造印刷スキーマのキーワードは、右側の座標空間に基づいており、正の XYZ 空間にモデル座標が表示されます。 プロデューサーとコンシューマーは、出力フィールドの右側に x 軸、y 軸が出力フィールドの後ろに増加し、z 軸を使用して、座標空間の原点を定義し、[印刷出力] フィールドの左下隅にマップする必要があります。[出力] フィールドの上部に増加します。

プロデューサーとコンシューマーは、座標空間の単位解像度を1ミクロンとして使用する必要があります。 3D 製造キーワードの印刷スキーマを適用する前に、モデルをこの座標空間に変換する必要があります。

![座標空間](images/coordinate-space.png)

### <a name="133-relative-directions-and-measurement"></a>1.3.3. 相対方向と測定値

この仕様の相対的な方向は、次のように定義されています。 *Top*という用語は、最大印刷可能な Z 値を持つ座標空間の XY 平面を指します。 [*下*] という用語は、座標空間の最小印刷可能な xy 平面を表します。これは、Z 値が0の xy 平面として定義されています。 通常、これは印刷ベッドの表面と一致します。 *左側*の用語は、座標空間の印刷可能な最小の平面を指します。これは、X 値が0の yz 平面として定義されています。 *右側*という用語は、最大印刷可能な X 値を持つ座標空間の YZ 平面を指します。 *Front*という用語は、座標空間の印刷可能な最小の XZ 平面を指し、Y 値が0の xz 平面として定義されています。 "*戻る*" という用語は、最大印刷可能な Y 値を持つ座標空間の XZ 平面を指します。

これらの用語はモデルにも適用されます。この場合、この仕様で定義されている座標空間に変換されると、モデルの境界ボックスに対して相対的に定義されます。

プロデューサーとコンシューマーは、この仕様で定義されている座標空間に関連する相対座標を解釈する必要があります。

## <a name="14-interpreting-keyword-descriptions"></a>1.4. キーワードの説明の解釈


このドキュメントでは、いくつかの標準テーブルのいずれかを使用して、印刷スキーマ3D 製造キーワードが指定されています。 これらの各テーブルの内容と要件は、「5.2」を参照してください。

## <a name="15-keyword-usage-in-print-schema-documents"></a>1.5. 印刷スキーマドキュメントでのキーワードの使用


印刷スキーマ3D 製造キーワードは、この仕様で明示的に記述されていないコンテキストでは使用できません。

Private キーワード拡張を含む**name**属性値を持つ要素は、印刷スキーマフレームワークで許可されているすべての要素の子である場合があります。

Print Schema 3D 製造キーワードは、プライベートキーワード拡張で識別された要素の値の子の文字データの内容として表示される場合があります (印刷スキーマの3D 製造によって識別される元の要素をその文字データが参照している場合)。同じ印刷スキーマドキュメント内の他の場所で適切に使用されるキーワード。

## <a name="16-scoping-prefixes"></a>1.6. スコーププレフィックス


スコーププレフィックスは、キーワードの先頭に付加されるテキスト形式のラベルであり、キーワードの範囲内の影響を表します。 スコーププレフィックスを使用すると、厳密な方法で特定の明確に解釈されたコンテキストをキーワードに適用できます。 3D 製造キーワードには、"Job3D" スコーププレフィックスが必要です。 ドキュメントおよびページのスコーププレフィックスは、3D 製造印刷スキーマドキュメントでは使用できません。 詳細については、「印刷スキーマの仕様」の5.4 「スコーププレフィックス」を参照してください。

## <a name="17-resource-identifiers"></a>1.7. リソース識別子


リソース識別子は Print Schema 3D 製造キーワードで使用できますが、印刷スキーマ仕様の 5.5 "リソース識別子" の要件に従う必要があります。

## <a name="18-parameter-types"></a>1.8。 パラメーターの型


Print Schema 3D 製造キーワードセットのパラメーターは、Print Schema キーワードが設定されているパラメーターと同じ要件に従います。 印刷スキーマ仕様の「5.6」、「パラメーターの型」を参照してください。

### <a name="181-materialmapparamtype"></a>1.8.1. MaterialMapParamType

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>[12 才以下]</th>
<th>xsi:type</th>
<th>Value</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>プロパティ psf: DataType</td>
<td>xsd: QName</td>
<td>パラメーターは materialMap 型で、psk3d: MaterialMap である必要があります。</td>
</tr>
<tr class="even">
<td>プロパティ psf: MaxLength</td>
<td>xsd:integer</td>
<td><p>このパラメーターを初期化できる文字列の最大長を指定します。</p>
<p>この値は、特定のキーワードに対して必要な場合よりも大きくする必要があります。 印刷スキーマで定義されたパラメーターでは、65535文字を超える値を指定することはできません。 値は正の整数または0にする必要があります。 値は psf: MinLength の値以上である必要があります。</p></td>
</tr>
<tr class="odd">
<td>プロパティ psf: MinLength</td>
<td>xsd:integer</td>
<td><p>このパラメーターを初期化できる文字列の最小長を指定します。</p>
<p>値は正の整数または0にする必要があります。</p></td>
</tr>
<tr class="even">
<td>プロパティ psf: 必須</td>
<td>xsd: QName</td>
<td>パラメーターを初期化する必要がある場合に指定します。 このプロパティの説明と要件については、「2.1.3.1.1、"Parameter psf: 必須プロパティ」を参照してください。</td>
</tr>
<tr class="odd">
<td>プロパティ psf: Unittype.pixel 単位</td>
<td>xsd:string</td>
<td>値は MaterialMapUnitType である必要があります。</td>
</tr>
<tr class="even">
<td>プロパティ psk3d: Job3DMaterialSelected</td>
<td>xsd: QName</td>
<td>この値は、このパラメーターが対応する Job3DMaterial を表します。</td>
</tr>
</tbody>
</table>

 

## <a name="19-common-properties"></a>1.9。 共通プロパティ


この仕様では、印刷スキーマの仕様の「共通プロパティ」5.7 で定義されている印刷スキーマキーワードと同じ共通プロパティを使用します。

Xsd: decimal 型を指定するプロパティ値は、IEEE 754 単精度浮動小数点値として表現できる必要があります。

## <a name="110-parameter-unit-types"></a>1.10。 パラメーターの単位の種類


印刷スキーマ仕様の「2.1.3.1.2 "Parameter psf: Unittype.pixel 単位 Property」で指定されているパラメーターの単位の種類に加えて、この仕様では次の単位の種類が追加されています。

| Unit type   | xsi:type    | 説明                                                                                                                                                  |
|-------------|-------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 数量    | xsd:integer | パラメーターの値の内容は、カウントまたはその他の数量を表します。                                                                             |
| 気温 | xsd:decimal | パラメーターの値の内容は、温度を摂氏で表します。 このパラメーターは、常に最も近い100倍の精度に丸められる必要があります。 |
| materialMap | xsd:string  | パラメーターの値の内容は、セミコロンで区切られた materialids のリストとして表す必要があります。                                                  |

 

 

 




