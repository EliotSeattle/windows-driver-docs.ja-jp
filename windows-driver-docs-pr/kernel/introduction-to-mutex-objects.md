---
title: ミューテックス オブジェクトの概要
description: ミューテックス オブジェクトの概要
ms.assetid: c35b4341-09dd-411d-b933-6c762fecd23c
keywords:
- カーネルディスパッチャーオブジェクト WDK、mutex オブジェクト
- ディスパッチャーオブジェクト WDK カーネル、ミューテックスオブジェクト
- mutex オブジェクト WDK カーネル
- 相互排他アクセス WDK カーネル
- mutex オブジェクトを待機しています
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5398f34435f95d797d9d6ef82e76731a52dd8725
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72828187"
---
# <a name="introduction-to-mutex-objects"></a>ミューテックス オブジェクトの概要


名前が示すように、mutex オブジェクトは、一連のカーネルモードスレッド間で共有される1つのリソースに相互に排他的にアクセスできるように設計された同期メカニズムです。 Executive ワーカースレッドを使用するファイルシステムドライバー (FSDs) などの最上位レベルのドライバーのみが、mutex オブジェクトを使用する可能性があります。

場合によっては、ドライバーによって作成されたスレッドまたはワーカースレッドのコールバックルーチンがある最上位レベルのドライバーで mutex オブジェクトを使用することがあります。 ただし、ページング可能なスレッドまたはワーカースレッドのコールバックルーチンを含むすべてのドライバーは、その mutex オブジェクトの取得、待機、およびリリースを非常に慎重に管理する必要があります。

Mutex オブジェクトには、システム (カーネルモードのみ) のスレッドが、SMP マシンの共有リソースへのデッドロックフリーのアクセスを提供する組み込みの機能があります。 カーネルはミューテックスの所有権を一度に1つのスレッドに割り当てます。

ミューテックスの所有権を取得すると、通常のカーネルモードの非同期プロシージャ呼び出し (Apc) が配信されなくなります。 カーネルが特別なカーネル APC を実行するために APC\_レベルのソフトウェア割り込みを発行する場合を除き、スレッドは APC によって割り込まれません。ただし、i/o 操作の元の要求元に結果を返す i/o マネージャーの IRP 完了ルーチンなどです。

スレッドは、既に所有している mutex オブジェクト (再帰的な所有権) の所有権を取得できますが、再帰的に取得した mutex オブジェクトは、スレッドが所有権を完全に解放するまで、シグナル状態に設定されません。 このようなスレッドは、別のスレッドがミューテックスを取得する前に、所有権を取得した回数だけミューテックスを明示的に解放する必要があります。

このカーネルでは、ミューテックスを所有するスレッドが、最初にミューテックスを解放してシグナル状態に設定することなく、ユーザーモードへの遷移を引き起こすことを許可することはありません。 ミューテックスを所有する FSD またはドライバーによって作成されたスレッドが、ミューテックスの所有権を解放する前に、i/o マネージャーに制御を戻しようとすると、カーネルによってシステムが停止します。

Mutex オブジェクトを使用するすべてのドライバーは、mutex オブジェクトを待機または解放する前に、 [**KeInitializeMutex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keinitializemutex)を1回呼び出す必要があります。 次の図は、2つのシステムスレッドが mutex オブジェクトを使用する方法を示しています。

![mutex オブジェクトを待機していることを示す図](images/3mutxobj.png)

前の図に示すように、mutex オブジェクトを使用するドライバーは、ミューテックスオブジェクトのストレージを提供する必要があります。このオブジェクトは常駐型である必要があります。 ドライバーで作成されたデバイスオブジェクトの[デバイス拡張機能](device-extensions.md)、コントローラー[オブジェクト](using-controller-objects.md)を使用している場合はコントローラー拡張機能、ドライバーによって割り当てられた非ページプールを使用できます。

ドライバーが**KeInitializeMutex**を (通常は[*AddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)ルーチンから) 呼び出すときは、ドライバーのストレージへのポインターを mutex オブジェクトに渡す必要があります。これにより、カーネルはシグナル状態に初期化されます。

このような最上位レベルのドライバーが初期化されると、前の図に示したように、共有リソースへの相互排他的なアクセスを管理できます。 たとえば、本質的に同期操作やスレッドのドライバーのディスパッチルーチンでは、ミューテックスを使用して、ドライバーによって作成された Irp のキューを保護することができます。

