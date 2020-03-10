---
uid: mvc/overview/older-versions-1/nerddinner/re-use-ui-using-master-pages-and-partials
title: 使用母版页和分区重复使用 UI |Microsoft Docs
author: microsoft
description: 步骤7介绍了如何在视图模板中应用 "晾干原则" 以消除代码重复，使用分部视图模板和母版页。
ms.author: riande
ms.date: 07/27/2010
ms.assetid: d4243a4a-e91c-4116-9ae0-5c08e5285677
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/re-use-ui-using-master-pages-and-partials
msc.type: authoredcontent
ms.openlocfilehash: 0b17cb6ac14b7f187bf1f175097a37907689d46e
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78468722"
---
# <a name="re-use-ui-using-master-pages-and-partials"></a><span data-ttu-id="a3a4d-103">使用母版页和部分重用 UI</span><span class="sxs-lookup"><span data-stu-id="a3a4d-103">Re-use UI Using Master Pages and Partials</span></span>

<span data-ttu-id="a3a4d-104">由[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="a3a4d-104">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="a3a4d-105">下载 PDF</span><span class="sxs-lookup"><span data-stu-id="a3a4d-105">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="a3a4d-106">这是免费的["NerdDinner" 应用程序教程](introducing-the-nerddinner-tutorial.md)的第7步，该教程演示如何使用 ASP.NET MVC 1 构建小型但完整的 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="a3a4d-106">This is step 7 of a free ["NerdDinner" application tutorial](introducing-the-nerddinner-tutorial.md) that walks-through how to build a small, but complete, web application using ASP.NET MVC 1.</span></span>
> 
> <span data-ttu-id="a3a4d-107">步骤7介绍了如何在视图模板中应用 "晾干原则" 以消除代码重复，使用分部视图模板和母版页。</span><span class="sxs-lookup"><span data-stu-id="a3a4d-107">Step 7 looks at ways we can apply the "DRY Principle" within our view templates to eliminate code duplication, using partial view templates and master pages.</span></span>
> 
> <span data-ttu-id="a3a4d-108">如果你使用的是 ASP.NET MVC 3，则建议你遵循[MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)或[Mvc 音乐应用商店](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)教程中的入门。</span><span class="sxs-lookup"><span data-stu-id="a3a4d-108">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>

## <a name="nerddinner-step-7-partials-and-master-pages"></a><span data-ttu-id="a3a4d-109">NerdDinner 步骤7：分区和母版页</span><span class="sxs-lookup"><span data-stu-id="a3a4d-109">NerdDinner Step 7: Partials and Master Pages</span></span>

<span data-ttu-id="a3a4d-110">MVC 所涉及的设计原则之一是 "不重复自己" 原则（通常称为 "干燥"）。</span><span class="sxs-lookup"><span data-stu-id="a3a4d-110">One of the design philosophies ASP.NET MVC embraces is the "Do Not Repeat Yourself" principle (commonly referred to as "DRY").</span></span> <span data-ttu-id="a3a4d-111">晾干设计有助于消除代码和逻辑的重复，最终使应用程序更快地进行构建和维护。</span><span class="sxs-lookup"><span data-stu-id="a3a4d-111">A DRY design helps eliminate the duplication of code and logic, which ultimately makes applications faster to build and easier to maintain.</span></span>

<span data-ttu-id="a3a4d-112">我们已经了解了在我们的多个 NerdDinner 方案中应用的晾干原则。</span><span class="sxs-lookup"><span data-stu-id="a3a4d-112">We've already seen the DRY principle applied in several of our NerdDinner scenarios.</span></span> <span data-ttu-id="a3a4d-113">几个示例：我们的验证逻辑是在模型层中实现的，这使其能够在控制器的编辑和创建方案中强制执行;我们正在跨编辑、详细信息和删除操作方法重复使用 "NotFound" 视图模板;我们正在将约定命名模式与我们的视图模板结合使用，这样就无需在调用 View （） helper 方法时显式指定名称;同时，我们还将为 "编辑" 和 "创建" 操作方案重复使用 DinnerFormViewModel 类。</span><span class="sxs-lookup"><span data-stu-id="a3a4d-113">A few examples: our validation logic is implemented within our model layer, which enables it to be enforced across both edit and create scenarios in our controller; we are re-using the "NotFound" view template across the Edit, Details and Delete action methods; we are using a convention- naming pattern with our view templates, which eliminates the need to explicitly specify the name when we call the View() helper method; and we are re-using the DinnerFormViewModel class for both Edit and Create action scenarios.</span></span>

<span data-ttu-id="a3a4d-114">现在，我们来看看如何在视图模板中应用 "晾干原则" 来消除代码重复。</span><span class="sxs-lookup"><span data-stu-id="a3a4d-114">Let's now look at ways we can apply the "DRY Principle" within our view templates to eliminate code duplication there as well.</span></span>

### <a name="re-visiting-our-edit-and-create-view-templates"></a><span data-ttu-id="a3a4d-115">重新访问编辑和创建视图模板</span><span class="sxs-lookup"><span data-stu-id="a3a4d-115">Re-visiting our Edit and Create View Templates</span></span>

<span data-ttu-id="a3a4d-116">目前，我们使用两个不同的视图模板： "Edit .aspx" 和 "创建 .aspx"-显示晚餐窗体 UI。</span><span class="sxs-lookup"><span data-stu-id="a3a4d-116">Currently we are using two different view templates – "Edit.aspx" and "Create.aspx" – to display our Dinner form UI.</span></span> <span data-ttu-id="a3a4d-117">快速直观地比较它们重点介绍它们的相似之处。</span><span class="sxs-lookup"><span data-stu-id="a3a4d-117">A quick visual comparison of them highlights how similar they are.</span></span> <span data-ttu-id="a3a4d-118">"创建窗体" 如下所示：</span><span class="sxs-lookup"><span data-stu-id="a3a4d-118">Below is what the create form looks like:</span></span>

![](re-use-ui-using-master-pages-and-partials/_static/image1.png)

<span data-ttu-id="a3a4d-119">下面是 "编辑" 窗体的外观：</span><span class="sxs-lookup"><span data-stu-id="a3a4d-119">And here is what our "Edit" form looks like:</span></span>

![](re-use-ui-using-master-pages-and-partials/_static/image2.png)

<span data-ttu-id="a3a4d-120">这不是什么不同？</span><span class="sxs-lookup"><span data-stu-id="a3a4d-120">Not much of a difference is there?</span></span> <span data-ttu-id="a3a4d-121">除了标题文本和标题文本，窗体布局和输入控件都是相同的。</span><span class="sxs-lookup"><span data-stu-id="a3a4d-121">Other than the title and header text, the form layout and input controls are identical.</span></span>

<span data-ttu-id="a3a4d-122">如果我们打开 "Edit .aspx" 和 "创建 .aspx" 视图模板，则会发现它们包含完全相同的窗体布局和输入控制代码。</span><span class="sxs-lookup"><span data-stu-id="a3a4d-122">If we open up the "Edit.aspx" and "Create.aspx" view templates we'll find that they contain identical form layout and input control code.</span></span> <span data-ttu-id="a3a4d-123">这种重复意味着，我们最终需要在引入或更改新晚餐财产时进行两次更改-这不是好的。</span><span class="sxs-lookup"><span data-stu-id="a3a4d-123">This duplication means we end up having to make changes twice anytime we introduce or change a new Dinner property - which is not good.</span></span>

### <a name="using-partial-view-templates"></a><span data-ttu-id="a3a4d-124">使用分部视图模板</span><span class="sxs-lookup"><span data-stu-id="a3a4d-124">Using Partial View Templates</span></span>

<span data-ttu-id="a3a4d-125">ASP.NET MVC 支持定义 "分部视图" 模板的功能，这些模板可用于封装页面子部分的视图呈现逻辑。</span><span class="sxs-lookup"><span data-stu-id="a3a4d-125">ASP.NET MVC supports the ability to define "partial view" templates that can be used to encapsulate view rendering logic for a sub-portion of a page.</span></span> <span data-ttu-id="a3a4d-126">"分区" 提供一种将视图呈现逻辑定义一次的有效方法，然后在应用程序的多个位置重复使用它。</span><span class="sxs-lookup"><span data-stu-id="a3a4d-126">"Partials" provide a useful way to define view rendering logic once, and then re-use it in multiple places across an application.</span></span>

<span data-ttu-id="a3a4d-127">为了帮助 "晾干" 我们的 "编辑 .aspx" 和 "创建 .aspx" 视图模板重复，我们可以创建一个名为 "DinnerForm" 的分部视图模板，该模板封装了这两个窗体布局和公用的输入元素。</span><span class="sxs-lookup"><span data-stu-id="a3a4d-127">To help "DRY-up" our Edit.aspx and Create.aspx view template duplication, we can create a partial view template named "DinnerForm.ascx" that encapsulates the form layout and input elements common to both.</span></span> <span data-ttu-id="a3a4d-128">为此，请右键单击/Views/Dinners 目录，然后选择 "添加&gt;视图" 菜单命令：</span><span class="sxs-lookup"><span data-stu-id="a3a4d-128">We'll do this by right-clicking on our /Views/Dinners directory and choosing the "Add-&gt;View" menu command:</span></span>

![](re-use-ui-using-master-pages-and-partials/_static/image3.png)

<span data-ttu-id="a3a4d-129">这会显示 "添加视图" 对话框。</span><span class="sxs-lookup"><span data-stu-id="a3a4d-129">This will display the "Add View" dialog.</span></span> <span data-ttu-id="a3a4d-130">我们将为要创建的新视图命名为 "DinnerForm"，在对话框中选择 "创建分部视图" 复选框，并指示我们将向其传递一个 DinnerFormViewModel 类：</span><span class="sxs-lookup"><span data-stu-id="a3a4d-130">We'll name the new view we want to create "DinnerForm", select the "Create a partial view" checkbox within the dialog, and indicate that we will pass it a DinnerFormViewModel class:</span></span>

![](re-use-ui-using-master-pages-and-partials/_static/image4.png)

<span data-ttu-id="a3a4d-131">单击 "添加" 按钮时，Visual Studio 将在 "\Views\Dinners" 目录中为我们创建一个新的 "DinnerForm" 视图模板。</span><span class="sxs-lookup"><span data-stu-id="a3a4d-131">When we click the "Add" button, Visual Studio will create a new "DinnerForm.ascx" view template for us within the "\Views\Dinners" directory.</span></span>

<span data-ttu-id="a3a4d-132">然后，可以将重复的窗体布局/输入控件代码从我们的 "Edit .aspx/Create .aspx" 视图模板复制/粘贴到新的 "DinnerForm" 分部视图模板：</span><span class="sxs-lookup"><span data-stu-id="a3a4d-132">We can then copy/paste the duplicate form layout / input control code from our Edit.aspx/ Create.aspx view templates into our new "DinnerForm.ascx" partial view template:</span></span>

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample1.aspx)]

