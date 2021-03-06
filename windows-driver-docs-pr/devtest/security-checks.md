---
title: セキュリティチェック
description: セキュリティチェック
ms.assetid: fca92bad-7bb8-4a30-b303-48fd54c20c42
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 205ac99627c83a5cfc3217e2e68477896d629d87
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840041"
---
# <a name="security-checks"></a>セキュリティチェック


ドライバーの検証ツールの [セキュリティチェック] オプションを使用すると、ドライバーは、セキュリティ上の脆弱性につながる可能性のある一般的なエラーを監視します。 このオプションは、Windows Vista 以降で使用できます。

具体的には、[セキュリティチェック] オプションでは、次のような不適切なドライバーの動作が検索されます。

- **ユーザーモードアドレスを持つカーネル ZwXxx ルーチンをパラメーターとして呼び出します。** ドライバーが**Zw * Xxx*** ルーチンを呼び出すと、ドライバーの検証ツールは、どのパラメーターもユーザーモードアドレスでないことを確認します。 **Zw * Xxx*** ルーチンを呼び出すと、現在の kprocessor\_モードが**kernelmode で**になり、そのルーチンに渡されたすべてのパラメーターがカーネルモードアドレスとして扱われます。 このため、ドライバーは、カーネル**Zw * Xxx*** ルーチンを呼び出す前に、アプリケーションから受信したユーザーモードバッファーを調査し、カーネルモードメモリ (たとえば、カーネルスタックに割り当てられているプールブロックやデータ構造) に配置する必要があります。 ドライバーは、 **Zw * Xxx*** ルーチンのパラメーターとして、ユーザーモードバッファーではなくキャプチャされたバッファーを使用する必要があります。

- **間違った形式の UNICODE\_文字列をパラメーターとして使用して、カーネル ZwXxx ルーチンを呼び出します。** ドライバーが任意の**Zw * Xxx*** ルーチンを呼び出すと、ドライバーの検証ツールは、UNICODE\_文字列値のすべてのパラメーターをチェックします。 このような文字列でドライバーの検証ツールによって検出される一般的なエラーは次のとおりです。
  -   **バッファーフィールドは、ユーザーモードのメモリを指します。**
  -   **長さまたは MaximumLength パラメーターが正しくありません。** たとえば、 *maximumlength* &lt;*長さ*です。 または、これらの値の一方または両方が奇数です。 これらの値はどちらも、Unicode 文字列を表すために使用されるバイト数を表すため、常にである必要があります。
- **正しくないオブジェクトを使用してカーネル ZwXxx ルーチンを呼び出すと、パラメーターとして属性構造\_れます。** ドライバーが任意の**Zw * Xxx*** ルーチンを呼び出すと、ドライバーの検証ツールは、オブジェクト\_属性構造であるパラメーターをチェックします。 属性構造パラメーター\_各オブジェクトのメンバーは、上記で説明したユーザーモードアドレスと UNICODE\_文字列値について同じチェックを受けます。

- **Irp&gt;Irp->requestormode と i/o 要求のパラメーターが矛盾しています。** **Irp&gt; irp->requestormode**が**kernelmode で**に設定されている場合、ドライバーの検証ツールは、I/o 要求パラメーター ( **irp-&gt;AssociatedIrp buffer**または**irp-&gt;UserBuffer**) がユーザーモードアドレスでないことを確認します。

Windows 7 以降では、任意のドライバーの検証ツールオプションを有効にすると、ドライバーの検証ツールによって次のドライバーの動作が確認されます。

**オブジェクト参照カウンターが0から1に変更されました。**
Windows カーネルオブジェクトマネージャーが、ファイルオブジェクトやスレッドオブジェクトなどのオブジェクトを作成すると、新しいオブジェクトの参照カウンターが1に設定されます。 [**Obreferenceobjectbypointer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obreferenceobjectbypointer)や[**Obreferenceobjectbypointer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obreferenceobjectbyhandle)などのシステム関数を呼び出すと、参照カウンターがインクリメントされます。 同じオブジェクトに対して[**ObDereferenceObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obdereferenceobject)を呼び出すたびに、参照カウンターがデクリメントされます。

参照カウンターが0の値に達すると、オブジェクトは解放されることになります。 オブジェクトマネージャーによってすぐに解放される場合もあれば、後で解放される場合もあります。 ドライバーの検証ツールは、同じオブジェクトの[**Obreferenceobjectbypointer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obreferenceobjectbypointer)と[**obreferenceobject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obfreferenceobject)への後続の呼び出しを確認します。 これらの呼び出しは、参照カウンターを0から1に変更します。これは、ドライバーが既に解放されているオブジェクトの参照カウンターをインクリメントしたことを意味します。 他のメモリ割り当てが破損する可能性があるため、この方法は常に正しくありません。

### <a name="span-idactivating_this_optionspanspan-idactivating_this_optionspanactivating-this-option"></a><span id="activating_this_option"></span><span id="ACTIVATING_THIS_OPTION"></span>このオプションをアクティブにする

1つまたは複数のドライバーの [セキュリティチェック] オプションをアクティブにするには、ドライバー検証マネージャーまたは Verifier コマンドラインを使用します。 詳細については、「[ドライバーの検証オプションの選択](selecting-driver-verifier-options.md)」を参照してください。

-   **コマンドラインの使用**

    コマンドラインでは、セキュリティチェックオプションは**ビット 8 (0x100)** で表されます。 セキュリティチェックをアクティブにするには、フラグ値0x100 を使用するか、フラグ値に0x100 を追加します。 例:

    ```
    verifier /flags 0x100 /driver MyDriver.sys
    ```

    このオプションは、コンピューターを再起動した後にアクティブになります。

    Windows Vista 以降では、 **/volatile**パラメーターをコマンドに追加することで、コンピューターを再起動しなくても、セキュリティチェックをアクティブ化および非アクティブ化することができます。 例:

    ```
    verifier /volatile /flags 0x100 /adddriver MyDriver.sys
    ```

    この設定は直ちに有効になりますが、コンピューターをシャットダウンまたは再起動すると失われます。 詳細については、「 [Volatile 設定の使用](using-volatile-settings.md)」を参照してください。

    [セキュリティチェック] オプションも、標準設定に含まれています。 例:

    ```
    verifier /standard /driver MyDriver.sys
    ```

-   **ドライバー検証マネージャーの使用**

    1.  ドライバー検証マネージャーを起動します。 コマンドプロンプトウィンドウで「 **Verifier** 」と入力します。
    2.  [**カスタム設定の作成] (コード開発者向け)** を選択し、 **[次へ]** をクリックします。
    3.  [**完全な一覧から個々の設定を選択]** を選択します。
    4.  **[セキュリティチェック]** を選択します。

    セキュリティチェック機能も、標準設定に含まれています。 ドライバー検証マネージャーでこの機能を使用するには、 **[標準設定の作成]** をクリックします。

 

 





