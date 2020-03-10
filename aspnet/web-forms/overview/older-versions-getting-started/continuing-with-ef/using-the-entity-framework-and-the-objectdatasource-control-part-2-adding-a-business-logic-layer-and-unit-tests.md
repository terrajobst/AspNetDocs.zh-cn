---
uid: web-forms/overview/older-versions-getting-started/continuing-with-ef/using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests
title: 使用实体框架4.0 和 ObjectDataSource 控件，第2部分：添加业务逻辑层和单元测试 |Microsoft Docs
author: tdykstra
description: 本教程系列在使用实体框架4.0 教程系列的入门创建的 Contoso 大学 web 应用程序上构建。 I...
ms.author: riande
ms.date: 01/26/2011
ms.assetid: efb0e677-10b8-48dc-93d3-9ba3902dd807
msc.legacyurl: /web-forms/overview/older-versions-getting-started/continuing-with-ef/using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests
msc.type: authoredcontent
ms.openlocfilehash: 24344cc33d7c26d7c408db26c0530ef2c708a7d3
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78439952"
---
# <a name="using-the-entity-framework-40-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests"></a>使用实体框架4.0 和 ObjectDataSource 控件，第2部分：添加业务逻辑层和单元测试

作者： [Tom Dykstra](https://github.com/tdykstra)

> 本教程系列在[使用实体框架 4.0](https://asp.net/entity-framework/tutorials#Getting%20Started)教程系列的入门创建的 Contoso 大学 web 应用程序上构建。 如果你没有完成前面的教程，作为本教程的起点，你可以下载你要创建[的应用程序](https://code.msdn.microsoft.com/ASPNET-Web-Forms-97f8ee9a)。 你还可以下载完整的系列教程创建的[应用程序](https://code.msdn.microsoft.com/ASPNET-Web-Forms-6c7197aa)。 如果有关于这些教程的问题，可以将其发布到[ASP.NET 实体框架论坛](https://forums.asp.net/1227.aspx)。

在上一教程中，你使用实体框架和 `ObjectDataSource` 控件创建了一个 n 层 web 应用程序。 本教程介绍如何在保持业务逻辑层（BLL）和数据访问层（DAL）的同时添加业务逻辑，并说明如何为 BLL 创建自动单元测试。

在本教程中，你将完成以下任务：

- 创建一个存储库接口，用于声明所需的数据访问方法。
- 在存储库类中实现存储库接口。
- 创建一个业务逻辑类，该类调用存储库类来执行数据访问函数。
- 将 `ObjectDataSource` 控件连接到业务逻辑类，而不是存储库类。
- 创建单元测试项目，并使用内存中集合的数据存储区。
- 为想要添加到业务逻辑类的业务逻辑创建单元测试，然后运行测试并查看其失败。
- 在业务逻辑类中实现业务逻辑，然后重新运行单元测试并查看它是否通过。

你将使用在上一教程中创建的*DepartmentsAdd 和 .aspx*页。

## <a name="creating-a-repository-interface"></a>创建存储库接口

首先，你将创建存储库接口。

[![Image08](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image2.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image1.png)

在*DAL*文件夹中，创建一个新的类文件，将其命名为*ISchoolRepository.cs*，并将现有代码替换为以下代码：

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample1.cs)]

接口为你在存储库类中创建的每个 CRUD （创建、读取、更新、删除）方法定义一个方法。

在*SchoolRepository.cs*中的 `SchoolRepository` 类中，指示此类实现 `ISchoolRepository` 接口：

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample2.cs)]

## <a name="creating-a-business-logic-class"></a>创建业务逻辑类

接下来，您将创建业务逻辑类。 这样做的目的是为了能够添加将由 `ObjectDataSource` 控件执行的业务逻辑，不过您还不会这样做。 现在，新的业务逻辑类将仅执行存储库所执行的相同 CRUD 操作。

[![Image09](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image4.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image3.png)

创建一个新文件夹并将其命名为*BLL*。 （在实际应用程序中，业务逻辑层通常将作为一个类库实现，而不是一个单独的项目，但为了简化本教程，将在项目文件夹中保留 BLL 类。）

在*BLL*文件夹中，创建一个新的类文件，将其命名为*SchoolBL.cs*，并将现有代码替换为以下代码：

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample3.cs)]

此代码将创建你在存储库类前面看到的相同 CRUD 方法，但不直接访问实体框架方法，而是调用存储库类方法。

保存对存储库类的引用的类变量定义为接口类型，而实例化存储库类的代码包含在两个构造函数中。 `ObjectDataSource` 控件将使用无参数的构造函数。 它创建之前创建的 `SchoolRepository` 类的实例。 另一个构造函数允许对业务逻辑类进行实例化的任何代码传递到实现存储库接口的任何对象。

通过调用存储库类和两个构造函数的 CRUD 方法，可以将业务逻辑类用于所选的任何后端数据存储。 业务逻辑类无需知道它所调用的类如何持久保存数据。 （这通常称为*持久性无感知*。）这可以简化单元测试，因为可以将业务逻辑类连接到存储库实现，该实现使用与内存中 `List` 集合一样简单的内容来存储数据。

