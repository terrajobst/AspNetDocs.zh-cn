---
uid: web-forms/overview/deployment/visual-studio-web-deployment/deploying-extra-files
title: 使用 Visual Studio 的 ASP.NET Web 部署：部署额外文件 |Microsoft Docs
author: tdykstra
description: 本系列教程介绍了如何通过来将 ASP.NET web 应用程序部署（发布）到 Azure App Service Web 应用或第三方托管提供程序。
ms.author: riande
ms.date: 03/23/2015
ms.assetid: 1cd91055-84bc-42c6-9d80-646f41429d4d
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/deploying-extra-files
msc.type: authoredcontent
ms.openlocfilehash: eaa3141c22980f0c816e2f33b5597ac9fe69c23c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78441362"
---
# <a name="aspnet-web-deployment-using-visual-studio-deploying-extra-files"></a>使用 Visual Studio 的 ASP.NET Web 部署：部署额外文件

作者： [Tom Dykstra](https://github.com/tdykstra)

[下载初学者项目](https://go.microsoft.com/fwlink/p/?LinkId=282627)

> 本系列教程介绍了如何使用 Visual Studio 2012 或 Visual Studio 2010，将 ASP.NET web 应用程序部署（发布）到 Azure App Service Web 应用或第三方托管提供商。 有关序列的信息，请参阅本[系列中的第一个教程](introduction.md)。

## <a name="overview"></a>概述

本教程介绍如何扩展 Visual Studio web 发布管道，以便在部署期间执行其他任务。 任务是将不在项目文件夹中的多余文件复制到目标网站。

对于本教程，你将复制一个额外的文件：*机器人。* 你希望将此文件部署到过渡，但不部署到生产环境。 在[部署到生产](deploying-to-production.md)教程中，你已将此文件添加到项目中，并已将生产发布配置文件配置为排除它。 在本教程中，你将看到用于处理这种情况的一种替代方法，一种方法可用于要部署但不想包含在项目中的任何文件。

## <a name="move-the-robotstxt-file"></a>移动机器人 .txt 文件

若要为*机器人 .txt*提供不同的处理方法，请在本教程的本部分中，将该文件移动到项目中未包含的文件夹，并从过渡环境中删除*机器人。* 需要从暂存中删除该文件，以便可以验证将该文件部署到该环境的新方法是否正常工作。

1. 在**解决方案资源管理器**中，右键单击*机器人 .txt*文件，然后单击 "**从项目中排除**"。
2. 使用 Windows 文件资源管理器在解决方案文件夹中创建一个新文件夹，并将其命名为*ExtraFiles*。
3. 将*机器人 .txt*文件从*ContosoUniversity*项目文件夹移动到*ExtraFiles*文件夹。

    ![ExtraFiles 文件夹](deploying-extra-files/_static/image1.png)
4. 使用 FTP 工具，从暂存网站中删除*机器人 .txt*文件。

    作为替代方法，你可以在过渡发布配置文件的 "**设置**" 选项卡上的 "**文件发布选项**" 下选择 "**删除目标上的其他文件**"，然后重新发布到 "过渡"。

## <a name="update-the-publish-profile-file"></a>更新发布配置文件

仅在暂存中需要*机器人 .txt* ，因此，要进行部署，只需暂存需要更新的发布配置文件。

1. 在 Visual Studio 中，打开 " *.pubxml*"。
2. 在文件末尾的结束 `</Project>` 标记之前，添加以下标记：

    [!code-xml[Main](deploying-extra-files/samples/sample1.xml)]

    此代码将创建一个新的目标，该*目标*将收集其他要部署的文件。 目标由一项或多项任务组成，MSBuild 将根据你指定的条件执行该任务。

    `Include` 特性指定要在其中查找文件的文件夹是*ExtraFiles*，位于与项目文件夹相同的级别。 MSBuild 将从该文件夹收集所有文件，并以递归方式从任何子文件夹中（双星号指定递归子文件夹）。 利用此代码，你可以将多个文件和文件放在*ExtraFiles*文件夹内的子文件夹中，所有文件都将被部署。

    `DestinationRelativePath` 元素指定应将文件夹和文件复制到目标网站的根文件夹中，与在*ExtraFiles*文件夹中找到的文件和文件夹结构相同。 如果要复制*ExtraFiles*文件夹本身，`DestinationRelativePath` 值将是*ExtraFiles\%（RecursiveDir）% （Filename）% （Extension）* 。
3. 在文件末尾的右 `</Project>` 标记之前，添加以下标记，以指定何时执行新的目标。

    [!code-xml[Main](deploying-extra-files/samples/sample2.xml)]

    此代码会在执行将文件复制到目标文件夹的目标时执行新的 `CustomCollectFiles` 目标。 有一个单独的目标用于发布和部署包创建，在你决定使用部署包而不是发布来部署的情况下，新目标将注入两个目标。

    *.Pubxml*文件现在如以下示例所示：

    [!code-xml[Main](deploying-extra-files/samples/sample3.xml?highlight=53-71)]
4. 保存并关闭 *.pubxml*文件。

## <a name="publish-to-staging"></a>发布到过渡

使用一键式发布或命令行，使用临时配置文件发布应用程序。

如果使用一键式发布，则可以在**预览**窗口中验证是否将复制*机器人。* 否则，请使用 FTP 工具来验证*机器人 .txt*文件是否在部署后位于该网站的根文件夹中。

## <a name="summary"></a>摘要

这将完成这一系列教程，介绍如何将 ASP.NET web 应用程序部署到第三方托管提供程序。 有关这些教程中所涉及的任何主题的详细信息，请参阅[ASP.NET 部署内容映射](https://go.microsoft.com/fwlink/p/?LinkId=282413)。

## <a name="more-information"></a>详细信息

如果你知道如何使用 MSBuild 文件，则可以通过在 *.pubxml*文件中（对于特定于配置文件的任务）或项目*wpp*文件（适用于适用于所有配置文件的任务）编写代码来自动执行许多其他部署任务。 有关 *.pubxml*和 .pubxml 文件的详细*信息，请*参阅[如何：在发布配置文件中编辑部署设置（.）文件和 Visual Studio Web 项目中的文件](https://msdn.microsoft.com/library/ff398069)。 有关 MSBuild 代码的基本介绍，请参阅企业部署系列中的**项目文件解析** [：了解项目文件](../web-deployment-in-the-enterprise/understanding-the-project-file.md)。 若要了解如何使用 MSBuild 文件来为自己的方案执行任务，请参阅此书籍：在[Microsoft 生成引擎：使用 MSBuild 和 Team Foundation build](http://msbuildbook.com) By Sayed Ibraham Hashimi 和 William Bartholomew。

## <a name="acknowledgements"></a>致谢

我想感谢以下人员对本系列教程的内容进行了重大贡献：

- [Alberto Poblacion，MVP &amp; MCT，西班牙](https://mvp.microsoft.com/mvp/Alberto%20Poblacion%20Bolano-36772)
- Jarod Ferguson，数据平台开发 MVP，美国
- 恶劣 Mittal，Microsoft
- [吴建 Galloway](https://weblogs.asp.net/jgalloway) （twitter： [@jongalloway](http://twitter.com/jongalloway)）
- [Kristina Olson，Microsoft](https://blogs.iis.net/krolson/default.aspx)
- [Mike Pope，Microsoft](http://www.mikepope.com/blog/DisplayBlog.aspx)
- Mohit Srivastava，Microsoft
- [Raffaele Rialdi，意大利](http://www.iamraf.net/)
- [Microsoft Rick Anderson](https://blogs.msdn.com/b/rickandy/)
- [Sayed Hashimi，Microsoft](http://sedodream.com/default.aspx)（twitter： [@sayedihashimi](http://twitter.com/sayedihashimi)）
- [Scott Hanselman](http://www.hanselman.com/blog/) （twitter： [@shanselman](http://twitter.com/shanselman)）
- [Scott Hunter，Microsoft](https://blogs.msdn.com/b/scothu/) （twitter： [@coolcsh](http://twitter.com/coolcsh)）
- [Srđan Božović，塞尔维亚](http://msforge.net/blogs/zmajcek/)
- [Vishal Joshi，Microsoft](http://vishaljoshi.blogspot.com/) （twitter： [@vishalrjoshi](http://twitter.com/vishalrjoshi)）

> [!div class="step-by-step"]
> [上一页](command-line-deployment.md)
> [下一页](troubleshooting.md)
