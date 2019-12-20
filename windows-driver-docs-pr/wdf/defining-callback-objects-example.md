---
title: コールバック オブジェクトの定義の例
description: コールバック オブジェクトの定義の例
ms.assetid: d987bb95-cbee-46aa-beaf-167572ca4a80
keywords:
- コールバックオブジェクト WDK UMDF、定義の例
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3bd034d0ac3a8b34034ce1d79b54db08ed1967ca
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75210488"
---
# <a name="defining-callback-objects-example"></a>コールバック オブジェクトの定義の例


[!include[UMDF 1 Deprecation](../includes/umdf-1-deprecation.md)]

次のコード例は、デバイスのコールバックオブジェクトを定義するために、ドライバーが[IPnpCallbackHardware](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-ipnpcallbackhardware)インターフェイスから継承する方法を示しています。

```cpp
class CMyDevice :
       // Callback interface exposed to the framework
       public IPnpCallbackHardware 
{// The following data members make up the context
private:
   HANDLE                  m_CompletionPort;
   WINUSB_INTERFACE HANDLE m_UsbHandle;
   UCHAR                   m_BulkOutPipe;
   ULONG                   m_BulkOutMaxPacket;
   ...
// The following methods make up the callback interfaces
public:
    virtual HRESULT stdcall OnPrepareHardware( 
                              IWDFDevice* pDevice
                              );
    STDMETHOD( OnReleaseHardware )( IWDFDevice *pDevice );

   // Method used to create a device callback object
   static HRESULT CreateInstance( 
                     IUnknown **ppUnknown, 
                     IWDFDeviceInitialize *pDeviceInit,
                     HANDLE CompletionPort 
                     );
   ...
};
```

 

 





