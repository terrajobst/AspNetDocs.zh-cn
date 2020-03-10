---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part8
title: 向模型添加列 |Microsoft Docs
author: shanselman
description: 本教程介绍了 ASP.NET MVC 的基本知识。 创建一个从数据库中读取和写入数据的简单 web 应用程序。
ms.author: riande
ms.date: 08/14/2010
ms.assetid: 7ae696b9-348f-4993-8ebb-a838acbe0c28
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part8
msc.type: authoredcontent
ms.openlocfilehash: 1cf092c3db3959d6f47006f1be2ba82833c5dc06
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78437222"
---
# <a name="adding-a-column-to-the-model"></a><span data-ttu-id="2efbd-104">向模型添加列</span><span class="sxs-lookup"><span data-stu-id="2efbd-104">Adding a Column to the Model</span></span>

<span data-ttu-id="2efbd-105">作者： [Scott Hanselman](https://github.com/shanselman)</span><span class="sxs-lookup"><span data-stu-id="2efbd-105">by [Scott Hanselman](https://github.com/shanselman)</span></span>

> <span data-ttu-id="2efbd-106">本教程介绍了 ASP.NET MVC 的基本知识。</span><span class="sxs-lookup"><span data-stu-id="2efbd-106">This is a beginner tutorial that introduces the basics of ASP.NET MVC.</span></span> <span data-ttu-id="2efbd-107">你将创建一个简单的 web 应用程序，用于读取和写入数据库。</span><span class="sxs-lookup"><span data-stu-id="2efbd-107">You'll create a simple web application that reads and writes from a database.</span></span> <span data-ttu-id="2efbd-108">请访问[ASP.NET mvc 学习中心](../../../index.md)，查找其他 ASP.NET mvc 教程和示例。</span><span class="sxs-lookup"><span data-stu-id="2efbd-108">Visit the [ASP.NET MVC learning center](../../../index.md) to find other ASP.NET MVC tutorials and samples.</span></span>

<span data-ttu-id="2efbd-109">在本部分中，我们将演练如何更改数据库的架构，并处理应用程序中的更改。</span><span class="sxs-lookup"><span data-stu-id="2efbd-109">In this section we are going to walk through how we can make changes to the schema of our database, and handle the changes within our application.</span></span>

<span data-ttu-id="2efbd-110">让我们将 "分级" 列添加到 "电影" 表中。</span><span class="sxs-lookup"><span data-stu-id="2efbd-110">Let's add a "Rating" Column to the Movie table.</span></span> <span data-ttu-id="2efbd-111">返回到 IDE，并单击数据库资源管理器。</span><span class="sxs-lookup"><span data-stu-id="2efbd-111">Go back to the IDE and click the Database Explorer.</span></span> <span data-ttu-id="2efbd-112">右键单击电影表，然后选择 "打开表定义"。</span><span class="sxs-lookup"><span data-stu-id="2efbd-112">Right click the Movie table and select Open Table Definition.</span></span>

<span data-ttu-id="2efbd-113">添加 "评级" 列，如下所示。</span><span class="sxs-lookup"><span data-stu-id="2efbd-113">Add a "Rating" column as seen below.</span></span> <span data-ttu-id="2efbd-114">由于我们现在没有任何分级，列可以允许空值。</span><span class="sxs-lookup"><span data-stu-id="2efbd-114">Since we don't have any Ratings now, the column can allow nulls.</span></span> <span data-ttu-id="2efbd-115">单击“保存”。</span><span class="sxs-lookup"><span data-stu-id="2efbd-115">Click Save.</span></span>

<span data-ttu-id="2efbd-116">[![编辑电影表](getting-started-with-mvc-part8/_static/image2.png)](getting-started-with-mvc-part8/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="2efbd-116">[![Editing Movies Table](getting-started-with-mvc-part8/_static/image2.png)](getting-started-with-mvc-part8/_static/image1.png)</span></span>

<span data-ttu-id="2efbd-117">接下来，返回到解决方案资源管理器并打开电影 .edmx 文件（在 \Models 文件夹中）。</span><span class="sxs-lookup"><span data-stu-id="2efbd-117">Next, return to the Solution Explorer and open up the Movies.edmx file (which is in the \Models folder).</span></span> <span data-ttu-id="2efbd-118">右键单击设计图面（白色区域），然后选择 "从数据库更新模型"。</span><span class="sxs-lookup"><span data-stu-id="2efbd-118">Right click on the design surface (the white area) and select Update Model from Database.</span></span>

<span data-ttu-id="2efbd-119">[![电影-Microsoft Visual Web Developer 2010 Express （11）](getting-started-with-mvc-part8/_static/image4.png)](getting-started-with-mvc-part8/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="2efbd-119">[![Movies - Microsoft Visual Web Developer 2010 Express (11)](getting-started-with-mvc-part8/_static/image4.png)](getting-started-with-mvc-part8/_static/image3.png)</span></span>

<span data-ttu-id="2efbd-120">这会启动 "更新向导"。</span><span class="sxs-lookup"><span data-stu-id="2efbd-120">This will launch the "Update Wizard".</span></span> <span data-ttu-id="2efbd-121">单击其中的 "刷新" 选项卡，然后单击 "完成"。</span><span class="sxs-lookup"><span data-stu-id="2efbd-121">Click the Refresh tab within it and click Finish.</span></span> <span data-ttu-id="2efbd-122">然后，将用新列更新我们的 Movie 模型类。</span><span class="sxs-lookup"><span data-stu-id="2efbd-122">Our Movie model class will then be updated with the new column.</span></span>

![更新向导（2）](getting-started-with-mvc-part8/_static/image5.png)

<span data-ttu-id="2efbd-124">单击 "完成" 后，可以看到新的 "评级" 列已添加到模型中的 "电影" 实体。</span><span class="sxs-lookup"><span data-stu-id="2efbd-124">After clicking Finish, you can see the new Rating Column has been added to the Movie Entity in our model.</span></span>

<span data-ttu-id="2efbd-125">[![电影实体](getting-started-with-mvc-part8/_static/image7.png)](getting-started-with-mvc-part8/_static/image6.png)</span><span class="sxs-lookup"><span data-stu-id="2efbd-125">[![Movie Entity](getting-started-with-mvc-part8/_static/image7.png)](getting-started-with-mvc-part8/_static/image6.png)</span></span>

<span data-ttu-id="2efbd-126">我们在数据库模型中添加了一个列，但视图并不知道它。</span><span class="sxs-lookup"><span data-stu-id="2efbd-126">We've added a column in the database model, but the Views don't know about it.</span></span>

## <a name="update-views-with-model-changes"></a><span data-ttu-id="2efbd-127">用模型更改更新视图</span><span class="sxs-lookup"><span data-stu-id="2efbd-127">Update Views with Model Changes</span></span>

<span data-ttu-id="2efbd-128">可以通过几种方式来更新视图模板，以反映新的评级列。</span><span class="sxs-lookup"><span data-stu-id="2efbd-128">There are a few ways we could update our view templates to reflect the new Rating column.</span></span> <span data-ttu-id="2efbd-129">由于我们通过 "添加视图" 对话框生成这些视图，因此可以将其删除并重新创建它们。</span><span class="sxs-lookup"><span data-stu-id="2efbd-129">Since we created these Views by generating them via the Add View dialog, we could delete them and recreate them again.</span></span> <span data-ttu-id="2efbd-130">不过，通常情况下，用户已从初始基架生成中对其视图模板进行了修改，并需要手动添加或删除字段，就像我们使用 Create 的 ID 字段做的一样。</span><span class="sxs-lookup"><span data-stu-id="2efbd-130">However, typically people will have already made modifications to their View templates from the initial scaffolded generation and will want to add or delete fields manually, just as we did with the ID field for Create.</span></span>

<span data-ttu-id="2efbd-131">打开 "\Views\Movies\Index.aspx" 模板，将 &lt;&gt;评级添加到 "电影" 表的开头&lt;"&gt;"。</span><span class="sxs-lookup"><span data-stu-id="2efbd-131">Open up the \Views\Movies\Index.aspx template and add a &lt;th&gt;Rating&lt;/th&gt; to the head of the Movie table.</span></span> <span data-ttu-id="2efbd-132">我添加了我在流派后的我。</span><span class="sxs-lookup"><span data-stu-id="2efbd-132">I added mine after Genre.</span></span> <span data-ttu-id="2efbd-133">然后，在同一列位置但向下减小，添加一行来输出我们的新分级。</span><span class="sxs-lookup"><span data-stu-id="2efbd-133">Then, in the same column position but lower down, add a line to output our new Rating.</span></span>

[!code-aspx[Main](getting-started-with-mvc-part8/samples/sample1.aspx)]

<span data-ttu-id="2efbd-134">最终的 "索引 .aspx" 模板将如下所示：</span><span class="sxs-lookup"><span data-stu-id="2efbd-134">Our final Index.aspx template will look like this:</span></span>

[!code-aspx[Main](getting-started-with-mvc-part8/samples/sample2.aspx)]

<span data-ttu-id="2efbd-135">接下来，打开 \Views\Movies\Create.aspx 模板，为新的 "分级" 属性添加标签和文本框：</span><span class="sxs-lookup"><span data-stu-id="2efbd-135">Let's then open up the \Views\Movies\Create.aspx template and add a Label and Textbox for our new Rating property:</span></span>

[!code-aspx[Main](getting-started-with-mvc-part8/samples/sample3.aspx)]

<span data-ttu-id="2efbd-136">我们的最后一个 Create .aspx 模板将如下所示，并将浏览器的标题和辅助 &lt;&gt; h2 改为将其标题更改为类似于 "创建电影" 的内容，而在这里我们就会这样！</span><span class="sxs-lookup"><span data-stu-id="2efbd-136">Our final Create.aspx template will look like this, and let's change our browser's title and secondary &lt;h2&gt; title to something like "Create a Movie" while we're in here!</span></span>

[!code-aspx[Main](getting-started-with-mvc-part8/samples/sample4.aspx)]

<span data-ttu-id="2efbd-137">运行你的应用程序，此时已在数据库中添加了一个新字段，该字段已添加到 "创建" 页。</span><span class="sxs-lookup"><span data-stu-id="2efbd-137">Run your app and now you've got a new field in the database that's been added to the Create page.</span></span> <span data-ttu-id="2efbd-138">添加新电影-这次带有评级，并单击 "创建"。</span><span class="sxs-lookup"><span data-stu-id="2efbd-138">Add a new Movie - this time with a Rating - and click Create.</span></span>

<span data-ttu-id="2efbd-139">[![创建电影-Windows Internet Explorer](getting-started-with-mvc-part8/_static/image9.png)](getting-started-with-mvc-part8/_static/image8.png)</span><span class="sxs-lookup"><span data-stu-id="2efbd-139">[![Create a Movie - Windows Internet Explorer](getting-started-with-mvc-part8/_static/image9.png)](getting-started-with-mvc-part8/_static/image8.png)</span></span>

<span data-ttu-id="2efbd-140">单击 "创建" 后，将被发送到 "索引" 页，在该页面中，新电影将与数据库中的新 "分级" 列一起列出。</span><span class="sxs-lookup"><span data-stu-id="2efbd-140">After you click Create, you're sent to the Index page where you new Movie is listed with the new Rating Column in the database</span></span>

<span data-ttu-id="2efbd-141">[![电影列表-Windows Internet Explorer （12）](getting-started-with-mvc-part8/_static/image11.png)](getting-started-with-mvc-part8/_static/image10.png)</span><span class="sxs-lookup"><span data-stu-id="2efbd-141">[![Movie List - Windows Internet Explorer (12)](getting-started-with-mvc-part8/_static/image11.png)](getting-started-with-mvc-part8/_static/image10.png)</span></span>

<span data-ttu-id="2efbd-142">本基本教程介绍了如何开始创建控制器，如何将它们与视图相关联，并将其传递给硬编码数据。</span><span class="sxs-lookup"><span data-stu-id="2efbd-142">This basic tutorial got you started making Controllers, associating them with Views and passing around hard-coded data.</span></span> <span data-ttu-id="2efbd-143">然后，我们创建并设计了一个数据库，并在其中放置了一些数据。</span><span class="sxs-lookup"><span data-stu-id="2efbd-143">Then we created and designed a Database and put some data it in.</span></span> <span data-ttu-id="2efbd-144">我们从数据库中检索数据并将其显示在 HTML 表中。</span><span class="sxs-lookup"><span data-stu-id="2efbd-144">We retrieved the data from the database and displayed it in an HTML table.</span></span> <span data-ttu-id="2efbd-145">然后，我们添加了一个 Create 窗体，该窗体使用户能够在 Web 应用程序中向数据库本身添加数据。</span><span class="sxs-lookup"><span data-stu-id="2efbd-145">Then we added a Create form that let the user add data to the database themselves from within the Web Application.</span></span> <span data-ttu-id="2efbd-146">我们添加了验证，然后在客户端使用 JavaScript 进行验证。</span><span class="sxs-lookup"><span data-stu-id="2efbd-146">We added validation, then made the validation use JavaScript on the client-side.</span></span> <span data-ttu-id="2efbd-147">最后，我们已将数据库更改为包含新的数据列，然后更新了两个页面以创建和显示此新数据。</span><span class="sxs-lookup"><span data-stu-id="2efbd-147">Finally, we changed the database to include a new column of data, then updated our two pages to create and display this new data.</span></span>

<span data-ttu-id="2efbd-148">我现在建议你转到我们的中级教程 "[MVC 音乐应用商店](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)"，以及[https://asp.net/mvc](https://asp.net/mvc)的多个视频和资源，以详细了解 ASP.NET MVC！</span><span class="sxs-lookup"><span data-stu-id="2efbd-148">I now encourage you to move on to our intermediate-level tutorial "[MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)" as well as the many videos and resources at [https://asp.net/mvc](https://asp.net/mvc) to learn even more about ASP.NET MVC!</span></span>

<span data-ttu-id="2efbd-149">请尽情体验吧！</span><span class="sxs-lookup"><span data-stu-id="2efbd-149">Enjoy!</span></span>

- <span data-ttu-id="2efbd-150">Scott Hanselman-在 Twitter 上[http://hanselman.com](http://hanselman.com)和[@shanselman](http://twitter.com/shanselman) 。</span><span class="sxs-lookup"><span data-stu-id="2efbd-150">Scott Hanselman - [http://hanselman.com](http://hanselman.com) and [@shanselman](http://twitter.com/shanselman) on Twitter.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="2efbd-151">上一页</span><span class="sxs-lookup"><span data-stu-id="2efbd-151">Previous</span></span>](getting-started-with-mvc-part7.md)
