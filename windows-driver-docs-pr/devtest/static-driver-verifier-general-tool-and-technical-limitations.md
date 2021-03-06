---
title: 静的ドライバー検証ツールの一般的なツールと技術的な制限
description: 静的ドライバー検証ツールの一般的なツールと技術的な制限
ms.assetid: d263dee5-2408-4772-96d7-d1895a445fab
keywords:
- 静的ドライバー検証ツール WDK、制限事項
- StaticDV WDK、制限事項
- SDV WDK、制限事項
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 143276aaa7c9235343a78a641c0432a5eedfe7f2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839315"
---
# <a name="static-driver-verifier-general-tool-and-technical-limitations"></a>静的ドライバー検証ツールの一般的なツールと技術的な制限


SDV には、次の一般的な制限があります。

-   SDV は一度に1つのドライバーのみを検証し、ドライバーは、WDM、KMDF、NDIS、または Storport のいずれかのドライバーモデルに従って完全に検証する必要があります。 サポートされているドライバーの詳細については、「[静的ドライバーの検証ツールがドライバーまたはライブラリをサポートするかどう](determining-if-static-driver-verifier-supports-your-driver-or-library.md)かを判断する」を参照してください。

-   上記のいずれかのカテゴリに分類されていないドライバーは、検証可能で、分析中に失敗する可能性のある規則に重大な制限を適用します。

-   ドライバープロジェクトファイルとソースコードは、ローカルコンピューター上に存在している必要があります。 ドライバーをリモートで検証することはできません。

-   SDV は、英語 (米国) のロケールでインストールされます。 その結果、ロケールに依存する要素 (文字列の書式設定など) では、英語 (米国) のバリアントが使用されます。 この制限は、SDV が英語 (米国) 以外のローカライズ版の Windows にインストールされている場合でも存在します。

SDV[検証エンジン](verification-engine.md)には、一部のドライバーコードが正しく解釈されないようにするための技術的な制限があります。 具体的には、検証エンジンは次のようになります。

-   では、32ビット整数が32ビットに制限されていることは認識されません。 その結果、オーバーフローまたはアンダーフローエラーは検出されません。

-   **Static**キーワードを使用してエントリポイントを宣言するドライバーが正しく処理されていることを確認します。 ただし、静的なエントリポイントが認識されるようにするために、SDV は静的関数に対して[sdv .h](sdv-map-h.md)ファイルを変更する必要があります。たとえば、静的なエントリポイントを宣言すると、次のようになります。

    ```
    static DRIVER_UNLOAD Unload;
    ```

    Sdv には、*楽しい\_DriverUnload*の通常のエントリは含まれません。

    ```
    #define fun_DriverUnload Unload
    ```

    代わりに、関数名が破損していることがわかります。

    ```
      #define fun_DriverUnload sdv_static_function_Unload_1
    ```

    これは、複数のモジュールが*Unload*という名前の静的関数を持つ可能性があるために必要です。 競合の可能性を回避するために、名前が破損しています。

-   では、エクスポートドライバーに定義されているドライバーのディスパッチまたはドライバーコールバック関数を解釈できません。エクスポートドライバーには、ドライバーのディスパッチ機能を非表示にするモジュール定義 (.def) ファイルがあります。 この問題を回避するには、モジュール定義 (.def) ファイルのエクスポートセクションに driver dispatch 関数を追加します。

-   この関数への次の参照が同じ*コンパイル単位*内にない場合、関数のロールの種類を正常に検出できません。

    -   関数の宣言。
    -   関数の定義。
    -   ドライバーエントリポイントまたはコールバック関数への関数の割り当て。

    このソースコードファイルに含まれるソースコードファイルとその他のソースファイルの最小セットとして、*コンパイル単位*がここで定義されます。

    SDV によって関数ロールの種類が検出されない場合、SDV は、この関数から発信されたトレースを検証しません。

    たとえば、ドライバーが[*Evtdriverdeviceadd*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)関数をファイル mydriver .c に定義 (または実装) する場合などです。 このコンパイル単位 (または、mydriver. c に含まれるすべての .h ファイル) には、 *Evtdriverdeviceadd*関数の関数ロール型の宣言が含まれている必要があります。

