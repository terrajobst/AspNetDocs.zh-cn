---
uid: whitepapers/aspnet-and-iis6
title: 运行带有 IIS 6.0 的 ASP.NET 1.1 |Microsoft Docs
author: rick-anderson
description: 虽然 Windows Server 2003 同时包含 IIS 6.0 和 ASP.NET 1.1，但默认情况下这些组件处于禁用状态。 本白皮书介绍了如何启用 IIS 6.0 。
ms.author: riande
ms.date: 02/10/2010
ms.assetid: 5a5537bf-2aaa-49e7-839f-9e6522b829d8
msc.legacyurl: /whitepapers/aspnet-and-iis6
msc.type: content
ms.openlocfilehash: 2e7812f34481afe9a71927c0d9ba2a9abc9632e4
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78419846"
---
# <a name="running-aspnet-11-with-iis-60"></a>通过 IIS 6.0 运行 ASP.NET 1.1

> 虽然 Windows Server 2003 同时包含 IIS 6.0 和 ASP.NET 1.1，但默认情况下这些组件处于禁用状态。 本白皮书介绍了如何启用 IIS 6.0 和 ASP.NET 1.1，并建议使用几个配置设置来获得 IIS 和 ASP.NET 的最佳性能。
> 
> 适用于 ASP.NET 1.1 和 IIS 6.0。

ASP.NET 1.1 附带 Windows Server 2003，其中还包括最新版本的 Internet Information Server （IIS）版本6.0。 IIS 6.0 和 ASP.NET 1.1 设计为无缝集成，而 ASP.NET 现在默认为新的 IIS 6.0 工作进程模型。

## <a name="aspnet-11-is-not-installed-by-default"></a>默认情况下未安装 ASP.NET 1。1

与早期版本的 Microsoft 服务器操作系统不同，默认情况下不启用 Internet Information Server （IIS）;也不是 ASP.NET 1.1。 有两个选项可用于启用 IIS：

### <a name="enabling-iis-option-1---configure-your-server-wizard"></a>启用 IIS，选项 #1-配置服务器向导

Windows Server 2003 提供了一个新的 "配置您的服务器向导"，以帮助您以所需的模式正确配置您的服务器。

若要启动向导-注意若要运行向导，必须以管理员身份登录： "开始" |程序 |"管理工具"，然后选择 "配置服务器"。

选择后，您应该会看到 "配置您的服务器向导" 打开屏幕：

![](aspnet-and-iis6/_static/image1.jpg)

单击 "下一 &gt;"：

![](aspnet-and-iis6/_static/image2.jpg)

单击 "下一 &gt;"

![](aspnet-and-iis6/_static/image3.jpg)

在此屏幕上，需要选择 "应用程序服务器（IIS、ASP.NET）" 作为要配置的选项。

单击 "下一 &gt;"。

![](aspnet-and-iis6/_static/image4.jpg)

选择将服务器配置为应用程序服务器后，将显示此屏幕，提示应安装的其他功能。 默认情况下，这两个选项都处于选中状态。 若要自动启用 ASP.NET，需要选择 "启用 ASP"。NET "。

单击 "下一 &gt;"。

![](aspnet-and-iis6/_static/image5.jpg)

此屏幕显示要安装的选项。

单击 "下一 &gt;"。

![](aspnet-and-iis6/_static/image6.jpg)

当你选择的选项正在安装时，你将看到此屏幕。 安装服务时，显示其他对话框是正常现象。 系统还会提示你输入 Windows 2003 服务器安装 CD 的位置。

完成后单击 "下一 &gt;"。

![](aspnet-and-iis6/_static/image7.jpg)

单击 "完成"-Windows Server 2003 现已配置为支持 IIS 6.0 和 ASP.NET 1.1。

### <a name="enabling-iis-option-2---manually-configuring-iis-and-aspnet"></a>启用 IIS，选项 #2-手动配置 IIS 和 ASP.NET

如果您不希望使用 "配置您的服务器向导"，则可以选择使用控制面板中的 "添加或删除程序" 来安装 IIS 6.0 和 ASP.NET 1.1。

首先，打开 "控制面板"：

