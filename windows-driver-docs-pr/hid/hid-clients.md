---
title: HID クライアントの概要
description: HID クライアントは、HID API を使用して通信するドライバー、サービス、またはアプリケーションで、多くの場合、特定の種類のデバイス (センサー、キーボード、マウスなど) を表します。
ms.assetid: C97E1F63-0CA5-42F3-A139-48E830F2E2B7
keywords:
- HID クライアント
- ドライバー
- サービス
- HID API
- HID コレクション
ms.date: 02/26/2020
ms.localizationpriority: medium
ms.openlocfilehash: ee60fb5d460caadc98ed45c0e1559c0c7c37230a
ms.sourcegitcommit: f1f641bd759b7bf6e45626ffcc090ffd28337c30
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/28/2020
ms.locfileid: "78166680"
---
# <a name="hid-clients-overview"></a>HID クライアントの概要

ヒューマンインターフェイスデバイス (HID) は、HID API を使用して通信するドライバー、サービス、アプリケーションであり、多くの場合、センサー、キーボード、マウスなどの特定の種類のデバイスを表します。 デバイスは、ハードウェア ID または特定の HID コレクションによって識別され、HID API を介して通信します。

| トピック | 説明 |
| --- | --- |
| [HID の使用](https://docs.microsoft.com/windows-hardware/drivers/hid/hid-usages) | _Hid usage_は、hid コントロールの使用目的、およびコントロールが実際にどのように測定するかを特定します。 |
| [HID コレクション](https://docs.microsoft.com/windows-hardware/drivers/hid/hid-collections) | Hid_コレクション_は、hid コントロールとそれぞれの[hid 使用法](https://docs.microsoft.com/windows-hardware/drivers/hid/hid-usages)を意味的にグループ化したものです。 |
| [HID コレクションを開く](https://docs.microsoft.com/windows-hardware/drivers/hid/opening-hid-collections) | このセクションでは、hid クライアントが HID クラスドライバー (HIDClass) と通信して、デバイスの HID コレクションを操作する方法について説明します。 |
| [HID レポートの処理](https://docs.microsoft.com/windows-hardware/drivers/hid/handling-hid-reports) | このセクションでは、ユーザーモードアプリケーションとカーネルモードドライバーが[HID レポート](https://docs.microsoft.com/windows-hardware/drivers/hid/introduction-to-hid-concepts)の処理に使用するメカニズムについて説明します。 |
| [リソースを解放する](https://docs.microsoft.com/windows-hardware/drivers/hid/freeing-resources) | HID クライアントであるユーザーモードアプリケーションとカーネルモードドライバーは、不要になったリソースを常に解放する必要があります。 |
| [HID クライアントのインストール](https://docs.microsoft.com/windows-hardware/drivers/hid/installing-hid-clients) | このセクションでは、Microsoft Windows で HIDClass デバイスをインストールするための次の要件について説明します。 |
| [最上位レベルのコレクションのハードウェア Id を HIDClass する](https://docs.microsoft.com/windows-hardware/drivers/hid/hidclass-hardware-ids-for-top-level-collections) |このセクションでは、HID クラスドライバーが最上位レベルのコレクションに対して生成するハードウェア Id を指定します。 |
| [キーボードとマウスの HID クライアントドライバー](https://docs.microsoft.com/windows-hardware/drivers/hid/keyboard-and-mouse-hid-client-drivers) | このトピックでは、キーボードとマウスの HID クライアントドライバーについて説明します。 キーボードとマウスは、HID の使用表で標準化され、Windows オペレーティングシステムに実装されている最初の HID クライアントのセットを表します。 |
| [センサー HID クラスドライバー](https://docs.microsoft.com/windows-hardware/drivers/hid/sensor-hid-class-driver) | Windows 8 以降、Windows オペレーティングシステムには、HID トランスポートを使用して通信する11種類のセンサーをサポートするインボックスセンサー HID クラスドライバー (SensorsHIDClassDriver .dll) が含まれています。 |
| [航空機モードのラジオ管理](https://docs.microsoft.com/windows-hardware/drivers/hid/airplane-mode-radio-management) | Windows 8 以降では、Windows オペレーティングシステムは、航空機モードのラジオ管理コントロール用に HID を介してサポートを提供します。 |
| [画面の明るさの調整](https://docs.microsoft.com/windows-hardware/drivers/hid/display-brightness-control) | Windows 8 以降では、標準のソリューションが追加されました。キーボードを使用して (外付けまたはノート pc に内蔵)、HID を通じてノート pc やタブレットの画面の明るさを制御します。 |
