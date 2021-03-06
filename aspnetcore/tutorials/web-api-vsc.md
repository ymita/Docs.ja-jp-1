---
title: "ASP.NET Core と VS Code で Web API を作成する"
author: rick-anderson
description: "macOS、Linux、Windows で ASP.NET Core MVC と Visual Studio Code を利用して Web API を構築する"
manager: wpickett
ms.author: riande
ms.date: 09/22/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: get-started-article
uid: tutorials/web-api-vsc
ms.openlocfilehash: 44566c4014400aa2ca3d512eeaa226637b5f0b97
ms.sourcegitcommit: a510f38930abc84c4b302029d019a34dfe76823b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2018
---
# <a name="create-a-web-api-with-aspnet-core-mvc-and-visual-studio-code-on-linux-macos-and-windows"></a>Linux、macOS、Windows で ASP.NET Core MVC と Visual Studio Code を利用して Web API を作成する

作成者: [Rick Anderson](https://twitter.com/RickAndMSFT) と [Mike Wasson](https://github.com/mikewasson)

このチュートリアルでは、"to-do" 項目の一覧を管理する Web API を構築します。 UI が構成されていません。

このチュートリアルには 3 つのバージョンがあります。

* macOS、Linux、Windows: Visual Studio Code で Web API を作成する (本チュートリアル)
* macOS: [Visual Studio for Mac で Web API を作成する](xref:tutorials/first-web-api-mac)
* Windows: [Visual Studio for Windows で Web API を作成する](xref:tutorials/first-web-api)

<!-- WARNING: The code AND images in this doc are used by uid: tutorials/web-api-vsc, tutorials/first-web-api-mac and tutorials/first-web-api. If you change any code/images in this tutorial, update uid: tutorials/web-api-vsc -->

[!INCLUDE[template files](../includes/webApi/intro.md)]

## <a name="set-up-your-development-environment"></a>開発環境を構える

次をダウンロードし、インストールします。
- [.NET Core 2.0.0 SDK](https://www.microsoft.com/net/core) 以降。
- [Visual Studio Code](https://code.visualstudio.com)
- Visual Studio Code [C# 拡張](https://marketplace.visualstudio.com/items?itemName=ms-vscode.csharp)

## <a name="create-the-project"></a>プロジェクトの作成

コンソールから、次のコマンドを実行します。

```console
mkdir TodoApi
cd TodoApi
dotnet new webapi
```

Visual Studio Code (VS Code) で *TodoApi* フォルダーを開き、*Startup.cs* ファイルを選択します。

- "'TodoApi' に作成とデバッグに必要な資産がありません。追加しますか?" という内容の**警告**メッセージが表示されたら、**[はい]** を 選択します。
- [There are unresolved dependencies]/(未解決の依存関係があります/) という内容の**情報**メッセージが表示されたら、**[復元]** を選択します。

<!-- uid: tutorials/first-mvc-app-xplat/start-mvc uses the pic below. If you change it, make sure it's consistent -->

!['TodoApi' に作成とデバッグに必要な資産がありません。 追加しますか?" という警告メッセージが表示された VS Code 今後このメッセージを表示しない, 後で, はい](web-api-vsc/_static/vsc_restore.png)

**[デバッグ]** (F5) を押してプログラムをビルドし、実行します。 ブラウザーで、http://localhost:5000/api/values に移動します。 次が表示されます。

`["value1","value2"]`

VS Code の使用に関するヒントが必要であれば、「[Visual Studio Code ヘルプ](#visual-studio-code-help)」を参照してください。

## <a name="add-support-for-entity-framework-core"></a>Entity Framework Core のサポートの追加

.NET Core 2.0 で新しいプロジェクトを作成すると、*TodoApi.csproj* ファイルに 'Microsoft.AspNetCore.All' プロバイダーが追加されます。 [Entity Framework Core InMemory](https://docs.microsoft.com/ef/core/providers/in-memory/) データベース プロバイダーを個別にインストールする必要はありません。 このデータベース プロバイダーにより、メモリ内のデータベースで Entity Framework Core を使用することが許可されます。

[!code-xml[Main](web-api-vsc/sample/TodoApi/TodoApi.csproj?highlight=12)]

## <a name="add-a-model-class"></a>モデル クラスの追加

モデルとは、アプリケーションのデータを表すオブジェクトです。 ここでは、唯一のモデルが to-do 項目です。

*Models* という名前のフォルダーを追加します。 モデル クラスはプロジェクト内のどこでも配置できますが、慣習で *Models* フォルダーが利用されます。

次のコードで `TodoItem` クラスを追加します。

[!code-csharp[Main](first-web-api/sample/TodoApi/Models/TodoItem.cs)]

`TodoItem` が作成されるとき、データベースは `Id` を生成します。

## <a name="create-the-database-context"></a>データベース コンテキストの作成

*データベース コンテキスト*は、所与のデータ モデルに対し、Entity Framework 機能を調整するメイン クラスです。 このクラスは、`Microsoft.EntityFrameworkCore.DbContext` クラスから派生させて作成します。

*Models* フォルダーに `TodoContext` クラスを追加します。

[!code-csharp[Main](first-web-api/sample/TodoApi/Models/TodoContext.cs)]

[!INCLUDE[Register the database context](../includes/webApi/register_dbContext.md)]

## <a name="add-a-controller"></a>コントローラーの追加

*Controllers* フォルダーで、「`TodoController`」という名前のクラスを作成します。 次のコードを追加します。

[!INCLUDE[code and get todo items](../includes/webApi/getTodoItems.md)]

### <a name="launch-the-app"></a>アプリの起動

VS Code で、F5 を押してアプリを起動します。 http://localhost:5000/api/todo に移動します (先ほど作成した `Todo` コントローラー)。

[!INCLUDE[last part of web API](../includes/webApi/end.md)]

## <a name="visual-studio-code-help"></a>Visual Studio Code ヘルプ

- [はじめに](https://code.visualstudio.com/docs)
- [デバッグ](https://code.visualstudio.com/docs/editor/debugging)
- [統合ターミナル](https://code.visualstudio.com/docs/editor/integrated-terminal)
- [ショートカット キー](https://code.visualstudio.com/docs/getstarted/keybindings#_keyboard-shortcuts-reference)

  - [Mac ショートカット キー](https://code.visualstudio.com/shortcuts/keyboard-shortcuts-macos.pdf)
  - [Linux ショートカット キー](https://code.visualstudio.com/shortcuts/keyboard-shortcuts-linux.pdf)
  - [Windows ショートカット キー](https://code.visualstudio.com/shortcuts/keyboard-shortcuts-windows.pdf)

[!INCLUDE[next steps](../includes/webApi/next.md)]


