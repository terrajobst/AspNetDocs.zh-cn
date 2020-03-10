---
uid: mvc/overview/older-versions-1/nerddinner/build-a-model-with-business-rule-validations
title: 使用业务规则验证构建模型 |Microsoft Docs
author: microsoft
description: 步骤3显示了如何创建可用于查询和更新 NerdDinner 应用程序数据库的模型。
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 0bc191b2-4311-479a-a83a-7f1b1c32e6fe
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/build-a-model-with-business-rule-validations
msc.type: authoredcontent
ms.openlocfilehash: 6ebf1b71c089229ba9139ff7dc788b8978724046
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78435578"
---
# <a name="build-a-model-with-business-rule-validations"></a>生成具有业务规则验证功能的模型

由[Microsoft](https://github.com/microsoft)

[下载 PDF](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> 这是免费的["NerdDinner" 应用程序教程](introducing-the-nerddinner-tutorial.md)的第3步，该教程演示如何使用 ASP.NET MVC 1 构建小型但完整的 web 应用程序。
> 
> 步骤3显示了如何创建可用于查询和更新 NerdDinner 应用程序数据库的模型。
> 
> 如果你使用的是 ASP.NET MVC 3，则建议你遵循[MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)或[Mvc 音乐应用商店](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)教程中的入门。

## <a name="nerddinner-step-3-building-the-model"></a>NerdDinner 步骤3：生成模型

在模型视图-控制器框架中，术语 "模型" 是指表示应用程序数据的对象，以及与之集成验证和业务规则的相应域逻辑。 模型在很多方面都是基于 MVC 的应用程序的 "核心"，我们稍后将对其进行操作。

ASP.NET MVC 框架支持使用任何数据访问技术，开发人员可以从各种丰富的 .NET 数据选项中进行选择，以实现其模型，其中包括： LINQ to Entities、LINQ to SQL、NHibernate、LLBLGen Pro、SubSonic、WilsonORM 或只是原始 ADO。NET Datareader 或数据集。

对于我们的 NerdDinner 应用程序，我们将使用 LINQ to SQL 来创建与我们的数据库设计相当紧密的简单模型，并添加一些自定义验证逻辑和业务规则。 接下来，我们将实现一个存储库类，以帮助你从应用程序的其余部分抽象掉数据持久性实现，并使我们能够轻松地对其进行单元测试。

### <a name="linq-to-sql"></a>LINQ to SQL

LINQ to SQL 是 .NET 3.5 中附带的 ORM （对象关系映射器）。

LINQ to SQL 提供了一种简单的方法，将数据库表映射到我们可以对其进行编码的 .NET 类。 对于我们的 NerdDinner 应用程序，我们将使用它将数据库中的就和 RSVP 表映射到晚餐和 RSVP 类。 就表和 RSVP 表中的列将与晚餐和 RSVP 类的属性相对应。 每个晚餐和 RSVP 对象将代表数据库中就表或 RSVP 表中的一行。

LINQ to SQL 使我们不必手动构建 SQL 语句来检索和更新包含数据库数据的晚餐和 RSVP 对象。 相反，我们将定义晚餐和 RSVP 类，它们如何映射到数据库以及它们之间的关系。 接下来，LINQ to SQL 将负责生成合适的 SQL 执行逻辑以便在运行时使用它们。

我们可以使用 VB 中的 LINQ 语言支持， C#并编写可从数据库中检索晚餐和 RSVP 对象的可表达性查询。 这可以最大程度地减少需要编写的数据代码量，并使我们能够构建真正干净的应用程序。

### <a name="adding-linq-to-sql-classes-to-our-project"></a>向项目添加 LINQ to SQL 类

首先，右键单击项目中的 "模型" 文件夹，然后选择 "**添加-&gt;新项**" 菜单命令：

![](build-a-model-with-business-rule-validations/_static/image1.png)

这会显示 "添加新项" 对话框。 我们将按 "数据" 类别进行筛选，并选择其中的 "LINQ to SQL 类" 模板：

![](build-a-model-with-business-rule-validations/_static/image2.png)

我们会将项目命名为 "NerdDinner"，并单击 "添加" 按钮。 Visual Studio 将在我们的 \Models 目录下添加一个 NerdDinner 文件，然后打开 LINQ to SQL 对象关系设计器：

![](build-a-model-with-business-rule-validations/_static/image3.png)

### <a name="creating-data-model-classes-with-linq-to-sql"></a>创建具有 LINQ to SQL 的数据模型类

LINQ to SQL 使我们可以从现有的数据库架构中快速创建数据模型类。 为此，我们将在服务器资源管理器中打开 NerdDinner 数据库，并选择要在其中进行建模的表：

![](build-a-model-with-business-rule-validations/_static/image4.png)

然后，可以将这些表拖放到 LINQ to SQL 设计器图面上。 如果执行此操作 LINQ to SQL 将使用表的架构（带有映射到数据库表列的类属性）自动创建晚餐和 RSVP 类：

![](build-a-model-with-business-rule-validations/_static/image5.png)

默认情况下，在基于数据库架构创建类时，LINQ to SQL 设计器会自动 "为" 表和列名。 例如，上面示例中的 "就" 表导致了 "晚餐" 类。 此类命名有助于使模型与 .NET 命名约定保持一致，并且通常会发现设计器很方便地解决这一问题（尤其是在添加大量表时）。 不过，如果您不喜欢设计器生成的类或属性的名称，您始终可以重写它并将其更改为任何所需的名称。 为此，可以在设计器中编辑实体/属性名称，也可以通过属性网格修改它。

默认情况下，LINQ to SQL 设计器还会检查表的主键/外键关系，并根据它们在创建的不同模型类之间自动创建默认的 "关系关联"。 例如，将就和 RSVP 表拖放到 LINQ to SQL 设计器上时，这两个表之间的一对多关系关联是根据 RSVP 表具有就表的外键得出的，这是由设计器）：

![](build-a-model-with-business-rule-validations/_static/image6.png)

上述关联将导致 LINQ to SQL 将强类型的 "晚餐" 属性添加到 RSVP 类，开发人员可以使用该属性来访问与给定 RSVP 相关的晚餐。 它还会导致晚餐类具有一个 "RSVPs" 集合属性，使开发人员能够检索和更新与特定晚餐关联的 RSVP 对象。

在下面，你可以在 Visual Studio 中看到一个 intellisense 示例，当我们创建新的 RSVP 对象并将其添加到晚餐的 RSVPs 集合时。 请注意 LINQ to SQL 如何自动在晚餐对象上添加 "RSVPs" 集合：

![](build-a-model-with-business-rule-validations/_static/image7.png)

通过将 RSVP 对象添加到晚餐的 RSVPs 集合中，我们会告诉 LINQ to SQL 在我们的数据库中关联晚餐和 RSVP 行之间的外键关系：

![](build-a-model-with-business-rule-validations/_static/image8.png)

如果您不喜欢设计器如何建模或命名表关联，则可以重写它。 只需单击设计器中的 "关联" 箭头并通过属性网格访问其属性，即可重命名、删除或修改它。 但对于我们的 NerdDinner 应用程序，默认关联规则适用于正在生成的数据模型类，并且我们只使用默认行为。

### <a name="nerddinnerdatacontext-class"></a>NerdDinnerDataContext 类

Visual Studio 将自动创建表示使用 LINQ to SQL 设计器定义的模型和数据库关系的 .NET 类。 还为添加到解决方案中的每个 LINQ to SQL 设计器文件生成一个 LINQ to SQL DataContext 类。 由于我们将 LINQ to SQL 类项命名为 "NerdDinner"，因此创建的 DataContext 类将称为 "NerdDinnerDataContext"。 此 NerdDinnerDataContext 类是我们将与数据库进行交互的主要方式。

我们的 NerdDinnerDataContext 类公开了两个属性-"就" 和 "RSVPs"-表示在数据库中建模的两个表。 我们可以使用C#编写针对这些属性的 LINQ 查询，以便从数据库中查询和检索晚餐和 RSVP 对象。

下面的代码演示如何实例化 NerdDinnerDataContext 对象，并对其执行 LINQ 查询以获取将来发生的就序列。 在编写 LINQ 查询时，Visual Studio 提供完整的 intellisense，从它返回的对象是强类型化的，并且还支持 intellisense：

![](build-a-model-with-business-rule-validations/_static/image9.png)

除了允许我们查询晚餐和 RSVP 对象外，NerdDinnerDataContext 还会自动跟踪我们通过它检索到的晚餐和 RSVP 对象所做的任何更改。 使用此功能可以轻松地将更改保存回数据库-无需编写任何显式的 SQL 更新代码。

例如，下面的代码演示了如何使用 LINQ 查询从数据库检索单个晚餐对象，更新两个晚餐属性，然后将更改保存回数据库：

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample1.cs)]

