---
uid: web-forms/overview/ajax-control-toolkit/getting-started/creating-a-custom-ajax-control-toolkit-control-extender-vb
title: 创建自定义 AJAX 控件工具包控件扩展程序（VB） |Microsoft Docs
author: microsoft
description: 自定义扩展程序使你可以自定义和扩展 ASP.NET 控件的功能，而无需创建新类。
ms.author: riande
ms.date: 05/12/2009
ms.assetid: 18b29834-c991-4e0c-b533-44d358fbfc9c
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/getting-started/creating-a-custom-ajax-control-toolkit-control-extender-vb
msc.type: authoredcontent
ms.openlocfilehash: 0849fa6c13679e0cd01bb20a4067a097acbce298
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78466862"
---
# <a name="creating-a-custom-ajax-control-toolkit-control-extender-vb"></a>创建自定义 AJAX 控件工具包控件扩展程序 (VB)

由[Microsoft](https://github.com/microsoft)

> 自定义扩展程序使你可以自定义和扩展 ASP.NET 控件的功能，而无需创建新类。

在本教程中，将了解如何创建自定义 AJAX 控件工具包控件扩展器。 我们创建了一个简单但有用的新扩展器，该扩展程序将按钮的状态从 "已禁用" 更改为 "已启用"，以便在文本框中键入文本。 阅读本教程后，你将能够用自己的控件扩展器扩展 ASP.NET AJAX 工具包。

你可以使用 Visual Studio 或 Visual Web Developer 创建自定义控件扩展器（确保具有最新版本的 Visual Web Developer）。

## <a name="overview-of-the-disabledbutton-extender"></a>DisabledButton 扩展器概述

新的控件扩展器命名为 DisabledButton 扩展器。 此扩展器将有三个属性：

- TargetControlID-控件扩展的文本框。
- TargetButtonIID-已禁用或已启用的按钮。
- DisabledText-按钮中最初显示的文本。 开始键入时，按钮会显示 "按钮文本" 属性的值。

将 DisabledButton 扩展器挂钩到 TextBox 和 Button 控件。 键入任何文本之前，按钮将被禁用，文本框和按钮如下所示：

[![](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image2.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image1.png)

（[单击以查看完全大小的映像](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image3.png)）

开始键入文本后，按钮将启用，文本框和按钮如下所示：

[![](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image5.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image4.png)

（[单击以查看完全大小的映像](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image6.png)）

若要创建控件扩展器，需要创建以下三个文件：

- DisabledButtonExtender-此文件是服务器端控件类，它将管理创建扩展器，并允许您在设计时设置属性。 它还定义了可在扩展器上设置的属性。 这些属性可通过代码和设计时访问，并与 DisableButtonBehavior 文件中定义的属性相匹配。
- DisabledButtonBehavior-此文件是你将在其中添加所有客户端脚本逻辑的位置。
- DisabledButtonDesigner-此类启用设计时功能。 如果希望控件扩展器能够正常使用 Visual Studio/Visual Web Developer 设计器，则需要此类。

因此，控件扩展器由服务器端控件、客户端行为和服务器端设计器类组成。 你将在以下部分中了解如何创建这三个文件。

## <a name="creating-the-custom-extender-website-and-project"></a>创建自定义扩展器网站和项目

第一步是在 Visual Studio/Visual Web Developer 中创建类库项目和网站。 我们将在类库项目中创建自定义扩展器，并测试网站中的自定义扩展器。

让我们从网站开始。 按照以下步骤创建网站：

1. 选择菜单选项 "**文件" "新建**网站"。
2. 选择**ASP.NET**网站模板。
3. 将新网站命名为 " *Website1*"。
4. 单击“确定”按钮。

接下来，我们需要创建一个类库项目，该项目将包含控件扩展程序的代码：

1. 选择菜单选项**文件 "添加" "新建项目**"。
2. 选择 "**类库**" 模板。
3. 将名为**CustomExtenders**的新类库命名为。
4. 单击“确定”按钮。

完成这些步骤后，"解决方案资源管理器" 窗口应如图1所示。

[![包含网站和类库项目的解决方案](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image8.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image7.png)

**图 01**：包含网站和类库项目的解决方案（[单击以查看完全大小的图像](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image9.png)）

接下来，需要将所有必需的程序集引用添加到类库项目中：

1. 右键单击 "CustomExtenders" 项目，然后选择 "**添加引用**" 菜单选项。
2. 选择 .NET 选项卡。
3. 添加对下列程序集的引用：

    1. System.Web.dll
    2. System.Web.Extensions.dll
    3. System.Design.dll
    4. System.Web.Extensions.Design.dll
4. 选择 "浏览" 选项卡。
5. 添加对 AjaxControlToolkit 程序集的引用。 此程序集位于下载 AJAX 控件工具包的文件夹中。

可以通过右键单击项目，选择 "属性"，然后单击 "引用" 选项卡，验证是否已添加了所有正确的引用（请参阅图2）。

[![引用具有所需引用的文件夹](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image11.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image10.png)

**图 02**：引用具有所需引用的文件夹（[单击查看完全大小的图像](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image12.png)）

## <a name="creating-the-custom-control-extender"></a>创建自定义控件扩展器

现在我们有了类库，接下来我们可以开始构建扩展器控件。 让我们从自定义扩展程序控件类的 bare 骨骼开始（请参阅列表1）。

**列表 1-MyCustomExtender**

[!code-vb[Main](creating-a-custom-ajax-control-toolkit-control-extender-vb/samples/sample1.vb)]

有关列表1中的控件扩展器类，有几个方面需要注意。 首先，请注意该类继承自基 ExtenderControlBase 类。 所有 AJAX 控件工具包扩展程序控件都从此基类派生。 例如，基类包含 TargetID 属性，该属性是每个控件扩展器的必需属性。

接下来，请注意，类包含以下两个与客户端脚本相关的属性：

- WebResource-使文件作为嵌入资源包含在程序集中。
- ClientScriptResource-导致从程序集检索脚本资源。

当编译自定义扩展器时，WebResource 属性用于将 MyControlBehavior JavaScript 文件嵌入到程序集中。 当在网页中使用自定义扩展器时，ClientScriptResource 属性用于从程序集中检索 MyControlBehavior 脚本。

为了使 WebResource 和 ClientScriptResource 属性正常工作，必须将 JavaScript 文件编译为嵌入的资源。 在 "解决方案资源管理器" 窗口中选择文件，打开属性表，并将值 "*嵌入资源*" 分配给 "**生成操作**" 属性。

请注意，控件扩展器还包括 TargetControlType 属性。 此属性用于指定控件扩展器所扩展的控件类型。 对于列表1，控件扩展器用于扩展文本框。

最后请注意，自定义扩展器包含一个名为 T.myproperty 的属性。 该属性标记有 ExtenderControlProperty 特性。 GetPropertyValue （）和 SetPropertyValue （）方法用于将属性值从服务器端控件扩展程序传递到客户端行为。

接下来，为 DisabledButton 扩展器实现代码。 此扩展器的代码可以在 "清单 2" 中找到。

**列表 2-DisabledButtonExtender**

[!code-vb[Main](creating-a-custom-ajax-control-toolkit-control-extender-vb/samples/sample2.vb)]

清单2中的 DisabledButton 扩展器具有两个名为 TargetButtonID 和 DisabledText 的属性。 应用于 TargetButtonID 属性的 IDReferenceProperty 阻止你将 Button 控件的 ID 之外的任何内容分配给此属性。

WebResource 和 ClientScriptResource 属性将位于名为 DisabledButtonBehavior 的文件中的客户端行为与此扩展器相关联。 我们将在下一节中讨论此 JavaScript 文件。

## <a name="creating-the-custom-extender-behavior"></a>创建自定义扩展器行为

控件扩展器的客户端组件称为行为。 "禁用" 和 "启用" 按钮的实际逻辑包含在 DisabledButton 行为中。 此行为的 JavaScript 代码包含在列表3中。

**列表 3-DisabledButton**

[!code-javascript[Main](creating-a-custom-ajax-control-toolkit-control-extender-vb/samples/sample3.js)]

清单3中的 JavaScript 文件包含名为 DisabledButtonBehavior 的客户端类。 此类（如其服务器端克隆）包含两个名为 TargetButtonID 和 DisabledText 的属性，可以使用 get\_TargetButtonID/set\_TargetButtonID 并获取\_DisabledText/set\_DisabledText。

Initialize （）方法将一个 keyup 事件处理程序与该行为的目标元素相关联。 每次在与此行为相关联的文本框中键入字母时，keyup 处理程序都将执行。 Keyup 处理程序启用或禁用该按钮，具体取决于与该行为关联的文本框是否包含任何文本。

请记住，你必须将清单3中的 JavaScript 文件编译为嵌入资源。 在 "解决方案资源管理器" 窗口中选择文件，打开属性表，并将值 "*嵌入资源*" 分配给 "**生成操作**" 属性（参见图3）。 Visual Studio 和 Visual Web Developer 中都提供了此选项。

[![将 JavaScript 文件添加为嵌入资源](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image14.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image13.png)

**图 03**：添加作为嵌入资源的 JavaScript 文件（[单击以查看完全大小的映像](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image15.png)）

## <a name="creating-the-custom-extender-designer"></a>创建自定义扩展器设计器

需要创建一个最后一个类来完成扩展器。 需要在列表4中创建设计器类。 此类是使扩展程序正确运行 Visual Studio/Visual Web Developer 设计器所必需的。

**列表 4-DisabledButtonDesigner**

[!code-vb[Main](creating-a-custom-ajax-control-toolkit-control-extender-vb/samples/sample4.vb)]

将清单4中的设计器与具有设计器属性的 DisabledButton 扩展器相关联。需要将设计器属性应用于 DisabledButtonExtender 类，如下所示：

[!code-vb[Main](creating-a-custom-ajax-control-toolkit-control-extender-vb/samples/sample5.vb)]

## <a name="using-the-custom-extender"></a>使用自定义扩展器

现在，我们已完成了 DisabledButton 控件扩展器的创建，接下来可以在我们的 ASP.NET 网站中使用它。 首先，需要将自定义扩展器添加到 "工具箱"。 请执行这些步骤：

1. 双击 "解决方案资源管理器" 窗口中的页面，打开 "ASP.NET" 页。
2. 右键单击 "工具箱"，然后选择菜单选项 "**选择项**"。
3. 在 "选择工具箱项" 对话框中，浏览到 CustomExtenders 程序集。
4. 单击 **"确定"** 按钮关闭对话框。

完成这些步骤后，DisabledButton 控件扩展器应会出现在 "工具箱" 中（参见图4）。

[工具箱中的 ![DisabledButton](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image17.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image16.png)

**图 04**：工具箱中的 DisabledButton （[单击查看完全尺寸的图像](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image18.png)）

接下来，我们需要创建一个新的 ASP.NET 页面。 请执行这些步骤：

1. 创建名为 ShowDisabledButton 的新 ASP.NET 页。
2. 将 ScriptManager 拖到页面上。
3. 将 TextBox 控件拖到页面上。
4. 将一个 "按钮" 控件拖到页面上。
5. 在属性窗口中，将 "Button ID" 属性更改为值 " <em>btnsave.dock</em> "，并将 "Text" 属性更改为 " *Save\** " 值。

我们创建了一个包含标准 ASP.NET 文本框和按钮控件的页面。

接下来，我们需要扩展 TextBox 控件和 DisabledButton 扩展器：

1. 选择 "**添加扩展**器任务" 选项以打开扩展器向导对话框（请参阅图5）。 请注意，此对话框包含我们的自定义 DisabledButton 扩展器。
2. 选择 DisabledButton 扩展器，然后单击 **"确定"** 按钮。

[![扩展器向导对话框](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image20.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image19.png)

**图 05**：扩展器向导对话框（[单击以查看完全大小的映像](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image21.png)）

最后，我们可以设置 DisabledButton 扩展器的属性。 可以通过修改 TextBox 控件的属性来修改 DisabledButton 扩展器的属性：

1. 在设计器中选择文本框。
2. 在属性窗口中，展开 "扩展器" 节点（见图6）。
3. 将值*Save*赋给 DisabledText 属性，并将值*Btnsave.dock*分配到 TargetButtonID 属性。

[![设置扩展器属性](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image23.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image22.png)

**图 06**：设置扩展器属性（[单击以查看完全大小的映像](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image24.png)）

运行页面时（通过按 F5），按钮控件最初处于禁用状态。 开始在文本框中输入文本后，就会启用 Button 控件（参见图7）。

[![操作中的 DisabledButton 扩展器](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image26.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image25.png)

**图 07**：操作中的 DisabledButton 扩展器（[单击以查看完全大小的映像](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image27.png)）

## <a name="summary"></a>摘要

本教程的目的是说明如何通过自定义扩展器控件扩展 AJAX 控件工具包。 在本教程中，我们创建了一个简单的 DisabledButton 控件扩展器。 我们通过创建 DisabledButtonExtender 类、DisabledButtonBehavior JavaScript 行为和 DisabledButtonDesigner 类实现了这种扩展。 每当创建自定义控件扩展器时，都应遵循一组类似的步骤。

> [!div class="step-by-step"]
> [上一页](using-ajax-control-toolkit-controls-and-control-extenders-vb.md)
