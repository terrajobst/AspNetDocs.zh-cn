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
# <a name="using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc---part-2"></a>将 HTML5 和 jQuery UI Datepicker 快捷日历与 ASP.NET MVC 一起使用-第2部分

作者： [Rick Anderson](https://twitter.com/RickAndMSFT)

> 本教程将指导你了解如何在 ASP.NET MVC Web 应用程序中使用编辑器模板、显示模板和 jQuery UI datepicker 快捷日历。

## <a name="adding-an-automatic-datetime-template"></a>添加自动日期时间模板

在本教程的第一部分中，您看到了如何向模型添加属性以显式指定格式设置，以及如何显式指定用于呈现模型的模板。 例如，以下代码中的[DisplayFormat](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx)属性显式指定 `ReleaseDate` 属性的格式。

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample1.cs)]

在下面的示例中，使用 `Date` 枚举的[DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx)特性指定应使用日期模板来呈现模型。 如果项目中没有日期模板，则使用内置日期模板。

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample2.cs)]

但 ASP。通过查找与类型名称匹配的模板，MVC 可以使用配置上的规则执行类型匹配。 这样，便可以创建一个自动设置数据格式的模板，而无需使用任何属性或代码。 对于本教程的本部分，你将创建一个模板，该模板将自动应用于类型为[DateTime](https://msdn.microsoft.com/library/system.datetime.aspx)的模型属性。 您无需使用特性或其他配置来指定应使用该模板来呈现类型为[DateTime](https://msdn.microsoft.com/library/system.datetime.aspx)的所有模型属性。

您还将学习如何自定义单个属性的显示，甚至是单个字段的显示方式。

首先，让我们删除现有格式设置信息，并在应用程序中显示完整的日期。

打开*Movie.cs*文件，并在 `ReleaseDate` 属性上注释掉 `DataType` 特性：

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample3.cs)]

按 Ctrl+F5 以运行应用程序。

请注意，`ReleaseDate` 属性现在同时显示日期和时间，因为在未提供格式设置信息时，这是默认值。

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/_static/image1.png)

### <a name="adding-css-styles-for-testing-new-templates"></a>添加 CSS 样式以测试新模板

在创建用于设置日期格式的模板之前，你将添加几个可应用于新模板的 CSS 样式规则。 这将帮助你验证呈现的页面是否正在使用新模板。

打开*Content\Site.cs*文件，并将以下 CSS 规则添加到文件底部：

[!code-css[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample4.css)]

### <a name="adding-datetime-display-templates"></a>添加 DateTime 显示模板

现在可以创建新模板。 在*Views\Movies*文件夹中，创建*DisplayTemplates*文件夹。

在*Views\Shared*文件夹中，创建*DisplayTemplates*文件夹和*EditorTemplates*文件夹。

所有控制器将使用*Views\Shared\DisplayTemplates*文件夹中的显示模板。 *Views\Movie\DisplayTemplates*文件夹中的显示模板将仅由 `Movie` 控制器使用。 （如果两个文件夹中都出现具有相同名称的模板，则*Views\Movie\DisplayTemplates*文件夹中的模板（即，更具体的模板）优先于 `Movie` 控制器返回的视图。）

在**解决方案资源管理器**中，展开 " *Views* " 文件夹，展开*共享*文件夹，然后右键单击*Views\Shared\DisplayTemplates*文件夹。

单击 "**添加**"，然后单击 "**查看**"。 将显示 "**添加视图**" 对话框。

在 "**视图名称**" 框中，键入 `DateTime`。 （必须使用此名称才能匹配类型的名称。）

选中 "**作为分部视图创建**" 复选框。 请确保未选中 "**使用布局或母版页**" 和 "**创建强类型视图**" 复选框。

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/_static/image2.png)

单击 **“添加”** 。 在*Views\Shared\DisplayTemplates*中创建一个*日期时间的日期。*

下图显示了在创建 `DateTime` 显示和编辑器模板之后**解决方案资源管理器**中的*Views*文件夹。

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/_static/image3.png)

打开*Views\Shared\DisplayTemplates\DateTime.cshtml*文件并添加以下标记，该标记使用[字符串. format](https://msdn.microsoft.com/library/system.string.format.aspx)方法将属性的格式设置为不带时间的日期。 （`{0:d}` 格式指定短日期格式。）

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample5.cs)]

重复此步骤，在*Views\Movie\DisplayTemplates*文件夹中创建 `DateTime` 模板。 在*Views\Movie\DisplayTemplates\DateTime.cshtml*文件中使用以下代码。

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample6.cs)]

`loud-1` CSS 类可使日期显示为粗体文本。 你添加了 `loud-1` CSS 类，就像是一个临时的度量，因此你可以轻松地查看使用此特定模板的时间。

