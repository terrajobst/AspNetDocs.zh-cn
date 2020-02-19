---
uid: mvc/overview/older-versions/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3
title: 将 HTML5 和 jQuery UI Datepicker 快捷日历与 ASP.NET MVC-第3部分 |Microsoft Docs
author: Rick-Anderson
description: 本教程将指导你了解如何在 ASP.NET MV ... 中使用编辑器模板、显示模板和 jQuery UI datepicker 快捷日历
ms.author: riande
ms.date: 08/29/2011
ms.assetid: 8f5f91ae-12d7-4cf3-ac09-4bb53d07ee60
msc.legacyurl: /mvc/overview/older-versions/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3
msc.type: authoredcontent
ms.openlocfilehash: b3249397e54e64538c4dc78e5fe8b94656e8962b
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457890"
---
# <a name="using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc---part-3"></a><span data-ttu-id="3c8c5-103">将 HTML5 和 jQuery UI Datepicker 快捷日历与 ASP.NET MVC 一起使用-第3部分</span><span class="sxs-lookup"><span data-stu-id="3c8c5-103">Using the HTML5 and jQuery UI Datepicker Popup Calendar with ASP.NET MVC - Part 3</span></span>

<span data-ttu-id="3c8c5-104">作者： [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="3c8c5-104">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

> <span data-ttu-id="3c8c5-105">本教程将指导你了解如何在 ASP.NET MVC Web 应用程序中使用编辑器模板、显示模板和 jQuery UI datepicker 快捷日历。</span><span class="sxs-lookup"><span data-stu-id="3c8c5-105">This tutorial will teach you the basics of how to work with editor templates, display templates, and the jQuery UI datepicker popup calendar in an ASP.NET MVC Web application.</span></span>

## <a name="working-with-complex-types"></a><span data-ttu-id="3c8c5-106">使用复杂类型</span><span class="sxs-lookup"><span data-stu-id="3c8c5-106">Working with Complex Types</span></span>

<span data-ttu-id="3c8c5-107">在本部分中，你将创建一个地址类，并了解如何创建模板来显示它。</span><span class="sxs-lookup"><span data-stu-id="3c8c5-107">In this section you'll create an address class and learn how to create a template to display it.</span></span>

<span data-ttu-id="3c8c5-108">在 "*模型*" 文件夹中，创建一个名为*Person.cs*的新类文件，在其中放置两个类型：一个 `Person` 类和一个 `Address` 类。</span><span class="sxs-lookup"><span data-stu-id="3c8c5-108">In the *Models* folder, create a new class file named *Person.cs* where you'll put two types: a `Person` class and an `Address` class.</span></span> <span data-ttu-id="3c8c5-109">`Person` 类将包含类型化为 `Address`的属性。</span><span class="sxs-lookup"><span data-stu-id="3c8c5-109">The `Person` class will contain a property that's typed as `Address`.</span></span> <span data-ttu-id="3c8c5-110">`Address` 类型是一种复杂类型，这意味着它不是 `int`、`string`或 `double`之类的内置类型之一。</span><span class="sxs-lookup"><span data-stu-id="3c8c5-110">The `Address` type is a complex type, meaning it's not one of the built-in types like `int`, `string`, or `double`.</span></span> <span data-ttu-id="3c8c5-111">相反，它具有多个属性。</span><span class="sxs-lookup"><span data-stu-id="3c8c5-111">Instead, it has several properties.</span></span> <span data-ttu-id="3c8c5-112">新类的代码如下所示：</span><span class="sxs-lookup"><span data-stu-id="3c8c5-112">The code for the new classes looks like this:</span></span>

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample1.cs)]

<span data-ttu-id="3c8c5-113">在 `Movie` 控制器中，添加以下 `PersonDetail` 操作以显示 person 实例：</span><span class="sxs-lookup"><span data-stu-id="3c8c5-113">In the `Movie` controller, add the following `PersonDetail` action to display a person instance:</span></span>

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample2.cs)]

<span data-ttu-id="3c8c5-114">然后，将以下代码添加到 `Movie` 控制器，用一些示例数据填充 `Person` 模型：</span><span class="sxs-lookup"><span data-stu-id="3c8c5-114">Then add the following code to the `Movie` controller to populate the `Person` model with some sample data:</span></span>

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample3.cs)]

<span data-ttu-id="3c8c5-115">打开*Views\Movies\PersonDetail.cshtml*文件并为 "`PersonDetail`" 视图添加以下标记。</span><span class="sxs-lookup"><span data-stu-id="3c8c5-115">Open the *Views\Movies\PersonDetail.cshtml* file and add the following markup for the `PersonDetail` view.</span></span>

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample4.cshtml)]

<span data-ttu-id="3c8c5-116">按 Ctrl + F5 运行应用程序并导航到*电影/PersonDetail*。</span><span class="sxs-lookup"><span data-stu-id="3c8c5-116">Press Ctrl+F5 to run the application and navigate to *Movies/PersonDetail*.</span></span>

