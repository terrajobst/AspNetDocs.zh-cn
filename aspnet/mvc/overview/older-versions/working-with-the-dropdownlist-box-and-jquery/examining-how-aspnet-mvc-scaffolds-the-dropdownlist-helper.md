---
uid: mvc/overview/older-versions/working-with-the-dropdownlist-box-and-jquery/examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper
title: 检查 ASP.NET MVC 如何基架 DropDownList 帮助器 |Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 01/12/2012
ms.assetid: 8921d7f2-21f0-427a-8b27-2df7251174b0
msc.legacyurl: /mvc/overview/older-versions/working-with-the-dropdownlist-box-and-jquery/examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper
msc.type: authoredcontent
ms.openlocfilehash: 275b20ad964b3e8ddc272a7448f0740ed0891eff
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78498356"
---
# <a name="examining--how--aspnet-mvc-scaffolds-the-dropdownlist-helper"></a><span data-ttu-id="b3050-102">检查 ASP.NET MVC 如何支持 DropDownList 帮助程序</span><span class="sxs-lookup"><span data-stu-id="b3050-102">Examining  how  ASP.NET MVC scaffolds the DropDownList Helper</span></span>

<span data-ttu-id="b3050-103">作者： [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="b3050-103">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="b3050-104">在**解决方案资源管理器**中，右键单击 "*控制器*" 文件夹，然后选择 "**添加控制器**"。</span><span class="sxs-lookup"><span data-stu-id="b3050-104">In **Solution Explorer**, right-click the *Controllers* folder and then select **Add Controller**.</span></span> <span data-ttu-id="b3050-105">将控制器命名为**StoreManagerController**。</span><span class="sxs-lookup"><span data-stu-id="b3050-105">Name the controller **StoreManagerController**.</span></span> <span data-ttu-id="b3050-106">设置 "**添加控制器**" 对话框的选项，如下图所示。</span><span class="sxs-lookup"><span data-stu-id="b3050-106">Set the options for the **Add Controller** dialog as shown in the image below.</span></span>

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image1.png)

<span data-ttu-id="b3050-107">编辑*StoreManager\Index.cshtml*视图并删除 `AlbumArtUrl`。</span><span class="sxs-lookup"><span data-stu-id="b3050-107">Edit the *StoreManager\Index.cshtml* view and remove `AlbumArtUrl`.</span></span> <span data-ttu-id="b3050-108">删除 `AlbumArtUrl` 将使演示更具可读性。</span><span class="sxs-lookup"><span data-stu-id="b3050-108">Removing `AlbumArtUrl` will make the presentation more readable.</span></span> <span data-ttu-id="b3050-109">完成的代码如下所示。</span><span class="sxs-lookup"><span data-stu-id="b3050-109">The completed code is shown below.</span></span>

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample1.cshtml)]

<span data-ttu-id="b3050-110">打开*Controllers\StoreManagerController.cs*文件并找到 `Index` 方法。</span><span class="sxs-lookup"><span data-stu-id="b3050-110">Open the *Controllers\StoreManagerController.cs* file and find the `Index` method.</span></span> <span data-ttu-id="b3050-111">添加 `OrderBy` 子句以便按价格对唱片集排序。</span><span class="sxs-lookup"><span data-stu-id="b3050-111">Add the `OrderBy` clause so the albums will be sorted by price.</span></span> <span data-ttu-id="b3050-112">完整的代码如下所示。</span><span class="sxs-lookup"><span data-stu-id="b3050-112">The complete code is shown below.</span></span>

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample2.cs)]

<span data-ttu-id="b3050-113">按价格排序会使测试数据库更改变得更加容易。</span><span class="sxs-lookup"><span data-stu-id="b3050-113">Sorting by price will make it easier to test changes to the database.</span></span> <span data-ttu-id="b3050-114">在测试 "编辑" 和 "创建" 方法时，可以使用低价位，因此保存的数据将首先显示。</span><span class="sxs-lookup"><span data-stu-id="b3050-114">When you are testing the edit and create methods, you can use a low price so the saved data will appear first.</span></span>

<span data-ttu-id="b3050-115">打开*StoreManager\Edit.cshtml*文件。</span><span class="sxs-lookup"><span data-stu-id="b3050-115">Open the *StoreManager\Edit.cshtml* file.</span></span> <span data-ttu-id="b3050-116">在图例标记后面添加以下行。</span><span class="sxs-lookup"><span data-stu-id="b3050-116">Add the following line just after the legend tag.</span></span>

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample3.cshtml)]

<span data-ttu-id="b3050-117">下面的代码显示了此更改的上下文：</span><span class="sxs-lookup"><span data-stu-id="b3050-117">The following code shows the context of this change:</span></span>

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample4.cshtml)]

