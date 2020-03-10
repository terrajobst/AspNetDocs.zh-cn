---
uid: web-forms/videos/how-do-i/how-do-i-embed-an-image-in-an-email-with-aspnet
title: '[如何实现：]使用 ASP.NET 在电子邮件中嵌入图像 |Microsoft Docs'
author: rick-anderson
description: 丽丽像素演示如何使用 ASP.NET 在电子邮件中嵌入图像。 他创建了一个 web 窗体（其中包含指向、发件人、主题和正文的字段），使用 AlternateView 。
ms.author: riande
ms.date: 11/06/2008
ms.assetid: 424788ac-0a43-4063-99e7-db5aa4c66a9d
msc.legacyurl: /web-forms/videos/how-do-i/how-do-i-embed-an-image-in-an-email-with-aspnet
msc.type: video
ms.openlocfilehash: fce565c7746acaa10ef1cf68e3ed98e052cca43e
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78458102"
---
# <a name="how-do-i-embed-an-image-in-an-email-with-aspnet"></a>[如何实现：]使用 ASP.NET 在电子邮件中嵌入图像

作者： [Chris 像素](https://twitter.com/chrispels)

丽丽像素演示如何使用 ASP.NET 在电子邮件中嵌入图像。 他创建了一个 web 窗体（其中包含指向、发件人、主题和正文的字段），使用 AlternateView 类创建电子邮件的文本和 HTML 版本，将图像存储在 LinkedResource 类实例中，并将其嵌入 HTML AlternateView。 然后，他将两个版本都添加到 Send-mailmessage 对象，并在启用了 HTML 接收功能的情况下，将电子邮件发送两次，并以纯文本形式发送电子邮件。 这两封电子邮件都出现在 Outlook 中。 HTML 版本显示嵌入的图像;文本版本不会。

[&#9654;观看视频（19分钟）](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-embed-an-image-in-an-email-with-aspnet)
