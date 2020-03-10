---
uid: web-pages/overview/ui-layouts-and-themes/18-customizing-site-wide-behavior
title: 为 ASP.NET 网页（Razor）站点自定义站点范围的行为 |Microsoft Docs
author: Rick-Anderson
description: 本章介绍如何将设置设置到整个网站或整个文件夹，而不只是一个页面。
ms.author: riande
ms.date: 02/17/2014
ms.assetid: e158bed7-226f-4275-b02e-7553bd58c669
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/18-customizing-site-wide-behavior
msc.type: authoredcontent
ms.openlocfilehash: f05e05f725d9209bce283ce18659ae5efe4de2ee
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78515246"
---
# <a name="customizing-site-wide-behavior-for-aspnet-web-pages-razor-sites"></a><span data-ttu-id="242aa-103">为 ASP.NET 网页（Razor）站点自定义站点范围的行为</span><span class="sxs-lookup"><span data-stu-id="242aa-103">Customizing Site-Wide Behavior for ASP.NET Web Pages (Razor) Sites</span></span>

<span data-ttu-id="242aa-104">作者： [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="242aa-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="242aa-105">本文介绍如何在 ASP.NET 网页（Razor）网站中进行页面的站点端设置。</span><span class="sxs-lookup"><span data-stu-id="242aa-105">This article explains how to make site-side settings for pages in an ASP.NET Web Pages (Razor) website.</span></span>
> 
> <span data-ttu-id="242aa-106">学习内容：</span><span class="sxs-lookup"><span data-stu-id="242aa-106">What you'll learn:</span></span>
> 
> - <span data-ttu-id="242aa-107">如何运行代码，使您可以为站点中的所有页面设置值（全局值或帮助设置）。</span><span class="sxs-lookup"><span data-stu-id="242aa-107">How to run code that lets you set values (global values or helper settings) for all pages in a site.</span></span>
> - <span data-ttu-id="242aa-108">如何运行代码，使你可以为文件夹中的所有页面设置值。</span><span class="sxs-lookup"><span data-stu-id="242aa-108">How to run code that lets you set values for all pages in a folder.</span></span>
> - <span data-ttu-id="242aa-109">如何在页面加载之前和之后运行代码。</span><span class="sxs-lookup"><span data-stu-id="242aa-109">How to run code before and after a page loads.</span></span>
> - <span data-ttu-id="242aa-110">如何将错误发送到中央错误页。</span><span class="sxs-lookup"><span data-stu-id="242aa-110">How to send errors to a central error page.</span></span>
> - <span data-ttu-id="242aa-111">如何将身份验证添加到文件夹中的所有页。</span><span class="sxs-lookup"><span data-stu-id="242aa-111">How to add authentication to all pages in a folder.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="242aa-112">本教程中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="242aa-112">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="242aa-113">ASP.NET 网页（Razor）2</span><span class="sxs-lookup"><span data-stu-id="242aa-113">ASP.NET Web Pages (Razor) 2</span></span>
> - <span data-ttu-id="242aa-114">WebMatrix 3</span><span class="sxs-lookup"><span data-stu-id="242aa-114">WebMatrix 3</span></span>
> - <span data-ttu-id="242aa-115">ASP.NET Web 帮助程序库（NuGet 包）</span><span class="sxs-lookup"><span data-stu-id="242aa-115">ASP.NET Web Helpers Library (NuGet package)</span></span>
>   
> 
> <span data-ttu-id="242aa-116">本教程还适用于 ASP.NET 网页3和 Visual Studio 2013 （对于 Web 为 Visual Studio Express 2013），但不能使用 ASP.NET Web 帮助程序库。</span><span class="sxs-lookup"><span data-stu-id="242aa-116">This tutorial also works with ASP.NET Web Pages 3 and Visual Studio 2013 (or Visual Studio Express 2013 for Web), except you cannot use the ASP.NET Web Helpers Library.</span></span>

<a id="Adding_Website_Startup_Code"></a>
## <a name="adding-website-startup-code-for-aspnet-web-pages"></a><span data-ttu-id="242aa-117">为 ASP.NET 网页添加网站启动代码</span><span class="sxs-lookup"><span data-stu-id="242aa-117">Adding Website Startup Code for ASP.NET Web Pages</span></span>

<span data-ttu-id="242aa-118">对于在 ASP.NET 网页中编写的大部分代码，单个页面可以包含该页所需的所有代码。</span><span class="sxs-lookup"><span data-stu-id="242aa-118">For much of the code that you write in ASP.NET Web Pages, an individual page can contain all the code that's required for that page.</span></span> <span data-ttu-id="242aa-119">例如，如果页面发送电子邮件，则可以将该操作的所有代码都放在一个页面中。</span><span class="sxs-lookup"><span data-stu-id="242aa-119">For example, if a page sends an email message, it's possible to put all the code for that operation in a single page.</span></span> <span data-ttu-id="242aa-120">这可能包括用于初始化用于发送电子邮件的设置（即 SMTP 服务器）以及用于发送电子邮件的代码。</span><span class="sxs-lookup"><span data-stu-id="242aa-120">This can include the code to initialize the settings for sending email (that is, for the SMTP server) and for sending the email message.</span></span>

<span data-ttu-id="242aa-121">但是，在某些情况下，你可能需要在运行站点上的任何页面之前运行一些代码。</span><span class="sxs-lookup"><span data-stu-id="242aa-121">However, in some situations, you might want to run some code before any page on the site runs.</span></span> <span data-ttu-id="242aa-122">这对于设置可以在站点中的任何位置使用的值（称为*全局值*）很有用。例如，某些帮助程序要求你提供电子邮件设置或帐户密钥之类的值。</span><span class="sxs-lookup"><span data-stu-id="242aa-122">This is useful for setting values that can be used anywhere in the site (referred to as *global values*.) For example, some helpers require you to provide values like email settings or account keys.</span></span> <span data-ttu-id="242aa-123">可以方便地将这些设置保存到全局值中。</span><span class="sxs-lookup"><span data-stu-id="242aa-123">It can be handy to keep these settings in global values.</span></span>

<span data-ttu-id="242aa-124">为此，可以在站点的根目录中创建一个名为 *\_AppStart*的页。</span><span class="sxs-lookup"><span data-stu-id="242aa-124">You can do this by creating a page named *\_AppStart.cshtml* in the root of the site.</span></span> <span data-ttu-id="242aa-125">如果此页面存在，则会在请求站点中的任何页面时首次运行。</span><span class="sxs-lookup"><span data-stu-id="242aa-125">If this page exists, it runs the first time any page in the site is requested.</span></span> <span data-ttu-id="242aa-126">因此，它是运行代码以设置全局值的好时机。</span><span class="sxs-lookup"><span data-stu-id="242aa-126">Therefore, it's a good place to run code to set global values.</span></span> <span data-ttu-id="242aa-127">（由于 *\_AppStart*具有下划线前缀，因此 ASP.NET 不会将页面发送到浏览器，即使用户直接请求它也是如此。）</span><span class="sxs-lookup"><span data-stu-id="242aa-127">(Because *\_AppStart.cshtml* has an underscore prefix, ASP.NET won't send the page to a browser even if users request it directly.)</span></span>

