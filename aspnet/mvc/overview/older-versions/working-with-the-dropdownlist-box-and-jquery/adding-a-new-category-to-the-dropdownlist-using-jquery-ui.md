---
uid: mvc/overview/older-versions/working-with-the-dropdownlist-box-and-jquery/adding-a-new-category-to-the-dropdownlist-using-jquery-ui
title: 使用 jQuery UI 将新类别添加到 DropDownList |Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 01/12/2012
ms.assetid: 44aa1ac4-6ea2-48a2-972d-52710c48eae5
msc.legacyurl: /mvc/overview/older-versions/working-with-the-dropdownlist-box-and-jquery/adding-a-new-category-to-the-dropdownlist-using-jquery-ui
msc.type: authoredcontent
ms.openlocfilehash: 3207079ee468232e5f75b081421241c232936baf
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78433154"
---
# <a name="adding-a-new-category-to-the-dropdownlist-using-jquery-ui"></a><span data-ttu-id="b44ba-102">使用 jQuery UI 向 DropDownList 添加新类别</span><span class="sxs-lookup"><span data-stu-id="b44ba-102">Adding a New Category to the DropDownList using jQuery UI</span></span>

<span data-ttu-id="b44ba-103">作者： [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="b44ba-103">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="b44ba-104">HTML `Select` 标记非常适合用于呈现固定类别数据的列表，但通常需要添加新类别。</span><span class="sxs-lookup"><span data-stu-id="b44ba-104">The HTML `Select` tag is ideal for presenting a list of fixed category data, but often times you need to add a new category.</span></span> <span data-ttu-id="b44ba-105">假设我们要将流派 "Opera" 添加到数据库中的类别？</span><span class="sxs-lookup"><span data-stu-id="b44ba-105">Suppose we want to add the genre "Opera" to the categories in our database?</span></span> <span data-ttu-id="b44ba-106">在本部分中，我们将使用 jQuery UI 来添加一个对话框，可使用该对话框添加新类别。</span><span class="sxs-lookup"><span data-stu-id="b44ba-106">In this section, we will use jQuery UI to add a dialog box we can use to add a new category.</span></span> <span data-ttu-id="b44ba-107">下图显示了 UI 在浏览器中的显示方式。</span><span class="sxs-lookup"><span data-stu-id="b44ba-107">The image below shows how the UI will present in the browser.</span></span>

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image1.png)

<span data-ttu-id="b44ba-108">当用户选择 "**添加新流派**" 链接时，会弹出一个对话框，提示用户输入新的流派名称（可选）。</span><span class="sxs-lookup"><span data-stu-id="b44ba-108">When a user selects the **Add New Genre** link, a pop-up dialog box prompts the user for a new genre name (and optionally a description).</span></span> <span data-ttu-id="b44ba-109">下图显示了 "**添加流派**" 弹出对话框。</span><span class="sxs-lookup"><span data-stu-id="b44ba-109">The image below show the **Add Genre** pop-up dialog.</span></span>

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image2.png)

<span data-ttu-id="b44ba-110">当输入新的流派名称并推送 "**保存**" 按钮时，将发生以下情况：</span><span class="sxs-lookup"><span data-stu-id="b44ba-110">When a new genre name is entered and the **Save** button is pushed, the following happens:</span></span>

1. <span data-ttu-id="b44ba-111">AJAX 调用将数据发布到流派控制器的 Create 方法，该方法将新的流派保存到数据库，并将新的流派信息（流派名称和 ID）作为 JSON 返回。</span><span class="sxs-lookup"><span data-stu-id="b44ba-111">An AJAX call posts the data to the Create method of the Genre Controller, which saves the new genre to the database and returns the new genre information (genre name and ID) as JSON.</span></span>
2. <span data-ttu-id="b44ba-112">JavaScript 将新的流派数据添加到选择列表。</span><span class="sxs-lookup"><span data-stu-id="b44ba-112">JavaScript adds the new genre data to the select list.</span></span>
3. <span data-ttu-id="b44ba-113">JavaScript 使新的流派成为所选项目。</span><span class="sxs-lookup"><span data-stu-id="b44ba-113">JavaScript makes the new genre the selected item.</span></span>

   <span data-ttu-id="b44ba-114">在下图中，将 " **Opera** " 添加到数据库，并在 "**流派**" 下拉列表中选择。</span><span class="sxs-lookup"><span data-stu-id="b44ba-114">In the image below, **Opera** was added to the database and selected in the **Genre** drop down list.</span></span> 

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image3.png)

