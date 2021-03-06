---
title: MB DNS の更新
description: MB DNS の更新
ms.assetid: be93f0b4-a075-455e-b03c-6d23a2be7b1d
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c578e0d4678d7608da10add204ab1c4b8558c67c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378002"
---
# <a name="mb-dns-updates"></a>MB DNS の更新


このトピックでは、DNS アドレスの更新プログラムに関する MB サービスに通知するための操作について説明します。

ミニポート ドライバーを設定する必要があります、**ネーム サーバー** DNS アドレスの変更について、Windows を更新するレジストリ キー。 次の表では、適切なレジストリ キー、期待値および IPv4 と IPv6 のネットワークの文字列の例について説明します。 ミニポート ドライバーでは、IPv4 ネットワークをのみをサポートする場合は、IPv4 のレジストリ キーのみを設定があります。 Windows メディアについては、送信することによってイベントを接続の通知を送信する前に、ミニポート ドライバーは、適切なレジストリ キーを設定する必要があります[ **NDIS\_状態\_リンク\_状態**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-link-state)通知します。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">IPv4 と IPv6</th>
<th align="left">レジストリ キー</th>
<th align="left">値</th>
<th align="left">例</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>IPv4</p></td>
<td align="left"><p>HKLM\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters\Interfaces\InterfaceGUID\NameServer</p></td>
<td align="left"><p>DNS サーバーの IPv4 アドレスのスペースで区切られます</p></td>
<td align="left"><p>10.20.30.41</p>
<p>10.20.30.40</p></td>
</tr>
<tr class="even">
<td align="left"><p>IPv6</p></td>
<td align="left"><p>HKLM\SYSTEM\CurrentControlSet\Services\Tcpip6\Parameters\Interfaces\InterfaceGUID\NameServer</p></td>
<td align="left"><p>DNS サーバー IPv6 アドレスのスペースで区切られます</p></td>
<td align="left"><p>2001:4898:7001:f000:1:2:3:4</p>
<p>2001:4898:7001:f000:1:2:3:5</p></td>
</tr>
</tbody>
</table>

 

ミニポート ドライバーを指定する場合にのみ、これらの操作を使用する必要があります**EnableDhcp**の INF ファイルでゼロにします。 つまり、ミニポート ドライバーでは、DHCP が実装されていません。

IP アドレスの通知の処理に関する詳細については、次を参照してください。 [MB ミニポート ドライバー IP アドレスの通知のガイドライン](guidelines-for-mb-miniport-driver-ip-address-notifications.md)します。

 

 





