---
uid: web-api/overview/testing-and-debugging/mocking-entity-framework-when-unit-testing-aspnet-web-api-2
title: 单元测试 ASP.NET Web API 2 时的模拟实体框架 |Microsoft Docs
author: Rick-Anderson
description: 本指南和应用程序演示如何为使用实体框架的 Web API 2 应用程序创建单元测试。 它演示如何修改 。
ms.author: riande
ms.date: 12/13/2013
ms.assetid: cd844025-ccad-41ce-8694-595f1022a49f
msc.legacyurl: /web-api/overview/testing-and-debugging/mocking-entity-framework-when-unit-testing-aspnet-web-api-2
msc.type: authoredcontent
ms.openlocfilehash: 258450107ee7443c4efd43a3b8e4851249745227
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78447086"
---
# <a name="mocking-entity-framework-when-unit-testing-aspnet-web-api-2"></a>单元测试 ASP.NET Web API 2 时的模拟实体框架

作者： [Tom FitzMacken](https://github.com/tfitzmac)

[下载完成的项目](https://code.msdn.microsoft.com/Unit-Testing-with-ASPNET-1374bc11)

> 本指南和应用程序演示如何为使用实体框架的 Web API 2 应用程序创建单元测试。 它演示如何修改基架控制器以便为测试传递上下文对象，以及如何创建用于实体框架的测试对象。
>
> 有关 ASP.NET Web API 的单元测试的简介，请参阅[使用 ASP.NET Web API 2 的单元测试](unit-testing-with-aspnet-web-api.md)。
>
> 本教程假设你熟悉 ASP.NET Web API 的基本概念。 有关介绍性教程，请参阅[使用 ASP.NET Web API 2 入门](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md)。
>
> ## <a name="software-versions-used-in-the-tutorial"></a>本教程中使用的软件版本
>
> - [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)
> - Web API 2

## <a name="in-this-topic"></a>主题内容

本主题包含以下各节：

- [先决条件](#prereqs)
- [下载代码](#download)
- [创建具有单元测试项目的应用程序](#appwithunittest)
- [创建模型类](#modelclass)
- [添加控制器](#controller)
- [添加依赖关系注入](#dependency)
- [在测试项目中安装 NuGet 包](#testpackages)
- [创建测试上下文](#testcontext)
- [创建测试](#tests)
- [运行测试](#runtests)

如果已[使用 ASP.NET Web API 2 完成单元测试](unit-testing-with-aspnet-web-api.md)中的步骤，则可以跳到[添加控制器](#controller)部分。

<a id="prereqs"></a>
## <a name="prerequisites"></a>系统必备

Visual Studio 2017 社区版、专业版或企业版

<a id="download"></a>
## <a name="download-code"></a>下载代码

下载[完成的项目](https://code.msdn.microsoft.com/Unit-Testing-with-ASPNET-1374bc11)。 可下载的项目包含本主题和[单元测试 ASP.NET Web API 2](unit-testing-with-aspnet-web-api.md)主题的单元测试代码。

<a id="appwithunittest"></a>
## <a name="create-application-with-unit-test-project"></a>创建具有单元测试项目的应用程序

可在创建应用程序时创建单元测试项目，或者将单元测试项目添加到现有应用程序。 本教程演示如何在创建应用程序时创建单元测试项目。

创建名为**StoreApp**的新 ASP.NET Web 应用程序。

在 "新建 ASP.NET 项目" 窗口中，选择 "**空**" 模板，并为 Web API 添加文件夹和核心引用。 选择 "**添加单元测试**" 选项。 单元测试项目被自动命名为**StoreApp**。 您可以保留此名称。

![创建单元测试项目](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image1.png)

创建应用程序后，你将看到它包含两个项目- **StoreApp**和**StoreApp**。

<a id="modelclass"></a>
## <a name="create-the-model-class"></a>创建模型类

在 StoreApp 项目中，将类文件添加到名为**Product.cs**的**模型**文件夹中。 将文件的内容替换为以下代码。

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample1.cs)]

生成解决方案。

<a id="controller"></a>
## <a name="add-the-controller"></a>添加控制器

右键单击 "控制器" 文件夹，然后选择 "**添加**并**新建基架项**"。 使用实体框架选择 "包含操作的 Web API 2 控制器"。

![添加新控制器](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image2.png)

设置下列值：

- 控制器名称： **ProductController**
- Model 类：**产品**
- 数据上下文类： [选择**新的数据上下文**按钮，该按钮可填充下面所示的值]

![指定控制器](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image3.png)

单击 "**添加**" 以创建带有自动生成的代码的控制器。 此代码包括用于创建、检索、更新和删除 Product 类的实例的方法。 下面的代码演示了用于添加产品的方法。 请注意，该方法将返回**IHttpActionResult**的实例。

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample2.cs)]

IHttpActionResult 是 Web API 2 中的一项新功能，它简化了单元测试的开发。

在下一部分中，你将自定义生成的代码，以便将测试对象传递到控制器。

<a id="dependency"></a>
## <a name="add-dependency-injection"></a>添加依赖关系注入

目前，ProductController 类硬编码为使用 StoreAppContext 类的实例。 将使用名为 "依赖关系注入" 的模式来修改应用程序，并删除硬编码的依赖关系。 通过中断此依赖项，你可以在测试时传入 mock 对象。

右键单击 "**模型**" 文件夹，然后添加一个名为**IStoreAppContext**的新接口。

将代码替换为以下代码。

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample3.cs)]

打开 StoreAppContext.cs 文件并进行以下突出显示的更改。 需要注意的重要更改如下：

- StoreAppContext 类实现 IStoreAppContext 接口
- 实现 MarkAsModified 方法

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample4.cs?highlight=6,14-17)]

打开 ProductController.cs 文件。 更改现有代码以匹配突出显示的代码。 这些更改将中断对 StoreAppContext 的依赖关系，并使其他类能够为上下文类传入不同的对象。 此更改将使你可以在单元测试期间传入测试上下文。

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample5.cs?highlight=4,7-12)]

还必须在 ProductController 中进行一项更改。 在**PutProduct**方法中，使用对 MarkAsModified 方法的调用替换设置要修改的实体状态的行。

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample6.cs?highlight=14-15)]

生成解决方案。

你现在已准备好设置测试项目。

<a id="testpackages"></a>
## <a name="install-nuget-packages-in-test-project"></a>在测试项目中安装 NuGet 包

使用空模板创建应用程序时，单元测试项目（StoreApp）不包含任何已安装的 NuGet 包。 其他模板（如 Web API 模板）在单元测试项目中包含一些 NuGet 包。 对于本教程，必须将实体框架包和 Microsoft ASP.NET Web API 2 核心包添加到测试项目。

右键单击 "StoreApp" 项目，然后选择 "**管理 NuGet 包**"。 您必须选择 StoreApp 项目，才能将包添加到该项目中。

![管理包](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image4.png)

在联机包中，查找并安装 EntityFramework 包（版本6.0 或更高版本）。 如果似乎已安装 EntityFramework 包，则可能已选择 StoreApp 项目而不是 StoreApp 项目。

![添加实体框架](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image5.png)

查找并安装 Microsoft ASP.NET Web API 2 核心包。

![安装 web api 核心包](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image6.png)

关闭 "管理 NuGet 包" 窗口。

<a id="testcontext"></a>
## <a name="create-test-context"></a>创建测试上下文

向测试项目添加一个名为**TestDbSet**的类。 此类用作测试数据集的基类。 将代码替换为以下代码。

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample7.cs)]

将名为**TestProductDbSet**的类添加到包含以下代码的测试项目。

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample8.cs)]

添加一个名为**TestStoreAppContext**的类，并将现有代码替换为以下代码。

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample9.cs)]

<a id="tests"></a>
## <a name="create-tests"></a>创建测试

默认情况下，你的测试项目包含一个名为**UnitTest1.cs**的空测试文件。 此文件显示用于创建测试方法的属性。 对于本教程，你可以删除此文件，因为你将添加新的测试类。

向测试项目添加一个名为**TestProductController**的类。 将代码替换为以下代码。

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample10.cs)]

<a id="runtests"></a>
## <a name="run-tests"></a>运行测试

你现在已准备好运行测试。 将测试标记为**TestMethod**属性的所有方法。 从 "**测试**" 菜单项中，运行测试。

![运行测试](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image7.png)

打开 "**测试资源管理器**" 窗口，并注意测试的结果。

![测试结果](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image8.png)