<span data-ttu-id="b44ba-115">打开*Views\StoreManager\Create.cshtml*文件，并将流派标记替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="b44ba-115">Open the *Views\StoreManager\Create.cshtml* file and replace the genre markup with the following the following code:</span></span>

[!code-cshtml[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample1.cshtml)]

<span data-ttu-id="b44ba-116">`_ChooseGenre` 分部视图将包含与用于实现添加新的流派功能的 JavaScript 和 jQuery 挂钩的所有逻辑。</span><span class="sxs-lookup"><span data-stu-id="b44ba-116">The `_ChooseGenre` partial view will contain all the logic to hook up the JavaScript and jQuery used to implement the add new genre feature.</span></span> <span data-ttu-id="b44ba-117">完成代码后，就可以轻松地使用艺术家 UI 执行相同操作。</span><span class="sxs-lookup"><span data-stu-id="b44ba-117">Once we have completed the code it will be simple to do the same with the artist UI.</span></span>

<span data-ttu-id="b44ba-118">在解决方案资源管理器中，右键单击*Views\StoreManager*文件夹，然后选择 "**添加**"，然后单击 "**查看**"。</span><span class="sxs-lookup"><span data-stu-id="b44ba-118">In Solution Explorer, right click the *Views\StoreManager* folder and select **Add**, then **View**.</span></span> <span data-ttu-id="b44ba-119">在 "**视图名称**" 输入中输入 `_ChooseGenre`，然后选择 "**添加**"。</span><span class="sxs-lookup"><span data-stu-id="b44ba-119">In the **View name** input, enter `_ChooseGenre` then select **Add**.</span></span> <span data-ttu-id="b44ba-120">将*Views\StoreManager\\_ChooseGenre*的标记替换为以下内容：</span><span class="sxs-lookup"><span data-stu-id="b44ba-120">Replace the markup in the *Views\StoreManager\\_ChooseGenre.cshtml* file with the following:</span></span>

[!code-cshtml[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample2.cshtml)]

<span data-ttu-id="b44ba-121">第一行声明我们作为模型传入了一个 `Album`，这与创建视图中找到的模型语句完全相同。</span><span class="sxs-lookup"><span data-stu-id="b44ba-121">The first line declares that we are passing in an `Album` as our model, exactly the same model statement found in the Create view.</span></span> <span data-ttu-id="b44ba-122">接下来的几行是**标签**帮助器标记。</span><span class="sxs-lookup"><span data-stu-id="b44ba-122">The next few lines are the **Label** helper markup.</span></span> <span data-ttu-id="b44ba-123">下一行是**DropDownList** helper 调用，与原始创建视图中的调用完全相同。</span><span class="sxs-lookup"><span data-stu-id="b44ba-123">The next line is the **DropDownList** helper call, exactly the same as in the original Create view.</span></span> <span data-ttu-id="b44ba-124">下一行添加一个名称 `Add New Genre`的链接，并将其样式用作按钮。</span><span class="sxs-lookup"><span data-stu-id="b44ba-124">The next line adds a link with the name `Add New Genre`, and styles it like a button.</span></span> <span data-ttu-id="b44ba-125">将直接从 "创建" 视图复制包含 `ValidationMessageFor` 的行。</span><span class="sxs-lookup"><span data-stu-id="b44ba-125">The line containing `ValidationMessageFor` is copied directly from the Create view.</span></span> <span data-ttu-id="b44ba-126">以下行：</span><span class="sxs-lookup"><span data-stu-id="b44ba-126">The following lines:</span></span>

[!code-html[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample3.html)]

<span data-ttu-id="b44ba-127">创建具有 `genreDialog`ID 的隐藏 div。</span><span class="sxs-lookup"><span data-stu-id="b44ba-127">creates a hidden div, with the ID of `genreDialog`.</span></span> <span data-ttu-id="b44ba-128">我们将使用 jQuery 挂钩 "**添加流派**" 对话框，该对话框具有此 div 中的 ID `genreDialog`。</span><span class="sxs-lookup"><span data-stu-id="b44ba-128">We will use jQuery to hook up our **Add Genre** dialog box with the ID `genreDialog` in this div.</span></span> <span data-ttu-id="b44ba-129">最后两个脚本标记包含指向用于实现 "添加新流派" 功能的 JavaScript 文件的链接。</span><span class="sxs-lookup"><span data-stu-id="b44ba-129">The last two script tags contain links to the JavaScript files we will use to implement the add new genre feature.</span></span> <span data-ttu-id="b44ba-130">*/Scripts/chooseGenre.js*文件是在项目中提供的，我们稍后将在本教程中对其进行检查。</span><span class="sxs-lookup"><span data-stu-id="b44ba-130">The */Scripts/chooseGenre.js* file is provided for you in the project, we will examine it later in the tutorial.</span></span>