<span data-ttu-id="b3050-118">需要 `AlbumId` 才能对唱片集记录进行更改。</span><span class="sxs-lookup"><span data-stu-id="b3050-118">The `AlbumId` is required to make changes to an album record.</span></span>

<span data-ttu-id="b3050-119">按 Ctrl+F5 以运行应用程序。</span><span class="sxs-lookup"><span data-stu-id="b3050-119">Press CTRL+F5 to run the application.</span></span> <span data-ttu-id="b3050-120">选择 "**管理**" 链接，然后选择 "**新建" 链接**创建新的唱片集。</span><span class="sxs-lookup"><span data-stu-id="b3050-120">Select to the **Admin** link, then select the **Create New** link to create a new album.</span></span> <span data-ttu-id="b3050-121">验证唱片集信息已保存。</span><span class="sxs-lookup"><span data-stu-id="b3050-121">Verify the album information was saved.</span></span> <span data-ttu-id="b3050-122">编辑唱片集并验证所做的更改是否已保存。</span><span class="sxs-lookup"><span data-stu-id="b3050-122">Edit an album and verify the changes you made are persisted.</span></span>

### <a name="the-album-schema"></a><span data-ttu-id="b3050-123">唱片集架构</span><span class="sxs-lookup"><span data-stu-id="b3050-123">The Album Schema</span></span>

<span data-ttu-id="b3050-124">MVC 基架机制创建的 `StoreManager` 控制器允许对音乐存储数据库中的唱集进行 CRUD （创建、读取、更新、删除）访问。</span><span class="sxs-lookup"><span data-stu-id="b3050-124">The `StoreManager` controller created by the MVC scaffolding mechanism allows CRUD (Create, Read, Update, Delete) access to the albums in the music store database.</span></span> <span data-ttu-id="b3050-125">唱片集信息的架构如下所示：</span><span class="sxs-lookup"><span data-stu-id="b3050-125">The schema for album information is shown below:</span></span>

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image2.png)

<span data-ttu-id="b3050-126">`Albums` 表未存储唱片集流派和说明，它将外键存储到 `Genres` 表。</span><span class="sxs-lookup"><span data-stu-id="b3050-126">The `Albums` table does not store the album genre and description, it stores a foreign key to the `Genres` table.</span></span> <span data-ttu-id="b3050-127">`Genres` 表包含流派名称和说明。</span><span class="sxs-lookup"><span data-stu-id="b3050-127">The `Genres` table contains the genre name and description.</span></span> <span data-ttu-id="b3050-128">同样，`Albums` 表不包含唱片集艺术家名称，而是 `Artists` 表的外键。</span><span class="sxs-lookup"><span data-stu-id="b3050-128">Likewise, the `Albums` table doesn't contain the album artists name, but a foreign key to the `Artists` table.</span></span> <span data-ttu-id="b3050-129">`Artists` 表包含艺术家的姓名。</span><span class="sxs-lookup"><span data-stu-id="b3050-129">The `Artists` table contains the artist's name.</span></span> <span data-ttu-id="b3050-130">如果检查 `Albums` 表中的数据，则可以看到每一行都包含 `Genres` 表的外键和 `Artists` 表的外键。</span><span class="sxs-lookup"><span data-stu-id="b3050-130">If you examine the data in the `Albums` table, you can see each row contains a foreign key to the `Genres` table and a foreign key to the `Artists` table.</span></span> <span data-ttu-id="b3050-131">下图显示了 `Albums` 表中的一些表数据。</span><span class="sxs-lookup"><span data-stu-id="b3050-131">The image below show some table data from the `Albums` table.</span></span>

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image3.png)

### <a name="the-html-select-tag"></a><span data-ttu-id="b3050-132">HTML 选择标记</span><span class="sxs-lookup"><span data-stu-id="b3050-132">The HTML Select Tag</span></span>