<span data-ttu-id="a3a4d-133">然后，我们可以更新编辑和创建视图模板来调用 DinnerForm 部分模板，并消除窗体复制。</span><span class="sxs-lookup"><span data-stu-id="a3a4d-133">We can then update our Edit and Create view templates to call the DinnerForm partial template and eliminate the form duplication.</span></span> <span data-ttu-id="a3a4d-134">可以通过在视图模板中调用 RenderPartial （"DinnerForm"）来实现此目的：</span><span class="sxs-lookup"><span data-stu-id="a3a4d-134">We can do this by calling Html.RenderPartial("DinnerForm") within our view templates:</span></span>

##### <a name="createaspx"></a><span data-ttu-id="a3a4d-135">创建 .aspx</span><span class="sxs-lookup"><span data-stu-id="a3a4d-135">Create.aspx</span></span>

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample2.aspx)]

##### <a name="editaspx"></a><span data-ttu-id="a3a4d-136">Edit.aspx</span><span class="sxs-lookup"><span data-stu-id="a3a4d-136">Edit.aspx</span></span>

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample3.aspx)]

<span data-ttu-id="a3a4d-137">调用 RenderPartial 时，可以显式限定所需的部分模板的路径（例如： ~ Views/就/DinnerForm）。</span><span class="sxs-lookup"><span data-stu-id="a3a4d-137">You can explicitly qualify the path of the partial template you want when calling Html.RenderPartial (for example: ~Views/Dinners/DinnerForm.ascx").</span></span> <span data-ttu-id="a3a4d-138">然而，在上面的代码中，我们在 ASP.NET MVC 中利用了基于约定的命名模式，并且只是将 "DinnerForm" 指定为要呈现的部分的名称。</span><span class="sxs-lookup"><span data-stu-id="a3a4d-138">In our code above, though, we are taking advantage of the convention-based naming pattern within ASP.NET MVC, and just specifying "DinnerForm" as the name of the partial to render.</span></span> <span data-ttu-id="a3a4d-139">如果执行此操作，ASP.NET MVC 将首先在基于约定的视图目录中查找（对于 DinnersController，这将是/Views/Dinners）。</span><span class="sxs-lookup"><span data-stu-id="a3a4d-139">When we do this ASP.NET MVC will look first in the convention-based views directory (for DinnersController this would be /Views/Dinners).</span></span> <span data-ttu-id="a3a4d-140">如果未找到部分模板，它将在/Views/Shared 目录中查找它。</span><span class="sxs-lookup"><span data-stu-id="a3a4d-140">If it doesn't find the partial template there it will then look for it in the /Views/Shared directory.</span></span>

<span data-ttu-id="a3a4d-141">如果调用 RenderPartial （）时只使用分部视图的名称，则 ASP.NET MVC 将向分部视图传递调用视图模板所使用的同一个模型和 ViewData 字典对象。</span><span class="sxs-lookup"><span data-stu-id="a3a4d-141">When Html.RenderPartial() is called with just the name of the partial view, ASP.NET MVC will pass to the partial view the same Model and ViewData dictionary objects used by the calling view template.</span></span> <span data-ttu-id="a3a4d-142">另外，还存在 RenderPartial （）的重载版本，使你能够传递替代模型对象和/或 ViewData 字典，使分部视图可以使用。</span><span class="sxs-lookup"><span data-stu-id="a3a4d-142">Alternatively, there are overloaded versions of Html.RenderPartial() that enable you to pass an alternate Model object and/or ViewData dictionary for the partial view to use.</span></span> <span data-ttu-id="a3a4d-143">这对于只需传递完整模型/ViewModel 的子集的情况非常有用。</span><span class="sxs-lookup"><span data-stu-id="a3a4d-143">This is useful for scenarios where you only want to pass a subset of the full Model/ViewModel.</span></span>

| <span data-ttu-id="a3a4d-144">**边主题：为什么 &lt;%%&gt; 而不是 &lt;% =%&gt;？**</span><span class="sxs-lookup"><span data-stu-id="a3a4d-144">**Side Topic: Why &lt;% %&gt; instead of &lt;%= %&gt;?**</span></span> |
| --- |
| <span data-ttu-id="a3a4d-145">你可能已注意到上面的代码之一是，在调用 RenderPartial （）时，我们使用的是 &lt;%%&gt; 块，而不是 &lt;% =%&gt; 块。</span><span class="sxs-lookup"><span data-stu-id="a3a4d-145">One of the subtle things you might have noticed with the code above is that we are using a &lt;% %&gt; block instead of a &lt;%= %&gt; block when calling Html.RenderPartial().</span></span> <span data-ttu-id="a3a4d-146">ASP.NET 中 &lt;% =%&gt; 块指示开发人员要呈现指定的值（例如： &lt;% = "Hello"%&gt; 会呈现 "Hello"）。</span><span class="sxs-lookup"><span data-stu-id="a3a4d-146">&lt;%= %&gt; blocks in ASP.NET indicate that a developer wants to render a specified value (for example: &lt;%= "Hello" %&gt; would render "Hello").</span></span> <span data-ttu-id="a3a4d-147">&lt;%%&gt; 块，而是指示开发人员想要执行代码，并且必须显式执行其中呈现的任何输出（例如： &lt;% Response （"Hello"）%&gt;。</span><span class="sxs-lookup"><span data-stu-id="a3a4d-147">&lt;% %&gt; blocks instead indicate that the developer wants to execute code, and that any rendered output within them must be done explicitly (for example: &lt;% Response.Write("Hello") %&gt;.</span></span> <span data-ttu-id="a3a4d-148">由于 RenderPartial （）方法不返回字符串，而是将内容直接输出到调用视图模板的输出流，因此我们使用了 &lt;%%&gt; 块的原因。</span><span class="sxs-lookup"><span data-stu-id="a3a4d-148">The reason we are using a &lt;% %&gt; block with our Html.RenderPartial code above is because the Html.RenderPartial() method doesn't return a string, and instead outputs the content directly to the calling view template's output stream.</span></span> <span data-ttu-id="a3a4d-149">它出于性能效率原因而执行此操作，这样做可以避免创建（可能非常大）的临时字符串对象。</span><span class="sxs-lookup"><span data-stu-id="a3a4d-149">It does this for performance efficiency reasons, and by doing so it avoids the need to create a (potentially very large) temporary string object.</span></span> <span data-ttu-id="a3a4d-150">这会减少内存使用量并提高总体应用程序吞吐量。</span><span class="sxs-lookup"><span data-stu-id="a3a4d-150">This reduces memory usage and improves overall application throughput.</span></span> <span data-ttu-id="a3a4d-151">使用 RenderPartial （）时，一个常见的错误是在调用结束时，忘记在调用末尾添加一个分号，因为它位于 &lt;%%&gt; 块内。</span><span class="sxs-lookup"><span data-stu-id="a3a4d-151">One common mistake when using Html.RenderPartial() is to forget to add a semi-colon at the end of the call when it is within a &lt;% %&gt; block.</span></span> <span data-ttu-id="a3a4d-152">例如，以下代码将导致编译器错误： &lt;% RenderPartial （"DinnerForm"）%&gt; 而不需要编写： &lt;% RenderPartial （"DinnerForm"）;%&gt; 这是因为 &lt;%%&gt; 块是自包含的代码语句，而使用C#的代码语句需要以分号结束。</span><span class="sxs-lookup"><span data-stu-id="a3a4d-152">For example, this code will cause a compiler error: &lt;% Html.RenderPartial("DinnerForm") %&gt; You instead need to write: &lt;% Html.RenderPartial("DinnerForm"); %&gt; This is because &lt;% %&gt; blocks are self-contained code statements, and when using C# code statements need to be terminated with a semi-colon.</span></span> |

### <a name="using-partial-view-templates-to-clarify-code"></a><span data-ttu-id="a3a4d-153">使用分部视图模板来阐明代码</span><span class="sxs-lookup"><span data-stu-id="a3a4d-153">Using Partial View Templates to Clarify Code</span></span>

<span data-ttu-id="a3a4d-154">我们创建了 "DinnerForm" 分部视图模板，以避免在多个位置复制视图呈现逻辑。</span><span class="sxs-lookup"><span data-stu-id="a3a4d-154">We created the "DinnerForm" partial view template to avoid duplicating view rendering logic in multiple places.</span></span> <span data-ttu-id="a3a4d-155">这是创建分部视图模板最常见的原因。</span><span class="sxs-lookup"><span data-stu-id="a3a4d-155">This is the most common reason to create partial view templates.</span></span>

<span data-ttu-id="a3a4d-156">有时，即使只是在单个位置调用分部视图，也仍有必要创建分部视图。</span><span class="sxs-lookup"><span data-stu-id="a3a4d-156">Sometimes it still makes sense to create partial views even when they are only being called in a single place.</span></span> <span data-ttu-id="a3a4d-157">在将视图呈现逻辑提取并分区到一个或多个命名的分部模板中时，非常复杂的视图模板通常会更易于阅读。</span><span class="sxs-lookup"><span data-stu-id="a3a4d-157">Very complicated view templates can often become much easier to read when their view rendering logic is extracted and partitioned into one or more well named partial templates.</span></span>

<span data-ttu-id="a3a4d-158">例如，从我们的项目中的站点 master 文件考虑以下代码片段（我们将在稍后介绍）。</span><span class="sxs-lookup"><span data-stu-id="a3a4d-158">For example, consider the below code-snippet from the Site.master file in our project (which we will be looking at shortly).</span></span> <span data-ttu-id="a3a4d-159">代码相对简单明了，因为显示屏幕右上角的 "登录/注销" 链接的逻辑封装在 "Logonusercontrol.ascx" 部分中：</span><span class="sxs-lookup"><span data-stu-id="a3a4d-159">The code is relatively straight-forward to read – partly because the logic to display a login/logout link at the top right of the screen is encapsulated within the "LogOnUserControl" partial:</span></span>

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample4.aspx)]

