---
uid: mvc/overview/older-versions-1/contact-manager/iteration-6-use-test-driven-development-vb
title: '迭代 #6 –使用测试驱动开发（VB） |Microsoft Docs'
author: microsoft
description: 在第六次迭代中，我们通过首先编写单元测试并针对单元测试编写代码，向应用程序添加新功能。 在此迭代中,。
ms.author: riande
ms.date: 02/20/2009
ms.assetid: e1fd226f-3f8e-4575-a179-5c75b240333d
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-6-use-test-driven-development-vb
msc.type: authoredcontent
ms.openlocfilehash: b166a1c6af29206d43558fa7de447c3f4da2ddfe
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78492698"
---
# <a name="iteration-6--use-test-driven-development-vb"></a>迭代 #6 –使用测试驱动开发（VB）

由[Microsoft](https://github.com/microsoft)

[下载代码](iteration-6-use-test-driven-development-vb/_static/contactmanager_6_vb1.zip)

> 在第六次迭代中，我们通过首先编写单元测试并针对单元测试编写代码，向应用程序添加新功能。 在此迭代中，我们添加联系人组。

## <a name="building-a-contact-management-aspnet-mvc-application-vb"></a>构建联系人管理 ASP.NET MVC 应用程序（VB）

在本系列教程中，我们从一开始就生成一个完整的联系人管理应用程序。 联系人管理器应用程序允许您存储联系人信息名称、电话号码和电子邮件地址，以获取人员列表。

我们通过多个迭代生成应用程序。 随着每次迭代，我们将逐步改进应用程序。 此多个迭代方法的目标是使您能够了解每个更改的原因。

- 迭代 #1-创建应用程序。 在第一次迭代中，我们以尽可能简单的方式创建联系人管理器。 添加对基本数据库操作的支持：创建、读取、更新和删除（CRUD）。

- 迭代 #2-使应用程序看起来不错。 在此迭代中，我们通过修改默认的 ASP.NET MVC 视图母版页和级联样式表来改善应用程序的外观。

- 迭代 #3-添加窗体验证。 在第三次迭代中，我们将添加基本的窗体验证。 我们阻止用户提交窗体，而无需填写所需的窗体字段。 我们还验证了电子邮件地址和电话号码。

- 迭代 #4-使应用程序松散耦合。 在第四次迭代中，我们将利用多种软件设计模式来更轻松地维护和修改联系人管理器应用程序。 例如，我们重构应用程序以使用存储库模式和依赖关系注入模式。

- 迭代 #5-创建单元测试。 在第五次迭代中，通过添加单元测试使应用程序更易于维护和修改。 我们模拟数据模型类，并为控制器和验证逻辑生成单元测试。

- 迭代 #6-使用测试驱动开发。 在第六次迭代中，我们通过首先编写单元测试并针对单元测试编写代码，向应用程序添加新功能。 在此迭代中，我们添加联系人组。

- 迭代 #7-添加 Ajax 功能。 在第七次迭代中，我们通过添加对 Ajax 的支持来提高应用程序的响应能力和性能。

## <a name="this-iteration"></a>此迭代

在联系人管理器应用程序的前一次迭代中，我们创建了单元测试，以便为代码提供安全网络。 创建单元测试的动机是使代码更具弹性性以进行更改。 使用单元测试后，我们可以对代码进行更改，并立即了解我们是否有损坏的现有功能。

在此迭代中，我们使用单元测试来实现完全不同的目的。 在此迭代中，我们将单元测试用作称为 "*测试驱动开发*" 的应用程序设计理念的一部分。 练习驱动开发时，先编写测试，然后针对测试编写代码。

更准确地说，在完成测试驱动开发时，创建代码时，需要完成三个步骤（红色/绿色/重构）：

1. 编写失败的单元测试（红色）
2. 编写通过单元测试的代码（绿色）
3. 重构你的代码（重构）

首先，编写单元测试。 单元测试应表示你希望你的代码的行为方式。 首次创建单元测试时，单元测试应失败。 测试应失败，因为尚未编写任何满足测试的应用程序代码。

接下来，编写足够的代码，使单元测试通过。 目标是以 laziest、sloppiest 和最快的方式编写代码。 您不应浪费时间思考您的应用程序的体系结构。 相反，应重点编写满足单元测试所需目的所需的最少量代码。

最后，在编写足够的代码后，你可以返回并考虑应用程序的总体体系结构。 在此步骤中，您将通过利用软件设计模式（例如存储库模式）重写（重构）您的代码，以便您的代码更易于维护。 你可以 fearlessly 在此步骤中重写代码，因为你的代码已被单元测试覆盖。

通过测试驱动开发，有很多好处。 首先，由测试驱动的开发强制您关注实际需要编写的代码。 由于你一直致力于编写足够的代码来传递特定测试，因此会阻止你 wandering 到黄龙，并编写大量不会使用的代码。

其次，"测试优先" 设计方法会强制您编写代码，从代码的使用角度来看。 换句话说，当练习驱动开发时，会不断地从用户角度编写测试。 因此，测试驱动的开发会导致更清晰且更易于理解的 Api。

最后，测试驱动的开发将强制你编写单元测试，作为编写应用程序的正常过程的一部分。 作为项目截止时间方法，测试通常是第一次进入窗口。 另一方面，在进行测试驱动开发时，更有可能良性编写单元测试，因为测试驱动的开发会使单元测试成为构建应用程序的过程的核心。

> [!NOTE] 
> 
> 若要了解有关测试驱动开发的详细信息，建议阅读 Michael Feathers 书籍，**并有效地使用旧代码**。

在此迭代中，我们将向联系人管理器应用程序添加新功能。 我们添加了对联系人组的支持。 您可以使用 "联系人组" 将您的联系人组织成不同的类别，例如业务和朋友组。

我们将按照测试驱动的开发过程将此新功能添加到我们的应用程序。 我们将首先编写单元测试，我们将针对这些测试编写所有代码。

## <a name="what-gets-tested"></a>测试的内容

如前面的迭代中所述，通常不为数据访问逻辑或查看逻辑编写单元测试。 你不为数据访问逻辑编写单元测试，因为访问数据库是相对较慢的操作。 你没有为视图逻辑编写单元测试，因为访问视图需要旋转 web 服务器，这是一个相对较慢的操作。 您不应编写单元测试，除非该测试可以在同一速度的情况上反复执行

由于测试驱动的开发由单元测试驱动，因此我们最初重点介绍如何编写控制器和业务逻辑。 我们避免对数据库或视图进行触摸。 在本教程的最后结束之前，我们不会修改数据库或创建视图。 我们从可测试的内容开始。

## <a name="creating-user-stories"></a>创建用户情景

在练习驱动开发时，您始终可以编写测试。 这会立即提出问题：如何确定要首先编写哪些测试？ 若要回答此问题，应编写一组[*用户情景*](http://en.wikipedia.org/wiki/User_stories)。

用户情景是软件要求的一种非常简短的（通常是一句）说明。 它应该是从用户角度编写的要求的非技术说明。

下面是描述新联系人组功能所需功能的一组用户情景：

1. 用户可以查看联系人组的列表。
2. 用户可以创建新的联系人组。
3. 用户可以删除现有的联系人组。
4. 创建新联系人时，用户可以选择联系人组。
5. 编辑现有联系人时，用户可以选择联系人组。
6. 联系人组的列表显示在 "索引" 视图中。
7. 当用户单击某个联系人组时，将显示匹配联系人的列表。

请注意，用户情景列表完全可由客户理解。 没有提到技术实现细节。

在构建应用程序的过程中，用户情景集可能会变得更加完善。 您可以将用户情景划分为多个情景（要求）。 例如，你可能会决定创建新的联系人组应涉及验证。 提交不带名称的联系人组应返回验证错误。

创建用户情景列表后，就可以编写第一个单元测试了。 首先，我们将创建一个单元测试，用于查看联系人组的列表。

## <a name="listing-contact-groups"></a>列出联系人组

第一个用户情景是，用户应该能够查看联系人组的列表。 我们需要通过测试来表达这一故事。

通过在 ContactManager 项目中右键单击 "控制器" 文件夹，选择 "**添加"、"新建测试**"，然后选择**单元测试**模板来创建新的单元测试（请参阅图1）。 将新单元测试命名为 GroupControllerTest，然后单击 **"确定"** 按钮。

[添加 GroupControllerTest 单元测试 ![](iteration-6-use-test-driven-development-vb/_static/image1.jpg)](iteration-6-use-test-driven-development-vb/_static/image1.png)

**图 01**：添加 GroupControllerTest 单元测试（[单击以查看完全大小的映像](iteration-6-use-test-driven-development-vb/_static/image2.png)）

第一个单元测试包含在列表1中。 此测试验证组控制器的 Index （）方法是否返回一组组。 测试将验证是否在视图数据中返回了组的集合。

**列表 1-Controllers\GroupControllerTest.vb**

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample1.vb)]