<span data-ttu-id="242aa-128">下图显示了 *\_AppStart*页面的工作方式。</span><span class="sxs-lookup"><span data-stu-id="242aa-128">The following diagram shows how the *\_AppStart.cshtml* page works.</span></span> <span data-ttu-id="242aa-129">当请求进入某个页面，并且这是对站点中任何页面的第一个请求时，ASP.NET 首先检查是否存在 *\_AppStart*的页面。</span><span class="sxs-lookup"><span data-stu-id="242aa-129">When a request comes in for a page, and if this is the first request for any page in the site, ASP.NET first checks whether a *\_AppStart.cshtml* page exists.</span></span> <span data-ttu-id="242aa-130">如果是这样，则 *\_AppStart* "页中的任何代码都将运行，然后将运行请求的页面。</span><span class="sxs-lookup"><span data-stu-id="242aa-130">If so, any code in the *\_AppStart.cshtml* page runs, and then the requested page runs.</span></span>

![[图像]](18-customizing-site-wide-behavior/_static/image1.jpg)

## <a name="setting-global-values-for-your-website"></a><span data-ttu-id="242aa-132">设置网站的全局值</span><span class="sxs-lookup"><span data-stu-id="242aa-132">Setting Global Values for Your Website</span></span>

1. <span data-ttu-id="242aa-133">在 WebMatrix 网站的根文件夹中，创建一个名为 *\_AppStart*的文件。</span><span class="sxs-lookup"><span data-stu-id="242aa-133">In the root folder of a WebMatrix website, create a file named *\_AppStart.cshtml*.</span></span> <span data-ttu-id="242aa-134">文件必须位于站点的根目录中。</span><span class="sxs-lookup"><span data-stu-id="242aa-134">The file must be in the root of the site.</span></span>
2. <span data-ttu-id="242aa-135">将现有内容替换为以下内容：</span><span class="sxs-lookup"><span data-stu-id="242aa-135">Replace the existing content with the following:</span></span> 

    [!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample1.cshtml)]

    <span data-ttu-id="242aa-136">此代码在 `AppState` 字典中存储一个值，此值可自动用于网站中的所有页。</span><span class="sxs-lookup"><span data-stu-id="242aa-136">This code stores a value in the `AppState` dictionary, which is automatically available to all pages in the site.</span></span> <span data-ttu-id="242aa-137">请注意， *\_AppStart*文件中没有任何标记。</span><span class="sxs-lookup"><span data-stu-id="242aa-137">Notice that the *\_AppStart.cshtml* file does not have any markup in it.</span></span> <span data-ttu-id="242aa-138">页面将运行代码，然后重定向到最初请求的页面。</span><span class="sxs-lookup"><span data-stu-id="242aa-138">The page will run the code and then redirect to the page that was originally requested.</span></span>

    > [!NOTE]
    > <span data-ttu-id="242aa-139">将代码放在 *\_AppStart*文件中时请小心。</span><span class="sxs-lookup"><span data-stu-id="242aa-139">Be careful when you put code in the *\_AppStart.cshtml* file.</span></span> <span data-ttu-id="242aa-140">如果 *\_AppStart*文件中的代码出现任何错误，网站将无法启动。</span><span class="sxs-lookup"><span data-stu-id="242aa-140">If any errors occur in code in the *\_AppStart.cshtml* file, the website won't start.</span></span>
