---
uid: web-pages/overview/performance-and-traffic/bundling-and-minifying-assets-in-an-aspnet-web-pages-razor-site
title: 捆绑和缩小资产在 ASP.NET Web Pages (Razor) 站点 |Microsoft Docs
author: microsoft
description: 捆绑和缩小种方法来更快地使您的网站。 绑定可让你组合多个 JavaScript (.js) 文件或多个级联样式表 （...
ms.author: riande
ms.date: 06/21/2012
ms.assetid: 8906f1e9-4b66-4a03-8e8a-9e9debf8ed91
msc.legacyurl: /web-pages/overview/performance-and-traffic/bundling-and-minifying-assets-in-an-aspnet-web-pages-razor-site
msc.type: authoredcontent
ms.openlocfilehash: 5e42111ad71ec65581e56c73822e23ecd5fcbd58
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/09/2019
ms.locfileid: "59400446"
---
# <a name="bundling-and-minifying-assets-in-an-aspnet-web-pages-razor-site"></a><span data-ttu-id="27b52-104">在 ASP.NET 网页 (Razor) 中绑定和缩小资产</span><span class="sxs-lookup"><span data-stu-id="27b52-104">Bundling and Minifying Assets in an ASP.NET Web Pages (Razor) Site</span></span>

<span data-ttu-id="27b52-105">by [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="27b52-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="27b52-106">捆绑和缩小种方法来更快地使您的网站。</span><span class="sxs-lookup"><span data-stu-id="27b52-106">Bundling and minification are ways to make your site faster.</span></span> <span data-ttu-id="27b52-107">绑定可让你组合多个 JavaScript (*.js*) 文件或多个级联样式表 (*.css*) 文件，以便它们可以作为一个单元，而不是一次一个地下载。</span><span class="sxs-lookup"><span data-stu-id="27b52-107">Bundling lets you combine multiple JavaScript (*.js*) files or multiple cascading style sheet (*.css*) files so that they can be downloaded as a unit, rather than one at a time.</span></span> <span data-ttu-id="27b52-108">缩小加大出空白并执行其他类型的压缩，以使可能发生的已下载的文件尽可能小。</span><span class="sxs-lookup"><span data-stu-id="27b52-108">Minification squeezes out whitespace and performs other types of compression to make the downloaded files as small a possible.</span></span>
> 
> > [!NOTE]
> > <span data-ttu-id="27b52-109">ASP.NET Web Pages 2 RC 版不支持绑定和缩减，因为尚不可用在 Microsoft WebMatrix 中包含所需的元素的包。</span><span class="sxs-lookup"><span data-stu-id="27b52-109">The RC release of ASP.NET Web Pages 2 does not support bundling and minification because the package that contains the required elements is not yet available in Microsoft WebMatrix.</span></span> <span data-ttu-id="27b52-110">对于由此引起的不便，我们深表歉意。</span><span class="sxs-lookup"><span data-stu-id="27b52-110">We apologize for this inconvenience.</span></span> <span data-ttu-id="27b52-111">包应在 ASP.NET Web Pages 2 和 WebMatrix 2 的最终版本中不可用。</span><span class="sxs-lookup"><span data-stu-id="27b52-111">The package is expected to be available in the final release of ASP.NET Web Pages 2 and WebMatrix 2.</span></span>
