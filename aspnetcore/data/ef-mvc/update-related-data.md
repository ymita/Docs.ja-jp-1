---
title: "ASP.NET MVC を持つコアを EF Core - 更新プログラムに関連したデータ - 10 の 7"
author: tdykstra
description: "このチュートリアルでは外部キー フィールドとナビゲーション プロパティを更新することによって関連するデータを更新します。"
keywords: "ASP.NET Core、Entity Framework Core では、関連するデータの結合します。"
ms.author: tdykstra
manager: wpickett
ms.date: 03/15/2017
ms.topic: get-started-article
ms.assetid: 67bd162b-bfb7-4750-9e7f-705228b5288c
ms.technology: aspnet
ms.prod: asp.net-core
uid: data/ef-mvc/update-related-data
ms.openlocfilehash: 85686fe4ebf95f95dc672fbc2d23cddd5bee85e5
ms.sourcegitcommit: 605dc99d241b6d955432bcd42c0178e6e6a212fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/31/2017
---
# <a name="updating-related-data---ef-core-with-aspnet-core-mvc-tutorial-7-of-10"></a><span data-ttu-id="b6cf6-104">関連するデータの EF コア ASP.NET Core MVC のチュートリアル (10 の 7) での更新</span><span class="sxs-lookup"><span data-stu-id="b6cf6-104">Updating related data - EF Core with ASP.NET Core MVC tutorial (7 of 10)</span></span>

