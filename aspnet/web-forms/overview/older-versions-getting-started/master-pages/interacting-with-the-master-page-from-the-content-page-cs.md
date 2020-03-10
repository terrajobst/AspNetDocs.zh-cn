---
uid: web-forms/overview/older-versions-getting-started/master-pages/interacting-with-the-master-page-from-the-content-page-cs
title: 与内容页中的母版页交互（C#） |Microsoft Docs
author: rick-anderson
description: 检查如何从内容页中的代码调用母版页的方法、设置属性等。
ms.author: riande
ms.date: 07/11/2008
ms.assetid: 32d54638-71b2-491d-81f4-f7417a13a62f
msc.legacyurl: /web-forms/overview/older-versions-getting-started/master-pages/interacting-with-the-master-page-from-the-content-page-cs
msc.type: authoredcontent
ms.openlocfilehash: 5ef030d3bed117e98fdd090f7c63643354b47f76
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78456128"
---
# <a name="interacting-with-the-master-page-from-the-content-page-c"></a>从内容页与母版页交互 (C#)

作者： [Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载代码](https://download.microsoft.com/download/1/8/4/184e24fa-fcc8-47fa-ac99-4b6a52d41e97/ASPNET_MasterPages_Tutorial_06_CS.zip)或[下载 PDF](https://download.microsoft.com/download/e/b/4/eb4abb10-c416-4ba4-9899-32577715b1bd/ASPNET_MasterPages_Tutorial_06_CS.pdf)

> 检查如何从内容页中的代码调用母版页的方法、设置属性等。

## <a name="introduction"></a>简介

在过去的五个教程中，我们已经介绍了如何创建母版页、定义内容区域、将 ASP.NET 页面绑定到母版页，并定义特定于页面的内容。 当访问者请求特定内容页时，会在运行时将内容和母版页的标记融合在一起，从而呈现统一的控件层次结构。 因此，我们已了解到母版页和其中一个内容页可以交互的方式： "内容" 页将对要 transfuse 到母版页的 ContentPlaceHolder 控件中的标记进行了拼写。

我们尚未要检查的是母版页和内容页面如何以编程方式交互。 除了为母版页的 ContentPlaceHolder 控件定义标记外，内容页还可以为其母版页的公共属性赋值并调用其公共方法。 同样，母版页可能与其内容页交互。 尽管母版页和内容页面之间的编程交互不如其声明性标记之间的交互交互，但在很多情况下都需要此类编程交互。

在本教程中，我们将检查内容页如何以编程方式与母版页交互。在下一教程中，我们将探讨母版页如何与内容页交互。

## <a name="examples-of-programmatic-interaction-between-a-content-page-and-its-master-page"></a>内容页和其母版页之间的编程交互示例

需要逐页配置页面的特定区域时，我们使用的是 ContentPlaceHolder 的控件。 但大多数页需要发出特定输出的情况如何，但少量页面需要对其进行自定义以显示其他内容呢？ 在[*多个 contentplaceholder 和默认内容*](multiple-contentplaceholders-and-default-content-cs.md)教程中，我们在此示例中所述的一个示例涉及在每一页上显示一个登录接口。 虽然大多数页应包括一个登录接口，但对于少量页面（例如：主登录页（`Login.aspx`）），应将其取消。"创建帐户" 页;和其他只有经过身份验证的用户可以访问的页面。 [*多 contentplaceholder 和默认内容*](multiple-contentplaceholders-and-default-content-cs.md)教程介绍了如何在母版页中定义 ContentPlaceHolder 的默认内容，以及如何在不需要默认内容的那些页面中替代该内容。

另一种方法是在母版页内创建一个公共属性或方法，该属性或方法指示是显示还是隐藏登录接口。 例如，母版页可能包含一个名为 `ShowLoginUI` 的公共属性，其值用于设置母版页中登录控件的 `Visible` 属性。 此时应禁止显示登录用户界面的内容页，然后以编程方式将 `ShowLoginUI` 属性设置为 `false`。

如果在 "内容" 页中早于当前某些操作后需要刷新母版页中显示的数据，则可能会发生内容和母版页交互的最常见示例。 假设有一个包含 GridView 的母版页，其中显示了来自特定数据库表的五个最近添加的记录，并且其一个内容页包含用于向同一表中添加新记录的接口。

当用户访问页面以添加新记录时，她会看到在母版页中显示的五个最近添加的记录。 在填写新记录的列的值之后，她提交窗体。 假定母版页的 "`EnableViewState`" 属性设置为 "true" （默认值），则会将其内容从视图状态重新加载，因此即使刚将较新的记录添加到数据库中，也会显示五个相同的记录。 这可能会给用户造成混淆。

> [!NOTE]
> 即使您禁用了 GridView 的视图状态，以便它在每次回发时重新绑定到它的基础数据源，它仍不会显示刚刚添加的记录，因为数据在页生命周期中比将新记录添加到数据库时的数据绑定到ase.

为了纠正这种情况，以便在回发的母版页上显示刚刚添加的记录，我们需要指示 GridView 在新记录添加到数据库*后*重新绑定到其数据源。 这需要在内容页和母版页之间进行交互，因为用于添加新记录（及其事件处理程序）的接口位于内容页，但需要刷新的 GridView 在母版页中。

由于从内容页中的事件处理程序刷新母版页的显示是内容和母版页交互的最常见要求之一，接下来让我们更详细地探讨这一主题。 本教程的下载内容包括网站 `App_Data` 文件夹中名为 `NORTHWIND.MDF` Microsoft SQL Server 2005 Express Edition 数据库。 Northwind 数据库存储虚构公司、Northwind 商贸的产品、员工和销售信息。

步骤1指导完成在母版页的 GridView 中显示五个最近添加的产品。 步骤2创建一个用于添加新产品的内容页。 步骤3介绍了如何在母版页中创建公共属性和方法，步骤4说明了如何以编程方式通过内容页中的这些属性和方法进行界面。

> [!NOTE]
> 本教程不深入探讨如何使用 ASP.NET 中的数据。 用于设置母版页以显示数据的步骤和用于插入数据的内容页已完成，但 breezy。 有关显示和插入数据以及使用 SqlDataSource 和 GridView 控件的更深入说明，请参阅本教程末尾的后续读取部分中的资源。

## <a name="step-1-displaying-the-five-most-recently-added-products-in-the-master-page"></a>步骤1：在母版页中显示最近添加的五个产品

打开 `Site.master` 母版页，并向 `leftContent` `<div>`添加 "标签" 和 "GridView" 控件。 清除标签的 `Text` 属性，将其 `EnableViewState` 属性设置为 false，并将其 `ID` 属性设置为 `GridMessage`;将 GridView 的 `ID` 属性设置为 "`RecentProducts`"。 接下来，从设计器展开 GridView 的智能标记，然后选择将其绑定到新的数据源。 这将启动 "数据源配置向导"。 由于 `App_Data` 文件夹中的 Northwind 数据库是 Microsoft SQL Server 数据库，因此请选择通过选择创建 SqlDataSource （请参阅图1）;将 SqlDataSource 命名为 `RecentProductsDataSource`。

[![将 GridView 绑定到名为 RecentProductsDataSource 的 SqlDataSource 控件](interacting-with-the-master-page-from-the-content-page-cs/_static/image2.png)](interacting-with-the-master-page-from-the-content-page-cs/_static/image1.png)

**图 01**：将 GridView 绑定到名为 `RecentProductsDataSource` 的 SqlDataSource 控件（[单击查看完全大小的图像](interacting-with-the-master-page-from-the-content-page-cs/_static/image3.png)）

下一步将要求我们指定要连接到的数据库。 从下拉列表中选择 "`NORTHWIND.MDF` 数据库文件"，然后单击 "下一步"。 由于这是我们首次使用此数据库，因此向导将提供将连接字符串存储在 `Web.config`中。 让它使用名称 `NorthwindConnectionString`存储连接字符串。

[![连接到 Northwind 数据库](interacting-with-the-master-page-from-the-content-page-cs/_static/image5.png)](interacting-with-the-master-page-from-the-content-page-cs/_static/image4.png)

**图 02**：连接到 Northwind 数据库（[单击以查看完全大小的图像](interacting-with-the-master-page-from-the-content-page-cs/_static/image6.png)）

"配置数据源" 向导提供了两种方法，通过该向导可以指定用于检索数据的查询：

- 通过指定自定义 SQL 语句或存储过程，或
- 选择表或视图，然后指定要返回的列

由于我们只需要返回最近添加的五个产品，因此需要指定自定义 SQL 语句。 使用以下 SELECT 查询：

[!code-sql[Main](interacting-with-the-master-page-from-the-content-page-cs/samples/sample1.sql)]

`TOP 5` 关键字只返回查询的前5条记录。 `Products` 表的主键 `ProductID`为 `IDENTITY` 列，这可确保添加到表中的每个新产品都将具有比上一个条目更大的值。 因此，`ProductID` 按降序对结果进行排序时，将返回以最近创建的产品开头的产品。

[![返回最近添加的五个产品](interacting-with-the-master-page-from-the-content-page-cs/_static/image8.png)](interacting-with-the-master-page-from-the-content-page-cs/_static/image7.png)

**图 03**：返回最近添加的五个产品（[单击以查看完全大小的映像](interacting-with-the-master-page-from-the-content-page-cs/_static/image9.png)）

完成向导后，Visual Studio 将为 GridView 生成两个 BoundFields，以显示从数据库返回的 `ProductName` 和 `UnitPrice` 字段。 此时，母版页的声明性标记应包含如下标记：

[!code-aspx[Main](interacting-with-the-master-page-from-the-content-page-cs/samples/sample2.aspx)]

如您所见，标记包含：标签 Web 控件（`GridMessage`）;GridView `RecentProducts`，具有两个 BoundFields;和一个 SqlDataSource 控件，该控件返回最近添加的五个产品。

创建此 GridView 并配置其 SqlDataSource 控件后，通过浏览器访问网站。 如图4所示，将在左下角看到一个网格，其中列出了五个最近添加的产品。

[![GridView 显示最近添加的五个产品](interacting-with-the-master-page-from-the-content-page-cs/_static/image11.png)](interacting-with-the-master-page-from-the-content-page-cs/_static/image10.png)

**图 04**： GridView 显示最近添加的五个产品（[单击以查看完全大小的图像](interacting-with-the-master-page-from-the-content-page-cs/_static/image12.png)）

> [!NOTE]
> 随意清理 GridView 的外观。 某些建议包括将显示的 `UnitPrice` 值的格式设置为货币，并使用背景色和字体来改善网格的外观。

## <a name="step-2-creating-a-content-page-to-add-new-products"></a>步骤2：创建内容页以添加新产品

下一个任务是创建一个内容页，用户可以从中将新产品添加到 `Products` 表。 将新的 "内容" 页添加到名为 "`AddProduct.aspx``Admin` 文件夹中，并确保将其绑定到 `Site.master` 母版页。 图5显示了在此页面添加到网站后解决方案资源管理器。

[![将新的 ASP.NET 页面添加到管理文件夹](interacting-with-the-master-page-from-the-content-page-cs/_static/image14.png)](interacting-with-the-master-page-from-the-content-page-cs/_static/image13.png)

**图 05**：将新的 "ASP.NET" 页添加到 `Admin` 文件夹（[单击查看完全大小的图像](interacting-with-the-master-page-from-the-content-page-cs/_static/image15.png)）

请记住，在母版页教程的 "[*指定标题、Meta 标记和其他 HTML 标题*](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs.md)" 中，我们创建了一个名为 `BasePage` 的自定义基类类，如果未显式设置该页面的标题，则生成该页面的标题。 转到 "`AddProduct.aspx`" 页的代码隐藏类，并使其从 `BasePage` （而不是从 `System.Web.UI.Page`）派生。

最后，更新 `Web.sitemap` 文件以包含本课中的条目。 在控件 ID 命名问题课程的 `<siteMapNode>` 下面添加以下标记：

[!code-xml[Main](interacting-with-the-master-page-from-the-content-page-cs/samples/sample3.xml)]

如图6所示，此 `<siteMapNode>` 元素的添加在课程列表中反映出来。

返回 `AddProduct.aspx`。 在 `MainContent` ContentPlaceHolder 的内容控件中，添加 DetailsView 控件并将其命名为 `NewProduct`。 将 DetailsView 绑定到名为 `NewProductDataSource`的新 SqlDataSource 控件。 与步骤1中的 SqlDataSource 类似，将向导配置为使用 Northwind 数据库，并选择指定自定义 SQL 语句。 因为 DetailsView 将用于向数据库添加项，所以需要同时指定 `SELECT` 语句和 `INSERT` 语句。 使用以下 `SELECT` 查询：

[!code-sql[Main](interacting-with-the-master-page-from-the-content-page-cs/samples/sample4.sql)]

然后，在 "插入" 选项卡中添加以下 `INSERT` 语句：

[!code-sql[Main](interacting-with-the-master-page-from-the-content-page-cs/samples/sample5.sql)]

完成向导后，请跳到 DetailsView 的智能标记，并选中 "启用插入" 复选框。 这会将 CommandField 添加到 DetailsView，并将其 `ShowInsertButton` 属性设置为 true。 由于此 DetailsView 仅用于插入数据，因此请将 DetailsView 的 `DefaultMode` 属性设置为 `Insert`。

就这么简单！ 让我们测试此页。 通过浏览器访问 `AddProduct.aspx`，输入名称和价格（见图6）。

[![将新产品添加到数据库](interacting-with-the-master-page-from-the-content-page-cs/_static/image17.png)](interacting-with-the-master-page-from-the-content-page-cs/_static/image16.png)

**图 06**：向数据库添加新产品（[单击以查看完全大小的映像](interacting-with-the-master-page-from-the-content-page-cs/_static/image18.png)）

键入新产品的名称和价格后，单击 "插入" 按钮。 这将导致窗体回发。 在回发时，将执行 SqlDataSource 控件的 `INSERT` 语句;它的两个参数用用户输入的值填充到 DetailsView 的两个 TextBox 控件中。 遗憾的是，没有出现插入的视觉反馈。 最好显示一条消息，确认已添加新记录。 我将此留给读者的练习。 此外，在从 DetailsView 添加新记录后，母版页中的 GridView 仍显示与以前相同的五个记录;它不包含刚刚添加的记录。 我们将在后面的步骤中检查如何解决此情况。

> [!NOTE]
> 除了添加某种形式的视觉反馈以使插入成功，我还鼓励您同时更新 DetailsView 的插入界面以包括验证。 目前没有任何验证。 如果用户为 "`UnitPrice`" 字段输入无效的值（例如 "开销太高"），则当系统尝试将该字符串转换为十进制时，回发时将引发异常。 有关自定义插入界面的详细信息，请参阅使用[数据教程系列](../../data-access/index.md)中的[*自定义数据修改界面*教程](../../data-access/editing-inserting-and-deleting-data/customizing-the-data-modification-interface-cs.md)。

## <a name="step-3-creating-public-properties-and-methods-in-the-master-page"></a>步骤3：在母版页中创建公共属性和方法

在步骤1中，我们在母版页的 GridView 上方添加了名为 `GridMessage` 的标签 Web 控件。 此标签用于选择性地显示消息。 例如，将新记录添加到 `Products` 表后，我们可能希望显示一条消息，其中包含： "*ProductName*已添加到数据库中"。 我们可能想要通过内容页自定义该消息，而不是在母版页中对此标签文本进行硬编码。

由于标签控件作为母版页内的受保护成员变量实现，因此无法直接从内容页访问它。 若要在内容页中处理母版页中的标签（或者在此情况下，在母版页中的任何 Web 控件），我们需要在公开 Web 控件或用作代理的母版页中创建一个公共属性，该属性可以是 存取. 将以下语法添加到母版页的代码隐藏类中，以公开标签的 `Text` 属性：

[!code-csharp[Main](interacting-with-the-master-page-from-the-content-page-cs/samples/sample6.cs)]

将新记录从内容页添加到 `Products` 表时，母版页中的 `RecentProducts` GridView 需要重新绑定到其基础数据源。 若要重新绑定 GridView，请调用其 `DataBind` 方法。 由于不能通过编程方式访问母版页中的 GridView，因此需要在母版页中创建一个公共方法，该方法在被调用时将数据重新绑定到 GridView。 将以下方法添加到母版页的代码隐藏类：

[!code-csharp[Main](interacting-with-the-master-page-from-the-content-page-cs/samples/sample7.cs)]

利用 `GridMessageText` 属性和 `RefreshRecentProductsGrid` 方法，任何内容页都可以以编程方式设置或读取 `GridMessage` 标签 `Text` 属性的值，或将数据重新绑定到 `RecentProducts` GridView。 步骤4检查如何从内容页访问母版页的公共属性和方法。

> [!NOTE]
> 不要忘记将母版页的属性和方法标记为 `public`。 如果未将这些属性和方法显式表示为 `public`，将无法从 "内容" 页访问这些属性和方法。

## <a name="step-4-calling-the-master-pages-public-members-from-a-content-page"></a>步骤4：从内容页调用母版页的公共成员

现在，母版页具有必要的公共属性和方法，接下来可以从 `AddProduct.aspx` 的内容页调用这些属性和方法。 具体而言，我们需要设置母版页的 `GridMessageText` 属性，并在将新产品添加到数据库后调用其 `RefreshRecentProductsGrid` 方法。 所有 ASP.NET 数据 Web 控件都在完成各种任务之前和之后引发事件，使页面开发人员可以轻松地在任务之前或之后执行某些编程操作。 例如，当最终用户单击 DetailsView 的 "插入" 按钮时，在回发之前，DetailsView 会引发其 `ItemInserting` 事件，然后再开始插入工作流。 然后，将记录插入到数据库中。 之后，DetailsView 会引发其 `ItemInserted` 事件。 因此，为了在添加新产品后使用母版页，请为 DetailsView 的 `ItemInserted` 事件创建事件处理程序。

内容页可以通过两种方式以编程方式与母版页交互：

- 使用 `Page.Master` 属性，该属性将返回对母版页的松散类型引用，或
- 通过 `@MasterType` 指令指定页的母版页类型或文件路径;这会自动将强类型属性添加到名为 `Master`的页面。

我们来看一下这两种方法。

### <a name="using-the-loosely-typedpagemasterproperty"></a>使用松散类型的`Page.Master`属性

所有 ASP.NET 网页必须派生自 `System.Web.UI` 命名空间中的 `Page` 类。 `Page` 类包含一个[`Master` 属性](https://msdn.microsoft.com/library/system.web.ui.page.master.aspx)，该属性返回对页的母版页的引用。 如果页面没有 `Master` 返回 `null`的母版页。

`Master` 属性返回[`MasterPage`](https://msdn.microsoft.com/library/system.web.ui.masterpage.aspx)类型的对象（也位于 `System.Web.UI` 命名空间），该对象是所有母版页从中派生的基类型。 因此，若要使用网站母版页中定义的公共属性或方法，必须将从 `Master` 属性返回的 `MasterPage` 对象转换为相应的类型。 由于我们将母版页文件命名 `Site.master`，因此代码隐藏类名为 `Site`。 因此，以下代码将 `Page.Master` 属性强制转换为 Site 类的实例。

[!code-csharp[Main](interacting-with-the-master-page-from-the-content-page-cs/samples/sample8.cs)]

现在，我们已将松散类型 `Page.Master` 属性强制转换到 `Site` 类型，接下来我们可以引用特定于站点的属性和方法。 如图7所示，公共属性 `GridMessageText` 会出现在 IntelliSense 下拉。

[![IntelliSense 显示母版页的公共属性和方法](interacting-with-the-master-page-from-the-content-page-cs/_static/image20.png)](interacting-with-the-master-page-from-the-content-page-cs/_static/image19.png)

**图 07**： IntelliSense 显示母版页的公共属性和方法（[单击以查看完全大小的图像](interacting-with-the-master-page-from-the-content-page-cs/_static/image21.png)）

> [!NOTE]
> 如果已将母版页文件命名 `MasterPage.master` 则母版页的代码隐藏类名称将 `MasterPage`。 从类型 `System.Web.UI.MasterPage` 转换到 `MasterPage` 类时，这可能导致不明确的代码。 简而言之，你需要完全限定要强制转换到的类型，这在使用网站项目模型时可能有点棘手。 我的建议是确保在创建母版页时将其命名为除 `MasterPage.master` 或更好的方式，即创建对母版页的强类型引用。

### <a name="creating-a-strongly-typed-reference-with-themastertypedirective"></a>使用`@MasterType`指令创建强类型引用

仔细查看时，可以看到 ASP.NET 页面的代码隐藏类是分部类（请注意类定义中的 `partial` 关键字）。 分部类在C#和 Visual Basic with.NET Framework 2.0 中引入，并且简言之，允许跨多个文件定义类的成员。 例如，代码隐藏类文件 `AddProduct.aspx.cs`，其中包含开发人员创建的代码。 除了我们的代码，ASP.NET 引擎还会自动创建一个单独的类文件，其中包含中的属性和事件处理程序，将声明性标记转换为该页的类层次结构。

只要访问 ASP.NET 页面，就会自动生成代码，铺平了道路为一些更有趣的有用方法。 对于母版页，如果我们告诉 ASP.NET 引擎我们的内容页面正在使用哪个母版页，它会为我们生成强类型的 `Master` 属性。

使用[`@MasterType` 指令](https://msdn.microsoft.com/library/ms228274.aspx)通知 ASP.NET 引擎内容页的母版页类型。 `@MasterType` 指令可以接受母版页的类型名称或其文件路径。 若要指定 `AddProduct.aspx` 页使用 `Site.master` 作为其母版页，请将以下指令添加到 `AddProduct.aspx`的顶部：

[!code-aspx[Main](interacting-with-the-master-page-from-the-content-page-cs/samples/sample9.aspx)]

此指令指示 ASP.NET 引擎通过名为 `Master`的属性向母版页添加强类型引用。 使用 `@MasterType` 指令后，可以直接通过 `Master` 属性调用 `Site.master` 母版页的公共属性和方法，无需进行任何强制转换。

> [!NOTE]
> 如果省略 `@MasterType` 指令，则语法 `Page.Master` 和 `Master` 返回相同的内容：到页面的母版页的松散类型的对象。 如果包括 `@MasterType` 指令，则 `Master` 返回对指定母版页的强类型引用。 但 `Page.Master`仍返回松类型引用。 若要更全面地了解这种情况的原因，以及如何在包含 `@MasterType` 指令时构造 `Master` 属性，请参阅[ASP.NET 2.0 中](http://odetocode.com/Blogs/scott/archive/2005/07/16/1944.aspx)的[Allen](http://odetocode.com/blogs/scott/default.aspx)的博客文章`@MasterType`。

### <a name="updating-the-master-page-after-adding-a-new-product"></a>添加新产品后更新母版页

现在，我们知道如何从内容页中调用母版页的公共属性和方法，接下来可以更新 `AddProduct.aspx` 页面，使母版页在添加新产品后进行刷新。 在步骤4开始时，我们为 DetailsView 控件的 `ItemInserting` 事件创建了一个事件处理程序，该事件将在新产品添加到数据库之后立即执行。 将以下代码添加到该事件处理程序：

[!code-csharp[Main](interacting-with-the-master-page-from-the-content-page-cs/samples/sample10.cs)]

上面的代码使用松散类型的 `Page.Master` 属性和强类型的 `Master` 属性。 请注意，`GridMessageText` 属性设置为 "已添加到网格的*ProductName* ..."可以通过 `e.Values` 集合访问刚刚添加的产品值;正如您所看到的，只需通过 `e.Values["ProductName"]`访问刚添加的 `ProductName` 值即可。

图8显示了一个新产品 Soda （已添加到数据库）后立即出现 `AddProduct.aspx` 页面。 请注意，在母版页的标签中将注明刚刚添加的产品名称，并且 GridView 已刷新为包含产品及其价格。

[![母版页的标签和 GridView 显示刚刚添加的产品](interacting-with-the-master-page-from-the-content-page-cs/_static/image23.png)](interacting-with-the-master-page-from-the-content-page-cs/_static/image22.png)

**图 08**：母版页的标签和 GridView 显示刚刚添加的产品（[单击查看完全尺寸的图像](interacting-with-the-master-page-from-the-content-page-cs/_static/image24.png)）

## <a name="summary"></a>摘要

理想情况下，母版页及其内容页完全独立，无需交互。 尽管母版页和内容页面的设计目的应考虑到这一点，但在某些常见情况下，内容页必须与其母版页交互。 最常见的原因之一是，基于在内容页中早于当前的某个操作更新母版页显示的特定部分。

好消息是，使内容页以编程方式与母版页交互是相对简单的。 首先在母版页中创建公共属性或方法，该母版页封装了内容页需要调用的功能。 然后，在 "内容" 页中，通过松散类型的 `Page.Master` 属性访问母版页的属性和方法，或使用 `@MasterType` 指令创建对母版页的强类型引用。

在下一教程中，我们将检查如何使母版页以编程方式与其中一个内容页交互。

很高兴编程！

### <a name="further-reading"></a>其他阅读材料

有关本教程中讨论的主题的详细信息，请参阅以下资源：

- [访问和更新 ASP.NET 中的数据](http://aspnet.4guysfromrolla.com/articles/011106-1.aspx)
- [ASP.NET 母版页：提示、技巧和陷阱](http://www.odetocode.com/articles/450.aspx)
- [ASP.NET 2.0 中的 `@MasterType`](http://odetocode.com/Blogs/scott/archive/2005/07/16/1944.aspx)
- [在内容和母版页之间传递信息](http://aspnet.4guysfromrolla.com/articles/013107-1.aspx)
- [使用 ASP.NET 教程中的数据](../../data-access/index.md)

### <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，创始人的多个 ASP/asp 和4GuysFromRolla.com 的作者已使用 Microsoft Web 技术，1998。 Scott 的工作方式是独立的顾问、培训师和撰稿人。 他的最新书籍是，[*在24小时内，sam ASP.NET 3.5*](https://www.amazon.com/exec/obidos/ASIN/0672329972/4guysfromrollaco)。 可以通过[http://ScottOnWriting.NET](http://scottonwriting.net/) [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)或通过他的博客访问 Scott。

### <a name="special-thanks-to"></a>特别感谢

此教程系列由许多有用的审阅者查看。 本教程的领导审查人员是 Zack 的。 想要查看我即将发布的 MSDN 文章？ 如果是这样，请在[mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一页](control-id-naming-in-content-pages-cs.md)
> [下一页](interacting-with-the-content-page-from-the-master-page-cs.md)
