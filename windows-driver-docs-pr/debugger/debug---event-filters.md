---
title: デバッグ イベント フィルター
description: デバッグ イベント フィルター
ms.assetid: ffa1241a-8a75-44ac-94b7-608393cf4138
keywords:
- デバッグ イベント フィルター
- 例外、イベント フィルターのデバッグ
- イベント、イベント フィルターのデバッグ
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: cc5a4284a241b2756acdef04bcbe55a133473bd0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63374362"
---
# <a name="debug--event-filters"></a>Debug | Event Filters (デバッグ | イベント フィルター)


## <span id="ddk_debug_event_filters_dbg"></span><span id="DDK_DEBUG_EVENT_FILTERS_DBG"></span>


をクリックして**イベント フィルター**上、**デバッグ**を開く メニュー、**イベント フィルター**  ダイアログ ボックス。 このダイアログ ボックスでは、中断状態と例外とイベントの処理状態を構成できます。

### <a name="span-iddialogboxspanspan-iddialogboxspandialog-box"></a><span id="dialog_box"></span><span id="DIALOG_BOX"></span>ダイアログ ボックス

**イベント フィルター**  ダイアログ ボックスに、デバッガーが認識するすべてのイベントが一覧表示します。 番号付きの例外は、表示し、一覧に追加できます。

イベントの中断状態を変更するイベントを選択しのいずれかをクリックし、**実行**オプション ボタン (**有効**、**無効**、**出力**、または**無視**)。

イベントの処理状態を変更するイベントを選択しのいずれかをクリックし、**続行**オプション ボタン (**Handled**または**処理されない**)。

新しい番号付きの例外を追加するには、クリックして**追加**します。 ときに、**例外フィルター**  ダイアログ ボックスが表示されたら、例外コードを入力して、中断状態と処理のステータスの適切なボタンをクリックします をクリックし、 **OK**します。

番号付きの例外を削除するには、例外を選択してクリックして**削除**します。 標準的なイベントを削除することはできません。

状態を設定すると、**モジュールの読み込み**または**モジュールのアンロード**イベント、特定のモジュールには、この状態を制限することができます。 をクリックして**引数**、モジュールの名前または内のモジュールのベース アドレスを入力、**フィルター引数**クリックしてダイアログ ボックスで、 **OK**。 使用することができます[ワイルドカード](string-wildcard-syntax.md)ベース アドレスを指定するとします。 モジュールを指定しないと、任意のモジュールがロードまたはアンロードされるときに中断が発生します。

状態を設定すると、**デバッグ出力**イベント、特定の出力のパターンには、この状態を制限することができます。 をクリックして**引数**、出力のパターンを入力、**フィルター引数**クリックしてダイアログ ボックスで、 **[ok]** します。 出力、パターンを指定しないと、出力を中断が発生します。

イベントを選択し、をクリックし、イベントがデバッガーを中断する場合に実行される自動コマンドを設定する場合は、**コマンド**します。 **Filter コマンド** ダイアログ ボックスが表示されます。 使用する任意のコマンドを入力して、**コマンド**または**セカンド チャンス コマンド**ボックス。 セミコロンを使用して複数のコマンドを分離し、これらのコマンドを引用符で囲まないでください。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

中断状態と状態、イベントのすべてのコード、すべてのイベント、およびこの状態を制御するための他のメソッドの既定の状態の処理の詳細については、次を参照してください。[を制御する例外とイベント](controlling-exceptions-and-events.md)します。

 

 