<span data-ttu-id="b6cf6-105">によって[Tom Dykstra](https://github.com/tdykstra)と[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="b6cf6-105">By [Tom Dykstra](https://github.com/tdykstra) and [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="b6cf6-106">Contoso 大学でサンプル web アプリケーションでは、Entity Framework のコアと Visual Studio を使用して ASP.NET Core MVC web アプリケーションを作成する方法を示します。</span><span class="sxs-lookup"><span data-stu-id="b6cf6-106">The Contoso University sample web application demonstrates how to create ASP.NET Core MVC web applications using Entity Framework Core and Visual Studio.</span></span> <span data-ttu-id="b6cf6-107">一連のチュートリアルについては、次を参照してください。[系列内の最初のチュートリアル](intro.md)です。</span><span class="sxs-lookup"><span data-stu-id="b6cf6-107">For information about the tutorial series, see [the first tutorial in the series](intro.md).</span></span>

<span data-ttu-id="b6cf6-108">前のチュートリアルでは、関連するデータが表示されます。このチュートリアルでは外部キー フィールドとナビゲーション プロパティを更新することによって関連するデータを更新します。</span><span class="sxs-lookup"><span data-stu-id="b6cf6-108">In the previous tutorial you displayed related data; in this tutorial you'll update related data by updating foreign key fields and navigation properties.</span></span>

<span data-ttu-id="b6cf6-109">次の図を使って作業するページの一部を表示します。</span><span class="sxs-lookup"><span data-stu-id="b6cf6-109">The following illustrations show some of the pages that you'll work with.</span></span>

![コースの編集 ページ](update-related-data/_static/course-edit.png)

![講師の編集 ページ](update-related-data/_static/instructor-edit-courses.png)

## <a name="customize-the-create-and-edit-pages-for-courses"></a><span data-ttu-id="b6cf6-112">コースを作成および編集ページをカスタマイズします。</span><span class="sxs-lookup"><span data-stu-id="b6cf6-112">Customize the Create and Edit Pages for Courses</span></span>

<span data-ttu-id="b6cf6-113">コースの新しいエンティティが作成されると、既存の部署とのリレーションシップが必要です。</span><span class="sxs-lookup"><span data-stu-id="b6cf6-113">When a new course entity is created, it must have a relationship to an existing department.</span></span> <span data-ttu-id="b6cf6-114">この作業を容易にスキャフォールディング コードには、コント ローラーのメソッドおよび部門を選択するためのドロップダウン リストを含むビューを作成および編集が含まれています。</span><span class="sxs-lookup"><span data-stu-id="b6cf6-114">To facilitate this, the scaffolded code includes controller methods and Create and Edit views that include a drop-down list for selecting the department.</span></span> <span data-ttu-id="b6cf6-115">ドロップダウン リストを設定、`Course.DepartmentID`外部キーのプロパティを読み込むために、Entity Framework が必要なすべてが、`Department`適切な部門 エンティティのナビゲーション プロパティ。</span><span class="sxs-lookup"><span data-stu-id="b6cf6-115">The drop-down list sets the `Course.DepartmentID` foreign key property, and that's all the Entity Framework needs in order to load the `Department` navigation property with the appropriate Department entity.</span></span> <span data-ttu-id="b6cf6-116">スキャフォールディングのコードを使用することが、エラー処理を追加し、ドロップダウン リストを並べ替えるには少し変更することもできます。</span><span class="sxs-lookup"><span data-stu-id="b6cf6-116">You'll use the scaffolded code, but change it slightly to add error handling and sort the drop-down list.</span></span>

<span data-ttu-id="b6cf6-117">*CoursesController.cs*、4 つの作成および編集する方法を削除し、次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="b6cf6-117">In *CoursesController.cs*, delete the four Create and Edit methods and replace them with the following code:</span></span>

<span data-ttu-id="b6cf6-118">[!code-csharp[Main](intro/samples/cu/Controllers/CoursesController.cs?name=snippet_CreateGet)]</span><span class="sxs-lookup"><span data-stu-id="b6cf6-118">[!code-csharp[Main](intro/samples/cu/Controllers/CoursesController.cs?name=snippet_CreateGet)]</span></span>

<span data-ttu-id="b6cf6-119">[!code-csharp[Main](intro/samples/cu/Controllers/CoursesController.cs?name=snippet_CreatePost)]</span><span class="sxs-lookup"><span data-stu-id="b6cf6-119">[!code-csharp[Main](intro/samples/cu/Controllers/CoursesController.cs?name=snippet_CreatePost)]</span></span>

<span data-ttu-id="b6cf6-120">[!code-csharp[Main](intro/samples/cu/Controllers/CoursesController.cs?name=snippet_EditGet)]</span><span class="sxs-lookup"><span data-stu-id="b6cf6-120">[!code-csharp[Main](intro/samples/cu/Controllers/CoursesController.cs?name=snippet_EditGet)]</span></span>

<span data-ttu-id="b6cf6-121">[!code-csharp[Main](intro/samples/cu/Controllers/CoursesController.cs?name=snippet_EditPost)]</span><span class="sxs-lookup"><span data-stu-id="b6cf6-121">[!code-csharp[Main](intro/samples/cu/Controllers/CoursesController.cs?name=snippet_EditPost)]</span></span>

<span data-ttu-id="b6cf6-122">後に、 `Edit` HttpPost メソッドをドロップダウン リストの部署の情報を読み込む新しいメソッドを作成します。</span><span class="sxs-lookup"><span data-stu-id="b6cf6-122">After the `Edit` HttpPost method, create a new method that loads department info for the drop-down list.</span></span>

<span data-ttu-id="b6cf6-123">[!code-csharp[Main](intro/samples/cu/Controllers/CoursesController.cs?name=snippet_Departments)]</span><span class="sxs-lookup"><span data-stu-id="b6cf6-123">[!code-csharp[Main](intro/samples/cu/Controllers/CoursesController.cs?name=snippet_Departments)]</span></span>

<span data-ttu-id="b6cf6-124">`PopulateDepartmentsDropDownList`メソッド名でソートのすべての部門の一覧を取得、作成、`SelectList`ドロップダウン一覧は、コレクション内のビューに、コレクションを渡すと`ViewBag`です。</span><span class="sxs-lookup"><span data-stu-id="b6cf6-124">The `PopulateDepartmentsDropDownList` method gets a list of all departments sorted by name, creates a `SelectList` collection for a drop-down list, and passes the collection to the view in `ViewBag`.</span></span> <span data-ttu-id="b6cf6-125">このメソッドは、省略可能な受け取ります`selectedDepartment`パラメーターをドロップダウン リストが表示される場合に選択される項目を指定する呼び出し元のコードを使用します。</span><span class="sxs-lookup"><span data-stu-id="b6cf6-125">The method accepts the optional `selectedDepartment` parameter that allows the calling code to specify the item that will be selected when the drop-down list is rendered.</span></span> <span data-ttu-id="b6cf6-126">ビューが名前"DepartmentID"に渡す、`<select>`とヘルパーのタグ ヘルパーに渡し、ファイルの場所を知っているし、`ViewBag`オブジェクトに対する、 `SelectList` "DepartmentID"という名前です。</span><span class="sxs-lookup"><span data-stu-id="b6cf6-126">The view will pass the name "DepartmentID" to the `<select>` tag helper, and the helper then knows to look in the `ViewBag` object for a `SelectList` named "DepartmentID".</span></span>

<span data-ttu-id="b6cf6-127">HttpGet`Create`メソッドの呼び出し、`PopulateDepartmentsDropDownList`新しいコースの部門が確立されていないため、選択したアイテムを設定しなくてもメソッド。</span><span class="sxs-lookup"><span data-stu-id="b6cf6-127">The HttpGet `Create` method calls the `PopulateDepartmentsDropDownList` method without setting the selected item, because for a new course the department is not established yet:</span></span>

<span data-ttu-id="b6cf6-128">[!code-csharp[Main](intro/samples/cu/Controllers/CoursesController.cs?highlight=3&name=snippet_CreateGet)]</span><span class="sxs-lookup"><span data-stu-id="b6cf6-128">[!code-csharp[Main](intro/samples/cu/Controllers/CoursesController.cs?highlight=3&name=snippet_CreateGet)]</span></span>

<span data-ttu-id="b6cf6-129">HttpGet`Edit`メソッドは編集されているコースに既に割り当てられている部門の ID に基づいて、選択したアイテムを設定します。</span><span class="sxs-lookup"><span data-stu-id="b6cf6-129">The HttpGet `Edit` method sets the selected item, based on the ID of the department that is already assigned to the course being edited:</span></span>

<span data-ttu-id="b6cf6-130">[!code-csharp[Main](intro/samples/cu/Controllers/CoursesController.cs?highlight=15&name=snippet_EditGet)]</span><span class="sxs-lookup"><span data-stu-id="b6cf6-130">[!code-csharp[Main](intro/samples/cu/Controllers/CoursesController.cs?highlight=15&name=snippet_EditGet)]</span></span>

<span data-ttu-id="b6cf6-131">両方の HttpPost メソッド`Create`と`Edit`もエラーが発生したページを再表示するときに、選択した項目を設定するコードが含まれます。</span><span class="sxs-lookup"><span data-stu-id="b6cf6-131">The HttpPost methods for both `Create` and `Edit` also include code that sets the selected item when they redisplay the page after an error.</span></span> <span data-ttu-id="b6cf6-132">これにより、エラー メッセージを表示する、ページが表示され、ときにどのような部門が選択されている選択されたままです。</span><span class="sxs-lookup"><span data-stu-id="b6cf6-132">This ensures that when the page is redisplayed to show the error message, whatever department was selected stays selected.</span></span>

### <a name="add-asnotracking-to-details-and-delete-methods"></a><span data-ttu-id="b6cf6-133">追加します。詳細を AsNoTracking および Delete メソッド</span><span class="sxs-lookup"><span data-stu-id="b6cf6-133">Add .AsNoTracking to Details and Delete methods</span></span>

<span data-ttu-id="b6cf6-134">コースの詳細と Delete のページのパフォーマンスを最適化するには追加`AsNoTracking`で呼び出し、`Details`と HttpGet`Delete`メソッドです。</span><span class="sxs-lookup"><span data-stu-id="b6cf6-134">To optimize performance of the Course Details and Delete pages, add `AsNoTracking` calls in the `Details` and HttpGet `Delete` methods.</span></span>

<span data-ttu-id="b6cf6-135">[!code-csharp[Main](intro/samples/cu/Controllers/CoursesController.cs?highlight=10&name=snippet_Details)]</span><span class="sxs-lookup"><span data-stu-id="b6cf6-135">[!code-csharp[Main](intro/samples/cu/Controllers/CoursesController.cs?highlight=10&name=snippet_Details)]</span></span>

<span data-ttu-id="b6cf6-136">[!code-csharp[Main](intro/samples/cu/Controllers/CoursesController.cs?highlight=10&name=snippet_DeleteGet)]</span><span class="sxs-lookup"><span data-stu-id="b6cf6-136">[!code-csharp[Main](intro/samples/cu/Controllers/CoursesController.cs?highlight=10&name=snippet_DeleteGet)]</span></span>

### <a name="modify-the-course-views"></a><span data-ttu-id="b6cf6-137">コースのビューを変更します。</span><span class="sxs-lookup"><span data-stu-id="b6cf6-137">Modify the Course views</span></span>

<span data-ttu-id="b6cf6-138">*Views/Courses/Create.cshtml*、"Select Department"オプションを追加、**部門**ドロップダウン リストで、変更のキャプションの変更**DepartmentID**に**部門**、検証メッセージを追加します。</span><span class="sxs-lookup"><span data-stu-id="b6cf6-138">In *Views/Courses/Create.cshtml*, add a "Select Department" option to the **Department** drop-down list, change the caption from **DepartmentID** to **Department**, and add a validation message.</span></span>

<span data-ttu-id="b6cf6-139">[!code-html[Main](intro/samples/cu/Views/Courses/Create.cshtml?highlight=2-6&range=29-34)]</span><span class="sxs-lookup"><span data-stu-id="b6cf6-139">[!code-html[Main](intro/samples/cu/Views/Courses/Create.cshtml?highlight=2-6&range=29-34)]</span></span>

<span data-ttu-id="b6cf6-140">*Views/Courses/Edit.cshtml*、部門フィールドだけで行ったの同じ変更を加える*Create.cshtml*です。</span><span class="sxs-lookup"><span data-stu-id="b6cf6-140">In *Views/Courses/Edit.cshtml*, make the same change for the Department field that you just did in *Create.cshtml*.</span></span>

<span data-ttu-id="b6cf6-141">また、 *Views/Courses/Edit.cshtml*、コースの前に数値フィールドを追加、**タイトル**フィールドです。</span><span class="sxs-lookup"><span data-stu-id="b6cf6-141">Also in *Views/Courses/Edit.cshtml*, add a course number field before the **Title** field.</span></span> <span data-ttu-id="b6cf6-142">コース番号は、主キーであるためが表示されますが、変更することはできません。</span><span class="sxs-lookup"><span data-stu-id="b6cf6-142">Because the course number is the primary key, it's displayed, but it can't be changed.</span></span>

<span data-ttu-id="b6cf6-143">[!code-html[Main](intro/samples/cu/Views/Courses/Edit.cshtml?range=15-18)]</span><span class="sxs-lookup"><span data-stu-id="b6cf6-143">[!code-html[Main](intro/samples/cu/Views/Courses/Edit.cshtml?range=15-18)]</span></span>

<span data-ttu-id="b6cf6-144">非表示フィールドが既に存在 (`<input type="hidden">`) の編集ビューでコース番号。</span><span class="sxs-lookup"><span data-stu-id="b6cf6-144">There's already a hidden field (`<input type="hidden">`) for the course number in the Edit view.</span></span> <span data-ttu-id="b6cf6-145">追加する、 `<label>` 、ユーザーがクリックしたときに、ポストされたデータに含まれるコース番号が原因であるために、タグ ヘルパーは隠しフィールドの必要性を排除しない**保存**上、**編集**ページ。</span><span class="sxs-lookup"><span data-stu-id="b6cf6-145">Adding a `<label>` tag helper doesn't eliminate the need for the hidden field because it doesn't cause the course number to be included in the posted data when the user clicks **Save** on the **Edit** page.</span></span>

<span data-ttu-id="b6cf6-146">*Views/Courses/Delete.cshtml*上部にある一連の数値フィールドを追加および部署名を部門 ID を変更します。</span><span class="sxs-lookup"><span data-stu-id="b6cf6-146">In *Views/Courses/Delete.cshtml*, add a course number field at the top and change department ID to department name.</span></span>

<span data-ttu-id="b6cf6-147">[!code-html[Main](intro/samples/cu/Views/Courses/Delete.cshtml?highlight=14-19,36)]</span><span class="sxs-lookup"><span data-stu-id="b6cf6-147">[!code-html[Main](intro/samples/cu/Views/Courses/Delete.cshtml?highlight=14-19,36)]</span></span>

<span data-ttu-id="b6cf6-148">*Views/Course/Details.cshtml*、だけで実行したの同じ変更を加えます*Delete.cshtml*です。</span><span class="sxs-lookup"><span data-stu-id="b6cf6-148">In *Views/Course/Details.cshtml*, make the same change that you just did for *Delete.cshtml*.</span></span>

### <a name="test-the-course-pages"></a><span data-ttu-id="b6cf6-149">コース ページをテストします。</span><span class="sxs-lookup"><span data-stu-id="b6cf6-149">Test the Course pages</span></span>

<span data-ttu-id="b6cf6-150">実行、**作成**ページ (コース インデックス ページを表示し、をクリックして**新規作成**) と新しいコースのデータを入力します。</span><span class="sxs-lookup"><span data-stu-id="b6cf6-150">Run the **Create** page (display the Course Index page and click **Create New**) and enter data for a new course:</span></span>

![コースの作成 ページ](update-related-data/_static/course-create.png)

<span data-ttu-id="b6cf6-152">
              **[作成]**をクリックします。</span><span class="sxs-lookup"><span data-stu-id="b6cf6-152">Click **Create**.</span></span> <span data-ttu-id="b6cf6-153">一覧に追加された新しいコース コース インデックス ページが表示されます。</span><span class="sxs-lookup"><span data-stu-id="b6cf6-153">The Courses Index page is displayed with the new course added to the list.</span></span> <span data-ttu-id="b6cf6-154">インデックス ページの一覧で、部門名を示すリレーションシップが正常に確立されているナビゲーション プロパティに由来します。</span><span class="sxs-lookup"><span data-stu-id="b6cf6-154">The department name in the Index page list comes from the navigation property, showing that the relationship was established correctly.</span></span>

<span data-ttu-id="b6cf6-155">実行、**編集**ページ (をクリックして**編集**コース インデックス ページ内のコースに)。</span><span class="sxs-lookup"><span data-stu-id="b6cf6-155">Run the **Edit** page (click **Edit** on a course in the Course Index page ).</span></span>

![コースの編集 ページ](update-related-data/_static/course-edit.png)

<span data-ttu-id="b6cf6-157">ページ上のデータを変更し、クリックして**保存**です。</span><span class="sxs-lookup"><span data-stu-id="b6cf6-157">Change data on the page and click **Save**.</span></span> <span data-ttu-id="b6cf6-158">コース インデックス ページには、更新された一連のデータが表示されます。</span><span class="sxs-lookup"><span data-stu-id="b6cf6-158">The Courses Index page is displayed with the updated course data.</span></span>

## <a name="add-an-edit-page-for-instructors"></a><span data-ttu-id="b6cf6-159">講習においてインストラクター編集ページを追加します。</span><span class="sxs-lookup"><span data-stu-id="b6cf6-159">Add an Edit Page for Instructors</span></span>

<span data-ttu-id="b6cf6-160">講師レコードを編集するときに、インストラクター オフィス割り当てを更新することにします。</span><span class="sxs-lookup"><span data-stu-id="b6cf6-160">When you edit an instructor record, you want to be able to update the instructor's office assignment.</span></span> <span data-ttu-id="b6cf6-161">Instructor エンティティには、OfficeAssignment エンティティが、コードには、次の状況を処理することを意味する 0 または 1 を 1 つのリレーションシップがあります。</span><span class="sxs-lookup"><span data-stu-id="b6cf6-161">The Instructor entity has a one-to-zero-or-one relationship with the OfficeAssignment entity, which means your code has to handle the following situations:</span></span>

* <span data-ttu-id="b6cf6-162">場合は、ユーザーがオフィス割り当てをクリアし、値が最初にあった、OfficeAssignment エンティティを削除します。</span><span class="sxs-lookup"><span data-stu-id="b6cf6-162">If the user clears the office assignment and it originally had a value, delete the OfficeAssignment entity.</span></span>

* <span data-ttu-id="b6cf6-163">ユーザーが office 代入値を入力し、空か最初場合、は、新しい OfficeAssignment エンティティを作成します。</span><span class="sxs-lookup"><span data-stu-id="b6cf6-163">If the user enters an office assignment value and it originally was empty, create a new OfficeAssignment entity.</span></span>

* <span data-ttu-id="b6cf6-164">ユーザーは、office の代入式の値を変更する場合は、OfficeAssignment の既存のエンティティの値を変更します。</span><span class="sxs-lookup"><span data-stu-id="b6cf6-164">If the user changes the value of an office assignment, change the value in an existing OfficeAssignment entity.</span></span>

### <a name="update-the-instructors-controller"></a><span data-ttu-id="b6cf6-165">講習においてインストラクター コント ローラーを更新します。</span><span class="sxs-lookup"><span data-stu-id="b6cf6-165">Update the Instructors controller</span></span>

<span data-ttu-id="b6cf6-166">*InstructorsController.cs*、コード、HttpGet を変更します`Edit`メソッドがロード Instructor エンティティのため`OfficeAssignment`ナビゲーション プロパティと呼び出し`AsNoTracking`:</span><span class="sxs-lookup"><span data-stu-id="b6cf6-166">In *InstructorsController.cs*, change the code in the HttpGet `Edit` method so that it loads the Instructor entity's `OfficeAssignment` navigation property and calls `AsNoTracking`:</span></span>

<span data-ttu-id="b6cf6-167">[!code-csharp[Main](intro/samples/cu/Controllers/InstructorsController.cs?highlight=9,10&name=snippet_EditGetOA)]</span><span class="sxs-lookup"><span data-stu-id="b6cf6-167">[!code-csharp[Main](intro/samples/cu/Controllers/InstructorsController.cs?highlight=9,10&name=snippet_EditGetOA)]</span></span>

<span data-ttu-id="b6cf6-168">置換、HttpPost `Edit` office 割り当ての更新を処理する次のコードにメソッド。</span><span class="sxs-lookup"><span data-stu-id="b6cf6-168">Replace the HttpPost `Edit` method with the following code to handle office assignment updates:</span></span>

<span data-ttu-id="b6cf6-169">[!code-csharp[Main](intro/samples/cu/Controllers/InstructorsController.cs?name=snippet_EditPostOA)]</span><span class="sxs-lookup"><span data-stu-id="b6cf6-169">[!code-csharp[Main](intro/samples/cu/Controllers/InstructorsController.cs?name=snippet_EditPostOA)]</span></span>

<span data-ttu-id="b6cf6-170">コードは次のとおり</span><span class="sxs-lookup"><span data-stu-id="b6cf6-170">The code does the following:</span></span>

-  <span data-ttu-id="b6cf6-171">メソッドの名前を変更`EditPost`署名は、ここでは、HttpGet と同じため`Edit`メソッド (、`ActionName`属性を指定する、 `/Edit/` URL はまだ使用)。</span><span class="sxs-lookup"><span data-stu-id="b6cf6-171">Changes the method name to `EditPost` because the signature is now the same as the HttpGet `Edit` method (the `ActionName` attribute specifies that the `/Edit/` URL is still used).</span></span>

-  <span data-ttu-id="b6cf6-172">一括読み込みのデータベースを使用して、現在 Instructor エンティティを取得、`OfficeAssignment`ナビゲーション プロパティ。</span><span class="sxs-lookup"><span data-stu-id="b6cf6-172">Gets the current Instructor entity from the database using eager loading for the `OfficeAssignment` navigation property.</span></span> <span data-ttu-id="b6cf6-173">これは、HttpGet で行ったのと同じ`Edit`メソッドです。</span><span class="sxs-lookup"><span data-stu-id="b6cf6-173">This is the same as what you did in the HttpGet `Edit` method.</span></span>

-  <span data-ttu-id="b6cf6-174">モデル バインダーから値を取得した Instructor エンティティを更新します。</span><span class="sxs-lookup"><span data-stu-id="b6cf6-174">Updates the retrieved Instructor entity with values from the model binder.</span></span> <span data-ttu-id="b6cf6-175">`TryUpdateModel`オーバー ロードでは、ホワイト リストに追加するプロパティです。</span><span class="sxs-lookup"><span data-stu-id="b6cf6-175">The `TryUpdateModel` overload enables you to whitelist the properties you want to include.</span></span> <span data-ttu-id="b6cf6-176">こうすれば、過剰な投稿で説明するよう、 [2 番目のチュートリアル](crud.md)です。</span><span class="sxs-lookup"><span data-stu-id="b6cf6-176">This prevents over-posting, as explained in the [second tutorial](crud.md).</span></span>

    <!-- Snippets do not play well with <ul> [!code-csharp[Main](intro/samples/cu/Controllers/InstructorsController.cs?range=241-244)] -->

    ```csharp
    if (await TryUpdateModelAsync<Instructor>(
        instructorToUpdate,
        "",
        i => i.FirstMidName, i => i.LastName, i => i.HireDate, i => i.OfficeAssignment))
    ```
    
-   <span data-ttu-id="b6cf6-177">オフィスの場所が空白の場合は、null OfficeAssignment の表に、関連する行が削除されるように Instructor.OfficeAssignment プロパティを設定します。</span><span class="sxs-lookup"><span data-stu-id="b6cf6-177">If the office location is blank, sets the Instructor.OfficeAssignment property to null so that the related row in the OfficeAssignment table will be deleted.</span></span>

    <!-- Snippets do not play well with <ul>  "intro/samples/cu/Controllers/InstructorsController.cs"} -->

    ```csharp
    if (String.IsNullOrWhiteSpace(instructorToUpdate.OfficeAssignment?.Location))
    {
        instructorToUpdate.OfficeAssignment = null;
    }
    ```

