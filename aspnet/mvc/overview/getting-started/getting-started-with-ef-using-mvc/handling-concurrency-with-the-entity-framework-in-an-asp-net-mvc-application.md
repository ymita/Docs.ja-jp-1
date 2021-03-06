---
uid: mvc/overview/getting-started/getting-started-with-ef-using-mvc/handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application
title: ASP.NET MVC 5 アプリケーション (10/12) で、Entity Framework 6 と同時実行の処理 |Microsoft ドキュメント
author: tdykstra
description: Contoso 大学でサンプル web アプリケーションでは、Entity Framework 6 の Code First と Visual Studio を使用して ASP.NET MVC 5 アプリケーションを作成する方法について説明しています.
ms.author: aspnetcontent
manager: wpickett
ms.date: 12/08/2014
ms.topic: article
ms.assetid: be0c098a-1fb2-457e-b815-ddca601afc65
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/getting-started/getting-started-with-ef-using-mvc/handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: b92aded80ad6b435a2409a137bb96fe4d0a726f4
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2018
---
<a name="handling-concurrency-with-the-entity-framework-6-in-an-aspnet-mvc-5-application-10-of-12"></a>ASP.NET MVC 5 アプリケーション (10/12) で、Entity Framework 6 と同時実行の処理
====================
によって[Tom Dykstra](https://github.com/tdykstra)

[完成したプロジェクトをダウンロード](http://code.msdn.microsoft.com/ASPNET-MVC-Application-b01a9fe8)または[PDF のダウンロード](http://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20Entity%20Framework%206%20Code%20First%20using%20MVC%205.pdf)

> Contoso 大学でサンプル web アプリケーションでは、Entity Framework 6 の Code First と Visual Studio 2013 を使用して ASP.NET MVC 5 アプリケーションを作成する方法を示します。 チュートリアル シリーズについては、[シリーズの最初のチュートリアル](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)をご覧ください。


前のチュートリアルでは、データを更新する方法について学習しました。 このチュートリアルでは、複数のユーザーが同じエンティティを同時に更新するときの競合の処理方法について説明します。

処理する web ページを変更、`Department`エンティティ、同時実行エラーを処理できるようにします。 次の図は、同時実行の競合が発生した場合に表示される一部のメッセージなどのインデックスと削除のページを表示します。

![Department_Index_page_before_edits](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)

![Department_Edit_page_2_after_clicking_Save](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image2.png)

## <a name="concurrency-conflicts"></a>同時実行の競合

あるユーザーがあるエンティティのデータを編集目的で表示したとき、別のユーザーが同じエンティティのデータを最初のユーザーの変更がデータベースに書き込まれる前に更新すると、同時実行の競合が発生します。 このような競合の検出を有効にしないと、最後にデータベースを更新したユーザーが他のユーザーの変更を上書きすることになります。 多くのアプリケーションでは、このリスクが許容されています。ユーザーや更新がわずかであれば、あるいは変更が一部上書きされても大きな問題なければ、同時実行のプログラミングにかかるコストが利点よりも重視されることがあります。 その場合、同時実行の競合を処理するようにアプリケーションを構成する必要はありません。

### <a name="pessimistic-concurrency-locking"></a>ペシミスティック同時実行制御 (ロック)

同時実行で偶発的にデータが失われる事態をアプリケーションで回避する必要があれば、その方法としてデータベース ロックがあります。 これと呼ばれる*ペシミスティック同時実行制御*です。 たとえば、データベースから行を読む前に、読み取り専用か更新アクセスでロックを要求します。 更新アクセスで行をロックすると、他のユーザーはその行を読み取り専用または更新アクセスでロックできなくなります。変更中のデータのコピーが与えられるためです。 読み取り専用で行をロックすると、他のユーザーはその行を読み取り専用でロックできますが、更新アクセスではロックできません。

ロックの利用には短所があります。 プログラムが複雑になります。 相当なデータベース管理リソースが必要になります。アプリケーションの利用者数が増えると、パフォーマンス上の問題を引き起こすことがあります。 そのような理由から、一部のデータベース管理システムはペシミスティック同時実行制御に対応していません。 Entity Framework には、組み込みのサポートはありません、このチュートリアルは示してそれを実装する方法。

### <a name="optimistic-concurrency"></a>オプティミスティック同時実行制御

ペシミスティック同時実行する代わりに、*オプティミスティック同時実行制御*です。 オプティミスティック同時実行制御では、同時実行の競合の発生を許し、発生したら適切に対処します。 John が部門の編集 ページで変更を実行するなど、**予算**$0.00 ドル 350,000.00 から英語部門の量。

![Changing_English_dept_budget_to_100000](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image3.png)

John が前に**保存**、加藤さんは、同じページと変更を実行、 **Start Date** 2013 年 8 月 8 日から 2007 年 9 月 1 日フィールドです。

![Changing_English_dept_start_date_to_1999](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image4.png)

John が**保存**first と認識し、加藤さん、インデックス ページにブラウザーが返されるときに、変更をクリックした**保存**です。 この後の動作は、同時実行の競合の処理方法によって決定します。 次のようなオプションがあります。

- ユーザーが変更したプロパティを追跡記録し、それに該当する列だけをデータベースで更新できます。 例のシナリオでは、2 人のユーザーが異なるプロパティを更新したため、データは失われません。 次に英語版の部門を参照する他のユーザーの John と Jane の両方の変更が表示されます: 2013 年 8 月 8 日の開始日と 0 個のドルの予算します。

    この更新方法では、データの損失につながる可能性がある競合の数を減らすことができますが、あるエンティティの同じプロパティに対して行われた変更が競合する場合、データの損失は避けられません。 Entity Framework がこのように動作するかどうかは、更新コードの実装方法に依存します。 これは Web アプリケーションの場合、実用的ではない場合が多いです。あるエンティティの新しい値に加え、元のプロパティ値もすべて追跡記録するため、大量のステータスを更新することになるからです。 大量のステータスを更新するとなると、サーバー リソースが必要になるか、Web ページ自体 (非表示フィールドなど) や Cookie に含める必要があるため、アプリケーションのパフォーマンスに影響が出ます。
- John の変更が上書きジェーンの変更することができます。 次に英語版の部門を参照するユーザーが、2013 年 8 月 8 日が表示されますと復元のドル 350,000.00 値。 これは *Client Wins* (クライアント側に合わせる) シナリオまたは *Last in Wins* (最終書き込み者優先) シナリオと呼ばれています。 (クライアントからの値がすべて、データ ストアの値より優先されます。)このセクションの冒頭でお伝えしたように、同時実行処理について何のコーディングもしない場合、これが自動的に行われます。
- ジェーンの変更は、データベースで更新されているを妨害することができます。 通常、エラー メッセージが表示、データの現在の状態を表示するユーザー、および彼女ようにする必要がある場合は、自分が加えた変更を再適用できるようにはします。 これは *Store Wins* (ストア側に合わせる) シナリオと呼ばれています。 (クライアントが送信した値よりデータストアの値が優先されます。)このチュートリアルでは、Store Wins シナリオを実装します。 この手法では、変更が上書きされるとき、それが必ずユーザーに警告されます。

### <a name="detecting-concurrency-conflicts"></a>同時実行の競合を検出します。

競合を解決するには処理することにより[OptimisticConcurrencyException](https://msdn.microsoft.com/library/system.data.optimisticconcurrencyexception.aspx) Entity Framework がスローする例外。 このような例外がスローされるタイミングを認識する目的で、Entity Framework は競合を検出できなければなりません。 そのため、データベースとデータ モデルを適宜構成する必要があります。 競合検出を有効にするためのオプションには次のようなものがあります。

- 行が変更されたタイミングを判断するトラッキング列をデータベース テーブルに追加します。 その列を含めるに Entity Framework を構成することができますし、 `Where` SQL の句`Update`または`Delete`コマンド。

    追跡列のデータ型は、通常[rowversion](https://msdn.microsoft.com/library/ms182776(v=sql.110).aspx)です。 [Rowversion](https://msdn.microsoft.com/library/ms182776(v=sql.110).aspx)値は、行が更新されるたびにインクリメントが連続番号です。 `Update`または`Delete`コマンド、`Where`句には、追跡列 (元の行バージョン) の元の値が含まれています。 更新された行が他のユーザーの値が変更されている場合、`rowversion`列は、元の値と異なるため、`Update`または`Delete`ステートメントがあるため更新する行を見つけることができません、`Where`句。 Entity Framework が、行が更新されていないことを見つけたとき、`Update`または`Delete`コマンドの (つまり、影響を受けた行の数が 0 である場合)、同時実行の競合として解釈します。
- テーブルのすべての列の元の値を含める Entity Framework の構成、`Where`の句`Update`と`Delete`コマンド。

    最初のオプションの場合は、行の任意のものが変更されたため、行が読み取られた最初のように、`Where`句しない行が返されます、更新するには、Entity Framework は同時実行の競合として解釈します。 多くの列を持つデータベース テーブルでは、このアプローチにつながる非常に大きな`Where`句、大量の状態を維持することが必要とします。 先に述べたように、大量のステータスを保守管理することになると、アプリケーションのパフォーマンスに影響が出ます。 そのため、この手法は一般的には推奨されません。このチュートリアルでも利用しません。

    追加することでの同時実行制御を追跡するエンティティのすべての非主キー プロパティをマークする必要がある同時実行するには、このアプローチを実装する場合、 [ConcurrencyCheck](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.concurrencycheckattribute.aspx)属性をします。 変更により、SQL にすべての列を含める Entity Framework`WHERE`の句`UPDATE`ステートメントです。

このチュートリアルの残りの部分では追加、 [rowversion](https://msdn.microsoft.com/library/ms182776(v=sql.110).aspx)追跡するプロパティ、`Department`エンティティ、コント ローラーとビューを作成し、すべてが正常に動作することを確認します。

## <a name="add-an-optimistic-concurrency-property-to-the-department-entity"></a>オプティミスティック同時実行プロパティを Department エンティティに追加します。

*Models\Department.cs*、という名前の追跡のプロパティを追加`RowVersion`:

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs?highlight=20-22)]

[タイムスタンプ](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.timestampattribute.aspx)属性は、この列に含まれることを指定します、`Where`の句`Update`と`Delete`データベースに送信されたコマンド。 属性といいます[タイムスタンプ](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.timestampattribute.aspx)旧バージョンの SQL Server、SQL を使用するため[タイムスタンプ](https://msdn.microsoft.com/library/ms182776(v=SQL.90).aspx)データ型に、SQL [rowversion](https://msdn.microsoft.com/library/ms182776(v=sql.110).aspx)に置き換えられます。 .Net 型を[rowversion](https://msdn.microsoft.com/library/ms182776(v=sql.110).aspx)バイト配列。

Fluent API を使用する場合は、使用、 [IsConcurrencyToken](https://msdn.microsoft.com/library/gg679501(v=VS.103).aspx)メソッドを次の例で示すように、追跡プロパティを指定します。

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]

プロパティを追加し、データベース モデルを変更したので、別の移行を行う必要があります。 パッケージ マネージャー コンソール (PMC) で、次のコマンドを入力します。

[!code-console[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cmd)]

## <a name="modify-the-department-controller"></a>部門コント ローラーを変更します。

*Controllers\DepartmentController.cs*、追加、`using`ステートメント。

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cs)]

*DepartmentController.cs*ファイルは、部門の管理者のドロップダウン リストは、インストラクターの完全な名前ではなく最後の名前だけが含まれるように、"FullName""LastName"の 4 つすべての項目を変更します。

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cs?highlight=1)]

