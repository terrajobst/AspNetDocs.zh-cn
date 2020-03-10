---
uid: mvc/overview/older-versions-1/nerddinner/provide-crud-create-read-update-delete-data-form-entry-support
title: 提供 CRUD （创建、读取、更新、删除）数据窗体项支持 |Microsoft Docs
author: microsoft
description: 步骤5演示了如何通过支持编辑、创建和删除就，进一步获取我们的 DinnersController 类。
ms.author: riande
ms.date: 07/27/2010
ms.assetid: bbb976e5-6150-4283-a374-c22fbafe29f5
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/provide-crud-create-read-update-delete-data-form-entry-support
msc.type: authoredcontent
ms.openlocfilehash: b3123af9a1477bc496a0d229d628510fc202b6d2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78468914"
---
# <a name="provide-crud-create-read-update-delete-data-form-entry-support"></a><span data-ttu-id="5944b-103">提供 CRUD（创建、读取、更新和删除）数据窗体输入支持</span><span class="sxs-lookup"><span data-stu-id="5944b-103">Provide CRUD (Create, Read, Update, Delete) Data Form Entry Support</span></span>

<span data-ttu-id="5944b-104">由[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="5944b-104">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="5944b-105">下载 PDF</span><span class="sxs-lookup"><span data-stu-id="5944b-105">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="5944b-106">这是免费的["NerdDinner" 应用程序教程](introducing-the-nerddinner-tutorial.md)的第5步，其中演练了如何使用 ASP.NET MVC 1 构建一个小型的、完整的 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="5944b-106">This is step 5 of a free ["NerdDinner" application tutorial](introducing-the-nerddinner-tutorial.md) that walks-through how to build a small, but complete, web application using ASP.NET MVC 1.</span></span>
> 
> <span data-ttu-id="5944b-107">步骤5演示了如何通过支持编辑、创建和删除就，进一步获取我们的 DinnersController 类。</span><span class="sxs-lookup"><span data-stu-id="5944b-107">Step 5 shows how to take our DinnersController class further by enable support for editing, creating and deleting Dinners with it as well.</span></span>
> 
> <span data-ttu-id="5944b-108">如果你使用的是 ASP.NET MVC 3，则建议你遵循[MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)或[Mvc 音乐应用商店](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)教程中的入门。</span><span class="sxs-lookup"><span data-stu-id="5944b-108">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>

## <a name="nerddinner-step-5-create-update-delete-form-scenarios"></a><span data-ttu-id="5944b-109">NerdDinner 步骤5：创建、更新、删除窗体方案</span><span class="sxs-lookup"><span data-stu-id="5944b-109">NerdDinner Step 5: Create, Update, Delete Form Scenarios</span></span>

<span data-ttu-id="5944b-110">我们引入了控制器和视图，并介绍了如何使用它们来实现站点上就的列表/详细信息体验。</span><span class="sxs-lookup"><span data-stu-id="5944b-110">We've introduced controllers and views, and covered how to use them to implement a listing/details experience for Dinners on site.</span></span> <span data-ttu-id="5944b-111">下一步是进一步学习我们的 DinnersController 类，并支持编辑、创建和删除就。</span><span class="sxs-lookup"><span data-stu-id="5944b-111">Our next step will be to take our DinnersController class further and enable support for editing, creating and deleting Dinners with it as well.</span></span>

### <a name="urls-handled-by-dinnerscontroller"></a><span data-ttu-id="5944b-112">DinnersController 处理的 Url</span><span class="sxs-lookup"><span data-stu-id="5944b-112">URLs handled by DinnersController</span></span>

<span data-ttu-id="5944b-113">我们之前向 DinnersController 添加了实现了对两个 Url 的支持的操作方法： */Dinners*和 */Dinners/Details/[id]* 。</span><span class="sxs-lookup"><span data-stu-id="5944b-113">We previously added action methods to DinnersController that implemented support for two URLs: */Dinners* and */Dinners/Details/[id]*.</span></span>

| <span data-ttu-id="5944b-114">**URL**</span><span class="sxs-lookup"><span data-stu-id="5944b-114">**URL**</span></span> | <span data-ttu-id="5944b-115">**谓词**</span><span class="sxs-lookup"><span data-stu-id="5944b-115">**VERB**</span></span> | <span data-ttu-id="5944b-116">**目的**</span><span class="sxs-lookup"><span data-stu-id="5944b-116">**Purpose**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5944b-117">*就*</span><span class="sxs-lookup"><span data-stu-id="5944b-117">*/Dinners/*</span></span> | <span data-ttu-id="5944b-118">GET</span><span class="sxs-lookup"><span data-stu-id="5944b-118">GET</span></span> | <span data-ttu-id="5944b-119">显示即将发布的就的 HTML 列表。</span><span class="sxs-lookup"><span data-stu-id="5944b-119">Display an HTML list of upcoming dinners.</span></span> |
| <span data-ttu-id="5944b-120">*/Dinners/Details/[id]*</span><span class="sxs-lookup"><span data-stu-id="5944b-120">*/Dinners/Details/[id]*</span></span> | <span data-ttu-id="5944b-121">GET</span><span class="sxs-lookup"><span data-stu-id="5944b-121">GET</span></span> | <span data-ttu-id="5944b-122">显示有关特定晚餐的详细信息。</span><span class="sxs-lookup"><span data-stu-id="5944b-122">Display details about a specific dinner.</span></span> |

<span data-ttu-id="5944b-123">现在，我们将添加操作方法来实现另外三个 Url： */Dinners/Edit/[id]* 、 */Dinners/Create*和 */Dinners/Delete/[id]* 。</span><span class="sxs-lookup"><span data-stu-id="5944b-123">We will now add action methods to implement three additional URLs: */Dinners/Edit/[id]*, */Dinners/Create*, and */Dinners/Delete/[id]*.</span></span> <span data-ttu-id="5944b-124">这些 Url 支持编辑现有的就、创建新的就以及删除就。</span><span class="sxs-lookup"><span data-stu-id="5944b-124">These URLs will enable support for editing existing Dinners, creating new Dinners, and deleting Dinners.</span></span>

<span data-ttu-id="5944b-125">我们将支持 HTTP GET 和 HTTP POST 谓词与这些新的 Url 的交互。</span><span class="sxs-lookup"><span data-stu-id="5944b-125">We will support both HTTP GET and HTTP POST verb interactions with these new URLs.</span></span> <span data-ttu-id="5944b-126">对这些 Url 的 HTTP GET 请求将显示数据的初始 HTML 视图（在 "编辑" 的情况下，用晚餐数据填充的窗体，在 "创建" 的情况下为空白窗体，在 "删除" 情况下为删除确认屏幕）。</span><span class="sxs-lookup"><span data-stu-id="5944b-126">HTTP GET requests to these URLs will display the initial HTML view of the data (a form populated with the Dinner data in the case of "edit", a blank form in the case of "create", and a delete confirmation screen in the case of "delete").</span></span> <span data-ttu-id="5944b-127">对这些 Url 发出的 HTTP POST 请求将保存/更新/删除 DinnerRepository （和数据库）中的晚餐数据。</span><span class="sxs-lookup"><span data-stu-id="5944b-127">HTTP POST requests to these URLs will save/update/delete the Dinner data in our DinnerRepository (and from there to the database).</span></span>

| <span data-ttu-id="5944b-128">**URL**</span><span class="sxs-lookup"><span data-stu-id="5944b-128">**URL**</span></span> | <span data-ttu-id="5944b-129">**谓词**</span><span class="sxs-lookup"><span data-stu-id="5944b-129">**VERB**</span></span> | <span data-ttu-id="5944b-130">**目的**</span><span class="sxs-lookup"><span data-stu-id="5944b-130">**Purpose**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5944b-131">*/Dinners/Edit/[id]*</span><span class="sxs-lookup"><span data-stu-id="5944b-131">*/Dinners/Edit/[id]*</span></span> | <span data-ttu-id="5944b-132">GET</span><span class="sxs-lookup"><span data-stu-id="5944b-132">GET</span></span> | <span data-ttu-id="5944b-133">显示可编辑的 HTML 窗体，其中填充了晚餐数据。</span><span class="sxs-lookup"><span data-stu-id="5944b-133">Display an editable HTML form populated with Dinner data.</span></span> |
| <span data-ttu-id="5944b-134">POST</span><span class="sxs-lookup"><span data-stu-id="5944b-134">POST</span></span> | <span data-ttu-id="5944b-135">将特定晚餐的窗体更改保存到数据库。</span><span class="sxs-lookup"><span data-stu-id="5944b-135">Save the form changes for a particular Dinner to the database.</span></span> |
| <span data-ttu-id="5944b-136">*/Dinners/Create*</span><span class="sxs-lookup"><span data-stu-id="5944b-136">*/Dinners/Create*</span></span> | <span data-ttu-id="5944b-137">GET</span><span class="sxs-lookup"><span data-stu-id="5944b-137">GET</span></span> | <span data-ttu-id="5944b-138">显示允许用户定义新就的空 HTML 窗体。</span><span class="sxs-lookup"><span data-stu-id="5944b-138">Display an empty HTML form that allows users to define new Dinners.</span></span> |
| <span data-ttu-id="5944b-139">POST</span><span class="sxs-lookup"><span data-stu-id="5944b-139">POST</span></span> | <span data-ttu-id="5944b-140">创建新晚餐，并将其保存在数据库中。</span><span class="sxs-lookup"><span data-stu-id="5944b-140">Create a new Dinner and save it in the database.</span></span> |
| <span data-ttu-id="5944b-141">*/Dinners/Delete/[id]*</span><span class="sxs-lookup"><span data-stu-id="5944b-141">*/Dinners/Delete/[id]*</span></span> | <span data-ttu-id="5944b-142">GET</span><span class="sxs-lookup"><span data-stu-id="5944b-142">GET</span></span> | <span data-ttu-id="5944b-143">显示删除确认屏幕。</span><span class="sxs-lookup"><span data-stu-id="5944b-143">Display delete confirmation screen.</span></span> |
| <span data-ttu-id="5944b-144">POST</span><span class="sxs-lookup"><span data-stu-id="5944b-144">POST</span></span> | <span data-ttu-id="5944b-145">从数据库中删除指定的晚餐。</span><span class="sxs-lookup"><span data-stu-id="5944b-145">Deletes the specified dinner from the database.</span></span> |

### <a name="edit-support"></a><span data-ttu-id="5944b-146">编辑支持</span><span class="sxs-lookup"><span data-stu-id="5944b-146">Edit Support</span></span>

<span data-ttu-id="5944b-147">首先，我们要实现 "编辑" 方案。</span><span class="sxs-lookup"><span data-stu-id="5944b-147">Let's begin by implementing the "edit" scenario.</span></span>

#### <a name="the-http-get-edit-action-method"></a><span data-ttu-id="5944b-148">HTTP-获取编辑操作方法</span><span class="sxs-lookup"><span data-stu-id="5944b-148">The HTTP-GET Edit Action Method</span></span>

<span data-ttu-id="5944b-149">首先，我们将实现编辑操作方法的 HTTP "GET" 行为。</span><span class="sxs-lookup"><span data-stu-id="5944b-149">We'll start by implementing the HTTP "GET" behavior of our edit action method.</span></span> <span data-ttu-id="5944b-150">当请求 */Dinners/Edit/[id]* URL 时，将调用此方法。</span><span class="sxs-lookup"><span data-stu-id="5944b-150">This method will be invoked when the */Dinners/Edit/[id]* URL is requested.</span></span> <span data-ttu-id="5944b-151">我们的实现如下所示：</span><span class="sxs-lookup"><span data-stu-id="5944b-151">Our implementation will look like:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample1.cs)]

<span data-ttu-id="5944b-152">上面的代码使用 DinnerRepository 检索晚餐对象。</span><span class="sxs-lookup"><span data-stu-id="5944b-152">The code above uses the DinnerRepository to retrieve a Dinner object.</span></span> <span data-ttu-id="5944b-153">然后，它使用晚餐对象呈现视图模板。</span><span class="sxs-lookup"><span data-stu-id="5944b-153">It then renders a View template using the Dinner object.</span></span> <span data-ttu-id="5944b-154">由于我们未将模板名称显式传递给*view （）* helper 方法，因此它将使用基于约定的默认路径来解析视图模板：/Views/Dinners/Edit.aspx。</span><span class="sxs-lookup"><span data-stu-id="5944b-154">Because we haven't explicitly passed a template name to the *View()* helper method, it will use the convention based default path to resolve the view template: /Views/Dinners/Edit.aspx.</span></span>

<span data-ttu-id="5944b-155">现在，创建此视图模板。</span><span class="sxs-lookup"><span data-stu-id="5944b-155">Let's now create this view template.</span></span> <span data-ttu-id="5944b-156">为此，我们将在编辑方法中右键单击，然后选择 "添加视图" 上下文菜单命令：</span><span class="sxs-lookup"><span data-stu-id="5944b-156">We will do this by right-clicking within the Edit method and selecting the "Add View" context menu command:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image1.png)

<span data-ttu-id="5944b-157">在 "添加视图" 对话框中，我们将指出我们要将晚餐对象作为其模型传递到我们的视图模板，并选择自动基架 "编辑" 模板：</span><span class="sxs-lookup"><span data-stu-id="5944b-157">Within the "Add View" dialog we'll indicate that we are passing a Dinner object to our view template as its model, and choose to auto-scaffold an "Edit" template:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image2.png)

<span data-ttu-id="5944b-158">单击 "添加" 按钮时，Visual Studio 将在 "\Views\Dinners" 目录中为我们添加新的 "Edit .aspx" 视图模板文件。</span><span class="sxs-lookup"><span data-stu-id="5944b-158">When we click the "Add" button, Visual Studio will add a new "Edit.aspx" view template file for us within the "\Views\Dinners" directory.</span></span> <span data-ttu-id="5944b-159">它还将在代码编辑器中打开新的 "Edit .aspx" 视图模板–用如下所示的初始 "编辑" 基架实现进行填充：</span><span class="sxs-lookup"><span data-stu-id="5944b-159">It will also open up the new "Edit.aspx" view template within the code-editor – populated with an initial "Edit" scaffold implementation like below:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image3.png)

