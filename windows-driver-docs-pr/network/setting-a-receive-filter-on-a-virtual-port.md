---
title: 仮想ポートでの受信フィルターの設定
description: 仮想ポートでの受信フィルターの設定
ms.assetid: F0137D59-1701-4DFC-BB30-27E477FC0706
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 47be2c6633368f628e4b3dbfacbdcfd336785c9d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573749"
---
# <a name="setting-a-receive-filter-on-a-virtual-port"></a>仮想ポートでの受信フィルターの設定


仮想ポート (VPort) を作成した後スイッチ、NIC のネットワーク アダプター、重なってドライバー セットを受信できる、VPort のフィルター。 作成、VPort ドライバーのみがその VPort で受信フィルターを設定できます。

このトピックには、次の情報が含まれています。

[に対して、VPort 受信フィルターを設定](#set)

[NDIS を使用して\_受信\_フィルター\_フィールド\_MAC\_ヘッダー\_VLAN\_UNTAGGED\_または\_0 フラグ](#flag)

[フィルターの識別子を使用してください。](#filter-id)

[処理の受信、VPort のフィルター](#handle)

VPort を作成する方法の詳細については、[仮想ポートを作成する](creating-a-virtual-port.md)を参照してください。

**注**  VPort の既定値は常に存在し、明示的に作成、ので上にあるドライバーが VPort の既定の受信フィルターを設定できます。 上にあるドライバーは、既定 VPort を所有していません。 そのため、ネットワーク アダプターにバインドされているすべてのプロトコル ドライバーには、既定 VPort を使用できます。 既定 VPort NDIS の識別子の値を持つ\_既定\_VPORT\_id。

 

## <a name="setting-a-receive-filter-on-a-vport"></a>に対して、VPort 受信フィルターを設定


オブジェクト識別子 (OID) メソッド要求を発行している上位のドライバーを設定し、VPort でフィルターを構成、 [OID\_受信\_フィルター\_設定\_フィルター](https://msdn.microsoft.com/library/windows/hardware/ff569795)します。 **InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造体は、初期状態へのポインターを含む、 [**NDIS\_受信\_フィルター\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff567181)構造体。

上にあるドライバーはこの OID メソッド要求を発行前に初期化する必要があります、 [ **NDIS\_受信\_フィルター\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff567181)構造体。 ドライバーは、次のようにこの構造体のメンバーを設定する必要があります。

-   **FilterType**にメンバーを設定する必要があります、 [ **NDIS\_受信\_フィルター\_型**](https://msdn.microsoft.com/library/windows/hardware/ff567186)列挙値。

    **注**  以降 NDIS 6.30 でのみ**NdisReceiveFilterTypeVMQueue**シングル ルート I/O 仮想化 (SR-IOV) インターフェイスのフィルターの種類がサポートされています。

     

-   **QueueId** NDIS にメンバーを設定する必要があります\_既定\_受信\_キュー\_id。

-   **VPortId** VPort に関連付けられている識別子にメンバーを設定する必要があります。 上にあるドライバーは、次の方法のいずれかで VPort 識別子を取得します。

    -   前の OID メソッド要求から[OID\_NIC\_スイッチ\_作成\_VPORT](https://msdn.microsoft.com/library/windows/hardware/hh451816)します。

    -   前の OID メソッド要求から[OID\_NIC\_スイッチ\_ENUM\_拡張](https://msdn.microsoft.com/library/windows/hardware/hh451821)します。

-   **FilterId** NDIS にメンバーを設定する必要があります\_既定\_受信\_フィルター\_id。

    **注**  NDIS ミニポート ドライバーの処理に OID 要求を転送する前にこのメンバーの一意のフィルター id が割り当てられます。

     

-   **FieldParametersArrayOffset**、 **FieldParametersArrayNumElements**、および**FieldParametersArrayElementSize**のメンバー、 [ **NDIS\_受信\_フィルター\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff567181)の配列を定義する構造体を適切に設定する必要があります[ **NDIS\_受信\_フィルター\_フィールド\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff567169)構造体。 各**NDIS\_受信\_フィルター\_フィールド\_パラメーター**配列内の構造は、ネットワーク ヘッダーで 1 つのフィールドのフィルターのテスト条件を設定します。

    SR-IOV のインターフェイスで、次のようなフィールド テスト パラメーターが定義されています。

    -   パケットの宛先メディア アクセス制御 (MAC) アドレスでは、指定された MAC アドレスと同じです。

    -   パケット内の仮想 LAN (VLAN) 識別子では、指定した VLAN 識別子と同じです。

OID メソッドの要求から正常に戻った後、 **InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造体ポインターが含まれています、 [ **NDIS\_受信\_フィルター\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff567181)新しいフィルターの識別子を持つ構造体。

## <a name="using-the-ndisreceivefilterfieldmacheadervlanuntaggedorzero-flag"></a>NDIS を使用して\_受信\_フィルター\_フィールド\_MAC\_ヘッダー\_VLAN\_UNTAGGED\_または\_0 フラグ


**フラグ**のメンバー、 [ **NDIS\_受信\_フィルター\_フィールド\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff567169)構造体の指定受信フィルターに対して実行するアクション。 次の点を適用する、 **NDIS\_受信\_フィルター\_フィールド\_MAC\_ヘッダー\_VLAN\_UNTAGGED\_または\_0**フラグ。

-   場合、 **NDIS\_受信\_フィルター\_フィールド\_MAC\_ヘッダー\_VLAN\_UNTAGGED\_または\_ゼロ**フラグに設定されて、**フラグ**メンバー、ネットワーク アダプターは、次のテスト条件のすべてに一致する受信パケットのみを示す必要があります。

    -   一致する MAC アドレスを持つパケットです。

    -   VLAN タグがない場合や 0 の VLAN 識別子を持つパケット。

    場合、 **NDIS\_受信\_フィルター\_フィールド\_MAC\_ヘッダー\_VLAN\_UNTAGGED\_または\_ゼロ**フラグが設定されて、ネットワーク アダプターが一致する MAC アドレスと 0 以外の場合、VLAN 識別子を持つパケットを示す必要がありますされません。

    **注**  仮想化スタックが、MAC アドレス フィルターを設定し VLAN 識別子フィルターが構成されていない場合、 [OID\_受信\_フィルター\_設定\_フィルター](https://msdn.microsoft.com/library/windows/hardware/ff569795)もセットの要求、スイッチの設定、 **NDIS\_受信\_フィルター\_フィールド\_MAC\_ヘッダー\_VLAN\_タグのない\_または\_0**フラグ。

     

-   場合は、NDIS 6.30、以降、 **NDIS\_受信\_フィルター\_フィールド\_MAC\_ヘッダー\_VLAN\_UNTAGGED\_または\_0**フラグが設定されていないとして構成されている VLAN 識別子フィルターがない、 [OID\_受信\_フィルター\_設定\_フィルター](https://msdn.microsoft.com/library/windows/hardware/ff569795)メソッド要求、ミニポート ドライバーは、次のいずれかを行う必要があります。

    -   ミニポート ドライバーでの失敗した状態を返す必要があります、 [OID\_受信\_フィルター\_設定\_フィルター](https://msdn.microsoft.com/library/windows/hardware/ff569795)メソッド要求。

    -   ミニポート ドライバーでは、MAC アドレスの指定されたフィールドをフィルター処理を検査してネットワーク アダプタを構成する必要があります。 VLAN タグの受信パケットに存在する場合、ネットワーク アダプターする必要がありますから削除パケット データ。 ミニポート ドライバーに VLAN タグを配置する必要があります、 [ **NDIS\_NET\_バッファー\_一覧\_8021Q\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff566565)関連付けられている、パケットの[ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)構造体。

-   プロトコル ドライバーは、MAC アドレス フィルターと VLAN 識別子フィルターを設定する場合、 [OID\_受信\_フィルター\_設定\_フィルター](https://msdn.microsoft.com/library/windows/hardware/ff569795)メソッドが要求、は設定しません**NDIS\_受信\_フィルター\_フィールド\_MAC\_ヘッダー\_VLAN\_UNTAGGED\_または\_0**フィルター フィールドのいずれかのフラグを設定します。 この場合、ミニポート ドライバーでは、指定された MAC アドレスと VLAN 識別子の両方に一致するパケットを示す必要があります。 ミニポート ドライバーでは、0 の VLAN 識別子またはタグなしのパケットは MAC アドレスを一致するパケットが示されませんする必要があります。

## <a name="using-the-filter-identifier"></a>フィルターの識別子を使用してください。


NDIS フィルター識別子を割り当てます、 **FilterId**のメンバー、 [ **NDIS\_受信\_フィルター\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff567181)構造体し、の OID メソッド要求を渡します[OID\_受信\_フィルター\_設定\_フィルター](https://msdn.microsoft.com/library/windows/hardware/ff569795)基になるミニポート ドライバーにします。 VPort が設定されている各フィルターには、ネットワーク アダプターのフィルターの一意な識別子があります。 つまり、フィルターの識別子は、ネットワーク アダプターを管理する別のキューでは複製されません。

上にあるドライバーは、フィルターを使用する必要があります以降 OID で NDIS を提供する識別子要求のフィルター パラメーターを変更するか、フィルターを解放します。

NDIS、VPort に対してフィルターを設定する OID 要求を受け取ると、フィルター パラメーターを確認します。 NDIS は、必要なリソースとフィルターの識別子を割り当て後、は、基になるネットワーク アダプターに OID 要求を送信します。 OID を使用して要求が完了する場合は、ネットワーク アダプターは、フィルター、必要なソフトウェアとハードウェア リソースを割り当てることができますが正常に、 **NDIS\_状態\_成功**します。

ミニポート ドライバーでは、割り当てられた受信のフィルターのフィルターの識別子を保持する必要があります。 NDIS は、以降の OID 要求と受信フィルター パラメーターを変更または受信のフィルターをクリアするフィルターのフィルターの識別子を使用します。 パラメーターを変更し、フィルターをクリアする方法の詳細については、[VM キュー パラメーターの更新の取得と](obtaining-and-updating-vm-queue-parameters.md)と[VMQ フィルターをクリア](clearing-a-vmq-filter.md)を参照してください。

## <a name="handling-receive-filters-on-a-vport"></a>処理の受信、VPort のフィルター


ミニポート ドライバーでは、次のように、フィルターに基づくネットワーク アダプターをプログラムします。

-   特定のフィルターのすべてのフィールド テスト パラメーターは、VPort にパケットを割り当てると一致する必要があります。

-   複数のフィルターは、VPort で設定できます。

-   フィルターのいずれかを渡す場合、パケットを VPort に割り当てられる必要があります。

ネットワーク アダプターが論理フィールドのすべてのテストの結果をまとめて**AND**操作。 任意のフィールドをテストする場合は、配列に含まれる、 [ **NDIS\_受信\_フィルター\_フィールド\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff567169)失敗した場合、構造体、ネットワーク パケットが、指定したフィルター条件を満たしていません。

ネットワーク アダプターでは、これらのフィルター条件に対して受信したパケットをテストは、パケットに指定されたテスト条件を持たないすべてのフィールドを無視する必要があります。

 

 




