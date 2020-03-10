---
uid: aspnet/overview/owin-and-katana/owin-oauth-20-authorization-server
title: OWIN OAuth 2.0 授权服务器 |Microsoft Docs
author: hongyes
description: 本教程将指导你了解如何使用 OWIN OAuth 中间件实现 OAuth 2.0 授权服务器。 这是一个高级教程，仅 outlin
ms.author: riande
ms.date: 01/28/2019
ms.assetid: 20acee16-c70c-41e9-b38f-92bfcf9a4c1c
msc.legacyurl: /aspnet/overview/owin-and-katana/owin-oauth-20-authorization-server
msc.type: authoredcontent
ms.openlocfilehash: 39c78ee57f791a94af7a5fb66c3ac42d7239760f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78500234"
---
# <a name="owin-oauth-20-authorization-server"></a><span data-ttu-id="5511a-104">OWIN OAuth 2.0 授权服务器</span><span class="sxs-lookup"><span data-stu-id="5511a-104">OWIN OAuth 2.0 Authorization Server</span></span>

<span data-ttu-id="5511a-105">使用[OAuth 2.0 framework](http://tools.ietf.org/html/rfc6749) ，第三方应用可以获得对 HTTP 服务的有限访问权限。</span><span class="sxs-lookup"><span data-stu-id="5511a-105">The [OAuth 2.0 framework](http://tools.ietf.org/html/rfc6749) enables a third-party app to obtain limited access to an HTTP service.</span></span> <span data-ttu-id="5511a-106">客户端不使用资源所有者的凭据来访问受保护的资源，而是获取一个访问令牌（表示特定范围、生存期和其他访问属性的字符串）。</span><span class="sxs-lookup"><span data-stu-id="5511a-106">Instead of using the resource owner's credentials to access a protected resource, the client obtains an access token (which is a string denoting a specific scope, lifetime, and other access attributes).</span></span> <span data-ttu-id="5511a-107">授权服务器将访问令牌颁发给第三方客户端，并批准资源所有者。</span><span class="sxs-lookup"><span data-stu-id="5511a-107">Access tokens are issued to third-party clients by an authorization server with the approval of the resource owner.</span></span>

<span data-ttu-id="5511a-108">OWIN 定义 .NET web 服务器和 web 应用程序之间的标准接口。</span><span class="sxs-lookup"><span data-stu-id="5511a-108">OWIN defines a standard interface between .NET web servers and web applications.</span></span> <span data-ttu-id="5511a-109">OWIN 接口的目标是将服务器和应用程序分离，鼓励开发简单的 .NET web 开发模块，并通过作为开放标准来鼓励 .NET web 开发工具的开源生态系统。</span><span class="sxs-lookup"><span data-stu-id="5511a-109">The goal of the OWIN interface is to decouple server and application, encourage the development of simple modules for .NET web development, and, by being an open standard, stimulate the open source ecosystem of .NET web development tools.</span></span>

<span data-ttu-id="5511a-110">有关详细信息，请参阅[OWIN](http://owin.org/)</span><span class="sxs-lookup"><span data-stu-id="5511a-110">For more information, see [OWIN](http://owin.org/)</span></span>
