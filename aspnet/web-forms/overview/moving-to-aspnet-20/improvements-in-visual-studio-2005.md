---
uid: web-forms/overview/moving-to-aspnet-20/improvements-in-visual-studio-2005
title: Visual Studio 2005 中的改进 |Microsoft Docs
author: microsoft
description: Visual Studio 2005 为 Web 应用程序开发人员提供了对 Web 项目的改进和增强功能。
ms.author: riande
ms.date: 02/20/2005
ms.assetid: 72d90cd0-b3d9-454c-b2eb-ed0d9812f32c
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/improvements-in-visual-studio-2005
msc.type: authoredcontent
ms.openlocfilehash: 64215d556ded0850537a13856fe69b094116ebca
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78464648"
---
# <a name="improvements-in-visual-studio-2005"></a>Visual Studio 2005 中的改进

由[Microsoft](https://github.com/microsoft)

> Visual Studio 2005 为 Web 应用程序开发人员提供了对 Web 项目的改进和增强功能。

Visual Studio 2005 为 Web 应用程序开发人员提供了对 Web 项目的改进和增强功能。 与 Visual Studio .NET 2002 和2003一样强大，处理 Web 项目的方式有很多投诉。 Visual Studio 2005 添加了大量新功能，以解决这些投诉。 对于更喜欢 Visual Studio .NET 2003 处理 Web 应用程序的编译方式的用户，请参阅[Web 应用程序项目](https://go.microsoft.com/fwlink/?LinkId=57870)。

在此模块中，我们在 Web 项目的创建、管理和开发方面做了改进。 在更高版本的模块中，在生成 Web 项目和部署它们方面做了改进。

## <a name="frontpage-server-extensions"></a>FrontPage 服务器扩展

需要在框中 FrontPage 服务器扩展 Visual Studio .NET 2002 和2003，才能创建或生成 Web 项目。 开发人员可在两种不同的访问模式（FrontPage 服务器扩展或文件访问模式）之间进行选择，这两种模式都 FrontPage 服务器扩展来执行任务，例如在 IIS 中设置应用程序根目录等。

Visual Studio 2005 消除了对本地项目 FrontPage 服务器扩展的依赖。 Visual Studio 2005 现在直接访问 IIS 元数据库，而不是使用 FrontPage 服务器扩展。 Visual Studio 2005 还添加了对允许远程项目访问的 FTP 支持，而无需 FrontPage 服务器扩展。

对于想要在项目中使用 FrontPage 服务器扩展的开发人员，此选项仍然可用。 但是，根据 ASP.NET 开发人员社区提供的强大反馈，这并不是必需的。

> [!NOTE]
> 远程项目创建、打开等仍需要 FrontPage 服务器扩展。

## <a name="aspnet-development-server"></a>ASP.NET Development Server

Visual Studio 2005 附带了一个名为 ASP.NET 开发服务器的新 Web 服务器。 （此 Web 服务器以前称为 Cassini。）

ASP.NET 开发服务器有多个优点。

- 非管理员现在可以针对 Web 服务器进行开发和调试。
- ASP.NET 开发服务器将虚拟目录动态映射到文件系统中的任何位置，以实现灵活的项目位置。
- Windows XP Professional 上已经使用 IIS 的用户现在可以创建新的 Web 应用程序，这些应用程序不会影响其在 IIS 中默认网站的文件或文件夹结构。

无需特殊配置即可利用 ASP.NET 开发服务器。 当调试或浏览文件系统上承载的 Web 项目时，Visual Studio 2005 将自动启动随机端口上的 ASP.NET 开发服务器实例以处理请求。

详细信息将在本模块后面的 ASP.NET 开发服务器中介绍。

## <a name="improved-file-management"></a>改进的文件管理

在 Visual Studio 2002 和2003中，为 Web 应用程序中的所有文件存储了一个C#项目文件（.vbproj for VB.NET 和 .csproj）。 解决方案资源管理器显示基于项目文件中的文件信息。 因此，在使用外部编辑器的情况下，解决方案资源管理器通常会显示不正确的信息。 Visual Studio 2002 和2003经常会覆盖文件更改或不显示最新版本的文件。

Visual Studio 2005 与项目文件不相同。 相反，它直接读取磁盘中的文件和文件夹信息，使项目中的文件显示准确。 由于 Visual Studio 2002 和2003中的 "引用" 文件夹并不表示你的 Web 应用程序中的实际文件夹，因此 Visual Studio 2005 还会删除解决方案资源管理器中的 "引用" 文件夹。 若要在 Visual Studio 2005 中访问你的项目的引用，你应使用项目的属性页。

## <a name="creating-web-projects"></a>创建 Web 项目

Web 开发人员在 Visual Studio 2005 中提供了许多可用于创建项目的新选项。 网站现在可以在文件系统中的任何位置创建，然后可以使用新 ASP.NET 开发服务器进行调试或浏览。 开发人员还可以使用 FTP 创建新网站。

单击此处查看在 Visual Studio 2005 中创建 Web 项目的视频演练。

![](improvements-in-visual-studio-2005/_static/image1.png)

[打开全屏视频](improvements-in-visual-studio-2005/_static/creating_projects1.wmv)

### <a name="file-system-projects"></a>文件系统项目

如视频演练中所示，可以选择在本地计算机上或通过文件共享在远程位置的文件系统上创建网站。 使用 ASP.NET 开发服务器浏览和调试在文件系统上创建的网站。

> [!NOTE]
> ASP.NET 开发服务器可能会对客户造成一些混淆。 如果在文件系统上的 IISs 目录结构（即 c：/inetpub/wwwroot）中创建 Web 项目，则在 Visual Studio 2005 中启动该网站时，该网站仍会通过 ASP.NET 开发服务器浏览。 因此，任何 IIS 配置（即身份验证方法）都不适用。

默认 web 项目还会通过仅包括 default.aspx page、default.cs 文件和 App/_Data 文件夹来消除大量开销。 在需要时添加 web.config 和特殊文件夹（即 app/_code）。 你的 web 项目仅包含所需的文件和文件夹。

### <a name="http-projects"></a>HTTP 项目

HTTP 项目可以是在本地 IIS 网站或远程网站上创建的项目。 默认项目位置为 `http://localhost`。 如果单击 "浏览" 按钮，则有两个 HTTP 选项： "本地 IIS" 和 "远程站点"。 这两个选项的主要区别是在 "选择位置" 对话框和文件复制到 Web 服务器的方式中显示网站信息的方法。

本地 IIS 选项读取本地计算机上的元数据库中的站点信息，并使用文件系统复制文件。 远程站点选项使用 FrontPage 服务器扩展，并使用 HTTP 和 FrontPage 服务器扩展 RPC 调用复制站点信息和文件。

> [!NOTE]
> 不会再使用 vs # # #/_tmp .htm 文件和 get/_aspx/_ver 来确定版本信息。

默认的 HTTP 选项为 "本地 IIS"。 此选项将读取 IIS 元数据库，以确定哪些网站可用以及要在其中创建内容的位置。 通过在树视图中选择其他文件夹或虚拟目录，可以选择该文件夹或虚拟目录。 你还可以创建一个新的虚拟目录，将文件夹标记为应用程序，以及从此对话框中删除现有虚拟目录。

!["选择位置" 对话框](improvements-in-visual-studio-2005/_static/image1.gif)

**图 1**： "选择位置" 对话框

与 Visual Studio 的早期版本不同，如果选中 "**使用安全套接字层**" 复选框，SSL 证书与要浏览的 URL 不匹配，则会显示一个安全警报对话框，询问你是否要继续。 使用 Visual Studio .NET 2003，如果证书不是匹配的证书，则创建项目将失败。

![与 SSL 证书有关的安全警报](improvements-in-visual-studio-2005/_static/image2.gif)

**图 2**：与 SSL 证书有关的安全警报

### <a name="note-on-host-headers"></a>主机标头上的说明

如果要在绑定到特定 IP 的站点上创建 Web 应用程序，则需要确保配置了主机标头。 否则，Visual Studio 将在 `http://localhost`创建网站，但在从 IDE 中浏览或调试该站点时，该 IP 地址将无法正确解析。

如果选择 "远程站点" 选项，则对话框将更改为允许您输入新网站的目标 URL。 此 URL 必须位于启用了 FrontPage 服务器扩展的服务器上。 如果要使用 FrontPage 服务器扩展使用本地 Web 服务器，可以使用 "远程站点" 选项并指定本地 URL。

![在远程服务器上创建网站](improvements-in-visual-studio-2005/_static/image1.jpg)

**图 3**：在远程服务器上创建网站

通过 SSL 在远程站点上创建应用程序时，如果 SSL 证书不匹配，确认对话框与使用本地 IIS 选项时显示的对话框略有不同。

![远程站点安全警报](improvements-in-visual-studio-2005/_static/image3.gif)

**图 4**：远程站点安全警报

<a id="_Toc116100243"></a>

#### <a name="ftp"></a>FTP

Visual Studio 2005 引入了通过 FTP 创建网站的选项。 使用此选项时，IDE 将在本地用户临时文件夹中创建文件，然后使用 FTP 将文件移动到 FTP 位置。

> [!NOTE]
> 临时文件夹位置为 "c：/文档和设置/&lt;用户&gt;/Local Settings/Temp/VWDWebCache/&lt;Server&gt;/_&lt;应用程序名称&gt;

使用 FTP 选项时，将显示 "选择位置" 对话框。 按如下所示，在此对话框中输入所需的 FTP 连接信息。

![FTP 的 "选择位置" 对话框](improvements-in-visual-studio-2005/_static/image2.jpg)

**图 5**： FTP 的 "选择位置" 对话框

## <a name="lab-setup-ftp-site-and-create-a-project"></a>Lab：设置 FTP 站点和创建项目

以下步骤将配置 FTP 站点，使用户拥有一个只能通过 FTP 上传到的位置。

### <a name="install-the-ftp-service"></a>安装 FTP 服务

1. 打开 "添加/删除程序"，选择 "添加/删除 Windows 组件"
2. 选择 Internet Information Services （Windows 2003 上的应用程序服务器）并单击 "**详细信息**"。
3. 检查**文件传输协议（FTP）服务**，然后单击 **"确定"** 。
4. 单击 "**下一步**" 以安装 FTP 服务。

### <a name="create-a-new-folder-for-content"></a>为内容创建新文件夹

1. 在 Windows 资源管理器中，在 c：/inetpub/wwwroot 内创建名为**User1**的新文件夹。

#### <a name="configure-folders-and-permissions-on-folders"></a>配置文件夹和文件夹的权限。

1. 从 "管理工具" 打开 Internet Information Services 管理单元。 你现在会在 "计算机名" 节点下有一个 "FTP 站点" 文件夹。
2. 展开 " **FTP 站点**"。
3. 右键单击**默认 FTP 站点**，依次选择 "**新建**" 和 "**虚拟目录**"，然后单击 "**下一步**"。
4. 输入**User1**作为虚拟目录名称，并单击 "**下一步**"。
5. 为路径输入**c：/inetpub/wwwroot/User1** ，然后单击 "**下一步**"。
6. 单击 "**下一步**"，然后单击 "**完成**" 完成向导。
7. 右键单击 "默认 FTP 站点" 下的**User1**虚拟目录，然后选择 "**属性**"。
8. 选中 "**写入**" 复选框，并单击 **"确定"** 以关闭对话框。
9. 右键单击 "**默认 FTP 站点**"，然后选择 "**属性**"。
10. 在 "**安全帐户**" 选项卡上，取消选中 "**允许匿名连接**"。
11. 询问是否要继续，请单击对话框中的 **"是"** 。
12. 单击 **“确定”** ，关闭对话框。
13. 展开 **"网站" 节点下**的 "**默认**网站"。
14. 右键单击**User1**目录，然后选择 "**属性**"
15. 在 "**应用程序设置**" 部分中，单击 "**创建**" 将文件夹标记为应用程序。
16. 单击 **“确定”** ，关闭对话框。
17. 关闭 "Internet Information Services" 管理单元。

### <a name="create-web-project"></a>创建 web 项目

1. 打开 Visual Studio 2005。
2. 从 "**文件**" 菜单中选择 "**新建**网站"。
3. 在 "**位置**" 下拉列表中，选择 " **FTP**"。
4. 单击“浏览”。
5. 在 "**服务器**" 文本框中输入**localhost** 。
6. 在 "目录" 文本框中输入**User1** 。
7. 单击“打开”。 将在 "新建网站" 对话框中输入 FTP 位置。
8. 单击“确定”。
9. 在 "FTP 登录" 对话框中取消选中 "**匿名登录**"，输入你的凭据，然后单击 **"确定"** 。
10. 项目的 URL 是什么？ （项目的 URL 将显示在解决方案资源管理器中。）
11. 在 "**生成**" 菜单中，选择 "**构建网站**" 或 "**生成解决方案**"。
12. 在解决方案资源管理器中右键单击 "default.aspx"，然后选择 "**在浏览器中查看**"。
13. 在 "要求提供网站 URL" 对话框中，输入 URL 的 `http://localhost/user1`，然后单击 **"确定"** 。

> [!NOTE]
> 如果收到一个错误，指示无法加载类型/_Default，请确保在您的网站上运行 ASP.NET 2.0，而不是较早的版本。 可以在 Internet Information Services 的 "ASP.NET" 选项卡中执行此操作。

## <a name="opening-web-projects"></a>打开 Web 项目

打开 Web 项目类似于创建项目。 以下各部分将介绍在 IDE 中工作时要保持引人注目的区域。 还介绍了如何使用 HTTP 和 FTP 来处理 Web 项目。

若要打开 Web 项目，请从 "文件" 菜单中选择 "打开网站"。 系统将提示您前面介绍的 "选择位置" 对话框，您可以使用相同的四个选项： "文件系统"、"本地 IIS"、"FTP" 和 "远程站点"。

<a id="_Toc116100245"></a>

## <a name="file-system"></a>文件系统

如前文所述，Visual Studio 不再使用项目文件。 因此，如果您选择从文件系统打开网站，则实际上可以选择所需的任何文件夹，即使您选择的文件夹不是最初在 Visual Studio 中创建的 Web 项目。 例如，你可以选择将 "我的文档" 文件夹作为网站打开，Visual Studio 会将其打开并显示你的文件，如下所示。

![作为网站打开的文档](improvements-in-visual-studio-2005/_static/image3.jpg)

**图 6**：作为网站打开的*文档*

由于 Visual Studio 仅在必要时才会创建其他文件和文件夹，因此，不会将其他文件或文件夹添加到打开的位置。 此体系结构的副作用是它阻止你将网站嵌套在文件系统上。 例如，请考虑以下目录结构。

C：/MyWebSite Web 项目

C：/MyWebSite/嵌套的另一个 web 项目

当你在 c：/MyWebSite 打开网站时，嵌套文件夹将显示为该应用程序的子文件夹。

<a id="_Toc116100246"></a>

## <a name="http"></a>HTTP

通过 HTTP 打开网站时，将从 IIS 元数据库（本地 IIS）或使用 FrontPage 服务器扩展（远程站点）读取设置。如果有嵌套的 web 应用程序，则这些应用程序也会显示为应用程序。 如果你熟悉如何在 FrontPage 中使用 web 应用程序，则 Visual Studio 2005 中的行为是类似的。

即使对于嵌套在 IDE 中当前打开的应用程序下的应用程序，Visual Studio 也会显示一个图标，但不允许您展开这些应用程序来查看其内容。 不过，您可以双击它们以打开它们。 当你执行此操作时，会显示一个对话框，提示你打开 web 应用程序（并替换当前打开的解决方案），或者将 Web 应用程序添加到当前解决方案。

![双击嵌套应用程序图标会显示此对话框](improvements-in-visual-studio-2005/_static/image4.jpg)

**图 7**：双击嵌套应用程序图标会显示此对话框

<a id="_Toc116100247"></a>

## <a name="ftp-site"></a>FTP 站点

通过 FTP 打开站点时，所有文件都将以本地方式复制到 temp 文件夹中。 本地存储位置的完整路径会显示在项目的 "属性" 窗格中，并使用以下格式创建。

C：/Documents and Settings/&lt;用户&gt;/Local Settings/Temp/VWDWebCache/&lt;Server&gt;/_&lt;应用程序名称&gt;

使用 FTP 时，Visual Studio 将需要为你的项目指定基 URL，以便你可以浏览该 URL，如下所示。 如果未指定基 URL，则 Visual Studio 将在您第一次尝试浏览网站中的页面时向您询问。

![指定 FTP 站点的基 URL](improvements-in-visual-studio-2005/_static/image5.jpg)

**图 8**：指定 FTP 站点的基 URL

## <a name="improvements-in-compilation"></a>编译中的改进

在 Visual Studio 2005 中使用 Web 应用程序比以前的版本更快。 这是由于编译体系结构中的更改所致。

在 Visual Studio 2002 和2003中，Web 应用程序编译到一个主程序集中，该程序集驻留在/bin 文件夹中。 在 Visual Studio 2005 中，添加了应用/_Code 文件夹。 类和其他非 UI 代码添加到 App/_Code 文件夹。 当 Visual Studio 生成项目时，应用/_Code 文件夹中的所有文件都将编译为单个应用/_Code .dll 文件。 此更改的结果是，后续版本比以前版本更快。

> [!NOTE]
> MSBuild 命令行实用工具也可用于生成 ASP.NET Web 应用程序。 此工具将在模块9中介绍。

另一种编译增强功能是 "生成" 菜单上的 "新建生成页" 选项。 利用此功能，开发人员可以仅重新生成当前页面（同时，还可重新生成依赖项），以便可以更快地编译更改。 由于C#出于更新 intellisense 等目的而不提供后台编译，因此它们将从该功能中受益，因为它只是重新生成单个页面就可以快速更新 intellisense。

项目的生成属性允许您配置在执行启动页之前发生的生成类型。 开发人员可以选择仅生成当前页面，以便 Visual Studio 可以在代码更改后更快速地开始调试应用程序。

!["生成" 页启动操作](improvements-in-visual-studio-2005/_static/image6.jpg)

**图 9**： "生成" 页的 "启动" 操作

Visual Studio 和 ASP.NET 体系结构的另一个强大增强功能位于 "编辑并继续" 区域。 在 Visual Studio 2005 中，开发人员可以开始调试项目，并对项目进行代码更改而无需分离调试器。 事实上，您可以通过任意方式开始调试项目、添加新类、向该类添加代码、将代码添加到创建该类的新实例并执行该类的方法的代码，所有这些都不需要分离调试器。 执行新的代码就像刷新浏览器一样简单！

单击此处查看 Visual Studio 2005 中 "编辑并继续" 功能的视频演练。

![](improvements-in-visual-studio-2005/_static/image2.png)

[打开全屏视频](improvements-in-visual-studio-2005/_static/editcontinue1.wmv)

ASP.NET 2.0 和 Visual Studio 2005 中的强大的 "编辑并继续" 功能是因为 ASP.NET 应用程序的体系结构更改。 在 ASP.NET 1.x 中，在 Visual Studio 2002/2003 中创建的应用程序编译为存储在/bin 文件夹中的主程序集。 应用程序的所有类、页等都编译到了一个 DLL 中。 然后，在运行时，ASP.NET 将编译页面内的所有控件、标记和 ASP.NET 代码，并将这些 Dll 复制到 ASP.NET 临时文件夹中。

在 Visual Studio 2005 中，使用 ASP.NET 2.0，上面的两个编译模型大纲（一个用于 Visual Studio，另一个用于运行时的 ASP.NET）已合并到一个公共编译模型中。 这意味着，在开发阶段（而不是运行时），所有编译问题都将被捕获。 它还允许对用户控件和母版页等功能进行设计和 IntelliSense 支持。

单击此处查看用户控件设计器支持的视频演练。

![](improvements-in-visual-studio-2005/_static/image3.png)

[打开全屏视频](improvements-in-visual-studio-2005/_static/usercontrols1.wmv)

> [!NOTE]
> 从页面中删除用户控件时，@Register 指令将保留在标记中，并且应手动删除，以避免在从网站中删除用户控件时出现分析器错误。

Visual Studio 编译模型中的另一项改进是 "发布网站" 功能。 由于发布功能对网站进行预编译，开发人员可享受到无需编译任何需求的附加性能。 它还将应用/_Code 文件夹中的所有源代码预编译为 DLL，以便不需要部署任何源代码。

!["发布网站" 对话框](improvements-in-visual-studio-2005/_static/image7.jpg)

**图 10**： "发布网站" 对话框

> [!NOTE]
> Aspnet/_compile .exe 实用程序还可以用于预编译 ASP.NET Web 应用程序。 此工具将在模块9中介绍。

发布网站时，预编译文件存储在临时 ASP.NET Files 文件夹中，如下所示。 具有*编译*文件扩展名的文件是为特定 dll 定义依赖项的 XML 文件。 任何 Webform 或用户控件都编译为以*App/_Web/_* 开头的随机 dll。

如果选中 "*允许更新此预编译站点以便进行更新*" 复选框，则 Webforms 和用户控件内的标记将不会预先编译为 DLL，使你可以在部署后进行更改。 如果你想要锁定标记，以便不允许对部署内容所做的更改，请取消选中此框。

"*使用固定命名和单页程序集*" 复选框允许您禁用批处理编译，以便将每个页编译为一个固定名称的程序集。 如果将此框保留为未选中状态，则可以利用批处理编译。

"对*预编译程序集启用强命名*" 复选框允许您对预编译的程序集进行强命名。

> [!NOTE]
> 在 ASP.NET 1.x 中，必须将具有强名称的程序集安装到全局程序集缓存（GAC）中。 在 ASP.NET 2.0 中，无需将强名称程序集安装到 GAC 中。

![ASP.NET 应用程序预编译文件](improvements-in-visual-studio-2005/_static/image8.jpg)

**图 11**： ASP.NET 应用程序预编译文件

> [!NOTE]
> 在上面的应用程序中，没有 web.config 文件。 如果有，则在发布网站进程后，它将被称为*PrecompiledApp。*

## <a name="improvements-in-deployment"></a>部署中的改进

与 Visual Studio 2002 和2003一样，Visual Studio 2005 还提供了一个复制项目功能。 但是，该功能已在 Visual Studio 2005 中 beefed，现在称为 "复制网站"。

"复制网站" 对话框拆分为左框架和右框架。 左框架称为源网站，右侧框架称为 "远程网站"。 其中一件事可能会混淆某些开发人员，正确框架中显示的站点不一定是远程站点。 它可以是本地文件系统上的站点或 IIS 的本地实例。 此外，左侧框架中显示的网站不一定是源网站，因为对话框允许您从远程网站*向*源网站发布。

如果要将项目复制到远程网站，则必须在该站点上安装 FrontPage 服务器扩展。 如果没有，则需要使用 FTP 进行连接。 另一方面，如果要将项目复制到本地 IIS 实例，则不需要 FrontPage 服务器扩展。

> [!NOTE]
> 如果尝试在本地 IIS 实例上创建新的网站，并安装 FrontPage 2002 服务器扩展，则将收到一条错误消息，告知你在 SharePoint 服务器上不支持创建网站。 在这种情况下，你可以选择安装 FrontPage 2000 服务器扩展或删除 FrontPage 服务器扩展。

单击此处查看 "复制网站" 功能的视频演练。

![](improvements-in-visual-studio-2005/_static/image4.png)

[打开全屏视频](improvements-in-visual-studio-2005/_static/copysite1.wmv)

## <a name="improvements-in-debugging"></a>调试改进

在 Visual Studio 2005 中进行调试有四项重要改进。

- 不能以非管理员身份在本地调试。
- 默认情况下，编译元素的 Debug 属性为 false。
- 远程调试设置和配置比以往更容易。
- 你现在可以调试通过 FTP 位置打开的网站。

## <a name="debugging-as-a-non-administrator"></a>作为非管理员调试

添加 ASP.NET 开发服务器允许非管理员轻松地立即调试 ASP.NET 应用程序。 当调试在本地文件系统上运行的 ASP.NET 应用程序时，Visual Studio 将在登录用户的上下文中启动 ASP.NET 开发服务器。 然后，该用户可以调试该应用程序，而无需进行任何其他配置。

## <a name="debug-is-false-by-default"></a>默认情况下，调试为 False

在 ASP.NET 1.x 中，web.config 文件的*编译*元素中的*debug*属性默认设置为*true* 。 在将应用程序部署到生产环境之前，始终建议开发人员将此特性设置为*false* ，但由于大多数开发人员并不完全了解将 debug 特性设置为 true 的结果，因此它们只是原样保留原样。

将 debug 属性设置为 true 时，最严重的问题是它禁用了网络批处理编译模型。 因此，每个页面都编译为单独的 DLL。 如果 Web 应用程序由数千个页面（而非闻所未闻）组成，这意味着该应用程序将创建数千个小的 Dll。 虽然这些 Dll 大小较小，但不会将其加载到内存中的任何特定位置。 因此，它们会导致系统内存碎片，并可能导致 OutOfMemoryException。

在 ASP.NET 2.0 中，debug 属性默认设置为 false。 正如您所看到的，当开发人员在 Visual Studio 2005 中调试 ASP.NET 应用程序时，系统将提示他们添加启用了调试的 web.config 文件。 这样做会产生与 ASP.NET 1.x 相同的缺点，但现在，开发人员可以清楚地警告，在将应用程序移至生产环境之前，应将该属性重置为 false。

## <a name="remote-debugging-setup-and-configuration"></a>远程调试设置和配置

在 Visual Studio 2002/2003 中，远程调试依赖于计算机调试管理器（wsdl.exe）和 vs7jit 进程。 因此，对于客户来说，排除远程调试问题通常是一个黑框，对于 PSS，这通常不是很好的做法。

Visual Studio 2005 消除了对 mdm 和 vs7jit 进程的依赖。 相反，它现在使用远程调试监视器服务（msvsmon）。

在 Visual Studio 2005 中远程调试的要求非常简单。 在调试之前，需要在远程服务器上运行 msvsmon。 你可以从 Visual Studio CD 安装远程调试监视器，也可以直接从共享运行 msvsmon，无需在 Web 服务器上安装任何内容。

运行 msvsmon 时，可能会抱怨阻止远程调试的端口。 幸运的是，你可以直接在警告对话框内取消阻止端口，如下所示。

![通知： Windows 防火墙正在阻止远程调试](improvements-in-visual-studio-2005/_static/image9.jpg)

**图 12**：通知： Windows 防火墙正在阻止远程调试

取消阻止调试所需的端口后，会看到远程调试监视器，如下所示。 通过此接口，你可以轻松监视连接和更改调试权限。

![远程调试监视器](improvements-in-visual-studio-2005/_static/image10.jpg)

**图 13**：远程调试监视器

还可以远程调试通过 FTP 打开的 Web 应用程序。 步骤与前面介绍的步骤相同。 但是，您需要指定一个基 URL 来浏览该模块，如上文所述。

## <a name="lab-2"></a>实验室2

## <a name="remote-debugging-with-visual-studio-2005"></a>用 Visual Studio 2005 进行远程调试

此实验室将引导你完成使用 Visual Studio 2005 的远程调试。

单击此处查看此实验的视频演练。

![](improvements-in-visual-studio-2005/_static/image5.png)

[打开全屏视频](improvements-in-visual-studio-2005/_static/remdebug1.wmv)

此实验要求您具有两台计算机，一个运行 Visual Studio 2005，另一个运行 IIS 5 或更高版本。

1. 打开 Visual Studio 2005 并在远程服务器上创建一个新网站。

> [!NOTE]
> 您可以在远程 IIS 实例或 FTP 上创建网站。

1. 在远程 Web 服务器上，使用 UNC 路径在开发计算机上查找 msvsmon 并执行它。  
 Msvsmon 的默认位置为//server/c $/Program Files/Microsoft Visual Studio 8/Common7/IDE/Remote 调试器/x86。
2. 如果系统提示您解除阻止用于远程调试的端口，请执行此操作。
3. 从开发计算机中，打开 default.aspx 的代码隐藏，并在 Page/_Load 方法中设置断点。
4. 开始从开发计算机进行调试。

应该按预期命中断点。

## <a name="aspnet-development-server"></a>ASP.NET Development Server

如前所述，Visual Studio 2005 附带了一个名为 ASP.NET 开发服务器的 Web 服务器。 （ASP.NET 开发服务器有时称为 Cassini。）此 Web 服务器是浏览和调试在文件系统上运行的 Web 应用程序的便捷方法。

ASP.NET 开发服务器是受限制的 Web 服务器。 它不允许远程连接，它不允许任何用户，而不是启动 Web 服务器的用户的任何请求。 它也不具备提供 ASP 页的功能。 仅提供 ASP.NET 资源和 HTML 资源（包括图像、CSS 文件等）。

ASP.NET 开发服务器可以通过命令行启动，方法是运行位于 c：/Windows/Webdev.webserver.exe/Framework/v2.0/v2.0/ */* / */* /* 的文件。 以下对话框显示可用的参数。

![](improvements-in-visual-studio-2005/_static/image11.jpg)

**图14**

> [!NOTE]
> 通过命令行显式启动时不支持 ASP.NET 开发服务器。
