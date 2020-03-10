---
uid: single-page-application/overview/templates/breezeknockout-template
title: 轻松/挖空模板 |Microsoft Docs
author: madskristensen
description: 轻松/挖空单页应用程序模板
ms.author: riande
ms.date: 01/30/2013
ms.assetid: 3bd94827-3c59-448f-abc3-36e6df4858db
msc.legacyurl: /single-page-application/overview/templates/breezeknockout-template
msc.type: authoredcontent
ms.openlocfilehash: 5bb9ee8f758a25afa6baf3ccbaf7d5864754c7df
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78449744"
---
# <a name="breezeknockout-template"></a>Breeze/Knockout 模板

作者： [Mads Kristensen](https://github.com/madskristensen)

> Ward 电铃编写了简单/挖空 MVC 模板
> 
> [下载简单/挖空 MVC 模板](https://go.microsoft.com/fwlink/?LinkId=282649)

你听说过 "单页面应用程序" （SPA），想知道它是什么。 虽然你可以阅读，但你可能会遇到这种情况。 但有时间下载示例的用户是谁？ 如果你已经有 Visual Studio，则会在60秒内使用 ASP.NET MVC 4 "轻松/挖空单页面应用程序" 模板来启动并运行 SPA。

![](http://www.breezejs.com/sites/all/images/spa-template/ZephyrRunning.png)

## <a name="what-is-the-breezeknockout-spa-template"></a>什么是简单/挖空的 SPA 模板？

大多数项目模板都会生成应用程序主干。 通过添加代码并最终传递工作应用程序，可以在这些骨骼上进行充实。 "简单/挖空的 SPA" 模板不同。 它会生成一个示例应用程序供您学习。 它演示了 SPA 应用程序设计以及用于生成 SPA 的许多技术。

"简单/挖空" 模板是 ASP.NET 和 Web 工具2012.2 更新中包含的[KNOCKOUTJS SPA 模板](../introduction/knockoutjs-template.md)的变化形式。 简单的 SPA 模板会生成一个具有相同用户体验的应用程序，但它具有不同的实现方式，可用于数据管理。

KnockoutJS SPA 模板利用原始 jQuery AJAX 进行服务请求，这些请求足以用于简单的应用程序。 但是，更复杂的应用具有更苛刻的数据管理要求。 例如，大多数应用程序：

- 在扩展用户会话过程中查询和重新查询服务器。
- 添加查询筛选器、排序和分页。
- 跨多个屏幕共享相同的数据。
- 累积对多个对象的更改，然后将其保存为单个事务。
- 验证客户端上的更改，使用户可以在将更改提交到数据库之前更正错误。

BreezeJS 库会为你处理这些事务，使你能够更重要地开发应用程序逻辑和用户体验。

简单地[**说，它是一个**](http://www.breezejs.com/?utm_source=ms-spa)开源库，用于在 JAVASCRIPT 和 HTML 中构建丰富的数据应用程序，这种应用程序一直作为独立桌面应用程序提供。

使用 "简单/挖空" 模板，你可以将第一个关键步骤用于更可靠的数据管理基础结构。 它会生成一个示例 Todo 应用程序，该应用程序的表面与 KnockoutJS SPA 模板完全相同。 在内部，它将 AJAX 数据层替换为简单的，以便您可以并排比较这两种方法。 当然，这种情况几乎只涉及到简单的应用程序。 不过，您将了解如何轻松地工作以及进行转换所需的时间。

让我们开始吧。

## <a name="create-a-breezeknockout-template-project"></a>创建简单/挖空模板项目

单击上面的 "下载" 按钮，下载并安装模板。 模板打包为 Visual Studio 扩展（VSIX）文件。 可能需要重启 Visual Studio。

在 "**模板**" 窗格中，选择 "**已安装模板**"，然后展开**视觉对象C#** 节点。 在 **" C#视觉对象**" 下选择 " **Web**"。 在项目模板列表中，选择 " **ASP.NET MVC 4 Web 应用程序**"。 命名项目并单击 **“确定”** 。

在 "**新建项目**" 向导中，选择 "**轻松挖空 SPA**"。

![](http://www.breezejs.com/sites/all/images/spa-template/SelectBreezeKOSpaTemplate.png)

按 Ctrl-F5 以生成并运行应用程序而不进行调试，或按 F5 运行调试。

![](http://www.breezejs.com/sites/all/images/spa-template/ZephyrRunning.png)

当应用程序首次运行时，它将显示登录屏幕。 单击 "注册" 链接和新页面 glides 进入 "查看"，可在其中输入用户名和密码。 （登录名和注册页是使用 ASP.NET MVC 生成的。）提交注册表单后，服务器会生成 TodoList，其中包含两个适用于你的帐户的项目。 然后，它会显示一个黄色便笺。

![](http://www.breezejs.com/sites/all/images/spa-template/TodoList.png)

现在你处于 SPA 的土地。 在客户端上，在操作 Todo 时所看到和管理的所有内容都将在客户端上呈现并管理。 以用户身份浏览应用 。 但对于开发人员而言， 使用浏览器中的开发人员工具来捕获网络流量。 （在 Internet Explorer 中：按 F12，选择 "**网络**" 选项卡，然后单击 "**开始捕获**"。）现在，请尝试以下操作：

- 添加新的 Todo 项。
- 单击标签，然后编辑 Todo 项标题
- 选中复选框可将项目标记为已完成。 请注意，textbox 处于禁用状态，因此不能再编辑标题。
- 单击标签右侧的 "x"。 该项将消失，并从数据库中删除。
- 选取另一项并清除其标题。 您将收到一个验证错误，指出标题是必需的。 短暂暂停后，将还原以前的标题。
- 键入十分长标题。 你会收到其他验证错误，指出标题太长。
- 单击 "添加待办事项列表" 按钮。 新列表将显示在上一个列表的左侧。
- 播放 TodoList 标题，触发其所需和长度的验证。
- 在标题文本框中单击以清除错误消息。
- 单击右上角圆圈中的 "x" 以删除 TodoList 及其 todo。

验证逻辑通过简单地执行客户端。 服务器模型类上的验证特性传播到客户端，并在客户端与服务器联系之前自动执行。

查看网络流量。 请注意，当出错时，没有对服务器的调用。 每个有效的更改都导致向 "/api/Todo/SaveChanges" 发出 POST 请求。 轻松绑定更改，并将其作为单个请求发送到 Web API 控制器的 `SaveChanges` 方法。 这不同于 KnockoutJS SPA 模板，后者分别对每个项发出 PUT、POST 和 DELETE 请求。

## <a name="peek-inside"></a>查看内部

此应用程序具有客户端和服务器端。 客户端堆栈包含一小部分 HTML 和应用程序 JavaScript 模块（在 "应用" 文件夹中）和第三方 JavaScript 库（在 "脚本" 文件夹中）的组合。

![](http://www.breezejs.com/sites/all/images/spa-template/ClientArchitecture.png)

如果已调查 KnockoutJS SPA 模板，这应该非常熟悉。 专注于蓝色框。 UI 体系结构是模型-视图-ViewModel （MVVM），其中，视图的 HTML 小组件与视图模型中的支持表示代码完全分离。 数据绑定系统（在本例中为挖空）协调视图和视图模型，以便每个都可以执行其作业，而无需深入了解另一个。

模型封装 Todo 数据。 模型中的实体是通过挖空的可观察属性轻松构造的，因此它们可以直接绑定到视图中的小组件。 视图模型要求数据上下文获取和保存模型实体。 数据上下文委托大部分工作。

服务器端堆栈包含某些开发人员代码和三个原则 .NET 库： Web API、实体框架和 Breeze.NET：

![](http://www.breezejs.com/sites/all/images/spa-template/ServerArchitecture.png)

基本体系结构与 KnockoutJS SPA 模板相同。 但是，实现要简单得多：删除了 Dto，并且大部分实体框架详细信息已委派给 Breeze.NET。

## <a name="next-steps"></a>后续步骤

我们建议您浏览代码，指导您在简单的网站上对客户端和服务器堆栈的[广泛讨论](http://www.breezejs.com/spa-template?utm_source=ms-spa)。

你可以尝试通过简单的客户端查询进行播放;添加一些筛选器和排序。 可以添加更多的模型属性和更多的实体，以更好地体验端到端 SPA 开发。 当你确信设计时，可以排除 Todo 功能并将其替换为你自己的功能。

不久后，你就可以开始下一个大步骤：添加客户端屏幕并在其之间导航。 你会将此 SPA 模板置于其后，并转换为一个更完整的 SPA 堆栈（如[John Papa 的](https://github.com/johnpapa/HotTowel#readme "暖色")Durandal），这会将添加到简单和挖空混合中。
