---
title: PnPUtil の例
description: PnPUtil の例
ms.assetid: 4805edb9-e4f8-441d-a7f4-0c962ddeae4e
ms.date: 01/31/2018
ms.localizationpriority: medium
ms.openlocfilehash: 45111ef2ad2bc4c39e9f41285a603dda5fcb3523
ms.sourcegitcommit: 4058fcb136cfb8255ca7bec68e8597c89f7b68cd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/21/2020
ms.locfileid: "80080153"
---
# <a name="pnputil-examples"></a>PnPUtil の例

このトピックでは、PnPUtil ツールを使用する方法の例を示します。

```
  pnputil /add-driver x:\driver.inf                                  <- Add driver package
  pnputil /add-driver c:\oem\*.inf                                   <- Add multiple driver packages
  pnputil /add-driver device.inf /install                            <- Add and install driver package
  pnputil /enum-drivers                                              <- Enumerate OEM driver packages
  pnputil /delete-driver oem0.inf                                    <- Delete driver package
  pnputil /delete-driver oem1.inf /force                             <- Force delete driver package
  pnputil /export-driver oem6.inf .                                  <- Export driver package
  pnputil /export-driver * c:\backup                                 <- Export all driver packages
  pnputil /disable-device "USB\VID_045E&PID_00DB\6&870CE29&0&1"      <- Disables device specified by device instance ID
  pnputil /enable-device "USB\VID_045E&PID_00DB\6&870CE29&0&1"       <- Enables device specified by device instance ID
  pnputil /restart-device "USB\VID_045E&PID_00DB\6&870CE29&0&1"      <- Restarts device specified by device instance ID
  pnputil /remove-device "USB\VID_045E&PID_00DB\6&870CE29&0&1"       <- Removes device specified by device instance ID
  pnputil /scan-devices                                              <- Scan the system for any device hardware changes
  pnputil /enum-devices /connected                                   <- Enumerate only connected devices on the system
  pnputil /enum-devices /instanceid "ACPI\PNP0A08\1"                 <- Enumerate device with specific instance ID
  pnputil /enum-devices /class Display                               <- Enumerate all devices with specific class
  pnputil /enum-devices /problem 28                                  <- Enumerate all devices with specific problem code
  pnputil /enum-devices /problem /ids                                <- Enumerate all devices with problems and display hardware/compatible IDs
  pnputil /enum-interfaces /enabled                                  <- Enumerate only enabled interfaces on the system
```

 

 