3. <span data-ttu-id="242aa-141">在根文件夹中，创建一个名为*AppName. cshtml*的新页。</span><span class="sxs-lookup"><span data-stu-id="242aa-141">In the root folder, create a new page named *AppName.cshtml*.</span></span>
4. <span data-ttu-id="242aa-142">将默认标记和代码替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="242aa-142">Replace the default markup and code with the following:</span></span> 

    [!code-html[Main](18-customizing-site-wide-behavior/samples/sample2.html)]

    <span data-ttu-id="242aa-143">此代码从在 *\_AppStart*页面中设置的 `AppState` 对象中提取值。</span><span class="sxs-lookup"><span data-stu-id="242aa-143">This code extracts the value from the `AppState` object that you set in the *\_AppStart.cshtml* page.</span></span>
5. <span data-ttu-id="242aa-144">在浏览器中运行*AppName. cshtml*页面。</span><span class="sxs-lookup"><span data-stu-id="242aa-144">Run the *AppName.cshtml* page in a browser.</span></span> <span data-ttu-id="242aa-145">（请确保在运行之前在 "**文件**" 工作区中选择了该页面。）该页显示全局值。</span><span class="sxs-lookup"><span data-stu-id="242aa-145">(Make sure the page is selected in the **Files** workspace before you run it.) The page displays the global value.</span></span> 

    ![[图像]](18-customizing-site-wide-behavior/_static/image2.jpg)

<a id="Setting_Values_For_Helpers"></a>
## <a name="setting-values-for-helpers"></a><span data-ttu-id="242aa-147">为帮助器设置值</span><span class="sxs-lookup"><span data-stu-id="242aa-147">Setting Values for Helpers</span></span>

<span data-ttu-id="242aa-148">*\_AppStart*文件的一个不错用途是为你在站点中使用的帮助程序设置值，并且必须进行初始化。</span><span class="sxs-lookup"><span data-stu-id="242aa-148">A good use for the *\_AppStart.cshtml* file is to set values for helpers that you use in your site and that have to be initialized.</span></span> <span data-ttu-id="242aa-149">典型示例是 `WebMail` 帮助程序的电子邮件设置，以及 `ReCaptcha` 帮助程序的私钥和公钥。</span><span class="sxs-lookup"><span data-stu-id="242aa-149">Typical examples are email settings for the `WebMail` helper and the private and public keys for the `ReCaptcha` helper.</span></span> <span data-ttu-id="242aa-150">在这种情况下，可以在 *\_AppStart*中设置值一次，然后为站点中的所有页面设置这些值。</span><span class="sxs-lookup"><span data-stu-id="242aa-150">In cases like these, you can set the values once in the *\_AppStart.cshtml* and then they're already set for all the pages in your site.</span></span>

<span data-ttu-id="242aa-151">此过程说明如何全局设置 `WebMail` 设置。</span><span class="sxs-lookup"><span data-stu-id="242aa-151">This procedure shows you how to set `WebMail` settings globally.</span></span> <span data-ttu-id="242aa-152">（有关使用 `WebMail` 帮助器的详细信息，请参阅向[ASP.NET 网页网站添加电子邮件](../getting-started/11-adding-email-to-your-web-site.md)。）</span><span class="sxs-lookup"><span data-stu-id="242aa-152">(For more information about using the `WebMail` helper, see [Adding Email to an ASP.NET Web Pages Site](../getting-started/11-adding-email-to-your-web-site.md).)</span></span>

