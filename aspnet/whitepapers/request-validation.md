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
# <a name="request-validation---preventing-script-attacks"></a><span data-ttu-id="88c71-103">请求验证 - 阻止脚本攻击</span><span class="sxs-lookup"><span data-stu-id="88c71-103">Request Validation - Preventing Script Attacks</span></span>

> <span data-ttu-id="88c71-104">本文介绍了 ASP.NET 的请求验证功能，其中，默认情况下，阻止应用程序处理提交给服务器的未编码的 HTML 内容。</span><span class="sxs-lookup"><span data-stu-id="88c71-104">This paper describes the request validation feature of ASP.NET where, by default, the application is prevented from processing unencoded HTML content submitted to the server.</span></span> <span data-ttu-id="88c71-105">当应用程序设计为安全处理 HTML 数据时，可以禁用此请求验证功能。</span><span class="sxs-lookup"><span data-stu-id="88c71-105">This request validation feature can be disabled when the application has been designed to safely process HTML data.</span></span>
> 
> <span data-ttu-id="88c71-106">适用于 ASP.NET 1.1 和 ASP.NET 2.0。</span><span class="sxs-lookup"><span data-stu-id="88c71-106">Applies to ASP.NET 1.1 and ASP.NET 2.0.</span></span>

<span data-ttu-id="88c71-107">请求验证是 ASP.NET 版本 1.1 中的一项功能，可阻止服务器接受包含未编码 HTML 的内容。</span><span class="sxs-lookup"><span data-stu-id="88c71-107">Request validation, a feature of ASP.NET since version 1.1, prevents the server from accepting content containing un-encoded HTML.</span></span> <span data-ttu-id="88c71-108">此功能旨在帮助阻止某些脚本注入攻击，避免在不知情的情况下将客户端脚本代码或 HTML提交到服务器，然后将其存储并提供给其他用户。</span><span class="sxs-lookup"><span data-stu-id="88c71-108">This feature is designed to help prevent some script-injection attacks whereby client script code or HTML can be unknowingly submitted to a server, stored, and then presented to other users.</span></span> <span data-ttu-id="88c71-109">尽管如此，我们仍旧强烈建议验证所有输入数据和 HTML，并在适当的情况下将其编码。</span><span class="sxs-lookup"><span data-stu-id="88c71-109">We still strongly recommend that you validate all input data and HTML encode it when appropriate.</span></span>

<span data-ttu-id="88c71-110">例如，你创建了一个网页，该网页请求用户的电子邮件地址，然后将该电子邮件地址存储在数据库中。</span><span class="sxs-lookup"><span data-stu-id="88c71-110">For example, you create a Web page that requests a user's email address and then stores that email address in a database.</span></span> <span data-ttu-id="88c71-111">如果用户输入 &lt;脚本&gt;警报（"hello from SCRIPT"）&lt;/SCRIPT&gt; 而不是有效的电子邮件地址，则在显示该数据时，如果未正确编码内容，则可以执行此脚本。</span><span class="sxs-lookup"><span data-stu-id="88c71-111">If the user enters &lt;SCRIPT&gt;alert("hello from script")&lt;/SCRIPT&gt; instead of a valid email address, when that data is presented, this script can be executed if the content was not properly encoded.</span></span> <span data-ttu-id="88c71-112">ASP.NET 的请求验证功能可防止发生这种情况。</span><span class="sxs-lookup"><span data-stu-id="88c71-112">The request validation feature of ASP.NET prevents this from happening.</span></span>

## <a name="why-this-feature-is-useful"></a><span data-ttu-id="88c71-113">此功能的用途</span><span class="sxs-lookup"><span data-stu-id="88c71-113">Why this feature is useful</span></span>

<span data-ttu-id="88c71-114">很多站点并不知道它们已经公开了简单的脚本注入攻击。</span><span class="sxs-lookup"><span data-stu-id="88c71-114">Many sites are not aware that they are open to simple script injection attacks.</span></span> <span data-ttu-id="88c71-115">无论这些攻击的目的是通过显示 HTML 来 deface 站点，还是可能执行客户端脚本以将用户重定向到黑客的站点，脚本注入攻击都是 Web 开发人员必须遇到的问题。</span><span class="sxs-lookup"><span data-stu-id="88c71-115">Whether the purpose of these attacks is to deface the site by displaying HTML, or to potentially execute client script to redirect the user to a hacker's site, script injection attacks are a problem that Web developers must contend with.</span></span>

<span data-ttu-id="88c71-116">脚本注入攻击是所有 web 开发人员的顾虑，无论他们使用的是 ASP.NET、ASP 还是其他 web 开发技术。</span><span class="sxs-lookup"><span data-stu-id="88c71-116">Script injection attacks are a concern of all web developers, whether they are using ASP.NET, ASP, or other web development technologies.</span></span>

