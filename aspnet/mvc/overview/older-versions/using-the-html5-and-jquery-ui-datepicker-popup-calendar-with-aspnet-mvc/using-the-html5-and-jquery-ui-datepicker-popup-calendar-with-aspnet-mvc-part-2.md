---
uid: mvc/overview/older-versions/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2
title: 将 HTML5 和 jQuery UI Datepicker 快捷日历与 ASP.NET MVC-第2部分一起使用 |Microsoft Docs
author: Rick-Anderson
description: 本教程将指导你了解如何在 ASP.NET MV ... 中使用编辑器模板、显示模板和 jQuery UI datepicker 快捷日历
ms.author: riande
ms.date: 08/29/2011
ms.assetid: 21a178de-4c5a-4211-8a9c-74ec576c0f30
msc.legacyurl: /mvc/overview/older-versions/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2
msc.type: authoredcontent
ms.openlocfilehash: 325cc90eb6e717c47863eda6253e0d48d796386b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78498416"
---
# <a name="using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc---part-2"></a><span data-ttu-id="27afe-103">将 HTML5 和 jQuery UI Datepicker 快捷日历与 ASP.NET MVC 一起使用-第2部分</span><span class="sxs-lookup"><span data-stu-id="27afe-103">Using the HTML5 and jQuery UI Datepicker Popup Calendar with ASP.NET MVC - Part 2</span></span>

<span data-ttu-id="27afe-104">作者： [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="27afe-104">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

> <span data-ttu-id="27afe-105">本教程将指导你了解如何在 ASP.NET MVC Web 应用程序中使用编辑器模板、显示模板和 jQuery UI datepicker 快捷日历。</span><span class="sxs-lookup"><span data-stu-id="27afe-105">This tutorial will teach you the basics of how to work with editor templates, display templates, and the jQuery UI datepicker popup calendar in an ASP.NET MVC Web application.</span></span>

## <a name="adding-an-automatic-datetime-template"></a><span data-ttu-id="27afe-106">添加自动日期时间模板</span><span class="sxs-lookup"><span data-stu-id="27afe-106">Adding an Automatic DateTime Template</span></span>

<span data-ttu-id="27afe-107">在本教程的第一部分中，您看到了如何向模型添加属性以显式指定格式设置，以及如何显式指定用于呈现模型的模板。</span><span class="sxs-lookup"><span data-stu-id="27afe-107">In the first part of this tutorial, you saw how you can add attributes to the model to explicitly specify formatting, and how you can explicitly specify the template that's used to render the model.</span></span> <span data-ttu-id="27afe-108">例如，以下代码中的[DisplayFormat](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx)属性显式指定 `ReleaseDate` 属性的格式。</span><span class="sxs-lookup"><span data-stu-id="27afe-108">For example, the [DisplayFormat](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx) attribute in the following code explicitly specifies the formatting for the `ReleaseDate` property.</span></span>

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample1.cs)]

<span data-ttu-id="27afe-109">在下面的示例中，使用 `Date` 枚举的[DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx)特性指定应使用日期模板来呈现模型。</span><span class="sxs-lookup"><span data-stu-id="27afe-109">In the following example, the [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) attribute, using the `Date` enumeration, specifies that the date template should be used to render the model.</span></span> <span data-ttu-id="27afe-110">如果项目中没有日期模板，则使用内置日期模板。</span><span class="sxs-lookup"><span data-stu-id="27afe-110">If there's no date template in your project, the built-in date template is used.</span></span>

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample2.cs)]

