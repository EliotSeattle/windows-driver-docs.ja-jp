---
title: OID_WDI_SET_NETWORK_LIST_OFFLOAD
description: OID_WDI_SET_NETWORK_LIST_OFFLOAD Ap をスキャンする、ファームウェアの Ssid を優先の一覧を設定します。
ms.assetid: 2df9ee2b-78df-4f92-9b40-5945ecc81c7e
ms.date: 07/18/2017
keywords:
- OID_WDI_SET_NETWORK_LIST_OFFLOAD ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 7f2822b15577706b69f0fcc59ebedd567b4a716d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67359196"
---
# <a name="oidwdisetnetworklistoffload"></a>OID\_WDI\_設定\_ネットワーク\_一覧\_オフロード


OID\_WDI\_設定\_ネットワーク\_一覧\_オフロード Ap をスキャンする、ファームウェアの Ssid を優先の一覧を設定します。

| Scope        | タスクでシリアル化された設定します。 | 通常の実行時間 (秒) |
|--------------|--------------------------|---------------------------------|
| プライマリ ポート | 〇                      | 1                               |

 

ネットワーク一覧のオフロード (NLO) の 2 種類があります。 1 つの型は、常に 常に Connected (AOAC) システムでの Nic にオフロードします。 もう 1 つは、Windows 8 および Windows 8.1、のみで使用されている非 AOAC システム休止状態から再開で Wi-fi を迅速に再接続する接続のインスタント NLO します。 インスタント connect では、システムが休止状態に移行する前に、リストは送信されます。 今後は、サポートされている AOAC システムで休止状態から再開の使用でインスタント接続されます。

## <a name="instant-connect"></a>インスタント接続します。


WDI はインスタント接続 NLO を処理し、対象を絞ったスキャンの組み合わせが、OS からの要求を満たすために使用します。 IHV ドライバーは、この接続のインスタント OS 要求を処理する必要はありません。

休止状態から再開すると、OS、OS は、インスタント接続 NLO を送信します。 WDI は、OID をスキャンする対象のすべてのチャネル ヒントの和集合です。 IHV ドライバーに定義されている対象となるスキャンをサポートする必要があります[OID\_WDI\_タスク\_スキャン](oid-wdi-task-scan.md)します。 次のセクションでは、ネットワークの一覧が AOAC システムに対応した Nic にオフロードに適用されます。

## <a name="network-list-offload"></a>ネットワークの一覧のオフロード


OS は定期的なバック グラウンドが CS にスキャンを要求しません。 NLO スキャンは、ユーザーが表示されているすべての Ap を見る必要がないときに、画面がオフであるため CS で推奨される方法です。 ユーザーが Ssid の自動接続プロファイルに自動接続設定 ap がのみ役に立ちます。 OS から負荷を軽減する Ssid の一覧には、推奨される認証と暗号とペアにして、最大 4 つのチャネルのヒント。 リストの少なくとも 1 つの SSID がファームウェアは NLO スキャンを自律的に、実行を開始する必要があります高速スキャンと低速スキャン フェーズのスケジュールに従ったします。 WDI 準拠のドライバーでは、ファームウェアの要求にオペレーティング システムの要求を変換します。 Ap のスケジュールに従って NLO スキャンを実行するには、ファームウェアが必要です。 Ap は、推奨される認証をサポートし、暗号ペア Ssid に関連付けられている必要があります。

ファームウェアへの要求では、Ssid をオフロードのすべてのチャネルのヒントの一覧があります。 WDI に準拠したドライバーは、ファームウェアのこれらを結合します。 たとえば場合、SSID1\[auth1 の場合、cipher1\] 1、6、および SSID2 のチャネルのヒントが\[auth2、cipher2\] 6 および 11 のチャネルのヒント、Ssid のファームウェアを要求に示します {SSID1\[cipher1 auth1 の場合\]、SSID2\[auth2、cipher2\] } と {1, 6, 11} をスキャンするチャネルのリスト。

各スキャンの期間中、チャネルの一覧に制約は必要ありませんが、チャネルのリストの条件に一致する Ssid のファームウェアをスキャンします。 検出された AP 情報は、取得するホスト キャッシュする必要があります。 ファームウェアは、SSID、アルゴリズム、および暗号を少なくとも 1 つ BSSID が一致するが、一致するチャネルが必要でないときに、NLO 検出を示します。

各 OID\_WDI\_設定\_ネットワーク\_一覧\_LE、UE 送信オフロードが新しい NLO スキャン要求を表します。 以前、このような要求または状態を更新します。 LE は NLO なスキャンされ、要求ごとに見つかった AP の 1 回のみを示します。 UE replumbs (12 回ですこれは変更される) では、Dx NLO 遷移見つかった AP が正常に接続されていない場合 (などの理由: AP が見つかりましたが、デバイスが移動、アジア太平洋の信号フェードし、接続は失敗します。 または、EAP 認証の失敗を長引かせる。途中まで)。 LE およびファームウェアには、遅延の構成に基づいて NLO スキャンのスケジュールを遅らせる必要があります[ **WDI\_TLV\_ネットワーク\_一覧\_オフロード\_CONFIG**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-network-list-offload-config). これは、オペレーティング システムの元の NLO コマンドのスケジュールに準拠するように、UE を使用する番号です。

NLO の既定のスキャンの種類が WDI\_スキャン\_型\_自動。 チャネルを積極的にスキャンするには、ファームウェアがワイルドカードの SSID を使用する必要があります。 表示されているアクセス ポイントは、一致するものを決定するオフロード リストに Ssid と比較する必要があります。 これは、プライバシーに関するリスクを軽減します。

NLO を示す探索は、2 つのケースです。

1.  D2 の NIC がある場合は、次の手順を実行にする必要があります。
    -   ウェイク割り込みをトリガーし、セットの電力 D0 を次の手順に進む前に待機します。
    -   ファームウェアが NLO 検出の理由でスタックを再開したことを示します。
    -   戻り値の D0 コマンド。
    -   すべての見つかった AP 情報 NLO 検出を指定します。

2.  D0 で NIC がある場合は、次の手順に行う必要があります。
    -   すべての見つかった AP 情報 NLO 検出を指定します。

## <a name="set-property-parameters"></a>プロパティ パラメーターの設定


| TLV                                                                                                  | 許可されている複数の TLV インスタンス | 省略可能 | 説明         |
|------------------------------------------------------------------------------------------------------|--------------------------------|----------|---------------------|
| [**WDI\_TLV\_ネットワーク\_一覧\_オフロード\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-network-list-offload-parameters) |                                |          | NLO パラメーター。 |

 

## <a name="set-property-results"></a>セットのプロパティの結果


追加データがありません。 ヘッダー内のデータで十分です。

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>サポートされている最小のクライアント</p></td>
<td><p>Windows 10</p></td>
</tr>
<tr class="even">
<td><p>サポートされている最小のサーバー</p></td>
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>Header</p></td>
<td>Dot11wdi.h</td>
</tr>
</tbody>
</table>

 

 




