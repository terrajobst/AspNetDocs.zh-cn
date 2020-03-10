---
uid: web-forms/overview/getting-started/code-editing-in-web-forms-pages
title: 在 Visual Studio 2013 中编辑 ASP.NET Web 窗体的代码 |Microsoft Docs
author: Erikre
description: ''
ms.author: riande
ms.date: 03/03/2014
ms.assetid: 5344b74e-b888-479a-92bc-601a33bd61a2
msc.legacyurl: /web-forms/overview/getting-started/code-editing-in-web-forms-pages
msc.type: authoredcontent
ms.openlocfilehash: 3473ad476fbbebc58e12586334b4600f57cf17ed
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78513638"
---
# <a name="code-editing-aspnet-web-forms-in-visual-studio-2013"></a>在 Visual Studio 2013 中编辑 ASP.NET Web 窗体的代码

作者： [Erik Reitan](https://github.com/Erikre)

在许多 ASP.NET Web 窗体页面中，你可以 Visual Basic、 C#或其他语言编写代码。 Visual Studio 中的代码编辑器可以帮助你快速编写代码，同时可帮助避免错误。 此外，该编辑器还提供了创建可重用代码的方法，以帮助减少需要执行的工作量。

此演练演示了 Visual Studio 代码编辑器的各种功能。

在本演练中，你将学会如何执行以下任务：

- 更正内联编码错误。
- 重构和重命名代码。
- 重命名变量和对象。
- 插入代码片段。

## <a name="prerequisites"></a>系统必备

若要完成本演练，你将需要：

- [Microsoft Visual Studio 2013](https://www.microsoft.com/visualstudio/11/downloads#vs)或[Microsoft Visual Studio Express 2013 for Web](https://www.microsoft.com/visualstudio/11/downloads#express-web)。 将自动安装 .NET Framework。 

    > [!NOTE] 
    > 
    > 在本系列教程中，Web 的 Microsoft Visual Studio 2013 和 Microsoft Visual Studio Express 2013 通常称为 Visual Studio。  
    >   
    > 如果你使用的是 Visual Studio，则本演练假定你在首次启动 Visual Studio 时选择了 " **Web 开发**" 设置集合。 有关详细信息，请参阅[如何：选择 Web 开发环境设置](https://msdn.microsoft.com/library/ff521558.aspx)。

## <a name="creating-a-web-application-project-and-a-page"></a>创建 Web 应用程序项目和页面

<a id="sectionToggle0"></a>

在本演练的此部分中，你将创建一个 Web 应用程序项目并向其添加新页。

### <a name="to-create-a-web-application-project"></a>创建 Web 应用程序项目

1. 打开 Microsoft Visual Studio。
2. 在“文件”菜单上，选择“新建项目”。  
    ![文件 "菜单](code-editing-in-web-forms-pages/_static/image1.png)

    此时将出现“新建项目”对话框。
3. 选择左侧的 "**模板**" -&gt; **Visual C#**  -&gt; **Web**模板 "组。
4. 在中心列中选择 " **ASP.NET Web 应用程序**" 模板。
5. 将项目命名为 " ***BasicWebApp*** "，然后单击 **"确定"** 按钮。   
![“新建项目”对话框](code-editing-in-web-forms-pages/_static/image2.png)
6. 接下来，选择 " **Web 窗体**" 模板，然后单击 "**确定"** 按钮创建项目。  
![新的 ASP.NET 项目 "对话框](code-editing-in-web-forms-pages/_static/image3.png)  

    Visual Studio 会创建一个新项目，其中包含基于 Web 窗体模板的预生成功能。

## <a name="creating-a-new-aspnet-web-forms-page"></a>创建新的 ASP.NET Web 窗体页

使用 " **ASP.NET Web 应用程序**" 项目模板创建新的 Web 窗体应用程序时，Visual Studio 会添加一个名为 " *default.aspx*" 的 ASP.NET 页面（Web 窗体页）以及多个其他文件和文件夹。 你可以使用*default.aspx*页作为你的 Web 应用程序的主页。 但是，对于本演练，您将创建并使用一个新页。

### <a name="to-add-a-page-to-the-web-application"></a>向 Web 应用程序添加页

1. 在**解决方案资源管理器**中，右键单击 Web 应用程序名称（在本教程中，应用程序名称为 " **BasicWebSite**"），然后单击 "**添加** -&gt;**新项**"。   
随即出现“添加新项”对话框。
2. 选择左侧的 " **Visual C#**  -&gt; **Web**模板" 组。 然后，从中间列表中选择 " **Web 窗体**" 并将其命名为 " *FirstWebPage*"。   
    ![“添加新项”对话框](code-editing-in-web-forms-pages/_static/image4.png)
3. 单击 "**添加**"，将 Web 窗体页添加到您的项目中。  
 Visual Studio 将创建新页并将其打开。
4. 接下来，将此新页设置为默认启动页。 在**解决方案资源管理器**中，右键单击名为*FirstWebPage*的新页面，然后选择 "**设为起始页**"。 下次运行此应用程序来测试进度时，会自动在浏览器中看到此新页。

## <a name="correcting-inline-coding-errors"></a>更正内联编码错误

Visual Studio 中的代码编辑器可帮助你在编写代码时避免错误，如果你发生了错误，代码编辑器将有助于更正此错误。 在本演练的此部分，您将编写一行代码，用于说明编辑器中的错误更正功能。

### <a name="to-correct-simple-coding-errors-in-visual-studio"></a>更正 Visual Studio 中的简单编码错误

1. 在 "**设计**" 视图中，双击空白页为该页的**Load**事件创建处理程序。   
   只能将事件处理程序用作编写某些代码的位置。
2. 在处理程序中，键入以下包含错误的行，然后按**enter**：

    [!code-csharp[Main](code-editing-in-web-forms-pages/samples/sample1.cs)]

   按下**enter**后，代码编辑器会将绿色和红色下划线（&quot;通常&quot; 行）置于出现问题的代码区域下。 绿色下划线表示警告。 红色下划线指示必须修复的错误。 

    将鼠标指针停留在 `myStr` 上可查看工具提示，告诉你有关警告。 同时，将鼠标指针停留在红色下划线上以查看错误消息。

    下图显示带下划线的代码。

    ![设计视图中的欢迎文本](code-editing-in-web-forms-pages/_static/image5.png "设计视图中的欢迎文本")  
   必须通过在行的末尾添加一个分号 `;` 来修复该错误。 警告只会通知你尚未使用 `myStr` 变量。  

    > [!NOTE] 
    > 
    > 在 Visual Studio 中查看当前代码格式设置，方法是选择 "**工具**" -&gt;**选项**" -&gt;**字体和颜色**"。

## <a name="refactoring-and-renaming"></a>重构和重命名

重构是一种软件方法，涉及重构你的代码，使其更易于理解和维护，同时保留其功能。 一个简单的示例是在事件处理程序中编写代码以从数据库中获取数据。 开发页面时，会发现需要从多个不同的处理程序访问数据。 因此，通过在页中创建数据访问方法并在处理程序中插入对方法的调用，可以重构该页的代码。

代码编辑器包含可帮助您执行各种重构任务的工具。 在本演练中，您将使用两种重构技术：重命名变量和提取方法。 其他重构选项包括封装字段、将局部变量升级到方法参数和管理方法参数。 这些重构选项的可用性取决于代码中的位置。

### <a name="refactoring-code"></a>重构代码

常见的重构方案是从位于另一个成员内的代码（如方法）中创建（提取）一个方法。 这会减少原始成员的大小，并使提取的代码可重复使用。

在本演练的此部分中，你将编写一些简单的代码，然后从中提取方法。 支持重构C#，因此你将创建一个使用C#作为其编程语言的页面。

### <a name="to-extract-a-method-in-a-c-page"></a>在C#页中提取方法

1. 切换到 "**设计**" 视图。
2. 在 "**工具箱**" 的 "**标准**" 选项卡上，将 "[按钮](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx)" 控件拖到页面上。
3. 双击**按钮**控件为其[单击](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.click.aspx)事件创建处理程序，然后添加以下突出显示的代码：

    [!code-csharp[Main](code-editing-in-web-forms-pages/samples/sample2.cs?highlight=3-16)]

   此代码创建一个**ArrayList**对象，使用一个循环将其加载到值，然后使用另一个循环来显示**ArrayList**对象的内容。
4. 按 " **CTRL + F5** " 运行该页面，然后单击 ""**按钮**以确保看到以下输出：   

    [!code-html[Main](code-editing-in-web-forms-pages/samples/sample3.html)]
5. 返回到代码编辑器，然后在事件处理程序中选择以下行。   

    [!code-html[Main](code-editing-in-web-forms-pages/samples/sample4.html)]
6. 右键单击所选内容，单击 "**重构**"，然后选择 "**提取方法**"。 

    此时将显示 "**提取方法**" 对话框。
7. 在 "**新方法名称**" 框中，键入**DisplayArray**，然后单击 **"确定"** 。 

    代码编辑器会创建一个名为 `DisplayArray`的新方法，并在该循环最初所在的**Click**处理程序中调用新方法。

    [!code-csharp[Main](code-editing-in-web-forms-pages/samples/sample5.cs?highlight=12)]
8. 按**CTRL + F5**再次运行该页，并单击**按钮**。

    页面的功能与以前相同。 现在，`DisplayArray` 方法可以从 page 类中的任意位置调用。

## <a name="renaming-variables"></a>重命名变量

使用变量和对象时，你可能希望在代码中引用它们后重命名它们。 但是，如果未重命名其中一个引用，重命名变量和对象会导致代码中断。 因此，您可以使用重构来执行重命名。

### <a name="to-use-refactoring-to-rename-a-variable"></a>使用重构重命名变量

1. 在**Click**事件处理程序中，找到以下行：

    [!code-csharp[Main](code-editing-in-web-forms-pages/samples/sample6.cs)]
2. 右键单击变量名称 `alist`，选择 "**重构**"，然后选择 "**重命名**"。

    此时将显示 "**重命名**" 对话框。
3. 在 "**新名称**" 框中，键入**ArrayList1** ，并确保已选中 "**预览引用更改**" 复选框。 然后单击 **“确定”** 。

    此时将显示 "**预览更改**" 对话框，并显示一个树，其中包含对您要重命名的变量的所有引用。
4. 单击 "**应用**" 以关闭 "**预览更改**" 对话框。

    专门引用所选实例的变量将被重命名。 但请注意，以下行中 `alist` 的变量不会重命名。

    [!code-csharp[Main](code-editing-in-web-forms-pages/samples/sample7.cs)]

    此行中的变量 `alist` 不会重命名，因为它与重命名的变量 `alist` 不表示相同的值。 `DisplayArray` 声明中的变量 `alist` 是该方法的局部变量。 这说明，使用重构对变量进行重命名不同于只在编辑器中执行查找和替换操作;重构会对变量进行重命名，并了解它正在使用的变量的语义。

## <a name="inserting-snippets"></a>插入代码段

由于 Web 窗体开发人员经常需要执行很多编码任务，因此代码编辑器提供了一个代码段库或预编写代码的块。 可以将这些代码段插入到页面中。

在 Visual Studio 中使用的每种语言都与插入代码片段的方式略有不同。 有关插入代码片段的信息，请参阅[Visual Basic IntelliSense 代码片段](https://msdn.microsoft.com/library/18yz4be4.aspx)。 有关在视觉对象C#中插入代码片段的信息，请参阅[visual C# Code 片段](https://msdn.microsoft.com/library/z41h7fat.aspx)。

## <a name="next-steps"></a>后续步骤

本演练演示了 Visual Studio 2010 代码编辑器的基本功能，用于更正代码中的错误、重构代码、重命名变量以及将代码段插入到代码中。 编辑器中的其他功能可以快速轻松地进行应用程序开发。 例如，你可能希望：

- 了解有关 IntelliSense 功能的详细信息，例如修改 IntelliSense 选项、管理代码片段和联机搜索代码片段。 有关详细信息，请参阅[使用 IntelliSense](https://msdn.microsoft.com/library/hcw1s69b.aspx)。
- 了解如何创建您自己的代码片段。 有关详细信息，请参阅[创建和使用 IntelliSense 代码片段](https://msdn.microsoft.com/library/ms165392.aspx)
- 了解有关 IntelliSense 代码片段的特定于 Visual Basic 的功能的详细信息，例如自定义代码段和故障排除。 有关详细信息，请参阅[Visual Basic IntelliSense 代码片段](https://msdn.microsoft.com/library/18yz4be4.aspx)
- 详细C#了解 IntelliSense 的特定功能，例如重构和代码片段。 有关详细信息，请[参阅C# Visual IntelliSense](https://msdn.microsoft.com/library/43f44291.aspx)。
