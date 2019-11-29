---
uid: web-forms/overview/older-versions-getting-started/deploying-web-site-projects/deploying-a-database-cs
title: 部署数据库（C#） |Microsoft Docs
author: rick-anderson
description: 部署 ASP.NET web 应用程序需要从开发环境到生产环境中获取必要的文件和资源。 对于 da 。
ms.author: riande
ms.date: 04/23/2009
ms.assetid: ff537a10-9f1f-43fe-9bcb-3dda161ba8f5
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deploying-web-site-projects/deploying-a-database-cs
msc.type: authoredcontent
ms.openlocfilehash: 83657be794e1ea31f6ad2f2b4adc274724d60cf2
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74579914"
---
# <a name="deploying-a-database-c"></a>部署数据库 (C#)

作者： [Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载代码](https://download.microsoft.com/download/E/6/F/E6FE3A1F-EE3A-4119-989A-33D1A9F6F6DD/ASPNET_Hosting_Tutorial_07_CS.zip)或[下载 PDF](https://download.microsoft.com/download/C/3/9/C391A649-B357-4A7B-BAA4-48C96871FEA6/aspnet_tutorial07_DeployDB_cs.pdf)

> 部署 ASP.NET web 应用程序需要从开发环境到生产环境中获取必要的文件和资源。 对于数据驱动的 web 应用程序，这包括数据库架构和数据。 本教程是一个系列教程中的第一个教程，其中介绍了成功将数据库从开发环境部署到生产环境所需的步骤。

## <a name="introduction"></a>简介

部署 ASP.NET web 应用程序需要从开发环境到生产环境中获取必要的文件和资源。 在过去六个教程中，我们介绍了如何部署简单的书籍评论 web 应用程序。 此演示网站由多个服务器端资源（ASP.NET 页面、配置文件、`Web.sitemap` 文件等）以及客户端资源（如图像和 CSS 文件）组成。 但数据驱动的 web 应用程序呢？ 部署使用数据库的 web 应用程序时必须采取哪些额外步骤？

在接下来的几个教程中，我们将介绍部署数据驱动的 web 应用程序所需的步骤。 本教程首先检查如何从开发环境将数据库的架构和内容获取到生产环境中，而后续教程将介绍所需的配置更改。 接下来，我们将探讨部署使用应用程序服务（成员资格、角色、配置文件等）的数据库的挑战。

## <a name="examining-the-updated-book-reviews-web-application"></a>检查更新的书籍评审 Web 应用程序

为了演示如何部署数据驱动的 web 应用程序，我已将一项简单的静态网站中的 web 应用程序更新到数据驱动的 web 应用程序。 与之前一样，本教程中有两个版本的应用程序下载：一个使用 Web 应用程序项目模型，另一个使用网站项目模型。

更新的书籍检查 web 应用程序使用[SQL Server 2008 Express Edition](https://www.microsoft.com/express/sql/default.aspx)数据库，该数据库存储在站点 s `App_Data` 文件夹（`~/App_Data/Reviews.mdf`）中。 如果在计算机上安装了 SQL Server 2008，则演示应运行且不出错。 如果你使用的是较旧版本的 SQL Server 你可以安装免费的 SQL Server 2008 Express Edition，也可以使用本教程的下载中提供的数据库脚本自行创建数据库。

`Reviews.mdf` 数据库包含四个表：

- `Genres`-为每个流派包括一条记录，如技术、小说和商务。
- `Books`-对于每个评审都包含一条记录，其中的列如 `Title`、`GenreId`、`ReviewDate`和 `Review`等。
- `Authors`-包含有关参与评审书籍的每个作者的信息。
- `BooksAuthors`-多对多联接表，用于指定作者编写了哪些书籍。

图1显示了这四个表的 ER 关系图。

[![书籍审阅 Web 应用程序数据库由四个表组成](deploying-a-database-cs/_static/image2.jpg)](deploying-a-database-cs/_static/image1.jpg) 

**图 1**：书籍回顾 Web 应用程序数据库由四个表组成（[单击以查看完全大小的图像](deploying-a-database-cs/_static/image3.jpg)）

前一版本的书籍评论网站为每本书提供了一个单独的 ASP.NET 页面。 例如，存在一个名为 `~/Tech/TYASP35.aspx` 的页，其中包含用于*在24小时内讲授自己 ASP.NET 3.5*的评审。 该网站的这一新的数据驱动版本包含存储在数据库中的审阅，以及一个 ASP.NET？ ID =*bookId*，用于显示指定书的评审。 同样，还会有一个 "*genreId* " 页，其中列出了指定流派中审阅的书籍。

图2和3显示了操作中的 `Genre.aspx` 和 `Review.aspx` 页面。 请注意每个页面的地址栏中的 URL。 在图2中，它是 "85d164ba-1123-4c47-82a0-c8ec75de7e0e"。 由于85d164ba-1123-4c47-82a0-c8ec75de7e0e 是技术流派的 `GenreId` 值，因此页面的标题将显示 "技术审阅"，而项目符号列表则会在此流派下的站点上枚举这些评审。

[![技术流派页面](deploying-a-database-cs/_static/image5.jpg)](deploying-a-database-cs/_static/image4.jpg) 

**图 2**：技术流派页面（[单击以查看完全尺寸的图像](deploying-a-database-cs/_static/image6.jpg)）

[![在24小时内讲授 ASP.NET 3.5 的评论](deploying-a-database-cs/_static/image8.jpg)](deploying-a-database-cs/_static/image7.jpg) 

**图 3**：*在24小时内讲授 ASP.NET 3.5*的评论（[单击查看全尺寸图像](deploying-a-database-cs/_static/image9.jpg)）

书籍评论 web 应用程序还包括管理部分，管理员可以在其中添加、编辑和删除流派、评论和作者信息。 目前，任何访问者都可以访问管理部分。 在将来的教程中，我们将为用户帐户添加支持，并仅允许授权用户进入 "管理" 页。

如果下载书籍评论应用程序，请记住，其目的是演示如何部署数据驱动的应用程序。 这并不像应用程序设计那样表现最佳做法。 例如，没有单独的数据访问层（DAL）;ASP.NET 页面通过其代码隐藏类中的 SqlDataSource 控件或 ADO.NET 代码直接与数据库进行通信。 若要深入了解如何使用分层体系结构创建数据驱动的应用程序，请参阅使用[*数据*教程](../../data-access/index.md)。

## <a name="databases-on-development-versus-production"></a>开发数据库与生产环境

当你开始在数据驱动的 web 应用程序上进行开发时，必须指定一个数据库连接字符串，该字符串提供有关如何连接到数据库的应用程序详细信息。 此连接字符串指定数据库服务器、数据库名称和安全信息。 大多数情况下，应用程序在开发期间使用的数据库与生产环境中使用的数据库不同。 使用不同的数据库进行开发与生产有很多好处。 如果在开发中使用其他数据库，就不必担心意外修改或删除实时数据。 它还允许你将虚拟测试数据放入虚拟测试数据或对数据模型进行重大更改，无需担心对应用程序在生产中的影响。 在开发和生产环境中具有不同数据库的缺点在于，在部署应用程序时，还必须部署数据库架构或数据的任何相关更改。

在第一次部署之前，只有数据库的一个实例，并且该实例位于开发环境中。 首次将应用程序部署到生产环境时，我们不仅必须复制必需的服务器端文件和客户端文件，还必须将数据库从开发环境复制到生产环境。 这就是我们目前所处的书籍回顾 web 应用程序的地方，数据库驻留在开发环境中的 `App_Data` 文件夹中，但尚未推送到生产环境。

部署应用程序后，会有两个数据库副本。 随着应用程序的成熟，可以添加新的功能，使得对数据模型的更改（例如，将新列添加到现有表、更改现有列、添加新表等）。 下一次部署 web 应用程序后，必须将更改应用到自上一次部署后开发环境中的数据库。 将来的教程中讨论了用于管理此过程的某些策略。 本教程重点介绍如何将整个数据库从开发环境部署到生产环境。

## <a name="deploying-the-database-to-the-production-environment"></a>将数据库部署到生产环境

本教程的其余部分介绍如何将数据库从开发环境部署到生产环境。 如果你要继续，请确保你的 web 主机提供商的帐户包含 Microsoft SQL Server 数据库支持。 还需要有一些信息，即数据库服务器名称、数据库名称，以及用于连接到数据库的用户名和密码。

如本教程前面所述，书籍检查网站的数据库是存储在 `App_Data` 文件夹中 SQL Server 2008 Express Edition 数据库。 部署此类数据库的原因与将 `App_Data` 文件夹从开发环境复制到生产环境一样简单。 但出于安全方面的考虑，大多数 web 宿主提供程序不支持在 `App_Data` 文件夹中承载数据库。 相反，web 主机会在其环境中的 SQL Server 数据库服务器上提供帐户。 若要将数据库从开发环境部署到生产环境，需要在 web 主机的数据库服务器上注册数据库。

那么，如何将数据库从开发环境转到生产环境呢？ 有几种方法可以完成此操作，具体取决于 web 主机提供的服务。 在某些主机（如 DiscountASP.NET）中，你可以将数据库或实际 `.mdf` 文件的备份 FTP 到你的网站，然后，从 "控制面板" 中还原备份文件或将 `.mdf` 文件附加到 SQL Server 数据库服务器。 利用此类工具，可以轻松地将 `App_Data` 文件夹复制到生产环境，然后通过控制面板附加该数据库。 这可能是首次发布数据库的最简单、最快捷的方式。

另一种方法是使用 "数据库发布向导"。 "数据库发布向导" 是一个 Windows 桌面应用程序，它将生成用于创建数据库架构的 SQL 命令（表、存储过程、视图、用户定义函数等），以及（可选）表中的数据。 然后，可以通过 SQL Server Management Studio 连接到 web 主机提供程序的数据库服务器，然后执行此脚本以在生产环境中复制数据库。 更好的是，如果您的 web 主机提供商支持 Microsoft[数据库发布服务](http://www.codeplex.com/sqlhost/Wiki/View.aspx?title=Database%20Publishing%20Services&amp;referringTitle=Home)，则您可以让 "数据库发布向导" 生成的脚本以您的身份自动在数据库服务器上执行。 由于 "数据库发布向导" 生成的脚本将创建数据库的架构和数据，因此无论 web 宿主提供程序是否提供附加已上传 `.mdf` 文件之类的功能，它都有效。

### <a name="generating-the-sql-commands-to-create-the-database-schema-and-data-using-the-database-publishing-wizard"></a>使用数据库发布向导生成用于创建数据库架构和数据的 SQL 命令

让我们逐步介绍如何使用数据库发布向导将书籍检查数据库部署到生产环境。 如果使用的是 Visual Studio 2008 或更高版本，则已安装 "数据库发布向导"。 如果你使用的是 Visual Studio 2005，你将需要先[下载并安装](https://www.microsoft.com/downloads/details.aspx?familyid=56E5B1C5-BF17-42E0-A410-371A838E570A&amp;displaylang=en)该向导。

打开 Visual Studio，然后导航到 `Reviews.mdf` 数据库。 如果你正在使用 Visual Web Developer，请前往数据库资源管理器;如果使用的是 Visual Studio，请使用服务器资源管理器。 图4显示了 Visual Web Developer 数据库资源管理器中的 `Reviews.mdf` 数据库。 如图4所示，`Reviews.mdf` 数据库由四个表组成，三个存储过程和用户定义函数组成。

[![在数据库资源管理器或服务器资源管理器中查找数据库](deploying-a-database-cs/_static/image11.jpg)](deploying-a-database-cs/_static/image10.jpg) 

**图 4**：在数据库资源管理器或服务器资源管理器中找到数据库（[单击查看完全大小的映像](deploying-a-database-cs/_static/image12.jpg)）

右键单击数据库名称，并从上下文菜单中选择 "发布到提供程序" 选项。 这将启动数据库发布向导（见图5）。 单击 "下一步" 以提前越过初始屏幕。

[![数据库发布向导初始屏幕](deploying-a-database-cs/_static/image14.jpg)](deploying-a-database-cs/_static/image13.jpg) 

**图 5**：数据库发布向导初始屏幕（[单击以查看完全大小的图像](deploying-a-database-cs/_static/image15.jpg)）

向导中的第二个屏幕列出了数据库发布向导可访问的数据库，并允许您选择是为所选数据库中的所有对象编写脚本，还是选择要编写脚本的对象。 选择适当的数据库，并选中 "为所选数据库中的所有对象编写脚本" 选项。

> [!NOTE]
> 如果在图6所示的屏幕中单击 "下一步"，则会出现错误 "此向导可编写脚本的数据库的数据库*名称*中没有对象"，请确保数据库文件的路径不太长。 已发现，如果数据库文件的路径太长，则会出现此错误。

[![数据库发布向导初始屏幕](deploying-a-database-cs/_static/image17.jpg)](deploying-a-database-cs/_static/image16.jpg) 

**图 6**：数据库发布向导初始屏幕（[单击以查看完全大小的图像](deploying-a-database-cs/_static/image18.jpg)）

在下一个屏幕中，你可以生成一个脚本文件，或者，如果你的 web 主机支持该文件，则将数据库直接发布到你的 web 主机提供程序的数据库服务器。 如图7所示，我已将脚本写入 `C:\REVIEWS.MDF.sql`文件中。

[![将数据库脚本保存到文件或将其直接发布到 Web 主机提供程序](deploying-a-database-cs/_static/image20.jpg)](deploying-a-database-cs/_static/image19.jpg) 

**图 7**：将数据库脚本保存到文件或将其直接发布到 Web 主机提供程序（[单击查看完全大小的图像](deploying-a-database-cs/_static/image21.jpg)）

后续屏幕将提示你提供各种脚本编写选项。 你可以指定脚本是否应包含 drop 语句来删除这些现有对象。 默认值为 True，这在第一次部署数据库时很合适。 你还可以指定目标数据库是 SQL Server 2000、SQL Server 2005 还是 SQL Server 2008。 最后，您可以指示是编写架构和数据的脚本、仅编写数据还是仅编写架构的脚本。 该架构是数据库对象、表、存储过程、视图等的集合。 数据是驻留在表中的信息。

如图8所示，将向导配置为删除现有数据库对象，为 SQL Server 2008 数据库生成脚本，同时发布架构和数据。

[![指定发布选项](deploying-a-database-cs/_static/image23.jpg)](deploying-a-database-cs/_static/image22.jpg) 

**图 8**：指定发布选项（[单击以查看完全大小的图像](deploying-a-database-cs/_static/image24.jpg)）

最后两个屏幕汇总了将要执行的操作，并显示脚本的状态。 运行向导的最终结果是，我们有一个脚本文件，其中包含在生产环境中创建数据库所需的 SQL 命令，并使用与开发时相同的数据进行填充。

### <a name="executing-the-sql-commands-on-the-production-environment-database"></a>在生产环境数据库上执行 SQL 命令

现在，我们已经有了包含用于创建数据库的 SQL 命令的脚本及其数据，接下来要对生产数据库执行该脚本。 某些 web 宿主提供程序在 "控制面板" 中提供一个文本框，您可以在其中输入要在数据库上执行的 SQL 命令。 如果你有一个非常大的脚本文件，则此选项可能不起作用（例如 `REVIEWS.MDF.sql` 脚本文件的大小超过 425 KB）。

更好的方法是使用 SQL Server Management Studio （SSMS）直接连接到生产数据库服务器。 如果计算机上安装了非 Express 版本的 SQL Server，则可能已经安装了 SSMS。 否则，你可以[下载并安装](https://www.microsoft.com/downloads/details.aspx?FamilyId=C243A5AE-4BD1-4E3D-94B8-5A0F62BF7796&amp;displaylang=en)SQL Server Management Studio Express Edition 的免费副本。

使用 web 主机提供商提供的信息启动 SSMS 并连接到 web 主机的数据库服务器。

[![连接到 Web 主机提供程序的数据库服务器](deploying-a-database-cs/_static/image26.jpg)](deploying-a-database-cs/_static/image25.jpg) 

**图 9**：连接到 Web 主机提供程序的数据库服务器（[单击以查看完全大小的映像](deploying-a-database-cs/_static/image27.jpg)）

展开 "数据库" 选项卡，找到数据库。 单击工具栏左上角的 "新建查询" 按钮，从数据库发布向导创建的脚本文件粘贴 SQL 命令，然后单击 "执行" 按钮在生产数据库服务器上运行这些命令。 如果脚本文件特别大，可能需要花费几分钟时间来执行命令。

[![连接到 Web 主机提供程序的数据库服务器](deploying-a-database-cs/_static/image29.jpg)](deploying-a-database-cs/_static/image28.jpg) 

**图 10**：连接到 Web 主机提供程序的数据库服务器（[单击以查看完全大小的映像](deploying-a-database-cs/_static/image30.jpg)）

就是这样！ 此时，开发数据库已复制到生产数据库中。 如果在 SSMS 中刷新数据库，则应该会看到新的数据库对象。 图11显示了生产数据库的表、存储过程和用户定义的函数，这些函数在开发数据库上进行镜像。 而且，由于我们指示 "数据库发布向导" 发布数据，因此在执行向导时，生产数据库的表与开发数据库的表具有相同的数据。 图12显示了生产数据库上 `Books` 表中的数据。

[![数据库对象在生产数据库上重复](deploying-a-database-cs/_static/image32.jpg)](deploying-a-database-cs/_static/image31.jpg) 

**图 11**：数据库对象在生产数据库上重复（[单击以查看完全大小的图像](deploying-a-database-cs/_static/image33.jpg)）

[![生产数据库包含与开发数据库相同的数据](deploying-a-database-cs/_static/image35.jpg)](deploying-a-database-cs/_static/image34.jpg) 

**图 12**：生产数据库包含与开发数据库相同的数据（[单击查看完全大小的映像](deploying-a-database-cs/_static/image36.jpg)）

此时，我们只将开发数据库部署到生产环境。 我们尚未介绍如何部署 web 应用程序，或检查在生产环境中使用生产数据库所需的配置更改。 在下一教程中，我们将介绍这些问题！

## <a name="summary"></a>总结

部署数据驱动的 web 应用程序需要将开发期间使用的数据库复制到生产环境中。 许多 web 宿主提供程序提供工具来简化数据库的部署过程。 例如，使用 DiscountASP.NET 可以将数据库 `.mdf` 文件（或备份）的 FTP，然后将数据库附加到控制面板中的数据库服务器。 如果你的 web 宿主提供程序提供的功能是 Microsoft 的数据库发布向导工具，则可以使用另一个选项，它将生成 SQL 命令的脚本来创建开发数据库的架构和数据。 生成此脚本后，可以在生产数据库中执行它。

现在，书籍检查 web 应用程序的数据库是否在生产环境中，我们可以部署该应用程序。 但是，web 应用程序的配置信息指定数据库的连接字符串，并且该连接字符串引用开发数据库。 在将站点部署到生产环境时，需要更新此连接字符串信息。 下一教程将介绍这些配置差异，并演练将数据驱动的书籍评论站点发布到生产所需的步骤。

很高兴编程！

#### <a name="further-reading"></a>其他阅读材料

有关本教程中讨论的主题的详细信息，请参阅以下资源：

- [下载 Microsoft SQL Server 数据库发布向导1。1](https://www.microsoft.com/downloads/details.aspx?familyid=56E5B1C5-BF17-42E0-A410-371A838E570A&amp;displaylang=en)
- [下载 Microsoft SQL Server Management Studio Express Edition](https://www.microsoft.com/downloads/details.aspx?FamilyId=C243A5AE-4BD1-4E3D-94B8-5A0F62BF7796&amp;displaylang=en)

> [!div class="step-by-step"]
> [上一页](core-differences-between-iis-and-the-asp-net-development-server-cs.md)
> [下一页](configuring-the-production-web-application-to-use-the-production-database-cs.md)
