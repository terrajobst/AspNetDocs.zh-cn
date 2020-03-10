---
uid: web-forms/overview/older-versions-security/introduction/forms-authentication-configuration-and-advanced-topics-cs
title: Forms 身份验证配置和高级主题C#（） |Microsoft Docs
author: rick-anderson
description: 在本教程中，我们将检查各种 forms 身份验证设置，并查看如何通过 forms 元素修改这些设置。 这将需要更详细的 。
ms.author: riande
ms.date: 01/14/2008
ms.assetid: b9c29865-a34e-48bb-92c0-c443a72cb860
msc.legacyurl: /web-forms/overview/older-versions-security/introduction/forms-authentication-configuration-and-advanced-topics-cs
msc.type: authoredcontent
ms.openlocfilehash: b296f31da1c73df97175d94402b4d618df425d8d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78521372"
---
# <a name="forms-authentication-configuration-and-advanced-topics-c"></a>Forms 身份验证配置和高级主题 (C#)

作者： [Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载代码](https://download.microsoft.com/download/2/F/7/2F705A34-F9DE-4112-BBDE-60098089645E/ASPNET_Security_Tutorial_03_CS.zip)或[下载 PDF](https://download.microsoft.com/download/2/F/7/2F705A34-F9DE-4112-BBDE-60098089645E/aspnet_tutorial03_AuthAdvanced_cs.pdf)

> 在本教程中，我们将检查各种 forms 身份验证设置，并查看如何通过 forms 元素修改这些设置。 这将需要详细了解如何使用带有自定义 URL （如登录 .aspx 而不是登录 .aspx）和无 cookie forms 身份验证票证的登录页自定义 forms 身份验证票证的超时值。

## <a name="introduction"></a>简介

在[上一教程](an-overview-of-forms-authentication-cs.md)中，我们介绍了在 ASP.NET 应用程序中实现 forms 身份验证所需的步骤，从在 web.config 中指定配置设置到创建登录页，以便为经过身份验证的用户和匿名用户显示不同的内容。 回忆一下，我们已将网站配置为使用 forms 身份验证，方法是将 &lt;authentication&gt; 元素的 mode 属性设置为 Forms。 &lt;authentication&gt; 元素可以选择性地包括 &lt;窗体&gt; 子元素，通过该元素可以指定一种形式的窗体身份验证设置。

在本教程中，我们将检查各种 forms 身份验证设置，并查看如何通过 &lt;窗体&gt; 元素来修改它们。 这将需要详细了解如何使用带有自定义 URL （如登录 .aspx 而不是登录 .aspx）和无 cookie forms 身份验证票证的登录页自定义 forms 身份验证票证的超时值。 我们还将更仔细地检查 forms 身份验证票证的构成，并了解 ASP.NET 采取的措施，以确保票证的数据免受检查和篡改。 最后，我们将介绍如何将额外的用户数据存储在 forms 身份验证票证中，以及如何通过自定义主体对象对此数据建模。

## <a name="step-1-examining-the-ltformsgt-configuration-settings"></a>步骤1：检查 &lt;窗体&gt; 配置设置

ASP.NET 中的 forms 身份验证系统提供了许多配置设置，这些设置可根据应用程序进行自定义。 这包括如下设置： forms 身份验证票证的生存期;对票证应用哪种类型的保护;在什么情况下使用无 cookie 身份验证票证;登录页的路径;和其他信息。 若要修改默认值，请将[&lt;窗体&gt; 元素](https://msdn.microsoft.com/library/1d3t3c61.aspx)添加为[&lt;authentication&gt; 元素](https://msdn.microsoft.com/library/532aee0e.aspx)的子元素，并指定要自定义为类似于 XML 特性的属性值，如下所示：

[!code-xml[Main](forms-authentication-configuration-and-advanced-topics-cs/samples/sample1.xml)]

表1汇总了可通过 &lt;窗体&gt; 元素自定义的属性。 由于 web.config 是一个 XML 文件，左栏中的属性名称区分大小写。

| <strong>特性</strong> |                                                                                                                                                                                                                                     <strong>描述</strong>                                                                                                                                                                                                                                      |
|----------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|         无         |                                                                                                                此属性指定在什么条件下，在 cookie 中存储身份验证票证，而不是将其嵌入到 URL 中。 允许的值为： UseCookies;UseUri;检测和 UseDeviceProfile （默认值）。 步骤2更详细地检查此设置。                                                                                                                |
|         defaultUrl         |                                                                                                                                                         如果查询字符串中未指定 RedirectUrl 值，则指示从登录页登录后用户重定向到的 URL。 默认值为 default.aspx。                                                                                                                                                         |
|           域           | 使用基于 cookie 的身份验证票证时，此设置指定 cookie 的域值。 默认值为空字符串，这将使浏览器使用其发出的域（如 www.yourdomain.com）。 在这种情况下，在向子域发出请求（如 admin.yourdomain.com）时，<strong>不</strong>会发送 cookie。 如果希望将 cookie 传递给所有子域，则需要自定义域属性将其设置为 yourdomain.com。 |
|  enableCrossAppRedirects   |                                                                                                                                                                   一个布尔值，指示在重定向到同一服务器上的其他 web 应用程序中的 Url 时是否记住经过身份验证的用户。 默认值为 false。                                                                                                                                                                   |
|          loginUrl          |                                                                                                                                                                                                                      登录页的 URL。 默认值为 login.aspx。                                                                                                                                                                                                                      |
|            NAME            |                                                                                                                                                                                                   使用基于 cookie 的身份验证票证时，该 cookie 的名称。 默认值为.ASPXAUTH.                                                                                                                                                                                                   |
|            path            |                                                                             使用基于 cookie 的身份验证票证时，此设置会指定 cookie 的 path 属性。 使用 path 特性，开发人员可以将 cookie 的作用域限制为特定的目录层次结构。 默认值为/，通知浏览器将身份验证票证 cookie 发送到向域发出的任何请求。                                                                              |
|         保护         |                                                                                                                                            指示用于保护 forms 身份验证票证的技术。 允许的值为： All （默认值）;密匙内容和验证。 步骤3中详细讨论了这些设置。                                                                                                                                            |
|         requireSSL         |                                                                                                                                                                                一个布尔值，指示是否需要 SSL 连接来传输身份验证 cookie。 默认值为 False。                                                                                                                                                                                |
|     slidingExpiration      |                                                                                                 一个布尔值，该值指示每次用户在单个会话期间访问站点时是否重置身份验证 cookie 的超时。 默认值为 true。 在指定票证的超时值部分中更详细地讨论了身份验证票证超时策略。                                                                                                 |
|          超时           |                                                                                                                               指定身份验证票证 cookie 过期的时间，以分钟为单位。 默认值为 30。 在指定票证的超时值部分中更详细地讨论了身份验证票证超时策略。                                                                                                                               |

**表 1**： &lt;窗体&gt; 元素属性的摘要

在 ASP.NET 2.0 和更高版本中，默认的窗体身份验证值在 .NET Framework 的 FormsAuthenticationConfiguration 类中进行硬编码。 在 web.config 文件中，必须逐个应用程序应用任何修改。 这不同于 ASP.NET 1.x，其中默认的 forms 身份验证值存储在 machine.config 文件中（因此可以通过编辑 machine.config 进行修改）。 尽管在 ASP.NET 1.x 的主题中，有必要说，在 ASP.NET 2.0 和 ASP.NET 1.x 中，许多 forms 身份验证系统设置具有不同的默认值。 如果要从 ASP.NET 1.x 环境迁移应用程序，请务必了解这些差异。 有关差异列表，请参阅[&lt;窗体&gt; 元素技术文档](https://msdn.microsoft.com/library/1d3t3c61.aspx)。

> [!NOTE]
> 多种 forms 身份验证设置（如超时、域和路径）为生成的 forms 身份验证票证 cookie 指定详细信息。 若要详细了解 cookie 及其工作原理，请阅读[此 cookie 教程](http://www.quirksmode.org/js/cookies.html)。

### <a name="specifying-the-tickets-timeout-value"></a>指定票证的超时值

Forms 身份验证票证是表示标识的令牌。 通过基于 cookie 的身份验证票证，此令牌以 cookie 的形式保存，并在每个请求上发送到 web 服务器。 该令牌的所有权实质上是声明的，我是*用户名*，我已经登录了，并使用了，这样就可以在页面访问之间记住用户的标识。

Forms 身份验证票证不仅包括用户的标识，还包含有助于确保令牌的完整性和安全性的信息。 毕竟，我们不希望恶意用户能够创建假冒令牌，或以某种 underhanded 的方式修改 legit 令牌。

票证中包含的一项信息是*过期*时间，即票证不再有效的日期和时间。 每次 FormsAuthenticationModule 检查一个身份验证票证时，它都会确保票证的到期时间尚未过。 如果已存在，它将忽略票证，并将用户标识为匿名用户。 此安全措施有助于防止重放攻击。 如果黑客能够亲自进入用户的有效身份验证票证（也许是通过获取其计算机的物理访问权限，并通过其 cookie 定位），就不会过期，他们可以使用此盗用的身份验证票证向服务器发送请求，获取项。 尽管过期不会阻止这种情况发生，但它确实限制了此类攻击可以成功的窗口。

> [!NOTE]
> 步骤3详细说明 forms authentication 系统用来保护身份验证票证的其他技术。

创建身份验证票证时，forms 身份验证系统通过查阅超时设置来确定其过期时间。 如表1所示，超时设置默认为30分钟，这意味着在创建 forms 身份验证票证时，其过期时间设置为将来的日期和时间30分钟。

当表单身份验证票证到期时，到期定义将来的绝对时间。 但通常情况下，开发人员需要实现一个可调过期，每次用户回顾站点时都会重置。 此行为由 slidingExpiration 设置确定。 如果设置为 true （默认值），则每次 FormsAuthenticationModule 对用户进行身份验证时，将更新票证的过期时间。 如果设置为 false，则不会对每个请求更新过期时间，从而导致票证的过期时间与首次创建票证时的超时时间完全相同。

> [!NOTE]
> 身份验证票证中存储的过期时间是一个绝对日期和时间值，如8月2日，2008 11:34 AM。 而且，日期和时间是相对于 web 服务器的本地时间。 此设计决策可能会对夏令时（DST）产生一些有趣的副作用，即，将美国中的时钟移到一小时后（假定 web 服务器在观察到夏令时的区域设置中）。 考虑在 DST 开始（上午2:00 点）接近30分钟过期后，ASP.NET 网站会发生什么情况。 假设有一个访问者在2008年3月11日上午1:55 登录到网站。 这会生成一个 forms 身份验证票证，该票证将于 2:25 2008 年3月11日（在未来30分钟）过期。 但是，在 2:00 AM 之后，时钟将跳转到 3:00 AM （由于 DST）。 如果用户在登录后六分钟加载新页（上午3:01），则 FormsAuthenticationModule 会注意到票证已过期，并将用户重定向到登录页。 有关此和其他身份验证票证超时问题以及解决方法的详细讨论，请选择 Stefan Schackow 的*ASP.NET 2.0 安全性、成员身份和角色管理*的副本（ISBN：978-0-7645-9698-8）。

图1说明了 slidingExpiration 设置为 false 时的工作流，而 timeout 设置为30。 请注意，在登录时生成的身份验证票证包含过期日期，此值不会在后续请求上更新。 如果 FormsAuthenticationModule 发现票证已过期，则会将其丢弃并将请求视为匿名。

[![slidingExpiration 为 false 时 Forms 身份验证票证到期的图形表示形式](forms-authentication-configuration-and-advanced-topics-cs/_static/image2.png)](forms-authentication-configuration-and-advanced-topics-cs/_static/image1.png)

**图 01**： slidingExpiration 为 False 时 Forms 身份验证票证到期的图形表示形式（[单击以查看完全大小的映像](forms-authentication-configuration-and-advanced-topics-cs/_static/image3.png)）

图2显示了当 slidingExpiration 设置为 true 且 timeout 设置为30时的工作流。 接收到身份验证的请求（具有非过期票证）后，其过期时间将更新到将来的超时分钟数。

[当 slidingExpiration 为 true 时，![Forms 身份验证票证的图形表示形式](forms-authentication-configuration-and-advanced-topics-cs/_static/image5.png)](forms-authentication-configuration-and-advanced-topics-cs/_static/image4.png)

**图 02**： slidingExpiration 为 True 时 Forms 身份验证票证的图形表示形式（[单击以查看完全大小的图像](forms-authentication-configuration-and-advanced-topics-cs/_static/image6.png)）

使用基于 cookie 的身份验证票证（默认值）时，此讨论就变得更加混乱，因为 cookie 还可以指定其自己的 expiries。 Cookie 的过期时间（或缺少此 cookie）会指示浏览器应销毁 cookie。 如果 cookie 缺少过期时间，则会在浏览器关闭时销毁该 cookie。 但是，如果存在过期，cookie 会一直存储在用户的计算机上，直到过期指定的日期和时间。 当浏览器销毁 cookie 时，它将不再发送到 web 服务器。 因此，cookie 的销毁类似于用户注销站点。

> [!NOTE]
> 当然，用户可以主动删除存储在计算机上的任何 cookie。 在 Internet Explorer 7 中，你将转到 "工具"、"选项"，然后单击 "浏览历史记录" 部分中的 "删除" 按钮。 在该处单击 "删除 cookie" 按钮。

Forms 身份验证系统根据传入到*persistCookie*参数的值创建基于会话或基于过期的 cookie。 回忆一下，FormsAuthentication 类的 GetAuthCookie、SetAuthCookie 和 Formsauthentication.redirectfromloginpage 方法采用两个输入参数： *username*和*persistCookie*。 在前面的教程中创建的登录页面包含一个 "记住我" 复选框，该复选框确定是否创建了持久性 cookie。 永久性 cookie 基于过期;非持久性 cookie 是基于会话的。

已讨论的超时和 slidingExpiration 概念对基于会话和过期的 cookie 同样适用。 在执行过程中只有一个细微差异：在将 slidingTimeout 设置为 true 时使用基于过期的 cookie 时，仅当超过指定时间的一半时才会更新 cookie 的过期时间。

让我们更新网站的身份验证票证超时策略，以便在一小时（60分钟）后使用滑动过期时间超时。 若要使此更改生效，请更新 Web.config 文件，将 &lt;窗体&gt; 元素添加到具有以下标记的 &lt;authentication&gt; 元素：

[!code-xml[Main](forms-authentication-configuration-and-advanced-topics-cs/samples/sample2.xml)]

### <a name="using-an-login-page-url-other-than-loginaspx"></a>使用除 Login 以外的登录页 URL

由于 FormsAuthenticationModule 会自动将未经授权的用户重定向到登录页，因此它需要知道登录页的 URL。 此 URL 由 &lt;窗体&gt; 元素中的 loginUrl 属性指定，并且默认为登录 .aspx。 如果要在现有网站上进行迁移，则可能已经有一个具有不同 URL 的登录页面，搜索引擎已将这些页面设置为书签并进行索引。 您可以改为将 loginUrl 属性修改为指向登录页，而不是将您的现有登录页重命名为 .aspx 并断开链接和用户的书签。

例如，如果您的登录页命名为 login .aspx 并且位于用户目录中，则可以将 loginUrl 配置设置指向 ~/Users/SignIn.aspx，如下所示：

[!code-xml[Main](forms-authentication-configuration-and-advanced-topics-cs/samples/sample3.xml)]

由于当前应用程序已经有一个名为 "Login" 的登录页，因此无需在 &lt;窗体&gt; 元素中指定自定义值。

## <a name="step-2-using-cookieless-forms-authentication-tickets"></a>步骤2：使用无 Cookie Forms 身份验证票证

默认情况下，窗体身份验证系统将确定是将其身份验证票证存储在 cookie 集合中，还是将其嵌入到基于访问站点的用户代理的 URL 中。 所有主流桌面浏览器（如 Internet Explorer、Firefox、Opera 和 Safari）都支持 cookie，但并非所有移动设备都支持。

Forms 身份验证系统使用的 cookie 策略取决于 &lt;窗体&gt; 元素中的无 cookie 设置，可以为其分配以下四个值之一：

- UseCookies-指定将始终使用基于 cookie 的身份验证票证。
- UseUri-指示将从不使用基于 cookie 的身份验证票证。
- 自动检测-如果设备配置文件不支持 cookie，则不使用基于 cookie 的身份验证票证;如果设备配置文件支持 cookie，则使用探测机制来确定是否启用了 cookie。
- UseDeviceProfile-默认值;如果设备配置文件支持 cookie，则使用基于 cookie 的身份验证票证。 不使用探测机制。

自动检测和 UseDeviceProfile 设置依赖于认定中的*设备配置文件*，无论使用基于 cookie 还是无 cookie 身份验证票证。 ASP.NET 维护各种设备及其功能的数据库，例如它们是否支持 cookie、它们支持的 JavaScript 版本等。 每次设备从 web 服务器请求网页时，它将沿标识设备类型的*用户代理*HTTP 标头进行发送。 ASP.NET 自动将提供的用户代理字符串与在其数据库中指定的相应配置文件进行匹配。

> [!NOTE]
> 此设备功能数据库存储在多个符合[浏览器定义文件架构](https://msdn.microsoft.com/library/ms228122.aspx)的 XML 文件中。 默认设备配置文件位于%WINDIR%\Microsoft.Net\Framework\v2.0.50727\CONFIG\Browsers. 中。 你还可以将自定义文件添加到应用程序\_浏览器 "文件夹中。 有关详细信息，请参阅[如何：在 ASP.NET 网页中检测浏览器类型](https://msdn.microsoft.com/library/3yekbd5b.aspx)。

由于默认设置为 UseDeviceProfile，因此当站点被其配置文件报告不支持 cookie 的设备访问该站点时，将使用无 cookie forms 身份验证票证。

### <a name="encoding-the-authentication-ticket-in-the-url"></a>编码 URL 中的身份验证票证

Cookie 是将每个请求中的信息从浏览器中包括到特定网站的自然媒介，这就是默认表单身份验证设置在访问设备支持 cookie 时使用 cookie 的原因。 如果不支持 cookie，则必须采用备用方法将身份验证票证从客户端传递到服务器。 在无 cookie 环境中使用的常见解决方法是在 URL 中编码 cookie 数据。

若要查看如何将此类信息嵌入 URL，最佳方法是强制站点使用无 cookie 的身份验证票证。 为此，可将无 cookie 的配置设置设置为 UseUri：

[!code-xml[Main](forms-authentication-configuration-and-advanced-topics-cs/samples/sample4.xml)]

做出此更改后，请通过浏览器访问站点。 作为匿名用户访问时，Url 看起来就像以前一样。 例如，在访问 default.aspx 页面时，浏览器的地址栏会显示以下 URL：

`http://localhost:2448/ASPNET\_Security\_Tutorial\_03\_CS/default.aspx`

但是，登录后，表单身份验证票证将嵌入到 URL 中。 例如，在访问登录页并以 Sam 身份登录后，我将返回到 default.aspx 页，但这一次，URL 如下：

`http://localhost:2448/ASPNET\_Security\_Tutorial\_03\_CS/(F(jaIOIDTJxIr12xYS-VVgkqKCVAuIoW30Bu0diWi6flQC-FyMaLXJfow\_Vd9GZkB2Cv-rfezq0gKadKX0YPZCkA2))/default.aspx`

Forms 身份验证票证已嵌入到 URL 中。 字符串（F （jaIOIDTJxIr12xYS-VVgkqKCVAuIoW30Bu0diWi6flQC-FyMaLXJfow\_Vd9GZkB2Cv-rfezq0gKadKX0YPZCkA2）表示十六进制编码的身份验证票证信息，并且是通常存储在 cookie 内的相同数据。

为了使无 cookie 身份验证票证正常工作，系统必须对页面上的所有 Url 进行编码以包括身份验证票证数据，否则当用户单击链接时，身份验证票证将丢失。 令人欣慰，此嵌入逻辑将自动执行。 若要演示此功能，请打开 default.aspx 页并添加一个超链接控件，并将其 Text 和 NavigateUrl 属性设置为 Test Link and SomePage。 不重要的是，我们的项目中不存在名为 SomePage 的页。

保存对 default.aspx 的更改，然后通过浏览器进行访问。 登录到站点，使 forms 身份验证票证嵌入到 URL 中。 接下来，从 default.aspx，单击 "测试链接" 链接。 这是怎么回事？ 如果不存在名为 SomePage 的页，则会出现404错误，但此处不重要。 而是在浏览器的地址栏上重点介绍。 请注意，它在 URL 中包含 forms 身份验证票证！

`http://localhost:2448/ASPNET\_Security\_Tutorial\_03\_CS/(F(jaIOIDTJxIr12xYS-VVgkqKCVAuIoW30Bu0diWi6flQC-FyMaLXJfow\_Vd9GZkB2Cv-rfezq0gKadKX0YPZCkA2))/SomePage.aspx`

链接中的 URL SomePage 已自动转换为包含身份验证票证的 URL-我们无需编写代码的舔！ 对于不以 `http://` 或 `/`开头的任何超链接，窗体身份验证票证将自动嵌入在 URL 中。 如果超链接出现在对响应的调用中，则不重要。重定向、超链接控件或定位点 HTML 元素（即 `<a href="...">...</a>`）。 只要 URL 不像 `http://www.someserver.com/SomePage.aspx` 或 `/SomePage.aspx`，就会嵌入 forms 身份验证票证。

> [!NOTE]
> 无 cookie forms 身份验证票证遵循与基于 cookie 的身份验证票证相同的超时策略。 但是，无 cookie 身份验证票证更容易重播攻击，因为身份验证票证直接嵌入 URL。 假设访问某个网站的用户登录，然后将其电子邮件中的 URL 粘贴到同事。 如果同事在达到过期之前单击了该链接，他们将以发送电子邮件的用户身份登录！

## <a name="step-3-securing-the-authentication-ticket"></a>步骤3：保护身份验证票证

Forms 身份验证票证是通过网络传输的，无论是在 cookie 中还是直接嵌入在 URL 中。 除了标识信息，身份验证票证还可以包含用户数据（如我们将在步骤4中看到的那样）。 因此，对票证的数据进行加密非常重要，因为 forms 身份验证系统可以保证票证不被篡改，这一点更重要。

为了确保票证的数据的隐私，表单身份验证系统可以加密票证数据。 未能加密票证数据会以纯文本格式通过网络发送潜在的敏感信息。

为了保证票证的真实性，forms authentication 系统必须*验证*该票证。 验证是指确保一段特定的数据未修改，并通过 *[消息身份验证代码（MAC）](http://en.wikipedia.org/wiki/Message_authentication_code)* 来实现的行为。 简而言之，MAC 是一小部分信息，用于标识需要验证的数据（在本例中为票据）。 如果修改了 MAC 表示的数据，则 MAC 和数据将不会匹配。 此外，为黑客提供一项计算工作来修改数据并生成自己的 MAC 以与修改后的数据相对应。

在创建（或修改）票证时，forms 身份验证系统将创建一个 MAC 并将其附加到票证的数据上。 当后续请求到达时，forms 身份验证系统会比较 MAC 和票证数据，以验证票证数据的真实性。 图3以图形方式说明了此工作流。

[![通过 MAC 确保票证的真实性](forms-authentication-configuration-and-advanced-topics-cs/_static/image8.png)](forms-authentication-configuration-and-advanced-topics-cs/_static/image7.png)

**图 03**：通过 MAC 确保票证的真实性（[单击以查看完全大小的映像](forms-authentication-configuration-and-advanced-topics-cs/_static/image9.png)）

应用于身份验证票证的安全措施取决于 &lt;forms&gt; 元素中的保护设置。 可以将保护设置分配给以下三个值之一：

- 所有-票证都是加密和数字签名（默认值）。
- 应用仅加密加密-不生成 MAC。
- 无-不加密票证，也不进行数字签名。
- 验证-生成 MAC，但票证数据是以纯文本格式通过网络发送的。

Microsoft 强烈建议使用 "全部" 设置。

### <a name="setting-the-validation-and-decryption-keys"></a>设置验证密钥和解密密钥

Forms authentication 系统用来加密和验证身份验证票证的加密和哈希算法可通过 Web.config 中[&lt;machineKey&gt; 元素](https://msdn.microsoft.com/library/w8h3skw9.aspx)进行自定义。表2列出了 &lt;machineKey&gt; 元素的属性及其可能的值。

| **特性** | **描述** |
| --- | --- |
| 解密 | 指示用于加密的算法。 此属性可以具有以下四个值之一：-Auto-默认值;确定基于 decryptionKey 属性长度的算法。 -AES-使用[高级加密标准（AES）](http://en.wikipedia.org/wiki/Advanced_Encryption_Standard)算法。 -DES-使用[数据加密标准（DES）](http://en.wikipedia.org/wiki/Data_Encryption_Standard)此算法被视为计算弱，不应使用。 -3DES-使用三重[des 算法，该算法通过](http://en.wikipedia.org/wiki/Triple_DES)应用 DES 算法三次来运行。 |
| decryptionKey | 加密算法使用的密钥。 此值必须是适当长度的十六进制字符串（基于解密的值）、自动生成或追加的值 IsolateApps。 添加 IsolateApps 将指示 ASP.NET 为每个应用程序使用唯一值。 默认值为自动生成 IsolateApps。 |
| 验证 | 指示用于验证的算法。 此属性可以具有以下四个值之一：-AES-使用高级加密标准（AES）算法。 -MD5-使用[消息摘要5（MD5）](http://en.wikipedia.org/wiki/MD5)算法。 -SHA1-使用[sha1](http://en.wikipedia.org/wiki/Sha1)算法（默认值）。 -3DES-使用三重 DES 算法。 |
| validationKey | 验证算法使用的机密密钥。 此值必须是适当长度的十六进制字符串（基于验证中的值）、自动生成或追加的值 IsolateApps。 添加 IsolateApps 将指示 ASP.NET 为每个应用程序使用唯一值。 默认值为自动生成 IsolateApps。 |

**表 2**： &lt;MachineKey&gt; 元素特性

全面讨论了这些加密和验证选项以及各种算法的优缺点，这超出了本教程的范围。 若要深入了解这些问题，包括有关要使用哪些加密和验证算法、要使用哪些密钥长度以及如何最好地生成这些密钥的指导，请参阅*专业 ASP.NET 2.0 安全性、成员身份和角色管理*。

默认情况下，将为每个应用程序自动生成用于加密和验证的密钥，这些密钥存储在本地安全机构（LSA）中。 简而言之，默认设置在 web 服务器和应用程序的基础上确保唯一的密钥。 因此，此默认行为不适用于以下两种情况：

- **Web 场**-在[web 场](http://en.wikipedia.org/wiki/Web_farm)方案中，单个 web 应用程序托管在多个 web 服务器上，以实现可伸缩性和冗余。 每个传入请求将被分派给场中的服务器，这意味着在用户会话的整个生存期内，可以使用不同的服务器来处理其不同的请求。 因此，每个服务器都必须使用相同的加密密钥和验证密钥，以便可以在服务器场中的其他服务器上解密和验证在一台服务器上创建、加密和验证的 forms 身份验证票证。
- **跨应用程序票证共享**-单个 web 服务器可以承载多个 ASP.NET 应用程序。 如果需要将这些不同的应用程序共享单个 forms 身份验证票证，则其加密和验证密钥必须匹配。

在 web 场中工作或在同一服务器上的应用程序之间共享身份验证票证时，需要在受影响的应用程序中配置 &lt;machineKey&gt; 元素，使其 decryptionKey 和 validationKey 值匹配。

尽管上述方案均不适用于我们的示例应用程序，但我们仍可以指定显式 decryptionKey 和 validationKey 值，并定义要使用的算法。 向 Web.config 文件添加一个 &lt;machineKey&gt; 设置：

[!code-xml[Main](forms-authentication-configuration-and-advanced-topics-cs/samples/sample5.xml)]

有关详细信息，请参阅[如何：配置 MachineKey in ASP.NET 2.0](https://msdn.microsoft.com/library/ms998288.aspx)。

> [!NOTE]
> DecryptionKey 和 validationKey 值取自[Steve Gibson](http://www.grc.com/stevegibson.htm)的 "[完美密码" 网页](https://www.grc.com/passwords.htm)，这会在每个页面访问时生成64个随机十六进制字符。 为了减少这些密钥进入生产应用程序的可能性，建议你将上述密钥替换为从完美密码页面随机生成的密钥。

## <a name="step-4-storing-additional-user-data-in-the-ticket"></a>步骤4：将其他用户数据存储在票证中

许多 web 应用程序都在当前登录的用户上显示有关或使页面显示的信息。 例如，网页可能会显示用户的名称以及每个页面上一次登录的日期。 Forms 身份验证票证存储当前登录的用户的用户名，但当需要任何其他信息时，该页必须发送到用户存储区（通常为数据库）来查找未存储在身份验证票证中的信息。

使用少量代码，我们可以在 forms 身份验证票证中存储其他用户信息。 此类数据可以通过[FormsAuthenticationTicket 类](https://msdn.microsoft.com/library/system.web.security.formsauthenticationticket.aspx)的[UserData 属性](https://msdn.microsoft.com/library/system.web.security.formsauthenticationticket.userdata.aspx)来表示。 这是一个有用的位置，用于放置通常需要的有关用户的少量信息。 在 "UserData" 属性中指定的值作为身份验证票证 cookie 的一部分包含在内，如其他票证字段一样，会根据 forms 身份验证系统的配置对其进行加密和验证。 默认情况下，UserData 为空字符串。

若要在身份验证票证中存储用户数据，我们需要在登录页中编写一些代码来获取特定于用户的信息，并将其存储在票证中。 由于 UserData 是字符串类型的属性，因此中存储的数据必须正确地序列化为字符串。 例如，假设用户存储包含每个用户的出生日期和其雇主的名称，并且我们希望将这两个属性值存储在身份验证票证中。 我们可以通过使用竖线（|）将用户的出生日期字符串连接到字符串，后跟雇主姓名，将这些值序列化为一个字符串。 对于在1974年8月15日（适用于 Northwind 商贸）的用户，我们将为 UserData 属性分配字符串： 1974-08-15 |Northwind 商贸。

每当需要访问存储在票证中的数据时，我们都可以通过获取当前请求的 FormsAuthenticationTicket 并反序列化 UserData 属性来实现此目的。 如果是出生日期和雇主姓名示例，我们会根据分隔符（|）将 UserData 字符串拆分为两个子字符串。

[![可以在身份验证票证中存储其他用户信息](forms-authentication-configuration-and-advanced-topics-cs/_static/image11.png)](forms-authentication-configuration-and-advanced-topics-cs/_static/image10.png)

**图 04**：其他用户信息可以存储在身份验证票证中（[单击以查看完全大小的映像](forms-authentication-configuration-and-advanced-topics-cs/_static/image12.png)）

### <a name="writing-information-to-userdata"></a>将信息写入 UserData

遗憾的是，将特定于用户的信息添加到 forms 身份验证票证并不像预期那样简单。 FormsAuthenticationTicket 类的 UserData 属性是只读的，并且只能通过 FormsAuthenticationTicket 类构造函数指定。 在构造函数中指定 UserData 属性时，我们还需要提供票证的其他值：用户名、发行日期、到期时间等。 当我们在上一教程中创建登录页时，此操作由 FormsAuthentication 类处理。 将 UserData 添加到 FormsAuthenticationTicket 时，需要编写代码来复制 FormsAuthentication 类已经提供的大部分功能。

让我们来了解通过更新 "登录 .aspx" 页来记录用户对身份验证票证的其他信息时使用的必要代码。 假设我们的用户存储区包含用户使用的公司的相关信息及其标题，并想要在身份验证票证中捕获此信息。 更新登录 .aspx 页的 LoginButton 单击事件处理程序，使代码如下所示：

[!code-csharp[Main](forms-authentication-configuration-and-advanced-topics-cs/samples/sample6.cs)]

让我们每次逐行执行此代码。 方法首先定义四个字符串数组：用户、密码、公司名称和 titleAtCompany。 这些数组保存系统中用户帐户的用户名、密码、公司名称和标题，其中有三个： Scott、Jisun 和 Sam。 在实际应用程序中，将从用户存储区中查询这些值，而不是在页面的源代码中进行硬编码。

在上一教程中，如果提供的凭据有效，我们只需调用 FormsAuthentication Formsauthentication.redirectfromloginpage （RememberMe），这会执行以下步骤：

1. 已创建 forms 身份验证票证
2. 已将票证写入适当的商店。 对于基于 cookie 的身份验证票证，使用浏览器的 cookie 集合;对于无 cookie 身份验证票证，会将票证数据序列化为 URL
3. 将用户重定向到适当页面

这些步骤将在上面的代码中进行复制。 首先，我们最终存储在 UserData 属性中的字符串是通过组合公司名称和标题组成的，并用竖线字符（|）分隔这两个值。

string userDataString = string.Concat(companyName[i], "|", titleAtCompany[i]);

接下来，调用 FormsAuthentication GetAuthCookie 方法，该方法将创建身份验证票证，根据配置设置对其进行加密和验证，然后将其放在 HttpCookie 对象中。

HttpCookie authCookie = FormsAuthentication.GetAuthCookie(UserName.Text, RememberMe.Checked);

若要处理 cookie 中嵌入的 FormAuthenticationTicket，需要调用 FormAuthentication 类的[解密方法](https://msdn.microsoft.com/library/system.web.security.formsauthentication.decrypt.aspx)，并传入 cookie 值。

FormsAuthenticationTicket ticket = FormsAuthentication.Decrypt(authCookie.Value);

然后，基于现有 FormsAuthenticationTicket 的值创建一个*新*的 FormsAuthenticationTicket 实例。 但是，此新票证包含用户特定的信息（userDataString）。

FormsAuthenticationTicket newTicket = new FormsAuthenticationTicket(ticket.Version, ticket.Name, ticket.IssueDate, ticket.Expiration, ticket.IsPersistent, userDataString);

然后，通过调用[encrypt 方法](https://msdn.microsoft.com/library/system.web.security.formsauthentication.encrypt.aspx)加密（和验证）新的 FormsAuthenticationTicket 实例，并将此加密（和验证）数据放回到 authCookie 中。

authCookie.Value = FormsAuthentication.Encrypt(newTicket);

最后，authCookie 将添加到响应中。 Cookie 集合和调用 GetRedirectUrl 方法，以确定发送用户的相应页面。

[!code-csharp[Main](forms-authentication-configuration-and-advanced-topics-cs/samples/sample7.cs)]

所有这些代码都是必需的，因为 UserData 属性是只读的，而 FormsAuthentication 类不提供任何用于在其 GetAuthCookie、SetAuthCookie 或 Formsauthentication.redirectfromloginpage 方法中指定 UserData 信息的方法。

> [!NOTE]
> 我们刚才检查的代码将用户特定的信息存储在基于 cookie 的身份验证票证中。 负责将 forms 身份验证票证序列化为 URL 的类在 .NET Framework 内部。 简短故事，你无法将用户数据存储在无 cookie forms 身份验证票证中。

### <a name="accessing-the-userdata-information"></a>访问 UserData 信息

此时，每个用户的公司名称和标题都存储在登录时的 forms 身份验证票证的 UserData 属性中。 可从任何页面上的身份验证票证访问此信息，而无需访问用户存储。 为了说明如何从 UserData 属性检索此信息，我们更新了 default.aspx，使其欢迎消息不仅包括用户的名称，而且还包括他们使用的公司及其职务。

目前，default.aspx 包含一个 AuthenticatedMessagePanel 面板，其中包含名为 WelcomeBackMessage 的标签控件。 此面板仅向经过身份验证的用户显示。 \_Load 事件处理程序中更新 .aspx 页面中的代码，使其类似于以下内容：

[!code-csharp[Main](forms-authentication-configuration-and-advanced-topics-cs/samples/sample8.cs)]

如果 IsAuthenticated 为 true，则 WelcomeBackMessage 的 Text 属性首先设置为 "欢迎回来，*用户名*"。 然后，将 User. Identity 属性强制转换为 FormsIdentity 对象，以便我们可以访问基础 FormsAuthenticationTicket。 有了 FormsAuthenticationTicket 后，我们会将 UserData 属性反序列化为公司名称和标题。 这是通过将字符串拆分为管道字符来完成的。 然后，将在 "WelcomeBackMessage" 标签中显示公司名称和标题。

图5显示了此显示在操作中的屏幕截图。 以 Scott 身份登录时，会显示一个包含 Scott 公司和职务的欢迎消息。

[显示当前登录的用户的公司和标题 ![](forms-authentication-configuration-and-advanced-topics-cs/_static/image14.png)](forms-authentication-configuration-and-advanced-topics-cs/_static/image13.png)

**图 05**：显示当前登录的用户的公司和标题（[单击查看完全大小的图像](forms-authentication-configuration-and-advanced-topics-cs/_static/image15.png)）

> [!NOTE]
> 身份验证票证的 UserData 属性用作用户存储的缓存。 与任何缓存一样，在修改基础数据时，需要对其进行更新。 例如，如果有一个网页可供用户更新其配置文件，则必须刷新在 UserData 属性中缓存的字段，以反映用户所做的更改。

## <a name="step-5-using-a-custom-principal"></a>步骤5：使用自定义主体

对于每个传入请求，FormsAuthenticationModule 将尝试对用户进行身份验证。 如果存在未过期的身份验证票证，则 FormsAuthenticationModule 会将 HttpContext 属性分配给新的 GenericPrincipal 对象。 此 GenericPrincipal 对象有一个 FormsIdentity 类型的标识，其中包括对 forms 身份验证票证的引用。 GenericPrincipal 类包含实现 IPrincipal 的类所需的最小功能-它只包含一个 Identity 属性和一个 IsInRole 方法。

主体对象有两个责任：指示用户所属的角色并提供标识信息。 这可以分别通过 IPrincipal 接口的*IsInRole （"* 标识"）方法和 "标识" 属性来实现。 GenericPrincipal 类允许通过其构造函数指定角色名称的字符串数组;它的 IsInRole *（"* 方法"）方法只检查字符串*数组中是否存在传入*的 "有条件"。 当 FormsAuthenticationModule 创建 GenericPrincipal 时，它将在一个空字符串数组中传递到 GenericPrincipal 的构造函数。 因此，对 IsInRole 的任何调用都将始终返回 false。

GenericPrincipal 类满足大多数基于窗体的身份验证方案的需求，其中不使用角色。 对于默认角色处理不足或需要将自定义 IIdentity 对象与用户关联的情况，可以在身份验证工作流过程中创建自定义 IPrincipal 对象，并将其分配给 HttpContext。

> [!NOTE]
> 在将来的教程中，我们将在 ASP 时看到。网络角色框架已启用。它创建[RolePrincipal](https://msdn.microsoft.com/library/system.web.security.roleprincipal.aspx)类型的自定义主体对象，并覆盖 forms 身份验证创建的 GenericPrincipal 对象。 这样做是为了自定义主体的 IsInRole 方法，以便与角色框架的 API 进行交互。

由于我们尚未关心角色，因此，在此结合创建自定义主体的唯一原因是将自定义 IIdentity 对象关联到主体。 在步骤4中，我们探讨了如何在身份验证票证的 UserData 属性中存储其他用户信息，尤其是用户的公司名称和标题。 但是，只需通过身份验证票证即可访问 UserData 信息，只需将其作为序列化字符串，这意味着，无论何时，只要要查看存储在票证中的用户信息，都需要分析 UserData 属性。

我们可以通过创建实现 IIdentity 的类，并包括 "公司名称" 和 "标题" 属性来改善开发人员体验。 这样一来，开发人员就可以直接通过 "公司名称" 和 "标题" 属性访问当前登录的用户的公司名称和标题，而无需知道如何分析 UserData 属性。

### <a name="creating-the-custom-identity-and-principal-classes"></a>创建自定义标识和主体类

对于本教程，让我们在应用程序\_代码文件夹中创建自定义主体和标识对象。 首先将应用\_代码文件夹添加到项目-右键单击解决方案资源管理器中的项目名称，选择 "添加 ASP.NET" 文件夹选项，然后选择 "应用\_代码"。 应用\_代码文件夹是一个特殊的 ASP.NET 文件夹，保存特定于网站的类文件。

> [!NOTE]
> 仅应在通过网站项目模型管理项目时使用应用\_代码文件夹。 如果你使用的是[Web 应用程序项目模型](https://msdn.microsoft.com/asp.net/Aa336618.aspx)，请创建一个标准文件夹并将类添加到该文件夹中。 例如，你可以添加一个名为类的新文件夹，并将你的代码放在此处。

接下来，将两个新的类文件添加到应用\_代码文件夹，一个名为 CustomIdentity.cs，另一个命名为 CustomPrincipal.cs。

[![将 CustomIdentity 和 CustomPrincipal 类添加到项目](forms-authentication-configuration-and-advanced-topics-cs/_static/image17.png)](forms-authentication-configuration-and-advanced-topics-cs/_static/image16.png)

**图 06**：向项目中添加 CustomIdentity 和 CustomPrincipal 类（[单击以查看完全大小的图像](forms-authentication-configuration-and-advanced-topics-cs/_static/image18.png)）

CustomIdentity 类负责实现 IIdentity 接口，该接口定义 AuthenticationType、IsAuthenticated 和 Name 属性。 除了这些所需的属性之外，我们还对公开底层 forms 身份验证票证以及用户公司名称和标题的属性感兴趣。 在 CustomIdentity 类中输入以下代码。

[!code-csharp[Main](forms-authentication-configuration-and-advanced-topics-cs/samples/sample9.cs)]

请注意，类包含 FormsAuthenticationTicket 成员变量（\_ticket），并且必须通过构造函数提供此票证信息。 此票证数据用于返回标识的名称;将分析其 UserData 属性以返回 "公司名称" 和 "标题" 属性的值。

接下来，创建 CustomPrincipal 类。 由于我们不关心此接合处的角色，CustomPrincipal 类的构造函数只接受 CustomIdentity 对象;它的 IsInRole 方法始终返回 false。

[!code-csharp[Main](forms-authentication-configuration-and-advanced-topics-cs/samples/sample10.cs)]

### <a name="assigning-a-customprincipal-object-to-the-incoming-requests-security-context"></a>将 CustomPrincipal 对象分配给传入请求的安全上下文

现在，我们有一个类，它将默认的 IIdentity 规范扩展为包含 "公司名称" 和 "标题" 属性以及使用自定义标识的自定义主体类。 我们已准备单步执行 ASP.NET 管道，并将自定义主体对象分配给传入请求的安全上下文。

ASP.NET 管道接收传入请求并通过多个步骤进行处理。 在每个步骤中，将引发特定事件，使开发人员能够在 ASP.NET 管道中点击并在其生命周期中的特定时间点修改请求。 例如，FormsAuthenticationModule 会等待 ASP.NET 引发[AuthenticateRequest 事件](https://msdn.microsoft.com/library/system.web.httpapplication.authenticaterequest.aspx)，此时，会检查传入请求的身份验证票证。 如果找到身份验证票证，则会创建一个 GenericPrincipal 对象，并将其分配给 HttpContext. User 属性。

AuthenticateRequest 事件完成后，ASP.NET 管道将引发[PostAuthenticateRequest 事件](https://msdn.microsoft.com/library/system.web.httpapplication.postauthenticaterequest.aspx)，可在其中将 FormsAuthenticationModule 创建的 GenericPrincipal 对象替换为我们的 CustomPrincipal 对象的实例。 图7介绍了此工作流。

[![GenericPrincipal 被 PostAuthenticationRequest 事件中的 CustomPrincipal 替换](forms-authentication-configuration-and-advanced-topics-cs/_static/image20.png)](forms-authentication-configuration-and-advanced-topics-cs/_static/image19.png)

**图 07**： GenericPrincipal 替换为 PostAuthenticationRequest 事件中的 CustomPrincipal （[单击以查看完全大小的图像](forms-authentication-configuration-and-advanced-topics-cs/_static/image21.png)）

为了执行代码以响应 ASP.NET 管道事件，可以在 global.asax 中创建相应的事件处理程序，或者创建我们自己的 HTTP 模块。 在本教程中，我们将在 global.asax 中创建事件处理程序。 首先将 global.asax 添加到你的网站。 在解决方案资源管理器中右键单击项目名称，并添加一个名为 "global.asax" 的全局应用程序类类型的项。

[![向网站添加一个 global.asax 文件](forms-authentication-configuration-and-advanced-topics-cs/_static/image23.png)](forms-authentication-configuration-and-advanced-topics-cs/_static/image22.png)

**图 08**：向网站添加一个 global.asax 文件（[单击以查看完全大小的图像](forms-authentication-configuration-and-advanced-topics-cs/_static/image24.png)）

默认的 global.asax 模板包括多个 ASP.NET 管道事件的事件处理程序，包括启动、结束和[错误事件](https://msdn.microsoft.com/library/system.web.httpapplication.error.aspx)，等等。 可以随意删除这些事件处理程序，因为对于此应用程序，我们不需要它们。 我们感兴趣的事件是 PostAuthenticateRequest。 更新 global.asax 文件，使其标记类似于以下内容：

[!code-aspx[Main](forms-authentication-configuration-and-advanced-topics-cs/samples/sample11.aspx)]

每次 ASP.NET 运行时引发 PostAuthenticateRequest 事件时，将执行应用程序\_OnPostAuthenticateRequest 方法，这会在每个传入页面请求发生一次。 事件处理程序通过检查是否已通过 forms 身份验证对用户进行身份验证和身份验证而开始。 如果是这样，则将创建一个新的 CustomIdentity 对象，并在其构造函数中传递当前请求的身份验证票证。 之后，将创建一个 CustomPrincipal 对象，并在其构造函数中传递刚刚创建的 CustomIdentity 对象。 最后，当前请求的安全上下文将分配给新创建的 CustomPrincipal 对象。

请注意，最后一步是将 CustomPrincipal 对象与请求的安全上下文相关联，将主体分配给两个属性： HttpContext. User 和 Thread.currentprincipal。 这两个赋值是必需的，因为在 ASP.NET 中处理安全上下文的方式。 .NET Framework 将安全上下文与每个正在运行的线程关联;此信息可通过[Thread 对象](https://msdn.microsoft.com/library/system.threading.thread.aspx)的[Thread.currentprincipal 属性](https://msdn.microsoft.com/library/system.threading.thread.currentcontext.aspx)作为 IPrincipal 对象提供。 令人费解的是，ASP.NET 具有其自己的安全上下文信息（HttpContext）。

在某些情况下，在确定安全上下文时会检查 Thread.currentprincipal 属性;在其他情况下，使用 HttpContext。 例如，.NET 中有一些安全功能，这些功能可让开发人员以声明方式陈述哪些用户或角色可以实例化类或调用特定的方法（请参阅[使用 PrincipalPermissionAttributes 将授权规则添加到业务层和数据层](https://weblogs.asp.net/scottgu/archive/2006/10/04/Tip_2F00_Trick_3A00_-Adding-Authorization-Rules-to-Business-and-Data-Layers-using-PrincipalPermissionAttributes.aspx)）。 这些声明性技术在涵盖范围下，通过 Thread.currentprincipal 属性确定安全上下文。

在其他情况下，将使用 HttpContext 属性。 例如，在上一教程中，我们使用此属性来显示当前登录的用户的用户名。 显然，Thread.currentprincipal 和 HttpContext 属性中的安全上下文信息都是匹配的。

ASP.NET 运行时自动为我们同步这些属性值。 但是，此同步发生在 AuthenticateRequest 事件之后，而在 PostAuthenticateRequest 事件*之前*发生。 因此，在 PostAuthenticateRequest 事件中添加自定义主体时，需要确保手动分配 Thread.currentprincipal 或 else Thread.currentprincipal 和 HttpContext。用户将不同步。有关此问题的详细讨论，请参阅[thread.currentprincipal](http://leastprivilege.com/2005/11/23/context-user-vs-thread-currentprincipal/) 。

### <a name="accessing-the-companyname-and-title-properties"></a>访问 "公司名称" 和 "标题" 属性

每当请求到达并被调度到 ASP.NET 引擎时，将激发 global.asax 中的应用程序\_OnPostAuthenticateRequest 事件处理程序。 如果请求已通过 FormsAuthenticationModule 成功进行身份验证，则事件处理程序将根据 forms 身份验证票证创建一个具有 CustomIdentity 对象的新 CustomPrincipal 对象。 利用这一逻辑，访问有关当前已登录用户的公司名称和职务的信息非常简单。

返回到\_Load 事件处理程序的页面。在步骤4中，我们编写了用于检索表单身份验证票证的代码，并分析了 UserData 属性，以便显示用户的公司名称和标题。 现在，使用 CustomPrincipal 和 CustomIdentity 对象，无需分析票证的 UserData 属性中的值。 相反，只需获取对 CustomIdentity 对象的引用并使用其 "公司名称" 和 "标题" 属性：

[!code-csharp[Main](forms-authentication-configuration-and-advanced-topics-cs/samples/sample12.cs)]

## <a name="summary"></a>摘要

在本教程中，我们介绍了如何通过 web.config 自定义 forms 身份验证系统的设置。我们查看了如何处理身份验证票证的过期，以及如何使用加密和验证安全措施来保护票证不被检查和修改。 最后，我们讨论了如何使用身份验证票证的 UserData 属性在票证本身中存储其他用户信息，以及如何使用自定义主体和标识对象以更好的开发人员更好的方式公开这些信息。

本教程介绍如何在 ASP.NET 中检查 forms 身份验证。 下一教程将开始我们的成员身份框架旅程。

很高兴编程！

### <a name="further-reading"></a>其他阅读材料

有关本教程中讨论的主题的详细信息，请参阅以下资源：

- [二级 Forms 身份验证](http://aspnet.4guysfromrolla.com/articles/072005-1.aspx)
- [说明： ASP.NET 2.0 中的 Forms 身份验证](https://msdn.microsoft.com/library/aa480476.aspx)
- [如何：在 ASP.NET 2.0 中保护 Forms 身份验证](https://msdn.microsoft.com/library/ms998310.aspx)
- [Professional ASP.NET 2.0 安全性、成员身份和角色管理](http://www.wrox.com/WileyCDA/WroxTitle/productCd-0764596985.html)（ISBN：978-0-7645-9698-8）
- [保护登录控件](https://msdn.microsoft.com/library/ms178346.aspx)
- [&lt;authentication&gt; 元素](https://msdn.microsoft.com/library/532aee0e.aspx)
- [&lt;身份验证的 &lt;窗体&gt; 元素&gt;](https://msdn.microsoft.com/library/1d3t3c61.aspx)
- [&lt;machineKey&gt; 元素](https://msdn.microsoft.com/library/w8h3skw9.aspx)
- [了解 Forms 身份验证票证和 Cookie](https://support.microsoft.com/kb/910443)

### <a name="video-training-on-topics-contained-in-this-tutorial"></a>本教程中包含的主题的视频培训

- [如何更改 Forms 身份验证属性](../../../videos/authentication/how-to-change-the-forms-authentication-properties.md)
- [如何在 ASP.NET 应用程序中设置和使用不区分 Cookie 的身份验证](../../../videos/authentication/how-to-setup-and-use-cookie-less-authentication-in-an-aspnet-application.md)
- [ASP 窗体登录重定位](../../../videos/authentication/asp-forms-login-relocation.md)
- [窗体登录自定义密钥配置](../../../videos/authentication/forms-login-custom-key-configuration.md)
- [向身份验证方法添加自定义数据](../../../videos/authentication/add-custom-data-to-the-authentication-method.md)
- [使用自定义主体对象](../../../videos/authentication/use-custom-principal-objects.md)

### <a name="about-the-author"></a>关于作者

Scott Mitchell，创始人的多个 ASP/ASP 和4GuysFromRolla.com 的作者已使用 Microsoft Web 技术，1998。 Scott 的工作方式是独立的顾问、培训师和撰稿人。 他的最新书籍是， *[在24小时内，sam ASP.NET 2.0](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)* 。 可以通过[http://ScottOnWriting.NET](http://scottonwriting.net/) [mitchell@4guysfromrolla.com](mailto:mitchell@4guysfromrolla.com)或通过他的博客访问 Scott。

### <a name="special-thanks-to"></a>特别感谢

此教程系列由许多有用的审阅者查看。 本教程的主管审查人员是 Alicja Maziarz。 想要查看我即将发布的 MSDN 文章？ 如果是这样，请在[mitchell@4GuysFromRolla.com](mailto:mitchell@4guysfromrolla.com)放置一行。

> [!div class="step-by-step"]
> [上一页](an-overview-of-forms-authentication-cs.md)
> [下一页](security-basics-and-asp-net-support-vb.md)
