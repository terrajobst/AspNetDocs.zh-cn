---
uid: web-forms/overview/older-versions-getting-started/deploying-web-site-projects/precompiling-your-website-cs
title: 预编译网站（C#） |Microsoft Docs
author: rick-anderson
description: Visual Studio 为 ASP.NET 开发人员提供两种类型的项目： Web 应用程序项目（WAPs）和网站项目（WSPs）。 其中一项重要差异 betwe
ms.author: riande
ms.date: 06/09/2009
ms.assetid: ecd5a4de-beb7-4d1d-bbbb-e31003633267
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deploying-web-site-projects/precompiling-your-website-cs
msc.type: authoredcontent
ms.openlocfilehash: cb42398f44f3cd16ab83a9976e7b34f132384456
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74635807"
---
# <a name="precompiling-your-website-c"></a>预编译网站 (C#)

作者： [Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载代码](https://download.microsoft.com/download/1/0/C/10CC829F-A808-4302-97D3-59989B8F9C01/ASPNET_Hosting_Tutorial_15_CS.zip)或[下载 PDF](https://download.microsoft.com/download/5/C/5/5C57DB8C-5DEA-4B3A-92CA-4405544D313B/aspnet_tutorial15_Precompiling_cs.pdf)

> Visual Studio 为 ASP.NET 开发人员提供两种类型的项目： Web 应用程序项目（WAPs）和网站项目（WSPs）。 这两种项目类型之间的主要区别之一是： WAPs 在部署前必须显式编译代码，而 WSP 中的代码可以在 web 服务器上自动编译。 但是，可以在部署前预编译 WSP。 本教程将探讨预编译的优点，并演示如何从 Visual Studio 和命令行中预编译网站。

## <a name="introduction"></a>简介

Visual Studio 为 ASP.NET 开发人员提供了两种不同的项目类型： Web 应用程序项目（WAP）和网站项目（WSP）。 这些项目类型之间的主要区别之一是 WAPs 需要*显式编译*，而 WSPs 默认情况下使用*自动编译*。 使用 WAPs，可将 web 应用程序的代码编译为单一程序集，该程序集在网站的 `Bin` 文件夹中创建。 部署需要在项目中复制标记内容（`.aspx.ascx`和 `.master` 文件）以及 `Bin` 文件夹中的程序集;不需要部署代码隐藏类文件本身。 另一方面，通过将标记页及其相应的代码隐藏类复制到生产环境来部署 WSPs。 代码隐藏类在 web 服务器上按需编译。

> [!NOTE]
> 请参阅 " [*确定需要部署哪些文件*" 教程](determining-what-files-need-to-be-deployed-cs.md)中的 "显式编译与自动编译" 部分，了解有关项目模型、显式和自动编译之间的差异的更多背景知识，以及编译模型如何影响部署。

自动编译选项易于使用。 没有显式编译步骤，只需要部署已修改的文件，而显式编译则需要部署已更改的标记页和刚编译的程序集。 但是，自动部署有两个潜在缺点：

- 由于在首次访问页面时必须自动编译页面，因此，在部署后首次请求 ASP.NET 页面时，可能会出现短暂但明显的延迟。
- 自动编译要求 web 服务器上存在声明性标记和源代码。 如果你计划将 web 应用程序销售给将在 web 服务器上安装的客户，则这可能是一个不严重选项。

如果上述两个缺点之一是 "再处理"，则可以切换到 WAP 模型或在部署前*预编译*WSP。 本教程检查最适用于托管网站的预编译选项，并演练预编译网站的预编译过程和部署。

## <a name="an-overview-of-aspnet-code-generation-and-compilation"></a>ASP.NET 代码生成和编译概述

