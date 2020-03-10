---
uid: web-pages/overview/ui-layouts-and-themes/18-customizing-site-wide-behavior
title: 为 ASP.NET 网页（Razor）站点自定义站点范围的行为 |Microsoft Docs
author: Rick-Anderson
description: 本章介绍如何将设置设置到整个网站或整个文件夹，而不只是一个页面。
ms.author: riande
ms.date: 02/17/2014
ms.assetid: e158bed7-226f-4275-b02e-7553bd58c669
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/18-customizing-site-wide-behavior
msc.type: authoredcontent
ms.openlocfilehash: f05e05f725d9209bce283ce18659ae5efe4de2ee
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78515246"
---
# <a name="customizing-site-wide-behavior-for-aspnet-web-pages-razor-sites"></a>为 ASP.NET 网页（Razor）站点自定义站点范围的行为

作者： [Tom FitzMacken](https://github.com/tfitzmac)

> 本文介绍如何在 ASP.NET 网页（Razor）网站中进行页面的站点端设置。
> 
> 学习内容：
> 
> - 如何运行代码，使您可以为站点中的所有页面设置值（全局值或帮助设置）。
> - 如何运行代码，使你可以为文件夹中的所有页面设置值。
> - 如何在页面加载之前和之后运行代码。
> - 如何将错误发送到中央错误页。
> - 如何将身份验证添加到文件夹中的所有页。
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>本教程中使用的软件版本
> 
> 
> - ASP.NET 网页（Razor）2
> - WebMatrix 3
> - ASP.NET Web 帮助程序库（NuGet 包）
>   
> 
> 本教程还适用于 ASP.NET 网页3和 Visual Studio 2013 （对于 Web 为 Visual Studio Express 2013），但不能使用 ASP.NET Web 帮助程序库。

<a id="Adding_Website_Startup_Code"></a>
## <a name="adding-website-startup-code-for-aspnet-web-pages"></a>为 ASP.NET 网页添加网站启动代码

对于在 ASP.NET 网页中编写的大部分代码，单个页面可以包含该页所需的所有代码。 例如，如果页面发送电子邮件，则可以将该操作的所有代码都放在一个页面中。 这可能包括用于初始化用于发送电子邮件的设置（即 SMTP 服务器）以及用于发送电子邮件的代码。

但是，在某些情况下，你可能需要在运行站点上的任何页面之前运行一些代码。 这对于设置可以在站点中的任何位置使用的值（称为*全局值*）很有用。例如，某些帮助程序要求你提供电子邮件设置或帐户密钥之类的值。 可以方便地将这些设置保存到全局值中。

为此，可以在站点的根目录中创建一个名为 *\_AppStart*的页。 如果此页面存在，则会在请求站点中的任何页面时首次运行。 因此，它是运行代码以设置全局值的好时机。 （由于 *\_AppStart*具有下划线前缀，因此 ASP.NET 不会将页面发送到浏览器，即使用户直接请求它也是如此。）

下图显示了 *\_AppStart*页面的工作方式。 当请求进入某个页面，并且这是对站点中任何页面的第一个请求时，ASP.NET 首先检查是否存在 *\_AppStart*的页面。 如果是这样，则 *\_AppStart* "页中的任何代码都将运行，然后将运行请求的页面。

![[图像]](18-customizing-site-wide-behavior/_static/image1.jpg)

## <a name="setting-global-values-for-your-website"></a>设置网站的全局值

1. 在 WebMatrix 网站的根文件夹中，创建一个名为 *\_AppStart*的文件。 文件必须位于站点的根目录中。
2. 将现有内容替换为以下内容： 

    [!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample1.cshtml)]

    此代码在 `AppState` 字典中存储一个值，此值可自动用于网站中的所有页。 请注意， *\_AppStart*文件中没有任何标记。 页面将运行代码，然后重定向到最初请求的页面。

    > [!NOTE]
    > 将代码放在 *\_AppStart*文件中时请小心。 如果 *\_AppStart*文件中的代码出现任何错误，网站将无法启动。
3. 在根文件夹中，创建一个名为*AppName. cshtml*的新页。
4. 将默认标记和代码替换为以下代码： 

    [!code-html[Main](18-customizing-site-wide-behavior/samples/sample2.html)]

    此代码从在 *\_AppStart*页面中设置的 `AppState` 对象中提取值。
5. 在浏览器中运行*AppName. cshtml*页面。 （请确保在运行之前在 "**文件**" 工作区中选择了该页面。）该页显示全局值。 

    ![[图像]](18-customizing-site-wide-behavior/_static/image2.jpg)

<a id="Setting_Values_For_Helpers"></a>
## <a name="setting-values-for-helpers"></a>为帮助器设置值

*\_AppStart*文件的一个不错用途是为你在站点中使用的帮助程序设置值，并且必须进行初始化。 典型示例是 `WebMail` 帮助程序的电子邮件设置，以及 `ReCaptcha` 帮助程序的私钥和公钥。 在这种情况下，可以在 *\_AppStart*中设置值一次，然后为站点中的所有页面设置这些值。

