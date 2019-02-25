---
title: HYPER-V 拡張可能スイッチの拡張機能を列挙します。
description: HYPER-V 拡張可能スイッチの拡張機能を列挙します。
ms.assetid: AC468A8F-5C48-419B-9E9E-D63925E1CE9D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 06c2019cdc8ce75135a6fa279d48573bc0132432
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559453"
---
# <a name="enumerating-hyper-v-extensible-switch-extensions"></a>HYPER-V 拡張可能スイッチの拡張機能を列挙します。


[Get-vmswitchextension](https://technet.microsoft.com/library/hh848603.aspx) PowerShell コマンドレットは、拡張可能スイッチのインスタンスにバインドされている HYPER-V 拡張可能スイッチ拡張機能を列挙します。 このコマンドレットは、拡張可能スイッチのインスタンスで、拡張機能が有効になっているかどうかも報告されます。

[Get-vmswitchextension](https://technet.microsoft.com/library/hh848603.aspx)コマンドレットは、次の構文を使用します。

``` syntax
Get-VMSwitchExtension [[-VMSwitchName] <string[]>] [[-Name] <string[]>] [-ComputerName <string[]>]
    [<CommonParameters>]

Get-VMSwitchExtension [[-VMSwitch] <VMSwitch[]>] [-ComputerName <string[]>] [<CommonParameters>]
```

次の例からの出力を示しています、 [Get-vmswitchextension](https://technet.microsoft.com/library/hh848603.aspx)コマンドレット。

``` syntax
PS C:\Windows\system32> Get-VMSwitchExtension PrivateNetwork | fl -property @("Name","ExtensionType", "SwitchName","Enabled")

Name          : NDIS Capture LightWeight Filter
ExtensionType : Capture
SwitchName    : PrivateNetwork
Enabled       : False

Name          : Switch Extensibility Test Extension 2
ExtensionType : Filter
SwitchName    : PrivateNetwork
Enabled       : False

Name          : Switch Extensibility Test Extension 1
ExtensionType : Filter
SwitchName    : PrivateNetwork
Enabled       : False

Name          : WFP extensible switch Layers LightWeight Filter
ExtensionType : Filter
SwitchName    : PrivateNetwork
Enabled       : True
```

**注**  例では、情報の量を最小限に抑えるためにフィルター コマンド"fl"から返される拡張オブジェクトをパイプ処理します。 これが原因で表示される情報のサブセットでありの属性と一致する、 **-プロパティ**スイッチします。

 

## <a name="related-topics"></a>関連トピック


[Get-vmswitchextension](https://technet.microsoft.com/library/hh848603.aspx)

[**Msvm\_EthernetSwitchExtension**](https://msdn.microsoft.com/library/hh850139)

 

 





