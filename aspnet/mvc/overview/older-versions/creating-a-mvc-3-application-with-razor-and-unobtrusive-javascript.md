---
uid: mvc/overview/older-versions/creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript
title: 使用 Razor 和非引人注目的 JavaScript 创建 MVC 3 应用程序 |Microsoft Docs
author: microsoft
description: 用户列表示例 web 应用程序演示了使用 Razor 视图引擎创建 ASP.NET MVC 3 应用程序的简单方法。 示例应用程序 。
ms.author: riande
ms.date: 11/01/2010
ms.assetid: 658b149b-d770-46bf-8b4b-4e47cca242f3
msc.legacyurl: /mvc/overview/older-versions/creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript
msc.type: authoredcontent
ms.openlocfilehash: fb63493ff22c9261fc5746a998a32f2511141f87
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78434996"
---
# <a name="creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript"></a>使用 Razor 和非介入性 JavaScript 创建 MVC 3 应用程序

by [Microsoft](https://github.com/microsoft)

> 用户列表示例 web 应用程序演示了使用 Razor 视图引擎创建 ASP.NET MVC 3 应用程序的简单方法。 该示例应用程序演示了如何将新的 Razor 视图引擎与 ASP.NET MVC 版本3和 Visual Studio 2010 一起使用，以创建包含创建、显示、编辑和删除用户等功能的虚拟用户列表网站。
> 
> 本教程介绍了生成用户列表示例 ASP.NET MVC 3 应用程序所采取的步骤。 本主题附带有与C#和 VB 源代码的 Visual Studio 项目：[下载](https://code.msdn.microsoft.com/aspnetmvcsamples/Release/ProjectReleases.aspx?ReleaseId=5114)。 如果你有关于本教程的问题，请将其发布到[MVC 论坛](https://forums.asp.net/1146.aspx)。

## <a name="overview"></a>概述

要构建的应用程序是一个简单的用户列表网站。 用户可以输入、查看和更新用户信息。

![示例站点](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image1.png)

可在此处下载 VB 和C#已完成[here](https://code.msdn.microsoft.com/Creating-a-MVC-3-28883c0f)的项目。

## <a name="creating-the-web-application"></a>创建 Web 应用程序

若要开始学习本教程，请打开 Visual Studio 2010 并使用 " *ASP.NET MVC 3 Web 应用程序*" 模板创建一个新项目。 将应用程序命名 &quot;Mvc3Razor&quot;。

[![新的 MVC 3 项目](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image3.png)](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image2.png)

在 "**新建 ASP.NET MVC 3 项目**" 对话框中，选择 " **Internet 应用程序**"，选择 "Razor" 视图引擎，然后单击 **"确定"** 。

![New ASP.NET MVC 3 项目对话框](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image4.png)

在本教程中，你将不使用 ASP.NET 成员资格提供程序，因此你可以删除与登录名和成员身份关联的所有文件。 在**解决方案资源管理器**中，删除以下文件和目录：

- *Controllers\AccountController*
- *Models\AccountModels*
- *Views\Shared\\_LogOnPartial*
- *Views\Account* （以及此目录中的所有文件）

![Soln Exp](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image5.png)

编辑<em>\_的布局 cshtml</em>文件，并<em>&quot;</em>将名为 `logindisplay` 的 `<div>` 元素内的标记替换为禁用了 "已禁用登录名"&quot;。 下面的示例显示了新标记：

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample1.cshtml)]

## <a name="adding-the-model"></a>添加模型

在**解决方案资源管理器**中，右键单击 "*模型*" 文件夹，选择 "**添加**"，然后单击 "**类**"。

![新用户 Mdl 类](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image6.png)

将此类命名为 `UserModel`。 将*UserModel*文件的内容替换为以下代码：

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample2.cs)]

`UserModel` 类表示用户。 类的每个成员都用[DataAnnotations](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx)命名空间中的[必需](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx)属性进行批注。 [DataAnnotations](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx)命名空间中的属性为 web 应用程序提供自动的客户端和服务器端验证。

打开 `HomeController` 类并添加 `using` 指令，以便可以访问 `UserModel` 和 `Users` 类：

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample3.cs)]

在 `HomeController` 声明的后面，添加以下注释和对 `Users` 类的引用：

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample4.cs)]