- <span data-ttu-id="b6cf6-178">データベースに変更を保存します。</span><span class="sxs-lookup"><span data-stu-id="b6cf6-178">Saves the changes to the database.</span></span>

### <a name="update-the-instructor-edit-view"></a><span data-ttu-id="b6cf6-179">更新プログラム、インストラクター ビューの編集</span><span class="sxs-lookup"><span data-stu-id="b6cf6-179">Update the Instructor Edit view</span></span>

<span data-ttu-id="b6cf6-180">*Views/Instructors/Edit.cshtml*、新しいフィールドを追加する前に最後に、オフィスの場所を編集、**保存**ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="b6cf6-180">In *Views/Instructors/Edit.cshtml*, add a new field for editing the office location, at the end before the **Save** button:</span></span>

<span data-ttu-id="b6cf6-181">[!code-html[Main](intro/samples/cu/Views/Instructors/Edit.cshtml?range=30-34)]</span><span class="sxs-lookup"><span data-stu-id="b6cf6-181">[!code-html[Main](intro/samples/cu/Views/Instructors/Edit.cshtml?range=30-34)]</span></span>

<span data-ttu-id="b6cf6-182">ページの実行 (選択、**講習においてインストラクター**  タブをクリックして**編集**インストラクターに)。</span><span class="sxs-lookup"><span data-stu-id="b6cf6-182">Run the page (select the **Instructors** tab and then click **Edit** on an instructor).</span></span> <span data-ttu-id="b6cf6-183">変更、**オフィス** をクリック**保存**です。</span><span class="sxs-lookup"><span data-stu-id="b6cf6-183">Change the **Office Location** and click **Save**.</span></span>

