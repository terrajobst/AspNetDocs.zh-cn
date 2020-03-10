---
uid: webhooks/index
title: ASP.NET Webhook 概述 |Microsoft Docs
author: rick-anderson
description: ASP.NET Webhook 简介。
ms.author: riande
ms.date: 01/17/2012
ms.assetid: 5e2843f0-f499-448f-a712-33d4e9858321
ms.openlocfilehash: 1e21c92e950893c0ff87c63f03f4710a158441fd
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78517532"
---
# <a name="aspnet-webhooks-overview"></a>ASP.NET Webhook 概述

Webhook 是一种轻型 HTTP 模式，它提供了一个简单的发布/订阅模型，用于将 Web Api 和 SaaS 服务连线在一起。 当服务中发生事件时，会以 HTTP POST 请求的形式向注册的订阅者发送通知。 POST 请求包含有关事件的信息，使接收方可以相应地执行操作。

由于其简易性，Webhook 已由大量服务公开，包括[Dropbox](http://dropbox.com/)、 [GitHub](https://www.github.com/)、 [Bitbucket](https://bitbucket.org/)、 [MailChimp](http://www.mailchimp.com/)、 [PayPal](http://www.paypal.com/)、[时差](http://www.slack.com)、[磁条](http://www.stripe.com)、 [Trello](http://www.trello.com/)等。 例如，WebHook 可以指示在[Dropbox](http://dropbox.com/)中更改了某个文件，或在 GitHub 中提交了代码更改，或在[PayPal](http://www.paypal.com/)中启动了一个付款，或者在[Trello](http://www.trello.com/)中创建了一个卡。 可能性无限！

Microsoft ASP.NET Webhook，可以更轻松地在 ASP.NET 应用程序中发送和接收 Webhook：

* 在接收端，它提供了用于从任意数量的 WebHook 提供程序接收和处理 Webhook 的通用模型。 它提供了对[Dropbox](http://dropbox.com/)、 [GitHub](https://www.github.com/)、 [Bitbucket](https://bitbucket.org/)、 [MailChimp](http://www.mailchimp.com/)、 [PayPal](http://www.paypal.com/)、 [Pusher](http://www.pusher.com)、 [Salesforce](http://www.salesforce.com)、[时差](http://www.slack.com)、[磁条](http://www.stripe.com)、 [Trello](http://www.trello.com/)、[WordPress](http://www.wordpress.com)和[Zendesk](https://www.zendesk.com/)的支持，但可以轻松地添加对更多的支持。

* 在发送端，它为管理和存储订阅提供支持，以及将事件通知发送到正确的订户集。 这允许您定义订阅者可以订阅的自己的一组事件，并在发生问题时通知他们。

这两个部分可以一起使用，也可以分离，具体取决于你的方案。 如果只需接收来自其他服务的 Webhook，则可以只使用接收方部分;如果只想要公开 Webhook 以供其他人使用，则可以执行此操作。

代码面向 ASP.NET Web API 2 和 ASP.NET MVC 5，在[GitHub 上作为 OSS](https://github.com/aspnet/WebHooks)提供。

## <a name="webhooks-overview"></a>Webhook 概述

Webhook 是一种模式，这意味着它会不同于服务间的使用方式，但基本思路是相同的。 您可以将 Webhook 视为一个简单的发布/订阅模型，在该模型中，用户可以订阅其他位置发生的事件。 事件通知作为 HTTP POST 请求传播，其中包含有关事件本身的信息。

通常，HTTP POST 请求包含由 WebHook 发送方确定的 JSON 对象或 HTML 窗体数据，其中包括有关导致 WebHook 触发 WebHook 的事件的信息。 例如， [GitHub](https://www.github.com/)发出的 WebHook POST 请求正文如下所示，这是因为在特定存储库中打开了新问题：

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

为了确保 WebHook 确实来自目标发送程序，POST 请求将以某种方式进行保护，并由接收方进行验证。 例如， [GitHub webhook](https://developer.github.com/webhooks/)包含一个*X 集线器签名*HTTP 标头，其中包含请求正文的哈希，该标头由接收方实现进行检查，因此你无需担心。

WebHook 流通常类似于：

* WebHook 发送方公开客户端可以订阅的事件。 这些事件描述了对系统的可观察的更改，例如，已插入新的数据项、进程已完成或其他内容。

* WebHook 接收方通过注册包含以下四项内容的 WebHook 进行订阅：

     1. 应以 HTTP POST 请求的形式发布事件通知的 URI;

     2. 描述应激发 WebHook 的特定事件的一组筛选器;

     3. 用于对 HTTP POST 请求进行签名的密钥;

     4. 要包含在 HTTP POST 请求中的其他数据。 例如，HTTP POST 请求正文中包含附加 HTTP 标头字段或属性。

* 事件发生后，会找到匹配的 WebHook 注册，并提交 HTTP POST 请求。 通常，如果由于某种原因而导致接收方不响应或 HTTP POST 请求导致错误响应，则会重试多次生成 HTTP POST 请求。

## <a name="webhooks-processing-pipeline"></a>Webhook 处理管道

传入 Webhook 的 Microsoft ASP.NET Webhook 处理管道如下所示：

![ASP.NET Webhook 处理管道](_static/WebHookReceivers.png)

这里有两个关键概念：*接收*方和*处理程序*：

* *接收*方负责处理来自给定发送方的 WebHook 的特定风格，并强制执行安全检查，以确保 WebHook 请求确实来自于预期的发送方。

* *处理程序*通常是用户代码运行处理特定 WebHook 的位置。

以下节点详细介绍了这些概念。
