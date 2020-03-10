---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-8
title: 第8部分：最终页面、异常处理和结论 |Microsoft Docs
author: JoeStagner
description: 本教程系列详细介绍了生成 Tailspin Spyworks 示例应用程序所需执行的所有步骤。 第8部分添加联系人页，"关于" 页和 "异常"。
ms.author: riande
ms.date: 07/21/2010
ms.assetid: 5aeadf8f-39f3-4f07-a78f-1c310c64fb23
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-8
msc.type: authoredcontent
ms.openlocfilehash: 707dc9d87ae324a7897c971a451e40bc54c96cb3
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78474338"
---
# <a name="part-8-final-pages-exception-handling-and-conclusion"></a><span data-ttu-id="2fee2-104">第8部分：最终页面、异常处理和结论</span><span class="sxs-lookup"><span data-stu-id="2fee2-104">Part 8: Final Pages, Exception Handling, and Conclusion</span></span>

<span data-ttu-id="2fee2-105">作者： [Joe Stagner](https://github.com/JoeStagner)</span><span class="sxs-lookup"><span data-stu-id="2fee2-105">by [Joe Stagner](https://github.com/JoeStagner)</span></span>

> <span data-ttu-id="2fee2-106">Tailspin Spyworks 演示了创建适用于 .NET 平台的功能强大的可缩放应用程序是多么简单。</span><span class="sxs-lookup"><span data-stu-id="2fee2-106">Tailspin Spyworks demonstrates how extraordinarily simple it is to create powerful, scalable applications for the .NET platform.</span></span> <span data-ttu-id="2fee2-107">其中展示了如何使用 ASP.NET 4 中的优秀新功能构建在线商店，包括购物、结帐和管理。</span><span class="sxs-lookup"><span data-stu-id="2fee2-107">It shows off how to use the great new features in ASP.NET 4 to build an online store, including shopping, checkout, and administration.</span></span>
> 
> <span data-ttu-id="2fee2-108">本教程系列详细介绍了生成 Tailspin Spyworks 示例应用程序所需执行的所有步骤。</span><span class="sxs-lookup"><span data-stu-id="2fee2-108">This tutorial series details all of the steps taken to build the Tailspin Spyworks sample application.</span></span> <span data-ttu-id="2fee2-109">第8部分添加联系人页、关于页和异常处理。</span><span class="sxs-lookup"><span data-stu-id="2fee2-109">Part 8 adds a contact page, about page, and exception handling.</span></span> <span data-ttu-id="2fee2-110">这是序列的结论。</span><span class="sxs-lookup"><span data-stu-id="2fee2-110">This is the conclusion of the series.</span></span>

## <a id="_Toc260221680"></a><span data-ttu-id="2fee2-111">联系人页（从 ASP.NET 发送电子邮件）</span><span class="sxs-lookup"><span data-stu-id="2fee2-111">Contact Page (Sending email from ASP.NET)</span></span>

<span data-ttu-id="2fee2-112">创建名为 ContactUs 的新页</span><span class="sxs-lookup"><span data-stu-id="2fee2-112">Create a new page named ContactUs.aspx</span></span>

<span data-ttu-id="2fee2-113">使用设计器创建以下窗体，以特殊说明将 ToolkitScriptManager 和 Editor 控件包含在 AjaxControlToolkit 中。</span><span class="sxs-lookup"><span data-stu-id="2fee2-113">Using the designer, create the following form taking special note to include the ToolkitScriptManager and the Editor control from the AjaxControlToolkit.</span></span> <span data-ttu-id="2fee2-114">.</span><span class="sxs-lookup"><span data-stu-id="2fee2-114">.</span></span>

![](tailspin-spyworks-part-8/_static/image1.jpg)

<span data-ttu-id="2fee2-115">双击 "提交" 按钮以在代码隐藏文件中生成一个 click 事件处理程序，并实现一个方法以将联系人信息作为电子邮件发送。</span><span class="sxs-lookup"><span data-stu-id="2fee2-115">Double click on the "Submit" button to generate a click event handler in the code behind file and implement a method to send the contact information as an email.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-8/samples/sample1.cs)]

<span data-ttu-id="2fee2-116">此代码要求 web.config 文件包含配置节中的条目，该条目指定用于发送邮件的 SMTP 服务器。</span><span class="sxs-lookup"><span data-stu-id="2fee2-116">This code requires that your web.config file contain an entry in the configuration section that specifies the SMTP server to use for sending mail.</span></span>

