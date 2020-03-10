---
uid: web-pages/overview/routing/creating-readable-urls-in-aspnet-web-pages-sites
title: 在 ASP.NET 网页（Razor）站点中创建可读 Url |Microsoft Docs
author: Rick-Anderson
description: 本文介绍如何在 ASP.NET 网页（Razor）网站中进行路由，以及如何使用它来利用更具可读性且更适用于 SEO 的 Url。 你将 。
ms.author: riande
ms.date: 02/17/2014
ms.assetid: a8aac1ac-89de-4415-afe0-97a41c6423d2
msc.legacyurl: /web-pages/overview/routing/creating-readable-urls-in-aspnet-web-pages-sites
msc.type: authoredcontent
ms.openlocfilehash: 832db8e144cab730f16c78f67c12feb9b7c92c7c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78509906"
---
# <a name="creating-readable-urls-in-aspnet-web-pages-razor-sites"></a>在 ASP.NET 网页（Razor）站点中创建可读 Url

作者： [Tom FitzMacken](https://github.com/tfitzmac)

> 本文介绍如何在 ASP.NET 网页（Razor）网站中进行路由，以及如何使用它来利用更具可读性且更适用于 SEO 的 Url。
> 
> 学习内容：
> 
> - ASP.NET 如何使用路由来使你可以使用可读性更强的可搜索 Url。
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>本教程中使用的软件版本
> 
> 
> - ASP.NET 网页（Razor）3
>   
> 
> 本教程还适用于 ASP.NET 网页2。

## <a name="about-routing"></a>关于路由

站点中页面的 Url 可能会影响站点的工作方式。 &quot;友好&quot; 的 URL 可以使用户更轻松地使用站点。 它还可帮助网站的搜索引擎优化（SEO）。 ASP.NET 网站包括自动使用友好 Url 的功能。

使用 ASP.NET 可以创建有意义的 Url，用于描述用户操作，而不是仅指向服务器上的文件。 请考虑以下用于虚构博客的 Url：

- `http://www.contoso.com/Blog/blog.cshtml?categories=hardware`
- `http://www.contoso.com//Blog/blog.cshtml?startdate=2009-11-01&enddate=2009-11-30`

将这些 Url 与以下 Url 进行比较：

- `http://www.contoso.com/Blog/categories/hardware/`
- `http://www.contoso.com/Blog/2009/November`

在第一对中，用户必须知道该博客是使用 "*博客 ...* " 页显示的，然后必须构造一个获取正确类别或日期范围的查询字符串。 第二组示例更易于理解和创建。

第一个示例的 Url 也直接指向特定文件（即*博客*）。 如果由于某种原因，博客被移到服务器上的另一个文件夹，或者重新编写博客以使用不同的页面，则链接会出错。 第二组 Url 未指向特定页面，因此即使在博客实现或位置发生更改时，Url 仍然有效。

在 ASP.NET 网页中，可以创建更友好的 Url，如上述示例中的 Url，因为 ASP.NET 使用*路由*。 路由创建从 URL 到可满足请求的页面的逻辑映射。 因为映射是逻辑的（而不是物理映射），所以路由为你定义站点的 Url 提供了极大的灵活性。

## <a name="how-routing-works"></a>路由的工作原理

当 ASP.NET 处理请求时，它会读取 URL 以确定如何路由该请求。 ASP.NET 尝试将 URL 的各个段与磁盘上的文件进行匹配，从左至右。 如果存在匹配项，则 URL 中剩余的任何内容将作为*路径信息*传递到页面。

假设有人使用此 URL 发出请求：

`http://www.contoso.com/a/b/c`

搜索如下所示：

1. 是否存在路径和名称为 */a/b/c.cshtml*的文件？ 如果是这样，请运行该页并向其传递无信息。 否则...
2. 是否存在路径和名称为 */a/b.cshtml*的文件？ 如果是这样，请运行该页并向其传递 `c` 值。 否则 。
3. 是否存在路径和名称为 */a.cshtml*的文件？ 如果是这样，请运行该页并向其传递 `b/c` 值。

如果搜索在其指定文件夹中找不到与 *.* # 文件完全匹配的项，ASP.NET 将继续依次查找这些文件：

1. */a/b/c/default.cshtml* （无路径信息）。
2. */a/b/c/index.cshtml* （无路径信息）。

> [!NOTE]
> 为清楚起见，对特定页面的请求（即包含 *.* # 文件扩展名的请求）的工作方式与预期的一样。 例如 `http://www.contoso.com/a/b.cshtml` 的请求会正常运行第*b.* 页。

在页面中，可以通过页面的 `UrlData` 属性获取路径信息，该属性是一个词典。 假设你有一个名为*ViewCustomers*的文件，并且你的站点获取此请求：

`http://mysite.com/myWebSite/ViewCustomers/1000`

如以上规则所述，请求将发送到你的页面。 在该页中，您可以使用如下所示的代码来获取和显示路径信息（在本例中，值 &quot;1000&quot;）：

[!code-html[Main](creating-readable-urls-in-aspnet-web-pages-sites/samples/sample1.html)]

> [!NOTE]
> 由于路由不涉及完整的文件名，因此，如果页面的名称相同但文件扩展名不同（例如， *m y*和*m y*），则可能存在歧义。 为了避免出现路由问题，最好确保站点中的页面的名称仅在扩展名上不同。

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a>其他资源

[WebMatrix-适用于 SEO 的 url、urldata.base 和路由](http://www.mikesdotnetting.com/Article/165/WebMatrix-URLs-UrlData-and-Routing-for-SEO)。 Mike Brind 的此博客文章提供了有关路由在 ASP.NET 网页中的工作原理的更多详细信息。
