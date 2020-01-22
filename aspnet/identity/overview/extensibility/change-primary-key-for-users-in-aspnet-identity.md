---
uid: identity/overview/extensibility/change-primary-key-for-users-in-aspnet-identity
title: 更改 ASP.NET Identity-ASP.NET 4.x 中用户的主密钥
author: Rick-Anderson
description: 在 Visual Studio 2013 中，默认的 web 应用程序使用用户帐户的键的字符串值。 ASP.NET Identity 使你能够更改 。
ms.author: riande
ms.date: 09/30/2014
ms.assetid: 44925849-5762-4504-a8cd-8f0cd06f6dc3
ms.custom: seoapril2019
msc.legacyurl: /identity/overview/extensibility/change-primary-key-for-users-in-aspnet-identity
msc.type: authoredcontent
ms.openlocfilehash: 0afea8eacfc646f1489b87629fdb2d437815d88c
ms.sourcegitcommit: 88fc80e3f65aebdf61ec9414810ddbc31c543f04
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/22/2020
ms.locfileid: "76519136"
---
# <a name="change-primary-key-for-users-in-aspnet-identity"></a>在 ASP.NET Identity 中更改用户的主键

通过[Tom FitzMacken](https://github.com/tfitzmac)

> 在 Visual Studio 2013 中，默认的 web 应用程序使用用户帐户的键的字符串值。 ASP.NET Identity 使你能够更改密钥的类型，以满足你的数据需求。 例如，可以将键的类型从字符串更改为整数。
> 
> 本主题说明如何从默认的 web 应用程序开始，并将用户帐户密钥更改为整数。 您可以使用相同的修改来实现项目中的任何类型的密钥。 它演示如何在默认 web 应用程序中进行这些更改，但您可以将类似的修改应用于自定义的应用程序。 其中显示了使用 MVC 或 Web 窗体时所需的更改。
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>本教程中使用的软件版本
> 
> 
> - Visual Studio 2013 更新2（或更高版本）
> - ASP.NET Identity 2.1 或更高版本

若要执行本教程中的步骤，必须具有 Visual Studio 2013 Update 2 （或更高版本）以及从 ASP.NET Web 应用程序模板创建的 web 应用程序。 在 Update 3 中更改的模板。 本主题说明如何在 Update 2 和 Update 3 中更改模板。

本主题包含以下各节：

- [更改标识用户类中的密钥类型](#userclass)
- [添加使用密钥类型的自定义标识类](#customclass)
- [更改上下文类和用户管理器以使用密钥类型](#context)
- [更改启动配置以使用密钥类型](#startup)
- [对于包含 Update 2 的 MVC，请更改 AccountController 以传递密钥类型](#mvcupdate2)
- [对于更新3的 MVC，请更改 AccountController 和 ManageController 以传递密钥类型](#mvcupdate3)
- [对于更新2的 Web 窗体，更改帐户页以传递密钥类型](#webformsupdate2)
- [对于更新3的 Web 窗体，更改帐户页以传递密钥类型](#webformsupdate3)
- [运行应用程序](#run)
- [其他资源](#other)

<a id="userclass"></a>
## <a name="change-the-type-of-the-key-in-the-identity-user-class"></a>更改标识用户类中的密钥类型

在从 ASP.NET Web 应用程序模板创建的项目中，指定 ApplicationUser 类对用户帐户的密钥使用整数。 在 IdentityModels.cs 中，更改 ApplicationUser 类，使其从类型为**int**的 IdentityUser 继承 TKey 泛型参数。 还将传递尚未实现的三个自定义类的名称。

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample1.cs?highlight=1-2)]

您已更改密钥的类型，但默认情况下，应用程序的其余部分仍假定该密钥是一个字符串。 必须在采用字符串的代码中显式指示密钥的类型。

在**ApplicationUser**类中，将**GenerateUserIdentityAsync**方法更改为包含 int，如下面突出显示的代码所示。 对于具有 Update 3 模板的 Web 窗体项目，此更改不是必需的。

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample2.cs?highlight=2)]

<a id="customclass"></a>
## <a name="add-customized-identity-classes-that-use-the-key-type"></a>添加使用密钥类型的自定义标识类

其他标识类，如 IdentityUserRole、IdentityUserClaim、IdentityUserLogin、IdentityRole、UserStore、RoleStore 仍设置为使用字符串键。 创建这些类的新版本，这些类指定键的整数。 不需要在这些类中提供很多实现代码，你主要是将 int 设置为键。

将以下类添加到 IdentityModels.cs 文件。

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample3.cs)]

<a id="context"></a>
## <a name="change-the-context-class-and-user-manager-to-use-the-key-type"></a>更改上下文类和用户管理器以使用密钥类型

在 IdentityModels.cs 中，更改**ApplicationDbContext**类的定义，以使用新的自定义类和密钥的**int** ，如突出显示的代码中所示。

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample4.cs?highlight=1-2)]

ThrowIfV1Schema 参数在构造函数中不再有效。 更改构造函数，使其不传递 ThrowIfV1Schema 值。

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample5.cs)]

打开 IdentityConfig.cs，并将**ApplicationUserManger**类更改为使用新用户存储类来保存数据，并使用**int**作为密钥。

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample6.cs?highlight=1,3,12,14,32,37,48)]

