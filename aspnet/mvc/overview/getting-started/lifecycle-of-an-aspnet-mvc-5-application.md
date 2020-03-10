---
uid: mvc/overview/getting-started/lifecycle-of-an-aspnet-mvc-5-application
title: ASP.NET MVC 5 应用程序的生命周期 |Microsoft Docs
author: cephalin
description: 下载一个 ASP.NET MVC 5 应用程序生命周期的 PDF 文档。 此生命周期文档提供了 MVC 生命周期的高级视图 。
ms.author: riande
ms.date: 02/28/2014
ms.assetid: 9c1e3a75-b644-4480-8326-11300b1ec4b3
msc.legacyurl: /mvc/overview/getting-started/lifecycle-of-an-aspnet-mvc-5-application
msc.type: authoredcontent
ms.openlocfilehash: f4a9b3fb61552b070db11fba617b5627fcd71cd5
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78470324"
---
# <a name="lifecycle-of-an-aspnet-mvc-5-application"></a>ASP.NET MVC 5 应用程序的生命周期

作者： [Cephas 链接](https://github.com/cephalin)

[下载 PDF 文档](lifecycle-of-an-aspnet-mvc-5-application/_static/lifecycle-of-an-aspnet-mvc-5-application1.pdf)

你可以在此处下载一个 PDF 文档，该文档将图表显示每个 ASP.NET MVC 5 应用程序的生命周期，从接收 HTTP 请求到将 HTTP 响应发送回客户端。 它既作为一项教育工具设计的，也是 ASP.NET MVC 的新手，还可以作为对需要深入了解应用程序的特定方面的人员的参考。 PDF 文档具有以下功能：

- 相关的[HttpApplication](https://msdn.microsoft.com/library/system.web.httpapplication.aspx)阶段，可帮助你了解 MVC 在[ASP.NET 应用程序生命周期](https://msdn.microsoft.com/library/bb470252.aspx)中的集成位置。
- MVC 应用程序生命周期的高级视图，可在其中了解每个 MVC 应用程序在请求处理管道中传递的主要阶段。  
    ![](lifecycle-of-an-aspnet-mvc-5-application/_static/image1.jpg)
- 显示请求处理管道的详细信息的详细信息视图。 您可以比较高级视图和详细信息视图，查看如何将生命周期详细信息收集到各个阶段。 [下载 PDF](lifecycle-of-an-aspnet-mvc-5-application/_static/lifecycle-of-an-aspnet-mvc-5-application1.pdf)以查看更大的视图。
    ![](lifecycle-of-an-aspnet-mvc-5-application/_static/image2.jpg)
- 请求处理管道中[控制器](https://msdn.microsoft.com/library/system.web.mvc.controller.aspx)对象上所有可重写方法的位置和用途。 您可能需要重写任何一种方法，但您必须了解其在应用程序生命周期中的角色，以便您可以在适当的生命周期阶段为您所需的效果编写代码。
- 显示了如何调用每个筛选器类型（身份验证、授权、操作和结果）的放大关系图。
- 从详细信息视图中的每个兴趣点链接到有用文章或博客。

## <a name="next-steps"></a>后续步骤

此文档是否满足你的需求？ 我们非常感谢你的反馈。 如果你对应用程序中的 ASP.NET MVC 生命周期有任何疑问， [Stackoverflow](http://stackoverflow.com/help)和[ASP.NET MVC 论坛](https://forums.asp.net/1146.aspx)是要问的好地方。 请在 twitter 上关注[我](https://twitter.com/Cephas_MSFT)，以便可以在我的最新教程中获取更新。
