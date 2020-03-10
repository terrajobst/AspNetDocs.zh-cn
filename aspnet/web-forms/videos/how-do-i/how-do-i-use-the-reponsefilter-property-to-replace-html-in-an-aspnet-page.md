---
uid: web-forms/videos/how-do-i/how-do-i-use-the-reponsefilter-property-to-replace-html-in-an-aspnet-page
title: '[如何实现：]在 ASP.NET 页中使用响应. Filter 属性替换 HTML |Microsoft Docs'
author: rick-anderson
description: 在此视频中，Chris 像素演示了如何使用响应. Filter 属性来截获和更改发送到页面的 HTML。 首先，创建一个示例页 。
ms.author: riande
ms.date: 01/29/2009
ms.assetid: 3e5ae74a-9798-47d8-a2b3-0d8ad42dd4bc
msc.legacyurl: /web-forms/videos/how-do-i/how-do-i-use-the-reponsefilter-property-to-replace-html-in-an-aspnet-page
msc.type: video
ms.openlocfilehash: 2ebd9162f81f5270c92c6b8d55e2d2dad4660701
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78487994"
---
# <a name="how-do-i-use-the-reponsefilter-property-to-replace-html-in-an-aspnet-page"></a><span data-ttu-id="1202a-104">[如何实现：]在 ASP.NET 页中使用响应. Filter 属性替换 HTML</span><span class="sxs-lookup"><span data-stu-id="1202a-104">[How Do I:] Use the Reponse.Filter Property to Replace HTML in an ASP.NET Page</span></span>

<span data-ttu-id="1202a-105">作者： [Chris 像素](https://twitter.com/chrispels)</span><span class="sxs-lookup"><span data-stu-id="1202a-105">by [Chris Pels](https://twitter.com/chrispels)</span></span>

<span data-ttu-id="1202a-106">在此视频中，Chris 像素演示了如何使用响应. Filter 属性来截获和更改发送到页面的 HTML。</span><span class="sxs-lookup"><span data-stu-id="1202a-106">In this video Chris Pels shows how to use the Reponse.Filter property to intercept and alter the HTML being sent to a page.</span></span> <span data-ttu-id="1202a-107">首先，用一些简单的文本创建一个示例页。</span><span class="sxs-lookup"><span data-stu-id="1202a-107">First, a sample page is created with some simple text.</span></span> <span data-ttu-id="1202a-108">然后，将创建一个自定义流类，作为要发送到用户浏览器的当前流的替换流。</span><span class="sxs-lookup"><span data-stu-id="1202a-108">Then, a custom Stream class is created which serves as the replacement stream for the current stream being sent to the user's browser.</span></span> <span data-ttu-id="1202a-109">在该自定义流类中，将从流中检索页面的内容，对其进行更改，然后将其写出到响应流。</span><span class="sxs-lookup"><span data-stu-id="1202a-109">In that custom stream class the contents of the page are retrieved from the stream, altered, and then written out to the response stream.</span></span> <span data-ttu-id="1202a-110">在此自定义流类中，Write 方法自定义为替换基本响应流中的 HTML，从而更改发送到用户浏览器的内容。</span><span class="sxs-lookup"><span data-stu-id="1202a-110">In this custom Stream class the Write method is customized to replace the HTML in the base Response stream, thereby altering what is sent to the user's browser.</span></span> <span data-ttu-id="1202a-111">最后，新的 stream 类将分配到\_Load 事件页中的 "筛选器" 属性，从而提供用于更改页面内容的机制。</span><span class="sxs-lookup"><span data-stu-id="1202a-111">Finally, the new stream class is assigned to the Response.Filter property in the Page\_Load event, thereby, providing the mechanism for altering the page content.</span></span>

[<span data-ttu-id="1202a-112">&#9654;观看视频（13分钟）</span><span class="sxs-lookup"><span data-stu-id="1202a-112">&#9654; Watch video (13 minutes)</span></span>](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-use-the-reponsefilter-property-to-replace-html-in-an-aspnet-page)
