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
# <a name="how-do-i-use-the-reponsefilter-property-to-replace-html-in-an-aspnet-page"></a>[如何实现：]在 ASP.NET 页中使用响应. Filter 属性替换 HTML

作者： [Chris 像素](https://twitter.com/chrispels)

在此视频中，Chris 像素演示了如何使用响应. Filter 属性来截获和更改发送到页面的 HTML。 首先，用一些简单的文本创建一个示例页。 然后，将创建一个自定义流类，作为要发送到用户浏览器的当前流的替换流。 在该自定义流类中，将从流中检索页面的内容，对其进行更改，然后将其写出到响应流。 在此自定义流类中，Write 方法自定义为替换基本响应流中的 HTML，从而更改发送到用户浏览器的内容。 最后，新的 stream 类将分配到\_Load 事件页中的 "筛选器" 属性，从而提供用于更改页面内容的机制。

[&#9654;观看视频（13分钟）](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-use-the-reponsefilter-property-to-replace-html-in-an-aspnet-page)
