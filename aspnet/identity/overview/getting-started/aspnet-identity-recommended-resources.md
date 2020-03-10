---
uid: identity/overview/getting-started/aspnet-identity-recommended-resources
title: ASP.NET Identity 推荐的资源-ASP.NET 4。x
author: Rick-Anderson
description: 本主题提供有关如何使用 ASP.NET Identity 的文档资源的链接。 如果你知道精彩的博客文章、stackoverflow 或任何其他链接 。
ms.author: riande
ms.date: 04/09/2015
ms.assetid: 0f78aec2-f509-46fa-b20f-d5208425d8ec
ms.custom: seoapril2019
msc.legacyurl: /identity/overview/getting-started/aspnet-identity-recommended-resources
msc.type: authoredcontent
ms.openlocfilehash: 4b2a6689839f66121f4a32ee5934f6cda50ae812
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78499790"
---
# <a name="aspnet-identity-recommended-resources"></a>ASP.NET Identity 建议的资源

作者： [Rick Anderson](https://twitter.com/RickAndMSFT)

> 本主题提供有关如何使用 ASP.NET Identity 的文档资源的链接。
>
> 如果你知道一篇非常有用的博客文章、 [stackoverflow](http://stackoverflow.com)或任何其他链接，请[向我们发送一封](mailto:aspnetue@microsoft.com?subject=Identity recommended resources)包含链接的电子邮件，或者只需在此页面底部留下一条消息。

- [ASP.NET 标识入门](#gettingstarted)
- [新功能必须阅读文章](#feat)
- [中间 ASP.NET Identity](#adv)
- [视频](#video)
- [在何处提出问题，请求功能，报告 bug 和夜间生成](#samp)
- [有关标识的博客文章](#blog)
- [ASP.NET Identity 的自定义存储提供程序](#cust)
- [其他标识资源](#additional)
- [问答 &amp; （问题/解答）](#qand)

<a id="gettingstarted"></a>

## <a name="getting-started-with-aspnet-identity"></a>ASP.NET Identity 入门

- [带有 Facebook、Twitter、LinkedIn 和 Google OAuth2 登录的 MVC 5 应用程序](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md)本教程介绍如何使用 Facebook 和 Google OAuth 2 授权编写 ASP.NET MVC 5 应用。 它还说明如何向标识数据库添加其他数据。
- [使用成员资格、OAuth 和 SQL 数据库将安全的 ASP.NET MVC 应用程序部署到 Azure](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)。 本教程添加 Azure 部署，如何使用角色保护应用，如何使用成员资格 API 添加用户和角色以及其他安全功能。
- [ASP.NET 标识简介](introduction-to-aspnet-identity.md)
- [创建具有登录、电子邮件确认及密码重置功能的安全 ASP.NET MVC 5 Web 应用程序](../../../mvc/overview/security/create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset.md)
- [具有 SMS 和电子邮件双因素身份验证的 ASP.NET MVC 5 应用](../../../mvc/overview/security/aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication.md)

<a id="feat"></a>

## <a name="new-featured-must-read-articles"></a>新功能必须阅读文章

- [演练：使用 Microsoft 帐户身份验证的 ASP.NET MVC 标识（](http://www.benday.com/2014/02/25/walkthrough-asp-net-mvc-identity-with-microsoft-account-authentication/)按[Benjamin 天](http://www.benday.com/about/)）
- [ASP.NET Identity 2.0 扩展标识模型以及使用整数键而不是字符串](http://typecastexception.com/post/2014/07/13/ASPNET-Identity-20-Extending-Identity-Models-and-Using-Integer-Keys-Instead-of-Strings.aspx)
- [使用 ASP.NET Web API 2、Owin 和 Identity 的 AngularJS 令牌身份验证](http://bitoftech.net/2014/06/09/angularjs-token-authentication-using-asp-net-web-api-2-owin-asp-net-identity/)
- [IdentityManager 替换为 WSAT 的 Thinktecture](http://www.hanselman.com/blog/ThinktectureIdentityManagerAsAReplacementForTheASPNETWebSiteAdministrationTool.aspx)
- [ASP.NET Identity 2.0：自定义用户和角色](http://typecastexception.com/post/2014/06/22/ASPNET-Identity-20-Customizing-Users-and-Roles.aspx)

<a id="adv"></a>

## <a name="intermediate-aspnet-identity"></a>中间 ASP.NET Identity

- [帐户确认和密码恢复与 ASP.NET Identity](../features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md)
- [使用 SMS 和 ASP.NET 标识的双因素身份验证](../features-api/two-factor-authentication-using-sms-and-email-with-aspnet-identity.md)
- [将现有网站从 SQL 成员身份迁移到 ASP.NET 标识](../migrations/migrating-an-existing-website-from-sql-membership-to-aspnet-identity.md)
- [向空的或现有的 Web 窗体项目添加 ASP.NET 标识](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project.md)
- MSDN 杂志使用 ASP.NET Identity 的 Dino Esposito 的[外部身份验证](https://msdn.microsoft.com/magazine/dn745860.aspx)
- MSDN 杂志[第一次](https://msdn.microsoft.com/magazine/dn605872.aspx)通过 Dino Esposito ASP.NET Identity
- [ASP.NET Identity –用户锁定](http://tech.trailmax.info/2014/06/asp-net-identity-user-lockout/)

<a id="samp"></a>

## <a name="where-to-ask-questions-request-features-report-a-bug-and-nightly-builds"></a>在何处提出问题，请求功能，报告 bug 和夜间生成

- 对于 StackOverflow，请使用标记[aspnet 标识](http://stackoverflow.com/questions/tagged/asp.net-identity)
- 对于 ASP.NET 论坛，请发布到[安全论坛](https://forums.asp.net/25.aspx)，并将**ASP.NET Identity**添加到标题中。
- [GitHub 上的 ASP.NET Identity](https://github.com/aspnet/AspNetIdentity)每夜生成，请求功能，打开 bug。

<a id="blog"></a>

## <a name="blog-posts-on-identity"></a>有关标识的博客文章

- [什么是 ASP.NET Identity 中的 SecurityStamp？](http://stackoverflow.com/questions/19487322/what-is-asp-net-identitys-iusersecuritystampstoretuser-interface/19505060#19505060)
- 作者： [John Atten](https://twitter.com/xivSolutions)

    - [ASP.NET Identity 2.0 扩展标识模型以及使用整数键而不是字符串](http://typecastexception.com/post/2014/07/13/ASPNET-Identity-20-Extending-Identity-Models-and-Using-Integer-Keys-Instead-of-Strings.aspx)
    - [ASP.NET Identity 2.0：自定义用户和角色](http://typecastexception.com/post/2014/06/22/ASPNET-Identity-20-Customizing-Users-and-Roles.aspx)
    - [ASP.NET MVC 和 Identity 2.0：了解基础知识](http://typecastexception.com/post/2014/04/20/ASPNET-MVC-and-Identity-20-Understanding-the-Basics.aspx)
    - [设置帐户验证和双重身份验证](http://typecastexception.com/post/2014/04/20/ASPNET-Identity-20-Setting-Up-Account-Validation-and-Two-Factor-Authorization.aspx)
    - [为 ASP.NET MVC 5 和 Visual Studio 2013 中的标识帐户配置 Db 连接和代码优先迁移](http://typecastexception.com/post/2013/10/27/Configuring-Db-Connection-and-Code-First-Migration-for-Identity-Accounts-in-ASPNET-MVC-5-and-Visual-Studio-2013.aspx)
- 作者： [Taiseer Joudeh](http://bitoftech.net/taiseer-joudeh-blog/)

    - [使用 ASP.NET Web API 2、Owin 中间件和 ASP.NET Identity 进行基于令牌的身份验证](http://bitoftech.net/2014/06/01/token-based-authentication-asp-net-web-api-2-owin-asp-net-identity/)
    - [使用 ASP.NET Web API 2、Owin 和 Identity 的 AngularJS 令牌身份验证](http://bitoftech.net/2014/06/09/angularjs-token-authentication-using-asp-net-web-api-2-owin-asp-net-identity/)
    - [使用 ASP .NET Web API 2 和 Owin –第3部分，在 AngularJS 应用中启用 OAuth 刷新令牌。](http://bitoftech.net/2014/07/16/enable-oauth-refresh-tokens-angularjs-app-using-asp-net-web-api-2-owin/)
- 作者： [Anders Abel](https://twitter.com/anders_abel)

    - [了解 Owin 外部身份验证管道](http://coding.abel.nu/2014/06/understanding-the-owin-external-authentication-pipeline/)
    - [ASP.NET Identity 和 Owin 概述](http://coding.abel.nu/2014/06/asp-net-identity-and-owin-overview/)

  作者： [Allen](https://twitter.com/OdeToCode)在 o) 上的代码

    - [ASP.NET Core 标识](http://odetocode.com/blogs/scott/archive/2013/11/25/asp-net-core-identity.aspx)此博客检查核心抽象，包括 IUser、IUserStore 和 I\*存储接口。
    - [与实体框架 ASP.NET Identity](http://odetocode.com/blogs/scott/archive/2014/01/03/asp-net-identity-with-the-entity-framework.aspx)MVC 5、Web API 和 SPA 应用中的单个用户帐户、连接字符串和管理上下文
    - [带有 ASP.NET Identity 的自定义选项](http://odetocode.com/blogs/scott/archive/2014/01/09/customization-options-with-asp-net-identity.aspx)
    - [实现 ASP.NET Identity](http://odetocode.com/blogs/scott/archive/2014/01/20/implementing-asp-net-identity.aspx)
- [Benjamin Day](http://www.benday.com/about/)[演练：通过 Microsoft 帐户身份验证 ASP.NET MVC 标识](http://www.benday.com/2014/02/25/walkthrough-asp-net-mvc-identity-with-microsoft-account-authentication/)
- [Brock Allen](https://twitter.com/BrockLAllen)

    - [使用 OWIN/Katana authentication 中间件的外部登录提供程序（社交登录）入门](http://brockallen.com/2014/01/09/a-primer-on-external-login-providers-social-logins-with-owinkatana-authentication-middleware/)
    - [介绍 IdentityReboot](http://brockallen.com/2014/02/11/introducing-identityreboot/)：一组用于实现我抱怨的主要缺少功能的 ASP.NET Identity 扩展。
- [Pranav Rastogi 撰写](https://twitter.com/rustd)

    - [从社交提供商获取详细信息](https://blogs.msdn.com/b/webdev/archive/2013/10/16/get-more-information-from-social-providers-used-in-the-vs-2013-project-templates.aspx)
- [@beabigrockstar](https://twitter.com/beabigrockstar) （Jerrie Pelser）

    - [双因素身份验证](http://www.beabigrockstar.com/blog/2-factor-authentication-with-asp-net-identity-2-0-beta-1/)
    - [将 Google 身份验证器与 ASP.NET Identity 配合使用](http://www.beabigrockstar.com/blog/using-google-authenticator-asp-net-identity/)
    - [ASP.NET MVC 5 身份验证指南](http://www.beabigrockstar.com/)
- [从 VS 2013 项目模板中使用的社交提供程序获取详细信息](https://blogs.msdn.com/b/webdev/archive/2013/10/16/get-more-information-from-social-providers-used-in-the-vs-2013-project-templates.aspx)
- [使用 ASP.NET Identity 生成简单的 ToDo 应用程序并将用户与 ToDoes 关联](https://blogs.msdn.com/b/webdev/archive/2013/10/20/building-a-simple-todo-application-with-asp-net-identity-and-associating-users-with-todoes.aspx)
- [ASP.NET Identity 的 Google OpenId 集成问题](http://blog.technovert.com/2014/01/google-openid-integration-issues-asp-net-identity/)如果收到错误： HTTP 错误404.15 –找不到请求筛选模块被配置为拒绝请求，其中查询字符串太长
- [IdentityManager 替换为 WSAT 的 Thinktecture](http://www.hanselman.com/blog/ThinktectureIdentityManagerAsAReplacementForTheASPNETWebSiteAdministrationTool.aspx)
- [使用 ASP.NET Web API 2、Owin 和 Identity 的 AngularJS 令牌身份验证](http://bitoftech.net/2014/06/09/angularjs-token-authentication-using-asp-net-web-api-2-owin-asp-net-identity/)
- [无实体框架的简单 Asp.net 标识核心](https://code.msdn.microsoft.com/Simple-Aspnet-Identiy-Core-7475a961)
- 通过[Sheo Narayan](http://www.dotnetfunda.com/profile/sheonarayan.aspx) [在 MVC ASP.NET Identity 中使用角色](http://www.dotnetfunda.com/articles/show/2898/working-with-roles-in-aspnet-identity-for-mvc)
- [转到从 ASP.NET 成员身份 ASP.NET Identity](http://webdojo.sharepoint.com/ajmatthews/_layouts/15/start.aspx#/Lists/Posts/Post.aspx?ID=2) Alistair Matthews

<a id="video"></a>

## <a name="videos"></a>视频

- 第9频道[：保护 ASP.NET 应用程序和服务： Ido Flatow 的新式应用程序的安全 Facelift](https://channel9.msdn.com/Events/TechEd/NorthAmerica/2014/DEV-B421#fbid=PhVT9E1WRtr?hashlink=fbid)
- 第9频道 ASP.NET Identity Pranav Rastogi 撰写[简介](https://channel9.msdn.com/Events/dotnetConf/2014/ASP-NET-Identity-Security)
- 第9频道[ASP.NET 使用 ASP.NET Identity](https://channel9.msdn.com/Shows/Web+Camps+TV/Special-Movember-Episode-ASPNET-Authentication-Provider)通过 Cory Fowler 进行身份验证
- 通道 9[构建新式 Web 应用： ASP.NET Identity](https://channel9.msdn.com/Series/Building-Modern-Web-Apps/03) Jeff Koch
- 第9频道：通过 Alex Thissen [ASP.NET Identity 保护你的网站](https://channel9.msdn.com/Events/TechDays/Techdays-2014-the-Netherlands/Securing-your-website-with-ASP-NET-Identity)
- 通过 Alexander Schmidt[使用现有 DB 模型上的 ASP.NET Identity](https://www.youtube.com/watch?v=elfqejow5hM)
- [ASP.NET](https://www.youtube.com/watch?v=w8GD-QIusKk) Ivaylo Kenov of Telerik
- [捷克 ASP.NET Identity](https://www.youtube.com/watch?v=tVbZp5brcpY)在此讲座中，我们将演示如何部署基本身份验证，如何添加对 Twitter 或 Facebook 等外部标识提供程序的支持，以及如何使用一次性密码（OTP）。 [ASP.NET Identity je nástupce 成员身份提供商&#367; ASP.NET、tedy knihovna pro zajišt&#283;ní autentizace uživatel。&#367; V této p&#345;ednášce si ukážeme，jak nasad]

<a id="cust"></a>

## <a name="custom-storage-providers-for-aspnet-identity"></a>ASP.NET Identity 的自定义存储提供程序

如果要编写自己的提供程序，请阅读[ASP.NET Identity 的自定义存储提供程序的概述](../extensibility/overview-of-custom-storage-providers-for-aspnet-identity.md)，并[实现 ASP.NET Identity](http://odetocode.com/blogs/scott/archive/2014/01/20/implementing-asp-net-identity.aspx) ，然后检查下面列出的其中一个 OSS 项目的来源。

- 教程： FitzMacken 的[自定义存储提供 ASP.NET Identity 程序概述](../extensibility/overview-of-custom-storage-providers-for-aspnet-identity.md)
- 博客：[实现 ASP.NET Identity](http://odetocode.com/blogs/scott/archive/2014/01/20/implementing-asp-net-identity.aspx)
- 教程：[设置基本标识帐户，并将其指向外部数据库](http://typecastexception.com/post/2013/10/27/Configuring-Db-Connection-and-Code-First-Migration-for-Identity-Accounts-in-ASPNET-MVC-5-and-Visual-Studio-2013.aspx)。 通过[@xivSolutions](https://twitter.com/xivSolutions)。
- 教程[：实现自定义 MySQL ASP.NET Identity 存储提供程序](../extensibility/implementing-a-custom-mysql-aspnet-identity-storage-provider.md)
- 按 James Randall) 的[Azure 表存储](https://www.nuget.org/packages/accidentalfish.aspnet.identity.azure/)。
- Azure 表存储：[表存储。](https://github.com/stuartleeks/leeksnet.AspNet.Identity.TableStorage)通过[@stuartleeks](https://twitter.com/stuartleeks)。
- [CouchDB/Cloudant by Daniel Wertheim。](https://github.com/danielwertheim/mycouch.aspnet.identity)
- [弹性搜索：](https://github.com/bmbsqd/elastic-identity) Bombsquad AB 的弹性标识。
- [MongoDB](http://www.nuget.org/packages/MongoDB.AspNet.Identity/) By Jonathan Sheely Jonathan Sheely。
- [NHibernate](https://github.com/milesibastos/NHibernate.AspNet.Identity) By Antônio Milesi Bastos。
- [RavenDB](http://www.nuget.org/packages/AspNet.Identity.RavenDB/1.0.0) [@tourismgeek](https://twitter.com/tourismgeek)。
- [ILMServices](http://www.ilmservice.com/)的[RavenDB](https://github.com/ILMServices/RavenDB.AspNet.Identity) 。
- Redis： [Redis](https://github.com/aminjam/Redis.AspNet.Identity)
- 用于为 "数据库第一个" 用户存储生成 EF 代码的 T4 模板： [EntityFramework](https://github.com/cbfrank/AspNet.Identity.EntityFramework)

<a id="additional"></a>

## <a name="additional-aspnet-identity-resources"></a>其他 ASP.NET Identity 资源

- [介绍 yahoo 和 Linkedin OAuth security providers FOR OWIN](http://blog.beabigrockstar.com/introducing-the-yahoo-linkedin-oauth-security-providers-for-owin/) By Jerrie Pelser for Yahoo 和 linkedin 说明。

<a id="qand"></a>

## <a name="qampa-questionanswer"></a>问答&amp;（问题/解答）

- 问：锁定了已启用 "记住我" 的用户（因此不需要在该计算机/浏览器上进行2FA）。为什么和如何防止这种情况？ [在此处](http://stackoverflow.com/questions/24312247/locked-out-users-can-login-if-they-have-auth-cookie)回答。
- **问**：我如何将自定义声明（例如用户的真实名称）存储在 ASP.NET Identity cookie 中，以避免对每个请求进行不必要的数据库查询。 [在此处](http://stackoverflow.com/questions/23622047/identity-cookie-loses-custom-claim-information-after-a-period-of-time)回答。
- **问：更新 AspNetUser 密码哈希**：我有2个项目。 其中一个使用 ASP.NET authentication，另一个使用 Windows 身份验证，这是管理端。 我希望管理项目能够管理另一个用户。 我可以修改除密码之外的所有内容。 [在此处回答](http://stackoverflow.com/questions/23880666/updating-aspnetuser-password-hash)。
- **问**：如何以管理员身份为其他用户重置密码？ [在此处](http://stackoverflow.com/questions/23783249/identity-2-0-reset-password-by-admin/24211766#24211766)回答。
- **问**：我是否可以在 ASP.NET MVC IdentityUser 中更改用户名字段的显示名称？ [在此处](http://stackoverflow.com/questions/23256650/can-i-change-the-displayed-name-of-the-username-field-in-asp-net-mvc-identityuse)回答。
- **问**：如何 gran 用户向特定角色添加其他用户的权限？ [在此处](http://stackoverflow.com/questions/23695373/allow-users-to-grant-permissions-to-other-users-for-their-account-in-asp-net-ide)回答。
- **问**：在 AspNetUsers 表与 AspNetUserClaims 表中存储配置文件信息。 [在此处](http://stackoverflow.com/questions/23215727/is-there-any-benefit-to-storing-user-information-in-aspnetuserclaims-with-asp-ne)回答。
- **问**：在使用外部身份验证提供程序时，请记住我。 [在此处](http://stackoverflow.com/questions/23180896/how-to-remember-the-login-in-mvc5-when-an-external-provider-is-used)回答。
- **问**：为什么每个请求都需要 ApplicationDBContext，这不会造成太大的开销？ 答：没有，开销较低。
- 问：如何实现获取已登录用户的列表？ [在此处](http://stackoverflow.com/questions/22995653/getting-a-list-of-logged-in-users-in-asp-net-identity/)回答。
- 问：如何在用户使用 Microsoft AspNet 标识登录时进行检测？ [在此处](http://stackoverflow.com/questions/22956486/how-can-i-detect-when-a-user-logs-in-with-microsoft-aspnet-identity/22970698#22970698)回答。
- 问：如何实现获取身份的本地化错误消息？ [在此处](http://stackoverflow.com/questions/22835981/asp-net-identity-localization-publickeytoken/22845864#22845864)回答。
- 问：如何实现将 CookieMiddleware 配置为每30分钟获得一次全新的声明？ [在此处](http://stackoverflow.com/questions/22682663/how-to-hold-the-cookies-claims-updated-with-mcv5-owin/22796932#22796932)回答。
- 问：用户登录后如何修改用户的声明？ [在此处](http://stackoverflow.com/questions/22768836/can-i-modify-claims-in-asp-net-identity-with-owin-after-calling-signin/22769963#22769963)回答。
- 问：如何实现使安全令牌无效？ [在此处](http://stackoverflow.com/questions/22755700/revoke-token-generated-by-usertokenprovider-in-asp-net-identity-2-0/22767286#22767286)回答。
- 问：如何将声明存储在 cookie 中间件？ [在此处](http://stackoverflow.com/questions/22320632/storing-retrieving-user-data-without-database-when-using-owin-cookie-authenticat/22541856#22541856)回答。
- 问：我想在 MVC 应用程序中对每个操作方法进行 PIN 或安全检查，但我希望存储用户成功，因此他们无需在每次向该操作方法发出请求时输入 PIN。 [在此处](http://stackoverflow.com/questions/22479958/security-check-an-user-to-a-access-controller-action/22486075#22486075)回答。
- 问：我想要将从社交提供商那里返回的电子邮件地址保存到数据库，如何实现此目的？ 答案[如下](http://stackoverflow.com/questions/22888397/save-claims-to-db-on-login/22970969#22970969)：
- 问：我如何检测用户是否同时用/注销 "记住我" cookie？ [在此处](http://stackoverflow.com/questions/22956486/how-can-i-detect-when-a-user-logs-in-with-microsoft-aspnet-identity/22970698#22970698)回答。
- 问：是否可以在调用登录后，在 OWIN 中修改声明 ASP.NET Identity？ 答：如果你想要修改用户的声明，则调用登录就正是你应该执行的操作。 它基本上会使 ClaimsIdentity 序列化为 cookie，这就是在后续请求上显示新声明的原因。
