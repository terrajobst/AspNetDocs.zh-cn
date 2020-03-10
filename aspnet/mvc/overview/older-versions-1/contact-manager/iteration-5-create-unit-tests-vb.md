---
uid: mvc/overview/older-versions-1/contact-manager/iteration-5-create-unit-tests-vb
title: '迭代 #5 –创建单元测试（VB） |Microsoft Docs'
author: microsoft
description: 在第五次迭代中，通过添加单元测试使应用程序更易于维护和修改。 我们模拟了数据模型类，并生成了用于 o 的单元测试 。
ms.author: riande
ms.date: 02/20/2009
ms.assetid: c6e5c036-2265-4fa7-a9eb-47f197bdc262
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-5-create-unit-tests-vb
msc.type: authoredcontent
ms.openlocfilehash: 4ce1c6224a7e9203ff62f136f4f3a43e4561a904
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78437834"
---
# <a name="iteration-5--create-unit-tests-vb"></a>迭代 #5 –创建单元测试（VB）

由[Microsoft](https://github.com/microsoft)

[下载代码](iteration-5-create-unit-tests-vb/_static/contactmanager_5_vb1.zip)

> 在第五次迭代中，通过添加单元测试使应用程序更易于维护和修改。 我们模拟数据模型类，并为控制器和验证逻辑生成单元测试。

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

在联系人管理器应用程序的前一次迭代中，我们重构了应用程序，使其更松耦合。 将应用程序分离到不同的控制器、服务和存储库层。 每一层通过接口与其下面的层交互。

我们重构了应用程序，使应用程序更易于维护和修改。 例如，如果需要使用新的数据访问技术，只需更改存储库层，无需接触控制器或服务层。 通过使 Contact Manager 松散耦合起来，我们使应用程序更具弹性性来进行更改。

但当我们需要向联系人管理器应用程序添加新功能时，会发生什么情况？ 或者，修复 bug 后会出现什么情况？ 一种很好的经验证的代码编写，就是每次触摸代码时都会产生新的 bug。

例如，你的经理可能会要求你向联系人经理添加新功能。 她希望你添加对联系人组的支持。 她希望您能够使用户能够将其联系人组织到朋友、商业等的组中。

为了实现这一新功能，您将需要修改联系人管理器应用程序的所有三个层。 需要向控制器、服务层和存储库添加新功能。 一旦开始修改代码，就会面临一些重大功能。

像之前的迭代一样，将应用程序重构为单独的层是一件好事。 这是一件好事，因为它使我们能够在不触及应用程序的其余部分的情况下对整个层进行更改。 但是，如果要使代码中的代码更易于维护和修改，则需要为代码创建单元测试。

使用单元测试来测试单个代码单元。 这些代码单元小于整个应用程序层。 通常，使用单元测试来验证代码中的某个特定方法的行为是否符合预期。 例如，你可以为 ContactManagerService 类公开的 CreateContact （）方法创建单元测试。

应用程序的单元测试与安全网络的工作方式相同。 每当在应用程序中修改代码时，都可以运行一组单元测试来检查修改是否会破坏现有功能。 单元测试使代码修改安全。 单元测试使得应用程序中的所有代码都能够更灵活地进行更改。

在此迭代中，我们向联系人管理器应用程序添加单元测试。 这样，在下一次迭代中，我们可以将联系人组添加到我们的应用程序，而无需担心破坏现有功能。

> [!NOTE] 
> 
> 有多种单元测试框架，包括 NUnit、xUnit.net 和 MbUnit。 在本教程中，我们将使用 Visual Studio 中包含的单元测试框架。 不过，您可以轻松地使用其中一种替代框架。

## <a name="what-gets-tested"></a>测试的内容

在完美的世界中，所有代码都将包含在单元测试中。 在完美的世界中，您可以获得完美的安全网络。 可以通过执行单元测试来修改应用程序中的任何代码行，并可立即了解更改是否会破坏现有功能。

但是，我们不会在完美的世界中生活。 在实践中，编写单元测试时，您将重点放在编写业务逻辑的测试（例如，验证逻辑）上。 特别是，*不*为数据访问逻辑或视图逻辑编写单元测试。

若要有用，必须非常快速地执行单元测试。 您可以轻松地为应用程序积累数百（甚至上千个）的单元测试。 如果单元测试需要很长时间才能运行，则可以避免执行它们。 换句话说，长时间运行的单元测试不能用于日常编码。

出于此原因，通常不会为与数据库交互的代码编写单元测试。 对活动数据库运行数百个单元测试将会太慢。 相反，您需要模拟您的数据库，并编写与 mock 数据库交互的代码（我们在下面讨论了模拟数据库）。

由于类似的原因，通常不会为视图编写单元测试。 若要测试视图，必须启动 web 服务器。 由于旋转 web 服务器的过程相对较慢，因此不建议为视图创建单元测试。

如果视图包含复杂逻辑，则应考虑将逻辑移到帮助器方法中。 你可以为在不旋转 web 服务器的情况下执行的帮助器方法编写单元测试。

> [!NOTE] 
> 
> 编写单元测试时，为数据访问逻辑或查看逻辑编写测试并不是一个好主意，这些测试在构建功能或集成测试时非常有用。

> [!NOTE] 
> 
> ASP.NET MVC 是 Web 窗体视图引擎。 尽管 Web 窗体视图引擎依赖于 web 服务器，但其他视图引擎可能不是。

## <a name="using-a-mock-object-framework"></a>使用 Mock 对象框架

构建单元测试时，几乎总是需要利用 Mock 对象框架。 Mock 对象框架使你可以为应用程序中的类创建模拟和存根。

例如，可以使用 Mock 对象框架生成存储库类的模拟版本。 这样，便可以在单元测试中使用 mock 存储库类，而不是实际存储库类。 使用 mock 存储库可以避免在执行单元测试时执行数据库代码。

Visual Studio 不包括 Mock 对象框架。 但是，有几个适用于 .NET framework 的商业和开源模拟对象框架：

1. Moq-此框架在开源 BSD 许可证下提供。 可以从[https://code.google.com/p/moq/](https://code.google.com/p/moq/)下载 Moq。
2. Rhino 模拟-在开源 BSD 许可证下提供此框架。 可以从[http://ayende.com/projects/rhino-mocks.aspx](http://ayende.com/projects/rhino-mocks.aspx)下载 Rhino 模拟。
3. Typemock Isolator-这是一个商业框架。 可以从[http://www.typemock.com/](http://www.typemock.com/)下载试用版。

在本教程中，我决定使用 Moq。 不过，您可以轻松地使用 Rhino 模拟或 Typemock Isolator 为 "联系人管理器" 应用程序创建 Mock 对象。

你需要先完成以下步骤，然后才能使用 Moq：

1. .
2. 解压缩下载之前，请确保右键单击该文件，然后单击标记为 "**解除阻止**" 的按钮（参见图1）。
3. 解压缩下载。
4. 通过选择菜单选项 "**项目"、"添加引用"，** 将对 Moq 程序集的引用添加到测试项目，以打开 "**添加引用**" 对话框。 在 "浏览" 选项卡下，浏览到解压缩 Moq 的文件夹，并选择 Moq 程序集。 单击 **"确定"** 按钮（见图2）。

[![取消阻止 Moq](iteration-5-create-unit-tests-vb/_static/image1.jpg)](iteration-5-create-unit-tests-vb/_static/image1.png)

**图 01**：取消阻止 Moq （[单击查看完全尺寸的图像](iteration-5-create-unit-tests-vb/_static/image2.png)）

[添加 Moq 后的 ![引用](iteration-5-create-unit-tests-vb/_static/image2.jpg)](iteration-5-create-unit-tests-vb/_static/image3.png)

**图 02**：添加 Moq 后的引用（[单击以查看完全大小的图像](iteration-5-create-unit-tests-vb/_static/image4.png)）

## <a name="creating-unit-tests-for-the-service-layer"></a>为服务层创建单元测试

首先，让我们为联系人管理器应用程序的服务层创建一组单元测试。 我们将使用这些测试来验证验证逻辑。

在 ContactManager 项目中创建名为 "模型" 的新文件夹。 接下来，右键单击 "模型" 文件夹，然后选择 "**添加"、"新建测试"** 。 此时将显示如图3所示的 "**添加新测试**" 对话框。 选择**单元测试**模板并将新测试命名为 ContactManagerServiceTest。 单击 **"确定"** 按钮将新测试添加到测试项目中。

> [!NOTE] 
> 
> 通常，你希望测试项目的文件夹结构与 ASP.NET MVC 项目的文件夹结构相匹配。 例如，你将控制器测试放在控制器文件夹中，在模型文件夹中放置模型测试，依此类推。

[![Models\ContactManagerServiceTest.cs](iteration-5-create-unit-tests-vb/_static/image3.jpg)](iteration-5-create-unit-tests-vb/_static/image5.png)

**图 03**： Models\ContactManagerServiceTest.cs （[单击查看完全大小的图像](iteration-5-create-unit-tests-vb/_static/image6.png)）

最初，我们想要测试由 ContactManagerService 类公开的 CreateContact （）方法。 我们会创建以下五项测试：

- CreateContact （）-当有效的联系人传递到方法时，CreateContact （）的测试将返回值 true。
- CreateContactRequiredFirstName （）-测试在将缺少名字的联系人传递到 CreateContact （）方法时，是否将错误消息添加到模型状态。
- CreateContactRequiredLastName （）-测试当缺少姓氏的联系人传递到 CreateContact （）方法时，是否将错误消息添加到模型状态。
- CreateContactInvalidPhone （）-测试将包含无效电话号码的联系人传递到 CreateContact （）方法时，是否将错误消息添加到模型状态。
- CreateContactInvalidEmail （）-测试将包含无效电子邮件地址的联系人传递到 CreateContact （）方法时，是否将错误消息添加到模型状态。

第一次测试验证有效的联系人是否不产生验证错误。 其余测试检查每个验证规则。

这些测试的代码包含在列表1中。

**列表 1-Models\ContactManagerServiceTest.vb**

[!code-vb[Main](iteration-5-create-unit-tests-vb/samples/sample1.vb)]

由于我们使用的是列表1中的 Contact 类，因此需要在测试项目中添加对 Microsoft 实体框架的引用。 添加对 System.web 程序集的引用。

列表1包含一个名为 Initialize （）的方法，该方法使用 [TestInitialize] 特性修饰。 此方法在运行每个单元测试之前自动调用（它将在每个单元测试之前的5倍之前调用）。 Initialize （）方法使用以下代码行创建 mock 存储库：

[!code-vb[Main](iteration-5-create-unit-tests-vb/samples/sample2.vb)]

下面这行代码使用 Moq 框架通过 IContactManagerRepository 接口生成模拟存储库。 使用 mock 存储库而不是实际的 EntityContactManagerRepository，以避免在运行每个单元测试时访问数据库。 Mock 存储库实现了 IContactManagerRepository 接口的方法，但方法实际上不会执行任何操作。

> [!NOTE] 
> 
> 使用 Moq 框架时，\_mockRepository 和 \_mockRepository 之间存在差异。 前者引用 Mock （of IContactManagerRepository）类，该类包含用于指定模拟存储库的行为方式的方法。 后者指的是实现 IContactManagerRepository 接口的实际模拟存储库。

在创建 ContactManagerService 类的实例时，将在 Initialize （）方法中使用 mock 存储库。 所有单个单元测试都使用此 ContactManagerService 类的实例。

列表1包含五个对应于每个单元测试的方法。 其中每个方法都用 [TestMethod] 属性修饰。 运行单元测试时，将调用具有此属性的任何方法。 换言之，使用 [TestMethod] 属性修饰的任何方法都是单元测试。

第一个名为 CreateContact （）的单元测试验证当 Contact 类的有效实例传递给方法时，调用 CreateContact （）将返回值 true。 该测试将创建 Contact 类的实例，调用 CreateContact （）方法，并验证 CreateContact （）是否返回值 true。

如果调用 CreateContact （）方法时使用了无效的联系人，则剩余的测试将验证该方法返回 false，并将预期的验证错误消息添加到模型状态。 例如，CreateContactRequiredFirstName （）测试创建 Contact 类的实例，其 FirstName 属性的字符串为空。 接下来，将调用 CreateContact （）方法与无效的联系人。 最后，测试验证 CreateContact （）是否返回 false，并且模型状态是否包含预期的验证错误消息 "名字是必需的"。

您可以通过选择 "**测试"、"运行" 解决方案中的所有测试（CTRL + R、A）** 来运行列表1中的单元测试。 测试结果将显示在 "测试结果" 窗口中（参见图4）。

[![测试结果](iteration-5-create-unit-tests-vb/_static/image4.jpg)](iteration-5-create-unit-tests-vb/_static/image7.png)

**图 04**：测试结果（[单击查看完全大小的图像](iteration-5-create-unit-tests-vb/_static/image8.png)）

## <a name="creating-unit-tests-for-controllers"></a>为控制器创建单元测试

ASP.NET MVC 应用程序控制用户交互的流。 测试控制器时，需要测试控制器是否返回正确的操作结果和查看数据。 你还可能需要测试控制器是否以预期的方式与模型类交互。

例如，列表2包含 Contact controller Create （）方法的两个单元测试。 第一个单元测试验证当有效的联系人传递到 Create （）方法时，Create （）方法将重定向到索引操作。 换言之，当传递了有效的联系人时，Create （）方法应返回表示索引操作的 RedirectToRouteResult。

测试控制器层时，不需要测试 ContactManager 服务层。 因此，我们会在 Initialize 方法中模拟包含以下代码的服务层：

[!code-vb[Main](iteration-5-create-unit-tests-vb/samples/sample3.vb)]

在 CreateValidContact （）单元测试中，我们模拟了用以下代码行调用服务层 CreateContact （）方法的行为：

[!code-vb[Main](iteration-5-create-unit-tests-vb/samples/sample4.vb)]

如果调用了 CreateContact （）方法，则这行代码会导致模拟 ContactManager 服务返回值 true。 通过模拟服务层，我们可以测试控制器的行为，而无需在服务层中执行任何代码。

第二个单元测试验证当向方法传递无效的联系人时，Create （）操作是否返回 "创建" 视图。 我们会使服务层 CreateContact （）方法将值 false 返回给以下代码行：

[!code-vb[Main](iteration-5-create-unit-tests-vb/samples/sample5.vb)]

如果 Create （）方法的行为与我们所期望的一样，则它应在服务层返回值为 false 时返回 Create view。 这样一来，控制器就可以在 "创建" 视图中显示验证错误消息，并且用户有机会更正无效的联系人属性。

如果打算为控制器构建单元测试，则需要从控制器操作返回显式视图名称。 例如，不要返回如下所示的视图：

返回视图（）

相反，返回如下所示的视图：

返回视图（"Create"）

如果在返回视图时不是显式的，则 ViewResult. ViewName 属性返回空字符串。

**列表 2-Controllers\ContactControllerTest.vb**

[!code-vb[Main](iteration-5-create-unit-tests-vb/samples/sample6.vb)]

## <a name="summary"></a>摘要

在此迭代中，我们为联系人管理器应用程序创建了单元测试。 我们可以随时运行这些单元测试，以验证应用程序是否仍按预期方式运行。 单元测试可充当应用程序的安全网络，使我们能够在将来安全地修改应用程序。

我们创建了两组单元测试。 首先，我们通过为服务层创建单元测试来测试验证逻辑。 接下来，我们通过为控制器层创建单元测试来测试流控制逻辑。 在测试我们的服务层时，我们通过模拟存储库层将我们的服务层的测试与存储库层隔离开来。 测试控制器层时，我们会通过模拟服务层，将我们的控制器层的测试隔离开来。

在下一次迭代中，我们修改联系人管理器应用程序，使其支持联系人组。 我们将使用名为 "测试驱动开发" 的软件设计过程将这一新功能添加到应用程序。

> [!div class="step-by-step"]
> [上一页](iteration-4-make-the-application-loosely-coupled-vb.md)
> [下一页](iteration-6-use-test-driven-development-vb.md)
