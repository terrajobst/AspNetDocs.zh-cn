---
uid: mvc/overview/older-versions/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4
title: 将 HTML5 和 jQuery UI Datepicker 快捷日历与 ASP.NET MVC-第4部分一起使用 |Microsoft Docs
author: Rick-Anderson
description: 本教程将指导你了解如何在 ASP.NET MV ... 中使用编辑器模板、显示模板和 jQuery UI datepicker 快捷日历
ms.author: riande
ms.date: 08/29/2011
ms.assetid: 57666c69-2b0f-423a-a61d-be49547fa585
msc.legacyurl: /mvc/overview/older-versions/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4
msc.type: authoredcontent
ms.openlocfilehash: 583e782641efea9a9517edb31f7718b28203d756
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78433250"
---
# <a name="using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc---part-4"></a><span data-ttu-id="0fb88-103">将 HTML5 和 jQuery UI Datepicker 快捷日历与 ASP.NET MVC 一起使用-第4部分</span><span class="sxs-lookup"><span data-stu-id="0fb88-103">Using the HTML5 and jQuery UI Datepicker Popup Calendar with ASP.NET MVC - Part 4</span></span>

<span data-ttu-id="0fb88-104">作者： [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="0fb88-104">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

> <span data-ttu-id="0fb88-105">本教程将指导你了解如何在 ASP.NET MVC Web 应用程序中使用编辑器模板、显示模板和 jQuery UI datepicker 快捷日历。</span><span class="sxs-lookup"><span data-stu-id="0fb88-105">This tutorial will teach you the basics of how to work with editor templates, display templates, and the jQuery UI datepicker popup calendar in an ASP.NET MVC Web application.</span></span>

### <a name="adding-a-template-for-editing-dates"></a><span data-ttu-id="0fb88-106">添加用于编辑日期的模板</span><span class="sxs-lookup"><span data-stu-id="0fb88-106">Adding a Template for Editing Dates</span></span>

<span data-ttu-id="0fb88-107">在本节中，你将创建一个用于编辑日期的模板，当 ASP.NET MVC 显示用于编辑模型属性的 UI 时，该模板将标记为[数据类型](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx)属性的**日期**枚举。</span><span class="sxs-lookup"><span data-stu-id="0fb88-107">In this section you'll create a template for editing dates that will be applied when ASP.NET MVC displays UI for editing model properties that are marked with the **Date** enumeration of the [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) attribute.</span></span> <span data-ttu-id="0fb88-108">模板将只呈现日期;不会显示时间。</span><span class="sxs-lookup"><span data-stu-id="0fb88-108">The template will render only the date; time will not be displayed.</span></span> <span data-ttu-id="0fb88-109">在模板中，你将使用[JQUERY UI Datepicker](http://jqueryui.com/demos/datepicker/)快捷日历来提供编辑日期的方法。</span><span class="sxs-lookup"><span data-stu-id="0fb88-109">In the template you'll use the [jQuery UI Datepicker](http://jqueryui.com/demos/datepicker/) popup calendar to provide a way to edit dates.</span></span>

<span data-ttu-id="0fb88-110">若要开始，请打开*Movie.cs*文件，并将包含**日期**枚举的[DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx)特性添加到 `ReleaseDate` 属性，如以下代码所示：</span><span class="sxs-lookup"><span data-stu-id="0fb88-110">To begin, open the *Movie.cs* file and add the [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx) attribute with the **Date** enumeration to the `ReleaseDate` property, as shown in the following code:</span></span>

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample1.cs)]

<span data-ttu-id="0fb88-111">此代码将导致显示 "`ReleaseDate`" 字段，而不会在显示模板和编辑模板中显示时间。</span><span class="sxs-lookup"><span data-stu-id="0fb88-111">This code causes the `ReleaseDate` field to be displayed without the time in both display templates and edit templates.</span></span> <span data-ttu-id="0fb88-112">如果你的应用程序在*Views\Shared\EditorTemplates*文件夹或*Views\Movies\EditorTemplates*文件夹中包含一个*日期 cshtml*模板，则该模板将用于在编辑时呈现任何 `DateTime` 属性。</span><span class="sxs-lookup"><span data-stu-id="0fb88-112">If your application contains a *date.cshtml* template in the *Views\Shared\EditorTemplates* folder or in the *Views\Movies\EditorTemplates* folder, that template will be used to render any `DateTime` property while editing.</span></span> <span data-ttu-id="0fb88-113">否则，内置 ASP.NET 模板系统将以日期形式显示属性。</span><span class="sxs-lookup"><span data-stu-id="0fb88-113">Otherwise the built-in ASP.NET templating system will display the property as a date.</span></span>