1. <span data-ttu-id="242aa-153">如在[ASP.NET 网页站点中安装帮助程序](https://go.microsoft.com/fwlink/?LinkId=252372)中所述，将 ASP.NET Web 帮助程序库添加到你的网站中（如果尚未添加）。</span><span class="sxs-lookup"><span data-stu-id="242aa-153">Add the ASP.NET Web Helpers Library to your website as described in [Installing Helpers in an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=252372), if you haven't already added it.</span></span>
2. <span data-ttu-id="242aa-154">如果还没有 *\_AppStart*文件，请在网站的根文件夹中创建一个名为 *\_AppStart*的文件。</span><span class="sxs-lookup"><span data-stu-id="242aa-154">If you don't already have a *\_AppStart.cshtml* file, in the root folder of a website create a file named *\_AppStart.cshtml*.</span></span>
3. <span data-ttu-id="242aa-155">将以下 `WebMail` 设置添加到 *\_AppStart*文件中：</span><span class="sxs-lookup"><span data-stu-id="242aa-155">Add the following `WebMail` settings to the *\_AppStart.cshtml* file:</span></span> 

    [!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample3.cshtml?highlight=2-7)]

    <span data-ttu-id="242aa-156">在代码中修改以下与电子邮件相关的设置：</span><span class="sxs-lookup"><span data-stu-id="242aa-156">Modify the following email related settings in the code:</span></span>

   - <span data-ttu-id="242aa-157">将 `your-SMTP-host` 设置为你有权访问的 SMTP 服务器的名称。</span><span class="sxs-lookup"><span data-stu-id="242aa-157">Set `your-SMTP-host` to the name of the SMTP server that you have access to.</span></span>
   - <span data-ttu-id="242aa-158">将 `your-user-name-here` 设置为 SMTP 服务器帐户的用户名。</span><span class="sxs-lookup"><span data-stu-id="242aa-158">Set `your-user-name-here` to the user name for your SMTP server account.</span></span>
   - <span data-ttu-id="242aa-159">将 `your-account-password` 设置为 SMTP 服务器帐户的密码。</span><span class="sxs-lookup"><span data-stu-id="242aa-159">Set `your-account-password` to the password for your SMTP server account.</span></span>
   - <span data-ttu-id="242aa-160">将 `your-email-address-here` 设置为你自己的电子邮件地址。</span><span class="sxs-lookup"><span data-stu-id="242aa-160">Set `your-email-address-here` to your own email address.</span></span> <span data-ttu-id="242aa-161">这是从其发送消息的电子邮件地址。</span><span class="sxs-lookup"><span data-stu-id="242aa-161">This is the email address that the message is sent from.</span></span> <span data-ttu-id="242aa-162">（某些电子邮件提供商不允许您指定其他 `From` 地址，并将使用您的用户名作为 `From` 地址。）</span><span class="sxs-lookup"><span data-stu-id="242aa-162">(Some email providers don't let you specify a different `From` address and will use your user name as the `From` address.)</span></span>

     <span data-ttu-id="242aa-163">有关 SMTP 设置的详细信息，请参阅在[从 ASP.NET 网页（razor）站点发送电子邮件](https://go.microsoft.com/fwlink/?LinkID=202899)中的[配置电子邮件设置](https://go.microsoft.com/fwlink/?LinkID=202899#configuring_email_settings)和[ASP.NET 网页（razor）故障排除指南](https://go.microsoft.com/fwlink/?LinkId=253001)中[发送电子邮件的问题](https://go.microsoft.com/fwlink/?LinkId=253001#email)。</span><span class="sxs-lookup"><span data-stu-id="242aa-163">For more information about SMTP settings, see [Configuring Email Settings](https://go.microsoft.com/fwlink/?LinkID=202899#configuring_email_settings) in the article [Sending Email from an ASP.NET Web Pages (Razor) Site](https://go.microsoft.com/fwlink/?LinkID=202899) and [Issues with Sending Email](https://go.microsoft.com/fwlink/?LinkId=253001#email) in the [ASP.NET Web Pages (Razor) Troubleshooting Guide](https://go.microsoft.com/fwlink/?LinkId=253001).</span></span>
4. <span data-ttu-id="242aa-164">保存 *\_AppStart*文件并将其关闭。</span><span class="sxs-lookup"><span data-stu-id="242aa-164">Save the *\_AppStart.cshtml* file and close it.</span></span>
5. <span data-ttu-id="242aa-165">在网站的根文件夹中，创建名为*TestEmail*的新页面。</span><span class="sxs-lookup"><span data-stu-id="242aa-165">In the root folder of a website, create new page named *TestEmail.cshtml*.</span></span>
6. <span data-ttu-id="242aa-166">将现有内容替换为以下内容：</span><span class="sxs-lookup"><span data-stu-id="242aa-166">Replace the existing content with the following:</span></span> 

     [!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample4.cshtml)]
7. <span data-ttu-id="242aa-167">在浏览器中运行*TestEmail*页。</span><span class="sxs-lookup"><span data-stu-id="242aa-167">Run the *TestEmail.cshtml* page in a browser.</span></span>
8. <span data-ttu-id="242aa-168">填写字段，向自己发送一封电子邮件，然后单击 "**发送**"。</span><span class="sxs-lookup"><span data-stu-id="242aa-168">Fill in the fields to send yourself an email message and then click **Send**.</span></span>
9. <span data-ttu-id="242aa-169">检查电子邮件以确保已收到该邮件。</span><span class="sxs-lookup"><span data-stu-id="242aa-169">Check your email to make sure you've gotten the message.</span></span>

<span data-ttu-id="242aa-170">此示例的重要部分是，不经常更改的设置（如 SMTP 服务器的名称和电子邮件凭据）在 *\_AppStart*文件中设置。</span><span class="sxs-lookup"><span data-stu-id="242aa-170">The important part of this example is that the settings that you don't usually change — like the name of your SMTP server and your email credentials — are set in the *\_AppStart.cshtml* file.</span></span> <span data-ttu-id="242aa-171">这样一来，就不需要在发送电子邮件的每个页面中再次设置它们。</span><span class="sxs-lookup"><span data-stu-id="242aa-171">That way you don't need to set them again in each page where you send email.</span></span> <span data-ttu-id="242aa-172">（但是，如果出于某种原因，您需要更改这些设置，则可以在页面中单独设置它们。）在该页中，只设置通常每次更改的值，例如收件人和电子邮件的正文。</span><span class="sxs-lookup"><span data-stu-id="242aa-172">(Although if for some reason you need to change those settings, you can set them individually in a page.) In the page, you only set the values that typically change each time, like the recipient and the body of the email message.</span></span>

<a id="Running_Code_Before_and_After"></a>
## <a name="running-code-before-and-after-files-in-a-folder"></a><span data-ttu-id="242aa-173">在文件夹中的文件之前和之后运行代码</span><span class="sxs-lookup"><span data-stu-id="242aa-173">Running Code Before and After Files in a Folder</span></span>

<span data-ttu-id="242aa-174">正如你可以在站点运行的页面之前使用 *\_AppStart*来编写代码，你可以编写在特定文件夹运行的任何页面之前（和之后）运行的代码。</span><span class="sxs-lookup"><span data-stu-id="242aa-174">Just like you can use *\_AppStart.cshtml* to write code before pages in the site run, you can write code that runs before (and after) any page in a particular folder run.</span></span> <span data-ttu-id="242aa-175">这对于为文件夹中的所有页面设置相同的布局页，或在运行文件夹中的页面之前检查用户是否登录都非常有用。</span><span class="sxs-lookup"><span data-stu-id="242aa-175">This is useful for things like setting the same layout page for all the pages in a folder, or for checking that a user is logged in before running a page in the folder.</span></span>

<span data-ttu-id="242aa-176">对于特定文件夹中的页面，可以在名为 *\_PageStart*的文件中创建代码。</span><span class="sxs-lookup"><span data-stu-id="242aa-176">For pages in particular folders, you can create code in a file named *\_PageStart.cshtml*.</span></span> <span data-ttu-id="242aa-177">下图显示了 *\_PageStart*页面的工作方式。</span><span class="sxs-lookup"><span data-stu-id="242aa-177">The following diagram shows how the *\_PageStart.cshtml* page works.</span></span> <span data-ttu-id="242aa-178">当请求进入某个页面时，ASP.NET 首先会检查 *\_AppStart* "页，并运行。</span><span class="sxs-lookup"><span data-stu-id="242aa-178">When a request comes in for a page, ASP.NET first checks for a *\_AppStart.cshtml* page and runs that.</span></span> <span data-ttu-id="242aa-179">然后，ASP.NET 将检查是否存在 *\_PageStart*页，如果是，则运行该页。</span><span class="sxs-lookup"><span data-stu-id="242aa-179">Then ASP.NET checks whether there's a *\_PageStart.cshtml* page, and if so, runs that.</span></span> <span data-ttu-id="242aa-180">然后，它将运行请求的页面。</span><span class="sxs-lookup"><span data-stu-id="242aa-180">It then runs the requested page.</span></span>

<span data-ttu-id="242aa-181">在 *\_PageStart* "页中，可以通过包含 `RunPage` 方法来指定处理所需的页的处理过程中的位置。</span><span class="sxs-lookup"><span data-stu-id="242aa-181">Inside the *\_PageStart.cshtml* page, you can specify where during processing you want the requested page to run by including a `RunPage` method.</span></span> <span data-ttu-id="242aa-182">这使您可以在请求的页运行之前运行代码，然后再次运行代码。</span><span class="sxs-lookup"><span data-stu-id="242aa-182">This lets you run code before the requested page runs and then again after it.</span></span> <span data-ttu-id="242aa-183">如果不包含 `RunPage`， *\_PageStart*中的所有代码都将运行，然后自动运行请求的页面。</span><span class="sxs-lookup"><span data-stu-id="242aa-183">If you don't include `RunPage`, all the code in *\_PageStart.cshtml* runs, and then the requested page runs automatically.</span></span>

![[图像]](18-customizing-site-wide-behavior/_static/image3.jpg)

<span data-ttu-id="242aa-185">ASP.NET 可让你创建 *\_PageStart*文件的层次结构。</span><span class="sxs-lookup"><span data-stu-id="242aa-185">ASP.NET lets you create a hierarchy of *\_PageStart.cshtml* files.</span></span> <span data-ttu-id="242aa-186">可以将 *\_PageStart*文件放置在站点的根目录和任何子文件夹中。</span><span class="sxs-lookup"><span data-stu-id="242aa-186">You can put a *\_PageStart.cshtml* file in the root of the site and in any subfolder.</span></span> <span data-ttu-id="242aa-187">请求页面时，位于最顶层的 *\_PageStart*文件（最接近站点根）将运行，后跟下一个子文件夹中的 *\_PageStart*文件，依此类推子文件夹结构，直到请求到达包含请求的页面的文件夹。</span><span class="sxs-lookup"><span data-stu-id="242aa-187">When a page is requested, the *\_PageStart.cshtml* file at the top-most level (nearest to the site root) runs, followed by the *\_PageStart.cshtml* file in the next subfolder, and so on down the subfolder structure until the request reaches the folder that contains the requested page.</span></span> <span data-ttu-id="242aa-188">在所有适用的 *\_PageStart*文件都已运行之后，将运行请求的页面。</span><span class="sxs-lookup"><span data-stu-id="242aa-188">After all the applicable *\_PageStart.cshtml* files have run, the requested page runs.</span></span>

<span data-ttu-id="242aa-189">例如，你可能有以下 *\_PageStart*文件和*默认的*# # 文件的组合：</span><span class="sxs-lookup"><span data-stu-id="242aa-189">For example, you might have the following combination of *\_PageStart.cshtml* files and *Default.cshtml* file:</span></span>

[!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample5.cshtml)]