<span data-ttu-id="5944b-160">让我们对生成的默认 "编辑" 基架进行一些更改，并更新 "编辑视图" 模板，使其包含以下内容（这会删除一些我们不想公开的属性）：</span><span class="sxs-lookup"><span data-stu-id="5944b-160">Let's make a few changes to the default "edit" scaffold generated, and update the edit view template to have the content below (which removes a few of the properties we don't want to expose):</span></span>

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample2.aspx)]

<span data-ttu-id="5944b-161">运行应用程序并请求 *"/Dinners/Edit/1"* URL 时，会看到以下页面：</span><span class="sxs-lookup"><span data-stu-id="5944b-161">When we run the application and request the *"/Dinners/Edit/1"* URL we will see the following page:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image4.png)

<span data-ttu-id="5944b-162">视图生成的 HTML 标记如下所示。</span><span class="sxs-lookup"><span data-stu-id="5944b-162">The HTML markup generated by our view looks like below.</span></span> <span data-ttu-id="5944b-163">标准 HTML –带有 &lt;窗体&gt; 元素，该元素在推送 "Save" &lt;输入类型 = "submit"/&gt; 按钮时执行到 */Dinners/Edit/1* URL 的 HTTP POST。</span><span class="sxs-lookup"><span data-stu-id="5944b-163">It is standard HTML – with a &lt;form&gt; element that performs an HTTP POST to the */Dinners/Edit/1* URL when the "Save" &lt;input type="submit"/&gt; button is pushed.</span></span> <span data-ttu-id="5944b-164">为每个可编辑属性输出了 HTML &lt;输入类型 = "text"/&gt; 元素：</span><span class="sxs-lookup"><span data-stu-id="5944b-164">A HTML &lt;input type="text"/&gt; element has been output for each editable property:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image5.png)

#### <a name="htmlbeginform-and-htmltextbox-html-helper-methods"></a><span data-ttu-id="5944b-165">Html.beginform （）和 .Html （） Html Helper 方法</span><span class="sxs-lookup"><span data-stu-id="5944b-165">Html.BeginForm() and Html.TextBox() Html Helper Methods</span></span>

<span data-ttu-id="5944b-166">我们的 "Edit .aspx" 视图模板使用几个 "Html Helper" 方法： ValidationSummary （）、Html.beginform （）、.Html （）和 ValidationMessage （）。</span><span class="sxs-lookup"><span data-stu-id="5944b-166">Our "Edit.aspx" view template is using several "Html Helper" methods: Html.ValidationSummary(), Html.BeginForm(), Html.TextBox(), and Html.ValidationMessage().</span></span> <span data-ttu-id="5944b-167">除了为我们生成 HTML 标记之外，这些帮助器方法还提供内置的错误处理和验证支持。</span><span class="sxs-lookup"><span data-stu-id="5944b-167">In addition to generating HTML markup for us, these helper methods provide built-in error handling and validation support.</span></span>

##### <a name="htmlbeginform-helper-method"></a><span data-ttu-id="5944b-168">Html.beginform （） helper 方法</span><span class="sxs-lookup"><span data-stu-id="5944b-168">Html.BeginForm() helper method</span></span>

<span data-ttu-id="5944b-169">Html.beginform （） helper 方法是在标记中输出 HTML &lt;窗体&gt; 元素的内容。</span><span class="sxs-lookup"><span data-stu-id="5944b-169">The Html.BeginForm() helper method is what output the HTML &lt;form&gt; element in our markup.</span></span> <span data-ttu-id="5944b-170">在我们的 Edit .aspx 视图模板中，你会注意到，在C#使用此方法时，我们正在应用 "using" 语句。</span><span class="sxs-lookup"><span data-stu-id="5944b-170">In our Edit.aspx view template you'll notice that we are applying a C# "using" statement when using this method.</span></span> <span data-ttu-id="5944b-171">左大括号指示 &lt;窗体&gt; 内容的开头，右大括号表示 &lt;/form&gt; 元素的末尾：</span><span class="sxs-lookup"><span data-stu-id="5944b-171">The open curly brace indicates the beginning of the &lt;form&gt; content, and the closing curly brace is what indicates the end of the &lt;/form&gt; element:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample3.cs)]

<span data-ttu-id="5944b-172">或者，如果你为这样的方案找到了 "using" 语句方法非自然，则可以使用 Html.beginform （）和 EndForm （）组合（执行相同的操作）：</span><span class="sxs-lookup"><span data-stu-id="5944b-172">Alternatively, if you find the "using" statement approach unnatural for a scenario like this, you can use a Html.BeginForm() and Html.EndForm() combination (which does the same thing):</span></span>

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample4.aspx)]

<span data-ttu-id="5944b-173">如果调用不带任何参数的 Html.beginform （），则将导致它输出一个对当前请求的 URL 执行 HTTP POST 的窗体元素。</span><span class="sxs-lookup"><span data-stu-id="5944b-173">Calling Html.BeginForm() without any parameters will cause it to output a form element that does an HTTP-POST to the current request's URL.</span></span> <span data-ttu-id="5944b-174">这就是为什么我们的编辑视图生成 *&lt;窗体 action = "/Dinners/Edit/1" method = "post"&gt;* 元素的原因。</span><span class="sxs-lookup"><span data-stu-id="5944b-174">That is why our Edit view generates a *&lt;form action="/Dinners/Edit/1" method="post"&gt;* element.</span></span> <span data-ttu-id="5944b-175">如果要发布到不同的 URL，可以将显式参数传递给 Html.beginform （）。</span><span class="sxs-lookup"><span data-stu-id="5944b-175">We could have alternatively passed explicit parameters to Html.BeginForm() if we wanted to post to a different URL.</span></span>

##### <a name="htmltextbox-helper-method"></a><span data-ttu-id="5944b-176">.Html （） helper 方法</span><span class="sxs-lookup"><span data-stu-id="5944b-176">Html.TextBox() helper method</span></span>

<span data-ttu-id="5944b-177">Edit .aspx 视图使用 .Html （） helper 方法输出 &lt;输入类型 = "text"/&gt; 元素：</span><span class="sxs-lookup"><span data-stu-id="5944b-177">Our Edit.aspx view uses the Html.TextBox() helper method to output &lt;input type="text"/&gt; elements:</span></span>

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample5.aspx)]

<span data-ttu-id="5944b-178">上面的 Html. TextBox （）方法采用单个参数，该参数用于指定要输出的 &lt;输入类型 = "text"/&gt; 元素的 id/名称特性，以及要从中填充 TextBox 值的模型属性。</span><span class="sxs-lookup"><span data-stu-id="5944b-178">The Html.TextBox() method above takes a single parameter – which is being used to specify both the id/name attributes of the &lt;input type="text"/&gt; element to output, as well as the model property to populate the textbox value from.</span></span> <span data-ttu-id="5944b-179">例如，我们传递到 "编辑" 视图的晚餐对象的 "Title" 属性值为 ".NET 先期"，因此我们的 Html. TextBox （"Title"）方法调用输出： *&lt;输入 id = "title" name = "title" type = "text" value = "Net.tcp 先期备货"/&gt;* 。</span><span class="sxs-lookup"><span data-stu-id="5944b-179">For example, the Dinner object we passed to the Edit view had a "Title" property value of ".NET Futures", and so our Html.TextBox("Title") method call output: *&lt;input id="Title" name="Title" type="text" value=".NET Futures" /&gt;*.</span></span>