<span data-ttu-id="b44ba-131">运行应用程序，并单击 "**添加新流派**" 按钮。</span><span class="sxs-lookup"><span data-stu-id="b44ba-131">Run the application and click on the **Add New Genre** button.</span></span> <span data-ttu-id="b44ba-132">在 "**添加流派**" 对话框中，在 "**名称**" 输入框中输入 " **Opera** "。</span><span class="sxs-lookup"><span data-stu-id="b44ba-132">In the **Add Genre** dialog box, enter **Opera** in the **Name** input box.</span></span>

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image4.png)

<span data-ttu-id="b44ba-133">单击“保存”按钮。</span><span class="sxs-lookup"><span data-stu-id="b44ba-133">Click the **Save** button.</span></span> <span data-ttu-id="b44ba-134">AJAX 调用创建了 "Opera" 类别，然后使用 Opera 填充下拉列表，并将 "Opera" 设置为所选的流派。</span><span class="sxs-lookup"><span data-stu-id="b44ba-134">An AJAX call creates the Opera category and then populates the dropdown list with Opera, and sets Opera as the selected genre.</span></span>

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image5.png)

<span data-ttu-id="b44ba-135">输入艺术家、标题和价格，然后选择 "**创建**" 按钮。</span><span class="sxs-lookup"><span data-stu-id="b44ba-135">Enter an artist, title and price, then select the **Create** button.</span></span> <span data-ttu-id="b44ba-136">如果输入小于 $8.99 的价格，则新的唱片集将显示在索引视图的顶部。</span><span class="sxs-lookup"><span data-stu-id="b44ba-136">If you enter a price less than $8.99, the new album will appear at the top of the Index view.</span></span> <span data-ttu-id="b44ba-137">验证新的唱片集条目是否已保存到数据库中。</span><span class="sxs-lookup"><span data-stu-id="b44ba-137">Verify the new album entry was saved in the database.</span></span>

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image6.png)

<span data-ttu-id="b44ba-138">尝试创建一个只包含一个字母的新流派。</span><span class="sxs-lookup"><span data-stu-id="b44ba-138">Try creating a new genre with only one letter.</span></span> <span data-ttu-id="b44ba-139">*Models\Genre.cs*文件中的以下代码设置了流派名称的最小长度和最大长度。</span><span class="sxs-lookup"><span data-stu-id="b44ba-139">The following code in the *Models\Genre.cs* file sets the minimum and maximum length of the genre name.</span></span>

[!code-csharp[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample4.cs)]

<span data-ttu-id="b44ba-140">客户端验证报表您必须输入一个介于2到20个字符之间的字符串。</span><span class="sxs-lookup"><span data-stu-id="b44ba-140">Client side validation reports you must enter a string between 2 and 20 characters.</span></span>

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image7.png)

### <a name="examining-how-a-new-genre-is-added-to-the-database-and-the-select-list"></a><span data-ttu-id="b44ba-141">检查如何将新的流派添加到数据库以及选择列表。</span><span class="sxs-lookup"><span data-stu-id="b44ba-141">Examining How a New Genre is Added to the Database and the Select List.</span></span>

<span data-ttu-id="b44ba-142">打开*Scripts\chooseGenre.js*文件并检查代码。</span><span class="sxs-lookup"><span data-stu-id="b44ba-142">Open the *Scripts\chooseGenre.js* file and examine the code.</span></span>

[!code-javascript[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample5.js)]

