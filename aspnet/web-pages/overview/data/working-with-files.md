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
# <a name="working-with-files-in-an-aspnet-web-pages-razor-site"></a><span data-ttu-id="5a2b5-103">使用 ASP.NET 网页（Razor）站点中的文件</span><span class="sxs-lookup"><span data-stu-id="5a2b5-103">Working with Files in an ASP.NET Web Pages (Razor) Site</span></span>

<span data-ttu-id="5a2b5-104">作者： [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="5a2b5-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="5a2b5-105">本文介绍如何在 ASP.NET 网页（Razor）站点中读取、写入、追加、删除和上传文件。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-105">This article explains how to read, write, append, delete, and upload files in an ASP.NET Web Pages (Razor) site.</span></span>
> 
> > [!NOTE]
> > <span data-ttu-id="5a2b5-106">如果要上传图像并对其进行操作（例如，对其进行翻转或调整大小），请参阅使用[ASP.NET 网页站点中的图像](/aspnet/web-pages/overview/ui-layouts-and-themes/9-working-with-images)。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-106">If you want to upload images and manipulate them (for example, flip or resize them), see [Working with Images in an ASP.NET Web Pages Site](/aspnet/web-pages/overview/ui-layouts-and-themes/9-working-with-images).</span></span>
> 
> 
> <span data-ttu-id="5a2b5-107">**你将学习的内容：**</span><span class="sxs-lookup"><span data-stu-id="5a2b5-107">**What you'll learn:**</span></span> 
> 
> - <span data-ttu-id="5a2b5-108">如何创建文本文件并向其中写入数据。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-108">How to create a text file and write data to it.</span></span>
> - <span data-ttu-id="5a2b5-109">如何将数据追加到现有文件。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-109">How to append data to an existing file.</span></span>
> - <span data-ttu-id="5a2b5-110">如何读取和显示文件。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-110">How to read a file and display from it.</span></span>
> - <span data-ttu-id="5a2b5-111">如何从网站删除文件。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-111">How to delete files from a website.</span></span>
> - <span data-ttu-id="5a2b5-112">如何让用户上传一个文件或多个文件。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-112">How to let users upload one file or multiple files.</span></span>
> 
> <span data-ttu-id="5a2b5-113">下面是本文中引入的 ASP.NET 编程功能：</span><span class="sxs-lookup"><span data-stu-id="5a2b5-113">These are the ASP.NET programming features introduced in the article:</span></span>
> 
> - <span data-ttu-id="5a2b5-114">`File` 对象，它提供了一种方法来管理文件。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-114">The `File` object, which provides a way to manage files.</span></span>
> - <span data-ttu-id="5a2b5-115">`FileUpload` 帮助程序。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-115">The `FileUpload` helper.</span></span>
> - <span data-ttu-id="5a2b5-116">`Path` 对象，它提供允许操作路径和文件名的方法。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-116">The `Path` object, which provides methods that let you manipulate path and file names.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="5a2b5-117">本教程中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="5a2b5-117">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="5a2b5-118">ASP.NET 网页（Razor）2</span><span class="sxs-lookup"><span data-stu-id="5a2b5-118">ASP.NET Web Pages (Razor) 2</span></span>
> - <span data-ttu-id="5a2b5-119">WebMatrix 2</span><span class="sxs-lookup"><span data-stu-id="5a2b5-119">WebMatrix 2</span></span>
>   
> 
> <span data-ttu-id="5a2b5-120">本教程还适用于 WebMatrix 3。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-120">This tutorial also works with WebMatrix 3.</span></span>

<a id="Creating_a_Text_File"></a>
## <a name="creating-a-text-file-and-writing-data-to-it"></a><span data-ttu-id="5a2b5-121">创建文本文件并向其中写入数据</span><span class="sxs-lookup"><span data-stu-id="5a2b5-121">Creating a Text File and Writing Data to It</span></span>

<span data-ttu-id="5a2b5-122">除了在网站中使用数据库之外，您还可以使用文件。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-122">In addition to using a database in your website, you might work with files.</span></span> <span data-ttu-id="5a2b5-123">例如，您可以使用文本文件作为存储站点数据的一种简单方法。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-123">For example, you might use text files as a simple way to store data for the site.</span></span> <span data-ttu-id="5a2b5-124">（用于存储数据的文本文件有时称为 "*平面文件*"。）文本文件可以采用不同的格式，如 *.txt*、 *.xml*或 *.csv* （逗号分隔的值）。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-124">(A text file that's used to store data is sometimes called a *flat file*.) Text files can be in different formats, like *.txt*, *.xml*, or *.csv* (comma-delimited values).</span></span>

<span data-ttu-id="5a2b5-125">如果要将数据存储在文本文件中，可以使用 `File.WriteAllText` 方法来指定要创建的文件和要写入的数据。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-125">If you want to store data in a text file, you can use the `File.WriteAllText` method to specify the file to create and the data to write to it.</span></span> <span data-ttu-id="5a2b5-126">在此过程中，您将创建一个页面，其中包含一个简单窗体，其中包含三个 `input` 元素（名字、姓氏和电子邮件地址）和**提交**按钮。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-126">In this procedure, you'll create a page that contains a simple form with three `input` elements (first name, last name, and email address) and a **Submit** button.</span></span> <span data-ttu-id="5a2b5-127">当用户提交窗体时，将在文本文件中存储用户的输入。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-127">When the user submits the form, you'll store the user's input in a text file.</span></span>

1. <span data-ttu-id="5a2b5-128">创建名为 "*应用\_* " 的新文件夹（如果它尚不存在）。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-128">Create a new folder named *App\_Data*, if it doesn't exist already.</span></span>
2. <span data-ttu-id="5a2b5-129">在网站的根目录中，创建一个名为 " *UserData*" 的新文件。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-129">At the root of your website, create a new file named *UserData.cshtml*.</span></span>
3. <span data-ttu-id="5a2b5-130">将现有内容替换为以下内容：</span><span class="sxs-lookup"><span data-stu-id="5a2b5-130">Replace the existing content with the following:</span></span> 

    [!code-cshtml[Main](working-with-files/samples/sample1.cshtml)]

    <span data-ttu-id="5a2b5-131">HTML 标记将创建包含三个文本框的窗体。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-131">The HTML markup creates the form with the three text boxes.</span></span> <span data-ttu-id="5a2b5-132">在代码中，可以使用 `IsPost` 属性来确定是否已在开始处理前提交了页面。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-132">In the code, you use the `IsPost` property to determine whether the page has been submitted before you start processing.</span></span>

    <span data-ttu-id="5a2b5-133">第一个任务是获取用户输入并将其分配给变量。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-133">The first task is to get the user input and assign it to variables.</span></span> <span data-ttu-id="5a2b5-134">然后，该代码将单独变量的值连接为一个逗号分隔的字符串，然后将其存储在不同的变量中。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-134">The code then concatenates the values of the separate variables into one comma-delimited string, which is then stored in a different variable.</span></span> <span data-ttu-id="5a2b5-135">请注意，逗号分隔符是引号（"，"）中包含的字符串，因为你要将逗号嵌入到所创建的大字符串。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-135">Notice that the comma separator is a string contained in quotation marks (","), because you're literally embedding a comma into the big string that you're creating.</span></span> <span data-ttu-id="5a2b5-136">在连接在一起的数据的末尾，添加 `Environment.NewLine`。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-136">At the end of the data that you concatenate together, you add `Environment.NewLine`.</span></span> <span data-ttu-id="5a2b5-137">这将添加换行符（换行符）。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-137">This adds a line break (a newline character).</span></span> <span data-ttu-id="5a2b5-138">所有此类连接所创建的内容是一个如下所示的字符串：</span><span class="sxs-lookup"><span data-stu-id="5a2b5-138">What you're creating with all this concatenation is a string that looks like this:</span></span>

    [!code-css[Main](working-with-files/samples/sample2.css)]

    <span data-ttu-id="5a2b5-139">（末尾有一个不可见的换行符。）</span><span class="sxs-lookup"><span data-stu-id="5a2b5-139">(With an invisible line break at the end.)</span></span>

    <span data-ttu-id="5a2b5-140">然后创建一个变量（`dataFile`），其中包含要在其中存储数据的文件的位置和名称。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-140">You then create a variable (`dataFile`) that contains the location and name of the file to store the data in.</span></span> <span data-ttu-id="5a2b5-141">设置位置需要一些特殊处理。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-141">Setting the location requires some special handling.</span></span> <span data-ttu-id="5a2b5-142">在网站中，将代码引用为 web 服务器*上的文件*的绝对路径是一种不好的做法。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-142">In websites, it's a bad practice to refer in code to absolute paths like *C:\Folder\File.txt* for files on the web server.</span></span> <span data-ttu-id="5a2b5-143">如果移动了某个网站，则绝对路径将会出错。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-143">If a website is moved, an absolute path will be wrong.</span></span> <span data-ttu-id="5a2b5-144">此外，对于托管站点（而不是在您自己的计算机上），通常您在编写代码时，您甚至不知道正确的路径。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-144">Moreover, for a hosted site (as opposed to on your own computer) you typically don't even know what the correct path is when you're writing the code.</span></span>

    <span data-ttu-id="5a2b5-145">但有时（如现在写入文件）需要完整的路径。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-145">But sometimes (like now, for writing a file) you do need a complete path.</span></span> <span data-ttu-id="5a2b5-146">解决方案是使用 `Server` 对象的 `MapPath` 方法。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-146">The solution is to use the `MapPath` method of the `Server` object.</span></span> <span data-ttu-id="5a2b5-147">这会返回网站的完整路径。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-147">This returns the complete path to your website.</span></span> <span data-ttu-id="5a2b5-148">若要获取网站根的路径，请将 `~` 运算符（要 represen 网站的虚拟根目录）的用户 `MapPath`。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-148">To get the path for the website root, you user the `~` operator (to represen the site's virtual root) to `MapPath`.</span></span> <span data-ttu-id="5a2b5-149">（还可以向其传递子文件夹名称，例如 *~/App\_Data/* ）以获取该子文件夹的路径。）然后，可以将附加信息连接到方法返回的任何内容，以创建完整的路径。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-149">(You can also pass a subfolder name to it, like *~/App\_Data/*, to get the path for that subfolder.) You can then concatenate additional information onto whatever the method returns in order to create a complete path.</span></span> <span data-ttu-id="5a2b5-150">在此示例中，将添加文件名。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-150">In this example, you add a file name.</span></span> <span data-ttu-id="5a2b5-151">（有关如何处理文件和文件夹路径的详细信息，请参阅[使用 Razor 语法 ASP.NET 网页编程](https://go.microsoft.com/fwlink/?LinkId=195205#ID_WorkingWithFileAndFolderPaths)。）</span><span class="sxs-lookup"><span data-stu-id="5a2b5-151">(You can read more about how to work with file and folder paths in [Introduction to ASP.NET Web Pages Programming Using the Razor Syntax](https://go.microsoft.com/fwlink/?LinkId=195205#ID_WorkingWithFileAndFolderPaths).)</span></span>

    <span data-ttu-id="5a2b5-152">该文件保存在*应用\_Data*文件夹中。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-152">The file is saved in the *App\_Data* folder.</span></span> <span data-ttu-id="5a2b5-153">此文件夹是 ASP.NET 中的一个特殊文件夹，用于存储数据文件，如在[ASP.NET 网页网站中使用数据库简介](https://go.microsoft.com/fwlink/?LinkId=195209)中所述。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-153">This folder is a special folder in ASP.NET that's used to store data files, as described in [Introduction to Working with a Database in ASP.NET Web Pages Sites](https://go.microsoft.com/fwlink/?LinkId=195209).</span></span>

    <span data-ttu-id="5a2b5-154">`File` 对象的 `WriteAllText` 方法将数据写入文件。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-154">The `WriteAllText` method of the `File` object writes the data to the file.</span></span> <span data-ttu-id="5a2b5-155">此方法采用两个参数：要写入的文件的名称（包含路径）以及要写入的实际数据。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-155">This method takes two parameters: the name (with path) of the file to write to, and the actual data to write.</span></span> <span data-ttu-id="5a2b5-156">请注意，第一个参数的名称包含 `@` 字符作为前缀。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-156">Notice that the name of the first parameter has an `@` character as a prefix.</span></span> <span data-ttu-id="5a2b5-157">这会告知 ASP.NET 你正在提供逐字字符串文本，并且不应以特殊方式解释 "/" 之类的字符。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-157">This tells ASP.NET that you're providing a verbatim string literal, and that characters like "/" should not be interpreted in special ways.</span></span> <span data-ttu-id="5a2b5-158">（有关详细信息，请参阅[使用 Razor 语法的 ASP.NET Web 编程简介](https://go.microsoft.com/fwlink/?LinkId=195205#ID_WorkingWithFileAndFolderPaths)。）</span><span class="sxs-lookup"><span data-stu-id="5a2b5-158">(For more information, see [Introduction to ASP.NET Web Programming Using the Razor Syntax](https://go.microsoft.com/fwlink/?LinkId=195205#ID_WorkingWithFileAndFolderPaths).)</span></span>

    > [!NOTE]
    > <span data-ttu-id="5a2b5-159">为了使你的代码将文件保存到*应用\_Data*文件夹中，应用程序需要对该文件夹具有读写权限。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-159">In order for your code to save files in the *App\_Data* folder, the application needs read-write permissions for that folder.</span></span> <span data-ttu-id="5a2b5-160">在您的开发计算机上，这通常不是问题。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-160">On your development computer this is not typically an issue.</span></span> <span data-ttu-id="5a2b5-161">但是，当你将网站发布到宿主提供程序的 web 服务器时，可能需要显式设置这些权限。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-161">However, when you publish your site to a hosting provider's web server, you might need to explicitly set those permissions.</span></span> <span data-ttu-id="5a2b5-162">如果在宿主提供程序的服务器上运行此代码并收到错误，请与宿主提供程序联系，以了解如何设置这些权限。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-162">If you run this code on a hosting provider's server and get errors, check with the hosting provider to find out how to set those permissions.</span></span>

- <span data-ttu-id="5a2b5-163">在浏览器中运行页。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-163">Run the page in a browser.</span></span> 

    ![](working-with-files/_static/image1.jpg)
- <span data-ttu-id="5a2b5-164">在字段中输入值，然后单击 "**提交**"。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-164">Enter values into the fields and then click **Submit**.</span></span>
- <span data-ttu-id="5a2b5-165">关闭浏览器。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-165">Close the browser.</span></span>
- <span data-ttu-id="5a2b5-166">返回到项目并刷新视图。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-166">Return to the project and refresh the view.</span></span>
- <span data-ttu-id="5a2b5-167">打开 "*数据 .txt* " 文件。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-167">Open the *data.txt* file.</span></span> <span data-ttu-id="5a2b5-168">您在表单中提交的数据在文件中。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-168">The data you submitted in the form is in the file.</span></span> 

    ![[图像]](working-with-files/_static/image2.jpg)
- <span data-ttu-id="5a2b5-170">关闭 "*数据 .txt* " 文件。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-170">Close the *data.txt* file.</span></span>

<a id="Appending_Data"></a>
## <a name="appending-data-to-an-existing-file"></a><span data-ttu-id="5a2b5-171">将数据追加到现有文件</span><span class="sxs-lookup"><span data-stu-id="5a2b5-171">Appending Data to an Existing File</span></span>

<span data-ttu-id="5a2b5-172">在上面的示例中，你使用 `WriteAllText` 创建一个文本文件，该文件中仅有一个数据块。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-172">In the previous example, you used `WriteAllText` to create a text file that's got just one piece of data in it.</span></span> <span data-ttu-id="5a2b5-173">如果再次调用方法并向其传递相同的文件名，则会完全覆盖现有文件。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-173">If you call the method again and pass it the same file name, the existing file is completely overwritten.</span></span> <span data-ttu-id="5a2b5-174">但是，创建文件后，通常需要将新数据添加到文件末尾。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-174">However, after you've created a file you often want to add new data to the end of the file.</span></span> <span data-ttu-id="5a2b5-175">您可以使用 `File` 对象的 `AppendAllText` 方法执行此操作。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-175">You can do that using the `AppendAllText` method of the `File` object.</span></span>

1. <span data-ttu-id="5a2b5-176">在网站中，创建一个*UserData*文件文件的副本，并将其命名为*UserDataMultiple*。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-176">In the website, make a copy of the *UserData.cshtml* file and name the copy *UserDataMultiple.cshtml*.</span></span>
2. <span data-ttu-id="5a2b5-177">用下面的代码块替换开始 `<!DOCTYPE html>` 标记前面的代码块：</span><span class="sxs-lookup"><span data-stu-id="5a2b5-177">Replace the code block before the opening `<!DOCTYPE html>` tag with the following code block:</span></span> 

    [!code-cshtml[Main](working-with-files/samples/sample3.cshtml)]

    <span data-ttu-id="5a2b5-178">此代码在前面的示例中有一个更改。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-178">This code has one change in it from the previous example.</span></span> <span data-ttu-id="5a2b5-179">它使用 `the AppendAllText` 方法，而不是使用 `WriteAllText`。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-179">Instead of using `WriteAllText`, it uses `the AppendAllText` method.</span></span> <span data-ttu-id="5a2b5-180">方法类似，不同之处在于 `AppendAllText` 将数据添加到文件末尾。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-180">The methods are similar, except that `AppendAllText` adds the data to the end of the file.</span></span> <span data-ttu-id="5a2b5-181">与 `WriteAllText`一样，`AppendAllText` 会创建文件（如果该文件尚不存在）。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-181">As with `WriteAllText`, `AppendAllText` creates the file if it doesn't already exist.</span></span>
3. <span data-ttu-id="5a2b5-182">在浏览器中运行页。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-182">Run the page in a browser.</span></span>
4. <span data-ttu-id="5a2b5-183">输入字段的值，然后单击 "**提交**"。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-183">Enter values for the fields and then click **Submit**.</span></span>
5. <span data-ttu-id="5a2b5-184">添加更多数据，然后重新提交表单。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-184">Add more data and submit the form again.</span></span>
6. <span data-ttu-id="5a2b5-185">返回到你的项目，右键单击项目文件夹，然后单击 "**刷新**"。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-185">Return to your project, right-click the project folder, and then click **Refresh**.</span></span>
7. <span data-ttu-id="5a2b5-186">打开 "*数据 .txt* " 文件。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-186">Open the *data.txt* file.</span></span> <span data-ttu-id="5a2b5-187">它现在包含刚输入的新数据。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-187">It now contains the new data that you just entered.</span></span> 

    ![[图像]](working-with-files/_static/image3.jpg)

<a id="Reading_and_Displaying_Data"></a>
## <a name="reading-and-displaying-data-from-a-file"></a><span data-ttu-id="5a2b5-189">读取和显示文件中的数据</span><span class="sxs-lookup"><span data-stu-id="5a2b5-189">Reading and Displaying Data from a File</span></span>

<span data-ttu-id="5a2b5-190">即使不需要将数据写入文本文件，有时也可能需要从一个文件中读取数据。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-190">Even if you don't need to write data to a text file, you'll probably sometimes need to read data from one.</span></span> <span data-ttu-id="5a2b5-191">为此，可以再次使用 `File` 对象。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-191">To do this, you can again use the `File` object.</span></span> <span data-ttu-id="5a2b5-192">您可以使用 `File` 对象单独读取每个行（用换行符分隔），也可以使用来读取单独的项，而不管它们是如何分离的。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-192">You can use the `File` object to read each line individually (separated by line breaks) or to read individual item no matter how they're separated.</span></span>

<span data-ttu-id="5a2b5-193">此过程说明如何读取和显示在前面的示例中创建的数据。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-193">This procedure shows you how to read and display the data that you created in the previous example.</span></span>

1. <span data-ttu-id="5a2b5-194">在网站的根目录中，创建一个名为*DisplayData*的新文件。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-194">At the root of your website, create a new file named *DisplayData.cshtml*.</span></span>
2. <span data-ttu-id="5a2b5-195">将现有内容替换为以下内容：</span><span class="sxs-lookup"><span data-stu-id="5a2b5-195">Replace the existing content with the following:</span></span> 

    [!code-cshtml[Main](working-with-files/samples/sample4.cshtml)]

    <span data-ttu-id="5a2b5-196">代码首先，使用此方法调用，将在上一示例中创建的文件读入名为 `userData`的变量：</span><span class="sxs-lookup"><span data-stu-id="5a2b5-196">The code starts by reading the file that you created in the previous example into a variable named `userData`, using this method call:</span></span>

    [!code-css[Main](working-with-files/samples/sample5.css)]

    <span data-ttu-id="5a2b5-197">用于执行此操作的代码位于 `if` 语句中。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-197">The code to do this is inside an `if` statement.</span></span> <span data-ttu-id="5a2b5-198">当您想要读取某个文件时，最好使用 `File.Exists` 方法来确定该文件是否可用。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-198">When you want to read a file, it's a good idea to use the `File.Exists` method to determine first whether the file is available.</span></span> <span data-ttu-id="5a2b5-199">此代码还会检查文件是否为空。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-199">The code also checks whether the file is empty.</span></span>

    <span data-ttu-id="5a2b5-200">页面的主体包含两个 `foreach` 循环，一个嵌套在另一个中。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-200">The body of the page contains two `foreach` loops, one nested inside the other.</span></span> <span data-ttu-id="5a2b5-201">外部 `foreach` 循环一次从数据文件中获取一行。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-201">The outer `foreach` loop gets one line at a time from the data file.</span></span> <span data-ttu-id="5a2b5-202">在这种情况下，行是由文件&#8212;中的分行符定义的，每个数据项都在单独的行中。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-202">In this case, the lines are defined by line breaks in the file &#8212; that is, each data item is on its own line.</span></span> <span data-ttu-id="5a2b5-203">外部循环在排序列表（`<ol>` 元素）中创建新项（`<li>` 元素）。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-203">The outer loop creates a new item (`<li>` element) inside an ordered list (`<ol>` element).</span></span>

    <span data-ttu-id="5a2b5-204">内部循环使用逗号作为分隔符将每个数据行拆分为多个项（字段）。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-204">The inner loop splits each data line into items (fields) using a comma as a delimiter.</span></span> <span data-ttu-id="5a2b5-205">（基于前面的示例，这意味着每一行都包含三个字段&#8212; ：名字、姓氏和电子邮件地址，每个字段用逗号分隔。）内部循环还创建 `<ul>` 列表，并为数据行中的每个字段显示一个列表项。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-205">(Based on the previous example, this means that each line contains three fields &#8212; the first name, last name, and email address, each separated by a comma.) The inner loop also creates a `<ul>` list and displays one list item for each field in the data line.</span></span>

    <span data-ttu-id="5a2b5-206">此代码演示如何使用两种数据类型：数组和 `char` 数据类型。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-206">The code illustrates how to use two data types, an array and the `char` data type.</span></span> <span data-ttu-id="5a2b5-207">数组是必需的，因为 `File.ReadAllLines` 方法以数组形式返回数据。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-207">The array is required because the `File.ReadAllLines` method returns data as an array.</span></span> <span data-ttu-id="5a2b5-208">`char` 的数据类型是必需的，因为 `Split` 方法返回 `array`，其中每个元素都是 `char`类型。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-208">The `char` data type is required because the `Split` method returns an `array` in which each element is of the type `char`.</span></span> <span data-ttu-id="5a2b5-209">（有关数组的信息，请参阅[使用 Razor 语法的 ASP.NET Web 编程简介](https://go.microsoft.com/fwlink/?LinkId=202890#ID_CollectionsAndObjects)。）</span><span class="sxs-lookup"><span data-stu-id="5a2b5-209">(For information about arrays, see [Introduction to ASP.NET Web Programming Using the Razor Syntax](https://go.microsoft.com/fwlink/?LinkId=202890#ID_CollectionsAndObjects).)</span></span>
3. <span data-ttu-id="5a2b5-210">在浏览器中运行页。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-210">Run the page in a browser.</span></span> <span data-ttu-id="5a2b5-211">将显示您为前面的示例输入的数据。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-211">The data you entered for the previous examples is displayed.</span></span> 

    ![[图像]](working-with-files/_static/image4.jpg)

> [!TIP] 
> 
> <span data-ttu-id="5a2b5-213">**显示以逗号分隔的 Microsoft Excel 文件中的数据**</span><span class="sxs-lookup"><span data-stu-id="5a2b5-213">**Displaying Data from a Microsoft Excel Comma-Delimited File**</span></span>
> 
> <span data-ttu-id="5a2b5-214">您可以使用 Microsoft Excel 将电子表格中包含的数据另存为逗号分隔的文件（ *.csv*文件）。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-214">You can use Microsoft Excel to save the data contained in a spreadsheet as a comma-delimited file (*.csv* file).</span></span> <span data-ttu-id="5a2b5-215">当你执行此操作时，文件将以纯文本格式保存，而不是以 Excel 格式保存。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-215">When you do, the file is saved in plain text, not in Excel format.</span></span> <span data-ttu-id="5a2b5-216">电子表格中的每一行都用文本文件中的换行符分隔，每个数据项用逗号分隔。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-216">Each row in the spreadsheet is separated by a line break in the text file, and each data item is separated by a comma.</span></span> <span data-ttu-id="5a2b5-217">您可以使用上一示例中所示的代码，只需在代码中更改数据文件的名称，即可读取 Excel 逗号分隔的文件。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-217">You can use the code shown in the previous example to read an Excel comma-delimited file just by changing the name of the data file in your code.</span></span>

<a id="Deleting_Files"></a>
## <a name="deleting-files"></a><span data-ttu-id="5a2b5-218">删除文件</span><span class="sxs-lookup"><span data-stu-id="5a2b5-218">Deleting Files</span></span>

<span data-ttu-id="5a2b5-219">若要从您的网站删除文件，您可以使用 `File.Delete` 方法。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-219">To delete files from your website, you can use the `File.Delete` method.</span></span> <span data-ttu-id="5a2b5-220">此过程说明如何允许用户从*images*文件夹中删除图像（ *.jpg*文件），前提是他们知道文件的名称。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-220">This procedure shows how to let users delete an image (*.jpg* file) from an *images* folder if they know the name of the file.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="5a2b5-221">**重要提示**在生产网站中，通常会限制允许对数据进行更改的人员。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-221">**Important** In a production website, you typically restrict who's allowed to make changes to the data.</span></span> <span data-ttu-id="5a2b5-222">有关如何设置成员身份和授权用户在网站上执行任务的方式的信息，请参阅向[ASP.NET 网页站点添加安全性和成员身份](https://go.microsoft.com/fwlink/?LinkId=202904)。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-222">For information about how to set up membership and about ways to authorize users to perform tasks on the site, see [Adding Security and Membership to an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=202904).</span></span>

1. <span data-ttu-id="5a2b5-223">在网站中，创建一个名为*images*的子文件夹。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-223">In the website, create a subfolder named *images*.</span></span>
2. <span data-ttu-id="5a2b5-224">将一个或多个 *.jpg*文件复制到*images*文件夹中。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-224">Copy one or more *.jpg* files into the *images* folder.</span></span>
3. <span data-ttu-id="5a2b5-225">在网站的根目录中，创建一个名为*FileDelete*的新文件。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-225">In the root of the website, create a new file named *FileDelete.cshtml*.</span></span>
4. <span data-ttu-id="5a2b5-226">将现有内容替换为以下内容：</span><span class="sxs-lookup"><span data-stu-id="5a2b5-226">Replace the existing content with the following:</span></span> 

    [!code-cshtml[Main](working-with-files/samples/sample6.cshtml)]

    <span data-ttu-id="5a2b5-227">此页面包含一个窗体，用户可以在其中输入图像文件的名称。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-227">This page contains a form where users can enter the name of an image file.</span></span> <span data-ttu-id="5a2b5-228">它们不会输入 *.jpg*文件扩展名;通过限制此名称，你可以帮助防止用户删除站点上的任意文件。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-228">They don't enter the *.jpg* file-name extension; by restricting the file name like this, you help prevents users from deleting arbitrary files on your site.</span></span>

    <span data-ttu-id="5a2b5-229">此代码读取用户输入的文件名，然后构造完整的路径。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-229">The code reads the file name that the user has entered and then constructs a complete path.</span></span> <span data-ttu-id="5a2b5-230">若要创建路径，代码将使用当前网站路径（由 `Server.MapPath` 方法返回）、*图像*文件夹名称、用户提供的名称和作为文本字符串的 ".jpg"。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-230">To create the path, the code uses the current website path (as returned by the `Server.MapPath` method), the *images* folder name, the name that the user has provided, and ".jpg" as a literal string.</span></span>

    <span data-ttu-id="5a2b5-231">若要删除该文件，代码将调用 `File.Delete` 方法，并向其传递您刚刚构造的完整路径。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-231">To delete the file, the code calls the `File.Delete` method, passing it the full path that you just constructed.</span></span> <span data-ttu-id="5a2b5-232">标记结束时，代码将显示一条确认消息，指出该文件已被删除。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-232">At the end of the markup, code displays a confirmation message that the file was deleted.</span></span>
5. <span data-ttu-id="5a2b5-233">在浏览器中运行页。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-233">Run the page in a browser.</span></span> 

    ![[图像]](working-with-files/_static/image5.jpg)
6. <span data-ttu-id="5a2b5-235">输入要删除的文件的名称，然后单击 "**提交**"。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-235">Enter the name of the file to delete and then click **Submit**.</span></span> <span data-ttu-id="5a2b5-236">如果已删除该文件，则该文件的名称将显示在该页的底部。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-236">If the file was deleted, the name of the file is displayed at the bottom of the page.</span></span>

<a id="Letting_Users_Upload_a_File"></a>
## <a name="letting-users-upload-a-file"></a><span data-ttu-id="5a2b5-237">允许用户上传文件</span><span class="sxs-lookup"><span data-stu-id="5a2b5-237">Letting Users Upload a File</span></span>

<span data-ttu-id="5a2b5-238">`FileUpload` 帮助器允许用户将文件上传到你的网站。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-238">The `FileUpload` helper lets users upload files to your website.</span></span> <span data-ttu-id="5a2b5-239">下面的过程演示如何让用户上传单个文件。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-239">The procedure below shows you how to let users upload a single file.</span></span>

1. <span data-ttu-id="5a2b5-240">如在[ASP.NET 网页站点中安装帮助程序](https://go.microsoft.com/fwlink/?LinkId=252372)中所述，将 ASP.NET Web 帮助程序库添加到你的网站中（如果你之前未添加）。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-240">Add the ASP.NET Web Helpers Library to your website as described in [Installing Helpers in an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=252372), if you didn't add it previously.</span></span>
2. <span data-ttu-id="5a2b5-241">在*应用\_Data*文件夹中，创建一个新文件夹并将其命名为*UploadedFiles*。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-241">In the *App\_Data* folder, create a new a folder and name it *UploadedFiles*.</span></span>
3. <span data-ttu-id="5a2b5-242">在根目录中，创建一个名为*FileUpload*的新文件。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-242">In the root, create a new file named *FileUpload.cshtml*.</span></span>
4. <span data-ttu-id="5a2b5-243">将页面中的现有内容替换为以下内容：</span><span class="sxs-lookup"><span data-stu-id="5a2b5-243">Replace the existing content in the page with the following:</span></span> 

    [!code-cshtml[Main](working-with-files/samples/sample7.cshtml)]

    <span data-ttu-id="5a2b5-244">页面的正文部分使用 `FileUpload` 帮助器创建你可能熟悉的 "上传" 框和按钮：</span><span class="sxs-lookup"><span data-stu-id="5a2b5-244">The body portion of the page uses the `FileUpload` helper to create the upload box and buttons that you're probably familiar with:</span></span>

    ![[图像]](working-with-files/_static/image6.jpg)

    <span data-ttu-id="5a2b5-246">你为 `FileUpload` 帮助程序设置的属性指定希望文件上传单个框，并且你希望 "提交" 按钮读取**上传**。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-246">The properties that you set for the `FileUpload` helper specify that you want a single box for the file to upload and that you want the submit button to read **Upload**.</span></span> <span data-ttu-id="5a2b5-247">（稍后将添加更多的框。）</span><span class="sxs-lookup"><span data-stu-id="5a2b5-247">(You'll add more boxes later in the article.)</span></span>

    <span data-ttu-id="5a2b5-248">当用户单击 "**上传**" 时，页面顶部的代码将获取文件并将其保存。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-248">When the user clicks **Upload**, the code at the top of the page gets the file and saves it.</span></span> <span data-ttu-id="5a2b5-249">通常用于从窗体字段获取值的 `Request` 对象还具有一个包含已上传的文件（或文件）的 `Files` 数组。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-249">The `Request` object that you normally use to get values from form fields also has a `Files` array that contains the file (or files) that have been uploaded.</span></span> <span data-ttu-id="5a2b5-250">您可以获取数组&#8212;中特定位置的单个文件，例如，获取第一个上载的文件，获取 `Request.Files[0]`，获取第二个文件，您将获得 `Request.Files[1]`等。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-250">You can get individual files out of specific positions in the array &#8212; for example, to get the first uploaded file, you get `Request.Files[0]`, to get the second file, you get `Request.Files[1]`, and so on.</span></span> <span data-ttu-id="5a2b5-251">（请记住，在编程中，计数通常从零开始。）</span><span class="sxs-lookup"><span data-stu-id="5a2b5-251">(Remember that in programming, counting usually starts at zero.)</span></span>

    <span data-ttu-id="5a2b5-252">提取已上传的文件时，将其放在变量（此处为 `uploadedFile`）中，以便可以对其进行操作。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-252">When you fetch an uploaded file, you put it in a variable (here, `uploadedFile`) so that you can manipulate it.</span></span> <span data-ttu-id="5a2b5-253">若要确定上传的文件的名称，只需获取其 `FileName` 属性即可。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-253">To determine the name of the uploaded file, you just get its `FileName` property.</span></span> <span data-ttu-id="5a2b5-254">但是，当用户上传文件时，`FileName` 包含用户的原始名称，其中包括整个路径。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-254">However, when the user uploads a file, `FileName` contains the user's original name, which includes the entire path.</span></span> <span data-ttu-id="5a2b5-255">它可能如下所示：</span><span class="sxs-lookup"><span data-stu-id="5a2b5-255">It might look like this:</span></span>

    <span data-ttu-id="5a2b5-256">*C:\Users\Public\Sample.txt*</span><span class="sxs-lookup"><span data-stu-id="5a2b5-256">*C:\Users\Public\Sample.txt*</span></span>

    <span data-ttu-id="5a2b5-257">但不想要所有的路径信息，因为这是用户计算机上的路径，而不是服务器的路径。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-257">You don't want all that path information, though, because that's the path on the user's computer, not for your server.</span></span> <span data-ttu-id="5a2b5-258">只需要实际的文件名（*Sample .txt*）。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-258">You just want the actual file name (*Sample.txt*).</span></span> <span data-ttu-id="5a2b5-259">可以通过使用 `Path.GetFileName` 方法仅去除路径中的文件，如下所示：</span><span class="sxs-lookup"><span data-stu-id="5a2b5-259">You can strip out just the file from a path by using the `Path.GetFileName` method, like this:</span></span>

    [!code-csharp[Main](working-with-files/samples/sample8.cs)]

    <span data-ttu-id="5a2b5-260">`Path` 对象是一个实用工具，其中包含许多方法，您可以使用这些方法来分割路径、组合路径等。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-260">The `Path` object is a utility that has a number of methods like this that you can use to strip paths, combine paths, and so on.</span></span>

    <span data-ttu-id="5a2b5-261">获取上传的文件的名称后，可以在网站中创建要将上传的文件存储到的位置的新路径。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-261">Once you've gotten the name of the uploaded file, you can build a new path for where you want to store the uploaded file in your website.</span></span> <span data-ttu-id="5a2b5-262">在这种情况下，你将 `Server.MapPath`、文件夹名称（*应用\_Data/UploadedFiles*）组合在一起，以创建新路径。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-262">In this case, you combine `Server.MapPath`, the folder names (*App\_Data/UploadedFiles*), and the newly stripped file name to create a new path.</span></span> <span data-ttu-id="5a2b5-263">然后，可以调用上传的文件的 `SaveAs` 方法来实际保存该文件。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-263">You can then call the uploaded file's `SaveAs` method to actually save the file.</span></span>
5. <span data-ttu-id="5a2b5-264">在浏览器中运行页。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-264">Run the page in a browser.</span></span> 

    ![[图像]](working-with-files/_static/image7.jpg)
6. <span data-ttu-id="5a2b5-266">单击 "**浏览**"，然后选择要上载的文件。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-266">Click **Browse** and then select a file to upload.</span></span> 

    ![[图像]](working-with-files/_static/image8.jpg)

    <span data-ttu-id="5a2b5-268">"**浏览**" 按钮旁边的文本框将包含路径和文件位置。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-268">The text box next to the **Browse** button will contain the path and file location.</span></span>

    ![[图像]](working-with-files/_static/image9.jpg)
7. <span data-ttu-id="5a2b5-270">单击“上载”。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-270">Click **Upload**.</span></span>
8. <span data-ttu-id="5a2b5-271">在网站中，右键单击项目文件夹，然后单击 "**刷新**"。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-271">In the website, right-click the project folder and then click **Refresh**.</span></span>
9. <span data-ttu-id="5a2b5-272">打开*UploadedFiles*文件夹。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-272">Open the *UploadedFiles* folder.</span></span> <span data-ttu-id="5a2b5-273">你上载的文件位于文件夹中。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-273">The file that you uploaded is in the folder.</span></span> 

    ![[图像]](working-with-files/_static/image10.jpg)

<a id="Letting_Users_Upload_Multiple_Files"></a>
## <a name="letting-users-upload-multiple-files"></a><span data-ttu-id="5a2b5-275">允许用户上传多个文件</span><span class="sxs-lookup"><span data-stu-id="5a2b5-275">Letting Users Upload Multiple Files</span></span>

<span data-ttu-id="5a2b5-276">在上面的示例中，允许用户上传一个文件。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-276">In the previous example, you let users upload one file.</span></span> <span data-ttu-id="5a2b5-277">但你可以使用 `FileUpload` 帮助程序一次上载多个文件。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-277">But you can use the `FileUpload` helper to upload more than one file at a time.</span></span> <span data-ttu-id="5a2b5-278">这对于上传照片的方案非常方便，其中一次上传一个文件会很繁琐。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-278">This is handy for scenarios like uploading photos, where uploading one file at a time is tedious.</span></span> <span data-ttu-id="5a2b5-279">（您可以阅读有关在使用[ASP.NET 网页网站中的图像时](https://go.microsoft.com/fwlink/?LinkId=202897)上载照片的信息。）此示例演示如何允许用户一次上传两个，但你可以使用相同的技术来上传。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-279">(You can read about uploading photos in [Working with Images in an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=202897).) This example shows how to let users upload two at a time, although you can use the same technique to upload more than that.</span></span>

1. <span data-ttu-id="5a2b5-280">根据在[ASP.NET 网页站点中安装帮助程序](https://go.microsoft.com/fwlink/?LinkId=252372)中所述，将 ASP.NET Web 帮助程序库添加到你的网站中（如果尚未安装）。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-280">Add the ASP.NET Web Helpers Library to your website as described in [Installing Helpers in an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=252372), if you haven't already.</span></span>
2. <span data-ttu-id="5a2b5-281">创建名为*FileUploadMultiple*的新页面。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-281">Create a new page named *FileUploadMultiple.cshtml*.</span></span>
3. <span data-ttu-id="5a2b5-282">将页面中的现有内容替换为以下内容：</span><span class="sxs-lookup"><span data-stu-id="5a2b5-282">Replace the existing content in the page with the following:</span></span>  

    [!code-cshtml[Main](working-with-files/samples/sample9.cshtml)]

    <span data-ttu-id="5a2b5-283">在此示例中，页面正文中的 `FileUpload` 帮助程序配置为允许用户在默认情况下上传两个文件。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-283">In this example, the `FileUpload` helper in the body of the page is configured to let users upload two files by default.</span></span> <span data-ttu-id="5a2b5-284">由于 `allowMoreFilesToBeAdded` 设置为 `true`，因此帮助器将呈现允许用户添加更多上传框的链接：</span><span class="sxs-lookup"><span data-stu-id="5a2b5-284">Because `allowMoreFilesToBeAdded` is set to `true`, the helper renders a link that lets user add more upload boxes:</span></span>

    ![[图像]](working-with-files/_static/image11.jpg)

    <span data-ttu-id="5a2b5-286">若要处理用户上传的文件，代码将使用上一示例&#8212;中所用的相同基本方法从 `Request.Files` 获取文件，然后保存该文件。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-286">To process the files that the user uploads, the code uses the same basic technique that you used in the previous example &#8212; get a file from `Request.Files` and then save it.</span></span> <span data-ttu-id="5a2b5-287">（包括获得正确的文件名和路径所需的各种功能。）在这种情况下，用户可能会上载多个文件，而你不知道很多。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-287">(Including the various things you need to do to get the right file name and path.) The innovation this time is that the user might be uploading multiple files and you don't know many.</span></span> <span data-ttu-id="5a2b5-288">若要了解，你可以获取 `Request.Files.Count`。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-288">To find out, you can get `Request.Files.Count`.</span></span>

    <span data-ttu-id="5a2b5-289">使用此数字，可以循环遍历 `Request.Files`，依次提取每个文件并保存。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-289">With this number in hand, you can loop through `Request.Files`, fetch each file in turn, and save it.</span></span> <span data-ttu-id="5a2b5-290">如果要在集合中循环一次已知的次数，可以使用 `for` 循环，如下所示：</span><span class="sxs-lookup"><span data-stu-id="5a2b5-290">When you want to loop a known number of times through a collection, you can use a `for` loop, like this:</span></span>

    [!code-csharp[Main](working-with-files/samples/sample10.cs)]

    <span data-ttu-id="5a2b5-291">变量 `i` 只是一个临时计数器，它将从零到你设置的任何上限。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-291">The variable `i` is just a temporary counter that will go from zero to whatever upper limit you set.</span></span> <span data-ttu-id="5a2b5-292">在这种情况下，上限为文件的数目。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-292">In this case, the upper limit is the number of files.</span></span> <span data-ttu-id="5a2b5-293">但由于计数器从零开始，因此对于在 ASP.NET 中计算方案的典型值，上限实际上比文件计数小1。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-293">But because the counter starts at zero, as is typical for counting scenarios in ASP.NET, the upper limit is actually one less than the file count.</span></span> <span data-ttu-id="5a2b5-294">（如果上传了三个文件，则计数为0到2。）</span><span class="sxs-lookup"><span data-stu-id="5a2b5-294">(If three files are uploaded, the count is zero to 2.)</span></span>

    <span data-ttu-id="5a2b5-295">`uploadedCount` 变量会对已成功上传并保存的所有文件进行总计。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-295">The `uploadedCount` variable totals all the files that are successfully uploaded and saved.</span></span> <span data-ttu-id="5a2b5-296">此代码可能会导致预期的文件无法上传。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-296">This code accounts for the possibility that an expected file may not be able to be uploaded.</span></span>
4. <span data-ttu-id="5a2b5-297">在浏览器中运行页。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-297">Run the page in a browser.</span></span> <span data-ttu-id="5a2b5-298">浏览器将显示该页及其两个上传框。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-298">The browser displays the page and its two upload boxes.</span></span>
5. <span data-ttu-id="5a2b5-299">选择两个要上载的文件。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-299">Select two files to upload.</span></span>
6. <span data-ttu-id="5a2b5-300">单击 "**添加其他文件**"。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-300">Click **Add another file**.</span></span> <span data-ttu-id="5a2b5-301">页面将显示新的上传框。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-301">The page displays a new upload box.</span></span> 

    ![[图像]](working-with-files/_static/image12.jpg)
7. <span data-ttu-id="5a2b5-303">单击“上载”。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-303">Click **Upload**.</span></span>
8. <span data-ttu-id="5a2b5-304">在网站中，右键单击项目文件夹，然后单击 "**刷新**"。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-304">In the website, right-click the project folder and then click **Refresh**.</span></span>
9. <span data-ttu-id="5a2b5-305">打开*UploadedFiles*文件夹，查看是否已成功上传文件。</span><span class="sxs-lookup"><span data-stu-id="5a2b5-305">Open the *UploadedFiles* folder to see the successfully uploaded files.</span></span>

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a><span data-ttu-id="5a2b5-306">其他资源</span><span class="sxs-lookup"><span data-stu-id="5a2b5-306">Additional Resources</span></span>

[<span data-ttu-id="5a2b5-307">使用 ASP.NET 网页站点中的图像</span><span class="sxs-lookup"><span data-stu-id="5a2b5-307">Working with Images in an ASP.NET Web Pages Site</span></span>](https://go.microsoft.com/fwlink/?LinkId=202897)

[<span data-ttu-id="5a2b5-308">导出到 CSV 文件</span><span class="sxs-lookup"><span data-stu-id="5a2b5-308">Exporting to a CSV File</span></span>](https://msdn.microsoft.com/library/ms155919.aspx)
