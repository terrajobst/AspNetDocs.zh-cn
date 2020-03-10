---
uid: single-page-application/overview/templates/emberjs-template
title: EmberJS 模板 |Microsoft Docs
author: xqiu
description: EmberJS 模板
ms.author: riande
ms.date: 01/30/2013
ms.assetid: 04d5f142-5f62-494a-b5ea-4f3d068d34cb
msc.legacyurl: /single-page-application/overview/templates/emberjs-template
msc.type: authoredcontent
ms.openlocfilehash: 1aefa46dd0841b1b06675409cc8a09f9a218d7ac
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78467156"
---
# <a name="emberjs-template"></a>EmberJS 模板

作者： [Xinyang Qiu](https://github.com/xqiu)

> EmberJS MVC 模板由 Nathan Totten、Thiago Santos 和 Xinyang Qiu 编写。
> 
> [下载 EmberJS MVC 模板](https://go.microsoft.com/fwlink/?LinkId=282647)

EmberJS SPA 模板旨在帮助你开始使用 EmberJS 快速构建交互式客户端 web 应用。

"单页应用程序（SPA）" 是 web 应用程序的常规术语，用于加载单个 HTML 页面，然后动态更新页面，而不是加载新页面。 初始页面加载后，SPA 通过 AJAX 请求与服务器进行通信。

![](emberjs-template/_static/image1.png)

AJAX 并非最新的内容，但现在提供了一些 JavaScript 框架，可以更轻松地构建和维护大型的 SPA 应用程序。 此外，HTML 5 和 CSS3 还可以更轻松地创建丰富的 Ui。

EmberJS SPA 模板使用[Ember](http://emberjs.com/) JavaScript 库处理 AJAX 请求的页面更新。 Ember 使用数据绑定将页面与最新数据同步。 这样，便无需编写任何代码来遍历 JSON 数据并更新 DOM。 而是将声明性特性置于 HTML 中，告诉 Ember 如何显示数据。

在服务器端，EmberJS 模板与[KNOCKOUTJS SPA 模板](../introduction/knockoutjs-template.md)几乎完全相同。 它使用 ASP.NET MVC 为 HTML 文档提供服务，并 ASP.NET Web API 处理来自客户端的 AJAX 请求。 有关模板的这些方面的详细信息，请参阅[KnockoutJS 模板](../introduction/knockoutjs-template.md)文档。 本主题重点介绍挖空模板与 EmberJS 模板之间的差异。

## <a name="create-an-emberjs-spa-template-project"></a>创建 EmberJS SPA 模板项目

单击上面的 "下载" 按钮，下载并安装模板。 可能需要重启 Visual Studio。

在 "**模板**" 窗格中，选择 "**已安装模板**"，然后展开**视觉对象C#** 节点。 在 **" C#视觉对象**" 下选择 " **Web**"。 在项目模板列表中，选择 " **ASP.NET MVC 4 Web 应用程序**"。 命名项目并单击 **“确定”** 。

![](emberjs-template/_static/image2.png)

在 "**新建项目**" 向导中，选择 " **Ember SPA 项目**"。

![](emberjs-template/_static/image4.png)

## <a name="emberjs-spa-template-overview"></a>EmberJS SPA 模板概述

EmberJS 模板结合使用 jQuery、Ember、Handlebars 来创建平滑的交互式 UI。

Ember 是使用客户端 MVC 模式的 JavaScript 库。

- 用 Handlebars 模板化语言编写的*模板*描述了应用程序用户界面。 在发布模式下， [Handlebars 编译器](https://github.com/Myslik/csharp-ember-handlebars)用于捆绑和编译 Handlebars 模板。
- *模型*存储从服务器获取的应用程序数据（ToDo 列表和 todo 项）。
- *控制器*存储应用程序状态。 控制器通常将模型数据呈现给相应的模板。
- *视图*将从应用程序转换基元事件并将这些事件传递给控制器。
- *路由器*管理应用程序状态，使 url 和模板保持同步。

此外，Ember 数据库还可用于同步 JSON 对象（通过 RESTful API 从服务器获得）和客户端模型。

EmberJS SPA 模板将脚本分为八层：

- webapi\_webapi，\_序列化程序：扩展 Ember 数据库以与 ASP.NET Web API 一起使用。
- 脚本/帮助器 node.js：定义新的 Ember Handlebars 帮助程序。
- Scripts/node.js：创建应用并配置适配器和序列化程序。
- 脚本/应用/模型/\*：定义模型。
- 脚本/应用/视图/\*：定义视图。
- 脚本/应用/控制器/\*：定义控制器。
- 脚本/应用/路由、脚本/app/路由器：定义路由。
- Templates/\*：定义 handlebars 模板。

让我们更详细地了解其中一些脚本。

## <a name="models"></a>模型

这些模型是在 "脚本/应用/模型" 文件夹中定义的。 有两个模型文件： "todoItem" 和 "todoList"。

**todo。 node.js**定义待办事项列表的客户端（浏览器）模型。 有两个模型类： todoItem 和 todoList。 在 Ember 中，模型是 DS 的子类。模式. 模型可以具有属性属性：

[!code-javascript[Main](emberjs-template/samples/sample1.js)]

模型可以定义与其他模型的关系：

[!code-css[Main](emberjs-template/samples/sample2.css)]

模型可以具有绑定到其他属性的计算属性：

[!code-javascript[Main](emberjs-template/samples/sample3.js)]

模型可以具有观察程序函数，这些函数在观察到的属性更改时被调用：

[!code-javascript[Main](emberjs-template/samples/sample4.js)]

## <a name="views"></a>视图

视图在 "脚本/应用/视图" 文件夹中定义。 视图从应用程序 UI 转换事件。 事件处理程序可以回调到控制器函数，或只是直接调用数据上下文。

例如，下面的代码来自 views/TodoItemEditView。 它定义输入文本字段的事件处理。

[!code-javascript[Main](emberjs-template/samples/sample5.js)]

## <a name="controller"></a>控制器

控制器在 "脚本/应用/控制器" 文件夹中定义。 若要表示单个模型，请扩展 `Ember.ObjectController`：

[!code-javascript[Main](emberjs-template/samples/sample6.js)]

控制器还可以通过扩展 `Ember.ArrayController`来表示模型的集合。 例如，Todolistcontroller.cs 表示 `todoList` 对象的数组。 控制器按 todoList ID 降序排序：

[!code-javascript[Main](emberjs-template/samples/sample7.js)]

控制器定义名为 `addTodoList`的函数，该函数创建新的 todoList 并将其添加到数组中。 若要查看如何调用此函数，请在 Templates 文件夹中打开名为 todoListTemplate 的模板文件。 以下模板代码将按钮绑定到 `addTodoList` 函数：

[!code-html[Main](emberjs-template/samples/sample8.html)]

控制器还包含一个 `error` 属性，该属性保存一条错误消息。 下面是用于显示错误消息的模板代码（也在 todoListTemplate 中）：

[!code-html[Main](emberjs-template/samples/sample9.html)]

## <a name="routes"></a>路由

Node.js 定义要显示的路由和默认模板，设置应用程序状态，并将 Url 与路由匹配：

[!code-javascript[Main](emberjs-template/samples/sample10.js)]

TodoListRoute 通过重写 setupController 函数为 TodoListRoute 加载数据：

[!code-javascript[Main](emberjs-template/samples/sample11.js)]

Ember 使用命名约定来匹配 Url、路由名称、控制器和模板。 有关详细信息，请参阅 EmberJS 文档中的[http://emberjs.com/guides/routing/defining-your-routes/](http://emberjs.com/guides/routing/defining-your-routes/) 。

## <a name="templates"></a>模板

Templates 文件夹包含四个模板：

- hbs：在应用程序启动时呈现的默认模板。
- hbs： "/about" 路由的模板。
- hbs：根 "/" 路由的模板。
- todoList hbs： "/todo" 路由的模板。
- \_hbs：模板定义导航菜单。

应用程序模板的作用类似于母版页。 它包含页眉、页脚和 "{{输出口}}"，用于根据路由插入其他模板。 有关 Ember 中的应用程序模板的详细信息，请参阅[http://guides.emberjs.com/v1.10.0/templates/the-application-template//](http://guides.emberjs.com/v1.10.0/templates/the-application-template/)。

"/Todolist)" 模板包含两个循环表达式。 外部循环 `{{#each controller}}`，`{{#each todos}}`内循环。 下面的代码演示了一个内置 `Ember.Checkbox` 视图、一个自定义 `App.TodoItemEditView`和一个具有 `deleteTodo` 操作的链接。

[!code-html[Main](emberjs-template/samples/sample12.html)]

在 HtmlHelperExtensions 中定义的 `HtmlHelperExtensions` 类定义 helper 函数，以便在 web.config 文件中将**调试**设置为**true**时缓存和插入模板文件。 此函数从在 Views/Home/ASP.NET 中定义的 "MVC 视图文件" 中调用：

[!code-cshtml[Main](emberjs-template/samples/sample13.cshtml)]

在没有参数的情况下调用，函数将在 Templates 文件夹中呈现所有模板文件。 还可以指定子文件夹或特定的模板文件。

Web.config 中的**debug**为**false**时，应用程序将包含绑定项 "~/bundles/templates"。 此捆绑项目使用 Handlebars 编译器库添加到 BundleConfig.cs 中：

[!code-csharp[Main](emberjs-template/samples/sample14.cs)]
