---
title: 印刷フィルターの非同期通知
description: 印刷フィルターの非同期通知
ms.assetid: 52b0790b-4927-4e1b-8ae5-6e2afc7c9df6
keywords:
- レンダーモジュール WDK XPSDrv、XPS フィルター
- XPS フィルター WDK XPSDrv
- WDK XPS をフィルター処理します
- 非同期通知 WDK XPS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c56615d841dc7f3080065d3d38fd37af91566b1f
ms.sourcegitcommit: 3ee05aabaf9c5e14af56ce5f1dde588c2c7eb4ec
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/06/2019
ms.locfileid: "74881926"
---
# <a name="asynchronous-notifications-in-print-filters"></a>印刷フィルターの非同期通知

印刷フィルターパイプラインには、非同期通知機能があります。この機能は、アプリケーションの印刷スプーラでサポートされている非同期通知によく似ています。 印刷スプーラーで使用できる[**RouterCreatePrintAsyncNotificationChannel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prnasntp/nf-prnasntp-routercreateprintasyncnotificationchannel)関数は、印刷フィルターでは使用できません。 印刷フィルターでは、 [IPrintClassObjectFactory](https://docs.microsoft.com/windows-hardware/drivers/ddi/filterpipeline/nn-filterpipeline-iprintclassobjectfactory)インターフェイスを使用して IPrintAsyncNotify オブジェクトを作成する必要があります。

このトピックでは、印刷フィルターで非同期通知機能を使用する方法について説明します。

> [!NOTE]
> 印刷フィルターからの非同期通知のスローは、v4 印刷ドライバーモデルではサポートされていません。

## <a name="iprintclassobjectfactory"></a>IPrintClassObjectFactory

[IPrintClassObjectFactory](https://docs.microsoft.com/windows-hardware/drivers/ddi/filterpipeline/nn-filterpipeline-iprintclassobjectfactory)インターフェイスは、通知インターフェイスへのアクセスを提供します。 次のコード例は、フィルターがプロパティバッグからこのインターフェイスを取得する方法を示しています。

```cpp
// This interface is defined as a private member variable in the filter class
IPrintClassObjectFactory  *m_pPrintClassFactory;

// The following code goes in the IntializeFilter method of the filter
VARIANT var;
VariantInit(&var);

HRESULT hr = pIPropertyBag->GetProperty(
    XPS_FP_PRINT_CLASS_FACTORY, 
    &var);

if (SUCCEEDED(hr))
{
    hr = V_UNKNOWN(&var)->QueryInterface(
 IID_IPrintClassObjectFactory,
 reinterpret_cast<void **>(&m_pPrintClassFactory));
}
```

## <a name="notification-channel"></a>通知チャンネル

IPrintClassObjectFactory インターフェイスを使用すると、フィルターのニーズに応じて、一方向または双方向の通知チャネルをフィルターで作成できます。 次のコード例は、前の例から続き、フィルターが一方向の通知チャネルを確立する方法を示しています。

```cpp
// Create a unidirectional notification channel
IPrintAsyncNotifyChannel  *pIAsyncNotifyChannel;
IPrintAsyncNotify  *pIAsyncNotify;

HRESULT hr = m_pPrintClassFactory->GetPrintClassObject(
 m_bstrPrinter,      // The printer name that was read from the property bag
 IID_IPrintAsyncNotify,
 reinterpret_cast<void**>(&pIAsyncNotify)));

if (SUCCEEDED(hr))
{
    hr = pIAsyncNotify->CreatePrintAsyncNotifyChannel(
 m_jobId,
 const_cast<GUID*>(&MS_ASYNCNOTIFY_UI),
 kPerUser,
 kUniDirectional,
        NULL,
        &pIAsyncNotifyChannel));

   // etc...
}
```

双方向の通知チャネルを作成するには、前の例の代わりに次のコード例を使用します。

```cpp
// Create a bidirectional notification channel
IPrintAsyncNotifyChannel *pIAsyncNotifyChannel;
IPrintAsyncNotify *pIAsyncNotify;

HRESULT hr = m_pPrintClassFactory->GetPrintClassObject(
 m_bstrPrinterName,   // The printer name that was read from the property bag
 IID_IPrintAsyncNotify,
 reinterpret_cast<void**>(&pIAsyncNotify)));

if (SUCCEEDED(hr))
{
    hr = pIAsyncNotify->CreatePrintAsyncNotifyChannel(
 m_jobId,
 const_cast<GUID*>(& SAMPLE_ASYNCNOTIFY_UI),
 kPerUser,
 kBiDirectional,
 pIAsyncCallback,
        &pIAsyncNotifyChannel));

    // etc...
}
```

前のコード例では、変数 `pIAsyncCallback` は、 [IPrintAsyncNotifyCallback](https://go.microsoft.com/fwlink/p/?linkid=124755)インターフェイスの呼び出し元の実装へのポインターです。

場合によっては、完了後に双方向通知チャネルを解放する必要があります。 これを行うには、 [IPrintAsyncNotifyChannel](https://go.microsoft.com/fwlink/p/?linkid=124758)で[Release](https://go.microsoft.com/fwlink/p/?linkid=98433)メソッドを呼び出します。 チャネルを解放するタイミングの詳細については、「 [Notification channel](notification-channel.md)」を参照してください。

## <a name="impersonation-and-notification"></a>権限借用と通知

フィルターは、IPrintAsyncNotify:: CreatePrintAsyncNotifyChannel メソッドを呼び出すときに、ユーザーアカウントを偽装しないようにする必要があります。 印刷スプーラの承認メカニズムでは、ローカルサービスアカウントから呼び出される必要があります。 フィルターが、ジョブを送信したユーザーのアカウントの権限を借用する必要がある場合は、CreatePrintAsyncNotifyChannel を呼び出す前にフィルターをそれ自体に戻す必要があります。 呼び出しが返された後、必要に応じて、フィルターを使用してユーザーアカウントに戻すことができます。

> [!NOTE]
> ローカルサービスコンテキストで通知の呼び出しが行われている場合でも、ジョブ ID のユーザーの関連付けに基づいてジョブを送信したユーザーには、kPerUser 通知が送信されます。

## <a name="adapting-the-wdk-sample-code"></a>WDK サンプルコードを適合させる

RouterCreatePrintAsyncNotificationChannel 呼び出しを次のコード例に置き換えることによって、WDK サンプルコードの通知サンプルを調整して印刷フィルターで動作させることができます。

```cpp
IPrintAsyncNotify  *pIAsyncNotify;

HRESULT hr = m_pPrintClassFactory->GetPrintClassObject(
 m_bstrPrinterName,      // get it from the property bag
 IID_IPrintAsyncNotify,
 reinterpret_cast<void**>(&pIAsyncNotify)));

if (SUCCEEDED(hr))
{
    hr = pIAsyncNotify->CreatePrintAsyncNotifyChannel(
 // the same arguments as for 
 // RouterCreatePrintAsyncNotificationChannel
        );

    // Etc.
}
```
