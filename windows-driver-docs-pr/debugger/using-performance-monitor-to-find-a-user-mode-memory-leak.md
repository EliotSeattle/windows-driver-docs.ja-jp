---
title: パフォーマンス モニターを使用したユーザーモード メモリ リークの検出
description: パフォーマンス モニターを使用したユーザーモード メモリ リークの検出
ms.assetid: 07ba4c55-299c-4558-b4c7-4ffe5c47f496
keywords:
- メモリ リーク、ユーザーモード、パフォーマンス モニター
ms.date: 05/23/2017
ms.localizationpriority: high
ms.openlocfilehash: 37a669e3f196ef32ea40bafd15fa526f44080715
ms.sourcegitcommit: 5598b4c767ab56461b976b49fd75e4e5fb6018d2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2020
ms.locfileid: "78335949"
---
# <a name="using-performance-monitor-to-find-a-user-mode-memory-leak"></a>パフォーマンス モニターを使用したユーザーモード メモリ リークの検出


ユーザーモード メモリ リークの発生が疑われるが、その原因となっているプロセスがわからない場合、パフォーマンス モニターを使用して個々のプロセスのメモリ使用量を測定することができます。

パフォーマンス モニターを起動します。 次のカウンターを追加します。

-   **Process**--&gt;**Private Bytes** (調査するプロセスごとに)

-   **Process**--&gt;**Virtual Bytes** (調査するプロセスごとに)

時間の経過に伴うリークのグラフをキャプチャできるように、更新時間を 600 秒に変更します。 また、後で調査するために、データをファイルに記録することもお勧めします。

**Private Bytes** カウンターではプロセスが割り当てたメモリの総量が示されます。他のプロセスと共有されているメモリは、これに含まれません。 **Virtual Bytes** カウンターでは、プロセスが使用している仮想アドレス空間の現在のサイズが示されます。

メモリ リークの中には、割り当てられたプライベート バイト数の増加としてデータ ファイルで確認できるものがあります。 他には仮想アドレス空間の増大として確認できるメモリ リークもあります。

メモリ リークが発生しているプロセスを特定したら、UMDH ツールを使用して、問題があるルーチンを具体的に特定します。 詳細については、[UMDH を使用したユーザーモード メモリ リークの検出](using-umdh-to-find-a-user-mode-memory-leak.md)に関するページを参照してください。

 

 





