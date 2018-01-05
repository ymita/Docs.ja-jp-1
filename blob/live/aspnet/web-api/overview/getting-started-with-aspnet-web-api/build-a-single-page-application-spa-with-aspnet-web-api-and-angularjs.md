---
uid: web-api/overview/getting-started-with-aspnet-web-api/build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs
title: "ハンズ オン ラボ: ビルドと ASP.NET Web API および Angular.js シングル ページ アプリケーション (SPA) |Microsoft ドキュメント"
author: rick-anderson
description: "従来の web アプリケーションでは、クライアント (ブラウザー) は、ページを要求することによって、サーバーとの通信を開始します。 サーバーは、要求を処理しています."
ms.author: aspnetcontent
manager: wpickett
ms.date: 09/30/2015
ms.topic: article
ms.assetid: 719727b7-bef3-45ad-bfe9-ba5bcdb2305f
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/getting-started-with-aspnet-web-api/build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs
msc.type: authoredcontent
ms.openlocfilehash: 9a748628d53878be380869ac5327de0111d2284d
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/10/2017
---
<a name="hands-on-lab-build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs"></a><span data-ttu-id="6fbeb-104">ハンズ オン ラボ: ビルドと ASP.NET Web API および Angular.js シングル ページ アプリケーション (SPA)</span><span class="sxs-lookup"><span data-stu-id="6fbeb-104">Hands On Lab: Build a Single Page Application (SPA) with ASP.NET Web API and Angular.js</span></span>
====================
<span data-ttu-id="6fbeb-105">によって[Web キャンプ チーム](https://twitter.com/webcamps)</span><span class="sxs-lookup"><span data-stu-id="6fbeb-105">by [Web Camps Team](https://twitter.com/webcamps)</span></span>

[<span data-ttu-id="6fbeb-106">Web キャンプ トレーニング キットをダウンロードします。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-106">Download Web Camps Training Kit</span></span>](http://aka.ms/webcamps-training-kit)

> <span data-ttu-id="6fbeb-107">従来の web アプリケーションでは、クライアント (ブラウザー) は、ページを要求することによって、サーバーとの通信を開始します。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-107">In traditional web applications, the client (browser) initiates the communication with the server by requesting a page.</span></span> <span data-ttu-id="6fbeb-108">サーバーは要求を処理し、ページの HTML クライアントに送信します。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-108">The server then processes the request and sends the HTML of the page to the client.</span></span> <span data-ttu-id="6fbeb-109">– ユーザーなどのリンクに移動またはフォームにデータを送信する – ページと後続のやり取りで新しい要求が、サーバーに送信され、フローをもう一度開始しますサーバーが要求を処理し、新しいページが新しいアクションの要求に応答してブラウザーに送信。クライアントによって ed です。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-109">In subsequent interactions with the page –e.g. the user navigates to a link or submits a form with data– a new request is sent to the server, and the flow starts again: the server processes the request and sends a new page to the browser in response to the new action requested by the client.</span></span>
> 
> <span data-ttu-id="6fbeb-110">単一ページ アプリケーション (SPAs) では、ブラウザーでページ全体を読み込む後、最初の要求が Ajax 要求を介して以降の操作が行わ。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-110">In Single-Page Applications (SPAs) the entire page is loaded in the browser after the initial request, but subsequent interactions take place through Ajax requests.</span></span> <span data-ttu-id="6fbeb-111">つまり、ブラウザーが変更されたページの部分のみを更新するにはページ全体を再読み込みする必要はありません。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-111">This means that the browser has to update only the portion of the page that has changed; there is no need to reload the entire page.</span></span> <span data-ttu-id="6fbeb-112">SPA アプローチより滑らかなエクスペリエンスに結果として得られる、ユーザー アクションに応答するアプリケーションでは時間が短縮されます。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-112">The SPA approach reduces the time taken by the application to respond to user actions, resulting in a more fluid experience.</span></span>
> 
> <span data-ttu-id="6fbeb-113">SPA のアーキテクチャでは、いくつかの課題が従来の web アプリケーションではありません。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-113">The architecture of a SPA involves certain challenges that are not present in traditional web applications.</span></span> <span data-ttu-id="6fbeb-114">ただし、AngularJS などの JavaScript フレームワークの ASP.NET Web API などのテクノロジに出現する、し CSS3 によって提供される新しいスタイル機能簡単本当に設計および SPAs を構築します。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-114">However, emerging technologies like ASP.NET Web API, JavaScript frameworks like AngularJS and new styling features provided by CSS3 make it really easy to design and build SPAs.</span></span>
> 
> <span data-ttu-id="6fbeb-115">この手の形でラボでは、マニア クイズ、SPA 概念に基づいてトリビア web サイトを実装するこれらのテクノロジの利点がかかります。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-115">In this hand-on lab, you will take advantage of those technologies to implement Geek Quiz, a trivia website based on the SPA concept.</span></span> <span data-ttu-id="6fbeb-116">まず、質問を取得し、回答を保存するに必要なエンドポイントを公開する ASP.NET Web API とサービス層を実装します。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-116">You will first implement the service layer with ASP.NET Web API to expose the required endpoints to retrieve the quiz questions and store the answers.</span></span> <span data-ttu-id="6fbeb-117">次に、AngularJS および css3 用の変換の効果を使用してや応答性の機能豊富な UI をビルドします。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-117">Then, you will build a rich and responsive UI using AngularJS and CSS3 transformation effects.</span></span>
> 
> <span data-ttu-id="6fbeb-118">すべてのサンプル コードとスニペットがで使用可能な Web キャンプ トレーニング キットに含まれている[http://aka.ms/webcamps-training-kit](http://aka.ms/webcamps-training-kit)です。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-118">All sample code and snippets are included in the Web Camps Training Kit, available at [http://aka.ms/webcamps-training-kit](http://aka.ms/webcamps-training-kit).</span></span>


## <a name="overview"></a><span data-ttu-id="6fbeb-119">概要</span><span class="sxs-lookup"><span data-stu-id="6fbeb-119">Overview</span></span>

<a id="Objectives"></a>
### <a name="objectives"></a><span data-ttu-id="6fbeb-120">目的</span><span class="sxs-lookup"><span data-stu-id="6fbeb-120">Objectives</span></span>

<span data-ttu-id="6fbeb-121">このハンズオン ラボでは学習する方法。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-121">In this hands-on lab, you will learn how to:</span></span>

- <span data-ttu-id="6fbeb-122">JSON データを送受信する ASP.NET Web API サービスを作成します。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-122">Create an ASP.NET Web API service to send and receive JSON data</span></span>
- <span data-ttu-id="6fbeb-123">AngularJS を使用して、応答性の高い UI を作成します。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-123">Create a responsive UI using AngularJS</span></span>
- <span data-ttu-id="6fbeb-124">CSS3 変換で UI エクスペリエンスを向上します。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-124">Enhance the UI experience with CSS3 transformations</span></span>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="6fbeb-125">必須コンポーネント</span><span class="sxs-lookup"><span data-stu-id="6fbeb-125">Prerequisites</span></span>

<span data-ttu-id="6fbeb-126">このハンズオン ラボを完了する、次が必要。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-126">The following is required to complete this hands-on lab:</span></span>

- <span data-ttu-id="6fbeb-127">[Visual Studio Express 2013 for Web](https://www.microsoft.com/visualstudio/)以上</span><span class="sxs-lookup"><span data-stu-id="6fbeb-127">[Visual Studio Express 2013 for Web](https://www.microsoft.com/visualstudio/) or greater</span></span>

<a id="Setup"></a>
### <a name="setup"></a><span data-ttu-id="6fbeb-128">セットアップ</span><span class="sxs-lookup"><span data-stu-id="6fbeb-128">Setup</span></span>

<span data-ttu-id="6fbeb-129">このハンズオン ラボでは、演習を実行するのには、最初に、環境を設定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-129">In order to run the exercises in this hands-on lab, you will need to set up your environment first.</span></span>

1. <span data-ttu-id="6fbeb-130">開いている Windows エクスプ ローラーおよびテスト環境の参照**ソース**フォルダーです。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-130">Open Windows Explorer and browse to the lab's **Source** folder.</span></span>
2. <span data-ttu-id="6fbeb-131">右クリックして**Setup.cmd**選択と**管理者として実行**を環境を構成して、このラボ用の Visual Studio のコード スニペットをインストールするセットアップ プロセスを起動します。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-131">Right-click on **Setup.cmd** and select **Run as administrator** to launch the setup process that will configure your environment and install the Visual Studio code snippets for this lab.</span></span>
3. <span data-ttu-id="6fbeb-132">ユーザー アカウント制御 ダイアログ ボックスが表示されている場合は、続行するアクションを確認します。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-132">If the User Account Control dialog box is shown, confirm the action to proceed.</span></span>

> [!NOTE]
> <span data-ttu-id="6fbeb-133">セットアップを実行する前に、このラボのすべての依存関係をチェックしたことを確認してください。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-133">Make sure you have checked all the dependencies for this lab before running the setup.</span></span>


<a id="CodeSnippets"></a>
### <a name="using-the-code-snippets"></a><span data-ttu-id="6fbeb-134">コード スニペットを使用します。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-134">Using the Code Snippets</span></span>

<span data-ttu-id="6fbeb-135">ラボ ドキュメント全体にわたって、コード ブロックを挿入するように指示されます。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-135">Throughout the lab document, you will be instructed to insert code blocks.</span></span> <span data-ttu-id="6fbeb-136">便宜上、このコードのほとんどは、Visual Studio コード スニペットを手動で追加することを回避する Visual Studio 2013 内からアクセスできるとして提供されます。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-136">For your convenience, most of this code is provided as Visual Studio Code Snippets, which you can access from within Visual Studio 2013 to avoid having to add it manually.</span></span>

> [!NOTE]
> <span data-ttu-id="6fbeb-137">各演習にある開始ソリューションが組み込まれた、**開始**個別に各手順をたどることによってこの作業のフォルダーです。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-137">Each exercise is accompanied by a starting solution located in the **Begin** folder of the exercise that allows you to follow each exercise independently of the others.</span></span> <span data-ttu-id="6fbeb-138">実習では、追加のコード スニペットがこれらのソリューションの開始から不足しており、演習を完了するまで動作しない可能性がありますに注意してください。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-138">Please be aware that the code snippets that are added during an exercise are missing from these starting solutions and may not work until you have completed the exercise.</span></span> <span data-ttu-id="6fbeb-139">演習では、ソース コード、内部も表示されます、**終了**を対応する手順の手順を実行した結果のコードの Visual Studio ソリューションを含むフォルダー。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-139">Inside the source code for an exercise, you will also find an **End** folder containing a Visual Studio solution with the code that results from completing the steps in the corresponding exercise.</span></span> <span data-ttu-id="6fbeb-140">このハンズオン ラボを使用すると、追加のヘルプを必要がある場合は、これらのソリューションをガイドとして使用できます。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-140">You can use these solutions as guidance if you need additional help as you work through this hands-on lab.</span></span>


* * *

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="6fbeb-141">演習</span><span class="sxs-lookup"><span data-stu-id="6fbeb-141">Exercises</span></span>

<span data-ttu-id="6fbeb-142">このハンズオン ラボには、次の実習が含まれます。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-142">This hands-on lab includes the following exercises:</span></span>

1. [<span data-ttu-id="6fbeb-143">Web API を作成します。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-143">Creating a Web API</span></span>](#Exercise1)
2. [<span data-ttu-id="6fbeb-144">SPA インターフェイスを作成します。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-144">Creating a SPA Interface</span></span>](#Exercise2)

<span data-ttu-id="6fbeb-145">この演習を完了する時間を推定: **60 分**</span><span class="sxs-lookup"><span data-stu-id="6fbeb-145">Estimated time to complete this lab: **60 minutes**</span></span>

> [!NOTE]
> <span data-ttu-id="6fbeb-146">Visual Studio を初めて起動するときに定義済みの設定のコレクションの 1 つを選択する必要があります。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-146">When you first start Visual Studio, you must select one of the predefined settings collections.</span></span> <span data-ttu-id="6fbeb-147">定義済みの各コレクションは、特定の開発スタイルと一致するものではまた、ウィンドウのレイアウト、エディターの動作、IntelliSense コード スニペットでは、およびダイアログ ボックスのオプションを判断します。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-147">Each predefined collection is designed to match a particular development style and determines window layouts, editor behavior, IntelliSense code snippets, and dialog box options.</span></span> <span data-ttu-id="6fbeb-148">このラボの手順を使用する場合は、Visual Studio での特定のタスクを実行に必要な操作を記述する、**全般的な開発設定**コレクション。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-148">The procedures in this lab describe the actions necessary to accomplish a given task in Visual Studio when using the **General Development Settings** collection.</span></span> <span data-ttu-id="6fbeb-149">開発環境に合わせてさまざまな設定のコレクションを選択する場合、考慮する必要がある手順に違いがあります。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-149">If you choose a different settings collection for your development environment, there may be differences in the steps that you should take into account.</span></span>


<a id="Exercise1"></a>
### <a name="exercise-1-creating-a-web-api"></a><span data-ttu-id="6fbeb-150">手順 1: Web API を作成します。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-150">Exercise 1: Creating a Web API</span></span>

<span data-ttu-id="6fbeb-151">サービス層は、SPA の主要部分のいずれかです。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-151">One of the key parts of a SPA is the service layer.</span></span> <span data-ttu-id="6fbeb-152">UI とその呼び出しに対する応答で返されるデータによって送信される Ajax 呼び出しの処理を行います。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-152">It is responsible for processing the Ajax calls sent by the UI and returning data in response to that call.</span></span> <span data-ttu-id="6fbeb-153">解析され、クライアントで利用するためにコンピューターが判読できる形式で取得されたデータを表示する必要があります。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-153">The data retrieved should be presented in a machine-readable format in order to be parsed and consumed by the client.</span></span>

<span data-ttu-id="6fbeb-154">Web API フレームワークでは、ASP.NET スタックの一部であるし、HTTP サービス、通常、RESTful API を通じて JSON または XML 形式のデータの送受信を実装するが簡単にいます。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-154">The Web API framework is part of the ASP.NET Stack and is designed to make it easy to implement HTTP services, generally sending and receiving JSON- or XML-formatted data through a RESTful API.</span></span> <span data-ttu-id="6fbeb-155">この演習では、マニア クイズ アプリケーションをホストし、バックエンド サービスを公開して、クイズを ASP.NET Web API を使用してデータを永続化を実装するには、Web サイトを作成します。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-155">In this exercise you will create the Web site to host the Geek Quiz application and then implement the back-end service to expose and persist the quiz data using ASP.NET Web API.</span></span>

<a id="Ex1Task1"></a>
#### <a name="task-1--creating-the-initial-project-for-geek-quiz"></a><span data-ttu-id="6fbeb-156">作業 1: マニア クイズの初期のプロジェクトを作成します。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-156">Task 1 – Creating the Initial Project for Geek Quiz</span></span>

<span data-ttu-id="6fbeb-157">このタスクでは作成を開始する新しい ASP.NET MVC プロジェクトのサポートの ASP.NET Web API に基づいて、 **1 つの ASP.NET** Visual Studio に付属している型を射影します。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-157">In this task you will start creating a new ASP.NET MVC project with support for ASP.NET Web API based on the **One ASP.NET** project type that comes with Visual Studio.</span></span> <span data-ttu-id="6fbeb-158">**1 つの ASP.NET**にすべての ASP.NET テクノロジをまとめを混在させるし、必要に応じて、それらが一致するオプションを選択できます。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-158">**One ASP.NET** unifies all ASP.NET technologies and gives you the option to mix and match them as desired.</span></span> <span data-ttu-id="6fbeb-159">Entity Framework のモデルのクラスとクイズの質問を挿入するデータベース initializator を追加します。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-159">You will then add the Entity Framework's model classes and the database initializator to insert the quiz questions.</span></span>

1. <span data-ttu-id="6fbeb-160">開いている**Visual Studio Express 2013 for Web**選択**ファイル |新しいプロジェクト.**を新しいソリューションを開始します。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-160">Open **Visual Studio Express 2013 for Web** and select **File | New Project...** to start a new solution.</span></span>

    <span data-ttu-id="6fbeb-161">![新しいプロジェクトを作成する](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image1.png "新規プロジェクトの作成")</span><span class="sxs-lookup"><span data-stu-id="6fbeb-161">![Creating a New Project](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image1.png "Creating a New Project")</span></span>

    <span data-ttu-id="6fbeb-162">*新しいプロジェクトを作成します。*</span><span class="sxs-lookup"><span data-stu-id="6fbeb-162">*Creating a New Project*</span></span>
2. <span data-ttu-id="6fbeb-163">**新しいプロジェクト**ダイアログ ボックスで、 **ASP.NET Web アプリケーション**下にある、 **Visual c# |Web**タブです。確認してください**.NET Framework 4.5**がという名前を選択すると、 *GeekQuiz*を選択、**場所** をクリック**OK**です。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-163">In the **New Project** dialog box, select **ASP.NET Web Application** under the **Visual C# | Web** tab. Make sure **.NET Framework 4.5** is selected, name it *GeekQuiz*, choose a **Location** and click **OK**.</span></span>

    <span data-ttu-id="6fbeb-164">![新しい ASP.NET Web アプリケーション プロジェクトを作成する](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image2.png "新しい ASP.NET Web アプリケーション プロジェクトを作成します。")</span><span class="sxs-lookup"><span data-stu-id="6fbeb-164">![Creating a new ASP.NET Web Application project](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image2.png "Creating a new ASP.NET Web Application project")</span></span>

    <span data-ttu-id="6fbeb-165">*新しい ASP.NET Web アプリケーション プロジェクトを作成します。*</span><span class="sxs-lookup"><span data-stu-id="6fbeb-165">*Creating a new ASP.NET Web Application project*</span></span>
3. <span data-ttu-id="6fbeb-166">**新しい ASP.NET プロジェクト**ダイアログ ボックスで、 **MVC**テンプレートを選択、 **Web API**オプション。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-166">In the **New ASP.NET Project** dialog box, select the **MVC** template and select the **Web API** option.</span></span> <span data-ttu-id="6fbeb-167">また、ことを確認、**認証**にオプションが設定されている**個々 のユーザー アカウント**です。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-167">Also, make sure that the **Authentication** option is set to **Individual User Accounts**.</span></span> <span data-ttu-id="6fbeb-168">**[OK]** をクリックして続行します。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-168">Click **OK** to continue.</span></span>

    ![Web API のコンポーネントを含め、MVC テンプレートに新しいプロジェクトの作成](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image3.png)

    <span data-ttu-id="6fbeb-170">*Web API のコンポーネントを含め、MVC テンプレートに新しいプロジェクトの作成*</span><span class="sxs-lookup"><span data-stu-id="6fbeb-170">*Creating a new project with the MVC template, including Web API components*</span></span>
4. <span data-ttu-id="6fbeb-171">**ソリューション エクスプ ローラー**を右クリックし、**モデル**のフォルダー、 **GeekQuiz**プロジェクトし、選択**追加 |既存アイテム.**.</span><span class="sxs-lookup"><span data-stu-id="6fbeb-171">In **Solution Explorer**, right-click the **Models** folder of the **GeekQuiz** project and select **Add | Existing Item...**.</span></span>

    <span data-ttu-id="6fbeb-172">![既存の項目を追加する](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image4.png "既存の項目を追加します。")</span><span class="sxs-lookup"><span data-stu-id="6fbeb-172">![Adding an existing item](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image4.png "Adding an existing item")</span></span>

    <span data-ttu-id="6fbeb-173">*既存の項目を追加します。*</span><span class="sxs-lookup"><span data-stu-id="6fbeb-173">*Adding an existing item*</span></span>
5. <span data-ttu-id="6fbeb-174">**既存項目の追加** ダイアログ ボックスに移動、**ソース/資産/モデル**フォルダーとすべてのファイルを選択します。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-174">In the **Add Existing Item** dialog box, navigate to the **Source/Assets/Models** folder and select all the files.</span></span> <span data-ttu-id="6fbeb-175">**[追加]**をクリックします。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-175">Click **Add**.</span></span>

    <span data-ttu-id="6fbeb-176">![モデルのアセットの追加](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image5.png "モデル アセットの追加")</span><span class="sxs-lookup"><span data-stu-id="6fbeb-176">![Adding the model assets](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image5.png "Adding the model assets")</span></span>

    <span data-ttu-id="6fbeb-177">*モデルのアセットの追加*</span><span class="sxs-lookup"><span data-stu-id="6fbeb-177">*Adding the model assets*</span></span>

    > [!NOTE]
    > <span data-ttu-id="6fbeb-178">これらのファイルを追加すると、データ モデル、エンティティ フレームワークのデータベースのコンテキストとマニア Quiz アプリケーションのデータベース初期化子を追加します。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-178">By adding these files, you are adding the data model, the Entity Framework's database context and the database initializer for the Geek Quiz application.</span></span>
    > 
    > <span data-ttu-id="6fbeb-179">**Entity Framework (EF)**は、オブジェクト リレーショナル マッパー (ORM) 直接リレーショナル ストレージ スキーマを使用したプログラミングではなく、概念アプリケーション モデルを使用したプログラミング、データ アクセス アプリケーションを作成することができます。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-179">**Entity Framework (EF)** is an object-relational mapper (ORM) that enables you to create data access applications by programming with a conceptual application model instead of programming directly using a relational storage schema.</span></span> <span data-ttu-id="6fbeb-180">Entity Framework に関する詳細については、[ここ](../../../entity-framework.md)です。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-180">You can learn more about Entity Framework [here](../../../entity-framework.md).</span></span>
    > 
    > <span data-ttu-id="6fbeb-181">追加したばかりのクラスの説明を次に示します。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-181">The following is a description of the classes you just added:</span></span>
    > 
    > - <span data-ttu-id="6fbeb-182">**TriviaOption:**クイズの質問に関連付けられている 1 つのオプションを表します</span><span class="sxs-lookup"><span data-stu-id="6fbeb-182">**TriviaOption:** represents a single option associated with a quiz question</span></span>
    > - <span data-ttu-id="6fbeb-183">**TriviaQuestion:**クイズの質問を表し、を通じて関連付けられているオプションを公開して、**オプション**プロパティ</span><span class="sxs-lookup"><span data-stu-id="6fbeb-183">**TriviaQuestion:** represents a quiz question and exposes the associated options through the **Options** property</span></span>
    > - <span data-ttu-id="6fbeb-184">**TriviaAnswer:**クイズの質問への応答でユーザーが選択されているオプションを表します</span><span class="sxs-lookup"><span data-stu-id="6fbeb-184">**TriviaAnswer:** represents the option selected by the user in response to a quiz question</span></span>
    > - <span data-ttu-id="6fbeb-185">**TriviaContext:**マニア Quiz アプリケーションの Entity Framework のデータベース コンテキストを表します。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-185">**TriviaContext:** represents the Entity Framework's database context of the Geek Quiz application.</span></span> <span data-ttu-id="6fbeb-186">このクラスから派生**DContext**と公開**DbSet**を上記で説明したエンティティのコレクションを表すプロパティ。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-186">This class derives from **DContext** and exposes **DbSet** properties that represent collections of the entities described above.</span></span>
    > - <span data-ttu-id="6fbeb-187">**TriviaDatabaseInitializer:** Entity Framework の初期化子の実装、 **TriviaContext**クラスから継承される**CreateDatabaseIfNotExists**です。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-187">**TriviaDatabaseInitializer:** the implementation of the Entity Framework initializer for the **TriviaContext** class which inherits from **CreateDatabaseIfNotExists**.</span></span> <span data-ttu-id="6fbeb-188">指定されたエンティティを挿入するこのクラスの既定の動作は、存在しない場合にのみ、データベースを作成するのには、**シード**メソッドです。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-188">The default behavior of this class is to create the database only if it does not exist, inserting the entities specified in the **Seed** method.</span></span>
6. <span data-ttu-id="6fbeb-189">開く、 **Global.asax.cs**ファイルし、次を追加するステートメントを使用します。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-189">Open the **Global.asax.cs** file and add the following using statement.</span></span>

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample1.cs)]
7. <span data-ttu-id="6fbeb-190">先頭に次のコードを追加、**アプリケーション\_開始**を設定するメソッド、 **TriviaDatabaseInitializer**データベース初期化子として。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-190">Add the following code at the beginning of the **Application\_Start** method to set the **TriviaDatabaseInitializer** as the database initializer.</span></span>

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample2.cs)]
8. <span data-ttu-id="6fbeb-191">変更、**ホーム**へのアクセスを制限するコント ローラーがユーザーを認証します。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-191">Modify the **Home** controller to restrict access to authenticated users.</span></span> <span data-ttu-id="6fbeb-192">これを行うには、開く、 **HomeController.cs**内のファイル、**コント ローラー**フォルダーを追加し、 **Authorize**属性を**HomeController**クラス定義です。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-192">To do this, open the **HomeController.cs** file inside the **Controllers** folder and add the **Authorize** attribute to the **HomeController** class definition.</span></span>

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample3.cs)]

    > [!NOTE]
    > <span data-ttu-id="6fbeb-193">**Authorize**フィルター処理、ユーザーが認証されるかどうかかどうかを確認します。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-193">The **Authorize** filter checks to see if the user is authenticated.</span></span> <span data-ttu-id="6fbeb-194">ユーザーが認証されていない場合は、アクションを呼び出すことがなく HTTP ステータス コード 401 (Unauthorized) を返します。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-194">If the user is not authenticated, it returns HTTP status code 401 (Unauthorized) without invoking the action.</span></span> <span data-ttu-id="6fbeb-195">コント ローラー レベル、または個々 のアクション レベルでグローバルに、フィルターを適用することができます。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-195">You can apply the filter globally, at the controller level, or at the level of individual actions.</span></span>
