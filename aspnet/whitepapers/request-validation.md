---
uid: whitepapers/request-validation
title: 请求验证-阻止脚本攻击 |Microsoft Docs
author: rick-anderson
description: 本文介绍了 ASP.NET 的请求验证功能，其中，默认情况下，阻止应用程序处理未编码的 HTML 内容 submitt 。
ms.author: riande
ms.date: 02/10/2010
ms.assetid: fa429113-5f8f-4ef4-97c5-5c04900a19fa
msc.legacyurl: /whitepapers/request-validation
msc.type: content
ms.openlocfilehash: 807cccd6fe1acdd6359b014387abd3878840d4cd
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78520580"
---
# <a name="request-validation---preventing-script-attacks"></a>请求验证 - 阻止脚本攻击

> 本文介绍了 ASP.NET 的请求验证功能，其中，默认情况下，阻止应用程序处理提交给服务器的未编码的 HTML 内容。 当应用程序设计为安全处理 HTML 数据时，可以禁用此请求验证功能。
> 
> 适用于 ASP.NET 1.1 和 ASP.NET 2.0。

请求验证是 ASP.NET 版本 1.1 中的一项功能，可阻止服务器接受包含未编码 HTML 的内容。 此功能旨在帮助阻止某些脚本注入攻击，避免在不知情的情况下将客户端脚本代码或 HTML提交到服务器，然后将其存储并提供给其他用户。 尽管如此，我们仍旧强烈建议验证所有输入数据和 HTML，并在适当的情况下将其编码。

例如，你创建了一个网页，该网页请求用户的电子邮件地址，然后将该电子邮件地址存储在数据库中。 如果用户输入 &lt;脚本&gt;警报（"hello from SCRIPT"）&lt;/SCRIPT&gt; 而不是有效的电子邮件地址，则在显示该数据时，如果未正确编码内容，则可以执行此脚本。 ASP.NET 的请求验证功能可防止发生这种情况。

## <a name="why-this-feature-is-useful"></a>此功能的用途

很多站点并不知道它们已经公开了简单的脚本注入攻击。 无论这些攻击的目的是通过显示 HTML 来 deface 站点，还是可能执行客户端脚本以将用户重定向到黑客的站点，脚本注入攻击都是 Web 开发人员必须遇到的问题。

脚本注入攻击是所有 web 开发人员的顾虑，无论他们使用的是 ASP.NET、ASP 还是其他 web 开发技术。

ASP.NET 请求验证功能可主动阻止服务器处理未编码的 HTML 内容，除非开发人员决定允许该内容。

## <a name="what-to-expect-error-page"></a>预期内容：错误页

下面的屏幕截图显示了一些示例 ASP.NET 代码：

![](request-validation/_static/image1.png)

运行此代码会生成一个简单的页面，使您可以在文本框中输入一些文本，单击按钮，然后在 "标签" 控件中显示文本：

![](request-validation/_static/image2.png)

然而，作为 JavaScript （如 `<script>alert("hello!")</script>` 输入和提交），我们会遇到异常：

![](request-validation/_static/image3.png)

该错误消息指出 "可能存在危险的请求。检测到窗体值"，并在说明中提供了确切发生的情况以及如何更改行为的详细信息。 例如:

请求验证检测到潜在危险的客户端输入值，并且已中止处理请求。 此值可能表示试图危害应用程序的安全性，如跨站点脚本攻击。 您可以通过在页指令或配置节中设置 `validateRequest=false` 来禁用请求验证。 不过，强烈建议您的应用程序在这种情况下显式检查所有输入。

## <a name="disabling-request-validation-on-a-page"></a>在页面上禁用请求验证

若要在页面上禁用请求验证，必须将 Page 指令的 `validateRequest` 属性设置为 `false`：

[!code-aspx[Main](request-validation/samples/sample1.aspx)]

> [!CAUTION]
> 禁用请求验证后，可以将内容提交到页面;页面开发人员负责确保内容经过正确编码或处理。

## <a name="disabling-request-validation-for-your-application"></a>禁用应用程序的请求验证

若要对应用程序禁用请求验证，必须修改或创建应用程序的 web.config 文件，并将 `<pages />` 部分的 validateRequest 属性设置为 `false`：

[!code-xml[Main](request-validation/samples/sample2.xml)]

如果要对服务器上的所有应用程序禁用请求验证，则可以对 Machine.config 文件进行此修改。

> [!CAUTION]
> 禁用请求验证后，可以将内容提交到应用程序;应用程序开发人员负责确保内容经过正确编码或处理。

修改下面的代码以关闭请求验证：

![](request-validation/_static/image4.png)

现在，如果在文本框中输入了以下 JavaScript `<script>alert("hello!")</script>` 则结果为：

![](request-validation/_static/image5.png)

为了防止发生这种情况，在请求验证关闭的情况下，我们需要对内容进行 HTML 编码。

## <a name="how-to-html-encode-content"></a>如何对内容进行 HTML 编码

如果已禁用请求验证，则最好对将存储的内容进行 HTML 编码，以便将来使用。 HTML 编码会自动将所有 "&lt;" 或 "&gt;" （以及其他多个符号）替换为其对应的 HTML 编码表示形式。 例如，"&lt;" 替换为 "&amp;lt;"，而 "&gt;" 替换为 "&amp;gt;"。 浏览器使用这些特殊代码在浏览器中显示 "&lt;" 或 "&gt;"。

使用 `Server.HtmlEncode(string)` API 可以在服务器上轻松地对内容进行 HTML 编码。 还可以轻松地对内容进行 HTML 解码，也就是说，使用 `Server.HtmlDecode(string)` 方法恢复为标准 HTML。

![](request-validation/_static/image6.png)

导致：

![](request-validation/_static/image7.png)
