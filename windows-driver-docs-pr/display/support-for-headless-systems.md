---
title: ヘッドレス システムのサポート
description: Windows 8 では、すべてのグラフィックス ハードウェアなしのブートをサポートします。
ms.assetid: 6351F6F9-6666-4040-A82A-3813ACCE8DEA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 522b2b4c9efc7792de9edc840d69f9c0a7bd09b2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63375903"
---
# <a name="support-for-headless-systems"></a>ヘッドレス システムのサポート


Windows 8 では、すべてのグラフィックス ハードウェアなしのブートをサポートします。 これは、ディスプレイ デバイスが見つからない場合は、スタブの表示出力を使用して行われます。 このスタブの表示は、一部のインボックス Microsoft 基本的な表示ドライバー (MSBDD) として実装されます。

PnP ドライバーが利用できない場合は、スタブの表示が使用され、サードパーティ製のドライバーは必要ありません。 偽のディスプレイ デバイスに必要なハードウェアまたはファームウェアのサポートがないように両方の通常の操作とシステムのクラッシュを動作します。

MSBDD は、ノルム VGA がされているアーキテクチャ、VGA がないことです。 正の確認が必要それ以外の場合、VGA ハードウェアが使用可能であり、システムがヘッドレスでないことを想定します。 システム ファームウェアは、IAPC で存在してしない VGA フラグを設定する必要があります\_ブート\_FADT のアーキテクチャのフィールドであり、空のモード一覧 VESA BIOS 拡張 (VBE) を通じてを実装する必要がありますすべて VBIOS がある場合。 これらのメカニズムでは、システムが Windows の以前のバージョンとの互換性の int 10 h モード 12 時間対応の VBIOS を実装している場合でもには、VGA が存在しないことを示す必要があります。 VBE のサポートがない場合は、基本の表示ドライバーは、ヘッドレス システムは、UEFI の GOP を作業の表示を表していない必要がありますので、ブート ローダーによって初期化される表示を使用します。

 

 





