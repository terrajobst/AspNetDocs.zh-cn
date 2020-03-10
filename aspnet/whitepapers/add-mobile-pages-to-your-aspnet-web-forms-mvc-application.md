---
uid: whitepapers/add-mobile-pages-to-your-aspnet-web-forms-mvc-application
title: 如何：向 ASP.NET Web 窗体/MVC 应用程序添加移动页面 |Microsoft Docs
author: rick-anderson
description: 本指南说明如何从 ASP.NET Web Forms/MVC 应用程序为移动设备提供优化页面的各种方法，并提供体系结构和 。
ms.author: riande
ms.date: 01/20/2011
ms.assetid: 3124f28e-cc32-418a-afe3-519fa56f4c36
msc.legacyurl: /whitepapers/add-mobile-pages-to-your-aspnet-web-forms-mvc-application
msc.type: content
ms.openlocfilehash: 63c555358d06a9506bb5c8c993800c3307108192
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78462212"
---
# <a name="how-to-add-mobile-pages-to-your-aspnet-web-forms--mvc-application"></a>如何：向 ASP.NET Web 窗体/MVC 应用程序添加移动页

> **适用于**
> 
> - ASP.NET Web 窗体4.0 版
> - ASP.NET MVC 版本3。0
> 
> **摘要**
> 
> 本指南介绍了从 ASP.NET Web Forms/MVC 应用程序为移动设备提供优化页面的各种方法，并提供了面向各种设备时要考虑的体系结构和设计问题。 本文档还介绍了从 ASP.NET 2.0 到3.5 的 ASP.NET 移动控件现在已过时的原因，并讨论了一些新式替代方法。

## <a name="contents"></a>内容

- 概述
- 体系结构选项
- 浏览器和设备检测
- ASP.NET Web 窗体应用程序如何提供特定于移动的页面
- ASP.NET MVC 应用程序如何提供特定于移动的页面
- 其他资源