> [!NOTE]
> 从技术上讲，实体对象仍然不是持久性未知的，因为它们是从从实体框架的 `EntityObject` 类继承的类实例化的。 对于完整的持久性无感知，可以使用*普通的旧 CLR 对象*或*poco*来代替从 `EntityObject` 类继承的对象。 使用 Poco 超出了本教程的范围。 有关详细信息，请参阅 MSDN 网站上的可[测试性和实体框架 4.0](https://msdn.microsoft.com/library/ff714955.aspx) 。）

现在，你可以将 `ObjectDataSource` 控件连接到业务逻辑类，而不是连接到存储库，并验证所有内容是否像以前一样正常工作。

在 *.aspx*和*DepartmentsAdd*中，将 `TypeName="ContosoUniversity.DAL.SchoolRepository"` 的每个匹配项更改 `TypeName="ContosoUniversity.BLL.SchoolBL`"。 （共有四个实例。）

运行 "node.js" 和 " *DepartmentsAdd* "*页，验证*它们是否仍像以前一样工作。

[![Image01](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image6.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image5.png)

[![Image02](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image8.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image7.png)

## <a name="creating-a-unit-test-project-and-repository-implementation"></a>创建单元测试项目和存储库实现

使用 "**测试项目**" 模板将新项目添加到解决方案，并将其命名为 `ContosoUniversity.Tests`。

在测试项目中，添加对 `System.Data.Entity` 的引用并将项目引用添加到 `ContosoUniversity` 项目。

你现在可以创建将用于单元测试的存储库类。 此存储库的数据存储将位于类中。

[![Image12](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image10.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image9.png)

在测试项目中，创建一个新的类文件，将其命名为*MockSchoolRepository.cs*，并将现有代码替换为以下代码：

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample4.cs)]

此存储库类具有与直接访问实体框架相同的 CRUD 方法，但它们使用的是内存中 `List` 集合，而不是与数据库一起使用。 这使得测试类可以更轻松地设置和验证业务逻辑类的单元测试。

## <a name="creating-unit-tests"></a>创建单元测试

**测试**项目模板为你创建了一个存根单元测试类，下一个任务是通过为要添加到业务逻辑类的业务逻辑添加单元测试方法来修改此类。

[![Image13](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image12.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image11.png)

在 Contoso 大学，任何单个指导员只能成为单个部门的管理员，并且你需要添加业务逻辑来强制实施此规则。 首先添加测试并运行测试，以查看它们是否失败。 然后，你将添加代码并重新运行测试，并希望其通过。

打开*UnitTest1.cs*文件并添加在 ContosoUniversity 项目中创建的业务逻辑和数据访问层的 `using` 语句：

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample5.cs)]

将 `TestMethod1` 方法替换为以下方法：

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample6.cs)]

`CreateSchoolBL` 方法创建为单元测试项目创建的存储库类的实例，然后将该实例传递给业务逻辑类的新实例。 然后，方法使用业务逻辑类插入三个可以在测试方法中使用的部门。

如果有人尝试插入具有与现有部门相同的管理员的新部门，或者如果有人尝试通过将其设置为人员的 ID 来更新部门的管理员，则测试方法将验证业务逻辑类是否引发异常。谁已是另一个部门的管理员。

尚未创建异常类，因此此代码将不会编译。 若要进行编译，请右键单击 `DuplicateAdministratorException`，然后选择 "**生成**"，然后选择 "**类**"。

[![Image14](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image14.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image13.png)

这会在测试项目中创建一个可在主项目中创建异常类后删除的类。 和实现业务逻辑。

运行测试项目。 如预期那样，测试将失败。

[![Image03](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image16.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image15.png)

## <a name="adding-business-logic-to-make-a-test-pass"></a>添加业务逻辑以便进行测试

接下来，你将实现业务逻辑，使其不能被设置为属于另一部门的管理员的部门的管理员。 如果用户编辑部门并在选择已成为管理员的人员后单击 "**更新**"，则将从业务逻辑层引发异常，然后在表示层中捕获该异常。 （您也可以从下拉列表中删除已在您呈现页面之前已经是管理员的指导员，但此处的目的是使用业务逻辑层。）

首先，创建一个异常类，当用户尝试使讲师成为多个部门的管理员时，将引发该异常类。 在主项目中，在*BLL*文件夹中创建一个新的类文件，将其命名为*DuplicateAdministratorException.cs*，并将现有代码替换为以下代码：

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample7.cs)]

现在删除之前在测试项目中创建的临时*DuplicateAdministratorException.cs*文件，以便能够进行编译。

在主项目中，打开*SchoolBL.cs*文件并添加以下包含验证逻辑的方法。 （代码引用稍后将创建的方法。）

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample8.cs)]

在插入或更新 `Department` 实体时，将调用此方法，以检查其他部门是否已具有相同的管理员。

