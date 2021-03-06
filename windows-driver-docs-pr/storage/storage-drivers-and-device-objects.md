---
title: ストレージドライバーとデバイスオブジェクトについて
description: ストレージ ドライバーとデバイス オブジェクト
ms.assetid: dbadebe6-b2ae-4dc2-837b-5ca9634d45d0
keywords:
- ストレージドライバー WDK、デバイスオブジェクト
- デバイスオブジェクト WDK ストレージ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d3f0194a1cfc3e725f773b237a927342ad4df8e1
ms.sourcegitcommit: e1ff1dd43b87dfb7349cebf70ed2878dc8d7c794
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/02/2020
ms.locfileid: "75606478"
---
# <a name="about-storage-drivers-and-device-objects"></a>ストレージドライバーとデバイスオブジェクトについて

記憶装置スタックは、システム上の記憶装置への i/o 処理に関係するドライバーによって作成されたデバイスオブジェクトのツリーで構成されます。 このツリーのルートは、記憶域アダプターまたは記憶域スタックと統合された別のドライバースタックの機能デバイスオブジェクト (FDO) です。 このツリーのリーフは、ファイルシステムおよびユーザーモードアプリケーションが使用するデバイスオブジェクトです。

任意の PnP ドライバーと同様に、ストレージクラスまたは記憶域フィルタードライバーは、初期化時に PnP マネージャーによってドライバーの AddDevice ルーチンに渡されたデバイスオブジェクトへのポインターを使用して、 **IoCreateDevice**でデバイスオブジェクトを作成し、それを**Ioattachdevicetodevicestack**を使用してデバイススタックにアタッチすることによって、それ自体をツリーに追加 **Ioattachdevicetodevicestack**新しいデバイスオブジェクトをデバイススタックの現在の上にアタッチします。

Tape miniclass、medium チェンジャー miniclass、または SCSI ミニポートドライバーは、デバイスオブジェクトを作成し、デバイススタックに接続するためには必要ありません。 代わりに、システムによって提供されるテープクラス、チェンジャークラス、または SCSI ポートドライバーが、miniclass/ミニポートに代わってこれらのタスクを処理し、miniclass/ミニポートドライバールーチンを呼び出して、デバイスオブジェクトを作成するために必要なデータを収集します。

記憶域ポートドライバーは、FILE_DEVICE_MASS_STORAGE 種類の物理デバイスオブジェクト (PDOs) を作成します。 ディスククラス、CD-ROM クラス、テープクラス、およびチェンジャークラスのドライバーは、それぞれ FILE_DEVICE_DISK、FILE_DEVICE_CD_ROM、FILE_DEVICE_TAPE、および FILE_DEVICE_CHANGER 型の FDOs を作成します。

PnP ドライバーの設計の詳細については、 [Pnp ドライバーの設計ガイドライン](https://docs.microsoft.com/windows-hardware/drivers/kernel/pnp-driver-design-guidelines)を参照してください。 PnP 関連の **Io * * Xxx*ルーチンの詳細については、[プラグアンドプレイルーチン](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)を参照してください。
