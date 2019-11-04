---
uid: web-forms/overview/getting-started/creating-a-basic-web-forms-page
title: 使用 Visual Studio 2013 创建基本 ASP.NET 4.5 Web 窗体页
author: Erikre
description: ''
ms.author: riande
ms.date: 03/03/2014
ms.assetid: a2f1c635-0817-4a9a-8c13-d5b5d29727c0
msc.legacyurl: /web-forms/overview/getting-started/creating-a-basic-web-forms-page
msc.type: authoredcontent
ms.openlocfilehash: 5d13a51128eecd92a82cfd06054448582a348e11
ms.sourcegitcommit: 84b1681d4e6253e30468c8df8a09fe03beea9309
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/02/2019
ms.locfileid: "73445686"
---
# <a name="using-visual-studio-2013-to-create-a-basic-aspnet-45-web-forms-page"></a>使用 Visual Studio 2013 创建基本 ASP.NET 4.5 Web 窗体页

作者： [Erik Reitan](https://github.com/Erikre)

[!INCLUDE[](~/includes/rp.md)]

本演练介绍了[Microsoft Visual Studio 2013](https://www.microsoft.com/visualstudio/11/downloads#vs)和[Microsoft Visual Studio Express 2013 for Web](https://www.microsoft.com/visualstudio/11/downloads#express-web)中的 web 开发环境。 本演练将指导您创建一个简单的 ASP.NET Web 窗体页，并说明创建新页、添加控件和编写代码的基本方法。

本演练涉及以下任务：

- 创建文件系统 Web 窗体应用程序项目。
- 通过 Visual Studio 熟悉自己的体验。
- 创建 ASP.NET 页。
- 添加控件。
- 添加事件处理程序。
- 运行和测试 Visual Studio 中的页面。

## <a name="prerequisites"></a>Prerequisites

若要完成本演练，你将需要：

- [Microsoft Visual Studio 2013](https://www.microsoft.com/visualstudio/11/downloads#vs)或[Microsoft Visual Studio Express 2013 for Web](https://www.microsoft.com/visualstudio/11/downloads#express-web)。 将自动安装 .NET Framework。 

    > [!NOTE] 
    > 
    > 在本系列教程中，Web 的 Microsoft Visual Studio 2013 和 Microsoft Visual Studio Express 2013 通常称为 Visual Studio。  
    >   
    > 如果你使用的是 Visual Studio，则本演练假定你在首次启动 Visual Studio 时选择了 " **Web 开发**" 设置集合。 有关详细信息，请参阅[如何：选择 Web 开发环境设置](https://msdn.microsoft.com/library/ff521558.aspx)。

## <a name="creating-a-web-application-project-and-a-page"></a>创建 Web 应用程序项目和页面

<a id="sectionToggle0"></a>

在本演练的此部分中，你将创建一个 Web 应用程序项目并向其添加新页。 你还将在浏览器中添加 HTML 文本并运行该页面。

### <a name="to-create-a-web-application-project"></a>创建 Web 应用程序项目

1. 打开 Microsoft Visual Studio。
2. 在“文件”菜单上，选择“新建项目”。  
    ![文件 "菜单](creating-a-basic-web-forms-page/_static/image1.png)

    此时将出现“新建项目”对话框。
3. 选择左侧的 "**模板**" -&gt; **Visual C#**  -&gt; **Web**模板 "组。
4. 在中心列中选择 " **ASP.NET Web 应用程序**" 模板。
5. 将项目命名为 " ***BasicWebApp*** "，然后单击 **"确定"** 按钮。   
!["新建项目" 对话框](creating-a-basic-web-forms-page/_static/image2.png)
6. 接下来，选择 " **Web 窗体**" 模板，然后单击 "**确定"** 按钮创建项目。  
![新的 ASP.NET 项目 "对话框](creating-a-basic-web-forms-page/_static/image3.png)  

    Visual Studio 会创建一个新项目，其中包含基于 Web 窗体模板的预生成功能。 它不但提供了一个*主页 .aspx*页面（一个*关于 .aspx*页面），还*提供了成员*资格功能，可注册用户并保存其凭据，使用户能够登录到你的网站。 创建新页面时，默认情况下，Visual Studio 会在 "**源**" 视图中显示该页面，您可以在其中查看该页面的 HTML 元素。 下图显示了在创建名为*BasicWebApp*的新网页的情况下，你将在 "**源**" 视图中看到的内容。  
    ![源视图](creating-a-basic-web-forms-page/_static/image4.png)

### <a name="a-tour-of-the-visual-studio-web-development-environment"></a>Visual Studio Web 开发环境教程

在继续修改页面之前，请先熟悉 Visual Studio 开发环境，这一点非常有用。 下图显示了 Visual Studio 中可用的 windows 和工具以及 Web Visual Studio Express。

> [!NOTE] 
> 
> 此关系图显示默认窗口和窗口位置。 "**视图**" 菜单允许您显示其他窗口，并重新排列窗口并调整其大小以适合您的喜好。 如果已对窗口排列进行了更改，则所显示的内容将与图中的内容不匹配。

 Visual Studio 环境

![Visual Studio 环境](creating-a-basic-web-forms-page/_static/image5.png)

### <a name="familiarize-yourself-with-the-web-designer"></a>熟悉 Web 设计器

检查上图并将文本与以下列表匹配，其中介绍了最常用的窗口和工具。 （并非所有你所看到的窗口和工具都列在此处，只列出了上图中标记的那些窗口和工具。）

- '. 提供用于设置文本格式、查找文本等的命令。 某些工具栏仅在 "**设计**" 视图中工作时可用。
- **解决方案资源管理器**"窗口。 显示您的 Web 应用程序中的文件和文件夹。
- 文档窗口。 在选项卡式窗口中显示正在处理的文档。 可以通过单击 "选项卡" 在文档之间进行切换。
- **属性**窗口。 允许您更改页面、HTML 元素、控件和其他对象的设置。
- 视图选项卡。 提供同一文档的不同视图。 **设计**视图是接近 WYSIWYG 的编辑图面。 **源**视图是页面的 HTML 编辑器。 **拆分**视图显示文档的**设计**视图和**源**视图。 稍后将在本演练中使用 "**设计**" 和 "**源**" 视图。 如果希望在 "**设计**" 视图中打开网页，请在 "**工具**" 菜单上单击 "**选项**"，选择 " **HTML 设计器**" 节点，然后更改中的 "**起始页**" 选项。
- **工具箱**。 提供可拖到页面上的控件和 HTML 元素。 **工具箱**元素按 common 函数分组。
- S **E) 资源管理器**。 显示数据库连接。 如果服务器资源管理器不可见，请在 "视图" 菜单上单击 "服务器资源管理器"。

### <a name="creating-a-new-aspnet-web-forms-page"></a>创建新的 ASP.NET Web 窗体页

使用 " **ASP.NET Web 应用程序**" 项目模板创建新的 Web 窗体应用程序时，Visual Studio 会添加一个名为 " *default.aspx*" 的 ASP.NET 页面（Web 窗体页）以及多个其他文件和文件夹。 你可以使用*default.aspx*页作为你的 Web 应用程序的主页。 但是，对于本演练，您将创建并使用一个新页。

### <a name="to-add-a-page-to-the-web-application"></a>向 Web 应用程序添加页

1. 关闭 " *default.aspx* " 页。 为此，请单击显示文件名的选项卡，然后单击 "关闭" 选项。
2. 在**解决方案资源管理器**中，右键单击 Web 应用程序名称（在本教程中，应用程序名称为 " **BasicWebSite**"），然后单击 "**添加** -&gt;**新项**"。   
随即出现“添加新项”对话框。
3. 选择左侧的 " **Visual C#**  -&gt; **Web**模板" 组。 然后，从中间列表中选择 " **Web 窗体**" 并将其命名为 " *FirstWebPage*"。   
    !["添加新项" 对话框](creating-a-basic-web-forms-page/_static/image6.png)
4. 单击 "**添加**" 以将网页添加到项目。  
Visual Studio 将创建新页并将其打开。

### <a name="adding-html-to-the-page"></a>将 HTML 添加到页面

在本演练的此部分中，将向页面添加一些静态文本。

### <a name="to-add-text-to-the-page"></a>向页面中添加文本

1. 在文档窗口的底部，单击 "**设计**" 选项卡以切换到 "**设计**" 视图。

    设计视图以类似于所见即所得的方式显示当前页面。 此时，您不能在页面上包含任何文本或控件，因此，除了用一条轮廓矩形的虚线外，该页面仍为空白。 此矩形表示页面上的**div**元素。
2. 在用虚线勾勒出的矩形内部单击。
3. 键入 "**欢迎使用 Visual Web Developer** "，然后按**enter**两次。

    下图显示了在 "**设计**" 视图中键入的文本。

    ![设计视图中的欢迎文本](creating-a-basic-web-forms-page/_static/image7.png "设计视图中的欢迎文本")
4. 切换到 "**源**" 视图。

    您可以在 "**设计**" 视图中键入时在 "**源**" 视图中查看 HTML。  
    ![包含静态文本](creating-a-basic-web-forms-page/_static/image8.png) 的网页

### <a name="running-the-page"></a>运行页面

在继续操作之前，可以先将控件添加到页面。

### <a name="to-run-the-page"></a>运行页面

1. 在**解决方案资源管理器**中，右键单击*FirstWebPage* ，然后选择 "**设为起始页**"。
2. 按**CTRL + F5**运行页面。

    页面将显示在浏览器中。 尽管您创建的页的文件扩展名为 *.aspx*，但它当前与任何 HTML 页面一样运行。

    若要在浏览器中显示页面，还可以在**解决方案资源管理器**中右键单击页面，然后选择 "**在浏览器中查看**"。
3. 关闭浏览器以停止 Web 应用程序。

## <a name="adding-and-programming-controls"></a>添加和编程控件

<a id="sectionToggle1"></a>

现在，你将向页面中添加服务器控件。 服务器控件（例如按钮、标签、文本框和其他熟悉控件）为 Web 窗体页提供典型的窗体处理功能。 但是，您可以用服务器上运行的代码而不是客户端对控件进行编程。

您将向页面添加一个[按钮](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx)控件、一个[文本框](https://msdn.microsoft.com/library/system.web.ui.webcontrols.textbox.aspx)控件和一个 "[标签](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx)" 控件，并编写代码来处理[Button](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx)控件的[Click](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.click.aspx)事件。

### <a name="to-add-controls-to-the-page"></a>向页面添加控件

1. 单击 "**设计**" 选项卡以切换到 "**设计**" 视图。
2. 将插入点放在**欢迎使用 Visual Web Developer**文本的末尾，然后按**enter** 5 次或多次，以在**div**元素框中腾出一些空间。
3. 在 "**工具箱**" 中，展开**标准**组（如果尚未展开）。  
请注意，您可能需要展开左侧的 **"工具箱**" 窗口以查看它。
4. 将[TextBox](https://msdn.microsoft.com/library/system.web.ui.webcontrols.textbox.aspx)控件拖到页面上，并将其放置在**欢迎使用**第一行中的 " **div**元素" 框的中部。
5. 将一个 "[按钮](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx)" 控件拖到页面上，然后将其放置在[TextBox](https://msdn.microsoft.com/library/system.web.ui.webcontrols.textbox.aspx)控件的右侧。
6. 将 "[标签](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx)" 控件拖动到页面上，将其放在[按钮](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx)控件下的单独行中。
7. 将插入点置于[TextBox](https://msdn.microsoft.com/library/system.web.ui.webcontrols.textbox.aspx)控件的上方，然后键入 "**输入您的姓名：** "。

    此静态 HTML 文本是[TextBox](https://msdn.microsoft.com/library/system.web.ui.webcontrols.textbox.aspx)控件的标题。 您可以在同一页上混合使用静态 HTML 和服务器控件。 下图显示了在 "**设计**" 视图中显示三个控件的方式。

    ![设计视图中的三个控件](creating-a-basic-web-forms-page/_static/image9.png "设计视图中的三个控件")

### <a name="setting-control-properties"></a>设置控件属性

Visual Studio 提供了各种方法来设置页面上控件的属性。 在本演练的此部分，您将在 "**设计**" 视图和 "**源**" 视图中设置属性。

### <a name="to-set-control-properties"></a>设置控件属性

1. 首先，通过在 "**视图**" 菜单中选择 "&gt;**其他 windows** -&gt;"**属性 "窗口**来显示"**属性**"窗口。 还可以选择**F4**以显示 "**属性**" 窗口。
2. 选择 " [Button](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx) " 控件，然后在 "**属性**" 窗口中，将 "**文本**" 的值设置为 "**显示名称**"。 您输入的文本将出现在设计器中的按钮上，如下图所示。

    ![设置按钮文本](creating-a-basic-web-forms-page/_static/image10.png "设置按钮文本")
3. 切换到 "**源**" 视图。

    "**源**" 视图显示页面的 HTML，其中包括 Visual Studio 为服务器控件创建的元素。 控件使用类似于 HTML 的语法进行声明，只不过标记使用前缀**asp：** 并包括属性**runat =&quot;server&quot;** 。

    控件属性被声明为属性。 例如，在步骤1中设置[按钮](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx)控件的 " [text](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.text.aspx) " 属性时，实际上是在控件的标记中设置**文本**特性。

    > [!NOTE] 
    > 
    > 所有控件都在**form**元素内，该元素还具有特性**runat =&quot;server&quot;** 。 **Runat =&quot;server&quot;** 属性和**asp：** control 标记的前缀标记这些控件，以便在页面运行时由服务器上的 ASP.NET 进行处理。 位于 **&lt;窗体 runat =&quot;server&quot;&gt;** 和 **&lt;script runat =&quot;server&quot;** &gt;元素的代码不会以任何形式发送到浏览器，这就是 ASP.NET 代码必须位于元素内的原因其开始标记包含**runat =&quot;server&quot;** 属性。
4. 接下来，您将向 "[标签](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx)" 控件添加其他属性。 将插入点直接置于 **&lt;asp： label&gt;** **标记中，** 然后按**空格键**。

    此时将显示一个下拉列表，其中显示可以为 "[标签](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx)" 控件设置的可用属性列表。 此功能称为**IntelliSense**，可帮助你在**源**视图中包含服务器控件、HTML 元素和页面上其他项的语法。 下图显示了 "[标签](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx)" 控件的**IntelliSense**下拉列表。

    ![IntelliSense 特性](creating-a-basic-web-forms-page/_static/image11.png "IntelliSense 特性")
5. 选择 "**前景色**"，然后键入一个等号。

    IntelliSense 显示颜色列表。

    > [!NOTE] 
    > 
    > 查看代码时，可随时按**CTRL + J**显示**IntelliSense**下拉列表。
6. 为 " **[标签](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx)** " 控件的文本选择颜色。 请确保选择一个足够深色的颜色，使其能够阅读白色背景。

    用您选择的颜色（包括右引号）完成**前景色**属性。

### <a name="programming-the-button-control"></a>对按钮控件进行编程

对于本演练，您将编写代码来读取用户在文本框中输入的名称，然后在 "[标签](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx)" 控件中显示该名称。

### <a name="add-a-default-button-event-handler"></a>添加默认按钮事件处理程序

1. 切换到 "**设计**" 视图。
2. 双击[按钮](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx)控件。

    默认情况下，Visual Studio 会切换到代码隐藏文件，并为[按钮](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx)控件的默认事件（即[单击](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.click.aspx)事件）创建主干事件处理程序。 代码隐藏文件将 UI 标记（如 HTML）从服务器代码（如C#）中分离出来。   
   光标定位到为此事件处理程序添加的代码。

    > [!NOTE] 
    > 
    > 在 "**设计**" 视图中双击控件只是创建事件处理程序的几种方法之一。
3. 在**Button1 内\_单击**"事件处理程序"，键入**Label1** ，后跟一个句点（ **.** ）。

    在标签（**Label1**）的**ID**后面键入句点时，Visual Studio 将显示 "[标签](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx)" 控件的可用成员列表，如下图所示。 成员通常是属性、方法或事件。

    ![代码视图中的 IntelliSense](creating-a-basic-web-forms-page/_static/image12.png "代码视图中的 IntelliSense")
4. 完成按钮的**单击**事件处理程序，使其读取，如下面的代码示例中所示。

    [!code-csharp[Main](creating-a-basic-web-forms-page/samples/sample1.cs?highlight=3)]

    [!code-vb[Main](creating-a-basic-web-forms-page/samples/sample2.vb?highlight=2)]
5. 在**解决方案资源管理器**中右键单击 " *FirstWebPage* "，然后选择 "**查看标记**"，切换回查看 HTML 标记的**源**视图。
6. 滚动到 **&lt;asp：按钮&gt;** 元素。 请注意， **&lt;asp： Button&gt;** 元素现在具有属性**Onclick =&quot;Button1\_单击 "&quot;** "。

    此属性将按钮的[Click](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.click.aspx)事件绑定到你在上一步中编码的处理程序方法。

    事件处理程序方法可以具有任何名称;你看到的名称是 Visual Studio 创建的默认名称。 重要的是，用于 HTML 中的**OnClick**特性的名称必须与代码隐藏中定义的方法的名称匹配。

### <a name="running-the-page"></a>运行页面

现在可以测试页上的服务器控件。

### <a name="to-run-the-page"></a>运行页面

1. 按**CTRL + F5**在浏览器中运行页。 如果发生错误，请重新检查以上步骤。
2. 在文本框中输入一个名称，然后单击 "**显示名称**" 按钮。

    您输入的名称将显示在 "[标签](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx)" 控件中。 请注意，单击该按钮时，该页将发送到 Web 服务器。 然后，ASP.NET 重新创建页面，运行你的代码（在这种情况下，[按钮](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx)控件的[Click](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.click.aspx)事件处理程序会运行），然后将新页发送到浏览器。 如果在浏览器中监视状态栏，则每次单击按钮时，都可以看到该页正在往返 Web 服务器。
3. 在浏览器中，右键单击该页并选择 "**查看源**"，查看正在运行的页面的源。

    在页源代码中，你将看到没有任何服务器代码的 HTML。 具体而言，你看不到 **&lt;asp：** 在**源**视图中使用的&gt;元素。 当页面运行时，ASP.NET 将处理服务器控件，并将 HTML 元素呈现给执行表示控件的函数的页面。 例如， **&lt;asp： Button&gt;** 控件呈现为 HTML **&lt;输入类型 =&quot;提交&quot;&gt;** 元素。
4. 关闭浏览器。

## <a name="working-with-additional-controls"></a>使用其他控件

<a id="sectionToggle2"></a>

在本演练的此部分，您将使用[Calendar](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx)控件，该控件每次显示一个月的日期。 [Calendar](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx)控件比你使用的 "按钮"、"文本框" 和 "标签" 更复杂，并说明了服务器控件的一些其他功能。

在本部分中，你将向页面中添加[WebControls](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx)控件并设置其格式。

### <a name="to-add-a-calendar-control"></a>添加日历控件

1. 在 Visual Studio 中，切换到 "**设计**" 视图。
2. 从 "**工具箱**" 的 "**标准**" 部分，将 "[日历](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx)" 控件拖动到页面上，并将其放置在包含其他控件的**div**元素下。

    将显示日历的智能标记面板。 该面板会显示命令，使您可以轻松地为所选控件执行最常见的任务。 下图显示了在 "**设计**" 视图中呈现的[日历](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx)控件。

    ![设计视图中的日历控件](creating-a-basic-web-forms-page/_static/image13.png "设计视图中的 Calendar 控件")
3. 在智能标记面板中，选择 "**自动套用格式**"。

    此时将显示 "**自动套用格式**" 对话框，使用该对话框可以选择日历的格式设置方案。 下图显示了[日历](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx)控件的 "**自动套用格式**" 对话框。

    !["自动套用格式" 对话框（日历控件）](creating-a-basic-web-forms-page/_static/image14.png "“自动套用格式”对话框（Calendar 控件）")
4. 从 "**选择方案**" 列表中，选择 "**简单**"，然后单击 **"确定"** 。
5. 切换到 "**源**" 视图。

    你可以查看 **&lt;asp： Calendar&gt;** 元素。 此元素比之前创建的简单控件的元素长很多。 它还包括子元素，如 **&lt;WeekEndDayStyle&gt;** ，它表示各种格式设置。 下图显示了 "**源**" 视图中的[日历](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx)控件。 （您在 "**源**" 视图中看到的确切标记可能与插图略有不同。）

    ![源视图中的日历控件](creating-a-basic-web-forms-page/_static/image15.png "源视图中的 Calendar 控件")

### <a name="programming-the-calendar-control"></a>设计 Calendar 控件

在本部分中，您将计划 "[日历](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx)" 控件以显示当前选定的日期。

### <a name="to-program-the-calendar-control"></a>对日历控件进行编程

1. 在 "**设计**" 视图中，双击 "[日历](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx)" 控件。

    将创建新的事件处理程序，并将其显示在名为*FirstWebPage.aspx.cs*的代码隐藏文件中。
2. 用下面的代码完成[SelectionChanged](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.selectionchanged.aspx)事件处理程序。

    [!code-csharp[Main](creating-a-basic-web-forms-page/samples/sample3.cs?highlight=3)]

    [!code-vb[Main](creating-a-basic-web-forms-page/samples/sample4.vb?highlight=2)]

    上面的代码将 "标签" 控件的文本设置为 calendar 控件的所选日期。

### <a name="running-the-page"></a>运行页面

现在可以测试日历。

### <a name="to-run-the-page"></a>运行页面

1. 按**CTRL + F5**在浏览器中运行页。
2. 单击日历中的日期。

    您单击的日期将显示在 "[标签](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx)" 控件中。
3. 在浏览器中，查看页面的源代码。

    请注意， [Calendar](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx)控件已以**表**的形式呈现到页面，每一天都作为**td**元素。
4. 关闭浏览器。

## <a name="next-steps"></a>后续步骤

<a id="nextStepsToggle"></a>

本演练演示了 Visual Studio 页面设计器的基本功能。 现在，你已了解如何在 Visual Studio 中创建和编辑 Web 窗体页面，你可能需要浏览其他功能。 例如，你可能需要执行以下操作：

- 按照[使用 ASP.NET 4.5 Web 窗体和 Visual Studio 2013 入门](getting-started-with-aspnet-45-web-forms/introduction-and-overview.md)分步教程系列来了解有关 ASP.NET Web 窗体的详细信息。
- 详细了解级联样式表（CSS）。 有关详细信息，请参阅[使用 CSS 概述](https://msdn.microsoft.com/library/bb398931.aspx)。
