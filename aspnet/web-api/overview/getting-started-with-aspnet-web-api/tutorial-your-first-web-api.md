---
uid: web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api
title: 开始处理 ASP.NET Web API 2 （C#）-ASP.NET 4。x
author: MikeWasson
description: 代码教程。 使用 ASP.NET Web API 创建返回产品列表的 Web API。
ms.author: riande
ms.date: 11/28/2017
ms.custom: seoapril2019
msc.legacyurl: /web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api
msc.type: authoredcontent
ms.openlocfilehash: 3e35c2bc0e46dfdb4544b772775eddd533f27be3
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78448550"
---
# <a name="get-started-with-aspnet-web-api-2-c"></a>ASP.NET Web API 2 （C#）入门

作者： [Mike Wasson](https://github.com/MikeWasson)

[下载完成的项目](https://code.msdn.microsoft.com/Sample-code-of-Getting-c56ccb28)

在本教程中，你将使用 ASP.NET Web API 创建返回产品列表的 Web API。

HTTP 并非仅用于为网页提供服务。 HTTP 也是一个功能强大的平台，用于构建公开服务和数据的 Api。 HTTP 简单、灵活且无处不在。 几乎任何可以考虑的平台都有一个 HTTP 库，因此 HTTP 服务可以访问范围广泛的客户端，包括浏览器、移动设备和传统的桌面应用程序。

ASP.NET Web API 是一个用于在 .NET Framework 之上构建 Web API 的框架。 

## <a name="software-versions-used-in-the-tutorial"></a>本教程中使用的软件版本

- [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)
- Web API 2

有关本教程的更高版本，请参阅[使用 ASP.NET Core 和 Visual Studio For Windows 创建 WEB API](https://docs.microsoft.com/aspnet/core/tutorials/first-web-api) 。

## <a name="create-a-web-api-project"></a>创建 Web API 项目

在本教程中，你将使用 ASP.NET Web API 创建返回产品列表的 Web API。 前端网页使用 jQuery 显示结果。

![](tutorial-your-first-web-api/_static/image1.png)

启动 Visual Studio，然后从**起始**页中选择 "**新建项目**"。 或者，从 "**文件**" 菜单中选择 "**新建**"，然后选择 "**项目**"。

在 "**模板**" 窗格中，选择 "**已安装模板**"，然后展开**视觉对象C#** 节点。 在 **" C#视觉对象**" 下选择 " **Web**"。 在项目模板列表中，选择 " **ASP.NET Web 应用程序**"。 将项目命名为 "ProductsApp"，然后单击 **"确定**"。

![](tutorial-your-first-web-api/_static/image2.png)

在 "**新建 ASP.NET 项目**" 对话框中，选择 "**空**" 模板。 在 &quot;为&quot;添加文件夹和核心引用 "下，检查**WEB API**。 单击“确定”。

![](tutorial-your-first-web-api/_static/image3.png)

> [!NOTE]
> 你还可以使用 &quot;Web API&quot; 模板创建 Web API 项目。 Web API 模板使用 ASP.NET MVC 提供 API 帮助页。 我使用的是本教程的空模板，因为我想要显示没有 MVC 的 Web API。 一般情况下，不需要知道 ASP.NET MVC 即可使用 Web API。

## <a name="adding-a-model"></a>添加模型

模型是表示应用程序中的数据的对象。 ASP.NET Web API 可以将模型自动序列化为 JSON、XML 或其他格式，然后将序列化的数据写入 HTTP 响应消息的正文中。 只要客户端可以读取序列化格式，它就可以反序列化该对象。 大多数客户端可以解析 XML 或 JSON。 而且，客户端可以通过在 HTTP 请求消息中设置 Accept 标头来指示它需要哪种格式。

首先，让我们创建一个表示产品的简单模型。

如果解决方案资源管理器尚未出现，请单击“视图”菜单，并选择“解决方案资源管理器”。 在解决方案资源管理器中，右键单击“模型”文件夹。 在上下文菜单中，依次选择“添加”、“类”。

![](tutorial-your-first-web-api/_static/image4.png)

将类命名为 &quot;产品&quot;。 将以下属性添加到 `Product` 类。

[!code-csharp[Main](tutorial-your-first-web-api/samples/sample1.cs)]

## <a name="adding-a-controller"></a>添加控制器

在 Web API 中，控制器是处理 HTTP 请求的对象。 我们将添加一个控制器，该控制器可返回产品列表或由 ID 指定的单个产品。

> [!NOTE]
> 如果已使用 ASP.NET MVC，则已熟悉控制器。 Web API 控制器类似于 MVC 控制器，但继承了**ApiController**类而不是**Controller**类。

在“解决方案资源管理器”中，右键单击“控制器”文件夹。 依次选择“添加”、“控制器”。

![](tutorial-your-first-web-api/_static/image5.png)

在“添加基架”对话框中，选择“Web API 控制器 - 空”。 单击 **“添加”** 。

![](tutorial-your-first-web-api/_static/image6.png)

在 "**添加控制器**" 对话框中，将控制器命名为 &quot;ProductsController&quot;。 单击 **“添加”** 。

![](tutorial-your-first-web-api/_static/image7.png)

基架会在 "控制器" 文件夹中创建一个名为 "ProductsController.cs" 的文件。

![](tutorial-your-first-web-api/_static/image8.png)

> [!NOTE]
> 不需要将控制器放入名为控制器的文件夹中。 文件夹名称只是一种用于组织源文件的简便方法。

如果此文件尚未打开，请双击文件将其打开。 将此文件中的代码替换为以下代码：

[!code-csharp[Main](tutorial-your-first-web-api/samples/sample2.cs)]

为了使示例简单，产品存储在控制器类内的固定阵列中。 当然，在实际的应用程序中，您将查询数据库或使用其他外部数据源。

控制器定义了返回产品的两个方法：

- `GetAllProducts` 方法将整个产品列表作为**IEnumerable&lt;产品&gt;** 类型返回。
- `GetProduct` 方法按 ID 查找单个产品。

就这么简单！ 你有一个有效的 web API。 控制器上的每个方法都对应于一个或多个 Uri：

| 控制器方法 | URI |
| --- | --- |
| GetAllProducts | /api/products |
| GetProduct | /api/products/*id* |

对于 `GetProduct` 方法，URI 中的*id*是占位符。 例如，若要获取 ID 为5的产品，请 `api/products/5`URI。

有关 Web API 如何将 HTTP 请求路由到控制器方法的详细信息，请参阅[中的路由 ASP.NET Web API](../web-api-routing-and-actions/routing-in-aspnet-web-api.md)。

## <a name="calling-the-web-api-with-javascript-and-jquery"></a>通过 Javascript 和 jQuery 调用 Web API

在本部分中，我们将添加一个使用 AJAX 调用 web API 的 HTML 页面。 我们将使用 jQuery 进行 AJAX 调用，并使用结果来更新页面。

在解决方案资源管理器中，右键单击项目并选择 "**添加**"，然后选择 "**新建项**"。

![](tutorial-your-first-web-api/_static/image9.png)

在 "**添加新项**" 对话框中，选择 "**视觉对象C#** " 下的 " **Web** " 节点，然后选择 " **HTML" 页**项。 将该页命名为 &quot;&quot;的索引。

![](tutorial-your-first-web-api/_static/image10.png)

将此文件中的所有内容替换为以下内容：

[!code-html[Main](tutorial-your-first-web-api/samples/sample3.html)]

有多种方式可以获取 jQuery。 在此示例中，我使用了[Microsoft AJAX CDN](../../../ajax/cdn/overview.md)。 你还可以从[http://jquery.com/](http://jquery.com/)下载它，ASP.NET 的 "Web API" 项目模板也包含 jQuery。

### <a name="getting-a-list-of-products"></a>获取产品列表

若要获取产品列表，请将 HTTP GET 请求发送到 &quot;/api/products&quot;。

JQuery [getJSON](http://api.jquery.com/jQuery.getJSON/)函数发送 AJAX 请求。 For response 包含 JSON 对象的数组。 `done` 函数指定在请求成功时调用的回调。 在回调中，我们用产品信息更新 DOM。

[!code-html[Main](tutorial-your-first-web-api/samples/sample4.html)]

### <a name="getting-a-product-by-id"></a>按 ID 获取产品

若要按 ID 获取产品，请将 HTTP GET 请求发送到 &quot;/api/products/*id*&quot;，其中*ID*为产品 id。

[!code-javascript[Main](tutorial-your-first-web-api/samples/sample5.js)]

我们仍调用 `getJSON` 来发送 AJAX 请求，但这次我们将 ID 放在请求 URI 中。 此请求的响应是单个产品的 JSON 表示形式。

## <a name="running-the-application"></a>运行应用程序

按 F5 开始调试应用程序。 网页应如下所示：

![](tutorial-your-first-web-api/_static/image11.png)

若要按 ID 获取产品，请输入 ID，然后单击 "搜索"：

![](tutorial-your-first-web-api/_static/image12.png)

如果输入的 ID 无效，服务器将返回 HTTP 错误：

![](tutorial-your-first-web-api/_static/image13.png)

## <a name="using-f12-to-view-the-http-request-and-response"></a>使用 F12 查看 HTTP 请求和响应

使用 HTTP 服务时，查看 HTTP 请求和请求消息可能非常有用。 可以通过使用 Internet Explorer 9 中的 F12 开发人员工具来执行此操作。 在 Internet Explorer 9 中，按**F12**打开工具。 单击 "**网络**" 选项卡，然后按 "**开始捕获**"。 现在返回网页并按**F5**重新加载网页。 Internet Explorer 将捕获浏览器与 web 服务器之间的 HTTP 流量。 "摘要" 视图显示页面的所有网络流量：

![](tutorial-your-first-web-api/_static/image14.png)

找到相对 URI "api/products/" 的条目。 选择此条目，并单击 "**前往详细信息**"。 在详细信息视图中，有选项卡可用于查看请求和响应标头和正文。 例如，如果单击 "**请求标头**" 选项卡，你可以看到客户端在 Accept 标头中请求 &quot;application/json&quot;。

![](tutorial-your-first-web-api/_static/image15.png)

如果单击 "响应正文" 选项卡，则可以看到如何将产品列表序列化为 JSON。 其他浏览器具有类似的功能。 另一种有用的工具是[Fiddler](http://www.fiddler2.com/fiddler2/)，这是一个 web 调试代理。 你可以使用 Fiddler 来查看 HTTP 流量，还可以编写 HTTP 请求，这使你可以完全控制请求中的 HTTP 标头。

## <a name="see-this-app-running-on-azure"></a>查看此应用在 Azure 上运行

要查看作为实时 web 应用运行的已完成站点吗？ 只需单击以下按钮，即可将应用程序的完整版本部署到 Azure 帐户。

[![](https://azuredeploy.net/deploybutton.png)](https://deploy.azure.com/?WT.mc_id=deploy_azure_aspnet&repository=https://github.com/tfitzmac/WebAPI-ProductsApp#/form/setup)

需要一个 Azure 帐户才能将此解决方案部署到 Azure。 如果还没有帐户，可以使用以下选项：

- [免费打开 Azure 帐户](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A443DD604)-获取可用来试用付费版 Azure 服务的信用额度，甚至在用完信用额度后，你仍可以保留帐户和使用免费的 azure 服务。
- [激活 msdn 订户权益](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604)-msdn 订阅每月提供可用于付费 Azure 服务的信用额度。

## <a name="next-steps"></a>后续步骤

- 有关支持 POST、PUT 和 DELETE 操作以及写入数据库的 HTTP 服务的更完整示例，请参阅将[WEB API 2 与实体框架6一起使用](../data/using-web-api-with-entity-framework/part-1.md)。
- 若要深入了解如何在 HTTP 服务的基础上创建流畅的响应式 web 应用程序，请参阅[ASP.NET 单页应用程序](../../../single-page-application/index.md)。
- 有关如何将 Visual Studio web 项目部署到 Azure App Service 的信息，请参阅[在 Azure App Service 中创建 ASP.NET web 应用](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-get-started/)。
