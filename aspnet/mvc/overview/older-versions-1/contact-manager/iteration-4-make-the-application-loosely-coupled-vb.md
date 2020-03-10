---
uid: mvc/overview/older-versions-1/contact-manager/iteration-4-make-the-application-loosely-coupled-vb
title: '迭代 #4 –使应用程序松散耦合（VB） |Microsoft Docs'
author: microsoft
description: 在第四次迭代中，我们将利用多种软件设计模式来更轻松地维护和修改联系人管理器应用程序。 预测...
ms.author: riande
ms.date: 02/20/2009
ms.assetid: 92c70297-4430-4e4e-919a-9c2333a8d09a
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-4-make-the-application-loosely-coupled-vb
msc.type: authoredcontent
ms.openlocfilehash: 422c75406d9c08279d0c2224ee4b6db3a71eb1b3
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78470222"
---
# <a name="iteration-4--make-the-application-loosely-coupled-vb"></a>迭代 #4 –使应用程序松散耦合（VB）

由[Microsoft](https://github.com/microsoft)

[下载代码](iteration-4-make-the-application-loosely-coupled-vb/_static/contactmanager_4_vb1.zip)

> 在第四次迭代中，我们将利用多种软件设计模式来更轻松地维护和修改联系人管理器应用程序。 例如，我们重构应用程序以使用存储库模式和依赖关系注入模式。

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

在联系人管理器应用程序的第四次迭代中，我们重构应用程序，使应用程序更松耦合。 当应用程序松耦合时，可以在应用程序的一个部分修改代码，而无需修改应用程序的其他部分中的代码。 松散耦合的应用程序可以更灵活地进行更改。

目前，联系人管理器应用程序使用的所有数据访问和验证逻辑都包含在控制器类中。 这是一个不错的想法。 无论何时需要修改应用程序的一部分，都可以在应用程序的其他部分中引入 bug。 例如，如果您修改了验证逻辑，则可能会向您的数据访问或控制器逻辑引入新的 bug。

> [!NOTE] 
> 
> （SRP），类不应有多个要更改的原因。 混合控制器、验证和数据库逻辑是单一责任原则的巨大冲突。

可能需要修改应用程序的原因有多种。 你可能需要向应用程序添加新功能，你可能需要在应用程序中修复 bug，或者可能需要修改应用程序的功能的实现方式。 应用程序很少是静态的。 它们倾向于随着时间的推移而不断变化。

例如，假设您决定更改如何实现数据访问层。 现在，联系人管理器应用程序使用 Microsoft 实体框架来访问数据库。 但是，你可能决定迁移到新的或替代的数据访问技术，如 ADO.NET Data Services 或 NHibernate。 但是，由于数据访问代码不与验证和控制器代码隔离，因此无法修改您的应用程序中的数据访问代码，而无需修改与数据访问直接相关的其他代码。

另一方面，如果应用程序是松散耦合的，则可以对应用程序的一个部分进行更改，而不会触及应用程序的其他部分。 例如，你可以在不修改验证或控制器逻辑的情况下切换数据访问技术。

在此迭代中，我们将利用多种软件设计模式，使我们能够将我们的联系人管理器应用程序重构为更松散耦合的应用程序。 完成后，联系人经理就会对其执行的操作不会执行任何操作。 不过，以后我们可以更轻松地更改应用程序。

> [!NOTE] 
> 
> 重构是以不丢失任何现有功能的方式重写应用程序的过程。

## <a name="using-the-repository-software-design-pattern"></a>使用存储库软件设计模式

第一次更改是利用称为存储库模式的软件设计模式。 我们将使用存储库模式将数据访问代码与我们的应用程序的其余部分隔离开来。

实现存储库模式需要我们完成以下两个步骤：

1. 创建接口
2. 创建实现接口的具体类

首先，我们需要创建一个接口，用于描述需要执行的所有数据访问方法。 IContactManagerRepository 接口包含在列表1中。 此接口描述了五种方法： CreateContact （）、DeleteContact （）、EditContact （）、GetContact 和 ListContacts （）。

**列表 1-Models\IContactManagerRepository.vb**

[!code-vb[Main](iteration-4-make-the-application-loosely-coupled-vb/samples/sample1.vb)]

接下来，我们需要创建一个具体的类来实现 IContactManagerRepository 接口。 由于我们使用 Microsoft 实体框架来访问数据库，我们将创建一个名为 EntityContactManagerRepository 的新类。 此类包含在清单2中。

**列表 2-Models\EntityContactManagerRepository.vb**

[!code-vb[Main](iteration-4-make-the-application-loosely-coupled-vb/samples/sample2.vb)]

请注意，EntityContactManagerRepository 类实现 IContactManagerRepository 接口。 类实现该接口描述的所有五个方法。

您可能想知道为什么需要使用接口进行干扰。 为什么需要同时创建一个接口和一个实现它的类呢？

除了一个例外，我们的应用程序的其余部分将与接口交互，而不是具体的类。 我们将调用由 IContactManagerRepository 接口公开的方法，而不是调用 EntityContactManagerRepository 类公开的方法。

这样，我们就可以使用新类实现接口，而无需修改应用程序的其余部分。 例如，在将来的某个日期，我们可能要实现实现 IContactManagerRepository 接口的 DataServicesContactManagerRepository 类。 DataServicesContactManagerRepository 类可能使用 ADO.NET Data Services 来访问数据库，而不是 Microsoft 实体框架。

如果针对 IContactManagerRepository 接口而不是具体 EntityContactManagerRepository 类对应用程序代码进行编程，则可以切换具体的类，而无需修改代码的其余部分。 例如，可以从 EntityContactManagerRepository 类切换到 DataServicesContactManagerRepository 类，而无需修改我们的数据访问或验证逻辑。

对接口（抽象）而不是具体的类进行编程可以使应用程序更具弹性的变化。

> [!NOTE] 
> 
> 通过选择菜单选项 "重构"、"提取接口"，可以在 Visual Studio 中从具体类快速创建接口。 例如，您可以首先创建 EntityContactManagerRepository 类，然后使用 "提取接口" 自动生成 IContactManagerRepository 接口。

## <a name="using-the-dependency-injection-software-design-pattern"></a>使用依赖关系注入软件设计模式

现在我们已将数据访问代码迁移到单独的存储库类，我们需要修改我们的联系人控制器才能使用此类。 我们将利用一个名为依赖关系注入的软件设计模式，在我们的控制器中使用存储库类。

修改后的联系人控制器包含在列表3中。

**列表 3-Controllers\ContactController.vb**

[!code-vb[Main](iteration-4-make-the-application-loosely-coupled-vb/samples/sample3.vb)]

请注意，列表3中的联系人控制器具有两个构造函数。 第一个构造函数将 IContactManagerRepository 接口的具体实例传递到第二个构造函数。 Contact controller 类使用*构造函数依赖关系注入*。

仅在第一个构造函数中使用 EntityContactManagerRepository 类。 类的其余部分使用 IContactManagerRepository 接口，而不是具体的 EntityContactManagerRepository 类。

这样一来，以后就可以轻松地切换 IContactManagerRepository 类的实现。 如果要使用 DataServicesContactRepository 类而不是 EntityContactManagerRepository 类，只需修改第一个构造函数。

构造函数依赖关系注入还会使 Contact controller 类非常易于测试。 在单元测试中，可以通过传递 IContactManagerRepository 类的 mock 实现来实例化联系人控制器。 当我们为联系人管理器应用程序生成单元测试时，在下一次迭代中，依赖关系注入的这一功能将非常重要。

> [!NOTE] 
> 
> 如果要从 IContactManagerRepository 接口的特定实现完全分离 Contact controller 类，可以利用支持依赖关系注入的框架，如 StructureMap 或 Microsoft实体框架（MEF）。 利用依赖项注入框架，你永远不需要在代码中引用具体的类。

## <a name="creating-a-service-layer"></a>创建服务层

您可能已注意到，验证逻辑仍与列表3的已修改控制器类中的控制器逻辑混合在一起。 由于相同的原因，若要隔离我们的数据访问逻辑，最好隔离验证逻辑。

若要解决此问题，可以创建一个单独的[服务层](http://martinfowler.com/eaaCatalog/serviceLayer.html)。 服务层是一个单独的层，可在控制器和存储库类之间插入。 服务层包含我们的业务逻辑，包括所有验证逻辑。

ContactManagerService 包含在列表4中。 它包含 Contact controller 类的验证逻辑。

**列表 4-Models\ContactManagerService.vb**

[!code-vb[Main](iteration-4-make-the-application-loosely-coupled-vb/samples/sample4.vb)]

请注意，ContactManagerService 的构造函数需要 ValidationDictionary。 服务层通过此 ValidationDictionary 与控制器层通信。 当我们讨论修饰器模式时，我们将在下一节中详细介绍 ValidationDictionary。

另外请注意，ContactManagerService 实现了 IContactManagerService 接口。 应始终努力针对接口而不是具体类进行编程。 联系人管理器应用程序中的其他类不会直接与 ContactManagerService 类交互。 相反，将根据 IContactManagerService 接口对联系人管理器应用程序的其余部分进行编程。

IContactManagerService 接口包含在列表5中。

**列表 5-Models\IContactManagerService.vb**

[!code-vb[Main](iteration-4-make-the-application-loosely-coupled-vb/samples/sample5.vb)]

已修改的 Contact controller 类包含在列表6中。 请注意，联系人控制器不再与 ContactManager 存储库交互。 联系人控制器改为与 ContactManager 服务交互。 每一层尽可能地与其他层隔离。

**列表 6-Controllers\ContactController.vb**

[!code-vb[Main](iteration-4-make-the-application-loosely-coupled-vb/samples/sample6.vb)]

我们的应用程序不再运行单一责任原则（SRP）的落入。 除了控制应用程序的执行流之外，列表6中的联系人控制器已被去除。 所有验证逻辑已从联系人控制器中删除并推送到服务层。 所有数据库逻辑都已推送到存储库层中。

## <a name="using-the-decorator-pattern"></a>使用修饰器模式

我们希望能够从我们的控制器层完全分离我们的服务层。 原则上，我们应该能够在不同的程序集中从我们的控制器层编译我们的服务层，而无需添加对 MVC 应用程序的引用。

但是，我们的服务层需要能够将验证错误消息传回控制器层。 如何使服务层能够在不耦合控制器和服务层的情况下传达验证错误消息？ 我们可以利用名为[修饰器模式](http://en.wikipedia.org/wiki/Decorator_pattern)的软件设计模式。

控制器使用名为 ModelState 的 ModelStateDictionary 来表示验证错误。 因此，你可能想要将 ModelState 从控制器层传递到服务层。 但是，在服务层中使用 ModelState 会使服务层依赖于 ASP.NET MVC 框架的一项功能。 这会是不正确的，因为在将来，你可能想要将服务层用于 WPF 应用程序而不是 ASP.NET MVC 应用程序。 在这种情况下，你不希望引用 ASP.NET MVC 框架来使用 ModelStateDictionary 类。

使用修饰器模式，可以在新类中包装现有类，以便实现接口。 我们的联系人管理器项目包含了包含在列表7中的 ModelStateWrapper 类。 ModelStateWrapper 类在清单8中实现接口。

**列表 7-Models\Validation\ModelStateWrapper.vb**

[!code-vb[Main](iteration-4-make-the-application-loosely-coupled-vb/samples/sample7.vb)]

**列表 8-Models\Validation\IValidationDictionary.vb**

[!code-vb[Main](iteration-4-make-the-application-loosely-coupled-vb/samples/sample8.vb)]

如果你仔细查看列表5，则会看到 ContactManager 服务层专门使用 IValidationDictionary 接口。 ContactManager 服务不依赖于 ModelStateDictionary 类。 当联系人控制器创建 ContactManager 服务时，控制器将包装其 ModelState，如下所示：

[!code-vb[Main](iteration-4-make-the-application-loosely-coupled-vb/samples/sample9.vb)]

## <a name="summary"></a>摘要

在此迭代中，未向联系人管理器应用程序添加任何新功能。 此迭代的目标是重构联系人管理器应用程序，以便更易于维护和修改。

首先，我们实现了存储库软件设计模式。 我们已将所有数据访问代码迁移到单独的 ContactManager 存储库类。

我们还将验证逻辑与控制器逻辑隔离开来。 我们创建了一个包含所有验证代码的单独的服务层。 控制器层与服务层交互，服务层与存储库层交互。

创建服务层时，我们充分利用了修饰器模式，将 ModelState 与我们的服务层隔离开来。 在我们的服务层，我们针对 IValidationDictionary 接口而不是 ModelState 进行了编程。

最后，我们充分利用了名为依赖关系注入模式的软件设计模式。 此模式使我们能够针对接口（抽象）而不是具体的类进行编程。 实现依赖关系注入设计模式还会使代码更易于测试。 在下一次迭代中，我们将向项目中添加单元测试。

> [!div class="step-by-step"]
> [上一页](iteration-3-add-form-validation-vb.md)
> [下一页](iteration-5-create-unit-tests-vb.md)
