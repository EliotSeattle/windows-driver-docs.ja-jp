---
title: デバイス インスタンス識別子の取得
description: デバイス インスタンス識別子の取得
ms.assetid: 6382fdf6-109a-430a-b6b5-322d3eebc4a1
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e218b76363a216c01dde86b97d8d45a94fadccc4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67387309"
---
# <a name="retrieving-a-device-instance-identifier"></a>デバイス インスタンス識別子の取得


Windows Vista および Windows での以降のバージョンで、[統一されたデバイス プロパティのモデル](unified-device-property-model--windows-vista-and-later-.md)デバイス インスタンス識別子を表すデバイスのプロパティをサポートしています。 統一されたデバイス プロパティのモデルを使用して、 [ **DEVPKEY_Device_InstanceId**](https://docs.microsoft.com/windows-hardware/drivers/install/devpkey-device-instanceid) [プロパティ キー](property-keys.md)をこのプロパティを表します。

Windows Server 2003、Windows XP、および Windows 2000 は、このプロパティもサポートします。 ただし、以前の Windows バージョンには、統一されたデバイス プロパティのモデルのプロパティのキーはできません。 呼び出すことによって、以前のバージョンの Windows でのデバイス インスタンス id を取得する代わりに、 [ **SetupDiGetDeviceInstanceId**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdeviceinstanceida)します。 Windows の以前のバージョンとの互換性を維持するために Windows Vista およびそれ以降のバージョンもサポート**SetupDiGetDeviceInstanceId**します。 ただし、Windows Vista では、このプロパティにアクセスするキーおよびそれ以降は、対応するプロパティを使用する必要があります。

プロパティのキーを使用して、Windows Vista およびそれ以降のバージョンのデバイス ドライバーのプロパティにアクセスする方法については、次を参照してください。[プロパティへのアクセス デバイス インスタンス (Windows Vista 以降)](accessing-device-instance-properties--windows-vista-and-later-.md)します。

Windows Server 2003、Windows XP、および Windows 2000 でデバイス インスタンス id を取得するには、次の手順に従います。

1.  呼び出す**SetupDiGetDeviceInstanceId**デバイス インスタンス id のバイト単位のサイズを取得します。 次のパラメーター値を指定します。

    -   設定*DeviceInfoSet*に要求されたデバイスのインスタンス識別子を取得する対象のデバイス情報の要素が含まれるデバイス情報のセットを識別するハンドル。
    -   設定*DeviceInfoData*へのポインター、 [ **SP_DEVINFO_DATA** ](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_devinfo_data)デバイス インスタンスを取得する対象のデバイス情報の要素を表す構造体識別子です。
    -   設定*DeviceInstanceId*に**NULL**します。
    -   設定*DeviceInstanceIdSize*をゼロにします。
    -   設定*RequiredSize*を NULL で終わるデバイス インスタンス識別子を格納するために必要な文字数を受け取る DWORD に型指定された変数へのポインター。

    最初の呼び出しに応答[ **SetupDiGetDeviceInstanceId**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdeviceinstanceida)、 **SetupDiGetDeviceInstanceId**設定\* *RequiredSize*プロパティ値を取得するために必要なバッファーのバイト単位でログ、ERROR_INSUFFICIENT_BUFFER エラー コードのサイズにし、返します**FALSE**します。 後続の呼び出し[GetLastError](https://go.microsoft.com/fwlink/p/?linkid=169416)最近ログインしたエラー コードを返します。

2.  呼び出す**SetupDiGetDeviceInstanceId**もう一度次の変更を除き、最初の呼び出しで指定された同じパラメーター値を提供します。
    -   設定*DeviceInstanceId*デバイス情報の要素に関連付けられているデバイスの NULL で終わるインスタンス識別子を受け取る文字列バッファーへのポインター。
    -   設定*DeviceInstanceIdSize*文字数、サイズの*DeviceInstanceId*バッファー。 最初の呼び出し**SetupDiGetDeviceInstanceId**の必要なサイズを取得、 *DeviceInstanceId*内でバッファー \* *RequiredSize*します。

2 番目の呼び出しに場合**SetupDiGetDeviceInstanceId**成功すると、 **SetupDiGetDeviceInstanceId**設定、 *DeviceInstanceId*デバイス インスタンス識別子では、バッファー設定\* *RequiredSize*文字単位のサイズのデバイスのインスタンス識別子が取得されたを返す**TRUE**します。 関数呼び出しが失敗した場合、 **SetupDiGetDeviceInstanceId**返します**FALSE**への呼び出しと[GetLastError](https://go.microsoft.com/fwlink/p/?linkid=169416)ログに記録されたエラー コードを返します。

 

 





