---
title: IOleCvt 自動化インターフェイス
description: IOleCvt 自動化インターフェイス
MS-HAID:
- webfnc\_0ca4054a-768a-44b9-bb7e-84a5cb81349b.xml
- print.iolecvt\_automation\_interface
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: 286ab231-c215-45cc-b0da-97ec8adf2de1
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 01fba7e9303d79ef2962788508a46eaec4e3c6ea
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63382604"
---
# <a name="iolecvt-automation-interface"></a>IOleCvt 自動化インターフェイス

オートメーション インターフェイス、 **IOleCvt**オブジェクトは、さまざまな 1 つの形式から別の文字列の変換を実行する ASP Web ページを使用できます。 次のようなクラスがあります。

-   Unicode から ANSI への変換

-   ANSI から Unicode への変換

-   Unicode から utf-8 (UCS Transformation Format 8) への変換

-   別のコード ページを使用して Unicode に 1 つのコード ページを使用して Unicode からの変換

ほとんどのアプリケーションでは、今すぐデータの文字エンコーディングを Unicode (utf-16) を使用して、いくつかの Windows デスクトップ アプリケーションは、Windows コード ページに基づいて文字セットを使用します。 コード ページは、国際文字を ANSI 文字のコードが 127 より大きい値に割り当てます。 コード ページに関する詳細については、Windows SDK のドキュメントを参照してください。

**IOleCvt**インターフェイスは、Windows 2000 以降をサポートします。

プログラム id を**IOleCvt**オブジェクトが OlePrn.OleCvt します。

ASP Web ページからプリンターへのアクセス方法の詳細については、次を参照してください。[インターネット印刷](https://docs.microsoft.com/windows-hardware/drivers/print/internet-printing)します。

「プロパティの取得」操作、 **IOleCvt**インターフェイスは次のセクションで説明します。

[IOleCvt プロパティの Get 操作](iolecvt-property-get-operations.md)