此过程说明如何全局设置 `WebMail` 设置。 （有关使用 `WebMail` 帮助器的详细信息，请参阅向[ASP.NET 网页网站添加电子邮件](../getting-started/11-adding-email-to-your-web-site.md)。）

1. 如在[ASP.NET 网页站点中安装帮助程序](https://go.microsoft.com/fwlink/?LinkId=252372)中所述，将 ASP.NET Web 帮助程序库添加到你的网站中（如果尚未添加）。
2. 如果还没有 *\_AppStart*文件，请在网站的根文件夹中创建一个名为 *\_AppStart*的文件。
3. 将以下 `WebMail` 设置添加到 *\_AppStart*文件中： 

    [!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample3.cshtml?highlight=2-7)]

    在代码中修改以下与电子邮件相关的设置：

   - 将 `your-SMTP-host` 设置为你有权访问的 SMTP 服务器的名称。
   - 将 `your-user-name-here` 设置为 SMTP 服务器帐户的用户名。
   - 将 `your-account-password` 设置为 SMTP 服务器帐户的密码。
   - 将 `your-email-address-here` 设置为你自己的电子邮件地址。 这是从其发送消息的电子邮件地址。 （某些电子邮件提供商不允许您指定其他 `From` 地址，并将使用您的用户名作为 `From` 地址。）

     有关 SMTP 设置的详细信息，请参阅在[从 ASP.NET 网页（razor）站点发送电子邮件](https://go.microsoft.com/fwlink/?LinkID=202899)中的[配置电子邮件设置](https://go.microsoft.com/fwlink/?LinkID=202899#configuring_email_settings)和[ASP.NET 网页（razor）故障排除指南](https://go.microsoft.com/fwlink/?LinkId=253001)中[发送电子邮件的问题](https://go.microsoft.com/fwlink/?LinkId=253001#email)。
4. 保存 *\_AppStart*文件并将其关闭。
5. 在网站的根文件夹中，创建名为*TestEmail*的新页面。
6. 将现有内容替换为以下内容： 

     [!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample4.cshtml)]
7. 在浏览器中运行*TestEmail*页。
8. 填写字段，向自己发送一封电子邮件，然后单击 "**发送**"。
9. 检查电子邮件以确保已收到该邮件。

此示例的重要部分是，不经常更改的设置（如 SMTP 服务器的名称和电子邮件凭据）在 *\_AppStart*文件中设置。 这样一来，就不需要在发送电子邮件的每个页面中再次设置它们。 （但是，如果出于某种原因，您需要更改这些设置，则可以在页面中单独设置它们。）在该页中，只设置通常每次更改的值，例如收件人和电子邮件的正文。

<a id="Running_Code_Before_and_After"></a>
## <a name="running-code-before-and-after-files-in-a-folder"></a>在文件夹中的文件之前和之后运行代码

正如你可以在站点运行的页面之前使用 *\_AppStart*来编写代码，你可以编写在特定文件夹运行的任何页面之前（和之后）运行的代码。 这对于为文件夹中的所有页面设置相同的布局页，或在运行文件夹中的页面之前检查用户是否登录都非常有用。

对于特定文件夹中的页面，可以在名为 *\_PageStart*的文件中创建代码。 下图显示了 *\_PageStart*页面的工作方式。 当请求进入某个页面时，ASP.NET 首先会检查 *\_AppStart* "页，并运行。 然后，ASP.NET 将检查是否存在 *\_PageStart*页，如果是，则运行该页。 然后，它将运行请求的页面。

在 *\_PageStart* "页中，可以通过包含 `RunPage` 方法来指定处理所需的页的处理过程中的位置。 这使您可以在请求的页运行之前运行代码，然后再次运行代码。 如果不包含 `RunPage`， *\_PageStart*中的所有代码都将运行，然后自动运行请求的页面。

![[图像]](18-customizing-site-wide-behavior/_static/image3.jpg)

ASP.NET 可让你创建 *\_PageStart*文件的层次结构。 可以将 *\_PageStart*文件放置在站点的根目录和任何子文件夹中。 请求页面时，位于最顶层的 *\_PageStart*文件（最接近站点根）将运行，后跟下一个子文件夹中的 *\_PageStart*文件，依此类推子文件夹结构，直到请求到达包含请求的页面的文件夹。 在所有适用的 *\_PageStart*文件都已运行之后，将运行请求的页面。

例如，你可能有以下 *\_PageStart*文件和*默认的*# # 文件的组合：

[!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample5.cshtml)]

[!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample6.cshtml)]

[!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample7.cshtml)]

运行 */myfolder/default.cshtml*时，将看到以下内容：

[!code-console[Main](18-customizing-site-wide-behavior/samples/sample8.cmd)]

## <a name="running-initialization-code-for-all-pages-in-a-folder"></a>为文件夹中的所有页面运行初始化代码

*\_PageStart*文件的一个不错用途是为一个文件夹中的所有文件初始化相同的布局页。

