---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/ui_and_navigation
title: UI 和导航 |Microsoft Docs
author: Erikre
description: 本系列教程将介绍使用 ASP.NET 4.5 构建 ASP.NET Web 窗体应用程序的基础知识，并为我们 Microsoft Visual Studio Express 2013 。
ms.author: riande
ms.date: 09/08/2014
ms.assetid: 5c76891d-e515-4885-b576-76bd2c494efe
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/ui_and_navigation
msc.type: authoredcontent
ms.openlocfilehash: ac1dcaf1ba911fdcaeb3845c6836ec771733d93e
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78522902"
---
# <a name="ui-and-navigation"></a>UI 和导航

作者： [Erik Reitan](https://github.com/Erikre)

[下载 Wingtip 玩具示例项目（C#）](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409)或[下载电子书（PDF）](https://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)

> 本系列教程将介绍使用 ASP.NET 4.5 构建 ASP.NET Web 窗体应用程序的基础知识，并为 Web Microsoft Visual Studio Express 2013。 此教程系列附带有[ C#源代码](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409)的 Visual Studio 2013 项目。

在本教程中，你将修改默认 Web 应用程序的 UI，以支持 Wingtip 玩具 store 前台应用程序的功能。 此外，还将添加简单的数据绑定导航。 本教程基于前面的 "创建数据访问层" 教程，是 Wingtip 玩具教程系列的一部分。

## <a name="what-youll-learn"></a>学习内容：

- 如何将 UI 更改为支持 Wingtip 玩具 store 前台应用程序的功能。
- 如何将 HTML5 元素配置为包括页面导航。
- 如何创建数据驱动的控件以导航到特定的产品数据。
- 如何显示使用实体框架 Code First 创建的数据库中的数据。

ASP.NET Web 窗体使你可以为 Web 应用程序创建动态内容。 每个 ASP.NET 网页的创建方式类似于静态 HTML 网页（不包含基于服务器的处理的页面），但 ASP.NET 网页包含一些额外的元素，ASP.NET 在页面运行时识别并处理生成 HTML。

使用静态 HTML 页（ *.htm*或 *.html*文件），服务器通过读取文件并按原样将其发送到浏览器来完成 `Web` 请求。 与此相反，当某人请求 ASP.NET 网页（ *.aspx*文件）时，该页面在 Web 服务器上以程序的形式运行。 当该页正在运行时，它可以执行您的网站所需的任何任务，包括计算值、读取或写入数据库信息或调用其他程序。 作为其输出，页面会动态生成标记（例如 HTML 中的元素），并将此动态输出发送到浏览器。

## <a name="modifying-the-ui"></a>修改 UI

通过修改*default.aspx*页，可以继续学习本系列教程。 您将修改已由用于创建应用程序的默认模板建立的 UI。 创建任何 Web 窗体应用程序时，通常会执行的修改类型。 你将通过更改标题、替换某些内容并删除不需要的默认内容来实现此目的。

1. 打开或切换到 " *default.aspx* " 页。
2. 如果该页出现在 "**设计**" 视图中，请切换到 "**源**" 视图。
3. 在页面顶部的 `@Page` 指令中，将 "`Title`" 属性更改为 "欢迎"，如下面的黄色突出显示部分所示。 

    [!code-aspx[Main](ui_and_navigation/samples/sample1.aspx?highlight=1)]
4. 同样，在*default.aspx*页上，替换 `<asp:Content>` 标记中包含的所有默认内容，以便标记显示如下。 

    [!code-aspx[Main](ui_and_navigation/samples/sample2.aspx)]
5. 通过从 "**文件**" 菜单中选择 "**保存**"，保存*default.aspx*页。

   生成的*default.aspx*页将如下所示： 

[!code-aspx[Main](ui_and_navigation/samples/sample3.aspx)]

在此示例中，您设置了 `@Page` 指令的 `Title` 属性。 当在浏览器中显示 HTML 时，服务器代码 `<%: Page.Title %>` 解析 `Title` 属性中包含的内容。

示例页面包含构成 ASP.NET 网页的基本元素。 此页包含静态文本，如您在 HTML 页中所拥有的一样，以及特定于 ASP.NET 的元素。 *Default.aspx*页中包含的内容将与母版页内容集成，本教程稍后将对此内容进行介绍。

### <a name="page-directive"></a>@Page 指令

ASP.NET Web 窗体通常包含允许您为页面指定页面属性和配置信息的指令。 ASP.NET 使用指令作为如何处理页面的说明，但不会将其作为发送到浏览器的标记的一部分呈现。

最常使用的指令是 `@Page` 指令，该指令允许您为页面指定许多配置选项，其中包括：

1. 页中代码的服务器编程语言，如C#。
2. 该页是否是直接在页中包含服务器代码的页面（称为单文件页），还是在单独的类文件中包含代码的页面（称为代码隐藏页）。
3. 页面是否具有关联的母版页，是否应将其视为内容页。
4. 调试和跟踪选项。

如果未在页中包含 `@Page` 指令，或者如果指令不包含特定的设置 *，则将从 web.config 配置文件*或*machine.config 配置文件*继承设置。 *Machine.config*文件为计算机上运行的所有应用程序提供其他配置设置。

> [!NOTE] 
> 
> *Machine.config*还提供了有关所有可能的配置设置的详细信息。

### <a name="web-server-controls"></a>Web 服务器控件

在大多数 ASP.NET Web 窗体应用程序中，您将添加允许用户与页面交互的控件，例如按钮、文本框、列表等。 这些 Web 服务器控件类似于 HTML 按钮和输入元素。 但是，它们是在服务器上处理的，因此可以使用服务器代码来设置其属性。 这些控件还会引发可在服务器代码中处理的事件。

服务器控件使用的特殊语法 ASP.NET 在页面运行时识别。 ASP.NET 服务器控件的标记名称以 `asp:` 前缀开头。 这允许 ASP.NET 识别并处理这些服务器控件。 如果控件不是 .NET Framework 的一部分，则前缀可能会有所不同。 除了 `asp:` 前缀以外，ASP.NET 服务器控件还包括 `runat="server"` 属性和可用于在服务器代码中引用控件的 `ID`。

当页面运行时，ASP.NET 将标识服务器控件，并运行与这些控件关联的代码。 许多控件在浏览器中显示时，会将一些 HTML 或其他标记呈现到页面中。

### <a name="server-code"></a>服务器代码

大多数 ASP.NET Web 窗体应用程序都包含处理页面时服务器上运行的代码。 如上所述，可以使用服务器代码执行多种操作，例如向 ListView 控件添加数据。 ASP.NET 支持在服务器上运行多种语言，包括C#、Visual Basic、j # 和其他语言。

ASP.NET 支持两种模型来编写网页的服务器代码。 在单文件模型中，页面的代码位于一个 script 元素中，其中开始标记包含 `runat="server"` 特性。 或者，您可以在单独的类文件中创建该页的代码，这称为 "代码隐藏" 模型。 在这种情况下，ASP.NET Web 窗体页通常不包含任何服务器代码。 相反，`@Page` 指令包含链接 *.aspx*页面及其关联的代码隐藏文件的信息。

`@Page` 指令中包含的 `CodeBehind` 特性指定了单独的类文件的名称，而 `Inherits` 特性指定了代码隐藏文件中对应于页的类的名称。

### <a name="updating-the-master-page"></a>更新母版页

在 ASP.NET Web 窗体中，母版页允许你在应用程序中创建一致的页面布局。 可以使用单个母版页定义应用程序中所有页（或一组页）的外观和标准行为。 然后，您可以创建包含要显示内容的单独内容页，如上文所述。 当用户请求内容页时，ASP.NET 会将内容页与母版页合并，以生成将母版面布局与内容页中的内容相结合的输出。

新站点需要单个徽标才能在每一页上显示。 若要添加此徽标，可以修改母版页上的 HTML。

1. 在**解决方案资源管理器**中，查找并打开 "**网站母版页**"。
2. 如果该页在 "**设计**" 视图中，请切换到 "**源**" 视图。
3. 通过**修改或添加**以黄色突出显示的标记来更新母版页： 

    [!code-aspx[Main](ui_and_navigation/samples/sample4.aspx?highlight=9,49,76-81,87)]

此 HTML 将在 Web 应用程序的*Images*文件夹中显示名为 "*徽标键*" 的图像，稍后将添加该图像。 当浏览器中显示使用母版页的页面时，将显示该徽标。 如果用户单击徽标，用户将导航回*default.aspx*页面。 HTML 定位点标记 `<a>` 包装图像服务器控件，并允许将该图像作为链接的一部分包含在内。 定位点标记的 `href` 特性指定网站的根 "`~/`" 作为链接位置。 默认情况下，当用户导航到网站的根目录时，将显示*default.aspx*页。 **Image** `<asp:Image>` server 控件包含在浏览器中显示时以 HTML 格式呈现的附加属性，如 `BorderStyle`。

### <a name="master-pages"></a>母版页

母版页是扩展名为 master （例如，ASP.NET）的*文件，其*预定义布局可以包含静态文本、HTML 元素和服务器控件。 母版页由特殊的 `@Master` 指令标识，该指令替换用于普通 *.aspx*页面的 `@Page` 指令。

除了 `@Master` 指令外，母版页还包含页的所有顶级 HTML 元素，如 `html`、`head`和 `form`。 例如，在上面添加的母版页上，使用 HTML `table` 进行布局，使用公司徽标、静态文本和服务器控件的 `img` 元素来处理网站的公共成员身份。 您可以使用任何 HTML 和任何 ASP.NET 元素作为母版页的一部分。

除了在所有页面上显示的静态文本和控件外，母版页还包括一个或多个**ContentPlaceHolder**控件。 这些占位符控件定义要在其中显示可替换内容的区域。 接下来，使用**内容**服务器控件在内容页（如*default.aspx*）中定义可替换内容。

#### <a name="adding-image-files"></a>添加图像文件

必须将上面引用的徽标图像与所有产品图像一起添加到 Web 应用程序，以便在浏览器中显示项目时可以查看它们。

#### <a name="download-from-msdn-samples-site"></a>从 MSDN 示例站点下载：

[与 ASP.NET 4.5 Web 窗体和 Visual Studio 2013-Wingtip 玩具](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409)（C#）入门

下载内容包括用于创建示例应用程序的 " *WingtipToys* " 文件夹中的资源。

1. 如果尚未执行此操作，请使用 MSDN 示例网站中的以上链接下载压缩的示例文件。
2. 下载后，打开 .zip 文件并将内容复制到计算机上的本地文件夹。
3. 查找并打开 " *WingtipToys* " 文件夹。
4. 通过拖放，将*目录*文件夹从本地文件夹复制到 Visual Studio**解决方案资源管理器**中 Web 应用程序项目的根目录。 

    ![UI 和导航-复制文件](ui_and_navigation/_static/image1.png)
5. 接下来，在**解决方案资源管理器**中右键单击 " **WingtipToys** " 项目，然后选择 "**添加** -&gt;**新文件夹**"，创建名为 "*映像*" 的新文件夹。
6. 从**文件资源管理器**中的 WingtipToys 文件夹将文件复制到 Visual Studio**解决方案资源管理器**的 Web 应用程序项目的*Images*文件夹*中。*
7. 如果看不到新文件，请单击**解决方案资源管理器**顶部的 "**显示所有文件**" 选项以更新文件列表。  
  
    现在**解决方案资源管理器**显示已更新的项目文件。 

    ![UI 和导航-解决方案资源管理器](ui_and_navigation/_static/image2.png)

### <a name="adding-pages"></a>添加页

向 Web 应用程序添加导航之前，首先要添加两个要导航到的新页面。 稍后在本系列教程中，你将在这些新页面上显示产品和产品详细信息。

1. 在**解决方案资源管理器**中，右键单击**WingtipToys**，单击 "**添加**"，然后单击 "**新建项**"。   
 随即出现“添加新项”对话框。
2. 选择左侧的 " **Visual C#**  -&gt; **Web**模板" 组。 然后，从中间列表中选择 "**带有母版页的 Web 窗体**"，并将其命名为*ProductList*。 

    ![UI 和导航-"添加新项" 对话框](ui_and_navigation/_static/image3.png)
3. 选择 "**站点**" 以将母版页附加到新创建的 *.aspx*页面。 

    ![UI 和导航-选择母版页](ui_and_navigation/_static/image4.png)
4. 按照相同的步骤，添加一个名为*ProductDetails*的附加页面。

### <a name="updating-bootstrap"></a>更新启动

Visual Studio 2013 项目模板使用由 Twitter 创建的[启动](http://getbootstrap.com/)、布局和主题框架。 启动使用 CSS3 来提供响应式设计，这意味着布局可以动态适应不同的浏览器窗口大小。 你还可以使用启动的主题功能轻松地对应用程序的外观进行更改。 默认情况下，Visual Studio 2013 中的 ASP.NET Web 应用程序模板包括作为 NuGet 包的启动。

在本教程中，你将通过替换启动 CSS 文件来更改 Wingtip 玩具应用程序的外观。

1. 在**解决方案资源管理器**中，打开 "*内容*" 文件夹。
2. 右键单击 "bootstrap-original" 文件，*然后将其*重命名为 ""。
3. 将 bootstrap-original 重命名*为 "* "。
4. 在**解决方案资源管理器**中，右键单击 "*内容*" 文件夹，然后选择 "**在文件资源管理器中打开文件夹**"。  
   将显示文件资源管理器。 将下载的启动 CSS 文件保存到此位置。
5. 在浏览器中转到[https://bootswatch.com/3/](https://bootswatch.com/3/)。
6. 滚动浏览器窗口，直到看到 "Cerulean" 主题。 

    ![UI 和 Cerulean 主题](ui_and_navigation/_static/image5.png)
7. 将*启动 .css*文件和文件*启动*文件都下载到*Content*文件夹中。 使用之前打开的 "**文件资源管理器**" 窗口中显示的内容文件夹的路径。
8. 在**Visual Studio**中**解决方案资源管理器**的顶部，选择 "**显示所有文件**" 选项以显示 "内容" 文件夹中的新文件。 

    ![UI 和导航-解决方案资源管理器](ui_and_navigation/_static/image6.png)

   你将在**Content**文件夹中看到两个新的 CSS 文件，但请注意，每个文件名旁边的图标都将灰显。这意味着该文件尚未添加到项目。
9. 右键单击 "*启动*" 和 *"文件"* ，然后选择 "**包括在项目中**"。   
   稍后在本教程中运行 Wingtip 玩具应用程序时，将显示新的 UI。

> [!NOTE] 
> 
> ASP.NET Web 应用程序模板使用项目*根目录中的文件来*存储启动 CSS 文件的路径。

### <a name="modifying-the-default-navigation"></a>修改默认导航

对于应用程序中的每个页面，都可以通过更改 "*网站母版页*" 中的未排序导航列表元素来修改默认导航。

1. 在**解决方案资源管理器**中，找到并打开 "*网站母版页*"。
2. 将以黄色突出显示的其他导航链接添加到下面显示的未排序列表中：   

    [!code-html[Main](ui_and_navigation/samples/sample5.html?highlight=5)]

如以上 HTML 所示，你修改了每个行项 `<li>` 包含带有 link `href` 特性的定位点标记 `<a>`。 每个 `href` 指向 Web 应用程序中的某个页面。 在浏览器中，当用户单击其中一个链接（如**Products**）时，他们将导航到 `href` 中包含的页面（如**ProductList**）。 在本教程结束时，将运行该应用程序。

> [!NOTE] 
> 
> 颚化符（`~`）用于指定 `href` 路径从项目的根开始。

### <a name="adding-a-data-control-to-display-navigation-data"></a>添加数据控件以显示导航数据

接下来，您将添加一个控件以显示数据库中的所有类别。 每个类别都将充当*ProductList*页面的链接。 当用户在浏览器中单击某个类别链接时，他们将导航到 "产品" 页，并且仅查看与所选类别关联的产品。

使用**ListView**控件可以显示数据库中包含的所有类别。 向母版页添加**ListView**控件：

1. 在 "*网站母版页*" 页中，将以下突出显示的 `<div>` 元素添加到 `<div>` 元素**之后**，该元素包含之前添加的 `id="TitleContent"`：  

    [!code-aspx[Main](ui_and_navigation/samples/sample6.aspx?highlight=7-21)]

此代码将显示数据库中的所有类别。 **ListView**控件将每个类别名称显示为链接文本，并包含指向*ProductList*页面的链接，该链接包含包含类别的 `ID` 的查询字符串值。 通过设置**ListView**控件中的 `ItemType` 属性，可在 `ItemTemplate` 节点内使用数据绑定表达式 `Item`，并将该控件变成强类型。 您可以使用 IntelliSense 选择 `Item` 对象的详细信息，例如指定 `CategoryName`。 此代码包含在标记数据绑定表达式的容器 `<%#: %>` 中。 通过添加（:)在 `<%#` 前缀的末尾，数据绑定表达式的结果是 HTML 编码的。 如果结果是 HTML 编码的，则您的应用程序会受到更好的保护，以防止出现跨站点脚本注入（XSS）和 HTML 注入攻击。

> [!NOTE] 
> 
> **提示**
> 
> 当你在开发过程中键入内容时，你可以确定是否找到了对象的有效成员，因为强类型数据控件显示基于 IntelliSense 的可用成员。 IntelliSense 在键入代码时提供了上下文适当的代码选项，如属性、方法和对象。

在下一步中，你将实现 `GetCategories` 方法来检索数据。

### <a name="linking-the-data-control-to-the-database"></a>将数据控件链接到数据库

你需要将数据控件链接到数据库，然后才能在数据控件中显示数据。 若要创建该链接，可以修改*Site.Master.cs*文件的隐藏代码。

1. 在**解决方案资源管理器**中，右键单击 "*站点" 母版页*，然后单击 "**查看代码**"。 *Site.Master.cs*文件将在编辑器中打开。
2. 在*Site.Master.cs*文件的开头附近，添加另外两个命名空间，以使所有包含的命名空间如下所示：  

    [!code-csharp[Main](ui_and_navigation/samples/sample7.cs?highlight=8-9)]
3. 将突出显示的 `GetCategories` 方法添加到 `Page_Load` 事件处理程序之后，如下所示：  

    [!code-csharp[Main](ui_and_navigation/samples/sample8.cs?highlight=6-11)]

当在浏览器中加载使用母版页的任何页面时，将执行上述代码。 你之前在本教程中添加的 `ListView` 控件（名为 "categoryList"）使用模型绑定来选择数据。 在 `ListView` 控件的标记中，将控件的 `SelectMethod` 属性设置为 `GetCategories` 方法，如上所示。 `ListView` 控件在页面生命周期中的适当时间调用 `GetCategories` 方法，并自动绑定返回的数据。 在下一教程中，你将了解有关绑定数据的详细信息。

### <a name="running-the-application-and-creating-the-database"></a>运行应用程序并创建数据库

在本教程的前面部分中，已创建一个名为 "ProductDatabaseInitializer" 的初始值设定项类，并在*global.asax.cs*文件中指定此类。 首次运行应用程序时，实体框架将生成数据库，因为*global.asax.cs*文件中包含的 `Application_Start` 方法将调用初始值设定项类。 初始值设定项类将使用之前在本教程系列中添加的模型类（`Category` 和 `Product`）来创建数据库。

1. 在**解决方案资源管理器**中，右键单击 " *default.aspx* " 页，然后选择 "**设为起始页**"。
2. 在 Visual Studio 中，按**F5**。   
 在第一次运行期间设置所有内容需要花费一些时间。   
    ![UI 和导航浏览器窗口](ui_and_navigation/_static/image7.png)  
 运行应用程序时，将编译该应用程序，并在*应用\_Data*文件夹中创建名为 wingtiptoys 的数据库 *。* 在浏览器中，会看到一个类别导航菜单。 此菜单是从数据库中检索类别生成的。 在下一教程中，你将实现导航。
3. 关闭浏览器以停止正在运行的应用程序。

### <a name="reviewing-the-database"></a>查看数据库

打开 web.config*文件，* 并查看 "连接字符串" 部分。 您可以看到，连接字符串中的 `AttachDbFilename` 值指向 Web 应用程序项目的 `DataDirectory`。 `|DataDirectory|` 的值是一个保留值，表示项目中的*应用\_Data*文件夹。 此文件夹是从实体类创建的数据库所在的位置。

[!code-xml[Main](ui_and_navigation/samples/sample9.xml)]

> [!NOTE] 
> 
> 如果*应用\_Data*文件夹不可见，或者如果文件夹为空，请选择 "**刷新**" 图标，然后选择 "**解决方案资源管理器**" 窗口顶部的 "**显示所有文件**" 图标。 若要显示所有可用的图标，可能需要扩展**解决方案资源管理器**窗口的宽度。

现在，可以使用 "**服务器资源管理器**" 窗口检查*wingtiptoys*数据库文件中包含的数据。

1. 展开*应用\_Data*文件夹。 如果*应用\_Data*文件夹不可见，请参阅上述说明。
2. 如果*wingtiptoys*数据库文件不可见，请选择 "**刷新**" 图标，然后选择 "**解决方案资源管理器**" 窗口顶部的 "**显示所有文件**" 图标。
3. 右键单击*wingtiptoys*数据库文件，然后选择 "**打开**"。  
    将显示**服务器资源管理器**。 

    ![UI 和导航-服务器资源管理器](ui_and_navigation/_static/image8.png)
4. 展开 *“表”* 文件夹。
5. 右键单击**Products**表，然后选择 "**显示表数据**"。  
 将显示**Products**表。 

    ![UI 和导航产品表](ui_and_navigation/_static/image9.png)
6. 使用此视图可以手动查看和修改**Products**表中的数据。
7. 关闭 " **Products**表" 窗口。
8. 在**服务器资源管理器**中，再次右键单击**Products**表，然后选择 "**打开表定义**"。  
 将显示**Products**表的数据设计。 

    ![UI 和导航产品设计](ui_and_navigation/_static/image10.png)
9. 在**t-sql**选项卡中，你将看到用于创建表的 SQL DDL 语句。 你还可以使用 "**设计**" 选项卡中的 UI 来修改架构。
10. 在**服务器资源管理器**中，右键单击 " **WingtipToys**数据库"，然后选择 "**关闭连接**"。   
 通过从 Visual Studio 中分离数据库，可以在本系列教程的后面部分修改数据库架构。
11. 选择**服务器资源管理器**窗口底部的 "**解决方案资源管理器**" 选项卡，返回到**解决方案资源管理器**。

## <a name="summary"></a>摘要

在本系列教程中，你添加了一些基本的 UI、图形、页面和导航。 此外，还运行了 Web 应用程序，该应用程序从你在上一教程中添加的数据类创建了数据库。 您还可以通过直接查看数据库来查看数据库的*Products*表的内容。 在下一教程中，您将显示数据库中的数据项和详细信息。

## <a name="additional-resources"></a>其他资源

[编程 ASP.NET 网页  简介](https://msdn.microsoft.com/library/ms178125.aspx)  
[ASP.NET Web 服务器控件概述](https://msdn.microsoft.com/library/zsyt68f1.aspx)   
[CSS 教程](http://www.w3schools.com/css/default.asp)

> [!div class="step-by-step"]
> [上一页](create_the_data_access_layer.md)
> [下一页](display_data_items_and_details.md)
