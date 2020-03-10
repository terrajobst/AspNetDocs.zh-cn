---
uid: mvc/overview/older-versions/aspnet-mvc-4-mobile-features
title: ASP.NET MVC 4 移动功能 |Microsoft Docs
author: Rick-Anderson
description: 现在，在 Azure 网站上部署 ASP.NET MVC 5 移动 Web 应用程序的代码示例中提供了本教程的 MVC 5 版本。
ms.author: riande
ms.date: 08/15/2012
ms.assetid: 27dc4fc8-1b51-43b0-933f-fc1b52476523
msc.legacyurl: /mvc/overview/older-versions/aspnet-mvc-4-mobile-features
msc.type: authoredcontent
ms.openlocfilehash: 9716def069ca9f7115af32e16381f41bd4d13342
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78468428"
---
# <a name="aspnet-mvc-4-mobile-features"></a><span data-ttu-id="a21a9-103">ASP.NET MVC 4 移动功能</span><span class="sxs-lookup"><span data-stu-id="a21a9-103">ASP.NET MVC 4 Mobile Features</span></span>

<span data-ttu-id="a21a9-104">作者： [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="a21a9-104">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

> <span data-ttu-id="a21a9-105">现在，在[Azure 网站上部署 ASP.NET mvc 5 移动 Web 应用程序](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/)的代码示例中提供了本教程的 MVC 5 版本。</span><span class="sxs-lookup"><span data-stu-id="a21a9-105">There is now an MVC 5 version of this tutorial with code samples at [Deploy an ASP.NET MVC 5 Mobile Web Application on Azure Web Sites](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/).</span></span>

<span data-ttu-id="a21a9-106">本教程将指导你了解如何使用 ASP.NET MVC 4 Web 应用程序中的移动功能。</span><span class="sxs-lookup"><span data-stu-id="a21a9-106">This tutorial will teach you the basics of how to work with mobile features in an ASP.NET MVC 4 Web application.</span></span> <span data-ttu-id="a21a9-107">对于本教程，可以使用[Visual Studio Express 2012](https://www.microsoft.com/visualstudio/11/products/express)或 Visual web Developer 2010 Express Service Pack 1 （&quot;Visual web DEVELOPER 或 VWD&quot;）。</span><span class="sxs-lookup"><span data-stu-id="a21a9-107">For this tutorial, you can use [Visual Studio Express 2012](https://www.microsoft.com/visualstudio/11/products/express) or Visual Web Developer 2010 Express Service Pack 1 (&quot;Visual Web Developer or VWD&quot;).</span></span> <span data-ttu-id="a21a9-108">你可以使用 Visual Studio 的专业版（如果已有）。</span><span class="sxs-lookup"><span data-stu-id="a21a9-108">You can use the professional version of Visual Studio if you already have that.</span></span>

<span data-ttu-id="a21a9-109">在开始之前，请确保已安装下列必备组件。</span><span class="sxs-lookup"><span data-stu-id="a21a9-109">Before you start, make sure you've installed the prerequisites listed below.</span></span>

- <span data-ttu-id="a21a9-110">[Visual Studio Express 2012](https://www.microsoft.com/visualstudio/11/products/express) （推荐）或 Visual Studio Web DEVELOPER Express SP1。</span><span class="sxs-lookup"><span data-stu-id="a21a9-110">[Visual Studio Express 2012](https://www.microsoft.com/visualstudio/11/products/express) (recommended) or Visual Studio Web Developer Express SP1.</span></span> <span data-ttu-id="a21a9-111">Visual Studio 2012 包含 ASP.NET MVC 4。</span><span class="sxs-lookup"><span data-stu-id="a21a9-111">Visual Studio 2012 contains ASP.NET MVC 4.</span></span> <span data-ttu-id="a21a9-112">如果使用的是 Visual Web Developer 2010，则必须安装[ASP.NET MVC 4](https://go.microsoft.com/fwlink/?LinkId=243392)。</span><span class="sxs-lookup"><span data-stu-id="a21a9-112">If you are using Visual Web Developer 2010, you must install [ASP.NET MVC 4](https://go.microsoft.com/fwlink/?LinkId=243392).</span></span>

<span data-ttu-id="a21a9-113">还需要安装移动浏览器模拟器。</span><span class="sxs-lookup"><span data-stu-id="a21a9-113">You will also need a mobile browser emulator.</span></span> <span data-ttu-id="a21a9-114">以下版本均可：</span><span class="sxs-lookup"><span data-stu-id="a21a9-114">Any of the following will work:</span></span>

- <span data-ttu-id="a21a9-115">[Windows 7 Phone 仿真程序](https://msdn.microsoft.com/library/ff402563(VS.92).aspx)。</span><span class="sxs-lookup"><span data-stu-id="a21a9-115">[Windows 7 Phone Emulator](https://msdn.microsoft.com/library/ff402563(VS.92).aspx).</span></span> <span data-ttu-id="a21a9-116">（本教程的大部分屏幕快照中都使用这种模拟器。）</span><span class="sxs-lookup"><span data-stu-id="a21a9-116">(This is the emulator that's used in most of the screen shots in this tutorial.)</span></span>
- <span data-ttu-id="a21a9-117">更改用户代理字符串以模拟 iPhone。</span><span class="sxs-lookup"><span data-stu-id="a21a9-117">Change the user agent string to emulate an iPhone.</span></span> <span data-ttu-id="a21a9-118">请参阅[此](http://www.howtogeek.com/113439/how-to-change-your-browsers-user-agent-without-installing-any-extensions/)博客文章。</span><span class="sxs-lookup"><span data-stu-id="a21a9-118">See [this](http://www.howtogeek.com/113439/how-to-change-your-browsers-user-agent-without-installing-any-extensions/) blog entry.</span></span>
- [<span data-ttu-id="a21a9-119">Opera 移动模拟器</span><span class="sxs-lookup"><span data-stu-id="a21a9-119">Opera Mobile Emulator</span></span>](http://www.opera.com/developer/tools/mobile/)
- <span data-ttu-id="a21a9-120">将用户代理设置为 iPhone 的[Apple Safari](http://www.apple.com/safari/download/) 。</span><span class="sxs-lookup"><span data-stu-id="a21a9-120">[Apple Safari](http://www.apple.com/safari/download/) with the user agent set to iPhone.</span></span> <span data-ttu-id="a21a9-121">有关如何将 Safari 中的用户代理设置为 "iPhone" 的说明，请参阅[如何让 Safari 假设它](http://www.davidalison.com/2008/05/how-to-let-safari-pretend-its-ie.html)在 David Alison 的博客上。</span><span class="sxs-lookup"><span data-stu-id="a21a9-121">For instructions on how to set the user agent in Safari to "iPhone", see [How to let Safari pretend it's IE](http://www.davidalison.com/2008/05/how-to-let-safari-pretend-its-ie.html) on David Alison's blog.</span></span>

<span data-ttu-id="a21a9-122">本主题可以附带包含具有 C# 源代码的 Visual Studio：</span><span class="sxs-lookup"><span data-stu-id="a21a9-122">Visual Studio projects with C# source code are available to accompany this topic:</span></span>

- [<span data-ttu-id="a21a9-123">初学者项目下载</span><span class="sxs-lookup"><span data-stu-id="a21a9-123">Starter project download</span></span>](https://go.microsoft.com/fwlink/?linkid=228307&amp;clcid=0x409)
- [<span data-ttu-id="a21a9-124">已完成项目下载</span><span class="sxs-lookup"><span data-stu-id="a21a9-124">Completed project download</span></span>](https://go.microsoft.com/fwlink/?linkid=228306&amp;clcid=0x409)

### <a name="what-youll-build"></a><span data-ttu-id="a21a9-125">你将生成</span><span class="sxs-lookup"><span data-stu-id="a21a9-125">What You'll Build</span></span>

<span data-ttu-id="a21a9-126">在本教程中，你将向[初学者项目](https://go.microsoft.com/fwlink/?LinkId=228307)中提供的简单会议列表应用程序添加移动功能。</span><span class="sxs-lookup"><span data-stu-id="a21a9-126">For this tutorial, you'll add mobile features to the simple conference-listing application that's provided in the [starter project](https://go.microsoft.com/fwlink/?LinkId=228307).</span></span> <span data-ttu-id="a21a9-127">以下屏幕截图显示了已完成的应用程序的 "标记" 页，如[Windows 7 Phone 模拟器](https://msdn.microsoft.com/library/ff402563(VS.92).aspx)中所示。</span><span class="sxs-lookup"><span data-stu-id="a21a9-127">The following screenshot shows the tags page of the completed application as seen in the [Windows 7 Phone Emulator](https://msdn.microsoft.com/library/ff402563(VS.92).aspx).</span></span> <span data-ttu-id="a21a9-128">请参阅[Windows Phone 模拟器的键盘映射](https://msdn.microsoft.com/library/ff754352(v=vs.92).aspx)，简化键盘输入。</span><span class="sxs-lookup"><span data-stu-id="a21a9-128">See [Keyboard Mapping for Windows Phone Emulator](https://msdn.microsoft.com/library/ff754352(v=vs.92).aspx) to simplify keyboard input.</span></span>

<span data-ttu-id="a21a9-129">[![p1_Tags_CompletedProj](aspnet-mvc-4-mobile-features/_static/image2.png)](aspnet-mvc-4-mobile-features/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="a21a9-129">[![p1_Tags_CompletedProj](aspnet-mvc-4-mobile-features/_static/image2.png)](aspnet-mvc-4-mobile-features/_static/image1.png)</span></span>

<span data-ttu-id="a21a9-130">可以通过设置[用户代理字符串](http://www.howtogeek.com/113439/how-to-change-your-browsers-user-agent-without-installing-any-extensions/)，使用 Internet Explorer 版本9或10、FireFox 或 Chrome 来开发移动应用程序。</span><span class="sxs-lookup"><span data-stu-id="a21a9-130">You can use Internet Explorer version 9 or 10, FireFox or Chrome to develop your mobile application by setting the [user agent string](http://www.howtogeek.com/113439/how-to-change-your-browsers-user-agent-without-installing-any-extensions/).</span></span> <span data-ttu-id="a21a9-131">下图显示了使用 Internet Explorer 模拟 iPhone 的已完成教程。</span><span class="sxs-lookup"><span data-stu-id="a21a9-131">The following image shows the completed tutorial using Internet Explorer emulating an iPhone.</span></span> <span data-ttu-id="a21a9-132">可以使用 Internet Explorer F-12 开发人员工具和[Fiddler 工具](http://www.fiddler2.com/fiddler2/)来帮助调试应用程序。</span><span class="sxs-lookup"><span data-stu-id="a21a9-132">You can use the Internet Explorer F-12 developer tools and the [Fiddler tool](http://www.fiddler2.com/fiddler2/) to help debug your application.</span></span>

![](aspnet-mvc-4-mobile-features/_static/image3.png)

### <a name="skills-youll-learn"></a><span data-ttu-id="a21a9-133">将要学到的技能</span><span class="sxs-lookup"><span data-stu-id="a21a9-133">Skills You'll Learn</span></span>

<span data-ttu-id="a21a9-134">学习内容：</span><span class="sxs-lookup"><span data-stu-id="a21a9-134">Here's what you'll learn:</span></span>

- <span data-ttu-id="a21a9-135">ASP.NET MVC 4 模板如何使用 HTML5 `viewport` 属性和自适应呈现来改善移动设备上的显示效果。</span><span class="sxs-lookup"><span data-stu-id="a21a9-135">How the ASP.NET MVC 4 templates use the HTML5 `viewport` attribute and adaptive rendering to improve display on mobile devices.</span></span>
- <span data-ttu-id="a21a9-136">如何创建移动特定视图。</span><span class="sxs-lookup"><span data-stu-id="a21a9-136">How to create mobile-specific views.</span></span>
- <span data-ttu-id="a21a9-137">如何创建视图切换器，以便用户能够在应用程序的移动视图与桌面视图间切换。</span><span class="sxs-lookup"><span data-stu-id="a21a9-137">How to create a view switcher that lets users toggle between a mobile view and a desktop view of the application.</span></span>

### <a name="getting-started"></a><span data-ttu-id="a21a9-138">入门</span><span class="sxs-lookup"><span data-stu-id="a21a9-138">Getting Started</span></span>

<span data-ttu-id="a21a9-139">使用以下链接下载初学者项目的会议列表应用程序：[下载](https://go.microsoft.com/fwlink/?LinkId=228307)。</span><span class="sxs-lookup"><span data-stu-id="a21a9-139">Download the conference-listing application for the starter project using the following link: [Download](https://go.microsoft.com/fwlink/?LinkId=228307).</span></span> <span data-ttu-id="a21a9-140">然后在 Windows 资源管理器中，右键单击*mvcmobile.sln*文件，然后选择 "**属性**"。</span><span class="sxs-lookup"><span data-stu-id="a21a9-140">Then in Windows Explorer, right-click the *MvcMobile.zip* file and choose **Properties**.</span></span> <span data-ttu-id="a21a9-141">在 " **Mvcmobile.sln 属性**" 对话框中，选择 "**取消阻止**" 按钮。</span><span class="sxs-lookup"><span data-stu-id="a21a9-141">In the **MvcMobile.zip Properties** dialog box, choose the **Unblock** button.</span></span> <span data-ttu-id="a21a9-142">（取消阻止后，尝试使用从 Web 下载的 *.zip* 文件时，不再显示安全警告。）</span><span class="sxs-lookup"><span data-stu-id="a21a9-142">(Unblocking prevents a security warning that occurs when you try to use a *.zip* file that you've downloaded from the web.)</span></span>

![p1_unBlock](aspnet-mvc-4-mobile-features/_static/image4.png)

<span data-ttu-id="a21a9-144">右键单击 " *mvcmobile.sln* " 文件，然后选择 "**全部提取**" 来解压缩该文件。</span><span class="sxs-lookup"><span data-stu-id="a21a9-144">Right-click the *MvcMobile.zip* file and select **Extract All** to unzip the file.</span></span> <span data-ttu-id="a21a9-145">在 Visual Studio 中，打开*mvcmobile.sln*文件。</span><span class="sxs-lookup"><span data-stu-id="a21a9-145">In Visual Studio, open the *MvcMobile.sln* file.</span></span>

<span data-ttu-id="a21a9-146">按 Ctrl + F5 运行该应用程序，它将在桌面浏览器中显示。</span><span class="sxs-lookup"><span data-stu-id="a21a9-146">Press CTRL+F5 to run the application, which will display it in your desktop browser.</span></span> <span data-ttu-id="a21a9-147">启动移动浏览器模拟器，将会议应用程序的 URL 复制到模拟器，然后单击 "**按标记浏览**" 链接。</span><span class="sxs-lookup"><span data-stu-id="a21a9-147">Start your mobile browser emulator, copy the URL for the conference application into the emulator, and then click the **Browse by tag** link.</span></span> <span data-ttu-id="a21a9-148">如果您使用的是 Windows Phone Emulator，则在 URL 栏中单击并按“暂停”键来访问键盘。</span><span class="sxs-lookup"><span data-stu-id="a21a9-148">If you are using the Windows Phone Emulator, click in the URL bar and press the Pause key to get keyboard access.</span></span> <span data-ttu-id="a21a9-149">下图显示了*AllTags*视图（选择 "**按标记浏览" 时**）。</span><span class="sxs-lookup"><span data-stu-id="a21a9-149">The image below shows the *AllTags* view (from choosing **Browse by tag**).</span></span>

<span data-ttu-id="a21a9-150">[![p1_browseTag](aspnet-mvc-4-mobile-features/_static/image6.png)](aspnet-mvc-4-mobile-features/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="a21a9-150">[![p1_browseTag](aspnet-mvc-4-mobile-features/_static/image6.png)](aspnet-mvc-4-mobile-features/_static/image5.png)</span></span>

<span data-ttu-id="a21a9-151">显示内容在移动设备上一目了然。</span><span class="sxs-lookup"><span data-stu-id="a21a9-151">The display is very readable on a mobile device.</span></span> <span data-ttu-id="a21a9-152">选择 ASP.NET 链接。</span><span class="sxs-lookup"><span data-stu-id="a21a9-152">Choose the ASP.NET link.</span></span>

<span data-ttu-id="a21a9-153">[![p1_tagged_ASPNET](aspnet-mvc-4-mobile-features/_static/image8.png)](aspnet-mvc-4-mobile-features/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="a21a9-153">[![p1_tagged_ASPNET](aspnet-mvc-4-mobile-features/_static/image8.png)](aspnet-mvc-4-mobile-features/_static/image7.png)</span></span>

<span data-ttu-id="a21a9-154">ASP.NET 标签视图显示非常混乱。</span><span class="sxs-lookup"><span data-stu-id="a21a9-154">The ASP.NET tag view is very cluttered.</span></span> <span data-ttu-id="a21a9-155">例如，"**日期**" 列很难阅读。</span><span class="sxs-lookup"><span data-stu-id="a21a9-155">For example, the **Date** column is very difficult to read.</span></span> <span data-ttu-id="a21a9-156">稍后在本教程中，你将创建一个*AllTags*视图的版本，该版本专门用于移动浏览器并使显示可读。</span><span class="sxs-lookup"><span data-stu-id="a21a9-156">Later in the tutorial you'll create a version of the *AllTags* view that's specifically for mobile browsers and that will make the display readable.</span></span>

<span data-ttu-id="a21a9-157">注意：目前移动缓存引擎中存在错误。</span><span class="sxs-lookup"><span data-stu-id="a21a9-157">Note: Currently a bug exists in the mobile caching engine.</span></span> <span data-ttu-id="a21a9-158">对于生产应用程序，必须安装[Fixed DisplayModes](http://nuget.org/packages/Microsoft.AspNet.Mvc.FixedDisplayModes) nugget 包。</span><span class="sxs-lookup"><span data-stu-id="a21a9-158">For production applications, you must install the [Fixed DisplayModes](http://nuget.org/packages/Microsoft.AspNet.Mvc.FixedDisplayModes) nugget package.</span></span> <span data-ttu-id="a21a9-159">有关修补程序的详细信息，请参阅[ASP.NET MVC 4 移动缓存 Bug](https://blogs.msdn.com/b/rickandy/archive/2012/09/17/asp-net-mvc-4-mobile-caching-bug-fixed.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="a21a9-159">See [ASP.NET MVC 4 Mobile Caching Bug Fixed](https://blogs.msdn.com/b/rickandy/archive/2012/09/17/asp-net-mvc-4-mobile-caching-bug-fixed.aspx) for details on the fix.</span></span>

## <a name="css-media-queries"></a><span data-ttu-id="a21a9-160">CSS 媒体查询</span><span class="sxs-lookup"><span data-stu-id="a21a9-160">CSS Media Queries</span></span>

<span data-ttu-id="a21a9-161">[Css 媒体查询](http://www.w3.org/TR/css3-mediaqueries/)是媒体类型的 css 扩展。</span><span class="sxs-lookup"><span data-stu-id="a21a9-161">[CSS media queries](http://www.w3.org/TR/css3-mediaqueries/) are an extension to CSS for media types.</span></span> <span data-ttu-id="a21a9-162">它们允许您创建规则来覆盖特定浏览器（用户代理）的默认 CSS 规则。</span><span class="sxs-lookup"><span data-stu-id="a21a9-162">They allow you to create rules that override the default CSS rules for specific browsers (user agents).</span></span> <span data-ttu-id="a21a9-163">面向移动浏览器的 CSS 的通用规则是定义最大屏幕大小。</span><span class="sxs-lookup"><span data-stu-id="a21a9-163">A common rule for CSS that targets mobile browsers is defining the maximum screen size.</span></span> <span data-ttu-id="a21a9-164">创建新的 ASP.NET MVC 4 Internet 项目时创建的*Content\Site.css*文件包含以下媒体查询：</span><span class="sxs-lookup"><span data-stu-id="a21a9-164">The *Content\Site.css* file that's created when you create a new ASP.NET MVC 4 Internet project contains the following media query:</span></span>

[!code-css[Main](aspnet-mvc-4-mobile-features/samples/sample1.css)]

<span data-ttu-id="a21a9-165">如果浏览器窗口的宽度为850像素或更小，则它将使用此媒体块内的 CSS 规则。</span><span class="sxs-lookup"><span data-stu-id="a21a9-165">If the browser window is 850 pixels wide or less, it will use the CSS rules inside this media block.</span></span> <span data-ttu-id="a21a9-166">您可以使用如下所示的 CSS 媒体查询，在小型浏览器（如移动浏览器）上更好地显示 HTML 内容，而不是为桌面浏览器的更大显示而设计的默认 CSS 规则。</span><span class="sxs-lookup"><span data-stu-id="a21a9-166">You can use CSS media queries like this to provide a better display of HTML content on small browsers (like mobile browsers) than the default CSS rules that are designed for the wider displays of desktop browsers.</span></span>

## <a name="the-viewport-meta-tag"></a><span data-ttu-id="a21a9-167">视区元标记</span><span class="sxs-lookup"><span data-stu-id="a21a9-167">The Viewport Meta Tag</span></span>

<span data-ttu-id="a21a9-168">大多数移动浏览器定义一个虚拟浏览器窗口宽度（*视区*），该宽度远远大于移动设备的实际宽度。</span><span class="sxs-lookup"><span data-stu-id="a21a9-168">Most mobile browsers define a virtual browser window width (the *viewport*) that's much larger than the actual width of the mobile device.</span></span> <span data-ttu-id="a21a9-169">这允许移动浏览器在虚拟显示中适应整个网页。</span><span class="sxs-lookup"><span data-stu-id="a21a9-169">This allows mobile browsers to fit the entire web page inside the virtual display.</span></span> <span data-ttu-id="a21a9-170">然后，用户可以放大感兴趣的内容。</span><span class="sxs-lookup"><span data-stu-id="a21a9-170">Users can then zoom in on interesting content.</span></span> <span data-ttu-id="a21a9-171">但是，如果将视区宽度设置为实际设备宽度，则不需要缩放，因为内容适合移动浏览器。</span><span class="sxs-lookup"><span data-stu-id="a21a9-171">However, if you set the viewport width to the actual device width, no zooming is required, because the content fits in the mobile browser.</span></span>

<span data-ttu-id="a21a9-172">ASP.NET MVC 4 布局文件中的视区 `<meta>` 标记将视区设置为设备宽度。</span><span class="sxs-lookup"><span data-stu-id="a21a9-172">The viewport `<meta>` tag in the ASP.NET MVC 4 layout file sets the viewport to the device width.</span></span> <span data-ttu-id="a21a9-173">以下行显示 ASP.NET MVC 4 布局文件中 `<meta>` 标记的视区。</span><span class="sxs-lookup"><span data-stu-id="a21a9-173">The following line shows the viewport `<meta>` tag in the ASP.NET MVC 4 layout file.</span></span>

[!code-html[Main](aspnet-mvc-4-mobile-features/samples/sample2.html)]

## <a name="examining-the-effect-of-css-media-queries-and-the-viewport-meta-tag"></a><span data-ttu-id="a21a9-174">检查 CSS 媒体查询和视区 Meta 标记的影响</span><span class="sxs-lookup"><span data-stu-id="a21a9-174">Examining the Effect of CSS Media Queries and the Viewport Meta Tag</span></span>

<span data-ttu-id="a21a9-175">在编辑器中打开 " *Views\Shared"\\_Layout* ，并注释掉视区 `<meta>` 标记。</span><span class="sxs-lookup"><span data-stu-id="a21a9-175">Open the *Views\Shared\\_Layout.cshtml* file in the editor and comment out the viewport `<meta>` tag.</span></span> <span data-ttu-id="a21a9-176">下面的标记显示了注释掉的行。</span><span class="sxs-lookup"><span data-stu-id="a21a9-176">The following markup shows the commented-out line.</span></span>

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample3.cshtml)]

<span data-ttu-id="a21a9-177">在编辑器中打开*MvcMobile\Content\Site.css*文件，并将 "媒体" 查询中的最大宽度更改为零像素。</span><span class="sxs-lookup"><span data-stu-id="a21a9-177">Open the *MvcMobile\Content\Site.css* file in the editor and change the maximum width in the media query to zero pixels.</span></span> <span data-ttu-id="a21a9-178">这会阻止在移动浏览器中使用 CSS 规则。</span><span class="sxs-lookup"><span data-stu-id="a21a9-178">This will prevent the CSS rules from being used in mobile browsers.</span></span> <span data-ttu-id="a21a9-179">以下行显示了修改后的媒体查询：</span><span class="sxs-lookup"><span data-stu-id="a21a9-179">The following line shows the modified media query:</span></span>

[!code-css[Main](aspnet-mvc-4-mobile-features/samples/sample4.css)]

<span data-ttu-id="a21a9-180">保存更改并在移动浏览器模拟器中浏览到会议应用程序。</span><span class="sxs-lookup"><span data-stu-id="a21a9-180">Save your changes and browse to the Conference application in a mobile browser emulator.</span></span> <span data-ttu-id="a21a9-181">下图中的小文本是删除视区 `<meta>` 标记的结果。</span><span class="sxs-lookup"><span data-stu-id="a21a9-181">The tiny text in the following image is the result of removing the viewport `<meta>` tag.</span></span> <span data-ttu-id="a21a9-182">如果没有视区 `<meta>` 标记，浏览器将缩小为默认视区宽度（对于大多数移动浏览器，则为850像素或更宽）。</span><span class="sxs-lookup"><span data-stu-id="a21a9-182">With no viewport `<meta>` tag, the browser is zooming out to the default viewport width (850 pixels or wider for most mobile browsers.)</span></span>

<span data-ttu-id="a21a9-183">[![p1_noViewPort](aspnet-mvc-4-mobile-features/_static/image10.png)](aspnet-mvc-4-mobile-features/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="a21a9-183">[![p1_noViewPort](aspnet-mvc-4-mobile-features/_static/image10.png)](aspnet-mvc-4-mobile-features/_static/image9.png)</span></span>

<span data-ttu-id="a21a9-184">撤消所做的更改：在布局文件中取消注释视区 `<meta>` 标记，并在*web.config*文件中将媒体查询还原为850像素。</span><span class="sxs-lookup"><span data-stu-id="a21a9-184">Undo your changes — uncomment the viewport `<meta>` tag in the layout file and restore the media query to 850 pixels in the *Site.css* file.</span></span> <span data-ttu-id="a21a9-185">保存你所做的更改并刷新移动浏览器，以验证移动友好的显示是否已还原。</span><span class="sxs-lookup"><span data-stu-id="a21a9-185">Save your changes and refresh the mobile browser to verify that the mobile-friendly display has been restored.</span></span>

<span data-ttu-id="a21a9-186">视区 `<meta>` 标记和 CSS 媒体查询并不特定于 ASP.NET MVC 4，你可以在任何 web 应用程序中利用这些功能。</span><span class="sxs-lookup"><span data-stu-id="a21a9-186">The viewport `<meta>` tag and the CSS media query are not specific to ASP.NET MVC 4, and you can take advantage of these features in any web application.</span></span> <span data-ttu-id="a21a9-187">但现在它们内置于创建新的 ASP.NET MVC 4 项目时生成的文件中。</span><span class="sxs-lookup"><span data-stu-id="a21a9-187">But they are now built into the files that are generated when you create a new ASP.NET MVC 4 project.</span></span>

<span data-ttu-id="a21a9-188">有关视区 `<meta>` 标记的详细信息，请参阅[第二个视区的 tale](http://www.quirksmode.org/mobile/viewports2.html)。</span><span class="sxs-lookup"><span data-stu-id="a21a9-188">For more information about the viewport `<meta>` tag, see [A tale of two viewports — part two](http://www.quirksmode.org/mobile/viewports2.html).</span></span>

<span data-ttu-id="a21a9-189">在下一部分中，你将了解如何提供移动浏览器特定的视图。</span><span class="sxs-lookup"><span data-stu-id="a21a9-189">In the next section you'll see how to provide mobile-browser specific views.</span></span>

## <a name="overriding-views-layouts-and-partial-views"></a><span data-ttu-id="a21a9-190">重写视图、布局和分部视图</span><span class="sxs-lookup"><span data-stu-id="a21a9-190">Overriding Views, Layouts, and Partial Views</span></span>

<span data-ttu-id="a21a9-191">ASP.NET MVC 4 中的一个重要新功能是一种允许您针对常规移动浏览器、单个移动浏览器或任何特定浏览器重写任何视图（包括布局和分部视图）的简单机制。</span><span class="sxs-lookup"><span data-stu-id="a21a9-191">A significant new feature in ASP.NET MVC 4 is a simple mechanism that lets you override any view (including layouts and partial views) for mobile browsers in general, for an individual mobile browser, or for any specific browser.</span></span> <span data-ttu-id="a21a9-192">要提供移动特定的视图，可以复制视图文件并在文件名中添加 *.Mobile*。</span><span class="sxs-lookup"><span data-stu-id="a21a9-192">To provide a mobile-specific view, you can copy a view file and add *.Mobile* to the file name.</span></span> <span data-ttu-id="a21a9-193">例如，若要创建移动*索引*视图，请将*Views\Home\Index.cshtml*复制到*Views\Home\Index.Mobile.cshtml*。</span><span class="sxs-lookup"><span data-stu-id="a21a9-193">For example, to create a mobile *Index* view, copy *Views\Home\Index.cshtml* to *Views\Home\Index.Mobile.cshtml*.</span></span>

<span data-ttu-id="a21a9-194">在本节中，你将创建一个移动特定布局文件。</span><span class="sxs-lookup"><span data-stu-id="a21a9-194">In this section, you'll create a mobile-specific layout file.</span></span>

<span data-ttu-id="a21a9-195">若要开始，请将*Views\Shared\\_Layout*中复制到*Views\Shared\\_Layout*。</span><span class="sxs-lookup"><span data-stu-id="a21a9-195">To start, copy *Views\Shared\\_Layout.cshtml* to *Views\Shared\\_Layout.Mobile.cshtml*.</span></span> <span data-ttu-id="a21a9-196">打开 *\_* **MVC4** ，并将标题从 "会议" 更改为 "**会议（移动）** "。</span><span class="sxs-lookup"><span data-stu-id="a21a9-196">Open *\_Layout.Mobile.cshtml* and change the title from **MVC4 Conference** to **Conference (Mobile)**.</span></span>

<span data-ttu-id="a21a9-197">在每个 `Html.ActionLink` 调用中，删除每*个链接中*的 "浏览者"。</span><span class="sxs-lookup"><span data-stu-id="a21a9-197">In each `Html.ActionLink` call, remove "Browse by" in each link *ActionLink*.</span></span> <span data-ttu-id="a21a9-198">以下代码显示已完成的移动布局文件主体部分。</span><span class="sxs-lookup"><span data-stu-id="a21a9-198">The following code shows the completed body section of the mobile layout file.</span></span>

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample5.cshtml)]

<span data-ttu-id="a21a9-199">将*Views\Home\AllTags.cshtml*文件复制到*Views\Home\AllTags.Mobile.cshtml*。</span><span class="sxs-lookup"><span data-stu-id="a21a9-199">Copy the *Views\Home\AllTags.cshtml* file to *Views\Home\AllTags.Mobile.cshtml*.</span></span> <span data-ttu-id="a21a9-200">打开新文件，将 `<h2>` 元素从 "Tags" 更改为 "Tags （M）"：</span><span class="sxs-lookup"><span data-stu-id="a21a9-200">Open the new file and change the `<h2>` element from "Tags" to "Tags (M)":</span></span>

[!code-html[Main](aspnet-mvc-4-mobile-features/samples/sample6.html)]

<span data-ttu-id="a21a9-201">使用桌面浏览器和移动浏览器模拟器浏览到标签页。</span><span class="sxs-lookup"><span data-stu-id="a21a9-201">Browse to the tags page using a desktop browser and using mobile browser emulator.</span></span> <span data-ttu-id="a21a9-202">移动浏览器模拟器显示您所做的两处改动。</span><span class="sxs-lookup"><span data-stu-id="a21a9-202">The mobile browser emulator shows the two changes you made.</span></span>

<span data-ttu-id="a21a9-203">[![p2m_layoutTags mobile](aspnet-mvc-4-mobile-features/_static/image12.png)](aspnet-mvc-4-mobile-features/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="a21a9-203">[![p2m_layoutTags.mobile](aspnet-mvc-4-mobile-features/_static/image12.png)](aspnet-mvc-4-mobile-features/_static/image11.png)</span></span>

<span data-ttu-id="a21a9-204">与此相反，桌面显示没有变化。</span><span class="sxs-lookup"><span data-stu-id="a21a9-204">In contrast, the desktop display has not changed.</span></span>

<span data-ttu-id="a21a9-205">[![p2_layoutTagsDesktop](aspnet-mvc-4-mobile-features/_static/image14.png)](aspnet-mvc-4-mobile-features/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="a21a9-205">[![p2_layoutTagsDesktop](aspnet-mvc-4-mobile-features/_static/image14.png)](aspnet-mvc-4-mobile-features/_static/image13.png)</span></span>

## <a name="browser-specific-views"></a><span data-ttu-id="a21a9-206">特定于浏览器的视图</span><span class="sxs-lookup"><span data-stu-id="a21a9-206">Browser-Specific Views</span></span>

<span data-ttu-id="a21a9-207">除了移动特定和桌面特定的视图以外，你还可以为单个浏览器创建视图。</span><span class="sxs-lookup"><span data-stu-id="a21a9-207">In addition to mobile-specific and desktop-specific views, you can create views for an individual browser.</span></span> <span data-ttu-id="a21a9-208">例如，可以创建专门针对 iPhone 浏览器的视图。</span><span class="sxs-lookup"><span data-stu-id="a21a9-208">For example, you can create views that are specifically for the iPhone browser.</span></span> <span data-ttu-id="a21a9-209">在本节中，将为 iPhone 浏览器和 iPhone 版本的 *AllTags* 视图创建布局。</span><span class="sxs-lookup"><span data-stu-id="a21a9-209">In this section, you'll create a layout for the iPhone browser and an iPhone version of the *AllTags* view.</span></span>

<span data-ttu-id="a21a9-210">打开*global.asax*文件，并将以下代码添加到 `Application_Start` 方法。</span><span class="sxs-lookup"><span data-stu-id="a21a9-210">Open the *Global.asax* file and add the following code to the `Application_Start` method.</span></span>

[!code-csharp[Main](aspnet-mvc-4-mobile-features/samples/sample7.cs)]

<span data-ttu-id="a21a9-211">此代码定义要与每个传入请求匹配的名为“iPhone”的新显示模式。</span><span class="sxs-lookup"><span data-stu-id="a21a9-211">This code defines a new display mode named "iPhone" that will be matched against each incoming request.</span></span> <span data-ttu-id="a21a9-212">如果传入请求与定义的条件（即，如果用户代理包含字符串“iPhone”）匹配，则 ASP.NET MVC 将查找名称包含“iPhone”后缀的视图。</span><span class="sxs-lookup"><span data-stu-id="a21a9-212">If the incoming request matches the condition you defined (that is, if the user agent contains the string "iPhone"), ASP.NET MVC will look for views whose name contains the "iPhone" suffix.</span></span>

<span data-ttu-id="a21a9-213">在代码中右键单击 `DefaultDisplayMode`，选择“解析”，并选择 `using System.Web.WebPages;`。</span><span class="sxs-lookup"><span data-stu-id="a21a9-213">In the code, right-click `DefaultDisplayMode`, choose **Resolve**, and then choose `using System.Web.WebPages;`.</span></span> <span data-ttu-id="a21a9-214">这会向 `System.Web.WebPages` 命名空间添加引用，该命名空间中定义了 `DisplayModes` 和 `DefaultDisplayMode` 类型。</span><span class="sxs-lookup"><span data-stu-id="a21a9-214">This adds a reference to the `System.Web.WebPages` namespace, which is where the `DisplayModes` and `DefaultDisplayMode` types are defined.</span></span>

<span data-ttu-id="a21a9-215">[![p2_resolve](aspnet-mvc-4-mobile-features/_static/image16.png)](aspnet-mvc-4-mobile-features/_static/image15.png)</span><span class="sxs-lookup"><span data-stu-id="a21a9-215">[![p2_resolve](aspnet-mvc-4-mobile-features/_static/image16.png)](aspnet-mvc-4-mobile-features/_static/image15.png)</span></span>

<span data-ttu-id="a21a9-216">或者，也可以简单地将以下行手动添加到文件的 `using` 章节。</span><span class="sxs-lookup"><span data-stu-id="a21a9-216">Alternatively, you can just manually add the following line to the `using` section of the file.</span></span>

[!code-csharp[Main](aspnet-mvc-4-mobile-features/samples/sample8.cs)]

<span data-ttu-id="a21a9-217">*Global.asax*文件的完整内容如下所示。</span><span class="sxs-lookup"><span data-stu-id="a21a9-217">The complete contents of the *Global.asax* file is shown below.</span></span>

[!code-csharp[Main](aspnet-mvc-4-mobile-features/samples/sample9.cs)]

<span data-ttu-id="a21a9-218">保存更改。</span><span class="sxs-lookup"><span data-stu-id="a21a9-218">Save the changes.</span></span> <span data-ttu-id="a21a9-219">将*MvcMobile\Views\Shared\\_Layout*文件复制到*MvcMobile\Views\Shared\\_Layout*。</span><span class="sxs-lookup"><span data-stu-id="a21a9-219">Copy the *MvcMobile\Views\Shared\\_Layout.Mobile.cshtml* file to *MvcMobile\Views\Shared\\_Layout.iPhone.cshtml*.</span></span> <span data-ttu-id="a21a9-220">打开新文件，然后将 `h1` 标题从 "`Conference (Mobile)`" 更改为 "`Conference (iPhone)`"。</span><span class="sxs-lookup"><span data-stu-id="a21a9-220">Open the new file and then change the `h1` heading from `Conference (Mobile)` to `Conference (iPhone)`.</span></span>

<span data-ttu-id="a21a9-221">将*MvcMobile\Views\Home\AllTags.Mobile.cshtml*文件复制到*MvcMobile\Views\Home\AllTags.iPhone.cshtml*。</span><span class="sxs-lookup"><span data-stu-id="a21a9-221">Copy the *MvcMobile\Views\Home\AllTags.Mobile.cshtml* file to *MvcMobile\Views\Home\AllTags.iPhone.cshtml*.</span></span> <span data-ttu-id="a21a9-222">在新文件中，将 `<h2>` 元素从 "Tags （M）" 更改为 "Tags （iPhone）"。</span><span class="sxs-lookup"><span data-stu-id="a21a9-222">In the new file, change the `<h2>` element from "Tags (M)" to "Tags (iPhone)".</span></span>

<span data-ttu-id="a21a9-223">运行该应用程序。</span><span class="sxs-lookup"><span data-stu-id="a21a9-223">Run the application.</span></span> <span data-ttu-id="a21a9-224">运行移动浏览器模拟器，确保将其用户代理设置为“iPhone”，并浏览到 *AllTags* 视图。</span><span class="sxs-lookup"><span data-stu-id="a21a9-224">Run a mobile browser emulator, make sure its user agent is set to "iPhone", and browse to the *AllTags* view.</span></span> <span data-ttu-id="a21a9-225">以下屏幕截图显示了[Safari](http://www.apple.com/safari/download/)浏览器中呈现的*AllTags*视图。</span><span class="sxs-lookup"><span data-stu-id="a21a9-225">The following screenshot shows the *AllTags* view rendered in the [Safari](http://www.apple.com/safari/download/) browser.</span></span> <span data-ttu-id="a21a9-226">可在[此处](https://support.apple.com/kb/DL1531)下载适用于 Windows 的 Safari。</span><span class="sxs-lookup"><span data-stu-id="a21a9-226">You can download Safari for Windows [here](https://support.apple.com/kb/DL1531).</span></span>

<span data-ttu-id="a21a9-227">[![p2_iphoneView](aspnet-mvc-4-mobile-features/_static/image18.png)](aspnet-mvc-4-mobile-features/_static/image17.png)</span><span class="sxs-lookup"><span data-stu-id="a21a9-227">[![p2_iphoneView](aspnet-mvc-4-mobile-features/_static/image18.png)](aspnet-mvc-4-mobile-features/_static/image17.png)</span></span>

<span data-ttu-id="a21a9-228">在本部分中，我们已了解如何创建移动布局和视图，以及如何为特定的设备（如 iPhone）创建布局和视图。</span><span class="sxs-lookup"><span data-stu-id="a21a9-228">In this section we've seen how to create mobile layouts and views and how to create layouts and views for specific devices such as the iPhone.</span></span> <span data-ttu-id="a21a9-229">在下一部分中，你将了解如何利用 jQuery Mobile 获得更引人注目的移动视图。</span><span class="sxs-lookup"><span data-stu-id="a21a9-229">In the next section you'll see how to leverage jQuery Mobile for more compelling mobile views.</span></span>

## <a name="using-jquery-mobile"></a><span data-ttu-id="a21a9-230">使用 jQuery Mobile</span><span class="sxs-lookup"><span data-stu-id="a21a9-230">Using jQuery Mobile</span></span>

<span data-ttu-id="a21a9-231">[JQuery mobile](http://jquerymobile.com/demos/1.0b3/#/demos/1.0b3/docs/about/intro.html)库提供了一个可在所有主要移动浏览器上使用的用户界面框架。</span><span class="sxs-lookup"><span data-stu-id="a21a9-231">The [jQuery Mobile](http://jquerymobile.com/demos/1.0b3/#/demos/1.0b3/docs/about/intro.html) library provides a user interface framework that works on all the major mobile browsers.</span></span> <span data-ttu-id="a21a9-232">jQuery Mobile 可对支持 CSS 和 JavaScript 的移动浏览器应用*渐进增强*。</span><span class="sxs-lookup"><span data-stu-id="a21a9-232">jQuery Mobile applies *progressive enhancement* to mobile browsers that support CSS and JavaScript.</span></span> <span data-ttu-id="a21a9-233">渐进增强允许所有浏览器显示网页的基本内容，同时允许更强大的浏览器和设备拥有更丰富的显示。</span><span class="sxs-lookup"><span data-stu-id="a21a9-233">Progressive enhancement allows all browsers to display the basic content of a web page, while allowing more powerful browsers and devices to have a richer display.</span></span> <span data-ttu-id="a21a9-234">jQuery Mobile 中包括的 JavaScript 和 CSS 文件为众多元素设定了样式来适应移动浏览器，无需对标记做任何更改。</span><span class="sxs-lookup"><span data-stu-id="a21a9-234">The JavaScript and CSS files that are included with jQuery Mobile style many elements to fit mobile browsers without making any markup changes.</span></span>

<span data-ttu-id="a21a9-235">在本部分中，你将安装*jquery* NuGet 包，它将安装 jquery Mobile 和视图切换器小组件。</span><span class="sxs-lookup"><span data-stu-id="a21a9-235">In this section you'll install the *jQuery.Mobile.MVC* NuGet package, which installs jQuery Mobile and a view-switcher widget.</span></span>

<span data-ttu-id="a21a9-236">若要开始，请删除之前创建的*共享\\_Layout*并*共享\\_Layout* 。</span><span class="sxs-lookup"><span data-stu-id="a21a9-236">To start, delete the *Shared\\_Layout.Mobile.cshtml* and *Shared\\_Layout.iPhone.cshtml* files that you created earlier.</span></span>

<span data-ttu-id="a21a9-237">将*Views\Home\AllTags.Mobile.cshtml*和*Views\Home\AllTags.iPhone.cshtml*文件重命名为*Views\Home\AllTags.iPhone.cshtml.hide*和*Views\Home\AllTags.Mobile.cshtml.hide*。</span><span class="sxs-lookup"><span data-stu-id="a21a9-237">Rename *Views\Home\AllTags.Mobile.cshtml* and *Views\Home\AllTags.iPhone.cshtml* files to *Views\Home\AllTags.iPhone.cshtml.hide* and *Views\Home\AllTags.Mobile.cshtml.hide*.</span></span> <span data-ttu-id="a21a9-238">由于这些文件不再具有*ASP.NET 扩展名，* 因此它们不会被 MVC 运行时用来呈现*AllTags*视图。</span><span class="sxs-lookup"><span data-stu-id="a21a9-238">Because the files no longer have a *.cshtml* extension, they won't be used by the ASP.NET MVC runtime to render the *AllTags* view.</span></span>

<span data-ttu-id="a21a9-239">通过执行以下操作安装*jQuery* NuGet 包：</span><span class="sxs-lookup"><span data-stu-id="a21a9-239">Install the *jQuery.Mobile.MVC* NuGet package by doing this:</span></span>

1. <span data-ttu-id="a21a9-240">从 "**工具**" 菜单中，选择 " **NuGet 包管理器**"，然后选择 "**程序包管理器控制台**"。</span><span class="sxs-lookup"><span data-stu-id="a21a9-240">From the **Tools** menu, select **NuGet Package Manager**, and then select **Package Manager Console**.</span></span>

    <span data-ttu-id="a21a9-241">[![p3_packageMgr](aspnet-mvc-4-mobile-features/_static/image20.png)](aspnet-mvc-4-mobile-features/_static/image19.png)</span><span class="sxs-lookup"><span data-stu-id="a21a9-241">[![p3_packageMgr](aspnet-mvc-4-mobile-features/_static/image20.png)](aspnet-mvc-4-mobile-features/_static/image19.png)</span></span>
2. <span data-ttu-id="a21a9-242">在 "**程序包管理器控制台**" 中，输入 `Install-Package jQuery.Mobile.MVC -version 1.0.0`</span><span class="sxs-lookup"><span data-stu-id="a21a9-242">In the **Package Manager Console**, enter `Install-Package jQuery.Mobile.MVC -version 1.0.0`</span></span>

<span data-ttu-id="a21a9-243">下图显示了 NuGet jQuery. Mvcmobile.sln 项目添加并更改的文件。</span><span class="sxs-lookup"><span data-stu-id="a21a9-243">The following image shows the files added and changed to the MvcMobile project by the NuGet jQuery.Mobile.MVC package.</span></span> <span data-ttu-id="a21a9-244">添加的文件的文件名后面追加了 [add]。</span><span class="sxs-lookup"><span data-stu-id="a21a9-244">Files which are added have [add] appended after the file name.</span></span> <span data-ttu-id="a21a9-245">该图像不显示添加到*Content\images*文件夹中的 GIF 和 PNG 文件。</span><span class="sxs-lookup"><span data-stu-id="a21a9-245">The image does not show the GIF and PNG files added to the *Content\images* folder.</span></span>

![](aspnet-mvc-4-mobile-features/_static/image21.png)

<span data-ttu-id="a21a9-246">jQuery.Mobile.MVC NuGet 程序包将安装以下内容：</span><span class="sxs-lookup"><span data-stu-id="a21a9-246">The jQuery.Mobile.MVC NuGet package installs the following:</span></span>

- <span data-ttu-id="a21a9-247">*应用\_Start\BundleMobileConfig.cs*文件，该文件用于引用添加的 jQuery JAVASCRIPT 和 CSS 文件。</span><span class="sxs-lookup"><span data-stu-id="a21a9-247">The *App\_Start\BundleMobileConfig.cs* file, which is needed to reference the jQuery JavaScript and CSS files added.</span></span> <span data-ttu-id="a21a9-248">必须按照下面的说明并引用该文件中定义的移动捆绑。</span><span class="sxs-lookup"><span data-stu-id="a21a9-248">You must follow the instructions below and reference the mobile bundle defined in this file.</span></span>
- <span data-ttu-id="a21a9-249">jQuery Mobile CSS 文件。</span><span class="sxs-lookup"><span data-stu-id="a21a9-249">jQuery Mobile CSS files.</span></span>
- <span data-ttu-id="a21a9-250">`ViewSwitcher` 控制器小组件（*Controllers\ViewSwitcherController.cs*）。</span><span class="sxs-lookup"><span data-stu-id="a21a9-250">A `ViewSwitcher` controller widget (*Controllers\ViewSwitcherController.cs*).</span></span>
- <span data-ttu-id="a21a9-251">jQuery Mobile JavaScript 文件。</span><span class="sxs-lookup"><span data-stu-id="a21a9-251">jQuery Mobile JavaScript files.</span></span>
- <span data-ttu-id="a21a9-252">JQuery Mobile 样式的布局文件（*Views\Shared\\_Layout*。</span><span class="sxs-lookup"><span data-stu-id="a21a9-252">A jQuery Mobile-styled layout file (*Views\Shared\\_Layout.Mobile.cshtml*).</span></span>
- <span data-ttu-id="a21a9-253">视图切换器分部视图 *（MvcMobile\Views\Shared\\_ViewSwitcher*），它在每个页面的顶部提供一个链接，用于从桌面视图切换到移动视图，反之亦然。</span><span class="sxs-lookup"><span data-stu-id="a21a9-253">A view-switcher partial view *(MvcMobile\Views\Shared\\_ViewSwitcher.cshtml*) that provides a link at the top of each page to switch from desktop view to mobile view and vice versa.</span></span>
- <span data-ttu-id="a21a9-254"><em>Content\images</em>文件夹中的几个<em>.png</em>和<em>.gif</em>图像文件。</span><span class="sxs-lookup"><span data-stu-id="a21a9-254">Several<em>.png</em> and <em>.gif</em> image files in the <em>Content\images</em> folder.</span></span>

<span data-ttu-id="a21a9-255">打开*global.asax*文件，并添加以下代码作为 `Application_Start` 方法的最后一行。</span><span class="sxs-lookup"><span data-stu-id="a21a9-255">Open the *Global.asax* file and add the following code as the last line of the `Application_Start` method.</span></span>

[!code-csharp[Main](aspnet-mvc-4-mobile-features/samples/sample10.cs)]

<span data-ttu-id="a21a9-256">下面的代码显示完整的*global.asax*文件。</span><span class="sxs-lookup"><span data-stu-id="a21a9-256">The following code shows the complete *Global.asax* file.</span></span>

[!code-csharp[Main](aspnet-mvc-4-mobile-features/samples/sample11.cs?highlight=26)]

> [!NOTE]
> <span data-ttu-id="a21a9-257">如果你使用的是 Internet Explorer 9，但在黄色突出显示中看不到上面的 "`BundleMobileConfig`" 行，请单击 IE 中!["兼容性视图" 按钮（关闭](https://res2.windows.microsoft.com/resbox/en/Windows 7/main/f080e77f-9b66-4ac8-9af0-803c4f8a859c_15.jpg ""兼容性视图" 按钮的图片（关闭）")）的 "[兼容性视图" 按钮](https://windows.microsoft.com/windows7/How-to-use-Compatibility-View-in-Internet-Explorer-9)图片，使图标从!["兼容性视图" 按钮（"关闭"）](https://res2.windows.microsoft.com/resbox/en/Windows 7/main/f080e77f-9b66-4ac8-9af0-803c4f8a859c_15.jpg ""兼容性视图" 按钮的图片（关闭）")的大纲图片更改为!["兼容性视图" 按钮（打开](https://res1.windows.microsoft.com/resbox/en/Windows 7/main/156805ff-3130-481b-a12d-4d3a96470f36_14.jpg ""兼容性视图" 按钮的图片（on）")）的纯色图片。</span><span class="sxs-lookup"><span data-stu-id="a21a9-257">If you are using Internet Explorer 9 and you don't see the `BundleMobileConfig` line above in yellow highlight, click the [Compatibility View button](https://windows.microsoft.com/windows7/How-to-use-Compatibility-View-in-Internet-Explorer-9)![Picture of the Compatibility View button (off)](https://res2.windows.microsoft.com/resbox/en/Windows 7/main/f080e77f-9b66-4ac8-9af0-803c4f8a859c_15.jpg "Picture of the Compatibility View button (off)") in IE to make the icon change from an outline ![Picture of the Compatibility View button (off)](https://res2.windows.microsoft.com/resbox/en/Windows 7/main/f080e77f-9b66-4ac8-9af0-803c4f8a859c_15.jpg "Picture of the Compatibility View button (off)") to a solid color ![Picture of the Compatibility View button (on)](https://res1.windows.microsoft.com/resbox/en/Windows 7/main/156805ff-3130-481b-a12d-4d3a96470f36_14.jpg "Picture of the Compatibility View button (on)").</span></span> <span data-ttu-id="a21a9-258">或者，您也可以在 FireFox 或 Chrome 中查看本教程。</span><span class="sxs-lookup"><span data-stu-id="a21a9-258">Alternatively you can view this tutorial in FireFox or Chrome.</span></span>

<span data-ttu-id="a21a9-259">打开*MvcMobile\Views\Shared\\_Layout*文件，并直接在 `Html.Partial` 调用后添加以下标记：</span><span class="sxs-lookup"><span data-stu-id="a21a9-259">Open the *MvcMobile\Views\Shared\\_Layout.Mobile.cshtml* file and add the following markup directly after the `Html.Partial` call:</span></span>

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample12.cshtml)]

<span data-ttu-id="a21a9-260">完整的*MvcMobile\Views\Shared\\_Layout*的文件如下所示：</span><span class="sxs-lookup"><span data-stu-id="a21a9-260">The complete *MvcMobile\Views\Shared\\_Layout.Mobile.cshtml* file is shown below:</span></span>

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample13.cshtml)]

<span data-ttu-id="a21a9-261">构建应用程序，在移动浏览器模拟器中浏览到*AllTags*视图。</span><span class="sxs-lookup"><span data-stu-id="a21a9-261">Build the application, and in your mobile browser emulator browse to the *AllTags* view.</span></span> <span data-ttu-id="a21a9-262">您会看到如下内容：</span><span class="sxs-lookup"><span data-stu-id="a21a9-262">You see the following:</span></span>

<span data-ttu-id="a21a9-263">[![p3_afterNuGet](aspnet-mvc-4-mobile-features/_static/image23.png)](aspnet-mvc-4-mobile-features/_static/image22.png)</span><span class="sxs-lookup"><span data-stu-id="a21a9-263">[![p3_afterNuGet](aspnet-mvc-4-mobile-features/_static/image23.png)](aspnet-mvc-4-mobile-features/_static/image22.png)</span></span>

> [!NOTE]
> <span data-ttu-id="a21a9-264">可以通过将 IE 或 Chrome 的[用户代理字符串设置](http://www.howtogeek.com/113439/how-to-change-your-browsers-user-agent-without-installing-any-extensions/)为 iPhone，然后使用 F-12 开发人员工具来调试移动特定代码。</span><span class="sxs-lookup"><span data-stu-id="a21a9-264">You can debug the mobile specific code by [setting the user agent string](http://www.howtogeek.com/113439/how-to-change-your-browsers-user-agent-without-installing-any-extensions/) for IE or Chrome to iPhone and then using the F-12 developer tools.</span></span> <span data-ttu-id="a21a9-265">如果你的移动浏览器未将 "**主页**"、"**发言人**"、"**标签**" 和 "**日期**" 链接显示为按钮，则对 jQuery mobile 脚本和 CSS 文件的引用可能不正确。</span><span class="sxs-lookup"><span data-stu-id="a21a9-265">If your mobile browser doesn't display the **Home**, **Speaker**, **Tag**, and **Date** links as buttons, the references to jQuery Mobile scripts and CSS files are probably not correct.</span></span>

<span data-ttu-id="a21a9-266">除了样式更改之外，你还可以看到 "**移动视图**" 和一个链接，通过该链接，你可以从移动视图切换到桌面视图。</span><span class="sxs-lookup"><span data-stu-id="a21a9-266">In addition to the style changes, you see **Displaying mobile view** and a link that lets you switch from mobile view to desktop view.</span></span> <span data-ttu-id="a21a9-267">选择 "**桌面视图**" 链接，随即显示桌面视图。</span><span class="sxs-lookup"><span data-stu-id="a21a9-267">Choose the **Desktop view** link, and the desktop view is displayed.</span></span>

<span data-ttu-id="a21a9-268">[![p3_desktopView](aspnet-mvc-4-mobile-features/_static/image25.png)](aspnet-mvc-4-mobile-features/_static/image24.png)</span><span class="sxs-lookup"><span data-stu-id="a21a9-268">[![p3_desktopView](aspnet-mvc-4-mobile-features/_static/image25.png)](aspnet-mvc-4-mobile-features/_static/image24.png)</span></span>

<span data-ttu-id="a21a9-269">桌面视图不提供直接导航回移动视图的途径。</span><span class="sxs-lookup"><span data-stu-id="a21a9-269">The desktop view doesn't provide a way to directly navigate back to the mobile view.</span></span> <span data-ttu-id="a21a9-270">现在来修复此问题。</span><span class="sxs-lookup"><span data-stu-id="a21a9-270">You'll fix that now.</span></span> <span data-ttu-id="a21a9-271">打开*Views\Shared\\_Layout cshtml*文件。</span><span class="sxs-lookup"><span data-stu-id="a21a9-271">Open the *Views\Shared\\_Layout.cshtml* file.</span></span> <span data-ttu-id="a21a9-272">在页面 `body` 元素的正下方，添加以下代码，用于呈现视图切换器小组件：</span><span class="sxs-lookup"><span data-stu-id="a21a9-272">Just under the page `body` element, add the following code, which renders the view-switcher widget:</span></span>

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample14.cshtml)]

<span data-ttu-id="a21a9-273">在移动浏览器中刷新 " *AllTags* " 视图。</span><span class="sxs-lookup"><span data-stu-id="a21a9-273">Refresh the *AllTags* view in the mobile browser.</span></span> <span data-ttu-id="a21a9-274">您现在可以在桌面和移动视图间导航了。</span><span class="sxs-lookup"><span data-stu-id="a21a9-274">You can now navigate between desktop and mobile views.</span></span>

<span data-ttu-id="a21a9-275">[![p3_desktopViewWithMobileLink](aspnet-mvc-4-mobile-features/_static/image27.png)](aspnet-mvc-4-mobile-features/_static/image26.png)</span><span class="sxs-lookup"><span data-stu-id="a21a9-275">[![p3_desktopViewWithMobileLink](aspnet-mvc-4-mobile-features/_static/image27.png)](aspnet-mvc-4-mobile-features/_static/image26.png)</span></span>

> [!NOTE]
> <span data-ttu-id="a21a9-276">调试说明：可以将以下代码添加到 Views\Shared\\_ViewSwitcher 的末尾，以便在使用浏览器时帮助调试视图。将用户代理字符串设置为移动设备。</span><span class="sxs-lookup"><span data-stu-id="a21a9-276">Debug note: You can add the following code to the end of the Views\Shared\\_ViewSwitcher.cshtml to help debug views when using a browser the user agent string set to a mobile device.</span></span>
>
> [!code-csharp[Main](aspnet-mvc-4-mobile-features/samples/sample15.cs)]
>
> <span data-ttu-id="a21a9-277">并将以下标题添加到*Views\Shared\\_Layout cshtml*文件中。</span><span class="sxs-lookup"><span data-stu-id="a21a9-277">and adding the following heading to the *Views\Shared\\_Layout.cshtml* file.</span></span>
>
> [!code-html[Main](aspnet-mvc-4-mobile-features/samples/sample16.html)]

<span data-ttu-id="a21a9-278">在桌面浏览器中浏览到*AllTags*页。</span><span class="sxs-lookup"><span data-stu-id="a21a9-278">Browse to the *AllTags* page in a desktop browser.</span></span> <span data-ttu-id="a21a9-279">因为只将视图切换器小组件添加到了移动布局页面中，所以在桌面浏览器中未显示该小组件。</span><span class="sxs-lookup"><span data-stu-id="a21a9-279">The view-switcher widget is not displayed in a desktop browser because it's added only to the mobile layout page.</span></span> <span data-ttu-id="a21a9-280">在教程的稍后部分中，您将学习如何将视图切换器小组件添加到桌面视图中。</span><span class="sxs-lookup"><span data-stu-id="a21a9-280">Later in the tutorial you'll see how you can add the view-switcher widget to the desktop view.</span></span>

<span data-ttu-id="a21a9-281">[![p3_desktopBrowser](aspnet-mvc-4-mobile-features/_static/image29.png)](aspnet-mvc-4-mobile-features/_static/image28.png)</span><span class="sxs-lookup"><span data-stu-id="a21a9-281">[![p3_desktopBrowser](aspnet-mvc-4-mobile-features/_static/image29.png)](aspnet-mvc-4-mobile-features/_static/image28.png)</span></span>

## <a name="improving-the-speakers-list"></a><span data-ttu-id="a21a9-282">改进发言人列表</span><span class="sxs-lookup"><span data-stu-id="a21a9-282">Improving the Speakers List</span></span>

<span data-ttu-id="a21a9-283">在移动浏览器中，选择“发言人”链接。</span><span class="sxs-lookup"><span data-stu-id="a21a9-283">In the mobile browser, select the **Speakers** link.</span></span> <span data-ttu-id="a21a9-284">因为没有移动视图（*allspeakers.mobile.cshtml*），所以使用移动布局视图（ *\_* allspeakers.mobile.cshtml）呈现默认的演讲者（）（可能为英语）。</span><span class="sxs-lookup"><span data-stu-id="a21a9-284">Because there's no mobile view(*AllSpeakers.Mobile.cshtml*), the default speakers display (*AllSpeakers.cshtml*) is rendered using the mobile layout view (*\_Layout.Mobile.cshtml*).</span></span>

<span data-ttu-id="a21a9-285">[![p3_speakersDeskTop](aspnet-mvc-4-mobile-features/_static/image31.png)](aspnet-mvc-4-mobile-features/_static/image30.png)</span><span class="sxs-lookup"><span data-stu-id="a21a9-285">[![p3_speakersDeskTop](aspnet-mvc-4-mobile-features/_static/image31.png)](aspnet-mvc-4-mobile-features/_static/image30.png)</span></span>

<span data-ttu-id="a21a9-286">你可以通过将 `RequireConsistentDisplayMode` 设置为 `true` 在视图中的 *_ViewStart\\视图*中，在移动布局内全局禁用默认（非移动）视图，如下所示：</span><span class="sxs-lookup"><span data-stu-id="a21a9-286">You can globally disable a default (non-mobile) view from rendering inside a mobile layout by setting `RequireConsistentDisplayMode` to `true` in the *Views\\_ViewStart.cshtml* file, like this:</span></span>

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample17.cshtml)]

<span data-ttu-id="a21a9-287">将 `RequireConsistentDisplayMode` 设置为 `true`时，移动布局（<em>\_layout</em>）只用于移动视图。</span><span class="sxs-lookup"><span data-stu-id="a21a9-287">When `RequireConsistentDisplayMode` is set to `true`, the mobile layout (<em>\_Layout.Mobile.cshtml</em>) is used only for mobile views.</span></span> <span data-ttu-id="a21a9-288">（也就是说，视图文件的格式为<em>\* \* ViewName</em><em>。</em>如果你的移动布局不太适合你的非移动视图，则可能需要将 `RequireConsistentDisplayMode` 设置为 `true`。</span><span class="sxs-lookup"><span data-stu-id="a21a9-288">(That is, the view file is of the form <em>\*\*ViewName</em><em>.Mobile.cshtml</em>.) You might want to set `RequireConsistentDisplayMode` to `true` if your mobile layout doesn't work well with your non-mobile views.</span></span> <span data-ttu-id="a21a9-289">下面的屏幕截图显示当 `RequireConsistentDisplayMode` 设置为 `true`时，如何呈现 "<em>发言人</em>" 页面。</span><span class="sxs-lookup"><span data-stu-id="a21a9-289">The screenshot below shows how the <em>Speakers</em> page renders when `RequireConsistentDisplayMode` is set to `true`.</span></span>

<span data-ttu-id="a21a9-290">[![p3_speakersConsistent](aspnet-mvc-4-mobile-features/_static/image33.png)](aspnet-mvc-4-mobile-features/_static/image32.png)</span><span class="sxs-lookup"><span data-stu-id="a21a9-290">[![p3_speakersConsistent](aspnet-mvc-4-mobile-features/_static/image33.png)](aspnet-mvc-4-mobile-features/_static/image32.png)</span></span>

<span data-ttu-id="a21a9-291">您可以通过在视图文件中将 `RequireConsistentDisplayMode` 设置为 `false` 来禁用视图中一致的显示模式。</span><span class="sxs-lookup"><span data-stu-id="a21a9-291">You can disable consistent display mode in a view by setting `RequireConsistentDisplayMode` to `false` in the view file.</span></span> <span data-ttu-id="a21a9-292">*Views\Home\AllSpeakers.cshtml*文件中的以下标记将 `RequireConsistentDisplayMode` 设置为 `false`：</span><span class="sxs-lookup"><span data-stu-id="a21a9-292">The following markup in the *Views\Home\AllSpeakers.cshtml* file sets `RequireConsistentDisplayMode` to `false`:</span></span>

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample18.cshtml)]

## <a name="creating-a-mobile-speakers-view"></a><span data-ttu-id="a21a9-293">创建移动发言人视图</span><span class="sxs-lookup"><span data-stu-id="a21a9-293">Creating a Mobile Speakers View</span></span>

<span data-ttu-id="a21a9-294">正如你刚才看到的，"*发言人*" 视图是可读的，但链接很小，难于在移动设备上点击。</span><span class="sxs-lookup"><span data-stu-id="a21a9-294">As you just saw, the *Speakers* view is readable, but the links are small and are difficult to tap on a mobile device.</span></span> <span data-ttu-id="a21a9-295">在本部分中，你将创建一个移动特定的 "*发言人*" 视图，它看起来像一个现代移动应用程序，它显示的是大、易于点击的链接，并包含一个搜索框，用于快速查找扬声器。</span><span class="sxs-lookup"><span data-stu-id="a21a9-295">In this section, you'll create a mobile-specific *Speakers* view that looks like a modern mobile application — it displays large, easy-to-tap links and contains a search box to quickly find speakers.</span></span>

<span data-ttu-id="a21a9-296">将*allspeakers.mobile.cshtml*复制到*allspeakers.mobile.cshtml*。</span><span class="sxs-lookup"><span data-stu-id="a21a9-296">Copy *AllSpeakers.cshtml* to *AllSpeakers.Mobile.cshtml*.</span></span> <span data-ttu-id="a21a9-297">打开*allspeakers.mobile.cshtml*文件并删除 `<h2>` 标题元素。</span><span class="sxs-lookup"><span data-stu-id="a21a9-297">Open the *AllSpeakers.Mobile.cshtml* file and remove the `<h2>` heading element.</span></span>

<span data-ttu-id="a21a9-298">在 `<ul>` 标记中，添加 `data-role` 属性，并将其值设置为 "`listview`"。</span><span class="sxs-lookup"><span data-stu-id="a21a9-298">In the `<ul>` tag, add the `data-role` attribute and set its value to `listview`.</span></span> <span data-ttu-id="a21a9-299">与其他[`data-*` 属性](http://html5doctor.com/html5-custom-data-attributes/)一样，`data-role="listview"` 使大型列表项更易于点击。</span><span class="sxs-lookup"><span data-stu-id="a21a9-299">Like other [`data-*` attributes](http://html5doctor.com/html5-custom-data-attributes/), `data-role="listview"` makes the large list items easier to tap.</span></span> <span data-ttu-id="a21a9-300">完成的标记如下所示：</span><span class="sxs-lookup"><span data-stu-id="a21a9-300">This is what the completed markup looks like:</span></span>

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample19.cshtml)]

<span data-ttu-id="a21a9-301">刷新移动浏览器。</span><span class="sxs-lookup"><span data-stu-id="a21a9-301">Refresh the mobile browser.</span></span> <span data-ttu-id="a21a9-302">更新的视图如下所示：</span><span class="sxs-lookup"><span data-stu-id="a21a9-302">The updated view looks like this:</span></span>

<span data-ttu-id="a21a9-303">[![p3_updatedSpeakerView1](aspnet-mvc-4-mobile-features/_static/image35.png)](aspnet-mvc-4-mobile-features/_static/image34.png)</span><span class="sxs-lookup"><span data-stu-id="a21a9-303">[![p3_updatedSpeakerView1](aspnet-mvc-4-mobile-features/_static/image35.png)](aspnet-mvc-4-mobile-features/_static/image34.png)</span></span>

<span data-ttu-id="a21a9-304">尽管移动视图得到了改进，但很难在较长的发言人列表中导航。</span><span class="sxs-lookup"><span data-stu-id="a21a9-304">Although the mobile view has improved, it's difficult to navigate the long list of speakers.</span></span> <span data-ttu-id="a21a9-305">若要解决此问题，请在 `<ul>` 标记中添加 `data-filter` 属性，并将其设置为 `true`。</span><span class="sxs-lookup"><span data-stu-id="a21a9-305">To fix this, in the `<ul>` tag, add the `data-filter` attribute and set it to `true`.</span></span> <span data-ttu-id="a21a9-306">下面的代码演示 `ul` 标记。</span><span class="sxs-lookup"><span data-stu-id="a21a9-306">The code below shows the `ul` markup.</span></span>

[!code-html[Main](aspnet-mvc-4-mobile-features/samples/sample20.html)]

<span data-ttu-id="a21a9-307">下图显示了 `data-filter` 属性生成的页面顶部的 "搜索筛选器" 框。</span><span class="sxs-lookup"><span data-stu-id="a21a9-307">The following image shows the search filter box at the top of the page that results from the `data-filter` attribute.</span></span>

<span data-ttu-id="a21a9-308">[![ps_Data_Filter](aspnet-mvc-4-mobile-features/_static/image37.png)](aspnet-mvc-4-mobile-features/_static/image36.png)</span><span class="sxs-lookup"><span data-stu-id="a21a9-308">[![ps_Data_Filter](aspnet-mvc-4-mobile-features/_static/image37.png)](aspnet-mvc-4-mobile-features/_static/image36.png)</span></span>

<span data-ttu-id="a21a9-309">当您在搜索框中键入每个字母时，jQuery Mobile 将筛选显示的列表，如下图所示。</span><span class="sxs-lookup"><span data-stu-id="a21a9-309">As you type each letter in the search box, jQuery Mobile filters the displayed list as shown in the image below.</span></span>

<span data-ttu-id="a21a9-310">[![ps_data_filter_SC](aspnet-mvc-4-mobile-features/_static/image39.png)](aspnet-mvc-4-mobile-features/_static/image38.png)</span><span class="sxs-lookup"><span data-stu-id="a21a9-310">[![ps_data_filter_SC](aspnet-mvc-4-mobile-features/_static/image39.png)](aspnet-mvc-4-mobile-features/_static/image38.png)</span></span>

## <a name="improving-the-tags-list"></a><span data-ttu-id="a21a9-311">改善标记列表</span><span class="sxs-lookup"><span data-stu-id="a21a9-311">Improving the Tags List</span></span>

<span data-ttu-id="a21a9-312">与默认 "*发言人*" 视图一样，"*标记*" 视图是可读的，但链接比较小，难于在移动设备上点击。</span><span class="sxs-lookup"><span data-stu-id="a21a9-312">Like the default *Speakers* view, the *Tags* view is readable, but the links are small and difficult to tap on a mobile device.</span></span> <span data-ttu-id="a21a9-313">在本部分中，您将修复 "*标记*" 视图，与修复 "*发言人*" 视图的方式相同。</span><span class="sxs-lookup"><span data-stu-id="a21a9-313">In this section, you'll fix the *Tags* view the same way you fixed the *Speakers* view.</span></span>

<span data-ttu-id="a21a9-314">删除 &quot;隐藏*Views\Home\AllTags.Mobile.cshtml.hide*文件的&quot; 后缀，使名称为*Views\Home\AllTags.Mobile.cshtml*。</span><span class="sxs-lookup"><span data-stu-id="a21a9-314">Remove the &quot;hide&quot; suffix to the *Views\Home\AllTags.Mobile.cshtml.hide* file so the name is *Views\Home\AllTags.Mobile.cshtml*.</span></span> <span data-ttu-id="a21a9-315">打开重命名的文件，并删除 `<h2>` 元素。</span><span class="sxs-lookup"><span data-stu-id="a21a9-315">Open the renamed file and remove the `<h2>` element.</span></span>

<span data-ttu-id="a21a9-316">将 `data-role` 和 `data-filter` 属性添加到 `<ul>` 标记，如下所示：</span><span class="sxs-lookup"><span data-stu-id="a21a9-316">Add the `data-role` and `data-filter` attributes to the `<ul>` tag, as shown here:</span></span>

[!code-html[Main](aspnet-mvc-4-mobile-features/samples/sample21.html)]

<span data-ttu-id="a21a9-317">下图显示了字母 `J`上的 "标记" 页筛选。</span><span class="sxs-lookup"><span data-stu-id="a21a9-317">The image below shows the tags page filtering on the letter `J`.</span></span>

<span data-ttu-id="a21a9-318">[![p3_tags_J](aspnet-mvc-4-mobile-features/_static/image41.png)](aspnet-mvc-4-mobile-features/_static/image40.png)</span><span class="sxs-lookup"><span data-stu-id="a21a9-318">[![p3_tags_J](aspnet-mvc-4-mobile-features/_static/image41.png)](aspnet-mvc-4-mobile-features/_static/image40.png)</span></span>

## <a name="improving-the-dates-list"></a><span data-ttu-id="a21a9-319">改进日期列表</span><span class="sxs-lookup"><span data-stu-id="a21a9-319">Improving the Dates List</span></span>

<span data-ttu-id="a21a9-320">你可以像改进 "*发言人*" 和 "*标签*" 视图那样改进 "*日期*" 视图，使其更易于在移动设备上使用。</span><span class="sxs-lookup"><span data-stu-id="a21a9-320">You can improve the *Dates* view like you improved the *Speakers* and *Tags* views, so that it's easier to use on a mobile device.</span></span>

<span data-ttu-id="a21a9-321">将*Views\Home\AllDates.cshtml*文件复制到*Views\Home\AllDates.Mobile.cshtml*。</span><span class="sxs-lookup"><span data-stu-id="a21a9-321">Copy the *Views\Home\AllDates.cshtml* file to *Views\Home\AllDates.Mobile.cshtml*.</span></span> <span data-ttu-id="a21a9-322">打开新文件并删除 `<h2>` 元素。</span><span class="sxs-lookup"><span data-stu-id="a21a9-322">Open the new file and remove the `<h2>` element.</span></span>

<span data-ttu-id="a21a9-323">向 `<ul>` 标记添加 `data-role="listview"`，如下所示：</span><span class="sxs-lookup"><span data-stu-id="a21a9-323">Add `data-role="listview"` to the `<ul>` tag, like this:</span></span>

[!code-html[Main](aspnet-mvc-4-mobile-features/samples/sample22.html)]

<span data-ttu-id="a21a9-324">下图显示了 "**日期**" 页面与 "`data-role`" 属性相同的外观。</span><span class="sxs-lookup"><span data-stu-id="a21a9-324">The image below shows what the **Date** page looks like with the `data-role` attribute in place.</span></span>

<span data-ttu-id="a21a9-325">[![p3_dates1](aspnet-mvc-4-mobile-features/_static/image43.png)](aspnet-mvc-4-mobile-features/_static/image42.png)将*Views\Home\AllDates.Mobile.cshtml*文件的内容替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="a21a9-325">[![p3_dates1](aspnet-mvc-4-mobile-features/_static/image43.png)](aspnet-mvc-4-mobile-features/_static/image42.png) Replace the contents of the *Views\Home\AllDates.Mobile.cshtml* file with the following code:</span></span>

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample23.cshtml)]

<span data-ttu-id="a21a9-326">此代码按日期将所有会话分组。</span><span class="sxs-lookup"><span data-stu-id="a21a9-326">This code groups all sessions by days.</span></span> <span data-ttu-id="a21a9-327">它为每个新日期创建一条列表分隔线，在分隔线下列出一天的所有会话。</span><span class="sxs-lookup"><span data-stu-id="a21a9-327">It creates a list divider for each new day, and it lists all the sessions for each day under a divider.</span></span> <span data-ttu-id="a21a9-328">当此代码运行时，它看起来像这样：</span><span class="sxs-lookup"><span data-stu-id="a21a9-328">Here's what it looks like when this code runs:</span></span>

<span data-ttu-id="a21a9-329">[![p3_dates2](aspnet-mvc-4-mobile-features/_static/image45.png)](aspnet-mvc-4-mobile-features/_static/image44.png)</span><span class="sxs-lookup"><span data-stu-id="a21a9-329">[![p3_dates2](aspnet-mvc-4-mobile-features/_static/image45.png)](aspnet-mvc-4-mobile-features/_static/image44.png)</span></span>

## <a name="improving-the-sessionstable-view"></a><span data-ttu-id="a21a9-330">改进 SessionsTable 视图</span><span class="sxs-lookup"><span data-stu-id="a21a9-330">Improving the SessionsTable View</span></span>

<span data-ttu-id="a21a9-331">在本节中，您将创建一个移动特定的会话视图。</span><span class="sxs-lookup"><span data-stu-id="a21a9-331">In this section, you'll create a mobile-specific view of sessions.</span></span> <span data-ttu-id="a21a9-332">我们所做的更改将比在我们创建的其他视图中更广泛。</span><span class="sxs-lookup"><span data-stu-id="a21a9-332">The changes we make will be more extensive than in other views we have created.</span></span>

<span data-ttu-id="a21a9-333">在移动浏览器中，点击 "**发言人**" 按钮，然后在搜索框中输入 `Sc`。</span><span class="sxs-lookup"><span data-stu-id="a21a9-333">In the mobile browser, tap the **Speaker** button, then enter `Sc` in the search box.</span></span>

<span data-ttu-id="a21a9-334">[![ps_data_filter_SC](aspnet-mvc-4-mobile-features/_static/image47.png)](aspnet-mvc-4-mobile-features/_static/image46.png)</span><span class="sxs-lookup"><span data-stu-id="a21a9-334">[![ps_data_filter_SC](aspnet-mvc-4-mobile-features/_static/image47.png)](aspnet-mvc-4-mobile-features/_static/image46.png)</span></span>

<span data-ttu-id="a21a9-335">点击**Scott Hanselman**链接。</span><span class="sxs-lookup"><span data-stu-id="a21a9-335">Tap the **Scott Hanselman** link.</span></span>

<span data-ttu-id="a21a9-336">[![p3_scottHa](aspnet-mvc-4-mobile-features/_static/image49.png)](aspnet-mvc-4-mobile-features/_static/image48.png)</span><span class="sxs-lookup"><span data-stu-id="a21a9-336">[![p3_scottHa](aspnet-mvc-4-mobile-features/_static/image49.png)](aspnet-mvc-4-mobile-features/_static/image48.png)</span></span>

<span data-ttu-id="a21a9-337">正如您所看到的，显示的内容难以在移动浏览器上阅读。</span><span class="sxs-lookup"><span data-stu-id="a21a9-337">As you can see, the display is difficult to read on a mobile browser.</span></span> <span data-ttu-id="a21a9-338">日期列难于阅读，标签列也超出了视图。</span><span class="sxs-lookup"><span data-stu-id="a21a9-338">The date column is hard to read and the tags column is out of the view.</span></span> <span data-ttu-id="a21a9-339">若要解决此问题，请将*Views\Home\SessionsTable.cshtml*复制到*Views\Home\SessionsTable.Mobile.cshtml*，然后将该文件的内容替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="a21a9-339">To fix this, copy *Views\Home\SessionsTable.cshtml* to *Views\Home\SessionsTable.Mobile.cshtml*, and then replace the contents of the file with the following code:</span></span>

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample24.cshtml)]

<span data-ttu-id="a21a9-340">该代码移除了 Room 和 Tag 列，将标题、发言人和日期设置为竖式，这样，即可在移动浏览器中阅读所有此类信息。</span><span class="sxs-lookup"><span data-stu-id="a21a9-340">The code removes the room and tags columns, and formats the title, speaker, and date vertically, so that all this information is readable on a mobile browser.</span></span> <span data-ttu-id="a21a9-341">下图反映了代码更改。</span><span class="sxs-lookup"><span data-stu-id="a21a9-341">The image below reflects the code changes.</span></span>

<span data-ttu-id="a21a9-342">[![ps_SessionsByScottHa](aspnet-mvc-4-mobile-features/_static/image51.png)](aspnet-mvc-4-mobile-features/_static/image50.png)</span><span class="sxs-lookup"><span data-stu-id="a21a9-342">[![ps_SessionsByScottHa](aspnet-mvc-4-mobile-features/_static/image51.png)](aspnet-mvc-4-mobile-features/_static/image50.png)</span></span>

## <a name="improving-the-sessionbycode-view"></a><span data-ttu-id="a21a9-343">改进 SessionByCode 视图</span><span class="sxs-lookup"><span data-stu-id="a21a9-343">Improving the SessionByCode View</span></span>

<span data-ttu-id="a21a9-344">最后，您将创建一个特定于移动设备的*SessionByCode*视图。</span><span class="sxs-lookup"><span data-stu-id="a21a9-344">Finally, you'll create a mobile-specific view of the *SessionByCode* view.</span></span> <span data-ttu-id="a21a9-345">在移动浏览器中，点击 "**发言人**" 按钮，然后在搜索框中输入 `Sc`。</span><span class="sxs-lookup"><span data-stu-id="a21a9-345">In the mobile browser, tap the **Speaker** button, then enter `Sc` in the search box.</span></span>

<span data-ttu-id="a21a9-346">[![ps_data_filter_SC](aspnet-mvc-4-mobile-features/_static/image53.png)](aspnet-mvc-4-mobile-features/_static/image52.png)</span><span class="sxs-lookup"><span data-stu-id="a21a9-346">[![ps_data_filter_SC](aspnet-mvc-4-mobile-features/_static/image53.png)](aspnet-mvc-4-mobile-features/_static/image52.png)</span></span>

<span data-ttu-id="a21a9-347">点击**Scott Hanselman**链接。</span><span class="sxs-lookup"><span data-stu-id="a21a9-347">Tap the **Scott Hanselman** link.</span></span> <span data-ttu-id="a21a9-348">将显示 Scott Hanselman 的会话。</span><span class="sxs-lookup"><span data-stu-id="a21a9-348">Scott Hanselman's sessions are displayed.</span></span>

<span data-ttu-id="a21a9-349">[![ps_SessionsByScottHa](aspnet-mvc-4-mobile-features/_static/image55.png)](aspnet-mvc-4-mobile-features/_static/image54.png)</span><span class="sxs-lookup"><span data-stu-id="a21a9-349">[![ps_SessionsByScottHa](aspnet-mvc-4-mobile-features/_static/image55.png)](aspnet-mvc-4-mobile-features/_static/image54.png)</span></span>

<span data-ttu-id="a21a9-350">选择 **"Microsoft 欢迎使用 Web 堆栈"** 链接的概述。</span><span class="sxs-lookup"><span data-stu-id="a21a9-350">Choose the **An Overview of the MS Web Stack of Love** link.</span></span>

<span data-ttu-id="a21a9-351">[![ps_love](aspnet-mvc-4-mobile-features/_static/image57.png)](aspnet-mvc-4-mobile-features/_static/image56.png)</span><span class="sxs-lookup"><span data-stu-id="a21a9-351">[![ps_love](aspnet-mvc-4-mobile-features/_static/image57.png)](aspnet-mvc-4-mobile-features/_static/image56.png)</span></span>

<span data-ttu-id="a21a9-352">默认桌面视图虽然不错，但仍可以改进。</span><span class="sxs-lookup"><span data-stu-id="a21a9-352">The default desktop view is fine, but you can improve it.</span></span>

<span data-ttu-id="a21a9-353">将*views\home\sessionbycode.cshtml 复制*复制到*Views\Home\SessionByCode.Mobile.cshtml* ，并将*Views\Home\SessionByCode.Mobile.cshtml*文件的内容替换为以下标记：</span><span class="sxs-lookup"><span data-stu-id="a21a9-353">Copy the *Views\Home\SessionByCode.cshtml* to *Views\Home\SessionByCode.Mobile.cshtml* and replace the contents of the *Views\Home\SessionByCode.Mobile.cshtml* file with the following markup:</span></span>

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample25.cshtml)]

<span data-ttu-id="a21a9-354">新标记使用 `data-role` 特性来改进视图的布局。</span><span class="sxs-lookup"><span data-stu-id="a21a9-354">The new markup uses the `data-role` attribute to improve the layout of the view.</span></span>

<span data-ttu-id="a21a9-355">刷新移动浏览器。</span><span class="sxs-lookup"><span data-stu-id="a21a9-355">Refresh the mobile browser.</span></span> <span data-ttu-id="a21a9-356">下图反映你刚才所做的代码更改：</span><span class="sxs-lookup"><span data-stu-id="a21a9-356">The following image reflects the code changes that you just made:</span></span>

<span data-ttu-id="a21a9-357">[![p3_love2](aspnet-mvc-4-mobile-features/_static/image59.png)](aspnet-mvc-4-mobile-features/_static/image58.png)</span><span class="sxs-lookup"><span data-stu-id="a21a9-357">[![p3_love2](aspnet-mvc-4-mobile-features/_static/image59.png)](aspnet-mvc-4-mobile-features/_static/image58.png)</span></span>

## <a name="wrapup-and-review"></a><span data-ttu-id="a21a9-358">Wrapup 和评审</span><span class="sxs-lookup"><span data-stu-id="a21a9-358">Wrapup and Review</span></span>

<span data-ttu-id="a21a9-359">本教程介绍了 ASP.NET MVC 4 开发者预览版的新移动功能。</span><span class="sxs-lookup"><span data-stu-id="a21a9-359">This tutorial has introduced the new mobile features of ASP.NET MVC 4 Developer Preview.</span></span> <span data-ttu-id="a21a9-360">移动功能包括：</span><span class="sxs-lookup"><span data-stu-id="a21a9-360">The mobile features include:</span></span>

- <span data-ttu-id="a21a9-361">覆盖全局视图和单个视图的布局、视图和分部视图的功能。</span><span class="sxs-lookup"><span data-stu-id="a21a9-361">The ability to override layout, views, and partial views, both globally and for an individual view.</span></span>
- <span data-ttu-id="a21a9-362">使用 `RequireConsistentDisplayMode` 属性控制布局和部分重写强制。</span><span class="sxs-lookup"><span data-stu-id="a21a9-362">Control over layout and partial override enforcement using the `RequireConsistentDisplayMode` property.</span></span>
- <span data-ttu-id="a21a9-363">移动视图的视图切换器小组件（而不是在桌面视图中显示）。</span><span class="sxs-lookup"><span data-stu-id="a21a9-363">A view-switcher widget for mobile views than can also be displayed in desktop views.</span></span>
- <span data-ttu-id="a21a9-364">支持特定的浏览器，例如 iPhone 浏览器。</span><span class="sxs-lookup"><span data-stu-id="a21a9-364">Support for supporting specific browsers, such as the iPhone browser.</span></span>

## <a name="see-also"></a><span data-ttu-id="a21a9-365">另请参阅</span><span class="sxs-lookup"><span data-stu-id="a21a9-365">See Also</span></span>

- <span data-ttu-id="a21a9-366">[JQuery mobile](http://jquerymobile.com)站点。</span><span class="sxs-lookup"><span data-stu-id="a21a9-366">[jQuery Mobile](http://jquerymobile.com) site.</span></span>
- [<span data-ttu-id="a21a9-367">jQuery Mobile 概述</span><span class="sxs-lookup"><span data-stu-id="a21a9-367">jQuery Mobile Overview</span></span>](http://jquerymobile.com/demos/1.0b3/docs/about/intro.html)
- [<span data-ttu-id="a21a9-368">W3C 建议移动 Web 应用程序的最佳做法</span><span class="sxs-lookup"><span data-stu-id="a21a9-368">W3C Recommendation Mobile Web Application Best Practices</span></span>](http://www.w3.org/TR/mwabp/)
- [<span data-ttu-id="a21a9-369">用于媒体查询的 W3C 候选建议方案</span><span class="sxs-lookup"><span data-stu-id="a21a9-369">W3C Candidate Recommendation for media queries</span></span>](http://www.w3.org/TR/css3-mediaqueries/)
