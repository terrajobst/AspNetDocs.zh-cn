---
uid: web-pages/overview/testing-and-debugging/aspnet-web-pages-razor-troubleshooting-guide
title: ASP.NET 网页（Razor）故障排除指南 |Microsoft Docs
author: Rick-Anderson
description: 本文介绍使用 ASP.NET 网页（Razor）和某些建议的解决方案时可能遇到的问题。 软件版本 ASP.NET Web 页的链接...
ms.author: riande
ms.date: 02/10/2014
ms.assetid: 2a2c1833-0bfe-4e2e-9cc0-341b52c7b121
msc.legacyurl: /web-pages/overview/testing-and-debugging/aspnet-web-pages-razor-troubleshooting-guide
msc.type: authoredcontent
ms.openlocfilehash: fc03767c16f46c1e282d24ee3a7df2409a7c38bb
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78473378"
---
# <a name="aspnet-web-pages-razor-troubleshooting-guide"></a><span data-ttu-id="13127-104">ASP.NET Web Pages (Razor) 疑难解答指南</span><span class="sxs-lookup"><span data-stu-id="13127-104">ASP.NET Web Pages (Razor) Troubleshooting Guide</span></span>

<span data-ttu-id="13127-105">作者： [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="13127-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="13127-106">本文介绍使用 ASP.NET 网页（Razor）和某些建议的解决方案时可能遇到的问题。</span><span class="sxs-lookup"><span data-stu-id="13127-106">This article describes issues that you might have when working with ASP.NET Web Pages (Razor) and some suggested solutions.</span></span>
> 
> ## <a name="software-versions"></a><span data-ttu-id="13127-107">软件版本</span><span class="sxs-lookup"><span data-stu-id="13127-107">Software versions</span></span>
> 
> 
> - <span data-ttu-id="13127-108">ASP.NET 网页（Razor）3</span><span class="sxs-lookup"><span data-stu-id="13127-108">ASP.NET Web Pages (Razor) 3</span></span>
>   
> 
> <span data-ttu-id="13127-109">本教程还适用于 ASP.NET 网页2和 ASP.NET 网页1.0。</span><span class="sxs-lookup"><span data-stu-id="13127-109">This tutorial also works with ASP.NET Web Pages 2 and ASP.NET Web Pages 1.0.</span></span>

<span data-ttu-id="13127-110">本主题包含以下各节：</span><span class="sxs-lookup"><span data-stu-id="13127-110">This topic contains the following sections:</span></span>

- [<span data-ttu-id="13127-111">正在运行的页面的问题</span><span class="sxs-lookup"><span data-stu-id="13127-111">Issues with Running Pages</span></span>](#Issues_Running_.cshtml_Pages)
- [<span data-ttu-id="13127-112">Razor 代码问题</span><span class="sxs-lookup"><span data-stu-id="13127-112">Issues with Razor Code</span></span>](#IssuesWithRazorCode)
- [<span data-ttu-id="13127-113">安全和成员身份问题</span><span class="sxs-lookup"><span data-stu-id="13127-113">Issues with Security and Membership</span></span>](#membership)
- [<span data-ttu-id="13127-114">发送电子邮件的问题</span><span class="sxs-lookup"><span data-stu-id="13127-114">Issues with Sending Email</span></span>](#email)
- [<span data-ttu-id="13127-115">其他资源</span><span class="sxs-lookup"><span data-stu-id="13127-115">Additional Resources</span></span>](#AdditionalResources)

<span data-ttu-id="13127-116">有关一般问题，请参阅[ASP.NET 网页（Razor）常见问题解答](https://go.microsoft.com/fwlink/?LinkId=253000)。</span><span class="sxs-lookup"><span data-stu-id="13127-116">For general questions, see [ASP.NET Web Pages (Razor) FAQ](https://go.microsoft.com/fwlink/?LinkId=253000).</span></span>

<a id="Issues_Running_.cshtml_Pages"></a>
## <a name="issues-with-running-pages"></a><span data-ttu-id="13127-117">正在运行的页面的问题</span><span class="sxs-lookup"><span data-stu-id="13127-117">Issues with Running Pages</span></span>

<span data-ttu-id="13127-118">许多问题都可能导致无法正常运行 *.*</span><span class="sxs-lookup"><span data-stu-id="13127-118">A variety of issues can prevent *.cshtml* and *.vbhtml* pages from running properly.</span></span> <span data-ttu-id="13127-119">本部分列出了常见的错误消息和可能的原因。</span><span class="sxs-lookup"><span data-stu-id="13127-119">This section lists common error messages and likely causes.</span></span>

### <a name="http-error-403---forbidden-access-is-denied"></a><span data-ttu-id="13127-120">HTTP 错误 403-禁止访问：访问被拒绝</span><span class="sxs-lookup"><span data-stu-id="13127-120">HTTP Error 403 - Forbidden: Access is denied</span></span>

<span data-ttu-id="13127-121">*您没有权限使用您提供的凭据查看此目录或页面。*</span><span class="sxs-lookup"><span data-stu-id="13127-121">*You do not have permission to view this directory or page using the credentials that you supplied.*</span></span>

<span data-ttu-id="13127-122">如果服务器未运行正确版本的 .NET Framework，则会发生此错误。</span><span class="sxs-lookup"><span data-stu-id="13127-122">This error can occur if the server is not running the correct version of the .NET Framework.</span></span> <span data-ttu-id="13127-123">请确保运行服务器的计算机（本地或远程）至少安装了 .NET Framework 4。</span><span class="sxs-lookup"><span data-stu-id="13127-123">Make sure that the computer that's running the server (locally or remotely) has at least the .NET Framework 4 installed.</span></span> <span data-ttu-id="13127-124">此外，请确保将应用程序本身配置为运行正确的版本。</span><span class="sxs-lookup"><span data-stu-id="13127-124">Also make sure that the application itself is configured to run the right version.</span></span>

<span data-ttu-id="13127-125">如果在 WebMatrix 中工作时本地发现此问题，请单击 "**站点**" 工作区，然后在 treeview 中单击 "**设置**"。</span><span class="sxs-lookup"><span data-stu-id="13127-125">If you see this problem locally while working in WebMatrix, click the **Site** workspace, and then in the treeview click **Settings**.</span></span> <span data-ttu-id="13127-126">在 "**选择 .NET Framework 版本**" 列表中，选择 " **.Net 4 （集成）** "。</span><span class="sxs-lookup"><span data-stu-id="13127-126">In the **Select .NET Framework Version** list, select **.NET 4 (Integrated)**.</span></span> <span data-ttu-id="13127-127">如果已设置此版本，请尝试以管理员身份运行 WebMatrix。</span><span class="sxs-lookup"><span data-stu-id="13127-127">If this version is already set, try running WebMatrix as an administrator.</span></span>

<span data-ttu-id="13127-128">请确保网站的根目录中至少包含一个*cshtml*文件。</span><span class="sxs-lookup"><span data-stu-id="13127-128">Make sure that the root of your website has at least one *.cshtml* file in it.</span></span>

<span data-ttu-id="13127-129">如果 web 服务器位于远程服务器上时看到此错误，请与服务器管理员联系。</span><span class="sxs-lookup"><span data-stu-id="13127-129">If you see this error when the web server is on a remote server, contact the server administrator.</span></span> <span data-ttu-id="13127-130">请确保已安装 .NET Framework 4 或更高版本的服务器。</span><span class="sxs-lookup"><span data-stu-id="13127-130">Make sure that the server has the .NET Framework 4 or later installed.</span></span> <span data-ttu-id="13127-131">此外，请确保应用程序在配置为使用该版本的 the.NET Framework 的应用程序池中运行。</span><span class="sxs-lookup"><span data-stu-id="13127-131">Also make sure that the application is running in an application pool that's configured to use that version of the.NET Framework.</span></span>

<span data-ttu-id="13127-132">如果你可以控制服务器，请确保它正在运行正确版本的 .NET Framework。</span><span class="sxs-lookup"><span data-stu-id="13127-132">If you have control over the server, make sure it's running the correct version of the .NET Framework.</span></span> <span data-ttu-id="13127-133">你还可以尝试通过运行 `aspnet_regiis -iru` 命令来修复安装。</span><span class="sxs-lookup"><span data-stu-id="13127-133">You might also try repairing the installation by running the `aspnet_regiis -iru` command.</span></span> <span data-ttu-id="13127-134">（例如，如果在安装 .NET Framework 后安装 IIS，则 IIS 将不会正确配置为运行 ASP.NET 页面。）有关详细信息，请参阅[ASP.NET IIS 注册工具（Aspnet\_regiis）](https://msdn.microsoft.com/library/k6h9cz8h(v=vs.100).aspx)。</span><span class="sxs-lookup"><span data-stu-id="13127-134">(For example, if you install IIS after you install the .NET Framework, IIS will not be correctly configured to run ASP.NET pages.) For more information, see [ASP.NET IIS Registration Tool (Aspnet\_regiis.exe)](https://msdn.microsoft.com/library/k6h9cz8h(v=vs.100).aspx).</span></span>

### <a name="http-error-40314---forbidden"></a><span data-ttu-id="13127-135">HTTP 错误 403.14-禁止访问</span><span class="sxs-lookup"><span data-stu-id="13127-135">HTTP Error 403.14 - Forbidden</span></span>

<span data-ttu-id="13127-136">*Web 服务器被配置为不列出此目录的内容。*</span><span class="sxs-lookup"><span data-stu-id="13127-136">*The Web server is configured to not list the contents of this directory.*</span></span>

<span data-ttu-id="13127-137">如果请求受保护的资源（如*web.config 文件）* 或在受保护的文件夹中（例如*应用\_数据*或*应用\_代码*），则会发生此错误。</span><span class="sxs-lookup"><span data-stu-id="13127-137">This error can occur if you request a resource that's protected (like the *Web.config* file) or that's in a folder that's protected (like *App\_Data* or *App\_Code*).</span></span>

### <a name="http-error-40417---not-found"></a><span data-ttu-id="13127-138">HTTP 错误 404.17-未找到</span><span class="sxs-lookup"><span data-stu-id="13127-138">HTTP Error 404.17 - Not Found</span></span>

<span data-ttu-id="13127-139">*请求的内容将显示为脚本，而不会由静态文件处理程序提供。*</span><span class="sxs-lookup"><span data-stu-id="13127-139">*The requested content appears to be script and will not be served by the static file handler.*</span></span>

<span data-ttu-id="13127-140">如果服务器未正确配置为使用 .NET Framework 4 或更高版本，则可能发生此错误，因此无法识别 `@{ }` 块中的代码。</span><span class="sxs-lookup"><span data-stu-id="13127-140">This error can occur if the server is not configured correctly to use the .NET Framework 4 or later, and therefore does not recognize the code in `@{ }` blocks.</span></span> <span data-ttu-id="13127-141">请参阅前面的说明，了解*HTTP 错误 403-禁止访问：访问被拒绝*。</span><span class="sxs-lookup"><span data-stu-id="13127-141">See the description earlier for *HTTP Error 403 - Forbidden: Access is denied*.</span></span>

### <a name="http-error-4047---not-found"></a><span data-ttu-id="13127-142">HTTP 错误 404.7-未找到</span><span class="sxs-lookup"><span data-stu-id="13127-142">HTTP Error 404.7 - Not Found</span></span>

<span data-ttu-id="13127-143">*请求筛选模块被配置为拒绝文件扩展名*</span><span class="sxs-lookup"><span data-stu-id="13127-143">*The request filtering module is configured to deny the file extension*</span></span>

<span data-ttu-id="13127-144">如果已在服务器上显式阻止了*cshtml*或*vbhtml*扩展，则会出现此错误。</span><span class="sxs-lookup"><span data-stu-id="13127-144">This error can occur if *.cshtml* or *.vbhtml* extensions have been explicitly blocked on the server.</span></span> <span data-ttu-id="13127-145">此问题的症状在于，当 Url 不包含扩展名时，它们会正常工作，但包含 *.*</span><span class="sxs-lookup"><span data-stu-id="13127-145">A symptom of this problem is that URLs work when they do not include the extension, but URLs that include *.cshtml* or *.vbhtml* do not work.</span></span> <span data-ttu-id="13127-146">一种可能的解决方案是重新启用站点的*web.config 文件中的扩展*。</span><span class="sxs-lookup"><span data-stu-id="13127-146">A possible solution is to re-enable the extensions in the site's *Web.config* file.</span></span> <span data-ttu-id="13127-147">下面的示例演示如何启用 *.* # 扩展名。</span><span class="sxs-lookup"><span data-stu-id="13127-147">The following example shows how to enable the *.cshtml* extension.</span></span>

[!code-xml[Main](aspnet-web-pages-razor-troubleshooting-guide/samples/sample1.xml?highlight=5-6)]

### <a name="http-error-4048---not-found"></a><span data-ttu-id="13127-148">HTTP 错误 404.8-未找到</span><span class="sxs-lookup"><span data-stu-id="13127-148">HTTP Error 404.8 - Not Found</span></span>

<span data-ttu-id="13127-149">*请求筛选模块被配置为拒绝包含 hiddenSegment 部分的 URL 中的路径。*</span><span class="sxs-lookup"><span data-stu-id="13127-149">*The request filtering module is configured to deny a path in the URL that contains a hiddenSegment section.*</span></span>

<span data-ttu-id="13127-150">如果请求受保护的资源（如*web.config 文件）* 或在受保护的文件夹中（例如*应用\_数据*或*应用\_代码*），则会发生此错误。</span><span class="sxs-lookup"><span data-stu-id="13127-150">This error can occur if you request a resource that's protected (like the *Web.config* file) or that's in a folder that's protected (like *App\_Data* or *App\_Code*).</span></span>

### <a name="this-type-of-page-is-not-served-server-error-in--application"></a><span data-ttu-id="13127-151">此类型的页未提供（"/" 应用程序中的服务器错误）</span><span class="sxs-lookup"><span data-stu-id="13127-151">This type of page is not served (Server Error in '/' Application)</span></span>

<span data-ttu-id="13127-152">请参阅前面的说明，了解 HTTP 错误404.17。</span><span class="sxs-lookup"><span data-stu-id="13127-152">See the description earlier for HTTP Error 404.17.</span></span>

<a id="IssuesWithRazorCode"></a>
## <a name="issues-with-razor-code"></a><span data-ttu-id="13127-153">Razor 代码问题</span><span class="sxs-lookup"><span data-stu-id="13127-153">Issues with Razor code</span></span>

### <a name="the-name-class-does-not-exist-in-the-current-context"></a><span data-ttu-id="13127-154">当前上下文中不存在名称 "*class*"</span><span class="sxs-lookup"><span data-stu-id="13127-154">The name '*class*' does not exist in the current context</span></span>

<span data-ttu-id="13127-155">通常情况下，出现此错误的原因是 `class` 引用了帮助程序，但未安装帮助器。</span><span class="sxs-lookup"><span data-stu-id="13127-155">Often, a reason you see this error is that `class` references a helper, but the helper is not installed.</span></span> <span data-ttu-id="13127-156">例如，如果你尝试使用帮助程序，但如果尚未从 NuGet 安装包，则会看到此错误。</span><span class="sxs-lookup"><span data-stu-id="13127-156">For example, if you try to use a helper, but if you haven't installed the package from NuGet, you'll see this error.</span></span> <span data-ttu-id="13127-157">使用 WebMatrix 中的库查找并安装帮助程序。</span><span class="sxs-lookup"><span data-stu-id="13127-157">Use the Gallery in WebMatrix to find and install the helper.</span></span>

<span data-ttu-id="13127-158">如果帮助程序已安装，但页面仍无法识别，请尝试向代码添加 `using` 语句。</span><span class="sxs-lookup"><span data-stu-id="13127-158">If the helper is installed, but the page still doesn't recognize it, try adding add a `using` statement to the code.</span></span> <span data-ttu-id="13127-159">在 `using` 语句中，引用包含帮助器的命名空间。</span><span class="sxs-lookup"><span data-stu-id="13127-159">In the `using` statement, reference the namespace that includes the helper.</span></span> <span data-ttu-id="13127-160">例如，ASP.NET Web 帮助程序包中的基本帮助程序位于 `System.Web.Helpers` 命名空间中。</span><span class="sxs-lookup"><span data-stu-id="13127-160">For example, the basic helpers that are in the ASP.NET Web Helpers package are in the `System.Web.Helpers` namespace.</span></span> <span data-ttu-id="13127-161">在要使用帮助器的页面的顶部，添加以下行：</span><span class="sxs-lookup"><span data-stu-id="13127-161">At the top of the page where you want to use the helper, add this line:</span></span>

`@using Microsoft.Web.Helpers;`

<a id="membership"></a>
## <a name="issues-with-security-and-membership"></a><span data-ttu-id="13127-162">安全和成员身份问题</span><span class="sxs-lookup"><span data-stu-id="13127-162">Issues with Security and Membership</span></span>

<span data-ttu-id="13127-163">如果在 ASP.NET 网页（Razor）中使用内置安全（成员）系统，则可能会遇到以下问题。</span><span class="sxs-lookup"><span data-stu-id="13127-163">If you are using the built-in security (membership) system in ASP.NET Web Pages (Razor), you might encounter the following issues.</span></span>

### <a name="to-call-this-method-the-membershipprovider-property-must-be-an-instance-of-extendedmembershipprovider"></a><span data-ttu-id="13127-164">若要调用此方法，"成员身份提供程序" 属性必须是 "ExtendedMembershipProvider" 的实例</span><span class="sxs-lookup"><span data-stu-id="13127-164">To call this method, the "Membership.Provider" property must be an instance of "ExtendedMembershipProvider"</span></span>

<span data-ttu-id="13127-165">此错误可能表示没有配置 `AspNetSqlMembershipProvider` 类。</span><span class="sxs-lookup"><span data-stu-id="13127-165">This error can indicate that no `AspNetSqlMembershipProvider` class is configured.</span></span> <span data-ttu-id="13127-166">（症状是站点在本地正常运行，但在将其发布到托管提供商的服务器时，会引发此错误。）此问题的一种解决方法是通过向站点的*web.config 文件添加*以下内容来显式启用简单成员身份：</span><span class="sxs-lookup"><span data-stu-id="13127-166">(A symptom is that the site works fine locally but throws this error when you publish it to a hosting provider's server.) One fix for this problem is to explicitly enable simple membership by adding the following to the site's *Web.config* file:</span></span>

[!code-xml[Main](aspnet-web-pages-razor-troubleshooting-guide/samples/sample2.xml?highlight=6)]

<a id="email"></a>
## <a name="issues-with-sending-email"></a><span data-ttu-id="13127-167">发送电子邮件的问题</span><span class="sxs-lookup"><span data-stu-id="13127-167">Issues with Sending Email</span></span>

<span data-ttu-id="13127-168">对于发送电子邮件的问题，调试起来可能很困难。</span><span class="sxs-lookup"><span data-stu-id="13127-168">Problems with sending email can be challenging to debug.</span></span> <span data-ttu-id="13127-169">初始问题可能是无法连接到 SMTP 服务器。</span><span class="sxs-lookup"><span data-stu-id="13127-169">An initial problem can be that you can't connect to the SMTP server.</span></span> <span data-ttu-id="13127-170">如果连接成功，ASP.NET 将消息发送到 SMTP 服务器。</span><span class="sxs-lookup"><span data-stu-id="13127-170">If the connection is successful, ASP.NET hands the message off to the SMTP server.</span></span> <span data-ttu-id="13127-171">但是，导致 SMTP 服务器无法发送的消息本身可能存在问题。</span><span class="sxs-lookup"><span data-stu-id="13127-171">However, there can be problems with the message itself that prevents the SMTP server from sending it.</span></span>

<span data-ttu-id="13127-172">如果你的应用程序未成功发送电子邮件，请尝试以下操作：</span><span class="sxs-lookup"><span data-stu-id="13127-172">If your application does not successfully send email, try the following:</span></span>

- <span data-ttu-id="13127-173">SMTP 服务器名称通常类似于 `smtp.provider.com` 或 `smtp.provider.net`。</span><span class="sxs-lookup"><span data-stu-id="13127-173">The SMTP server name is often something like `smtp.provider.com` or `smtp.provider.net`.</span></span> <span data-ttu-id="13127-174">但是，如果将网站发布到宿主提供程序，此时可能会 `localhost`该点的 SMTP 服务器名称。</span><span class="sxs-lookup"><span data-stu-id="13127-174">However, if you publish your site to a hosting provider, the SMTP server name at that point might be `localhost`.</span></span> <span data-ttu-id="13127-175">出现这种情况的原因是，在发布并在提供程序的服务器上运行了站点后，SMTP 服务器可能从应用程序的角度来看是本地的。</span><span class="sxs-lookup"><span data-stu-id="13127-175">This situation occurs because after you've published and your site is running on the provider's server, the SMTP server might be local from the perspective of your application.</span></span> <span data-ttu-id="13127-176">服务器名称中的这一更改可能意味着必须在发布过程中更改 SMTP 服务器名称。</span><span class="sxs-lookup"><span data-stu-id="13127-176">This change in server names might mean that you have to change the SMTP server name as part of your publishing process.</span></span>
- <span data-ttu-id="13127-177">端口号通常为25。</span><span class="sxs-lookup"><span data-stu-id="13127-177">The port number is usually 25.</span></span> <span data-ttu-id="13127-178">但是，某些提供程序要求使用端口587或其他端口。</span><span class="sxs-lookup"><span data-stu-id="13127-178">However, some providers require you to use port 587 or some other port.</span></span> <span data-ttu-id="13127-179">向 SMTP 服务器的所有者咨询他们希望使用的端口号。</span><span class="sxs-lookup"><span data-stu-id="13127-179">Check with the owner of the SMTP server what port number they expect you to use.</span></span>
- <span data-ttu-id="13127-180">请确保使用正确的凭据。</span><span class="sxs-lookup"><span data-stu-id="13127-180">Make sure that you use the right credentials.</span></span> <span data-ttu-id="13127-181">如果你已将站点发布到托管提供商，请使用提供商专门指出的凭据来发送电子邮件。</span><span class="sxs-lookup"><span data-stu-id="13127-181">If you've published your site to a hosting provider, use the credentials that the provider has specifically indicated are for email.</span></span> <span data-ttu-id="13127-182">这些凭据可能不同于用于发布的凭据。</span><span class="sxs-lookup"><span data-stu-id="13127-182">These credentials might be different from the credentials you use to publish.</span></span>
- <span data-ttu-id="13127-183">有时你根本不需要凭据。</span><span class="sxs-lookup"><span data-stu-id="13127-183">Sometimes you don't need credentials at all.</span></span> <span data-ttu-id="13127-184">如果你使用个人 ISP 发送电子邮件，则电子邮件提供商可能已知道你的凭据。</span><span class="sxs-lookup"><span data-stu-id="13127-184">If you're sending email by using your personal ISP, your email provider might already know your credentials.</span></span> <span data-ttu-id="13127-185">发布后，可能需要使用不同于在本地计算机上进行测试时使用的凭据。</span><span class="sxs-lookup"><span data-stu-id="13127-185">After you publish, you might need to use different credentials than when you test on your local computer.</span></span>
- <span data-ttu-id="13127-186">如果电子邮件提供程序使用加密，请将 `WebMail.EnableSsl` 设置为 `true`。</span><span class="sxs-lookup"><span data-stu-id="13127-186">If your email provider uses encryption, set `WebMail.EnableSsl` to `true`.</span></span>

<span data-ttu-id="13127-187">如果发送电子邮件时出错，可能会看到标准 ASP.NET 错误消息，如下所示：</span><span class="sxs-lookup"><span data-stu-id="13127-187">If there is an error sending email, you might see a standard ASP.NET error message, which looks like this:</span></span>

![电子邮件出现问题时出现 ASP.NET 错误消息](aspnet-web-pages-razor-troubleshooting-guide/_static/image1.png)

<span data-ttu-id="13127-189">你还可以使用 `try-catch` 块调试发送电子邮件的问题，如以下示例中所示。</span><span class="sxs-lookup"><span data-stu-id="13127-189">You can also debug problems with sending email by using a `try-catch` block, as in the following example.</span></span> <span data-ttu-id="13127-190">使用 `try-catch` 块时，ASP.NET 不会显示其标准错误消息。</span><span class="sxs-lookup"><span data-stu-id="13127-190">When you use a `try-catch` block, ASP.NET does not display its standard error messages.</span></span> <span data-ttu-id="13127-191">相反，你可以在块的 `catch` 部分捕获该错误。</span><span class="sxs-lookup"><span data-stu-id="13127-191">Instead, you can capture the error in the `catch` portion of the block.</span></span>

[!code-cshtml[Main](aspnet-web-pages-razor-troubleshooting-guide/samples/sample3.cshtml)]

<span data-ttu-id="13127-192">用适当的值替换 `your-SMTP-server-name`等。</span><span class="sxs-lookup"><span data-stu-id="13127-192">Substitute the appropriate values for `your-SMTP-server-name`, and so on.</span></span> <span data-ttu-id="13127-193">此方法可能会出现以下错误消息：</span><span class="sxs-lookup"><span data-stu-id="13127-193">Some of the error messages you might see this way include the following:</span></span>

- <span data-ttu-id="13127-194">*发送邮件失败。*</span><span class="sxs-lookup"><span data-stu-id="13127-194">*Failure sending mail.*</span></span>

    <span data-ttu-id="13127-195">或</span><span class="sxs-lookup"><span data-stu-id="13127-195">-or-</span></span>

    <span data-ttu-id="13127-196">*由于连接的参与方在一段时间后未正确响应，连接尝试失败，或者已建立连接失败，因为连接的主机无法响应*</span><span class="sxs-lookup"><span data-stu-id="13127-196">*A connection attempt failed because the connected party did not properly respond after a period of time, or established connection failed because connected host has failed to respond*</span></span>

    <span data-ttu-id="13127-197">此错误通常表示应用程序无法连接到 SMTP 服务器。</span><span class="sxs-lookup"><span data-stu-id="13127-197">This error usually means that the application could not connect to the SMTP server.</span></span> <span data-ttu-id="13127-198">请检查服务器名称和端口号。</span><span class="sxs-lookup"><span data-stu-id="13127-198">Check the server name and port number.</span></span>
- <span data-ttu-id="13127-199">*邮箱不可用。服务器响应为： 5.1.0 &lt;someuser@invaliddomain&gt; 发送方已拒绝：无效的发送方域*</span><span class="sxs-lookup"><span data-stu-id="13127-199">*Mailbox unavailable. The server response was: 5.1.0 &lt;someuser@invaliddomain&gt; sender rejected : invalid sender domain*</span></span>

    <span data-ttu-id="13127-200">此消息可能表示 `From` 地址不正确或缺失。</span><span class="sxs-lookup"><span data-stu-id="13127-200">This message can indicate that the `From` address is not correct or is missing.</span></span>
- <span data-ttu-id="13127-201">*指定的字符串不是电子邮件地址所需的形式。*</span><span class="sxs-lookup"><span data-stu-id="13127-201">*The specified string is not in the form required for an email address.*</span></span>

    <span data-ttu-id="13127-202">此错误可能表示 `To` 或 `From` 属性的值未被识别为电子邮件地址。</span><span class="sxs-lookup"><span data-stu-id="13127-202">This error might indicate that the value of the `To` or `From` properties are not recognized as email addresses.</span></span> <span data-ttu-id="13127-203">（ASP.NET 无法检查电子邮件地址是否有效，只是其格式正确，如 *name@domain.com* 。）</span><span class="sxs-lookup"><span data-stu-id="13127-203">(ASP.NET cannot check that the email address is valid, only that it's in the correct format, like *name@domain.com*.)</span></span>

> [!NOTE]
> <span data-ttu-id="13127-204">在将页面发布到活动站点之前，请删除显示错误（`@errorMessage`）的标记。</span><span class="sxs-lookup"><span data-stu-id="13127-204">Remove the markup that displays the error (`@errorMessage`) before you publish the page to a live site.</span></span> <span data-ttu-id="13127-205">最好不要让用户看到从服务器获得的错误消息。</span><span class="sxs-lookup"><span data-stu-id="13127-205">It's not a good idea to let users see error messages that you get from a server.</span></span>

<a id="AdditionalResources"></a>
## <a name="additional-resources"></a><span data-ttu-id="13127-206">其他资源</span><span class="sxs-lookup"><span data-stu-id="13127-206">Additional Resources</span></span>

[<span data-ttu-id="13127-207">ASP.NET 网页 (Razor) 常见问题解答</span><span class="sxs-lookup"><span data-stu-id="13127-207">ASP.NET Web Pages (Razor) FAQ</span></span>](https://go.microsoft.com/fwlink/?LinkId=253000)

<span data-ttu-id="13127-208">ASP.NET 网站上的[WebMatrix 和 ASP.NET 网页](https://forums.asp.net/1224.aspx/1?WebMatrix)论坛</span><span class="sxs-lookup"><span data-stu-id="13127-208">[WebMatrix and ASP.NET Web Pages](https://forums.asp.net/1224.aspx/1?WebMatrix) forum on the ASP.NET website</span></span>