![講師の編集 ページ](update-related-data/_static/instructor-edit-office.png)

## <a name="add-course-assignments-to-the-instructor-edit-page"></a><span data-ttu-id="b6cf6-185">コースの課題をインストラクターの編集 ページに追加します。</span><span class="sxs-lookup"><span data-stu-id="b6cf6-185">Add Course assignments to the Instructor Edit page</span></span>

<span data-ttu-id="b6cf6-186">講習においてインストラクターには、コースの任意の数を教えることがあります。</span><span class="sxs-lookup"><span data-stu-id="b6cf6-186">Instructors may teach any number of courses.</span></span> <span data-ttu-id="b6cf6-187">次のスクリーン ショットに示すように、チェック ボックスのグループを使用して、course 割り当てを変更する機能を追加することでインストラクターの編集 ページを拡張します。</span><span class="sxs-lookup"><span data-stu-id="b6cf6-187">Now you'll enhance the Instructor Edit page by adding the ability to change course assignments using a group of check boxes, as shown in the following screen shot:</span></span>

![コースをインストラクターの編集 ページ](update-related-data/_static/instructor-edit-courses.png)

<span data-ttu-id="b6cf6-189">コース、インストラクター エンティティ間のリレーションシップは、多対多です。</span><span class="sxs-lookup"><span data-stu-id="b6cf6-189">The relationship between the Course and Instructor entities is many-to-many.</span></span> <span data-ttu-id="b6cf6-190">追加し、リレーションシップを削除、追加し、CourseAssignments 結合エンティティ セットからエンティティを削除します。</span><span class="sxs-lookup"><span data-stu-id="b6cf6-190">To add and remove relationships, you add and remove entities to and from the CourseAssignments join entity set.</span></span>

