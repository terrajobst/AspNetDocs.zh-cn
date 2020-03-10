---
uid: web-forms/videos/how-do-i/how-do-i-control-the-caching-of-an-aspnet-page-based-upon-custom-information
title: '[如何实现：]基于自定义信息控制 ASP.NET 页面的缓存 |Microsoft Docs'
author: rick-anderson
description: 在此视频中，Chris 像素演示了如何控制基于自定义信息缓存 ASP.NET 页面的条件。 将创建一个示例页，然后创建
ms.author: riande
ms.date: 02/19/2009
ms.assetid: f230c316-1313-4b8f-967c-62f9684fe378
msc.legacyurl: /web-forms/videos/how-do-i/how-do-i-control-the-caching-of-an-aspnet-page-based-upon-custom-information
msc.type: video
ms.openlocfilehash: 676bc8f234a6e517104d07fd58a0ff14aec73e69
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78506768"
---
# <a name="how-do-i-control-the-caching-of-an-aspnet-page-based-upon-custom-information"></a>[如何实现：]基于自定义信息控制 ASP.NET 页面的缓存

作者： [Chris 像素](https://twitter.com/chrispels)

在此视频中，Chris 像素演示了如何控制基于自定义信息缓存 ASP.NET 页面的条件。 将创建一个示例页，然后将 OutputCache 指令与包含自定义值的 VaryByCustom 属性一起使用。 接下来，在 global.asax 模块中重写 GetVaryCustomByString （）方法，该模块提供自定义属性的处理。 在该方法中，将返回一个字符串，该字符串唯一标识页面的缓存版本。 最后，还讨论了如何使用自定义值进行缓存，以多种方式用于网站。

[&#9654;观看视频（12分钟）](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-control-the-caching-of-an-aspnet-page-based-upon-custom-information)
