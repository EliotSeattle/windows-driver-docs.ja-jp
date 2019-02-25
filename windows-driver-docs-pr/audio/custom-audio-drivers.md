---
title: カスタム オーディオ ドライバー
description: カスタム オーディオ ドライバー
ms.assetid: d5f19a72-0b43-4fe1-b0e1-0198344b4d19
keywords:
- WDM オーディオ ドライバー WDK、カスタム
- オーディオ ドライバー WDK、カスタム
- カスタム オーディオ ドライバー WDK
- ベンダーから提供されたドライバー WDK オーディオ
- PortCls WDK のオーディオ、カスタムのオーディオ ドライバー
ms.date: 05/08/2018
ms.localizationpriority: medium
ms.openlocfilehash: 25539abfe183dc1090abebb04b5ce5ca16499d29
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559051"
---
# <a name="custom-audio-drivers"></a>カスタム オーディオ ドライバー


UAA と互換性がないオーディオ デバイスでは、ベンダーから提供されたカスタム ドライバーが必要です。 さらに、UAA と互換性のあるオーディオ アダプターが UAA クラス ドライバー; でサポートされていない独自の機能を組み込むことができます。これらの機能は、カスタム オーディオ ドライバーをベンダーが提供する場合にのみアプリケーションにアクセスできます。 システム提供の UAA ドライバーを通じてアクセスされる標準の UAA 機能のみです。 UAA でサポートされている機能については、次を参照してください。、[ユニバーサル オーディオ アーキテクチャ](https://download.microsoft.com/download/9/c/5/9c5b2167-8017-4bae-9fde-d599bac8184a/UAA_Guidelines.doc)ホワイト ペーパー。

カスタム オーディオ ドライバーを記述するための 2 つのオプションはハードウェア ベンダーに利用可能な: PortCls システム ドライバー (Portcls.sys) で使用するカスタム オーディオ アダプター ドライバーの開発やカスタムのミニドライバー AVStream クラスのシステム ドライバー (Ks.sys) で使用するための開発.

オーディオのアダプターのほとんどのカスタム ドライバーを使用して、PortCls で、オペレーティング システムの一部として提供されます。 PortCls システム ドライバー (Portcls.sys) には、タスクを簡単にカスタム オーディオ ドライバーを記述する組み込みのオーディオ ドライバー インフラストラクチャが含まれています。 PortCls は、wave、MIDI、またはミキサーのデバイスの特定の種類の汎用的な機能を管理するそれぞれの特殊化は、いくつかのポート ドライバーを実装します。 仕入先ポート ドライバー、オーディオのアダプターでのオーディオ機能を管理するのに適切なセットを選択すると、ミニポート ドライバーを選択したポート ドライバーと連携して動作しのハードウェアに依存する機能を制御の補完的なセットを開発してください。オーディオ デバイス。

仕入先では、カスタム AVStream クラス ミニドライバーを開発することで、オーディオ デバイスもサポートできます。 ミニドライバーはオペレーティング システムの一部として提供された AVStream クラス システム ドライバーと連動します。 PortCls を使用するよりも難しく、AVStream ドライバーの実装しますが、行うので可能性がありますオーディオとビデオを統合するデバイスに適したできます。 AVStream ドライバーは、既存の USB ドライブまたは IEEE 1394 オーディオ デバイス、システムによって提供される USBAudio または AVCAudio クラス システム ドライバーの要件に準拠するために失敗したために必要な場合もあります。

ほぼすべての PCI オーディオ アダプター ベンダーから提供されたカスタム ドライバーを必要とする、ベンダーは PortCls を選択する必要があります。

AVStream クラスのシステム ドライバー (Ks.sys) には、ほとんどの PortCls 内に存在するオーディオ固有のサポート機能が不足しています。

PortCls の詳細については、次を参照してください。[ポート クラスの概要](introduction-to-port-class.md)します。 AVStream の詳細については、次を参照してください。 [AVStream の概要](https://msdn.microsoft.com/library/windows/hardware/ff554240)します。

 

 



