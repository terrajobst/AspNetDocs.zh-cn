---
uid: webhooks/source
title: ASP.NET Webhook 源代码和 NuGet 包 |Microsoft Docs
author: rick-anderson
description: ASP.NET Webhook 源代码和 NuGet 包的链接
ms.author: riande
ms.date: 01/17/2012
ms.assetid: 91a62bfa-ea3a-41f9-a2e1-e90d2c8fc8ca
ms.openlocfilehash: ff716b476f7dc69b6071d3febd5b5871e4f02689
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57027184"
---
# <a name="aspnet-webhooks-source-code-and-nuget-packages"></a>ASP.NET Webhook 源代码和 NuGet 包

Microsoft ASP.NET Webhook 是模块的 Microsoft ASP.NET 系列的一部分，作为托管[GitHub 上的开放源项目](https://github.com/aspnet/WebHooks)。 这意味着我们接受发布内容，但请看一下[投稿准则](https://github.com/aspnet/Home/blob/master/CONTRIBUTING.md)之前提交拉取请求。

你正在阅读此联机文档现在还作为承载[GitHub 上的开放源代码](http://docs.asp.net/en/latest/contribute/style-guide.html#style-guide)并接受发布内容。

## <a name="nuget-packages"></a>NuGet 包

[NuGet 包](https://nuget.org/packages?q=Microsoft.AspNet.WebHooks)划分为三个部分：

* [常见](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Common):发送者和接收者之间共享一个通用包。

* [发件人](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Custom):一组支持你自己的 Webhook 发送给他人的包。 中更详细地介绍了用于发送 Webhook 功能[发送 Webhook](sending/index.md)。

* [接收方](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers):一组支持从其他人接收 Webhook 的包。 中更详细地介绍了用于接收 Webhook 功能[接收 Webhook](receiving/index.md)。
