---
uid: web-forms/overview/data-access/advanced-data-access-scenarios/protecting-connection-strings-and-other-configuration-information-cs
title: 保护连接字符串和其他配置信息（C#） |Microsoft Docs
author: rick-anderson
description: ASP.NET 应用程序通常将配置信息存储在 web.config 文件中。 此信息中的某些信息是敏感的，并保证受到保护。 通过定义 。
ms.author: riande
ms.date: 08/03/2007
ms.assetid: ad8dd396-30f7-4abe-ac02-a0b84422e5be
msc.legacyurl: /web-forms/overview/data-access/advanced-data-access-scenarios/protecting-connection-strings-and-other-configuration-information-cs
msc.type: authoredcontent
ms.openlocfilehash: 15970bee1e990d3a139673efe12486e08f79814c
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74573514"
---
# <a name="protecting-connection-strings-and-other-configuration-information-c"></a>保护连接字符串和其他配置信息 (C#)

作者： [Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载代码](https://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_73_CS.zip)或[下载 PDF](protecting-connection-strings-and-other-configuration-information-cs/_static/datatutorial73cs1.pdf)

> ASP.NET 应用程序通常将配置信息存储在 web.config 文件中。 此信息中的某些信息是敏感的，并保证受到保护。 默认情况下，不会向网站访问者提供此文件，但管理员或黑客可能会获得对 Web 服务器的文件系统的访问权限，并查看文件的内容。 在本教程中，我们将了解 ASP.NET 2.0 通过加密 Web.config 文件的各节来保护敏感信息。

## <a name="introduction"></a>简介

ASP.NET 应用程序的配置信息通常存储在名为 `Web.config`的 XML 文件中。 在这些教程中，我们已更新了几次 `Web.config`。 例如，在[第一个教程](../introduction/creating-a-data-access-layer-cs.md)中创建 `Northwind` 类型化的数据集时，会自动将连接字符串信息添加到 `<connectionStrings>` 部分的 `Web.config` 中。 稍后，在[母版页和站点导航](../introduction/master-pages-and-site-navigation-cs.md)教程中，我们手动更新 `Web.config`，添加一个 `<pages>` 元素，该元素指示项目中的所有 ASP.NET 页面都应使用 `DataWebControls` 主题。

由于 `Web.config` 可能包含敏感数据（如连接字符串），因此 `Web.config` 的内容在未经授权的查看器中保持安全和隐藏非常重要。 默认情况下，ASP.NET 引擎将处理对具有 `.config` 扩展的文件发出的任何 HTTP 请求，该引擎将返回图1所示的 "*此类型的页未提供*" 消息。 这意味着，访问者只需在浏览器的地址栏中输入 http://www.YourServer.com/Web.config ，就不能查看 `Web.config` 的文件内容。

[![通过浏览器访问 web.config 返回了此类型的页未提供消息](protecting-connection-strings-and-other-configuration-information-cs/_static/image2.png)](protecting-connection-strings-and-other-configuration-information-cs/_static/image1.png)

**图 1**：通过浏览器访问 `Web.config` 返回此类型的页未提供消息（[单击以查看完全大小的图像](protecting-connection-strings-and-other-configuration-information-cs/_static/image3.png)）

但是，如果攻击者能够找到允许她查看 `Web.config` 文件内容的其他攻击，该怎么办？ 攻击者使用此信息可以做什么，以及可以采取哪些步骤来进一步保护 `Web.config`中的敏感信息？ 幸运的是，`Web.config` 中的大部分部分都不包含敏感信息。 如果攻击者知道您的 ASP.NET 页面所使用的默认主题的名称，攻击者会 perpetrate 哪些损害？

但是，某些 `Web.config` 部分包含敏感信息，这些信息可能包括连接字符串、用户名、密码、服务器名称、加密密钥等。 此信息通常在以下 `Web.config` 部分中找到：

- `<appSettings>`
- `<connectionStrings>`
- `<identity>`
- `<sessionState>`

在本教程中，我们将介绍保护此类敏感配置信息的方法。 如我们所见，.NET Framework 版本2.0 包含一个受保护的配置系统，它使所选配置节以编程方式加密和解密。

> [!NOTE]
> 本教程最后介绍了从 ASP.NET 应用程序连接到数据库的 Microsoft 建议。 除了对连接字符串进行加密以外，还可以通过确保以安全的方式连接到数据库来帮助强化系统。

## <a name="step-1-exploring-aspnet-20-s-protected-configuration-options"></a>步骤1：浏览 ASP.NET 2.0 s 受保护的配置选项

ASP.NET 2.0 包含用于加密和解密配置信息的受保护配置系统。 这包括 .NET Framework 中可用于以编程方式加密或解密配置信息的方法。 受保护的配置系统使用[提供程序模型](http://aspnet.4guysfromrolla.com/articles/101905-1.aspx)，这允许开发人员选择使用哪种加密实现。

.NET Framework 附带了两个受保护的配置提供程序：

- [`RSAProtectedConfigurationProvider`](https://msdn.microsoft.com/library/system.configuration.rsaprotectedconfigurationprovider.aspx) -使用非对称[RSA 算法](http://en.wikipedia.org/wiki/Rsa)进行加密和解密。
- [`DPAPIProtectedConfigurationProvider`](https://msdn.microsoft.com/system.configuration.dpapiprotectedconfigurationprovider.aspx) -使用 Windows[数据保护 API （DPAPI）](https://msdn.microsoft.com/library/ms995355.aspx)进行加密和解密。

由于受保护的配置系统实现了提供程序的设计模式，因此，可以创建自己的受保护配置提供程序并将其插入应用程序。 有关此过程的详细信息，请参阅[实现受保护的配置提供程序](https://msdn.microsoft.com/library/wfc2t3az(VS.80).aspx)。

RSA 和 DPAPI 提供程序使用密钥进行加密和解密例程，这些密钥可以存储在计算机或用户级别。 如果 web 应用程序在其自己的专用服务器上运行，或者如果服务器上有多个应用程序需要共享加密信息，则计算机级别的密钥非常适合使用。 在共享托管环境中，用户级密钥是一种更安全的选项，在这种环境中，同一服务器上的其他应用程序应该无法对应用程序的受保护配置部分进行解密。

在本教程中，我们的示例将使用 DPAPI 提供程序和计算机级别的密钥。 具体而言，我们将在 `Web.config`中查看加密 `<connectionStrings>` 部分，尽管受保护的配置系统可用于对大多数 `Web.config` 部分进行加密。 有关使用用户级密钥或使用 RSA 提供程序的信息，请参阅本教程末尾的 "后续读取" 部分中的资源。

> [!NOTE]
> `RSAProtectedConfigurationProvider` 和 `DPAPIProtectedConfigurationProvider` 提供程序在 `machine.config` 文件中注册，并且提供程序名称分别为 `RsaProtectedConfigurationProvider` 和 `DataProtectionConfigurationProvider`。 加密或解密配置信息时，需要提供相应的提供程序名称（`RsaProtectedConfigurationProvider` 或 `DataProtectionConfigurationProvider`），而不是实际的类型名称（`RSAProtectedConfigurationProvider` 和 `DPAPIProtectedConfigurationProvider`）。 可以在 "`$WINDOWS$\Microsoft.NET\Framework\version\CONFIG`" 文件夹中找到 `machine.config` 文件。

## <a name="step-2-programmatically-encrypting-and-decrypting-configuration-sections"></a>步骤2：以编程方式加密和解密配置节

只需几行代码，我们就可以使用指定的提供程序对特定的配置节进行加密或解密。 这段代码在不久就会看到，只需以编程方式引用适当的配置节，调用其 `ProtectSection` 或 `UnprotectSection` 方法，然后调用 `Save` 方法来持久保存这些更改。 此外，.NET Framework 还提供了一个有用的命令行实用程序，可以加密和解密配置信息。 我们将在步骤3中探索此命令行实用工具。

为了说明如何以编程方式保护配置信息，让我们创建一个包含用于加密和解密 `Web.config`中 `<connectionStrings>` 节的按钮的 ASP.NET 页面。

首先打开 `AdvancedDAL` 文件夹中的 "`EncryptingConfigSections.aspx`" 页。 将 "TextBox" 控件从工具箱拖到设计器上，将其 `ID` 属性设置为 `WebConfigContents`，其 `TextMode` 属性设置为 `MultiLine`，并将其 `Width` 和 `Rows` 属性分别设置为95% 和15。 此 TextBox 控件将显示 `Web.config` 的内容，以便我们能够快速查看内容是否已加密。 当然，在实际应用程序中，您永远不希望显示 `Web.config`的内容。

在文本框下，添加名为 `EncryptConnStrings` 和 `DecryptConnStrings`的两个按钮控件。 设置其文本属性以对连接字符串进行加密和解密连接字符串。

此时，屏幕应类似于图2。

[![向页面添加一个文本框和两个按钮 Web 控件](protecting-connection-strings-and-other-configuration-information-cs/_static/image5.png)](protecting-connection-strings-and-other-configuration-information-cs/_static/image4.png)

**图 2**：向页面添加文本框和两个按钮 Web 控件（[单击以查看完全大小的图像](protecting-connection-strings-and-other-configuration-information-cs/_static/image6.png)）

接下来，需要编写代码，以便在第一次加载页面时加载和显示 "`WebConfigContents`" 文本框中 `Web.config` 的内容。 将以下代码添加到页的代码隐藏类中。 此代码将添加一个名为 `DisplayWebConfig` 的方法，并在 `false``Page.IsPostBack` 时从 `Page_Load` 事件处理程序调用该方法：

[!code-csharp[Main](protecting-connection-strings-and-other-configuration-information-cs/samples/sample1.cs)]

`DisplayWebConfig` 方法使用[`File` 类](https://msdn.microsoft.com/library/system.io.file.aspx)打开应用程序的 `Web.config` 文件、 [`StreamReader` 类](https://msdn.microsoft.com/library/system.io.streamreader.aspx)以将其内容读入字符串中，并使用[`Path` 类](https://msdn.microsoft.com/library/system.io.path.aspx)生成 `Web.config` 文件的物理路径。 这三个类都位于[`System.IO` 命名空间](https://msdn.microsoft.com/library/system.io.aspx)中。 因此，您需要将 `using` `System.IO` 语句添加到代码隐藏类的顶部，或者使用 `System.IO.` 为这些类名称添加前缀。

接下来，我们需要为这两个按钮控件添加事件处理程序 `Click` 事件，并添加必要的代码，以便使用计算机级密钥和 DPAPI 提供程序加密和解密 `<connectionStrings>` 部分。 在设计器中，双击每个按钮以在代码隐藏类中添加 `Click` 事件处理程序，然后添加以下代码：

[!code-csharp[Main](protecting-connection-strings-and-other-configuration-information-cs/samples/sample2.cs)]

这两个事件处理程序中使用的代码几乎完全相同。 它们都首先通过[`WebConfigurationManager` 类](https://msdn.microsoft.com/library/system.web.configuration.webconfigurationmanager.aspx)s [`OpenWebConfiguration` 方法](https://msdn.microsoft.com/library/system.web.configuration.webconfigurationmanager.openwebconfiguration.aspx)获取有关当前应用程序 `Web.config` 文件的信息。 此方法返回指定虚拟路径的 web 配置文件。 接下来，通过[`Configuration` 类](https://msdn.microsoft.com/library/system.configuration.configuration.aspx)的[`GetSection(sectionName)` 方法](https://msdn.microsoft.com/library/system.configuration.configuration.getsection.aspx)访问 `Web.config` 文件 s `<connectionStrings>` 部分，该方法返回[`ConfigurationSection`](https://msdn.microsoft.com/library/system.configuration.configurationsection.aspx)对象。

`ConfigurationSection` 对象包含一个[`SectionInformation` 属性](https://msdn.microsoft.com/library/system.configuration.configurationsection.sectioninformation.aspx)，该属性提供有关配置节的附加信息和功能。 如上面的代码所示，我们可以通过检查 `SectionInformation` 属性的 `IsProtected` 属性来确定配置节是否已加密。 此外，可以通过 `SectionInformation` 属性 `ProtectSection(provider)` 和 `UnprotectSection` 方法对节进行加密或解密。

`ProtectSection(provider)` 方法接受字符串作为输入，该字符串指定要在加密时使用的受保护配置提供程序的名称。 在 `EncryptConnString` 按钮 s 事件处理程序中，我们将 DataProtectionConfigurationProvider 传递到 `ProtectSection(provider)` 方法，以便使用 DPAPI 提供程序。 `UnprotectSection` 方法可以确定用于对配置节进行加密的访问接口，因此不需要任何输入参数。

调用 `ProtectSection(provider)` 或 `UnprotectSection` 方法后，必须调用 `Configuration` 对象[`Save` 方法](https://msdn.microsoft.com/library/system.configuration.configuration.save.aspx)来保存更改。 加密或解密配置信息并保存更改后，我们会调用 `DisplayWebConfig` 将更新的 `Web.config` 内容加载到 TextBox 控件中。

输入以上代码后，通过浏览器访问 `EncryptingConfigSections.aspx` 页面进行测试。 最初应该会看到一个页面，其中列出了以纯文本形式显示的 `<connectionStrings>` 部分 `Web.config` 的内容（请参阅图3）。

[![向页面添加一个文本框和两个按钮 Web 控件](protecting-connection-strings-and-other-configuration-information-cs/_static/image8.png)](protecting-connection-strings-and-other-configuration-information-cs/_static/image7.png)

**图 3**：向页面添加文本框和两个按钮 Web 控件（[单击以查看完全大小的图像](protecting-connection-strings-and-other-configuration-information-cs/_static/image9.png)）

现在，单击 "加密连接字符串" 按钮。 如果启用了请求验证，则从 "`WebConfigContents`" 文本框中回发的标记将生成一个 `HttpRequestValidationException`，其中显示消息 "从客户端检测到潜在危险的 `Request.Form` 值"。 默认情况下，在 ASP.NET 2.0 中启用了请求验证，这将禁止包含未编码的 HTML 的回发，并旨在帮助防止脚本注入攻击。 可以在页面或应用程序级别禁用此检查。 若要关闭此页，请在 `@Page` 指令中将 `ValidateRequest` 设置设置为 `false`。 `@Page` 指令位于页面声明性标记的顶部。

[!code-aspx[Main](protecting-connection-strings-and-other-configuration-information-cs/samples/sample3.aspx)]

有关请求验证、其用途、如何在页级和应用程序级禁用它的详细信息，以及如何对标记进行 HTML 编码的详细信息，请参阅[请求验证-阻止脚本攻击](../../../../whitepapers/request-validation.md)。

为页面禁用请求验证后，请尝试再次单击 "加密连接字符串" 按钮。 在回发时，将访问配置文件，并使用 DPAPI 提供程序对其 `<connectionStrings>` 部分进行加密。 然后，将更新文本框以显示新的 `Web.config` 内容。 如图4所示，`<connectionStrings>` 信息现在已加密。

[![单击 "加密连接字符串" 按钮会对 &lt;connectionString&gt; 节进行加密](protecting-connection-strings-and-other-configuration-information-cs/_static/image11.png)](protecting-connection-strings-and-other-configuration-information-cs/_static/image10.png)

**图 4**：单击 "加密连接字符串" 按钮将加密 `<connectionString>` 部分（[单击以查看完全大小的图像](protecting-connection-strings-and-other-configuration-information-cs/_static/image12.png)）

我的计算机上生成的加密 `<connectionStrings>` 部分如下所示，不过为了简洁起见，`<CipherData>` 元素中的某些内容已被删除：

[!code-xml[Main](protecting-connection-strings-and-other-configuration-information-cs/samples/sample4.xml)]

> [!NOTE]
> `<connectionStrings>` 元素指定用于执行加密的提供程序（`DataProtectionConfigurationProvider`）。 当单击 "解密连接字符串" 按钮时，`UnprotectSection` 方法将使用此信息。

从 `Web.config` 访问连接字符串信息时，可以通过从 SqlDataSource 控件编写的代码，或者从类型化数据集中的 Tableadapter 中自动生成的代码-它会自动解密。 简而言之，我们不需要添加任何其他代码或逻辑来解密已加密的 `<connectionString>` 部分。 为了说明这一点，请访问前面的教程之一，如基本报表部分（`~/BasicReporting/SimpleDisplay.aspx`）中的简单显示教程。 如图5所示，本教程的工作方式与预期的方式完全相同，指出加密的连接字符串信息通过 ASP.NET 页自动解密。

[![，数据访问层会自动解密连接字符串信息](protecting-connection-strings-and-other-configuration-information-cs/_static/image14.png)](protecting-connection-strings-and-other-configuration-information-cs/_static/image13.png)

**图 5**：数据访问层自动对连接字符串信息进行解密（[单击以查看完全大小的图像](protecting-connection-strings-and-other-configuration-information-cs/_static/image15.png)）

若要将 `<connectionStrings>` 部分恢复为其纯文本表示形式，请单击 "解密连接字符串" 按钮。 在回发时，以纯文本形式显示 `Web.config` 中的连接字符串。 此时，屏幕应类似于第一次访问此页面时（请参阅图3）。

## <a name="step-3-encrypting-configuration-sections-usingaspnet_regiisexe"></a>步骤3：使用`aspnet_regiis.exe` 加密配置节

.NET Framework 包括 `$WINDOWS$\Microsoft.NET\Framework\version\` 文件夹中的各种命令行工具。 例如，在[使用 Sql 缓存依赖项](../caching-data/using-sql-cache-dependencies-cs.md)教程中，我们介绍了如何使用 `aspnet_regsql.exe` 命令行工具添加 SQL 缓存依赖关系所需的基础结构。 此文件夹中的另一个有用的命令行工具是[ASP.NET IIS 注册工具（`aspnet_regiis.exe`）](https://msdn.microsoft.com/library/k6h9cz8h(VS.80).aspx)。 顾名思义，ASP.NET IIS 注册工具主要用于将 ASP.NET 2.0 应用程序注册到 Microsoft 的专业级 Web 服务器（IIS）。 除了与 IIS 相关的功能之外，还可以使用 ASP.NET IIS 注册工具对 `Web.config`中指定的配置节进行加密或解密。

以下语句显示了使用 `aspnet_regiis.exe` 命令行工具对配置节进行加密的一般语法：

[!code-console[Main](protecting-connection-strings-and-other-configuration-information-cs/samples/sample5.cmd)]

*部分*是要加密的配置节（如 connectionStrings），*物理\_目录*是 web 应用程序根目录的完整物理路径，*提供程序*是要使用的受保护配置提供程序的名称（例如 DataProtectionConfigurationProvider）。 或者，如果 web 应用程序是在 IIS 中注册的，则可以使用以下语法输入虚拟路径而不是物理路径：

[!code-console[Main](protecting-connection-strings-and-other-configuration-information-cs/samples/sample6.cmd)]

以下 `aspnet_regiis.exe` 示例使用具有计算机级密钥的 DPAPI 提供程序对 `<connectionStrings>` 部分进行加密：

[!code-console[Main](protecting-connection-strings-and-other-configuration-information-cs/samples/sample7.cmd)]

同样，`aspnet_regiis.exe` 命令行工具可用于解密配置节。 使用 `-pdf` （或代替 `-pe`，使用 `-pd`），而不是使用 `-pef` 开关。 另请注意，解密时不需要提供程序名称。

[!code-console[Main](protecting-connection-strings-and-other-configuration-information-cs/samples/sample8.cmd)]

> [!NOTE]
> 由于我们使用的是使用特定于计算机的密钥的 DPAPI 提供程序，因此你必须从提供 web 页面的同一台计算机上运行 `aspnet_regiis.exe`。 例如，如果在本地开发计算机上运行此命令行程序，然后将加密的 Web.config 文件上传到生产服务器，则生产服务器将无法对连接字符串信息进行解密，因为它已加密使用特定于您的开发计算机的密钥。 RSA 提供程序没有此限制，因为可以将 RSA 密钥导出到另一台计算机。

## <a name="understanding-database-authentication-options"></a>了解数据库身份验证选项

在任何应用程序都可以发出对 Microsoft SQL Server 数据库 `SELECT`、`INSERT`、`UPDATE`或 `DELETE` 查询之前，数据库必须首先识别请求者。 此过程称为*身份验证*，SQL Server 提供了两种身份验证方法：

- **Windows 身份验证**-用于运行应用程序的进程用于与数据库通信。 当通过 Visual Studio 2005 s ASP.NET 开发服务器运行 ASP.NET 应用程序时，ASP.NET 应用程序会假定当前登录的用户的标识。 对于 Microsoft Internet Information Server （IIS）上的 ASP.NET 应用程序，ASP.NET 应用程序通常假定 `domainName``\MachineName` 或 `domainName``\NETWORK SERVICE`的标识，尽管可以对此进行自定义。
- **SQL 身份验证**-提供用户 ID 和密码值作为身份验证凭据。 通过 SQL 身份验证，在连接字符串中提供用户 ID 和密码。

Windows 身份验证优于 SQL 身份验证，因为它更安全。 使用 Windows 身份验证时，无用户名和密码即可使用连接字符串，如果 web 服务器和数据库服务器驻留在两个不同的计算机上，则不会通过网络以纯文本形式发送凭据。 但是，通过 SQL 身份验证，在连接字符串中对身份验证凭据进行硬编码，并以纯文本形式从 web 服务器传输到数据库服务器。

这些教程使用了 Windows 身份验证。 可以通过检查连接字符串来判断正在使用的身份验证模式。 教程的 `Web.config` 中的连接字符串已：

`Data Source=.\SQLEXPRESS; AttachDbFilename=|DataDirectory|\NORTHWND.MDF; Integrated Security=True; User Instance=True`

集成安全性 = True，缺少用户名和密码表示正在使用 Windows 身份验证。 在某些连接字符串中，术语 "可信连接 = 是" 或 "集成安全性 = SSPI"，而不是集成安全性 = "True"，但所有这三个都表示使用 Windows 身份验证。

下面的示例演示使用 SQL 身份验证的连接字符串。 请注意嵌入在连接字符串中的凭据：

`Server=serverName; Database=Northwind; uid=userID; pwd=password`

假设攻击者能够查看应用程序的 `Web.config` 文件。 如果使用 SQL 身份验证连接到可通过 Internet 访问的数据库，则攻击者可以使用此连接字符串通过 SQL Management Studio 或从其自己的网站上的 ASP.NET 页连接到您的数据库。 为了帮助减轻此威胁，请使用受保护的配置系统加密 `Web.config` 中的连接字符串信息。

> [!NOTE]
> 有关 SQL Server 中可用的不同身份验证类型的详细信息，请参阅[构建安全的 ASP.NET 应用程序：身份验证、授权和安全通信](https://msdn.microsoft.com/library/aa302392.aspx)。 若要进一步了解 Windows 和 SQL 身份验证语法之间的差异，请参阅[ConnectionStrings.com](http://www.connectionstrings.com/)。

## <a name="summary"></a>总结

默认情况下，不能通过浏览器访问 ASP.NET 应用程序中扩展名为 `.config` 的文件。 不会返回这些类型的文件，因为它们可能包含敏感信息，例如数据库连接字符串、用户名和密码等。 .NET 2.0 中的受保护配置系统通过允许加密指定的配置节来帮助进一步保护敏感信息。 有两个内置的受保护配置提供程序：一个使用 RSA 算法，另一个使用 Windows 数据保护 API （DPAPI）。

在本教程中，我们介绍了如何使用 DPAPI 提供程序加密和解密配置设置。 这可以通过编程方式完成，如我们在步骤2中看到的那样，还可以通过 `aspnet_regiis.exe` 命令行工具完成，如步骤3中所述。 若要详细了解如何使用用户级密钥或使用 RSA 提供程序，请参阅进一步阅读部分中的资源。

很高兴编程！

## <a name="further-reading"></a>其他阅读材料

有关本教程中讨论的主题的详细信息，请参阅以下资源：

- [构建安全的 ASP.NET 应用程序：身份验证、授权和安全通信](https://msdn.microsoft.com/library/aa302392.aspx)
- [加密 ASP.NET 2.0 应用程序中的配置信息](http://aspnet.4guysfromrolla.com/articles/021506-1.aspx)
- [在 ASP.NET 2.0 中加密 `Web.config` 值](https://weblogs.asp.net/scottgu/archive/2006/01/09/434893.aspx)
- [如何：使用 DPAPI 加密 ASP.NET 2.0 中的配置节](https://msdn.microsoft.com/library/ms998280.aspx)
- [如何：使用 RSA 加密 ASP.NET 2.0 中的配置节](https://msdn.microsoft.com/library/ms998283.aspx)
- [.NET 2.0 中的配置 API](http://www.odetocode.com/Articles/418.aspx)
- [Windows 数据保护](https://msdn.microsoft.com/library/ms995355.aspx)

## <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，创始人的[4GuysFromRolla.com](http://www.4guysfromrolla.com)，已在使用 Microsoft Web 技术，自1998开始。 Scott 的工作方式是独立的顾问、培训师和撰稿人。 他的最新书籍是，[*在24小时内，sam ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 可以[mitchell@4GuysFromRolla.com访问。](mailto:mitchell@4GuysFromRolla.com) 或通过他的博客，可以在[http://ScottOnWriting.NET](http://ScottOnWriting.NET)找到。

## <a name="special-thanks-to"></a>特别感谢

此教程系列由许多有用的审阅者查看。 本教程的主管评审者是 Teresa Murphy 和 Randy Schmidt。 想要查看我即将发布的 MSDN 文章？ 如果是这样，请在mitchell@4GuysFromRolla.com放置一行[。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一页](configuring-the-data-access-layer-s-connection-and-command-level-settings-cs.md)
> [下一页](debugging-stored-procedures-cs.md)
