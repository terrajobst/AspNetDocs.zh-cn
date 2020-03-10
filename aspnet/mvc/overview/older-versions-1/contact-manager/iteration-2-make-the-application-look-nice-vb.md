---
uid: mvc/overview/older-versions-1/contact-manager/iteration-2-make-the-application-look-nice-vb
title: '迭代 #2 –使应用程序看起来很漂亮（VB） |Microsoft Docs'
author: microsoft
description: 在此迭代中，我们通过修改默认的 ASP.NET MVC 视图母版页和级联样式表来改善应用程序的外观。
ms.author: riande
ms.date: 02/20/2009
ms.assetid: f65cb436-e493-46fd-9608-384b27385aa1
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-2-make-the-application-look-nice-vb
msc.type: authoredcontent
ms.openlocfilehash: cd392baaefcfc9eef3551bc534e0b912ccd349cc
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78487280"
---
# <a name="iteration-2--make-the-application-look-nice-vb"></a>迭代 #2 –使应用程序看起来很漂亮（VB）

由[Microsoft](https://github.com/microsoft)

[下载代码](iteration-2-make-the-application-look-nice-vb/_static/contactmanager_2_vb1.zip)

> 在此迭代中，我们通过修改默认的 ASP.NET MVC 视图母版页和级联样式表来改善应用程序的外观。

## <a name="building-a-contact-management-aspnet-mvc-application-vb"></a>构建联系人管理 ASP.NET MVC 应用程序（VB）

在本系列教程中，我们从一开始就生成一个完整的联系人管理应用程序。 使用联系人管理器应用程序可以存储联系人信息–姓名、电话号码和电子邮件地址。

我们通过多个迭代生成应用程序。 随着每次迭代，我们将逐步改进应用程序。 此多个迭代方法的目标是使您能够了解每个更改的原因。

- 迭代 #1 –创建应用程序。 在第一次迭代中，我们以尽可能简单的方式创建联系人管理器。 添加对基本数据库操作的支持：创建、读取、更新和删除（CRUD）。

- 迭代 #2 –使应用程序看起来不错。 在此迭代中，我们通过修改默认的 ASP.NET MVC 视图母版页和级联样式表来改善应用程序的外观。

- 迭代 #3 –添加窗体验证。 在第三次迭代中，我们将添加基本的窗体验证。 我们阻止用户提交窗体，而无需填写所需的窗体字段。 我们还验证了电子邮件地址和电话号码。

- 迭代 #4 –使应用程序松散耦合。 在第四次迭代中，我们将利用多种软件设计模式来更轻松地维护和修改联系人管理器应用程序。 例如，我们重构应用程序以使用存储库模式和依赖关系注入模式。

- 迭代 #5 –创建单元测试。 在第五次迭代中，通过添加单元测试使应用程序更易于维护和修改。 我们模拟数据模型类，并为控制器和验证逻辑生成单元测试。

- 迭代 #6 –使用测试驱动开发。 在第六次迭代中，我们通过首先编写单元测试并针对单元测试编写代码，向应用程序添加新功能。 在此迭代中，我们添加联系人组。

- 迭代 #7 –添加 Ajax 功能。 在第七次迭代中，我们通过添加对 Ajax 的支持来提高应用程序的响应能力和性能。

## <a name="this-iteration"></a>此迭代

此迭代的目标是改进联系人管理器应用程序的外观。 目前，联系人管理器使用默认的 ASP.NET MVC 视图母版页和级联样式表（参见图1）。 这似乎不是很糟糕，但我不想让联系人经理看起来就像其他每个 ASP.NET MVC 网站。 我要将这些文件替换为自定义文件。

[!["新建项目" 对话框](iteration-2-make-the-application-look-nice-vb/_static/image1.jpg)](iteration-2-make-the-application-look-nice-vb/_static/image1.png)

**图 01**： ASP.NET MVC 应用程序的默认外观（[单击以查看完全大小的图像](iteration-2-make-the-application-look-nice-vb/_static/image2.png)）

在此迭代中，我讨论了用于改进应用程序的可视化设计的两种方法。 首先，我将向您介绍如何利用 ASP.NET MVC 设计库下载免费的 ASP.NET MVC 设计模板。 ASP.NET MVC 设计库使你可以创建专业的 web 应用程序，而无需执行任何操作。

我决定不使用 "联系人管理器" 应用程序的 ASP.NET MVC 设计库中的模板。 而是由专业设计公司创建的自定义设计。 在本教程的第二部分中，我将介绍如何使用专业设计公司来创建最终的 ASP.NET MVC 设计。

## <a name="the-aspnet-mvc-design-gallery"></a>ASP.NET MVC 设计库

ASP.NET MVC 设计库是 Microsoft 提供的免费资源。 ASP.NET MVC 库位于以下地址：

[https://www.asp.net/mvc/gallery](https://www.asp.net/mvc/gallery)

ASP.NET MVC 设计库承载一个免费网站设计的集合，这些设计是专门为在 ASP.NET MVC 项目中使用而创建的。 设计由社区成员上传。 库的访问者可以为其偏好的设计投票（参见图2）。

[!["新建项目" 对话框](iteration-2-make-the-application-look-nice-vb/_static/image2.jpg)](iteration-2-make-the-application-look-nice-vb/_static/image3.png)

**图 02**： ASP.NET MVC 设计库（[单击以查看完全大小的图像](iteration-2-make-the-application-look-nice-vb/_static/image4.png)）

当我撰写本教程时，库中最流行的设计是一种名为10月10日的设计。 可以通过完成以下步骤，将此设计用于 ASP.NET MVC 项目：

1. 单击 "**下载**" 按钮，将10月的 .zip 文件下载到你的计算机。
2. 右键单击下载的十月. .zip 文件，然后单击 "**解除阻止**" 按钮（请参阅图3）。
3. 将文件解压缩到10月的文件夹中。
4. 选择十月文件夹中包含的 DesignTemplate 文件夹中的所有文件，右键单击文件，然后选择 "**复制**" 菜单选项。
5. 右键单击 "Visual Studio 解决方案资源管理器" 窗口中的 ContactManager 项目节点，然后选择 "**粘贴**" 菜单选项（见图4）。
6. 选择 Visual Studio 菜单选项 "**编辑、查找和替换"、"快速替换" 和 "** 将 *[MyProjectName]* 替换为*ContactManager* " （参见图5）。

[!["新建项目" 对话框](iteration-2-make-the-application-look-nice-vb/_static/image3.jpg)](iteration-2-make-the-application-look-nice-vb/_static/image5.png)

**图 03**：取消阻止从 web 下载的文件（[单击查看完全大小的图像](iteration-2-make-the-application-look-nice-vb/_static/image6.png)）

[!["新建项目" 对话框](iteration-2-make-the-application-look-nice-vb/_static/image4.jpg)](iteration-2-make-the-application-look-nice-vb/_static/image7.png)

**图 04**：覆盖解决方案资源管理器中的文件（[单击以查看完全大小的图像](iteration-2-make-the-application-look-nice-vb/_static/image8.png)）

[!["新建项目" 对话框](iteration-2-make-the-application-look-nice-vb/_static/image5.jpg)](iteration-2-make-the-application-look-nice-vb/_static/image9.png)

**图 05**：用 ContactManager 替换 [项目名称] （[单击以查看完全大小的图像](iteration-2-make-the-application-look-nice-vb/_static/image10.png)）

完成这些步骤后，你的 web 应用程序将使用新设计。 图6中的页说明了 "联系人管理器" 应用程序在10月的外观。

[!["新建项目" 对话框](iteration-2-make-the-application-look-nice-vb/_static/image6.jpg)](iteration-2-make-the-application-look-nice-vb/_static/image11.png)

**图 06**：带十月模板的 ContactManager （[单击查看完全大小的图像](iteration-2-make-the-application-look-nice-vb/_static/image12.png)）

## <a name="creating-a-custom-aspnet-mvc-design"></a>创建自定义 ASP.NET MVC 设计

ASP.NET MVC 设计库可以选择不同的设计样式。 库为您提供了一种轻松的方法，可自定义 ASP.NET MVC 应用程序的外观。 当然，库具有完全免费的强大优势。

不过，您可能需要为您的网站创建完全唯一的设计。 在这种情况下，与网站设计公司合作是有意义的。 我决定采用此方法来设计联系人管理器应用程序。

我从迭代 #1 中压缩了联系人管理器，并将项目发送到了设计公司。 它们不是 Visual Studio （shame 上的），但这并不是问题。 他们能够从[https://www.asp.net](https://www.asp.net)网站免费下载 Microsoft Visual web Developer，并在 Visual Web developer 中打开联系人管理器应用程序。 几天后，它们已在图7中生成了设计。

[!["新建项目" 对话框](iteration-2-make-the-application-look-nice-vb/_static/image7.jpg)](iteration-2-make-the-application-look-nice-vb/_static/image13.png)

**图 07**： ASP.NET MVC 联系人经理设计（[单击查看完全大小的图像](iteration-2-make-the-application-look-nice-vb/_static/image14.png)）

新的设计包括两个主要文件：一个新的级联样式表文件和一个新的视图母版页文件。 视图母版页包含 ASP.NET MVC 应用程序中视图的布局和共享内容。 例如，视图母版页包含图7中所示的标头、导航选项卡和页脚。 我覆盖了现有站点。 Views\Shared 文件夹中的母版视图母版页，其中包含来自设计公司的新网站 .Master 文件。

设计公司还创建了一个新的级联样式表和一组图像。 我将这些新文件放在 Content 文件夹中，并覆盖了现有的 web.config 文件。 应将所有静态内容放在 Content 文件夹中。

请注意，联系人管理器的新设计包含用于编辑和删除联系人的图像。 "编辑" 和 "删除" 图像显示在 "联系人" 的 HTML 表中的每个联系人旁边。

最初，这些链接是通过 HTML 呈现的。Html.actionlink （）帮助程序，如下所示：

[!code-aspx[Main](iteration-2-make-the-application-look-nice-vb/samples/sample1.aspx)]

.Html （）方法不支持图像（出于安全原因，方法为 HTML 编码链接文本）。 因此，我将对 Html.actionlink （）的调用替换为对 Url 的调用。

[!code-aspx[Main](iteration-2-make-the-application-look-nice-vb/samples/sample2.aspx)]

.Html （）方法呈现整个 HTML 超链接。 另一方面，.Url （）方法只呈现 URL，而不会 &lt;&gt; 标记。

另外请注意，新的设计包括选定和未选定的选项卡。 例如，在图8中，选择了 "新建**联系人**" 选项卡，并选择了 "**我的联系人**" 选项卡。

[!["新建项目" 对话框](iteration-2-make-the-application-look-nice-vb/_static/image8.jpg)](iteration-2-make-the-application-look-nice-vb/_static/image15.png)

**图 08**：选中和未选中的选项卡（[单击以查看完全大小的图像](iteration-2-make-the-application-look-nice-vb/_static/image16.png)）

为了支持显示选定和未选定的选项卡，我创建了一个名为 MenuItemHelper 的自定义 HTML 帮助程序。 此帮助器方法将 &lt;li&gt; 标记或 &lt;li 类 = "selected"&gt; 标记，具体取决于当前控制器和操作是否对应于传递给帮助器的控制器和操作名称。 MenuItemHelper 的代码包含在列表1中。

**列表1– Helpers\MenuItemHelper.vb**

[!code-vb[Main](iteration-2-make-the-application-look-nice-vb/samples/sample3.vb)]

MenuItemHelper 在内部使用 TagBuilder 类来生成 &lt;li&gt; HTML 标记。 TagBuilder 类是一个非常有用的实用工具类，每当需要构建新的 HTML 标记时，就可以使用该类。 它包括添加属性、添加 CSS 类、生成 Id 以及修改标记的内部 HTML 的方法。

## <a name="summary"></a>摘要

在此迭代中，我们改进了 ASP.NET MVC 应用程序的可视化设计。 首先，已引入 ASP.NET MVC 设计库。 你已学习如何从 ASP.NET MVC 设计库下载免费设计模板，你可以在 ASP.NET MVC 应用程序中使用这些模板。

接下来，我们讨论了如何通过修改默认级联样式表文件和母版视图页面文件来创建自定义设计。 为了支持新的设计，我们必须对联系人管理器应用程序进行一些小的更改。 例如，我们添加了一个名为 MenuItemHelper 的新 HTML 助手，其中显示了选定和未选定的选项卡。

在下一次迭代中，我们将处理验证的非常重要的主题。 我们将验证代码添加到应用程序，以便用户无法在不提供所需的值（例如人员的姓氏和名字）的情况下创建新联系人。

> [!div class="step-by-step"]
> [上一页](iteration-1-create-the-application-vb.md)
> [下一页](iteration-3-add-form-validation-vb.md)