9. <span data-ttu-id="6fbeb-196">これで、web ページと、ブランド化のレイアウトをカスタマイズします。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-196">You will now customize the layout of the web pages and the branding.</span></span> <span data-ttu-id="6fbeb-197">これを行うには、開く、  **\_Layout.cshtml**内のファイル、**ビュー |共有**フォルダーの内容を更新し、 **&lt;タイトル&gt;**に置き換えることで要素*マイ ASP.NET アプリケーション*で*マニア クイズ*.</span><span class="sxs-lookup"><span data-stu-id="6fbeb-197">To do this, open the **\_Layout.cshtml** file inside the **Views | Shared** folder and update the content of the **&lt;title&gt;** element by replacing *My ASP.NET Application* with *Geek Quiz*.</span></span>

    [!code-cshtml[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample4.cshtml)]
10. <span data-ttu-id="6fbeb-198">同じファイル内には、削除することで、ナビゲーション バーを更新、*に関する*と*連絡先*リンクと名前を変更する、*ホーム*へのリンク*再生*です。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-198">In the same file, update the navigation bar by removing the *About* and *Contact* links and renaming the *Home* link to *Play*.</span></span> <span data-ttu-id="6fbeb-199">さらに、名前の変更、*アプリケーション名*へのリンク*マニア Quiz*です。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-199">Additionally, rename the *Application name* link to *Geek Quiz*.</span></span> <span data-ttu-id="6fbeb-200">ナビゲーション バーの HTML は、次のコードのようになります。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-200">The HTML for the navigation bar should look like the following code.</span></span>

    [!code-cshtml[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample5.cshtml)]
