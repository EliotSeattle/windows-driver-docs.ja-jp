---
title: クライアント側レンダリングの既知の問題
description: クライアント側レンダリングの既知の問題
ms.assetid: ad17639d-6671-466b-8f72-e635e79fd1cc
keywords:
- クライアント側のレンダリング WDK の印刷、既知の問題
ms.date: 01/24/2019
ms.localizationpriority: medium
ms.openlocfilehash: 5341cd48c106547511308f8abb532bb59540ad15
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63388128"
---
# <a name="known-issues-with-client-side-rendering"></a>クライアント側レンダリングの既知の問題

クライアント側のレンダリング既定では、すべてのドライバーの有効なため、ほとんどのプリンター ドライバーに透過的であり、ユーザーに明確な特典を提供します。 ほとんどのプリンター ドライバーでは、この機能を有効になっている問題は発生しません。

ただし、プリンタ ドライバに問題が発生した場合は、クライアント側のレンダリング機能を無効にすることができます、プリンター ドライバーは、以前のバージョンの Windows オペレーティング システムのように、プリント サーバーの印刷ジョブを表示します。 システム管理者には、サーバーのグループ ポリシーを常にレンダリングの印刷ジョブを使用してクライアント側のレンダリングも無効にします。

> [!NOTE]
> クライアント側のレンダリング機能を無効にすると、印刷ジョブの表示は、プリント サーバー、プリント サーバーのパフォーマンスに悪影響を移動します。

ドライバー パッケージ内にインストールされているプリンター ドライバーでは、クライアント側のレンダリングの問題はありません。

次の一覧では、クライアント側のレンダリングに関する既知の問題のいくつかについて説明します。

- プリンター ドライバーがカスタムのプリント プロセッサを使用しますが、プリント プロセッサがクライアント コンピューターにインストールされていない場合、クライアント側のレンダリングが自動的に無効にします。

  場合によっては、ドライバー パッケージとして構成されていないプリンター ドライバーのプリント プロセッサがインストールされないクライアント コンピューターのポイント アンド プリントの中にします。 印刷スプーラで問題が検出された場合は、その印刷キューのクライアント側のレンダリングが無効になります。 この問題を回避するには、プリンター ドライバーをドライバー パッケージを作成します。

- プリント プロセッサがエラーを返した場合は、印刷キューのクライアント側のレンダリングが無効です。

  印刷キューのクライアント側のレンダリングを無効にした後、印刷スプーラーは、サーバー側のレンダリングを使用して印刷ジョブを再試行します。 印刷キューのクライアント側のレンダリングを無効にした後、印刷キューが不要になったあるオフライン印刷などのクライアント側のレンダリングの利点のいずれかに注意してください。

- プリンターの構成データは、非標準の構成データを使用するプリンター ドライバーの完了でない可能性があります。

  ポイント アンド プリントが、保存して、このデータの通信を独自の方法を使用するプリンター ドライバーの完全なプリンターの構成データは転送されません。 この問題を修正するを使用して、 **SetPrinterData**または**SetPrinterDataEx**プリンター構成データとを使用して格納する関数、 **GetPrinterData**または**GetPrinterDataEx**プリンター構成データを回収する関数。 これらの関数の詳細については、Microsoft Windows SDK のドキュメントを参照してください。

- ドライバーの不一致によるクライアント側のレンダリングします。

  サーバーがあるクライアント コンピューターに別のバージョンのプリンタ ドライバがある場合、プリンター ドライバーの不一致が存在します。 通常、プリンターのドライバーが一致しない場合は、ポイント アンド プリントは、サーバー上のプリンタ ドライバの一致するようにクライアント コンピューターのプリンター ドライバーを更新します。 状況によっては、プリント サーバー上のプリンター ドライバーのバージョンに一致しない印刷ドライバーのバージョンを使用するクライアント コンピューターで印刷キューを必要があります。 たとえば、クライアント コンピューターのプリンター ドライバーを更新するには、ポイント アンド プリントをしないする可能性があります。

  - クライアント コンピューターで実行すると、プリント サーバー上のプリンタ ドライバの互換性の問題がある場合
  - 生成されるネットワーク トラフィックを削減するには、とポイント アンド プリントのダウンロード新しいプリンタ ドライバ。
  - デバッグまたはテストする場合。

  ポイント アンド プリントを防ぐことができます、プリンター ドライバーと既にインストールされているクライアント コンピューターの代わりに最適なドライバーを使用するクライアント コンピューターが強制的にダウンロードします。 この動作を選択するには、HKLM の値を設定\\システム\\CurrentControlSet\\コントロール\\印刷\\*PrinterName*\\PrinterDriverData\\DriverPolicy レジストリ キー、プリンター ドライバーの名前。 置換*PrinterName*プリント サーバーから使用できるプリンター ドライバーではなくローカルで利用可能なプリンター ドライバーを使用する印刷キューの名前に置き換えます。 このレジストリ キーに入力するドライバー名は、クライアント コンピューターにインストールされているかの使用可能なインストールは、互換性のあるプリンタ ドライバの名前である必要があります。

  作成することも、プリンター接続のプリンター ドライバーの不一致によりプログラムで呼び出すことによって**AddPrinterConnection2**、プリンターの設定\_接続\_不一致フラグとの名前を指定します。プリンターのプリンター ドライバー\_接続\_情報\_1 構造体、 *pConnectionInfo*引数の参照。 **AddPrinterConnection2** Windows SDK のドキュメントに記載されています。

- Windows 8 以降では、クライアント側のレンダリングが自動的に無効に EMFDespoolingSetting 値がレジストリに存在しないと、クライアント コンピューターのプロファイルはモバイル プラットフォーム。

  クライアントが、ラップトップやタブレット デバイスなどのモバイル プラットフォームの場合は、電源消費量、スプーラーの保存を自動的に有効にするを無効にクライアント側のレンダリングこの値がレジストリに存在しない場合。 印刷キューの EMFDespoolingSetting 値を 0 に設定する SetPrinterData を呼び出すことによって、ドライバーで明示的にモバイル プラットフォーム用のクライアント側のレンダリングを有効にできます。

  コンピューターが msinfo32.exe を使用して、モバイルまたはデスクトップのプロファイルとして構成されているかどうかを確認できます。

  ![msinfo32.exe プロファイルのスクリーン ショット](images/emfdespoolingsetting.png)

テスト中に、クライアント側のレンダリング機能が原因となった可能性がありますが、プリンター ドライバーの問題を検出場合、ドライバーのクライアント側のレンダリングを無効にできます。 呼び出すことによって、ドライバーでクライアント側のレンダリングを無効にできます**SetPrinterData**印刷キューの EMFDespoolingSetting 値を 1 に設定します。 この値は、サーバー上の印刷ジョブを表示するために、印刷キューに接続するすべてのクライアントになります。
