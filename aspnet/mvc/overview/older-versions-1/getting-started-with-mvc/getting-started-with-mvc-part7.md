---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part7
title: 向模型添加验证 |Microsoft Docs
author: shanselman
description: 本教程介绍了 ASP.NET MVC 的基本知识。 创建一个从数据库中读取和写入数据的简单 web 应用程序。
ms.author: riande
ms.date: 08/14/2010
ms.assetid: aa7b3e8e-e23d-49f1-b160-f99a7f2982bd
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part7
msc.type: authoredcontent
ms.openlocfilehash: 9403be574324c34edf93bef1e0e4fd7ba68a3a9d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78437276"
---
# <a name="adding-validation-to-the-model"></a><span data-ttu-id="4b0be-104">向模型添加验证</span><span class="sxs-lookup"><span data-stu-id="4b0be-104">Adding Validation to the Model</span></span>

<span data-ttu-id="4b0be-105">作者： [Scott Hanselman](https://github.com/shanselman)</span><span class="sxs-lookup"><span data-stu-id="4b0be-105">by [Scott Hanselman](https://github.com/shanselman)</span></span>

> <span data-ttu-id="4b0be-106">本教程介绍了 ASP.NET MVC 的基本知识。</span><span class="sxs-lookup"><span data-stu-id="4b0be-106">This is a beginner tutorial that introduces the basics of ASP.NET MVC.</span></span> <span data-ttu-id="4b0be-107">你将创建一个简单的 web 应用程序，用于读取和写入数据库。</span><span class="sxs-lookup"><span data-stu-id="4b0be-107">You'll create a simple web application that reads and writes from a database.</span></span> <span data-ttu-id="4b0be-108">请访问[ASP.NET mvc 学习中心](../../../index.md)，查找其他 ASP.NET mvc 教程和示例。</span><span class="sxs-lookup"><span data-stu-id="4b0be-108">Visit the [ASP.NET MVC learning center](../../../index.md) to find other ASP.NET MVC tutorials and samples.</span></span>

<span data-ttu-id="4b0be-109">在本部分中，我们将实现在应用程序中启用输入验证所需的支持。</span><span class="sxs-lookup"><span data-stu-id="4b0be-109">In this section we are going to implement the support necessary to enable input validation within our application.</span></span> <span data-ttu-id="4b0be-110">我们将确保数据库内容始终正确，并在最终用户尝试输入电影数据无效时向最终用户提供有用的错误消息。</span><span class="sxs-lookup"><span data-stu-id="4b0be-110">We'll ensure that our database content is always correct, and provide helpful error messages to end users when they try and enter Movie data which is not valid.</span></span> <span data-ttu-id="4b0be-111">首先向 Movie 类添加少量验证逻辑。</span><span class="sxs-lookup"><span data-stu-id="4b0be-111">We'll begin by adding a little validation logic to the Movie class.</span></span>

<span data-ttu-id="4b0be-112">右键单击模型文件夹，然后选择 "添加类"。</span><span class="sxs-lookup"><span data-stu-id="4b0be-112">Right click on the Model folder and select Add Class.</span></span> <span data-ttu-id="4b0be-113">将类命名为 "Movie"。</span><span class="sxs-lookup"><span data-stu-id="4b0be-113">Name your class Movie.</span></span>

<span data-ttu-id="4b0be-114">当我们前面创建了 "电影" 实体模型时，IDE 创建了一个 Movie 类。</span><span class="sxs-lookup"><span data-stu-id="4b0be-114">When we created the Movie Entity Model earlier, the IDE created a Movie class.</span></span> <span data-ttu-id="4b0be-115">事实上，Movie 类的一部分可以在一个文件中，也可以位于另一个文件中。</span><span class="sxs-lookup"><span data-stu-id="4b0be-115">In fact, part of the Movie class can be in one file and part in another.</span></span> <span data-ttu-id="4b0be-116">这称为分部类。</span><span class="sxs-lookup"><span data-stu-id="4b0be-116">This is called a Partial Class.</span></span> <span data-ttu-id="4b0be-117">我们要从另一个文件扩展 Movie 类。</span><span class="sxs-lookup"><span data-stu-id="4b0be-117">We're going to extend the Movie class from another file.</span></span>

<span data-ttu-id="4b0be-118">我们将创建一个指向 "合作者类" 的部分电影类，其中的某些属性将向系统提供验证提示。</span><span class="sxs-lookup"><span data-stu-id="4b0be-118">We'll create a partial movie class that points to a "buddy class" with some attributes that will give validation hints to the system.</span></span> <span data-ttu-id="4b0be-119">我们将根据需要标记标题和价格，还会坚持价格在某个范围内。</span><span class="sxs-lookup"><span data-stu-id="4b0be-119">We'll mark the Title and Price as Required, and also insist that the Price be within a certain range.</span></span> <span data-ttu-id="4b0be-120">右键单击 "模型" 文件夹，然后选择 "添加类"。</span><span class="sxs-lookup"><span data-stu-id="4b0be-120">Right click the Models folder and select Add Class.</span></span> <span data-ttu-id="4b0be-121">命名类电影，并单击 "确定" 按钮。</span><span class="sxs-lookup"><span data-stu-id="4b0be-121">Name your class Movie and Click the OK button.</span></span> <span data-ttu-id="4b0be-122">下面是我们的部分电影类的外观。</span><span class="sxs-lookup"><span data-stu-id="4b0be-122">Here's what our partial Movie class looks like.</span></span>

[!code-csharp[Main](getting-started-with-mvc-part7/samples/sample1.cs)]

<span data-ttu-id="4b0be-123">重新运行应用程序，并尝试输入价格超过100的电影。</span><span class="sxs-lookup"><span data-stu-id="4b0be-123">Re-Run your application and try to enter a movie with a price over 100.</span></span> <span data-ttu-id="4b0be-124">提交表单后，会收到错误。</span><span class="sxs-lookup"><span data-stu-id="4b0be-124">You'll get an error after you've submitted the form.</span></span> <span data-ttu-id="4b0be-125">此错误在服务器端捕获，并在发布窗体后发生。</span><span class="sxs-lookup"><span data-stu-id="4b0be-125">The error is caught on the server side and occurs after the Form is POSTed.</span></span> <span data-ttu-id="4b0be-126">请注意，ASP.NET MVC 的内置 HTML 帮助程序的智能方式足以显示错误消息，并在 textbox 元素中为我们维护值：</span><span class="sxs-lookup"><span data-stu-id="4b0be-126">Notice how ASP.NET MVC's built-in HTML helpers were smart enough to display the error message and maintain the values for us within the textbox elements:</span></span>

<span data-ttu-id="4b0be-127">[![CreateMovieWithValidation](getting-started-with-mvc-part7/_static/image2.png)](getting-started-with-mvc-part7/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="4b0be-127">[![CreateMovieWithValidation](getting-started-with-mvc-part7/_static/image2.png)](getting-started-with-mvc-part7/_static/image1.png)</span></span>

<span data-ttu-id="4b0be-128">这很好，但如果我们可以立即在客户端上通知用户，则这会很好。</span><span class="sxs-lookup"><span data-stu-id="4b0be-128">This works great, but it'd be nice if we could tell the user on the client-side, immediately, before the server gets involved.</span></span>

<span data-ttu-id="4b0be-129">让我们使用 JavaScript 启用一些客户端验证。</span><span class="sxs-lookup"><span data-stu-id="4b0be-129">Let's enable some client-side validation with JavaScript.</span></span>

## <a name="adding-client-side-validation"></a><span data-ttu-id="4b0be-130">添加客户端验证</span><span class="sxs-lookup"><span data-stu-id="4b0be-130">Adding Client-Side Validation</span></span>

<span data-ttu-id="4b0be-131">由于我们的 Movie 类已经有一些验证属性，因此我们只需将一些 JavaScript 文件添加到我们的 Create .aspx 视图模板，然后添加一行代码来实现客户端验证。</span><span class="sxs-lookup"><span data-stu-id="4b0be-131">Since our Movie class already has some validation attributes, we'll just need to add a few JavaScript files to our Create.aspx View template and add a line of code to enable client-side validation to take place.</span></span>

<span data-ttu-id="4b0be-132">从 VWD 中，请访问我们的 "视图"/"电影" 文件夹，然后打开 "创建 .aspx"。</span><span class="sxs-lookup"><span data-stu-id="4b0be-132">From within VWD go our Views/Movie folder and open up Create.aspx.</span></span>

<span data-ttu-id="4b0be-133">在解决方案资源管理器中打开 "脚本" 文件夹，并将以下三个脚本拖到 &lt;head&gt; 标记中。</span><span class="sxs-lookup"><span data-stu-id="4b0be-133">Open up the Scripts folder in the Solution Explorer and drag the following three scripts to within the &lt;head&gt; tag.</span></span>

- <span data-ttu-id="4b0be-134">MicrosoftAjax.js</span><span class="sxs-lookup"><span data-stu-id="4b0be-134">MicrosoftAjax.js</span></span>
- <span data-ttu-id="4b0be-135">MicrosoftMvcValidation.js</span><span class="sxs-lookup"><span data-stu-id="4b0be-135">MicrosoftMvcValidation.js</span></span>

<span data-ttu-id="4b0be-136">希望这些脚本文件按此顺序显示。</span><span class="sxs-lookup"><span data-stu-id="4b0be-136">You want these script files to appear in this order.</span></span>

[!code-html[Main](getting-started-with-mvc-part7/samples/sample2.html)]

<span data-ttu-id="4b0be-137">此外，将此单行添加到 Html.beginform：</span><span class="sxs-lookup"><span data-stu-id="4b0be-137">Also, add this single line above the Html.BeginForm:</span></span>

[!code-aspx[Main](getting-started-with-mvc-part7/samples/sample3.aspx)]

<span data-ttu-id="4b0be-138">下面是 IDE 中显示的代码。</span><span class="sxs-lookup"><span data-stu-id="4b0be-138">Here's the code shown within the IDE.</span></span>

<span data-ttu-id="4b0be-139">[![电影-Microsoft Visual Web Developer 2010 Express （10）](getting-started-with-mvc-part7/_static/image4.png)](getting-started-with-mvc-part7/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="4b0be-139">[![Movies - Microsoft Visual Web Developer 2010 Express (10)](getting-started-with-mvc-part7/_static/image4.png)](getting-started-with-mvc-part7/_static/image3.png)</span></span>

<span data-ttu-id="4b0be-140">运行应用程序并再次访问/Movies/Create，并单击 "创建" 而不输入任何数据。</span><span class="sxs-lookup"><span data-stu-id="4b0be-140">Run your application and visit /Movies/Create again, and click Create without entering any data.</span></span> <span data-ttu-id="4b0be-141">错误消息会立即显示，而不是将数据完全发送到服务器时所关联的页面 flash。</span><span class="sxs-lookup"><span data-stu-id="4b0be-141">The error messages appear immediately without the page flash that we associate with sending data all the way back to the server.</span></span> <span data-ttu-id="4b0be-142">这是因为 ASP.NET MVC 现在正在验证客户端（使用 JavaScript）和服务器上的输入。</span><span class="sxs-lookup"><span data-stu-id="4b0be-142">This is because ASP.NET MVC is now validating the input on both the client (using JavaScript) and on the server.</span></span>

<span data-ttu-id="4b0be-143">[![创建-Windows Internet Explorer](getting-started-with-mvc-part7/_static/image6.png)](getting-started-with-mvc-part7/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="4b0be-143">[![Create - Windows Internet Explorer](getting-started-with-mvc-part7/_static/image6.png)](getting-started-with-mvc-part7/_static/image5.png)</span></span>

<span data-ttu-id="4b0be-144">这看起来不错！</span><span class="sxs-lookup"><span data-stu-id="4b0be-144">This is looking good!</span></span> <span data-ttu-id="4b0be-145">现在，我们将另一个列添加到数据库中。</span><span class="sxs-lookup"><span data-stu-id="4b0be-145">Let's now add one additional column to the database.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="4b0be-146">[上一页](getting-started-with-mvc-part6.md)
> [下一页](getting-started-with-mvc-part8.md)</span><span class="sxs-lookup"><span data-stu-id="4b0be-146">[Previous](getting-started-with-mvc-part6.md)
[Next](getting-started-with-mvc-part8.md)</span></span>
