---
uid: web-forms/overview/getting-started/hands-on-labs/whats-new-in-web-forms-in-aspnet-45
title: ASP.NET 4.5 中 Web 窗体的新增功能 |Microsoft Docs
author: rick-anderson
description: ASP.NET Web 窗体的新版本引入了大量改进，重点是改进使用数据时的用户体验。 在以前版本的中 。
ms.author: riande
ms.date: 02/18/2013
ms.assetid: 0a1f88bd-97da-4ed1-86f1-605199dc75a4
msc.legacyurl: /web-forms/overview/getting-started/hands-on-labs/whats-new-in-web-forms-in-aspnet-45
msc.type: authoredcontent
ms.openlocfilehash: 301af8ed877b58624e419c04f605c41f27dbdd0c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78421922"
---
# <a name="whats-new-in-web-forms-in-aspnet-45"></a>ASP.NET 4.5 中 Web 窗体的新增功能

由[Web 训练营团队](https://twitter.com/webcamps)使用

> ASP.NET Web 窗体的新版本引入了大量改进，重点是改进使用数据时的用户体验。
> 
> 在以前版本的 Web 窗体中，当使用数据绑定来发出对象成员的值时，您使用的是数据绑定表达式 Bind （）或 Eval （）。 在 ASP.NET 的新版本中，可以使用新的 ItemType 属性声明控件将绑定到的数据类型。 通过设置此属性，你可以使用强类型化的变量来获得 Visual Studio 开发体验的全部优势，例如 IntelliSense、成员导航和编译时检查。
> 
> 通过数据绑定控件，你现在还可以指定你自己的自定义方法用于选择、更新、删除和插入数据，从而简化了页面控件和应用程序逻辑之间的交互。 此外，已向 ASP.NET 添加了模型绑定功能，这意味着您可以将页面中的数据直接映射到方法类型参数。
> 
> 通过最新版本的 Web 窗体验证用户输入也应该更简单。 你现在可以使用**system.componentmodel. DataAnnotations**命名空间中的验证属性批注模型类，并请求你的所有站点控件使用该信息验证用户输入。 Web 窗体中的客户端验证现在与 jQuery 集成，提供更清晰的客户端代码和非引人注目的 JavaScript 功能。
> 
> 在 "请求验证" 区域中，已进行了改进，使你可以更轻松地关闭对应用程序特定部分的请求验证或读取无效的请求数据。
> 
> 对 Web 窗体服务器控件进行了一些改进，以利用 HTML5 的新功能：
> 
> - 已更新 TextBox 控件的 TextMode 属性，以支持新的 HTML5 输入类型（如电子邮件、日期时间等）。
> - FileUpload 控件现在支持支持此 HTML5 功能的浏览器中的多个文件上传。
> - 验证程序控件现在支持验证 HTML5 输入元素。
> - 具有表示 URL 的特性的新 HTML5 元素现在支持 runat =&quot;server&quot;。 因此，可以在 URL 路径中使用 ASP.NET 约定，如 ~ 运算符来表示应用程序根（例如 &lt;视频 runat =&quot;server&quot; src =&quot;~/myVideo.wmv&quot;&gt;&lt;/video&gt;）。
> - 已修复 UpdatePanel 控件以支持发布 HTML5 输入字段。
> 
> 在官方 ASP.NET 门户中，可以在 ASP.NET WebForms 4.5 中找到新功能的更多示例： [ASP.NET 4.5 和 Visual Studio 2012 中的新增](../../../../whitepapers/whats-new-in-aspnet-45-and-visual-studio-2012.md#_Toc318097385)功能
> 
> 所有示例代码和代码段都包含在 Web 训练营培训工具包中， [https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409](https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409)提供。

<a id="Objectives"></a>
### <a name="objectives"></a>目标

在本动手实验中，您将了解如何：

- 使用强类型化的数据绑定表达式
- 在 Web 窗体中使用新的模型绑定功能
- 使用值提供程序将页面数据映射到代码隐藏方法
- 使用数据批注进行用户输入验证
- 通过 Web 窗体中的 jQuery 利用不引人注目的客户端验证
- 实现精细请求验证
- 在 Web 窗体中实现异步页面处理

<a id="Prerequisites"></a>
### <a name="prerequisites"></a>系统必备

你必须具有以下项才能完成此实验室：

- 适用于 Web 或高级的[Microsoft Visual Studio Express 2012](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) （阅读[附录 A](#AppendixA)以获取有关如何安装的说明）。

<a id="Setup"></a>
### <a name="setup"></a>安装

**安装代码片段**

为方便起见，你将通过此实验室管理的大部分代码都作为 Visual Studio code 片段提供。 若要安装代码段，请运行 **.\Source\Setup\CodeSnippets.vsi**文件。

如果你不熟悉 Visual Studio Code 代码段，并且想要了解如何使用它们，则可以参考本文档中的附录[C： &quot;附录 C：&quot;的代码段](#AppendixC)。

<a id="Exercises"></a>
## <a name="exercises"></a>练习

本动手实验包括以下练习：

1. [练习1： ASP.NET Web 窗体中的模型绑定](#Exercise1)
2. [练习2：数据验证](#Exercise2)
3. [练习3： ASP.NET Web 窗体中的异步页面处理](#Exercise3)

> [!NOTE]
> 每个练习都带有一个**结束**文件夹，其中包含在完成练习后应获得的结果解决方案。 如果需要更多帮助，请使用此解决方案作为指导。

完成本实验的估计时间： **60 分钟**。

<a id="Exercise1"></a>

<a id="Exercise_1_Model_Binding_in_ASPNET_Web_Forms"></a>
### <a name="exercise-1-model-binding-in-aspnet-web-forms"></a>练习1： ASP.NET Web 窗体中的模型绑定

ASP.NET Web 窗体的新版本引入了大量增强功能，重点是改进处理数据时的体验。 在此练习中，您将了解强类型化数据控件和模型绑定。

<a id="Task_1_-_Using_Strongly-Typed_Data-Bindings"></a>
#### <a name="task-1---using-strongly-typed-data-bindings"></a>任务 1-使用强类型数据绑定

在此任务中，您将发现 ASP.NET 4.5 中提供了新的强类型绑定。

1. 打开位于**Source/Ex1-ModelBinding/begin/** Folder 的**begin**解决方案。

   1. 在继续之前，需要下载一些缺少的 NuGet 包。 为此，请单击 "**项目**" 菜单并选择 "**管理 NuGet 包**"。
   2. 在 "**管理 NuGet 包**" 对话框中，单击 "**还原**" 以下载缺少的包。
   3. 最后，通过单击 "**生成** | **生成解决方案**" 来生成解决方案。

      > [!NOTE]
      > 使用 NuGet 的优点之一是，无需将所有库都送到项目中，从而减少了项目的大小。 使用 NuGet 功能，通过在包 .config 文件中指定包版本，你可以在首次运行项目时下载所有必需的库。 这就是在从此实验室打开现有解决方案之后需要运行这些步骤的原因。
2. 打开 " **Customers** " 页。 在主控件中放置未编号的列表，并在内包含一个用于列出每个客户的 repeater 控件。 将 repeater 名称设置为**customersRepeater** ，如以下代码所示。

    在以前版本的 Web 窗体中，当使用数据绑定在要进行数据绑定的对象上发出成员的值时，应使用数据绑定表达式和对 Eval 方法的调用，并将成员的名称作为字符串进行传递。

    在运行时，对 Eval 的这些调用将对当前绑定的对象使用反射来读取具有给定名称的成员的值，并在 HTML 中显示结果。 利用这种方法，可以非常轻松地对任意 unshaped 的数据进行数据绑定。

    遗憾的是，您在 Visual Studio 中丢失了许多优秀的开发时体验功能，其中包括用于成员名称的 IntelliSense、对导航的支持（如中转到定义）和编译时检查。

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample1.aspx)]
3. 打开**Customers.aspx.cs**文件。
4. 添加以下 using 语句。

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample2.cs)]
5. 在**页面\_Load**方法中，添加代码以用客户列表填充中继器。

    （代码段- *Web 窗体 Ex01-绑定客户数据源*）

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample3.cs)]

    解决方案结合使用 EntityFramework 和 CodeFirst 来创建和访问数据库。 在下面的代码中，customersRepeater 绑定到一个具体化查询，该查询将返回数据库中的所有客户。
6. 按**F5**运行解决方案并访问 "**客户**" 页，查看操作中的中继器。 当解决方案使用 CodeFirst 时，在运行应用程序时，将创建数据库并将其填充到本地 SQL Express 实例中。

    ![使用中继器列出客户](whats-new-in-web-forms-in-aspnet-45/_static/image1.png "使用中继器列出客户")

    *使用中继器列出客户*

    > [!NOTE]
    > 在 Visual Studio 2012 中，IIS Express 是默认的 Web 开发服务器。
7. 关闭浏览器并返回到 Visual Studio。
8. 现在，将该实现替换为使用强类型绑定。 打开 " **customer .aspx** " 页，并在 repeater 中使用 "新建**ItemType** " 属性将 "**客户**类型" 设置为 "绑定类型"。

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample4.aspx)]

    ItemType 属性使你能够声明控件将绑定到的数据类型，并允许在数据绑定控件内使用强类型绑定。
9. 将 ItemTemplate 内容替换为以下代码。

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample5.aspx)]

    上面的方法的一个缺点是对 Eval （）和 Bind （）的调用是后期绑定的，也就是说，传递字符串来表示属性名称。 这意味着，你不会获得有关成员名称、对代码导航的支持（如 "转到定义"）和编译时检查支持的 Intellisense。

    设置 ItemType 属性会导致在数据绑定表达式的作用域中生成两个新的类型化变量： **Item**和**BindItem**。 您可以在数据绑定表达式中使用这些强类型化变量，并获得 Visual Studio 开发体验的全部好处。

    表达式中使用的 &quot; **：** &quot; 将自动对输出进行 HTML 编码，以避免安全问题（例如跨站点脚本攻击）。 自 .NET 4 后，此批注可用于响应写入，但现在也可用于数据绑定表达式。

    > [!NOTE]
    > 项成员适用于单向绑定。 如果要执行双向绑定，请使用**BindItem**成员。

    ![强类型绑定中的 IntelliSense 支持](whats-new-in-web-forms-in-aspnet-45/_static/image2.png "强类型绑定中的 IntelliSense 支持")

    *强类型绑定中的 IntelliSense 支持*
10. 按**F5**运行解决方案并中转到 "客户" 页，以确保更改按预期方式工作。

    ![列出客户详细信息](whats-new-in-web-forms-in-aspnet-45/_static/image3.png "列出客户详细信息")

    *列出客户详细信息*
11. 关闭浏览器并返回到 Visual Studio。

<a id="Task_2_-_Introducing_Model_Binding_in_Web_Forms"></a>
#### <a name="task-2---introducing-model-binding-in-web-forms"></a>任务 2-Web 窗体中的模型绑定简介

在以前版本的 ASP.NET Web 窗体中，当你想要执行双向数据绑定（检索和更新数据）时，你需要使用数据源对象。 这可以是对象数据源、SQL 数据源、LINQ 数据源等。 但是，如果您的方案需要用于处理数据的自定义代码，则需要使用对象数据源，这会带来一些缺点。 例如，你需要避免复杂类型，并在执行验证逻辑时需要处理异常。

在新版本的 ASP.NET Web 窗体中，数据绑定控件支持模型绑定。 这意味着，你可以直接在数据绑定控件中指定 select、update、insert 和 delete 方法，以便从代码隐藏文件或其他类调用逻辑。

要了解这一点，你将使用一个 GridView 来列出使用新**SelectMethod**属性的产品类别。 使用此属性可以指定用于检索 GridView 数据的方法。

1. 打开 " **default.aspx** " 页并包含**GridView**。 按如下所示配置 GridView，使用强类型绑定并启用排序和分页。

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample6.aspx)]
2. 使用新的**SelectMethod**属性可将 GridView 配置为调用**GetCategories**方法来选择数据。

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample7.aspx)]
3. 打开**Products.aspx.cs**代码隐藏文件，并添加以下 using 语句。

    （代码段- *Web 窗体 Ex01-命名空间*）

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample8.cs)]
4. 在**Products**类中添加私有成员，并分配**ProductsContext**的新实例。 此属性将存储可用于连接到数据库的实体框架数据上下文。

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample9.cs)]
5. 使用 LINQ 创建**GetCategories**方法以检索类别列表。 该查询将包含**products**属性，以便 GridView 可以显示每个类别的产品数量。 请注意，该方法返回一个原始 IQueryable 对象，该对象表示稍后要在页面生命周期中执行的查询。

    （代码段- *Web 窗体 Ex01-GetCategories*）

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample10.cs)]

    > [!NOTE]
    > 在以前版本的 ASP.NET Web 窗体中，通过在对象数据源上下文中使用自己的存储库逻辑启用排序和分页，需要编写自己的自定义代码并接收所有必需的参数。 现在，由于数据绑定方法可以返回 IQueryable，这表示仍在执行查询，ASP.NET 可以负责修改查询以添加正确的排序和分页参数。
6. 按**F5**开始调试站点并中转到 "产品" 页。 应会看到 GridView 用 GetCategories 方法返回的类别填充。

    ![使用模型绑定填充 GridView](whats-new-in-web-forms-in-aspnet-45/_static/image4.png "使用模型绑定填充 GridView")

    *使用模型绑定填充 GridView*
7. 按**SHIFT**+**F5**停止调试。

<a id="Task_3_-_Value_Providers_in_Model_Binding"></a>
#### <a name="task-3---value-providers-in-model-binding"></a>任务 3-模型绑定中的值提供程序

模型绑定不仅使你能够指定自定义方法来直接在数据绑定控件中处理数据，而且还允许你将页面中的数据映射到这些方法中的参数。 在 method 参数上，可以使用值提供程序特性来指定值的数据源。 例如:

- 页面上的控件
- 查询字符串值
- 查看数据
- 会话状态
- Cookie
- 已发布的表单数据
- 视图状态
- 同时支持自定义值提供程序

如果使用了 ASP.NET MVC 4，则会注意到模型绑定支持类似。 实际上，这些功能是从 ASP.NET MVC 获取的，并移**到了 system.web**程序集中，也可以在 Web 窗体上使用这些功能。

在此任务中，您将更新 GridView 以便按每个类别的产品数量来筛选结果，并通过模型绑定接收筛选器参数。

1. 返回到 " **Products** " 页。
2. 在 GridView 顶部，添加一个**标签**和一个**ComboBox** ，为每个类别选择产品数，如下所示。

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample11.aspx)]
3. 向 GridView 添加**EmptyDataTemplate** ，以便在不存在具有所选产品数的类别时显示一条消息。

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample12.aspx)]
4. 打开**Products.aspx.cs**代码隐藏并添加以下 using 语句。

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample13.cs)]
5. 修改**GetCategories**方法以接收整数**minProductsCount**参数并筛选返回的结果。 为此，请将方法替换为以下代码。

    （代码段- *Web 窗体 Ex01-GetCategories 2*）

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample14.cs)]

    **MinProductsCount**参数上的新 **[Control]** 属性将使 ASP.NET 知道其值必须使用页面中的控件填充。 ASP.NET 将查找与参数名称（minProductsCount）匹配的任何控件，并执行所需的映射和转换，以用控件值填充参数。

    此外，特性还提供了一个重载构造函数，该构造函数使你能够指定从何处获取该值的控件。

    > [!NOTE]
    > 数据绑定功能的一个目标是减少需要为页面交互编写的代码量。 除了 [Control] 值提供程序外，你还可以在方法参数中使用其他模型绑定提供程序。 其中一些部分在任务介绍中列出。
6. 按**F5**开始调试站点并中转到 "产品" 页。 在下拉列表中选择多个产品，并注意 GridView 现在的更新方式。

    ![使用下拉列表值筛选 GridView](whats-new-in-web-forms-in-aspnet-45/_static/image5.png "使用下拉列表值筛选 GridView")

    *使用下拉列表值筛选 GridView*
7. 停止调试。

<a id="Task_4_-_Using_Model_Binding_for_Filtering"></a>
#### <a name="task-4---using-model-binding-for-filtering"></a>任务 4-使用模型绑定进行筛选

在此任务中，您将添加第二个子 GridView，以显示所选类别中的产品。

1. 打开 " **default.aspx** " 页，并将 "GridView" 类别更新为 "自动生成" 选择按钮。

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample15.aspx)]
2. 在底部添加名为**productsGrid**的第二个**GridView** 。 将**ItemType**设置为**WebFormsLab**，将**DataKeyNames**设置为**ProductId** ，将**SelectMethod**设置为**GetProducts**。 将**AutoGenerateColumns**设置为**false** ，并添加 ProductId、ProductName、Description 和单价的列。

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample16.aspx)]
3. 打开**Products.aspx.cs**代码隐藏文件。 实现**GetProducts**方法，以从类别 GridView 接收类别 ID 并筛选产品。 模型绑定将使用**categoriesGrid**中的选定行设置参数值。 由于参数名称和控件名称不匹配，因此应在控件值提供程序中指定控件的名称。

    （代码段- *Web 窗体 Ex01-GetProducts*）

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample17.cs)]

    > [!NOTE]
    > 此方法可以更轻松地对这些方法进行单元测试。 在未执行 Web 窗体的单元测试上下文上，[Control] 特性不会执行任何特定操作。
4. 打开 " **products** " 页，找到 "产品" GridView。 更新 "产品" GridView 以显示用于编辑所选产品的链接。

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample18.aspx)]
5. 打开**ProductDetails**页代码隐藏，并将**SelectProduct**方法替换为以下代码。

    （代码段- *Web 窗体 Ex01-SelectProduct 方法*）

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample19.cs)]

    > [!NOTE]
    > 请注意， **[QueryString]** 特性用于通过查询字符串中的 productId 参数填充方法参数。
6. 按**F5**开始调试站点并中转到 "产品" 页。 从 "类" GridView 中选择任意类别，并注意 "产品" GridView 已更新。

    ![显示所选类别的产品](whats-new-in-web-forms-in-aspnet-45/_static/image6.png "显示所选类别的产品")

    *显示所选类别的产品*
7. 单击产品上的 "**查看**" 链接，打开 "ProductDetails" 页。

    请注意，页面使用来自查询字符串的 productId 参数从 SelectMethod 检索产品。

    ![查看产品详细信息](whats-new-in-web-forms-in-aspnet-45/_static/image7.png "查看产品详细信息")

    *查看产品详细信息*

    > [!NOTE]
    > 在下一练习中将实现键入 HTML 说明的功能。

<a id="Task_5_-_Using_Model_Binding_for_Update_Operations"></a>
#### <a name="task-5---using-model-binding-for-update-operations"></a>任务 5-对更新操作使用模型绑定

在上一任务中，你已使用了模型绑定来选择数据，在此任务中，你将了解如何在更新操作中使用模型绑定。

你将更新 "GridView" 类别以允许用户更新类别。

1. 打开 " **Products** " 页，并将 "GridView" 类别更新为 "自动生成编辑" 按钮，然后使用 new **UpdateMethod**属性指定**UpdateCategory**方法来更新所选项目。

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample20.aspx)]

    GridView 中的 DataKeyNames 属性定义了唯一标识模型绑定对象的成员，因此，这是 update 方法至少应接收的参数。
2. 打开**Products.aspx.cs**代码隐藏文件并实现**UpdateCategory**方法。 方法应接收类别 ID 以加载当前类别，并填充 GridView 中的值，然后更新类别。

    （代码段- *Web 窗体 Ex01-UpdateCategory*）

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample21.cs)]

    Page 类中的新**TryUpdateModel**方法负责使用页面中控件的值填充模型对象。 在这种情况下，它会将正在编辑的当前 GridView 行中的更新值替换为**category**对象。

    > [!NOTE]
    > 下一步将说明如何使用 ModelState 在编辑对象时验证用户输入的数据。
3. 运行站点并中转到 "产品" 页。 编辑类别。 键入新名称，然后单击 "**更新**" 以保存更改。

    ![编辑类别](whats-new-in-web-forms-in-aspnet-45/_static/image8.png "编辑类别")

    *编辑类别*

<a id="Exercise2"></a>

<a id="Exercise_2_Data_Validation"></a>
### <a name="exercise-2-data-validation"></a>练习2：数据验证

在此练习中，您将了解 ASP.NET 4.5 中的新数据验证功能。 你将在 Web 窗体中查看新的非引人注目验证功能。 您将使用应用程序模型类中的数据注释进行用户输入验证，最后，您将学习如何打开或关闭对页面中各个控件的请求验证。

<a id="Task_1_-_Unobtrusive_Validation"></a>
#### <a name="task-1---unobtrusive-validation"></a>任务 1-不引人注目的验证

包含复杂数据（包括验证程序）的窗体往往会在页面中生成太多 JavaScript 代码，这可能表示约60% 的代码。 启用非引人注目验证后，HTML 代码将显示为 "整洁" 和 "整齐"。

在本部分中，将在 ASP.NET 中启用不引人注目的验证，以比较两个配置生成的 HTML 代码。

1. 打开**Visual Studio 2012**并打开位于此实验室的**Source\Ex2-Validation\Begin**文件夹中的 "**开始**" 解决方案。 或者，你可以继续在上一个练习中使用现有解决方案。

   1. 如果你打开了提供的**开始**解决方案，则需要下载一些缺少的 NuGet 包，然后再继续。 为此，请在解决方案资源管理器中，单击 " **WebFormsLab** " 项目 "**管理 NuGet 包**"。
   2. 在 "**管理 NuGet 包**" 对话框中，单击 "**还原**" 以下载缺少的包。
   3. 最后，通过单击 "**生成** | **生成解决方案**" 来生成解决方案。

      > [!NOTE]
      > 使用 NuGet 的优点之一是，无需将所有库都送到项目中，从而减少了项目的大小。 使用 NuGet 功能，通过在包 .config 文件中指定包版本，你可以在首次运行项目时下载所有必需的库。 这就是在从此实验室打开现有解决方案之后需要运行这些步骤的原因。
2. 按**F5**启动 web 应用程序。 中转到 "客户" 页，然后单击 "**添加新客户**" 链接。
3. 右键单击浏览器页，然后选择 "**查看源**" 选项以打开应用程序生成的 HTML 代码。

    ![显示页面 HTML 代码](whats-new-in-web-forms-in-aspnet-45/_static/image9.png "显示页面 HTML 代码")

    *显示页面 HTML 代码*
4. 滚动页面源代码，注意 ASP.NET 已在页面中注入了 JavaScript 代码和数据验证器以执行验证并显示 "错误列表"。

    ![在 CustomerDetails 页中验证 JavaScript 代码](whats-new-in-web-forms-in-aspnet-45/_static/image10.png "在 CustomerDetails 页中验证 JavaScript 代码")

    *在 CustomerDetails 页中验证 JavaScript 代码*
5. 关闭浏览器并返回到 Visual Studio。
6. 现在，您将启用非引人注目的验证。 打开**web.config**并在**AppSettings**节中找到**ValidationSettings： UnobtrusiveValidationMode**键 **。** 将键值设置为**WebForms**。

    [!code-xml[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample22.xml)]

    > [!NOTE]
    > 你还可以在 "&quot;" 页中设置此属性 **\_Load**&quot; 事件，以防只为某些页面启用不引人注目的验证。
7. 打开**CustomerDetails**并按**F5**启动 Web 应用程序。
8. 按 F12 键打开 IE 开发人员工具。 开发人员工具打开后，选择 "脚本" 选项卡。从菜单中选择 " **CustomerDetails** "，并注意在页面上运行 jQuery 所需的脚本已从本地站点加载到浏览器中。

    ![直接从本地 IIS 服务器加载 jQuery JavaScript 文件](whats-new-in-web-forms-in-aspnet-45/_static/image11.png "直接从本地 IIS 服务器加载 jQuery JavaScript 文件")

    *直接从本地 IIS 服务器加载 jQuery JavaScript 文件*
9. 关闭浏览器以返回到 Visual Studio。 再次打开 " **Master** " 文件并找到**ScriptManager**。 添加属性**EnableCdn**属性，其值**为 True**。 这将强制从联机 URL 而不是从本地站点的 URL 加载 jQuery。
10. 在 Visual Studio 中打开**CustomerDetails** 。 按 F5 键以运行站点。 Internet Explorer 打开后，按 F12 键打开开发人员工具。 选择 "**脚本**" 选项卡，然后查看下拉列表。 请注意，jQuery JavaScript 文件不再从本地站点加载，而是从联机 jQuery CDN 中加载。

    ![正在从 CDN 加载 jQuery JavaScript 文件](whats-new-in-web-forms-in-aspnet-45/_static/image12.png "正在从 CDN 加载 jQuery JavaScript 文件")

    *正在从 CDN 加载 jQuery JavaScript 文件*
11. 使用浏览器中的 "查看源" 选项再次打开 HTML 页源代码。 请注意，启用非引人注目验证 ASP.NET 已将插入的 JavaScript 代码替换为数据 \*特性。

    ![非引人注目的验证代码](whats-new-in-web-forms-in-aspnet-45/_static/image13.png "非引人注目的验证代码")

    *非引人注目的验证代码*

    > [!NOTE]
    > 在此示例中，您看到了如何将带有数据批注的验证摘要简化为仅有少量的 HTML 和 JavaScript 行。 以前，如果不进行非引人注目的验证，添加的验证控件就越多，JavaScript 验证代码也就越大。

<a id="Task_2_-_Validating_the_Model_with_Data_Annotations"></a>
#### <a name="task-2---validating-the-model-with-data-annotations"></a>任务 2-通过数据批注验证模型

ASP.NET 4.5 引入了针对 Web 窗体的数据批注验证。 你现在可以在模型类中定义约束并跨所有 web 应用程序使用它们，而无需对每个输入进行验证控制。 在本部分中，您将学习如何使用数据批注来验证新的/编辑客户窗体。

1. 打开**CustomerDetail**页。 请注意，" **EditItemTemplate** " 和 "**则**" 部分中的 customer first name 和 second name 使用 RequiredFieldValidator 控件进行验证。 每个验证程序都与特定的条件相关联，因此，需要将任意数量的验证程序包含为要检查的条件。
2. 添加数据批注来验证 Customer 模型类。 打开**模型**文件夹中的**Customer.cs**类，并使用数据批注特性*修饰*每个属性。

    （代码段- *Web 窗体 Ex02-数据批注*）

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample23.cs)]

    > [!NOTE]
    > .NET Framework 4.5 已扩展现有数据批注集合。 下面是一些可以使用的数据批注： [CreditCard]、[Phone]、[EmailAddress]、[Range]、[Compare]、[Url]、[FileExtensions]、[Required]、 [Key]、[RegularExpression]。
    > 
    > 一些用法示例：
    > 
    > [Key]: Specifies that an attribute is the unique identifier
    > 
    > [Range(0.4, 0.5, ErrorMessage=&quot;{Write an error message}&quot;]: Double range
    > 
    > [EmailAddress(ErrorMessage=&quot;Invalid Email&quot;), MaxLength(56)]: Two annotations in the same line.
    > 
    > 您还可以在每个属性中定义自己的错误消息。
3. 打开**CustomerDetails** ，并删除 FormView 控件的 EditItemTemplate 和则部分中的第一个和最后一个名称字段的所有 RequiredFieldValidators。

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample24.aspx)]

    > [!NOTE]
    > 使用数据批注的一个优点是，验证逻辑不会在应用程序页中重复。 在模型中定义一次，并在操作数据的所有应用程序页中使用它。
4. 打开**CustomerDetails**代码隐藏并找到 SaveCustomer 方法。 当插入新客户并从 FormView 控制值接收 Customer 参数时，将调用此方法。 当页控件和参数对象之间的映射发生时，ASP.NET 将对所有数据批注特性执行模型验证，并在 ModelState 字典中填充遇到的错误（如果有）。

    如果模型中的所有字段在执行验证后均有效，则 ModelState 将仅返回 true。

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample25.cs)]
5. 在 CustomerDetails 页的末尾添加一个**ValidationSummary**控件以显示模型错误的列表。

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample26.aspx)]

    **ShowModelStateErrors**是 ValidationSummary 控件上的新属性，当设置为**true**时，控件将显示 ModelState 字典中的错误。 这些错误来自数据批注验证。
6. 按**F5**运行 Web 应用程序。 用一些错误值填写窗体，并单击 "**保存**" 以执行验证。 请注意底部的 "错误摘要"。

    ![数据批注验证](whats-new-in-web-forms-in-aspnet-45/_static/image14.png "数据批注验证")

    *数据批注验证*

<a id="Task_3_-_Handling_Custom_Database_Errors_with_ModelState"></a>
#### <a name="task-3---handling-custom-database-errors-with-modelstate"></a>任务 3-处理 ModelState 的自定义数据库错误

在以前版本的 Web 窗体中，处理数据库错误（如太长的字符串或唯一键冲突）可能涉及在你的存储库代码中引发异常，然后在代码隐藏中处理异常以显示错误。 需要大量代码来执行相对简单的操作。

在 Web 窗体4.5 中，可以通过一致的方式将 ModelState 对象用于显示页面上的错误，不管是从模型还是从数据库。

在此任务中，您将添加代码来正确处理数据库异常，并使用 ModelState 对象向用户显示相应的消息。

1. 在应用程序仍在运行时，尝试使用重复的值更新类别的名称。

    ![更新具有重复名称的类别](whats-new-in-web-forms-in-aspnet-45/_static/image15.png "更新具有重复名称的类别")

    *更新具有重复名称的类别*

    请注意，由于 "**类别名称**" 列 &quot;唯一&quot; 约束，将引发异常。

    ![重复类别名称的异常](whats-new-in-web-forms-in-aspnet-45/_static/image16.png "重复类别名称的异常")

    *重复类别名称的异常*
2. 停止调试。 在**Products.aspx.cs**代码隐藏文件中，更新**UpdateCategory**方法以处理 db 引发的异常。SaveChanges （）方法调用，并将错误添加到**ModelState**对象。

    新的**TryUpdateModel**方法使用用户提供的窗体数据更新从数据库检索的类别对象。

    （代码段- *Web 窗体 Ex02-UpdateCategory 处理错误*）

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample27.cs)]

    > [!NOTE]
    > 理想情况下，您必须确定 DbUpdateException 的原因，并检查根本原因是否违反了唯一键约束。
3. 打开 " **default.aspx** "，然后在 "类别" GridView 下面添加**ValidationSummary**控件，以显示模型错误的列表。

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample28.aspx)]
4. 运行站点并中转到 "产品" 页。 尝试使用重复的值更新类别的名称。

    请注意，已处理异常并且错误消息显示在**ValidationSummary**控件中。

    ![类别重复错误](whats-new-in-web-forms-in-aspnet-45/_static/image17.png "类别重复错误")

    *类别重复错误*

<a id="Task_4_-_Request_Validation_in_ASPNET_Web_Forms_45"></a>
#### <a name="task-4---request-validation-in-aspnet-web-forms-45"></a>任务 4-ASP.NET Web 窗体4.5 中的请求验证

ASP.NET 中的请求验证功能针对跨站点脚本（XSS）攻击提供一定程度的默认保护。 在以前版本的 ASP.NET 中，请求验证在默认情况下处于启用状态，并且只能为整个页面禁用。 使用新版本的 ASP.NET Web 窗体，你现在可以对单个控件禁用请求验证，执行延迟请求验证或访问未经验证的请求数据（如果你这样做，请注意）。

1. 按**Ctrl + F5**以启动站点而不进行调试，并中转到 "产品" 页。 选择一个类别，然后单击任意产品上的 "**编辑**" 链接。
2. 键入一个说明，其中包含可能危险的内容，例如，HTML 标记。 请注意因请求验证而引发的异常。

    ![编辑具有潜在危险内容的产品](whats-new-in-web-forms-in-aspnet-45/_static/image18.png "编辑具有潜在危险内容的产品")

    *编辑具有潜在危险内容的产品*

    ![由于请求验证而引发的异常](whats-new-in-web-forms-in-aspnet-45/_static/image19.png "由于请求验证而引发的异常")

    *由于请求验证而引发的异常*
3. 关闭页面，并在 Visual Studio 中按**SHIFT + F5**停止调试。
4. 打开 " **ProductDetails** " 页，找到 "**说明**" 文本框。
5. 向文本框中添加新的 " **ValidateRequestMode** " 属性，并将其值设置为 "**已禁用**"。

    新的**ValidateRequestMode**属性允许您在每个控件上按粒度禁用请求验证。 当你想要使用可能接收 HTML 代码的输入，但想要在页面的其余部分保持验证工作时，这非常有用。

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample29.aspx)]
6. 按**F5**运行 web 应用程序。 再次打开 "编辑产品" 页，并完成包含 HTML 标记的产品说明。 请注意，现在可以将 HTML 内容添加到说明中。

    ![已对产品说明禁用请求验证](whats-new-in-web-forms-in-aspnet-45/_static/image20.png "已对产品说明禁用请求验证")

    *已对产品说明禁用请求验证*

    > [!NOTE]
    > 在生产应用程序中，您应该净化用户输入的 HTML 代码，以确保仅输入安全 HTML 标记（例如，没有&gt; 标记的 &lt;脚本）。 为此，可以使用[Microsoft Web 保护库](https://www.nuget.org/packages/AntiXSS)。
7. 再次编辑该产品。 在 "名称" 字段中键入 HTML 代码，然后单击 "**保存**"。 请注意，仅对 "说明" 字段禁用请求验证，其余字段仍将根据潜在的危险内容进行验证。

    ![在其余字段中启用了请求验证](whats-new-in-web-forms-in-aspnet-45/_static/image21.png "在其余字段中启用了请求验证")

    *在其余字段中启用了请求验证*

    ASP.NET Web Forms 4.5 包括一种新的请求验证模式，用于延迟执行请求验证。 当请求验证模式设置为**4.5**时，如果一段代码访问*请求。窗体 [&quot;键&quot;]* ，ASP.NET 4.5 的请求验证仅对窗体集合中的特定元素触发请求验证。

    此外，ASP.NET 4.5 现在包含 Microsoft 反 XSS 库 v4.0 提供的核心编码例程。 在新的**AntiXss**命名空间中找到的新*AntiXssEncoder*类型实现了 anti-spam 编码例程。 如果将**encoderType**参数配置为使用*AntiXssEncoder*，则 ASP.NET 中的所有输出编码会自动使用新的编码例程。
8. ASP.NET 4.5 请求验证还支持对请求数据进行未经验证的访问。 ASP.NET 4.5 将新的集合属性添加到名为**未经验证**的**HttpRequest**对象。 导航到**HttpRequest**时，可以访问请求数据的所有常见部分，包括 Forms、Querystring、Cookie、url 等。

    ![未经验证对象](whats-new-in-web-forms-in-aspnet-45/_static/image22.png "未经验证对象")

    *未经验证对象*

    > [!NOTE]
    > **请谨慎使用 HttpRequest 属性！** 请确保仔细对原始请求数据执行自定义验证，以确保不会将危险文本作为往返，并将其呈现给不太严格的客户！

<a id="Exercise3"></a>

<a id="Exercise_3_Asynchronous_Page_Processing_in_ASPNET_Web_Forms"></a>
### <a name="exercise-3-asynchronous-page-processing-in-aspnet-web-forms"></a>练习3： ASP.NET Web 窗体中的异步页面处理

在此练习中，将引入 ASP.NET Web 窗体中的新的异步页处理功能。

<a id="Task_1_-_Updating_the_Product_Details_Page_to_Upload_and_Show_Images"></a>
#### <a name="task-1---updating-the-product-details-page-to-upload-and-show-images"></a>任务 1-更新产品详细信息页以上传和显示图像

在此任务中，你将更新 "产品详细信息" 页，以允许用户为产品指定图像 URL，并将其显示在只读视图中。 您将通过同步下载指定映像的本地副本。 在下一任务中，您将更新此实现以使其以异步方式运行。

1. 打开**Visual Studio 2012**并从该实验室的文件夹中加载位于**Source\Ex3-Async\Begin**的**开始**解决方案。 或者，你可以继续处理前面练习中的现有解决方案。

   1. 如果你打开了提供的**开始**解决方案，则需要下载一些缺少的 NuGet 包，然后再继续。 为此，请在解决方案资源管理器中单击 " **WebFormsLab** " 项目，并选择 "**管理 NuGet 包**"。
   2. 在 "**管理 NuGet 包**" 对话框中，单击 "**还原**" 以下载缺少的包。
   3. 最后，通过单击 "**生成** | **生成解决方案**" 来生成解决方案。

      > [!NOTE]
      > 使用 NuGet 的优点之一是，无需将所有库都送到项目中，从而减少了项目的大小。 使用 NuGet 功能，通过在包 .config 文件中指定包版本，你可以在首次运行项目时下载所有必需的库。 这就是在从此实验室打开现有解决方案之后需要运行这些步骤的原因。
2. 打开**ProductDetails**页源，并在 FormView 的 ItemTemplate 中添加一个字段，以显示产品映像。

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample30.aspx)]
3. 添加字段以指定 FormView 的 EditTemplate 中的图像 URL。

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample31.aspx)]
4. 打开**ProductDetails.aspx.cs**代码隐藏文件，并添加以下命名空间指令。

    （代码段- *Web 窗体 Ex03-命名空间*）

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample32.cs)]
5. 创建**UpdateProductImage**方法，将远程映像存储在本地**images**文件夹中，并使用新的映像位置值更新 product 实体。

    （代码段- *Web 窗体 Ex03-UpdateProductImage*）

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample33.cs)]
6. 更新**UpdateProduct**方法，以调用**UpdateProductImage**方法。

    （代码段- *Web 窗体 Ex03-UpdateProductImage 调用*）

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample34.cs)]
7. 运行应用程序并尝试上传产品的映像。 例如，可以使用 Office 剪贴画中的以下图像 URL： [ [http://officeimg.vo.msecnd.net/images/MB900437099.jpg](http://officeimg.vo.msecnd.net/images/MB900437099.jpg)](http://officeimg.vo.msecnd.net/images/MB900437099.jpg)

    ![为产品设置图像](whats-new-in-web-forms-in-aspnet-45/_static/image23.png "为产品设置图像")

    *为产品设置图像*

<a id="Task_2_-_Adding_Asynchronous_Processing_to_the_Product_Details_Page"></a>
#### <a name="task-2---adding-asynchronous-processing-to-the-product-details-page"></a>任务 2-将异步处理添加到产品详细信息页

在此任务中，你将更新产品详细信息页，使其以异步方式运行。 你将通过使用 ASP.NET 4.5 异步页面处理来增强长时间运行的任务-映像下载过程。

Web 应用程序中的异步方法可用于优化使用 ASP.NET 线程池的方式。 在 ASP.NET 中，线程池中有有限数量的线程用于参与请求，因此，当所有线程都处于繁忙状态时，ASP.NET 将开始拒绝新请求，发送应用程序错误消息并使站点不可用。

您的网站上的耗时操作非常适合用于异步编程，因为它们长时间占用了分配的线程。 这包括长时间运行的请求、包含大量不同元素的页和需要脱机操作的页，例如查询数据库或访问外部 web 服务器。 优点在于，如果对这些操作使用异步方法，则在页正在处理时，线程将被释放并返回到线程池，并可用于参与到新的页面请求。 这意味着，此页将在线程池的一个线程中开始处理，并可能在异步处理完成后在另一个线程中完成处理。

1. 打开**ProductDetails**页。 在**Page**元素中添加**Async**特性，并将其设置为**true**。 此属性告知 ASP.NET 实现 IHttpAsyncHandler 接口。

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample35.aspx)]
2. 在页面底部添加标签以显示运行页面的线程的详细信息。

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample36.aspx)]
3. 打开**ProductDetails.aspx.cs**并添加以下命名空间指令。

    （代码段- *Web 窗体 Ex03-命名空间 2*）

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample37.cs)]
4. 修改**UpdateProductImage**方法以使用异步任务下载映像。 将**WebClient** **DownloadFile**方法替换为**DownloadFileTaskAsync**方法，并包含**await**关键字。

    （代码段- *Web 窗体 Ex03-UpdateProductImage Async*）

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample38.cs)]

    Onendselect 注册要在不同的线程中执行的新页面异步任务。 它将接收包含要执行的任务（t）的 lambda 表达式。 **DownloadFileTaskAsync**方法中的**await**关键字将方法的其余部分转换为在**DownloadFileTaskAsync**方法完成后异步调用的回调。 ASP.NET 将自动维护所有 HTTP 请求的原始值，从而恢复方法的执行。 .NET 4.5 中的新异步编程模型使你能够编写类似于同步代码的异步代码，并让编译器处理回调函数或继续代码的复杂性。
    > [!NOTE]
    > 自 .NET 2.0 起，Onendselect 和 PageAsyncTask 已可用。 Await 关键字是 .NET 4.5 异步编程模型中的新，可与 .NET WebClient 对象中的新 TaskAsync 方法一起使用。
5. 添加代码以显示启动并完成执行代码的线程。 为此，请将**UpdateProductImage**方法更新为以下代码。

    （代码段- *Web 窗体 Ex03-显示线程*）

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample39.cs)]
6. 打开**网站的 web.config 文件。** 添加以下 appSetting 变量。

    [!code-xml[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample40.xml)]
7. 按**F5**运行应用程序并上传产品的映像。 请注意，代码启动和完成的线程 ID 可能不同。 这是因为异步任务在 ASP.NET 线程池的单独线程上运行。 任务完成后，ASP.NET 会将任务放回队列中并分配任何可用线程。

    ![异步下载图像](whats-new-in-web-forms-in-aspnet-45/_static/image24.png "异步下载图像")

    *异步下载图像*

> [!NOTE]
> 此外，你可以遵循[附录 B：使用 Web 部署发布 ASP.NET MVC 4 应用程序](#AppendixB)，将此应用程序部署到 Azure。

---

<a id="Summary"></a>
## <a name="summary"></a>摘要

在此动手实验中，已解决并演示了以下概念：

- 使用强类型化的数据绑定表达式
- 在 Web 窗体中使用新的模型绑定功能
- 使用值提供程序将页面数据映射到代码隐藏方法
- 使用数据批注进行用户输入验证
- 通过 Web 窗体中的 jQuery 利用不引人注目的客户端验证
- 实现精细请求验证
- 在 Web 窗体中实现异步页面处理

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a>附录 A：安装 Visual Studio Express 2012 for Web

您可以使用 **[Microsoft Web 平台安装程序](https://www.microsoft.com/web/downloads/platform.aspx)** 为 Web 或其他 &quot;Express&quot; 版本安装**Microsoft Visual Studio Express 2012** 。 以下说明将指导你完成使用*Microsoft Web 平台安装程序*安装*Visual studio Express 2012 for Web*的步骤。

1. 请参阅[[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169)。 或者，如果你已经安装了 Web 平台安装程序，则可以打开它，并<em>使用 AZURE SDK&quot;搜索 Visual Studio Express 2012 For web</em>的产品 &quot;。
2. 单击 "**立即安装**"。 如果你没有**Web 平台安装程序**，则会重定向到 "下载并安装"。
3. **Web 平台安装程序**打开后，单击 "**安装**" 以启动安装程序。

    ![安装 Visual Studio Express](whats-new-in-web-forms-in-aspnet-45/_static/image25.png "安装 Visual Studio Express")

    *安装 Visual Studio Express*
4. 阅读所有产品的许可证和条款，单击 "**我接受**" 以继续。

    ![接受许可条款](whats-new-in-web-forms-in-aspnet-45/_static/image26.png)

    *接受许可条款*
5. 等待下载和安装过程完成。

    ![安装进度](whats-new-in-web-forms-in-aspnet-45/_static/image27.png)

    *安装进度*
6. 安装完成后，单击 "**完成**"。

    ![安装完成](whats-new-in-web-forms-in-aspnet-45/_static/image28.png)

    *安装完成*
7. 单击 "**退出**" 以关闭 Web 平台安装程序。
8. 若要打开 Web Visual Studio Express，请在 "**开始**" 屏幕上，开始书写 &quot;**VS Express**&quot;，然后单击 " **VS Express for Web** " 磁贴。

    ![VS Express for Web 磁贴](whats-new-in-web-forms-in-aspnet-45/_static/image29.png)

    *VS Express for Web 磁贴*

<a id="AppendixB"></a>

<a id="Appendix_B_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
## <a name="appendix-b-publishing-an-aspnet-mvc-4-application-using-web-deploy"></a>附录 B：使用 Web 部署发布 ASP.NET MVC 4 应用程序

本附录将演示如何从 Azure 门户创建新网站，以及如何利用 Azure 提供的 Web 部署发布功能，发布通过实验室获取的应用程序。

<a id="ApxBTask1"></a>

<a id="Task_1_-_Creating_a_New_Web_Site_from_the_Windows_Azure_Portal"></a>
#### <a name="task-1---creating-a-new-web-site-from-the-azure-portal"></a>任务 1-从 Azure 门户创建新网站

1. 请使用[Azure 管理门户](https://manage.windowsazure.com/)，并使用与你的订阅关联的 Microsoft 凭据登录。

    > [!NOTE]
    > 借助 Azure，你可以免费托管10个 ASP.NET 的网站，然后随着流量的增长进行扩展。 你可以在[此处](https://aka.ms/aspnet-hol-azure)注册。

    ![登录到 Windows Azure 门户](whats-new-in-web-forms-in-aspnet-45/_static/image30.png "登录到 Microsoft Azure 门户")

    *登录到门户*
2. 单击命令栏上的 "**新建**"。

    ![创建新网站](whats-new-in-web-forms-in-aspnet-45/_static/image31.png "创建新网站")

    *创建新网站*
3. 单击 "**计算** | **网站**"。 然后选择 "**快速创建**" 选项。 为新网站提供可用 URL，并单击 "**创建**网站"。

    > [!NOTE]
    > Azure 是在云中运行的 web 应用程序的宿主，你可以控制和管理这些应用程序。 使用 "快速创建" 选项，可以从门户外部将已完成的 web 应用程序部署到 Azure。 它不包括设置数据库的步骤。

    ![使用 "快速创建" 创建新网站](whats-new-in-web-forms-in-aspnet-45/_static/image32.png "使用“快速创建”创建新网站")

    *使用 "快速创建" 创建新网站*
4. 请**等到新网站创建完毕。**
5. 创建网站后，单击 " **URL** " 列下的链接。 检查新网站是否正常工作。

    ![浏览到新网站](whats-new-in-web-forms-in-aspnet-45/_static/image33.png "浏览到新网站")

    *浏览到新网站*

    ![网站正在运行](whats-new-in-web-forms-in-aspnet-45/_static/image34.png "网站正在运行")

    *网站正在运行*
6. 返回到门户，并在 "**名称**" 列下单击网站的名称以显示管理页面。

    ![打开网站管理页](whats-new-in-web-forms-in-aspnet-45/_static/image35.png "打开网站管理页")

    *打开网站管理页*
7. 在 "**仪表板**" 页的 "**速览**" 部分下，单击 "**下载发布配置文件**" 链接。

    > [!NOTE]
    > *发布配置文件*包含为每个已启用的发布方法将 web 应用程序发布到 Azure 所需的所有信息。 发布配置文件包含有连接到并且验证该发布方法启用的每个端点所需的 URL、用户凭据和数据库字符串。 **Microsoft WebMatrix 2**、 **Microsoft Visual Studio Express for Web**和**Microsoft Visual Studio 2012**支持读取发布配置文件，以便自动配置这些程序以将 Web 应用程序发布到 Azure。

    ![下载网站发布配置文件](whats-new-in-web-forms-in-aspnet-45/_static/image36.png "下载网站发布配置文件")

    *下载网站发布配置文件*
8. 将发布配置文件下载到已知位置。 在本练习中，你将了解如何使用此文件从 Visual Studio 将 web 应用程序发布到 Azure。

    ![正在保存发布配置文件](whats-new-in-web-forms-in-aspnet-45/_static/image37.png "正在保存发布配置文件")

    *正在保存发布配置文件*

<a id="ApxBTask2"></a>

<a id="Task_2_-_Configuring_the_Database_Server"></a>
#### <a name="task-2---configuring-the-database-server"></a>任务 2-配置数据库服务器

如果应用程序使用 SQL Server 数据库，则需要创建 SQL 数据库服务器。 如果要部署不使用 SQL Server 的简单应用程序，则可以跳过此任务。

1. 你将需要一个用于存储应用程序数据库的 SQL 数据库服务器。 可以在 Azure 管理门户中的**sql** **数据库 | server** | **服务器的仪表板**上的 Azure 管理门户中查看 sql 数据库服务器。 如果尚未创建服务器，可以使用命令栏上的 "**添加**" 按钮创建一个服务器。 记下**服务器名称和 URL、管理员登录名和密码**，因为你将在后续任务中使用它们。 请不要创建数据库，因为它将在后面的阶段创建。

    ![SQL 数据库服务器仪表板](whats-new-in-web-forms-in-aspnet-45/_static/image38.png "SQL 数据库服务器仪表板")

    *SQL 数据库服务器仪表板*
2. 在下一任务中，您将从 Visual Studio 测试数据库连接，因此，需要在服务器的**允许 IP 地址**列表中包含本地 ip 地址。 为此，请单击 "**配置**"，从 "**当前客户端 IP 地址**" 中选择 IP 地址，并将其粘贴到 "**起始 Ip 地址**" 和 "**结束 ip 地址**" 文本框，然后单击 "![添加-客户端-IP 地址-](whats-new-in-web-forms-in-aspnet-45/_static/image39.png)" 按钮。

    ![添加客户端 IP 地址](whats-new-in-web-forms-in-aspnet-45/_static/image40.png)

    *添加客户端 IP 地址*
3. 将**客户端 Ip 地址**添加到 "允许的 IP 地址" 列表中后，单击 "**保存**" 以确认更改。

    ![确认更改](whats-new-in-web-forms-in-aspnet-45/_static/image41.png)

    *确认更改*

<a id="ApxBTask3"></a>

<a id="Task_3_-_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
#### <a name="task-3---publishing-an-aspnet-mvc-4-application-using-web-deploy"></a>任务 3-使用 Web 部署发布 ASP.NET MVC 4 应用程序

1. 返回到 ASP.NET MVC 4 解决方案。 在**解决方案资源管理器**中，右键单击网站项目，然后选择 "**发布**"。

    ![发布应用程序](whats-new-in-web-forms-in-aspnet-45/_static/image42.png "发布应用程序")

    *发布网站*
2. 导入您在第一个任务中保存的发布配置文件。

    ![导入发布配置文件](whats-new-in-web-forms-in-aspnet-45/_static/image43.png "导入发布配置文件")

    *导入发布配置文件*
3. 单击 "**验证连接**"。 验证完成后，单击 "**下一步**"。

    > [!NOTE]
    > 验证完成后，"验证连接" 按钮旁边会出现一个绿色的复选标记。

    ![正在验证连接](whats-new-in-web-forms-in-aspnet-45/_static/image44.png "正在验证连接")

    *正在验证连接*
4. 在 "**设置**" 页的 "**数据库**" 部分下，单击数据库连接的文本框旁边的按钮（即**DefaultConnection**）。

    ![Web 部署配置](whats-new-in-web-forms-in-aspnet-45/_static/image45.png "Web 部署配置")

    *Web 部署配置*
5. 按如下所示配置数据库连接：

   - 在 "**服务器名称**" 中，键入您的 SQL 数据库服务器 URL，使用*tcp：* prefix。
   - 在 "**用户名**" 中键入服务器管理员登录名。
   - 在 "**密码**" 中键入服务器管理员登录密码。
   - 键入新的数据库名称。

     ![正在配置目标连接字符串](whats-new-in-web-forms-in-aspnet-45/_static/image46.png "正在配置目标连接字符串")

     *正在配置目标连接字符串*
6. 然后单击 **“确定”** 。 系统提示创建数据库时，单击 **"是"** 。

    ![创建数据库](whats-new-in-web-forms-in-aspnet-45/_static/image47.png "创建数据库字符串")

    *创建数据库*
7. 将用于连接到 Azure 中的 SQL 数据库的连接字符串显示在 "默认连接" 文本框中。 再单击 **“下一步”** 。

    ![指向 SQL 数据库的连接字符串](whats-new-in-web-forms-in-aspnet-45/_static/image48.png "指向 SQL 数据库的连接字符串")

    *指向 SQL 数据库的连接字符串*
8. 在 "**预览**" 页上，单击 "**发布**"。

    ![发布 web 应用程序](whats-new-in-web-forms-in-aspnet-45/_static/image49.png "发布 web 应用程序")

    *发布 web 应用程序*
9. 发布过程完成后，您的默认浏览器将打开已发布的网站。

<a id="AppendixC"></a>

<a id="Appendix_C_Using_Code_Snippets"></a>
## <a name="appendix-c-using-code-snippets"></a>附录 C：使用代码片段

使用代码片段，您可以随时获得所需的全部代码。 实验室文档将告诉你何时可以使用它们，如下图所示。

![使用 Visual Studio code 代码段将代码插入到项目中](whats-new-in-web-forms-in-aspnet-45/_static/image50.png "使用 Visual Studio code 代码段将代码插入到项目中")

*使用 Visual Studio code 代码段将代码插入到项目中*

***使用键盘添加代码片段（C#仅限）***

1. 将光标放在要插入代码的位置。
2. 开始键入代码片段名称（不含空格或连字符）。
3. 请注意，IntelliSense 显示匹配的代码段名称。
4. 选择正确的代码段（或保留键入内容，直到选择了整个代码段的名称）。
5. 按 Tab 键两次，将代码段插入到光标位置。

![开始键入代码片段名称](whats-new-in-web-forms-in-aspnet-45/_static/image51.png "开始键入代码片段名称")

*开始键入代码片段名称*

![按 Tab 键以选择突出显示的代码段](whats-new-in-web-forms-in-aspnet-45/_static/image52.png "按 Tab 键以选择突出显示的代码段")

*按 Tab 键以选择突出显示的代码段*

![再次按 Tab 键，代码片段将展开](whats-new-in-web-forms-in-aspnet-45/_static/image53.png "再次按 Tab 键，代码片段将展开")

*再次按 Tab 键，代码片段将展开*

***使用鼠标添加代码片段（C#、Visual Basic 和 XML）*** 2. 右键单击要插入代码片段的位置。

1. 选择 "**插入**代码片段"，然后选择 **"我的代码片段"** 。
2. 通过单击从列表中选择相关的代码片段。

![右键单击要插入代码片段的位置，然后选择 "插入代码片段"](whats-new-in-web-forms-in-aspnet-45/_static/image54.png "右键单击要插入代码片段的位置，然后选择 "插入代码片段"")

*右键单击要插入代码片段的位置，然后选择 "插入代码片段"*

![通过单击从列表中选择相关的代码片段](whats-new-in-web-forms-in-aspnet-45/_static/image55.png "通过单击从列表中选择相关的代码片段")

*通过单击从列表中选择相关的代码片段*
