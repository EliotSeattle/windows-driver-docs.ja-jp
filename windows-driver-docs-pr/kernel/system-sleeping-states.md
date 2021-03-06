---
title: システムのスリープ状態
description: システムのスリープ状態
ms.assetid: 2fd883b5-4e89-4ce9-b75a-b821348ac860
keywords:
- システムの電源状態 WDK カーネル、スリープ状態
- システムのスリープ状態 WDK 電源管理
- スリープ状態 WDK 電源管理
- S1 WDK 電源管理
- S2 WDK 電源管理
- S3 WDK 電源管理
- S4 WDK 電源管理
- ソフトウェアの再開 WDK 電源管理
- 再開 WDK 電源管理
- ハードウェア待機時間 WDK 電源管理
- システム ハードウェア コンテキスト WDK 電源管理
- ハードウェア コンテキスト WDK 電源管理
- コンテキスト WDK 電源管理
- 待機時間 WDK 電源管理
ms.date: 06/16/2017
ms.localizationpriority: High
ms.openlocfilehash: 52144a68515e30a58a398ab593f0f1ff160d505a
ms.sourcegitcommit: 5598b4c767ab56461b976b49fd75e4e5fb6018d2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2020
ms.locfileid: "72007650"
---
# <a name="system-sleeping-states"></a>システムのスリープ状態





状態 S1、S2、S3、および S4 はスリープ状態です。 これらのいずれかの状態にあるシステムでは計算タスクが実行されないため、オフになっているように見えます。 ただし、シャットダウン状態 (S5) のシステムとは異なり、スリープ状態のシステムでは、ハードウェアまたはディスクにメモリ状態が保持されます。 コンピューターを動作状態に戻すために、オペレーティング システムを再起動する必要はありません。

一部のデバイスでは、特定のイベント (モデムへの着信呼び出しなど) が発生したときに、システムをスリープ解除させることができます。 さらに、一部のコンピューターでは、外部インジケーターによって、システムが単にスリープ状態であることがユーザーに通知されます。

S1 から S4 に続く各スリープ状態ごとに、より多くのコンピューターがシャットダウンされます。 ACPI に準拠しているすべてのコンピューターでは、以下のセクションに記載されているように、S1 でプロセッサ クロックがシャットダウンされ、S4 でシステム ハードウェア コンテキストを失います (シャットダウン前に休止ファイルが書き込まれていない場合)。 中間スリープ状態の詳細は、製造元によるコンピューターの設計方法によって異なります。 たとえば、一部のコンピューターでは、マザーボード上の特定のチップが S3 で電力を失う一方で、その他のチップでは、S4 まで電力が保持されます。 さらに、一部のデバイスでは、S1 からのみシステムをスリープ解除でき、それ以降の状態からは解除できない場合があります。

### <a name="system-power-state-s1"></a>システムの電源状態 S1

システムの電源状態 S1 は、次の特性を持つスリープ状態です。

<a href="" id="power-consumption"></a>**電力消費**  
S0 よりも消費量が少なく、他のスリープ状態よりも多くなっています。 プロセッサ クロックはオフになっており、バス クロックは停止されています。

<a href="" id="software-resumption"></a>**ソフトウェアの再開**  
制御は、中断された箇所から再開されます。

<a href="" id="hardware-latency"></a>**ハードウェアの待機時間**  
通常は 2 秒以内です。

<a href="" id="system-hardware-context"></a>**システム ハードウェア コンテキスト**  
すべてのコンテキストは、ハードウェアによって保持および管理されます。

### <a name="system-power-state-s2"></a>システムの電源状態 S2

システムの電源状態 S2 は S1 に似ていますが、プロセッサの電源が切れているために、システム キャッシュの CPU コンテキストとコンテンツが失われる点が異なります。 状態 S2 には以下の特徴があります。

<a href="" id="power-consumption"></a>**電力消費**  
状態 S1 よりも消費量が少なく、S3 よりも多くなっています。 プロセッサはオフになっています。 バス クロックは停止されています。そのため、一部のバスで電力が失われる可能性があります。

<a href="" id="software-resumption"></a>**ソフトウェアの再開**  
スリープ解除後、制御はプロセッサのリセット ベクターから開始されます。

<a href="" id="hardware-latency"></a>**ハードウェアの待機時間**  
2 秒以上。S1 の待機時間以上。

<a href="" id="system-hardware-context"></a>**システム ハードウェア コンテキスト**  
CPU コンテキストとシステム キャッシュの内容が失われます。

### <a name="system-power-state-s3"></a>システムの電源状態 S3

システムの電源状態 S3 は、次の特性を持つスリープ状態です。

<a href="" id="power-consumption"></a>**電力消費**  
状態 S2 よりも消費量が少なくなります。 プロセッサはオフになっていて、マザーボード上の一部のチップもオフになっている可能性があります。

<a href="" id="software-resumption"></a>**ソフトウェアの再開**  
スリープ解除イベントの後、制御はプロセッサのリセット ベクターから開始されます。

<a href="" id="hardware-latency"></a>**ハードウェアの待機時間**  
S2 とほとんど区別できません。

<a href="" id="system-hardware-context"></a>**システム ハードウェア コンテキスト**  
システム メモリのみが保持されます。 CPU コンテキスト、キャッシュの内容、およびチップセットのコンテキストが失われます。

### <a name="system-power-state-s4"></a>システムの電源状態 S4

システムの電源状態 S4 (休止状態) は、給電量が最も低いスリープ状態であり、スリープ解除の待機時間が最も長くなります。 電力消費を最小限に抑えるために、ハードウェアのすべてのデバイスの電源がオフになります。 ただし、オペレーティング システムのコンテキストは、システムが S4 状態に入る前にディスクに書き込む休止ファイル (メモリのイメージ) に保持されます。 再起動時に、ローダーでこのファイルが読み取られ、システムの休止前の場所にジャンプします。

S1、S2、または S3 状態のコンピューターが AC またはバッテリ電力をすべて失った場合、システム ハードウェア コンテキストが失われるため、再起動して S0 に戻る必要があります。 ただし、状態 S4 のコンピューターはオペレーティング システムのコンテキストが休止ファイルに保持されているため、バッテリまたは AC 電源が失われた後でも、以前の場所から再起動できます。 休止状態のコンピューターは電力を使用しません (トリクル充電の例外はあり)。

状態 S4 には以下の特徴があります。

<a href="" id="power-consumption"></a>**電力消費**  
オフ。ただし、電源ボタンと同様のデバイスに対しするトリクル充電を除きます。

<a href="" id="software-resumption"></a>**ソフトウェアの再開**  
システムは、保存された休止状態ファイルから再起動されます。 休止状態ファイルを読み込めない場合は、再起動が必要です。 システムが S4 状態のときにハードウェアを再構成すると、休止ファイルが変更され、正しく読み込まれない可能性があります。

<a href="" id="hardware-latency"></a>**ハードウェアの待機時間**  
長く、定義されていません。 システムを動作状態に復帰するのは、物理的に操作することのみです。 このような操作には、ユーザーによって起動スイッチが押されたこと、またはスリープ解除機能が有効になっているハードウェアが存在する場合は、LAN 上のモデムまたはアクティビティの着信が含まれる場合があります。 ハードウェアでサポートされている場合、マシンは再開タイマーからもスリープ解除できます。

<a href="" id="system-hardware-context"></a>**システム ハードウェア コンテキスト**  
ハードウェアには保持されません。 システムは、電源を切る前に、休止状態ファイルにメモリのイメージを書き込みます。 オペレーティング システムが読み込まれると、このファイルが読み取られ、前の場所にジャンプします。

 

 




