---
title: 省略可能なコマンド
description: 省略可能なコマンド
ms.assetid: b9c411b1-0061-468a-b900-47c6062aa3b0
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: d879fbc47d03a6beac72c49f204c4cf702a02481
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536959"
---
# <a name="optional-commands"></a>省略可能なコマンド


## <span id="ddk_optional_commands_si"></span><span id="DDK_OPTIONAL_COMMANDS_SI"></span>


次のコマンドは、microdriver によって実装されることができますが、これを行うには必要ありません。

<span id="CMD_GETSUPPORTEDFILEFORMATS"></span><span id="cmd_getsupportedfileformats"></span>CMD\_GETSUPPORTEDFILEFORMATS  
追加のファイル形式の数を取得する WIA ベッド ドライバーによって呼び出されます。 渡された 2 つのメンバー [ **VAL** ](https://msdn.microsoft.com/library/windows/hardware/ff548627)構造体を入力する必要があります: **lVal**追加のファイル形式の数に設定する必要があります**pGuid**イメージ形式の Guid の配列を指す必要があります。 この配列に割り当てられたメモリは、microdriver によって所有されており、によってのみ解放する必要があります。

イメージ形式は、「 *wiadef.h*またはカスタムの書式として定義できます。 BMP (ファイル) と MEMORYBMP (メモリ) の形式は、必要な形式で、WIA ベッド ドライバー自動的に追加するために注意します。 Microdriver、その拡張リストに追加しない必要があります。

このコマンドは、デバイスは、余分なファイル形式をサポートできる場合を除き、省略可能です。

<span id="CMD_GETSUPPORTEDMEMORYFORMATS"></span><span id="cmd_getsupportedmemoryformats"></span>CMD\_GETSUPPORTEDMEMORYFORMATS  
追加のメモリの形式の数を取得する WIA ベッド ドライバーによって呼び出されます。 渡された 2 つのメンバー [ **VAL** ](https://msdn.microsoft.com/library/windows/hardware/ff548627)構造体を入力する必要があります: **lVal**追加のメモリ別の形式の数に設定する必要があります**pGuid**イメージ形式の Guid の配列を指す必要があります。 この配列に割り当てられたメモリは、microdriver によって所有されており、によってのみ解放する必要があります。

イメージ形式は、「 *wiadef.h*またはカスタムの書式として定義できます。 BMP (ファイル) と MEMORYBMP (メモリ) の形式は、必要な形式で、WIA ベッド ドライバー自動的に追加するために注意します。 Microdriver、その拡張リストに追加しない必要があります。

このコマンドは、デバイスは、余分なメモリの形式をサポートできる場合を除き、省略可能です。

<span id="CMD_SETFORMAT"></span><span id="cmd_setformat"></span>CMD\_SETFORMAT  
クラスのドライバーでは、アプリケーションによって要求されるとおり、現在の形式を設定するには、このコマンドを送信します。 **PGuid**のメンバー、 [ **VAL** ](https://msdn.microsoft.com/library/windows/hardware/ff548627)構造には、イメージ形式 GUID にはが含まれています。 Microdriver は、現在のイメージ形式の設定を追跡するために、その秘密のコンテキストでこのイメージ形式の ID を保存する必要があります。

Microdrivers 拡張形式をレポートする場合にのみ、このコマンドをサポートする必要があります。 クラスのドライバーでは、拡張の形式でデータを検証することはできません、ため、適切なデータを生成する microdriver の責任になります。 拡張の形式でデータを転送するときにすべてのデータ転送してください、イメージのヘッダーを含みます。 たとえばには、ドライバーが報告された場合、JPEG 形式をサポートしている jpeg ファイルのすべてを転送する必要があります、イメージ ビットだけでなく。

クラスのドライバーが指すメモリを所有している、 **pGuid** microdriver は解放する必要がありますので、VAL 構造体のメンバー。

このコマンドが、microdriver が呼び出しに応答する方法に影響に注意してください。 その[**スキャン**](https://msdn.microsoft.com/library/windows/hardware/ff547322)関数。 通常どおり、microdriver がの値を確認する必要があります、 *lPhase*、 *pScanInfo*、および*lLength*がこの関数、およびデータ バッファー内のパラメーターが指す、*pBuffer*と*pReceived*に応じて適切なパラメーター。

WiaImgFmt ファイルのみをサポートするドライバー\_BMP と WiaImgFmt\_MEMORYBMP 形式 (microdrivers の既定の形式) は、CMD を受信できる\_SETFORMAT コマンド。 これらのドライバーは、クラス ドライバーは、既定の書式を使用してすべてのデータ転送を処理するため、このコマンドを無視できます。

<span id="CMD_SETSCANMODE"></span><span id="cmd_setscanmode"></span>CMD\_SETSCANMODE  
Microdriver のデバイスのスキャン モード - プレビュー版または最終的な--を設定する WIA ベッド ドライバーによって呼び出されます。 **LVal**のメンバー、 [ **VAL** ](https://msdn.microsoft.com/library/windows/hardware/ff548627)構造体で定義されているは、次の値の 1 つは*wiamicro.h*:

SCANMODE\_PREVIEWSCAN − プレビュー スキャン モード

SCANMODE\_FINALSCAN − 最終スキャン モード

<span id="CMD_SETSTIDEVICEHKEY"></span><span id="cmd_setstidevicehkey"></span>CMD\_SETSTIDEVICEHKEY  
インストールされているレジストリ セクション内のレジストリ エントリを読み取る microdriver を許可する WIA ベッド ドライバーによって呼び出されます。 このコマンドは、そのデバイスのプライベート レジストリ値にアクセスできるように、microdriver にインストールされているレジストリ HKEY STI デバイスを提供します。 **PHandle**のメンバー、 [ **VAL** ](https://msdn.microsoft.com/library/windows/hardware/ff548627)構造体は、WIA ベッド ドライバーに STI の中に指定された HKEY へのポインターを含める[ **IStiUSD::Initialize** ](https://msdn.microsoft.com/library/windows/hardware/ff543824)メソッド。 これは、インストールされているデバイス セクションの最上位レベルの HKEY です。 **DeviceData**キーは、この HKEY を使用して直接開くことができます。 参照してください[WIA デバイスの INF ファイル](https://msdn.microsoft.com/library/windows/hardware/ff542770)詳細についてはします。

注:このキーが開いたときおよび閉じた*のみ*WIA ベッド ドライバー。 有効です。 このコマンドと CMD の中にのみ\_初期化 (を参照してください[コマンドのために必要な](required-commands.md))。 これらのコマンドが return の後、キーが無効になっています。 HKEY 値*しないで*キャッシュします。

 

 




