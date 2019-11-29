---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/create_the_data_access_layer
title: 创建数据访问层 |Microsoft Docs
author: Erikre
description: 本系列教程将介绍使用 ASP.NET 4.5 构建 ASP.NET Web 窗体应用程序的基础知识，并为我们 Microsoft Visual Studio Express 2013 。
ms.author: riande
ms.date: 09/08/2014
ms.assetid: 0bbf7a6e-d7eb-4091-91e4-fff892777f32
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/create_the_data_access_layer
msc.type: authoredcontent
ms.openlocfilehash: 0fcf050474a57be9ed53ec0783a6d6b7dde2bf4c
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74575748"
---
# <a name="create-the-data-access-layer"></a>创建数据访问层

作者： [Erik Reitan](https://github.com/Erikre)

[下载 Wingtip 玩具示例项目（C#）](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409)或[下载电子书（PDF）](https://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)

> 本系列教程将介绍使用 ASP.NET 4.5 构建 ASP.NET Web 窗体应用程序的基础知识，并为 Web Microsoft Visual Studio Express 2013。 此教程系列附带有[ C#源代码](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409)的 Visual Studio 2013 项目。

本教程介绍如何使用 ASP.NET Web 窗体和实体框架 Code First 从数据库创建、访问和查看数据。 本教程基于前面的 "创建项目" 教程，是 Wingtip 玩具应用商店教程系列的一部分。 完成本教程后，您将生成一组数据访问类，这些类位于项目的 "*模型*" 文件夹中。

## <a name="what-youll-learn"></a>你将学习的内容：

- 如何创建数据模型。
- 如何初始化和播种数据库。
- 如何更新和配置应用程序以支持数据库。

### <a name="these-are-the-features-introduced-in-the-tutorial"></a>这些是教程中引入的功能：

- 实体框架 Code First
- LocalDB
- 数据注释

## <a name="creating-the-data-models"></a>创建数据模型

[实体框架](https://msdn.microsoft.com/data/aa937723)是对象关系映射（ORM）框架。 它使您可以将关系数据作为对象处理，从而消除了通常需要编写的大部分数据访问代码。 使用实体框架，可以使用[LINQ](https://msdn.microsoft.com/library/bb397926.aspx)发出查询，然后将数据作为强类型对象检索和操作。 LINQ 提供了用于查询和更新数据的模式。 使用实体框架使你可以专注于创建应用程序的其余部分，而不是专注于数据访问基础知识。 稍后在本系列教程中，我们将向您演示如何使用数据来填充导航和产品查询。

实体框架支持名为*Code First*的开发模式。 Code First 允许使用类定义数据模型。 类是一种构造，使你能够通过将其他类型、方法和事件的变量组合在一起来创建自己的自定义类型。 您可以将类映射到现有数据库，或使用它们来生成数据库。 在本教程中，您将通过编写数据模型类来创建数据模型。 接下来，您将实体框架从这些新类动态创建数据库。

首先，您将创建为 Web 窗体应用程序定义数据模型的实体类。 然后，将创建一个上下文类，该类用于管理实体类并提供对数据库的数据访问。 你还将创建一个用于填充数据库的初始化表达式类。

### <a name="entity-framework-and-references"></a>实体框架和引用

默认情况下，当你使用**Web 窗体**模板创建新的**ASP.NET Web 应用程序**时，将包含实体框架。 可以安装、卸载实体框架，并将其更新为 NuGet 包。

此 NuGet 包包括项目中的以下**运行时**程序集：

- EntityFramework-实体框架使用的所有常见运行时代码
- EntityFramework –实体框架的 Microsoft SQL Server 提供程序

### <a name="entity-classes"></a>实体类

你创建的用于定义数据架构的类称为实体类。 如果您不熟悉数据库设计，请将实体类视为数据库的表定义。 类中的每个属性指定数据库的表中的列。 这些类提供了面向对象的代码与数据库的关系表结构之间的轻型对象关系接口。

在本教程中，您将添加代表产品和类别的架构的简单实体类。 Products 类将包含每个产品的定义。 Product 类的每个成员的名称将为 `ProductID`、`ProductName`、`Description`、`ImagePath`、`UnitPrice`、`CategoryID`和 `Category`。 Category 类将包含产品可以属于的每个类别的定义，例如汽车、船或飞机。 类别类的每个成员的名称将为 `CategoryID`、`CategoryName`、`Description`和 `Products`。 每个产品都属于某个类别。 这些实体类将添加到项目的现有*模型*文件夹中。

1. 在**解决方案资源管理器**中，右键单击 "*模型*" 文件夹，然后选择 "**添加** -&gt;**新项**"。 

    ![创建数据访问层-新建项菜单](create_the_data_access_layer/_static/image1.png)

   随即出现“添加新项”对话框。
2. 在左侧的 "**已安装**" 窗格中，选择 "**代码**"。 **C#** 

    ![创建数据访问层-新建项菜单](create_the_data_access_layer/_static/image2.png)
3. 从中间窗格中选择 "**类**"，并将此新类命名为*Product.cs*。
4. 单击 **添加**。  
   新的类文件将显示在编辑器中。
5. 将默认代码替换为以下代码：   

    [!code-csharp[Main](create_the_data_access_layer/samples/sample1.cs)]
6. 通过重复步骤1到步骤4创建另一个类，但将新类命名为*Category.cs* ，并将默认代码替换为以下代码：  

    [!code-csharp[Main](create_the_data_access_layer/samples/sample2.cs)]

如前所述，`Category` 类表示应用程序设计用于销售的产品类型（如<a id="a"></a>&quot;轿车&quot;、&quot;Boats&quot;、&quot;Rockets&quot;等），`Product` 类表示数据库中的各个产品（玩具）。 `Product` 对象的每个实例都对应于关系数据库表中的一行，Product 类的每个属性都将映射到关系数据库表中的一个列。 稍后在本教程中，你将查看数据库中包含的产品数据。

### <a name="data-annotations"></a>数据注释

您可能已注意到，类的某些成员具有指定成员详细信息的属性，如 `[ScaffoldColumn(false)]`。 这些是*数据批注*。 数据批注属性可以描述如何验证该成员的用户输入、指定其格式设置，以及指定在创建数据库时如何对其进行建模。

### <a name="context-class"></a>Context 类

若要开始使用类进行数据访问，必须定义一个上下文类。 如前所述，上下文类管理实体类（如 `Product` 类和 `Category` 类）并提供对数据库的数据访问。

此过程将新C#的上下文类添加到 "*模型*" 文件夹。

1. 右键单击 "*模型*" 文件夹，然后选择 "**添加** -&gt;**新项**"。   
   随即出现“添加新项”对话框。
2. 从中间窗格中选择 "**类**"，将其命名为*ProductContext.cs* ，然后单击 "**添加**"。
3. 将类中包含的默认代码替换为以下代码：   

    [!code-csharp[Main](create_the_data_access_layer/samples/sample3.cs)]

此代码将添加 `System.Data.Entity` 命名空间，以便您可以访问实体框架的所有核心功能，其中包括使用强类型对象查询、插入、更新和删除数据的功能。

`ProductContext` 类表示实体框架产品数据库上下文，用于处理数据库中 `Product` 类实例的提取、存储和更新。 `ProductContext` 类从实体框架提供的 `DbContext` 基类派生。

### <a name="initializer-class"></a>初始值设定项类

第一次使用上下文时，需要运行一些自定义逻辑来初始化数据库。 这将允许将种子数据添加到数据库，以便可以立即显示产品和类别。

此过程将新C#的初始值设定项类添加到*模型*文件夹中。

1. 在 "*模型*" 文件夹中创建另一个 `Class`，并将其命名为*ProductDatabaseInitializer.cs*。
2. 将类中包含的默认代码替换为以下代码：   

    [!code-csharp[Main](create_the_data_access_layer/samples/sample4.cs)]

如以上代码所示，在创建和初始化数据库时，将重写并设置 `Seed` 属性。 设置 `Seed` 属性后，将使用类别和产品中的值填充数据库。 如果尝试在创建数据库后通过修改上述代码来更新种子数据，则在运行 Web 应用程序时，将看不到任何更新。 原因是上面的代码使用 `DropCreateDatabaseIfModelChanges` 类的实现来识别模型（架构）是否在重置种子数据之前已更改。 如果没有对 `Category` 和 `Product` 实体类进行更改，则不会用种子数据重新初始化数据库。

> [!NOTE] 
> 
> 如果希望在每次运行应用程序时重新创建数据库，可以使用 `DropCreateDatabaseAlways` 类，而不是 `DropCreateDatabaseIfModelChanges` 类。 但对于本系列教程，请使用 `DropCreateDatabaseIfModelChanges` 类。

此时，在本教程中，您将拥有一个具有四个新类和一个默认类的*模型*文件夹：

![创建数据访问层-模型文件夹](create_the_data_access_layer/_static/image3.png)

### <a name="configuring-the-application-to-use-the-data-model"></a>将应用程序配置为使用数据模型

现在，你已创建表示数据的类，你必须将应用程序配置为使用这些类。 在*global.asax*文件中，您将添加初始化模型的代码。 *在 web.config 文件中*，添加信息，告诉应用程序将用于存储新数据类所表示的数据的数据库。 *Global.asax*文件可用于处理应用程序事件或方法。 Web.config*文件允许*您控制 ASP.NET Web 应用程序的配置。

#### <a name="updating-the-globalasax-file"></a>更新 global.asax 文件

若要在应用程序启动时初始化数据模型，您将更新*Global.asax.cs*文件中的 `Application_Start` 处理程序。

> [!NOTE] 
> 
> 在解决方案资源管理器中，可以选择*global.asax*文件或*Global.asax.cs*文件来编辑*Global.asax.cs*文件。

1. 将以下突出显示的代码添加到*Global.asax.cs*文件中的 `Application_Start` 方法。   

    [!code-csharp[Main](create_the_data_access_layer/samples/sample5.cs?highlight=9-10,22-23)]

> [!NOTE] 
> 
> 浏览器在浏览器中查看此教程系列时，您的浏览器必须支持 HTML5 来查看黄色突出显示的代码。

如上面的代码所示，当应用程序启动时，应用程序会指定第一次访问数据时将运行的初始值设定项。 访问 `Database` 对象和 `ProductDatabaseInitializer` 对象需要使用另外两个命名空间。

 修改 Web.config 文件 

尽管实体框架 Code First 会在使用种子数据填充数据库时在默认位置为你生成数据库，但将你自己的连接信息添加到你的应用程序可以控制数据库位置。 在项目根目录下，使用应用程序的*web.config*文件中的连接字符串指定此数据库连接。 通过添加新的连接字符串，您可以将数据库（*wingtiptoys*）的位置定向到在应用程序的数据目录（*应用程序\_数据*）中生成，而不是在其默认位置。 进行此更改将允许您在本教程的后面查找并检查数据库文件。

1. 在**解决方案资源管理器**中，找到并打开*web.config 文件。*
2. 将以黄色突出显示的连接字符串添加到*web.config 文件的*`<connectionStrings>` 节，如下所示：  

    [!code-xml[Main](create_the_data_access_layer/samples/sample6.xml?highlight=4-7)]

首次运行应用程序时，它将在连接字符串指定的位置生成数据库。 但在运行应用程序之前，让我们先进行构建。

## <a name="building-the-application"></a>生成应用程序

若要确保对 Web 应用程序的所有类和更改都有效，应生成应用程序。

1. 从 "**调试**" 菜单中选择 "**生成 WingtipToys**"。  
 显示 "**输出**" 窗口，如果一切正常，都将看到 "*成功*" 消息。  

    ![创建数据访问层-输出窗口](create_the_data_access_layer/_static/image4.png)

如果遇到错误，请重新检查以上步骤。 "**输出**" 窗口中的信息将指示存在问题的文件，以及文件中需要进行更改的位置。 此信息使你能够确定需要在你的项目中查看和修复上述哪些步骤。

## <a name="summary"></a>总结

在本系列教程中，您已创建了数据模型，并添加了将用于初始化和播种数据库的代码。 您还将应用程序配置为在应用程序运行时使用数据模型。

在下一教程中，你将更新 UI，添加导航，并从数据库中检索数据。 这将导致根据你在本教程中创建的实体类来自动创建数据库。

## <a name="additional-resources"></a>其他资源

[实体框架概述](https://msdn.microsoft.com/library/bb399567.aspx)   
[ADO.NET 实体框架初学者指南](https://msdn.microsoft.com/data/ee712907)   
[实体框架的 Code First 开发](http://www.msteched.com/2010/Europe/DEV212)（视频）   
[Code First 关系流畅 API](https://msdn.microsoft.com/data/hh134698)   
[Code First 数据批注](https://msdn.microsoft.com/data/gg193958)  
[实体框架的工作效率改进](https://blogs.msdn.com/b/efdesign/archive/2010/06/21/productivity-improvements-for-the-entity-framework.aspx?wa=wsignin1.0)

> [!div class="step-by-step"]
> [上一页](create-the-project.md)
> [下一页](ui_and_navigation.md)
