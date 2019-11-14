---
uid: mvc/overview/older-versions/hands-on-labs/whats-new-in-aspnet-mvc-4
title: ASP.NET MVC 4 中的新增功能 |Microsoft Docs
author: rick-anderson
description: ASP.NET MVC 4 是一个框架，用于生成可缩放的基于标准的 web 应用程序，该应用程序使用良好构建的设计模式以及 ASP.NET 和 。
ms.author: riande
ms.date: 02/18/2013
ms.assetid: 48f7feb3-872f-485d-b96f-e30011ff8c4a
msc.legacyurl: /mvc/overview/older-versions/hands-on-labs/whats-new-in-aspnet-mvc-4
msc.type: authoredcontent
ms.openlocfilehash: 4235f4fe666cdeb7d0821127a2b349f2ff30cd6e
ms.sourcegitcommit: 295cf898a4c87e264b0c35c7254b0fa4169f2278
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/13/2019
ms.locfileid: "74057033"
---
# <a name="whats-new-in-aspnet-mvc-4"></a>ASP.NET MVC 4 的新增功能

由[Web 训练营团队](https://twitter.com/webcamps)使用

[下载 Web 训练营培训工具包](https://aka.ms/webcamps-training-kit)

ASP.NET MVC 4 是一个框架，用于生成可缩放的基于标准的 web 应用程序，该应用程序使用良好构建的设计模式以及 ASP.NET 和 .NET framework 的强大功能。 这一新的第四个版本的框架侧重于使移动 web 应用程序的开发变得更简单。

首先，当你创建新的 ASP.NET MVC 4 项目时，现在可以使用一个移动应用程序项目模板来构建专用于移动设备的独立应用程序。 此外，ASP.NET MVC 4 还通过 jQuery NuGet 包与 jQuery Mobile 集成。 jQuery Mobile 是一个基于 HTML5 的框架，用于开发与所有常用移动设备平台（包括 Windows Phone、iPhone、Android 等）兼容的 web 应用。 但是，如果你需要特殊化，ASP.NET MVC 4 还可以为不同的设备提供不同的视图，并提供特定于设备的优化。

在此动手实验中，你将从 ASP.NET MVC 4 &quot;Internet 应用程序&quot; 项目模板开始，以创建照片库应用程序。 你将使用 jQuery Mobile 和 ASP.NET MVC 4 的新功能逐步提高应用，使其与不同的移动设备和桌面 web 浏览器兼容。 你还将了解用于代码生成的新代码食谱，以及 ASP.NET MVC 4 如何通过支持 Task&lt;ActionResult&gt; 返回类型来更轻松地编写异步操作方法。

> [!NOTE]
> 所有示例代码和代码段都包含在 Web 训练营培训工具包中，在[Microsoft-Web/WebCampTrainingKit 版本](https://aka.ms/webcamps-training-kit)中提供。 [ASP.NET 4.5 中 Web 窗体的新增功能中](https://github.com/Microsoft-Web/HOL-ASPNETWebForms)提供了此实验室特定的项目。

<a id="Objectives"></a>
### <a name="objectives"></a>目标

在此动手实验中，您将学习如何：

- 充分利用 ASP.NET MVC 项目模板的增强功能，包括新的移动应用程序项目模板
- 使用 HTML5 视区属性和 CSS 媒体查询改善移动设备上的显示
- 使用 jQuery Mobile 进行渐进式增强，并构建触摸优化 web UI
- 创建特定于移动设备的视图
- 使用视图切换器组件在应用程序的移动视图与桌面视图之间切换
- 使用任务支持创建异步控制器

<a id="Prerequisites"></a>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a>Prerequisites

你必须具有以下项才能完成此实验室：

- [适用于 Web 或高级的 Microsoft Visual Studio Express 2012](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) （有关如何安装的说明，请参阅[附录 B](#AppendixB) ）。
- [ASP.NET MVC 4](../../../mvc4.md) （包含在 Microsoft Visual Studio 2012 安装中）
- Windows Phone 模拟器（包括在[Windows Phone 7.1.1 SDK](https://www.microsoft.com/download/details.aspx?id=29233)中）
- 可选-附带**电气 Plum IPhone 模拟器**扩展的[WebMatrix 2](https://www.microsoft.com/web/webmatrix/) （仅适用于使用 iPhone 模拟器浏览 Web 应用程序的练习3）

<a id="Setup"></a>

<a id="Setup"></a>
### <a name="setup"></a>安装

在整个实验室文档中，系统会指示您插入代码块。 为方便起见，其中的大多数代码都作为 Visual Studio Code 代码段提供，你可以在 Visual Studio 中使用这些代码段，以避免手动添加它。

安装代码片段：

1. 打开 Windows 资源管理器窗口并浏览到实验室的**Source\Setup**文件夹。
2. 双击此文件夹中的**Setup .cmd**文件以安装 Visual Studio code 代码段。

如果你不熟悉 Visual Studio Code 代码段，并且想要了解如何使用它们，则可以参考本文档中的附录[A &quot;附录 A：使用代码段](#AppendixA)&quot;。

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a>练习

此动手实验包括以下练习：

1. [New ASP.NET MVC 4 项目模板](#Exercise1)
2. [创建照片库 Web 应用程序](#Exercise2)
3. [添加对移动设备的支持](#Exercise3)
4. [使用异步控制器](#Exercise4)

> [!NOTE]
> 每个练习都带有一个**结束**文件夹，其中包含在完成练习后应获得的结果解决方案。 如果需要更多帮助，请使用此解决方案作为指导。

完成本实验的估计时间： **60 分钟**。

<a id="Exercise1"></a>

<a id="Exercise_1_New_ASPNET_MVC_4_Project_Templates"></a>
### <a name="exercise-1-new-aspnet-mvc-4-project-templates"></a>练习1： New ASP.NET MVC 4 项目模板

在此练习中，你将了解 ASP.NET MVC 4 项目模板中的增强功能。 除了 Internet 应用程序模板外，在 MVC 3 中，此版本现在包含用于移动应用程序的单独模板。 首先，您将了解每个模板的一些相关功能。 然后，使用正确的方法在不同的平台上正确呈现页面。

<a id="Task_1_-_Exploring_the_Internet_Application_Template"></a>
#### <a name="task-1---exploring-the-internet-application-template"></a>任务 1-浏览 Internet 应用程序模板

1. 打开**Visual Studio**。
2. 选择**文件 |新建 |项目**菜单命令。 在 "**新建项目**" 对话框中，选择 "**视觉C#对象 |Web**模板 "，并选择" **ASP.NET MVC 4 Web 应用程序 "。** 将项目命名为**PhotoGallery**，选择一个位置（或保留默认值），然后单击 **"确定"** 。

    > [!NOTE]
    > 稍后将自定义要创建的 PhotoGallery ASP.NET MVC 4 解决方案。

    ![创建新项目](whats-new-in-aspnet-mvc-4/_static/image1.png "创建新项目")

    *创建新项目*
3. 在 "**新建 ASP.NET MVC 4 项目**" 对话框中，选择 " **Internet 应用程序**" 项目模板，然后单击 **"确定"** 。 请确保已选择 Razor 作为视图引擎。

    ![创建新的 ASP.NET MVC 4 Internet 应用程序](whats-new-in-aspnet-mvc-4/_static/image2.png "创建新的 ASP.NET MVC 4 Internet 应用程序")

    *创建新的 ASP.NET MVC 4 Internet 应用程序*

    > [!NOTE]
    > ASP.NET MVC 3 中引入了 Razor 语法。 其目标是最大程度地减少文件中所需的字符和击键数量，从而实现快速、流畅的编码工作流。 Razor 利用了C#现有/VB （或其他）语言技能，并提供了一个模板标记语法，可实现出色的 HTML 构造工作流。
4. 按**F5**运行解决方案并查看续订的模板。 您可以查看以下功能：

    **新式模板**

    这些模板已续订，提供了更新式的样式。

    ![ASP.NET MVC 4 改变模板](whats-new-in-aspnet-mvc-4/_static/image3.png "MVC 4 改变模板")

    *ASP.NET MVC 4 改变模板*

    ![新建联系人页](whats-new-in-aspnet-mvc-4/_static/image4.png "新建联系人页")

    *新建联系人页*

    **自适应呈现**

    查看调整浏览器窗口的大小，并注意页面布局如何动态适应新的窗口大小。 这些模板使用自适应呈现技术在桌面和移动平台中正确呈现，无需进行任何自定义。

    ![不同浏览器大小的 ASP.NET MVC 4 项目模板](whats-new-in-aspnet-mvc-4/_static/image5.png "不同浏览器大小的 ASP.NET MVC 4 项目模板")

    *不同浏览器大小的 ASP.NET MVC 4 项目模板*

    **JavaScript 更丰富的 UI**

    默认项目模板的另一增强功能是使用 JavaScript 提供更具交互性的 JavaScript。 在模板中使用的登录名和寄存器链接求知欲了如何使用 jQuery 验证来验证客户端的输入字段。

    ![jQuery 验证](whats-new-in-aspnet-mvc-4/_static/image6.png)

    *jQuery 验证*

    > [!NOTE]
    > 请注意两个登录部分，在第一部分中，你可以使用站点中的注册帐户登录，也可以使用其他身份验证服务（例如，默认情况下禁用）登录。
5. 关闭浏览器以停止调试器并返回到 Visual Studio。
6. 打开位于**应用\_Start**文件夹下的文件**AuthConfig.cs** 。
7. 删除最后一行中的注释，为*OAuth*身份验证注册 Google 客户端。

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample1.cs)]

    > [!NOTE]
    > 请注意，可以使用任何 OpenID 或 OAuth 服务（如 Facebook、Twitter、Microsoft 等）轻松启用身份验证。
8. 按**F5**运行解决方案，然后导航到登录页。
9. 选择 " **Google**服务" 以登录。

    ![选择登录服务](whats-new-in-aspnet-mvc-4/_static/image7.png)

    *选择登录服务*
10. 使用 Google 帐户登录。
11. 允许站点（localhost）从 Google 帐户中检索信息。
12. 最后，你必须在站点中注册以关联 Google 帐户。

   ![关联 Google 帐户](whats-new-in-aspnet-mvc-4/_static/image8.png)

   *关联 Google 帐户*
13. 关闭浏览器以停止调试器并返回到 Visual Studio。
14. 现在，浏览解决方案，查看项目模板中的 ASP.NET MVC 4 引入的一些其他新功能。

   ![ASP.NET MVC 4 Internet 应用程序项目模板](whats-new-in-aspnet-mvc-4/_static/image9.png "ASP.NET MVC 4 Internet 应用程序项目模板")

   *ASP.NET MVC 4 Internet 应用程序项目模板*

    - **HTML 5 标记**

       浏览模板视图以找出新的主题标记。

       ![新模板，使用 Razor 和 HTML5 标记关于 cshtml。](whats-new-in-aspnet-mvc-4/_static/image10.png "新模板，使用 Razor 和 HTML5 标记关于 cshtml。")

       *新模板，使用 Razor 和 HTML5 标记（关于 cshtml）。*
    - **更新的 JavaScript 库**

       ASP.NET MVC 4 默认模板现在包括 KnockoutJS，这是一个 JavaScript MVVM 框架，可让你使用 JavaScript 和 HTML 创建丰富且响应迅速的 web 应用程序。 与在 MVC3 中一样，jQuery 和 jQuery UI 库也包含在 ASP.NET MVC 4 中。

     > [!NOTE]
     > 可在以下链接中获取有关 KnockOutJS 库的详细信息： [[http://learn.knockoutjs.com/](http://learn.knockoutjs.com/)](http://learn.knockoutjs.com/)。 此外，还可以了解[[http://docs.jquery.com/](http://docs.jquery.com/)](http://docs.jquery.com/)中的 jQuery 和 jquery UI。

<a id="Task_2_-_Exploring_the_Mobile_Application_Template"></a>
#### <a name="task-2---exploring-the-mobile-application-template"></a>任务 2-浏览移动应用程序模板

ASP.NET MVC 4 简化了移动和平板浏览器的网站开发。 此模板的应用程序结构与 Internet 应用程序模板相同（请注意，控制器代码几乎完全相同），但其样式已修改为在基于触摸的移动设备中正确呈现。

1. 选择**文件 |新建 |项目**菜单命令。 在 "**新建项目**" 对话框中，选择 "**视觉C#对象 |Web**模板 "，并选择" **ASP.NET MVC 4 Web 应用程序 "。** 将项目命名为**PhotoGallery**，选择一个位置（或保留默认值），选择 &quot;添加到解决方案&quot; 并单击 **"确定"** 。
2. 在 "**新建 ASP.NET MVC 4 项目**" 对话框中，选择 "**移动应用程序**" 项目模板，然后单击 **"确定"** 。 请确保已选择 Razor 作为视图引擎。

    ![创建新的 ASP.NET MVC 4 移动应用程序](whats-new-in-aspnet-mvc-4/_static/image11.png "创建新的 ASP.NET MVC 4 移动应用程序")

    *创建新的 ASP.NET MVC 4 移动应用程序*
3. 现在，你可以浏览解决方案并查看适用于 mobile 的 ASP.NET MVC 4 解决方案模板引入的一些新功能：

    - **jQuery Mobile 库**

        "移动应用程序" 项目模板包含 jQuery Mobile 库，这是用于移动浏览器兼容性的开源库。 jQuery Mobile 可对支持 CSS 和 JavaScript 的移动浏览器应用渐进增强。 渐进式增强功能允许所有浏览器显示网页的基本内容，而仅允许最强大的浏览器显示丰富的内容。 JQuery Mobile style 中包含的 JavaScript 和 CSS 文件可帮助移动浏览器适应屏幕内容，而无需在页面标记中进行任何更改。

        ![jQuery-包含模板中的](whats-new-in-aspnet-mvc-4/_static/image12.png)

        *模板中包含的 jQuery mobile 库*
    - **基于 HTML5 的标记**

        ![移动应用程序-使用-HTML5-标记](whats-new-in-aspnet-mvc-4/_static/image13.png)

        *使用 HTML5 标记的移动应用程序模板（登录名和索引. cshtml）*
4. 按**F5**运行解决方案。
5. 打开**Windows Phone 7 模拟器**。
6. 在手机的 "开始" 屏幕上，打开 Internet Explorer。 查看桌面应用程序的启动 URL，并从手机浏览到该 URL （例如 `http://localhost:[PortNumber]/`）。
7. 现在，你可以输入登录页面或查看 "关于" 页。 请注意，网站的样式基于适用于移动设备的新地铁应用。 ASP.NET MVC 4 项目模板已正确显示在移动设备上，请确保页面的所有元素都可见且已启用。 请注意，标题上的链接足够大，可以单击或点击。

    ![移动设备中的项目模板页](whats-new-in-aspnet-mvc-4/_static/image14.png "移动设备中的项目模板页")

    *移动设备中的项目模板页*
8. 新模板还使用**视区 meta 标记**。 大多数移动浏览器定义虚拟浏览器窗口或 &quot;视区的宽度&quot;，该值大于移动设备的实际宽度。 这使移动浏览器能够在虚拟显示内显示整个网页。 利用**视区 meta 标记**，web 开发人员可以设置移动设备上浏览器区域的宽度、高度和比例 **。** 适用于移动应用程序的 ASP.NET MVC 4 模板在布局模板（*Views\Shared\_layout*）中将视区设置为设备宽度（&quot;width = 设备宽度&quot;），以便所有页面都将其视区设置为设备屏幕宽度。 请注意，视区 meta 标记将不会更改默认浏览器视图。
9. 打开位于 "视图" 中 **\_布局 ...** **共享**文件夹，并注释视区 meta 标记。 运行应用程序（如果尚未打开），并查看不同之处。

[!code-cshtml[Main](whats-new-in-aspnet-mvc-4/samples/sample2.cshtml)]

![注释视区 meta 标记后的站点](whats-new-in-aspnet-mvc-4/_static/image15.png "注释视区 meta 标记后的站点")

*注释视区 meta 标记后的站点*
10. 在 Visual Studio 中，按**SHIFT** + **F5**停止调试应用程序。
11. 取消注释视区 meta 标记。

[!code-cshtml[Main](whats-new-in-aspnet-mvc-4/samples/sample3.cshtml)]

<a id="Task_3_-_Using_Adaptive_Rendering"></a>
#### <a name="task-3---using-adaptive-rendering"></a>任务 3-使用自适应呈现

在此任务中，你将学习在不进行任何自定义的情况下，在移动设备和 Web 浏览器上正确呈现网页的另一种方法。 您已经使用了类似用途的视区 meta 标记。 现在，您将满足另一个功能强大的方法：*自适应呈现*。

自适应呈现是一种技术，使用**CSS3 媒体查询**自定义应用于页面的样式。 媒体查询定义样式表中的条件，在特定条件下对 CSS 样式进行分组。 仅当条件为 true 时，才将样式应用于已声明的对象。

自适应呈现技术提供的灵活性使您能够在不同设备上显示网站。 您可以在单个样式表中定义任意数量的样式，而无需编写逻辑代码来选择样式。 因此，它是一种非常巧妙的页面样式调整方法，因为它减少了用于呈现的代码和逻辑的数量。 另一方面，带宽消耗会增加，因为 CSS 文件的大小可能会略微增长。

通过使用自适应呈现技术，你的网站将**正常显示，而与浏览器无关。** 但是，您应该考虑是否需要考虑带宽额外负载。

> [!NOTE]
> 媒体查询的基本格式为： @media \[范围： all |手持式 |打印 |投影 |屏幕\] （[属性：值] 和 。[属性：值]）

媒体查询示例： &gt; **@media all 和（最大宽度：1000px）和（最小宽度：700px） {}：** 700px 和1000px 之间的所有解决方法。

> **@media 屏幕和（最小宽度：400px）和（最大宽度：700px） {...}：** 仅适用于屏幕。 分辨率必须介于400和700px 之间。
> 
> **@media 手持型和（最小宽度：20em）、屏幕和（最小宽度：20em） {...}：** 对于手持设备（移动设备和设备）和屏幕。 最小宽度必须大于20em。
> 
> 可以在[W3C 网站](http://www.w3.org/TR/css3-mediaqueries/)上找到有关此内容的详细信息。

现在，你将浏览自适应呈现的工作原理，提高 ASP.NET MVC 4 默认网站模板的可读性。

1. 打开你在任务1创建的**PhotoGallery**解决方案，然后选择 " **PhotoGallery** " 项目。 按**F5**运行解决方案。
2. 调整浏览器的宽度，将窗口设置为半或小于其原始大小的四分之一。 请注意标题中的项会发生什么情况：某些元素将不会显示在标头的可见区域中。
3. 从 Visual Studio 解决方案资源管理器中打开位于**内容**项目文件夹中的**web.config**文件。 按**CTRL + F**打开 Visual Studio 集成搜索，并编写 `@media` 以查找**CSS 媒体查询**。

    此模板中定义的媒体查询条件的工作方式如下：当浏览器的窗口大小低于**850 像素**时，应用的 CSS 规则是此媒体块中定义的规则。

    ![查找媒体查询](whats-new-in-aspnet-mvc-4/_static/image16.png "查找媒体查询")

    *查找媒体查询*
4. 将 850 px 中设置的最大宽度属性值替换为**10px**，以便禁用自适应呈现，并按**CTRL + S**保存更改。 返回到浏览器，并按**CTRL + F5**以使用您所做的更改刷新页面。 请注意，在调整窗口的宽度时，两个页面之间的差异。

    ![在左侧，页面正在应用 @media 样式，则省略样式](whats-new-in-aspnet-mvc-4/_static/image17.png "在左侧，页面正在应用 @media 样式，则省略样式")

    *在左侧，页面正在应用 @media 样式，则省略样式*

    现在，我们来看看移动设备上发生的情况：

    ![在左侧，页面正在应用 @media 样式，则省略样式](whats-new-in-aspnet-mvc-4/_static/image18.png "在左侧，页面正在应用 @media 样式，则省略样式")

    *在左侧，页面正在应用 @media 样式，则省略样式*

    尽管你会注意到，在 Web 浏览器中呈现页面时所做的更改并不重要，但在使用移动设备时，差别会变得更加明显。 在图像的左侧，可以看到自定义样式提高了可读性。

    自适应呈现可用于更多方案，使您可以更轻松地将条件样式应用于网站并使用巧妙的方法解决常见的样式问题。

    视区 meta 标记和 CSS 媒体查询并不特定于 ASP.NET MVC 4，因此你可以在任何 web 应用程序中利用这些功能。
5. 在 Visual Studio 中，按**SHIFT** + **F5**停止调试应用程序。

<a id="Exercise2"></a>

<a id="Exercise_2_Creating_the_Photo_Gallery_Web_Application"></a>
### <a name="exercise-2-creating-the-photo-gallery-web-application"></a>练习2：创建照片库 Web 应用程序

在此练习中，您将使用照片库应用程序来显示照片。 你将从 ASP.NET MVC 4 项目模板开始，然后添加功能以从服务中检索照片，并将其显示在主页中。

在以下练习中，你将更新此解决方案以增强它在移动设备上的显示方式。

<a id="Task_1_-_Creating_a_Mock_Photo_Service"></a>
#### <a name="task-1---creating-a-mock-photo-service"></a>任务 1-创建模拟照片服务

在此任务中，您将创建照片服务的模拟，以检索将在库中显示的内容。 为此，您将添加一个新的控制器，它将只返回包含每张照片数据的 JSON 文件。

1. 如果尚未打开，请打开**Visual Studio** 。
2. 选择**文件 |新建 |项目**菜单命令。 在 "**新建项目**" 对话框中，选择 "**视觉C#对象 |Web**模板 "，并选择" **ASP.NET MVC 4 Web 应用程序 "。** 将项目命名为**PhotoGallery**，选择一个位置（或保留默认值），然后单击 **"确定"** 。 或者，你可以从**练习 1**中的现有 ASP.NET MVC 4 **Internet 应用程序**解决方案继续工作，并跳过下一步。
3. 在 "**新建 ASP.NET MVC 4 项目**" 对话框中，选择 " **Internet 应用程序**" 项目模板，然后单击 **"确定"** 。 请确保选择 "Razor" 作为视图引擎。
4. 在**解决方案资源管理器**中，右键单击项目 **\_"数据**" 文件夹中的 "应用"，然后选择 "**添加 |现有项**。 浏览到此实验室的**Source\Assets\App\_Data**文件夹，并**添加文件。**
5. 创建名为**PhotoController**的新控制器。 为此，请右键单击 "**控制器**" 文件夹，然后单击 "**添加**"，然后选择 "**控制器"。** 填写控制器名称，保留**空 MVC 控制器**模板并单击 "**添加**"。

    ![添加 PhotoController](whats-new-in-aspnet-mvc-4/_static/image19.png "添加 PhotoController")

    *添加 PhotoController*
6. 将**Index**方法替换为以下**库**操作，并返回最近添加到项目的 JSON 文件中的内容。

    （代码段- *ASP.NET MVC 4 实验室-Ex02 操作*）

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample4.cs)]
7. 按**F5**运行解决方案，然后浏览到以下 URL，以便测试模拟 photo service： `http://localhost:[port]/photo/gallery` （[端口] 值取决于启动应用程序的当前端口）。 对此 URL 的请求应检索**照片 json**文件的内容。

    ![测试模拟照片服务](whats-new-in-aspnet-mvc-4/_static/image20.png "测试模拟照片服务")

    *测试模拟照片服务*

在实际实现中，可以使用[ASP.NET Web API](../../../../web-api/index.md)来实现照片库服务。 ASP.NET Web API 是一种框架，可让你轻松地生成可访问范围广泛的客户端（包括浏览器和移动设备）的 HTTP 服务。 ASP.NET Web API 是用于在 .NET Framework 上生成 RESTful 应用程序的理想平台。

<a id="Task_2_-_Displaying_the_Photo_Gallery"></a>
#### <a name="task-2---displaying-the-photo-gallery"></a>任务 2-显示照片库

在此任务中，您将使用在本练习的第一个任务中创建的模拟服务来更新主页以显示照片库。 您将添加模型文件并更新库视图。

1. 在 Visual Studio 中，按**SHIFT** + **F5**停止调试应用程序。
2. 在 "**模型**" 文件夹中创建**Photo**类。 为此，请右键单击 "**模型**" 文件夹，选择 "**添加**"，然后单击 "**类**"。 然后，将名称设置为**Photo.cs** ，并单击 "**添加**"。
3. 将以下成员添加到**Photo**类中。

    （代码段- *ASP.NET MVC 4 实验室-Ex02*）

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample5.cs)]
4. 从“控制器”文件夹打开 HomeController.cs 文件。
5. 添加下面的 using 语句。

    （代码段- *ASP.NET MVC 4 Lab-Ex02-HomeController using*）

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample6.cs)]
6. 更新**索引**操作以使用**HttpClient**检索库数据，然后使用**JavaScriptSerializer**将其反序列化到视图模型。

    （代码段- *ASP.NET MVC 4 Ex02-索引操作*）

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample7.cs)]
7. 打开位于 Views\Home 文件夹下的 **文件，** 并将所有内容替换为以下代码。

    此代码循环访问从服务中检索到的所有照片，并将其显示为未排序列表。

    （代码段- *ASP.NET MVC 4 Ex02-Photo List*）

    [!code-cshtml[Main](whats-new-in-aspnet-mvc-4/samples/sample8.cshtml)]
8. 在**解决方案资源管理器**中，右键单击项目的 "**内容**" 文件夹，然后选择 "**添加 |现有项**。 浏览到此实验室的**Source\Assets\Content**文件夹并添加**web.config 文件。** 需要确认它的替换。 如果已打开**web.config**文件，则还必须确认是否要重新加载文件。
9. 打开文件资源管理器，将位于此实验室的**Source\Assets**文件夹下的整个**照片**文件夹复制到解决方案资源管理器中项目的根文件夹下。
10. 运行该应用程序。 现在，你应看到在库中显示照片的主页。

    ![照片库](whats-new-in-aspnet-mvc-4/_static/image21.png "照片库")

    *照片库*
11. 在 Visual Studio 中，按**SHIFT** + **F5**停止调试应用程序。

<a id="Exercise3"></a>

<a id="Exercise_3_Adding_support_for_mobile_devices"></a>
### <a name="exercise-3-adding-support-for-mobile-devices"></a>练习3：添加对移动设备的支持

ASP.NET MVC 4 中的一个重要更新是支持移动开发。 在此练习中，你将通过扩展你在上一练习中创建的 PhotoGallery 解决方案来浏览移动应用程序的 ASP.NET MVC 4 新功能。

<a id="Task_1_-_Installing_jQuery_Mobile_in_an_ASPNET_MVC_4_Application"></a>
#### <a name="task-1---installing-jquery-mobile-in-an-aspnet-mvc-4-application"></a>任务 1-在 ASP.NET MVC 4 应用程序中安装 jQuery Mobile

1. 打开位于**Source/section-cs-MobileSupport/begin/** Folder 的**begin**解决方案。 否则，你可以继续使用通过完成前一练习所获得的**最终**解决方案。

   1. 如果你打开了提供的**开始**解决方案，则需要下载一些缺少的 NuGet 包，然后再继续。 为此，请单击 "**项目**" 菜单并选择 "**管理 NuGet 包**"。
   2. 在 "**管理 NuGet 包**" 对话框中，单击 "**还原**" 以下载缺少的包。
   3. 最后，通过单击 "**生成** | **生成解决方案**" 来生成解决方案。

      > [!NOTE]
      > 使用 NuGet 的优点之一是，无需将所有库都送到项目中，从而减少了项目的大小。 使用 NuGet 功能，通过在包 .config 文件中指定包版本，你可以在首次运行项目时下载所有必需的库。 这就是在从此实验室打开现有解决方案之后需要运行这些步骤的原因。
2. 通过单击 " > **NuGet 包管理器** > **包管理器控制台**" 菜单选项中的 "**工具**" 打开**程序包管理器控制台**。

    ![打开 NuGet 包管理器控制台](whats-new-in-aspnet-mvc-4/_static/image22.png "打开 NuGet 包管理器控制台")

    *打开 NuGet 包管理器控制台*
3. 在 "包管理器控制台" 中运行以下命令以安装**jQuery** . node.js 包。

    jQuery Mobile 是用于构建触摸优化 web UI 的开源库。 JQuery. node.js NuGet 包包含用于将 jQuery Mobile 与 ASP.NET MVC 4 应用程序结合使用的帮助程序。

    > [!NOTE]
    > 通过运行以下命令，你将从 Nuget 下载 jQuery library。

    PM

    [!code-powershell[Main](whats-new-in-aspnet-mvc-4/samples/sample9.ps1)]

    此命令安装 jQuery Mobile 和一些 helper 文件，包括以下内容：

    - **Views/Shared/\_layout。** node.js：是一种针对小屏幕优化的基于 jQuery mobile 的布局。 当网站收到来自移动浏览器的请求时，它会将原始布局（\_Layout）替换为此布局。
    - 视图切换器组件：由**Views/Shared/\_ViewSwitcher**分部视图和**ViewSwitcherController.cs**控制器组成。 此组件将在移动浏览器上显示一个链接，以使用户能够切换到页面的桌面版本。  
        ![具有移动支持的照片库项目](whats-new-in-aspnet-mvc-4/_static/image23.png "Ph带有移动支持的照片库项目

        *具有移动支持的照片库项目*
4. 注册移动捆绑包。 为此，请打开**Global.asax.cs**文件并添加以下行。

    （代码段- *ASP.NET MVC 4 Ex03-注册移动包*）

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample10.cs)]
5. 使用桌面 web 浏览器运行应用程序。
6. 打开位于 "开始" 菜单中的**Windows Phone 7 仿真程序** **|所有程序 |Windows Phone SDK 7.1 |Windows Phone 模拟器。**
7. 在手机的 "开始" 屏幕上，打开 Internet Explorer。 查看应用程序启动的 URL，并通过手机浏览器（例如 `http://localhost:[PortNumber]/`）浏览到该 URL。

    你会注意到，在 Windows Phone 模拟器中，你的应用程序的外观有所不同，因为 jQuery. node.js 在你的项目中创建了新资产，其中显示了为移动设备优化的视图。

    请注意手机顶部的消息，其中显示了切换到桌面视图的链接。 此外，在应用程序中安装的包所创建的 **\_布局.** node.js 布局也是如此。

    > [!NOTE]
    > 到目前为止，没有可返回到移动视图的链接。 它将包含在更高版本中。

    ![照片库主页的移动视图](whats-new-in-aspnet-mvc-4/_static/image24.png "照片库主页的移动视图")

    *照片库主页的移动视图*
8. 在 Visual Studio 中，按**SHIFT** + **F5**停止调试应用程序。

<a id="Task_2_-_Creating_Mobile_Views"></a>
#### <a name="task-2---creating-mobile-views"></a>任务 2-创建移动视图

在此任务中，你将创建一个移动版本的索引视图，并将内容改编以便在移动设备中更好地显示。

1. 复制**Views\Home\Index.cshtml**视图并将其粘贴以创建副本，并将新文件重命名**为 "** "。
2. 打开新创建的**索引.** node.js 视图，并将现有 &lt;ul&gt; 标记替换为此代码。 通过执行此操作，你将使用 jQuery Mobile 数据批注更新 &lt;ul&gt; 标记，以使用 jQuery 中的移动主题。

    [!code-html[Main](whats-new-in-aspnet-mvc-4/samples/sample11.html)]

    > [!NOTE] 
    > 
    > 请注意：
    > 
    > - 设置为**listview**的**数据角色**属性将使用 listview 样式呈现列表。
    > 
    > - "**数据嵌入**" 特性设置为 "true" 将显示具有圆角边框和边距的列表。
    > 
    > - "**数据筛选器**" 属性设置为 " **true** " 将生成一个搜索框。
    > 
    > 可以在项目文档中了解有关 jQuery Mobile 约定的详细信息： [ [http://jquerymobile.com/demos/1.1.1/](http://jquerymobile.com/demos/1.1.1/)](http://jquerymobile.com/demos/1.1.1/)
3. 按**CTRL + S**保存更改。
4. 切换到**Windows Phone 模拟器**并刷新站点。 请注意库列表的新外观和外观，以及顶部的新 "搜索" 框。 然后，在 "搜索" 框中键入一个词（例如， **Tulips**），在照片库中开始搜索。

    ![使用带有筛选功能的 listview 样式的库](whats-new-in-aspnet-mvc-4/_static/image25.png "使用带有筛选功能的 listview 样式的库")

    *使用带有筛选功能的 listview 样式的库*

    总而言之，已使用 View Mobilizer 食谱创建索引视图的副本，该副本具有 &quot;移动&quot; 后缀。 此后缀指示 ASP.NET MVC 4，每个从移动设备生成的请求都将使用此索引副本。 此外，还更新了索引视图的移动版本，使用 jQuery Mobile 增强了移动设备中的站点外观。
5. 返回到**Content**文件夹下的 Visual Studio**并打开 "node.js"。**
6. 修复照片标题的位置，使其显示在图像的右侧。 为此，请将以下代码添加到 node.js**文件中。**

    CSS

    [!code-css[Main](whats-new-in-aspnet-mvc-4/samples/sample12.css)]
7. 按**CTRL + S**保存更改。
8. 切换回**Windows Phone 模拟器**并刷新站点。 请注意，照片标题现在正确定位。

    ![位于图像右侧的标题](whats-new-in-aspnet-mvc-4/_static/image26.png "位于图像右侧的标题")

    *位于图像右侧的标题*

<a id="Task_3_-_jQuery_Mobile_Themes"></a>
#### <a name="task-3---jquery-mobile-themes"></a>任务 3-jQuery Mobile Themes

JQuery Mobile 中的每个布局和小组件都围绕面向对象的新 CSS 框架设计，使你可以将完整的统一视觉对象设计主题应用到站点和应用程序。

jQuery Mobile 的默认主题包括5个样本，其中包含字母（a、b、c、d、e），用于快速参考。

在此任务中，你将更新移动布局以使用不同于默认设置的主题。

1. 切换回 Visual Studio。
2. 打开位于 Views\Shared 中的 **\_** 文件。
3. 查找数据角色设置为 &quot;页面&quot; 并将**数据主题**更新为 &quot;**e**&quot;的 div 元素。

    [!code-html[Main](whats-new-in-aspnet-mvc-4/samples/sample13.html)]
4. 按**CTRL + S**保存更改。
5. 刷新**Windows Phone 模拟器**中的站点，并注意新的颜色方案。

    ![具有不同配色方案的移动版式](whats-new-in-aspnet-mvc-4/_static/image27.png "具有不同配色方案的移动版式")

    *具有不同配色方案的移动版式*

<a id="Task_4_-_Using_the_View-Switcher_Component_and_the_Browser_Overriding_Features"></a>
#### <a name="task-4---using-the-view-switcher-component-and-the-browser-overriding-features"></a>任务 4-使用视图切换器组件和浏览器覆盖功能

移动优化的网页约定是添加一个链接，其文本的内容类似于桌面视图或完整站点模式，使用户能够切换到页面的桌面版本。 JQuery. node.js 包在 **\_Layout**视图中包含用于此目的的示例**视图切换**器组件。

![用于切换到桌面视图的链接](whats-new-in-aspnet-mvc-4/_static/image28.png "用于切换到桌面视图的链接")

*用于切换到桌面视图的链接*

视图切换器使用称为 "**浏览器重写**" 的新功能。 此功能使应用程序可以处理请求，就好像这些请求来自于它们实际来自的浏览器（用户代理）。

在此任务中，你将了解 jQuery 所添加的视图切换器的示例实现，而新浏览器则覆盖 ASP.NET MVC 4 中的功能。

1. 切换回 Visual Studio。
2. 打开位于 Views\Shared 文件夹下的 **\_** " " 视图，并注意作为分部视图引用的视图切换器组件。

    ![使用视图切换器组件的移动布局](whats-new-in-aspnet-mvc-4/_static/image29.png "使用视图切换器组件的移动布局")

    *使用视图切换器组件的移动布局*
3. 打开 **\_ViewSwitcher**分部视图。

    分部视图使用新方法**ViewContext GetOverriddenBrowser （）** 来确定 web 请求的来源，并显示相应的链接以切换到桌面或移动视图。

    **GetOverriddenBrowser**方法返回一个**HttpBrowserCapabilitiesBase**实例，该实例对应于当前为请求设置的用户代理（实际或重写）。 可以使用此值获取属性，如**IsMobileDevice**。

    ![ViewSwitcher 分部视图](whats-new-in-aspnet-mvc-4/_static/image30.png "ViewSwitcher 分部视图")

    *ViewSwitcher 分部视图*
4. 打开位于 "**控制器**" 文件夹中的**ViewSwitcherController.cs**类。 查看 ViewSwitcher 组件中的链接是否调用了 SwitchView 操作，并注意新的 HttpContext 方法。

    - **ClearOverriddenBrowser （）** 方法删除当前请求的任何重写的用户代理。
    - **SetOverriddenBrowser （）** 方法使用指定的用户代理覆盖请求的实际用户代理值。  
        ![ViewSwitcher 控制器](whats-new-in-aspnet-mvc-4/_static/image31.png "ViewSwitcher 控制器 "）  
*ViewSwitcher 控制器*

        浏览器重写是 ASP.NET MVC 4 的一项核心功能，即使不安装 jQuery. node.js 包也是如此。 但是，此功能只会影响视图、布局和分部视图，而不会影响依赖于请求 .Browser 对象的任何功能。

<a id="Task_5_-_Adding_the_View-Switcher_in_the_Desktop_View"></a>
#### <a name="task-5---adding-the-view-switcher-in-the-desktop-view"></a>任务 5-在桌面视图中添加视图切换器

在此任务中，你将更新桌面布局以包含视图切换器。 这将允许移动用户在浏览桌面视图时返回到移动视图。

1. 刷新**Windows Phone 模拟器**中的站点。
2. 单击库顶部的 "**桌面视图**" 链接。 请注意，桌面视图中没有视图切换器允许返回到移动视图。
3. 返回到 Visual Studio 并打开 **\_布局. cshtml**视图。
4. 查找 login 节，并插入一个对 **\_LogOnPartial**分部视图下面 **\_ViewSwitcher**分部视图的调用。 然后，按**CTRL + S**保存更改。

    [!code-cshtml[Main](whats-new-in-aspnet-mvc-4/samples/sample14.cshtml)]
5. 按**CTRL + S**保存更改。
6. 刷新 Windows Phone 模拟器中的页面，然后双击屏幕进行放大。 请注意，主页现在会显示从移动到桌面视图切换的**移动视图**链接。

    ![在桌面视图中呈现的视图切换器](whats-new-in-aspnet-mvc-4/_static/image32.png "在桌面视图中呈现的视图切换器")

    *在桌面视图中呈现的视图切换器*
7. 再次切换到移动视图并浏览到 "**关于**" 页（ http://localhost [port]/Home/About）。 请注意，即使尚未创建 "关于" 视图，"关于" 页也会使用移动布局（\_Layout）来显示。

    ![关于页面](whats-new-in-aspnet-mvc-4/_static/image33.png "“关于”页面")

    *关于页面*
8. 最后，在桌面 Web 浏览器中打开该站点。 请注意，前面的所有更新都不会影响桌面视图。

    ![PhotoGallery 桌面视图](whats-new-in-aspnet-mvc-4/_static/image34.png "PhotoGallery 桌面视图")

    *PhotoGallery 桌面视图*

<a id="Task_6_-_Creating_New_Display_Modes"></a>
#### <a name="task-6---creating-new-display-modes"></a>任务 6-创建新的显示模式

使用新的显示模式功能，应用程序可以根据生成请求的浏览器选择视图。 例如，如果桌面浏览器请求主页，应用程序将返回**Views\Home\Index.cshtml**模板。 然后，如果移动浏览器请求主页，应用程序将返回**Views\Home\Index.mobile.cshtml**模板。

在此任务中，您将为 iPhone 设备创建自定义布局，并且必须模拟来自 iPhone 设备的请求。 为此，可以使用 iPhone 模拟器/模拟器（如[电气移动模拟器](http://www.electricplum.com/)）或带有修改用户代理的加载项的浏览器。 有关如何在 Safari 浏览器中设置用户代理字符串以模拟 iPhone 的说明，请参阅[如何让 Safari](http://www.davidalison.com/2008/05/how-to-let-safari-pretend-its-ie.html)在 David Alison 的博客中伪装成 IE。

**请注意，此任务是可选的，可以在整个实验室中继续执行，而无需执行此任务。**

1. 在 Visual Studio 中，按**SHIFT** + **F5**停止调试应用程序。
2. 打开**Global.asax.cs**并添加以下 using 语句。

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample15.cs)]
3. 将以下突出显示的代码添加到应用程序\_Start 方法。

    （代码段- *ASP.NET MVC 4 Lab-Ex03-IPhone DisplayMode*）

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample16.cs)]

已在静态**DisplayModeProvider**静态列表中注册了**名为 &quot;iPhone&quot;** 的新 DefaultDisplayMode，该名称将与每个传入请求匹配。 如果传入请求包含 &quot;iPhone&quot;的字符串，则 ASP.NET MVC 将查找其名称包含 &quot;iPhone&quot; 后缀的视图。 0参数指示新模式的特定方式;例如，此视图比常规 &quot;移动&quot; 规则更具体，与移动设备的请求相匹配。

此代码运行后，当 iPhone 浏览器生成请求时，你的应用程序将使用**Views\Shared\\_Layout**将在后续步骤中创建的布局。

> [!NOTE]
> 这种测试 iPhone 请求的方法已为演示目的进行了简化，并可能不会按预期方式针对每个 iPhone 用户代理字符串（例如，测试区分大小写）。

4. 在 Views\Shared 文件夹中创建 **\_** 的文件的副本，并将该副本重命名为 &quot;\_&quot;**Layout** 。
5. 打开你在上一步中创建 **\_Layout. cshtml** 。
6. 查找数据角色属性设置为 "**页**" 的 div 元素，并将 "**数据"-"主题**" 属性更改**为 &quot;&quot;** 。

[!code-cshtml[Main](whats-new-in-aspnet-mvc-4/samples/sample17.cshtml)]

现在，ASP.NET MVC 4 应用程序中有3个布局：

1. **\_布局。 cshtml**：用于桌面浏览器的默认布局。
2. **\_layout**：移动设备使用的默认布局。
3. **\_layout**： iphone 设备的特定布局，使用不同的配色方案来区分 \_的布局。
7. 按**F5**运行应用程序并浏览**Windows Phone 模拟器**中的站点。
8. 打开**iphone 模拟器**（有关如何安装和配置 iPhone 模拟器的说明，请参阅[附录 C](#AppendixC) ），并浏览到站点。 请注意，每个电话使用特定的模板。

    ![使用-设备 2-不同的视图](whats-new-in-aspnet-mvc-4/_static/image35.png)

    *为每个移动设备使用不同的视图*

<a id="Exercise4"></a>

<a id="Exercise_4_Using_Asynchronous_Controllers"></a>
### <a name="exercise-4-using-asynchronous-controllers"></a>练习4：使用异步控制器

Microsoft .NET Framework 4.5 介绍了和 Visual Basic 中C#的新语言功能，以便为 .net 编程中的异步提供新的基础。 这一新基础使异步编程与-相关，并与同步编程一样简单。 现在可以使用**AsyncController**类在 ASP.NET MVC 4 中编写异步操作方法。 对于长时间运行的非 CPU 绑定请求，可以使用异步操作方法。 这可以避免在处理请求时阻止 Web 服务器执行工作。 AsyncController 类通常用于长时间运行的 Web 服务调用。

本练习介绍 ASP.NET MVC 4 中异步操作的基本知识。 如果需要深入了解，可以查看以下文章： [ [https://msdn.microsoft.com/library/ee728598%28v=vs.100%29.aspx](https://msdn.microsoft.com/library/ee728598%28v=vs.100%29.aspx)](https://msdn.microsoft.com/library/ee728598%28v=vs.100%29.aspx)

<a id="Task_1_-_Implementing_an_Asynchronous_Controller"></a>
#### <a name="task-1---implementing-an-asynchronous-controller"></a>任务 1-实现异步控制器

1. 打开位于**Source/Ex4-Async/begin/** Folder 的**begin**解决方案。 否则，你可以继续使用通过完成前一练习所获得的**最终**解决方案。

   1. 如果你打开了提供的**开始**解决方案，则需要下载一些缺少的 NuGet 包，然后再继续。 为此，请单击 "**项目**" 菜单并选择 "**管理 NuGet 包**"。
   2. 在 "**管理 NuGet 包**" 对话框中，单击 "**还原**" 以下载缺少的包。
   3. 最后，通过单击 "**生成** | **生成解决方案**" 来生成解决方案。

      > [!NOTE]
      > 使用 NuGet 的优点之一是，无需将所有库都送到项目中，从而减少了项目的大小。 使用 NuGet 功能，通过在包 .config 文件中指定包版本，你可以在首次运行项目时下载所有必需的库。 这就是在从此实验室打开现有解决方案之后需要运行这些步骤的原因。
2. 从 "**控制器**" 文件夹打开**HomeController.cs**类。
3. 添加以下 using 语句。

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample18.cs)]
4. 更新**HomeController**类，使其从**AsyncController**继承。 从 AsyncController 派生的控制器使 ASP.NET 能够处理异步请求，并且它们仍可为同步操作方法提供服务。

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample19.cs)]
5. 将**async**关键字添加到**Index**方法，并使其返回类型**任务&lt;ActionResult&gt;** 。

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample20.cs)]

    > [!NOTE]
    > **Async**关键字是 .NET Framework 4.5 提供的新关键字之一;它通知编译器此方法包含异步代码。 **Task**对象表示在将来的某个时间点可能完成的异步操作。
6. 替换**客户端。** 使用 await 关键字的完整异步版本的 GetAsync （）调用，如下所示。

    （代码段- *ASP.NET MVC 4 Lab-Ex04-GetAsync*）

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample21.cs)]

    > [!NOTE]
    > 在以前的版本中，你使用**Task**对象的**Result**属性来阻止线程，直到返回结果（同步版本）。
    > 
    > 添加**await**关键字告诉编译器异步等待从方法调用返回的任务。 这意味着，在等待的方法完成后，代码的其余部分将作为回调执行。 需要注意的另一点是，您无需更改您的 try-catch 块即可执行此操作：仍将捕获在后台或前台发生的异常，而不会使用框架提供的处理程序执行任何额外的工作。
7. 更改代码，通过将行替换为新代码来继续异步实现，如下所示

    （代码段- *ASP.NET MVC 4 Lab-Ex04-ReadAsStringAsync*）

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample22.cs)]
8. 运行该应用程序。 你将注意到没有重大更改，但你的代码不会阻止线程池中的线程，从而更好地使用服务器资源和提高性能。

    > [!NOTE]
    > 若要详细了解实验室中新的异步编程功能，请 &quot; **.net 4.5 中的异步编程C#功能，以及**Visual Studio 培训工具包中包含的和 Visual Basic&quot;。

<a id="Task_2_-_Handling_Time-Outs_with_Cancellation_Tokens"></a>
#### <a name="task-2---handling-time-outs-with-cancellation-tokens"></a>任务 2-用取消标记处理超时

返回任务实例的异步操作方法还可以支持超时。 在此任务中，您将更新 Index 方法代码，以使用取消标记处理超时情况。

1. 返回到 Visual Studio 并按**SHIFT + F5**停止调试。
2. 将以下 using 语句添加到**HomeController.cs**文件。

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample23.cs)]
3. 更新索引操作以接收**CancellationToken**参数。

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample24.cs)]
4. 更新**GetAsync**调用以传递取消标记。

    （代码段- *ASP.NET MVC 4 Lab-Ex04-SendAsync With CancellationToken*）

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample25.cs)]
5. 使用设置为500毫秒的**AsyncTimeout**特性装饰*索引*方法，并使用配置为通过重定向到**超时**视图来处理**TaskCanceledException**的**HandleError**属性。

    （代码段- *ASP.NET MVC 4 Lab-Ex04*）

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample26.cs)]
6. 打开**PhotoController**类并更新**库**方法，以延迟执行1000毫秒（1秒）以模拟长时间运行的任务。

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample27.cs)]
7. 打开 web.config**文件，** 并添加以下元素，启用自定义错误。

    [!code-xml[Main](whats-new-in-aspnet-mvc-4/samples/sample28.xml)]
8. 在**Views\Shared**中创建一个名为**超时**的新视图，并使用默认布局。 在解决方案资源管理器中，右键单击**Views\Shared**文件夹，然后选择 "**添加 |视图**。

    ![为每个移动设备使用不同的视图](whats-new-in-aspnet-mvc-4/_static/image36.png "为每个移动设备使用不同的视图")

    *为每个移动设备使用不同的视图*
9. 按如下所示更新**超时**视图内容。

    [!code-cshtml[Main](whats-new-in-aspnet-mvc-4/samples/sample29.cshtml)]
10. 运行应用程序并导航到根 URL。 你添加了一个**线程。睡眠**1000 毫秒，你将会收到超时错误，该错误由**AsyncTimeout**属性生成，并由**HandleError**属性捕获。

    ![处理超时异常](whats-new-in-aspnet-mvc-4/_static/image37.png "处理超时异常")

    *处理超时异常*

> [!NOTE]
> 此外，还可以遵循[附录 D：使用 Web 部署发布 ASP.NET MVC 4 应用程序的](#AppendixD)Microsoft Azure 网站。

<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a>总结

在此动手实验中，你已发现 ASP.NET MVC 4 中的一些新功能。 讨论了以下概念：

- 充分利用 ASP.NET MVC 项目模板的增强功能，包括新的移动应用程序项目模板
- 使用 HTML5 视区属性和 CSS 媒体查询改善移动设备上的显示
- 使用 jQuery Mobile 进行渐进式增强，并构建触摸优化 web UI
- 创建特定于移动设备的视图
- 使用视图切换器组件在应用程序的移动视图与桌面视图之间切换
- 使用任务支持创建异步控制器

<a id="AppendixA"></a>

<a id="Appendix_A_Using_Code_Snippets"></a>
## <a name="appendix-a-using-code-snippets"></a>附录 A：使用代码片段

使用代码片段，您可以随时获得所需的全部代码。 实验室文档将告诉你何时可以使用它们，如下图所示。

![使用 Visual Studio code 代码段将代码插入到项目中](whats-new-in-aspnet-mvc-4/_static/image38.png "使用 Visual Studio code 代码段将代码插入到项目中")

*使用 Visual Studio code 代码段将代码插入到项目中*

***使用键盘添加代码片段（C#仅限）***

1. 将光标放在要插入代码的位置。
2. 开始键入代码片段名称（不含空格或连字符）。
3. 请注意，IntelliSense 显示匹配的代码段名称。
4. 选择正确的代码段（或保留键入内容，直到选择了整个代码段的名称）。
5. 按 Tab 键两次，将代码段插入到光标位置。

![开始键入代码片段名称](whats-new-in-aspnet-mvc-4/_static/image39.png "开始键入代码片段名称")

*开始键入代码片段名称*

![按 Tab 键以选择突出显示的代码段](whats-new-in-aspnet-mvc-4/_static/image40.png "按 Tab 键以选择突出显示的代码段")

*按 Tab 键以选择突出显示的代码段*

![再次按 Tab 键，代码片段将展开](whats-new-in-aspnet-mvc-4/_static/image41.png "再次按 Tab 键，代码片段将展开")

*再次按 Tab 键，代码片段将展开*

***使用鼠标添加代码片段（C#、VISUAL BASIC 和 XML）***

1. 右键单击要插入代码片段的位置。
2. 选择 "**插入**代码片段"，然后选择 **"我的代码片段"** 。
3. 通过单击从列表中选择相关的代码片段。

![右键单击要插入代码片段的位置，然后选择 "插入代码片段"](whats-new-in-aspnet-mvc-4/_static/image42.png "右键单击要插入代码片段的位置，然后选择 "插入代码片段"")

*右键单击要插入代码片段的位置，然后选择 "插入代码片段"*

![通过单击从列表中选择相关的代码片段](whats-new-in-aspnet-mvc-4/_static/image43.png "通过单击从列表中选择相关的代码片段")

*通过单击从列表中选择相关的代码片段*

<a id="AppendixB"></a>

<a id="Appendix_B_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-b-installing-visual-studio-express-2012-for-web"></a>附录 B：安装 Web Visual Studio Express 2012

您可以使用 **[Microsoft Web 平台安装程序](https://www.microsoft.com/web/downloads/platform.aspx)** 为 Web 或其他 &quot;Express&quot; 版本安装**Microsoft Visual Studio Express 2012** 。 以下说明将指导你完成使用*Microsoft Web 平台安装程序*安装*Visual studio Express 2012 for Web*的步骤。

1. 请参阅[[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169)。 或者，如果你已经安装了 Web 平台安装程序，则可以打开它并*使用 Windows AZURE SDK&quot;搜索 Visual Studio Express 2012 For Web*的产品 &quot;。
2. 单击 "**立即安装**"。 如果你没有**Web 平台安装程序**，则会重定向到 "下载并安装"。
3. **Web 平台安装程序**打开后，单击 "**安装**" 以启动安装程序。

    ![安装 Visual Studio Express](whats-new-in-aspnet-mvc-4/_static/image44.png "安装 Visual Studio Express")

    *安装 Visual Studio Express*
4. 阅读所有产品的许可证和条款，单击 "**我接受**" 以继续。

    ![接受许可条款](whats-new-in-aspnet-mvc-4/_static/image45.png)

    *接受许可条款*
5. 等待下载和安装过程完成。

    ![安装进度](whats-new-in-aspnet-mvc-4/_static/image46.png)

    *安装进度*
6. 安装完成后，单击 "**完成**"。

    ![安装完成](whats-new-in-aspnet-mvc-4/_static/image47.png)

    *安装完成*
7. 单击 "**退出**" 以关闭 Web 平台安装程序。
8. 若要打开 Web Visual Studio Express，请在 "**开始**" 屏幕上，开始书写 &quot;**VS Express**&quot;，然后单击 " **VS Express for Web** " 磁贴。

    ![VS Express for Web 磁贴](whats-new-in-aspnet-mvc-4/_static/image48.png)

    *VS Express for Web 磁贴*

<a id="AppendixC"></a>

<a id="Appendix_C_Installing_WebMatrix_2_and_iPhone_Simulator"></a>
## <a name="appendix-c-installing-webmatrix-2-and-iphone-simulator"></a>附录 C：安装 WebMatrix 2 和 iPhone 模拟器

若要在模拟的 iPhone 设备中运行站点，可以使用 WebMatrix 扩展 &quot;适用于 iPhone&quot;的电子移动模拟器。 此外，还可以配置相同的扩展，以便从 Visual Studio 2012 运行模拟器。

<a id="ApxCTask1"></a>

<a id="Task_1_-_Installing_WebMatrix_2"></a>
#### <a name="task-1---installing-webmatrix-2"></a>任务 1-安装 WebMatrix 2

1. 请参阅[[https://go.microsoft.com/?linkid=9809776](https://go.microsoft.com/?linkid=9809776)](https://go.microsoft.com/?linkid=9810169)。 或者，如果你已经安装了 Web 平台安装程序，则可以打开该安装程序并搜索产品 &quot;*WebMatrix 2*&quot;。
2. 单击 "**立即安装**"。 如果你没有**Web 平台安装程序**，则会重定向到 "下载并安装"。
3. **Web 平台安装程序**打开后，单击 "**安装**" 以启动安装程序。

    ![安装 WebMatrix 2](whats-new-in-aspnet-mvc-4/_static/image49.png "安装 WebMatrix 2")

    *安装 WebMatrix 2*
4. 阅读所有产品的许可证和条款，单击 "**我接受**" 以继续。

    ![接受许可条款](whats-new-in-aspnet-mvc-4/_static/image50.png "接受许可条款")

    *接受许可条款*
5. 等待下载和安装过程完成。

    ![安装进度](whats-new-in-aspnet-mvc-4/_static/image51.png "安装进度")

    *安装进度*
6. 安装完成后，单击 "**完成**"。

    ![安装完成](whats-new-in-aspnet-mvc-4/_static/image52.png "安装完成")

    *安装完成*
7. 单击 "**退出**" 以关闭 Web 平台安装程序。

<a id="ApxCTask2"></a>

<a id="Task_2_-_Installing_the_iPhone_Simulator_Extension"></a>
#### <a name="task-2---installing-the-iphone-simulator-extension"></a>任务 2-安装 iPhone 模拟器扩展

1. 运行**WebMatrix**并打开任何现有网站，或创建新网站。
2. 单击 "**主页**" 功能区中的 "**运行**" 按钮，然后选择 "**添加新**的"。

    ![正在添加新的 WebMatrix 扩展](whats-new-in-aspnet-mvc-4/_static/image53.png "正在添加新的 WebMatrix 扩展")

    *正在添加新的 WebMatrix 扩展*
3. 选择**IPhone 模拟器**，然后单击 "**安装**"。

    ![浏览 WebMatrix 扩展](whats-new-in-aspnet-mvc-4/_static/image54.png "浏览 WebMatrix 扩展")

    *浏览 WebMatrix 扩展*
4. 在 "包详细信息" 中，单击 "**安装**" 以继续安装扩展。

    ![iPhone 模拟器扩展](whats-new-in-aspnet-mvc-4/_static/image55.png "iPhone 模拟器扩展")

    *iPhone 模拟器扩展*
5. 阅读并接受该扩展 EULA。

    ![WebMatrix 扩展 EULA](whats-new-in-aspnet-mvc-4/_static/image56.png "WebMatrix 扩展 EULA")

    *WebMatrix 扩展 EULA*
6. 现在，你可以使用 iPhone 模拟器选项从 WebMatrix 运行你的网站。

    ![使用 iPhone 运行](whats-new-in-aspnet-mvc-4/_static/image57.png "使用 iPhone 运行")

    *使用 iPhone 运行*

<a id="ApxCTask3"></a>

<a id="Task_3_-_Configuring_Visual_Studio_2012_to_run_iPhone_Simulator"></a>
#### <a name="task-3---configuring-visual-studio-2012-to-run-iphone-simulator"></a>任务 3-配置 Visual Studio 2012 以运行 iPhone 模拟器

1. 打开**Visual Studio 2012**并打开任何网站或创建新的项目。
2. 单击 "运行" 按钮上的向下箭头，然后选择 "**浏览方式**"。

    ![浏览方式](whats-new-in-aspnet-mvc-4/_static/image58.png "浏览方式")

    *浏览方式*
3. 在 &quot;浏览&quot; "对话框中，单击"**添加**"。
4. 在 &quot;添加程序&quot; "对话框中，使用以下值：

   - **Program**： C:\Users\*{CurrentUser} * \AppData\Local\Microsoft\WebMatrix\Extensions\20\iPhoneSimulator\ElectricMobileSim\ElectricMobileSim.exe *（相应地更新路径）*
   - **参数**： &quot;1&quot;
   - **友好名称**： iPhone 模拟器

     ![添加程序](whats-new-in-aspnet-mvc-4/_static/image59.png "添加程序")

     *添加要浏览的程序*
5. 单击 **"确定"** 并关闭对话框。
6. 现在，你可以从 Visual Studio 2012 在 iPhone 模拟器中运行你的 Web 应用程序。

    ![通过 iPhone 模拟器进行浏览](whats-new-in-aspnet-mvc-4/_static/image60.png "通过 iPhone 模拟器进行浏览")

    *通过 iPhone 模拟器进行浏览*

<a id="AppendixD"></a>

<a id="Appendix_D_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
## <a name="appendix-d-publishing-an-aspnet-mvc-4-application-using-web-deploy"></a>附录 D：使用 Web 部署发布 ASP.NET MVC 4 应用程序

本附录将演示如何从 Windows Azure 管理门户创建新的网站，以及如何利用 Microsoft Azure 提供的 Web 部署发布功能，发布通过实验室获取的应用程序。

<a id="ApxDTask1"></a>

<a id="Task_1_-_Creating_a_New_Web_Site_from_the_Windows_Azure_Portal"></a>
#### <a name="task-1---creating-a-new-web-site-from-the-windows-azure-portal"></a>任务 1-从 Microsoft Azure 门户创建新网站

1. 请使用[Windows Azure 管理门户](https://manage.windowsazure.com/)，并使用与你的订阅关联的 Microsoft 凭据登录。

    > [!NOTE]
    > 借助 Windows Azure，你可以免费托管10个 ASP.NET 的网站，然后随着流量的增长进行扩展。 你可以在[此处](https://aka.ms/aspnet-hol-azure)注册。

    ![登录到 Windows Azure 门户](whats-new-in-aspnet-mvc-4/_static/image61.png "登录到 Windows Azure 门户")

    *登录到 Windows Azure 管理门户*
2. 单击命令栏上的 "**新建**"。

    ![创建新网站](whats-new-in-aspnet-mvc-4/_static/image62.png "创建新网站")

    *创建新网站*
3. 单击 "**计算** | **网站**"。 然后选择 "**快速创建**" 选项。 为新网站提供可用 URL，并单击 "**创建**网站"。

    > [!NOTE]
    > Windows Azure 网站是在云中运行的 Web 应用程序的宿主，你可以控制和管理这些应用程序。 使用 "快速创建" 选项，可以从门户外部将已完成的 web 应用程序部署到 Microsoft Azure 网站。 它不包括设置数据库的步骤。

    ![使用 "快速创建" 创建新网站](whats-new-in-aspnet-mvc-4/_static/image63.png "使用 "快速创建" 创建新网站")

    *使用 "快速创建" 创建新网站*
4. 请**等到新网站创建完毕。**
5. 创建网站后，单击 " **URL** " 列下的链接。 检查新网站是否正常工作。

    ![浏览到新网站](whats-new-in-aspnet-mvc-4/_static/image64.png "浏览到新网站")

    *浏览到新网站*

    ![网站正在运行](whats-new-in-aspnet-mvc-4/_static/image65.png "网站正在运行")

    *网站正在运行*
6. 返回到门户，并在 "**名称**" 列下单击网站的名称以显示管理页面。

    ![打开网站管理页](whats-new-in-aspnet-mvc-4/_static/image66.png "打开网站管理页")

    *打开网站管理页*
7. 在 "**仪表板**" 页的 "**速览**" 部分下，单击 "**下载发布配置文件**" 链接。

    > [!NOTE]
    > *发布配置文件*包含为每个已启用的发布方法将 web 应用程序发布到 microsoft Azure 网站所需的所有信息。 发布配置文件包含连接到每个终结点并对其进行身份验证所需的 Url、用户凭据和数据库字符串。 **Microsoft WebMatrix 2**、 **Microsoft Visual Studio Express for Web**和**Microsoft Visual Studio 2012**支持读取发布配置文件，以便自动配置这些程序以将 Web 应用程序发布到 microsoft Azure 网站。

    ![下载网站发布配置文件](whats-new-in-aspnet-mvc-4/_static/image67.png "下载网站发布配置文件")

    *下载网站发布配置文件*
8. 将发布配置文件下载到已知位置。 在本练习中，您将了解如何使用此文件从 Visual Studio 将 web 应用程序发布到 Microsoft Azure 网站。

    ![正在保存发布配置文件](whats-new-in-aspnet-mvc-4/_static/image68.png "正在保存发布配置文件")

    *正在保存发布配置文件*

<a id="ApxDTask2"></a>

<a id="Task_2_-_Configuring_the_Database_Server"></a>
#### <a name="task-2---configuring-the-database-server"></a>任务 2-配置数据库服务器

如果应用程序使用 SQL Server 数据库，则需要创建 SQL 数据库服务器。 如果要部署不使用 SQL Server 的简单应用程序，则可以跳过此任务。

1. 你将需要一个用于存储应用程序数据库的 SQL 数据库服务器。 可以在 Microsoft Azure 管理门户中的**sql** **数据库 | server** | **服务器的仪表板**上的 MICROSOFT Azure 管理门户中查看 sql 数据库服务器。 如果尚未创建服务器，可以使用命令栏上的 "**添加**" 按钮创建一个服务器。 记下**服务器名称和 URL、管理员登录名和密码**，因为你将在后续任务中使用它们。 请不要创建数据库，因为它将在后面的阶段创建。

    ![SQL 数据库服务器仪表板](whats-new-in-aspnet-mvc-4/_static/image69.png "SQL 数据库服务器仪表板")

    *SQL 数据库服务器仪表板*
2. 在下一任务中，您将从 Visual Studio 测试数据库连接，因此，需要在服务器的**允许 IP 地址**列表中包含本地 ip 地址。 为此，请单击 "**配置**"，从 "**当前客户端 IP 地址**" 中选择 IP 地址，并将其粘贴到 "**起始 Ip 地址**" 和 "**结束 ip 地址**" 文本框，然后单击 "![添加-客户端-IP 地址-](whats-new-in-aspnet-mvc-4/_static/image70.png)" 按钮。

    ![添加客户端 IP 地址](whats-new-in-aspnet-mvc-4/_static/image71.png)

    *添加客户端 IP 地址*
3. 将**客户端 Ip 地址**添加到 "允许的 IP 地址" 列表中后，单击 "**保存**" 以确认更改。

    ![确认更改](whats-new-in-aspnet-mvc-4/_static/image72.png)

    *确认更改*

<a id="ApxDTask3"></a>

<a id="Task_3_-_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
#### <a name="task-3---publishing-an-aspnet-mvc-4-application-using-web-deploy"></a>任务 3-使用 Web 部署发布 ASP.NET MVC 4 应用程序

1. 返回到 ASP.NET MVC 4 解决方案。 在**解决方案资源管理器**中，右键单击网站项目，然后选择 "**发布**"。

    ![发布应用程序](whats-new-in-aspnet-mvc-4/_static/image73.png "发布应用程序")

    *发布网站*
2. 导入您在第一个任务中保存的发布配置文件。

    ![导入发布配置文件](whats-new-in-aspnet-mvc-4/_static/image74.png "导入发布配置文件")

    *导入发布配置文件*
3. 单击 "**验证连接**"。 验证完成后，单击 "**下一步**"。

    > [!NOTE]
    > 验证完成后，"验证连接" 按钮旁边会出现一个绿色的复选标记。

    ![正在验证连接](whats-new-in-aspnet-mvc-4/_static/image75.png "正在验证连接")

    *正在验证连接*
4. 在 "**设置**" 页的 "**数据库**" 部分下，单击数据库连接的文本框旁边的按钮（即**DefaultConnection**）。

    ![Web 部署配置](whats-new-in-aspnet-mvc-4/_static/image76.png "Web 部署配置")

    *Web 部署配置*
5. 按如下所示配置数据库连接：

   - 在 "**服务器名称**" 中，键入您的 SQL 数据库服务器 URL，使用*tcp：* prefix。
   - 在 "**用户名**" 中键入服务器管理员登录名。
   - 在 "**密码**" 中键入服务器管理员登录密码。
   - 键入新的数据库名称，例如： *MVC4SampleDB*。

     ![正在配置目标连接字符串](whats-new-in-aspnet-mvc-4/_static/image77.png "正在配置目标连接字符串")

     *正在配置目标连接字符串*
6. 然后单击“确定”。 系统提示创建数据库时，单击 **"是"** 。

    ![创建数据库](whats-new-in-aspnet-mvc-4/_static/image78.png "创建数据库字符串")

    *创建数据库*
7. 将用于连接到 Windows Azure 中的 SQL 数据库的连接字符串显示在 "默认连接" 文本框中。 然后单击 **“下一步”** 。

    ![指向 SQL 数据库的连接字符串](whats-new-in-aspnet-mvc-4/_static/image79.png "指向 SQL 数据库的连接字符串")

    *指向 SQL 数据库的连接字符串*
8. 在 "**预览**" 页上，单击 "**发布**"。

    ![发布 web 应用程序](whats-new-in-aspnet-mvc-4/_static/image80.png "发布 web 应用程序")

    *发布 web 应用程序*
9. 发布过程完成后，您的默认浏览器将打开已发布的网站。

    ![发布到 Windows Azure 的应用程序](whats-new-in-aspnet-mvc-4/_static/image81.png "发布到 Windows Azure 的应用程序")

    *发布到 Windows Azure 的应用程序*
