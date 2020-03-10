---
uid: web-forms/overview/moving-to-aspnet-20/data-source-controls
title: 数据源控件 |Microsoft Docs
author: microsoft
description: ASP.NET 1.x 中的 DataGrid 控件在 Web 应用程序中对数据访问进行了很大的改进。 但是，这并不是用户友好的，因为它可能已经 ...。
ms.author: riande
ms.date: 02/20/2005
ms.assetid: 78fd0e92-f9c6-4e96-a5e9-0375b307a828
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/data-source-controls
msc.type: authoredcontent
ms.openlocfilehash: a2e2cfbec3e5aebf42a2de30bab7d45b4b610298
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78519350"
---
# <a name="data-source-controls"></a>数据源控件

由[Microsoft](https://github.com/microsoft)

> ASP.NET 1.x 中的 DataGrid 控件在 Web 应用程序中对数据访问进行了很大的改进。 但是，它并不像用户那样友好，因为它可能已经存在。 它仍需要大量的代码来从其获取有用的功能。 这就是在1.x 中的所有数据访问工作中的模型。

ASP.NET 1.x 中的 DataGrid 控件在 Web 应用程序中对数据访问进行了很大的改进。 但是，它并不像用户那样友好，因为它可能已经存在。 它仍需要大量的代码来从其获取有用的功能。 这就是在1.x 中的所有数据访问工作中的模型。

ASP.NET 2.0 在部分中与数据源控件进行寻址。 ASP.NET 2.0 中的数据源控件为开发人员提供了用于检索数据、显示数据和编辑数据的声明性模型。 数据源控件的用途是为数据绑定控件提供一致的数据表示形式，而不考虑这些数据的源。 ASP.NET 2.0 中数据源控件的核心是 DataSourceControl 抽象类。 DataSourceControl 类提供了 IDataSource 接口和 IListSource 接口的基实现，后者允许您将数据源控件指定为数据绑定控件的数据源（通过 new DataSourceId 属性）稍后讨论）并公开作为列表的数据。 数据源控件中的每个数据列表都作为 DataSourceView 对象公开。 对 DataSourceView 实例的访问由 IDataSource 接口提供。 例如，GetViewNames 方法返回一个 ICollection，该 ICollection 允许您枚举与特定数据源控件关联的 DataSourceViews，而 GetView 方法允许您按名称访问特定的 DataSourceView 实例。

数据源控件没有用户界面。 它们是作为服务器控件实现的，因此它们可以支持声明性语法，以便它们可以访问页状态（如果需要）。 数据源控件不会将任何 HTML 标记呈现给客户端。

> [!NOTE]
> 正如您稍后将看到的那样，还可以使用数据源控件获取缓存权益。

## <a name="storing-connection-strings"></a>存储连接字符串

在了解如何配置数据源控件之前，应介绍 ASP.NET 2.0 中关于连接字符串的新功能。 ASP.NET 2.0 在配置文件中引入了一个新的节，使你能够轻松地存储可在运行时动态读取的连接字符串。 &lt;connectionStrings&gt; "部分，可以轻松地存储连接字符串。

下面的代码片段将添加新的连接字符串。

[!code-xml[Main](data-source-controls/samples/sample1.xml)]

> [!NOTE]
> 与 &lt;appSettings&gt; 部分一样，&lt;connectionStrings&gt; 部分显示在配置文件中的 &lt;system.web&gt; 节之外。

若要使用此连接字符串，可以在设置服务器控件的 ConnectionString 属性时使用以下语法。

[!code-aspx[Main](data-source-controls/samples/sample2.aspx)]

还可以加密 &lt;connectionStrings&gt; 部分，以便不公开敏感信息。 此功能将在后面的模块中介绍。

## <a name="caching-data-sources"></a>缓存数据源

每个 DataSourceControl 都提供四个用于配置缓存的属性;EnableCaching、CacheDuration、CacheExpirationPolicy 和 CacheKeyDependency。

## <a name="enablecaching"></a>EnableCaching

EnableCaching 是一个布尔属性，用于确定是否为数据源控件启用缓存。

## <a name="cacheduration-property"></a>CacheDuration 属性

CacheDuration 属性设置缓存保持有效的秒数。 将此属性设置为**0**会使缓存保持有效，直到显式失效。

## <a name="cacheexpirationpolicy-property"></a>CacheExpirationPolicy 属性

CacheExpirationPolicy 属性可以设置为 "**绝对**" 或 "**可调**"。 如果将其设置为 "绝对"，则表示缓存数据所用的最长时间是 CacheDuration 属性指定的秒数。 通过将其设置为滑动，可在执行每个操作时重置过期时间。

## <a name="cachekeydependency-property"></a>CacheKeyDependency 属性

如果为 CacheKeyDependency 属性指定了字符串值，ASP.NET 将基于该字符串设置新的缓存依赖项。 这样，只需更改或删除 CacheKeyDependency，便可显式使缓存失效。

**重要提示**：如果启用模拟，并且对数据源和/或数据内容的访问基于客户端标识，则建议通过将 EnableCaching 设置为 False 来禁用缓存。 如果在此方案中启用了缓存，而用户不是最初请求数据发出请求的用户，则不会强制执行对数据源的授权。 数据将直接从缓存进行提供。

## <a name="the-sqldatasource-control"></a>SqlDataSource 控件

SqlDataSource 控件允许开发人员访问任何支持 ADO.NET 的关系数据库中存储的数据。 它可以使用 SqlClient 提供程序访问一个 SQL Server 数据库、一个提供程序、一个 System.data.oracleclient 提供程序或一个访问 Oracle 的提供程序的访问接口。 因此，SqlDataSource 并不是只用于访问 SQL Server 数据库中的数据。

为了使用 SqlDataSource，只需为 ConnectionString 属性提供一个值并指定一个 SQL 命令或存储过程。 SqlDataSource 控件负责处理基础 ADO.NET 体系结构。 它将打开连接，查询数据源或执行存储过程，返回数据，然后关闭连接。

> [!NOTE]
> 由于 DataSourceControl 类会自动为你关闭连接，因此它应减少通过泄漏数据库连接生成的客户调用的数量。

下面的代码片段使用存储在配置文件中的连接字符串，将 DropDownList 控件绑定到 SqlDataSource 控件，如上所示。

[!code-aspx[Main](data-source-controls/samples/sample3.aspx)]

如上图所示，SqlDataSource 的 DataSourceMode 属性指定了数据源的模式。 在上面的示例中，DataSourceMode 设置为 DataReader。 在这种情况下，SqlDataSource 将使用只进和只读游标返回 IDataReader 对象。 返回的对象的指定类型由所使用的提供程序控制。 在这种情况下，我使用的是 web.config 文件的 &lt;connectionStrings&gt; 部分中指定的 SqlClient 提供程序。 因此，返回的对象将为 SqlDataReader 类型。 通过指定数据集的 DataSourceMode 值，可将数据存储在服务器上的数据集中。 此模式允许添加排序、分页等功能。如果我已将 SqlDataSource 数据绑定到 GridView 控件，我将选择数据集模式。 但对于 DropDownList，DataReader 模式是正确的选择。

> [!NOTE]
> 缓存 SqlDataSource 或 AccessDataSource 时，DataSourceMode 属性必须设置为 DataSet。 如果使用 DataReader 的 DataSourceMode 启用缓存，则会出现异常。

## <a name="sqldatasource-properties"></a>SqlDataSource 属性

下面是 SqlDataSource 控件的某些属性。

### <a name="cancelselectonnullparameter"></a>CancelSelectOnNullParameter

一个布尔值，指定在其中一个参数为 null 时是否取消 select 命令。 默认值为 True。

### <a name="conflictdetection"></a>ConflictDetection

在多个用户可能同时更新数据源的情况下，ConflictDetection 属性决定了 SqlDataSource 控件的行为。 此属性的计算结果为 ConflictOptions 枚举的值之一。 这些值为**CompareAllValues**和**OverwriteChanges**。 如果设置为 OverwriteChanges，则最后一次将数据写入数据源的用户会覆盖以前的所有更改。 但是，如果将 ConflictDetection 属性设置为 CompareAllValues，则会为 SelectCommand 返回的列创建参数，同时还会创建参数来保存每个列中的原始值，从而使 SqlDataSource 成为确定在执行 SelectCommand 后值是否已更改。

### <a name="deletecommand"></a>DeleteCommand

设置或获取从数据库中删除行时使用的 SQL 字符串。 这可以是 SQL 查询或存储过程名称。

### <a name="deletecommandtype"></a>DeleteCommandType

设置或获取删除命令的类型（SQL 查询（Text）或存储过程（StoredProcedure））。

### <a name="deleteparameters"></a>DeleteParameters

返回与 SqlDataSource 控件关联的 SqlDataSourceView 对象的 DeleteCommand 使用的参数。

### <a name="oldvaluesparameterformatstring"></a>OldValuesParameterFormatString

当 ConflictDetection 属性设置为 CompareAllValues 时，此属性用于指定原始值参数的格式。 默认值为 {0} 这意味着原始值参数将采用与原始参数相同的名称。 换言之，如果字段名称为 "雇员 Id"，则原始值参数将 @EmployeeID。

### <a name="selectcommand"></a>SelectCommand

设置或获取用于从数据库检索数据的 SQL 字符串。 这可以是 SQL 查询或存储过程名称。

### <a name="selectcommandtype"></a>SelectCommandType

设置或获取 select 命令的类型（SQL 查询（Text）或存储过程（StoredProcedure））。

### <a name="selectparameters"></a>SelectParameters

返回与 SqlDataSource 控件关联的 SqlDataSourceView 对象的 SelectCommand 使用的参数。

### <a name="sortparametername"></a>SortParameterName

获取或设置在对数据源控件检索到的数据进行排序时使用的存储过程参数的名称。 仅当 SelectCommandType 设置为 StoredProcedure 时才有效。

### <a name="sqlcachedependency"></a>SqlCacheDependency

用分号分隔的字符串，用于指定 SQL Server 缓存依赖项中使用的数据库和表。 （SQL 缓存依赖关系将在后面的模块中讨论。）

### <a name="updatecommand"></a>UpdateCommand

设置或获取更新数据库中的数据时使用的 SQL 字符串。 这可以是 SQL 查询或存储过程名称。

### <a name="updatecommandtype"></a>UpdateCommandType

设置或获取更新命令的类型（SQL 查询（Text）或存储过程（StoredProcedure））。

### <a name="updateparameters"></a>UpdateParameters

返回与 SqlDataSource 控件关联的 SqlDataSourceView 对象的 UpdateCommand 使用的参数。

## <a name="the-accessdatasource-control"></a>AccessDataSource 控件

AccessDataSource 控件派生自 SqlDataSource 类，用于将数据绑定到 Microsoft Access 数据库。 AccessDataSource 控件的 ConnectionString 属性为只读属性。 "数据文件" 属性不使用 ConnectionString 属性，而是指向 Access 数据库，如下所示。

[!code-aspx[Main](data-source-controls/samples/sample4.aspx)]

AccessDataSource 将始终将基 SqlDataSource 的 ProviderName 设置为，并使用 OLE DB 提供程序连接到数据库中。 不能使用 AccessDataSource 控件连接到受密码保护的访问数据库。 如果必须连接到受密码保护的数据库，则应使用 SqlDataSource 控件。

> [!NOTE]
> 应将存储在网站中的数据库放置在应用\_数据目录中。 ASP.NET 不允许浏览该目录中的文件。 使用 Access 数据库时，需要将应用程序的 "读取" 和 "写入" 权限授予\_Data directory。

## <a name="the-xmldatasource-control"></a>XmlDataSource 控件

XmlDataSource 用于将 XML 数据绑定到数据绑定控件。 您可以使用数据文件属性绑定到 XML 文件，也可以使用数据属性绑定到 XML 字符串。 XmlDataSource 将 XML 特性公开为可绑定的字段。 如果需要绑定到不表示为属性的值，则需要使用 XSL 转换。 还可以使用 XPath 表达式来筛选 XML 数据。

请看下面的 XML 文件：

[!code-xml[Main](data-source-controls/samples/sample5.xml)]

请注意，XmlDataSource 使用*人员/人员*的 XPath 属性来仅筛选 &lt;人员&gt; 节点。 然后，DropDownList 使用 DataTextField 属性，将数据绑定到 LastName 特性。

尽管 XmlDataSource 控件主要用于数据绑定到只读 XML 数据，但可以编辑 XML 数据文件。 请注意，在这种情况下，XML 文件中的信息的自动插入、更新和删除操作不会自动发生，与其他数据源控件的操作一样。 相反，您必须编写代码以使用 XmlDataSource 控件的以下方法手动编辑数据。

### <a name="getxmldocument"></a>GetXmlDocument

检索包含由 XmlDataSource 检索到的 XML 代码的 XML。

### <a name="save"></a>保存

将内存中的 Xml 存储回数据源。

请注意，Save 方法仅在满足以下两个条件时才起作用：

1. XmlDataSource 使用数据文件属性来绑定到 XML 文件，而不是绑定到内存中 XML 数据的数据属性。
2. 不通过 Transform 或 TransformFile 属性指定转换。

另请注意，当多个用户同时调用时，Save 方法可能产生意外结果。

## <a name="the-objectdatasource-control"></a>ObjectDataSource 控件

我们已涵盖到目前为止的数据源控件是两层应用程序的最佳选择，其中的数据源控件直接与数据存储进行通信。 但是，许多实际应用程序是多层应用程序，其中的数据源控件可能需要与业务对象通信，而该对象又会与数据层通信。 在这些情况下，ObjectDataSource 会很好地填充帐单。 ObjectDataSource 与源对象一起工作。 如果对象具有实例方法而不是静态方法（在 Visual Basic 中共享），则 ObjectDataSource 控件将创建源对象的实例，调用指定的方法，并在单个请求的范围内释放对象实例。 因此，您的对象必须是无状态的。 也就是说，你的对象应获取并释放单个请求范围内的所有所需资源。 可以通过处理 ObjectDataSource 控件的 ObjectCreating 事件来控制如何创建源对象。 您可以创建源对象的实例，然后将 ObjectDataSourceEventArgs 类的 ObjectInstance 属性设置为该实例。 ObjectDataSource 控件将使用在 ObjectCreating 事件中创建的实例，而不是自己创建实例。

如果 ObjectDataSource 控件的源对象公开可调用以检索和修改数据的公共静态方法（在 Visual Basic 中共享），则 ObjectDataSource 控件将直接调用这些方法。 如果 ObjectDataSource 控件必须创建源对象的实例才能进行方法调用，则该对象必须包含不带任何参数的公共构造函数。 当 ObjectDataSource 控件创建源对象的新实例时，将调用此构造函数。

如果源对象不包含没有参数的公共构造函数，则可以创建将由 ObjectCreating 事件中的 ObjectDataSource 控件使用的源对象的实例。

## <a name="specifying-object-methods"></a>指定对象方法

ObjectDataSource 控件的源对象可以包含任意数量的用于选择、插入、更新或删除数据的方法。 根据方法的名称，ObjectDataSource 控件调用这些方法，如使用 ObjectDataSource 控件的 SelectMethod、InsertMethod、UpdateMethod 或 DeleteMethod 属性标识。 源对象还可以包含可选的 SelectCount 方法，该方法由 ObjectDataSource 控件使用 SelectCountMethod 属性标识，该方法返回数据源中对象的总数的计数。 在调用 Select 方法以检索数据源中用于分页的记录总数后，ObjectDataSource 控件将调用 SelectCount 方法。

## <a name="lab-using-data-source-controls"></a>使用数据源控件的实验室

## <a name="exercise-1---displaying-data-with-the-sqldatasource-control"></a>练习 1-通过 SqlDataSource 控件显示数据

以下练习使用 SqlDataSource 控件连接到 Northwind 数据库。 它假定您有权访问 SQL Server 2000 实例上的 Northwind 数据库。

1. 创建一个新的 ASP.NET 网站。
2. 添加新的 web.config 文件。

    1. 在解决方案资源管理器中右键单击该项目，然后单击 "添加新项"。
    2. 从模板列表中选择 "Web 配置文件"，然后单击 "添加"。
3. 编辑 &lt;connectionStrings&gt; "部分，如下所示： 

    [!code-aspx[Main](data-source-controls/samples/sample6.aspx)]
4. 切换到代码视图，并将 ConnectionString 属性和 SelectCommand 属性添加到 &lt;asp： SqlDataSource&gt; 控件，如下所示： 

    [!code-aspx[Main](data-source-controls/samples/sample7.aspx)]
5. 在设计视图中，添加一个新的 GridView 控件。
6. 从 "GridView 任务" 菜单中的 "选择数据源" 下拉列表中，选择 "SqlDataSource1"。
7. 右键单击 "default.aspx"，然后从菜单中选择 "在浏览器中查看"。 系统提示保存时单击 "是"。
8. GridView 显示 Products 表中的数据。

## <a name="exercise-2---editing-data-with-the-sqldatasource-control"></a>练习 2-用 SqlDataSource 控件编辑数据

以下练习演示了如何使用声明性语法对 DropDownList 控件进行数据绑定，并允许编辑 DropDownList 控件中显示的数据。

1. 在设计视图中，从 default.aspx 删除 GridView 控件。 

    **重要说明**：将 SqlDataSource 控件保留在页面上。
2. 将 DropDownList 控件添加到 default.aspx。
3. 切换到 "源" 视图。
4. 向 &lt;asp： DropDownList&gt; 控件添加 DataSourceId、DataTextField 和 DataValueField 属性，如下所示： 

    [!code-aspx[Main](data-source-controls/samples/sample8.aspx)]
5. 保存 default.aspx 并在浏览器中查看它。 请注意，DropDownList 包含 Northwind 数据库中的所有产品。
6. 关闭浏览器。
7. 在 default.aspx 的 "源" 视图中，在 DropDownList 控件下方添加一个新的 TextBox 控件。 将文本框的 "ID" 属性更改为 "txtProductName"。
8. 在 TextBox 控件下，添加一个新的按钮控件。 将按钮的 ID 属性更改为 btnUpdate，并将 Text 属性更改为 "**更新产品名称**"。
9. 在 default.aspx 的 "源" 视图中，将 UpdateCommand 属性和两个新 UpdateParameters 添加到 SqlDataSource 标记，如下所示： 

    [!code-aspx[Main](data-source-controls/samples/sample9.aspx)]

    > [!NOTE]
    > 请注意，在此代码中添加了两个更新参数（ProductName 和 ProductID）。 这些参数将映射到 txtProductName 文本框的 Text 属性和 ddlProducts DropDownList 的 SelectedValue 属性。
10. 切换到设计视图，然后双击按钮控件添加事件处理程序。
11. 将以下代码添加到 btnUpdate\_单击 "代码"： 

    [!code-csharp[Main](data-source-controls/samples/sample10.cs)]
12. 右键单击 "default.aspx"，然后选择在浏览器中查看它。 出现提示时单击 "是" 以保存所有更改。
13. ASP.NET 2.0 分部类允许在运行时进行编译。 为了查看代码更改生效，无需生成应用程序。
14. 从 DropDownList 中选择一个产品。
15. 在文本框中为所选产品输入新名称，然后单击 "更新" 按钮。
16. 在数据库中更新产品名称。

## <a name="exercise-3-using-the-objectdatasource-control"></a>练习3使用 ObjectDataSource 控件

本练习将演示如何使用 ObjectDataSource 控件和源对象与 Northwind 数据库进行交互。

1. 右键单击 "解决方案资源管理器中的项目，然后单击" 添加新项 "。
2. 在 "模板" 列表中选择 "Web 窗体"。 将名称更改为 default.aspx，然后单击 "添加"。
3. 右键单击 "解决方案资源管理器中的项目，然后单击" 添加新项 "。
4. 在 "模板" 列表中选择 "类"。 将类的名称更改为 NorthwindData.cs，然后单击 "添加"。
5. 系统提示将类添加到应用\_代码文件夹时，单击 "是"。
6. 将以下代码添加到 NorthwindData.cs 文件： 

    [!code-csharp[Main](data-source-controls/samples/sample11.cs)]
7. 将以下代码添加到对象的源视图： 

    [!code-aspx[Main](data-source-controls/samples/sample12.aspx)]
8. 保存所有文件并浏览对象 .aspx。
9. 通过查看详细信息、编辑员工、添加员工和删除员工，与界面进行交互。
