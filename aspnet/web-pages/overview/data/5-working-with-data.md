---
uid: web-pages/overview/data/5-working-with-data
title: 在 ASP.NET 网页（Razor）站点中使用数据库的简介 |Microsoft Docs
author: Rick-Anderson
description: 本章介绍了如何从数据库访问数据，并使用 ASP.NET 网页来显示数据。
ms.author: riande
ms.date: 02/18/2014
ms.assetid: 673d502f-2c16-4a6f-bb63-dbfd9a77ef47
msc.legacyurl: /web-pages/overview/data/5-working-with-data
msc.type: authoredcontent
ms.openlocfilehash: 45e988d037465e59ad352bb9444af2c69fd3cd70
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78474038"
---
# <a name="introduction-to-working-with-a-database-in-aspnet-web-pages-razor-sites"></a>在 ASP.NET 网页（Razor）站点中使用数据库简介

作者： [Tom FitzMacken](https://github.com/tfitzmac)

> 本文介绍如何使用 Microsoft WebMatrix 工具在 ASP.NET 网页（Razor）网站中创建数据库，以及如何创建可用于显示、添加、编辑和删除数据的页面。
> 
> **你将学习的内容：** 
> 
> - 如何创建数据库。
> - 如何连接到数据库。
> - 如何在网页中显示数据。
> - 如何插入、更新和删除数据库记录。
> 
> 下面是本文中介绍的功能：
> 
> - 使用 Microsoft SQL Server Compact 版本的数据库。
> - 使用 SQL 查询。
> - `Database` 类。
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>本教程中使用的软件版本
> 
> 
> - ASP.NET 网页（Razor）2
> - WebMatrix 2
>   
> 
> 本教程还适用于 WebMatrix 3。 你可以使用 ASP.NET 网页3和 Visual Studio 2013 （对于 Web 为 Visual Studio Express 2013）;但是，用户界面将有所不同。

## <a name="introduction-to-databases"></a>数据库简介

假设一个典型的通讯簿。 对于通讯簿中的每个条目（即，对于每个人），都有几个信息，如名字、姓氏、地址、电子邮件地址和电话号码。

图片数据的一种典型方式是使用行和列作为表。 在数据库术语中，每行通常称为记录。 每个列（有时称为字段）都包含每个数据类型的值：名字、姓氏等。

| **ID** | **FirstName** | **LastName** | **地址** | **电子邮件** | **电话** |
| --- | --- | --- | --- | --- | --- |
| 1 | Jim | Abrus | 210 100th St SE Orcas WA 98031 | jim@contoso.com | 555 0100 |
| 2 | Terry | Adams | 1234主要圣西雅图 WA 99011 | terry@cohowinery.com | 555 0101 |

对于大多数数据库表，表必须具有包含唯一标识符的列，如客户编号、帐户号等。这称为表的*主键*，你可以使用它来标识表中的每一行。 在此示例中，ID 列是通讯簿的主键。

通过这一对数据库的基本了解，你可以了解如何创建简单的数据库并执行一些操作，如添加、修改和删除数据。

> [!TIP] 
> 
> **关系数据库**
> 
> 可以通过多种方式存储数据，包括文本文件和电子表格。 但对于大多数业务用途，数据存储在关系数据库中。
> 
> 本文不会深入到数据库。 但是，你可能会发现很少理解它们。 在关系数据库中，信息以逻辑方式划分为单独的表。 例如，学校的数据库可能包含学生的单独表和类产品。 数据库软件（如 SQL Server）支持功能强大的命令，可让您动态建立表之间的关系。 例如，您可以使用关系数据库建立学生与类之间的逻辑关系，以便创建计划。 将数据存储在单独的表中可降低表结构的复杂性，并减少在表中保留冗余数据的需要。

## <a name="creating-a-database"></a>创建数据库

此过程说明如何使用 WebMatrix 中包含的 SQL Server Compact 数据库设计工具创建名为 SmallBakery 的数据库。 虽然您可以使用代码创建数据库，但使用 WebMatrix 等设计工具创建数据库表和数据库表更常见。

1. 启动 WebMatrix，然后在 "快速入门" 页上，单击 "**从模板中选择站点**"。
2. 选择 "**空站点**"，然后在 "**站点名称**" 框中输入 "SmallBakery"，然后单击 **"确定**"。 在 WebMatrix 中创建并显示该站点。
3. 在左窗格中，单击 "**数据库**" 工作区。
4. 在功能区中，单击 "**新建数据库**"。 使用与你的站点相同的名称创建一个空数据库。
5. 在左窗格中，展开 " **SmallBakery** " 节点，然后单击 "**表**"。
6. 在功能区中，单击 "**新建表**"。 WebMatrix 打开表设计器。

    ![[图像]](5-working-with-data/_static/image1.jpg)
7. 单击 "**名称**" 列，并输入 &quot;Id&quot;。
8. 在 "**数据类型**" 列中，选择**int**。
9. 是否设置**为主键？** 并将 **？选项标识**为**Yes**。

    如名称所示，**为 Primary key**告诉数据库这将是表的主键。 **Is Identity**告诉数据库自动为每个新记录创建一个 ID 号，并向其分配下一个顺序编号（从1开始）。
10. 单击下一行。 编辑器会启动新的列定义。
11. 对于 "名称" 值，请输入 &quot;名称&quot;。
12. 对于 "**数据类型**"，请选择 "&quot;nvarchar&quot; 并将长度设置为50。 `nvarchar` 的*var*部分通知数据库，此列的数据将是字符串，其大小可能因记录而异。 （ *N*前缀表示*国家/地区*，表示该字段可以保存表示任何字母或书写系统&#8212;的字符数据，即，该字段包含 Unicode 数据。）
13. 将 "**允许 Null 值**" 选项设置为 "**否**"。 这会强制 "*名称*" 列不留空。
14. 使用同一个过程创建一个名为*Description*的列。 将**数据类型**设置为 "nvarchar"，将50设置为长度，将 "**允许 null 值**" 设置为 "false"。
15. 创建名为*Price*的列。 将 **"数据类型" 设置为 "money"** 并将 "**允许 null** " 设置为 "false"。
16. 在顶部的框中，将表命名为 &quot;产品&quot;。

    完成后，定义将如下所示：

    ![[图像]](5-working-with-data/_static/image2.png)
17. 按 Ctrl + S 保存表。

## <a name="adding-data-to-the-database"></a>向数据库添加数据

现在，你可以将一些示例数据添加到你稍后将在本文中使用的数据库。

1. 在左窗格中，展开 " **SmallBakery** " 节点，然后单击 "**表**"。
2. 右键单击 Product 表，然后单击 "**数据**"。
3. 在 "编辑" 窗格中，输入以下记录：

    | **Name** | **描述** | **价值** |
    | --- | --- | --- |
    | 面包 | 每日融入。 | 2.99 |
    | 草莓松饼 | 与我们的菜园 strawberries。 | 9.99 |
    | Apple 饼图 | 第二次仅限您母亲的饼图。 | 12.99 |
    | Pecan 饼图 | 如果您喜欢 pecans，这就是您的。 | 10.99 |
    | 柠檬饼图 | 利用世界上最好的 lemons。 | 11.99 |
    | 纸托蛋糕 | 你的孩子和你的孩子会喜欢这些。 | 7.99 |

    请记住，您不必为*Id*列输入任何内容。 创建*Id*列后，将其 "**为标识**" 属性设置为 "true"，这会使其自动填充。

    输入完数据后，表设计器将如下所示：

    ![[图像]](5-working-with-data/_static/image3.jpg)
4. 关闭包含数据库数据的选项卡。

## <a name="displaying-data-from-a-database"></a>显示数据库中的数据

如果数据库中包含数据，则可以在 ASP.NET 网页中显示数据。 若要选择要显示的表行，请使用 SQL 语句，该语句是传递到数据库的命令。

1. 在左窗格中，单击 "**文件**" 工作区。
2. 在网站的根目录中，创建一个名为*ListProducts*的新的 CSHTML 页面。
3. 将现有标记替换为以下内容：

    [!code-cshtml[Main](5-working-with-data/samples/sample1.cshtml)]

    在第一个代码块中，打开前面创建的*SmallBakery*文件（数据库）。 `Database.Open` 方法假定 *.sdf*文件位于网站的*应用\_Data*文件夹中。 （请注意，不需要指定&#8212; .sdf 扩展名 *。* 实际上，如果您这样做，`Open` 方法将不起作用。）

    > [!NOTE]
    > *应用\_Data*文件夹是 ASP.NET 中用于存储数据文件的特殊文件夹。 有关详细信息，请参阅本文后面的[连接到数据库](#SB_ConnectingToADatabase)。

    然后，使用以下 SQL `Select` 语句发出查询数据库的请求：

    [!code-sql[Main](5-working-with-data/samples/sample2.sql)]

    在语句中，`Product` 标识要查询的表。 `*` 字符指定查询应返回表中的所有列。 （如果只想查看某些列，也可以单独列出列，用逗号分隔）。`Order By` 子句指示在这种情况下，应&#8212;按*名称*列对数据进行排序的方式。 这意味着数据根据每行的 "*名称*" 列的值按字母顺序排序。

    在页面的正文中，标记创建将用于显示数据的 HTML 表。 在 `<tbody>` 元素中，使用 `foreach` 循环单独获取查询返回的每个数据行。 对于每个数据行，创建一个 HTML 表行（`<tr>` 元素）。 然后，为每个列创建 HTML 表单元格（`<td>` 元素）。 每次遍历循环时，数据库中的下一个可用行将位于 `row` 变量（在 `foreach` 语句中设置此项）。 若要从行中获取单个列，可以使用 `row.Name` 或 `row.Description`，或者使用所需的列名称。
4. 在浏览器中运行页。 （请确保在运行之前在 "**文件**" 工作区中选择了该页面。）页面将显示如下所示的列表：

    ![[图像]](5-working-with-data/_static/image4.jpg)

> [!TIP] 
> 
> **结构化查询语言 (SQL)**
> 
> SQL 是在大多数关系数据库中用于管理数据库中的数据的一种语言。 它包含的命令可用于检索和更新数据，并允许您创建、修改和管理数据库表。 SQL 不同于编程语言（例如，您在 WebMatrix 中使用的语言），因为使用 SQL 时，这一理念是告诉数据库您所需的内容，而数据库的工作是确定如何获取数据或执行任务。 下面是一些 SQL 命令的示例和它们的作用：
> 
> `SELECT Id, Name, Price FROM Product WHERE Price > 10.00 ORDER BY Name`
> 
> 如果 "*价格*" 的值大于10，则将从*Product*表的记录中提取*Id*、*名称*和*价格*列，并根据*Name*列的值以字母顺序返回结果。 此命令将返回一个结果集，其中包含满足条件的记录; 如果没有记录匹配，则返回空集。
> 
> `INSERT INTO Product (Name, Description, Price) VALUES ("Croissant", "A flaky delight", 1.99)`
> 
> 这会在*Product*表中插入一条新记录，将*Name*列设置为 &quot;新月形面包&quot;，将*Description*列设置为 &quot;不可靠感到满意&quot;，并将价格设置为1.99。
> 
> `DELETE FROM Product WHERE ExpirationDate < "01/01/2008"`
> 
> 此命令删除*Product*表中的记录，其到期日期列早于2008年1月1日。 （这假定*Product*表具有这样的列。）此处以 MM/DD/YYYY 格式输入日期，但应以用于区域设置的格式输入。
> 
> `Insert Into` 和 `Delete` 命令不返回结果集。 相反，它们将返回一个数字，该数字告诉你命令所影响的记录数。
> 
> 对于某些操作（例如插入和删除记录），请求操作的进程必须在数据库中具有适当的权限。 这就是在连接到数据库时，生产数据库经常必须提供用户名和密码的原因。
> 
> 有多个 SQL 命令，但它们都遵循类似的模式。 您可以使用 SQL 命令来创建数据库表，计算表中的记录数，计算价格，以及执行更多操作。

## <a name="inserting-data-in-a-database"></a>在数据库中插入数据

本部分介绍如何创建一个页面，使用户能够向*产品*数据库表添加新产品。 插入新产品记录后，页面将使用您在上一节中创建的*ListProducts*页面显示更新后的表。

此页包括验证以确保用户输入的数据对数据库有效。 例如，页面中的代码可确保已为所有必需列输入了值。

1. 在网站中，创建一个名为*InsertProducts*的新的 CSHTML 文件。
2. 将现有标记替换为以下内容：

    [!code-cshtml[Main](5-working-with-data/samples/sample3.cshtml)]

    页面的正文包含一个 HTML 窗体，其中包含三个文本框，用户可以在其中输入名称、说明和价格。 当用户单击 "**插入**" 按钮时，页面顶部的代码会打开与*SmallBakery*数据库的连接。 然后，使用 `Request` 对象获取用户已提交的值，并将这些值分配给本地变量。

    若要验证用户是否输入了每个所需列的值，需注册要验证的每个 `<input>` 元素：

    [!code-csharp[Main](5-working-with-data/samples/sample4.cs)]

    `Validation` helper 检查已注册的每个字段中是否存在值。 您可以通过检查 `Validation.IsValid()`来测试所有字段是否通过验证，这通常是在处理您从用户那里获取的信息之前执行的：

    [!code-csharp[Main](5-working-with-data/samples/sample5.cs)]

    （`&&` 运算符表示和，这是因为*这是一个窗体提交并且所有字段均已通过验证*。）

    如果所有列均已验证（none 均为空），则继续并创建一个 SQL 语句来插入数据，然后执行该语句，如下所示：

    [!code-csharp[Main](5-working-with-data/samples/sample6.cs)]

    要插入的值包括参数占位符（`@0`、`@1``@2`）。

    > [!NOTE]
    > 作为安全预防措施，请始终使用参数将值传递给 SQL 语句，如前面的示例中所示。 这使您有机会验证用户的数据，并帮助防止尝试向数据库发送恶意命令（有时称为 SQL 注入式攻击）。

    若要执行查询，请使用此语句，并向其传递包含用于替换占位符的值的变量：

    [!code-csharp[Main](5-working-with-data/samples/sample7.cs)]

    执行 `Insert Into` 语句后，可以使用以下行将用户发送到列出产品的页面：

    [!code-javascript[Main](5-working-with-data/samples/sample8.js)]

    如果验证未成功，则会跳过插入。 相反，可以在页面中使用一个帮助器来显示累积的错误消息（如果有）：

    [!code-cshtml[Main](5-working-with-data/samples/sample9.cshtml)]

    请注意，标记中的样式块包含名为 `.validation-summary-errors`的 CSS 类定义。 这是默认情况下为包含任何验证错误的 `<div>` 元素使用的 CSS 类的名称。 在这种情况下，CSS 类指定验证摘要错误以红色和粗体显示，但你可以定义 `.validation-summary-errors` 类以显示你喜欢的任何格式。

### <a name="testing-the-insert-page"></a>测试插入页

1. 查看浏览器中的页面。 页面将显示类似于下图所示的窗体。

    ![[图像]](5-working-with-data/_static/image5.jpg)
2. 输入所有列的值，但请确保将 " *Price* " 列留空。
3. 单击“插入”。 此页将显示一条错误消息，如下图所示。 （不创建新记录。）

    ![[图像]](5-working-with-data/_static/image6.jpg)
4. 完全填写表单，然后单击 "**插入**"。 此时，将显示 " *ListProducts* " 页，并显示新记录。

## <a name="updating-data-in-a-database"></a>更新数据库中的数据

将数据输入到表中后，可能需要对其进行更新。 此过程说明如何创建两个与之前为数据插入创建的页面相似的页面。 第一页显示产品，并允许用户选择一个要更改的产品。 在第二页中，用户可以实际进行编辑并保存。

> [!NOTE] 
> 
> **重要提示**在生产网站中，通常会限制允许对数据进行更改的人员。 有关如何设置成员身份和授权用户在网站上执行任务的方式的信息，请参阅向[ASP.NET 网页站点添加安全性和成员身份](https://go.microsoft.com/fwlink/?LinkId=202904)。

1. 在网站中，创建一个名为*EditProducts*的新的 CSHTML 文件。
2. 将文件中的现有标记替换为以下内容：

    [!code-cshtml[Main](5-working-with-data/samples/sample10.cshtml)]

    此页与之前的*ListProducts*页之间的唯一区别是，此页中的 HTML 表包含一个额外的列，其中显示了 "**编辑**" 链接。 单击此链接后，将转到*UpdateProducts*页（接下来将创建），可以在其中编辑选定的记录。

    查看创建**编辑**链接的代码：

    [!code-cshtml[Main](5-working-with-data/samples/sample11.cshtml)]

    这会创建一个 HTML `<a>` 元素，其 `href` 属性进行动态设置。 `href` 属性指定用户单击链接时要显示的页面。 它还将当前行的 `Id` 值传递到链接。 当页面运行时，页面源可能会包含如下所示的链接：

    [!code-html[Main](5-working-with-data/samples/sample12.html)]

    请注意，`href` 特性设置为 "`UpdateProducts/n`"，其中*n*是一个产品编号。 当用户单击其中一个链接时，生成的 URL 将如下所示：

    `http://localhost:18816/UpdateProducts/6`

    换言之，要编辑的产品编号将传入 URL。
3. 查看浏览器中的页面。 页面按如下格式显示数据：

    ![[图像]](5-working-with-data/_static/image7.jpg)

    接下来，您将创建允许用户实际更新数据的页面。 "更新" 页包括用于验证用户输入的数据的验证。 例如，页面中的代码可确保已为所有必需列输入了值。
4. 在网站中，创建一个名为*UpdateProducts*的新的 CSHTML 文件。
5. 将文件中的现有标记替换为以下项。

    [!code-cshtml[Main](5-working-with-data/samples/sample13.cshtml)]

    页面正文包含一个 HTML 窗体，其中显示了产品以及用户可以对其进行编辑。 要使产品显示，请使用以下 SQL 语句：

    [!code-sql[Main](5-working-with-data/samples/sample14.sql)]

    这会选择其 ID 与 `@0` 参数中传递的值匹配的产品。 （因为*Id*是主键，因此必须是唯一的，因此，只能通过这种方式选择一个产品记录。）若要获取要传递给此 `Select` 语句的 ID 值，可以使用以下语法读取作为 URL 的一部分传递到页面的值：

    [!code-csharp[Main](5-working-with-data/samples/sample15.cs)]

    若要实际提取产品记录，可以使用 `QuerySingle` 方法，该方法将仅返回一条记录：

    [!code-csharp[Main](5-working-with-data/samples/sample16.cs)]

    将单个行返回 `row` 变量。 可以从每个列中获取数据，并将其分配给本地变量，如下所示：

    [!code-csharp[Main](5-working-with-data/samples/sample17.cs)]

    在窗体的标记中，这些值通过使用嵌入的代码自动显示在单独的文本框中，如下所示：

    [!code-html[Main](5-working-with-data/samples/sample18.html)]

    代码的该部分显示要更新的产品记录。 显示记录后，用户可以编辑单独的列。

    当用户通过单击 "**更新**" 按钮提交窗体时，`if(IsPost)` 块中的代码将运行。 这将从 `Request` 对象获取用户的值，将值存储在变量中，并验证是否已填充每个列。 如果验证通过，代码将创建以下 SQL Update 语句：

    [!code-sql[Main](5-working-with-data/samples/sample19.sql)]

    在 SQL `Update` 语句中，可以指定要更新的每个列以及要将其设置为的值。 在此代码中，将使用参数占位符指定值 `@0`、`@1`、`@2`等。 （如前文所述，为安全，应始终使用参数将值传递给 SQL 语句。）

    调用 `db.Execute` 方法时，将按与 SQL 语句中的参数对应的顺序传递包含值的变量：

    [!code-csharp[Main](5-working-with-data/samples/sample20.cs)]

    执行 `Update` 语句后，调用以下方法，以便将用户重定向回编辑页面：

    [!code-cshtml[Main](5-working-with-data/samples/sample21.cshtml)]

    其作用是用户在数据库中查看数据的更新列表，并可以编辑其他产品。
6. 保存页。
7. 运行*EditProducts*页（而不是 "更新" 页），然后单击 "**编辑**" 以选择要编辑的产品。 随即显示 " *UpdateProducts* " 页，其中显示了所选的记录。

    ![[图像]](5-working-with-data/_static/image8.jpg)
8. 进行更改，然后单击 "**更新**"。 "产品" 列表将再次显示您更新的数据。

## <a name="deleting-data-in-a-database"></a>删除数据库中的数据

本部分说明如何允许用户从*产品*数据库表中删除产品。 该示例由两个页面组成。 在第一页中，用户选择要删除的记录。 然后，将在另一页中显示要删除的记录，让他们确认是否要删除该记录。

> [!NOTE] 
> 
> **重要提示**在生产网站中，通常会限制允许对数据进行更改的人员。 有关如何设置成员身份和授权用户在网站上执行任务的方式的信息，请参阅[将安全性和成员身份添加到 ASP.NET 网页站点](https://go.microsoft.com/fwlink/?LinkId=202904)。

1. 在网站中，创建一个名为*ListProductsForDelete*的新的 CSHTML 文件。
2. 将现有标记替换为以下内容：

    [!code-cshtml[Main](5-working-with-data/samples/sample22.cshtml)]

    此页面类似于前面的*EditProducts*页面。 但是，它不会显示每个产品的**编辑**链接，而是显示 "**删除**" 链接。 使用标记中的以下嵌入代码创建 "**删除**" 链接：

    [!code-cshtml[Main](5-working-with-data/samples/sample23.cshtml)]

    当用户单击链接时，这会创建如下所示的 URL：

    `http://<server>/DeleteProduct/4`

    此 URL 调用名为*DeleteProduct*的页面（稍后将创建），并向其传递要删除的产品的 ID （此处为4）。
3. 保存该文件，但将其保持打开状态。
4. 创建另一个名为*DeleteProduct*的 CHTML 文件。 将现有内容替换为以下内容：

    [!code-cshtml[Main](5-working-with-data/samples/sample24.cshtml)]

    此页面由*ListProductsForDelete*调用，并允许用户确认他们要删除产品。 若要列出要删除的产品，请使用以下代码获取要从 URL 中删除的产品的 ID：

    [!code-csharp[Main](5-working-with-data/samples/sample25.cs)]

    然后，该页会要求用户单击某个按钮以实际删除该记录。 这是一项重要的安全措施：在网站中执行敏感操作（如更新或删除数据）时，这些操作应始终使用 POST 操作完成，而不是 GET 操作。 如果你的站点已设置为可以使用 GET 操作执行删除操作，则任何人都可以传递类似 `http://<server>/DeleteProduct/4` 的 URL，并从数据库中删除所需的任何内容。 通过添加确认和编码页面，以便只能使用 POST 来执行删除操作，可将安全度量值添加到站点。

    使用以下代码执行实际的删除操作，该操作首先确认这是 post 操作，并且该 ID 不为空：

    [!code-csharp[Main](5-working-with-data/samples/sample26.cs)]

    此代码运行一个 SQL 语句，该语句删除指定的记录，然后将该用户重定向回列表页。
5. 在浏览器中运行*ListProductsForDelete* 。

    ![[图像]](5-working-with-data/_static/image9.jpg)
6. 单击其中一个产品的 "**删除**" 链接。 随即显示 " *DeleteProduct* " 页，确认是否要删除该记录。
7. 单击“删除”按钮。 将删除产品记录，并使用更新的产品列表刷新页面。

> [!TIP]
> 
> <a id="SB_ConnectingToADatabase"></a>
> ### <a name="connecting-to-a-database"></a>连接到数据库
> 
> 可以通过两种方式连接到数据库。 第一种方法是使用 `Database.Open` 方法并指定数据库文件的名称（更少为 *.sdf*扩展名）：
> 
> `var db = Database.Open("SmallBakery");`
> 
> `Open` 方法假定。 *.sdf*文件位于网站的*应用\_Data*文件夹中。 此文件夹专用于存放数据。 例如，它有适当的权限允许网站读取和写入数据，作为一种安全措施，WebMatrix 不允许从此文件夹访问文件。
> 
> 第二种方法是使用连接字符串。 连接字符串包含数据库连接方式的相关信息。 这可以包括文件路径，也可以包含本地或远程服务器上 SQL Server 数据库的名称，以及用于连接到该服务器的用户名和密码。 （如果将数据保存在 SQL Server 的集中管理的版本中，如在托管提供商的站点上，则始终使用连接字符串指定数据库连接信息。）
> 
> 在 WebMatrix 中，连接字符串通常存储*在名为 web.config 的*XML 文件中。顾名思义，你可以在网站的根目录中使用*web.config 文件来*存储站点的配置信息，包括站点可能需要的任何连接字符串。 *Web.config 文件中*的连接字符串的示例可能如下所示：
> 
> [!code-xml[Main](5-working-with-data/samples/sample27.xml)]
> 
> 在此示例中，连接字符串指向在服务器上运行的 SQL Server 实例中的某个数据库（而不是本地 *.sdf*文件）。 你需要用适当的名称替换 `myServer` 和 `myDatabase`，并为 `username` 和 `password`指定 SQL Server 登录值。 （"用户名" 和 "密码" 值不一定与你的 Windows 凭据相同，或与你的托管提供商提供的用于登录到其服务器的值相同。 请与管理员联系以获取所需的确切值。）
> 
> `Database.Open` 方法非常灵活，因为它允许您传递数据库 *.sdf*文件的名称或存储在*web.config 文件中的连接*字符串的名称。 下面的示例演示如何使用前面示例中所示的连接字符串连接到数据库：
> 
> [!code-cshtml[Main](5-working-with-data/samples/sample28.cshtml)]
> 
> 如上所述，使用 `Database.Open` 方法可以传递数据库名称或连接字符串，并且它将找出要使用的数据库名称或连接字符串。 当你部署（发布）你的网站时，这非常有用。 当你在开发和测试网站时，可以在应用中使用 *.sdf*文件 *\_Data*文件夹。 然后，当你将站点移到生产服务器时，可以在*web.config 文件中*使用与 *.sdf*文件相同的连接字符串，但这&#8212;一切都不需要更改你的代码。
> 
> 最后，如果要直接使用连接字符串，可以调用 `Database.OpenConnectionString` 方法，并向其传递实际的连接字符串，而不只是*web.config*文件中的连接字符串的名称。 此方法在以下情况下可能非常有用：由于某种原因，你无法访问连接字符串（或其中的值，如 *.sdf*文件名），直到页面运行为止。 但在大多数情况下，你可以使用本文中所述的 `Database.Open`。

## <a name="additional-resources"></a>其他资源

- [SQL Server Compact](https://www.microsoft.com/sqlserver/2008/en/us/compact.aspx)
- [连接到 WebMatrix 中的 SQL Server 或 MySQL 数据库](https://go.microsoft.com/fwlink/?LinkId=208661)
- [在 ASP.NET 网站中验证用户输入](https://go.microsoft.com/fwlink/?LinkId=253002)
