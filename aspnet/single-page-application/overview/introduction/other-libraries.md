---
uid: single-page-application/overview/introduction/other-libraries
title: 了解 Knockout 之外的库? | Microsoft Docs
author: madskristensen
description: 了解 Knockout 之外的库?
ms.author: riande
ms.date: 02/05/2013
ms.assetid: a8367c6d-ef94-4dff-a010-5eff9e6eea96
msc.legacyurl: /single-page-application/overview/introduction/other-libraries
msc.type: authoredcontent
ms.openlocfilehash: 64a4ad1fb411f7291a5cba634afdf4d2fdb16d55
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78467192"
---
# <a name="know-a-library-other-than-knockout"></a>了解 Knockout 之外的库?

作者： [Mads Kristensen](https://github.com/madskristensen)

[单页应用程序（SPA）模板](knockoutjs-template.md)是一种开始编写单页应用程序的绝佳方式。 该模板使用[KnockoutJS](http://knockoutjs.com/)将应用程序数据绑定到 DOM 元素。

但挖空不是用于创建丰富客户端应用程序的 JavaScript 库。 其他库以不同的方式解决了类似的挑战。 您可能更倾向于使用一个库，因此我们提供了多个可供下载的社区创建的模板。 其中每个模板都使用不同的客户端 JavaScript 库组合。

若要安装社区创建的模板，请访问下面列出的其中一个模板页面，然后单击 "下载" 按钮。 模板作为 VSIX 文件提供。

## <a name="backbonejs"></a>BackboneJS

[骨干作为 SPA 模板](../templates/backbonejs-template.md)。 此模板提供了用于在 ASP.NET MVC 中开发[主干 node.js](http://backbonejs.org/)应用程序的初始主干。 它提供基本的用户登录功能，包括用户注册、登录、密码重置和具有基本电子邮件模板的用户确认。

## <a name="breezejs"></a>BreezeJS

[BreezeJS](http://www.breezejs.com/?utm_source=ms-spa)是用于在 JavaScript 客户端中管理丰富数据的开源库。 轻松处理查询、缓存、更改跟踪、验证等。 两个模板功能非常简单：

- "简单[/挖空](../templates/breezeknockout-template.md)" 模板扩展了 "挖空 SPA" 模板，演示了如何轻松地生成单页面应用程序，并轻松实现数据管理和 KnockoutJS 数据绑定。
- [轻松/角度](../templates/breezeangular-template.md)模板还可以轻松扩展挖空的 SPA 模板，但使用[AngularJS](http://angularjs.org)库进行数据绑定、依赖关系注入和屏幕管理。

此外，BreezeJS 中的 "热"， [SPA 模板](../templates/hottowel-template.md)也使用。

## <a name="emberjs"></a>EmberJS

[EMBERJS SPA 模板](../templates/emberjs-template.md)。 此模板使用[Ember](http://emberjs.com/)，这是一个功能强大的 MVC JavaScript 库，可解决用于构建丰富客户端应用程序的各种挑战。

Ember SPA 模板使用 EmberJS 和 Handlebars 模板重新实现了挖空的 SPA 模板。

## <a name="hot-towel"></a>暖色

[热的 SPA SPA 模板](../templates/hottowel-template.md)。 此模板引入了多个 JavaScript 库，包括简单、挖空、RequireJS 和 Twitter 启动。

与此处列出的其他模板相比，"热输入" 模板提供了一个更完整的应用程序，您可以从中构建自己的应用程序。 还需要了解更多概念，但一旦你了解这些概念，此模板可能只是你要查找的内容。 如果要生成 SPA 但不能决定从何处开始，请使用 "热"，并在几秒钟内构建你需要的 SPA 和所有工具。

## <a name="feature-table"></a>功能表

下面是每个 SPA 模板提供的功能：

|                        | ASP.NET SPA | 主轴 | 轻松/角度 | 简单/KO |  Ember   | 暖色 |
|------------------------|-------------|----------|----------------|-----------|----------|-----------|
|      ToDo 示例       |  &#10003;   |          |    &#10003;    | &#10003;  | &#10003; |           |
|     Bare 模板      |             | &#10003; |                |           |          | &#10003;  |
| 导航和历史记录 |             | &#10003; |    &#10003;    |           | &#10003; | &#10003;  |
|        库       |             |          |                |           |          |           |
|        Angular         |             |          |    &#10003;    |           |          |           |
|    &#8195;Backbone     |             | &#10003; |                |           |          |           |
|         轻而易举         |             |          |    &#10003;    | &#10003;  |          | &#10003;  |
|        durandal        |             |          |                |           |          | &#10003;  |
|         Ember          |             |          |                |           | &#10003; |           |
|        拆装        |  &#10003;   |          |                | &#10003;  |          | &#10003;  |