<span data-ttu-id="b3050-133">HTML `<select>` 元素（由 HTML [DropDownList](https://msdn.microsoft.com/library/dd492948.aspx) helper 创建）用于显示值的完整列表（例如，流派列表）。</span><span class="sxs-lookup"><span data-stu-id="b3050-133">The HTML `<select>` element (created by the HTML [DropDownList](https://msdn.microsoft.com/library/dd492948.aspx) helper) is used to display a complete list of values (such as the list of genres).</span></span> <span data-ttu-id="b3050-134">对于编辑窗体，当当前值已知时，选择列表可以显示当前值。</span><span class="sxs-lookup"><span data-stu-id="b3050-134">For edit forms, when the current value is known, the select list can display the current value.</span></span> <span data-ttu-id="b3050-135">当我们将选定值设置为**喜剧**时，我们看到了这一点。</span><span class="sxs-lookup"><span data-stu-id="b3050-135">We saw this previously when we set the selected value to **Comedy**.</span></span> <span data-ttu-id="b3050-136">选择列表是显示类别或外键数据的理想选择。</span><span class="sxs-lookup"><span data-stu-id="b3050-136">The select list is ideal for displaying category or foreign key data.</span></span> <span data-ttu-id="b3050-137">流派外键的 `<select>` 元素显示了可能的流派名称的列表，但当您保存窗体时，将用流派外键值而不是显示的流派名称更新 "流派" 属性。</span><span class="sxs-lookup"><span data-stu-id="b3050-137">The `<select>` element for the Genre foreign key displays the list of possible genre names, but when you save the form the Genre property is updated with the Genre foreign key value, not the displayed genre name.</span></span> <span data-ttu-id="b3050-138">在下图中，所选的流派为**Disco** ，并且艺术家为**Donna 夏令时**。</span><span class="sxs-lookup"><span data-stu-id="b3050-138">In the image below, the genre selected is **Disco** and the artist is **Donna Summer**.</span></span>

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image4.png)

### <a name="examining-the-aspnet-mvc-scaffolded-code"></a><span data-ttu-id="b3050-139">检查 ASP.NET MVC 基架代码</span><span class="sxs-lookup"><span data-stu-id="b3050-139">Examining the ASP.NET MVC Scaffolded Code</span></span>

<span data-ttu-id="b3050-140">打开*Controllers\StoreManagerController.cs*文件并找到 `HTTP GET Create` 方法。</span><span class="sxs-lookup"><span data-stu-id="b3050-140">Open the *Controllers\StoreManagerController.cs* file and find the `HTTP GET Create` method.</span></span>

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample5.cs)]

<span data-ttu-id="b3050-141">`Create` 方法将两个[SelectList](https://msdn.microsoft.com/library/system.web.mvc.selectlist.aspx)对象添加到 `ViewBag`，一个对象包含流派信息，另一个用于包含艺术家信息。</span><span class="sxs-lookup"><span data-stu-id="b3050-141">The `Create` method adds two [SelectList](https://msdn.microsoft.com/library/system.web.mvc.selectlist.aspx) objects to the `ViewBag`, one to contain the genre information, and one to contain the artist information.</span></span> <span data-ttu-id="b3050-142">上面使用的[SelectList](https://msdn.microsoft.com/library/dd505286.aspx)构造函数重载采用三个参数：</span><span class="sxs-lookup"><span data-stu-id="b3050-142">The [SelectList](https://msdn.microsoft.com/library/dd505286.aspx) constructor overload used above takes three arguments:</span></span>

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample6.cs)]

1. <span data-ttu-id="b3050-143">*项*：一个[IEnumerable](https://msdn.microsoft.com/library/system.collections.ienumerable.aspx) ，其中包含列表中的项。</span><span class="sxs-lookup"><span data-stu-id="b3050-143">*items*: An [IEnumerable](https://msdn.microsoft.com/library/system.collections.ienumerable.aspx) containing the items in the list.</span></span> <span data-ttu-id="b3050-144">在上面的示例中，`db.Genres`返回的流派列表。</span><span class="sxs-lookup"><span data-stu-id="b3050-144">In the example above, the list of genres returned by `db.Genres`.</span></span>
2. <span data-ttu-id="b3050-145">*dataValueField*：包含密钥值的**IEnumerable**列表中属性的名称。</span><span class="sxs-lookup"><span data-stu-id="b3050-145">*dataValueField*: The name of the property in the **IEnumerable** list that contains the key value.</span></span> <span data-ttu-id="b3050-146">在上面的示例中，`GenreId` 和 `ArtistId`。</span><span class="sxs-lookup"><span data-stu-id="b3050-146">In the example above, `GenreId` and `ArtistId`.</span></span>
3. <span data-ttu-id="b3050-147">*dataTextField*： **IEnumerable**列表中包含要显示的信息的属性的名称。</span><span class="sxs-lookup"><span data-stu-id="b3050-147">*dataTextField*: The name of the property in the **IEnumerable** list that contains the information to display.</span></span> <span data-ttu-id="b3050-148">在 "艺术家" 和 "流派" 表中，将使用 "`name`" 字段。</span><span class="sxs-lookup"><span data-stu-id="b3050-148">In both the artists and genre table, the `name` field is used.</span></span>

<span data-ttu-id="b3050-149">打开*Views\StoreManager\Create.cshtml*文件并检查 "流派" 字段的 `Html.DropDownList` 帮助程序标记。</span><span class="sxs-lookup"><span data-stu-id="b3050-149">Open the *Views\StoreManager\Create.cshtml* file and examine the `Html.DropDownList` helper markup for the genre field.</span></span>

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample7.cshtml)]

