---
uid: web-forms/overview/deployment/visual-studio-web-deployment/deploying-a-code-update
title: 使用 Visual Studio 的 ASP.NET Web 部署：部署代码更新 |Microsoft Docs
author: tdykstra
description: 本系列教程介绍了如何通过来将 ASP.NET web 应用程序部署（发布）到 Azure App Service Web 应用或第三方托管提供程序。
ms.author: riande
ms.date: 02/15/2013
ms.assetid: c76dbc35-a914-4ee3-919c-4f4d1fa05104
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/deploying-a-code-update
msc.type: authoredcontent
ms.openlocfilehash: 3881833bfe2a50a38a357614f92f434a04a8ab08
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74626782"
---
# <a name="aspnet-web-deployment-using-visual-studio-deploying-a-code-update"></a>使用 Visual Studio 的 ASP.NET Web 部署：部署代码更新

作者： [Tom Dykstra](https://github.com/tdykstra)

[下载初学者项目](https://go.microsoft.com/fwlink/p/?LinkId=282627)

> 本系列教程介绍了如何使用 Visual Studio 2012 或 Visual Studio 2010，将 ASP.NET web 应用程序部署（发布）到 Azure App Service Web 应用或第三方托管提供商。 有关序列的信息，请参阅本[系列中的第一个教程](introduction.md)。

## <a name="overview"></a>概述

初始部署完成后，你维护和开发网站的工作将继续进行，在此之前，你将需要部署更新。 本教程将指导你完成将更新部署到应用程序代码的过程。 在本教程中实现和部署的更新不涉及数据库更改;在下一教程中，你将看到有关部署数据库更改的不同之处。

提醒：如果你收到一条错误消息或在你完成本教程时无法正常工作，请务必查看[故障排除页](troubleshooting.md)。

## <a name="make-a-code-change"></a>更改代码

作为应用程序更新的简单示例，你将向**讲师**页添加选定讲师讲授的课程列表。

如果您运行的是**讲师**页，您会注意到网格中有**选择**的链接，但除了使行背景变为灰色以外，它们不会执行任何操作。

![带有选择的指导员页面](deploying-a-code-update/_static/image1.png)

现在，你将添加在单击 "**选择**" 链接时运行的代码，并显示所选指导员讲授的课程列表。

1. 在*default.aspx*中，在**ErrorMessageLabel** `Label` 控件后立即添加以下标记：

    [!code-aspx[Main](deploying-a-code-update/samples/sample1.aspx)]
2. 运行页面并选择一个指导员。 你将看到该教师讲授的课程列表。

    ![讲授课程的教师页面](deploying-a-code-update/_static/image2.png)
3. 关闭浏览器。

## <a name="deploy-the-code-update-to-the-test-environment"></a>将代码更新部署到测试环境

在可以使用您的发布配置文件部署到测试、过渡和生产环境之前，您需要更改数据库发布选项。 不再需要为成员资格数据库运行 grant 和数据部署脚本。

1. 右键单击 "ContosoUniversity" 项目并单击 "**发布**"，打开 "**发布 Web** " 向导。
2. 单击 "**配置文件**" 下拉列表中的**测试**配置文件。
3. 单击 "**设置**" 选项卡。
4. 在 "**数据库**" 部分的 " **DefaultConnection** " 下，清除 "**更新数据库**" 复选框。
5. 单击 "**配置文件**" 选项卡，然后单击 "**配置文件**" 下拉列表中的**临时**配置文件。
6. 当系统询问你是否要保存对**测试**配置文件所做的更改时，请单击 **"是"** 。
7. 在临时配置文件中进行相同的更改。
8. 重复此过程以在生产配置文件中进行相同的更改。
9. 关闭 "**发布 Web** " 向导。

现在，只需运行一次单击 "发布" 即可部署到测试环境。 若要使此过程更快，你可以使用**Web 一键式发布**工具栏。

1. 在 "**视图**" 菜单中选择 "**工具栏**"，然后选择 **"Web 一键式发布"** 。

    ![Selecting_One_Click_Publish_toolbar](deploying-a-code-update/_static/image3.png)
2. 在**解决方案资源管理器**中，选择 ContosoUniversity 项目。
3. **Web 一键式发布**工具栏上，选择 "**测试**发布配置文件"，然后单击 "**发布 Web** " （其箭头指向左侧和右侧的图标）。

    ![Web_One_Click_Publish_toolbar](deploying-a-code-update/_static/image4.png)
4. Visual Studio 将部署更新后的应用程序，浏览器会自动打开到主页。
5. 运行 "讲师" 页，然后选择一个教师来验证更新是否已成功部署。

通常情况下，还会进行回归测试（即，测试站点的其余部分以确保新的更改不会破坏现有的任何功能）。 但对于本教程，你将跳过该步骤，并继续将更新部署到过渡和生产环境。

重新部署时，Web 部署会自动确定哪些文件已更改，并且仅将更改的文件复制到服务器。 默认情况下，Web 部署使用文件上次更改的日期来确定哪些文件已更改。 某些源代码管理系统会更改文件日期，即使您不更改文件内容也是如此。 在这种情况下，你可能希望将 Web 部署配置为使用文件校验和来确定哪些文件已更改。 有关详细信息，请参阅 ASP.NET 部署常见问题解答中的[为什么我不更改所有文件就](https://msdn.microsoft.com/library/ee942158.aspx#use_checksum)会重新部署。

## <a name="take-the-application-offline-during-deployment"></a>在部署过程中使应用程序脱机

现在正在部署的更改是单个页面的简单更改。 但有时，你可以部署更大的更改，或者同时部署代码和数据库更改，如果用户在部署完成之前请求页面，则站点的行为可能会错误。 若要防止用户在部署过程中访问网站，可以使用*应用\_脱机 .htm*文件。 在应用程序的根文件夹中将名为 "app" 的文件\_为 " *offline* " 时，IIS 会自动显示该文件，而不是运行应用程序。 因此，若要在部署过程中阻止访问，请在根文件夹中将*应用\_为 offline* ，运行部署过程，然后在成功部署后删除*应用\_脱机 .htm。*

可以将 Web 部署配置为在服务器上开始部署时将默认*应用程序\_脱机 .htm*文件，并在其完成后将其删除。 为此，只需将以下 XML 元素添加到发布配置文件（.pubxml）文件中：

[!code-xml[Main](deploying-a-code-update/samples/sample2.xml)]

在本教程中，你将了解如何创建和使用自定义*应用\_脱机 .htm*文件。

不需要在暂存站点中使用*应用\_.htm* ，因为你没有访问过渡站点的用户。 但使用过渡测试计划在生产中部署的方式是一种很好的做法。

### <a name="create-app_offlinehtm"></a>创建脱机应用\_

1. 在**解决方案资源管理器**中，右键单击解决方案并单击 "**添加**"，然后单击 "**新建项**"。
2. 创建一个名为 " *app\_* " 的**HTML 页面**（在默认情况下，Visual Studio 创建的 *.html*扩展中删除最终的 "l"）。
3. 将模板标记替换为以下标记：

    [!code-html[Main](deploying-a-code-update/samples/sample3.html)]
4. 保存并关闭文件。

### <a name="copy-app_offlinehtm-to-the-root-folder-of-the-web-site"></a>将应用\_脱机复制到网站的根文件夹

您可以使用任何 FTP 工具将文件复制到网站。 [FileZilla](http://filezilla-project.org/)是一种常用的 FTP 工具，在屏幕截图中显示。

若要使用 FTP 工具，需要执行以下三项操作： FTP URL、用户名和密码。

URL 显示在 Azure 管理门户中网站的 "仪表板" 页上，可以在前面下载的 *.publishsettings*文件中找到 FTP 的用户名和密码。 以下步骤演示如何获取这些值。

1. 在 Azure 管理门户中，单击 **"网站" 选项卡**，然后单击 "暂存" 网站。
2. 在 "**仪表板**" 页上，向下滚动到 "**速览**" 部分中的 "FTP 主机名"。

    ![FTP 主机名](deploying-a-code-update/_static/image5.png)
3. 在记事本或其他文本编辑器中打开 *.publishsettings*文件。
4. 找到 FTP 配置文件的 `publishProfile` 元素。
5. 复制 `userName` 和 `userPWD` 值。

    ![FTP 凭据](deploying-a-code-update/_static/image6.png)
6. 打开 FTP 工具并登录到 FTP URL。
7. 将*应用\_.htm*从解决方案文件夹复制到临时站点中的 */site/wwwroot*文件夹。

    ![复制 app_offline](deploying-a-code-update/_static/image7.png)
8. 浏览到过渡站点的 URL。 此时将显示 "*应用\_offline* " 页，而不是主页。

    ![在浏览器窗口中 app_offline .htm](deploying-a-code-update/_static/image8.png)

你现在已准备好部署到过渡环境。

## <a name="deploy-the-code-update-to-staging-and-production"></a>将代码更新部署到过渡和生产环境

1. 在**Web 一键式发布**工具栏中，选择**过渡**发布配置文件，然后单击 "**发布 Web**"。

    Visual Studio 将部署更新后的应用程序，并将浏览器打开到站点的主页。 将显示*应用程序\_脱机 .htm*文件。 必须先删除*应用\_脱机 .htm*文件，然后才能进行测试以验证部署是否成功。
2. 返回到 FTP 工具，并从临时站点删除**应用\_offline。**
3. 在浏览器中，打开过渡站点中的 "讲师" 页，然后选择一个教师来验证更新是否已成功部署。
4. 对于生产，请遵循与进行过渡时相同的过程。

<a id="specificfiles"></a>

## <a name="reviewing-changes-and-deploying-specific-files"></a>查看更改并部署特定文件

Visual Studio 2012 还提供了部署单个文件的能力。 对于选定的文件，您可以查看本地版本和已部署的版本之间的差异，将文件部署到目标环境，或将文件从目标环境复制到本地项目中。 在本教程的此部分中，你将了解如何使用这些功能。

### <a name="make-a-change-to-deploy"></a>进行部署更改

1. 打开*Content/站点导航*，查找 `body` 标记的块。
2. 将 `background-color` 的值从 "`#fff`" 更改为 "`darkblue`"。

    [!code-css[Main](deploying-a-code-update/samples/sample4.css?highlight=2)]

### <a name="view-the-change-in-the-publish-preview-window"></a>在发布预览窗口中查看更改

使用 "**发布 Web** " 向导发布项目时，可以通过在**预览**窗口中双击文件来查看要发布的更改。

1. 右键单击 "ContosoUniversity" 项目，然后单击 "**发布**"。
2. 从 "**配置文件**" 下拉列表中，选择 "**测试**发布配置文件"。
3. 单击 "**预览**"，然后单击 "**开始预览**"。
4. 在**预览**窗格中，双击 **"web.config"。**

    ![双击 "网站地图"](deploying-a-code-update/_static/image9.png)

    "**预览更改**" 对话框显示将要部署的更改的预览。

    ![预览对站点的更改](deploying-a-code-update/_static/image10.png)

    如果双击*web.config 文件，* 则 "**预览更改**" 对话框将显示生成配置转换和发布配置文件转换的效果。 此时，你未执行任何操作来导致服务器上的*web.config 文件发生*更改，因此你不会看到任何更改。 但是，"**预览更改**" 窗口错误地显示两个更改。 将删除两个 XML 元素。 当你在 Code First 上下文类的**应用程序启动上选择 "执行 Code First 迁移**时，发布过程将添加这些元素。 比较是在发布过程添加这些元素之前完成的，因此，它看起来像是要删除它们，不过它们将不会被删除。 此错误将在将来的版本中得到更正。
5. 单击 **“关闭”** 。
6. 单击“发布”。
7. 当浏览器打开到测试网站的主页时，按 CTRL + F5 以引发硬刷新，以便查看 CSS 更改的效果。

    ![CSS 更改的效果](deploying-a-code-update/_static/image11.png)
8. 关闭浏览器。

### <a name="publish-specific-files-from-solution-explorer"></a>从解决方案资源管理器发布特定文件

假设您不喜欢蓝色背景并且要恢复为原始颜色。 在本部分中，你将通过直接从**解决方案资源管理器**发布特定文件来还原原始设置。

1. 打开*Content/Site .css*并将 `background-color` 设置还原为 `#fff`。
2. 在**解决方案资源管理器**中，右键单击*Content/Site .css*文件。

    上下文菜单显示了三个发布选项。

    ![从解决方案资源管理器发布选项](deploying-a-code-update/_static/image12.png)
3. 单击 "**预览对站点的更改**"。

    此时会打开一个窗口，以显示本地文件与目标环境中的本地文件版本之间的差异。

    ![Diff-Content/站点导航](deploying-a-code-update/_static/image13.png)
4. 在**解决方案资源管理器**中，再次右键单击 "**网站**"，然后单击 "**发布网站**"。

    " **Web 发布活动**" 窗口显示该文件已发布。

    !["Web 发布活动" 窗口](deploying-a-code-update/_static/image14.png)
5. 在浏览器中打开 `http://localhost/contosouniversity` URL，然后按 CTRL + F5 以引发硬刷新，以便查看 CSS 更改的效果。

    ![包含普通 CSS 的主页](deploying-a-code-update/_static/image15.png)
6. 关闭浏览器。

## <a name="summary"></a>总结

现在，您已看到了几种部署不涉及数据库更改的应用程序更新的方法，并且您已了解如何预览更改以验证将更新的内容。 讲师页现在提供了一个**课程讲授**部分。

![讲授课程的教师页面](deploying-a-code-update/_static/image16.png)

下一教程将演示如何部署数据库更改：将 "生日" 字段添加到数据库和 "讲师" 页。

> [!div class="step-by-step"]
> [上一页](deploying-to-production.md)
> [下一页](deploying-a-database-update.md)