<span data-ttu-id="3c8c5-117">`PersonDetail` 视图不包含 `Address` 复杂类型，如此屏幕截图中所示。</span><span class="sxs-lookup"><span data-stu-id="3c8c5-117">The `PersonDetail` view doesn't contain the `Address` complex type, as you can see in this screenshot.</span></span> <span data-ttu-id="3c8c5-118">（不显示地址。）</span><span class="sxs-lookup"><span data-stu-id="3c8c5-118">(No address is shown.)</span></span>

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/_static/image1.png)

<span data-ttu-id="3c8c5-119">不显示 `Address` 模型数据，因为它是复杂类型。</span><span class="sxs-lookup"><span data-stu-id="3c8c5-119">The `Address` model data is not displayed because it's a complex type.</span></span> <span data-ttu-id="3c8c5-120">若要显示地址信息，请再次打开*Views\Movies\PersonDetail.cshtml*文件并添加以下标记。</span><span class="sxs-lookup"><span data-stu-id="3c8c5-120">To display the address information, open the *Views\Movies\PersonDetail.cshtml* file again and add the following markup.</span></span>

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample5.cshtml)]

<span data-ttu-id="3c8c5-121">现在 `PersonDetail` 视图的完整标记如下所示：</span><span class="sxs-lookup"><span data-stu-id="3c8c5-121">The complete markup for the `PersonDetail` now view looks like this:</span></span>

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample6.cshtml)]

<span data-ttu-id="3c8c5-122">再次运行该应用程序并显示 `PersonDetail` 视图。</span><span class="sxs-lookup"><span data-stu-id="3c8c5-122">Run the application again and display the `PersonDetail` view.</span></span> <span data-ttu-id="3c8c5-123">现在会显示地址信息：</span><span class="sxs-lookup"><span data-stu-id="3c8c5-123">The address information is now displayed:</span></span>

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/_static/image2.png)

### <a name="creating-a-template-for-a-complex-type"></a><span data-ttu-id="3c8c5-124">为复杂类型创建模板</span><span class="sxs-lookup"><span data-stu-id="3c8c5-124">Creating a Template for a Complex Type</span></span>

<span data-ttu-id="3c8c5-125">在本部分中，你将创建一个模板，该模板将用于呈现 `Address` 复杂类型。</span><span class="sxs-lookup"><span data-stu-id="3c8c5-125">In this section you'll create a template that will be used to render the `Address` complex type.</span></span> <span data-ttu-id="3c8c5-126">为 `Address` 类型创建模板时，ASP.NET MVC 可以自动使用它在应用程序中的任何位置格式化地址模型。</span><span class="sxs-lookup"><span data-stu-id="3c8c5-126">When you create a template for the `Address` type, ASP.NET MVC can automatically use it to format an address model anywhere in the application.</span></span> <span data-ttu-id="3c8c5-127">这使你可以仅从应用程序中的一个位置控制 `Address` 类型的呈现。</span><span class="sxs-lookup"><span data-stu-id="3c8c5-127">This gives you a way to control the rendering of the `Address` type from just one place in the application.</span></span>

<span data-ttu-id="3c8c5-128">在*Views\Shared\DisplayTemplates*文件夹中，创建名为**Address**的强类型分部视图：</span><span class="sxs-lookup"><span data-stu-id="3c8c5-128">In the *Views\Shared\DisplayTemplates* folder, create a strongly typed partial view named **Address**:</span></span>

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/_static/image3.png)

<span data-ttu-id="3c8c5-129">单击 "**添加**"，然后打开新的*Views\Shared\DisplayTemplates\Address.cshtml*文件。</span><span class="sxs-lookup"><span data-stu-id="3c8c5-129">Click **Add**, and then open the new *Views\Shared\DisplayTemplates\Address.cshtml* file.</span></span> <span data-ttu-id="3c8c5-130">新视图包含以下生成的标记：</span><span class="sxs-lookup"><span data-stu-id="3c8c5-130">The new view contains the following generated markup:</span></span>

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample7.cshtml)]

<span data-ttu-id="3c8c5-131">运行应用程序并显示 "`PersonDetail`" 视图。</span><span class="sxs-lookup"><span data-stu-id="3c8c5-131">Run the application and display the `PersonDetail` view.</span></span> <span data-ttu-id="3c8c5-132">此时，您刚刚创建的 `Address` 模板用于显示 `Address` 复杂类型，因此显示如下所示：</span><span class="sxs-lookup"><span data-stu-id="3c8c5-132">This time, the `Address` template that you just created is used to display the `Address` complex type, so the display looks like the following:</span></span>

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/_static/image4.png)

### <a name="summary-ways-to-specify-the-model-display-format-and-template"></a><span data-ttu-id="3c8c5-133">摘要：指定模型显示格式和模板的方法</span><span class="sxs-lookup"><span data-stu-id="3c8c5-133">Summary: Ways to Specify the Model Display Format and Template</span></span>

<span data-ttu-id="3c8c5-134">您已经了解到，您可以使用以下方法为模型属性指定格式或模板：</span><span class="sxs-lookup"><span data-stu-id="3c8c5-134">You've seen that you can specify the format or template for a model property by using the following approaches:</span></span>

