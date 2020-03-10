---
uid: web-pages/overview/getting-started/11-adding-email-to-your-web-site
title: 从 ASP.NET 网页（Razor）站点发送电子邮件 |Microsoft Docs
author: Rick-Anderson
description: 本章介绍如何从网站发送自动电子邮件。
ms.author: riande
ms.date: 02/20/2014
ms.assetid: fc49bcb9-f1a9-4048-8c3f-b60951853200
msc.legacyurl: /web-pages/overview/getting-started/11-adding-email-to-your-web-site
msc.type: authoredcontent
ms.openlocfilehash: 23e9717329525fb5a0ed505c9dc94505d4f9dbbe
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78515324"
---
# <a name="sending-email-from-an-aspnet-web-pages-razor-site"></a><span data-ttu-id="fc5e0-103">从 ASP.NET 网页（Razor）站点发送电子邮件</span><span class="sxs-lookup"><span data-stu-id="fc5e0-103">Sending Email from an ASP.NET Web Pages (Razor) Site</span></span>

<span data-ttu-id="fc5e0-104">作者： [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="fc5e0-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="fc5e0-105">本文介绍如何在使用 ASP.NET 网页（Razor）时从网站发送电子邮件。</span><span class="sxs-lookup"><span data-stu-id="fc5e0-105">This article explains how to send an email message from a website when you use ASP.NET Web Pages (Razor).</span></span>
> 
> <span data-ttu-id="fc5e0-106">学习内容：</span><span class="sxs-lookup"><span data-stu-id="fc5e0-106">What you'll learn:</span></span>
> 
> - <span data-ttu-id="fc5e0-107">如何从网站发送电子邮件。</span><span class="sxs-lookup"><span data-stu-id="fc5e0-107">How to send an email message from your website.</span></span>
> - <span data-ttu-id="fc5e0-108">如何将文件附加到电子邮件。</span><span class="sxs-lookup"><span data-stu-id="fc5e0-108">How to attach a file to an email message.</span></span>
> 
> <span data-ttu-id="fc5e0-109">这是本文中介绍的 ASP.NET 功能：</span><span class="sxs-lookup"><span data-stu-id="fc5e0-109">This is the ASP.NET feature introduced in the article:</span></span>
> 
> - <span data-ttu-id="fc5e0-110">`WebMail` 帮助程序。</span><span class="sxs-lookup"><span data-stu-id="fc5e0-110">The `WebMail` helper.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="fc5e0-111">本教程中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="fc5e0-111">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="fc5e0-112">ASP.NET 网页（Razor）3</span><span class="sxs-lookup"><span data-stu-id="fc5e0-112">ASP.NET Web Pages (Razor) 3</span></span>
>   
> 
> <span data-ttu-id="fc5e0-113">本教程还适用于 ASP.NET 网页2。</span><span class="sxs-lookup"><span data-stu-id="fc5e0-113">This tutorial also works with ASP.NET Web Pages 2.</span></span>

<a id="Sending_Email_Messages"></a>
## <a name="sending-email-messages-from-your-website"></a><span data-ttu-id="fc5e0-114">从网站发送电子邮件</span><span class="sxs-lookup"><span data-stu-id="fc5e0-114">Sending Email Messages from Your Website</span></span>

<span data-ttu-id="fc5e0-115">可能需要从网站发送电子邮件的原因有多种。</span><span class="sxs-lookup"><span data-stu-id="fc5e0-115">There are all sorts of reasons why you might need to send email from your website.</span></span> <span data-ttu-id="fc5e0-116">您可以向用户发送确认消息，也可以向自己发送通知（例如，新用户已注册。）利用 `WebMail` 帮助程序，你可以轻松地发送电子邮件。</span><span class="sxs-lookup"><span data-stu-id="fc5e0-116">You might send confirmation messages to users, or you might send notifications to yourself (for example, that a new user has registered.) The `WebMail` helper makes it easy for you to send email.</span></span>

<span data-ttu-id="fc5e0-117">若要使用 `WebMail` 帮助程序，你必须具有对 SMTP 服务器的访问权限。</span><span class="sxs-lookup"><span data-stu-id="fc5e0-117">To use the `WebMail` helper, you have to have access to an SMTP server.</span></span> <span data-ttu-id="fc5e0-118">（SMTP 代表*简单邮件传输协议*。）SMTP 服务器是一种电子邮件服务器，只向收件人的服务器&#8212;转发邮件，它是电子邮件的出站端。</span><span class="sxs-lookup"><span data-stu-id="fc5e0-118">(SMTP stands for *Simple Mail Transfer Protocol*.) An SMTP server is an email server that only forwards messages to the recipient's server &#8212; it's the outbound side of email.</span></span> <span data-ttu-id="fc5e0-119">如果你为网站使用托管提供程序，他们可能会将你设置为电子邮件，并可以告诉你你的 SMTP 服务器名称。</span><span class="sxs-lookup"><span data-stu-id="fc5e0-119">If you use a hosting provider for your website, they probably set you up with email and they can tell you what your SMTP server name is.</span></span> <span data-ttu-id="fc5e0-120">如果你在公司网络内工作，则管理员或你的 IT 部门通常可以向你显示有关你可以使用的 SMTP 服务器的信息。</span><span class="sxs-lookup"><span data-stu-id="fc5e0-120">If you're working inside a corporate network, an administrator or your IT department can usually give you the information about an SMTP server that you can use.</span></span> <span data-ttu-id="fc5e0-121">如果在家工作，您甚至可以使用普通的电子邮件提供程序进行测试，用户可以告诉您 SMTP 服务器的名称。</span><span class="sxs-lookup"><span data-stu-id="fc5e0-121">If you're working at home, you might even be able to test using your ordinary email provider, who can tell you the name of their SMTP server.</span></span> <span data-ttu-id="fc5e0-122">通常需要：</span><span class="sxs-lookup"><span data-stu-id="fc5e0-122">You typically need:</span></span>

- <span data-ttu-id="fc5e0-123">SMTP 服务器的名称。</span><span class="sxs-lookup"><span data-stu-id="fc5e0-123">The name of the SMTP server.</span></span>
- <span data-ttu-id="fc5e0-124">端口号。</span><span class="sxs-lookup"><span data-stu-id="fc5e0-124">The port number.</span></span> <span data-ttu-id="fc5e0-125">这几乎始终为25。</span><span class="sxs-lookup"><span data-stu-id="fc5e0-125">This is almost always 25.</span></span> <span data-ttu-id="fc5e0-126">但是，ISP 可能要求使用端口587。</span><span class="sxs-lookup"><span data-stu-id="fc5e0-126">However, your ISP may require you to use port 587.</span></span> <span data-ttu-id="fc5e0-127">如果为电子邮件使用安全套接字层（SSL），则可能需要不同的端口。</span><span class="sxs-lookup"><span data-stu-id="fc5e0-127">If you are using secure sockets layer (SSL) for email, you might need a different port.</span></span> <span data-ttu-id="fc5e0-128">请咨询你的电子邮件提供商。</span><span class="sxs-lookup"><span data-stu-id="fc5e0-128">Check with your email provider.</span></span>
- <span data-ttu-id="fc5e0-129">凭据（用户名和密码）。</span><span class="sxs-lookup"><span data-stu-id="fc5e0-129">Credentials (user name, password).</span></span>

<span data-ttu-id="fc5e0-130">在此过程中，您将创建两个页面。</span><span class="sxs-lookup"><span data-stu-id="fc5e0-130">In this procedure, you create two pages.</span></span> <span data-ttu-id="fc5e0-131">第一页提供了一个窗体，用户可以在其中输入说明，就好像这些用户填写了技术支持窗体一样。</span><span class="sxs-lookup"><span data-stu-id="fc5e0-131">The first page has a form that lets users enter a description, as if they were filling in a technical-support form.</span></span> <span data-ttu-id="fc5e0-132">第一页将其信息提交到第二页。</span><span class="sxs-lookup"><span data-stu-id="fc5e0-132">The first page submits its information to a second page.</span></span> <span data-ttu-id="fc5e0-133">在第二页中，代码提取用户的信息并发送一封电子邮件。</span><span class="sxs-lookup"><span data-stu-id="fc5e0-133">In the second page, code extracts the user's information and sends an email message.</span></span> <span data-ttu-id="fc5e0-134">它还会显示一条消息，确认已接收到问题报告。</span><span class="sxs-lookup"><span data-stu-id="fc5e0-134">It also displays a message confirming that the problem report has been received.</span></span>

![[图像]](11-adding-email-to-your-web-site/_static/image1.jpg)

> [!NOTE]
> <span data-ttu-id="fc5e0-136">为了使此示例简单，代码在使用它的页中初始化 `WebMail` 帮助程序。</span><span class="sxs-lookup"><span data-stu-id="fc5e0-136">To keep this example simple, the code initializes the `WebMail` helper right in the page where you use it.</span></span> <span data-ttu-id="fc5e0-137">但对于实际网站，最好将类似于下面的初始化代码置于全局文件中，以便为网站中的所有文件初始化 `WebMail` 帮助程序。</span><span class="sxs-lookup"><span data-stu-id="fc5e0-137">However, for real websites, it's a better idea to put initialization code like this in a global file, so that you initialize the `WebMail` helper for all files in your website.</span></span> <span data-ttu-id="fc5e0-138">有关详细信息，请参阅[为 ASP.NET 网页自定义站点范围的行为](https://go.microsoft.com/fwlink/?LinkId=202906#Setting_Values_For_Helpers)。</span><span class="sxs-lookup"><span data-stu-id="fc5e0-138">For more information, see [Customizing Site-Wide Behavior for ASP.NET Web Pages](https://go.microsoft.com/fwlink/?LinkId=202906#Setting_Values_For_Helpers).</span></span>

1. <span data-ttu-id="fc5e0-139">创建新网站。</span><span class="sxs-lookup"><span data-stu-id="fc5e0-139">Create a new website.</span></span>
2. <span data-ttu-id="fc5e0-140">添加一个名为*EmailRequest*的新页面并添加以下标记：</span><span class="sxs-lookup"><span data-stu-id="fc5e0-140">Add a new page named *EmailRequest.cshtml* and add the following markup:</span></span> 

    [!code-html[Main](11-adding-email-to-your-web-site/samples/sample1.html)]

    <span data-ttu-id="fc5e0-141">请注意，窗体元素的 `action` 属性已设置为*ProcessRequest*。</span><span class="sxs-lookup"><span data-stu-id="fc5e0-141">Notice that the `action` attribute of the form element has been set to *ProcessRequest.cshtml*.</span></span> <span data-ttu-id="fc5e0-142">这意味着表单将提交到该页面，而不是返回到当前页面。</span><span class="sxs-lookup"><span data-stu-id="fc5e0-142">This means that the form will be submitted to that page instead of back to the current page.</span></span>
3. <span data-ttu-id="fc5e0-143">将名为*ProcessRequest*的新页添加到网站，并添加以下代码和标记：</span><span class="sxs-lookup"><span data-stu-id="fc5e0-143">Add a new page named *ProcessRequest.cshtml* to the website and add the following code and markup:</span></span>   

    [!code-cshtml[Main](11-adding-email-to-your-web-site/samples/sample2.cshtml)]

    <span data-ttu-id="fc5e0-144">在代码中，你将获取提交到页面的窗体字段的值。</span><span class="sxs-lookup"><span data-stu-id="fc5e0-144">In the code, you get the values of the form fields that were submitted to the page.</span></span> <span data-ttu-id="fc5e0-145">然后调用 `WebMail` 帮助器的 `Send` 方法来创建和发送电子邮件。</span><span class="sxs-lookup"><span data-stu-id="fc5e0-145">You then call the `WebMail` helper's `Send` method to create and send the email message.</span></span> <span data-ttu-id="fc5e0-146">在这种情况下，要使用的值由与从窗体提交的值连接的文本组成。</span><span class="sxs-lookup"><span data-stu-id="fc5e0-146">In this case, the values to use are made up of text that you concatenate with the values that were submitted from the form.</span></span>

    <span data-ttu-id="fc5e0-147">此页的代码位于 `try/catch` 块内。</span><span class="sxs-lookup"><span data-stu-id="fc5e0-147">The code for this page is inside a `try/catch` block.</span></span> <span data-ttu-id="fc5e0-148">如果出于任何原因而无法发送电子邮件，则无法正常工作（例如，设置不正确），`catch` 块中的代码将运行，并将 `errorMessage` 变量设置为发生的错误。</span><span class="sxs-lookup"><span data-stu-id="fc5e0-148">If for any reason the attempt to send an email doesn't work (for example, the settings aren't right), the code in the `catch` block runs and sets the `errorMessage` variable to the error that has occurred.</span></span> <span data-ttu-id="fc5e0-149">（有关 `try/catch` 块或 `<text>` 标记的详细信息，请参阅[使用 Razor 语法 ASP.NET 网页编程简介](https://go.microsoft.com/fwlink/?LinkID=251587#ID_HandlingErrors)。）</span><span class="sxs-lookup"><span data-stu-id="fc5e0-149">(For more information about `try/catch` blocks or the `<text>` tag, see [Introduction to ASP.NET Web Pages Programming Using the Razor Syntax](https://go.microsoft.com/fwlink/?LinkID=251587#ID_HandlingErrors).)</span></span>

    <span data-ttu-id="fc5e0-150">在页面的正文中，如果 `errorMessage` 变量为空（默认值），则用户将看到一条消息，指出电子邮件已发送。</span><span class="sxs-lookup"><span data-stu-id="fc5e0-150">In the body of the page, if the `errorMessage` variable is empty (the default), the user sees a message that the email message has been sent.</span></span> <span data-ttu-id="fc5e0-151">如果 `errorMessage` 变量设置为 true，则用户将看到一条消息，指出发送消息时出现问题。</span><span class="sxs-lookup"><span data-stu-id="fc5e0-151">If the `errorMessage` variable is set to true, the user sees a message that there's been a problem sending the message.</span></span>

    <span data-ttu-id="fc5e0-152">请注意，在显示错误消息的页面部分中有一个额外的测试： `if(debuggingFlag)`。</span><span class="sxs-lookup"><span data-stu-id="fc5e0-152">Notice that in the portion of the page that displays an error message, there's an additional test: `if(debuggingFlag)`.</span></span> <span data-ttu-id="fc5e0-153">如果在发送电子邮件时遇到问题，则可以将此变量设置为 true。</span><span class="sxs-lookup"><span data-stu-id="fc5e0-153">This is a variable that you can set to true if you're having trouble sending email.</span></span> <span data-ttu-id="fc5e0-154">如果 `debuggingFlag` 为 true，并且在发送电子邮件时出现问题，将显示一条额外的错误消息，其中显示了在尝试发送电子邮件时报告的任何 ASP.NET。</span><span class="sxs-lookup"><span data-stu-id="fc5e0-154">When `debuggingFlag` is true, and if there's a problem sending email, an additional error message is displayed that shows whatever ASP.NET has reported when it tried to send the email message.</span></span> <span data-ttu-id="fc5e0-155">但会出现公平警告： ASP.NET 报告无法发送电子邮件的错误消息可以是通用的。</span><span class="sxs-lookup"><span data-stu-id="fc5e0-155">Fair warning, though: the error messages that ASP.NET reports when it can't send an email message can be generic.</span></span> <span data-ttu-id="fc5e0-156">例如，如果 ASP.NET 无法联系 SMTP 服务器（例如，因为服务器名称中出现错误），则会 `Failure sending mail`错误。</span><span class="sxs-lookup"><span data-stu-id="fc5e0-156">For example, if ASP.NET can't contact the SMTP server (for example, because you made an error in the server name), the error is `Failure sending mail`.</span></span>

    > [!NOTE] 
    > 
    > <span data-ttu-id="fc5e0-157">**重要提示**从异常对象（在代码中为`ex`）收到错误消息时，*不要定期将*该消息传递给用户。</span><span class="sxs-lookup"><span data-stu-id="fc5e0-157">**Important** When you get an error message from an exception object (`ex` in the code), do *not* routinely pass that message through to users.</span></span> <span data-ttu-id="fc5e0-158">异常对象通常包含用户不应该看到的信息，甚至是安全漏洞。</span><span class="sxs-lookup"><span data-stu-id="fc5e0-158">Exception objects often include information that users should not see and that can even be a security vulnerability.</span></span> <span data-ttu-id="fc5e0-159">这就是为什么此代码包含变量 `debuggingFlag` 用于显示错误消息的开关，并且默认情况下变量设置为 false。</span><span class="sxs-lookup"><span data-stu-id="fc5e0-159">That's why this code includes the variable `debuggingFlag` that's used as a switch to display the error message, and why the variable by default is set to false.</span></span> <span data-ttu-id="fc5e0-160">仅当你在发送电子邮件时遇到问题并且需要进行调试时，*才*应将此变量设置为 true （因此显示错误消息）。</span><span class="sxs-lookup"><span data-stu-id="fc5e0-160">You should set that variable to true (and therefore display the error message) *only* if you're having a problem with sending email and you need to debug.</span></span> <span data-ttu-id="fc5e0-161">解决所有问题后，将 `debuggingFlag` 设置回 false。</span><span class="sxs-lookup"><span data-stu-id="fc5e0-161">Once you have fixed any problems, set `debuggingFlag` back to false.</span></span>

    <span data-ttu-id="fc5e0-162">在代码中修改以下与电子邮件相关的设置：</span><span class="sxs-lookup"><span data-stu-id="fc5e0-162">Modify the following email related settings in the code:</span></span>

   - <span data-ttu-id="fc5e0-163">将 `your-SMTP-host` 设置为你有权访问的 SMTP 服务器的名称。</span><span class="sxs-lookup"><span data-stu-id="fc5e0-163">Set `your-SMTP-host` to the name of the SMTP server that you have access to.</span></span>
   - <span data-ttu-id="fc5e0-164">将 `your-user-name-here` 设置为 SMTP 服务器帐户的用户名。</span><span class="sxs-lookup"><span data-stu-id="fc5e0-164">Set `your-user-name-here` to the user name for your SMTP server account.</span></span>
   - <span data-ttu-id="fc5e0-165">将 `your-account-password` 设置为 SMTP 服务器帐户的密码。</span><span class="sxs-lookup"><span data-stu-id="fc5e0-165">Set `your-account-password` to the password for your SMTP server account.</span></span>
   - <span data-ttu-id="fc5e0-166">将 `your-email-address-here` 设置为你自己的电子邮件地址。</span><span class="sxs-lookup"><span data-stu-id="fc5e0-166">Set `your-email-address-here` to your own email address.</span></span> <span data-ttu-id="fc5e0-167">这是从其发送消息的电子邮件地址。</span><span class="sxs-lookup"><span data-stu-id="fc5e0-167">This is the email address that the message is sent from.</span></span> <span data-ttu-id="fc5e0-168">（某些电子邮件提供商不允许您指定其他 `From` 地址，并将使用您的用户名作为 `From` 地址。）</span><span class="sxs-lookup"><span data-stu-id="fc5e0-168">(Some email providers don't let you specify a different `From` address and will use your user name as the `From` address.)</span></span>

     > [!TIP] 
     > 
     > <a id="configuring_email_settings"></a>
     > ### <a name="configuring-email-settings"></a><span data-ttu-id="fc5e0-169">配置电子邮件设置</span><span class="sxs-lookup"><span data-stu-id="fc5e0-169">Configuring Email Settings</span></span>
     > 
     > <span data-ttu-id="fc5e0-170">有时需要确保对 SMTP 服务器和端口号等设置正确的设置，这可能是一项挑战。</span><span class="sxs-lookup"><span data-stu-id="fc5e0-170">It can be a challenge sometimes to make sure you have the right settings for the SMTP server, port number, and so on.</span></span> <span data-ttu-id="fc5e0-171">下面是一些提示：</span><span class="sxs-lookup"><span data-stu-id="fc5e0-171">Here are a few tips:</span></span>
     > 
     > - <span data-ttu-id="fc5e0-172">SMTP 服务器名称通常类似于 `smtp.provider.com` 或 `smtp.provider.net`。</span><span class="sxs-lookup"><span data-stu-id="fc5e0-172">The SMTP server name is often something like `smtp.provider.com` or `smtp.provider.net`.</span></span> <span data-ttu-id="fc5e0-173">但是，如果将网站发布到宿主提供程序，此时可能会 `localhost`该点的 SMTP 服务器名称。</span><span class="sxs-lookup"><span data-stu-id="fc5e0-173">However, if you publish your site to a hosting provider, the SMTP server name at that point might be `localhost`.</span></span> <span data-ttu-id="fc5e0-174">这是因为，在发布并在提供程序的服务器上运行站点后，电子邮件服务器可能从应用程序的角度来看是本地的。</span><span class="sxs-lookup"><span data-stu-id="fc5e0-174">This is because after you've published and your site is running on the provider's server, the email server might be local from the perspective of your application.</span></span> <span data-ttu-id="fc5e0-175">服务器名称中的这一更改可能意味着你必须在发布过程中更改 SMTP 服务器名称。</span><span class="sxs-lookup"><span data-stu-id="fc5e0-175">This change in server names might mean you have to change the SMTP server name as part of your publishing process.</span></span>
     > - <span data-ttu-id="fc5e0-176">端口号通常为25。</span><span class="sxs-lookup"><span data-stu-id="fc5e0-176">The port number is usually 25.</span></span> <span data-ttu-id="fc5e0-177">但是，某些提供程序要求使用端口587或其他端口。</span><span class="sxs-lookup"><span data-stu-id="fc5e0-177">However, some providers require you to use port 587 or some other port.</span></span>
     > - <span data-ttu-id="fc5e0-178">请确保使用正确的凭据。</span><span class="sxs-lookup"><span data-stu-id="fc5e0-178">Make sure that you use the right credentials.</span></span> <span data-ttu-id="fc5e0-179">如果你已将站点发布到托管提供商，请使用提供商专门指出的凭据来发送电子邮件。</span><span class="sxs-lookup"><span data-stu-id="fc5e0-179">If you've published your site to a hosting provider, use the credentials that the provider has specifically indicated are for email.</span></span> <span data-ttu-id="fc5e0-180">它们可能与发布所用的凭据不同。</span><span class="sxs-lookup"><span data-stu-id="fc5e0-180">These might be different from the credentials you use to publish.</span></span>
     > - <span data-ttu-id="fc5e0-181">有时你根本不需要凭据。</span><span class="sxs-lookup"><span data-stu-id="fc5e0-181">Sometimes you don't need credentials at all.</span></span> <span data-ttu-id="fc5e0-182">如果你使用个人 ISP 发送电子邮件，则电子邮件提供商可能已知道你的凭据。</span><span class="sxs-lookup"><span data-stu-id="fc5e0-182">If you're sending email using your personal ISP, your email provider might already know your credentials.</span></span> <span data-ttu-id="fc5e0-183">发布后，可能需要使用不同于在本地计算机上进行测试时使用的凭据。</span><span class="sxs-lookup"><span data-stu-id="fc5e0-183">After you publish, you might need to use different credentials than when you test on your local computer.</span></span>
     > - <span data-ttu-id="fc5e0-184">如果电子邮件提供程序使用加密，则必须将 `WebMail.EnableSsl` 设置为 `true`。</span><span class="sxs-lookup"><span data-stu-id="fc5e0-184">If your email provider uses encryption, you have to set `WebMail.EnableSsl` to `true`.</span></span>
4. <span data-ttu-id="fc5e0-185">在浏览器中运行*EmailRequest*页。</span><span class="sxs-lookup"><span data-stu-id="fc5e0-185">Run the *EmailRequest.cshtml* page in a browser.</span></span> <span data-ttu-id="fc5e0-186">（请确保在运行之前在 "**文件**" 工作区中选择了该页面。）</span><span class="sxs-lookup"><span data-stu-id="fc5e0-186">(Make sure the page is selected in the **Files** workspace before you run it.)</span></span>
5. <span data-ttu-id="fc5e0-187">输入您的姓名和问题说明，然后单击 "**提交**" 按钮。</span><span class="sxs-lookup"><span data-stu-id="fc5e0-187">Enter your name and a problem description, and then click the **Submit** button.</span></span> <span data-ttu-id="fc5e0-188">你会被重定向到*ProcessRequest*页，该页面确认消息，并向你发送电子邮件。</span><span class="sxs-lookup"><span data-stu-id="fc5e0-188">You're redirected to the *ProcessRequest.cshtml* page, which confirms your message and which sends you an email message.</span></span> 

    ![[图像]](11-adding-email-to-your-web-site/_static/image2.jpg)

<a id="Sending_a_File"></a>
## <a name="sending-a-file-using-email"></a><span data-ttu-id="fc5e0-190">使用电子邮件发送文件</span><span class="sxs-lookup"><span data-stu-id="fc5e0-190">Sending a File Using Email</span></span>

<span data-ttu-id="fc5e0-191">你还可以发送附加到电子邮件的文件。</span><span class="sxs-lookup"><span data-stu-id="fc5e0-191">You can also send files that are attached to email messages.</span></span> <span data-ttu-id="fc5e0-192">在此过程中，您将创建一个文本文件和两个 HTML 页面。</span><span class="sxs-lookup"><span data-stu-id="fc5e0-192">In this procedure, you create a text file and two HTML pages.</span></span> <span data-ttu-id="fc5e0-193">将该文本文件用作电子邮件附件。</span><span class="sxs-lookup"><span data-stu-id="fc5e0-193">You'll use the text file as an email attachment.</span></span>

1. <span data-ttu-id="fc5e0-194">在网站中，添加一个新的文本文件并将其命名为*myfile.txt*。</span><span class="sxs-lookup"><span data-stu-id="fc5e0-194">In the website, add a new text file and name it *MyFile.txt*.</span></span>
2. <span data-ttu-id="fc5e0-195">复制以下文本并将其粘贴到文件中：</span><span class="sxs-lookup"><span data-stu-id="fc5e0-195">Copy the following text and paste it in the file:</span></span> 

    `Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.`
3. <span data-ttu-id="fc5e0-196">创建一个名为*SendFile*的页，并添加以下标记：</span><span class="sxs-lookup"><span data-stu-id="fc5e0-196">Create a page named *SendFile.cshtml* and add the following markup:</span></span> 

    [!code-html[Main](11-adding-email-to-your-web-site/samples/sample3.html)]
4. <span data-ttu-id="fc5e0-197">创建一个名为*ProcessFile*的页，并添加以下标记：</span><span class="sxs-lookup"><span data-stu-id="fc5e0-197">Create a page named *ProcessFile.cshtml* and add the following markup:</span></span> 

    [!code-cshtml[Main](11-adding-email-to-your-web-site/samples/sample4.cshtml)]
5. <span data-ttu-id="fc5e0-198">在示例的代码中修改以下与电子邮件相关的设置：</span><span class="sxs-lookup"><span data-stu-id="fc5e0-198">Modify the following email related settings in the code from the example:</span></span>

    - <span data-ttu-id="fc5e0-199">将 `your-SMTP-host` 设置为你有权访问的 SMTP 服务器的名称。</span><span class="sxs-lookup"><span data-stu-id="fc5e0-199">Set `your-SMTP-host` to the name of an SMTP server that you have access to.</span></span>
    - <span data-ttu-id="fc5e0-200">将 `your-user-name-here` 设置为 SMTP 服务器帐户的用户名。</span><span class="sxs-lookup"><span data-stu-id="fc5e0-200">Set `your-user-name-here` to the user name for your SMTP server account.</span></span>
    - <span data-ttu-id="fc5e0-201">将 `your-email-address-here` 设置为你自己的电子邮件地址。</span><span class="sxs-lookup"><span data-stu-id="fc5e0-201">Set `your-email-address-here` to your own email address.</span></span> <span data-ttu-id="fc5e0-202">这是从其发送消息的电子邮件地址。</span><span class="sxs-lookup"><span data-stu-id="fc5e0-202">This is the email address that the message is sent from.</span></span>
    - <span data-ttu-id="fc5e0-203">将 `your-account-password` 设置为 SMTP 服务器帐户的密码。</span><span class="sxs-lookup"><span data-stu-id="fc5e0-203">Set `your-account-password` to the password for your SMTP server account.</span></span>
    - <span data-ttu-id="fc5e0-204">将 `target-email-address-here` 设置为你自己的电子邮件地址。</span><span class="sxs-lookup"><span data-stu-id="fc5e0-204">Set `target-email-address-here` to your own email address.</span></span> <span data-ttu-id="fc5e0-205">（如前所述，你通常会向其他人发送一封电子邮件，但对于测试，你可以将其发送给你自己。）</span><span class="sxs-lookup"><span data-stu-id="fc5e0-205">(As before, you'd normally send an email to someone else, but for testing, you can send it to yourself.)</span></span>
6. <span data-ttu-id="fc5e0-206">在浏览器中运行*SendFile*页。</span><span class="sxs-lookup"><span data-stu-id="fc5e0-206">Run the *SendFile.cshtml* page in a browser.</span></span>
7. <span data-ttu-id="fc5e0-207">输入名称、主题行以及要附加的文本文件的名称（*myfile.txt*）。</span><span class="sxs-lookup"><span data-stu-id="fc5e0-207">Enter your name, a subject line, and the name of the text file to attach (*MyFile.txt*).</span></span>
8. <span data-ttu-id="fc5e0-208">单击 `Submit` 按钮。</span><span class="sxs-lookup"><span data-stu-id="fc5e0-208">Click the `Submit` button.</span></span> <span data-ttu-id="fc5e0-209">如前所述，你会被重定向到*ProcessFile*页，该页面会确认消息，并向你发送一封电子邮件，其中包含附加文件。</span><span class="sxs-lookup"><span data-stu-id="fc5e0-209">As before, you're redirected to the *ProcessFile.cshtml* page, which confirms your message and which sends you an email message with the attached file.</span></span>

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a><span data-ttu-id="fc5e0-210">其他资源</span><span class="sxs-lookup"><span data-stu-id="fc5e0-210">Additional Resources</span></span>

- [<span data-ttu-id="fc5e0-211">ASP.NET 网页 (Razor) 疑难解答指南</span><span class="sxs-lookup"><span data-stu-id="fc5e0-211">ASP.NET Web Pages (Razor) Troubleshooting Guide</span></span>](https://go.microsoft.com/fwlink/?LinkId=253001)
- [<span data-ttu-id="fc5e0-212">简单邮件传输协议</span><span class="sxs-lookup"><span data-stu-id="fc5e0-212">Simple Mail Transfer Protocol</span></span>](https://msdn.microsoft.com/library/aa480435.aspx)
- [<span data-ttu-id="fc5e0-213">为 ASP.NET 网页自定义站点范围的行为</span><span class="sxs-lookup"><span data-stu-id="fc5e0-213">Customizing Site-Wide Behavior for ASP.NET Web Pages</span></span>](https://go.microsoft.com/fwlink/?LinkId=202906)
