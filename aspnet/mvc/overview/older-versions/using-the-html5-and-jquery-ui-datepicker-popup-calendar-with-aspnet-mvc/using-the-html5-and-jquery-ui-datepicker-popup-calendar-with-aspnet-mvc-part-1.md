---
uid: mvc/overview/older-versions/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-1
title: 将 HTML5 和 jQuery UI Datepicker 快捷日历与 ASP.NET MVC-第1部分一起使用 |Microsoft Docs
author: Rick-Anderson
description: 本教程将指导你了解如何在 ASP.NET MV ... 中使用编辑器模板、显示模板和 jQuery UI datepicker 快捷日历
ms.author: riande
ms.date: 08/29/2011
ms.assetid: c23d27f7-b0cf-44f2-8445-fb69e045c674
msc.legacyurl: /mvc/overview/older-versions/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-1
msc.type: authoredcontent
ms.openlocfilehash: c1c2380f24c72f6aabaaacaf975e95288a384ff1
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457617"
---
# <a name="using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc---part-1"></a><span data-ttu-id="2a994-103">将 HTML5 和 jQuery UI Datepicker 快捷日历与 ASP.NET MVC 一起使用-第1部分</span><span class="sxs-lookup"><span data-stu-id="2a994-103">Using the HTML5 and jQuery UI Datepicker Popup Calendar with ASP.NET MVC - Part 1</span></span>