`Users` 类是一种简化的内存中数据存储区，你将在本教程中使用它。 在实际应用程序中，您将使用数据库来存储用户信息。 下面的示例演示了 `HomeController` 文件的前几行：

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample5.cs)]

构建应用程序，以便在下一步中将用户模型提供给基架向导使用。

## <a name="creating-the-default-view"></a>创建默认视图

下一步是添加操作方法和视图以显示用户。

删除现有的*Views\Home\Index*文件。 您将创建一个新的*索引*文件以显示用户。

在 `HomeController` 类中，将 `Index` 方法的内容替换为以下代码：

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample6.cs)]

在 `Index` 方法中右键单击，然后单击 "**添加视图**"。

![添加视图](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image7.png)

选择 "**创建强类型视图**" 选项。 对于 "**视图数据类**"，请选择**Mvc3Razor。 UserModel**。 （如果在 "**查看数据类**" 框中看不到**Mvc3Razor** ，则需要生成项目。）请确保 "视图引擎" 设置为 " **Razor**"。 将 "**查看内容**" 设置为 "**列表**"，然后单击 "**添加**"。

![添加索引视图](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image8.png)

新视图将自动基架传递到 `Index` 视图的用户数据。 检查新生成的*Views\Home\Index*文件。 "**新建**"、"**编辑**"、"**详细信息**" 和 "**删除**" 链接不起作用，但页面的其余部分都正常工作。 运行页面。 你将看到用户列表。

![索引页](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image9.png)

打开*索引.* # 文件，并将 "**编辑**"、"**详细信息**" 和 "**删除**" `ActionLink` 标记替换为以下代码：

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample7.cshtml)]

用户名用作 ID，以在 "**编辑**"、"**详细信息**" 和 "**删除**" 链接中查找所选记录。

## <a name="creating-the-details-view"></a>创建详细信息视图

下一步是添加 `Details` 操作方法和视图，以便显示用户详细信息。

![详细信息](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image10.png)

将以下 `Details` 方法添加到 home 控制器：

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample8.cs)]

在 `Details` 方法中右键单击，然后选择 "<strong>添加视图</strong>"。 验证 "<strong>查看数据类</strong>" 框是否包含<strong>Mvc3Razor。 UserModel</strong><em>。</em> 将 "<strong>查看内容</strong>" 设置为<strong>详细信息</strong>，然后单击 "<strong>添加</strong>"。

![添加详细信息视图](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image11.png)

运行应用程序并选择 "详细信息" 链接。 自动基架显示模型中的每个属性。

![详细信息](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image12.png)

## <a name="creating-the-edit-view"></a>创建编辑视图

将以下 `Edit` 方法添加到 home 控制器。

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample9.cs)]

按照前面的步骤添加视图，但将 "**查看内容**" 设置为 "**编辑**"。

![添加编辑视图](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image13.png)

运行应用程序，并编辑一个用户的名字和姓氏。 如果违反了已应用于 `UserModel` 类的任何 `DataAnnotation` 约束，则在提交窗体时，将会看到由服务器代码生成的验证错误。 例如，如果将王&quot; &quot;的名字改为 &quot;&quot;，则在提交窗体时，窗体上将显示以下错误：

`The field First Name must be a string with a minimum length of 3 and a maximum length of 8.`

在本教程中，你要将用户名视为主键。 因此，不能更改 "用户名" 属性。 在*编辑*`Html.BeginForm` 语句后，将用户名设置为隐藏的字段。 这将导致在模型中传递属性。 以下代码段显示了 `Hidden` 语句的位置：

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample10.cshtml)]

使用 `DisplayFor` 调用替换用户名的 `TextBoxFor` 和 `ValidationMessageFor` 标记。 `DisplayFor` 方法将属性显示为只读元素。 下面的示例演示了完整标记。 原始 `TextBoxFor` 和 `ValidationMessageFor` 调用被注释掉 Razor 开始注释和结束注释字符（`@* *@`）

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample11.cshtml)]

## <a name="enabling-client-side-validation"></a>启用客户端验证

若要在 ASP.NET MVC 3 中启用客户端验证，必须设置两个标志，并且必须包含三个 JavaScript 文件。