第一次在 Visual Studio 中的列表1中键入代码时，会收到大量红色波浪线。 尚未创建 GroupController 类或组类。

此时，我们甚至无法生成应用程序，因此我们不能执行第一个单元测试。 这就好了。 这会计为失败测试。 因此，我们现在有权开始编写应用程序代码。 我们需要编写足够的代码来执行测试。

清单2中的组控制器类包含传递单元测试所需的最少代码。 Index （）操作返回一个静态编码的组列表（组类在列表3中定义）。

**列表 2-Controllers\GroupController.vb**

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample2.vb)]

**列表 3-Models\Group.vb**

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample3.vb)]

将 GroupController 和 Group 类添加到项目中后，第一个单元测试成功完成（参见图2）。 我们已经完成了通过测试所需的最少工作量。 现在可以庆祝了。

[![成功！](iteration-6-use-test-driven-development-vb/_static/image2.jpg)](iteration-6-use-test-driven-development-vb/_static/image3.png)

**图 02**： Success！（[单击以查看完全大小的映像](iteration-6-use-test-driven-development-vb/_static/image4.png)）

## <a name="creating-contact-groups"></a>创建联系人组

现在，我们可以转到第二个用户案例。 我们需要能够创建新的联系人组。 我们需要通过测试表达这一意图。

