---
title: 印刷フィルター パイプライン サービスにデバッガーを接続する
description: 印刷フィルター パイプライン サービスにデバッガーを接続する
ms.assetid: d2e032f8-bdce-415a-8cf4-d9816b7c9de5
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 93f632312ddd5a85fa8f1c8620d2224b4333172c
ms.sourcegitcommit: 5decd841b9fcd9f4245c96ee0c028894c1e19f94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/22/2019
ms.locfileid: "67325929"
---
# <a name="attaching-a-debugger-to-the-print-filter-pipeline-service"></a>印刷フィルター パイプライン サービスにデバッガーを接続する


XPSDrv ドライバーのフィルターは、印刷フィルター パイプライン サービス (printfilterpipelinesvc.exe) によってホストされます。 Microsoft Windows デバッガー (WinDbg) を印刷フィルター パイプラインのサービスにアタッチする場合は、これを行う 2 つの基本的な方法があります。

1.  コマンドラインから WinDbg を使用して、プロセスを開始します。

2.  WinDbg を既存のプロセスにアタッチします。

2 番目のオプションを使用して、WinDbg をプロセスにアタッチする必要があります、印刷スプーラーによってフィルター パイプラインのホストを開始する必要があります。 ただし、フィルター パイプラインのホストは、永続的なできない可能性があります。 アプリケーションは、印刷キューにジョブを送信して、ジョブが完了したらすぐに、サービスが終了したときに、サービスの新しいインスタンスが開始されます。 印刷ジョブを送信した後、デバッグしようとしているフィルターがフィルターのスタートアップや初期化コードをデバッグする場合に特に、実行を開始する前に、WinDbg を printfilterpipelinesvc.exe にアタッチする困難な場合があります。

この問題を回避するには、容量を変更できます時間、その printfilterpipelinesvc.exe では、印刷ジョブが完了したらが引き続き発生します。 値がにより制御されること、 **PipelineHostTimeout** 、HKEY @property\_ローカル\_マシン\\システム\\CurrentControlSet\\コントロール\\レジストリ キーを印刷します。

フィルター パイプラインのサービスのタイムアウト値を変更するのにには、次の手順を使用します。

1.  Microsoft レジストリ エディター (RegEdit) を実行し、HKEY に\_ローカル\_マシン\\システム\\CurrentControlSet\\コントロール\\印刷します。

2.  追加、 **PipelineHostTimeout** REG\_DWORD 値が存在しない場合は、キーをします。

3.  設定**PipelineHostTimeout**ミリ秒のタイムアウト値にします。 ブレークポイントを設定してプロセスをアタッチする十分な時間を持たせるための十分な大きさの値を設定します。 たとえば、1.5 分のタイムアウト値にする場合は、設定**PipelineHostTimeout** 90000 にします。

設定した後、 **PipelineHostTimeout**値には、次の手順を使用して、パイプラインのフィルター サービスに WinDbg をアタッチします。

1.  WinDbg を昇格された特権で実行しますが、プロセスにアタッチできません。

2.  ドライバーに印刷ジョブを送信し、完了するまで待機します。 フィルター パイプラインのサービスでは、指定したタイムアウト値を実行し続けます。

3.  WinDbg ファイル メニューから、プロセスへのアタッチを選択します。

4.  ダイアログ ボックスのプロセスにアタッチ、printfilterpipelinesvc.exe を選択し、[ok] をクリックします。 プロセスは、「アクセスが拒否されました」と表示されて場合、は、おそらく WinDbg が昇格した特権で実行されていないことを意味します。

5.  必要に応じて、ブレークポイントを設定します。

6.  印刷ジョブを再送信します。

フィルターのホスト プロセスは、最初のブレークポイントでデバッガーを中断する必要がありますか、どちらか早い、最初の検証が停止します。 そこから、コードをステップ実行、変数を調べたりおよびにすることができます。

 

 