<span data-ttu-id="5944b-180">此外，我们还可以使用第一个 Html. TextBox （）参数指定元素的 id/名称，然后将值显式传递为用作第二个参数：</span><span class="sxs-lookup"><span data-stu-id="5944b-180">Alternatively, we can use the first Html.TextBox() parameter to specify the id/name of the element, and then explicitly pass in the value to use as a second parameter:</span></span>

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample6.aspx)]

<span data-ttu-id="5944b-181">通常，我们需要对输出的值执行自定义格式设置。</span><span class="sxs-lookup"><span data-stu-id="5944b-181">Often we'll want to perform custom formatting on the value that is output.</span></span> <span data-ttu-id="5944b-182">内置于 .NET 中的字符串. Format （）静态方法对于这些方案非常有用。</span><span class="sxs-lookup"><span data-stu-id="5944b-182">The String.Format() static method built-into .NET is useful for these scenarios.</span></span> <span data-ttu-id="5944b-183">我们的 "Edit .aspx" 视图模板使用此来设置 EventDate 值（类型为 DateTime 的值）的格式，以便它不会显示时间的秒数：</span><span class="sxs-lookup"><span data-stu-id="5944b-183">Our Edit.aspx view template is using this to format the EventDate value (which is of type DateTime) so that it doesn't show seconds for the time:</span></span>

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample7.aspx)]

<span data-ttu-id="5944b-184">可以选择使用 Html. TextBox （）的第三个参数来输出其他 HTML 特性。</span><span class="sxs-lookup"><span data-stu-id="5944b-184">A third parameter to Html.TextBox() can optionally be used to output additional HTML attributes.</span></span> <span data-ttu-id="5944b-185">下面的代码段演示如何在 &lt;输入类型 = "text"/&gt; 元素上呈现附加大小为 "30" 的属性和类 = "mycssclass" 属性。</span><span class="sxs-lookup"><span data-stu-id="5944b-185">The code-snippet below demonstrates how to render an additional size="30" attribute and a class="mycssclass" attribute on the &lt;input type="text"/&gt; element.</span></span> <span data-ttu-id="5944b-186">请注意，在中C#，如何使用 "@" character because "类" 作为保留关键字来转义类属性的名称：</span><span class="sxs-lookup"><span data-stu-id="5944b-186">Note how we are escaping the name of the class attribute using a "@" character because "class" is a reserved keyword in C#:</span></span>

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample8.aspx)]

#### <a name="implementing-the-http-post-edit-action-method"></a><span data-ttu-id="5944b-187">实现 HTTP POST 编辑操作方法</span><span class="sxs-lookup"><span data-stu-id="5944b-187">Implementing the HTTP-POST Edit Action Method</span></span>

<span data-ttu-id="5944b-188">现在，我们已实现了编辑操作方法的 HTTP 获取版本。</span><span class="sxs-lookup"><span data-stu-id="5944b-188">We now have the HTTP-GET version of our Edit action method implemented.</span></span> <span data-ttu-id="5944b-189">当用户请求 */Dinners/Edit/1* URL 时，他们将收到如下所示的 HTML 页面：</span><span class="sxs-lookup"><span data-stu-id="5944b-189">When a user requests the */Dinners/Edit/1* URL they receive an HTML page like the following:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image6.png)

<span data-ttu-id="5944b-190">按 "保存" 按钮将导致窗体发布到 */Dinners/Edit/1* URL，并使用 HTTP post 谓词提交 HTML &lt;输入&gt; 窗体值。</span><span class="sxs-lookup"><span data-stu-id="5944b-190">Pressing the "Save" button causes a form post to the */Dinners/Edit/1* URL, and submits the HTML &lt;input&gt; form values using the HTTP POST verb.</span></span> <span data-ttu-id="5944b-191">现在，让我们实现编辑操作方法的 HTTP POST 行为-这将处理保存晚餐。</span><span class="sxs-lookup"><span data-stu-id="5944b-191">Let's now implement the HTTP POST behavior of our edit action method – which will handle saving the Dinner.</span></span>

<span data-ttu-id="5944b-192">首先，我们将向 DinnersController 添加一个重载的 "Edit" 操作方法，该方法具有一个 "AcceptVerbs" 属性，指示它处理 HTTP POST 方案：</span><span class="sxs-lookup"><span data-stu-id="5944b-192">We'll begin by adding an overloaded "Edit" action method to our DinnersController that has an "AcceptVerbs" attribute on it that indicates it handles HTTP POST scenarios:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample9.cs)]

<span data-ttu-id="5944b-193">将 [AcceptVerbs] 特性应用于重载操作方法时，ASP.NET MVC 会自动根据传入的 HTTP 谓词来处理向相应操作方法发出的请求。</span><span class="sxs-lookup"><span data-stu-id="5944b-193">When the [AcceptVerbs] attribute is applied to overloaded action methods, ASP.NET MVC automatically handles dispatching requests to the appropriate action method depending on the incoming HTTP verb.</span></span> <span data-ttu-id="5944b-194">对 */Dinners/Edit/[id]* url 发出的 http POST 请求将跳到上述 Edit 方法，而对 */Dinners/Edit/[id]* url 发出的所有其他 HTTP 谓词请求将发送到我们实现的第一个编辑方法（没有 `[AcceptVerbs]` 属性）。</span><span class="sxs-lookup"><span data-stu-id="5944b-194">HTTP POST requests to */Dinners/Edit/[id]* URLs will go to the above Edit method, while all other HTTP verb requests to */Dinners/Edit/[id]* URLs will go to the first Edit method we implemented (which did not have an `[AcceptVerbs]` attribute).</span></span>

| <span data-ttu-id="5944b-195">**侧面主题：为何通过 HTTP 谓词进行区分？**</span><span class="sxs-lookup"><span data-stu-id="5944b-195">**Side Topic: Why differentiate via HTTP verbs?**</span></span> |
| --- |
| <span data-ttu-id="5944b-196">您可能会问，为什么使用单个 URL 并通过 HTTP 谓词来区分其行为呢？</span><span class="sxs-lookup"><span data-stu-id="5944b-196">You might ask – why are we using a single URL and differentiating its behavior via the HTTP verb?</span></span> <span data-ttu-id="5944b-197">为什么不只使用两个单独的 Url 来处理加载和保存编辑更改？</span><span class="sxs-lookup"><span data-stu-id="5944b-197">Why not just have two separate URLs to handle loading and saving edit changes?</span></span> <span data-ttu-id="5944b-198">例如：/Dinners/Edit/[id] 显示初始窗体，并将/Dinners/Save/[id] 用于处理窗体发布以保存该窗体？</span><span class="sxs-lookup"><span data-stu-id="5944b-198">For example: /Dinners/Edit/[id] to display the initial form and /Dinners/Save/[id] to handle the form post to save it?</span></span> <span data-ttu-id="5944b-199">发布两个单独的 Url 的缺点是，在以下情况下，我们将发布到/Dinners/Save/2，然后由于输入错误而需要重新显示 HTML 窗体，最终用户将在其浏览器的地址栏中显示/Dinners/Save/2 URL （因为这是窗体发布到的 URL）。</span><span class="sxs-lookup"><span data-stu-id="5944b-199">The downside with publishing two separate URLs is that in cases where we post to /Dinners/Save/2, and then need to redisplay the HTML form because of an input error, the end-user will end up having the /Dinners/Save/2 URL in their browser's address bar (since that was the URL the form posted to).</span></span> <span data-ttu-id="5944b-200">如果最终用户将此重新显示页面的书签设置为浏览器收藏夹列表，或复制/粘贴该 URL 并将其电子邮件发送给朋友，则他们将最终保存一个以后不起作用的 URL （因为该 URL 依赖于 post 值）。</span><span class="sxs-lookup"><span data-stu-id="5944b-200">If the end-user bookmarks this redisplayed page to their browser favorites list, or copy/pastes the URL and emails it to a friend, they will end up saving a URL that won't work in the future (since that URL depends on post values).</span></span> <span data-ttu-id="5944b-201">通过公开单一 URL （如：/Dinners/Edit/[id]）并区分 HTTP 谓词对其进行处理，最终用户可以将编辑页面加入书签，并/或将 URL 发送给其他人。</span><span class="sxs-lookup"><span data-stu-id="5944b-201">By exposing a single URL (like: /Dinners/Edit/[id]) and differentiating the processing of it by HTTP verb, it is safe for end-users to bookmark the edit page and/or send the URL to others.</span></span> |

#### <a name="retrieving-form-post-values"></a><span data-ttu-id="5944b-202">检索窗体发布值</span><span class="sxs-lookup"><span data-stu-id="5944b-202">Retrieving Form Post Values</span></span>

<span data-ttu-id="5944b-203">可以通过多种方式访问 HTTP POST "编辑" 方法中的已发布表单参数。</span><span class="sxs-lookup"><span data-stu-id="5944b-203">There are a variety of ways we can access posted form parameters within our HTTP POST "Edit" method.</span></span> <span data-ttu-id="5944b-204">一种简单的方法是只使用控制器基类上的 Request 属性访问窗体集合并直接检索已发布的值：</span><span class="sxs-lookup"><span data-stu-id="5944b-204">One simple approach is to just use the Request property on the Controller base class to access the form collection and retrieve the posted values directly:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample10.cs)]

<span data-ttu-id="5944b-205">不过，上述方法稍微详细一些，特别是添加错误处理逻辑。</span><span class="sxs-lookup"><span data-stu-id="5944b-205">The above approach is a little verbose, though, especially once we add error handling logic.</span></span>

<span data-ttu-id="5944b-206">对于此方案，更好的方法是在控制器基类上利用内置的*UpdateModel （）* helper 方法。</span><span class="sxs-lookup"><span data-stu-id="5944b-206">A better approach for this scenario is to leverage the built-in *UpdateModel()* helper method on the Controller base class.</span></span> <span data-ttu-id="5944b-207">它支持使用传入的窗体参数来更新对象的属性。</span><span class="sxs-lookup"><span data-stu-id="5944b-207">It supports updating the properties of an object we pass it using the incoming form parameters.</span></span> <span data-ttu-id="5944b-208">它使用反射来确定对象上的属性名称，然后根据客户端提交的输入值自动转换和分配值。</span><span class="sxs-lookup"><span data-stu-id="5944b-208">It uses reflection to determine the property names on the object, and then automatically converts and assigns values to them based on the input values submitted by the client.</span></span>

<span data-ttu-id="5944b-209">我们可以使用 UpdateModel （）方法来简化使用此代码的 HTTP POST 编辑操作：</span><span class="sxs-lookup"><span data-stu-id="5944b-209">We could use the UpdateModel() method to simplify our HTTP-POST Edit Action using this code:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample11.cs)]

<span data-ttu-id="5944b-210">现在，我们可以访问 */Dinners/Edit/1* URL，更改晚餐的标题：</span><span class="sxs-lookup"><span data-stu-id="5944b-210">We can now visit the */Dinners/Edit/1* URL, and change the title of our Dinner:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image7.png)

