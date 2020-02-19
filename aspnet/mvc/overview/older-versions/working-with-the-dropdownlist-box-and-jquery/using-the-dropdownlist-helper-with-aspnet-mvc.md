---
uid: mvc/overview/older-versions/working-with-the-dropdownlist-box-and-jquery/using-the-dropdownlist-helper-with-aspnet-mvc
title: 将 DropDownList Helper 与 ASP.NET MVC 一起使用 |Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 01/12/2012
ms.assetid: 53767e05-c8ab-42e1-a94b-22d906195200
msc.legacyurl: /mvc/overview/older-versions/working-with-the-dropdownlist-box-and-jquery/using-the-dropdownlist-helper-with-aspnet-mvc
msc.type: authoredcontent
ms.openlocfilehash: 6375bb2be158cea18309ffa71c71ac3e67bc91ed
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457864"
---
# <a name="using-the-dropdownlist-helper-with-aspnet-mvc"></a>通过 ASP.NET MVC 使用 DropDownList 帮助程序

作者： [Rick Anderson](https://twitter.com/RickAndMSFT)

本教程将指导你在 ASP.NET MVC Web 应用程序中使用[DropDownList](https://msdn.microsoft.com/library/dd492948.aspx) Helper 和[ListBox](https://msdn.microsoft.com/library/system.web.mvc.html.selectextensions.listbox.aspx)帮助器的基本知识。 你可以使用 Microsoft Visual Web Developer 2010 Express Service Pack 1，它是 Microsoft Visual Studio 的免费版本，可按照本教程进行操作。 在开始之前，请确保已安装下列必备组件。 可以通过单击以下链接安装所有这些[程序： Web 平台安装程序](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)。 或者，你可以使用以下链接单独安装必备组件：

- [Visual Studio Web Developer EXPRESS SP1 必备组件](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)<a id="post"></a>
- [ASP.NET MVC 3 工具更新](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
- [SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)（运行时 + 工具支持）

如果你使用的是 Visual Studio 2010 而不是 Visual Web Developer 2010，请通过单击以下链接安装必备组件： [Visual Studio 2010 必备组件](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)。 本教程假定你已完成[简介 ASP.NET mvc](../getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)教程或[ASP.NET Mvc 音乐应用商店](../mvc-music-store/mvc-music-store-part-1.md)教程，或者你熟悉 ASP.NET MVC 开发。 本教程从[ASP.NET MVC 音乐应用商店](../mvc-music-store/mvc-music-store-part-1.md)教程中已修改的项目开始。 可以通过以下链接下载该 starter 项目：[下载C#版本](https://archive.msdn.microsoft.com/Project/Download/FileDownload.aspx?ProjectName=aspnetmvcsamples&amp;DownloadId=15829)。

本主题附带有已完成的教程C#源代码的 Visual Web Developer 项目。 [下载](https://code.msdn.microsoft.com/Using-the-DropDownList-67f9367d)。

### <a name="what-youll-build"></a>所需操作

您将创建使用[DropDownList](https://msdn.microsoft.com/library/system.web.mvc.html.selectextensions.dropdownlist.aspx) helper 选择类别的操作方法和视图。 你还将使用**jQuery**添加可在需要新类别（如流派或艺术家）时使用的 "插入类别" 对话框。 下面是 "创建" 视图的屏幕截图，显示用于添加新流派并添加新音乐家的链接。

![](using-the-dropdownlist-helper-with-aspnet-mvc/_static/image1.png)

### <a name="skills-youll-learn"></a>将要学到的技能

学习内容：

- 如何使用[DropDownList](https://msdn.microsoft.com/library/system.web.mvc.html.selectextensions.dropdownlist.aspx)帮助器选择类别数据。
- 如何添加**jQuery**对话框以添加新类别。

### <a name="getting-started"></a>入门

首先，使用以下链接下载入门项目：[下载](https://archive.msdn.microsoft.com/Project/Download/FileDownload.aspx?ProjectName=aspnetmvcsamples&amp;DownloadId=15829)。 在 Windows 资源管理器中，右键单击*DDL\_Starter .zip*文件，然后选择 "属性"。 在 " **DDL\_Starter .Zip 属性**" 对话框中，选择 "取消阻止"。

![](using-the-dropdownlist-helper-with-aspnet-mvc/_static/image2.png)

右键单击 DDL\_Starter .zip 文件，然后选择 "**全部提取**" 来解压缩该文件。 打开*StartMusicStore*文件，其中包含 Visual web Developer 2010 Express （"Visual web developer" 或 "VWD"）或 visual Studio 2010。

按 CTRL + F5 运行应用程序，并单击 "**测试**" 链接。

![](using-the-dropdownlist-helper-with-aspnet-mvc/_static/image3.png)

选择 "**选择电影类别（简单）** " 链接。 显示 "电影类型" 选择列表，并将喜剧选定的值。

![](using-the-dropdownlist-helper-with-aspnet-mvc/_static/image4.png)

在浏览器中右键单击，然后选择 "查看源"。 将显示该页的 HTML。 下面的代码显示了 select 元素的 HTML。

[!code-html[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample1.html)]

你可以看到，选择列表中的每一项都具有值（0表示操作，1表示 Drama，2表示喜剧，3表示科学小说）和显示名称（操作、Drama、喜剧和科学小说）。 上面的代码是选择列表的标准 HTML。

将选择列表更改为 Drama，并单击 "**提交**" 按钮。 浏览器中的 URL 是 `http://localhost:2468/Home/CategoryChosen?MovieType=1` 的，页面将显示**您选择的内容： 1**。

![](using-the-dropdownlist-helper-with-aspnet-mvc/_static/image5.png)

打开*Controllers\HomeController.cs*文件并检查 `SelectCategory` 方法。

[!code-csharp[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample2.cs)]

用于创建 HTML 选择列表的[DropDownList](https://msdn.microsoft.com/library/dd492738.aspx) helper 需要显式或隐式 **&lt;SelectListItem &gt;** 。 也就是说，您可以将**ienumerable&lt;&gt;SelectListItem**显式传递到[DropDownList](https://msdn.microsoft.com/library/dd492738.aspx)帮助程序，也可以将**ienumerable&lt;SelectListItem &gt;** 添加[到使用与](https://blogs.msdn.com/b/rickandy/archive/2011/01/28/dynamic-v-strongly-typed-views.aspx)该**SelectListItem**相同的名称作为模型属性。 在本教程的下一部分中，隐式和显式地传入了**SelectListItem** 。 上面的代码演示了创建**IEnumerable&lt;SelectListItem &gt;** 并使用文本和值填充该方法的最简单方法。 请注意，`Comedy`[SelectListItem](https://msdn.microsoft.com/library/system.web.mvc.selectlistitem.aspx)将[选定](https://msdn.microsoft.com/library/system.web.mvc.selectlistitem.selected.aspx)的属性设置为**true;** 这将导致呈现的选择列表将**喜剧**显示为列表中的选定项。

上面创建的**IEnumerable&lt;SelectListItem &gt;** 将添加到名称为 MovieType 的[ViewBag](https://blogs.msdn.com/b/rickandy/archive/2011/01/28/dynamic-v-strongly-typed-views.aspx)中。 这就是我们将**IEnumerable&lt;SelectListItem**隐式 &gt;隐式传递到下面所示的[DropDownList](https://msdn.microsoft.com/library/dd492738.aspx)帮助器的方式。

打开*Views\Home\SelectCategory.cshtml*文件并检查标记。

[!code-cshtml[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample3.cshtml)]

在第三行中，我们将布局设置为 Views/Shared/\_简单\_Layout，这是标准布局文件的简化版本。 这样做是为了使显示和呈现的 HTML 简单。

在此示例中，我们不会更改应用程序的状态，因此，我们将使用**HTTP GET**而非**http POST**提交数据。 请参阅 W3C 部分[用于选择 HTTP GET 或 POST 的快速清单](http://www.w3.org/2001/tag/doc/whenToUseGet.html#checklist)。 由于我们不会更改应用程序和发布窗体，因此我们使用[html.beginform](https://msdn.microsoft.com/library/dd460344.aspx)重载来指定操作方法、控制器和窗体方法（**Http POST**或**http GET**）。 通常，视图包含不采用任何参数的[html.beginform](https://msdn.microsoft.com/library/dd505244.aspx)重载。 无参数版本默认为将表单数据发布到相同操作方法和控制器的 POST 版本。

下面的行

[!code-cshtml[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample4.cshtml)]

将字符串自变量传递给**DropDownList** helper。 此字符串在我们的示例中为 "MovieType"，执行两项操作：

- 它为**DropDownList** helper 提供密钥，以便在**ViewBag**中查找**IEnumerable&lt;SelectListItem &gt;** 。
- 它被数据绑定到 MovieType 窗体元素。 如果提交方法是**HTTP GET**，`MovieType` 将是查询字符串。 如果 submit 方法为**HTTP POST**，则 `MovieType` 将添加到邮件正文中。 下图显示了值为1的查询字符串。

![](using-the-dropdownlist-helper-with-aspnet-mvc/_static/image6.png)

下面的代码演示提交窗体的 `CategoryChosen` 方法。

[!code-csharp[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample5.cs)]

向后导航到 "测试" 页，选择 " **HTML SelectList** " 链接。 HTML 页呈现一个类似于简单 ASP.NET MVC 测试页的 select 元素。 右键单击浏览器窗口，然后选择 "**查看源**"。 选择列表的 HTML 标记本质上是相同的。 测试 HTML 页面，它的工作方式类似于 ASP.NET MVC 操作方法和前面测试过的视图。

### <a name="improving-the-movie-select-list-with-enums"></a>通过枚举改进电影选择列表

如果你的应用程序中的类别是固定的并且不会更改，则可以利用枚举来使你的代码更可靠，更易于扩展。 添加新类别时，会生成正确的类别值。 当你添加新类别但忘记更新类别值时，可避免复制和粘贴错误。

打开*Controllers\HomeController.cs*文件并检查以下代码：

[!code-csharp[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample6.cs)]

[枚举](https://msdn.microsoft.com/library/sbbt4032(VS.80).aspx)`eMovieCategories` 捕获四种影片类型。 `SetViewBagMovieType` 方法从 `eMovieCategories`**枚举**创建**IEnumerable&lt;SelectListItem &gt;** ，并从 `Selected` 参数设置 `selectedMovie` 属性。 `SelectCategoryEnum` 操作方法使用与 `SelectCategory` 操作方法相同的视图。

导航到 "测试" 页，然后单击 "`Select Movie Category (Enum)`" 链接。 此时，将显示表示枚举的字符串，而不是显示值（数字）。

### <a name="posting-enum-values"></a>发布枚举值

HTML 窗体通常用于将数据发布到服务器。 下面的代码演示 `SelectCategoryEnumPost` 方法的 `HTTP GET` 和 `HTTP POST` 版本。

[!code-csharp[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample7.cs)]

通过向 `POST` 方法传递 `eMovieCategories` 枚举，可以提取枚举值和枚举字符串。 运行示例并导航到 "测试" 页。 单击 "`Select Movie Category(Enum Post)`" 链接。 选择一种电影类型，然后单击 "提交" 按钮。 显示显示电影类型的值和名称。

![](using-the-dropdownlist-helper-with-aspnet-mvc/_static/image7.png)

### <a name="creating-a-multiple-section-select-element"></a>创建多部分 Select 元素

[ListBox](https://msdn.microsoft.com/library/system.web.mvc.html.selectextensions.listbox.aspx) html 帮助器用 "`multiple`" 属性呈现 HTML `<select>` 元素，这允许用户进行多个选择。 导航到 "测试" 链接，然后选择 "**多选国家/地区**" 链接。 呈现的 UI 允许您选择多个国家/地区。 在下图中，选中了加拿大和中国。

![](using-the-dropdownlist-helper-with-aspnet-mvc/_static/image8.png)

### <a name="examining-the-multiselectcountry-code"></a>检查 MultiSelectCountry 代码

检查*Controllers\HomeController.cs*文件中的以下代码。

[!code-csharp[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample8.cs)]

`GetCountries` 方法创建国家/地区列表，然后将其传递给 `MultiSelectList` 构造函数。 上面的 `GetCountries` 方法中使用的 `MultiSelectList` 构造函数重载采用四个参数：

[!code-csharp[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample9.cs)]

1. *项*：一个[IEnumerable](https://msdn.microsoft.com/library/system.collections.ienumerable.aspx) ，其中包含列表中的项。 在上面的示例中，是国家/地区列表。
2. *dataValueField*：包含该值的**IEnumerable**列表中的属性的名称。 在上面的示例中，`ID` 属性。
3. *dataTextField*： **IEnumerable**列表中包含要显示的信息的属性的名称。 在上面的示例中，`name` 属性。
4. *selectedValues*：选定值的列表。

在上面的示例中，`MultiSelectCountry` 方法传递所选国家/地区的 `null` 值，因此在显示 UI 时不会选择国家/地区。 以下代码显示了用于渲染 `MultiSelectCountry` 视图的 Razor 标记。

[!code-cshtml[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample10.cshtml)]

上面使用的 HTML helper [ListBox](https://msdn.microsoft.com/library/dd470200.aspx)方法使用两个参数：属性名称到模型绑定，以及包含选择选项和值的[MultiSelectList](https://msdn.microsoft.com/library/system.web.mvc.multiselectlist.aspx) 。 上面的 `ViewBag.YouSelected` 代码用于显示在提交表单时所选国家/地区的值。 检查 `MultiSelectCountry` 方法的 HTTP POST 重载。

[!code-csharp[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample11.cs)]

`ViewBag.YouSelected` 动态属性包含所选国家/地区，为窗体集合中的 `Countries` 条目获得。 在此版本中，会向 GetCountries 方法传递所选国家/地区的列表，因此，当显示 "`MultiSelectCountry`" 视图时，将在用户界面中选择所选国家/地区。

### <a name="making-a-select-element-friendly-with-the-harvest-chosen-jquery-plugin"></a>使选择元素适合使用 "获取所选 jQuery" 插件

可以将所[选](https://harvesthq.github.com/chosen/)的 jQuery 插件添加到 HTML &lt;选择&gt; 元素来创建用户友好的 UI。 下图演示了 `MultiSelectCountry` 视图中[选择](https://harvesthq.github.com/chosen/)的 jQuery 插件。

![](using-the-dropdownlist-helper-with-aspnet-mvc/_static/image9.png)

在下面两个图像中，选择**加拿大**。

![](using-the-dropdownlist-helper-with-aspnet-mvc/_static/image10.png)

![](using-the-dropdownlist-helper-with-aspnet-mvc/_static/image11.png)

在上面的图像中，选择了加拿大，并包含一个可以单击以删除所选内容的**x** 。 下图显示了所选的加拿大、中国和日本。

![](using-the-dropdownlist-helper-with-aspnet-mvc/_static/image12.png)

### <a name="hooking-up-the-harvest-chosen-jquery-plugin"></a>挂接所选 jQuery 插件

如果你有使用 jQuery 的经验，以下部分将更易于理解。 如果你之前从未使用 jQuery，你可能想要尝试以下 jQuery 教程之一。

- 由[John Resig](http://ejohn.org/)的[jQuery 如何工作](http://docs.jquery.com/Tutorials:How_jQuery_Works)
- [使用 jQuery](http://docs.jquery.com/Tutorials:Getting_Started_with_jQuery) By [Jörn Zaefferer](http://bassistance.de/)入门
- JQuery by [Cody Lindley](http://codylindley.com/) [的实时示例](http://codylindley.com/blogstuff/js/jquery/#)

本教程附带的入门和已完成的示例项目中包含所选的插件。 对于本教程，只需使用 jQuery 将其挂钩到 UI。 若要在 ASP.NET MVC 项目中使用所选的 jQuery 插件，必须执行以下操作：

1. 从[github](https://github.com/harvesthq/chosen/)下载所选插件。 此步骤已经完成。
2. 将所选文件夹添加到 ASP.NET MVC 项目。 将在上一步中下载的所选插件中的资产添加到所选文件夹。 此步骤已经完成。
3. 将所选插件与**DropDownList**或**ListBox** HTML 帮助器挂钩。

### <a name="hooking-up-the-chosen-plugin-to-the-multiselectcountry-view"></a>将所选插件挂接到 MultiSelectCountry 视图。

打开*Views\Home\MultiSelectCountry.cshtml*文件，并将 `htmlAttributes` 参数添加到 `Html.ListBox`。 要添加的参数包含选择列表的类名称（`@class = "chzn-select"`）。 完成的代码如下所示：

[!code-cshtml[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample12.cshtml)]

在上面的代码中，我们将 `class = "chzn-select"`中添加 HTML 属性和属性值。 前面的 \@ 字符类与 Razor 视图引擎无关。 `class` 是[ C#关键字](https://msdn.microsoft.com/library/x53a06bb.aspx)。 C#关键字不能用作标识符，除非它们包含 \@ 作为前缀。 在上面的示例中，`@class` 是有效的标识符，但**类**不是因为**类**是关键字。

将引用添加到所*选的或 jquery* ，并选择或选择的 *.css*文件。 *选择的或 jquery* ，并实现所选插件的功能。 所*选的或 css*文件提供样式设置。 将这些引用添加到*Views\Home\MultiSelectCountry.cshtml*文件的底部。 下面的代码演示如何引用所选的插件。

[!code-cshtml[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample13.cshtml)]

使用在**Html. ListBox**代码中使用的类名称激活选定的插件。 在上面的示例中，类名称是 `chzn-select`。 将以下行添加到*Views\Home\MultiSelectCountry.cshtml*视图文件的底部。 此行激活所选的插件。

[!code-html[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample14.html)]

以下行是用于调用 jQuery ready 函数的语法，该函数选择具有类名 `chzn-select`的 DOM 元素。

[!code-powershell[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample15.ps1)]

然后，从上述调用返回的包装集将应用所选的方法（`.chosen();`），该方法与所选的插件挂钩。

下面的代码显示已完成的*Views\Home\MultiSelectCountry.cshtml*视图文件。

[!code-cshtml[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample16.cshtml)]

运行应用程序并导航到 "`MultiSelectCountry`" 视图。 尝试添加和删除国家/地区。 提供的示例下载还包含使用视图模型而不是**ViewBag**实现 MultiSelectCountry 功能的 `MultiCountryVM` 方法和视图。

在下一部分中，你将了解 ASP.NET MVC 基架机制如何与**DropDownList** helper 一起工作。

> [!div class="step-by-step"]
> [Next](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper.md)