![](aspnet-and-iis6/_static/image8.jpg)

接下来，单击 "添加/删除 Windows 组件"，这将打开 "Windows 组件向导"：

![](aspnet-and-iis6/_static/image9.jpg)

突出显示并选中 "应用程序服务器"，然后单击 "详细信息" 鼠标

![](aspnet-and-iis6/_static/image10.jpg)

若要安装 ASP.NET，请选中 "ASP"。NET "。

单击 "确定" 以返回到 Windows 组件向导。 在 Windows 组件向导中单击 "下一 &gt;" 开始安装：

![](aspnet-and-iis6/_static/image11.jpg)

安装服务时，显示其他对话框是正常现象。 系统还会提示你输入 Windows 2003 服务器安装 CD 的位置。

安装完成后，你将看到 "Windows 组件向导" 的最后一个屏幕：

![](aspnet-and-iis6/_static/image12.jpg)

IIS 6.0 和 ASP.NET 1.1 现在已配置并且可用。

## <a name="recommended-settings"></a>建议的设置

当使用 IIS 6.0 运行 ASP.NET 1.1 时，建议使用几个配置设置从 ASP.NET 获得最佳性能：

- 配置工作进程内存限制
- 配置工作进程回收

### <a name="configuring-worker-process-memory-limits"></a>配置工作进程内存限制

默认情况下，IIS 6.0 不会对允许 IIS 使用的内存量设置限制。 ASP.NET.NET 的缓存功能依赖于内存的限制，因此缓存可以主动地从内存中删除未使用的项。

建议配置 IIS 6.0 的内存回收功能。 若要配置此打开的 Internet Information Services 管理器（开始 |程序 |管理工具 |Internet Information Services）。 打开后，展开 "应用程序池" 文件夹：

对于每个应用程序池：

![](aspnet-and-iis6/_static/image13.jpg)

1. 右键单击应用程序池，例如 "DefaultAppPool"，然后选择 "属性"：

![](aspnet-and-iis6/_static/image14.jpg)

2. 接下来，单击 "最大使用的内存（mb）：" 以启用内存回收。 此值不应大于服务器上的物理（非虚拟）内存量，良好的近似值是物理内存的60%，即，对于具有512MB 的物理内存的服务器，选择310。 使用2GB 地址空间时，还建议最大值不能超过800MB。 如果服务器的内存地址空间为3GB，则工作进程的最大内存限制可以高达1，800MB：

![](aspnet-and-iis6/_static/image15.jpg)

单击 "应用"，然后单击 "确定" 退出属性对话框。 对所有可用的应用程序池重复此操作。

### <a name="configuring-worker-recycling"></a>配置辅助角色回收

默认情况下，IIS 6.0 配置为每29小时回收其工作进程。 这对运行 ASP.NET 的应用程序来说有点迫切，建议禁用自动工作进程回收。

若要禁用自动工作进程回收，请先打开 Internet Information Services Manager （开始 |程序 |管理工具 |Internet Information Services）。 打开后，展开 "应用程序池" 文件夹：

![](aspnet-and-iis6/_static/image16.jpg)

对于每个应用程序池：

1. 右键单击应用程序池，例如 "DefaultAppPool"，然后选择 "属性"：

![](aspnet-and-iis6/_static/image17.jpg)

2. 取消选中 "回收工作进程（分钟）："：

![](aspnet-and-iis6/_static/image18.jpg)

单击 "应用"，然后单击 "确定" 退出属性对话框。 对所有可用的应用程序池重复此操作。

## <a name="granting-write-access-to-the-file-system"></a>授予对文件系统的写访问权限

如果你的应用程序需要对文件系统的写入访问权限，并且你使用的是 NTFS，则需要修改文件夹或文件上的访问控制列表（ACL），以授予对的 ASP.NET 访问权限。

例如，若要授予 ASP.NET 对 c:\inetpub\wwwroot 的写入访问权限，请先打开资源管理器，然后导航到该目录：

![](aspnet-and-iis6/_static/image19.jpg)

接下来，右键单击目录，例如 "wwwroot"，然后选择 "属性"。 "属性" 对话框打开后，选择 "安全" 选项卡：

