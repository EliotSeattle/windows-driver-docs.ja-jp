---
title: GetDisplayConfigBufferSizes の概要とシナリオ
description: GetDisplayConfigBufferSizes の概要とシナリオ
ms.assetid: b0d14ba7-fe61-49e9-81c5-097e6e07a51a
keywords:
- Windows 7 の WDK の表示、CCD Api、GetDisplayConfigBufferSizes 接続が表示されます。
- WDK の Windows Server 2008 R2 の表示、CCD Api、GetDisplayConfigBufferSizes 接続が表示されます。
- Windows 7 の WDK の表示、CCD Api、GetDisplayConfigBufferSizes 構成が表示されます。
- 構成するには、WDK Windows Server 2008 R2 の表示、CCD Api、GetDisplayConfigBufferSizes が表示されます。
- CCD WDK Windows 7 の概念の表示、GetDisplayConfigBufferSizes
- CCD 概念 WDK Windows Server 2008 R2 の表示、GetDisplayConfigBufferSizes
- GetDisplayConfigBufferSizes WDK Windows 7 の表示
- GetDisplayConfigBufferSizes WDK Windows Server 2008 R2 の表示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cd7f0b58de1cdd9fba79e238ffa530e4e439b16d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379985"
---
# <a name="getdisplayconfigbuffersizes-summary-and-scenarios"></a>GetDisplayConfigBufferSizes の概要とシナリオ


このセクションでは、Windows 7 以降および Windows Server 2008 R2 以降のバージョンの Windows オペレーティング システムにのみ適用されます。

次のセクションでは、呼び出し元が使用する方法を要約[ **GetDisplayConfigBufferSizes** ](https://docs.microsoft.com/windows/desktop/api/winuser/nf-winuser-getdisplayconfigbuffersizes) CCD 関数を使用するためのシナリオを提供**GetDisplayConfigBufferSizes**します。

### <a name="span-idgetdisplayconfigbuffersizessummaryspanspan-idgetdisplayconfigbuffersizessummaryspangetdisplayconfigbuffersizes-summary"></a><span id="getdisplayconfigbuffersizes_summary"></span><span id="GETDISPLAYCONFIGBUFFERSIZES_SUMMARY"></span>GetDisplayConfigBufferSizes の概要

呼び出し元が使用できる[ **GetDisplayConfigBufferSizes** ](https://docs.microsoft.com/windows/desktop/api/winuser/nf-winuser-getdisplayconfigbuffersizes)を呼び出し元が必要とする情報を取得する、 [ **QueryDisplayConfig** ](https://docs.microsoft.com/windows/desktop/api/winuser/nf-winuser-querydisplayconfig)CCD 関数。

### <a name="span-idgetdisplayconfigbuffersizesscenariosspanspan-idgetdisplayconfigbuffersizesscenariosspangetdisplayconfigbuffersizes-scenarios"></a><span id="getdisplayconfigbuffersizes_scenarios"></span><span id="GETDISPLAYCONFIGBUFFERSIZES_SCENARIOS"></span>GetDisplayConfigBufferSizes シナリオ

[**GetDisplayConfigBufferSizes** ](https://docs.microsoft.com/windows/desktop/api/winuser/nf-winuser-getdisplayconfigbuffersizes)呼び出す前に必ず呼び出される[ **QueryDisplayConfig**](https://docs.microsoft.com/windows/desktop/api/winuser/nf-winuser-querydisplayconfig)します。

 

 





