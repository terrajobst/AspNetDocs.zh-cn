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
# <a name="how-do-i-create-a-custom-html-helper-for-an-mvc-application"></a>如何实现：创建 MVC 应用程序的自定义 HTML 帮助程序？

作者： [Chris 像素](https://twitter.com/chrispels)

在此视频中，Chris 像素演示了如何创建在 MVC 应用程序的标准集中不可用的自定义 HtmlHelper。 首先，创建一个包含演示控制器和视图的示例 MVC 应用程序，用于测试自定义 HtmlHelper。 接下来，创建一个模块，其中包含一个公共函数，该函数是一个表示自定义 HtmlHelper 的实现的扩展方法。 自定义帮助程序用于在页中创建 `<img>` 标记，并为图像标记接收多个入站参数，包括 id、url 和替换文本。 然后，将逻辑添加到函数，以返回带有指定信息的已完成 `<img>` 标记。 然后，在 "演示" 页上使用自定义 HtmlHelper 来显示图像。 最后，自定义 HtmlHelper 将扩展为包含多个构造函数重写，这为更轻松地创建不同 `<img>` 标记提供了灵活性。

[&#9654;观看视频（18分钟）](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-create-a-custom-html-helper-for-an-mvc-application)

> [!div class="step-by-step"]
> [上一页](how-do-i-implement-view-models-to-manage-data-for-aspnet-mvc-views.md)
> [下一页](how-do-i-work-with-model-binders-in-an-mvc-application.md)
