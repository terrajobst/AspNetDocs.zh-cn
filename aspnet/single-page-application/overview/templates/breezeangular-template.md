---
uid: single-page-application/overview/templates/breezeangular-template
title: 轻松/角度模板 |Microsoft Docs
author: madskristensen
description: 轻松/角度单页面应用程序模板
ms.author: riande
ms.date: 03/08/2013
ms.assetid: db31e909-563a-4516-aadd-62aa210ac7e4
msc.legacyurl: /single-page-application/overview/templates/breezeangular-template
msc.type: authoredcontent
ms.openlocfilehash: 3e4e63d385a56d51d3d08696782b43d6228f6201
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78467186"
---
# <a name="breezeangular-template"></a>Breeze/Angular 模板

作者： [Mads Kristensen](https://github.com/madskristensen)

> Ward 电铃编写了简单/角度 MVC 模板
> 
> [下载轻松/角度 MVC 模板](https://go.microsoft.com/fwlink/?LinkId=286437)

[AngularJS](http://angularjs.org)是 Google 的开源库，用于构建单页应用程序（spa）。 它提供数据绑定、依赖关系注入和屏幕管理。 将其与[BreezeJS](http://www.breezejs.com/?utm_source=ms-spa)、用于数据建模和数据管理的另一个开源库相结合，并为强大的 HTML/JavaScript 客户端应用程序提供重要的组成部分。

"轻松/角 SPA" 模板是 ASP.NET 和 Web 工具2012.2 更新中包含的[KNOCKOUTJS SPA 模板](../introduction/knockoutjs-template.md)上的一个变体。 如果有 Visual Studio，则会在60秒内启动并运行一个示例 SPA。

![](http://www.breezejs.com/sites/all/images/spa-template/NgRunningTodoPage.png)

表面，应用程序看起来与 KnockoutJS SPA 模板非常类似。 但在这种情况下，它的差别很大。 KnockoutJS 模板对数据绑定和原始 AJAX 使用挖空以实现数据访问。 轻松/角度模板使用角度进行数据绑定，并使数据访问更加轻松。 这些库可实现其他功能，包括页面导航和历史记录。

下面是应用程序的 "关于" 页：

![](http://www.breezejs.com/sites/all/images/spa-template/NgRunningAboutPage.png)

此页显示当前用户会话期间运行的事件日志，包括：

- 分页. 请注意在 #2 和 #7 创建 Todo 控制器。
- 远程查询（#3）和本地缓存查询（#7）。
- 保存新的（#5、#6）和已修改（#4）实体。
- 已在客户端上验证更改（#9），因此用户可以在将更改提交到数据库之前更正错误。

此模板中还有更多内容可供浏览，其中包括：

- 动态加载 HTML 视图模板。
- 通过角 "指令" 自定义数据绑定。
- 模块化和依赖关系注入。
- 查询筛选器、排序、分页、预测和包含相关实体。
- 跨多个屏幕共享数据。
- 将多个更改保存为一个事务。
- 从服务器自动传播到 JavaScript 客户端的验证规则。

让我们开始吧。

## <a name="create-a-breezeangular-template-project"></a>创建一个简单的模板项目

单击上面的 "下载" 按钮，下载并安装模板。 模板打包为 Visual Studio 扩展（VSIX）文件。 可能需要重启 Visual Studio。

在 "**模板**" 窗格中，选择 "**已安装模板**"，然后展开**视觉对象C#** 节点。 在 **" C#视觉对象**" 下选择 " **Web**"。 在项目模板列表中，选择 " **ASP.NET MVC 4 Web 应用程序**"。 命名项目并单击 **“确定”** 。

在 "**新建项目**" 向导中，选择 "**轻松角 SPA**"。

![](http://www.breezejs.com/sites/all/images/spa-template/SelectBreezeNgSpaTemplate.png)

按 Ctrl-F5 以生成并运行应用程序而不进行调试，或按 F5 运行调试。

![](http://www.breezejs.com/sites/all/images/spa-template/ZephyrLogin.png)

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
- 单击右上角的 "关于" 链接可查看这些活动的日志。

验证逻辑通过简单地执行客户端。 服务器模型类上的验证特性传播到客户端，并在客户端与服务器联系之前自动执行。

查看网络流量。 请注意，当出错时，没有对服务器的调用。 每个有效的更改都导致向 "/api/Todo/SaveChanges" 发出 POST 请求。 轻松绑定更改，并将其作为单个请求发送到 Web API 控制器的 `SaveChanges` 方法。 这不同于 KnockoutJS SPA 模板，后者分别对每个项发出 PUT、POST 和 DELETE 请求。

另外，请注意，当你在 TodoList 和 About 页面之间切换时，没有任何网络流量。 这是因为该查询已被限制为本地简单缓存。

## <a name="peek-inside"></a>查看内部

此应用程序具有客户端和服务器端。 客户端堆栈包含一小部分 HTML 和应用程序 JavaScript 模块（在 "应用" 文件夹中）和第三方 JavaScript 库（在 "脚本" 文件夹中）的组合。

![](http://www.breezejs.com/sites/all/images/spa-template/NgClientArchitecture2.png)

UI 体系结构将视图的 HTML 小组件与控制器中的支持表示代码分开。 角数据绑定系统协调视图和控制器，以便每个视图和控制器都可以执行其作业，而无需对其他项进行深入了解。

控制器要求数据上下文获取并保存模型实体。 数据上下文将大部分工作委托给很多工作，这将从 JSON 查询结果构造自我跟踪模型对象。

服务器端堆栈包含某些开发人员代码和三个原则 .NET 库： Web API、实体框架和 Breeze.NET：

![](http://www.breezejs.com/sites/all/images/spa-template/ServerArchitecture.png)

基本体系结构与 KnockoutJS SPA 模板相同。 但是，实现要简单得多：删除了 Dto，并且大部分实体框架详细信息已委派给 Breeze.NET。

## <a name="next-steps"></a>后续步骤

我们建议您浏览代码，指导您在简单的网站上对客户端和服务器堆栈的[广泛讨论](http://www.breezejs.com/ng-spa-template?utm_source=ms-spa)。

你可以尝试通过简单的客户端查询进行播放;添加一些筛选器和排序。 可以添加更多的模型属性和更多的实体，以更好地体验端到端 SPA 开发。 当你确信设计时，可以排除 Todo 功能并将其替换为你自己的功能。

祝你编码愉快！
