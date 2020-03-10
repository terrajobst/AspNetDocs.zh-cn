---
uid: web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-2
title: 入门实体框架 4.0 Database First 和 ASP.NET 4 Web 窗体-第2部分 |Microsoft Docs
author: tdykstra
description: Contoso 大学示例 web 应用程序演示了如何使用实体框架创建 ASP.NET Web 窗体应用程序。 示例应用程序为 。
ms.author: riande
ms.date: 12/03/2010
ms.assetid: fb63a326-a4ae-4b0c-a4f5-412327197216
msc.legacyurl: /web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-2
msc.type: authoredcontent
ms.openlocfilehash: bd6a2e29e6f0df04e39be29160e2e08cc99c4706
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78456446"
---
# <a name="getting-started-with-entity-framework-40-database-first-and-aspnet-4-web-forms---part-2"></a>入门实体框架 4.0 Database First 和 ASP.NET 4 Web 窗体-第2部分

作者： [Tom Dykstra](https://github.com/tdykstra)

> Contoso 大学示例 web 应用程序演示了如何使用实体框架4.0 和 Visual Studio 2010 创建 ASP.NET Web 窗体应用程序。 有关本教程系列的信息，请参阅[系列教程中的第一个教程](the-entity-framework-and-aspnet-getting-started-part-1.md)

## <a name="the-entitydatasource-control"></a>EntityDataSource 控件

在上一教程中，您创建了一个网站、一个数据库和一个数据模型。 在本教程中，您将使用 ASP.NET 提供的 `EntityDataSource` 控件以便于处理实体框架的数据模型。 您将创建一个 `GridView` 控件用于显示和编辑学生数据、用于添加新学生的 `DetailsView` 控件，以及用于选择部门的 `DropDownList` 控件（稍后将用于显示相关的课程）。

[![Image20](the-entity-framework-and-aspnet-getting-started-part-2/_static/image2.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image1.png)

[![Image09](the-entity-framework-and-aspnet-getting-started-part-2/_static/image4.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image3.png)

[![Image18](the-entity-framework-and-aspnet-getting-started-part-2/_static/image6.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image5.png)

请注意，在此应用程序中，不会向更新数据库的页面添加输入验证，并且某些错误处理将不会像生产应用程序中所需的那样可靠。 这使教程重点介绍实体框架并使其不会太长。 有关如何向应用程序添加这些功能的详细信息，请参阅在[ASP.NET 页和应用程序](https://msdn.microsoft.com/library/w16865z6.aspx)中验证 ASP.NET 网页和错误处理中的[用户输入](https://msdn.microsoft.com/library/7kh55542.aspx)。

## <a name="adding-and-configuring-the-entitydatasource-control"></a>添加和配置 EntityDataSource 控件

首先，将 `EntityDataSource` 控件配置为读取 `People` 实体集中的 `Person` 实体。

请确保已打开 Visual Studio，并且使用的是在第1部分中创建的项目。 如果你在创建数据模型后，或自上次更改后生成了项目，请立即生成项目。 在生成项目之前，不能对数据模型进行更改。

使用 "母版页" 模板创建一个使用**Web 窗体**的新网页，*并将其*命名为 "student"。

[![Image23](the-entity-framework-and-aspnet-getting-started-part-2/_static/image8.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image7.png)

指定*网站地图*作为母版页。 你为这些教程创建的所有页面都将使用此母版页。

[![Image24](the-entity-framework-and-aspnet-getting-started-part-2/_static/image10.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image9.png)

在 "**源**" 视图中，将 `h2` 标题添加到名为 `Content2`的 `Content` 控件，如以下示例中所示：

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-2/samples/sample1.aspx)]

从 "工具箱" 的 "**数据**" 选项卡中，将 **"** `EntityDataSource`" 控件拖动到页面上，将其放在标题下方，将 ID 更改为 `StudentsEntityDataSource`：

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-2/samples/sample2.aspx)]

切换到 "**设计**" 视图，单击数据源控件的智能标记，然后单击 "**配置数据源**" 以启动 "**配置数据源**" 向导。

[![Image01](the-entity-framework-and-aspnet-getting-started-part-2/_static/image12.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image11.png)

在 "**配置 ObjectContext**向导" 步骤中，选择 " **SchoolEntities** " 作为 "**命名连接**" 的值，并选择 " **SchoolEntities** " 作为 " **DefaultContainerName** " 值。 再单击 **“下一步”** 。

[![Image02](the-entity-framework-and-aspnet-getting-started-part-2/_static/image14.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image13.png)

注意：如果此时获取以下对话框，则必须先生成项目，然后才能继续。

[![Image25](the-entity-framework-and-aspnet-getting-started-part-2/_static/image16.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image15.png)

在 "**配置数据选择**" 步骤中，选择 "**用户**" 作为**EntitySetName**的值。 在 "**选择**" 下，确保选中 "**选择**ll" 复选框。 然后选择用于启用更新和删除的选项。 完成后，单击 "**完成**"。

[![Image03](the-entity-framework-and-aspnet-getting-started-part-2/_static/image18.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image17.png)

## <a name="configuring-database-rules-to-allow-deletion"></a>将数据库规则配置为允许删除

你将创建一个页面，使用户能够从 `Person` 表中删除学生，此表与其他表（`Course`、`StudentGrade`和 `OfficeAssignment`）有三个关系。 默认情况下，如果其中一个表中存在相关行，数据库将阻止您删除 `Person` 中的行。 您可以先手动删除相关行，也可以将数据库配置为删除 `Person` 行时自动删除这些行。 对于本教程中的学生记录，你将配置数据库以自动删除相关数据。 由于学生只能在 `StudentGrade` 表中有相关的行，因此只需配置这三个关系之一。

如果使用从本教程中的项目下载的*School .mdf*文件，则可以跳过此部分，因为这些配置更改已经完成。 如果通过运行脚本来创建数据库，请通过执行以下过程来配置数据库。

在**服务器资源管理器**中，打开你在第1部分中创建的数据库关系图。 右键单击 "`Person`" 和 "`StudentGrade`" 之间的关系（"表之间的线条"），然后选择 "**属性**"。

[![Image04](the-entity-framework-and-aspnet-getting-started-part-2/_static/image20.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image19.png)

在 "**属性**" 窗口中，展开 "**插入并更新规范**"，并将 " **DeleteRule** " 属性设置为**Cascade**。

[![Image05](the-entity-framework-and-aspnet-getting-started-part-2/_static/image22.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image21.png)

保存并关闭关系图。 如果系统询问您是否要更新数据库，请单击 **"是"** 。

若要确保模型将内存中的实体与数据库所执行的操作保持同步，必须在数据模型中设置相应的规则。 打开*SchoolModel*，右键单击 `Person` 和 `StudentGrade`之间的关联线，然后选择 "**属性**"。

[![Image21](the-entity-framework-and-aspnet-getting-started-part-2/_static/image24.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image23.png)

在 "**属性**" 窗口中，将**End1 OnDelete**设置为**Cascade**。

[![Image22](the-entity-framework-and-aspnet-getting-started-part-2/_static/image26.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image25.png)

保存并关闭*SchoolModel*文件，然后重新生成项目。

通常，当数据库发生更改时，可以选择多个选项来同步模型：

- 对于某些类型的更改（例如，添加或刷新表、视图或存储过程），请在设计器中右键单击，然后选择 "**从数据库更新模型**" 使设计器自动进行更改。
- 重新生成数据模型。
- 进行手动更新，与此类似。

在这种情况下，您可以重新生成模型或刷新由关系更改影响的表，但随后必须重新进行字段名称更改（从 `FirstName` 到 `FirstMidName`）。

## <a name="using-a-gridview-control-to-read-and-update-entities"></a>使用 GridView 控件读取和更新实体

在本部分中，你将使用 `GridView` 控件来显示、更新或删除学生。

打开或切换到 "student *" 并切换到 "* **设计**" 视图。 从 "**工具箱**" 的 "**数据**" 选项卡中，将 `GridView` 控件拖动到 `EntityDataSource` 控件的右侧，将其命名为 `StudentsGridView`，单击智能标记，然后选择 " **StudentsEntityDataSource** " 作为数据源。

[![Image06](the-entity-framework-and-aspnet-getting-started-part-2/_static/image28.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image27.png)

单击 "**刷新架构**" （如果系统提示确认，请单击 **"是"** ），然后单击 "**启用分页**"、"**启用排序**"、"**启用编辑**" 和 "**启用删除**"。

单击 "**编辑列**"。

[![Image10](the-entity-framework-and-aspnet-getting-started-part-2/_static/image30.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image29.png)

在 "**所选字段**" 框中，删除**PersonID**、 **LastName**和**雇佣**日期。 你通常不会向用户显示记录键，雇用日期与学生无关，你会将这两部分名称放在一个字段中，因此你只需要一个名称字段。）

[![Image11](the-entity-framework-and-aspnet-getting-started-part-2/_static/image32.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image31.png)

选择**FirstMidName**字段，然后单击 "**将此字段转换为 TemplateField**"。

对**EnrollmentDate**执行相同的操作。

[![Image13](the-entity-framework-and-aspnet-getting-started-part-2/_static/image34.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image33.png)

单击 **"确定"** ，然后切换到 "**源**" 视图。 其余更改将更容易直接在标记中进行。 `GridView` 控件标记现在如下例所示。

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-2/samples/sample3.aspx)]

命令字段之后的第一列是当前显示名字的模板字段。 更改此模板字段的标记，使其类似于以下示例：

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-2/samples/sample4.aspx)]

在显示模式下，两个 `Label` 控件显示名字和姓氏。 在编辑模式下，提供了两个文本框，以便您可以更改名字和姓氏。 与在显示模式下 `Label` 控件一样，你可以像使用直接连接到数据库的 ASP.NET 数据源控件一样使用 `Bind` 和 `Eval` 表达式。 唯一的差别在于，您指定的是实体属性而不是数据库列。

最后一列是显示注册日期的模板字段。 更改此字段的标记，使其类似于以下示例：

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-2/samples/sample5.aspx)]

在显示模式和编辑模式下，格式字符串 "{0，d}" 会使日期以 "短日期" 格式显示。 （您的计算机可能配置为以不同于本教程中所示的屏幕图像显示此格式。）

请注意，在每个模板字段中，设计器默认使用 `Bind` 表达式，但您已将其更改为 `ItemTemplate` 元素中的 `Eval` 表达式。 `Bind` 表达式使数据在 `GridView` 控件属性中可用，以防需要在代码中访问数据。 在此页中，您不需要在代码中访问此数据，因此您可以使用 `Eval`，这种效率更高。 有关详细信息，请参阅[从数据控件中获取数据](https://weblogs.asp.net/davidfowler/archive/2008/12/12/getting-your-data-out-of-the-data-controls.aspx)。

## <a name="revising-entitydatasource-control-markup-to-improve-performance"></a>修改 EntityDataSource 控件标记以提高性能

在 `EntityDataSource` 控件的标记中，删除 `ConnectionString` 和 `DefaultContainerName` 属性，并将其替换为 `ContextTypeName="ContosoUniversity.DAL.SchoolEntities"` 特性。 这是每次创建 `EntityDataSource` 控件时应进行的更改，除非你需要使用与在对象上下文类中进行硬编码的连接不同的连接。 使用 `ContextTypeName` 特性具有以下优势：

- 性能更好。 当 `EntityDataSource` 控件使用 `ConnectionString` 和 `DefaultContainerName` 特性初始化数据模型时，它将执行额外的工作以加载每个请求的元数据。 如果指定 `ContextTypeName` 属性，则不是必需的。
- 默认情况下，延迟加载在实体框架4.0 中生成的对象上下文类（如本教程 `SchoolEntities`）中处于打开状态。 这意味着，导航属性将在需要时自动加载相关数据。 稍后将在本教程中更详细地介绍延迟加载。
- 已应用于对象上下文类的所有自定义项（在此示例中，`SchoolEntities` 类）将可用于使用 `EntityDataSource` 控件的控件。 自定义对象上下文类是本系列教程未涵盖的高级主题。 有关详细信息，请参阅[扩展实体框架生成的类型](https://msdn.microsoft.com/library/dd456844.aspx)。

标记现在将类似于以下示例（属性的顺序可能不同）：

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-2/samples/sample6.aspx)]

`EnableFlattening` 属性指的是早期版本的实体框架中所需的功能，因为外键列并未作为实体属性公开。 当前版本允许使用*外键关联*，这意味着外键属性是针对所有但多对多关联公开的。 如果实体具有外键属性，而没有[复杂类型](https://msdn.microsoft.com/library/bb738472.aspx)，则可以将此特性设置为 `False`。 请勿从标记中删除属性，因为默认值为 `True`。 有关详细信息，请参阅[平展对象（EntityDataSource）](https://msdn.microsoft.com/library/ee404746.aspx)。

运行页面，你将看到学生和员工的列表（在下一教程中，你将仅针对学生进行筛选）。 名字和姓氏一起显示在一起。

[![Image07](the-entity-framework-and-aspnet-getting-started-part-2/_static/image36.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image35.png)

若要对显示进行排序，请单击列名称。

单击任意行中的 "**编辑**"。 此时会显示文本框，可以在其中更改名字和姓氏。

[![Image08](the-entity-framework-and-aspnet-getting-started-part-2/_static/image38.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image37.png)

"**删除**" 按钮也可以正常工作。 对于具有注册日期的行，单击 "删除"，该行将会消失。 （无注册日期的行表示讲师，你可能会收到引用完整性错误。 在下一教程中，你将筛选此列表，使其仅包含学生。）

## <a name="displaying-data-from-a-navigation-property"></a>显示导航属性中的数据

现在假设你想要了解每个学生注册的课程数。 实体框架在 `Person` 实体的 `StudentGrades` 导航属性中提供这些信息。 由于数据库设计不允许学生在没有分配评分的情况下注册，因此，对于本教程，您可以假设与课程关联的 `StudentGrade` 表行中的行与在课程中注册的行相同。 （`Courses` 导航属性仅适用于讲师。）

当你使用 `EntityDataSource` 控件的 `ContextTypeName` 属性时，在访问该属性时，实体框架会自动检索导航属性的信息。 这称为 "*延迟加载*"。 但是，这可能效率低下，因为这会导致每次需要额外信息时都单独调用数据库。 如果您需要 `EntityDataSource` 控件返回的每个实体的导航属性中的数据，则在对数据库的单个调用中检索相关数据以及实体本身会更有效。 这称为*预先加载*，通过设置 `EntityDataSource` 控件的 `Include` 属性，为导航属性指定预先加载。

在*default.aspx*中，你希望显示每个学生的课程数量，因此预先加载是最佳选择。 如果你正在显示所有学生，但只显示几个课程的课程数量（这需要编写除标记之外的一些代码），则延迟加载可能是更好的选择。

打开或切换到 *"student*"，切换到 "**设计**" 视图，选择 "`StudentsEntityDataSource`"，然后在 "**属性**" 窗口中将 " **StudentGrades**" 属性设置**为 ""** 。 （如果你想要获取多个导航属性，则可以指定它们的名称，用逗号分隔，例如**StudentGrades、课程**。）

[![Image19](the-entity-framework-and-aspnet-getting-started-part-2/_static/image40.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image39.png)

切换到 "**源**" 视图。 在 `StudentsGridView` 控件中的最后一个 `asp:TemplateField` 元素之后，添加以下新的模板字段：

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-2/samples/sample7.aspx)]

在 `Eval` 表达式中，可以 `StudentGrades`引用导航属性。 由于此属性包含一个集合，因此它具有一个 `Count` 属性，您可以使用该属性来显示注册了学生的课程的数目。 在后面的教程中，你将了解如何显示包含单个实体而不是集合的导航属性中的数据。 （请注意，不能使用 `BoundField` 元素显示导航属性中的数据。）

运行该页，现在可以看到每个学生注册了多少课程。

[![Image20](the-entity-framework-and-aspnet-getting-started-part-2/_static/image42.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image41.png)

## <a name="using-a-detailsview-control-to-insert-entities"></a>使用 DetailsView 控件插入实体

下一步是创建一个具有 `DetailsView` 控件的页面，您可以在其中添加新的学生。 关闭浏览器，然后使用 "*网站*母版页" 创建新网页。 将该页命名为*StudentsAdd*，然后切换到 "**源**" 视图。

添加以下标记，以替换名为 `Content2`的 `Content` 控件的现有标记：

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-2/samples/sample8.aspx)]

此标记创建一个 `EntityDataSource` 控件，该控件类似于在*default.aspx*中创建的控件，但它允许插入。 与 `GridView` 控件一样，`DetailsView` 控件的绑定字段的编码方式与直接连接到数据库的数据控件的绑定字段不同，只不过它们引用实体属性。 在这种情况下，`DetailsView` 控件仅用于插入行，因此您已将默认模式设置为 `Insert`。

运行该页并添加新的学生。

[![Image09](the-entity-framework-and-aspnet-getting-started-part-2/_static/image44.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image43.png)

插入新的学生后不会发生什么情况，但如果你现在*运行了*student，你将看到新的学生信息。

## <a name="displaying-data-in-a-drop-down-list"></a>在下拉列表中显示数据

在下面的步骤中，你将使用 `EntityDataSource` 控件将 `DropDownList` 控件 databind 到实体集。 在本教程的此部分中，你将不会执行此操作。 但在后续部分中，你将使用列表让用户选择一个部门来显示与该部门关联的课程。

创建新的名为 "*课程*" 的网页。 在 "**源**" 视图中，将标题添加到名为 `Content2`的 `Content` 控件：

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-2/samples/sample9.aspx)]

在 "**设计**" 视图中，像以前一样向页面添加 `EntityDataSource` 控件，只不过此时间名 `DepartmentsEntityDataSource`。 选择 "**部门**" 作为**EntitySetName**值，并仅选择 " **DepartmentID** " 和 " **Name** " 属性。

[![Image15](the-entity-framework-and-aspnet-getting-started-part-2/_static/image46.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image45.png)

从 "工具箱" 的 "**标准**" 选项卡中，将 **"** `DropDownList`" 控件拖动到页面上，将其命名为 `DepartmentsDropDownList`，单击智能标记，然后选择 "**选择数据源**" 以启动 "数据源**配置向导**"。

[![Image16](the-entity-framework-and-aspnet-getting-started-part-2/_static/image48.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image47.png)

在 "**选择数据源**" 步骤中，选择 " **DepartmentsEntityDataSource** " 作为数据源，单击 "**刷新架构**"，然后选择 "**名称**" 作为要显示的数据字段，并选择 " **DepartmentID** " 作为值数据字段。 单击“确定”。

[![Image17](the-entity-framework-and-aspnet-getting-started-part-2/_static/image50.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image49.png)

使用实体框架对控件进行数据绑定的方法与其他 ASP.NET 数据源控件相同，不同之处在于指定实体和实体属性。

切换到 "**源**" 视图，并在 `DropDownList` 控件之前添加 "选择一个部门："。

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-2/samples/sample10.aspx)]

作为提醒，请将 `ConnectionString` 和 `DefaultContainerName` 特性替换为 `ContextTypeName="ContosoUniversity.DAL.SchoolEntities"` 特性，此时更改 `EntityDataSource` 控件的标记。 在更改 `EntityDataSource` 控件标记之前，通常最好等待，直到创建了链接到数据源控件的数据绑定控件，因为在进行更改后，设计器不会在数据绑定控件中提供**刷新架构**选项。

运行页面，您可以从下拉列表中选择一个部门。

[![Image18](the-entity-framework-and-aspnet-getting-started-part-2/_static/image52.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image51.png)

这将完成使用 `EntityDataSource` 控件的简介。 通常，使用此控件与使用其他 ASP.NET 数据源控件没有什么不同，只是引用实体和属性，而不是引用表和列。 唯一的例外是要访问导航属性。 在下一教程中，您将看到，在对数据进行筛选、分组和排序时，您用于 `EntityDataSource` 控件的语法也可能与其他数据源控件不同。

> [!div class="step-by-step"]
> [上一页](the-entity-framework-and-aspnet-getting-started-part-1.md)
> [下一页](the-entity-framework-and-aspnet-getting-started-part-3.md)
