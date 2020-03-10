---
uid: whitepapers/aspnet4/breaking-changes
title: ASP.NET 4 重大更改 |Microsoft Docs
author: rick-anderson
description: 本文档介绍了对 .NET Framework 版本4版本进行的更改，这些更改可能会影响使用 。
ms.author: riande
ms.date: 02/10/2010
ms.assetid: d601c540-f86b-4feb-890c-20c806b3da6c
msc.legacyurl: /whitepapers/aspnet4/breaking-changes
msc.type: content
ms.openlocfilehash: 8ccad3b40a723c92a3164de082e1f94577141008
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78439508"
---
# <a name="aspnet-4-breaking-changes"></a><span data-ttu-id="a4c77-103">ASP.NET 4 重大更改</span><span class="sxs-lookup"><span data-stu-id="a4c77-103">ASP.NET 4 Breaking Changes</span></span>

> <span data-ttu-id="a4c77-104">本文档介绍了对 .NET Framework 版本4版本进行的更改，这些更改可能会影响使用早期版本（包括 ASP.NET 4 Beta 1 和 Beta 2 版）创建的应用程序。</span><span class="sxs-lookup"><span data-stu-id="a4c77-104">This document describes changes that have been made for the .NET Framework version 4 release that can potentially affect applications that were created using earlier releases, including the ASP.NET 4 Beta 1 and Beta 2 releases.</span></span>
> 
> [<span data-ttu-id="a4c77-105">下载此白皮书</span><span class="sxs-lookup"><span data-stu-id="a4c77-105">Download This Whitepaper</span></span>](https://download.microsoft.com/download/7/1/A/71A105A9-89D6-4201-9CC5-AD6A3B7E2F22/ASP_NET_4_Breaking_Changes.pdf)

<a id="0.1__Toc256768952"></a><a id="0.1__Toc256770056"></a>

## <a name="contents"></a><span data-ttu-id="a4c77-106">内容</span><span class="sxs-lookup"><span data-stu-id="a4c77-106">Contents</span></span>

[<span data-ttu-id="a4c77-107">Web.config 文件中的 ControlRenderingCompatibilityVersion 设置</span><span class="sxs-lookup"><span data-stu-id="a4c77-107">ControlRenderingCompatibilityVersion Setting in the Web.config File</span></span>](#0.1__Toc256770141 "_Toc256770141")  
[<span data-ttu-id="a4c77-108">ClientIDMode 更改</span><span class="sxs-lookup"><span data-stu-id="a4c77-108">ClientIDMode Changes</span></span>](#0.1__Toc256770142 "_Toc256770142")  
[<span data-ttu-id="a4c77-109">Server.htmlencode 和 UrlEncode 现在对单引号进行编码</span><span class="sxs-lookup"><span data-stu-id="a4c77-109">HtmlEncode and UrlEncode Now Encode Single Quotation Marks</span></span>](#0.1__Toc256770143 "_Toc256770143")  
[<span data-ttu-id="a4c77-110">ASP.NET 页（.aspx）分析器更严格</span><span class="sxs-lookup"><span data-stu-id="a4c77-110">ASP.NET Page (.aspx) Parser is Stricter</span></span>](#0.1__Toc256770144 "_Toc256770144")  
[<span data-ttu-id="a4c77-111">已更新浏览器定义文件</span><span class="sxs-lookup"><span data-stu-id="a4c77-111">Browser Definition Files Updated</span></span>](#0.1__Toc256770145 "_Toc256770145")  
[<span data-ttu-id="a4c77-112">从根 Web 配置文件中删除了 system.web. .dll</span><span class="sxs-lookup"><span data-stu-id="a4c77-112">System.Web.Mobile.dll Removed from Root Web Configuration File</span></span>](#0.1__Toc256770146 "_Toc256770146")  
[<span data-ttu-id="a4c77-113">ASP.NET 请求验证</span><span class="sxs-lookup"><span data-stu-id="a4c77-113">ASP.NET Request Validation</span></span>](#0.1__Toc256770147 "_Toc256770147")  
[<span data-ttu-id="a4c77-114">默认哈希算法现在为 HMACSHA256</span><span class="sxs-lookup"><span data-stu-id="a4c77-114">Default Hashing Algorithm Is Now HMACSHA256</span></span>](#0.1__Toc256770148 "_Toc256770148")  
[<span data-ttu-id="a4c77-115">与新的 ASP.NET 4 根配置相关的配置错误</span><span class="sxs-lookup"><span data-stu-id="a4c77-115">Configuration Errors Related to New ASP.NET 4 Root Configuration</span></span>](#0.1__Toc256770149 "_Toc256770149")  
[<span data-ttu-id="a4c77-116">ASP.NET 4 子应用程序在 ASP.NET 2.0 或 ASP.NET 3.5 应用程序下无法启动</span><span class="sxs-lookup"><span data-stu-id="a4c77-116">ASP.NET 4 Child Applications Fail to Start When Under ASP.NET 2.0 or ASP.NET 3.5 Applications</span></span>](#0.1__Toc256770150 "_Toc256770150")  
[<span data-ttu-id="a4c77-117">ASP.NET 4 网站无法在安装了 SharePoint 的计算机上启动</span><span class="sxs-lookup"><span data-stu-id="a4c77-117">ASP.NET 4 Web Sites Fail to Start on Computers Where SharePoint Is Installed</span></span>](#0.1__Toc256770151 "_Toc256770151")  
[<span data-ttu-id="a4c77-118">HttpRequest 属性不再包括 PathInfo 值</span><span class="sxs-lookup"><span data-stu-id="a4c77-118">The HttpRequest.FilePath Property No Longer Includes PathInfo Values</span></span>](#0.1__Toc256770152 "_Toc256770152")  
[<span data-ttu-id="a4c77-119">ASP.NET 2.0 应用程序可能生成引用 eurl 的 HttpException 错误</span><span class="sxs-lookup"><span data-stu-id="a4c77-119">ASP.NET 2.0 Applications Might Generate HttpException Errors that Reference eurl.axd</span></span>](#0.1__Toc256770153 "_Toc256770153")  
[<span data-ttu-id="a4c77-120">IIS 7 或 IIS 7.5 集成模式下的默认文档中可能不会引发事件处理程序</span><span class="sxs-lookup"><span data-stu-id="a4c77-120">Event Handlers Might Not Be Not Raised in a Default Document in IIS 7 or IIS 7.5 Integrated Mode</span></span>](#0.1__Toc256770154 "_Toc256770154")  
[<span data-ttu-id="a4c77-121">对 ASP.NET 代码访问安全性（CAS）实现的更改</span><span class="sxs-lookup"><span data-stu-id="a4c77-121">Changes to the ASP.NET Code Access Security (CAS) Implementation</span></span>](#0.1__Toc256770155 "_Toc256770155")  
[<span data-ttu-id="a4c77-122">MembershipUser 命名空间中的其他类型已移动</span><span class="sxs-lookup"><span data-stu-id="a4c77-122">MembershipUser and Other Types in the System.Web.Security Namespace Have Been Moved</span></span>](#0.1__Toc256770156 "_Toc256770156")  
[<span data-ttu-id="a4c77-123">\* HTTP 标头变化的输出缓存更改</span><span class="sxs-lookup"><span data-stu-id="a4c77-123">Output Caching Changes to Vary \* HTTP Header</span></span>](#0.1__Toc256770157 "_Toc256770157")  
[<span data-ttu-id="a4c77-124">Passport 的安全类型已过时</span><span class="sxs-lookup"><span data-stu-id="a4c77-124">System.Web.Security Types for Passport are Obsolete</span></span>](#0.1__Toc256770158 "_Toc256770158")  
[<span data-ttu-id="a4c77-125">PopOutImageUrl 属性未能呈现 ASP.NET 4 中的图像</span><span class="sxs-lookup"><span data-stu-id="a4c77-125">The MenuItem.PopOutImageUrl Property Fails to Render an Image in ASP.NET 4</span></span>](#0.1__Toc256770159 "_Toc256770159")  
[<span data-ttu-id="a4c77-126">当路径包含反斜杠时，StaticPopOutImageUrl 和 DynamicPopOutImageUrl 无法呈现图像</span><span class="sxs-lookup"><span data-stu-id="a4c77-126">Menu.StaticPopOutImageUrl and Menu.DynamicPopOutImageUrl Fail to Render Images When Paths Contain Backslashes</span></span>](#0.1__Toc256770160 "_Toc256770160")  
[<span data-ttu-id="a4c77-127">否认</span><span class="sxs-lookup"><span data-stu-id="a4c77-127">Disclaimer</span></span>](#0.1__Toc256770161 "_Toc256770161")

<a id="0.1__ControlRenderingCompatibilityVersio"></a><a id="0.1__Toc245724853"></a><a id="0.1__Toc255587630"></a><a id="0.1__Toc256770141"></a>

## <a name="controlrenderingcompatibilityversion-setting-in-the-webconfig-file"></a><span data-ttu-id="a4c77-128">Web.config 文件中的 ControlRenderingCompatibilityVersion 设置</span><span class="sxs-lookup"><span data-stu-id="a4c77-128">ControlRenderingCompatibilityVersion Setting in the Web.config File</span></span>

<span data-ttu-id="a4c77-129">.NET Framework 版本4中修改了 ASP.NET 控件，以便更准确地指定它们呈现标记的方式。</span><span class="sxs-lookup"><span data-stu-id="a4c77-129">ASP.NET controls have been modified in the .NET Framework version 4 in order to let you specify more precisely how they render markup.</span></span> <span data-ttu-id="a4c77-130">在以前版本的 .NET Framework 中，某些控件发出了你无法禁用的标记。</span><span class="sxs-lookup"><span data-stu-id="a4c77-130">In previous versions of the .NET Framework, some controls emitted markup that you had no way to disable.</span></span> <span data-ttu-id="a4c77-131">默认情况下，ASP.NET 4 不再生成这种类型的标记。</span><span class="sxs-lookup"><span data-stu-id="a4c77-131">By default, ASP.NET 4 this type of markup is no longer generated.</span></span>

<span data-ttu-id="a4c77-132">如果使用 Visual Studio 2010 从 ASP.NET 2.0 或 ASP.NET 3.5 升级应用程序，则该工具会自动将设置添加到保留旧呈现的 `Web.config` 文件中。</span><span class="sxs-lookup"><span data-stu-id="a4c77-132">If you use Visual Studio 2010 to upgrade your application from ASP.NET 2.0 or ASP.NET 3.5, the tool automatically adds a setting to the `Web.config` file that preserves legacy rendering.</span></span> <span data-ttu-id="a4c77-133">但是，如果通过在 IIS 中将应用程序池更改为面向 .NET Framework 4 来升级应用程序，ASP.NET 默认使用新的呈现模式。</span><span class="sxs-lookup"><span data-stu-id="a4c77-133">However, if you upgrade an application by changing the application pool in IIS to target the .NET Framework 4, ASP.NET uses the new rendering mode by default.</span></span> <span data-ttu-id="a4c77-134">若要禁用新的呈现模式，请在 `Web.config` 文件中添加以下设置：</span><span class="sxs-lookup"><span data-stu-id="a4c77-134">To disable the new rendering mode, add the following setting in the `Web.config` file:</span></span>

[!code-xml[Main](breaking-changes/samples/sample1.xml)]

<span data-ttu-id="a4c77-135">新行为带来的主要呈现变化如下：</span><span class="sxs-lookup"><span data-stu-id="a4c77-135">The major rendering changes that the new behavior brings are as follows:</span></span>

- <span data-ttu-id="a4c77-136">**Image**和**ImageButton**控件不再呈现 `border="0"` 特性。</span><span class="sxs-lookup"><span data-stu-id="a4c77-136">The **Image** and **ImageButton** controls no longer render a `border="0"` attribute.</span></span>
- <span data-ttu-id="a4c77-137">默认情况下，从派生的**BaseValidator**类和验证控件不再呈现红色文本。</span><span class="sxs-lookup"><span data-stu-id="a4c77-137">The **BaseValidator** class and validation controls that derive from it no longer render red text by default.</span></span>
- <span data-ttu-id="a4c77-138">**HtmlForm**控件不呈现**name**特性。</span><span class="sxs-lookup"><span data-stu-id="a4c77-138">The **HtmlForm** control does not render a **name** attribute.</span></span>
- <span data-ttu-id="a4c77-139">**Table**控件不再呈现 `border="0"` 特性。</span><span class="sxs-lookup"><span data-stu-id="a4c77-139">The **Table** control no longer renders a `border="0"` attribute.</span></span>
- <span data-ttu-id="a4c77-140">如果控件的**Enabled**属性设置为**false** （或从容器控件继承此设置），则不是为用户输入（例如**标签**控件）设计的控件将不再呈现 `disabled="disabled"` 特性。</span><span class="sxs-lookup"><span data-stu-id="a4c77-140">Controls that are not designed for user input (for example, the **Label** control) no longer render the `disabled="disabled"` attribute if their **Enabled** property is set to **false** (or if they inherit this setting from a container control).</span></span>

<a id="0.1__Toc245724854"></a><a id="0.1__Toc255587631"></a><a id="0.1__Toc256770142"></a>

## <a name="clientidmode-changes"></a><span data-ttu-id="a4c77-141">ClientIDMode 更改</span><span class="sxs-lookup"><span data-stu-id="a4c77-141">ClientIDMode Changes</span></span>

<span data-ttu-id="a4c77-142">通过 ASP.NET 4 中的**ClientIDMode**设置，你可以指定 ASP.NET 生成 HTML 元素的**id**属性的方式。</span><span class="sxs-lookup"><span data-stu-id="a4c77-142">The **ClientIDMode** setting in ASP.NET 4 lets you specify how ASP.NET generates the **id** attribute for HTML elements.</span></span> <span data-ttu-id="a4c77-143">在以前版本的 ASP.NET 中，默认行为等效于**ClientIDMode**的**AutoID**设置。</span><span class="sxs-lookup"><span data-stu-id="a4c77-143">In previous versions of ASP.NET, the default behavior was equivalent to the **AutoID** setting of **ClientIDMode**.</span></span> <span data-ttu-id="a4c77-144">但是，默认设置现在是**可预测**的。</span><span class="sxs-lookup"><span data-stu-id="a4c77-144">However, the default setting is now **Predictable**.</span></span>

<span data-ttu-id="a4c77-145">如果你使用 Visual Studio 2010 从 ASP.NET 2.0 或 ASP.NET 3.5 升级应用程序，则该工具会自动将设置添加到 `Web.config` 文件中，该文件保留 .NET Framework 早期版本的行为。</span><span class="sxs-lookup"><span data-stu-id="a4c77-145">If you use Visual Studio 2010 to upgrade your application from ASP.NET 2.0 or ASP.NET 3.5, the tool automatically adds a setting to the `Web.config` file that preserves the behavior of earlier versions of the .NET Framework.</span></span> <span data-ttu-id="a4c77-146">但是，如果通过在 IIS 中将应用程序池更改为面向 .NET Framework 4 来升级应用程序，ASP.NET 默认使用新的模式。</span><span class="sxs-lookup"><span data-stu-id="a4c77-146">However, if you upgrade an application by changing the application pool in IIS to target the .NET Framework 4, ASP.NET uses the new mode by default.</span></span> <span data-ttu-id="a4c77-147">若要禁用新的客户端 ID 模式，请在 `Web.config` 文件中添加以下设置：</span><span class="sxs-lookup"><span data-stu-id="a4c77-147">To disable the new client ID mode, add the following setting in the `Web.config` file:</span></span>

[!code-xml[Main](breaking-changes/samples/sample2.xml)]

<a id="0.1__Toc245724855"></a><a id="0.1__Toc255587632"></a><a id="0.1__Toc256770143"></a>

## <a name="htmlencode-and-urlencode-now-encode-single-quotation-marks"></a><span data-ttu-id="a4c77-148">Server.htmlencode 和 UrlEncode 现在对单引号进行编码</span><span class="sxs-lookup"><span data-stu-id="a4c77-148">HtmlEncode and UrlEncode Now Encode Single Quotation Marks</span></span>

<span data-ttu-id="a4c77-149">在 ASP.NET 4 中， **httputility.javascriptstringencode**和**HttpServerUtility**类的**server.htmlencode**和**UrlEncode**方法已更新，以对单引号字符（'）进行编码，如下所示：</span><span class="sxs-lookup"><span data-stu-id="a4c77-149">In ASP.NET 4, the **HtmlEncode** and **UrlEncode** methods of the **HttpUtility** and **HttpServerUtility** classes have been updated to encode the single quotation mark character (') as follows:</span></span>

- <span data-ttu-id="a4c77-150">**Server.htmlencode**方法将单引号的实例编码为 "。</span><span class="sxs-lookup"><span data-stu-id="a4c77-150">The **HtmlEncode** method encodes instances of the single quotation mark as ' .</span></span>
- <span data-ttu-id="a4c77-151">**UrlEncode**方法将单引号的实例编码为 %27。</span><span class="sxs-lookup"><span data-stu-id="a4c77-151">The **UrlEncode** method encodes instances of the single quotation mark as %27.</span></span>

<a id="0.1__Toc255587633"></a><a id="0.1__Toc256770144"></a><a id="0.1__Toc245724856"></a>

## <a name="aspnet-page-aspx-parser-is-stricter"></a><span data-ttu-id="a4c77-152">ASP.NET 页（.aspx）分析器更严格</span><span class="sxs-lookup"><span data-stu-id="a4c77-152">ASP.NET Page (.aspx) Parser is Stricter</span></span>

<span data-ttu-id="a4c77-153">ASP.NET 页（`.aspx` 文件）和用户控件（`.ascx` 文件）的页分析器在 ASP.NET 4 中更严格，并将拒绝无效标记的更多实例。</span><span class="sxs-lookup"><span data-stu-id="a4c77-153">The page parser for ASP.NET pages (`.aspx` files) and user controls (`.ascx` files) is stricter in ASP.NET 4 and will reject more instances of invalid markup.</span></span> <span data-ttu-id="a4c77-154">例如，以下两个代码段将在早期版本的 ASP.NET 中成功进行分析，但现在会在 ASP.NET 4 中引发分析器错误。</span><span class="sxs-lookup"><span data-stu-id="a4c77-154">For example, the following two snippets would successfully parse in earlier releases of ASP.NET, but will now raise parser errors in ASP.NET 4.</span></span>

[!code-aspx[Main](breaking-changes/samples/sample3.aspx)]

<span data-ttu-id="a4c77-155">请注意**HiddenField**标记结尾的无效分号。</span><span class="sxs-lookup"><span data-stu-id="a4c77-155">Notice the invalid semicolon at the end of the **HiddenField** tag.</span></span>

[!code-aspx[Main](breaking-changes/samples/sample4.aspx)]

<span data-ttu-id="a4c77-156">请注意，在**CssClass**属性中运行的未闭合**样式**特性。</span><span class="sxs-lookup"><span data-stu-id="a4c77-156">Notice the unclosed **style** attribute that runs into the **CssClass** attribute.</span></span>

<a id="0.1__Toc255587634"></a><a id="0.1__Toc256770145"></a>

## <a name="browser-definition-files-updated"></a><span data-ttu-id="a4c77-157">已更新浏览器定义文件</span><span class="sxs-lookup"><span data-stu-id="a4c77-157">Browser Definition Files Updated</span></span>

<span data-ttu-id="a4c77-158">浏览器定义文件已更新，以包括有关新的和已更新的浏览器和设备的信息。</span><span class="sxs-lookup"><span data-stu-id="a4c77-158">The browser definition files have been updated to include information about new and updated browsers and devices.</span></span> <span data-ttu-id="a4c77-159">旧式浏览器和设备（如 Netscape Navigator）已被删除，并且已添加更新的浏览器和设备（如 Google Chrome 和 Apple iPhone）。</span><span class="sxs-lookup"><span data-stu-id="a4c77-159">Older browsers and devices such as Netscape Navigator have been removed, and newer browsers and devices such as Google Chrome and Apple iPhone have been added.</span></span>

<span data-ttu-id="a4c77-160">如果应用程序包含的自定义浏览器定义继承自一个已删除的浏览器定义，将会出现错误。</span><span class="sxs-lookup"><span data-stu-id="a4c77-160">If your application contains custom browser definitions that inherit from one of the browser definitions that have been removed, you will see an error.</span></span> <span data-ttu-id="a4c77-161">例如，如果 `App_Browsers` 文件夹中包含继承自 IE2 浏览器定义的浏览器定义，则你将收到以下配置错误消息：</span><span class="sxs-lookup"><span data-stu-id="a4c77-161">For example, if the `App_Browsers` folder contains a browser definition that inherits from the IE2 browser definition, you will receive the following configuration error message:</span></span>

- <span data-ttu-id="a4c77-162">找不到 ID 为 "IE2" 的浏览器或网关元素。</span><span class="sxs-lookup"><span data-stu-id="a4c77-162">The browser or gateway element with ID 'IE2' cannot be found.</span></span>

> [!NOTE]
> <span data-ttu-id="a4c77-163">**HttpBrowserCapabilities**对象（由页面的**Request**属性公开）由浏览器定义文件驱动。</span><span class="sxs-lookup"><span data-stu-id="a4c77-163">The **HttpBrowserCapabilities** object (which is exposed by the page's **Request.Browser** property) is driven by the browser definitions files.</span></span> <span data-ttu-id="a4c77-164">因此，通过在 ASP.NET 4 中访问此对象的属性返回的信息可能与早期版本的 ASP.NET 中返回的信息不同。</span><span class="sxs-lookup"><span data-stu-id="a4c77-164">Therefore, the information returned by accessing a property of this object in ASP.NET 4 might be different than the information returned in an earlier version of ASP.NET.</span></span>

<span data-ttu-id="a4c77-165">可以通过从以下文件夹复制浏览器定义文件来恢复到旧的浏览器定义文件：</span><span class="sxs-lookup"><span data-stu-id="a4c77-165">You can revert to the old browser definition files by copying the browser definition files from the following folder:</span></span>

[!code-console[Main](breaking-changes/samples/sample5.cmd)]

<span data-ttu-id="a4c77-166">将文件复制到 ASP.NET 4 的相应 `\CONFIG\Browsers` 文件夹中。</span><span class="sxs-lookup"><span data-stu-id="a4c77-166">Copy the files into the corresponding `\CONFIG\Browsers` folder for ASP.NET 4.</span></span> <span data-ttu-id="a4c77-167">复制文件后，请运行 Aspnet\_regbrowsers 命令行工具。</span><span class="sxs-lookup"><span data-stu-id="a4c77-167">After you copy the files, run the Aspnet\_regbrowsers.exe command-line tool.</span></span>

<a id="0.1__Toc255587635"></a><a id="0.1__Toc256770146"></a>

## <a name="systemwebmobiledll-removed-from-root-web-configuration-file"></a><span data-ttu-id="a4c77-168">从根 Web 配置文件中删除了 system.web. .dll</span><span class="sxs-lookup"><span data-stu-id="a4c77-168">System.Web.Mobile.dll Removed from Root Web Configuration File</span></span>

<span data-ttu-id="a4c77-169">在以前版本的 ASP.NET 中，对 System.web 程序集的引用包含在下的**程序集**部分的根 `Web.config` 文件中。</span><span class="sxs-lookup"><span data-stu-id="a4c77-169">In previous versions of ASP.NET, a reference to the System.Web.Mobile.dll assembly was included in the root `Web.config` file in the **assemblies** section under.</span></span> <span data-ttu-id="a4c77-170">为了提高性能，已删除对此程序集的引用。</span><span class="sxs-lookup"><span data-stu-id="a4c77-170">In order to improve performance, the reference to this assembly was removed.</span></span>

<span data-ttu-id="a4c77-171">ASP.NET 4 中包括了 System.web .dll 程序集，但该程序集已弃用。</span><span class="sxs-lookup"><span data-stu-id="a4c77-171">The System.Web.Mobile.dll assembly is included in ASP.NET 4, but it is deprecated.</span></span> <span data-ttu-id="a4c77-172">如果要使用 System.web 程序集的类型，请将对此程序集的引用添加到根 `Web.config` 文件或应用程序 `Web.config` 文件中。</span><span class="sxs-lookup"><span data-stu-id="a4c77-172">If you want to use types from the System.Web.Mobile.dll assembly, add a reference to this assembly to either the root `Web.config` file or to an application `Web.config` file.</span></span> <span data-ttu-id="a4c77-173">例如，如果要使用任何（弃用的） ASP.NET 移动控件，则必须将对 System.web 程序集的引用添加到 `Web.config` 文件中。</span><span class="sxs-lookup"><span data-stu-id="a4c77-173">For example, if you want to use any of the (deprecated) ASP.NET mobile controls, you must add a reference to the System.Web.Mobile.dll assembly to the `Web.config` file.</span></span>

<a id="0.1__Toc245724857"></a><a id="0.1__Toc255587636"></a><a id="0.1__Toc256770147"></a>

## <a name="aspnet-request-validation"></a><span data-ttu-id="a4c77-174">ASP.NET 请求验证</span><span class="sxs-lookup"><span data-stu-id="a4c77-174">ASP.NET Request Validation</span></span>

<span data-ttu-id="a4c77-175">ASP.NET 中的请求验证功能针对跨站点脚本（XSS）攻击提供一定程度的默认保护。</span><span class="sxs-lookup"><span data-stu-id="a4c77-175">The request validation feature in ASP.NET provides a certain level of default protection against cross-site scripting (XSS) attacks.</span></span> <span data-ttu-id="a4c77-176">在以前版本的 ASP.NET 中，默认情况下已启用请求验证。</span><span class="sxs-lookup"><span data-stu-id="a4c77-176">In previous versions of ASP.NET, request validation was enabled by default.</span></span> <span data-ttu-id="a4c77-177">但是，它仅应用于 ASP.NET 页（`.aspx` 文件和它们的类文件），并且仅适用于这些页的执行时间。</span><span class="sxs-lookup"><span data-stu-id="a4c77-177">However, it applied only to ASP.NET pages (`.aspx` files and their class files) and only when those pages were executing.</span></span>

<span data-ttu-id="a4c77-178">默认情况下，在 ASP.NET 4 中，为所有请求启用了请求验证，因为在 HTTP 请求的**BeginRequest**阶段之前启用了请求验证。</span><span class="sxs-lookup"><span data-stu-id="a4c77-178">In ASP.NET 4, by default, request validation is enabled for all requests, because it is enabled before the **BeginRequest** phase of an HTTP request.</span></span> <span data-ttu-id="a4c77-179">因此，请求验证适用于对所有 ASP.NET 资源的请求，而不只是 .aspx 页面请求。</span><span class="sxs-lookup"><span data-stu-id="a4c77-179">As a result, request validation applies to requests for all ASP.NET resources, not just .aspx page requests.</span></span> <span data-ttu-id="a4c77-180">这包括诸如 Web 服务调用和自定义 HTTP 处理程序之类的请求。</span><span class="sxs-lookup"><span data-stu-id="a4c77-180">This includes requests such as Web service calls and custom HTTP handlers.</span></span> <span data-ttu-id="a4c77-181">当自定义 HTTP 模块读取 HTTP 请求的内容时，请求验证也处于活动状态。</span><span class="sxs-lookup"><span data-stu-id="a4c77-181">Request validation is also active when custom HTTP modules are reading the contents of an HTTP request.</span></span>

<span data-ttu-id="a4c77-182">因此，对于之前未触发错误的请求，此时可能会发生请求验证错误。</span><span class="sxs-lookup"><span data-stu-id="a4c77-182">As a result, request validation errors might now occur for requests that previously did not trigger errors.</span></span> <span data-ttu-id="a4c77-183">若要恢复到 ASP.NET 2.0 请求验证功能的行为，请在 `Web.config` 文件中添加以下设置：</span><span class="sxs-lookup"><span data-stu-id="a4c77-183">To revert to the behavior of the ASP.NET 2.0 request validation feature, add the following setting in the `Web.config` file:</span></span>

[!code-xml[Main](breaking-changes/samples/sample6.xml)]

<span data-ttu-id="a4c77-184">但是，我们建议你分析任何请求验证错误，以确定现有处理程序、模块或其他自定义代码是否访问可能是 XSS 攻击向量的可能不安全的 HTTP 输入。</span><span class="sxs-lookup"><span data-stu-id="a4c77-184">However, we recommend that you analyze any request validation errors to determine whether existing handlers, modules, or other custom code accesses potentially unsafe HTTP inputs that could be XSS attack vectors.</span></span>

<a id="0.1__Toc245724858"></a><a id="0.1__Toc255587637"></a><a id="0.1__Toc256770148"></a>

## <a name="default-hashing-algorithm-is-now-hmacsha256"></a><span data-ttu-id="a4c77-185">默认哈希算法现在为 HMACSHA256</span><span class="sxs-lookup"><span data-stu-id="a4c77-185">Default Hashing Algorithm Is Now HMACSHA256</span></span>

<span data-ttu-id="a4c77-186">ASP.NET 使用加密算法和哈希算法来帮助保护数据（如窗体身份验证 Cookie 和视图状态）。</span><span class="sxs-lookup"><span data-stu-id="a4c77-186">ASP.NET uses both encryption and hashing algorithms to help secure data such as forms authentication cookies and view state.</span></span> <span data-ttu-id="a4c77-187">默认情况下，ASP.NET 4 现在使用 HMACSHA256 算法对 cookie 和视图状态进行哈希操作。</span><span class="sxs-lookup"><span data-stu-id="a4c77-187">By default, ASP.NET 4 now uses the HMACSHA256 algorithm for hash operations on cookies and view state.</span></span> <span data-ttu-id="a4c77-188">早期版本的 ASP.NET 使用了较旧的 HMACSHA1 算法。</span><span class="sxs-lookup"><span data-stu-id="a4c77-188">Earlier versions of ASP.NET used the older HMACSHA1 algorithm.</span></span>

<span data-ttu-id="a4c77-189">如果运行混合 ASP.NET 2.0/ASP，应用程序可能会受到影响。 NET 4 环境，其中的数据（如 forms 身份验证 cookie）必须在 across.NET Framework 版本中工作。</span><span class="sxs-lookup"><span data-stu-id="a4c77-189">Your applications might be affected if you run mixed ASP.NET 2.0/ASP.NET 4 environments where data such as forms authentication cookies must work across.NET Framework versions.</span></span> <span data-ttu-id="a4c77-190">若要将 ASP.NET 4 Web 应用程序配置为使用较旧的 HMACSHA1 算法，请在 `Web.config` 文件中添加以下设置：</span><span class="sxs-lookup"><span data-stu-id="a4c77-190">To configure an ASP.NET 4 Web application to use the older HMACSHA1 algorithm, add the following setting in the `Web.config` file:</span></span>

[!code-xml[Main](breaking-changes/samples/sample7.xml)]

<a id="0.1__Toc245724859"></a><a id="0.1__Toc255587638"></a><a id="0.1__Toc256770149"></a>

## <a name="configuration-errors-related-to-new-aspnet-4-root-configuration"></a><span data-ttu-id="a4c77-191">与新的 ASP.NET 4 根配置相关的配置错误</span><span class="sxs-lookup"><span data-stu-id="a4c77-191">Configuration Errors Related to New ASP.NET 4 Root Configuration</span></span>

<span data-ttu-id="a4c77-192">已更新 .NET Framework 4 （因此 ASP.NET 4）的根配置文件（`machine.config` 文件和根 `Web.config` 文件），以包含3.5 在应用程序 `Web.config` 文件中找到的大多数样本配置信息。</span><span class="sxs-lookup"><span data-stu-id="a4c77-192">The root configuration files (the `machine.config` file and the root `Web.config` file) for the .NET Framework 4 (and therefore ASP.NET 4) have been updated to include most of the boilerplate configuration information that in ASP.NET 3.5 was found in the application `Web.config` files.</span></span> <span data-ttu-id="a4c77-193">由于托管 IIS 7 和 IIS 7.5 配置系统的复杂性，在 ASP.NET 4 和 iis 7 和 IIS 7.5 下运行 ASP.NET 3.5 应用程序可能会导致 ASP.NET 或 IIS 配置错误。</span><span class="sxs-lookup"><span data-stu-id="a4c77-193">Because of the complexity of the managed IIS 7 and IIS 7.5 configuration systems, running ASP.NET 3.5 applications under ASP.NET 4 and under IIS 7 and IIS 7.5 can result in either ASP.NET or IIS configuration errors.</span></span>

<span data-ttu-id="a4c77-194">如果可行，建议使用 Visual Studio 2010 中的项目升级工具将 ASP.NET 3.5 应用程序升级到 ASP.NET 4。</span><span class="sxs-lookup"><span data-stu-id="a4c77-194">We recommend that you upgrade ASP.NET 3.5 applications to ASP.NET 4 by using the project upgrade tools in Visual Studio 2010, if practical.</span></span> <span data-ttu-id="a4c77-195">Visual Studio 2010 自动修改 ASP.NET 3.5 应用程序的 `Web.config` 文件，使其包含 ASP.NET 4 的相应设置。</span><span class="sxs-lookup"><span data-stu-id="a4c77-195">Visual Studio 2010 automatically modifies the ASP.NET 3.5 application's `Web.config` file to contain the appropriate settings for ASP.NET 4.</span></span>

<span data-ttu-id="a4c77-196">但是，在不重新编译的情况下，使用 .NET Framework 4 运行 ASP.NET 3.5 应用程序是受支持的方案。</span><span class="sxs-lookup"><span data-stu-id="a4c77-196">However, it is a supported scenario to run ASP.NET 3.5 applications using the .NET Framework 4 without recompilation.</span></span> <span data-ttu-id="a4c77-197">在这种情况下，你可能必须先手动修改应用程序的 `Web.config` 文件，然后才能在 .NET Framework 4 和 IIS 7 或 IIS 7.5 下运行该应用程序。</span><span class="sxs-lookup"><span data-stu-id="a4c77-197">In that case, you might have to manually modify the application's `Web.config` file before you run the application under the .NET Framework 4 and under IIS 7 or IIS 7.5.</span></span>

<span data-ttu-id="a4c77-198">接下来的两部分介绍了你可能需要对不同软件组合做出的更改。</span><span class="sxs-lookup"><span data-stu-id="a4c77-198">The next two sections describe changes that you might need to make for different combinations of software.</span></span>

<span data-ttu-id="a4c77-199">**Windows Vista SP1 或 Windows Server 2008 SP1，其中不安装修补程序 KB958854 和 SP2。**</span><span class="sxs-lookup"><span data-stu-id="a4c77-199">**Windows Vista SP1 or Windows Server 2008 SP1, where neither hotfix KB958854 nor SP2 are installed.**</span></span> <span data-ttu-id="a4c77-200">在此配置中，IIS 7 配置系统会将应用程序级 `Web.config` 文件与 ASP.NET 2.0 `machine.config` 文件进行比较，从而错误地合并应用程序的托管配置。</span><span class="sxs-lookup"><span data-stu-id="a4c77-200">In this configuration, the IIS 7 configuration system incorrectly merges an application's managed configuration by comparing the application-level `Web.config` file to the ASP.NET 2.0 `machine.config` files.</span></span> <span data-ttu-id="a4c77-201">因此，.NET Framework 3.5 或更高版本中的应用程序级 `Web.config` 文件必须具有一个**system.web. extension**配置节定义（元素），以便不会导致 IIS 7 验证失败。</span><span class="sxs-lookup"><span data-stu-id="a4c77-201">Because of this, application-level `Web.config` files from the .NET Framework 3.5 or later must have a **system.web.extensions** configuration section definition (the element) in order not to cause an IIS 7 validation failure.</span></span>

<span data-ttu-id="a4c77-202">但是，手动修改的应用程序级 `Web.config` 文件项与 Visual Studio 2008 中引入的原始样本配置节定义不完全匹配，将导致 ASP.NET 配置错误。</span><span class="sxs-lookup"><span data-stu-id="a4c77-202">However, manually modified application-level `Web.config` file entries that do not precisely match the original boilerplate configuration section definitions that were introduced with Visual Studio 2008 will cause ASP.NET configuration errors.</span></span> <span data-ttu-id="a4c77-203">（Visual Studio 2008 生成的默认配置项工作正常。）一个常见的问题是，手动修改 `Web.config` 文件会遗漏在各种配置节定义中找到的**allowDefinition**和**requirePermission**配置属性。</span><span class="sxs-lookup"><span data-stu-id="a4c77-203">(The default configuration entries that are generated by Visual Studio 2008 work correctly.) A common problem is that manually modified `Web.config` files leave out the **allowDefinition** and **requirePermission** configuration attributes that are found on various configuration section definitions.</span></span> <span data-ttu-id="a4c77-204">这会导致应用程序级别 `Web.config` 文件中的缩写配置节和 ASP.NET 4 `machine.config` 文件中的完整定义不匹配。</span><span class="sxs-lookup"><span data-stu-id="a4c77-204">This causes a mismatch between the abbreviated configuration section in application-level `Web.config` files and the complete definition in the ASP.NET 4 `machine.config` file.</span></span> <span data-ttu-id="a4c77-205">因此，在运行时，ASP.NET 4 配置系统将引发配置错误。</span><span class="sxs-lookup"><span data-stu-id="a4c77-205">As a result, at run time, the ASP.NET 4 configuration system throws a configuration error.</span></span>

<span data-ttu-id="a4c77-206">**Windows Vista SP2、Windows Server 2008 SP2、Windows 7、Windows Server 2008 R2，以及安装了修补程序 KB958854 的 Windows Vista SP1 和 Windows Server 2008 SP1。**</span><span class="sxs-lookup"><span data-stu-id="a4c77-206">**Windows Vista SP2, Windows Server 2008 SP2, Windows 7, Windows Server 2008 R2, and also Windows Vista SP1 and Windows Server 2008 SP1 where hotfix KB958854 is installed.**</span></span>

<span data-ttu-id="a4c77-207">在这种情况下，IIS 7 和 IIS 7.5 本机配置系统返回配置错误，因为它对为托管配置节处理程序定义的**类型**属性执行文本比较。</span><span class="sxs-lookup"><span data-stu-id="a4c77-207">In this scenario, the IIS 7 and IIS 7.5 native configuration system returns a configuration error because it performs a text comparison on the **type** attribute that is defined for a managed configuration section handler.</span></span> <span data-ttu-id="a4c77-208">由于 Visual Studio 2008 和 Visual Studio 2008 SP1 生成的所有 `Web.config` 文件在系统的类型字符串中都有 "3.5"。由于在同一配置节处理程序的类型属性中，ASP.NET 4 `machine.config` 文件中有 "4.0"，在 Visual Studio 2008 或 Visual Studio 2008 SP1 中生成的应用程序在 IIS 7 和 IIS 7.5 中始终无法进行配置验证，因此， **web extensions** （及相关）配置节处理程序以及这**种**配置节处理程序和。</span><span class="sxs-lookup"><span data-stu-id="a4c77-208">Because all `Web.config` files that are generated by Visual Studio 2008 and Visual Studio 2008 SP1 have "3.5" in the type string for the **system.web.extensions** (and related) configuration section handlers, and because the ASP.NET 4 `machine.config` file has "4.0" in the **type** attribute for the same configuration section handlers, applications that are generated in Visual Studio 2008 or Visual Studio 2008 SP1 always fail configuration validation in IIS 7 and IIS 7.5.</span></span>

<a id="0.1__Toc251910248"></a>

### <a name="resolving-these-issues"></a><span data-ttu-id="a4c77-209">解决这些问题</span><span class="sxs-lookup"><span data-stu-id="a4c77-209">Resolving These Issues</span></span>

<span data-ttu-id="a4c77-210">第一种情况的解决方法是通过将样本配置文本包含在 Visual Studio 2008 自动生成的 `Web.config` 文件中，来更新应用程序级别的 `Web.config` 文件。</span><span class="sxs-lookup"><span data-stu-id="a4c77-210">The workaround for the first scenario is to update the application-level `Web.config` file by including the boilerplate configuration text from a `Web.config` file that was generated automatically by Visual Studio 2008.</span></span>

<span data-ttu-id="a4c77-211">第一种方案的另一种解决方法是在您的计算机上安装适用于 Vista 或 Windows Server 2008 的 Service Pack 2，或者安装修补程序 KB958854 （[https://support.microsoft.com/kb/958854](https://support.microsoft.com/kb/958854)）来修复 IIS 配置系统的错误配置-合并行为。</span><span class="sxs-lookup"><span data-stu-id="a4c77-211">An alternative workaround for the first scenario is to install Service Pack 2 for Vista or Windows Server 2008 on your computer or to install hotfix KB958854 ([https://support.microsoft.com/kb/958854](https://support.microsoft.com/kb/958854)) to fix the incorrect configuration-merge behavior of the IIS configuration system.</span></span> <span data-ttu-id="a4c77-212">但是，在执行上述任一操作后，你的应用程序可能会遇到配置错误，因为第二个方案中描述的问题。</span><span class="sxs-lookup"><span data-stu-id="a4c77-212">However, after you perform either of these actions, your application will likely encounter a configuration error due to the issue described for the second scenario.</span></span>

<span data-ttu-id="a4c77-213">第二种方案的解决方法是从应用程序级 `Web.config` 文件中删除或注释掉所有**system.web. extensions**配置节定义和配置节组定义。</span><span class="sxs-lookup"><span data-stu-id="a4c77-213">The workaround for the second scenario is to delete or comment out all the **system.web.extensions** configuration section definitions and configuration section group definitions from the application-level `Web.config` file.</span></span> <span data-ttu-id="a4c77-214">这些定义通常位于应用程序级别 `Web.config` 文件的顶部，可由**configSections**元素及其子元素标识。</span><span class="sxs-lookup"><span data-stu-id="a4c77-214">These definitions are usually at the top of the application-level `Web.config` file and can be identified by the **configSections** element and its children.</span></span>

<span data-ttu-id="a4c77-215">对于这两种方案，建议你也手动删除**system.object**部分，尽管这不是必需的。</span><span class="sxs-lookup"><span data-stu-id="a4c77-215">For both scenarios, it is recommended that you also manually delete the **system.codedom** section, although this is not required.</span></span>

<a id="0.1__Toc252995490"></a><a id="0.1__Toc255587639"></a><a id="0.1__Toc256770150"></a><a id="0.1__Toc245724860"></a>

## <a name="aspnet-4-child-applications-fail-to-start-when-under-aspnet-20-or-aspnet-35-applications"></a><span data-ttu-id="a4c77-216">ASP.NET 4 子应用程序在 ASP.NET 2.0 或 ASP.NET 3.5 应用程序下无法启动</span><span class="sxs-lookup"><span data-stu-id="a4c77-216">ASP.NET 4 Child Applications Fail to Start When Under ASP.NET 2.0 or ASP.NET 3.5 Applications</span></span>

<span data-ttu-id="a4c77-217">由于配置或编译错误，配置为运行 ASP.NET 早期版本的应用程序子级的 ASP.NET 4 应用程序可能无法启动。</span><span class="sxs-lookup"><span data-stu-id="a4c77-217">ASP.NET 4 applications that are configured as children of applications that run earlier versions of ASP.NET might fail to start because of configuration or compilation errors.</span></span> <span data-ttu-id="a4c77-218">下面的示例显示受影响的应用程序的目录结构。</span><span class="sxs-lookup"><span data-stu-id="a4c77-218">The following example shows a directory structure for an affected application.</span></span>

<span data-ttu-id="a4c77-219">`/parentwebapp` （配置为使用 ASP.NET 2.0 或 ASP.NET 3.5）</span><span class="sxs-lookup"><span data-stu-id="a4c77-219">`/parentwebapp` (configured to use ASP.NET 2.0 or ASP.NET 3.5)</span></span>  
<span data-ttu-id="a4c77-220">`/childwebapp` （配置为使用 ASP.NET 4）</span><span class="sxs-lookup"><span data-stu-id="a4c77-220">`/childwebapp` (configured to use ASP.NET 4)</span></span>

<span data-ttu-id="a4c77-221">`childwebapp` 文件夹中的应用程序将无法在 IIS 7 或 IIS 7.5 上启动，并将报告配置错误。</span><span class="sxs-lookup"><span data-stu-id="a4c77-221">The application in the `childwebapp` folder will fail to start on IIS 7 or IIS 7.5 and will report a configuration error.</span></span> <span data-ttu-id="a4c77-222">错误文本将包含类似于下面的消息：</span><span class="sxs-lookup"><span data-stu-id="a4c77-222">The error text will include a message similar to the following:</span></span>

- `The requested page cannot be accessed because the related configuration data for the page is invalid.`

- `The configuration section 'configSections' cannot be read because it is missing a section declaration.`

<span data-ttu-id="a4c77-223">在 IIS 6 上，`childwebapp` 文件夹中的应用程序也将无法启动，但会报告其他错误。</span><span class="sxs-lookup"><span data-stu-id="a4c77-223">On IIS 6, the application in the `childwebapp` folder will also fail to start, but it will report a different error.</span></span> <span data-ttu-id="a4c77-224">例如，错误文本可能会声明以下内容：</span><span class="sxs-lookup"><span data-stu-id="a4c77-224">For example, the error text might state the following:</span></span>

- `The value for the 'compilerVersion' attribute in the provider options must be 'v4.0' or later if you are compiling for version 4.0 or later of the .NET Framework. To compile this Web application for version 3.5 or earlier of the .NET Framework, remove the 'targetFramework' attribute from the element of the Web.config file`

<span data-ttu-id="a4c77-225">之所以出现这种情况，是因为 `parentwebapp` 文件夹中的父应用程序的配置信息是配置信息层次结构的一部分，这些配置信息确定子 web 应用程序在 `childwebapp` 文件夹中所使用的最终合并配置设置。</span><span class="sxs-lookup"><span data-stu-id="a4c77-225">These scenarios occur because the configuration information from the parent application in the `parentwebapp` folder is part of the hierarchy of configuration information that determines the final merged configuration settings that are used by the child web application in the `childwebapp` folder.</span></span> <span data-ttu-id="a4c77-226">根据 ASP.NET 4 Web 应用程序是在 IIS 7.5 7 上运行还是在 iis 6 上运行，IIS 配置系统或 ASP.NET 4 编译系统都将返回错误。</span><span class="sxs-lookup"><span data-stu-id="a4c77-226">Depending on whether the ASP.NET 4 Web application is running on IIS 7 (or IIS 7.5) or on IIS 6, either the IIS configuration system or the ASP.NET 4 compilation system will return an error.</span></span>

<span data-ttu-id="a4c77-227">解决此问题并使子 ASP.NET 4 应用程序工作所必须遵循的步骤取决于 ASP.NET 4 应用程序是在 IIS 6 上运行还是在 IIS 7 上运行（或 IIS 7.5）。</span><span class="sxs-lookup"><span data-stu-id="a4c77-227">The steps that you must follow to resolve this issue and to get the child ASP.NET 4 application to work depend on whether the ASP.NET 4 application runs on IIS 6 or on IIS 7 (or IIS 7.5).</span></span>

### <a name="step-1-iis-7-or-iis-75-only"></a><span data-ttu-id="a4c77-228">步骤1（仅限 IIS 7 或 IIS 7.5）</span><span class="sxs-lookup"><span data-stu-id="a4c77-228">Step 1 (IIS 7 or IIS 7.5 only)</span></span>

<span data-ttu-id="a4c77-229">此步骤仅在运行 IIS 7 或 IIS 7.5 的操作系统（包括 Windows Vista、Windows Server 2008、Windows 7 和 Windows Server 2008 R2）上是必需的。</span><span class="sxs-lookup"><span data-stu-id="a4c77-229">This step is necessary only on operating systems that run IIS 7 or IIS 7.5, which includes Windows Vista, Windows Server 2008, Windows 7, and Windows Server 2008 R2.</span></span>

<span data-ttu-id="a4c77-230">将父应用程序（运行 ASP.NET 2.0 或 ASP.NET 3.5）的 `Web.config` 文件中的**configSections**定义移动到 the.NET Framework 2.0 的根 `Web.config` 文件中。</span><span class="sxs-lookup"><span data-stu-id="a4c77-230">Move the **configSections** definition in the `Web.config` file of the parent application (the application that runs ASP.NET 2.0 or ASP.NET 3.5) into the root `Web.config` file for the.NET Framework 2.0.</span></span> <span data-ttu-id="a4c77-231">当**configSections**元素合并配置文件的层次结构时，iis 7 和 iis 7.5 本机配置系统会对其进行扫描。</span><span class="sxs-lookup"><span data-stu-id="a4c77-231">The IIS 7 and IIS 7.5 native configuration system scans the **configSections** element when it merges the hierarchy of configuration files.</span></span> <span data-ttu-id="a4c77-232">将**configSections**定义从父 Web 应用程序的 `Web.config` 文件移到根 `Web.config` 文件，可以有效地隐藏为子 ASP.NET 4 应用程序发生的配置合并过程中的元素。</span><span class="sxs-lookup"><span data-stu-id="a4c77-232">Moving the **configSections** definition from the parent Web application's `Web.config` file to the root `Web.config` file effectively hides the element from the configuration merge process that occurs for the child ASP.NET 4 application.</span></span>

<span data-ttu-id="a4c77-233">在32位操作系统或32位应用程序池上，ASP.NET 2.0 和 ASP.NET 3.5 的根 `Web.config` 文件通常位于以下文件夹中：</span><span class="sxs-lookup"><span data-stu-id="a4c77-233">On a 32-bit operating system or for 32-bit application pools, the root `Web.config` file for ASP.NET 2.0 and ASP.NET 3.5 is normally located in the following folder:</span></span>

`C:\Windows\Microsoft.NET\Framework\v2.0.50727\CONFIG`

<span data-ttu-id="a4c77-234">在64位操作系统或64位应用程序池上，ASP.NET 2.0 和 ASP.NET 3.5 的根 `Web.config` 文件通常位于以下文件夹中：</span><span class="sxs-lookup"><span data-stu-id="a4c77-234">On a 64-bit operating system or for 64-bit application pools, the root `Web.config` file for ASP.NET 2.0 and ASP.NET 3.5 is normally located in the following folder:</span></span>

`C:\Windows\Microsoft.NET\Framework64\v2.0.50727\CONFIG`

<span data-ttu-id="a4c77-235">如果在64位计算机上同时运行32位和64位 Web 应用程序，则必须将**configSections**元素向上移动到32和64位系统的根 `Web.config` 文件中。</span><span class="sxs-lookup"><span data-stu-id="a4c77-235">If you run both 32-bit and 64-bit Web applications on a 64-bit computer, you must move the **configSections** element up into root `Web.config` files for both the 32-bit and the 64-bit systems.</span></span>

<span data-ttu-id="a4c77-236">将**configSections**元素放在根 `Web.config` 文件中后，立即将该节粘贴到**configuration**元素之后。</span><span class="sxs-lookup"><span data-stu-id="a4c77-236">When you put the **configSections** element in the root `Web.config` file, paste the section immediately after the **configuration** element.</span></span> <span data-ttu-id="a4c77-237">下面的示例显示了在完成移动元素后，根 `Web.config` 文件的顶层内容应如下所示。</span><span class="sxs-lookup"><span data-stu-id="a4c77-237">The following example shows what the top portion of the root `Web.config` file should look like when you have finished moving the elements.</span></span>

> [!NOTE]
> <span data-ttu-id="a4c77-238">在下面的示例中，已换行以方便阅读。</span><span class="sxs-lookup"><span data-stu-id="a4c77-238">In the following example, lines have been wrapped for readability.</span></span>

[!code-xml[Main](breaking-changes/samples/sample8.xml)]

### <a name="step-2-all-versions-of-iis"></a><span data-ttu-id="a4c77-239">步骤2（所有版本的 IIS）</span><span class="sxs-lookup"><span data-stu-id="a4c77-239">Step 2 (all versions of IIS)</span></span>

<span data-ttu-id="a4c77-240">无论 ASP.NET 4 子 Web 应用程序是在 IIS 6 上运行还是在 IIS 7 上运行（或 IIS 7.5），都需要执行此步骤。</span><span class="sxs-lookup"><span data-stu-id="a4c77-240">This step is required whether the ASP.NET 4 child Web application is running on IIS 6 or on IIS 7 (or IIS 7.5).</span></span>

<span data-ttu-id="a4c77-241">在运行 ASP.NET 2 或 ASP.NET 3.5 的父 Web 应用程序的 `Web.config` 文件中，添加一个**位置**标记，该标记显式指定（适用于 IIS 和 ASP.NET 配置系统），而这些配置项仅适用于父 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="a4c77-241">In the `Web.config` file of the parent Web application that is running ASP.NET 2 or ASP.NET 3.5, add a **location** tag that explicitly specifies (for both the IIS and ASP.NET configuration systems) that the configuration entries only apply to the parent Web application.</span></span> <span data-ttu-id="a4c77-242">下面的示例显示要添加的**location**元素的语法：</span><span class="sxs-lookup"><span data-stu-id="a4c77-242">The following example shows the syntax of the **location** element to add:</span></span>

[!code-xml[Main](breaking-changes/samples/sample9.xml)]

<span data-ttu-id="a4c77-243">下面的示例演示如何使用**location**标记来包装从**appSettings**部分开始、以**system.webserver**节结尾的所有配置节。</span><span class="sxs-lookup"><span data-stu-id="a4c77-243">The following example shows how the **location** tag is used to wrap all configuration sections starting with the **appSettings** section and ending with **system.webServer** section.</span></span>

[!code-xml[Main](breaking-changes/samples/sample10.xml)]

<span data-ttu-id="a4c77-244">完成步骤1和步骤2后，子 ASP.NET 4 Web 应用程序将会启动且不会出错。</span><span class="sxs-lookup"><span data-stu-id="a4c77-244">When you have completed steps 1 and 2, child ASP.NET 4 Web applications will start without errors.</span></span>

<a id="0.1__Toc252995491"></a><a id="0.1__Toc255587640"></a><a id="0.1__Toc256770151"></a>

## <a name="aspnet-4-web-sites-fail-to-start-on-computers-where-sharepoint-is-installed"></a><span data-ttu-id="a4c77-245">ASP.NET 4 网站无法在安装了 SharePoint 的计算机上启动</span><span class="sxs-lookup"><span data-stu-id="a4c77-245">ASP.NET 4 Web Sites Fail to Start on Computers Where SharePoint Is Installed</span></span>

<span data-ttu-id="a4c77-246">运行 SharePoint 的 Web 服务器具有一个在 SharePoint 网站的根目录（例如，默认网站 `c:\inetpub\wwwroot\web.config`）下部署的 `Web.config` 文件。</span><span class="sxs-lookup"><span data-stu-id="a4c77-246">Web servers that run SharePoint have a `Web.config` file that is deployed at the root of a SharePoint Web site (for example, `c:\inetpub\wwwroot\web.config` for Default Web Site).</span></span> <span data-ttu-id="a4c77-247">在此 `Web.config` 文件中，SharePoint 会将名为 WSS\_的自定义部分信任级别设置为 "最小"。</span><span class="sxs-lookup"><span data-stu-id="a4c77-247">In this `Web.config` file, SharePoint sets a custom partial-trust level named WSS\_Minimal.</span></span>

<span data-ttu-id="a4c77-248">如果尝试运行部署为此类 SharePoint 网站的子网站的 ASP.NET 4 网站，将看到以下错误：</span><span class="sxs-lookup"><span data-stu-id="a4c77-248">If you try to run an ASP.NET 4 Web site that is deployed as a child of this type of SharePoint Web site, you will see the following error:</span></span>

`Could not find permission set named 'ASP.NET'.`

<span data-ttu-id="a4c77-249">发生此错误的原因是 ASP.NET 4 代码访问安全性（CAS）基础结构查找名为 ASP.NET 的权限集。</span><span class="sxs-lookup"><span data-stu-id="a4c77-249">This error occurs because the ASP.NET 4 code access security (CAS) infrastructure looks for a permission set named ASP.NET.</span></span> <span data-ttu-id="a4c77-250">但是，WSS\_所引用的部分信任配置文件不包含具有该名称的任何权限集。</span><span class="sxs-lookup"><span data-stu-id="a4c77-250">However, the partial trust configuration file that is referenced by WSS\_Minimal does not contain any permission sets with that name.</span></span>

<span data-ttu-id="a4c77-251">当前没有可与 ASP.NET 兼容的 SharePoint 版本。</span><span class="sxs-lookup"><span data-stu-id="a4c77-251">Currently there is not a version of SharePoint available that is compatible with ASP.NET.</span></span> <span data-ttu-id="a4c77-252">因此，不应尝试将 ASP.NET 4 网站作为子站点运行在 SharePoint 网站下。</span><span class="sxs-lookup"><span data-stu-id="a4c77-252">As a result, you should not attempt to run an ASP.NET 4 Web site as a child site underneath SharePoint Web sites.</span></span>

<a id="0.1__Toc255587641"></a><a id="0.1__Toc256770152"></a>

## <a name="the-httprequestfilepath-property-no-longer-includes-pathinfo-values"></a><span data-ttu-id="a4c77-253">HttpRequest 属性不再包括 PathInfo 值</span><span class="sxs-lookup"><span data-stu-id="a4c77-253">The HttpRequest.FilePath Property No Longer Includes PathInfo Values</span></span>

<span data-ttu-id="a4c77-254">以前版本的 ASP.NET 在从与文件路径相关的各种属性返回的值（包括**HttpRequest**、 **HttpRequest** **和 AppRelativeCurrentExecutionFilePath）** 中包含**PathInfo**值。</span><span class="sxs-lookup"><span data-stu-id="a4c77-254">Previous versions of ASP.NET included a **PathInfo** value in the value returned from various file path-related properties, including **HttpRequest.FilePath**, **HttpRequest.AppRelativeCurrentExecutionFilePath**, and **HttpRequest.CurrentExecutionFilePath**.</span></span> <span data-ttu-id="a4c77-255">ASP.NET 4 不再包含这些属性返回值中的**PathInfo**值。</span><span class="sxs-lookup"><span data-stu-id="a4c77-255">ASP.NET 4 no longer includes the **PathInfo** value in the return values from these properties.</span></span> <span data-ttu-id="a4c77-256">相反， **PathInfo**信息可在**HttpRequest**中找到。</span><span class="sxs-lookup"><span data-stu-id="a4c77-256">Instead, the **PathInfo** information is available in **HttpRequest.PathInfo**.</span></span> <span data-ttu-id="a4c77-257">例如，假定以下 URL 片段：</span><span class="sxs-lookup"><span data-stu-id="a4c77-257">For example, imagine the following URL fragment:</span></span>

`/testapp/Action.mvc/SomeAction`

<span data-ttu-id="a4c77-258">在早期版本的 ASP.NET 中， **HttpRequest**属性具有以下值：</span><span class="sxs-lookup"><span data-stu-id="a4c77-258">In earlier versions of ASP.NET, **HttpRequest** properties have the following values:</span></span>

<span data-ttu-id="a4c77-259">**HttpRequest**： `/testapp/Action.mvc/SomeAction`</span><span class="sxs-lookup"><span data-stu-id="a4c77-259">**HttpRequest.FilePath**: `/testapp/Action.mvc/SomeAction`</span></span>

<span data-ttu-id="a4c77-260">**HttpRequest. PathInfo**：（空）</span><span class="sxs-lookup"><span data-stu-id="a4c77-260">**HttpRequest.PathInfo**: (empty)</span></span>

<span data-ttu-id="a4c77-261">在 ASP.NET 4 中， **HttpRequest**属性改为具有以下值：</span><span class="sxs-lookup"><span data-stu-id="a4c77-261">In ASP.NET 4, **HttpRequest** properties instead have the following values:</span></span>

<span data-ttu-id="a4c77-262">**HttpRequest**： `/testapp/Action.mvc`</span><span class="sxs-lookup"><span data-stu-id="a4c77-262">**HttpRequest.FilePath**: `/testapp/Action.mvc`</span></span>

<span data-ttu-id="a4c77-263">**HttpRequest. PathInfo**： `SomeAction`</span><span class="sxs-lookup"><span data-stu-id="a4c77-263">**HttpRequest.PathInfo**: `SomeAction`</span></span>

<a id="0.1__Toc252995493"></a><a id="0.1__Toc255587642"></a><a id="0.1__Toc256770153"></a><a id="0.1__Toc245724861"></a>

## <a name="aspnet-20-applications-might-generate-httpexception-errors-that-reference-eurlaxd"></a><span data-ttu-id="a4c77-264">ASP.NET 2.0 应用程序可能生成引用 eurl 的 HttpException 错误</span><span class="sxs-lookup"><span data-stu-id="a4c77-264">ASP.NET 2.0 Applications Might Generate HttpException Errors that Reference eurl.axd</span></span>

<span data-ttu-id="a4c77-265">在 IIS 6 上启用 ASP.NET 4 后，IIS 6 上运行的 ASP.NET 2.0 应用（在 Windows Server 2003 或 Windows Server 2003 R2 中）可能会生成错误，如下所示：</span><span class="sxs-lookup"><span data-stu-id="a4c77-265">After ASP.NET 4 has been enabled on IIS 6, ASP.NET 2.0 applications that run on IIS 6 (in either Windows Server 2003 or Windows Server 2003 R2) might generate errors such as the following:</span></span>

`System.Web.HttpException: Path '/[yourApplicationRoot]/eurl.axd/[Value]' was not found.`

<span data-ttu-id="a4c77-266">之所以发生此错误，是因为当 ASP.NET 检测到网站配置为使用 ASP.NET 4 时，ASP.NET 4 的本机组件会将无扩展名 URL 传递到 ASP.NET 的托管部分，以便进一步处理。</span><span class="sxs-lookup"><span data-stu-id="a4c77-266">This error occurs because when ASP.NET detects that a Web site is configured to use ASP.NET 4, a native component of ASP.NET 4 passes an extensionless URL to the managed portion of ASP.NET for further processing.</span></span> <span data-ttu-id="a4c77-267">但是，如果将 ASP.NET 4 网站下的虚拟目录配置为使用 ASP.NET 2.0，则以这种方式处理无扩展名 URL 会导致修改的 URL 包含字符串 "eurl"。</span><span class="sxs-lookup"><span data-stu-id="a4c77-267">However, if virtual directories that are below an ASP.NET 4 Web site are configured to use ASP.NET 2.0, processing the extensionless URL in this way results in a modified URL that contains the string "eurl.axd".</span></span> <span data-ttu-id="a4c77-268">然后，将此修改后的 URL 发送到 ASP.NET 2.0 应用程序。</span><span class="sxs-lookup"><span data-stu-id="a4c77-268">This modified URL is then sent to the ASP.NET 2.0 application.</span></span> <span data-ttu-id="a4c77-269">ASP.NET 2.0 无法识别 "eurl" 格式。</span><span class="sxs-lookup"><span data-stu-id="a4c77-269">ASP.NET 2.0 cannot recognize the "eurl.axd" format.</span></span> <span data-ttu-id="a4c77-270">因此，ASP.NET 2.0 将尝试查找名为 `eurl.axd` 的文件并执行它。</span><span class="sxs-lookup"><span data-stu-id="a4c77-270">Therefore, ASP.NET 2.0 tries to find a file named `eurl.axd` and execute it.</span></span> <span data-ttu-id="a4c77-271">由于不存在此类文件，请求会失败，并出现**HttpException**异常。</span><span class="sxs-lookup"><span data-stu-id="a4c77-271">Because no such file exists, the request fails with an **HttpException** exception.</span></span>

<span data-ttu-id="a4c77-272">可以使用以下选项之一解决此问题。</span><span class="sxs-lookup"><span data-stu-id="a4c77-272">You can work around this issue using one of the following options.</span></span>

### <a name="option-1"></a><span data-ttu-id="a4c77-273">选项 1</span><span class="sxs-lookup"><span data-stu-id="a4c77-273">Option 1</span></span>

<span data-ttu-id="a4c77-274">如果运行该网站不需要 ASP.NET 4，请重新映射该网站以改用 ASP.NET 2.0。</span><span class="sxs-lookup"><span data-stu-id="a4c77-274">If ASP.NET 4 is not required in order to run the Web site, remap the site to use ASP.NET 2.0 instead.</span></span>

### <a name="option-2"></a><span data-ttu-id="a4c77-275">方法 2</span><span class="sxs-lookup"><span data-stu-id="a4c77-275">Option 2</span></span>

<span data-ttu-id="a4c77-276">如果需要 ASP.NET 4 才能运行该网站，请将所有子 ASP.NET 2.0 虚拟目录移动到映射到 ASP.NET 2.0 的其他网站。</span><span class="sxs-lookup"><span data-stu-id="a4c77-276">If ASP.NET 4 is required in order to run the Web site, move any child ASP.NET 2.0 virtual directories to a different Web site that is mapped to ASP.NET 2.0.</span></span>

### <a name="option-3"></a><span data-ttu-id="a4c77-277">选项3</span><span class="sxs-lookup"><span data-stu-id="a4c77-277">Option 3</span></span>

<span data-ttu-id="a4c77-278">如果无法将网站重新映射到 ASP.NET 2.0 或更改虚拟目录的位置，请在 ASP.NET 4 中显式禁用无扩展名 URL 处理。</span><span class="sxs-lookup"><span data-stu-id="a4c77-278">If it is not practical to remap the Web site to ASP.NET 2.0 or to change the location of a virtual directory, explicitly disable extensionless URL processing in ASP.NET 4.</span></span> <span data-ttu-id="a4c77-279">请按以下过程操作：</span><span class="sxs-lookup"><span data-stu-id="a4c77-279">Use the following procedure:</span></span>

1. <span data-ttu-id="a4c77-280">在 Windows 注册表中，打开以下节点：</span><span class="sxs-lookup"><span data-stu-id="a4c77-280">In the Windows registry, open the following node:</span></span>

`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ASP.NET\4.0.30319.0`

1. <span data-ttu-id="a4c77-281">创建名为**EnableExtensionlessUrls**的新**DWORD**值。</span><span class="sxs-lookup"><span data-stu-id="a4c77-281">Create a new **DWORD** value named **EnableExtensionlessUrls**.</span></span>
2. <span data-ttu-id="a4c77-282">将**EnableExtensionlessUrls**设置为0。</span><span class="sxs-lookup"><span data-stu-id="a4c77-282">Set **EnableExtensionlessUrls** to 0.</span></span> <span data-ttu-id="a4c77-283">这将禁用无扩展名 URL 行为。</span><span class="sxs-lookup"><span data-stu-id="a4c77-283">This disables extensionless URL behavior.</span></span>
3. <span data-ttu-id="a4c77-284">保存注册表值并关闭注册表编辑器。</span><span class="sxs-lookup"><span data-stu-id="a4c77-284">Save the registry value and close the registry editor.</span></span>
4. <span data-ttu-id="a4c77-285">运行**iisreset**命令行工具，该工具导致 IIS 读取新的注册表值。</span><span class="sxs-lookup"><span data-stu-id="a4c77-285">Run the **iisreset** command-line tool, which causes IIS to read the new registry value.</span></span>

> [!NOTE]
> <span data-ttu-id="a4c77-286">将**EnableExtensionlessUrls**设置为1可启用无扩展名 URL 行为。</span><span class="sxs-lookup"><span data-stu-id="a4c77-286">Setting **EnableExtensionlessUrls** to 1 enables extensionless URL behavior.</span></span> <span data-ttu-id="a4c77-287">如果未指定任何值，则这是默认设置。</span><span class="sxs-lookup"><span data-stu-id="a4c77-287">This is the default setting if no value is specified.</span></span>

<a id="0.1__Toc252995494"></a><a id="0.1__Toc255587643"></a><a id="0.1__Toc256770154"></a><a id="0.1__Toc245724862"></a>

## <a name="event-handlers-might-not-be-not-raised-in-a-default-document-in-iis-7-or-iis-75-integrated-mode"></a><span data-ttu-id="a4c77-288">IIS 7 或 IIS 7.5 集成模式下的默认文档中可能不会引发事件处理程序</span><span class="sxs-lookup"><span data-stu-id="a4c77-288">Event Handlers Might Not Be Not Raised in a Default Document in IIS 7 or IIS 7.5 Integrated Mode</span></span>

<span data-ttu-id="a4c77-289">ASP.NET 4 包含一些修改，这些修改将更改在无扩展名 URL 解析为默认文档时如何呈现 HTML **form**元素的**action**属性。</span><span class="sxs-lookup"><span data-stu-id="a4c77-289">ASP.NET 4 includes modifications that change how the **action** attribute of the HTML **form** element is rendered when an extensionless URL resolves to a default document.</span></span> <span data-ttu-id="a4c77-290">将[http://contoso.com/](http://contoso.com/)解析为默认文档的无扩展名 URL 示例，导致[http://contoso.com/Default.aspx](http://contoso.com/Default.aspx)的请求。</span><span class="sxs-lookup"><span data-stu-id="a4c77-290">An example of an extensionless URL resolving to a default document would be [http://contoso.com/](http://contoso.com/), resulting in a request to [http://contoso.com/Default.aspx](http://contoso.com/Default.aspx).</span></span>

<span data-ttu-id="a4c77-291">ASP.NET 4 现在会将 HTML**窗体**元素的**action**属性值呈现为空字符串，同时向其提供默认文档的无扩展名 URL 发出请求。</span><span class="sxs-lookup"><span data-stu-id="a4c77-291">ASP.NET 4 now renders the HTML **form** element's **action** attribute value as an empty string when a request is made to an extensionless URL that has a default document mapped to it.</span></span> <span data-ttu-id="a4c77-292">例如，在早期版本的 ASP.NET 中，对[http://contoso.com](http://contoso.com)的请求将导致请求 `Default.aspx`。</span><span class="sxs-lookup"><span data-stu-id="a4c77-292">For example, in earlier releases of ASP.NET, a request to [http://contoso.com](http://contoso.com) would result in a request to `Default.aspx`.</span></span> <span data-ttu-id="a4c77-293">在该文档中，开始**窗体**标记将呈现为，如以下示例中所示：</span><span class="sxs-lookup"><span data-stu-id="a4c77-293">In that document, the opening **form** tag would be rendered as in the following example:</span></span>

`<form action="Default.aspx" />`

<span data-ttu-id="a4c77-294">在 ASP.NET 4 中， [http://contoso.com](http://contoso.com)的请求也会导致对 `Default.aspx`的请求。</span><span class="sxs-lookup"><span data-stu-id="a4c77-294">In ASP.NET 4, a request to [http://contoso.com](http://contoso.com) also results in a request to `Default.aspx`.</span></span> <span data-ttu-id="a4c77-295">但是，ASP.NET 现在会呈现 HTML 打开的**窗体**标记，如以下示例中所示：</span><span class="sxs-lookup"><span data-stu-id="a4c77-295">However, ASP.NET now renders the HTML opening **form** tag as in the following example:</span></span>

`<form action="" />`

<span data-ttu-id="a4c77-296">如何呈现**操作**属性的这一差异可能会导致 IIS 和 ASP.NET 处理窗体发布的方式发生细微的更改。</span><span class="sxs-lookup"><span data-stu-id="a4c77-296">This difference in how the **action** attribute is rendered can cause subtle changes in how a form post is processed by IIS and ASP.NET.</span></span> <span data-ttu-id="a4c77-297">当**action**属性为空字符串时，IIS **DefaultDocumentModule**对象将创建 `Default.aspx`的子请求。</span><span class="sxs-lookup"><span data-stu-id="a4c77-297">When the **action** attribute is an empty string, the IIS **DefaultDocumentModule** object will create a child request to `Default.aspx`.</span></span> <span data-ttu-id="a4c77-298">在大多数情况下，此子请求对于应用程序代码是透明的，并且 "`Default.aspx`" 页将正常运行。</span><span class="sxs-lookup"><span data-stu-id="a4c77-298">Under most conditions, this child request is transparent to application code, and the `Default.aspx` page runs normally.</span></span>

<span data-ttu-id="a4c77-299">但托管代码和 IIS 7 或 IIS 7.5 集成模式之间可能的交互会导致托管 .aspx 页在子请求期间停止正常工作。</span><span class="sxs-lookup"><span data-stu-id="a4c77-299">However, a potential interaction between managed code and IIS 7 or IIS 7.5 Integrated mode can cause managed .aspx pages to stop working properly during the child request.</span></span> <span data-ttu-id="a4c77-300">如果出现以下情况，对 `Default.aspx` 文档的子请求将导致错误或意外行为：</span><span class="sxs-lookup"><span data-stu-id="a4c77-300">If the following conditions occur, the child request to a `Default.aspx` document will result in an error or in unexpected behavior:</span></span>

1. <span data-ttu-id="a4c77-301">.Aspx 页面将发送到浏览器，并将**form**元素的**action**特性设置为 ""。</span><span class="sxs-lookup"><span data-stu-id="a4c77-301">An .aspx page is sent to the browser with the **form** element's **action** attribute set to "".</span></span>
2. <span data-ttu-id="a4c77-302">窗体将回发到 ASP.NET。</span><span class="sxs-lookup"><span data-stu-id="a4c77-302">The form is posted back to ASP.NET.</span></span>
3. <span data-ttu-id="a4c77-303">托管 HTTP 模块读取实体正文的一部分。</span><span class="sxs-lookup"><span data-stu-id="a4c77-303">A managed HTTP module reads some part of the entity body.</span></span> <span data-ttu-id="a4c77-304">例如，模块读取**Request**或**request**。</span><span class="sxs-lookup"><span data-stu-id="a4c77-304">For example, a module reads **Request.Form** or **Request.Params**.</span></span> <span data-ttu-id="a4c77-305">这会使 POST 请求的实体正文读入托管内存中。</span><span class="sxs-lookup"><span data-stu-id="a4c77-305">This causes the entity body of the POST request to be read into managed memory.</span></span> <span data-ttu-id="a4c77-306">因此，实体正文不再对在 IIS 7 或 IIS 7.5 集成模式中运行的任何本机代码模块可用。</span><span class="sxs-lookup"><span data-stu-id="a4c77-306">As a result, the entity body is no longer available to any native code modules that are running in IIS 7 or IIS 7.5 Integrated mode.</span></span>
4. <span data-ttu-id="a4c77-307">IIS **DefaultDocumentModule**对象最终将运行并创建对 `Default.aspx` 文档的子请求。</span><span class="sxs-lookup"><span data-stu-id="a4c77-307">The IIS **DefaultDocumentModule** object eventually runs and creates a child request to the `Default.aspx` document.</span></span> <span data-ttu-id="a4c77-308">但由于一段托管代码已读取实体正文，因此没有可发送给子请求的实体正文。</span><span class="sxs-lookup"><span data-stu-id="a4c77-308">However, because the entity body has already been read by a piece of managed code, there is no entity body available to send to the child request.</span></span>
5. <span data-ttu-id="a4c77-309">当 HTTP 管道为子请求运行时，`.aspx` 文件的处理程序在处理程序执行阶段中运行。</span><span class="sxs-lookup"><span data-stu-id="a4c77-309">When the HTTP pipeline runs for the child request, the handler for `.aspx` files runs during the handler-execute phase.</span></span>
6. <span data-ttu-id="a4c77-310">由于没有实体正文，因此没有窗体变量和视图状态，因此 .aspx 页面处理程序不能使用任何信息来确定应引发哪个事件（如果有）。</span><span class="sxs-lookup"><span data-stu-id="a4c77-310">Because there is no entity body, there are no form variables and no view state, and therefore no information is available for the .aspx page handler to determine what event (if any) is supposed to be raised.</span></span> <span data-ttu-id="a4c77-311">因此，不会运行针对受影响 .aspx 页的任何回发事件处理程序。</span><span class="sxs-lookup"><span data-stu-id="a4c77-311">As a result, none of the postback event handlers for the affected .aspx page run.</span></span>

<span data-ttu-id="a4c77-312">可以通过以下方式解决此问题：</span><span class="sxs-lookup"><span data-stu-id="a4c77-312">You can work around this behavior in the following ways:</span></span>

- <span data-ttu-id="a4c77-313">标识在默认文档请求期间访问请求的实体正文的 HTTP 模块，并确定是否可将其配置为仅针对托管请求运行。</span><span class="sxs-lookup"><span data-stu-id="a4c77-313">Identify the HTTP module that is accessing the request's entity body during default document requests and determine whether it can be configured to run only for managed requests.</span></span> <span data-ttu-id="a4c77-314">在用于 IIS 7 和 IIS 7.5 的集成模式下，可通过将以下属性添加到模块的**system.webserver/** module 条目来将 HTTP 模块标记为仅针对托管请求运行：</span><span class="sxs-lookup"><span data-stu-id="a4c77-314">In Integrated mode for both IIS 7 and IIS 7.5, HTTP modules can be marked to run only for managed requests by adding the following attribute to the module's **system.webServer/modules** entry:</span></span>

- `precondition="managedHandler"`

- <span data-ttu-id="a4c77-315">此设置将禁用 IIS 7 和 IIS 7.5 确定为不是托管请求的请求的模块。</span><span class="sxs-lookup"><span data-stu-id="a4c77-315">This setting disables the module for requests that IIS 7 and IIS 7.5 determine as not being managed requests.</span></span> <span data-ttu-id="a4c77-316">对于默认的文档请求，第一个请求是无扩展名 URL。</span><span class="sxs-lookup"><span data-stu-id="a4c77-316">For default document requests, the first request is to an extensionless URL.</span></span> <span data-ttu-id="a4c77-317">因此，在初始请求处理过程中，IIS 不会运行用托管处理程序的前置条件标记的任何托管模块。</span><span class="sxs-lookup"><span data-stu-id="a4c77-317">Therefore, IIS does not run any managed modules that are marked with a precondition of managed Handler during initial request processing.</span></span> <span data-ttu-id="a4c77-318">因此，托管模块不会意外读取实体正文，因此实体正文仍可用，并传递给子请求和默认文档。</span><span class="sxs-lookup"><span data-stu-id="a4c77-318">As a result, managed modules will not accidentally read the entity body and thus the entity body is still available and is passed along to the child request and to the default document.</span></span>

- <span data-ttu-id="a4c77-319">如果有问题的 HTTP 模块必须为所有请求运行（对于可解析为**DefaultDocumentModule**对象的无扩展名 url，对于托管请求，等等），请通过将页面的**HtmlForm**控件的**Action**属性显式设置为非空字符串来修改受影响的 .aspx 页。</span><span class="sxs-lookup"><span data-stu-id="a4c77-319">If the problematic HTTP modules have to run for all requests (for static files, for extensionless URLs that resolve to the **DefaultDocumentModule** object, for managed requests, etc.), modify the affected .aspx pages by explicitly setting the **Action** property of the page's **System.Web.UI.HtmlControls.HtmlForm** control to a non-empty string.</span></span> <span data-ttu-id="a4c77-320">例如，如果 `Default.aspx`默认文档，请修改该页的代码，将**HtmlForm**控件的**Action**属性显式设置为 "default.aspx"。</span><span class="sxs-lookup"><span data-stu-id="a4c77-320">For example, if the default document is `Default.aspx`, modify the page's code to explicitly set the **HtmlForm** control's **Action** property to "Default.aspx".</span></span>

<a id="0.1__Toc255587644"></a><a id="0.1__Toc256770155"></a>

## <a name="changes-to-the-aspnet-code-access-security-cas-implementation"></a><span data-ttu-id="a4c77-321">对 ASP.NET 代码访问安全性（CAS）实现的更改</span><span class="sxs-lookup"><span data-stu-id="a4c77-321">Changes to the ASP.NET Code Access Security (CAS) Implementation</span></span>

<span data-ttu-id="a4c77-322">ASP.NET 2.0，通过扩展3.5 中添加的 ASP.NET 功能，请使用 .NET Framework 1.1 和2.0 代码访问安全性（CAS）模型。</span><span class="sxs-lookup"><span data-stu-id="a4c77-322">ASP.NET 2.0, and by extension the ASP.NET features that were added in 3.5, use the .NET Framework 1.1 and 2.0 code access security (CAS) model.</span></span> <span data-ttu-id="a4c77-323">但是，实质上已对 ASP.NET 4 中的 CAS 实现进行了检查。</span><span class="sxs-lookup"><span data-stu-id="a4c77-323">However, the implementation of CAS in ASP.NET 4 has been substantially overhauled.</span></span> <span data-ttu-id="a4c77-324">因此，依赖于全局程序集缓存（GAC）中运行的受信任代码的部分信任 ASP.NET 应用程序可能会失败，并会出现各种安全异常。</span><span class="sxs-lookup"><span data-stu-id="a4c77-324">As a result, partial-trust ASP.NET applications that rely on trusted code running in the global assembly cache (GAC) might fail with various security exceptions.</span></span> <span data-ttu-id="a4c77-325">依赖于计算机 CAS 策略的广泛修改的部分信任应用程序可能也会失败，并出现安全异常。</span><span class="sxs-lookup"><span data-stu-id="a4c77-325">Partial-trust applications that rely on extensive modifications to machine CAS policy might also fail with security exceptions.</span></span>

<span data-ttu-id="a4c77-326">你可以使用**信任**配置元素中的新**legacyCasModel**特性，将部分信任 ASP.NET 4 应用程序还原为 ASP.NET 1.1 和2.0 的行为，如以下示例中所示：</span><span class="sxs-lookup"><span data-stu-id="a4c77-326">You can revert partial-trust ASP.NET 4 applications to the behavior of ASP.NET 1.1 and 2.0 using the new **legacyCasModel** attribute in the **trust** configuration element, as shown in the following example:</span></span>

`<trust level= "Medium" legacyCasModel="true" />`

<span data-ttu-id="a4c77-327">恢复为旧的 CAS 模型时，会启用以下旧的 CA 行为：</span><span class="sxs-lookup"><span data-stu-id="a4c77-327">When you revert to the legacy CAS model, the following old CAS behaviors are enabled:</span></span>

- <span data-ttu-id="a4c77-328">计算机 CAS 策略已生效。</span><span class="sxs-lookup"><span data-stu-id="a4c77-328">Machine CAS policy is honored.</span></span>
- <span data-ttu-id="a4c77-329">允许在单个应用程序域中使用多个不同的权限集。</span><span class="sxs-lookup"><span data-stu-id="a4c77-329">Multiple different permission sets in a single application domain are allowed.</span></span>
- <span data-ttu-id="a4c77-330">如果在堆栈上只有 ASP.NET 或其他 .NET Framework 代码，则将调用 GAC 中的程序集不需要显式权限断言。</span><span class="sxs-lookup"><span data-stu-id="a4c77-330">Explicit permission assertions are not required for assemblies in the GAC that are invoked when only ASP.NET or other .NET Framework code is on the stack.</span></span>

<span data-ttu-id="a4c77-331">无法在 .NET Framework 4 中还原一个方案：非 Web 部分信任应用程序无法再调用 System.web 和 System.web 中的某些 Api。</span><span class="sxs-lookup"><span data-stu-id="a4c77-331">One scenario cannot be reverted in the .NET Framework 4: non-Web partial-trust applications can no longer call certain APIs in System.Web.dll and System.Web.Extensions.dll.</span></span> <span data-ttu-id="a4c77-332">在 .NET Framework 的以前版本中，可能会向非 Web 部分信任应用程序显式授予**AspNetHostingPermission**权限。</span><span class="sxs-lookup"><span data-stu-id="a4c77-332">In previous versions of the .NET Framework, it was possible for non-Web partial-trust applications to be explicitly granted **AspNetHostingPermission** permissions.</span></span> <span data-ttu-id="a4c77-333">然后，这些应用程序可使用**httputility.javascriptstringencode**、 **microsoft.samples.synchronization.clientservices.custom.\*** 命名空间中的类型和与成员资格、角色和配置文件相关的类型。</span><span class="sxs-lookup"><span data-stu-id="a4c77-333">These applications could then use **System.Web.HttpUtility**, types in the **System.Web.ClientServices.\*** namespaces, and types related to membership, roles, and profiles.</span></span> <span data-ttu-id="a4c77-334">.NET Framework 4 中不再支持从非 Web 部分信任应用程序调用这些类型。</span><span class="sxs-lookup"><span data-stu-id="a4c77-334">Calling these types from non-Web partial trust applications is no longer supported in the .NET Framework 4.</span></span>

> [!NOTE]
> <span data-ttu-id="a4c77-335">**Httputility.javascriptstringencode**类的**server.htmlencode**和**system.net.webutility.htmldecode**功能已移至新的 .NET Framework 4**系统 .net**类。</span><span class="sxs-lookup"><span data-stu-id="a4c77-335">The **HtmlEncode** and **HtmlDecode** functionality of the **System.Web.HttpUtility** class was moved to the new .NET Framework 4 **System.Net.WebUtility** class.</span></span> <span data-ttu-id="a4c77-336">如果这是唯一使用的 ASP.NET 功能，请修改应用程序的代码以改用新的**webutility.htmldecode**类。</span><span class="sxs-lookup"><span data-stu-id="a4c77-336">If that was the only ASP.NET functionality that was being used, modify the application's code to use the new **WebUtility** class instead.</span></span>

<span data-ttu-id="a4c77-337">下面是对 ASP.NET 4 中默认 CAS 实现所做更改的高级摘要：</span><span class="sxs-lookup"><span data-stu-id="a4c77-337">The following is a high-level summary of the changes to the default CAS implementation in ASP.NET 4:</span></span>

- <span data-ttu-id="a4c77-338">ASP.NET 应用程序域现在是同类应用程序域。</span><span class="sxs-lookup"><span data-stu-id="a4c77-338">ASP.NET application domains are now homogeneous application domains.</span></span> <span data-ttu-id="a4c77-339">只有部分信任和完全信任授权集在应用程序域中可用。</span><span class="sxs-lookup"><span data-stu-id="a4c77-339">Only partial-trust and full-trust grant sets are available in an application domain.</span></span>
- <span data-ttu-id="a4c77-340">ASP.NET 部分信任授予集独立于任何企业级、计算机级别或用户级别的 CAS 策略。</span><span class="sxs-lookup"><span data-stu-id="a4c77-340">ASP.NET partial-trust grant sets are independent from any enterprise-level, machine-level, or user-level CAS policy.</span></span>
- <span data-ttu-id="a4c77-341">3\.5 和 3.5 SP1 随附的 ASP.NET 程序集已转换为使用 .NET Framework 4 透明度模型。</span><span class="sxs-lookup"><span data-stu-id="a4c77-341">ASP.NET assemblies that shipped in 3.5 and 3.5 SP1 have been converted to use the .NET Framework 4 transparency model.</span></span>
- <span data-ttu-id="a4c77-342">ASP.NET **AspNetHostingPermission**属性的使用大大减少。</span><span class="sxs-lookup"><span data-stu-id="a4c77-342">Use of the ASP.NET **AspNetHostingPermission** attribute has been substantially reduced.</span></span> <span data-ttu-id="a4c77-343">此属性的大多数实例已从公共 ASP.NET Api 中删除。</span><span class="sxs-lookup"><span data-stu-id="a4c77-343">Most instances of this attribute have been removed from the public ASP.NET APIs.</span></span>
- <span data-ttu-id="a4c77-344">已更新由 ASP.NET 生成提供程序创建的动态编译的程序集，以将程序集显式标记为透明。</span><span class="sxs-lookup"><span data-stu-id="a4c77-344">Dynamically compiled assemblies that are created by ASP.NET build providers have been updated to explicitly mark assemblies as transparent.</span></span>
- <span data-ttu-id="a4c77-345">现在，所有 ASP.NET 程序集都标记为只能在 Web 宿主环境中使用 APTCA 特性。</span><span class="sxs-lookup"><span data-stu-id="a4c77-345">All ASP.NET assemblies are now marked in such a way that the APTCA attribute is honored only in Web hosting environments.</span></span> <span data-ttu-id="a4c77-346">部分受信任的非 Web 宿主环境（如 ClickOnce）将无法调用到 ASP.NET 程序集。</span><span class="sxs-lookup"><span data-stu-id="a4c77-346">Partially trusted non-Web hosting environments like ClickOnce will not be able to call into ASP.NET assemblies.</span></span>

<span data-ttu-id="a4c77-347">有关新的 ASP.NET 4 代码访问安全模型的详细信息，请参阅 MSDN 网站上的[使用 ASP.NET 应用程序中的代码访问安全性](https://msdn.microsoft.com/library/dd984947%28VS.100%29.aspx)。</span><span class="sxs-lookup"><span data-stu-id="a4c77-347">For more information about the new ASP.NET 4 code access security model, see [Using Code Access Security in ASP.NET Applications](https://msdn.microsoft.com/library/dd984947%28VS.100%29.aspx) on the MSDN Web site.</span></span>

<a id="0.1__Toc256770156"></a><a id="0.1__Toc245724863"></a><a id="0.1__Toc252995496"></a><a id="0.1__Toc255587645"></a><a id="0.1__Toc245724864"></a>

## <a name="membershipuser-and-other-types-in-the-systemwebsecurity-namespace-have-been-moved"></a><span data-ttu-id="a4c77-348">MembershipUser 命名空间中的其他类型已移动</span><span class="sxs-lookup"><span data-stu-id="a4c77-348">MembershipUser and Other Types in the System.Web.Security Namespace Have Been Moved</span></span>

<span data-ttu-id="a4c77-349">ASP.NET 成员身份中使用的某些类型已从 `System.Web.dll` 移动到新的 Microsoft.visualbasic.applicationservices.cantstartsingleinstanceexception 程序集。</span><span class="sxs-lookup"><span data-stu-id="a4c77-349">Some types that are used in ASP.NET membership have been moved from `System.Web.dll` to the new System.Web.ApplicationServices.dll assembly.</span></span> <span data-ttu-id="a4c77-350">移动这些类型是为了解析客户端中的类型与扩展的 .NET Framework SKU 中的类型之间的体系结构层依赖关系。</span><span class="sxs-lookup"><span data-stu-id="a4c77-350">The types were moved in order to resolve architectural layering dependencies between types in the client and in extended .NET Framework SKUs.</span></span>

<span data-ttu-id="a4c77-351">由于已将 Microsoft.visualbasic.applicationservices.cantstartsingleinstanceexception 添加到由 ASP.NET 编译系统默认使用的被引用程序集的列表中，因此网站项目在移动这些类型时没有问题。</span><span class="sxs-lookup"><span data-stu-id="a4c77-351">Web site projects do not have problems as a result of moving these types, because System.Web.ApplicationServices.dll was added to the list of referenced assemblies that is used by default by the ASP.NET compilation system.</span></span> <span data-ttu-id="a4c77-352">如果将使用早期版本的 ASP.NET 创建的网站项目升级到 ASP.NET 4，则在 Visual Studio 2010 中打开该项目时，该项目将在编译时不会出错。</span><span class="sxs-lookup"><span data-stu-id="a4c77-352">If you upgrade a Web site project that was created using an earlier version of ASP.NET to ASP.NET 4 by opening it in Visual Studio 2010, the project will compile without errors.</span></span>

<span data-ttu-id="a4c77-353">同样，如果你将在早期版本的 ASP.NET 中创建的 Web 应用程序项目升级到 ASP.NET 4，则在 Visual Studio 2010 中打开该项目时，升级过程会将对该项目的引用添加到该项目中。</span><span class="sxs-lookup"><span data-stu-id="a4c77-353">Similarly, if you upgrade a Web application project that was created in an earlier version of ASP.NET to ASP.NET 4 by opening it in Visual Studio 2010, the upgrade process adds a reference to System.Web.ApplicationServices.dll to the project.</span></span> <span data-ttu-id="a4c77-354">因此，升级后的 Web 应用程序项目也会编译而不出错。</span><span class="sxs-lookup"><span data-stu-id="a4c77-354">Therefore, upgraded Web application projects will also compile without errors.</span></span>

<span data-ttu-id="a4c77-355">使用早期版本的 ASP.NET 创建的已编译（二进制）文件也会在 ASP.NET 4 上运行而不会出现错误，即使成员身份类型已移到不同的程序集。</span><span class="sxs-lookup"><span data-stu-id="a4c77-355">Compiled (binary) files that were created using earlier versions of ASP.NET will also run without errors on ASP.NET 4, even though the membership types were moved to a different assembly.</span></span> <span data-ttu-id="a4c77-356">类型转发信息已添加到 `System.Web.dll` 的 ASP.NET 4 版本中，可自动将这些类型的运行时引用路由到类型的新位置。</span><span class="sxs-lookup"><span data-stu-id="a4c77-356">Type forwarding information has been added to the ASP.NET 4 version of `System.Web.dll` that automatically routes run-time references for these types to the new location for the types.</span></span>

<span data-ttu-id="a4c77-357">但是，使用特定成员身份类型并且已从早期版本的 ASP.NET 升级的类库在 ASP.NET 4 项目中使用时将无法进行编译。</span><span class="sxs-lookup"><span data-stu-id="a4c77-357">However, class libraries that use specific membership types and that have been upgraded from earlier versions of ASP.NET will fail to compile when used in an ASP.NET 4 project.</span></span> <span data-ttu-id="a4c77-358">例如，类库项目可能无法编译并报告错误，如下所示：</span><span class="sxs-lookup"><span data-stu-id="a4c77-358">For example, a class library project might fail to compile and report an error such as the following:</span></span>

- `The type 'System.Web.Security.MembershipUser' is defined in an assembly that is not referenced. You must add a reference to assembly 'System.Web.ApplicationServices, Version=4.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35'.`

- `The type name 'MembershipUser' could not be found. This type has been forwarded to assembly 'System.Web.ApplicationServices, Version=4.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35'. Consider adding a reference to that assembly.`

<span data-ttu-id="a4c77-359">可以通过将类库项目中的引用添加到 Microsoft.visualbasic.applicationservices.cantstartsingleinstanceexception 来解决此问题。</span><span class="sxs-lookup"><span data-stu-id="a4c77-359">You can work around this problem by adding a reference in your class library project to System.Web.ApplicationServices.dll.</span></span>

<span data-ttu-id="a4c77-360">以下列表显示了已从 `System.Web.dll` 移动到 Microsoft.visualbasic.applicationservices.cantstartsingleinstanceexception 的*system.web. Security*类型：</span><span class="sxs-lookup"><span data-stu-id="a4c77-360">The following list shows the *System.Web.Security* types that were moved from `System.Web.dll` to System.Web.ApplicationServices.dll:</span></span>

- <span data-ttu-id="a4c77-361">*System.web. MembershipCreateStatus*</span><span class="sxs-lookup"><span data-stu-id="a4c77-361">*System.Web.Security.MembershipCreateStatus*</span></span>
- <span data-ttu-id="a4c77-362">*"CreateUserException"。*</span><span class="sxs-lookup"><span data-stu-id="a4c77-362">*System.Web.Security.Membership.CreateUserException*</span></span>
- <span data-ttu-id="a4c77-363">*System.web. System.web.security.membershippasswordexception*</span><span class="sxs-lookup"><span data-stu-id="a4c77-363">*System.Web.Security.MembershipPasswordException*</span></span>
- <span data-ttu-id="a4c77-364">*System.web. MembershipPasswordFormat*</span><span class="sxs-lookup"><span data-stu-id="a4c77-364">*System.Web.Security.MembershipPasswordFormat*</span></span>
- <span data-ttu-id="a4c77-365">*System.web. node.js*</span><span class="sxs-lookup"><span data-stu-id="a4c77-365">*System.Web.Security.MembershipProvider*</span></span>
- <span data-ttu-id="a4c77-366">*System.web. MembershipProviderCollection*</span><span class="sxs-lookup"><span data-stu-id="a4c77-366">*System.Web.Security.MembershipProviderCollection*</span></span>
- <span data-ttu-id="a4c77-367">*System.web. MembershipUser*</span><span class="sxs-lookup"><span data-stu-id="a4c77-367">*System.Web.Security.MembershipUser*</span></span>
- <span data-ttu-id="a4c77-368">*System.web. MembershipUserCollection*</span><span class="sxs-lookup"><span data-stu-id="a4c77-368">*System.Web.Security.MembershipUserCollection*</span></span>
- <span data-ttu-id="a4c77-369">*System.web. MembershipValidatePasswordEventHandler*</span><span class="sxs-lookup"><span data-stu-id="a4c77-369">*System.Web.Security.MembershipValidatePasswordEventHandler*</span></span>
- <span data-ttu-id="a4c77-370">*System.web. ValidatePasswordEventArgs*</span><span class="sxs-lookup"><span data-stu-id="a4c77-370">*System.Web.Security.ValidatePasswordEventArgs*</span></span>
- <span data-ttu-id="a4c77-371">*System.web. RoleProvider*</span><span class="sxs-lookup"><span data-stu-id="a4c77-371">*System.Web.Security.RoleProvider*</span></span>
- <a id="0.1_a"></a><span data-ttu-id="a4c77-372">*System.web. MembershipPasswordCompatibilityMode*</span><span class="sxs-lookup"><span data-stu-id="a4c77-372">*System.Web.Configuration.MembershipPasswordCompatibilityMode*</span></span>

<a id="0.1__Toc256770157"></a>

## <a name="output-caching-changes-to-vary--http-header"></a><span data-ttu-id="a4c77-373">\* HTTP 标头变化的输出缓存更改</span><span class="sxs-lookup"><span data-stu-id="a4c77-373">Output Caching Changes to Vary \* HTTP Header</span></span>

<span data-ttu-id="a4c77-374">在 ASP.NET 1.0 中，bug 导致指定 `Location="ServerAndClient"` 作为输出的缓存页在响应中发出 `Vary:*` HTTP 标头。</span><span class="sxs-lookup"><span data-stu-id="a4c77-374">In ASP.NET 1.0, a bug caused cached pages that specified `Location="ServerAndClient"` as an output–cache setting to emit a `Vary:*` HTTP header in the response.</span></span> <span data-ttu-id="a4c77-375">这还能起到告知客户端浏览器绝不要本地对页进行缓存的作用。</span><span class="sxs-lookup"><span data-stu-id="a4c77-375">This had the effect of telling client browsers to never cache the page locally.</span></span>

<span data-ttu-id="a4c77-376">在 ASP.NET 1.1 中，添加了**HttpCachePolicy. SetOmitVaryStar**方法，你可以调用它来取消 `Vary:*` 标头。</span><span class="sxs-lookup"><span data-stu-id="a4c77-376">In ASP.NET 1.1, the **System.Web.HttpCachePolicy.SetOmitVaryStar** method was added, which you could call to suppress the `Vary:*` header.</span></span> <span data-ttu-id="a4c77-377">之所以选择此方法，是因为更改发出的 HTTP 标头时被视为可能重大更改。</span><span class="sxs-lookup"><span data-stu-id="a4c77-377">This method was chosen because changing the emitted HTTP header was considered a potentially breaking change at the time.</span></span> <span data-ttu-id="a4c77-378">但是，开发人员与 ASP.NET 中的行为感到困惑，bug 报告建议开发人员不知道现有的**SetOmitVaryStar**行为。</span><span class="sxs-lookup"><span data-stu-id="a4c77-378">However, developers have been confused by the behavior in ASP.NET, and bug reports suggest that developers are unaware of the existing **SetOmitVaryStar** behavior.</span></span>

<span data-ttu-id="a4c77-379">在 ASP.NET 4 中，决定解决根本问题。</span><span class="sxs-lookup"><span data-stu-id="a4c77-379">In ASP.NET 4, the decision was made to fix the root problem.</span></span> <span data-ttu-id="a4c77-380">不再从指定以下指令的响应发出 `Vary:*` HTTP 标头：</span><span class="sxs-lookup"><span data-stu-id="a4c77-380">The `Vary:*` HTTP header is no longer emitted from responses that specify the following directive:</span></span>

`<%@OutputCache Location="ServerAndClient" %>`

<span data-ttu-id="a4c77-381">因此，不再需要**SetOmitVaryStar**来禁止 `Vary:*` 标头。</span><span class="sxs-lookup"><span data-stu-id="a4c77-381">As a result, **SetOmitVaryStar** is no longer needed in order to suppress the `Vary:*` header.</span></span>

<span data-ttu-id="a4c77-382">在指定页面上 **@ OutputCache**指令中的 `Location="ServerAndClient"` 的应用程序中，现在可以看到**Location**属性的值的名称所隐含的行为，即，可以在浏览器中缓存页面，而无需调用**SetOmitVaryStar**方法。</span><span class="sxs-lookup"><span data-stu-id="a4c77-382">In applications that specify `Location="ServerAndClient"` in the **@ OutputCache** directive on a page, you will now see the behavior implied by the name of the **Location** attribute's value – that is, pages will be cacheable in the browser without requiring that you call the **SetOmitVaryStar** method.</span></span>

<span data-ttu-id="a4c77-383">如果应用程序中的页必须发出 `Vary:*`，请调用**AppendHeader**方法，如以下示例中所示：</span><span class="sxs-lookup"><span data-stu-id="a4c77-383">If pages in your application must emit `Vary:*`, call the **AppendHeader** method, as in the following example:</span></span>

`HttpResponse.AppendHeader("Vary","*");`

<span data-ttu-id="a4c77-384">或者，您可以将 "输出缓存**位置**" 属性的值更改为 "Server"。</span><span class="sxs-lookup"><span data-stu-id="a4c77-384">Alternatively, you can change the value of the output caching **Location** attribute to "Server".</span></span>

<a id="0.1__Toc255587646"></a><a id="0.1__Toc256770158"></a>

## <a name="systemwebsecurity-types-for-passport-are-obsolete"></a><span data-ttu-id="a4c77-385">Passport 的安全类型已过时</span><span class="sxs-lookup"><span data-stu-id="a4c77-385">System.Web.Security Types for Passport are Obsolete</span></span>

<span data-ttu-id="a4c77-386">由于 Passport 中的更改（现在是 LiveID），ASP.NET 2.0 中内置的 Passport 支持已过时且不受支持。</span><span class="sxs-lookup"><span data-stu-id="a4c77-386">The Passport support built into ASP.NET 2.0 has been obsolete and unsupported for a few years due to changes in Passport (now LiveID).</span></span> <span data-ttu-id="a4c77-387">因此，与**system.web**中的 Passport 相关的五个类型现在使用**ObsoleteAttribute**属性进行标记。</span><span class="sxs-lookup"><span data-stu-id="a4c77-387">As a result, the five types related to Passport in **System.Web.Security** are now marked with the **ObsoleteAttribute** attribute.</span></span>

<a id="0.1__The_MenuItem.PopOutImageUrl_Propert"></a><a id="0.1__Toc256770159"></a>

## <a name="the-menuitempopoutimageurl-property-fails-to-render-an-image-in-aspnet-4"></a><span data-ttu-id="a4c77-388">PopOutImageUrl 属性未能呈现 ASP.NET 4 中的图像</span><span class="sxs-lookup"><span data-stu-id="a4c77-388">The MenuItem.PopOutImageUrl Property Fails to Render an Image in ASP.NET 4</span></span>

<span data-ttu-id="a4c77-389">在 ASP.NET 3.5 中， *PopOutImageUrl*属性允许你指定显示在菜单项中的图像的 URL，以指示菜单项具有动态子菜单。</span><span class="sxs-lookup"><span data-stu-id="a4c77-389">In ASP.NET 3.5, the *MenuItem.PopOutImageUrl* property lets you specify the URL for an image that is displayed in a menu item to indicate that the menu item has a dynamic submenu.</span></span> <span data-ttu-id="a4c77-390">下面的示例演示如何在 ASP.NET 3.5 的标记中指定此属性。</span><span class="sxs-lookup"><span data-stu-id="a4c77-390">The following example shows how to specify this property in markup in ASP.NET 3.5.</span></span>

[!code-aspx[Main](breaking-changes/samples/sample11.aspx)]

<span data-ttu-id="a4c77-391">由于 ASP.NET 4 中的设计更改，如果为*MenuItem*类设置了属性，则不会呈现*PopOutImageUrl*的输出。</span><span class="sxs-lookup"><span data-stu-id="a4c77-391">As a result of a design change in ASP.NET 4, no output is rendered for the *PopOutImageUrl* if the property is set for the *MenuItem* class.</span></span> <span data-ttu-id="a4c77-392">相反，必须使用*StaticPopOutImageUrl*属性或*DynamicPopOutImageUrl*属性直接在*MENU*控件中指定图像 URL。</span><span class="sxs-lookup"><span data-stu-id="a4c77-392">Instead, you must specify an image URL directly in the *Menu* control using either the *StaticPopOutImageUrl* property or the *DynamicPopOutImageUrl* property.</span></span> <span data-ttu-id="a4c77-393">使用静态菜单时， *StaticPopOutImageUrl*属性指定显示的图像的 URL，以指示静态菜单项包含子菜单，如以下示例中所示：</span><span class="sxs-lookup"><span data-stu-id="a4c77-393">When you work with a static menu, the *Menu.StaticPopOutImageUrl* property specifies the URL for an image that is displayed in order to indicate that the static menu item has a submenu, as shown in the following example:</span></span>

[!code-aspx[Main](breaking-changes/samples/sample12.aspx)]

<span data-ttu-id="a4c77-394">如果使用的是动态菜单，请使用*DynamicPopOutImageUrl*属性来指定图像的 URL，该图像指示动态菜单项具有子菜单。</span><span class="sxs-lookup"><span data-stu-id="a4c77-394">If you are working with a dynamic menu, you use the *Menu.DynamicPopOutImageUrl* property to specify the URL for an image that indicates that a dynamic menu item has a submenu.</span></span> <span data-ttu-id="a4c77-395">下面的示例与上一个示例类似，但演示了如何设置动态菜单的*DynamicPopOutImageUrl*属性。</span><span class="sxs-lookup"><span data-stu-id="a4c77-395">The following example is similar to the previous one, but shows how to set the *DynamicPopOutImageUrl* property for a dynamic menu.</span></span>

[!code-aspx[Main](breaking-changes/samples/sample13.aspx)]

<span data-ttu-id="a4c77-396">如果未设置*DynamicPopOutImageUrl*属性，并且*DynamicEnableDefaultPopOutImage*属性设置为*false*，则不会显示图像。</span><span class="sxs-lookup"><span data-stu-id="a4c77-396">If the *Menu.DynamicPopOutImageUrl* property is not set and the *Menu.DynamicEnableDefaultPopOutImage* property is set to *false*, no image is displayed.</span></span> <span data-ttu-id="a4c77-397">同样，如果未设置*StaticPopOutImageUrl*属性，并且*StaticEnableDefaultPopOutImage*属性设置为*false*，则不会显示图像。</span><span class="sxs-lookup"><span data-stu-id="a4c77-397">Similarly, if the *StaticPopOutImageUrl* property is not set and the *StaticEnableDefaultPopOutImage* property is set to *false*, no image is displayed.</span></span>

<span data-ttu-id="a4c77-398">设置这些属性的路径时，请使用正斜杠（/）而不是反斜杠（\)。</span><span class="sxs-lookup"><span data-stu-id="a4c77-398">When you set the paths for these properties, use a forward slash (/) instead of a backslash (\).</span></span> <span data-ttu-id="a4c77-399">有关详细信息，请参阅[StaticPopOutImageUrl 和 DynamicPopOutImageUrl 无法呈现图像，因为路径包含](#0.1__Menu.StaticPopOutImageUrl_and_Menu. "_Menu. StaticPopOutImageUrl_and_Menu。")本文档其他位置的反斜杠。</span><span class="sxs-lookup"><span data-stu-id="a4c77-399">For more information, see [Menu.StaticPopOutImageUrl and Menu.DynamicPopOutImageUrl Fail to Render Images When Paths Contain Backslashes](#0.1__Menu.StaticPopOutImageUrl_and_Menu. "_Menu.StaticPopOutImageUrl_and_Menu.") elsewhere in this document.</span></span>

<a id="0.1__Menu.StaticPopOutImageUrl_and_Menu."></a><a id="0.1__Toc256770160"></a>

## <a name="menustaticpopoutimageurl-and-menudynamicpopoutimageurl-fail-to-render-images-when-paths-contain-backslashes"></a><span data-ttu-id="a4c77-400">当路径包含反斜杠时，StaticPopOutImageUrl 和 DynamicPopOutImageUrl 无法呈现图像</span><span class="sxs-lookup"><span data-stu-id="a4c77-400">Menu.StaticPopOutImageUrl and Menu.DynamicPopOutImageUrl Fail to Render Images When Paths Contain Backslashes</span></span>

<span data-ttu-id="a4c77-401">在 ASP.NET 4 中，如果路径包含 backlashes （\)，则不会呈现使用*StaticPopOutImageUrl*和*DynamicPopOutImageUrl*属性指定的图像。</span><span class="sxs-lookup"><span data-stu-id="a4c77-401">In ASP.NET 4, the images that you specify using the *Menu.StaticPopOutImageUrl* and *Menu.DynamicPopOutImageUrl* properties will not render if the path contains backlashes (\).</span></span> <span data-ttu-id="a4c77-402">这是对早期版本的 ASP.NET 的更改。</span><span class="sxs-lookup"><span data-stu-id="a4c77-402">This is a change from earlier versions of ASP.NET.</span></span>

<span data-ttu-id="a4c77-403">以下*Menu*控件标记的示例显示了*StaticPopOutImageUrl*属性集，其中使用了包含反斜杠的路径。</span><span class="sxs-lookup"><span data-stu-id="a4c77-403">The following example of *Menu* control markup shows the *StaticPopOutImageUrl* property set using a path that contains a backslash.</span></span> <span data-ttu-id="a4c77-404">在 ASP.NET 4 中，将不呈现在属性中指定的图像。</span><span class="sxs-lookup"><span data-stu-id="a4c77-404">In ASP.NET 4, the image specified in the property will not render.</span></span>

[!code-aspx[Main](breaking-changes/samples/sample14.aspx)]

<span data-ttu-id="a4c77-405">若要更正此问题，请将*StaticPopOutImageUrl*和*DynamicPopOutImageUrl*属性中指定的路径值更改为使用正斜杠（/）。</span><span class="sxs-lookup"><span data-stu-id="a4c77-405">To correct this issue, change path values that are specified in the *StaticPopOutImageUrl* and *DynamicPopOutImageUrl* properties to use forward slashes (/).</span></span> <span data-ttu-id="a4c77-406">下面的示例演示了此更改：</span><span class="sxs-lookup"><span data-stu-id="a4c77-406">The following example shows this change:</span></span>

[!code-aspx[Main](breaking-changes/samples/sample15.aspx)]

<span data-ttu-id="a4c77-407">请注意，从早期版本的 ASP.NET 迁移到 ASP.NET 4 的应用程序可能也会受到影响，因为*PopOutImageUrl*属性已更改。</span><span class="sxs-lookup"><span data-stu-id="a4c77-407">Note that applications that were migrated from earlier versions of ASP.NET to ASP.NET 4 might also be affected, because the *MenuItem.PopOutImageUrl* property has been changed.</span></span> <span data-ttu-id="a4c77-408">有关详细信息，请参阅 PopOutImageUrl 属性无法在本文档中的其他位置[呈现 ASP.NET 4 中的图像](#0.1__The_MenuItem.PopOutImageUrl_Propert "_The_MenuItem. PopOutImageUrl_Propert")。</span><span class="sxs-lookup"><span data-stu-id="a4c77-408">For more information, see [The MenuItem.PopOutImageUrl Property Fails to Render an Image in ASP.NET 4](#0.1__The_MenuItem.PopOutImageUrl_Propert "_The_MenuItem.PopOutImageUrl_Propert") elsewhere in this document.</span></span>

<a id="0.1__Toc224729061"></a><a id="0.1__Toc255587647"></a><a id="0.1__Toc256770161"></a>

## <a name="disclaimer"></a><span data-ttu-id="a4c77-409">免责声明</span><span class="sxs-lookup"><span data-stu-id="a4c77-409">Disclaimer</span></span>

<span data-ttu-id="a4c77-410">这是一份初稿，并可能在本文所述软件最终商业发布之前进行大幅更改。</span><span class="sxs-lookup"><span data-stu-id="a4c77-410">This is a preliminary document and may be changed substantially prior to final commercial release of the software described herein.</span></span>

<span data-ttu-id="a4c77-411">本文所含信息代表 Microsoft Corporation 对截至发布之日所讨论问题持有的当前观点。</span><span class="sxs-lookup"><span data-stu-id="a4c77-411">The information contained in this document represents the current view of Microsoft Corporation on the issues discussed as of the date of publication.</span></span> <span data-ttu-id="a4c77-412">由于 Microsoft 必须对不断变化的市场情况作出响应，所以不应将本文解释为是 Microsoft 做出的承诺，Microsoft 并不保证所提供的任何信息在公布之日后的准确性。</span><span class="sxs-lookup"><span data-stu-id="a4c77-412">Because Microsoft must respond to changing market conditions, it should not be interpreted to be a commitment on the part of Microsoft, and Microsoft cannot guarantee the accuracy of any information presented after the date of publication.</span></span>

<span data-ttu-id="a4c77-413">本白皮书仅用于提供信息。</span><span class="sxs-lookup"><span data-stu-id="a4c77-413">This White Paper is for informational purposes only.</span></span> <span data-ttu-id="a4c77-414">MICROSOFT 对本文档中的信息不做任何明示、暗示或法定的担保。</span><span class="sxs-lookup"><span data-stu-id="a4c77-414">MICROSOFT MAKES NO WARRANTIES, EXPRESS, IMPLIED OR STATUTORY, AS TO THE INFORMATION IN THIS DOCUMENT.</span></span>

<span data-ttu-id="a4c77-415">遵守所有适用的著作权法是用户的责任。</span><span class="sxs-lookup"><span data-stu-id="a4c77-415">Complying with all applicable copyright laws is the responsibility of the user.</span></span> <span data-ttu-id="a4c77-416">未经 Microsoft Corporation 明确的书面许可，不得出于任何目的或以任何形式或任何手段（电子、机械、影印、记录或其他方法）复制本文档的任何部分，或者将其存储或引入检索系统，或者将其进行传播。受版权法保护的权利不受此限制。</span><span class="sxs-lookup"><span data-stu-id="a4c77-416">Without limiting the rights under copyright, no part of this document may be reproduced, stored in or introduced into a retrieval system, or transmitted in any form or by any means (electronic, mechanical, photocopying, recording, or otherwise), or for any purpose, without the express written permission of Microsoft Corporation.</span></span>

<span data-ttu-id="a4c77-417">对于本文档中的主题，Microsoft 可能具有专利、专利申请、商标、版权或其他知识产权。</span><span class="sxs-lookup"><span data-stu-id="a4c77-417">Microsoft may have patents, patent applications, trademarks, copyrights, or other intellectual property rights covering subject matter in this document.</span></span> <span data-ttu-id="a4c77-418">除非 Microsoft 的任何书面许可协议明确提出，否则，本文档的提供并不表示 Microsoft 已将这些专利、商标、版权或其他知识产权的任何许可权限授予您。</span><span class="sxs-lookup"><span data-stu-id="a4c77-418">Except as expressly provided in any written license agreement from Microsoft, the furnishing of this document does not give you any license to these patents, trademarks, copyrights, or other intellectual property.</span></span>

<span data-ttu-id="a4c77-419">除非另有说明，否则本示例中描述的公司、组织、产品、域名、电子邮件地址、徽标、人物、地点和事件均属虚构，与任何真实的公司、组织、产品、域名、电子邮件关联应推断地址、徽标、人物、地点或事件。</span><span class="sxs-lookup"><span data-stu-id="a4c77-419">Unless otherwise noted, the example companies, organizations, products, domain names, email addresses, logos, people, places and events depicted herein are fictitious, and no association with any real company, organization, product, domain name, email address, logo, person, place or event is intended or should be inferred.</span></span>

<span data-ttu-id="a4c77-420">© 2010 Microsoft Corporation.</span><span class="sxs-lookup"><span data-stu-id="a4c77-420">© 2010 Microsoft Corporation.</span></span> <span data-ttu-id="a4c77-421">保留所有权利。</span><span class="sxs-lookup"><span data-stu-id="a4c77-421">All rights reserved.</span></span>

<span data-ttu-id="a4c77-422">Microsoft 和 Windows 是 Microsoft Corporation 在美国和/或其他国家/地区的注册商标或商标。</span><span class="sxs-lookup"><span data-stu-id="a4c77-422">Microsoft and Windows are either registered trademarks or trademarks of Microsoft Corporation in the United States and/or other countries.</span></span>

<span data-ttu-id="a4c77-423">本文档所涉及的真实公司和产品名称可能是其各自所有者的商标。</span><span class="sxs-lookup"><span data-stu-id="a4c77-423">The names of actual companies and products mentioned herein may be the trademarks of their respective owners.</span></span>
