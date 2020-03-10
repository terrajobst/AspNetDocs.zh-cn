---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-7
title: 第7部分：成员身份和授权 |Microsoft Docs
author: jongalloway
description: 本教程系列详细介绍了生成 ASP.NET MVC 音乐应用商店示例应用程序所需执行的所有步骤。 第7部分涵盖成员身份和授权。
ms.author: riande
ms.date: 10/13/2010
ms.assetid: c8511ebe-68bc-4240-87c3-d5ced84a3f37
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-7
msc.type: authoredcontent
ms.openlocfilehash: a6a1a936e0ea29ea36721ba78f35845401f74c01
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78433466"
---
# <a name="part-7-membership-and-authorization"></a>第7部分：成员身份和授权

作者： [Jon Galloway](https://github.com/jongalloway)

> MVC 音乐应用商店是一个教程应用程序，该应用程序逐步介绍了如何使用 ASP.NET MVC 和 Visual Studio 进行 web 开发。  
>   
> MVC 音乐应用商店是一种轻型示例存储实现，它可以在线销售音乐专辑，并实现基本的网站管理、用户登录和购物车功能。  
>   
> 本教程系列详细介绍了生成 ASP.NET MVC 音乐应用商店示例应用程序所需执行的所有步骤。 第7部分涵盖成员身份和授权。

我们的商店经理控制器目前可供访问我们的站点的任何人访问。 让我们对此进行更改，将权限限制为站点管理员。

## <a name="adding-the-accountcontroller-and-views"></a>添加 AccountController 和视图

完整的 ASP.NET MVC 3 Web 应用程序模板和 ASP.NET MVC 3 空 Web 应用程序模板之间的一个差异是，空模板不包含帐户控制器。 我们将通过从完整 ASP.NET MVC 3 Web 应用程序模板创建的新 ASP.NET MVC 应用程序复制一些文件来添加帐户控制器。

使用 full ASP.NET MVC 3 Web 应用程序模板创建新的 ASP.NET MVC 应用程序，并将以下文件复制到项目中的相同目录中：

1. 复制控制器目录中的 AccountController.cs
2. 在模型目录中复制 AccountModels
3. 在 Views 目录内创建帐户目录，并将所有四个视图复制到

更改控制器和模型类的命名空间，以使它们以 MvcMusicStore 开头。 AccountController 类应使用 MvcMusicStore 命名空间，而 AccountModels 类应使用 MvcMusicStore 命名空间。

*注意：这些文件也会在 MvcMusicStore-Assets 下载中提供，我们将在本教程的开头复制我们的站点设计文件。成员资格文件位于代码目录中。*

更新后的解决方案应如下所示：

![](mvc-music-store-part-7/_static/image1.png)

## <a name="adding-an-administrative-user-with-the-aspnet-configuration-site"></a>添加具有 ASP.NET 配置站点的管理用户

在我们的网站中需要授权之前，我们需要创建一个具有访问权限的用户。 若要创建用户，最简单的方法是使用内置的 ASP.NET 配置网站。

单击解决方案资源管理器中的图标，启动 ASP.NET 配置网站。

![](mvc-music-store-part-7/_static/image2.png)

这会启动配置网站。 单击主屏幕上的 "安全" 选项卡，然后单击屏幕中心的 "启用角色" 链接。

![](mvc-music-store-part-7/_static/image3.png)

单击 "创建或管理角色" 链接。

![](mvc-music-store-part-7/_static/image4.png)

输入 "管理员" 作为角色名称，然后按 "添加角色" 按钮。

![](mvc-music-store-part-7/_static/image5.png)

单击 "返回" 按钮，然后单击左侧的 "创建用户" 链接。

![](mvc-music-store-part-7/_static/image6.png)

使用以下信息填写左侧的 "用户信息" 字段：

| **字段** | **值** |
| --- | --- |
| **用户名** | 管理员 |
| **密码** | password123! |
| **确认密码** | password123! |
| **电子邮件** | （任何电子邮件地址都有效） |
| **安全提示问题** | （任何所需内容） |
| **安全提示问题的答案** | （任何所需内容） |

*注意：当然，你可以使用任何所需的密码。默认密码安全设置要求密码长度为7个字符，并且包含一个非字母数字字符。*

为此用户选择管理员角色，然后单击 "创建用户" 按钮。

![](mvc-music-store-part-7/_static/image7.png)

此时，应会看到一条消息，指示已成功创建用户。

![](mvc-music-store-part-7/_static/image8.png)

你现在可以关闭浏览器窗口。

## <a name="role-based-authorization"></a>基于角色的授权

现在，我们可以使用 [授权] 特性限制对 StoreManagerController 的访问，同时指定用户必须是管理员角色才能访问类中的任何控制器操作。

[!code-csharp[Main](mvc-music-store-part-7/samples/sample1.cs)]

*注意：可以将 [授权] 特性置于特定操作方法和控制器类级别。*

现在，浏览到/StoreManager 会打开一个登录对话框：

![](mvc-music-store-part-7/_static/image9.png)

在用新的管理员帐户登录后，我们就可以像以前一样来进入唱集编辑屏幕。

> [!div class="step-by-step"]
> [上一页](mvc-music-store-part-6.md)
> [下一页](mvc-music-store-part-8.md)
