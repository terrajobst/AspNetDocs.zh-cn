---
uid: web-api/overview/mobile-clients/calling-web-api-from-a-windows-phone-8-application
title: 从 Windows Phone 8 应用程序调用 Web API （C#）-ASP.NET 4。x
author: rmcmurray
description: 代码教程：在 ASP.NET 4.x 中创建 ASP.NET Web API 应用程序，该应用程序向 Windows Phone 8 应用程序提供书籍目录。
ms.author: riande
ms.date: 10/09/2013
ms.custom: seoapril2019
ms.assetid: b9775f41-352a-4f82-baa6-23e95b342e20
msc.legacyurl: /web-api/overview/mobile-clients/calling-web-api-from-a-windows-phone-8-application
msc.type: authoredcontent
ms.openlocfilehash: c5da14a6856f551343b6fb14f0aedc659e792f6b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78498212"
---
# <a name="calling-web-api-from-a-windows-phone-8-application-c"></a>从 Windows Phone 8 应用程序调用 Web API (C#)

作者： [Robert mcmurray 有关](https://github.com/rmcmurray)

在本教程中，你将了解如何创建一个完整的端到端方案，该方案包含一个 ASP.NET Web API 应用程序，该方案向 Windows Phone 8 应用程序提供书籍目录。

### <a name="overview"></a>概述

RESTful 服务（如 ASP.NET Web API）通过抽象服务器端和客户端应用程序的体系结构，为开发人员简化了基于 HTTP 的应用程序的创建过程。 Web API 开发人员只需为其应用程序发布必要的 HTTP 方法（例如： GET、POST、PUT、DELETE）和客户端应用程序开发人员只需使用其应用程序所需的 HTTP 方法。

本端到端教程介绍如何使用 Web API 创建以下项目：

- 在[本教程的第一部分](#STEP1)中，你将创建一个 ASP.NET Web API 应用程序，该应用程序支持用于管理书籍目录的所有创建、读取、更新和删除（CRUD）操作。 此应用程序将使用 MSDN 的[示例 XML 文件（books.xml）](https://msdn.microsoft.com/library/windows/desktop/ms762271.aspx) 。
- 在[本教程的第二部分](#STEP2)中，你将创建一个交互式 Windows Phone 8 应用程序，该应用程序从 Web API 应用程序检索数据。

#### <a name="prerequisites"></a>系统必备

- Visual Studio 2013 安装了 Windows Phone 8 SDK
- Windows 8 或更高版本位于安装了 Hyper-v 的64位系统上
- 有关其他要求的列表，请参阅[WINDOWS PHONE SDK 8.0](https://www.microsoft.com/download/details.aspx?id=35471)下载页面上的 "*系统要求*" 部分。

> [!NOTE]
> 如果要在本地系统上测试 Web API 与 Windows Phone 8 项目之间的连接，则需按照将 *[Windows Phone 8 模拟器连接到本地计算机上的 WEB Api 应用程序](https://go.microsoft.com/fwlink/?LinkId=324014)* 一文中的说明设置测试环境。

<a id="STEP1"></a>
### <a name="step-1-creating-the-web-api-bookstore-project"></a>步骤1：创建 Web API 书店项目

本端到端教程的第一步是创建一个支持所有 CRUD 操作的 Web API 项目;请注意，你将在本教程的[第2步](#STEP2)中将 Windows Phone 应用程序项目添加到此解决方案。

1. 打开**Visual Studio 2013**。
2. 依次单击 "**文件**"、"**新建**"、"**项目**"。
3. 显示 "**新建项目**" 对话框时，依次展开 "**已安装**"、"**模板**"、" **C#Visual**" 和 " **Web**"。

   | [![](calling-web-api-from-a-windows-phone-8-application/_static/image2.png)](calling-web-api-from-a-windows-phone-8-application/_static/image1.png) |
   |-----------------------------------------------------------------------------------------------------------------------------------------------------|
   |                                                                单击图像进行扩展                                                                |

4. 突出显示 " **ASP.NET Web 应用程序**"，输入**书店**作为项目名称，然后单击 **"确定"** 。
5. 在 "**新建 ASP.NET 项目**" 对话框出现时，选择 " **Web API** " 模板，然后单击 **"确定"** 。

   | [![](calling-web-api-from-a-windows-phone-8-application/_static/image4.png)](calling-web-api-from-a-windows-phone-8-application/_static/image3.png) |
   |-----------------------------------------------------------------------------------------------------------------------------------------------------|
   |                                                                单击图像进行扩展                                                                |

6. 当 Web API 项目打开时，从项目中删除示例控制器：

    1. 展开 "解决方案资源管理器" 中的 "**控制器**" 文件夹。
    2. 右键单击 " **ValuesController.cs** " 文件，然后单击 "**删除**"。
    3. 系统提示确认删除时，单击 **"确定"** 。
7. 将 XML 数据文件添加到 Web API 项目;此文件包含书店目录的内容：

   1. 在 "解决方案资源管理器" 中右键单击**应用\_Data**文件夹，然后单击 "**添加**"，然后单击 "**新建项**"。
   2. 当显示 "**添加新项**" 对话框时，突出显示**XML 文件**模板。
   3. 将文件命名为**books.xml**，然后单击 "**添加**"。
   4. 打开**books.xml**文件后，将文件中的代码替换为 MSDN 上的示例**books.xml**文件中的 xml： 

       [!code-xml[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample1.xml)]
   5. 保存并关闭该 XML 文件。

8. 将书店模型添加到 Web API 项目;此模型包含书店应用程序的创建、读取、更新和删除（CRUD）逻辑：

   1. 在 "解决方案资源管理器" 中，右键单击 "**模型**" 文件夹，单击 "**添加**"，然后单击 "**类**"。
   2. 显示 "**添加新项**" 对话框时，将类文件命名为 " **BookDetails.cs**"，然后单击 "**添加**"。
   3. 打开**BookDetails.cs**文件时，将文件中的代码替换为以下代码： 

       [!code-csharp[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample2.cs)]
   4. 保存并关闭**BookDetails.cs**文件。

9. 将书店控制器添加到 Web API 项目：

   1. 右键单击 "解决方案资源管理器" 中的 "**控制器**" 文件夹，然后单击 "**添加**"，然后单击 "**控制器**"。
   2. 显示 "**添加基架**" 对话框时，突出显示 " **Web API 2 控制器-空**"，然后单击 "**添加**"。
   3. 显示 "**添加控制器**" 对话框后，将控制器命名为 " **BooksController**"，然后单击 "**添加**"。
   4. 打开**BooksController.cs**文件时，将文件中的代码替换为以下代码： 

       [!code-csharp[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample3.cs)]
   5. 保存并关闭**BooksController.cs**文件。

10. 生成 Web API 应用程序以检查是否有错误。

<a id="STEP2"></a>
### <a name="step-2-adding-the-windows-phone-8-bookstore-catalog-project"></a>步骤2：添加 Windows Phone 8 书店目录项目

此端到端方案的下一步是为 Windows Phone 8 创建目录应用程序。 此应用程序将使用默认用户界面的*Windows Phone 数据绑定应用*程序模板，它将使用在本教程的[第1步](#STEP1)中创建的 Web API 应用程序作为数据源。

1. 右键单击 "解决方案资源管理器" 中的 "**书店**解决方案"，然后依次单击 "**添加**" 和 "**新建项目**"。
2. 显示 "**新建项目**" 对话框时，依次展开 "**已安装**" 和 " **C#Visual**"，然后**Windows Phone**"。
3. 突出显示**Windows Phone 的数据绑定应用程序**，输入 " **BookCatalog** " 作为名称，然后单击 **"确定"** 。
4. 将 Json.NET NuGet 包添加到**BookCatalog**项目：

    1. 在 "解决方案资源管理器" 中，右键单击**BookCatalog**项目的 "**引用**"，然后单击 "**管理 NuGet 包**"。
    2. 当显示 "**管理 NuGet 包**" 对话框时，展开 "**联机**" 部分，然后突出显示 " **nuget.org**"。
    3. 在搜索字段中输入**Json.NET** ，然后单击搜索图标。
    4. 突出显示搜索结果中的**Json.NET** ，然后单击 "**安装**"。
    5. 安装完成后，单击 "**关闭**"。
5. 将**BookDetails**模型添加到**BookCatalog**项目;这包含书店类的通用模型：

   1. 右键单击解决方案资源管理器中的**BookCatalog**项目，然后单击 "**添加**"，然后单击 "**新建文件夹**"。
   2. 命名新文件夹**模型**。
   3. 在 "解决方案资源管理器" 中，右键单击 "**模型**" 文件夹，单击 "**添加**"，然后单击 "**类**"。
   4. 显示 "**添加新项**" 对话框时，将类文件命名为 " **BookDetails.cs**"，然后单击 "**添加**"。
   5. 打开**BookDetails.cs**文件时，将文件中的代码替换为以下代码： 

       [!code-csharp[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample4.cs)]
   6. 保存并关闭**BookDetails.cs**文件。

6. 更新**MainViewModel.cs**类，使其包含与书店 Web API 应用程序通信的功能：

   1. 展开 "解决方案资源管理器" 中的**viewmodel**文件夹，然后双击**MainViewModel.cs**文件。
   2. 在打开**MainViewModel.cs**文件时，将文件中的代码替换为以下代码：请注意，需要将 `apiUrl` 常量的值更新为你的 Web API 的实际 URL： 

       [!code-csharp[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample5.cs)]
   3. 保存并关闭**MainViewModel.cs**文件。

7. 更新**MainPage**文件以自定义应用程序名称：

   1. 双击 "解决方案资源管理器" 中的**MainPage**文件。
   2. 在打开**MainPage**文件时，找到以下代码行： 

       [!code-xml[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample6.xml)]
   3. 将这些行替换为以下内容： 

       [!code-xml[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample7.xml)]
   4. 保存并关闭**MainPage**文件。

8. 更新**DetailsPage**文件以自定义显示的项：

   1. 双击 "解决方案资源管理器" 中的**DetailsPage**文件。
   2. 在打开**DetailsPage**文件时，找到以下代码行： 

       [!code-xml[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample8.xml)]
   3. 将这些行替换为以下内容： 

       [!code-xml[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample9.xml)]
   4. 保存并关闭**DetailsPage**文件。

9. 构建 Windows Phone 应用程序以检查是否有错误。

### <a name="step-3-testing-the-end-to-end-solution"></a>步骤3：测试端到端解决方案

如本教程的 "*先决条件*" 部分中所述，当你在本地系统上测试 Web API 与 Windows Phone 8 项目之间的连接时，你将需要按照将 *[Windows Phone 8 仿真程序连接到本地计算机上的 Web api 应用程序](https://go.microsoft.com/fwlink/?LinkId=324014)* 一文中的说明设置你的测试环境。

配置测试环境后，需要将 Windows Phone 应用程序设置为启动项目。 为此，请在 "解决方案资源管理器" 中突出显示**BookCatalog**应用程序，然后单击 "**设为启动项目**"：

| [![](calling-web-api-from-a-windows-phone-8-application/_static/image6.png)](calling-web-api-from-a-windows-phone-8-application/_static/image5.png) |
| --- |
| 单击图像进行扩展 |

按 F5 时，Visual Studio 将启动 Windows Phone 模拟器，这将显示 &quot;请等待&quot; 消息，同时从 Web API 检索应用程序数据：

| [![](calling-web-api-from-a-windows-phone-8-application/_static/image8.png)](calling-web-api-from-a-windows-phone-8-application/_static/image7.png) |
| --- |
| 单击图像进行扩展 |

如果一切成功，应会看到目录显示：

| [![](calling-web-api-from-a-windows-phone-8-application/_static/image10.png)](calling-web-api-from-a-windows-phone-8-application/_static/image9.png) |
| --- |
| 单击图像进行扩展 |

如果点击任何书籍标题，应用程序会显示书籍说明：

| [![](calling-web-api-from-a-windows-phone-8-application/_static/image12.png)](calling-web-api-from-a-windows-phone-8-application/_static/image11.png) |
| --- |
| 单击图像进行扩展 |

如果应用程序无法与 Web API 通信，则将显示一条错误消息：

| [![](calling-web-api-from-a-windows-phone-8-application/_static/image14.png)](calling-web-api-from-a-windows-phone-8-application/_static/image13.png) |
| --- |
| 单击图像进行扩展 |

如果点击错误消息，将显示有关错误的任何其他详细信息：

| [![](calling-web-api-from-a-windows-phone-8-application/_static/image16.png)](calling-web-api-from-a-windows-phone-8-application/_static/image15.png) |
|-------------------------------------------------------------------------------------------------------------------------------------------------------|
|                                                                 单击图像进行扩展                                                                 |