<span data-ttu-id="b6cf6-191">UI コースを変更することができるインストラクターに割り当てられているチェック ボックスのグループです。</span><span class="sxs-lookup"><span data-stu-id="b6cf6-191">The UI that enables you to change which courses an instructor is assigned to is a group of check boxes.</span></span> <span data-ttu-id="b6cf6-192">データベース内のすべてのコースのチェック ボックスが表示され、インストラクターに現在割り当てられているものを選択します。</span><span class="sxs-lookup"><span data-stu-id="b6cf6-192">A check box for every course in the database is displayed, and the ones that the instructor is currently assigned to are selected.</span></span> <span data-ttu-id="b6cf6-193">ユーザーでは、選択したり、コースの割り当てを変更する チェック ボックスをオフにすることができます。</span><span class="sxs-lookup"><span data-stu-id="b6cf6-193">The user can select or clear check boxes to change course assignments.</span></span> <span data-ttu-id="b6cf6-194">コースの数が非常に大きい場合は、他のビューでは、データの表示方法を使用することはおそらくはメソッドを使用する、同じ結合エンティティを操作するためのリレーションシップを作成または削除します。</span><span class="sxs-lookup"><span data-stu-id="b6cf6-194">If the number of courses were much greater, you would probably want to use a different method of presenting the data in the view, but you'd use the same method of manipulating a join entity to create or delete relationships.</span></span>

### <a name="update-the-instructors-controller"></a><span data-ttu-id="b6cf6-195">講習においてインストラクター コント ローラーを更新します。</span><span class="sxs-lookup"><span data-stu-id="b6cf6-195">Update the Instructors controller</span></span>

<span data-ttu-id="b6cf6-196">チェック ボックスの一覧については、ビューにデータを提供するには、ビュー モデル クラスを使用します。</span><span class="sxs-lookup"><span data-stu-id="b6cf6-196">To provide data to the view for the list of check boxes, you'll use a view model class.</span></span>

<span data-ttu-id="b6cf6-197">作成*AssignedCourseData.cs*で、 *SchoolViewModels*フォルダーと、既存のコードを次のコードを置換します。</span><span class="sxs-lookup"><span data-stu-id="b6cf6-197">Create *AssignedCourseData.cs* in the *SchoolViewModels* folder and replace the existing code with the following code:</span></span>

<span data-ttu-id="b6cf6-198">[!code-csharp[Main](intro/samples/cu/Models/SchoolViewModels/AssignedCourseData.cs)]</span><span class="sxs-lookup"><span data-stu-id="b6cf6-198">[!code-csharp[Main](intro/samples/cu/Models/SchoolViewModels/AssignedCourseData.cs)]</span></span>

<span data-ttu-id="b6cf6-199">*InstructorsController.cs*、置換、HttpGet`Edit`メソッドを次のコード。</span><span class="sxs-lookup"><span data-stu-id="b6cf6-199">In *InstructorsController.cs*, replace the HttpGet `Edit` method with the following code.</span></span> <span data-ttu-id="b6cf6-200">変更が強調表示されます。</span><span class="sxs-lookup"><span data-stu-id="b6cf6-200">The changes are highlighted.</span></span>

<span data-ttu-id="b6cf6-201">[!code-csharp[Main](intro/samples/cu/Controllers/InstructorsController.cs?highlight=10,17,21,22,23,24,25,26,27,28,29,30,31,32,33,34,35,36&name=snippet_EditGetCourses)]</span><span class="sxs-lookup"><span data-stu-id="b6cf6-201">[!code-csharp[Main](intro/samples/cu/Controllers/InstructorsController.cs?highlight=10,17,21,22,23,24,25,26,27,28,29,30,31,32,33,34,35,36&name=snippet_EditGetCourses)]</span></span>

<span data-ttu-id="b6cf6-202">コードでは、追加の一括読み込み、`Courses`ナビゲーション プロパティ、新しいを呼び出すと`PopulateAssignedCourseData` チェック ボックスを配列の使用に関する情報を提供するメソッドを`AssignedCourseData`モデル クラスを表示します。</span><span class="sxs-lookup"><span data-stu-id="b6cf6-202">The code adds eager loading for the `Courses` navigation property and calls the new `PopulateAssignedCourseData` method to provide information for the check box array using the `AssignedCourseData` view model class.</span></span>

<span data-ttu-id="b6cf6-203">内のコード、`PopulateAssignedCourseData`メソッドをビュー モデル クラスを使用してコースの一覧を読み込むためにすべてのコース エンティティを読み取ります。</span><span class="sxs-lookup"><span data-stu-id="b6cf6-203">The code in the `PopulateAssignedCourseData` method reads through all Course entities in order to load a list of courses using the view model class.</span></span> <span data-ttu-id="b6cf6-204">コードが、インストラクターにコースが存在するかどうかをチェック各コースに`Courses`ナビゲーション プロパティ。</span><span class="sxs-lookup"><span data-stu-id="b6cf6-204">For each course, the code checks whether the course exists in the instructor's `Courses` navigation property.</span></span> <span data-ttu-id="b6cf6-205">コースをインストラクターに割り当てられているかどうかをチェックするときに、効率的な参照を作成するには、インストラクターに割り当てられているコースに配置されます、`HashSet`コレクション。</span><span class="sxs-lookup"><span data-stu-id="b6cf6-205">To create efficient lookup when checking whether a course is assigned to the instructor, the courses assigned to the instructor are put into a `HashSet` collection.</span></span> <span data-ttu-id="b6cf6-206">`Assigned`プロパティに設定されているコースの場合は true、インストラクターに割り当てられます。</span><span class="sxs-lookup"><span data-stu-id="b6cf6-206">The `Assigned` property  is set to true for courses the instructor is assigned to.</span></span> <span data-ttu-id="b6cf6-207">ビューは、このプロパティを使用して、どのチェック ボックスとして表示する選択を確認されます。</span><span class="sxs-lookup"><span data-stu-id="b6cf6-207">The view will use this property to determine which check boxes must be displayed as selected.</span></span> <span data-ttu-id="b6cf6-208">最後に、一覧は、ビューに渡される`ViewData`です。</span><span class="sxs-lookup"><span data-stu-id="b6cf6-208">Finally, the list is passed to the view in `ViewData`.</span></span>

<span data-ttu-id="b6cf6-209">次に、ユーザーがクリックしたときに実行されるコードを追加**保存**です。</span><span class="sxs-lookup"><span data-stu-id="b6cf6-209">Next, add the code that's executed when the user clicks **Save**.</span></span> <span data-ttu-id="b6cf6-210">置換、`EditPost`メソッドに次のコードし、更新する新しいメソッドを追加、 `Courses` Instructor エンティティのナビゲーション プロパティ。</span><span class="sxs-lookup"><span data-stu-id="b6cf6-210">Replace the `EditPost` method with the following code, and add a new method that updates the `Courses` navigation property of the Instructor entity.</span></span>

<span data-ttu-id="b6cf6-211">[!code-csharp[Main](intro/samples/cu/Controllers/InstructorsController.cs?highlight=1,3,12,13,25,39-40&name=snippet_EditPostCourses)]</span><span class="sxs-lookup"><span data-stu-id="b6cf6-211">[!code-csharp[Main](intro/samples/cu/Controllers/InstructorsController.cs?highlight=1,3,12,13,25,39-40&name=snippet_EditPostCourses)]</span></span>

