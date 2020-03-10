---
uid: mvc/overview/older-versions-1/deployment/using-asp-net-mvc-with-different-versions-of-iis-vb
title: 将 ASP.NET MVC 用于不同版本的 IIS （VB） |Microsoft Docs
author: microsoft
description: 在本教程中，将了解如何使用 Internet Information Services 的不同版本的 ASP.NET MVC 和 URL 路由。 了解不同的策略 。
ms.author: riande
ms.date: 08/19/2008
ms.assetid: 1c1283b2-6956-4937-b568-d30de432ce23
msc.legacyurl: /mvc/overview/older-versions-1/deployment/using-asp-net-mvc-with-different-versions-of-iis-vb
msc.type: authoredcontent
ms.openlocfilehash: b754175c853c20eec6be3521376b62d62f33106d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78470012"
---
# <a name="using-aspnet-mvc-with-different-versions-of-iis-vb"></a>通过不同版本的 IIS 使用 ASP.NET MVC (VB)

由[Microsoft](https://github.com/microsoft)

> 在本教程中，将了解如何使用 Internet Information Services 的不同版本的 ASP.NET MVC 和 URL 路由。 你将了解将 ASP.NET MVC 与 IIS 7.0 （经典模式）、IIS 6.0 和 iis 的早期版本结合使用的不同策略。

ASP.NET MVC 框架依赖于 ASP.NET 路由，将浏览器请求路由到控制器操作。 为了充分利用 ASP.NET 路由，你可能需要在 web 服务器上执行其他配置步骤。 这一切都取决于应用程序的 Internet Information Services （IIS）和请求处理模式的版本。

下面是不同版本的 IIS 的摘要：

- IIS 7.0 （集成模式）-使用 ASP.NET 路由无需特殊配置。
- IIS 7.0 （经典模式）-需要执行特殊配置才能使用 ASP.NET 路由。
- IIS 6.0 或更低-需要执行特殊配置才能使用 ASP.NET 路由。

最新版本的 IIS 为版本7.5 （在 Win7 上）。 Iis 7 的 IIS 包含在 Windows Server 2008 和 VISTA/SP1 及更高版本中。 你还可以在任何版本的 Vista 操作系统（Home Basic 除外）上安装 IIS 7.0 （请参阅[https://technet.microsoft.com/library/cc731179%28WS.10%29.aspx](https://technet.microsoft.com/library/cc731179%28WS.10%29.aspx)）。

IIS 7.0 支持两种模式来处理请求。 您可以使用集成模式或经典模式。 在集成模式下使用 IIS 7.0 时，无需执行任何特殊的配置步骤。 但是，在经典模式下使用 IIS 7.0 时，需要执行其他配置。

Microsoft Windows Server 2003 包括 IIS 6.0。 使用 Windows Server 2003 操作系统时，不能将 IIS 6.0 升级到 IIS 7.0。 使用 IIS 6.0 时，必须执行其他配置步骤。

Microsoft Windows XP Professional 包括 IIS 5.1。 使用 IIS 5.1 时，必须执行其他配置步骤。

最后，Microsoft Windows 2000 和 Microsoft Windows 2000 Professional 包括 IIS 5.0。 使用 IIS 5.0 时，必须执行其他配置步骤。

## <a name="integrated-versus-classic-mode"></a>集成模式与经典模式

IIS 7.0 可以使用两种不同的请求处理模式来处理请求：集成和经典。 集成模式提供更好的性能和更多功能。 包含经典模式是为了与 IIS 的早期版本向后兼容。

请求处理模式取决于应用程序池。 通过确定与应用程序关联的应用程序池，你可以确定特定的 web 应用程序所使用的处理模式。 请执行这些步骤：

1. 启动 Internet Information Services 管理器
2. 在 "连接" 窗口中，选择一个应用程序
3. 在 "操作" 窗口中，单击 "**基本设置**" 链接以打开 "编辑应用程序" 对话框（请参阅图1）
4. 记下所选的应用程序池。

默认情况下，IIS 配置为支持两个应用程序池： **DefaultAppPool**和**经典 .net AppPool**。 如果选择了 "DefaultAppPool"，则你的应用程序将在集成请求处理模式下运行。 如果选择了经典 .NET AppPool，你的应用程序将在经典请求处理模式下运行。

[!["新建项目" 对话框](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image1.jpg)](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image1.png)

**图 1**：检测请求处理模式（[单击以查看完全大小的映像](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image2.png)）

请注意，你可以在 "编辑应用程序" 对话框中修改 "请求处理" 模式。 单击 "选择" 按钮并更改与应用程序关联的应用程序池。 请注意，将 ASP.NET 应用程序从经典模式更改为集成模式时存在兼容性问题。 有关详细信息，请参阅以下文章：

- 在 Windows Vista 和 Windows Server 2008 上将 ASP.NET 1.1 升级到 IIS 7.0-- [https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/upgrading-aspnet-11-to-iis-on-windows-vista-and-windows-server-2008](https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/upgrading-aspnet-11-to-iis-on-windows-vista-and-windows-server-2008)

- 与 IIS 7.0 的 ASP.NET 集成- [https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/aspnet-integration-with-iis](https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/aspnet-integration-with-iis)

如果 ASP.NET 应用程序使用的是 DefaultAppPool，则无需执行任何附加步骤即可获得 ASP.NET 路由（因而 ASP.NET MVC）才能正常工作。 但是，如果将 ASP.NET 应用程序配置为使用经典 .NET AppPool，然后继续阅读，则有更多工作要做。

## <a name="using-aspnet-mvc-with-older-versions-of-iis"></a>将 ASP.NET MVC 与较旧版本的 IIS 一起使用

如果需要使用比 IIS 7.0 更早版本的 ASP.NET MVC，或者需要在经典模式下使用 IIS 7.0，则有两个选择。 首先，可以修改路由表以使用文件扩展名。 例如，你应该请求 URL （如/Store/Details），而不是请求 URL （如/Store.aspx/Details.）。

第二种方法是创建一个名为*通配符脚本映射*的内容。 使用通配符脚本映射，可以将每个请求映射到 ASP.NET 框架。

如果你无法访问你的 web 服务器（例如，你的 ASP.NET MVC 应用程序由 Internet 服务提供商托管），则需要使用第一个选项。 如果你不想修改 Url 的外观，并且可以访问你的 web 服务器，则可以使用第二个选项。

我们将在以下各节中详细探讨每个选项。

## <a name="adding-extensions-to-the-route-table"></a>向路由表添加扩展

若要使 ASP.NET 路由与较旧版本的 IIS 一起使用，最简单的方法是修改 global.asax 文件中的路由表。 列表1中的默认和未修改的 Global.asa 文件配置一个名为默认路由的路由。

**列表 1-global.asax （未修改）**

[!code-vb[Main](using-asp-net-mvc-with-different-versions-of-iis-vb/samples/sample1.vb)]

通过在列表1中配置的默认路由，你可以路由如下所示的 Url：

/Home/Index

/Product/Details/3

/Product

遗憾的是，较旧版本的 IIS 不会将这些请求传递到 ASP.NET 框架。 因此，这些请求不会路由到控制器。 例如，如果发出浏览器请求 URL/Home/Index，则会收到图2中的错误页。

[!["新建项目" 对话框](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image2.jpg)](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image3.png)

**图 2**：收到 "找不到 404" 错误（[单击以查看完全大小的映像](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image4.png)）

较早版本的 IIS 仅将某些请求映射到 ASP.NET 框架。 请求必须为具有正确文件扩展名的 URL。 例如，/SomePage.aspx 的请求将映射到 ASP.NET framework。 但是，/SomePage.htm 的请求不会。

因此，若要使 ASP.NET 路由正常工作，必须修改默认路由，使其包含映射到 ASP.NET 框架的文件扩展名。

这是使用名为 `registermvc.wsf`的脚本来完成的。 它包含在 `C:\Program Files\Microsoft ASP.NET\ASP.NET MVC\Scripts`中的 ASP.NET MVC 1 版本中，但从 ASP.NET 2 开始，此脚本已移至 ASP.NET 先期备货， [http://aspnet.codeplex.com/releases/view/39978](http://aspnet.codeplex.com/releases/view/39978)提供。

执行此脚本会向 IIS 注册一个新的 mvc 扩展。 注册 mvc 扩展后，可以修改 global.asax 文件中的路由，以便路由使用 mvc 扩展。

清单2中修改的 Global.asa 文件与较旧版本的 IIS 一起使用。

**列表 2-global.asax （已通过扩展进行修改）**

[!code-vb[Main](using-asp-net-mvc-with-different-versions-of-iis-vb/samples/sample2.vb)]

重要提示：请记得在更改 global.asax 文件后再次生成 ASP.NET MVC 应用程序。

清单2中的 global.asax 文件有两个重要更改。 现在，global.asax 中定义了两个路由。 默认路由的 URL 模式（第一个路由）现在如下所示：

{controller}.mvc/{action}/{id}

添加 mvc 扩展会更改 ASP.NET 路由模块截获的文件类型。 进行此更改后，ASP.NET MVC 应用程序现在会路由请求，如下所示：

/Home.mvc/Index/

/Product.mvc/Details/3

/Product.mvc/

第二个路由，根路由是新的。 根路由的此 URL 模式为空字符串。 对于对应用程序的根目录进行的匹配请求，此路由是必需的。 例如，根路由将匹配类似于下面的请求：

[http://www.YourApplication.com/](http://www.YourApplication.com/)

对路由表进行这些修改后，需要确保应用程序中的所有链接都与这些新的 URL 模式兼容。 换句话说，请确保所有的链接都包含 mvc 扩展名。 如果使用 Html.actionlink （）帮助器方法来生成链接，则不需要进行任何更改。

可以不使用 registermvc 脚本，而是向 IIS 添加新的扩展，并将其手动映射到 ASP.NET framework。 当你自己添加新扩展时，请确保未选中标有 "**验证该文件是否存在**" 的复选框。

## <a name="hosted-server"></a>托管服务器

您不会始终有权访问您的 web 服务器。 例如，如果使用 Internet 宿主提供程序托管 ASP.NET MVC 应用程序，则无需访问 IIS。

在这种情况下，应使用映射到 ASP.NET 框架的现有文件扩展名之一。 映射到 ASP.NET 的文件扩展名的示例包括 .aspx、axd 和. foo.ashx 扩展。

例如，在列表3中修改的 global.asax 文件使用 .aspx 扩展名而不是 mvc 扩展名。

**列表 3-global.asax （已修改为 .aspx 扩展名）**

[!code-vb[Main](using-asp-net-mvc-with-different-versions-of-iis-vb/samples/sample3.vb)]

清单3中的 Global.asa 文件与以前的 Global.asa 文件完全相同，只是它使用 .aspx 扩展名而不是 mvc 扩展名。 无需在远程 web 服务器上执行任何设置即可使用 .aspx 扩展。

## <a name="creating-a-wildcard-script-map"></a>创建通配符脚本映射

如果不想修改 ASP.NET MVC 应用程序的 Url，并且有权访问 web 服务器，则可以使用其他选项。 你可以创建一个通配符脚本映射，用于将对 web 服务器的所有请求映射到 ASP.NET 框架。 通过这种方式，可以将默认的 ASP.NET MVC 路由表与 IIS 7.0 （在经典模式下）或 IIS 6.0 一起使用。

请注意，此选项会使 IIS 截获针对 web 服务器发出的每个请求。 这包括图像、经典 ASP 页面和 HTML 页面的请求。 因此，启用 ASP.NET 的通配符脚本映射确实会影响性能。

下面介绍如何为 IIS 7.0 启用通配符脚本映射：

1. 在 "连接" 窗口中选择应用程序
2. 请确保已选择 "**功能**视图"
3. 双击 "**处理程序映射**" 按钮
4. 单击 "**添加通配符脚本映射**" 链接（见图3）
5. 输入 aspnet\_isapi .dll 文件的路径（可以从 Pagehandlerfactory-isapi 脚本映射复制此路径）
6. 输入名称 MVC
7. 单击 **"确定"** 按钮

[!["新建项目" 对话框](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image3.jpg)](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image5.png)

**图 3**：使用 IIS 7.0 创建通配符脚本映射（[单击以查看完全大小的映像](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image6.png)）

按照以下步骤使用 IIS 6.0 创建通配符脚本映射：

1. 右键单击网站，然后选择 "属性"
2. 选择 "**主目录**" 选项卡
3. 单击 "**配置**" 按钮
4. 选择 "**映射**" 选项卡
5. 单击 "**插入**" 按钮（见图4）
6. 将 aspnet\_的路径粘贴到可执行字段中（可从 .aspx 文件的脚本映射复制此路径）
7. 取消选中标有 "**验证该文件是否存在**" 的复选框
8. 单击 **"确定"** 按钮

[!["新建项目" 对话框](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image4.jpg)](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image7.png)

**图 4**：使用 IIS 6.0 创建通配符脚本映射（[单击以查看完全大小的映像](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image8.png)）

启用通配符脚本映射后，需要修改 global.asax 文件中的路由表，使其包含根路由。 否则，在对应用程序的根页发出请求时，会收到图5中的错误页。 可以在清单4中使用修改后的 global.asax 文件。

[!["新建项目" 对话框](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image5.jpg)](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image9.png)

**图 5**：缺少根路由错误（[单击以查看完全大小的映像](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image10.png)）

**列表 4-global.asax （已在根路由中修改）**

[!code-vb[Main](using-asp-net-mvc-with-different-versions-of-iis-vb/samples/sample4.vb)]

为 IIS 7.0 或 IIS 6.0 启用通配符脚本映射后，可以发出请求来处理默认路由表，如下所示：

/

/Home/Index

/Product/Details/3

/Product

## <a name="summary"></a>摘要

本教程的目的是说明如何在使用较旧版本的 IIS （或经典模式下的 IIS 7.0）时使用 ASP.NET MVC。 我们讨论了两种方法来获取 ASP.NET 路由，以便使用较旧版本的 IIS：修改默认路由表或创建通配符脚本映射。

第一个选项要求修改 ASP.NET MVC 应用程序中使用的 Url。 第一种方法的一个非常重要的优点是，您不需要访问 web 服务器即可修改路由表。 这意味着，即使在向 Internet 托管公司托管 ASP.NET MVC 应用程序时，也可以使用第一个选项。

第二种方法是创建通配符脚本映射。 此第二个选项的优点是不需要修改 Url。 此第二个选项的缺点是它可能会影响 ASP.NET MVC 应用程序的性能。

> [!div class="step-by-step"]
> [上一页](using-asp-net-mvc-with-different-versions-of-iis-cs.md)
