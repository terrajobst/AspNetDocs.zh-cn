---
uid: web-forms/overview/older-versions-getting-started/continuing-with-ef/using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering
title: 使用实体框架4.0 和 ObjectDataSource 控件，第3部分：排序和筛选 |Microsoft Docs
author: tdykstra
description: 本教程系列在使用实体框架4.0 教程系列的入门创建的 Contoso 大学 web 应用程序上构建。 I...
ms.author: riande
ms.date: 01/26/2011
ms.assetid: 2990bd10-590d-43d5-9529-6b503ce5455d
msc.legacyurl: /web-forms/overview/older-versions-getting-started/continuing-with-ef/using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering
msc.type: authoredcontent
ms.openlocfilehash: 603120864528b9a5ff81214270eb9a7f1b68b347
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78512714"
---
# <a name="using-the-entity-framework-40-and-the-objectdatasource-control-part-3-sorting-and-filtering"></a>使用实体框架4.0 和 ObjectDataSource 控件，第3部分：排序和筛选

作者： [Tom Dykstra](https://github.com/tdykstra)

> 本教程系列在[使用实体框架 4.0](https://asp.net/entity-framework/tutorials#Getting%20Started)教程系列的入门创建的 Contoso 大学 web 应用程序上构建。 如果你没有完成前面的教程，作为本教程的起点，你可以下载你要创建[的应用程序](https://code.msdn.microsoft.com/ASPNET-Web-Forms-97f8ee9a)。 你还可以下载完整的系列教程创建的[应用程序](https://code.msdn.microsoft.com/ASPNET-Web-Forms-6c7197aa)。 如果有关于这些教程的问题，可以将其发布到[ASP.NET 实体框架论坛](https://forums.asp.net/1227.aspx)。

在上一教程中，你已在使用实体框架和 `ObjectDataSource` 控件的 n 层 web 应用程序中实现了存储库模式。 本教程介绍如何进行排序和筛选，以及如何处理主/从方案。 你将在 "*部门*" 页中添加以下增强功能：

- 允许用户按名称选择部门的文本框。
- 网格中显示的每个部门的课程列表。
- 通过单击列标题进行排序的功能。

[![Image01](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image2.png)](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image1.png)

## <a name="adding-the-ability-to-sort-gridview-columns"></a>添加对 GridView 列排序的功能

打开 " *default.aspx* " 页，并将 `SortParameterName="sortExpression"` 特性添加到名为 `DepartmentsObjectDataSource`的 `ObjectDataSource` 控件。 （稍后，你将创建一个 `GetDepartments` 方法，该方法采用名为 `sortExpression`的参数。）控件开始标记的标记现在类似于下面的示例。

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample1.aspx)]

将 `AllowSorting="true"` 特性添加到 `GridView` 控件的开始标记中。 控件开始标记的标记现在类似于下面的示例。

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample2.aspx)]

在*Departments.aspx.cs*中，通过从 `Page_Load` 方法调用 `GridView` 控件的 `Sort` 方法来设置默认排序顺序：

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample3.cs)]

可以在业务逻辑类或存储库类中添加排序或筛选的代码。 如果在业务逻辑类中执行此操作，则会在从数据库中检索数据后执行排序或筛选工作，因为业务逻辑类使用存储库返回的 `IEnumerable` 对象。 如果在存储库类中添加排序和筛选代码，并在将 LINQ 表达式或对象查询转换为 `IEnumerable` 对象之前执行此操作，则会将命令传递到数据库进行处理，这通常更有效。 在本教程中，您将以一种使处理由数据库（即存储在存储库中）完成的方式进行排序和筛选。

若要添加排序功能，必须将新方法添加到存储库接口和存储库类以及业务逻辑类中。 在*ISchoolRepository.cs*文件中，添加一个新的 `GetDepartments` 方法，该方法采用将用于对返回的部门列表进行排序的 `sortExpression` 参数：

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample4.cs)]

`sortExpression` 参数将指定要排序的列以及排序方向。

将新方法的代码添加到*SchoolRepository.cs*文件：

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample5.cs)]

更改现有的无参数 `GetDepartments` 方法以调用新方法：

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample6.cs)]

在测试项目中，将以下新方法添加到*MockSchoolRepository.cs*：

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample7.cs)]

