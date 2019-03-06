---
title: 複数ロケールのデバイス マニフェスト パッケージの提出
description: 複数ロケールのデバイス マニフェスト パッケージの提出
ms.assetid: b6748bff-d730-434e-9316-dc7b7222b727
ms.topic: article
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a458e1d7dab7983d78b6018eef83ea7762fe5176
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56518980"
---
# <a name="submit-a-multiple-locale-device-manifest-package"></a>複数ロケールのデバイス マニフェスト パッケージの提出


## <a name="span-idsubmittingamultiple-localedevicemanifestpackagespanspan-idsubmittingamultiple-localedevicemanifestpackagespanspan-idsubmittingamultiple-localedevicemanifestpackagespansubmitting-a-multiple-locale-device-manifest-package"></a><span id="Submitting_a_multiple-locale_device_manifest_package"></span><span id="submitting_a_multiple-locale_device_manifest_package"></span><span id="SUBMITTING_A_MULTIPLE-LOCALE_DEVICE_MANIFEST_PACKAGE"></span>複数ロケールのデバイス マニフェスト パッケージの提出


同じ方法を使って、パッケージをプレビュー用またはリリース用に提出できます。

**デバイス マニフェスト パッケージを申請するには**

1.  [SignTool](https://go.microsoft.com/fwlink/p/?LinkId=238330) ツールを使って、devicemanifest-ms パッケージに署名します。

2.  ハードウェア デベロッパー センターまたは Windows デベロッパー センターから Microsoft アカウントで**ダッシュボード**にサインインします。

3.  **[Device metadata]** (デバイス メタデータ) で、新しいエクスペリエンスを申請する場合は **[Create experience]** (エクスペリエンスの作成)、既にあるエクスペリエンスを変更する場合は **[Manage experience]** (エクスペリエンスの管理) をクリックします。

4.  新しい devicemanifest-ms パッケージを参照して選び、**[Submit]** (送信) をクリックします。

## <a name="span-idcreatingadevicemanifestsubmissionpackagespanspan-idcreatingadevicemanifestsubmissionpackagespanspan-idcreatingadevicemanifestsubmissionpackagespancreating-a-device-manifest-submission-package"></a><span id="Creating_a_Device_Manifest_Submission_Package"></span><span id="creating_a_device_manifest_submission_package"></span><span id="CREATING_A_DEVICE_MANIFEST_SUBMISSION_PACKAGE"></span>デバイス マニフェスト サブミッション パッケージの作成


すべての複数ロケール デバイス メタデータは、デバイス マニフェスト提出パッケージとしてハードウェア デベロッパー センター ダッシュボードに提出する必要があります。

デバイス マニフェスト提出パッケージには、ロケールのサポートを宣言するためのファイルが含まれます。 デバイス マニフェスト パッケージには、デバイス メタデータ パッケージも含まれています。

デバイス マニフェスト提出パッケージは、デバイス メタデータ パッケージと同じ方法でハードウェア デベロッパー センター ダッシュボードにアップロードできます。 同じユーザー インターフェイスとアップロード ボックスを使って、アップロードする \*.devicemanifest-ms ファイルの名前を入力します。

ダッシュボードのユーザー インターフェイスのバルク (一括) アップロード用ボックスを除くすべてのファイル アップロード ボックスで、デバイス マニフェスト提出パッケージを指定できます。

### <a name="span-iddevicemanifestsubmissionpackagecontentsspanspan-iddevicemanifestsubmissionpackagecontentsspanspan-iddevicemanifestsubmissionpackagecontentsspandevice-manifest-submission-package-contents"></a><span id="Device_Manifest_Submission_Package_Contents"></span><span id="device_manifest_submission_package_contents"></span><span id="DEVICE_MANIFEST_SUBMISSION_PACKAGE_CONTENTS"></span>デバイス マニフェスト サブミッション パッケージの内容

デバイス マニフェスト サブミッション パッケージは、それぞれ次のコンポーネントで構成されます。

-   デバイス メタデータ パッケージ

    このパッケージには、Windows でのデバイス アイコンの表示、アクションの設定、デバイス エクスペリエンス機能の使用に必要な、情報とグラフィックスが格納されます。

    デバイス メタデータ パッケージは、常に必須です。

-   LocaleInfo XML ドキュメント

    このドキュメントには、同梱のデバイス メタデータ パッケージに含まれるロケールのデータが含まれます。 ハードウェア デベロッパー センターでは、このデータに基づいてデバイス メタデータ パッケージのロケールが検証されます。

    デバイス メタデータ パッケージのロケールが 1 つしかない場合でも、LocaleInfo XML ドキュメントは必須です。

### <a name="span-idstructureofadevicemanifestsubmissionpackagespanspan-idstructureofadevicemanifestsubmissionpackagespanspan-idstructureofadevicemanifestsubmissionpackagespanstructure-of-a-device-manifest-submission-package"></a><span id="Structure_of_a_Device_Manifest_Submission_Package"></span><span id="structure_of_a_device_manifest_submission_package"></span><span id="STRUCTURE_OF_A_DEVICE_MANIFEST_SUBMISSION_PACKAGE"></span>デバイス マニフェスト サブミッション パッケージの構造

デバイス マニフェスト パッケージの構造は、含まれているデバイス メタデータが PC 用とモバイル ブロードバンド用のどちらであるかと、複数のロケールのサポートが含まれているかどうかに依存します。

デバイス メタデータが 3 つのカテゴリのいずれにも該当しない場合、デバイス マニフェスト パッケージは必要ありません。 ただし、デバイス マニフェスト パッケージは、デバイス メタデータ パッケージが単一のロケール用であることを示すために使うこともできます。

### <a name="span-idstructureofmulti-localedevicemanifestsubmissionpackagesspanspan-idstructureofmulti-localedevicemanifestsubmissionpackagesspanspan-idstructureofmulti-localedevicemanifestsubmissionpackagesspanstructure-of-multi-locale-device-manifest-submission-packages"></a><span id="Structure_of_Multi-locale_Device_Manifest_Submission_Packages"></span><span id="structure_of_multi-locale_device_manifest_submission_packages"></span><span id="STRUCTURE_OF_MULTI-LOCALE_DEVICE_MANIFEST_SUBMISSION_PACKAGES"></span>複数ロケールのデバイス マニフェスト サブミッション パッケージの構造

デバイス メタデータ パッケージに複数ロケールをサポートするための情報が含まれている場合も、デバイス マニフェスト パッケージで申請する必要があります。

デバイス マニフェスト サブミッション パッケージのコンポーネントは、圧縮キャビネット ファイルに格納されています。 ファイル名には .devicemanifest-ms というサフィックスを含める必要があります。

それぞれのデバイス マニフェスト サブミッション パッケージに、次の構造が必要です。

``` syntax
GUID1.devicemanifest-ms
\GUID1.devicemetadata-ms
\LocaleInfo.xml
```

"GUID1" には GUID を指定してください。

LocaleInfo.xml を作成する手順については、以降で説明します。

デバイス メタデータ パッケージ (\*.devicemetadata-ms) を開発する方法について詳しくは、[Windows 8 のデバイス メタデータ パッケージのスキーマ リファレンス](https://go.microsoft.com/fwlink/p/?LinkId=226753)をご覧ください。

Cabarc ツールを使って、このような CAB パッケージを作成できます。 このツールについて詳しくは、[Cabarc の概要](https://go.microsoft.com/fwlink/p/?LinkId=248843)に関するページをご覧ください。

Cabarc ツールを使って \*.devicemanifest-ms ファイルを作成した場合、ローカル ディレクトリを作成して、そのルートにデバイス メタデータ パッケージ (\*.devicemetadata-ms) と LocaleInfo XML ドキュメントを格納する必要があります。

**注釈**

-   .devicemanifest -ms と .devicemetadata-ms のファイル名で指定する GUID は、中かっこ ({}) で区切らないでください。

-   それぞれのデバイス マニフェスト サブミッションの GUID とデバイス メタデータ パッケージの GUID は、一意である必要があります。 新しいパッケージまたは変更したパッケージを作成するときには、新しい GUID を作成する必要があります。

-   キャビネット ファイルを作成する方法について詳しくは、[Microsoft キャビネット ソフトウェア開発キット](https://go.microsoft.com/fwlink/p/?LinkId=248844)に関するページをご覧ください。

**例**

Cabarc ツールを使って .devicemanifest-ms ファイルを作成する方法の例を以下に示します。 この例では、デバイス マニフェスト ファイルのコンポーネントは、DeviceManifestPackages という名前のローカル ディレクトリに格納されています。

``` syntax
.\DeviceManifestPackages\
.\DeviceManifestPackages\LocaleInfo.xml
.\DeviceManifestPackages\GUID.devicemetadata-ms
```

ManifestFiles という名前のローカル ディレクトリに、GUID.devicemanifest-ms ファイルが作成されています。

``` syntax
Cabarc.exe -r -p -P  .\DeviceManifestPackages\ 
N .\ManifestFiles\ GUID.devicemanifest-ms 
.\DeviceManifestPackages\LocaleInfo.xml
.\DeviceManifestPackages\GUID.devicemetadata-ms
```

## <a name="span-idcreatinglocaleinfoxmlspanspan-idcreatinglocaleinfoxmlspancreating-localeinfoxml"></a><span id="creating_localeinfo.xml"></span><span id="CREATING_LOCALEINFO.XML"></span>LocaleInfo.xml の作成


Localeinfo.xml ファイルを申請用に作成する方法について詳しくは、「[LocaleInfo.xml サブミッション ファイルの作成](https://msdn.microsoft.com/library/windows/hardware/hh801885.aspx)」をご覧ください。

 

 




