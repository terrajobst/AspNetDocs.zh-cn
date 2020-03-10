---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part3
title: 添加视图 |Microsoft Docs
author: shanselman
description: 本教程介绍了 ASP.NET MVC 的基本知识。 创建一个从数据库中读取和写入数据的简单 web 应用程序。
ms.author: riande
ms.date: 08/14/2010
ms.assetid: e8f1515c-c277-47ff-a23e-224118f13f02
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part3
msc.type: authoredcontent
ms.openlocfilehash: 462b1210c45da67058899193afcea973f3daf122
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78469772"
---
# <a name="adding-a-view"></a><span data-ttu-id="c771d-104">添加视图</span><span class="sxs-lookup"><span data-stu-id="c771d-104">Adding a View</span></span>

<span data-ttu-id="c771d-105">作者： [Scott Hanselman](https://github.com/shanselman)</span><span class="sxs-lookup"><span data-stu-id="c771d-105">by [Scott Hanselman](https://github.com/shanselman)</span></span>

> <span data-ttu-id="c771d-106">本教程介绍了 ASP.NET MVC 的基本知识。</span><span class="sxs-lookup"><span data-stu-id="c771d-106">This is a beginner tutorial that introduces the basics of ASP.NET MVC.</span></span> <span data-ttu-id="c771d-107">你将创建一个简单的 web 应用程序，用于读取和写入数据库。</span><span class="sxs-lookup"><span data-stu-id="c771d-107">You'll create a simple web application that reads and writes from a database.</span></span> <span data-ttu-id="c771d-108">请访问[ASP.NET mvc 学习中心](../../../index.md)，查找其他 ASP.NET mvc 教程和示例。</span><span class="sxs-lookup"><span data-stu-id="c771d-108">Visit the [ASP.NET MVC learning center](../../../index.md) to find other ASP.NET MVC tutorials and samples.</span></span>

<span data-ttu-id="c771d-109">在本部分中，我们将了解如何让 HelloWorldController 类使用视图模板文件来将生成 HTML 响应完全封装回客户端。</span><span class="sxs-lookup"><span data-stu-id="c771d-109">In this section we are going to look at how we can have our HelloWorldController class use a View template file to cleanly encapsulate generating HTML responses back to a client.</span></span>

<span data-ttu-id="c771d-110">首先，让我们将视图模板与索引方法结合使用。</span><span class="sxs-lookup"><span data-stu-id="c771d-110">Let's start by using a View template with our Index method.</span></span> <span data-ttu-id="c771d-111">我们的方法称为 Index，它位于 HelloWorldController 中。</span><span class="sxs-lookup"><span data-stu-id="c771d-111">Our method is called Index and it's in the HelloWorldController.</span></span> <span data-ttu-id="c771d-112">目前，Index （）方法返回一个字符串，其中包含在控制器类中硬编码的消息。</span><span class="sxs-lookup"><span data-stu-id="c771d-112">Currently our Index() method returns a string with a message that is hardcoded within the Controller class.</span></span>

[!code-csharp[Main](getting-started-with-mvc-part3/samples/sample1.cs)]

<span data-ttu-id="c771d-113">现在，让我们将 Index 方法更改为，如下所示：</span><span class="sxs-lookup"><span data-stu-id="c771d-113">Let's now change the Index method to instead look like this:</span></span>

[!code-csharp[Main](getting-started-with-mvc-part3/samples/sample2.cs)]

<span data-ttu-id="c771d-114">现在，我们将一个视图模板添加到我们的项目，我们可以将其用于索引（）方法。</span><span class="sxs-lookup"><span data-stu-id="c771d-114">Let's now add a View template to our project that we can use for our Index() method.</span></span> <span data-ttu-id="c771d-115">为此，请在 Index 方法中间的某个位置右键单击鼠标，然后单击 "添加视图 ..."</span><span class="sxs-lookup"><span data-stu-id="c771d-115">To do this, right-click with your mouse somewhere in the middle of the Index method and click Add View...</span></span>

![图像](getting-started-with-mvc-part3/_static/image1.png)

<span data-ttu-id="c771d-117">这将显示 "添加视图" 对话框，该对话框提供了一些选项，用于说明我们如何创建可供索引方法使用的视图模板。</span><span class="sxs-lookup"><span data-stu-id="c771d-117">This will bring up the "Add View" dialog which provides us some options for how we want to create a view template that can be used by our Index method.</span></span> <span data-ttu-id="c771d-118">现在，请不要更改任何内容，只需单击 "添加" 按钮即可。</span><span class="sxs-lookup"><span data-stu-id="c771d-118">For now, don't change anything, and just click the Add button.</span></span>

<span data-ttu-id="c771d-119">[!["添加视图" 对话框](getting-started-with-mvc-part3/_static/image3.png)](getting-started-with-mvc-part3/_static/image2.png)</span><span class="sxs-lookup"><span data-stu-id="c771d-119">[![Add View Dialog](getting-started-with-mvc-part3/_static/image3.png)](getting-started-with-mvc-part3/_static/image2.png)</span></span>

<span data-ttu-id="c771d-120">单击 "添加" 后，解决方案文件夹中将显示一个新文件夹和一个新文件，如下所示。</span><span class="sxs-lookup"><span data-stu-id="c771d-120">After you click Add, a new folder and a new file will appear in the Solution Folder, as seen here.</span></span> <span data-ttu-id="c771d-121">我现在在 Views 下有一个 HelloWorld 文件夹，该文件夹内有一个索引 .aspx 文件。</span><span class="sxs-lookup"><span data-stu-id="c771d-121">I now have a HelloWorld folder under Views, and an Index.aspx file inside that folder.</span></span>

<span data-ttu-id="c771d-122">[![solutionexplorerwithindex](getting-started-with-mvc-part3/_static/image5.png)](getting-started-with-mvc-part3/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="c771d-122">[![solutionexplorerwithindex](getting-started-with-mvc-part3/_static/image5.png)](getting-started-with-mvc-part3/_static/image4.png)</span></span>

<span data-ttu-id="c771d-123">新的索引文件也已经打开并可以进行编辑。</span><span class="sxs-lookup"><span data-stu-id="c771d-123">The new Index file is also already opened and ready for editing.</span></span> <span data-ttu-id="c771d-124">在第一个 &lt;h2 下添加一些文本&gt;Index&lt;/h2&gt; 如 "Hello World"。</span><span class="sxs-lookup"><span data-stu-id="c771d-124">Add some text under the first &lt;h2&gt;Index&lt;/h2&gt; like "Hello World."</span></span>

[!code-html[Main](getting-started-with-mvc-part3/samples/sample3.html)]

<span data-ttu-id="c771d-125">运行应用程序，并在浏览器中再次访问[`http://localhost:xx/HelloWorld`](http://localhostxx) 。</span><span class="sxs-lookup"><span data-stu-id="c771d-125">Run your application and visit [`http://localhost:xx/HelloWorld`](http://localhostxx) again in your browser.</span></span> <span data-ttu-id="c771d-126">在此示例中，控制器中的 Index 方法未执行任何操作，但调用了 "return View （）"，这表明我们希望使用视图模板文件来将响应呈现给客户端。</span><span class="sxs-lookup"><span data-stu-id="c771d-126">The Index method in our controller in this example didn't do any work, but did call "return View()" which indicated that we wanted to use a view template file to render a response back to the client.</span></span> <span data-ttu-id="c771d-127">由于我们未显式指定要使用的视图模板文件的名称，因此 ASP.NET MVC 默认使用 \Views\HelloWorld 文件夹中的 "" 视图文件。</span><span class="sxs-lookup"><span data-stu-id="c771d-127">Because we did not explicitly specify the name of the view template file to use, ASP.NET MVC defaulted to using the Index.aspx view file within the \Views\HelloWorld folder.</span></span> <span data-ttu-id="c771d-128">现在我们看到我们在视图中进行了硬编码的字符串。</span><span class="sxs-lookup"><span data-stu-id="c771d-128">Now we see the string we hard-coded in our View.</span></span>

<span data-ttu-id="c771d-129">[![索引-Windows Internet Explorer](getting-started-with-mvc-part3/_static/image7.png)](getting-started-with-mvc-part3/_static/image6.png)</span><span class="sxs-lookup"><span data-stu-id="c771d-129">[![Index - Windows Internet Explorer](getting-started-with-mvc-part3/_static/image7.png)](getting-started-with-mvc-part3/_static/image6.png)</span></span>

<span data-ttu-id="c771d-130">看起来不错。</span><span class="sxs-lookup"><span data-stu-id="c771d-130">Looks pretty good.</span></span> <span data-ttu-id="c771d-131">但请注意，浏览器的标题显示 "索引"，而页面上的大标题显示 "我的 MVC 应用程序"。</span><span class="sxs-lookup"><span data-stu-id="c771d-131">However, notice that the Browser's title says "Index" and the big title on the page says "My MVC Application."</span></span> <span data-ttu-id="c771d-132">让我们更改这些。</span><span class="sxs-lookup"><span data-stu-id="c771d-132">Let's change those.</span></span>

### <a name="changing-views-and-master-pages"></a><span data-ttu-id="c771d-133">更改视图和母版页</span><span class="sxs-lookup"><span data-stu-id="c771d-133">Changing Views and Master Pages</span></span>

<span data-ttu-id="c771d-134">首先，让我们更改文本 "我的 MVC 应用程序"。</span><span class="sxs-lookup"><span data-stu-id="c771d-134">First, let's change the text "My MVC Application."</span></span> <span data-ttu-id="c771d-135">该文本是共享的，并显示在每一页上。</span><span class="sxs-lookup"><span data-stu-id="c771d-135">That text is shared and appears on every page.</span></span> <span data-ttu-id="c771d-136">它实际上只显示在代码中的一个位置，即使它在应用程序的每一页上也是如此。</span><span class="sxs-lookup"><span data-stu-id="c771d-136">It actually appears in only one place in our code, even though it's on every page in our app.</span></span> <span data-ttu-id="c771d-137">中转到解决方案资源管理器中的/Views/Shared 文件夹，然后打开 "Master" 文件。</span><span class="sxs-lookup"><span data-stu-id="c771d-137">Go to the /Views/Shared folder in the Solution Explorer and open the Site.Master file.</span></span> <span data-ttu-id="c771d-138">此文件称为母版页，它是其他所有页面都使用的共享 "shell"。</span><span class="sxs-lookup"><span data-stu-id="c771d-138">This file is called a Master Page and it's the shared "shell" that all our other pages use.</span></span>

<span data-ttu-id="c771d-139">请注意一些文本，其中显示了此文件中的 ContentPlaceholder "MainContent"。</span><span class="sxs-lookup"><span data-stu-id="c771d-139">Notice some text that says ContentPlaceholder "MainContent" in this file.</span></span>

[!code-aspx[Main](getting-started-with-mvc-part3/samples/sample4.aspx)]

<span data-ttu-id="c771d-140">占位符是您创建的所有页面都显示在母版页中的位置。</span><span class="sxs-lookup"><span data-stu-id="c771d-140">That placeholder is where all the pages you create will show up, "wrapped" in the master page.</span></span> <span data-ttu-id="c771d-141">尝试更改标题，并运行应用程序并访问多个页面。</span><span class="sxs-lookup"><span data-stu-id="c771d-141">Try changing the title, then run your app and visit multiple pages.</span></span> <span data-ttu-id="c771d-142">你会注意到，你的一个更改出现在多个页面上。</span><span class="sxs-lookup"><span data-stu-id="c771d-142">You'll notice that your one change appears on multiple pages.</span></span>

[!code-html[Main](getting-started-with-mvc-part3/samples/sample5.html)]

<span data-ttu-id="c771d-143">现在，每个页面都有主要标题，即 "我的 MVC 电影应用程序" 的 "H1"。</span><span class="sxs-lookup"><span data-stu-id="c771d-143">Now every page will have the Primary Heading - that's H1 - of "My MVC Movie Application."</span></span> <span data-ttu-id="c771d-144">处理所有页面之间共享的白色文本。</span><span class="sxs-lookup"><span data-stu-id="c771d-144">That handles the white text at the top there that's shared across all the pages.</span></span>

<span data-ttu-id="c771d-145">下面是一个完整的站点，其中包含已更改的标题：</span><span class="sxs-lookup"><span data-stu-id="c771d-145">Here is the Site.Master in its entirety with our changed title:</span></span>

[!code-aspx[Main](getting-started-with-mvc-part3/samples/sample6.aspx)]

<span data-ttu-id="c771d-146">现在，让我们更改索引页的标题。</span><span class="sxs-lookup"><span data-stu-id="c771d-146">Now, let's change the title of the Index page.</span></span>

<span data-ttu-id="c771d-147">打开/HelloWorld/Index.aspx。</span><span class="sxs-lookup"><span data-stu-id="c771d-147">Open /HelloWorld/Index.aspx.</span></span> <span data-ttu-id="c771d-148">这里有两个要更改的位置。</span><span class="sxs-lookup"><span data-stu-id="c771d-148">There's two places to change.</span></span> <span data-ttu-id="c771d-149">首先，在浏览器标题中显示的标题，然后是辅助标头。</span><span class="sxs-lookup"><span data-stu-id="c771d-149">First, the Title that appears in the title of the browser, then the secondary header - that's H2 - as well.</span></span> <span data-ttu-id="c771d-150">我要使它们略有不同，以便您可以看到哪个代码更改了应用程序的哪一部分。</span><span class="sxs-lookup"><span data-stu-id="c771d-150">I'll make them each slightly different so you can see which bit of code changes which part of the app.</span></span>

[!code-aspx[Main](getting-started-with-mvc-part3/samples/sample7.aspx)]

<span data-ttu-id="c771d-151">运行应用并访问/Movies。</span><span class="sxs-lookup"><span data-stu-id="c771d-151">Run your app and visit /Movies.</span></span> <span data-ttu-id="c771d-152">请注意，浏览器标题、主标题和辅助标题已更改。</span><span class="sxs-lookup"><span data-stu-id="c771d-152">Notice that the browser title, the primary heading and the secondary headings have changed.</span></span> <span data-ttu-id="c771d-153">在您的应用程序中对视图进行较小的更改时，可以轻松地进行重大更改。</span><span class="sxs-lookup"><span data-stu-id="c771d-153">It's easy to make big changes in your app with small changes to your view.</span></span>

<span data-ttu-id="c771d-154">[![电影列表-Windows Internet Explorer](getting-started-with-mvc-part3/_static/image9.png)](getting-started-with-mvc-part3/_static/image8.png)</span><span class="sxs-lookup"><span data-stu-id="c771d-154">[![Movie List - Windows Internet Explorer](getting-started-with-mvc-part3/_static/image9.png)](getting-started-with-mvc-part3/_static/image8.png)</span></span>

<span data-ttu-id="c771d-155">我们有点 "数据" （在本例中为 "Hello World！"</span><span class="sxs-lookup"><span data-stu-id="c771d-155">Our little bit of "data" (in this case the "Hello World!"</span></span> <span data-ttu-id="c771d-156">消息）虽然是硬编码的。</span><span class="sxs-lookup"><span data-stu-id="c771d-156">message) was hard coded though.</span></span> <span data-ttu-id="c771d-157">我们有 V （Views），我们有 C （控制器），但没有 M （模型）。</span><span class="sxs-lookup"><span data-stu-id="c771d-157">We've got V (Views) and we've got C (Controllers), but no M (Model) yet.</span></span> <span data-ttu-id="c771d-158">我们很快会演练如何创建数据库并从中检索模型数据。</span><span class="sxs-lookup"><span data-stu-id="c771d-158">We'll shortly walk through how create a database and retrieve model data from it.</span></span>

## <a name="passing-a-viewmodel"></a><span data-ttu-id="c771d-159">传递 ViewModel</span><span class="sxs-lookup"><span data-stu-id="c771d-159">Passing a ViewModel</span></span>

<span data-ttu-id="c771d-160">不过，在开始使用数据库并讨论模型之前，先来谈谈 "Viewmodel"。</span><span class="sxs-lookup"><span data-stu-id="c771d-160">Before we go to a database and talk about Models, though, let's first talk about "ViewModels."</span></span> <span data-ttu-id="c771d-161">这些对象表示视图模板在向客户端呈现 HTML 响应时所需的内容。</span><span class="sxs-lookup"><span data-stu-id="c771d-161">These are objects that represent what a View template requires to render an HTML response back to a client.</span></span> <span data-ttu-id="c771d-162">它们通常由控制器类创建并传递给视图模板，只应包含视图模板所需的数据，而不能有更多的数据。</span><span class="sxs-lookup"><span data-stu-id="c771d-162">They are typically created and passed by a Controller class to a View template, and should only contain the data that the View template requires - and no more.</span></span>

<span data-ttu-id="c771d-163">以前，我们的 HelloWorld 示例使用了一个名称和一个 numTimes 参数，并将其输出到浏览器。</span><span class="sxs-lookup"><span data-stu-id="c771d-163">Previously with our HelloWorld sample, our Welcome() action method took a name and a numTimes parameter and output it to the browser.</span></span> <span data-ttu-id="c771d-164">不要让控制器继续直接呈现此响应，而是创建一个小类来保存该数据，然后将其传递到视图模板，以使用它呈现回 HTML 响应。</span><span class="sxs-lookup"><span data-stu-id="c771d-164">Rather than have the Controller continue to render this response directly,let's instead make a small class to hold that data and then pass it over to a View template to render back the HTML response using it.</span></span> <span data-ttu-id="c771d-165">这样一来，控制器就会考虑到一个问题，另一个是查看模板，使我们能够在应用程序中保持干净的 "问题分离"。</span><span class="sxs-lookup"><span data-stu-id="c771d-165">This way the Controller is concerned with one thing and the View template another – enabling us to maintain clean "separation of concerns" within our application.</span></span>

<span data-ttu-id="c771d-166">返回到 HelloWorldController.cs 文件并添加新的 "WelcomeViewModel" 类，并更改控制器中的 "欢迎" 方法。</span><span class="sxs-lookup"><span data-stu-id="c771d-166">Return to the HelloWorldController.cs file and add a new "WelcomeViewModel" class and change the Welcome method inside your controller.</span></span> <span data-ttu-id="c771d-167">下面是在同一文件中包含新类的完整 HelloWorldController.cs。</span><span class="sxs-lookup"><span data-stu-id="c771d-167">Here is the complete HelloWorldController.cs with the new class in the same file.</span></span>

[!code-csharp[Main](getting-started-with-mvc-part3/samples/sample8.cs)]

<span data-ttu-id="c771d-168">即使是在多行上，欢迎方法也只是两个代码语句。</span><span class="sxs-lookup"><span data-stu-id="c771d-168">Even though it's on multiple lines, our Welcome method is really only two code statements.</span></span> <span data-ttu-id="c771d-169">第一个语句将两个参数打包到一个 ViewModel 对象中，第二个语句将生成的对象传递到视图。</span><span class="sxs-lookup"><span data-stu-id="c771d-169">The first statement packages up our two parameters into a ViewModel object, and the second passes the resulting object onto the View.</span></span>

<span data-ttu-id="c771d-170">现在，我们需要一个欢迎视图模板！</span><span class="sxs-lookup"><span data-stu-id="c771d-170">Now we need a Welcome View template!</span></span> <span data-ttu-id="c771d-171">右键单击欢迎方法，然后选择 "添加视图"。</span><span class="sxs-lookup"><span data-stu-id="c771d-171">Right click in the Welcome method and select Add View.</span></span> <span data-ttu-id="c771d-172">这次，我们将选中 "创建强类型视图"，然后从下拉列表中选择我们的 WelcomeViewModel 类。</span><span class="sxs-lookup"><span data-stu-id="c771d-172">This time, we'll check "Create a strongly-typed view" and select our WelcomeViewModel class from the drop down list.</span></span> <span data-ttu-id="c771d-173">此新视图将仅了解 WelcomeViewModels 和其他类型的对象。</span><span class="sxs-lookup"><span data-stu-id="c771d-173">This new view will only know about WelcomeViewModels and no other types of objects.</span></span>

> <span data-ttu-id="c771d-174">*注意：将 WelcomeViewModel 添加到后，需要编译一次，以便显示在下拉列表中。*</span><span class="sxs-lookup"><span data-stu-id="c771d-174">*NOTE: You'll need to have compiled once after adding your WelcomeViewModel for to show up in the drop down list.*</span></span>

<span data-ttu-id="c771d-175">"添加视图" 对话框应如下所示。</span><span class="sxs-lookup"><span data-stu-id="c771d-175">Here's what your Add View dialog should look like.</span></span> <span data-ttu-id="c771d-176">单击“添加”按钮。</span><span class="sxs-lookup"><span data-stu-id="c771d-176">Click the Add button.</span></span> ![添加带圆圈的视图](getting-started-with-mvc-part3/_static/image10.png)

<span data-ttu-id="c771d-178">将此代码添加到新的 "欢迎"&gt; 中的 "&lt;h2" 下。</span><span class="sxs-lookup"><span data-stu-id="c771d-178">Add this code under the &lt;h2&gt; in your new Welcome.aspx.</span></span> <span data-ttu-id="c771d-179">我们将进行一次循环，并将 "Hello" 当作用户说我们应该！</span><span class="sxs-lookup"><span data-stu-id="c771d-179">We'll make a loop and say Hello as many times as the user says we should!</span></span>

[!code-aspx[Main](getting-started-with-mvc-part3/samples/sample9.aspx)]

<span data-ttu-id="c771d-180">另外，请注意，当你键入这一点时，这是因为我们告诉此关于 WelcomeViewModel 的视图（他们已结婚，请记住？），我们每次引用模型对象时都会获得有用的 Intellisense，如以下屏幕截图所示：</span><span class="sxs-lookup"><span data-stu-id="c771d-180">Also, notice while you're typing that because we told this View about the WelcomeViewModel (they are married, remember?) that we get helpful Intellisense each time we reference our Model object as seen in the screenshot below:</span></span>

<span data-ttu-id="c771d-181">[![NumTime 源代码](getting-started-with-mvc-part3/_static/image12.png)](getting-started-with-mvc-part3/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="c771d-181">[![NumTime Source Code](getting-started-with-mvc-part3/_static/image12.png)](getting-started-with-mvc-part3/_static/image11.png)</span></span>

<span data-ttu-id="c771d-182">运行应用程序并再次访问 `http://localhost:xx/HelloWorld/Welcome?name=Scott&numtimes=4`。</span><span class="sxs-lookup"><span data-stu-id="c771d-182">Run your application and visit `http://localhost:xx/HelloWorld/Welcome?name=Scott&numtimes=4` again.</span></span> <span data-ttu-id="c771d-183">现在，我们从 URL 获得数据，并自动将数据传递到控制器，控制器会将数据打包到 ViewModel，并将该对象传递到视图。</span><span class="sxs-lookup"><span data-stu-id="c771d-183">Now we're taking data from the URL, it's passed into our Controller automatically, our Controller packages up the data into a ViewModel and passes that object onto our View.</span></span> <span data-ttu-id="c771d-184">视图比向用户显示 HTML 数据。</span><span class="sxs-lookup"><span data-stu-id="c771d-184">The View than displays the data as HTML to the user.</span></span>

<span data-ttu-id="c771d-185">[![欢迎使用 Windows Internet Explorer](getting-started-with-mvc-part3/_static/image14.png)](getting-started-with-mvc-part3/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="c771d-185">[![Welcome - Windows Internet Explorer](getting-started-with-mvc-part3/_static/image14.png)](getting-started-with-mvc-part3/_static/image13.png)</span></span>

<span data-ttu-id="c771d-186">嗯，这是模型的 "M" 类型，但不是数据库类型。</span><span class="sxs-lookup"><span data-stu-id="c771d-186">Well, that was a kind of an "M" for Model, but not the database kind.</span></span> <span data-ttu-id="c771d-187">接下来，我们来看一下我们学到的内容，创建了一个电影数据库。</span><span class="sxs-lookup"><span data-stu-id="c771d-187">Let's take what we've learned and create a database of Movies.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="c771d-188">[上一页](getting-started-with-mvc-part2.md)
> [下一页](getting-started-with-mvc-part4.md)</span><span class="sxs-lookup"><span data-stu-id="c771d-188">[Previous](getting-started-with-mvc-part2.md)
[Next](getting-started-with-mvc-part4.md)</span></span>
