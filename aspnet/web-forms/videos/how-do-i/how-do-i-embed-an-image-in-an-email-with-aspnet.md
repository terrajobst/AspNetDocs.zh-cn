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
# <a name="how-do-i-embed-an-image-in-an-email-with-aspnet"></a><span data-ttu-id="d606d-104">[如何实现：]使用 ASP.NET 在电子邮件中嵌入图像</span><span class="sxs-lookup"><span data-stu-id="d606d-104">[How Do I:] Embed an Image in an Email with ASP.NET</span></span>

<span data-ttu-id="d606d-105">作者： [Chris 像素](https://twitter.com/chrispels)</span><span class="sxs-lookup"><span data-stu-id="d606d-105">by [Chris Pels](https://twitter.com/chrispels)</span></span>

<span data-ttu-id="d606d-106">丽丽像素演示如何使用 ASP.NET 在电子邮件中嵌入图像。</span><span class="sxs-lookup"><span data-stu-id="d606d-106">Chris Pels shows how to embed an image in an email with ASP.NET.</span></span> <span data-ttu-id="d606d-107">他创建了一个 web 窗体（其中包含指向、发件人、主题和正文的字段），使用 AlternateView 类创建电子邮件的文本和 HTML 版本，将图像存储在 LinkedResource 类实例中，并将其嵌入 HTML AlternateView。</span><span class="sxs-lookup"><span data-stu-id="d606d-107">He creates a web form (with fields for To, From, Subject, and Body), uses the AlternateView class to create text and HTML versions of an email, stores an image in a LinkedResource class instance, embeds it in the HTML AlternateView.</span></span> <span data-ttu-id="d606d-108">然后，他将两个版本都添加到 Send-mailmessage 对象，并在启用了 HTML 接收功能的情况下，将电子邮件发送两次，并以纯文本形式发送电子邮件。</span><span class="sxs-lookup"><span data-stu-id="d606d-108">He then adds both versions to the MailMessage object and sends the email twice, first with HTML-receiving capabilities enabled and then as text-only.</span></span> <span data-ttu-id="d606d-109">这两封电子邮件都出现在 Outlook 中。</span><span class="sxs-lookup"><span data-stu-id="d606d-109">Both email messages appear in Outlook.</span></span> <span data-ttu-id="d606d-110">HTML 版本显示嵌入的图像;文本版本不会。</span><span class="sxs-lookup"><span data-stu-id="d606d-110">The HTML version shows the embedded image; the text version does not.</span></span>

[<span data-ttu-id="d606d-111">&#9654;观看视频（19分钟）</span><span class="sxs-lookup"><span data-stu-id="d606d-111">&#9654; Watch video (19 minutes)</span></span>](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-embed-an-image-in-an-email-with-aspnet)
