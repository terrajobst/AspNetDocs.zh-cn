---
uid: webhooks/source
title: ASP.NET Webhook 源代码和 NuGet 包 |Microsoft Docs
author: rick-anderson
description: 指向 ASP.NET Webhook 源代码和 NuGet 包的链接
ms.author: riande
ms.date: 01/17/2012
ms.assetid: 91a62bfa-ea3a-41f9-a2e1-e90d2c8fc8ca
ms.openlocfilehash: 8d07848754d9efda9c893b8ba54ac6d0c0214a53
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78513908"
---
# <a name="aspnet-webhooks-source-code-and-nuget-packages"></a><span data-ttu-id="452f3-103">ASP.NET Webhook 源代码和 NuGet 包</span><span class="sxs-lookup"><span data-stu-id="452f3-103">ASP.NET WebHooks source code and NuGet packages</span></span>

<span data-ttu-id="452f3-104">Microsoft ASP.NET Webhook 是模块 Microsoft ASP.NET 系列的一部分，并作为[开源项目托管在 GitHub 上](https://github.com/aspnet/WebHooks)。</span><span class="sxs-lookup"><span data-stu-id="452f3-104">Microsoft ASP.NET WebHooks is part of the Microsoft ASP.NET family of modules and is hosted as an [Open Source Project on GitHub](https://github.com/aspnet/WebHooks).</span></span> <span data-ttu-id="452f3-105">这意味着我们接受发布内容，但在提交拉取请求之前，请查看[贡献原则](https://github.com/aspnet/Home/blob/master/CONTRIBUTING.md)。</span><span class="sxs-lookup"><span data-stu-id="452f3-105">This means that we accept contributions, but please look at the [Contribution Guidelines](https://github.com/aspnet/Home/blob/master/CONTRIBUTING.md) before submitting a pull request.</span></span>

<span data-ttu-id="452f3-106">你现在正在阅读的这一联机文档也作为[开源在 GitHub 上](http://docs.asp.net/en/latest/contribute/style-guide.html#style-guide)托管，还接受发布内容。</span><span class="sxs-lookup"><span data-stu-id="452f3-106">This online documentation which you are reading now is also hosted as [Open Source on GitHub](http://docs.asp.net/en/latest/contribute/style-guide.html#style-guide) and also accepts contributions.</span></span>

## <a name="nuget-packages"></a><span data-ttu-id="452f3-107">NuGet 包</span><span class="sxs-lookup"><span data-stu-id="452f3-107">NuGet packages</span></span>

<span data-ttu-id="452f3-108">[NuGet 包](https://nuget.org/packages?q=Microsoft.AspNet.WebHooks)分为三个部分：</span><span class="sxs-lookup"><span data-stu-id="452f3-108">The [NuGet packages](https://nuget.org/packages?q=Microsoft.AspNet.WebHooks) are divided into three parts:</span></span>

* <span data-ttu-id="452f3-109">[常见](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Common)：发送方和接收方之间共享的公用包。</span><span class="sxs-lookup"><span data-stu-id="452f3-109">[Common](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Common): A common package that is shared between senders and receivers.</span></span>

* <span data-ttu-id="452f3-110">[发件人](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Custom)：一组支持将您自己的 webhook 发送给其他人的包。</span><span class="sxs-lookup"><span data-stu-id="452f3-110">[Sender](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Custom): A set of packages supporting sending your own WebHooks to others.</span></span> <span data-ttu-id="452f3-111">[发送 webhook](sending/senders.md)中更详细地介绍了发送 webhook 的功能。</span><span class="sxs-lookup"><span data-stu-id="452f3-111">The functionality for sending WebHooks is described in more detail in [Sending WebHooks](sending/senders.md).</span></span>

* <span data-ttu-id="452f3-112">[接收](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers)方：一组支持从其他人接收 webhook 的包。</span><span class="sxs-lookup"><span data-stu-id="452f3-112">[Receivers](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers): A set of packages supporting receiving WebHooks from others.</span></span> <span data-ttu-id="452f3-113">[接收 webhook](receiving/index.md)中更详细地介绍了接收 webhook 的功能。</span><span class="sxs-lookup"><span data-stu-id="452f3-113">The functionality for receiving WebHooks is described in more detail in [Receiving WebHooks](receiving/index.md).</span></span>