<span data-ttu-id="a3a4d-160">当你发现在视图模板内尝试理解 html/代码标记时感到困惑时，请考虑在将其中一些部分提取并重构为命名完好的分部视图时，它是否更清晰。</span><span class="sxs-lookup"><span data-stu-id="a3a4d-160">Whenever you find yourself getting confused trying to understand the html/code markup within a view-template, consider whether it wouldn't be clearer if some of it was extracted and refactored into well-named partial views.</span></span>

### <a name="master-pages"></a><span data-ttu-id="a3a4d-161">母版页</span><span class="sxs-lookup"><span data-stu-id="a3a4d-161">Master Pages</span></span>

<span data-ttu-id="a3a4d-162">除了支持分部视图以外，ASP.NET MVC 还支持创建 "母版页" 模板的功能，这些模板可用于定义站点的通用布局和顶级 html。</span><span class="sxs-lookup"><span data-stu-id="a3a4d-162">In addition to supporting partial views, ASP.NET MVC also supports the ability to create "master page" templates that can be used to define the common layout and top-level html of a site.</span></span> <span data-ttu-id="a3a4d-163">然后，可以将内容占位符控件添加到母版页，以标识可由视图覆盖或 "填充" 的可替换区域。</span><span class="sxs-lookup"><span data-stu-id="a3a4d-163">Content placeholder controls can then be added to the master page to identify replaceable regions that can be overridden or "filled in" by views.</span></span> <span data-ttu-id="a3a4d-164">这提供了一种非常有效的方法，可在应用程序中应用通用布局。</span><span class="sxs-lookup"><span data-stu-id="a3a4d-164">This provides a very effective (and DRY) way to apply a common layout across an application.</span></span>

