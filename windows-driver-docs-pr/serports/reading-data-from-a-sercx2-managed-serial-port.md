---
title: SerCx2 で管理されるシリアル ポートからデータを読み取る
description: シリアルのコント ローラー (または UART) 受信 FIFO が通常含まれます。
ms.assetid: 36522E60-3616-4431-8C8C-3EAC4A6E4422
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ffa65fdddff4119e56a0c909444463c41f27b2fd
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580431"
---
# <a name="reading-data-from-a-sercx2-managed-serial-port"></a>SerCx2 で管理されるシリアル ポートからデータを読み取る


シリアルのコント ローラー (または UART) 受信 FIFO が通常含まれます。 この FIFO では、シリアル ポートに接続されている周辺機器のデバイスから受信したデータのバッファリング ハードウェア制御を提供します。 受信 FIFO からデータを読み取る、このデバイスの周辺機器のドライバーが読み取り送信 ([**IRP\_MJ\_読み取り**](https://msdn.microsoft.com/library/windows/hardware/ff546883)) のシリアル ポートに要求します。

シリアル ポートは、データの受信データを読み取ることができます、周辺機器のドライバーよりも高速に引き続き場合、受信 FIFO できますオーバーフローが発生します。 周辺機器のオーバーフローが原因のデータの損失を防ぐためにドライバーは通常ハードウェア フロー制御を使用するシリアル ポートを構成する必要があります。 フローの制御とシリアル コント ローラーのハードウェアは自動的に受信 FIFO がほぼいっぱいになったときにデータを送信を停止する周辺機器を通知します。 原則として、SerCx2 で管理されているシリアル ポートはハードウェア フロー制御を使用する必要があります。 詳細については、[フロー制御の詳細](#flow-control-details)を参照してください。

ただし、長い期間データの送信から周辺機器のデバイスを停止するフロー制御を使用しない必要があります。 またはデバイスが正常に動作を続行可能性があります。 たとえば、周辺機器のデバイスには、オーバーフローすることができない場合は、デバイスはの長時間のシリアル ポートに、このバッファーからデータを送信する内部データ バッファーがあります。

**このページで**

-   [非同期の読み取り要求を使用します。](#using-asynchronous-read-requests)
-   [間隔タイムアウトの詳細](#interval-time-out-details)
-   [フロー制御の詳細](#flow-control-details)

## <a name="using-asynchronous-read-requests"></a>非同期の読み取り要求を使用します。


正しくない操作とデータ損失の可能性を回避するには、シリアル コント ローラーからデータを読み取り、FIFO 迅速に受信の周辺のドライバーが担当します。 通常、データを受信すると、前に周辺機器のドライバー送信非同期読み取りの要求に応じるためのデータの将来の到着のシリアル ポートに周辺機器のデバイスからします。 これは読み取るデータが受信 FIFO から読み取り可能になるまでの SerCx2 I/O キューで保留中の要求のままです。

ほとんどのハードウェア プラットフォームで周辺のドライバーが、一度に保留中のような 1 つ以上の読み取り要求がある必要はありません。 まれなケースでドライバーが 1 つ以上の未処理の読み取り要求がある場合、データが受信されると、読み取り要求時間がかかるプロセスを完了する結果として得られるデータのバックアップ データが失われるまたはそれ以外の周辺機器を原因となる前にする必要があります。正しくないです。

周辺機器のドライバーでは、一度に保留中のような 1 つだけの読み取り要求は、この要求にデータ バッファーに必要なサイズは、周辺機器の既知の動作に大きく依存します。 たとえば、ドライバーが事前に、デバイスからデータのバイト数を知っている場合、ドライバーはこのバイト数への要求でバッファー サイズを設定します。 受信 FIFO のデータをバッファーを入力するとすぐには、読み取り要求が完了しました。 ドライバーは応答で、新しい読み取り、次のデータ ブロックを待機する要求を非同期的に送信します。

ただし、周辺機器のドライバーは周辺機器から予想されるデータの事前に量を知ることはできません。 ここでは、ドライバーは、読み取り要求を適切なサイズのデータ バッファーを設定し、周辺機器のデバイスからのデータの末尾を識別するために、間隔のタイムアウトを利用しています。 読み取りバッファーの適切なサイズを選択すると、周辺機器の動作方法について詳しい知識が必要があります。 読み取りバッファーが小さすぎる場合、ドライバーは、データの読み取りが完了する 1 つまたは複数の追加読み取り要求を送信する必要があります。

## <a name="interval-time-out-details"></a>間隔タイムアウトの詳細


読み取りのタイムアウト パラメーターを設定および書き込み要求に周辺機器のドライバーを送信する、 [ **IOCTL\_シリアル\_設定\_タイムアウト**](https://msdn.microsoft.com/library/windows/hardware/ff546772)シリアル ポートに要求します。 読み取りのタイムアウトがによって制御される、 **ReadIntervalTimeout**、 **ReadTotalTimeoutMultiplier**、および**読み出し**この要求にパラメーター値。 **ReadIntervalTimeout**受信トランザクションで 2 つの連続するバイトの間で許可される最大時間間隔を指定します。 場合**ReadTotalTimeoutMultiplier**と**読み出し**はどちらも 0、およびシリアル コント ローラーの受信、読み取り要求がシリアル ポートに送信されるときに、FIFO が空の場合この要求は期間内にありませんout (および SerCx2 I/O キューで保留中のまま) まで、ポートは、少なくとも 1 バイトの新しいデータを受信した後。 詳細については、[**シリアル\_タイムアウト**](https://msdn.microsoft.com/library/windows/hardware/hh439614)を参照してください。

チップ (SoC) 統合の回線ではシステムでシリアル ポートは、いくつかのメガビット/秒以上のピーク時の料金での周辺機器のデバイスからデータを受信できる可能性があります。 このデバイスの周辺機器のドライバーの開発者は、間隔のタイムアウト値を設定したくなるかもしれません (で指定されたとおり、 **ReadIntervalTimeout**パラメーター) を 1 ミリ秒以下が、この値は、必要な場合が多いは効果です。 間隔タイムアウトを検出するために使用されるタイマーの精度が、システム クロックの粒度によって制限されているためにです。

たとえば、システム クロックの期間は 15 (ミリ秒単位) と、ドライバーの設定、 **ReadIntervalTimeout** 1 ミリ秒、0 から 15 を超える少しミリ秒単位までの範囲の任意のバイト単位の間隔に値が、時間をトリガータイムアウトになりました。場合によっては、この設定は、周辺機器のデバイスからのデータ転送の途中で発生するタイムアウトを発生する可能性があります。 この転送の完了後にのみ、タイムアウトが発生することが確実に、ドライバーを設定できます**ReadIntervalTimeout** 15 ミリ秒よりも少し大きい値にします。 たとえば場合、 **ReadIntervalTimeout**設定されている 20 (ミリ秒単位) をバイト単位の間隔は 30 ミリ秒確実にトリガーがタイムアウトと 15 ミリ秒以内の間隔、タイムアウトは発生しません。

タイマー精度は、システム クロックに依存する方法の詳細については、[タイマー精度](https://msdn.microsoft.com/library/windows/hardware/jj602805)を参照してください。

## <a name="flow-control-details"></a>フロー制御の詳細


ベスト プラクティスとして、SerCx2 で管理されたシリアル ポートを使用して、周辺機器のドライバーは受信 FIFO のオーバーフローを防ぐためにハードウェア フロー制御を使用するこれらのポートを構成する必要があります。 保留中の読み取り要求がない場合、SerCx2 を提供しないソフトウェアは、受信 FIFO の容量を超える受信データのバッファリングします。 この FIFO のオーバーフローが許可された場合、データは失われます。

周辺機器のドライバーの送信ハードウェア フロー制御を有効にする可能性があります、 [ **IOCTL\_シリアル\_設定\_HANDFLOW** ](https://msdn.microsoft.com/library/windows/hardware/ff546736)ハンドシェイクとフロー制御を設定する要求シリアル ポートの設定です。 または、ドライバーが送信することがあります、 [ **IOCTL\_シリアル\_適用\_既定\_構成**](https://msdn.microsoft.com/library/windows/hardware/hh406621)要求のセットを使用するシリアル ポートを構成するにはハードウェア フロー制御を含む既定のハードウェアの設定。 **IOCTL\_シリアル\_設定\_HANDFLOW**使用を要求、 [**シリアル\_HANDFLOW** ](https://msdn.microsoft.com/library/windows/hardware/jj680685)構造体をフロー制御の設定について説明します。 **IOCTL\_シリアル\_適用\_既定\_構成**要求が仕入先が指定したデータ形式で同様の情報を含む可能性があります。

周辺機器のドライバーを使用している場合、 **IOCTL\_シリアル\_設定\_HANDFLOW**ハードウェア フロー制御を有効にするには、ドライバーは、次のフラグを設定する必要があります、**シリアル\_HANDFLOW**この要求で構造体。

-   シリアル\_CTS\_ハンドシェイク フラグ、 **ControlHandShake**構造体のメンバー。 このフラグにより、シリアル ポートのフロー制御を使用する受信操作。
-   シリアル\_RTS\_コントロールおよびシリアル\_RTS\_ハンドシェイクでフラグを設定、 **FlowReplace**メンバー。 これらのフラグは、シリアル ポートへのフロー制御を使用して有効にする操作を送信します。

 

 