[!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample6.cshtml)]

[!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample7.cshtml)]

<span data-ttu-id="242aa-190">运行 */myfolder/default.cshtml*时，将看到以下内容：</span><span class="sxs-lookup"><span data-stu-id="242aa-190">When you run */myfolder/default.cshtml*, you'll see the following:</span></span>

[!code-console[Main](18-customizing-site-wide-behavior/samples/sample8.cmd)]

## <a name="running-initialization-code-for-all-pages-in-a-folder"></a><span data-ttu-id="242aa-191">为文件夹中的所有页面运行初始化代码</span><span class="sxs-lookup"><span data-stu-id="242aa-191">Running Initialization Code for All Pages in a Folder</span></span>

<span data-ttu-id="242aa-192">*\_PageStart*文件的一个不错用途是为一个文件夹中的所有文件初始化相同的布局页。</span><span class="sxs-lookup"><span data-stu-id="242aa-192">A good use for *\_PageStart.cshtml* files is to initialize the same layout page for all files in a single folder.</span></span>

1. <span data-ttu-id="242aa-193">在根文件夹中，创建一个名为*InitPages*的新文件夹。</span><span class="sxs-lookup"><span data-stu-id="242aa-193">In the root folder, create a new folder named *InitPages*.</span></span>
2. <span data-ttu-id="242aa-194">在网站的*InitPages*文件夹中，创建一个名为 *\_PageStart*的文件，并将默认标记和代码替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="242aa-194">In the *InitPages* folder of your website, create a file named *\_PageStart.cshtml* and replace the default markup and code with the following:</span></span> 

    [!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample9.cshtml)]
