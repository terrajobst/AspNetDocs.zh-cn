---
uid: web-pages/overview/security/using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site
title: 使用 CAPTCHA 阻止 Bot 使用 ASP.NET Web Razor）网站 |Microsoft Docs
author: microsoft
description: 本文介绍如何使用 ReCaptcha （安全措施）来防止自动程序（bot）在 ASP.NET 网页（Razor）中执行任务 。
ms.author: riande
ms.date: 05/21/2012
ms.assetid: 2b381a41-2cb3-40c0-8545-1d393e22877f
msc.legacyurl: /web-pages/overview/security/using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site
msc.type: authoredcontent
ms.openlocfilehash: 2647a3155893a3dfb3214795a5f9cf1e8931fa91
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78440192"
---
# <a name="using-a-captcha-to-prevent-bots-from-using-your-aspnet-web-razor-site"></a><span data-ttu-id="20442-103">使用 CAPTCHA 阻止 Bot 使用 ASP.NET Web Razor）站点</span><span class="sxs-lookup"><span data-stu-id="20442-103">Using a CAPTCHA to Prevent Bots from Using Your ASP.NET Web Razor) Site</span></span>

<span data-ttu-id="20442-104">由[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="20442-104">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="20442-105">本文介绍如何使用 ReCaptcha （安全措施）来防止自动程序（bot）在 ASP.NET 网页（Razor）网站中执行任务。</span><span class="sxs-lookup"><span data-stu-id="20442-105">This article explains how to use ReCaptcha (a security measure) to prevent automated programs (bots) from performing tasks in an ASP.NET Web Pages (Razor) website.</span></span>
> 
> <span data-ttu-id="20442-106">**你将学习的内容：**</span><span class="sxs-lookup"><span data-stu-id="20442-106">**What you'll learn:**</span></span> 
> 
> - <span data-ttu-id="20442-107">如何将 CAPTCHA 测试添加到您的站点。</span><span class="sxs-lookup"><span data-stu-id="20442-107">How to add a CAPTCHA test to your site.</span></span>
> 
> <span data-ttu-id="20442-108">下面是本文中介绍的 ASP.NET 功能：</span><span class="sxs-lookup"><span data-stu-id="20442-108">These are the ASP.NET features introduced in the article:</span></span>
> 
> - <span data-ttu-id="20442-109">`ReCaptcha` 帮助程序。</span><span class="sxs-lookup"><span data-stu-id="20442-109">The `ReCaptcha` helper.</span></span>
> 
> > [!NOTE]
> > <span data-ttu-id="20442-110">本文中的信息适用于 ASP.NET 网页1.0 和网页2。</span><span class="sxs-lookup"><span data-stu-id="20442-110">The information in this article applies to ASP.NET Web Pages 1.0 and Web Pages 2.</span></span>

## <a name="about-captchas"></a><span data-ttu-id="20442-111">关于 CAPTCHAs</span><span class="sxs-lookup"><span data-stu-id="20442-111">About CAPTCHAs</span></span>

<span data-ttu-id="20442-112">只要你允许用户在你的网站中注册，甚至只是输入名称和 URL （如博客评论），你可能会收到大量的虚假名称。</span><span class="sxs-lookup"><span data-stu-id="20442-112">Any time you let people register in your site, or even just enter a name and URL (like for a blog comment), you might get a flood of fake names.</span></span> <span data-ttu-id="20442-113">这通常由自动程序（bot）留下，尝试将 Url 保留在他们可以找到的每个网站中。</span><span class="sxs-lookup"><span data-stu-id="20442-113">These are often left by automated programs (bots) that try to leave URLs in every website they can find.</span></span> <span data-ttu-id="20442-114">（常见的动机是发布产品的 Url 以供销售。）</span><span class="sxs-lookup"><span data-stu-id="20442-114">(A common motivation is to post the URLs of products for sale.)</span></span>

<span data-ttu-id="20442-115">可以通过使用*CAPTCHA*在用户注册或输入其名称和站点时对用户进行验证，来帮助确保用户是真实人员而不是计算机程序。</span><span class="sxs-lookup"><span data-stu-id="20442-115">You can help make sure that a user is real person and not a computer program by using a *CAPTCHA* to validate users when they register or otherwise enter their name and site.</span></span> <span data-ttu-id="20442-116">CAPTCHA 代表完全自动化的公共把测试，使计算机和人与众不同。</span><span class="sxs-lookup"><span data-stu-id="20442-116">CAPTCHA stands for Completely Automated Public Turing test to tell Computers and Humans Apart.</span></span> <span data-ttu-id="20442-117">CAPTCHA 是一种*质询-响应*测试，要求用户执行一项操作，该操作对于某个人来说是一件容易的事情，但这是一项很难实现的自动化计划。</span><span class="sxs-lookup"><span data-stu-id="20442-117">A CAPTCHA is a *challenge-response* test in which the user is asked to do something that is easy for a person to do but hard for an automated program to do.</span></span> <span data-ttu-id="20442-118">最常见的 CAPTCHA 类型是：其中显示一些失真的字母并要求键入它们。</span><span class="sxs-lookup"><span data-stu-id="20442-118">The most common type of CAPTCHA is one where you see some distorted letters and are asked to type them.</span></span> <span data-ttu-id="20442-119">（这种扭曲应该会使机器人难以破解这些字母。）</span><span class="sxs-lookup"><span data-stu-id="20442-119">(The distortion is supposed to make it hard for bots to decipher the letters.)</span></span>

## <a name="adding-a-recaptcha-test"></a><span data-ttu-id="20442-120">添加 ReCaptcha 测试</span><span class="sxs-lookup"><span data-stu-id="20442-120">Adding a ReCaptcha Test</span></span>

<span data-ttu-id="20442-121">在 ASP.NET 页中，可以使用 `ReCaptcha` 帮助器呈现基于 ReCaptcha 服务（[http://recaptcha.net](http://recaptcha.net)）的 CAPTCHA 测试。</span><span class="sxs-lookup"><span data-stu-id="20442-121">In ASP.NET pages, you can use the `ReCaptcha` helper to render a CAPTCHA test that is based on the ReCaptcha service ([http://recaptcha.net](http://recaptcha.net)).</span></span> <span data-ttu-id="20442-122">`ReCaptcha` 帮助程序显示在验证页面之前用户必须正确输入的两个扭曲词的图像。</span><span class="sxs-lookup"><span data-stu-id="20442-122">The `ReCaptcha` helper displays an image of two distorted words that users have to enter correctly before the page is validated.</span></span> <span data-ttu-id="20442-123">用户响应通过 ReCaptcha.Net 服务进行验证。</span><span class="sxs-lookup"><span data-stu-id="20442-123">The user response is validated by the ReCaptcha.Net service.</span></span>

![](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/_static/image1.jpg)

1. <span data-ttu-id="20442-124">在 ReCaptcha.Net （[http://recaptcha.net](http://recaptcha.net)）注册你的网站。</span><span class="sxs-lookup"><span data-stu-id="20442-124">Register your website at ReCaptcha.Net ([http://recaptcha.net](http://recaptcha.net)).</span></span> <span data-ttu-id="20442-125">完成注册后，你将获得一个公钥和一个私钥。</span><span class="sxs-lookup"><span data-stu-id="20442-125">When you've completed registration, you'll get a public key and a private key.</span></span>
2. <span data-ttu-id="20442-126">根据在[ASP.NET 网页站点中安装帮助程序](https://go.microsoft.com/fwlink/?LinkId=252372)中所述，将 ASP.NET Web 帮助程序库添加到你的网站中（如果尚未安装）。</span><span class="sxs-lookup"><span data-stu-id="20442-126">Add the ASP.NET Web Helpers Library to your website as described in [Installing Helpers in an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=252372), if you haven't already.</span></span>
3. <span data-ttu-id="20442-127">如果还没有 *\_AppStart*文件，请在网站的根文件夹中创建一个名为 *\_AppStart*的文件。</span><span class="sxs-lookup"><span data-stu-id="20442-127">If you don't already have a *\_AppStart.cshtml* file, in the root folder of a website create a file named *\_AppStart.cshtml*.</span></span>
4. <span data-ttu-id="20442-128">在 *\_AppStart*文件中添加以下 `Recaptcha` 帮助程序设置：</span><span class="sxs-lookup"><span data-stu-id="20442-128">Add the following `Recaptcha` helper settings in the *\_AppStart.cshtml* file:</span></span> 

    [!code-cshtml[Main](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/samples/sample1.cshtml?highlight=6-7)]
5. <span data-ttu-id="20442-129">使用自己的公钥和私钥设置 "`PublicKey`" 和 "`PrivateKey`" 属性。</span><span class="sxs-lookup"><span data-stu-id="20442-129">Set the `PublicKey` and `PrivateKey` properties using your own public and private keys.</span></span>
6. <span data-ttu-id="20442-130">保存 *\_AppStart*文件并将其关闭。</span><span class="sxs-lookup"><span data-stu-id="20442-130">Save the *\_AppStart.cshtml* file and close it.</span></span>
7. <span data-ttu-id="20442-131">在网站的根文件夹中，创建名为*Recaptcha*的新页面。</span><span class="sxs-lookup"><span data-stu-id="20442-131">In the root folder of a website, create new page named *Recaptcha.cshtml*.</span></span>
8. <span data-ttu-id="20442-132">将现有内容替换为以下内容：</span><span class="sxs-lookup"><span data-stu-id="20442-132">Replace the existing content with the following:</span></span> 

    [!code-cshtml[Main](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/samples/sample2.cshtml)]
9. <span data-ttu-id="20442-133">在浏览器中运行*Recaptcha*页。</span><span class="sxs-lookup"><span data-stu-id="20442-133">Run the *Recaptcha.cshtml* page in a browser.</span></span> <span data-ttu-id="20442-134">如果 `PrivateKey` 的值有效，则页面将显示 ReCaptcha 控件和按钮。</span><span class="sxs-lookup"><span data-stu-id="20442-134">If the `PrivateKey` value is valid, the page displays the ReCaptcha control and a button.</span></span> <span data-ttu-id="20442-135">如果未在 *\_AppStart*中全局设置密钥，则页面将显示错误。</span><span class="sxs-lookup"><span data-stu-id="20442-135">If you had not set the keys globally in *\_AppStart.html*, the page would display an error.</span></span> 

    ![](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/_static/image1.png)
10. <span data-ttu-id="20442-136">输入测试的字词。</span><span class="sxs-lookup"><span data-stu-id="20442-136">Enter the words for the test.</span></span> <span data-ttu-id="20442-137">如果通过了 ReCaptcha 测试，则会看到一条消息。</span><span class="sxs-lookup"><span data-stu-id="20442-137">If you pass the ReCaptcha test, you see a message to that effect.</span></span> <span data-ttu-id="20442-138">否则，会显示一条错误消息，并重新显示 ReCaptcha 控件。</span><span class="sxs-lookup"><span data-stu-id="20442-138">Otherwise you see an error message and the ReCaptcha control is redisplayed.</span></span>

> [!NOTE]
> <span data-ttu-id="20442-139">如果您的计算机位于使用代理服务器的域中，则您可能需要配置*web.config*文件的 `defaultproxy` 元素。</span><span class="sxs-lookup"><span data-stu-id="20442-139">If your computer is on a domain that uses proxy server, you might need to configure the `defaultproxy` element of the *Web.config* file.</span></span> <span data-ttu-id="20442-140">下面的示例演示一个*web.config*文件，其中的 `defaultproxy` 元素配置为使 ReCaptcha 服务能够正常工作。</span><span class="sxs-lookup"><span data-stu-id="20442-140">The following example shows a *Web.config* file with the `defaultproxy` element configured to enable the ReCaptcha service to work.</span></span>
> 
> [!code-xml[Main](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/samples/sample3.xml)]

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a><span data-ttu-id="20442-141">其他资源</span><span class="sxs-lookup"><span data-stu-id="20442-141">Additional Resources</span></span>

- [<span data-ttu-id="20442-142">为 ASP.NET 网页站点自定义站点范围的行为</span><span class="sxs-lookup"><span data-stu-id="20442-142">Customizing Site-Wide Behavior for ASP.NET Web Pages Sites</span></span>](https://go.microsoft.com/fwlink/?LinkId=202906)
- [<span data-ttu-id="20442-143">ReCaptcha 站点</span><span class="sxs-lookup"><span data-stu-id="20442-143">ReCaptcha site</span></span>](https://www.google.com/recaptcha)