如果要创建依赖于此方法的任何单元测试返回已排序的列表，则需要在返回列表之前对其进行排序。 在本教程中，您将不会创建像这样的测试，因此该方法只返回未排序的部门列表。

在*SchoolBL.cs*文件中，将以下新方法添加到业务逻辑类：

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample8.cs)]

此代码将排序参数传递给存储库方法。

运行 " *node.js" 页。*

[![Image02](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image4.png)](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image3.png)

你现在可以单击任何列标题以按该列进行排序。 如果已对列进行排序，则单击标题会反转排序方向。

## <a name="adding-a-search-box"></a>添加搜索框

在本节中，您将添加一个 "搜索" 文本框，使用控制参数将其链接到 `ObjectDataSource` 控件，并将方法添加到业务逻辑类以支持筛选。

打开 " *default.aspx* " 页，并在标题和第一个 `ObjectDataSource` 控件之间添加以下标记：

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample9.aspx)]

在名为 `DepartmentsObjectDataSource`的 `ObjectDataSource` 控件中，执行以下操作：

- 添加一个名为 `nameSearchString` 的参数的 `SelectParameters` 元素，该参数获取 `SearchTextBox` 控件中输入的值。
- 将 `SelectMethod` 特性值更改为 `GetDepartmentsByName`。 （稍后将创建此方法。）

`ObjectDataSource` 控件的标记现在类似于以下示例：

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample10.aspx)]

在*ISchoolRepository.cs*中，添加一个 `GetDepartmentsByName` 方法，该方法采用 `sortExpression` 和 `nameSearchString` 参数：

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample11.cs)]

在*SchoolRepository.cs*中，添加以下新方法：

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample12.cs)]

此代码使用 `Where` 方法来选择包含搜索字符串的项。 如果搜索字符串为空，则将选择所有记录。 请注意，当你将方法调用一起指定到此类语句（`Include`，然后 `OrderBy`，然后 `Where`）中时，`Where` 方法必须始终是最后一个。

更改采用 `sortExpression` 参数的现有 `GetDepartments` 方法，以调用新方法：

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample13.cs)]

在测试项目的*MockSchoolRepository.cs*中，添加以下新方法：

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample14.cs)]

在*SchoolBL.cs*中，添加以下新方法：

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample15.cs)]

运行 " *node.js* " 页并输入搜索字符串以确保选择逻辑正常工作。 将文本框留空，然后尝试搜索，确保返回所有记录。

[![Image03](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image6.png)](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image5.png)

## <a name="adding-a-details-column-for-each-grid-row"></a>为每个网格行添加详细信息列

接下来，您需要查看在网格右侧单元格中显示的每个部门的所有课程。 为此，你将使用嵌套 `GridView` 控件，并将其数据绑定到 `Department` 实体的 `Courses` 导航属性中的数据。

在 `GridView` 控件的标记*中打开 node.js* ，并为 `RowDataBound` 事件指定处理程序。 控件开始标记的标记现在类似于下面的示例。

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample16.aspx)]

在 `Administrator` 模板字段后添加新的 `TemplateField` 元素：

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample17.aspx)]

此标记创建一个嵌套的 `GridView` 控件，该控件显示课程列表的编号和标题。 它不指定数据源，因为您将在 `RowDataBound` 处理程序中的代码中进行数据绑定。

打开*Departments.aspx.cs*并为 `RowDataBound` 事件添加以下处理程序：

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample18.cs)]

此代码从事件参数中获取 `Department` 实体，将 `Courses` 导航属性转换为 `List` 集合，并将嵌套的 `GridView` databinds 到集合中。

通过在 `GetDepartmentsByName` 方法中创建的对象查询中调用 `Include` 方法，打开*SchoolRepository.cs*文件并指定预先加载 `Courses` 导航属性。 `GetDepartmentsByName` 方法中的 `return` 语句现在类似于下面的示例。

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample19.cs)]

运行页面。 除了前面添加的排序和筛选功能，GridView 控件现在还显示每个部门的嵌套课程详细信息。

[![Image01](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image8.png)](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image7.png)

这将完成对排序、筛选和主/详细方案的介绍。 在下一教程中，你将了解如何处理并发。

> [!div class="step-by-step"]
> [上一页](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests.md)
> [下一页](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application.md)