3. <span data-ttu-id="242aa-195">在网站的根目录中，创建一个名为 "*共享*" 的文件夹。</span><span class="sxs-lookup"><span data-stu-id="242aa-195">In the root of the website, create a folder named *Shared*.</span></span>
4. <span data-ttu-id="242aa-196">在*共享*文件夹中，创建一个名为 *\_Layout1*的文件，并将默认标记和代码替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="242aa-196">In the *Shared* folder, create a file named *\_Layout1.cshtml* and replace the default markup and code with the following:</span></span> 

    [!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample10.cshtml)]
5. <span data-ttu-id="242aa-197">在*InitPages*文件夹中，创建一个名为*Content1*的文件，并将现有内容替换为以下内容：</span><span class="sxs-lookup"><span data-stu-id="242aa-197">In the *InitPages* folder, create a file named *Content1.cshtml* and replace the existing content with the following:</span></span> 

    [!code-html[Main](18-customizing-site-wide-behavior/samples/sample11.html)]
6. <span data-ttu-id="242aa-198">在*InitPages*文件夹中，创建另一个名为*Content2*的文件，并将默认标记替换为以下内容：</span><span class="sxs-lookup"><span data-stu-id="242aa-198">In the *InitPages* folder, create another file named *Content2.cshtml* and replace the default markup with the following:</span></span> 

    [!code-html[Main](18-customizing-site-wide-behavior/samples/sample12.html)]
7. <span data-ttu-id="242aa-199">在浏览器中运行*Content1* 。</span><span class="sxs-lookup"><span data-stu-id="242aa-199">Run *Content1.cshtml* in a browser.</span></span> 

    ![[图像]](18-customizing-site-wide-behavior/_static/image4.jpg)

    <span data-ttu-id="242aa-201">*Content1*页运行时， *\_PageStart*文件将设置 `Layout` 并将 `PageData["MyBackground"]` 设置为颜色。</span><span class="sxs-lookup"><span data-stu-id="242aa-201">When the *Content1.cshtml* page runs, the *\_PageStart.cshtml* file sets `Layout` and also sets `PageData["MyBackground"]` to a color.</span></span> <span data-ttu-id="242aa-202">在*Content1*中，将应用布局和颜色。</span><span class="sxs-lookup"><span data-stu-id="242aa-202">In *Content1.cshtml*, the layout and color are applied.</span></span>
8. <span data-ttu-id="242aa-203">在浏览器中显示*Content2* 。</span><span class="sxs-lookup"><span data-stu-id="242aa-203">Display *Content2.cshtml* in a browser.</span></span> 

    <span data-ttu-id="242aa-204">布局是相同的，因为这两个页使用 *\_PageStart*中的初始化的相同布局页和颜色。</span><span class="sxs-lookup"><span data-stu-id="242aa-204">The layout is the same, because both pages use the same layout page and color as initialized in *\_PageStart.cshtml*.</span></span>