<span data-ttu-id="0fb88-114">按 Ctrl+F5 以运行应用程序。</span><span class="sxs-lookup"><span data-stu-id="0fb88-114">Press CTRL+F5 to run the application.</span></span> <span data-ttu-id="0fb88-115">选择 "编辑" 链接以验证 "发布日期" 的输入字段是否只显示日期。</span><span class="sxs-lookup"><span data-stu-id="0fb88-115">Select an edit link to verify that the input field for the release date is showing only the date.</span></span>

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/_static/image1.png)

<span data-ttu-id="0fb88-116">在**解决方案资源管理器**中，展开 " *Views* " 文件夹，展开*共享*文件夹，然后右键单击*Views\Shared\EditorTemplates*文件夹。</span><span class="sxs-lookup"><span data-stu-id="0fb88-116">In **Solution Explorer**, expand the *Views* folder, expand the *Shared* folder, and then right-click the *Views\Shared\EditorTemplates* folder.</span></span>

<span data-ttu-id="0fb88-117">单击 "**添加**"，然后单击 "**查看**"。</span><span class="sxs-lookup"><span data-stu-id="0fb88-117">Click **Add**, and then click **View**.</span></span> <span data-ttu-id="0fb88-118">将显示 "**添加视图**" 对话框。</span><span class="sxs-lookup"><span data-stu-id="0fb88-118">The **Add View** dialog box is displayed.</span></span>

<span data-ttu-id="0fb88-119">在 "**视图名称**" 框中，键入 &quot;Date&quot;。</span><span class="sxs-lookup"><span data-stu-id="0fb88-119">In the **View name** box, type &quot;Date&quot;.</span></span>

<span data-ttu-id="0fb88-120">选中 "**作为分部视图创建**" 复选框。</span><span class="sxs-lookup"><span data-stu-id="0fb88-120">Select the **Create as a partial view** check box.</span></span> <span data-ttu-id="0fb88-121">请确保未选中 "**使用布局或母版页**" 和 "**创建强类型视图**" 复选框。</span><span class="sxs-lookup"><span data-stu-id="0fb88-121">Make sure that the **Use a layout or master page** and **Create a strongly-typed view** check boxes are not selected.</span></span>

<span data-ttu-id="0fb88-122">单击 **“添加”** 。</span><span class="sxs-lookup"><span data-stu-id="0fb88-122">Click **Add**.</span></span> <span data-ttu-id="0fb88-123">将创建*Views\Shared\EditorTemplates\Date.cshtml*模板。</span><span class="sxs-lookup"><span data-stu-id="0fb88-123">The *Views\Shared\EditorTemplates\Date.cshtml* template is created.</span></span>

<span data-ttu-id="0fb88-124">将以下代码添加到*Views\Shared\EditorTemplates\Date.cshtml*模板。</span><span class="sxs-lookup"><span data-stu-id="0fb88-124">Add the following code to the *Views\Shared\EditorTemplates\Date.cshtml* template.</span></span>

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample2.cshtml)]