1. 在根文件夹中，创建一个名为*InitPages*的新文件夹。
2. 在网站的*InitPages*文件夹中，创建一个名为 *\_PageStart*的文件，并将默认标记和代码替换为以下代码： 

    [!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample9.cshtml)]
3. 在网站的根目录中，创建一个名为 "*共享*" 的文件夹。
4. 在*共享*文件夹中，创建一个名为 *\_Layout1*的文件，并将默认标记和代码替换为以下代码： 

    [!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample10.cshtml)]
5. 在*InitPages*文件夹中，创建一个名为*Content1*的文件，并将现有内容替换为以下内容： 

    [!code-html[Main](18-customizing-site-wide-behavior/samples/sample11.html)]
6. 在*InitPages*文件夹中，创建另一个名为*Content2*的文件，并将默认标记替换为以下内容： 

    [!code-html[Main](18-customizing-site-wide-behavior/samples/sample12.html)]
7. 在浏览器中运行*Content1* 。 

    ![[图像]](18-customizing-site-wide-behavior/_static/image4.jpg)

    *Content1*页运行时， *\_PageStart*文件将设置 `Layout` 并将 `PageData["MyBackground"]` 设置为颜色。 在*Content1*中，将应用布局和颜色。
8. 在浏览器中显示*Content2* 。 

    布局是相同的，因为这两个页使用 *\_PageStart*中的初始化的相同布局页和颜色。

## <a name="using-_pagestartcshtml-to-handle-errors"></a>使用 \_PageStart 处理错误

*\_PageStart*文件的另一种不错的用途是创建一种方法来处理可能出现在文件夹中的任何*cshtml*页面的编程错误（异常）。 此示例演示了执行此操作的一种方法。

1. 在根文件夹中，创建一个名为*InitCatch*的文件夹。
2. 在网站的*InitCatch*文件夹中，创建一个名为 *\_PageStart*的文件，并将现有标记和代码替换为以下代码： 

    [!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample13.cshtml)]

    在此代码中，你尝试通过调用 `try` 块内的 `RunPage` 方法来显式运行请求的页面。 如果请求的页面中出现任何编程错误，则会运行 `catch` 块中的代码。 在这种情况下，代码将重定向到页面（*错误. cshtml*），并将遇到错误的文件的名称作为 URL 的一部分传递。 （稍后会创建页面。）
3. 在网站的*InitCatch*文件夹中，创建一个名为*Exception*的文件，并将现有标记和代码替换为以下代码： 

    [!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample14.cshtml)]

    在此示例中，在此页中所做的工作是通过尝试打开不存在的数据库文件来特意创建一个错误。
4. 在根文件夹中，创建一个名为 "*错误*" 的文件，并将现有标记和代码替换为以下代码： 

    [!code-html[Main](18-customizing-site-wide-behavior/samples/sample15.html)]

    在此页中，表达式 `@Request["source"]` 获取 URL 的值并将其显示出来。
5. 在工具栏中，单击 "**保存**"。
6. 在浏览器中运行*Exception。* 

    ![[图像]](18-customizing-site-wide-behavior/_static/image5.jpg)

    由于*异常*中发生错误，因此 *\_PageStart*页面重定向到*错误 cshtml*文件，该文件将显示消息。

    有关异常的详细信息，请参阅[使用 Razor 语法 ASP.NET 网页编程简介](https://go.microsoft.com/fwlink/?LinkID=251587)。

<a id="Using__PageStart.cshtml_to_Restrict_Folder_Access"></a>
## <a name="using-_pagestartcshtml-to-restrict-folder-access"></a>使用 \_PageStart 来限制文件夹访问

你还可以使用 *\_PageStart*文件来限制对文件夹中所有文件的访问。

1. 在 WebMatrix 中，使用 "**从模板创建网站**" 选项创建新网站。
2. 从可用模板中选择 " **Starter Site**"。
3. 在根文件夹中，创建一个名为*AuthenticatedContent*的文件夹。
4. 在*AuthenticatedContent*文件夹中，创建一个名为 *\_PageStart*的文件，并将现有标记和代码替换为以下代码： 

    [!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample16.cshtml)]

    代码首先阻止缓存文件夹中的所有文件。 （对于公共计算机这样的方案是必需的，在这种情况下，你不希望向下一个用户提供一个用户的缓存页面。）接下来，该代码确定用户是否已登录到站点，然后才能查看文件夹中的任何页面。 如果用户未登录，则代码将重定向到登录页。 如果包含名为 "`ReturnUrl`" 的查询字符串值，登录页可能会将用户返回到最初请求的页面。
5. 在名为*AuthenticatedContent*的文件夹中创建一个新*页。*
6. 将默认标记替换为以下内容：  

    [!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample17.cshtml)]
7. 在浏览器中运行*页。* 该代码会将您重定向到登录页。 必须在登录前注册。 注册并登录后，可以导航到页面并查看其内容。

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a>其他资源

[使用 Razor 语法 ASP.NET 网页编程简介](https://go.microsoft.com/fwlink/?LinkID=251587)