列表4中的测试验证通过新组调用 Create （）方法将该组添加到 Index （）方法返回的组列表。 换句话说，如果我创建一个新组，则应该能够从 Index （）方法返回的组列表返回新组。

**列表 4-Controllers\GroupControllerTest.vb**

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample4.vb)]

列表4中的测试通过新的联系人组调用组控制器 Create （）方法。 接下来，测试验证调用组控制器索引（）方法是否在视图数据中返回新组。

列表5中修改后的组控制器包含通过新测试所需的最小更改。

**列表 5-Controllers\GroupController.vb**

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample5.vb)]

## <a name="the-group-controller-in-listing-5-has-a-new-create-action-this-action-adds-a-group-to-a-collection-of-groups-notice-that-the-index-action-has-been-modified-to-return-the-contents-of-the-collection-of-groups"></a>列表5中的组控制器具有新的 Create （）操作。 此操作可将组添加到组的集合。 请注意，已修改 Index （）操作以返回组集合的内容。

同样，我们已执行完传递单元测试所需的最少工作量。 对组控制器进行这些更改后，我们的所有单元测试都通过。

## <a name="adding-validation"></a>添加验证

用户情景中未明确说明此要求。 但是，要求组具有名称是合理的。 否则，将联系人组织到组中将不会非常有用。

清单6包含一个表示此目的的新测试。 此测试验证尝试在未提供名称的情况下创建组会导致在模型状态中出现验证错误消息。

**列表 6-Controllers\GroupControllerTest.vb**

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample6.vb)]

为了满足此测试要求，我们需要将 "名称" 属性添加到我们的组类（请参阅列表7）。 此外，我们还需要向组控制器 s Create （）操作添加一小段验证逻辑（请参阅列表8）。

**列表 7-Models\Group.vb**

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample7.vb)]

**列表 8-Controllers\GroupController.vb**

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample8.vb)]

请注意，组控制器 Create （）操作现在同时包含验证和数据库逻辑。 目前，组控制器使用的数据库不只包含内存中集合。

## <a name="time-to-refactor"></a>重构时间

红色/绿色/重构的第三步是重构部分。 此时，我们需要从代码返回，并考虑如何重构应用程序以改善其设计。 "重构" 阶段是我们认为难以实现软件设计原则和模式的最佳方式。

我们可以按我们选择的任何方式修改代码，以改进代码设计。 我们有一个安全的单元测试，阻止我们破坏现有功能。

目前，我们的组控制器从优秀的软件设计的角度来看是一种混乱。 组控制器包含验证和数据访问代码的混杂。 若要避免违反单一责任原则，需要将这些问题分隔到不同的类中。

重构的组控制器类包含在列表9中。 已将控制器修改为使用 ContactManager 服务层。 这是与联系人控制器一起使用的服务层。

列表10包含添加到 ContactManager 服务层的新方法，以支持验证、列出和创建组。 更新了 IContactManagerService 接口，以包含新的方法。

