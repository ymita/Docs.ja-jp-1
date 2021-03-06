---
uid: mvc/overview/older-versions-1/controllers-and-routing/improving-performance-with-output-caching-vb
title: キャッシュ (VB) を出力によるパフォーマンスの向上 |Microsoft ドキュメント
author: microsoft
description: このチュートリアルでは、出力キャッシュを活用して、ASP.NET MVC web アプリケーションのパフォーマンスを大幅に向上する方法を学習します。 あなたが。。。
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/27/2009
ms.topic: article
ms.assetid: 0e7b4d85-2c46-4eaf-b6a8-6cd566a67334
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/improving-performance-with-output-caching-vb
msc.type: authoredcontent
ms.openlocfilehash: 8ee933b477307f5c3f2377e112a1a98d3d6bc337
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2018
---
<a name="improving-performance-with-output-caching-vb"></a>出力 (VB) のキャッシュによるパフォーマンスの向上
====================
によって[Microsoft](https://github.com/microsoft)

> このチュートリアルでは、出力キャッシュを活用して、ASP.NET MVC web アプリケーションのパフォーマンスを大幅に向上する方法を学習します。 同じコンテンツは、新しいユーザーがアクションを呼び出すたびに作成する必要はありません、コント ローラーのアクションから返される結果をキャッシュする方法について学びます。


このチュートリアルの目的では、出力キャッシュを活用して、ASP.NET MVC アプリケーションのパフォーマンスを大幅に向上する方法について説明します。 出力キャッシュには、コント ローラーのアクションによって返されるコンテンツをキャッシュすることができます。 このように、同じコンテンツは、同じコント ローラー アクションが呼び出されるたびに生成する必要はありません。

たとえば、ASP.NET MVC アプリケーションがインデックスをという名前のビューでデータベース レコードの一覧を表示することに想像してください。 通常、ユーザーが、インデックス ビューを返すコント ローラーのアクションを呼び出すたびにデータベース レコードのセットする必要がありますデータベースから取得する、データベース クエリを実行しています。

その一方で、使用すると、出力キャッシュの場合は、すべてのユーザーが同じコント ローラー アクションを呼び出すたびに、データベース クエリの実行を回避できます。 ビューは、コント ローラーのアクションから再生成されることがなくキャッシュから取得できます。 サーバー上で動作する冗長な実行を回避するキャッシュを有効します。

#### <a name="enabling-output-caching"></a>出力キャッシュの有効化

出力を追加することでキャッシュを有効にする、 &lt;OutputCache&gt;属性を各コント ローラー アクションまたは全体のコント ローラー クラスのいずれか。 たとえば、リスト 1 のコント ローラーは、Index() をという名前のアクションを公開します。 Index() アクションの出力は、10 秒間キャッシュされます。

**1 – Controllers\HomeController.vb を一覧表示します。**

[!code-vb[Main](improving-performance-with-output-caching-vb/samples/sample1.vb)]


ASP.NET MVC のベータ版で出力キャッシュが機能しないような URL [ http://www.MySite.com/](http://www.mysite.com/)です。 代わりに、ような URL を入力する必要があります[ http://www.MySite.com/Home/Index](http://www.mysite.com/Home/Index)です。


リストの 1 の Index() アクションの出力が 10 秒間キャッシュされます。 場合は、かなり長くキャッシュの存続期間を指定できます。 たとえば、1 日のコント ローラーのアクションの出力をキャッシュする場合を指定できます (86400 秒) のキャッシュの存続期間 (60 秒\*60 分\*24 時間)。

指定した時間分保証コンテンツはキャッシュされません。 メモリ リソースが不足になると、キャッシュは削除のコンテンツを自動的に起動します。

1 の一覧で、Home コント ローラーは、2 の一覧表示するインデックス ビューを返します。 このビューに関する特別なはありません。 インデックス ビューには、単に、現在の時刻が表示されます (図 1 を参照してください)。

**Listing 2 – Views\Home\Index.aspx**

[!code-aspx[Main](improving-performance-with-output-caching-vb/samples/sample2.aspx)]

**図 1 – キャッシュのインデックス ビュー**

![clip_image002](improving-performance-with-output-caching-vb/_static/image1.jpg)

お使いのブラウザーのアドレス バーに URL/Home/インデックスを入力し、インデックス ビューによって表示される時間し、繰り返し、お使いのブラウザーの更新/再読み込み ボタンを押すで複数回 Index() アクションを起動する場合は、10 秒間に変更されません。 ビューがキャッシュされるため、同時が表示されます。

同じビューが、アプリケーションにアクセスしたすべてのキャッシュされていることを理解しておく必要です。 Index() アクションを起動したすべてのユーザーをインデックス ビューの場合は、同じキャッシュされたバージョンとなります。 これは、インデックス ビューを提供する web サーバーが行う作業の量が大幅に削減することを意味します。

ビューを一覧表示する 2 は、操作を行っている実に簡単に発生します。 ビューには、現在の時刻だけが表示されます。 ただし、簡単にキャッシュを一連のデータベース レコードを表示するビューと同じようにできます。 その場合は、データベース レコードのセットでは、ビューを返しますコント ローラーのアクションが呼び出されるたびに、データベースから取得する必要はありません。 キャッシュと、web サーバーおよびデータベース サーバーの両方が実行する必要がある作業の量を減らすことができます。

ページを使用しない&lt;% @ OutputCache %&gt; MVC ビュー内のディレクティブ。 このディレクティブは、Web フォームの世界から漏れると、ASP.NET MVC アプリケーションでは使用できません。 

#### <a name="where-content-is-cached"></a>コンテンツがキャッシュされています。

既定では、使用すると、 &lt;OutputCache&gt;属性、コンテンツは、3 つの場所にキャッシュされて: web サーバー、すべてのプロキシ サーバーと web ブラウザー。 Location プロパティを変更することによってコンテンツがキャッシュされているに正確に制御することができます、 &lt;OutputCache&gt;属性。

次の値のいずれかに、Location プロパティを設定できます。

> ·任意
> 
> ·クライアント
> 
> ·ダウン ストリーム
> 
> ·サーバー
> 
> ·[なし]
> 
> ·ServerAndClient


既定では、Location プロパティに値 Any です。 ただし、ブラウザーでのみ、またはサーバー上でのみキャッシュにすることがありますもあります。 たとえば、ユーザーごとに個人用に設定された情報をキャッシュする場合は必要がありますいないサーバー上の情報をキャッシュします。 ユーザーごとに異なる情報を表示する場合は、クライアント上にのみ情報をキャッシュする必要があります。

たとえば、リスト 3 でのコント ローラーを現在のユーザー名を返す GetName() をという名前のアクションを公開します。 回線のモジュラー ジャックが、web サイトにログインすると、GetName() アクションを呼び出しますアクションの文字列を返します「やあジャック」です。 後で、Jill は、web サイトにログインし、GetName() アクションが呼び出されます場合、し、彼女はもは文字列を取得「やあジャック」。 文字列は、回線のモジュラー ジャックが最初にコント ローラーのアクションを起動した後、すべてのユーザー用の web サーバーにキャッシュされます。

**3 – Controllers\BadUserController.vb を一覧表示します。**

[!code-vb[Main](improving-performance-with-output-caching-vb/samples/sample3.vb)]

ほとんどの場合、リスト 3 でのコント ローラーでは、使用する方法は機能しません。 Jill に「やあジャック」メッセージを表示します。

サーバーのキャッシュ内の個人用に設定されたコンテンツをキャッシュすることはありません。 ただし、パフォーマンスを向上させるためにブラウザー キャッシュ内の個人用に設定されたコンテンツをキャッシュすることができます。 ブラウザーで、コンテンツをキャッシュする、ユーザーは、同じコント ローラー アクションを複数回呼び出す場合は、コンテンツは、サーバーではなく、ブラウザーのキャッシュから取得できます。

リスト 4 に変更されたコント ローラーは、GetName() アクションの出力をキャッシュします。 ただし、ブラウザーでのみ、サーバーではなく、コンテンツがキャッシュされます。 このように、複数のユーザーが GetName() メソッドを呼び出すときは、各ユーザーは、ユーザー名と他のユーザーのユーザー名を取得します。

**4 – Controllers\UserController.vb を一覧表示します。**

[!code-vb[Main](improving-performance-with-output-caching-vb/samples/sample4.vb)]

注意して、 &lt;OutputCache&gt;リスト 4 属性には OutputCacheLocation.Client 値に設定された場所プロパティが含まれています。 &lt;OutputCache&gt;属性には、NoStore プロパティも含まれています。 NoStore プロパティは、キャッシュされたコンテンツの永続的なコピーを格納しないようにすることのプロキシ サーバーとブラウザーを通知するために使用されます。

#### <a name="varying-the-output-cache"></a>出力キャッシュの変更

状況によっては、非常に同じコンテンツの別のキャッシュされたバージョンを必要があります。 たとえば、マスター/詳細ページを作成することに想像してください。 マスター ページには、ムービーのタイトルの一覧が表示されます。 タイトルをクリックすると、選択したムービーの詳細を取得します。

詳細ページをキャッシュする場合、同じ映画の詳細が表示 ムービーに関係なく をクリックします。 最初のユーザーが選択した最初のムービーが将来のすべてのユーザーに表示されます。

この問題を修正するには、VaryByParam プロパティを活用して、 &lt;OutputCache&gt;属性。 このプロパティでは、フォームのパラメーターのときに非常に同じコンテンツの別のキャッシュされたバージョンを作成できます。 または、クエリ文字列パラメーターが異なります。

たとえば、5 の一覧で、コント ローラーは、Master() および Details() という名前の 2 つのアクションを公開します。 Master() アクションはムービーのタイトルの一覧を返し、Details() アクションは、選択したムービーの詳細を返します。

**5 – Controllers\MoviesController.vb を一覧表示します。**

[!code-vb[Main](improving-performance-with-output-caching-vb/samples/sample5.vb)]

Master() アクションには、値を持つ VaryByParam プロパティが含まれています。"none"です。 アクションが呼び出されると、Master() マスターの場合は、同じキャッシュされたバージョンの表示とが返されます。 パラメーターは、フォームのパラメーターまたはクエリ文字列には、(図 2 を参照) が無視されます。

**図 2 –/Movies/Master ビュー**

![clip_image004](improving-performance-with-output-caching-vb/_static/image2.jpg)

**図 3 –/ビデオ/詳細ビュー**

![clip_image006](improving-performance-with-output-caching-vb/_static/image3.jpg)

Details() アクションには、"Id"の値を持つ VaryByParam プロパティが含まれています。 Id パラメーターの異なる値は、コント ローラーのアクションに渡され、詳細ビューの別のキャッシュされたバージョンが生成されます。

詳細キャッシュでは、VaryByParam プロパティ結果を使用することを理解して重要でない小さいをお勧めします。 別のキャッシュされたバージョンの詳細ビューの Id パラメーターの各バージョンが作成されます。

VaryByParam プロパティは、次の値を設定することができます。

> \* = フォームまたはクエリ文字列パラメーターが変化するたびに、別のキャッシュされたバージョンを作成します。
> 
> none = しない別のキャッシュされたバージョンを作成します。
> 
> セミコロンのパラメーター リスト内のフォームまたはクエリ文字列パラメーターのいずれかによって異なりますされるたびに作成のさまざまなキャッシュされたバージョンを =


#### <a name="creating-a-cache-profile"></a>キャッシュ プロファイルを作成します。

プロパティを変更することで出力キャッシュのプロパティを構成する代わりに、 &lt;OutputCache&gt;属性に、web の構成 (web.config) ファイルでキャッシュ プロファイルを作成することができます。 Web 構成ファイルでキャッシュ プロファイルを作成するには、重要な利点のいくつか用意されています。

最初に、web 構成ファイルで出力キャッシュを構成すると、コント ローラーのアクションが 1 つの場所にコンテンツをキャッシュする方法を制御できます。 1 つのキャッシュ プロファイルを作成し、いくつかのコント ローラーまたはコント ローラーのアクションにプロファイルを適用できます。

次に、アプリケーションを再コンパイルしなくても web 構成ファイルを変更できます。 実稼働環境に既に配置されているアプリケーションのキャッシュを無効にする必要がある場合、web 構成ファイルで定義されているキャッシュ プロファイルだけで変更できます。 Web 構成ファイルへの変更が自動的に検出され、適用します。

たとえば、&lt;キャッシュ&gt;リスト 6 での web 構成セクションを Cache1Hour をという名前のキャッシュ プロファイルを定義します。 &lt;キャッシュ&gt;内のセクションに表示されます、 &lt;system.web&gt; web 構成ファイルのセクションです。

**6 – web.config のキャッシュ セクションを一覧表示します。**

[!code-xml[Main](improving-performance-with-output-caching-vb/samples/sample6.xml)]

一覧表示する 7 でのコント ローラーとコント ローラーのアクションに Cache1Hour プロファイルを適用する方法を示しています、 &lt;OutputCache&gt;属性。

**7 – Controllers\ProfileController.vb を一覧表示します。**

[!code-vb[Main](improving-performance-with-output-caching-vb/samples/sample7.vb)]

リスト 7 でのコント ローラーによって公開される Index() アクションを呼び出す場合、同時にが 1 時間に返されます。

#### <a name="summary"></a>まとめ

出力キャッシュ、ASP.NET MVC アプリケーションのパフォーマンスを大幅に向上させるの非常に簡単な方法を提供します。 このチュートリアルで使用する方法を学びました、 &lt;OutputCache&gt;コント ローラー アクションの出力をキャッシュする属性。 プロパティを変更する方法も学習しました、 &lt;OutputCache&gt;コンテンツがキャッシュを取得する方法を変更するプロパティの期間と VaryByParam プロパティなどの属性です。 最後に、web 構成ファイルでキャッシュ プロファイルを定義する方法を学習します。

> [!div class="step-by-step"]
> [前へ](understanding-action-filters-vb.md)
> [次へ](adding-dynamic-content-to-a-cached-page-vb.md)
