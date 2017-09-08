---
title: "ASP.NET MVC を持つコアを Entity Framework Core - 10 のチュートリアル 1"
author: tdykstra
description: 
keywords: "ASP.NET Core、Entity Framework Core、チュートリアル"
ms.author: tdykstra
manager: wpickett
ms.date: 03/15/2017
ms.topic: get-started-article
ms.assetid: b67c3d4a-f2bf-4132-a48b-4b0d599d7981
ms.technology: aspnet
ms.prod: asp.net-core
uid: data/ef-mvc/intro
ms.openlocfilehash: b8ef101458e0a6e6284624693689181646ced051
ms.sourcegitcommit: 5355c96a1768e5a1d5698a98c190e7addcc4ded5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/05/2017
---
# <a name="getting-started-with-aspnet-core-mvc-and-entity-framework-core-using-visual-studio-1-of-10"></a><span data-ttu-id="b67dc-103">ASP.NET Core MVC と Visual Studio (10 の 1) を使用して Entity Framework Core の概要</span><span class="sxs-lookup"><span data-stu-id="b67dc-103">Getting started with ASP.NET Core MVC and Entity Framework Core using Visual Studio (1 of 10)</span></span>

<span data-ttu-id="b67dc-104">によって[Tom Dykstra](https://github.com/tdykstra)と[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="b67dc-104">By [Tom Dykstra](https://github.com/tdykstra) and [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="b67dc-105">Contoso 大学でサンプル web アプリケーションでは、Entity Framework (EF) コア 2.0 と Visual Studio 2017 を使用して ASP.NET Core 2.0 MVC web アプリケーションを作成する方法を示します。</span><span class="sxs-lookup"><span data-stu-id="b67dc-105">The Contoso University sample web application demonstrates how to create ASP.NET Core 2.0 MVC web applications using Entity Framework (EF) Core 2.0 and Visual Studio 2017.</span></span>

<span data-ttu-id="b67dc-106">サンプル アプリケーションは、架空の Contoso 大学の web サイトです。</span><span class="sxs-lookup"><span data-stu-id="b67dc-106">The sample application is a web site for a fictional Contoso University.</span></span> <span data-ttu-id="b67dc-107">学生受付、コースの作成、およびインストラクター割り当てなどの機能が含まれています。</span><span class="sxs-lookup"><span data-stu-id="b67dc-107">It includes functionality such as student admission, course creation, and instructor assignments.</span></span> <span data-ttu-id="b67dc-108">これは、最初の一連の最初から Contoso 大学サンプル アプリケーションをビルドする方法を説明するチュートリアルです。</span><span class="sxs-lookup"><span data-stu-id="b67dc-108">This is the first in a series of tutorials that explain how to build the Contoso University sample application from scratch.</span></span>

[<span data-ttu-id="b67dc-109">ダウンロードまたは完成したアプリケーションを表示します。</span><span class="sxs-lookup"><span data-stu-id="b67dc-109">Download or view the completed application.</span></span>](https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-mvc/intro/samples/cu-final)

<span data-ttu-id="b67dc-110">EF の最新バージョンであるが EF のすべての機能がない、EF コア 2.0 6.x です。</span><span class="sxs-lookup"><span data-stu-id="b67dc-110">EF Core 2.0 is the latest version of EF but does not yet have all the features of EF 6.x.</span></span> <span data-ttu-id="b67dc-111">EF との間を選択する方法については 6.x と EF コアを参照してください。 [EF コア vs です。EF6.x](https://docs.microsoft.com/ef/efcore-and-ef6/)です。</span><span class="sxs-lookup"><span data-stu-id="b67dc-111">For information about how to choose between EF 6.x and EF Core, see [EF Core vs. EF6.x](https://docs.microsoft.com/ef/efcore-and-ef6/).</span></span> <span data-ttu-id="b67dc-112">EF を選択した場合、6.x を参照してください[このチュートリアル シリーズの以前のバージョン](https://docs.microsoft.com/aspnet/mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application)します。</span><span class="sxs-lookup"><span data-stu-id="b67dc-112">If you choose EF 6.x, see [the previous version of this tutorial series](https://docs.microsoft.com/aspnet/mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application).</span></span>

> [!NOTE]
> * <span data-ttu-id="b67dc-113">このチュートリアルの ASP.NET Core の 1.1 バージョンを参照してください、 [VS 2017 Update 2 のバージョンを PDF 形式では、このチュートリアルの](https://github.com/aspnet/Docs/blob/master/aspnetcore/data/efmvc/intro/_static/efmvc1.1.pdf)します。</span><span class="sxs-lookup"><span data-stu-id="b67dc-113">For the ASP.NET Core 1.1 version of this tutorial, see the [VS 2017 Update 2 version of this tutorial in PDF format](https://github.com/aspnet/Docs/blob/master/aspnetcore/data/efmvc/intro/_static/efmvc1.1.pdf).</span></span>
> * <span data-ttu-id="b67dc-114">このチュートリアルの Visual Studio 2015 バージョンを参照してください、 [VS 2015 バージョンの PDF 形式での ASP.NET Core ドキュメント](https://github.com/aspnet/Docs/blob/master/aspnetcore/common/_static/aspnet-core-project-json.pdf)です。</span><span class="sxs-lookup"><span data-stu-id="b67dc-114">For the Visual Studio 2015 version of this tutorial, see the [VS 2015 version of ASP.NET Core documentation in PDF format](https://github.com/aspnet/Docs/blob/master/aspnetcore/common/_static/aspnet-core-project-json.pdf).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b67dc-115">必須コンポーネント</span><span class="sxs-lookup"><span data-stu-id="b67dc-115">Prerequisites</span></span>

[!INCLUDE[install 2.0](../../includes/install2.0.md)]

## <a name="troubleshooting"></a><span data-ttu-id="b67dc-116">トラブルシューティング</span><span class="sxs-lookup"><span data-stu-id="b67dc-116">Troubleshooting</span></span>

<span data-ttu-id="b67dc-117">問題を解決できない場合に発生した場合、コードを比較することでのソリューションを見つけることは通常、[完成したプロジェクト](https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-mvc/intro/samples/cu-final)です。</span><span class="sxs-lookup"><span data-stu-id="b67dc-117">If you run into a problem you can't resolve, you can generally find the solution by comparing your code to the [completed project](https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-mvc/intro/samples/cu-final).</span></span> <span data-ttu-id="b67dc-118">一般的なエラーとそれらを解決する方法の一覧は、次を参照してください。[系列の最後のチュートリアルの「トラブルシューティング](advanced.md#common-errors)です。</span><span class="sxs-lookup"><span data-stu-id="b67dc-118">For a list of common errors and how to solve them, see [the Troubleshooting section of the last tutorial in the series](advanced.md#common-errors).</span></span> <span data-ttu-id="b67dc-119">必要なものがない場合は、StackOverflow.com に質問を投稿することができます[ASP.NET Core](http://stackoverflow.com/questions/tagged/asp.net-core)または[EF コア](http://stackoverflow.com/questions/tagged/entity-framework-core)です。</span><span class="sxs-lookup"><span data-stu-id="b67dc-119">If you don't find what you need there, you can post a question to StackOverflow.com for  [ASP.NET Core](http://stackoverflow.com/questions/tagged/asp.net-core) or [EF Core](http://stackoverflow.com/questions/tagged/entity-framework-core).</span></span>

> [!TIP] 
> <span data-ttu-id="b67dc-120">これは、一連の 10 のチュートリアルでは、それぞれは、前のチュートリアルの処理に基づいています。</span><span class="sxs-lookup"><span data-stu-id="b67dc-120">This is a series of 10 tutorials, each of which builds on what is done in earlier tutorials.</span></span>  <span data-ttu-id="b67dc-121">各チュートリアルが正常に完了した後、プロジェクトのコピーを保存することを検討してください。</span><span class="sxs-lookup"><span data-stu-id="b67dc-121">Consider saving a copy of the project after each successful tutorial completion.</span></span>  <span data-ttu-id="b67dc-122">問題に遭遇した場合は、前のチュートリアルの一連の先頭に戻るとではなく、経由で開始できます。</span><span class="sxs-lookup"><span data-stu-id="b67dc-122">Then if you run into problems, you can start over from the previous tutorial instead of going back to the beginning of the whole series.</span></span>

## <a name="the-contoso-university-web-application"></a><span data-ttu-id="b67dc-123">Contoso 大学 web アプリケーション</span><span class="sxs-lookup"><span data-stu-id="b67dc-123">The Contoso University web application</span></span>

<span data-ttu-id="b67dc-124">これらのチュートリアルで構築するアプリケーションは、単純な大学 web サイトです。</span><span class="sxs-lookup"><span data-stu-id="b67dc-124">The application you'll be building in these tutorials is a simple university web site.</span></span>

<span data-ttu-id="b67dc-125">ユーザーでは、表示でき、学生、コース、インストラクターの情報を更新することができます。</span><span class="sxs-lookup"><span data-stu-id="b67dc-125">Users can view and update student, course, and instructor information.</span></span> <span data-ttu-id="b67dc-126">ここでは、いくつかの画面を作成します。</span><span class="sxs-lookup"><span data-stu-id="b67dc-126">Here are a few of the screens you'll create.</span></span>

![インデックス ページの受講者](intro/_static/students-index.png)

![受講者の編集 ページ](intro/_static/student-edit.png)

<span data-ttu-id="b67dc-129">このサイトの UI スタイルを維持して組み込みのテンプレートによって生成されたものに近いチュートリアルは、Entity Framework を使用する方法の主に集中することです。</span><span class="sxs-lookup"><span data-stu-id="b67dc-129">The UI style of this site has been kept close to what's generated by the built-in templates, so that the tutorial can focus mainly on how to use the Entity Framework.</span></span>

## <a name="create-an-aspnet-core-mvc-web-application"></a><span data-ttu-id="b67dc-130">ASP.NET Core MVC web アプリケーションを作成します。</span><span class="sxs-lookup"><span data-stu-id="b67dc-130">Create an ASP.NET Core MVC web application</span></span>

<span data-ttu-id="b67dc-131">Visual Studio を開き、新しい ASP.NET Core c# web という名前のプロジェクト"ContosoUniversity"を作成します。</span><span class="sxs-lookup"><span data-stu-id="b67dc-131">Open Visual Studio and create a new ASP.NET Core C# web project named "ContosoUniversity".</span></span>

* <span data-ttu-id="b67dc-132">**ファイル**メニューの **新規 > プロジェクト**です。</span><span class="sxs-lookup"><span data-stu-id="b67dc-132">From the **File** menu, select **New > Project**.</span></span>

* <span data-ttu-id="b67dc-133">左側のウィンドウから次のように選択します。**インストール > Visual c# > Web**です。</span><span class="sxs-lookup"><span data-stu-id="b67dc-133">From the left pane, select **Installed > Visual C# > Web**.</span></span>

* <span data-ttu-id="b67dc-134">選択、 **ASP.NET Core Web アプリケーション**プロジェクト テンプレート。</span><span class="sxs-lookup"><span data-stu-id="b67dc-134">Select the **ASP.NET Core Web Application** project template.</span></span>

* <span data-ttu-id="b67dc-135">入力**ContosoUniversity**クリックと名前として**OK**です。</span><span class="sxs-lookup"><span data-stu-id="b67dc-135">Enter **ContosoUniversity** as the name and click **OK**.</span></span>

  ![[新しいプロジェクト] ダイアログ](intro/_static/new-project.png)

* <span data-ttu-id="b67dc-137">待って、**新しい ASP.NET Core Web アプリケーション (.NET Core)**ダイアログを表示するには</span><span class="sxs-lookup"><span data-stu-id="b67dc-137">Wait for the **New ASP.NET Core Web Application (.NET Core)** dialog to appear</span></span>

* <span data-ttu-id="b67dc-138">選択**ASP.NET Core 2.0**と**Web アプリケーション (モデル-ビュー-コント ローラー)**テンプレート。</span><span class="sxs-lookup"><span data-stu-id="b67dc-138">Select **ASP.NET Core 2.0** and the **Web Application (Model-View-Controller)** template.</span></span>

  <span data-ttu-id="b67dc-139">**注:**このチュートリアルでは、ASP.NET Core 2.0 と EF コア 2.0 以降--、以下のことを確認が必要です**ASP.NET Core 1.1**が選択されていません。</span><span class="sxs-lookup"><span data-stu-id="b67dc-139">**Note:** This tutorial requires ASP.NET Core 2.0 and EF Core 2.0 or later -- make sure that **ASP.NET Core 1.1** is not selected.</span></span>

* <span data-ttu-id="b67dc-140">確認**認証**に設定されている**認証なし**です。</span><span class="sxs-lookup"><span data-stu-id="b67dc-140">Make sure **Authentication** is set to **No Authentication**.</span></span>

* <span data-ttu-id="b67dc-141">[OK] をクリックします。 ****</span><span class="sxs-lookup"><span data-stu-id="b67dc-141">Click **OK**</span></span>

  ![新しい ASP.NET プロジェクト ダイアログ ボックス](intro/_static/new-aspnet.png)

## <a name="set-up-the-site-style"></a><span data-ttu-id="b67dc-143">サイトのスタイルを設定します。</span><span class="sxs-lookup"><span data-stu-id="b67dc-143">Set up the site style</span></span>

<span data-ttu-id="b67dc-144">いくつかの簡単な変更は、[サイト] メニューのレイアウト、およびホーム ページを設定します。</span><span class="sxs-lookup"><span data-stu-id="b67dc-144">A few simple changes will set up the site menu, layout, and home page.</span></span>

<span data-ttu-id="b67dc-145">開いている*Views/Shared/_Layout.cshtml*次の変更を加えます。</span><span class="sxs-lookup"><span data-stu-id="b67dc-145">Open *Views/Shared/_Layout.cshtml* and make the following changes:</span></span>

* <span data-ttu-id="b67dc-146">「Contoso 大学」を"ContosoUniversity"の各出現する位置を変更します。</span><span class="sxs-lookup"><span data-stu-id="b67dc-146">Change each occurrence of "ContosoUniversity" to "Contoso University".</span></span> <span data-ttu-id="b67dc-147">次の 3 つの出現があります。</span><span class="sxs-lookup"><span data-stu-id="b67dc-147">There are three occurrences.</span></span>

* <span data-ttu-id="b67dc-148">メニュー エントリを追加**受講者**、**コース**、**講習においてインストラクター**、および**部門**、および削除、 **にお問い合わせください**メニュー エントリです。</span><span class="sxs-lookup"><span data-stu-id="b67dc-148">Add menu entries for **Students**, **Courses**, **Instructors**, and **Departments**, and delete the **Contact** menu entry.</span></span>

<span data-ttu-id="b67dc-149">変更が強調表示されます。</span><span class="sxs-lookup"><span data-stu-id="b67dc-149">The changes are highlighted.</span></span>

[!code-html[](intro/samples/cu/Views/Shared/_Layout.cshtml?highlight=6,30,36-39,48)]

<span data-ttu-id="b67dc-150">*Views/Home/Index.cshtml*ファイルの内容をこのアプリケーションについてのテキストで ASP.NET と MVC に関するテキストを置き換える次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="b67dc-150">In *Views/Home/Index.cshtml*, replace the contents of the file with the following code to replace the text about ASP.NET and MVC with text about this application:</span></span>

[!code-html[](intro/samples/cu/Views/Home/Index.cshtml)]

<span data-ttu-id="b67dc-151">CTRL + f5 キーを押してプロジェクトを実行または選択**デバッグ > デバッグなしで開始** メニューからです。</span><span class="sxs-lookup"><span data-stu-id="b67dc-151">Press CTRL+F5 to run the project or choose **Debug > Start Without Debugging** from the menu.</span></span> <span data-ttu-id="b67dc-152">これらのチュートリアルで作成された、ページのタブで、ホーム ページを参照してください。</span><span class="sxs-lookup"><span data-stu-id="b67dc-152">You see the home page with tabs for the pages you'll create in these tutorials.</span></span>

![Contoso 大学のホーム ページ](intro/_static/home-page.png)

## <a name="entity-framework-core-nuget-packages"></a><span data-ttu-id="b67dc-154">Entity Framework Core NuGet パッケージの管理</span><span class="sxs-lookup"><span data-stu-id="b67dc-154">Entity Framework Core NuGet packages</span></span>

<span data-ttu-id="b67dc-155">プロジェクトに EF Core のサポートを追加するには、対象となるデータベース プロバイダーをインストールします。</span><span class="sxs-lookup"><span data-stu-id="b67dc-155">To add EF Core support to a project, install the database provider that you want to target.</span></span> <span data-ttu-id="b67dc-156">このチュートリアルは、SQL Server を使用し、プロバイダー パッケージ[Microsoft.EntityFrameworkCore.SqlServer](https://www.nuget.org/packages/Microsoft.EntityFrameworkCore.SqlServer/)です。</span><span class="sxs-lookup"><span data-stu-id="b67dc-156">This tutorial uses SQL Server, and the provider package is [Microsoft.EntityFrameworkCore.SqlServer](https://www.nuget.org/packages/Microsoft.EntityFrameworkCore.SqlServer/).</span></span> <span data-ttu-id="b67dc-157">このパッケージに含まれる、 [Microsoft.AspNetCore.All](xref:fundamentals/metapackage) metapackage、ためをインストールする必要はありません。</span><span class="sxs-lookup"><span data-stu-id="b67dc-157">This package is included in the [Microsoft.AspNetCore.All](xref:fundamentals/metapackage) metapackage, so you don't have to install it.</span></span>

<span data-ttu-id="b67dc-158">このパッケージとその依存関係 (`Microsoft.EntityFrameworkCore`と`Microsoft.EntityFrameworkCore.Relational`) EF のランタイム サポートを提供します。</span><span class="sxs-lookup"><span data-stu-id="b67dc-158">This package and its dependencies (`Microsoft.EntityFrameworkCore` and `Microsoft.EntityFrameworkCore.Relational`) provide runtime support for EF.</span></span> <span data-ttu-id="b67dc-159">ツール パッケージを追加後の「、[移行](migrations.md)チュートリアルです。</span><span class="sxs-lookup"><span data-stu-id="b67dc-159">You'll add a tooling package later, in the [Migrations](migrations.md) tutorial.</span></span> 

<span data-ttu-id="b67dc-160">Entity Framework のコアで利用可能なその他のデータベース プロバイダーについては、次を参照してください。[データベース プロバイダー](https://docs.microsoft.com/ef/core/providers/)です。</span><span class="sxs-lookup"><span data-stu-id="b67dc-160">For information about other database providers that are available for Entity Framework Core, see [Database providers](https://docs.microsoft.com/ef/core/providers/).</span></span>

## <a name="create-the-data-model"></a><span data-ttu-id="b67dc-161">データ モデルを作成します。</span><span class="sxs-lookup"><span data-stu-id="b67dc-161">Create the data model</span></span>

<span data-ttu-id="b67dc-162">次に、Contoso 大学アプリケーション用にエンティティ クラスを作成します。</span><span class="sxs-lookup"><span data-stu-id="b67dc-162">Next you'll create entity classes for the Contoso University application.</span></span> <span data-ttu-id="b67dc-163">次の 3 つのエンティティを開始します。</span><span class="sxs-lookup"><span data-stu-id="b67dc-163">You'll start with the following three entities.</span></span>

![受講者コース-登録データ モデルのダイアグラム](intro/_static/data-model-diagram.png)

<span data-ttu-id="b67dc-165">一対多の関係がある`Student`と`Enrollment`エンティティ、一対多の関係があると`Course`と`Enrollment`エンティティです。</span><span class="sxs-lookup"><span data-stu-id="b67dc-165">There's a one-to-many relationship between `Student` and `Enrollment` entities, and there's a one-to-many relationship between `Course` and `Enrollment` entities.</span></span> <span data-ttu-id="b67dc-166">つまり、任意の数に、コースの受講者を登録して、コースに受講者に、登録の任意の数を持つことができます。</span><span class="sxs-lookup"><span data-stu-id="b67dc-166">In other words, a student can be enrolled in any number of courses, and a course can have any number of students enrolled in it.</span></span>

<span data-ttu-id="b67dc-167">次のセクションでは、これらのエンティティのいずれかのクラスを作成します。</span><span class="sxs-lookup"><span data-stu-id="b67dc-167">In the following sections you'll create a class for each one of these entities.</span></span>

### <a name="the-student-entity"></a><span data-ttu-id="b67dc-168">学生エンティティ</span><span class="sxs-lookup"><span data-stu-id="b67dc-168">The Student entity</span></span>

![学生のエンティティの図](intro/_static/student-entity.png)

<span data-ttu-id="b67dc-170">*モデル*フォルダー、という名前のクラス ファイルを作成する*Student.cs*テンプレート コードを次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="b67dc-170">In the *Models* folder, create a class file named *Student.cs* and replace the template code with the following code.</span></span>

<span data-ttu-id="b67dc-171">[!code-csharp[Main](intro/samples/cu/Models/Student.cs?name=snippet_Intro)]</span><span class="sxs-lookup"><span data-stu-id="b67dc-171">[!code-csharp[Main](intro/samples/cu/Models/Student.cs?name=snippet_Intro)]</span></span>

<span data-ttu-id="b67dc-172">`ID`プロパティは、このクラスに対応するデータベース テーブルの主キー列になります。</span><span class="sxs-lookup"><span data-stu-id="b67dc-172">The `ID` property will become the primary key column of the database table that corresponds to this class.</span></span> <span data-ttu-id="b67dc-173">既定では、Entity Framework では、解釈というプロパティ`ID`または`classnameID`主キーとして。</span><span class="sxs-lookup"><span data-stu-id="b67dc-173">By default, the Entity Framework interprets a property that's named `ID` or `classnameID` as the primary key.</span></span>

<span data-ttu-id="b67dc-174">`Enrollments`プロパティは、ナビゲーション プロパティ。</span><span class="sxs-lookup"><span data-stu-id="b67dc-174">The `Enrollments` property is a navigation property.</span></span> <span data-ttu-id="b67dc-175">ナビゲーション プロパティは、このエンティティに関連するその他のエンティティを保持します。</span><span class="sxs-lookup"><span data-stu-id="b67dc-175">Navigation properties hold other entities that are related to this entity.</span></span> <span data-ttu-id="b67dc-176">ここで、`Enrollments`のプロパティ、`Student entity`のすべてを保持する、`Enrollment`に関連付けられているエンティティ`Student`エンティティです。</span><span class="sxs-lookup"><span data-stu-id="b67dc-176">In this case, the `Enrollments` property of a `Student entity` will hold all of the `Enrollment` entities that are related to that `Student` entity.</span></span> <span data-ttu-id="b67dc-177">つまり場合、データベース内の特定の学生行が関連する 2 つ登録行 (その StudentID 外部キー列に、そのスチューデントの主キーの値が含まれている行) を`Student`エンティティの`Enrollments`ナビゲーション プロパティで、それらが格納されます2 つ`Enrollment`エンティティです。</span><span class="sxs-lookup"><span data-stu-id="b67dc-177">In other words, if a given Student row in the database has two related Enrollment rows (rows that contain that student's primary key value in their StudentID foreign key column), that `Student` entity's `Enrollments` navigation property will contain those two `Enrollment` entities.</span></span>

<span data-ttu-id="b67dc-178">その型が一覧にエントリを追加、削除すると、更新できるなどをする必要があります、ナビゲーション プロパティ (多対多または一対多のリレーションシップ) のように複数のエンティティに保持できる場合`ICollection<T>`です。</span><span class="sxs-lookup"><span data-stu-id="b67dc-178">If a navigation property can hold multiple entities (as in many-to-many or one-to-many relationships), its type must be a list in which entries can be added, deleted, and updated, such as `ICollection<T>`.</span></span>  <span data-ttu-id="b67dc-179">指定できます`ICollection<T>`またはなど型`List<T>`または`HashSet<T>`です。</span><span class="sxs-lookup"><span data-stu-id="b67dc-179">You can specify `ICollection<T>` or a type such as `List<T>` or `HashSet<T>`.</span></span> <span data-ttu-id="b67dc-180">指定した場合`ICollection<T>`、EF の作成、`HashSet<T>`既定のコレクション。</span><span class="sxs-lookup"><span data-stu-id="b67dc-180">If you specify `ICollection<T>`, EF creates a `HashSet<T>` collection by default.</span></span>

### <a name="the-enrollment-entity"></a><span data-ttu-id="b67dc-181">登録エンティティ</span><span class="sxs-lookup"><span data-stu-id="b67dc-181">The Enrollment entity</span></span>

![エンティティの登録の図](intro/_static/enrollment-entity.png)

<span data-ttu-id="b67dc-183">*モデル*フォルダー作成*Enrollment.cs*し、既存のコードを次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="b67dc-183">In the *Models* folder, create *Enrollment.cs* and replace the existing code with the following code:</span></span>

<span data-ttu-id="b67dc-184">[!code-csharp[Main](intro/samples/cu/Models/Enrollment.cs?name=snippet_Intro)]</span><span class="sxs-lookup"><span data-stu-id="b67dc-184">[!code-csharp[Main](intro/samples/cu/Models/Enrollment.cs?name=snippet_Intro)]</span></span>

<span data-ttu-id="b67dc-185">`EnrollmentID`プロパティは、主キーになります。 このエンティティを使用して、`classnameID`パターンの代わりに`ID`で学習したとしてそれ自体で、`Student`エンティティです。</span><span class="sxs-lookup"><span data-stu-id="b67dc-185">The `EnrollmentID` property will be the primary key; this entity uses the `classnameID` pattern instead of `ID` by itself as you saw in the `Student` entity.</span></span> <span data-ttu-id="b67dc-186">通常 1 つパターンを選択し、データ モデル全体で使用するとします。</span><span class="sxs-lookup"><span data-stu-id="b67dc-186">Ordinarily you would choose one pattern and use it throughout your data model.</span></span> <span data-ttu-id="b67dc-187">ここでは、いずれかのパターンを使用することができます、バリエーションを示しています。</span><span class="sxs-lookup"><span data-stu-id="b67dc-187">Here, the variation illustrates that you can use either pattern.</span></span> <span data-ttu-id="b67dc-188">[後のチュートリアル](inheritance.md)、classname せず ID を使用して簡単方法、データ モデルで継承の実装が表示されます。</span><span class="sxs-lookup"><span data-stu-id="b67dc-188">In a [later tutorial](inheritance.md), you'll see how using ID without classname makes it easier to implement inheritance in the data model.</span></span>

<span data-ttu-id="b67dc-189">`Grade`プロパティは、`enum`です。</span><span class="sxs-lookup"><span data-stu-id="b67dc-189">The `Grade` property is an `enum`.</span></span> <span data-ttu-id="b67dc-190">後に疑問符 ()、`Grade`型宣言では、ことを示します、`Grade`プロパティが null 値を許容します。</span><span class="sxs-lookup"><span data-stu-id="b67dc-190">The question mark after the `Grade` type declaration indicates that the `Grade` property is nullable.</span></span> <span data-ttu-id="b67dc-191">Null である評価とは異なる、ゼロ グレード--null またはため、評価はまだ割り当てられていません。</span><span class="sxs-lookup"><span data-stu-id="b67dc-191">A grade that's null is different from a zero grade -- null means a grade isn't known or hasn't been assigned yet.</span></span>

<span data-ttu-id="b67dc-192">`StudentID`プロパティは、foreign key、および対応するナビゲーション プロパティは`Student`します。</span><span class="sxs-lookup"><span data-stu-id="b67dc-192">The `StudentID` property is a foreign key, and the corresponding navigation property is `Student`.</span></span> <span data-ttu-id="b67dc-193">`Enrollment`エンティティが 1 つに関連付けられた`Student`エンティティ、プロパティは、1 つのみを保持できるように`Student`エンティティ (とは異なり、`Student.Enrollments`ナビゲーション プロパティ先ほど見た、複数を格納する`Enrollment`エンティティ)。</span><span class="sxs-lookup"><span data-stu-id="b67dc-193">An `Enrollment` entity is associated with one `Student` entity, so the property can only hold a single `Student` entity (unlike the `Student.Enrollments` navigation property you saw earlier, which can hold multiple `Enrollment` entities).</span></span>

<span data-ttu-id="b67dc-194">`CourseID`プロパティは、foreign key、および対応するナビゲーション プロパティは`Course`します。</span><span class="sxs-lookup"><span data-stu-id="b67dc-194">The `CourseID` property is a foreign key, and the corresponding navigation property is `Course`.</span></span> <span data-ttu-id="b67dc-195">`Enrollment`エンティティが 1 つに関連付けられた`Course`エンティティです。</span><span class="sxs-lookup"><span data-stu-id="b67dc-195">An `Enrollment` entity is associated with one `Course` entity.</span></span>

<span data-ttu-id="b67dc-196">Entity Framework がという名前が場合に、外部キーのプロパティとしてプロパティを解釈`<navigation property name><primary key property name>`(たとえば、`StudentID`の`Student`以降のナビゲーション プロパティ、`Student`エンティティの主キーが`ID`)。</span><span class="sxs-lookup"><span data-stu-id="b67dc-196">Entity Framework interprets a property as a foreign key property if it's named `<navigation property name><primary key property name>` (for example, `StudentID` for the `Student` navigation property since the `Student` entity's primary key is `ID`).</span></span> <span data-ttu-id="b67dc-197">外部キー プロパティは単にも呼ばれます`<primary key property name>`(たとえば、`CourseID`ので、`Course`エンティティの主キーが`CourseID`)。</span><span class="sxs-lookup"><span data-stu-id="b67dc-197">Foreign key properties can also be named simply `<primary key property name>` (for example, `CourseID` since the `Course` entity's primary key is `CourseID`).</span></span>

### <a name="the-course-entity"></a><span data-ttu-id="b67dc-198">Course エンティティ</span><span class="sxs-lookup"><span data-stu-id="b67dc-198">The Course entity</span></span>

![Course エンティティの図](intro/_static/course-entity.png)

<span data-ttu-id="b67dc-200">*モデル*フォルダー作成*Course.cs*し、既存のコードを次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="b67dc-200">In the *Models* folder, create *Course.cs* and replace the existing code with the following code:</span></span>

<span data-ttu-id="b67dc-201">[!code-csharp[Main](intro/samples/cu/Models/Course.cs?name=snippet_Intro)]</span><span class="sxs-lookup"><span data-stu-id="b67dc-201">[!code-csharp[Main](intro/samples/cu/Models/Course.cs?name=snippet_Intro)]</span></span>

<span data-ttu-id="b67dc-202">`Enrollments`プロパティは、ナビゲーション プロパティ。</span><span class="sxs-lookup"><span data-stu-id="b67dc-202">The `Enrollments` property is a navigation property.</span></span> <span data-ttu-id="b67dc-203">A`Course`エンティティを任意の数に関連付けることができます`Enrollment`エンティティです。</span><span class="sxs-lookup"><span data-stu-id="b67dc-203">A `Course` entity can be related to any number of `Enrollment` entities.</span></span>

<span data-ttu-id="b67dc-204">ここでの詳細について、`DatabaseGenerated`属性、[後のチュートリアル](complex-data-model.md)この系列にします。</span><span class="sxs-lookup"><span data-stu-id="b67dc-204">We'll say more about the `DatabaseGenerated` attribute in a [later tutorial](complex-data-model.md) in this series.</span></span> <span data-ttu-id="b67dc-205">基本的には、この属性には、それを生成、データベースのではなく、コースのプライマリ キーを入力することができます。</span><span class="sxs-lookup"><span data-stu-id="b67dc-205">Basically, this attribute lets you enter the primary key for the course rather than having the database generate it.</span></span>

## <a name="create-the-database-context"></a><span data-ttu-id="b67dc-206">データベース コンテキストを作成します。</span><span class="sxs-lookup"><span data-stu-id="b67dc-206">Create the Database Context</span></span>

<span data-ttu-id="b67dc-207">指定されたデータ モデルの Entity Framework 機能を調整するのメイン クラスは、データベース コンテキスト クラスです。</span><span class="sxs-lookup"><span data-stu-id="b67dc-207">The main class that coordinates Entity Framework functionality for a given data model is the database context class.</span></span> <span data-ttu-id="b67dc-208">派生することによってこのクラスを作成する、`Microsoft.EntityFrameworkCore.DbContext`クラスです。</span><span class="sxs-lookup"><span data-stu-id="b67dc-208">You create this class by deriving from the `Microsoft.EntityFrameworkCore.DbContext` class.</span></span> <span data-ttu-id="b67dc-209">コードでは、データ モデルのエンティティが含まれているを指定します。</span><span class="sxs-lookup"><span data-stu-id="b67dc-209">In your code you specify which entities are included in the data model.</span></span> <span data-ttu-id="b67dc-210">特定の Entity Framework の動作をカスタマイズすることもできます。</span><span class="sxs-lookup"><span data-stu-id="b67dc-210">You can also customize certain Entity Framework behavior.</span></span> <span data-ttu-id="b67dc-211">クラスの名前は、このプロジェクトで`SchoolContext`です。</span><span class="sxs-lookup"><span data-stu-id="b67dc-211">In this project, the class is named `SchoolContext`.</span></span>

<span data-ttu-id="b67dc-212">プロジェクト フォルダー内には、という名前のフォルダーを作成*データ*です。</span><span class="sxs-lookup"><span data-stu-id="b67dc-212">In the project folder, create a folder named *Data*.</span></span>

<span data-ttu-id="b67dc-213">*データ*という新しいクラス ファイルを作成するフォルダー *SchoolContext.cs*、テンプレート コードを次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="b67dc-213">In the *Data* folder create a new class file named *SchoolContext.cs*, and replace the template code with the following code:</span></span>

<span data-ttu-id="b67dc-214">[!code-csharp[Main](intro/samples/cu/Data/SchoolContext.cs?name=snippet_Intro)]</span><span class="sxs-lookup"><span data-stu-id="b67dc-214">[!code-csharp[Main](intro/samples/cu/Data/SchoolContext.cs?name=snippet_Intro)]</span></span>

<span data-ttu-id="b67dc-215">このコードを作成、`DbSet`各エンティティ セットのプロパティです。</span><span class="sxs-lookup"><span data-stu-id="b67dc-215">This code creates a `DbSet` property for each entity set.</span></span> <span data-ttu-id="b67dc-216">Entity Framework の用語で、エンティティ セットは、通常は、データベース テーブルに対応しています、エンティティをテーブル内の行に対応しています。</span><span class="sxs-lookup"><span data-stu-id="b67dc-216">In Entity Framework terminology, an entity set typically corresponds to a database table, and an entity corresponds to a row in the table.</span></span>

<span data-ttu-id="b67dc-217">省略した可能性がありますが、`DbSet<Enrollment>`と`DbSet<Course>`ステートメントと同じように動作します。</span><span class="sxs-lookup"><span data-stu-id="b67dc-217">You could have omitted the `DbSet<Enrollment>` and `DbSet<Course>` statements and it would work the same.</span></span> <span data-ttu-id="b67dc-218">Entity Framework はそれらを含める暗黙的に、`Student`エンティティ参照、`Enrollment`エンティティと`Enrollment`エンティティ参照、`Course`エンティティです。</span><span class="sxs-lookup"><span data-stu-id="b67dc-218">The Entity Framework would include them implicitly because the `Student` entity references the `Enrollment` entity and the `Enrollment` entity references the `Course` entity.</span></span>

<span data-ttu-id="b67dc-219">データベースが作成される、EF 作成と同じ名前を持つテーブルを`DbSet`プロパティの名前。</span><span class="sxs-lookup"><span data-stu-id="b67dc-219">When the database is created, EF creates tables that have names the same as the `DbSet` property names.</span></span> <span data-ttu-id="b67dc-220">コレクションのプロパティ名は、通常 (受講者ではなく学生)、複数形が開発者と異なるかどうかテーブル名をする複数化か。</span><span class="sxs-lookup"><span data-stu-id="b67dc-220">Property names for collections are typically plural (Students rather than Student), but developers disagree about whether table names should be pluralized or not.</span></span> <span data-ttu-id="b67dc-221">これらのチュートリアル DbContext で単数形のテーブル名を指定して既定の動作をオーバーライドします。</span><span class="sxs-lookup"><span data-stu-id="b67dc-221">For these tutorials you'll override the default behavior by specifying singular table names in the DbContext.</span></span> <span data-ttu-id="b67dc-222">実行するには、DbSet の最後のプロパティの後に、次の強調表示されたコードを追加します。</span><span class="sxs-lookup"><span data-stu-id="b67dc-222">To do that, add the following highlighted code after the last DbSet property.</span></span>

<span data-ttu-id="b67dc-223">[!code-csharp[Main](intro/samples/cu/Data/SchoolContext.cs?name=snippet_TableNames&highlight=16-21)]</span><span class="sxs-lookup"><span data-stu-id="b67dc-223">[!code-csharp[Main](intro/samples/cu/Data/SchoolContext.cs?name=snippet_TableNames&highlight=16-21)]</span></span>

## <a name="register-the-context-with-dependency-injection"></a><span data-ttu-id="b67dc-224">依存関係の挿入をコンテキストに登録します。</span><span class="sxs-lookup"><span data-stu-id="b67dc-224">Register the context with dependency injection</span></span>

<span data-ttu-id="b67dc-225">ASP.NET Core を実装する[依存性の注入](../../fundamentals/dependency-injection.md)既定です。</span><span class="sxs-lookup"><span data-stu-id="b67dc-225">ASP.NET Core implements [dependency injection](../../fundamentals/dependency-injection.md) by default.</span></span> <span data-ttu-id="b67dc-226">EF データベース コンテキストで) などのサービスは、アプリケーションの起動時に依存関係の挿入に登録されます。</span><span class="sxs-lookup"><span data-stu-id="b67dc-226">Services (such as the EF database context) are registered with dependency injection during application startup.</span></span> <span data-ttu-id="b67dc-227">これらのサービス (など、MVC コント ローラー) を必要とするコンポーネントは、コンス トラクターのパラメーターを使用してこれらのサービスに提供されます。</span><span class="sxs-lookup"><span data-stu-id="b67dc-227">Components that require these services (such as MVC controllers) are provided these services via constructor parameters.</span></span> <span data-ttu-id="b67dc-228">このチュートリアルで後ほどコンテキストのインスタンスを取得するコント ローラーのコンス トラクター コードが表示されます。</span><span class="sxs-lookup"><span data-stu-id="b67dc-228">You'll see the controller constructor code that gets a context instance later in this tutorial.</span></span>

<span data-ttu-id="b67dc-229">登録する`SchoolContext`をサービスとして開く*Startup.cs*を強調表示された行を追加し、`ConfigureServices`メソッドです。</span><span class="sxs-lookup"><span data-stu-id="b67dc-229">To register `SchoolContext` as a service, open *Startup.cs*, and add the highlighted lines to the `ConfigureServices` method.</span></span>

<span data-ttu-id="b67dc-230">[!code-csharp[Main](intro/samples/cu/Startup.cs?name=snippet_SchoolContext&highlight=3-4)]</span><span class="sxs-lookup"><span data-stu-id="b67dc-230">[!code-csharp[Main](intro/samples/cu/Startup.cs?name=snippet_SchoolContext&highlight=3-4)]</span></span>

<span data-ttu-id="b67dc-231">接続文字列の名前によって渡されるコンテキストでメソッドを呼び出す、`DbContextOptionsBuilder`オブジェクト。</span><span class="sxs-lookup"><span data-stu-id="b67dc-231">The name of the connection string is passed in to the context by calling a method on a `DbContextOptionsBuilder` object.</span></span> <span data-ttu-id="b67dc-232">ローカルの開発、 [ASP.NET Core 構成システム](../../fundamentals/configuration.md)から接続文字列を読み取り、*される appsettings.json*ファイル。</span><span class="sxs-lookup"><span data-stu-id="b67dc-232">For local development, the [ASP.NET Core configuration system](../../fundamentals/configuration.md) reads the connection string from the *appsettings.json* file.</span></span>

<span data-ttu-id="b67dc-233">追加`using`に対してステートメントを`ContosoUniversity.Data`と`Microsoft.EntityFrameworkCore`名前空間、し、プロジェクトを作成します。</span><span class="sxs-lookup"><span data-stu-id="b67dc-233">Add `using` statements for `ContosoUniversity.Data`  and `Microsoft.EntityFrameworkCore` namespaces, and then build the project.</span></span>

<span data-ttu-id="b67dc-234">[!code-csharp[Main](intro/samples/cu/Startup.cs?name=snippet_Usings)]</span><span class="sxs-lookup"><span data-stu-id="b67dc-234">[!code-csharp[Main](intro/samples/cu/Startup.cs?name=snippet_Usings)]</span></span>

<span data-ttu-id="b67dc-235">開く、*される appsettings.json*ファイルし、次の例に示すように、接続文字列を追加します。</span><span class="sxs-lookup"><span data-stu-id="b67dc-235">Open the *appsettings.json* file and add a connection string as shown in the following example.</span></span>

[!code-json[](./intro/samples/cu/appsettings1.json?highlight=2-4)]

### <a name="sql-server-express-localdb"></a><span data-ttu-id="b67dc-236">SQL Server Express LocalDB</span><span class="sxs-lookup"><span data-stu-id="b67dc-236">SQL Server Express LocalDB</span></span>

<span data-ttu-id="b67dc-237">接続文字列では、SQL Server LocalDB データベースを指定します。</span><span class="sxs-lookup"><span data-stu-id="b67dc-237">The connection string specifies a SQL Server LocalDB database.</span></span> <span data-ttu-id="b67dc-238">LocalDB は、SQL Server Express データベース エンジンの簡易バージョンがあり、アプリケーションの開発では、実稼働環境を使用しないものです。</span><span class="sxs-lookup"><span data-stu-id="b67dc-238">LocalDB is a lightweight version of the SQL Server Express Database Engine and is intended for application development, not production use.</span></span> <span data-ttu-id="b67dc-239">LocalDB は、要求時に開始され、ユーザー モードで実行されるため、複雑な構成はありません。</span><span class="sxs-lookup"><span data-stu-id="b67dc-239">LocalDB starts on demand and runs in user mode, so there is no complex configuration.</span></span> <span data-ttu-id="b67dc-240">既定では、LocalDB が作成されます*.mdf*データベース内のファイル、`C:/Users/<user>`ディレクトリ。</span><span class="sxs-lookup"><span data-stu-id="b67dc-240">By default, LocalDB creates *.mdf* database files in the `C:/Users/<user>` directory.</span></span>

## <a name="add-code-to-initialize-the-database-with-test-data"></a><span data-ttu-id="b67dc-241">データベースにテスト データを初期化するコードを追加します。</span><span class="sxs-lookup"><span data-stu-id="b67dc-241">Add code to initialize the database with test data</span></span>

<span data-ttu-id="b67dc-242">Entity Framework を空のデータベースに作成されます。</span><span class="sxs-lookup"><span data-stu-id="b67dc-242">The Entity Framework will create an empty database for you.</span></span>  <span data-ttu-id="b67dc-243">このセクションで、テスト データを設定するために、データベースが作成された後に呼び出されるメソッドを記述します。</span><span class="sxs-lookup"><span data-stu-id="b67dc-243">In this section, you write a method that is called after the database is created in order to populate it with test data.</span></span>

<span data-ttu-id="b67dc-244">ここで使用する、`EnsureCreated`メソッドを自動的にデータベースを作成します。</span><span class="sxs-lookup"><span data-stu-id="b67dc-244">Here you'll use the `EnsureCreated` method to automatically create the database.</span></span> <span data-ttu-id="b67dc-245">[後のチュートリアル](migrations.md)を削除して、データベースを再作成ではなく、データベース スキーマを変更する Code First Migrations を使用してモデルの変更を処理する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="b67dc-245">In a [later tutorial](migrations.md) you'll see how to handle model changes by using Code First Migrations to change the database schema instead of dropping and re-creating the database.</span></span>

<span data-ttu-id="b67dc-246">*データ*フォルダー、という名前の新しいクラス ファイルを作成する*DbInitializer.cs*により必要な時に作成されるデータベースの次のコードで、テンプレート コードを置き換えるし、ロード テストを新しいデータデータベースです。</span><span class="sxs-lookup"><span data-stu-id="b67dc-246">In the *Data* folder, create a new class file named *DbInitializer.cs* and replace the template code with the following code, which causes a database to be created when needed and loads test data into the new database.</span></span>

<span data-ttu-id="b67dc-247">[!code-csharp[Main](intro/samples/cu/Data/DbInitializer.cs?name=snippet_Intro)]</span><span class="sxs-lookup"><span data-stu-id="b67dc-247">[!code-csharp[Main](intro/samples/cu/Data/DbInitializer.cs?name=snippet_Intro)]</span></span>

<span data-ttu-id="b67dc-248">コードは、場合は、データベースが新しいと、テスト データをシード処理する必要がありますいない場合は、想定していますが、データベースの任意の受講者を確認します。</span><span class="sxs-lookup"><span data-stu-id="b67dc-248">The code checks if there are any students in the database, and if not, it assumes the database is new and needs to be seeded with test data.</span></span>  <span data-ttu-id="b67dc-249">テスト データを配列に読み込むのではなく`List<T>`パフォーマンスを最適化するコレクション。</span><span class="sxs-lookup"><span data-stu-id="b67dc-249">It loads test data into arrays rather than `List<T>` collections to optimize performance.</span></span>

<span data-ttu-id="b67dc-250">*Program.cs*、変更、`Main`メソッドをアプリケーションの起動時に次の操作します。</span><span class="sxs-lookup"><span data-stu-id="b67dc-250">In *Program.cs*, modify the `Main` method to do the following on application startup:</span></span>

* <span data-ttu-id="b67dc-251">依存関係性の注入コンテナーからのデータベース コンテキストのインスタンスを取得します。</span><span class="sxs-lookup"><span data-stu-id="b67dc-251">Get a database context instance from the dependency injection container.</span></span>
* <span data-ttu-id="b67dc-252">コンテキストを引き渡しシード メソッドを呼び出します。</span><span class="sxs-lookup"><span data-stu-id="b67dc-252">Call the seed method, passing to it the context.</span></span>
* <span data-ttu-id="b67dc-253">Seed メソッドを実行する場合は、コンテキストを破棄します。</span><span class="sxs-lookup"><span data-stu-id="b67dc-253">Dispose the context when the seed method is done.</span></span>

<span data-ttu-id="b67dc-254">[!code-csharp[Main](intro/samples/cu/Program.cs?name=snippet_Seed&highlight=3-20)]</span><span class="sxs-lookup"><span data-stu-id="b67dc-254">[!code-csharp[Main](intro/samples/cu/Program.cs?name=snippet_Seed&highlight=3-20)]</span></span>

<span data-ttu-id="b67dc-255">追加`using`ステートメント。</span><span class="sxs-lookup"><span data-stu-id="b67dc-255">Add `using` statements:</span></span>

<span data-ttu-id="b67dc-256">[!code-csharp[Main](intro/samples/cu/Program.cs?name=snippet_Usings)]</span><span class="sxs-lookup"><span data-stu-id="b67dc-256">[!code-csharp[Main](intro/samples/cu/Program.cs?name=snippet_Usings)]</span></span>

<span data-ttu-id="b67dc-257">古いチュートリアルは、同様のコードを生じる可能性があります、`Configure`メソッド*Startup.cs*です。</span><span class="sxs-lookup"><span data-stu-id="b67dc-257">In older tutorials, you may see similar code in the `Configure` method in *Startup.cs*.</span></span> <span data-ttu-id="b67dc-258">使用することをお勧め、`Configure`メソッド、要求パイプラインを設定するだけです。</span><span class="sxs-lookup"><span data-stu-id="b67dc-258">We recommend that you use the `Configure` method only to set up the request pipeline.</span></span> <span data-ttu-id="b67dc-259">アプリケーションのスタートアップ コードが属している、`Main`メソッドです。</span><span class="sxs-lookup"><span data-stu-id="b67dc-259">Application startup code belongs in the `Main` method.</span></span>

<span data-ttu-id="b67dc-260">今すぐ初めてアプリケーションを実行するデータベースが作成され、テスト データのシード処理します。</span><span class="sxs-lookup"><span data-stu-id="b67dc-260">Now the first time you run the application, the database will be created and seeded with test data.</span></span> <span data-ttu-id="b67dc-261">データ モデルを変更するたびには、データベースを削除して、そのシード メソッドを更新して開始した後もう一度新しいデータベースと同じ方法ことができます。</span><span class="sxs-lookup"><span data-stu-id="b67dc-261">Whenever you change your data model, you can delete the database, update your seed method, and start afresh with a new database the same way.</span></span> <span data-ttu-id="b67dc-262">以降のチュートリアルでは、データ モデルの変更、削除して再作成するときに、データベースを変更する方法が表示されます。</span><span class="sxs-lookup"><span data-stu-id="b67dc-262">In later tutorials, you'll see how to modify the database when the data model changes, without deleting and re-creating it.</span></span>

## <a name="create-a-controller-and-views"></a><span data-ttu-id="b67dc-263">コント ローラーとビューを作成します。</span><span class="sxs-lookup"><span data-stu-id="b67dc-263">Create a controller and views</span></span>

<span data-ttu-id="b67dc-264">次に、ある MVC コント ローラーとクエリおよびデータを保存するのに EF を使用するビューを追加するのに Visual Studio でスキャフォールディング エンジンを使用します。</span><span class="sxs-lookup"><span data-stu-id="b67dc-264">Next, you'll use the scaffolding engine in Visual Studio to add an MVC controller and views that will use EF to query and save data.</span></span>

<span data-ttu-id="b67dc-265">CRUD アクション メソッドとビューの自動作成は、スキャフォールディングと呼ばれます。</span><span class="sxs-lookup"><span data-stu-id="b67dc-265">The automatic creation of CRUD action methods and views is known as scaffolding.</span></span> <span data-ttu-id="b67dc-266">スキャフォールディングは、スキャフォールディング コードが通常生成されたコードを変更しない一方、独自の要件に合わせて変更できる開始点に、コードの生成とは異なります。</span><span class="sxs-lookup"><span data-stu-id="b67dc-266">Scaffolding differs from code generation in that the scaffolded code is a starting point that you can modify to suit your own requirements, whereas you typically don't modify generated code.</span></span> <span data-ttu-id="b67dc-267">生成されたコードをカスタマイズする必要がある場合は、部分クラスを使用するまたは変更発生時に、コードが再生成します。</span><span class="sxs-lookup"><span data-stu-id="b67dc-267">When you need to customize generated code, you use partial classes or you regenerate the code when things change.</span></span>

* <span data-ttu-id="b67dc-268">右クリックし、**コント ローラー**フォルダー**ソリューション エクスプ ローラー**選択**追加 > スキャフォールディングされた新しい項目**です。</span><span class="sxs-lookup"><span data-stu-id="b67dc-268">Right-click the **Controllers** folder in **Solution Explorer** and select **Add > New Scaffolded Item**.</span></span>

* <span data-ttu-id="b67dc-269">**MVC 依存関係の追加**ダイアログで、**最小の依存関係**を選択して**追加**です。</span><span class="sxs-lookup"><span data-stu-id="b67dc-269">In the **Add MVC Dependencies** dialog, select **Minimal Dependencies**, and select **Add**.</span></span>

  ![依存関係を追加します。](intro/_static/add-depend.png)

  <span data-ttu-id="b67dc-271">Visual Studio では、コント ローラーをスキャフォールディングするために必要な依存関係を追加します。</span><span class="sxs-lookup"><span data-stu-id="b67dc-271">Visual Studio adds the dependencies needed to scaffold a controller.</span></span> <span data-ttu-id="b67dc-272">プロジェクト ファイル内の唯一の違いは、の追加、`Microsoft.VisualStudio.Web.CodeGeneration.Design`パッケージです。</span><span class="sxs-lookup"><span data-stu-id="b67dc-272">The only change in the project file is the addition of the `Microsoft.VisualStudio.Web.CodeGeneration.Design` package.</span></span>

  <span data-ttu-id="b67dc-273">A *ScaffoldingReadMe.txt*ファイルが作成、削除可能です。</span><span class="sxs-lookup"><span data-stu-id="b67dc-273">A *ScaffoldingReadMe.txt* file is created which you can delete.</span></span>

* <span data-ttu-id="b67dc-274">もう一度右クリックし、**コント ローラー**フォルダー**ソリューション エクスプ ローラー**選択**追加 > スキャフォールディングされた新しい項目**です。</span><span class="sxs-lookup"><span data-stu-id="b67dc-274">Once again, right-click the **Controllers** folder in **Solution Explorer** and select **Add > New Scaffolded Item**.</span></span>

* <span data-ttu-id="b67dc-275">**追加 Scaffold**  ダイアログ ボックス。</span><span class="sxs-lookup"><span data-stu-id="b67dc-275">In the **Add Scaffold** dialog box:</span></span>

  * <span data-ttu-id="b67dc-276">選択**Entity Framework を使用して、ビューがある MVC コント ローラー**です。</span><span class="sxs-lookup"><span data-stu-id="b67dc-276">Select **MVC controller with views, using Entity Framework**.</span></span>

  * <span data-ttu-id="b67dc-277">**[追加]**をクリックします。</span><span class="sxs-lookup"><span data-stu-id="b67dc-277">Click **Add**.</span></span>

* <span data-ttu-id="b67dc-278">**コント ローラーの追加** ダイアログ ボックス。</span><span class="sxs-lookup"><span data-stu-id="b67dc-278">In the **Add Controller** dialog box:</span></span>

  * <span data-ttu-id="b67dc-279">**モデル クラス**選択**学生**です。</span><span class="sxs-lookup"><span data-stu-id="b67dc-279">In **Model class** select **Student**.</span></span>

  * <span data-ttu-id="b67dc-280">**データ コンテキスト クラス**選択**SchoolContext**です。</span><span class="sxs-lookup"><span data-stu-id="b67dc-280">In **Data context class** select **SchoolContext**.</span></span>

  * <span data-ttu-id="b67dc-281">既定値を受け入れる**StudentsController**名として。</span><span class="sxs-lookup"><span data-stu-id="b67dc-281">Accept the default **StudentsController** as the name.</span></span>

  * <span data-ttu-id="b67dc-282">**[追加]**をクリックします。</span><span class="sxs-lookup"><span data-stu-id="b67dc-282">Click **Add**.</span></span>

  ![Scaffold 受講者](intro/_static/scaffold-student.png)

  <span data-ttu-id="b67dc-284">クリックすると、**追加**、Visual Studio のスキャフォールディング エンジンを作成、 *StudentsController.cs*ファイルと、一連のビュー (*.cshtml*ファイル)、コント ローラーで動作します。</span><span class="sxs-lookup"><span data-stu-id="b67dc-284">When you click **Add**, the Visual Studio scaffolding engine creates a *StudentsController.cs* file and a set of views (*.cshtml* files) that work with the controller.</span></span>

<span data-ttu-id="b67dc-285">(スキャフォールディング エンジンも、データベース コンテキストを作成手動で作成しない場合はこのチュートリアルの前に行ったようにまずします。</span><span class="sxs-lookup"><span data-stu-id="b67dc-285">(The scaffolding engine can also create the database context for you if you don't create it manually first as you did earlier for this tutorial.</span></span> <span data-ttu-id="b67dc-286">新しいコンテキスト クラスを指定することができます、**コント ローラーの追加**の右側にあるプラス記号をクリックしてボックス**データ コンテキスト クラス**です。</span><span class="sxs-lookup"><span data-stu-id="b67dc-286">You can specify a new context class in the **Add Controller** box by clicking the plus sign to the right of **Data context class**.</span></span>  <span data-ttu-id="b67dc-287">Visual Studio は作成し、`DbContext`コント ローラーとビューだけでなくクラスです)。</span><span class="sxs-lookup"><span data-stu-id="b67dc-287">Visual Studio will then create your `DbContext` class as well as the controller and views.)</span></span>

<span data-ttu-id="b67dc-288">コント ローラーを取ることがわかります、`SchoolContext`コンス トラクターのパラメーターとして。</span><span class="sxs-lookup"><span data-stu-id="b67dc-288">You'll notice that the controller takes a `SchoolContext` as a constructor parameter.</span></span>

<span data-ttu-id="b67dc-289">[!code-csharp[Main](intro/samples/cu/Controllers/StudentsController.cs?name=snippet_Context&highlight=5,7,9)]</span><span class="sxs-lookup"><span data-stu-id="b67dc-289">[!code-csharp[Main](intro/samples/cu/Controllers/StudentsController.cs?name=snippet_Context&highlight=5,7,9)]</span></span>

<span data-ttu-id="b67dc-290">ASP.NET の依存関係の挿入のインスタンスを渡す場合の注意`SchoolContext`コント ローラーにします。</span><span class="sxs-lookup"><span data-stu-id="b67dc-290">ASP.NET dependency injection will take care of passing an instance of `SchoolContext` into the controller.</span></span> <span data-ttu-id="b67dc-291">構成されている、 *Startup.cs*前ファイルします。</span><span class="sxs-lookup"><span data-stu-id="b67dc-291">You configured that in the *Startup.cs* file earlier.</span></span>

<span data-ttu-id="b67dc-292">コント ローラーが含まれています、`Index`アクション メソッドは、データベース内のすべての受講者を表示します。</span><span class="sxs-lookup"><span data-stu-id="b67dc-292">The controller contains an `Index` action method, which displays all students in the database.</span></span> <span data-ttu-id="b67dc-293">メソッドは、受講者のエンティティを読み取ってセットから受講者の一覧を取得、`Students`データベース コンテキストのインスタンスのプロパティ。</span><span class="sxs-lookup"><span data-stu-id="b67dc-293">The method gets a list of students from the Students entity set by reading the `Students` property of the database context instance:</span></span>

<span data-ttu-id="b67dc-294">[!code-csharp[Main](intro/samples/cu/Controllers/StudentsController.cs?name=snippet_ScaffoldedIndex&highlight=3)]</span><span class="sxs-lookup"><span data-stu-id="b67dc-294">[!code-csharp[Main](intro/samples/cu/Controllers/StudentsController.cs?name=snippet_ScaffoldedIndex&highlight=3)]</span></span>

<span data-ttu-id="b67dc-295">このコードで非同期のプログラミング要素は、このチュートリアルで後ほどについて説明します。</span><span class="sxs-lookup"><span data-stu-id="b67dc-295">You'll learn about the asynchronous programming elements in this code later in the tutorial.</span></span>

<span data-ttu-id="b67dc-296">*Views/Students/Index.cshtml*ビューは、テーブルのこの一覧を表示します。</span><span class="sxs-lookup"><span data-stu-id="b67dc-296">The *Views/Students/Index.cshtml* view displays this list in a table:</span></span>

[!code-html[](intro/samples/cu/Views/Students/Index1.cshtml)]

<span data-ttu-id="b67dc-297">CTRL + f5 キーを押してプロジェクトを実行または選択**デバッグ > デバッグなしで開始** メニューからです。</span><span class="sxs-lookup"><span data-stu-id="b67dc-297">Press CTRL+F5 to run the project or choose **Debug > Start Without Debugging** from the menu.</span></span>

<span data-ttu-id="b67dc-298">テスト データを表示する、受講者タブをクリックする、`DbInitializer.Initialize`メソッドを挿入します。</span><span class="sxs-lookup"><span data-stu-id="b67dc-298">Click the Students tab to see the test data that the `DbInitializer.Initialize` method inserted.</span></span> <span data-ttu-id="b67dc-299">どの幅の狭い、ブラウザー ウィンドウがによってが表示されます、`Student`ページの上部にあるタブ リンクは、リンクを表示する右上隅で、ナビゲーション アイコンをクリックする必要があります。</span><span class="sxs-lookup"><span data-stu-id="b67dc-299">Depending on how narrow your browser window is, you'll see the `Student` tab link at the top of the page or you'll have to click the navigation icon in the upper right corner to see the link.</span></span>

![Contoso 大学のホーム ページの幅の狭い](intro/_static/home-page-narrow.png)

![インデックス ページの受講者](intro/_static/students-index.png)

## <a name="view-the-database"></a><span data-ttu-id="b67dc-302">データベースを表示します。</span><span class="sxs-lookup"><span data-stu-id="b67dc-302">View the Database</span></span>

<span data-ttu-id="b67dc-303">アプリケーションを起動したときに、`DbInitializer.Initialize`メソッド呼び出し`EnsureCreated`です。</span><span class="sxs-lookup"><span data-stu-id="b67dc-303">When you started the application, the `DbInitializer.Initialize` method calls `EnsureCreated`.</span></span> <span data-ttu-id="b67dc-304">EF データベースがありませんでした。 そのために作成され、1 つの残りの部分の説明、`Initialize`メソッドのコードには、データベースにデータが設定されます。</span><span class="sxs-lookup"><span data-stu-id="b67dc-304">EF saw that there was no database and so it created one, then the remainder of the `Initialize` method code populated the database with data.</span></span> <span data-ttu-id="b67dc-305">使用することができます**SQL Server オブジェクト エクスプ ローラー** Visual Studio でデータベースを表示するには、(SSOX)。</span><span class="sxs-lookup"><span data-stu-id="b67dc-305">You can use **SQL Server Object Explorer** (SSOX) to view the database in Visual Studio.</span></span>

<span data-ttu-id="b67dc-306">ブラウザーを閉じます。</span><span class="sxs-lookup"><span data-stu-id="b67dc-306">Close the browser.</span></span>

<span data-ttu-id="b67dc-307">SSOX ウィンドウが開いていない場合を選択してから、**ビュー** Visual Studio のメニュー。</span><span class="sxs-lookup"><span data-stu-id="b67dc-307">If the SSOX window isn't already open, select it from the **View** menu in Visual Studio.</span></span>

<span data-ttu-id="b67dc-308">SSOX、クリックして**(localdb) \MSSQLLocalDB > データベース**、内の接続文字列に含まれるデータベース名のエントリをクリックして、*される appsettings.json*ファイル。</span><span class="sxs-lookup"><span data-stu-id="b67dc-308">In SSOX, click **(localdb)\MSSQLLocalDB > Databases**, and then click the entry for the database name that is in the connection string in your *appsettings.json* file.</span></span>

<span data-ttu-id="b67dc-309">展開して、**テーブル**ノードをデータベース内のテーブルを参照してください。</span><span class="sxs-lookup"><span data-stu-id="b67dc-309">Expand the **Tables** node to see the tables in your database.</span></span>

![SSOX 内のテーブル](intro/_static/ssox-tables.png)

<span data-ttu-id="b67dc-311">右クリックし、**学生**テーブルし、をクリックして**ビュー データ**に作成された列とテーブルに挿入された行を参照してください。</span><span class="sxs-lookup"><span data-stu-id="b67dc-311">Right-click the **Student** table and click **View Data** to see the columns that were created and the rows that were inserted into the table.</span></span>

![SSOX で student テーブル](intro/_static/ssox-student-table.png)

<span data-ttu-id="b67dc-313">*.Mdf*と*.ldf*データベース ファイルは、 *C:\Users\<yourusername >*フォルダーです。</span><span class="sxs-lookup"><span data-stu-id="b67dc-313">The *.mdf* and *.ldf* database files are in the *C:\Users\<yourusername>* folder.</span></span>

<span data-ttu-id="b67dc-314">呼び出しているため`EnsureCreated`アプリの起動で実行されている初期化メソッドででした今すぐ変更を行うには`Student`クラス、データベースを削除して、もう一度、アプリケーションを実行し、するとデータベースに自動的に変更内容を一致するように再作成します。</span><span class="sxs-lookup"><span data-stu-id="b67dc-314">Because you're calling `EnsureCreated` in the initializer method that runs on app start, you could now make a change to the `Student` class, delete the database, run the application again, and the database would automatically be re-created to match your change.</span></span> <span data-ttu-id="b67dc-315">たとえば、追加する場合、`EmailAddress`プロパティを`Student`クラスが表示されます、新しい`EmailAddress`再作成されたテーブル内の列です。</span><span class="sxs-lookup"><span data-stu-id="b67dc-315">For example, if you add an `EmailAddress` property to the `Student` class, you'll see a new `EmailAddress` column in the re-created table.</span></span>

## <a name="conventions"></a><span data-ttu-id="b67dc-316">規則</span><span class="sxs-lookup"><span data-stu-id="b67dc-316">Conventions</span></span>

<span data-ttu-id="b67dc-317">完全なデータベースを作成できるように、Entity Framework の順序で記述したコードの量は、規則、または Entity Framework は、前提を使用するためは最小限です。</span><span class="sxs-lookup"><span data-stu-id="b67dc-317">The amount of code you had to write in order for the Entity Framework to be able to create a complete database for you is minimal because of the use of conventions, or assumptions that the Entity Framework makes.</span></span>

* <span data-ttu-id="b67dc-318">名前`DbSet`プロパティ テーブル名として使用されます。</span><span class="sxs-lookup"><span data-stu-id="b67dc-318">The names of `DbSet` properties are used as table names.</span></span> <span data-ttu-id="b67dc-319">参照されていないエンティティに対して、`DbSet`プロパティ、エンティティ クラスの名前テーブル名として使用されます。</span><span class="sxs-lookup"><span data-stu-id="b67dc-319">For entities not referenced by a `DbSet` property, entity class names are used as table names.</span></span>

* <span data-ttu-id="b67dc-320">エンティティのプロパティ名は、列名に使用されます。</span><span class="sxs-lookup"><span data-stu-id="b67dc-320">Entity property names are used for column names.</span></span>

* <span data-ttu-id="b67dc-321">ID または classnameID という名前はエンティティのプロパティは、主キー プロパティとして認識されます。</span><span class="sxs-lookup"><span data-stu-id="b67dc-321">Entity properties that are named ID or classnameID are recognized as primary key properties.</span></span>

* <span data-ttu-id="b67dc-322">という名前が場合、プロパティが外部キーのプロパティとして解釈されます *<navigation property name> <primary key property name>*  (たとえば、`StudentID`の`Student`以降のナビゲーション プロパティ、`Student`エンティティの主キーとは`ID`).</span><span class="sxs-lookup"><span data-stu-id="b67dc-322">A property is interpreted as a foreign key property if it's named *<navigation property name><primary key property name>* (for example, `StudentID` for the `Student` navigation property since the `Student` entity's primary key is `ID`).</span></span> <span data-ttu-id="b67dc-323">外部キー プロパティは単にも呼ばれます *<primary key property name>*  (たとえば、`EnrollmentID`ので、`Enrollment`エンティティの主キーが`EnrollmentID`)。</span><span class="sxs-lookup"><span data-stu-id="b67dc-323">Foreign key properties can also be named simply *<primary key property name>* (for example, `EnrollmentID` since the `Enrollment` entity's primary key is `EnrollmentID`).</span></span>

<span data-ttu-id="b67dc-324">従来の動作をオーバーライドできます。</span><span class="sxs-lookup"><span data-stu-id="b67dc-324">Conventional behavior can be overridden.</span></span> <span data-ttu-id="b67dc-325">たとえば、このチュートリアルで既に説明したとおり、テーブル名を明示的に指定することができます。</span><span class="sxs-lookup"><span data-stu-id="b67dc-325">For example, you can explicitly specify table names, as you saw earlier in this tutorial.</span></span> <span data-ttu-id="b67dc-326">列名を設定してでわかる foreign key、または主キーとして任意のプロパティを設定し、[後のチュートリアル](complex-data-model.md)このシリーズのです。</span><span class="sxs-lookup"><span data-stu-id="b67dc-326">And you can set column names and set any property as primary key or foreign key, as you'll see in a [later tutorial](complex-data-model.md) in this series.</span></span>

## <a name="asynchronous-code"></a><span data-ttu-id="b67dc-327">非同期コード</span><span class="sxs-lookup"><span data-stu-id="b67dc-327">Asynchronous code</span></span>

<span data-ttu-id="b67dc-328">非同期プログラミングは、ASP.NET Core と EF コアの既定モードです。</span><span class="sxs-lookup"><span data-stu-id="b67dc-328">Asynchronous programming is the default mode for ASP.NET Core and EF Core.</span></span>

<span data-ttu-id="b67dc-329">Web サーバーは、使用可能なスレッド数を限定を持ち、負荷が高い状況でのすべての利用可能なスレッドがありますで使用します。</span><span class="sxs-lookup"><span data-stu-id="b67dc-329">A web server has a limited number of threads available, and in high load situations all of the available threads might be in use.</span></span> <span data-ttu-id="b67dc-330">そのような場合は、サーバーは、スレッドが解放されるまで新しい要求を処理できません。</span><span class="sxs-lookup"><span data-stu-id="b67dc-330">When that happens, the server can't process new requests until the threads are freed up.</span></span> <span data-ttu-id="b67dc-331">同期コードはの I/O 完了を待機しているため、実際には、作業の実行されない中に多数のスレッド関連付ける可能性があります。</span><span class="sxs-lookup"><span data-stu-id="b67dc-331">With synchronous code, many threads may be tied up while they aren't actually doing any work because they're waiting for I/O to complete.</span></span> <span data-ttu-id="b67dc-332">非同期コードは、プロセスが完了するには I/O の待機している場合、他の要求を処理するために使用するサーバー用に、スレッドが解放されます。</span><span class="sxs-lookup"><span data-stu-id="b67dc-332">With asynchronous code, when a process is waiting for I/O to complete, its thread is freed up for the server to use for processing other requests.</span></span> <span data-ttu-id="b67dc-333">その結果、非同期コード サーバー リソースをより効率的に使用でき、遅延なしのより多くのトラフィックを処理するサーバーが有効になっています。</span><span class="sxs-lookup"><span data-stu-id="b67dc-333">As a result, asynchronous code enables server resources to be used more efficiently, and the server is enabled to handle more traffic without delays.</span></span>

<span data-ttu-id="b67dc-334">非同期のコードは、実行時に少量のオーバーヘッドを導入がトラフィックの少ない状況がパフォーマンスの低下はごくわずかであり、中に大量のトラフィックの場合、潜在的なパフォーマンスの向上は大きくします。</span><span class="sxs-lookup"><span data-stu-id="b67dc-334">Asynchronous code does introduce a small amount of overhead at run time, but for low traffic situations the performance hit is negligible, while for high traffic situations, the potential performance improvement is substantial.</span></span>

<span data-ttu-id="b67dc-335">次のコードで、`async`キーワード、`Task<T>`値を返す`await`キーワード、および`ToListAsync`メソッドが非同期的に実行するコードを作成します。</span><span class="sxs-lookup"><span data-stu-id="b67dc-335">In the following code, the `async` keyword, `Task<T>` return value, `await` keyword, and `ToListAsync` method make the code execute asynchronously.</span></span>

<span data-ttu-id="b67dc-336">[!code-csharp[Main](intro/samples/cu/Controllers/StudentsController.cs?name=snippet_ScaffoldedIndex)]</span><span class="sxs-lookup"><span data-stu-id="b67dc-336">[!code-csharp[Main](intro/samples/cu/Controllers/StudentsController.cs?name=snippet_ScaffoldedIndex)]</span></span>

* <span data-ttu-id="b67dc-337">`async`キーワード、コンパイラはメソッド本体の各部分のコールバックを生成して自動的に作成する、`Task<IActionResult>`返されるオブジェクト。</span><span class="sxs-lookup"><span data-stu-id="b67dc-337">The `async` keyword tells the compiler to generate callbacks for parts of the method body and to automatically create the `Task<IActionResult>` object that is returned.</span></span>

* <span data-ttu-id="b67dc-338">戻り値の型`Task<IActionResult>`型の結果で進行中の作業を表す`IActionResult`です。</span><span class="sxs-lookup"><span data-stu-id="b67dc-338">The return type `Task<IActionResult>` represents ongoing work with a result of type `IActionResult`.</span></span>

* <span data-ttu-id="b67dc-339">`await`キーワードによって、コンパイラにメソッドを 2 つの部分に分割します。</span><span class="sxs-lookup"><span data-stu-id="b67dc-339">The `await` keyword causes the compiler to split the method into two parts.</span></span> <span data-ttu-id="b67dc-340">最初の部分は、非同期的に開始される操作を終了します。</span><span class="sxs-lookup"><span data-stu-id="b67dc-340">The first part ends with the operation that is started asynchronously.</span></span> <span data-ttu-id="b67dc-341">2 番目の部分は、操作が完了したときに呼び出されるコールバック メソッドに配置されます。</span><span class="sxs-lookup"><span data-stu-id="b67dc-341">The second part is put into a callback method that is called when the operation completes.</span></span>

* <span data-ttu-id="b67dc-342">`ToListAsync`非同期バージョンの`ToList`拡張メソッド。</span><span class="sxs-lookup"><span data-stu-id="b67dc-342">`ToListAsync` is the asynchronous version of the `ToList` extension method.</span></span>

<span data-ttu-id="b67dc-343">Entity Framework を使用する非同期コードを作成する場合の注意すべき点がいくつか:</span><span class="sxs-lookup"><span data-stu-id="b67dc-343">Some things to be aware of when you are writing asynchronous code that uses the Entity Framework:</span></span>

* <span data-ttu-id="b67dc-344">クエリまたはコマンドのデータベースに送信されるステートメントだけが非同期的に実行されます。</span><span class="sxs-lookup"><span data-stu-id="b67dc-344">Only statements that cause queries or commands to be sent to the database are executed asynchronously.</span></span> <span data-ttu-id="b67dc-345">たとえばを含む`ToListAsync`、 `SingleOrDefaultAsync`、および`SaveChangesAsync`です。</span><span class="sxs-lookup"><span data-stu-id="b67dc-345">That includes, for example, `ToListAsync`, `SingleOrDefaultAsync`, and `SaveChangesAsync`.</span></span>  <span data-ttu-id="b67dc-346">含まれません、たとえば、だけを変更するステートメント、`IQueryable`など`var students = context.Students.Where(s => s.LastName == "Davolio")`です。</span><span class="sxs-lookup"><span data-stu-id="b67dc-346">It does not include, for example, statements that just change an `IQueryable`, such as `var students = context.Students.Where(s => s.LastName == "Davolio")`.</span></span>

* <span data-ttu-id="b67dc-347">EF コンテキストはスレッド セーフではありません: を並列で複数の操作を行うにはしないでください。</span><span class="sxs-lookup"><span data-stu-id="b67dc-347">An EF context is not thread safe: don't try to do multiple operations in parallel.</span></span> <span data-ttu-id="b67dc-348">ある非同期 EF メソッドを呼び出すときに、常に使用して、`await`キーワード。</span><span class="sxs-lookup"><span data-stu-id="b67dc-348">When you call any async EF method, always use the `await` keyword.</span></span>

* <span data-ttu-id="b67dc-349">非同期コードのパフォーマンスの利点を活用、任意のライブラリのパッケージにあるかどうかを確認する場合、(ページングなど) を使用している、データベースに送信されるクエリを Entity Framework メソッドを呼び出す場合にも非同期を使用します。</span><span class="sxs-lookup"><span data-stu-id="b67dc-349">If you want to take advantage of the performance benefits of async code, make sure that any library packages that you're using (such as for paging), also use async if they call any Entity Framework methods that cause queries to be sent to the database.</span></span>

<span data-ttu-id="b67dc-350">.NET における非同期プログラミングの詳細については、次を参照してください。 [Async 概要](https://docs.microsoft.com/dotnet/articles/standard/async)です。</span><span class="sxs-lookup"><span data-stu-id="b67dc-350">For more information about asynchronous programming in .NET, see [Async Overview](https://docs.microsoft.com/dotnet/articles/standard/async).</span></span>

## <a name="summary"></a><span data-ttu-id="b67dc-351">概要</span><span class="sxs-lookup"><span data-stu-id="b67dc-351">Summary</span></span>

<span data-ttu-id="b67dc-352">保存し、データを表示する、エンティティ フレームワークのコアと SQL Server Express LocalDB を使用する単純なアプリケーションが作成されました。</span><span class="sxs-lookup"><span data-stu-id="b67dc-352">You've now created a simple application that uses the Entity Framework Core and SQL Server Express LocalDB to store and display data.</span></span> <span data-ttu-id="b67dc-353">次のチュートリアルでは基本的な CRUD を実行する方法を学習 (作成、読み取り、更新、削除) 操作です。</span><span class="sxs-lookup"><span data-stu-id="b67dc-353">In the following tutorial, you'll learn how to perform basic CRUD (create, read, update, delete) operations.</span></span>

>[!div class="step-by-step"]
[<span data-ttu-id="b67dc-354">次へ</span><span class="sxs-lookup"><span data-stu-id="b67dc-354">Next</span></span>](crud.md)  