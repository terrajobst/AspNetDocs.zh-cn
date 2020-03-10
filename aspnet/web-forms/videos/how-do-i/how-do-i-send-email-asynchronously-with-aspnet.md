---
uid: web-forms/videos/how-do-i/how-do-i-send-email-asynchronously-with-aspnet
title: '[如何实现：]通过 ASP.NET 异步发送电子邮件 |Microsoft Docs'
author: rick-anderson
description: 在此视频中，Chris 像素演示了如何在 ASP.NET 中使用系统 .Net. Mail 类发送异步电子邮件。 首先，请参阅如何配置 web si 。
ms.author: riande
ms.date: 09/24/2008
ms.assetid: 77a5c8fa-ebb2-426d-b56b-a5a98a46b516
msc.legacyurl: /web-forms/videos/how-do-i/how-do-i-send-email-asynchronously-with-aspnet
msc.type: video
ms.openlocfilehash: ea29823446cc1339003160bd3e945bde1af42473
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78516170"
---
# <a name="how-do-i-send-email-asynchronously-with-aspnet"></a><span data-ttu-id="f72a1-104">[如何实现：]通过 ASP.NET 异步发送电子邮件</span><span class="sxs-lookup"><span data-stu-id="f72a1-104">[How Do I:] Send Email Asynchronously with ASP.NET</span></span>

<span data-ttu-id="f72a1-105">作者： [Chris 像素](https://twitter.com/chrispels)</span><span class="sxs-lookup"><span data-stu-id="f72a1-105">by [Chris Pels](https://twitter.com/chrispels)</span></span>

<span data-ttu-id="f72a1-106">在此视频中，Chris 像素演示了如何在 ASP.NET 中使用系统 .Net. Mail 类发送异步电子邮件。</span><span class="sxs-lookup"><span data-stu-id="f72a1-106">In this video, Chris Pels shows how to use the System.Net.Mail classes in ASP.NET to send an asynchronous email message.</span></span> <span data-ttu-id="f72a1-107">首先，请参阅如何将网站配置为使用 web.config 文件中的 &lt;mailSettings&gt; 元素发送电子邮件。</span><span class="sxs-lookup"><span data-stu-id="f72a1-107">First, see how to configure a web site to send email using the &lt;mailSettings&gt; element in the web.config file.</span></span> <span data-ttu-id="f72a1-108">接下来，创建一个用于输入电子邮件信息的简单用户界面。</span><span class="sxs-lookup"><span data-stu-id="f72a1-108">Next, create a simple user interface for entering email information.</span></span> <span data-ttu-id="f72a1-109">然后了解如何创建，使用 Send-mailmessage 类在页的代码隐藏中创建电子邮件。</span><span class="sxs-lookup"><span data-stu-id="f72a1-109">Then learn how to create use the MailMessage class to create an email message in the code behind for the page.</span></span> <span data-ttu-id="f72a1-110">作为该过程的一部分，请在发送电子邮件后，为异步回调创建事件处理程序。</span><span class="sxs-lookup"><span data-stu-id="f72a1-110">As part of that process create an event handler for the asynchronous callback following the sending of the email.</span></span> <span data-ttu-id="f72a1-111">在事件处理程序中，请参阅如何使用 AsynchCompletedEventArgs 类的实例，该类提供有关电子邮件发送过程的信息。</span><span class="sxs-lookup"><span data-stu-id="f72a1-111">In the event handler see how to use the instance of the AsynchCompletedEventArgs class which provides information about the email sending process.</span></span> <span data-ttu-id="f72a1-112">最后，按照调试模式中的步骤异步发送测试电子邮件，并查看从该流程接收的实际电子邮件。</span><span class="sxs-lookup"><span data-stu-id="f72a1-112">Finally, send a test email asynchronously, following the steps in the debug mode, and view the actual email received from the process.</span></span>

[<span data-ttu-id="f72a1-113">&#9654;观看视频（18分钟）</span><span class="sxs-lookup"><span data-stu-id="f72a1-113">&#9654; Watch video (18 minutes)</span></span>](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-send-email-asynchronously-with-aspnet)
