---
title: WDM ドライバーの種類
description: WDM ドライバー バス ドライバー、機能のドライバー、およびフィルター ドライバーの 3 種類があります。
ms.assetid: 86acc77e-816e-46c8-b63c-2bb10920acd6
keywords:
- WDM ドライバー WDK カーネルの種類
- WDM ドライバー WDK カーネル、複数層のドライバー
- 階層型ドライバー WDK カーネル
- ドライバーは、WDK WDM をレイヤーします。
- バス ドライバー WDK WDM
- 機能ドライバー WDK WDM
- フィルター ドライバー WDK WDM
- WDM バス ドライバー WDK
- WDM 関数ドライバー WDK
- WDM フィルター ドライバー WDK
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: b81d7cf1f0f7d31e9674d39a47a23439d20f8f7c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56539236"
---
# <a name="types-of-wdm-drivers"></a>WDM ドライバーの種類


WDM ドライバーの 3 つの種類があります。 バス ドライバー、ドライバーの関数、およびフィルター ドライバー。




-   A[バス ドライバー](bus-drivers.md)ドライブの個々 の I/O バス デバイスとデバイスに依存しないスロットごとの機能を提供します。 バス ドライバーは、検出し、バスに接続されている子デバイスを報告します。
-   A[関数ドライバー](function-drivers.md)ドライブの個々 のデバイス。
-   A[フィルター ドライバー](filter-drivers.md)デバイスや、デバイスのクラス、バスの I/O 要求をフィルター処理します。

このコンテキストで、 *bus*は任意のデバイスを他の物理、論理、または仮想デバイスが接続されている; バスには、SCSI、PCI、並列と同様のポートのシリアル ポート、および i8042 ポートなどの従来のバスが含まれています。

WDM ドライバーのさまざまな種類を理解し、書き込んでいるドライバーの種類を把握するドライバー開発者向けに重要です。 たとえば、かどうか、ドライバーは、処理の各[プラグ アンド プレイ](implementing-plug-and-play.md)IRP とそのような Irp の処理方法 (バス ドライバー、機能のドライバーまたはフィルター ドライバー)、ドライバーの種類が書き込まれているに依存します。

### <a href="" id="possible-driver-layers"></a>

次の図は、バス ドライバー、機能のドライバー、およびデバイスのフィルター ドライバー間の関係を示します。

![可能なドライバーのレイヤーを示す図](images/drvlyr.png)

通常、各デバイスには、親の I/O バス、デバイスの機能のドライバーとデバイスの 0 個以上のフィルター ドライバー、バス ドライバーがあります。 多くのフィルター ドライバーが必要なドライバーの設計では、最適なパフォーマンスは生成しません。

前の図に、ドライバー、次に示します。

1.  A*バス ドライバー*サービス バス コント ローラー、アダプター、またはブリッジです。 バス ドライバーが必要なドライバーです。コンピューター上のバスの種類ごとに 1 つのバス ドライバーがあります。 Microsoft では、最も一般的なバスのバス ドライバーを提供します。 Ihv と Oem は、その他のバス ドライバーを提供できます。

2.  A *bus フィルター ドライバー*通常、バスに値を追加し、Microsoft またはシステムの OEM によって提供されます。 任意の数、バスの bus フィルター ドライバーのことができます。

3.  *下位レベルのフィルター ドライバー*通常デバイス ハードウェアの動作を変更します。 省略可能、Ihv によって通常提供されます。 任意の数のデバイスの下位レベルのフィルター ドライバーがあります。

4.  A*関数ドライバー*デバイスの主なドライバーです。 関数のドライバーがデバイスのベンダーによって通常書き込まれが必要です (デバイスで使用されている場合を除き、 *raw モード*)。

5.  *上位レベルのフィルター ドライバー*通常デバイスの付加価値機能を提供します。 省略可能なされ、通常は Ihv によって提供されます。

次のトピックでは、WDM ドライバーの 3 つの一般的な種類-関数ドライバー、バス ドライバーのフィルター ドライバー-の詳細。 サンプルの USB ドライバーを使用している WDM ドライバー レイヤーの例に示しますも含まれています。

## <a name="in-this-section"></a>このセクションの内容


-   [バス ドライバー](bus-drivers.md)
-   [関数のドライバー](function-drivers.md)
-   [フィルター ドライバー](filter-drivers.md)
-   [WDM ドライバー レイヤー:例](wdm-driver-layers---an-example.md)

 

 



