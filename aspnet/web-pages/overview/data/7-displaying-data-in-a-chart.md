---
uid: web-pages/overview/data/7-displaying-data-in-a-chart
title: 使用 ASP.NET 网页（Razor）在图表中显示数据 |Microsoft Docs
author: microsoft
description: 本章介绍如何在图表中显示数据。 在前面的章节中，已学习了如何手动和在网格中显示数据。 本章介绍 。
ms.author: riande
ms.date: 05/22/2012
ms.assetid: f889fd46-4dac-4ecb-83d8-60e64c22036e
msc.legacyurl: /web-pages/overview/data/7-displaying-data-in-a-chart
msc.type: authoredcontent
ms.openlocfilehash: 6dad67d4e3d38d57a761c567d937d714a3184ea9
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78509132"
---
# <a name="displaying-data-in-a-chart-with-aspnet-web-pages-razor"></a>使用 ASP.NET 网页（Razor）在图表中显示数据

由[Microsoft](https://github.com/microsoft)

> 本文介绍如何使用 "`Chart` 帮助程序" 在 ASP.NET 网页（Razor）网站中显示数据。
> 
> **你将学习的内容**：
> 
> - 如何在图表中显示数据。
> - 如何使用内置主题为图表建立样式。
> - 如何保存图表以及如何缓存它们以获得更好的性能。
> 
> 下面是本文中引入的 ASP.NET 编程功能：
> 
> - `Chart` 帮助程序。
> 
> > [!NOTE]
> > 本文中的信息适用于 ASP.NET 网页1.0 和网页2。

<a id="The_Chart_Helper"></a>
## <a name="the-chart-helper"></a>图表帮助器

如果要以图形形式显示数据，可以使用 `Chart` 帮助程序。 `Chart` 帮助程序可以呈现图像，该图像显示各种图表类型的数据。 它支持多种格式和标签选项。 `Chart` helper 可以呈现30多种类型的图表，包括您可能熟悉的 Microsoft Excel 或其他工具&#8212;区域图表、条形图、柱形图、折线图和饼图的所有类型的图表，以及股价图之类的更专业化的图表。

| **面积图**![说明：面积图类型的图片](7-displaying-data-in-a-chart/_static/image1.jpg) | **条形图**![说明：条形图类型的图片](7-displaying-data-in-a-chart/_static/image2.jpg) |
| --- | --- |
| **柱形图**![说明：柱形图类型的图片](7-displaying-data-in-a-chart/_static/image3.jpg) | **折线图**![说明：折线图类型的图片](7-displaying-data-in-a-chart/_static/image4.jpg) |
| **饼图**![说明：饼图类型的图片](7-displaying-data-in-a-chart/_static/image5.jpg) | **股价图**![说明：股价图类型的图片](7-displaying-data-in-a-chart/_static/image6.jpg) |

### <a name="chart-elements"></a>图表元素

图表显示数据和其他元素（如图例、轴、序列等）。 下图显示了在使用 `Chart` 帮助程序时可以自定义的许多图表元素。 本文介绍如何设置这些元素的部分（而非全部）。

![说明：显示图表元素的图片](7-displaying-data-in-a-chart/_static/image7.jpg)

<a id="Creating_a_Chart"></a>
## <a name="creating-a-chart-from-data"></a>从数据创建图表

在图表中显示的数据可以来自数组、从数据库返回的结果或 XML 文件中的数据。

### <a name="using-an-array"></a>使用数组

如[使用 Razor 语法 ASP.NET 网页编程](https://go.microsoft.com/fwlink/?LinkId=202890)中所述，数组允许您在单个变量中存储类似项的集合。 您可以使用数组来包含要包含在图表中的数据。

此过程说明如何使用默认图表类型，通过数组中的数据创建图表。 它还演示如何在页面中显示图表。

1. 创建名为*ChartArrayBasic*的新文件。
2. 将现有内容替换为以下内容： 

    [!code-cshtml[Main](7-displaying-data-in-a-chart/samples/sample1.cshtml)]

    代码首先创建一个新图表并设置其宽度和高度。 使用 `AddTitle` 方法指定图表标题。 若要添加数据，请使用 `AddSeries` 方法。 在此示例中，将使用 `AddSeries` 方法的 `name`、`xValue`和 `yValues` 参数。 `name` 参数将显示在图表图例中。 `xValue` 参数包含沿图表水平轴显示的数据数组。 `yValues` 参数包含用于绘制图表垂直点的数据数组。

    `Write` 方法实际上会呈现图表。 在这种情况下，由于未指定图表类型，`Chart` 帮助器将呈现其默认图表，这是一个柱形图。
3. 在浏览器中运行页。 浏览器将显示图表。 

    ![](7-displaying-data-in-a-chart/_static/image8.jpg)

### <a name="using-a-database-query-for-chart-data"></a>对图表数据使用数据库查询

如果您想要图表的信息位于数据库中，则可以运行数据库查询，然后使用结果中的数据创建图表。 此过程说明如何读取和显示有关在[ASP.NET 网页站点中使用数据库的简介](https://go.microsoft.com/fwlink/?LinkId=202893)中创建的数据库的数据。

1. 如果文件夹尚不存在，则将*应用\_Data*文件夹添加到网站的根目录。
2. 在*应用\_Data*文件夹中，添加使用[ASP.NET 网页站点中的数据库简介](https://go.microsoft.com/fwlink/?LinkId=202893)中描述的名为 SmallBakery 的数据库文件 *。*
3. 创建名为*ChartDataQuery*的新文件。
4. 将现有内容替换为以下内容：   

    [!code-cshtml[Main](7-displaying-data-in-a-chart/samples/sample2.cshtml)]

    代码首先打开 SmallBakery 数据库，并将其分配给名为 `db`的变量。 此变量表示可用于读取和写入数据库的 `Database` 对象。 接下来，代码将运行 SQL 查询，以获取每个产品的名称和价格。 该代码将创建一个新的图表，并通过调用图表的 `DataBindTable` 方法，将数据库查询传递给它。 此方法采用两个参数： `dataSource` 参数用于查询中的数据，而 `xField` 参数用于设置用于图表的 x 轴的数据列。

    作为使用 `DataBindTable` 方法的替代方法，您可以使用 `Chart` 帮助器的 `AddSeries` 方法。 利用 `AddSeries` 方法，你可以设置 `xValue` 和 `yValues` 参数。 例如，不使用如下所示的 `DataBindTable` 方法：

    [!code-css[Main](7-displaying-data-in-a-chart/samples/sample3.css)]

    可以使用如下所示的 `AddSeries` 方法：

    [!code-html[Main](7-displaying-data-in-a-chart/samples/sample4.html)]

    两者都呈现相同的结果。 `AddSeries` 方法更灵活，因为你可以更明确地指定图表类型和数据，但如果不需要额外的灵活性，则 `DataBindTable` 方法更易于使用。
5. 在浏览器中运行页。 

    ![](7-displaying-data-in-a-chart/_static/image9.jpg)

### <a name="using-xml-data"></a>使用 XML 数据

用于绘制图表的第三个选项是使用 XML 文件作为图表的数据。 这要求 XML 文件还具有描述 XML 结构的架构文件（ *.xsd*文件）。 此过程演示如何从 XML 文件读取数据。

1. 在*应用\_data* "文件夹中，创建一个名为" *data .xml*"的新 XML 文件。
2. 将现有的 XML 替换为以下项，这是有关虚构公司中的员工的一些 XML 数据。 

    [!code-xml[Main](7-displaying-data-in-a-chart/samples/sample5.xml)]
3. 在*应用\_data*文件夹中，创建一个名为 " *data .xsd*" 的新 XML 文件。 （请注意，此时间的扩展名为 *.xsd*。）
4. 将现有的 XML 替换为以下内容： 

    [!code-xml[Main](7-displaying-data-in-a-chart/samples/sample6.xml)]
5. 在网站的根目录中，创建一个名为*ChartDataXML*的新文件。
6. 将现有内容替换为以下内容： 

    [!code-cshtml[Main](7-displaying-data-in-a-chart/samples/sample7.cshtml)]

    代码首先创建一个 `DataSet` 对象。 此对象用于管理从 XML 文件中读取的数据，并根据架构文件中的信息对其进行组织。 （请注意，代码顶部包含语句 `using SystemData`。 这是为了能够处理 `DataSet` 对象所必需的。 有关详细信息，请参阅本文后面的[&quot;使用&quot; 语句和完全限定的名称](#SB_UsingStatements)。）

    接下来，该代码基于数据集创建一个 `DataView` 对象。 数据视图提供了一个图表可以绑定到&#8212;的对象，该对象是读取和绘制的。 图表将使用 `AddSeries` 方法绑定到数据，正如你之前在对数组数据进行图表时看到的一样，只是这次 `xValue` 和 `yValues` 参数设置为 `DataView` 对象。

    此示例还演示如何指定特定图表类型。 在 `AddSeries` 方法中添加数据时，还会将 `chartType` 参数设置为显示饼图。
7. 在浏览器中运行页。 

    ![](7-displaying-data-in-a-chart/_static/image10.jpg)

> [!TIP]
> 
> <a id="SB_UsingStatements"></a>
> ### <a name="using-statements-and-fully-qualified-names"></a>"Using" 语句和完全限定名称
> 
> 与 Razor 语法 ASP.NET 网页的 .NET Framework 基于包含数千个组件（类）的。 为了使其可用于处理所有这些类，它们被组织到一些*命名空间*中，这些命名空间有点像库。 例如，`System.Web` 命名空间包含支持浏览器/服务器通信的类，`System.Xml` 命名空间包含用于创建和读取 XML 文件的类，`System.Data` 命名空间包含可用于处理数据的类。
> 
> 为了访问 .NET Framework 中的任何给定类，代码不仅需要知道类名称，还需要知道类所在的命名空间。 例如，为了使用 `Chart` 帮助程序，代码需要查找 `System.Web.Helpers.Chart` 类，该类将命名空间（`System.Web.Helpers`）与类名称（`Chart`）组合在一起。 这称为类的*完全限定*名称&#8212; ，它在 .NET Framework 的 vastness 中具有完整的明确位置。 在代码中，这将如下所示：
> 
> `var myChart = new System.Web.Helpers.Chart(width: 600, height: 400) // etc.`
> 
> 然而，每次需要引用一个类或帮助器时，都必须使用这些长的、完全限定的名称，这是一项很繁琐的（并且容易出错）。 因此，为了更轻松地使用类名称，你可以*导入*感兴趣的命名空间，这通常只是 .NET Framework 中的多个命名空间中的少数几个。 如果导入了命名空间，则只能使用类名称（`Chart`）而不是完全限定的名称（`System.Web.Helpers.Chart`）。 当你的代码运行并遇到类名称时，它可以仅查看已导入的命名空间以找到该类。
> 
> 使用 Razor 语法的 ASP.NET 网页创建网页时，通常每次使用相同的一组类，包括 `WebPage` 类、各种帮助程序等。 为了节省每次创建网站时导入相关命名空间的工作，ASP.NET 配置为每个网站自动导入一组核心命名空间。 这就是你不必处理命名空间或导入的原因，你曾经处理过的所有类都在已为你导入的命名空间中。
> 
> 但是，有时你需要使用不在自动导入的命名空间中的类。 在这种情况下，可以使用该类的完全限定名称，也可以手动导入包含该类的命名空间。 若要导入命名空间，请使用 `using` 语句（`import` 在 Visual Basic 中），如上文所述。
> 
> 例如，`DataSet` 类在 `System.Data` 命名空间中。 `System.Data` 命名空间不会自动用于 ASP.NET Razor 页面。 因此，若要使用其完全限定名称来处理 `DataSet` 类，可以使用如下所示的代码：
> 
> `var dataSet = new System.Data.DataSet();`
> 
> 如果必须重复使用 `DataSet` 类，可以导入如下所示的命名空间，然后在代码中只使用类名称：
> 
> [!code-cshtml[Main](7-displaying-data-in-a-chart/samples/sample8.cshtml)]
> 
> 您可以为要引用的任何其他 .NET Framework 命名空间添加 `using` 语句。 但正如前面所述，你不需要经常执行此操作，因为你将使用的大多数类都位于 ASP.NET 自动导入的命名空间中，以便在 *.* # 和*vbhtml*页中使用。

<a id="Displaying_Charts"></a>
## <a name="displaying-charts-inside-a-web-page"></a>在网页中显示图表

在到目前为止，您已经看到了一个图表，然后将该图表作为图形直接呈现到浏览器。 但在许多情况下，你希望将图表显示为页的一部分，而不只是在浏览器中显示。 若要执行此操作，需要一个两步过程。 第一步是创建一个生成图表的页面，正如您所看到的那样。

第二步是在另一页中显示生成的图像。 若要显示图像，请使用 HTML `<img>` 元素，其方式与显示任何图像的方式相同。 但是，`<img>` 元素不是引用 *.jpg*或 *.png*文件，而是引用包含创建图表的 `Chart` 帮助器的*cshtml 文件。* 当显示页运行时，`<img>` 元素将获取 `Chart` 帮助器的输出，并呈现图表。

![](7-displaying-data-in-a-chart/_static/image11.jpg)

1. 创建名为*ShowChart*的文件。
2. 将现有内容替换为以下内容： 

    [!code-html[Main](7-displaying-data-in-a-chart/samples/sample9.html)]

    代码使用 `<img>` 元素显示你之前在*ChartArrayBasic*文件中创建的图表。
3. 在浏览器中运行网页。 *ShowChart*文件根据*ChartArrayBasic*文件中包含的代码显示图表图像。

<a id="Styling_a_Chart"></a>
## <a name="styling-a-chart"></a>设置图表样式

`Chart` 帮助器支持大量选项，使您可以自定义图表的外观。 可以设置颜色、字体、边框等。 若要自定义图表的外观，一种简单的方法是使用*主题*。 主题是信息的集合，用于指定如何使用字体、颜色、标签、调色板、边框和效果来呈现图表。 （请注意，图表样式不指示图表类型。）

下表列出了内置主题。

| 主题 | 说明 |
| --- | --- |
| `Vanilla` | 在白色背景上显示红色列。 |
| `Blue` | 显示蓝色渐变背景上的蓝色列。 |
| `Green` | 显示绿色渐变背景上的蓝色列。 |
| `Yellow` | 在黄色渐变背景上显示橙色列。 |
| `Vanilla3D` | 在白色背景上显示三维红列。 |

您可以指定在创建新图表时要使用的主题。

1. 创建名为*ChartStyleGreen*的新文件。
2. 将页面中的现有内容替换为以下内容：

    [!code-cshtml[Main](7-displaying-data-in-a-chart/samples/sample10.cshtml)]

    此代码与使用数据库作为数据的前面的示例相同，但在创建 `Chart` 对象时将添加 `theme` 参数。 下面显示了更改后的代码：

    [!code-csharp[Main](7-displaying-data-in-a-chart/samples/sample11.cs)]
3. 在浏览器中运行页。 您看到的数据与以前相同，但图表看起来更精美： 

    ![](7-displaying-data-in-a-chart/_static/image12.jpg)

<a id="Saving_a_Chart"></a>
## <a name="saving-a-chart"></a>保存图表

当您在本文中看到到目前为止，使用 `Chart` 帮助程序时，帮助程序将在每次调用时从头开始重新创建图表。 必要时，图表的代码还会重新查询数据库或重新读取 XML 文件以获取数据。 在某些情况下，执行此操作可能是一项复杂的操作，例如，如果要查询的数据库很大，或者 XML 文件包含大量数据。 即使图表不涉及大量数据，动态创建映像的过程也会占用服务器资源，如果很多人请求显示图表的页面，可能会对网站的性能产生影响。

为了帮助您降低创建图表的潜在性能影响，您可以在第一次需要图表时创建图表，并保存它。 如果再次需要图表，而不是重新生成它，则可以只提取保存的版本并呈现。

可以通过以下方式保存图表：

- 在计算机内存（在服务器上）缓存图表。
- 将该图表保存为图像文件。
- 将图表另存为 XML 文件。 此选项允许您在保存图表之前修改图表。

### <a name="caching-a-chart"></a>缓存图表

创建图表后，可以对其进行缓存。 缓存图表意味着无需重新创建它，如果需要再次显示它。 将图表保存到缓存中时，请为其指定一个必须对该图表唯一的键。

如果服务器内存不足，则可能会删除保存到缓存中的图表。 此外，如果应用程序出于任何原因而重新启动，则会清除缓存。 因此，使用缓存的图表的标准方法是始终首先检查它是否在缓存中可用，如果没有，则创建或重新创建它。

1. 在网站的根目录中，创建一个名为 " *ShowCachedChart*" 的文件。
2. 将现有内容替换为以下内容： 

    [!code-html[Main](7-displaying-data-in-a-chart/samples/sample12.html)]

    `<img>` 标记包含指向*ChartSaveToCache*文件的 `src` 属性，并将一个键作为查询字符串传递到页面。 项包含 &quot;myChartKey&quot;的值。 *ChartSaveToCache*文件包含创建图表的 `Chart` 帮助程序。 稍后你将创建此页。

    页面末尾有一个指向名为*ClearCache*的页面的链接。 这是你稍后将创建的一个页面。 仅需*ClearCache*来测试此示例的缓存，而不是在处理缓存图表时通常会包含的链接或页面。
3. 在网站的根目录中，创建一个名为*ChartSaveToCache*的新文件。
4. 将现有内容替换为以下内容：

    [!code-cshtml[Main](7-displaying-data-in-a-chart/samples/sample13.cshtml)]

    代码首先检查是否有任何内容作为键值传递到查询字符串中。 如果是这样，则代码会尝试通过调用 `GetFromCache` 方法并向其传递密钥来读取缓存中的图表。 如果事实证明，该密钥下的缓存中没有任何内容（这会在第一次请求图表时出现），则代码会照常创建图表。 图表完成后，代码通过调用 `SaveToCache`将其保存到缓存中。 该方法需要一个键（以便以后可以请求图表）和在缓存中保存图表的时间量。 （缓存图表所需的确切时间取决于您认为数据所代表的数据可能发生变化的频率。）如果将此参数设置为 true， &#8212;则 `SaveToCache` 方法还需要 `slidingExpiration` 参数，每次访问该图表时都会重置超时计数器。 在这种情况下，它实际上是指在用户上一次访问图表后，图表的缓存条目将在2分钟后过期。 （可调过期的替代方法是绝对过期，这意味着缓存项在放入缓存后会刚好在2分钟后过期，无论其访问频率如何。）

    最后，代码使用 `WriteFromCache` 方法从缓存中提取并呈现图表。 请注意，此方法不在检查缓存的 `if` 块的外部，因为它将从缓存中获取图表，无论图表是以哪种方式开始，还是必须在缓存中生成并保存。

    请注意，在此示例中，`AddTitle` 方法包含时间戳。 （将当前日期和时间&#8212; `DateTime.Now` &#8212;添加到标题中。）
5. 创建名为*ClearCache*的新页面，并将其内容替换为以下内容：

    [!code-cshtml[Main](7-displaying-data-in-a-chart/samples/sample14.cshtml)]

    此页使用 `WebCache` 帮助器删除*ChartSaveToCache*中缓存的图表。 如前文所述，您通常不需要像下面这样的页面。 此处只需创建它，以便更轻松地测试缓存。
6. 在浏览器中运行*ShowCachedChart*网页。 页面根据*ChartSaveToCache*文件中包含的代码显示图表图像。 记录时间戳在图表标题中显示的内容。 

    ![说明：图表标题中带有时间戳的基本图表图片](7-displaying-data-in-a-chart/_static/image13.jpg)
7. 关闭浏览器。
8. 再次运行*ShowCachedChart* 。 请注意，时间戳与以前相同，这指示图表不会重新生成，而是从缓存中读取。
9. 在*ShowCachedChart*中，单击 "**清除缓存**" 链接。 这会将你转到*ClearCache*，该操作报告缓存已清除。
10. 单击 "**返回 ShowCachedChart** " 链接，或从 WebMatrix 重新运行*ShowCachedChart* 。 请注意，此时间戳已更改，因为缓存已被清除。 因此，该代码必须重新生成图表并将其放回到缓存中。

### <a name="saving-a-chart-as-an-image-file"></a>将图表保存为图像文件

你还可以将图表保存为服务器上的图像文件（例如， *.jpg*文件）。 然后，你可以像使用任何映像一样使用映像文件。 其优势在于存储文件，而不是保存到临时缓存中。 您可以在不同的时间（例如，每小时）保存一个新的图表图像，然后保留一段时间内发生的更改的永久记录。 请注意，您必须确保您的 web 应用程序有权将文件保存到服务器上要放置映像文件的文件夹中。

1. 在网站的根目录中，创建一个名为 *\_ChartFiles*的文件夹（如果它尚不存在）。
2. 在网站的根目录中，创建一个名为*ChartSave*的新文件。
3. 将现有内容替换为以下内容：

    [!code-cshtml[Main](7-displaying-data-in-a-chart/samples/sample15.cshtml)]

    代码首先通过调用 `File.Exists` 方法来查看 *.jpg*文件是否存在。 如果该文件不存在，则代码将从数组创建新 `Chart`。 这一次，代码调用 `Save` 方法，并传递 `path` 参数以指定保存图表的位置的文件路径和文件名。 在页面的正文中，`<img>` 元素使用指向要显示的 *.jpg*文件的路径。
4. 运行*ChartSave*文件。
5. 返回到 WebMatrix。 请注意，名为*chart01*的图像文件已保存在 *\_ChartFiles*文件夹中。

### <a name="saving-a-chart-as-an-xml-file"></a>将图表另存为 XML 文件

最后，可以将图表保存为服务器上的 XML 文件。 使用此方法对图表进行缓存或将图表保存到文件的一个优点是，可以在显示图表之前修改 XML （如果需要）。 您的应用程序必须对要放置映像文件的服务器上的文件夹具有读/写权限。

1. 在网站的根目录中，创建一个名为*ChartSaveXml*的新文件。
2. 将现有内容替换为以下内容：

    [!code-cshtml[Main](7-displaying-data-in-a-chart/samples/sample16.cshtml)]

    此代码类似于您之前在缓存中存储图表所看到的代码，只不过它使用 XML 文件。 代码首先通过调用 `File.Exists` 方法来检查 XML 文件是否存在。 如果该文件存在，则代码会创建一个新的 `Chart` 对象，并将该文件名作为 `themePath` 参数传递。 这将根据 XML 文件中的内容创建图表。 如果 XML 文件尚不存在，则代码会创建一个图表，如 normal，然后调用 `SaveXml` 将其保存。 如之前所见，使用 `Write` 方法呈现图表。

    与显示缓存的页面一样，此代码在图表标题中包含时间戳。
3. 创建名为*ChartDisplayXMLChart*的新页面，并向其添加以下标记： 

    [!code-html[Main](7-displaying-data-in-a-chart/samples/sample17.html)]
4. 运行*ChartDisplayXMLChart*页。 将显示图表。 记下图表标题中的时间戳。
5. 关闭浏览器。
6. 在 WebMatrix 中，右键单击 *\_ChartFiles* "文件夹，单击"**刷新**"，然后打开该文件夹。 此文件夹中的*XMLChart*文件是由 `Chart` 帮助程序创建的。 

    ![说明： _ChartFiles 文件夹，其中显示了由图表帮助器创建的 XMLChart 文件。](7-displaying-data-in-a-chart/_static/image14.jpg)
7. 再次运行*ChartDisplayXMLChart*页。 图表显示的时间戳与首次运行页面时的时间戳相同。 这是因为，该图表是从之前保存的 XML 生成的。
8. 在 WebMatrix 中，打开 *\_ChartFiles*文件夹并删除*XMLChart*文件。
9. 再次运行*ChartDisplayXMLChart*页。 此时，时间戳会更新，因为 `Chart` 帮助程序必须重新创建 XML 文件。 如果需要，请检查 *\_ChartFiles* "文件夹，并注意该 XML 文件已返回。

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a>其他资源

- [使用 ASP.NET 网页站点中的数据库简介](https://go.microsoft.com/fwlink/?LinkId=202893)
- [在 ASP.NET 网页站点中使用缓存来提高性能](https://go.microsoft.com/fwlink/?LinkId=202903)
- [Chart 类](https://msdn.microsoft.com/library/system.web.helpers.chart(v=vs.99))（MSDN 上的 ASP.NET 网页 API 参考）
