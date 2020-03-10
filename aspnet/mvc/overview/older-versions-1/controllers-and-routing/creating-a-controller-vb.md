---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-a-controller-vb
title: 创建控制器（VB） |Microsoft Docs
author: StephenWalther
description: 在本教程中，Stephen Walther 演示了如何将控制器添加到 ASP.NET MVC 应用程序。
ms.author: riande
ms.date: 03/02/2009
ms.assetid: 204b7e86-f560-4611-8adb-785b33e777b9
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-a-controller-vb
msc.type: authoredcontent
ms.openlocfilehash: 60636b79ab5fc06ca904dee90ce74f256e046d12
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78486830"
---
# <a name="creating-a-controller-vb"></a>创建控制器 (VB)

作者： [Stephen Walther](https://github.com/StephenWalther)

> 在本教程中，Stephen Walther 演示了如何将控制器添加到 ASP.NET MVC 应用程序。

本教程的目的是介绍如何创建新的 ASP.NET MVC 控制器。 了解如何使用 Visual Studio 的 "添加控制器" 菜单选项和手动创建类文件来创建控制器。

### <a name="using-the-add-controller-menu-option"></a>使用 "添加控制器" 菜单选项

若要创建新的控制器，最简单的方法是在 Visual Studio 解决方案资源管理器窗口中右键单击 "控制器" 文件夹，然后选择 "**添加"、"控制器**" 菜单选项（参见图1）。 选择此菜单选项将打开 "**添加控制器**" 对话框（参见图2）。

[!["新建项目" 对话框](creating-a-controller-vb/_static/image1.jpg)](creating-a-controller-vb/_static/image1.png)

**图 01**：添加新控制器（[单击以查看完全大小的映像](creating-a-controller-vb/_static/image2.png)）

[!["新建项目" 对话框](creating-a-controller-vb/_static/image2.jpg)](creating-a-controller-vb/_static/image3.png)

**图 02**： "添加控制器" 对话框（[单击以查看完全大小的映像](creating-a-controller-vb/_static/image4.png)）

请注意，控制器名称的第一部分在 "**添加控制器**" 对话框中突出显示。 每个控制器名称必须以后缀*控制器*结尾。 例如，可以创建名为*ProductController*的控制器，而不是名为*Product*的控制器。

如果创建的控制器缺少*控制器*后缀，则无法调用该控制器。 不要这样做-在进行此错误后，我还浪费了无数小时的生活。

**列表 1-Controllers\ProductController.vb**

[!code-vb[Main](creating-a-controller-vb/samples/sample1.vb)]

应始终在 "控制器" 文件夹中创建控制器。 否则，你将违反 ASP.NET MVC 的约定，其他开发人员将会更难理解你的应用程序。

### <a name="scaffolding-action-methods"></a>基架操作方法

创建控制器时，可以选择自动生成创建、更新和详细信息操作方法（请参阅图3）。 如果选择此选项，则生成清单2中的控制器类。

[![自动创建操作方法](creating-a-controller-vb/_static/image3.jpg)](creating-a-controller-vb/_static/image5.png)

**图 03**：自动创建操作方法（[单击以查看完全大小的图像](creating-a-controller-vb/_static/image6.png)）

**列表 2-Controllers\CustomerController.vb**

[!code-vb[Main](creating-a-controller-vb/samples/sample2.vb)]

这些生成的方法是存根方法。 您必须添加用于创建、更新和显示客户的详细信息的实际逻辑。 但存根方法为您提供了一个很好的起点。

### <a name="creating-a-controller-class"></a>创建控制器类

ASP.NET MVC 控制器只是一个类。 如果愿意，可以忽略便利的 Visual Studio 控制器基架，手动创建控制器类。 请执行这些步骤：

1. 右键单击 "控制器" 文件夹，然后选择菜单选项 "**添加"、"新建项**"，然后选择**类**模板（请参阅图4）。
2. 将新类命名为 PersonController，然后单击 "**添加**" 按钮。
3. 修改生成的类文件，使该类继承自基 System.web 类（请参阅列表3）。

[![创建新类](creating-a-controller-vb/_static/image4.jpg)](creating-a-controller-vb/_static/image7.png)

**图 04**：创建新类（[单击以查看完全大小的映像](creating-a-controller-vb/_static/image8.png)）

**列表 3-Controllers\PersonController.vb**

[!code-vb[Main](creating-a-controller-vb/samples/sample3.vb)]

列表3中的控制器公开一个名为 Index （）的操作，该操作返回字符串 "Hello World！"。 您可以通过运行您的应用程序并请求如下 URL 来调用此控制器操作：

`http://localhost:40071/Person`

> [!NOTE]
> 
> ASP.NET 开发服务器使用随机端口号（例如，40071）。 输入用于调用控制器的 URL 时，需要提供正确的端口号。 可以通过将鼠标悬停在 Windows 通知区域（屏幕右下角）的 ASP.NET 开发服务器图标上来确定端口号。
> 
> [!div class="step-by-step"]
> [上一页](adding-dynamic-content-to-a-cached-page-vb.md)
> [下一页](creating-an-action-vb.md)
