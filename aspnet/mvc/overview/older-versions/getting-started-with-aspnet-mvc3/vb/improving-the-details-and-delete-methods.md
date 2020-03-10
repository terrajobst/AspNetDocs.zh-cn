---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/improving-the-details-and-delete-methods
title: 改善详细信息和删除方法（VB） |Microsoft Docs
author: Rick-Anderson
description: 本教程将教你如何使用 Microsoft Visual Web Developer 2010 Express Service Pack 1 构建 ASP.NET MVC Web 应用程序的基础知识 。
ms.author: riande
ms.date: 01/12/2011
ms.assetid: c5c14ef0-c128-4dc1-8c01-7f0fdb09e411
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/improving-the-details-and-delete-methods
msc.type: authoredcontent
ms.openlocfilehash: 08d80cac071907e927bb30df53c6f84a28f53156
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78485540"
---
# <a name="improving-the-details-and-delete-methods-vb"></a>改进 Details 和 Delete 方法 (VB)

作者： [Rick Anderson](https://twitter.com/RickAndMSFT)

> 本教程将教你如何使用 Microsoft Visual Web Developer 2010 Express Service Pack 1 （Microsoft Visual Studio 免费版）生成 ASP.NET MVC Web 应用程序的基础知识。 在开始之前，请确保已安装下列必备组件。 可以通过单击以下链接安装所有这些[程序： Web 平台安装程序](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)。 或者，你可以使用以下链接单独安装必备组件：
> 
> - [Visual Studio Web Developer Express SP1 必备组件](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [ASP.NET MVC 3 工具更新](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - [SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)（运行时 + 工具支持）
> 
> 如果你使用的是 Visual Studio 2010 而不是 Visual Web Developer 2010，请通过单击以下链接安装必备组件： [Visual Studio 2010 必备组件](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)。
> 
> 本主题附带有 VB.NET 源代码的 Visual Web Developer 项目。 [下载 VB.NET 版本](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098)。 如果愿意C#，请切换到本教程的[ C#版本](../cs/improving-the-details-and-delete-methods.md)。

在本教程的此部分中，将对自动生成的 `Details` 和 `Delete` 方法进行一些改进。 不需要这些更改，只需少量的代码，就可以轻松地增强应用程序。

## <a name="improving-the-details-and-delete-methods"></a>改善详细信息和删除方法

当你基架 `Movie` 控制器时，ASP.NET MVC 生成的代码非常有用，但这样做只需少量的小更改就能实现更高的可靠性。

打开 `Movie` 控制器，并在找不到电影时，通过返回 `HttpNotFound` 来修改 `Details` 方法。 还应修改 `Details` 方法，以设置传递给它的 ID 的默认值。 （在本教程的第[6 部分](examining-the-edit-methods-and-edit-view.md)中，你对 `Edit` 方法进行了类似的更改。）但是，必须将 `Details` 方法的返回类型从 `ViewResult` 改为 `ActionResult`，因为 `HttpNotFound` 方法不会返回 `ViewResult` 对象。 下面的示例显示了修改后的 `Details` 方法。

[!code-vb[Main](improving-the-details-and-delete-methods/samples/sample1.vb)]

Code First 使用 `Find` 方法可以轻松地搜索数据。 在方法中内置的一项重要的安全功能是，代码验证 `Find` 方法在代码尝试使用影片之前是否找到了电影。 例如，黑客可以通过将 `http://localhost:xxxx/Movies/Details/1` 链接创建的 URL 更改为类似于 `http://localhost:xxxx/Movies/Details/12345` （或其他不表示实际电影的值），将错误引入到站点中。 如果不检查是否有空电影，这可能会导致数据库错误。

同样，更改 `Delete` 和 `DeleteConfirmed` 方法以指定 ID 参数的默认值，并在找不到电影时返回 `HttpNotFound`。 下面显示了 `Movie` 控制器中更新的 `Delete` 方法。

[!code-vb[Main](improving-the-details-and-delete-methods/samples/sample2.vb)]

请注意，`Delete` 方法不会删除数据。 执行删除操作以响应 GET 请求（或者说，执行编辑操作、创建操作或更改数据的任何其他操作）会打开安全漏洞。 有关此操作的详细信息，请参阅 Stephen Walther 的博客文章[ASP.NET MVC Tip #46 —不要使用删除链接，因为它们创建了安全漏洞](http://stephenwalther.com/blog/archive/2009/01/21/asp.net-mvc-tip-46-ndash-donrsquot-use-delete-links-because.aspx)。

删除数据的 `HttpPost` 方法命名为 `DeleteConfirmed`，以便为 HTTP POST 方法提供一个唯一的签名或名称。 下面显示了两个方法签名：

[!code-vb[Main](improving-the-details-and-delete-methods/samples/sample3.vb)]

公共语言运行时（CLR）要求重载方法具有唯一签名（相同名称、不同的参数列表）。 但在这里，你需要两个删除方法-一个用于 GET，另一个用于 POST，这两种方法都需要相同的签名。 （它们都需要接受单个整数作为参数。）

为此，可以执行几项操作。 一种方式是为方法指定不同的名称。 这就是我们在前面的示例中执行的操作。 但是，这会造成一个小问题：ASP.NET 按名称将 URL 段映射到操作方法，如果重命名方法，则路由通常无法找到该方法。 该示例中也提供了解决方案，即向 `ActionName("Delete")` 方法添加 `DeleteConfirmed` 属性。 这将有效地为路由系统执行映射，以便包含 POST 请求的<em>/Delete/</em>的 URL 将查找 `DeleteConfirmed` 方法。

避免具有相同名称和签名的方法的问题的另一种方法是，通过人为更改 POST 方法的签名，以包含未使用的参数。 例如，某些开发人员添加了一个传递给 POST 方法的参数类型 `FormCollection`，只是不使用参数：

[!code-vb[Main](improving-the-details-and-delete-methods/samples/sample4.vb)]

## <a name="wrapping-up"></a>总结

现在，你有了一个完整的 ASP.NET MVC 应用程序，它将数据存储在 SQL Server Compact 数据库中。 你可以创建、读取、更新、删除和搜索电影。

![](improving-the-details-and-delete-methods/_static/image1.png)

本基本教程介绍了如何开始创建控制器，如何将它们与视图相关联，以及如何传递硬编码数据。 然后，您创建并设计了一个数据模型。 实体框架 Code First 动态地从数据模型创建数据库，ASP.NET MVC 基架系统会自动生成基本 CRUD 操作的操作方法和视图。 然后，你添加了一个允许用户在数据库中搜索的搜索窗体。 您已将数据库更改为包含新的数据列，然后更新了两个页面以创建和显示此新数据。 您通过使用 `DataAnnotations` 命名空间中的特性标记数据模型来添加验证。 生成的验证在客户端和服务器上运行。

如果要部署应用程序，最好先在本地 IIS 7 服务器上测试应用程序。 你可以使用此[Web 平台安装程序](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=ASPNET;)链接对 ASP.NET 应用程序启用 IIS 设置。 请参阅以下部署链接：

- [ASP.NET 部署内容映射](https://msdn.microsoft.com/library/dd394698.aspx)
- [启用 IIS 7、windows](https://blogs.msdn.com/b/rickandy/archive/2011/03/14/enabling-iis-7-x-on-windows-7-vista-sp1-windows-2008-windows-2008-r2.aspx)
- [Web 应用程序项目部署](https://msdn.microsoft.com/library/dd394698.aspx)

我现在建议你转到我们的中级，为 ASP.NET MVC 应用程序和[MVC 音乐应用商店](../../mvc-music-store/mvc-music-store-part-1.md)教程[创建实体框架数据模型](../../../getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)，探索[MSDN 上的 ASP.NET 文章](https://msdn.microsoft.com/library/gg416514(VS.98).aspx)，并查看[https://asp.net/mvc](https://asp.net/mvc)的多个视频和资源，以便更多地了解 ASP.NET MVC！ [ASP.NET MVC 论坛](https://forums.asp.net/1146.aspx)是提出问题的好地方。

请尽情体验吧！

-Scott Hanselman （[http://hanselman.com](http://hanselman.com)和[@shanselman](http://twitter.com/shanselman)在 Twitter 上）和 Rick Anderson [blogs.msdn.com/rickAndy](https://blogs.msdn.com/rickAndy)

> [!div class="step-by-step"]
> [上一页](adding-validation-to-the-model.md)
