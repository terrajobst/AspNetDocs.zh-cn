---
uid: web-forms/overview/data-access/introduction/creating-a-data-access-layer-cs
title: 创建数据访问层（C#） |Microsoft Docs
author: rick-anderson
description: 在本教程中，我们将从头开始，使用类型化数据集创建数据访问层（DAL）来访问数据库中的信息。
ms.author: riande
ms.date: 04/05/2010
ms.assetid: cfe2a6a0-1e56-4dc8-9537-c8ec76ba96a4
msc.legacyurl: /web-forms/overview/data-access/introduction/creating-a-data-access-layer-cs
msc.type: authoredcontent
ms.openlocfilehash: 5aaf97dc8448dcb7b94ef2e4e23f34fd37ac4426
ms.sourcegitcommit: 6f0e10e4ca61a1e5534b09c655fd35cdc6886c8a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/15/2019
ms.locfileid: "74115278"
---
# <a name="creating-a-data-access-layer-c"></a>创建数据访问层 (C#)

作者： [Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载 PDF](creating-a-data-access-layer-cs/_static/datatutorial01cs1.pdf)

> 在本教程中，我们将从头开始，使用类型化数据集创建数据访问层（DAL）来访问数据库中的信息。

## <a name="introduction"></a>简介

作为 web 开发人员，我们的生活正在处理数据。 我们创建用于存储数据的数据库、用于检索和修改数据的代码，以及用于收集和汇总数据的网页。 这是较长系列教程中的第一个教程，该教程将探讨在 ASP.NET 2.0 中实现这些常用模式的方法。 首先，我们将创建由数据访问层（DAL）组成的[软件体系结构](http://en.wikipedia.org/wiki/Software_architecture)，使用类型化数据集、强制执行自定义业务规则的业务逻辑层（BLL）以及共享公共页面布局的 ASP.NET 页面。 在此后端基础布局完成后，我们将转到报告中，其中展示了如何显示、汇总、收集和验证来自 web 应用程序的数据。 这些教程旨在简洁明了，并提供有关多个屏幕截图的分步说明，以直观地完成此过程。 每个教程都在C#和 Visual Basic 版本中提供，并包括所使用的完整代码的下载。 （本教程中的第一个教程非常耗时，但其余的理解块会更多。）

对于这些教程，我们将使用位于**应用\_数据**目录中的 Northwind 数据库的 Microsoft SQL Server 2005 Express Edition 版本。 除了数据库文件，**应用\_Data**文件夹还包含用于创建数据库的 SQL 脚本，以防您要使用不同的数据库版本。 如果愿意，也可以[直接从 Microsoft 下载](https://www.microsoft.com/downloads/details.aspx?FamilyID=06616212-0356-46a0-8da2-eebc53a68034&amp;DisplayLang=en)这些脚本。 如果使用不同的 SQL Server 版本的 Northwind 数据库，则需要更新应用程序的**web.config**文件中的**NORTHWNDConnectionString**设置。 Web 应用程序是使用 Visual Studio 2005 Professional Edition 作为基于文件系统的网站项目生成的。 但是，所有教程都将同样适用于 Visual Studio 2005 （ [Visual Web Developer](https://msdn.microsoft.com/vstudio/express/vwd/)）的免费版本。  
  
在本教程中，我们将从头开始创建数据访问层（DAL），然后在第二个教程中创建业务逻辑层（BLL），并在第三个教程中处理页面布局和导航。 第三个教程之后的教程将基于前三个中的基础布局进行构建。 在本教程的第一篇教程中，我们有很多介绍，因此请启动 Visual Studio，让我们开始吧！

## <a name="step-1-creating-a-web-project-and-connecting-to-the-database"></a>步骤1：创建 Web 项目并连接到数据库

在我们可以创建数据访问层（DAL）之前，首先需要创建一个网站并设置数据库。 首先，创建新的基于文件系统的 ASP.NET 网站。 若要实现此目的，请在 "文件" 菜单中选择 "新建网站"，并显示 "新建网站" 对话框。 选择 ASP.NET 网站模板，将 "位置" 下拉列表设置为 "文件系统"，选择要放置该网站的文件夹，并将语言设置为C#。

[![创建基于文件系统的新网站](creating-a-data-access-layer-cs/_static/image2.png)](creating-a-data-access-layer-cs/_static/image1.png)

**图 1**：创建新的基于文件系统的网站（[单击查看完全大小的图像](creating-a-data-access-layer-cs/_static/image3.png)）

这将创建一个新网站，其中包含**默认的 .aspx** ASP.NET 页和一个**应用\_Data**文件夹。

创建网站后，下一步是在 Visual Studio 的服务器资源管理器中添加对数据库的引用。 通过将数据库添加到服务器资源管理器您可以在 Visual Studio 中添加表、存储过程、视图等。 还可以通过查询生成器手动或以图形方式查看表数据或创建自己的查询。 此外，当我们为 DAL 生成类型化数据集时，我们需要将 Visual Studio 指向用于构造类型化数据集的数据库。 虽然我们可以在该时间点提供此连接信息，但 Visual Studio 会自动填充已在服务器资源管理器中注册的数据库的下拉列表。

将 Northwind 数据库添加到服务器资源管理器的步骤取决于您是要使用**应用\_Data**文件夹中的 SQL Server 2005 Express Edition 数据库，还是要改为使用 Microsoft SQL Server 2000 或2005数据库服务器安装程序。

## <a name="using-a-database-in-the-app_data-folder"></a>在应用中使用数据库\_Data 文件夹

如果没有要连接到 SQL Server 2000 或2005数据库服务器，或者只是想要避免将数据库添加到数据库服务器，则可以使用下载网站的**应用\_Data**文件夹（northwnd.mdf）中的 SQL Server 2005 Express Edition 版本 Northwind 数据库 **.MDF**）。

放置在**应用\_Data**文件夹中的数据库将自动添加到服务器资源管理器中。 假设计算机上已安装 SQL Server 2005 Express Edition，应会看到名为 NORTHWND.MDF 的节点。服务器资源管理器中的 MDF，你可以展开并浏览其表、视图、存储过程等（参见图2）。

**应用\_Data**文件夹还可以保存 Microsoft Access **.mdb**文件，如其 SQL Server 对应项，它们会自动添加到服务器资源管理器中。 如果不想使用任何 SQL Server 选项，则始终可以[下载 Northwind 数据库文件的 Microsoft Access 版本](https://www.microsoft.com/downloads/details.aspx?FamilyID=C6661372-8DBE-422B-8676-C632D66C529C&amp;displaylang=EN)，并将其放入**应用\_数据**目录中。 但请记住，访问数据库与 SQL Server 功能不同，并且不是在网站方案中使用而设计的。 而且，有几个以上的教程将使用 Access 不支持的某些数据库级功能。

## <a name="connecting-to-the-database-in-a-microsoft-sql-server-2000-or-2005-database-server"></a>连接到 Microsoft SQL Server 2000 或2005数据库服务器中的数据库

或者，您可以连接到在数据库服务器上安装的 Northwind 数据库。 如果数据库服务器尚未安装 Northwind 数据库，则必须先通过运行本教程下载中包含的安装脚本，或直接从 Microsoft 网站[下载 SQL Server 2000 版 Northwind 和安装脚本](https://www.microsoft.com/downloads/details.aspx?FamilyID=06616212-0356-46a0-8da2-eebc53a68034&amp;DisplayLang=en)，将其添加到数据库服务器。

安装数据库后，请在 Visual Studio 中转到服务器资源管理器，右键单击 "数据连接" 节点，然后选择 "添加连接"。 如果看不到 "服务器资源管理器请访问视图/服务器资源管理器，或按 Ctrl + Alt + S。 此时将显示 "添加连接" 对话框，你可以在该对话框中指定要连接的服务器、身份验证信息和数据库名称。 成功配置数据库连接信息并单击 "确定" 按钮后，该数据库将添加为 "数据连接" 节点下的节点。 您可以展开 "数据库" 节点以浏览其表、视图和存储过程等。

![添加与数据库服务器的 Northwind 数据库的连接](creating-a-data-access-layer-cs/_static/image4.png)

**图 2**：将连接添加到数据库服务器的 Northwind 数据库

## <a name="step-2-creating-the-data-access-layer"></a>步骤2：创建数据访问层

当处理数据时，一个选项是将特定于数据的逻辑直接嵌入到表示层（在 web 应用程序中，ASP.NET 页面构成表示层）。 这可能采用以下形式：在 ASP.NET 页面的代码部分中编写 ADO.NET 代码，或从标记部分使用 SqlDataSource 控件。 在这两种情况下，这种方法将数据访问逻辑与表示层紧密耦合在一起。 不过，建议的方法是将数据访问逻辑与表示层区分开来。 这个单独的层称为数据访问层，DAL 表示 short，通常作为单独的类库项目来实现。 此分层体系结构的优点已记录良好（有关这些优点的信息，请参阅本教程末尾的 "进一步阅读" 部分），这是我们将在此系列中采用的方法。

所有特定于基础数据源的代码（例如创建与数据库的连接、发出**SELECT**、 **INSERT**、 **UPDATE**和**DELETE**命令等）都应该位于 DAL。 表示层不应包含对此类数据访问代码的任何引用，但应改为对任何和所有数据请求调用 DAL。 数据访问层通常包含用于访问基础数据库数据的方法。 例如，Northwind 数据库具有 "**产品**" 和 "**类别**" 表，它们记录要销售的产品及其所属的类别。 在我们的 DAL 中，我们将有如下方法：

- **GetCategories （），** 将返回有关所有类别的信息
- **GetProducts （）** ，将返回有关所有产品的信息
- **GetProductsByCategoryID （*类别 id*）** ，将返回属于指定类别的所有产品
- **GetProductByProductID （*productID*）** ，将返回有关特定产品的信息

这些方法在调用时会连接到数据库，发出适当的查询并返回结果。 我们返回这些结果的方式非常重要。 这些方法只是返回由数据库查询填充的数据集或 DataReader，但最好使用*强类型对象*返回这些结果。 强类型对象是其架构在编译时严格定义的对象，相反，松散类型化对象是指其架构在运行时之前是未知的。

例如，DataReader 和 DataSet （默认情况下）是松散类型化的对象，因为它们的架构由用于填充它们的数据库查询所返回的列定义。 若要从松散类型的 DataTable 访问特定列，需要使用类似于以下内容的语法：  <strong><em>DataTable</em>。Rows [<em>index</em>] ["<em>columnName</em>"]</strong>。 在此示例中，DataTable 的松散类型会表现为需要使用字符串或序号索引访问列名的事实。 另一方面，强类型的数据表会将其每个列作为属性实现，生成的代码如下所示：  <strong><em>DataTable</em>。Rows [<em>index</em>]。*columnName</strong>* 。

若要返回强类型对象，开发人员可以创建自己的自定义业务对象或使用类型化数据集。 业务对象由开发人员作为类实现，该类的属性通常反映业务对象表示的基础数据库表的列。 类型化数据集是由 Visual Studio 基于数据库架构生成的类，其成员根据此架构进行强类型化。 类型化数据集本身由扩展 ADO.NET 数据集、DataTable 和 DataRow 类的类组成。 除了强类型数据表以外，类型化的数据集现在还包括 Tableadapter，这些类具有用于填充数据集的数据表和将数据表中的修改传播回数据库的方法。

> [!NOTE]
> 有关使用类型化数据集与自定义业务对象的优点和缺点的详细信息，请参阅[设计数据层组件和通过层传递数据](https://msdn.microsoft.com/library/ms978496.aspx)。

我们会将强类型化数据集用于这些教程的体系结构。 图3说明了使用类型化数据集的应用程序的不同层之间的工作流。

[![将所有数据访问代码归入 DAL](creating-a-data-access-layer-cs/_static/image6.png)](creating-a-data-access-layer-cs/_static/image5.png)

**图 3**：将所有数据访问代码归入 DAL （[单击以查看完全大小的图像](creating-a-data-access-layer-cs/_static/image7.png)）

## <a name="creating-a-typed-dataset-and-table-adapter"></a>创建类型化数据集和表适配器

若要开始创建 DAL，我们首先向项目中添加类型化数据集。 若要实现此目的，请在解决方案资源管理器中右键单击项目节点，然后选择 "添加新项"。 从模板列表中选择 "数据集" 选项，并将其命名为 " **Northwind**"。

[![选择向项目添加新的数据集](creating-a-data-access-layer-cs/_static/image9.png)](creating-a-data-access-layer-cs/_static/image8.png)

**图 4**：选择将新的数据集添加到项目中（[单击以查看完全大小的图像](creating-a-data-access-layer-cs/_static/image10.png)）

单击 "添加" 后，系统提示将数据集添加到**应用\_代码**文件夹中时，请选择 "是"。 然后，将显示类型化数据集的设计器，并启动 TableAdapter 配置向导，使你可以将第一个 TableAdapter 添加到类型化数据集。

类型化数据集用作数据的强类型集合;它由强类型的 DataTable 实例组成，其中每个实例又构成强类型的 DataRow 实例。 我们将为每个需要在本教程系列中使用的基础数据库表创建一个强类型的数据表。 首先，让我们为**Products**表创建 DataTable。

请记住，强类型的数据表不包含有关如何访问其基础数据库表中的数据的任何信息。 为了检索用于填充 DataTable 的数据，我们使用 TableAdapter 类作为数据访问层。 对于**Products** DataTable，TableAdapter 将包含方法**GetProducts （）** 、 **GetProductByCategoryID （*类别 id*）** 等，我们将从表示层调用这些方法。 DataTable 的角色充当用于在层之间传递数据的强类型对象。

TableAdapter 配置向导首先提示您选择要使用的数据库。 下拉列表显示了服务器资源管理器中的数据库。 如果未将 Northwind 数据库添加到服务器资源管理器，则此时可以单击 "新建连接" 按钮来执行此操作。

[从下拉列表中 ![选择 Northwind 数据库](creating-a-data-access-layer-cs/_static/image12.png)](creating-a-data-access-layer-cs/_static/image11.png)

**图 5**：从下拉列表中选择 Northwind 数据库（[单击以查看完全大小的映像](creating-a-data-access-layer-cs/_static/image13.png)）

选择数据库并单击 "下一步" 后，系统会询问你是否要将连接字符串**保存到 web.config 文件中**。 通过保存连接字符串，你将避免在 TableAdapter 类中对其进行硬编码，从而简化了连接字符串信息将来的更改。 如果选择将连接字符串保存在配置文件中，则该字符串位于 **&lt;connectionStrings&gt;** "部分中，可以选择对其进行[加密](http://aspnet.4guysfromrolla.com/articles/021506-1.aspx)以提高安全性，也可以在以后通过 IIS GUI 管理工具中的" 新建 ASP.NET 2.0 "属性页进行修改，这对管理员更加理想。

[![将连接字符串保存到 web.config](creating-a-data-access-layer-cs/_static/image15.png)](creating-a-data-access-layer-cs/_static/image14.png)

**图 6**：将连接字符串保存到**web.config （** [单击以查看完全大小的图像](creating-a-data-access-layer-cs/_static/image16.png)）

接下来，我们需要为第一个强类型的 DataTable 定义架构，并提供在填充强类型化数据集时用于 TableAdapter 的第一种方法。 这两个步骤是通过创建一个查询来实现的，该查询返回表中我们要在 DataTable 中反映的列。 在向导结束时，我们将为此查询指定方法名称。 完成此操作后，可以从表示层调用此方法。 方法将执行定义的查询并填充强类型的 DataTable。

若要开始定义 SQL 查询，我们必须首先指出我们希望 TableAdapter 如何发出查询。 我们可以使用即席 SQL 语句、创建新的存储过程或使用现有的存储过程。 对于这些教程，我们将使用即席 SQL 语句。 有关使用存储过程的示例，请参阅[Brian Noyes](http://briannoyes.net/)的文章[使用 Visual Studio 2005 数据集设计器生成数据访问层](http://www.theserverside.net/articles/showarticle.tss?id=DataSetDesigner)。

[使用即席 SQL 语句 ![查询数据](creating-a-data-access-layer-cs/_static/image18.png)](creating-a-data-access-layer-cs/_static/image17.png)

**图 7**：使用即席 SQL 语句查询数据（[单击以查看完全大小的映像](creating-a-data-access-layer-cs/_static/image19.png)）

此时，我们可以手动键入 SQL 查询。 在 TableAdapter 中创建第一个方法时，通常希望让查询返回那些需要在对应的 DataTable 中表达的列。 为此，我们可以创建一个查询，该查询返回**Products**表中的所有列和所有行：

[![在文本框中输入 SQL 查询](creating-a-data-access-layer-cs/_static/image21.png)](creating-a-data-access-layer-cs/_static/image20.png)

**图 8**：在文本框中输入 SQL 查询（[单击以查看完全大小的图像](creating-a-data-access-layer-cs/_static/image22.png)）

或者，使用查询生成器，并以图形方式构造查询，如图9所示。

[![通过查询编辑器以图形方式创建查询](creating-a-data-access-layer-cs/_static/image24.png)](creating-a-data-access-layer-cs/_static/image23.png)

**图 9**：通过查询编辑器以图形方式创建查询（[单击查看完全大小的图像](creating-a-data-access-layer-cs/_static/image25.png)）

创建查询后，但在转到下一屏之前，请单击 "高级选项" 按钮。 在网站项目中，"生成 Insert、Update 和 Delete 语句" 是默认情况下唯一选择的高级选项;如果从类库或 Windows 项目运行此向导，则还将选择 "使用开放式并发" 选项。 暂时取消选中 "使用开放式并发" 选项。 我们将在将来的教程中检查乐观并发。

[![仅选择 "生成 Insert、Update 和 Delete 语句" 选项](creating-a-data-access-layer-cs/_static/image27.png)](creating-a-data-access-layer-cs/_static/image26.png)

**图 10**：仅选择 "生成 Insert、Update 和 Delete 语句" 选项（[单击以查看完全大小的映像](creating-a-data-access-layer-cs/_static/image28.png)）

验证高级选项后，请单击 "下一步" 以进入最终屏幕。 此时，系统会要求选择要添加到 TableAdapter 的方法。 用于填充数据的模式有两种：

- 使用此方法**填充 datatable**会创建一个方法，该方法以 DataTable 作为参数，并根据查询的结果来填充它。 例如，ADO.NET DataAdapter 类通过其**Fill （）** 方法实现此模式。
- 使用此方法**返回 datatable** 。方法创建并填充 datatable，并将其作为方法返回值返回。

可以让 TableAdapter 实现其中一种或两种模式。 还可以重命名此处提供的方法。 让我们将这两个复选框保持选中状态，尽管我们在这些教程中只使用后一种模式。 同样，让我们将**GetProducts** **的方法重**命名为。

如果选中，最后一个复选框 "GenerateDBDirectMethods" 将为 TableAdapter 创建**Insert （）** 、 **Update （）** 和**Delete （）** 方法。 如果将此选项保留为未选中状态，则需要通过 TableAdapter 的唯一**Update （）** 方法完成所有更新，该方法采用类型化数据集、DataTable、单个 DataRow 或 datarow 数组。 （如果已从图9的高级属性中取消选中 "生成插入、更新和删除语句" 选项，则此复选框的设置不起作用。）让我们选中此复选框。

[![将方法名称从 "GetProducts" 更改为 ""](creating-a-data-access-layer-cs/_static/image30.png)](creating-a-data-access-layer-cs/_static/image29.png)

**图 11**：将方法**名称从 "** GetProducts" 更改为["" （单击查看完全大小的图像](creating-a-data-access-layer-cs/_static/image31.png)）

单击 "完成" 完成向导。 向导关闭后，将返回到 "数据集设计器"，其中显示刚刚创建的 DataTable。 您可以在**Products**数据表（**ProductID**、 **ProductName**等）中查看列的列表，以及**ProductsTableAdapter** （**Fill （）** 和**GetProducts （）** ）的方法。

[![Products DataTable 和 ProductsTableAdapter 已添加到类型化数据集](creating-a-data-access-layer-cs/_static/image33.png)](creating-a-data-access-layer-cs/_static/image32.png)

**图 12**：已将**Products** DataTable 和**ProductsTableAdapter**添加到类型化数据集（[单击以查看完全大小的图像](creating-a-data-access-layer-cs/_static/image34.png)）

此时，我们有一个具有单个 DataTable （**Northwind**）的类型化数据集，以及一个具有**GetProducts （）** 方法的强类型 DataAdapter 类（**NorthwindTableAdapters. ProductsTableAdapter**）。 这些对象可用于从代码访问所有产品的列表，例如：

[!code-html[Main](creating-a-data-access-layer-cs/samples/sample1.html)]

此代码不要求我们编写一位特定于数据访问的代码。 我们不必实例化任何 ADO.NET 类，我们也不必引用任何连接字符串、SQL 查询或存储过程。 而 TableAdapter 为我们提供低级别的数据访问代码。

在此示例中使用的每个对象都是强类型的，允许 Visual Studio 提供 IntelliSense 和编译时类型检查。 并且最重要的是，TableAdapter 返回的所有数据表都可以绑定到 ASP.NET 数据 Web 控件，如 GridView、DetailsView、DropDownList、CheckBoxList 等。 下面的示例演示如何将**GetProducts （）** 方法返回的 DataTable 绑定到仅在**页面\_Load**事件处理程序中的扫描三行代码中。

AllProducts .aspx

[!code-aspx[Main](creating-a-data-access-layer-cs/samples/sample2.aspx)]

AllProducts.aspx.cs

[!code-csharp[Main](creating-a-data-access-layer-cs/samples/sample3.cs)]

[![产品列表显示在 GridView 中](creating-a-data-access-layer-cs/_static/image36.png)](creating-a-data-access-layer-cs/_static/image35.png)

**图 13**：产品列表显示在 GridView 中（[单击以查看完全大小的图像](creating-a-data-access-layer-cs/_static/image37.png)）

尽管此示例需要我们在 ASP.NET 页面的页面中编写三行代码 **\_Load**事件处理程序中，但在将来的教程中，我们将检查如何使用 ObjectDataSource 以声明方式从 DAL 检索数据。 使用 ObjectDataSource 时，我们不需要编写任何代码，也会获得分页和排序支持！

## <a name="step-3-adding-parameterized-methods-to-the-data-access-layer"></a>步骤3：将参数化方法添加到数据访问层

此时，我们的**ProductsTableAdapter**类具有一个**GetProducts （）** 方法，该方法返回数据库中的所有产品。 虽然能够使用所有产品都非常有用，但有时我们需要检索有关特定产品或属于特定类别的所有产品的信息。 若要将此类功能添加到数据访问层，可以将参数化方法添加到 TableAdapter。

我们来添加**GetProductsByCategoryID （*类别 id*）** 方法。 若要将新方法添加到 DAL，请返回到 "数据集设计器"，右键单击 " **ProductsTableAdapter** " 部分，然后选择 "添加查询"。

![右键单击 TableAdapter，然后选择 "添加查询"](creating-a-data-access-layer-cs/_static/image38.png)

**图 14**：右键单击 TableAdapter，然后选择 "添加查询"

我们首先会提示你是否要使用即席 SQL 语句或新的或现有的存储过程来访问数据库。 让我们再次选择使用即席 SQL 语句。 接下来，我们会询问我们要使用哪种类型的 SQL 查询。 由于我们希望返回属于指定类别的所有产品，因此我们希望编写一个返回行的**SELECT**语句。

[![选择创建返回行的 SELECT 语句](creating-a-data-access-layer-cs/_static/image40.png)](creating-a-data-access-layer-cs/_static/image39.png)

**图 15**：选择创建返回行的**SELECT**语句（[单击以查看完全大小的图像](creating-a-data-access-layer-cs/_static/image41.png)）

下一步是定义用于访问数据的 SQL 查询。 由于我们只想返回属于特定类别的产品，因此我使用<strong>GetProducts （）</strong>中的相同<strong>SELECT</strong>语句，但添加以下<strong>WHERE</strong>子句：<strong>其中，类别 id = @CategoryID</strong>。 <strong>@CategoryID</strong>参数向 TableAdapter 向导指示我们正在创建的方法将需要相应类型的输入参数（即，可以为 null 的整数）。

[![输入查询以仅返回指定类别中的产品](creating-a-data-access-layer-cs/_static/image43.png)](creating-a-data-access-layer-cs/_static/image42.png)

**图 16**：输入仅返回指定类别中的产品的查询（[单击以查看完全大小的图像](creating-a-data-access-layer-cs/_static/image44.png)）

在最后一步中，我们可以选择要使用的数据访问模式，还可以自定义生成的方法的名称。 对于填充模式，让我们将名称更改为<strong>FillByCategoryID</strong> ，并为返回 DataTable 返回模式（ <strong>Get*X</strong>* 方法），让我们使用<strong>GetProductsByCategoryID</strong>。

[![选择 TableAdapter 方法的名称](creating-a-data-access-layer-cs/_static/image46.png)](creating-a-data-access-layer-cs/_static/image45.png)

**图 17**：选择 TableAdapter 方法的名称（[单击以查看完全大小的映像](creating-a-data-access-layer-cs/_static/image47.png)）

完成向导后，数据集设计器会包括新的 TableAdapter 方法。

![现在可以按类别查询产品](creating-a-data-access-layer-cs/_static/image48.png)

**图 18**：现在可以按类别查询产品

请花点时间使用相同的方法添加**GetProductByProductID （*productID*）** 方法。

这些参数化查询可以直接从数据集设计器进行测试。 右键单击 TableAdapter 中的方法，然后选择 "预览数据"。 接下来，输入要用于参数的值，然后单击 "预览"。

[![显示属于饮料类别的产品](creating-a-data-access-layer-cs/_static/image50.png)](creating-a-data-access-layer-cs/_static/image49.png)

**图 19**：显示属于 "饮料" 类别的产品（[单击以查看完全尺寸的图像](creating-a-data-access-layer-cs/_static/image51.png)）

对于 DAL 中的**GetProductsByCategoryID （*类别 id*）** 方法，我们现在可以创建只显示指定类别中的产品的 ASP.NET 页面。 下面的示例显示 "饮料" 类别中的所有产品，其类别**id**为 "1"。

饮料

[!code-aspx[Main](creating-a-data-access-layer-cs/samples/sample4.aspx)]

Beverages.aspx.cs

[!code-csharp[Main](creating-a-data-access-layer-cs/samples/sample5.cs)]

[![显示 "饮料" 类别中的产品](creating-a-data-access-layer-cs/_static/image53.png)](creating-a-data-access-layer-cs/_static/image52.png)

**图 20**：显示 "饮料" 类别中的产品（[单击以查看完全尺寸的图像](creating-a-data-access-layer-cs/_static/image54.png)）

## <a name="step-4-inserting-updating-and-deleting-data"></a>步骤4：插入、更新和删除数据

通常有两种模式可用于插入、更新和删除数据。 第一种模式是，我将调用数据库直接模式，这涉及到创建在调用时向处理单个数据库记录的数据库发出**INSERT**、 **UPDATE**或**DELETE**命令的方法。 此类方法通常以与要插入、更新或删除的值对应的一系列标量值（整数、字符串、布尔值、Datetime 等）进行传递。 例如，对于**Products**表，delete 方法将采用一个整数参数，指示要删除的记录的**ProductID** ，而 Insert 方法将接受**ProductName**的字符串，为**单价**使用一个小数，为**UnitsOnStock**提供一个整数，依此类推。

[![会立即向数据库发送每个 Insert、Update 和 Delete 请求](creating-a-data-access-layer-cs/_static/image56.png)](creating-a-data-access-layer-cs/_static/image55.png)

**图 21**：每个插入、更新和删除请求都将立即发送到数据库（[单击查看完全大小的映像](creating-a-data-access-layer-cs/_static/image57.png)）

另一种模式是将作为批处理更新模式，它是在一个方法调用中更新整个数据集、DataTable 或 Datarow 集合。 使用此模式，开发人员可以删除、插入和修改 DataTable 中的 Datarow，然后将这些 Datarow 或 DataTable 传递到 update 方法。 然后，此方法枚举传入的 Datarow，确定是否已修改、添加或删除它们（通过 DataRow 的[RowState 属性](https://msdn.microsoft.com/library/system.data.datarow.rowstate.aspx)值），并为每个记录发出适当的数据库请求。

[在调用 Update 方法时，![所有更改均与数据库同步](creating-a-data-access-layer-cs/_static/image59.png)](creating-a-data-access-layer-cs/_static/image58.png)

**图 22**：调用 Update 方法时，所有更改都将与数据库同步（[单击查看完全大小的映像](creating-a-data-access-layer-cs/_static/image60.png)）

默认情况下，TableAdapter 使用批处理更新模式，但也支持 DB 直接模式。 由于在创建 TableAdapter 时，我们从高级属性中选择了 "生成插入、更新和删除语句" 选项，因此**ProductsTableAdapter**包含用于实现批处理更新模式的**Update （）** 方法。 具体而言，TableAdapter 包含**Update （）** 方法，该方法可以传递类型化的数据集、强类型的 DataTable 或一个或多个 datarow。 如果在首次创建 TableAdapter 时选中了 "GenerateDBDirectMethods" 复选框，则 DB 直接模式也将通过**Insert （）** 、 **Update （）** 和**Delete （）** 方法实现。

这两种数据修改模式都使用 TableAdapter 的**InsertCommand**、 **UpdateCommand**和**DeleteCommand**属性向数据库发出**INSERT**、 **UPDATE**和**DELETE**命令。 可以通过在数据集设计器中单击 TableAdapter，然后转到属性窗口来检查和修改**InsertCommand**、 **UpdateCommand**和**DeleteCommand**属性。 （请确保已选择 TableAdapter，并且**ProductsTableAdapter**对象是在属性窗口的下拉列表中选择的对象。）

[![TableAdapter 具有 InsertCommand、UpdateCommand 和 DeleteCommand 属性](creating-a-data-access-layer-cs/_static/image62.png)](creating-a-data-access-layer-cs/_static/image61.png)

**图 23**： TableAdapter 具有**InsertCommand**、 **UpdateCommand**和**DeleteCommand**属性（[单击以查看完全大小的图像](creating-a-data-access-layer-cs/_static/image63.png)）

若要检查或修改这些数据库命令属性中的任何一个，请单击 " **CommandText** " 子属性，此时将显示查询生成器。

[![在查询生成器中配置 INSERT、UPDATE 和 DELETE 语句](creating-a-data-access-layer-cs/_static/image65.png)](creating-a-data-access-layer-cs/_static/image64.png)

**图 24**：在查询生成器中配置**INSERT**、 **UPDATE**和**DELETE**语句（[单击以查看完全大小的图像](creating-a-data-access-layer-cs/_static/image66.png)）

下面的代码示例演示如何使用批处理更新模式将所有未停用的产品的价格翻倍，并使其具有25个单位或更低的价格：

[!code-csharp[Main](creating-a-data-access-layer-cs/samples/sample6.cs)]

下面的代码演示了如何使用 DB 直接模式以编程方式删除特定产品，然后更新一个产品，然后添加一个新产品：

[!code-csharp[Main](creating-a-data-access-layer-cs/samples/sample7.cs)]

## <a name="creating-custom-insert-update-and-delete-methods"></a>创建自定义插入、更新和删除方法

DB 直接方法创建的**Insert （）** 、 **Update （）** 和**Delete （）** 方法可能有点麻烦，特别是对于包含多个列的表。 查看上面的代码示例，如果不包含 IntelliSense 的帮助，就不会特别清楚哪些**Products**表列将映射到**Update （）** 和**Insert （）** 方法的每个输入参数。 有时，我们可能只想要更新单个列或两个列，或者需要一个自定义的**Insert （）** 方法，该方法可能会返回新插入记录的**标识**（自动递增）字段的值。

若要创建此类自定义方法，请返回到数据集设计器。 右键单击 TableAdapter，然后选择 "添加查询"，返回到 "TableAdapter 向导"。 在第二个屏幕上，可以指示要创建的查询类型。 让我们创建一个方法，该方法添加一个新产品，然后返回新添加的记录的**ProductID**的值。 因此，选择创建**插入**查询。

[![创建方法以便向 Products 表中添加新行](creating-a-data-access-layer-cs/_static/image68.png)](creating-a-data-access-layer-cs/_static/image67.png)

**图 25**：创建方法以便向**Products**表中添加新行（[单击以查看完全大小的图像](creating-a-data-access-layer-cs/_static/image69.png)）

在下一个屏幕上，将显示**InsertCommand**的**CommandText** 。 通过在查询的末尾添加**SELECT SCOPE\_IDENTITY （）** 来增加此查询，这将返回插入到同一范围内的**identity**列中的最后一个标识值。 （有关详细信息，请参阅[技术文档](https://msdn.microsoft.com/library/ms190315.aspx) **\_标识（）** ，以及为何要[使用范围\_identity （）代替 @@IDENTITY](http://weblogs.sqlteam.com/travisl/archive/2003/10/29/405.aspx)。）请确保在添加**SELECT**语句前用分号结束**INSERT**语句。

[![增加查询以返回 SCOPE_IDENTITY （）值](creating-a-data-access-layer-cs/_static/image71.png)](creating-a-data-access-layer-cs/_static/image70.png)

**图 26**：增加查询以返回**范围\_IDENTITY （）** 值（[单击查看完全大小的映像](creating-a-data-access-layer-cs/_static/image72.png)）

最后，将新方法命名为**InsertProduct**。

[![将新方法名称设置为 InsertProduct](creating-a-data-access-layer-cs/_static/image74.png)](creating-a-data-access-layer-cs/_static/image73.png)

**图 27**：将新方法名称设置为**InsertProduct** （[单击查看完全大小的图像](creating-a-data-access-layer-cs/_static/image75.png)）

当你返回到数据集设计器时，你将看到**ProductsTableAdapter**包含一个新的方法**InsertProduct**。 如果此新方法不具有**Products**表中每个列的参数，则可能是忘记使用分号终止**INSERT**语句。 配置**InsertProduct**方法，并确保用分号分隔**INSERT**和**SELECT**语句。

默认情况下，插入方法发出非查询方法，这意味着它们会返回受影响的行数。 但是，我们希望**InsertProduct**方法返回查询返回的值，而不是受影响的行数。 若要实现此目的，请将**InsertProduct**方法的**ExecuteMode**属性调整为**标量**。

[![将 ExecuteMode 属性更改为标量](creating-a-data-access-layer-cs/_static/image77.png)](creating-a-data-access-layer-cs/_static/image76.png)

**图 28**：将**ExecuteMode**属性更改为**标量**（[单击以查看完全大小的图像](creating-a-data-access-layer-cs/_static/image78.png)）

下面的代码演示了此新的**InsertProduct**方法：

[!code-csharp[Main](creating-a-data-access-layer-cs/samples/sample8.cs)]

## <a name="step-5-completing-the-data-access-layer"></a>步骤5：完成数据访问层

请注意， **ProductsTableAdapters**类从**Products**表中返回 "类别名称"**和 "** **供应商**" 值，但不包括 "类别" 表中的 "**类别** **名称**" 列或 "**供应商**" 表中的 "**公司名称**" 列，尽管这可能是我们在显示产品信息时要显示的列。 我们可以扩充 TableAdapter 的初始方法**GetProducts （）** ，以同时包含 "**类别名称**" 和 "**公司名称**" 列值，这将更新强类型的 DataTable 以包含这些新列。

但这可能会出现问题，因为用于插入、更新和删除数据的 TableAdapter 方法基于此初始方法。 幸运的是，用于插入、更新和删除的自动生成的方法不受**SELECT**子句中的子查询的影响。 通过小心将查询添加到**类别**和**供应商**（而不是**联接**），我们将避免不得不改编这些方法来修改数据。 右键单击**ProductsTableAdapter**中的**GetProducts （）** 方法，然后选择 "配置"。 然后，调整**SELECT**子句，使其类似于：

[!code-sql[Main](creating-a-data-access-layer-cs/samples/sample9.sql)]

[![为 GetProducts （）方法更新 SELECT 语句](creating-a-data-access-layer-cs/_static/image80.png)](creating-a-data-access-layer-cs/_static/image79.png)

**图 29**：更新**GetProducts （）** 方法的**SELECT**语句（[单击以查看完全大小的图像](creating-a-data-access-layer-cs/_static/image81.png)）

更新**GetProducts （）** 方法以使用此新查询后，DataTable 将包括两个新列：**类别名称**和**供应商**。

![Products DataTable 有两个新列](creating-a-data-access-layer-cs/_static/image82.png)

**图 30**： **Products** DataTable 有两个新列

请花点时间更新**GetProductsByCategoryID （*类别 id*）** 方法中的**SELECT**子句。

如果使用**联接**语法更新**GetProducts （）** **选择**，则数据集设计器将无法自动生成用于使用 DB 直接模式插入、更新和删除数据库数据的方法。 相反，您必须手动创建它们，这与本教程前面的**InsertProduct**方法相同。 而且，如果要使用批更新模式，则必须手动提供**InsertCommand**、 **UpdateCommand**和**DeleteCommand**属性值。

## <a name="adding-the-remaining-tableadapters"></a>添加剩余的 Tableadapter

到现在为止，我们只介绍了如何使用单个数据库表的一个 TableAdapter。 但 Northwind 数据库包含多个相关表，我们需要在 web 应用程序中使用它们。 类型化数据集可以包含多个相关数据表。 因此，若要完成 DAL，需要为在这些教程中使用的其他表添加数据表。 若要将新的 TableAdapter 添加到类型化数据集，请打开数据集设计器，在设计器中右键单击，然后选择 "添加/TableAdapter"。 这将创建一个新的 DataTable 和 TableAdapter，并引导你完成本教程前面所述的向导。

使用以下查询创建以下 Tableadapter 和方法需要几分钟时间。 请注意， **ProductsTableAdapter**中的查询包含用于获取每个产品类别和供应商名称的子查询。 此外，如果已执行过后续工作，则已添加**ProductsTableAdapter**类的**GetProducts （）** 和**GetProductsByCategoryID （*类别 id*）** 方法。

- **ProductsTableAdapter**

  - **GetProducts**： 

      [!code-sql[Main](creating-a-data-access-layer-cs/samples/sample10.sql)]
  - **GetProductsByCategoryID**： 

      [!code-sql[Main](creating-a-data-access-layer-cs/samples/sample11.sql)]
  - **GetProductsBySupplierID**： 

      [!code-sql[Main](creating-a-data-access-layer-cs/samples/sample12.sql)]
  - **GetProductByProductID**： 

      [!code-sql[Main](creating-a-data-access-layer-cs/samples/sample13.sql)]
- **CategoriesTableAdapter**

  - **GetCategories**： 

      [!code-sql[Main](creating-a-data-access-layer-cs/samples/sample14.sql)]
  - **GetCategoryByCategoryID**： 

      [!code-sql[Main](creating-a-data-access-layer-cs/samples/sample15.sql)]
- **SuppliersTableAdapter**

  - **GetSuppliers**： 

      [!code-sql[Main](creating-a-data-access-layer-cs/samples/sample16.sql)]
  - **GetSuppliersByCountry**： 

      [!code-sql[Main](creating-a-data-access-layer-cs/samples/sample17.sql)]
  - **GetSupplierBySupplierID**： 

      [!code-sql[Main](creating-a-data-access-layer-cs/samples/sample18.sql)]
- **EmployeesTableAdapter**

  - **GetEmployees**： 

      [!code-sql[Main](creating-a-data-access-layer-cs/samples/sample19.sql)]
  - **GetEmployeesByManager**： 

      [!code-sql[Main](creating-a-data-access-layer-cs/samples/sample20.sql)]
  - **GetEmployeeByEmployeeID**： 

      [!code-sql[Main](creating-a-data-access-layer-cs/samples/sample21.sql)]

[添加四个 Tableadapter 后，在数据集设计器 ![](creating-a-data-access-layer-cs/_static/image84.png)](creating-a-data-access-layer-cs/_static/image83.png)

**图 31**：添加四个 tableadapter 后的数据集设计器（[单击以查看完全大小的图像](creating-a-data-access-layer-cs/_static/image85.png)）

## <a name="adding-custom-code-to-the-dal"></a>将自定义代码添加到 DAL

添加到类型化数据集的 Tableadapter 和数据表以 XML 架构定义文件（**Northwind**）表示。 您可以通过右键单击 "解决方案资源管理器中的**Northwind .xsd**文件，然后选择" 查看代码 "来查看此架构信息。

[![Northwinds 类型化数据集的 XML 架构定义（XSD）文件](creating-a-data-access-layer-cs/_static/image87.png)](creating-a-data-access-layer-cs/_static/image86.png)

**图 32**： Northwinds 类型化数据集的 XML 架构定义（XSD）文件（[单击以查看完全大小的图像](creating-a-data-access-layer-cs/_static/image88.png)）

此架构信息在编译时C#或运行时（如果需要）在设计时转换为或 Visual Basic 代码（如果需要），此时你可以使用调试器执行该操作。 若要查看自动生成的代码，请跳到类视图并向下钻取到 TableAdapter 或类型化数据集类。 如果在屏幕上看不到 "类视图"，请转到 "视图" 菜单并从中选择，或按 Ctrl + Shift + C。 类视图可以查看类型化数据集和 TableAdapter 类的属性、方法和事件。 若要查看特定方法的代码，请在类视图中双击方法名称，或右键单击该方法，然后选择 "转向定义"。

![通过从类视图中选择 "转向定义" 来检查自动生成的代码](creating-a-data-access-layer-cs/_static/image89.png)

**图 33**：通过从类视图中选择 "转向定义" 来检查自动生成的代码

尽管自动生成的代码可能是很好的时间保护程序，但代码通常非常通用，需要对其进行自定义以满足应用程序的独特需求。 不过，扩展自动生成的代码的风险在于，生成代码的工具可能决定是时间 "重新生成" 并覆盖您的自定义项。 使用 .NET 2.0 的新分部类概念，可以轻松地跨多个文件拆分一个类。 这使我们能够将自己的方法、属性和事件添加到自动生成的类，而无需担心 Visual Studio 覆盖我们的自定义。

若要演示如何自定义 DAL，请将**GetProducts （）** 方法添加到**SuppliersRow**类。 **SuppliersRow**类表示**供应商**表中的单个记录;每个供应商可以向多个产品提供零个，因此**GetProducts （）** 将返回指定供应商的那些产品。 若要完成此操作，请在**应用\_程序**中创建一个名为**SuppliersRow.cs**的新类文件，并添加以下代码：

[!code-csharp[Main](creating-a-data-access-layer-cs/samples/sample22.cs)]

此分部类指示编译器在生成**SuppliersRow**类时，包括我们刚才定义的**GetProducts （）** 方法。 如果生成项目，然后返回到类视图你将看到**GetProducts （）** 现在作为**SuppliersRow**的方法列出。

![GetProducts （）方法现在是 SuppliersRow 类的一部分](creating-a-data-access-layer-cs/_static/image90.png)

**图 34**： **GetProducts （）** 方法现在是**SuppliersRow**类的一部分

现在可以使用**GetProducts （）** 方法来枚举特定供应商的一组产品，如以下代码所示：

[!code-html[Main](creating-a-data-access-layer-cs/samples/sample23.html)]

此数据还可以显示在 ASP 的任何一个中。网络的数据 Web 控件。 以下页面使用包含两个字段的 GridView 控件：

- 显示每个供应商名称的 BoundField，
- 一个 TemplateField，其中包含一个 BulletedList 控件，该控件绑定到每个供应商的**GetProducts （）** 方法返回的结果。

我们将在以后的教程中检查如何显示此类主/详细信息报表。 现在，此示例旨在说明如何使用添加到**SuppliersRow**类的自定义方法。

SuppliersAndProducts .aspx

[!code-aspx[Main](creating-a-data-access-layer-cs/samples/sample24.aspx)]

SuppliersAndProducts.aspx.cs

[!code-csharp[Main](creating-a-data-access-layer-cs/samples/sample25.cs)]

[![供应商的公司名称列在左栏中，其产品显示在右侧](creating-a-data-access-layer-cs/_static/image92.png)](creating-a-data-access-layer-cs/_static/image91.png)

**图 35**：在左列中列出了供应商的公司名称，他们的产品显示在右侧（[单击以查看完全大小的图像](creating-a-data-access-layer-cs/_static/image93.png)）

## <a name="summary"></a>总结

构建 web 应用程序时，创建 DAL 的操作应该是您在开始创建表示层之前要执行的第一个步骤。 使用 Visual Studio 时，基于类型化数据集创建 DAL 是一项任务，可以在10-15 分钟内完成，而无需编写代码行。 后续教程将在此 DAL 上构建。 在[下一教程](creating-a-business-logic-layer-cs.md)中，我们将定义一些业务规则，并了解如何在单独的业务逻辑层中实现它们。

很高兴编程！

## <a name="further-reading"></a>其他阅读材料

有关本教程中讨论的主题的详细信息，请参阅以下资源：

- [使用 VS 2005 和 ASP.NET 2.0 中的强类型化 Tableadapter 和数据表构建 DAL](https://weblogs.asp.net/scottgu/435498)
- [设计数据层组件，并通过层传递数据](https://msdn.microsoft.com/library/ms978496.aspx)
- [使用 Visual Studio 2005 数据集设计器生成数据访问层](http://www.theserverside.net/articles/showarticle.tss?id=DataSetDesigner)
- [加密 ASP.NET 2.0 应用程序中的配置信息](http://aspnet.4guysfromrolla.com/articles/021506-1.aspx)
- [TableAdapter 概述](https://msdn.microsoft.com/library/bz9tthwx.aspx)
- [使用类型化数据集](https://msdn.microsoft.com/library/esbykkzb.aspx)
- [在 Visual Studio 2005 和 ASP.NET 2.0 中使用强类型化数据访问](http://aspnet.4guysfromrolla.com/articles/020806-1.aspx)
- [如何扩展 TableAdapter 方法](https://blogs.msdn.com/vbteam/archive/2005/05/04/ExtendingTableAdapters.aspx)
- [从存储过程中检索标量数据](http://aspnet.4guysfromrolla.com/articles/062905-1.aspx)

### <a name="video-training-on-topics-contained-in-this-tutorial"></a>本教程中包含的主题的视频培训

- [ASP.NET 应用程序中的数据访问层](../../../videos/data-access/adonet-data-services/data-access-layers-in-aspnet-applications.md)
- [如何手动将数据集绑定到 Datagrid](../../../videos/data-access/adonet-data-services/how-to-manually-bind-a-dataset-to-a-datagrid.md)
- [如何从 ASP 应用程序使用数据集和筛选器](../../../videos/data-access/adonet-data-services/how-to-work-with-datasets-and-filters-from-an-asp-application.md)

## <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，创始人的[4GuysFromRolla.com](http://www.4guysfromrolla.com)，已在使用 Microsoft Web 技术，自1998开始。 Scott 的工作方式是独立的顾问、培训师和撰稿人。 他的最新书籍是，[*在24小时内，sam ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 可以[mitchell@4GuysFromRolla.com访问。](mailto:mitchell@4GuysFromRolla.com) 或通过他的博客，可以在[http://ScottOnWriting.NET](http://ScottOnWriting.NET)找到。

## <a name="special-thanks-to"></a>特别感谢

此教程系列由许多有用的审阅者查看。 本教程的主管评审者是 Ron 绿、Hilton Giesenow、Dennis Patterson 将、Liz Shulok、Abel Gomez 和 Carlos Santos。 想要查看我即将发布的 MSDN 文章？ 如果是这样，请在mitchell@4GuysFromRolla.com放置一行[。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [下一页](creating-a-business-logic-layer-cs.md)