在查看可用预编译选项之前，先来讨论在第一次请求 ASP.NET 页（自创建或上次更新以来）时所发生的代码生成和编译。 如您所知，ASP.NET 页面由两部分组成： `.aspx` 文件中的声明性标记;和一个源代码部分，通常在单独的代码隐藏类文件中（`.aspx.cs`）。 当请求 ASP.NET 页时，运行时执行的步骤取决于应用程序的编译模型。

使用 WAPs 时，必须在部署之前将页面的源代码显式编译到单个程序集中。 在部署期间，会将此程序集和各种标记页复制到生产环境中。 当请求到达 ASP.NET 页面的 web 服务器时，运行时将创建页面的代码隐藏类的实例并调用其 `ProcessRequest` 方法，该方法将启动页面生命周期，并最终生成页面的内容，并将其返回给请求者。 运行时可以使用 ASP.NET 页的代码隐藏类，因为在部署之前，代码隐藏类已经编译到一个程序集中。

对于 WSPs 和自动编译，在部署之前没有显式编译步骤。 相反，部署涉及将声明性代码和源代码内容复制到生产环境。 如果在创建或上次更新页面后首次向 web 服务器发出请求，则运行时必须首先将代码隐藏类编译为程序集。 此编译的程序集保存在 `%WINDIR%\Microsoft.NET\Framework\v2.0.50727\Temporary ASP.NET Files`文件夹中，但可以通过 `<system.web>`的 `<compilation tempDirectory="" />` 元素（通常在 `Web.config`中）自定义此文件夹的位置。 由于程序集保存到磁盘中，因此不需要在对同一页的后续请求中重新编译该程序集。

> [!NOTE]
> 正如您所料，在使用自动编译的站点中首次请求页面时（或在首次更改时），会稍微延迟，因为服务器需要一段时间来编译页面的代码，并将生成的程序集保存到磁盘.

简而言之，对于显式编译，你需要在部署前编译网站的源代码，保存运行时无需执行该步骤。 使用自动编译时，运行时将处理页面源代码的编译，但在创建或上次更新页面后首次访问页面时的初始化开销略有降低。

但 ASP.NET 页（`.aspx` 文件）的声明性部分呢？ 显然，在代码分离类中的 `.aspx` 文件和代码之间存在关系，因为声明性标记中定义的 Web 控件在代码中是可访问的。 这也很明显，`.aspx` 文件中的内容大大地影响页面生成的呈现的标记。 那么，运行时如何处理 `.aspx` 文件中定义的文本、HTML 和 Web 控件语法，以生成请求页面的呈现内容呢？

