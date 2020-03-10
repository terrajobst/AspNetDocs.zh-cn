---
uid: mvc/overview/older-versions-1/controllers-and-routing/improving-performance-with-output-caching-cs
title: 通过输出缓存（C#）提高性能 |Microsoft Docs
author: microsoft
description: 在本教程中，你将了解如何通过利用输出缓存来大幅提高 ASP.NET MVC web 应用程序的性能。 你 。
ms.author: riande
ms.date: 01/27/2009
ms.assetid: 521c9117-81cd-4d8d-9d96-0256dc7bf50f
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/improving-performance-with-output-caching-cs
msc.type: authoredcontent
ms.openlocfilehash: 548c5bea2e9cf26e0574e72d2c0ea204dbd90f9c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78486668"
---
# <a name="improving-performance-with-output-caching-c"></a>通过输出缓存提升性能 (C#)

由[Microsoft](https://github.com/microsoft)

> 在本教程中，你将了解如何通过利用输出缓存来大幅提高 ASP.NET MVC web 应用程序的性能。 了解如何缓存控制器操作返回的结果，以便每次新用户调用该操作时都不需要创建相同的内容。

本教程的目的是说明如何通过使用输出缓存来大幅提高 ASP.NET MVC 应用程序的性能。 使用输出缓存可以缓存控制器操作返回的内容。 这样，每次调用同一控制器操作时，都不需要生成相同的内容。

例如，假设 ASP.NET MVC 应用程序在名为 Index 的视图中显示数据库记录的列表。 通常，每次用户调用返回索引视图的控制器操作时，都必须通过执行数据库查询来从数据库中检索数据库记录集。

另一方面，如果你可以利用输出缓存，则每次用户调用同一控制器操作时，都可以避免执行数据库查询。 视图可以从缓存中检索，而不是从控制器操作重新生成。 使用缓存可以避免在服务器上执行冗余工作。

## <a name="enabling-output-caching"></a>启用输出缓存

可以通过将 [OutputCache] 特性添加到单个控制器操作或整个控制器类来启用输出缓存。 例如，列表1中的控制器公开一个名为 Index （）的操作。 索引（）操作的输出将缓存10秒。

**列表1– Controllers\HomeController.cs**

[!code-csharp[Main](improving-performance-with-output-caching-cs/samples/sample1.cs)]

在 ASP.NET MVC 的 Beta 版本中，输出缓存不适用于[http://www.MySite.com/](http://www.mysite.com/)的 URL。 相反，你必须输入类似[http://www.MySite.com/Home/Index](http://www.mysite.com/Home/Index)的 URL。 

在列表1中，Index （）操作的输出缓存了10秒。 如果需要，可以指定更长的缓存持续时间。 例如，如果想要将控制器操作的输出缓存一天，则可以将缓存持续时间指定为86400秒（60秒 \* 60 分钟 \* 24 小时）。

不能保证在指定的时间内缓存内容。 当内存资源较低时，缓存将开始自动逐出内容。

列表1中的主控制器返回列表2中的索引视图。 此视图没有什么特别之处。 "索引" 视图只显示当前时间（请参阅图1）。

**列表 2-Views\Home\Index.aspx**

[!code-aspx[Main](improving-performance-with-output-caching-cs/samples/sample2.aspx)]

**图1–缓存的索引视图**

![clip_image002](improving-performance-with-output-caching-cs/_static/image1.jpg)

如果通过在浏览器的地址栏中输入 URL/Home/Index 来多次调用 Index （）操作，并反复在浏览器中点击 "刷新/重新加载" 按钮，则索引视图显示的时间不会更改10秒。 因为视图被缓存，所以会显示相同的时间。

需要了解的是，将为访问应用程序的所有用户缓存相同的视图。 调用 Index （）操作的任何人都将获取索引视图的相同缓存版本。 这意味着，web 服务器为索引视图提供服务所必须执行的工作量大大减少。

清单2中的视图执行的操作确实非常简单。 视图只显示当前时间。 不过，您可以轻松地缓存一个显示一组数据库记录的视图。 在这种情况下，每次调用返回视图的控制器操作时，都不需要从数据库中检索一组数据库记录。 缓存可以减少 web 服务器和数据库服务器必须执行的工作量。

请勿在 MVC 视图中使用 &lt;% @ OutputCache%&gt; 指令的页面。 此指令从 Web 窗体世界中出血，不应在 ASP.NET MVC 应用程序中使用。

## <a name="where-content-is-cached"></a>内容缓存位置

默认情况下，当你使用 [OutputCache] 属性时，内容将缓存在三个位置： web 服务器、任何代理服务器和 web 浏览器。 您可以通过修改 [OutputCache] 属性的 Location 属性来控制缓存内容的确切位置。

可以将 "位置" 属性设置为以下值之一：

> ·随时
> 
> ·机
> 
> ·数量
> 
> ·服务
> 
> ·内容
> 
> ·ServerAndClient

默认情况下，Location 属性的值为 Any。 但是，在某些情况下，你可能只想要在浏览器或服务器上缓存。 例如，如果你要缓存为每个用户个性化的信息，则不应在服务器上缓存该信息。 如果向不同用户显示不同的信息，则应该仅在客户端上缓存该信息。

例如，列表3中的控制器公开了一个名为 GetName （）的操作，该操作将返回当前用户名。 如果插孔登录到网站并调用 GetName （）操作，则该操作将返回字符串 "Hi 插孔"。 随后，如果 Jill 登录到网站并调用 GetName （）操作，她还将获得字符串 "Hi 插座"。 在插孔最初调用控制器操作后，将在 web 服务器上为所有用户缓存此字符串。

**列表 3-Controllers\BadUserController.cs**

[!code-csharp[Main](improving-performance-with-output-caching-cs/samples/sample3.cs)]

大多数情况下，列表3中的控制器不能按您所需的方式工作。 您不希望将消息 "Jill"。

永远不应在服务器缓存中缓存个性化内容。 但是，你可能需要在浏览器缓存中缓存个性化内容以提高性能。 如果在浏览器中缓存内容，并且用户多次调用同一控制器操作，则可以从浏览器缓存而不是服务器检索内容。

列表4中修改后的控制器将缓存 GetName （）操作的输出。 但是，仅在浏览器上缓存内容，而不是在服务器上缓存内容。 这样一来，当多个用户调用 GetName （）方法时，每个人都将获得自己的用户名，而不是其他人的用户名。

**列表 4-Controllers\UserController.cs**

[!code-csharp[Main](improving-performance-with-output-caching-cs/samples/sample4.cs)]

请注意，列表4中的 [OutputCache] 属性包含一个设置为值 OutputCacheLocation 的位置属性。 [OutputCache] 属性还包括一个 NoStore 属性。 NoStore 属性用于通知代理服务器和浏览器不应存储缓存内容的永久副本。

## <a name="varying-the-output-cache"></a>改变输出缓存

在某些情况下，你可能希望具有相同内容的不同缓存版本。 例如，假设您要创建一个主/详细信息页。 母版页显示电影标题列表。 单击标题时，将获得所选电影的详细信息。

如果缓存详细信息页，则无论单击哪个电影，都将显示相同电影的详细信息。 第一个用户选择的第一个电影将显示给未来的所有用户。

可以利用 [OutputCache] 属性的 VaryByParam 属性来解决此问题。 当窗体参数或查询字符串参数不同时，此属性可让你创建具有相同内容的不同缓存版本。

例如，列表5中的控制器公开了两个名为 Master （）和 Details （）的操作。 Master （）操作返回电影标题列表，详细信息（）操作返回所选电影的详细信息。

**列表5– Controllers\MoviesController.cs**

[!code-csharp[Main](improving-performance-with-output-caching-cs/samples/sample5.cs)]

Master （）操作包含值为 "none" 的 VaryByParam 属性。 调用 Master （）操作时，将返回母版视图的相同缓存版本。 忽略任何窗体参数或查询字符串参数（参见图2）。

**图 2-/Movies/Master 视图**

![clip_image004](improving-performance-with-output-caching-cs/_static/image2.jpg)

**图 3-/Movies/Details 视图**

![clip_image006](improving-performance-with-output-caching-cs/_static/image3.jpg)

详细信息（）操作包括一个值为 "Id" 的 VaryByParam 属性。 当 Id 参数的不同值传递到控制器操作时，将生成详细信息视图的不同缓存版本。

务必要了解，使用 VaryByParam 属性会导致更多的缓存，而不是更少。 为 Id 参数的每个不同版本创建详细信息视图的不同缓存版本。

可以将 VaryByParam 属性设置为以下值：

> \* = 在窗体或查询字符串参数不同时创建不同的缓存版本。
> 
> 无 = 从不创建不同的缓存版本
> 
> 参数的分号列表，只要列表中有任何窗体或查询字符串参数发生变化，就创建不同的缓存版本

## <a name="creating-a-cache-profile"></a>创建缓存配置文件

作为通过修改 [OutputCache] 属性的属性来配置输出缓存属性的替代方法，可以在 web 配置文件（web.config）中创建缓存配置文件。 在 web 配置文件中创建缓存配置文件可提供几个重要优势。

首先，通过在 web 配置文件中配置输出缓存，可以控制控制器操作在一个中央位置缓存内容的方式。 你可以创建一个缓存配置文件，并将该配置文件应用于多个控制器或控制器操作。

其次，你可以修改 web 配置文件，而无需重新编译应用程序。 如果需要对已部署到生产环境的应用程序禁用缓存，只需修改在 web 配置文件中定义的缓存配置文件即可。 将自动检测并应用对 web 配置文件所做的任何更改。

例如，清单6中的 &lt;缓存&gt; web 配置部分定义了一个名为 Cache1Hour 的缓存配置文件。 &lt;缓存&gt; 部分必须出现在 web 配置文件的 &lt;system.web&gt; 部分中。

**清单6– web.config 的缓存部分**

[!code-xml[Main](improving-performance-with-output-caching-cs/samples/sample6.xml)]

列表7中的控制器说明了如何使用 [OutputCache] 属性将 Cache1Hour 配置文件应用到控制器操作。

**列表 7-Controllers\ProfileController.cs**

[!code-csharp[Main](improving-performance-with-output-caching-cs/samples/sample7.cs)]

如果在列表7中调用由控制器公开的索引（）操作，则将返回1小时的相同时间。

## <a name="summary"></a>摘要

输出缓存提供了一种非常简单的方法，可显著提高 ASP.NET MVC 应用程序的性能。 在本教程中，已学习如何使用 [OutputCache] 属性来缓存控制器操作的输出。 还了解了如何修改 [OutputCache] 属性（如 Duration 和 VaryByParam 属性）的属性，以修改如何缓存内容。 最后，你已了解如何在 web 配置文件中定义缓存配置文件。

> [!div class="step-by-step"]
> [上一页](understanding-action-filters-cs.md)
> [下一页](adding-dynamic-content-to-a-cached-page-cs.md)
