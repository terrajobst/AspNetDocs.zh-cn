---
uid: mvc/overview/older-versions-1/views/using-the-tagbuilder-class-to-build-html-helpers-cs
title: 使用 TagBuilder 类生成 HTML 帮助器（C#） |Microsoft Docs
author: StephenWalther
description: Stephen Walther 介绍了名为 TagBuilder 类的 ASP.NET MVC 框架中的有用实用工具类。 你可以使用 TagBuilder 类轻松 。
ms.author: riande
ms.date: 03/02/2009
ms.assetid: 3975a52f-bd15-4edd-8f3d-1df93672515b
msc.legacyurl: /mvc/overview/older-versions-1/views/using-the-tagbuilder-class-to-build-html-helpers-cs
msc.type: authoredcontent
ms.openlocfilehash: c8eaea9932a30c744b9a69861619ce9458b5a23a
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78485606"
---
# <a name="using-the-tagbuilder-class-to-build-html-helpers-c"></a><span data-ttu-id="30ff8-104">使用 TagBuilder 类生成 HTML 帮助器（C#）</span><span class="sxs-lookup"><span data-stu-id="30ff8-104">Using the TagBuilder Class to Build HTML Helpers (C#)</span></span>

<span data-ttu-id="30ff8-105">作者： [Stephen Walther](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="30ff8-105">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

> <span data-ttu-id="30ff8-106">Stephen Walther 介绍了名为 TagBuilder 类的 ASP.NET MVC 框架中的有用实用工具类。</span><span class="sxs-lookup"><span data-stu-id="30ff8-106">Stephen Walther introduces you to a useful utility class in the ASP.NET MVC framework named the TagBuilder class.</span></span> <span data-ttu-id="30ff8-107">可以使用 TagBuilder 类轻松生成 HTML 标记。</span><span class="sxs-lookup"><span data-stu-id="30ff8-107">You can use the TagBuilder class to easily build HTML tags.</span></span>

<span data-ttu-id="30ff8-108">ASP.NET MVC 框架包含一类有用的实用工具类，该类可在生成 HTML 帮助器时使用。</span><span class="sxs-lookup"><span data-stu-id="30ff8-108">The ASP.NET MVC framework includes a useful utility class named the TagBuilder class that you can use when building HTML helpers.</span></span> <span data-ttu-id="30ff8-109">作为类的名称，TagBuilder 类使你能够轻松地生成 HTML 标记。</span><span class="sxs-lookup"><span data-stu-id="30ff8-109">The TagBuilder class, as the name of the class suggests, enables you to easily build HTML tags.</span></span> <span data-ttu-id="30ff8-110">本 brief 教程提供了 TagBuilder 类的概述，并介绍了如何在生成简单的 HTML 帮助器时使用此类，该帮助器将 HTML &lt;img&gt; 标记。</span><span class="sxs-lookup"><span data-stu-id="30ff8-110">In this brief tutorial, you are provided with an overview of the TagBuilder class and you learn how to use this class when building a simple HTML helper that renders HTML &lt;img&gt; tags.</span></span>

## <a name="overview-of-the-tagbuilder-class"></a><span data-ttu-id="30ff8-111">TagBuilder 类概述</span><span class="sxs-lookup"><span data-stu-id="30ff8-111">Overview of the TagBuilder Class</span></span>

<span data-ttu-id="30ff8-112">TagBuilder 类包含在 System.web 命名空间中。</span><span class="sxs-lookup"><span data-stu-id="30ff8-112">The TagBuilder class is contained in the System.Web.Mvc namespace.</span></span> <span data-ttu-id="30ff8-113">它有五种方法：</span><span class="sxs-lookup"><span data-stu-id="30ff8-113">It has five methods:</span></span>

- <span data-ttu-id="30ff8-114">AddCssClass （）-允许向标记添加新的*类 = ""* 特性。</span><span class="sxs-lookup"><span data-stu-id="30ff8-114">AddCssClass() - Enables you to add a new *class=""* attribute to a tag.</span></span>
- <span data-ttu-id="30ff8-115">GenerateId （）-允许向标记添加 id 属性。</span><span class="sxs-lookup"><span data-stu-id="30ff8-115">GenerateId() - Enables you to add an id attribute to a tag.</span></span> <span data-ttu-id="30ff8-116">此方法自动替换 id 中的句点（默认情况下，句点替换为下划线）</span><span class="sxs-lookup"><span data-stu-id="30ff8-116">This method automatically replaces periods in the id (by default, periods are replaced by underscores)</span></span>
- <span data-ttu-id="30ff8-117">MergeAttribute （）-允许向标记添加特性。</span><span class="sxs-lookup"><span data-stu-id="30ff8-117">MergeAttribute() - Enables you to add attributes to a tag.</span></span> <span data-ttu-id="30ff8-118">此方法有多个重载。</span><span class="sxs-lookup"><span data-stu-id="30ff8-118">There are multiple overloads of this method.</span></span>
- <span data-ttu-id="30ff8-119">SetInnerText （）-用于设置标记的内部文本。</span><span class="sxs-lookup"><span data-stu-id="30ff8-119">SetInnerText() - Enables you to set the inner text of the tag.</span></span> <span data-ttu-id="30ff8-120">内部文本自动编码。</span><span class="sxs-lookup"><span data-stu-id="30ff8-120">The inner text is HTML encode automatically.</span></span>
- <span data-ttu-id="30ff8-121">ToString （）-可用于呈现标记。</span><span class="sxs-lookup"><span data-stu-id="30ff8-121">ToString() - Enables you to render the tag.</span></span> <span data-ttu-id="30ff8-122">您可以指定是要创建普通标记、开始标记、结束标记还是自结束标记。</span><span class="sxs-lookup"><span data-stu-id="30ff8-122">You can specify whether you want to create a normal tag, a start tag, an end tag, or a self-closing tag.</span></span>

<span data-ttu-id="30ff8-123">TagBuilder 类具有四个重要属性：</span><span class="sxs-lookup"><span data-stu-id="30ff8-123">The TagBuilder class has four important properties:</span></span>

- <span data-ttu-id="30ff8-124">特性-表示标记的所有属性。</span><span class="sxs-lookup"><span data-stu-id="30ff8-124">Attributes - Represents all of the attributes of the tag.</span></span>
- <span data-ttu-id="30ff8-125">IdAttributeDotReplacement-表示 GenerateId （）方法用来替换句号的字符（默认值为下划线）。</span><span class="sxs-lookup"><span data-stu-id="30ff8-125">IdAttributeDotReplacement - Represents the character used by the GenerateId() method to replace periods (the default is an underscore).</span></span>
- <span data-ttu-id="30ff8-126">InnerHTML-表示标记的内部内容。</span><span class="sxs-lookup"><span data-stu-id="30ff8-126">InnerHTML - Represents the inner contents of the tag.</span></span> <span data-ttu-id="30ff8-127">将字符串分配给此属性不*会*对字符串进行 HTML 编码。</span><span class="sxs-lookup"><span data-stu-id="30ff8-127">Assigning a string to this property *does not* HTML encode the string.</span></span>
- <span data-ttu-id="30ff8-128">TagName-表示标记的名称。</span><span class="sxs-lookup"><span data-stu-id="30ff8-128">TagName - Represents the name of the tag.</span></span>

<span data-ttu-id="30ff8-129">这些方法和属性为您生成一个 HTML 标记所需的所有基本方法和属性。</span><span class="sxs-lookup"><span data-stu-id="30ff8-129">These methods and properties give you all of the basic methods and properties that you need to build up an HTML tag.</span></span> <span data-ttu-id="30ff8-130">你实际上不需要使用 TagBuilder 类。</span><span class="sxs-lookup"><span data-stu-id="30ff8-130">You don't really need to use the TagBuilder class.</span></span> <span data-ttu-id="30ff8-131">可以改用 StringBuilder 类。</span><span class="sxs-lookup"><span data-stu-id="30ff8-131">You could use a StringBuilder class instead.</span></span> <span data-ttu-id="30ff8-132">但是，TagBuilder 类使你的生活变得更加简单。</span><span class="sxs-lookup"><span data-stu-id="30ff8-132">However, the TagBuilder class makes your life a little easier.</span></span>

## <a name="creating-an-image-html-helper"></a><span data-ttu-id="30ff8-133">创建图像 HTML 帮助器</span><span class="sxs-lookup"><span data-stu-id="30ff8-133">Creating an Image HTML Helper</span></span>

<span data-ttu-id="30ff8-134">当你创建 TagBuilder 类的实例时，会将你想要生成的标记的名称传递到 TagBuilder 构造函数。</span><span class="sxs-lookup"><span data-stu-id="30ff8-134">When you create an instance of the TagBuilder class, you pass the name of the tag that you want to build to the TagBuilder constructor.</span></span> <span data-ttu-id="30ff8-135">接下来，可以调用 AddCssClass 和 MergeAttribute （）方法等方法来修改标记的属性。</span><span class="sxs-lookup"><span data-stu-id="30ff8-135">Next, you can call methods like the AddCssClass and MergeAttribute() methods to modify the attributes of the tag.</span></span> <span data-ttu-id="30ff8-136">最后，调用 ToString （）方法以呈现标记。</span><span class="sxs-lookup"><span data-stu-id="30ff8-136">Finally, you call the ToString() method to render the tag.</span></span>

<span data-ttu-id="30ff8-137">例如，列表1包含图像 HTML 帮助器。</span><span class="sxs-lookup"><span data-stu-id="30ff8-137">For example, Listing 1 contains an Image HTML helper.</span></span> <span data-ttu-id="30ff8-138">图像帮助器在内部使用表示 HTML &lt;img&gt; 标记的 TagBuilder 来实现。</span><span class="sxs-lookup"><span data-stu-id="30ff8-138">The Image helper is implemented internally with a TagBuilder that represents an HTML &lt;img&gt; tag.</span></span>

<span data-ttu-id="30ff8-139">**列表 1-Helpers\ImageHelper.cs**</span><span class="sxs-lookup"><span data-stu-id="30ff8-139">**Listing 1 - Helpers\ImageHelper.cs**</span></span>

[!code-csharp[Main](using-the-tagbuilder-class-to-build-html-helpers-cs/samples/sample1.cs)]

<span data-ttu-id="30ff8-140">列表1中的类包含两个名为 Image 的静态重载方法。</span><span class="sxs-lookup"><span data-stu-id="30ff8-140">The class in Listing 1 contains two static overloaded methods named Image.</span></span> <span data-ttu-id="30ff8-141">调用 Image （）方法时，可以传递表示一组 HTML 特性的对象。</span><span class="sxs-lookup"><span data-stu-id="30ff8-141">When you call the Image() method, you can pass an object which represents a set of HTML attributes or not.</span></span>

<span data-ttu-id="30ff8-142">请注意如何使用 MergeAttribute （）方法将 TagBuilder 属性（如 src 属性）添加到 TagBuilder。</span><span class="sxs-lookup"><span data-stu-id="30ff8-142">Notice how the TagBuilder.MergeAttribute() method is used to add individual attributes such as the src attribute to the TagBuilder.</span></span> <span data-ttu-id="30ff8-143">另外请注意，TagBuilder MergeAttributes （）方法如何用于将属性集合添加到 TagBuilder。</span><span class="sxs-lookup"><span data-stu-id="30ff8-143">Notice, furthermore, how the TagBuilder.MergeAttributes() method is used to add a collection of attributes to the TagBuilder.</span></span> <span data-ttu-id="30ff8-144">MergeAttributes （）方法接受&lt;string、object&gt; 参数的字典。</span><span class="sxs-lookup"><span data-stu-id="30ff8-144">The MergeAttributes() method accepts a Dictionary&lt;string,object&gt; parameter.</span></span> <span data-ttu-id="30ff8-145">RouteValueDictionary 类用于将表示属性集合的对象转换为字典&lt;string、Object&gt;。</span><span class="sxs-lookup"><span data-stu-id="30ff8-145">The RouteValueDictionary class is used to convert the Object representing the collection of attributes into a Dictionary&lt;string,object&gt;.</span></span>

<span data-ttu-id="30ff8-146">创建图像帮助器后，可以像使用任何其他标准 HTML 帮助器一样在 ASP.NET MVC 视图中使用帮助器。</span><span class="sxs-lookup"><span data-stu-id="30ff8-146">After you create the Image helper, you can use the helper in your ASP.NET MVC views just like any of the other standard HTML helpers.</span></span> <span data-ttu-id="30ff8-147">清单2中的视图使用图像帮助器来显示同一次 Xbox 的同一图像（参见图1）。</span><span class="sxs-lookup"><span data-stu-id="30ff8-147">The view in Listing 2 uses the Image helper to display the same image of an Xbox twice (see Figure 1).</span></span> <span data-ttu-id="30ff8-148">Image （）帮助器在带有和不带 HTML 特性集合的情况下调用。</span><span class="sxs-lookup"><span data-stu-id="30ff8-148">The Image() helper is called both with and without an HTML attribute collection.</span></span>

<span data-ttu-id="30ff8-149">**列表 2-Home\Index.aspx**</span><span class="sxs-lookup"><span data-stu-id="30ff8-149">**Listing 2 - Home\Index.aspx**</span></span>

[!code-aspx[Main](using-the-tagbuilder-class-to-build-html-helpers-cs/samples/sample2.aspx)]

<span data-ttu-id="30ff8-150">[!["新建项目" 对话框](using-the-tagbuilder-class-to-build-html-helpers-cs/_static/image1.jpg)](using-the-tagbuilder-class-to-build-html-helpers-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="30ff8-150">[![The New Project dialog box](using-the-tagbuilder-class-to-build-html-helpers-cs/_static/image1.jpg)](using-the-tagbuilder-class-to-build-html-helpers-cs/_static/image1.png)</span></span>

<span data-ttu-id="30ff8-151">**图 01**：使用图像帮助器（[单击以查看完全大小的图像](using-the-tagbuilder-class-to-build-html-helpers-cs/_static/image2.png)）</span><span class="sxs-lookup"><span data-stu-id="30ff8-151">**Figure 01**: Using the Image helper([Click to view full-size image](using-the-tagbuilder-class-to-build-html-helpers-cs/_static/image2.png))</span></span>

<span data-ttu-id="30ff8-152">请注意，您必须导入与 "索引 .aspx" 视图顶部的图像帮助器关联的命名空间。</span><span class="sxs-lookup"><span data-stu-id="30ff8-152">Notice that you must import the namespace associated with the Image helper at the top of the Index.aspx view.</span></span> <span data-ttu-id="30ff8-153">将通过以下指令导入帮助器：</span><span class="sxs-lookup"><span data-stu-id="30ff8-153">The helper is imported with the following directive:</span></span>

[!code-aspx[Main](using-the-tagbuilder-class-to-build-html-helpers-cs/samples/sample3.aspx)]

> [!div class="step-by-step"]
> <span data-ttu-id="30ff8-154">[上一页](creating-custom-html-helpers-cs.md)
> [下一页](creating-page-layouts-with-view-master-pages-cs.md)</span><span class="sxs-lookup"><span data-stu-id="30ff8-154">[Previous](creating-custom-html-helpers-cs.md)
[Next](creating-page-layouts-with-view-master-pages-cs.md)</span></span>