<span data-ttu-id="27afe-111">但 ASP。通过查找与类型名称匹配的模板，MVC 可以使用配置上的规则执行类型匹配。</span><span class="sxs-lookup"><span data-stu-id="27afe-111">However, ASP.MVC can perform type matching using convention-over-configuration, by looking for a template that matches the name of a type.</span></span> <span data-ttu-id="27afe-112">这样，便可以创建一个自动设置数据格式的模板，而无需使用任何属性或代码。</span><span class="sxs-lookup"><span data-stu-id="27afe-112">This lets you create a template that automatically formats data without using any attributes or code at all.</span></span> <span data-ttu-id="27afe-113">对于本教程的本部分，你将创建一个模板，该模板将自动应用于类型为[DateTime](https://msdn.microsoft.com/library/system.datetime.aspx)的模型属性。</span><span class="sxs-lookup"><span data-stu-id="27afe-113">For this part of the tutorial, you'll create a template that's automatically applied to model properties of type [DateTime](https://msdn.microsoft.com/library/system.datetime.aspx).</span></span> <span data-ttu-id="27afe-114">您无需使用特性或其他配置来指定应使用该模板来呈现类型为[DateTime](https://msdn.microsoft.com/library/system.datetime.aspx)的所有模型属性。</span><span class="sxs-lookup"><span data-stu-id="27afe-114">You won't need to use an attribute or other configuration to specify that the template should be used to render all model properties of type [DateTime](https://msdn.microsoft.com/library/system.datetime.aspx).</span></span>

<span data-ttu-id="27afe-115">您还将学习如何自定义单个属性的显示，甚至是单个字段的显示方式。</span><span class="sxs-lookup"><span data-stu-id="27afe-115">You'll also learn a way to customize the display of individual properties or even individual fields.</span></span>

<span data-ttu-id="27afe-116">首先，让我们删除现有格式设置信息，并在应用程序中显示完整的日期。</span><span class="sxs-lookup"><span data-stu-id="27afe-116">To begin, let's remove existing formatting information and display full dates in the application.</span></span>

<span data-ttu-id="27afe-117">打开*Movie.cs*文件，并在 `ReleaseDate` 属性上注释掉 `DataType` 特性：</span><span class="sxs-lookup"><span data-stu-id="27afe-117">Open the *Movie.cs* file and comment out the `DataType` attribute on the `ReleaseDate` property:</span></span>

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample3.cs)]

<span data-ttu-id="27afe-118">按 Ctrl+F5 以运行应用程序。</span><span class="sxs-lookup"><span data-stu-id="27afe-118">Press CTRL+F5 to run the application.</span></span>

<span data-ttu-id="27afe-119">请注意，`ReleaseDate` 属性现在同时显示日期和时间，因为在未提供格式设置信息时，这是默认值。</span><span class="sxs-lookup"><span data-stu-id="27afe-119">Notice that the `ReleaseDate` property now displays both the date and time, because that's the default when no formatting information is provided.</span></span>

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/_static/image1.png)

### <a name="adding-css-styles-for-testing-new-templates"></a><span data-ttu-id="27afe-120">添加 CSS 样式以测试新模板</span><span class="sxs-lookup"><span data-stu-id="27afe-120">Adding CSS Styles for Testing New Templates</span></span>

<span data-ttu-id="27afe-121">在创建用于设置日期格式的模板之前，你将添加几个可应用于新模板的 CSS 样式规则。</span><span class="sxs-lookup"><span data-stu-id="27afe-121">Before you create a template for formatting dates, you'll add a few CSS style rules that you can apply to the new templates.</span></span> <span data-ttu-id="27afe-122">这将帮助你验证呈现的页面是否正在使用新模板。</span><span class="sxs-lookup"><span data-stu-id="27afe-122">These will help you verify that the rendered page is using the new template.</span></span>

<span data-ttu-id="27afe-123">打开*Content\Site.cs*文件，并将以下 CSS 规则添加到文件底部：</span><span class="sxs-lookup"><span data-stu-id="27afe-123">Open the *Content\Site.cs*s file and add the following CSS rules to the bottom of the file:</span></span>

[!code-css[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample4.css)]

### <a name="adding-datetime-display-templates"></a><span data-ttu-id="27afe-124">添加 DateTime 显示模板</span><span class="sxs-lookup"><span data-stu-id="27afe-124">Adding DateTime Display Templates</span></span>