## <a name="using-_pagestartcshtml-to-handle-errors"></a><span data-ttu-id="242aa-205">使用 \_PageStart 处理错误</span><span class="sxs-lookup"><span data-stu-id="242aa-205">Using \_PageStart.cshtml to Handle Errors</span></span>

<span data-ttu-id="242aa-206">*\_PageStart*文件的另一种不错的用途是创建一种方法来处理可能出现在文件夹中的任何*cshtml*页面的编程错误（异常）。</span><span class="sxs-lookup"><span data-stu-id="242aa-206">Another good use for the *\_PageStart.cshtml* file is to create a way to handle programming errors (exceptions) that might occur in any *.cshtml* page in a folder.</span></span> <span data-ttu-id="242aa-207">此示例演示了执行此操作的一种方法。</span><span class="sxs-lookup"><span data-stu-id="242aa-207">This example shows you one way to do this.</span></span>

1. <span data-ttu-id="242aa-208">在根文件夹中，创建一个名为*InitCatch*的文件夹。</span><span class="sxs-lookup"><span data-stu-id="242aa-208">In the root folder, create a folder named *InitCatch*.</span></span>
2. <span data-ttu-id="242aa-209">在网站的*InitCatch*文件夹中，创建一个名为 *\_PageStart*的文件，并将现有标记和代码替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="242aa-209">In the *InitCatch* folder of your website, create a file named *\_PageStart.cshtml* and replace the existing markup and code with the following:</span></span> 

    [!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample13.cshtml)]

    <span data-ttu-id="242aa-210">在此代码中，你尝试通过调用 `try` 块内的 `RunPage` 方法来显式运行请求的页面。</span><span class="sxs-lookup"><span data-stu-id="242aa-210">In this code, you try running the requested page explicitly by calling the `RunPage` method inside a `try` block.</span></span> <span data-ttu-id="242aa-211">如果请求的页面中出现任何编程错误，则会运行 `catch` 块中的代码。</span><span class="sxs-lookup"><span data-stu-id="242aa-211">If any programming errors occur in the requested page, the code inside the `catch` block runs.</span></span> <span data-ttu-id="242aa-212">在这种情况下，代码将重定向到页面（*错误. cshtml*），并将遇到错误的文件的名称作为 URL 的一部分传递。</span><span class="sxs-lookup"><span data-stu-id="242aa-212">In this case, the code redirects to a page (*Error.cshtml*) and passes the name of the file that experienced the error as part of the URL.</span></span> <span data-ttu-id="242aa-213">（稍后会创建页面。）</span><span class="sxs-lookup"><span data-stu-id="242aa-213">(You'll create the page shortly.)</span></span>
3. <span data-ttu-id="242aa-214">在网站的*InitCatch*文件夹中，创建一个名为*Exception*的文件，并将现有标记和代码替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="242aa-214">In the *InitCatch* folder of your website, create a file named *Exception.cshtml* and replace the existing markup and code with the following:</span></span> 

    [!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample14.cshtml)]

    <span data-ttu-id="242aa-215">在此示例中，在此页中所做的工作是通过尝试打开不存在的数据库文件来特意创建一个错误。</span><span class="sxs-lookup"><span data-stu-id="242aa-215">For purposes of this example, what you're doing in this page is deliberately creating an error by trying to open a database file that doesn't exist.</span></span>
4. <span data-ttu-id="242aa-216">在根文件夹中，创建一个名为 "*错误*" 的文件，并将现有标记和代码替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="242aa-216">In the root folder, create a file named *Error.cshtml* and replace the existing markup and code with the following:</span></span> 

    [!code-html[Main](18-customizing-site-wide-behavior/samples/sample15.html)]

    <span data-ttu-id="242aa-217">在此页中，表达式 `@Request["source"]` 获取 URL 的值并将其显示出来。</span><span class="sxs-lookup"><span data-stu-id="242aa-217">In this page, the expression `@Request["source"]` gets the value out of the URL and displays it.</span></span>
