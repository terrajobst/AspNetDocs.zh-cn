---
uid: identity/overview/extensibility/overview-of-custom-storage-providers-for-aspnet-identity
title: ASP.NET Identity 的自定义存储提供程序概述-ASP.NET 4。x
author: Rick-Anderson
description: ASP.NET Identity 是一种可扩展系统，可让你创建自己的存储提供程序，并将其插入应用程序，而无需重新运行应用 。
ms.author: riande
ms.date: 10/13/2014
ms.assetid: 681a9204-462e-4260-9a0b-19f0644d6ad7
ms.custom: seoapril2019
msc.legacyurl: /identity/overview/extensibility/overview-of-custom-storage-providers-for-aspnet-identity
msc.type: authoredcontent
ms.openlocfilehash: 21baedf6285b411f89627df9ca25d47a2a42e387
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78472220"
---
# <a name="overview-of-custom-storage-providers-for-aspnet-identity"></a>ASP.NET Identity 的自定义存储提供程序概述

作者： [Tom FitzMacken](https://github.com/tfitzmac)

> ASP.NET Identity 是一种可扩展系统，可让你创建自己的存储提供程序，并将其插入到应用程序中，而无需重新运行应用程序。 本主题介绍如何为 ASP.NET Identity 创建自定义的存储提供程序。 它介绍了用于创建自己的存储提供程序的重要概念，但它不是实现自定义存储提供程序的分步演练。
> 
> 有关实现自定义存储提供程序的示例，请参阅[实现自定义 MySQL ASP.NET Identity 存储提供程序](implementing-a-custom-mysql-aspnet-identity-storage-provider.md)。
> 
> 本主题已针对 ASP.NET Identity 2.0 进行了更新。
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>本教程中使用的软件版本
> 
> 
> - Visual Studio 2013 更新2
> - ASP.NET Identity 2

## <a name="introduction"></a>简介

默认情况下，ASP.NET Identity 系统会将用户信息存储在 SQL Server 数据库中，并使用实体框架 Code First 来创建数据库。 对于许多应用程序而言，这种方法的效果很好。 但是，你可能更倾向于使用其他类型的持久性机制（如 Azure 表存储），或者你的数据库表的结构与默认实现的结构不同。 在任一情况下，都可以为存储机制编写自定义的提供程序，并将该提供程序插入到应用程序中。

默认情况下，许多 Visual Studio 2013 模板中都包含 ASP.NET Identity。 可以通过[Microsoft AspNet Identity EntityFramework NuGet 包](http://www.nuget.org/packages/Microsoft.AspNet.Identity.EntityFramework/)获取 ASP.NET Identity 更新。

本主题包括以下部分：

- [了解体系结构](#architecture)
- [了解存储的数据](#data)
- [创建数据访问层](#dal)
- [自定义用户类](#user)
- [自定义用户存储](#userstore)
- [自定义 role 类](#role)
- [自定义角色存储](#rolestore)
- [重新配置应用程序以使用新的存储提供程序](#reconfigure)
- [自定义存储提供程序的其他实现](#other)

<a id="architecture"></a>
## <a name="understand-the-architecture"></a>了解体系结构

ASP.NET Identity 由名为管理器和存储的类组成。 管理器是应用程序开发人员用来在 ASP.NET Identity 系统中执行操作（如创建用户）的高级类。 存储是用于指定如何保存实体（如用户和角色）的较低级别类。 存储与持久性机制紧密耦合，但管理器与存储分离，这意味着可以替换持久性机制，而不会中断整个应用程序。

下图显示了 web 应用程序如何与管理器进行交互，以及如何存储与数据访问层交互。

![](overview-of-custom-storage-providers-for-aspnet-identity/_static/image1.png)

若要为 ASP.NET Identity 创建自定义的存储提供程序，必须创建数据源、数据访问层以及与此数据访问层交互的存储类。 你可以继续使用相同的管理器 Api 在用户上执行数据操作，但现在数据将保存到不同的存储系统中。

不需要自定义管理器类，因为在创建 UserManager 或 RoleManager 的新实例时，提供 user 类的类型并将 store 类的实例作为参数传递。 此方法使你能够将自定义类插入现有结构。 在将[应用程序配置为使用新的存储提供程序](#reconfigure)部分中，你将了解如何使用自定义存储类实例化 UserManager 和 RoleManager。

<a id="data"></a>
## <a name="understand-the-data-that-is-stored"></a>了解存储的数据

若要实现自定义存储提供程序，您必须了解与 ASP.NET Identity 一起使用的数据类型，并决定哪些功能与您的应用程序相关。

| 数据 | 说明 |
| --- | --- |
| 用户 | 网站的已注册用户。 包括用户 Id 和用户名。 如果用户使用特定于你的站点的凭据（而不是使用 Facebook 之类的外部站点的凭据）登录，则可能包含哈希密码，以及用于指示用户凭据中是否有任何更改的安全标记。 还可能包括电子邮件地址、电话号码、是否启用了双因素身份验证、当前失败的登录数以及某个帐户是否已锁定。 |
| 用户声明 | 有关表示用户标识的用户的一组语句（或声明）。 可以启用用户标识的更大表达式，而不能通过角色来实现。 |
| 用户登录 | 用于在用户登录时使用的外部身份验证提供程序（如 Facebook）的相关信息。 |
| 角色 | 站点的授权组。 包括角色 Id 和角色名称（如 "管理员" 或 "Employee"）。 |

<a id="dal"></a>
## <a name="create-the-data-access-layer"></a>创建数据访问层

本主题假定您熟悉要使用的持久性机制以及如何创建该机制的实体。 本主题不提供有关如何创建存储库或数据访问类的详细信息;相反，它提供了有关使用 ASP.NET Identity 时所需的设计决策的一些建议。

为自定义的存储提供程序设计存储库时，您有许多自由。 只需要为要在应用程序中使用的功能创建存储库。 例如，如果你未在应用程序中使用角色，则无需为角色或用户角色创建存储。 你的技术和现有基础结构可能需要结构，这与 ASP.NET Identity 的默认实现非常不同。 在数据访问层中，提供用于处理存储库结构的逻辑。

有关 ASP.NET Identity 2.0 的数据存储库的 MySQL 实现，请参阅[MySQLIdentity](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/MySQLIdentity.sql)。

在数据访问层中，提供用于将数据从 ASP.NET Identity 保存到数据源的逻辑。 自定义存储提供程序的数据访问层可能包含以下类来存储用户和角色信息。

| 类 | 说明 | 示例 |
| --- | --- | --- |
| 上下文 | 封装信息以连接到永久性机制并执行查询。 此类是你的数据访问层的核心。 其他数据类将需要此类的实例来执行其操作。 您还将使用此类的实例初始化您的存储类。 | [MySQLDatabase](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/MySQLDatabase.cs) |
| 用户存储 | 存储和检索用户信息（例如用户名和密码哈希）。 | [UserTable （MySQL）](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/UserTable.cs) |
| 角色存储 | 存储和检索角色信息（如角色名称）。 | [RoleTable （MySQL）](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/RoleTable.cs) |
| UserClaims 存储 | 存储和检索用户声明信息（如声明类型和值）。 | [UserClaimsTable （MySQL）](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/UserClaimsTable.cs) |
| UserLogins 存储 | 存储和检索用户登录信息（如外部身份验证提供程序）。 | [UserLoginsTable （MySQL）](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/UserLoginsTable.cs) |
| UserRole 存储 | 存储和检索用户分配到的角色。 | [UserRoleTable （MySQL）](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/UserRoleTable.cs) |

同样，只需实现打算在应用程序中使用的类。

在数据访问类中，你可以为特定的持久性机制提供执行数据操作的代码。 例如，在 MySQL 实现中，UserTable 类包含一个方法，用于将新记录插入到用户数据库表中。 名为 `_database` 的变量是 MySQLDatabase 类的实例。

[!code-csharp[Main](overview-of-custom-storage-providers-for-aspnet-identity/samples/sample1.cs)]

创建数据访问类后，必须创建调用数据访问层中特定方法的存储类。

<a id="user"></a>
## <a name="customize-the-user-class"></a>自定义用户类

实现自己的存储提供程序时，必须创建一个与[EntityFramework](https://msdn.microsoft.com/library/microsoft.aspnet.identity.entityframework(v=vs.108).aspx)命名空间中的[IdentityUser](https://msdn.microsoft.com/library/microsoft.aspnet.identity.entityframework.identityuser(v=vs.108).aspx)类等效的 user 类：

下图显示了必须创建的 IdentityUser 类以及要在此类中实现的接口。

![](overview-of-custom-storage-providers-for-aspnet-identity/_static/image2.png)

[IUser&lt;TKey&gt;](https://msdn.microsoft.com/library/dn613291(v=vs.108).aspx)接口定义 UserManager 在执行请求的操作时尝试调用的属性。 此接口包含两个属性-Id 和用户名。 使用[IUser&lt;TKey&gt;](https://msdn.microsoft.com/library/dn613291(v=vs.108).aspx)接口，可以通过泛型**TKey**参数指定用户的密钥类型。 Id 属性的类型与 TKey 参数的值相匹配。

如果要对键使用字符串值，则标识框架还提供[IUser](https://msdn.microsoft.com/library/microsoft.aspnet.identity.iuser(v=vs.108).aspx)接口（不包含泛型参数）。

IdentityUser 类实现 IUser，并包含网站上用户的任何其他属性或构造函数。 下面的示例演示了一个 IdentityUser 类，该类对键使用整数。 Id 字段设置为**int** ，以匹配泛型参数的值。 

[!code-csharp[Main](overview-of-custom-storage-providers-for-aspnet-identity/samples/sample2.cs)]

 有关完整的实现，请参阅[IdentityUser （MySQL）](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/IdentityUser.cs)。 

<a id="userstore"></a>
## <a name="customize-the-user-store"></a>自定义用户存储

还将创建一个 UserStore 类，该类提供用户的所有数据操作的方法。 此类等效于[EntityFramework](https://msdn.microsoft.com/library/microsoft.aspnet.identity.entityframework(v=vs.108).aspx)命名空间中的[UserStore&lt;TUser&gt;](https://msdn.microsoft.com/library/dn315446(v=vs.108).aspx)类。 在 UserStore 类中，可实现[IUserStore&lt;TUser、TKey&gt;](https://msdn.microsoft.com/library/dn613276(v=vs.108).aspx)和任何可选接口。 根据希望在应用程序中提供的功能，选择要实现的可选接口。

下图显示了必须创建的 UserStore 类以及相关接口。

![](overview-of-custom-storage-providers-for-aspnet-identity/_static/image3.png)

Visual Studio 中的默认项目模板包含的代码假定已在用户存储中实现了许多可选接口。 如果你使用的是自定义用户存储的默认模板，则必须在你的用户存储中实现可选接口，或更改模板代码，使其不再调用尚未实现的接口中的方法。

 下面的示例演示一个简单的用户存储类。 **TUser**泛型参数采用用户类的类型，通常是你定义的 IdentityUser 类。 **TKey**泛型参数采用用户密钥的类型。 

[!code-csharp[Main](overview-of-custom-storage-providers-for-aspnet-identity/samples/sample3.cs)]

 在此示例中，采用类型为 ExampleDatabase 的类型为*数据库*的参数的构造函数只说明了如何传入数据访问类。 例如，在 MySQL 实现中，此构造函数采用类型为 MySQLDatabase 的参数。 

在 UserStore 类中，使用创建的数据访问类来执行操作。 例如，在 MySQL 实现中，UserStore 类具有 CreateAsync 方法，该方法使用 UserTable 的实例插入新记录。 **UserTable**对象上的**Insert**方法与上一节中所示的方法相同。 

[!code-csharp[Main](overview-of-custom-storage-providers-for-aspnet-identity/samples/sample4.cs)]

### <a name="interfaces-to-implement-when-customizing-user-store"></a>自定义用户存储时要实现的接口

下图显示了有关每个接口中定义的功能的更多详细信息。 所有可选接口都继承自 IUserStore。

![](overview-of-custom-storage-providers-for-aspnet-identity/_static/image4.png)

- **IUserStore**  
  [IUserStore&lt;TUser，TKey&gt;](https://msdn.microsoft.com/library/dn613278(v=vs.108).aspx) interface 是你必须在用户存储中实现的唯一接口。 它定义用于创建、更新、删除和检索用户的方法。
- **IUserClaimStore**  
  [IUserClaimStore&lt;TUser，TKey&gt;](https://msdn.microsoft.com/library/dn613265(v=vs.108).aspx)接口定义你必须在用户存储中实现以启用用户声明的方法。 它包含方法，或者添加、删除和检索用户声明。
- **IUserLoginStore**  
  [IUserLoginStore&lt;TUser，TKey&gt;](https://msdn.microsoft.com/library/dn613272(v=vs.108).aspx)定义用户存储中必须实现的方法，以启用外部身份验证提供程序。 它包含添加、删除和检索用户登录名的方法，以及用于根据登录信息检索用户的方法。
- **IUserRoleStore**  
  [IUserRoleStore&lt;TKey，TUser&gt;](https://msdn.microsoft.com/library/dn613276(v=vs.108).aspx)接口定义用户存储中必须实现的方法，以便将用户映射到角色。 它包含添加、删除和检索用户角色的方法，以及用于检查是否向用户分配了角色的方法。
- **IUserPasswordStore**  
  [IUserPasswordStore&lt;TUser，TKey&gt;](https://msdn.microsoft.com/library/dn613273(v=vs.108).aspx)接口定义用户存储中必须实现的方法，以保存哈希密码。 它包含用于获取和设置哈希密码的方法，以及一个指示用户是否已设置密码的方法。
- **IUserSecurityStampStore**  
  [IUserSecurityStampStore&lt;TUser，TKey&gt;](https://msdn.microsoft.com/library/dn613277(v=vs.108).aspx)接口定义在用户存储中必须实现的方法，以使用安全戳记来指示用户的帐户信息是否已更改。 当用户更改密码或添加或删除登录名时，此戳记会更新。 它包含用于获取和设置安全标记的方法。
- **IUserTwoFactorStore**  
  [IUserTwoFactorStore&lt;TUser，TKey&gt;](https://msdn.microsoft.com/library/dn613279(v=vs.108).aspx)接口定义为实现双重身份验证而必须实现的方法。 它包含的方法可用于获取和设置是否为用户启用了双因素身份验证。
- **IUserPhoneNumberStore**  
  [IUserPhoneNumberStore&lt;TUser，TKey&gt;](https://msdn.microsoft.com/library/dn613275(v=vs.108).aspx)接口定义为存储用户电话号码而必须实现的方法。 它包含的方法可用于获取和设置电话号码，以及电话号码是否已确认。
- **IUserEmailStore**  
  [IUserEmailStore&lt;TUser，TKey&gt;](https://msdn.microsoft.com/library/dn613143(v=vs.108).aspx)接口定义为存储用户电子邮件地址而必须实现的方法。 它包含用于获取和设置电子邮件地址以及是否已确认电子邮件的方法。
- **IUserLockoutStore**  
  [IUserLockoutStore&lt;TUser，TKey&gt;](https://msdn.microsoft.com/library/dn613271(v=vs.108).aspx)接口定义为存储有关锁定帐户的信息而必须实现的方法。 它包含的方法可用于获取当前失败的访问尝试次数，获取并设置该帐户是否可以锁定，获取并设置锁定结束日期，增加失败尝试次数，并重置失败尝试次数。
- **IQueryableUserStore**  
  [IQueryableUserStore&lt;TUser，TKey&gt;](https://msdn.microsoft.com/library/dn613267(v=vs.108).aspx)接口定义为提供可查询用户存储而必须实现的成员。 它包含保存可查询用户的属性。

  实现应用程序中所需的接口;例如，IUserClaimStore、IUserLoginStore、IUserRoleStore、IUserPasswordStore 和 IUserSecurityStampStore 接口，如下所示。 

[!code-csharp[Main](overview-of-custom-storage-providers-for-aspnet-identity/samples/sample5.cs)]

有关完整实现（包括所有接口），请参阅[UserStore （MySQL）](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/UserStore.cs)。

### <a name="identityuserclaim-identityuserlogin-and-identityuserrole"></a>IdentityUserClaim、IdentityUserLogin 和 IdentityUserRole

EntityFramework 命名空间包含[IdentityUserClaim](https://msdn.microsoft.com/library/dn613250(v=vs.108).aspx)、 [IdentityUserLogin](https://msdn.microsoft.com/library/dn613251(v=vs.108).aspx)和[IdentityUserRole](https://msdn.microsoft.com/library/dn613252(v=vs.108).aspx)类的实现。 如果使用这些功能，可能需要创建自己版本的这些类，并定义应用程序的属性。 但是，在执行基本操作（如添加或删除用户的声明）时，如果不将这些实体加载到内存中，有时会更有效。 而后端存储类可以直接对数据源执行这些操作。 例如，UserStore. GetClaimsAsync （）方法可以调用 userClaimTable. FindByUserId （user。Id）方法对该表直接执行查询，并返回声明列表。

[!code-csharp[Main](overview-of-custom-storage-providers-for-aspnet-identity/samples/sample6.cs)]

<a id="role"></a>
## <a name="customize-the-role-class"></a>自定义 role 类

实现自己的存储提供程序时，必须创建与[EntityFramework](https://msdn.microsoft.com/library/microsoft.aspnet.identity.entityframework(v=vs.108).aspx)命名空间中的[IdentityRole](https://msdn.microsoft.com/library/microsoft.aspnet.identity.entityframework.identityrole(v=vs.108).aspx)类等效的 role 类：

下图显示了必须创建的 IdentityRole 类以及要在此类中实现的接口。

![](overview-of-custom-storage-providers-for-aspnet-identity/_static/image5.png)

[IRole&lt;TKey&gt;](https://msdn.microsoft.com/library/dn613268(v=vs.108).aspx)接口定义 RoleManager 在执行请求的操作时尝试调用的属性。 此接口包含两个属性-Id 和名称。 使用[IRole&lt;TKey&gt;](https://msdn.microsoft.com/library/dn613268(v=vs.108).aspx)接口，可以通过泛型**TKey**参数为角色指定密钥类型。 Id 属性的类型与 TKey 参数的值相匹配。

如果要对键使用字符串值，则标识框架还提供[IRole](https://msdn.microsoft.com/library/microsoft.aspnet.identity.irole(v=vs.108).aspx)接口（不包含泛型参数）。

下面的示例演示了一个 IdentityRole 类，该类对键使用整数。 Id 字段设置为 int，以匹配泛型参数的值。 

[!code-csharp[Main](overview-of-custom-storage-providers-for-aspnet-identity/samples/sample7.cs)]

 有关完整的实现，请参阅[IdentityRole （MySQL）](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/IdentityRole.cs)。 

<a id="rolestore"></a>
## <a name="customize-the-role-store"></a>自定义角色存储

还将创建一个 RoleStore 类，该类提供针对角色的所有数据操作的方法。 此类等效于 EntityFramework 命名空间中的[RoleStore&lt;TRole&gt;](https://msdn.microsoft.com/library/dn468181(v=vs.108).aspx)类。 在 RoleStore 类中，可实现[IRoleStore&lt;TRole、TKey&gt;](https://msdn.microsoft.com/library/dn613266(v=vs.108).aspx) ，还可以选择[IQueryableRoleStore&lt;TRole，TKey&gt;](https://msdn.microsoft.com/library/dn613262(v=vs.108).aspx)接口。

![](overview-of-custom-storage-providers-for-aspnet-identity/_static/image6.png)

下面的示例演示了一个角色存储类。 TRole 泛型参数采用你的角色类的类型，通常为你定义的 IdentityRole 类。 TKey 泛型参数采用你的角色密钥的类型。 

[!code-csharp[Main](overview-of-custom-storage-providers-for-aspnet-identity/samples/sample8.cs)]

- **IRoleStore&lt;TRole&gt;**  
  [IRoleStore](https://msdn.microsoft.com/library/dn468195.aspx)接口定义要在角色存储类中实现的方法。 它包含用于创建、更新、删除和检索角色的方法。
- **RoleStore&lt;TRole&gt;**  
  若要自定义 RoleStore，请创建一个实现 IRoleStore 接口的类。 如果要在系统上使用角色，只需实现此类。 采用类型为 ExampleDatabase 的类型为*数据库*的参数的构造函数只说明了如何传入数据访问类。 例如，在 MySQL 实现中，此构造函数采用类型为 MySQLDatabase 的参数。  
  
  有关完整的实现，请参阅[RoleStore （MySQL）](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/RoleStore.cs) 。

<a id="reconfigure"></a>
## <a name="reconfigure-application-to-use-new-storage-provider"></a>重新配置应用程序以使用新的存储提供程序

你已经实现了新的存储提供程序。 现在，你必须将应用程序配置为使用此存储提供程序。 如果项目中包含默认存储提供程序，则必须删除默认提供程序并将其替换为提供程序。

### <a name="replace-default-storage-provider-in-mvc-project"></a>替换 MVC 项目中的默认存储提供程序

1. 在 "**管理 NuGet 包**" 窗口中，卸载**Microsoft ASP.NET Identity EntityFramework** package。 可以通过在已安装的包中搜索 EntityFramework 来查找此包。  
    ![](overview-of-custom-storage-providers-for-aspnet-identity/_static/image7.png) 系统会询问你是否也要卸载实体框架。 如果你不需要在应用程序的其他部分中执行此操作，则可以将其卸载。
2. 在模型文件夹的 IdentityModels.cs 文件中，删除或注释掉**ApplicationUser**和**ApplicationDbContext**类。 在 MVC 应用程序中，可以删除整个 IdentityModels.cs 文件。 在 Web 窗体应用程序中，删除这两个类，但请确保保留也位于 IdentityModels.cs 文件中的帮助器类。
3. 如果你的存储提供程序驻留在单独的项目中，请在你的 web 应用程序中添加对它的引用。
4. 使用存储提供程序的命名空间的 using 语句替换对 `using Microsoft.AspNet.Identity.EntityFramework;` 的所有引用。
5. 在**Startup.Auth.cs**类中，将**ConfigureAuth**方法更改为使用适当上下文的单个实例。 

    [!code-csharp[Main](overview-of-custom-storage-providers-for-aspnet-identity/samples/sample9.cs?highlight=3)]
6. 在应用\_"开始" 文件夹中，打开**IdentityConfig.cs**。 在 ApplicationUserManager 类中，更改**Create**方法以返回使用自定义用户存储的用户管理员。 

    [!code-csharp[Main](overview-of-custom-storage-providers-for-aspnet-identity/samples/sample10.cs?highlight=3)]
7. 将对**ApplicationUser**的所有引用替换为**IdentityUser**。
8. 默认项目包含用户类中未在 IUser 接口中定义的某些成员;例如 Email、PasswordHash 和 GenerateUserIdentityAsync。 如果用户类没有这些成员，则必须实现它们或更改使用这些成员的代码。
9. 如果已创建 RoleManager 的任何实例，请更改该代码以使用新的 RoleStore 类。  

    [!code-csharp[Main](overview-of-custom-storage-providers-for-aspnet-identity/samples/sample11.cs)]
10. 默认项目是为具有键的字符串值的用户类设计的。 如果用户类的键类型不同（如整数），则必须更改项目以使用您的类型。 请参阅[在 ASP.NET Identity 中更改用户的主密钥](change-primary-key-for-users-in-aspnet-identity.md)。
11. 如果需要，请将连接字符串添加到 web.config 文件。

<a id="other"></a>
## <a name="other-resources"></a>其他资源

- 博客：[实现 ASP.NET Identity](http://odetocode.com/blogs/scott/archive/2014/01/20/implementing-asp-net-identity.aspx)
- 教程和 GIT 代码： [Simple。数据 Asp.Net 标识提供程序](http://designcoderelease.blogspot.co.uk/2015/03/simpledata-aspnet-identity-provider.html)
- 教程：[设置基本标识帐户，并将其指向外部数据库](http://typecastexception.com/post/2013/10/27/Configuring-Db-Connection-and-Code-First-Migration-for-Identity-Accounts-in-ASPNET-MVC-5-and-Visual-Studio-2013.aspx)。 通过[@xivSolutions](https://twitter.com/xivSolutions)。
- 教程[：实现自定义 MySQL ASP.NET Identity 存储提供程序](implementing-a-custom-mysql-aspnet-identity-storage-provider.md)
- 按[SoftFluent](http://www.softfluent.com/) [CodeFluent 实体](http://blog.codefluententities.com/2014/04/30/asp-net-identity-v2-and-codefluent-entities/)
- 按 James Randall) 的[Azure 表存储](https://www.nuget.org/packages/accidentalfish.aspnet.identity.azure/)。
- Azure 表存储：[表存储。](https://github.com/stuartleeks/leeksnet.AspNet.Identity.TableStorage)通过[@stuartleeks](https://twitter.com/stuartleeks)。
- [CouchDB/Cloudant by Daniel Wertheim。](https://github.com/danielwertheim/mycouch.aspnet.identity)
- 弹性搜索[h：](https://github.com/bmbsqd/elastic-identity)通过 Bombsquad AB 进行弹性标识。
- [MongoDB](http://www.nuget.org/packages/MongoDB.AspNet.Identity/) By Jonathan Sheely Jonathan Sheely。
- [NHibernate](https://github.com/milesibastos/NHibernate.AspNet.Identity) By Antônio Milesi Bastos。
- [RavenDB](http://www.nuget.org/packages/AspNet.Identity.RavenDB/1.0.0) [@tourismgeek](https://twitter.com/tourismgeek)。
- [ILMServices](http://www.ilmservice.com/)的[RavenDB](https://github.com/ILMServices/RavenDB.AspNet.Identity) 。
- Redis： [Redis](https://github.com/aminjam/Redis.AspNet.Identity)
- 用于为 "数据库第一个" 用户存储生成 EF 代码的 T4 模板： [EntityFramework](https://github.com/cbfrank/AspNet.Identity.EntityFramework)
