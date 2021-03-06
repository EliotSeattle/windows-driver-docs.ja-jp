---
title: 過去 28 日以内に WU がダウンロードの成功を報告したマシンの割合
description: この測定値は、28 日間のスライディング ウィンドウからのテレメトリを、Windows Update からダウンロードの成功が報告されたマシンの割合に集計したものです
ms.topic: article
ms.date: 02/28/2020
ms.localizationpriority: medium
ms.openlocfilehash: 49b87ebde647736dc73821f31946517138ce92e2
ms.sourcegitcommit: 774d42aa3392ae88f4890d901dbd3e8945cb2658
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/24/2020
ms.locfileid: "82138649"
---
# <a name="percent-of-machines-that-windows-update-wu-reported-a-successful-download-within-the-last-28-days"></a>過去 28 日以内に Windows Update (WU) がダウンロードの成功を報告したマシンの割合

## <a name="description"></a>説明

過去 28 日以内に WU がダウンロードの成功を報告したマシンの割合
 
Windows Update エラー コードの詳細については次を参照してください。
* [コンポーネント別の Windows Update エラーコード](https://docs.microsoft.com/windows/deployment/update/windows-update-error-reference)
* [Windows Update の一般的なエラーと軽減策](https://docs.microsoft.com/windows/deployment/update/windows-update-errors)

## <a name="measure-attributes"></a>測定値の属性

|属性|値|
|----|----|
|**オーディエンス**|小売と内部関係者|
|**期間**|28 日間のスライディング ウィンドウ|
|**測定基準**|マシンの集計|
|**最小インスタンス**|100|
|**合格基準**|95% 以上|
|**測定 ID**|24186432|

## <a name="calculation"></a>計算

WU がダウンロードの成功を報告したマシンの数 (status == 0) / 

WU のダウンロードを試行したマシンの数
