---
uid: web-forms/overview/older-versions-getting-started/continuing-with-ef/what-s-new-in-the-entity-framework-4
title: 实体框架4.0 中的新增功能 |Microsoft Docs
author: tdykstra
description: 本教程系列在使用实体框架4.0 教程系列的入门创建的 Contoso 大学 web 应用程序上构建。 I...
ms.author: riande
ms.date: 01/26/2011
ms.assetid: 393df4a8-b1db-44c4-9db7-2b533ca887d0
msc.legacyurl: /web-forms/overview/older-versions-getting-started/continuing-with-ef/what-s-new-in-the-entity-framework-4
msc.type: authoredcontent
ms.openlocfilehash: 29d2bd61e8361b130e7b9415dad4fe1d5b847945
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78522146"
---
# <a name="whats-new-in-the-entity-framework-40"></a>Entity Framework 4.0 的新增功能

作者： [Tom Dykstra](https://github.com/tdykstra)

> 本教程系列在[使用实体框架](../getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-1.md)教程系列的入门创建的 Contoso 大学 web 应用程序上构建。 如果你没有完成前面的教程，作为本教程的起点，你可以下载你要创建[的应用程序](https://code.msdn.microsoft.com/ASPNET-Web-Forms-97f8ee9a)。 你还可以下载完整的系列教程创建的[应用程序](https://code.msdn.microsoft.com/ASPNET-Web-Forms-6c7197aa)。 如果有关于这些教程的问题，可以将其发布到[ASP.NET 实体框架论坛](https://forums.asp.net/1227.aspx)。

在上一教程中，你看到了一些方法，用于最大程度地提高使用实体框架的 web 应用程序的性能。 本教程回顾实体框架版本4中的一些最重要的新功能，并链接到可提供更完整的所有新功能的资源。 本教程中突出显示的功能包括：

- 外键关联。
- 正在执行用户定义的 SQL 命令。
- 模型优先开发。
- POCO 支持。

此外，本教程将简要介绍*代码优先开发*，这是下一版本的实体框架的一项功能。

若要开始学习本教程，请启动 Visual Studio，并打开在上一教程中使用的 Contoso 大学 web 应用程序。

## <a name="foreign-key-associations"></a>外键关联

实体框架的3.5 版包含导航属性，但它不包括数据模型中的外键属性。 例如，`StudentGrade` 实体中将省略 `StudentGrade` 表的 `CourseID` 和 `StudentID` 列。

[![Image01](what-s-new-in-the-entity-framework-4/_static/image2.png)](what-s-new-in-the-entity-framework-4/_static/image1.png)

此方法的原因在于，严格地说，外键是物理实现细节，不属于概念数据模型。 但实际上，当你具有对外键的直接访问权限时，通常可以更轻松地在代码中处理实体。

有关如何使用数据模型中的外键来简化代码的示例，请考虑在没有这些外键的情况下，你必须如何编码*DepartmentsAdd*页。 在 `Department` 实体中，`Administrator` 属性是与 `Person` 实体中 `PersonID` 对应的外键。 若要在新的部门及其管理员之间建立关联，只需要在数据绑定控件的 `ItemInserting` 事件处理程序中设置 "`Administrator`" 属性的值：

[!code-csharp[Main](what-s-new-in-the-entity-framework-4/samples/sample1.cs)]

如果数据模型中没有外键，则需要处理数据源控件的 `Inserting` 事件，而不是数据绑定控件的 `ItemInserting` 事件，以便在将实体添加到实体集之前获取对实体本身的引用。 使用该引用时，可以使用类似于以下示例的代码建立关联：

[!code-csharp[Main](what-s-new-in-the-entity-framework-4/samples/sample2.cs)]

[!code-csharp[Main](what-s-new-in-the-entity-framework-4/samples/sample3.cs)]

正如你在实体框架团队的[有关外键关联的博客文章](https://blogs.msdn.com/b/efdesign/archive/2009/03/16/foreign-keys-in-the-entity-framework.aspx)中所看到的，在其他情况下，代码复杂性的差异要大得多。 为了满足更简单代码的概念数据模型中更喜欢使用实现细节的用户的需求，实体框架现在提供了在数据模型中包括外键的选项。

在实体框架术语中，如果你在使用*外键关联*的数据模型中包含外键，并且你排除使用*独立关联*的外键，则为。

## <a name="executing-user-defined-sql-commands"></a>执行用户定义的 SQL 命令

在实体框架的早期版本中，不能轻松地创建自己的 SQL 命令并运行这些命令。 实体框架为您动态生成 SQL 命令，或者您必须创建一个存储过程并将其作为函数导入。 版本4添加了 `ObjectContext` 类 `ExecuteStoreQuery` 和 `ExecuteStoreCommand` 方法，使您可以更轻松地将任何查询直接传递到数据库。

假设 Contoso 大学管理员希望能够在数据库中执行大容量更改，而不必完成创建存储过程并将其导入到数据模型中的过程。 它们的第一个请求是针对页面，使其可以更改数据库中所有课程的信用额度。 在网页上，他们希望能够输入一个数字，用来将每个 `Course` 行 `Credits` 列的值相乘。

创建一个使用*网站母版页*的新页面，并将其命名为*UpdateCredits*。 然后，将以下标记添加到名为 `Content2`的 `Content` 控件：

[!code-aspx[Main](what-s-new-in-the-entity-framework-4/samples/sample4.aspx)]

此标记创建一个 `TextBox` 控件，用户可在其中输入乘数值、要单击以执行命令的 `Button` 控件，以及指示受影响的行数的 `Label` 控件。

打开*UpdateCredits.aspx.cs*，并为按钮的 `Click` 事件添加以下 `using` 语句和处理程序：

[!code-csharp[Main](what-s-new-in-the-entity-framework-4/samples/sample5.cs)]

[!code-csharp[Main](what-s-new-in-the-entity-framework-4/samples/sample6.cs)]

此代码使用文本框中的值执行 SQL `Update` 命令，并使用标签显示受影响的行数。 在运行页面之前，请运行 "*课程 .aspx* " 页，获取一些数据的 "之前" 图片。

[![Image02](what-s-new-in-the-entity-framework-4/_static/image4.png)](what-s-new-in-the-entity-framework-4/_static/image3.png)

运行*UpdateCredits*，输入 "10" 作为乘数，然后单击 "**执行**"。

[![Image03](what-s-new-in-the-entity-framework-4/_static/image6.png)](what-s-new-in-the-entity-framework-4/_static/image5.png)

再次运行 "*课程 .aspx* " 页以查看更改后的数据。

[![Image04](what-s-new-in-the-entity-framework-4/_static/image8.png)](what-s-new-in-the-entity-framework-4/_static/image7.png)

（如果要将富余点数设置回其原始值，请在 " *UpdateCredits.aspx.cs*更改 `Credits * {0}`" 中 `Credits / {0}` 并重新运行该页面，输入10作为除数。）

有关执行在代码中定义的查询的详细信息，请参阅[如何：直接对数据源执行命令](https://msdn.microsoft.com/library/ee358769.aspx)。

## <a name="model-first-development"></a>模型优先开发

在这些演练中，首先创建了数据库，然后根据数据库结构生成了数据模型。 在实体框架4中，可以改为从数据模型开始，并基于数据模型结构生成数据库。 如果创建的应用程序数据库尚不存在，则使用模型优先方法可以创建在概念上适用于该应用程序的实体和关系，而无需担心物理实现细节. （不过，这一点仅通过开发的初始阶段才适用。 最终会创建数据库，并在其中包含生产数据，并从模型重新创建该数据库将不再可行;此时，您将返回到数据库优先的方法。）

在本教程的此部分中，你将创建一个简单的数据模型，并从该模型生成数据库。

在**解决方案资源管理器**中，右键单击*DAL*文件夹，然后选择 "**添加新项**"。 在 "**添加新项**" 对话框中，在 "**已安装的模板**" 下选择 "**数据**"，然后选择 " **ADO.NET 实体数据模型**" 模板。 将新文件命名为*AlumniAssociationModel* ，然后单击 "**添加**"。

[![Image06](what-s-new-in-the-entity-framework-4/_static/image10.png)](what-s-new-in-the-entity-framework-4/_static/image9.png)

这将启动实体数据模型向导。 在 "**选择模型内容**" 步骤中，选择 "**空模型**"，然后单击 "**完成**"。

[![Image07](what-s-new-in-the-entity-framework-4/_static/image12.png)](what-s-new-in-the-entity-framework-4/_static/image11.png)

此时将打开**实体数据模型设计器**，其中显示一个空白设计图面。 将一个**实体**项从**工具箱**拖到设计图面上。

[![Image08](what-s-new-in-the-entity-framework-4/_static/image14.png)](what-s-new-in-the-entity-framework-4/_static/image13.png)

将实体名称从 `Entity1` 更改为 `Alumnus`，将 `Id` 属性名称更改为 `AlumnusId`，并添加名为 `Name`的新标量属性。 若要添加新属性，可在更改 `Id` 列的名称后按 Enter，或右键单击该实体并选择 "**添加标量属性**"。 新属性的默认类型为 `String`，这对于这一简单的演示非常不错，但您也可以在 "**属性**" 窗口中更改数据类型等。

以相同的方式创建另一个实体，并将其命名 `Donation`。 将 `Id` 属性更改为 `DonationId` 并添加一个名为 `DateAndAmount`的标量属性。

[![Image09](what-s-new-in-the-entity-framework-4/_static/image16.png)](what-s-new-in-the-entity-framework-4/_static/image15.png)

若要添加这两个实体之间的关联，请右键单击 `Alumnus` 实体，选择 "**添加**"，然后选择 "**关联**"。

[![Image10](what-s-new-in-the-entity-framework-4/_static/image18.png)](what-s-new-in-the-entity-framework-4/_static/image17.png)

"**添加关联**" 对话框中的默认值是你想要的内容（一对多，包括导航属性，包括外键），因此只需单击 **"确定"** 。

[![Image11](what-s-new-in-the-entity-framework-4/_static/image20.png)](what-s-new-in-the-entity-framework-4/_static/image19.png)

设计器添加关联连线和外键属性。

[![Image12](what-s-new-in-the-entity-framework-4/_static/image22.png)](what-s-new-in-the-entity-framework-4/_static/image21.png)

现在，可以创建数据库了。 右键单击设计图面，然后选择 "**从模型生成数据库**"。

[![Image13](what-s-new-in-the-entity-framework-4/_static/image24.png)](what-s-new-in-the-entity-framework-4/_static/image23.png)

这将启动 "生成数据库向导"。 （如果您看到指示实体未映射的警告，则可以忽略这些实体。）

在 "**选择你的数据连接**" 步骤中，单击 "**新建连接**"。

[![Image14](what-s-new-in-the-entity-framework-4/_static/image26.png)](what-s-new-in-the-entity-framework-4/_static/image25.png)

在 "**连接属性**" 对话框中，选择本地 SQL Server Express 实例，并将数据库命名为 `AlumniAssociation`。

[![Image15](what-s-new-in-the-entity-framework-4/_static/image28.png)](what-s-new-in-the-entity-framework-4/_static/image27.png)

当系统询问您是否要创建数据库时，请单击 **"是"** 。 再次显示 "**选择数据连接**" 步骤时，单击 "**下一**步"。

在 "**摘要和设置**" 步骤中，单击 "**完成**"。

[![Image18](what-s-new-in-the-entity-framework-4/_static/image30.png)](what-s-new-in-the-entity-framework-4/_static/image29.png)

已创建包含数据定义语言（DDL）命令的 *.sql*文件，但尚未运行这些命令。

[![Image20](what-s-new-in-the-entity-framework-4/_static/image32.png)](what-s-new-in-the-entity-framework-4/_static/image31.png)

使用诸如**SQL Server Management Studio**之类的工具运行脚本和创建表，就像你在为[入门教程系列中的第一个教程](../getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-1.md)创建 `School` 数据库时所做的那样。 （除非已下载数据库。）

现在，你可以在网页中使用 `AlumniAssociation` 数据模型，就像使用 `School` 模型一样。 为此，请将一些数据添加到表中，并创建一个显示数据的网页。

使用**服务器资源管理器**将以下行添加到 `Alumnus` 并 `Donation` 表中。

[![Image21](what-s-new-in-the-entity-framework-4/_static/image34.png)](what-s-new-in-the-entity-framework-4/_static/image33.png)

创建一个使用校友*母版页的*名为的新网页。 将以下标记添加到名为 `Content2`的 `Content` 控件：

[!code-aspx[Main](what-s-new-in-the-entity-framework-4/samples/sample7.aspx)]

此标记创建嵌套 `GridView` 控件，外部控件用于显示校友的名称和内部控件，以显示捐赠日期和金额。

打开*Alumni.aspx.cs*。 添加数据访问层的 `using` 语句，并为外部 `GridView` 控件的 `RowDataBound` 事件添加处理程序：

[!code-csharp[Main](what-s-new-in-the-entity-framework-4/samples/sample8.cs)]

此代码使用当前行的 `Alumnus` 实体的 `Donations` 导航属性 databinds 内部 `GridView` 控件。

运行页面。

[![Image22](what-s-new-in-the-entity-framework-4/_static/image36.png)](what-s-new-in-the-entity-framework-4/_static/image35.png)

（注意：可下载的项目中包含此页，但要使其正常工作，必须在本地 SQL Server Express 实例中创建数据库; 该数据库不作为*应用\_数据*文件夹中的 *.mdf*文件包含。）

有关使用实体框架的模型优先功能的详细信息，请参阅[实体框架4中的 "模型优先](https://msdn.microsoft.com/data/ff830362.aspx)"。

## <a name="poco-support"></a>POCO 支持

使用域驱动的设计方法时，可以设计数据类，这些类表示与业务域相关的数据和行为。 这些类应独立于用于存储（持久）数据的任何特定技术;换言之，它们应该是*持久性未知*的。 持久性无感知还可以使类更易于进行单元测试，因为单元测试项目可以使用最方便测试的任何持久性技术。 早期版本的实体框架提供对持久性无感知的有限支持，因为实体类必须继承自 `EntityObject` 类，因此包含大量实体框架特定的功能。

实体框架4引入了使用不从 `EntityObject` 类继承的实体类，因而是持久性未知的功能。 在实体框架的上下文中，通常会将类似于这样的类称为 "*纯旧 CLR 对象*（POCO 或 poco）"。 您可以手动编写 POCO 类，也可以使用实体框架提供的文本模板转换工具包（T4）模板基于现有数据模型自动生成它们。

有关在实体框架中使用 Poco 的详细信息，请参阅以下资源：

- 使用[POCO 实体](https://msdn.microsoft.com/library/dd456853.aspx)。 这是一个 MSDN 文档，其中概述了 Poco，并提供了指向更详细信息的其他文档的链接。
- [演练：用于实体框架的 POCO 模板](https://blogs.msdn.com/b/adonet/archive/2010/01/25/walkthrough-poco-template-for-the-entity-framework.aspx)这是来自实体框架开发团队的博客文章，其中提供了有关 Poco 的其他博客文章的链接。

## <a name="code-first-development"></a>代码优先开发

实体框架4中的 POCO 支持仍要求您创建一个数据模型，并将实体类链接到数据模型。 下一版本的实体框架将包括一项名为*代码优先开发*的功能。 此功能使你能够将实体框架用于自己的 POCO 类，而无需使用数据模型设计器或数据模型 XML 文件。 （因此，此选项也被称为*仅限代码*;*代码优先*和*仅代码*都引用相同的实体框架功能。）

有关使用代码优先方法进行开发的详细信息，请参阅以下资源：

- [代码优先开发与实体框架 4](https://weblogs.asp.net/scottgu/archive/2010/07/16/code-first-development-with-entity-framework-4.aspx)。 这是 Scott Guthrie 的博客文章，其中介绍了代码优先开发。
- [实体框架开发团队博客-标记为 CodeOnly 的文章](https://blogs.msdn.com/b/efdesign/archive/tags/codeonly/)
- [实体框架开发团队博客-已标记的文章 Code First](https://blogs.msdn.com/b/efdesign/archive/tags/code+first/)
- [MVC 音乐应用商店教程-第4部分：模型和数据访问](../../../../mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-4.md)
- [入门 MVC 3-第4部分：实体框架代码优先开发](../../../../mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/adding-a-model.md)

此外，还会在[https://asp.net/entity-framework/tutorials](../../../../entity-framework.md) 2011 的弹簧中发布一个新的 MVC 代码优先教程，该教程与 Contoso 大学应用程序类似

## <a name="more-information"></a>详细信息

这将完成实体框架中的新增功能的概述，这将继续学习实体框架教程系列。 有关此处未涵盖的实体框架4中的新功能的详细信息，请参阅以下资源：

- [ADO.NET 中的新增功能](https://msdn.microsoft.com/library/ex6y04yf.aspx)MSDN 主题，介绍实体框架版本4中的新增功能。
- [宣布发布实体框架 4](https://blogs.msdn.com/b/efdesign/archive/2010/04/12/announcing-the-release-of-entity-framework-4.aspx)实体框架开发团队的博客文章版本4中的新功能。

> [!div class="step-by-step"]
> [上一页](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application.md)
