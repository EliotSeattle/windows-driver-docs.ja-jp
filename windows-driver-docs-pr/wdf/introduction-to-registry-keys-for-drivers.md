---
title: ドライバーのレジストリ キーの概要
description: ドライバーのレジストリ キーの概要
ms.assetid: ec1a21db-1a31-4041-941d-31156884ffae
keywords:
- レジストリ WDK KMDF
- レジストリキーオブジェクト WDK KMDF
- フレームワークベースのドライバー WDK KMDF、レジストリ
- カーネルモードドライバー WDK KMDF、レジストリ
- KMDF WDK、レジストリ
- カーネルモードドライバーフレームワーク WDK、レジストリ
- パラメーターキー WDK KMDF
- ソフトウェアキー WDK KMDF
- ドライバーキー WDK KMDF
- ハードウェアキー WDK KMDF
- キー WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 629ee67117cc78ff673658a7ab4032e90c277a7a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843161"
---
# <a name="introduction-to-registry-keys-for-drivers"></a>ドライバーのレジストリ キーの概要


通常、ドライバーは、システム定義のレジストリキーのセットを使用して、ドライバー固有またはデバイス固有の情報を格納したり、アクセスしたりします。 ドライバーが次のレジストリキーにアクセスする可能性があります。

-   **パラメーター**キー

    ドライバーの**Parameters**キーには、ドライバーの構成情報を含めることができます。 カーネルモードドライバーフレームワーク (KMDF) ドライバーの場合、このキーは、 [**HKLM\\SYSTEM\\CurrentControlSet\\Services**](https://docs.microsoft.com/windows-hardware/drivers/install/hklm-system-currentcontrolset-services-registry-tree)ツリーのドライバーのサービス名の下にあります。 ユーザーモードドライバーフレームワーク (UMDF) ドライバーの場合、このキーは、 **Microsoft\\WINDOWS NT\\CurrentVersion\\WUDF\\サービスツリーの HKLM\\ソフトウェア\\** 、ドライバーのサービス名の下にあります。 ドライバーのファイル名とサービス名が異なる場合でも、ドライバーのサブキーは常にドライバーのサービス名を使用します。

    システムはドライバーの[**Driverentry**](https://docs.microsoft.com/windows-hardware/drivers/wdf/driverentry-for-kmdf-drivers)ルーチンを呼び出すと、ドライバーの**サービス**ツリーへのパスを渡します。 ドライバーは、このパスを[**Wdfdrivercreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nf-wdfdriver-wdfdrivercreate)に渡す必要があります。 その後、ドライバーは[**WdfDriverGetRegistryPath**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nf-wdfdriver-wdfdrivergetregistrypath)を呼び出すことによってパスを取得でき、ドライバーは[**WdfDriverOpenParametersRegistryKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nf-wdfdriver-wdfdriveropenparametersregistrykey)を呼び出すことによって**パラメーター**キーを開くことができます。

-   ソフトウェアキー

    ドライバーのソフトウェアキーは、その*ドライバーキー*とも呼ばれます。 システムは、各ドライバーに関する情報をソフトウェアキーの下に保存します。

    ドライバーは、 [**Wdffdoinitopenregistrykey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdffdo/nf-wdffdo-wdffdoinitopenregistrykey)と[**wdfdeviceopenregistrykey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceopenregistrykey)を呼び出して、デバイスのソフトウェアキーを開くことができます。

    ドライバーの INF ファイルには、inf [**DDInstall セクション**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-ddinstall-section)を使用して、ソフトウェアキーの下にレジストリ値を設定する[**inf AddReg ディレクティブ**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addreg-directive)を含めることができます。

-   ハードウェアキー

    デバイスがシステムに接続されていることをドライバースタックがプラグアンドプレイ (PnP) マネージャーに通知すると、PnP マネージャーによってそのデバイスのハードウェアキーが作成されます。 このキーは、*デバイスキー*とも呼ばれます。 ハードウェア (割り込み設定など) に関連する設定は、ドライバーによってここに格納できます。

    ドライバーは、 [**Wdffdoinitopenregistrykey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdffdo/nf-wdffdo-wdffdoinitopenregistrykey)と[**wdfdeviceopenregistrykey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceopenregistrykey)を呼び出して、デバイスのハードウェアキーを開くことができます。

    ドライバーの INF ファイルには、inf [**DDInstall. HW セクション**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-ddinstall-hw-section)を使用して、ハードウェアキーの下にレジストリ値を設定する[**inf AddReg ディレクティブ**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addreg-directive)を含めることができます。

ドライバーの種類で、特定のレジストリキーの下に情報を保存する必要があるかどうかを判断するには、このドキュメントの目次を使用して、ドライバーのデバイスの種類について説明しているセクションを参照してください。

ドライバーのレジストリキーの詳細については、次を参照してください。

-   [レジストリツリーとキーの概要](https://docs.microsoft.com/windows-hardware/drivers/install/overview-of-registry-trees-and-keys)

-   [ドライバーでのレジストリの使用](https://docs.microsoft.com/windows-hardware/drivers/kernel/using-the-registry-in-a-driver)

 

 