上面代码中的 NerdDinnerDataContext 对象自动跟踪对其检索到的晚餐对象所做的属性更改。 当我们调用了 "SubmitChanges （）" 方法时，它会对数据库执行适当的 SQL "UPDATE" 语句，以将更新后的值保留回去。

### <a name="creating-a-dinnerrepository-class"></a>创建 DinnerRepository 类

对于小型应用程序，有时可以让控制器直接处理 LINQ to SQL DataContext 类，并在控制器中嵌入 LINQ 查询。 然而，随着应用程序变得更大，维护和测试此方法会变得很繁琐。 它还会导致我们在多个位置复制相同的 LINQ 查询。

可以使应用程序更易于维护和测试的一种方法是使用 "存储库" 模式。 存储库类有助于封装数据查询和持久性逻辑，并从应用程序中提取数据持久性的实现细节。 除了使应用程序代码更整洁，使用存储库模式还可以更轻松地在将来更改数据存储实现，并且它有助于简化应用程序的单元测试，而无需实际数据库。

对于我们的 NerdDinner 应用程序，我们将使用以下签名定义一个 DinnerRepository 类：

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample2.cs)]

*注意：本章稍后将从此类中提取 IDinnerRepository 接口，并在控制器上启用依赖项注入。不过，从开始，我们将简单直接使用 DinnerRepository 类。*