<span data-ttu-id="27afe-125">现在可以创建新模板。</span><span class="sxs-lookup"><span data-stu-id="27afe-125">Now you can create the new template.</span></span> <span data-ttu-id="27afe-126">在*Views\Movies*文件夹中，创建*DisplayTemplates*文件夹。</span><span class="sxs-lookup"><span data-stu-id="27afe-126">In the *Views\Movies* folder, create a *DisplayTemplates* folder.</span></span>

<span data-ttu-id="27afe-127">在*Views\Shared*文件夹中，创建*DisplayTemplates*文件夹和*EditorTemplates*文件夹。</span><span class="sxs-lookup"><span data-stu-id="27afe-127">In the *Views\Shared* folder, create a *DisplayTemplates* folder and an *EditorTemplates* folder.</span></span>

<span data-ttu-id="27afe-128">所有控制器将使用*Views\Shared\DisplayTemplates*文件夹中的显示模板。</span><span class="sxs-lookup"><span data-stu-id="27afe-128">The display templates in the *Views\Shared\DisplayTemplates* folder will be used by all controllers.</span></span> <span data-ttu-id="27afe-129">*Views\Movie\DisplayTemplates*文件夹中的显示模板将仅由 `Movie` 控制器使用。</span><span class="sxs-lookup"><span data-stu-id="27afe-129">The display templates in the *Views\Movie\DisplayTemplates* folder will be used only by the `Movie` controller.</span></span> <span data-ttu-id="27afe-130">（如果两个文件夹中都出现具有相同名称的模板，则*Views\Movie\DisplayTemplates*文件夹中的模板（即，更具体的模板）优先于 `Movie` 控制器返回的视图。）</span><span class="sxs-lookup"><span data-stu-id="27afe-130">(If a template with the same name appears in both folders, the template in the *Views\Movie\DisplayTemplates* folder — that is, the more specific template — takes precedence for views returned by the `Movie` controller.)</span></span>

<span data-ttu-id="27afe-131">在**解决方案资源管理器**中，展开 " *Views* " 文件夹，展开*共享*文件夹，然后右键单击*Views\Shared\DisplayTemplates*文件夹。</span><span class="sxs-lookup"><span data-stu-id="27afe-131">In **Solution Explorer**, expand the *Views* folder, expand the *Shared* folder, and then right-click the *Views\Shared\DisplayTemplates* folder.</span></span>

<span data-ttu-id="27afe-132">单击 "**添加**"，然后单击 "**查看**"。</span><span class="sxs-lookup"><span data-stu-id="27afe-132">Click **Add** and then click **View**.</span></span> <span data-ttu-id="27afe-133">将显示 "**添加视图**" 对话框。</span><span class="sxs-lookup"><span data-stu-id="27afe-133">The **Add View** dialog box is displayed.</span></span>

<span data-ttu-id="27afe-134">在 "**视图名称**" 框中，键入 `DateTime`。</span><span class="sxs-lookup"><span data-stu-id="27afe-134">In the **View name** box, type `DateTime`.</span></span> <span data-ttu-id="27afe-135">（必须使用此名称才能匹配类型的名称。）</span><span class="sxs-lookup"><span data-stu-id="27afe-135">(You must use this name in order to match the name of the type.)</span></span>

<span data-ttu-id="27afe-136">选中 "**作为分部视图创建**" 复选框。</span><span class="sxs-lookup"><span data-stu-id="27afe-136">Select the **Create as a partial view** check box.</span></span> <span data-ttu-id="27afe-137">请确保未选中 "**使用布局或母版页**" 和 "**创建强类型视图**" 复选框。</span><span class="sxs-lookup"><span data-stu-id="27afe-137">Make sure that the **Use a layout or master page** and **Create a strongly-typed view** check boxes are not selected.</span></span>

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/_static/image2.png)

<span data-ttu-id="27afe-138">单击 **“添加”** 。</span><span class="sxs-lookup"><span data-stu-id="27afe-138">Click **Add**.</span></span> <span data-ttu-id="27afe-139">在*Views\Shared\DisplayTemplates*中创建一个*日期时间的日期。*</span><span class="sxs-lookup"><span data-stu-id="27afe-139">A *DateTime.cshtml* template is created in the *Views\Shared\DisplayTemplates*.</span></span>