<span data-ttu-id="0fb88-125">第一行将模型声明为 `DateTime` 类型。</span><span class="sxs-lookup"><span data-stu-id="0fb88-125">The first line declares the model to be a `DateTime` type.</span></span> <span data-ttu-id="0fb88-126">尽管不需要在 "编辑" 和 "显示模板" 中声明模型类型，但这是一种最佳做法，以便您可以对要传递到视图的模型进行编译时检查。</span><span class="sxs-lookup"><span data-stu-id="0fb88-126">Although you don't need to declare the model type in edit and display templates, it's a best practice so that you get compile-time checking of the model being passed to the view.</span></span> <span data-ttu-id="0fb88-127">（另一个优点是，你可以在 Visual Studio 的视图中获取模型的 IntelliSense。）如果未声明模型类型，则 ASP.NET MVC 会将其视为[动态](https://msdn.microsoft.com/library/dd264741.aspx)类型，并且不会进行编译时类型检查。</span><span class="sxs-lookup"><span data-stu-id="0fb88-127">(Another benefit is that you then get IntelliSense for the model in the view in Visual Studio.) If the model type is not declared, ASP.NET MVC considers it a [dynamic](https://msdn.microsoft.com/library/dd264741.aspx) type and there's no compile-time type checking.</span></span> <span data-ttu-id="0fb88-128">如果将模型声明为 `DateTime` 类型，则它将成为强类型。</span><span class="sxs-lookup"><span data-stu-id="0fb88-128">If you declare the model to be a `DateTime` type, it becomes strongly typed.</span></span>

<span data-ttu-id="0fb88-129">第二行只是文本 HTML 标记，该标记显示在日期字段之前使用日期模板&quot; &quot;。</span><span class="sxs-lookup"><span data-stu-id="0fb88-129">The second line is just literal HTML markup that displays &quot;Using Date Template&quot; before a date field.</span></span> <span data-ttu-id="0fb88-130">你将暂时使用此行来验证是否正在使用此日期模板。</span><span class="sxs-lookup"><span data-stu-id="0fb88-130">You'll use this line temporarily to verify that this date template is being used.</span></span>

<span data-ttu-id="0fb88-131">下一行是一个[Html. TextBox](https://msdn.microsoft.com/library/system.web.mvc.html.inputextensions.textbox.aspx)帮助器，用于呈现一个文本框 `input` 字段。</span><span class="sxs-lookup"><span data-stu-id="0fb88-131">The next line is an [Html.TextBox](https://msdn.microsoft.com/library/system.web.mvc.html.inputextensions.textbox.aspx) helper that renders an `input` field that's a text box.</span></span> <span data-ttu-id="0fb88-132">帮助器的第三个参数使用匿名类型将文本框的类设置为要 `datefield` 的类型和要 `date`的类型。</span><span class="sxs-lookup"><span data-stu-id="0fb88-132">The third parameter for the helper uses an anonymous type to set the class for the text box to `datefield` and the type to `date`.</span></span> <span data-ttu-id="0fb88-133">（由于 `class` 是中C#的保留的，因此需要使用 `@` 字符来转义C#分析器中的 `class` 特性。）</span><span class="sxs-lookup"><span data-stu-id="0fb88-133">(Because `class` is a reserved in C#, you need to use the `@` character to escape the `class` attribute in the C# parser.)</span></span>

<span data-ttu-id="0fb88-134">"`date` 类型" 是一种 HTML5 输入类型，可用于启用 HTML5 感知浏览器来呈现 HTML5 日历控件。</span><span class="sxs-lookup"><span data-stu-id="0fb88-134">The `date` type is an HTML5 input type that enables HTML5-aware browsers to render a HTML5 calendar control.</span></span> <span data-ttu-id="0fb88-135">稍后，你将使用 `datefield` 类添加一些 JavaScript，以将 jQuery datepicker 挂钩到 `Html.TextBox` 元素。</span><span class="sxs-lookup"><span data-stu-id="0fb88-135">Later on you'll add some JavaScript to hook up the jQuery datepicker to the `Html.TextBox` element using the `datefield` class.</span></span>

<span data-ttu-id="0fb88-136">按 Ctrl+F5 以运行应用程序。</span><span class="sxs-lookup"><span data-stu-id="0fb88-136">Press CTRL+F5 to run the application.</span></span> <span data-ttu-id="0fb88-137">您可以验证 "编辑" 视图中的 "`ReleaseDate`" 属性是否正在使用编辑模板，因为模板显示 &quot;使用日期模板&quot; 紧靠 `ReleaseDate` 文本输入框之前，如下图所示：</span><span class="sxs-lookup"><span data-stu-id="0fb88-137">You can verify that the `ReleaseDate` property in the edit view is using the edit template because the template displays &quot;Using Date Template&quot; just before the `ReleaseDate` text input box, as shown in this image:</span></span>

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/_static/image2.png)

<span data-ttu-id="0fb88-138">在浏览器中查看页面的源。</span><span class="sxs-lookup"><span data-stu-id="0fb88-138">In your browser, view the source of the page.</span></span> <span data-ttu-id="0fb88-139">（例如，右键单击该页并选择 "**查看源**"。）下面的示例演示了页面的某些标记，阐释了呈现的 HTML 中的 `class` 和 `type` 特性。</span><span class="sxs-lookup"><span data-stu-id="0fb88-139">(For example, right-click the page and select **View source**.) The following example shows some of the markup for the page, illustrating the `class` and `type` attributes in the rendered HTML.</span></span>

[!code-html[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample3.html)]

<span data-ttu-id="0fb88-140">返回到*Views\Shared\EditorTemplates\Date.cshtml*模板，并&quot; 标记中删除 &quot;使用日期模板。</span><span class="sxs-lookup"><span data-stu-id="0fb88-140">Return to the *Views\Shared\EditorTemplates\Date.cshtml* template and remove the &quot;Using Date Template&quot; markup.</span></span> <span data-ttu-id="0fb88-141">现在，已完成的模板如下所示：</span><span class="sxs-lookup"><span data-stu-id="0fb88-141">Now the completed template looks like this:</span></span>

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample4.cshtml)]

### <a name="adding-a-jquery-ui-datepicker-popup-calendar-using-nuget"></a><span data-ttu-id="0fb88-142">使用 NuGet 添加 jQuery UI Datepicker 快捷日历</span><span class="sxs-lookup"><span data-stu-id="0fb88-142">Adding a jQuery UI Datepicker Popup Calendar using NuGet</span></span>