<span data-ttu-id="b44ba-143">第二行使用 ID `genreDialog` 在*Views\StoreManager\\_ChooseGenre* # # 文件中的 div 标记上创建一个对话框。</span><span class="sxs-lookup"><span data-stu-id="b44ba-143">The second line uses the ID `genreDialog` to create a dialog box on the div tag in the *Views\StoreManager\\_ChooseGenre.cshtml* file.</span></span> <span data-ttu-id="b44ba-144">大多数命名参数都是一目了然的。</span><span class="sxs-lookup"><span data-stu-id="b44ba-144">Most of the named parameters are self explanatory.</span></span> <span data-ttu-id="b44ba-145">`autoOpen` 参数设置为 "false"，则选择 "**创建流派**" 按钮将显式打开对话（这在中对此进行了说明）。</span><span class="sxs-lookup"><span data-stu-id="b44ba-145">The `autoOpen` parameter is set to false, selecting the **Create Genre** button will open the dialogue explicitly (this is described latter on).</span></span> <span data-ttu-id="b44ba-146">此对话框包含两个按钮： "**保存**" 和 "**取消**"。</span><span class="sxs-lookup"><span data-stu-id="b44ba-146">The dialog has two buttons, **Save** and **Cancel**.</span></span> <span data-ttu-id="b44ba-147">"**取消**" 按钮关闭对话框。</span><span class="sxs-lookup"><span data-stu-id="b44ba-147">The **Cancel** button closes the dialog.</span></span> <span data-ttu-id="b44ba-148">下面的代码显示 "**保存**" 按钮函数。</span><span class="sxs-lookup"><span data-stu-id="b44ba-148">The following code shows the **Save** button function.</span></span>

[!code-javascript[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample6.js)]

<span data-ttu-id="b44ba-149">将从 `createGenreForm` ID 中选择 `var createGenreForm`。</span><span class="sxs-lookup"><span data-stu-id="b44ba-149">The `var createGenreForm` is selected from the `createGenreForm` ID.</span></span> <span data-ttu-id="b44ba-150">`createGenreForm` ID 在*Views\Genre\\_CreateGenre.* # 文件中找到的以下代码中进行了设置。</span><span class="sxs-lookup"><span data-stu-id="b44ba-150">The `createGenreForm` ID was set in the following code found in the *Views\Genre\\_CreateGenre.cshtml* file.</span></span>

[!code-cshtml[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample7.cshtml)]

<span data-ttu-id="b44ba-151">Views\Genre\\中使用的[html.beginform](https://msdn.microsoft.com/library/dd492714.aspx) helper 重载 *_CreateGenre. #. #. #. #. #.*</span><span class="sxs-lookup"><span data-stu-id="b44ba-151">The [Html.BeginForm](https://msdn.microsoft.com/library/dd492714.aspx) helper overload used in the *Views\Genre\\_CreateGenre.cshtml* file generates HTML with an action attribute containing the URL to submit the form.</span></span> <span data-ttu-id="b44ba-152">可以通过在浏览器中显示 "创建唱片集" 页，然后在浏览器中选择 "显示源" 来查看此项。</span><span class="sxs-lookup"><span data-stu-id="b44ba-152">You can see this by displaying the create album page in a browser and selecting show source in the browser.</span></span> <span data-ttu-id="b44ba-153">以下标记显示了包含表单标记的生成的 HTML。</span><span class="sxs-lookup"><span data-stu-id="b44ba-153">The following markup shows the generated HTML containing the form tag.</span></span>

[!code-html[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample8.html)]

<span data-ttu-id="b44ba-154">JQuery `$.post` 行对操作属性（`/StoreManager/Create`）进行 AJAX 调用，并传入 "**创建流派**" 对话框中的数据。</span><span class="sxs-lookup"><span data-stu-id="b44ba-154">The jQuery `$.post` line makes an AJAX call to the action attribute (`/StoreManager/Create`) and passes in the data from the **Create Genre** dialog box.</span></span> <span data-ttu-id="b44ba-155">数据包含新流派的名称和可选说明。</span><span class="sxs-lookup"><span data-stu-id="b44ba-155">The data consists of the name for the new genre and an optional description.</span></span> <span data-ttu-id="b44ba-156">如果 AJAX 调用成功，新的流派名称和值将添加到 "选择标记"，并将新的流派设置为所选值。</span><span class="sxs-lookup"><span data-stu-id="b44ba-156">If the AJAX call is successful, the new genre name and value are added to the Select markup, and the new genre is set to the selected value.</span></span> <span data-ttu-id="b44ba-157">由于这是动态生成的标记，因此无法通过在浏览器中查看源来查看新的选择选项。</span><span class="sxs-lookup"><span data-stu-id="b44ba-157">Because this is dynamically generated markup, you can't see the new select option by viewing the source in the browser.</span></span> <span data-ttu-id="b44ba-158">你可以看到具有 IE 9 F12 开发人员工具的新 HTML。</span><span class="sxs-lookup"><span data-stu-id="b44ba-158">You can see the new HTML with the IE 9 F12 developer tools.</span></span> <span data-ttu-id="b44ba-159">若要查看新的选择选项，请在 Internet Explorer 9 中按 F12 键启动 F12 开发人员工具。</span><span class="sxs-lookup"><span data-stu-id="b44ba-159">To view the new select option, in Internet Explorer 9, hit the F12 key to start the F12 developer tools.</span></span> <span data-ttu-id="b44ba-160">导航到 "创建" 页并添加一个新的流派，以便在 "流派选择列表" 中选择新的流派。</span><span class="sxs-lookup"><span data-stu-id="b44ba-160">Navigate to the Create page and add a new genre so the new genre is selected in the genre select list.</span></span> <span data-ttu-id="b44ba-161">在 F12 开发人员工具中：</span><span class="sxs-lookup"><span data-stu-id="b44ba-161">In the F12 developer tools:</span></span>

1. <span data-ttu-id="b44ba-162">选择 "HTML" 选项卡。</span><span class="sxs-lookup"><span data-stu-id="b44ba-162">Select the HTML tab.</span></span>
2. <span data-ttu-id="b44ba-163">点击刷新图标。</span><span class="sxs-lookup"><span data-stu-id="b44ba-163">Hit the refresh icon.</span></span>  
    ![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image8.png)
3. <span data-ttu-id="b44ba-164">在搜索框中，输入 "GenreID"。</span><span class="sxs-lookup"><span data-stu-id="b44ba-164">In the search box, enter GenreID.</span></span>
4. <span data-ttu-id="b44ba-165">使用下一个图标，</span><span class="sxs-lookup"><span data-stu-id="b44ba-165">Using the next icon,</span></span>   
    ![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image9.png)  
   <span data-ttu-id="b44ba-166">导航到以下选择标记：</span><span class="sxs-lookup"><span data-stu-id="b44ba-166">navigate to the following select tag:</span></span>

    [!code-html[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample9.html)]
5. <span data-ttu-id="b44ba-167">展开最后一个选项值。</span><span class="sxs-lookup"><span data-stu-id="b44ba-167">Expand the last option value.</span></span>

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image10.png)

