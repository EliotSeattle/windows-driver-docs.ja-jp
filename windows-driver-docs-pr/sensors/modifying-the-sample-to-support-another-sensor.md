---
title: 別のセンサーをサポートするために、サンプルを変更します。
description: 別のセンサーをサポートするために、サンプルを変更します。
ms.assetid: E759E022-C1E6-4403-B3DC-82A269E04B93
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b0a93c6920e41868a0bfacb2c0a549faf6ab634a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551302"
---
# <a name="modify-the-sample-to-support-another-sensor"></a>別のセンサーをサポートするために、サンプルを変更します。


SpbAccelerometer サンプルでは、ADXL345 加速度計のドライバーを作成する方法を示します。 ドライバーは、1 つのセンサー (つまり、加速度計ではない) をサポートする場合は、修正、または置き換えるには、次のファイルと機能します。

| ファイル                    | 変更履歴                                                                                                                                                                                                                                                                                                                                                                             |
|-------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| SpbAccelerometer.inx    | ファイルの名前を変更します。 デバイスの名前を反映するように、デバイス名の文字列を更新します。 (検索し、「SPB の加速度計」および"SpbAccelerometer"のインスタンスを置き換えます)。そのハードウェアを必ず INF ファイル内の識別子に"ACPI"文字列が含まれています。                                                                                                                                      |
| SpbAccelerometer.asl    | ファイルの名前を変更します。 更新プログラム、 \_CRS セクション、デバイスに必要な I2C と GPIO のリソースを指定できるようにします。                                                                                                                                                                                                                                                                    |
| Adxl345.h               | ファイルの名前を変更します。 デバイスが、ADXL345 と似ており、レジスタのセットをサポートし、対応する読み取りと書き込み操作、レジスタ、および操作にマップされるように、このファイルを変更する場合は、デバイスでサポートします。 デバイスは、レジスタ、または読み取り/書き込み操作をサポートしていない、このファイルを削除します。                                                             |
| AccelerometerDevice.h   | ファイルの名前を変更します。 デバイスの機能に対応するメソッドと ADXL345 の特定の機能に対応するプライベート メソッドを置き換えます。 たとえば、デバイスがレジスタと割り込みを使用しない場合は、ReadRegister、WriterRegister、ConnectInterrupt メソッドを置き換えます。 不要になったデバイスの機能を反映するプライベート メンバーを置き換えます。 |
| AccelerometerDevice.cpp | ファイルの名前を変更します。 ヘッダー ファイルから抜粋したが、メソッドを削除し、デバイスの機能に対応する新しいメソッドの定義を挿入します。                                                                                                                                                                                                                  |

 

 

 