5. <span data-ttu-id="242aa-218">在工具栏中，单击 "**保存**"。</span><span class="sxs-lookup"><span data-stu-id="242aa-218">In the toolbar, click **Save**.</span></span>
6. <span data-ttu-id="242aa-219">在浏览器中运行*Exception。*</span><span class="sxs-lookup"><span data-stu-id="242aa-219">Run *Exception.cshtml* in a browser.</span></span> 

    ![[图像]](18-customizing-site-wide-behavior/_static/image5.jpg)

    <span data-ttu-id="242aa-221">由于*异常*中发生错误，因此 *\_PageStart*页面重定向到*错误 cshtml*文件，该文件将显示消息。</span><span class="sxs-lookup"><span data-stu-id="242aa-221">Because an error occurs in *Exception.cshtml*, the *\_PageStart.cshtml* page redirects to the *Error.cshtml* file, which displays the message.</span></span>

    <span data-ttu-id="242aa-222">有关异常的详细信息，请参阅[使用 Razor 语法 ASP.NET 网页编程简介](https://go.microsoft.com/fwlink/?LinkID=251587)。</span><span class="sxs-lookup"><span data-stu-id="242aa-222">For more information about exceptions, see [Introduction to ASP.NET Web Pages Programming Using the Razor Syntax](https://go.microsoft.com/fwlink/?LinkID=251587).</span></span>

<a id="Using__PageStart.cshtml_to_Restrict_Folder_Access"></a>
## <a name="using-_pagestartcshtml-to-restrict-folder-access"></a><span data-ttu-id="242aa-223">使用 \_PageStart 来限制文件夹访问</span><span class="sxs-lookup"><span data-stu-id="242aa-223">Using \_PageStart.cshtml to Restrict Folder Access</span></span>

<span data-ttu-id="242aa-224">你还可以使用 *\_PageStart*文件来限制对文件夹中所有文件的访问。</span><span class="sxs-lookup"><span data-stu-id="242aa-224">You can also use the *\_PageStart.cshtml* file to restrict access to all the files in a folder.</span></span>

1. <span data-ttu-id="242aa-225">在 WebMatrix 中，使用 "**从模板创建网站**" 选项创建新网站。</span><span class="sxs-lookup"><span data-stu-id="242aa-225">In WebMatrix, create a new website using the **Site From Template** option.</span></span>
2. <span data-ttu-id="242aa-226">从可用模板中选择 " **Starter Site**"。</span><span class="sxs-lookup"><span data-stu-id="242aa-226">From the available templates, select **Starter Site**.</span></span>
3. <span data-ttu-id="242aa-227">在根文件夹中，创建一个名为*AuthenticatedContent*的文件夹。</span><span class="sxs-lookup"><span data-stu-id="242aa-227">In the root folder, create a folder named *AuthenticatedContent*.</span></span>
4. <span data-ttu-id="242aa-228">在*AuthenticatedContent*文件夹中，创建一个名为 *\_PageStart*的文件，并将现有标记和代码替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="242aa-228">In the *AuthenticatedContent* folder, create a file named *\_PageStart.cshtml* and replace the existing markup and code with the following:</span></span> 

    [!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample16.cshtml)]

    <span data-ttu-id="242aa-229">代码首先阻止缓存文件夹中的所有文件。</span><span class="sxs-lookup"><span data-stu-id="242aa-229">The code starts by preventing all files in the folder from being cached.</span></span> <span data-ttu-id="242aa-230">（对于公共计算机这样的方案是必需的，在这种情况下，你不希望向下一个用户提供一个用户的缓存页面。）接下来，该代码确定用户是否已登录到站点，然后才能查看文件夹中的任何页面。</span><span class="sxs-lookup"><span data-stu-id="242aa-230">(This is required for scenarios like public computers, where you don't want one user's cached pages to be available to the next user.) Next, the code determines whether the user has signed in to the site before they can view any of the pages in the folder.</span></span> <span data-ttu-id="242aa-231">如果用户未登录，则代码将重定向到登录页。</span><span class="sxs-lookup"><span data-stu-id="242aa-231">If the user is not signed in, the code redirects to the login page.</span></span> <span data-ttu-id="242aa-232">如果包含名为 "`ReturnUrl`" 的查询字符串值，登录页可能会将用户返回到最初请求的页面。</span><span class="sxs-lookup"><span data-stu-id="242aa-232">The login page can return the user to the page that was originally requested if you include a query string value named `ReturnUrl`.</span></span>
5. <span data-ttu-id="242aa-233">在名为*AuthenticatedContent*的文件夹中创建一个新*页。*</span><span class="sxs-lookup"><span data-stu-id="242aa-233">Create a new page in the *AuthenticatedContent* folder named *Page.cshtml*.</span></span>
6. <span data-ttu-id="242aa-234">将默认标记替换为以下内容：</span><span class="sxs-lookup"><span data-stu-id="242aa-234">Replace the default markup with the following:</span></span>  

    [!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample17.cshtml)]
7. <span data-ttu-id="242aa-235">在浏览器中运行*页。*</span><span class="sxs-lookup"><span data-stu-id="242aa-235">Run *Page.cshtml* in a browser.</span></span> <span data-ttu-id="242aa-236">该代码会将您重定向到登录页。</span><span class="sxs-lookup"><span data-stu-id="242aa-236">The code redirects you to a login page.</span></span> <span data-ttu-id="242aa-237">必须在登录前注册。</span><span class="sxs-lookup"><span data-stu-id="242aa-237">You must register before logging in.</span></span> <span data-ttu-id="242aa-238">注册并登录后，可以导航到页面并查看其内容。</span><span class="sxs-lookup"><span data-stu-id="242aa-238">After you've registered and logged in, you can navigate to the page and view its contents.</span></span>

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a><span data-ttu-id="242aa-239">其他资源</span><span class="sxs-lookup"><span data-stu-id="242aa-239">Additional Resources</span></span>

[<span data-ttu-id="242aa-240">使用 Razor 语法 ASP.NET 网页编程简介</span><span class="sxs-lookup"><span data-stu-id="242aa-240">Introduction to ASP.NET Web Pages Programming Using the Razor Syntax</span></span>](https://go.microsoft.com/fwlink/?LinkID=251587)
