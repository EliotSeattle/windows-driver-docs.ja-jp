---
title: アップグレード テストの実行と結果の調査
description: アップグレード テストの実行と結果の調査
ms.assetid: 82a2427e-94ed-4f7e-93e7-7952ca0d98e8
keywords:
- テスト ネットワーク コンポーネントをアップグレード WDK
- アップグレードのテストの WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 629d08fe474c3aaa181b437a3abfb555c91d8d3d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63386174"
---
# <a name="running-the-upgrade-test-and-examining-the-results"></a>アップグレード テストの実行と結果の調査





**注**  Microsoft Windows XP では、ベンダーから提供されたネットワークのアップグレードはサポートされていない (SP1 以降)、Microsoft Windows Server 2003、および以降のオペレーティング システム。

 

Windows 2000 またはそれ以降のシステムをアップグレードする前にアップグレードするには、各ネットワーク コンポーネントのレジストリ内のパラメーター値に注意してください。

**アップグレードのテストを実行するには**

1.  Windows 2000 以降のチェックのビルドを含む CD-ROM が CD-ROM ドライブであることを確認します。

2.  テスト システムでは、winnt32.exe を実行します。 たとえば、次のコマンドを使用して、CD-ROM ドライブ/o: での Intel ベースのシステム上の winnt32.exe を実行するには
    ```CMD
    winnt32.exe /s:o\i386
    ```

3.  Windows 2000 以降をインストールした後は、アップグレード後のネットワーク コンポーネントのパラメーターが新しいオペレーティング システムに正しく移行されたことを確認します。

 

 





