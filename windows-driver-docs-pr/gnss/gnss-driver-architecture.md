---
title: グローバルナビゲーションサテライトシステム (GNSS) ドライバーのアーキテクチャ
description: グローバルナビゲーションサテライトシステム (GNSS) の UMDF 2.0 ドライバーアーキテクチャと i/o に関する考慮事項の概要を示し、いくつかの種類の追跡と修正セッションについて説明します。
ms.assetid: 11B54F92-DC84-4D74-9BBE-C85047AD2167
ms.date: 05/17/2018
ms.localizationpriority: medium
ms.openlocfilehash: d2393e7385a60092dc3f1945b62f225cad02fa01
ms.sourcegitcommit: 96f94bffe426b7f92913fa0ffff1918c76e0e52c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/04/2020
ms.locfileid: "76980701"
---
# <a name="global-navigation-satellite-system-gnss-driver-architecture"></a>グローバルナビゲーションサテライトシステム (GNSS) ドライバーのアーキテクチャ

グローバルナビゲーションサテライトシステム (GNSS) の UMDF 2.0 ドライバーアーキテクチャと i/o に関する考慮事項の概要を示し、いくつかの種類の追跡と修正セッションについて説明します。

## <a name="architecure-overview"></a>アーキテクチャの概要

次の高レベルのコンポーネントブロック図は、グローバルナビゲーションサテライトシステム (GNSS) の UMDF 2.0 ドライバーが Windows 10 プラットフォームとどのように統合されるかを示しています。

![ユーザーモード gnss アーキテクチャを示す図](images/gnss-architecture-4.png)

図のコンポーネントについては、次を参照してください。

- **アプリケーションの実行 (ポンド):** Windows 10 プラットフォームの場所機能を使用するユーザーアプリケーション

- **テストアプリケーション:** GNSS 機能をテストするためのアプリケーション。

- **GNSS API:** **Ignssadapter** COM (コンポーネントオブジェクトモデル) インターフェイス。 gnss デバイスの機能をロケーションサービスの内部コンポーネントに公開したり、アプリケーションをテストしたりします。 この API の正確な構造は、このドキュメントの範囲外です。 Windows コンポーネントは、 **Ignssadapter** COM インターフェイスに対してプログラミングすることによって、gnss デバイスを使用します。 GNSS API セットは、場所のプラットフォームコンポーネント (ロケーションサービスや場所のテストアプリケーションなど) のみに対するプライベート API であり、他のファーストパーティまたはサードパーティ製のアプリケーションでは使用できません。

- **Gnss アダプター:** これは、 **Ignssadapter** COM インターフェイスを実装するシングルトン com オブジェクトです。 テストアプリケーションとロケーションサービスの内部コンポーネントは、このオブジェクトをインスタンス化し、 **Ignssadapter**インターフェイスを介して gnss デバイスを使用します。 ロケーションサービスの GNSS ポジショニングエンジンコンポーネントは、 **Ignssadapter**インターフェイスを公開する COM クラスを実装します。 ロケーションサービスは、場所サービス内で GNSS adapter COM クラスのシングルトン COM オブジェクトをインスタンス化するために、テストおよびその他のアウトプロセスアプリケーションをテストするファクトリメカニズムを公開します。 アウトプロセスアプリケーションは、COM インターフェイスポインターを使用して、GNSS ドライバーに対してプログラムを実行します。

    > [!NOTE]
    > COM はアウトプロセスアプリケーションへのインターフェイスポインターを処理します。これにより、アプリケーションは**Ignssadapter**インターフェイスポインターをインプロセス COM オブジェクトとして処理しますが、呼び出しは実際にロケーションサービス内のシングルトン gnss アダプターオブジェクトによって処理されます。

    GNSS ポジショニングエンジンは、location service に場所固有の機能を提供するために、内部の GNSS アダプターオブジェクトを使用します。 GNSS アダプターは、 **CreateFile** API を使用して gnss ドライバーへのファイルハンドルを開き、gnss ネイティブ api 呼び出しを適切な**DeviceIoControl**呼び出しにラップして、gnss ドライバーオブジェクトを使用してステートマシンを保持し、上位層からのさまざまな受信要求の状態を維持します。 このコンポーネントは、このドキュメントで定義されているパブリック GNSS IOCTL インターフェイスを介して、基になる GNSS デバイススタックと直接やり取りします。 GNSS デバイスは、論理的に排他的なリソースとして扱われるため、シングルトンのデバイスへのすべてのアクセスを制御します。

    > [!NOTE]
    >特定のホワイトボックスドライバーテストアプリケーションでは、gnss プライベート Api を介して gnss アダプターを使用するのではなく、非運用環境で、GNSS ドライバーの IOCTL インターフェイスを直接使用することもでき  。 ただし、これらのテストアプリケーションでは、GNSS アダプターの特定の機能を模倣するために、独自のステートマシンと処理を実装する必要があります。

- **Gnss ドライバー:** UMDF 2.0 を使用して実装された、IHV が提供するドライバー。 GNSS ドライバーは、実際の GNSS ハードウェアとやり取りすることで、GNSS **DeviceIoControl** api をサポートしています。 GNSS ドライバーは、SUPL 関数の媒介/インテグレーターとしても機能します。

- **Gnss デバイス/エンジン:** これは、GNSS デバイスの SoC とハードウェアの部分をカプセル化した概念コンポーネントです。 IHV は、このコンポーネント内に GNSS の機能の大部分を実装することを選択することができます。これにより、GNSS ドライバーレイヤーが非常に薄い (基本的には、GNSS デバイスとの通信用のアダプター) ことになります。

## <a name="support-for-global-navigation-satellite-system-gnss-devices-and-drivers-that-follow-the-legacy-windows-model"></a>従来の Windows モデルに準拠するグローバルナビゲーションサテライトシステム (GNSS) デバイスとドライバーのサポート