列表11包含一个实现 IContactManagerRepository 接口的新 FakeContactManagerRepository 类。 与也实现 IContactManagerRepository 接口的 EntityContactManagerRepository 类不同，我们的新 FakeContactManagerRepository 类不与数据库通信。 FakeContactManagerRepository 类使用内存中集合作为数据库的代理。 我们将在单元测试中使用此类作为假存储库层。

**列表 9-Controllers\GroupController.vb**

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample9.vb)]

**列表 10-Controllers\ContactManagerService.vb**

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample10.vb)]

**列表 11-Controllers\FakeContactManagerRepository.vb**

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample11.vb)]

修改 IContactManagerRepository 接口需要使用来实现 EntityContactManagerRepository 类中的 CreateGroup （）和 ListGroups （）方法。 实现此目的的 laziest 和最快方法是添加如下所示的存根方法：

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample12.vb)]

最后，对应用程序设计所做的这些更改需要我们对单元测试进行一些修改。 我们现在需要在执行单元测试时使用 FakeContactManagerRepository。 已更新的 GroupControllerTest 类包含在列表12中。

**列表 12-Controllers\GroupControllerTest.vb**

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample13.vb)]

完成所有这些更改后，我们会再次通过所有单元测试。 我们已经完成了红色/绿色/重构的整个循环。 我们已经实现了前两个用户情景。 现在，我们已支持用户情景中表示的要求的单元测试。 实现用户情景的其余部分涉及重复相同的红色/绿色/重构循环。

## <a name="modifying-our-database"></a>修改数据库

遗憾的是，尽管我们已经满足单元测试所表示的所有需求，但我们的工作却不能完成。 我们仍需要修改数据库。

我们需要创建一个新的组数据库表。 请执行这些步骤：

1. 在 "服务器资源管理器" 窗口中，右键单击 "表" 文件夹，然后选择 "**添加新表**" 菜单选项。
2. 在表设计器中输入下面所述的两个列。
3. 将 Id 列标记为主键和标识列。
4. 通过单击软盘的图标，使用名称组保存新表。

<a id="0.12_table01"></a>

| **列名称** | **数据类型** | **允许 Null 值** |
| --- | --- | --- |
| Id | int | False |
| “属性” | nvarchar(50) | False |

接下来，需要删除 Contacts 表中的所有数据（否则，我们将无法在 "联系人" 和 "组" 表之间创建关系）。 请执行这些步骤：

1. 右键单击 "联系人" 表，然后选择菜单选项 "**显示表数据**"。
2. 删除所有行。

接下来，需要定义组数据库表和现有联系人数据库表之间的关系。 请执行这些步骤：

1. 双击 "服务器资源管理器" 窗口中的 "联系人" 表，打开表设计器。
2. 向名为 GroupId 的联系人表中添加一个新的整数列。
3. 单击 "关系" 按钮以打开 "外键关系" 对话框（请参阅图3）。
4. 单击“添加”按钮。
5. 单击出现在 "表和列规范" 按钮旁的省略号按钮。
6. 在 "表和列" 对话框中，选择 "组" 作为主键表，Id 作为主键列。 选择 "联系人" 作为外键表，并选择 "GroupId" 作为外键列（参见图4）。 单击“确定”按钮。
7. 在 "**插入和更新规范**" 下，选择 "**删除规则**的值**级联**"。
8. 单击 "关闭" 按钮以关闭 "外键关系" 对话框。
9. 单击 "保存" 按钮以保存对 "联系人" 表所做的更改。

[创建数据库表关系 ![](iteration-6-use-test-driven-development-vb/_static/image3.jpg)](iteration-6-use-test-driven-development-vb/_static/image5.png)

**图 03**：创建数据库表关系（[单击查看完全大小的图像](iteration-6-use-test-driven-development-vb/_static/image6.png)）

[指定表关系 ![](iteration-6-use-test-driven-development-vb/_static/image4.jpg)](iteration-6-use-test-driven-development-vb/_static/image7.png)

**图 04**：指定表关系（[单击查看完全大小的图像](iteration-6-use-test-driven-development-vb/_static/image8.png)）

### <a name="updating-our-data-model"></a>更新数据模型

接下来，我们需要更新数据模型以表示新的数据库表。 请执行这些步骤：

