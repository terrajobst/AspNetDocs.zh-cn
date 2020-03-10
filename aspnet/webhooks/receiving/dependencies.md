---
uid: webhooks/receiving/dependencies
title: ASP.NET Webhook 接收方依赖项 |Microsoft Docs
author: rick-anderson
description: ASP.NET Webhook 中的接收方依赖关系和依赖关系注入。
ms.author: riande
ms.date: 01/17/2012
ms.assetid: 5125e483-c2bb-435b-8cd1-21d3499bfaaf
ms.openlocfilehash: 477b8828209d0da1d485ef883b0f99b4e1b9b5bf
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78517526"
---
# <a name="aspnet-webhooks-receiver-dependencies"></a><span data-ttu-id="844d0-103">ASP.NET Webhook 接收方依赖项</span><span class="sxs-lookup"><span data-stu-id="844d0-103">ASP.NET WebHooks receiver dependencies</span></span>

<span data-ttu-id="844d0-104">Microsoft ASP.NET Webhook 旨在考虑依赖项注入。</span><span class="sxs-lookup"><span data-stu-id="844d0-104">Microsoft ASP.NET WebHooks is designed with dependency injection in mind.</span></span> <span data-ttu-id="844d0-105">使用依赖关系注入引擎，可以将系统中的大多数依赖项替换为替代实现。</span><span class="sxs-lookup"><span data-stu-id="844d0-105">Most dependencies in the system can be replaced with alternative implementations using a dependency injection engine.</span></span>

<span data-ttu-id="844d0-106">有关接收方依赖项的列表，请参阅[DependencyScopeExtensions](https://github.com/aspnet/aspnetWebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/Extensions/DependencyScopeExtensions.cs) 。</span><span class="sxs-lookup"><span data-stu-id="844d0-106">See [DependencyScopeExtensions](https://github.com/aspnet/aspnetWebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/Extensions/DependencyScopeExtensions.cs) for a list of receiver dependencies.</span></span> <span data-ttu-id="844d0-107">如果尚未注册任何依赖项，则使用默认实现。</span><span class="sxs-lookup"><span data-stu-id="844d0-107">If no dependency has been registered, a default implementation is used.</span></span> <span data-ttu-id="844d0-108">有关默认实现的列表，请参阅[ReceiverServices](https://github.com/aspnet/aspnetWebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/Services/ReceiverServices.cs) 。</span><span class="sxs-lookup"><span data-stu-id="844d0-108">See [ReceiverServices](https://github.com/aspnet/aspnetWebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/Services/ReceiverServices.cs) for a list of default implementations.</span></span>