Windows 10 のロケーションプラットフォームでは、従来のセンサー v1.0 クラスドライバーを使用して統合された GNSS デバイス、または「その[Gnss driver reference](https://docs.microsoft.com/windows-hardware/drivers/ddi/gnssdriver)」で説明されている新しい GNSS DDI を通じて統合さ[れている](writing-a-location-sensor-driver.md)デバイスをサポートしています。

このため、windows 7、Windows 8、および Windows 8.1 に存在していたセンサー v1.0 クラス拡張モデルと統合された Windows デバイスは、変更を必要とせずに Windows 10 で動作を継続することが期待されます。 ユーザーのアップグレードプロセスを改善するために、これらのドライバー (および新しいドライバー) を Windows Update に発行することを強くお勧めします。

また、Windows 10 で発行されたハードウェアラボキット (HLK) の GNSS デバイスに対して、2つの異なるテストセットがあります。

- 新しいモデルに従ってドライバーを認定する新しいテストセット。

- 古いモデルに従ってドライバーを認定するための別のテストセット。 これらのテストは、Windows 8.1 の WHCK 用意されていたものと同じです。

HLK の新しい gatherer コンポーネントによって、システムで実行する必要がある2つのテストセット (存在する場合) が識別されます。

![gnss 2.0 ドライバーとアダプターの通信を示す図](images/gnss-architecture-5.png)

## <a name="coexistence-of-global-navigation-satellite-system-gnss-devices"></a>グローバルナビゲーションサテライトシステム (GNSS) デバイスの共存

システムで複数の GNSS デバイスが検出された場合は、システムの全体的な電力消費量を減らすために、主に1つのデバイスのみを使用します。 次の仮定が考慮されました。

- 新しい DDI を使用するデバイスは、より新しいものになる可能性が高いため、電力消費が増える可能性が高く、より多くの constellations をサポートし、サポートを向上させることができます。 したがって、古いドライバーモデルを使用しているデバイスと新しいドライバーモデルを使用しているデバイスが検出された場合、後者は選択されたものになります。

- 内部の GNSS デバイスが存在するときにユーザーが外部の GNSS デバイスを接続した場合、この外部デバイスが使用される可能性が最も高くなります。

次のような仮定に基づいて、ロケーションプラットフォームの動作が決まります。

- 2つの coexistent レガシドライバーの場合: 互換性の問題を回避するために、動作は Windows 8.1 と同じになります。この動作は、両方の GNSS デバイスが同時に使用され、応答の1つがアプリケーションにスタックとして伝達されます。

- デバイスに1つのレガシドライバーがあり、1つの新しいドライバーが外部に接続されている場合: 外部接続された GNSS デバイスが使用されます。

- デバイスに1つの新しいドライバーがあり、1つの新しいドライバーが外部に接続されている場合: 外部に接続されている GNSS デバイスが使用されます。

選択した GNSS デバイスがジオフェンシングまたはその他のオフロード操作をサポートしている場合、そのデバイスが使用されている間はオフロードが実行されます。 GNSS アダプターでは、複数の GNSS デバイス間で機能またはセッションが分割されることはありません。

## <a name="global-navigation-satellite-system-gnss-interface-overview"></a>グローバルナビゲーションサテライトシステム (GNSS) インターフェイスの概要

GNSS アダプターと GNSS ドライバー間の相互作用は、次のカテゴリに分類されます。

### <a name="capability-information-exchange"></a>機能情報の交換

Windows プラットフォームでの GNSS スタックの拡張性と適応性をサポートするために、GNSS アダプターと GNSS ドライバーは、基になる GNSS スタックの明確に定義されたさまざまな機能に加えて、Windows プラットフォーム。 機能の側面は、この GNSS インターフェイス定義の一部として Microsoft によって適切に定義されています。また、GNSS でのイノベーションが続き、市場でさまざまなチップセット/ドライバーが登場していくにつれて進化します。 GNSS アダプターは、初期化時または必要に応じて、基になる GNSS ドライバー/デバイスのさまざまな機能を照会し、それに従って、GNSS ドライバーとの対話を最適化します。

GNSS アダプターと GNSS ドライバーとの間の機能情報交換は、 [ **\_プラットフォーム\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/gnssdriver/ni-gnssdriver-ioctl_gnss_send_platform_capability)および ioctl\_\_を送信することによって、[**デバイス\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/gnssdriver/ni-gnssdriver-ioctl_gnss_get_device_capability)の\_機能を取得するという制御コード\_使用します。

### <a name="global-navigation-satellite-system-gnss-driver-command-and-configuration"></a>グローバルナビゲーションサテライトシステム (GNSS) ドライバーのコマンドと構成

GNSS アダプターは、1回限りの構成、または GNSS ドライバーの定期的な再構成を実行する場合があります。 同様に、GNSS アダプターは、ドライバーを介して特定の GNSS 固有のコマンドを実行する場合があります。 これを実現するには、ドライバーと上位レベルのオペレーティングシステム (HLOS) の間にコマンド実行プロトコルを定義します。 特定のコマンドの種類によっては、意図した操作が直ちに有効になるか、またはシステムの再起動後に有効になることがあります。 Gnss デバイスの機能情報と同様に、GNSS のコマンドも、この GNSS インターフェイス定義の一部として、Microsoft によって適切に定義されています。さらに、今後のイノベーションと、GNSS デバイス/ドライバーの分散によって進化し続けます。

デバイスコマンドの実行と構成は、コントロールコード[**IOCTL\_GNSS\_SEND\_DRIVERCOMMAND**](https://docs.microsoft.com/windows-hardware/drivers/ddi/gnssdriver/ni-gnssdriver-ioctl_gnss_send_drivercommand)を使用して行います。

### <a name="position-information"></a>位置情報

これは、基になる GNSS デバイスの主な機能です。 最も基本的な形式では、GNSS アダプターは、GNSS ドライバーからのデバイスの現在の位置を要求します。 位置要求のバリエーションには、次の位置のセッションの種類が含まれます (ただし、これらに限定されるわけではありません)。

- デバイスの現在の位置 (単一ショット修正)

- 修正の継続的な周期的なストリーム (時間ベースの追跡)

- 移動のしきい値に基づく修正の連続ストリーム (距離ベースの追跡)

すべての GNSS ハードウェアおよび GNSS ドライバーで必要な必須の位置のセッションの種類は、セッションの種類を1回だけ修正することです。 Native (SOC で実装され、gnss デバイス、またはアプリケーションプロセッサで実行されているサービスでは実装されません)、時間ベースの追跡セッション、および距離ベースの追跡セッションが必要に応じてサポートされます。 これら2種類のネイティブ追跡セッションの主な利点は、SOC での処理をより多く実行し、必要な場合にのみ変更を報告することによって、アプリケーションプロセッサ (AP) を長時間休止状態に保つことによって電力を節約できることです。 ネイティブの距離ベースの追跡のサポートは、ネイティブの時間ベースの追跡セッションよりもインパクトが高くなります。これは、アプリケーションによって広く使用されているので、電力を節約できるためです。

GNSS ドライバーから位置情報を取得する操作は、次のアクションで構成されるステートフルな一意の修正セッションを介して行われます。

1. **セッションの修正を開始します。** GNSS アダプターは、(ポンドアプリケーションからの要求の結果として) start fix セッションを開始します。 GNSS アダプターは、要求と関連付けられている特定の要件と基本設定を設定します。また、intimates ドライバーを起動して、 [ **\_FIXSESSION\_開始**](https://docs.microsoft.com/windows-hardware/drivers/ddi/gnssdriver/ni-gnssdriver-ioctl_gnss_start_fixsession)するための制御コード IOCTL\_gnss を発行して修正プログラムを取得します。

1. **デバイスの位置の取得 (データの修正):** 修正セッションが開始されると、GNSS アダプターはコード[**IOCTL\_GNSS に発行し、\_FIXDATA\_取得**](https://docs.microsoft.com/windows-hardware/drivers/ddi/gnssdriver/ni-gnssdriver-ioctl_gnss_get_fixdata)して、ドライバーからの修正の待機を開始します。 新しい位置情報がエンジンから使用可能になると、GNSS ドライバーは、この保留中の get 修正要求に応答します。

    > [!NOTE]
    > 修正セッションの種類が (現在の修正ではなく) LKG 修正の場合、位置情報はドライバーのキャッシュから取得されます。

    GNSS アダプターでは、GNSS ドライバーが、使用可能な場合に修正データを返すために、常に非同期 i/o 要求を使用できるようにします。 修正の性質によっては、より多くの修正データが必要な場合、GNSS アダプターは別の i/o 要求 (同じ IOCTL を使用) を発行します。このシーケンスは、データが使用できなくなるか、または修正セッションが停止されるまで続行されます。

1. **修正セッションの変更:** GNSS ドライバーで同じ種類の修正セッションの多重化がサポートされていない場合、GNSS\_アダプターは、そのレベルで多重化を行うときに、その修正セッションの種類に対して[ **\_fixsession\_変更**](https://docs.microsoft.com/windows-hardware/drivers/ddi/gnssdriver/ni-gnssdriver-ioctl_gnss_modify_fixsession)します。

1. **セッションの修正の停止:** 特定の修正セッションに関連するその他の位置情報が必要であるか予想されていない場合、GNSS アダプターは、修正セッションの停止を発行します。

### <a name="native-geofencing-support"></a>ネイティブジオフェンシングのサポート

GNSS DDI は、この仕様で定義されている Ioctl のセットを使用したジオフェンスオフロードシナリオをサポートしています。 このサポートを示すために、ドライバーに特別な機能フラグが定義されています。このフラグは、GNSS スタックがネイティブでジオフェンシングをサポートしている場合にのみ設定する必要があります (つまり、アプリケーションプロセッサではなく、GNSS チップにジオフェンシングを実装します)。 ドライバーがジオフェンスをネイティブでサポートしていない場合は、フラグを設定しないでください。 HLOS は、アプリケーションプロセッサ (AP) ベースのジオフェンス追跡エンジンを既にサポートしています。このソリューションは、ネイティブソリューションの場合と同じように最適化されているわけではありませんが、十分にテストおよび最適化されているため、AP で実装されている同等のソリューションに置き換えることはできません。

> [!NOTE]
> HLOS によるジオフェンスの追跡では、アプリケーションプロセッサがジオフェンスの侵害を検出するために定期的にスリープ状態にする必要があります。これにより、フェンスが侵害されていない場合でも電源をドレインします。 したがって、この実装は最適ではないと見なされます。

また、ネイティブのジオフェンス tracking ソリューションから受信したエラー通知によって、シグナル状態が低いか、またはその他の一時的なエラーが原因で、基になるドライバーがジオフェンスを追跡できない場合、HLOS は、フェールオーバーメカニズムとして AP ベースのジオフェンス追跡を使用します。
ネイティブジオフェンシングのサポートは、ジオフェンスの追跡が SoC に完全にオフになっていて、アプリケーションプロセッサがジオフェンス関連のイベントを処理するためにのみウェイクアップされている場合にのみ役立ちます。 ハードウェアがネイティブジオフェンスの追跡をサポートしていない場合、GNSS ドライバーはドライバーレイヤーでの実装を試みることはできません。

GNSS エンジンは、ドキュメントに記載されている IHV 固有のチューニングパラメーターを公開して、電力消費とユーザーエクスペリエンスの間で適切なバランスを見つけることができるようにする必要があります。 さらに、サポートされるジオフェンスの数は、ヘッダーファイルで定義されている**最小\_ジオフェンス\_必要な**値よりも大きくする必要があります。 1つのアプリケーションには、他のアプリケーションまたは携帯電話で使用されているジオフェンスの数に関する情報がないため、アプリケーションごとに**必要な最小\_ジオフェンス\_** が定義されていることに注意してください。

ジオフェンシングオフロードのサポートには、次の要件があります。

- HLOS は、DDI を介して1つ以上のジオフェンスを作成し、ドライバーがそれらをハードウェアに送信して追跡を開始することができるものとします。

- HLOS は、以前に作成された1つ以上のジオフェンスを DDI 経由で削除でき、ドライバーはそれらをハードウェアに送信して追跡を停止します。

- 最も理想的には、GNSS ハードウェアは各ジオフェンスの最初のジオフェンス tracking 状態を理解し、この初期状態からの変更のみをレポートするために使用します。 GNSS ハードウェアがこの機能をサポートしていない場合は、ジオフェンスが作成されるたびに初期状態が HLOS に報告されます。

- GNSS ハードウェアでは、デバイスの現在の位置を電源効率の高い方法で追跡し、デバイスが入力されたとき、または追跡されたジオフェンスを終了したときに、AP をウェイクアップします。 GNSS ドライバーは、ジオフェンスアラートを HLOS に渡します。

- [サテライト信号が少ない] とその他の一時的なエラー状態の場合、GNSS エンジンは既存のジオフェンスを確実に追跡できない可能性があります。 GNSS エンジンは追跡中断を検出できる必要があり、GNSS ドライバーは追跡ステータスエラーアラートを HLOS に渡す必要があります。 HLOS は、GNSS ハードウェアがジオフェンスを再び復旧して追跡できるようになるまで、既定の AP ベースのジオフェンス追跡に切り替えます。

- GNSS エンジンが、ジオフェンスを追跡できないことを示す通知を提供する必要がある正確な条件は異なるため、実装は IHV 固有のものになります。 実装に関するガイドラインを次に示します。

  - ユーザーが移動しておらず、25メートル以内にジオフェンス境界がないという確信を持つ、GNSS エンジンが検出できる場合、GNSS エンジンは追跡エラーを送信する必要はありません。

  - ユーザーが移動しておらず、25メートル以下のジオフェンスの境界があることを確認できた場合、gnss エンジンは、1分以内に追跡エラーを送信する必要があります。

  - GNSS エンジンが、ユーザーが移動していることを検出して100メートル以内にジオフェンス境界がある場合、GNSS エンジンは1分以内に追跡エラーを送信する必要があります。

  - GNSS エンジンが、ユーザーが移動しているかどうかを判断できず、100メートル以内にジオフェンス境界がある場合、GNSS エンジンは1分以内に追跡エラーを送信する必要があります。

  - ユーザーが移動中であることが GNSS エンジンによって検出された場合、GNSS エンジンは、移動の推定速度と最も近いジオフェンスへの距離に比例して、追跡エラーを時間内に送信する必要があります。 \[でエラーを送信することをお勧めします (距離は、最も近い、フェンス、15s (m)/推定速度 (m/s))-\]です。 GNSS エンジンは、移動検出のインジケーターを使用して、追跡エラーを送信するタイミングを決定する場合があります。

  - ユーザーが移動しているかどうかを GNSS エンジンが判断できない場合、GNSS エンジンは、動きの速い速度と最も近いジオフェンスへの距離に比例して、追跡エラーを送信する必要があります。 \[距離 (m)/343 (m/s)\]内でエラーを送信することをお勧めします。

- GNSS エンジンがジオフェンス tracking 状態エラーを報告した期間中は、ジオフェンスブリーチイベントが HLOS に送信されていないことが必要です。

- HLOS では、1つのコマンドで以前に作成したすべてのジオフェンスを削除することで、ジオフェンスの追跡をリセットできます。

- 再起動またはドライバーの再起動を通じて、モバイルから送信されたジオフェンスは、GNSS のハードウェアまたはドライバーに保持されません。 HLOS は、エンドユーザーアプリケーションに代わって永続化を処理し、必要に応じてジオフェンスを作成/削除します。

ネイティブのジオフェンシングオフロードをサポートする GNSS アダプターと GNSS エンジン間のやり取りの観点から見ると、ジオフェンス tracking エラーの場合、GNSS アダプターは次のように実行します。

- GNSS ドライバーが追跡の失敗を返すと、AP ベースの追跡が使用されます。

- 現在 OS レベルで追跡されているジオフェンス内の更新 (追加/削除) も、同期されるように、引き続きドライバーにプッシュされます。これにより、GNSS エンジンは、現在 OS によってどのようなジオフェンスが追跡されているかを知ることができます。また、を使用して、新しいデータに基づいて判断することができます。

- これにより、ジオフェンス状態の変更が、管理者によって管理されるようになります。

### <a name="driver-notifications-for-assistance-and-helper-data"></a>サポートとヘルパーデータのドライバー通知

場合によっては、GNSS ドライバーは、GNSS アダプターからのサポートデータまたはヘルパーアクションが必要になることがあります。 これには、さまざまな形式の AGNSS データ (時間の挿入、ephemeris、初期の粗い位置)、ネットワークによって開始されたユーザーの飛行機の配置をサポートするためのユーザーの同意ポップアップなどが含まれます。

- Gnss のサポートデータは、gnss アダプターを使用せずに、GNSS ドライバーによって取得される可能性があります。 ただし、次のような理由から、GNSS アダプターを使用し、Microsoft ポジショニングサービスを活用することをお勧めします。

  - Microsoft の場所スタックは、データ接続の確立と、ローミングの制約、データの設定、ネットワーク非表示モードの統合などに準拠します。

  - Microsoft ポジショニングサービスは、サーバー間のバックエンド接続経由で、IHV 固有の情報を定期的に取得し、必要なすべてのデバイスに提供することができます。これにより、IHV は、フロントエンドアシスタンスサービスをデプロイするための必要があります。可用性、スケーラビリティ、および応答性の要件を満たす。

- 受信トレイアプリケーションのプライバシーに関するユーザー同意は、オペレーティングシステムによって所有されています。 そのため、ネットワークで開始された場所の要求についてユーザーに通知するための UI は、ネットワークによって開始された場所の要求に対するユーザーの同意を要求するために、Microsoft によって所有されます。 GNSS ドライバーは、ネットワークから開始された場所の要求が受信されたときに GNSS アダプターに通知し、必要に応じて、ユーザーからの応答が既定の時間まで待機してから、要求の満たすために進みます。

GNSS ドライバーは自身の上位層への要求を開始できないため、この種の操作は、gnss のアダプターが gnss ドライバーから要求を事前に探しているため、常に1つ以上の保留中の Irp を維持して、GNSS dr にすることができます。i は、このような保留中の要求に対して応答を返すことができます。 サポート/ヘルパーの日付を要求した場合、GNSS アダプターはデータを取得し (または、GNSS ドライバーに代わって特定のアクションを実行します)、その後、別の**DeviceIoControl**呼び出しによって必要な情報を gnss ドライバーに挿入します。

ドライバーからの通知は、共通のイベントモデルを通じて処理されます。 たとえば、GNSS アシスタンスの場合、GNSS アダプターは、gnss [ **\_リッスン\_AGNSS を\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/gnssdriver/ni-gnssdriver-ioctl_gnss_listen_agnss)使用して、gnss ドライバーからの AGNSS 要求を受信します。 その後、GNSS アダプターは AGNSS アシスタンスデータをフェッチし、AGNSS を挿入して、gnss ドライバーにデータをプッシュする[ **\_を挿入\_\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/gnssdriver/ni-gnssdriver-ioctl_gnss_inject_agnss)します。

この通知メカニズムは、ジオフェンスに関連するアラートデータとステータスの更新を受信するためにも使用されます。 このアダプターでは、ジオフェンスのアラートを受信するためのコントロールコード[**IOCTL\_\_リッスン\_ジオフェンス\_アラート**](https://docs.microsoft.com/windows-hardware/drivers/ddi/gnssdriver/ni-gnssdriver-ioctl_gnss_listen_geofence_alert)を使用します。また、 [**ioctl\_GNSS\_リッスン\_ジオフェンス\_trackingstatus**](https://docs.microsoft.com/windows-hardware/drivers/ddi/gnssdriver/ni-gnssdriver-ioctl_gnss_listen_geofences_trackingstatus)を使用して、ジオフェンス追跡の全体的な状態の変更を受信します。

### <a name="global-navigation-satellite-system-gnss-driver-logging"></a>グローバルナビゲーションサテライトシステム (GNSS) ドライバーのログ記録

診断を目的として、GNSS ドライバーは、以下で説明する Microsoft の規定ログ機構 (WPP) を使用して、エラーおよびその他の診断情報をログに記録する必要があります。 ドライバーでは、ETW ではなく、ログ記録の目的で WPP を使用することをお勧めします。ただし、両方のメカニズムがサポートされています。 WPP が推奨される理由の中には、ドライバーのデバッグに役立つツールがあることが挙げられます。

ドライバーは、この指定されたログ記録手法を通じて、情報を記録したり、人間が読み取れるようにしたりすることはできません。 詳細については、「 [WPP ソフトウェアのトレース](https://docs.microsoft.com/windows-hardware/drivers/devtest/wpp-software-tracing)」を参照してください。

WPP ソフトウェアトレースを使用したメッセージのログ記録は、Windows イベントログサービスの使用に似ています。 ドライバーは、メッセージ ID と書式設定されていないバイナリデータをログファイルに記録します。 その後、ポストプロセッサは、ログファイル内の情報を人間が判読できる形式に変換します。 ただし、WPP ソフトウェアのトレースでは、イベントログサービスでサポートされているものよりも高い柔軟性と柔軟性を備えたメッセージ形式がサポートされています。 たとえば、WPP ソフトウェアトレースには、IP アドレス、Guid、システム Id、タイムスタンプ、およびその他の便利なデータ型のサポートが組み込まれています。 さらに、ユーザーは、アプリケーションに関連するカスタムデータ型を追加できます。

### <a name="mobile-operator-protocol-support"></a>携帯電話会社のプロトコルサポート

さまざまなモバイルオペレーターの配置プロトコル (SUPL、UPL、CP など) をサポートするには、指定された IHV SS スタック (gnss ドライバー、GNSS デバイス/エンジン) が必要です。 そうしないと、デバイスはモバイルオペレーターからの受け入れを受けられず、デバイスをはできる場所が大幅に制限されます。

> [!NOTE]
> 特定の携帯電話会社のデバイスを出荷するには、これらのプロトコルのサポートと携帯電話の要件への準拠が必須です。 モバイルオペレータープロトコルのサポートは、プラットフォームにモバイルブロードバンド (MBB) のサポートが含まれていない場合に特に、ほとんどの非電話プラットフォームにとっては重要ではない可能性があります。

すべての実装部分は、IHV スタックで抽象化されており、Microsoft HLOS コンポーネントは次のことに依存していません。

- プロトコルの実装に関する具体的な詳細 (プロトコルのしくみ、プロトコルメッセージの解釈など) を示します。

- 実装スタックの構造 (たとえば、の実装は、GNSS デバイス/エンジンまたは GNSS ドライバー内に存在する場合もあれば、別の HLOS サービスが必要な場合)。

- プロトコルを実装するための、IHV が所有する GNSS スタック内のさまざまな部分の間の相互作用。 たとえば、GNSS ドライバーが特定の SUPL プロトコルメッセージに応答するために Wi-fi スキャンの結果を必要とする場合、プライベート IOCTL 呼び出しを使用して Wi-fi スキャンの結果をドライバーに挿入するか、または UMDF 2.0 ドライブの一部にすることで、この処理を実行できます。この相互作用を下位レベルで処理します。 Microsoft GNSS HLOS コンポーネントは、IHV GNSS stack コンポーネント間のこのような相互作用に無関係されています。

要約すると、IHV または OEM は、SUPL クライアント (およびシステムが中国に出荷される場合は UPL クライアント) を提供し、それを GNSS ドライバーとの間で統合する必要があります。 配置プラットフォームと SUPL クライアントとのすべてのやり取りは、GNSS DDI を通じて行われます。

モバイルオペレータープロトコルの実装を容易にし、プラットフォーム固有のテクノロジを使用してソフトウェア開発の負担を軽減するために、GNSS アダプターは、IHV GNSS スタックに特定の機能を提供します。 GNSS ドライバーは、HLOS コンポーネントからこのような機能を受信するための仲介役として扱われます。たとえば、GNSS アダプターは GNSS ドライバーだけを操作し、IHV GNSS スタックの他の部分では対話しません。 GNSS ドライバーの Ioctl は、GNSS ドライバーと GNSS アダプター間の機能の構文とセマンティクスを定義します。 GNSS ドライバーは、携帯電話会社のプロトコルを実装する特定の IHV コンポーネントへのルーティングを担当します。 GNSS アダプターは、広く使用されている GNSS ドライバーに次の機能を提供します。

1. **構成:** 携帯電話事業者は、OMA-URI プロトコル標準によって定められた構成メカニズムを使用して、デバイスをプロビジョニングし、構成を変更します。 たとえば、SUPL 標準では、UICC に基づいて SUPL 構成を行う必要があります。または、OMA-URI または OMA-URI で取得した SUPL OMA-URI 構成プロファイル情報を使用して実行する必要があります。

    > [!NOTE]
    > 構成目的で電話で利用できる特定の機能 (OMA-URI および OMA CP) は、Windows 10 まで他のプラットフォームでは使用できませんでした。 Windows 10 以降のすべてのプラットフォームでは、新しい GNSS DDI が使用されている限り、SUPL 構成サービスプロバイダー (CSP) を介して SUPL 構成をサポートできます。 CSP によって挿入されるプロビジョニングは、イメージ自体 (provxml または multivariant を通じて)、または OMA-URI または OMA-URI を介して携帯電話事業者から取得できます。

    Windows 10 では、構成データを解釈および抽出するために、構成サービスプロバイダー (CSP) を使用したデバイス管理という独自のテクノロジを定義しています。 Microsoft は、OMA-URI 構成を使用して、GNSS アダプターを介して構成を GNSS ドライバーにプッシュするための CSP を提供しています。

    > [!NOTE]
    > また、IHV は、電話固有のデバイス管理技術 (Csp) を使用して、モバイルオペレーターの構成仕様を使用するユーザーモードコンポーネントを作成することもできます。 ただし、これは IHV に追加の負担となるため、推奨されません。

    システムでサポートされているのは、デュアル SIM デバイスの場合を含め、1つの構成のみです。 Microsoft では、UICC と UICC の変更に基づいて、SUPL を再構成する機能を提供しています。 また、デバイスローミングの場合、HLOS はスタンドアロンモードで動作するように SUPL クライアントを再構成します。 このドキュメントでは、さまざまなモバイル操作プロトコル (SUPL 1.0 と2.0、v2UPL など) のために、このような構成データをプッシュするための Ioctl を定義します。

1. **ユーザーの同意 UI:** プライバシー要件を満たすには、ネットワークによって開始される特定の配置要求にユーザーの同意が必要です。 Ihv は、プラットフォームコンポーネントの UI の書き込みを許可されていません。 そのため、GNSS アダプターは、GNSS ドライバーに代わってユーザーの同意を得るために UI を処理します。 UI ポップアップを要求するための GNSS ドライバーの通知 Ioctl と、そのような要求に対するユーザー応答を伝えるための GNSS アダプターの Ioctl は、 [gnss Driver ioctl](https://docs.microsoft.com/windows-hardware/drivers/ddi/gnssdriver)で定義されています。

完全に機能する SUPL クライアントを実装するには、IHV スタックで、OS プラットフォームで使用できるインターフェイスまたは一般的な機能を使用する必要があります。 次に、Windows 10 で使用できる機能の一覧を示します。この一覧は、Ihv が SUPL クライアントを実装するために利用できます。

> [!NOTE]
>この機能のいずれも、location platform または GNSS DDI には含まれていませんが、ここに記載されているので、わかりやすく、GNSS ドライバーの開発者は、この機能を使用して OS から利用できる機能を理解することができます。  

![SUPL クライアントと GNSS ドライバーの相互作用](images/gnss-architecture-6.png)

- **SMS ルーター:** SMS ルーターを使用すると、SUPL クライアントは、SUPL NI 要求を保持する SIP プッシュメッセージの WAP プッシュをサブスクライブできます。

- 接続**マネージャーは、このような接続を要求するために使用する接続を構成できます。** 携帯電話の場合、専用の接続では、または単に既定のインターネット接続とは異なる接続を行う必要があります。 これを行うために、**接続マネージャー**は次の機能を提供します。

  - OEM または携帯電話事業者が、対応のために使用する接続を構成するために使用できる構成サービスプロバイダー。

  - Supl 接続の接続パラメーターを照会する SUPL クライアントの API。

  - 前の手順で取得したパラメーターを使用して、SUPL 接続を確立するための API。

- **携帯ネットワーク接続の構成:** 異なる携帯電話接続のパラメーター (たとえば、SUPL 接続のパラメーター) を構成するには、OEM または携帯電話会社が使用できる構成サービスプロバイダーがあります。 これにより、**接続マネージャー**でこの接続を使用することができます。

- **SUPL 接続の進行中に接続をアクティブ状態を維持するように要求します。** システムがコネクトスタンバイ状態のときに、SUPL クライアントが HSLP との接続を開始することが必要になる場合があります。 これは、Microsoft ベースの配置を使用するように構成されている場合、または携帯電話事業者が NI 要求を送信した場合に、GNSS デバイスがサポート情報を取得する必要があるために発生する可能性があります。 この場合、SUPL クライアントは HSLP との接続を開始し、SUPL セッションが完了するまで接続がアクティブであることを確認する必要があります。

- **モバイルブロードバンド (MBB) モジュールとの対話:** Windows 10 では、携帯電話の測定値を取得するために HLOS を通じて利用できる Api はなく、緊急電話がかけられたタイミングを知ることができます。 MBB との対話は、MBB と直接統合することによって行う必要があります (コマンドや他の独自の方法で)。

### <a name="manufacturing-testing"></a>製造テスト

Oem は、製造時に検証する手段を持っている必要があります。また、GNSS ハードウェアと GNSS スタック (GNSS ドライバーと GNSS デバイス/エンジン) が正常に動作していることをカスタマーサポートポイントで確認する必要があります。 IHV は、Oem がこのテストを実行できるようにするための独自のメカニズムを提供したり、必要に応じて、OEM が製造テストを開始して結果を取得できるように、そのインターフェイスを DDI に実装したりすることができます。

テストの中心がハードウェアの検証またはドライバーの検証に重点を置いている場合、製造テストを行うときに location framework はバイパスされます。 一般に、デバイスは特殊な "安全なオペレーティングシステムモード" になります。この場合、コンポーネントとサービスの最小セットが読み込まれます。 このモードでは、OEM はテストケースをトリガーする一連のテストアプリケーションを開始できます。 製造時の効率と速度を高めるために、さまざまなコンポーネント内のテストに対して同時実行をサポートすることを強くお勧めします。

製造テストのインターフェイスには、次の2種類のテストが含まれています。

1. **キャリア波テスト:** このテストは、外部接続/アンテナテストを検証するためのものです。 このテストでは、GNSS エンジンは、応答で、CW 信号を検索し、SNRs (ノイズ定量または航空母艦への信号) の測定値を提供する必要があります。 テストでは、10 Hz で応答を返すことが理想的です。

1. **自己テスト:** このテストは、GNSS エンジンの基本的な機能を検証するためのものです。 自己テストでは、外部の信号を挿入しなくても、エンジンの基本的な問題 (欠陥のあるハードウェア、GNSS ハードウェアの不適切な接続) を検出できる必要があります。 この検証の目的は、この低コストのテストを実行し、それを運用ラインのゲートとして使用することです。これは、デバイスがより包括的で負荷の大きいテストを行う前に行われます。 このテストでは、GNSS エンジンとドライバーは pin 接続に対して自己検証を実行し、すべてが OK であるか、またはエラーが発生したことを示す状態コードを返します。 エラーのエラーコードは、検出されたエラーを示す必要があります。 エラーコードは、IHV によって設定されます。

## <a name="io-considerations"></a>I/o に関する考慮事項

GNSS**機能は**デバイスドライバーに対する従来のファイル読み取りおよび書き込み要求にはマップされないため、この関数**は、** gnss ドライバー api では使用されません。 すべての GNSS 機能は、適切に定義された GNSS 固有のデバイス i/o 制御 (**DeviceIoControl**) 要求 (ioctl とも呼ばれます) を使用して実装されます。

すべての Ioctl は、入力データと出力データの両方について、データ転送メカニズムとしてバッファリングさ\_メソッドを使用します。 GNSS 関連のデータのサイズは比較的小さいため、余分なバッファーのコピーはシステムのパフォーマンスに影響しません。

GNSS ドライバーは、 **CreateFile**関数の**FILE\_FLAG\_OVERLAPPED**オプションを使用して開きます。 したがって、すべての Ioctl が暗黙的に非同期になります。 ただし、ほとんどの GNSS Ioctl は意味的に非同期になりますが (たとえば、IOCTL はドライバー内のアクティビティをトリガーし、結果は非同期に返されます)、一部の Ioctl は論理的には存在しないという意味で同期的に同期されます。このような Ioctl に関係する非同期アクションまたはアクティビティ。 これらのいくつかの Ioctl の同期動作は、i/o 操作が完了するまで**DeviceIoControl**呼び出しを発行した後に gnss アダプタースレッドをブロックするだけで実現されます。 そのため、すべての Ioctl の処理の一環として常に IRP を完了するのは、GNSS ドライバーの役割です。 GNSS アダプターは、同期呼び出しのコントラクトを受け入れるだけで、エラーが発生した場合や、これらのコマンドを再試行できない場合があります。 IHV ドライバーは、エラーを返す前に、ドライバー側にすべてのさえが組み込まれていることを確認する必要があります。

要求と応答の操作の場合、GNSS アダプターは常に保留中の i/o 操作を使用できるようにします。これにより、GNSS ドライバーに、以前に呼び出された操作に対する応答として送信するデータがあるときに、保留中の IRP を介して応答を送信できるようになります。

## <a name="single-shot-session"></a>ワンショットセッション

ドライバーに対するワンショット修正の start fix 要求には、精度と応答時間の値が含まれます。 GNSS エンジンでは、これらの値を使用して、アプリケーション要求の目的を理解し、インテリジェントな意思決定を行うことができます。 ドライバーが要求を受信すると、エンジンによって生成された中間の修正プログラムが返されます。 中間修正は、精度要件を満たす修正プログラムを計算する際にエンジンによって生成される修正プログラムです。 これらの中間修正の頻度は適用されず、エンジンの実装の詳細です。 GNSS アダプターは、数秒ごとに修正が行われることを想定しており、最後の中間修正とは異なるものにする必要があります。

GNSS エンジンは、現在のシグナル条件下でより適切な修正を行うことができないと判断したら、最終的な修正を返し、それ以降の計算の実行を停止する必要があります。 最終修正は、精度の要件を満たしているか、またはエンジンが現在の条件下で指定された精度を向上できないことを示しています。

GNSS アダプターは、次の2つのケースのいずれかで、ワンショットセッションの停止修正を発行します。

- ドライバーから最終的な修正プログラムを取得します。

- 要求の応答時間に達しました。 ここで、最後の中間修正プログラムがアプリケーションに送信されます。

次の図は、2つのシングルショットセッションを示しています。

![2つのセッションの仲介の修正を示す図](images/gnss-architecture-7.png)

**セッション 1:** ドライバーには、精度と応答時間のパラメーターが指定されていました。 [修正の開始] コマンドの後に、ドライバーが中間修正の送信を開始しました。 しばらくすると、より正確な修正プログラムを返すことができなかったと判断され、最後の修正が最終として示されました。 これは、応答時間の制限に達した前に発生しました。 アダプターが最後の修正プログラムをアプリケーションに送信し、[修正の停止] コマンドを発行しました。

**セッション 2:** 上記のセッション1と同じですが、この場合、エンジンは精度要件を満たすための修正を行い、中間の修正を送信し続けることができました。 セッション応答時間の制限に達すると、アダプターは、ドライバーでこのセッションを閉じる必要がある停止修正を発行しました。 最後に受信した中間の修正プログラムがアプリケーションに送信されました。

単一ショットサポートを実装するときに考慮する必要がある重要な設計側面の1つは、距離ベースの追跡セッションと時間ベースの追跡セッションの両方がサポートされていない場合、GNSS エンジンは、後の 3 ~ 5 秒間サテライトの追跡を継続するということです。停止修復コマンドを受信しています。 これは、シングルショット修正セッションを使用して、シミュレートされた距離ベースの追跡セッションまたは時間ベースの追跡セッションを実装する必要があるためです。また、GNSS エンジンがサテライトの追跡を直ちに停止した場合、ほとんどの GNSS デバイスは、ナビゲーション、実行の追跡、またはマッピングアプリケーションのニーズを満たすシミュレートされた

コンピューターがアクティブになっているときだけでなく、システムがコネクトスタンバイ状態のときに、GNSS アダプターがシングルショット修正の要求を開始する場合があります。 これは、アプリケーションプロセッサまたはその他のケースでのバックグラウンドタスク、システムサービス、ジオフェンス追跡の必要性を満たすために発生する可能性があります。 GNSS ドライバーは、これらのセッション要求を GNSS デバイスに渡し、要求を満たすか、または GNSS アダプターにエラーを提供できる必要があります。

次のシーケンス図は、スタンドアロンの GNSS 修正プログラムの取得に関連する高レベルのアクションを示しています。 これには、サポートデータの要求は含まれないことに注意してください。

![gnss アーキテクチャのシーケンス図 ](images/gnss-architecture-8.png)

シーケンスの説明は次のとおりです。

1. GNSS アダプターは、 **CreateFile** API を使用して gnss ドライバーを開きます。 WDF/KMDF/UMDF を使用すると、必要に応じて、GNSS ドライバーへのコールバックが可能になります。 返されたファイルハンドルは、後続のすべての操作に使用されます。

1. GNSS アダプターは、さまざまなプラットフォーム機能をドライバーに通知するために IOCTL を発行します。 GNSS ドライバーは、i/o 操作を完了します。

1. GNSS アダプターは、デバイスの機能を取得するために IOCTL を発行します。 GNSS ドライバーはデバイスの機能を返し、i/o 操作を完了します。

1. GNSS アダプターは、ドライバー固有の構成またはコマンドに対して Ioctl を発行します。 GNSS ドライバーは必要な操作を実行し、i/o 操作を完了します。

1. GNSS アダプターは、 [ **\_の\_fixsession\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/gnssdriver/ni-gnssdriver-ioctl_gnss_start_fixsession)、修正の型とその他の側面を指定するパラメーターと共に、IOCTL を発行します。 この IOCTL が受信されると、GNSS ドライバーは、基になるデバイスとやり取りして修正プログラムの受け取りを開始し、i/o 操作を完了します。

1. GNSS アダプターは、 [ **\_FIXDATA\_取得**](https://docs.microsoft.com/windows-hardware/drivers/ddi/gnssdriver/ni-gnssdriver-ioctl_gnss_get_fixdata)し、i/o 完了を待機する IOCTL\_を発行します。 GNSS ドライバーに使用可能な中間修正プログラムがある場合は、i/o 操作を完了することによってデータが返されます。

1. GNSS ドライバーによって、修正が必要でないことが示されるまで、手順 6. が繰り返されます (最終的な修正が行われました)。

1. GNSS アダプターは、 [ **\_FIXSESSION\_停止**](https://docs.microsoft.com/windows-hardware/drivers/ddi/gnssdriver/ni-gnssdriver-ioctl_gnss_stop_fixsession)するように IOCTL\_を発行します。 GNSS ドライバーでは、元の修正要求に関連付けられたクリーンアップ操作が必要です。

1. GNSS アダプターは、 **CloseHandle** API を使用してドライバーファイルハンドルを閉じます。

GNSS Ioctl および関連するデータ構造の詳細については、「 [gnss ドライバーリファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/gnssdriver/)」を参照してください。

## <a name="distance-based-tracking-session"></a>距離ベースの追跡セッション

距離ベースの追跡セッションは、エンドユーザーアプリケーションによって頻繁に使用されます。これは、.NET Api で使用できる唯一のセッションの種類でした。 Distance 値が0の場合は、GNSS エンジンが、可能な限り高い割合で修正プログラムを提供する必要があることを示します。

GNSS アダプターは、後で**SupportDistanceTracking**機能があることを示している場合にのみ、gnss ドライバーとの距離追跡セッションを開始します。

距離追跡セッションのドライバーに対する start fix 要求には、必要な水平方向の精度と移動のしきい値が含まれます。これは、GNSS ドライバーが位置の更新を提供する前に、システムがカバーする haversine 距離です。 GNSS エンジンでは、これらの値を使用して、アプリケーション要求の目的を理解し、場所を確認する頻度を調整するなど、インテリジェントな決定を行うことができます。

Start fix 要求がドライバーによって受信されると、最終的な修正プログラムを取得するまで、エンジンによって生成された中間の修正プログラムが返されます。 これは、セッションの最初の位置と見なされます。 その後、GNSS エンジンは、haversine 距離がほぼカバーされていることを検出するたびに、修正プログラムの提供を開始します。

GNSS エンジンがデバイスの場所を追跡できないと判断した場合 (たとえば、サテライトがこれ以上表示されない場合)、GNSS アダプターにエラーが返されます。これにより、ロケーションプラットフォームは、他のメカニズムにフォールバックしてエンドユーザーアプリケーションに更新を配置します。 GNSS アダプターは、次の時間内にエラーを提供する必要があります。

\[(距離-最後の既知の位置 (m)/推定速度 (m/s)) –5秒\] または5秒 (どちらか大きい方)。

Gnss エンジンが GNSS アダプターにエラーを提供したにもかかわらず、GNSS アダプターが追跡セッションを停止していない場合、GNSS エンジンは、追跡場所を再開できるかどうかを、電力最適化された方法で継続してチェックする必要があります。 IHV は最適化を使用して、この検出を低電力で行うことができます。 最適化に関する一般的な手法は次のとおりです。

- プログレッシブバックオフ

- デバイスの移動を再確認することを示す低コストの信号を待機しています

- 衛星信号の省電力チェック

GNSS エンジンは、エラー状態の後に最後の修正を再び提供できるようになった後、追跡が正常に再開されたことを示すために、その位置を GNSS アダプターに送信する必要があります。

GNSS アダプターは、追跡セッションを要求した1つまたは複数のアプリケーションが要求をキャンセルした場合、または新しいアプリケーションが距離ベースの追跡セッションを要求している場合に、距離ベースの追跡セッションの修正修正コマンドを発行します。 このような場合、GNSS アダプターは、異なるアクティブなセッションを多重化するために必要な新しい集計されたセッションパラメーターを計算し、これらのパラメーターを使用して GNSS ドライバーを更新します。

GNSS アダプターは、次の場合に、距離ベースの追跡セッションに対して [修復の停止] コマンドを発行します。

- 追跡セッションは、システムで使用可能な別の配置エンジンに渡されました。

- 追跡セッションを要求したアプリケーションは、要求を取り消しました。

次の図は、2つの距離ベースの追跡セッションを示しています。

![gnss ドライバーの内部追跡 ](images/gnss-architecture-9.png)

**セッション 1:** GNSS ドライバーには、追跡セッションを開始するときに、精度および移動しきい値パラメーターが指定されていました。 [修正の開始] コマンドの後、ドライバーは、最終的な修正プログラムを取得するまで、または修正プログラムの送信を開始します。これにより、このような修正が GNSS アダプターに提供され、GNSS エンジンが距離追跡プロセスを開始します。 セッションがアクティブである間、GNSS アダプターは T1 と T2 のセッションパラメーターを変更する要求を送信します。 パラメーターを変更するたびに、GNSS ドライバーによって更新プログラムが GNSS アダプターに送信され、GNSS アダプターが [修正の停止] コマンドを送信するまで、新しいパラメーターを使用した距離追跡セッションが再開されます。

**セッション 2:** セッション開始プロセスは上記のセッション1に似ていますが、指定された時点では、GNSS エンジンは位置を追跡できません。 移動の距離と推定速度に依存する時間が経過すると、GNSS ドライバーはエラーを送信します。 GNSS エンジンは、回復可能な場合には電力を低くチェックし続け、復旧すると新しい修正プログラムを送信することによって、GNSS アダプターにそのことを示します。 このセッションは、GNSS アダプターが [修正の停止] コマンドを送信するまで、必要に応じて新しい修正によって更新されます。

コンピューターがアクティブになっているときだけでなく、システムがコネクトスタンバイ状態のときでも、GNSS アダプターはアクティブな状態を維持します。 これは、アプリケーションプロセッサまたはその他のケースでのバックグラウンドタスク、システムサービス、ジオフェンス追跡の必要性を満たすために発生する可能性があります。 GNSS ドライバーは、これらのセッション要求を GNSS デバイスに渡し、要求を満たすか、または GNSS アダプターにエラーを提供できる必要があります。

## <a name="time-based-tracking-session"></a>時間ベースの追跡セッション

時間ベースの追跡セッションは、ユーザーインターフェイス (マップ、ナビゲーションアプリケーションなど) を更新するために頻繁かつ定期的な位置の更新を必要とするアプリケーションで使用できます。

GNSS アダプターは、GNSS ドライバーを使用して時間ベースの追跡セッションを開始します。これは、後で、によって機能が**サポート**されていることが示されている場合に限ります。

時間ベースの追跡セッションのドライバーに対する start fix 要求には、必要な水平方向の精度と、GNSS ドライバーが位置の更新を提供する時間間隔が含まれます。 GNSS エンジンでは、これらの値を使用して、アプリケーションの要求の目的を理解し、場所を確認する頻度を調整したり、次のように、間隔の前に数秒後にサテライトの取得を開始したりすることができます。更新プログラムを適時に配置します。

Start fix 要求がドライバーによって受信されると、最終的な修正プログラムを取得するまで、エンジンによって生成された中間の修正プログラムが返されます。 これは、セッションの最初の位置と見なされます。 その後、GNSS エンジンは、セッションパラメーターに必要な間隔で修正プログラムの提供を開始します。 GNSS エンジンが、アプリケーションで必要とされる頻度で位置情報を提供できない場合は、単に、可能な最大速度で修正プログラムを提供する必要があります。

GNSS エンジンがデバイスの場所を追跡できないと判断した場合 (たとえば、サテライトが表示されなくなった場合) は、場所のプラットフォームが他の機構にフォールバックして位置を指定できるように、GNSS アダプターにエラーを返す必要があります。エンドユーザーアプリケーションを更新します。

Gnss エンジンが GNSS アダプターにエラーを提供したにもかかわらず、GNSS アダプターが追跡セッションを停止していない場合、GNSS エンジンは、追跡場所を再開できるかどうかを、電力最適化された方法で継続してチェックする必要があります。

IHV は最適化を使用して、前のセクションで説明したように、この検出を低電力で行うことができます。 GNSS エンジンは、エラー状態の後に最後の修正を再び提供できるようになった後、追跡が正常に再開されたことを示すために、その位置を GNSS アダプターに送信する必要があります。

GNSS アダプターは、追跡セッションを要求した1つまたは複数のアプリケーションが要求をキャンセルした場合、または新しいアプリケーションが時間ベースの追跡セッションを要求している場合に、時間ベースの追跡セッションの修正修正コマンドを発行します。 このような場合、GNSS アダプターは、異なるアクティブなセッションを多重化するために必要な新しい集計されたセッションパラメーターを計算し、これらのパラメーターを使用して GNSS ドライバーを更新します。

次の場合、GNSS アダプターは、時間ベースの追跡セッションに対して [修正の停止] コマンドを発行します。

- 追跡セッションは、システムで使用可能な別の配置エンジンに渡されました。

- 追跡セッションを要求したアプリケーションは、要求を取り消しました。

次の図は、2つの時間ベースの追跡セッションを示しています。

![gnss ドライバー修正プログラムの時間ベースの追跡図](images/gnss-architecture-10.png)

**セッション 1:** 管理セッションを開始するときに、GNSS ドライバーに精度と優先間隔パラメーターが指定されました。 [修正の開始] コマンドの後、ドライバーは、最終的な修正プログラムを取得するまで、または修正プログラムの送信を開始します。この場合、このような修正が GNSS アダプターに提供され、GNSS エンジンが時間ベースの追跡プロセスを開始します。 セッションがアクティブである間、GNSS アダプターは T1 と T2 のセッションパラメーターを変更する要求を送信します。 パラメーターを変更するたびに、GNSS ドライバーは更新プログラムを GNSS アダプターに送信し、新しいパラメーターを使用して時間ベースの追跡セッションを再開します。このとき、GNSS アダプターは、[修正の停止] コマンドを送信します。

**セッション 2:** セッション開始プロセスは、上記のセッション1の手順と似ていますが、特定の時点では、GNSS エンジンは位置の追跡ができなくなります。 GNSS エンジンが、セッションパラメーターで必要とされる間隔の15秒以内に修正を提供できない場合、GNSS ドライバーはエラーを送信します。 GNSS エンジンは、回復可能な場合には電力を低くチェックし続け、復旧すると新しい修正プログラムを送信することによって、GNSS アダプターにそのことを示します。 このセッションは、GNSS アダプターが [修正の停止] コマンドを送信するまで、必要に応じて新しい修正によって更新されます。

コンピューターがアクティブになっているときだけでなく、システムがコネクトスタンバイ状態のときでも、GNSS アダプターはアクティブな状態または開始時刻に基づく追跡セッションを維持することができます。 これは、バックグラウンドタスク、システムサービス、アプリケーションプロセッサでのジオフェンスの追跡などのニーズを満たすために発生する可能性があります。 GNSS ドライバーは、これらのセッション要求を GNSS デバイスに渡し、要求を満たすか、または GNSS アダプターにエラーを提供できる必要があります。

## <a name="handle-different-types-of-fix-session-simultaneously"></a>さまざまな種類の修正セッションを同時に処理する

高度な GNSS エンジンによっては、距離ベースまたは時間ベースの追跡セッションを使用して、同時に単一ショットセッションを処理できる場合があります。 理想的には独立したセッションは相互に影響しないようにする必要がありますが、これは常に可能であるとは限りません。同時にシングルショットを作成し、時間ベースの追跡セッションを行う場合には、 このセクションでは、さまざまな種類のセッションを同時に処理するために侵害を行う必要がある場合に、の IHV 実装についていくつかのガイドラインを提供します。

このセクションでは、次の略語を使用します。

- **SS:** ワンショットセッション

- **DBT:** 距離ベースの追跡セッション

- **Tbt**: 時間ベースの追跡セッション

- **TBF:** 修正間隔

次の表は、単一ショットと時間ベースの追跡セッションを同時に処理するシナリオを示しています。

<table style="width:100%;">
<colgroup>
<col width="16%" />
<col width="16%" />
<col width="16%" />
<col width="16%" />
<col width="16%" />
<col width="16%" />
</colgroup>
<thead>
<tr class="header">
<th>ケース</th>
<th>アクティブですか?</th>
<th>TBT はアクティブですか?</th>
<th>ケースの詳細</th>
<th>修正の許容範囲</th>
<th>備考</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>ケース1</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>TBT 定期セッションの時点で進行中のセッションは、残りのタイムアウト &gt;= 間隔で開始されます</p></td>
<td><p>TBT 間隔と同じ</p></td>
<td><p>SS セッションの動作:</p>
<ul>
<li><p>中間および最終の修正は、タイムアウトまで送信されます。</p></li>
<li><p>停止後すぐにセッションが終了しました。</p></li>
</ul>
<p>TBT セッションの動作:</p>
<ul>
<li><p>中級者と最終的な修正プログラムが送信されます。</p></li>
<li><p>間隔とほぼ同様に、受信した修正プログラム。</p></li>
<li><p>停止後すぐにセッションが終了しました。</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>ケース2</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>TBT 周期セッションの時点で進行中のセッションは、残りのタイムアウト &lt; 間隔で開始されます</p></td>
<td><p>SS セッションが満たされるまで、間隔は SS タイムアウトと同じままです。</p>
<p>その後、間隔を更新して TBT 間隔と同じにすることができます。</p></td>
<td><p>SS セッションの動作:</p>
<ul>
<li><p>中間および最終の修正は、タイムアウトまで送信されます。</p></li>
<li><p>停止後すぐにセッションが終了しました。</p></li>
</ul>
<p>TBT セッションの動作:</p>
<ul>
<li><p>中間および最終の修正が送信されます</p></li>
<li><p>一定の間隔での修正が行われましたが、SS セッションの処理中により頻繁に発生する可能性があります。</p></li>
<li><p>停止後すぐにセッションが終了しました。</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>ケース3</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>SS セッションが開始されましたが、タイムアウト &gt;= 間隔で開始された TBT 定期的なセッションがあります</p></td>
<td><p>TBT 間隔と同じ</p></td>
<td><p>SS セッションの動作:</p>
<ul>
<li><p>中間および最終の修正は、タイムアウトまで送信されます。</p></li>
<li><p>停止後すぐにセッションが終了しました。</p></li>
</ul>
<p>TBT セッションの動作:</p>
<ul>
<li><p>中間および最終の修正が送信されます</p></li>
<li><p>間隔とほぼ同様に、受信した修正プログラム。</p></li>
<li><p>停止後すぐにセッションが終了しました。</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>ケース4</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>SS セッションが開始されましたが、タイムアウト &lt; 間隔で開始された TBT 定期的なセッションがあります</p></td>
<td><p>Ss セッションが満たされるまで、SS タイムアウトと同じになるように間隔を変更します。 その後、間隔を更新して TBT 間隔と同じにすることができます。</p></td>
<td><p>SS セッションの動作:</p>
<ul>
<li><p>中間および最終の修正は、タイムアウトまで送信されます。</p></li>
<li><p>停止後すぐにセッションが終了しました。</p></li>
</ul>
<p>TBT セッションの動作:</p>
<ul>
<li><p>中級者と最終的な修正プログラムが送信されます。</p></li>
<li><p>一定の間隔での修正が行われましたが、SS セッションの処理中により頻繁に発生する可能性があります。</p></li>
<li><p>停止後すぐにセッションが終了しました。</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>ケース5</p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p>更新間隔が変更されたために TBT 周期的セッションが開始されました</p></td>
<td><p>モデムを使用したセッションは、TBT 間隔と同じになるように、新しい間隔に更新されます。 必要に応じて、モデムセッションを再起動します。</p></td>
<td><p>SS セッションの動作:</p>
<ul>
<li><p>適用できません</p></li>
</ul>
<p>TBT セッションの動作:</p>
<ul>
<li><p>中級者と最終的な修正プログラムが送信されます。</p></li>
<li><p>間隔とほぼ同様に、受信した修正プログラム。</p></li>
<li><p>停止後すぐにセッションが終了しました。</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>ケース6</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>実行中の TBT 定期的なセッションが間隔の変更を受信した時点で進行中のセッション (残りのタイムアウト &gt;= 間隔)</p></td>
<td><p>TBT 間隔と同じ</p></td>
<td><p>SS セッションの動作:</p>
<ul>
<li><p>中間および最終の修正は、タイムアウトまで送信されます。</p></li>
<li><p>停止後すぐにセッションが終了しました。</p></li>
</ul>
<p>TBT セッションの動作:</p>
<ul>
<li><p>中間および最終の修正が送信されます</p></li>
<li><p>間隔とほぼ同様に、受信した修正プログラム。</p></li>
<li><p>停止後すぐにセッションが終了しました。</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>ケース7</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>実行中の TBT 定期的なセッションが間隔の変化を受けた時点で進行中のセッション (残りのタイムアウト &lt; 間隔)</p></td>
<td><p>Ss セッションが満たされるまで、SS の残りのタイムアウトと同じになるように間隔を変更します。 その後、間隔を更新して TBT 間隔と同じにすることができます。</p></td>
<td><p>SS セッションの動作:</p>
<ul>
<li><p>中間および最終の修正は、タイムアウトまで送信されます。</p></li>
<li><p>停止後すぐにセッションが終了しました。</p></li>
</ul>
<p>TBT セッションの動作:</p>
<ul>
<li><p>中間および最終の修正が送信されます</p></li>
<li><p>一定の間隔での修正が行われましたが、SS セッションの処理中により頻繁に発生する可能性があります。</p></li>
<li><p>停止後すぐにセッションが終了しました。</p></li>
</ul></td>
</tr>
</tbody>
</table>

時間ベースの追跡セッションと距離ベースの追跡セッションの両方が同時に存在する場合、GNSS エンジンの精度の追跡は、その2つのうち最も小さいものを処理するように設定できます。 次の表では、同時に単一のショットと追跡セッションがある場合に必要な精度の値が異なる場合のガイドラインについても説明します。

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th>ケース</th>
<th>SS 精度</th>
<th>DBT または TBT の精度</th>
<th>全体の GNSS エンジンの精度</th>
<th>備考</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>ケース1</p></td>
<td><p>中/低--&gt; 高</p></td>
<td><p>適用できません</p></td>
<td><p>中/低--&gt; 高</p></td>
<td><p><strong>SS セッションの動作:</strong>GNSS デバイスとのセッションが更新されるか再起動され、高精度の結果が得られます。 中級者向けの修正プログラムは、使用可能な場合に提供されます。</p></td>
</tr>
<tr class="even">
<td><p>ケース2</p></td>
<td><p>高--&gt; 中/低</p></td>
<td><p>適用できません</p></td>
<td><p>高--&gt; 中/低</p></td>
<td><p><strong>SS セッションの動作:</strong>GNSS デバイスとのセッションが更新または再起動され、中/低精度の結果を取得します。 要件を満たす修正プログラムが既に提供されている場合は、最終的な修正プログラムとして返されます。 それ以外の場合は、中間の修正プログラムが利用可能になったときに HLOS に提供されます。</p></td>
</tr>
<tr class="odd">
<td><p>ケース3</p></td>
<td><p>中/低--&gt; 高</p></td>
<td><p>[高]</p></td>
<td><p>[高]</p></td>
<td><p><strong>SS セッションの動作:</strong>DBT または TBT セッションに対して高精度のセッションが既に存在する場合、SS セッションでは、最終的な精度が得られるまで、または最終修正が取得されるまで、HLOS に対してさらに詳細な修正が提供されます。</p></td>
</tr>
<tr class="even">
<td><p>ケース4</p></td>
<td><p>高--&gt; 中/低</p></td>
<td><p>[高]</p></td>
<td><p>[高]</p></td>
<td><p><strong>SS セッションの動作:</strong>DBT または TBT セッションに対して高精度のセッションが既に存在する場合、SS セッションでは、最終的な精度が得られるまで、または最終修正が取得されるまで、HLOS に対してさらに詳細な修正が提供されます。</p></td>
</tr>
<tr class="odd">
<td><p>ケース5</p></td>
<td><p>中/低--&gt; 高</p></td>
<td><p>中/低</p></td>
<td><p>中/低--SS セッションが完了した後、&gt; 高から中/低に戻る</p></td>
<td><p><strong>SS セッションの動作:</strong>GNSS デバイスとのセッションが更新されるか再起動され、高精度の結果が得られます。 中級者向けの修正プログラムは、使用可能な場合に提供されます。</p>
<p><strong>DBT または TBT セッションの動作:</strong>このセッションでは、一時的に高精度の結果を受け取ることができます。 ただし、SS セッションが提供された後、このセッションの精度は Medium/Low に戻ります。</p></td>
</tr>
<tr class="even">
<td><p>ケース6</p></td>
<td><p>高--&gt; 中/低</p></td>
<td><p>中/低</p></td>
<td><p>高--&gt; 中/低</p></td>
<td><p><strong>SS セッションの動作:</strong>GNSS デバイスとのセッションが更新または再起動され、中/低精度の結果を取得します。 要件を満たす修正プログラムが既に提供されている場合は、最終的な修正プログラムとして返されます。 それ以外の場合は、中間の修正プログラムが利用可能になったときに HLOS に提供されます。</p></td>
</tr>
<tr class="odd">
<td><p>ケース7</p></td>
<td><p>適用できません</p></td>
<td><p>中/低--&gt; 高</p></td>
<td><p>中/低--&gt; 高</p></td>
<td><p><strong>DBT または TBT セッションの動作:</strong>GNSS デバイスとのセッションは、高精度の結果を得るために更新または再起動されます。 中級者向けの修正プログラムは、使用可能な場合に提供されます。</p></td>
</tr>
<tr class="even">
<td><p>ケース8</p></td>
<td><p>適用できません</p></td>
<td><p>高--&gt; 中/低</p></td>
<td><p>高--&gt; 中/低</p></td>
<td><p><strong>DBT または TBT セッションの動作:</strong>GNSS デバイスとのセッションが更新または再起動され、中/低精度の結果を取得します。 要件を満たす修正プログラムが既に提供されている場合は、最終的な修正プログラムとして返されます。 それ以外の場合は、中間の修正プログラムが利用可能になったときに HLOS に提供されます。</p></td>
</tr>
<tr class="odd">
<td><p>ケース9</p></td>
<td><p>[高]</p></td>
<td><p>中/低--&gt; 高</p></td>
<td><p>[高]</p></td>
<td><p><strong>DBT または TBT セッションの動作:</strong>セッションは既に精度の高い修正プログラムまたは中間の修正プログラムを取得しているため、変更はありません。</p></td>
</tr>
<tr class="even">
<td><p>ケース10</p></td>
<td><p>[高]</p></td>
<td><p>高--&gt; 中/低</p></td>
<td><p>その後、SS セッションが完了した後、高/低に変更されます。</p></td>
<td><p><strong>DBT または TBT セッションの動作:</strong>セッションは、SS セッションが完了するまで、高精度の修正または中間の修正を引き続き取得できます。 その後、中/低精度の修正に変更されます。</p></td>
</tr>
<tr class="odd">
<td><p>ケース11</p></td>
<td><p>中/低</p></td>
<td><p>中/低--&gt; 高</p></td>
<td><p>中/低--&gt; 高</p></td>
<td><p><strong>DBT または TBT セッションの動作:</strong>GNSS デバイスとのセッションは、高精度の結果を得るために更新または再起動されます。 中級者向けの修正プログラムは、使用可能な場合に提供されます。</p></td>
</tr>
<tr class="even">
<td><p>ケース12</p></td>
<td><p>中/低</p></td>
<td><p>高--&gt; 中/低</p></td>
<td><p>高--&gt; 中/低</p></td>
<td><p><strong>DBT または TBT セッションの動作:</strong>GNSS デバイスとのセッションが更新または再起動され、中/低精度の結果を取得します。 要件を満たす修正プログラムが既に提供されている場合は、最終的な修正プログラムとして返されます。 それ以外の場合は、中間の修正プログラムが利用可能になったときに HLOS に提供されます。</p></td>
</tr>
</tbody>
</table>