既存のコードを置き換える、 `HttpPost` `Edit`メソッドを次のコード。

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.cs)]

`FindAsync` が null を返した場合、部署は別のユーザーが削除しています。 示すコードでは、ポストされたフォーム値を使用して、エラー メッセージでの編集 ページを再表示できるように、department エンティティを作成します。 あるいは、部署フィールドを再表示せず、エラー メッセージのみを表示するのであれば、部署エンティティを再作成する必要はないでしょう。

ビュー、元の格納`RowVersion`、隠しフィールドとメソッドの値を受け取ることで、`rowVersion`パラメーター。 `SaveChanges` を呼び出す前に、エンティティの `OriginalValues` コレクションにその元の `RowVersion` プロパティ値を置く必要があります。 ときに、Entity Framework は、SQL`UPDATE`コマンド、コマンドが含まれる、`WHERE`句が元のある行を検索する`RowVersion`値。

によって行に影響がない場合、`UPDATE`コマンド (行には、元のあるありません`RowVersion`値)、Entity Framework がスローされます、`DbUpdateConcurrencyException`例外、および内のコード、`catch`ブロックを取得、影響を受ける`Department`例外からのエンティティオブジェクト。

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cs)]

このオブジェクトでユーザーが入力した新しい値にはその`Entity`プロパティ、およびするが呼び出すことによって、データベースから読み取られた値を取得できます、`GetDatabaseValues`メソッドです。

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.cs)]