<span data-ttu-id="27afe-140">下图显示了在创建 `DateTime` 显示和编辑器模板之后**解决方案资源管理器**中的*Views*文件夹。</span><span class="sxs-lookup"><span data-stu-id="27afe-140">The following image shows the *Views* folder in **Solution Explorer** after the `DateTime` display and editor templates are created.</span></span>

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/_static/image3.png)

<span data-ttu-id="27afe-141">打开*Views\Shared\DisplayTemplates\DateTime.cshtml*文件并添加以下标记，该标记使用[字符串. format](https://msdn.microsoft.com/library/system.string.format.aspx)方法将属性的格式设置为不带时间的日期。</span><span class="sxs-lookup"><span data-stu-id="27afe-141">Open the *Views\Shared\DisplayTemplates\DateTime.cshtml* file and add the following markup, which uses the [String.Format](https://msdn.microsoft.com/library/system.string.format.aspx) method to format the property as a date without the time.</span></span> <span data-ttu-id="27afe-142">（`{0:d}` 格式指定短日期格式。）</span><span class="sxs-lookup"><span data-stu-id="27afe-142">(The `{0:d}` format specifies short date format.)</span></span>

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample5.cs)]

<span data-ttu-id="27afe-143">重复此步骤，在*Views\Movie\DisplayTemplates*文件夹中创建 `DateTime` 模板。</span><span class="sxs-lookup"><span data-stu-id="27afe-143">Repeat this step to create a `DateTime` template in the *Views\Movie\DisplayTemplates* folder.</span></span> <span data-ttu-id="27afe-144">在*Views\Movie\DisplayTemplates\DateTime.cshtml*文件中使用以下代码。</span><span class="sxs-lookup"><span data-stu-id="27afe-144">Use the following code in the *Views\Movie\DisplayTemplates\DateTime.cshtml* file.</span></span>

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample6.cs)]

<span data-ttu-id="27afe-145">`loud-1` CSS 类可使日期显示为粗体文本。</span><span class="sxs-lookup"><span data-stu-id="27afe-145">The `loud-1` CSS class causes the date to be display in bold red text.</span></span> <span data-ttu-id="27afe-146">你添加了 `loud-1` CSS 类，就像是一个临时的度量，因此你可以轻松地查看使用此特定模板的时间。</span><span class="sxs-lookup"><span data-stu-id="27afe-146">You added the `loud-1` CSS class just as a temporary measure so you can easily see when this particular template is being used.</span></span>

<span data-ttu-id="27afe-147">已创建的内容，以及 ASP.NET 将用于显示日期的自定义模板。</span><span class="sxs-lookup"><span data-stu-id="27afe-147">What you've done is created and customized templates that ASP.NET will use to display dates.</span></span> <span data-ttu-id="27afe-148">更常规的模板（在*Views\Shared\DisplayTemplates*文件夹中）显示一个简单的短日期。</span><span class="sxs-lookup"><span data-stu-id="27afe-148">The more general template (in the *Views\Shared\DisplayTemplates* folder) displays a simple short date.</span></span> <span data-ttu-id="27afe-149">专门用于 `Movie` 控制器的模板（在*Views\Movies\DisplayTemplates*文件夹中）将显示一个也设置为粗体红色文本的短日期。</span><span class="sxs-lookup"><span data-stu-id="27afe-149">The template that's specifically for the `Movie` controller (in the *Views\Movies\DisplayTemplates* folder) displays a short date that's also formatted as bold red text.</span></span>

<span data-ttu-id="27afe-150">按 Ctrl+F5 以运行应用程序。</span><span class="sxs-lookup"><span data-stu-id="27afe-150">Press CTRL+F5 to run the application.</span></span> <span data-ttu-id="27afe-151">浏览器呈现应用程序的索引视图。</span><span class="sxs-lookup"><span data-stu-id="27afe-151">The browser renders the Index view for the application.</span></span>