11. <span data-ttu-id="6fbeb-201">レイアウト ページのフッターを置き換えることで更新*マイ ASP.NET アプリケーション*で*マニア Quiz*です。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-201">Update the footer of the layout page by replacing *My ASP.NET Application* with *Geek Quiz*.</span></span> <span data-ttu-id="6fbeb-202">これを行うには、コンテンツを置き換え、 **&lt;フッター&gt;** 要素を次の強調表示されたコード。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-202">To do this, replace the content of the **&lt;footer&gt;** element with the following highlighted code.</span></span>

    [!code-html[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample6.html)]

<a id="Ex1Task2"></a>
#### <a name="task-2--creating-the-triviacontroller-web-api"></a><span data-ttu-id="6fbeb-203">タスク 2: TriviaController Web API を作成します。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-203">Task 2 – Creating the TriviaController Web API</span></span>

<span data-ttu-id="6fbeb-204">前のタスクでは、マニア クイズの web アプリケーションの初期の構造を作成します。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-204">In the previous task, you created the initial structure of the Geek Quiz web application.</span></span> <span data-ttu-id="6fbeb-205">クイズ データ モデルと対話し、次の操作を公開する単純な Web API サービスが作成されます。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-205">You will now build a simple Web API service that interacts with the quiz data model and exposes the following actions:</span></span>

- <span data-ttu-id="6fbeb-206">**GET api/トリビア**: 認証済みユーザーが回答するクイズ リストから次の質問を取得します。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-206">**GET /api/trivia**: Retrieves the next question from the quiz list to be answered by the authenticated user.</span></span>
- <span data-ttu-id="6fbeb-207">**POST api/トリビア**: 認証されたユーザーを指定してクイズの答えを格納します。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-207">**POST /api/trivia**: Stores the quiz answer specified by the authenticated user.</span></span>

