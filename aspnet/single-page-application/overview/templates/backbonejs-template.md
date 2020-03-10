---
uid: single-page-application/overview/templates/backbonejs-template
title: 骨干模板 |Microsoft Docs
author: madskristensen
description: 骨干的 SPA SPA 模板
ms.author: riande
ms.date: 04/04/2013
ms.assetid: 00aca413-f067-4108-9bd1-cf21e64a2646
msc.legacyurl: /single-page-application/overview/templates/backbonejs-template
msc.type: authoredcontent
ms.openlocfilehash: 7297db7d5b35a53b40f9d9162960e529a167bd12
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78449774"
---
# <a name="backbone-template"></a>Backbone 模板

作者： [Mads Kristensen](https://github.com/madskristensen)

> 主干 SPA 模板由 Kazi Manzur Rashid 编写
> 
> [下载骨干 SPA 模板](https://go.microsoft.com/fwlink/?LinkId=293631)

骨干的 SPA 模板旨在让你快速开始使用骨干构建交互式客户端 web 应用[。](http://backbonejs.org/)

此模板提供了用于在 ASP.NET MVC 中开发主干 node.js 应用程序的初始主干。 它提供基本的用户登录功能，包括用户注册、登录、密码重置和具有基本电子邮件模板的用户确认。

要求：

- [ASP.NET 和 Web 工具2012.2 更新](https://go.microsoft.com/fwlink/?LinkId=282650)

## <a name="create-a-backbone-template-project"></a>创建主干模板项目

单击上面的 "下载" 按钮，下载并安装模板。 模板打包为 Visual Studio 扩展（VSIX）文件。 可能需要重启 Visual Studio。

在 "**模板**" 窗格中，选择 "**已安装模板**"，然后展开**视觉对象C#** 节点。 在 **" C#视觉对象**" 下选择 " **Web**"。 在项目模板列表中，选择 " **ASP.NET MVC 4 Web 应用程序**"。 命名项目并单击 **“确定”** 。

![](backbonejs-template/_static/image1.png)

在 "**新建项目**" 向导中，选择 "骨干 SPA 项目"。

![](backbonejs-template/_static/image2.png)

按 Ctrl-F5 以生成并运行应用程序而不进行调试，或按 F5 运行调试。

![](backbonejs-template/_static/image3.png)

单击 "我的帐户" 会打开登录页：

![](backbonejs-template/_static/image4.png)

## <a name="walkthrough-client-code"></a>演练：客户端代码

让我们从客户端开始。 客户端应用程序脚本位于 ~/Scripts/application 文件夹中。 应用程序是用[TypeScript](http://www.typescriptlang.org/) （ts 文件）编写的，这些文件编译为 JavaScript （.js 文件）。

**应用程序**

`Application` 是在 application. ts 中定义的。 此对象初始化应用程序并充当根命名空间。 它保留在应用程序之间共享的配置和状态信息，例如用户是否已登录。

`application.start` 方法创建模式视图，并为应用程序级事件附加事件处理程序，如用户登录。 接下来，它会创建默认路由器，并检查是否指定了任何客户端 URL。 如果不是，则它将重定向到默认 url （#！/）。

**事件**

开发松散耦合组件时，事件始终很重要。 应用程序通常会执行多个操作来响应用户操作。 骨干提供内置事件，其中包含模型、集合和视图等组件。 该模板使用 "发布/订阅" 模型，而不是创建这些组件之间的依赖关系，而是使用 "发布/订阅" 模型：在事件中定义的 `events` 对象充当用于发布和订阅应用程序事件的事件中心。 `events` 对象是单一实例。 下面的代码演示如何订阅事件，并触发事件：

[!code-csharp[Main](backbonejs-template/samples/sample1.cs)]

**路由器**

在主干 node.js 中，路由器提供了用于路由客户端页以及将它们连接到操作和事件的方法。 此模板定义了路由器中的单个路由器。 路由器创建 activable 视图，并在切换视图时维持状态。 （下一节介绍了 Activable 视图。）最初，该项目有两个虚拟视图： "主页" 和 "关于"。 它还具有一个 NotFound 视图，如果该路由是未知的，则会显示此视图。

**Views**

视图在 ~/Scripts/application/views. 中定义。 有两种类型的视图： activable 视图和模式对话框视图。 Activable 视图由路由器调用。 显示 activable 视图时，所有其他 activable 视图都将变为非活动状态。 若要创建 activable 视图，请使用 `Activable` 对象扩展视图：

[!code-javascript[Main](backbonejs-template/samples/sample2.js)]

通过扩展 `Activable` 向视图添加两个新方法 `activate` 和 `deactivate`。 路由器调用这些方法来激活和停用视图。

模式视图以[Twitter 启动](https://twitter.github.com/bootstrap/)模式对话框的形式实现。 `Membership` 视图和 `Profile` 视图都是模式视图。 所有应用程序事件都可以调用模型视图。 例如，在 "`Navigation`" 视图中，单击 "我的帐户" 链接将显示 "`Membership`" 视图或 "`Profile`" 视图，具体取决于用户是否已登录。 `Navigation` 将 click 事件处理程序附加到具有 `data-command` 属性的任何子元素。 HTML 标记如下所示：

[!code-html[Main](backbonejs-template/samples/sample3.html)]

下面是用于挂钩事件的导航中的代码：

[!code-csharp[Main](backbonejs-template/samples/sample4.cs)]

Models

模型在 ~/Scripts/application/models. 中定义。 这些模型都有三个基本功能：默认属性、验证规则和服务器端终结点。 下面是一个典型示例：

[!code-javascript[Main](backbonejs-template/samples/sample5.js)]

**插件**

~/Scripts/application/lib 文件夹包含几个方便的 jQuery 插件。此形式的 ts 文件定义用于处理窗体数据的插件。 通常，您需要序列化或反序列化窗体数据，并显示任何模型验证错误。 Ts 插件的方法 `serializeFields`、`deserializeFields`和 `showFieldErrors`。 下面的示例演示如何将窗体序列化到模型。

[!code-javascript[Main](backbonejs-template/samples/sample6.js)]

Flashbar 插件向用户提供各种类型的反馈消息。 方法 `$.showSuccessbar`、`$.showErrorbar` 和 `$.showInfobar`。 在后台，它使用 Twitter 启动警报显示有效果很好的消息。

尽管 API 略有不同，但 confirm 插件会替换浏览器的 "确认" 对话框：

[!code-javascript[Main](backbonejs-template/samples/sample7.js)]

## <a name="walkthrough-server-code"></a>演练：服务器代码

现在让我们看看服务器端。

**Controllers**

在单页面应用程序中，服务器仅在用户界面中扮演小型角色。 通常，服务器会呈现初始页面，然后发送和接收 JSON 数据。

模板具有两个 MVC 控制器： `HomeController` 呈现初始页面，`SupportsController` 用于确认新用户帐户和重置密码。 模板中的所有其他控制器均为发送和接收 JSON 数据 ASP.NET Web API 控制器。 默认情况下，控制器使用新的 `WebSecurity` 类来执行用户相关的任务。 但是，它们还具有可选的构造函数，可让你为这些任务传入委托。 这使测试变得更加容易，并使你可以使用 IoC 容器将 `WebSecurity` 替换为其他内容。 下面是一个示例：

[!code-csharp[Main](backbonejs-template/samples/sample8.cs)]

## <a name="views"></a>视图

视图设计为模块化：页面的每个部分都有其自己的专用视图。 在单页面应用程序中，常见的情况是包含没有任何对应控制器的视图。 您可以通过调用 `@Html.Partial('myView')`来包含视图，但这会变得枯燥乏味。 为了使此操作变得更简单，模板定义了一个帮助器方法 `IncludeClientViews`，该方法呈现指定文件夹中的所有视图：

[!code-cshtml[Main](backbonejs-template/samples/sample9.cshtml)]

如果未指定文件夹名称，则默认文件夹名称为 "ClientViews"。 如果客户端视图还使用分部视图，请使用下划线字符命名分部视图（例如 `_SignUp`）。 `IncludeClientViews` 方法排除名称以下划线开头的任何视图。 若要在客户端视图中包含分部视图，请调用 `Html.ClientView('SignUp')` 而不是 `Html.Partial('_SignUp')`。

**发送电子邮件**

若要发送电子邮件，模板需要使用[邮政](http://aboutcode.net/postal)。 不过，从代码的其余部分中提取邮政的 `IMailer` 接口，因此你可以轻松地将其替换为另一实现。 电子邮件模板位于 "视图"/"电子邮件" 文件夹中。 发件人的电子邮件地址是在 web.config 文件中的**appSettings**节的 `sender.email` 项中指定的。 此外，当在 web.config 中 `debug="true"` 时，应用程序不需要用户电子邮件确认即可加快开发速度。

## <a name="github"></a>GitHub

还可在[GitHub](https://github.com/kazimanzurrashid/AspNetMvcBackboneJsSpa)上找到主干 SPA 模板。
