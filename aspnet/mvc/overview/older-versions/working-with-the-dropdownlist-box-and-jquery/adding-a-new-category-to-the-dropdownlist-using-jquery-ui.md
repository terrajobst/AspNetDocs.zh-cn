---
uid: mvc/overview/older-versions/working-with-the-dropdownlist-box-and-jquery/adding-a-new-category-to-the-dropdownlist-using-jquery-ui
title: 使用 jQuery UI 将新类别添加到 DropDownList |Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 01/12/2012
ms.assetid: 44aa1ac4-6ea2-48a2-972d-52710c48eae5
msc.legacyurl: /mvc/overview/older-versions/working-with-the-dropdownlist-box-and-jquery/adding-a-new-category-to-the-dropdownlist-using-jquery-ui
msc.type: authoredcontent
ms.openlocfilehash: cb9053593e2ea788638aec063c845cb91121861b
ms.sourcegitcommit: e365196c75ce93cd8967412b1cfdc27121816110
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/07/2020
ms.locfileid: "77075107"
---
# <a name="adding-a-new-category-to-the-dropdownlist-using-jquery-ui"></a>使用 jQuery UI 向 DropDownList 添加新类别

作者： [Rick Anderson]((https://twitter.com/RickAndMSFT))

HTML `Select` 标记非常适合用于呈现固定类别数据的列表，但通常需要添加新类别。 假设我们要将流派 "Opera" 添加到数据库中的类别？ 在本部分中，我们将使用 jQuery UI 来添加一个对话框，可使用该对话框添加新类别。 下图显示了 UI 在浏览器中的显示方式。

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image1.png)

当用户选择 "**添加新流派**" 链接时，会弹出一个对话框，提示用户输入新的流派名称（可选）。 下图显示了 "**添加流派**" 弹出对话框。

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image2.png)

当输入新的流派名称并推送 "**保存**" 按钮时，将发生以下情况：

1. AJAX 调用将数据发布到流派控制器的 Create 方法，该方法将新的流派保存到数据库，并将新的流派信息（流派名称和 ID）作为 JSON 返回。
2. JavaScript 将新的流派数据添加到选择列表。
3. JavaScript 使新的流派成为所选项目。

   在下图中，将 " **Opera** " 添加到数据库，并在 "**流派**" 下拉列表中选择。 

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image3.png)

打开*Views\StoreManager\Create.cshtml*文件，并将流派标记替换为以下代码：

[!code-cshtml[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample1.cshtml)]

`_ChooseGenre` 分部视图将包含与用于实现添加新的流派功能的 JavaScript 和 jQuery 挂钩的所有逻辑。 完成代码后，就可以轻松地使用艺术家 UI 执行相同操作。

在解决方案资源管理器中，右键单击*Views\StoreManager*文件夹，然后选择 "**添加**"，然后单击 "**查看**"。 在 "**视图名称**" 输入中输入 `_ChooseGenre`，然后选择 "**添加**"。 将*Views\StoreManager\\_ChooseGenre*的标记替换为以下内容：

[!code-cshtml[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample2.cshtml)]

第一行声明我们作为模型传入了一个 `Album`，这与创建视图中找到的模型语句完全相同。 接下来的几行是**标签**帮助器标记。 下一行是**DropDownList** helper 调用，与原始创建视图中的调用完全相同。 下一行添加一个名称 `Add New Genre`的链接，并将其样式用作按钮。 将直接从 "创建" 视图复制包含 `ValidationMessageFor` 的行。 以下行：

[!code-html[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample3.html)]

创建具有 `genreDialog`ID 的隐藏 div。 我们将使用 jQuery 挂钩 "**添加流派**" 对话框，该对话框具有此 div 中的 ID `genreDialog`。 最后两个脚本标记包含指向用于实现 "添加新流派" 功能的 JavaScript 文件的链接。 */Scripts/chooseGenre.js*文件是在项目中提供的，我们稍后将在本教程中对其进行检查。

运行应用程序，并单击 "**添加新流派**" 按钮。 在 "**添加流派**" 对话框中，在 "**名称**" 输入框中输入 " **Opera** "。

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image4.png)

单击“保存”按钮 。 AJAX 调用创建了 "Opera" 类别，然后使用 Opera 填充下拉列表，并将 "Opera" 设置为所选的流派。

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image5.png)

输入艺术家、标题和价格，然后选择 "**创建**" 按钮。 如果输入小于 $8.99 的价格，则新的唱片集将显示在索引视图的顶部。 验证新的唱片集条目是否已保存到数据库中。

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image6.png)

尝试创建一个只包含一个字母的新流派。 *Models\Genre.cs*文件中的以下代码设置了流派名称的最小长度和最大长度。

[!code-csharp[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample4.cs)]

