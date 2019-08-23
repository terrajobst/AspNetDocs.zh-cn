---
uid: overview
title: ASP.NET 概述 |Microsoft Docs
author: rick-anderson
description: 'ASP.NET 简介: 用于创建网站、web 应用程序和 web Api 的免费框架。'
ms.assetid: 3a309468-f1ca-4e51-b9c3-536af79d7a8b
ms.author: riande
ms.date: 08/10/2019
msc.legacyurl: ''
msc.type: content
ms.openlocfilehash: 9a6d08849f09c9d7a779df64f70e8770d2af3c87
ms.sourcegitcommit: b67ffd5b2c5cff01ec4c8eb12a21f693f2e11887
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/23/2019
ms.locfileid: "69995289"
---
# <a name="aspnet-overview"></a>ASP.NET 概述

ASP.NET 是一个免费的 web 框架, 用于使用 HTML、CSS 和 JavaScript 构建强大的网站和 web 应用程序。 还可以创建 Web Api 并使用 Web 套接字等实时技术。

[ASP.NET Core](https://docs.microsoft.com/aspnet/core/)是 ASP.NET 的一种替代方法。  请参阅有关[如何在 ASP.NET 与 ASP.NET Core 之间进行选择的指南](https://docs.microsoft.com/aspnet/core/choose-aspnet-framework)。

## <a name="get-started"></a>入门

安装[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)社区版, 适用于 Windows 上的 ASP.NET 的免费 IDE。

## <a name="websites-and-web-applications"></a>网站和 web 应用程序

 ASP.NET 提供了三个用于创建 web 应用程序的框架:Web 窗体、ASP.NET MVC 和 ASP.NET 网页。 所有这三个框架都是稳定且成熟的, 你可以用其中任何一个框架创建优秀的 web 应用程序。 无论选择何种框架, 都可以在任何位置获得 ASP.NET 的所有优点和功能。

每个框架都以不同的开发样式为目标。 选择哪一种取决于编程资产的组合 (知识、技能和开发经验)、要创建的应用程序类型, 以及你熟悉的开发方法。

下面是每个框架的概述, 以及如何在它们之间进行选择的一些建议。 如果你更喜欢视频简介, 请参阅[使用 ASP.NET 生成网站](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/Making-Websites-with-ASPNET)和[什么是 Web 工具？](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/what-is-web-tools)

|   | 如果你有经验 | 开发样式 | 专业知识 |
|-----------|----------------------|-----------------------------------------------------|----------------|
| Web Forms — Web 窗体 | Win 窗体, WPF, .NET | 使用封装 HTML 标记的丰富控件库进行快速开发 | 中级、高级 RAD |
| MVC       | Ruby on Rails, .NET  | 完全控制 HTML 标记、代码和标记的分隔, 并易于编写测试。 适用于移动和单页应用程序 (SPA) 的最佳选择。 | 中级、高级 |
| 网页  | 经典 ASP, PHP     | 同一文件中的 HTML 标记和代码 | 新的中级 |

### <a name="web-forms"></a>Web Forms — Web 窗体

使用 ASP.NET Web 窗体, 可以使用熟悉的拖放事件驱动模型构建动态网站。 使用设计图面和数百个控件和组件, 您可以使用数据访问快速构建功能强大、功能强大的 UI 驱动站点。

[了解有关 Web 窗体的详细信息](web-forms/index.md)

### <a name="mvc"></a>MVC

ASP.NET MVC 为你提供了一种功能强大的、基于模式的方法来构建动态网站, 使你能够轻松地分离问题并为你提供对标记的完全控制, 以实现愉快的敏捷开发。 ASP.NET MVC 包含许多功能, 可用于创建使用最新 web 标准的复杂应用程序的快速、TDD 友好的开发。

[了解有关 MVC 的详细信息](mvc/index.md)

### <a name="aspnet-web-pages"></a>ASP.NET 网页

ASP.NET 网页和 Razor 语法提供一种将服务器代码与 HTML 组合在一起以创建动态 Web 内容的快速、易学的简便方法。 连接到数据库, 添加视频, 链接到社交网络网站, 并提供更多的功能, 可帮助您创建符合最新 web 标准的精美站点。

[详细了解网页](web-pages/index.md)

### <a name="notes-about-web-forms-mvc-and-web-pages"></a>有关 Web 窗体、MVC 和网页的注释

所有三个 ASP.NET 框架都基于 .NET 和 ASP.NET 的 .NET Framework 和共享核心功能。 例如, 所有三个框架都提供一个基于成员身份的登录安全模型, 而所有三个共享相同的功能来管理请求、处理会话等, 这是核心 ASP.NET 功能的组成部分。

此外, 三个框架并不完全独立, 而是选择不能排除使用另一个框架。 由于框架可以共存于同一个 web 应用程序中, 因此查看使用不同框架编写的应用程序的各个组件并不少见。 例如, 应用程序的面向客户的部分可能在 MVC 中进行开发以优化标记, 而数据访问和管理部分则在 Web 窗体中开发, 以利用数据控件和简单的数据访问。

## <a name="web-apis"></a>Web API

ASP.NET Web API 是一种框架, 可让你轻松地生成可访问范围广泛的客户端 (包括浏览器和移动设备) 的 HTTP 服务。 ASP.NET Web API 是用于在 .NET Framework 上生成 RESTful 应用程序的理想平台。

[详细了解 Web API](web-api/index.md)

<!-- Put first under Web API TOC:  Watch video (9 minutes) https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/services-and-aspnet -->

## <a name="real-time-technologies"></a>实时技术

ASP.NET SignalR 是 ASP.NET 开发人员的新库, 使开发实时 web 功能变得更加容易。 SignalR 允许服务器和客户端之间的双向通信。 服务器可以立即将内容推送到连接的客户端。 SignalR 支持 Web 套接字, 并回退到旧版浏览器的其他兼容技术。 SignalR 包括用于连接管理的 Api (例如, 连接和断开连接事件)、分组连接和授权。

[了解有关 SignalR 的详细信息](signalr/index.md)

<!-- Put first under SignalR TOC:  Watch video (6 minutes) https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/signalr-and-the-real-time-web -->

## <a name="mobile-apps-and-sites"></a>移动应用和站点

ASP.NET 可以使用 Web API 后端为本机移动应用程序提供支持, 还可以使用 Twitter 启动等响应式设计框架来处理移动网站。 如果要生成本机移动应用, 可以轻松创建基于 JSON 的 Web API 来处理应用的数据访问、身份验证和推送通知。 如果要构建一个响应迅速的移动站点, 则可以使用所需的任何 CSS 框架或打开的网格系统, 或使用 PhoneGap 选择一个功能强大的移动系统, 如 jQuery Mobile 或 Sencha 和出色的移动应用程序。

[了解有关移动应用和站点开发的详细信息](mobile/index.md)

<!-- Put first under mobile TOC:  Watch video (11 minutes) https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/aspnet-and-mobile -->

## <a name="single-page-applications"></a>单页应用程序

ASP.NET 单页应用程序 (SPA) 可帮助你使用 HTML 5、CSS 3 和 JavaScript 构建包含重要客户端交互的应用程序。 Visual Studio 包含一个模板, 用于使用挖空和 ASP.NET Web API 生成单页面应用程序。 除了内置的 SPA 模板以外, 还可下载社区创建的 SPA 模板。

[了解有关单页应用开发的详细信息](single-page-application/index.md)

## <a name="webhooks"></a>WebHook

Webhook 是一种轻型 HTTP 模式, 它提供了一个简单的发布/订阅模型, 用于将 Web Api 和 SaaS 服务连线在一起。 当服务中发生事件时, 会以 HTTP POST 请求的形式向注册的订阅者发送通知。 POST 请求包含有关事件的信息, 使接收方可以相应地执行操作。

Webhook 由大量服务公开, 包括 Dropbox、GitHub、Instagram、MailChimp、PayPal、时差、Trello 等。 例如, WebHook 可以指示在 Dropbox 中更改了某个文件, 或在 GitHub 中提交了代码更改, 或在 PayPal 中启动了一个付款, 或者在 Trello 中创建了一个卡。

[了解有关 Webhook 的详细信息](webhooks/index.md)

<!--
Create Deployment TOC based on https://www.asp.net/aspnet/overview/deployment
Copy deployment content map to MVC, WebForms, Web Pages, Web API sections.
Copy Web Deployment in Enterprise from WebForms to MVC
Move under ASP.NET Best practices
    What not to do in ASP.NET, and what to do instead https://review.docs.microsoft.cus/aspnet/aspnet/overview/web-development-best-practices/what-not-to-do-in-aspnet-and-what-to-do-instead
    Async and await https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/async-and-await
    Building Real World Cloud Apps with Azure https://review.docs.microsoft.com/aspnet/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/introduction
    Hands on Lab: Maintainable Azure Websites: Managing Change and Scale https://review.docs.microsoft.com/aspnet/aspnet/overview/developing-apps-with-windows-azure/maintainable-azure-websites-managing-change-and-scale

-->