<span data-ttu-id="b44ba-168">*Scripts\chooseGenre.js*文件中的以下代码显示了如何将 "**添加新的流派**" 按钮连接到 click 事件，以及如何创建 "**添加新流派**" 对话框。</span><span class="sxs-lookup"><span data-stu-id="b44ba-168">The following code in the *Scripts\chooseGenre.js* file shows the how the **Add New Genre** button gets connected to the click event, and how the **Add New Genre** dialog box is created.</span></span>

[!code-javascript[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample10.js)]

<span data-ttu-id="b44ba-169">第一行创建附加到 "**添加新流派**" 按钮的 click 函数。</span><span class="sxs-lookup"><span data-stu-id="b44ba-169">The first line creates a click function attached to the **Add New Genre** button.</span></span> <span data-ttu-id="b44ba-170">Views\StoreManager\\_ChooseGenre. # 文件中的以下标记显示了如何创建 "**添加新流派**" 按钮：</span><span class="sxs-lookup"><span data-stu-id="b44ba-170">The following markup from the Views\StoreManager\\_ChooseGenre.cshtml file shows how the **Add New Genre** button is created:</span></span>

[!code-cshtml[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample11.cshtml)]

<span data-ttu-id="b44ba-171">Load 方法创建并打开 "添加流派" 对话框并调用 jQuery `parse` 方法，以便在对话框中输入的数据上进行客户端验证。</span><span class="sxs-lookup"><span data-stu-id="b44ba-171">The load method creates and opens the Add Genre dialog and calls the jQuery `parse` method so client validation occurs on data entered in the dialog.</span></span>

