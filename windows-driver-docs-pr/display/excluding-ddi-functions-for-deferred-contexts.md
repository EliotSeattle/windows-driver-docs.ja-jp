---
title: 遅延コンテキスト DDI 関数を除外
description: 遅延コンテキスト DDI 関数を除外
ms.assetid: f6e7898a-7fb8-4a70-ab2e-3372a28db6f4
keywords:
- Direct3D のバージョン 11 WDK Windows 7 を表示する DDI 関数を除く、コンテキストの遅延
- Direct3D のバージョン 11 WDK Windows Server 2008 R2 表示、DDI 関数を除く、遅延のコンテキスト
- 遅延コンテキスト WDK Windows 7 の表示、DDI 関数を除く
- 遅延コンテキスト WDK Windows Server 2008 R2 の表示、DDI 関数を除く
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c8a7532626cab62b764fff86c4b813f36a74de0f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529146"
---
# <a name="excluding-ddi-functions-for-deferred-contexts"></a>遅延コンテキスト DDI 関数を除外


このセクションでは、Windows 7 以降および Windows Server 2008 R2 以降のバージョンの Windows オペレーティング システムにのみ適用されます。

マイクロソフトの Direct3D ランタイムがユーザー モードのディスプレイ ドライバーを呼び出すときに[ **CreateDeferredContext** ](https://msdn.microsoft.com/library/windows/hardware/ff540622)ドライバー遅延コンテキストを作成する関数は、ランタイムが呼び出すことができる関数を提供します。そのため、コンテキストを遅延しました。 ドライバーがのメンバー、 [ **D3D11DDI\_DEVICEFUNCS** ](https://msdn.microsoft.com/library/windows/hardware/ff542141)構造体、 **p11ContextFuncs**のメンバー、 [ **D3D11DDIARG\_CREATEDEFERREDCONTEXT** ](https://msdn.microsoft.com/library/windows/hardware/ff542044)へのポインターを構造体します。 ドライバーは、ドライバーと遅延のコンテキストの機能のサブセットのみが、イミディ エイト コンテキストを提供します。

ドライバーの次のメンバーを設定して遅延コンテキストの多くの関数を除外する[ **D3D11DDI\_DEVICEFUNCS** ](https://msdn.microsoft.com/library/windows/hardware/ff542141)または[ **D3D11\_1DDI\_DEVICEFUNCS** ](https://msdn.microsoft.com/library/windows/hardware/hh406443)に**NULL**:

```cpp
typedef struct D3D11DDI_DEVICEFUNCS {
...
  PFND3D10DDI_RESOURCEMAP  pfnStagingResourceMap;
  PFND3D10DDI_RESOURCEUNMAP  pfnStagingResourceUnmap;
  PFND3D10DDI_QUERYGETDATA  pfnQueryGetData;
  PFND3D10DDI_FLUSH  pfnFlush;
  PFND3D10DDI_RESOURCEMAP  pfnResourceMap;
  PFND3D10DDI_RESOURCEUNMAP  pfnResourceUnmap;
  PFND3D10DDI_RESOURCEISSTAGINGBUSY  pfnResourceIsStagingBusy;
  PFND3D11DDI_CALCPRIVATERESOURCESIZE  pfnCalcPrivateResourceSize;
  PFND3D10DDI_CALCPRIVATEOPENEDRESOURCESIZE  pfnCalcPrivateOpenedResourceSize;
  PFND3D10DDI_OPENRESOURCE  fnOpenResource;
  PFND3D11DDI_CALCPRIVATESHADERRESOURCEVIEWSIZE  pfnCalcPrivateShaderResourceViewSize;
  PFND3D10DDI_CALCPRIVATERENDERTARGETVIEWSIZE  pfnCalcPrivateRenderTargetViewSize;
  PFND3D11DDI_CALCPRIVATEDEPTHSTENCILVIEWSIZE  pfnCalcPrivateDepthStencilViewSize;
  PFND3D10DDI_CALCPRIVATEELEMENTLAYOUTSIZE  pfnCalcPrivateElementLayoutSize;
  PFND3D10_1DDI_CALCPRIVATEBLENDSTATESIZE  pfnCalcPrivateBlendStateSize;
  PFND3D10DDI_CALCPRIVATEDEPTHSTENCILSTATESIZE  pfnCalcPrivateDepthStencilStateSize;
  PFND3D10DDI_CALCPRIVATERASTERIZERSTATESIZE  pfnCalcPrivateRasterizerStateSize;
  PFND3D10DDI_CALCPRIVATESHADERSIZE  pfnCalcPrivateShaderSize;
  PFND3D11DDI_CALCPRIVATEGEOMETRYSHADERWITHSTREAMOUTPUT  pfnCalcPrivateGeometryShaderWithStreamOutput;
  PFND3D10DDI_CALCPRIVATESAMPLERSIZE  pfnCalcPrivateSamplerSize;
  PFND3D10DDI_CALCPRIVATEQUERYSIZE  pfnCalcPrivateQuerySize;
  PFND3D10DDI_CHECKFORMATSUPPORT  pfnCheckFormatSupport;
  PFND3D10DDI_CHECKMULTISAMPLEQUALITYLEVELS  pfnCheckMultisampleQualityLevels;
  PFND3D10DDI_CHECKCOUNTERINFO  pfnCheckCounterInfo;
  PFND3D10DDI_CHECKCOUNTER  pfnCheckCounter;
  PFND3D11DDI_CHECKDEFERREDCONTEXTHANDLESIZES  pfnCheckDeferredContextHandleSizes;
  PFND3D11DDI_CALCDEFERREDCONTEXTHANDLESIZE  pfnCalcDeferredContextHandleSize;
  PFND3D11DDI_CALCPRIVATEDEFERREDCONTEXTSIZE  pfnCalcPrivateDeferredContextSize;
  PFND3D11DDI_CREATEDEFERREDCONTEXT  pfnCreateDeferredContext;
  PFND3D11DDI_CALCPRIVATECOMMANDLISTSIZE  pfnCalcPrivateCommandListSize;
  PFND3D11DDI_CALCPRIVATETESSELLATIONSHADERSIZE  pfnCalcPrivateTessellationShaderSize;
  PFND3D11DDI_CALCPRIVATEUNORDEREDACCESSVIEWSIZE  pfnCalcPrivateUnorderedAccessViewSize;
  PFND3D11DDI_SETRESOURCEMINLOD  pfnSetResourceMinLOD;
} D3D11DDI_DEVICEFUNCS;
```

```cpp
typedef struct D3D11_1DDI_DEVICEFUNCS {
...
  PFND3D10DDI_RESOURCEMAP  pfnStagingResourceMap;
  PFND3D10DDI_RESOURCEUNMAP  pfnStagingResourceUnmap;
  PFND3D10DDI_QUERYGETDATA  pfnQueryGetData;
  PFND3D11_1DDI_FLUSH  pfnFlush;
  PFND3D10DDI_RESOURCEMAP  pfnResourceMap;
  PFND3D10DDI_RESOURCEUNMAP  pfnResourceUnmap;
  PFND3D10DDI_RESOURCEISSTAGINGBUSY  pfnResourceIsStagingBusy;
  PFND3D11DDI_CALCPRIVATERESOURCESIZE  pfnCalcPrivateResourceSize;
  PFND3D10DDI_CALCPRIVATEOPENEDRESOURCESIZE  pfnCalcPrivateOpenedResourceSize;
  PFND3D10DDI_OPENRESOURCE  fnOpenResource;
  PFND3D11DDI_CALCPRIVATESHADERRESOURCEVIEWSIZE  pfnCalcPrivateShaderResourceViewSize;
  PFND3D10DDI_CALCPRIVATERENDERTARGETVIEWSIZE  pfnCalcPrivateRenderTargetViewSize;
  PFND3D11DDI_CALCPRIVATEDEPTHSTENCILVIEWSIZE  pfnCalcPrivateDepthStencilViewSize;
  PFND3D10DDI_CALCPRIVATEELEMENTLAYOUTSIZE  pfnCalcPrivateElementLayoutSize;
  PFND3D11_1DDI_CALCPRIVATEBLENDSTATESIZE  pfnCalcPrivateBlendStateSize;
  PFND3D10DDI_CALCPRIVATEDEPTHSTENCILSTATESIZE  pfnCalcPrivateDepthStencilStateSize;
  PFND3D11_1DDI_CALCPRIVATERASTERIZERSTATESIZE  pfnCalcPrivateRasterizerStateSize;
  PFND3D11_1DDI_CALCPRIVATESHADERSIZE  pfnCalcPrivateShaderSize;
  PFND3D11_1DDI_CALCPRIVATEGEOMETRYSHADERWITHSTREAMOUTPUT  pfnCalcPrivateGeometryShaderWithStreamOutput;
  PFND3D10DDI_CALCPRIVATESAMPLERSIZE  pfnCalcPrivateSamplerSize;
  PFND3D10DDI_CALCPRIVATEQUERYSIZE  pfnCalcPrivateQuerySize;
  PFND3D10DDI_CHECKFORMATSUPPORT  pfnCheckFormatSupport;
  PFND3D10DDI_CHECKMULTISAMPLEQUALITYLEVELS  pfnCheckMultisampleQualityLevels;
  PFND3D10DDI_CHECKCOUNTERINFO  pfnCheckCounterInfo;
  PFND3D10DDI_CHECKCOUNTER  pfnCheckCounter;
  PFND3D11DDI_CHECKDEFERREDCONTEXTHANDLESIZES  pfnCheckDeferredContextHandleSizes;
  PFND3D11DDI_CALCDEFERREDCONTEXTHANDLESIZE  pfnCalcDeferredContextHandleSize;
  PFND3D11DDI_CALCPRIVATEDEFERREDCONTEXTSIZE  pfnCalcPrivateDeferredContextSize;
  PFND3D11DDI_CREATEDEFERREDCONTEXT  pfnCreateDeferredContext;
  PFND3D11DDI_CALCPRIVATECOMMANDLISTSIZE  pfnCalcPrivateCommandListSize;
  PFND3D11_1DDI_CALCPRIVATETESSELLATIONSHADERSIZE  pfnCalcPrivateTessellationShaderSize;
  PFND3D11DDI_CALCPRIVATEUNORDEREDACCESSVIEWSIZE  pfnCalcPrivateUnorderedAccessViewSize;
  PFND3D11DDI_SETRESOURCEMINLOD  pfnSetResourceMinLOD;
} D3D11DDI_DEVICEFUNCS;
```

 

 