<span data-ttu-id="27afe-152">`ReleaseDate` 属性现在以粗体显示日期，而不显示时间。这可以帮助你确认*Views\Movies\DisplayTemplates*文件夹中的 `DateTime` 模板化帮助器是在共享文件夹（*Views\Shared\DisplayTemplates*）中的 `DateTime` 模板化帮助器上选择的。</span><span class="sxs-lookup"><span data-stu-id="27afe-152">The `ReleaseDate` property now displays the date in a bold red font without the time.This helps you confirm that the `DateTime` templated helper in the *Views\Movies\DisplayTemplates* folder is selected over the `DateTime` templated helper in the shared folder (*Views\Shared\DisplayTemplates*).</span></span>

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/_static/image4.png)

<span data-ttu-id="27afe-153">现在，将*Views\Movies\DisplayTemplates\DateTime.cshtml*文件重命名为*Views\Movies\DisplayTemplates\LoudDateTime.cshtml*。</span><span class="sxs-lookup"><span data-stu-id="27afe-153">Now rename the *Views\Movies\DisplayTemplates\DateTime.cshtml* file to *Views\Movies\DisplayTemplates\LoudDateTime.cshtml*.</span></span>

<span data-ttu-id="27afe-154">按 Ctrl+F5 以运行应用程序。</span><span class="sxs-lookup"><span data-stu-id="27afe-154">Press CTRL+F5 to run the application.</span></span>

<span data-ttu-id="27afe-155">这次 `ReleaseDate` 属性显示一个日期，该日期没有时间且不带粗体。</span><span class="sxs-lookup"><span data-stu-id="27afe-155">This time the `ReleaseDate` property displays a date without the time and without the bold red font.</span></span> <span data-ttu-id="27afe-156">这说明了具有数据类型名称（在本例中为 `DateTime`）的模板会自动用于显示该类型的所有模型属性。</span><span class="sxs-lookup"><span data-stu-id="27afe-156">This illustrates that a template that has the name of the data type (in this case `DateTime`) is automatically used to display all model properties of that type.</span></span> <span data-ttu-id="27afe-157">将 LoudDateTime*文件重*命名为后，ASP.NET 不再在*Views\Movies\DisplayTemplates*文件夹中找到模板，因此它使用了 \*\* *Views\Movies\Shared 中的模板。*</span><span class="sxs-lookup"><span data-stu-id="27afe-157">After you renamed the *DateTime.cshtml* file to *LoudDateTime.cshtml*, ASP.NET no longer found a template in the *Views\Movies\DisplayTemplates* folder, so it used the *DateTime.cshtml* template from the \*Views\Movies\Shared\* folder.</span></span>

<span data-ttu-id="27afe-158">（模板匹配不区分大小写，因此你可以创建具有任何大小写形式的模板文件名。</span><span class="sxs-lookup"><span data-stu-id="27afe-158">(The template matching is case insensitive, so you could have created the template file name with any casing.</span></span> <span data-ttu-id="27afe-159">例如， *datetime. cshtml、datetime.* *cshtml 和 datetime. cshtml*都与 `DateTime` 类型匹配。）</span><span class="sxs-lookup"><span data-stu-id="27afe-159">For example, *DATETIME.cshtml, datetime.cshtml*, and *DaTeTiMe.cshtml* would all match the `DateTime` type.)</span></span>

<span data-ttu-id="27afe-160">若要查看：此时将使用*Views\Movies\DisplayTemplates\DateTime.cshtml*模板显示 "`ReleaseDate`" 字段，该模板使用短日期格式显示数据，否则不添加任何特殊格式。</span><span class="sxs-lookup"><span data-stu-id="27afe-160">To review: at this point, the `ReleaseDate` field is being displayed using the *Views\Movies\DisplayTemplates\DateTime.cshtml* template, which displays the data using a short date format, but otherwise adds no special format.</span></span>

### <a name="using-uihint-to-specify-a-display-template"></a><span data-ttu-id="27afe-161">使用 UIHint 指定显示模板</span><span class="sxs-lookup"><span data-stu-id="27afe-161">Using UIHint to Specify a Display Template</span></span>

