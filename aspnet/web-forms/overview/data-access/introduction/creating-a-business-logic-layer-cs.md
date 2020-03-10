---
uid: web-forms/overview/data-access/introduction/creating-a-business-logic-layer-cs
title: 创建业务逻辑层（C#） |Microsoft Docs
author: rick-anderson
description: 在本教程中，我们将了解如何将业务规则集中到一种业务逻辑层（BLL）中，作为在 t 。
ms.author: riande
ms.date: 03/31/2010
ms.assetid: 85554606-47cb-4e4f-9848-eed9da579056
msc.legacyurl: /web-forms/overview/data-access/introduction/creating-a-business-logic-layer-cs
msc.type: authoredcontent
ms.openlocfilehash: df96f3e7422a0537bf1b003a33fe8d71a671ac33
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78490400"
---
# <a name="creating-a-business-logic-layer-c"></a>创建业务逻辑层 (C#)

作者： [Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载示例应用](https://download.microsoft.com/download/4/6/3/463cf87c-4724-4cbc-b7b5-3f866f43ba50/ASPNET_Data_Tutorial_2_CS.exe)或[下载 PDF](creating-a-business-logic-layer-cs/_static/datatutorial02cs1.pdf)

> 在本教程中，我们将了解如何将业务规则集中到业务逻辑层（BLL）中，以便作为表示层与 DAL 之间的数据交换中介。

## <a name="introduction"></a>简介

在[第一个教程](creating-a-data-access-layer-cs.md)中创建的数据访问层（DAL）将数据访问逻辑与表示逻辑完全分离。 但是，当 DAL 将数据访问详细信息与表示层完全分离时，它不会强制实施任何可能适用的业务规则。 例如，对于我们的应用程序，我们可能希望在 "`Discontinued`" 字段设置为1时不允许修改 `Products` 表的 `CategoryID` 或 `SupplierID` 字段，或者建议强制使用资历规则，禁止在员工由他们之后聘用的人员管理的情况。 另一种常见情况是授权，这种情况下，只有特定角色的用户才能删除产品，或者可以更改 `UnitPrice` 值。

在本教程中，我们将了解如何将这些业务规则集中到一种业务逻辑层（BLL）中，作为表示层与 DAL 之间的数据交换中介。 在实际应用程序中，BLL 应作为单独的类库项目实现;但对于这些教程，我们会将 BLL 作为 `App_Code` 文件夹中的一系列类来实现，以便简化项目结构。 图1演示了表示层、BLL 和 DAL 之间的体系结构关系。

![BLL 将表示层与数据访问层隔开，并施加业务规则](creating-a-business-logic-layer-cs/_static/image1.png)

**图 1**： BLL 将表示层与数据访问层隔开，并施加业务规则

## <a name="step-1-creating-the-bll-classes"></a>步骤1：创建 BLL 类

我们的 BLL 由四个类组成，其中一个用于 DAL 中的每个 TableAdapter;其中每个 BLL 类都具有从 DAL 中的相应 TableAdapter 检索、插入、更新和删除的方法，并应用相应的业务规则。

若要更清晰地分隔 DAL 与 BLL 相关的类，请在 `App_Code` 文件夹中创建两个子文件夹，`DAL` 和 `BLL`。 只需右键单击解决方案资源管理器中的 "`App_Code`" 文件夹，然后选择 "新建文件夹" 即可。 创建这两个文件夹后，将在第一个教程中创建的类型化数据集移动到 `DAL` 子文件夹中。

接下来，在 `BLL` 子文件夹中创建四个 BLL 类文件。 为此，请右键单击 `BLL` 子文件夹，选择 "添加新项"，然后选择 "类" 模板。 将四个类命名为 `ProductsBLL`、`CategoriesBLL`、`SuppliersBLL`和 `EmployeesBLL`。

![将四个新类添加到 App_Code 文件夹](creating-a-business-logic-layer-cs/_static/image2.png)

**图 2**：将四个新类添加到 `App_Code` 文件夹

接下来，让我们向每个类添加方法，以便在第一个教程中简单地包装为 Tableadapter 定义的方法。 现在，这些方法只需直接调用 DAL;稍后我们将返回以添加任何所需的业务逻辑。

> [!NOTE]
> 如果你使用的是 Visual Studio Standard Edition 或更高版本（即，你*不*是使用 Visual Web Developer），则可以选择使用[类设计器](https://msdn.microsoft.com/library/default.asp?url=/library/dv_vstechart/html/clssdsgnr.asp)直观地设计你的类。 有关 Visual Studio 中的此新功能的详细信息，请参阅[类设计器博客](https://blogs.msdn.com/classdesigner/default.aspx)。

对于 `ProductsBLL` 类，我们需要添加全部七个方法：

- `GetProducts()` 返回所有产品
- `GetProductByProductID(productID)` 返回具有指定产品 ID 的产品
- `GetProductsByCategoryID(categoryID)` 返回指定类别中的所有产品
- `GetProductsBySupplier(supplierID)` 返回指定供应商的所有产品
- `AddProduct(productName, supplierID, categoryID, quantityPerUnit, unitPrice, unitsInStock, unitsOnOrder, reorderLevel, discontinued)` 使用传入的值将新产品插入到数据库中;返回新插入记录的 `ProductID` 值
- `UpdateProduct(productName, supplierID, categoryID, quantityPerUnit, unitPrice, unitsInStock, unitsOnOrder, reorderLevel, discontinued, productID)` 使用传入的值更新数据库中的现有产品，如果精确更新一行，则返回 `true`，否则返回 `false`
- `DeleteProduct(productID)` 从数据库中删除指定的产品

ProductsBLL.cs

[!code-csharp[Main](creating-a-business-logic-layer-cs/samples/sample1.cs)]

仅返回数据 `GetProducts`、`GetProductByProductID`、`GetProductsByCategoryID`和 `GetProductBySuppliersID` 的方法非常简单，因为它们只是向下调用 DAL。 在某些情况下，可能需要在此级别实现业务规则（例如基于当前登录用户的授权规则或用户所属的角色），只需按原样保留这些方法。 对于这些方法，BLL 只充当一个代理，通过该代理，表示层可以访问数据访问层中的基础数据。

`AddProduct` 和 `UpdateProduct` 方法均将各种产品字段的值作为参数，并分别添加新产品或更新现有产品。 由于许多 `Product` 表的列都可以接受 `NULL` 值（`CategoryID`、`SupplierID`和 `UnitPrice`），因此映射到此类列的 `AddProduct` 和 `UpdateProduct` 的输入参数使用[可以为 null 的类型](https://msdn.microsoft.com/library/1t3y8s4s(v=vs.80).aspx)。 可以为 null 的类型是 .NET 2.0 的新手，并提供一种方法，用于指示是否应 `null`值类型。 在C#中，可以通过在类型（如 `int? x;`）之后添加 `?`，将值类型标记为可以为 null 的类型。 有关详细信息，请参阅[ C#编程指南](https://msdn.microsoft.com/library/67ef8sbd%28VS.80%29.aspx)中的[可为 null 的类型](https://msdn.microsoft.com/library/1t3y8s4s.aspx)部分。

所有这三种方法都返回一个布尔值，指示在该操作可能不会导致受影响的行后，是否插入、更新或删除行。 例如，如果页开发人员调用了不存在的产品 `DeleteProduct` 传入 `ProductID`，则向数据库发出的 `DELETE` 语句将不会产生任何影响，因此 `DeleteProduct` 方法将返回 `false`。

请注意，当添加新的产品或更新现有的产品时，我们会将新的或已修改的产品的字段值作为标量列表，而不是接受 `ProductsRow` 的实例。 之所以选择此方法，是因为 `ProductsRow` 类派生自 ADO.NET `DataRow` 类，该类没有默认的无参数构造函数。 若要创建新的 `ProductsRow` 实例，必须首先创建一个 `ProductsDataTable` 实例，然后调用其 `NewProductRow()` 方法（在 `AddProduct`中执行此操作）。 当我们转而使用 ObjectDataSource 插入和更新产品时，这种缺点会 rears。 简而言之，ObjectDataSource 将尝试创建输入参数的实例。 如果 BLL 方法需要 `ProductsRow` 实例，则 ObjectDataSource 将尝试创建一个实例，但由于缺少默认的无参数构造函数而失败。 有关此问题的详细信息，请参阅以下两个 ASP.NET 论坛文章：[用强类型化数据集更新 objectdatasource](https://forums.asp.net/1098630/ShowPost.aspx)，并为[ObjectDataSource 和强类型化数据集提供问题](https://forums.asp.net/1048212/ShowPost.aspx)。

接下来，在 `AddProduct` 和 `UpdateProduct`中，代码创建一个 `ProductsRow` 实例，并使用刚刚传入的值填充该实例。 将值分配到 DataRow 的 Datacolumn 时，可能会发生不同的字段级验证检查。 因此，手动将传入的值放回 DataRow，有助于确保传递到 BLL 方法的数据的有效性。 遗憾的是，Visual Studio 生成的强类型 DataRow 类不使用可以为 null 的类型。 相反，若要指示 DataRow 中的特定 DataColumn 应对应于 `NULL` 数据库值，则必须使用 `SetColumnNameNull()` 方法。

在中 `UpdateProduct` 首先加载要使用 `GetProductByProductID(productID)`进行更新的产品。 尽管这可能是不必要的数据库行程，但在将来探索开放式并发的教程中，这种额外的行程会很有价值。 乐观并发是一项技术，可确保同时处理相同数据的两个用户不会意外覆盖另一个数据更改。 通过抓取整个记录，还可以更轻松地在 BLL 中创建仅修改 DataRow 列子集的更新方法。 当我们浏览 `SuppliersBLL` 类时，我们将看到这样一个示例。

最后请注意，`ProductsBLL` 类应用了[DataObject 特性](https://msdn.microsoft.com/library/system.componentmodel.dataobjectattribute.aspx)（在文件顶部附近的类语句之前 `[System.ComponentModel.DataObject]` 语法），并且方法具有[DataObjectMethodAttribute 特性](https://msdn.microsoft.com/library/system.componentmodel.dataobjectmethodattribute.aspx)。 `DataObject` 特性将该类标记为适合绑定到[ObjectDataSource 控件](https://msdn.microsoft.com/library/9a4kyhcx.aspx)的对象，而 `DataObjectMethodAttribute` 指示该方法的用途。 我们将在将来的教程中看到，ASP.NET 2.0 的 ObjectDataSource 使你可以轻松地从类中轻松地访问数据。 为了帮助在 ObjectDataSource 的向导中筛选要绑定到的可能类的列表，默认情况下，仅在向导的下拉列表中显示标记为 `DataObjects` 的类。 `ProductsBLL` 类将同样适用于没有这些属性的情况，但添加它们可使其在 ObjectDataSource 的向导中更易于使用。

## <a name="adding-the-other-classes"></a>添加其他类

由于 `ProductsBLL` 类完成，我们仍然需要添加类，以便与类别、供应商和员工一起使用。 使用上述示例中的概念花点时间创建以下类和方法：

- **CategoriesBLL.cs**

    - `GetCategories()`
    - `GetCategoryByCategoryID(categoryID)`
- **SuppliersBLL.cs**

    - `GetSuppliers()`
    - `GetSupplierBySupplierID(supplierID)`
    - `GetSuppliersByCountry(country)`
    - `UpdateSupplierAddress(supplierID, address, city, country)`
- **EmployeesBLL.cs**

    - `GetEmployees()`
    - `GetEmployeeByEmployeeID(employeeID)`
    - `GetEmployeesByManager(managerID)`

需要注意的一种方法是 `SuppliersBLL` 类的 `UpdateSupplierAddress` 方法。 此方法提供了一个用于仅更新供应商地址信息的接口。 在内部，此方法在指定的 `supplierID` （使用 `GetSupplierBySupplierID`）的 `SupplierDataRow` 对象中读取，设置与地址相关的属性，然后向下调用 `SupplierDataTable`的 `Update` 方法。 `UpdateSupplierAddress` 方法如下：

[!code-csharp[Main](creating-a-business-logic-layer-cs/samples/sample2.cs)]

请参阅本文的下载内容，了解如何实现 BLL 类的完整实现。

## <a name="step-2-accessing-the-typed-datasets-through-the-bll-classes"></a>步骤2：通过 BLL 类访问类型化数据集

在第一个教程中，我们看到了以编程方式直接使用类型化数据集的示例，但在添加了 BLL 类后，表示层应改为与 BLL 一起工作。 在第一个教程的 `AllProducts.aspx` 示例中，`ProductsTableAdapter` 用于将产品列表绑定到 GridView，如以下代码所示：

[!code-csharp[Main](creating-a-business-logic-layer-cs/samples/sample3.cs)]

若要使用新的 BLL 类，所有需要更改的都是代码的第一行，只需将 `ProductsTableAdapter` 对象替换为 `ProductBLL` 对象：

[!code-csharp[Main](creating-a-business-logic-layer-cs/samples/sample4.cs)]

还可以通过使用 ObjectDataSource 以声明方式（如类型化的数据集）访问 BLL 类。 我们将在以下教程中更详细地讨论 ObjectDataSource。

[![产品列表显示在 GridView 中](creating-a-business-logic-layer-cs/_static/image4.png)](creating-a-business-logic-layer-cs/_static/image3.png)

**图 3**：产品列表显示在 GridView 中（[单击以查看完全大小的图像](creating-a-business-logic-layer-cs/_static/image5.png)）

## <a name="step-3-adding-field-level-validation-to-the-datarow-classes"></a>步骤3：向 DataRow 类添加字段级验证

字段级验证是在插入或更新时与业务对象的属性值有关的检查。 某些产品的字段级验证规则包括：

- `ProductName` 字段长度不能超过40个字符
- `QuantityPerUnit` 字段长度不能超过20个字符
- `ProductID`、`ProductName`和 `Discontinued` 字段是必需的，但所有其他字段都是可选的
- `UnitPrice`、`UnitsInStock`、`UnitsOnOrder`和 `ReorderLevel` 字段必须大于或等于零

这些规则可以和应在数据库级别表示。 `ProductName` 和 `QuantityPerUnit` 字段的字符限制由 `Products` 表中这些列的数据类型（分别为`nvarchar(40)` 和 `nvarchar(20)`）捕获。 如果数据库表列允许 `NULL`，则是否需要字段和可选字段。 存在四个[检查约束](https://msdn.microsoft.com/library/ms188258.aspx)，以确保只有大于或等于零的值才能使其成为 `UnitPrice`、`UnitsInStock`、`UnitsOnOrder`或 `ReorderLevel` 列。

除了在数据库中实施这些规则外，还应在数据集级别强制执行这些规则。 事实上，对于每个 DataTable 的 Datacolumn 集，字段长度和值是必需的还是可选的。 若要查看自动提供的现有字段级别验证，请在 "数据集设计器" 中选择一个数据表中的字段，然后访问属性窗口。 如图4所示，`ProductsDataTable` 中的 `QuantityPerUnit` DataColumn 的最大长度为20个字符，且允许 `NULL` 值。 如果尝试将 `ProductsDataRow`的 `QuantityPerUnit` 属性设置为长度超过20个字符的字符串值，将会引发 `ArgumentException`。

[![DataColumn 提供基本的字段级验证](creating-a-business-logic-layer-cs/_static/image7.png)](creating-a-business-logic-layer-cs/_static/image6.png)

**图 4**： DataColumn 提供基本的字段级验证（[单击查看完全尺寸的图像](creating-a-business-logic-layer-cs/_static/image8.png)）

遗憾的是，无法通过属性窗口指定边界检查（如 `UnitPrice` 值必须大于或等于零）。 为了提供此类型的字段级验证，需要为 DataTable 的[ColumnChanging](https://msdn.microsoft.com/library/system.data.datatable.columnchanging%28VS.80%29.aspx)事件创建事件处理程序。 如[前面的教程](creating-a-data-access-layer-cs.md)中所述，可通过使用分部类扩展由类型化数据集创建的数据集、数据表和 DataRow 对象。 使用此技术，我们可以为 `ProductsDataTable` 类创建 `ColumnChanging` 事件处理程序。 首先在名为 `ProductsDataTable.ColumnChanging.cs``App_Code` 文件夹中创建一个类。

[![将新类添加到 App_Code 文件夹](creating-a-business-logic-layer-cs/_static/image10.png)](creating-a-business-logic-layer-cs/_static/image9.png)

**图 5**：将新类添加到 `App_Code` 文件夹（[单击查看完全大小的图像](creating-a-business-logic-layer-cs/_static/image11.png)）

接下来，为 `ColumnChanging` 事件创建事件处理程序，该事件可确保 `UnitPrice`、`UnitsInStock`、`UnitsOnOrder`和 `ReorderLevel` 列值（如果不 `NULL`）大于或等于零。 如果任何这样的列超出范围，则会引发 `ArgumentException`。

ProductsDataTable.ColumnChanging.cs

[!code-csharp[Main](creating-a-business-logic-layer-cs/samples/sample5.cs)]

## <a name="step-4-adding-custom-business-rules-to-the-blls-classes"></a>步骤4：向 BLL 的类添加自定义业务规则

除了字段级验证外，可能还存在一些高级自定义业务规则，这些规则涉及无法在单列级别表达的不同实体或概念，例如：

- 如果产品停用，则无法更新其 `UnitPrice`
- 员工居住的国家/地区必须与其居住的经理所在国家/地区相同
- 如果产品是供应商提供的唯一产品，则无法停产

BLL 类应包含检查以确保遵守应用程序的业务规则。 这些检查可以直接添加到它们所应用到的方法中。

假设我们的业务规则规定，如果产品是来自给定供应商的唯一产品，则不能将其标记为停用。 也就是说，如果 product *X*是我们从供应商*Y*购买的唯一产品，我们无法将*X*标记为已停用;然而，如果供应商*Y*向我们提供了三种产品： *A*、 *B*和*C*，则可以将所有这些都标记为已停用。 不是一种很好的业务规则，但业务规则和常见意义并不总是一致！

若要在 `UpdateProducts` 方法中强制实施此业务规则，我们首先检查是否已将 `Discontinued` 设置为 `true`，如果是，我们会调用 `GetProductsBySupplierID` 来确定从此产品的供应商那里购买了多少产品。 如果仅从此供应商购买一种产品，则会引发 `ApplicationException`。

[!code-csharp[Main](creating-a-business-logic-layer-cs/samples/sample6.cs)]

## <a name="responding-to-validation-errors-in-the-presentation-tier"></a>响应表示层中的验证错误

从表示层调用 BLL 时，我们可以决定是尝试处理可能引发的任何异常，还是让它们向上冒泡到 ASP.NET （这会引发 `HttpApplication`的 `Error` 事件）。 若要在以编程方式使用 BLL 时处理异常，可以使用[try 。catch](https://msdn.microsoft.com/library/0yd65esw.aspx)块，如以下示例所示：

[!code-csharp[Main](creating-a-business-logic-layer-cs/samples/sample7.cs)]

正如我们将在将来的教程中看到的那样，在使用数据 Web 控件插入、更新或删除数据时，处理从 BLL 向上冒泡的异常可以直接在事件处理程序中处理，而不必在 `try...catch` 块中包装代码。

## <a name="summary"></a>摘要

设计良好的应用程序可在不同的层中进行设计，每个层封装一个特定角色。 在本文的第一个教程中，我们创建了一个使用类型化数据集的数据访问层;在本教程中，我们构建了一个业务逻辑层作为应用程序 `App_Code` 文件夹中的一系列类，该文件夹向下调用 DAL。 BLL 实现了应用程序的字段级和业务级逻辑。 除了创建单独的 BLL 外，与我们在本教程中所做的一样，另一个选项是通过使用分部类来扩展 Tableadapter 的方法。 然而，使用这种方法并不允许我们覆盖现有方法，也不能将 DAL 和 BLL 与我们在本文中所采用的方法完全分离。

当 DAL 和 BLL 完成后，就可以开始在我们的表示层上着手。 在[下一教程](master-pages-and-site-navigation-cs.md)中，我们将简单 detour 数据访问主题，并定义一致的页面布局，以便在整个教程中使用。

很高兴编程！

## <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，创始人的[4GuysFromRolla.com](http://www.4guysfromrolla.com)，已在使用 Microsoft Web 技术，自1998开始。 Scott 的工作方式是独立的顾问、培训师和撰稿人。 他的最新书籍是，[*在24小时内，sam ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 可以[mitchell@4GuysFromRolla.com访问。](mailto:mitchell@4GuysFromRolla.com) 或通过他的博客，可以在[http://ScottOnWriting.NET](http://ScottOnWriting.NET)找到。

## <a name="special-thanks-to"></a>特别感谢

此教程系列由许多有用的审阅者查看。 本教程的主管评审者是 Liz Shulok、Dennis Patterson 将、Carlos Santos 和 Hilton Giesenow。 想要查看我即将发布的 MSDN 文章？ 如果是这样，请在mitchell@4GuysFromRolla.com放置一行[。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一页](creating-a-data-access-layer-cs.md)
> [下一页](master-pages-and-site-navigation-cs.md)
