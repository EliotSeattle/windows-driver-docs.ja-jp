---
title: システムの電源状態
description: システムの電源状態
ms.assetid: bb30bc89-d1f2-4cb3-bcfb-fb76c69dba27
keywords:
- システム電源の状態 WDK カーネル、システム電源の状態について
- 状態遷移の WDK 電源管理
- Sx 名 WDK の電源管理
- ソフトウェアの再開 WDK 電源管理
- WDK の電源管理の再開
- ハードウェアの遅延 WDK 電源管理
- システム ハードウェア コンテキスト WDK 電源管理
- ハードウェア コンテキスト WDK 電源管理
- WDK の電源管理のコンテキスト
- WDK 電源管理の状態を解除
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 073611a13d298cdf2a8289b01815f2bfb5d9e7e2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63345443"
---
# <a name="system-power-states"></a>システムの電源状態





システム電源の状態では、全体として、システムの電力消費量について説明します。 オペレーティング システムのサポート s5 までからの S0 (完全におよび運用) と呼ばれる 6 つのシステム電源の状態 (電源オフ)。 各状態は、次のように分類されます。

-   消費電力: 電力量は、コンピューターを使用しますか?

-   ソフトウェアの再開: どのようなポイントからは、オペレーティング システムを再起動しますか?

-   ハードウェアの遅延: どのくらいの時間がかかりますにコンピューターを稼働状態に戻りますか?

-   (揮発性のプロセッサのレジスタ、メモリ キャッシュ、および RAM の内容) などのシステム ハードウェアのコンテキスト: 量システム ハードウェアのコンテキストが保持されますか? オペレーティング システムを稼働状態に戻るに再起動する必要がありますか。

S0 の状態では、作業の状態です。 状態 S1、S2、S3 の場合、および S4 はコンピューターが消費電力の削減のため無効が表示されますが、オペレーティング システムを再起動しなくても、稼働状態に戻るには、十分なコンテキストを保持するときに、状態、休止します。 S5 がシャット ダウン状態または状態はオフです。

システムが*ウェイク*とシャット ダウン状態 (S5) または (S1 S4) スリープ状態から作業の状態 (S0) への移行では、作業の状態からスリープ状態またはシャット ダウン状態への移行にあるときにスリープ状態になります. 次の図は、実行可能なシステム電源の状態遷移を示します。

![実行可能なシステム電源の状態遷移を示す図](images/sysstate.png)

システムが別; から直接 1 つのスリープ状態に入ることはできません前の図に示すよう作業の状態、スリープ状態に入る前に入れるように常にする必要があります。 たとえば、システムは、状態 S2、S4 からも S2 に状態 S4 から移行できません。 最初に返す必要があります、S0 を元となることができます、次のスリープ状態を入力します。 中間のスリープ状態にシステムがいくつかの操作コンテキストを失った既にあるため、追加の状態の移行を行うには、そのコンテキストを復元する作業の状態を返す必要があります。

 

 