此代码将调用一个方法，以便在数据库中搜索与要插入或更新的实体具有相同 `Administrator` 属性值的 `Department` 实体。 如果找到一个，代码将引发异常。 如果要插入或更新的实体没有 `Administrator` 值，则不需要验证检查; 如果在更新过程中调用方法，则不会引发异常，并且找到的 `Department` 实体与正在更新的 `Department` 实体匹配。

从 `Insert` 和 `Update` 方法中调用新方法：

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample9.cs)]

在*ISchoolRepository.cs*中，为新的数据访问方法添加以下声明：

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample10.cs)]

在*SchoolRepository.cs*中，添加以下 `using` 语句：

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample11.cs)]

在*SchoolRepository.cs*中，添加以下新的数据访问方法：

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample12.cs)]

此代码检索具有指定管理员 `Department` 实体。 只应找到一个部门（如果有）。 但是，由于数据库中没有内置的约束，因此在找到多个部门的情况下，返回类型是一个集合。

默认情况下，当对象上下文从数据库中检索实体时，它将在其对象状态管理器中进行跟踪。 `MergeOption.NoTracking` 参数指定不会对此查询执行此跟踪。 这是必需的，因为查询可能返回您尝试更新的确切实体，然后您将无法附加该实体。 例如，如果在 " *default.aspx* " 页中编辑历史记录部门并使管理员保持不变，则此查询将返回历史记录部门。 如果未设置 `NoTracking`，则对象上下文的对象状态管理器中已包含 "历史记录部门" 实体。 然后，在附加从视图状态重新创建的历史部门实体时，对象上下文将引发指出 `"An object with the same key already exists in the ObjectStateManager. The ObjectStateManager cannot track multiple objects with the same key"`的异常。

（作为指定 `MergeOption.NoTracking`的替代方法，您可以为此查询创建一个新的对象上下文。 由于新的对象上下文会有自己的对象状态管理器，因此在调用 `Attach` 方法时，不会发生冲突。 新的对象上下文将与原始对象上下文共享元数据和数据库连接，因此这种替代方法的性能损失会很小。 但此处显示的方法引入了 `NoTracking` 选项，你会在其他上下文中找到该选项。 本系列后面的教程进一步讨论了 `NoTracking` 选项。）

在测试项目中，将新的数据访问方法添加到*MockSchoolRepository.cs*：

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample13.cs)]

此代码使用 LINQ 执行 `ContosoUniversity` 的项目存储库使用 LINQ to Entities 的相同数据选择。

再次运行测试项目。 这次测试通过了。

[![Image04](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image18.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image17.png)

## <a name="handling-objectdatasource-exceptions"></a>处理 ObjectDataSource 异常

在 `ContosoUniversity` 项目中，运行 "node.js *" 页，* 然后尝试将某个部门的管理员更改为已是另一个部门的管理员的用户。 （请记住，您只能编辑您在本教程中添加的部门，因为数据库预加载了无效的数据。）出现以下服务器错误页：

[![Image05](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image20.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image19.png)

您不希望用户看到此类错误页面，因此您需要添加错误处理代码。 打开 "*部门*"，并为 `DepartmentsObjectDataSource`的 `OnUpdated` 事件指定处理程序。 `ObjectDataSource` 开始标记现在类似于以下示例。

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample14.aspx)]

在*Departments.aspx.cs*中，添加以下 `using` 语句：

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample15.cs)]

为 `Updated` 事件添加以下处理程序：

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample16.cs)]

如果 `ObjectDataSource` 控件在尝试执行更新时捕获到异常，则它会将事件自变量（`e`）中的异常传递给该处理程序。 处理程序中的代码检查异常是否是重复的管理员异常。 如果是，该代码将创建一个验证程序控件，其中包含要显示的 `ValidationSummary` 控件的错误消息。

运行该页并再次尝试让两个部门的管理员。 这次 `ValidationSummary` 控件将显示错误消息。

[![Image06](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image22.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image21.png)

对*DepartmentsAdd*页进行类似的更改。 在*DepartmentsAdd*中，为 `DepartmentsObjectDataSource`的 `OnInserted` 事件指定处理程序。 生成的标记将类似于下面的示例。

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample17.aspx)]

在*DepartmentsAdd.aspx.cs*中，添加相同的 `using` 语句：

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample18.cs)]

添加以下事件处理程序：

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample19.cs)]

你现在可以测试*DepartmentsAdd.aspx.cs*页，验证它是否还正确地处理使一个用户成为多个部门的管理员的尝试。

这就完成了实现使用实体框架的 `ObjectDataSource` 控件的存储库模式的简介。 有关存储库模式和可测试性的详细信息，请参阅 MSDN 白皮书可[测试性和4.0 实体框架](https://msdn.microsoft.com/library/ff714955.aspx)。

在以下教程中，你将了解如何将排序和筛选功能添加到应用程序。

> [!div class="step-by-step"]
> [上一页](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started.md)
> [下一页](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering.md)