<span data-ttu-id="b44ba-172">在本部分中，您学习了如何创建一个对话框，该对话框可用于将新的类别数据添加到选择列表。</span><span class="sxs-lookup"><span data-stu-id="b44ba-172">In this section you have learned how to create a dialog that can be used to add new category data to a select list.</span></span> <span data-ttu-id="b44ba-173">可以按照相同的过程来创建 UI，以将新的艺术家添加到艺术家选择列表。</span><span class="sxs-lookup"><span data-stu-id="b44ba-173">You can follow the same procedure to create UI to add a new artist to the artist select list.</span></span> <span data-ttu-id="b44ba-174">本教程大致介绍了如何使用 ASP.NET MVC HTML helper **DropDownList**。</span><span class="sxs-lookup"><span data-stu-id="b44ba-174">This tutorial has given an overview of working with the ASP.NET MVC HTML helper **DropDownList**.</span></span> <span data-ttu-id="b44ba-175">有关使用**DropDownList**的其他信息，请参阅下面的加法引用部分。</span><span class="sxs-lookup"><span data-stu-id="b44ba-175">For additional information on working with the **DropDownList**, see the addition references section below.</span></span> <span data-ttu-id="b44ba-176">如果本教程有帮助，请告知我们。</span><span class="sxs-lookup"><span data-stu-id="b44ba-176">Please let us know if this tutorial has been helpful.</span></span>

<span data-ttu-id="b44ba-177">Rick.Anderson[at]Microsoft.com</span><span class="sxs-lookup"><span data-stu-id="b44ba-177">Rick.Anderson[at]Microsoft.com</span></span>

### <a name="additional-references"></a><span data-ttu-id="b44ba-178">其他参考</span><span class="sxs-lookup"><span data-stu-id="b44ba-178">Additional References</span></span>

- <span data-ttu-id="b44ba-179">[ASP.NET MVC –级联下拉列表教程（](https://weblogs.asp.net/raduenuca/archive/2011/03/06/asp-net-mvc-cascading-dropdown-lists-tutorial-part-1-defining-the-problem-and-the-context.aspx) [Radu enuca on](https://weblogs.asp.net/raduenuca/default.aspx) ）</span><span class="sxs-lookup"><span data-stu-id="b44ba-179">[ASP.NET MVC–Cascading Dropdown Lists Tutorial](https://weblogs.asp.net/raduenuca/archive/2011/03/06/asp-net-mvc-cascading-dropdown-lists-tutorial-part-1-defining-the-problem-and-the-context.aspx) by [Radu Enuca](https://weblogs.asp.net/raduenuca/default.aspx)</span></span>
- <span data-ttu-id="b44ba-180">已[选择](https://harvesthq.github.com/chosen/)支持多选和筛选的 JavaScript 插件。</span><span class="sxs-lookup"><span data-stu-id="b44ba-180">[Chosen](https://harvesthq.github.com/chosen/) A JavaScript plugin that support multi-select and filtering.</span></span>

### <a name="contributors"></a><span data-ttu-id="b44ba-181">参与者</span><span class="sxs-lookup"><span data-stu-id="b44ba-181">Contributors</span></span>

- [<span data-ttu-id="b44ba-182">Radu Enuca on</span><span class="sxs-lookup"><span data-stu-id="b44ba-182">Radu Enuca</span></span>](https://weblogs.asp.net/raduenuca/default.aspx)
- <span data-ttu-id="b44ba-183">Jean-Sébastien Goupil</span><span class="sxs-lookup"><span data-stu-id="b44ba-183">Jean-Sébastien Goupil</span></span>
- [<span data-ttu-id="b44ba-184">Brad Wilson</span><span class="sxs-lookup"><span data-stu-id="b44ba-184">Brad Wilson</span></span>](http://bradwilson.typepad.com/)

### <a name="reviewers"></a><span data-ttu-id="b44ba-185">审阅者</span><span class="sxs-lookup"><span data-stu-id="b44ba-185">Reviewers</span></span>

- <span data-ttu-id="b44ba-186">Jean-Sébastien Goupil</span><span class="sxs-lookup"><span data-stu-id="b44ba-186">Jean-Sébastien Goupil</span></span>
- [<span data-ttu-id="b44ba-187">Brad Wilson</span><span class="sxs-lookup"><span data-stu-id="b44ba-187">Brad Wilson</span></span>](http://bradwilson.typepad.com/)
- <span data-ttu-id="b44ba-188">Mike Pope</span><span class="sxs-lookup"><span data-stu-id="b44ba-188">Mike Pope</span></span>
- <span data-ttu-id="b44ba-189">Tom Dykstra</span><span class="sxs-lookup"><span data-stu-id="b44ba-189">Tom Dykstra</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="b44ba-190">上一页</span><span class="sxs-lookup"><span data-stu-id="b44ba-190">Previous</span></span>](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper.md)