<span data-ttu-id="27afe-162">如果你的 web 应用程序有许多 `DateTime` 字段，并且默认情况下，你想要以仅限日期的格式显示全部或大部分字段，则可以使用*DateTime. cshtml*模板。</span><span class="sxs-lookup"><span data-stu-id="27afe-162">If your web application has many `DateTime` fields and by default you want to display all or most of them in date-only format, the *DateTime.cshtml* template is a good approach.</span></span> <span data-ttu-id="27afe-163">但如果您有几个日期要显示完整的日期和时间怎么办？</span><span class="sxs-lookup"><span data-stu-id="27afe-163">But what if you have a few dates where you want to display the full date and time?</span></span> <span data-ttu-id="27afe-164">没问题。</span><span class="sxs-lookup"><span data-stu-id="27afe-164">No problem.</span></span> <span data-ttu-id="27afe-165">你可以创建一个附加模板，并使用[UIHint](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.uihintattribute.uihint.aspx)属性来指定完整日期和时间的格式设置。</span><span class="sxs-lookup"><span data-stu-id="27afe-165">You can create an additional template and use the [UIHint](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.uihintattribute.uihint.aspx) attribute to specify formatting for the full date and time.</span></span> <span data-ttu-id="27afe-166">然后，可以有选择地应用该模板。</span><span class="sxs-lookup"><span data-stu-id="27afe-166">You can then selectively apply that template.</span></span> <span data-ttu-id="27afe-167">您可以在模型级别使用[UIHint](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.uihintattribute.uihint.aspx)属性，也可以在视图内指定模板。</span><span class="sxs-lookup"><span data-stu-id="27afe-167">You can use the [UIHint](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.uihintattribute.uihint.aspx) attribute at the model level or you can specify the template inside a view.</span></span> <span data-ttu-id="27afe-168">在本部分中，你将了解如何使用 `UIHint` 特性为日期时间字段的某些实例有选择地更改格式设置。</span><span class="sxs-lookup"><span data-stu-id="27afe-168">In this section, you'll see how to use the `UIHint` attribute to selectively change the formatting for some instances of date-time fields.</span></span>

<span data-ttu-id="27afe-169">打开*Views\Movies\DisplayTemplates\LoudDateTime.cshtml*文件，并将现有代码替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="27afe-169">Open the *Views\Movies\DisplayTemplates\LoudDateTime.cshtml* file and replace the existing code with the following:</span></span>

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample7.cshtml)]

<span data-ttu-id="27afe-170">这将导致显示完整的日期和时间，并添加使文本变为绿色和较大的 CSS 类。</span><span class="sxs-lookup"><span data-stu-id="27afe-170">This causes the full date and time to be displayed and adds the CSS class that makes the text green and large.</span></span>

<span data-ttu-id="27afe-171">打开*Movie.cs*文件，并将[UIHint](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.uihintattribute.uihint.aspx)属性添加到 `ReleaseDate` 属性，如以下示例中所示：</span><span class="sxs-lookup"><span data-stu-id="27afe-171">Open the *Movie.cs* file and add the [UIHint](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.uihintattribute.uihint.aspx) attribute to the `ReleaseDate` property, as shown in the following example:</span></span>

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample8.cs)]

<span data-ttu-id="27afe-172">这会告知 ASP.NET MVC 当它显示 `ReleaseDate` 属性时（具体而言，并不只是任何 `DateTime` 对象），它应使用*LoudDateTime*模板。</span><span class="sxs-lookup"><span data-stu-id="27afe-172">This tells ASP.NET MVC that when it displays the `ReleaseDate` property (specifically, and not just any `DateTime` object), it should use the *LoudDateTime.cshtml* template.</span></span>

<span data-ttu-id="27afe-173">按 Ctrl+F5 以运行应用程序。</span><span class="sxs-lookup"><span data-stu-id="27afe-173">Press CTRL+F5 to run the application.</span></span>

<span data-ttu-id="27afe-174">请注意，`ReleaseDate` 属性现在以大绿色字体显示日期和时间。</span><span class="sxs-lookup"><span data-stu-id="27afe-174">Notice that the `ReleaseDate` property now displays the date and time in a large green font.</span></span>

