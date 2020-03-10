---
uid: web-pages/overview/security/using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site
title: 使用 CAPTCHA 阻止 Bot 使用 ASP.NET Web Razor）网站 |Microsoft Docs
author: microsoft
description: 本文介绍如何使用 ReCaptcha （安全措施）来防止自动程序（bot）在 ASP.NET 网页（Razor）中执行任务 。
ms.author: riande
ms.date: 05/21/2012
ms.assetid: 2b381a41-2cb3-40c0-8545-1d393e22877f
msc.legacyurl: /web-pages/overview/security/using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site
msc.type: authoredcontent
ms.openlocfilehash: 2647a3155893a3dfb3214795a5f9cf1e8931fa91
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78440192"
---
# <a name="using-a-captcha-to-prevent-bots-from-using-your-aspnet-web-razor-site"></a>使用 CAPTCHA 阻止 Bot 使用 ASP.NET Web Razor）站点

由[Microsoft](https://github.com/microsoft)

> 本文介绍如何使用 ReCaptcha （安全措施）来防止自动程序（bot）在 ASP.NET 网页（Razor）网站中执行任务。
> 
> **你将学习的内容：** 
> 
> - 如何将 CAPTCHA 测试添加到您的站点。
> 
> 下面是本文中介绍的 ASP.NET 功能：
> 
> - `ReCaptcha` 帮助程序。
> 
> > [!NOTE]
> > 本文中的信息适用于 ASP.NET 网页1.0 和网页2。

## <a name="about-captchas"></a>关于 CAPTCHAs

只要你允许用户在你的网站中注册，甚至只是输入名称和 URL （如博客评论），你可能会收到大量的虚假名称。 这通常由自动程序（bot）留下，尝试将 Url 保留在他们可以找到的每个网站中。 （常见的动机是发布产品的 Url 以供销售。）

可以通过使用*CAPTCHA*在用户注册或输入其名称和站点时对用户进行验证，来帮助确保用户是真实人员而不是计算机程序。 CAPTCHA 代表完全自动化的公共把测试，使计算机和人与众不同。 CAPTCHA 是一种*质询-响应*测试，要求用户执行一项操作，该操作对于某个人来说是一件容易的事情，但这是一项很难实现的自动化计划。 最常见的 CAPTCHA 类型是：其中显示一些失真的字母并要求键入它们。 （这种扭曲应该会使机器人难以破解这些字母。）

## <a name="adding-a-recaptcha-test"></a>添加 ReCaptcha 测试

在 ASP.NET 页中，可以使用 `ReCaptcha` 帮助器呈现基于 ReCaptcha 服务（[http://recaptcha.net](http://recaptcha.net)）的 CAPTCHA 测试。 `ReCaptcha` 帮助程序显示在验证页面之前用户必须正确输入的两个扭曲词的图像。 用户响应通过 ReCaptcha.Net 服务进行验证。

![](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/_static/image1.jpg)

1. 在 ReCaptcha.Net （[http://recaptcha.net](http://recaptcha.net)）注册你的网站。 完成注册后，你将获得一个公钥和一个私钥。
2. 根据在[ASP.NET 网页站点中安装帮助程序](https://go.microsoft.com/fwlink/?LinkId=252372)中所述，将 ASP.NET Web 帮助程序库添加到你的网站中（如果尚未安装）。
3. 如果还没有 *\_AppStart*文件，请在网站的根文件夹中创建一个名为 *\_AppStart*的文件。
4. 在 *\_AppStart*文件中添加以下 `Recaptcha` 帮助程序设置： 

    [!code-cshtml[Main](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/samples/sample1.cshtml?highlight=6-7)]
5. 使用自己的公钥和私钥设置 "`PublicKey`" 和 "`PrivateKey`" 属性。
6. 保存 *\_AppStart*文件并将其关闭。
7. 在网站的根文件夹中，创建名为*Recaptcha*的新页面。
8. 将现有内容替换为以下内容： 

    [!code-cshtml[Main](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/samples/sample2.cshtml)]
9. 在浏览器中运行*Recaptcha*页。 如果 `PrivateKey` 的值有效，则页面将显示 ReCaptcha 控件和按钮。 如果未在 *\_AppStart*中全局设置密钥，则页面将显示错误。 

    ![](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/_static/image1.png)
10. 输入测试的字词。 如果通过了 ReCaptcha 测试，则会看到一条消息。 否则，会显示一条错误消息，并重新显示 ReCaptcha 控件。

> [!NOTE]
> 如果您的计算机位于使用代理服务器的域中，则您可能需要配置*web.config*文件的 `defaultproxy` 元素。 下面的示例演示一个*web.config*文件，其中的 `defaultproxy` 元素配置为使 ReCaptcha 服务能够正常工作。
> 
> [!code-xml[Main](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/samples/sample3.xml)]

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a>其他资源

- [为 ASP.NET 网页站点自定义站点范围的行为](https://go.microsoft.com/fwlink/?LinkId=202906)
- [ReCaptcha 站点](https://www.google.com/recaptcha)