<span data-ttu-id="a3a4d-165">默认情况下，新的 ASP.NET MVC 项目会自动添加一个母版页模板。</span><span class="sxs-lookup"><span data-stu-id="a3a4d-165">By default, new ASP.NET MVC projects have a master page template automatically added to them.</span></span> <span data-ttu-id="a3a4d-166">此母版页的名称为 "\Views\Shared\"，位于 "" 文件夹中：</span><span class="sxs-lookup"><span data-stu-id="a3a4d-166">This master page is named "Site.master" and lives within the \Views\Shared\ folder:</span></span>

![](re-use-ui-using-master-pages-and-partials/_static/image5.png)

<span data-ttu-id="a3a4d-167">默认网站 .master 文件如下所示。</span><span class="sxs-lookup"><span data-stu-id="a3a4d-167">The default Site.master file looks like below.</span></span> <span data-ttu-id="a3a4d-168">它定义了站点的外部 html，以及顶部导航菜单。</span><span class="sxs-lookup"><span data-stu-id="a3a4d-168">It defines the outer html of the site, along with a menu for navigation at the top.</span></span> <span data-ttu-id="a3a4d-169">它包含两个可替换内容占位符控件–一个用于标题，另一个用于替换页面的主要内容：</span><span class="sxs-lookup"><span data-stu-id="a3a4d-169">It contains two replaceable content placeholder controls – one for the title, and the other for where the primary content of a page should be replaced:</span></span>

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample5.aspx)]