<span data-ttu-id="27afe-175">返回*Movie.cs*文件中的 `UIHint` 属性，将其注释掉，以便不使用*LoudDateTime*模板。</span><span class="sxs-lookup"><span data-stu-id="27afe-175">Return to the `UIHint` attribute in the *Movie.cs* file and comment it out so the *LoudDateTime.cshtml* template won't be used.</span></span> <span data-ttu-id="27afe-176">再次运行该应用程序。</span><span class="sxs-lookup"><span data-stu-id="27afe-176">Run the application again.</span></span> <span data-ttu-id="27afe-177">发布日期不会显示为 "大" 和 "绿色"。</span><span class="sxs-lookup"><span data-stu-id="27afe-177">The release date is not displayed large and green.</span></span> <span data-ttu-id="27afe-178">这会验证 "索引" 和 "详细信息" 视图中是否使用了*Views\Shared\DisplayTemplates\DateTime.cshtml*模板。</span><span class="sxs-lookup"><span data-stu-id="27afe-178">This verifies that the *Views\Shared\DisplayTemplates\DateTime.cshtml* template is used in the Index and Details views.</span></span>

<span data-ttu-id="27afe-179">如前文所述，还可以在视图中应用模板，这样就可以将模板应用于某些数据的单个实例。</span><span class="sxs-lookup"><span data-stu-id="27afe-179">As mentioned earlier, you can also apply a template in a view, which lets you apply the template to an individual instance of some data.</span></span> <span data-ttu-id="27afe-180">打开 " *Views\Movies\Details.cshtml* " 视图。</span><span class="sxs-lookup"><span data-stu-id="27afe-180">Open the *Views\Movies\Details.cshtml* view.</span></span> <span data-ttu-id="27afe-181">添加 `"LoudDateTime"` 作为 `ReleaseDate` 字段的[DisplayFor](https://msdn.microsoft.com/library/ee407420.aspx)调用的第二个参数。</span><span class="sxs-lookup"><span data-stu-id="27afe-181">Add `"LoudDateTime"` as the second parameter of the [Html.DisplayFor](https://msdn.microsoft.com/library/ee407420.aspx) call for the `ReleaseDate` field.</span></span> <span data-ttu-id="27afe-182">完整代码如下所示：</span><span class="sxs-lookup"><span data-stu-id="27afe-182">The completed code looks like this:</span></span>

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample9.cshtml)]

<span data-ttu-id="27afe-183">这将指定 `LoudDateTime` 模板应用于显示模型属性，而不考虑应用于模型的属性。</span><span class="sxs-lookup"><span data-stu-id="27afe-183">This specifies that the `LoudDateTime` template should be used to display the model property, regardless of what attributes are applied to the model.</span></span>

<span data-ttu-id="27afe-184">按 Ctrl+F5 以运行应用程序。</span><span class="sxs-lookup"><span data-stu-id="27afe-184">Press CTRL+F5 to run the application.</span></span>

<span data-ttu-id="27afe-185">验证电影索引页使用的是*Views\Shared\DisplayTemplates\DateTime.cshtml*模板（红色粗体），并且*Movie\Details*页使用的是*Views\Movies\DisplayTemplates\LoudDateTime.cshtml*模板（大和绿色）。</span><span class="sxs-lookup"><span data-stu-id="27afe-185">Verify that the movie index page is using the *Views\Shared\DisplayTemplates\DateTime.cshtml* template (red bold) and the *Movie\Details* page is using the *Views\Movies\DisplayTemplates\LoudDateTime.cshtml* template (large and green).</span></span>

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/_static/image5.png)

<span data-ttu-id="27afe-186">在下一部分中，你将为复杂类型创建模板。</span><span class="sxs-lookup"><span data-stu-id="27afe-186">In the next section, you'll create a template for a complex type.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="27afe-187">[上一页](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-1.md)
> [下一页](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3.md)</span><span class="sxs-lookup"><span data-stu-id="27afe-187">[Previous](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-1.md)
[Next](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3.md)</span></span>
