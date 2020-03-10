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
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78433214"
---
# <a name="using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc---part-3"></a>将 HTML5 和 jQuery UI Datepicker 快捷日历与 ASP.NET MVC 一起使用-第3部分

作者： [Rick Anderson](https://twitter.com/RickAndMSFT)

> 本教程将指导你了解如何在 ASP.NET MVC Web 应用程序中使用编辑器模板、显示模板和 jQuery UI datepicker 快捷日历。

## <a name="working-with-complex-types"></a>使用复杂类型

在本部分中，你将创建一个地址类，并了解如何创建模板来显示它。

在 "*模型*" 文件夹中，创建一个名为*Person.cs*的新类文件，在其中放置两个类型：一个 `Person` 类和一个 `Address` 类。 `Person` 类将包含类型化为 `Address`的属性。 `Address` 类型是一种复杂类型，这意味着它不是 `int`、`string`或 `double`之类的内置类型之一。 相反，它具有多个属性。 新类的代码如下所示：

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample1.cs)]

在 `Movie` 控制器中，添加以下 `PersonDetail` 操作以显示 person 实例：

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample2.cs)]

然后，将以下代码添加到 `Movie` 控制器，用一些示例数据填充 `Person` 模型：

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample3.cs)]

打开*Views\Movies\PersonDetail.cshtml*文件并为 "`PersonDetail`" 视图添加以下标记。

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample4.cshtml)]

按 Ctrl + F5 运行应用程序并导航到*电影/PersonDetail*。

`PersonDetail` 视图不包含 `Address` 复杂类型，如此屏幕截图中所示。 （不显示地址。）

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/_static/image1.png)

不显示 `Address` 模型数据，因为它是复杂类型。 若要显示地址信息，请再次打开*Views\Movies\PersonDetail.cshtml*文件并添加以下标记。

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample5.cshtml)]

现在 `PersonDetail` 视图的完整标记如下所示：

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample6.cshtml)]

再次运行该应用程序并显示 `PersonDetail` 视图。 现在会显示地址信息：

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/_static/image2.png)

### <a name="creating-a-template-for-a-complex-type"></a>为复杂类型创建模板

在本部分中，你将创建一个模板，该模板将用于呈现 `Address` 复杂类型。 为 `Address` 类型创建模板时，ASP.NET MVC 可以自动使用它在应用程序中的任何位置格式化地址模型。 这使你可以仅从应用程序中的一个位置控制 `Address` 类型的呈现。

在*Views\Shared\DisplayTemplates*文件夹中，创建名为**Address**的强类型分部视图：

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/_static/image3.png)

单击 "**添加**"，然后打开新的*Views\Shared\DisplayTemplates\Address.cshtml*文件。 新视图包含以下生成的标记：

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample7.cshtml)]

运行应用程序并显示 "`PersonDetail`" 视图。 此时，您刚刚创建的 `Address` 模板用于显示 `Address` 复杂类型，因此显示如下所示：

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/_static/image4.png)

### <a name="summary-ways-to-specify-the-model-display-format-and-template"></a>摘要：指定模型显示格式和模板的方法

您已经了解到，您可以使用以下方法为模型属性指定格式或模板：

- 将 `DisplayFormat` 特性应用于模型中的属性。 例如，以下代码将导致显示不带时间的日期：

    [!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample8.cs)]
- 将[DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx)特性应用于模型中的属性并指定数据类型。 例如，以下代码将导致显示不带时间的日期。

    [!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample9.cs)]

    如果应用程序在*Views\Shared\DisplayTemplates*文件夹或*Views\Movies\DisplayTemplates*文件夹中包含一个*日期 cshtml*模板，则该模板将用于呈现 `DateTime` 属性。 否则，内置 ASP.NET 模板系统会将属性显示为日期。
- 在*Views\Shared\DisplayTemplates*文件夹或*Views\Movies\DisplayTemplates*文件夹中创建一个显示模板，其名称与要设置格式的数据类型相匹配。 例如，你发现*Views\Shared\DisplayTemplates\DateTime.cshtml*用于呈现模型中 `DateTime` 属性，而无需将属性添加到模型，也不会向视图添加任何标记。
- 使用模型上的[UIHint](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.uihintattribute.uihint.aspx)属性来指定用于显示模型属性的模板。
- 在视图中将显示模板名称显式添加到[DisplayFor](https://msdn.microsoft.com/library/ee407420.aspx)调用。

你使用的方法取决于你需要在应用程序中执行的操作。 混合这些方法以获得所需的格式，这种情况并不常见。

在下一节中，您将稍微切换齿轮，并从自定义数据的显示方式，以自定义如何输入数据。 你将在应用程序的 "编辑" 视图中挂接 jQuery datepicker，以便提供一种巧妙的方法来指定日期。

> [!div class="step-by-step"]
> [上一页](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2.md)
> [下一页](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4.md)