<span data-ttu-id="2a994-104">作者： [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="2a994-104">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

> <span data-ttu-id="2a994-105">本教程将指导你了解如何在 ASP.NET MVC Web 应用程序中使用编辑器模板、显示模板和 jQuery UI datepicker 快捷日历。</span><span class="sxs-lookup"><span data-stu-id="2a994-105">This tutorial will teach you the basics of how to work with editor templates, display templates, and the jQuery UI datepicker popup calendar in an ASP.NET MVC Web application.</span></span>

<span data-ttu-id="2a994-106">本教程将指导你了解如何在 ASP.NET MVC Web 应用程序中使用编辑器模板、显示模板和 jQuery [UI datepicker 快捷日历](http://plugins.jquery.com/project/datepicker)。</span><span class="sxs-lookup"><span data-stu-id="2a994-106">This tutorial will teach you the basics of how to work with editor templates, display templates, and the jQuery [UI datepicker popup calendar](http://plugins.jquery.com/project/datepicker) in an ASP.NET MVC Web application.</span></span> <span data-ttu-id="2a994-107">对于本教程，你可以使用 Microsoft Visual Web Developer 2010 Express Service Pack 1 （&quot;Visual Web Developer&quot;），该版本是 Microsoft Visual Studio 的免费版本，或者你可以使用 Visual Studio 2010 SP1 （如果已有）。</span><span class="sxs-lookup"><span data-stu-id="2a994-107">For this tutorial, you can use Microsoft Visual Web Developer 2010 Express Service Pack 1 (&quot;Visual Web Developer&quot;), which is a free version of Microsoft Visual Studio, or you can use Visual Studio 2010 SP1 if you already have that.</span></span>

<span data-ttu-id="2a994-108">在开始之前，请确保已安装下列必备组件。</span><span class="sxs-lookup"><span data-stu-id="2a994-108">Before you start, make sure you've installed the prerequisites listed below.</span></span> <span data-ttu-id="2a994-109">可以通过单击以下链接安装所有这些[程序： Web 平台安装程序](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)。</span><span class="sxs-lookup"><span data-stu-id="2a994-109">You can install all of them by clicking the following link: [Web Platform Installer](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack).</span></span> <span data-ttu-id="2a994-110">或者，你可以使用以下链接单独安装所需的软件：</span><span class="sxs-lookup"><span data-stu-id="2a994-110">Alternatively, you can individually install the required software using the following links:</span></span>

- [<span data-ttu-id="2a994-111">Visual Studio Web Developer Express SP1 必备组件</span><span class="sxs-lookup"><span data-stu-id="2a994-111">Visual Studio Web Developer Express SP1 prerequisites</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
- [<span data-ttu-id="2a994-112">ASP.NET MVC 3 工具更新</span><span class="sxs-lookup"><span data-stu-id="2a994-112">ASP.NET MVC 3 Tools Update</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
- <span data-ttu-id="2a994-113">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)（运行时 + 工具支持）</span><span class="sxs-lookup"><span data-stu-id="2a994-113">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(runtime + tools support)</span></span>

<span data-ttu-id="2a994-114">如果你使用的是 Visual Studio 2010 而不是 Visual Web Developer，请通过单击以下链接安装必备组件： [Visual studio 2010 必备组件](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)。</span><span class="sxs-lookup"><span data-stu-id="2a994-114">If you're using Visual Studio 2010 instead of Visual Web Developer, install the prerequisites by clicking the following link: [Visual Studio 2010 prerequisites](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack).</span></span>

<span data-ttu-id="2a994-115">本教程假定你已完成[使用 mvc 3 的入门](../getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)教程，或者你熟悉 ASP.NET MVC 开发。</span><span class="sxs-lookup"><span data-stu-id="2a994-115">This tutorial assumes you have completed the [Getting Started with MVC 3](../getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) tutorial or that you're familiar with ASP.NET MVC development.</span></span> <span data-ttu-id="2a994-116">本教程从[入门与 MVC 3](../getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)教程中的已完成项目开始。</span><span class="sxs-lookup"><span data-stu-id="2a994-116">This tutorial starts with the completed project from the [Getting Started with MVC 3](../getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) tutorial.</span></span>

<span data-ttu-id="2a994-117">本教程使用 C# 代码。</span><span class="sxs-lookup"><span data-stu-id="2a994-117">This tutorial shows code in C#.</span></span> <span data-ttu-id="2a994-118">但是，[初学者项目](https://archive.msdn.microsoft.com/Project/Download/FileDownload.aspx?ProjectName=aspnetmvcsamples&amp;DownloadId=15800)和已完成项目在 Visual Basic 中也可用。</span><span class="sxs-lookup"><span data-stu-id="2a994-118">However, the [starter project](https://archive.msdn.microsoft.com/Project/Download/FileDownload.aspx?ProjectName=aspnetmvcsamples&amp;DownloadId=15800) and completed project are also available in Visual Basic.</span></span>

<span data-ttu-id="2a994-119">本主题提供了包含C#和 Visual Basic 源代码的 Visual Studio 项目：[下载](https://archive.msdn.microsoft.com/Project/Download/FileDownload.aspx?ProjectName=aspnetmvcsamples&amp;DownloadId=15800)。</span><span class="sxs-lookup"><span data-stu-id="2a994-119">A Visual Studio project with C# and Visual Basic source code is available to accompany this topic: [Download](https://archive.msdn.microsoft.com/Project/Download/FileDownload.aspx?ProjectName=aspnetmvcsamples&amp;DownloadId=15800).</span></span>

### <a name="what-youll-build"></a><span data-ttu-id="2a994-120">所需操作</span><span class="sxs-lookup"><span data-stu-id="2a994-120">What You'll Build</span></span>

<span data-ttu-id="2a994-121">将模板（具体而言，是编辑和显示模板）添加到在[入门](../getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)中创建的简单电影列表应用程序。</span><span class="sxs-lookup"><span data-stu-id="2a994-121">You'll add templates (specifically, edit and display templates) to the simple movie-listing application that was created in the [Getting Started with MVC 3](../getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) tutorial.</span></span> <span data-ttu-id="2a994-122">还将添加[JQUERY UI datepicker](http://jqueryui.com/demos/datepicker/)快捷方式日历，以简化输入日期的过程。</span><span class="sxs-lookup"><span data-stu-id="2a994-122">You will also add a [jQuery UI datepicker](http://jqueryui.com/demos/datepicker/) popup calendar to simplify the process of entering dates.</span></span> <span data-ttu-id="2a994-123">以下屏幕截图显示了已修改的应用程序，其中显示了 jQuery UI datepicker 快捷日历。</span><span class="sxs-lookup"><span data-stu-id="2a994-123">The following screenshot shows the modified application with the jQuery UI datepicker popup calendar displayed.</span></span>

![已完成 jQuery](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-1/_static/image1.png)

### <a name="skills-youll-learn"></a><span data-ttu-id="2a994-125">将要学到的技能</span><span class="sxs-lookup"><span data-stu-id="2a994-125">Skills You'll Learn</span></span>

<span data-ttu-id="2a994-126">学习内容：</span><span class="sxs-lookup"><span data-stu-id="2a994-126">Here's what you'll learn:</span></span>

- <span data-ttu-id="2a994-127">如何使用[DataAnnotations](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx)命名空间中的属性来控制显示数据的格式以及处于编辑模式时的数据格式。</span><span class="sxs-lookup"><span data-stu-id="2a994-127">How to use attributes from the [DataAnnotations](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx) namespace to control the format of data when it's displayed and when it's in edit mode.</span></span>
- <span data-ttu-id="2a994-128">如何创建模板（编辑和显示模板）来控制数据的格式。</span><span class="sxs-lookup"><span data-stu-id="2a994-128">How to create templates (edit and display templates) to control the formatting of data.</span></span>
- <span data-ttu-id="2a994-129">如何添加[JQUERY UI datepicker](http://jqueryui.com/demos/datepicker/)作为一种输入日期字段的方式。</span><span class="sxs-lookup"><span data-stu-id="2a994-129">How to add the [jQuery UI datepicker](http://jqueryui.com/demos/datepicker/) as a way to enter date fields.</span></span>

### <a name="getting-started"></a><span data-ttu-id="2a994-130">入门</span><span class="sxs-lookup"><span data-stu-id="2a994-130">Getting Started</span></span>

<span data-ttu-id="2a994-131">如果尚未从初学者项目获得电影列表应用程序，请下载：</span><span class="sxs-lookup"><span data-stu-id="2a994-131">If you don't already have the movie-listing application from the starter project, download it:</span></span> 

* <span data-ttu-id="2a994-132">[下载](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098)。</span><span class="sxs-lookup"><span data-stu-id="2a994-132">[Download](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098).</span></span>
* <span data-ttu-id="2a994-133">在 Windows 资源管理器中，右键单击*MvcMovie*文件，然后选择 "**属性**"。</span><span class="sxs-lookup"><span data-stu-id="2a994-133">In Windows Explorer, right-click the *MvcMovie.zip* file and select **Properties**.</span></span> 
* <span data-ttu-id="2a994-134">在 " **MvcMovie 属性**" 对话框中，选择 "**取消阻止**"。</span><span class="sxs-lookup"><span data-stu-id="2a994-134">In the **MvcMovie.zip Properties** dialog box, select **Unblock**.</span></span> <span data-ttu-id="2a994-135">（取消阻止后，尝试使用从 Web 下载的 *.zip* 文件时，不再显示安全警告。）</span><span class="sxs-lookup"><span data-stu-id="2a994-135">(Unblocking prevents a security warning that occurs when you try to use a *.zip* file that you've downloaded from the web.)</span></span>

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-1/_static/image2.png)

<span data-ttu-id="2a994-136">右键单击 " *MvcMovie* " 文件，然后选择 "**全部提取**" 来解压缩该文件。</span><span class="sxs-lookup"><span data-stu-id="2a994-136">Right-click the *MvcMovie.zip* file and select **Extract All** to unzip the file.</span></span> <span data-ttu-id="2a994-137">在 Visual Web Developer 或 Visual Studio 2010 中，打开*MvcMovieCS\_TU*文件。</span><span class="sxs-lookup"><span data-stu-id="2a994-137">In Visual Web Developer or Visual Studio 2010, open the *MvcMovieCS\_TU.sln* file.</span></span>

<span data-ttu-id="2a994-138">在**解决方案资源管理器**中，双击 " *Views\Shared _Layout\\* " 以将其打开。</span><span class="sxs-lookup"><span data-stu-id="2a994-138">In **Solution Explorer**, double-click the *Views\Shared\\_Layout.cshtml* to open it.</span></span> <span data-ttu-id="2a994-139">将 `H1` 标题从**MVC 电影应用**更改为**Movie jQuery**。</span><span class="sxs-lookup"><span data-stu-id="2a994-139">Change the `H1` header from **MVC Movie App** to **Movie jQuery**.</span></span> <span data-ttu-id="2a994-140">按 CTRL + F5 运行应用程序，然后单击 "**主页**" 选项卡，该选项卡将转到电影控制器的 `Index` 方法。</span><span class="sxs-lookup"><span data-stu-id="2a994-140">Press CTRL+F5 to run the application and click the **Home** tab, which takes you to the `Index` method of the movie controller.</span></span> <span data-ttu-id="2a994-141">若要试用该应用程序，请选择其中一个影片的**编辑**链接和**详细信息**链接。</span><span class="sxs-lookup"><span data-stu-id="2a994-141">To try out the application, select the **Edit** link and the **Details** link for one of the movies.</span></span> <span data-ttu-id="2a994-142">请注意，在 "索引"、"编辑" 和 "详细信息" 视图中，发布日期和价格格式良好：</span><span class="sxs-lookup"><span data-stu-id="2a994-142">Notice that in the Index, Edit, and Details views, the release date and price are nicely formatted:</span></span>

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-1/_static/image3.png)

<span data-ttu-id="2a994-143">日期和价格的格式设置是对 `Movie` 类的属性使用[DisplayFormat](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx)特性的结果。</span><span class="sxs-lookup"><span data-stu-id="2a994-143">The formatting for the date and the price is the result of using the [DisplayFormat](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx) attribute on properties of the `Movie` class.</span></span>

<span data-ttu-id="2a994-144">打开*Movie.cs*文件并注释掉 `ReleaseDate` 和 `Price` 属性上的 `DisplayFormat` 属性。</span><span class="sxs-lookup"><span data-stu-id="2a994-144">Open the *Movie.cs* file and comment out the `DisplayFormat` attribute on the `ReleaseDate` and `Price` properties.</span></span> <span data-ttu-id="2a994-145">生成的 `Movie` 类如下所示：</span><span class="sxs-lookup"><span data-stu-id="2a994-145">The resulting `Movie` class looks like this:</span></span>

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-1/samples/sample1.cs)]

<span data-ttu-id="2a994-146">再次按 CTRL + F5 运行应用程序，并选择 "**主页**" 选项卡以查看电影列表。</span><span class="sxs-lookup"><span data-stu-id="2a994-146">Press CTRL+F5 again to run the application and select the **Home** tab to view the movie list.</span></span> <span data-ttu-id="2a994-147">此时，发布日期会显示日期和时间，并且 "价格" 字段将不再显示货币符号。</span><span class="sxs-lookup"><span data-stu-id="2a994-147">This time the release date shows the date and time, and the price field no longer shows the currency symbol.</span></span> <span data-ttu-id="2a994-148">你在 `Movie` 类中的更改已撤消你先前看到的精美格式，但你稍后会解决此问题。</span><span class="sxs-lookup"><span data-stu-id="2a994-148">Your change in the `Movie` class has undone the nice formatting that you saw earlier, but you'll fix that in a moment.</span></span>

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-1/_static/image4.png)

