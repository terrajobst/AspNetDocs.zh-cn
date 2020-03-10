---
uid: web-pages/overview/getting-started/introducing-aspnet-web-pages-2/displaying-data
title: 介绍 ASP.NET 网页-显示数据 |Microsoft Docs
author: Rick-Anderson
description: 本教程演示如何在 WebMatrix 中创建数据库，以及如何在使用 ASP.NET 网页（Razor）时在页面中显示数据库数据。 它假定 。
ms.author: riande
ms.date: 05/28/2015
ms.assetid: b3a006a0-3ea2-4d45-b833-e20e3a3c0a1a
msc.legacyurl: /web-pages/overview/getting-started/introducing-aspnet-web-pages-2/displaying-data
msc.type: authoredcontent
ms.openlocfilehash: 9e665ca8dd064c23a8b8bd3593014969d0c3da48
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78421484"
---
# <a name="introducing-aspnet-web-pages---displaying-data"></a>介绍 ASP.NET 网页-显示数据

作者： [Tom FitzMacken](https://github.com/tfitzmac)

> 本教程演示如何在 WebMatrix 中创建数据库，以及如何在使用 ASP.NET 网页（Razor）时在页面中显示数据库数据。 它假定您已完成了关于[ASP.NET 网页编程的介绍](../introducing-razor-syntax-c.md)。
> 
> 学习内容：
> 
> - 如何使用 WebMatrix 工具创建数据库表和数据库表。
> - 如何使用 WebMatrix 工具向数据库添加数据。
> - 如何在页面上显示数据库中的数据。
> - 如何在 ASP.NET 网页中运行 SQL 命令。
> - 如何自定义 `WebGrid` 帮助程序以更改数据显示以及添加分页和排序。
>   
> 
> 介绍的功能/技术：
> 
> - WebMatrix 数据库工具。
> - `WebGrid` 帮助程序。

## <a name="what-youll-build"></a>你将生成

在上一教程中，你已引入 ASP.NET 网页（*cshtml*文件）、Razor 语法的基础知识和帮助程序。 在本教程中，您将开始创建将用于序列的其余部分的实际 web 应用程序。 该应用程序是一个简单的电影应用程序，可让你查看、添加、更改和删除有关电影的信息。

完成本教程后，你将能够查看类似于此页面的电影列表：

![WebGrid 显示，其中包括设置为 CSS 类名称的参数](displaying-data/_static/image1.png)

但若要开始，必须创建数据库。

## <a name="a-very-brief-introduction-to-databases"></a>数据库简介

本教程仅提供数据库的 briefest 简介。 如果你有数据库经验，则可以跳过此部分。

数据库包含一个或多个表，其中包含 &mdash; 的信息，例如，客户、订单和供应商的表，或者学生、教师、班级和成绩。 从结构上来说，数据库表类似于电子表格。 假设一个典型的通讯簿。 对于通讯簿中的每个条目（即，对于每个人），都有几个信息，如名字、姓氏、地址、电子邮件地址和电话号码。

![作为简单网格的示例数据库表](displaying-data/_static/image2.png)

（行有时称为*记录*，列有时称为*字段*。）

对于大多数数据库表，表必须具有一个包含唯一值（如客户编号、帐号等）的列。 此值称为表的*主键*，你可以使用它来标识表中的每一行。 在此示例中，ID 列是前面示例中所示的通讯簿的主键。

您在 web 应用程序中执行的大部分工作都包含从数据库读取信息，并将信息显示在页面上。 您还将经常收集用户的信息并将其添加到数据库中，或者您将修改数据库中已经存在的记录。 （在本教程集的过程中，我们将介绍所有这些操作。）

数据库工作可能避免它过度，并需要专门的知识。 但对于本教程，你必须仅了解基本概念，这些概念将在你开始时进行说明。

## <a name="creating-a-database"></a>创建数据库

WebMatrix 包含一些工具，使您可以轻松地创建数据库并在数据库中创建表。 （数据库的结构称为数据库的*架构*。）对于本教程集，你将创建一个数据库，该数据库中只有一个表 &mdash; 电影中。

打开 WebMatrix （如果尚未这样做），并打开在上一教程中创建的 WebPagesMovies 站点。

在左窗格中，单击 "**数据库**" 工作区。

![WebMatrix 数据库工作区选项卡](displaying-data/_static/image3.png)

功能区更改为显示与数据库相关的任务。 在功能区中，单击 "**新建数据库**"。

![WebMatrix 功能区中的 "新建数据库" 按钮](displaying-data/_static/image4.png)

WebMatrix 创建一个与你的站点 &mdash; *WebPagesMovies*同名的 SQL Server CE 数据库（ *.sdf*文件）。 （您不需要这样做，但您可以将该文件重命名为您喜欢的任何内容，前提是它具有 *.sdf*扩展名。）

## <a name="creating-a-table"></a>创建表

在功能区中，单击 "**新建表**"。 WebMatrix 在新选项卡中打开表设计器。（如果 "新表" 选项不可用，请确保在左侧树视图中选择了 "新建数据库"。）

![WebMatrix 功能区中的 "新建表" 按钮](displaying-data/_static/image5.png)

在顶部的文本框（其中水印显示 "输入表名称"）中，输入 "电影"。

![在 WebMatrix 数据库设计器中输入表名称](displaying-data/_static/image6.png)

表名下的窗格是定义单个列的位置。 对于本教程中的*电影*表，只需创建几列： *ID*、*标题*、*流派*和*年份*。

在 "**名称**" 框中，输入 "ID"。 此处输入值会激活新列的所有控件。

选择 "**数据类型**" 列表，并选择**int**。此值指定 ID 列将包含整数（数字）数据。

> [!NOTE]
> 我们不会在此处（很多）调用此方法，但你可以使用标准的 Windows 键盘笔势在此网格中导航。 例如，可以在字段之间进行制表符，只需开始键入即可选择列表中的项，依此类推。

选项卡 "超过**默认值**" 框（即将其留空）。 按 Tab**键 "为主键**" 复选框并将其选中。 此选项告知数据库*ID*列将包含标识单个行的数据。 （也就是说，每行在 ID 列中都有一个唯一的值，您可以使用该 ID 列查找该行。）

选择 "**为标识**" 选项。 此选项告知数据库它应该为每个新行自动生成下一个序列号。 （仅当你还选择了 "**是主键**" 选项时，"**为标识**" 选项才起作用。）

单击下一个网格行，或按 Tab 两次以完成当前行。 笔势将保存当前行并启动下一个行。 请注意，"**默认值**" 列现在显示**Null**。 （默认值为 Null，表示为。）

定义完新**ID**列后，设计器将如下图所示：

![为电影表定义 ID 列后，WebMatrix 数据库设计器](displaying-data/_static/image7.png)

若要创建下一列，请单击 "**名称**" 列中的框。 输入列的 "Title"，然后为 "**数据类型**" 值选择 " **nvarchar** "。 **Nvarchar**的 "var" 部分告知数据库，此列的数据将是字符串，其大小可能因记录而异。 （"N" 前缀表示 "国家"，这表示该字段可以保存任何字母或书写系统的字符数据，也就是说，该字段包含 Unicode 数据。）

选择 " **nvarchar**" 时，将显示另一个框，您可以在其中输入字段的最大长度。 输入50，假设要在本教程中使用的电影标题不会超过50个字符。

跳过**默认值**并清除 "**允许 null**值" 选项。 您不希望数据库允许将任何电影输入到没有标题的数据库中。

完成并转到下一行后，设计器将如下图所示：

![定义电影表的 "标题" 列后 WebMatrix 数据库设计器](displaying-data/_static/image8.png)

重复上述步骤以创建名为 "流派" 的列，长度除外，将其设置为 "仅 30"。

创建另一个名为 "Year" 的列。 对于 "数据类型"，请选择 " **nchar** （而非**nvarchar**）"，并将长度设置为4。 对于年份，你将使用如 "1995" 或 "2010" 这样的4位数字，因此你不需要可变大小的列。

完成的设计如下所示：

![为电影表定义所有字段后，WebMatrix 数据库设计器](displaying-data/_static/image9.png)

按 Ctrl + S 或单击快速访问工具栏中的 "**保存**" 按钮。 关闭 "数据库设计器"，关闭该选项卡。

## <a name="adding-some-example-data"></a>添加一些示例数据

在本系列教程的后面部分中，你将创建一个可在表单中输入新电影的页面。 不过，现在可以添加一些示例数据，然后您可以在页面上显示这些数据。

请注意，在 WebMatrix 的 "**数据库**" 工作区中，有一个树显示你之前创建的 *.sdf*文件。 打开新的 *.sdf*文件的节点，然后打开 "**表**" 节点。

![将树打开到电影表格的 WebMatrix 数据库工作区](displaying-data/_static/image10.png)

右键单击 "**电影**" 节点，然后选择 "**数据**"。 WebMatrix 打开一个网格，你可以在其中输入*电影*表的数据：

![WebMatrix 中的数据库输入网格（空）](displaying-data/_static/image11.png)

单击 "**标题**" 列并输入 "当 Harry 满足 Sally 时"。 转到 "**流派**" 列（可以使用 Tab 键），然后输入 "Romantic 喜剧"。 转到**Year**列并输入 "1989"：

![在 WebMatrix 中包含一条记录的数据库输入网格](displaying-data/_static/image12.png)

按 Enter，WebMatrix 保存新电影。 请注意， **ID**列已填充。

![WebMatrix 中的数据库条目网格，其中包含一条记录和自动生成的 ID](displaying-data/_static/image13.png)

输入另一个电影（例如，"不带风"、"Drama"、"1939"）。 ID 列再次填充：

![具有两个记录和自动生成的 Id 的 WebMatrix 中的数据库输入网格](displaying-data/_static/image14.png)

输入第三个电影（例如 "Ghostbusters"、"喜剧"）。 作为实验，将**Year**列保留为空白，然后按 enter。 由于未选择 "**允许 Null 值**" 选项，数据库显示错误：

![如果必需的列值为空，则显示 "无效数据" 错误](displaying-data/_static/image15.png)

单击 **"确定**" 返回并修复该条目（"Ghostbusters" 的年份为1984），然后按 enter。

填写几个电影，直到有8个或如此。 （输入8使稍后可以更轻松地使用分页。 但如果这太多，请只输入几部分。）实际数据并不重要。

![具有任意记录的 WebMatrix 中的数据库条目网格](displaying-data/_static/image16.png)

如果输入了所有电影，但没有出现任何错误，则 ID 值为顺序值。 如果尝试保存未完成的电影记录，则 ID 号可能不是连续的。 如果是这样，那就没关系。 这些数字没有任何固有含义，唯一重要的是，它们在*电影*表中是唯一的。

关闭包含数据库设计器的选项卡。

现在，您可以转到在网页上显示此数据。

## <a name="displaying-data-in-a-page-by-using-the-webgrid-helper"></a>使用 WebGrid Helper 在页中显示数据

若要在页面中显示数据，请使用 `WebGrid` 帮助程序。 此帮助器在网格或表中生成显示（行和列）。 如您所见，您可以通过格式设置和其他功能优化网格。

若要运行网格，必须编写几行代码。 对于您在本教程中执行的几乎所有数据访问，这几个行都将用作一种模式。

> [!NOTE]
> 实际上有许多选项可用于在页面上显示数据;`WebGrid` 帮助程序只是一个。 对于本教程，我们选择了它，因为这是最简单的显示数据的方法，因为它相当灵活。 在下一教程中，你将了解如何使用更多的 "手动" 方法来处理页面中的数据，这使你可以更直接地控制如何显示数据。

在 WebMatrix 的左窗格中，单击 "**文件**" 工作区。

你创建的新数据库位于*应用\_Data*文件夹中。 如果文件夹尚不存在，则 WebMatrix 将为新数据库创建该文件夹。 （如果您以前安装了帮助程序，则可能存在该文件夹。）

在树视图中，选择网站的根目录。 您必须选择网站的根目录;否则，可能会将新文件添加到应用\_Data 文件夹中。

在功能区中，单击 "**新建**"。 在 "**选择文件类型**" 框中，选择 " **CSHTML**"。

在 "**名称**" 框中，将新页面命名为 "电影. cshtml"：

![显示 "电影" 页面的 "选择文件类型" 对话框](displaying-data/_static/image17.png)

单击“确定”按钮。 WebMatrix 打开一个新文件，其中包含某些主干元素。 首先，您将编写一些代码以从数据库中获取数据。 然后，您将向页添加标记以实际显示数据。

### <a name="writing-the-data-query-code"></a>编写数据查询代码

在页面顶部的 "`@{`" 和 "`}`" 字符之间，输入以下代码。 （请确保在左大括号和右大括号之间输入此代码。）

[!code-csharp[Main](displaying-data/samples/sample1.cs)]

第一行打开之前创建的数据库，该数据库始终是执行数据库操作之前的第一个步骤。 通知要打开的数据库 `Database.Open` 方法名称。 请注意，名称中不包含 *.sdf。* `Open` 方法假定它正在查找 *.sdf*文件（即*WebPagesMovies*），并且 *.Sdf*文件位于*应用\_Data*文件夹中。） （如前所述，我们记下*应用\_Data*文件夹，这种情况是 ASP.NET 对该名称进行假设的地方之一。）

打开数据库时，会将对该数据库的引用放入名为 `db`的变量中。 （可将其命名为任意名称。）`db` 变量是结束与数据库的交互的方式。

第二行实际使用 `Query` 方法提取数据库数据。 请注意此代码的工作原理： `db` 变量具有对打开的数据库的引用，并且通过使用 `db` 变量（`db.Query`）调用 `Query` 方法。

查询本身就是 SQL `Select` 语句。 （有关 SQL 的简短背景，请参阅后面的说明。）在语句中，`Movies` 标识要查询的表。 `*` 字符指定查询应返回表中的所有列。 （还可以单独列出列，用逗号分隔。）

查询的结果（如果有）将返回并在 `selectedData` 变量中可用。 同样，该变量可以命名为任意名称。

最后，第三行告诉 ASP.NET 你想要使用 `WebGrid` 帮助器的实例。 您可以使用 `new` 关键字创建（*实例化*） helper 对象，并通过 `selectedData` 变量向其传递查询结果。 新的 `WebGrid` 对象和数据库查询的结果都在 `grid` 变量中可用。 需要一段时间才能实际在页面中显示数据。

在此阶段，数据库已打开，你已获得所需的数据，并且已为该数据准备好 `WebGrid` 帮助程序。 接下来，在页面中创建标记。

> [!TIP] 
> 
> **结构化查询语言 (SQL)**
> 
> SQL 是在大多数关系数据库中用于管理数据库中的数据的一种语言。 它包含的命令可用于检索和更新数据，并允许您创建、修改和管理数据库表中的数据。 SQL 不同于编程语言（例如C#）。 对于 SQL，你会告诉数据库你所需的内容，数据库的工作是确定如何获取数据或执行任务。 下面是一些 SQL 命令的示例和它们的作用：
> 
> `Select * From Movies`
> 
> `SELECT ID, Name, Price FROM Product WHERE Price > 10.00 ORDER BY Name`
> 
> 第一个 `Select` 语句获取 "*电影*" 表中的所有列（由 `*`指定）。
> 
> 第二个 `Select` 语句从*产品*表中的价格列值大于10的记录中提取 ID、名称和价格列。 命令根据 Name 列的值以字母顺序返回结果。 如果没有任何记录与价格条件匹配，则该命令返回空集。
> 
> `INSERT INTO Product (Name, Description, Price) VALUES ('Croissant', 'A flaky delight', 1.99)`
> 
> 此命令在*Product*表中插入一条新记录，将 "名称" 列设置为 "新月形面包"，将 "说明" 列设置为 "a 不可靠感到满意"，并将价格设置为1.99。
> 
> 请注意，在指定非数值时，该值括在单引号（而不是双引号）中，如中C#所示。 用引号将文本或日期值括起来，而不是用引号将其引起来。
> 
> `DELETE FROM Product WHERE ExpirationDate < '01/01/2008'`
> 
> 此命令删除*Product*表中的记录，其到期日期列早于2008年1月1日。 （该命令假定*Product*表具有这样的列。）此处以 MM/DD/YYYY 格式输入日期，但应以用于区域设置的格式输入。
> 
> `Insert` 和 `Delete` 命令不返回结果集。 相反，它们将返回一个数字，该数字告诉你命令所影响的记录数。
> 
> 对于某些操作（例如插入和删除记录），请求操作的进程必须在数据库中具有适当的权限。 这就是为什么在连接到数据库时，生产数据库经常必须提供用户名和密码。
> 
> 有许多 SQL 命令，但它们都遵循您在此处看到的命令。 您可以使用 SQL 命令来创建数据库表，计算表中的记录数，计算价格，以及执行更多操作。

### <a name="adding-markup-to-display-the-data"></a>添加标记以显示数据

在 `<head>` 元素中，将 `<title>` 元素的内容设置为 "影片"：

[!code-html[Main](displaying-data/samples/sample2.html?highlight=3)]

在页面的 `<body>` 元素中，添加以下内容：

[!code-html[Main](displaying-data/samples/sample3.html)]

介绍完毕。 `grid` 变量是在前面的代码中创建 `WebGrid` 对象时创建的值。

在 WebMatrix 树视图中，右键单击页面并选择 "**在浏览器中启动"** 。 你将看到类似于此页面的内容：

![电影表中的默认 WebGrid helper 输出](displaying-data/_static/image18.png)

单击列标题链接可按该列进行排序。 通过单击标题，就是**WebGrid**帮助程序中内置的一项功能。

如名称所示，`GetHtml` 方法会生成显示数据的标记。 默认情况下，`GetHtml` 方法会生成 HTML `<table>` 元素。 （如果需要，可以通过在浏览器中查看页面源来验证呈现。）

## <a name="modifying-the-look-of-the-grid"></a>修改网格的外观

像您一样使用 `WebGrid` 帮助程序非常简单，但生成的显示是普通的。 `WebGrid` 帮助程序具有各种选项，可用于控制数据的显示方式。 本教程中的内容太多，但本部分介绍其中一些选项。 本系列后面的教程将介绍一些其他选项。

### <a name="specifying-individual-columns-to-display"></a>指定要显示的单个列

若要开始，可以指定只显示某些列。 默认情况下，正如您所看到的，该网格显示了*电影*表中的所有四个列。

在 "*影院*" 文件中，将刚才添加的 `@grid.GetHtml()` 标记替换为以下内容：

[!code-css[Main](displaying-data/samples/sample4.css)]

若要告知帮助器显示哪些列，请为 `GetHtml` 方法包含 `columns` 参数，并传入一组列。 在集合中，指定要包含的每一列。 您可以通过包含 `grid.Column` 对象来指定要显示的单个列，并传入所需的数据列的名称。 （这些列必须包括在 SQL 查询结果中— `WebGrid` 帮助程序不能显示查询未返回的列。）

再次在浏览器中启动 "在浏览器中显示 *" 页面，* 此时会显示如下所示的显示内容（请注意，未显示 ID 列）：

![仅显示所选列的 WebGrid 显示](displaying-data/_static/image19.png)

### <a name="changing-the-look-of-the-grid"></a>更改网格的外观

还有其他几个选项可用于显示列，其中一些选项将在本集中的后续教程中进行探讨。 现在，本部分将介绍如何将网格作为一个整体进行样式。

在页面的 `<head>` 部分中，紧靠在关闭 `</head>` 标记之前，添加以下 `<style>` 元素：

[!code-css[Main](displaying-data/samples/sample5.css)]

此 CSS 标记定义名为 `grid`、`head`等的类。 你还可以将这些样式定义放在单独的 *.css*文件中，并将其链接到该页。 （事实上，您将在本教程的后面部分执行此操作。）但为了简化本教程，它们位于显示数据的同一页面中。

现在，可以获取 `WebGrid` 帮助器来使用这些样式类。 帮助器有许多属性（例如 `tableStyle`），只是为了实现此目的，即向它们分配一个 CSS 样式类名称，并且该类名称呈现为帮助器呈现的标记的一部分。

更改 `grid.GetHtml` 标记，使其现在类似于以下代码：

[!code-css[Main](displaying-data/samples/sample6.css)]

新增功能是你已将 `tableStyle`、`headerStyle`和 `alternatingRowStyle` 参数添加到 `GetHtml` 方法。 已将这些参数设置为稍后添加的 CSS 样式的名称。

运行该页面，此时你会看到一个看起来比之前更简单的网格：

![WebGrid 显示，其中包括设置为 CSS 类名称的参数](displaying-data/_static/image20.png)

若要查看 `GetHtml` 方法的生成内容，可以在浏览器中查看页面的源。 本文不会详细介绍，但重要的一点是，通过指定 `tableStyle`的参数，导致网格生成如下所示的 HTML 标记：

`<table class="grid">`

`<table>` 标记添加了一个 `class` 属性，该属性引用前面添加的其中一个 CSS 规则。 此代码显示了基本模式 &mdash; 不同的 `GetHtml` 方法参数可让你引用该方法随后随标记一起生成的 CSS 类。 CSS 类的作用由您决定。

## <a name="adding-paging"></a>添加分页

作为本教程的最后一个任务，您将向网格中添加分页。 现在，不会出现一次显示所有电影的问题。 但如果添加了数百个电影，则页面显示将变长。

在页代码中，将创建 `WebGrid` 对象的行更改为以下代码：

[!code-csharp[Main](displaying-data/samples/sample7.cs)]

与之前的唯一区别在于，你添加了一个设置为3的 `rowsPerPage` 参数。

运行页面。 网格每次显示3行，还显示允许您在数据库中浏览电影的导航链接：

![分页显示 WebGrid](displaying-data/_static/image21.png)

## <a name="coming-up-next"></a>下一步

在下一教程中，您将学习如何使用 Razor 和C#代码来获取窗体中的用户输入。 将搜索框添加到 "电影" 页，以便可以按标题或流派查找电影。

## <a name="complete-listing-for-movies-page"></a>"完成电影列表" 页面

[!code-cshtml[Main](displaying-data/samples/sample8.cshtml)]

## <a name="additional-resources"></a>其他资源

- [使用 Razor 语法的 ASP.NET Web 编程简介](https://go.microsoft.com/fwlink/?LinkID=202890)

> [!div class="step-by-step"]
> [上一页](intro-to-web-pages-programming.md)
> [下一页](form-basics.md)
