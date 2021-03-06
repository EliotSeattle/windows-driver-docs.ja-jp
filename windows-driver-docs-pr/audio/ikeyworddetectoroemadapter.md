---
title: IKeywordDetectorOemAdapter インターフェイス
description: IKeywordDetectorOemAdapter は、音声のライセンス認証ドライバー インターフェイスと対話するためのコンポーネント オブジェクト モデル (COM) インターフェイスです。 IKeywordDetectorOemAdapter インターフェイスは、Windows 10 および Windows の以降のバージョンでサポートされます。
ms.assetid: FB243792-C0B0-4BCA-B4C4-B6E17FDB615C
keywords:
- IKeywordDetectorOemAdapter インターフェイス オーディオ デバイス
- 説明されている IKeywordDetectorOemAdapter インターフェイス オーディオ デバイス
topic_type:
- apiref
api_name:
- IKeywordDetectorOemAdapter
api_type:
- COM
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: aabd2d129a43d7add6b7e19d8097f68da2b8d915
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67359951"
---
# <a name="ikeyworddetectoroemadapter-interface"></a>IKeywordDetectorOemAdapter インターフェイス


**IKeywordDetectorOemAdapter**音声のライセンス認証ドライバー インターフェイスと対話するためのコンポーネント オブジェクト モデル (COM) のインターフェイスです。 **IKeywordDetectorOemAdapter**インターフェイスは、Windows 10 および以降のバージョンの Windows でサポートされます。

計算やを使ってオーディオ ドライバーに読み取りし、書き込みは非透過的なデータを解析して、オペレーティング システムと、ドライバーの間の媒介として機能する COM オブジェクトの実装を提供する OEM [ **KSPROPERTY\_SOUNDDETECTOR\_パターン**](ksproperty-sounddetector-patterns.md)と[ **KSPROPERTY\_SOUNDDETECTOR\_MATCHRESULT**](ksproperty-sounddetector-matchresult.md)します。

COM オブジェクトのクラス id (CLSID) が検出器パターンの種類によって返される GUID、 [ **KSPROPERTY\_SOUNDDETECTOR\_SUPPORTEDPATTERNS**](ksproperty-sounddetector-supportedpatterns.md)します。 オペレーティング システムの呼び出し[ **CoCreateInstance** ](https://docs.microsoft.com/windows/desktop/api/combaseapi/nf-combaseapi-cocreateinstance)キーワード パターンの種類と互換性のオブジェクトのメソッドを呼び出して適切な COM オブジェクトをインスタンス化するパターンの種類の GUID を渡す**IKeywordDetectorOemAdapter**インターフェイス。 オペレーティング システムのプロキシとスタブを提供**IKeywordDetectorOemAdapter**します。 OEM の実装には、COM スレッド モデルのいずれかを選択できます。

インターフェイスのデザインは、オブジェクトの実装をステートレスに保持しようとします。 つまり、実装する必要がありますは必要ありませんメソッド呼び出しの間に格納される状態。 実際には、可能性の高い内部の C++ クラスには、一般に、COM オブジェクトを実装するために必要なもの以外のすべてのメンバー変数は必要ありません。

<a name="members"></a>Members
-------

**IKeywordDetectorOemAdapter**インターフェイスから継承、 [ **IUnknown** ](https://docs.microsoft.com/windows/desktop/api/unknwn/nn-unknwn-iunknown)インターフェイスしますが、追加のメンバーはありません。

 

 