<span data-ttu-id="0fb88-143">在本部分中，会将[JQUERY UI datepicker](http://jqueryui.com/demos/datepicker/)快捷日历添加到日期编辑模板。</span><span class="sxs-lookup"><span data-stu-id="0fb88-143">In this section you'll add the [jQuery UI datepicker](http://jqueryui.com/demos/datepicker/) popup calendar to the date-edit template.</span></span> <span data-ttu-id="0fb88-144">[JQUERY UI](http://jqueryui.com/)库为动画、高级效果和可自定义的小组件提供支持。</span><span class="sxs-lookup"><span data-stu-id="0fb88-144">The [jQuery UI](http://jqueryui.com/) library provides support for animation, advanced effects, and customizable widgets.</span></span> <span data-ttu-id="0fb88-145">它构建于 jQuery JavaScript 库之上。</span><span class="sxs-lookup"><span data-stu-id="0fb88-145">It's built on top of the jQuery JavaScript library.</span></span> <span data-ttu-id="0fb88-146">使用日历（而不是输入字符串），datepicker 弹出日历使输入日期变得简单和自然。</span><span class="sxs-lookup"><span data-stu-id="0fb88-146">The datepicker popup calendar makes it easy and natural to enter dates using a calendar instead of entering a string.</span></span> <span data-ttu-id="0fb88-147">此快捷方式还会将用户限制为法律日期-日期的普通文本输入允许输入诸如 `2/33/1999` （2月33rd，1999）之类的内容，但[JQUERY UI datepicker](http://jqueryui.com/demos/datepicker/) popup 日历不允许这样做。</span><span class="sxs-lookup"><span data-stu-id="0fb88-147">The popup calendar also limits users to legal dates — ordinary text entry for a date would let you enter something like `2/33/1999` ( February 33rd, 1999), but the [jQuery UI datepicker](http://jqueryui.com/demos/datepicker/) popup calendar won't allow that.</span></span>

<span data-ttu-id="0fb88-148">首先，必须安装 jQuery UI 库。</span><span class="sxs-lookup"><span data-stu-id="0fb88-148">First, you have to install the jQuery UI libraries.</span></span> <span data-ttu-id="0fb88-149">为此，你将使用 NuGet，这是 SP1 版本的 Visual Studio 2010 和 Visual Web Developer 中包含的程序包管理器。</span><span class="sxs-lookup"><span data-stu-id="0fb88-149">To do that, you'll use NuGet, which is a package manager that's included in SP1 versions of Visual Studio 2010 and Visual Web Developer.</span></span>

<span data-ttu-id="0fb88-150">在 Visual Web Developer 中的 "**工具**" 菜单中，选择 " **Nuget 包管理器**"，然后选择 "**管理 nuget 包**"。</span><span class="sxs-lookup"><span data-stu-id="0fb88-150">In Visual Web Developer, from the **Tools** menu, select **NuGet Package Manager** and then select **Manage NuGet Packages**.</span></span>

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/_static/image3.png)

<span data-ttu-id="0fb88-151">注意：如果 "**工具**" 菜单未显示 " **Nuget 包管理器**" 命令，则需按照 NuGet 网站 "[安装 nuget](http://docs.nuget.org/docs/start-here/installing-nuget) " 页上的说明安装 nuget。</span><span class="sxs-lookup"><span data-stu-id="0fb88-151">Note: If the **Tools** menu doesn't display the **NuGet Package Manager** command, you need to install NuGet by following the instructions on the [Installing NuGet](http://docs.nuget.org/docs/start-here/installing-nuget) page of the NuGet website.</span></span>   
  
<span data-ttu-id="0fb88-152">如果使用的是 Visual Studio，而不是 Visual Web Developer，请从 "**工具**" 菜单中选择 " **NuGet 包管理器**"，然后选择 "**添加库程序包引用**"。</span><span class="sxs-lookup"><span data-stu-id="0fb88-152">If you're using Visual Studio instead of Visual Web Developer, from the **Tools** menu, select **NuGet Package Manager** and then select **Add Library Package Reference**.</span></span>

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/_static/image4.png)

<span data-ttu-id="0fb88-153">在 " **MVCMovie-管理 NuGet 包**" 对话框中，单击左侧的 "**联机**" 选项卡，然后在 "搜索" 框中输入 &quot;jQuery. UI&quot;。</span><span class="sxs-lookup"><span data-stu-id="0fb88-153">In the **MVCMovie - Manage NuGet Packages** dialog box, click the **Online** tab on the left and then enter &quot;jQuery.UI&quot; in the search box.</span></span> <span data-ttu-id="0fb88-154">选择 "j**查询 UI 小组件： Datepicker**"，并选择 "**安装**" 按钮。</span><span class="sxs-lookup"><span data-stu-id="0fb88-154">Select j **Query UI Widgets:Datepicker**, then select the **Install** button.</span></span>

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/_static/image5.png)

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/_static/image6.png)

<span data-ttu-id="0fb88-155">NuGet 将 jQuery UI Core 和 jQuery UI 日期选取器的这些调试版本和缩小版本添加到你的项目：</span><span class="sxs-lookup"><span data-stu-id="0fb88-155">NuGet adds these debug versions and minified versions of jQuery UI Core and the jQuery UI date picker to your project:</span></span>