`GetDatabaseValues`メソッドが他のユーザーには、データベースから行が削除する場合は null を返します。 それ以外の場合、返されたオブジェクトをキャストする必要がある、`Department`クラスにアクセスするために、`Department`プロパティです。 (削除対象として既にチェックされているため`databaseEntry`部門が後に削除された場合にのみ、null になります`FindAsync`実行前に`SaveChanges`を実行します)。

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample9.cs)]

次に、コードでは、カスタム エラー メッセージをデータベース内の編集 ページで入力したユーザーから別の値を持つ各列を追加します。

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample10.cs)]

長いエラー メッセージには、何が起こりについての対処方法について説明します。

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample11.cs)]

コードの最後に、設定、`RowVersion`の値、`Department`データベースから新しい値にオブジェクトを取得します。 Edit ページが再表示されるとき、この新しい `RowVersion` 値が非表示フィールドに保存されます。今度ユーザーが **[保存]** をクリックすると、Edit ページの再表示後に発生した同時実行エラーのみが取得されます。

*Views\Department\Edit.cshtml*、保存する隠しフィールドを追加、`RowVersion`プロパティの値、用の隠しフィールドの直後、`DepartmentID`プロパティ。

[!code-cshtml[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample12.cshtml?highlight=18)]

## <a name="testing-optimistic-concurrency-handling"></a>オプティミスティック同時実行処理のテスト

