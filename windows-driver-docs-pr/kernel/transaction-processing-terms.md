---
title: トランザクション処理の用語
description: KTM の使用を開始する前に、次のような用語の定義を把握しておく必要があります。トランザクション、resource manager、トランザクションクライアント、トランザクションマネージャー、ログストリーム、参加リスト、およびトランザクション処理システムです。
Robots: noindex, nofollow
ms.assetid: c8a8806f-a228-4d02-9995-c8cf45e57935
keywords:
- カーネルトランザクションマネージャー WDK、用語
- KTM WDK、用語
- トランザクション WDK KTM、定義
- リソースマネージャー WDK KTM、定義
- トランザクションクライアント WDK KTM、定義
- トランザクションマネージャー WDK KTM、定義
- ログストリーム WDK KTM、定義
- 、WDK KTM、定義の参加
- トランザクション処理システム WDK KTM、定義
- TPS WDK KTM、定義
- トランザクション WDK KTM、用語
- トランザクションマネージャーの WDK KTM
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: bae9d3d11a3986f6eeb101f6cfddf278950c7f9a
ms.sourcegitcommit: b316c97bafade8b76d5d3c30d48496915709a9df
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/13/2020
ms.locfileid: "79242961"
---
# <a name="transaction-processing-terms"></a>トランザクション処理の用語


