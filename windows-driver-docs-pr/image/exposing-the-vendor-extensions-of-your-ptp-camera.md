---
title: PTP カメラのベンダー拡張の公開
description: PTP カメラのベンダー拡張の公開
ms.assetid: b3a8b70b-c7ac-4e45-97bb-9b58e013100d
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3e8c38cb4457a99f093d5c0a2f973b8872459cc8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56582363"
---
# <a name="exposing-the-vendor-extensions-of-your-ptp-camera"></a>PTP カメラのベンダー拡張の公開





PTP デバイスには、ベンダー拡張プロパティ、ベンダー拡張のイベントおよびコマンドのベンダー拡張をサポートできます。

ベンダー拡張プロパティとイベントを次に、 **DeviceData** INF ファイルのエントリ (を参照してください[WIA デバイスの INF ファイル](inf-files-for-wia-devices.md)詳細については) ので、ドライバーは処理できません。 ベンダー拡張機能の ID を一覧表示するエントリが必要です。 これは、DeviceInfo データセットで VendorExtensionID フィールドと一致する必要があります。 その他のエントリの例が次のとおりし、次のセクションで説明します。

```INF
[DeviceData]
VendorExtID=0x12345678
PropCode="0xD001,0xD002,0xD003"
PropCodeD001="0x00009802,VendorProperty1"
PropCodeD002="0x00009803,VendorProperty2"
PropCodeD003="0x00009804,VendorProperty3"
EventCode="0xC001,0xC002"
EventCodeC001={191D9AE7-EE8C-443c-B3E8-A3F87E0CF3CC}
EventCodeC002={8162F5ED-62B7-42c5-9C2B-B1625AC0DB93}
```

 

 




