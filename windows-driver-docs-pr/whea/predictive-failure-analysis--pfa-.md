---
title: Predictive Failure Analysis (PFA)
description: Predictive Failure Analysis (PFA)
ms.assetid: d2ded330-edcc-4bdd-9b52-73c1961d8ef2
keywords:
- Windows ハードウェア エラー アーキテクチャ WDK、予測的な失敗の分析
- Windows Hardware Error Architecture、WDK PFA
- WHEA WDK、予測的な失敗の分析
- WHEA WDK、PFA
- 予測的な失敗の分析 (PFA) WDK WHEA
- PFA WDK WHEA
- WDK WHEA 失敗の分析
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0aa20c31aa995cc3b23d6c242d5b486249beb650
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63340740"
---
# <a name="predictive-failure-analysis-pfa"></a>Predictive Failure Analysis (PFA)


Windows ハードウェア エラー アーキテクチャ (WHEA) は、ECC メモリの予測的な障害の分析 (PFA) をサポートします。 WHEA は PFA を使用すると、以前のエラーが発生している 1 つまたは複数の ECC メモリ ページを監視できます。 エラーの数は、時間間隔内で、同じページに対するしきい値を超えた、WHEA はメモリのページをオフラインにしようとします。

コンピューター システム、特に server システムの場合は、通常、メモリ エラーの特定の種類を自動的に修正できるエラー修正コード (ECC) メモリは装備されています。 ECC メモリ システムで修正されたエラーとその頻度に関する情報は、オペレーティング システムで使用できると壊滅的な原因となる予定外のダウンタイムにできる修正不可能なエラーなどの兆候の不具合を予測に使用できます.

レジストリ設定を使用して、WHEA を PFA エラーのしきい値、時間間隔、およびその他のパラメーターを構成できます。 これを行う方法の詳細については、次を参照してください。 [WHEA ポリシー設定](whea-pfa-registry-settings.md)します。

WHEA PFA を実行する方法の概要については、次を参照してください。 [PFA が WHEA によって実行される](pfa-performed-by-whea.md)します。

A[プラットフォーム固有のハードウェア エラー ドライバー (PSHED) プラグイン ドライバー](platform-specific-hardware-error-driver-plug-ins2.md) ECC メモリ PFA も実行できます。 これにより、プラグイン (WHEA ではありません) は、ECC メモリ ページを監視する必要があります。 PSHED プラグインが PFA を実行する方法の詳細については、次を参照してください。 [PFA 実行プラグイン PSHED](pfa-performed-by-a-pshed-plug-in.md)します。

PFA、ECC メモリ ページは失敗、予測が保存 (または*が解決しない*)、ブート構成データ (BCD) のシステム ストアの結果。 このプロセスの詳細については、次を参照してください。 [PFA 結果の永続化](persistence-of-pfa-results.md)します。

WHEA では、Windows 7 および Windows の以降のバージョンで PFA をサポートしています。

 

 