我不想在低级别实现细节上获得太 sidetracked，这在 WAPs 和 WSPs 之间有所不同，但简言之，运行时自动生成一个类文件，其中包含各种 Web 控件作为受保护的成员和方法。 此生成的文件作为*分部类*实现到相应的代码隐藏类。 （[分部类](http://www.dotnet-guide.com/partialclasses.html)允许将单个类的内容分布到多个文件中。）因此，代码隐藏类在两个位置中定义：在创建的 `.aspx.cs` 文件中，以及在运行时创建的自动生成的类中。 此自动生成的类存储在 `%WINDIR%\Microsoft.NET\Framework\v2.0.50727\Temporary ASP.NET Files` 文件夹中。

需要注意的是，对于要由运行时呈现的 ASP.NET 页，其声明性和源代码部分必须编译到程序集。 使用 WAPs，源代码在部署前显式编译为程序集，但声明性标记必须仍转换为代码，并由运行时在 web 服务器上编译。 使用自动编译的 WSPs，必须由 web 服务器编译源代码和声明性标记。

可以将显式编译与 WSP 模型一起使用。 可以显式编译源代码部分，如 WAP 模型。 此外，还可以编译声明性标记。

## <a name="precompilation-options"></a>预编译选项

该 .NET Framework 附带了[ASP.NET 编译工具（`aspnet_compiler.exe`）](https://msdn.microsoft.com/library/ms229863.aspx) ，通过该工具，可以编译使用 WSP 模型生成的 ASP.NET 应用程序的源代码（甚至是内容）。 此工具随 .NET Framework 版本2.0 一起发布，位于 `%WINDIR%\Microsoft.NET\Framework\v2.0.50727` 文件夹中;它可从命令行使用，或通过 "生成" 菜单的 "发布网站" 选项从 Visual Studio 中启动。

编译工具提供了两种常规形式的编译：就地预编译和用于部署的预编译。 使用就地预编译，你可以从命令行运行 `aspnet_compiler.exe` 工具，并指定位于计算机上的网站的虚拟目录或物理路径的路径。 然后，编译工具编译项目中的每个 ASP.NET 页面，将编译后的版本存储在 `%WINDIR%\Microsoft.NET\Framework\v2.0.50727\Temporary ASP.NET Files` 文件夹中，就像第一次通过浏览器访问这些页面一样。 就地预编译可以加快向网站上新部署的 ASP.NET 页发出的第一个请求，因为这样可以使运行时不需要执行此步骤。 但就地预编译对于大多数托管网站都不起作用，因为它需要你能够从 web 服务器的命令行运行程序。 在共享托管环境中，不允许这种访问级别。

> [!NOTE]
> 有关就地预编译的详细信息，请参阅如何：[在 ASP.NET 2.0 中](http://www.odetocode.com/Articles/417.aspx)[预编译 ASP.NET 网站](https://msdn.microsoft.com/library/ms227972.aspx)和预编译。

部署的预编译不会将网站中的页面编译到 `Temporary ASP.NET Files` 文件夹中，而是将这些页面编译为你所选的目录，并采用可部署到生产环境中的格式。

在本教程中，我们浏览了两种用于部署的预编译类型：预编译使用可更新的用户界面，以及使用不可更新的用户界面进行预编译。 使用可更新的用户界面的预编译会使声明性标记保留在 `.aspx`、`.ascx`和 `.master` 文件中，从而允许开发人员查看和（如果需要）修改生产服务器上的声明性标记（如果需要）。 使用不可更新的用户界面进行预编译会生成 `.aspx` 的页面，这些页面包含任何内容的 void，并删除 `.ascx` 和 `.master` 文件，从而隐藏声明性标记，阻止开发人员在生产环境中对其进行更改。

### <a name="precompiling-for-deployment-with-an-updatable-user-interface"></a>使用可更新的用户界面进行部署预编译

了解部署的预编译的最佳方式是查看操作中的示例。 让我们来预编译本书，以使用可更新的用户界面进行部署。 可从 Visual Studio 的 "生成" 菜单或命令行调用 ASP.NET 编译工具。 本部分介绍如何使用 Visual Studio 中的工具;"从命令行预编译" 部分介绍如何从命令行运行编译器工具。

在 Visual Studio 中打开 "查看" 菜单，打开 "生成" 菜单，然后选择 "发布网站" 菜单选项。 此时将启动 "发布网站" 对话框（请参阅**图 1**），您可以在该对话框中指定目标位置、预编译站点的用户界面是否可更新以及其他编译器工具选项。 目标位置可以是远程 web 服务器或 FTP 服务器，但现在选择计算机硬盘驱动器上的文件夹。 由于我们要使用可更新的用户界面预编译站点，因此选中 "允许更新此预编译站点以便进行更新" 复选框，并单击 "确定"。

[![](precompiling-your-website-cs/_static/image2.png)](precompiling-your-website-cs/_static/image1.png)

**图 1**： ASP.NET 编译工具会将你的网站预编译到指定的目标位置  
 （[单击以查看完全大小的映像](precompiling-your-website-cs/_static/image3.png)）

> [!NOTE]
> 在 Visual Web Developer 中，"生成" 菜单中的 "发布网站" 选项不可用。 如果你正在使用 Visual Web Developer，则需要使用 ASP.NET 编译工具的命令行版本，该版本在 "从命令行预编译" 部分中介绍。

预编译网站后，导航到在 "发布网站" 对话框中输入的目标位置。 请花点时间将此文件夹的内容与网站内容进行比较。 **图 2**显示了本书回顾网站文件夹。 请注意，它同时包含 `.aspx` 和 `.aspx.cs` 文件。 另请注意，`Bin` 目录仅包括我们在[上一教程](logging-error-details-with-elmah-cs.md)中添加的一个 `Elmah.dll`文件

[![](precompiling-your-website-cs/_static/image5.png)](precompiling-your-website-cs/_static/image4.png)

**图 2**：项目目录包含 `.aspx` 和 `.aspx.cs` 文件;`Bin` 文件夹只包括 `Elmah.dll`  
 （[单击以查看完全大小的映像](precompiling-your-website-cs/_static/image6.png)）

**图 3**显示了其内容由 ASP.NET 编译工具创建的目标位置文件夹。 此文件夹不包含任何代码隐藏文件。 此外，此文件夹的 `Bin` 目录还包括多个程序集和两个 `.compiled` 文件以及 `Elmah.dll` 程序集。

[![](precompiling-your-website-cs/_static/image8.png)](precompiling-your-website-cs/_static/image7.png)

**图 3**：目标位置文件夹包含用于部署的文件  
 （[单击以查看完全大小的映像](precompiling-your-website-cs/_static/image9.png)）

与 WAPs 中的显式编译不同，部署过程的预编译不会为整个站点创建一个程序集。 相反，它将多个页面分批放入每个程序集。 它还将 `Global.asax` 文件（如果存在）编译到其自己的程序集中，以及 `App_Code` 文件夹中的任何类。 保存 ASP.NET 网页、用户控件和母版页的声明性标记的文件（分别为`.aspx`、`.ascx`和 `.master` 文件）将按原样复制到目标位置目录。 同样，`Web.config` 文件与任何静态文件（如图像、CSS 类和 PDF 文件）一起直接复制。 有关编译工具如何处理各种文件类型的更正式说明，请参阅[ASP.NET 预编译期间的文件处理](https://msdn.microsoft.com/library/e22s60h9.aspx)。

> [!NOTE]
> 通过选中 "发布网站" 对话框中的 "使用固定命名和单页程序集" 复选框，可以指示编译工具为每个 ASP.NET 页、用户控件或母版页创建一个程序集。 将每个 ASP.NET 页编译到其自己的程序集中，可以更精细地控制部署。 例如，如果更新了单个 ASP.NET 网页并需要部署该更改，则只需将该页面的 `.aspx` 文件和关联的程序集部署到生产环境。 有关详细信息，请参阅[如何：通过 ASP.NET 编译工具生成固定名称](https://msdn.microsoft.com/library/ms228040.aspx)。

目标位置目录还包含一个文件，该文件不属于预编译的 web 项目，即 `PrecompiledApp.config`。 此文件通知 ASP.NET 运行时，应用程序已预编译，以及该应用程序是否已使用可更新或可更新的 UI 进行预编译。

最后，请花点时间使用 Visual Studio 或所选的文本编辑器，打开目标位置中的 `.aspx` 文件之一。 使用可更新的用户界面进行预编译时，目标位置目录中的 ASP.NET 页包含与网站中的相应文件完全相同的标记。

### <a name="precompiling-for-deployment-with-a-non-updatable-user-interface"></a>使用不可更新的用户界面进行部署预编译

ASP.NET 编译器工具还可用于预编译站点以使用不可更新的 UI 进行部署。 使用不可更新的 UI 预编译站点的工作方式非常类似于使用可更新 UI 的预编译，主要区别在于目标目录中的 ASP.NET 页、用户控件和母版页已去除其标记。 若要使用不可更新的 UI 预编译网站以进行部署，请从 "生成" 菜单中选择 "发布网站" 选项，但不选中 "允许更新此预编译站点" 选项（参见**图 4**）。

[![](precompiling-your-website-cs/_static/image11.png)](precompiling-your-website-cs/_static/image10.png)

**图 4**：取消选中 "允许更新此预编译站点以便更新" 选项以使用不可更新的 UI 进行预编译  
 （[单击以查看完全大小的映像](precompiling-your-website-cs/_static/image12.png)）

**图 5**显示了使用不可更新的用户界面预编译后的目标位置文件夹。

[![](precompiling-your-website-cs/_static/image14.png)](precompiling-your-website-cs/_static/image13.png)

**图 5**：使用不可更新的 UI 进行部署的目标位置文件夹  
 （[单击以查看完全大小的映像](precompiling-your-website-cs/_static/image15.png)）

将**图 3**与**图 5**进行比较。 虽然这两个文件夹可能看起来相同，但请注意，不可更新的 UI 文件夹缺少母版页，`Site.master`。 尽管**图 5**包含各种 ASP.NET 页面，但如果您查看这些文件的内容，您将看到它们已被删除其声明性标记并替换为占位符文本： "这是预编译工具生成的标记文件，不应删除！"

[![](precompiling-your-website-cs/_static/image17.png)](precompiling-your-website-cs/_static/image16.png)

**图 5**：声明性标记已从 ASP.NET 页中删除

**图 3**和**5**中的 `Bin` 文件夹差别较大。 除了程序集外，**图 5**中的 `Bin` 文件夹还包括每个 ASP.NET 页、用户控件和母版页的 `.compiled` 文件。

如果你不希望在生产环境中安装或管理网站的人员或公司修改 ASP.NET 页面的内容，则可以使用不可更新的 UI 预编译站点。 如果你构建了向客户销售的 ASP.NET web 应用程序，并将其安装在自己的 web 服务器上，则可能需要确保他们不会通过直接编辑你发送的 `.aspx` 页面来修改你的网站的外观。 通过使用不可更新的 UI 预编译你的网站，你会在安装过程中提供占位符 `.aspx` 页面，从而阻止你的客户检查或修改其内容。

### <a name="precompiling-from-the-command-line"></a>从命令行预编译

在后台，Visual Studio 的 "发布网站" 对话框调用 ASP.NET 编译工具（`aspnet_compiler.exe`）来预编译网站。 或者，您可以从命令行调用此工具。 事实上，如果使用 Visual Web Developer，则需要从命令行运行编译器工具，因为 Visual Web Developer 的 "生成" 菜单不包含 "发布网站" 选项。

若要从命令行使用编译器工具，请首先删除命令行并导航到框架目录，`%WINDIR%\Microsoft.NET\Framework\v2.0.50727`。 接下来，在命令行中输入以下语句：

`aspnet_compiler -p "physical_path_to_app" -v / -f -u "target_location_folder"`

上述命令将启动 ASP.NET 编译器工具（`aspnet_compiler.exe`），并通过 `-p` 开关指示它将以*物理\_\_路径*为根的网站预编译为\_应用;此值将与 `C:\MySites\BookReviews`类似，并且应由引号分隔。

`-v` 开关指定站点的虚拟目录。 如果你的站点在 IIS 元数据库中注册为默认网站，则可以省略 `-p` 交换机，只需指定应用程序的虚拟目录。 如果使用 `-p` 开关，则继续 `-v` 开关的值指示网站的根，并用于解析应用程序根引用。 例如，如果将的值指定为 `-v /MySite` 则应用程序中要 `~/path/file` 的引用将解析为 `~/MySite/path/file`。 由于书籍评论站点位于我的 web 托管公司的根目录中，因此我使用了开关 `-v /`。

`-f` 开关（如果存在）指示编译工具覆盖*目标\_位置\_文件夹*目录（如果已存在）。 如果省略 `-f` 开关并且目标位置文件夹已存在，则编译工具将退出，并出现以下错误： "错误 ASPRUNTIME：目标目录不为空。 请手动将其删除或选择其他目标。 "

`-u` 开关（如果存在）将通知工具创建可更新的用户界面。 省略此开关将使用不可更新的用户界面预编译站点。

最后，*目标\_位置\_文件夹*是目标位置目录的物理路径;此值将与 `C:\MySites\Output\BookReviews`类似，并且应由引号分隔。

## <a name="deploying-the-precompiled-website"></a>部署预编译网站

此时，我们已了解如何使用 ASP.NET 编译工具通过可更新和不可更新的用户界面选项预编译网站。 但到目前为止，我们的示例已将网站预编译到了本地文件夹，而不是生产环境中。 好消息是，部署预编译网站非常简单，可以通过 Visual Studio 或其他一些文件复制机制完成，如从独立的 FTP 客户端。

"发布网站" 对话框（如**图 1**所示）具有 "目标位置" 选项，该选项指示将预编译的网站文件复制到的位置。 此位置可以是远程 web 服务器或 FTP 服务器。 在此文本框中输入远程服务器会在一步中预编译网站并将其部署到指定的服务器。 或者，你可以将网站预编译为本地文件夹，然后通过 FTP 或其他方法手动将该文件夹的内容复制到生产环境。

通过 Visual Studio 的 "发布网站" 对话框自动部署的预编译网站有助于实现开发环境和生产环境之间没有配置差异的简单网站。 然而，如[*开发和生产教程之间的常见配置差异*](common-configuration-differences-between-development-and-production-cs.md)中所述，这种差异并不少见。 例如，书籍评审 web 应用程序在生产环境中使用的数据库与开发环境中的数据库不同。 当 Visual Studio 将网站发布到远程服务器时，它会盲目地复制开发环境中的配置文件信息。

对于在开发和生产环境之间具有配置差异的站点，最好将站点预编译为本地目录，复制特定于生产的配置文件，然后将预编译输出的内容复制到成品.

有关将文件从开发环境复制到生产环境的复习，请参阅[*使用 FTP 客户端部署网站*](deploying-your-site-using-an-ftp-client-cs.md)和[*使用 Visual Studio 部署网站*](determining-what-files-need-to-be-deployed-cs.md)教程。

## <a name="summary"></a>总结

ASP.NET 支持两种编译模式：自动和显式。 如前面的教程中所述，Web 应用程序项目（WAPs）使用显式编译，而网站项目（WSPs）在默认情况下使用自动编译。 但是，可以使用 ASP.NET 编译工具在部署之前显式编译 WSP。

本教程重点介绍用于部署支持的编译工具预编译。 在针对部署进行预编译时，编译工具会创建一个目标位置文件夹，编译指定的 web 应用程序的源代码，并将这些已编译的程序集和内容文件复制到目标位置文件夹中。 可以将编译工具配置为创建可更新或不可更新的用户界面。 当使用不可更新的用户界面选项进行预编译时，内容文件中的声明性标记将被删除。 简而言之，预编译允许您部署基于网站项目的应用程序，而无需包含任何源代码文件和声明性标记（如果需要）。

很高兴编程！

### <a name="further-reading"></a>其他阅读材料

有关本教程中讨论的主题的详细信息，请参阅以下资源：

- [ASP.NET 网站预编译](https://msdn.microsoft.com/library/ms228015.aspx)
- [ASP.NET 2.0 中的代码隐藏和编译](https://msdn.microsoft.com/magazine/cc163675.aspx)
- [ASP.NET 中的预编译](http://www.odetocode.com/Articles/417.aspx)
- [ASP.NET 中的预编译站点选项](http://www.dotnetperls.com/precompiled)

> [!div class="step-by-step"]
> [上一页](logging-error-details-with-elmah-cs.md)
> [下一页](users-and-roles-on-the-production-website-cs.md)