<span data-ttu-id="5944b-211">单击 "保存" 按钮时，将对编辑操作执行窗体发布，并且更新的值将保留在数据库中。</span><span class="sxs-lookup"><span data-stu-id="5944b-211">When we click the "Save" button, we'll perform a form post to our Edit action, and the updated values will be persisted in the database.</span></span> <span data-ttu-id="5944b-212">然后，我们将重定向到晚餐的详细信息 URL （将显示新保存的值）：</span><span class="sxs-lookup"><span data-stu-id="5944b-212">We will then be redirected to the Details URL for the Dinner (which will display the newly saved values):</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image8.png)

#### <a name="handling-edit-errors"></a><span data-ttu-id="5944b-213">处理编辑错误</span><span class="sxs-lookup"><span data-stu-id="5944b-213">Handling Edit Errors</span></span>

<span data-ttu-id="5944b-214">当前的 HTTP POST 实现工作正常–出现错误时除外。</span><span class="sxs-lookup"><span data-stu-id="5944b-214">Our current HTTP-POST implementation works fine – except when there are errors.</span></span>

<span data-ttu-id="5944b-215">如果用户编辑窗体时出错，则需要确保窗体重新显示，并显示信息性错误消息，指导他们修复该窗体。</span><span class="sxs-lookup"><span data-stu-id="5944b-215">When a user makes a mistake editing a form, we need to make sure that the form is redisplayed with an informative error message that guides them to fix it.</span></span> <span data-ttu-id="5944b-216">这包括最终用户发布不正确输入（例如：格式错误的日期字符串）的情况，以及输入格式有效但存在业务规则冲突的情况。</span><span class="sxs-lookup"><span data-stu-id="5944b-216">This includes cases where an end-user posts incorrect input (for example: a malformed date string), as well as cases where the input format is valid but there is a business rule violation.</span></span> <span data-ttu-id="5944b-217">出现错误时，窗体应保留用户最初输入的输入数据，以便他们无需手动重填其更改。</span><span class="sxs-lookup"><span data-stu-id="5944b-217">When errors occur the form should preserve the input data the user originally entered so that they don't have to refill their changes manually.</span></span> <span data-ttu-id="5944b-218">此过程应根据需要重复多次，直至窗体成功完成。</span><span class="sxs-lookup"><span data-stu-id="5944b-218">This process should repeat as many times as necessary until the form successfully completes.</span></span>

<span data-ttu-id="5944b-219">ASP.NET MVC 包括一些极好的内置功能，这些功能可简化错误处理并使其变得简单。</span><span class="sxs-lookup"><span data-stu-id="5944b-219">ASP.NET MVC includes some nice built-in features that make error handling and form redisplay easy.</span></span> <span data-ttu-id="5944b-220">若要在操作中查看这些功能，请将编辑操作方法更新为以下代码：</span><span class="sxs-lookup"><span data-stu-id="5944b-220">To see these features in action let's update our Edit action method with the following code:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample12.cs)]

<span data-ttu-id="5944b-221">上面的代码与我们以前的实现类似，只是我们正在包装工作的 try/catch 错误处理块。</span><span class="sxs-lookup"><span data-stu-id="5944b-221">The above code is similar to our previous implementation – except that we are now wrapping a try/catch error handling block around our work.</span></span> <span data-ttu-id="5944b-222">如果在调用 UpdateModel （）时出现异常，或当我们尝试并保存 DinnerRepository 时（如果我们尝试保存的晚餐对象由于模型中的规则冲突而无效，将引发异常），我们的 catch 错误处理块将运行.</span><span class="sxs-lookup"><span data-stu-id="5944b-222">If an exception occurs either when calling UpdateModel(), or when we try and save the DinnerRepository (which will raise an exception if the Dinner object we are trying to save is invalid because of a rule violation within our model), our catch error handling block will execute.</span></span> <span data-ttu-id="5944b-223">在此示例中，我们将遍历晚餐对象中存在的任何规则冲突，并将其添加到 ModelState 对象（我们稍后将对此进行讨论）。</span><span class="sxs-lookup"><span data-stu-id="5944b-223">Within it we loop over any rule violations that exist in the Dinner object and add them to a ModelState object (which we'll discuss shortly).</span></span> <span data-ttu-id="5944b-224">然后重新显示视图。</span><span class="sxs-lookup"><span data-stu-id="5944b-224">We then redisplay the view.</span></span>

<span data-ttu-id="5944b-225">若要查看此工作，请重新运行该应用程序，编辑晚餐，并将其更改为具有空标题，EventDate 为 "假"，并使用英国电话号码，并使用美国国家/地区值。</span><span class="sxs-lookup"><span data-stu-id="5944b-225">To see this working let's re-run the application, edit a Dinner, and change it to have an empty Title, an EventDate of "BOGUS", and use a UK phone number with a country value of USA.</span></span> <span data-ttu-id="5944b-226">当我们按下 "保存" 按钮时，我们的 HTTP POST 编辑方法将不能保存晚餐（因为存在错误）并将重新显示表单：</span><span class="sxs-lookup"><span data-stu-id="5944b-226">When we press the "Save" button our HTTP POST Edit method will not be able to save the Dinner (because there are errors) and will redisplay the form:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image9.png)

<span data-ttu-id="5944b-227">应用程序的错误体验非常不错。</span><span class="sxs-lookup"><span data-stu-id="5944b-227">Our application has a decent error experience.</span></span> <span data-ttu-id="5944b-228">具有无效输入的文本元素以红色突出显示，并向最终用户显示验证错误消息。</span><span class="sxs-lookup"><span data-stu-id="5944b-228">The text elements with the invalid input are highlighted in red, and validation error messages are displayed to the end user about them.</span></span> <span data-ttu-id="5944b-229">窗体还会保留用户最初输入的输入数据，从而无需重新填充任何内容。</span><span class="sxs-lookup"><span data-stu-id="5944b-229">The form is also preserving the input data the user originally entered – so that they don't have to refill anything.</span></span>

<span data-ttu-id="5944b-230">您可能会问，这是不是吗？</span><span class="sxs-lookup"><span data-stu-id="5944b-230">How, you might ask, did this occur?</span></span> <span data-ttu-id="5944b-231">"标题"、"EventDate" 和 "ContactPhone" 文本框的显示效果如何，并知道是否输出最初输入的用户值？</span><span class="sxs-lookup"><span data-stu-id="5944b-231">How did the Title, EventDate, and ContactPhone textboxes highlight themselves in red and know to output the originally entered user values?</span></span> <span data-ttu-id="5944b-232">如何在顶部列表中显示错误消息？</span><span class="sxs-lookup"><span data-stu-id="5944b-232">And how did error messages get displayed in the list at the top?</span></span> <span data-ttu-id="5944b-233">好消息是，这种情况并不是因为，因为我们使用了一些内置的 ASP.NET MVC 功能，使输入验证和错误处理方案变得很简单。</span><span class="sxs-lookup"><span data-stu-id="5944b-233">The good news is that this didn't occur by magic - rather it was because we used some of the built-in ASP.NET MVC features that make input validation and error handling scenarios easy.</span></span>

#### <a name="understanding-modelstate-and-the-validation-html-helper-methods"></a><span data-ttu-id="5944b-234">了解 ModelState 和验证 HTML 帮助器方法</span><span class="sxs-lookup"><span data-stu-id="5944b-234">Understanding ModelState and the Validation HTML Helper Methods</span></span>

<span data-ttu-id="5944b-235">控制器类具有一个 "ModelState" 属性集合，它提供了一种方法，用于指示将模型对象传递到视图时存在错误。</span><span class="sxs-lookup"><span data-stu-id="5944b-235">Controller classes have a "ModelState" property collection which provides a way to indicate that errors exist with a model object being passed to a View.</span></span> <span data-ttu-id="5944b-236">ModelState 集合中的错误条目标识包含问题的模型属性的名称（例如： "Title"、"EventDate" 或 "ContactPhone"），并允许指定用户友好的错误消息（例如： "需要标题"）。</span><span class="sxs-lookup"><span data-stu-id="5944b-236">Error entries within the ModelState collection identify the name of the model property with the issue (for example: "Title", "EventDate", or "ContactPhone"), and allow a human-friendly error message to be specified (for example: "Title is required").</span></span>

<span data-ttu-id="5944b-237">当尝试将窗体值分配给模型对象的属性时， *UpdateModel （）* helper 方法会自动填充 ModelState 集合。</span><span class="sxs-lookup"><span data-stu-id="5944b-237">The *UpdateModel()* helper method automatically populates the ModelState collection when it encounters errors while trying to assign form values to properties on the model object.</span></span> <span data-ttu-id="5944b-238">例如，晚餐对象的 EventDate 属性的类型为 DateTime。</span><span class="sxs-lookup"><span data-stu-id="5944b-238">For example, our Dinner object's EventDate property is of type DateTime.</span></span> <span data-ttu-id="5944b-239">在上述方案中，如果 UpdateModel （）方法无法将字符串值 "假" 赋给它，则 UpdateModel （）方法会将一个条目添加到 ModelState 集合，指示该属性发生了分配错误。</span><span class="sxs-lookup"><span data-stu-id="5944b-239">When the UpdateModel() method was unable to assign the string value "BOGUS" to it in the scenario above, the UpdateModel() method added an entry to the ModelState collection indicating an assignment error had occurred with that property.</span></span>

<span data-ttu-id="5944b-240">开发人员还可以编写代码，以显式将错误条目添加到 ModelState 集合中，如我们在我们的 "catch" 错误处理块中执行的操作。晚餐对象：</span><span class="sxs-lookup"><span data-stu-id="5944b-240">Developers can also write code to explicitly add error entries into the ModelState collection like we are doing below within our "catch" error handling block, which is populating the ModelState collection with entries based on the active Rule Violations in the Dinner object:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample13.cs)]

#### <a name="html-helper-integration-with-modelstate"></a><span data-ttu-id="5944b-241">Html Helper 与 ModelState 的集成</span><span class="sxs-lookup"><span data-stu-id="5944b-241">Html Helper Integration with ModelState</span></span>

<span data-ttu-id="5944b-242">HTML 帮助器方法（如 Html. TextBox （））-在呈现输出时检查 ModelState 集合。</span><span class="sxs-lookup"><span data-stu-id="5944b-242">HTML helper methods - like Html.TextBox() - check the ModelState collection when rendering output.</span></span> <span data-ttu-id="5944b-243">如果该项存在错误，它们将呈现用户输入的值和 CSS 错误类。</span><span class="sxs-lookup"><span data-stu-id="5944b-243">If an error for the item exists, they render the user-entered value and a CSS error class.</span></span>

<span data-ttu-id="5944b-244">例如，在我们的 "编辑" 视图中，我们使用 Html. TextBox （） helper 方法呈现晚餐对象的 EventDate：</span><span class="sxs-lookup"><span data-stu-id="5944b-244">For example, in our "Edit" view we are using the Html.TextBox() helper method to render the EventDate of our Dinner object:</span></span>

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample14.aspx)]

