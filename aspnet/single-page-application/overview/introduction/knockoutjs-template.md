---
uid: single-page-application/overview/introduction/knockoutjs-template
title: 单页应用程序： KnockoutJS 模板 |Microsoft Docs
author: MikeWasson
description: 挖空模板
ms.author: riande
ms.date: 01/30/2013
ms.assetid: f9c07af0-4b20-4b08-af8f-47fc3df169a2
msc.legacyurl: /single-page-application/overview/introduction/knockoutjs-template
msc.type: authoredcontent
ms.openlocfilehash: 3a551db1caa9636eb7f2e04c287d3ef371263584
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78467318"
---
# <a name="single-page-application-knockoutjs-template"></a>单页应用程序： KnockoutJS 模板

作者： [Mike Wasson](https://github.com/MikeWasson)

> 挖空 MVC 模板属于 ASP.NET 和 Web 工具2012。2
> 
> [下载 ASP.NET 和 Web 工具2012。2](https://go.microsoft.com/fwlink/?LinkId=282650)

ASP.NET 和 Web 工具2012.2 更新包含 ASP.NET MVC 4 的单页应用程序（SPA）模板。 此模板旨在帮助你快速开始构建交互式客户端 web 应用。

"单页应用程序（SPA）" 是 web 应用程序的常规术语，用于加载单个 HTML 页面，然后动态更新页面，而不是加载新页面。 初始页面加载后，SPA 通过 AJAX 请求与服务器进行通信。

![](knockoutjs-template/_static/image1.png)

AJAX 并非最新的内容，但现在提供了一些 JavaScript 框架，可以更轻松地构建和维护大型的 SPA 应用程序。 此外，HTML 5 和 CSS3 还可以更轻松地创建丰富的 Ui。

若要开始，SPA 模板会创建一个 "待办事项列表" 应用程序示例。 在本教程中，我们将对模板进行指导教程。 首先，我们将介绍待办事项列表应用程序，然后检查使其正常工作的技术部分。

## <a name="create-a-new-spa-template-project"></a>创建新的 SPA 模板项目

要求：

- 用于 Web 的 Visual Studio 2012 或 Visual Studio Express 2012
- ASP.NET Web Tools 2012.2 更新。 你可以在[此处](https://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=ASPDOTNETandWebTools2012_2)安装更新。

启动 Visual Studio，然后从起始页中选择 "**新建项目**"。 或者，从 "**文件**" 菜单中选择 "**新建**"，然后选择 "**项目**"。

在 "**模板**" 窗格中，选择 "**已安装模板**"，然后展开**视觉对象C#** 节点。 在 **" C#视觉对象**" 下选择 " **Web**"。 在项目模板列表中，选择 " **ASP.NET MVC 4 Web 应用程序**"。 命名项目并单击 **“确定”** 。

![](knockoutjs-template/_static/image2.png)

在 "**新建项目**" 向导中，选择 "**单页面应用程序**"。

![](knockoutjs-template/_static/image3.png)

按 F5 生成并运行该应用程序。 当应用程序首次运行时，它将显示登录屏幕。

![](knockoutjs-template/_static/image4.png)

单击 "&quot;注册&quot;" 链接并创建新用户。

![](knockoutjs-template/_static/image5.png)

登录后，应用程序将创建包含两个项的默认 Todo 列表。 您可以单击 "添加待办事项列表" 来添加新列表。

![](knockoutjs-template/_static/image6.png)

重命名列表，向列表中添加项，然后将其签出。 你还可以删除项或删除整个列表。 更改将自动保存到服务器上的数据库（此时实际上为 LocalDB，因为你是在本地运行应用程序）。

![](knockoutjs-template/_static/image7.png)

## <a name="architecture-of-the-spa-template"></a>SPA 模板的体系结构

此图显示了应用程序的主要构建基块。

![](knockoutjs-template/_static/image8.png)

在服务器端，ASP.NET MVC 提供 HTML，还处理基于窗体的身份验证。

ASP.NET Web API 处理与 ToDoLists 和 ToDoItems 相关的所有请求，包括获取、创建、更新和删除。 客户端以 JSON 格式将数据与 Web API 进行交换。

实体框架（EF）是 O/RM 层。 它在面向对象的 ASP.NET 与基础数据库之间进行协调。 数据库使用 LocalDB，但你可以在 web.config 文件中更改此项。 通常使用 LocalDB 进行本地开发，然后使用 EF code first 迁移将其部署到服务器上的 SQL 数据库。

在客户端，挖空的 node.js 库处理来自 AJAX 请求的页面更新。 挖空使用数据绑定将页面与最新数据同步。 这样，便无需编写任何代码来遍历 JSON 数据并更新 DOM。 相反，您可以将声明性特性置于 HTML 中，告诉挖空如何显示数据。

此体系结构的一个大优点是它将表示层与应用程序逻辑分离。 你可以创建 Web API 部分，而不知道网页的外观。 在客户端，您可以创建一个 "视图模型" 来表示该数据，视图模型使用 "挖空" 绑定到 HTML。 这样就可以轻松地更改 HTML，而无需更改视图模型。 （我们稍后将介绍挖空的部分。）

## <a name="models"></a>模型

在 Visual Studio 项目中，模型文件夹包含服务器端使用的模型。 （客户端也有一些模型; 我们将转到这些模型。）

![](knockoutjs-template/_static/image9.png)

**TodoItem、TodoList**

这些是实体框架 Code First 的数据库模型。 请注意，这些模型具有相互之间的属性。 `ToDoList` 包含 ToDoItems 的集合，每个 `ToDoItem` 都具有返回给其父 ToDoList 的引用。 这些属性称为 "导航属性"，它们表示 "待办事项列表" 和 "待办事项" 这一一对多关系。

`ToDoItem` 类还使用 **[ForeignKey]** 特性来指定 `ToDoListId` 是 `ToDoList` 表中的外键。 这会告知 EF 向数据库添加外键约束。

[!code-csharp[Main](knockoutjs-template/samples/sample1.cs)]

**TodoItemDto, TodoListDto**

这些类定义将发送到客户端的数据。 "DTO" 代表 "数据传输对象"。 DTO 定义如何将实体序列化为 JSON。 通常，使用 Dto 有几个原因：

- 控制要序列化的属性。 DTO 可以包含域模型中的属性的子集。 出于安全原因（隐藏敏感数据）或只是减少发送的数据量，您可以执行此操作。
- 若要更改数据形状，例如，平展更复杂的数据结构。
- 将所有业务逻辑都排除在 DTO 之外（需要分离问题）。
- 如果由于某种原因无法序列化你的域模型。 例如，在序列化对象时，循环引用可能会导致问题（请参阅[处理循环对象引用](../../../web-api/overview/formats-and-model-binding/json-and-xml-serialization.md#handling_circular_object_references)）：但使用 DTO 只是完全避免了问题。

在 SPA 模板中，Dto 包含与域模型相同的数据。 但是，它们仍然有用，因为它们避免了导航属性中的循环引用，并演示了一般 DTO 模式。

**AccountModels.cs**

此文件包含站点成员身份的模型。 `UserProfile` 类定义成员资格数据库中用户配置文件的架构。 （在这种情况下，唯一的信息是用户 ID 和用户名。）此文件中的其他模型类用于创建用户注册和登录窗体。

## <a name="entity-framework"></a>Entity Framework

SPA 模板使用 EF Code First。 在 Code First 开发中，首先在代码中定义模型，然后 EF 使用该模型来创建数据库。 你还可以将 EF 用于现有数据库（[Database First](https://msdn.microsoft.com/data/jj206878.aspx)）。

模型文件夹中的 `TodoItemContext` 类派生自**DbContext**。 此类提供模型和 EF 之间的 "粘附"。 `TodoItemContext` 包含 `ToDoItem` 集合和 `TodoList` 集合。 若要查询数据库，只需编写针对这些集合的 LINQ 查询。 例如，以下是你可以为用户 "Alice" 选择所有待办事项列表的方式：

[!code-csharp[Main](knockoutjs-template/samples/sample2.cs)]

您还可以向集合添加新项、更新项或删除集合中的项，并将所做的更改保存到数据库中。

## <a name="aspnet-web-api-controllers"></a>ASP.NET Web API 控制器

在 ASP.NET Web API 中，控制器是处理 HTTP 请求的对象。 如前所述，SPA 模板使用 Web API 来对 `ToDoList` 和 `ToDoItem` 实例启用 CRUD 操作。 控制器位于解决方案的 "控制器" 文件夹中。

![](knockoutjs-template/_static/image10.png)

- `TodoController`：处理待办事项的 HTTP 请求
- `TodoListController`：处理待办事项列表的 HTTP 请求。

这些名称很重要，因为 Web API 会将 URI 路径与控制器名称匹配。 （若要了解 Web API 如何将 HTTP 请求路由到控制器，请参阅[ASP.NET Web API 中的路由](../../../web-api/overview/web-api-routing-and-actions/routing-in-aspnet-web-api.md)。）

让我们看看 `ToDoListController` 类。 它包含单个数据成员：

[!code-csharp[Main](knockoutjs-template/samples/sample3.cs)]

如前文所述，`TodoItemContext` 用于与 EF 通信。 控制器上的方法实现 CRUD 操作。 Web API 将来自客户端的 HTTP 请求映射到控制器方法，如下所示：

| HTTP 请求 | 控制器方法 | 说明 |
| --- | --- | --- |
| GET /api/todo | `GetTodoLists` | 获取待办事项列表的集合。 |
| 获取/api/todo/*id* | `GetTodoList` | 按 ID 获取待办事项列表 |
| PUT/api/todo/*id* | `PutTodoList` | 更新待办事项列表。 |
| POST /api/todo | `PostTodoList` | 创建新的待办事项列表。 |
| 删除/api/todo/*id* | `DeleteTodoList` | 删除 TODO 列表。 |

请注意，某些操作的 Uri 包含 ID 值的占位符。 例如，若要删除 ID 为42的列表，请 `/api/todo/42`URI。

若要详细了解如何使用 Web API 进行 CRUD 操作，请参阅[创建支持 Crud 操作的 WEB api](../../../web-api/overview/older-versions/creating-a-web-api-that-supports-crud-operations.md)。 此控制器的代码非常简单。 下面是一些有趣的要点：

- `GetTodoLists` 方法使用 LINQ 查询按登录用户的 ID 来筛选结果。 这样一来，用户只会看到属于他或她的数据。 另请注意，Select 语句用于将 `ToDoList` 实例转换为 `TodoListDto` 实例。
- PUT 和 POST 方法在修改数据库之前检查模型状态。 如果**ModelState**为 false，则这些方法将返回 HTTP 400，错误请求。 在[模型验证](../../../web-api/overview/formats-and-model-binding/model-validation-in-aspnet-web-api.md)中详细了解 Web API 中的模型验证。
- 控制器类还用 **[授权]** 特性修饰。 此属性检查是否对 HTTP 请求进行身份验证。 如果请求未经过身份验证，则客户端会收到 HTTP 401 （未授权）。 [在 ASP.NET Web API 中](../../../web-api/overview/security/authentication-and-authorization-in-aspnet-web-api.md)详细了解身份验证和授权。

`TodoController` 类非常类似于 `TodoListController`。 最大的区别在于，它不定义任何 GET 方法，因为客户端将获取待办事项以及每个待办事项列表。

## <a name="mvc-controllers-and-views"></a>MVC 控制器和视图

MVC 控制器也位于解决方案的 "控制器" 文件夹中。 `HomeController` 呈现应用程序的主 HTML。 Home 控制器的视图在 Views/Home/索引中定义。 主视图呈现不同的内容，具体取决于用户是否已登录：

[!code-cshtml[Main](knockoutjs-template/samples/sample4.cshtml)]

当用户登录时，他们将看到主 UI。 否则，它们会看到登录面板。 请注意，此条件呈现在服务器端发生。 永远不要尝试隐藏客户端&#8212;上发送的敏感内容在 HTTP 响应中发送的任何内容对正在观看原始 HTTP 消息的用户可见。

## <a name="client-side-javascript-and-knockoutjs"></a>客户端 JavaScript 和挖空

现在，让我们从应用程序的服务器端转到客户端。 SPA 模板结合使用 jQuery 和挖空来创建平滑的交互式 UI。 "挖空" 是一种 JavaScript 库，使用它可以轻松地将 HTML 绑定到数据。 挖空 .js 使用名为 "ViewModel" 的模式。

- 模型为域数据（ToDo 列表和 ToDo 项）。
- 视图为 HTML 文档。
- 视图模型是包含模型数据的 JavaScript 对象。 视图模型是 UI 的代码抽象。 它不知道 HTML 表示形式。 相反，它表示视图的抽象功能，如 "待办事项列表"。

视图被数据绑定到视图模型。 视图模型的更新会自动反映在视图中。 绑定也适用于其他方向。 DOM 中的事件（如单击）被数据绑定到视图模型上的函数，这将触发 AJAX 调用。

SPA 模板将客户端 JavaScript 组织成三个层：

- todo node.js：发送 AJAX 请求。
- todo：定义模型。
- viewmodel：定义视图模型。

![](knockoutjs-template/_static/image11.png)

这些脚本文件位于解决方案的脚本/应用程序文件夹中。

![](knockoutjs-template/_static/image12.png)

**todo。 datacontext**处理对 Web API 控制器的所有 AJAX 调用。 （在 ajaxlogin 中的其他地方定义用于登录的 AJAX 调用。）

**todo。 node.js**定义待办事项列表的客户端（浏览器）模型。 有两个模型类： todoItem 和 todoList。

模型类中的许多属性都属于类型 "可观察的"。 可观察量是挖空的神奇之处。 从[挖空文档](http://knockoutjs.com/documentation/introduction.html)：可观测对象是一个 "JavaScript 对象，可通知订阅服务器的更改"。 当可观察的值更改时，挖空会更新绑定到这些可观察量的所有 HTML 元素。 例如，todoItem 具有可观察量的标题和操作属性：

[!code-javascript[Main](knockoutjs-template/samples/sample5.js)]

你还可以在代码中订阅一个可观测对象。 例如，todoItem 类订阅 "操作" 和 "title" 属性中的更改：

[!code-javascript[Main](knockoutjs-template/samples/sample6.js)]

**查看模型**

视图模型是在 viewmodel 中定义的。 视图模型是应用程序将 HTML 页面元素绑定到域数据的中心点。 在 SPA 模板中，视图模型包含 todoLists 的可观察数组。 视图模型中的以下代码告诉挖空以应用绑定：

[!code-javascript[Main](knockoutjs-template/samples/sample7.js)]

## <a name="html-and-data-binding"></a>HTML 和数据绑定

页面的主 HTML 在 Views/Home/索引中定义。 由于我们使用的是数据绑定，因此 HTML 只是实际呈现内容的模板。 挖空使用*声明性*绑定。 可以通过将 "数据绑定" 属性添加到元素，将页面元素绑定到数据。 下面是一个非常简单的示例，该示例摘自挖空文档：

[!code-html[Main](knockoutjs-template/samples/sample8.html)]

在此示例中，挖空将 **&lt;范围&gt;** 元素的内容更新为 `myItems.count()`的值。 每当此值发生更改时，挖空将更新文档。

挖空提供了许多不同的绑定类型。 下面是用于 SPA 模板的一些绑定：

- **foreach**：允许循环访问循环，并将相同的标记应用到列表中的每个项。 这用于呈现待办事项列表和待办事项。 在**foreach**中，将绑定应用于列表的元素。
- **visible**：用于切换可见性。 当集合为空时隐藏标记，或使错误消息可见。
- **值**：用于填充窗体值。
- **单击**：将 click 事件绑定到视图模型上的函数。

## <a name="anti-csrf-protection"></a>反 CSRF 防护

跨站点请求伪造（CSRF）是一种攻击，其中恶意站点将请求发送到用户当前登录到的有漏洞站点。 为了帮助防止 CSRF 攻击，ASP.NET MVC 使用了*防伪令牌*，也称为请求验证令牌。 其思路是服务器将随机生成的令牌放入网页中。 当客户端向服务器提交数据时，它必须在请求消息中包含此值。

由于存在相同的源策略，恶意页面无法读取用户的令牌，因此，防伪令牌工作正常。 （相同源策略阻止在两个不同站点上托管的文档访问彼此的内容。）

ASP.NET MVC 通过[防伪](https://msdn.microsoft.com/library/system.web.helpers.antiforgery.aspx)类和[[ValidateAntiForgeryToken]](https://msdn.microsoft.com/library/system.web.mvc.validateantiforgerytokenattribute.aspx)属性为防伪令牌提供内置支持。 目前，此功能不是内置于 Web API 中的。 但是，SPA 模板包含 Web API 的自定义实现。 此代码在 `ValidateHttpAntiForgeryTokenAttribute` 类中定义，该类位于解决方案的 "筛选器" 文件夹中。 若要详细了解 Web API 中的 CSRF，请参阅[防止跨站点请求伪造（CSRF）攻击](../../../web-api/overview/security/preventing-cross-site-request-forgery-csrf-attacks.md)。

## <a name="conclusion"></a>结束语

SPA 模板旨在帮助你快速开始编写新式交互式 web 应用程序。 它使用挖空的 node.js 库分隔数据和应用程序逻辑中的演示文稿（HTML 标记）。 但挖空不是唯一可用于创建 SPA 的 JavaScript 库。 如果要浏览一些其他选项，请查看[社区创建的 SPA 模板](../templates/index.md)。
