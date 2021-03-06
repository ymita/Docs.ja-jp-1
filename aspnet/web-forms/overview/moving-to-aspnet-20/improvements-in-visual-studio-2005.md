---
uid: web-forms/overview/moving-to-aspnet-20/improvements-in-visual-studio-2005
title: "Visual Studio 2005 の機能強化 |Microsoft ドキュメント"
author: microsoft
description: "Visual Studio 2005 では、Web アプリケーションの開発者の強化機能と Web プロジェクトの機能強化の長い一覧を提供します。"
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/20/2005
ms.topic: article
ms.assetid: 72d90cd0-b3d9-454c-b2eb-ed0d9812f32c
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/improvements-in-visual-studio-2005
msc.type: authoredcontent
ms.openlocfilehash: aafc59980e807677d6023110d324365ce92bb5fc
ms.sourcegitcommit: d8aa1d314891e981460b5e5c912afb730adbb3ad
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/05/2018
---
<a name="improvements-in-visual-studio-2005"></a>Visual Studio 2005 の機能強化
====================
によって[Microsoft](https://github.com/microsoft)

> Visual Studio 2005 では、Web アプリケーションの開発者の強化機能と Web プロジェクトの機能強化の長い一覧を提供します。


Visual Studio 2005 では、Web アプリケーションの開発者の強化機能と Web プロジェクトの機能強化の長い一覧を提供します。 Visual Studio .NET 2002 および 2003 は、強力なありました多く Web プロジェクトが処理された方法でします。 Visual Studio 2005 では、これらのクレームに対処するために多数の新機能を追加します。 管理者向け Visual Studio .NET 2003 Web アプリケーションのコンパイルの処理方法を必要に応じて、次を参照してください。 [Web アプリケーション プロジェクト](https://go.microsoft.com/fwlink/?LinkId=57870)です。

このモジュールでは、Web プロジェクトの作成、管理、および開発の機能強化をについて説明します。 モジュールでは、後で、Web プロジェクトのビルドと配置の機能強化をも説明します。

## <a name="frontpage-server-extensions"></a>FrontPage Server Extensions

Visual Studio .NET 2002 および 2003 の作成または Web プロジェクトをビルドするために、ボックスの FrontPage Server Extensions が必要です。 開発者は 2 つの異なるアクセス モード (FrontPage Server Extensions またはファイルのアクセス モード) のいずれかが、IIS などのアプリケーション ルートの設定などのタスクを実行する両方の FrontPage Server Extensions を使用します。

Visual Studio 2005 では、ローカル プロジェクトの場合は、FrontPage Server Extensions への依存を削除します。 Visual Studio 2005 は、FrontPage Server Extensions を使用する代わりに直接 IIS メタベースを今すぐアクセスします。 Visual Studio 2005 では、使用できるプロジェクトのリモート アクセスの FrontPage Server Extensions を必要とせず FTP のサポートも追加されます。

開発者にとって、プロジェクトで、FrontPage Server Extensions を使用する、オプションは引き続き使用できます。 ただし、ASP.NET 開発者コミュニティからの強力なフィードバックに基づいて、その必要はありません。

> [!NOTE]
> FrontPage Server Extensions は、リモートのプロジェクトの作成、開始なども必要です。


## <a name="aspnet-development-server"></a>ASP.NET 開発サーバー

Visual Studio 2005 は、ASP.NET 開発サーバーと呼ばれる新しい Web サーバーに付属します。 (この Web サーバーが以前 Cassini。)

これには、ASP.NET 開発サーバーのいくつかの利点があります。

- 開発および Web サーバーに対してデバッグを「管理者以外ことがなりました。
- ASP.NET 開発サーバーは、柔軟なプロジェクトの場所を許可するファイル システム内の仮想ディレクトリを任意の場所に動的にマッピングします。
- IIS を使用して既に Windows XP Professional のユーザーは、ファイルまたはフォルダーの構造の既定の Web サイトの IIS では無効にする新しい Web アプリケーションを作成することになります。

ASP.NET 開発サーバーを活用するために特別な構成は必要ありません。 ファイル システムでホストされている Web プロジェクトがデバッグしたり、参照、ときに Visual Studio 2005 は自動的に開始されている要求の処理をランダム ポートで、ASP.NET 開発サーバーのインスタンスを使用します。

詳細については、後でこのモジュールで ASP.NET 開発サーバーで取り上げます。

## <a name="improved-file-management"></a>強化されたファイルの管理

Visual Studio の 2002、2003 では、プロジェクト ファイル (VB.NET の .vbproj) と c# の .csproj は、Web アプリケーションのすべてのファイルに情報を格納します。 ソリューション エクスプ ローラーの表示は、プロジェクト ファイル内のファイル情報に基づいています。 このため、ソリューション エクスプ ローラーは多くの場合、情報が表示不正確な外部エディターが使用されている場合。 Visual Studio の 2002年、2003 は多くの場合、ファイルの変更を上書きしたり、ファイルの最新バージョンは表示されません。

Visual Studio 2005 では、プロジェクト ファイルで、休暇から。 代わりに、その結果、プロジェクト内のファイルの正確に表示、ディスクから直接ファイルとフォルダーの情報を読み取ります。 Visual Studio の 2002、2003 の [参照設定] フォルダーが、Web アプリケーションで実際のフォルダーを表さないため Visual Studio 2005 もソリューション エクスプ ローラーから、[参照] フォルダーを削除します。 Visual Studio 2005 でプロジェクトの参照にアクセスするには、プロジェクトのプロパティ ページを使用する必要があります。

## <a name="creating-web-projects"></a>Web プロジェクトの作成

Web 開発者では、Visual Studio 2005 でプロジェクトの作成に使用できる多くの新しいオプションがあります。 Web サイトようになりましたまたは作成できます任意の場所、ファイル システム内とし、デバッグすることができます、新しい ASP.NET 開発サーバーを使用して参照します。 開発者は、FTP を使用して新しい Web サイトを作成もできます。

ここをクリックすると、Visual Studio 2005 で Web プロジェクトの作成のビデオ チュートリアルを表示します。


![](improvements-in-visual-studio-2005/_static/image1.png)


[開いているビデオを全画面](improvements-in-visual-studio-2005/_static/creating_projects1.wmv)


### <a name="file-system-projects"></a>ファイル システムのプロジェクト

ビデオ チュートリアルで説明したとおり、ローカル コンピューターまたはリモートの場所をファイル共有からファイル システム上の Web サイトを作成することもできます。 ファイル システム上に作成される web サイトでは、参照がおよび、ASP.NET 開発サーバーを使用してデバッグします。

> [!NOTE]
> ASP.NET 開発サーバーは、顧客の混乱を招くにあります。 IISs ディレクトリ構造 (つまり c:/inetpub/wwwroot) 内のファイル システムで Web プロジェクトを作成する場合、Visual Studio 2005 内から起動されたときに、ASP.NET 開発サーバー経由で Web サイトが参照も。 そのため、IIS 構成 (認証方法など) は適用されません。


既定の web プロジェクトがたくさん削除もでオーバーヘッドののみが含まれています、Default.aspx ページ、default.cs ファイル、およびアプリ/_Data フォルダーです。 Web.config および特別なフォルダー (つまりアプリ/_code) は、必要な分だけに追加されます。 Web プロジェクトは、ファイルとする必要があるフォルダーに含まれています。

### <a name="http-projects"></a>HTTP プロジェクト

HTTP プロジェクトは、ローカル IIS Web サイトまたはリモートの Web サイトに作成されたプロジェクトになります。 既定のプロジェクトの場所が`http://localhost`です。 [参照] ボタンをクリックする場合は、次の 2 つの HTTP オプション: ローカル IIS サイトとリモート サイト。 これら 2 つのオプションの主な違いは、Web サーバーにファイルをコピーする方法と場所の選択 ダイアログで web サイトの情報を表示する方法です。

ローカル IIS オプションは、ローカル コンピューター上のメタベースからサイト情報を読み取るし、ファイル システムを使用してファイルをコピーします。 リモート サイト オプションは、FrontPage Server Extensions とサイトの情報と HTTP を使用してファイルがコピーされ、FrontPage Server Extensions の RPC を呼び出します。

> [!NOTE]
> Vs###/_tmp.htm ファイルと get/_aspx/_ver.aspx はバージョン情報を決定するのには使用されません。


既定の HTTP オプションは、ローカル IIS です。 このオプションは、どのサイトが利用できるかを判断する IIS メタベースおよびコンテンツを作成する場所を読み取ります。 ツリー ビューで選択して、別のフォルダーまたは仮想ディレクトリを選択できます。 ことができますも、新しい仮想ディレクトリを作成、フォルダー、アプリケーションとしてのマークを付けるだけでなくこのダイアログ ボックスから既存の仮想ディレクトリを削除します。


![場所のダイアログ ボックスを選択](improvements-in-visual-studio-2005/_static/image1.gif)

**図 1**: の場所のダイアログ ボックスを選択


異なりをチェックする場合、Visual Studio の以前のバージョンで、**を使用して Secure Sockets Layer**  チェック ボックスと、SSL 証明書を参照している URL が一致しません、確認するかどうかはセキュリティの警告ダイアログ ボックスが表示されます続行すると同様にします。 証明書が一致するものではない場合は、Visual Studio .NET 2003 を使用して、プロジェクトの作成は失敗します。


![セキュリティ アラートに関する SSL 証明書](improvements-in-visual-studio-2005/_static/image2.gif)

**図 2**: SSL 証明書に関するセキュリティの警告


### <a name="note-on-host-headers"></a>ホスト ヘッダーに関する注意事項

特定の IP にバインドされているサイトで Web アプリケーションを作成する場合は、ホスト ヘッダーを構成できるようにする必要があります。 Visual Studio が、サイトを作成するそれ以外の場合、`http://localhost`は、サイトを参照または IDE 内からデバッグする場合に、IP アドレスが正常に解決されません。

リモート サイトのオプションを選択した場合、ダイアログ ボックスは、新しい Web サイトの送信先 URL を入力するように変更されます。 この URL は、有効になっている FrontPage Server Extensions をされているサーバーにする必要があります。 FrontPage Server Extensions を使用して、ローカル Web サーバーを使用する場合は、リモート サイト オプションを使用してローカル URL を指定します。


![リモート サーバーで Web サイトの作成](improvements-in-visual-studio-2005/_static/image1.jpg)

**図 3**: リモート サーバーで Web サイトの作成


SSL 証明書が一致しない場合は、SSL 経由でリモート サイトでのアプリケーションを作成するときに確認のダイアログ ボックスは、ローカル IIS オプションを使用する場合に表示されるダイアログ ボックスと若干異なるです。


![リモート サイト セキュリティの警告](improvements-in-visual-studio-2005/_static/image3.gif)

**図 4**: リモート サイト セキュリティの警告


<a id="_Toc116100243"></a>

#### <a name="ftp"></a>FTP

Visual Studio 2005 には、FTP 経由で Web サイトを作成するオプションが導入されています。 このオプションを使用するときにユーザーの一時フォルダーにファイルをローカルに作成され、FTP を使用して、ファイルを FTP の場所に移動されます。

> [!NOTE]
> 一時フォルダーの場所は、c:/Documents and Settings/&lt;ユーザー&gt;/ローカルの設定/Temp/VWDWebCache/&lt;サーバー&gt;/_&lt;アプリケーション名&gt;


FTP オプションを使用する場合は、場所の選択 ダイアログ ボックスが表示されます。 次のようにこのダイアログ ボックスに、必要な FTP 接続情報を入力します。


![FTP の場所 ダイアログ ボックスを選択](improvements-in-visual-studio-2005/_static/image2.jpg)

**図 5**: FTP の場所 ダイアログ ボックスを選択


## <a name="lab-setup-ftp-site-and-create-a-project"></a>ラボ: セットアップ FTP サイトおよびプロジェクトの作成

次の手順は、ユーザーがある FTP 経由でをアップロードできるのみ、場所を持つように、FTP サイトを構成します。

### <a name="install-the-ftp-service"></a>FTP サービスをインストールします。

1. プログラムの追加と削除を開き、Windows コンポーネントの追加と削除を選択
2. インターネット インフォメーション サービス (Windows 2003 上のアプリケーション サーバー) を選択し、クリックして**詳細**です。
3. 確認**ファイル転送プロトコル (FTP) サービス** をクリック**OK**です。
4. をクリックして**次**FTP サービスをインストールします。

### <a name="create-a-new-folder-for-content"></a>コンテンツの新しいフォルダーを作成します。

1. Windows エクスプローラと呼ばれる新しいフォルダーを作成**User1** c:/inetpub/wwwroot 内で。

#### <a name="configure-folders-and-permissions-on-folders"></a>フォルダーのフォルダーとアクセス許可を構成します。

1. 管理ツールから、インターネット インフォメーション サービス スナップインを開きます。 コンピューター名のノードの下、FTP サイトのフォルダーが表示されます。
2. 展開**FTP サイト**です。
3. 右クリックし、 **FTP サイトの既定の****新規**、し**仮想ディレクトリ**、をクリックして**次へ**です。
4. 入力**User1**をクリックして、仮想ディレクトリ名の**次**です。
5. 入力**c:/inetpub/wwwroot/User1**クリックとパスの**次**です。
6. をクリックして**[次へ]**し**完了**ウィザードを完了します。
7. 右クリックし、 **User1**既定の FTP サイトと選択対象の仮想ディレクトリ**プロパティ**です。
8. チェック、**書き込み** チェック ボックス をクリック**ok**ダイアログ ボックスを閉じます。
9. 右クリック**FTP サイトの既定の**選択**プロパティ**です。
10. **セキュリティ アカウント** タブで、オフにして**匿名接続を許可する**です。
11. をクリックして**はい**続行するかどうかたずねるダイアログ ボックスでします。
12. をクリックして**OK**ダイアログ ボックスを閉じます。
13. 展開、**既定の Web サイト**下にある、 **Websites**ノード。
14. 右クリックし、 **User1**ディレクトリおよび select**プロパティ**
15. **アプリケーション設定**セクションで、**作成**アプリケーションとしてフォルダーをマークします。
16. をクリックして**OK**ダイアログ ボックスを閉じます。
17. インターネット インフォメーション サービス スナップインを閉じます。

### <a name="create-web-project"></a>Web プロジェクトを作成します。

1. Visual Studio 2005 を開きます。
2. **ファイル**メニューの **新しい Web サイト**です。
3. **場所**ドロップダウンで、 **FTP**です。
4. **[参照]**をクリックします。
5. 入力**localhost**で、**サーバー**  テキスト ボックス。
6. 入力**User1**ディレクトリ ボックスで、します。
7. をクリックして**開く**です。 FTP の場所は、新しい Web サイト ダイアログに入力されます。
8. **[OK]**をクリックします。
9. オフに**匿名ログオンを**FTP ログオン ダイアログ ボックスで、資格情報を入力し、クリックして**OK**です。
10. プロジェクトの URL とは何ですか。 (プロジェクトの URL はソリューション エクスプ ローラーで表示されます)。
11. **ビルド**メニューの  **Web サイトのビルド**または**ソリューションのビルド**です。
12. ソリューション エクスプ ローラーで Default.aspx を右クリックし、選択**ブラウザーで表示**です。
13. Web サイト URL が必要です ダイアログ ボックスで、次を入力してください。 `http://localhost/user1` URL およびクリック**ok**です。

> [!NOTE]
> 型/_Default を読み込むことができないことを示すエラーが発生した場合は、Web サイトと以前のバージョンではなくで ASP.NET 2.0 を実行していることを確認します。 インターネット インフォメーション サービスで、[ASP.NET] タブから、ことを行うことができます。


## <a name="opening-web-projects"></a>Web プロジェクトを開く

Web プロジェクトを開くことは、プロジェクトの作成に似ています。 次のセクションでは、IDE で作業しているの監視する領域を呼び出します。 HTTP と FTP を使用して Web プロジェクトでの作業についても説明します。

Web プロジェクトを開くには、[ファイル] メニューから開く Web サイトを選択します。 使用する同じの 4 つのオプションを使用して以前に対象の場所の選択ダイアログと同じで求められます。 ファイル システム、ローカル IIS、FTP、およびリモート サイト。

<a id="_Toc116100245"></a>

## <a name="file-system"></a>ファイル システム

このモジュールで示したように Visual Studio は不要になったプロジェクト ファイルを使用します。 そのため、ある場合は、Web サイトを開く、ファイル システムから選択すると、実際に、オプション選択したフォルダーが Visual Studio で最初に Web プロジェクトとして作成されていない場合でも、任意のフォルダーを選択します。 たとえばを Web サイトとして [マイ ドキュメント] フォルダーを開くことができ、Visual Studio が問題なくを開き、次に示すように、ファイルを表示します。


![Web サイトとして開くマイ ドキュメント](improvements-in-visual-studio-2005/_static/image3.jpg)

**図 6**:*マイ ドキュメント*Web サイトとして開く


Visual Studio では、追加のファイルおよびフォルダーの必要な場合にのみ作成するため追加のファイルまたはフォルダーは追加されませんを開いた場所にします。 このアーキテクチャの副作用は、ことはできないので、ファイル システム上の Web サイトを入れ子です。 たとえば、次のディレクトリ構造があるとします。

C:/mywebsite という web プロジェクト

C:/MyWebSite/入れ子になった別の web プロジェクト

C:/mywebsite という Web サイトを開くと、入れ子になったフォルダーは、そのアプリケーションのサブ フォルダーとして表示されます。

<a id="_Toc116100246"></a>

## <a name="http"></a>HTTP

IIS メタベース (ローカルの IIS) または FrontPage Server Extensions (リモート サイト) を使用して、設定が読み取り HTTP 経由で Web サイトを開くとき入れ子になった web アプリケーションがある場合は、アプリケーションとして指定するアイコンもこれら表示されます。 Frontpage web アプリケーションの操作に慣れている場合は、Visual Studio 2005 での動作は似ています。

場合でも、Visual Studio IDE 内で現在開かれているアプリケーションの下に入れ子になっているアプリケーションのアイコンが表示され、ことはできません、コンテンツを参照するように展開します。 ダブルクリックすると、ただし、それらを開くこともできます。 操作を実行するとするか、web アプリケーションを開きます (および現在開いているソリューションを置き換えます) を求めるダイアログ ボックスが表示されますか、現在のソリューションに Web アプリケーションを追加します。


![このダイアログ ボックスが表示、入れ子になったアプリケーション アイコンをダブルクリックします。](improvements-in-visual-studio-2005/_static/image4.jpg)

**図 7**: 入れ子になったアプリケーション アイコンをダブルクリックしてこのダイアログ ボックスで表示


<a id="_Toc116100247"></a>

## <a name="ftp-site"></a>FTP サイト

FTP 経由でサイトを開くと、ファイルはすべてにローカルにコピー、temp フォルダーです。 ローカル ストレージの場所の完全なパスはプロジェクトのプロパティ ペインに表示され、次の形式を使用して作成されます。

C:/Documents and Settings/&lt;ユーザー&gt;/ローカルの設定/Temp/VWDWebCache/&lt;サーバー&gt;/_&lt;アプリケーション名&gt;

FTP を使用する場合、Visual Studio は、次に示すように参照できるように、プロジェクトのベース URL を指定する必要があります。 ベース URL を指定しない場合 Visual Studio のためを依頼する Web サイトのページを参照しようとする最初の時間。


![FTP サイトのベース URL を指定します。](improvements-in-visual-studio-2005/_static/image5.jpg)

**図 8**: FTP サイトのベース URL を指定します。


## <a name="improvements-in-compilation"></a>コンパイルの向上

Visual Studio 2005 で Web アプリケーションの操作は、以前のバージョンよりも著しく高速です。 これは、期限切れになる小さないかなる部分もコンパイル アーキテクチャでの変更にです。

2003 と Visual Studio の 2002 では、Web アプリケーションが/bin フォルダー内に存在する 1 つのプライマリ アセンブリにコンパイルされました。 Visual Studio 2005 で、アプリ/_Code フォルダーが追加されました。 クラスとその他の非 UI コードは、アプリ/_Code フォルダーに追加されます。 Visual Studio では、プロジェクトをビルド、アプリ/_Code フォルダー内のすべてのファイルは 1 つ App/_Code.dll ファイルにコンパイルされます。 この変更の結果は、後続のビルドが以前のバージョンよりも高速です。

> [!NOTE]
> MSBuild コマンド ライン ユーティリティは、ASP.NET Web アプリケーションの構築にも使用できます。 ツールは、モジュール 9 で取り上げます。


別のコンパイルの機能強化は、[ビルド] メニューで新しいビルド ページ オプションです。 この機能によりより迅速に変更をコンパイルできるように、現在のページのみ (と共に、当然、依存関係の) を再構築する開発者です。 C# の IntelliSense などの更新の目的でバック グラウンドのコンパイルを提供しません、ためような利点が非常にこの機能のため、IntelliSense が 1 つのページの再構築するだけで簡単に更新するためにできるようになります。

プロジェクトのビルド プロパティを使用すると、最初のページが実行される前に実行されるビルドの種類を構成できます。 開発者は、Visual Studio のコードの変更後のアプリケーションをより迅速にデバッグを開始するために、現在のページをのみビルドを選択できます。


![ビルド ページ開始アクション](improvements-in-visual-studio-2005/_static/image6.jpg)

**図 9**: ビルド ページ開始アクション


Visual Studio と ASP.NET のアーキテクチャを別の優れた機能強化は編集の領域にあり、続行します。 Visual Studio 2005 では、開発者はプロジェクトのデバッグを開始し、デバッガーをデタッチしてもプロジェクトでコードの変更を行います。 実際には、新しいクラスを追加、プロジェクトのデバッグを開始することができます文字どおり、そのクラスにコードを追加、コード ページを追加、そのクラスの新しいインスタンスを作成およびすべてデバッガーをデタッチすることがなく、クラスのメソッドを実行します。 新しいコードを実行することは、文字どおりブラウザーを更新する同じくらい簡単です!

ここをクリックすると Visual Studio 2005 の機能をコンティニュ編集のビデオ チュートリアルを参照してください。


![](improvements-in-visual-studio-2005/_static/image2.png)


[開いているビデオを全画面](improvements-in-visual-studio-2005/_static/editcontinue1.wmv)


堅牢なエディット コンティニュ機能で ASP.NET 2.0 と Visual Studio 2005 は ASP.NET アプリケーションのアーキテクチャの変更に起因します。 ASP.NET で 1.x では、Visual Studio の 2002年/2003 で作成されたアプリケーションが/bin フォルダーに保存されているプライマリ アセンブリにコンパイルされました。 すべてのクラス、ページなどをその 1 つの DLL にコンパイルされたアプリケーション。 実行時に、ASP.NET はすべてのコントロール、マークアップ、およびページ内での ASP.NET コードをコンパイルし、ASP.NET 一時フォルダーにそれらの Dll をコピーします。

ASP.NET 2.0 では、実行時に (Visual Studio のいずれか) と ASP.NET のいずれかの上の 2 つのコンパイル モデルの概要を使用して Visual Studio 2005 では 1 つの一般的なコンパイル モデルにマージされました。 つまり、コンパイルの問題をすべてが実行時の代わりに開発段階で発見ようになりましたことです。 デザイナーとユーザー コントロールおよびマスター ページなどの機能の IntelliSense サポートこともできます。

ここをクリックすると、ユーザー コントロールのデザイナー サポートのビデオ チュートリアルを参照してください。


![](improvements-in-visual-studio-2005/_static/image3.png)


[開いているビデオを全画面](improvements-in-visual-studio-2005/_static/usercontrols1.wmv)


> [!NOTE]
> ユーザー コントロールがページから削除されたときに、@Registerディレクティブは、マークアップに残され、Web サイトからユーザー コントロールが削除された場合、パーサー エラーを回避するために手動で削除する必要があります。


Visual Studio のコンパイル モデル内の別の向上は、Web サイトの発行の機能です。 パブリッシュ機能は、Web サイトをプリコンパイル、ために、開発者は要求時に何もコンパイルする必要がないの追加されたパフォーマンスを利用できます。 これもがプリコンパイル アプリ/_Code フォルダー内のすべてのソース コードの DLL に配置するソース コードを持たないようにします。


![Web サイトの発行ダイアログ ボックス](improvements-in-visual-studio-2005/_static/image7.jpg)

**図 10**: Web サイトの発行ダイアログ ボックス


> [!NOTE]
> Aspnet/_compile.exe ユーティリティは、ASP.NET Web アプリケーションをプリコンパイルするも使用できます。 ツールは、モジュール 9 で取り上げます。


公開 Web サイトをプリコンパイル済みのファイルが格納されている場合 Temporary ASP.NET Files フォルダーに次のようにします。 ファイルが、 *.compiled*ファイル拡張子が dll の特定の依存関係を定義する XML ファイルです。 Web フォームまたはユーザー コントロールが始まるランダムの Dll にコンパイルされる*アプリ/_Web/_*です。

ままにする場合、*このプリコンパイル済みサイトを更新できるように*チェック ボックスをオンになって、Webforms とユーザー コントロールの内部でのマークアップを展開後に変更を設定するための DLL にコンパイル済みにすることはできません。 場合は、展開されたコンテンツへの変更は許可されませんが、マークアップをロックする場合は、このボックスをオフにします。

*固定名およびシングル ページ アセンブリを使用する* チェック ボックスでは、各ページは固定という名前のアセンブリにコンパイルできるように、バッチ コンパイルを無効にすることができます。 このボックスをオフにしたままにすると、バッチ コンパイルを利用することができます。

*プリコンパイル済みアセンブリに厳密な名前を有効にする* チェック ボックスでは、厳密な名前に、プリコンパイル済みのアセンブリ。

> [!NOTE]
> ASP.NET で 1.x では、厳密な名前付きアセンブリをグローバル アセンブリ キャッシュ (GAC) をインストールする必要があります。 ASP.NET 2.0 の厳密な名前付きアセンブリを GAC にインストールする必要はありません。


![ASP.NET アプリケーションのコンパイル済みファイル](improvements-in-visual-studio-2005/_static/image8.jpg)

**図 11**: ASP.NET アプリケーションのコンパイル済みファイル


> [!NOTE]
> 上記のアプリケーションでは、web.config ファイルはありませんでした。 あった場合、これが呼び出された*PrecompiledApp.config* Web の発行後にサイトのプロセスです。


## <a name="improvements-in-deployment"></a>展開の機能強化

Visual Studio の 2002 と 2003 では、Visual Studio 2005 機能が用意されてプロジェクトのコピー。 ただし、機能は、Visual Studio 2005 で強化されて、Web サイトのコピーの名称が。

Web サイトのコピー ダイアログは、左側のフレームと右側のフレームに分割されます。 左側のフレームは、ソース Web サイトと呼ばれ、右側のフレームは、リモートの Web サイトと呼ばれます。 一部の開発者が混乱ことの 1 つは右側のフレームに表示されるサイトがある点とは限りませんリモート サイトです。 ローカル ファイル システムまたは IIS のローカル インスタンス上のサイトがある可能性があります。 さらに、左側のフレームに表示されるサイトが必ずしも、ソース Web サイトあるダイアログ ボックスでは、リモートの Web サイトから発行することができます*に*ソース Web サイトです。

リモート Web サイトに、プロジェクトをコピーする場合、そのサイトは、FrontPage Server Extensions がインストールされていることが必要です。 そうでない場合は、FTP を使用して接続する必要があります。 その一方で、IIS のローカル インスタンスにプロジェクトをコピーする場合の FrontPage Server Extensions は必要ありません。

> [!NOTE]
> ローカル IIS インスタンスで新しい Web サイトを作成しようとする、FrontPage 2002 Server Extensions がインストールされている場合は、Web サイトの作成はサポートされていないこと、SharePoint サーバーを示すエラー メッセージが表示されます。 その場合は、2000年の FrontPage Server Extensions のインストールまたは FrontPage Server Extensions を削除するオプションがあります。


Web サイトのコピー機能のビデオ チュートリアルについてはここをクリックします。


![](improvements-in-visual-studio-2005/_static/image4.png)


[開いているビデオを全画面](improvements-in-visual-studio-2005/_static/copysite1.wmv)


## <a name="improvements-in-debugging"></a>デバッグ機能の強化

これが、Visual Studio 2005 でのデバッグに 4 つのキー向上します。

- 非管理者としてローカルでのデバッグは、すぐに可能性があります。
- Compilation 要素に Debug 属性は、既定値はようになりました。
- リモート デバッグのセットアップと構成は、前より簡単です。
- FTP の場所を使用して開いた Web サイトをデバッグできます。

## <a name="debugging-as-a-non-administrator"></a>非管理者としてデバッグ

ASP.NET 開発サーバーの追加は、管理者以外のユーザー-すぐ ASP.NET アプリケーションを簡単にデバッグできます。 ローカル ファイル システムで実行されている ASP.NET アプリケーションのデバッグ時に、Visual Studio は、ログオン ユーザーのコンテキストで ASP.NET 開発サーバーを起動します。 そのユーザーは、追加の構成なしには、そのアプリケーションをデバッグできます。

## <a name="debug-is-false-by-default"></a>デバッグは、False を既定では

ASP.NET で 1.x では、*デバッグ*属性、*コンパイル*、web.config ファイルの要素に設定された*true*既定です。 これが常に推奨の開発者がこの属性を設定する*false* 、実稼働環境にアプリケーションを展開する前にほとんどの開発者がデバッグ属性を設定するを残すような影響を完全に理解しないため、true の場合、単に出るはします。

最も重大な問題を true に設定が ASP.NETs バッチ コンパイル モデルを無効にすることが debug 属性を持つを使用します。 したがって、各ページは、別個の DLL にコンパイルされます。 意味する Web アプリケーションは、数千のページ (いない認識のすべての手段) で構成される場合、1000 単位の複数の小さな Dll がそのアプリケーションによって作成されます。 これらの Dll は、サイズの小さいが、されないメモリ内の特定の位置に読み込まれます。 そのため、システム メモリ内の断片化が発生し、OutOfMemoryException の発生を行うことができます。

ASP.NET 2.0 で debug 属性は既定で false に設定します。 既にきたよう、開発者が Visual Studio 2005 で、ASP.NET アプリケーションをデバッグする場合は、デバッグを有効にする web.config ファイルを追加するように求められます。 ASP.NET で存在していた同じ欠点を負担そう 1.x が、今すぐ開発者明確に通知する警告が実稼働環境にアプリケーションを移行する前に、false に属性をリセットする必要があります。

## <a name="remote-debugging-setup-and-configuration"></a>リモート デバッグのセットアップと構成

Visual Studio の 2002年/2003 でのリモート デバッグ マシン デバッグ マネージャー (mdm.exe) および vs7jit.exe プロセスに依存します。 そのため、リモート デバッグの問題のトラブルシューティングが、多くの顧客の黒いボックスおよび PSS の方が、ほとんどの場合。

Visual Studio 2005 では、mdm.exe と vs7jit.exe プロセスへの依存を削除します。 代わりに、現在使用して、リモート デバッグ モニター (msvsmon.exe) をサービス

Visual Studio 2005 でリモートでデバッグするための要件は、非常にシンプルです。 デバッグする前に、リモート サーバーで msvsmon.exe を実行する必要があります。 リモート デバッグ モニターをインストールするには、Visual Studio CD からか、Web サーバー上で何もインストールせず、共有から msvsmon.exe を実行することだけことができます。

Msvsmon.exe を実行するときに、リモート デバッグがブロックされているポートの不満がある可能性があります。 幸いにも、簡単にブロックを解除できます警告ダイアログ ボックスで右からポート次のようにします。


![Windows ファイアウォールは、リモート デバッグをブロックしている通知](improvements-in-visual-studio-2005/_static/image9.jpg)

**図 12**: Windows ファイアウォールの通知はリモート デバッグをブロック


デバッグに必要なポートのブロックを解除して後は、次に示すように、リモート デバッグ モニターが表示されます。 このインターフェイスからは、接続を監視し、変更する権限を簡単にデバッグできます。


![リモート デバッグ モニター](improvements-in-visual-studio-2005/_static/image10.jpg)

**図 13**: リモート デバッグ モニター


FTP 経由で開かれた Web アプリケーションをリモートでデバッグすることもできます。 手順は、以前説明と同じです。 ただし、このモジュールで既に説明したように FTP プロジェクトの参照をベース URL を指定する必要があります。

## <a name="lab-2"></a>ラボ 2

## <a name="remote-debugging-with-visual-studio-2005"></a>Visual Studio 2005 でのリモート デバッグ

このラボでは、Visual Studio 2005 でのリモート デバッグを説明します。

このラボのビデオ チュートリアルについては、ここをクリックします。


![](improvements-in-visual-studio-2005/_static/image5.png)


[開いているビデオを全画面](improvements-in-visual-studio-2005/_static/remdebug1.wmv)


このラボでは、1 つの実行中の Visual Studio 2005 と、その他の実行されている IIS 5 以上、2 つのマシンがある必要があります。

1. Visual Studio 2005 を開き、リモート サーバーで新しい Web サイトを作成します。

> [!NOTE]
> リモートの IIS インスタンス、または FTP を使用して、Web サイトを作成できます。


1. リモートの Web サーバーから UNC パスを使用して開発用コンピューターで msvsmon.exe を検索し、それを実行します。  
 既定の場所 msvsmon.exe は、//server/c$/Program ファイル/Microsoft Visual Studio 8/Common7/IDE/リモート デバッガー/x86 です。
2. リモート デバッグ用のポートのブロックを解除するメッセージが表示されたら、ようになります。
3. 開発用コンピューターから、Default.aspx の分離コードを開き、ページ/(_l) メソッドにブレークポイントを設定します。
4. 開発用コンピューターからデバッグを開始します。

期待どおりには、ブレークポイントをヒットする必要があります。

## <a name="aspnet-development-server"></a>ASP.NET 開発サーバー

既に説明したようにこれまで、として Visual Studio 2005 は、ASP.NET 開発サーバーをという名前の Web サーバーに付属します。 (ASP.NET 開発サーバーが呼ばれます Cassini として。)この Web サーバーは、[参照] をファイル システムで実行されている Web アプリケーションをデバッグする便利な手段です。

ASP.NET 開発サーバーとは、制限付きの Web サーバーです。 リモート接続を許可しないこと、Web サーバーを開始したユーザー以外のユーザーからの要求はできません。 またがないと、ASP ページの提供の機能です。 ASP.NET のリソースと HTML リソース (画像、CSS ファイルなどを含む) だけが処理されます。

C:/Windows/Microsoft.NET/Framework/v2.0./ にある WebDev.WebServer.exe ファイルを実行して、コマンドラインを使用して、ASP.NET 開発サーバーを起動できる*/*  /  */*/*. 次のダイアログ ボックスには、使用可能なパラメーターが表示されます。


![](improvements-in-visual-studio-2005/_static/image11.jpg)

**図 14**


> [!NOTE]
> コマンドラインを使用して明示的に起動されたときに、ASP.NET 開発サーバーがサポートされていません。