<span data-ttu-id="b6cf6-212">[!code-csharp[Main](intro/samples/cu/Controllers/InstructorsController.cs?name=snippet_UpdateCourses&highlight=1-31)]</span><span class="sxs-lookup"><span data-stu-id="b6cf6-212">[!code-csharp[Main](intro/samples/cu/Controllers/InstructorsController.cs?name=snippet_UpdateCourses&highlight=1-31)]</span></span>

<span data-ttu-id="b6cf6-213">メソッドのシグネチャは、HttpGet を異なるようになりました`Edit`メソッド、メソッド名の変更から`EditPost`に`Edit`です。</span><span class="sxs-lookup"><span data-stu-id="b6cf6-213">The method signature is now different from the HttpGet `Edit` method, so the method name changes from `EditPost` back to `Edit`.</span></span>

<span data-ttu-id="b6cf6-214">モデル バインダーを自動的に更新できないビューでは、コース エンティティのコレクションがあるないため、`CourseAssignments`ナビゲーション プロパティ。</span><span class="sxs-lookup"><span data-stu-id="b6cf6-214">Since the view doesn't have a collection of Course entities, the model binder can't automatically update the `CourseAssignments` navigation property.</span></span> <span data-ttu-id="b6cf6-215">モデル バインダーを使用して更新するのではなく、`CourseAssignments`ナビゲーション プロパティ、新しいすれば`UpdateInstructorCourses`メソッドです。</span><span class="sxs-lookup"><span data-stu-id="b6cf6-215">Instead of using the model binder to update the `CourseAssignments` navigation property, you do that in the new `UpdateInstructorCourses` method.</span></span> <span data-ttu-id="b6cf6-216">除外する必要があるため、`CourseAssignments`モデル バインドからのプロパティです。</span><span class="sxs-lookup"><span data-stu-id="b6cf6-216">Therefore you need to exclude the `CourseAssignments` property from model binding.</span></span> <span data-ttu-id="b6cf6-217">これを呼び出すコードの変更が必要としない`TryUpdateModel`ホワイト リストをオーバー ロードを使用しているためと`CourseAssignments`は include リストではありません。</span><span class="sxs-lookup"><span data-stu-id="b6cf6-217">This doesn't require any change to the code that calls `TryUpdateModel` because you're using the whitelisting overload and `CourseAssignments` isn't in the include list.</span></span>

<span data-ttu-id="b6cf6-218">チェックを行わないボックスを選択した場合のコード場合、`UpdateInstructorCourses`を初期化、`CourseAssignments`ナビゲーション プロパティが空のコレクションを返します。</span><span class="sxs-lookup"><span data-stu-id="b6cf6-218">If no check boxes were selected, the code in `UpdateInstructorCourses` initializes the `CourseAssignments` navigation property with an empty collection and returns:</span></span>

<span data-ttu-id="b6cf6-219">[!code-csharp[Main](intro/samples/cu/Controllers/InstructorsController.cs?name=snippet_UpdateCourses&highlight=3-7)]</span><span class="sxs-lookup"><span data-stu-id="b6cf6-219">[!code-csharp[Main](intro/samples/cu/Controllers/InstructorsController.cs?name=snippet_UpdateCourses&highlight=3-7)]</span></span>

<span data-ttu-id="b6cf6-220">コードは、データベース内のすべてのコースをループ処理し、ビューで選択されたものではなくインストラクターに現在割り当てられているものに対しては、各コースを確認します。</span><span class="sxs-lookup"><span data-stu-id="b6cf6-220">The code then loops through all courses in the database and checks each course against the ones currently assigned to the instructor versus the ones that were selected in the view.</span></span> <span data-ttu-id="b6cf6-221">効率的な検索を容易に後者の 2 つのコレクションが格納されている`HashSet`オブジェクト。</span><span class="sxs-lookup"><span data-stu-id="b6cf6-221">To facilitate efficient lookups, the latter two collections are stored in `HashSet` objects.</span></span>

<span data-ttu-id="b6cf6-222">コースのチェック ボックスが選択されましたが、コースがにないかどうか、`Instructor.CourseAssignments`ナビゲーション プロパティ、コースはナビゲーション プロパティで、コレクションに追加します。</span><span class="sxs-lookup"><span data-stu-id="b6cf6-222">If the check box for a course was selected but the course isn't in the `Instructor.CourseAssignments` navigation property, the course is added to the collection in the navigation property.</span></span>

<span data-ttu-id="b6cf6-223">[!code-csharp[Main](intro/samples/cu/Controllers/InstructorsController.cs?highlight=14-20&name=snippet_UpdateCourses)]</span><span class="sxs-lookup"><span data-stu-id="b6cf6-223">[!code-csharp[Main](intro/samples/cu/Controllers/InstructorsController.cs?highlight=14-20&name=snippet_UpdateCourses)]</span></span>

<span data-ttu-id="b6cf6-224">コースのチェック ボックスが選択されますが、コースは場合、`Instructor.CourseAssignments`コースのナビゲーション プロパティは、ナビゲーション プロパティから削除します。</span><span class="sxs-lookup"><span data-stu-id="b6cf6-224">If the check box for a course wasn't selected, but the course is in the `Instructor.CourseAssignments` navigation property, the course is removed from the navigation property.</span></span>

<span data-ttu-id="b6cf6-225">[!code-csharp[Main](intro/samples/cu/Controllers/InstructorsController.cs?highlight=21-29&name=snippet_UpdateCourses)]</span><span class="sxs-lookup"><span data-stu-id="b6cf6-225">[!code-csharp[Main](intro/samples/cu/Controllers/InstructorsController.cs?highlight=21-29&name=snippet_UpdateCourses)]</span></span>

### <a name="update-the-instructor-views"></a><span data-ttu-id="b6cf6-226">講師ビューを更新します。</span><span class="sxs-lookup"><span data-stu-id="b6cf6-226">Update the Instructor views</span></span>

<span data-ttu-id="b6cf6-227">*Views/Instructors/Edit.cshtml*、追加、**コース**フィールドのチェック ボックスを次を追加することで配列にコードの直後に、`div`用の要素、 **Office**フィールドとの前に、`div`要素を**保存**ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="b6cf6-227">In *Views/Instructors/Edit.cshtml*, add a **Courses** field with an array of check boxes by adding the following code immediately after the `div` elements for the **Office** field and before the `div` element for the **Save** button.</span></span>

<a id="notepad"></a>
> [!NOTE] 
> <span data-ttu-id="b6cf6-228">Visual Studio でコードを貼り付けるときに、改行は、コードを中断するように変更されます。</span><span class="sxs-lookup"><span data-stu-id="b6cf6-228">When you paste the code in Visual Studio, line breaks will be changed in a way that breaks the code.</span></span>  <span data-ttu-id="b6cf6-229">Ctrl + Z を 1 回押して、オート フォーマットを元に戻します。</span><span class="sxs-lookup"><span data-stu-id="b6cf6-229">Press Ctrl+Z one time to undo the automatic formatting.</span></span>  <span data-ttu-id="b6cf6-230">ここで分かるように表示されるよう、改行は解決します。</span><span class="sxs-lookup"><span data-stu-id="b6cf6-230">This will fix the line breaks so that they look like what you see here.</span></span> <span data-ttu-id="b6cf6-231">インデント完璧なのに、する必要はありませんが、 `@</tr><tr>`、 `@:<td>`、 `@:</td>`、および`@:</tr>`行ことはできません。 1 行に示すように、または実行時エラーが表示されます。</span><span class="sxs-lookup"><span data-stu-id="b6cf6-231">The indentation doesn't have to be perfect, but the `@</tr><tr>`, `@:<td>`, `@:</td>`, and `@:</tr>` lines must each be on a single line as shown or you'll get a runtime error.</span></span> <span data-ttu-id="b6cf6-232">選択された新しいコードのブロックして、Tab キーを押して 3 回、新しいコードと既存のコードの行にします。</span><span class="sxs-lookup"><span data-stu-id="b6cf6-232">With the block of new code selected, press Tab three times to line up the new code with the existing code.</span></span>

