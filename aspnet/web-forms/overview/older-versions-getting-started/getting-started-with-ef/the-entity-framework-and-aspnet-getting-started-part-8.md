---
uid: web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-8
title: 入门实体框架 4.0 Database First 和 ASP.NET 4 Web 窗体-第8部分 |Microsoft Docs
author: tdykstra
description: Contoso 大学示例 web 应用程序演示了如何使用实体框架创建 ASP.NET Web 窗体应用程序。 示例应用程序为 。
ms.author: riande
ms.date: 12/03/2010
ms.assetid: aaadd9bb-5508-448c-ad57-5497dff90e13
msc.legacyurl: /web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-8
msc.type: authoredcontent
ms.openlocfilehash: ff6a808dd501df8056c0fb0784a8e42e094d5db7
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78473504"
---
# <a name="getting-started-with-entity-framework-40-database-first-and-aspnet-4-web-forms---part-8"></a>入门实体框架 4.0 Database First 和 ASP.NET 4 Web 窗体-第8部分

作者： [Tom Dykstra](https://github.com/tdykstra)

> Contoso 大学示例 web 应用程序演示了如何使用实体框架4.0 和 Visual Studio 2010 创建 ASP.NET Web 窗体应用程序。 有关本教程系列的信息，请参阅[系列教程中的第一个教程](the-entity-framework-and-aspnet-getting-started-part-1.md)

## <a name="using-dynamic-data-functionality-to-format-and-validate-data"></a>使用动态数据功能格式化和验证数据

在上一教程中，您将实现存储过程。 本教程将演示动态数据功能如何提供以下好处：

- 根据字段的数据类型，字段将自动进行格式设置。
- 根据字段的数据类型自动验证字段。
- 您可以将元数据添加到数据模型，以自定义格式设置和验证行为。 执行此操作时，只需在一个位置添加格式设置和验证规则，这些规则就会自动应用到使用动态数据控件访问这些字段的任何位置。

若要查看其工作原理，你将更改用于显示和*编辑现有 "* student" 页中的字段的控件，并将格式设置和验证元数据添加到 `Student` 实体类型的 "名称" 和 "日期" 字段。

[![Image01](the-entity-framework-and-aspnet-getting-started-part-8/_static/image2.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image1.png)

## <a name="using-dynamicfield-and-dynamiccontrol-controls"></a>使用 DynamicField 和 DynamicControl 控件

打开 "student *" 页，* 然后在 `StudentsGridView` 控件中，用以下标记替换**名称**和**注册日期**`TemplateField` 元素：

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-8/samples/sample1.aspx)]

此标记使用 `DynamicControl` 控件来代替 `TextBox` 并在 "学生姓名模板" 字段中 `Label` 控件，并对注册日期使用 `DynamicField` 控件。 未指定格式字符串。

将 `ValidationSummary` 控件添加到 `StudentsGridView` 控件之后。

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-8/samples/sample2.aspx)]

在 `SearchGridView` 控件中，将 "**名称**" 和 "**注册日期**" 列的标记替换为在 `StudentsGridView` 控件中执行的操作，但省略 `EditItemTemplate` 元素除外。 `SearchGridView` 控件的 `Columns` 元素现在包含以下标记：

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-8/samples/sample3.aspx)]

打开*Students.aspx.cs*并添加以下 `using` 语句：

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-8/samples/sample4.cs)]

为页面的 `Init` 事件添加处理程序：

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-8/samples/sample5.cs)]

此代码指定动态数据将在 `Student` 实体的字段的这些数据绑定控件中提供格式设置和验证。 如果在运行页面时收到类似于以下示例的错误消息，则通常意味着你在 `Page_Init`中忘记了调用 `EnableDynamicData` 方法：

`Could not determine a MetaTable. A MetaTable could not be determined for the data source 'StudentsEntityDataSource' and one could not be inferred from the request URL.`

运行页面。