<span data-ttu-id="a3a4d-170">我们为 NerdDinner 应用程序创建的所有视图模板（"列表"、"详细信息"、"编辑"、"创建"、"NotFound" 等）都基于此站点。主模板。</span><span class="sxs-lookup"><span data-stu-id="a3a4d-170">All of the view templates we've created for our NerdDinner application ("List", "Details", "Edit", "Create", "NotFound", etc) have been based on this Site.master template.</span></span> <span data-ttu-id="a3a4d-171">这是通过在使用 "添加视图" 对话框创建视图时默认添加到 &lt;% @ Page%&gt; 指令的 "MasterPageFile" 属性指示的：</span><span class="sxs-lookup"><span data-stu-id="a3a4d-171">This is indicated via the "MasterPageFile" attribute that was added by default to the top &lt;% @ Page %&gt; directive when we created our views using the "Add View" dialog:</span></span>

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample6.aspx)]

<span data-ttu-id="a3a4d-172">这意味着我们可以更改站点的主内容，并在呈现任何视图模板时自动应用和使用这些更改。</span><span class="sxs-lookup"><span data-stu-id="a3a4d-172">What this means is that we can change the Site.master content, and have the changes automatically be applied and used when we render any of our view templates.</span></span>

<span data-ttu-id="a3a4d-173">接下来，我们将更新我们的站点。 master 的标头部分，使我们的应用程序的标头为 "NerdDinner" 而不是 "我的 MVC 应用程序"。</span><span class="sxs-lookup"><span data-stu-id="a3a4d-173">Let's update our Site.master's header section so that the header of our application is "NerdDinner" instead of "My MVC Application".</span></span> <span data-ttu-id="a3a4d-174">接下来，我们将更新导航菜单，以便第一个选项卡为 "查找晚餐" （由 HomeController 的 Index （）操作方法处理），并让我们添加一个名为 "承载晚餐" 的新选项卡（由 DinnersController 的 Create （）操作方法处理）：</span><span class="sxs-lookup"><span data-stu-id="a3a4d-174">Let's also update our navigation menu so that the first tab is "Find a Dinner" (handled by the HomeController's Index() action method), and let's add a new tab called "Host a Dinner" (handled by the DinnersController's Create() action method):</span></span>

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample7.aspx)]

