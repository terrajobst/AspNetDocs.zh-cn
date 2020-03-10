---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-2
title: 第2部分：控制器 |Microsoft Docs
author: jongalloway
description: 本教程系列详细介绍了生成 ASP.NET MVC 音乐应用商店示例应用程序所需执行的所有步骤。 第2部分涵盖控制器。
ms.author: riande
ms.date: 04/21/2011
ms.assetid: 998ce4e1-9d72-435b-8f1c-399a10ae4360
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-2
msc.type: authoredcontent
ms.openlocfilehash: 9dc2226f4951d4bed122df37d35bbb94730a00ad
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78451190"
---
# <a name="part-2-controllers"></a>第2部分：控制器

作者： [Jon Galloway](https://github.com/jongalloway)

> MVC 音乐应用商店是一个教程应用程序，该应用程序逐步介绍了如何使用 ASP.NET MVC 和 Visual Studio 进行 web 开发。  
>   
> MVC 音乐应用商店是一种轻型示例存储实现，它可以在线销售音乐专辑，并实现基本的网站管理、用户登录和购物车功能。  
>   
> 本教程系列详细介绍了生成 ASP.NET MVC 音乐应用商店示例应用程序所需执行的所有步骤。 第2部分涵盖控制器。

对于传统的 web 框架，传入 Url 通常映射到磁盘上的文件。 例如： "/Products.aspx" 或 "/Products.php" 等 URL 请求可能由 "Products" 或 "Products" 文件处理。

基于 Web 的 MVC 框架以略有不同的方式将 Url 映射到服务器代码。 它们不会将传入 Url 映射到文件，而是将 Url 映射到类的方法。 这些类称为 "控制器"，它们负责处理传入的 HTTP 请求，处理用户输入，检索和保存数据，确定要发送回客户端的响应（显示 HTML、下载文件、重定向到其他URL，等等）。

## <a name="adding-a-homecontroller"></a>添加 HomeController

我们将通过添加一个控制器类来开始我们的 MVC 音乐应用商店应用程序，该控制器类将处理 Url 到我们站点的主页。 我们将遵循 ASP.NET MVC 的默认命名约定，并将其称为 HomeController。

右键单击解决方案资源管理器中的 "控制器" 文件夹，选择 "添加"，然后选择 "控制器 ..."command

![](mvc-music-store-part-2/_static/image1.jpg)

此时将显示 "添加控制器" 对话框。 将控制器命名为 "HomeController"，然后按 "添加" 按钮。

![](mvc-music-store-part-2/_static/image1.png)

这将创建一个具有以下代码的新文件 HomeController.cs：

[!code-csharp[Main](mvc-music-store-part-2/samples/sample1.cs)]

若要尽可能简单地启动，请将 Index 方法替换为简单方法，只返回一个字符串。 我们将进行两个更改：

- 更改方法以返回字符串而不是 ActionResult
- 更改 return 语句以返回 "Hello from Home"

方法现在应如下所示：

[!code-csharp[Main](mvc-music-store-part-2/samples/sample2.cs)]

## <a name="running-the-application"></a>运行应用程序

现在，让我们运行站点。 我们可以启动我们的 web 服务器，并使用以下任意一种来尝试使用该站点：

- 选择 Debug ⇨开始调试菜单项
- 单击工具栏中的绿色箭头按钮 ![](mvc-music-store-part-2/_static/image2.jpg)
- 使用键盘快捷方式 F5。

使用上述任一步骤，将编译项目，然后导致开始使用 Visual Web Developer 的 ASP.NET 开发服务器。 屏幕的底部会出现一个通知，指示 ASP.NET 开发服务器已启动，并将显示在其下运行的端口号。

![](mvc-music-store-part-2/_static/image2.png)

然后，Visual Web Developer 会自动打开其 URL 指向我们的 Web 服务器的浏览器窗口。 这样，我们就可以快速试用我们的 web 应用程序：

![](mvc-music-store-part-2/_static/image3.png)

好了，这很简单–我们创建了一个新的网站，添加了一个三行函数，并且我们在浏览器中获得了文本。 不是火箭的，但它是一种开始。

*请注意，Visual Web Developer 包含 ASP.NET 开发服务器，它将以随机免费的 "端口" 号运行你的网站。在上面的屏幕截图中，站点正在 `http://localhost:26641/`上运行，因此使用的是端口26641。端口号会有所不同。当我们在本教程中讨论 URL （如/Store/Browse）时，将在端口号后发送。假设端口号为26641，浏览到/Store/Browse 将意味着浏览到 `http://localhost:26641/Store/Browse`。*

## <a name="adding-a-storecontroller"></a>添加 StoreController

我们添加了一个简单的 HomeController，用于实现网站的主页。 现在，让我们添加另一个要用于实现音乐商店浏览功能的控制器。 我们的应用商店控制器将支持三个方案：

- 音乐应用商店中音乐流派的列表页
- 列出特定流派中所有音乐唱片集的浏览页
- 显示特定音乐唱片集相关信息的详细信息页

首先，我们将添加一个新的 StoreController 类。 如果尚未这样做，请通过关闭浏览器或选择 Debug ⇨停止调试菜单项来停止运行该应用程序。

现在，添加一个新 StoreController。 与使用 HomeController 时一样，通过右键单击解决方案资源管理器中的 "控制器" 文件夹，然后选择 "&gt;控制器" 菜单项来实现此目的。

![](mvc-music-store-part-2/_static/image4.png)

新 StoreController 已有 "Index" 方法。 我们将使用此 "索引" 方法来实现列出音乐商店中所有流派的列表页。 我们还将添加另外两个方法来实现我们希望 StoreController 处理的其他两个方案：浏览和详细信息。

我们的控制器中的这些方法（索引、浏览和详细信息）称为 "控制器操作"，正如您已看到的 HomeController （）操作方法，其工作是响应 URL 请求，（一般而言，）确定哪些内容应发送回调用该 URL 的浏览器或用户。

我们将通过将 theIndex （）方法更改为返回字符串 "Hello from StoreController （）" 来开始我们的实现，我们将为浏览（）和详细信息（）添加类似的方法：

[!code-csharp[Main](mvc-music-store-part-2/samples/sample3.cs)]

再次运行该项目，并浏览以下 Url：

- /Store
- /Store/Browse
- /Store/Details

访问这些 Url 将调用控制器中的操作方法，并返回字符串响应：

![](mvc-music-store-part-2/_static/image5.png)

这很好，但这只是常量字符串。 让我们将它们设置为动态，使其从 URL 获取信息并在页面输出中显示信息。

首先，我们将更改浏览操作方法，以从 URL 中检索查询字符串值。 为此，我们可以将 "流派" 参数添加到操作方法。 当我们执行此操作时，MVC 会自动将名为 "流派" 的查询参数或窗体 post 参数传递给调用方法。

[!code-csharp[Main](mvc-music-store-part-2/samples/sample4.cs)]

*注意：我们使用的是 Httputility.javascriptstringencode Server.htmlencode 实用工具方法来净化用户输入。这会阻止用户使用类似/Store/Browse 的链接向视图中注入 Javascript？流派 =&lt;脚本&gt;window。 location = "http://hackersite.com"&lt;/script&gt;。*

现在让我们浏览到/Store/Browse？流派 = Disco

![](mvc-music-store-part-2/_static/image6.png)

接下来，请更改详细信息操作以读取和显示名为 ID 的输入参数。 与我们以前的方法不同，我们不会将 ID 值作为 querystring 参数嵌入。 相反，我们会直接将它嵌入到 URL 内。 例如：/Store/Details/5。

ASP.NET MVC 使我们无需配置任何内容即可轻松实现此目的。 ASP.NET MVC 的默认路由约定是将操作方法名称后面的 URL 段视为名为 "ID" 的参数。 如果操作方法有一个名为 ID 的参数，ASP.NET MVC 会自动将 URL 段作为参数传递给你。

[!code-csharp[Main](mvc-music-store-part-2/samples/sample5.cs)]

运行应用程序并浏览到/Store/Details/5：

![](mvc-music-store-part-2/_static/image7.png)

我们来回顾一下我们目前所做的事情：

- 我们已在 Visual Web Developer 中创建了新的 ASP.NET MVC 项目
- 我们讨论了 ASP.NET MVC 应用程序的基本文件夹结构
- 我们已了解如何使用 ASP.NET 开发服务器
- 我们创建了两个控制器类： HomeController 和 StoreController
- 我们已向控制器添加了操作方法，这些方法可响应 URL 请求并向浏览器返回文本

> [!div class="step-by-step"]
> [上一页](mvc-music-store-part-1.md)
> [下一页](mvc-music-store-part-3.md)