<span data-ttu-id="b3050-150">第一行显示 "创建" 视图采用 `Album` 模型。</span><span class="sxs-lookup"><span data-stu-id="b3050-150">The first line shows that the create view takes an `Album` model.</span></span> <span data-ttu-id="b3050-151">在上面所示的 `Create` 方法中，未传递任何模型，因此视图将获取**null** `Album` 模型。</span><span class="sxs-lookup"><span data-stu-id="b3050-151">In the `Create` method shown above, no model was passed, so the view gets a **null** `Album` model.</span></span> <span data-ttu-id="b3050-152">此时，我们将创建一个新的唱片集，因此没有任何 `Album` 数据。</span><span class="sxs-lookup"><span data-stu-id="b3050-152">At this point we are creating a new album so we don't have any `Album` data for it.</span></span>

<span data-ttu-id="b3050-153">上面所示的[DropDownList](https://msdn.microsoft.com/library/dd492948.aspx)重载使用字段的名称来绑定到模型。</span><span class="sxs-lookup"><span data-stu-id="b3050-153">The [Html.DropDownList](https://msdn.microsoft.com/library/dd492948.aspx) overload shown above takes the name of the field to bind to the model.</span></span> <span data-ttu-id="b3050-154">它还使用此名称来查找包含[SelectList](https://msdn.microsoft.com/library/dd505286.aspx)对象的**ViewBag**对象。</span><span class="sxs-lookup"><span data-stu-id="b3050-154">It also uses this name to look for a **ViewBag** object containing a [SelectList](https://msdn.microsoft.com/library/dd505286.aspx) object.</span></span> <span data-ttu-id="b3050-155">如果使用此重载，则需要将**ViewBag SelectList**对象命名 `GenreId`。</span><span class="sxs-lookup"><span data-stu-id="b3050-155">Using this overload, you are required to name the **ViewBag SelectList** object `GenreId`.</span></span> <span data-ttu-id="b3050-156">第二个参数（`String.Empty`）是在没有选中任何项时要显示的文本。</span><span class="sxs-lookup"><span data-stu-id="b3050-156">The second parameter (`String.Empty`) is the text to display when no item is selected.</span></span> <span data-ttu-id="b3050-157">这正是我们在创建新唱片集时所希望的。</span><span class="sxs-lookup"><span data-stu-id="b3050-157">This is exactly what we want when creating a new album.</span></span> <span data-ttu-id="b3050-158">如果删除了第二个参数，并使用了以下代码：</span><span class="sxs-lookup"><span data-stu-id="b3050-158">If you removed the second parameter and used the following code:</span></span>

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample8.cshtml)]

<span data-ttu-id="b3050-159">选择列表将默认为示例中的第一个元素或摇滚。</span><span class="sxs-lookup"><span data-stu-id="b3050-159">The select list would default to the first element, or Rock in our sample.</span></span>

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image5.png)

<span data-ttu-id="b3050-160">检查 `HTTP POST Create` 方法。</span><span class="sxs-lookup"><span data-stu-id="b3050-160">Examining the `HTTP POST Create` method.</span></span>

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample9.cs)]

<span data-ttu-id="b3050-161">`Create` 方法的此重载采用 `album` 对象，该对象由发布的窗体值创建的 ASP.NET MVC 模型绑定系统。</span><span class="sxs-lookup"><span data-stu-id="b3050-161">This overload of the `Create` method takes an `album` object, created by the ASP.NET MVC model binding system from the form values posted.</span></span> <span data-ttu-id="b3050-162">提交新的唱片集时，如果模型状态有效并且没有数据库错误，则会将该新的唱片集添加到该数据库中。</span><span class="sxs-lookup"><span data-stu-id="b3050-162">When you submit a new album, if model state is valid and there are no database errors, the new album is added the database.</span></span> <span data-ttu-id="b3050-163">下图显示了如何创建新的唱片集。</span><span class="sxs-lookup"><span data-stu-id="b3050-163">The following image shows the creation of a new album.</span></span>

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image6.png)

