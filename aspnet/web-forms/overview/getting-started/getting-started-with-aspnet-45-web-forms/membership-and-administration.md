---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/membership-and-administration
title: 成员资格和管理 |Microsoft Docs
author: Erikre
description: 本系列教程将介绍使用 ASP.NET 4.5 构建 ASP.NET Web 窗体应用程序的基础知识，并为我们 Microsoft Visual Studio Express 2013 。
ms.author: riande
ms.date: 09/08/2014
ms.assetid: 732a2316-e49f-4f72-becd-0cd72f14457e
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/membership-and-administration
msc.type: authoredcontent
ms.openlocfilehash: ab00bc90bfc767d06e747be6dfb973245b5aae88
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74615474"
---
# <a name="membership-and-administration"></a>成员身份和管理

作者： [Erik Reitan](https://github.com/Erikre)

[下载 Wingtip 玩具示例项目（C#）](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409)或[下载电子书（PDF）](https://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)

> 本系列教程将介绍使用 ASP.NET 4.5 构建 ASP.NET Web 窗体应用程序的基础知识，并为 Web Microsoft Visual Studio Express 2013。 此教程系列附带有[ C#源代码](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409)的 Visual Studio 2013 项目。

本教程演示如何更新 Wingtip 玩具示例应用程序，以添加自定义角色并使用 ASP.NET Identity。 还介绍了如何实现一个管理页面，通过该页面，具有自定义角色的用户可以在网站中添加和删除产品。

[ASP.NET Identity](../../../../identity/overview/getting-started/introduction-to-aspnet-identity.md)是用于构建 ASP.NET web 应用程序的成员资格系统，在 ASP.NET 4.5 中提供。 ASP.NET Identity 用于 Visual Studio 2013 Web 窗体项目模板，以及用于[ASP.NET MVC](../../../../mvc/index.md)、 [ASP.NET Web API](../../../../web-api/index.md)和[ASP.NET 单页面应用程序](../../../../single-page-application/index.md)的模板。 你还可以在使用空白 Web 应用程序启动时，使用 NuGet 专门安装 ASP.NET Identity 系统。 但是，在本教程系列中，你将使用**Web 窗体**projecttemplate，其中包含 ASP.NET Identity 系统。 ASP.NET Identity 可以轻松地将特定于用户的配置文件数据与应用程序数据相集成。 此外，ASP.NET 标识允许你为应用程序中的用户配置文件选择持久模型。 你可以将数据存储在 SQL Server 数据库或其他数据存储中，包括*NoSQL*数据存储，如 Windows Azure 存储表。

本教程建立在 Wingtip 玩具教程系列标题为 "通过 PayPal 结帐和付款" 的前一教程中。

## <a name="what-youll-learn"></a>你将学习的内容：

- 如何使用代码将自定义角色和用户添加到应用程序。
- 如何限制对管理文件夹和页面的访问。
- 如何为属于自定义角色的用户提供导航。
- 如何使用模型绑定填充产品类别的[DropDownList](https://msdn.microsoft.com/library/system.web.ui.webcontrols.dropdownlist(v=vs.110).aspx)控件。
- 如何使用[FileUpload](https://msdn.microsoft.com/library/system.web.ui.webcontrols.fileupload(v=vs.110).aspx)控件将文件上传到 web 应用程序。
- 如何使用验证控件来实现输入验证。
- 如何在应用程序中添加和删除产品。

## <a name="these-features-are-included-in-the-tutorial"></a>本教程包括以下功能：

- ASP.NET 标识
- 配置和授权
- 模型绑定
- 非引人注目验证

ASP.NET Web 窗体提供成员资格功能。 通过使用默认模板，您可以使用内置成员资格功能，以便在应用程序运行时立即使用。 本教程演示如何使用 ASP.NET Identity 添加自定义角色并将用户分配给该角色。 你将了解如何限制对管理文件夹的访问。 你将向 "管理" 文件夹中添加一个页面，该页面允许具有自定义角色的用户添加和删除产品，以及在添加产品后预览产品。

## <a name="adding-a-custom-role"></a>添加自定义角色

使用 ASP.NET Identity，可以使用代码添加自定义角色并将用户分配给该角色。

1. 在**解决方案资源管理器**中，右键单击*逻辑*文件夹，然后创建新类。
2. 将新类命名为*RoleActions.cs*。
3. 修改代码，使其显示如下：  

    [!code-csharp[Main](membership-and-administration/samples/sample1.cs?highlight=8)]
4. 在**解决方案资源管理器**中，打开*Global.asax.cs*文件。
5. 通过添加黄色突出显示的代码来修改*Global.asax.cs*文件，使其显示如下：  

    [!code-csharp[Main](membership-and-administration/samples/sample2.cs?highlight=11,26-28)]
6. 请注意，`AddUserAndRole` 以红色下划线表示。 双击 "AddUserAndRole" 代码。  
   突出显示的方法开头的字母 "A" 将带有下划线。
7. 将鼠标悬停在该字母 "A" 上，并单击允许您为 `AddUserAndRole` 方法生成方法存根的 UI。 

    ![成员资格和管理-生成方法存根](membership-and-administration/_static/image1.png)
8. 单击标题为以下内容的选项：  
    `Generate method stub for "AddUserAndRole" in "WingtipToys.Logic.RoleActions"`
9. 从*逻辑*文件夹打开*RoleActions.cs*文件。  
   已将 `AddUserAndRole` 方法添加到了类文件中。
10. 通过删除 `NotImplementedException` 并添加以黄色突出显示的代码来修改*RoleActions.cs*文件，使其显示如下：  

    [!code-csharp[Main](membership-and-administration/samples/sample3.cs?highlight=5-7,15-51)]

上面的代码首先为成员资格数据库建立数据库上下文。 成员资格数据库还以 *.mdf*文件的形式存储在*应用\_Data*文件夹中。 第一个用户登录到此 web 应用程序后，你将能够查看此数据库。 

> [!NOTE] 
> 
> 如果希望将成员资格数据与产品数据一起存储，可以考虑使用在上面的代码中用于存储产品数据的相同**DbContext** 。

 *Internal*关键字是类型（如类）和类型成员（如方法或属性）的访问修饰符。 只能在同一程序集 *（.dll*文件）中包含的文件内访问内部类型或成员。 生成应用程序时，将创建一个程序集文件 *（.dll*），其中包含运行应用程序时执行的代码。 

提供角色管理的 `RoleStore` 对象基于数据库上下文创建。

> [!NOTE] 
> 
> 请注意，创建 `RoleStore` 对象时，它将使用泛型 `IdentityRole` 类型。 这意味着 `RoleStore` 只允许包含 `IdentityRole` 对象。 此外，通过使用泛型，可以更好地处理内存中的资源。

接下来，`RoleManager` 对象基于刚刚创建的 `RoleStore` 对象创建。 `RoleManager` 对象公开与角色相关的 API，可用于自动将更改保存到 `RoleStore`。 只允许 `RoleManager` 包含 `IdentityRole` 对象，因为代码使用 `<IdentityRole>` 的泛型类型。

调用 `RoleExists` 方法来确定成员资格数据库中是否存在 "canEdit" 角色。 如果不是，则创建角色。

创建 `UserManager` 对象显得比 `RoleManager` 控件更复杂，但几乎相同。 它只是在一行上编码，而不是在多行上编码。 此处，要传递的参数将实例化为括号中包含的新对象。

接下来，通过创建新的 `ApplicationUser` 对象创建 "canEditUser" 用户。 如果成功创建用户，请将该用户添加到新角色。

> [!NOTE] 
> 
> 本系列教程后面的 "ASP.NET 错误处理" 教程中将更新错误处理。

下一次启动应用程序时，会将名为 "canEditUser" 的用户添加为应用程序的名为 "canEdit" 的角色。 稍后在本教程中，你将以 "canEditUser" 用户身份登录，以显示你将在本教程中添加的其他功能。 有关 ASP.NET Identity 的 API 详细信息，请参阅 " [Microsoft Node.js 命名空间](https://msdn.microsoft.com/library/microsoft.aspnet.identity(v=vs.111).aspx)"。 有关初始化 ASP.NET Identity 系统的其他详细信息，请参阅[AspnetIdentitySample](https://github.com/rustd/AspnetIdentitySample/blob/master/AspnetIdentitySample/App_Start/IdentityConfig.cs)。

### <a name="restricting-access-to-the-administration-page"></a>限制对管理页的访问

Wingtip 玩具示例应用程序允许匿名用户和已登录用户查看和购买产品。 但是，具有自定义 "canEdit" 角色的已登录用户可以访问受限制的页面，以便添加和删除产品。

#### <a name="add-an-administration-folder-and-page"></a>添加管理文件夹和页面

接下来，你将为属于 Wingtip 玩具示例应用程序的自定义角色的 "canEditUser" 用户创建名为*Admin*的文件夹。

1. 在**解决方案资源管理器**中右键单击项目名称（**Wingtip 玩具**），然后选择 "**添加** -&gt;**新文件夹**"。
2. 将新文件夹命名为 "*管理员*"。
3. 右键单击 "*管理*" 文件夹，然后选择 "**添加** -&gt;**新项**"。   
   随即出现“添加新项”对话框。
4. 选择左侧的 " <strong>Visual C#</strong> -&gt; <strong>Web</strong>模板" 组。 从中间列表中，选择 "<strong>带有母版页的 Web 窗体</strong>"，将其命名为<em>AdminPage</em>，然后选择 "<strong>添加</strong><strong>"</strong> 。
5. 选择 "*网站*" 作为母版页的主文件，然后选择 **"确定"** 。

#### <a name="add-a-webconfig-file"></a>添加 web.config 文件

通过将*web.config*文件添加到*管理*文件夹，可以限制对文件夹中包含的页的访问。

1. 右键单击 "*管理*" 文件夹，然后选择 "**添加** -&gt;**新项**"。  
   随即出现“添加新项”对话框。
2. C#从 Visual web 模板列表中，从中间列表中选择 " <strong>web 配置文件</strong>"，接受 web.config 的默认<strong>名称，然后</strong>选择 "<strong>添加</strong>"。
3. *将 web.config 文件中*的现有 XML 内容替换为以下内容：  

    [!code-xml[Main](membership-and-administration/samples/sample4.xml)]

保存 web.config*文件。* Web.config*文件指定*只有属于应用程序的 "canEdit" 角色的用户才能访问*管理*文件夹中包含的页。

### <a name="including-custom-role-navigation"></a>包括自定义角色导航

若要使自定义 "canEdit" 角色的用户可以导航到应用程序的 "管理" 部分，必须将链接添加到*网站母版页*。 只有属于 "canEdit" 角色的用户才能看到 "**管理员**" 链接并访问 "管理" 部分。

1. 在解决方案资源管理器中，查找并打开 "*网站母版页*"。
2. 若要为 "canEdit" 角色的用户创建链接，请将黄色突出显示的标记添加 `<ul>` 元素，以便列表如下所示：  

    [!code-html[Main](membership-and-administration/samples/sample5.html?highlight=2-3)]
3. 打开*Site.Master.cs*文件。 通过将黄色突出显示的代码添加到 `Page_Load` 处理程序，使**管理员**链接仅对 "canEditUser" 用户可见。 `Page_Load` 处理程序将如下所示：   

    [!code-csharp[Main](membership-and-administration/samples/sample6.cs?highlight=3-6)]

加载页面时，代码会检查登录用户是否具有 "canEdit" 角色。 如果用户属于 "canEdit" 角色，则会使包含指向*AdminPage*页面的链接的 span 元素（进而使范围内的链接）变得可见。

### <a name="enabling-product-administration"></a>启用产品管理

到目前为止，您已经创建了 "canEdit" 角色并添加了 "canEditUser" 用户、管理文件夹和管理页面。 已为管理文件夹和页面设置访问权限，并已将 "canEdit" 角色的用户的导航链接添加到了应用程序。 接下来，您将向*AdminPage*页和代码添加标记，将其添加到*AdminPage.aspx.cs*代码隐藏文件中，该文件允许具有 "canEdit" 角色的用户添加和删除产品。

1. 在**解决方案资源管理器**中，打开*管理*文件夹中的*AdminPage*文件。
2. 将现有标记替换为以下内容：  

    [!code-aspx[Main](membership-and-administration/samples/sample7.aspx)]
3. 接下来，通过右键单击 " *AdminPage* " 并单击 "**查看代码**" 来打开*AdminPage.aspx.cs*代码隐藏文件。
4. 将*AdminPage.aspx.cs*代码隐藏文件中的现有代码替换为以下代码：  

    [!code-csharp[Main](membership-and-administration/samples/sample8.cs)]

在为*AdminPage.aspx.cs*代码隐藏文件输入的代码中，名为 `AddProducts` 的类将执行将产品添加到数据库的实际工作。 此类尚不存在，因此你现在会创建它。

1. 在**解决方案资源管理器**中，右键单击*逻辑*文件夹，然后选择 "**添加** -&gt;**新项**"。   
   随即出现“添加新项”对话框。
2. 选择左侧的 " **Visual C#**  -&gt;**代码**模板" 组。 然后，从中间列表中选择 "**类**"，并将其命名为*AddProducts.cs*。   
   将显示新的类文件。
3. 将现有代码替换为以下代码：  

    [!code-csharp[Main](membership-and-administration/samples/sample9.cs)]

*AdminPage*页允许属于 "canEdit" 角色的用户添加和删除产品。 添加新产品后，将验证有关该产品的详细信息，并将其输入到数据库中。 新产品立即可供 web 应用程序的所有用户使用。

#### <a name="unobtrusive-validation"></a>非引人注目验证

用户在*AdminPage*页上提供的产品详细信息使用验证控件（`RequiredFieldValidator` 和 `RegularExpressionValidator`）进行验证。 这些控件会自动使用不引人注目的验证。 非介入式验证允许验证控件将 JavaScript 用于客户端验证逻辑，这意味着该页不需要与服务器进行验证。 默认情况下，基于以下配置设置，不引人注目的验证包含在*web.config 文件中*：

[!code-xml[Main](membership-and-administration/samples/sample10.xml)]

#### <a name="regular-expressions"></a>正则表达式

使用**RegularExpressionValidator**控件验证*AdminPage*页上的产品价格。 此控件验证关联的输入控件（"AddProductPrice" 文本框）的值是否与正则表达式指定的模式匹配。 正则表达式是模式匹配表示法，可用于快速查找和匹配特定字符模式。 **RegularExpressionValidator**控件包含一个名为 `ValidationExpression` 的属性，该属性包含用于验证价格输入的正则表达式，如下所示：

[!code-aspx[Main](membership-and-administration/samples/sample11.aspx)]

#### <a name="fileupload-control"></a>FileUpload 控件

除了输入和验证控件外，还可以将**FileUpload**控件添加到*AdminPage*页。 此控件提供上传文件的功能。 在这种情况下，只允许上传图像文件。 在代码隐藏文件（*AdminPage.aspx.cs*）中，单击 `AddProductButton` 时，代码会检查**FileUpload**控件的 `HasFile` 属性。 如果控件包含文件，并且允许文件类型（基于文件扩展名），则图像将保存到*images*文件夹和应用程序的*images/拇指*文件夹中。

#### <a name="model-binding"></a>模型绑定

在本教程的前面部分，你使用了模型绑定来填充**ListView**控件、 **FormsView**控件、 **GridView**控件和**DetailView**控件。 在本教程中，您将使用模型绑定来用产品类别列表填充**DropDownList**控件。

添加到*AdminPage*文件的标记包含名为 `DropDownAddCategory`的**DropDownList**控件：

[!code-aspx[Main](membership-and-administration/samples/sample12.aspx)]

通过设置 `ItemType` 特性和 `SelectMethod` 特性，可以使用模型绑定来填充此**DropDownList** 。 `ItemType` 特性指定在填充控件时使用 `WingtipToys.Models.Category` 类型。 可以通过创建 `Category` 类（如下所示）在本教程系列的开头定义此类型。 `Category` 类位于*Category.cs*文件中的 "*模型*" 文件夹内。

[!code-csharp[Main](membership-and-administration/samples/sample13.cs)]

**DropDownList**控件的 `SelectMethod` 特性指定你使用代码隐藏文件（*AdminPage.aspx.cs*）中包含的 `GetCategories` 方法（如下所示）。

[!code-csharp[Main](membership-and-administration/samples/sample14.cs)]

此方法指定使用 `IQueryable` 接口来计算针对 `Category` 类型的查询。 返回的值用于填充页面标记中的**DropDownList** （*AdminPage*）。

为列表中的每个项显示的文本通过设置 `DataTextField` 特性来指定。 `DataTextField` 属性使用 `Category` 类的 `CategoryName` （如上所示）显示**DropDownList**控件中的每个类别。 在**DropDownList**控件中选择项时所传递的实际值基于 `DataValueField` 特性。 `DataValueField` 特性设置为 `CategoryID` 在 `Category` 类中为 define （如上所示）。

### <a name="how-the-application-will-work"></a>应用程序的工作原理

当属于 "canEdit" 角色的用户第一次导航到页面时，将按照上述说明填充 `DropDownAddCategory`**DropDownList**控件。 `DropDownRemoveProduct`**DropDownList**控件也使用相同的方法填充产品。 属于 "canEdit" 角色的用户选择类别类型并添加产品详细信息（**名称**、**说明**、**价格**和**图像文件**）。 当属于 "canEdit" 角色的用户单击 "**添加产品**" 按钮时，将触发 `AddProductButton_Click` 事件处理程序。 位于代码隐藏文件（*AdminPage.aspx.cs*）中的 `AddProductButton_Click` 事件处理程序将检查映像文件，以确保它与允许的文件类型 *（.gif*、 *.png*、 *jpeg*或 *.jpg*）相匹配。 然后，将图像文件保存到 Wingtip 玩具示例应用程序的文件夹中。 接下来，将新产品添加到数据库中。 为了实现新的产品，将创建 `AddProducts` 类的新实例，并将其命名为 "产品"。 `AddProducts` 类具有一个名为 `AddProduct`的方法，products 对象调用此方法将产品添加到数据库中。

[!code-csharp[Main](membership-and-administration/samples/sample15.cs)]

如果代码成功将新产品添加到数据库，则会重新加载该页面，并 `ProductAction=add`查询字符串值。

[!code-csharp[Main](membership-and-administration/samples/sample16.cs)]

重新加载页面时，查询字符串将包含在 URL 中。 通过重新加载页面，属于 "canEdit" 角色的用户可以立即在*AdminPage*页面上的**DropDownList**控件中查看更新。 此外，通过在 URL 中包含查询字符串，页面可以向属于 "canEdit" 角色的用户显示一条成功消息。

当*AdminPage*页重新加载时，将调用 `Page_Load` 事件。

[!code-csharp[Main](membership-and-administration/samples/sample17.cs)]

`Page_Load` 事件处理程序检查查询字符串值，并确定是否显示成功消息。

## <a name="running-the-application"></a>运行应用程序

现在可以运行应用程序，了解如何添加、删除和更新购物车中的项目。 购物车总计将反映购物车中所有物品的总成本。

1. 在解决方案资源管理器中，按**F5**运行 Wingtip 玩具示例应用程序。  
   浏览器将打开并显示*default.aspx*页。
2. 单击页面顶部的 "**登录**" 链接。 

    ![成员身份和管理-登录链接](membership-and-administration/_static/image2.png)

   将显示*登录 .aspx*页。
3. 使用以下用户名和密码：  
   用户名： canEditUser@wingtiptoys.com  
   密码： Pa $ $word 1 

    ![成员资格和管理-登录页](membership-and-administration/_static/image3.png)
4. 单击页面底部附近的 "**登录**" 按钮。
5. 在下一页的顶部，选择 "**管理**" 链接以导航到 " *AdminPage* " 页。 

    ![成员身份和管理-管理链接](membership-and-administration/_static/image4.png)
6. 若要测试输入验证，请单击 "**添加产品**" 按钮，而不添加任何产品详细信息。 

    ![成员资格和管理-管理页面](membership-and-administration/_static/image5.png)

   请注意，将显示必填字段消息。
7. 为新产品添加详细信息，然后单击 "**添加产品**" 按钮。 

    ![成员资格和管理-添加产品](membership-and-administration/_static/image6.png)
8. 从顶部导航菜单中选择 "**产品**"，以查看添加的新产品。 

    ![成员资格和管理-显示新产品](membership-and-administration/_static/image7.png)
9. 单击 "**管理**" 链接以返回到 "管理" 页。
10. 在页面的 "**删除产品**" 部分中，选择在**DropDownListBox**中添加的新产品。
11. 单击 "**删除产品**" 按钮，从应用程序中删除新产品。 

    ![成员资格和管理-删除产品](membership-and-administration/_static/image8.png)
12. 从顶部导航菜单中选择 "**产品**"，确认已删除该产品。
13. 单击 "**注销**" 以存在管理模式。   
    请注意，顶部导航窗格不再显示 "**管理**" 菜单项。

## <a name="summary"></a>总结

在本教程中，你添加了一个自定义角色和一个属于该自定义角色的用户、对管理文件夹和页面的有限访问权限，并为属于该自定义角色的用户提供了导航。 你使用了模型绑定来用数据填充**DropDownList**控件。 实现了**FileUpload**控件和验证控件。 此外，您还了解了如何在数据库中添加和删除产品。 在下一教程中，你将学习如何实现 ASP.NET 路由。

## <a name="additional-resources"></a>其他资源

[Web.config-authorization 元素](https://msdn.microsoft.com/library/8d82143t(v=vs.100).aspx)  
[ASP.NET Identity](../../../../identity/overview/getting-started/introduction-to-aspnet-identity.md)  
[使用成员资格、OAuth 和 SQL 数据库将安全的 ASP.NET Web 窗体应用程序部署到 Azure 网站](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-webforms-app-membership-oauth-sql-database/)  
[Microsoft Azure 免费试用版](https://azure.microsoft.com/pricing/free-trial/)

> [!div class="step-by-step"]
> [上一页](checkout-and-payment-with-paypal.md)
> [下一页](url-routing.md)