[!code-xml[Main](tailspin-spyworks-part-8/samples/sample2.xml)]

## <a id="_Toc260221681"></a><span data-ttu-id="2fee2-117">关于页面</span><span class="sxs-lookup"><span data-stu-id="2fee2-117">About Page</span></span>

<span data-ttu-id="2fee2-118">创建一个名为 "AboutUs" 的页面，并添加所需的任何内容。</span><span class="sxs-lookup"><span data-stu-id="2fee2-118">Create a page named AboutUs.aspx and add whatever content you like.</span></span>

## <a id="_Toc260221682"></a><span data-ttu-id="2fee2-119">全局异常处理程序</span><span class="sxs-lookup"><span data-stu-id="2fee2-119">Global Exception Handler</span></span>

<span data-ttu-id="2fee2-120">最后，在整个应用程序中，我们引发了异常，并且在某些情况下，冷还会导致在 web 应用程序中出现未经处理的异常。</span><span class="sxs-lookup"><span data-stu-id="2fee2-120">Lastly, throughout the application we have thrown exceptions and there are unforeseen circumstances that cold also cause unhandled exceptions in our web application.</span></span>

<span data-ttu-id="2fee2-121">我们永远不希望向网站访问者显示未处理的异常。</span><span class="sxs-lookup"><span data-stu-id="2fee2-121">We never want an unhandled exception to be displayed to a web site visitor.</span></span>

![](tailspin-spyworks-part-8/_static/image2.jpg)

<span data-ttu-id="2fee2-122">除了造成严重的用户体验，未经处理的异常也可能是安全问题。</span><span class="sxs-lookup"><span data-stu-id="2fee2-122">Apart from being a terrible user experience unhandled exceptions can also be a security problem.</span></span>

<span data-ttu-id="2fee2-123">为了解决此问题，我们将实现一个全局异常处理程序。</span><span class="sxs-lookup"><span data-stu-id="2fee2-123">To solve this problem we will implement a global exception handler.</span></span>

<span data-ttu-id="2fee2-124">为此，请打开 global.asax 文件，并记下预先生成的事件处理程序。</span><span class="sxs-lookup"><span data-stu-id="2fee2-124">To do this, open the Global.asax file and note the following pre-generated event handler.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-8/samples/sample3.cs)]

<span data-ttu-id="2fee2-125">添加代码以实现应用程序\_错误处理程序，如下所示。</span><span class="sxs-lookup"><span data-stu-id="2fee2-125">Add code to implement the Application\_Error handler as follows.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-8/samples/sample4.cs)]

<span data-ttu-id="2fee2-126">然后向解决方案添加一个名为 "Error" 的页，并添加此标记段。</span><span class="sxs-lookup"><span data-stu-id="2fee2-126">Then add a page named Error.aspx to the solution and add this markup snippet.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-8/samples/sample5.aspx)]

<span data-ttu-id="2fee2-127">现在，在页面\_Load 事件处理程序从 Request 对象中提取错误消息。</span><span class="sxs-lookup"><span data-stu-id="2fee2-127">Now in the Page\_Load event handler extract the error messages from the Request Object.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-8/samples/sample6.cs)]

## <a id="_Toc260221683"></a><span data-ttu-id="2fee2-128">结论</span><span class="sxs-lookup"><span data-stu-id="2fee2-128">Conclusion</span></span>

<span data-ttu-id="2fee2-129">我们已看到，ASP.NET WebForms 可让你轻松地创建具有数据库访问权限、成员资格、AJAX 等的复杂网站。</span><span class="sxs-lookup"><span data-stu-id="2fee2-129">We've seen that ASP.NET WebForms makes it easy to create a sophisticated website with database access, membership, AJAX, etc.</span></span> <span data-ttu-id="2fee2-130">速度非常快。</span><span class="sxs-lookup"><span data-stu-id="2fee2-130">pretty quickly.</span></span>

<span data-ttu-id="2fee2-131">希望本教程提供了开始构建自己的 ASP.NET WebForms 应用程序所需的工具！</span><span class="sxs-lookup"><span data-stu-id="2fee2-131">Hopefully this tutorial has given you the tools you need to get started building your own ASP.NET WebForms applications!</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="2fee2-132">上一页</span><span class="sxs-lookup"><span data-stu-id="2fee2-132">Previous</span></span>](tailspin-spyworks-part-7.md)
