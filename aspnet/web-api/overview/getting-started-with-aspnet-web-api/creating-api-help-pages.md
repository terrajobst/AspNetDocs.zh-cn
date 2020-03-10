---
uid: web-api/overview/getting-started-with-aspnet-web-api/creating-api-help-pages
title: 为 ASP.NET Web API 创建帮助页-ASP.NET 4。x
author: MikeWasson
description: 本教程中的代码演示了如何在 ASP.NET 4.x 中创建 ASP.NET Web API 的帮助页。
ms.author: riande
ms.date: 04/01/2013
ms.custom: seoapril2019
ms.assetid: 0150e67b-c50d-4613-83ea-7b4ef8cacc5a
msc.legacyurl: /web-api/overview/getting-started-with-aspnet-web-api/creating-api-help-pages
msc.type: authoredcontent
ms.openlocfilehash: 8308dab8bd66aa8f5a3c5fb4133fc7a3df78f671
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78448616"
---
# <a name="creating-help-pages-for-aspnet-web-api"></a><span data-ttu-id="eab93-103">为 ASP.NET Web API 创建帮助页</span><span class="sxs-lookup"><span data-stu-id="eab93-103">Creating Help Pages for ASP.NET Web API</span></span>

<span data-ttu-id="eab93-104">作者： [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="eab93-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="eab93-105">本教程中的代码演示了如何在 ASP.NET 4.x 中创建 ASP.NET Web API 的帮助页。</span><span class="sxs-lookup"><span data-stu-id="eab93-105">This tutorial with code shows how to create help pages for ASP.NET Web API in ASP.NET 4.x.</span></span>

<span data-ttu-id="eab93-106">创建 web API 时，创建帮助页通常很有用，因为其他开发人员将知道如何调用 API。</span><span class="sxs-lookup"><span data-stu-id="eab93-106">When you create a web API, it is often useful to create a help page, so that other developers will know how to call your API.</span></span> <span data-ttu-id="eab93-107">您可以手动创建所有文档，但最好尽可能地自动生成。</span><span class="sxs-lookup"><span data-stu-id="eab93-107">You could create all of the documentation manually, but it is better to autogenerate as much as possible.</span></span> <span data-ttu-id="eab93-108">为了更轻松地执行此任务，ASP.NET Web API 提供了一个库，用于在运行时自动生成帮助页面。</span><span class="sxs-lookup"><span data-stu-id="eab93-108">To make this task easier, ASP.NET Web API provides a library for auto-generating help pages at run time.</span></span>

![](creating-api-help-pages/_static/image1.png)

## <a name="creating-api-help-pages"></a><span data-ttu-id="eab93-109">创建 API 帮助页</span><span class="sxs-lookup"><span data-stu-id="eab93-109">Creating API Help Pages</span></span>

<span data-ttu-id="eab93-110">安装[ASP.NET 和 Web 工具2012.2 更新](https://go.microsoft.com/fwlink/?LinkId=282650)。</span><span class="sxs-lookup"><span data-stu-id="eab93-110">Install [ASP.NET and Web Tools 2012.2 Update](https://go.microsoft.com/fwlink/?LinkId=282650).</span></span> <span data-ttu-id="eab93-111">此更新将帮助页集成到 Web API 项目模板中。</span><span class="sxs-lookup"><span data-stu-id="eab93-111">This update integrates help pages into the Web API project template.</span></span>

<span data-ttu-id="eab93-112">接下来，创建新的 ASP.NET MVC 4 项目，并选择 "Web API" 项目模板。</span><span class="sxs-lookup"><span data-stu-id="eab93-112">Next, create a new ASP.NET MVC 4 project and select the Web API project template.</span></span> <span data-ttu-id="eab93-113">项目模板创建一个名为 `ValuesController`的示例 API 控制器。</span><span class="sxs-lookup"><span data-stu-id="eab93-113">The project template creates an example API controller named `ValuesController`.</span></span> <span data-ttu-id="eab93-114">该模板还会创建 API 帮助页。</span><span class="sxs-lookup"><span data-stu-id="eab93-114">The template also creates the API help pages.</span></span> <span data-ttu-id="eab93-115">"帮助" 页的所有代码文件都放置在项目的 "区域" 文件夹中。</span><span class="sxs-lookup"><span data-stu-id="eab93-115">All of the code files for the help page are placed in the Areas folder of the project.</span></span>

![](creating-api-help-pages/_static/image2.png)

<span data-ttu-id="eab93-116">运行应用程序时，主页包含指向 API 帮助页的链接。</span><span class="sxs-lookup"><span data-stu-id="eab93-116">When you run the application, the home page contains a link to the API help page.</span></span> <span data-ttu-id="eab93-117">从主页中，相对路径为/Help。</span><span class="sxs-lookup"><span data-stu-id="eab93-117">From the home page, the relative path is /Help.</span></span>

![](creating-api-help-pages/_static/image3.png)

<span data-ttu-id="eab93-118">此链接会将你带到 API 摘要页。</span><span class="sxs-lookup"><span data-stu-id="eab93-118">This link brings you to an API summary page.</span></span>

![](creating-api-help-pages/_static/image4.png)

<span data-ttu-id="eab93-119">此页的 MVC 视图在区域/HelpPage/Views/Help/Index 中定义。</span><span class="sxs-lookup"><span data-stu-id="eab93-119">The MVC view for this page is defined in Areas/HelpPage/Views/Help/Index.cshtml.</span></span> <span data-ttu-id="eab93-120">您可以编辑此页以修改布局、简介、标题、样式等。</span><span class="sxs-lookup"><span data-stu-id="eab93-120">You can edit this page to modify the layout, introduction, title, styles, and so forth.</span></span>

<span data-ttu-id="eab93-121">页面的主要部分是 Api 表，按控制器分组。</span><span class="sxs-lookup"><span data-stu-id="eab93-121">The main part of the page is a table of APIs, grouped by controller.</span></span> <span data-ttu-id="eab93-122">表项是使用**IApiExplorer**接口动态生成的。</span><span class="sxs-lookup"><span data-stu-id="eab93-122">The table entries are generated dynamically, using the **IApiExplorer** interface.</span></span> <span data-ttu-id="eab93-123">（稍后我将详细讨论此接口。）如果添加新的 API 控制器，则表会在运行时自动更新。</span><span class="sxs-lookup"><span data-stu-id="eab93-123">(I'll talk more about this interface later.) If you add a new API controller, the table is automatically updated at run time.</span></span>

<span data-ttu-id="eab93-124">"API" 列列出了 HTTP 方法和相对 URI。</span><span class="sxs-lookup"><span data-stu-id="eab93-124">The "API" column lists the HTTP method and relative URI.</span></span> <span data-ttu-id="eab93-125">"说明" 列包含每个 API 的文档。</span><span class="sxs-lookup"><span data-stu-id="eab93-125">The "Description" column contains documentation for each API.</span></span> <span data-ttu-id="eab93-126">最初，文档只是占位符文本。</span><span class="sxs-lookup"><span data-stu-id="eab93-126">Initially, the documentation is just placeholder text.</span></span> <span data-ttu-id="eab93-127">在下一部分中，我将向您演示如何从 XML 注释添加文档。</span><span class="sxs-lookup"><span data-stu-id="eab93-127">In the next section, I'll show you how to add documentation from XML comments.</span></span>

<span data-ttu-id="eab93-128">每个 API 都具有指向包含更详细信息的页面的链接，包括示例请求和响应正文。</span><span class="sxs-lookup"><span data-stu-id="eab93-128">Each API has a link to a page with more detailed information, including example request and response bodies.</span></span>

![](creating-api-help-pages/_static/image5.png)

## <a name="adding-help-pages-to-an-existing-project"></a><span data-ttu-id="eab93-129">向现有项目添加帮助页</span><span class="sxs-lookup"><span data-stu-id="eab93-129">Adding Help Pages to an Existing Project</span></span>

<span data-ttu-id="eab93-130">可以使用 NuGet 包管理器将帮助页添加到现有 Web API 项目。</span><span class="sxs-lookup"><span data-stu-id="eab93-130">You can add help pages to an existing Web API project by using NuGet Package Manager.</span></span> <span data-ttu-id="eab93-131">从与 "Web API" 模板不同的项目模板开始，此选项很有用。</span><span class="sxs-lookup"><span data-stu-id="eab93-131">This option is useful you start from a different project template than the "Web API" template.</span></span>

<span data-ttu-id="eab93-132">从 "**工具**" 菜单中，选择 " **NuGet 包管理器**"，然后选择 "**程序包管理器控制台**"。</span><span class="sxs-lookup"><span data-stu-id="eab93-132">From the **Tools** menu, select **NuGet Package Manager**, and then select **Package Manager Console**.</span></span> <span data-ttu-id="eab93-133">在 "[包管理器控制台](http://docs.nuget.org/docs/start-here/using-the-package-manager-console)" 窗口中，键入以下命令之一：</span><span class="sxs-lookup"><span data-stu-id="eab93-133">In the [Package Manager Console](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) window, type one of the following commands:</span></span>

<span data-ttu-id="eab93-134">对于**C#** 应用程序： `Install-Package Microsoft.AspNet.WebApi.HelpPage`</span><span class="sxs-lookup"><span data-stu-id="eab93-134">For a **C#** application: `Install-Package Microsoft.AspNet.WebApi.HelpPage`</span></span>

<span data-ttu-id="eab93-135">对于**Visual Basic**应用程序： `Install-Package Microsoft.AspNet.WebApi.HelpPage.VB`</span><span class="sxs-lookup"><span data-stu-id="eab93-135">For a **Visual Basic** application: `Install-Package Microsoft.AspNet.WebApi.HelpPage.VB`</span></span>

<span data-ttu-id="eab93-136">有两个包，一个用于C# ，一个用于 Visual Basic。</span><span class="sxs-lookup"><span data-stu-id="eab93-136">There are two packages, one for C# and one for Visual Basic.</span></span> <span data-ttu-id="eab93-137">请确保使用与你的项目匹配的项目。</span><span class="sxs-lookup"><span data-stu-id="eab93-137">Make sure to use the one that matches your project.</span></span>

<span data-ttu-id="eab93-138">此命令将安装所需的程序集，并添加帮助页（位于 Areas/HelpPage 文件夹中）的 MVC 视图。</span><span class="sxs-lookup"><span data-stu-id="eab93-138">This command installs the necessary assemblies and adds the MVC views for the help pages (located in the Areas/HelpPage folder).</span></span> <span data-ttu-id="eab93-139">您需要手动添加指向 "帮助" 页的链接。</span><span class="sxs-lookup"><span data-stu-id="eab93-139">You'll need to manually add a link to the Help page.</span></span> <span data-ttu-id="eab93-140">URI 为/Help。</span><span class="sxs-lookup"><span data-stu-id="eab93-140">The URI is /Help.</span></span> <span data-ttu-id="eab93-141">若要在 razor 视图中创建链接，请添加以下内容：</span><span class="sxs-lookup"><span data-stu-id="eab93-141">To create a link in a razor view, add the following:</span></span>

[!code-cshtml[Main](creating-api-help-pages/samples/sample1.cshtml)]

<span data-ttu-id="eab93-142">此外，请确保注册区域。</span><span class="sxs-lookup"><span data-stu-id="eab93-142">Also, make sure to register areas.</span></span> <span data-ttu-id="eab93-143">在 global.asax 文件中，将以下代码添加到**应用程序\_Start**方法（如果尚未这样做）：</span><span class="sxs-lookup"><span data-stu-id="eab93-143">In the Global.asax file, add the following code to the **Application\_Start** method, if it is not there already:</span></span>

[!code-csharp[Main](creating-api-help-pages/samples/sample2.cs?highlight=4)]

## <a name="adding-api-documentation"></a><span data-ttu-id="eab93-144">添加 API 文档</span><span class="sxs-lookup"><span data-stu-id="eab93-144">Adding API Documentation</span></span>

<span data-ttu-id="eab93-145">默认情况下，帮助页包含文档的占位符字符串。</span><span class="sxs-lookup"><span data-stu-id="eab93-145">By default, the help pages have placeholder strings for documentation.</span></span> <span data-ttu-id="eab93-146">您可以使用[XML 文档注释](https://msdn.microsoft.com/library/b2s063f7.aspx)来创建文档。</span><span class="sxs-lookup"><span data-stu-id="eab93-146">You can use [XML documentation comments](https://msdn.microsoft.com/library/b2s063f7.aspx) to create the documentation.</span></span> <span data-ttu-id="eab93-147">若要启用此功能，请打开文件区域/HelpPage/应用\_Start/HelpPageConfig，并取消注释以下行：</span><span class="sxs-lookup"><span data-stu-id="eab93-147">To enable this feature, open the file Areas/HelpPage/App\_Start/HelpPageConfig.cs and uncomment the following line:</span></span>

[!code-csharp[Main](creating-api-help-pages/samples/sample3.cs)]

<span data-ttu-id="eab93-148">现在启用 XML 文档。</span><span class="sxs-lookup"><span data-stu-id="eab93-148">Now enable XML documentation.</span></span> <span data-ttu-id="eab93-149">在解决方案资源管理器中，右键单击项目，然后选择 "**属性**"。</span><span class="sxs-lookup"><span data-stu-id="eab93-149">In Solution Explorer, right-click the project and select **Properties**.</span></span> <span data-ttu-id="eab93-150">选择 "**生成**" 页。</span><span class="sxs-lookup"><span data-stu-id="eab93-150">Select the **Build** page.</span></span>

![](creating-api-help-pages/_static/image6.png)

<span data-ttu-id="eab93-151">在 "**输出**" 下，检查**XML 文档文件**。</span><span class="sxs-lookup"><span data-stu-id="eab93-151">Under **Output**, check **XML documentation file**.</span></span> <span data-ttu-id="eab93-152">在编辑框中，键入 "App\_Data/xml"。</span><span class="sxs-lookup"><span data-stu-id="eab93-152">In the edit box, type "App\_Data/XmlDocument.xml".</span></span>

![](creating-api-help-pages/_static/image7.png)

<span data-ttu-id="eab93-153">接下来，打开/Controllers/ValuesController.cs. 中定义的 `ValuesController` API 控制器的代码。</span><span class="sxs-lookup"><span data-stu-id="eab93-153">Next, open the code for the `ValuesController` API controller, which is defined in /Controllers/ValuesController.cs.</span></span> <span data-ttu-id="eab93-154">向控制器方法添加一些文档注释。</span><span class="sxs-lookup"><span data-stu-id="eab93-154">Add some documentation comments to the controller methods.</span></span> <span data-ttu-id="eab93-155">例如:</span><span class="sxs-lookup"><span data-stu-id="eab93-155">For example:</span></span>

[!code-csharp[Main](creating-api-help-pages/samples/sample4.cs)]

> [!NOTE]
> <span data-ttu-id="eab93-156">提示：如果将插入符号放置在方法上面的行上，并键入三个正斜杠，则 Visual Studio 将自动插入 XML 元素。</span><span class="sxs-lookup"><span data-stu-id="eab93-156">Tip: If you position the caret on the line above the method and type three forward slashes, Visual Studio automatically inserts the XML elements.</span></span> <span data-ttu-id="eab93-157">然后，可以填写空白。</span><span class="sxs-lookup"><span data-stu-id="eab93-157">Then you can fill in the blanks.</span></span>

<span data-ttu-id="eab93-158">现在，重新生成并运行应用程序，然后导航到帮助页。</span><span class="sxs-lookup"><span data-stu-id="eab93-158">Now build and run the application again, and navigate to the help pages.</span></span> <span data-ttu-id="eab93-159">文档字符串应显示在 API 表中。</span><span class="sxs-lookup"><span data-stu-id="eab93-159">The documentation strings should appear in the API table.</span></span>

![](creating-api-help-pages/_static/image8.png)

<span data-ttu-id="eab93-160">"帮助" 页在运行时读取 XML 文件中的字符串。</span><span class="sxs-lookup"><span data-stu-id="eab93-160">The help page reads the strings from the XML file at run time.</span></span> <span data-ttu-id="eab93-161">（部署应用程序时，请确保部署该 XML 文件。）</span><span class="sxs-lookup"><span data-stu-id="eab93-161">(When you deploy the application, make sure to deploy the XML file.)</span></span>

## <a name="under-the-hood"></a><span data-ttu-id="eab93-162">在后台</span><span class="sxs-lookup"><span data-stu-id="eab93-162">Under the Hood</span></span>

<span data-ttu-id="eab93-163">帮助页构建在**ApiExplorer**类之上，该类是 Web API 框架的一部分。</span><span class="sxs-lookup"><span data-stu-id="eab93-163">The help pages are built on top of the **ApiExplorer** class, which is part of the Web API framework.</span></span> <span data-ttu-id="eab93-164">**ApiExplorer**类提供创建帮助页的原始材料。</span><span class="sxs-lookup"><span data-stu-id="eab93-164">The **ApiExplorer** class provides the raw material for creating a help page.</span></span> <span data-ttu-id="eab93-165">对于每个 API， **ApiExplorer**包含描述 API 的**ApiDescription** 。</span><span class="sxs-lookup"><span data-stu-id="eab93-165">For each API, **ApiExplorer** contains an **ApiDescription** that describes the API.</span></span> <span data-ttu-id="eab93-166">为此，"API" 定义为 HTTP 方法和相对 URI 的组合。</span><span class="sxs-lookup"><span data-stu-id="eab93-166">For this purpose, an "API" is defined as the combination of HTTP method and relative URI.</span></span> <span data-ttu-id="eab93-167">例如，下面是一些不同的 Api：</span><span class="sxs-lookup"><span data-stu-id="eab93-167">For example, here are some distinct APIs:</span></span>

- <span data-ttu-id="eab93-168">获取/api/Products</span><span class="sxs-lookup"><span data-stu-id="eab93-168">GET /api/Products</span></span>
- <span data-ttu-id="eab93-169">获取/api/Products/{id}</span><span class="sxs-lookup"><span data-stu-id="eab93-169">GET /api/Products/{id}</span></span>
- <span data-ttu-id="eab93-170">POST/api/Products</span><span class="sxs-lookup"><span data-stu-id="eab93-170">POST /api/Products</span></span>

<span data-ttu-id="eab93-171">如果控制器操作支持多个 HTTP 方法，则**ApiExplorer**会将每个方法视为不同的 API。</span><span class="sxs-lookup"><span data-stu-id="eab93-171">If a controller action supports multiple HTTP methods, the **ApiExplorer** treats each method as a distinct API.</span></span>

<span data-ttu-id="eab93-172">若要从**ApiExplorer**中隐藏 API，请将**ApiExplorerSettings**属性添加到操作，并将*IgnoreApi*设置为 true。</span><span class="sxs-lookup"><span data-stu-id="eab93-172">To hide an API from the **ApiExplorer**, add the **ApiExplorerSettings** attribute to the action and set *IgnoreApi* to true.</span></span>

[!code-csharp[Main](creating-api-help-pages/samples/sample5.cs)]

<span data-ttu-id="eab93-173">你还可以将此属性添加到控制器，以排除整个控制器。</span><span class="sxs-lookup"><span data-stu-id="eab93-173">You can also add this attribute to the controller, to exclude the entire controller.</span></span>

<span data-ttu-id="eab93-174">ApiExplorer 类从**IDocumentationProvider**接口获取文档字符串。</span><span class="sxs-lookup"><span data-stu-id="eab93-174">The ApiExplorer class gets documentation strings from the **IDocumentationProvider** interface.</span></span> <span data-ttu-id="eab93-175">如前文所述，帮助页库提供了从 XML 文档字符串获取文档的**IDocumentationProvider** 。</span><span class="sxs-lookup"><span data-stu-id="eab93-175">As you saw earlier, the Help Pages library provides an **IDocumentationProvider** that gets documentation from XML documentation strings.</span></span> <span data-ttu-id="eab93-176">代码位于/Areas/HelpPage/XmlDocumentationProvider.cs. 中。</span><span class="sxs-lookup"><span data-stu-id="eab93-176">The code is located in /Areas/HelpPage/XmlDocumentationProvider.cs.</span></span> <span data-ttu-id="eab93-177">可以通过编写自己的**IDocumentationProvider**从其他源获取文档。</span><span class="sxs-lookup"><span data-stu-id="eab93-177">You can get documentation from another source by writing your own **IDocumentationProvider**.</span></span> <span data-ttu-id="eab93-178">若要将其连接起来，请调用**SetDocumentationProvider**扩展方法，该方法在**HelpPageConfigurationExtensions**中定义。</span><span class="sxs-lookup"><span data-stu-id="eab93-178">To wire it up, call the **SetDocumentationProvider** extension method, defined in **HelpPageConfigurationExtensions**</span></span>

<span data-ttu-id="eab93-179">**ApiExplorer**自动调入**IDocumentationProvider**接口，以获取每个 API 的文档字符串。</span><span class="sxs-lookup"><span data-stu-id="eab93-179">**ApiExplorer** automatically calls into the **IDocumentationProvider** interface to get documentation strings for each API.</span></span> <span data-ttu-id="eab93-180">它将它们存储在**ApiDescription**和**ApiParameterDescription**对象的**文档**属性中。</span><span class="sxs-lookup"><span data-stu-id="eab93-180">It stores them in the **Documentation** property of the **ApiDescription** and **ApiParameterDescription** objects.</span></span>

## <a name="next-steps"></a><span data-ttu-id="eab93-181">后续步骤</span><span class="sxs-lookup"><span data-stu-id="eab93-181">Next Steps</span></span>

<span data-ttu-id="eab93-182">你并不局限于此处显示的帮助页。</span><span class="sxs-lookup"><span data-stu-id="eab93-182">You aren't limited to the help pages shown here.</span></span> <span data-ttu-id="eab93-183">事实上， **ApiExplorer**并不局限于创建帮助页。</span><span class="sxs-lookup"><span data-stu-id="eab93-183">In fact, **ApiExplorer** is not limited to creating help pages.</span></span> <span data-ttu-id="eab93-184">Yao Huang 链接编写了一些精彩的博客文章，让你考虑一下你的想法：</span><span class="sxs-lookup"><span data-stu-id="eab93-184">Yao Huang Lin has written some great blog posts to get you thinking out of the box:</span></span>

- [<span data-ttu-id="eab93-185">将简单的测试客户端添加到 ASP.NET Web API 帮助页</span><span class="sxs-lookup"><span data-stu-id="eab93-185">Adding a simple Test Client to ASP.NET Web API Help Page</span></span>](https://blogs.msdn.com/b/yaohuang1/archive/2012/12/02/adding-a-simple-test-client-to-asp-net-web-api-help-page.aspx)
- [<span data-ttu-id="eab93-186">使 ASP.NET Web API 帮助页在自承载服务上工作</span><span class="sxs-lookup"><span data-stu-id="eab93-186">Making ASP.NET Web API Help Page work on self-hosted services</span></span>](https://blogs.msdn.com/b/yaohuang1/archive/2012/12/20/making-asp-net-web-api-help-page-work-on-self-hosted-services.aspx)
- [<span data-ttu-id="eab93-187">ASP.NET Web API 的设计时生成帮助页（或客户端）</span><span class="sxs-lookup"><span data-stu-id="eab93-187">Design-time generation of help page (or client) for ASP.NET Web API</span></span>](https://blogs.msdn.com/b/yaohuang1/archive/2013/01/20/design-time-generation-of-help-page-or-proxy-for-asp-net-web-api.aspx)
- [<span data-ttu-id="eab93-188">高级帮助页自定义</span><span class="sxs-lookup"><span data-stu-id="eab93-188">Advanced Help Page customizations</span></span>](https://blogs.msdn.com/b/yaohuang1/archive/2012/12/10/asp-net-web-api-help-page-part-3-advanced-help-page-customizations.aspx)
