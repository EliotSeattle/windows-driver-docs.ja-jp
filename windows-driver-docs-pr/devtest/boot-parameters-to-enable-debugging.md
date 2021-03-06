---
title: デバッグを有効にするためのブート パラメーター
description: デバッグを有効にするためのブート パラメーター
ms.assetid: acbe2fcd-6f8f-49c8-9de6-1617a1723cf5
keywords:
- WDK のブート パラメーター
- ブート エントリ パラメーター WDK
- カーネル デバッグ サポート WDK ブート オプション
- ローカル デバッグ WDK のブート パラメーター
- 1 台のコンピューター デバッグ WDK ブート パラメーター
- WDK のブート パラメーターをデバッグ ケーブル
- IEEE 1394 ケーブルの WDK のブート パラメーター
- 1394 接続 WDK のブート パラメーター
- USB 2.0 のデバッグ接続 WDK のブート パラメーター
- ヌル モデム ケーブル WDK のブート パラメーター
ms.date: 04/23/2019
ms.localizationpriority: medium
ms.openlocfilehash: c7191a7c182ae2e85706f9810de06b21924107c6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371654"
---
# <a name="boot-parameters-to-enable-debugging"></a>デバッグを有効にするためのブート パラメーター


## <span id="ddk_boot_parameters_to_enable_debugging_tools"></span><span id="DDK_BOOT_PARAMETERS_TO_ENABLE_DEBUGGING_TOOLS"></span>


カーネル デバッグ接続が確立されると、システムでの実行、カーネル デバッガー制御できます。 また、バグ チェックが発生またはカーネル モードのプログラムがデバッガーと通信すると、コンピューターの応答を待機カーネル デバッガーから続行することです。

ブート パラメーターを使用して構成できる 4 つの基本的なデバッグ方法はあります。

- 1 台のコンピューター (ローカル) のデバッグ

- ヌル モデム ケーブルを使用したデバッグ

- (Microsoft Windows 7 または Windows の以降のバージョン、ターゲット コンピューターとホスト コンピューターの両方が実行) の場合のみ、IEEE 1394 ケーブルでのデバッグ

- (Microsoft Windows 7 または Windows の以降のバージョン、ターゲット コンピューターとホスト コンピューターの両方が実行) の場合のみ、USB 2.0 デバッグ ケーブルでのデバッグ

### <a name="span-idbootoptionforlocaldebugginginwindowsvistaandlaterspanspan-idbootoptionforlocaldebugginginwindowsvistaandlaterspanboot-option-for-local-debugging-in-windows"></a><span id="boot_option_for_local_debugging_in_windows_vista_and_later"></span><span id="BOOT_OPTION_FOR_LOCAL_DEBUGGING_IN_WINDOWS_VISTA_AND_LATER"></span>Windows でのローカル デバッグのブート オプション

1 台のコンピューターのカーネル デバッグを有効にする、BCDEdit を使用して、 **/debug**ブート オプション。

BCDEdit を使用するには、管理者特権でコマンド プロンプト ウィンドウを開きます (を右クリックして**コマンド プロンプト**クリック**管理者として実行**ショートカット メニューから)。

**/Debug**オプションには、次の構文。

```console
bcdedit /debug [{ID}] { on | off }
```

**{** <em>ID</em> **}** ブート エントリ、{DEFAULT} などの OS の既定のブート エントリに関連付けられている ID です。 指定しない場合、 **{** <em>ID</em> **}** のコマンドは、現在アクティブになっているオペレーティング システムを変更します。 ブート エントリの識別子を持つ操作の詳細については、次を参照してください。[ブート オプション識別子](boot-options-identifiers.md)します。

次のコマンドは、カーネルの現在の Windows オペレーティング システムのブート エントリのデバッグを有効にします。

```console
bcdedit /debug on
```

使用することができます、 **bcdedit/enum**を現在のブート エントリとその設定を表示するコマンド。