<span data-ttu-id="5944b-245">当在错误情况下呈现视图时，Html. TextBox （）方法检查了 ModelState 集合，以查看是否存在与晚餐对象的 "EventDate" 属性相关联的任何错误。</span><span class="sxs-lookup"><span data-stu-id="5944b-245">When the view was rendered in the error scenario, the Html.TextBox() method checked the ModelState collection to see if there were any errors associated with the "EventDate" property of our Dinner object.</span></span> <span data-ttu-id="5944b-246">当它确定出现错误时，它将提交的用户输入（"假"）作为值，并将 css 错误类添加到它生成的 &lt;输入类型 = "textbox"/&gt; 标记：</span><span class="sxs-lookup"><span data-stu-id="5944b-246">When it determined that there was an error it rendered the submitted user input ("BOGUS") as the value, and added a css error class to the &lt;input type="textbox"/&gt; markup it generated:</span></span>

[!code-html[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample15.html)]

<span data-ttu-id="5944b-247">您可以自定义 css 错误类的外观，以查找所需的外观。</span><span class="sxs-lookup"><span data-stu-id="5944b-247">You can customize the appearance of the css error class to look however you want.</span></span> <span data-ttu-id="5944b-248">默认的 CSS 错误类– "输入验证-错误" –在 *\content\site.css*样式表中定义，如下所示：</span><span class="sxs-lookup"><span data-stu-id="5944b-248">The default CSS error class – "input-validation-error" – is defined in the *\content\site.css* stylesheet and looks like below:</span></span>

[!code-css[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample16.css)]

<span data-ttu-id="5944b-249">此 CSS 规则导致无效输入元素突出显示，如下所示：</span><span class="sxs-lookup"><span data-stu-id="5944b-249">This CSS rule is what caused our invalid input elements to be highlighted like below:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image10.png)

##### <a name="htmlvalidationmessage-helper-method"></a><span data-ttu-id="5944b-250">ValidationMessage （） Helper 方法</span><span class="sxs-lookup"><span data-stu-id="5944b-250">Html.ValidationMessage() Helper Method</span></span>

<span data-ttu-id="5944b-251">ValidationMessage （） helper 方法可用于输出与特定模型属性关联的 ModelState 错误消息：</span><span class="sxs-lookup"><span data-stu-id="5944b-251">The Html.ValidationMessage() helper method can be used to output the ModelState error message associated with a particular model property:</span></span>

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample17.aspx)]

<span data-ttu-id="5944b-252">上面的代码输出： *&lt;范围 = "字段验证-错误"&gt; 值 "虚假" 无效，&lt;/span&gt;*</span><span class="sxs-lookup"><span data-stu-id="5944b-252">The above code outputs: *&lt;span class="field-validation-error"&gt; The value ‘BOGUS' is invalid&lt;/span&gt;*</span></span>

<span data-ttu-id="5944b-253">ValidationMessage （） helper 方法还支持第二个参数，使开发人员能够重写显示的错误文本消息：</span><span class="sxs-lookup"><span data-stu-id="5944b-253">The Html.ValidationMessage() helper method also supports a second parameter that allows developers to override the error text message that is displayed:</span></span>

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample18.aspx)]

<span data-ttu-id="5944b-254">上述代码输出：在 EventDate 属性存在错误时， *&lt;跨类 = "字段验证-错误"&gt;\*&lt;/span&gt;* 而不是默认错误文本。</span><span class="sxs-lookup"><span data-stu-id="5944b-254">The above code outputs: *&lt;span class="field-validation-error"&gt;\*&lt;/span&gt;* instead of the default error text when an error is present for the EventDate property.</span></span>

##### <a name="htmlvalidationsummary-helper-method"></a><span data-ttu-id="5944b-255">ValidationSummary （） Helper 方法</span><span class="sxs-lookup"><span data-stu-id="5944b-255">Html.ValidationSummary() Helper Method</span></span>

<span data-ttu-id="5944b-256">ValidationSummary （） helper 方法可用于呈现摘要错误消息，该消息附带一个 &lt;ul&gt;&lt;li/&gt;&lt;/ul&gt; ModelState 集合中所有详细错误消息的列表：</span><span class="sxs-lookup"><span data-stu-id="5944b-256">The Html.ValidationSummary() helper method can be used to render a summary error message, accompanied by a &lt;ul&gt;&lt;li/&gt;&lt;/ul&gt; list of all detailed error messages in the ModelState collection:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image11.png)

<span data-ttu-id="5944b-257">ValidationSummary （） helper 方法使用可选的字符串参数，该参数定义要显示在详细错误列表上方的摘要错误消息：</span><span class="sxs-lookup"><span data-stu-id="5944b-257">The Html.ValidationSummary() helper method takes an optional string parameter – which defines a summary error message to display above the list of detailed errors:</span></span>

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample19.aspx)]

<span data-ttu-id="5944b-258">您可以选择使用 CSS 来替代 "错误列表" 的外观。</span><span class="sxs-lookup"><span data-stu-id="5944b-258">You can optionally use CSS to override what the error list looks like.</span></span>

#### <a name="using-a-addruleviolations-helper-method"></a><span data-ttu-id="5944b-259">使用 AddRuleViolations Helper 方法</span><span class="sxs-lookup"><span data-stu-id="5944b-259">Using a AddRuleViolations Helper Method</span></span>

<span data-ttu-id="5944b-260">初始的 HTTP POST 编辑实现使用其 catch 块内的 foreach 语句来循环接管晚餐对象的规则冲突，并将其添加到控制器的 ModelState 集合：</span><span class="sxs-lookup"><span data-stu-id="5944b-260">Our initial HTTP-POST Edit implementation used a foreach statement within its catch block to loop over the Dinner object's Rule Violations and add them to the controller's ModelState collection:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample20.cs)]

<span data-ttu-id="5944b-261">我们可以通过将 "ControllerHelpers" 类添加到 NerdDinner 项目中来使此代码变得更清晰，并在其中实现 "AddRuleViolations" 扩展方法，将 helper 方法添加到 ASP.NET MVC ModelStateDictionary 类。</span><span class="sxs-lookup"><span data-stu-id="5944b-261">We can make this code a little cleaner by adding a "ControllerHelpers" class to the NerdDinner project, and implement an "AddRuleViolations" extension method within it that adds a helper method to the ASP.NET MVC ModelStateDictionary class.</span></span> <span data-ttu-id="5944b-262">此扩展方法可以封装用 RuleViolation 错误列表填充 ModelStateDictionary 所需的逻辑：</span><span class="sxs-lookup"><span data-stu-id="5944b-262">This extension method can encapsulate the logic necessary to populate the ModelStateDictionary with a list of RuleViolation errors:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample21.cs)]

<span data-ttu-id="5944b-263">接下来，我们可以更新 HTTP POST 编辑操作方法，使用此扩展方法，通过晚餐规则违规填充 ModelState 集合。</span><span class="sxs-lookup"><span data-stu-id="5944b-263">We can then update our HTTP-POST Edit action method to use this extension method to populate the ModelState collection with our Dinner Rule Violations.</span></span>

#### <a name="complete-edit-action-method-implementations"></a><span data-ttu-id="5944b-264">完成编辑操作方法实现</span><span class="sxs-lookup"><span data-stu-id="5944b-264">Complete Edit Action Method Implementations</span></span>

<span data-ttu-id="5944b-265">下面的代码实现了编辑方案所需的所有控制器逻辑：</span><span class="sxs-lookup"><span data-stu-id="5944b-265">The code below implements all of the controller logic necessary for our Edit scenario:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample22.cs)]

<span data-ttu-id="5944b-266">我们的编辑实现的一个好办法是，我们的控制器类和我们的视图模板都不能了解有关我们的晚餐模型强制执行的特定验证或业务规则的任何信息。</span><span class="sxs-lookup"><span data-stu-id="5944b-266">The nice thing about our Edit implementation is that neither our Controller class nor our View template has to know anything about the specific validation or business rules being enforced by our Dinner model.</span></span> <span data-ttu-id="5944b-267">将来，我们可以在我们的模型中添加更多规则，而无需对控制器或视图进行任何代码更改，就可以对其进行更改。</span><span class="sxs-lookup"><span data-stu-id="5944b-267">We can add additional rules to our model in the future and do not have to make any code changes to our controller or view in order for them to be supported.</span></span> <span data-ttu-id="5944b-268">这为我们提供了灵活的灵活性，可以在将来轻松地轻松地改进应用程序要求，只需进行少量的代码更改。</span><span class="sxs-lookup"><span data-stu-id="5944b-268">This provides us with the flexibility to easily evolve our application requirements in the future with a minimum of code changes.</span></span>

### <a name="create-support"></a><span data-ttu-id="5944b-269">创建支持</span><span class="sxs-lookup"><span data-stu-id="5944b-269">Create Support</span></span>

<span data-ttu-id="5944b-270">我们已经完成了 DinnersController 类的 "编辑" 行为。</span><span class="sxs-lookup"><span data-stu-id="5944b-270">We've finished implementing the "Edit" behavior of our DinnersController class.</span></span> <span data-ttu-id="5944b-271">现在，让我们继续实现对它的 "创建" 支持-这将使用户能够添加新就。</span><span class="sxs-lookup"><span data-stu-id="5944b-271">Let's now move on to implement the "Create" support on it – which will enable users to add new Dinners.</span></span>

#### <a name="the-http-get-create-action-method"></a><span data-ttu-id="5944b-272">HTTP 获取创建操作方法</span><span class="sxs-lookup"><span data-stu-id="5944b-272">The HTTP-GET Create Action Method</span></span>

<span data-ttu-id="5944b-273">首先，我们将实现创建操作方法的 HTTP "GET" 行为。</span><span class="sxs-lookup"><span data-stu-id="5944b-273">We'll begin by implementing the HTTP "GET" behavior of our create action method.</span></span> <span data-ttu-id="5944b-274">当有人访问 */Dinners/Create* URL 时，将调用此方法。</span><span class="sxs-lookup"><span data-stu-id="5944b-274">This method will be called when someone visits the */Dinners/Create* URL.</span></span> <span data-ttu-id="5944b-275">我们的实现如下所示：</span><span class="sxs-lookup"><span data-stu-id="5944b-275">Our implementation looks like:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample23.cs)]

<span data-ttu-id="5944b-276">上面的代码创建一个新的晚餐对象，并将其 EventDate 属性分配为将来一周。</span><span class="sxs-lookup"><span data-stu-id="5944b-276">The code above creates a new Dinner object, and assigns its EventDate property to be one week in the future.</span></span> <span data-ttu-id="5944b-277">然后，它呈现基于新晚餐对象的视图。</span><span class="sxs-lookup"><span data-stu-id="5944b-277">It then renders a View that is based on the new Dinner object.</span></span> <span data-ttu-id="5944b-278">由于我们未将名称显式传递给*view （）* helper 方法，因此它将使用基于约定的默认路径来解析视图模板：/Views/Dinners/Create.aspx。</span><span class="sxs-lookup"><span data-stu-id="5944b-278">Because we haven't explicitly passed a name to the *View()* helper method, it will use the convention based default path to resolve the view template: /Views/Dinners/Create.aspx.</span></span>