有关演示如何将此白皮书用于 ASP.NET Web 窗体和 MVC 的可下载代码示例，请参阅[采用 ASP.NET & 站点的移动应用](https://docs.microsoft.com/aspnet/mobile/overview)。

## <a name="overview"></a>概述

移动设备–智能手机、功能电话和平板电脑–以一种访问 Web 的方式继续增长。 对于许多 web 开发人员和面向 web 的企业而言，这意味着对于使用这些设备的访问者而言，为访问者提供丰富的浏览体验变得越来越重要。

### <a name="how-earlier-versions-of-aspnet-supported-mobile-browsers"></a>更早版本的 ASP.NET 支持的移动浏览器

ASP.NET 版本2.0 到3.5 包括*ASP.NET 移动控件*：针对移动设备的一组服务器控件和*MobileControls*命名空间*中的移动*设备。 该程序集仍包含在 ASP.NET 4 中，但已弃用。 建议开发人员迁移到更现代的方法，如本文中所述。

将 ASP.NET 移动控件标记为过时的原因是其设计面向2005及更早版本常见的移动电话。 控件的主要目的是为该时代的 WAP 浏览器呈现 WML 或 cHTML 标记（而不是常规 HTML）。 但对于大多数项目，WAP、WML 和 cHTML 不再相关，因为现在 HTML 已成为移动和桌面浏览器的广泛标记语言。

### <a name="the-challenges-of-supporting-mobile-devices-today"></a>目前支持移动设备的挑战

尽管移动浏览器现在已经完全支持 HTML，但当您想要创建精彩的移动浏览体验时，您仍会遇到许多挑战：

- ***屏幕大小***-移动设备外形明显不同，其屏幕通常比桌面监视器小得多。 因此，您可能需要为它们设计完全不同的页面布局。
- ***输入法***–某些设备有键盘，某些设备有 styluses，其他设备使用触控。 您可能需要考虑多个导航机制和数据输入方法。
- ***标准相容性***–许多移动浏览器不支持最新的 HTML、CSS 或 JavaScript 标准。
- ***带宽***–移动电话数据网络性能差异很高，某些最终用户在 tariffs 上按兆字节收费。

没有一种适合全部的解决方案;根据访问应用程序的设备，应用程序的外观和行为将有所不同。 对于 web 开发人员来说，这对于桌面 "browser 大战" 来说可能是一个更大的挑战。

首次出现移动浏览器支持的开发人员最初认为仅支持最新和最先进的智能手机（例如 Windows Phone 7、iPhone 或 Android），这可能是因为开发人员通常是装置. 然而，更便宜的手机仍然非常受欢迎，其所有者确实会使用它们来浏览 web，尤其是在使用手机进行宽带连接的国家/地区。 企业需要通过考虑其可能的客户来决定要支持的设备范围。 如果要为一项高级的运行状况 spa 构建在线小册子，则可以仅针对高级智能手机进行业务决策，而如果要为电影创建票证预定系统，则可能需要考虑到功能不太强大的访问者部.

## <a name="architectural-options"></a>体系结构选项

在转到 ASP.NET Web 窗体或 MVC 的特定技术详细信息之前，请注意，一般情况下，web 开发人员有三个主要可能选项用于支持移动浏览器：

1. ***不执行任何操作–*** 你只需创建一个面向桌面的标准 web 应用程序，然后依赖移动浏览器将其呈现为可接受。 

    - **优势**：这是实施和维护的最便宜的选项–无需额外工作
    - **缺点**：提供最差的最终用户体验： 

        - 最新的智能手机可能会呈现您的 HTML 和桌面浏览器，但用户仍会被迫水平和垂直滚动以在小屏幕上使用您的内容。 这并不是最佳做法。
        - 较旧的设备和功能电话可能无法以令人满意的方式呈现你的标记。
        - 即使是最新的 tablet 设备（其屏幕可以像便携式计算机屏幕一样大），也会应用不同的交互规则。 基于触摸的输入最适用于更大的按钮和链接，并使链接更进一步，而且没有办法将鼠标光标悬停在弹出菜单上。
2. ***解决客户端问题*-** 通过使用 CSS 和[渐进式增强功能](http://en.wikipedia.org/wiki/Progressive_enhancement)，你可以创建可适应每个浏览器运行的标记、样式和脚本。 例如，使用[CSS 3 媒体查询](http://www.w3.org/TR/2010/CR-css3-mediaqueries-20100727/)，您可以创建多列布局，在其屏幕比所选阈值更窄的设备上启用单列布局。 

    - **优势**：针对使用中的特定设备优化呈现，甚至根据所拥有的任何屏幕和输入特征，对未知未来的设备进行渲染
    - **优势**：使你能够在所有设备类型之间共享服务器端逻辑–最小程度地重复代码或工作量
    - **缺点**：移动设备与桌面设备的不同之处在于，你可能希望你的移动页面与桌面页面完全不同，并显示不同的信息。 此类变体可能效率低下，甚至不可能通过 CSS 来实现可靠地实现，尤其是考虑旧设备如何解释 CSS 规则。 这对于 CSS 3 属性尤其如此。
    - **缺点**：不支持不同设备的不同服务器端逻辑和工作流。 例如，你不能通过单独使用 CSS 来实现移动用户的简化购物车结帐工作流。
    - **缺点**：带宽使用效率低下。 您的服务器可能必须传输适用于所有可能设备的标记和样式，即使目标设备将仅使用该信息的子集。
3. ***解决服务器上的问题*–** 如果服务器知道哪个设备正在访问它（或至少具有该设备的特征，例如，其屏幕大小和输入方法，以及它是否是移动设备），则可运行不同的逻辑并输出不同的 HTML 标记。 

    - **优势：** 最大灵活性。 对于移动的服务器端逻辑大小并无限制，或者针对所需的特定于设备的布局优化了标记。
    - **优势：** 有效的带宽使用。 只需传输目标设备将要使用的标记和样式信息。
    - **缺点：** 有时会强制重复工作或编写代码（例如，使您可以创建 Web 窗体页或 MVC 视图的类似但稍有不同的副本）。 在可能的情况下，你会将公共逻辑划分为基础层或服务，但仍需要复制某些 UI 代码或标记部分，然后进行并行维护。
    - **缺点：** 设备检测并不重要。 它需要一个列表或已知设备类型的数据库及其特征（可能并非始终都是最新的），并且不保证能够精确地匹配每个传入的请求。 本文档稍后将介绍某些选项及其缺陷。

为了获得最佳结果，大多数开发人员都发现需要组合选项（2）和（3）。 使用 CSS 或 JavaScript 的客户端最适合使用次要样式差别，而在服务器端代码中最有效地实现了数据、工作流或标记的主要差异。

### <a name="this-paper-focuses-on-server-side-techniques"></a>本白皮书重点介绍服务器端技术

由于 ASP.NET Web 窗体和 MVC 主要是服务器端技术，因此此白皮书将重点介绍服务器端技术，使你可以为移动浏览器生成不同的标记和逻辑。 当然，您还可以将其与任何客户端技术（例如，CSS 3 媒体查询、渐进式增强 JavaScript）结合在一起，但这比 ASP.NET 开发的 web 设计更重要。

## <a name="browser-and-device-detection"></a>浏览器和设备检测

用于支持移动设备的所有服务器端技术的主要先决条件是了解访问者所使用的设备。 事实上，甚至比知道设备的制造商和型号，也知道设备的*特性*。 特征可能包括：

- 它是移动设备吗？
- 输入法（鼠标/键盘、触控、键盘、操纵杆、...）
- 屏幕大小（物理和以像素为单位）
- 支持的媒体和数据格式
- 等。

最好根据特征来做出决策，而不是型号，因为这样就可以更好地处理将来的设备了。

### <a name="using-aspnets-built-in-browser-detection-support"></a>使用 ASP。网络的内置浏览器检测支持

ASP.NET Web 窗体和 MVC 开发人员可以通过检查*请求 .browser*对象的属性来立即发现访问浏览器的重要特性。 例如，请参阅

- Request.Browser.IsMobileDevice
- MobileDeviceManufacturer，请求. MobileDeviceModel
- Request.Browser.ScreenPixelsWidth
- Request.Browser.SupportsXmlHttp
- ...和其他许多

在后台，ASP.NET 平台会将传入*用户代理*（UA） HTTP 标头与一组浏览器定义 XML 文件中的正则表达式匹配。 默认情况下，平台包括许多常见移动设备的定义，你可以为要识别的其他用户添加自定义浏览器定义文件。 有关更多详细信息，请参阅 MSDN 页面[ASP.NET Web 服务器控件和浏览器功能](https://msdn.microsoft.com/library/x3k2ssx2.aspx)。

### <a name="using-the-wurfl-device-database-via-51degreesmobi-foundation"></a>通过 51Degrees.mobi Foundation 使用 WURFL 设备数据库

.ASP。对于许多应用程序而言，网络的内置浏览器检测支持就足以满足以下两个主要情况：

- ***你需要识别最新的设备***（不为其手动创建浏览器定义文件）。 请注意，.NET 4 的浏览器定义文件不是最新的，不能识别 Windows Phone 7、Android 手机、Opera 移动浏览器或 Apple Ipad。
- ***你需要有关设备功能的更多详细信息***。 可能需要了解设备的输入法（例如，touch vs 小键盘）或浏览器支持的音频格式。 此信息不适用于标准浏览器定义文件。

[*无线通用资源文件*（WURFL）项目](http://wurfl.sourceforge.net/)维护有关目前正在使用的移动设备的更多最新信息和详细信息。

.NET 开发人员的优秀新闻是 ASP。网络的浏览器检测功能是可扩展的，因此可以对其进行增强，以解决这些问题。 例如，你可以将开源[*51Degrees.mobi Foundation*](https://github.com/51Degrees/dotNET-Device-Detection)库添加到你的项目。 它是一个 ASP.NET IHttpModule 或 Browser 功能提供程序（可在 Web 窗体和 MVC 应用程序上使用），可直接读取 WURFL 数据并将其挂接到 ASP。网络的内置浏览器检测机制。 安装该模块后， *Browser*会突然包含更准确和更详细的信息：它将正确识别之前提到的许多设备并列出其功能（包括其他功能，例如输入方法）。 有关更多详细信息，请参阅项目的文档。

## <a name="how-web-forms-applications-can-present-mobile-specific-pages"></a>Web 窗体应用程序如何提供特定于移动的页面

默认情况下，新的 Web 窗体应用程序在常见的移动设备上的显示方式如下：

![](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/_static/image1.png)

很显然，这两种布局看起来都不太方便移动–此页面适用于面向横向的大型监视器，不适用于面向纵向的小屏幕。 那么，您该怎么办呢？

如本文前面所述，有多种方法可为移动设备定制页面。 某些技术是基于服务器的，其他技术在客户端上运行。

### <a name="creating-a-mobile-specific-master-page"></a>创建特定于移动设备的母版页

根据你的要求，你可以为所有访问者使用相同的 Web 窗体，但可以有两个单独的母版页：一个用于桌面访问者，另一个用于移动访问者。 这使你可以灵活地更改 CSS 样式表或顶级 HTML 标记，使其适合移动设备，而不会强制复制任何页面逻辑。

这很简单。 例如，可以将以下 PreInit 处理程序添加到 Web 窗体：

[!code-csharp[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample1.cs)]

现在，在应用程序的顶层文件夹中创建名为 "Mobile" 的母版页，并在检测到移动设备时使用该母版页。 如果需要，你的移动母版页可以引用特定于移动的 CSS 样式表。 桌面访问者仍将看到您的默认母版页，而不是移动设备。

### <a name="creating-independent-mobile-specific-web-forms"></a>创建独立的移动特定 Web 窗体

为了最大限度地提高灵活性，您可以进一步了解不同设备类型的单独母版页。 可以实现两种*完全不同的 Web 窗体页*集–一组用于桌面浏览器，另一组用于移动。 如果要向移动用户提供非常不同的信息或工作流，这种方法的效果最佳。 本部分的其余部分详细介绍了这种方法。

假设已有为桌面浏览器设计的 Web 窗体应用程序，最简单的方法是在项目中创建一个名为 "Mobile" 的子文件夹，并在该文件夹中生成移动页。 您可以使用与任何其他 Web 窗体应用程序相同的方法来构造整个子站点及其自己的母版页、样式表和页面。 不一定需要为桌面站点中的*每个*页面生成等效的移动设备;你可以选择哪些功能子集对于移动访问者是有意义的。

如果需要，您的移动页面可以与您的常规页面共享常见静态资源（例如图像、JavaScript 或 CSS 文件）。 由于你的 "Mobile" 文件夹在 IIS 中承载时*不*会标记为单独的应用程序（它只是 Web 窗体页的简单子文件夹），因此它还将与桌面页面共享所有相同的配置、会话数据和其他基础结构。

> [!NOTE]
> 由于这种方法通常涉及到一些代码重复（移动页面可能与桌面页面共享某些相似之处），因此，将任何常见业务逻辑或数据访问代码分解为共享的基础层或服务非常重要。 否则，会将创建和维护应用程序的工作量加倍。

#### <a name="redirecting-mobile-visitors-to-your-mobile-pages"></a>将移动访问者重定向到你的移动页面

通常，仅在其浏览会话中（而不是在其会话*中的每*个请求中）将移动访问者重定向到移动页，这通常很方便，因为：

- 然后，你可以轻松地允许移动访问者访问你的桌面页面（如果需要），只需在母版页上放置一个指向 "桌面版本" 的链接即可。 访问者将不会重定向回移动页，因为它不再是其会话中的第一个请求。
- 它避免了干扰在站点的桌面和移动部件之间共享的任何动态资源的请求的风险（例如，如果你有一个常见的 Web 窗体，你的网站的桌面和移动部分都显示在 IFRAME 或特定的 Ajax 处理程序中）

为此，可以 **\_Start**方法将重定向逻辑放入会话中。 例如，将以下方法添加到 Global.asax.cs 文件：

[!code-csharp[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample2.cs)]

#### <a name="configuring-forms-authentication-to-respect-your-mobile-pages"></a>配置 Forms 身份验证以遵守你的移动页面

请注意，窗体身份验证在身份验证过程中和之后就可以在何处重定向访问者做出一些假设：

- 当用户需要进行身份验证时，表单身份验证会将他们重定向到桌面登录页，无论他们是桌面还是移动用户（因为它仅具有*一个*登录 URL 的概念）。 假设你想要以不同的方式为移动登录页样式，则需要增强你的桌面登录页，以便将移动用户重定向到单独的移动登录页。 例如，将以下代码添加到你的**桌面**登录页代码隐藏中： 

    [!code-csharp[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample3.cs)]
- 用户成功登录后，窗体身份验证默认情况下会将其重定向到桌面主页（因为它只有*一个*默认页面的概念）。 需要增强移动登录页面，使其在成功登录后重定向到移动主页。 例如，将以下代码添加到**移动**登录页的代码隐藏中： 

    [!code-csharp[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample4.cs)]
  
  此代码假定页面具有名为 LoginUser 的登录服务器控件，如默认项目模板中所示。

### <a name="working-with-output-caching"></a>使用输出缓存

如果使用的是输出缓存，请注意，默认情况下，桌面用户可以访问某个 URL （导致其输出被缓存），后跟移动用户，随后将收到缓存的桌面输出。 无论是按设备类型改变母版页还是按设备实现完全不同的 Web 窗体，此警告都适用。

若要避免此问题，可以指示 ASP.NET 根据访问者是否使用移动设备来改变缓存条目。 将 VaryByCustom 参数添加到页面的 OutputCache 声明中，如下所示：

[!code-aspx[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample5.aspx)]

接下来，通过将以下方法重写添加到 Global.asax.cs 文件，将*isMobileDevice*定义为自定义缓存参数：

[!code-csharp[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample6.cs)]

这将确保页面的移动访问者不接收先前由桌面访问者放入缓存的输出。

### <a name="a-working-example"></a>工作示例

若要查看这些方法的运行情况，请下载[此白皮书的代码示例](https://docs.microsoft.com/aspnet/mobile/overview)。 Web 窗体示例应用程序将移动用户自动重定向到名为 Mobile 的子文件夹中的一组特定于移动的页面。 这些页面的标记和样式更适合移动浏览器，如以下屏幕截图所示：

![](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/_static/image2.png)

有关优化移动浏览器的标记和 CSS 的更多提示，请参阅本文档后面的 "移动浏览器的样式移动页样式" 部分。

## <a name="how-aspnet-mvc-applications-can-present-mobile-specific-pages"></a>ASP.NET MVC 应用程序如何提供特定于移动的页面

由于模型-视图-控制器模式将应用程序逻辑（在控制器中）与表示逻辑（在视图中）分离开来，因此，您可以从以下任何方法中进行选择，以便在服务器端代码中处理移动支持：

1. ***为桌面和移动浏览器使用相同的控制器和视图，但根据设备类型，使用不同的 Razor 布局呈现视图。** 如果要在所有设备上显示相同的数据，但只是想要提供不同的 CSS 样式表或更改移动的一些顶级 HTML 元素，此选项效果最佳。
2. ***为桌面和移动浏览器使用相同的控制器，但根据设备类型呈现不同的视图***。 如果要显示大致相同的数据并为最终用户提供相同的工作流，则此选项最有效，但要呈现与所使用的设备不同的 HTML 标记。
3. ***为桌面和移动浏览器创建不同的区域，同时为每个 * 实现独立的控制器和视图。** 如果要显示的屏幕非常不同，其中包含不同的信息，并通过为其设备类型优化的不同工作流，则此选项的效果最佳。 这可能意味着某些代码重复，但你可以通过将常见逻辑分解为基础层或服务来最大程度地减少这种情况。

如果要采用**第一个**选项，并且仅改变每个设备类型的 Razor 布局，则非常简单。 只需修改 \_Viewstart.cshtml 文件，如下所示：

[!code-cshtml[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample7.cshtml)]

现在，你可以使用为移动设备优化的页面结构和 CSS 规则，创建名为 \_LayoutMobile 的特定于移动设备的布局。

如果要根据访问者的设备类型使用**第二个**选项呈现完全不同的视图，请参阅[Scott Hanselman 的博客文章](http://www.hanselman.com/blog/ABetterASPNETMVCMobileDeviceCapabilitiesViewEngine.aspx)。

本文的其余部分重点介绍**第三个**选项–为移动设备创建单独的控制器*和*视图–因此，你可以精确控制为移动用户提供的功能的子集。

### <a name="setting-up-a-mobile-area-within-your-aspnet-mvc-application"></a>在 ASP.NET MVC 应用程序中设置移动区域

您可以按如下方式将名为 "Mobile" 的区域添加到现有的 ASP.NET MVC 应用程序：右键单击 "解决方案资源管理器中的项目名称，然后选择" 添加à区域 "。 然后，你可以像对 ASP.NET MVC 应用程序中的任何其他区域一样添加控制器和视图。 例如，将名为 HomeController 的新控制器添加到你的移动区域，作为移动访问者的主页。

### <a name="ensuring-the-url-mobile-reaches-the-mobile-homepage"></a>确保 URL/移动到达移动主页

如果希望 URL/移动在移动区域内的 HomeController 上达到索引操作，则需要对路由配置进行两处小的更改。 首先，更新 MobileAreaRegistration 类，使 HomeController 成为移动区域中的默认控制器，如以下代码所示：

[!code-csharp[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample8.cs)]

这意味着移动主页现在位于/移动而不是/Mobile/Home，因为 "Home" 现在是移动页面的隐式默认控制器名称。

接下来，请注意，通过将第二个 HomeController 添加到你的应用程序（即移动设备，除了现有桌面一台），你将会损坏你的常规桌面主页。 它将失败，并出现错误 "*找到多个匹配名称为 ' Home ' 的控制器的类型*"。 若要解决此问题，请更新顶层路由配置（在 Global.asax.cs 中），以指定在存在不明确的情况下桌面 HomeController 应优先使用：

[!code-csharp[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample9.cs)]

现在，此错误将消失，URL http：\/\/*yoursite*/将到达桌面主页，并且 http：\/\/*yoursite*/mobile/将到达移动主页。

### <a name="redirecting-mobile-visitors-to-your-mobile-area"></a>将移动访问者重定向到你的移动区域

ASP.NET MVC 中有许多不同的扩展点，因此有许多可能的方法来注入重定向逻辑。 一个巧妙的方法是创建一个筛选器属性 [RedirectMobileDevicesToMobileArea]，如果满足以下条件，则执行重定向：

1. 这是用户会话中的第一个请求（即 IsNewSession 等于 true）
2. 请求来自移动浏览器（即 IsMobileDevice 等于 true）
3. 用户还没有在移动区域请求资源（即 URL 的*路径*部分不以/移动开头）

本白皮书附带的可下载示例包括此逻辑的实现。 它实现为从 AuthorizeAttribute 派生的授权筛选器，这意味着即使你使用的是输出缓存，也可以正常工作，即使桌面访问者首次访问某个 URL，也可能会缓存桌面输出，并将其提供给后续的移动访问者）。

作为筛选器，你可以选择将其应用于特定控制器和操作，例如，

[!code-csharp[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample10.cs)]

… 也可以将其作为 Global.asax.cs 文件中的 MVC 3*全局筛选器*应用于所有控制器和操作：

[!code-csharp[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample11.cs)]

可下载的示例还演示了如何创建此属性的子类，以重定向到移动区域中的特定位置。 例如，这意味着您可以：

- 按上面所示注册一个全局筛选器，默认情况下将移动访问者发送到移动主页。
- 还将特殊的 [RedirectMobileDevicesToMobileProductPage] 筛选器应用于 "查看产品" 操作，该操作会将移动访问者移动到所请求的任何产品页的移动版本。
- 同时将筛选器的其他特殊子类应用于特定操作，将移动访问者重定向到等效的移动页面

### <a name="configuring-forms-authentication-to-respect-your-mobile-pages"></a>配置 Forms 身份验证以遵守你的移动页面

如果使用 Forms 身份验证，应注意，当用户需要登录时，它会自动将用户重定向到单个特定的 "登录" URL，默认情况下，该 URL 为 **/Account/LogOn**。 这意味着移动用户可能会被重定向到桌面的 "登录" 操作。

若要避免此问题，请将逻辑添加到桌面的 "登录" 操作，以便它再次将移动用户重定向到移动设备上的 "登录" 操作。 如果使用的是默认的 ASP.NET MVC 应用程序模板，请按如下所示更新 AccountController 的登录操作：

[!code-csharp[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample12.cs)]

… 然后，在移动区域中名为 AccountController 的控制器上实施适当的特定于移动设备的 "登录" 操作。

### <a name="working-with-output-caching"></a>使用输出缓存

如果使用的是 [OutputCache] 筛选器，则必须根据设备类型强制缓存项发生变化。 例如，编写：

[!code-javascript[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample13.js)]

然后，将以下方法添加到 Global.asax.cs 文件：

[!code-csharp[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample14.cs)]

这将确保页面的移动访问者不接收先前由桌面访问者放入缓存的输出。

### <a name="a-working-example"></a>工作示例

若要查看这些方法的运行情况，请下载[此白皮书代码关联的示例](https://docs.microsoft.com/aspnet/mobile/overview)。 该示例包括一个 ASP.NET MVC 3 （候选发布版）应用程序，该应用程序已增强，可使用上述方法支持移动设备。

## <a name="further-guidance-and-suggestions"></a>进一步指导和建议

以下讨论适用于使用本文档中所述的技术的 Web 窗体和 MVC 开发人员。

### <a name="enhancing-your-redirection-logic-using-51degreesmobi-foundation"></a>使用 51Degrees.mobi Foundation 增强重定向逻辑

本文档中所示的重定向逻辑对于您的应用程序而言可能是足够的，但如果您需要禁用会话，或在拒绝 cookie 的移动浏览器（它们不能有会话）时，它将不起作用，因为它不知道给定的请求是否为该访问者的第一个。

您已经了解了开源 51Degrees.mobi Foundation 如何提高 ASP 的准确性。网络浏览器检测。 它还可以将移动访问者重定向到 web.config 中配置的特定位置。它可以通过存储访问者的 HTTP 标头和 IP 地址的哈希哈希的哈希值，而不依赖于 ASP.NET 会话（和 cookie），因此它知道每个请求是否是来自给定 vistor 的第一个请求。

添加到 web.config 文件的 fiftyOne 部分的以下元素会将第一个请求从检测到的移动设备重定向到页面 ~/Mobile/Default.aspx。 无论设备类型如何，都*不*会重定向对移动文件夹下的页面的任何请求。 如果移动设备在20分钟或更长时间内处于非活动状态，则将忘记该设备，并将后续请求作为新请求被视为用于重定向目的的新请求。

[!code-xml[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample15.xml)]

有关更多详细信息，请参阅[51Degrees.mobi Foundation 文档](https://github.com/51Degrees/dotNET-Device-Detection)。

> [!NOTE]
> 你*可以*在 ASP.NET MVC 应用程序上使用 51Degrees.mobi Foundation 的重定向功能，但你将需要根据普通 url 定义重定向配置，而不是按路由参数或在操作上放置 MVC 筛选器。 这是因为（在撰写本文时），51Degrees.mobi Foundation 无法识别筛选器或路由。

### <a name="disabling-transcoders-and-proxy-servers"></a>禁用转码器和代理服务器

移动网络运营商的移动 internet 方法分为两大目标：

1. 提供尽可能多的相关内容
2. 最大限度地提高可共享有限无线网络带宽的客户数量

由于大多数网页是针对大型桌面大小的屏幕和快速固定线宽带连接而设计的，因此许多运算符使用*转码器*或*代理服务器*来动态地更改 web 内容。 它们可能会修改您的 HTML 标记或 CSS，使其适合较小的屏幕（特别是对于缺少处理复杂布局的处理能力的 "功能电话"），并且它们可能会重新压缩图像（大幅降低其质量）以提高页面交付速度。

但是，如果你已完成生成移动优化的网站的版本，你可能不希望网络运营商进一步干扰。 可以在任何 ASP.NET Web 窗体中将以下行添加到页面\_Load 事件：

[!code-csharp[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample16.cs)]

或者，对于 ASP.NET MVC 控制器，可以添加以下方法替代，使其适用于该控制器上的所有操作：

[!code-csharp[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample17.cs)]

生成的 HTTP 消息通知 W3C 兼容转码器和代理不更改内容。 当然，不保证移动网络操作员会遵守此消息。

### <a name="styling-mobile-pages-for-mobile-browsers"></a>移动浏览器的样式移动页面

它不在本文档的讨论范围内，可以更详细地说明哪些类型的 HTML 标记正确工作，或者哪些 web 设计技术可最大程度地提高特定设备的可用性。 你需要找到一个非常简单的布局，针对移动大小的屏幕进行了优化，无需使用不可靠的 HTML 或 CSS 定位技巧。 但值得一提的一项重要技巧是*视区 meta 标记*。

某些新式移动浏览器在工作中显示用于桌面监视器的网页，在虚拟画布上呈现页面，也称为 "视区" （例如，在 iPhone 上，虚拟视口为980像素宽，在默认情况下，在 Opera Mobile 上为850像素宽），然后缩小结果以适应屏幕的物理像素。 然后，用户可以放大并平移该视区。 这种方法的优点在于，浏览器可让浏览器按其预期的布局来显示页面，但它也具有一些强制缩放和平移的缺点，这对用户来说不方便。 如果你正在设计 mobile，则最好设计较窄的屏幕，这样就不需要缩放或水平滚动。

通过非标准*视区*meta 标记，告诉移动浏览器视区的宽度。 例如，如果将以下内容添加到页面的 HEAD 部分，

[!code-html[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample18.html)]

… 然后，支持 smartphone 浏览器会在480像素宽的虚拟画布上设计页面。 这意味着，如果 HTML 元素以百分比的形式定义其宽度，则将根据此480像素宽度（而非默认视区宽度）来解释百分比。 因此，用户不太可能需要水平缩放和平移–大幅改善移动浏览体验。

如果希望视区宽度与设备的物理像素匹配，可以指定以下内容：

[!code-html[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample19.html)]

为了使其正常工作，您不能显式强制元素超过该宽度（例如，使用*width*特性或 CSS 属性），否则浏览器将被强制使用更大的视区，而不考虑。 另请参阅：[有关非标准视口标记的更多详细信息](https://developer.apple.com/library/safari/#documentation/AppleApplications/Reference/SafariHTMLRef/Articles/MetaTags.html)。

大多数新式智能手机支持*双重方向*：它们可以处于纵向或横向模式。 因此，不一定要对屏幕宽度（以像素为单位）做出假设。 不要假设屏幕宽度是固定的，因为用户可以在页面上重新定向其设备。

较早的 Windows Mobile 和 Blackberry 设备还可以接受页眉中的以下 meta 标记，以通知它们内容已针对移动优化，因此不应进行转换。

[!code-html[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample20.html)]

## <a name="additional-resources"></a>其他资源

有关可用于测试移动 ASP.NET web 应用程序的移动设备仿真程序和模拟器的列表，请参阅 "[模拟常用移动设备进行测试](../mobile/device-simulators.md)" 页。

## <a name="credits"></a>学分

- 主要作者： Steven Sanderson
- 审阅者/其他内容作者： James Rosewell、Mikael Söderström、Scott Hanselman、Scott Hunter
