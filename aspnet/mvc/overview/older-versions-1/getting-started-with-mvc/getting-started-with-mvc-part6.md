---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part6
title: 添加 Create 方法和 Create View |Microsoft Docs
author: shanselman
description: 本教程介绍了 ASP.NET MVC 的基本知识。 创建一个从数据库中读取和写入数据的简单 web 应用程序。
ms.author: riande
ms.date: 08/14/2010
ms.assetid: a3a90963-0286-4fa0-9b3d-c230cc18b0a3
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part6
msc.type: authoredcontent
ms.openlocfilehash: 05a281720f76b107fe8d902ef60d5d2e72af3ef5
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78437288"
---
# <a name="adding-a-create-method-and-create-view"></a><span data-ttu-id="7dd62-104">添加 Create 方法和创建视图</span><span class="sxs-lookup"><span data-stu-id="7dd62-104">Adding a Create Method and Create View</span></span>

<span data-ttu-id="7dd62-105">作者： [Scott Hanselman](https://github.com/shanselman)</span><span class="sxs-lookup"><span data-stu-id="7dd62-105">by [Scott Hanselman](https://github.com/shanselman)</span></span>

> <span data-ttu-id="7dd62-106">本教程介绍了 ASP.NET MVC 的基本知识。</span><span class="sxs-lookup"><span data-stu-id="7dd62-106">This is a beginner tutorial that introduces the basics of ASP.NET MVC.</span></span> <span data-ttu-id="7dd62-107">你将创建一个简单的 web 应用程序，用于读取和写入数据库。</span><span class="sxs-lookup"><span data-stu-id="7dd62-107">You'll create a simple web application that reads and writes from a database.</span></span> <span data-ttu-id="7dd62-108">请访问[ASP.NET mvc 学习中心](../../../index.md)，查找其他 ASP.NET mvc 教程和示例。</span><span class="sxs-lookup"><span data-stu-id="7dd62-108">Visit the [ASP.NET MVC learning center](../../../index.md) to find other ASP.NET MVC tutorials and samples.</span></span>

<span data-ttu-id="7dd62-109">在本部分中，我们将实现使用户能够在数据库中创建新电影所需的支持。</span><span class="sxs-lookup"><span data-stu-id="7dd62-109">In this section we are going to implement the support necessary to enable users to create new movies in our database.</span></span> <span data-ttu-id="7dd62-110">我们将通过实现/Movies/Create URL 操作来实现此目的。</span><span class="sxs-lookup"><span data-stu-id="7dd62-110">We'll do this by implementing the /Movies/Create URL action.</span></span>

<span data-ttu-id="7dd62-111">实现/Movies/Create URL 的过程分为两个步骤。</span><span class="sxs-lookup"><span data-stu-id="7dd62-111">Implementing the /Movies/Create URL is a two step process.</span></span> <span data-ttu-id="7dd62-112">当用户首次访问/Movies/Create URL 时，我们想要向他们显示一个 HTML 窗体，用户可以填写该表单以输入新电影。</span><span class="sxs-lookup"><span data-stu-id="7dd62-112">When a user first visits the /Movies/Create URL we want to show them an HTML form that they can fill out to enter a new movie.</span></span> <span data-ttu-id="7dd62-113">然后，当用户提交窗体并将数据回发到服务器时，我们想要检索已发布的内容并将其保存到数据库中。</span><span class="sxs-lookup"><span data-stu-id="7dd62-113">Then, when the user submits the form and posts the data back to the server, we want to retrieve the posted contents and save it into our database.</span></span>

<span data-ttu-id="7dd62-114">我们将在 MoviesController 类中的两个 Create （）方法内实现这两个步骤。</span><span class="sxs-lookup"><span data-stu-id="7dd62-114">We'll implement these two steps within two Create() methods within our MoviesController class.</span></span> <span data-ttu-id="7dd62-115">一种方法将显示 &lt;窗体&gt; 用户应填写该窗体来创建新电影。</span><span class="sxs-lookup"><span data-stu-id="7dd62-115">One method will show the &lt;form&gt; that the user should fill out to create a new movie.</span></span> <span data-ttu-id="7dd62-116">第二种方法将处理在用户将 &lt;窗体&gt; 回服务器，并将新电影保存在数据库中时，处理已发布数据。</span><span class="sxs-lookup"><span data-stu-id="7dd62-116">The second method will handle processing the posted data when the user submits the &lt;form&gt; back to the server, and save a new Movie within our database.</span></span>

<span data-ttu-id="7dd62-117">下面是我们要将其添加到 MoviesController 类以实现此操作的代码：</span><span class="sxs-lookup"><span data-stu-id="7dd62-117">Below is the code we'll add to our MoviesController class to implement this:</span></span>

[!code-csharp[Main](getting-started-with-mvc-part6/samples/sample1.cs)]

<span data-ttu-id="7dd62-118">上面的代码包含我们在控制器中需要的所有代码。</span><span class="sxs-lookup"><span data-stu-id="7dd62-118">The above code contains all of the code that we'll need within our Controller.</span></span>

<span data-ttu-id="7dd62-119">现在，让我们实现 "创建视图" 模板，用于向用户显示窗体。</span><span class="sxs-lookup"><span data-stu-id="7dd62-119">Let's now implement the Create View template that we'll use to display a form to the user.</span></span> <span data-ttu-id="7dd62-120">我们将在第一个 Create 方法中右键单击，然后选择 "添加视图"，为电影窗体创建视图模板。</span><span class="sxs-lookup"><span data-stu-id="7dd62-120">We'll right click in the first Create method and select "Add View" to create the view template for our Movie form.</span></span>

<span data-ttu-id="7dd62-121">我们将选择我们要将 "电影" 作为其视图数据类传递到 "电影"，并指出我们想要 "基架" 模板。</span><span class="sxs-lookup"><span data-stu-id="7dd62-121">We'll select that we are going to pass the view template a "Movie" as its view data class, and indicate that we want to "scaffold" a "Create" template.</span></span>

<span data-ttu-id="7dd62-122">[![添加视图](getting-started-with-mvc-part6/_static/image2.png)](getting-started-with-mvc-part6/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="7dd62-122">[![Add View](getting-started-with-mvc-part6/_static/image2.png)](getting-started-with-mvc-part6/_static/image1.png)</span></span>

<span data-ttu-id="7dd62-123">单击 "添加" 按钮后，将为你创建 \Movies\Create.aspx 视图模板。</span><span class="sxs-lookup"><span data-stu-id="7dd62-123">After you click the Add button, \Movies\Create.aspx View template will be created for you.</span></span> <span data-ttu-id="7dd62-124">由于我们从 "查看内容" 下拉列表中选择了 "创建"，因此 "添加视图" 对话框会自动 "基架" 某些默认内容。</span><span class="sxs-lookup"><span data-stu-id="7dd62-124">Because we selected "Create" from the "view content" dropdown, the Add View dialog automatically "scaffolded" some default content for us.</span></span> <span data-ttu-id="7dd62-125">基架创建了 HTML &lt;窗体&gt;、用于验证错误消息的位置，并且由于基架知道了电影，因此它为类的每个属性创建了标签和字段。</span><span class="sxs-lookup"><span data-stu-id="7dd62-125">The scaffolding created an HTML &lt;form&gt;, a place for validation error messages to go, and since scaffolding knows about Movies, it created Label and Fields for each property of our class.</span></span>

[!code-aspx[Main](getting-started-with-mvc-part6/samples/sample2.aspx)]

<span data-ttu-id="7dd62-126">由于数据库会自动为电影提供 ID，因此请删除引用模型的那些字段。创建视图的 Id。</span><span class="sxs-lookup"><span data-stu-id="7dd62-126">Since our database automatically gives a Movie an ID, let's remove those fields that reference model.Id from our Create View.</span></span> <span data-ttu-id="7dd62-127">在 &lt;图例后删除7行&gt;字段&lt;/legend&gt;，因为它们显示了我们不想要的 ID 字段。</span><span class="sxs-lookup"><span data-stu-id="7dd62-127">Remove the 7 lines after &lt;legend&gt;Fields&lt;/legend&gt; as they show the ID field that we don't want.</span></span>

<span data-ttu-id="7dd62-128">现在，让我们创建一个新电影，并将其添加到数据库中。</span><span class="sxs-lookup"><span data-stu-id="7dd62-128">Let's now create a new movie and add it to the database.</span></span> <span data-ttu-id="7dd62-129">为此，我们将再次运行该应用程序，并访问 "/Movies" URL，并单击 "创建" 链接以添加新电影。</span><span class="sxs-lookup"><span data-stu-id="7dd62-129">We'll do this by running the application again and visit the "/Movies" URL and click the "Create" link to add a new Movie.</span></span>

<span data-ttu-id="7dd62-130">[![创建-Windows Internet Explorer](getting-started-with-mvc-part6/_static/image4.png)](getting-started-with-mvc-part6/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="7dd62-130">[![Create - Windows Internet Explorer](getting-started-with-mvc-part6/_static/image4.png)](getting-started-with-mvc-part6/_static/image3.png)</span></span>

<span data-ttu-id="7dd62-131">单击 "创建" 按钮时，会将此窗体上的数据回发到刚刚创建的/Movies/Create 方法（通过 HTTP POST）。</span><span class="sxs-lookup"><span data-stu-id="7dd62-131">When we click the Create button, we'll be posting back (via HTTP POST) the data on this form to the /Movies/Create method that we just created.</span></span> <span data-ttu-id="7dd62-132">就像系统自动从 URL 开始使用 "numTimes" 和 "name" 参数，并将其映射到前面方法中的参数时，系统将自动从 POST 获取窗体字段，并将它们映射到对象。</span><span class="sxs-lookup"><span data-stu-id="7dd62-132">Just like when the system automatically took the "numTimes" and "name " parameter out of the URL and mapped them to parameters on a method earlier, the system will automatically take the Form Fields from a POST and map them to an object.</span></span> <span data-ttu-id="7dd62-133">在这种情况下，HTML 中的字段中的值（如 "ReleaseDate" 和 "Title"）将自动放入电影新实例的正确属性。</span><span class="sxs-lookup"><span data-stu-id="7dd62-133">In this case, values from fields in HTML like "ReleaseDate" and "Title" will automatically be put into the correct properties of a new instance of a Movie.</span></span>

<span data-ttu-id="7dd62-134">让我们再次看一看 MoviesController 中的第二个 Create 方法。</span><span class="sxs-lookup"><span data-stu-id="7dd62-134">Let's look at the second Create method from our MoviesController again.</span></span> <span data-ttu-id="7dd62-135">请注意它如何将 "电影" 对象作为参数：</span><span class="sxs-lookup"><span data-stu-id="7dd62-135">Notice how it takes a "Movie" object as an argument:</span></span>

[!code-csharp[Main](getting-started-with-mvc-part6/samples/sample3.cs)]

<span data-ttu-id="7dd62-136">然后将此电影对象传递到创建操作方法的 [HttpPost] 版本，并将其保存在数据库中，然后将用户重定向回 Index （）操作方法，该操作方法会在电影列表中显示保存的结果：</span><span class="sxs-lookup"><span data-stu-id="7dd62-136">This Movie object was then passed to the [HttpPost] version of our Create action method, and we saved it in the database and then redirected the user back to the Index() action method which will show the saved result in the movie list:</span></span>

<span data-ttu-id="7dd62-137">[![电影列表-Windows Internet Explorer](getting-started-with-mvc-part6/_static/image6.png)](getting-started-with-mvc-part6/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="7dd62-137">[![Movie List - Windows Internet Explorer](getting-started-with-mvc-part6/_static/image6.png)](getting-started-with-mvc-part6/_static/image5.png)</span></span>

<span data-ttu-id="7dd62-138">但我们不会检查电影是否正确，并且数据库不会允许我们保存无标题的电影。</span><span class="sxs-lookup"><span data-stu-id="7dd62-138">We aren't checking if our movies are correct, though, and the database won't allow us to save a movie with no Title.</span></span> <span data-ttu-id="7dd62-139">如果可以告诉用户在数据库出现错误之前，这会很好。</span><span class="sxs-lookup"><span data-stu-id="7dd62-139">It'd be nice if we could tell the user that before the database threw an error.</span></span> <span data-ttu-id="7dd62-140">接下来，我们将向应用程序添加验证支持。</span><span class="sxs-lookup"><span data-stu-id="7dd62-140">We'll do this next by adding validation support to our application.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="7dd62-141">[上一页](getting-started-with-mvc-part5.md)
> [下一页](getting-started-with-mvc-part7.md)</span><span class="sxs-lookup"><span data-stu-id="7dd62-141">[Previous](getting-started-with-mvc-part5.md)
[Next](getting-started-with-mvc-part7.md)</span></span>
