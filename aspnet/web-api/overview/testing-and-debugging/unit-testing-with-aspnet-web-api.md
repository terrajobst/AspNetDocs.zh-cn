---
uid: web-api/overview/testing-and-debugging/unit-testing-with-aspnet-web-api
title: 单元测试 ASP.NET Web API 2 |Microsoft Docs
author: Rick-Anderson
description: 本指南和应用程序演示了如何为 Web API 2 应用程序创建简单的单元测试。 本教程介绍如何包括单元测试的一 。
ms.author: riande
ms.date: 06/05/2014
ms.assetid: bf20f78d-ff91-48be-abd1-88e23dcc70ba
msc.legacyurl: /web-api/overview/testing-and-debugging/unit-testing-with-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: f2d60b977475e048a3a74aabff4adc768ee22baf
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78446984"
---
# <a name="unit-testing-aspnet-web-api-2"></a>单元测试 ASP.NET Web API 2

作者： [Tom FitzMacken](https://github.com/tfitzmac)

[下载完成的项目](https://code.msdn.microsoft.com/Unit-Testing-with-ASPNET-1374bc11)

> 本指南和应用程序演示了如何为 Web API 2 应用程序创建简单的单元测试。 本教程演示如何在解决方案中包括单元测试项目，并编写用于检查控制器方法返回的值的测试方法。
>
> 本教程假设你熟悉 ASP.NET Web API 的基本概念。 有关介绍性教程，请参阅[使用 ASP.NET Web API 2 入门](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md)。
>
> 本主题中的单元测试有意限制为简单的数据应用场景。 有关更高级数据方案的单元测试，请参阅[单元测试 ASP.NET Web API 2 时的模拟实体框架](mocking-entity-framework-when-unit-testing-aspnet-web-api-2.md)。
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
    - [创建应用程序时添加单元测试项目](#whencreate)
    - [向现有应用程序添加单元测试项目](#addtoexisting)
- [设置 Web API 2 应用程序](#setupproject)
- [在测试项目中安装 NuGet 包](#testpackages)
- [创建测试](#tests)
- [运行测试](#runtests)

<a id="prereqs"></a>
## <a name="prerequisites"></a>系统必备

[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)社区版、专业版或企业版

<a id="download"></a>
## <a name="download-code"></a>下载代码

下载[完成的项目](https://code.msdn.microsoft.com/Unit-Testing-with-ASPNET-1374bc11)。 可下载的项目包含本主题的单元测试代码以及[单元测试 ASP.NET Web API 主题的模拟实体框架](mocking-entity-framework-when-unit-testing-aspnet-web-api-2.md)。

<a id="appwithunittest"></a>
## <a name="create-application-with-unit-test-project"></a>创建具有单元测试项目的应用程序

可在创建应用程序时创建单元测试项目，或者将单元测试项目添加到现有应用程序。 本教程演示创建单元测试项目的两种方法。 若要按照本教程操作，可以使用这两种方法。

<a id="whencreate"></a>
### <a name="add-unit-test-project-when-creating-the-application"></a>创建应用程序时添加单元测试项目

创建名为**StoreApp**的新 ASP.NET Web 应用程序。

![创建项目](unit-testing-with-aspnet-web-api/_static/image1.png)

在 "新建 ASP.NET 项目" 窗口中，选择 "**空**" 模板，并为 Web API 添加文件夹和核心引用。 选择 "**添加单元测试**" 选项。 单元测试项目被自动命名为**StoreApp**。 您可以保留此名称。

![创建单元测试项目](unit-testing-with-aspnet-web-api/_static/image2.png)

创建应用程序后，您将看到它包含两个项目。

![两个项目](unit-testing-with-aspnet-web-api/_static/image3.png)

<a id="addtoexisting"></a>
### <a name="add-unit-test-project-to-an-existing-application"></a>向现有应用程序添加单元测试项目

如果在创建应用程序时未创建单元测试项目，则可以随时添加一个。 例如，假设已有一个名为 StoreApp 的应用程序，并且想要添加单元测试。 若要添加单元测试项目，请右键单击解决方案，然后选择 "**添加**" 和 "**新建项目**"。

![向解决方案添加新项目](unit-testing-with-aspnet-web-api/_static/image4.png)

在左窗格中选择 "**测试**"，然后选择 "**单元测试项目**" 作为 "项目类型"。 将项目命名为**StoreApp**。

![添加单元测试项目](unit-testing-with-aspnet-web-api/_static/image5.png)

你将在你的解决方案中看到该单元测试项目。

在单元测试项目中，添加对原始项目的项目引用。

<a id="setupproject"></a>
## <a name="set-up-the-web-api-2-application"></a>设置 Web API 2 应用程序

在 StoreApp 项目中，将类文件添加到名为**Product.cs**的**模型**文件夹中。 将文件的内容替换为以下代码。

[!code-csharp[Main](unit-testing-with-aspnet-web-api/samples/sample1.cs)]

生成解决方案。

右键单击 "控制器" 文件夹，然后选择 "**添加**并**新建基架项**"。 选择 " **WEB API 2 控制器-空**"。

![添加新控制器](unit-testing-with-aspnet-web-api/_static/image6.png)

将控制器名称设置为**SimpleProductController**，并单击 "**添加**"。

![指定控制器](unit-testing-with-aspnet-web-api/_static/image7.png)

用下面的代码替换现有代码。 为了简化此示例，数据存储在列表中，而不是数据库中。 此类中定义的列表表示生产数据。 请注意，控制器包含一个构造函数，该构造函数采用产品对象列表作为参数。 此构造函数使你能够在单元测试时传递测试数据。 控制器还包括两个**异步**方法，用于说明单元测试的异步方法。 这些异步方法是通过调用**system.threading.tasks.task.fromresult**来实现的，以最大程度地减少无关的代码，但通常情况下，方法会包括消耗大量资源的操作。

[!code-csharp[Main](unit-testing-with-aspnet-web-api/samples/sample2.cs)]

GetProduct 方法返回**IHttpActionResult**接口的实例。 IHttpActionResult 是 Web API 2 中的一项新功能，它简化了单元测试的开发。 [在 IHttpActionResult 命名空间](https://msdn.microsoft.com/library/system.web.http.results.aspx)中找到实现了接口的类。 这些类表示来自操作请求的可能响应，它们对应于 HTTP 状态代码。

生成解决方案。

你现在已准备好设置测试项目。

<a id="testpackages"></a>
## <a name="install-nuget-packages-in-test-project"></a>在测试项目中安装 NuGet 包

使用空模板创建应用程序时，单元测试项目（StoreApp）不包含任何已安装的 NuGet 包。 其他模板（如 Web API 模板）在单元测试项目中包含一些 NuGet 包。 对于本教程，必须将 Microsoft ASP.NET Web API 2 核心包添加到测试项目中。

右键单击 "StoreApp" 项目，然后选择 "**管理 NuGet 包**"。 您必须选择 StoreApp 项目，才能将包添加到该项目中。

![管理包](unit-testing-with-aspnet-web-api/_static/image8.png)

查找并安装 Microsoft ASP.NET Web API 2 核心包。

![安装 web api 核心包](unit-testing-with-aspnet-web-api/_static/image9.png)

关闭 "管理 NuGet 包" 窗口。

<a id="tests"></a>
## <a name="create-tests"></a>创建测试

默认情况下，你的测试项目包含一个名为 UnitTest1.cs 的空测试文件。 此文件显示用于创建测试方法的属性。 对于单元测试，可以使用此文件，也可以创建自己的文件。

![UnitTest1](unit-testing-with-aspnet-web-api/_static/image10.png)

在本教程中，您将创建自己的测试类。 你可以删除 UnitTest1.cs 文件。 添加一个名为**TestSimpleProductController.cs**的类，并将代码替换为以下代码。

[!code-csharp[Main](unit-testing-with-aspnet-web-api/samples/sample3.cs)]

<a id="runtests"></a>
## <a name="run-tests"></a>运行测试

你现在已准备好运行测试。 将测试标记为**TestMethod**属性的所有方法。 从 "**测试**" 菜单项中，运行测试。

![运行测试](unit-testing-with-aspnet-web-api/_static/image11.png)

打开 "**测试资源管理器**" 窗口，并注意测试的结果。

![测试结果](unit-testing-with-aspnet-web-api/_static/image12.png)

## <a name="summary"></a>摘要

您已完成本教程的学习。 本教程中的数据特意进行了简化，以专注于单元测试情况。 有关更高级数据方案的单元测试，请参阅[单元测试 ASP.NET Web API 2 时的模拟实体框架](mocking-entity-framework-when-unit-testing-aspnet-web-api-2.md)。