- <span data-ttu-id="0fb88-156">*jquery. node.js*</span><span class="sxs-lookup"><span data-stu-id="0fb88-156">*jquery.ui.core.js*</span></span>
- <span data-ttu-id="0fb88-157">*jquery. core. .js*</span><span class="sxs-lookup"><span data-stu-id="0fb88-157">*jquery.ui.core.min.js*</span></span>
- <span data-ttu-id="0fb88-158">*jquery. datepicker*</span><span class="sxs-lookup"><span data-stu-id="0fb88-158">*jquery.ui.datepicker.js*</span></span>
- <span data-ttu-id="0fb88-159">*jquery. datepicker。*</span><span class="sxs-lookup"><span data-stu-id="0fb88-159">*jquery.ui.datepicker.min.js*</span></span>

<span data-ttu-id="0fb88-160">注意：调试版本（没有 *. .js*扩展名的文件）对调试非常有用，但在生产站点中，只包含缩小版本。</span><span class="sxs-lookup"><span data-stu-id="0fb88-160">Note: The debug versions (the files without the *.min.js* extension) are useful for debugging, but in a production site, you'd include only the minified versions.</span></span>

<span data-ttu-id="0fb88-161">若要实际使用 jQuery 日期选取器，需要创建一个将日历小组件挂钩到编辑模板的 jQuery 脚本。</span><span class="sxs-lookup"><span data-stu-id="0fb88-161">To actually use the jQuery date picker, you need to create a jQuery script that will hook up the calendar widget to the edit template.</span></span> <span data-ttu-id="0fb88-162">在**解决方案资源管理器**中，右键单击 "*脚本*" 文件夹，然后依次选择 "**添加**"、"**新建项**" 和 " **JScript 文件**"。</span><span class="sxs-lookup"><span data-stu-id="0fb88-162">In **Solution Explorer**, right-click the *Scripts* folder and select **Add**, then **New Item**, and then **JScript File**.</span></span> <span data-ttu-id="0fb88-163">将该文件命名为*DatePickerReady*。</span><span class="sxs-lookup"><span data-stu-id="0fb88-163">Name the file *DatePickerReady.js*.</span></span>

<span data-ttu-id="0fb88-164">将以下代码添加到*DatePickerReady*文件：</span><span class="sxs-lookup"><span data-stu-id="0fb88-164">Add the following code to the *DatePickerReady.js* file:</span></span>

[!code-javascript[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample5.js)]

<span data-ttu-id="0fb88-165">如果你不熟悉 jQuery，这里提供了有关此操作的简要说明：第一行是 &quot;jQuery ready&quot; 函数，该函数在页中的所有 DOM 元素都已加载时调用。</span><span class="sxs-lookup"><span data-stu-id="0fb88-165">If you're not familiar with jQuery, here's a brief explanation of what this does: the first line is the &quot;jQuery ready&quot; function, which is called when all the DOM elements in a page have loaded.</span></span> <span data-ttu-id="0fb88-166">第二行选择具有类名 `datefield`的所有 DOM 元素，然后为每个元素调用 `datepicker` 函数。</span><span class="sxs-lookup"><span data-stu-id="0fb88-166">The second line selects all DOM elements that have the class name `datefield`, then invokes the `datepicker` function for each of them.</span></span> <span data-ttu-id="0fb88-167">（请记住，在本教程的前面部分中，已将 `datefield` 类添加到*Views\Shared\EditorTemplates\Date.cshtml*模板。）</span><span class="sxs-lookup"><span data-stu-id="0fb88-167">(Remember that you added the `datefield` class to the *Views\Shared\EditorTemplates\Date.cshtml* template earlier in the tutorial.)</span></span>

<span data-ttu-id="0fb88-168">接下来，打开*Views\Shared\\_Layout* 。</span><span class="sxs-lookup"><span data-stu-id="0fb88-168">Next, open the *Views\Shared\\_Layout.cshtml* file.</span></span> <span data-ttu-id="0fb88-169">你需要添加对以下文件的引用，这些文件都是必需的，以便你可以使用日期选取器：</span><span class="sxs-lookup"><span data-stu-id="0fb88-169">You need to add references to the following files, which are all required so that you can use the date picker:</span></span>

- <span data-ttu-id="0fb88-170">*内容/主题/基/jquery。*</span><span class="sxs-lookup"><span data-stu-id="0fb88-170">*Content/themes/base/jquery.ui.core.css*</span></span>
- <span data-ttu-id="0fb88-171">*Content/themes/base/jquery. datepicker*</span><span class="sxs-lookup"><span data-stu-id="0fb88-171">*Content/themes/base/jquery.ui.datepicker.css*</span></span>
- <span data-ttu-id="0fb88-172">*内容/主题/基/jquery. ui*</span><span class="sxs-lookup"><span data-stu-id="0fb88-172">*Content/themes/base/jquery.ui.theme.css*</span></span>
- <span data-ttu-id="0fb88-173">*jquery. core. .js*</span><span class="sxs-lookup"><span data-stu-id="0fb88-173">*jquery.ui.core.min.js*</span></span>
- <span data-ttu-id="0fb88-174">*jquery. datepicker。*</span><span class="sxs-lookup"><span data-stu-id="0fb88-174">*jquery.ui.datepicker.min.js*</span></span>
- <span data-ttu-id="0fb88-175">*DatePickerReady*</span><span class="sxs-lookup"><span data-stu-id="0fb88-175">*DatePickerReady.js*</span></span>

