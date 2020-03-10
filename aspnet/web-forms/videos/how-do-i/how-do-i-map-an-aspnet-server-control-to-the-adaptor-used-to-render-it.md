---
uid: web-forms/videos/how-do-i/how-do-i-map-an-aspnet-server-control-to-the-adaptor-used-to-render-it
title: '[如何实现：]将 ASP.NET 服务器控件映射到用于呈现该控件的适配器 |Microsoft Docs'
author: rick-anderson
description: 在此视频中，Chris 像素将演示如何使用控制适配器为 ASP.NET 服务器控件提供不同的呈现，而无需实际更改 c 。
ms.author: riande
ms.date: 06/19/2008
ms.assetid: d4b498ef-8e1c-4fa2-9c35-1f32f20bb9b7
msc.legacyurl: /web-forms/videos/how-do-i/how-do-i-map-an-aspnet-server-control-to-the-adaptor-used-to-render-it
msc.type: video
ms.openlocfilehash: 757c90fac3345b448513fb4c7cd946a3d10f3f89
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78473420"
---
# <a name="how-do-i-map-an-aspnet-server-control-to-the-adaptor-used-to-render-it"></a>[如何实现：]将 ASP.NET 服务器控件映射到用于呈现该控件的适配器

作者： [Chris 像素](https://twitter.com/chrispels)

在此视频中，Chris 像素将演示如何使用控制适配器为 ASP.NET 服务器控件提供不同的呈现，而无需实际更改控件本身。 在此视频中，ASP.NET BulletList 控件将改编为使用 DIV 元素（而不是传统的 UL 元素）以水平方式显示每个列表项。 首先，请参阅如何创建继承 WebControlAdaptor 的类，然后实现代码以呈现新的列表格式。 接下来，了解如何将新的控件适配器映射到 .browser 定义文件中的 ASP.NET 服务器控件。 然后，请参阅如何在网站中的页面上使用新控制适配器。 最后，了解如何将控件适配器与所有浏览器或特定类型的浏览器相关联。

[&#9654;观看视频（23分钟）](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-map-an-aspnet-server-control-to-the-adaptor-used-to-render-it)
