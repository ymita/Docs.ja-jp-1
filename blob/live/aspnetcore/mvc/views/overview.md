---
title: "ASP.NET Core MVC ビュー"
author: ardalis
description: "ビューが、アプリのデータの表示と ASP.NET Core MVC でのユーザーとの対話を処理する方法について説明します。"
keywords: "ASP.NET Core、表示、MVC、razor、viewmodel、viewdata、viewbag"
ms.author: riande
manager: wpickett
ms.date: 12/12/2017
ms.topic: article
ms.technology: aspnet
ms.prod: asp.net-core
uid: mvc/views/overview
ms.openlocfilehash: 2562d4e5fb85159e6ccb47990f54448ddc188077
ms.sourcegitcommit: 198fb0488e961048bfa376cf58cb853ef1d1cb91
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2017
---
# <a name="views-in-aspnet-core-mvc"></a><span data-ttu-id="6b849-104">ASP.NET Core MVC ビュー</span><span class="sxs-lookup"><span data-stu-id="6b849-104">Views in ASP.NET Core MVC</span></span>

<span data-ttu-id="6b849-105">によって[Steve Smith](https://ardalis.com/)と[Luke Latham](https://github.com/guardrex)</span><span class="sxs-lookup"><span data-stu-id="6b849-105">By [Steve Smith](https://ardalis.com/) and [Luke Latham](https://github.com/guardrex)</span></span>

<span data-ttu-id="6b849-106">このドキュメントでは、ASP.NET Core MVC アプリケーションで使用されるビューについて説明します。</span><span class="sxs-lookup"><span data-stu-id="6b849-106">This document explains views used in ASP.NET Core MVC applications.</span></span> <span data-ttu-id="6b849-107">Razor ページについては、次を参照してください。 [Razor ページの概要](xref:mvc/razor-pages/index)です。</span><span class="sxs-lookup"><span data-stu-id="6b849-107">For information on Razor Pages, see [Introduction to Razor Pages](xref:mvc/razor-pages/index).</span></span>

<span data-ttu-id="6b849-108">**M**odel -**V**ビュー -**C**ontroller (MVC) パターン、*ビュー*アプリのデータのプレゼンテーションとユーザーの操作を処理します。</span><span class="sxs-lookup"><span data-stu-id="6b849-108">In the **M**odel-**V**iew-**C**ontroller (MVC) pattern, the *view* handles the app's data presentation and user interaction.</span></span> <span data-ttu-id="6b849-109">ビューは、HTML テンプレートが埋め込まれて[Razor マークアップ](xref:mvc/views/razor)です。</span><span class="sxs-lookup"><span data-stu-id="6b849-109">A view is an HTML template with embedded [Razor markup](xref:mvc/views/razor).</span></span> <span data-ttu-id="6b849-110">Razor のマークアップは、クライアントに送信される web ページを生成するために HTML マークアップが対話するコードです。</span><span class="sxs-lookup"><span data-stu-id="6b849-110">Razor markup is code that interacts with HTML markup to produce a webpage that's sent to the client.</span></span>

<span data-ttu-id="6b849-111">ASP.NET Core MVC ビューは*.cshtml*ファイルを使用する、 [c# プログラミング言語](/dotnet/csharp/)Razor マークアップでします。</span><span class="sxs-lookup"><span data-stu-id="6b849-111">In ASP.NET Core MVC, views are *.cshtml* files that use the [C# programming language](/dotnet/csharp/) in Razor markup.</span></span> <span data-ttu-id="6b849-112">通常、ファイルの表示はフォルダーの各アプリの名前にグループ化[コント ローラー](xref:mvc/controllers/actions)です。</span><span class="sxs-lookup"><span data-stu-id="6b849-112">Usually, view files are grouped into folders named for each of the app's [controllers](xref:mvc/controllers/actions).</span></span> <span data-ttu-id="6b849-113">フォルダーが格納されている、*ビュー*アプリのルートにあるフォルダー。</span><span class="sxs-lookup"><span data-stu-id="6b849-113">The folders are stored in a *Views* folder at the root of the app:</span></span>

![Visual Studio のソリューション エクスプ ローラーで、views フォルダーは About.cshtml、Contact.cshtml、および Index.cshtml ファイルを表示するのには開放の [ホーム] フォルダーで開く](overview/_static/views_solution_explorer.png)

<span data-ttu-id="6b849-115">*ホーム*コント ローラーがによって表される、*ホーム*内のフォルダー、*ビュー*フォルダーです。</span><span class="sxs-lookup"><span data-stu-id="6b849-115">The *Home* controller is represented by a *Home* folder inside the *Views* folder.</span></span> <span data-ttu-id="6b849-116">*ホーム*フォルダーには用のビューが含まれています、*に関する*、*連絡先*、および*インデックス*(ホーム ページ) の web ページ。</span><span class="sxs-lookup"><span data-stu-id="6b849-116">The *Home* folder contains the views for the *About*, *Contact*, and *Index* (homepage) webpages.</span></span> <span data-ttu-id="6b849-117">ユーザーがこれらの 3 つ web サイト、コント ローラー アクションのいずれかを要求するときに、*ホーム*コント ローラーは、3 つのビューのどちらを使用してビルドし、ユーザーに web ページを返すを決定します。</span><span class="sxs-lookup"><span data-stu-id="6b849-117">When a user requests one of these three webpages, controller actions in the *Home* controller determine which of the three views is used to build and return a webpage to the user.</span></span>

<span data-ttu-id="6b849-118">使用して[レイアウト](xref:mvc/views/layout)を一貫性のある web ページのセクションを提供し、コードの繰り返しを削減します。</span><span class="sxs-lookup"><span data-stu-id="6b849-118">Use [layouts](xref:mvc/views/layout) to provide consistent webpage sections and reduce code repetition.</span></span> <span data-ttu-id="6b849-119">多くの場合、レイアウトには、ヘッダー、ナビゲーションとメニューの要素、およびフッターが含まれています。</span><span class="sxs-lookup"><span data-stu-id="6b849-119">Layouts often contain the header, navigation and menu elements, and the footer.</span></span> <span data-ttu-id="6b849-120">ヘッダーとフッター多くのメタデータ要素とスクリプトとスタイルの資産へのリンクの定型的なマークアップを通常含まれます。</span><span class="sxs-lookup"><span data-stu-id="6b849-120">The header and footer usually contain boilerplate markup for many metadata elements and links to script and style assets.</span></span> <span data-ttu-id="6b849-121">レイアウトでは、ビューでは、この定型的なマークアップを回避できます。</span><span class="sxs-lookup"><span data-stu-id="6b849-121">Layouts help you avoid this boilerplate markup in your views.</span></span>

<span data-ttu-id="6b849-122">[部分ビュー](xref:mvc/views/partial)ビューの再利用可能な部分を管理することにより、コードの重複を削減します。</span><span class="sxs-lookup"><span data-stu-id="6b849-122">[Partial views](xref:mvc/views/partial) reduce code duplication by managing reusable parts of views.</span></span> <span data-ttu-id="6b849-123">たとえば、部分ビューは、いくつかのビューに表示されているブログ web サイトで、作成者略歴に役立ちます。</span><span class="sxs-lookup"><span data-stu-id="6b849-123">For example, a partial view is useful for an author biography on a blog website that appears in several views.</span></span> <span data-ttu-id="6b849-124">作成者略歴は、通常のビューのコンテンツを必要し、しない web ページのコンテンツを生成するために実行するコードです。</span><span class="sxs-lookup"><span data-stu-id="6b849-124">An author biography is ordinary view content and doesn't require code to execute in order to produce the content for the webpage.</span></span> <span data-ttu-id="6b849-125">作成者略歴コンテンツは単独で、モデル バインディングによってビューに表示する部分ビューを使用して、この種類のコンテンツは、最適です。</span><span class="sxs-lookup"><span data-stu-id="6b849-125">Author biography content is available to the view by model binding alone, so using a partial view for this type of content is ideal.</span></span>

<span data-ttu-id="6b849-126">[コンポーネントの表示](xref:mvc/views/view-components)部分のようなビューは、コードの繰り返しを削減することができる点で、web ページを表示するために、サーバーで実行するコードを必要とするコンテンツの表示に適していますがします。</span><span class="sxs-lookup"><span data-stu-id="6b849-126">[View components](xref:mvc/views/view-components) are similar to partial views in that they allow you to reduce repetitive code, but they're appropriate for view content that requires code to run on the server in order to render the webpage.</span></span> <span data-ttu-id="6b849-127">ビューのコンポーネントは、描画された内容は、ショッピング カートの web サイトのように、データベースとの対話を必要とする場合に便利です。</span><span class="sxs-lookup"><span data-stu-id="6b849-127">View components are useful when the rendered content requires database interaction, such as for a website shopping cart.</span></span> <span data-ttu-id="6b849-128">コンポーネントの表示は web ページの出力を生成するためにモデル バインディングに制限されます。</span><span class="sxs-lookup"><span data-stu-id="6b849-128">View components aren't limited to model binding in order to produce webpage output.</span></span>

## <a name="benefits-of-using-views"></a><span data-ttu-id="6b849-129">ビューを使用する利点</span><span class="sxs-lookup"><span data-stu-id="6b849-129">Benefits of using views</span></span>

<span data-ttu-id="6b849-130">ビューを確立するために、 [ **S**eparation **o**f **C**oncerns (SoC) デザイン](http://deviq.com/separation-of-concerns/)からユーザー インターフェイスのマークアップを分離することにより、MVC アプリケーション内でアプリの他の部分です。</span><span class="sxs-lookup"><span data-stu-id="6b849-130">Views help to establish a [**S**eparation **o**f **C**oncerns (SoC) design](http://deviq.com/separation-of-concerns/) within an MVC app by separating the user interface markup from other parts of the app.</span></span> <span data-ttu-id="6b849-131">次の SoC 設計により、アプリ モジュール、いくつかの利点を提供します。</span><span class="sxs-lookup"><span data-stu-id="6b849-131">Following SoC design makes your app modular, which provides several benefits:</span></span>

* <span data-ttu-id="6b849-132">アプリより適切に編成されていますのでを維持するために簡単です。</span><span class="sxs-lookup"><span data-stu-id="6b849-132">The app is easier to maintain because it's better organized.</span></span> <span data-ttu-id="6b849-133">ビューは、アプリの機能によって一般にグループ化されます。</span><span class="sxs-lookup"><span data-stu-id="6b849-133">Views are generally grouped by app feature.</span></span> <span data-ttu-id="6b849-134">これにより、機能を使用する場合は、関連するビューを見つけやすくします。</span><span class="sxs-lookup"><span data-stu-id="6b849-134">This makes it easier to find related views when working on a feature.</span></span>
* <span data-ttu-id="6b849-135">アプリの一部は疎結合します。</span><span class="sxs-lookup"><span data-stu-id="6b849-135">The parts of the app are loosely coupled.</span></span> <span data-ttu-id="6b849-136">構築し、ビジネス ロジックとデータ アクセス コンポーネントから個別に、アプリのビューを更新できます。</span><span class="sxs-lookup"><span data-stu-id="6b849-136">You can build and update the app's views separately from the business logic and data access components.</span></span> <span data-ttu-id="6b849-137">必ずしも、アプリの他の部分を更新することがなく、アプリのビューを変更できます。</span><span class="sxs-lookup"><span data-stu-id="6b849-137">You can modify the views of the app without necessarily having to update other parts of the app.</span></span>
* <span data-ttu-id="6b849-138">個別の単位は、ビューがあるために、ユーザー インターフェイスがアプリの一部をテストする簡単です。</span><span class="sxs-lookup"><span data-stu-id="6b849-138">It's easier to test the user interface parts of the app because the views are separate units.</span></span>
* <span data-ttu-id="6b849-139">効率的な整理、により可能性は低くなりますユーザー インターフェイスの繰り返しセクションでは誤ってを学習します。</span><span class="sxs-lookup"><span data-stu-id="6b849-139">Due to better organization, it's less likely that you'll accidently repeat sections of the user interface.</span></span>

## <a name="creating-a-view"></a><span data-ttu-id="6b849-140">ビューを作成します。</span><span class="sxs-lookup"><span data-stu-id="6b849-140">Creating a view</span></span>

<span data-ttu-id="6b849-141">コント ローラーに固有のビューを作成するのには*ビュー/[ControllerName]*フォルダーです。</span><span class="sxs-lookup"><span data-stu-id="6b849-141">Views that are specific to a controller are created in the *Views/[ControllerName]* folder.</span></span> <span data-ttu-id="6b849-142">コント ローラー間で共有されるビューについてに、 *Views/shared*フォルダーです。</span><span class="sxs-lookup"><span data-stu-id="6b849-142">Views that are shared among controllers are placed in the *Views/Shared* folder.</span></span> <span data-ttu-id="6b849-143">ビューを作成するには、新しいファイルを追加し、関連付けられたコント ローラー アクションのと同じ名前を付けます、 *.cshtml*ファイル拡張子。</span><span class="sxs-lookup"><span data-stu-id="6b849-143">To create a view, add a new file and give it the same name as its associated controller action with the *.cshtml* file extension.</span></span> <span data-ttu-id="6b849-144">対応するビューを作成する、*に関する*アクションで、*ホーム*コント ローラーで、作成、 *About.cshtml*ファイルで、*ビュー/ホーム*フォルダー。</span><span class="sxs-lookup"><span data-stu-id="6b849-144">To create a view that corresponds with the *About* action in the *Home* controller, create an *About.cshtml* file in the *Views/Home* folder:</span></span>

[!code-cshtml[Main](../../common/samples/WebApplication1/Views/Home/About.cshtml)]

<span data-ttu-id="6b849-145">*Razor*マークアップが始まり、`@`シンボル。</span><span class="sxs-lookup"><span data-stu-id="6b849-145">*Razor* markup starts with the `@` symbol.</span></span> <span data-ttu-id="6b849-146">内のコードを配置する (C#) で実行 (C#) ステートメント[Razor コードのブロック](xref:mvc/views/razor#razor-code-blocks)中かっこで off に設定 (`{ ... }`)。</span><span class="sxs-lookup"><span data-stu-id="6b849-146">Run C# statements by placing C# code within [Razor code blocks](xref:mvc/views/razor#razor-code-blocks) set off by curly braces (`{ ... }`).</span></span> <span data-ttu-id="6b849-147">たとえばに"About"の割り当てを参照してください`ViewData["Title"]`上に示したです。</span><span class="sxs-lookup"><span data-stu-id="6b849-147">For example, see the assignment of "About" to `ViewData["Title"]` shown above.</span></span> <span data-ttu-id="6b849-148">HTML 内の値を表示するには単に値が参照することによって、`@`シンボル。</span><span class="sxs-lookup"><span data-stu-id="6b849-148">You can display values within HTML by simply referencing the value with the `@` symbol.</span></span> <span data-ttu-id="6b849-149">内容を参照してください、`<h2>`と`<h3>`要素上です。</span><span class="sxs-lookup"><span data-stu-id="6b849-149">See the contents of the `<h2>` and `<h3>` elements above.</span></span>

<span data-ttu-id="6b849-150">前に示したコンテンツの表示は、ユーザーに表示される web ページ全体の一部のみです。</span><span class="sxs-lookup"><span data-stu-id="6b849-150">The view content shown above is only part of the entire webpage that's rendered to the user.</span></span> <span data-ttu-id="6b849-151">ページのレイアウトの残りの部分とビューの他の一般的な側面は、他のビュー ファイルに指定されます。</span><span class="sxs-lookup"><span data-stu-id="6b849-151">The rest of the page's layout and other common aspects of the view are specified in other view files.</span></span> <span data-ttu-id="6b849-152">詳細については、次を参照してください。、[レイアウト トピック](xref:mvc/views/layout)です。</span><span class="sxs-lookup"><span data-stu-id="6b849-152">To learn more, see the [Layout topic](xref:mvc/views/layout).</span></span>

## <a name="how-controllers-specify-views"></a><span data-ttu-id="6b849-153">コント ローラーがビューを指定する方法</span><span class="sxs-lookup"><span data-stu-id="6b849-153">How controllers specify views</span></span>

<span data-ttu-id="6b849-154">ビューは通常の操作から返される、 [ViewResult](/aspnet/core/api/microsoft.aspnetcore.mvc.viewresult)の型である[ActionResult](/aspnet/core/api/microsoft.aspnetcore.mvc.actionresult)です。</span><span class="sxs-lookup"><span data-stu-id="6b849-154">Views are typically returned from actions as a [ViewResult](/aspnet/core/api/microsoft.aspnetcore.mvc.viewresult), which is a type of [ActionResult](/aspnet/core/api/microsoft.aspnetcore.mvc.actionresult).</span></span> <span data-ttu-id="6b849-155">アクション メソッドが作成して返すことができます、`ViewResult`を直接一般的に実行されていないことができます。</span><span class="sxs-lookup"><span data-stu-id="6b849-155">Your action method can create and return a `ViewResult` directly, but that isn't commonly done.</span></span> <span data-ttu-id="6b849-156">ほとんどのコント ローラーが継承ため[コント ローラー](/aspnet/core/api/microsoft.aspnetcore.mvc.controller)、単に使用する、`View`を返すヘルパー メソッド、 `ViewResult`:</span><span class="sxs-lookup"><span data-stu-id="6b849-156">Since most controllers inherit from [Controller](/aspnet/core/api/microsoft.aspnetcore.mvc.controller), you simply use the `View` helper method to return the `ViewResult`:</span></span>

<span data-ttu-id="6b849-157">*HomeController.cs*</span><span class="sxs-lookup"><span data-stu-id="6b849-157">*HomeController.cs*</span></span>

[!code-csharp[Main](../../common/samples/WebApplication1/Controllers/HomeController.cs?highlight=5&range=16-21)]

<span data-ttu-id="6b849-158">この操作から制御が戻るとき、 *About.cshtml*最後のセクションに表示されているビューは、次の web ページとして表示されます。</span><span class="sxs-lookup"><span data-stu-id="6b849-158">When this action returns, the *About.cshtml* view shown in the last section is rendered as the following webpage:</span></span>

![Edge ブラウザーでレンダリングされるページについて](overview/_static/about-page.png)

<span data-ttu-id="6b849-160">`View`ヘルパー メソッドが複数のオーバー ロードします。</span><span class="sxs-lookup"><span data-stu-id="6b849-160">The `View` helper method has several overloads.</span></span> <span data-ttu-id="6b849-161">必要に応じて指定できます。</span><span class="sxs-lookup"><span data-stu-id="6b849-161">You can optionally specify:</span></span>

* <span data-ttu-id="6b849-162">返される明示的なビュー。</span><span class="sxs-lookup"><span data-stu-id="6b849-162">An explicit view to return:</span></span>

  ```csharp
  return View("Orders");
  ```
* <span data-ttu-id="6b849-163">A[モデル](xref:mvc/models/model-binding)に渡す、ビュー。</span><span class="sxs-lookup"><span data-stu-id="6b849-163">A [model](xref:mvc/models/model-binding) to pass to the the view:</span></span>

  ```csharp
  return View(Orders);
  ```
* <span data-ttu-id="6b849-164">ビューとモデルの両方で:</span><span class="sxs-lookup"><span data-stu-id="6b849-164">Both a view and a model:</span></span>

  ```csharp
  return View("Orders", Orders);
  ```

### <a name="view-discovery"></a><span data-ttu-id="6b849-165">ビューの検出</span><span class="sxs-lookup"><span data-stu-id="6b849-165">View discovery</span></span>

<span data-ttu-id="6b849-166">アクションは、ビューを返します、ときに、プロセスを呼び出す*ビュー検出*行われます。</span><span class="sxs-lookup"><span data-stu-id="6b849-166">When an action returns a view, a process called *view discovery* takes place.</span></span> <span data-ttu-id="6b849-167">このプロセスでは、ビュー名に基づいて、どのファイルの表示が使用されるを決定します。</span><span class="sxs-lookup"><span data-stu-id="6b849-167">This process determines which view file is used based on the view name.</span></span> 

<span data-ttu-id="6b849-168">既定の動作、`View`メソッド (`return View();`) を呼び出し元のアクション メソッドと同じ名前のビューを返すことです。</span><span class="sxs-lookup"><span data-stu-id="6b849-168">The default behavior of the `View` method (`return View();`) is to return a view with the same name as the action method from which it's called.</span></span> <span data-ttu-id="6b849-169">たとえば、*に関する*`ActionResult`という名前のビュー ファイルを検索するコント ローラーのメソッド名が使用される*About.cshtml*です。</span><span class="sxs-lookup"><span data-stu-id="6b849-169">For example, the *About* `ActionResult` method name of the controller is used to search for a view file named *About.cshtml*.</span></span> <span data-ttu-id="6b849-170">ランタイムが最初に、検索、*ビュー/[ControllerName]*ビューのフォルダーです。</span><span class="sxs-lookup"><span data-stu-id="6b849-170">First, the runtime looks in the *Views/[ControllerName]* folder for the view.</span></span> <span data-ttu-id="6b849-171">検索に一致するビューがありますが見つからない場合は、 *Shared*ビューのフォルダーです。</span><span class="sxs-lookup"><span data-stu-id="6b849-171">If it doesn't find a matching view there, it searches the *Shared* folder for the view.</span></span>

<span data-ttu-id="6b849-172">暗黙的に返す場合にかかわらず、`ViewResult`で`return View();`にビューの名前を明示的に渡すことも、`View`メソッドを`return View("<ViewName>");`です。</span><span class="sxs-lookup"><span data-stu-id="6b849-172">It doesn't matter if you implicitly return the `ViewResult` with `return View();` or explicitly pass the view name to the `View` method with `return View("<ViewName>");`.</span></span> <span data-ttu-id="6b849-173">どちらの場合は、ビューの検出は、この順序で一致するビュー ファイルを検索します。</span><span class="sxs-lookup"><span data-stu-id="6b849-173">In both cases, view discovery searches for a matching view file in this order:</span></span>

   1. <span data-ttu-id="6b849-174">*ビュー/\[ControllerName]\[ViewName] .cshtml*</span><span class="sxs-lookup"><span data-stu-id="6b849-174">*Views/\[ControllerName]\[ViewName].cshtml*</span></span>
   1. <span data-ttu-id="6b849-175">*ビュー/共有/\[ViewName] .cshtml*</span><span class="sxs-lookup"><span data-stu-id="6b849-175">*Views/Shared/\[ViewName].cshtml*</span></span>

<span data-ttu-id="6b849-176">ビュー名の代わりに、ビューのファイル パスを指定できます。</span><span class="sxs-lookup"><span data-stu-id="6b849-176">A view file path can be provided instead of a view name.</span></span> <span data-ttu-id="6b849-177">アプリのルートから始まる絶対パスを使用した場合 (必要に応じて開始され、「/」または"~/") では、 *.cshtml*拡張機能を指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="6b849-177">If using an absolute path starting at the app root (optionally starting with "/" or "~/"), the *.cshtml* extension must be specified:</span></span>

```csharp
return View("Views/Home/About.cshtml");
```

<span data-ttu-id="6b849-178">相対パスを使用することがなく異なるディレクトリにビューを指定する、 *.cshtml*拡張機能です。</span><span class="sxs-lookup"><span data-stu-id="6b849-178">You can also use a relative path to specify views in different directories without the *.cshtml* extension.</span></span> <span data-ttu-id="6b849-179">内部、 `HomeController`、返すことができます、*インデックス*の表示、*管理*相対パスを持つビュー。</span><span class="sxs-lookup"><span data-stu-id="6b849-179">Inside the `HomeController`, you can return the *Index* view of your *Manage* views with a relative path:</span></span>

```csharp
return View("../Manage/Index");
```

<span data-ttu-id="6b849-180">同様に、現在のコント ローラーに固有のディレクトリでを指定することができます、"./"プレフィックス。</span><span class="sxs-lookup"><span data-stu-id="6b849-180">Similarly, you can indicate the current controller-specific directory with the "./" prefix:</span></span>

```csharp
return View("./About");
```

<span data-ttu-id="6b849-181">[部分ビュー](xref:mvc/views/partial)と[コンポーネントを表示](xref:mvc/views/view-components)似ています (ただしと一致しない) の検出メカニズムを使用します。</span><span class="sxs-lookup"><span data-stu-id="6b849-181">[Partial views](xref:mvc/views/partial) and [view components](xref:mvc/views/view-components) use similar (but not identical) discovery mechanisms.</span></span>

<span data-ttu-id="6b849-182">どのビューは、アプリ内にあるを使用して、カスタムの既定の規則をカスタマイズする[IViewLocationExpander](/aspnet/core/api/microsoft.aspnetcore.mvc.razor.iviewlocationexpander)です。</span><span class="sxs-lookup"><span data-stu-id="6b849-182">You can customize the default convention for how views are located within the app by using a custom [IViewLocationExpander](/aspnet/core/api/microsoft.aspnetcore.mvc.razor.iviewlocationexpander).</span></span>

<span data-ttu-id="6b849-183">ビューの検出は、ファイル名でファイルの表示を検出することに依存しています。</span><span class="sxs-lookup"><span data-stu-id="6b849-183">View discovery relies on finding view files by file name.</span></span> <span data-ttu-id="6b849-184">基になるファイル システムが大文字と小文字の場合は、ビューの名前はおそらく大文字小文字を区別です。</span><span class="sxs-lookup"><span data-stu-id="6b849-184">If the underlying file system is case sensitive, view names are probably case sensitive.</span></span> <span data-ttu-id="6b849-185">オペレーティング システム間で互換性のため、コント ローラーとアクション名および関連するビューのフォルダーとファイル名の間のケースに一致します。</span><span class="sxs-lookup"><span data-stu-id="6b849-185">For compatibility across operating systems, match case between controller and action names and associated view folders and file names.</span></span> <span data-ttu-id="6b849-186">ファイルの表示を区別するファイル システムの操作中に検出できないエラーが発生した場合は、要求されたビュー ファイルと実際のビューのファイル名の大文字と小文字が一致していることを確認します。</span><span class="sxs-lookup"><span data-stu-id="6b849-186">If you encounter an error that a view file can't be found while working with a case-sensitive file system, confirm that the casing matches between the requested view file and the actual view file name.</span></span>

<span data-ttu-id="6b849-187">コント ローラー、アクション、および保守容易性とわかりやすくするためのビューの間の関係を反映するように、ビューのファイル構造を整理するためのベスト プラクティスに従ってください。</span><span class="sxs-lookup"><span data-stu-id="6b849-187">Follow the best practice of organizing the file structure for your views to reflect the relationships among controllers, actions, and views for maintainability and clarity.</span></span>

## <a name="passing-data-to-views"></a><span data-ttu-id="6b849-188">ビューにデータを渡す</span><span class="sxs-lookup"><span data-stu-id="6b849-188">Passing data to views</span></span>

<span data-ttu-id="6b849-189">いくつかのアプローチを使用して、ビューにデータを渡すことができます。</span><span class="sxs-lookup"><span data-stu-id="6b849-189">You can pass data to views using several approaches.</span></span> <span data-ttu-id="6b849-190">最も堅牢な方法は、指定する、[モデル](xref:mvc/models/model-binding)ビュー内の型。</span><span class="sxs-lookup"><span data-stu-id="6b849-190">The most robust approach is to specify a [model](xref:mvc/models/model-binding) type in the view.</span></span> <span data-ttu-id="6b849-191">このモデルと呼ばれる一般的な*viewmodel*です。</span><span class="sxs-lookup"><span data-stu-id="6b849-191">This model is commonly referred to as a *viewmodel*.</span></span> <span data-ttu-id="6b849-192">Viewmodel 型のインスタンスは、アクションからビューに渡します。</span><span class="sxs-lookup"><span data-stu-id="6b849-192">You pass an instance of the viewmodel type to the view from the action.</span></span>

<span data-ttu-id="6b849-193">により、利用するためにビューをビューにデータを渡して、viewmodel を使用して*強力な*型チェックします。</span><span class="sxs-lookup"><span data-stu-id="6b849-193">Using a viewmodel to pass data to a view allows the view to take advantage of *strong* type checking.</span></span> <span data-ttu-id="6b849-194">*厳密な型指定*(または*厳密に型指定された*) すべての変数および定数では、明示的に定義された型 (たとえば、 `string`、 `int`、または`DateTime`)。</span><span class="sxs-lookup"><span data-stu-id="6b849-194">*Strong typing* (or *strongly-typed*) means that every variable and constant has an explicitly defined type (for example, `string`, `int`, or `DateTime`).</span></span> <span data-ttu-id="6b849-195">ビューで使用される型の妥当性は、コンパイル時にチェックされます。</span><span class="sxs-lookup"><span data-stu-id="6b849-195">The validity of types used in a view is checked at compile time.</span></span>

<span data-ttu-id="6b849-196">[Visual Studio](https://www.visualstudio.com/vs/)と[Visual Studio Code](https://code.visualstudio.com/)と呼ばれる機能を使用して、厳密に型指定されたクラス メンバーを一覧表示[IntelliSense](/visualstudio/ide/using-intellisense)です。</span><span class="sxs-lookup"><span data-stu-id="6b849-196">[Visual Studio](https://www.visualstudio.com/vs/) and [Visual Studio Code](https://code.visualstudio.com/) list strongly-typed class members using a feature called [IntelliSense](/visualstudio/ide/using-intellisense).</span></span> <span data-ttu-id="6b849-197">Viewmodel のプロパティを表示する場合は、入力変数名のピリオドが続く viewmodel (`.`)。</span><span class="sxs-lookup"><span data-stu-id="6b849-197">When you want to see the properties of a viewmodel, type the variable name for the viewmodel followed by a period (`.`).</span></span> <span data-ttu-id="6b849-198">これにより、エラーの少ないコードをより早く作成できます。</span><span class="sxs-lookup"><span data-stu-id="6b849-198">This helps you write code faster with fewer errors.</span></span>

<span data-ttu-id="6b849-199">使用してモデルを指定して、`@model`ディレクティブです。</span><span class="sxs-lookup"><span data-stu-id="6b849-199">Specify a model using the `@model` directive.</span></span> <span data-ttu-id="6b849-200">使用してモデルを使用して`@Model`:</span><span class="sxs-lookup"><span data-stu-id="6b849-200">Use the model with `@Model`:</span></span>

```cshtml
@model WebApplication1.ViewModels.Address

<h2>Contact</h2>
<address>
    @Model.Street<br>
    @Model.City, @Model.State @Model.PostalCode<br>
    <abbr title="Phone">P:</abbr> 425.555.0100
</address>
```

<span data-ttu-id="6b849-201">ビューにモデルを提供するには、コント ローラーは、それをパラメーターとして渡します。</span><span class="sxs-lookup"><span data-stu-id="6b849-201">To provide the model to the view, the controller passes it as a parameter:</span></span>

```csharp
public IActionResult Contact()
{
    ViewData["Message"] = "Your contact page.";

    var viewModel = new Address()
    {
        Name = "Microsoft",
        Street = "One Microsoft Way",
        City = "Redmond",
        State = "WA",
        PostalCode = "98052-6399"
    };

    return View(viewModel);
}
```

<span data-ttu-id="6b849-202">ビューを提供できるモデルの種類に制限はありません。</span><span class="sxs-lookup"><span data-stu-id="6b849-202">There are no restrictions on the model types that you can provide to a view.</span></span> <span data-ttu-id="6b849-203">使用することをお勧め**P**lain **O**%ld **C**LR **O**オブジェクト (POCO) viewmodels ほとんどまたはまったく動作 (メソッド) を定義します。</span><span class="sxs-lookup"><span data-stu-id="6b849-203">We recommend using **P**lain **O**ld **C**LR **O**bject (POCO) viewmodels with little or no behavior (methods) defined.</span></span> <span data-ttu-id="6b849-204">通常、viewmodel クラスは、いずれかに格納されて、*モデル*フォルダーまたは個別の*ViewModels*アプリのルートにあるフォルダーです。</span><span class="sxs-lookup"><span data-stu-id="6b849-204">Usually, viewmodel classes are either stored in the *Models* folder or a separate *ViewModels* folder at the root of the app.</span></span> <span data-ttu-id="6b849-205">*アドレス*viewmodel 上記の例で使用される、という名前のファイルに格納されている POCO viewmodel *Address.cs*:</span><span class="sxs-lookup"><span data-stu-id="6b849-205">The *Address* viewmodel used in the example above is a POCO viewmodel stored in a file named *Address.cs*:</span></span>

```csharp
namespace WebApplication1.ViewModels
{
    public class Address
    {
        public string Name { get; set; }
        public string Street { get; set; }
        public string City { get; set; }
        public string State { get; set; }
        public string PostalCode { get; set; }
    }
}
```

> [!NOTE]
> <span data-ttu-id="6b849-206">Viewmodel 型やビジネス モデルの種類の両方を同じクラスを使用して何もできません。</span><span class="sxs-lookup"><span data-stu-id="6b849-206">Nothing prevents you from using the same classes for both your viewmodel types and your business model types.</span></span> <span data-ttu-id="6b849-207">ただし、別のモデルを使用してでは、ビューとは異なるいない個別にビジネス ロジックとデータ、アプリのアクセスの部分です。</span><span class="sxs-lookup"><span data-stu-id="6b849-207">However, using separate models allows your views to vary independently from the business logic and data access parts of your app.</span></span> <span data-ttu-id="6b849-208">モデルと viewmodels の分離はセキュリティ上の利点をモデルで使用する場合にも[モデル バインディング](xref:mvc/models/model-binding)と[検証](xref:mvc/models/validation)ユーザーがアプリに送信されるデータにします。</span><span class="sxs-lookup"><span data-stu-id="6b849-208">Separation of models and viewmodels also offers security benefits when models use [model binding](xref:mvc/models/model-binding) and [validation](xref:mvc/models/validation) for data sent to the app by the user.</span></span>


<a name="VD_VB"></a>

### <a name="weakly-typed-data-viewdata-and-viewbag"></a><span data-ttu-id="6b849-209">弱い型指定のデータ (ViewData と ViewBag)</span><span class="sxs-lookup"><span data-stu-id="6b849-209">Weakly-typed data (ViewData and ViewBag)</span></span>

<span data-ttu-id="6b849-210">注: `ViewBag` Razor ページでは使用できません。</span><span class="sxs-lookup"><span data-stu-id="6b849-210">Note: `ViewBag` is not available in the Razor Pages.</span></span>

<span data-ttu-id="6b849-211">ビューへのアクセスのある、厳密に型指定されたビューだけでなく、*弱い型指定*(とも呼ばれる*弱い型指定*) データのコレクション。</span><span class="sxs-lookup"><span data-stu-id="6b849-211">In addition to strongly-typed views, views have access to a *weakly-typed* (also called *loosely-typed*) collection of data.</span></span> <span data-ttu-id="6b849-212">厳密な型とは異なり*弱い型*(または*型が失われる*) 使用するデータの型を明示的に宣言しないことを意味します。</span><span class="sxs-lookup"><span data-stu-id="6b849-212">Unlike strong types, *weak types* (or *loose types*) means that you don't explicitly declare the type of data you're using.</span></span> <span data-ttu-id="6b849-213">少量のコント ローラーとビューとの間のデータを渡すため、厳密に型指定されたデータのコレクションを使用できます。</span><span class="sxs-lookup"><span data-stu-id="6b849-213">You can use the collection of weakly-typed data for passing small amounts of data in and out of controllers and views.</span></span>

| <span data-ttu-id="6b849-214">間でデータを渡すことをしています.</span><span class="sxs-lookup"><span data-stu-id="6b849-214">Passing data between a ...</span></span>                        | <span data-ttu-id="6b849-215">例</span><span class="sxs-lookup"><span data-stu-id="6b849-215">Example</span></span>                                                                        |
| ------------------------------------------------- | ------------------------------------------------------------------------------ |
| <span data-ttu-id="6b849-216">コント ローラーとビュー</span><span class="sxs-lookup"><span data-stu-id="6b849-216">Controller and a view</span></span>                             | <span data-ttu-id="6b849-217">ドロップダウン リストをデータを作成します。</span><span class="sxs-lookup"><span data-stu-id="6b849-217">Populating a dropdown list with data.</span></span>                                          |
| <span data-ttu-id="6b849-218">ビューと[[レイアウト] ビュー](xref:mvc/views/layout)</span><span class="sxs-lookup"><span data-stu-id="6b849-218">View and a [layout view](xref:mvc/views/layout)</span></span>   | <span data-ttu-id="6b849-219">設定、 **\<タイトル >**ビュー ファイルから、レイアウト ビューの要素の内容。</span><span class="sxs-lookup"><span data-stu-id="6b849-219">Setting the **\<title>** element content in the layout view from a view file.</span></span>  |
| <span data-ttu-id="6b849-220">[部分ビュー](xref:mvc/views/partial)とビュー</span><span class="sxs-lookup"><span data-stu-id="6b849-220">[Partial view](xref:mvc/views/partial) and a view</span></span> | <span data-ttu-id="6b849-221">ユーザーが要求した web ページに基づいてデータを表示するウィジェット。</span><span class="sxs-lookup"><span data-stu-id="6b849-221">A widget that displays data based on the webpage that the user requested.</span></span>      |

<span data-ttu-id="6b849-222">このコレクションは、いずれかで参照できる、`ViewData`または`ViewBag`コント ローラーとビューのプロパティです。</span><span class="sxs-lookup"><span data-stu-id="6b849-222">This collection can be referenced through either the `ViewData` or `ViewBag` properties on controllers and views.</span></span> <span data-ttu-id="6b849-223">`ViewData`プロパティは、弱い型指定のオブジェクトのディクショナリ。</span><span class="sxs-lookup"><span data-stu-id="6b849-223">The `ViewData` property is a dictionary of weakly-typed objects.</span></span> <span data-ttu-id="6b849-224">`ViewBag`プロパティはラッパー `ViewData` 、基になるの動的なプロパティを提供する`ViewData`コレクション。</span><span class="sxs-lookup"><span data-stu-id="6b849-224">The `ViewBag` property is a wrapper around `ViewData` that provides dynamic properties for the underlying `ViewData` collection.</span></span>

<span data-ttu-id="6b849-225">`ViewData`および`ViewBag`は実行時に動的に解決されます。</span><span class="sxs-lookup"><span data-stu-id="6b849-225">`ViewData` and `ViewBag` are dynamically resolved at runtime.</span></span> <span data-ttu-id="6b849-226">コンパイル時の型チェック見て、どちらも通常よりエラーを起こしやすい、viewmodel を使用するよりもです。</span><span class="sxs-lookup"><span data-stu-id="6b849-226">Since they don't offer compile-time type checking, both are generally more error-prone than using a viewmodel.</span></span> <span data-ttu-id="6b849-227">そのため、一部の開発者が最小限に抑えるまたはまったく使用しないたい`ViewData`と`ViewBag`です。</span><span class="sxs-lookup"><span data-stu-id="6b849-227">For that reason, some developers prefer to minimally or never use `ViewData` and `ViewBag`.</span></span>


<a name="VD"></a>

<span data-ttu-id="6b849-228">**ViewData**</span><span class="sxs-lookup"><span data-stu-id="6b849-228">**ViewData**</span></span>

<span data-ttu-id="6b849-229">`ViewData`[ViewDataDictionary](/aspnet/core/api/microsoft.aspnetcore.mvc.viewfeatures.viewdatadictionary)を介してアクセスするオブジェクト`string`キー。</span><span class="sxs-lookup"><span data-stu-id="6b849-229">`ViewData` is a [ViewDataDictionary](/aspnet/core/api/microsoft.aspnetcore.mvc.viewfeatures.viewdatadictionary) object accessed through `string` keys.</span></span> <span data-ttu-id="6b849-230">その他のキャストする必要がありますが、文字列データを格納し、キャストの必要性なしで直接使用`ViewData`オブジェクトの値を特定の型に抽出するときにします。</span><span class="sxs-lookup"><span data-stu-id="6b849-230">String data can be stored and used directly without the need for a cast, but you must cast other `ViewData` object values to specific types when you extract them.</span></span> <span data-ttu-id="6b849-231">使用することができます`ViewData`およびなどのビュー内でビューをビューには、コント ローラーからデータを渡す[部分ビュー](xref:mvc/views/partial)と[レイアウト](xref:mvc/views/layout)です。</span><span class="sxs-lookup"><span data-stu-id="6b849-231">You can use `ViewData` to pass data from controllers to views and within views, including [partial views](xref:mvc/views/partial) and [layouts](xref:mvc/views/layout).</span></span>

<span data-ttu-id="6b849-232">するとあいさつ文とアドレスを使用して、値を設定する例を次に示します`ViewData`アクションで。</span><span class="sxs-lookup"><span data-stu-id="6b849-232">The following is an example that sets values for a greeting and an address using `ViewData` in an action:</span></span>

```csharp
public IActionResult SomeAction()
{
    ViewData["Greeting"] = "Hello";
    ViewData["Address"]  = new Address()
    {
        Name = "Steve",
        Street = "123 Main St",
        City = "Hudson",
        State = "OH",
        PostalCode = "44236"
    };

    return View();
}
```

<span data-ttu-id="6b849-233">ビューでデータを操作します。</span><span class="sxs-lookup"><span data-stu-id="6b849-233">Work with the data in a view:</span></span>

```cshtml
@{
    // Since Address isn't a string, it requires a cast.
    var address = ViewData["Address"] as Address;
}

@ViewData["Greeting"] World!

<address>
    @address.Name<br>
    @address.Street<br>
    @address.City, @address.State @address.PostalCode
</address>
```

<span data-ttu-id="6b849-234">**ViewBag**</span><span class="sxs-lookup"><span data-stu-id="6b849-234">**ViewBag**</span></span>

<span data-ttu-id="6b849-235">注: `ViewBag` Razor ページでは使用できません。</span><span class="sxs-lookup"><span data-stu-id="6b849-235">Note: `ViewBag` is not available in the Razor Pages.</span></span>

<span data-ttu-id="6b849-236">`ViewBag`[DynamicViewData](/aspnet/core/api/microsoft.aspnetcore.mvc.viewfeatures.internal.dynamicviewdata)に格納されているオブジェクトへの動的アクセスを提供するオブジェクト`ViewData`です。</span><span class="sxs-lookup"><span data-stu-id="6b849-236">`ViewBag` is a [DynamicViewData](/aspnet/core/api/microsoft.aspnetcore.mvc.viewfeatures.internal.dynamicviewdata) object that provides dynamic access to the objects stored in `ViewData`.</span></span> <span data-ttu-id="6b849-237">`ViewBag`簡単にキャストする必要がないため、操作を指定できます。</span><span class="sxs-lookup"><span data-stu-id="6b849-237">`ViewBag` can be more convenient to work with, since it doesn't require casting.</span></span> <span data-ttu-id="6b849-238">次の例は、使用する方法を示しています。`ViewBag`を使用するのと同じ結果に`ViewData`上。</span><span class="sxs-lookup"><span data-stu-id="6b849-238">The following example shows how to use `ViewBag` with the same result as using `ViewData` above:</span></span>

```csharp
public IActionResult SomeAction()
{
    ViewBag.Greeting = "Hello";
    ViewBag.Address  = new Address()
    {
        Name = "Steve",
        Street = "123 Main St",
        City = "Hudson",
        State = "OH",
        PostalCode = "44236"
    };

    return View();
}
```

```cshtml
@ViewBag.Greeting World!

<address>
    @ViewBag.Address.Name<br>
    @ViewBag.Address.Street<br>
    @ViewBag.Address.City, @ViewBag.Address.State @ViewBag.Address.PostalCode
</address>
```

<span data-ttu-id="6b849-239">**ViewBag、ViewData を同時に使用します。**</span><span class="sxs-lookup"><span data-stu-id="6b849-239">**Using ViewData and ViewBag simultaneously**</span></span>

<span data-ttu-id="6b849-240">注: `ViewBag` Razor ページでは使用できません。</span><span class="sxs-lookup"><span data-stu-id="6b849-240">Note: `ViewBag` is not available in the Razor Pages.</span></span>

<span data-ttu-id="6b849-241">`ViewData`と`ViewBag`同じ基になるを参照してください`ViewData`コレクション、両方を使用することができます`ViewData`と`ViewBag`を混在させるし、値を読み書きするときにそれらの間に一致します。</span><span class="sxs-lookup"><span data-stu-id="6b849-241">Since `ViewData` and `ViewBag` refer to the same underlying `ViewData` collection, you can use both `ViewData` and `ViewBag` and mix and match between them when reading and writing values.</span></span>

<span data-ttu-id="6b849-242">設定を使用して、タイトル`ViewBag`を使用して、および`ViewData`の上部にある、 *About.cshtml*ビュー。</span><span class="sxs-lookup"><span data-stu-id="6b849-242">Set the title using `ViewBag` and the description using `ViewData` at the top of an *About.cshtml* view:</span></span>

```cshtml
@{
    Layout = "/Views/Shared/_Layout.cshtml";
    ViewBag.Title = "About Contoso";
    ViewData["Description"] = "Let us tell you about Contoso's philosophy and mission.";
}
```

<span data-ttu-id="6b849-243">プロパティを読み取るがの使用を反転`ViewData`と`ViewBag`です。</span><span class="sxs-lookup"><span data-stu-id="6b849-243">Read the properties but reverse the use of `ViewData` and `ViewBag`.</span></span> <span data-ttu-id="6b849-244">*_Layout.cshtml*ファイルを使用して、タイトルを入手してください`ViewData`しを使用して、取得する`ViewBag`:</span><span class="sxs-lookup"><span data-stu-id="6b849-244">In the *_Layout.cshtml* file, obtain the title using `ViewData` and obtain the description using `ViewBag`:</span></span>

```cshtml
<!DOCTYPE html>
<html lang="en">
<head>
    <title>@ViewData["Title"]</title>
    <meta name="description" content="@ViewBag.Description">
    ...
```

<span data-ttu-id="6b849-245">文字列でのキャストを必要としないことに注意してください`ViewData`です。</span><span class="sxs-lookup"><span data-stu-id="6b849-245">Remember that strings don't require a cast for `ViewData`.</span></span> <span data-ttu-id="6b849-246">使用することができます`@ViewData["Title"]`キャストなし。</span><span class="sxs-lookup"><span data-stu-id="6b849-246">You can use `@ViewData["Title"]` without casting.</span></span>

<span data-ttu-id="6b849-247">両方を使用して`ViewData`と`ViewBag`に混在させると、読み取りと書き込みのプロパティに一致すると、同じ時間動作します。</span><span class="sxs-lookup"><span data-stu-id="6b849-247">Using both `ViewData` and `ViewBag` at the same time works, as does mixing and matching reading and writing the properties.</span></span> <span data-ttu-id="6b849-248">次のマークアップがレンダリングされます。</span><span class="sxs-lookup"><span data-stu-id="6b849-248">The following markup is rendered:</span></span>

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <title>About Contoso</title>
    <meta name="description" content="Let us tell you about Contoso's philosophy and mission.">
    ...
```

<span data-ttu-id="6b849-249">**ViewBag、ViewData の違いの概要**</span><span class="sxs-lookup"><span data-stu-id="6b849-249">**Summary of the differences between ViewData and ViewBag**</span></span>

 <span data-ttu-id="6b849-250">`ViewBag`Razor ページで使用できません。</span><span class="sxs-lookup"><span data-stu-id="6b849-250">`ViewBag` is not available in the Razor Pages.</span></span>

* `ViewData`
  * <span data-ttu-id="6b849-251">派生した[ViewDataDictionary](/aspnet/core/api/microsoft.aspnetcore.mvc.viewfeatures.viewdatadictionary)など、役に立ちます辞書プロパティがあるため、 `ContainsKey`、 `Add`、 `Remove`、および`Clear`です。</span><span class="sxs-lookup"><span data-stu-id="6b849-251">Derives from [ViewDataDictionary](/aspnet/core/api/microsoft.aspnetcore.mvc.viewfeatures.viewdatadictionary), so it has dictionary properties that can be useful, such as `ContainsKey`, `Add`, `Remove`, and `Clear`.</span></span>
  * <span data-ttu-id="6b849-252">ディクショナリ内のキーは、空白が許可されているために、文字列、です。</span><span class="sxs-lookup"><span data-stu-id="6b849-252">Keys in the dictionary are strings, so whitespace is allowed.</span></span> <span data-ttu-id="6b849-253">例 : `ViewData["Some Key With Whitespace"]`</span><span class="sxs-lookup"><span data-stu-id="6b849-253">Example: `ViewData["Some Key With Whitespace"]`</span></span>
  * <span data-ttu-id="6b849-254">任意の型以外の場合、`string`を使用するビューでキャストする必要があります`ViewData`です。</span><span class="sxs-lookup"><span data-stu-id="6b849-254">Any type other than a `string` must be cast in the view to use `ViewData`.</span></span>
* `ViewBag`
  * <span data-ttu-id="6b849-255">派生した[DynamicViewData](/aspnet/core/api/microsoft.aspnetcore.mvc.viewfeatures.internal.dynamicviewdata)が、ドット表記を使用して動的なプロパティの作成を許可するため、(`@ViewBag.SomeKey = <value or object>`)、キャストは必要ありません。</span><span class="sxs-lookup"><span data-stu-id="6b849-255">Derives from [DynamicViewData](/aspnet/core/api/microsoft.aspnetcore.mvc.viewfeatures.internal.dynamicviewdata), so it allows the creation of dynamic properties using dot notation (`@ViewBag.SomeKey = <value or object>`), and no casting is required.</span></span> <span data-ttu-id="6b849-256">構文`ViewBag`コント ローラーとビューを追加する方が手軽になります。</span><span class="sxs-lookup"><span data-stu-id="6b849-256">The syntax of `ViewBag` makes it quicker to add to controllers and views.</span></span>
  * <span data-ttu-id="6b849-257">Null 値をチェックする方が簡単です。</span><span class="sxs-lookup"><span data-stu-id="6b849-257">Simpler to check for null values.</span></span> <span data-ttu-id="6b849-258">例 : `@ViewBag.Person?.Name`</span><span class="sxs-lookup"><span data-stu-id="6b849-258">Example: `@ViewBag.Person?.Name`</span></span>

<span data-ttu-id="6b849-259">**ViewBag、ViewData、またはを使用する場合**</span><span class="sxs-lookup"><span data-stu-id="6b849-259">**When to use ViewData or ViewBag**</span></span>

<span data-ttu-id="6b849-260">両方`ViewData`と`ViewBag`少量のコント ローラーとビューの間でデータを渡すための有効なアプローチでは同じようにします。</span><span class="sxs-lookup"><span data-stu-id="6b849-260">Both `ViewData` and `ViewBag` are equally valid approaches for passing small amounts of data among controllers and views.</span></span> <span data-ttu-id="6b849-261">基本設定に基づいて使用するかを選択します。</span><span class="sxs-lookup"><span data-stu-id="6b849-261">The choice of which one to use is based on preference.</span></span> <span data-ttu-id="6b849-262">混在して一致`ViewData`と`ViewBag`オブジェクトは、コードが読みやすくし、一貫して使用方法の 1 つを維持します。</span><span class="sxs-lookup"><span data-stu-id="6b849-262">You can mix and match `ViewData` and `ViewBag` objects, however, the code is easier to read and maintain with one approach used consistently.</span></span> <span data-ttu-id="6b849-263">両方の方法は、実行時に動的に解決される原因で、実行時エラーが発生しやすくします。</span><span class="sxs-lookup"><span data-stu-id="6b849-263">Both approaches are dynamically resolved at runtime and thus prone to causing runtime errors.</span></span> <span data-ttu-id="6b849-264">一部の開発チームは、それを回避します。</span><span class="sxs-lookup"><span data-stu-id="6b849-264">Some development teams avoid them.</span></span>

### <a name="dynamic-views"></a><span data-ttu-id="6b849-265">動的ビュー</span><span class="sxs-lookup"><span data-stu-id="6b849-265">Dynamic views</span></span>

<span data-ttu-id="6b849-266">使用して、モデルは宣言しないでビュー型`@model`に渡されたモデルのインスタンスがあるが (たとえば、 `return View(Address);`) 動的にインスタンスのプロパティを参照できます。</span><span class="sxs-lookup"><span data-stu-id="6b849-266">Views that don't declare a model type using `@model` but that have a model instance passed to them (for example, `return View(Address);`) can reference the instance's properties dynamically:</span></span>

```cshtml
<address>
    @Model.Street<br>
    @Model.City, @Model.State @Model.PostalCode<br>
    <abbr title="Phone">P:</abbr> 425.555.0100
</address>
```

<span data-ttu-id="6b849-267">この機能は、柔軟性を提供していますが、コンパイルの保護や IntelliSense は提供していません。</span><span class="sxs-lookup"><span data-stu-id="6b849-267">This feature offers flexibility but doesn't offer compilation protection or IntelliSense.</span></span> <span data-ttu-id="6b849-268">プロパティが存在しない場合は、実行時に web ページの生成が失敗します。</span><span class="sxs-lookup"><span data-stu-id="6b849-268">If the property doesn't exist, webpage generation fails at runtime.</span></span>

## <a name="more-view-features"></a><span data-ttu-id="6b849-269">詳細ビュー</span><span class="sxs-lookup"><span data-stu-id="6b849-269">More view features</span></span>

<span data-ttu-id="6b849-270">[タグ ヘルパー](xref:mvc/views/tag-helpers/intro)容易に既存の HTML タグにサーバー側の動作を追加します。</span><span class="sxs-lookup"><span data-stu-id="6b849-270">[Tag Helpers](xref:mvc/views/tag-helpers/intro) make it easy to add server-side behavior to existing HTML tags.</span></span> <span data-ttu-id="6b849-271">タグ ヘルパーを使用するには、カスタム コードや、ビューの中でヘルパーを記述する必要が回避できます。</span><span class="sxs-lookup"><span data-stu-id="6b849-271">Using Tag Helpers avoids the need to write custom code or helpers within your views.</span></span> <span data-ttu-id="6b849-272">タグ ヘルパーは、HTML 要素に属性として適用され、処理できないエディターでは無視されます。</span><span class="sxs-lookup"><span data-stu-id="6b849-272">Tag helpers are applied as attributes to HTML elements and are ignored by editors that can't process them.</span></span> <span data-ttu-id="6b849-273">これにより、さまざまなツールのビューのマークアップを表示して編集できます。</span><span class="sxs-lookup"><span data-stu-id="6b849-273">This allows you to edit and render view markup in a variety of tools.</span></span>

<span data-ttu-id="6b849-274">カスタムの HTML マークアップを生成するは、多くの組み込み HTML ヘルパーを実現できます。</span><span class="sxs-lookup"><span data-stu-id="6b849-274">Generating custom HTML markup can be achieved with many built-in HTML Helpers.</span></span> <span data-ttu-id="6b849-275">複雑なユーザー インターフェイス ロジックで処理できる[ビュー コンポーネント](xref:mvc/views/view-components)です。</span><span class="sxs-lookup"><span data-stu-id="6b849-275">More complex user interface logic can be handled by [View Components](xref:mvc/views/view-components).</span></span> <span data-ttu-id="6b849-276">ビューのコンポーネントは、同じ SoC そのコント ローラーを提供し、ビューを提供します。</span><span class="sxs-lookup"><span data-stu-id="6b849-276">View components provide the same SoC that controllers and views offer.</span></span> <span data-ttu-id="6b849-277">アクションおよび一般的なユーザー インターフェイス要素で使用されるデータを処理するビューの必要をなくしことができます。</span><span class="sxs-lookup"><span data-stu-id="6b849-277">They can eliminate the need for actions and views that deal with data used by common user interface elements.</span></span>

<span data-ttu-id="6b849-278">ASP.NET Core の他の多くの側面と同様にサポートをビュー[依存性の注入](xref:fundamentals/dependency-injection)、するサービスを許可する[ビューに挿入される](xref:mvc/views/dependency-injection)です。</span><span class="sxs-lookup"><span data-stu-id="6b849-278">Like many other aspects of ASP.NET Core, views support [dependency injection](xref:fundamentals/dependency-injection), allowing services to be [injected into views](xref:mvc/views/dependency-injection).</span></span>