<span data-ttu-id="0fb88-176">下面的示例演示了应在*Views\Shared\\_Layout*的 `head` 元素的底部添加的实际代码。</span><span class="sxs-lookup"><span data-stu-id="0fb88-176">The following example shows the actual code that you should add at the bottom of the `head` element in the *Views\Shared\\_Layout.cshtml* file.</span></span>

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample6.cshtml)]

<span data-ttu-id="0fb88-177">完整的 `head` 部分如下所示：</span><span class="sxs-lookup"><span data-stu-id="0fb88-177">The complete `head` section is shown here:</span></span>

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample7.cshtml)]

<span data-ttu-id="0fb88-178">[URL 内容帮助器](https://msdn.microsoft.com/library/system.web.mvc.urlhelper.content.aspx)方法将资源路径转换为绝对路径。</span><span class="sxs-lookup"><span data-stu-id="0fb88-178">The [URL content helper](https://msdn.microsoft.com/library/system.web.mvc.urlhelper.content.aspx) method converts the resource path to an absolute path.</span></span> <span data-ttu-id="0fb88-179">当应用程序在 IIS 上运行时，必须使用 `@URL.Content` 来正确引用这些资源。</span><span class="sxs-lookup"><span data-stu-id="0fb88-179">You must use `@URL.Content` to correctly reference these resources when the application is running on IIS.</span></span>

<span data-ttu-id="0fb88-180">按 Ctrl+F5 以运行应用程序。</span><span class="sxs-lookup"><span data-stu-id="0fb88-180">Press CTRL+F5 to run the application.</span></span> <span data-ttu-id="0fb88-181">选择 "编辑" 链接，然后将插入点放入 " **ReleaseDate** " 字段。</span><span class="sxs-lookup"><span data-stu-id="0fb88-181">Select an edit link, then put the insertion point into the **ReleaseDate** field.</span></span> <span data-ttu-id="0fb88-182">显示 jQuery UI 快捷日历。</span><span class="sxs-lookup"><span data-stu-id="0fb88-182">The jQuery UI popup calendar is displayed.</span></span>

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/_static/image7.png)

<span data-ttu-id="0fb88-183">与大多数 jQuery 控件一样，datepicker 可让你对其进行广泛的自定义。</span><span class="sxs-lookup"><span data-stu-id="0fb88-183">Like most jQuery controls, the datepicker lets you customize it extensively.</span></span> <span data-ttu-id="0fb88-184">有关信息，请参阅可视化自定义：在[JQUERY ui](http://learn.jquery.com/jquery-ui/getting-started/)网站上[设计 jquery ui 主题](http://learn.jquery.com/jquery-ui/getting-started/#visual-customization-designing-a-jquery-ui-theme)。</span><span class="sxs-lookup"><span data-stu-id="0fb88-184">For information, see [Visual Customization: Designing a jQuery UI theme](http://learn.jquery.com/jquery-ui/getting-started/#visual-customization-designing-a-jquery-ui-theme) on the [jQuery UI](http://learn.jquery.com/jquery-ui/getting-started/) site.</span></span>

### <a name="supporting-the-html5-date-input-control"></a><span data-ttu-id="0fb88-185">支持 HTML5 日期输入控件</span><span class="sxs-lookup"><span data-stu-id="0fb88-185">Supporting the HTML5 Date Input Control</span></span>

<span data-ttu-id="0fb88-186">随着更多浏览器支持 HTML5，你将需要使用本机 HTML5 输入，例如 `date` input 元素，而不是使用 jQuery UI 日历。</span><span class="sxs-lookup"><span data-stu-id="0fb88-186">As more browsers support HTML5, you'll want to use the native HTML5 input, such as the `date` input element, and not use the jQuery UI calendar.</span></span> <span data-ttu-id="0fb88-187">可以向应用程序添加逻辑，以便在浏览器支持 HTML5 控件时自动使用它们。</span><span class="sxs-lookup"><span data-stu-id="0fb88-187">You can add logic to your application to automatically use HTML5 controls if the browser supports them.</span></span> <span data-ttu-id="0fb88-188">为此，请将*DatePickerReady*文件的内容替换为以下内容：</span><span class="sxs-lookup"><span data-stu-id="0fb88-188">To do this, replace the contents of the *DatePickerReady.js* file with the following:</span></span>

[!code-javascript[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample8.js)]

<span data-ttu-id="0fb88-189">此脚本的第一行使用 Modernizr 来验证是否支持 HTML5 日期输入。</span><span class="sxs-lookup"><span data-stu-id="0fb88-189">The first line of this script uses Modernizr to verify that HTML5 date input is supported.</span></span> <span data-ttu-id="0fb88-190">如果不支持，则改为与 jQuery UI 日期选取器挂钩。</span><span class="sxs-lookup"><span data-stu-id="0fb88-190">If it's not supported, the jQuery UI date picker is hooked up instead.</span></span> <span data-ttu-id="0fb88-191">（[Modernizr](http://www.modernizr.com/docs/)是一个开源 JavaScript 库，用于检测 HTML5 和 CSS3 的本机实现的可用性。</span><span class="sxs-lookup"><span data-stu-id="0fb88-191">([Modernizr](http://www.modernizr.com/docs/) is an open-source JavaScript library that detects the availability of native implementations of HTML5 and CSS3.</span></span> <span data-ttu-id="0fb88-192">Modernizr 包含在您创建的任何新的 ASP.NET MVC 项目中。）</span><span class="sxs-lookup"><span data-stu-id="0fb88-192">Modernizr is included in any new ASP.NET MVC projects that you create.)</span></span>

<span data-ttu-id="0fb88-193">做出此更改后，可以使用支持 HTML5 的浏览器（如 Opera 11）对其进行测试。</span><span class="sxs-lookup"><span data-stu-id="0fb88-193">After you've made this change, you can test it by using a browser that supports HTML5, such as Opera 11.</span></span> <span data-ttu-id="0fb88-194">使用与 HTML5 兼容的浏览器运行应用程序，并编辑电影条目。</span><span class="sxs-lookup"><span data-stu-id="0fb88-194">Run the application using an HTML5-compatible browser and edit a movie entry.</span></span> <span data-ttu-id="0fb88-195">使用 HTML5 日期控件，而不是 jQuery UI 快捷方式日历：</span><span class="sxs-lookup"><span data-stu-id="0fb88-195">The HTML5 date control is used instead of the jQuery UI popup calendar:</span></span>

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/_static/image8.png)

