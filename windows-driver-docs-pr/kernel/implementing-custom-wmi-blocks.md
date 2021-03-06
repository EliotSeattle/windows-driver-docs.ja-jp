---
title: カスタム WMI ブロックの実装
description: カスタム WMI ブロックの実装
ms.assetid: c596924f-9f82-4ca7-b0f0-afc596d7bf99
keywords:
- WMI WDK カーネル、イベントブロック
- イベントブロック WDK WMI
- データブロック WDK WMI
- WMI WDK カーネル、データブロック
- WDK WMI をブロックする
- カスタムブロック WDK WMI
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: b897e9c695490eb93790a2ac00ff09154059960b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838637"
---
# <a name="implementing-custom-wmi-blocks"></a>カスタム WMI ブロックの実装





ドライバーは、デバイス固有のインストルメンテーションを公開する*カスタムブロック*を実装できます。 たとえば、温度を報告できるディスクドライブのドライバーは、ドライブの温度が安全なしきい値を超えたときに WMI クライアントに通知するカスタムイベントブロックを実装する場合があります。

カスタムブロックを実装するには、ドライバーを次のようにします。

-   は、MOF ファイルでクラスを定義し、MOF ファイルをリソースにコンパイルします。また、「 [WMI スキーマの発行](publishing-a-wmi-schema.md)」で説明されているように、ドライバーにリソースを含めます。

-   「 [Wmi Data Provider として登録する](registering-as-a-wmi-data-provider.md)」で説明されているように、ドライバーによってサポートされる他の標準ブロックとカスタムブロックと共に、ブロックを wmi に登録します。

-   Wmi[要求の処理](handling-wmi-requests.md)に関するページで説明されているように、**データパス**にあるドライバーのデバイスオブジェクトポインターを指定するすべての wmi 要求を**処理します**。

ドライバーは、バイナリ MOF ファイルが読み込まれる順序を制御できません。 唯一の保証は、ドライバー固有の MOF ファイルの前に wmicore が読み込まれることです。 したがって、カスタム WMI クラスは、同じ MOF ファイル内のいずれかのクラス、または wmicore 内のいずれかのクラスからのみ継承する必要があります。

カスタム WMI データブロックのパフォーマンスと使いやすさを向上させるには、次のガイドラインを考慮してください。

-   同じデータブロック内にグループ化されたデータ項目を格納します。

    たとえば、i8042 ポートコントローラーは、キーボードとマウスの両方のポートに関する状態情報を保持する場合があります。 ドライバーでは、マウスとキーボードのすべての情報を含む1つの大きなデータブロックではなく、マウスポート用のデータブロックと、キーボードポート用の別のデータブロックを定義できます。

-   頻繁に使用されるデータ項目を個別のデータブロックに配置します。特に、あまり使用されない項目と共にグループ化する場合に使用します。

    たとえば、ドライバーが1つの項目を持つデータブロックの CPU 使用率を公開する場合、WMI クライアントは、ブロック内の追加データ項目を取得するオーバーヘッドを発生させることなく、CPU 使用率を追跡できます。 WMI クライアントは単一のデータ項目を照会できないため、1つの項目を取得するには、データブロックのインスタンス全体に対してクエリを実行する必要があります。

-   イベントブロックを使用して、エラーログの代わりにではなく、例外的なイベントを WMI クライアントに通知します。

    一度にキューに登録できるイベントの数は限られています。キューがいっぱいになると、イベントは失われます。 また、WMI クライアントにイベントを配信するタイミングを保証することはできません。

-   イベントブロックを最大サイズの1K バイトに制限します。

    イベント項目は、生成されたイベントを含む[**Wnode\_イベント\_項目**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_event_item)構造全体に対して、レジストリ定義のサイズ制限 (最初は 1k) があるため、小さいデータ型として定義する必要があります。 大量の通知の場合、ドライバーは、データブロックの単一のインスタンスを指定する[**Wnode\_イベント\_参照**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_event_reference)構造を送信できます。この場合、WMI はクエリを実行して実際のイベントを取得します。 ただし、これにより、イベントの発生と通知の間のタイムラグが増加します。

-   固定サイズのデータ項目をデータブロックの先頭に配置し、その後に任意の可変サイズのデータ項目を配置します。

    たとえば、3つの DWORD データ項目と1つの可変長文字列を含むデータブロックでは、最初に3つの Dword を入力し、次にその文字列を指定します。 固定サイズのデータ項目をブロックの先頭に配置すると、WMI クライアントはそれらを簡単に抽出できます。

-   ドライバーのデータブロックにアクセスするシステムユーザーの種類を検討します。 システムは、すべての WMI クラス Guid の既定のセキュリティ記述子を提供します。 必要に応じて、デバイスの INF ファイル内で別のセキュリティ記述子を指定できます。 詳細については、「[安全なデバイスのインストールの作成](https://docs.microsoft.com/windows-hardware/drivers/install/creating-secure-device-installations)」を参照してください。

WMI ではバージョン管理がサポートされていないため、ドライバーライターは新しい MOF クラスを定義し、新しい GUID を生成して既存のカスタムブロックを修正する必要があります。

 

 




