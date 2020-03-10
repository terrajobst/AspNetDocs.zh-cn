---
uid: web-api/overview/getting-started-with-aspnet-web-api/using-web-api-with-aspnet-web-forms
title: 结合使用 Web API 和 ASP.NET Web Forms-ASP.NET 4。x
author: MikeWasson
description: 有关将 Web API 添加到 ASP.NET 4.x 的 ASP.NET Forms 应用程序的分步指南
ms.author: riande
ms.date: 04/03/2012
ms.custom: seoapril2019
ms.assetid: 25da8c3f-4e90-4946-9765-4f160985e1e4
msc.legacyurl: /web-api/overview/getting-started-with-aspnet-web-api/using-web-api-with-aspnet-web-forms
msc.type: authoredcontent
ms.openlocfilehash: ae553b62998fefd128e12711cbde958ea42d8c63
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78448532"
---
# <a name="using-web-api-with-aspnet-web-forms"></a>向 ASP.NET Web 窗体使用 Web API

作者： [Mike Wasson](https://github.com/MikeWasson)

本教程将指导你完成将 Web API 添加到 ASP.NET 4.x 中的传统 ASP.NET Web 窗体应用程序的步骤。 

## <a name="overview"></a>概述

尽管 ASP.NET Web API 与 ASP.NET MVC 一起打包，但可以轻松地将 Web API 添加到传统的 ASP.NET Web 窗体应用程序。

若要在 Web 窗体应用程序中使用 Web API，需要执行两个主要步骤：

- 添加一个派生自**ApiController**类的 Web API 控制器。
- 将路由表添加到**应用程序\_Start**方法。

## <a name="create-a-web-forms-project"></a>创建 Web 窗体项目

启动 Visual Studio，然后从**起始**页中选择 "**新建项目**"。 或者，从 "**文件**" 菜单中选择 "**新建**"，然后选择 "**项目**"。

在 "**模板**" 窗格中，选择 "**已安装模板**"，然后展开**视觉对象C#** 节点。 在 **" C#视觉对象**" 下选择 " **Web**"。 在项目模板列表中，选择 " **ASP.NET Web 窗体应用程序**"。 输入项目的名称，然后单击 **"确定"** 。

![](using-web-api-with-aspnet-web-forms/_static/image1.png)

## <a name="create-the-model-and-controller"></a>创建模型和控制器

本教程使用与[入门](tutorial-your-first-web-api.md)教程相同的模型和控制器类。

首先，添加一个模型类。 在**解决方案资源管理器**中，右键单击项目，然后选择 "**添加类**"。 将类命名为 "Product"，并添加以下实现：

[!code-csharp[Main](using-web-api-with-aspnet-web-forms/samples/sample1.cs)]

接下来，将 Web API 控制器添加到项目。，*控制器*是处理 Web API 的 HTTP 请求的对象。

在“解决方案资源管理器”中，右键单击项目。 选择 "**添加新项**"。

![](using-web-api-with-aspnet-web-forms/_static/image2.png)

在 "**已安装的模板**" 下，展开 **C#视觉对象**并选择**Web**。 然后，在模板列表中，选择 " **WEB API 控制器类**"。 将控制器命名为 "ProductsController"，然后单击 "**添加**"。

![](using-web-api-with-aspnet-web-forms/_static/image3.png)

"**添加新项**" 向导将创建一个名为 "ProductsController.cs" 的文件。 删除向导包含的方法并添加以下方法：

[!code-csharp[Main](using-web-api-with-aspnet-web-forms/samples/sample2.cs)]

有关此控制器中代码的详细信息，请参阅[入门](tutorial-your-first-web-api.md)教程。

## <a name="add-routing-information"></a>添加路由信息

接下来，我们将添加 URI 路由，以便将 &quot;/api/products/&quot; 格式的 Uri 路由到控制器。

在**解决方案资源管理器**中，双击 "global.asax" 打开代码隐藏文件 Global.asax.cs。 添加以下**using**语句。

[!code-csharp[Main](using-web-api-with-aspnet-web-forms/samples/sample3.cs)]

然后，将以下代码添加到**应用程序\_Start**方法：

[!code-csharp[Main](using-web-api-with-aspnet-web-forms/samples/sample4.cs)]

有关路由表的详细信息，请参阅[中的路由 ASP.NET Web API](../web-api-routing-and-actions/routing-in-aspnet-web-api.md)。

## <a name="add-client-side-ajax"></a>添加客户端 AJAX

这就是创建客户端可以访问的 web API 所需的全部工作。 现在，让我们添加一个使用 jQuery 调用 API 的 HTML 页面。

请确保母版页（例如*master*）包含 `ID="HeadContent"`的 `ContentPlaceHolder`：

[!code-html[Main](using-web-api-with-aspnet-web-forms/samples/sample8.html)]

打开文件 "default.aspx"。 替换主要内容部分中的样本文本，如下所示：

[!code-aspx[Main](using-web-api-with-aspnet-web-forms/samples/sample5.aspx)]

接下来，在 `HeaderContent` 部分中添加对 jQuery 源文件的引用：

[!code-aspx[Main](using-web-api-with-aspnet-web-forms/samples/sample6.aspx?highlight=2)]

注意：通过将文件从**解决方案资源管理器**拖放到代码编辑器窗口中，可以轻松地添加脚本引用。

![](using-web-api-with-aspnet-web-forms/_static/image4.png)

在 jQuery script 标记下面添加以下脚本块：

[!code-html[Main](using-web-api-with-aspnet-web-forms/samples/sample7.html)]

加载文档时，此脚本将发出 AJAX 请求，&quot;api/产品&quot;。 请求返回 JSON 格式的产品列表。 该脚本将产品信息添加到 HTML 表中。

运行应用程序时，该应用程序应如下所示：

![](using-web-api-with-aspnet-web-forms/_static/image5.png)
