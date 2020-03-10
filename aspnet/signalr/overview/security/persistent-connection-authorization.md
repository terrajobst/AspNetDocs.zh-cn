---
uid: signalr/overview/security/persistent-connection-authorization
title: SignalR 持久性连接的身份验证和授权 |Microsoft Docs
author: bradygaster
description: 本主题介绍如何在持久性连接上强制实施授权。 有关将安全性集成到 SignalR 应用程序的一般信息,。
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: e264677b-9c01-47ec-94f9-3cd8f08f94af
msc.legacyurl: /signalr/overview/security/persistent-connection-authorization
msc.type: authoredcontent
ms.openlocfilehash: 7e69d3c1a18f1239142891734ba58cd2b0078f84
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78467474"
---
# <a name="authentication-and-authorization-for-signalr-persistent-connections"></a><span data-ttu-id="fd403-104">SignalR 永久性连接身份验证和授权</span><span class="sxs-lookup"><span data-stu-id="fd403-104">Authentication and Authorization for SignalR Persistent Connections</span></span>

<span data-ttu-id="fd403-105">作者： [Fletcher](https://github.com/pfletcher)， [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="fd403-105">by [Patrick Fletcher](https://github.com/pfletcher), [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="fd403-106">本主题介绍如何在持久性连接上强制实施授权。</span><span class="sxs-lookup"><span data-stu-id="fd403-106">This topic describes how to enforce authorization on a persistent connection.</span></span> <span data-ttu-id="fd403-107">有关将安全性集成到 SignalR 应用程序的一般信息，请参阅[安全性简介](introduction-to-security.md)。</span><span class="sxs-lookup"><span data-stu-id="fd403-107">For general information about integrating security into a SignalR application, see [Introduction to Security](introduction-to-security.md).</span></span>
>
> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="fd403-108">本主题中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="fd403-108">Software versions used in this topic</span></span>
>
>
> - [<span data-ttu-id="fd403-109">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="fd403-109">Visual Studio 2013</span></span>](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - <span data-ttu-id="fd403-110">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="fd403-110">.NET 4.5</span></span>
> - <span data-ttu-id="fd403-111">SignalR 版本2</span><span class="sxs-lookup"><span data-stu-id="fd403-111">SignalR version 2</span></span>
>
>
>
> ## <a name="previous-versions-of-this-topic"></a><span data-ttu-id="fd403-112">本主题的早期版本</span><span class="sxs-lookup"><span data-stu-id="fd403-112">Previous versions of this topic</span></span>
>
> <span data-ttu-id="fd403-113">有关早期版本的 SignalR 的信息，请参阅[SignalR 旧版本](../older-versions/index.md)。</span><span class="sxs-lookup"><span data-stu-id="fd403-113">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="fd403-114">问题和注释</span><span class="sxs-lookup"><span data-stu-id="fd403-114">Questions and comments</span></span>
>
> <span data-ttu-id="fd403-115">请提供有关你喜欢本教程的方式的反馈，并在页面底部的评论中留下反馈。</span><span class="sxs-lookup"><span data-stu-id="fd403-115">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="fd403-116">如果你有与本教程不直接相关的问题，则可以将其发布到[ASP.NET SignalR 论坛](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR)或[StackOverflow.com](http://stackoverflow.com/)。</span><span class="sxs-lookup"><span data-stu-id="fd403-116">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>

## <a name="enforce-authorization"></a><span data-ttu-id="fd403-117">强制授权</span><span class="sxs-lookup"><span data-stu-id="fd403-117">Enforce authorization</span></span>

<span data-ttu-id="fd403-118">若要在使用[PersistentConnection](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.persistentconnection(v=vs.111).aspx)时强制执行授权规则，必须重写 `AuthorizeRequest` 方法。</span><span class="sxs-lookup"><span data-stu-id="fd403-118">To enforce authorization rules when using a [PersistentConnection](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.persistentconnection(v=vs.111).aspx) you must override the `AuthorizeRequest` method.</span></span> <span data-ttu-id="fd403-119">不能将 `Authorize` 特性与持久性连接一起使用。</span><span class="sxs-lookup"><span data-stu-id="fd403-119">You cannot use the `Authorize` attribute with persistent connections.</span></span> <span data-ttu-id="fd403-120">SignalR 框架在每次请求之前调用 `AuthorizeRequest` 方法，以验证用户是否有权执行请求的操作。</span><span class="sxs-lookup"><span data-stu-id="fd403-120">The `AuthorizeRequest` method is called by the SignalR Framework before every request to verify that the user is authorized to perform the requested action.</span></span> <span data-ttu-id="fd403-121">不会从客户端调用 `AuthorizeRequest` 方法;相反，你可以通过应用程序的标准身份验证机制来对用户进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="fd403-121">The `AuthorizeRequest` method is not called from the client; instead, you authenticate the user through your application's standard authentication mechanism.</span></span>

<span data-ttu-id="fd403-122">下面的示例演示如何将请求限制为已通过身份验证的用户。</span><span class="sxs-lookup"><span data-stu-id="fd403-122">The example below shows how to limit requests to authenticated users.</span></span>

[!code-csharp[Main](persistent-connection-authorization/samples/sample1.cs)]

<span data-ttu-id="fd403-123">可以在 AuthorizeRequest 方法中添加任何自定义的授权逻辑;例如，检查用户是否属于特定角色。</span><span class="sxs-lookup"><span data-stu-id="fd403-123">You can add any customized authorization logic in the AuthorizeRequest method; such as, checking whether a user belongs to a particular role.</span></span>