KTM の使用を開始する前に、次の用語の定義を把握しておく必要があります。[トランザクション](#ktm-term-transaction)、[リソースマネージャー](#ktm-term-resource-manager)、[トランザクションクライアント](#ktm-term-transactional-client)、[トランザクションマネージャー](#ktm-term-transaction-manager)、[ログストリーム](#ktm-term-log-stream)、[参加リスト](#ktm-term-enlistment)、および[トランザクション処理システム](#ktm-term-transaction-processing-system)です。

<a href="" id="ktm-term-transaction"></a>**取引**  
*トランザクション*は、データ操作のコレクションです。 トランザクションを成功させるには、すべての操作を成功させる必要があります。 すべての操作が成功した場合は、トランザクションを*コミット*できます (つまり、その結果を永続的かつパブリックにすることができます)。 いずれかの操作が失敗した場合は、トランザクションを*ロールバック*する必要があります (つまり、トランザクションの操作が開始される前と同じ状態になるようにすべての変更を削除する必要があります)。

トランザクションの操作は、*原子*性、*一貫性*、*分離* *性、持続性*(ACID) です。

-   これらはアトミックであるため、コミットまたはロールバックする必要があります。

-   これらの操作は、コミットされるかロールバックされるかにかかわらず、常に正確な結果を生成するため、一貫しています。

-   トランザクションの操作がコミットまたはロールバックされるまでは、各トランザクションの結果が他のトランザクションから参照できないため、分離されています。

-   トランザクションの操作がコミットまたはロールバックされた後、操作の結果が永続的であるため、持続性があります。

トランザクションの例としては、自動預け払い機 (ATM) を使用して当座預金アカウントから預金口座に money を転送するときに実行する必要がある一連の操作が挙げられます。 当座預金口座からのデビットと貯蓄アカウントのクレジットは、単一のアトミックな操作であると思われます。

トランザクションの一部である操作は、トランザクション*操作*とも呼ばれます。

<a href="" id="ktm-term-resource-manager"></a>**リソースマネージャー**  
*リソースマネージャー*は、トランザクション操作によって更新できるデータリソースを管理するソフトウェアコンポーネントです。 たとえば、データベースシステムを設計する場合は、データベースのデータを格納して取得するリソースマネージャーを用意することができます。 単純な[トランザクション処理システム](#ktm-term-transaction-processing-system)(TPS) には、リソースマネージャーが1つだけ存在する場合があります。

リソースマネージャーは、通常、トランザクションクライアントがリソースマネージャーのデータにアクセスするために呼び出すことができるパブリックインターフェイスも提供します。 たとえば、データベースのリソースマネージャーは、クライアントがデータベースへの読み取りと書き込みを行うために呼び出すことができる一連の関数を提供する場合があります。

より複雑な TP は複数のリソースマネージャーを持つことができ、それぞれがシステムのトランザクションに参加している間に個別のデータベースまたは他のリソースを管理します。

リソースマネージャーの詳細については、「[リソースマネージャーの作成](creating-a-resource-manager.md)」を参照してください。

場合によっては、一方のリソースマネージャーが他のリソースマネージャーよりも*優れ*ており、コミット操作を開始できます。 KTM では、このようなリソースマネージャーは[上位トランザクションマネージャー](creating-a-superior-transaction-manager.md)と呼ばれます。

<a href="" id="ktm-term-transactional-client"></a>**トランザクションクライアント**  
*トランザクションクライアント*は、リソースマネージャーがサポートするデータベースにアクセスするソフトウェアコンポーネントです。通常は、リソースマネージャーによってエクスポートされる関数を呼び出します。 クライアントは、トランザクションを作成し、リソースマネージャーがサポートする一連の操作を実行して、トランザクションをコミットまたはロールバックする必要があることをトランザクションマネージャー (KTM) に通知します。

トランザクションクライアントの詳細については、「[トランザクションクライアントの作成](creating-a-transactional-client.md)」を参照してください。

<a href="" id="ktm-term-transaction-manager"></a>**トランザクションマネージャー**  
KTM などの*トランザクションマネージャー*は、トランザクションクライアントとリソースマネージャーが相互に通信できるようにするインフラストラクチャを提供します。 また、各トランザクションの状態も追跡します (クライアントとリソースマネージャーが処理するデータではありません)。

トランザクションマネージャーは、システムのクラッシュ後に復旧操作を調整することもできます。

トランザクションマネージャーは、トランザクションを構成するデータや操作に関する情報を持っていません。 データと操作は、クライアントおよびリソースマネージャーによって制御されます。

KTM には、トランザクションクライアントが呼び出すことができる関数が用意されています。 これらの関数を使用すると、クライアントはトランザクションの作成、コミット、およびロールバックを行うことができます。

KTM には、リソースマネージャーが呼び出すことができる関数も用意されています。 これらの関数は、トランザクションに関する通知を受信できるように、リソースマネージャーがトランザクションに参加できるようにします。 リソースマネージャーをトランザクションに参加させると、トランザクションクライアントがトランザクションをコミットまたはロールバックする準備ができたとき、または復旧操作が発生したときに、通知を受け取ることができます。

<a href="" id="ktm-term-log-stream"></a>**ログストリーム**  
*ログストリーム*は、トランザクションに対して発生したイベントの記録された履歴です。 KTM は、[共通ログファイルシステム](using-common-log-file-system.md)(CLFS) を使用してログストリームを保持します。 KTM では、必要に応じてロールバックと回復操作をサポートできるように、各トランザクションの状態の変化を記録します。

リソースマネージャーは、ログストリームを使用してデータと操作を記録する必要もあります。

ロールバック操作を実行するには、KTM とリソースマネージャーでトランザクションとすべてのデータを初期状態に復元する必要があります。 KTM およびリソースマネージャーは、ロールバック操作中にフェッチできるように、ログストリーム内の各トランザクションの初期状態を記録します。

回復操作は、システムがクラッシュした後に行われます。 その後、オペレーティングシステムが再起動すると、KTM およびリソースマネージャーはログストリームの内容を使用して、トランザクションの状態をクラッシュ前の状態に再構築できます。

KTM のログストリームの詳細については、「 [ktm でのログストリームの使用](using-log-streams-with-ktm.md)」を参照してください。

<a href="" id="ktm-term-enlistment"></a>**参加**  
*参加リスト*は、リソースマネージャーとトランザクションの間の関連付けです。 KTM には、リソースマネージャーが参加リストを作成して管理するために呼び出す一連の関数が用意されています。 リソースマネージャーが参加リストを作成すると、そのトランザクションの状態が変化したときに、KTM によってリソースマネージャーに通知が送信されます。

<a href="" id="ktm-term-transaction-processing-system"></a>**トランザクション処理システム**  
*トランザクション処理システム*(TPS) は、トランザクションマネージャー、1つ以上のリソースマネージャー、1つ以上のログストリーム、およびリソースマネージャーのリソースにアクセスする1つ以上のトランザクションクライアントのコレクションです。

 

 