客户端验证报表您必须输入一个介于2到20个字符之间的字符串。

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image7.png)

### <a name="examining-how-a-new-genre-is-added-to-the-database-and-the-select-list"></a>检查如何将新的流派添加到数据库以及选择列表。

打开*Scripts\chooseGenre.js*文件并检查代码。

[!code-javascript[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample5.js)]

第二行使用 ID `genreDialog` 在*Views\StoreManager\\_ChooseGenre* # # 文件中的 div 标记上创建一个对话框。 大多数命名参数都是一目了然的。 `autoOpen` 参数设置为 "false"，则选择 "**创建流派**" 按钮将显式打开对话（这在中对此进行了说明）。 此对话框包含两个按钮： "**保存**" 和 "**取消**"。 "**取消**" 按钮关闭对话框。 下面的代码显示 "**保存**" 按钮函数。

[!code-javascript[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample6.js)]

将从 `createGenreForm` ID 中选择 `var createGenreForm`。 `createGenreForm` ID 在*Views\Genre\\_CreateGenre.* # 文件中找到的以下代码中进行了设置。

[!code-cshtml[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample7.cshtml)]

Views\Genre\\中使用的[html.beginform](https://msdn.microsoft.com/library/dd492714.aspx) helper 重载 *_CreateGenre. #. #. #. #. #.* 可以通过在浏览器中显示 "创建唱片集" 页，然后在浏览器中选择 "显示源" 来查看此项。 以下标记显示了包含表单标记的生成的 HTML。

[!code-html[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample8.html)]

JQuery `$.post` 行对操作属性（`/StoreManager/Create`）进行 AJAX 调用，并传入 "**创建流派**" 对话框中的数据。 数据包含新流派的名称和可选说明。 如果 AJAX 调用成功，新的流派名称和值将添加到 "选择标记"，并将新的流派设置为所选值。 由于这是动态生成的标记，因此无法通过在浏览器中查看源来查看新的选择选项。 你可以看到具有 IE 9 F12 开发人员工具的新 HTML。 若要查看新的选择选项，请在 Internet Explorer 9 中按 F12 键启动 F12 开发人员工具。 导航到 "创建" 页并添加一个新的流派，以便在 "流派选择列表" 中选择新的流派。 在 F12 开发人员工具中：

1. 选择 "HTML" 选项卡。
2. 点击刷新图标。  
    ![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image8.png)
3. 在搜索框中，输入 "GenreID"。
4. 使用下一个图标，   
    ![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image9.png)  
   导航到以下选择标记：

    [!code-html[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample9.html)]
5. 展开最后一个选项值。

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image10.png)

*Scripts\chooseGenre.js*文件中的以下代码显示了如何将 "**添加新的流派**" 按钮连接到 click 事件，以及如何创建 "**添加新流派**" 对话框。

[!code-javascript[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample10.js)]

第一行创建附加到 "**添加新流派**" 按钮的 click 函数。 Views\StoreManager\\_ChooseGenre. # 文件中的以下标记显示了如何创建 "**添加新流派**" 按钮：

[!code-cshtml[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample11.cshtml)]

Load 方法创建并打开 "添加流派" 对话框并调用 jQuery `parse` 方法，以便在对话框中输入的数据上进行客户端验证。

在本部分中，您学习了如何创建一个对话框，该对话框可用于将新的类别数据添加到选择列表。 可以按照相同的过程来创建 UI，以将新的艺术家添加到艺术家选择列表。 本教程大致介绍了如何使用 ASP.NET MVC HTML helper **DropDownList**。 有关使用**DropDownList**的其他信息，请参阅下面的加法引用部分。 如果本教程有帮助，请告知我们。

Rick.Anderson[at]Microsoft.com

### <a name="additional-references"></a>其他参考

- [ASP.NET MVC –级联下拉列表教程（](https://weblogs.asp.net/raduenuca/archive/2011/03/06/asp-net-mvc-cascading-dropdown-lists-tutorial-part-1-defining-the-problem-and-the-context.aspx) [Radu enuca on](https://weblogs.asp.net/raduenuca/default.aspx) ）
- 已[选择](https://harvesthq.github.com/chosen/)支持多选和筛选的 JavaScript 插件。

### <a name="contributors"></a>参与者

- [Radu Enuca on](https://weblogs.asp.net/raduenuca/default.aspx)
- Jean-Sébastien Goupil
- [Brad Wilson](http://bradwilson.typepad.com/)

### <a name="reviewers"></a>审阅者

- Jean-Sébastien Goupil
- [Brad Wilson](http://bradwilson.typepad.com/)
- Mike Pope
- Tom Dykstra

> [!div class="step-by-step"]
> [“上一步”](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper.md)