若要实现此类，请右键单击 "模型" 文件夹，然后选择 "**添加-&gt;新项**" 菜单命令。 在 "添加新项" 对话框中，选择 "类" 模板，并将文件命名为 "DinnerRepository.cs"：

![](build-a-model-with-business-rule-validations/_static/image10.png)

然后，可以使用以下代码实现 DinnerRepository 类：

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample3.cs)]

### <a name="retrieving-updating-inserting-and-deleting-using-the-dinnerrepository-class"></a>使用 DinnerRepository 类检索、更新、插入和删除

现在，我们已经创建了 DinnerRepository 类，接下来让我们看看一些代码示例，这些示例演示了我们可以使用它完成的常见任务：

#### <a name="querying-examples"></a>查询示例

以下代码使用 DinnerID 值检索单个晚宴：

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample4.cs)]

下面的代码检索所有即将发布的就和循环：

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample5.cs)]

#### <a name="insert-and-update-examples"></a>插入和更新示例

下面的代码演示如何添加两个新的就。 在对存储库进行添加/修改之前，不会将其添加到数据库中。 LINQ to SQL 自动包装数据库事务中的所有更改-因此，在存储库保存时，所有更改都将发生，或者都不执行更改：

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample6.cs)]

下面的代码检索现有晚餐对象，并修改其中的两个属性。 在我们的存储库中调用 "Save （）" 方法时，会将更改提交回数据库：

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample7.cs)]

下面的代码检索晚餐，然后向其添加 RSVP。 它使用 LINQ to SQL 为我们创建的晚餐对象上的 RSVPs 集合来完成此工作（因为数据库中的两者之间存在主键/外键关系）。 当在存储库中调用 "Save （）" 方法时，此更改将作为新的 RSVP 表行保留回数据库：

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample8.cs)]

#### <a name="delete-example"></a>删除示例

下面的代码检索现有晚餐对象，然后将其标记为已删除。 在存储库中调用 "Save （）" 方法时，它会将删除提交回数据库：

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample9.cs)]

### <a name="integrating-validation-and-business-rule-logic-with-model-classes"></a>将验证和业务规则逻辑与模型类集成

集成验证和业务规则逻辑是适用于数据的任何应用程序的关键部分。

#### <a name="schema-validation"></a>架构验证

当使用 LINQ to SQL 设计器定义模型类时，数据模型类中的属性的数据类型对应于数据库表的数据类型。 例如：如果就表中的 "EventDate" 列是 "datetime"，则 LINQ to SQL 创建的数据模型类将是 "DateTime" 类型（这是一种内置的 .NET 数据类型）。 这意味着，如果您尝试从代码向代码分配一个整数或布尔值，将会出现编译错误，如果在运行时尝试将无效字符串类型隐式转换为它，则会自动引发错误。

使用字符串时，LINQ to SQL 还将自动为你处理转义 SQL 值，这有助于在使用它时防止出现 SQL 注入式攻击。

#### <a name="validation-and-business-rule-logic"></a>验证和业务规则逻辑

架构验证在第一步中非常有用，但这很少。 大多数现实情况下，都需要能够指定更丰富的验证逻辑，该逻辑可跨多个属性、执行代码，并经常识别模型的状态（例如：是在/updated/deleted 中创建，还是在特定于域的状态，如 "已存档"）。 有多种不同的模式和框架可用于定义模型类并将其应用于模型类，并且有多个基于 .NET 的框架可用于帮助解决此问题。 在 ASP.NET MVC 应用程序中，可以使用它们中的任何一个。

