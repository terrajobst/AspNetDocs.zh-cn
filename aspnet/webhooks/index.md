---
uid: webhooks/index
title: ASP.NET Webhook 概述 |Microsoft Docs
author: rick-anderson
description: ASP.NET Webhook 简介。
ms.author: riande
ms.date: 01/17/2012
ms.assetid: 5e2843f0-f499-448f-a712-33d4e9858321
ms.openlocfilehash: 1e21c92e950893c0ff87c63f03f4710a158441fd
ms.sourcegitcommit: e365196c75ce93cd8967412b1cfdc27121816110
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/07/2020
ms.locfileid: "77075081"
---
# <a name="aspnet-webhooks-overview"></a><span data-ttu-id="eb8e6-103">ASP.NET Webhook 概述</span><span class="sxs-lookup"><span data-stu-id="eb8e6-103">ASP.NET WebHooks overview</span></span>

<span data-ttu-id="eb8e6-104">Webhook 是一种轻型 HTTP 模式，它提供了一个简单的发布/订阅模型，用于将 Web Api 和 SaaS 服务连线在一起。</span><span class="sxs-lookup"><span data-stu-id="eb8e6-104">WebHooks is a lightweight HTTP pattern providing a simple pub/sub model for wiring together Web APIs and SaaS services.</span></span> <span data-ttu-id="eb8e6-105">当服务中发生事件时，会以 HTTP POST 请求的形式向注册的订阅者发送通知。</span><span class="sxs-lookup"><span data-stu-id="eb8e6-105">When an event happens in a service, a notification is sent in the form of an HTTP POST request to registered subscribers.</span></span> <span data-ttu-id="eb8e6-106">POST 请求包含有关事件的信息，使接收方可以相应地执行操作。</span><span class="sxs-lookup"><span data-stu-id="eb8e6-106">The POST request contains information about the event which makes it possible for the receiver to act accordingly.</span></span>