<span data-ttu-id="b6cf6-233">[!code-html[Main](intro/samples/cu/Views/Instructors/Edit.cshtml?range=35-61)]</span><span class="sxs-lookup"><span data-stu-id="b6cf6-233">[!code-html[Main](intro/samples/cu/Views/Instructors/Edit.cshtml?range=35-61)]</span></span>

<span data-ttu-id="b6cf6-234">このコードでは、次の 3 つの列を含んでいる HTML テーブルを作成します。</span><span class="sxs-lookup"><span data-stu-id="b6cf6-234">This code creates an HTML table that has three columns.</span></span> <span data-ttu-id="b6cf6-235">各列ではコースの番号とタイトルから構成されるキャプションを続けて チェック ボックスです。</span><span class="sxs-lookup"><span data-stu-id="b6cf6-235">In each column is a check box followed by a caption that consists of the course number and title.</span></span> <span data-ttu-id="b6cf6-236">すべてのチェック ボックスをグループとして扱う場合にモデル バインダーを通知する同じ名前 ("selectedCourses") であります。</span><span class="sxs-lookup"><span data-stu-id="b6cf6-236">The check boxes all have the same name ("selectedCourses"), which informs the model binder that they are to be treated as a group.</span></span> <span data-ttu-id="b6cf6-237">各チェック ボックスの値の属性がの値に設定`CourseID`です。</span><span class="sxs-lookup"><span data-stu-id="b6cf6-237">The value attribute of each check box is set to the value of `CourseID`.</span></span> <span data-ttu-id="b6cf6-238">モデル バインダーがコント ローラーで構成される配列を渡しますページがポストされるときに、`CourseID`のチェック ボックスが選択されている値。</span><span class="sxs-lookup"><span data-stu-id="b6cf6-238">When the page is posted, the model binder passes an array to the controller that consists of the `CourseID` values for only the check boxes which are selected.</span></span>

<span data-ttu-id="b6cf6-239">チェック ボックスが最初に表示されると、適合インストラクターに割り当てられているコースのチェックが属性、選択を (それらのチェックが表示される) にあります。</span><span class="sxs-lookup"><span data-stu-id="b6cf6-239">When the check boxes are initially rendered, those that are for courses assigned to the instructor have checked attributes, which selects them (displays them checked).</span></span>

<span data-ttu-id="b6cf6-240">インストラクター インデックス ページを実行し、をクリックして**編集**、インストラクターを表示するには**編集**ページ。</span><span class="sxs-lookup"><span data-stu-id="b6cf6-240">Run the Instructor Index page, and click **Edit** on an instructor to see the **Edit** page.</span></span>

![コースをインストラクターの編集 ページ](update-related-data/_static/instructor-edit-courses.png)

<span data-ttu-id="b6cf6-242">一部のコース割り当てを変更し、[保存] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="b6cf6-242">Change some course assignments and click Save.</span></span> <span data-ttu-id="b6cf6-243">インデックス ページには、加えた変更が反映されます。</span><span class="sxs-lookup"><span data-stu-id="b6cf6-243">The changes you make are reflected on the Index page.</span></span>

> [!NOTE] 
> <span data-ttu-id="b6cf6-244">講師コースのデータを編集するのには、ここに採用されているアプローチは、コースの数に制限がある場合にも動作します。</span><span class="sxs-lookup"><span data-stu-id="b6cf6-244">The approach taken here to edit instructor course data works well when there is a limited number of courses.</span></span> <span data-ttu-id="b6cf6-245">非常に大きいコレクションを別の UI と更新の別の方法が必要になります。</span><span class="sxs-lookup"><span data-stu-id="b6cf6-245">For collections that are much larger, a different UI and a different updating method would be required.</span></span>

## <a name="update-the-delete-page"></a><span data-ttu-id="b6cf6-246">更新プログラムの削除 ページ</span><span class="sxs-lookup"><span data-stu-id="b6cf6-246">Update the Delete page</span></span>

<span data-ttu-id="b6cf6-247">*InstructorsController.cs*、削除、`DeleteConfirmed`代わりに、次のコードにメソッドおよび挿入します。</span><span class="sxs-lookup"><span data-stu-id="b6cf6-247">In *InstructorsController.cs*, delete the `DeleteConfirmed` method and insert the following code in its place.</span></span>

<span data-ttu-id="b6cf6-248">[!code-csharp[Main](intro/samples/cu/Controllers/InstructorsController.cs?highlight=5-7,9-12&name=snippet_DeleteConfirmed)]</span><span class="sxs-lookup"><span data-stu-id="b6cf6-248">[!code-csharp[Main](intro/samples/cu/Controllers/InstructorsController.cs?highlight=5-7,9-12&name=snippet_DeleteConfirmed)]</span></span>

<span data-ttu-id="b6cf6-249">このコードは、次の変更を加えます。</span><span class="sxs-lookup"><span data-stu-id="b6cf6-249">This code makes the following changes:</span></span>

* <span data-ttu-id="b6cf6-250">読み込みが eager、`CourseAssignments`ナビゲーション プロパティ。</span><span class="sxs-lookup"><span data-stu-id="b6cf6-250">Does eager loading for the `CourseAssignments` navigation property.</span></span>  <span data-ttu-id="b6cf6-251">これを含めることも EF 認識しないので関連`CourseAssignment`エンティティし、削除されません。</span><span class="sxs-lookup"><span data-stu-id="b6cf6-251">You have to include this or EF won't know about related `CourseAssignment` entities and won't delete them.</span></span>  <span data-ttu-id="b6cf6-252">通すしなくても済むようにここでする可能性があります連鎖削除データベースを構成します。</span><span class="sxs-lookup"><span data-stu-id="b6cf6-252">To avoid needing to read them here you could configure cascade delete in the database.</span></span>

* <span data-ttu-id="b6cf6-253">講師が削除されますが、部門の管理者として割り当てられている場合は、その部門からインストラクター割り当てを削除します。</span><span class="sxs-lookup"><span data-stu-id="b6cf6-253">If the instructor to be deleted is assigned as administrator of any departments, removes the instructor assignment from those departments.</span></span>

## <a name="add-office-location-and-courses-to-the-create-page"></a><span data-ttu-id="b6cf6-254">オフィスの場所およびコースを作成 ページに追加します。</span><span class="sxs-lookup"><span data-stu-id="b6cf6-254">Add office location and courses to the Create page</span></span>

<span data-ttu-id="b6cf6-255">*InstructorsController.cs*、HttpPost、HttpGet を削除`Create`メソッド、代わりに、次のコードを追加します。</span><span class="sxs-lookup"><span data-stu-id="b6cf6-255">In *InstructorsController.cs*, delete the HttpGet and HttpPost `Create` methods, and then add the following code in their place:</span></span>