已创建的内容，以及 ASP.NET 将用于显示日期的自定义模板。 更常规的模板（在*Views\Shared\DisplayTemplates*文件夹中）显示一个简单的短日期。 专门用于 `Movie` 控制器的模板（在*Views\Movies\DisplayTemplates*文件夹中）将显示一个也设置为粗体红色文本的短日期。

按 Ctrl+F5 以运行应用程序。 浏览器呈现应用程序的索引视图。

`ReleaseDate` 属性现在以粗体显示日期，而不显示时间。这可以帮助你确认*Views\Movies\DisplayTemplates*文件夹中的 `DateTime` 模板化帮助器是在共享文件夹（*Views\Shared\DisplayTemplates*）中的 `DateTime` 模板化帮助器上选择的。

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/_static/image4.png)

现在，将*Views\Movies\DisplayTemplates\DateTime.cshtml*文件重命名为*Views\Movies\DisplayTemplates\LoudDateTime.cshtml*。

按 Ctrl+F5 以运行应用程序。

这次 `ReleaseDate` 属性显示一个日期，该日期没有时间且不带粗体。 这说明了具有数据类型名称（在本例中为 `DateTime`）的模板会自动用于显示该类型的所有模型属性。 将 LoudDateTime*文件重*命名为后，ASP.NET 不再在*Views\Movies\DisplayTemplates*文件夹中找到模板，因此它使用了 *\* *Views\Movies\Shared 中的模板。*

（模板匹配不区分大小写，因此你可以创建具有任何大小写形式的模板文件名。 例如， *datetime. cshtml、datetime.* *cshtml 和 datetime. cshtml*都与 `DateTime` 类型匹配。）

若要查看：此时将使用*Views\Movies\DisplayTemplates\DateTime.cshtml*模板显示 "`ReleaseDate`" 字段，该模板使用短日期格式显示数据，否则不添加任何特殊格式。

### <a name="using-uihint-to-specify-a-display-template"></a>使用 UIHint 指定显示模板

如果你的 web 应用程序有许多 `DateTime` 字段，并且默认情况下，你想要以仅限日期的格式显示全部或大部分字段，则可以使用*DateTime. cshtml*模板。 但如果您有几个日期要显示完整的日期和时间怎么办？ 没问题。 你可以创建一个附加模板，并使用[UIHint](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.uihintattribute.uihint.aspx)属性来指定完整日期和时间的格式设置。 然后，可以有选择地应用该模板。 您可以在模型级别使用[UIHint](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.uihintattribute.uihint.aspx)属性，也可以在视图内指定模板。 在本部分中，你将了解如何使用 `UIHint` 特性为日期时间字段的某些实例有选择地更改格式设置。

打开*Views\Movies\DisplayTemplates\LoudDateTime.cshtml*文件，并将现有代码替换为以下代码：

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample7.cshtml)]

这将导致显示完整的日期和时间，并添加使文本变为绿色和较大的 CSS 类。

打开*Movie.cs*文件，并将[UIHint](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.uihintattribute.uihint.aspx)属性添加到 `ReleaseDate` 属性，如以下示例中所示：

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample8.cs)]

这会告知 ASP.NET MVC 当它显示 `ReleaseDate` 属性时（具体而言，并不只是任何 `DateTime` 对象），它应使用*LoudDateTime*模板。

按 Ctrl+F5 以运行应用程序。

请注意，`ReleaseDate` 属性现在以大绿色字体显示日期和时间。

返回*Movie.cs*文件中的 `UIHint` 属性，将其注释掉，以便不使用*LoudDateTime*模板。 再次运行该应用程序。 发布日期不会显示为 "大" 和 "绿色"。 这会验证 "索引" 和 "详细信息" 视图中是否使用了*Views\Shared\DisplayTemplates\DateTime.cshtml*模板。

如前文所述，还可以在视图中应用模板，这样就可以将模板应用于某些数据的单个实例。 打开 " *Views\Movies\Details.cshtml* " 视图。 添加 `"LoudDateTime"` 作为 `ReleaseDate` 字段的[DisplayFor](https://msdn.microsoft.com/library/ee407420.aspx)调用的第二个参数。 完整代码如下所示：

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample9.cshtml)]

这将指定 `LoudDateTime` 模板应用于显示模型属性，而不考虑应用于模型的属性。

按 Ctrl+F5 以运行应用程序。

验证电影索引页使用的是*Views\Shared\DisplayTemplates\DateTime.cshtml*模板（红色粗体），并且*Movie\Details*页使用的是*Views\Movies\DisplayTemplates\LoudDateTime.cshtml*模板（大和绿色）。

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/_static/image5.png)

在下一部分中，你将为复杂类型创建模板。

> [!div class="step-by-step"]
> [上一页](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-1.md)
> [下一页](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3.md)
