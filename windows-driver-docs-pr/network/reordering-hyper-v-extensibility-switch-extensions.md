---
title: Hyper-V 拡張可能スイッチ拡張機能の並べ替え
description: Hyper-V 拡張可能スイッチ拡張機能の並べ替え
ms.assetid: DAB7FAE0-1632-4FD1-8697-48553A51BD20
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e315791f501d11e65a513e808b70a0e3ace6c4ce
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373292"
---
# <a name="reordering-hyper-v-extensible-switch-extensions"></a>Hyper-V 拡張可能スイッチ拡張機能の並べ替え


拡張可能スイッチの各インスタンスでは、複数の HYPER-V 拡張可能スイッチのキャプチャまたはフィルター拡張機能を有効にできます。

**注**  拡張可能スイッチの各インスタンスで 1 つだけの転送拡張機能を有効にすることができます。

 

既定値、複数のキャプチャまたはフィルター拡張機能では順序付けベースの種類を使用してインストールされています。 たとえば、スイッチのプロトコルのエッジに最も近い、最近インストールされた拡張機能で拡張可能スイッチ ドライバー スタックで複数のキャプチャ拡張機能が重ねられています。

複数のキャプチャまたはフィルター拡張機能がインストールされている場合は、拡張可能スイッチ ドライバー スタックのドライバーの順序を変更する PowerShell コマンドレットを使用できます。 次の例では、これを行う PowerShell ウィンドウから入力したコマンドを示します。

``` syntax
# Show the current order. The ExtensionOrder field contains paths to WMI extension instances.
# The [wmi] operator can be used to convert the paths to full WMI objects. 
PS C:\Windows\system32> $privateNetwork = Get-VMSwitch PrivateNetwork
PS C:\Windows\system32> $extensionOrder = $privateNetwork.ExtensionOrder
PS C:\Windows\system32> $extensionOrder | ForEach-Object { Write-Host "Name:" ([wmi]$_).ElementName }
Name: NDIS Capture LightWeight Filter
Name: Switch Extensibility Test Extension 2
Name: Switch Extensibility Test Extension 1
Name: WFP extensible switch Layers LightWeight Filter

# Place “Test Extension 1” above “Test Extension 2” in the ordered list of extensions.
PS C:\Windows\system32> $tmp = $extensionOrder[1]
PS C:\Windows\system32> $extensionOrder[1] = $extensionOrder[2]
PS C:\Windows\system32> $extensionOrder[2] = $tmp

# Commit the updated order.
PS C:\Windows\system32> $privateNetwork.ExtensionOrder = $extensionOrder

# Retrieve the switch information again to validate the order.
PS C:\Windows\system32> $privateNetwork = Get-VMSwitch PrivateNetwork
PS C:\Windows\system32> $privateNetwork.ExtensionOrder | ForEach-Object { Write-Host "Name:" ([wmi]$_).ElementName }
Name: NDIS Capture LightWeight Filter
Name: Switch Extensibility Test Extension 1
```

## <a name="related-topics"></a>関連トピック


[Get-vmswitch](https://docs.microsoft.com/powershell/module/hyper-v/get-vmswitch)

[**Msvm\_EthernetSwitchExtension**](https://docs.microsoft.com/windows/desktop/HyperV_v2/msvm-ethernetswitchextension)

[**Msvm\_VirtualEthernetSwitchSettingData**](https://docs.microsoft.com/windows/desktop/HyperV_v2/msvm-virtualethernetswitchsettingdata)

 

 






