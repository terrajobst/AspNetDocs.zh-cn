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
# <a name="using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc---part-1"></a>将 HTML5 和 jQuery UI Datepicker 快捷日历与 ASP.NET MVC 一起使用-第1部分

作者： [Rick Anderson](https://twitter.com/RickAndMSFT)

> 本教程将指导你了解如何在 ASP.NET MVC Web 应用程序中使用编辑器模板、显示模板和 jQuery UI datepicker 快捷日历。

本教程将指导你了解如何在 ASP.NET MVC Web 应用程序中使用编辑器模板、显示模板和 jQuery [UI datepicker 快捷日历](http://plugins.jquery.com/project/datepicker)。 对于本教程，你可以使用 Microsoft Visual Web Developer 2010 Express Service Pack 1 （&quot;Visual Web Developer&quot;），该版本是 Microsoft Visual Studio 的免费版本，或者你可以使用 Visual Studio 2010 SP1 （如果已有）。

在开始之前，请确保已安装下列必备组件。 可以通过单击以下链接安装所有这些[程序： Web 平台安装程序](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)。 或者，你可以使用以下链接单独安装所需的软件：

- [Visual Studio Web Developer Express SP1 必备组件](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
- [ASP.NET MVC 3 工具更新](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
- [SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)（运行时 + 工具支持）

如果你使用的是 Visual Studio 2010 而不是 Visual Web Developer，请通过单击以下链接安装必备组件： [Visual studio 2010 必备组件](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)。

本教程假定你已完成[使用 mvc 3 的入门](../getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)教程，或者你熟悉 ASP.NET MVC 开发。 本教程从[入门与 MVC 3](../getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)教程中的已完成项目开始。

本教程使用 C# 代码。 但是，[初学者项目](https://archive.msdn.microsoft.com/Project/Download/FileDownload.aspx?ProjectName=aspnetmvcsamples&amp;DownloadId=15800)和已完成项目在 Visual Basic 中也可用。

本主题提供了包含C#和 Visual Basic 源代码的 Visual Studio 项目：[下载](https://archive.msdn.microsoft.com/Project/Download/FileDownload.aspx?ProjectName=aspnetmvcsamples&amp;DownloadId=15800)。

### <a name="what-youll-build"></a>所需操作

将模板（具体而言，是编辑和显示模板）添加到在[入门](../getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)中创建的简单电影列表应用程序。 还将添加[JQUERY UI datepicker](http://jqueryui.com/demos/datepicker/)快捷方式日历，以简化输入日期的过程。 以下屏幕截图显示了已修改的应用程序，其中显示了 jQuery UI datepicker 快捷日历。

![已完成 jQuery](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-1/_static/image1.png)

### <a name="skills-youll-learn"></a>将要学到的技能

学习内容：

- 如何使用[DataAnnotations](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx)命名空间中的属性来控制显示数据的格式以及处于编辑模式时的数据格式。
- 如何创建模板（编辑和显示模板）来控制数据的格式。
- 如何添加[JQUERY UI datepicker](http://jqueryui.com/demos/datepicker/)作为一种输入日期字段的方式。

### <a name="getting-started"></a>入门

如果尚未从初学者项目获得电影列表应用程序，请下载： 

* [下载](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098)。
* 在 Windows 资源管理器中，右键单击*MvcMovie*文件，然后选择 "**属性**"。 
* 在 " **MvcMovie 属性**" 对话框中，选择 "**取消阻止**"。 （取消阻止后，尝试使用从 Web 下载的 *.zip* 文件时，不再显示安全警告。）

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-1/_static/image2.png)

右键单击 " *MvcMovie* " 文件，然后选择 "**全部提取**" 来解压缩该文件。 在 Visual Web Developer 或 Visual Studio 2010 中，打开*MvcMovieCS\_TU*文件。

在**解决方案资源管理器**中，双击 " *Views\Shared _Layout\\* " 以将其打开。 将 `H1` 标题从**MVC 电影应用**更改为**Movie jQuery**。 按 CTRL + F5 运行应用程序，然后单击 "**主页**" 选项卡，该选项卡将转到电影控制器的 `Index` 方法。 若要试用该应用程序，请选择其中一个影片的**编辑**链接和**详细信息**链接。 请注意，在 "索引"、"编辑" 和 "详细信息" 视图中，发布日期和价格格式良好：

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-1/_static/image3.png)

日期和价格的格式设置是对 `Movie` 类的属性使用[DisplayFormat](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx)特性的结果。

打开*Movie.cs*文件并注释掉 `ReleaseDate` 和 `Price` 属性上的 `DisplayFormat` 属性。 生成的 `Movie` 类如下所示：

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-1/samples/sample1.cs)]

再次按 CTRL + F5 运行应用程序，并选择 "**主页**" 选项卡以查看电影列表。 此时，发布日期会显示日期和时间，并且 "价格" 字段将不再显示货币符号。 你在 `Movie` 类中的更改已撤消你先前看到的精美格式，但你稍后会解决此问题。

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-1/_static/image4.png)

### <a name="using-the-dataannotations-datatype-attribute-to-specify-the-data-type"></a>使用 DataAnnotations DataType 特性指定数据类型

使用 `Date` 枚举，将 `ReleaseDate` 属性的已注释掉 `DisplayFormat` 特性替换为[DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx)特性。 再次将 `Price` 属性的 `DisplayFormat` 特性替换为[DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx)特性，这一次使用 `Currency` 枚举。 完成后的代码如下所示：

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-1/samples/sample2.cs)]

运行应用程序。 现在，发布日期和价格属性的格式正确（即，使用适当的日期和货币格式）。 [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx)特性提供内置 ASP.NET MVC 模板的类型元数据，以便字段以正确格式呈现。 使用 `DataType` 特性优于最初位于代码中的 `DisplayFormat` 属性，因为 `DataType` 特性使模型更整洁，更灵活地用于国际化。

在下一部分中，你将了解如何创建自定义模板来显示日期字段。

> [!div class="step-by-step"]
> [Next](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2.md)