### <a name="using-the-dataannotations-datatype-attribute-to-specify-the-data-type"></a><span data-ttu-id="2a994-149">使用 DataAnnotations DataType 特性指定数据类型</span><span class="sxs-lookup"><span data-stu-id="2a994-149">Using the DataAnnotations DataType Attribute to Specify the Data Type</span></span>

<span data-ttu-id="2a994-150">使用 `Date` 枚举，将 `ReleaseDate` 属性的已注释掉 `DisplayFormat` 特性替换为[DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx)特性。</span><span class="sxs-lookup"><span data-stu-id="2a994-150">Replace the commented-out `DisplayFormat` attribute for the `ReleaseDate` property with the [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) attribute, using the `Date` enumeration.</span></span> <span data-ttu-id="2a994-151">再次将 `Price` 属性的 `DisplayFormat` 特性替换为[DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx)特性，这一次使用 `Currency` 枚举。</span><span class="sxs-lookup"><span data-stu-id="2a994-151">Replace the `DisplayFormat` attribute for the `Price` property with the [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) attribute again, this time using the `Currency` enumeration.</span></span> <span data-ttu-id="2a994-152">完成后的代码如下所示：</span><span class="sxs-lookup"><span data-stu-id="2a994-152">This is what the completed code looks like:</span></span>

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-1/samples/sample2.cs)]

