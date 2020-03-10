---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part5
title: 从控制器访问模型的数据 |Microsoft Docs
author: shanselman
description: 本教程介绍了 ASP.NET MVC 的基本知识。 创建一个从数据库中读取和写入数据的简单 web 应用程序。
ms.author: riande
ms.date: 08/14/2010
ms.assetid: 004703cd-e0e9-4ba7-9974-1b0475c71222
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part5
msc.type: authoredcontent
ms.openlocfilehash: 207ed880977d794d81efdc1ea458d17a68d501d8
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78437366"
---
# <a name="accessing-your-models-data-from-a-controller"></a><span data-ttu-id="52dc8-104">从控制器访问模型的数据</span><span class="sxs-lookup"><span data-stu-id="52dc8-104">Accessing your Model's Data from a Controller</span></span>

<span data-ttu-id="52dc8-105">作者： [Scott Hanselman](https://github.com/shanselman)</span><span class="sxs-lookup"><span data-stu-id="52dc8-105">by [Scott Hanselman](https://github.com/shanselman)</span></span>

> <span data-ttu-id="52dc8-106">本教程介绍了 ASP.NET MVC 的基本知识。</span><span class="sxs-lookup"><span data-stu-id="52dc8-106">This is a beginner tutorial that introduces the basics of ASP.NET MVC.</span></span> <span data-ttu-id="52dc8-107">你将创建一个简单的 web 应用程序，用于读取和写入数据库。</span><span class="sxs-lookup"><span data-stu-id="52dc8-107">You'll create a simple web application that reads and writes from a database.</span></span> <span data-ttu-id="52dc8-108">请访问[ASP.NET mvc 学习中心](../../../index.md)，查找其他 ASP.NET mvc 教程和示例。</span><span class="sxs-lookup"><span data-stu-id="52dc8-108">Visit the [ASP.NET MVC learning center](../../../index.md) to find other ASP.NET MVC tutorials and samples.</span></span>

<span data-ttu-id="52dc8-109">在本部分中，我们将创建一个新的 MoviesController 类，并编写一些代码来检索电影数据，并使用视图模板将其显示到浏览器。</span><span class="sxs-lookup"><span data-stu-id="52dc8-109">In this section we are going to create a new MoviesController class, and write some code that retrieves our Movie data and displays it back to the browser using a View template.</span></span>

<span data-ttu-id="52dc8-110">右键单击 "控制器" 文件夹，然后创建新的 MoviesController。</span><span class="sxs-lookup"><span data-stu-id="52dc8-110">Right click on the Controllers folder and make a new MoviesController.</span></span>

<span data-ttu-id="52dc8-111">[![添加控制器](getting-started-with-mvc-part5/_static/image2.png)](getting-started-with-mvc-part5/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="52dc8-111">[![Add Controller](getting-started-with-mvc-part5/_static/image2.png)](getting-started-with-mvc-part5/_static/image1.png)</span></span>

<span data-ttu-id="52dc8-112">这会在我们的项目中的 \Controllers 文件夹下创建新的 "MoviesController.cs" 文件。</span><span class="sxs-lookup"><span data-stu-id="52dc8-112">This will create a new "MoviesController.cs" file underneath our \Controllers folder within our project.</span></span> <span data-ttu-id="52dc8-113">让我们更新 MovieController，以便从新填充的数据库中检索电影列表。</span><span class="sxs-lookup"><span data-stu-id="52dc8-113">Let's update the MovieController to retrieve the list of movies from our newly populated database.</span></span>

[!code-csharp[Main](getting-started-with-mvc-part5/samples/sample1.cs)]

<span data-ttu-id="52dc8-114">我们正在执行 LINQ 查询，以便我们仅检索在1984年夏季发布的电影。</span><span class="sxs-lookup"><span data-stu-id="52dc8-114">We are performing a LINQ query so that we only retrieve movies released after the summer of 1984.</span></span> <span data-ttu-id="52dc8-115">我们需要一个视图模板来呈现此电影列表，因此右键单击方法并选择 "添加视图" 以创建它。</span><span class="sxs-lookup"><span data-stu-id="52dc8-115">We'll need a View template to render this list of movies back, so right-click in the method and select Add View to create it.</span></span>

<span data-ttu-id="52dc8-116">在 "添加视图" 对话框中，我们将指示要将列表&lt;的电影.&gt; 电影传递到我们的视图模板。</span><span class="sxs-lookup"><span data-stu-id="52dc8-116">Within the Add View dialog we'll indicate that we are passing a List&lt;Movies.Models.Movie&gt; to our View template.</span></span> <span data-ttu-id="52dc8-117">与以前使用 "添加视图" 对话框并选择创建 "空" 模板不同的是，这次我们将指示我们希望 Visual Studio 自动 "基架" 视图模板用于某些默认内容。</span><span class="sxs-lookup"><span data-stu-id="52dc8-117">Unlike the previous times we used the Add View dialog and chose to create an "Empty" template, this time we'll indicate that we want Visual Studio to automatically "scaffold" a view template for us with some default content.</span></span> <span data-ttu-id="52dc8-118">为此，请选择 "查看内容" 下拉菜单中的 "列表" 项。</span><span class="sxs-lookup"><span data-stu-id="52dc8-118">We'll do this by selecting the "List" item within the "View content dropdown menu.</span></span>

<span data-ttu-id="52dc8-119">请记住，当你创建了一个新类时，需要编译你的应用程序，使其显示在 "添加视图" 对话框中。</span><span class="sxs-lookup"><span data-stu-id="52dc8-119">Remember, when you have a created a new class you'll need to compile your application for it to show up in the Add View Dialog.</span></span>

![添加视图](getting-started-with-mvc-part5/_static/image3.png)

<span data-ttu-id="52dc8-121">单击 "添加"，系统将自动为我们的视图生成显示电影列表的代码。</span><span class="sxs-lookup"><span data-stu-id="52dc8-121">Click add and the system will automatically generate the code for a View for us that displays our list of movies.</span></span> <span data-ttu-id="52dc8-122">这是将 &lt;h2&gt; 标题更改为类似于 "我的电影列表" 的时间的好时机，就像我们先前在 Hello World 视图中做的一样。</span><span class="sxs-lookup"><span data-stu-id="52dc8-122">This is a good time to change the &lt;h2&gt; heading to something like "My Movie List" like we did earlier with the Hello World view.</span></span>

<span data-ttu-id="52dc8-123">[![电影-Microsoft Visual Web Developer 2010 Express](getting-started-with-mvc-part5/_static/image5.png)](getting-started-with-mvc-part5/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="52dc8-123">[![Movies - Microsoft Visual Web Developer 2010 Express](getting-started-with-mvc-part5/_static/image5.png)](getting-started-with-mvc-part5/_static/image4.png)</span></span>

<span data-ttu-id="52dc8-124">运行应用程序，并在地址栏中访问/Movies。</span><span class="sxs-lookup"><span data-stu-id="52dc8-124">Run your application and visit /Movies in the address bar.</span></span> <span data-ttu-id="52dc8-125">现在，我们已使用控制器中的基本查询从数据库中检索数据，并将数据返回到了解电影的视图。</span><span class="sxs-lookup"><span data-stu-id="52dc8-125">Now we've retrieved data from the database using a basic query inside the Controller and returned the data to a View that knows about Movies.</span></span> <span data-ttu-id="52dc8-126">然后，该视图将旋转影片列表，并为我们创建一个数据表。</span><span class="sxs-lookup"><span data-stu-id="52dc8-126">That View then spins through the list of Movies and creates a table of data for us.</span></span>

<span data-ttu-id="52dc8-127">[![电影列表-Windows Internet Explorer](getting-started-with-mvc-part5/_static/image7.png)](getting-started-with-mvc-part5/_static/image6.png)</span><span class="sxs-lookup"><span data-stu-id="52dc8-127">[![Movie List - Windows Internet Explorer](getting-started-with-mvc-part5/_static/image7.png)](getting-started-with-mvc-part5/_static/image6.png)</span></span>

<span data-ttu-id="52dc8-128">我们不会对此应用程序实现编辑、详细信息和删除功能，因此，我们不需要基架模板为我们创建的默认链接。</span><span class="sxs-lookup"><span data-stu-id="52dc8-128">We won't be implementing Edit, Details and Delete functionality with this application - so we don't need the default links that the scaffold template created for us.</span></span> <span data-ttu-id="52dc8-129">打开/Movies/Index.aspx 文件并将其删除。</span><span class="sxs-lookup"><span data-stu-id="52dc8-129">Open up the /Movies/Index.aspx file and remove them.</span></span>

<span data-ttu-id="52dc8-130">下面是我们进行这些更改后，更新的视图模板应类似于的源代码：</span><span class="sxs-lookup"><span data-stu-id="52dc8-130">Here is the source code for what our updated View template should look like once we make these changes:</span></span>

[!code-aspx[Main](getting-started-with-mvc-part5/samples/sample2.aspx)]

<span data-ttu-id="52dc8-131">它正在创建不需要的链接，因此，我们将在此示例中删除这些链接。</span><span class="sxs-lookup"><span data-stu-id="52dc8-131">It's creating links that we won't need, so we'll delete them for this example.</span></span> <span data-ttu-id="52dc8-132">不过，我们将继续创建新的链接，接下来是这样！</span><span class="sxs-lookup"><span data-stu-id="52dc8-132">We will keep our Create New link though, as that's next!</span></span> <span data-ttu-id="52dc8-133">下面是删除此列后应用的外观。</span><span class="sxs-lookup"><span data-stu-id="52dc8-133">Here's what our app looks like with that column removed.</span></span>

<span data-ttu-id="52dc8-134">[![电影列表-Windows Internet Explorer](getting-started-with-mvc-part5/_static/image9.png)](getting-started-with-mvc-part5/_static/image8.png)</span><span class="sxs-lookup"><span data-stu-id="52dc8-134">[![Movie List - Windows Internet Explorer](getting-started-with-mvc-part5/_static/image9.png)](getting-started-with-mvc-part5/_static/image8.png)</span></span>

<span data-ttu-id="52dc8-135">现在，我们提供了电影数据的简单列表。</span><span class="sxs-lookup"><span data-stu-id="52dc8-135">We now have a simple listing of our movie data.</span></span> <span data-ttu-id="52dc8-136">但是，如果单击 "新建" 链接，则会出现错误，因为它未挂钩！</span><span class="sxs-lookup"><span data-stu-id="52dc8-136">However, if we click the "Create New" link, we'll get an error as it's not hooked up!</span></span> <span data-ttu-id="52dc8-137">让我们实现一个创建操作方法，使用户能够在数据库中输入新电影。</span><span class="sxs-lookup"><span data-stu-id="52dc8-137">Let's implement a Create Action method and enable a user to enter new movies in our database.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="52dc8-138">[上一页](getting-started-with-mvc-part4.md)
> [下一页](getting-started-with-mvc-part6.md)</span><span class="sxs-lookup"><span data-stu-id="52dc8-138">[Previous](getting-started-with-mvc-part4.md)
[Next](getting-started-with-mvc-part6.md)</span></span>