-   構造化例外処理を解釈しません。 **Try/except**ステートメントの場合、sdv は、例外がスローされなかったかのように保護されたセクションを分析します。 は、式または例外ハンドラーコードを分析しません。

    ```
    // The try/except statement
    __try 
    {
       // guarded section
    }
    __except ( expression )
    {
       // exception handler
    } 
    ```

    **Try/finally**ステートメントの場合、sdv は保護されたセクションを分析し、例外がスローされない場合と同様に終了ハンドラーを分析します。

    ```
    // The try/finally statement
    __try {
       // guarded section
    }
    __finally {
       // termination handler
    }
    ```

    **Try/except**ステートメントと**try/finally**ステートメントの両方について、sdv は**leave**ステートメントを無視します。

    Try **/except**ステートメントと**try/finally**ステートメントの両方で、 **try**ブロックからジャンプすると、 **except**または**finally**ステートメントの分析ができなくなります。 Leave ステートメントを使用できるように書き換える方法の詳細については、「コンパイラの警告[C6242](https://go.microsoft.com/fwlink/p/?linkid=153317)」を参照してください。

-   ポインター演算を無視します。 たとえば、ポインターがインクリメントまたはデクリメントされた状況を見逃すことがあります。 この制限により、偽陽性と偽陽性の結果が返される可能性があります。

-   共用体を無視します。 ほとんどの場合、**共用**体は**構造体**として扱われ、偽陽性または誤否定になる可能性があります。

-   キャスト操作を無視します。したがって、recasting によって解決されるエラーと、キャストによって発生するエラーの両方を見逃すことがあります。 たとえば、エンジンは、文字として再キャストされている整数がまだ整数値を保持していると想定しています。

-   は、関数ポインター配列である配列のみを初期化します。 SDV は警告を発行し、配列初期化子を最初の1000要素に圧縮します。 その他の配列型では、最初の要素のみが初期化されます。

-   配列で初期化されたオブジェクトのコンストラクターは呼び出されません。 たとえば、次のコードスニペットでは、SDV がコンストラクターを呼び出さないため、 *x*は10に設定されません。

    ```
    class A
    {
    public:
        A() {
          x = 10;
        }

        int x;
    };

    void main()
    {
        A a[1];
    }
    ```

-   SDV では、コンストラクターを使用した配列の初期化はサポートされていません。 たとえば、次のコードスニペットでは、P のコンストラクターは main 関数では正しく呼び出されず、配列 p2 の要素は初期化されません。
    ```
    class P
    {
    public:
        P() : x(0) {}
        int x;
    };

    void main()
    {
        P* p1 = new P[1];

        P p2[1] = {P()};
    }
    ```

-   SDV はプリコンパイル済みヘッダーを無視します。 コンパイルを高速化するためだけにプリコンパイル済みヘッダーを使用するドライバーは、SDV でコンパイルが遅くなります。 コンパイルを成功させるためにプリコンパイル済みヘッダーを使用する必要があるドライバーは、SDV ではコンパイルされません。

-   **Rtlゼロメモリ**または**NdisZeroMemory**の呼び出しによって作成されたいくつかの型の暗黙的な割り当てを推論することはできません。 エンジンは、メモリをゼロに初期化するためのベストエフォート分析を実行しますが、その型を識別できる場合に限ります。 その結果、これらの関数に依存するコードがメモリを初期化すると、コードパスによって誤欠陥が発生する可能性があります。

-   では、KMDF ドライバーへの i/o 要求の手動ディスパッチを追跡できるようにするメモリモデルはサポートされていません。 エンジンは、フレームワークに依存するメソッドのみをサポートしています。このメソッドは、i/o 要求をドライバーに配信します (順次または並行ディスパッチの場合)。

-   では、比較に float データ型を使用することはできません。 この技術的な制限により、偽陽性と偽陽性の結果が生成される可能性があります。

-   SDV では、仮想継承または仮想関数はサポートされていません。 SDV は、仮想関数によるコードパスに従う欠陥を生成しません。これにより、実際の欠陥が失われる可能性があります。 仮想継承は通常の継承と同様に扱われ、偽の欠陥や実際の欠陥が失われる可能性があります。

 

 