サイトを実行し、クリックして**部門**:

![Department_Index_page_before_edits](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image5.png)

右クリックして、**編集**ハイパーリンクをクリックし、英語版の部門**[新規] タブで開く**順にクリックして、**編集**英語部門のハイパーリンクのです。 2 つのタブは、同じ情報を表示します。

![Department_Edit_page_before_changes](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image6.png)

最初のブラウザー タブでフィールドを変更し、**[保存]** をクリックします。

![Department_Edit_page_1_after_change](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image7.png)

値が変更された Index ページがブラウザーに表示されます。

![Departments_Index_page_after_first_budget_edit](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image8.png)

2 番目のブラウザー タブ内のフィールドを変更し、クリックして**保存**です。

![Department_Edit_page_2_after_change](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image9.png)

をクリックして**保存**2 番目のブラウザー タブでします。エラー メッセージが表示されます。

![Department_Edit_page_2_after_clicking_Save](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image10.png)

**[保存]** をもう一度クリックします。 2 番目のブラウザー タブで入力した値は、最初のブラウザーで変更されたデータの元の値と共に保存されます。 Index ページが表示されると、保存した値を確認できます。

![Department_Index_page_with_change_from_second_browser](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image11.png)

## <a name="updating-the-delete-page"></a>ページの削除 を更新

Delete ページの場合、Entity Framework は、同様の方法で部署を編集している他のユーザーが起した同時実行の競合を検出します。 ときに、 `HttpGet` `Delete`メソッドは、確認のビューを表示、ビューに含まれる元`RowVersion`隠しフィールドの値。 値が、使用できること、 `HttpPost` `Delete`ユーザー削除を確認するときに呼び出されるメソッド。 Entity Framework が、SQL を作成するときに`DELETE`コマンドが含まれている、`WHERE`を元の句`RowVersion`値。 0 個の行で、コマンドの結果 (つまり、削除の確認 ページが表示された後に、行が変更された)、影響を受ける場合は、同時実行例外がスローされ、および`HttpGet Delete`エラー フラグを設定するメソッドが呼び出された`true`再表示するために、エラー メッセージを確認 ページ。 その場合、別のエラー メッセージが表示されるように、別のユーザーによって行が削除されたため 0 行が影響を受けたこともできます。