<span data-ttu-id="6fbeb-208">Visual Studio によって提供される ASP.NET スキャフォールディング ツールを使用する Web API コント ローラー クラスの基準を作成します。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-208">You will use the ASP.NET Scaffolding tools provided by Visual Studio to create the baseline for the Web API controller class.</span></span>

1. <span data-ttu-id="6fbeb-209">開く、 **WebApiConfig.cs**内のファイル、**アプリ\_開始**フォルダーです。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-209">Open the **WebApiConfig.cs** file inside the **App\_Start** folder.</span></span> <span data-ttu-id="6fbeb-210">このファイルは、Web API コント ローラーのアクションをルートをマップする方法と同様に、Web API サービスの構成を定義します。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-210">This file defines the configuration of the Web API service, like how routes are mapped to Web API controller actions.</span></span>
2. <span data-ttu-id="6fbeb-211">次の追加、ファイルの先頭にステートメントを使用します。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-211">Add the following using statement at the beginning of the file.</span></span>

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample7.cs)]
3. <span data-ttu-id="6fbeb-212">次の強調表示されたコードを追加、**登録**Web API のアクション メソッドによって取得された JSON データのフォーマッタをグローバルに構成する方法です。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-212">Add the following highlighted code to the **Register** method to globally configure the formatter for the JSON data retrieved by the Web API action methods.</span></span>

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample8.cs)]

    > [!NOTE]
    > <span data-ttu-id="6fbeb-213">**CamelCasePropertyNamesContractResolver**にプロパティ名を自動的に変換*camel 形式*場合は、JavaScript のプロパティ名の一般的な規則です。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-213">The **CamelCasePropertyNamesContractResolver** automatically converts property names to *camel* case, which is the general convention for property names in JavaScript.</span></span>
4. <span data-ttu-id="6fbeb-214">**ソリューション エクスプ ローラー**を右クリックし、**コント ローラー**のフォルダー、 **GeekQuiz**プロジェクトし、選択**追加 |新しい項目のスキャフォールディングしています.**.</span><span class="sxs-lookup"><span data-stu-id="6fbeb-214">In **Solution Explorer**, right-click the **Controllers** folder of the **GeekQuiz** project and select **Add | New Scaffolded Item...**.</span></span>

    <span data-ttu-id="6fbeb-215">![スキャフォールディングされた新しい項目を作成する](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image6.png "新しいスキャフォールディングされた項目を作成します。")</span><span class="sxs-lookup"><span data-stu-id="6fbeb-215">![Creating a new scaffolded item](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image6.png "Creating a new scaffolded item")</span></span>

    <span data-ttu-id="6fbeb-216">*スキャフォールディングされた新しい項目を作成します。*</span><span class="sxs-lookup"><span data-stu-id="6fbeb-216">*Creating a new scaffolded item*</span></span>
5. <span data-ttu-id="6fbeb-217">**追加 Scaffold**  ダイアログ ボックスで、ことを確認して、**共通**左側のウィンドウでノードを選択します。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-217">In the **Add Scaffold** dialog box, make sure that the **Common** node is selected in the left pane.</span></span> <span data-ttu-id="6fbeb-218">次に、選択、 **Web API 2 コント ローラー - 空**中央のペインにテンプレート**追加**です。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-218">Then, select the **Web API 2 Controller - Empty** template in the center pane and click **Add**.</span></span>

    <span data-ttu-id="6fbeb-219">![Web API 2 コント ローラー空のテンプレートを選択する](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image7.png "Web API 2 コント ローラー空のテンプレートを選択します。")</span><span class="sxs-lookup"><span data-stu-id="6fbeb-219">![Selecting the Web API 2 Controller Empty template](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image7.png "Selecting the Web API 2 Controller Empty template")</span></span>

    <span data-ttu-id="6fbeb-220">*Web API 2 コント ローラー空のテンプレートを選択します。*</span><span class="sxs-lookup"><span data-stu-id="6fbeb-220">*Selecting the Web API 2 Controller Empty template*</span></span>

    > [!NOTE]
    > <span data-ttu-id="6fbeb-221">**ASP.NET スキャフォールディング**は、ASP.NET Web アプリケーションのコード生成のフレームワークです。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-221">**ASP.NET Scaffolding** is a code generation framework for ASP.NET Web applications.</span></span> <span data-ttu-id="6fbeb-222">Visual Studio 2013 には、MVC、Web API プロジェクトに対して事前インストールされているコード ジェネレーターが含まれています。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-222">Visual Studio 2013 includes pre-installed code generators for MVC and Web API projects.</span></span> <span data-ttu-id="6fbeb-223">標準的なデータ操作を開発するために必要な時間の量を削減するためにデータ モデルと対話するコードを簡単に追加するときに、プロジェクトのスキャフォールディングを使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-223">You should use scaffolding in your project when you want to quickly add code that interacts with data models in order to reduce the amount of time required to develop standard data operations.</span></span>
    > 
    > <span data-ttu-id="6fbeb-224">スキャフォールディング プロセスは、プロジェクトに必要なすべての依存関係がインストールされているできるようになります。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-224">The scaffolding process also ensures that all the required dependencies are installed in the project.</span></span> <span data-ttu-id="6fbeb-225">たとえば、空の ASP.NET プロジェクトを開始して、スキャフォールディングを使用して Web API コント ローラーを追加した場合、必要な Web API NuGet パッケージと参照をプロジェクトに自動的に追加されます。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-225">For example, if you start with an empty ASP.NET project and then use scaffolding to add a Web API controller, the required Web API NuGet packages and references are added to your project automatically.</span></span>
6. <span data-ttu-id="6fbeb-226">**コント ローラーの追加** ダイアログ ボックスで、「 *TriviaController*で、**コント ローラー名**テキスト ボックスをクリック**追加**です。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-226">In the **Add Controller** dialog box, type *TriviaController* in the **Controller name** text box and click **Add**.</span></span>

    <span data-ttu-id="6fbeb-227">![トリビア コント ローラーを追加する](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image8.png "トリビア コント ローラーを追加します。")</span><span class="sxs-lookup"><span data-stu-id="6fbeb-227">![Adding the Trivia Controller](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image8.png "Adding the Trivia Controller")</span></span>

    <span data-ttu-id="6fbeb-228">*トリビア コント ローラーを追加します。*</span><span class="sxs-lookup"><span data-stu-id="6fbeb-228">*Adding the Trivia Controller*</span></span>
7. <span data-ttu-id="6fbeb-229">**TriviaController.cs**にファイルが追加し、**コント ローラー**のフォルダー、 **GeekQuiz** 、空を含むプロジェクトは、 **TriviaController**クラスです。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-229">The **TriviaController.cs** file is then added to the **Controllers** folder of the **GeekQuiz** project, containing an empty **TriviaController** class.</span></span> <span data-ttu-id="6fbeb-230">次の追加、ファイルの先頭にステートメントを使用します。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-230">Add the following using statements at the beginning of the file.</span></span>

    <span data-ttu-id="6fbeb-231">(コード スニペットの*AspNetWebApiSpa - Ex1 - TriviaControllerUsings*)</span><span class="sxs-lookup"><span data-stu-id="6fbeb-231">(Code Snippet - *AspNetWebApiSpa - Ex1 - TriviaControllerUsings*)</span></span>

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample9.cs)]
8. <span data-ttu-id="6fbeb-232">先頭に次のコードを追加、 **TriviaController**クラスを定義、初期化および破棄、 **TriviaContext**コント ローラーのインスタンス。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-232">Add the following code at the beginning of the **TriviaController** class to define, initialize and dispose the **TriviaContext** instance in the controller.</span></span>

    <span data-ttu-id="6fbeb-233">(コード スニペットの*AspNetWebApiSpa - Ex1 - TriviaControllerContext*)</span><span class="sxs-lookup"><span data-stu-id="6fbeb-233">(Code Snippet - *AspNetWebApiSpa - Ex1 - TriviaControllerContext*)</span></span>

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample10.cs)]

    > [!NOTE]
    > <span data-ttu-id="6fbeb-234">**Dispose**メソッドの**TriviaController**呼び出します、 **Dispose**のメソッド、 **TriviaContext**インスタンスで、確実にすべてコンテキスト オブジェクトで使用されているリソースがリリースされたときに、 **TriviaContext**インスタンスを破棄またはガベージ コレクションします。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-234">The **Dispose** method of **TriviaController** invokes the **Dispose** method of the **TriviaContext** instance, which ensures that all the resources used by the context object are released when the **TriviaContext** instance is disposed or garbage-collected.</span></span> <span data-ttu-id="6fbeb-235">これには、Entity Framework によって開かれたすべてのデータベース接続の終了が含まれます。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-235">This includes closing all database connections opened by Entity Framework.</span></span>
