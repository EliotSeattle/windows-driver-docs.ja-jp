---
title: デバイスの低電力状態
description: デバイスの低電力状態
ms.assetid: f594a63f-10ce-439d-abe3-d342555d98f0
keywords:
- デバイスの電源状態の WDK カーネル
- 低電力状態 WDK でデバイスの電源管理
- スリープの電源管理の WDK カーネル
- Dx 名 WDK の電源管理
- WDK のスリープ状態のデバイスの電源管理
- デバイスの最下位の電源状態の WDK カーネル
- highest-powered デバイス低電力状態の WDK カーネル
- 中間のスリープ状態 WDK カーネル
- 省電力モードの WDK カーネル
- 省電力モード WDK カーネル
- 継続的な電源 WDK カーネル
- WDK の遅延の電源管理
- 状態遷移の遅延の WDK 電源管理
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: d6bb4590a1fa97a27dc4ea9bb834bc793e31f0b1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573440"
---
# <a name="device-low-power-states"></a>デバイスの低電力状態





デバイスの電源状態 D1、d2 に切り替わり、および D3 は、デバイスの低電力状態です。 Windows 8 以降、D3 が 2 つの下位に分割[D3hot](#d3hot)と[D3cold](#d3cold)します。

D1 と D2 は、中間の省電力状態です。 デバイスの多くのクラスは、これらの状態を定義してください。 すべてのデバイスでは、D3hot を定義する必要があります。

次のセクションでは、D1、d2 に切り替わり、および D3 について説明します。

-   [デバイスの電源状態 D1](#d1)
-   [デバイスの電源状態 D2](#d2)
-   [デバイスの電源状態 D3](#d3)

### <a href="" id="d1"></a>デバイスの電源状態 D1

デバイス D1 の電源状態は、highest-powered デバイス低電力状態です。 次の特性があります。

<a href="" id="power-consumption"></a>*電力消費量*  
使用量は、値を D2 状態でに等しいかそれよりも多くの状態、D0 でより小さくなります。 多くの場合、D1 は、デバイスがデバイスのハードウェアのコンテキストを保持するために十分な能力だけを受信する時計ゲートの状態です。 通常、バスまたはデバイス D1 をサポートするクラスの仕様では、さらに詳しくは、この状態について説明します。

<a href="" id="device-context"></a>*デバイス コンテキスト*  
一般に、デバイス コンテキストでは、ハードウェアが保持され、ドライバーでは復元されません必要があります。 通常 D1 をサポートするバスまたはデバイス クラスの仕様では、このコンテキストを保持する機能の詳細な要件を提供します。

<a href="" id="device-driver-behavior"></a>*デバイス ドライバーの動作*  
ドライバーでは、保存、復元、またはハードウェアによって失われた任意のコンテキストを再初期化する必要があります。 通常、ただし、デバイス コンテキストが失われるほとんどこの状態を入力するとします。

<a href="" id="restore-time"></a>*復元時間*  
一般に、D1 から D0 にデバイスを復元するために必要な時間では、D0 へ D2 からの復元より小さくする必要があります。

<a href="" id="wake-up-capability"></a>*ウェイク アップ機能*  
D1 内のデバイスは、ウェイク アップを要求できる可能性があります。 この状態がウェイク信号をサポートするかどうかに関する情報を指定するバス ドライバーを使用して、 [**デバイス\_機能**](https://msdn.microsoft.com/library/windows/hardware/ff543095)構造体、または Windows 8 では、以降では、 [GUID\_D3COLD\_サポート\_インターフェイス](https://msdn.microsoft.com/library/windows/hardware/hh967714)ドライバー インターフェイス。

通常、D1 を使用するデバイスはこの状態から再開すると、デバイスの完全なハードウェアのコンテキストを復元するドライバーが必要ないためです。 ユーザーの認識の遅延を最小限に抑えるには、デバイスを復元する D0 D1 から可能な限り最小限の遅延が発生する必要があります。 状態遷移の遅延を最小限に抑えることは、電力消費量を減らすことよりも重要です。

### <a href="" id="d2"></a>デバイスの電源状態 D2

D2 は、次の特性を持つ中間デバイス低電力の状態を示します。

<a href="" id="power-consumption"></a>*電力消費量*  
消費量が D1 状態と等しいかそれよりもです。

<a href="" id="device-context"></a>*デバイス コンテキスト*  
一般に、ほとんどのデバイス コンテキストは、ハードウェアが失われます。 多くの場合、この状態は、ウェイク イベントを通知するために使用されるコンテキストの一部を保持します。 通常 D2 をサポートするバスまたはデバイス クラスの仕様では、このコンテキストを保持する機能の詳細な要件を提供します。

<a href="" id="device-driver-behavior"></a>*デバイス ドライバーの動作*  
デバイス ドライバーは、保存し復元やハードウェアによって失われた任意のコンテキストを再初期化する必要があります。 一般的なデバイスでは、D2 が入ると、ほとんどのコンテキストが失われます。

<a href="" id="restore-time"></a>*復元時間*  
少なくとも D1 から D0 にデバイスを復元すると同程度に時間がかかり D2 から D0 にデバイスを復元します。 大規模なフレーム バッファーをグラフィックス アダプターでは、大量の D2 から D0 への移行後に復元するハードウェアのコンテキストがあるデバイスの例を示します。 このようなデバイスは、D2 からの復元時は D1 から、復元時間よりもはるかにあります。

<a href="" id="wake-up-capability"></a>*ウェイク アップ機能*  
D2 内のデバイスは、ウェイク アップを要求できる可能性があります。 この状態がウェイク信号をサポートするかどうかに関する情報を指定するバス ドライバーを使用して、 [**デバイス\_機能**](https://msdn.microsoft.com/library/windows/hardware/ff543095)構造体、または Windows 8 では、以降では、 [GUID\_D3COLD\_サポート\_インターフェイス](https://msdn.microsoft.com/library/windows/hardware/hh967714)ドライバー インターフェイス。

通常、D2 をサポートするドライバーは自分のデバイスは、D3 からのスリープ解除をサポートできないので。 これらのデバイス D2 状態の電力消費量はウェイク信号への応答で元のデバイスが回復できる最も低いレベルを削除します。 ユーザーによって認識される遅延を減らしますが実装されている D1 の状態とは対照的 D2 の状態を実装する目的は、電源を節約するためにです。 その結果、D0 D2 からの復元時間通常を超えています D1 から D0 にします。 D2 の状態などバス上の制限の power 可能性が、デバイスを再起動し、デバイスを復元するまでに時間必要になるため、その機能の一部を無効にします。

デバイスの多くのクラスでは、この状態は定義しません。

### <a href="" id="d3"></a>デバイスの電源状態 D3

D3 は、デバイスの電源が最も低い低電力状態です。 すべてのデバイスでは、この状態をサポートする必要があります。

オペレーティング システム以降 Windows 8 では、2 つ異なる下位、D3hot と D3cold に D3 に細分化します。 Windows の以前のバージョンが D3 の状態が D3hot できませんを定義し、D3cold substates します。 ただし、すべてのバージョンの[PCI バス Power Management Interface Specification](http://www.pcisig.com/specifications/conventional/)個別 D3hot と D3cold の下位と 4 以降のバージョンを定義、 [Advanced Configuration and Power Interface Specification](https://go.microsoft.com/fwlink/p/?linkid=57185) D3hot を定義し、D3cold substates します。

Windows 8 の前に Windows のバージョンは D3 の D3hot と D3cold 下位を明示的に定義しても、これらの下位は以前のバージョンの Windows で暗黙的に存在しません。 デバイスは暗黙的に D3hot 下位状態場合は、デバイスが明示的に D3 の状態であり、コンピューターが S0 システム電源の状態。 累乗に D3hot でデバイスが接続されている (ただし、現在の低を描画するためには、デバイスを構成する場合があります)、ソースおよびバス上のデバイスの存在を検出できます。 D3 の状態が明示的にあり、コンピューターが省電力 Sx 状態 (S0 以外の状態) の場合、デバイスは下位 D3cold 状態で暗黙的にです。 この暗黙的な D3cold 下位状態でそのデバイスは現在、トリクルを受け取る可能性があります、デバイスとコンピューターが効果的に無効になっていますウェイク イベントが発生するまで。

Windows 8 以降、デバイスは入力し、コンピューターの S0 状態のまま D3cold 下位状態のままにします。 この新しい動作をサポートするには、D3hot と D3cold する必要があります明示的に定義する D3 の個別の下位として。

D3hot は、唯一の下位状態の D3 D0 から直接入力できるデバイスです。 デバイスを遷移 D0 から D3hot ソフトウェア管理下にあるデバイス ドライバー。 D3hot では、バスに接続されているデバイスを検出できます。 バスは、中、デバイスは下位 D3hot 状態 D0 状態で維持する必要があります。 D3hot から、デバイス D0 に戻るか D3cold を入力します。 D3cold は、D3hot からのみ入力できます。

D3cold は、下位状態の D3、デバイスがバスに物理的に接続されているが、(これは、デバイスがもう一度オン) まで、バス上のデバイスの存在を検出することはできません。 D3cold で、次のいずれかが true:

-   バスに接続するデバイスは、低電力状態です。
-   デバイスをバス ドライバー、バス上の存在を検出しようとするときに、デバイスが応答しない低電力状態にあります。

D3hot から D3cold への移行は、デバイス ドライバーの操作なしに発生します。 代わりに、デバイス ドライバーは、それが D0 から D3hot への移行を開始する前に D3cold 遷移の準備がかどうかを示します。 その後、D3hot から D3cold への移行は、ことはできません、すべての条件がこの移行を有効にする適切なかどうかによって異なります。

このような 2 つの条件ではすべて同じ電源を使用するデバイスの D3hot に D3cold に移行するために準備されます。 これらのデバイスの最後には、D3hot が入ると、親バス ドライバーまたはフィルター ドライバーの ACPI オフにこれらのデバイスを電源とデバイスが D3cold を入力することはします。

D3cold 内にあるデバイスのままに substate D0 を入力することによってのみです。 D3cold から D3hot への直接の移行はありません。

コンピューターが S0 状態として、デバイス入力 D3hot 下位状態、デバイス ドライバーは、デバイスの次の移行を D3cold または D0 されるかどうかを事前に確認する通常できません。 1 つの例外は、S0 状態のままにするコンピューターを準備する場合です。 この場合、次の移行では D3cold です。

次のセクションでは、D3hot と D3cold について説明します。

-   [D3hot 下位状態](#d3hot)
-   [D3cold 下位状態](#d3cold)

詳細については、[ドライバーではサポートしている D3cold](supporting-d3cold-in-a-driver.md)を参照してください。

### <a href="" id="d3hot"></a>D3hot 下位状態

D3hot には、次の特徴があります。

<a href="" id="power-consumption"></a>*電力消費量*  
全体としては、電源はコンピューターからではなく、デバイスからは削除してほとんどの場合。 S0 状態であると、コンピューターは、この状態で実行を続ける可能性があります。 または低電力状態に Sx S0 を移動する準備する可能性があります。

<a href="" id="device-context"></a>*デバイス コンテキスト*  
デバイス ドライバーは、デバイス コンテキストを復元する責任を負うものです。 ドライバーを保持する必要がありますすべてのデバイス コンテキストを復元するか、D0 状態への遷移時にデバイスを再初期化する必要があります。

<a href="" id="device-driver-behavior"></a>*デバイス ドライバーの動作*  
デバイス ドライバーが最新の作業中の構成から通常デバイス コンテキストを復元する責任を負うものです。

<a href="" id="restore-time"></a>*復元時間*  
合計復元時間は D3cold、以外の電源の状態は、デバイスのいずれかの最大値が、通常は D2 からの復元時刻よりも大きくありません。

<a href="" id="wake-up-capability"></a>*ウェイク アップ機能*  
下位 D3hot 状態内のデバイスでは、可能性があります。 またはできないウェイク アップを要求することがあります。 バス ドライバーを使用してこの下位状態がウェイク信号をサポートするかどうかに関する情報を指定する、 [**デバイス\_機能**](https://msdn.microsoft.com/library/windows/hardware/ff543095)構造体、または Windows 8 では、以降では、 [GUID\_D3COLD\_サポート\_インターフェイス](https://msdn.microsoft.com/library/windows/hardware/hh967714)ドライバー インターフェイス。

D3hot、最小限のトリクル現在は使用できます。 電源の有無は、ドライバーとハードウェアを準備する必要があります。 通常 D3hot をサポートするバスの仕様では、この状態で使用できる電源の詳細な要件を提供します。 デバイスを動作状態に戻ります、デバイスのドライバーを復元し、オプションでは、デバイスで利用できる可能性がある ROM コードが実行している BIOS によってことがなく、デバイスを再初期化する必要がありますできます。

親のバス ドライバーでは、システム電源 D3hot が入力した場合を除き、任意のデバイスの親バスから削除されません S0 状態に全体の遷移とコンピューター。

デバイスのすべてのクラスは、下位 D3hot 状態を定義します。

### <a href="" id="d3cold"></a>D3cold 下位状態

D3cold には、次の特徴があります。

<a href="" id="power-consumption"></a>*電力消費量*  
電源が完全に削除されました、デバイスおよびシステム全体から可能性があります。 デバイスは、その構造に応じて、側アウトオブ バンドのソースから現在を描画することができます。

<a href="" id="device-context"></a>*デバイス コンテキスト*  
デバイス ドライバーは、デバイス コンテキストを復元する責任を負うものです。 ドライバーが保持し、デバイス コンテキストを復元する必要がありますか、D0 状態への遷移時にデバイスを再初期化する必要があります。

<a href="" id="device-driver-behavior"></a>*デバイス ドライバーの動作*  
デバイス ドライバーが最新の作業中の構成から通常デバイス コンテキストを復元する責任を負うものです。

<a href="" id="restore-time"></a>*復元時間*  
合計復元時間は、デバイスの電源状態のいずれかの最大値。

<a href="" id="wake-up-capability"></a>*ウェイク アップ機能*  
D3cold 下位状態で、デバイスは休止中のコンピューターをウェイクするためウェイク信号をトリガーすることにあります。 この機能が報告される、 [**デバイス\_機能**](https://msdn.microsoft.com/library/windows/hardware/ff543095)構造体し、によって、Windows 8 以降、 [ *GetIdleWakeInfo*](https://msdn.microsoft.com/library/windows/hardware/hh967712)で日常的な[GUID\_D3COLD\_サポート\_インターフェイス](https://msdn.microsoft.com/library/windows/hardware/hh967714)ドライバー インターフェイス。 シグナルは、コンピューターを起動した後、デバイス ドライバーは D3cold から D0 へのデバイスの移行を開始します。 詳細については、次の「解説」を参照してください。

Windows 8 以降、D3cold 下位状態内のデバイスは S0 システム電源の状態にあるコンピューターにウェイク信号をトリガーすることがあります。 この機能がによって報告された、 *GetIdleWakeInfo*ルーチン。 **デバイス\_機能**構造では、この機能の詳細についての情報は含まれません。 ウェイク信号が到着すると、デバイス ドライバーは D3cold から D0 へのデバイスの移行を開始します。 この場合は、信号が到着すると、デバイスのみをスリープ解除する必要がある場合は、コンピューターが起動します。

多くの既存のハードウェア プラットフォームで低電力 Dx の状態にあるデバイスがスリープ状態のコンピューターをウェイクするためウェイク信号をトリガーできます。 ただし、同じデバイスでは S0 状態で、コンピューターが実行されている場合、ウェイク信号をトリガーできません可能性があります。 したがって、コンピューターが S0 状態の場合、このデバイスのドライバーは D0 から低電力 Dx 状態へのデバイスの移行を開始できません必要があります。 それ以外の場合、デバイスが D0 を離れた後ことはできなくなりますコンピューター S0 状態のままになるまでです。 このデバイスでは、S0 状態のままにするコンピューターを準備する場合にのみ、D0 状態のままにしてください。

低電力 Dx の状態にあるデバイスは、S0 状態で実行されているコンピューターにウェイク信号をトリガーできる場合、デバイスは、コンピューターが S0、D0 で維持する必要はありません。 コンピューターが S0 でデバイス D0 では、アイドル状態されているが、ドライバーはウェイク信号をトリガーするデバイスを arm し、D0 からこの低電力 Dx 状態へのデバイスの移行を開始できます。

デバイスの一部のクラスは、下位 D3cold 状態を定義します。

詳細については、[ドライバーではサポートしている D3cold](supporting-d3cold-in-a-driver.md)を参照してください。

 

 