<span data-ttu-id="2a994-153">运行应用程序。</span><span class="sxs-lookup"><span data-stu-id="2a994-153">Run the application.</span></span> <span data-ttu-id="2a994-154">现在，发布日期和价格属性的格式正确（即，使用适当的日期和货币格式）。</span><span class="sxs-lookup"><span data-stu-id="2a994-154">Now the release date and the price properties are formatted correctly (that is, using appropriate date and currency formats).</span></span> <span data-ttu-id="2a994-155">[DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx)特性提供内置 ASP.NET MVC 模板的类型元数据，以便字段以正确格式呈现。</span><span class="sxs-lookup"><span data-stu-id="2a994-155">The [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) attribute provides type metadata for the built-in ASP.NET MVC templates so that the fields render in the correct format.</span></span> <span data-ttu-id="2a994-156">使用 `DataType` 特性优于最初位于代码中的 `DisplayFormat` 属性，因为 `DataType` 特性使模型更整洁，更灵活地用于国际化。</span><span class="sxs-lookup"><span data-stu-id="2a994-156">Using the `DataType` attribute is preferable to using the `DisplayFormat` attribute that was originally in the code, because the `DataType` attribute makes the model cleaner and more flexible for purposes like internationalization.</span></span>

<span data-ttu-id="2a994-157">在下一部分中，你将了解如何创建自定义模板来显示日期字段。</span><span class="sxs-lookup"><span data-stu-id="2a994-157">In the next section you'll see how to make custom templates to display date fields.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="2a994-158">Next</span><span class="sxs-lookup"><span data-stu-id="2a994-158">Next</span></span>](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2.md)
