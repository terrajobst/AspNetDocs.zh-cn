---
uid: aspnet/overview/developing-apps-with-windows-azure/maintainable-azure-websites-managing-change-and-scale
title: 动手实验：可维护 Azure 网站：管理更改和缩放 |Microsoft Docs
author: rick-anderson
description: 在此实验室中，了解 Microsoft Azure 如何轻松地构建网站并将其部署到生产环境。
ms.author: riande
ms.date: 07/16/2014
ms.assetid: ecfd0eb4-c4ad-44e6-9db9-a2a66611ff6a
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/maintainable-azure-websites-managing-change-and-scale
msc.type: authoredcontent
ms.openlocfilehash: c88bae40a8aa092037c0b359ee391acaf161cf10
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78506372"
---
# <a name="hands-on-lab-maintainable-azure-websites-managing-change-and-scale"></a>动手实验：可维护 Azure 网站：管理更改和缩放

由[Web 训练营团队](https://twitter.com/webcamps)使用

[下载 Web 训练营培训工具包](https://aka.ms/webcamps-training-kit)

> Microsoft Azure 可以轻松地构建网站并将其部署到生产环境。 但当您的应用程序处于活动中时，您就会开始吧！ 需要处理不断变化的要求、数据库更新、规模等。 幸运的是，Azure App Service 都包含了一些功能，可帮助您保持站点顺利运行。
>
> Azure 为任意规模的 web 应用程序提供安全而灵活的开发、部署和扩展选项。 利用现有工具创建和部署应用程序，而无需管理基础结构。
>
> 使用最喜欢的开发工具轻松部署创建的内容，以分钟为单位轻松预配生产 web 应用程序。 可以直接从源代码管理部署现有网站，支持**Git**、 **GitHub**、 **Bitbucket**、 **TFS**甚至**DropBox**。 在 Windows 中使用 PowerShell 或在任何 OS 上运行的**CLI**工具中使用**PowerShell**直接从你喜欢的 IDE 或脚本进行部署。 部署完成后，使你的网站始终保持最新状态，并支持连续部署。
>
> Azure 为任何数据（大或小）提供可缩放、持久的云存储、备份和恢复解决方案。 将应用程序部署到生产环境时，存储服务（如表、Blob 和 SQL 数据库）可帮助你在云中扩展应用程序。
>
> 在 SQL 数据库中，当部署应用程序的新版本时，重要的是使您的生产数据库保持最新。 感谢您**Entity Framework Code First 迁移**，您的数据模型的开发和部署已经过简化，只需几分钟就能更新您的环境。 此动手实验将向你显示在 Microsoft Azure 中将 web 应用部署到生产环境时可能会遇到的不同主题。
>
> 所有示例代码和代码段都包含在 Web 训练营培训工具包中， [https://aka.ms/webcamps-training-kit](https://aka.ms/webcamps-training-kit)提供。
>
> 若要深入了解本主题，请参阅[利用 Azure 电子书构建实际的云应用](building-real-world-cloud-apps-with-windows-azure/introduction.md)。

<a id="Overview"></a>
## <a name="overview"></a>概述

<a id="Objectives"></a>
### <a name="objectives"></a>目标

在本动手实验中，您将了解如何：

- 使用现有模型启用实体框架迁移
- 使用实体框架迁移相应地更新对象模型和数据库
- 使用 Git 部署到 Azure App Service
- 使用 Azure 管理门户回滚到以前的部署
- 使用 Azure 存储缩放 web 应用
- 使用 Azure 管理门户配置 web 应用的自动缩放
- 在 Visual Studio 中创建和配置负载测试项目

<a id="Prerequisites"></a>
### <a name="prerequisites"></a>系统必备

完成本动手实验需要以下各项：

- Web 或更高版本[的 Visual Studio Express 2013](https://www.microsoft.com/visualstudio/)
- [用于 .NET 的 Azure SDK 2。2](https://www.microsoft.com/windowsazure/sdk/)
- [GIT 版本控制系统](http://git-scm.com/download)
- Microsoft Azure 订阅

    - 注册[免费试用版](https://aka.ms/watk-freetrial)
    - 如果你是 Visual Studio Professional，请 Test Professional、高级或旗舰版（MSDN 或 MSDN 平台订阅者）立即激活你的[msdn 权益](https://aka.ms/watk-msdn)，开始在 Azure 上进行开发和测试
    - [BizSpark](https://aka.ms/watk-bizspark)成员通过其 Visual Studio Ultimate with MSDN 订阅自动获得 Azure 权益
    - [Microsoft 合作伙伴网络](https://aka.ms/watk-mpn)Cloud Essentials 计划的成员免费接收每月 Azure 额度

<a id="Setup"></a>
### <a name="setup"></a>安装

若要运行此动手实验中的练习，您需要先设置您的环境。

1. 打开 Windows 资源管理器并浏览到实验室的**源**文件夹。
2. 右键单击 " **setup.exe** "，然后选择 "以**管理员身份运行**" 以启动安装过程，该过程将配置环境并安装 Visual Studio code 代码段。
3. 如果显示“用户帐户控制”对话框，请确认操作以继续。

> [!NOTE]
> 确保在运行安装过程之前，您已检查本实验的所有依赖项。

<a id="CodeSnippets"></a>
### <a name="using-the-code-snippets"></a>使用代码段

在整个实验文档中，将指示您插入代码块。 为方便起见，此代码的大部分作为 Visual Studio Code 代码段提供，你可以从 Visual Studio 2013 中访问这些代码段，以避免手动添加它。

> [!NOTE]
> 每个练习都附带了一个起始解决方案，该解决方案位于练习的 "**开始**" 文件夹中，使您可以单独执行每个练习。 请注意，这些开始解决方案中缺少在练习中添加的代码段，并且在完成此练习之前，可能无法工作。 在练习的源代码中，还会找到一个包含 Visual Studio 解决方案的**结束**文件夹，该解决方案的代码是完成相应练习中的步骤所产生的。 如果您在演练本动手实验时需要其他帮助，则可以使用这些解决方案作为指南。

---

<a id="Exercises"></a>
## <a name="exercises"></a>练习

本动手实验包括以下练习：

1. [使用实体框架迁移](#Exercise1)
2. [将 Web 应用部署到过渡环境](#Exercise2)
3. [在生产环境中执行部署回滚](#Exercise3)
4. [使用 Azure 存储进行缩放](#Exercise4)
5. [对 Web 应用使用自动缩放](#Exercise5)（适用于 Visual Studio 2013 旗舰版）

完成本实验的估计时间： **75 分钟**

> [!NOTE]
> 首次启动 Visual Studio 时，必须选择一个预定义的设置集合。 每个预定义的集合都设计为与特定的开发风格相匹配，并确定窗口布局、编辑器行为、IntelliSense 代码段和对话框选项。 此实验室中的过程描述在使用**常规开发设置**集合时，在 Visual Studio 中完成给定任务所需执行的操作。 如果为开发环境选择了其他设置集合，则需要考虑的步骤可能会有所不同。

<a id="Exercise1"></a>
### <a name="exercise-1-using-entity-framework-migrations"></a>练习1：使用实体框架迁移

开发应用程序时，数据模型可能会随时间而改变。 这些更改可能会影响数据库中的现有模型（如果要创建新的版本），并且必须保持数据库的最新状态，以防出现错误。

为了简化模型中对这些更改的跟踪， **Entity Framework Code First 迁移**自动检测与数据库架构比较模型的更改，并生成特定代码来更新数据库，从而创建新*版本*的数据库。

本练习演示如何为应用程序启用**迁移**，以及如何轻松地检测和生成更改来更新数据库。

<a id="Ex1Task1"></a>
#### <a name="task-1--enabling-migrations"></a>任务1–启用迁移

在此任务中，您将完成为**书呆子测验**数据库启用**Entity Framework Code First 迁移**的步骤，更改模型并了解这些更改在数据库中的反射方式。

1. 打开 Visual Studio，并从**Source\Ex1-UsingEntityFrameworkMigrations\Begin**打开**GeekQuiz**解决方案文件。
2. 构建解决方案以便下载并安装**NuGet**程序包依赖项。 为此，请右键单击该解决方案，然后单击 "**生成解决方案**" 或按**Ctrl + Shift + B**。
3. 在 Visual Studio 的 "**工具**" 菜单中，选择 " **NuGet 包管理器**"，然后单击 "**程序包管理器控制台**"。
4. 在 "**程序包管理器控制台**" 中，输入以下命令，然后按**enter**。 将创建基于现有模型的初始迁移。

    [!code-powershell[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample1.ps1)]

    ![启用迁移](maintainable-azure-websites-managing-change-and-scale/_static/image1.png "启用迁移")

    *启用迁移*

    > [!NOTE]
    > 此命令向书呆子阅卷项目添加一个包含名为**Configuration.cs**的文件的**迁移**文件夹。 **配置**类允许配置迁移对上下文的行为方式。
5. 启用迁移后，需要更新**配置**类，以便用**书呆子测验**所需的初始数据填充数据库。 在 "**迁移**" 下，将**Configuration.cs**文件替换为位于此实验室的**Source\Assets**文件夹中的文件。

    > [!NOTE]
    > 因为**迁移**将对每个数据库更新调用**Seed**方法，所以需要确保在数据库中不会复制记录。 **AddOrUpdate**方法有助于防止重复数据。
6. 若要添加初始迁移，请输入以下命令，然后按**enter**。

    > [!NOTE]
    > 请确保 LocalDB 实例中没有名为 &quot;GeekQuizProd&quot; 的数据库。

    [!code-powershell[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample2.ps1)]

    ![添加基础架构迁移](maintainable-azure-websites-managing-change-and-scale/_static/image2.png "添加基础架构迁移")

    *添加基础架构迁移*

    > [!NOTE]
    > **添加迁移**将基于自上次创建迁移后对模型所做的更改基架下一次迁移。 在这种情况下，因为它是项目的首次迁移，所以它将添加脚本，以创建在**TriviaContext**类中定义的所有表。
7. 通过运行以下命令执行迁移以更新数据库。 对于此命令，您将指定**详细**标志以查看应用于目标数据库的 SQL 语句。

    [!code-powershell[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample3.ps1)]

    ![正在创建初始数据库](maintainable-azure-websites-managing-change-and-scale/_static/image3.png "正在创建初始数据库")

    *正在创建初始数据库*

    > [!NOTE]
    > **更新-数据库**将应用任何挂起的到数据库的迁移。 在这种情况下，它将使用 web.config 文件中定义的连接字符串来创建数据库。
8. 中转到 "**视图**" 菜单并打开**SQL Server 对象资源管理器**。

    ![在 SQL Server 对象资源管理器中打开](maintainable-azure-websites-managing-change-and-scale/_static/image4.png "在 SQL Server 对象资源管理器中打开")

    *在 SQL Server 对象资源管理器中打开*
9. 在 " **SQL Server 对象资源管理器**" 窗口中，右键单击 " **SQL Server** " 节点，然后选择 "**添加 SQL Server ...** " 选项，连接到 LocalDB 实例。

    ![添加 SQL Server 实例](maintainable-azure-websites-managing-change-and-scale/_static/image5.png "添加 SQL Server 实例")

    *将 SQL Server 实例添加到 SQL Server 对象资源管理器*
10. 将**服务器名称**设置为 *（localdb） \v11.0* ，并将**Windows 身份验证**设置为身份验证模式。 单击“ **连接** ”以继续。

    ![连接到 LocalDB](maintainable-azure-websites-managing-change-and-scale/_static/image6.png "连接到 LocalDB")

    *连接到 LocalDB*
11. 打开**GeekQuizProd**数据库，然后展开 "**表**" 节点。 如您所见，**更新数据库**命令生成了**TriviaContext**类中定义的所有表。 找到**dbo。TriviaQuestions**表并打开 "列" 节点。 在下一任务中，您将向此表中添加一个新列，并使用**迁移**更新数据库。

    ![琐碎内容问题列](maintainable-azure-websites-managing-change-and-scale/_static/image7.png "琐碎内容问题列")

    *琐碎内容问题列*

<a id="Ex1Task2"></a>
#### <a name="task-2--updating-database-schema-using-migrations"></a>任务2–使用迁移更新数据库架构

在此任务中，您将使用**Entity Framework Code First 迁移**来检测模型的更改，并生成必要的代码来更新数据库。 你将通过向**TriviaQuestions**实体添加新属性来更新该实体。 然后，你将运行命令来创建新的迁移，以将新列包含在表中。

1. 在**解决方案资源管理器**中，双击位于 "**模型**" 文件夹中的**TriviaQuestion.cs**文件。
2. 添加一个名为 "**提示**" 的新属性，如下面的代码段所示。

    [!code-csharp[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample4.cs)]
3. 在 "**程序包管理器控制台**" 中，输入以下命令，然后按**enter**。 将创建新的迁移，以反映模型中的更改。

    [!code-powershell[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample5.ps1)]

    ![添加-迁移](maintainable-azure-websites-managing-change-and-scale/_static/image8.png "Add-Migration")

    *添加-迁移*

    > [!NOTE]
    > 迁移文件由两种方法组成：**向上**和**向下**。
    >
    > - **Up**方法用于指定应用程序的当前版本应用程序需要应用于数据库的更改。
    > - **Down**用于反转添加到**Up**方法中的更改。
    >
    > 当数据库迁移更新数据库时，它将按时间戳顺序运行所有迁移，并且仅运行自上次更新以来尚未使用的迁移（\_MigrationHistory 表会跟踪已应用的迁移）。 将调用所有迁移的向上方法，并将所做的更改**设置**为数据库。 如果我们决定返回到以前的迁移，则将调用**Down**方法以按相反顺序重做更改。
4. 在 "**程序包管理器控制台**" 中，输入以下命令，然后按**enter**。

    [!code-powershell[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample6.ps1)]
5. TriviaQuestions 命令的输出**生成了** **Alter Table** SQL 语句，以将新列添加到表中，如下图所示。

    ![添加了生成列 SQL 语句](maintainable-azure-websites-managing-change-and-scale/_static/image9.png "添加了生成列 SQL 语句")

    *添加了生成列 SQL 语句*
6. 在**SQL Server 对象资源管理器**中，刷新**dbo。TriviaQuestions**表并检查是否显示了新的**提示**列。

    ![显示新提示列](maintainable-azure-websites-managing-change-and-scale/_static/image10.png "显示新提示列")

    *显示新提示列*
7. 返回到**TriviaQuestion.cs**编辑器，将**StringLength**约束添加到*提示*属性，如下面的代码段所示。

    [!code-csharp[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample7.cs)]
8. 在 "**程序包管理器控制台**" 中，输入以下命令，然后按**enter**。

    [!code-powershell[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample8.ps1)]
9. 在 "**程序包管理器控制台**" 中，输入以下命令，然后按**enter**。

    [!code-powershell[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample9.ps1)]
10. TriviaQuestions 命令的输出**生成了** **Alter table** SQL 语句以更新表的*提示*列类型，如下图所示。

    ![已生成 Alter column SQL 语句](maintainable-azure-websites-managing-change-and-scale/_static/image11.png "已生成 Alter column SQL 语句")

    *已生成 Alter column SQL 语句*
11. 在**SQL Server 对象资源管理器**中，刷新**dbo。TriviaQuestions**表并检查**提示**列类型是否为**nvarchar （150）** 。

    ![显示新约束](maintainable-azure-websites-managing-change-and-scale/_static/image12.png "显示新约束")

    *显示新约束*

<a id="Exercise2"></a>
### <a name="exercise-2-deploying-a-web-app-to-staging"></a>练习2：将 Web 应用部署到过渡环境

**Azure App Service 中的 Web 应用**可用于执行分阶段发布。 过渡发布为每个默认生产站点创建一个过渡站点槽，并使你能够在不停机的情况下交换这些槽。 这对于在发布到公共、增量集成站点内容之前验证更改，以及在更改未按预期工作时回滚的操作非常有用。

在此练习中，你将使用 Git 源代码管理将**书呆子测验**应用程序部署到 web 应用的过渡环境。 为此，需要在管理门户中创建 web 应用并设置所需的组件，配置**Git**存储库，并将应用程序源代码从本地计算机推送到过渡槽。 你还将用在上一个练习中创建的**Code First 迁移**更新生产数据库。 然后，你将在此测试环境中执行应用程序以验证其操作。 一旦您认为它是根据您的预期工作，您就会将该应用程序提升到生产环境。

> [!NOTE]
> 若要启用过渡发布，web 应用必须处于 "**标准" 模式**。 请注意，如果你将 web 应用更改为 "标准" 模式，则会产生额外费用。 有关定价的详细信息，请参阅[应用服务定价](https://azure.microsoft.com/pricing/details/app-service/)。

<a id="Ex2Task1"></a>
#### <a name="task-1--creating-a-web-app-in-azure-app-service"></a>任务1–在 Azure App Service 中创建 Web 应用

在此任务中，你将在管理门户的**Azure App Service**中创建 web 应用。 你还将配置一个**SQL 数据库**来持久保存应用程序数据，并为源代码管理配置一个本地 Git 存储库。

1. 请参阅[Azure 管理门户](https://manage.windowsazure.com)，并使用与你的订阅关联的 Microsoft 帐户登录。

    ![登录到 Azure 管理门户](maintainable-azure-websites-managing-change-and-scale/_static/image13.png)

    *登录到 Azure 管理门户*
2. 单击页面底部命令栏中的 "**新建**"。

    ![创建新的 web 应用](maintainable-azure-websites-managing-change-and-scale/_static/image14.png "创建新的 web 应用")

    *创建新的 web 应用*
3. 单击 "**计算**"、"**网站**"，然后单击 "**自定义创建**"。

    ![使用 "自定义创建" 创建新的 web 应用](maintainable-azure-websites-managing-change-and-scale/_static/image15.png "使用 "自定义创建" 创建新的 web 应用")

    *使用 "自定义创建" 创建新的 web 应用*
4. 在 "**新建网站-自定义创建**" 对话框中，提供可用的**URL** （例如*书呆子*），在 "**区域**" 下拉列表中选择一个位置，然后在 "**数据库**" 下拉列表中选择 "**创建新的 SQL 数据库**"。 最后，选中 "**从源代码管理发布**" 复选框，然后单击 "**下一步**"。

    ![自定义新的 web 应用](maintainable-azure-websites-managing-change-and-scale/_static/image16.png)

    *自定义新的 web 应用*
5. 指定数据库设置的下列信息：

   - 在 "**名称**" 文本框中，输入数据库名称（例如， *geekquiz\_db*）
   - 在 "服务器"**下拉**列表中，选择 "**新建 SQL 数据库服务器**"。 或者，您可以选择现有服务器。
   - 在 "**数据库用户名**" 和 "**数据库密码**" 框中，输入 SQL 数据库服务器的管理员用户名和密码。 如果选择一个已创建的服务器，系统会提示输入密码。

     ![指定数据库设置](maintainable-azure-websites-managing-change-and-scale/_static/image17.png)

     *指定数据库设置*
6. 单击 **“下一步”** 以继续。
7. 选择要使用的源代码管理的 "**本地 Git 存储库**"，然后单击 "**下一步**"。

    > [!NOTE]
    > 系统可能会提示你输入部署凭据（用户名和密码）。

    ![创建 Git 存储库](maintainable-azure-websites-managing-change-and-scale/_static/image18.png)

    *创建 Git 存储库*
8. 等待，直到创建新的 web 应用。

    > [!NOTE]
    > 默认情况下，Azure 在*azurewebsites.net*提供域，还可以使用 azure 管理门户设置自定义域。 但是，如果你使用某些 Azure App Service 模式，则只能管理自定义域。
    >
    > Azure App Service 提供免费、共享、基本、标准和高级版。 在 "免费" 和 "共享" 模式下，所有 web 应用都在多租户环境中运行，并具有 CPU、内存和网络使用情况的配额。 最大可用应用数可能因计划而异。 在 "标准" 模式下，你可以选择在与标准 Azure 计算资源相对应的专用虚拟机上运行的应用。 可在 web 应用的 "**缩放**" 菜单中找到 web 应用模式配置。
    >
    > ![Azure App Service 模式](maintainable-azure-websites-managing-change-and-scale/_static/image19.png "Azure App Service 模式")
    >
    > 如果你使用的是 "**共享**" 或 "**标准**" 模式，你将能够通过转到应用的 "**配置**" 菜单，并在 "*域名*" 下单击 "**管理域**" 来管理 web 应用的自定义域。
    >
    > ![管理域](maintainable-azure-websites-managing-change-and-scale/_static/image20.png "管理域")
    >
    > ![管理自定义域](maintainable-azure-websites-managing-change-and-scale/_static/image21.png "管理自定义域")
9. 创建 web 应用后，单击 " **URL** " 列下的链接，检查新的 web 应用是否正在运行。

    ![浏览到新的 web 应用](maintainable-azure-websites-managing-change-and-scale/_static/image22.png)

    *浏览到新的 web 应用*

    ![web 应用正在运行](maintainable-azure-websites-managing-change-and-scale/_static/image23.png)

    *web 应用正在运行*

<a id="Ex2Task2"></a>
#### <a name="task-2--creating-the-production-sql-database"></a>任务2–创建生产 SQL 数据库

在此任务中，你将使用**Entity Framework Code First 迁移**创建面向你在上一任务中创建的**Azure SQL 数据库**实例的数据库。

1. 在管理门户中，导航到在上一任务中创建的 web 应用，并转到其**仪表板**。
2. 在 "**仪表板**" 页上，单击 **"速览" 部分下**的 "**查看连接字符串**" 链接。

    ![查看连接字符串](maintainable-azure-websites-managing-change-and-scale/_static/image24.png "查看连接字符串")

    *查看连接字符串*
3. 复制 "**连接字符串**" 值并关闭对话框。

    ![Azure 管理门户中的连接字符串](maintainable-azure-websites-managing-change-and-scale/_static/image25.png "Azure 管理门户中的连接字符串")

    *Azure 管理门户中的连接字符串*
4. 单击 " **Sql 数据库**" 以查看 Azure 中的 sql 数据库列表

    ![SQL 数据库菜单](maintainable-azure-websites-managing-change-and-scale/_static/image26.png "SQL 数据库菜单")

    *SQL 数据库菜单*
5. 找到在上一任务中创建的数据库，然后单击该服务器。

    ![SQL 数据库服务器](maintainable-azure-websites-managing-change-and-scale/_static/image27.png "SQL 数据库服务器")

    *SQL 数据库服务器*
6. 在服务器的 "**快速入门**" 页上，单击 "**配置**"。

    ![配置菜单](maintainable-azure-websites-managing-change-and-scale/_static/image28.png "配置菜单")

    *配置菜单*
7. 在 "**允许的 ip 地址**" 部分中，单击 **"添加到允许的 ip 地址"** 链接，以使你的 IP 能够连接到 SQL 数据库服务器。

    ![允许的 IP 地址](maintainable-azure-websites-managing-change-and-scale/_static/image29.png "允许的 IP 地址")

    *允许的 IP 地址*
8. 单击页面底部的 "**保存**" 以完成该步骤。
9. 切换回 Visual Studio。
10. 在**包管理器控制台**中，执行以下命令，将 *[你的连接字符串]* 占位符替换为从 Azure 复制的连接字符串

    [!code-powershell[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample10.ps1)]

    ![更新面向 Windows Azure SQL 数据库的数据库](maintainable-azure-websites-managing-change-and-scale/_static/image30.png "更新面向 Windows Azure SQL 数据库的数据库")

    *更新面向 Azure SQL 数据库的数据库*

<a id="Ex2Task3"></a>
#### <a name="task-3--deploying-geek-quiz-to-staging-using-git"></a>任务3–使用 Git 将书呆子测验部署到过渡

在此任务中，将在 web 应用中启用过渡发布。 然后，将使用 Git 将书呆子测验应用程序从本地计算机直接发布到 web 应用的过渡环境。

1. 返回到门户，并在 "**名称**" 列下单击 web 应用的名称以显示管理页面。

    ![打开 web 应用管理页](maintainable-azure-websites-managing-change-and-scale/_static/image31.png)

    *打开 web 应用管理页*
2. 导航到 "**缩放**" 页。 在 "**常规**" 部分下，选择 "**标准**" 作为配置，并单击命令栏中的 "**保存**"。

    > [!NOTE]
    > 若要在 "**标准**" 模式下运行当前区域和订阅中的所有 web 应用，请将 "选择**站点**" 配置中的 "**全**选" 复选框保持选中状态。 否则，请清除 "**全选**" 复选框。

    ![将 web 应用升级到标准模式](maintainable-azure-websites-managing-change-and-scale/_static/image32.png "将 web 应用升级到标准模式")

    *将 Web 应用升级到标准模式*
3. 单击 **"是"** 确认更改。

    ![确认更改为 "标准" 模式](maintainable-azure-websites-managing-change-and-scale/_static/image33.png "继续更改 web 应用模式")

    *确认更改为 "标准" 模式*
4. 中转到 "**仪表板**" 页，然后单击 "**速览**" 部分下的 "**启用过渡发布**"。

    ![启用过渡发布](maintainable-azure-websites-managing-change-and-scale/_static/image34.png "启用过渡发布")

    *启用过渡发布*
5. 单击 **"是"** 以启用过渡发布。

    ![正在确认暂存发布](maintainable-azure-websites-managing-change-and-scale/_static/image35.png "单击 "是" 以启用过渡发布")

    *正在确认暂存发布*
6. 在 web 应用列表中，展开 web 应用名称左侧的标记以显示过渡站点槽。 它包含你的 web 应用的名称，后跟 " ***（过渡）***"。 单击暂存站点以切换到 "管理" 页。

    ![导航到过渡 web 应用](maintainable-azure-websites-managing-change-and-scale/_static/image36.png "导航到过渡 web 应用")

    *导航到过渡应用*
7. 请注意，此管理页看起来与任何其他 web 应用程序的管理页一样。 导航到 "**部署**" 页并复制 " **Git URL** " 值。 稍后在本练习中将使用它。

    ![复制 Git URL 值](maintainable-azure-websites-managing-change-and-scale/_static/image37.png)

    *复制 Git URL 值*
8. 打开新的**Git Bash**控制台并执行以下命令。 将 *[应用程序路径]* 占位符更新为**GeekQuiz**解决方案的路径，该路径位于此实验室的**Source\Ex1-DeployingWebSiteToStaging\Begin**文件夹中。

    [!code-console[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample11.cmd)]

    ![Git 初始化和首次提交](maintainable-azure-websites-managing-change-and-scale/_static/image38.png)

    *Git 初始化和首次提交*
9. 运行以下命令，将 web 应用推送到远程**Git**存储库。 将占位符替换为你从管理门户获取的 URL。 系统将提示你输入部署密码。

    [!code-console[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample12.cmd)]

    ![推送到 Microsoft Azure](maintainable-azure-websites-managing-change-and-scale/_static/image39.png)

    *推送到 Azure*

    > [!NOTE]
    > 将内容部署到 web 应用的 FTP 主机或 GIT 存储库时，必须使用从 web 应用的**快速入门**或**仪表板**管理页创建的**部署凭据**进行身份验证。 如果你不知道你的部署凭据，则可以使用管理门户轻松地重置它们。 打开 web 应用的 "**仪表板**" 页，然后单击 "**重置部署凭据**" 链接。 提供新密码，并单击 **"确定"** 。 部署凭据可用于与你的订阅关联的所有 web 应用。
10. 若要验证是否已成功将 web 应用推送到 Azure，请返回到管理门户，然后单击 "**网站**"。
11. 找到 web 应用，然后展开该条目以显示过渡站点槽。 单击其**名称**以打开 "管理" 页。
12. 单击 "**部署**" 以查看**部署历史记录**。 使用 *&quot;初始提交&quot;* 验证是否存在**活动的部署**。

    ![活动部署](maintainable-azure-websites-managing-change-and-scale/_static/image40.png)

    *活动部署*
13. 最后，单击命令栏中的 "**浏览**"，转到 web 应用。

    ![浏览 web 应用](maintainable-azure-websites-managing-change-and-scale/_static/image41.png)

    *浏览 web 应用*
14. 如果已成功部署应用程序，你将看到书呆子测验登录页。

    > [!NOTE]
    > 部署的应用程序的地址 URL 包含你的 web 应用的名称，并在*中间进行过渡*。

    ![在过渡环境中运行的应用程序](maintainable-azure-websites-managing-change-and-scale/_static/image42.png)

    *在过渡环境中运行的应用程序*
15. 如果要浏览应用程序，请单击 "**注册**" 以注册新用户。 输入用户名、电子邮件地址和密码来填写帐户详细信息。 接下来，应用程序会显示测验的第一个问题。 回答几个问题，以确保它按预期方式工作。

    ![可供使用的应用程序](maintainable-azure-websites-managing-change-and-scale/_static/image43.png)

    *可供使用的应用程序*

<a id="Ex2Task4"></a>
#### <a name="task-4--promoting-the-web-app-to-production"></a>任务 4-将 Web 应用升级到生产环境

在过渡环境中验证 web 应用是否正常工作后，就可以将其升级到生产环境了。 在此任务中，你要将过渡站点槽与生产站点槽交换。

1. 返回到管理门户，并选择 "暂存" 站点槽。 在命令栏中单击 "**交换**"。

    ![交换到生产](maintainable-azure-websites-managing-change-and-scale/_static/image44.png)

    *交换到生产*
2. 在确认对话框中单击 **"是"** 以继续执行交换操作。 Azure 会立即将生产站点的内容与过渡站点的内容交换。

    > [!NOTE]
    > 过渡版版本中的某些设置将自动复制到生产版本（例如，连接字符串替代、处理程序映射等），但其他设置将不会更改（例如 DNS 终结点、SSL 绑定等）。

    ![正在确认交换操作](maintainable-azure-websites-managing-change-and-scale/_static/image45.png)

    *正在确认交换操作*
3. 交换完成后，选择 "生产" 槽，并单击命令栏中的 "**浏览**" 以打开生产站点。 请注意地址栏中的 URL。

    > [!NOTE]
    > 可能需要刷新浏览器以清除缓存。 在 Internet Explorer 中，可以通过按**CTRL + R**来完成此操作。

    ![在生产环境中运行的 Web 应用](maintainable-azure-websites-managing-change-and-scale/_static/image46.png)
4. 在**GitBash**控制台中，更新本地 Git 存储库的远程 URL，使其面向生产槽。 为此，请运行以下命令，将占位符替换为部署用户名和 web 应用名称。

    > [!NOTE]
    > 在以下练习中，你会将更改推送到生产站点，而不是仅针对实验室的简单性进行过渡。 在实际方案中，建议在升级到生产环境之前，验证过渡环境中的更改。

    [!code-console[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample13.cmd)]

<a id="Exercise3"></a>
### <a name="exercise-3-performing-deployment-rollback-in-production"></a>练习3：在生产环境中执行部署回滚

在某些情况下，如果你使用的是 "**免费**" 或 "**共享**" 模式，则无需使用过渡槽在过渡与生产之间执行热交换。 在这些情况下，在部署到生产环境之前，你应该在测试环境中测试你的应用程序（本地或远程站点）。 但是，在测试阶段未检测到的问题可能出现在生产站点中。 在这种情况下，一定要使用一种机制，尽快尽快切换到以前的、更稳定的应用程序版本。

在**Azure App Service**中，通过源代码管理进行持续部署可让你使用管理门户中的 "重新**部署**" 操作。 Azure 会跟踪与推送到存储库的提交相关联的部署，并提供一个选项，用于随时使用你以前的任何部署重新部署应用程序。

在本练习中，您将在**书呆子测验**应用程序中对代码进行更改，以故意注入*bug*。 你要将应用程序部署到生产环境以查看错误，然后你将利用重新部署功能返回到以前的状态。

<a id="Ex3Task1"></a>
#### <a name="task-1--updating-the-geek-quiz-application"></a>任务1–更新书呆子测验应用程序

在此任务中，您将重构**TriviaController**类的一小段代码，以便将从数据库中检索所选测验选项的部分逻辑提取到新方法中。

1. 切换到 Visual Studio 实例，其中包含上一练习中的**GeekQuiz**解决方案。
2. 在**解决方案资源管理器**中，打开 "**控制器**" 文件夹中的**TriviaController.cs**文件。
3. 找到**StoreAsync**方法，然后选择下图中突出显示的代码。

    ![选择代码](maintainable-azure-websites-managing-change-and-scale/_static/image47.png)

    *选择代码*
4. 右键单击所选代码，展开 "**重构**" 菜单，然后选择 "**提取方法 ...** "。

    ![将代码提取为新方法](maintainable-azure-websites-managing-change-and-scale/_static/image48.png)

    *选择提取方法*
5. 在 "**提取方法**" 对话框中，将新方法命名为*MatchesOption* ，然后单击 **"确定"** 。

    ![指定方法名称](maintainable-azure-websites-managing-change-and-scale/_static/image49.png)

    *指定提取方法的名称*
6. 然后，将选定的代码提取到**MatchesOption**方法中。 生成的代码将显示在以下代码段中。

    [!code-csharp[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample14.cs)]
7. 按**CTRL + S**保存更改。

<a id="Ex3Task2"></a>
#### <a name="task-2--redeploying-the-geek-quiz-application"></a>任务2–重新部署书呆子测验应用程序

你现在将在上一任务中所做的更改推送到存储库，这将触发到生产环境的新部署。 然后，你将使用 Internet Explorer 提供的**F12 开发工具**对问题进行故障排除，然后从 Azure 管理门户执行到以前的部署的回滚。

1. 打开新的**Git Bash**控制台，将更新的应用程序部署到 Azure App Service。
2. 执行以下命令将更改推送到 Azure。 将 *[应用程序路径]* 占位符更新为**GeekQuiz**解决方案的路径。 系统将提示你输入部署密码。

    [!code-console[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample15.cmd)]

    ![将重构的代码推送到 Azure](maintainable-azure-websites-managing-change-and-scale/_static/image50.png)

    *将重构的代码推送到 Azure*
3. 打开 Internet Explorer 并导航到 web 应用（例如 `http://<your-web-site>.azurewebsites.net`）。 使用前面创建的凭据登录。
4. 按**F12**启动开发工具，选择 "**网络**" 选项卡，然后单击 "**播放**" 按钮开始录制。

    ![正在启动网络记录](maintainable-azure-websites-managing-change-and-scale/_static/image51.png "正在启动网络记录")

    *正在启动网络记录*
5. 选择测验的任何选项。 你将看到没有任何反应。
6. 在**F12**窗口中，与 POST http 请求对应的条目显示 HTTP **500**结果。

    ![HTTP 500 错误](maintainable-azure-websites-managing-change-and-scale/_static/image52.png)

    *HTTP 500 错误*
7. 选择 "**控制台**" 选项卡。将记录一个错误，其中包含原因的详细信息。

    ![记录的错误](maintainable-azure-websites-managing-change-and-scale/_static/image53.png)

    *记录的错误*
8. 找到错误的详细信息部分。 很显然，此错误是由您在前面的步骤中提交的代码重构引起的。

    `Details: LINQ to Entities does not recognize the method 'Boolean MatchesOption ...`。
9. 不要关闭浏览器。
10. 在新的浏览器实例中，导航到[Azure 管理门户](https://manage.windowsazure.com)，并使用与你的订阅关联的 Microsoft 帐户进行登录。
11. 选择 "**网站**"，然后单击在练习2中创建的 web 应用。
12. 导航到 "**部署**" 页。 请注意，部署历史记录中列出了执行的所有提交。

    ![现有部署列表](maintainable-azure-websites-managing-change-and-scale/_static/image54.png)

    *现有部署列表*
13. 选择上一个提交，并单击命令栏上的 "重新**部署**"。

    ![重新部署以前的提交](maintainable-azure-websites-managing-change-and-scale/_static/image55.png)

    *重新部署以前的提交*
14. 出现确认提示时，单击“是”。

    ![确认重新部署](maintainable-azure-websites-managing-change-and-scale/_static/image56.png)
15. 部署完成后，请切换回 web 应用的浏览器实例，并按**CTRL + F5**。
16. 单击任一选项。 现在，翻转动画将发生，并显示结果（*正确/错误*）。
17. 可有可无切换到**Git Bash**控制台并执行以下命令以恢复到以前的提交。

    > [!NOTE]
    > 这些命令将创建一个新的 commit，以撤消在错误提交中进行的 Git 存储库中的所有更改。 然后，Azure 将使用新的提交重新部署应用程序。

    [!code-console[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample16.cmd)]

<a id="Exercise4"></a>
### <a name="exercise-4-scaling-using-azure-storage"></a>练习4：使用 Azure 存储进行缩放

**Blob**是存储大量非结构化文本或二进制数据（如视频、音频和图像）的最简单方法。 将应用程序的静态内容移动到存储，有助于通过直接向浏览器提供图像或文档来扩展应用程序。

在此练习中，你要将应用程序的静态内容移动到 Blob 容器。 然后，将应用程序配置为**在 web.config 中**添加**ASP.NET URL 重写规则**，以将内容重定向到 Blob 容器。

<a id="Ex4Task1"></a>
#### <a name="task-1--creating-an-azure-storage-account"></a>任务1–创建 Azure 存储帐户

在此任务中，你将了解如何使用管理门户创建新的存储帐户。

1. 导航到[Azure 管理门户](https://manage.windowsazure.com)，并使用与你的订阅关联的 Microsoft 帐户登录。
2. 选择**新 |数据服务 |存储 |"快速创建**" 以开始创建新的存储帐户。 输入帐户的唯一名称，并从列表中选择一个**区域**。 单击 "**创建存储帐户**" 以继续。

    ![创建新的存储帐户](maintainable-azure-websites-managing-change-and-scale/_static/image57.png "创建新的存储帐户")

    *创建新的存储帐户*
3. 在 "**存储**" 部分中，等到新存储帐户的 "状态" 更改为 "*联机*"，才能继续执行以下步骤。

    ![已创建存储帐户](maintainable-azure-websites-managing-change-and-scale/_static/image58.png "已创建存储帐户")

    *已创建存储帐户*
4. 单击存储帐户名称，然后单击页面顶部的 "**仪表板**" 链接。 "**仪表板**" 页提供了有关帐户状态和可在应用程序中使用的服务终结点的信息。

    ![显示存储帐户仪表板](maintainable-azure-websites-managing-change-and-scale/_static/image59.png "显示存储帐户仪表板")

    *显示存储帐户仪表板*
5. 单击导航栏中的 "**管理访问密钥**" 按钮。

    !["管理访问密钥" 按钮](maintainable-azure-websites-managing-change-and-scale/_static/image60.png ""管理访问密钥" 按钮")

    *"管理访问密钥" 按钮*
6. 在 "**管理访问密钥**" 对话框中，复制 "**存储帐户名称**" 和 "**主访问密钥**"，因为在以下练习中将需要它们。 然后关闭对话框。

    !["管理访问密钥" 对话框](maintainable-azure-websites-managing-change-and-scale/_static/image61.png ""管理访问密钥" 对话框")

    *"管理访问密钥" 对话框*

<a id="Ex4Task2"></a>
#### <a name="task-2--uploading-an-asset-to-azure-blob-storage"></a>任务 2-将资产上传到 Azure Blob 存储

在此任务中，将使用 Visual Studio 中的 "服务器资源管理器" 窗口连接到存储帐户。 然后，将创建一个 blob 容器，并将带有书呆子测验徽标的文件上传到该容器。

1. 切换到 Visual Studio 实例，其中包含上一练习中的**GeekQuiz**解决方案。
2. 从菜单栏中选择 "**视图**"，然后单击 "**服务器资源管理器**"。
3. 在**服务器资源管理器**中，右键单击**Azure**节点，并选择 "**连接到 Azure ...** "。使用与你的订阅关联的 Microsoft 帐户登录。

    ![连接到 Windows Azure](maintainable-azure-websites-managing-change-and-scale/_static/image62.png)

    *连接到 Azure*
4. 展开 " **Azure** " 节点，右键单击 "**存储**"，然后选择 "**附加外部存储 ...** "。
5. 在 "**添加新存储帐户**" 对话框中，输入你在上一任务中获取的**帐户名称**和**帐户密钥**，然后单击 **"确定"** 。

    !["添加新存储帐户" 对话框](maintainable-azure-websites-managing-change-and-scale/_static/image63.png)

    *"添加新存储帐户" 对话框*
6. 存储帐户应该出现在 "**存储**" 节点下。 展开存储帐户，右键单击 " **blob** "，然后选择 "**创建 Blob 容器 ...** "。

    ![创建 Blob 容器](maintainable-azure-websites-managing-change-and-scale/_static/image64.png "创建 Blob 容器")

    *创建 Blob 容器*
7. 在 "**创建 Blob 容器**" 对话框中，输入 Blob 容器的名称，然后单击 **"确定"** 。

    !["创建 Blob 容器" 对话框](maintainable-azure-websites-managing-change-and-scale/_static/image65.png ""创建 Blob 容器" 对话框")

    *"创建 Blob 容器" 对话框*
8. 应将新的 blob 容器添加到**blob**节点。 更改容器中的访问权限，使容器成为公共容器。 为此，请右键单击**images**容器，然后选择 "**属性**"。

    ![图像容器属性](maintainable-azure-websites-managing-change-and-scale/_static/image66.png "图像容器属性")

    *图像容器属性*
9. 在 "**属性**" 窗口中，将 "**公共读取访问权限**" 设置为 "**容器**"。

    ![更改公共读取访问属性](maintainable-azure-websites-managing-change-and-scale/_static/image67.png "更改公共读取访问属性")

    *更改公共读取访问属性*
10. 当系统提示你是否确定要更改公共访问属性时，请单击 **"是"** 。

    ![Microsoft Visual Studio 警告](maintainable-azure-websites-managing-change-and-scale/_static/image68.png "Microsoft Visual Studio 警告")

    *Microsoft Visual Studio 警告*
11. 在**服务器资源管理器**中，右键单击**images** blob 容器，然后选择 "**查看 blob 容器**"。

    ![查看 Blob 容器](maintainable-azure-websites-managing-change-and-scale/_static/image69.png "查看 Blob 容器")

    *查看 Blob 容器*
12. 图像容器应在新窗口中打开，并且应显示不含任何条目的图例。 单击 "**上传**" 图标，将文件上传到 blob 容器。

    ![没有条目的图像容器](maintainable-azure-websites-managing-change-and-scale/_static/image70.png "没有条目的图像容器")

    *没有条目的图像容器*
13. 在 "**上传 Blob** " 对话框中，导航到实验室的 "**资产**" 文件夹。 选择**logo-big**文件并单击 "**打开**"。
14. 等待文件上传。 上传完成后，该文件应在 images 容器中列出。 右键单击该文件条目，然后选择 "**复制 URL**"。

    ![复制 blob URL](maintainable-azure-websites-managing-change-and-scale/_static/image71.png "复制 blob 文件 URL")

    *复制 blob URL*
15. 打开 Internet Explorer 并粘贴 URL。 以下图像应显示在浏览器中。

    ![Windows Blob 存储中的 logo-big 映像](maintainable-azure-websites-managing-change-and-scale/_static/image72.png "logo-big 存储中的 .png 映像")

    *Azure Blob 存储中的 logo-big 映像*

<a id="Ex4Task3"></a>
#### <a name="task-3--updating-the-solution-to-consume-static-content-from-azure-blob-storage"></a>任务3–更新解决方案以使用 Azure Blob 存储中的静态内容

在此任务中，你将配置**GeekQuiz**解决方案，以使用上传到 Azure Blob 存储（而不是位于 web 应用中的映像）的图像，方法是在**web.config 文件中**添加 ASP.NET URL 重写规则。

1. 在 Visual Studio 中，打开**GeekQuiz**项目**中的 web.config 文件，** 并找到 **&lt;system.webserver&gt;** 元素。
2. 添加以下代码以添加 URL 重写规则，并使用您的存储帐户名称更新占位符。

    （代码段- *WebSitesInProduction-Ex4-UrlRewriteRule*）

    [!code-xml[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample17.xml)]

    > [!NOTE]
    > URL 重写是拦截传入的 Web 请求并将请求重定向到其他资源的过程。 URL 重写规则告诉重写引擎何时需要重定向请求，以及应重定向到的位置。 重写规则由以下两个字符串组成：要在请求的 URL 中查找的模式（通常使用正则表达式）和替换模式的字符串（如果找到）。 有关详细信息，请参阅[ASP.NET 中的 URL 重写](https://msdn.microsoft.com/library/ms972974.aspx)。
3. 按**CTRL + S**保存更改。
4. 打开新的**Git Bash**控制台，将更新的应用程序部署到 Azure App Service。
5. 执行以下命令将更改推送到 Azure。 将 *[应用程序路径]* 占位符更新为**GeekQuiz**解决方案的路径。 系统将提示你输入部署密码。

    [!code-console[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample18.cmd)]

    ![将更新部署到 Azure](maintainable-azure-websites-managing-change-and-scale/_static/image73.png)

    *将更新部署到 Azure*

<a id="Ex4Task4"></a>
#### <a name="task-4--verification"></a>任务 4 – 验证

在此任务中，你将使用**Internet Explorer**来浏览**书呆子测验**应用程序，并检查图像的 URL 重写规则是否正常工作，以及你是否已重定向到**Azure Blob 存储**上托管的映像。

1. 打开 Internet Explorer 并导航到 web 应用（例如 `http://<your-web-site>.azurewebsites.net`）。 使用前面创建的凭据登录。

    ![显示包含图像的书呆子测验 web 应用](maintainable-azure-websites-managing-change-and-scale/_static/image74.png "显示包含图像的书呆子测验 web 应用")

    *显示包含图像的书呆子测验 web 应用*
2. 按**F12**启动开发工具，选择 "**网络**" 选项卡并开始记录。

    ![正在启动网络记录](maintainable-azure-websites-managing-change-and-scale/_static/image75.png "正在启动网络记录")

    *正在启动网络记录*
3. 按**CTRL + F5**刷新网页。
4. 页面加载完成后，应会看到 **/Img/logo-big.png** url 发出 http 请求，其中包含 http **301**结果（重定向），另一请求使用 HTTP **200**结果 `http://[YOUR-STORAGE-ACCOUNT].blob.core.windows.net/images/logo-big.png` url。

    ![验证 URL 重定向](maintainable-azure-websites-managing-change-and-scale/_static/image76.png "在开发工具中显示重定向")

    *验证 URL 重定向*

<a id="Exercise5"></a>
### <a name="exercise-5-using-autoscale-for-web-apps"></a>练习5：对 Web 应用使用自动缩放

> [!NOTE]
> 此练习是可选的，因为它需要支持 Web 负载 &amp; 仅适用于**Visual Studio 2013 旗舰版**的性能测试。 有关特定 Visual Studio 2013 功能的详细信息，请在[此处](https://www.microsoft.com/visualstudio/eng/products/compare)比较版本。

**Azure App Service Web apps**为在 "**标准" 模式下**运行的 Web 应用提供自动缩放功能。 自动缩放可让 Azure 根据负载自动缩放 web 应用的实例计数。 启用自动缩放后，Azure 每五分钟检查一次 web 应用的 CPU，并根据需要在该时间点添加实例。 如果 CPU 使用率较低，Azure 将每两小时删除一次实例，以确保 web 应用的性能不会下降。

在本练习中，你将完成配置**书呆子测验**web 应用的**自动缩放**功能所需的步骤。 你将通过运行 Visual Studio 负载测试来验证此功能，以便在应用程序上生成足够的 CPU 负载以触发实例升级。

<a id="Ex5Task1"></a>
#### <a name="task-1--configuring-autoscale-based-on-the-cpu-metric"></a>任务1–基于 CPU 指标配置自动缩放

在此任务中，你将使用 Azure 管理门户为在练习2中创建的 web 应用启用自动缩放功能。

1. 在[Azure 管理门户](https://manage.windowsazure.com/)中，选择 "**网站**"，然后单击在练习2中创建的 web 应用。
2. 导航到 "**缩放**" 页。 在 "**容量**" 部分下，为 "**按度量值缩放**" 配置选择 " **CPU** "。

    > [!NOTE]
    > 按 CPU 进行缩放时，Azure 会动态调整应用在 CPU 使用率变化时使用的实例数。

    ![选择按 CPU 进行缩放](maintainable-azure-websites-managing-change-and-scale/_static/image77.png "选择自动缩放的 CPU 指标")

    *选择按 CPU 进行缩放*
3. 将**目标 CPU**配置更改为**20**-**40** %。

    > [!NOTE]
    > 此范围表示 web 应用的平均 CPU 使用率。 Azure 将添加或删除实例，以使你的 web 应用保持在此范围中。 用于缩放的最小和最大实例数是在**实例计数**配置中指定的。 Azure 绝不会超出或超出该限制。
    >
    > 默认情况下，仅为此实验室修改默认**目标 CPU**值。 通过使用较小的值配置 CPU 范围，可以增加在应用程序上放置了中等负载时触发自动缩放的机会。

    ![将目标 CPU 更改为20% 到40%](maintainable-azure-websites-managing-change-and-scale/_static/image78.png "将目标 CPU 更改为20% 到40%")

    *将目标 CPU 更改为20% 到40%*
4. 单击命令栏中的 "**保存**" 以保存更改。

<a id="Ex5Task2"></a>
#### <a name="task-2--load-testing-with-visual-studio"></a>任务 2-通过 Visual Studio 进行负载测试

现在已配置**自动缩放**，你将在 Visual Studio 中创建**Web 性能和负载测试项目**，以在 Web 应用上生成一些 CPU 负载。

1. 打开**Visual Studio Ultimate 2013** ，然后选择 "**文件" |新建 |项目 ...** 启动新解决方案。

    ![创建新项目](maintainable-azure-websites-managing-change-and-scale/_static/image79.png "创建新的项目")

    *创建新项目*
2. 在 "**新建项目**" 对话框中，选择 " **Web 性能和负载测试项目**"。  **C#** 请确保选择 **.NET Framework 4.5** ，将项目命名为*WebAndLoadTestProject*，选择一个**位置**，然后单击 **"确定"** 。

    ![创建新的 Web 和负载测试项目](maintainable-azure-websites-managing-change-and-scale/_static/image80.png "创建新的 Web 和负载测试项目")

    *创建新的 Web 和负载测试项目*
3. 在**webtest1.webtest**中，右键单击**webtest1.webtest**节点，然后单击 "**添加请求**"。

    ![向 Webtest1.webtest 添加请求](maintainable-azure-websites-managing-change-and-scale/_static/image81.png "向 Webtest1.webtest 添加请求")

    *向 Webtest1.webtest 添加请求*
4. 在新请求节点的 "**属性**" 窗口中，将 " **url** " 属性更新为指向 web 应用的 url （例如 *[http://geek-quiz.azurewebsites.net/](http://geek-quiz.azurewebsites.net/)* ）。

    ![更改 Url 属性](maintainable-azure-websites-managing-change-and-scale/_static/image82.png "更改 Url 属性")

    *更改 Url 属性*
5. 在**webtest1.webtest webtest**窗口中，右键单击**webtest1.webtest** ，然后单击 "**添加循环 ...** "。

    ![向 Webtest1.webtest 添加循环](maintainable-azure-websites-managing-change-and-scale/_static/image83.png "向 Webtest1.webtest 添加循环")

    *向 Webtest1.webtest 添加循环*
6. 在 "**添加条件规则" 和 "要循环的项**" 对话框中，选择**for 循环**规则并修改以下属性。

   1. **终止值：** 1000
   2. **上下文参数名称：** 器
   3. **增量值：** 1

      ![选择 For 循环规则并更新属性](maintainable-azure-websites-managing-change-and-scale/_static/image84.png "选择 For 循环规则并更新属性")

      *选择 For 循环规则并更新属性*
7. 在 "**循环中的项**" 部分下，选择之前创建的请求作为该循环的第一项和最后一项。 单击 **“确定”** 继续。

    ![选择循环的第一项和最后一项](maintainable-azure-websites-managing-change-and-scale/_static/image85.png "选择循环的第一项和最后一项")

    *选择循环的第一项和最后一项*
8. 在**解决方案资源管理器**中，右键单击**WebAndLoadTestProject**项目，展开 "**添加**" 菜单，然后选择 "**负载测试 ...** "。

    ![将负载测试添加到 WebAndLoadTestProject 项目](maintainable-azure-websites-managing-change-and-scale/_static/image86.png "将负载测试添加到 WebAndLoadTestProject 项目")

    *将负载测试添加到 WebAndLoadTestProject 项目*
9. 在 "**新建负载测试向导**" 对话框中，单击 "**下一步**"。

    ![新负载测试向导](maintainable-azure-websites-managing-change-and-scale/_static/image87.png "新负载测试向导")

    *新负载测试向导*
10. 在 "**方案**" 页上，选择 "**不使用思考时间**"，然后单击 "**下一步**"。

    ![选择不使用思考时间](maintainable-azure-websites-managing-change-and-scale/_static/image88.png "选择不使用思考时间")

    *选择不使用思考时间*
11. 在 "**负载模式**" 页上，确保选择 "**常量加载**" 选项。 将**用户计数**设置更改为**250**用户，然后单击 "**下一步**"。

    ![将用户计数更改为250](maintainable-azure-websites-managing-change-and-scale/_static/image89.png "将用户计数更改为250")

    *将用户计数更改为250*
12. 在 "**测试组合模型**" 页中，选择 "**基于顺序测试顺序**"，然后单击 "**下一步**"。

    ![选择测试组合模型](maintainable-azure-websites-managing-change-and-scale/_static/image90.png "选择测试组合模型")

    *选择测试组合模型*
13. 在 "**测试组合模型**" 页中，单击 "**添加 ...** " 将测试添加到组合。

    ![向测试组合中添加测试](maintainable-azure-websites-managing-change-and-scale/_static/image91.png "向测试组合中添加测试")

    *向测试组合中添加测试*
14. 在 "**添加测试**" 对话框中，双击 " **webtest1.webtest** " 将测试添加到 "**选定的测试**" 列表。 单击 **“确定”** 继续。

    ![添加 Webtest1.webtest 测试](maintainable-azure-websites-managing-change-and-scale/_static/image92.png "添加 Webtest1.webtest 测试")

    *添加 Webtest1.webtest 测试*
15. 返回到**测试组合**页，单击 "**下一步**"。

    ![完成测试组合页](maintainable-azure-websites-managing-change-and-scale/_static/image93.png "完成测试组合页")

    *完成测试组合页*
16. 在 "**网络组合**" 页上，单击 "**下一步**"。

    ![在网络组合页面中单击 "下一步"](maintainable-azure-websites-managing-change-and-scale/_static/image94.png "在网络组合页面中单击 "下一步"")

    *在网络组合页面中单击 "下一步"*
17. 在 "**浏览器组合**" 页面中，选择**Internet Explorer 10.0**作为浏览器类型，然后单击 "**下一步**"。

    ![选择浏览器类型](maintainable-azure-websites-managing-change-and-scale/_static/image95.png "选择浏览器类型")

    *选择浏览器类型*
18. 在 "**计数器集**" 页中，单击 "**下一步**"。

    ![在 "计数器集" 页中单击 "下一步"](maintainable-azure-websites-managing-change-and-scale/_static/image96.png "在 "计数器集" 页中单击 "下一步"")

    *在 "计数器集" 页中单击 "下一步"*
19. 在 "**运行设置**" 页中，将 "**负载测试持续时间**" 设置为**5 分钟**，然后单击 "**完成**"。

    ![将负载测试持续时间设置为5分钟](maintainable-azure-websites-managing-change-and-scale/_static/image97.png "将负载测试持续时间设置为5分钟")

    *将负载测试持续时间设置为5分钟*
20. 在**解决方案资源管理器**中，双击**本地设置**文件以浏览测试设置。 默认情况下，Visual Studio 使用本地计算机来运行测试。

    > [!NOTE]
    > 或者，可以使用**Azure Test Plans**将测试项目配置为在云中运行负载测试。 Azure Test Plans 提供了一种基于云的负载测试服务，用于模拟更真实的负载，从而避免了本地环境约束（如 CPU 容量、可用内存和网络带宽）。 有关使用 Azure Test Plans 运行负载测试的详细信息，请参阅[负载测试方案](/azure/devops/test/load-test/overview?view=vsts)。

    ![测试设置](maintainable-azure-websites-managing-change-and-scale/_static/image98.png)

<a id="Ex5Task3"></a>
#### <a name="task-3--autoscale-verification"></a>任务3–自动缩放验证

现在，你将执行在上一任务中创建的负载测试，并查看你的 web 应用在负载下的行为。

1. 在**解决方案资源管理器**中，双击 " **LoadTest1** " 以打开负载测试。

    ![打开 LoadTest1. loadtest](maintainable-azure-websites-managing-change-and-scale/_static/image99.png "打开 LoadTest1. loadtest")

    *打开 LoadTest1. loadtest*
2. 在**LoadTest1 loadtest**窗口中，单击 "工具箱" 中的第一个按钮以运行负载测试。

    ![运行负载测试](maintainable-azure-websites-managing-change-and-scale/_static/image100.png "运行负载测试")

    *运行负载测试*
3. 等待负载测试完成。

    > [!NOTE]
    > 负载测试模拟将请求同时发送到 web 应用的多个用户。 当测试正在运行时，您可以监视可用的计数器，以检测任何与您的负载测试运行有关的错误、警告或其他信息。

    ![负载测试正在运行](maintainable-azure-websites-managing-change-and-scale/_static/image101.png "正在等待负载测试完成")

    *负载测试正在运行*
4. 测试完成后，返回到管理门户并导航到 web 应用的 "**缩放**" 页。 在 "**容量**" 部分下，你应在图形中看到自动部署了新实例的。

    ![已自动部署新实例](maintainable-azure-websites-managing-change-and-scale/_static/image102.png)

    *已自动部署新实例*

    > [!NOTE]
    > 可能需要花费几分钟时间，更改才会显示在图形中（定期按**CTRL + F5**刷新页面）。 如果看不到任何更改，可以尝试以下操作：
    >
    > - 增加负载测试的持续时间（例如**10 分钟**）
    > - 减少 web 应用的自动缩放配置中**目标 CPU**范围的最大值和最小值
    > - 在云中运行负载测试，并**Azure Test Plans**。 详细信息请参见[此处](/azure/devops/test/load-test/index?view=vsts)

---

<a id="Summary"></a>
## <a name="summary"></a>摘要

在此动手实验中，你已了解如何在 Azure 中设置应用程序并将其部署到生产 web 应用。 首先，通过使用**Entity Framework Code First 迁移**检测和更新数据库，然后使用**Git**部署站点的新版本并执行回滚到最新稳定版本的站点。 此外，还了解了如何使用存储缩放应用，将静态内容移动到 Blob 容器。