9. <span data-ttu-id="6fbeb-236">末尾に次のヘルパー メソッドを追加、 **TriviaController**クラスです。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-236">Add the following helper method at the end of the **TriviaController** class.</span></span> <span data-ttu-id="6fbeb-237">このメソッドは、応答するように、指定したユーザー データベースからクイズの次の質問を取得します。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-237">This method retrieves the following quiz question from the database to be answered by the specified user.</span></span>

    <span data-ttu-id="6fbeb-238">(コード スニペットの*AspNetWebApiSpa - Ex1 - TriviaControllerNextQuestion*)</span><span class="sxs-lookup"><span data-stu-id="6fbeb-238">(Code Snippet - *AspNetWebApiSpa - Ex1 - TriviaControllerNextQuestion*)</span></span>

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample11.cs)]
10. <span data-ttu-id="6fbeb-239">次の追加**取得**アクション メソッド、 **TriviaController**クラスです。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-239">Add the following **Get** action method to the **TriviaController** class.</span></span> <span data-ttu-id="6fbeb-240">このアクション メソッドを呼び出す、 **NextQuestionAsync**認証されたユーザーの次の質問を取得する前の手順で定義されているヘルパー メソッドです。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-240">This action method calls the **NextQuestionAsync** helper method defined in the previous step to retrieve the next question for the authenticated user.</span></span>

    <span data-ttu-id="6fbeb-241">(コード スニペットの*AspNetWebApiSpa - Ex1 - TriviaControllerGetAction*)</span><span class="sxs-lookup"><span data-stu-id="6fbeb-241">(Code Snippet - *AspNetWebApiSpa - Ex1 - TriviaControllerGetAction*)</span></span>

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample12.cs)]
11. <span data-ttu-id="6fbeb-242">末尾に次のヘルパー メソッドを追加、 **TriviaController**クラスです。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-242">Add the following helper method at the end of the **TriviaController** class.</span></span> <span data-ttu-id="6fbeb-243">このメソッドは、データベースに指定された応答を格納し、答えが正しいかどうかを示すブール値を返します。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-243">This method stores the specified answer in the database and returns a Boolean value indicating whether or not the answer is correct.</span></span>

    <span data-ttu-id="6fbeb-244">(コード スニペットの*AspNetWebApiSpa - Ex1 - TriviaControllerStoreAsync*)</span><span class="sxs-lookup"><span data-stu-id="6fbeb-244">(Code Snippet - *AspNetWebApiSpa - Ex1 - TriviaControllerStoreAsync*)</span></span>

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample13.cs)]
12. <span data-ttu-id="6fbeb-245">次の追加**Post**アクション メソッド、 **TriviaController**クラスです。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-245">Add the following **Post** action method to the **TriviaController** class.</span></span> <span data-ttu-id="6fbeb-246">このアクション メソッドが、認証されたユーザーとの呼び出しに応答を関連付ける、 **StoreAsync**ヘルパー メソッドです。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-246">This action method associates the answer to the authenticated user and calls the **StoreAsync** helper method.</span></span> <span data-ttu-id="6fbeb-247">その後、ヘルパー メソッドによって返されるブール値を持つ応答を送信します。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-247">Then, it sends a response with the Boolean value returned by the helper method.</span></span>

    <span data-ttu-id="6fbeb-248">(コード スニペットの*AspNetWebApiSpa - Ex1 - TriviaControllerPostAction*)</span><span class="sxs-lookup"><span data-stu-id="6fbeb-248">(Code Snippet - *AspNetWebApiSpa - Ex1 - TriviaControllerPostAction*)</span></span>

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample14.cs)]
13. <span data-ttu-id="6fbeb-249">追加することで認証されたユーザーへのアクセスを制限する Web API コント ローラーの変更、 **Authorize**属性を**TriviaController**クラス定義です。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-249">Modify the Web API controller to restrict access to authenticated users by adding the **Authorize** attribute to the **TriviaController** class definition.</span></span>

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample15.cs)]

<a id="Ex1Task3"></a>
#### <a name="task-3--running-the-solution"></a><span data-ttu-id="6fbeb-250">タスク 3: ソリューションの実行</span><span class="sxs-lookup"><span data-stu-id="6fbeb-250">Task 3 – Running the Solution</span></span>

<span data-ttu-id="6fbeb-251">このタスクでは、前のタスクでビルドした Web API サービスが正しく動作することを確認します。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-251">In this task you will verify that the Web API service you built in the previous task is working as expected.</span></span> <span data-ttu-id="6fbeb-252">Internet Explorer を使用する、 **F12 開発者ツール**ネットワーク トラフィックをキャプチャし、Web API サービスから応答の全体を検査します。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-252">You will use the Internet Explorer **F12 Developer Tools** to capture the network traffic and inspect the full response from the Web API service.</span></span>

> [!NOTE]
> <span data-ttu-id="6fbeb-253">確認して**Internet Explorer**でが選択されている、**開始**Visual Studio ツールバー上にあるボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-253">Make sure that **Internet Explorer** is selected in the **Start** button located on the Visual Studio toolbar.</span></span>
> 
> ![Internet Explorer オプション](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image9.png)


1. <span data-ttu-id="6fbeb-255">キーを押して**f5 キーを押して**ソリューションを実行します。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-255">Press **F5** to run the solution.</span></span> <span data-ttu-id="6fbeb-256">**ログイン**ページがブラウザーに表示する必要があります。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-256">The **Log in** page should appear in the browser.</span></span>

    > [!NOTE]
    > <span data-ttu-id="6fbeb-257">アプリケーションの起動時に既定の MVC ルートがトリガーされる、既定でにマップされて、**インデックス**のアクション、 **HomeController**クラスです。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-257">When the application starts, the default MVC route is triggered, which by default is mapped to the **Index** action of the **HomeController** class.</span></span> <span data-ttu-id="6fbeb-258">**HomeController**認証されたユーザーに制限されます (そのクラスを装飾することに注意してください、 **Authorize**演習 1 の属性) し、ユーザーが認証されていない、まだアプリケーションがあります。元の要求をログイン ページにリダイレクトします。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-258">Since **HomeController** is restricted to authenticated users (remember that you decorated that class with the **Authorize** attribute in Exercise 1) and there is no user authenticated yet, the application redirects the original request to the log in page.</span></span>

    <span data-ttu-id="6fbeb-259">![ソリューションを実行している](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image10.png "ソリューションの実行")</span><span class="sxs-lookup"><span data-stu-id="6fbeb-259">![Running the solution](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image10.png "Running the solution")</span></span>

    <span data-ttu-id="6fbeb-260">*ソリューションの実行*</span><span class="sxs-lookup"><span data-stu-id="6fbeb-260">*Running the solution*</span></span>
2. <span data-ttu-id="6fbeb-261">をクリックして**登録**新しいユーザーを作成します。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-261">Click **Register** to create a new user.</span></span>

    <span data-ttu-id="6fbeb-262">![新しいユーザーを登録する](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image11.png "新しいユーザーを登録します。")</span><span class="sxs-lookup"><span data-stu-id="6fbeb-262">![Registering a new user](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image11.png "Registering a new user")</span></span>

    <span data-ttu-id="6fbeb-263">*新しいユーザーを登録します。*</span><span class="sxs-lookup"><span data-stu-id="6fbeb-263">*Registering a new user*</span></span>
3. <span data-ttu-id="6fbeb-264">**登録** ページで、入力、**ユーザー名**と**パスワード**、クリックして**登録**です。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-264">In the **Register** page, enter a **User name** and **Password**, and then click **Register**.</span></span>

    <span data-ttu-id="6fbeb-265">![登録 ページ](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image12.png "登録ページ")</span><span class="sxs-lookup"><span data-stu-id="6fbeb-265">![Register page](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image12.png "Register page")</span></span>

    <span data-ttu-id="6fbeb-266">*登録 ページ*</span><span class="sxs-lookup"><span data-stu-id="6fbeb-266">*Register page*</span></span>
4. <span data-ttu-id="6fbeb-267">アプリケーションが、新しいアカウントを登録し、ユーザーが認証され、ホーム ページにリダイレクトします。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-267">The application registers the new account and the user is authenticated and redirected back to the home page.</span></span>

    <span data-ttu-id="6fbeb-268">![ユーザーが認証される](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image13.png "認証されたユーザー")</span><span class="sxs-lookup"><span data-stu-id="6fbeb-268">![User is authenticated](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image13.png "User authenticated")</span></span>

    <span data-ttu-id="6fbeb-269">*ユーザーが認証されます。*</span><span class="sxs-lookup"><span data-stu-id="6fbeb-269">*User is authenticated*</span></span>
5. <span data-ttu-id="6fbeb-270">ブラウザーで、キーを押して**F12**を開くには、 **Developer Tools**パネルです。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-270">In the browser, press **F12** to open the **Developer Tools** panel.</span></span> <span data-ttu-id="6fbeb-271">キーを押して**CTRL + 4**  をクリックして、**ネットワーク**アイコンをクリックしてネットワーク トラフィックのキャプチャを開始する緑色の矢印ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-271">Press **CTRL + 4** or click the **Network** icon, and then click the green arrow button to begin capturing network traffic.</span></span>

    <span data-ttu-id="6fbeb-272">![Web API のネットワーク キャプチャを開始する](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image14.png "ネットワーク キャプチャを開始する Web API")</span><span class="sxs-lookup"><span data-stu-id="6fbeb-272">![Initiating Web API network capture](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image14.png "Initiating Web API network capture")</span></span>

    <span data-ttu-id="6fbeb-273">*Web API のネットワーク キャプチャを開始しています*</span><span class="sxs-lookup"><span data-stu-id="6fbeb-273">*Initiating Web API network capture*</span></span>
6. <span data-ttu-id="6fbeb-274">追加**api/トリビア**ブラウザーのアドレス バーの URL にします。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-274">Append **api/trivia** to the URL in the browser's address bar.</span></span> <span data-ttu-id="6fbeb-275">応答の詳細を調査して、ここでは、**取得**でアクション メソッド**TriviaController**です。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-275">You will now inspect the details of the response from the **Get** action method in **TriviaController**.</span></span>

    <span data-ttu-id="6fbeb-276">![Web API を介して次質問データを取得する](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image15.png "Web API を介して次質問データを取得します。")</span><span class="sxs-lookup"><span data-stu-id="6fbeb-276">![Retrieving the next question data through Web API](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image15.png "Retrieving the next question data through Web API")</span></span>

    <span data-ttu-id="6fbeb-277">*Web API を介して次質問データを取得します。*</span><span class="sxs-lookup"><span data-stu-id="6fbeb-277">*Retrieving the next question data through Web API*</span></span>

    > [!NOTE]
    > <span data-ttu-id="6fbeb-278">ダウンロードが終了した、ダウンロードしたファイルの操作を行うが求められます。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-278">Once the download finishes, you will be prompted to make an action with the downloaded file.</span></span> <span data-ttu-id="6fbeb-279">ダイアログ ボックスは、開発者ツール ウィンドウから応答のコンテンツを監視するために開いたままにしておきます。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-279">Leave the dialog box open in order to be able to watch the response content through the Developers Tool window.</span></span>
