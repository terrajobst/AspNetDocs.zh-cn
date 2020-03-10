---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-2
title: 添加模型和控制器 |Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/16/2014
ms.assetid: 88908ff8-51a9-40eb-931c-a8139128b680
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-2
msc.type: authoredcontent
ms.openlocfilehash: 57dacda421968f341284d89c9a3ad80040c16e25
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78449186"
---
# <a name="add-models-and-controllers"></a>添加模型和控制器

作者： [Mike Wasson](https://github.com/MikeWasson)

[下载完成的项目](https://github.com/MikeWasson/BookService)

在本部分中，您将添加定义数据库实体的模型类。 然后，将添加对这些实体执行 CRUD 操作的 Web API 控制器。

## <a name="add-model-classes"></a>添加模型类

在本教程中，我们将使用 "Code First" 方法实体框架（EF）创建数据库。 通过 Code First，您可以C#编写与数据库表相对应的类，而 EF 会创建数据库。 （有关详细信息，请参阅[实体框架开发方法](https://msdn.microsoft.com/library/ms178359%28v=vs.110%29.aspx#dbfmfcf)。）

首先，我们将域对象定义为 Poco （纯旧 CLR 对象）。 我们将创建以下 Poco：

- 作者
- Book

在解决方案资源管理器中，右键单击 "模型" 文件夹。 选择 "**添加**"，然后选择 "**类**"。 将此类命名为 `Author`。

![](part-2/_static/image1.png)

将 Author.cs 中的所有样本代码替换为以下代码。

[!code-csharp[Main](part-2/samples/sample1.cs)]

添加另一个名为 `Book`的类，其中包含以下代码。

[!code-csharp[Main](part-2/samples/sample2.cs)]

实体框架将使用这些模型创建数据库表。 对于每个模型，`Id` 属性将成为数据库表的主键列。

在 Book 类中，`AuthorId` 定义 `Author` 表中的外键。 （为简单起见，我假定每本书只有一个作者。）Book 类还包含相关 `Author`的导航属性。 可以使用导航属性访问代码中的相关 `Author`。 我在第4部分中详细介绍了导航属性，[处理实体关系](part-4.md)。

## <a name="add-web-api-controllers"></a>添加 Web API 控制器

在本部分中，我们将添加支持 CRUD 操作（创建、读取、更新和删除）的 Web API 控制器。 控制器将使用实体框架与数据库层进行通信。

首先，可以删除文件控制器/ValuesController。 此文件包含一个示例 Web API 控制器，但本教程不需要此文件。

![](part-2/_static/image2.png)

接下来，生成项目。 Web API 基架使用反射查找模型类，因此它需要编译的程序集。

在解决方案资源管理器中，右键单击 "控制器" 文件夹。 选择 "**添加**"，然后选择 "**控制器**"。

![](part-2/_static/image3.png)

在 "**添加基架**" 对话框中，选择 "包含操作的 Web API 2 控制器，使用实体框架"。 单击 **“添加”** 。

![](part-2/_static/image4.png)

在 "**添加控制器**" 对话框中，执行以下操作：

1. 在 "**模型类**" 下拉列表中，选择 `Author` 类。 （如果未在下拉列表中看到它，请确保生成了项目。）
2. 选中 "使用异步控制器操作"。
3. 将控制器名称保留为 &quot;AuthorsController&quot;。
4. 单击 "**数据上下文类**" 旁边的加号（+）按钮。

![](part-2/_static/image5.png)

在 "**新建数据上下文**" 对话框中，保留默认名称，然后单击 "**添加**"。

![](part-2/_static/image6.png)

单击 "**添加**" 以完成 "**添加控制器**" 对话框。 此对话框将两个类添加到项目中：

- `AuthorsController` 定义 Web API 控制器。 控制器实现了客户端用于对作者列表执行 CRUD 操作的 REST API。
- `BookServiceContext` 在运行时管理实体对象，这包括使用数据库中的数据填充对象、更改跟踪以及将数据保存到数据库。 它继承自 `DbContext`。

![](part-2/_static/image7.png)

此时，请重新生成项目。 现在，请执行相同的步骤，为 `Book` 实体添加 API 控制器。 这一次，请选择模型类 `Book`，并为数据上下文类选择现有 `BookServiceContext` 类。 （请勿创建新的数据上下文。）单击 "**添加**" 以添加该控制器。

![](part-2/_static/image8.png)

> [!div class="step-by-step"]
> [上一页](part-1.md)
> [下一页](part-3.md)