打开应用程序的*web.config 文件。* 在应用程序设置中验证 `that ClientValidationEnabled` 和 `UnobtrusiveJavaScriptEnabled` 是否设置为 true。 *根 web.config*文件中的以下片段显示了正确的设置：

[!code-xml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample12.xml)]

将 `UnobtrusiveJavaScriptEnabled` 设置为 true 可启用非引人注目的 Ajax 和不引人注目的客户端验证。 使用非介入式验证时，验证规则将被转换为 HTML5 属性。 HTML5 属性名称只能包含小写字母、数字和短划线。

将 `ClientValidationEnabled` 设置为 true 可启用客户端验证。 通过在应用程序的 web.config 文件中设置这些密钥，可为整个*应用程序启用*客户端验证和非引人注目的 JavaScript。 你还可以使用以下代码在各个视图或控制器方法中启用或禁用这些设置：

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample13.cs)]

还需要在呈现的视图中包含多个 JavaScript 文件。 在所有视图中包含 JavaScript 的简单方法是将其添加到*Views\Shared\\_Layout cshtml*文件中。 用以下代码替换 *\_布局*的 `<head>` 元素：

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample14.cshtml)]

前两个 jQuery 脚本由 Microsoft Ajax 内容交付网络（CDN）承载。 利用 Microsoft Ajax CDN，可以显著提高应用程序的第一次命中率。

运行应用程序，并单击 "编辑" 链接。 在浏览器中查看该页的源。 Browser source 显示了 `data-val` 格式（用于数据验证）的许多属性。 如果启用了客户端验证和非介入式 JavaScript，则具有客户端验证规则的输入字段将包含 `data-val="true"` 特性来触发非引人注目的客户端验证。 例如，模型中的 "`City`" 字段是用[Required](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx)属性修饰的，这将生成以下示例中所示的 HTML：

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample15.cshtml)]

对于每个客户端验证规则，会添加格式 `data-val-rulename="message"`的属性。 使用前面所示的 `City` 字段示例，必需的客户端验证规则生成 `data-val-required` 属性，&quot;City 字段&quot;消息。 运行应用程序，编辑用户之一，然后清除 "`City`" 字段。 当您通过 tab 键跳出字段时，您会看到客户端验证错误消息。

![需要城市](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image14.png)

同样，对于客户端验证规则中的每个参数，都会添加格式 `data-val-rulename-paramname=paramvalue`的属性。 例如，`FirstName` 属性使用[StringLength](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx)属性进行批注，并指定最小长度为3且最大长度为8。 名为 `length` 的数据验证规则的参数名称 `max` 和参数值8。 下面显示了在编辑用户之一时为 "`FirstName`" 字段生成的 HTML：

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample16.cshtml)]

有关非介入式客户端验证的详细信息，请参阅 Brad Wilson 博客中的[ASP.NET MVC 3 中的条目不引人注目的客户端验证](http://bradwilson.typepad.com/blog/2010/10/mvc3-unobtrusive-validation.html)。

> [!NOTE]
> 在 ASP.NET MVC 3 Beta 中，有时需要提交窗体以便启动客户端验证。 对于最终发布，这可能会发生更改。

## <a name="creating-the-create-view"></a>创建 "创建" 视图

下一步是添加 `Create` 操作方法和视图，以便使用户能够创建新用户。 将以下 `Create` 方法添加到 home 控制器：

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample17.cs)]

按照前面的步骤添加视图，但将 "**查看内容**" 设置为 "**创建**"。

![创建视图](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image15.png)

运行应用程序，选择 "**创建**" 链接，然后添加一个新用户。 `Create` 方法自动利用客户端和服务器端验证。 尝试输入包含空白的用户名，例如 &quot;Ben X&quot;。 当您从 "用户名" 字段中按 tab 键时，将显示客户端验证错误（`White space is not allowed`）。

## <a name="add-the-delete-method"></a>添加 Delete 方法

若要完成本教程，请将以下 `Delete` 方法添加到 home 控制器：

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample18.cs)]

如前面的步骤中所示，添加 "`Delete`" 视图，将 "**查看内容**" 设置为 "**删除**"。

![删除视图](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image16.png)

现在，你有了一个简单但功能完备的 ASP.NET MVC 3 应用程序，并具有验证。