为了实现 NerdDinner 应用程序的目的，我们将使用一个相对简单的直连模式，在此模式下，我们将在晚餐模型对象上公开 IsValid 属性和 GetRuleViolations （）方法。 IsValid 属性将返回 true 或 false，具体取决于验证和业务规则是否都有效。 GetRuleViolations （）方法将返回任何规则错误的列表。

我们将通过向项目中添加 "partial 类"，为晚餐模型实现 IsValid 和 GetRuleViolations （）。 分部类可用于将方法/属性/事件添加到 VS 设计器所维护的类（例如，由 LINQ to SQL 设计器生成的晚餐类），并有助于避免使用我们的代码以免混乱该工具。 可以通过右键单击 \Models 文件夹，然后选择 "添加新项" 菜单命令向项目中添加一个新的分部类。 然后，可以在 "添加新项" 对话框中选择 "类" 模板，并将其命名为 Dinner.cs。

![](build-a-model-with-business-rule-validations/_static/image11.png)

单击 "添加" 按钮会将 Dinner.cs 文件添加到项目中，并在 IDE 中打开它。 然后，可以使用以下代码实现基本规则/验证强制框架：

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample10.cs)]

有关上述代码的几点说明：

- 晚餐类以 "partial" 关键字开头-这意味着，其中包含的代码将与 LINQ to SQL 设计器生成/维护并编译为单一类的类结合使用。
- RuleViolation 类是一个帮助器类，它将添加到项目中，以允许我们提供有关规则冲突的更多详细信息。
- GetRuleViolations （）方法会导致对验证和业务规则进行评估（我们将很快实现这些规则）。 然后返回一系列 RuleViolation 对象，这些对象提供有关任何规则错误的更多详细信息。
- "晚餐" 属性提供了一个方便的帮助程序属性，该属性指示晚餐对象是否具有任何活动的 RuleViolations。 开发人员可随时使用晚餐对象进行主动检查（不会引发异常）。
- OnValidate （）分部方法是 LINQ to SQL 提供的挂钩，使我们能够在该数据库中保留晚餐对象时收到通知。 上述 OnValidate （）实现可确保晚餐在保存前没有 RuleViolations。 如果它处于无效状态，则会引发异常，这将导致 LINQ to SQL 中止该事务。

此方法提供了一个简单的框架，可将验证和业务规则集成到其中。 现在，让我们将以下规则添加到 GetRuleViolations （）方法：

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample11.cs)]

我们使用的C# "yield return" 功能返回任何 RuleViolations 的序列。 以上六个规则检查只是强制执行晚餐上的字符串属性，不能为 null 或空。 最后一个规则比较有趣，并调用 IsValidNumber （） helper 方法，我们可以将其添加到项目中，以验证 ContactPhone 数字格式是否与晚餐的国家/地区匹配。

我们可以使用。为实现此电话验证支持，网络的正则表达式支持。 下面是一个简单的 PhoneValidator 实现，我们可以将其添加到项目中，使我们能够添加特定于国家的 Regex 模式检查：

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample12.cs)]

#### <a name="handling-validation-and-business-logic-violations"></a>处理验证和业务逻辑冲突

现在，我们已添加了上述验证和业务规则代码，因此，只要我们尝试创建或更新晚餐，就会评估并强制实施验证逻辑规则。

开发人员可以编写如下代码来主动确定晚餐对象是否有效，并检索其中所有违规的列表而不引发任何异常：

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample13.cs)]

如果尝试保存的晚餐处于无效状态，则当我们对 DinnerRepository 调用 Save （）方法时，将引发异常。 之所以发生这种情况，是因为 LINQ to SQL 会在保存晚餐的更改之前自动调用 OnValidate （）分部方法，并且我们将代码添加到 OnValidate （）以在晚餐中存在任何规则冲突时引发异常。 我们可以捕获此异常，并被动检索要修复的冲突列表：

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample14.cs)]

由于我们的验证和业务规则是在模型层中实现的，而不是在 UI 层内实现的，因此它们将在应用程序的所有方案中应用和使用。 稍后我们可以更改或添加业务规则，并让所有与晚餐对象结合使用的代码遵守这些规则。

可以灵活地在一个位置更改业务规则，而无需在整个应用程序和 UI 逻辑中使用这些更改，这是一个编写完善的应用程序的符号，而 MVC 框架可帮助鼓励您这样做。

### <a name="next-step"></a>下一步

现在，我们提供了一个可用于查询和更新数据库的模型。

现在，让我们向项目添加一些控制器和视图，我们可以使用它们来构建 HTML UI 体验。

> [!div class="step-by-step"]
> [上一页](create-a-database.md)
> [下一页](use-controllers-and-views-to-implement-a-listingdetails-ui.md)