<span data-ttu-id="b6cf6-256">[!code-csharp[Main](intro/samples/cu/Controllers/InstructorsController.cs?name=snippet_Create&highlight=3-5,12,14-22,29)]</span><span class="sxs-lookup"><span data-stu-id="b6cf6-256">[!code-csharp[Main](intro/samples/cu/Controllers/InstructorsController.cs?name=snippet_Create&highlight=3-5,12,14-22,29)]</span></span>

<span data-ttu-id="b6cf6-257">このコードはの表示に似ています、`Edit`コースは最初にありません以外の方法を選択します。</span><span class="sxs-lookup"><span data-stu-id="b6cf6-257">This code is similar to what you saw for the `Edit` methods except that initially no courses are selected.</span></span> <span data-ttu-id="b6cf6-258">HttpGet`Create`メソッドの呼び出し、`PopulateAssignedCourseData`メソッド コースが選択されている場合がある可能性がありますのでない注文の空のコレクションを提供する、 `foreach` (それ以外の場合、コードの表示は、例外をスロー null 参照)、ビューでループします。</span><span class="sxs-lookup"><span data-stu-id="b6cf6-258">The HttpGet `Create` method calls the `PopulateAssignedCourseData` method not because there might be courses selected but in order to provide an empty collection for the `foreach` loop in the view (otherwise the view code would throw a null reference exception).</span></span>

<span data-ttu-id="b6cf6-259">HttpPost`Create`メソッドを選択した各コースは追加、`CourseAssignments`ナビゲーション プロパティの検証エラーをチェックして、データベースに新しいインストラクターを追加する前にします。</span><span class="sxs-lookup"><span data-stu-id="b6cf6-259">The HttpPost `Create` method adds each selected course to the `CourseAssignments` navigation property before it checks for validation errors and adds the new instructor to the database.</span></span> <span data-ttu-id="b6cf6-260">行ったコース選択内容を自動的に復元 (例については、無効な日付をキーとしたユーザー)、モデル エラーがあるし、エラー メッセージで、ページが表示され、モデル エラーがある場合でも、コースが追加されます。</span><span class="sxs-lookup"><span data-stu-id="b6cf6-260">Courses are added even if there are model errors so that when there are model errors (for an example, the user keyed an invalid date), and the page is redisplayed with an error message, any course selections that were made are automatically restored.</span></span>

<span data-ttu-id="b6cf6-261">コースを追加できるようにすることを確認、`CourseAssignments`ナビゲーション プロパティが空のコレクションとしてプロパティを初期化する必要があります。</span><span class="sxs-lookup"><span data-stu-id="b6cf6-261">Notice that in order to be able to add courses to the `CourseAssignments` navigation property you have to initialize the property as an empty collection:</span></span>

```csharp
instructor.CourseAssignments = new List<CourseAssignment>();
```

<span data-ttu-id="b6cf6-262">コント ローラーのコードでこれを行う代わりに、としてでしたで行うこと、インストラクター モデルを自動的に作成、コレクションが存在しない場合、次の例に示すようにプロパティ get アクセス操作子を変更することで。</span><span class="sxs-lookup"><span data-stu-id="b6cf6-262">As an alternative to doing this in controller code, you could do it in the Instructor model by changing the property getter to automatically create the collection if it doesn't exist, as shown in the following example:</span></span>

```csharp
private ICollection<CourseAssignment> _courseAssignments;
public ICollection<CourseAssignment> CourseAssignments
{
    get
    {
        return _courseAssignments ?? (_courseAssignments = new List<CourseAssignment>());
    }
    set
    {
        _courseAssignments = value;
    }
}
```

<span data-ttu-id="b6cf6-263">変更する場合、`CourseAssignments`プロパティこの方法では、コント ローラーの明示的なプロパティの初期化コードを削除することができます。</span><span class="sxs-lookup"><span data-stu-id="b6cf6-263">If you modify the `CourseAssignments` property in this way, you can remove the explicit property initialization code in the controller.</span></span>

<span data-ttu-id="b6cf6-264">*Views/Instructor/Create.cshtml*オフィスの場所テキスト ボックスを追加、および送信ボタンの前にコースのチェック ボックスをします。</span><span class="sxs-lookup"><span data-stu-id="b6cf6-264">In *Views/Instructor/Create.cshtml*, add an office location text box and check boxes for courses before the Submit button.</span></span> <span data-ttu-id="b6cf6-265">編集ページの場合、[貼り付けをすると、Visual Studio が、コードを再フォーマットする場合、書式設定を修正](#notepad)です。</span><span class="sxs-lookup"><span data-stu-id="b6cf6-265">As in the case of the Edit page, [fix the formatting if Visual Studio reformats the code when you paste it](#notepad).</span></span>

<span data-ttu-id="b6cf6-266">[!code-html[Main](intro/samples/cu/Views/Instructors/Create.cshtml?range=29-61)]</span><span class="sxs-lookup"><span data-stu-id="b6cf6-266">[!code-html[Main](intro/samples/cu/Views/Instructors/Create.cshtml?range=29-61)]</span></span>

<span data-ttu-id="b6cf6-267">テストを実行して、**作成**ページと、インストラクターを追加します。</span><span class="sxs-lookup"><span data-stu-id="b6cf6-267">Test by running the **Create** page and adding an instructor.</span></span> 

## <a name="handling-transactions"></a><span data-ttu-id="b6cf6-268">トランザクションの処理</span><span class="sxs-lookup"><span data-stu-id="b6cf6-268">Handling Transactions</span></span>

<span data-ttu-id="b6cf6-269">説明に従って、 [CRUD チュートリアル](crud.md)、Entity Framework は、トランザクションを暗黙的に実装します。</span><span class="sxs-lookup"><span data-stu-id="b6cf6-269">As explained in the [CRUD tutorial](crud.md), the Entity Framework implicitly implements transactions.</span></span> <span data-ttu-id="b6cf6-270">必要な複数を制御する--など--トランザクションでは Entity Framework の外部で実行する操作を追加する場合のシナリオを参照してください[トランザクション](https://docs.microsoft.com/ef/core/saving/transactions)です。</span><span class="sxs-lookup"><span data-stu-id="b6cf6-270">For scenarios where you need more control -- for example, if you want to include operations done outside of Entity Framework in a transaction -- see [Transactions](https://docs.microsoft.com/ef/core/saving/transactions).</span></span>

## <a name="summary"></a><span data-ttu-id="b6cf6-271">概要</span><span class="sxs-lookup"><span data-stu-id="b6cf6-271">Summary</span></span>

<span data-ttu-id="b6cf6-272">関連するデータの操作の概要が完了しました。</span><span class="sxs-lookup"><span data-stu-id="b6cf6-272">You have now completed the introduction to working with related data.</span></span> <span data-ttu-id="b6cf6-273">次のチュートリアルでは、同時実行の競合を処理する方法が表示されます。</span><span class="sxs-lookup"><span data-stu-id="b6cf6-273">In the next tutorial you'll see how to handle concurrency conflicts.</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="b6cf6-274">[前へ](read-related-data.md)
[次へ](concurrency.md)</span><span class="sxs-lookup"><span data-stu-id="b6cf6-274">[Previous](read-related-data.md)
[Next](concurrency.md)</span></span>  