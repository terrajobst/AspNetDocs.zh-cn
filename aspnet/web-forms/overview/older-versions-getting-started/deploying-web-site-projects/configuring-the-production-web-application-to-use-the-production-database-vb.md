---
uid: web-forms/overview/older-versions-getting-started/deploying-web-site-projects/configuring-the-production-web-application-to-use-the-production-database-vb
title: 配置生产 Web 应用程序以使用生产数据库（VB） |Microsoft Docs
author: rick-anderson
description: 如前面的教程中所述，在开发环境和生产环境之间的配置信息不是很常见。 这是 es 。
ms.author: riande
ms.date: 04/23/2009
ms.assetid: a64a7aa0-6608-449e-83bf-1ef8cceee504
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deploying-web-site-projects/configuring-the-production-web-application-to-use-the-production-database-vb
msc.type: authoredcontent
ms.openlocfilehash: 7fe4f545a76992ad687827af447d9a9e95bea73f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78516620"
---
# <a name="configuring-the-production-web-application-to-use-the-production-database-vb"></a>配置生产 Web 应用程序以使用生产数据库 (VB)

作者： [Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载代码](https://download.microsoft.com/download/E/6/F/E6FE3A1F-EE3A-4119-989A-33D1A9F6F6DD/ASPNET_Hosting_Tutorial_08_VB.zip)或[下载 PDF](https://download.microsoft.com/download/C/3/9/C391A649-B357-4A7B-BAA4-48C96871FEA6/aspnet_tutorial08_DBConfig_vb.pdf)

> 如前面的教程中所述，在开发环境和生产环境之间的配置信息不是很常见。 这对于数据驱动的 web 应用程序尤其如此，因为开发环境和生产环境之间的数据库连接字符串不同。 本教程探讨如何配置生产环境以更详细地包含适当的连接字符串。

## <a name="introduction"></a>简介

在开发时，数据驱动的 web 应用程序通常使用不同的数据库，而不是在生产环境中。 对于由 web 宿主提供程序托管并在本地开发的应用程序，开发数据库通常驻留在开发人员计算机上，而生产数据库承载在 web 托管公司的网站上的数据库服务器上。 部署数据驱动的 web 应用程序需要将开发数据库复制到生产数据库服务器。 在上一教程中，我们介绍了完成此步骤的方法。

Web 应用程序使用*连接字符串*中的信息建立与数据库的连接。 连接字符串通常存储在 `Web.config`中，指定数据库服务器名称、数据库名称、安全上下文和其他信息。 由于 web 应用程序使用的数据库取决于 web 应用程序是在开发环境还是在生产环境中运行，因此，两种环境之间的连接字符串必须不同。

开发环境和生产环境之间的配置信息不同，这种情况并不常见。 *开发和生产教程之间的常见配置差异*讨论了在这两个环境之间维护单独的配置信息的方法，以及对数据库连接字符串的简要讨论。 本教程探讨如何配置生产环境以更详细地包含适当的连接字符串。

## <a name="examining-the-connection-string-information"></a>检查连接字符串信息

书籍审阅 web 应用程序使用的连接字符串存储在应用程序的配置文件中，`Web.config`。 `Web.config` 包含用于存储连接字符串的特殊部分，其名称为[&lt;connectionStrings&gt;](https://msdn.microsoft.com/library/bf7sd233.aspx)名称正好。 书籍审阅网站的 `Web.config` 文件中有一个名为 `ReviewsConnectionString`的此部分中定义的连接字符串：

[!code-xml[Main](configuring-the-production-web-application-to-use-the-production-database-vb/samples/sample1.xml)]

连接字符串-Data Source = .\SQLEXPRESS;AttachDbFilename = |DataDirectory | \Reviews.mdf; 集成安全性 = True;User Instance = True-由多个选项和值组成，选项/值对由分号分隔，每个选项和值用等号分隔。 此连接字符串中使用的四个选项为：

- `Data Source`-指定数据库服务器和数据库服务器实例名称（如果有）的位置。 `.\SQLEXPRESS`的值就是一个包含数据库服务器和实例名称的示例。 句点指定数据库服务器与应用程序在同一台计算机上;实例名称为 `SQLEXPRESS`。
- `AttachDbFilename`-指定数据库文件的位置。 值包含占位符 `|DataDirectory|`，它在运行时解析为应用程序的完整路径 `App_Data` 文件夹。
- `Integrated Security`-一个布尔值，该值指示在连接到数据库时是否使用指定的用户名/密码（false）或当前的 Windows 帐户凭据（true）。
- `User Instance`-特定于 SQL Server Express 版本的配置选项，用于指示是否允许本地计算机上的非管理用户附加和连接到 SQL Server Express 版数据库。 有关此设置的详细信息，请参阅[SQL Server Express 用户实例](https://msdn.microsoft.com/library/ms254504.aspx)。

允许的连接字符串选项取决于要连接到的数据库和正在使用的[ADO.NET](http://ADO.NET)数据库提供程序。 例如，用于连接到 Microsoft SQL Server 数据库的连接字符串不同于用于连接到 Oracle 数据库的连接字符串。 同样，使用 SqlClient 提供程序连接到 Microsoft SQL Server 数据库时，使用的连接字符串与使用 OLE DB 访问接口时使用的字符串不同。

你可以手动构建数据库连接字符串，方法是使用[ConnectionStrings.com](http://www.connectionstrings.com/)作为资源来处理可用的选项。 但是，更简单的方法是将数据库添加到 Visual Studio 中的服务器资源管理器，然后从属性窗口中获取连接字符串。 使用后一种方法将连接字符串构造到生产数据库服务器。

打开 Visual Studio，然后导航到 "服务器资源管理器" 窗口（在 Visual Web Developer 中，此窗口称为 "数据库资源管理器）"。 右键单击 "数据连接" 选项，然后从上下文菜单中选择 "添加连接" 选项。 此时将打开图1所示的向导。 选择适当的数据源，然后单击 "继续"。

[![选择将新数据库添加到服务器资源管理器](configuring-the-production-web-application-to-use-the-production-database-vb/_static/image2.jpg)](configuring-the-production-web-application-to-use-the-production-database-vb/_static/image1.jpg) 

**图 1**：选择将新数据库添加到服务器资源管理器（[单击以查看完全大小的映像](configuring-the-production-web-application-to-use-the-production-database-vb/_static/image3.jpg)）

接下来，指定不同的数据库连接信息（参见图2）。 注册到 web 托管公司时，他们应该已经提供了有关如何连接到数据库的信息，即数据库服务器名称、数据库名称、用于连接到数据库的用户名和密码等。 输入此信息后，请单击 "确定" 以完成该向导并将数据库添加到服务器资源管理器。

[![指定数据库连接信息](configuring-the-production-web-application-to-use-the-production-database-vb/_static/image5.jpg)](configuring-the-production-web-application-to-use-the-production-database-vb/_static/image4.jpg) 

**图 2**：指定数据库连接信息（[单击以查看完全大小的映像](configuring-the-production-web-application-to-use-the-production-database-vb/_static/image6.jpg)）

生产环境数据库现在应在服务器资源管理器中列出。 从服务器资源管理器中选择数据库并中转到属性窗口。 在这里，你将看到一个名为 "连接字符串" 的属性，其中包含数据库的连接字符串。 假设你在生产环境和 SqlClient 提供程序上使用 Microsoft SQL Server 数据库，则连接字符串应如下所示：

<strong>数据源 =<em>serverName</em>;初始目录 =<em>databaseName</em>;持久性安全信息 = True;User ID =<em>username</em>;密码 =*密码</strong>*

其中*serverName*、 *databaseName*、 *username*和*password*均为数据库服务器名称、数据库名称以及 web 主机公司提供给你的用户名和密码的值。

## <a name="deploying-the-book-reviews-web-application"></a>部署书籍评审 Web 应用程序

以上教程逐步介绍了如何将开发数据库复制到生产环境中，但未探索如何部署数据驱动的应用程序。 此时，生产环境包含数据库，但使用的是书籍的版本通过静态审核检查应用程序。 需要将新的、数据驱动的应用程序部署到生产服务器，以及更新的配置信息。

花点时间将数据驱动的应用程序从开发环境部署到生产环境。 之前的教程中详细介绍了此过程。 如果需要刷新程序，请参阅*使用 FTP 客户端部署网站*或*使用 Visual Studio 部署网站*教程。 你将需要确保生产数据库连接字符串与生产环境中使用的字符串相同，这意味着必须部署备用的 `Web.config` 文件。 具体而言，此修改后的 `Web.config` 文件 s `<connectionStrings>` 元素需要包含生产数据库连接字符串，应如下所示：

[!code-xml[Main](configuring-the-production-web-application-to-use-the-production-database-vb/samples/sample2.xml)]

请注意，`<connectionStrings>` 元素中的连接字符串的名称相同（`ReviewsConnectionString`），但现在包含生产数据库连接字符串而不是开发数据库连接字符串。

除非您具有更正规的部署工作流，否则请手动修改 `Web.config` 文件，以便在部署之前使用生产数据库连接字符串（请记住将其恢复回使用开发数据库连接字符串），或维护单独的 `Web.config` 文件，其中包含将作为部署过程的一部分上载到生产环境的生产环境配置信息。

> [!NOTE]
> 如果意外部署了包含开发数据库连接字符串的 `Web.config` 文件，则当生产中的应用程序尝试连接到数据库时，将会出现错误。 此错误将作为 `SqlException`，其中包含一条消息，报告服务器找不到或无法访问。

将站点部署到生产环境后，请通过浏览器访问生产站点。 你应看到并获得与在本地运行数据驱动的应用程序相同的用户体验。 当然，在生产环境中访问该网站时，该站点由生产数据库服务器提供支持，而访问开发环境中的网站则使用开发环境中的数据库。 图3显示了在生产环境中从网站向*自己 ASP.NET 3.5 的24小时*检查页面（请注意浏览器地址栏中的 URL）。

[![数据驱动的应用程序现在可以在生产环境中使用！](configuring-the-production-web-application-to-use-the-production-database-vb/_static/image8.jpg)](configuring-the-production-web-application-to-use-the-production-database-vb/_static/image7.jpg) 

**图 3**：数据驱动的应用程序现在可以在生产环境中使用！ （[单击以查看完全大小的映像](configuring-the-production-web-application-to-use-the-production-database-vb/_static/image9.jpg)）

### <a name="storing-connection-strings-in-a-separate-configuration-file"></a>在单独的配置文件中存储连接字符串

在开发和生产环境中维护单独的配置信息的一种常用方法是使用 `Web.config`的两个版本：一个用于开发环境，另一个用于生产环境。 在部署时，可以将适当的 `Web.config` 版本复制到生产环境中。 理想情况下，此过程将作为部署工作流的一部分自动执行。

您可以根据需要维护两个单独的 `Web.config` 文件，而不是提供更精细的差别。 可在 `Web.config` 文件中引用的外部配置文件中定义构成 `Web.config` 文件的元素。 简言之，两种环境都可以有一个 `Web.config` 文件，该文件将包含应用程序使用的连接字符串，并且对于每个环境都是唯一的。 我发现，将不同的配置信息分隔到单独的文件中提供了整齐和更简单的 `Web.config` 文件，并且更清晰地概述了开发和生产环境之间的配置差异。

若要使用此方法，请首先在名为 `ConfigSections`的 web 应用程序中创建一个新文件夹。 接下来，将两个文件添加到名为 "databaseConnectionStrings" 和 "databaseConnectionStrings" 的新文件夹中。接下来，将 `Web.config` 中的 `<connectionStrings>` 元素复制到 databaseConnectionStrings 和 databaseConnectionStrings 文件中，然后修改 databaseConnectionStrings 文件中的连接字符串，使其指定生产数据库连接字符串。 例如，databaseConnectionStrings 文件只应包含具有引用开发数据库的连接字符串的 `<connectionStrings>` 元素：

[!code-xml[Main](configuring-the-production-web-application-to-use-the-production-database-vb/samples/sample3.xml)]

同样，databaseConnectionStrings 文件应该只包含一个 `<connectionStrings>` 元素，但是一个包含生产数据库连接字符串的元素。

创建 databaseConnectionStrings 文件的副本，并将其命名为 databaseConnectionStrings。

> [!NOTE]
> 如果需要，你可以将配置文件命名为除 databaseConnectionStrings 以外的其他内容，如 `connectionStrings.config` 或 `dbInfo.config`。 但是，请务必使用 `.config` 扩展名命名文件，因为默认情况下，ASP.NET 引擎不提供 `.config` 文件。 如果你将该文件命名为其他内容（如 `connectionStrings.txt`），则用户可以将其浏览器指向[www.yoursite.com/ConfigSettings/connectionStrings.txt](http://www.yoursite.com/ConfigSettings/connectionStrings.txt)并查看该文件的内容！

此时，`ConfigSections` 文件夹应包含三个文件（请参阅图4）。 DatabaseConnectionStrings 和 databaseConnectionStrings 文件分别包含适用于开发环境和生产环境的连接字符串。 DatabaseConnectionStrings 文件包含 web 应用程序在运行时将使用的连接字符串信息。 因此，databaseConnectionStrings 文件应与开发环境中的 databaseConnectionStrings 文件相同，而在生产环境中，databaseConnectionStrings 文件应等同于databaseConnectionStrings。

[![ConfigSections](configuring-the-production-web-application-to-use-the-production-database-vb/_static/image11.jpg)](configuring-the-production-web-application-to-use-the-production-database-vb/_static/image10.jpg) 

**图 4**： ConfigSections （[单击查看完全尺寸的图像](configuring-the-production-web-application-to-use-the-production-database-vb/_static/image12.jpg)）

现在，我们需要指示 `Web.config` 为其连接字符串存储使用 databaseConnectionStrings 文件。 打开 `Web.config` 并将现有 `<connectionStrings>` 元素替换为以下内容：

[!code-xml[Main](configuring-the-production-web-application-to-use-the-production-database-vb/samples/sample4.xml)]

`configSource` 特性指定相对于 `Web.config` 文件的物理路径。 如果外部 `.config` 文件与 `Web.config` 在同一目录中，则将此属性设置为 `.config` 文件的文件名。 如果它在子目录中，就像 databaseConnectionStrings 一样，使用反斜杠指定该子文件夹，以分隔文件夹和文件名，例如 ConfigSections\databaseConnectionStrings.config。

进行此修改后，开发和生产环境包含相同的 `Web.config` 文件。 现在，唯一的区别在于 databaseConnectionStrings 文件。 将 databaseConnectionStrings 文件复制到生产，并将其重命名为 databaseConnectionStrings。如果以后对生产数据库连接字符串进行了更改，则需要将其提供给 databaseConnectionStrings 文件，然后将该文件上载到生产，并将其重命名为 databaseConnectionStrings。

> [!NOTE]
> 您可以在单独的文件中指定任何 `Web.config` 元素的信息，然后使用 `configSource` 属性从 `Web.config`中引用该文件。

## <a name="summary"></a>摘要

数据驱动的应用程序通常在开发和生产环境中使用不同的数据库。 因此，存储在 web 应用程序中的数据库连接字符串在每个环境中必须是唯一的。 在本教程中，我们将介绍如何确定生产数据库连接字符串，以及在两个环境中维护唯一连接字符串信息的方法。

很高兴编程！

### <a name="further-reading"></a>其他阅读材料

有关本教程中讨论的主题的详细信息，请参阅以下资源：

- [连接字符串和配置文件](https://msdn.microsoft.com/library/ms254494.aspx)
- [数据库配置字符串信息 @ ConnectionStrings.com](http://www.connectionstrings.com/)
- [将设置移出 web.config 文件](http://www.asp101.com/tips/index.asp?id=154)
- [&lt;connectionStrings&gt; 元素的技术文档](https://msdn.microsoft.com/library/bf7sd233.aspx)

> [!div class="step-by-step"]
> [上一页](deploying-a-database-vb.md)
> [下一页](configuring-a-website-that-uses-application-services-vb.md)
