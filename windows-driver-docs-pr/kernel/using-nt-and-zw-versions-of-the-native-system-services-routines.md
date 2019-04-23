---
title: Nt および Zw バージョンのネイティブ システム サービス ルーチンの使用
description: Nt および Zw バージョンのネイティブ システム サービス ルーチンの使用
ms.assetid: 89627ddb-621d-4d27-acd6-16308689165d
keywords:
- Native System Services API WDK
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3ea0e42c42cad7f7ebdef549eac488c43224bcfa
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574076"
---
# <a name="using-nt-and-zw-versions-of-the-native-system-services-routines"></a>Nt および Zw バージョンのネイティブ システム サービス ルーチンの使用


Windows ネイティブのオペレーティング システムのサービス API は、カーネル モードで実行されるルーチンのセットとして実装されます。 これらのルーチンは、プレフィックスで始まる名前を持つ**Nt**または**Zw**します。 カーネル モード ドライバーでは、これらのルーチンを直接呼び出すことができます。 ユーザー モード アプリケーションは、システムの呼び出しを使用してこれらのルーチンにアクセスできます。

いくつかの例外では、ネイティブ システム サービス ルーチンはそれぞれ異なるプレフィックスが、名前が似ている 2 つの異なるバージョンがあります。 呼び出しなど[NtCreateFile](https://go.microsoft.com/fwlink/p/?linkid=157250)と[ **ZwCreateFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566424)同様の操作を実行し、同じカーネル モード システム ルーチンが、実際には、サービスを提供します。 ユーザー モードからシステムの呼び出し、 **Nt**と**Zw**ルーチンのバージョンの動作は同じです。 カーネル モード ドライバーからの呼び出し、 **Nt**と**Zw**ルーチンのバージョンを呼び出し元がルーチンに渡すパラメーターの値を扱う方法が異なります。

カーネル モード ドライバーは呼び出し、 **Zw**サービス パラメーターが、信頼されたカーネル モードのソースから取得したルーチンを通知するルーチンのネイティブ システムのバージョン。 この場合、ルーチンは、安全に検証しことがなくパラメーターを使用、できることを前提とします。 ただし、ユーザー モードのソースまたはカーネル モードのソースからパラメーターがある場合、ドライバー代わりに呼び出して、 **Nt**かどうかを決定する、そのルーチンのバージョンを呼び出し元のスレッドの履歴に基づくパラメーターユーザー モードまたはカーネル モードで開始されます。 ルーチンがカーネル モードのパラメーターとユーザー モード パラメーターを区別する方法の詳細については、[ **PreviousMode**](previousmode.md)を参照してください。

ユーザー モード アプリケーションを呼び出すと、 **Nt**または**Zw**サービス ルーチンのネイティブ システムのバージョン、ルーチン常に受信したパラメーターは値として処理されるユーザー モードのソースから取得しました。信頼されていません。 ルーチンは、パラメーターを使用する前に、パラメーター値を十分に検証します。 具体的には、ルーチンは、バッファーは有効なユーザー モードのメモリ内にあるし、位置が正しく調整を確認する呼び出し元が指定したバッファーをプローブします。

ネイティブ システム サービス ルーチンでは、受け取ったパラメーターに関する追加の前提条件を確認します。 ルーチンは、カーネル モード ドライバーで割り当てられたバッファーへのポインターを受け取る場合、ルーチンでは、ユーザー モードのメモリではなく、システム メモリ内でバッファーを割り当てられたこと前提としています。 ルーチンは、ユーザー モード アプリケーションによって開かれたハンドルを受信する場合、ルーチンは、カーネル モードのハンドル テーブルではなくユーザー モードのハンドル テーブルでのハンドルを検索します。

いくつかの点では、パラメーター値の意味はユーザー モードおよびカーネル モードからの呼び出しで大幅に異なります。 たとえば、 [ **ZwNotifyChangeKey** ](https://msdn.microsoft.com/library/windows/hardware/ff566488)ルーチン (またはその**NtNotifyChangeKey**対応)、入力パラメーターのペアを持つ*ApcRoutine*と*ApcContext*、ということで、パラメーターがユーザー モードまたはカーネル モードのソースからかどうかによって異なります。 ユーザー モードからの呼び出しに対して*ApcRoutine* 、APC ルーチンを指すと*ApcContext* APC ルーチンを呼び出すときに、オペレーティング システムが提供するコンテキスト値を指します。 カーネル モードからの呼び出しに対して*ApcRoutine*を指す、 [**作業\_キュー\_項目**](https://msdn.microsoft.com/library/windows/hardware/ff557304)構造、および*ApcContext*によって定義された作業のキュー項目の種類を指定します、**作業\_キュー\_項目**構造体。

ここでは、次のトピックについて説明します。

[**PreviousMode**](previousmode.md)

[ライブラリとヘッダー](libraries-and-headers.md)

[Zw プレフィックスは何を意味しますか。](what-does-the-zw-prefix-mean-.md)

[アクセス権を指定します。](access-mask.md)

[NtXxx ルーチン](ntxxx-routines.md)

 

 