<span data-ttu-id="eb8e6-107">由于其简易性，Webhook 已由大量服务公开，包括[Dropbox](http://dropbox.com/)、 [GitHub](https://www.github.com/)、 [Bitbucket](https://bitbucket.org/)、 [MailChimp](http://www.mailchimp.com/)、 [PayPal](http://www.paypal.com/)、[时差](http://www.slack.com)、[磁条](http://www.stripe.com)、 [Trello](http://www.trello.com/)等。</span><span class="sxs-lookup"><span data-stu-id="eb8e6-107">Because of their simplicity, WebHooks are already exposed by a large number of services including [Dropbox](http://dropbox.com/), [GitHub](https://www.github.com/), [Bitbucket](https://bitbucket.org/), [MailChimp](http://www.mailchimp.com/), [PayPal](http://www.paypal.com/), [Slack](http://www.slack.com), [Stripe](http://www.stripe.com), [Trello](http://www.trello.com/), and many more.</span></span> <span data-ttu-id="eb8e6-108">例如，WebHook 可以指示在[Dropbox](http://dropbox.com/)中更改了某个文件，或在 GitHub 中提交了代码更改，或在[PayPal](http://www.paypal.com/)中启动了一个付款，或者在[Trello](http://www.trello.com/)中创建了一个卡。</span><span class="sxs-lookup"><span data-stu-id="eb8e6-108">For example, a WebHook can indicate that a file has changed in [Dropbox](http://dropbox.com/), or a code change has been committed in GitHub, or a payment has been initiated in [PayPal](http://www.paypal.com/), or a card has been created in [Trello](http://www.trello.com/).</span></span> <span data-ttu-id="eb8e6-109">可能性无限！</span><span class="sxs-lookup"><span data-stu-id="eb8e6-109">The possibilities are endless!</span></span>

<span data-ttu-id="eb8e6-110">Microsoft ASP.NET Webhook，可以更轻松地在 ASP.NET 应用程序中发送和接收 Webhook：</span><span class="sxs-lookup"><span data-stu-id="eb8e6-110">Microsoft ASP.NET WebHooks makes it easier to both send and receive WebHooks as part of your ASP.NET application:</span></span>

* <span data-ttu-id="eb8e6-111">在接收端，它提供了用于从任意数量的 WebHook 提供程序接收和处理 Webhook 的通用模型。</span><span class="sxs-lookup"><span data-stu-id="eb8e6-111">On the receiving side, it provides a common model for receiving and processing WebHooks from any number of WebHook providers.</span></span> <span data-ttu-id="eb8e6-112">它提供了对[Dropbox](http://dropbox.com/)、 [GitHub](https://www.github.com/)、 [Bitbucket](https://bitbucket.org/)、 [MailChimp](http://www.mailchimp.com/)、 [PayPal](http://www.paypal.com/)、 [Pusher](http://www.pusher.com)、 [Salesforce](http://www.salesforce.com)、[时差](http://www.slack.com)、[磁条](http://www.stripe.com)、 [Trello](http://www.trello.com/)、[WordPress](http://www.wordpress.com)和[Zendesk](https://www.zendesk.com/)的支持，但可以轻松地添加对更多的支持。</span><span class="sxs-lookup"><span data-stu-id="eb8e6-112">It comes out of the box with support for [Dropbox](http://dropbox.com/), [GitHub](https://www.github.com/), [Bitbucket](https://bitbucket.org/), [MailChimp](http://www.mailchimp.com/), [PayPal](http://www.paypal.com/), [Pusher](http://www.pusher.com), [Salesforce](http://www.salesforce.com), [Slack](http://www.slack.com), [Stripe](http://www.stripe.com), [Trello](http://www.trello.com/),[WordPress](http://www.wordpress.com) and [Zendesk](https://www.zendesk.com/) but it is easy to add support for more.</span></span>

* <span data-ttu-id="eb8e6-113">在发送端，它为管理和存储订阅提供支持，以及将事件通知发送到正确的订户集。</span><span class="sxs-lookup"><span data-stu-id="eb8e6-113">On the sending side it provides support for managing and storing subscriptions as well as for sending event notifications to the right set of subscribers.</span></span> <span data-ttu-id="eb8e6-114">这允许您定义订阅者可以订阅的自己的一组事件，并在发生问题时通知他们。</span><span class="sxs-lookup"><span data-stu-id="eb8e6-114">This allows you to define your own set of events that subscribers can subscribe to and notify them when things happens.</span></span>

<span data-ttu-id="eb8e6-115">这两个部分可以一起使用，也可以分离，具体取决于你的方案。</span><span class="sxs-lookup"><span data-stu-id="eb8e6-115">The two parts can be used together or apart depending on your scenario.</span></span> <span data-ttu-id="eb8e6-116">如果只需接收来自其他服务的 Webhook，则可以只使用接收方部分;如果只想要公开 Webhook 以供其他人使用，则可以执行此操作。</span><span class="sxs-lookup"><span data-stu-id="eb8e6-116">If you only need to receive WebHooks from other services then you can use just the receiver part; if you only want to expose WebHooks for others to consume, then you can do just that.</span></span>

<span data-ttu-id="eb8e6-117">代码面向 ASP.NET Web API 2 和 ASP.NET MVC 5，在[GitHub 上作为 OSS](https://github.com/aspnet/WebHooks)提供。</span><span class="sxs-lookup"><span data-stu-id="eb8e6-117">The code targets ASP.NET Web API 2 and ASP.NET MVC 5 and is available as [OSS on GitHub](https://github.com/aspnet/WebHooks).</span></span>

## <a name="webhooks-overview"></a><span data-ttu-id="eb8e6-118">Webhook 概述</span><span class="sxs-lookup"><span data-stu-id="eb8e6-118">WebHooks Overview</span></span>

<span data-ttu-id="eb8e6-119">Webhook 是一种模式，这意味着它会不同于服务间的使用方式，但基本思路是相同的。</span><span class="sxs-lookup"><span data-stu-id="eb8e6-119">WebHooks is a pattern which means that it varies how it is used from service to service but the basic idea is the same.</span></span> <span data-ttu-id="eb8e6-120">您可以将 Webhook 视为一个简单的发布/订阅模型，在该模型中，用户可以订阅其他位置发生的事件。</span><span class="sxs-lookup"><span data-stu-id="eb8e6-120">You can think of WebHooks as a simple pub/sub model where a user can subscribe to events happening elsewhere.</span></span> <span data-ttu-id="eb8e6-121">事件通知作为 HTTP POST 请求传播，其中包含有关事件本身的信息。</span><span class="sxs-lookup"><span data-stu-id="eb8e6-121">The event notifications are propagated as HTTP POST requests containing information about the event itself.</span></span>

<span data-ttu-id="eb8e6-122">通常，HTTP POST 请求包含由 WebHook 发送方确定的 JSON 对象或 HTML 窗体数据，其中包括有关导致 WebHook 触发 WebHook 的事件的信息。</span><span class="sxs-lookup"><span data-stu-id="eb8e6-122">Typically the HTTP POST request contains a JSON object or HTML form data determined by the WebHook sender including information about the event causing the WebHook to trigger.</span></span> <span data-ttu-id="eb8e6-123">例如， [GitHub](https://www.github.com/)发出的 WebHook POST 请求正文如下所示，这是因为在特定存储库中打开了新问题：</span><span class="sxs-lookup"><span data-stu-id="eb8e6-123">For example, a WebHook POST request body from [GitHub](https://www.github.com/) looks like this as a result of a new issue being opened in a particular repository:</span></span>

```json
{
  "action": "opened",
  "issue": {
      "url": "https://api.github.com/repos/octocat/Hello-World/issues/1347",
      "number": 1347,
      ...
  },
  "repository": {
      "id": 1296269,
      "full_name": "octocat/Hello-World",
      "owner": {
          "login": "octocat",
          "id": 1
          ...
      },
      ...
  },
  "sender": {
      "login": "octocat",
      "id": 1,
      ...
  }
}
```

<span data-ttu-id="eb8e6-124">为了确保 WebHook 确实来自目标发送程序，POST 请求将以某种方式进行保护，并由接收方进行验证。</span><span class="sxs-lookup"><span data-stu-id="eb8e6-124">To ensure that the WebHook is indeed from the intended sender, the POST request is secured in some way and then verified by the receiver.</span></span> <span data-ttu-id="eb8e6-125">例如， [GitHub webhook](https://developer.github.com/webhooks/)包含一个*X 集线器签名*HTTP 标头，其中包含请求正文的哈希，该标头由接收方实现进行检查，因此你无需担心。</span><span class="sxs-lookup"><span data-stu-id="eb8e6-125">For example, [GitHub WebHooks](https://developer.github.com/webhooks/) includes an *X-Hub-Signature* HTTP header with a hash of the request body which is checked by the receiver implementation so you don't have to worry about it.</span></span>

<span data-ttu-id="eb8e6-126">WebHook 流通常类似于：</span><span class="sxs-lookup"><span data-stu-id="eb8e6-126">The WebHook flow generally goes something like this:</span></span>

* <span data-ttu-id="eb8e6-127">WebHook 发送方公开客户端可以订阅的事件。</span><span class="sxs-lookup"><span data-stu-id="eb8e6-127">The WebHook sender exposes events that a client can subscribe to.</span></span> <span data-ttu-id="eb8e6-128">这些事件描述了对系统的可观察的更改，例如，已插入新的数据项、进程已完成或其他内容。</span><span class="sxs-lookup"><span data-stu-id="eb8e6-128">The events describe observable changes to the system, for example that a new data item has been inserted, that a process has completed, or something else.</span></span>

* <span data-ttu-id="eb8e6-129">WebHook 接收方通过注册包含以下四项内容的 WebHook 进行订阅：</span><span class="sxs-lookup"><span data-stu-id="eb8e6-129">The WebHook receiver subscribes by registering a WebHook consisting of four things:</span></span>

     1. <span data-ttu-id="eb8e6-130">应以 HTTP POST 请求的形式发布事件通知的 URI;</span><span class="sxs-lookup"><span data-stu-id="eb8e6-130">A URI for where the event notification should be posted in the form of an HTTP POST request;</span></span>

     2. <span data-ttu-id="eb8e6-131">描述应激发 WebHook 的特定事件的一组筛选器;</span><span class="sxs-lookup"><span data-stu-id="eb8e6-131">A set of filters describing the particular events for which the WebHook should be fired;</span></span>

     3. <span data-ttu-id="eb8e6-132">用于对 HTTP POST 请求进行签名的密钥;</span><span class="sxs-lookup"><span data-stu-id="eb8e6-132">A secret key which is used to sign the HTTP POST request;</span></span>

     4. <span data-ttu-id="eb8e6-133">要包含在 HTTP POST 请求中的其他数据。</span><span class="sxs-lookup"><span data-stu-id="eb8e6-133">Additional data which is to be included in the HTTP POST request.</span></span> <span data-ttu-id="eb8e6-134">例如，HTTP POST 请求正文中包含附加 HTTP 标头字段或属性。</span><span class="sxs-lookup"><span data-stu-id="eb8e6-134">This can for example be additional HTTP header fields or properties included in the HTTP POST request body.</span></span>

* <span data-ttu-id="eb8e6-135">事件发生后，会找到匹配的 WebHook 注册，并提交 HTTP POST 请求。</span><span class="sxs-lookup"><span data-stu-id="eb8e6-135">Once an event happens, the matching WebHook registrations are found and HTTP POST requests are submitted.</span></span> <span data-ttu-id="eb8e6-136">通常，如果由于某种原因而导致接收方不响应或 HTTP POST 请求导致错误响应，则会重试多次生成 HTTP POST 请求。</span><span class="sxs-lookup"><span data-stu-id="eb8e6-136">Typically, the generation of the HTTP POST requests are retried several times if for some reason the recipient is not responding or the HTTP POST request results in an error response.</span></span>

## <a name="webhooks-processing-pipeline"></a><span data-ttu-id="eb8e6-137">Webhook 处理管道</span><span class="sxs-lookup"><span data-stu-id="eb8e6-137">WebHooks Processing Pipeline</span></span>

<span data-ttu-id="eb8e6-138">传入 Webhook 的 Microsoft ASP.NET Webhook 处理管道如下所示：</span><span class="sxs-lookup"><span data-stu-id="eb8e6-138">The Microsoft ASP.NET WebHooks processing pipeline for incoming WebHooks looks like this:</span></span>

![ASP.NET Webhook 处理管道](_static/WebHookReceivers.png)

<span data-ttu-id="eb8e6-140">这里有两个关键概念：*接收*方和*处理程序*：</span><span class="sxs-lookup"><span data-stu-id="eb8e6-140">The two key concepts here are *Receivers* and *Handlers*:</span></span>

* <span data-ttu-id="eb8e6-141">*接收*方负责处理来自给定发送方的 WebHook 的特定风格，并强制执行安全检查，以确保 WebHook 请求确实来自于预期的发送方。</span><span class="sxs-lookup"><span data-stu-id="eb8e6-141">*Receivers* are responsible for handling the particular flavor of WebHook from a given sender and for enforcing security checks to ensure that the WebHook request indeed is from the intended sender.</span></span>

* <span data-ttu-id="eb8e6-142">*处理程序*通常是用户代码运行处理特定 WebHook 的位置。</span><span class="sxs-lookup"><span data-stu-id="eb8e6-142">*Handlers* are typically where user code runs processing the particular WebHook.</span></span>

<span data-ttu-id="eb8e6-143">以下节点详细介绍了这些概念。</span><span class="sxs-lookup"><span data-stu-id="eb8e6-143">In the following nodes these concepts are described in more details.</span></span>