詳細については、次を参照してください。 [ **BCDEdit/debug**](https://docs.microsoft.com/windows-hardware/drivers/devtest/bcdedit--debug)します。

### <a name="span-idbootoptionstodebugwithanullmodemcableinwindowsvistaandlatspanspan-idbootoptionstodebugwithanullmodemcableinwindowsvistaandlatspanboot-options-to-debug-with-a-null-modem-cable-in-windows"></a><span id="boot_options_to_debug_with_a_null_modem_cable_in_windows_vista_and_lat"></span><span id="BOOT_OPTIONS_TO_DEBUG_WITH_A_NULL_MODEM_CABLE_IN_WINDOWS_VISTA_AND_LAT"></span>Windows でヌル モデム ケーブルを使用してデバッグするブート オプション

Windows でヌル モデム ケーブルを使用したデバッグを有効にするには、BCDEdit を使用し、「シリアル」デバッグ接続の種類を設定します。 使用してグローバルに設定することができます、 [ **BCDEdit/dbgsettings** ](https://docs.microsoft.com/windows-hardware/drivers/devtest/bcdedit--dbgsettings)コマンドに続けて**シリアル**を使用して特定のブート エントリの設定も、 [ **BCDEdit/set** ](https://docs.microsoft.com/windows-hardware/drivers/devtest/bcdedit--set)コマンドに続けて**debugtype serial**します。 使用することも必要があります、 [ **BCDEdit/debug** ](https://docs.microsoft.com/windows-hardware/drivers/devtest/bcdedit--debug)グローバルまたは目的のオペレーティング システムのカーネル デバッグを有効にするコマンド。

BCDEdit が使用されていない場合、既定のグローバルのデバッグ設定は COM1 との 115,200 ボー レートを使用して、シリアル通信です。

現在の設定を表示するには、次のコマンドを使用します。

```console
bcdedit /dbgsettings

debugtype               Serial
debugport               1
baudrate                115200
```

BCDEdit を使用するには、管理者特権でコマンド プロンプト ウィンドウを開きます (を右クリックして**コマンド プロンプト**クリック**管理者として実行**ショートカット メニューから)。

グローバルのデバッグの設定をシリアル通信を設定するには、次の構文を使用します。

**bcdedit/dbgsettings シリアル** \[ **debugport:** <em>ポート</em>\] \[ **baudrate:** *ボー*\]

次の例では、グローバルのデバッグ設定とシリアル通信を指定する方法を示します。

```console
bcdedit /dbgsettings serial debugport:1 baudrate:115200
```

特定のブート エントリ、または現在のエントリのシリアル デバッグ設定を設定するには、次の構文を使用します。

**bcdedit /set** \[ **{** <em>ID</em> **}** \] **debugtype serial**

**bcdedit /set** \[ **{** <em>ID</em> **}** \] **debugport** *port*

**bcdedit /set** \[ **{** <em>ID</em> **}** \] **baudrate** *baud*

ない場合は **{** <em>ID</em> **}** を指定すると、現在アクティブなブート エントリを設定が適用されます。

次の例では、シリアル デバッグ設定を指定する方法、既定のブート エントリ。 デバッグの設定を有効にする必要があるには、コンピューターを再起動し、デバッグ用に構成したブート エントリを選択します。

```console
bcdedit /set debugtype serial
```

```console
bcdedit /set debugport 1
```

```console
bcdedit /set baudrate 115200
```

```console
bcdedit /debug on
```

使用することができます、 **bcdedit/enum**を現在のブート エントリとその設定を表示するコマンド。

詳細については、次を参照してください。 [ **BCDEdit/debug** ](https://docs.microsoft.com/windows-hardware/drivers/devtest/bcdedit--debug)と[ **BCDEdit/dbgsettings**](https://docs.microsoft.com/windows-hardware/drivers/devtest/bcdedit--dbgsettings)します。

### <a name="span-idbootparameterstodebugwitha1394cableinwindowsvistaandlaterspanspan-idbootparameterstodebugwitha1394cableinwindowsvistaandlaterspanboot-parameters-to-debug-with-a-1394-cable-in-windows"></a><span id="boot_parameters_to_debug_with_a_1394_cable_in_windows_vista_and_later"></span><span id="BOOT_PARAMETERS_TO_DEBUG_WITH_A_1394_CABLE_IN_WINDOWS_VISTA_AND_LATER"></span>Windows で 1394 ケーブルを使用してデバッグするブート パラメーター

Windows の IEEE 1394 ケーブルを使用したデバッグを有効にするには、BCDEdit を使用し、「1394」するデバッグ接続の種類を設定します。 使用してグローバルに設定することができます、 [ **BCDEdit/dbgsettings** ](https://docs.microsoft.com/windows-hardware/drivers/devtest/bcdedit--dbgsettings)コマンドに続けて**1394**を使用して特定のブート エントリの設定も、 [ **BCDEdit/set** ](https://docs.microsoft.com/windows-hardware/drivers/devtest/bcdedit--set)コマンドに続けて**debugtype 1394**します。 使用することも必要があります、 [ **BCDEdit/debug** ](https://docs.microsoft.com/windows-hardware/drivers/devtest/bcdedit--debug)グローバルまたは目的のオペレーティング システムのカーネル デバッグを有効にするコマンド。

BCDEdit を使用するには、管理者特権でコマンド プロンプト ウィンドウを開きます (を右クリックして**コマンド プロンプト**クリック**管理者として実行**ショートカット メニューから)。

1394 のデバッグの設定をグローバルに設定するには、次の構文を使用します。

**bcdedit /dbgsettings 1394** \[ **channel:** <em>channel</em> \]

次の例では、1394 デバッグのグローバル設定を指定する方法を示します。

```console
bcdedit /dbgsettings 1394 channel:32 
```

デバッグの設定を 1394 の特定のブート エントリの場合、または現在のエントリを設定するには、次の構文を使用します。

**bcdedit /set** \[ **{** <em>ID</em> **}** \] **debugtype 1394**

**bcdedit /set** \[ **{** <em>ID</em> **}** \] **channel** *channel*

場合、 **{** <em>ID</em> **}** が指定されていない、現在のブート エントリを設定が適用されます。

次の例では、特定のブート エントリの場合は、1394 デバッグ設定を指定する方法と使用方法を示しています、 **/debug**既定のブート エントリのカーネル デバッグを有効にするオプション。 デバッグの設定を有効にする必要があります、コンピューターの再起動をデバッグ用に構成したブート エントリを選択に注意してください。

```console
bcdedit /set debugtype 1394
```

```console
bcdedit /set channel 32
```

```console
bcdedit /debug on
```

使用することができます、 **bcdedit/enum**を現在のブート エントリとその設定を表示するコマンド。

詳細については、次を参照してください。 [ **BCDEdit/debug** ](https://docs.microsoft.com/windows-hardware/drivers/devtest/bcdedit--debug)と[ **BCDEdit/dbgsettings**](https://docs.microsoft.com/windows-hardware/drivers/devtest/bcdedit--dbgsettings)します。

### <a name="span-idbootparameterstodebugwithausb20debuggingcableinwindowsvisspanspan-idbootparameterstodebugwithausb20debuggingcableinwindowsvisspanboot-parameters-to-debug-with-a-usb-20-debugging-cable-in-windows"></a><span id="boot_parameters_to_debug_with_a_usb_2_0_debugging_cable_in_windows_vis"></span><span id="BOOT_PARAMETERS_TO_DEBUG_WITH_A_USB_2_0_DEBUGGING_CABLE_IN_WINDOWS_VIS"></span>Windows での USB 2.0 デバッグ ケーブルでデバッグするブート パラメーター

これらのバージョンの Windows での USB ケーブルを使用したデバッグを有効にするには、BCDEdit を使用し、"usb"デバッグ接続の種類を設定します。 使用してグローバルに設定することができます、 [ **BCDEdit/dbgsettings** ](https://docs.microsoft.com/windows-hardware/drivers/devtest/bcdedit--dbgsettings)コマンドに続けて**usb**を使用して特定のブート エントリの設定も、 [ **BCDEdit/set** ](https://docs.microsoft.com/windows-hardware/drivers/devtest/bcdedit--set)コマンドに続けて**debugtype usb**します。 使用することも必要があります、 [ **BCDEdit/debug** ](https://docs.microsoft.com/windows-hardware/drivers/devtest/bcdedit--debug)グローバルまたは目的のオペレーティング システムのカーネル デバッグを有効にするコマンド。

BCDEdit を使用するには、管理者特権でコマンド プロンプト ウィンドウを開きます (を右クリックして**コマンド プロンプト**クリック**管理者として実行**ショートカット メニューから)。

USB のデバッグ設定をグローバルに設定するには、次の構文を使用します。

**bcdedit /dbgsettings usb** \[**targetname:** <em>name</em>\]

次の例では、グローバルのデバッグ設定と USB を指定する方法を示します。

```console
bcdedit /dbgsettings usb targetname:U1
```

特定のブート エントリ、または現在のエントリは、usb デバッグの設定を設定するには、次の構文を使用します。

**bcdedit /set** \[ **{** <em>ID</em> **}** \] **debugtype usb**

**bcdedit /set** \[ **{** <em>ID</em> **}** \] **targetname** *name*\]

ない場合は **{** <em>ID</em> **}** を指定すると、現在のブート エントリを設定が適用されます。

次の例では、USB デバッグを特定のブート エントリの設定を指定する方法と使用方法を示しています、 **/debug**既定のブート エントリのカーネル デバッグを有効にするコマンド。 デバッグの設定を有効にする必要があります、コンピューターの再起動をデバッグ用に構成したブート エントリを選択に注意してください。

```console
bcdedit /set debugtype usb
```

```console
bcdedit /set targetname u2
```

```console
bcdedit /debug on
```

使用することができます、 **bcdedit/enum**を現在のブート エントリとその設定を表示するコマンド。

詳細については、次を参照してください。 [ **BCDEdit/debug** ](https://docs.microsoft.com/windows-hardware/drivers/devtest/bcdedit--debug)と[ **BCDEdit/dbgsettings**](https://docs.microsoft.com/windows-hardware/drivers/devtest/bcdedit--dbgsettings)します。

### <a name="span-idbootparameterstodebugthebootprocessinwindowsvistaandlaterspanspan-idbootparameterstodebugthebootprocessinwindowsvistaandlaterspanboot-parameters-to-debug-the-boot-process-in-windows"></a><span id="boot_parameters_to_debug_the_boot_process_in_windows_vista_and_later"></span><span id="BOOT_PARAMETERS_TO_DEBUG_THE_BOOT_PROCESS_IN_WINDOWS_VISTA_AND_LATER"></span>Windows のブート プロセスをデバッグするブート パラメーター

ブート デバッグを有効にするには使用、 [ **BCDEdit/bootdebug** ](https://docs.microsoft.com/windows-hardware/drivers/devtest/bcdedit--bootdebug)コマンドし、適切なブート コンポーネントを指定します。 Windows の起動後のカーネル デバッグを実行するには、使用する場合、 [ **BCDEdit/debug** ](https://docs.microsoft.com/windows-hardware/drivers/devtest/bcdedit--debug)もコマンド。

デバッグ接続を選択することも必要があります (、serial、1394、または USB)。 いずれかで表示できます、 [ **BCDEdit/dbgsettings** ](https://docs.microsoft.com/windows-hardware/drivers/devtest/bcdedit--dbgsettings)または[ **BCDEdit/set** ](https://docs.microsoft.com/windows-hardware/drivers/devtest/bcdedit--set)コマンドを通常のカーネル デバッグと同じようにします。

詳細については、次を参照してください。 [ **BCDEdit/bootdebug**](https://docs.microsoft.com/windows-hardware/drivers/devtest/bcdedit--bootdebug)します。