<span data-ttu-id="0fb88-196">因为新版本的浏览器以增量方式实现 HTML5，所以现在最好的方法是将代码添加到适合各种 HTML5 支持的网站。</span><span class="sxs-lookup"><span data-stu-id="0fb88-196">Because new versions of browsers are implementing HTML5 incrementally, a good approach for now is to add code to your website that accommodates a wide variety of HTML5 support.</span></span> <span data-ttu-id="0fb88-197">例如，下面显示了一个更可靠的*DatePickerReady*脚本，使你的站点支持仅部分支持 HTML5 日期控件的浏览器。</span><span class="sxs-lookup"><span data-stu-id="0fb88-197">For example, a more robust *DatePickerReady.js* script is shown below that lets your site support browsers that only partially support the HTML5 date control.</span></span>

[!code-javascript[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample9.js)]

<span data-ttu-id="0fb88-198">此脚本选择 `date` 类型的 HTML5 `input` 元素，这些元素不完全支持 HTML5 日期控件。</span><span class="sxs-lookup"><span data-stu-id="0fb88-198">This script selects HTML5 `input` elements of type `date` that don't fully support the HTML5 date control.</span></span> <span data-ttu-id="0fb88-199">对于这些元素，它将挂钩 jQuery UI 弹出日历，然后将 `type` 属性从 `date` 更改为 `text`。</span><span class="sxs-lookup"><span data-stu-id="0fb88-199">For those elements, it hooks up the jQuery UI popup calendar and then changes the `type` attribute from `date` to `text`.</span></span> <span data-ttu-id="0fb88-200">通过将 `type` 属性从 `date` 改为 `text`，消除了部分 HTML5 日期支持。</span><span class="sxs-lookup"><span data-stu-id="0fb88-200">By changing the `type` attribute from `date` to `text`, partial HTML5 date support is eliminated.</span></span> <span data-ttu-id="0fb88-201">更可靠的*DatePickerReady*脚本可在[JSFIDDLE](http://jsfiddle.net/XSTK8/15/)中找到。</span><span class="sxs-lookup"><span data-stu-id="0fb88-201">An even more robust *DatePickerReady.js* script can be found at [JSFIDDLE](http://jsfiddle.net/XSTK8/15/).</span></span>

### <a name="adding-nullable-dates-to-the-templates"></a><span data-ttu-id="0fb88-202">向模板添加可以为 Null 的日期</span><span class="sxs-lookup"><span data-stu-id="0fb88-202">Adding Nullable Dates to the Templates</span></span>

