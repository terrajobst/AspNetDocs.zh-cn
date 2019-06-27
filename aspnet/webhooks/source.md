---
uid: webhooks/source
title: ASP.NET Webhook 源代码和 NuGet 包 |Microsoft Docs
author: rick-anderson
description: ASP.NET Webhook 源代码和 NuGet 包的链接
ms.author: riande
ms.date: 01/17/2012
ms.assetid: 91a62bfa-ea3a-41f9-a2e1-e90d2c8fc8ca
ms.openlocfilehash: f88d9247f9d8aa0c5edc1ffc462be21d9319a725
ms.sourcegitcommit: dd0dc556a3d99a31d8fdbc763e9a2e53f3441b70
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/27/2019
ms.locfileid: "67410802"
---
# <a name="aspnet-webhooks-source-code-and-nuget-packages"></a><span data-ttu-id="b1995-103">ASP.NET Webhook 源代码和 NuGet 包</span><span class="sxs-lookup"><span data-stu-id="b1995-103">ASP.NET WebHooks source code and NuGet packages</span></span>

<span data-ttu-id="b1995-104">Microsoft ASP.NET Webhook 是模块的 Microsoft ASP.NET 系列的一部分，作为托管[GitHub 上的开放源项目](https://github.com/aspnet/WebHooks)。</span><span class="sxs-lookup"><span data-stu-id="b1995-104">Microsoft ASP.NET WebHooks is part of the Microsoft ASP.NET family of modules and is hosted as an [Open Source Project on GitHub](https://github.com/aspnet/WebHooks).</span></span> <span data-ttu-id="b1995-105">这意味着我们接受发布内容，但请看一下[投稿准则](https://github.com/aspnet/Home/blob/master/CONTRIBUTING.md)之前提交拉取请求。</span><span class="sxs-lookup"><span data-stu-id="b1995-105">This means that we accept contributions, but please look at the [Contribution Guidelines](https://github.com/aspnet/Home/blob/master/CONTRIBUTING.md) before submitting a pull request.</span></span>

<span data-ttu-id="b1995-106">你正在阅读此联机文档现在还作为承载[GitHub 上的开放源代码](http://docs.asp.net/en/latest/contribute/style-guide.html#style-guide)并接受发布内容。</span><span class="sxs-lookup"><span data-stu-id="b1995-106">This online documentation which you are reading now is also hosted as [Open Source on GitHub](http://docs.asp.net/en/latest/contribute/style-guide.html#style-guide) and also accepts contributions.</span></span>

## <a name="nuget-packages"></a><span data-ttu-id="b1995-107">NuGet 包</span><span class="sxs-lookup"><span data-stu-id="b1995-107">NuGet packages</span></span>

<span data-ttu-id="b1995-108">[NuGet 包](https://nuget.org/packages?q=Microsoft.AspNet.WebHooks)划分为三个部分：</span><span class="sxs-lookup"><span data-stu-id="b1995-108">The [NuGet packages](https://nuget.org/packages?q=Microsoft.AspNet.WebHooks) are divided into three parts:</span></span>

* <span data-ttu-id="b1995-109">[常见](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Common):发送者和接收者之间共享一个通用包。</span><span class="sxs-lookup"><span data-stu-id="b1995-109">[Common](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Common): A common package that is shared between senders and receivers.</span></span>

* <span data-ttu-id="b1995-110">[发件人](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Custom):一组支持你自己的 Webhook 发送给他人的包。</span><span class="sxs-lookup"><span data-stu-id="b1995-110">[Sender](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Custom): A set of packages supporting sending your own WebHooks to others.</span></span> <span data-ttu-id="b1995-111">中更详细地介绍了用于发送 Webhook 功能[发送 Webhook](sending/senders)。</span><span class="sxs-lookup"><span data-stu-id="b1995-111">The functionality for sending WebHooks is described in more detail in [Sending WebHooks](sending/senders).</span></span>

* <span data-ttu-id="b1995-112">[接收方](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers):一组支持从其他人接收 Webhook 的包。</span><span class="sxs-lookup"><span data-stu-id="b1995-112">[Receivers](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers): A set of packages supporting receiving WebHooks from others.</span></span> <span data-ttu-id="b1995-113">中更详细地介绍了用于接收 Webhook 功能[接收 Webhook](receiving/index.md)。</span><span class="sxs-lookup"><span data-stu-id="b1995-113">The functionality for receiving WebHooks is described in more detail in [Receiving WebHooks](receiving/index.md).</span></span>