- <span data-ttu-id="3c8c5-135">将 `DisplayFormat` 特性应用于模型中的属性。</span><span class="sxs-lookup"><span data-stu-id="3c8c5-135">Applying the `DisplayFormat` attribute to a property in the model.</span></span> <span data-ttu-id="3c8c5-136">例如，以下代码将导致显示不带时间的日期：</span><span class="sxs-lookup"><span data-stu-id="3c8c5-136">For example, the following code causes the date to be displayed without the time:</span></span>

    [!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample8.cs)]
- <span data-ttu-id="3c8c5-137">将[DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx)特性应用于模型中的属性并指定数据类型。</span><span class="sxs-lookup"><span data-stu-id="3c8c5-137">Applying a [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) attribute to a property in the model and specifying the data type.</span></span> <span data-ttu-id="3c8c5-138">例如，以下代码将导致显示不带时间的日期。</span><span class="sxs-lookup"><span data-stu-id="3c8c5-138">For example, the following code causes the date to be displayed without the time.</span></span>

    [!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample9.cs)]

    <span data-ttu-id="3c8c5-139">如果应用程序在*Views\Shared\DisplayTemplates*文件夹或*Views\Movies\DisplayTemplates*文件夹中包含一个*日期 cshtml*模板，则该模板将用于呈现 `DateTime` 属性。</span><span class="sxs-lookup"><span data-stu-id="3c8c5-139">If the application contains a *date.cshtml* template in the *Views\Shared\DisplayTemplates* folder or the *Views\Movies\DisplayTemplates* folder, that template will be used to render the `DateTime` property.</span></span> <span data-ttu-id="3c8c5-140">否则，内置 ASP.NET 模板系统会将属性显示为日期。</span><span class="sxs-lookup"><span data-stu-id="3c8c5-140">Otherwise the built-in ASP.NET templating system displays the property as a date.</span></span>
- <span data-ttu-id="3c8c5-141">在*Views\Shared\DisplayTemplates*文件夹或*Views\Movies\DisplayTemplates*文件夹中创建一个显示模板，其名称与要设置格式的数据类型相匹配。</span><span class="sxs-lookup"><span data-stu-id="3c8c5-141">Creating a display template in the *Views\Shared\DisplayTemplates* folder or the *Views\Movies\DisplayTemplates* folder whose name matches the data type that you want to format.</span></span> <span data-ttu-id="3c8c5-142">例如，你发现*Views\Shared\DisplayTemplates\DateTime.cshtml*用于呈现模型中 `DateTime` 属性，而无需将属性添加到模型，也不会向视图添加任何标记。</span><span class="sxs-lookup"><span data-stu-id="3c8c5-142">For example, you saw that the *Views\Shared\DisplayTemplates\DateTime.cshtml* was used to render `DateTime` properties in a model, without adding an attribute to the model and without adding any markup to views.</span></span>
- <span data-ttu-id="3c8c5-143">使用模型上的[UIHint](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.uihintattribute.uihint.aspx)属性来指定用于显示模型属性的模板。</span><span class="sxs-lookup"><span data-stu-id="3c8c5-143">Using the [UIHint](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.uihintattribute.uihint.aspx) attribute on the model to specify the template to display the model property.</span></span>
- <span data-ttu-id="3c8c5-144">在视图中将显示模板名称显式添加到[DisplayFor](https://msdn.microsoft.com/library/ee407420.aspx)调用。</span><span class="sxs-lookup"><span data-stu-id="3c8c5-144">Explicitly adding the display template name to the [Html.DisplayFor](https://msdn.microsoft.com/library/ee407420.aspx) call in a view.</span></span>

<span data-ttu-id="3c8c5-145">你使用的方法取决于你需要在应用程序中执行的操作。</span><span class="sxs-lookup"><span data-stu-id="3c8c5-145">The approach you use depends on what you need to do in your application.</span></span> <span data-ttu-id="3c8c5-146">混合这些方法以获得所需的格式，这种情况并不常见。</span><span class="sxs-lookup"><span data-stu-id="3c8c5-146">It's not uncommon to mix these approaches to get exactly the kind of formatting that you need.</span></span>

<span data-ttu-id="3c8c5-147">在下一节中，您将稍微切换齿轮，并从自定义数据的显示方式，以自定义如何输入数据。</span><span class="sxs-lookup"><span data-stu-id="3c8c5-147">In the next section, you'll switch gears a bit and move from customizing how data is displayed to customizing how it's entered.</span></span> <span data-ttu-id="3c8c5-148">你将在应用程序的 "编辑" 视图中挂接 jQuery datepicker，以便提供一种巧妙的方法来指定日期。</span><span class="sxs-lookup"><span data-stu-id="3c8c5-148">You'll hook up the jQuery datepicker to the edit views in the application in order to provide a slick way to specify dates.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="3c8c5-149">[上一页](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2.md)
> [下一页](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4.md)</span><span class="sxs-lookup"><span data-stu-id="3c8c5-149">[Previous](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2.md)
[Next](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4.md)</span></span>
