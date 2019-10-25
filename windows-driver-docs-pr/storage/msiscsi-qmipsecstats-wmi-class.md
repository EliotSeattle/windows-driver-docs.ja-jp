---
title: MSiSCSI\_QMIPSECStats WMI クラス
description: MSiSCSI\_QMIPSECStats WMI クラス
ms.assetid: 81a21c25-5f03-4ad0-a892-3947d65975d2
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 2b1e204e28437a9d1a86ede56ca3d3b023d28a7d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840626"
---
# <a name="msiscsi_qmipsecstats-wmi-class"></a>MSiSCSI\_QMIPSECStats WMI クラス


## <span id="ddk_msiscsi_qmipsecstats_wmi_class_kr"></span><span id="DDK_MSISCSI_QMIPSECSTATS_WMI_CLASS_KR"></span>


MSiSCSI\_MMIPSECStats WMI クラスは、iSCSI Hba のクイックモード IPsec 統計情報を公開します。

このクラスは記憶域ミニポートドライバーの特定のインスタンスに関連付けられているため、ミニポートドライバーは、ミニポートドライバーが管理する特定の物理デバイスオブジェクト (PDO) の名前を使用してクラスを登録する必要があります。

MSiSCSI\_MMIPSECStats クラスは*Iscsiprf*で定義されています。

