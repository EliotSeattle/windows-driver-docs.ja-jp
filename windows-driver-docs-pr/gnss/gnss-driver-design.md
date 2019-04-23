---
title: GNSS ドライバーの設計
description: データ構造体、エラー報告、およびドライバーのバージョン管理を含む Windows 10 用 GNSS ドライバーの開発時に考慮する設計原則について説明します。
ms.assetid: E10B1149-CC8B-438D-B537-258F7FCFA0E7
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0b473f66d65a4bb251272f149a5b7110f57de3b6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56579601"
---
# <a name="gnss-driver-design"></a>GNSS ドライバーの設計


データ構造体、エラー報告、およびドライバーのバージョン管理を含む Windows 10 用 GNSS ドライバーの開発時に考慮する設計原則について説明します。

## <a name="data-structures"></a>データ構造体


旧バージョンとの互換性と将来の機能拡張は、すべてのデータ構造は将来の拡張機能と下位互換性の問題に対応するには、バージョン番号とサイズを開始します。 各構造体は、追加の保護対策として、新しい場合でも、同じフィールドが追加された静的構造体のサイズを保持する埋め込みバッファーもあります。 これは、誤って構造体の静的コンパイル時のサイズを使用して古い GNSS ドライバーに対して保護する (を使用して**sizeof**) 構造体の動的なサイズの代わりにします。

指定しない場合、すべてのパラメーターは、国際国際単位系 (SI) に従います。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>パラメーター</th>
<th>単位</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>距離、しきい値、またはレベル</p></td>
<td><p><strong>メーター</strong></p></td>
</tr>
<tr class="even">
<td><p>タイムアウトまたは間隔</p></td>
<td><p><strong>second</strong></p></td>
</tr>
<tr class="odd">
<td><p>速度</p></td>
<td><p><strong>メートル/秒</strong></p></td>
</tr>
</tbody>
</table>

 

## <a name="error-reporting"></a>エラー レポート


GNSS DDI が必要ですが、 **NTSTATUS**ドライバーからの戻り値として。 成功と失敗するケースだけで高レベルのオペレーティング システム (HLOS) 機能は、これらのエラー メッセージに基づいており、特定のエラー メッセージを検索しません。 推奨されますが、ドライバーが、対応する厳密にマップされているエラーを返します**NTSTATUS**エラー メッセージ。 GNSS ドライバーは、独自のカスタムを送信できる**NTSTATUS**診断に役に立つエラー メッセージ。

## <a name="driver-versioning"></a>ドライバーのバージョン管理


GNSS DDI の指定されたすべての構造体には、ドライバーのバージョン フィールドが含まれています、多くの構造体は、埋め込みフィールドを含めることができます。 これらのコンポーネントの両方が次のポリシーを使用して、GNSS DDI の新しいバージョンを軽減するために使用されます。

-   フレームワークと、ドライバーは、機能の交換プロセスを使用してそれぞれのバージョンを通信します。 これらの Ioctl はバージョン フィールドを使用して、そのバージョンを通信することで、特別なと見なされます。 そのため、デバイスとプラットフォームの機能確認を周囲の実装をする必要がありますバージョンが最初に、返され、使用量の格納を後で明示的にチェックします。 バージョンのメンバー、 [ **GNSS\_デバイス\_機能**](https://msdn.microsoft.com/library/windows/hardware/dn925104)構造体は、ドライバーのバージョン番号を通信します。 バージョンのメンバー、 [ **GNSS\_プラットフォーム\_機能**](https://msdn.microsoft.com/library/windows/hardware/dn925205)構造通信 GNSS アダプターのバージョン番号。

-   領域はバイナリの互換性を保持する構造体に追加する代わりに埋め込み取り出しは新しいフィールドを追加すると、埋め込みフィールドを構造がある場合は、されるたびに

-   GNSS DDI のバージョンと見なされます新しいフィールドを追加するたびにインクリメントします。 これは、コメント、GNSS DDI ヘッダー内に反映されますが定数として公開されています。 GNSS アダプターと GNSS ドライバーの両方を現在のバージョンを示すためにでプライベートの定数値が使用されます。 これにより、GNSS アダプターとドライバーが特定のバージョンに対してコード化できます。

-   GNSS アダプター GNSS ドライバーの以前のバージョンとの下位互換性があります。 DDI の新しいバージョンのプロトコルの変更が導入された、GNSS アダプターが新しい GNSS DDI 準拠ではのドライバーの新しいバージョンにのみ新しいプロトコルを実装し、ドライバーの以前のバージョンの古いプロトコルを使用する必要があります。

-   GNSS ドライバーでは、GNSS アダプターの新しいバージョンとの上位互換性がある必要があり、コードが対象の現在のバージョンと同じ方法で GNSS アダプターの新しいバージョンを扱う必要があります。

-   GNSS アダプターの以前のバージョンは、GNSS ドライバーの新しいバージョンで正常に機能する必要はありません。 GNSS アダプターおよび DDI の新しいバージョンに対する GNSS ドライバーの共同開発を容易に厳密なバージョンのチェックは存在しない新しい GNSS ドライバーをブロックする GNSS アダプターで。 ただし、DDI の新しいバージョンに対して実装される GNSS ドライバーは GNSS DDI の以前のバージョンに対して実装される GNSS アダプターが含まれている製品版のデバイスに出荷されません。

-   任意の Windows 8.1 または古い GNSS センサー ドライバーは GNSS アダプターによってサポートされません。 これらのドライバーは、従来のスタックを Windows 10 で機能になってしまいます。 別の Windows 10 GNSS ドライバーの存在でレガシ GNSS センサー ドライバーの使用量は定義されません。

 

 