7. <span data-ttu-id="6fbeb-280">ようになりましたが、応答の本文を検査します。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-280">Now you will inspect the body of the response.</span></span> <span data-ttu-id="6fbeb-281">これを行うをクリックして、**詳細** タブをクリックして**応答本文**です。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-281">To do this, click the **Details** tab and then click **Response body**.</span></span> <span data-ttu-id="6fbeb-282">ダウンロードしたデータが、プロパティを持つオブジェクトをチェックする**オプション**(の一覧は**TriviaOption**オブジェクト)、 **id**と**タイトル**に対応する、 **TriviaQuestion**クラスです。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-282">You can check that the downloaded data is an object with the properties **options** (which is a list of **TriviaOption** objects), **id** and **title** that correspond to the **TriviaQuestion** class.</span></span>

    <span data-ttu-id="6fbeb-283">![Web API の応答本文を表示する](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image16.png "Web API の応答本文を表示します。")</span><span class="sxs-lookup"><span data-stu-id="6fbeb-283">![Viewing the Web API Response Body](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image16.png "Viewing the Web API Response Body")</span></span>

    <span data-ttu-id="6fbeb-284">*表示する Web API の応答本文*</span><span class="sxs-lookup"><span data-stu-id="6fbeb-284">*Viewing Web API Response Body*</span></span>
8. <span data-ttu-id="6fbeb-285">Visual Studio とキーを押してに戻って**shift キーを押しながら f5 キーを押して**デバッグを停止します。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-285">Go back to Visual Studio and press **SHIFT + F5** to stop debugging.</span></span>

<a id="Exercise2"></a>
### <a name="exercise-2-creating-the-spa-interface"></a><span data-ttu-id="6fbeb-286">手順 2: SPA インターフェイスの作成</span><span class="sxs-lookup"><span data-stu-id="6fbeb-286">Exercise 2: Creating the SPA Interface</span></span>

<span data-ttu-id="6fbeb-287">この演習では最初をビルドする、web フロント エンドの部分マニア クイズ、単一ページ アプリケーションの相互作用を使用して、焦点を当てた**AngularJS**です。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-287">In this exercise you will first build the web front-end portion of Geek Quiz, focusing on the Single-Page Application interaction using **AngularJS**.</span></span> <span data-ttu-id="6fbeb-288">機能豊富なアニメーションを実行し、コンテキストの切り替えを 1 つの質問へ移行する場合の視覚効果を提供する css3 用のユーザー エクスペリエンスを拡張します。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-288">You will then enhance the user experience with CSS3 to perform rich animations and provide a visual effect of context switching when transitioning from one question to the next.</span></span>

<a id="Ex2Task1"></a>
#### <a name="task-1--creating-the-spa-interface-using-angularjs"></a><span data-ttu-id="6fbeb-289">作業 1: AngularJS を使用して SPA インターフェイスを作成します。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-289">Task 1 – Creating the SPA Interface Using AngularJS</span></span>

<span data-ttu-id="6fbeb-290">このタスクでは、使用**AngularJS**マニア Quiz アプリケーションのクライアント側を実装します。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-290">In this task you will use **AngularJS** to implement the client side of the Geek Quiz application.</span></span> <span data-ttu-id="6fbeb-291">**AngularJS**でブラウザー ベースのアプリケーションを補足するオープン ソースの JavaScript フレームワークは*モデル-ビュー-コント ローラー* (MVC) の機能、両方の開発を容易にすることと、テストします。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-291">**AngularJS** is an open-source JavaScript framework that augments browser-based applications with *Model-View-Controller* (MVC) capability, facilitating both development and testing.</span></span>

<span data-ttu-id="6fbeb-292">Visual Studio のパッケージ マネージャー コンソールから AngularJS をインストールすることで始めます。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-292">You will start by installing AngularJS from Visual Studio's Package Manager Console.</span></span> <span data-ttu-id="6fbeb-293">その後、マニア クイズ アプリと、クイズの質問と回答 AngularJS テンプレート エンジンを使用して表示するビューの動作を提供するコント ローラーを作成します。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-293">Then, you will create the controller to provide the behavior of the Geek Quiz app and the view to render the quiz questions and answers using the AngularJS template engine.</span></span>