```cpp
class MSiSCSI_QMIPSECStats : Win32_PerfRawData {
  [read,key] String  InstanceName;
  [read] boolean  Active;
  [read, WmiDataId(1), 
    CounterType(PERF_COUNTER_LARGE_RAWCOUNT), 
    DefaultScale(0), PerfDetail(100), Description("The 
    number of active IPsec SAs"): amended, 
    cpp_quote(
    "// The number of active IPsec SAs")] 
    uint64  ActiveSA;
  [read, WmiDataId(2), 
    CounterType(PERF_COUNTER_LARGE_RAWCOUNT), 
    DefaultScale(0), PerfDetail(100), Description("The 
    number of IPsec key operations in progress"): amended, 
    cpp_quote("
    // The number of IPsec key operations in progress")] 
    uint64  PendingKeyOperations;
  [read, WmiDataId(3), 
    CounterType(PERF_COUNTER_LARGE_RAWCOUNT), 
    DefaultScale(0), PerfDetail(100), Description("The total 
    number of successful IPsec SA negotiations"): amended, 
    cpp_quote(
    "// The total number of successful IPsec SA 
    negotiations")] 
    uint64  KeyAdditions;
  [read, WmiDataId(4), 
    CounterType(PERF_COUNTER_LARGE_RAWCOUNT), 
    DefaultScale(0), PerfDetail(100), Description("The total 
    number of key deletions for IPsec SA"): amended, 
    cpp_quote("// The total number of key deletions for 
    IPsec SA")] 
    uint64  KeyDeletions;
  [read, WmiDataId(5), 
    CounterType(PERF_COUNTER_LARGE_RAWCOUNT), 
    DefaultScale(0), PerfDetail(100), Description("The 
    number of rekey operations for IPsec SAs."): amended, 
    cpp_quote("
    // The number of rekey operations for IPsec SAs.")] 
    uint64  ReKeys;
  [read, WmiDataId(6),
    CounterType(PERF_COUNTER_LARGE_RAWCOUNT), 
    DefaultScale(0), PerfDetail(100), Description("The 
    number of active IPsec tunnels."): amended, 
    cpp_quote(
    "// The number of active IPsec tunnels.")] 
    uint64  ActiveTunnels;
  [read, WmiDataId(7), 
    CounterType(PERF_COUNTER_LARGE_RAWCOUNT), 
    DefaultScale(0), PerfDetail(100), Description("The total 
    number of packets for which the Security Parameters 
    Index (SPI) was incorrect."): amended, 
    cpp_quote(
    "// The total number of packets for which the Security 
    Parameters Index (SPI) was incorrect.")] 
    uint64  BadSPIPackets;
  [read, WmiDataId(8), 
    CounterType(PERF_COUNTER_LARGE_RAWCOUNT), 
    DefaultScale(0), PerfDetail(100), Description("The total 
    number of packets that failed decryption."): amended, 
    cpp_quote(
    "// The total number of packets that failed 
    decryption.")] 
    uint64  PacketsNotDecrypted;
  [read, WmiDataId(9), 
    CounterType(PERF_COUNTER_LARGE_RAWCOUNT), 
    DefaultScale(0), PerfDetail(100), Description("The total 
    number of packets for which data could not be verified. 
    "): amended, 
    cpp_quote(
    "// The total number of packets for which data could not 
    be verified. ")] 
    uint64  PacketsNotAuthenticated;
  [read, WmiDataId(10), 
    CounterType(PERF_COUNTER_BULK_COUNT),
    DefaultScale(0), 
    PerfDetail(100), Description("The total number of 
    packets that contained a valid Sequence Number field."): 
    amended, 
    cpp_quote(
    "// The total number of packets that contained a valid 
    Sequence Number field.")] 
    uint64  PacketsWithReplayDetection;
  [read, WmiDataId(11), 
    CounterType(PERF_COUNTER_BULK_COUNT), DefaultScale(0), 
    PerfDetail(100), Description("The number of bytes sent 
    using the ESP protocol."): amended, 
    cpp_quote(
    "// The number of bytes sent using the ESP protocol.")] 
    uint64  ConfidentialBytesSent;
  [read, WmiDataId(12), 
    CounterType(PERF_COUNTER_BULK_COUNT), DefaultScale(0), 
    PerfDetail(100), Description("The number of bytes 
    received using the ESP protocol."): amended, 
    cpp_quote(
    "// The number of bytes received using the ESP 
    rotocol.")] 
    uint64  ConfidentialBytesReceived;
  [read, WmiDataId(13), 
    CounterType(PERF_COUNTER_BULK_COUNT), DefaultScale(0), 
    PerfDetail(100), Description("The number of bytes sent 
    using the AH protocol."): amended, 
    cpp_quote(
    "// The number of bytes sent using the AH protocol.")] 
    uint64  AuthenticatedBytesSent;
  [read, WmiDataId(14), 
    CounterType(PERF_COUNTER_BULK_COUNT), DefaultScale(0), 
    PerfDetail(100), Description("The number of bytes 
    received using the AH protocol."): amended, cpp_quote(
    "// The number of bytes received using the AH 
    rotocol.")] 
    uint64  AuthenticatedBytesReceived;
  [read, WmiDataId(15), 
    CounterType(PERF_COUNTER_BULK_COUNT), DefaultScale(0), 
    PerfDetail(100), Description("The number of bytes sent 
    using the IPsec protocol."): amended, 
    cpp_quote(
    "// The number of bytes sent using the IPsec 
    rotocol.")] 
    uint64  TransportBytesSent;
  [read, WmiDataId(16), 
    CounterType(PERF_COUNTER_BULK_COUNT), DefaultScale(0), 
    PerfDetail(100), Description("The number of bytes 
    received using the IPsec protocol."): amended, 
    cpp_quote(
    "// The number of bytes received using the IPsec
    protocol.")] 
    uint64  TransportBytesReceived;
  [read, WmiDataId(17), 
    CounterType(PERF_COUNTER_BULK_COUNT),
    DefaultScale(0), 
    PerfDetail(100), Description("The number of bytes sent 
    using the IPsec tunnel mode."): amended, 
    cpp_quote(
    "// The number of bytes sent using the IPsec tunnel 
    node.")] 
    uint64  TunnelBytesSent;
  [read, WmiDataId(18), 
    CounterType(PERF_COUNTER_BULK_COUNT), DefaultScale(0), 
    PerfDetail(100), Description("The number of bytes 
    received using the IPsec tunnel mode."): amended, 
    cpp_quote(
    "// The number of bytes received using the IPsec tunnel 
    node.")] 
    uint64  TunnelBytesReceived;
};
```

WMI ツールスイートは、前のクラス定義をコンパイルするときに、 [**Msiscsi\_QMIPSECStats**](https://docs.microsoft.com/windows-hardware/drivers/ddi/iscsiprf/ns-iscsiprf-_msiscsi_qmipsecstats)データ構造体を生成します。

 

 





