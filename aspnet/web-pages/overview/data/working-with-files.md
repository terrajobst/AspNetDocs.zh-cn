---
uid: web-pages/overview/data/working-with-files
title: 在 ASP.NET 网页（Razor）站点中使用文件 |Microsoft Docs
author: Rick-Anderson
description: 本章介绍如何读取、写入、追加、删除和上传文件。
ms.author: riande
ms.date: 02/20/2014
ms.assetid: eee916e4-ba4c-439a-a24e-68df7d45a569
msc.legacyurl: /web-pages/overview/data/working-with-files
msc.type: authoredcontent
ms.openlocfilehash: 684c47a8a8480dc040e5144144577c94c35d39e5
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78521882"
---
# <a name="working-with-files-in-an-aspnet-web-pages-razor-site"></a>使用 ASP.NET 网页（Razor）站点中的文件

作者： [Tom FitzMacken](https://github.com/tfitzmac)

> 本文介绍如何在 ASP.NET 网页（Razor）站点中读取、写入、追加、删除和上传文件。
> 
> > [!NOTE]
> > 如果要上传图像并对其进行操作（例如，对其进行翻转或调整大小），请参阅使用[ASP.NET 网页站点中的图像](/aspnet/web-pages/overview/ui-layouts-and-themes/9-working-with-images)。
> 
> 
> **你将学习的内容：** 
> 
> - 如何创建文本文件并向其中写入数据。
> - 如何将数据追加到现有文件。
> - 如何读取和显示文件。
> - 如何从网站删除文件。
> - 如何让用户上传一个文件或多个文件。
> 
> 下面是本文中引入的 ASP.NET 编程功能：
> 
> - `File` 对象，它提供了一种方法来管理文件。
> - `FileUpload` 帮助程序。
> - `Path` 对象，它提供允许操作路径和文件名的方法。
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>本教程中使用的软件版本
> 
> 
> - ASP.NET 网页（Razor）2
> - WebMatrix 2
>   
> 
> 本教程还适用于 WebMatrix 3。

<a id="Creating_a_Text_File"></a>
## <a name="creating-a-text-file-and-writing-data-to-it"></a>创建文本文件并向其中写入数据

除了在网站中使用数据库之外，您还可以使用文件。 例如，您可以使用文本文件作为存储站点数据的一种简单方法。 （用于存储数据的文本文件有时称为 "*平面文件*"。）文本文件可以采用不同的格式，如 *.txt*、 *.xml*或 *.csv* （逗号分隔的值）。

如果要将数据存储在文本文件中，可以使用 `File.WriteAllText` 方法来指定要创建的文件和要写入的数据。 在此过程中，您将创建一个页面，其中包含一个简单窗体，其中包含三个 `input` 元素（名字、姓氏和电子邮件地址）和**提交**按钮。 当用户提交窗体时，将在文本文件中存储用户的输入。

1. 创建名为 "*应用\_* " 的新文件夹（如果它尚不存在）。
2. 在网站的根目录中，创建一个名为 " *UserData*" 的新文件。
3. 将现有内容替换为以下内容： 

    [!code-cshtml[Main](working-with-files/samples/sample1.cshtml)]

    HTML 标记将创建包含三个文本框的窗体。 在代码中，可以使用 `IsPost` 属性来确定是否已在开始处理前提交了页面。

    第一个任务是获取用户输入并将其分配给变量。 然后，该代码将单独变量的值连接为一个逗号分隔的字符串，然后将其存储在不同的变量中。 请注意，逗号分隔符是引号（"，"）中包含的字符串，因为你要将逗号嵌入到所创建的大字符串。 在连接在一起的数据的末尾，添加 `Environment.NewLine`。 这将添加换行符（换行符）。 所有此类连接所创建的内容是一个如下所示的字符串：

    [!code-css[Main](working-with-files/samples/sample2.css)]

    （末尾有一个不可见的换行符。）

    然后创建一个变量（`dataFile`），其中包含要在其中存储数据的文件的位置和名称。 设置位置需要一些特殊处理。 在网站中，将代码引用为 web 服务器*上的文件*的绝对路径是一种不好的做法。 如果移动了某个网站，则绝对路径将会出错。 此外，对于托管站点（而不是在您自己的计算机上），通常您在编写代码时，您甚至不知道正确的路径。

    但有时（如现在写入文件）需要完整的路径。 解决方案是使用 `Server` 对象的 `MapPath` 方法。 这会返回网站的完整路径。 若要获取网站根的路径，请将 `~` 运算符（要 represen 网站的虚拟根目录）的用户 `MapPath`。 （还可以向其传递子文件夹名称，例如 *~/App\_Data/* ）以获取该子文件夹的路径。）然后，可以将附加信息连接到方法返回的任何内容，以创建完整的路径。 在此示例中，将添加文件名。 （有关如何处理文件和文件夹路径的详细信息，请参阅[使用 Razor 语法 ASP.NET 网页编程](https://go.microsoft.com/fwlink/?LinkId=195205#ID_WorkingWithFileAndFolderPaths)。）

    该文件保存在*应用\_Data*文件夹中。 此文件夹是 ASP.NET 中的一个特殊文件夹，用于存储数据文件，如在[ASP.NET 网页网站中使用数据库简介](https://go.microsoft.com/fwlink/?LinkId=195209)中所述。

    `File` 对象的 `WriteAllText` 方法将数据写入文件。 此方法采用两个参数：要写入的文件的名称（包含路径）以及要写入的实际数据。 请注意，第一个参数的名称包含 `@` 字符作为前缀。 这会告知 ASP.NET 你正在提供逐字字符串文本，并且不应以特殊方式解释 "/" 之类的字符。 （有关详细信息，请参阅[使用 Razor 语法的 ASP.NET Web 编程简介](https://go.microsoft.com/fwlink/?LinkId=195205#ID_WorkingWithFileAndFolderPaths)。）

    > [!NOTE]
    > 为了使你的代码将文件保存到*应用\_Data*文件夹中，应用程序需要对该文件夹具有读写权限。 在您的开发计算机上，这通常不是问题。 但是，当你将网站发布到宿主提供程序的 web 服务器时，可能需要显式设置这些权限。 如果在宿主提供程序的服务器上运行此代码并收到错误，请与宿主提供程序联系，以了解如何设置这些权限。

- 在浏览器中运行页。 

    ![](working-with-files/_static/image1.jpg)
- 在字段中输入值，然后单击 "**提交**"。
- 关闭浏览器。
- 返回到项目并刷新视图。
- 打开 "*数据 .txt* " 文件。 您在表单中提交的数据在文件中。 

    ![[图像]](working-with-files/_static/image2.jpg)
- 关闭 "*数据 .txt* " 文件。

<a id="Appending_Data"></a>
## <a name="appending-data-to-an-existing-file"></a>将数据追加到现有文件

在上面的示例中，你使用 `WriteAllText` 创建一个文本文件，该文件中仅有一个数据块。 如果再次调用方法并向其传递相同的文件名，则会完全覆盖现有文件。 但是，创建文件后，通常需要将新数据添加到文件末尾。 您可以使用 `File` 对象的 `AppendAllText` 方法执行此操作。

1. 在网站中，创建一个*UserData*文件文件的副本，并将其命名为*UserDataMultiple*。
2. 用下面的代码块替换开始 `<!DOCTYPE html>` 标记前面的代码块： 

    [!code-cshtml[Main](working-with-files/samples/sample3.cshtml)]

    此代码在前面的示例中有一个更改。 它使用 `the AppendAllText` 方法，而不是使用 `WriteAllText`。 方法类似，不同之处在于 `AppendAllText` 将数据添加到文件末尾。 与 `WriteAllText`一样，`AppendAllText` 会创建文件（如果该文件尚不存在）。
3. 在浏览器中运行页。
4. 输入字段的值，然后单击 "**提交**"。
5. 添加更多数据，然后重新提交表单。
6. 返回到你的项目，右键单击项目文件夹，然后单击 "**刷新**"。
7. 打开 "*数据 .txt* " 文件。 它现在包含刚输入的新数据。 

    ![[图像]](working-with-files/_static/image3.jpg)

<a id="Reading_and_Displaying_Data"></a>
## <a name="reading-and-displaying-data-from-a-file"></a>读取和显示文件中的数据

即使不需要将数据写入文本文件，有时也可能需要从一个文件中读取数据。 为此，可以再次使用 `File` 对象。 您可以使用 `File` 对象单独读取每个行（用换行符分隔），也可以使用来读取单独的项，而不管它们是如何分离的。

此过程说明如何读取和显示在前面的示例中创建的数据。

1. 在网站的根目录中，创建一个名为*DisplayData*的新文件。
2. 将现有内容替换为以下内容： 

    [!code-cshtml[Main](working-with-files/samples/sample4.cshtml)]

    代码首先，使用此方法调用，将在上一示例中创建的文件读入名为 `userData`的变量：

    [!code-css[Main](working-with-files/samples/sample5.css)]

    用于执行此操作的代码位于 `if` 语句中。 当您想要读取某个文件时，最好使用 `File.Exists` 方法来确定该文件是否可用。 此代码还会检查文件是否为空。

    页面的主体包含两个 `foreach` 循环，一个嵌套在另一个中。 外部 `foreach` 循环一次从数据文件中获取一行。 在这种情况下，行是由文件&#8212;中的分行符定义的，每个数据项都在单独的行中。 外部循环在排序列表（`<ol>` 元素）中创建新项（`<li>` 元素）。

    内部循环使用逗号作为分隔符将每个数据行拆分为多个项（字段）。 （基于前面的示例，这意味着每一行都包含三个字段&#8212; ：名字、姓氏和电子邮件地址，每个字段用逗号分隔。）内部循环还创建 `<ul>` 列表，并为数据行中的每个字段显示一个列表项。

    此代码演示如何使用两种数据类型：数组和 `char` 数据类型。 数组是必需的，因为 `File.ReadAllLines` 方法以数组形式返回数据。 `char` 的数据类型是必需的，因为 `Split` 方法返回 `array`，其中每个元素都是 `char`类型。 （有关数组的信息，请参阅[使用 Razor 语法的 ASP.NET Web 编程简介](https://go.microsoft.com/fwlink/?LinkId=202890#ID_CollectionsAndObjects)。）
3. 在浏览器中运行页。 将显示您为前面的示例输入的数据。 

    ![[图像]](working-with-files/_static/image4.jpg)

> [!TIP] 
> 
> **显示以逗号分隔的 Microsoft Excel 文件中的数据**
> 
> 您可以使用 Microsoft Excel 将电子表格中包含的数据另存为逗号分隔的文件（ *.csv*文件）。 当你执行此操作时，文件将以纯文本格式保存，而不是以 Excel 格式保存。 电子表格中的每一行都用文本文件中的换行符分隔，每个数据项用逗号分隔。 您可以使用上一示例中所示的代码，只需在代码中更改数据文件的名称，即可读取 Excel 逗号分隔的文件。

<a id="Deleting_Files"></a>
## <a name="deleting-files"></a>删除文件

若要从您的网站删除文件，您可以使用 `File.Delete` 方法。 此过程说明如何允许用户从*images*文件夹中删除图像（ *.jpg*文件），前提是他们知道文件的名称。

> [!NOTE] 
> 
> **重要提示**在生产网站中，通常会限制允许对数据进行更改的人员。 有关如何设置成员身份和授权用户在网站上执行任务的方式的信息，请参阅向[ASP.NET 网页站点添加安全性和成员身份](https://go.microsoft.com/fwlink/?LinkId=202904)。

1. 在网站中，创建一个名为*images*的子文件夹。
2. 将一个或多个 *.jpg*文件复制到*images*文件夹中。
3. 在网站的根目录中，创建一个名为*FileDelete*的新文件。
4. 将现有内容替换为以下内容： 

    [!code-cshtml[Main](working-with-files/samples/sample6.cshtml)]

    此页面包含一个窗体，用户可以在其中输入图像文件的名称。 它们不会输入 *.jpg*文件扩展名;通过限制此名称，你可以帮助防止用户删除站点上的任意文件。

    此代码读取用户输入的文件名，然后构造完整的路径。 若要创建路径，代码将使用当前网站路径（由 `Server.MapPath` 方法返回）、*图像*文件夹名称、用户提供的名称和作为文本字符串的 ".jpg"。

    若要删除该文件，代码将调用 `File.Delete` 方法，并向其传递您刚刚构造的完整路径。 标记结束时，代码将显示一条确认消息，指出该文件已被删除。
5. 在浏览器中运行页。 

    ![[图像]](working-with-files/_static/image5.jpg)
6. 输入要删除的文件的名称，然后单击 "**提交**"。 如果已删除该文件，则该文件的名称将显示在该页的底部。

<a id="Letting_Users_Upload_a_File"></a>
## <a name="letting-users-upload-a-file"></a>允许用户上传文件

`FileUpload` 帮助器允许用户将文件上传到你的网站。 下面的过程演示如何让用户上传单个文件。

1. 如在[ASP.NET 网页站点中安装帮助程序](https://go.microsoft.com/fwlink/?LinkId=252372)中所述，将 ASP.NET Web 帮助程序库添加到你的网站中（如果你之前未添加）。
2. 在*应用\_Data*文件夹中，创建一个新文件夹并将其命名为*UploadedFiles*。
3. 在根目录中，创建一个名为*FileUpload*的新文件。
4. 将页面中的现有内容替换为以下内容： 

    [!code-cshtml[Main](working-with-files/samples/sample7.cshtml)]

    页面的正文部分使用 `FileUpload` 帮助器创建你可能熟悉的 "上传" 框和按钮：

    ![[图像]](working-with-files/_static/image6.jpg)

    你为 `FileUpload` 帮助程序设置的属性指定希望文件上传单个框，并且你希望 "提交" 按钮读取**上传**。 （稍后将添加更多的框。）

    当用户单击 "**上传**" 时，页面顶部的代码将获取文件并将其保存。 通常用于从窗体字段获取值的 `Request` 对象还具有一个包含已上传的文件（或文件）的 `Files` 数组。 您可以获取数组&#8212;中特定位置的单个文件，例如，获取第一个上载的文件，获取 `Request.Files[0]`，获取第二个文件，您将获得 `Request.Files[1]`等。 （请记住，在编程中，计数通常从零开始。）

    提取已上传的文件时，将其放在变量（此处为 `uploadedFile`）中，以便可以对其进行操作。 若要确定上传的文件的名称，只需获取其 `FileName` 属性即可。 但是，当用户上传文件时，`FileName` 包含用户的原始名称，其中包括整个路径。 它可能如下所示：

    *C:\Users\Public\Sample.txt*

    但不想要所有的路径信息，因为这是用户计算机上的路径，而不是服务器的路径。 只需要实际的文件名（*Sample .txt*）。 可以通过使用 `Path.GetFileName` 方法仅去除路径中的文件，如下所示：

    [!code-csharp[Main](working-with-files/samples/sample8.cs)]

    `Path` 对象是一个实用工具，其中包含许多方法，您可以使用这些方法来分割路径、组合路径等。

    获取上传的文件的名称后，可以在网站中创建要将上传的文件存储到的位置的新路径。 在这种情况下，你将 `Server.MapPath`、文件夹名称（*应用\_Data/UploadedFiles*）组合在一起，以创建新路径。 然后，可以调用上传的文件的 `SaveAs` 方法来实际保存该文件。
5. 在浏览器中运行页。 

    ![[图像]](working-with-files/_static/image7.jpg)
6. 单击 "**浏览**"，然后选择要上载的文件。 

    ![[图像]](working-with-files/_static/image8.jpg)

    "**浏览**" 按钮旁边的文本框将包含路径和文件位置。

    ![[图像]](working-with-files/_static/image9.jpg)
7. 单击“上载”。
8. 在网站中，右键单击项目文件夹，然后单击 "**刷新**"。
9. 打开*UploadedFiles*文件夹。 你上载的文件位于文件夹中。 

    ![[图像]](working-with-files/_static/image10.jpg)

<a id="Letting_Users_Upload_Multiple_Files"></a>
## <a name="letting-users-upload-multiple-files"></a>允许用户上传多个文件

在上面的示例中，允许用户上传一个文件。 但你可以使用 `FileUpload` 帮助程序一次上载多个文件。 这对于上传照片的方案非常方便，其中一次上传一个文件会很繁琐。 （您可以阅读有关在使用[ASP.NET 网页网站中的图像时](https://go.microsoft.com/fwlink/?LinkId=202897)上载照片的信息。）此示例演示如何允许用户一次上传两个，但你可以使用相同的技术来上传。

1. 根据在[ASP.NET 网页站点中安装帮助程序](https://go.microsoft.com/fwlink/?LinkId=252372)中所述，将 ASP.NET Web 帮助程序库添加到你的网站中（如果尚未安装）。
2. 创建名为*FileUploadMultiple*的新页面。
3. 将页面中的现有内容替换为以下内容：  

    [!code-cshtml[Main](working-with-files/samples/sample9.cshtml)]

    在此示例中，页面正文中的 `FileUpload` 帮助程序配置为允许用户在默认情况下上传两个文件。 由于 `allowMoreFilesToBeAdded` 设置为 `true`，因此帮助器将呈现允许用户添加更多上传框的链接：

    ![[图像]](working-with-files/_static/image11.jpg)

    若要处理用户上传的文件，代码将使用上一示例&#8212;中所用的相同基本方法从 `Request.Files` 获取文件，然后保存该文件。 （包括获得正确的文件名和路径所需的各种功能。）在这种情况下，用户可能会上载多个文件，而你不知道很多。 若要了解，你可以获取 `Request.Files.Count`。

    使用此数字，可以循环遍历 `Request.Files`，依次提取每个文件并保存。 如果要在集合中循环一次已知的次数，可以使用 `for` 循环，如下所示：

    [!code-csharp[Main](working-with-files/samples/sample10.cs)]

    变量 `i` 只是一个临时计数器，它将从零到你设置的任何上限。 在这种情况下，上限为文件的数目。 但由于计数器从零开始，因此对于在 ASP.NET 中计算方案的典型值，上限实际上比文件计数小1。 （如果上传了三个文件，则计数为0到2。）

    `uploadedCount` 变量会对已成功上传并保存的所有文件进行总计。 此代码可能会导致预期的文件无法上传。
4. 在浏览器中运行页。 浏览器将显示该页及其两个上传框。
5. 选择两个要上载的文件。
6. 单击 "**添加其他文件**"。 页面将显示新的上传框。 

    ![[图像]](working-with-files/_static/image12.jpg)
7. 单击“上载”。
8. 在网站中，右键单击项目文件夹，然后单击 "**刷新**"。
9. 打开*UploadedFiles*文件夹，查看是否已成功上传文件。

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a>其他资源

[使用 ASP.NET 网页站点中的图像](https://go.microsoft.com/fwlink/?LinkId=202897)

[导出到 CSV 文件](https://msdn.microsoft.com/library/ms155919.aspx)
