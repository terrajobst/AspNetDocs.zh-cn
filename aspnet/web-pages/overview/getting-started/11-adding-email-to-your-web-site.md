---
uid: web-pages/overview/getting-started/11-adding-email-to-your-web-site
title: 从 ASP.NET 网页（Razor）站点发送电子邮件 |Microsoft Docs
author: Rick-Anderson
description: 本章介绍如何从网站发送自动电子邮件。
ms.author: riande
ms.date: 02/20/2014
ms.assetid: fc49bcb9-f1a9-4048-8c3f-b60951853200
msc.legacyurl: /web-pages/overview/getting-started/11-adding-email-to-your-web-site
msc.type: authoredcontent
ms.openlocfilehash: 23e9717329525fb5a0ed505c9dc94505d4f9dbbe
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78515324"
---
# <a name="sending-email-from-an-aspnet-web-pages-razor-site"></a>从 ASP.NET 网页（Razor）站点发送电子邮件

作者： [Tom FitzMacken](https://github.com/tfitzmac)

> 本文介绍如何在使用 ASP.NET 网页（Razor）时从网站发送电子邮件。
> 
> 学习内容：
> 
> - 如何从网站发送电子邮件。
> - 如何将文件附加到电子邮件。
> 
> 这是本文中介绍的 ASP.NET 功能：
> 
> - `WebMail` 帮助程序。
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>本教程中使用的软件版本
> 
> 
> - ASP.NET 网页（Razor）3
>   
> 
> 本教程还适用于 ASP.NET 网页2。

<a id="Sending_Email_Messages"></a>
## <a name="sending-email-messages-from-your-website"></a>从网站发送电子邮件

可能需要从网站发送电子邮件的原因有多种。 您可以向用户发送确认消息，也可以向自己发送通知（例如，新用户已注册。）利用 `WebMail` 帮助程序，你可以轻松地发送电子邮件。

若要使用 `WebMail` 帮助程序，你必须具有对 SMTP 服务器的访问权限。 （SMTP 代表*简单邮件传输协议*。）SMTP 服务器是一种电子邮件服务器，只向收件人的服务器&#8212;转发邮件，它是电子邮件的出站端。 如果你为网站使用托管提供程序，他们可能会将你设置为电子邮件，并可以告诉你你的 SMTP 服务器名称。 如果你在公司网络内工作，则管理员或你的 IT 部门通常可以向你显示有关你可以使用的 SMTP 服务器的信息。 如果在家工作，您甚至可以使用普通的电子邮件提供程序进行测试，用户可以告诉您 SMTP 服务器的名称。 通常需要：

- SMTP 服务器的名称。
- 端口号。 这几乎始终为25。 但是，ISP 可能要求使用端口587。 如果为电子邮件使用安全套接字层（SSL），则可能需要不同的端口。 请咨询你的电子邮件提供商。
- 凭据（用户名和密码）。

在此过程中，您将创建两个页面。 第一页提供了一个窗体，用户可以在其中输入说明，就好像这些用户填写了技术支持窗体一样。 第一页将其信息提交到第二页。 在第二页中，代码提取用户的信息并发送一封电子邮件。 它还会显示一条消息，确认已接收到问题报告。

![[图像]](11-adding-email-to-your-web-site/_static/image1.jpg)

> [!NOTE]
> 为了使此示例简单，代码在使用它的页中初始化 `WebMail` 帮助程序。 但对于实际网站，最好将类似于下面的初始化代码置于全局文件中，以便为网站中的所有文件初始化 `WebMail` 帮助程序。 有关详细信息，请参阅[为 ASP.NET 网页自定义站点范围的行为](https://go.microsoft.com/fwlink/?LinkId=202906#Setting_Values_For_Helpers)。

1. 创建新网站。
2. 添加一个名为*EmailRequest*的新页面并添加以下标记： 

    [!code-html[Main](11-adding-email-to-your-web-site/samples/sample1.html)]

    请注意，窗体元素的 `action` 属性已设置为*ProcessRequest*。 这意味着表单将提交到该页面，而不是返回到当前页面。
3. 将名为*ProcessRequest*的新页添加到网站，并添加以下代码和标记：   

    [!code-cshtml[Main](11-adding-email-to-your-web-site/samples/sample2.cshtml)]

    在代码中，你将获取提交到页面的窗体字段的值。 然后调用 `WebMail` 帮助器的 `Send` 方法来创建和发送电子邮件。 在这种情况下，要使用的值由与从窗体提交的值连接的文本组成。

    此页的代码位于 `try/catch` 块内。 如果出于任何原因而无法发送电子邮件，则无法正常工作（例如，设置不正确），`catch` 块中的代码将运行，并将 `errorMessage` 变量设置为发生的错误。 （有关 `try/catch` 块或 `<text>` 标记的详细信息，请参阅[使用 Razor 语法 ASP.NET 网页编程简介](https://go.microsoft.com/fwlink/?LinkID=251587#ID_HandlingErrors)。）

    在页面的正文中，如果 `errorMessage` 变量为空（默认值），则用户将看到一条消息，指出电子邮件已发送。 如果 `errorMessage` 变量设置为 true，则用户将看到一条消息，指出发送消息时出现问题。

    请注意，在显示错误消息的页面部分中有一个额外的测试： `if(debuggingFlag)`。 如果在发送电子邮件时遇到问题，则可以将此变量设置为 true。 如果 `debuggingFlag` 为 true，并且在发送电子邮件时出现问题，将显示一条额外的错误消息，其中显示了在尝试发送电子邮件时报告的任何 ASP.NET。 但会出现公平警告： ASP.NET 报告无法发送电子邮件的错误消息可以是通用的。 例如，如果 ASP.NET 无法联系 SMTP 服务器（例如，因为服务器名称中出现错误），则会 `Failure sending mail`错误。

    > [!NOTE] 
    > 
    > **重要提示**从异常对象（在代码中为`ex`）收到错误消息时，*不要定期将*该消息传递给用户。 异常对象通常包含用户不应该看到的信息，甚至是安全漏洞。 这就是为什么此代码包含变量 `debuggingFlag` 用于显示错误消息的开关，并且默认情况下变量设置为 false。 仅当你在发送电子邮件时遇到问题并且需要进行调试时，*才*应将此变量设置为 true （因此显示错误消息）。 解决所有问题后，将 `debuggingFlag` 设置回 false。

    在代码中修改以下与电子邮件相关的设置：

   - 将 `your-SMTP-host` 设置为你有权访问的 SMTP 服务器的名称。
   - 将 `your-user-name-here` 设置为 SMTP 服务器帐户的用户名。
   - 将 `your-account-password` 设置为 SMTP 服务器帐户的密码。
   - 将 `your-email-address-here` 设置为你自己的电子邮件地址。 这是从其发送消息的电子邮件地址。 （某些电子邮件提供商不允许您指定其他 `From` 地址，并将使用您的用户名作为 `From` 地址。）

     > [!TIP] 
     > 
     > <a id="configuring_email_settings"></a>
     > ### <a name="configuring-email-settings"></a>配置电子邮件设置
     > 
     > 有时需要确保对 SMTP 服务器和端口号等设置正确的设置，这可能是一项挑战。 下面是一些提示：
     > 
     > - SMTP 服务器名称通常类似于 `smtp.provider.com` 或 `smtp.provider.net`。 但是，如果将网站发布到宿主提供程序，此时可能会 `localhost`该点的 SMTP 服务器名称。 这是因为，在发布并在提供程序的服务器上运行站点后，电子邮件服务器可能从应用程序的角度来看是本地的。 服务器名称中的这一更改可能意味着你必须在发布过程中更改 SMTP 服务器名称。
     > - 端口号通常为25。 但是，某些提供程序要求使用端口587或其他端口。
     > - 请确保使用正确的凭据。 如果你已将站点发布到托管提供商，请使用提供商专门指出的凭据来发送电子邮件。 它们可能与发布所用的凭据不同。
     > - 有时你根本不需要凭据。 如果你使用个人 ISP 发送电子邮件，则电子邮件提供商可能已知道你的凭据。 发布后，可能需要使用不同于在本地计算机上进行测试时使用的凭据。
     > - 如果电子邮件提供程序使用加密，则必须将 `WebMail.EnableSsl` 设置为 `true`。
4. 在浏览器中运行*EmailRequest*页。 （请确保在运行之前在 "**文件**" 工作区中选择了该页面。）
5. 输入您的姓名和问题说明，然后单击 "**提交**" 按钮。 你会被重定向到*ProcessRequest*页，该页面确认消息，并向你发送电子邮件。 

    ![[图像]](11-adding-email-to-your-web-site/_static/image2.jpg)

<a id="Sending_a_File"></a>
## <a name="sending-a-file-using-email"></a>使用电子邮件发送文件

你还可以发送附加到电子邮件的文件。 在此过程中，您将创建一个文本文件和两个 HTML 页面。 将该文本文件用作电子邮件附件。

1. 在网站中，添加一个新的文本文件并将其命名为*myfile.txt*。
2. 复制以下文本并将其粘贴到文件中： 

    `Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.`
3. 创建一个名为*SendFile*的页，并添加以下标记： 

    [!code-html[Main](11-adding-email-to-your-web-site/samples/sample3.html)]
4. 创建一个名为*ProcessFile*的页，并添加以下标记： 

    [!code-cshtml[Main](11-adding-email-to-your-web-site/samples/sample4.cshtml)]
5. 在示例的代码中修改以下与电子邮件相关的设置：

    - 将 `your-SMTP-host` 设置为你有权访问的 SMTP 服务器的名称。
    - 将 `your-user-name-here` 设置为 SMTP 服务器帐户的用户名。
    - 将 `your-email-address-here` 设置为你自己的电子邮件地址。 这是从其发送消息的电子邮件地址。
    - 将 `your-account-password` 设置为 SMTP 服务器帐户的密码。
    - 将 `target-email-address-here` 设置为你自己的电子邮件地址。 （如前所述，你通常会向其他人发送一封电子邮件，但对于测试，你可以将其发送给你自己。）
6. 在浏览器中运行*SendFile*页。
7. 输入名称、主题行以及要附加的文本文件的名称（*myfile.txt*）。
8. 单击 `Submit` 按钮。 如前所述，你会被重定向到*ProcessFile*页，该页面会确认消息，并向你发送一封电子邮件，其中包含附加文件。

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a>其他资源

- [ASP.NET 网页 (Razor) 疑难解答指南](https://go.microsoft.com/fwlink/?LinkId=253001)
- [简单邮件传输协议](https://msdn.microsoft.com/library/aa480435.aspx)
- [为 ASP.NET 网页自定义站点范围的行为](https://go.microsoft.com/fwlink/?LinkId=202906)
