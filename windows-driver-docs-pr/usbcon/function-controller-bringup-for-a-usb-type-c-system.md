---
Description: 関数コント ローラーのドライバーは、その型から C の USB コネクタがサポートし、課金を開始し、デバイスに描画できる現在の最大量ときにバッテリ サブシステムに通知充電中レベルの詳細について、オペレーティング システムを通知します。
title: USB Type-C Windows システムにおけるファンクション コントローラーの起動
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5965d5bbd91cc2d9d73fd9afe11f69c742670273
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378356"
---
# <a name="bring-up-the-function-controller-on-a-usb-type-c-windows-system"></a>USB Type-C Windows システムにおけるファンクション コントローラーの起動


**要約**

-   OEM は、USB 型-c コネクタがある関数のコント ローラーのタスクを表示します。

**適用対象**

-   Windows 10 Mobile

**最終更新日**

-   2015 年 11 月

**重要な API**

-   [USB 関数コント ローラー クライアント ドライバーのプログラミング リファレンス](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/mt188010(v=vs.85))
-   [独自の充電器をサポートするための USB フィルター ドライバー](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/mt188012(v=vs.85))

関数コント ローラーのドライバーは、その型から C の USB コネクタがサポートし、課金を開始し、デバイスに描画できる現在の最大量ときにバッテリ サブシステムに通知充電中レベルの詳細について、オペレーティング システムを通知します。

ここでは、特定の時点で、関数のコント ローラーが 1 つのコネクタ (UFP) を管理します。

## <a name="1-load-the-usb-device-side-drivers"></a>1. デバイス側の USB ドライバーを読み込む


関数のコント ローラーの操作を管理する 2 つのドライバーがあります。 ペアは、Microsoft 提供の USB 関数クラスの拡張機能とそのクライアント ドライバーがします。 クラスの拡張機能は、クライアント ドライバーによって、オペレーティング システムに送信される情報を報告します。 クライアント ドライバーでは、ハードウェアのインターフェイスを使用して、ハードウェアと通信します。 参照してください、 [Windows での USB デバイス側ドライバー](usb-device-side-drivers-in-windows.md)します。

![usb 関数コント ローラーのドライバー](images/function-controller.png)

-   場合は、システムでは、ChipIdea および Synopsys コント ローラーを使用します。
    1.  ChipIdea および Synopsys コント ローラーの組み込みのクライアント ドライバーを提供する Microsoft を読み込みます。
    2.  下位のフィルター ドライバーを取得しますアタッチ/デタッチ充電が接続されているときにイベントを記述します。 ドライバーは、充電器と構成プロパティの種類を決定します。 USB BC1.2 仕様で定義されたポートを充電中も検出できます。 課金調停ドライバー (CAD.sys) ことを報告できるように、クラスの拡張機能に情報を充電渡されます。 詳細については、次を参照してください。[独自の充電器をサポートするための USB フィルター ドライバー](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/mt188012(v=vs.85))します。
-   システムは、カスタムのコント ローラーを使用している場合は、クライアント ドライバーを記述します。 BC1.2 は検出ロジックは、クライアント ドライバーで実装されます。 詳しくは、次のトピックをご覧ください。

    [USB 関数コント ローラー クライアント ドライバーのプログラミング リファレンス](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/mt188010(v=vs.85))

    [関数の USB コント ローラーの Windows ドライバーの開発](developing-windows-drivers-for-usb-function-controllers.md)

## <a name="2-modify-system-acpi-to-indicate-to-the-function-controller-driver-that-the-connector-is-a-usb-type-c-connector"></a>2. コネクタは、USB 型-C# のコネクタを関数のコント ローラー ドライバーに示すために、ACPI システムを変更します。


これは、ACPI 6.0 仕様で定義されている ACPI メソッドを通じて行われます

`_UPC (USB Port Capabilities)`

ACPI 6.0 で定義されている新しい値を使用して、適切な種類の"種類 C USB2"と「型 C USB2 とスイッチを使用して SS」などの C-USB 型コネクタを示します。 関数のドライバーは、適切な充電ソースを決定する USB 種類 C 固有調停ロジックを使用するよう CAD.sys、するには、この情報を通信します。

```cpp
Device (UFN0)
{
    ...

    Name (_UPC, Package()
    {
        0x1,    // Connectable
        0x9,    // Type-C USB2 and Type-C USB2 and SS with switch
        0x0,    // Reserved
        0x0     // Reserved
    })

    Name (_CRS, ResourceTemplate()
    {
        ...
    })

    ...
```

## <a name="related-topics"></a>関連トピック
[USB Type-C コネクタ用 Windows ドライバーの開発](developing-windows-drivers-for-usb-type-c-connectors.md)  



