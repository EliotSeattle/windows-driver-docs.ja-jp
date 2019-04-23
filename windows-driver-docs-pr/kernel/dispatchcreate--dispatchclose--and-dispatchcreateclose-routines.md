---
title: DispatchCreate、DispatchClose、DispatchCreateClose ルーチン
description: DispatchCreate、DispatchClose、DispatchCreateClose ルーチン
ms.assetid: 5c1c0036-71b1-4410-b157-f9ebe3b6ecfc
keywords:
- ディスパッチ ルーチンの WDK カーネル、DispatchCreate ルーチン
- ディスパッチ ルーチンの WDK カーネル、DispatchClose ルーチン
- ディスパッチ ルーチンの WDK カーネル、DispatchCreateClose ルーチン
- DispatchCreateClose ルーチン
- DispatchClose ルーチン
- DispatchCreate ルーチン
- Irp_mj_create 用 I/O 関数のコード
- 未完了の I/O 関数のコード
- ディスパッチ ルーチン WDK カーネルを作成します。
- ディスパッチ ルーチン WDK カーネルを閉じる
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 539efa05a13f866c6aeb66b2af6a982cf6fda117
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573457"
---
# <a name="dispatchcreate-dispatchclose-and-dispatchcreateclose-routines"></a>DispatchCreate、DispatchClose、DispatchCreateClose ルーチン





ドライバーの[ *DRIVER_DISPATCH* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch) Irp の I/O 関数のコードを持つ[ **IRP\_MJ\_作成**](https://msdn.microsoft.com/library/windows/hardware/ff550729)と[**IRP\_MJ\_閉じる**](https://msdn.microsoft.com/library/windows/hardware/ff550720)、それぞれします。 または、組み合わされた[ *DispatchCreateClose* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)ルーチンは、これらの I/O 関数コードの両方の Irp を処理できます。

作成要求の送信元のいずれか (場合によって、アプリケーションまたはサブシステム レベル ドライバー) に代わって、デバイスを表すファイル オブジェクトを識別するハンドルを取得または呼び出しでより高度なドライバーのユーザー モード サブシステムの試行から[ **IoGetDeviceObjectPointer** ](https://msdn.microsoft.com/library/windows/hardware/ff549198)または[ **IoAttachDevice**](https://msdn.microsoft.com/library/windows/hardware/ff548294)します。

相互の終了要求は、ドライバーのデバイス オブジェクトに関連付けられたファイル オブジェクトのハンドルのユーザー モード サブシステムの終了から発生します。

これらの要求の各機能は、本質的に同期します。

 

 