在 Update 3 模板中，必须更改 ApplicationSignInManager 类。

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample7.cs?highlight=1)]

<a id="startup"></a>
## <a name="change-start-up-configuration-to-use-the-key-type"></a>更改启动配置以使用密钥类型

在 Startup.Auth.cs 中，替换 OnValidateIdentity 代码，如下所示。 请注意，getUserIdCallback 定义会将字符串值分析为一个整数。

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample8.cs?highlight=7-12)]

如果你的项目不能识别**GetUserId**方法的泛型实现，你可能需要将 ASP.NET Identity NuGet 包更新到版本2。1

你已对 ASP.NET Identity 使用的基础结构类进行了大量更改。 如果尝试编译项目，会注意到很多错误。 幸运的是，剩下的错误都是类似的。 标识类需要键的整数，但控制器（或 Web 窗体）传递的是一个字符串值。 在每种情况下，都需要通过调用**GetUserId&lt;int&gt;** ，将字符串转换为和整数。 可以通过编译来处理 "错误列表"，也可以执行以下更改。

剩余的更改取决于要创建的项目的类型，以及在 Visual Studio 中安装的更新。 可以通过以下链接直接进入相关部分

- [对于包含 Update 2 的 MVC，请更改 AccountController 以传递密钥类型](#mvcupdate2)
- [对于更新3的 MVC，请更改 AccountController 和 ManageController 以传递密钥类型](#mvcupdate3)
- [对于更新2的 Web 窗体，更改帐户页以传递密钥类型](#webformsupdate2)
- [对于更新3的 Web 窗体，更改帐户页以传递密钥类型](#webformsupdate3)

<a id="mvcupdate2"></a>
## <a name="for-mvc-with-update-2-change-the-accountcontroller-to-pass-the-key-type"></a>对于包含 Update 2 的 MVC，请更改 AccountController 以传递密钥类型

打开 AccountController.cs 文件。 需要更改以下方法。

**ConfirmEmail**方法

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample9.cs?highlight=1,3)]

**解除关联**方法

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample10.cs?highlight=5,9)]

**管理（ManageUserViewModel）** 方法

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample11.cs?highlight=11,17,41)]

**LinkLoginCallback**方法

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample12.cs?highlight=10)]

**RemoveAccountList**方法

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample13.cs?highlight=3)]

**HasPassword**方法

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample14.cs?highlight=3)]

现在可以[运行应用程序](#run)并注册新用户。

<a id="mvcupdate3"></a>
## <a name="for-mvc-with-update-3-change-the-accountcontroller-and-managecontroller-to-pass-the-key-type"></a>对于更新3的 MVC，请更改 AccountController 和 ManageController 以传递密钥类型

打开 AccountController.cs 文件。 需要更改以下方法。

**ConfirmEmail**方法

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample15.cs?highlight=1,3)]

**SendCode**方法

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample16.cs?highlight=4)]

打开 ManageController.cs 文件。 需要更改以下方法。

