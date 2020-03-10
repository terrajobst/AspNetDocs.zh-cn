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
# <a name="creating-help-pages-for-aspnet-web-api"></a>为 ASP.NET Web API 创建帮助页

作者： [Mike Wasson](https://github.com/MikeWasson)

本教程中的代码演示了如何在 ASP.NET 4.x 中创建 ASP.NET Web API 的帮助页。

创建 web API 时，创建帮助页通常很有用，因为其他开发人员将知道如何调用 API。 您可以手动创建所有文档，但最好尽可能地自动生成。 为了更轻松地执行此任务，ASP.NET Web API 提供了一个库，用于在运行时自动生成帮助页面。

![](creating-api-help-pages/_static/image1.png)

## <a name="creating-api-help-pages"></a>创建 API 帮助页

安装[ASP.NET 和 Web 工具2012.2 更新](https://go.microsoft.com/fwlink/?LinkId=282650)。 此更新将帮助页集成到 Web API 项目模板中。

接下来，创建新的 ASP.NET MVC 4 项目，并选择 "Web API" 项目模板。 项目模板创建一个名为 `ValuesController`的示例 API 控制器。 该模板还会创建 API 帮助页。 "帮助" 页的所有代码文件都放置在项目的 "区域" 文件夹中。

![](creating-api-help-pages/_static/image2.png)

运行应用程序时，主页包含指向 API 帮助页的链接。 从主页中，相对路径为/Help。

![](creating-api-help-pages/_static/image3.png)

此链接会将你带到 API 摘要页。

![](creating-api-help-pages/_static/image4.png)

此页的 MVC 视图在区域/HelpPage/Views/Help/Index 中定义。 您可以编辑此页以修改布局、简介、标题、样式等。

页面的主要部分是 Api 表，按控制器分组。 表项是使用**IApiExplorer**接口动态生成的。 （稍后我将详细讨论此接口。）如果添加新的 API 控制器，则表会在运行时自动更新。

"API" 列列出了 HTTP 方法和相对 URI。 "说明" 列包含每个 API 的文档。 最初，文档只是占位符文本。 在下一部分中，我将向您演示如何从 XML 注释添加文档。

每个 API 都具有指向包含更详细信息的页面的链接，包括示例请求和响应正文。

![](creating-api-help-pages/_static/image5.png)

## <a name="adding-help-pages-to-an-existing-project"></a>向现有项目添加帮助页

可以使用 NuGet 包管理器将帮助页添加到现有 Web API 项目。 从与 "Web API" 模板不同的项目模板开始，此选项很有用。

从 "**工具**" 菜单中，选择 " **NuGet 包管理器**"，然后选择 "**程序包管理器控制台**"。 在 "[包管理器控制台](http://docs.nuget.org/docs/start-here/using-the-package-manager-console)" 窗口中，键入以下命令之一：

对于**C#** 应用程序： `Install-Package Microsoft.AspNet.WebApi.HelpPage`

对于**Visual Basic**应用程序： `Install-Package Microsoft.AspNet.WebApi.HelpPage.VB`

有两个包，一个用于C# ，一个用于 Visual Basic。 请确保使用与你的项目匹配的项目。

此命令将安装所需的程序集，并添加帮助页（位于 Areas/HelpPage 文件夹中）的 MVC 视图。 您需要手动添加指向 "帮助" 页的链接。 URI 为/Help。 若要在 razor 视图中创建链接，请添加以下内容：

[!code-cshtml[Main](creating-api-help-pages/samples/sample1.cshtml)]

此外，请确保注册区域。 在 global.asax 文件中，将以下代码添加到**应用程序\_Start**方法（如果尚未这样做）：

[!code-csharp[Main](creating-api-help-pages/samples/sample2.cs?highlight=4)]

## <a name="adding-api-documentation"></a>添加 API 文档

默认情况下，帮助页包含文档的占位符字符串。 您可以使用[XML 文档注释](https://msdn.microsoft.com/library/b2s063f7.aspx)来创建文档。 若要启用此功能，请打开文件区域/HelpPage/应用\_Start/HelpPageConfig，并取消注释以下行：

[!code-csharp[Main](creating-api-help-pages/samples/sample3.cs)]

现在启用 XML 文档。 在解决方案资源管理器中，右键单击项目，然后选择 "**属性**"。 选择 "**生成**" 页。

![](creating-api-help-pages/_static/image6.png)

在 "**输出**" 下，检查**XML 文档文件**。 在编辑框中，键入 "App\_Data/xml"。

![](creating-api-help-pages/_static/image7.png)

接下来，打开/Controllers/ValuesController.cs. 中定义的 `ValuesController` API 控制器的代码。 向控制器方法添加一些文档注释。 例如:

[!code-csharp[Main](creating-api-help-pages/samples/sample4.cs)]

> [!NOTE]
> 提示：如果将插入符号放置在方法上面的行上，并键入三个正斜杠，则 Visual Studio 将自动插入 XML 元素。 然后，可以填写空白。

现在，重新生成并运行应用程序，然后导航到帮助页。 文档字符串应显示在 API 表中。

![](creating-api-help-pages/_static/image8.png)

"帮助" 页在运行时读取 XML 文件中的字符串。 （部署应用程序时，请确保部署该 XML 文件。）

## <a name="under-the-hood"></a>在后台

帮助页构建在**ApiExplorer**类之上，该类是 Web API 框架的一部分。 **ApiExplorer**类提供创建帮助页的原始材料。 对于每个 API， **ApiExplorer**包含描述 API 的**ApiDescription** 。 为此，"API" 定义为 HTTP 方法和相对 URI 的组合。 例如，下面是一些不同的 Api：

- 获取/api/Products
- 获取/api/Products/{id}
- POST/api/Products

如果控制器操作支持多个 HTTP 方法，则**ApiExplorer**会将每个方法视为不同的 API。

若要从**ApiExplorer**中隐藏 API，请将**ApiExplorerSettings**属性添加到操作，并将*IgnoreApi*设置为 true。

[!code-csharp[Main](creating-api-help-pages/samples/sample5.cs)]

你还可以将此属性添加到控制器，以排除整个控制器。

ApiExplorer 类从**IDocumentationProvider**接口获取文档字符串。 如前文所述，帮助页库提供了从 XML 文档字符串获取文档的**IDocumentationProvider** 。 代码位于/Areas/HelpPage/XmlDocumentationProvider.cs. 中。 可以通过编写自己的**IDocumentationProvider**从其他源获取文档。 若要将其连接起来，请调用**SetDocumentationProvider**扩展方法，该方法在**HelpPageConfigurationExtensions**中定义。

**ApiExplorer**自动调入**IDocumentationProvider**接口，以获取每个 API 的文档字符串。 它将它们存储在**ApiDescription**和**ApiParameterDescription**对象的**文档**属性中。

## <a name="next-steps"></a>后续步骤

你并不局限于此处显示的帮助页。 事实上， **ApiExplorer**并不局限于创建帮助页。 Yao Huang 链接编写了一些精彩的博客文章，让你考虑一下你的想法：

- [将简单的测试客户端添加到 ASP.NET Web API 帮助页](https://blogs.msdn.com/b/yaohuang1/archive/2012/12/02/adding-a-simple-test-client-to-asp-net-web-api-help-page.aspx)
- [使 ASP.NET Web API 帮助页在自承载服务上工作](https://blogs.msdn.com/b/yaohuang1/archive/2012/12/20/making-asp-net-web-api-help-page-work-on-self-hosted-services.aspx)
- [ASP.NET Web API 的设计时生成帮助页（或客户端）](https://blogs.msdn.com/b/yaohuang1/archive/2013/01/20/design-time-generation-of-help-page-or-proxy-for-asp-net-web-api.aspx)
- [高级帮助页自定义](https://blogs.msdn.com/b/yaohuang1/archive/2012/12/10/asp-net-web-api-help-page-part-3-advanced-help-page-customizations.aspx)
