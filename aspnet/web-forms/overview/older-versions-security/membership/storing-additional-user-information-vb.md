---
uid: web-forms/overview/older-versions-security/membership/storing-additional-user-information-vb
title: 存储其他用户信息（VB） |Microsoft Docs
author: rick-anderson
description: 在本教程中，我们将通过构建一个非常基本的留言簿应用程序来回答这个问题。 在此过程中，我们将查看 modeli 的不同选项 。
ms.author: riande
ms.date: 01/18/2008
ms.assetid: ee4b924e-8002-4dc3-819f-695fca1ff867
msc.legacyurl: /web-forms/overview/older-versions-security/membership/storing-additional-user-information-vb
msc.type: authoredcontent
ms.openlocfilehash: cb352de6f7c2d117b41532112a87956c8dde62f8
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74639316"
---
# <a name="storing-additional-user-information-vb"></a>存储其他用户信息 (VB)

作者： [Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载代码](https://download.microsoft.com/download/3/f/5/3f5a8605-c526-4b34-b3fd-a34167117633/ASPNET_Security_Tutorial_08_VB.zip)或[下载 PDF](https://download.microsoft.com/download/3/f/5/3f5a8605-c526-4b34-b3fd-a34167117633/aspnet_tutorial08_ExtraUserInfo_vb.pdf)

> 在本教程中，我们将通过构建一个非常基本的留言簿应用程序来回答这个问题。 在此过程中，我们将查看用于在数据库中对用户信息建模的不同选项，然后查看如何将此数据与成员资格框架创建的用户帐户相关联。

## <a name="introduction"></a>简介

ASP.NET.NET 的成员身份框架为管理用户提供了一个灵活的界面。 成员资格 API 包括用于验证凭据、检索当前已登录用户的信息、创建新的用户帐户以及删除用户帐户的方法。 成员身份框架中的每个用户帐户只包含验证凭据和执行与用户帐户相关的重要任务所需的属性。 这是由[`MembershipUser` 类](https://msdn.microsoft.com/library/system.web.security.membershipuser.aspx)的方法和属性出现的，该类对成员身份框架中的用户帐户建模。 此类具有一些属性，如[`UserName`](https://msdn.microsoft.com/library/system.web.security.membershipuser.username.aspx)、 [`Email`](https://msdn.microsoft.com/library/system.web.security.membershipuser.email.aspx)和[`IsLockedOut`](https://msdn.microsoft.com/library/system.web.security.membershipuser.islockedout.aspx)，以及[`GetPassword`](https://msdn.microsoft.com/library/system.web.security.membershipuser.getpassword.aspx)和[`UnlockUser`](https://msdn.microsoft.com/library/system.web.security.membershipuser.unlockuser.aspx)等方法。

通常，应用程序需要存储成员身份框架中未包含的其他用户信息。 例如，在线零售商可能需要让每个用户存储其发货和帐单地址、支付信息、交货首选项和联系电话号码。 而且，系统中的每个订单都与特定的用户帐户相关联。

`MembershipUser` 类不包括 `PhoneNumber` 或 `DeliveryPreferences` 或 `PastOrders`之类的属性。 那么，我们如何跟踪应用程序所需的用户信息并将其与成员身份框架集成？ 在本教程中，我们将通过构建一个非常基本的留言簿应用程序来回答这个问题。 在此过程中，我们将查看用于在数据库中对用户信息建模的不同选项，然后查看如何将此数据与成员资格框架创建的用户帐户相关联。 让我们进入正题！

## <a name="step-1-creating-the-guestbook-applications-data-model"></a>步骤1：创建留言簿应用程序的数据模型

有多种方法可用于在数据库中捕获用户信息，并将其与成员身份框架创建的用户帐户相关联。 为了说明这些方法，我们需要增加教程 web 应用程序，使其能够捕获某些用户相关数据。 （目前，应用程序的数据模型仅包含 `SqlMembershipProvider`所需的应用程序服务表。）

让我们创建一个非常简单的留言簿应用程序，在该应用程序中，经过身份验证的用户可以留下评论。 除了存储留言簿评论外，让每位用户都可以存储他的 "城市"、"主页" 和 "签名"。 如果提供了，则用户的 "住宅"、"主页" 和 "签名" 将显示在其在留言簿中留下的每个邮件上。

### <a name="adding-theguestbookcommentstable"></a>添加`GuestbookComments`表

为了捕获留言簿评论，我们需要创建一个名为 `GuestbookComments` 的数据库表，该表中的列如 `CommentId`、`Subject`、`Body`和 `CommentDate`。 还需要让 `GuestbookComments` 表中的每条记录都引用留下注释的用户。

若要将此表添加到数据库，请在 Visual Studio 中转到数据库资源管理器，并向下钻取到 `SecurityTutorials` 数据库。 右键单击 "表" 文件夹，然后选择 "添加新表"。 这将打开一个接口，该接口允许我们定义新表的列。

[![向 SecurityTutorials 数据库添加新表](storing-additional-user-information-vb/_static/image2.png)](storing-additional-user-information-vb/_static/image1.png)

**图 1**：将新表添加到 `SecurityTutorials` 数据库（[单击以查看完全大小的图像](storing-additional-user-information-vb/_static/image3.png)）

接下来，定义 `GuestbookComments`的列。 首先添加一个名为 `uniqueidentifier`的名为 `CommentId` 的列。 此列将唯一标识留言簿中的每个注释，因此不允许 `NULL` 并将其标记为表的主键。 我们 `INSERT` `uniqueidentifier` 可以通过将列的默认值设置为 `NEWID()`，而不是为每个 `INSERT`上的 "`CommentId`" 字段提供值。 添加此第一个字段，将其标记为主键并设置其默认值后，屏幕应类似于图2中所示的屏幕截图。

[![添加名为 CommentId 的主列](storing-additional-user-information-vb/_static/image5.png)](storing-additional-user-information-vb/_static/image4.png)

**图 2**：添加名为 `CommentId` 的主列（[单击以查看完全大小的图像](storing-additional-user-information-vb/_static/image6.png)）

接下来，添加一个名为 `Subject` 类型为 `nvarchar(50)` 的列和一个名为 `nvarchar(MAX)`类型 `Body` 的列，这两列中不允许使用 `NULL`。 然后，添加一个名为 `datetime`的名为 `CommentDate` 的列。 禁止 `NULL`，并将 `CommentDate` 列的默认值设置为 "`getdate()`"。

剩下的就是添加一个将用户帐户与每个留言簿注释相关联的列。 一种选择是添加 `nvarchar(256)`类型为 `UserName` 的列。 当使用 `SqlMembershipProvider`以外的成员资格提供程序时，这是一个合适的选择。 但使用 `SqlMembershipProvider`时，正如本系列教程中所述，`aspnet_Users` 表中的 `UserName` 列不一定是唯一的。 `aspnet_Users` 表的主键 `UserId`，其类型为 `uniqueidentifier`。 因此，`GuestbookComments` 表需要一个类型为 `UserId` 的列 `uniqueidentifier` （不允许 `NULL` 值）。 继续并添加此列。

> [!NOTE]
> 正如我们在 SQL Server 教程中[*创建成员身份架构*](creating-the-membership-schema-in-sql-server-vb.md)中讨论的那样，成员身份框架旨在使具有不同用户帐户的多个 web 应用程序共享相同的用户存储区。 它通过将用户帐户分区到不同的应用程序中来实现此功能。 虽然在应用程序中保证每个用户名都是唯一的，但使用相同的用户存储可以在不同的应用程序中使用相同的用户名。 `UserName` 和 `ApplicationId` 字段的 `aspnet_Users` 表中有一个复合的 `UNIQUE` 约束，但不只是 `UserName` 字段上有一个。 因此，aspnet\_Users "表有可能有两个（或更多） `UserName` 值相同的记录。 但 `aspnet_Users` 表的 `UserId` 字段有 `UNIQUE` 约束（因为它是主键）。 `UNIQUE` 约束很重要，因为如果没有此约束，则无法在 `GuestbookComments` 和 `aspnet_Users` 表之间建立外键约束。

添加 `UserId` 列后，通过单击工具栏中的 "保存" 图标来保存表。 将新表命名 `GuestbookComments`。

我们有一个在 `GuestbookComments` 表中出席的最后一个问题：我们需要在 `GuestbookComments.UserId` 列与 `aspnet_Users.UserId` 列之间创建一个[外键约束](https://msdn.microsoft.com/library/ms175464.aspx)。 若要实现此目的，请单击工具栏中的 "关系" 图标以启动 "外键关系" 对话框。 （或者，您可以通过转到 "表设计器" 菜单并选择 "关系" 来启动此对话框。）

单击 "外键关系" 对话框左下角的 "添加" 按钮。 这将添加新的 foreign key 约束，但我们仍需要定义参与关系的表。

[![使用 "外键关系" 对话框管理表的外键约束](storing-additional-user-information-vb/_static/image8.png)](storing-additional-user-information-vb/_static/image7.png)

**图 3**：使用 "外键关系" 对话框管理表的外键约束（[单击以查看完全大小的图像](storing-additional-user-information-vb/_static/image9.png)）

接下来，单击右侧 "表和列规范" 行中的省略号图标。 这将启动 "表和列" 对话框，通过该对话框可以从 `GuestbookComments` 表中指定主键表和列和外键列。 特别是，选择 `aspnet_Users`，并将其 `UserId` 为主键表和列，并将 `GuestbookComments` 表中的 `UserId` 用作外键列（参见图4）。 定义主键和外键表和列后，单击 "确定" 以返回到 "外键关系" 对话框。

[![在 "aspnet_Users" 表和 "GuesbookComments" 表之间建立外键约束](storing-additional-user-information-vb/_static/image11.png)](storing-additional-user-information-vb/_static/image10.png)

**图 4**：建立 `aspnet_Users` 和 `GuesbookComments` 表之间的外键约束（[单击以查看完全大小的图像](storing-additional-user-information-vb/_static/image12.png)）

此时，已建立外键约束。 此约束的存在确保两个表之间的[关系完整性](http://en.wikipedia.org/wiki/Referential_integrity)，方法是确保不会有引用不存在的用户帐户的留言簿条目。 默认情况下，如果存在相应的子记录，则 foreign key 约束将禁止删除父记录。 也就是说，如果用户发出一个或多个留言簿注释，然后我们尝试删除该用户帐户，则删除将失败，除非首先删除他的留言簿评论。

外键约束可以配置为在删除父记录时自动删除关联的子记录。 换句话说，我们可以设置此 foreign key 约束，以便在删除用户的用户帐户时自动删除用户的留言簿条目。 若要实现此目的，请展开 "INSERT 和 UPDATE 规范" 部分，并将 "删除规则" 属性设置为 Cascade。

[![配置用于级联删除的外键约束](storing-additional-user-information-vb/_static/image14.png)](storing-additional-user-information-vb/_static/image13.png)

**图 5**：将外键约束配置为级联删除（[单击以查看完全大小的映像](storing-additional-user-information-vb/_static/image15.png)）

若要保存外键约束，请单击 "关闭" 按钮退出外键关系。 然后单击工具栏中的 "保存" 图标以保存表和此关系。

### <a name="storing-the-users-home-town-homepage-and-signature"></a>存储用户的家庭城镇、主页和签名

`GuestbookComments` 表说明了如何存储与用户帐户共享一对多关系的信息。 由于每个用户帐户可能具有任意数量的关联注释，因此可以通过创建一个表来存储注释集，使其包含一组注释，其中包含一个链接回每个注释给特定用户的列。 使用 `SqlMembershipProvider`时，最好是通过创建一个类型为 `UserId` 的列 `uniqueidentifier`，并在此列和 `aspnet_Users.UserId`之间创建一个外键约束，来建立此链接。

现在，我们需要将三列与每个用户帐户相关联，以存储用户的 "住宅"、"主页" 和 "签名"，这些列将显示在他的留言簿评论中。 可以通过多种不同的方法来实现此目的：

- 向<strong>`aspnet_Users`</strong><strong>或</strong><strong>`aspnet_Membership`</strong><strong>表</strong>中<strong>添加新列</strong>。 我不建议使用此方法，因为它会修改 `SqlMembershipProvider`使用的架构。 这一决定可能会 haunt 您的路上。 例如，如果 ASP.NET 的未来版本使用不同的 `SqlMembershipProvider` 架构。 Microsoft 可能会包含一种工具，用于将 ASP.NET 2.0 `SqlMembershipProvider` 的数据迁移到新的架构，但如果修改了 ASP.NET 2.0 `SqlMembershipProvider` 架构，则可能无法进行此类转换。

- **使用 ASP。NET 的配置文件框架，定义家庭城镇、主页和签名的配置文件属性。** ASP.NET 包含一个配置文件框架，用于存储其他特定于用户的数据。 与成员身份框架一样，配置文件框架是在提供程序模型的顶层生成的。 该 .NET Framework 附带了一个将配置文件数据存储在 SQL Server 数据库中的 `SqlProfileProvider`。 事实上，数据库已具有 `SqlProfileProvider` （`aspnet_Profile`）所用的表，因为在[*SQL Server 教程中创建成员身份架构*](creating-the-membership-schema-in-sql-server-vb.md)时添加了应用程序服务。   
  配置文件框架的主要优点是它允许开发人员定义 `Web.config` 中的配置文件属性–无需编写任何代码来序列化与基础数据存储区中的配置文件数据。 简而言之，定义一组配置文件属性并在代码中使用它们非常简单。 但是，当涉及到版本控制时，配置文件系统会给您带来很大的需要，因此，如果您有一个应用程序，该应用程序在以后要添加新的用户特定属性，或要删除或修改现有的特定属性，则配置文件框架可能不是 最佳选项。 此外，`SqlProfileProvider` 将配置文件属性以高度非规范化的方式存储，使其成为无法直接对配置文件数据运行查询（例如，有多少用户拥有纽约的用户）。   
  有关配置文件框架的详细信息，请参阅本教程末尾的 "进一步阅读" 一节。

- <strong>将这三列添加到数据库中的新表，并在此表和`aspnet_Users`之间建立一对一关系</strong> <strong>。</strong> 此方法所涉及的工作比分析框架要多得多，但在数据库中建模附加用户属性的方式提供了最大的灵活性。 这是我们将在本教程中使用的选项。

我们将创建一个名为 `UserProfiles` 的新表，以保存每个用户的 home 镇、主页和签名。 右键单击 "数据库资源管理器" 窗口中的 "表" 文件夹，然后选择创建新表。 将第一列命名 `UserId` 并将其类型设置为 `uniqueidentifier`。 禁止 `NULL` 值并将列标记为主键。 接下来，添加名为的列：类型为 `nvarchar(50)`的 `HomeTown`;`nvarchar(100)`类型的 `HomepageUrl`;`nvarchar(500)`类型的和签名。 这三列中的每一列都可以接受 `NULL` 值。

[![创建 UserProfiles 表](storing-additional-user-information-vb/_static/image17.png)](storing-additional-user-information-vb/_static/image16.png)

**图 6**：创建 `UserProfiles` 表（[单击以查看完全大小的图像](storing-additional-user-information-vb/_static/image18.png)）

保存该表并将其命名为 `UserProfiles`。 最后，在 `UserProfiles` 表的 `UserId` 字段与 `aspnet_Users.UserId` 字段之间建立外键约束。 与 `GuestbookComments` 和 `aspnet_Users` 表之间的外键约束一样，请将此约束删除。 由于 `UserProfiles` 中的 `UserId` 字段是主键，这可确保每个用户帐户的 `UserProfiles` 表中不会有多条记录。 这种关系称为一对一关系。

现在，我们已经创建了数据模型，接下来可以使用它了。 在步骤2和步骤3中，我们将看看当前登录的用户可以如何查看和编辑其家庭城镇、主页和签名信息。 在步骤4中，我们将为经过身份验证的用户创建用于向留言簿提交新评论并查看现有评论的界面。

## <a name="step-2-displaying-the-users-home-town-homepage-and-signature"></a>步骤2：显示用户的 "住宅"、"主页" 和 "签名"

有多种方式允许当前登录的用户查看和编辑其 home、主页和签名信息。 我们可以使用文本框和标签控件手动创建用户界面，也可以使用其中一个数据 Web 控件（如 DetailsView 控件）。 若要执行数据库 `SELECT` 和 `UPDATE` 语句，我们可以在页面的代码隐藏类中编写 ADO.NET 代码，或者在 SqlDataSource 中使用声明性方法。 理想情况下，我们的应用程序将包含分层体系结构，可以通过编程方式从页面的代码隐藏类调用，或通过 ObjectDataSource 控件以声明方式调用。

由于本教程系列重点介绍 forms 身份验证、授权、用户帐户和角色，因此将不会全面讨论这些不同的数据访问选项，或者为什么使用分层体系结构直接执行 SQL 语句从 "ASP.NET" 页。 我将逐步介绍如何使用 DetailsView 和 SqlDataSource –最快捷、最简单的选项，但讨论的概念肯定适用于替代 Web 控件和数据访问逻辑。 有关使用 ASP.NET 中的数据的详细信息，请参阅使用 *[ASP.NET 2.0 教程系列中的数据](../../data-access/index.md)* 。

打开 `Membership` 文件夹中的 "`AdditionalUserInfo.aspx`" 页，向页面添加 "DetailsView" 控件，并将其 ID 属性设置为 "`UserProfile`" 并清除其 `Width` 和 `Height` 属性。 展开 DetailsView 的智能标记，然后选择将其绑定到新的数据源控件。 这将启动 "数据源配置向导" （参见图7）。 第一个步骤要求您指定数据源类型。 由于我们要直接连接到 `SecurityTutorials` 数据库，因此请选择 "数据库" 图标，将 "`ID`" 指定为 "`UserProfileDataSource`"。

[![添加一个名为 UserProfileDataSource 的新 SqlDataSource 控件](storing-additional-user-information-vb/_static/image20.png)](storing-additional-user-information-vb/_static/image19.png)

**图 7**：添加名为 `UserProfileDataSource` 的新 SqlDataSource 控件（[单击以查看完全大小的图像](storing-additional-user-information-vb/_static/image21.png)）

下一屏幕将提示数据库使用。 已在 `Web.config` 中为 `SecurityTutorials` 数据库定义了一个连接字符串。 此连接字符串名称– `SecurityTutorialsConnectionString` –应在下拉列表中。 选择此选项，然后单击 "下一步"。

[![从下拉列表中选择 "SecurityTutorialsConnectionString"](storing-additional-user-information-vb/_static/image23.png)](storing-additional-user-information-vb/_static/image22.png)

**图 8**：从下拉列表中选择 "`SecurityTutorialsConnectionString`" （[单击查看完全大小的图像](storing-additional-user-information-vb/_static/image24.png)）

后续屏幕会要求我们指定要查询的表和列。 从下拉列表中选择 `UserProfiles` 表，然后检查所有列。

[![返回 UserProfiles 表中的所有列](storing-additional-user-information-vb/_static/image26.png)](storing-additional-user-information-vb/_static/image25.png)

**图 9**：取回 `UserProfiles` 表中的所有列（[单击以查看完全大小的图像](storing-additional-user-information-vb/_static/image27.png)）

图9中的当前查询将返回 `UserProfiles`中的*所有*记录，但我们只对当前登录的用户记录感兴趣。 若要添加 `WHERE` 子句，请单击 "`WHERE`" 按钮以显示 "添加 `WHERE` 子句" 对话框（请参阅图10）。 您可以在此处选择要筛选的列、运算符和筛选器参数的源。 选择 "`UserId`" 作为列，选择 "=" 作为运算符。

遗憾的是，没有内置参数源来返回当前登录用户的 `UserId` 值。 我们需要以编程方式获取此值。 因此，将 "源" 下拉列表设置为 "无"，单击 "添加" 按钮添加参数，然后单击 "确定"。

[![在 UserId 列上添加筛选器参数](storing-additional-user-information-vb/_static/image29.png)](storing-additional-user-information-vb/_static/image28.png)

**图 10**：在 `UserId` 列上添加筛选器参数（[单击以查看完全大小的图像](storing-additional-user-information-vb/_static/image30.png)）

单击 "确定" 后，将返回到图9中所示的屏幕。 但这一次，屏幕底部的 SQL 查询应包含一个 `WHERE` 子句。 单击 "下一步" 转到 "测试查询" 屏幕。 可在此处运行查询并查看结果。 单击“完成”按钮以完成向导。

完成数据源配置向导后，Visual Studio 将基于在向导中指定的设置创建 SqlDataSource 控件。 此外，它还会针对 SqlDataSource 的 `SelectCommand`返回的每个列，手动将 BoundFields 添加到 DetailsView。 不需要在 DetailsView 中显示 "`UserId`" 字段，因为用户无需知道此值。 您可以直接从 DetailsView 控件的声明性标记中删除此字段，或单击其智能标记中的 "编辑字段" 链接。

此时，页面的声明性标记应如下所示：

[!code-aspx[Main](storing-additional-user-information-vb/samples/sample1.aspx)]

在选择数据之前，我们需要以编程方式将 SqlDataSource 控件的 `UserId` 参数设置为当前已登录用户的 `UserId`。 为此，可以创建 SqlDataSource 的 `Selecting` 事件的事件处理程序，并在其中添加以下代码：

[!code-vb[Main](storing-additional-user-information-vb/samples/sample2.vb)]

上面的代码首先通过调用 `Membership` 类的 `GetUser` 方法来获取对当前已登录用户的引用。 这会返回 `MembershipUser` 对象，该对象的 `ProviderUserKey` 属性包含 `UserId`。 然后，将 `UserId` 值分配给 SqlDataSource 的 `@UserId` 参数。

> [!NOTE]
> `Membership.GetUser()` 方法返回有关当前已登录用户的信息。 如果匿名用户正在访问该页面，它将返回值 `Nothing`。 在这种情况下，当尝试读取 `ProviderUserKey` 属性时，这将导致 `NullReferenceException` 以下代码行。 当然，我们不必担心在 `AdditionalUserInfo.aspx` 页中不返回任何内容 `Membership.GetUser()`，因为我们在上一教程中配置了 URL 授权，以便只有经过身份验证的用户才能访问此文件夹中的 ASP.NET 资源。 如果需要在允许匿名访问的页面中访问有关当前已登录用户的信息，请确保从 `GetUser()` 方法返回 `MembershipUser` 对象不是任何内容，然后再引用其属性。

如果通过浏览器访问 `AdditionalUserInfo.aspx` 页面，您将看到一个空白页面，因为我们尚未向 `UserProfiles` 表中添加任何行。 在步骤6中，我们将介绍如何自定义 CreateUserWizard 控件，以便在创建新的用户帐户时自动将新行添加到 `UserProfiles` 表。 但现在，我们需要手动在表中创建一条记录。

在 Visual Studio 中导航到数据库资源管理器，然后展开 "表" 文件夹。 右键单击 `aspnet_Users` 表，然后选择 "显示表数据" 以查看表中的记录;对 `UserProfiles` 表执行相同的操作。 图11在垂直平铺时显示这些结果。 在数据库中，当前有 `aspnet_Users` Bruce、Fred 和 Tito 的记录，但 `UserProfiles` 表中没有记录。

[![显示 aspnet_Users 表和 UserProfiles 表的内容](storing-additional-user-information-vb/_static/image32.png)](storing-additional-user-information-vb/_static/image31.png)

**图 11**：显示了 `aspnet_Users` 和 `UserProfiles` 表的内容（[单击查看完全大小的图像](storing-additional-user-information-vb/_static/image33.png)）

通过手动键入 `HomeTown`、`HomepageUrl`和 `Signature` 字段的值，将新记录添加到 `UserProfiles` 表。 若要在新的 `UserProfiles` 记录中获得有效 `UserId` 值，最简单的方法是从 `aspnet_Users` 表的特定用户帐户中选择 `UserId` 字段，并将其复制并粘贴到 `UserId` 中的 `UserProfiles`字段。 图12显示了为 Bruce 添加了新记录后的 `UserProfiles` 表。

[![已将记录添加到 Bruce 的 UserProfiles](storing-additional-user-information-vb/_static/image35.png)](storing-additional-user-information-vb/_static/image34.png)

**图 12**：已将记录添加到 Bruce 的 `UserProfiles` （[单击查看完全大小的图像](storing-additional-user-information-vb/_static/image36.png)）

返回到作为 Bruce 登录的 `AdditionalUserInfo.aspx page`。 如图13所示，将显示 Bruce 的设置。

[![当前访问的用户显示其设置](storing-additional-user-information-vb/_static/image38.png)](storing-additional-user-information-vb/_static/image37.png)

**图 13**：当前正在访问的用户显示其设置（[单击查看完全大小的图像](storing-additional-user-information-vb/_static/image39.png)）

> [!NOTE]
> 继续在 `UserProfiles` 表中为每个成员身份用户手动添加记录。 在步骤6中，我们将介绍如何自定义 CreateUserWizard 控件，以便在创建新的用户帐户时自动将新行添加到 `UserProfiles` 表。

## <a name="step-3-allowing-the-user-to-edit-his-home-town-homepage-and-signature"></a>步骤3：允许用户编辑其家庭城镇、主页和签名

此时，当前登录的用户可以查看其 "住宅"、"主页" 和 "签名" 设置，但他们无法修改它们。 让我们更新 DetailsView 控件以便可以编辑数据。

我们需要做的第一件事是为 SqlDataSource 添加 `UpdateCommand`，并指定要执行的 `UPDATE` 语句及其相应的参数。 选择 "SqlDataSource"，属性窗口然后单击 "UpdateQuery" 属性旁边的省略号，打开 "命令和参数编辑器" 对话框。 在文本框中输入以下 `UPDATE` 语句：

[!code-sql[Main](storing-additional-user-information-vb/samples/sample3.sql)]

接下来，单击 "刷新参数" 按钮，该按钮将在 SqlDataSource 控件的 `UpdateParameters` 集合中为 `UPDATE` 语句中的每个参数创建一个参数。 保留设置为 "无" 的所有参数的源，然后单击 "确定" 按钮完成对话框。

[![指定 SqlDataSource 的 UpdateCommand 和 UpdateParameters](storing-additional-user-information-vb/_static/image41.png)](storing-additional-user-information-vb/_static/image40.png)

**图 14**：指定 SqlDataSource 的 `UpdateCommand` 和 `UpdateParameters` （[单击以查看完全大小的图像](storing-additional-user-information-vb/_static/image42.png)）

由于我们对 SqlDataSource 控件进行了添加，DetailsView 控件现在可以支持编辑。 在 DetailsView 的智能标记中，选中 "启用编辑" 复选框。 这会将 CommandField 添加到控件的 `Fields` 集合，并将其 `ShowEditButton` 属性设置为 True。 当 DetailsView 显示为只读模式，并在编辑模式下显示 "更新" 和 "取消" 按钮时，此按钮将呈现 "编辑" 按钮。 但不要求用户单击 "编辑"，而是可以通过将 DetailsView 控件的[`DefaultMode` 属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.detailsview.defaultmode.aspx)设置为 `Edit`，将 detailsview 渲染为 "始终可编辑" 状态。

进行这些更改后，DetailsView 控件的声明性标记应如下所示：

[!code-aspx[Main](storing-additional-user-information-vb/samples/sample4.aspx)]

请注意，CommandField 和 `DefaultMode` 属性的添加。

继续在浏览器中测试此页。 当使用 `UserProfiles`中的相应记录访问用户时，用户的设置将显示在可编辑的界面中。

[![DetailsView 呈现可编辑接口](storing-additional-user-information-vb/_static/image44.png)](storing-additional-user-information-vb/_static/image43.png)

**图 15**： DetailsView 呈现一个可编辑界面（[单击以查看完全尺寸的图像](storing-additional-user-information-vb/_static/image45.png)）

尝试更改这些值，然后单击 "更新" 按钮。 好像没有发生任何变化。 存在回发，并将值保存到数据库中，但不存在保存的视觉反馈。

若要解决此情况，请返回到 Visual Studio，并在 DetailsView 上方添加标签控件。 将其 `ID` 设置为 `SettingsUpdatedMessage`，其 `Text` 属性设置为 "已更新设置"，并将其 `Visible` 和 `EnableViewState` 属性设置为 `False`。

[!code-aspx[Main](storing-additional-user-information-vb/samples/sample5.aspx)]

每当更新 DetailsView 时，都需要显示 `SettingsUpdatedMessage` 标签。 为此，请为 DetailsView 的 `ItemUpdated` 事件创建事件处理程序，并添加以下代码：

[!code-vb[Main](storing-additional-user-information-vb/samples/sample6.vb)]

通过浏览器返回 `AdditionalUserInfo.aspx` 页面并更新数据。 此时将显示有用的状态消息。

[更新设置时，会显示一条短消息 ![](storing-additional-user-information-vb/_static/image47.png)](storing-additional-user-information-vb/_static/image46.png)

**图 16**：更新设置时显示一条短消息（[单击以查看完全大小的图像](storing-additional-user-information-vb/_static/image48.png)）

> [!NOTE]
> DetailsView 控件的编辑界面会有很大的需要。 它使用标准大小的文本框，但签名字段可能是一个多行文本框。 应使用 RegularExpressionValidator 来确保主页 URL （如果输入）以 "http://" 或 "https://" 开头。 此外，由于 DetailsView 控件的 `DefaultMode` 属性设置为 `Edit`，因此 "取消" 按钮不会执行任何操作。 应将其删除，或者单击时，将用户重定向到其他某个页面（如 `~/Default.aspx`）。 我将这些增强功能留给读者演练。

### <a name="adding-a-link-to-theadditionaluserinfoaspxpage-in-the-master-page"></a>将链接添加到母版页中的 "`AdditionalUserInfo.aspx`" 页

目前，该网站不提供任何指向 `AdditionalUserInfo.aspx` 页面的链接。 只需要在浏览器的地址栏中直接输入页面的 URL 即可。 让我们在 `Site.master` 母版页中添加指向此页面的链接。

回忆一下，母版页包含其 `LoginContent` ContentPlaceHolder 中的登录视图 Web 控件，该控件为经过身份验证和匿名访问者显示不同标记。 更新登录视图控件的 `LoggedInTemplate` 以包含指向 `AdditionalUserInfo.aspx` 页面的链接。 进行这些更改后，登录视图控件的声明性标记应如下所示：

[!code-aspx[Main](storing-additional-user-information-vb/samples/sample7.aspx)]

请注意，向 `LoggedInTemplate`添加 `lnkUpdateSettings` 超链接控件。 设置此链接后，经过身份验证的用户可以快速跳转到页面，以查看和修改其家庭城镇、主页和签名设置。

## <a name="step-4-adding-new-guestbook-comments"></a>步骤4：添加新的留言簿评论

在 "`Guestbook.aspx`" 页中，经过身份验证的用户可以查看留言簿并留下评论。 首先，让我们创建一个添加新的留言簿评论的界面。

在 Visual Studio 中打开 "`Guestbook.aspx`" 页，并构造一个包含两个 TextBox 控件的用户界面，一个用于新注释主题，另一个用于正文。 将第一个 TextBox 控件的 `ID` 属性设置为 `Subject`，其 `Columns` 属性设置为 40;将第二个 `ID` 设置为 `Body`，其 `TextMode` `MultiLine`，并将其 `Width` 和 `Rows` 属性分别设置为 "95%" 和8。 若要完成用户界面，请添加一个名为 `PostCommentButton` 的按钮 Web 控件，并将其 `Text` 属性设置为 "发布评论"。

由于每个留言簿评论都需要主题和正文，因此请为每个文本框添加 RequiredFieldValidator。 将这些控件的 `ValidationGroup` 属性设置为 "EnterComment";同样，将 `PostCommentButton` 控件的 `ValidationGroup` 属性设置为 "EnterComment"。 有关 ASP 的详细信息。NET 的验证控件，请查看[ASP.NET 中的窗体验证](http://www.4guysfromrolla.com/webtech/090200-1.shtml)，[二级 ASP.NET 2.0 中的验证控件](http://aspnet.4guysfromrolla.com/articles/112305-1.aspx)，以及[W3Schools](http://www.w3schools.com/)上的[验证服务器控件教程](http://www.w3schools.com/aspnet/aspnet_refvalidationcontrols.asp)。

在精心编写用户界面后，页面的声明性标记应如下所示：

[!code-aspx[Main](storing-additional-user-information-vb/samples/sample8.aspx)]

完成用户界面后，下一任务是在单击 `PostCommentButton` 时，将新记录插入到 `GuestbookComments` 表中。 可以通过多种方式完成此操作：我们可以在按钮 `Click` 事件处理程序中编写 ADO.NET 代码;我们可以将 SqlDataSource 控件添加到页面，配置其 `InsertCommand`，然后从 `Click` 事件处理程序调用其 `Insert` 方法;或者，我们可以生成负责插入新的留言簿注释并从 `Click` 事件处理程序调用此功能的中间层。 由于我们已在步骤3中介绍了如何使用 SqlDataSource，因此请在此处使用 ADO.NET 代码。

> [!NOTE]
> 用于以编程方式访问 Microsoft SQL Server 数据库中的数据的 ADO.NET 类位于 `System.Data.SqlClient` 命名空间中。 可能需要将该命名空间导入页面的代码隐藏类（即 `Imports System.Data.SqlClient`）中。

为 `PostCommentButton`的 `Click` 事件创建事件处理程序并添加以下代码：

[!code-vb[Main](storing-additional-user-information-vb/samples/sample9.vb)]

`Click` 事件处理程序首先检查用户提供的数据是否有效。 如果不是，则在插入记录之前，事件处理程序将退出。 假设提供的数据有效，将检索当前登录用户的 `UserId` 值并将其存储在 `currentUserId` 本地变量中。 此值是必需的，因为我们必须在向 `GuestbookComments`中插入记录时提供 `UserId` 值。

之后，将从 `Web.config` 检索 `SecurityTutorials` 数据库的连接字符串，并指定 `INSERT` SQL 语句。 然后创建并打开一个 `SqlConnection` 对象。 接下来，将构造一个 `SqlCommand` 对象，并为 `INSERT` 查询中使用的参数指定值。 然后执行 `INSERT` 语句，并关闭连接。 在事件处理程序结束时，将清除 "`Subject`" 和 "`Body`" 文本框的 `Text` 属性，以便不会在回发期间保留用户的值。

继续在浏览器中测试此页。 由于此页面位于 `Membership` 文件夹中，匿名访问者无法访问该文件夹。 因此，你需要先登录（如果尚未这样做）。 在 "`Subject`" 和 "`Body`" 文本框中输入一个值，然后单击 "`PostCommentButton`" 按钮。 这会导致将新记录添加到 `GuestbookComments`。 在回发时，会从文本框中擦除提供的主题和正文。

单击 "`PostCommentButton`" 按钮后，就不会向留言簿添加注释。 我们仍需要更新此页以显示现有的留言簿评论，我们将在步骤5中执行此操作。 完成此项后，只需注释即可显示在注释列表中，提供足够的视觉反馈。 现在，请通过检查 `GuestbookComments` 表的内容来确认是否已保存留言簿注释。

图17显示了两个注释后，`GuestbookComments` 表的内容。

[![你可以在 GuestbookComments 表中查看留言簿注释](storing-additional-user-information-vb/_static/image50.png)](storing-additional-user-information-vb/_static/image49.png)

**图 17**：你可以在 `GuestbookComments` 表中查看留言簿注释（[单击查看完全大小的图像](storing-additional-user-information-vb/_static/image51.png)）

> [!NOTE]
> 如果用户尝试插入包含潜在危险标记的留言簿注释（如 HTML – ASP.NET 将引发 `HttpRequestValidationException`。 若要了解有关此异常的详细信息、引发原因以及如何允许用户提交潜在的危险值，请参阅[请求验证白皮书](../../../../whitepapers/request-validation.md)。

## <a name="step-5-listing-the-existing-guestbook-comments"></a>步骤5：列出现有留言簿评论

除了留下注释外，访问 `Guestbook.aspx` 页面的用户还应能够查看留言簿的现有评论。 若要实现此目的，请将名为 `CommentList` 的 ListView 控件添加到页面底部。

> [!NOTE]
> ListView 控件是 ASP.NET 版本3.5 的新控件。 它旨在以非常可自定义且灵活的布局显示项列表，但仍提供内置的编辑、插入、删除、分页和排序功能，如 GridView。 如果使用的是 ASP.NET 2.0，则需改为使用 DataList 或 Repeater 控件。 有关使用 ListView 的详细信息，请参阅[Scott Guthrie](https://weblogs.asp.net/scottgu/)的博客文章[： listview 控件](https://weblogs.asp.net/scottgu/archive/2007/08/10/the-asp-listview-control-part-1-building-a-product-listing-page-with-clean-css-ui.aspx)和我的文章，[使用 ListView 控件显示数据](http://aspnet.4guysfromrolla.com/articles/122607-1.aspx)。

打开 ListView 的智能标记，然后从 "选择数据源" 下拉列表中将控件绑定到新的数据源。 正如我们在步骤2中看到的那样，这将启动 "数据源配置向导"。 选择数据库图标，将生成的 `CommentsDataSource`SqlDataSource 命名为，然后单击 "确定"。 接下来，从下拉列表中选择 `SecurityTutorialsConnectionString` 连接字符串，然后单击 "下一步"。

在步骤2的这一步中，我们通过从下拉列表中选择 `UserProfiles` 表并选择要返回的列来指定要查询的数据（参见图9）。 但这一次，我们想要创建一个 SQL 语句，该语句不仅提取来自 `GuestbookComments`的记录，还会提取注释者的 home、home、签名和用户名。 因此，请选择 "指定自定义 SQL 语句或存储过程" 单选按钮，然后单击 "下一步"。

这将显示 "定义自定义语句或存储过程" 屏幕。 单击 "查询生成器" 按钮以图形方式生成查询。 查询生成器首先提示我们指定要查询的表。 选择 `GuestbookComments`、`UserProfiles`和 `aspnet_Users` 表，然后单击 "确定"。 这会将所有三个表添加到设计图面。 由于 `GuestbookComments`、`UserProfiles`和 `aspnet_Users` 表之间存在外键约束，因此查询生成器会自动 `JOIN` 这些表。

剩下的就是指定要返回的列。 从 "`GuestbookComments`" 表中，选择 "`Subject`"、"`Body`" 和 "`CommentDate`" 列;从 `UserProfiles` 表中返回 `HomeTown`、`HomepageUrl`和 `Signature` 列;并从 `aspnet_Users`返回 `UserName`。 此外，将 "`ORDER BY CommentDate DESC`" 添加到 `SELECT` 查询的末尾，以便先返回最新的帖子。 进行这些选择后，查询生成器界面应类似于图18中的屏幕截图。

[![构造的查询联接了 GuestbookComments、UserProfiles 和 aspnet_Users 表](storing-additional-user-information-vb/_static/image53.png)](storing-additional-user-information-vb/_static/image52.png)

**图 18**：构造的查询 `JOIN` `GuestbookComments`、`UserProfiles`和 `aspnet_Users` 表（[单击查看完全大小的图像](storing-additional-user-information-vb/_static/image54.png)）

单击 "确定" 以关闭查询生成器窗口，并返回到 "定义自定义语句或存储过程" 屏幕。 单击 "下一步" 以转到 "测试查询" 屏幕，你可以通过单击 "测试查询" 按钮查看查询结果。 准备就绪后，单击 "完成" 以完成 "配置数据源" 向导。

完成步骤2中的 "配置数据源" 向导时，会更新关联的 DetailsView 控件的 `Fields` 集合，使其包含 `SelectCommand`返回的每个列的 BoundField。 但 ListView 仍保持不变;我们仍需要定义其布局。 ListView 的布局可以通过其声明性标记或其智能标记中的 "配置 ListView" 选项手动构造。 我通常更喜欢手动定义标记，但使用最适合您的任何方法。

对于我的 ListView 控件，我最终使用了以下 `LayoutTemplate`、`ItemTemplate`和 `ItemSeparatorTemplate`：

[!code-aspx[Main](storing-additional-user-information-vb/samples/sample10.aspx)]

`LayoutTemplate` 定义控件发出的标记，而 `ItemTemplate` 呈现 SqlDataSource 返回的每个项。 `ItemTemplate`的结果标记放置在 `LayoutTemplate`的 `itemPlaceholder` 控件中。 除了 `itemPlaceholder`之外，`LayoutTemplate` 还包括一个 DataPager 控件，该控件限制 ListView 只显示每个页面10个留言簿评论（默认值），并呈现分页接口。

我的 `ItemTemplate` 会在 `<h4>` 元素中显示每个留言簿评论的主题，正文位于该主题下。 请注意，用于显示正文的语法采用 `Eval("Body")` databinding 语句返回的数据，将其转换为字符串，并将换行符替换为 `<br />` 元素。 需要进行此转换，以便在提交注释时显示所输入的换行符，因为 HTML 将忽略空格。 用户的签名显示在正文的下方，以斜体显示，后跟用户的主城市、指向其主页的链接、注释的日期和时间，以及离开评论的人员的用户名。

花点时间查看浏览器中的页面。 应该会看到你在此处显示的步骤5中已添加到留言簿的注释。

[![留言簿现在显示留言簿的评论](storing-additional-user-information-vb/_static/image56.png)](storing-additional-user-information-vb/_static/image55.png)

**图 19**： `Guestbook.aspx` 现在显示留言簿的注释（[单击查看完全大小的图像](storing-additional-user-information-vb/_static/image57.png)）

尝试向留言簿添加新评论。 单击 "`PostCommentButton`" 按钮将回发页面，并将注释添加到数据库中，但不会更新 ListView 控件以显示新注释。 这可以通过以下方法之一来解决：

- 更新 `PostCommentButton` 按钮 `Click` 事件处理程序，以便在将新注释插入数据库后调用 ListView 控件的 `DataBind()` 方法，或
- 将 ListView 控件的 `EnableViewState` 属性设置为 `False`。 此方法的工作方式是，通过禁用控件的视图状态，它必须在每次回发时重新绑定到基础数据。

本教程中的可下载的教程网站演示了这两种方法。 要 `False` 的 ListView 控件的 `EnableViewState` 属性以及以编程方式将数据重新绑定到 ListView 所需的代码存在于 `Click` 事件处理程序中，但已被注释掉。

> [!NOTE]
> 目前，"`AdditionalUserInfo.aspx`" 页允许用户查看和编辑其主城市、主页和签名设置。 更新 `AdditionalUserInfo.aspx` 以显示已登录用户的留言簿注释可能很好。 也就是说，除了检查和修改信息，用户还可以访问 "`AdditionalUserInfo.aspx`" 页面，查看她在过去做出了哪些留言簿评论。 对于感兴趣的读者来说，我将其作为练习。

## <a name="step-6-customizing-the-createuserwizard-control-to-include-an-interface-for-the-home-town-homepage-and-signature"></a>步骤6：自定义 CreateUserWizard 控件，使其包含家庭城镇、主页和签名的接口

`Guestbook.aspx` 页使用的 `SELECT` 查询使用 `INNER JOIN` 来合并 `GuestbookComments`、`UserProfiles`和 `aspnet_Users` 表中的相关记录。 如果在 `UserProfiles` 中没有记录的用户发出留言簿注释，则注释将不会显示在 ListView 中，因为 `INNER JOIN` 仅当存在匹配的 `UserProfiles` 和 `aspnet_Users`中的记录时，才会返回 `GuestbookComments` 记录。 如步骤3中所示，如果用户在中没有记录 `UserProfiles` 她无法在 `AdditionalUserInfo.aspx` 页中查看或编辑她的设置。

不用说，由于我们的设计决策，成员资格系统中的每个用户帐户在 `UserProfiles` 表中都有匹配的记录，这一点很重要。 我们想要在每次通过 CreateUserWizard 创建新的成员资格用户帐户时，将相应的记录添加到 `UserProfiles`。

如创建[*用户帐户*](creating-user-accounts-vb.md)教程中所述，在创建新的成员资格用户帐户后，CreateUserWizard 控件会引发其[`CreatedUser` 事件](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.createduser.aspx)。 我们可以为此事件创建事件处理程序，获取刚刚创建的用户的 UserId，然后使用 `HomeTown`、`HomepageUrl`和 `Signature` 列的默认值将记录插入到 `UserProfiles` 表中。 另外，还可以通过自定义 CreateUserWizard 控件的界面以包括其他文本框来提示用户输入这些值。

首先，让我们看看如何使用默认值向 `CreatedUser` 事件处理程序中的 `UserProfiles` 表中添加新行。 接下来，我们将了解如何自定义 CreateUserWizard 控件的用户界面，以包含其他窗体字段以收集新用户的 "住宅"、"主页" 和 "签名"。

### <a name="adding-a-default-row-touserprofiles"></a>向`UserProfiles` 添加默认行

在[*创建用户帐户*](creating-user-accounts-vb.md)教程中，我们向 `Membership` 文件夹中的 `CreatingUserAccounts.aspx` 页添加了 CreateUserWizard 控件。 为了使 CreateUserWizard 控件在创建用户帐户时向 `UserProfiles` 表添加一条记录，我们需要更新 CreateUserWizard 控件的功能。 我们改为将新的 CreateUserWizard 控件添加到 `EnhancedCreateUserWizard.aspx` 页面，并在其中进行本教程的修改，而不是对 `CreatingUserAccounts.aspx` 页面进行这些更改。

在 Visual Studio 中打开 `EnhancedCreateUserWizard.aspx` 页面，并将 "CreateUserWizard" 控件从 "工具箱" 拖到页面上。 将 CreateUserWizard 控件的 `ID` 属性设置为 `NewUserWizard`。 如我们在[*创建用户帐户*](creating-user-accounts-vb.md)教程中所述，CreateUserWizard 的默认用户界面将提示访问者提供所需的信息。 提供此信息后，控件将在成员身份框架中创建新的用户帐户，所有这些都无需编写一行代码即可。

CreateUserWizard 控件在其工作流中引发了许多事件。 在访问者提供请求信息并提交窗体后，CreateUserWizard 控件最初会激发其[`CreatingUser` 事件](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.creatinguser.aspx)。 如果在创建过程中出现问题，则激发[`CreateUserError` 事件](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.createusererror.aspx);但是，如果已成功创建用户，则会引发[`CreatedUser` 事件](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.createduser.aspx)。 在[*创建用户帐户*](creating-user-accounts-vb.md)教程中，我们为 `CreatingUser` 事件创建了一个事件处理程序，以确保所提供的用户名不包含任何前导空格或尾随空格，并且该用户名未出现在密码中的任何位置。

若要为刚创建的用户添加 `UserProfiles` 表中的行，则需要为 `CreatedUser` 事件创建事件处理程序。 当 `CreatedUser` 事件激发时，已在成员身份框架中创建用户帐户，从而使我们能够检索帐户的 UserId 值。

为 `NewUserWizard`的 `CreatedUser` 事件创建事件处理程序并添加以下代码：

[!code-vb[Main](storing-additional-user-information-vb/samples/sample11.vb)]

上述代码将检索刚刚添加的用户帐户的 UserId。 这是通过使用 `Membership.GetUser(username)` 方法返回特定用户的信息，然后使用 `ProviderUserKey` 属性检索其 UserId 来实现的。 用户在 CreateUserWizard 控件中输入的用户名通过其[`UserName` 属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.username.aspx)提供。

接下来，从 `Web.config` 检索连接字符串，并指定 `INSERT` 语句。 必要的 ADO.NET 对象将实例化并执行命令。 该代码将[`DBNull`](https://msdn.microsoft.com/library/system.dbnull.aspx)实例分配给 `@HomeTown`、`@HomepageUrl`和 `@Signature` 参数，这会对 `NULL`、`HomeTown`和 `HomepageUrl`字段插入数据库 `Signature` 值的影响。

通过浏览器访问 `EnhancedCreateUserWizard.aspx` 页面，然后创建新的用户帐户。 完成此操作后，返回到 Visual Studio 并检查 `aspnet_Users` 和 `UserProfiles` 表的内容（如图12所示）。 你应该会在 `aspnet_Users` 中看到新用户帐户，并在相应的 `UserProfiles` 行中看到 `NULL` 值 `HomeTown`、`HomepageUrl`和 `Signature`。

[已添加新用户帐户和 UserProfiles 记录 ![](storing-additional-user-information-vb/_static/image59.png)](storing-additional-user-information-vb/_static/image58.png)

**图 20**：添加了新的用户帐户和 `UserProfiles` 记录（[单击查看完全大小的映像](storing-additional-user-information-vb/_static/image60.png)）

在访问者提供了新的帐户信息并单击 "创建用户" 按钮后，将创建用户帐户，并将一行添加到 `UserProfiles` 表。 然后，CreateUserWizard 将显示其 `CompleteWizardStep`，它将显示一条成功消息和一个 "继续" 按钮。 单击 "继续" 按钮会导致回发，但不会执行任何操作，而是使用户停留在 `EnhancedCreateUserWizard.aspx` 页面上。

通过 CreateUserWizard 控件的[`ContinueDestinationPageUrl` 属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.continuedestinationpageurl.aspx)单击 "继续" 按钮时，可以指定用于将用户发送到的 URL。 将 `ContinueDestinationPageUrl` 属性设置为 "~/Membership/AdditionalUserInfo.aspx"。 这会使新用户 `AdditionalUserInfo.aspx`，用户可以在其中查看和更新其设置。

### <a name="customizing-the-createuserwizards-interface-to-prompt-for-the-new-users-home-town-homepage-and-signature"></a>自定义 CreateUserWizard 的界面，以提示输入新用户的家庭城镇、主页和签名

CreateUserWizard 控件的默认接口足以满足只收集核心用户帐户信息（如用户名、密码和电子邮件）的简单帐户创建方案。 但是，如果我们希望在创建帐户时提示访问者输入她的住宅、主页和签名，该怎么办？ 可以自定义 CreateUserWizard 控件的接口，以便在注册时收集其他信息，该信息可在 `CreatedUser` 事件处理程序中使用，以将其他记录插入到基础数据库中。

CreateUserWizard 控件扩展了 ASP.NET 向导控件，该控件允许页开发人员定义一系列排序 `WizardSteps`。 向导控件将呈现活动步骤并提供导航界面，使访问者可以在这些步骤中完成操作。 向导控件非常适合用于将较长的任务分解为几个简短的步骤。 有关向导控件的详细信息，请参阅[使用 ASP.NET 2.0 向导控件创建分步用户界面](http://aspnet.4guysfromrolla.com/articles/061406-1.aspx)。

CreateUserWizard 控件的默认标记定义了两个 `WizardSteps`： `CreateUserWizardStep` 和 `CompleteWizardStep`。

[!code-aspx[Main](storing-additional-user-information-vb/samples/sample12.aspx)]

第一个 `WizardStep``CreateUserWizardStep`，它会呈现提示输入用户名、密码、电子邮件等的接口。 在访问者提供此信息并单击 "创建用户" 后，将显示 "`CompleteWizardStep`"，其中显示了 "成功" 消息和 "继续" 按钮。

若要自定义 CreateUserWizard 控件的接口以包含其他窗体字段，可以：

- <strong>创建一个或多个新</strong>的<strong>`WizardStep`</strong> <strong>，以包含其他用户界面元素</strong>。 若要将新 `WizardStep` 添加到 CreateUserWizard，请单击其智能标记中的 "添加/删除 `WizardStep` s" 链接以启动 `WizardStep` 集合编辑器。 在该处，你可以在向导中添加、删除或重新排序步骤。 本教程将使用这种方法。

- <strong>将</strong><strong>`CreateUserWizardStep`</strong>转换为<strong>可编辑</strong><strong>`WizardStep`</strong> <strong>。</strong> 这会将 `CreateUserWizardStep` 替换为等效的 `WizardStep`，其标记定义了与 `CreateUserWizardStep`的匹配的用户界面。 通过将 `CreateUserWizardStep` 转换为 `WizardStep` 我们可以重新定位控件或向此步骤添加其他用户界面元素。 若要将 `CreateUserWizardStep` 或 `CompleteWizardStep` 转换为可编辑 `WizardStep`，请在控件的智能标记中单击 "自定义创建用户步骤" 或 "自定义完整步骤" 链接。

- **使用上述两个选项的某种组合。**

需要注意的一个重要事项是，CreateUserWizard 控件在其 `CreateUserWizardStep`中单击 "创建用户" 按钮时执行其用户帐户创建过程。 如果 `CreateUserWizardStep` 之后还有其他 `WizardStep`，就不是那么重要。

将自定义 `WizardStep` 添加到 CreateUserWizard 控件以收集其他用户输入时，可以将自定义 `WizardStep` 置于 `CreateUserWizardStep`之前或之后。 如果在 `CreateUserWizardStep` 之前，则从自定义 `WizardStep` 收集的其他用户输入可用于 `CreatedUser` 事件处理程序。 但是，如果自定义 `WizardStep` 晚于 `CreateUserWizardStep` 然后在自定义 `WizardStep` 显示时，则已创建新用户帐户，并且已激发 `CreatedUser` 事件。

图21显示了在 `CreateUserWizardStep`之前添加的 `WizardStep` 的工作流。 由于在 `CreatedUser` 事件引发时，已收集了其他用户信息，因此我们只需更新 `CreatedUser` 事件处理程序来检索这些输入，并将这些输入用于 `INSERT` 语句的参数值（而不是 `DBNull.Value`）。

[如果在 Createuserwizardstep.contenttemplate 之前附加 WizardStep，![CreateUserWizard 工作流](storing-additional-user-information-vb/_static/image62.png)](storing-additional-user-information-vb/_static/image61.png)

**图 21**： CreateUserWizard 工作流在 `CreateUserWizardStep` 之前 `WizardStep` （[单击查看完全大小的图像](storing-additional-user-information-vb/_static/image63.png)）

但是，如果将自定义 `WizardStep` 放置在 `CreateUserWizardStep`*之后*，则在用户有机会进入她的 home、home 或 signature 之前，会发生 "创建用户帐户" 过程。 在这种情况下，在创建用户帐户后，需要将此附加信息插入到数据库中，如图22所示。

[Createuserwizardstep.contenttemplate 后的其他 WizardStep ![CreateUserWizard 工作流](storing-additional-user-information-vb/_static/image65.png)](storing-additional-user-information-vb/_static/image64.png)

**图 22**： `CreateUserWizardStep` 上出现其他 `WizardStep` 时的 CreateUserWizard 工作流（[单击以查看完全大小的图像](storing-additional-user-information-vb/_static/image66.png)）

图22中显示的工作流将等待在步骤2完成之后，将记录插入到 `UserProfiles` 表中。 不过，如果访问者在步骤1后关闭她的浏览器，则会在创建用户帐户时达到状态，但不会将任何记录添加到 `UserProfiles`。 一种解决方法是将具有 `NULL` 或默认值的记录插入到 `CreatedUser` 事件处理程序中的 `UserProfiles` （在步骤1之后触发），然后在步骤2完成后更新此记录。 这可确保将为用户帐户添加 `UserProfiles` 记录，即使用户在中间退出注册过程也是如此。

在本教程中，我们将创建一个在 `CreateUserWizardStep` 之后但在 `CompleteWizardStep`之前发生的新 `WizardStep`。 首先，让我们准备好 WizardStep 并进行配置，然后查看代码。

在 CreateUserWizard 控件的智能标记中，选择 "添加/删除 `WizardStep` s"，这将打开 "`WizardStep` 集合编辑器" 对话框。 添加新的 `WizardStep`，并将其 `ID` 设置为 `UserSettings`，并将其 `Title` 为 "你的设置"，并将其 `StepType` 设置为 `Step`。 然后将其定位到 `CreateUserWizardStep` （"注册新帐户"）之前和 `CompleteWizardStep` （"完成"）之前，如图23所示。

[![将新的 WizardStep 添加到 CreateUserWizard 控件](storing-additional-user-information-vb/_static/image68.png)](storing-additional-user-information-vb/_static/image67.png)

**图 23**：向 CreateUserWizard 控件添加新的 `WizardStep` （[单击以查看完全大小的图像](storing-additional-user-information-vb/_static/image69.png)）

单击 "确定" 以关闭 "`WizardStep` 集合编辑器" 对话框。 新 `WizardStep` 由 CreateUserWizard 控件的更新声明性标记出现：

[!code-aspx[Main](storing-additional-user-information-vb/samples/sample13.aspx)]

请注意新的 `<asp:WizardStep>` 元素。 需要在此处添加用户界面以收集新用户的 "住宅"、"主页" 和 "签名"。 可在声明性语法中或通过设计器输入此内容。 若要使用设计器，请从智能标记的下拉列表中选择 "设置" 步骤，以查看设计器中的步骤。

> [!NOTE]
> 通过智能标记的下拉列表选择一个步骤，可更新 CreateUserWizard 控件的[`ActiveStepIndex` 属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.activestepindex.aspx)，该属性指定起始步骤的索引。 因此，如果使用此下拉列表来编辑设计器中的 "设置" 步骤，请确保将其设置回 "注册新帐户"，以便在用户首次访问 `EnhancedCreateUserWizard.aspx` 页面时显示此步骤。

在 "设置" 步骤中创建一个用户界面，其中包含三个名为 `HomeTown`、`HomepageUrl`和 `Signature`的 TextBox 控件。 构造此接口后，CreateUserWizard 的声明性标记应如下所示：

[!code-aspx[Main](storing-additional-user-information-vb/samples/sample14.aspx)]

继续下一步，通过浏览器访问此页，创建新的用户帐户，并指定 home、home 和签名的值。 完成后 `CreateUserWizardStep` 在成员身份框架中创建用户帐户，并运行 `CreatedUser` 事件处理程序，该事件处理程序会将新行添加到 `UserProfiles`，但对于 `HomeTown`、`HomepageUrl`和 `Signature`，数据库 `NULL` 值为。 为 home、home 和 signature 输入的值永远不会使用。 Net 结果是一个新的用户帐户，其中包含尚未指定其 `HomeTown`、`HomepageUrl`和 `Signature` 字段的 `UserProfiles` 记录。

我们需要在 "你的设置" 步骤后执行代码，该步骤使用用户输入的 "住宅"、"honepage" 和 "签名" 值，并更新相应的 `UserProfiles` 记录。 用户每次在向导控件中的步骤间移动时，都会激发向导的[`ActiveStepChanged` 事件](https://msdn.microsoft.com/library/system.web.ui.webcontrols.wizard.activestepchanged.aspx)。 我们可以创建此事件的事件处理程序，并在 "设置" 步骤完成后更新 `UserProfiles` 表。

为 CreateUserWizard 的 `ActiveStepChanged` 事件添加事件处理程序，并添加以下代码：

[!code-vb[Main](storing-additional-user-information-vb/samples/sample15.vb)]

上述代码首先确定是否已到达 "完成" 步骤。 由于 "完成" 步骤会在 "您的设置" 步骤之后立即发生，因此当访问者达到 "完成" 步骤时，意味着她刚刚完成了 "您的设置" 步骤。

在这种情况下，我们需要以编程方式引用 `UserSettings WizardStep`中的 TextBox 控件。 首先使用 `FindControl` 方法以编程方式引用 `UserSettings WizardStep`，然后再次从 `WizardStep`中引用文本框来完成此操作。 引用文本框后，便可以执行 `UPDATE` 语句了。 `UPDATE` 语句与 `CreatedUser` 事件处理程序中的 `INSERT` 语句具有相同数目的参数，但此处我们使用的是用户提供的 home 城镇、主页和签名值。

完成此事件处理程序后，通过浏览器访问 `EnhancedCreateUserWizard.aspx` 页面，然后创建新的用户帐户，以指定 home、主页和签名的值。 创建新帐户后，应重定向到 "`AdditionalUserInfo.aspx`" 页，其中显示刚刚输入的 "住宅"、"主页" 和 "签名" 信息。

> [!NOTE]
> 网站当前有两个页面，访问者可以在其中创建新帐户： `CreatingUserAccounts.aspx` 和 `EnhancedCreateUserWizard.aspx`。 网站的 "站点地图" 和 "登录" 页指向 "`CreatingUserAccounts.aspx`" 页，但 "`CreatingUserAccounts.aspx`" 页不会提示用户输入其 home 城镇、主页和签名信息，也不会将相应的行添加到 `UserProfiles`中。 因此，请更新 `CreatingUserAccounts.aspx` 页面，使其提供此功能，或更新站点地图和登录页以引用 `EnhancedCreateUserWizard.aspx` 而不是 `CreatingUserAccounts.aspx`。 如果选择后一种方法，请确保更新 `Membership` 文件夹的 `Web.config` 文件，以便允许匿名用户访问 `EnhancedCreateUserWizard.aspx` 页面。

## <a name="summary"></a>总结

在本教程中，我们将介绍与成员身份框架中的用户帐户相关的数据建模方法。 具体而言，我们了解到与用户帐户共享一对多关系的建模实体，以及共享一对一关系的数据。 此外，我们还看到了如何显示、插入和更新此相关信息，其中有一些示例使用 SqlDataSource 控件和其他使用 ADO.NET 代码的示例。

本教程介绍了用户帐户。 从下一教程开始，我们将关注角色。 在接下来的几个教程中，我们将探讨角色框架，了解如何创建新角色，如何为用户分配角色，如何确定用户所属的角色，以及如何应用基于角色的授权。

很高兴编程！

### <a name="further-reading"></a>其他阅读材料

有关本教程中讨论的主题的详细信息，请参阅以下资源：

- [在 ASP.NET 2.0 中访问和更新数据](http://aspnet.4guysfromrolla.com/articles/011106-1.aspx)
- [ASP.NET 2.0 向导控件](https://weblogs.asp.net/scottgu/archive/2006/02/21/438732.aspx)
- [使用 ASP.NET 2.0 向导控件创建分步用户界面](http://aspnet.4guysfromrolla.com/articles/061406-1.aspx)
- [创建自定义数据源控件参数](http://aspnet.4guysfromrolla.com/articles/110106-1.aspx)
- [自定义 CreateUserWizard 控件](http://aspnet.4guysfromrolla.com/articles/070506-1.aspx)
- [DetailsView 控件快速入门](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/ctrlref/data/detailsview.aspx)
- [用 ListView 控件显示数据](http://aspnet.4guysfromrolla.com/articles/122607-1.aspx)
- [二级 ASP.NET 2.0 中的验证控件](http://aspnet.4guysfromrolla.com/articles/112305-1.aspx)
- [编辑插入和删除数据](../../data-access/editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-cs.md)
- [ASP.NET 中的窗体验证](http://www.4guysfromrolla.com/webtech/090200-1.shtml)
- [正在收集自定义用户注册信息](https://weblogs.asp.net/scottgu/archive/2006/07/05/Tip_2F00_Trick_3A00_-Gathering-Custom-User-Registration-Information.aspx)
- [ASP.NET 2.0 中的配置文件](http://www.odetocode.com/Articles/440.aspx)
- [Asp： ListView 控件](https://weblogs.asp.net/scottgu/archive/2007/08/10/the-asp-listview-control-part-1-building-a-product-listing-page-with-clean-css-ui.aspx)
- [用户配置文件快速入门](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/profile/default.aspx)

### <a name="about-the-author"></a>关于作者

Scott Mitchell，创始人的多个 ASP/ASP 和4GuysFromRolla.com 的作者已使用 Microsoft Web 技术，1998。 Scott 的工作方式是独立的顾问、培训师和撰稿人。 他的最新书籍是， *[在24小时内，sam ASP.NET 2.0](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)* 。 可以通过[http://ScottOnWriting.NET](http://scottonwriting.net/) [mitchell@4guysfromrolla.com](mailto:mitchell@4guysfromrolla.com)或通过他的博客访问 Scott。

### <a name="special-thanks-to"></a>特别感谢 。

此教程系列由许多有用的审阅者查看。 想要查看我即将发布的 MSDN 文章？ 如果是这样，请在[mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)放置一行。

> [!div class="step-by-step"]
> [上一部分](user-based-authorization-vb.md)