<span data-ttu-id="5944b-279">现在，创建此视图模板。</span><span class="sxs-lookup"><span data-stu-id="5944b-279">Let's now create this view template.</span></span> <span data-ttu-id="5944b-280">为此，可以在 "创建操作" 方法中右键单击，然后选择 "添加视图" 上下文菜单命令。</span><span class="sxs-lookup"><span data-stu-id="5944b-280">We can do this by right-clicking within the Create action method and selecting the "Add View" context menu command.</span></span> <span data-ttu-id="5944b-281">在 "添加视图" 对话框中，我们将指出我们要将晚餐对象传递到视图模板，并选择自动基架 "创建" 模板：</span><span class="sxs-lookup"><span data-stu-id="5944b-281">Within the "Add View" dialog we'll indicate that we are passing a Dinner object to the view template, and choose to auto-scaffold a "Create" template:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image12.png)

<span data-ttu-id="5944b-282">单击 "添加" 按钮时，Visual Studio 会将基于基架的新 "Create .aspx" 视图保存到 "\Views\Dinners" 目录中，并在 IDE 中打开它：</span><span class="sxs-lookup"><span data-stu-id="5944b-282">When we click the "Add" button, Visual Studio will save a new scaffold-based "Create.aspx" view to the "\Views\Dinners" directory, and open it up within the IDE:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image13.png)

<span data-ttu-id="5944b-283">让我们对为我们生成的默认 "创建" 基架文件进行一些更改，并将其修改为如下所示：</span><span class="sxs-lookup"><span data-stu-id="5944b-283">Let's make a few changes to the default "create" scaffold file that was generated for us, and modify it up to look like below:</span></span>

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample24.aspx)]

<span data-ttu-id="5944b-284">现在，当我们运行应用程序并访问浏览器内的 *"/Dinners/Create"* URL 时，它会在创建操作实现中呈现如下所示的 UI：</span><span class="sxs-lookup"><span data-stu-id="5944b-284">And now when we run our application and access the *"/Dinners/Create"* URL within the browser it will render UI like below from our Create action implementation:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image14.png)

#### <a name="implementing-the-http-post-create-action-method"></a><span data-ttu-id="5944b-285">实现 HTTP POST 创建操作方法</span><span class="sxs-lookup"><span data-stu-id="5944b-285">Implementing the HTTP-POST Create Action Method</span></span>

<span data-ttu-id="5944b-286">我们已经实现了创建操作方法的 HTTP GET 版本。</span><span class="sxs-lookup"><span data-stu-id="5944b-286">We have the HTTP-GET version of our Create action method implemented.</span></span> <span data-ttu-id="5944b-287">当用户单击 "保存" 按钮时，它将执行窗体发布到 */Dinners/Create* URL，并使用 HTTP post 谓词提交 HTML &lt;输入&gt; 窗体值。</span><span class="sxs-lookup"><span data-stu-id="5944b-287">When a user clicks the "Save" button it performs a form post to the */Dinners/Create* URL, and submits the HTML &lt;input&gt; form values using the HTTP POST verb.</span></span>

<span data-ttu-id="5944b-288">现在，让我们实现 "创建操作" 方法的 HTTP POST 行为。</span><span class="sxs-lookup"><span data-stu-id="5944b-288">Let's now implement the HTTP POST behavior of our create action method.</span></span> <span data-ttu-id="5944b-289">首先，我们将向 DinnersController 添加一个重载的 "Create" 操作方法，该方法的 "AcceptVerbs" 属性指示它处理 HTTP POST 方案：</span><span class="sxs-lookup"><span data-stu-id="5944b-289">We'll begin by adding an overloaded "Create" action method to our DinnersController that has an "AcceptVerbs" attribute on it that indicates it handles HTTP POST scenarios:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample25.cs)]

<span data-ttu-id="5944b-290">可以通过多种方式访问已启用 HTTP POST 的 "创建" 方法中的已发布表单参数。</span><span class="sxs-lookup"><span data-stu-id="5944b-290">There are a variety of ways we can access the posted form parameters within our HTTP-POST enabled "Create" method.</span></span>

<span data-ttu-id="5944b-291">一种方法是创建一个新的晚餐对象，然后使用*UpdateModel （）* helper 方法（与 "编辑" 操作一样），用已发布的表单值来填充它。</span><span class="sxs-lookup"><span data-stu-id="5944b-291">One approach is to create a new Dinner object and then use the *UpdateModel()* helper method (like we did with the Edit action) to populate it with the posted form values.</span></span> <span data-ttu-id="5944b-292">接下来，我们可以将其添加到 DinnerRepository，将其保存到数据库中，然后将用户重定向到详细信息操作，以使用下面的代码显示新创建的晚餐：</span><span class="sxs-lookup"><span data-stu-id="5944b-292">We can then add it to our DinnerRepository, persist it to the database, and redirect the user to our Details action to show the newly created Dinner using the code below:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample26.cs)]

<span data-ttu-id="5944b-293">此外，我们还可以使用一种方法，在此方法中，我们的 Create （）操作方法将晚餐对象作为方法参数。</span><span class="sxs-lookup"><span data-stu-id="5944b-293">Alternatively, we can use an approach where we have our Create() action method take a Dinner object as a method parameter.</span></span> <span data-ttu-id="5944b-294">然后，ASP.NET MVC 将自动实例化新的晚餐对象，使用表单输入填充其属性，并将其传递给操作方法：</span><span class="sxs-lookup"><span data-stu-id="5944b-294">ASP.NET MVC will then automatically instantiate a new Dinner object for us, populate its properties using the form inputs, and pass it to our action method:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample27.cs)]

<span data-ttu-id="5944b-295">上述操作方法通过检查 ModelState 属性来验证是否已使用窗体 post 值成功填充晚餐对象。</span><span class="sxs-lookup"><span data-stu-id="5944b-295">Our action method above verifies that the Dinner object has been successfully populated with the form post values by checking the ModelState.IsValid property.</span></span> <span data-ttu-id="5944b-296">如果存在输入转换问题（例如： "EventDate" 属性的字符串 "虚假"），则此方法将返回 false; 如果有任何问题，则操作方法将重新出现该窗体。</span><span class="sxs-lookup"><span data-stu-id="5944b-296">This will return false if there are input conversion issues (for example: a string of "BOGUS" for the EventDate property), and if there are any issues our action method redisplays the form.</span></span>

<span data-ttu-id="5944b-297">如果输入值有效，则操作方法会尝试将新晚餐添加并保存到 DinnerRepository。</span><span class="sxs-lookup"><span data-stu-id="5944b-297">If the input values are valid, then the action method attempts to add and save the new Dinner to the DinnerRepository.</span></span> <span data-ttu-id="5944b-298">它在 try/catch 块中包装此工作，如果存在任何业务规则冲突（这会导致 dinnerRepository （）方法引发异常），则会重新出现该窗体。</span><span class="sxs-lookup"><span data-stu-id="5944b-298">It wraps this work within a try/catch block and redisplays the form if there are any business rule violations (which would cause the dinnerRepository.Save() method to raise an exception).</span></span>

<span data-ttu-id="5944b-299">若要查看此操作中的错误处理行为，可以请求 */Dinners/Create* URL 并填写有关新晚餐的详细信息。</span><span class="sxs-lookup"><span data-stu-id="5944b-299">To see this error handling behavior in action, we can request the */Dinners/Create* URL and fill out details about a new Dinner.</span></span> <span data-ttu-id="5944b-300">输入或值不正确将导致重新显示 "创建窗体"，其中突出显示的错误如下所示：</span><span class="sxs-lookup"><span data-stu-id="5944b-300">Incorrect input or values will cause the create form to be redisplayed with the errors highlighted like below:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image15.png)

<span data-ttu-id="5944b-301">请注意，我们的 "创建窗体" 将采用与编辑窗体完全相同的验证和业务规则。</span><span class="sxs-lookup"><span data-stu-id="5944b-301">Notice how our Create form is honoring the exact same validation and business rules as our Edit form.</span></span> <span data-ttu-id="5944b-302">这是因为我们的验证和业务规则是在模型中定义的，而不是嵌入在应用程序的 UI 或控制器中。</span><span class="sxs-lookup"><span data-stu-id="5944b-302">This is because our validation and business rules were defined in the model, and were not embedded within the UI or controller of the application.</span></span> <span data-ttu-id="5944b-303">这意味着我们稍后可以在一个位置更改/发展验证或业务规则，并在整个应用程序中应用这些规则。</span><span class="sxs-lookup"><span data-stu-id="5944b-303">This means we can later change/evolve our validation or business rules in a single place and have them apply throughout our application.</span></span> <span data-ttu-id="5944b-304">我们不需要在 "编辑" 或 "创建" 操作方法中更改任何代码，即可自动服从任何新规则或对现有规则的修改。</span><span class="sxs-lookup"><span data-stu-id="5944b-304">We will not have to change any code within either our Edit or Create action methods to automatically honor any new rules or modifications to existing ones.</span></span>

<span data-ttu-id="5944b-305">当我们修复输入值并再次单击 "保存" 按钮时，DinnerRepository 的添加将会成功，并且新的晚餐将添加到数据库中。</span><span class="sxs-lookup"><span data-stu-id="5944b-305">When we fix the input values and click the "Save" button again, our addition to the DinnerRepository will succeed, and a new Dinner will be added to the database.</span></span> <span data-ttu-id="5944b-306">接下来，我们将重定向到 */Dinners/Details/[id]* URL，其中会显示有关新创建的晚餐的详细信息：</span><span class="sxs-lookup"><span data-stu-id="5944b-306">We will then be redirected to the */Dinners/Details/[id]* URL – where we will be presented with details about the newly created Dinner:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image16.png)

### <a name="delete-support"></a><span data-ttu-id="5944b-307">删除支持</span><span class="sxs-lookup"><span data-stu-id="5944b-307">Delete Support</span></span>

<span data-ttu-id="5944b-308">现在，我们将 "删除" 支持添加到我们的 DinnersController。</span><span class="sxs-lookup"><span data-stu-id="5944b-308">Let's now add "Delete" support to our DinnersController.</span></span>

#### <a name="the-http-get-delete-action-method"></a><span data-ttu-id="5944b-309">HTTP 获取删除操作方法</span><span class="sxs-lookup"><span data-stu-id="5944b-309">The HTTP-GET Delete Action Method</span></span>

