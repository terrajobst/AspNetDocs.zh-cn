---
uid: web-forms/overview/presenting-and-managing-data/model-binding/integrating-jquery-ui
title: 将 JQuery UI Datepicker 与模型绑定和 web 窗体集成 |Microsoft Docs
author: Rick-Anderson
description: 本教程系列演示了将模型绑定用于 ASP.NET Web 窗体项目的基本方面。 模型绑定使数据交互更加直接-。
ms.author: riande
ms.date: 02/27/2014
ms.assetid: 3cbab37b-fb0f-4751-9ec4-74e068c3f380
msc.legacyurl: /web-forms/overview/presenting-and-managing-data/model-binding/integrating-jquery-ui
msc.type: authoredcontent
ms.openlocfilehash: c8d711dd44950116f3a3e09d5d12c507918c543f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78521978"
---
# <a name="integrating-jquery-ui-datepicker-with-model-binding-and-web-forms"></a>将 JQuery UI Datepicker 与模型绑定和 web 窗体集成

通过[Tom FitzMacken](https://github.com/tfitzmac)

> 本教程系列演示了将模型绑定用于 ASP.NET Web 窗体项目的基本方面。 与处理数据源对象（如 ObjectDataSource 或 SqlDataSource）相比，模型绑定使数据交互更直接。 此系列从介绍性材料开始，并在后面的教程中转到更高级的概念。
> 
> 本教程演示如何将 JQuery UI [Datepicker 小组件](http://jqueryui.com/datepicker/)添加到 Web 窗体，并使用模型绑定来更新具有所选值的数据库。
> 
> 本教程基于在序列的[第一个](retrieving-data.md)和[第二个](updating-deleting-and-creating-data.md)部分中创建的项目构建。
> 
> 可以在或 VB 中C#[下载](https://go.microsoft.com/fwlink/?LinkId=286116)完整项目。 可下载的代码适用于 Visual Studio 2012 或 Visual Studio 2013。 它使用 Visual Studio 2012 模板，该模板与本教程中所示的 Visual Studio 2013 模板略有不同。

## <a name="what-youll-build"></a>要生成的内容

在本教程中，你将：

1. 向模型添加属性以记录学生的注册日期
2. 允许用户使用 JQuery UI Datepicker 小组件选择注册日期
3. 强制执行注册日期的验证规则

使用 JQuery UI Datepicker 小组件，用户可以轻松地从日历中选择一个日期，该日期在用户与字段交互时弹出。 与手动键入日期相比，使用此小组件的用户可以更方便地使用此小组件。 将 Datepicker 小组件集成到用于数据操作的模型绑定的页面只需少量的额外工作。

## <a name="add-a-new-property-to-the-model"></a>向模型添加新属性

首先，将 "**日期时间**" 属性添加到 "学生模型"，并将该更改迁移到数据库。 打开**UniversityModels.cs**，并将突出显示的代码添加到 "学生" 模型。

[!code-csharp[Main](integrating-jquery-ui/samples/sample1.cs?highlight=16-18)]

包含**RangeAttribute**来强制执行属性的验证规则。 对于本教程，我们假定 Contoso 大学在2013年1月1日成立，因此更早的注册日期无效。

在 "包管理" 窗口中，通过运行**AddEnrollmentDate**命令添加迁移。 请注意，迁移代码会将新的 Datetime 列添加到 Student 表中。 若要匹配在 RangeAttribute 中指定的值，请为新列添加默认值，如下面突出显示的代码所示。

[!code-csharp[Main](integrating-jquery-ui/samples/sample2.cs?highlight=11)]

保存对迁移文件的更改。

无需再次对数据进行种子设定。 因此，请在 "迁移" 文件夹中打开**Configuration.cs** ，删除或注释掉**Seed**方法中的代码。 保存并关闭文件。

现在，运行命令**更新-数据库**。 请注意，列现在存在于数据库中，所有现有记录都具有 EnrollmentDate 的默认值。

## <a name="add-dynamic-controls-for-enrollment-date"></a>为注册日期添加动态控件

现在，你将添加用于显示和编辑注册日期的控件。 此时，通过文本框编辑值。 稍后在本教程中，您将把文本框更改为 JQuery Datepicker 小组件。

首先，请务必注意，无需对**AddStudent**文件进行任何更改。 DynamicEntity 控件将自动呈现新的属性。

打开 **"** student"，并添加以下突出显示的代码。

[!code-aspx[Main](integrating-jquery-ui/samples/sample3.aspx?highlight=13)]

运行应用程序，请注意，可以通过键入日期来设置注册日期的值。 添加新学生时：

![设置日期](integrating-jquery-ui/_static/image1.png)

或编辑现有值：

![编辑日期](integrating-jquery-ui/_static/image2.png)

键入日期是可行的，但它可能不是你希望提供的客户体验。 在下一部分中，你将启用通过日历选择日期。

## <a name="install-nuget-package-to-work-with-jquery-ui"></a>安装 NuGet 包以使用 JQuery UI

**汁 ui** NuGet 包可以轻松地将 JQuery UI 小组件集成到 web 应用程序中。 若要使用此包，请通过 NuGet 安装它。

![添加汁 UI](integrating-jquery-ui/_static/image3.png)

安装的汁 UI 版本可能与应用程序中的 JQuery 版本冲突。 在继续学习本教程之前，请尝试运行你的应用程序。 如果遇到 JavaScript 错误，需协调 JQuery 版本。 你可以将所需的 JQuery 版本添加到脚本文件夹（在编写本教程时为版本1.8.2），也可以在 Site 中添加。 master 指定 JQuery 文件的路径。

[!code-aspx[Main](integrating-jquery-ui/samples/sample4.aspx)]

## <a name="customize-datetime-template-to-include-datepicker-widget"></a>自定义日期时间模板以包含 Datepicker 小组件

将 Datepicker 小组件添加到动态数据模板，以编辑日期时间值。 通过将小组件添加到模板中，它会自动呈现在用于添加新学生的表单和用于编辑学生的 "网格" 视图中。 打开**DateTime\_编辑 .ascx**，并添加以下突出显示的代码。

[!code-aspx[Main](integrating-jquery-ui/samples/sample5.aspx?highlight=3)]

在代码隐藏文件中，您将设置 DatePicker 的最小和最大日期。 通过设置这些值，你将会阻止用户导航到无效日期。 如果提供了一个值，则将从 DateTime 属性的**RangeAttribute**中检索最小值和最大值。 打开**DateTime\_Edit.ascx.cs**，并将以下突出显示的代码添加到页面\_Load 方法。

[!code-csharp[Main](integrating-jquery-ui/samples/sample6.cs?highlight=9-14)]

运行 web 应用程序并导航到 AddStudent 页。 提供字段的值，请注意，当你单击 "注册日期" 文本框时，将显示 "日历"。

![日期选取器](integrating-jquery-ui/_static/image4.png)

选择一个日期，然后单击 "**插入**"。 RangeAttribute 在服务器上强制执行验证。 通过设置 Datepicker 上的 minDate 属性，还可以在客户端上应用验证。 日历不允许用户导航到 minDate 值之前的日期。

在网格视图中编辑记录时，也会显示该日历。

![GridView 中的 Datepicker](integrating-jquery-ui/_static/image5.png)

## <a name="conclusion"></a>结论

在本教程中，已学习如何将 JQuery 小组件合并到使用模型绑定的 web 窗体中。

在下一[教程](using-query-string-values-to-retrieve-data.md)中，您将在选择数据时使用查询字符串值。

> [!div class="step-by-step"]
> [上一页](sorting-paging-and-filtering-data.md)
> [下一页](using-query-string-values-to-retrieve-data.md)