**KeInitializeMutex**は常に mutex オブジェクトの初期状態をシグナル状態に設定します (前の図に示すように)。

1.  *Mutex*ポインターを使用した[**KeWaitForSingleObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kewaitforsingleobject)へのディスパッチルーチンの最初の呼び出しでは、現在のスレッドがすぐに準備完了状態になり、ミューテックスのスレッド所有権が与えられ、Mutex 状態が Not シグナル状態にリセットされます。 ディスパッチルーチンの実行が再開されるとすぐに、IRP をミューテックスで保護されたキューに安全に挿入できます。

2.  2番目のスレッド (別のディスパッチルーチン、ドライバーによって提供されるワーカースレッドのコールバックルーチン、またはドライバーによって作成されたスレッド) が*Mutex*ポインターを使用して**KeWaitForSingleObject**を呼び出すと、2番目のスレッドが待機状態になります。

3.  手順 1. で説明されているように、ディスパッチルーチンが IRP のキューを終了すると、 *Mutex*ポインターとブール値の*待機*値を使用して[**KeReleaseMutex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleasemutex)を呼び出します。これは、 **KeWaitForSingleObject** [**を呼び出す必要があるかどうかを示します。** ](https://msdn.microsoft.com/library/windows/hardware/ff553344) **KeReleaseMutex**が制御を返すとすぐに*Mutex*を含む KeWaitForMutexObject)。

4.  ディスパッチルーチンが、手順 3 ( **FALSE**に設定された*待機*) でミューテックスの所有権を解放したと仮定した場合、ミューテックスは**KeReleaseMutex**によってシグナル状態に設定されます。 ミューテックスには現在所有者が存在しないため、別のスレッドがそのミューテックスを待機しているかどうかがカーネルによって判断されます。 その場合、カーネルは2番目のスレッド (手順2を参照) を mutex 所有者にします。これにより、スレッドの優先度が最も低い優先順位値になる可能性があり、その状態が準備完了に変わります。

5.  カーネルは、プロセッサが使用可能になるとすぐに、2番目のスレッドの実行をディスパッチします。つまり、優先順位の高い他のスレッドが現在準備完了状態であり、カーネルモードルーチンが上位の IRQL で実行されない場合です。 2番目のスレッド (IRP をキューに置いているディスパッチルーチン、またはドライバーによって作成されたスレッドが irp をデキューした場合) は、 **KeReleaseMutex**を呼び出すまで、irp の mutex で保護されたキューに安全にアクセスできるようになりました。

スレッドが mutex オブジェクトの所有権を再帰的に取得した場合、そのスレッドは mutex オブジェクトをシグナル状態に設定するために、ミューテックスで待機している回数だけ**KeReleaseMutex**を明示的に呼び出す必要があります。 たとえば、スレッドが**KeWaitForSingleObject**を呼び出した後、同じ*Mutex*ポインターで**Kewaitformutexobject**を呼び出した場合、ミューテックスオブジェクトをシグナルに設定するために、ミューテックスを取得するときに**KeReleaseMutex**を2回呼び出す必要があります。状態.

*Wait*パラメーターを**TRUE**に設定して**KeReleaseMutex**を呼び出すと、呼び出し元が**KeReleaseMutex**から戻るときに**kewait * Xxx*** サポートルーチンをすぐに呼び出すことを示します。

**Wait パラメーターを KeReleaseMutex に設定する場合は、次のガイドラインを考慮してください。**

IRQL パッシブ\_レベルで実行されるページング可能なスレッドまたはページング可能なドライバールーチンは、 *Wait*パラメーターを**TRUE**に設定して**KeReleaseMutex**を呼び出すことはできません。 このような呼び出しでは、 **KeReleaseMutex**と**kewait*Xxx*オブジェクト**の呼び出しの間に呼び出し元がページアウトされた場合に、致命的なページフォールトが発生します。

パッシブ\_レベルよりも大きい IRQL で実行される標準ドライバールーチンでは、システムをダウンさせずに、任意のディスパッチャーオブジェクトで0以外の間隔を待機することはできません。 ただし、このようなルーチンは、ディスパッチ\_レベル以下の IRQL で実行中に mutex を所有している場合、 **KeReleaseMutex**を呼び出すことができます。

標準のドライバールーチンを実行する IRQLs の概要については、「[ハードウェアの優先順位の管理](managing-hardware-priorities.md)」を参照してください。

 

 




