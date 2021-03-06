---
title: デバイス メタデータ パッケージの概要
description: デバイス メタデータ パッケージの概要
ms.assetid: 1b17bdab-44e4-498b-ab80-f28fa94d9821
keywords:
- デバイス メタデータ、WDK をパッケージ化について
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c257eb5f37e7a73fa5c12fe7db5099f61801e9b0
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379442"
---
# <a name="overview-of-device-metadata-packages"></a>デバイス メタデータ パッケージの概要

Windows 7 以降のデバイス メタデータ パッケージには、デバイスとそのハードウェア関数のプロパティを表す XML ドキュメントが含まれています。 デバイスとプリンターのユーザー インターフェイスでは、デバイスのメタデータ パッケージの XML ドキュメントに基づくユーザーをデバイスに固有の情報を表示します。

デバイス メタデータ パッケージは複数の XML ドキュメントと各ドキュメントは、デバイスの属性のさまざまなコンポーネントを指定します。

通常は 1 つのウィンドウ内のコンピューターに接続するデバイスのほとんどは、以降、Windows 7 デバイスの場合、新しいユーザー インターフェイスでデバイスとプリンター から示します。 このウィンドウには、ギャラリー ビューが呼び出されます。 ギャラリー ビューに表示される各デバイスのデバイスとプリンターは、デバイスのメタデータ パッケージの XML ドキュメントに基づくユーザーをデバイスに固有の情報が表示されます。 これらの XML ドキュメントを使用すると、OEM は、どのような情報が含まれており、この情報の表示方法をカスタマイズできます。 たとえば、ギャラリー ビュー内のデバイスは、カスタム アイコンおよび OEM が提供する説明のテキストで表現できます。

デバイス メタデータ パッケージ内に含まれる XML ドキュメントでは、物理デバイスを記述する情報を指定します。 次に、XML ドキュメントが指定できる情報の種類を示します。

-   OEM の名前。

-   モデル名とデバイスの説明。

-   デバイスをサポートする 1 つまたは複数の機能カテゴリ。

各デバイス メタデータ パッケージは、次のコンポーネントで構成されます。

<a href="" id="packageinfo-xml-document"></a>[PackageInfo の XML ドキュメント](packageinfo-xml-document.md)  
このドキュメントには、デバイス メタデータ パッケージの内容を指定するデータが含まれています。 オペレーティング システムでは、このデータを使用するパッケージをインストールし、その内容を参照します。

このデータはに基づいて書式設定、 [PackageInfo XML スキーマ](https://docs.microsoft.com/previous-versions/windows/hardware/metadata/ff549614(v=vs.85))します。

<a href="" id="deviceinfo-xml-document"></a>[DeviceInfo XML ドキュメント](deviceinfo-xml-document.md)  
このドキュメントには、デバイスのカテゴリおよびモデルの名前などのデバイスのプロパティを指定するデータが含まれています。 デバイスとプリンターのユーザー インターフェイスでは、このデータを使用して、デバイスに関する詳細情報を示します。

このデータはに基づいて書式設定、 [DeviceInfo XML スキーマ](https://docs.microsoft.com/previous-versions/windows/hardware/metadata/ff541135(v=vs.85))します。

<a href="" id="device-icon-file"></a>[デバイス アイコン ファイル](device-icon-file.md)  
このファイルには、デバイスとプリンターのユーザー インターフェイスでデバイスを表す写真のようなイメージが含まれます。

<a href="" id="windowsinfo-xml-document"></a>[WindowsInfo XML ドキュメント](windowsinfo-xml-document.md)  
このドキュメントには、デバイス メタデータ パッケージの指定したデバイスのデバイスとプリンターのユーザー インターフェイスを実行するアクションを表示を指定するデータが含まれています。

このデータはに基づいて書式設定、 [WindowsInfo XML スキーマ](https://docs.microsoft.com/previous-versions/windows/hardware/metadata/ff553992(v=vs.85))します。

各デバイス メタデータ パッケージは、Cabarc を使用して 1 つのファイルに圧縮のコンポーネント (*Cabarc.exe*) ツール。 このツールの詳細についてを参照してください、 [Cabarc 概要](https://go.microsoft.com/fwlink/p/?linkid=145395)web サイト。

デバイス メタデータ パッケージのファイル名は、次の名前付け規則を使用します。

```cpp
<GUID>.devicemetadata-ms
```

*&lt;GUID&gt;* ファイルのプレフィックスは、デバイス メタデータ パッケージの作成はグローバル一意識別子 (GUID)。 各メタデータ パッケージのファイル名の GUID は一意である必要があります。 新規または変更されたメタデータ パッケージを作成するときに、変更はわずか場合でも、新しい GUID を作成する必要があります。

詳細については、次を参照してください。[デバイス メタデータ パッケージのビルドに関して](building-device-metadata-packages.md)します。

 

 





