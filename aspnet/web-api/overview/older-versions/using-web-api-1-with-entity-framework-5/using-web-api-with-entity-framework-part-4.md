---
uid: web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-4
title: 第4部分：添加管理视图 |Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 07/04/2012
ms.assetid: 792f4513-a508-4d14-a0dd-1a2fe282c7bb
msc.legacyurl: /web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-4
msc.type: authoredcontent
ms.openlocfilehash: 664aeb33031e933322886a6d6bdd989277e9fda2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78447878"
---
# <a name="part-4-adding-an-admin-view"></a>第4部分：添加管理员视图

作者： [Mike Wasson](https://github.com/MikeWasson)

[下载完成的项目](https://code.msdn.microsoft.com/ASP-NET-Web-API-with-afa30545)

## <a name="add-an-admin-view"></a>添加管理员视图

现在，我们将转到客户端，并添加可使用管理控制器中的数据的页面。 此页允许用户通过将 AJAX 请求发送到控制器来创建、编辑或删除产品。

在解决方案资源管理器中，展开 "控制器" 文件夹，然后打开名为 "HomeController.cs" 的文件。 此文件包含 MVC 控制器。 添加一个名为 `Admin`的方法：

[!code-csharp[Main](using-web-api-with-entity-framework-part-4/samples/sample1.cs)]

**HttpRouteUrl**方法创建 web API 的 URI，并将其存储在查看包中供以后查看。

接下来，将文本光标置于 `Admin` 操作方法中，然后右键单击并选择 "**添加视图**"。 此时将显示 "**添加视图**" 对话框。

![](using-web-api-with-entity-framework-part-4/_static/image1.png)

在 "**添加视图**" 对话框中，将视图命名为 "Admin"。 选中标签为 "**创建强类型视图**" 的复选框。 在 "**模型类**" 下，选择 "Product （ProductStore）"。 将所有其他选项保留为其默认值。

![](using-web-api-with-entity-framework-part-4/_static/image2.png)

单击 "**添加**" 将在 "视图"/"主页" 打开此文件并添加以下 HTML。 此 HTML 定义了页面的结构，但尚未连接任何功能。

[!code-cshtml[Main](using-web-api-with-entity-framework-part-4/samples/sample2.cshtml)]

## <a name="create-a-link-to-the-admin-page"></a>创建指向管理页面的链接

在解决方案资源管理器中，展开 "Views" 文件夹，然后展开 "共享" 文件夹。 打开名为 \_Layout 的文件。 找到 id 为 "menu" 的**ul**元素，并找到 "管理" 视图的操作链接：

[!code-cshtml[Main](using-web-api-with-entity-framework-part-4/samples/sample3.cshtml)]

> [!NOTE]
> 在示例项目中，我进行了一些其他修饰更改，如替换字符串 "您的徽标"。 这不会影响应用程序的功能。 您可以下载项目并比较文件。

运行应用程序，并单击 "管理" 链接，该链接显示在主页的顶部。 "管理员" 页应该如下所示：

![](using-web-api-with-entity-framework-part-4/_static/image3.png)

现在，页面不会执行任何操作。 在下一部分中，我们将使用挖空创建动态 UI。

## <a name="add-authorization"></a>添加授权

访问站点的任何人当前都可以访问 "管理" 页。 让我们将其更改为限制管理员权限。

首先添加 "管理员" 角色和管理员用户。 在解决方案资源管理器中，展开 "筛选器" 文件夹，然后打开名为 "InitializeSimpleMembershipAttribute.cs" 的文件。 找到 `SimpleMembershipInitializer` 构造函数。 调用**WebSecurity InitializeDatabaseConnection**后，添加以下代码：

[!code-csharp[Main](using-web-api-with-entity-framework-part-4/samples/sample4.cs)]

这是添加 "管理员" 角色并为角色创建用户的一种快速而完善的方式。

在解决方案资源管理器中，展开 "控制器" 文件夹并打开 HomeController.cs 文件。 将**授权**特性添加到 `Admin` 方法。

[!code-csharp[Main](using-web-api-with-entity-framework-part-4/samples/sample5.cs)]

打开 AdminController.cs 文件，并将**授权**属性添加到整个 `AdminController` 类中。

[!code-csharp[Main](using-web-api-with-entity-framework-part-4/samples/sample6.cs)]

> [!NOTE]
> MVC 和 Web API 在不同的命名空间中定义**授权**属性。 MVC 使用**AuthorizeAttribute**，而 Web API 使用**AuthorizeAttribute**的情况下。

现在，只有管理员才能查看 "管理" 页。 此外，如果向管理控制器发送 HTTP 请求，则该请求必须包含身份验证 cookie。 如果没有，则服务器将发送 HTTP 401 （未授权）响应。 可以通过将 GET 请求发送到 `http://localhost:*port*/api/admin`在 Fiddler 中查看此项。

> [!div class="step-by-step"]
> [上一页](using-web-api-with-entity-framework-part-3.md)
> [下一页](using-web-api-with-entity-framework-part-5.md)
