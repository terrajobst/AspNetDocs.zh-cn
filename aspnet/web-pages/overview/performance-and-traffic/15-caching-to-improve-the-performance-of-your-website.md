---
uid: web-pages/overview/performance-and-traffic/15-caching-to-improve-the-performance-of-your-website
title: 缓存 ASP.NET 网页（Razor）站点中的数据以获得更好的性能 |Microsoft Docs
author: Rick-Anderson
description: 你可以通过让网站存储（即缓存）来加速你的网站，通常需要相当长的时间来检索或处理 。
ms.author: riande
ms.date: 02/14/2014
ms.assetid: 961e525b-7700-469e-8a68-d7010b6fb68c
msc.legacyurl: /web-pages/overview/performance-and-traffic/15-caching-to-improve-the-performance-of-your-website
msc.type: authoredcontent
ms.openlocfilehash: 01796d3ca699a6af5d9162b22a926551435c2040
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78521156"
---
# <a name="caching-data-in-an-aspnet-web-pages-razor-site-for-better-performance"></a>缓存 ASP.NET 网页（Razor）站点中的数据以获得更好的性能

作者： [Tom FitzMacken](https://github.com/tfitzmac)

> 本文介绍如何使用 helper 来缓存信息，以便在 ASP.NET 网页（Razor）网站中提高性能。 你可以通过使你的网站存储&#8212;起来来加速你的网站&#8212; ，并缓存通常会花费相当长的时间来检索或处理的数据结果，并且不经常更改。
> 
> **你将学习的内容：** 
> 
> - 如何使用缓存来提高网站的响应能力。
> 
> 下面是本文中介绍的 ASP.NET 功能：
> 
> - `WebCache` 帮助程序。
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>本教程中使用的软件版本
> 
> 
> - ASP.NET 网页（Razor）3
>   
> 
> 本教程还适用于 ASP.NET 网页2。

每次从网站请求页面时，web 服务器都必须执行一些工作才能完成请求。 对于某些页面，服务器可能需要执行耗时较长的任务，例如从数据库中检索数据。 即使这些任务不需要花费很长时间，如果您的站点遇到大量的流量，导致 web 服务器执行复杂或慢任务的一系列单独请求也可能会增加许多工作。 这最终会影响站点的性能。

在这种情况下改善网站性能的一种方法是缓存数据。 如果你的站点获取相同信息的重复请求，并且无需为每个人员修改信息，并且不需要对其进行重新计算，则可以提取一次数据，然后存储结果。 下次收到请求时，只需将其从缓存中取出。

通常情况下，您将缓存不经常更改的信息。 将信息放入缓存中时，它存储在 web 服务器的内存中。 可以指定应缓存的时间长度（以秒为单位）。 缓存期到期时，会自动从缓存中删除信息。

> [!NOTE]
> 缓存中的条目可能会因为其过期而被删除。 例如，web 服务器的内存可能会很低，并且它可以回收内存的一种方法是从缓存中引发条目。 您将看到，即使您已将信息放入缓存，也必须检查以确保它在需要时仍然存在。

假设您的网站具有显示当前温度和天气预报的页面。 若要获取此类信息，你可以向外部服务发送请求。 由于此信息不会有很多变化（例如，在两个小时的时间段内），并且由于外部调用需要时间和带宽，因此它非常适合用于缓存。

## <a name="adding-caching-to-a-page"></a>向页面添加缓存

ASP.NET 包含一个 `WebCache` 帮助程序，使你可以轻松地向网站添加缓存并将数据添加到缓存中。 在此过程中，您将创建一个缓存当前时间的页面。 这并不是实际的示例，因为当前时间是经常更改的内容，而这种情况并不是很复杂的计算。 不过，这是一个很好的方法来说明缓存的操作方式。

1. 将名为*WebCache*的新页面添加到网站。
2. 将以下代码和标记添加到页面：

    [!code-cshtml[Main](15-caching-to-improve-the-performance-of-your-website/samples/sample1.cshtml)]

    缓存数据时，可以使用一个名称将其放入缓存，此名称在整个网站中是唯一的。 在这种情况下，将使用名为 `CachedTime`的缓存条目。 这是代码示例中所示的 `cacheItemKey`。

    代码首先读取 `CachedTime` 缓存条目。 如果返回值（即，如果缓存项不为 null），则代码仅将时间变量的值设置为缓存数据。

    但是，如果缓存项不存在（也就是说，它为 null），则代码将设置时间值，将其添加到缓存中，并将过期值设置为1分钟。 一分钟后，将放弃缓存条目。 （缓存中某个项目的默认过期值为20分钟。）命令 `WebCache.Set(cacheItemKey, time, 1, false)` 显示了如何将当前时间值添加到缓存，并将其有效期设置为1分钟。 将*slidingExpiration*参数设置为 `false` 意味着在每次请求过期时间时，不会对其进行续订。 它将在其最初添加到缓存后的一分钟后过期。 如果将此值设置为 `true` 则每次从缓存请求该值时，将重置 "1 分钟过期时间"。

    此代码演示缓存数据时应始终使用的模式。 在从缓存中获取内容之前，始终首先检查 `WebCache.Get` 方法是否返回了 null。 请记住，缓存条目可能已过期，或者出于其他某种原因可能已被删除，因此任何给定的条目永远都不能保证位于缓存中。
3. 在浏览器中运行*WebCache* 。 （请确保在运行之前在 "**文件**" 工作区中选择了该页面。）第一次请求页面时，时间数据不在缓存中，代码必须将时间值添加到缓存中。

    ![cache-1](15-caching-to-improve-the-performance-of-your-website/_static/image1.jpg)
4. 在浏览器中刷新*WebCache* 。 这次，时间数据位于缓存中。 请注意，自上次查看页面后的时间未更改。

    ![cache-2](15-caching-to-improve-the-performance-of-your-website/_static/image2.jpg)
5. 等待一分钟以便清空缓存，然后刷新页面。 该页再次指示在缓存中找不到时间数据，并将更新的时间添加到缓存中。

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a>其他资源

- [在图表中显示数据](https://go.microsoft.com/fwlink/?LinkId=202895)
- [WEBCACHE API 参考](https://msdn.microsoft.com/library/system.web.helpers.webcache(v=vs.99).aspx)（MSDN）