[![Image03](the-entity-framework-and-aspnet-getting-started-part-8/_static/image4.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image3.png)

在 "**注册日期**" 列中，时间与日期一起显示，因为属性类型为 `DateTime`。 稍后你将解决此问题。

请注意，动态数据会自动提供基本的数据验证。 例如，单击 "**编辑**"，清除 "日期" 字段，单击 "**更新**"，您将看到动态数据自动使此字段成为必填字段，因为在数据模型中值不可为 null。 该页在字段后面显示星号，在 `ValidationSummary` 控件中显示错误消息：

[![Image05](the-entity-framework-and-aspnet-getting-started-part-8/_static/image6.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image5.png)

您可以省略 `ValidationSummary` 控件，因为还可以将鼠标指针停留在星号上以查看错误消息：

[![Image06](the-entity-framework-and-aspnet-getting-started-part-8/_static/image8.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image7.png)

动态数据还将验证在 "**注册日期**" 字段中输入的数据是否为有效日期：

[![Image04](the-entity-framework-and-aspnet-getting-started-part-8/_static/image10.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image9.png)

如您所见，这是一个一般性错误消息。 在下一部分中，你将了解如何自定义消息以及验证和格式设置规则。

## <a name="adding-metadata-to-the-data-model"></a>将元数据添加到数据模型

通常，您需要自定义动态数据提供的功能。 例如，你可以更改数据的显示方式以及错误消息的内容。 通常，你还可以自定义数据验证规则，以提供比动态数据基于数据类型自动提供的功能更多的功能。 为此，可以创建与实体类型相对应的分部类。

在**解决方案资源管理器**中，右键单击**ContosoUniversity**项目，选择 "**添加引用**"，并添加对 `System.ComponentModel.DataAnnotations`的引用。

[![Image11](the-entity-framework-and-aspnet-getting-started-part-8/_static/image12.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image11.png)

在*DAL*文件夹中，创建一个新的类文件，将其命名为*Student.cs*，并将其中的模板代码替换为以下代码。

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-8/samples/sample6.cs)]

此代码将创建 `Student` 实体的分部类。 应用于此分部类的 `MetadataType` 属性标识用于指定元数据的类。 Metadata 类可以具有任何名称，但使用实体名称加 "Metadata" 是常见做法。

应用于元数据类中的属性的特性指定格式设置、验证、规则和错误消息。 此处显示的属性将具有以下结果：

- `EnrollmentDate` 将显示为日期（没有时间）。
- 两个名称字段的长度必须小于或等于25个字符，并提供自定义错误消息。
- 这两个名称字段都是必需的，并且提供了一个自定义错误消息。

再次运行*student 页面，* 你会看到现在没有时间显示日期：

[![Image08](the-entity-framework-and-aspnet-getting-started-part-8/_static/image14.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image13.png)

编辑行，并尝试清除 "名称" 字段中的值。 在您单击 "**更新**" 之前，一旦您离开字段，就会出现指示域错误的星号。 单击 "**更新**" 时，页面将显示您指定的错误消息文本。

[![Image10](the-entity-framework-and-aspnet-getting-started-part-8/_static/image16.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image15.png)

尝试输入超过25个字符的名称，单击 "**更新**"，该页将显示您指定的错误消息文本。

[![Image09](the-entity-framework-and-aspnet-getting-started-part-8/_static/image18.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image17.png)

现在，你已在数据模型元数据中设置这些格式设置和验证规则，只要你使用 `DynamicControl` 或 `DynamicField` 控件，规则就会自动应用于显示或允许对这些字段进行更改的每个页面。 这会减少您必须编写的冗余代码量，使编程和测试变得更加容易，并且确保数据格式和验证在整个应用程序中保持一致。

## <a name="more-information"></a>详细信息

这将在与实体框架入门的这一系列教程结束。 若要详细了解如何使用实体框架，请继续学习[下一实体框架教程系列中的第一个教程](../continuing-with-ef/using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started.md)，或访问以下站点：

- [实体框架常见问题](http://www.ef-faq.org/introduction.html)
- [实体框架团队博客](https://blogs.msdn.com/b/adonet/)
- [MSDN Library 中的实体框架](https://msdn.microsoft.com/library/bb399572.aspx)
- [MSDN 数据开发人员中心中的实体框架](https://msdn.microsoft.com/data/ef.aspx)
- [MSDN Library 中的 EntityDataSource Web 服务器控件概述](https://msdn.microsoft.com/library/cc488502.aspx)
- [MSDN Library 中的 EntityDataSource 控件 API 参考](https://msdn.microsoft.com/library/system.web.ui.webcontrols.entitydatasource.aspx)
- [MSDN 上的实体框架论坛](https://social.msdn.microsoft.com/forums/adodotnetentityframework/)
- [Julie Lerman 的博客](http://thedatafarm.com/blog/)

> [!div class="step-by-step"]
> [上一页](the-entity-framework-and-aspnet-getting-started-part-7.md)