<span data-ttu-id="5944b-310">首先，我们将实现删除操作方法的 HTTP GET 行为。</span><span class="sxs-lookup"><span data-stu-id="5944b-310">We'll begin by implementing the HTTP GET behavior of our delete action method.</span></span> <span data-ttu-id="5944b-311">当有人访问 */Dinners/Delete/[id]* URL 时，将调用此方法。</span><span class="sxs-lookup"><span data-stu-id="5944b-311">This method will get called when someone visits the */Dinners/Delete/[id]* URL.</span></span> <span data-ttu-id="5944b-312">下面是实现：</span><span class="sxs-lookup"><span data-stu-id="5944b-312">Below is the implementation:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample28.cs)]

<span data-ttu-id="5944b-313">操作方法尝试检索要删除的晚餐。</span><span class="sxs-lookup"><span data-stu-id="5944b-313">The action method attempts to retrieve the Dinner to be deleted.</span></span> <span data-ttu-id="5944b-314">如果晚餐存在，它将基于晚餐对象呈现视图。</span><span class="sxs-lookup"><span data-stu-id="5944b-314">If the Dinner exists it renders a View based on the Dinner object.</span></span> <span data-ttu-id="5944b-315">如果该对象不存在（或已删除），则它将返回一个视图，该视图呈现我们之前为我们的 "详细信息" 操作方法创建的 "NotFound" 视图模板。</span><span class="sxs-lookup"><span data-stu-id="5944b-315">If the object doesn't exist (or has already been deleted) it returns a View that renders the "NotFound" view template we created earlier for our "Details" action method.</span></span>

<span data-ttu-id="5944b-316">可以通过在 "删除" 操作方法中右键单击并选择 "添加视图" 上下文菜单命令来创建 "删除" 视图模板。</span><span class="sxs-lookup"><span data-stu-id="5944b-316">We can create the "Delete" view template by right-clicking within the Delete action method and selecting the "Add View" context menu command.</span></span> <span data-ttu-id="5944b-317">在 "添加视图" 对话框中，我们将指出我们要将晚餐对象作为其模型传递到我们的视图模板，并选择创建一个空模板：</span><span class="sxs-lookup"><span data-stu-id="5944b-317">Within the "Add View" dialog we'll indicate that we are passing a Dinner object to our view template as its model, and choose to create an empty template:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image17.png)

<span data-ttu-id="5944b-318">单击 "添加" 按钮时，Visual Studio 将在 "\Views\Dinners" 目录中为我们添加新的 "删除 .aspx" 视图模板文件。</span><span class="sxs-lookup"><span data-stu-id="5944b-318">When we click the "Add" button, Visual Studio will add a new "Delete.aspx" view template file for us within our "\Views\Dinners" directory.</span></span> <span data-ttu-id="5944b-319">我们会将一些 HTML 和代码添加到模板，以实现如下所示的删除确认屏幕：</span><span class="sxs-lookup"><span data-stu-id="5944b-319">We'll add some HTML and code to the template to implement a delete confirmation screen like below:</span></span>

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample29.aspx)]

<span data-ttu-id="5944b-320">上面的代码将显示要删除的晚餐的标题，如果最终用户单击其中的 "删除" 按钮，则输出 &lt;窗体&gt; 元素，该元素执行向/Dinners/Delete/[id] URL 的 POST。</span><span class="sxs-lookup"><span data-stu-id="5944b-320">The code above displays the title of the Dinner to be deleted, and outputs a &lt;form&gt; element that does a POST to the /Dinners/Delete/[id] URL if the end-user clicks the "Delete" button within it.</span></span>

<span data-ttu-id="5944b-321">当我们运行应用程序并访问有效晚餐对象的 *"/Dinners/Delete/[id]"* URL 时，它将呈现如下所示的 UI：</span><span class="sxs-lookup"><span data-stu-id="5944b-321">When we run our application and access the *"/Dinners/Delete/[id]"* URL for a valid Dinner object it renders UI like below:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image18.png)

| <span data-ttu-id="5944b-322">**侧面主题：为什么要进行 POST？**</span><span class="sxs-lookup"><span data-stu-id="5944b-322">**Side Topic: Why are we doing a POST?**</span></span> |
| --- |
| <span data-ttu-id="5944b-323">您可能会问：我们为什么要在我们的 "删除" 确认屏幕中创建 &lt;表单&gt;？</span><span class="sxs-lookup"><span data-stu-id="5944b-323">You might ask – why did we go through the effort of creating a &lt;form&gt; within our Delete confirmation screen?</span></span> <span data-ttu-id="5944b-324">为什么不只使用标准超链接链接到执行实际删除操作的操作方法？</span><span class="sxs-lookup"><span data-stu-id="5944b-324">Why not just use a standard hyperlink to link to an action method that does the actual delete operation?</span></span> <span data-ttu-id="5944b-325">原因在于，我们想要小心防范 web 爬网程序和搜索引擎查找 Url，并在出现以下链接时意外导致数据被删除。</span><span class="sxs-lookup"><span data-stu-id="5944b-325">The reason is because we want to be careful to guard against web-crawlers and search engines discovering our URLs and inadvertently causing data to be deleted when they follow the links.</span></span> <span data-ttu-id="5944b-326">基于 HTTP GET 的 Url 被视为 "安全"，以便它们能够访问/爬网，它们应该不遵循 HTTP POST。</span><span class="sxs-lookup"><span data-stu-id="5944b-326">HTTP-GET based URLs are considered "safe" for them to access/crawl, and they are supposed to not follow HTTP-POST ones.</span></span> <span data-ttu-id="5944b-327">一个好的规则是确保始终将破坏性或数据修改操作置于 HTTP POST 请求后面。</span><span class="sxs-lookup"><span data-stu-id="5944b-327">A good rule is to make sure you always put destructive or data modifying operations behind HTTP-POST requests.</span></span> |

#### <a name="implementing-the-http-post-delete-action-method"></a><span data-ttu-id="5944b-328">实现 HTTP POST 删除操作方法</span><span class="sxs-lookup"><span data-stu-id="5944b-328">Implementing the HTTP-POST Delete Action Method</span></span>

<span data-ttu-id="5944b-329">现在，我们已实现了 "删除" 操作方法的 HTTP 获取版本，其中显示了 "删除" 确认屏幕。</span><span class="sxs-lookup"><span data-stu-id="5944b-329">We now have the HTTP-GET version of our Delete action method implemented which displays a delete confirmation screen.</span></span> <span data-ttu-id="5944b-330">当最终用户单击 "删除" 按钮时，它将对 */Dinners/Dinner/[id]* URL 执行窗体发布。</span><span class="sxs-lookup"><span data-stu-id="5944b-330">When an end user clicks the "Delete" button it will perform a form post to the */Dinners/Dinner/[id]* URL.</span></span>

<span data-ttu-id="5944b-331">现在，让我们使用下面的代码来实现 delete 操作方法的 HTTP "POST" 行为：</span><span class="sxs-lookup"><span data-stu-id="5944b-331">Let's now implement the HTTP "POST" behavior of the delete action method using the code below:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample30.cs)]

<span data-ttu-id="5944b-332">删除操作方法的 HTTP POST 版本尝试检索要删除的晚餐对象。</span><span class="sxs-lookup"><span data-stu-id="5944b-332">The HTTP-POST version of our Delete action method attempts to retrieve the dinner object to delete.</span></span> <span data-ttu-id="5944b-333">如果找不到它（因为已删除），则它将呈现我们的 "NotFound" 模板。</span><span class="sxs-lookup"><span data-stu-id="5944b-333">If it can't find it (because it has already been deleted) it renders our "NotFound" template.</span></span> <span data-ttu-id="5944b-334">如果找到晚餐，则会将其从 DinnerRepository 中删除。</span><span class="sxs-lookup"><span data-stu-id="5944b-334">If it finds the Dinner, it deletes it from the DinnerRepository.</span></span> <span data-ttu-id="5944b-335">然后呈现 "已删除" 模板。</span><span class="sxs-lookup"><span data-stu-id="5944b-335">It then renders a "Deleted" template.</span></span>

<span data-ttu-id="5944b-336">若要实现 "已删除" 模板，我们将在操作方法中右键单击，然后选择 "添加视图" 上下文菜单。</span><span class="sxs-lookup"><span data-stu-id="5944b-336">To implement the "Deleted" template we'll right-click in the action method and choose the "Add View" context menu.</span></span> <span data-ttu-id="5944b-337">我们会将视图命名为 "已删除"，并将其命名为空模板（而不采用强类型模型对象）。</span><span class="sxs-lookup"><span data-stu-id="5944b-337">We'll name our view "Deleted" and have it be an empty template (and not take a strongly-typed model object).</span></span> <span data-ttu-id="5944b-338">然后，将一些 HTML 内容添加到其中：</span><span class="sxs-lookup"><span data-stu-id="5944b-338">We'll then add some HTML content to it:</span></span>

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample31.aspx)]

<span data-ttu-id="5944b-339">现在，当我们运行应用程序并访问有效晚餐对象的 *"/Dinners/Delete/[id]"* URL 时，它将呈现我们的晚餐删除确认屏幕，如下所示：</span><span class="sxs-lookup"><span data-stu-id="5944b-339">And now when we run our application and access the *"/Dinners/Delete/[id]"* URL for a valid Dinner object it will render our Dinner delete confirmation screen like below:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image19.png)

<span data-ttu-id="5944b-340">当我们单击 "删除" 按钮时，它将对 */Dinners/Delete/[id]* URL 执行 HTTP POST，该 URL 将从数据库中删除晚餐，并显示 "已删除" 视图模板：</span><span class="sxs-lookup"><span data-stu-id="5944b-340">When we click the "Delete" button it will perform an HTTP-POST to the */Dinners/Delete/[id]* URL, which will delete the Dinner from our database, and display our "Deleted" view template:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image20.png)

### <a name="model-binding-security"></a><span data-ttu-id="5944b-341">模型绑定安全性</span><span class="sxs-lookup"><span data-stu-id="5944b-341">Model Binding Security</span></span>

<span data-ttu-id="5944b-342">我们讨论了两种不同的方法来使用 ASP.NET MVC 的内置模型绑定功能。</span><span class="sxs-lookup"><span data-stu-id="5944b-342">We've discussed two different ways to use the built-in model-binding features of ASP.NET MVC.</span></span> <span data-ttu-id="5944b-343">第一种方法是使用 UpdateModel （）方法来更新现有模型对象上的属性，第二种方法是使用 ASP.NET MVC 支持将模型对象作为操作方法参数传入。</span><span class="sxs-lookup"><span data-stu-id="5944b-343">The first using the UpdateModel() method to update properties on an existing model object, and the second using ASP.NET MVC's support for passing model objects in as action method parameters.</span></span> <span data-ttu-id="5944b-344">这两种方法都非常强大且非常有用。</span><span class="sxs-lookup"><span data-stu-id="5944b-344">Both of these techniques are very powerful and extremely useful.</span></span>