<span data-ttu-id="88c71-117">ASP.NET 请求验证功能可主动阻止服务器处理未编码的 HTML 内容，除非开发人员决定允许该内容。</span><span class="sxs-lookup"><span data-stu-id="88c71-117">The ASP.NET request validation feature proactively prevents these attacks by not allowing unencoded HTML content to be processed by the server unless the developer decides to allow that content.</span></span>

## <a name="what-to-expect-error-page"></a><span data-ttu-id="88c71-118">预期内容：错误页</span><span class="sxs-lookup"><span data-stu-id="88c71-118">What to expect: Error Page</span></span>

<span data-ttu-id="88c71-119">下面的屏幕截图显示了一些示例 ASP.NET 代码：</span><span class="sxs-lookup"><span data-stu-id="88c71-119">The screen shot below shows some sample ASP.NET code:</span></span>

![](request-validation/_static/image1.png)

<span data-ttu-id="88c71-120">运行此代码会生成一个简单的页面，使您可以在文本框中输入一些文本，单击按钮，然后在 "标签" 控件中显示文本：</span><span class="sxs-lookup"><span data-stu-id="88c71-120">Running this code results in a simple page that allows you to enter some text in the textbox, click the button, and display the text in the label control:</span></span>

![](request-validation/_static/image2.png)

<span data-ttu-id="88c71-121">然而，作为 JavaScript （如 `<script>alert("hello!")</script>` 输入和提交），我们会遇到异常：</span><span class="sxs-lookup"><span data-stu-id="88c71-121">However, were JavaScript, such as `<script>alert("hello!")</script>` to be entered and submitted we would get an exception:</span></span>

![](request-validation/_static/image3.png)

<span data-ttu-id="88c71-122">该错误消息指出 "可能存在危险的请求。检测到窗体值"，并在说明中提供了确切发生的情况以及如何更改行为的详细信息。</span><span class="sxs-lookup"><span data-stu-id="88c71-122">The error message states that a 'potentially dangerous Request.Form value was detected' and provides more details in the description as to exactly what occurred and how to change the behavior.</span></span> <span data-ttu-id="88c71-123">例如:</span><span class="sxs-lookup"><span data-stu-id="88c71-123">For example:</span></span>

<span data-ttu-id="88c71-124">请求验证检测到潜在危险的客户端输入值，并且已中止处理请求。</span><span class="sxs-lookup"><span data-stu-id="88c71-124">Request validation has detected a potentially dangerous client input value, and processing of the request has been aborted.</span></span> <span data-ttu-id="88c71-125">此值可能表示试图危害应用程序的安全性，如跨站点脚本攻击。</span><span class="sxs-lookup"><span data-stu-id="88c71-125">This value may indicate an attempt to compromise the security of your application, such as a cross-site scripting attack.</span></span> <span data-ttu-id="88c71-126">您可以通过在页指令或配置节中设置 `validateRequest=false` 来禁用请求验证。</span><span class="sxs-lookup"><span data-stu-id="88c71-126">You can disable request validation by setting `validateRequest=false` in the Page directive or in the configuration section.</span></span> <span data-ttu-id="88c71-127">不过，强烈建议您的应用程序在这种情况下显式检查所有输入。</span><span class="sxs-lookup"><span data-stu-id="88c71-127">However, it is strongly recommended that your application explicitly check all inputs in this case.</span></span>

## <a name="disabling-request-validation-on-a-page"></a><span data-ttu-id="88c71-128">在页面上禁用请求验证</span><span class="sxs-lookup"><span data-stu-id="88c71-128">Disabling request validation on a page</span></span>

<span data-ttu-id="88c71-129">若要在页面上禁用请求验证，必须将 Page 指令的 `validateRequest` 属性设置为 `false`：</span><span class="sxs-lookup"><span data-stu-id="88c71-129">To disable request validation on a page you must set the `validateRequest` attribute of the Page directive to `false`:</span></span>

[!code-aspx[Main](request-validation/samples/sample1.aspx)]

> [!CAUTION]
> <span data-ttu-id="88c71-130">禁用请求验证后，可以将内容提交到页面;页面开发人员负责确保内容经过正确编码或处理。</span><span class="sxs-lookup"><span data-stu-id="88c71-130">When request validation is disabled, content can be submitted to a page; it is the responsibility of the page developer to ensure that content is properly encoded or processed.</span></span>

## <a name="disabling-request-validation-for-your-application"></a><span data-ttu-id="88c71-131">禁用应用程序的请求验证</span><span class="sxs-lookup"><span data-stu-id="88c71-131">Disabling request validation for your application</span></span>