*DepartmentController.cs*、置換、 `HttpGet` `Delete`メソッドを次のコード。

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample13.cs)]

このメソッドは、同時実行エラー後にページが再表示されたかどうかを示すオプション パラメーターを受け取ります。 このフラグは場合`true`を使用してビューに、エラー メッセージを送信、`ViewBag`プロパティです。

コードで置き換え、 `HttpPost` `Delete`メソッド (名前付き`DeleteConfirmed`) を次のコード。

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample14.cs)]

置き換えたスキャフォールディングされたコードで、このメソッドがレコード ID を 1 つだけ受け取りました。

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample15.cs)]

このパラメーターを変更する、`Department`モデル バインダーによって作成されたエンティティのインスタンス。 これにより、利用できる、`RowVersion`だけでなく、レコードのキー プロパティの値。

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample16.cs)]

また、アクション メソッドの名前を `DeleteConfirmed` から `Delete` に変更しています。 名前付きスキャフォールディング コード、 `HttpPost` `Delete`メソッド`DeleteConfirmed`を与える、`HttpPost`メソッド固有の署名。 (CLR には、別のメソッドのパラメーターを持つオーバー ロードされたメソッドが必要があります)。署名が一意ではこれでは、MVC 規則のオプションを使用と同じ名前を使用、`HttpPost`と`HttpGet`メソッドを削除します。

同時実行エラーがキャッチされた場合、このコードは削除確認ページを再表示し、同時実行エラー メッセージを表示するかどうかを示すフラグを提供します。

*Views\Department\Delete.cshtml*、スキャフォールディングのコードをエラー メッセージ フィールドと DepartmentID および RowVersion のプロパティの非表示フィールドを追加する次のコードに置き換えます。 変更が強調表示されています。

[!code-cshtml[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample17.cshtml?highlight=9-10,21,52-54)]

このコードの間でエラー メッセージを追加する、`h2`と`h3`見出し。

[!code-cshtml[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample18.cshtml)]

置き換えられます`LastName`で`FullName`で、`Administrator`フィールド。

[!code-cshtml[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample19.cshtml)]

最後に、非表示フィールドを追加、`DepartmentID`と`RowVersion`後プロパティ、`Html.BeginForm`ステートメント。

[!code-cshtml[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample20.cshtml)]

部門のインデックス ページを実行します。 右クリックして、**削除**ハイパーリンクをクリックし、英語版の部門**[新規] タブで開く**最初のタブをクリックして、**編集**英語部門のハイパーリンクのです。

最初のウィンドウで、値のいずれかを変更し、クリックして**保存**:

![Department_Edit_page_after_change_before_delete](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image12.png)

インデックス ページは、変更を確認します。

![Departments_Index_page_after_budget_edit_before_delete](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image13.png)

2 番目のタブで **[削除]** をクリックします。

![Department_Delete_confirmation_page_before_concurrency_error](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image14.png)

同時実行エラー メッセージが表示されます。Department 値がデータベースの現在の内容で更新されています。

![Department_Delete_confirmation_page_with_concurrency_error](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image15.png)

**[削除]** をもう一度クリックすると、Index ページにリダイレクトされます。Index ページには、部署が削除されていることが表示されます。

## <a name="summary"></a>まとめ

同時実行の競合処理の入門編はこれで終わりです。 同時実行のさまざまなシナリオを処理する方法については、次を参照してください。[オプティミスティック同時実行パターン](https://msdn.microsoft.com/data/jj592904)と[プロパティ値を持つ作業](https://msdn.microsoft.com/data/jj592677)msdn です。 次のチュートリアルでは、テーブルの階層あたり継承を実装する方法、`Instructor`と`Student`エンティティです。

その他の Entity Framework リソースへのリンクは含まれて、 [ASP.NET データ アクセス - リソースのことをお勧め](../../../../whitepapers/aspnet-data-access-content-map.md)です。

> [!div class="step-by-step"]
> [前へ](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application.md)
> [次へ](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application.md)