<span data-ttu-id="5944b-345">此功能还具有 it 责任。</span><span class="sxs-lookup"><span data-stu-id="5944b-345">This power also brings with it responsibility.</span></span> <span data-ttu-id="5944b-346">在接受任何用户输入时始终偏执安全，这一点很重要，在将对象绑定到表单输入时也是如此。</span><span class="sxs-lookup"><span data-stu-id="5944b-346">It is important to always be paranoid about security when accepting any user input, and this is also true when binding objects to form input.</span></span> <span data-ttu-id="5944b-347">应注意始终对任何用户输入的值进行 HTML 编码，以避免 HTML 和 JavaScript 注入攻击，并小心 SQL 注入式攻击（注意：我们使用的是应用程序的 LINQ to SQL，这会自动对参数进行编码，以防止出现这种情况攻击类型）。</span><span class="sxs-lookup"><span data-stu-id="5944b-347">You should be careful to always HTML encode any user-entered values to avoid HTML and JavaScript injection attacks, and be careful of SQL injection attacks (note: we are using LINQ to SQL for our application, which automatically encodes parameters to prevent these types of attacks).</span></span> <span data-ttu-id="5944b-348">切勿单独依赖于客户端验证，始终使用服务器端验证来防止黑客尝试发送虚假值。</span><span class="sxs-lookup"><span data-stu-id="5944b-348">You should never rely on client-side validation alone, and always employ server-side validation to guard against hackers attempting to send you bogus values.</span></span>

<span data-ttu-id="5944b-349">另外一个安全项目，请确保你在使用 ASP.NET MVC 的绑定功能时要考虑的是要绑定的对象的范围。</span><span class="sxs-lookup"><span data-stu-id="5944b-349">One additional security item to make sure you think about when using the binding features of ASP.NET MVC is the scope of the objects you are binding.</span></span> <span data-ttu-id="5944b-350">具体而言，你需要确保了解你允许绑定的属性的安全影响，并确保仅允许更新最终用户可以更新的那些属性，这一点非常明显。</span><span class="sxs-lookup"><span data-stu-id="5944b-350">Specifically, you want to make sure you understand the security implications of the properties you are allowing to be bound, and make sure you only allow those properties that really should be updatable by an end-user to be updated.</span></span>

<span data-ttu-id="5944b-351">默认情况下，UpdateModel （）方法将尝试更新与传入窗体参数值匹配的模型对象的所有属性。</span><span class="sxs-lookup"><span data-stu-id="5944b-351">By default, the UpdateModel() method will attempt to update all properties on the model object that match incoming form parameter values.</span></span> <span data-ttu-id="5944b-352">同样，作为操作方法参数传递的对象也会在默认情况下通过窗体参数设置其所有属性。</span><span class="sxs-lookup"><span data-stu-id="5944b-352">Likewise, objects passed as action method parameters also by default can have all of their properties set via form parameters.</span></span>

#### <a name="locking-down-binding-on-a-per-usage-basis"></a><span data-ttu-id="5944b-353">按使用情况锁定绑定</span><span class="sxs-lookup"><span data-stu-id="5944b-353">Locking down binding on a per-usage basis</span></span>

<span data-ttu-id="5944b-354">可以通过提供可更新的属性的显式 "包含列表"，按使用情况锁定绑定策略。</span><span class="sxs-lookup"><span data-stu-id="5944b-354">You can lock down the binding policy on a per-usage basis by providing an explicit "include list" of properties that can be updated.</span></span> <span data-ttu-id="5944b-355">为此，可将额外的字符串数组参数传递给 UpdateModel （）方法，如下所示：</span><span class="sxs-lookup"><span data-stu-id="5944b-355">This can be done by passing an extra string array parameter to the UpdateModel() method like below:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample32.cs)]

<span data-ttu-id="5944b-356">作为操作方法参数传递的对象还支持 "[Bind]" 属性，该属性可指定如下所示的 "允许" 属性的 "包含列表"：</span><span class="sxs-lookup"><span data-stu-id="5944b-356">Objects passed as action method parameters also support a [Bind] attribute that enables an "include list" of allowed properties to be specified like below:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample33.cs)]

#### <a name="locking-down-binding-on-a-type-basis"></a><span data-ttu-id="5944b-357">基于类型锁定绑定</span><span class="sxs-lookup"><span data-stu-id="5944b-357">Locking down binding on a type basis</span></span>

<span data-ttu-id="5944b-358">你还可以基于每个类型锁定绑定规则。</span><span class="sxs-lookup"><span data-stu-id="5944b-358">You can also lock down the binding rules on a per-type basis.</span></span> <span data-ttu-id="5944b-359">这允许您指定一次绑定规则，然后将它们应用于所有控制器和操作方法的所有方案（包括 UpdateModel 和操作方法参数方案）。</span><span class="sxs-lookup"><span data-stu-id="5944b-359">This allows you to specify the binding rules once, and then have them apply in all scenarios (including both UpdateModel and action method parameter scenarios) across all controllers and action methods.</span></span>

<span data-ttu-id="5944b-360">您可以自定义每种类型的绑定规则，方法是将 [Bind] 特性添加到类型上，或在应用程序的 global.asax 文件中注册它（对于不属于该类型的方案非常有用）。</span><span class="sxs-lookup"><span data-stu-id="5944b-360">You can customize the per-type binding rules by adding a [Bind] attribute onto a type, or by registering it within the Global.asax file of the application (useful for scenarios where you don't own the type).</span></span> <span data-ttu-id="5944b-361">然后，可以使用 Bind 特性的 Include 和 Exclude 属性控制哪些属性可绑定到特定类或接口。</span><span class="sxs-lookup"><span data-stu-id="5944b-361">You can then use the Bind attribute's Include and Exclude properties to control which properties are bindable for the particular class or interface.</span></span>

<span data-ttu-id="5944b-362">我们将为 NerdDinner 应用程序中的晚餐类使用此技术，并向其添加一个 "[Bind]" 属性，将可绑定属性列表限制如下：</span><span class="sxs-lookup"><span data-stu-id="5944b-362">We'll use this technique for the Dinner class in our NerdDinner application, and add a [Bind] attribute to it that restricts the list of bindable properties to the following:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample34.cs)]

<span data-ttu-id="5944b-363">请注意，我们不允许通过绑定操作 RSVPs 集合，也不允许通过绑定设置 DinnerID 或 HostedBy 属性。</span><span class="sxs-lookup"><span data-stu-id="5944b-363">Notice we are not allowing the RSVPs collection to be manipulated via binding, nor are we allowing the DinnerID or HostedBy properties to be set via binding.</span></span> <span data-ttu-id="5944b-364">出于安全原因，我们将改为仅使用操作方法中的显式代码来操作这些特定属性。</span><span class="sxs-lookup"><span data-stu-id="5944b-364">For security reasons we'll instead only manipulate these particular properties using explicit code within our action methods.</span></span>

### <a name="crud-wrap-up"></a><span data-ttu-id="5944b-365">CRUD 向上环绕</span><span class="sxs-lookup"><span data-stu-id="5944b-365">CRUD Wrap-Up</span></span>

<span data-ttu-id="5944b-366">ASP.NET MVC 包含许多可帮助实现窗体发布方案的内置功能。</span><span class="sxs-lookup"><span data-stu-id="5944b-366">ASP.NET MVC includes a number of built-in features that help with implementing form posting scenarios.</span></span> <span data-ttu-id="5944b-367">我们使用了各种功能，在我们的 DinnerRepository 上提供 CRUD UI 支持。</span><span class="sxs-lookup"><span data-stu-id="5944b-367">We used a variety of these features to provide CRUD UI support on top of our DinnerRepository.</span></span>

<span data-ttu-id="5944b-368">我们使用以模型为中心的方法来实现我们的应用程序。</span><span class="sxs-lookup"><span data-stu-id="5944b-368">We are using a model-focused approach to implement our application.</span></span> <span data-ttu-id="5944b-369">这意味着，所有验证和业务规则逻辑都是在模型层中定义的，而不是在我们的控制器或视图中定义的。</span><span class="sxs-lookup"><span data-stu-id="5944b-369">This means that all our validation and business rule logic is defined within our model layer – and not within our controllers or views.</span></span> <span data-ttu-id="5944b-370">我们的控制器类和我们的视图模板都不知道我们的晚餐模型类强制执行的特定业务规则。</span><span class="sxs-lookup"><span data-stu-id="5944b-370">Neither our Controller class nor our View templates know anything about the specific business rules being enforced by our Dinner model class.</span></span>

<span data-ttu-id="5944b-371">这会使应用程序体系结构保持整洁，并使测试更容易。</span><span class="sxs-lookup"><span data-stu-id="5944b-371">This will keep our application architecture clean and make it easier to test.</span></span> <span data-ttu-id="5944b-372">将来，我们可以将其他业务规则添加到我们的模型层中，而无需对控制器或视图*进行任何代码更改*，即可获得支持。</span><span class="sxs-lookup"><span data-stu-id="5944b-372">We can add additional business rules to our model layer in the future and *not have to make any code changes* to our Controller or View in order for them to be supported.</span></span> <span data-ttu-id="5944b-373">这将为我们提供大量的灵活性，以便在将来发展和更改应用程序。</span><span class="sxs-lookup"><span data-stu-id="5944b-373">This is going to provide us with a great deal of agility to evolve and change our application in the future.</span></span>

<span data-ttu-id="5944b-374">我们的 DinnersController 现在启用晚餐列表/详细信息，以及创建、编辑和删除支持。</span><span class="sxs-lookup"><span data-stu-id="5944b-374">Our DinnersController now enables Dinner listings/details, as well as create, edit and delete support.</span></span> <span data-ttu-id="5944b-375">可以在下面找到类的完整代码：</span><span class="sxs-lookup"><span data-stu-id="5944b-375">The complete code for the class can be found below:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample35.cs)]

### <a name="next-step"></a><span data-ttu-id="5944b-376">下一步</span><span class="sxs-lookup"><span data-stu-id="5944b-376">Next Step</span></span>

<span data-ttu-id="5944b-377">现在，我们在 DinnersController 类中拥有基本的 CRUD （创建、读取、更新和删除）支持。</span><span class="sxs-lookup"><span data-stu-id="5944b-377">We now have basic CRUD (Create, Read, Update and Delete) support implement within our DinnersController class.</span></span>

<span data-ttu-id="5944b-378">现在我们来看看如何使用 ViewData 和 ViewModel 类在窗体上实现甚至更丰富的 UI。</span><span class="sxs-lookup"><span data-stu-id="5944b-378">Let's now look at how we can use ViewData and ViewModel classes to enable even richer UI on our forms.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="5944b-379">[上一页](use-controllers-and-views-to-implement-a-listingdetails-ui.md)
> [下一页](use-viewdata-and-implement-viewmodel-classes.md)</span><span class="sxs-lookup"><span data-stu-id="5944b-379">[Previous](use-controllers-and-views-to-implement-a-listingdetails-ui.md)
[Next](use-viewdata-and-implement-viewmodel-classes.md)</span></span>