**Index**方法

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample17.cs?highlight=15-17)]

**RemoveLogin**方法

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample18.cs?highlight=3,13,17)]

**AddPhoneNumber**方法

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample19.cs?highlight=9)]

**EnableTwoFactorAuthentication**方法

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample20.cs?highlight=3-4)]

**DisableTwoFactorAuthentication**方法

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample21.cs?highlight=3-4)]

**VerifyPhoneNumber**方法

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample22.cs?highlight=4,18,21)]

**RemovePhoneNumber**方法

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample23.cs?highlight=3,8)]

**ChangePassword**方法

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample24.cs?highlight=10,13)]

**SetPassword**方法

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample25.cs?highlight=5,8)]

**ManageLogins**方法

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample26.cs?highlight=7,12)]

**LinkLoginCallback**方法

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample27.cs?highlight=8)]

**HasPassword**方法

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample28.cs?highlight=3)]

**HasPhoneNumber**方法

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample29.cs?highlight=3)]

现在可以[运行应用程序](#run)并注册新用户。

<a id="webformsupdate2"></a>
## <a name="for-web-forms-with-update-2-change-account-pages-to-pass-the-key-type"></a>对于更新2的 Web 窗体，更改帐户页以传递密钥类型

对于更新2的 Web 窗体，需要更改以下页面。

**Confirm.aspx.cx**

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample30.cs?highlight=8)]

**RegisterExternalLogin.aspx.cs**

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample31.cs?highlight=36)]

**Manage.aspx.cs**

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample32.cs?highlight=3,22,47,52,69,85,93,98)]

现在可以[运行应用程序](#run)并注册新用户。

<a id="webformsupdate3"></a>
## <a name="for-web-forms-with-update-3-change-account-pages-to-pass-the-key-type"></a>对于更新3的 Web 窗体，更改帐户页以传递密钥类型

对于更新3的 Web 窗体，需要更改以下页面。

**Confirm.aspx.cx**

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample33.cs?highlight=8)]

**RegisterExternalLogin.aspx.cs**

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample34.cs?highlight=36)]

**Manage.aspx.cs**

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample35.cs?highlight=11,27,32,34,82,87,99,108)]

**VerifyPhoneNumber.aspx.cs**

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample36.cs?highlight=8,23,27)]

**AddPhoneNumber.aspx.cs**

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample37.cs?highlight=7)]

**ManagePassword.aspx.cs**

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample38.cs?highlight=11,47,50,68)]

**ManageLogins.aspx.cs**

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample39.cs?highlight=16,23,32,41,45)]

**TwoFactorAuthenticationSignIn.aspx.cs**

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample40.cs?highlight=14-15,29,53)]

<a id="run"></a>
## <a name="run-application"></a>运行应用程序

已完成对默认 Web 应用程序模板所需的所有更改。 运行应用程序并注册新用户。 注册用户后，您会注意到，AspNetUsers 表的 Id 列是整数。

![新主键](change-primary-key-for-users-in-aspnet-identity/_static/image1.png)

如果以前使用不同的主键创建了 ASP.NET Identity 表，则需要进行一些额外的更改。 如果可能，只需删除现有的数据库。 在运行 web 应用程序并添加新用户时，将使用正确的设计重新创建数据库。 如果无法删除，请运行 code first 迁移来更改表。 但是，新的整数主键将不会设置为数据库中的 "SQL 标识" 属性。 您必须手动将 "Id" 列设置为标识。

<a id="other"></a>
## <a name="other-resources"></a>其他资源

- [ASP.NET 标识的自定义存储提供程序概述](overview-of-custom-storage-providers-for-aspnet-identity.md)
- [将现有网站从 SQL 成员身份迁移到 ASP.NET 标识](../migrations/migrating-an-existing-website-from-sql-membership-to-aspnet-identity.md)
- [将成员身份和用户配置文件的通用提供程序数据迁移到 ASP.NET Identity](../migrations/migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity.md)
- 带有更改的主键的[示例应用程序](https://github.com/aspnet/samples/tree/master/samples/aspnet/Identity/ChangePK)
