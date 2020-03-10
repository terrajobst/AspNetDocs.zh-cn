---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/adding-validation-to-the-model
title: 向模型添加验证（VB） |Microsoft Docs
author: Rick-Anderson
description: 本教程将教你如何使用 Microsoft Visual Web Developer 2010 Express Service Pack 1 构建 ASP.NET MVC Web 应用程序的基础知识 。
ms.author: riande
ms.date: 01/12/2011
ms.assetid: 878f6c31-972d-45f4-8849-5c633b511409
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/adding-validation-to-the-model
msc.type: authoredcontent
ms.openlocfilehash: 7f3f195bc30ed23a637b59f15e6fc8431e39e217
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78498572"
---
# <a name="adding-validation-to-the-model-vb"></a>向模型添加验证 (VB)

作者： [Rick Anderson](https://twitter.com/RickAndMSFT)

> 本教程将教你如何使用 Microsoft Visual Web Developer 2010 Express Service Pack 1 （Microsoft Visual Studio 免费版）生成 ASP.NET MVC Web 应用程序的基础知识。 在开始之前，请确保已安装下列必备组件。 可以通过单击以下链接安装所有这些[程序： Web 平台安装程序](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)。 或者，你可以使用以下链接单独安装必备组件：
> 
> - [Visual Studio Web Developer Express SP1 必备组件](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [ASP.NET MVC 3 工具更新](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - [SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)（运行时 + 工具支持）
> 
> 如果你使用的是 Visual Studio 2010 而不是 Visual Web Developer 2010，请通过单击以下链接安装必备组件： [Visual Studio 2010 必备组件](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)。
> 
> 本主题附带有 VB.NET 源代码的 Visual Web Developer 项目。 [下载 VB.NET 版本](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098)。 如果愿意C#，请切换到本教程的[ C#版本](../cs/adding-validation-to-the-model.md)。

在本部分中，你将向 `Movie` 模型中添加验证逻辑，并确保每当用户尝试使用应用程序创建或编辑电影时，都会强制执行验证规则。

## <a name="keeping-things-dry"></a>使东西干燥

ASP.NET MVC 的核心设计原则之一是晾干（"不要自我重复"）。 ASP.NET MVC 鼓励您仅指定一次功能或行为，然后让它在应用程序中的任何位置进行反映。 这会减少编写所需的代码量，并使编写的代码更易于维护。

ASP.NET MVC 和实体框架 Code First 提供的验证支持是有效的操作原理示例。 您可以在一个位置以声明方式指定验证规则（在 model 类中），然后在应用程序的任何位置强制执行这些规则。

让我们看看如何在电影应用程序中利用此验证支持。

## <a name="adding-validation-rules-to-the-movie-model"></a>向影片模型添加验证规则

首先，将一些验证逻辑添加到 `Movie` 类。

打开*电影 .vb*文件。 在该文件的顶部添加引用[`System.ComponentModel.DataAnnotations`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx)命名空间的 `Imports` 语句：

[!code-vb[Main](adding-validation-to-the-model/samples/sample1.vb)]

命名空间是 .NET Framework 的一部分。 它提供了一组内置验证特性，可通过声明方式应用于任何类或属性。

现在更新 `Movie` 类，以利用内置[`Required`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx)、 [`StringLength`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx)和[`Range`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.rangeattribute.aspx)验证特性。 使用以下代码作为应用属性的示例。

[!code-vb[Main](adding-validation-to-the-model/samples/sample2.vb)]

验证特性指定要对应用这些特性的模型属性强制执行的行为。 `Required` 特性指示属性必须具有值;在此示例中，电影必须具有 `Title`、`ReleaseDate`、`Genre`和 `Price` 属性的值才能有效。 `Range` 特性将值限制在指定范围内。 `StringLength` 特性使你能够设置字符串属性的最大长度，以及可选的最小长度。

Code First 确保在应用程序将更改保存到数据库中之前，强制执行在模型类上指定的验证规则。 例如，以下代码将在调用 `SaveChanges` 方法时引发异常，因为缺少几个必需的 `Movie` 属性值，并且价格为零（超出有效范围）。

[!code-vb[Main](adding-validation-to-the-model/samples/sample3.vb)]

验证规则由 .NET Framework 自动强制实施有助于提高应用程序的可靠性。 同时它能确保你无法忘记验证某些内容，并防止你无意中将错误数据导入数据库。

下面是已更新的*Movie .vb*文件的完整代码列表：

[!code-vb[Main](adding-validation-to-the-model/samples/sample4.vb)]

## <a name="validation-error-ui-in-aspnet-mvc"></a>ASP.NET MVC 中的验证错误 UI

重新运行应用程序并导航到 */Movies* URL。

单击 "**创建电影**" 链接以添加新电影。 用一些无效值填写表单，然后单击 "**创建**" 按钮。

[![8_validationErrors](adding-validation-to-the-model/_static/image2.png)](adding-validation-to-the-model/_static/image1.png)

请注意表单如何自动使用背景色突出显示包含无效数据的文本框，并在每个文本框旁边发出适当的验证错误消息。 错误消息与您注释 `Movie` 类时指定的错误字符串匹配。 这两个错误都是在客户端（使用 JavaScript）和服务器端（如果用户禁用了 JavaScript）上进行的。

真正的好处是，您无需更改 `MoviesController` 类或*创建 vbhtml*视图中的单个代码行即可启用此验证 UI。 您在本教程前面创建的控制器和视图会自动选取在 `Movie` 模型类上使用特性指定的验证规则。

## <a name="how-validation-occurs-in-the-create-view-and-create-action-method"></a>如何在 "创建视图" 和 "创建操作" 方法中进行验证

你可能想知道在不对控制器或视图中的代码进行任何更新的情况下，验证 UI 是如何生成的。 下一条列表显示了 `MovieController` 类中 `Create` 方法的外观。 在本教程的前面部分中创建它们的方式没有改变。

[!code-vb[Main](adding-validation-to-the-model/samples/sample5.vb)]

第一个操作方法显示初始 Create 窗体。 第二个处理窗体发布。 第二个 `Create` 方法调用 `ModelState.IsValid` 以检查电影是否有任何验证错误。 调用此方法将评估已应用于对象的任何验证特性。 如果对象具有验证错误，则 `Create` 方法将重新出现该窗体。 如果没有错误，此方法则将新电影保存在数据库中。

下面是在本教程的前面部分中基架的*Create vbhtml*视图模板。 以上所示的操作方法使用它来显示初始表单，并在发生错误时重新显示此表单。

[!code-vbhtml[Main](adding-validation-to-the-model/samples/sample6.vbhtml)]

请注意，代码如何使用 `Html.EditorFor` 帮助器来输出每个 `Movie` 属性的 `<input>` 元素。 此帮助器旁边的调用 `Html.ValidationMessageFor` 帮助器方法。 这两个帮助器方法使用由控制器传递到视图的模型对象（在本例中为 `Movie` 对象）。 它们会自动查找在模型上指定的验证属性，并根据需要显示错误消息。

这种方法的真正优点在于，控制器和 Create view 模板都不知道要强制执行的实际验证规则或显示的特定错误消息。 仅可在 `Movie` 类中指定验证规则和错误字符串。

如果以后要更改验证逻辑，可以在一个位置刚好如此。 无需担心对应用程序的不同部分所强制执行规则的方式不一致 - 所有验证逻辑都将定义在一个位置并用于整个应用程序。 这使代码非常简洁，并且更易于维护和改进。 这意味着对 DRY 原则的完全遵守。

## <a name="adding-formatting-to-the-movie-model"></a>向影片模型添加格式设置

打开*电影 .vb*文件。 除了内置的验证特性集外， [`System.ComponentModel.DataAnnotations`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx)命名空间还提供格式特性。 将[`DisplayFormat`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx)特性和[`DataType`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx)枚举值应用于发布日期和价格字段。 下面的代码演示具有相应[`DisplayFormat`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx)特性的 `ReleaseDate` 和 `Price` 属性。

[!code-vb[Main](adding-validation-to-the-model/samples/sample7.vb)]

或者，您可以显式设置[`DataFormatString`](https://msdn.microsoft.com/library/system.string.format.aspx)值。 下面的代码显示具有日期格式字符串（即 "d"）的发布日期属性。 使用此来指定你不希望时间作为发布日期的一部分。

[!code-vb[Main](adding-validation-to-the-model/samples/sample8.vb)]

下面的代码将 `Price` 属性的格式设置为货币。

[!code-vb[Main](adding-validation-to-the-model/samples/sample9.vb)]

完整的 `Movie` 类如下所示。

[!code-vb[Main](adding-validation-to-the-model/samples/sample10.vb)]

运行应用程序并浏览到 `Movies` 控制器。

![8_format_SM](adding-validation-to-the-model/_static/image3.png)

在本系列的下一部分中，我们将查看应用程序，并对自动生成的 `Details` 和 `Delete` 方法进行一些改进。

> [!div class="step-by-step"]
> [上一页](adding-a-new-field.md)
> [下一页](improving-the-details-and-delete-methods.md)