<span data-ttu-id="b3050-164">您可以使用[fiddler 工具](http://www.fiddler2.com/fiddler2/)来检查 ASP.NET MVC 模型绑定用来创建唱片集对象的已发布的窗体值。</span><span class="sxs-lookup"><span data-stu-id="b3050-164">You can use the [fiddler tool](http://www.fiddler2.com/fiddler2/) to examine the posted form values that ASP.NET MVC model binding uses to create the album object.</span></span>

<span data-ttu-id="b3050-165">![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image7.png)。</span><span class="sxs-lookup"><span data-stu-id="b3050-165">![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image7.png).</span></span>

### <a name="refactoring-the-viewbag-selectlist-creation"></a><span data-ttu-id="b3050-166">重构 ViewBag SelectList 创建</span><span class="sxs-lookup"><span data-stu-id="b3050-166">Refactoring the ViewBag SelectList Creation</span></span>

<span data-ttu-id="b3050-167">`Edit` 方法和 `HTTP POST Create` 方法都具有相同的代码，可以在**ViewBag**中设置**SelectList** 。</span><span class="sxs-lookup"><span data-stu-id="b3050-167">Both the `Edit` methods and the `HTTP POST Create` method have identical code to set up the **SelectList** in the **ViewBag**.</span></span> <span data-ttu-id="b3050-168">在[晾干](http://en.wikipedia.org/wiki/Don't_repeat_yourself)精神中，我们将重构此代码。</span><span class="sxs-lookup"><span data-stu-id="b3050-168">In the spirit of [DRY](http://en.wikipedia.org/wiki/Don't_repeat_yourself), we will refactor this code.</span></span> <span data-ttu-id="b3050-169">稍后我们将使用此重构代码。</span><span class="sxs-lookup"><span data-stu-id="b3050-169">We'll make use of this refactored code later.</span></span>

<span data-ttu-id="b3050-170">创建新方法，将流派和艺术家**SelectList**添加到**ViewBag**中。</span><span class="sxs-lookup"><span data-stu-id="b3050-170">Create a new method to add a genre and artist **SelectList** to the **ViewBag**.</span></span>

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample10.cs)]

<span data-ttu-id="b3050-171">使用对 `SetGenreArtistViewBag` 方法的调用，将每个 `Create` 和 `Edit` 方法中的 `ViewBag` 替换为两行。</span><span class="sxs-lookup"><span data-stu-id="b3050-171">Replace the two lines setting the `ViewBag` in each of the `Create` and `Edit` methods with a call to the `SetGenreArtistViewBag` method.</span></span> <span data-ttu-id="b3050-172">完成的代码如下所示。</span><span class="sxs-lookup"><span data-stu-id="b3050-172">The completed code is shown below.</span></span>

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample11.cs)]

<span data-ttu-id="b3050-173">创建新的唱片集并编辑唱片集来验证更改是否正常工作。</span><span class="sxs-lookup"><span data-stu-id="b3050-173">Create a new album and edit an album to verify the changes work.</span></span>

### <a name="explicitly-passing-the-selectlist-to-the-dropdownlist"></a><span data-ttu-id="b3050-174">将 SelectList 显式传递给 DropDownList</span><span class="sxs-lookup"><span data-stu-id="b3050-174">Explicitly Passing the SelectList to the DropDownList</span></span>

<span data-ttu-id="b3050-175">ASP.NET MVC 基架创建的创建和编辑视图使用以下**DropDownList**重载：</span><span class="sxs-lookup"><span data-stu-id="b3050-175">The create and edit views created by the ASP.NET MVC scaffolding use the following **DropDownList** overload:</span></span>

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample12.cs)]

<span data-ttu-id="b3050-176">"创建" 视图的 `DropDownList` 标记如下所示。</span><span class="sxs-lookup"><span data-stu-id="b3050-176">The `DropDownList` markup for the create view is shown below.</span></span>

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample13.cshtml)]

<span data-ttu-id="b3050-177">由于 `SelectList` 的 `ViewBag` 属性名为 `GenreId`， **DropDownList** helper 将使用**ViewBag**中的 `GenreId`**SelectList** 。</span><span class="sxs-lookup"><span data-stu-id="b3050-177">Because the `ViewBag` property for the `SelectList` is named `GenreId`, the **DropDownList** helper will use the `GenreId`**SelectList** in the **ViewBag**.</span></span> <span data-ttu-id="b3050-178">在以下**DropDownList**重载中，`SelectList` 显式传入。</span><span class="sxs-lookup"><span data-stu-id="b3050-178">In the following **DropDownList** overload, the `SelectList` is explicitly passed in.</span></span>

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample14.cs)]