1. 双击 "模型" 文件夹中的 ContactManagerModel 文件以打开 Entity Designer。
2. 右键单击设计器图面，然后选择 "**从数据库更新模型**" 菜单选项。
3. 在更新向导中，选择 "组" 表，然后单击 "完成" 按钮（见图5）。
4. 右键单击 "组" 实体并选择 "**重命名**" 菜单选项。 将 "*组*" 实体的名称更改为 "*分组*（单数）"。
5. 右键单击显示在 Contact 实体底部的 "组" 导航属性。 将*组*导航属性的名称更改为 "*分组*（单数）"。

[![从数据库更新实体框架模型](iteration-6-use-test-driven-development-vb/_static/image5.jpg)](iteration-6-use-test-driven-development-vb/_static/image9.png)

**图 05**：从数据库更新实体框架模型（[单击以查看完全大小的映像](iteration-6-use-test-driven-development-vb/_static/image10.png)）

完成这些步骤后，你的数据模型将同时表示 "联系人" 和 "组" 表。 Entity Designer 应显示这两个实体（见图6）。

[显示组和联系人 Entity Designer ![](iteration-6-use-test-driven-development-vb/_static/image6.jpg)](iteration-6-use-test-driven-development-vb/_static/image11.png)

**图 06**：显示组和联系人的 Entity Designer （[单击查看完全大小的图像](iteration-6-use-test-driven-development-vb/_static/image12.png)）

### <a name="creating-our-repository-classes"></a>创建我们的存储库类

接下来，我们需要实现存储库类。 在此迭代过程中，我们在编写代码来满足单元测试的同时，在 IContactManagerRepository 接口中添加了几个新方法。 IContactManagerRepository 接口的最终版本包含在列表14中。

**列表 14-Models\IContactManagerRepository.vb**

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample14.vb)]

我们实际上并未实现任何与在实际 EntityContactManagerRepository 类中使用联系人组相关的方法。 目前，EntityContactManagerRepository 类具有 IContactManagerRepository 接口中列出的每个联系人组方法的存根方法。 例如，ListGroups （）方法当前如下所示：

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample15.vb)]

存根方法使我们能够编译应用程序并传递单元测试。 不过，现在可以实际实现这些方法。 列表13中包含了 EntityContactManagerRepository 类的最终版本。

**列表 13-Models\EntityContactManagerRepository.vb**

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample16.vb)]

### <a name="creating-the-views"></a>创建视图

当你使用默认的 ASP.NET 视图引擎时，ASP.NET MVC 应用程序。 因此，你不会创建用于响应特定单元测试的视图。 但是，因为在没有视图的情况下，应用程序不能使用，因此，我们无法在不创建和修改 Contact Manager 应用程序中包含的视图的情况下完成此迭代。

我们需要创建以下新视图来管理联系人组（请参阅图7）：

- Views\Group\Index.aspx-显示联系人组列表
- Views\Group\Delete.aspx-显示用于删除联系人组的确认表单

[![组索引视图](iteration-6-use-test-driven-development-vb/_static/image7.jpg)](iteration-6-use-test-driven-development-vb/_static/image13.png)

**图 07**：组索引视图（[单击以查看完全大小的图像](iteration-6-use-test-driven-development-vb/_static/image14.png)）

我们需要修改以下现有视图，使其包括联系人组：

- Views\Home\Create.aspx
- Views\Home\Edit.aspx
- Views\Home\Index.aspx

通过查看本教程附带的 Visual Studio 应用程序，可以看到修改后的视图。 例如，图8说明了联系人索引视图。

[![联系人索引视图](iteration-6-use-test-driven-development-vb/_static/image8.jpg)](iteration-6-use-test-driven-development-vb/_static/image15.png)

**图 08**：联系人索引视图（[单击查看完全大小的图像](iteration-6-use-test-driven-development-vb/_static/image16.png)）

## <a name="summary"></a>摘要

在此迭代中，我们将按照测试驱动的开发应用程序设计方法，向联系人管理器应用程序添加新功能。 我们首先创建一组用户情景。 我们创建了一组与用户情景表示的要求相对应的单元测试。 最后，我们编写了足够的代码来满足单元测试所表示的需求。

编写完足够的代码来满足单元测试所表示的要求后，我们更新了数据库和视图。 我们向数据库中添加了一个新的 "组" 表，并更新了实体框架数据模型。 我们还创建和修改了一组视图。

在下一次迭代中，最后一次迭代-我们会重写应用程序以利用 Ajax。 利用 Ajax，我们将提高联系人管理器应用程序的响应能力和性能。

> [!div class="step-by-step"]
> [上一页](iteration-5-create-unit-tests-vb.md)
> [下一页](iteration-7-add-ajax-functionality-vb.md)