<span data-ttu-id="88c71-132">若要对应用程序禁用请求验证，必须修改或创建应用程序的 web.config 文件，并将 `<pages />` 部分的 validateRequest 属性设置为 `false`：</span><span class="sxs-lookup"><span data-stu-id="88c71-132">To disable request validation for your application, you must modify or create a Web.config file for your application and set the validateRequest attribute of the `<pages />` section to `false`:</span></span>

[!code-xml[Main](request-validation/samples/sample2.xml)]

<span data-ttu-id="88c71-133">如果要对服务器上的所有应用程序禁用请求验证，则可以对 Machine.config 文件进行此修改。</span><span class="sxs-lookup"><span data-stu-id="88c71-133">If you wish to disable request validation for all applications on your server, you can make this modification to your Machine.config file.</span></span>

> [!CAUTION]
> <span data-ttu-id="88c71-134">禁用请求验证后，可以将内容提交到应用程序;应用程序开发人员负责确保内容经过正确编码或处理。</span><span class="sxs-lookup"><span data-stu-id="88c71-134">When request validation is disabled, content can be submitted to your application; it is the responsibility of the application developer to ensure that content is properly encoded or processed.</span></span>

<span data-ttu-id="88c71-135">修改下面的代码以关闭请求验证：</span><span class="sxs-lookup"><span data-stu-id="88c71-135">The code below is modified to turn off request validation:</span></span>

![](request-validation/_static/image4.png)

<span data-ttu-id="88c71-136">现在，如果在文本框中输入了以下 JavaScript `<script>alert("hello!")</script>` 则结果为：</span><span class="sxs-lookup"><span data-stu-id="88c71-136">Now if the following JavaScript was entered into the textbox `<script>alert("hello!")</script>` the result would be:</span></span>

![](request-validation/_static/image5.png)

<span data-ttu-id="88c71-137">为了防止发生这种情况，在请求验证关闭的情况下，我们需要对内容进行 HTML 编码。</span><span class="sxs-lookup"><span data-stu-id="88c71-137">To prevent this from happening, with request validation turned off, we need to HTML encode the content.</span></span>

## <a name="how-to-html-encode-content"></a><span data-ttu-id="88c71-138">如何对内容进行 HTML 编码</span><span class="sxs-lookup"><span data-stu-id="88c71-138">How to HTML encode content</span></span>

<span data-ttu-id="88c71-139">如果已禁用请求验证，则最好对将存储的内容进行 HTML 编码，以便将来使用。</span><span class="sxs-lookup"><span data-stu-id="88c71-139">If you have disabled request validation, it is good practice to HTML-encode content that will be stored for future use.</span></span> <span data-ttu-id="88c71-140">HTML 编码会自动将所有 "&lt;" 或 "&gt;" （以及其他多个符号）替换为其对应的 HTML 编码表示形式。</span><span class="sxs-lookup"><span data-stu-id="88c71-140">HTML encoding will automatically replace any ‘&lt;' or ‘&gt;' (together with several other symbols) with their corresponding HTML encoded representation.</span></span> <span data-ttu-id="88c71-141">例如，"&lt;" 替换为 "&amp;lt;"，而 "&gt;" 替换为 "&amp;gt;"。</span><span class="sxs-lookup"><span data-stu-id="88c71-141">For example, ‘&lt;' is replaced by ‘&amp;lt;' and ‘&gt;' is replaced by ‘&amp;gt;'.</span></span> <span data-ttu-id="88c71-142">浏览器使用这些特殊代码在浏览器中显示 "&lt;" 或 "&gt;"。</span><span class="sxs-lookup"><span data-stu-id="88c71-142">Browsers use these special codes to display the ‘&lt;' or ‘&gt;' in the browser.</span></span>

<span data-ttu-id="88c71-143">使用 `Server.HtmlEncode(string)` API 可以在服务器上轻松地对内容进行 HTML 编码。</span><span class="sxs-lookup"><span data-stu-id="88c71-143">Content can be easily HTML-encoded on the server using the `Server.HtmlEncode(string)` API.</span></span> <span data-ttu-id="88c71-144">还可以轻松地对内容进行 HTML 解码，也就是说，使用 `Server.HtmlDecode(string)` 方法恢复为标准 HTML。</span><span class="sxs-lookup"><span data-stu-id="88c71-144">Content can also be easily HTML-decoded, that is, reverted back to standard HTML using the `Server.HtmlDecode(string)` method.</span></span>

![](request-validation/_static/image6.png)

<span data-ttu-id="88c71-145">导致：</span><span class="sxs-lookup"><span data-stu-id="88c71-145">Resulting in:</span></span>

![](request-validation/_static/image7.png)
