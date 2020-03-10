---
uid: web-forms/overview/data-access/advanced-data-access-scenarios/debugging-stored-procedures-cs
title: 调试存储过程（C#） |Microsoft Docs
author: rick-anderson
description: Visual Studio Professional 和 Team System 版本允许您在 SQL Server 中设置断点并单步执行存储过程，从而调试存储 。
ms.author: riande
ms.date: 08/03/2007
ms.assetid: c655c324-2ffa-4c21-8265-a254d79a693d
msc.legacyurl: /web-forms/overview/data-access/advanced-data-access-scenarios/debugging-stored-procedures-cs
msc.type: authoredcontent
ms.openlocfilehash: 12a8500b107345b9cc9ab457016fdef09ca1bb9d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78428390"
---
# <a name="debugging-stored-procedures-c"></a>调试存储过程 (C#)

作者： [Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载代码](https://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_74_CS.zip)或[下载 PDF](debugging-stored-procedures-cs/_static/datatutorial74cs1.pdf)

> Visual Studio Professional 和 Team System 版本允许您在 SQL Server 中设置断点并单步执行存储过程，从而使调试存储过程与调试应用程序代码一样简单。 本教程演示了存储过程的直接数据库调试和应用程序调试。

## <a name="introduction"></a>简介

Visual Studio 提供丰富的调试体验。 使用几个击键或单击鼠标，就可以使用断点来停止程序的执行并检查其状态和控制流。 除了调试应用程序代码，Visual Studio 还支持在 SQL Server 中调试存储过程。 与可以在 ASP.NET 代码隐藏类或业务逻辑层类的代码中设置断点一样，它们也可以放在存储过程中。

在本教程中，我们将介绍如何从 Visual Studio 中的服务器资源管理器单步执行存储过程，以及如何设置从运行 ASP.NET 应用程序调用存储过程时命中的断点。

> [!NOTE]
> 遗憾的是，存储过程只能通过 Visual Studio 的专业版和团队系统版本来进入和调试。 如果你正在使用 Visual Web Developer 或 Visual Studio 的标准版本，则欢迎你在完成调试存储过程时所需的步骤，但无法在计算机上复制这些步骤。

## <a name="sql-server-debugging-concepts"></a>SQL Server 调试概念

Microsoft SQL Server 2005 旨在提供与[公共语言运行时（CLR）](https://msdn.microsoft.com/netframework/aa497266.aspx)的集成，这是所有 .net 程序集所使用的运行时。 因此，SQL Server 2005 支持托管数据库对象。 也就是说，你可以创建诸如存储过程和用户定义的函数（Udf）之类的C#数据库对象作为类中的方法。 这使得这些存储过程和 Udf 能够利用 .NET Framework 中的功能以及您自己的自定义类中的功能。 当然，SQL Server 2005 还提供对 T-sql 数据库对象的支持。

SQL Server 2005 为 T-sql 和托管数据库对象提供调试支持。 但是，这些对象只能通过 Visual Studio 2005 Professional 和 Team Systems 版本进行调试。 在本教程中，我们将检查 SQL T-sql 数据库对象。 后续教程介绍了如何调试托管数据库对象。

[SQL Server 2005 CLR 集成团队](https://blogs.msdn.com/sqlclr/default.aspx) [SQL Server 2005 博客文章中的 T-sql 和 CLR 调试概述](https://blogs.msdn.com/sqlclr/archive/2006/06/29/651644.aspx)介绍了从 Visual Studio 调试 SQL Server 2005 对象的三种方法：

- **直接数据库调试（DDD）** -从服务器资源管理器可以单步执行任何 t-sql 数据库对象，如存储过程和 udf。 我们将在步骤1中检查 DDD。
- **应用程序调试**-可以在数据库对象中设置断点，然后运行我们的 ASP.NET 应用程序。 当执行数据库对象时，断点将被命中并控制转换为调试器。 请注意，使用应用程序调试时，无法从应用程序代码单步执行数据库对象。 我们必须在要停止调试器的存储过程或 Udf 中显式设置断点。 从步骤2开始检查应用程序调试。
- **从 SQL Server 项目**-Visual Studio Professional 和 Team Systems 版本进行调试时，包括一个通常用于创建托管数据库对象的 SQL Server 项目类型。 下一教程将介绍如何使用 SQL Server 项目和调试其内容。

Visual Studio 可以在本地和远程 SQL Server 实例上调试存储过程。 本地 SQL Server 实例是安装在与 Visual Studio 相同的计算机上的实例。 如果正在使用的 SQL Server 数据库不位于开发计算机上，则将其视为远程实例。 对于这些教程，我们使用了本地 SQL Server 实例。 与在本地实例上调试存储过程相比，调试远程 SQL server 实例上的存储过程需要更多的配置步骤。

如果你使用的是本地 SQL Server 实例，则可以从步骤1开始，然后完成本教程。 但是，如果您使用的是远程 SQL Server 实例，则首先需要确保在调试时将使用 Windows 用户帐户登录到您的开发计算机，该帐户在远程实例上具有 SQL Server 登录名。 此外，此数据库登录名和用于从正在运行的 ASP.NET 应用程序连接到数据库的数据库登录名都必须是 `sysadmin` 角色的成员。 有关将 Visual Studio 和 SQL Server 配置为调试远程实例的详细信息，请参阅本教程末尾的 "调试 T-sql 数据库对象" 部分。

最后，请了解对 T-sql 数据库对象的调试支持并不像功能丰富，因为调试支持 .NET 应用程序。 例如，断点条件和筛选器不受支持，仅调试窗口的一部分可用，不能使用 "编辑并继续"，"即时" 窗口呈现为无用窗口，依此类推。 有关详细信息，请参阅[调试程序命令和功能的限制](https://msdn.microsoft.com/library/ms165035(VS.80).aspx)。

## <a name="step-1-directly-stepping-into-a-stored-procedure"></a>步骤1：直接单步执行存储过程

使用 Visual Studio 可以轻松地直接调试数据库对象。 让我们看看如何使用直接数据库调试（DDD）功能单步执行 Northwind 数据库中的 `Products_SelectByCategoryID` 存储过程。 顾名思义，`Products_SelectByCategoryID` 返回特定类别的产品信息;它是在[使用类型化数据集的 tableadapter 教程的现有存储过程](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs.md)中创建的。 首先转到 "服务器资源管理器"，然后展开 Northwind 数据库节点。 接下来，向下钻取到 "存储过程" 文件夹，右键单击 `Products_SelectByCategoryID` 存储过程，然后从上下文菜单中选择 "单步执行存储过程" 选项。 这会启动调试器。

由于 `Products_SelectByCategoryID` 存储过程需要一个 `@CategoryID` 输入参数，因此系统会要求提供此值。 输入1，这将返回有关饮料的信息。

![将值1用于 @CategoryID 参数](debugging-stored-procedures-cs/_static/image1.png)

**图 1**：将值1用于 `@CategoryID` 参数

为 `@CategoryID` 参数提供值后，将执行存储过程。 尽管调试器在第一条语句上暂停执行，但并不是运行到完成。 记下边距中的黄色箭头，指示存储过程中的当前位置。 可以通过监视窗口或通过将鼠标悬停在存储过程中的参数名称上来查看和编辑参数值。

[![调试程序在存储过程的第一条语句上暂停](debugging-stored-procedures-cs/_static/image3.png)](debugging-stored-procedures-cs/_static/image2.png)

**图 2**：调试器在存储过程的第一条语句上暂停（[单击查看完全大小的图像](debugging-stored-procedures-cs/_static/image4.png)）

若要逐语句单步执行存储过程，请单击工具栏中的 "逐过程" 按钮或按 F10 键。 `Products_SelectByCategoryID` 存储过程包含单个 `SELECT` 语句，因此按 F10 将逐语句执行该语句并完成存储过程的执行。 存储过程完成后，其输出将显示在 "输出" 窗口中，并且调试器将终止。

> [!NOTE]
> T-sql 调试在语句级别进行;不能单步执行 `SELECT` 语句。

## <a name="step-2-configuring-the-website-for-application-debugging"></a>步骤2：配置网站以进行应用程序调试

直接从服务器资源管理器调试存储过程很方便，在许多情况下，当从 ASP.NET 应用程序调用存储过程时，我们对调试该存储过程有更多的兴趣。 我们可以在 Visual Studio 中向存储过程添加断点，然后开始调试 ASP.NET 应用程序。 当从应用程序调用带有断点的存储过程时，执行将在断点处暂停，并且我们可以查看和更改存储过程的参数值，并单步执行语句，就像我们在步骤1中执行的操作一样。

在开始调试从应用程序调用的存储过程之前，我们需要指示 ASP.NET web 应用程序与 SQL Server 调试器集成。 首先右键单击解决方案资源管理器（`ASPNET_Data_Tutorial_74_CS`）中的网站名称。 从上下文菜单中选择 "属性页" 选项，在左侧选择 "启动选项" 项，并选中 "调试器" 部分中的 "SQL Server" 复选框（请参阅图3）。

[![选中 "应用程序" 属性页中的 SQL Server 复选框](debugging-stored-procedures-cs/_static/image6.png)](debugging-stored-procedures-cs/_static/image5.png)

**图 3**：选中 "应用程序" 属性页中的 "SQL Server" 复选框（[单击查看完全大小的图像](debugging-stored-procedures-cs/_static/image7.png)）

此外，我们还需要更新应用程序使用的数据库连接字符串，以便禁用连接池。 关闭与数据库的连接时，相应的 `SqlConnection` 对象将被置于可用连接池中。 建立与数据库的连接时，可从此池中检索可用连接对象，而不必创建和建立新连接。 这种连接对象池是一种性能增强功能，并在默认情况下启用。 但是，当调试时，我们希望关闭连接池，因为在使用从池中获取的连接时无法正确重新建立调试基础结构。

若要禁用连接池，请更新 `Web.config` 中的 `NORTHWNDConnectionString`，使其包括 `Pooling=false` 设置。

[!code-xml[Main](debugging-stored-procedures-cs/samples/sample1.xml)]

> [!NOTE]
> 通过 ASP.NET 应用程序完成调试 SQL Server，请通过从连接字符串中删除 `Pooling` 设置（或将其设置为 `Pooling=true`）来确保恢复连接池。

此时，ASP.NET 应用程序已配置为允许 Visual Studio 在通过 web 应用程序调用 SQL Server 数据库对象时对其进行调试。 现在剩下的就是向存储过程添加断点并开始调试！

## <a name="step-3-adding-a-breakpoint-and-debugging"></a>步骤3：添加断点和调试

打开 `Products_SelectByCategoryID` 存储过程，然后在 `SELECT` 语句开头处，单击相应位置处的边距设置断点，或将光标置于 `SELECT` 语句的开头，并按 F9。 如图4所示，断点在边距中显示为红色圆圈。

[![在 Products_SelectByCategoryID 存储过程中设置断点](debugging-stored-procedures-cs/_static/image9.png)](debugging-stored-procedures-cs/_static/image8.png)

**图 4**：在 `Products_SelectByCategoryID` 存储过程中设置断点（[单击以查看完全大小的图像](debugging-stored-procedures-cs/_static/image10.png)）

为了使 SQL 数据库对象可以通过客户端应用程序进行调试，必须将数据库配置为支持应用程序调试。 首次设置断点时，应自动打开此设置，但应仔细检查此设置。 右键单击服务器资源管理器中的 "`NORTHWND.MDF`" 节点。 上下文菜单应包括名为 "应用程序调试" 的选中菜单项。

![确保启用了 "应用程序调试" 选项](debugging-stored-procedures-cs/_static/image11.png)

**图 5**：确保启用了 "应用程序调试" 选项

启用断点并启用应用程序调试选项后，便可以在从 ASP.NET 应用程序调用时调试存储过程。 转到 "调试" 菜单，选择 "启动调试"，通过按 F5 或单击工具栏中的绿色播放图标来启动调试器。 这会启动调试器并启动该网站。

`Products_SelectByCategoryID` 存储过程是在[使用类型化数据集的 tableadapter 教程的现有存储过程](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs.md)中创建的。 其对应的网页（`~/AdvancedDAL/ExistingSprocs.aspx`）包含一个显示此存储过程返回的结果的 GridView。 通过浏览器访问此页。 到达页面后，将命中 `Products_SelectByCategoryID` 存储过程中的断点，并将控制权返回给 Visual Studio。 就像在步骤1中一样，可以单步执行存储过程语句并查看和修改参数值。

[![ExistingSprocs 页面最初显示饮料](debugging-stored-procedures-cs/_static/image13.png)](debugging-stored-procedures-cs/_static/image12.png)

**图 6**： "`ExistingSprocs.aspx`" 页最初显示饮料（[单击以查看完全大小的图像](debugging-stored-procedures-cs/_static/image14.png)）

[已达到存储过程的断点 ![](debugging-stored-procedures-cs/_static/image16.png)](debugging-stored-procedures-cs/_static/image15.png)

**图 7**：已达到存储过程的断点（[单击以查看完全大小的映像](debugging-stored-procedures-cs/_static/image17.png)）

如图7所示的监视窗口，`@CategoryID` 参数的值为1。 这是因为 `ExistingSprocs.aspx` 页最初显示饮料类别中的产品，其 `CategoryID` 值为1。 从下拉列表中选择一个不同的类别。 这样做会导致回发并重新执行 `Products_SelectByCategoryID` 存储过程。 再次命中断点，但这次 `@CategoryID` 参数 s 值将反映所选的下拉列表项 `CategoryID`。

[![从下拉列表中选择其他类别](debugging-stored-procedures-cs/_static/image19.png)](debugging-stored-procedures-cs/_static/image18.png)

**图 8**：从下拉列表中选择其他类别（[单击以查看完全大小的图像](debugging-stored-procedures-cs/_static/image20.png)）

[![@CategoryID 参数反映从网页中选择的类别](debugging-stored-procedures-cs/_static/image22.png)](debugging-stored-procedures-cs/_static/image21.png)

**图 9**： `@CategoryID` 参数反映了从网页中选择的类别（[单击以查看完全大小的图像](debugging-stored-procedures-cs/_static/image23.png)）

> [!NOTE]
> 如果在访问 "`ExistingSprocs.aspx`" 页时未命中 `Products_SelectByCategoryID` 存储过程中的断点，请确保已在 ASP.NET 应用程序的 "属性" 页的 "调试器" 部分中选中 "SQL Server" 复选框，该连接池已禁用，并且已启用 "数据库 s 应用程序调试" 选项。 如果仍然遇到问题，请重新启动 Visual Studio 并重试。

## <a name="debugging-t-sql-database-objects-on-remote-instances"></a>调试远程实例上的 T-sql 数据库对象

当 SQL Server 数据库实例与 Visual Studio 位于同一台计算机上时，通过 Visual Studio 调试数据库对象非常简单。 但是，如果 SQL Server 和 Visual Studio 驻留在不同的计算机上，则需要进行一些仔细的配置才能使一切正常运行。 我们面临两个核心任务：

- 确保用于通过 ADO.NET 连接到数据库的登录名属于 `sysadmin` 角色。
- 确保开发计算机上的 Visual Studio 所用的 Windows 用户帐户是属于 `sysadmin` 角色的有效 SQL Server 登录帐户。

第一步相对简单。 首先，确定用于从 ASP.NET 应用程序连接到数据库的用户帐户，然后从 SQL Server Management Studio 中，将该登录帐户添加到 `sysadmin` 角色。

第二个任务要求用于调试应用程序的 Windows 用户帐户是远程数据库中的有效登录名。 但是，你登录到工作站的 Windows 帐户很可能是 SQL Server 上的有效登录。 更好的选择是将一些 Windows 用户帐户指定为 SQL Server 调试帐户，而不是将您的特定登录帐户添加到 SQL Server。 然后，若要调试远程 SQL Server 实例的数据库对象，请使用该 Windows 登录帐户的凭据运行 Visual Studio。

示例应有助于澄清问题。 假设在 Windows 域中有一个名为 `SQLDebug` 的 Windows 帐户。 需要将此帐户作为有效登录名添加到远程 SQL Server 实例，并作为 `sysadmin` 角色的成员添加。 然后，若要从 Visual Studio 调试远程 SQL Server 实例，需要以 `SQLDebug` 用户身份运行 Visual Studio。 这可以通过以下方式完成：从工作站注销，以 `SQLDebug`登录并启动 Visual Studio，但更简单的方法是使用自己的凭据登录到工作站，然后使用 `runas.exe` 以 `SQLDebug` 用户身份启动 Visual Studio。 `runas.exe` 允许在不同用户帐户的借助下执行特定的应用程序。 若要将 Visual Studio 作为 `SQLDebug`启动，可以在命令行中输入以下语句：

[!code-console[Main](debugging-stored-procedures-cs/samples/sample2.cmd)]

有关此过程的更详细说明，请参阅 Visual Studio 的[William Vaughn](http://betav.com/BLOG/billva/) s *Hitchhiker 和 SQL Server 第7版，* 以及[如何：设置 SQL Server 调试权限](https://msdn.microsoft.com/library/w1bhybwz(VS.80).aspx)。

> [!NOTE]
> 如果开发计算机运行的是 Windows XP Service Pack 2，则需要配置 Internet 连接防火墙以允许远程调试。 How [To： Enable SQL Server 2005 调试](https://msdn.microsoft.com/library/s0fk6z6e(VS.80).aspx)文章说明这涉及两个步骤：（a）在 Visual Studio 主机上，必须将 `Devenv.exe` 添加到 "例外" 列表中并打开 TCP 135 端口;在远程（SQL）计算机上，必须打开 TCP 135 端口并将 `sqlservr.exe` 添加到 "例外" 列表中。 如果域策略要求通过 IPSec 进行网络通信，则必须打开 UDP 4500 和 UDP 500 端口。

## <a name="summary"></a>摘要

除了提供对 .NET 应用程序代码的调试支持之外，Visual Studio 还提供了用于 SQL Server 2005 的各种调试选项。 在本教程中，我们讨论了两个选项：直接数据库调试和应用程序调试。 若要直接调试 T-sql 数据库对象，请通过服务器资源管理器找到对象，然后右键单击该对象并选择 "单步执行"。 这会启动调试器并在数据库对象中的第一个语句处暂停，此时可以单步执行对象的语句并查看和修改参数值。 在步骤1中，我们使用此方法单步执行 `Products_SelectByCategoryID` 存储过程。

应用程序调试允许直接在数据库对象中设置断点。 当从客户端应用程序（例如 ASP.NET web 应用程序）调用带有断点的数据库对象时，该程序会在调试器接管时停止。 应用程序调试非常有用，因为它更清晰地显示了哪些应用程序操作会导致调用特定的数据库对象。 但是，它需要比直接数据库调试更多的配置和设置。

还可以通过 SQL Server 项目来调试数据库对象。 在下一教程中，我们将介绍如何使用 SQL Server 项目以及如何使用它们来创建和调试托管数据库对象。

很高兴编程！

## <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，创始人的[4GuysFromRolla.com](http://www.4guysfromrolla.com)，已在使用 Microsoft Web 技术，自1998开始。 Scott 的工作方式是独立的顾问、培训师和撰稿人。 他的最新书籍是，[*在24小时内，sam ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 可以[mitchell@4GuysFromRolla.com访问。](mailto:mitchell@4GuysFromRolla.com) 或通过他的博客，可以在[http://ScottOnWriting.NET](http://ScottOnWriting.NET)找到。

> [!div class="step-by-step"]
> [上一页](protecting-connection-strings-and-other-configuration-information-cs.md)
> [下一页](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs.md)
