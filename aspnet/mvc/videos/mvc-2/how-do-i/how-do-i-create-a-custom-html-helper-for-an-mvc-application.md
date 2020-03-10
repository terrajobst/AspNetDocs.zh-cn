---
uid: mvc/videos/mvc-2/how-do-i/how-do-i-create-a-custom-html-helper-for-an-mvc-application
title: 如何实现：创建 MVC 应用程序的自定义 HTML 帮助程序？ | Microsoft Docs
author: rick-anderson
description: 在此视频中，Chris 像素演示了如何创建在 MVC 应用程序的标准集中不可用的自定义 HtmlHelper。 首先，是一个示例 MVC 应用程序 。
ms.author: riande
ms.date: 12/11/2009
ms.assetid: 58b5eb15-4160-4ce2-ae70-6ba94262ea73
msc.legacyurl: /mvc/videos/mvc-2/how-do-i/how-do-i-create-a-custom-html-helper-for-an-mvc-application
msc.type: video
ms.openlocfilehash: 60953243d3038667e4f729b1394e68f0c9d7c178
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78450476"
---
# <a name="how-do-i-create-a-custom-html-helper-for-an-mvc-application"></a><span data-ttu-id="04d98-105">如何实现：创建 MVC 应用程序的自定义 HTML 帮助程序？</span><span class="sxs-lookup"><span data-stu-id="04d98-105">How Do I: Create a Custom HTML Helper for an MVC Application?</span></span>

<span data-ttu-id="04d98-106">作者： [Chris 像素](https://twitter.com/chrispels)</span><span class="sxs-lookup"><span data-stu-id="04d98-106">by [Chris Pels](https://twitter.com/chrispels)</span></span>

<span data-ttu-id="04d98-107">在此视频中，Chris 像素演示了如何创建在 MVC 应用程序的标准集中不可用的自定义 HtmlHelper。</span><span class="sxs-lookup"><span data-stu-id="04d98-107">In this video Chris Pels shows how to create a custom HtmlHelper that is not available in the standard set in an MVC application.</span></span> <span data-ttu-id="04d98-108">首先，创建一个包含演示控制器和视图的示例 MVC 应用程序，用于测试自定义 HtmlHelper。</span><span class="sxs-lookup"><span data-stu-id="04d98-108">First, a sample MVC application is created with a demo controller and view to test the custom HtmlHelper.</span></span> <span data-ttu-id="04d98-109">接下来，创建一个模块，其中包含一个公共函数，该函数是一个表示自定义 HtmlHelper 的实现的扩展方法。</span><span class="sxs-lookup"><span data-stu-id="04d98-109">Next, a module is created with a public function that is an extension method which represents the implementation of the custom HtmlHelper.</span></span> <span data-ttu-id="04d98-110">自定义帮助程序用于在页中创建 `<img>` 标记，并为图像标记接收多个入站参数，包括 id、url 和替换文本。</span><span class="sxs-lookup"><span data-stu-id="04d98-110">The custom helper is for creating `<img>` tags in a page and receives several inbound parameters including the id, url, and alt text for the image tag.</span></span> <span data-ttu-id="04d98-111">然后，将逻辑添加到函数，以返回带有指定信息的已完成 `<img>` 标记。</span><span class="sxs-lookup"><span data-stu-id="04d98-111">The logic is then added to the function for returning the completed `<img>` tag with the specified information.</span></span> <span data-ttu-id="04d98-112">然后，在 "演示" 页上使用自定义 HtmlHelper 来显示图像。</span><span class="sxs-lookup"><span data-stu-id="04d98-112">Then the custom HtmlHelper is used on the demo page to display an image.</span></span> <span data-ttu-id="04d98-113">最后，自定义 HtmlHelper 将扩展为包含多个构造函数重写，这为更轻松地创建不同 `<img>` 标记提供了灵活性。</span><span class="sxs-lookup"><span data-stu-id="04d98-113">Finally, the custom HtmlHelper is expanded to include multiple constructor overrides which provide flexibility for more easily creating different `<img>` tags.</span></span>

[<span data-ttu-id="04d98-114">&#9654;观看视频（18分钟）</span><span class="sxs-lookup"><span data-stu-id="04d98-114">&#9654; Watch video (18 minutes)</span></span>](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-create-a-custom-html-helper-for-an-mvc-application)

> [!div class="step-by-step"]
> <span data-ttu-id="04d98-115">[上一页](how-do-i-implement-view-models-to-manage-data-for-aspnet-mvc-views.md)
> [下一页](how-do-i-work-with-model-binders-in-an-mvc-application.md)</span><span class="sxs-lookup"><span data-stu-id="04d98-115">[Previous](how-do-i-implement-view-models-to-manage-data-for-aspnet-mvc-views.md)
[Next](how-do-i-work-with-model-binders-in-an-mvc-application.md)</span></span>
