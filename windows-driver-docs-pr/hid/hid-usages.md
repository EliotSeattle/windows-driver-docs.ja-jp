---
title: HID の使用状況
description: HID usage は、HID コントロールの使用目的、およびコントロールが実際にどのように測定するかを特定します。
ms.assetid: 84fed314-3554-4291-b51c-734d874a4bab
keywords:
- ヒューマンインターフェイスデバイス WDK、使用法
- HID WDK、usage
- 対話型の入力デバイス WDK、使用法
- 入力デバイス WDK、使用法
- ヒューマンインターフェイスデバイス WDK、コントロール
- HID WDK、コントロール
- 対話型の入力デバイス WDK、コントロール
- 入力デバイス WDK、コントロール
- WDK HID を制御します
- 使用量ページ WDK HID
- 使用状況 Id WDK HID
- 拡張使用量 WDK HID
- 使用範囲 WDK HID
- 別名使用法 WDK HID
- 使用状況 WDK HID
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b120368916b603000602e0a1074ab1fbf124011e
ms.sourcegitcommit: f8c3585ec7b1bdfcd65f7f2cc9aa688655de4d20
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/15/2020
ms.locfileid: "81396306"
---
#  <a name="hid-usages"></a>HID の使用状況


*Hid usage*は、hid コントロールの使用目的、およびコントロールが実際にどのように測定するかを特定します。




WDK の HID ドキュメント全体で、次の概念と用語が使用されています。

[[使用状況] ページ](#usage-page)

[使用状況 ID](#usage-id)

[拡張使用量](#extended-usage)

[使用範囲](#usage-range)

[エイリアス使用](#aliased-usages)

Windows コンポーネントがアクセスする特定の使用例については、「[システムで使用するために windows によって開かれたトップレベルのコレクション](top-level-collections-opened-by-windows-for-system-use.md)」を参照してください。

HIDClass デバイスでサポートされている使用状況を確認する方法の詳細については、以下を参照してください。

[コレクション機能](collection-capability.md)

[ボタン機能配列](button-capability-arrays.md)

[値機能配列](value-capability-arrays.md)

[HID レポートの解釈](interpreting-hid-reports.md)

業界標準の HID 使用法の詳細については、 [Usb 実装フォーラム](https://www.usb.org/hid)の web サイトにある Universal Serial BUS (usb) 仕様の**hid 使用表**を参照してください。

### <a name="usage-page"></a>[使用状況] ページ

HID の使用は、関連するコントロールの*使用状況ページ*にまとめられています。 特定のコントロールの使用方法は、使用状況ページ、[使用 ID](#usage-id)、名前、および説明で定義されています。 使用状況ページの値は16ビットの符号なしの値です。

使用状況ページの例を次に示します。

| ページ ID | ページ名                | *hidusage. h*定数  |
|:-------:|--------------------------|------------------------|
| 0x01    | 汎用デスクトップコントロール | HID_USAGE_PAGE_GENERIC |
| 0x05    | ゲームコントロール            | HID_USAGE_PAGE_GAME    |
| 0x08    | Led                     | HID_USAGE_PAGE_LED     |
| 0x09    | ボタン                   | HID_USAGE_PAGE_BUTTON  |

### <a name="usage-id"></a>使用状況 ID

使用状況ページのコンテキストでは、有効な使用 id (使用状況*id*) が使用状況ページで使用されていることを示します。 使用状況 ID 0 は予約されています。 使用 ID 値は16ビットの符号なしの値です。

**汎用デスクトップコントロール**の [使用状況] ページに表示されるコントロールの例を次に示します。

| 使用状況 ID | 使用法の名前            | *hidusage. h*定数                    |
|:--------:|-----------------------|------------------------------------------|
| 0x01     | ポインター               | HID_USAGE_GENERIC_POINTER                |
| 0x02     | マウス                 | HID_USAGE_GENERIC_MOUSE                  |
| 0x04     | ジョイ              | HID_USAGE_GENERIC_JOYSTICK               |
| 0x05     | ゲームパッド              | HID_USAGE_GENERIC_GAMEPAD                |
| 0x06     | キーボード              | HID_USAGE_GENERIC_KEYBOARD               |
| 0x07     | キーパッド                | HID_USAGE_GENERIC_KEYPAD                 |
| 0x08     | 複数の軸を持つコントローラー | HID_USAGE_GENERIC_MULTI_AXIS_CONTROLLER  |

### <a name="extended-usage"></a>拡張使用量

*拡張使用*とは、最大の2バイトの16ビット[使用量ページ](#usage-page)値を指定する32ビット値で、拡張使用率の最小値の2バイトを16ビット[使用 ID](#usage-id)で指定します。

### <a name="usage-range"></a>使用範囲

*使用範囲*は、連続した一連の[使用量 id](#usage-id)であり、すべて同じ [[使用状況] ページ](#usage-page)にあります。 使用範囲は、レポート記述子の使用量の最小値と使用量の最大値によって指定されます。

### <a name="aliased-usages"></a>エイリアス使用

[**リンクコレクション**](link-collections.md)または HID コントロールに複数の使用方法を指定できます。 特定のコレクションまたはコントロールについては、このような使用のグループは相互の別名であり、*別名使用*と呼ばれます。 区切り記号項目は、エイリアス化された使用法を指定するために使用されます。 [使用範囲](#usage-range)を別名にすることはできません。

最上位レベルのコレクションの機能配列にエイリアス使用法を指定する方法については、「[ボタン機能配列](button-capability-arrays.md)と[値機能](value-capability-arrays.md)配列」を参照してください。

 

 