<span data-ttu-id="b3050-179">打开*Views\StoreManager\Edit.cshtml*文件，并使用上面的重载更改**DropDownList**调用以显式传入**SelectList**。</span><span class="sxs-lookup"><span data-stu-id="b3050-179">Open the *Views\StoreManager\Edit.cshtml* file, and change the **DropDownList** call to explicitly pass in the **SelectList**, using the overload above.</span></span> <span data-ttu-id="b3050-180">为 "流派" 类别执行此操作。</span><span class="sxs-lookup"><span data-stu-id="b3050-180">Do this for the Genre category.</span></span> <span data-ttu-id="b3050-181">完成的代码如下所示：</span><span class="sxs-lookup"><span data-stu-id="b3050-181">The completed code is shown below:</span></span>

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample15.cshtml)]

<span data-ttu-id="b3050-182">运行应用程序，并单击 "**管理**" 链接，然后导航到 "爵士乐" 唱片集并选择 "**编辑**" 链接。</span><span class="sxs-lookup"><span data-stu-id="b3050-182">Run the application and click the **Admin** link, then navigate to a Jazz album and select the **Edit** link.</span></span>

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image8.png)

<span data-ttu-id="b3050-183">显示 "摇滚"，而不是显示与当前所选流派相同的爵士乐。</span><span class="sxs-lookup"><span data-stu-id="b3050-183">Instead of showing Jazz as the currently selected genre, Rock is displayed.</span></span> <span data-ttu-id="b3050-184">当字符串参数（要绑定的属性）和**SelectList**对象具有相同的名称时，不会使用所选值。</span><span class="sxs-lookup"><span data-stu-id="b3050-184">When the string argument (the property to bind) and the **SelectList** object have the same name, the selected value is not used.</span></span> <span data-ttu-id="b3050-185">如果未提供选定值，浏览器将默认为**SelectList**中的第一个元素（在上面的示例中为 "**摇滚**"）。</span><span class="sxs-lookup"><span data-stu-id="b3050-185">When there is no selected value provided, browsers default to the first element in the **SelectList**(which is **Rock** in the example above).</span></span> <span data-ttu-id="b3050-186">这是**DropDownList**帮助器的已知限制。</span><span class="sxs-lookup"><span data-stu-id="b3050-186">This is a known limitation of the **DropDownList** helper.</span></span>

<span data-ttu-id="b3050-187">打开*Controllers\StoreManagerController.cs*文件，并将**SelectList**对象名称更改为 `Genres` 和 `Artists`。</span><span class="sxs-lookup"><span data-stu-id="b3050-187">Open the *Controllers\StoreManagerController.cs* file and change the **SelectList** object names to `Genres` and `Artists`.</span></span> <span data-ttu-id="b3050-188">完成的代码如下所示：</span><span class="sxs-lookup"><span data-stu-id="b3050-188">The completed code is shown below:</span></span>

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample16.cs)]

<span data-ttu-id="b3050-189">名称流派和艺术家是类别的更好的名称，因为它们不仅包含每个类别的 ID。</span><span class="sxs-lookup"><span data-stu-id="b3050-189">The names Genres and Artists are better names for the categories, as they contain more than just the ID of each category.</span></span> <span data-ttu-id="b3050-190">之前已支付的重构。</span><span class="sxs-lookup"><span data-stu-id="b3050-190">The refactoring we did earlier paid off.</span></span> <span data-ttu-id="b3050-191">我们所做的更改与 `SetGenreArtistViewBag` 方法隔离，而不是以四种方法更改**ViewBag** 。</span><span class="sxs-lookup"><span data-stu-id="b3050-191">Instead of changing the **ViewBag** in four methods, our changes were isolated to the `SetGenreArtistViewBag` method.</span></span>

<span data-ttu-id="b3050-192">更改 "创建" 和 "编辑" 视图中的**DropDownList**调用，以使用新的**SelectList**名称。</span><span class="sxs-lookup"><span data-stu-id="b3050-192">Change the **DropDownList** call in the create and edit views to use the new **SelectList** names.</span></span> <span data-ttu-id="b3050-193">编辑视图的新标记如下所示：</span><span class="sxs-lookup"><span data-stu-id="b3050-193">The new markup for the edit view is shown below:</span></span>

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample17.cshtml)]

<span data-ttu-id="b3050-194">Create view 需要空字符串，以防止显示 SelectList 中的第一项。</span><span class="sxs-lookup"><span data-stu-id="b3050-194">The Create view requires an empty string to prevent the first item in the SelectList from being displayed.</span></span>

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample18.cshtml)]

<span data-ttu-id="b3050-195">创建新的唱片集并编辑唱片集来验证更改是否正常工作。</span><span class="sxs-lookup"><span data-stu-id="b3050-195">Create a new album and edit an album to verify the changes work.</span></span> <span data-ttu-id="b3050-196">通过选择一个具有 "摇滚" 流派的唱片集来测试编辑代码。</span><span class="sxs-lookup"><span data-stu-id="b3050-196">Test the edit code by selecting an album with a genre other than Rock.</span></span>

