---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/url-routing
title: URL 路由 |Microsoft Docs
author: Erikre
description: 本系列教程将介绍使用 ASP.NET 4.5 构建 ASP.NET Web 窗体应用程序的基础知识，并为我们 Microsoft Visual Studio Express 2013 。
ms.author: riande
ms.date: 09/08/2014
ms.assetid: 4f4bf092-c400-471f-a876-78fda0417890
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/url-routing
msc.type: authoredcontent
ms.openlocfilehash: 66b727b69ca4f9a3d35b67f492f9a554146e09ef
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74590714"
---
# <a name="url-routing"></a>URL 路由

作者： [Erik Reitan](https://github.com/Erikre)

[下载 Wingtip 玩具示例项目（C#）](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409)或[下载电子书（PDF）](https://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)

> 本系列教程将介绍使用 ASP.NET 4.5 构建 ASP.NET Web 窗体应用程序的基础知识，并为 Web Microsoft Visual Studio Express 2013。 此教程系列附带有[ C#源代码](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409)的 Visual Studio 2013 项目。

在本教程中，您将修改 Wingtip 玩具示例应用程序以支持 URL 路由。 使用路由，你的 web 应用程序可以使用友好、更易于记住且更好的搜索引擎支持的 Url。 本教程基于前面的 "成员资格和管理" 教程，是 Wingtip 玩具教程系列的一部分。

## <a name="what-youll-learn"></a>你将学习的内容：

- 如何注册 ASP.NET Web 窗体应用程序的路由。
- 如何将路由添加到网页。
- 如何从数据库中选择数据以支持路由。

## <a name="aspnet-routing-overview"></a>ASP.NET 路由概述

使用 URL 路由，你可以将应用程序配置为接受不映射到物理文件的请求 Url。 请求 URL 只是用户在浏览器中输入的 URL，用于在您的网站上查找页面。 使用路由定义对用户具有语义意义的 Url，并可帮助搜索引擎优化（SEO）。

默认情况下，Web 窗体模板包括[ASP.NET 友好 url](http://www.nuget.org/packages/Microsoft.AspNet.FriendlyUrls/)。 许多基本的路由工作都将使用*友好的 url*来实现。 但是，在本教程中，您将添加自定义的路由功能。

自定义 URL 路由之前，Wingtip 玩具示例应用程序可以使用以下 URL 链接到产品：

`https://localhost:44300/ProductDetails.aspx?productID=2`

通过自定义 URL 路由，Wingtip 玩具示例应用程序将使用易于阅读的 URL 链接到同一产品：

`https://localhost:44300/Product/Convertible%20Car`

### <a name="routes"></a>路由

路由是映射到处理程序的 URL 模式。 处理程序可以是物理文件，例如 Web 窗体应用程序中的 .aspx 文件。 处理程序也可以是处理请求的类。 若要定义路由，可以通过指定 URL 模式、处理程序和（可选）路由名称来创建路由类的实例。

可以通过将 `Route` 对象添加到 `RouteTable` 类的静态 `Routes` 属性来向应用程序添加路由。 路由属性是存储应用程序的所有路由的 `RouteCollection` 对象。

### <a name="url-patterns"></a>URL 模式

URL 模式可以包含文本值和变量占位符（称为 URL 参数）。 文本和占位符位于 URL 的段中，这些段用斜杠（`/`）字符分隔。

对 web 应用程序发出请求时，会将 URL 分析为段和占位符，并将变量值提供给请求处理程序。 此过程类似于分析查询字符串中的数据并将其传递给请求处理程序的方式。 在这两种情况下，变量信息都包含在 URL 中，并以键值对的形式传递给处理程序。 对于查询字符串，键和值都在 URL 中。 对于路由，密钥是 URL 模式中定义的占位符名称，并且只有这些值位于 URL 中。

在 URL 模式中，可以通过将占位符括在大括号中来定义占位符（`{` 和 `}`）。 您可以在一个段中定义多个占位符，但占位符必须由文本值分隔。 例如，`{language}-{country}/{action}` 是有效的路由模式。 但 `{language}{country}/{action}` 不是有效的模式，因为占位符之间没有文本值或分隔符。 因此，路由不能确定从国家/地区占位符的值中将语言占位符的值隔开的位置。

### <a name="mapping-and-registering-routes"></a>映射和注册路由

在将路由添加到 Wingtip 玩具示例应用程序的页面之前，必须在应用程序启动时注册路由。 若要注册路由，需要修改 `Application_Start` 事件处理程序。

1. 在 Visual Studio**解决方案资源管理器**中，找到并打开*Global.asax.cs*文件。
2. 将黄色突出显示的代码添加到*Global.asax.cs*文件，如下所示：   

    [!code-csharp[Main](url-routing/samples/sample1.cs?highlight=30-31,34-46)]

当 Wingtip 玩具示例应用程序启动时，它将调用 `Application_Start` 事件处理程序。 在此事件处理程序结束时，将调用 `RegisterCustomRoutes` 方法。 `RegisterCustomRoutes` 方法通过调用 `RouteCollection` 对象的 `MapPageRoute` 方法添加每个路由。 路由使用路由名称、路由 URL 和物理 URL 来定义。

第一个参数（"`ProductsByCategoryRoute`"）是路由名称。 它用于在需要时调用路由。 第二个参数（"`Category/{categoryName}`"）定义友好的替换 URL，该 URL 可基于代码动态。 使用基于数据生成的链接填充数据控件时，可以使用此路由。 路由如下所示：

[!code-csharp[Main](url-routing/samples/sample2.cs)]

路由的第二个参数包括由大括号（`{ }`）指定的动态值。 在这种情况下，`categoryName` 是将用于确定正确路由路径的变量。

> [!NOTE] 
> 
> **Optional**
> 
> 通过将 `RegisterCustomRoutes` 方法移动到单独的类中，你可能会发现管理代码更容易。 在*逻辑*文件夹中，创建一个单独的 `RouteActions` 类。 将上面的 `RegisterCustomRoutes` 方法从*Global.asax.cs*文件移到新的 `RoutesActions` 类中。 使用 `RoleActions` 类和 `createAdmin` 方法作为如何从*Global.asax.cs*文件调用 `RegisterCustomRoutes` 方法的示例。

你还可能已注意到，在 `Application_Start` 事件处理程序的开头使用 `RouteConfig` 对象的 `RegisterRoutes` 方法调用。 此调用用于实现默认路由。 当使用 Visual Studio 的 Web 窗体模板创建应用程序时，该应用程序作为默认代码包括。

## <a name="retrieving-and-using-route-data"></a>检索和使用路由数据

如上所述，可以定义路由。 添加到*Global.asax.cs*文件中 `Application_Start` 事件处理程序的代码将加载可定义的路由。

### <a name="setting-routes"></a>设置路由

路由要求你添加更多代码。 在本教程中，您将使用模型绑定来检索使用数据控件中的数据生成路由时使用的 `RouteValueDictionary` 对象。 `RouteValueDictionary` 对象将包含属于特定产品类别的产品名称列表。 将基于数据和路由为每个产品创建一个链接。

#### <a name="enable-routes-for-categories-and-products"></a>启用类别和产品的路由

接下来，你将更新应用程序以使用 `ProductsByCategoryRoute` 来确定要为每个产品类别链接包含的正确路由。 你还将更新*ProductList*页，以包含每个产品的路由链接。 链接将显示在更改之前，但链接现在将使用 URL 路由。

1. 在**解决方案资源管理器**中，打开 "*站点" 母版页*（如果尚未打开）。
2. 用黄色突出显示的更改更新名为 "`categoryList`" 的**ListView**控件，使标记显示如下：   

    [!code-aspx[Main](url-routing/samples/sample3.aspx?highlight=7-9)]
3. 在**解决方案资源管理器**中，打开*ProductList*页。
4. 更新*ProductList*页的 `ItemTemplate` 元素，其中的更新以黄色突出显示，使标记如下所示：   

    [!code-aspx[Main](url-routing/samples/sample4.aspx?highlight=6-9,14-16)]
5. 打开*ProductList.aspx.cs*的代码隐藏，并添加以下具有黄色突出显示的命名空间：  

    [!code-csharp[Main](url-routing/samples/sample5.cs?highlight=9)]
6. 将代码隐藏（*ProductList.aspx.cs*）的 `GetProducts` 方法替换为以下代码：   

    [!code-csharp[Main](url-routing/samples/sample6.cs)]

#### <a name="add-code-for-product-details"></a>添加产品详细信息的代码

现在，请更新*ProductDetails*页的代码隐藏（*ProductDetails.aspx.cs*）以使用路由数据。 请注意，新的 `GetProduct` 方法还接受查询字符串值，这种情况下，用户具有使用较旧的非路由 URL 作为书签的链接。

1. 将代码隐藏（*ProductDetails.aspx.cs*）的 `GetProduct` 方法替换为以下代码：   

    [!code-csharp[Main](url-routing/samples/sample7.cs)]

## <a name="running-the-application"></a>运行应用程序

现在可以运行应用程序来查看更新的路由。

1. 按**F5**运行 Wingtip 玩具示例应用程序。  
 浏览器将打开并显示*default.aspx*页。
2. 单击页面顶部的 "**产品**" 链接。  
 所有产品都显示在*ProductList*页上。 将为浏览器显示以下 URL （使用端口号）：  
    `https://localhost:44300/ProductList`
3. 接下来，单击页面顶部附近的 "**汽车**类别" 链接。  
 仅汽车显示在*ProductList*页上。 将为浏览器显示以下 URL （使用端口号）：  
    `https://localhost:44300/Category/Cars`
4. 单击包含该页上列出的第一辆轿车名称的链接（"**转换汽车**"）以显示产品详细信息。  
 将为浏览器显示以下 URL （使用端口号）：  
    `https://localhost:44300/Product/Convertible%20Car`
5. 接下来，在浏览器中输入以下非路由 URL （使用端口号）：  
    `https://localhost:44300/ProductDetails.aspx?productID=2`  
 如果用户具有标记为书签的链接，则代码仍会识别包含查询字符串的 URL。

## <a name="summary"></a>总结

在本教程中，您已添加了类别和产品的路由。 您已经了解了如何将路由与使用模型绑定的数据控件集成。 在下一教程中，你将实现全局错误处理。

## <a name="additional-resources"></a>其他资源

[ASP.NET 友好 Url](http://www.nuget.org/packages/Microsoft.AspNet.FriendlyUrls/)  
[使用成员资格、OAuth 和 SQL 数据库将安全的 ASP.NET Web 窗体应用程序部署到 Azure App Service](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-webforms-app-membership-oauth-sql-database/)  
[Microsoft Azure 免费试用版](https://azure.microsoft.com/pricing/free-trial/)

> [!div class="step-by-step"]
> [上一页](membership-and-administration.md)
> [下一页](aspnet-error-handling.md)
