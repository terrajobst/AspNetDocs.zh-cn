---
uid: mvc/overview/older-versions-1/nerddinner/enable-automated-unit-testing
title: 启用自动单元测试 |Microsoft Docs
author: microsoft
description: 步骤12显示了如何开发一套自动单元测试，用于验证我们的 NerdDinner 功能，并将为我们提供信心来进行更改 。
ms.author: riande
ms.date: 07/27/2010
ms.assetid: a19ff2ce-3f7e-4358-9a51-a1403da9c63e
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/enable-automated-unit-testing
msc.type: authoredcontent
ms.openlocfilehash: 09a7aa186605a6cce48ee94028425ded957c00d3
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78435590"
---
# <a name="enable-automated-unit-testing"></a>启用自动单元测试

由[Microsoft](https://github.com/microsoft)

[下载 PDF](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> 这是免费的["NerdDinner" 应用程序教程](introducing-the-nerddinner-tutorial.md)的步骤12，该教程演示如何使用 ASP.NET MVC 1 构建小型但完整的 web 应用程序。
> 
> 步骤12显示了如何开发一套自动单元测试，这些测试将验证我们的 NerdDinner 功能，并使我们能够在以后对应用程序进行更改和改进。
> 
> 如果你使用的是 ASP.NET MVC 3，则建议你遵循[MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)或[Mvc 音乐应用商店](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)教程中的入门。

## <a name="nerddinner-step-12-unit-testing"></a>NerdDinner 步骤12：单元测试

让我们来开发一套自动单元测试，以验证我们的 NerdDinner 功能，这将使我们能够在以后对应用程序进行更改和改进。

### <a name="why-unit-test"></a>为什么要进行单元测试？

在该驱动器上，早上，你对正在处理的应用程序的灵感突然闪烁。 你认识到，你可以实现一种更改，这会使应用程序变得更好。 它可能是一个清理代码、添加新功能或修复 bug 的重构。

当你到达计算机时，confronts 你的问题是 "如何安全地实现这一改进？" 如果更改有副作用或中断某些内容怎么办？ 更改可能很简单，只需几分钟即可完成，但如果手动测试所有应用程序方案需要数小时呢？ 如果您忘记涵盖某个方案并且损坏的应用程序进入生产环境，该怎么办？ 此改进是否确实值得努力？

自动单元测试可以提供一个安全网络，使你能够持续增强你的应用程序，并避免对你正在处理的代码产生任何担心。 通过使自动测试快速验证功能，你可以放心地进行编码，并使你能够更轻松地进行改进。 它们还有助于创建更易于维护的解决方案，并具有较长的生存期-这将导致投资回报率更高。

ASP.NET MVC 框架使单元测试应用程序功能变得简单快捷。 它还启用了一个测试驱动开发（TDD）工作流，该工作流启用了测试优先的开发。

### <a name="nerddinnertests-project"></a>NerdDinner 项目

当我们在本教程开始时创建 NerdDinner 应用程序时，会出现一个对话框，询问你是否想要创建单元测试项目来与应用程序项目一起使用：

![](enable-automated-unit-testing/_static/image1.png)

已选中 "是，创建单元测试项目" 单选按钮，这将导致向解决方案中添加 "NerdDinner" 项目：

![](enable-automated-unit-testing/_static/image2.png)

NerdDinner 项目引用 NerdDinner 应用程序项目程序集，使我们可以轻松地向其添加验证应用程序功能的自动测试。

### <a name="creating-unit-tests-for-our-dinner-model-class"></a>为晚餐模型类创建单元测试

让我们向 NerdDinner 项目添加一些测试，以验证我们在构建模型层时创建的晚餐类。

首先，我们将在测试项目中创建一个名为 "模型" 的新文件夹，我们将在其中放置模型相关的测试。 然后，右键单击该文件夹，然后选择 "**添加-&gt;新测试**" 菜单命令。 此时将显示 "添加新测试" 对话框。

我们将选择创建 "单元测试" 并将其命名为 "DinnerTest.cs"：

![](enable-automated-unit-testing/_static/image3.png)

单击 "确定" 按钮时，Visual Studio 会将 DinnerTest.cs 文件添加（并打开）到项目中：

![](enable-automated-unit-testing/_static/image4.png)

默认的 Visual Studio 单元测试模板在其中有一组样板代码，我发现有点杂乱。 让我们将其清理，只包含以下代码：

[!code-csharp[Main](enable-automated-unit-testing/samples/sample1.cs)]

上述 DinnerTest 类的 [TestClass] 属性将其标识为包含测试的类，以及可选的测试初始化和拆卸代码。 可以通过在其上添加具有 [TestMethod] 属性的公共方法，在其中定义测试。

下面是我们要添加的两个测试中的第一个测试。 第一次测试验证在创建新晚餐后，如果没有正确设置所有属性，则晚餐无效。 第二个测试验证晚餐是否有效，并且所有属性都设置了有效值：

[!code-csharp[Main](enable-automated-unit-testing/samples/sample2.cs)]

你会注意到，我们的测试名称非常明确（并且稍有详细）。 我们这样做的原因是，我们可能最终会创建数百个或数千个小测试，因此，我们希望能够轻松快速地确定每个测试的意图和行为（特别是当我们要在测试运行程序中查找故障列表）。 测试名称应在要测试的功能之后命名。 以上我们使用的是 "名词\_应\_谓词" 命名模式。

我们使用 "AAA" 测试模式来构建测试，这种模式代表 "排列，Act，断言"：

- 排列：设置要测试的单元
- Act：练习测试单元并捕获结果
- Assert：验证行为

编写测试时，我们希望避免各个测试的操作过多。 相反，每个测试应该只验证单个概念（这会使查找失败的原因变得更加容易）。 一种很好的指导原则是尝试每个测试只使用一个 assert 语句。 如果在测试方法中有多个 assert 语句，请确保它们都用于测试相同的概念。 如果有疑问，请进行另一个测试。

### <a name="running-tests"></a>正在运行测试

Visual Studio 2008 Professional （及更高版本）包含一个内置的测试运行程序，可用于在 IDE 中运行 Visual Studio 单元测试项目。 可以在 "解决方案" 菜单命令中选择 "**测试&gt;运行&gt;所有测试"** （或按 Ctrl R，A），以运行所有单元测试。 或者，也可以将游标定位在特定的测试类或测试方法中，并使用**测试&gt;在当前上下文菜单命令中运行&gt;测试**（或按 Ctrl R，t）来运行单元测试的子集。

让我们将光标置于 DinnerTest 类中，并键入 "Ctrl R，T" 以运行刚刚定义的两个测试。 执行此操作时，将在 Visual Studio 中显示 "测试结果" 窗口，并在其中列出测试运行的结果：

![](enable-automated-unit-testing/_static/image5.png)

*注意：默认情况下，VS 测试结果窗口不显示 "类名" 列。可以通过在 "测试结果" 窗口中右键单击并使用 "添加/删除列" 菜单命令来添加此项。*

这两个测试只需运行一小部分，并且可以看到它们都通过。 现在，我们可以通过创建其他测试来验证具体规则验证，并涵盖添加到晚餐类的两个帮助器方法-IsUserHost （）和 IsUserRegistered （），来对这些方法进行补充。 为晚餐类准备好所有这些测试后，就可以更轻松、更安全地添加新的业务规则并在将来对其进行验证。 我们可以将新的规则逻辑添加到晚餐，然后在几秒钟内验证它是否未被任何以前的逻辑功能中断。

请注意，使用描述性测试名称可以轻松地快速了解每个测试要验证的内容。 我建议使用 "**工具-&gt;选项**" 菜单命令，打开 "测试工具-&gt;测试执行配置" 屏幕，并选中 "双击失败或无结论的单元测试结果将显示测试中的失败点" 复选框。 这将允许您双击 "测试结果" 窗口中的故障并立即跳转到断言失败。

### <a name="creating-dinnerscontroller-unit-tests"></a>创建 DinnersController 单元测试

现在，让我们创建一些单元测试来验证我们的 DinnersController 功能。 首先，右键单击测试项目中的 "控制器" 文件夹，然后选择 "**添加-&gt;新测试**" 菜单命令。 我们将创建 "单元测试" 并将其命名为 "DinnersControllerTest.cs"。

我们将创建两个测试方法，用于验证 DinnersController 上的详细信息（）操作方法。 第一种验证是否在请求现有晚宴时返回视图。 第二个验证请求不存在的晚餐时返回 "NotFound" 视图：

[!code-csharp[Main](enable-automated-unit-testing/samples/sample3.cs)]

上面的代码编译干净。 但在运行测试时，它们都将失败：

![](enable-automated-unit-testing/_static/image6.png)

如果查看错误消息，我们将看到测试失败的原因，因为我们的 DinnersRepository 类无法连接到数据库。 我们的 NerdDinner 应用程序使用连接字符串连接到本地 SQL Server Express 文件，该文件位于 NerdDinner 应用程序项目的 \App\_数据目录下。 由于我们的 NerdDinner 项目在不同的目录中进行编译和运行，因此，该应用程序项目的连接字符串的相对路径位置不正确。

我们*可以*通过将 SQL Express 数据库文件复制到测试项目中来解决此问题，然后在测试项目的 app.config 中将相应的测试连接字符串添加到该文件中。 这会使上面的测试解除阻止并运行。

然而，使用实际数据库的单元测试代码带来了许多挑战。 尤其是在下列情况下：

- 它显著降低了单元测试的执行时间。 运行测试所花费的时间越长，频繁执行它们的可能性就越低。 理想情况下，你希望你的单元测试能够在数秒内运行，并将其作为编译项目的自然方式。
- 它会使测试内的设置和清理逻辑复杂化。 您希望每个单元测试都是独立的，并且不依赖于其他单元测试（无副作用或依赖项）。 处理真实数据库时，必须注意状态，并在测试之间重置。

让我们看一下称为 "依赖关系注入" 的设计模式，这可以帮助我们解决这些问题，并避免需要在测试中使用实际数据库。

### <a name="dependency-injection"></a>依赖关系注入

现在，DinnersController 紧靠 DinnerRepository 类。 "耦合" 指的是类显式依赖于另一类以便正常工作的情况：

[!code-csharp[Main](enable-automated-unit-testing/samples/sample4.cs)]

由于 DinnerRepository 类需要对数据库的访问权限，DinnersController 类在 DinnerRepository 上具有紧密耦合的依赖项，因此，为了对 DinnersController 操作方法进行测试，要求我们具有一个数据库。

我们可以通过使用名为 "依赖关系注入" 的设计模式来解决此问题，这种方法在使用它们的类中不再隐式创建依赖项（如提供数据访问的存储库类）。 相反，可以将依赖项显式传递到使用构造函数参数的类。 如果使用接口定义依赖项，则我们可以灵活地为单元测试方案传递 "假" 依赖项实现。 这样，我们便可以创建不需要访问数据库的特定于测试的依赖项实现。

要了解这一点，让我们通过 DinnersController 实现依赖关系注入。

#### <a name="extracting-an-idinnerrepository-interface"></a>提取 IDinnerRepository 接口

第一步是创建一个新的 IDinnerRepository 接口，用于封装控制器检索和更新就时所需的存储库协定。

可以通过右键单击 \Models 文件夹，然后选择 "**添加-&gt;新项**" 菜单命令并创建一个名为 IDinnerRepository.cs 的新接口，来手动定义此接口协定。

此外，我们还可以使用内置 Visual Studio Professional （和更高版本）的重构工具为我们从现有的 DinnerRepository 类中自动提取和创建一个接口。 若要使用 VS 提取此接口，只需将光标置于 DinnerRepository 类的文本编辑器中，然后右键单击并选择 "**重构-&gt;提取接口**" 菜单命令：

![](enable-automated-unit-testing/_static/image7.png)

这将启动 "提取接口" 对话框，并提示我们输入要创建的接口的名称。 它将默认为 IDinnerRepository，并自动选择现有 DinnerRepository 类中的所有公共方法，以添加到接口：

![](enable-automated-unit-testing/_static/image8.png)

单击 "确定" 按钮时，Visual Studio 将向应用程序添加新的 IDinnerRepository 接口：

[!code-csharp[Main](enable-automated-unit-testing/samples/sample5.cs)]

将更新现有的 DinnerRepository 类，使其实现接口：

[!code-csharp[Main](enable-automated-unit-testing/samples/sample6.cs)]

#### <a name="updating-dinnerscontroller-to-support-constructor-injection"></a>更新 DinnersController 以支持构造函数注入

现在，我们将更新 DinnersController 类以使用新的接口。

当前 DinnersController 是硬编码的，因此其 "dinnerRepository" 字段始终是一个 DinnerRepository 类：

[!code-csharp[Main](enable-automated-unit-testing/samples/sample7.cs)]

我们将对其进行更改，使 "dinnerRepository" 字段的类型为 IDinnerRepository 而不是 DinnerRepository。 接下来，我们将添加两个公共 DinnersController 构造函数。 其中一个构造函数允许将 IDinnerRepository 作为参数进行传递。 另一个是使用现有 DinnerRepository 实现的默认构造函数：

[!code-csharp[Main](enable-automated-unit-testing/samples/sample8.cs)]

由于 ASP.NET MVC 默认使用默认构造函数创建控制器类，因此，我们在运行时 DinnersController 将继续使用 DinnerRepository 类来执行数据访问。

不过，现在我们可以更新单元测试，以使用参数构造函数传入 "虚假" 晚餐存储库实现。 此 "虚假" 晚餐存储库不需要访问实际数据库，而是使用内存中示例数据。

#### <a name="creating-the-fakedinnerrepository-class"></a>创建 FakeDinnerRepository 类

让我们创建一个 FakeDinnerRepository 类。

首先，我们将在 NerdDinner 项目中创建一个 "Fakes" 目录，然后向其添加新的 FakeDinnerRepository 类（右键单击该文件夹，然后选择 "**添加-&gt;新类**）"：

![](enable-automated-unit-testing/_static/image9.png)

我们将更新代码，使 FakeDinnerRepository 类实现 IDinnerRepository 接口。 然后，可以右键单击它并选择 "实现接口 IDinnerRepository" 上下文菜单命令：

![](enable-automated-unit-testing/_static/image10.png)

这将导致 Visual Studio 将所有 IDinnerRepository 接口成员自动添加到 FakeDinnerRepository 类，其默认值为 "stub out" 实现：

[!code-csharp[Main](enable-automated-unit-testing/samples/sample9.cs)]

然后，可以将 FakeDinnerRepository 实现更新为在内存中列表中工作，&lt;晚餐&gt; 集合作为构造函数参数传递给它：

[!code-csharp[Main](enable-automated-unit-testing/samples/sample10.cs)]

现在，我们有了一个不需要数据库的虚设 IDinnerRepository 实现，可以改为使用内存中的晚餐对象列表。

#### <a name="using-the-fakedinnerrepository-with-unit-tests"></a>将 FakeDinnerRepository 用于单元测试

让我们返回到以前失败的 DinnersController 单元测试，因为数据库不可用。 我们可以使用以下代码更新测试方法，以将使用内存中的内存导入数据的 FakeDinnerRepository 与 DinnersController 一起使用：

[!code-csharp[Main](enable-automated-unit-testing/samples/sample11.cs)]

现在，当我们运行这些测试时，它们都通过：

![](enable-automated-unit-testing/_static/image11.png)

最重要的是，它们只需运行一小部分，无需任何复杂的设置/清理逻辑。 现在，我们可以对所有 DinnersController 操作方法代码（包括列表、分页、详细信息、创建、更新和删除）进行单元测试，而无需连接到实际数据库。

| **边主题：依赖关系注入框架** |
| --- |
| 执行手动依赖关系注入（如我们的工作方式）运行正常，但随着应用程序中的依赖项和组件数量的增加，维护变得越来越困难。 .NET 存在多个依赖关系注入框架，可帮助提供更多依赖关系管理灵活性。 这些框架（有时也称为 "控制反转" （IoC）容器）提供了一些机制，允许在运行时指定对象的依赖项并将依赖项传递到对象（最常使用构造函数注入）). .NET 中的一些更常见的 OSS 依赖关系注入/IOC 框架包括： AutoFac、Ninject、Spring.NET、StructureMap 和 Windsor。 ASP.NET MVC 公开了可扩展性 Api，使开发人员能够参与控制器的解析和实例化，并使依赖关系注入/IoC 框架在此过程中完全集成。 使用 DI/IOC 框架还可以从 DinnersController 中删除默认的构造函数，这将完全删除它与 DinnerRepository 之间的耦合。 我们不会在 NerdDinner 应用程序中使用依赖关系注入/IOC 框架。 但如果 NerdDinner 的基本代码和功能增长，我们可能会考虑到这一点。 |

### <a name="creating-edit-action-unit-tests"></a>创建编辑操作单元测试

现在，让我们创建一些单元测试来验证 DinnersController 的编辑功能。 首先，我们将测试编辑操作的 HTTP 获取版本：

[!code-csharp[Main](enable-automated-unit-testing/samples/sample12.cs)]

接下来，我们将创建一个测试，用于验证请求某个 DinnerFormViewModel 对象所支持的视图时，该视图将呈现回来：

[!code-csharp[Main](enable-automated-unit-testing/samples/sample13.cs)]

但在运行测试时，我们会发现它失败，因为在编辑方法访问 User.Identity.Name 属性以执行 IsHostedBy （）检查时，会引发空引用异常。

控制器基类上的 User 对象封装了有关已登录用户的详细信息，并在运行时创建控制器时由 ASP.NET MVC 填充。 由于我们要在 web 服务器环境之外测试 DinnersController，因此不会设置 User 对象（因此为空引用异常）。

### <a name="mocking-the-useridentityname-property"></a>模拟 User.Identity.Name 属性

模拟框架通过使我们能够动态创建支持测试的各种依赖对象，使测试变得更加轻松。 例如，我们可以在编辑操作测试中使用模拟框架来动态创建用户对象，DinnersController 可使用该对象查找模拟的用户名。 这将避免在我们运行测试时引发空引用。

可以将许多 .NET 模拟框架与 ASP.NET MVC 一起使用（可在此处查看这些框架的列表： [http://www.mockframeworks.com/](http://www.mockframeworks.com/)）。 若要测试我们的 NerdDinner 应用程序，我们将使用名为 "Moq" 的开源模拟 framework， [http://www.mockframeworks.com/moq](http://www.mockframeworks.com/moq)可以免费下载该框架。

下载完成后，我们会在 NerdDinner 项目中添加对 Moq 程序集的引用：

![](enable-automated-unit-testing/_static/image12.png)

然后，将 "CreateDinnersControllerAs （用户名）" 帮助器方法添加到将用户名作为参数的测试类，然后 "模拟" DinnersController 实例上的 User.Identity.Name 属性：

[!code-csharp[Main](enable-automated-unit-testing/samples/sample14.cs)]

以上我们使用 Moq 来创建 fakes ControllerContext 对象的 Mock 对象（这就是 ASP.NET MVC 传递到 Controller 类的对象，用于公开用户、请求、响应和会话等运行时对象）。 我们正在模拟模拟上的 "SetupGet" 方法，指示 ControllerContext 上的 HttpContext.User.Identity.Name 属性应返回传递给帮助器方法的用户名字符串。

可以模拟任意数量的 ControllerContext 属性和方法。 为了说明这一点，我还添加了 SetupGet （）调用，以用于 IsAuthenticated 属性（对于下面的测试，实际上不需要此属性），但这有助于阐释您如何模拟请求属性。 完成后，我们将 ControllerContext mock 的实例分配给 DinnersController 的帮助器方法返回的。

现在，我们可以编写使用此帮助器方法的单元测试来测试涉及不同用户的编辑方案：

[!code-csharp[Main](enable-automated-unit-testing/samples/sample15.cs)]

现在，当我们运行它们所通过的测试时：

![](enable-automated-unit-testing/_static/image13.png)

### <a name="testing-updatemodel-scenarios"></a>测试 UpdateModel （）方案

我们已经创建了包含编辑操作的 HTTP GET 版本的测试。 现在，让我们创建一些测试来验证 HTTP POST 版本的编辑操作：

[!code-csharp[Main](enable-automated-unit-testing/samples/sample16.cs)]

我们使用此操作方法支持的有趣的新测试方案是在控制器基类上使用 UpdateModel （） helper 方法。 我们使用此帮助器方法将窗体发布值绑定到晚餐对象实例。

下面是两个测试，演示了如何为要使用的 UpdateModel （）帮助程序方法提供窗体的已发布值。 为此，我们将创建并填充 FormCollection 对象，然后将其分配给控制器上的 "ValueProvider" 属性。

第一次测试验证是否在成功保存浏览器时，将浏览器重定向到详细信息操作。 第二个测试验证在发布无效输入时，操作再次重新显示 "编辑" 视图并显示错误消息。

[!code-csharp[Main](enable-automated-unit-testing/samples/sample17.cs)]

### <a name="testing-wrap-up"></a>测试向上环绕

我们介绍了单元测试控制器类中涉及的核心概念。 我们可以使用这些技术轻松创建数百个验证应用程序行为的简单测试。

由于控制器和模型测试不需要实际数据库，因此它们的运行速度极快且运行非常简单。 我们将能够在几秒内执行数百个自动测试，并立即获得反馈，以确定是否有更改中断了某些内容。 这将有助于我们满怀信心地不断改进、重构和改进我们的应用程序。

我们已将测试作为本章中的最后一个主题进行，但不是因为在开发过程结束时应该执行测试！ 相反，应在开发过程中尽早编写自动测试。 这样做使您可以在开发时立即获得反馈，有助于您周全应用程序的用例方案，并指导您在设计应用程序时使用干净的分层和耦合。

本书后面的一章将讨论测试驱动开发（TDD），以及如何将其与 ASP.NET MVC 一起使用。 TDD 是一种迭代编码实践，你首先编写生成的代码将满足的测试。 使用 TDD，通过创建用于验证要实现的功能的测试，开始每个功能。 首先编写单元测试有助于确保你清楚地了解该功能及其工作原理。 只有在编写测试（并且已验证它失败）后，才可以实现测试所验证的实际功能。 因为您已经花了时间考虑该功能的工作原理，您将更好地理解这些要求以及实现它们的最佳方式。 完成实现后，您可以重新运行测试，并获得有关该功能是否正常工作的即时反馈。 我们将在第10章中介绍 TDD。

### <a name="next-step"></a>下一步

某些最终的汇总注释。

> [!div class="step-by-step"]
> [上一页](use-ajax-to-implement-mapping-scenarios.md)
> [下一页](nerddinner-wrap-up.md)