### <a name="using-a-view-model-with-the-dropdownlist-helper"></a><span data-ttu-id="b3050-197">将视图模型与 DropDownList Helper 一起使用</span><span class="sxs-lookup"><span data-stu-id="b3050-197">Using a View Model with the DropDownList Helper</span></span>

<span data-ttu-id="b3050-198">在名为 `AlbumSelectListViewModel`的 Viewmodel 文件夹中创建一个新类。</span><span class="sxs-lookup"><span data-stu-id="b3050-198">Create a new class in the ViewModels folder named `AlbumSelectListViewModel`.</span></span> <span data-ttu-id="b3050-199">将 `AlbumSelectListViewModel` 类中的代码替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="b3050-199">Replace the code in the `AlbumSelectListViewModel` class with the following:</span></span>

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample19.cs)]

<span data-ttu-id="b3050-200">`AlbumSelectListViewModel` 构造函数采用唱片集、艺术家和流派列表，并创建包含唱片集的对象和流派和艺术家的 `SelectList`。</span><span class="sxs-lookup"><span data-stu-id="b3050-200">The `AlbumSelectListViewModel` constructor takes an album, a list of artists and genres and creates an object containing the album and a `SelectList` for genres and artists.</span></span>

<span data-ttu-id="b3050-201">生成项目，以便在下一步中创建视图时，可以使用 `AlbumSelectListViewModel`。</span><span class="sxs-lookup"><span data-stu-id="b3050-201">Build the project so the `AlbumSelectListViewModel` is available when we create a view in the next step.</span></span>

<span data-ttu-id="b3050-202">向 `StoreManagerController`中添加 `EditVM` 方法。</span><span class="sxs-lookup"><span data-stu-id="b3050-202">Add an `EditVM` method to the `StoreManagerController`.</span></span> <span data-ttu-id="b3050-203">完成的代码如下所示。</span><span class="sxs-lookup"><span data-stu-id="b3050-203">The completed code is shown below.</span></span>

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample20.cs)]

<span data-ttu-id="b3050-204">右键单击 `AlbumSelectListViewModel`，选择 "**解析**"，然后**使用 viewmodel;** 。</span><span class="sxs-lookup"><span data-stu-id="b3050-204">Right click `AlbumSelectListViewModel`, select **Resolve**, then **using MvcMusicStore.ViewModels;**.</span></span>

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image9.png)

<span data-ttu-id="b3050-205">或者，您可以添加以下 using 语句：</span><span class="sxs-lookup"><span data-stu-id="b3050-205">Alternatively, you can add the following using statement:</span></span>

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample21.cs)]

<span data-ttu-id="b3050-206">右键单击 `EditVM`，然后选择 "**添加视图**"。</span><span class="sxs-lookup"><span data-stu-id="b3050-206">Right click `EditVM` and select **Add View**.</span></span> <span data-ttu-id="b3050-207">使用如下所示的选项。</span><span class="sxs-lookup"><span data-stu-id="b3050-207">Use the options shown below.</span></span>

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image10.png)

<span data-ttu-id="b3050-208">选择 "**添加**"，然后将*Views\StoreManager\EditVM.cshtml*文件的内容替换为以下内容：</span><span class="sxs-lookup"><span data-stu-id="b3050-208">Select **Add**, then replace the contents of the *Views\StoreManager\EditVM.cshtml* file with the following:</span></span>

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample22.cshtml)]

<span data-ttu-id="b3050-209">`EditVM` 标记与原始 `Edit` 标记非常相似，但有以下例外情况。</span><span class="sxs-lookup"><span data-stu-id="b3050-209">The `EditVM` markup is very similar to the original `Edit` markup with the following exceptions.</span></span>

