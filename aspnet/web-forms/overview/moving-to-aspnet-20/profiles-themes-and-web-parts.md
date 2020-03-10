---
uid: web-forms/overview/moving-to-aspnet-20/profiles-themes-and-web-parts
title: 配置文件、主题和 Web 部件 |Microsoft Docs
author: microsoft
description: ASP.NET 2.0 中的配置和检测有重大变化。 新的 ASP.NET 配置 API 允许将配置更改为 pr 。
ms.author: riande
ms.date: 02/20/2005
ms.assetid: 92df4051-77c6-492c-bd34-23d24189cea4
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/profiles-themes-and-web-parts
msc.type: authoredcontent
ms.openlocfilehash: cf5c45781be6d003d28c6aa27efa08032579a6dd
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78474638"
---
# <a name="profiles-themes-and-web-parts"></a>配置文件、主题和 Web 部件

由[Microsoft](https://github.com/microsoft)

> ASP.NET 2.0 中的配置和检测有重大变化。 新的 ASP.NET 配置 API 允许以编程方式进行配置更改。 此外，还存在许多新的配置设置，允许进行新配置和检测。

ASP.NET 2.0 表示个性化网站领域的重大改进。 除了我们已介绍的成员资格功能外，ASP.NET 的配置文件、主题和 Web 部件还大幅增强了网站的个性化。

## <a name="aspnet-profiles"></a>ASP.NET 配置文件

ASP.NET 配置文件类似于会话。 差别在于，配置文件是持久性的，而当浏览器关闭时会话丢失。 会话和配置文件的另一个重要区别在于，配置文件是强类型，因此在开发过程中为您提供 IntelliSense。

配置文件是在计算机配置文件或应用程序的 web.config 文件中定义的。 （无法在子文件夹的 web.config 文件中定义配置文件。）下面的代码定义了一个配置文件，用于存储网站访问者的名字和姓氏。

[!code-xml[Main](profiles-themes-and-web-parts/samples/sample1.xml)]

配置文件属性的默认数据类型为 System.string。 在上面的示例中，未指定数据类型。 因此，FirstName 和 LastName 属性都是 String 类型。 如前文所述，配置文件属性为强类型。 下面的代码为类型为 Int32 的 age 添加了一个新属性。

[!code-xml[Main](profiles-themes-and-web-parts/samples/sample2.xml)]

配置文件通常用于 ASP.NET Forms 身份验证。 与 Forms 身份验证结合使用时，每个用户都有一个与其用户 ID 相关联的单独的配置文件。 但是，还可以使用配置文件中 &lt;anonymousIdentification&gt; 元素和**allowAnonymous**属性，允许在匿名应用程序中使用配置文件，如下所示：

[!code-xml[Main](profiles-themes-and-web-parts/samples/sample3.xml)]

匿名用户浏览站点时，ASP.NET 将为用户创建**ProfileCommon**的实例。 此配置文件使用存储在浏览器的 cookie 中的唯一 ID 将用户标识为唯一的访问者。 通过这种方式，您可以为匿名浏览的用户存储配置文件信息。

## <a name="profile-groups"></a>配置文件组

可以对配置文件的属性进行分组。 通过对属性进行分组，可以为特定的应用程序模拟多个配置文件。

以下配置配置两个组的 FirstName 和 LastName 属性;买家和潜在客户。

[!code-xml[Main](profiles-themes-and-web-parts/samples/sample4.xml)]

然后，可以设置特定组的属性，如下所示：

[!code-csharp[Main](profiles-themes-and-web-parts/samples/sample5.cs)]

## <a name="storing-complex-objects"></a>存储复杂对象

到目前为止，我们介绍的示例已经在配置文件中存储了简单的数据类型。 还可以通过使用**serializeAs**特性指定序列化方法，将复杂数据类型存储在配置文件中，如下所示：

[!code-xml[Main](profiles-themes-and-web-parts/samples/sample6.xml)]

在这种情况下，类型为 PurchaseInvoice。 需要将 PurchaseInvoice 类标记为可序列化，并且可以包含任意数量的属性。 例如，如果 PurchaseInvoice 有一个名为**NumItemsPurchased**的属性，则可以在代码中引用该属性，如下所示：

[!code-css[Main](profiles-themes-and-web-parts/samples/sample7.css)]

## <a name="profile-inheritance"></a>配置文件继承

可以创建一个配置文件，以便在多个应用程序中使用。 通过创建派生自 ProfileBase 的配置文件类，您可以使用**继承**属性在多个应用程序中重复使用配置文件，如下所示：

[!code-xml[Main](profiles-themes-and-web-parts/samples/sample8.xml)]

在这种情况下，类**PurchasingProfile**如下所示：

[!code-csharp[Main](profiles-themes-and-web-parts/samples/sample9.cs)]

## <a name="profile-providers"></a>配置文件提供程序

ASP.NET 配置文件使用提供程序模型。 默认提供程序使用 SqlProfileProvider 提供程序，将信息存储在 Web 应用程序的应用\_数据文件夹中的 SQL Server Express 数据库中。 如果数据库不存在，则当配置文件尝试存储信息时，ASP.NET 将自动创建该数据库。

但是，在某些情况下，你可能想要开发自己的配置文件提供程序。 使用 ASP.NET 配置文件可以轻松地使用不同的提供程序。

在以下情况时创建自定义配置文件提供程序：

- 需要将配置文件信息存储在数据源中，如在 FoxPro 数据库或 Oracle 数据库中，.NET Framework 中包含的配置文件提供程序不支持此信息。
- 你需要使用与 .NET Framework 中包含的提供程序使用的数据库架构不同的数据库架构来管理配置文件信息。 常见的示例是，你想要将配置文件信息与现有 SQL Server 数据库中的用户数据集成。

### <a name="required-classes"></a>必需的类

若要实现配置文件提供程序，需要创建一个继承 ProfileProvider 抽象类的类。 **ProfileProvider**抽象类又继承了 SettingsProvider 抽象类，该类继承了 ProviderBase 抽象类的情况。 由于此继承链，除了**ProfileProvider**类的必需成员以外，还必须实现**SettingsProvider**和**ProviderBase**类的必需成员。

下表描述了必须从**ProviderBase**、 **SettingsProvider**和**ProfileProvider**抽象类实现的属性和方法。

### <a name="providerbase-members"></a>ProviderBase 成员

| **成员** | **描述** |
| --- | --- |
| Initialize 方法 | 使用提供程序实例的名称和配置设置的 NameValueCollection 作为输入。 用于设置提供程序实例的选项和属性值，包括在计算机配置或 web.config 文件中指定的特定于实现的值和选项。 |

### <a name="settingsprovider-members"></a>SettingsProvider 成员

| **成员** | **描述** |
| --- | --- |
| ApplicationName 属性 | 随每个配置文件一起存储的应用程序名称。 配置文件提供程序使用应用程序名称分别存储每个应用程序的配置文件信息。 这样，如果在不同的应用程序中创建相同的用户名，多个 ASP.NET 应用程序就可以使用相同的数据源，而不会发生冲突。 另外，多个 ASP.NET 应用程序可以通过指定相同的应用程序名称来共享配置文件数据源。 |
| System.configuration.settingsprovider.getpropertyvalues 方法 | 将 SettingsContext 和 SettingsPropertyCollection 对象作为输入。 **SettingsContext**提供有关用户的信息。 您可以使用此信息作为主键来检索用户的配置文件属性信息。 使用**SettingsContext**对象可获取用户名，以及用户是否已通过身份验证或匿名身份验证。 **SettingsPropertyCollection**包含 SettingsProperty 对象的集合。 每个**SettingsProperty**对象都提供属性的名称和类型，以及附加信息（例如属性的默认值）以及属性是否为只读。 **System.configuration.settingsprovider.getpropertyvalues**方法根据作为输入提供的**SettingsProperty**对象，将 SettingsPropertyValueCollection 替换为 SettingsPropertyValue 对象。 将指定用户的数据源中的值分配给每个**SettingsPropertyValue**对象的 PropertyValue 属性，并返回整个集合。 调用方法还会将指定用户配置文件的 LastActivityDate 值更新为当前日期和时间。 |
| SetPropertyValues 方法 | 将**SettingsContext**和**SettingsPropertyValueCollection**对象作为输入。 **SettingsContext**提供有关用户的信息。 您可以使用此信息作为主键来检索用户的配置文件属性信息。 使用**SettingsContext**对象可获取用户名，以及用户是否已通过身份验证或匿名身份验证。 **SettingsPropertyValueCollection**包含**SettingsPropertyValue**对象的集合。 每个**SettingsPropertyValue**对象都提供属性的名称、类型和值以及其他信息，如属性的默认值以及属性是否为只读。 **SetPropertyValues**方法更新指定用户的数据源中的配置文件属性值。 调用方法还会将指定用户配置文件的**LastActivityDate**和 LastUpdatedDate 值更新为当前日期和时间。 |

### <a name="profileprovider-members"></a>ProfileProvider 成员

| **成员** | **描述** |
| --- | --- |
| DeleteProfiles 方法 | 采用用户名的字符串数组作为输入，并从数据源中删除应用程序名称与**ApplicationName**属性值匹配的指定名称的所有配置文件信息和属性值。 如果你的数据源支持事务，则建议你将所有删除操作包含在一个事务中，并在任何删除操作失败的情况下回滚该事务并引发异常。 |
| DeleteProfiles 方法 | 作为输入输入 ProfileInfo 对象的集合，并从数据源中删除应用程序名称与**ApplicationName**属性值匹配的每个配置文件的所有配置文件信息和属性值。 如果您的数据源支持事务，则建议您在一个事务中包含所有删除操作，并回滚该事务，并且在任何删除操作失败时引发异常。 |
| DeleteInactiveProfiles 方法 | 将 ProfileAuthenticationOption 值和 DateTime 对象作为输入，并从数据源中删除所有的配置文件信息和属性值，其中最后一个活动的日期小于或等于指定的日期和时间，且应用程序名称与**ApplicationName**属性值匹配。 **ProfileAuthenticationOption**参数指定是仅删除匿名配置文件、仅删除经过身份验证的配置文件还是删除所有配置文件。 如果您的数据源支持事务，则建议您在一个事务中包含所有删除操作，并回滚该事务，并且在任何删除操作失败时引发异常。 |
| GetAllProfiles 方法 | 采用**ProfileAuthenticationOption**值作为输入，指定页面索引的整数，指定页面大小的整数，以及对将设置为配置文件总数的整数的引用。 返回一个 ProfileInfoCollection，其中包含与**ApplicationName**属性值匹配的数据源中所有配置文件的**ProfileInfo**对象。 **ProfileAuthenticationOption**参数指定是只返回匿名配置文件、仅返回经过身份验证的配置文件还是返回所有配置文件。 **GetAllProfiles**方法返回的结果受页索引和页大小值的约束。 页面大小值指定要在**ProfileInfoCollection**中返回的**ProfileInfo**对象的最大数目。 页索引值指定要返回的结果页，其中1标识第一页。 Total 记录的参数是 out 参数（可以在 Visual Basic 中使用**ByRef** ），该参数设置为配置文件总数。 例如，如果数据存储包含应用程序的13个配置文件，并且页索引值为2且页面大小为5，则返回的**ProfileInfoCollection**包含第六个到第10个配置文件。 当该方法返回时，总记录值设置为13。 |
| GetAllInactiveProfiles 方法 | 使用**ProfileAuthenticationOption**值、 **DateTime**对象、指定页面索引的整数、指定页面大小的整数和对将设置为配置文件总数的整数的引用。 返回一个**ProfileInfoCollection** ，该对象包含数据源中的所有配置文件的**ProfileInfo**对象，其中最后一个活动日期小于或等于指定的**DateTime** ，其中应用程序名称与**ApplicationName**属性值匹配。 **ProfileAuthenticationOption**参数指定是只返回匿名配置文件、仅返回经过身份验证的配置文件还是返回所有配置文件。 **GetAllInactiveProfiles**方法返回的结果受页索引和页大小值的约束。 页面大小值指定要在**ProfileInfoCollection**中返回的**ProfileInfo**对象的最大数目。 页索引值指定要返回的结果页，其中1标识第一页。 Total 记录的参数是 out 参数（可以在 Visual Basic 中使用**ByRef** ），该参数设置为配置文件总数。 例如，如果数据存储包含应用程序的13个配置文件，并且页索引值为2且页面大小为5，则返回的**ProfileInfoCollection**包含第六个到第10个配置文件。 当该方法返回时，总记录值设置为13。 |
| FindProfilesByUserName 方法 | 输入一个**ProfileAuthenticationOption**值、一个包含用户名的字符串、一个指定页面索引的整数、一个指定页面大小的整数和对将设置为配置文件总数的整数的引用。 返回一个**ProfileInfoCollection** ，该对象包含数据源中的所有配置文件的**ProfileInfo**对象，其中用户名与指定用户名匹配，其中应用程序名称与**ApplicationName**属性值匹配。 **ProfileAuthenticationOption**参数指定是只返回匿名配置文件、仅返回经过身份验证的配置文件还是返回所有配置文件。 如果数据源支持其他搜索功能（如通配符），则可以为用户名提供更广泛的搜索功能。 **FindProfilesByUserName**方法返回的结果受页索引和页大小值的约束。 页面大小值指定要在**ProfileInfoCollection**中返回的**ProfileInfo**对象的最大数目。 页索引值指定要返回的结果页，其中1标识第一页。 Total 记录的参数是 out 参数（可以在 Visual Basic 中使用**ByRef** ），该参数设置为配置文件总数。 例如，如果数据存储包含应用程序的13个配置文件，并且页索引值为2且页面大小为5，则返回的**ProfileInfoCollection**包含第六个到第10个配置文件。 当该方法返回时，总记录值设置为13。 |
| FindInactiveProfilesByUserName 方法 | 输入**ProfileAuthenticationOption**值、包含用户名的字符串、**日期时间**对象、指定页面索引的整数、指定页面大小的整数和对将设置为配置文件总计数的整数的引用。 返回一个**ProfileInfoCollection** ，该对象包含数据源中的所有配置文件的**ProfileInfo**对象，其中的用户名与指定的用户名相匹配，最后一个活动日期小于或等于指定的**DateTime**，其中应用程序名称与**ApplicationName**属性值匹配。 **ProfileAuthenticationOption**参数指定是只返回匿名配置文件、仅返回经过身份验证的配置文件还是返回所有配置文件。 如果数据源支持其他搜索功能（如通配符），则可以为用户名提供更广泛的搜索功能。 **FindInactiveProfilesByUserName**方法返回的结果受页索引和页大小值的约束。 页面大小值指定要在**ProfileInfoCollection**中返回的**ProfileInfo**对象的最大数目。 页索引值指定要返回的结果页，其中1标识第一页。 Total 记录的参数是 out 参数（可以在 Visual Basic 中使用**ByRef** ），该参数设置为配置文件总数。 例如，如果数据存储包含应用程序的13个配置文件，并且页索引值为2且页面大小为5，则返回的**ProfileInfoCollection**包含第六个到第10个配置文件。 当该方法返回时，总记录值设置为13。 |
| GetNumberOfInActiveProfiles 方法 | 将**ProfileAuthenticationOption**值和**DateTime**对象作为输入，并返回数据源中最后一个活动日期小于或等于指定的**日期时间**并且应用程序名称与**ApplicationName**属性值匹配的所有配置文件的计数。 **ProfileAuthenticationOption**参数指定是否仅对匿名配置文件、仅对经过身份验证的配置文件或所有配置文件进行计数。 |

### <a name="applicationname"></a>ApplicationName

因为配置文件提供程序分别为每个应用程序存储配置文件信息，所以你必须确保你的数据架构包括应用程序名称，并且查询和更新还包括应用程序名称。 例如，下面的命令用于根据用户名和配置文件是否为匿名，从数据库检索属性值，并确保在查询中包括**ApplicationName**值。

[!code-sql[Main](profiles-themes-and-web-parts/samples/sample10.sql)]

## <a name="aspnet-themes"></a>ASP.NET 主题

## <a name="what-are-aspnet-20-themes"></a>什么是 ASP.NET 2.0 主题？

Web 应用程序中最重要的一个方面是网站上一致的外观。 ASP.NET 1.x 开发人员通常使用级联样式表（CSS）来实现一致的外观。 ASP.NET 2.0 主题可显著改进 CSS，因为它们使 ASP.NET 开发人员能够定义 ASP.NET 服务器控件和 HTML 元素的外观。 ASP.NET 主题可应用于单个控件、特定网页或整个 Web 应用程序。 主题结合使用 CSS 文件、可选的外观文件和可选的 Images 目录（如果需要映像）。 外观文件控制 ASP.NET 服务器控件的视觉外观。

## <a name="where-are-themes-stored"></a>主题存储在何处？

根据其作用域，存储主题的位置会有所不同。 可应用到任何应用程序的主题将存储在以下文件夹中：

`C:\WINDOWS\Microsoft.NET\Framework\v2.x.xxxxx\ASP.NETClientFiles\Themes\<Theme_Name>`

特定于特定应用程序的主题存储在网站根目录的 `App\_Themes\<Theme\_Name>` 目录中。

> [!NOTE]
> 外观文件只应修改影响外观的服务器控件属性。

全局主题是可应用于在 Web 服务器上运行的任何应用程序或网站的主题。 默认情况下，这些主题存储在 NETClientfiles\Themes 目录中，该目录位于 v2. x. x。 或者，您可以将主题文件移动到网站根目录下的 aspnet\_client/system\_web/[version]/Themes/[主题\_名称] 文件夹中。

特定于应用程序的主题只能应用于这些文件所在的应用程序。 这些文件存储在网站根目录的 `App\_Themes/<theme\_name>` 目录中。

## <a name="the-components-of-a-theme"></a>主题组件

主题由一个或多个 CSS 文件、一个可选的外观文件和一个可选的 Images 文件夹组成。 CSS 文件可以是任何所需的名称（即，css 或主题 .css 等），并且必须位于 themes 文件夹的根目录中。 CSS 文件用于为特定的选择器定义普通的 CSS 类和属性。 若要将某一 CSS 类应用于 page 元素，请使用**CSSClass**属性。

外观文件是一个 XML 文件，其中包含 ASP.NET 服务器控件的属性定义。 下面列出的代码是一个示例外观文件。

[!code-aspx[Main](profiles-themes-and-web-parts/samples/sample11.aspx)]

下面的**图 1**显示了一个在未应用主题的情况下浏览的小型 ASP.NET 页面。 **图 2**显示了应用主题的同一文件。 通过 CSS 文件配置背景色和文本颜色。 按钮和文本框的外观是使用上面列出的外观文件配置的。

![无主题](profiles-themes-and-web-parts/_static/image1.gif)

**图 1**：无主题

![应用主题](profiles-themes-and-web-parts/_static/image2.gif)

**图 2**：应用主题

上面列出的外观文件定义了所有 TextBox 控件和按钮控件的默认外观。 这意味着，在页上插入的每个 TextBox 控件和 Button 控件都将采用此外观。 你还可以使用控件的**SkinID**属性定义可应用于这些控件的特定实例的外观。

下面的代码定义按钮控件的外观。 只有具有**goButton**的**SkinID**属性的按钮控件才会获得外观的外观。

[!code-aspx[Main](profiles-themes-and-web-parts/samples/sample12.aspx)]

每个服务器控件类型只能有一个默认的外观。 如果需要其他外观，则应使用 SkinID 属性。

## <a name="applying-themes-to-pages"></a>将主题应用于页面

可以使用以下任一方法应用主题：

- 在 web.config 文件的 &lt;pages&gt; 元素中
- 在页面的 @Page 指令中
- 以编程方式

## <a name="applying-a-theme-in-the-configuration-file"></a>在配置文件中应用主题

若要在应用程序配置文件中应用主题，请使用以下语法：

[!code-xml[Main](profiles-themes-and-web-parts/samples/sample13.xml)]

此处指定的主题名称必须与 themes 文件夹的名称匹配。 此文件夹可在本课程前面提到的任何一个位置中存在。 如果尝试应用不存在的主题，将出现配置错误。

## <a name="applying-a-theme-in-the-page-directive"></a>在 Page 指令中应用主题

您还可以在 @ Page 指令中应用主题。 此方法允许你使用特定页面的主题。

若要在 @Page 指令中应用主题，请使用以下语法：

[!code-aspx[Main](profiles-themes-and-web-parts/samples/sample14.aspx)]

同样，此处指定的主题必须与前面提到的主题文件夹匹配。 如果尝试应用不存在的主题，将会发生生成失败。 Visual Studio 还将突出显示该属性，并通知你不存在此类主题。

## <a name="applying-a-theme-programmatically"></a>以编程方式应用主题

若要以编程方式应用主题，必须在**页面\_PreInit**方法中指定页面的**主题**属性。

若要以编程方式应用主题，请使用以下语法：

[!code-csharp[Main](profiles-themes-and-web-parts/samples/sample15.cs)]

由于页面生命周期，需要在 PreInit 方法中应用主题。 如果在该点之后应用此方法，则运行时已应用页面主题，并且在生命周期中该点的更改太晚。 如果应用不存在的主题，则会发生**HttpException** 。 以编程方式应用主题时，如果有任何服务器控件指定了 SkinID 属性，则会发生生成警告。 此警告旨在通知你未以声明方式应用主题，并且可以将其忽略。

## <a name="exercise-1--applying-a-theme"></a>练习1：应用主题

在此练习中，您将向网站应用 ASP.NET 主题。

> [!IMPORTANT]
> 如果使用 Microsoft Word 将信息输入到皮肤文件中，请确保不将引号替换为智能引号。 Smart 引号会导致皮肤文件出现问题。

1. 创建一个新的 ASP.NET 网站。
2. 右键单击 "解决方案资源管理器中的项目，然后选择" 添加新项 "。
3. 从文件列表中选择 "Web 配置文件"，然后单击 "添加"。
4. 右键单击 "解决方案资源管理器中的项目，然后选择" 添加新项 "。
5. 选择 "外观文件"，然后单击 "添加"。
6. 当系统询问你是否要将该文件放置在应用程序\_Themes 文件夹中时，请单击 "是"。
7. 右键单击解决方案资源管理器中应用\_Themes 文件夹内的 "SkinFile" 文件夹，然后选择 "添加新项"。
8. 从文件列表中选择 "样式表"，然后单击 "添加"。 现在，你拥有了实现新主题所需的全部文件。 但是，Visual Studio 已将主题文件夹命名为 SkinFile。 右键单击该文件夹，然后将名称更改为 CoolTheme。
9. 打开 SkinFile 文件，并在该文件的末尾添加以下代码： 

    [!code-aspx[Main](profiles-themes-and-web-parts/samples/sample16.aspx)]
10. 保存 SkinFile 文件。
11. 打开样式表 .css。
12. 将其中的所有文本替换为以下内容： 

    [!code-css[Main](profiles-themes-and-web-parts/samples/sample17.css)]
13. 保存样式表 .css 文件。
14. 打开 default.aspx 页。
15. 添加 TextBox 控件和按钮控件。
16. 保存页。 现在，浏览 default.aspx 页。 它应显示为普通的 Web 窗体。
17. 打开 web.config 文件。
18. 在开始 `<system.web>` 标记下直接添加以下内容： 

    [!code-xml[Main](profiles-themes-and-web-parts/samples/sample18.xml)]
19. 保存 web.config 文件。 现在，浏览 default.aspx 页。 它应显示应用主题。
20. 如果它尚未打开，则在 Visual Studio 中打开 "default.aspx" 页。
21. 选择该按钮。
22. 将**SkinID**属性更改为 goButton。 请注意，Visual Studio 会提供一个下拉列表，其中包含一个按钮控件的有效 SkinID 值。
23. 保存页。 现在，请在浏览器中再次预览页面。 此时，该按钮应显示 "跳过"，并且应以更宽的外观显示。

使用**SkinID**属性，您可以轻松地为特定类型的服务器控件的不同实例配置不同的外观。

## <a name="the-stylesheettheme-property"></a>StyleSheetTheme 属性

到目前为止，我们仅讨论了如何使用主题属性应用主题。 使用主题属性时，外观文件将重写服务器控件的任何声明性设置。 例如，在练习1中，为按钮控件指定了 "goButton" 的 SkinID，并已将该按钮的文本更改为 "开始"。 您可能已注意到，设计器中的按钮的 Text 属性设置为 "Button"，而主题 u.i。 主题将始终重写设计器中的所有属性设置。

如果希望能够使用设计器中指定的属性覆盖主题外观文件中定义的属性，可以使用**StyleSheetTheme**属性，而不是主题属性。 StyleSheetTheme 属性与主题属性相同，不同之处在于，它不会重写所有显式属性设置，如主题属性所示。

若要查看此操作，请打开练习1中项目的 web.config 文件，并将 `<pages>` 元素更改为以下内容：

[!code-xml[Main](profiles-themes-and-web-parts/samples/sample19.xml)]

现在，浏览 default.aspx 页，您会看到 Button 控件再次具有一个 "按钮" 的文本属性。 这是因为设计器中的显式属性设置是重写 goButton SkinID 设置的 Text 属性。

## <a name="overriding-themes"></a>重写主题

全局主题可以通过应用程序\_Themes 文件夹中的同名应用程序来进行重写。 但是，主题不会应用于真正的替代方案。 如果运行时在应用中遇到主题文件\_Themes 文件夹，将使用这些文件应用主题，并将忽略全局主题。

StyleSheetTheme 属性是可重写的，可在代码中重写，如下所示：

[!code-csharp[Main](profiles-themes-and-web-parts/samples/sample20.cs)]

## <a name="web-parts"></a>Web 部件

ASP.NET Web 部件是一组集成控件，用于创建网站使最终用户可以直接从浏览器修改网页的内容、外观和行为。 修改可以应用于网站上的所有用户，也可以应用于单个用户。 当用户修改页面和控件时，可以保存设置，以便在将来的浏览器会话中保留用户的个人首选项，该功能称为个性化。 这些 Web 部件功能意味着开发人员可以让最终用户动态地个性化 Web 应用程序，而无需开发人员或管理员干预。

使用 Web 部件控件集，作为开发人员，你可以让最终用户：

- 个性化页面内容。 用户可以将新的 Web 部件控件添加到页面、删除它们、隐藏它们，或将其最小化为普通的窗口。
- 个性化页面布局。 用户可以将 Web 部件控件拖动到页面上的不同区域，或更改其外观、属性和行为。
- 导出和导入控件。 用户可以导入或导出 Web 部件控件设置，以便在其他页面或站点中使用，同时保留属性、外观，甚至控件中的数据。 这会减少最终用户的数据输入和配置要求。
- 创建连接。 用户可以在控件之间建立连接，例如，图表控件可以在股票行情滚动插件控件中显示数据图。 用户不仅可以自定义连接本身，而且还可以自定义图表控件显示数据的外观和详细信息。
- 管理并个性化站点级别设置。 授权用户可以配置站点级设置、确定谁可以访问站点或页面、设置对控件的基于角色的访问等。 例如，管理角色中的用户可以将 Web 部件控件设置为由所有用户共享，并阻止非管理员用户对共享控件进行个性化设置。

通常可以通过以下三种方式之一来处理 Web 部件：创建使用 Web 部件控件的页面、创建单个 Web 部件控件或创建完整的可个性化 Web 应用程序，例如门户。

## <a name="page-development"></a>页面开发

页面开发人员可以使用可视化设计工具（如 Microsoft Visual Studio 2005）创建使用 Web 部件的页面。 使用 Visual Studio 之类的工具的一个优点是，Web 部件控件集提供了一些功能，用于在可视化设计器中对 Web 部件控件进行拖放创建和配置。 例如，您可以使用设计器将 Web 部件区域或 Web 部件编辑器控件拖到设计图面上，然后使用 Web 部件控件集提供的 UI 在设计器中配置该控件。 这可以加快 Web 部件应用程序的开发，减少需要编写的代码量。

## <a name="control-development"></a>控件开发

您可以使用任何现有的 ASP.NET 控件作为 Web 部件控件，包括标准 Web 服务器控件、自定义服务器控件和用户控件。 若要以编程方式对您的环境进行最大的编程控制，您还可以创建从 WebPart 类派生的自定义 Web 部件控件。 对于单个 Web 部件控件开发，通常会创建一个用户控件，并将其用作 Web 部件控件，或开发自定义 Web 部件控件。

作为开发自定义 Web 部件控件的一个示例，你可以创建一个控件来提供其他 ASP.NET 服务器控件提供的任何功能，这些功能对于打包为可个性化的 Web 部件控件可能会很有用：日历、列表、财务信息、新闻、计算器、用于更新内容的丰富文本控件、连接到数据库的可编辑网格、动态更新其显示的图表，或天气和旅行信息。 如果你为控件提供了一个可视化设计器，则使用 Visual Studio 的任何页开发人员只需将控件拖到 Web 部件区域并在设计时进行配置，而无需编写其他代码。

个性化设置是 Web 部件功能的基础。 它使用户能够修改（或个性化）页面上 Web 部件控件的布局、外观和行为。 个性化设置的生存期很长：在当前浏览器会话（与视图状态相同）的过程中，也不会保留这些设置，但在长期存储中，还会保存用户的设置以供将来浏览器会话使用。 默认情况下，为 Web 部件页启用了个性化设置。

UI 结构组件依赖于个性化，并提供所有 Web 部件控件所需的核心结构和服务。 每个 Web 部件页上所需的一个 UI 结构组件是 WebPartManager 控件。 尽管从不可见，但此控件具有协调页面上所有 Web 部件控件的关键任务。 例如，它将跟踪所有单个 Web 部件控件。 它管理 Web 部件区域（包含页上 Web 部件控件的区域）以及哪些控件在哪些区域中。 它还可以跟踪和控制页可以使用的不同显示模式，如 "浏览"、"连接"、"编辑" 或 "目录" 模式，以及个性化设置更改是应用于所有用户还是应用于单个用户。 最后，它会启动并跟踪 Web 部件控件之间的连接和通信。

第二类 UI 结构组件是区域。 区域作为 Web 部件页上的布局管理器。 它们包含和组织从 Part 类（部件控件）派生的控件，并提供以水平或垂直方向执行模块化页面布局的功能。 区域还为其所包含的每个控件提供通用和一致的 UI 元素（如页眉和页脚样式、标题、边框样式、操作按钮等）;这些公共元素称为控件的 chrome。 在不同的显示模式下使用几种专用类型的区域，并使用各种控件。 下面的 "Web 部件基本控制" 部分介绍了不同类型的区域。

Web 部件的 UI 控件，它们都派生自**Part**类，它们构成了 Web 部件页上的主 UI。 Web 部件控件集在提供用于创建部件控件的选项中是灵活的和包含的。 除了创建自己的自定义 Web 部件控件外，还可以使用现有的 ASP.NET 服务器控件、用户控件或自定义服务器控件作为 Web 部件控件。 下一节将介绍最常用于创建 Web 部件页的基本控件。

## <a name="web-parts-essential-controls"></a>Web 部件基本控件

Web 部件控制集很大，但某些控件是必需的，因为它们是运行 Web 部件所必需的，也可能是因为它们是 Web 部件页上最常使用的控件。 开始使用 Web 部件和创建基本 Web 部件页面时，熟悉下表中所述的基本 Web 部件控件是非常有帮助的。

| **Web 部件控件** | **描述** |
| --- | --- |
| WebPartManager | 管理页上的所有 Web 部件控件。 每个 Web 部件页都需要一个（且仅有一个） **WebPartManager**控件。 |
| CatalogZone | 包含 CatalogPart 控件。 使用此区域可创建 Web 部件控件的目录，用户可以从中选择要添加到页面的控件。 |
| EditorZone | 包含 EditorPart 控件。 使用此区域可使用户能够在页面上编辑和个性化 Web 部件控件。 |
| WebPartZone | 包含，并为构成页面的主 UI 的 WebPart 控件提供整体布局。 无论何时使用 Web 部件控件创建页面，都应使用此区域。 页面可以包含一个或多个区域。 |
| ConnectionsZone | 包含 System.web.ui.webcontrols.webparts.webpartconnection 控件，并提供用于管理连接的 UI。 |
| WebPart （GenericWebPart） | 呈现主 UI;大多数 Web 部件 UI 控件都属于此类别。 若要实现最大的编程控制，可以创建从基本**Web 部件**控件派生的自定义 Web 部件控件。 您还可以将现有服务器控件、用户控件或自定义控件用作 Web 部件控件。 无论何时将这些控件中的任何一个放到区域中， **WebPartManager**控件都将在运行时自动将其与**GenericWebPart**控件包装，以便可以将它们用于 Web 部件功能。 |
| CatalogPart | 包含用户可添加到页面的可用 Web 部件控件的列表。 |
| WebPartConnection | 在页上的两个 Web 部件控件之间创建连接。 该连接将其中一个 Web 部件控件定义为提供程序（数据），另一个作为使用者。 |
| EditorPart | 用作专用编辑器控件的基类。 |
| EditorPart 控件（AppearanceEditorPart、LayoutEditorPart、BehaviorEditorPart 和 PropertyGridEditorPart） | 允许用户个性化页面上 Web 部件 UI 控件的各个方面 |

## <a name="lab-create-a-web-part-page"></a>Lab：创建 Web 部件页

在此实验室中，您将创建一个 Web 部件页，该页将通过 ASP.NET 配置文件持久保存信息。

### <a name="creating-a-simple-page-with-web-parts"></a>使用 Web 部件创建简单页面

在本演练的此部分中，你将创建一个使用 Web 部件控件来显示静态内容的页面。 使用 Web 部件的第一步是创建包含两个所需结构元素的页面。 首先，Web 部件页需要使用 WebPartManager 控件来跟踪和协调所有 Web 部件控件。 其次，Web 部件页面需要一个或多个区域，这些区域是包含 WebPart 或其他服务器控件并占用页面的指定区域的复合控件。

> [!NOTE]
> 无需执行任何操作即可启用 Web 部件个性化;默认情况下，将为 Web 部件控件集启用此功能。 首次在站点上运行 Web 部件页面时，ASP.NET 将设置默认个性化设置提供程序以存储用户个性化设置。 有关个性化的详细信息，请参阅 Web 部件个性化概述。

### <a name="to-create-a-page-for-containing-web-parts-controls"></a>创建包含 Web 部件控件的页

1. 关闭默认页面，并将新页面添加到名为 WebPartsDemo 的站点。
2. 切换到 "**设计**" 视图。
3. 从 "**视图**" 菜单上，确保已选中 "**非可视控件**和**详细信息**" 选项，以便您可以查看没有 UI 的布局标记和控件。
4. 将插入点放在设计图面上 `<div>` 标记之前，并按 ENTER 添加新行。 将插入点放置在新行字符之前，单击菜单上的 "**块格式**" 下拉列表控件，然后选择 "**标题 1** " 选项。 在标题中，添加文本**Web 部件演示 "页**。
5. 从 "工具箱" 的 " **Web 部件**" 选项卡中，将 " **WebPartManager** " 控件拖动到页面上，将其放置在新行字符之后、`<div>`标记之前。   
  
   **WebPartManager**控件不呈现任何输出，因此它在设计器图面上显示为灰色框。
6. 将插入点置于 `<div>` 标记中。
7. 在 "**布局**" 菜单中，单击 "**插入表**"，然后创建一个包含一行和三列的新表。 单击 "**单元格属性**" 按钮，从 "**垂直对齐**" 下拉列表中选择 "**顶部**"，单击 **"确定**"，然后再次单击 **"确定"** 以创建表。
8. 将 WebPartZone 控件拖到左表列中。 右键单击 " **WebPartZone** " 控件，选择 "**属性**"，然后设置以下属性：   
  
   ID： SidebarZone   
  
   HeaderText：边栏
9. 将第二个**WebPartZone**控件拖到中间表中，并设置以下属性：   
  
   ID： MainZone   
  
   HeaderText： Main
10. 保存该文件。

页面现在具有两个不同的区域，您可以单独控制它们。 但是，这两个区域都不包含任何内容，因此，下一步是创建内容。 对于本演练，你将使用只显示静态内容 Web 部件控件。

Web 部件区域的布局由 &lt;方法是&gt; 元素指定。 在区域模板中，你可以添加任何 ASP.NET 控件，无论它是自定义 Web 部件控件、用户控件还是现有服务器控件。 请注意，在使用 "标签" 控件时，只需添加静态文本。 当你将常规服务器控件放在**WebPartZone**区域中时，ASP.NET 会在运行时将该控件视为 Web 部件控件，这样就可以在控件上启用 Web 部件功能。

**为主区域创建内容**

1. 在 "**设计**" 视图中，将 "**标签**" 控件从 "工具箱" 的 "**标准**" 选项卡拖到 " **ID** " 属性设置为 MainZone 的区域的 "内容" 区域。
2. 切换到 "**源**" 视图。 请注意，添加了一个 &lt;方法是&gt; 元素，用于在 MainZone 中包装**标签**控件。
3. 将名为 " **title** " 的属性添加到 &lt;asp： label&gt; 元素，并将其值设置为 "内容"。 从 &lt;asp： label&gt; 元素中删除 Text = "Label" 特性。 在 &lt;asp 的开始标记和结束标记之间：标签&gt; 元素，在一对 &lt;h2&gt; 元素标记中添加一些文本，如 **"欢迎使用我的主页**"。 你的代码应如下所示。 

    [!code-aspx[Main](profiles-themes-and-web-parts/samples/sample21.aspx)]
4. 保存该文件。

接下来，创建一个用户控件，该控件还可以作为 Web 部件控件添加到页中。

### <a name="to-create-a-user-control"></a>创建用户控件

1. 将新的 Web 用户控件添加到您的网站，以用作搜索控件。 取消选择将**源代码放在单独的文件中**的选项。 将其添加到 WebPartsDemo 页面所在的同一目录中，并将其命名为 SearchUserControl。   
  
    > [!NOTE]
    > 此演练的用户控件不实现实际搜索功能;它仅用于演示 Web 部件功能。
2. 切换到 "**设计**" 视图。 从 "工具箱" 的 "**标准**" 选项卡中，将 TextBox 控件拖到页面上。
3. 将插入点置于刚添加的文本框之后，然后按 ENTER 添加新行。
4. 将一个按钮控件拖动到刚添加的文本框下面的新行上的页上。
5. 切换到 "**源**" 视图。 确保用户控件的源代码类似于下面的示例。 

    [!code-aspx[Main](profiles-themes-and-web-parts/samples/sample22.aspx)]
6. 保存并关闭文件。

现在，你可以将 Web 部件控件添加到侧栏区域。 你要将两个控件添加到侧栏区域，一个包含链接列表，另一个是在上一过程中创建的用户控件。 链接以标准**标签**服务器控件的形式添加，类似于创建主区域的静态文本的方式。 但是，尽管用户控件中包含的单个服务器控件可以直接包含在区域中（如 "标签" 控件），但在本例中，它们不是。 相反，它们是在上一过程中创建的用户控件的一部分。 这说明了将用户控件中所需的任何控件和额外功能打包，然后将区域中的控件作为 Web 部件控件引用的常用方法。

在运行时，Web 部件控件集用 GenericWebPart 控件包装两个控件。 当**GenericWebPart**控件包装 Web 服务器控件时，通用部件控件是父控件，你可以通过父控件的 ChildControl 属性访问服务器控件。 使用泛型部件控件时，标准 Web 服务器控件可以与派生自**WebPart**类 Web 部件控件具有相同的基本行为和特性。

### <a name="to-add-web-parts-controls-to-the-sidebar-zone"></a>向侧栏区域添加 Web 部件控件

1. 打开 WebPartsDemo 页。
2. 切换到 "**设计**" 视图。
3. 将创建的用户控件页 SearchUserControl 从**解决方案资源管理器**拖动到其**ID**属性设置为 SidebarZone 的区域，并将其放在此处。
4. 保存 WebPartsDemo 页。
5. 切换到 "**源**" 视图。
6. 在 SidebarZone 的 &lt;asp： webpartzone&gt; 元素中，就在对用户控件的引用的上方，添加一个 &lt;asp： label&gt; 包含链接的元素，如下面的示例中所示。 此外，将 "**标题**" 属性添加到 "用户控件" 标记，值为 "**搜索**"，如下所示。 

    [!code-aspx[Main](profiles-themes-and-web-parts/samples/sample23.aspx)]
7. 保存并关闭文件。

现在，可以通过在浏览器中浏览到页面来对其进行测试。 该页显示两个区域。 以下屏幕截图显示该页。

**包含两个区域的 Web 部件演示页面**

![Web 部件 VS 演练1屏幕截图](profiles-themes-and-web-parts/_static/image3.gif)

**图 3**： Web 部件 VS 演练1屏幕截图

在每个控件的标题栏中是向下箭头，它提供对可对控件执行的可用操作的谓词菜单的访问。 单击其中一个控件的谓词菜单，然后单击**最小化**谓词，并注意该控件已最小化。 从谓词菜单中，单击 "还原"，控件将**恢复**为其正常大小。

### <a name="enabling-users-to-edit-pages-and-change-layout"></a>使用户能够编辑页面和更改布局

Web 部件提供了一项功能，使用户可以通过将 Web 部件控件的布局从一个区域拖动到另一个区域来更改它们的布局。 除了允许用户将**Web 部件**控件从一个区域移到另一个区域，你还可以允许用户编辑控件的各种特征，包括其外观、布局和行为。 Web 部件控件集提供**WebPart**控件的基本编辑功能。 尽管在本演练中你不会这样做，但你也可以创建自定义编辑器控件，使用户能够编辑**Web 部件**控件的功能。 与更改**Web 部件**控件的位置一样，编辑控件的属性依赖于 ASP.NET 个性化设置来保存用户所做的更改。

在本演练的此部分中，你将添加功能，以便用户能够编辑页面上任何**Web 部件**控件的基本特征。 若要启用这些功能，请向页面中添加另一个自定义用户控件，以及 &lt;asp： editorzone&gt; 元素和两个编辑控件。

### <a name="to-create-a-user-control-that-enables-changing-page-layout"></a>创建启用更改页面布局的用户控件

1. 在 Visual Studio 中的 "**文件**" 菜单上，选择 "**新建**" 子菜单，然后单击 "**文件**" 选项。
2. 在 "**添加新项**" 对话框中，选择 " **Web 用户控件**"。 将新文件命名为 DisplayModeMenu。 取消选择将**源代码放在单独的文件中**的选项。
3. 单击 "添加" 以创建新控件。
4. 切换到 "**源**" 视图。
5. 删除新文件中的所有现有代码，并粘贴以下代码。 此用户控件代码使用 Web 部件控件集的功能，该控件集使页面可以更改其视图或显示模式，还可以在处于某些显示模式下时更改页面的物理外观和布局。 

    [!code-aspx[Main](profiles-themes-and-web-parts/samples/sample24.aspx)]
6. 单击工具栏上的 "保存" 图标，或在 "**文件**" 菜单上选择 "**保存**"，保存该文件。

### <a name="to-enable-users-to-change-the-layout"></a>使用户能够更改布局

1. 打开 "WebPartsDemo" 页，并切换到 "**设计**" 视图。
2. 将插入点放置在 "**设计**" 视图中，就在前面添加的**WebPartManager**控件之后。 在文本后面添加一个硬回车，使**WebPartManager**控件后有一个空白行。 将插入点放置在空行上。
3. 将刚刚创建的用户控件（该文件命名为 DisplayModeMenu）放入 WebPartsDemo 页面，并将其放在空行上。
4. 将 EditorZone 控件从 "工具箱" 的 " **webpart** " 部分拖到 "WebPartsDemo" 页中的其余打开的表单元。
5. 从工具箱的**webpart**部分，将 AppearanceEditorPart 控件和 LayoutEditorPart 控件拖到**EditorZone**控件中。
6. 切换到 "**源**" 视图。 表单元中生成的代码应类似于以下代码。 

    [!code-aspx[Main](profiles-themes-and-web-parts/samples/sample25.aspx)]
7. 保存 WebPartsDemo 文件。 您已经创建了一个用户控件，该控件允许您更改显示模式和更改页面布局，并且您在主网页上引用了该控件。

你现在可以测试编辑页面和更改布局的功能。

### <a name="to-test-layout-changes"></a>测试布局更改

1. 在浏览器中加载页面。
2. 单击 "**显示模式**" 下拉菜单，然后选择 "**编辑**"。 显示区域标题。
3. 将 "**我的链接**" 控件从侧栏区域拖到主区域的底部。 页面应类似于以下屏幕截图。

### <a name="web-parts-demo-page-with-my-links-control-moved"></a>已移动 "我的链接" 控件 Web 部件演示页

![Web 部件 VS 演练2屏幕截图](profiles-themes-and-web-parts/_static/image4.gif)

**图 4**： Web 部件 VS 演练2屏幕截图

1. 单击 "**显示模式**" 下拉菜单，然后选择 "**浏览**"。 页面会刷新，区域名称消失，"**我的链接**" 控件仍保留在你的位置。
2. 若要演示个性化设置工作，请关闭浏览器，然后重新加载页面。 您所做的更改将保存起来以便将来浏览器会话。
3. 从 "**显示模式**" 菜单中选择 "**编辑**"。   
  
   页面上的每个控件现在都显示在其标题栏中，其中包含谓词下拉菜单。
4. 单击箭头以显示 "**我的链接**" 控件上的谓词菜单。 单击 "**编辑**" 谓词。   
  
   此时将显示**EditorZone**控件，其中显示了所添加的 EditorPart 控件。
5. 在编辑控件的 "**外观**" 部分，将 "**标题**" 更改为 "我的收藏夹"，使用 " **Chrome 类型**" 下拉列表选择 "**仅标题**"，然后单击 "**应用**"。 以下屏幕截图显示处于编辑模式的页面。

### <a name="web-parts-demo-page-in-edit-mode"></a>在编辑模式下 Web 部件演示页

![Web 部件 VS 演练3屏幕截图](profiles-themes-and-web-parts/_static/image5.gif)

**图 5**： Web 部件 VS 演练3屏幕截图

1. 单击 "**显示模式**" 菜单，然后选择 "**浏览**" 以返回到 "浏览" 模式。
2. 控件现在具有更新后的标题和边框，如以下屏幕截图所示。

### <a name="edited-web-parts-demo-page"></a>编辑 Web 部件演示页

![Web 部件 VS 演练4屏幕截图](profiles-themes-and-web-parts/_static/image6.gif)

**图 4**： Web 部件 VS 演练4屏幕截图

### <a name="adding-web-parts-at-run-time"></a>在运行时添加 Web 部件

还可以允许用户在运行时向页面添加 Web 部件控件。 为此，请使用 Web 部件目录配置页面，其中包含要提供给用户的 Web 部件控件的列表。

**允许用户在运行时添加 Web 部件**

1. 打开 "WebPartsDemo" 页，并切换到 "**设计**" 视图。
2. 从 "工具箱" 的 " **Web 部件**" 选项卡中，将 CatalogZone 控件拖到 " **EditorZone** " 控件下表的右侧列中。   
  
   这两个控件可以位于同一个表单元中，因为它们不会同时显示。
3. 在 "属性" 窗格中，将 "**添加 Web 部件字符串添加**到**CatalogZone**控件的 HeaderText 属性。
4. 从 "工具箱" 的 " **webpart** " 部分，将 "DeclarativeCatalogPart" 控件拖动到 " **CatalogZone** " 控件的内容区域。
5. 单击**DeclarativeCatalogPart**控件右上角的箭头以显示其 "任务" 菜单，然后选择 "**编辑模板**"。
6. 从 "工具箱" 的 "**标准**" 部分，将 " **FileUpload** " 控件和 "**日历**" 控件拖动到**DeclarativeCatalogPart**控件的 " **WebPartsTemplate** " 部分。
7. 切换到 "**源**" 视图。 检查 &lt;asp： catalogzone&gt; 元素的源代码。 请注意， **DeclarativeCatalogPart**控件包含一个 &lt;webpartstemplate&gt; 元素，其中包含两个包含的服务器控件，您可以从目录添加到您的页面。
8. 使用以下代码示例中为每个标题显示的字符串值向添加到目录中的每个控件添加**标题**属性。 即使标题不是在设计时可以在这两个服务器控件上设置的属性，当用户在运行时将这些控件从目录添加到**WebPartZone**区域时，它们都将使用**GenericWebPart**控件进行包装。 这使它们可以充当 Web 部件控件，因此可以显示标题。   
  
   **DeclarativeCatalogPart**控件中包含的两个控件的代码应如下所示。 

    [!code-aspx[Main](profiles-themes-and-web-parts/samples/sample26.aspx)]
9. 保存页。

你现在可以测试目录。

### <a name="to-test-the-web-parts-catalog"></a>测试 Web 部件目录

1. 在浏览器中加载页面。
2. 单击 "**显示模式**" 下拉菜单，然后选择 "**目录**"。   
  
   将显示名为**Add Web 部件**的目录。
3. 将 "**我的收藏夹**" 控件从主要区域移回边栏区域的顶部，并将其放在此处。
4. 在 "**添加 Web 部件**目录" 中，选择这两个复选框，然后从包含可用区域的下拉列表中选择 " **Main** "。
5. 在目录中单击 "**添加**"。 控件将添加到主区域。 如果需要，可以将目录中的多个控件实例添加到页面中。   
  
   下面的屏幕截图显示了在主区域中具有文件上传控件和日历的页面。 

![从目录添加到主区域的控件](profiles-themes-and-web-parts/_static/image7.gif)

    **Figure 5**: Controls added to Main zone from the catalog
6. 单击 "**显示模式**" 下拉菜单，然后选择 "**浏览**"。 目录将消失，并刷新页面。
7. 关闭浏览器。 再次加载页面。 您所做的更改将保持不变。
