---
uid: mvc/overview/older-versions-1/security/preventing-javascript-injection-attacks-cs
title: 阻止 JavaScript 注入攻击（C#） |Microsoft Docs
author: StephenWalther
description: 阻止 JavaScript 注入攻击和跨站点脚本攻击。 在本教程中，Stephen Walther 介绍了如何轻松地消除 。
ms.author: riande
ms.date: 08/19/2008
ms.assetid: d0136da6-81a4-4815-b002-baa84744c09e
msc.legacyurl: /mvc/overview/older-versions-1/security/preventing-javascript-injection-attacks-cs
msc.type: authoredcontent
ms.openlocfilehash: fb00ee8a7e3d678e824052060eb5d9fd5d4b6a42
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78485930"
---
# <a name="preventing-javascript-injection-attacks-c"></a>阻止 JavaScript 注入攻击 (C#)

作者： [Stephen Walther](https://github.com/StephenWalther)

[下载 PDF](https://download.microsoft.com/download/8/4/8/84843d8d-1575-426c-bcb5-9d0c42e51416/ASPNET_MVC_Tutorial_06_CS.pdf)

> 阻止 JavaScript 注入攻击和跨站点脚本攻击。 在本教程中，Stephen Walther 介绍了如何通过 HTML 编码内容轻松抵御这些类型的攻击。

本教程的目的是介绍如何防止 ASP.NET MVC 应用程序中出现 JavaScript 注入攻击。 本教程讨论了用于防范 JavaScript 注入攻击网站的两种方法。 了解如何通过对显示的数据进行编码来防止 JavaScript 注入攻击。 你还将了解如何通过对你接受的数据进行编码来防止 JavaScript 注入攻击。

## <a name="what-is-a-javascript-injection-attack"></a>什么是 JavaScript 注入攻击？

只要你接受用户输入并重新显示用户输入，就会打开你的网站，并显示 JavaScript 注入攻击。 我们来看一看公开了 JavaScript 注入攻击的具体应用程序。

假设您已经创建了一个客户反馈网站（请参阅图1）。 客户可以访问该网站，并使用你的产品输入其体验的反馈。 当客户提交其反馈时，反馈页面上会重新显示反馈。

[![客户反馈网站](preventing-javascript-injection-attacks-cs/_static/image2.png)](preventing-javascript-injection-attacks-cs/_static/image1.png)

**图 01**：客户反馈网站（[单击查看全尺寸图像](preventing-javascript-injection-attacks-cs/_static/image3.png)）

客户反馈网站使用列表1中的 `controller`。 此 `controller` 包含两个名为 `Index()` 和 `Create()`的操作。

**列表1– `HomeController.cs`**

[!code-csharp[Main](preventing-javascript-injection-attacks-cs/samples/sample1.cs)]

`Index()` 方法显示 `Index` 视图。 此方法通过从数据库检索反馈（使用 LINQ to SQL 查询）将以前的所有客户反馈传递到 `Index` 视图。

`Create()` 方法创建新的反馈项并将其添加到数据库中。 客户在窗体中输入的消息将传递给 message 参数中的 `Create()` 方法。 将创建一个反馈项，并将该消息分配给反馈项的 `Message` 属性。 通过 `DataContext.SubmitChanges()` 方法调用将反馈项提交到数据库。 最后，访问者将重定向回 `Index` 视图，其中显示了所有反馈。

`Index` 视图包含在清单2中。

**列表2– `Index.aspx`**

[!code-aspx[Main](preventing-javascript-injection-attacks-cs/samples/sample2.aspx)]

`Index` 视图包含两部分。 顶部部分包含实际的客户反馈窗体。 下半部分包含用于的。每个循环遍历前面的所有客户反馈项，并显示每个反馈项的 EntryDate 和消息属性。

客户反馈网站是一个简单的网站。 遗憾的是，该网站公开了 JavaScript 注入攻击。

假设您在客户反馈窗体中输入以下文本：

[!code-html[Main](preventing-javascript-injection-attacks-cs/samples/sample3.html)]

此文本表示显示警报消息框的 JavaScript 脚本。 有人将此脚本提交到反馈窗体后，消息<em>Boo！</em>只要有人在以后访问客户反馈网站，就会出现此情况（参见图2）。

[![JavaScript 注入](preventing-javascript-injection-attacks-cs/_static/image5.png)](preventing-javascript-injection-attacks-cs/_static/image4.png)

**图 02**： JavaScript 注入（[单击以查看完全大小的映像](preventing-javascript-injection-attacks-cs/_static/image6.png)）

现在，最初对 JavaScript 注入攻击的响应可能是自傲的。 您可能认为 JavaScript 注入攻击只是一种*篡改*攻击。 你可能会相信，任何人都不能通过提交 JavaScript 注入攻击来执行任何操作。

遗憾的是，黑客可以通过将 JavaScript 注入到网站来完成一些实际工作。 你可以使用 JavaScript 注入攻击来执行跨站点脚本（XSS）攻击。 在跨站点脚本攻击中，会盗取机密用户信息，并将信息发送到其他网站。

例如，黑客可以使用 JavaScript 注入攻击来窃取其他用户的浏览器 cookie 值。 如果敏感信息（如密码、信用卡号或社会安全号码）存储在浏览器 cookie 中，则黑客可以使用 JavaScript 注入攻击来窃取此信息。 或者，如果用户在页面中包含的窗体字段中输入的敏感信息已受到 JavaScript 攻击，则黑客可以使用注入的 JavaScript 来捕获窗体数据并将其发送到另一个网站。

*请恐惧*。 认真考虑 JavaScript 注入攻击，并保护用户的机密信息。 在接下来的两个部分中，我们将介绍两种可用于阻止 ASP.NET MVC 应用程序防御 JavaScript 注入式攻击的技术。

## <a name="approach-1-html-encode-in-the-view"></a>方法 #1：视图中的 HTML 编码

阻止 JavaScript 注入攻击的一种简单方法是在视图中重新显示数据时对网站用户输入的任何数据进行 HTML 编码。 在列表3中更新的 `Index` 视图遵循此方法。

**列表 3-`Index.aspx` （HTML 编码）**

[!code-aspx[Main](preventing-javascript-injection-attacks-cs/samples/sample4.aspx)]

请注意，在显示值之前，`feedback.Message` 的值为 HTML 编码，并显示以下代码：

[!code-aspx[Main](preventing-javascript-injection-attacks-cs/samples/sample5.aspx)]

对字符串进行 HTML 编码是什么意思？ 在对字符串进行 HTML 编码时，诸如 `<` 和 `>` 之类的危险字符将替换为 HTML 实体引用，如 `&lt;` 和 `&gt;`。 因此，如果字符串 `<script>alert("Boo!")</script>` 是 HTML 编码的，则会将其转换为 `&lt;script&gt;alert(&quot;Boo!&quot;)&lt;/script&gt;`。 当浏览器解释时，已编码的字符串不再作为 JavaScript 脚本执行。 相反，你会看到图3中的无害页面。

[![失效的 JavaScript 攻击](preventing-javascript-injection-attacks-cs/_static/image8.png)](preventing-javascript-injection-attacks-cs/_static/image7.png)

**图 03**：无法通过 JavaScript 攻击（[单击查看完全大小的映像](preventing-javascript-injection-attacks-cs/_static/image9.png)）

请注意，在列表3的 `Index` 视图中，只对 `feedback.Message` 的值进行编码。 不编码 `feedback.EntryDate` 的值。 只需对用户输入的数据进行编码。 因为 EntryDate 的值是在控制器中生成的，所以无需对此值进行 HTML 编码。

## <a name="approach-2-html-encode-in-the-controller"></a>方法 #2：控制器中的 HTML 编码

当你在视图中显示数据时，你可以在将数据提交到数据库之前对数据进行 HTML 编码，而不是使用 HTML 编码数据。 此第二种方法是在列出 4 `controller` 的情况下执行的。

**列表 4-`HomeController.cs` （HTML 编码）**

[!code-csharp[Main](preventing-javascript-injection-attacks-cs/samples/sample6.cs)]

请注意，在 `Create()` 操作内将值提交到数据库之前，消息的值是 HTML 编码的。 当消息重新显示在视图中时，消息是 HTML 编码的，并且不会执行消息中注入的任何 JavaScript。

通常，您应该优先考虑本教程中介绍的第一种方法。 此第二种方法的问题是，你最终会在数据库中得到 HTML 编码数据。 换句话说，您的数据库数据更新具有有趣的字符。

为什么这很糟糕？ 如果需要在网页以外的其他内容中显示数据库数据，则会出现问题。 例如，你无法在 Windows 窗体的应用程序中轻松地显示数据。

## <a name="summary"></a>摘要

本教程的目的是心有余悸您对 JavaScript 注入攻击的目标。 本教程讨论了两种防御 JavaScript 注入式攻击的 ASP.NET MVC 应用程序的方法：可以通过 HTML 编码方式在视图中编码用户提交的数据，也可以在控制器中对用户提交的数据进行 HTML 编码。

> [!div class="step-by-step"]
> [上一页](authenticating-users-with-windows-authentication-cs.md)
> [下一页](authenticating-users-with-forms-authentication-vb.md)
