---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-4
title: 第4部分：模型和数据访问 |Microsoft Docs
author: jongalloway
description: 本教程系列详细介绍了生成 ASP.NET MVC 音乐应用商店示例应用程序所需执行的所有步骤。 第4部分介绍了模型和数据访问。
ms.author: riande
ms.date: 04/21/2011
ms.assetid: ab55ca81-ab9b-44a0-8700-dc6da2599335
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-4
msc.type: authoredcontent
ms.openlocfilehash: 402be340f1ea3344675e7b859cea8c5130cfc8ee
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78451016"
---
# <a name="part-4-models-and-data-access"></a><span data-ttu-id="0803f-104">第4部分：模型和数据访问</span><span class="sxs-lookup"><span data-stu-id="0803f-104">Part 4: Models and Data Access</span></span>

<span data-ttu-id="0803f-105">作者： [Jon Galloway](https://github.com/jongalloway)</span><span class="sxs-lookup"><span data-stu-id="0803f-105">by [Jon Galloway](https://github.com/jongalloway)</span></span>

> <span data-ttu-id="0803f-106">MVC 音乐应用商店是一个教程应用程序，该应用程序逐步介绍了如何使用 ASP.NET MVC 和 Visual Studio 进行 web 开发。</span><span class="sxs-lookup"><span data-stu-id="0803f-106">The MVC Music Store is a tutorial application that introduces and explains step-by-step how to use ASP.NET MVC and Visual Studio for web development.</span></span>  
>   
> <span data-ttu-id="0803f-107">MVC 音乐应用商店是一种轻型示例存储实现，它可以在线销售音乐专辑，并实现基本的网站管理、用户登录和购物车功能。</span><span class="sxs-lookup"><span data-stu-id="0803f-107">The MVC Music Store is a lightweight sample store implementation which sells music albums online, and implements basic site administration, user sign-in, and shopping cart functionality.</span></span>
> 
> <span data-ttu-id="0803f-108">本教程系列详细介绍了生成 ASP.NET MVC 音乐应用商店示例应用程序所需执行的所有步骤。</span><span class="sxs-lookup"><span data-stu-id="0803f-108">This tutorial series details all of the steps taken to build the ASP.NET MVC Music Store sample application.</span></span> <span data-ttu-id="0803f-109">第4部分介绍了模型和数据访问。</span><span class="sxs-lookup"><span data-stu-id="0803f-109">Part 4 covers Models and Data Access.</span></span>

<span data-ttu-id="0803f-110">到目前为止，我们只是将控制器中的 "虚拟数据" 传递到我们的视图模板。</span><span class="sxs-lookup"><span data-stu-id="0803f-110">So far, we've just been passing "dummy data" from our Controllers to our View templates.</span></span> <span data-ttu-id="0803f-111">现在，我们已准备好挂钩实际数据库。</span><span class="sxs-lookup"><span data-stu-id="0803f-111">Now we're ready to hook up a real database.</span></span> <span data-ttu-id="0803f-112">在本教程中，我们将介绍如何使用 SQL Server Compact 版（通常称为 SQL CE）作为数据库引擎。</span><span class="sxs-lookup"><span data-stu-id="0803f-112">In this tutorial we'll be covering how to use SQL Server Compact Edition (often called SQL CE) as our database engine.</span></span> <span data-ttu-id="0803f-113">SQL CE 是一个基于文件的免费嵌入式数据库，不需要任何安装或配置，这使得本地开发非常方便。</span><span class="sxs-lookup"><span data-stu-id="0803f-113">SQL CE is a free, embedded, file based database that doesn't require any installation or configuration, which makes it really convenient for local development.</span></span>

## <a name="database-access-with-entity-framework-code-first"></a><span data-ttu-id="0803f-114">使用实体框架代码的数据库访问-第一项</span><span class="sxs-lookup"><span data-stu-id="0803f-114">Database access with Entity Framework Code-First</span></span>

<span data-ttu-id="0803f-115">我们将使用 ASP.NET MVC 3 项目中包含的实体框架（EF）支持来查询和更新数据库。</span><span class="sxs-lookup"><span data-stu-id="0803f-115">We'll use the Entity Framework (EF) support that is included in ASP.NET MVC 3 projects to query and update the database.</span></span> <span data-ttu-id="0803f-116">EF 是一个灵活的对象关系映射（ORM）数据 API，使开发人员能够以面向对象的方式查询和更新存储在数据库中的数据。</span><span class="sxs-lookup"><span data-stu-id="0803f-116">EF is a flexible object relational mapping (ORM) data API that enables developers to query and update data stored in a database in an object-oriented way.</span></span>

<span data-ttu-id="0803f-117">实体框架版本4支持称为 "代码优先" 的开发模式。</span><span class="sxs-lookup"><span data-stu-id="0803f-117">Entity Framework version 4 supports a development paradigm called code-first.</span></span> <span data-ttu-id="0803f-118">代码优先允许您通过编写简单的类（也称为 "纯旧式" CLR 对象中的 POCO）来创建模型对象，甚至可以通过类动态创建数据库。</span><span class="sxs-lookup"><span data-stu-id="0803f-118">Code-first allows you to create model object by writing simple classes (also known as POCO from "plain-old" CLR objects), and can even create the database on the fly from your classes.</span></span>

### <a name="changes-to-our-model-classes"></a><span data-ttu-id="0803f-119">对模型类的更改</span><span class="sxs-lookup"><span data-stu-id="0803f-119">Changes to our Model Classes</span></span>

<span data-ttu-id="0803f-120">在本教程的实体框架中，我们将利用数据库创建功能。</span><span class="sxs-lookup"><span data-stu-id="0803f-120">We will be leveraging the database creation feature in Entity Framework in this tutorial.</span></span> <span data-ttu-id="0803f-121">不过，在这样做之前，让我们对我们的模型类进行一些小的更改，以便添加到我们稍后将使用的一些功能。</span><span class="sxs-lookup"><span data-stu-id="0803f-121">Before we do that, though, let's make a few minor changes to our model classes to add in some things we'll be using later on.</span></span>

#### <a name="adding-the-artist-model-classes"></a><span data-ttu-id="0803f-122">添加艺术家模型类</span><span class="sxs-lookup"><span data-stu-id="0803f-122">Adding the Artist Model Classes</span></span>

<span data-ttu-id="0803f-123">我们的唱集将与艺术家相关联，因此，我们将添加一个用于描述艺术家的简单模型类。</span><span class="sxs-lookup"><span data-stu-id="0803f-123">Our Albums will be associated with Artists, so we'll add a simple model class to describe an Artist.</span></span> <span data-ttu-id="0803f-124">使用如下所示的代码，将一个新类添加到名为 Artist.cs 的模型文件夹中。</span><span class="sxs-lookup"><span data-stu-id="0803f-124">Add a new class to the Models folder named Artist.cs using the code shown below.</span></span>

[!code-csharp[Main](mvc-music-store-part-4/samples/sample1.cs)]

#### <a name="updating-our-model-classes"></a><span data-ttu-id="0803f-125">更新模型类</span><span class="sxs-lookup"><span data-stu-id="0803f-125">Updating our Model Classes</span></span>

<span data-ttu-id="0803f-126">更新唱片集类，如下所示。</span><span class="sxs-lookup"><span data-stu-id="0803f-126">Update the Album class as shown below.</span></span>

[!code-csharp[Main](mvc-music-store-part-4/samples/sample2.cs)]

<span data-ttu-id="0803f-127">接下来，对流派类进行以下更新。</span><span class="sxs-lookup"><span data-stu-id="0803f-127">Next, make the following updates to the Genre class.</span></span>

[!code-csharp[Main](mvc-music-store-part-4/samples/sample3.cs)]

### <a name="adding-the-app_data-folder"></a><span data-ttu-id="0803f-128">添加应用\_Data 文件夹</span><span class="sxs-lookup"><span data-stu-id="0803f-128">Adding the App\_Data folder</span></span>

<span data-ttu-id="0803f-129">我们会将一个应用\_数据目录添加到项目中，以便保存 SQL Server Express 数据库文件。</span><span class="sxs-lookup"><span data-stu-id="0803f-129">We'll add an App\_Data directory to our project to hold our SQL Server Express database files.</span></span> <span data-ttu-id="0803f-130">应用\_数据是 ASP.NET 中的一个特殊目录，它已经具有数据库访问的正确安全访问权限。</span><span class="sxs-lookup"><span data-stu-id="0803f-130">App\_Data is a special directory in ASP.NET which already has the correct security access permissions for database access.</span></span> <span data-ttu-id="0803f-131">从 "项目" 菜单中，选择 "添加 ASP.NET 文件夹"，然后选择 "应用\_数据"。</span><span class="sxs-lookup"><span data-stu-id="0803f-131">From the Project menu, select Add ASP.NET Folder, then App\_Data.</span></span>

![](mvc-music-store-part-4/_static/image1.png)

### <a name="creating-a-connection-string-in-the-webconfig-file"></a><span data-ttu-id="0803f-132">在 web.config 文件中创建连接字符串</span><span class="sxs-lookup"><span data-stu-id="0803f-132">Creating a Connection String in the web.config file</span></span>

<span data-ttu-id="0803f-133">我们将在网站的配置文件中添加几行，以便实体框架知道如何连接到数据库。</span><span class="sxs-lookup"><span data-stu-id="0803f-133">We will add a few lines to the website's configuration file so that Entity Framework knows how to connect to our database.</span></span> <span data-ttu-id="0803f-134">双击位于项目根目录中的 web.config 文件。</span><span class="sxs-lookup"><span data-stu-id="0803f-134">Double-click on the Web.config file located in the root of the project.</span></span>

![](mvc-music-store-part-4/_static/image2.png)

<span data-ttu-id="0803f-135">滚动到此文件的底部，并将 &lt;connectionStrings&gt; 部分直接添加到最后一行的上方，如下所示。</span><span class="sxs-lookup"><span data-stu-id="0803f-135">Scroll to the bottom of this file and add a &lt;connectionStrings&gt; section directly above the last line, as shown below.</span></span>

[!code-xml[Main](mvc-music-store-part-4/samples/sample4.xml)]

### <a name="adding-a-context-class"></a><span data-ttu-id="0803f-136">添加上下文类</span><span class="sxs-lookup"><span data-stu-id="0803f-136">Adding a Context Class</span></span>

<span data-ttu-id="0803f-137">右键单击 "模型" 文件夹，并添加名为 MusicStoreEntities.cs 的新类。</span><span class="sxs-lookup"><span data-stu-id="0803f-137">Right-click the Models folder and add a new class named MusicStoreEntities.cs.</span></span>

![](mvc-music-store-part-4/_static/image3.png)

<span data-ttu-id="0803f-138">此类将表示实体框架数据库上下文，并将为我们处理创建、读取、更新和删除操作。</span><span class="sxs-lookup"><span data-stu-id="0803f-138">This class will represent the Entity Framework database context, and will handle our create, read, update, and delete operations for us.</span></span> <span data-ttu-id="0803f-139">此类的代码如下所示。</span><span class="sxs-lookup"><span data-stu-id="0803f-139">The code for this class is shown below.</span></span>

[!code-csharp[Main](mvc-music-store-part-4/samples/sample5.cs)]

<span data-ttu-id="0803f-140">就是这样-没有其他配置、特殊接口等。通过扩展 DbContext 基类，我们的 MusicStoreEntities 类能够处理我们的数据库操作。</span><span class="sxs-lookup"><span data-stu-id="0803f-140">That's it - there's no other configuration, special interfaces, etc. By extending the DbContext base class, our MusicStoreEntities class is able to handle our database operations for us.</span></span> <span data-ttu-id="0803f-141">至此，我们已经知道了，接下来，让我们将更多属性添加到我们的模型类，以利用数据库中的一些附加信息。</span><span class="sxs-lookup"><span data-stu-id="0803f-141">Now that we've got that hooked up, let's add a few more properties to our model classes to take advantage of some of the additional information in our database.</span></span>

### <a name="adding-our-store-catalog-data"></a><span data-ttu-id="0803f-142">添加我们的商店目录数据</span><span class="sxs-lookup"><span data-stu-id="0803f-142">Adding our store catalog data</span></span>

<span data-ttu-id="0803f-143">我们将利用实体框架的一项功能，该功能可将 "种子" 数据添加到新创建的数据库中。</span><span class="sxs-lookup"><span data-stu-id="0803f-143">We will take advantage of a feature in Entity Framework which adds "seed" data to a newly created database.</span></span> <span data-ttu-id="0803f-144">这将使用流派、艺术家和专辑列表预填充我们的商店目录。</span><span class="sxs-lookup"><span data-stu-id="0803f-144">This will pre-populate our store catalog with a list of Genres, Artists, and Albums.</span></span> <span data-ttu-id="0803f-145">MvcMusicStore-Assets 下载-其中包含我们在本教程前面部分使用的站点设计文件，其中包含一个带有此种子数据的类文件，位于名为 Code 的文件夹中。</span><span class="sxs-lookup"><span data-stu-id="0803f-145">The MvcMusicStore-Assets.zip download - which included our site design files used earlier in this tutorial - has a class file with this seed data, located in a folder named Code.</span></span>

<span data-ttu-id="0803f-146">在 "代码/模型" 文件夹中，找到 "SampleData.cs" 文件并将其放入项目中的 "模型" 文件夹，如下所示。</span><span class="sxs-lookup"><span data-stu-id="0803f-146">Within the Code / Models folder, locate the SampleData.cs file and drop it into the Models folder in our project, as shown below.</span></span>

![](mvc-music-store-part-4/_static/image4.png)

<span data-ttu-id="0803f-147">现在，我们需要添加一行代码，告诉实体框架此 SampleData 类。</span><span class="sxs-lookup"><span data-stu-id="0803f-147">Now we need to add one line of code to tell Entity Framework about that SampleData class.</span></span> <span data-ttu-id="0803f-148">双击项目根目录中的 Global.asa 文件以将其打开，然后将以下行添加到应用程序\_Start 方法的顶部。</span><span class="sxs-lookup"><span data-stu-id="0803f-148">Double-click on the Global.asax file in the root of the project to open it and add the following line to the top the Application\_Start method.</span></span>

[!code-csharp[Main](mvc-music-store-part-4/samples/sample6.cs)]

<span data-ttu-id="0803f-149">此时，我们已完成为项目配置实体框架所需的工作。</span><span class="sxs-lookup"><span data-stu-id="0803f-149">At this point, we've completed the work necessary to configure Entity Framework for our project.</span></span>

## <a name="querying-the-database"></a><span data-ttu-id="0803f-150">查询数据库</span><span class="sxs-lookup"><span data-stu-id="0803f-150">Querying the Database</span></span>

<span data-ttu-id="0803f-151">现在，让我们更新 StoreController，以便不使用 "虚拟数据" 调用数据库来查询其所有信息。</span><span class="sxs-lookup"><span data-stu-id="0803f-151">Now let's update our StoreController so that instead of using "dummy data" it instead calls into our database to query all of its information.</span></span> <span data-ttu-id="0803f-152">首先，在**StoreController**上声明一个字段，以保存名为 StoreDB 的 MusicStoreEntities 类的实例：</span><span class="sxs-lookup"><span data-stu-id="0803f-152">We'll start by declaring a field on the **StoreController** to hold an instance of the MusicStoreEntities class, named storeDB:</span></span>

[!code-csharp[Main](mvc-music-store-part-4/samples/sample7.cs)]

### <a name="updating-the-store-index-to-query-the-database"></a><span data-ttu-id="0803f-153">更新存储索引以查询数据库</span><span class="sxs-lookup"><span data-stu-id="0803f-153">Updating the Store Index to query the database</span></span>

<span data-ttu-id="0803f-154">MusicStoreEntities 类由实体框架维护，并为数据库中的每个表公开一个集合属性。</span><span class="sxs-lookup"><span data-stu-id="0803f-154">The MusicStoreEntities class is maintained by the Entity Framework and exposes a collection property for each table in our database.</span></span> <span data-ttu-id="0803f-155">让我们更新 StoreController 的索引操作，以检索数据库中的所有流派。</span><span class="sxs-lookup"><span data-stu-id="0803f-155">Let's update our StoreController's Index action to retrieve all Genres in our database.</span></span> <span data-ttu-id="0803f-156">以前，我们通过对字符串数据进行硬编码来完成此操作。</span><span class="sxs-lookup"><span data-stu-id="0803f-156">Previously we did this by hard-coding string data.</span></span> <span data-ttu-id="0803f-157">现在，可以改为仅使用实体框架上下文 Generes 集合：</span><span class="sxs-lookup"><span data-stu-id="0803f-157">Now we can instead just use the Entity Framework context Generes collection:</span></span>

[!code-csharp[Main](mvc-music-store-part-4/samples/sample8.cs)]

<span data-ttu-id="0803f-158">我们的视图模板不需要进行任何更改，因为我们仍将返回以前返回的相同 StoreIndexViewModel-我们现在只从数据库返回实时数据。</span><span class="sxs-lookup"><span data-stu-id="0803f-158">No changes need to happen to our View template since we're still returning the same StoreIndexViewModel we returned before - we're just returning live data from our database now.</span></span>

<span data-ttu-id="0803f-159">当我们再次运行该项目并访问 "/Store" URL 时，我们现在会看到数据库中所有流派的列表：</span><span class="sxs-lookup"><span data-stu-id="0803f-159">When we run the project again and visit the "/Store" URL, we'll now see a list of all Genres in our database:</span></span>

![](mvc-music-store-part-4/_static/image1.jpg)

### <a name="updating-store-browse-and-details-to-use-live-data"></a><span data-ttu-id="0803f-160">更新存储浏览和详细信息以使用实时数据</span><span class="sxs-lookup"><span data-stu-id="0803f-160">Updating Store Browse and Details to use live data</span></span>

<span data-ttu-id="0803f-161">使用/Store/Browse？流派 = *[部分流派]* 操作方法时，我们将按名称搜索流派。</span><span class="sxs-lookup"><span data-stu-id="0803f-161">With the /Store/Browse?genre=*[some-genre]* action method, we're searching for a Genre by name.</span></span> <span data-ttu-id="0803f-162">我们只需要一个结果，因为对于同一流派名称，我们不应该有两个条目，因此，我们可以使用。LINQ 中的 Single （）扩展，用于查询相应的流派对象，如下所示（不要再键入）：</span><span class="sxs-lookup"><span data-stu-id="0803f-162">We only expect one result, since we shouldn't ever have two entries for the same Genre name, and so we can use the .Single() extension in LINQ to query for the appropriate Genre object like this (don't type this yet):</span></span>

[!code-csharp[Main](mvc-music-store-part-4/samples/sample9.cs)]

<span data-ttu-id="0803f-163">单个方法采用 Lambda 表达式作为参数，该参数指定我们想要一个流派对象，使其名称与我们定义的值匹配。</span><span class="sxs-lookup"><span data-stu-id="0803f-163">The Single method takes a Lambda expression as a parameter, which specifies that we want a single Genre object such that its name matches the value we've defined.</span></span> <span data-ttu-id="0803f-164">在上面的示例中，我们将加载一个名称值与 Disco 匹配的单一流派对象。</span><span class="sxs-lookup"><span data-stu-id="0803f-164">In the case above, we are loading a single Genre object with a Name value matching Disco.</span></span>

<span data-ttu-id="0803f-165">我们将利用一项实体框架功能，使我们能够在检索流派对象时，指出我们想要加载的其他相关实体。</span><span class="sxs-lookup"><span data-stu-id="0803f-165">We'll take advantage of an Entity Framework feature that allows us to indicate other related entities we want loaded as well when the Genre object is retrieved.</span></span> <span data-ttu-id="0803f-166">此功能称为查询结果调整，使我们可以减少访问数据库以检索所需的所有信息所需的次数。</span><span class="sxs-lookup"><span data-stu-id="0803f-166">This feature is called Query Result Shaping, and enables us to reduce the number of times we need to access the database to retrieve all of the information we need.</span></span> <span data-ttu-id="0803f-167">我们想要为我们检索的流派预先提取唱集，因此我们将更新查询，使其包括在流派中。包括（"唱片集"）表示我们还需要相关唱片集。</span><span class="sxs-lookup"><span data-stu-id="0803f-167">We want to pre-fetch the Albums for Genre we retrieve, so we'll update our query to include from Genres.Include("Albums") to indicate that we want related albums as well.</span></span> <span data-ttu-id="0803f-168">这会更有效，因为它将在单个数据库请求中检索流派和唱片集数据。</span><span class="sxs-lookup"><span data-stu-id="0803f-168">This is more efficient, since it will retrieve both our Genre and Album data in a single database request.</span></span>

<span data-ttu-id="0803f-169">通过这种说明，我们更新的 "浏览控制器" 操作的外观如下：</span><span class="sxs-lookup"><span data-stu-id="0803f-169">With the explanations out of the way, here's how our updated Browse controller action looks:</span></span>

[!code-csharp[Main](mvc-music-store-part-4/samples/sample10.cs)]

<span data-ttu-id="0803f-170">现在，我们可以更新应用商店浏览视图，以显示每个流派中可用的唱片集。</span><span class="sxs-lookup"><span data-stu-id="0803f-170">We can now update the Store Browse View to display the albums which are available in each Genre.</span></span> <span data-ttu-id="0803f-171">打开视图模板（在/Views/Store/Browse.cshtml 中找到），并按如下所示添加相册的项目符号列表。</span><span class="sxs-lookup"><span data-stu-id="0803f-171">Open the view template (found in /Views/Store/Browse.cshtml) and add a bulleted list of Albums as shown below.</span></span>

[!code-cshtml[Main](mvc-music-store-part-4/samples/sample11.cshtml)]

<span data-ttu-id="0803f-172">运行应用程序并浏览到/Store/Browse？流派 = 爵士乐显示，当前正在从数据库中提取结果，并显示所选流派中的所有唱片集。</span><span class="sxs-lookup"><span data-stu-id="0803f-172">Running our application and browsing to /Store/Browse?genre=Jazz shows that our results are now being pulled from the database, displaying all albums in our selected Genre.</span></span>

![](mvc-music-store-part-4/_static/image2.jpg)

<span data-ttu-id="0803f-173">我们将对/Store/Details/[id] URL 进行相同的更改，并将我们的虚拟数据替换为加载其 ID 与参数值匹配的唱片集的数据库查询。</span><span class="sxs-lookup"><span data-stu-id="0803f-173">We'll make the same change to our /Store/Details/[id] URL, and replace our dummy data with a database query which loads an Album whose ID matches the parameter value.</span></span>

[!code-csharp[Main](mvc-music-store-part-4/samples/sample12.cs)]

<span data-ttu-id="0803f-174">运行应用程序并浏览到/Store/Details/1 表明现在正在从数据库中提取结果。</span><span class="sxs-lookup"><span data-stu-id="0803f-174">Running our application and browsing to /Store/Details/1 shows that our results are now being pulled from the database.</span></span>

![](mvc-music-store-part-4/_static/image5.png)

<span data-ttu-id="0803f-175">现在我们的商店详细信息页已设置为按唱片集 ID 显示唱片集，接下来，我们将**浏览**视图更新为链接到详细信息视图。</span><span class="sxs-lookup"><span data-stu-id="0803f-175">Now that our Store Details page is set up to display an album by the Album ID, let's update the **Browse** view to link to the Details view.</span></span> <span data-ttu-id="0803f-176">我们将使用 Html.actionlink，与从存储索引链接到在上一部分末尾浏览存储的操作完全一样。</span><span class="sxs-lookup"><span data-stu-id="0803f-176">We will use Html.ActionLink, exactly as we did to link from Store Index to Store Browse at the end of the previous section.</span></span> <span data-ttu-id="0803f-177">浏览视图的完整源如下所示。</span><span class="sxs-lookup"><span data-stu-id="0803f-177">The complete source for the Browse view appears below.</span></span>

[!code-cshtml[Main](mvc-music-store-part-4/samples/sample13.cshtml)]

<span data-ttu-id="0803f-178">现在，我们可以从应用商店页浏览到流派页面，其中列出了可用的唱片集，然后单击唱片集查看该唱片集的详细信息。</span><span class="sxs-lookup"><span data-stu-id="0803f-178">We're now able to browse from our Store page to a Genre page, which lists the available albums, and by clicking on an album we can view details for that album.</span></span>

![](mvc-music-store-part-4/_static/image6.png)

> [!div class="step-by-step"]
> <span data-ttu-id="0803f-179">[上一页](mvc-music-store-part-3.md)
> [下一页](mvc-music-store-part-5.md)</span><span class="sxs-lookup"><span data-stu-id="0803f-179">[Previous](mvc-music-store-part-3.md)
[Next](mvc-music-store-part-5.md)</span></span>