![](aspnet-and-iis6/_static/image20.jpg)

C:\inetpub\wwwroot\ 目录是一个特殊的目录，其中已授予特殊 IIS 6.0 组 "IIS\_WPG" 的读取 &amp; 执行、列出文件夹内容和读取权限。 但是，若要授予写入权限，需要单击 "写入时允许" 复选框：

![](aspnet-and-iis6/_static/image21.jpg)

IIS 6.0 现在对此文件夹具有写入权限。 若要授予对其他文件夹的写权限，请按照以下步骤进行操作：注意，如果 IIS\_WPG 组尚不存在，则可能需要将其添加。

> [!CAUTION]
> 为 IIS\_WPG 授予写入权限将允许任何 ASP.NET 应用程序写入此目录。

## <a name="supporting-integrated-authentication-with-sql-server"></a>支持 SQL Server 的集成身份验证

集成身份验证允许 SQL Server 利用 Windows NT 身份验证来验证 SQL Server 登录帐户。 这允许用户绕过标准 SQL Server 登录过程。 使用此方法，网络用户无需提供单独的登录标识或密码即可访问 SQL Server 数据库，因为 SQL Server 从 Windows NT 网络安全过程获取用户和密码信息。

为 ASP.NET 应用程序选择 "集成身份验证" 是一个不错的选择，因为你的应用程序的连接字符串中没有存储任何凭据。 相反，用于连接到 SQL 的连接字符串将如下所示：

`"server=localhost; database=Northwind;Trusted_Connection=true"`

此连接字符串通知 SQL Server 使用尝试访问 SQL Server 的应用程序的 Windows 凭据。 对于 ASP.NET/IIS 6，这是 IIS\_WPG 组中的帐户。

若要在 SQL Server 与 ASP.NET 之间启用集成身份验证，需要首先确保已将 SQL Server 配置为使用集成身份验证或混合模式身份验证-请检查你的 DBA 以确定这一点。 如果 SQL Server 采用这两种模式之一，则可以使用集成身份验证。

打开 SQL Server Enterprise 管理器（开始 |程序 |Microsoft SQL Server |企业管理器）中，选择适当的服务器，然后展开 "安全性" 文件夹：

![](aspnet-and-iis6/_static/image22.jpg)

如果未列出 "BUILTINT\IIS\_WPG" 组，请右键单击 "登录名"，然后选择 "新建 Login：

![](aspnet-and-iis6/_static/image23.jpg)

在 "名称：" 文本框中，输入 "[Server/Domain Name] \IIS\_WPG" 或单击省略号按钮以打开 Windows NT 用户/组选取器：

![](aspnet-and-iis6/_static/image24.jpg)

选择当前计算机的 IIS\_WPG 组，然后单击 "添加"，然后单击 "确定" 以关闭选取器。

然后还需要设置默认数据库和访问数据库的权限。 若要设置默认数据库，请从下拉列表中选择，例如 "Northwind：

![](aspnet-and-iis6/_static/image25.jpg)

接下来，单击 "数据库访问" 选项卡：

![](aspnet-and-iis6/_static/image26.jpg)

单击要允许访问的每个数据库的 "允许" 复选框。 还需要选择数据库角色，检查 db\_所有者将确保您的登录名具有管理和使用所选数据库所需的所有权限。

单击 "确定" 退出属性对话框。 现在，你的 ASP.NET 应用程序已配置为支持集成 SQL Server 身份验证。

## <a name="dont-run-aspnet-10-in-iis-60-native-mode"></a>不要在 IIS 6.0 本机模式下运行 ASP.NET 1。0

Iis 6.0 上的 ASP.NET 1.0 仅在 IIS 5 兼容模式下受支持。

若要将 ASP.NET 1.0 配置为在 IIS 5.0 兼容模式下运行，请打开 Internet 服务管理器并右键单击 "网站"，然后选择 "属性"：

![](aspnet-and-iis6/_static/image27.jpg)

切换到 "服务" 选项卡并检查？在 IIS 5.0 隔离模式下运行 WWW 服务？：

![](aspnet-and-iis6/_static/image28.jpg)