- <span data-ttu-id="b3050-210">`Edit` 视图中的模型属性的格式为 `model.property`（例如 `model.Title`）。</span><span class="sxs-lookup"><span data-stu-id="b3050-210">Model properties in the `Edit` view are of the form `model.property`(for example, `model.Title` ).</span></span> <span data-ttu-id="b3050-211">`EditVm` 视图中的模型属性的格式为 `model.Album.property`（例如 `model.Album.Title`）。</span><span class="sxs-lookup"><span data-stu-id="b3050-211">Model properties in the `EditVm` view are of the form `model.Album.property`(for example, `model.Album.Title`).</span></span> <span data-ttu-id="b3050-212">这是因为 `EditVM` 视图向 `Album`传递了一个容器，而不是 `Edit` 视图中的 `Album`。</span><span class="sxs-lookup"><span data-stu-id="b3050-212">That's because the `EditVM` view is passed a container for an `Album`, not an `Album` as in the `Edit` view.</span></span>
- <span data-ttu-id="b3050-213">**DropDownList**第二个参数来自视图模型，而不是**ViewBag**。</span><span class="sxs-lookup"><span data-stu-id="b3050-213">The **DropDownList** second parameter comes from the view model, not the **ViewBag**.</span></span>
- <span data-ttu-id="b3050-214">`EditVM` 视图中的**html.beginform** helper 显式回发到 `Edit` 操作方法。</span><span class="sxs-lookup"><span data-stu-id="b3050-214">The **BeginForm** helper in the `EditVM` view explicitly posts back to the `Edit` action method.</span></span> <span data-ttu-id="b3050-215">通过回发到 `Edit` 操作，我们无需编写 `HTTP POST EditVM` 操作，并可重复使用 `HTTP POST` `Edit` 操作。</span><span class="sxs-lookup"><span data-stu-id="b3050-215">By posting back to the `Edit` action, we don't have to write an `HTTP POST EditVM` action and can reuse the `HTTP POST` `Edit` action.</span></span>

<span data-ttu-id="b3050-216">运行应用程序并编辑唱片集。</span><span class="sxs-lookup"><span data-stu-id="b3050-216">Run the application and edit an album.</span></span> <span data-ttu-id="b3050-217">更改 URL 以使用 `EditVM`。</span><span class="sxs-lookup"><span data-stu-id="b3050-217">Change the URL to use `EditVM`.</span></span> <span data-ttu-id="b3050-218">更改字段并单击 "**保存**" 按钮以验证代码是否正常工作。</span><span class="sxs-lookup"><span data-stu-id="b3050-218">Change a field and hit the **Save** button to verify the code is working.</span></span>

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image11.png)

### <a name="which-approach-should-you-use"></a><span data-ttu-id="b3050-219">应使用哪种方法？</span><span class="sxs-lookup"><span data-stu-id="b3050-219">Which Approach Should You Use?</span></span>

<span data-ttu-id="b3050-220">这三种方法都是可接受的。</span><span class="sxs-lookup"><span data-stu-id="b3050-220">All three approaches shown are acceptable.</span></span> <span data-ttu-id="b3050-221">许多开发人员更喜欢使用 `ViewBag`将 `SelectList` 显式传递到 `DropDownList` 中。</span><span class="sxs-lookup"><span data-stu-id="b3050-221">Many developers prefer to explicitly pass the `SelectList` to the `DropDownList` using the `ViewBag`.</span></span> <span data-ttu-id="b3050-222">此方法具有增加的优点，使你可以灵活地为集合使用更合适的名称。</span><span class="sxs-lookup"><span data-stu-id="b3050-222">This approach has the added advantage of giving you the flexibility of using a more appropriate name for the collection.</span></span> <span data-ttu-id="b3050-223">需要注意的一点是，您不能将 `ViewBag SelectList` 对象命名为与 model 属性相同的名称。</span><span class="sxs-lookup"><span data-stu-id="b3050-223">The one caveat is you cannot name the `ViewBag SelectList` object the same name as the model property.</span></span>

<span data-ttu-id="b3050-224">某些开发人员倾向于使用 ViewModel 方法。</span><span class="sxs-lookup"><span data-stu-id="b3050-224">Some developers prefer the ViewModel approach.</span></span> <span data-ttu-id="b3050-225">其他人将更详细的标记和生成的 HTML 用于 ViewModel 方法。</span><span class="sxs-lookup"><span data-stu-id="b3050-225">Others consider the more verbose markup and generated HTML of the ViewModel approach a disadvantage.</span></span>

<span data-ttu-id="b3050-226">在本部分中，我们了解了将**DropDownList**与类别数据结合使用的三种方法。</span><span class="sxs-lookup"><span data-stu-id="b3050-226">In this section we have learned three approaches to using the **DropDownList** with category data.</span></span> <span data-ttu-id="b3050-227">在下一部分中，我们将介绍如何添加新类别。</span><span class="sxs-lookup"><span data-stu-id="b3050-227">In the next section, we'll show how to add a new category.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="b3050-228">[上一页](using-the-dropdownlist-helper-with-aspnet-mvc.md)
> [下一页](adding-a-new-category-to-the-dropdownlist-using-jquery-ui.md)</span><span class="sxs-lookup"><span data-stu-id="b3050-228">[Previous](using-the-dropdownlist-helper-with-aspnet-mvc.md)
[Next](adding-a-new-category-to-the-dropdownlist-using-jquery-ui.md)</span></span>