<span data-ttu-id="a3a4d-175">当我们保存站点 .master 文件并刷新浏览器时，我们将看到标题更改显示在应用程序内的所有视图中。</span><span class="sxs-lookup"><span data-stu-id="a3a4d-175">When we save the Site.master file and refresh our browser we'll see our header changes show up across all views within our application.</span></span> <span data-ttu-id="a3a4d-176">例如:</span><span class="sxs-lookup"><span data-stu-id="a3a4d-176">For example:</span></span>

![](re-use-ui-using-master-pages-and-partials/_static/image6.png)

<span data-ttu-id="a3a4d-177">并带有 */Dinners/Edit/[id]* URL：</span><span class="sxs-lookup"><span data-stu-id="a3a4d-177">And with the */Dinners/Edit/[id]* URL:</span></span>

![](re-use-ui-using-master-pages-and-partials/_static/image7.png)

### <a name="next-step"></a><span data-ttu-id="a3a4d-178">下一步</span><span class="sxs-lookup"><span data-stu-id="a3a4d-178">Next Step</span></span>

<span data-ttu-id="a3a4d-179">分区和母版页提供了非常灵活的选项，使您可以对视图进行清晰的组织。</span><span class="sxs-lookup"><span data-stu-id="a3a4d-179">Partials and master pages provide very flexible options that enable you to cleanly organize views.</span></span> <span data-ttu-id="a3a4d-180">你会发现它们有助于避免重复查看内容/代码，并使你的视图模板更易于阅读和维护。</span><span class="sxs-lookup"><span data-stu-id="a3a4d-180">You'll find that they help you avoid duplicating view content/ code, and make your view templates easier to read and maintain.</span></span>

<span data-ttu-id="a3a4d-181">现在，让我们重新访问我们前面构建的列表方案，并启用可伸缩分页支持。</span><span class="sxs-lookup"><span data-stu-id="a3a4d-181">Let's now revisit the listing scenario we built earlier and enable scalable paging support.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="a3a4d-182">[上一页](use-viewdata-and-implement-viewmodel-classes.md)
> [下一页](implement-efficient-data-paging.md)</span><span class="sxs-lookup"><span data-stu-id="a3a4d-182">[Previous](use-viewdata-and-implement-viewmodel-classes.md)
[Next](implement-efficient-data-paging.md)</span></span>