<span data-ttu-id="0fb88-203">如果使用现有的日期模板之一并传递 null 日期，则会出现运行时错误。</span><span class="sxs-lookup"><span data-stu-id="0fb88-203">If you use one of the existing date templates and pass a null date, you'll get a run-time error.</span></span> <span data-ttu-id="0fb88-204">若要使日期模板更可靠，请将其更改为处理 null 值。</span><span class="sxs-lookup"><span data-stu-id="0fb88-204">To make the date templates more robust, you'll change them to handle null values.</span></span> <span data-ttu-id="0fb88-205">若要支持可以为 null 的日期，请将*Views\Shared\DisplayTemplates\DateTime.cshtml*中的代码更改为以下内容：</span><span class="sxs-lookup"><span data-stu-id="0fb88-205">To support nullable dates, change the code in the *Views\Shared\DisplayTemplates\DateTime.cshtml* to the following:</span></span>

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample10.cshtml)]

<span data-ttu-id="0fb88-206">当模型为**null**时，该代码将返回空字符串。</span><span class="sxs-lookup"><span data-stu-id="0fb88-206">The code returns an empty string when the model is **null**.</span></span>

<span data-ttu-id="0fb88-207">将*Views\Shared\EditorTemplates\Date.cshtml*文件中的代码更改为以下内容：</span><span class="sxs-lookup"><span data-stu-id="0fb88-207">Change the code in the *Views\Shared\EditorTemplates\Date.cshtml* file to the following:</span></span>

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample11.cshtml)]

<span data-ttu-id="0fb88-208">当此代码运行时，如果模型不为 null，则使用模型的 `DateTime` 值。</span><span class="sxs-lookup"><span data-stu-id="0fb88-208">When this code runs, if the model is not null, the model's `DateTime` value is used.</span></span> <span data-ttu-id="0fb88-209">如果模型为 null，则改为使用当前日期。</span><span class="sxs-lookup"><span data-stu-id="0fb88-209">If the model is null, the current date is used instead.</span></span>

### <a name="wrapup"></a><span data-ttu-id="0fb88-210">Wrapup</span><span class="sxs-lookup"><span data-stu-id="0fb88-210">Wrapup</span></span>

<span data-ttu-id="0fb88-211">本教程介绍了 ASP.NET 模板化帮助器的基本知识，并演示了如何在 ASP.NET MVC 应用程序中使用 jQuery UI datepicker 弹出日历。</span><span class="sxs-lookup"><span data-stu-id="0fb88-211">This tutorial has covered the basics of ASP.NET templated helpers and shows you how to use the jQuery UI datepicker popup calendar in an ASP.NET MVC application.</span></span> <span data-ttu-id="0fb88-212">有关详细信息，请尝试以下资源：</span><span class="sxs-lookup"><span data-stu-id="0fb88-212">For more information, try these resources:</span></span>

- <span data-ttu-id="0fb88-213">有关本地化的详细信息，请参阅 Rajeesh 的博客[JQueryUI Datepicker in ASP.NET MVC](http://www.rajeeshcv.com/2010/02/jqueryui-datepicker-in-asp-net-mvc/)。</span><span class="sxs-lookup"><span data-stu-id="0fb88-213">For information on localization, see Rajeesh's blog [JQueryUI Datepicker in ASP.NET MVC](http://www.rajeeshcv.com/2010/02/jqueryui-datepicker-in-asp-net-mvc/).</span></span>
- <span data-ttu-id="0fb88-214">有关 jQuery UI 的信息，请参阅[JQUERY ui](http://docs.jquery.com/UI)。</span><span class="sxs-lookup"><span data-stu-id="0fb88-214">For information about jQuery UI, see [jQuery UI](http://docs.jquery.com/UI).</span></span>
- <span data-ttu-id="0fb88-215">有关如何本地化 datepicker 控件的信息，请参阅[UI/datepicker/本地化](http://docs.jquery.com/UI/Datepicker/Localization)。</span><span class="sxs-lookup"><span data-stu-id="0fb88-215">For information about how to localize the datepicker control, see [UI/Datepicker/Localization](http://docs.jquery.com/UI/Datepicker/Localization).</span></span>
- <span data-ttu-id="0fb88-216">有关 ASP.NET MVC 模板的详细信息，请参阅[ASP.NET MVC 2 模板](http://bradwilson.typepad.com/blog/2009/10/aspnet-mvc-2-templates-part-1-introduction.html)上的 Brad Wilson 的博客系列。</span><span class="sxs-lookup"><span data-stu-id="0fb88-216">For more information about the ASP.NET MVC templates, see Brad Wilson's blog series on [ASP.NET MVC 2 Templates](http://bradwilson.typepad.com/blog/2009/10/aspnet-mvc-2-templates-part-1-introduction.html).</span></span> <span data-ttu-id="0fb88-217">尽管此系列是为 ASP.NET MVC 2 编写的，但材料仍适用于当前版本的 ASP.NET MVC。</span><span class="sxs-lookup"><span data-stu-id="0fb88-217">Although the series was written for ASP.NET MVC 2, the material still applies for the current version of ASP.NET MVC.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="0fb88-218">上一页</span><span class="sxs-lookup"><span data-stu-id="0fb88-218">Previous</span></span>](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3.md)