> [!NOTE]
> <span data-ttu-id="6fbeb-294">AngularJS の詳細についてを参照してください[ [http://angularjs.org/](http://angularjs.org/)](http://angularjs.org/)です。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-294">For more information about AngularJS, refer to [[http://angularjs.org/](http://angularjs.org/)](http://angularjs.org/).</span></span>


1. <span data-ttu-id="6fbeb-295">開く**Visual Studio Express 2013 for Web**を開くと、 **GeekQuiz.sln**にソリューションがある、**ソース/Ex2-CreatingASPAInterface/開始**フォルダーです。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-295">Open **Visual Studio Express 2013 for Web** and open the **GeekQuiz.sln** solution located in the **Source/Ex2-CreatingASPAInterface/Begin** folder.</span></span> <span data-ttu-id="6fbeb-296">代わりに、前の手順で取得した、ソリューションを続行できます。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-296">Alternatively, you can continue with the solution that you obtained in the previous exercise.</span></span>
2. <span data-ttu-id="6fbeb-297">開く、 **Package Manager Console**から**ツール** | **ライブラリ パッケージ マネージャー**です。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-297">Open the **Package Manager Console** from **Tools** | **Library Package Manager**.</span></span> <span data-ttu-id="6fbeb-298">インストールする次のコマンドを入力、 **AngularJS.Core** NuGet パッケージです。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-298">Type the following command to install the **AngularJS.Core** NuGet package.</span></span>

    [!code-powershell[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample16.ps1)]
3. <span data-ttu-id="6fbeb-299">**ソリューション エクスプ ローラー**を右クリックし、**スクリプト**のフォルダー、 **GeekQuiz**プロジェクトし、選択**追加 |新しいフォルダー**です。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-299">In **Solution Explorer**, right-click the **Scripts** folder of the **GeekQuiz** project and select **Add | New Folder**.</span></span> <span data-ttu-id="6fbeb-300">名前のフォルダー**アプリ**とキーを押します**Enter**です。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-300">Name the folder **app** and press **Enter**.</span></span>
4. <span data-ttu-id="6fbeb-301">右クリックし、**アプリ**フォルダーだけを作成し、選択**追加 |JavaScript ファイル**です。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-301">Right-click the **app** folder you just created and select **Add | JavaScript File**.</span></span>

    ![新しい JavaScript ファイルを作成します。](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image17.png)

    <span data-ttu-id="6fbeb-303">*新しい JavaScript ファイルを作成します。*</span><span class="sxs-lookup"><span data-stu-id="6fbeb-303">*Creating a new JavaScript file*</span></span>
5. <span data-ttu-id="6fbeb-304">**項目の名前を指定** ダイアログ ボックスで、「*クイズ コント ローラー*で、**項目の名前**テキスト ボックスをクリック**OK**です。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-304">In the **Specify Name for Item** dialog box, type *quiz-controller* in the **Item name** text box and click **OK**.</span></span>

    ![新しい JavaScript ファイルの名前を付ける](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image18.png)

    <span data-ttu-id="6fbeb-306">*新しい JavaScript ファイルの名前を付ける*</span><span class="sxs-lookup"><span data-stu-id="6fbeb-306">*Naming the new JavaScript file*</span></span>
6. <span data-ttu-id="6fbeb-307">**クイズ controller.js**ファイルに追加し、次のコードを宣言および初期化する AngularJS **QuizCtrl**コント ローラー。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-307">In the **quiz-controller.js** file, add the following code to declare and initialize the AngularJS **QuizCtrl** controller.</span></span>

    <span data-ttu-id="6fbeb-308">(コード スニペットの*AspNetWebApiSpa - Ex2 - AngularQuizController*)</span><span class="sxs-lookup"><span data-stu-id="6fbeb-308">(Code Snippet - *AspNetWebApiSpa - Ex2 - AngularQuizController*)</span></span>

    [!code-javascript[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample17.js)]

    > [!NOTE]
    > <span data-ttu-id="6fbeb-309">コンス トラクター関数、 **QuizCtrl**コント ローラーという injectable のパラメーターが必要ですが**$scope**です。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-309">The constructor function of the **QuizCtrl** controller expects an injectable parameter named **$scope**.</span></span> <span data-ttu-id="6fbeb-310">スコープの初期状態必要がありますでセットアップされているコンス トラクター関数のプロパティをアタッチすることによって、 **$scope**オブジェクト。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-310">The initial state of the scope should be set up in the constructor function by attaching properties to the **$scope** object.</span></span> <span data-ttu-id="6fbeb-311">プロパティに含まれる、**ビュー モデル**、コント ローラーを登録するときに、テンプレートにアクセスできるとします。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-311">The properties contain the **view model**, and will be accessible to the template when the controller is registered.</span></span>
    > 
    > <span data-ttu-id="6fbeb-312">**QuizCtrl**コント ローラーがという名前のモジュール内に定義されている**QuizApp**です。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-312">The **QuizCtrl** controller is defined inside a module named **QuizApp**.</span></span> <span data-ttu-id="6fbeb-313">モジュールは、個別のコンポーネントにすることのできる作業単位が、アプリケーションを中断します。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-313">Modules are units of work that let you break your application into separate components.</span></span> <span data-ttu-id="6fbeb-314">モジュールを使用する主な利点は、コードは理解しやすいされ、単体テスト、再利用性と保守が容易になります。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-314">The main advantages of using modules is that the code is easier to understand and facilitates unit testing, reusability and maintainability.</span></span>
7. <span data-ttu-id="6fbeb-315">ビューからトリガーされたイベントに反応するために、スコープを今すぐ動作を追加します。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-315">You will now add behavior to the scope in order to react to events triggered from the view.</span></span> <span data-ttu-id="6fbeb-316">末尾に次のコードを追加、 **QuizCtrl**を定義するコント ローラー、 **nextQuestion**で機能、 **$scope**オブジェクト。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-316">Add the following code at the end of the **QuizCtrl** controller to define the **nextQuestion** function in the **$scope** object.</span></span>

    <span data-ttu-id="6fbeb-317">(コード スニペットの*AspNetWebApiSpa - Ex2 - AngularQuizControllerNextQuestion*)</span><span class="sxs-lookup"><span data-stu-id="6fbeb-317">(Code Snippet - *AspNetWebApiSpa - Ex2 - AngularQuizControllerNextQuestion*)</span></span>

    [!code-javascript[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample18.js)]

    > [!NOTE]
    > <span data-ttu-id="6fbeb-318">この関数から次の質問を取得する、**トリビア**Web API は、前述の手順で作成し、質問にデータを**$scope**オブジェクト。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-318">This function retrieves the next question from the **Trivia** Web API created in the previous exercise and attaches the question data to the **$scope** object.</span></span>
8. <span data-ttu-id="6fbeb-319">最後に、次のコードを挿入、 **QuizCtrl**を定義するコント ローラー、 **sendAnswer**で機能、 **$scope**オブジェクト。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-319">Insert the following code at the end of the **QuizCtrl** controller to define the **sendAnswer** function in the **$scope** object.</span></span>

    <span data-ttu-id="6fbeb-320">(コード スニペットの*AspNetWebApiSpa - Ex2 - AngularQuizControllerSendAnswer*)</span><span class="sxs-lookup"><span data-stu-id="6fbeb-320">(Code Snippet - *AspNetWebApiSpa - Ex2 - AngularQuizControllerSendAnswer*)</span></span>

    [!code-javascript[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample19.js)]

    > [!NOTE]
    > <span data-ttu-id="6fbeb-321">この関数は、ユーザーが選択されている応答を送信、**トリビア**Web API で – つまり、応答が正しいかどう – 場合の結果を格納し、 **$scope**オブジェクト。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-321">This function sends the answer selected by the user to the **Trivia** Web API and stores the result –i.e. if the answer is correct or not– in the **$scope** object.</span></span>
    > 
    > <span data-ttu-id="6fbeb-322">**NextQuestion**と**sendAnswer**上記の関数は、AngularJS を使用して**$http** XMLHttpRequest 経由で Web API との通信を抽象化するオブジェクトJavaScript オブジェクト ブラウザーからです。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-322">The **nextQuestion** and **sendAnswer** functions from above use the AngularJS **$http** object to abstract the communication with the Web API via the XMLHttpRequest JavaScript object from the browser.</span></span> <span data-ttu-id="6fbeb-323">AngularJS には、高い RESTful Api を介してリソースに対して CRUD 操作を実行する抽象化レベルを表示する別のサービスがサポートしています。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-323">AngularJS supports another service that brings a higher level of abstraction to perform CRUD operations against a resource through RESTful APIs.</span></span> <span data-ttu-id="6fbeb-324">AngularJS **$resource**オブジェクトと対話する必要がない高度な動作を提供するアクション メソッドがあります、 **$http**オブジェクト。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-324">The AngularJS **$resource** object has action methods which provide high-level behaviors without the need to interact with the **$http** object.</span></span> <span data-ttu-id="6fbeb-325">使用を検討して、 **$resource** CRUD モデルを必要とするシナリオでのオブジェクト (fore についてを参照してください、 [$resource ドキュメント](https://docs.angularjs.org/api/ngResource/service/$resource))。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-325">Consider using the **$resource** object in scenarios that requires the CRUD model (fore information, see the [$resource documentation](https://docs.angularjs.org/api/ngResource/service/$resource)).</span></span>
9. <span data-ttu-id="6fbeb-326">次の手順では、クイズのビューを定義する AngularJS テンプレートを作成します。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-326">The next step is to create the AngularJS template that defines the view for the quiz.</span></span> <span data-ttu-id="6fbeb-327">これを行うには、開く、 **Index.cshtml**内のファイル、**ビュー |ホーム**フォルダーと次のコードにコンテンツを置換します。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-327">To do this, open the **Index.cshtml** file inside the **Views | Home** folder and replace the content with the following code.</span></span>

    <span data-ttu-id="6fbeb-328">(コード スニペットの*AspNetWebApiSpa - Ex2 - GeekQuizView*)</span><span class="sxs-lookup"><span data-stu-id="6fbeb-328">(Code Snippet - *AspNetWebApiSpa - Ex2 - GeekQuizView*)</span></span>

    [!code-cshtml[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample20.cshtml)]

    > [!NOTE]
    > <span data-ttu-id="6fbeb-329">AngularJS テンプレートは、static のマークアップをブラウザーでユーザーに表示する動的ビューに変換するモデルとコント ローラーからの情報を使用して宣言型の仕様です。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-329">The AngularJS template is a declarative specification that uses information from the model and the controller to transform static markup into the dynamic view that the user sees in the browser.</span></span> <span data-ttu-id="6fbeb-330">AngularJS 要素とテンプレートで使用できる要素の属性の例を次に示します。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-330">The following are examples of AngularJS elements and element attributes that can be used in a template:</span></span>
    > 
    > - <span data-ttu-id="6fbeb-331">**Ng アプリ**ディレクティブは AngularJS アプリケーションのルート要素を表す DOM 要素。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-331">The **ng-app** directive tells AngularJS the DOM element that represents the root element of the application.</span></span>
    > - <span data-ttu-id="6fbeb-332">**Ng コント ローラー**ディレクティブでは、コント ローラーをディレクティブが宣言されている時点で、DOM にアタッチします。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-332">The **ng-controller** directive attaches a controller to the DOM at the point where the directive is declared.</span></span>
    > - <span data-ttu-id="6fbeb-333">中かっこによる表記**{{}}**コント ローラーで定義されているスコープのプロパティへのバインドを表します。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-333">The curly brace notation **{{ }}** denotes bindings to the scope properties defined in the controller.</span></span>
    > - <span data-ttu-id="6fbeb-334">**Ng** ディレクティブを使用して、ユーザーのクリックに応答では、スコープで定義された関数を呼び出します。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-334">The **ng-click** directive is used to invoke the functions defined in the scope in response to user clicks.</span></span>
10. <span data-ttu-id="6fbeb-335">開く、 **Site.css**内のファイル、**コンテンツ**フォルダー クイズのビューのルック アンド フィールを提供するファイルの末尾に次の強調表示されているスタイルを追加します。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-335">Open the **Site.css** file inside the **Content** folder and add the following highlighted styles at the end of the file to provide a look and feel for the quiz view.</span></span>

    <span data-ttu-id="6fbeb-336">(コード スニペットの*AspNetWebApiSpa - Ex2 - GeekQuizStyles*)</span><span class="sxs-lookup"><span data-stu-id="6fbeb-336">(Code Snippet - *AspNetWebApiSpa - Ex2 - GeekQuizStyles*)</span></span>

    [!code-css[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample21.css)]

<a id="Ex2Task2"></a>
#### <a name="task-2--running-the-solution"></a><span data-ttu-id="6fbeb-337">タスク 2 – ソリューションの実行</span><span class="sxs-lookup"><span data-stu-id="6fbeb-337">Task 2 – Running the Solution</span></span>

<span data-ttu-id="6fbeb-338">このタスクを実行します、新しいユーザーを使用してソリューションをインターフェイスに答えるクイズの質問のために AngularJS でビルドします。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-338">In this task you will execute the solution using the new user interface you built with AngularJS to answer some of the quiz questions.</span></span>

1. <span data-ttu-id="6fbeb-339">キーを押して**f5 キーを押して**ソリューションを実行します。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-339">Press **F5** to run the solution.</span></span>
2. <span data-ttu-id="6fbeb-340">新しいユーザー アカウントを登録します。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-340">Register a new user account.</span></span> <span data-ttu-id="6fbeb-341">これを行うには、手順 1 では、タスク 3 で説明されている登録の手順に従います。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-341">To do this, follow the registration steps described in Exercise 1, Task 3.</span></span>

    > [!NOTE]
    > <span data-ttu-id="6fbeb-342">前の手順からソリューションを使用している場合は、以前に作成したユーザー アカウントを使用してログインすることができます。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-342">If you are using the solution from the previous exercise, you can log in with the user account you created before.</span></span>
3. <span data-ttu-id="6fbeb-343">**ホーム**ページが表示されます、クイズの最初の質問を表示します。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-343">The **Home** page should appear, showing the first question of the quiz.</span></span> <span data-ttu-id="6fbeb-344">オプションのいずれかをクリックして、質問に答えます。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-344">Answer the question by clicking one of the options.</span></span> <span data-ttu-id="6fbeb-345">これにより、 **sendAnswer**が選択したオプションを送信する前に、定義されている関数、**トリビア**Web API です。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-345">This will trigger the **sendAnswer** function defined earlier, which sends the selected option to the **Trivia** Web API.</span></span>

    <span data-ttu-id="6fbeb-346">![質問の回答](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image19.png "質問に答えること")</span><span class="sxs-lookup"><span data-stu-id="6fbeb-346">![Answering a question](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image19.png "Answering a question")</span></span>

    <span data-ttu-id="6fbeb-347">*質問に答えること*</span><span class="sxs-lookup"><span data-stu-id="6fbeb-347">*Answering a question*</span></span>
4. <span data-ttu-id="6fbeb-348">一方のボタンをクリックすると、回答が表示されます。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-348">After clicking one of the buttons, the answer should appear.</span></span> <span data-ttu-id="6fbeb-349">をクリックして**次の質問**を次の質問を表示します。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-349">Click **Next Question** to show the following question.</span></span> <span data-ttu-id="6fbeb-350">これにより、 **nextQuestion**コント ローラーで定義された関数。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-350">This will trigger the **nextQuestion** function defined in the controller.</span></span>

    <span data-ttu-id="6fbeb-351">![次の質問を要求する](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image20.png "次の質問を要求します。")</span><span class="sxs-lookup"><span data-stu-id="6fbeb-351">![Requesting the next question](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image20.png "Requesting the next question")</span></span>

    <span data-ttu-id="6fbeb-352">*次の質問を要求します。*</span><span class="sxs-lookup"><span data-stu-id="6fbeb-352">*Requesting the next question*</span></span>
5. <span data-ttu-id="6fbeb-353">次の質問が表示されます。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-353">The next question should appear.</span></span> <span data-ttu-id="6fbeb-354">必要な回数だけの質問に回答を続行します。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-354">Continue answering questions as many times as you want.</span></span> <span data-ttu-id="6fbeb-355">すべての質問を完了した後は、最初の質問を返す必要があります。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-355">After completing all the questions you should return to the first question.</span></span>

    <span data-ttu-id="6fbeb-356">![別の質問](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image21.png "別の問題")</span><span class="sxs-lookup"><span data-stu-id="6fbeb-356">![Another question](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image21.png "Another question")</span></span>

    <span data-ttu-id="6fbeb-357">*次の質問*</span><span class="sxs-lookup"><span data-stu-id="6fbeb-357">*Next question*</span></span>
6. <span data-ttu-id="6fbeb-358">Visual Studio とキーを押してに戻って**shift キーを押しながら f5 キーを押して**デバッグを停止します。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-358">Go back to Visual Studio and press **SHIFT + F5** to stop debugging.</span></span>

<a id="Ex2Task3"></a>
#### <a name="task-3--creating-a-flip-animation-using-css3"></a><span data-ttu-id="6fbeb-359">タスク 3 – CSS3 を使用して反転アニメーションを作成します。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-359">Task 3 – Creating a Flip Animation Using CSS3</span></span>

<span data-ttu-id="6fbeb-360">このタスクでは、CSS3 プロパティを使用して、豊富なアニメーションを実行するには、質問に答えると、次の質問を取得するときに反転効果を追加します。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-360">In this task you will use CSS3 properties to perform rich animations by adding a flip effect when a question is answered and when the next question is retrieved.</span></span>

1. <span data-ttu-id="6fbeb-361">**ソリューション エクスプ ローラー**を右クリックし、**コンテンツ**のフォルダー、 **GeekQuiz**プロジェクトし、選択**追加 |既存アイテム.**.</span><span class="sxs-lookup"><span data-stu-id="6fbeb-361">In **Solution Explorer**, right-click the **Content** folder of the **GeekQuiz** project and select **Add | Existing Item...**.</span></span>

    <span data-ttu-id="6fbeb-362">![コンテンツのフォルダーへの既存の項目の追加](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image22.png "コンテンツのフォルダーへの既存の項目の追加")</span><span class="sxs-lookup"><span data-stu-id="6fbeb-362">![Adding an existing item to the Content folder](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image22.png "Adding an existing item to the Content folder")</span></span>

    <span data-ttu-id="6fbeb-363">*コンテンツのフォルダーへの既存の項目の追加*</span><span class="sxs-lookup"><span data-stu-id="6fbeb-363">*Adding an existing item to the Content folder*</span></span>
2. <span data-ttu-id="6fbeb-364">**既存項目の追加** ダイアログ ボックスに移動、**ソース/資産**フォルダーと選択**Flip.css**です。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-364">In the **Add Existing Item** dialog box, navigate to the **Source/Assets** folder and select **Flip.css**.</span></span> <span data-ttu-id="6fbeb-365">**[追加]**をクリックします。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-365">Click **Add**.</span></span>

    <span data-ttu-id="6fbeb-366">![アセットから Flip.css ファイルを追加する](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image23.png "アセットから Flip.css ファイルを追加します。")</span><span class="sxs-lookup"><span data-stu-id="6fbeb-366">![Adding the Flip.css file from Assets](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image23.png "Adding the Flip.css file from Assets")</span></span>

    <span data-ttu-id="6fbeb-367">*アセットから Flip.css ファイルを追加します。*</span><span class="sxs-lookup"><span data-stu-id="6fbeb-367">*Adding the Flip.css file from Assets*</span></span>
3. <span data-ttu-id="6fbeb-368">開く、 **Flip.css**ファイルだけを追加して、その内容を確認します。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-368">Open the **Flip.css** file you just added and inspect its content.</span></span>
4. <span data-ttu-id="6fbeb-369">検索、**変換を反転**コメントです。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-369">Locate the **flip transformation** comment.</span></span> <span data-ttu-id="6fbeb-370">そのコメントの下のスタイルが CSS を使用して**パースペクティブ**と**rotateY**を生成する変換、&quot;カードのフリップ&quot;効果。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-370">The styles below that comment use the CSS **perspective** and **rotateY** transformations to generate a &quot;card flip&quot; effect.</span></span>

    [!code-css[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample22.css)]
5. <span data-ttu-id="6fbeb-371">検索、**フリップ中にウィンドウの非表示に**コメントです。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-371">Locate the **hide back of pane during flip** comment.</span></span> <span data-ttu-id="6fbeb-372">直面しているビューアーから離れた場所で設定するときにそのコメントの下のスタイルを面の背面にある非表示に、**背面可視性**CSS プロパティを*隠し*です。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-372">The style below that comment hides the back-side of the faces when they are facing away from the viewer by setting the **backface-visibility** CSS property to *hidden*.</span></span>

    [!code-css[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample23.css)]
6. <span data-ttu-id="6fbeb-373">開く、 **BundleConfig.cs**内のファイル、**アプリ\_開始**フォルダーへの参照を追加し、 **Flip.css**ファイルで、  **&quot;~/Content/css&quot;** スタイル バンドル</span><span class="sxs-lookup"><span data-stu-id="6fbeb-373">Open the **BundleConfig.cs** file inside the **App\_Start** folder and add the reference to the **Flip.css** file in the **&quot;~/Content/css&quot;** style bundle</span></span>

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample24.cs)]
7. <span data-ttu-id="6fbeb-374">キーを押して**f5 キーを押して**ソリューションと、資格情報でログインを実行します。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-374">Press **F5** to run the solution and log in with your credentials.</span></span>
8. <span data-ttu-id="6fbeb-375">クリックすると、オプションのいずれかの質問に回答します。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-375">Answer a question by clicking one of the options.</span></span> <span data-ttu-id="6fbeb-376">ビュー間を遷移するときに、反転効果に注目してください。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-376">Notice the flip effect when transitioning between views.</span></span>

    <span data-ttu-id="6fbeb-377">![フリップ効果のある質問の回答](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image24.png "フリップ効果のある質問の回答")</span><span class="sxs-lookup"><span data-stu-id="6fbeb-377">![Answering a question with the flip effect](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image24.png "Answering a question with the flip effect")</span></span>

    <span data-ttu-id="6fbeb-378">*フリップ効果のある質問の回答*</span><span class="sxs-lookup"><span data-stu-id="6fbeb-378">*Answering a question with the flip effect*</span></span>
9. <span data-ttu-id="6fbeb-379">をクリックして**次の質問**を次の質問を取得します。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-379">Click **Next Question** to retrieve the following question.</span></span> <span data-ttu-id="6fbeb-380">フリップ効果が再度表示されます。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-380">The flip effect should appear again.</span></span>

    <span data-ttu-id="6fbeb-381">![次の質問、フリップの効果を取得する](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image25.png "フリップ効果の次の質問を取得します。")</span><span class="sxs-lookup"><span data-stu-id="6fbeb-381">![Retrieving the following question with the flip effect](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image25.png "Retrieving the following question with the flip effect")</span></span>

    <span data-ttu-id="6fbeb-382">*次の質問、フリップの効果を取得します。*</span><span class="sxs-lookup"><span data-stu-id="6fbeb-382">*Retrieving the following question with the flip effect*</span></span>

* * *

<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="6fbeb-383">概要</span><span class="sxs-lookup"><span data-stu-id="6fbeb-383">Summary</span></span>

<span data-ttu-id="6fbeb-384">このハンズオン ラボを完了して学習した方法。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-384">By completing this hands-on lab you have learned how to:</span></span>

- <span data-ttu-id="6fbeb-385">ASP.NET のスキャフォールディングを使用した ASP.NET Web API コント ローラーを作成します。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-385">Create an ASP.NET Web API controller using ASP.NET Scaffolding</span></span>
- <span data-ttu-id="6fbeb-386">クイズの次の質問を取得する Web API 取得操作を実装します。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-386">Implement a Web API Get action to retrieve the next quiz question</span></span>
- <span data-ttu-id="6fbeb-387">質問に対する回答を格納する Web API の後のアクションを実装します。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-387">Implement a Web API Post action to store the quiz answers</span></span>
- <span data-ttu-id="6fbeb-388">Visual Studio パッケージ マネージャー コンソールから AngularJS をインストールします。</span><span class="sxs-lookup"><span data-stu-id="6fbeb-388">Install AngularJS from the Visual Studio Package Manager Console</span></span>
- <span data-ttu-id="6fbeb-389">実装する AngularJS テンプレートとコント ローラー</span><span class="sxs-lookup"><span data-stu-id="6fbeb-389">Implement AngularJS templates and controllers</span></span>
- <span data-ttu-id="6fbeb-390">CSS3 切り替え効果を使用して、アニメーション効果を実行するには</span><span class="sxs-lookup"><span data-stu-id="6fbeb-390">Use CSS3 transitions to perform animation effects</span></span>