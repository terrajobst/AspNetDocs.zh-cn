---
uid: mvc/overview/older-versions-1/nerddinner/enable-automated-unit-testing
title: 启用自动单元测试 |Microsoft Docs
author: microsoft
description: 步骤12显示了如何开发一套自动单元测试，用于验证我们的 NerdDinner 功能，并将为我们提供信心来进行更改 。
ms.author: riande
ms.date: 07/27/2010
ms.assetid: a19ff2ce-3f7e-4358-9a51-a1403da9c63e
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/enable-automated-unit-testing
msc.type: authoredcontent
ms.openlocfilehash: 09a7aa186605a6cce48ee94028425ded957c00d3
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78435590"
---
# <a name="enable-automated-unit-testing"></a><span data-ttu-id="b67ec-103">启用自动单元测试</span><span class="sxs-lookup"><span data-stu-id="b67ec-103">Enable Automated Unit Testing</span></span>

<span data-ttu-id="b67ec-104">由[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="b67ec-104">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="b67ec-105">下载 PDF</span><span class="sxs-lookup"><span data-stu-id="b67ec-105">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="b67ec-106">这是免费的["NerdDinner" 应用程序教程](introducing-the-nerddinner-tutorial.md)的步骤12，该教程演示如何使用 ASP.NET MVC 1 构建小型但完整的 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="b67ec-106">This is step 12 of a free ["NerdDinner" application tutorial](introducing-the-nerddinner-tutorial.md) that walks-through how to build a small, but complete, web application using ASP.NET MVC 1.</span></span>
> 
> <span data-ttu-id="b67ec-107">步骤12显示了如何开发一套自动单元测试，这些测试将验证我们的 NerdDinner 功能，并使我们能够在以后对应用程序进行更改和改进。</span><span class="sxs-lookup"><span data-stu-id="b67ec-107">Step 12 shows how to develop a suite of automated unit tests that verify our NerdDinner functionality, and which will give us the confidence to make changes and improvements to the application in the future.</span></span>
> 
> <span data-ttu-id="b67ec-108">如果你使用的是 ASP.NET MVC 3，则建议你遵循[MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)或[Mvc 音乐应用商店](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)教程中的入门。</span><span class="sxs-lookup"><span data-stu-id="b67ec-108">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>

## <a name="nerddinner-step-12-unit-testing"></a><span data-ttu-id="b67ec-109">NerdDinner 步骤12：单元测试</span><span class="sxs-lookup"><span data-stu-id="b67ec-109">NerdDinner Step 12: Unit Testing</span></span>

<span data-ttu-id="b67ec-110">让我们来开发一套自动单元测试，以验证我们的 NerdDinner 功能，这将使我们能够在以后对应用程序进行更改和改进。</span><span class="sxs-lookup"><span data-stu-id="b67ec-110">Let's develop a suite of automated unit tests that verify our NerdDinner functionality, and which will give us the confidence to make changes and improvements to the application in the future.</span></span>

### <a name="why-unit-test"></a><span data-ttu-id="b67ec-111">为什么要进行单元测试？</span><span class="sxs-lookup"><span data-stu-id="b67ec-111">Why Unit Test?</span></span>

<span data-ttu-id="b67ec-112">在该驱动器上，早上，你对正在处理的应用程序的灵感突然闪烁。</span><span class="sxs-lookup"><span data-stu-id="b67ec-112">On the drive into work one morning you have a sudden flash of inspiration about an application you are working on.</span></span> <span data-ttu-id="b67ec-113">你认识到，你可以实现一种更改，这会使应用程序变得更好。</span><span class="sxs-lookup"><span data-stu-id="b67ec-113">You realize there is a change you can implement that will make the application dramatically better.</span></span> <span data-ttu-id="b67ec-114">它可能是一个清理代码、添加新功能或修复 bug 的重构。</span><span class="sxs-lookup"><span data-stu-id="b67ec-114">It might be a refactoring that cleans up the code, adds a new feature, or fixes a bug.</span></span>

<span data-ttu-id="b67ec-115">当你到达计算机时，confronts 你的问题是 "如何安全地实现这一改进？"</span><span class="sxs-lookup"><span data-stu-id="b67ec-115">The question that confronts you when you arrive at your computer is – "how safe is it to make this improvement?"</span></span> <span data-ttu-id="b67ec-116">如果更改有副作用或中断某些内容怎么办？</span><span class="sxs-lookup"><span data-stu-id="b67ec-116">What if making the change has side effects or breaks something?</span></span> <span data-ttu-id="b67ec-117">更改可能很简单，只需几分钟即可完成，但如果手动测试所有应用程序方案需要数小时呢？</span><span class="sxs-lookup"><span data-stu-id="b67ec-117">The change might be simple and only take a few minutes to implement, but what if it takes hours to manually test out all of the application scenarios?</span></span> <span data-ttu-id="b67ec-118">如果您忘记涵盖某个方案并且损坏的应用程序进入生产环境，该怎么办？</span><span class="sxs-lookup"><span data-stu-id="b67ec-118">What if you forget to cover a scenario and a broken application goes into production?</span></span> <span data-ttu-id="b67ec-119">此改进是否确实值得努力？</span><span class="sxs-lookup"><span data-stu-id="b67ec-119">Is making this improvement really worth all the effort?</span></span>

<span data-ttu-id="b67ec-120">自动单元测试可以提供一个安全网络，使你能够持续增强你的应用程序，并避免对你正在处理的代码产生任何担心。</span><span class="sxs-lookup"><span data-stu-id="b67ec-120">Automated unit tests can provide a safety net that enables you to continually enhance your applications, and avoid being afraid of the code you are working on.</span></span> <span data-ttu-id="b67ec-121">通过使自动测试快速验证功能，你可以放心地进行编码，并使你能够更轻松地进行改进。</span><span class="sxs-lookup"><span data-stu-id="b67ec-121">Having automated tests that quickly verify functionality enables you to code with confidence – and empower you to make improvements you might otherwise not have felt comfortable doing.</span></span> <span data-ttu-id="b67ec-122">它们还有助于创建更易于维护的解决方案，并具有较长的生存期-这将导致投资回报率更高。</span><span class="sxs-lookup"><span data-stu-id="b67ec-122">They also help create solutions that are more maintainable and have a longer lifetime - which leads to a much higher return on investment.</span></span>

<span data-ttu-id="b67ec-123">ASP.NET MVC 框架使单元测试应用程序功能变得简单快捷。</span><span class="sxs-lookup"><span data-stu-id="b67ec-123">The ASP.NET MVC Framework makes it easy and natural to unit test application functionality.</span></span> <span data-ttu-id="b67ec-124">它还启用了一个测试驱动开发（TDD）工作流，该工作流启用了测试优先的开发。</span><span class="sxs-lookup"><span data-stu-id="b67ec-124">It also enables a Test Driven Development (TDD) workflow that enables test-first based development.</span></span>

### <a name="nerddinnertests-project"></a><span data-ttu-id="b67ec-125">NerdDinner 项目</span><span class="sxs-lookup"><span data-stu-id="b67ec-125">NerdDinner.Tests Project</span></span>

<span data-ttu-id="b67ec-126">当我们在本教程开始时创建 NerdDinner 应用程序时，会出现一个对话框，询问你是否想要创建单元测试项目来与应用程序项目一起使用：</span><span class="sxs-lookup"><span data-stu-id="b67ec-126">When we created our NerdDinner application at the beginning of this tutorial, we were prompted with a dialog asking whether we wanted to create a unit test project to go along with the application project:</span></span>

![](enable-automated-unit-testing/_static/image1.png)

<span data-ttu-id="b67ec-127">已选中 "是，创建单元测试项目" 单选按钮，这将导致向解决方案中添加 "NerdDinner" 项目：</span><span class="sxs-lookup"><span data-stu-id="b67ec-127">We kept the "Yes, create a unit test project" radio button selected – which resulted in a "NerdDinner.Tests" project being added to our solution:</span></span>

![](enable-automated-unit-testing/_static/image2.png)

<span data-ttu-id="b67ec-128">NerdDinner 项目引用 NerdDinner 应用程序项目程序集，使我们可以轻松地向其添加验证应用程序功能的自动测试。</span><span class="sxs-lookup"><span data-stu-id="b67ec-128">The NerdDinner.Tests project references the NerdDinner application project assembly, and enables us to easily add automated tests to it that verify the application functionality.</span></span>

### <a name="creating-unit-tests-for-our-dinner-model-class"></a><span data-ttu-id="b67ec-129">为晚餐模型类创建单元测试</span><span class="sxs-lookup"><span data-stu-id="b67ec-129">Creating Unit Tests for our Dinner Model Class</span></span>

<span data-ttu-id="b67ec-130">让我们向 NerdDinner 项目添加一些测试，以验证我们在构建模型层时创建的晚餐类。</span><span class="sxs-lookup"><span data-stu-id="b67ec-130">Let's add some tests to our NerdDinner.Tests project that verify the Dinner class we created when we built our model layer.</span></span>

<span data-ttu-id="b67ec-131">首先，我们将在测试项目中创建一个名为 "模型" 的新文件夹，我们将在其中放置模型相关的测试。</span><span class="sxs-lookup"><span data-stu-id="b67ec-131">We'll start by creating a new folder within our test project called "Models" where we'll place our model-related tests.</span></span> <span data-ttu-id="b67ec-132">然后，右键单击该文件夹，然后选择 "**添加-&gt;新测试**" 菜单命令。</span><span class="sxs-lookup"><span data-stu-id="b67ec-132">We'll then right-click on the folder and choose the **Add-&gt;New Test** menu command.</span></span> <span data-ttu-id="b67ec-133">此时将显示 "添加新测试" 对话框。</span><span class="sxs-lookup"><span data-stu-id="b67ec-133">This will bring up the "Add New Test" dialog.</span></span>

<span data-ttu-id="b67ec-134">我们将选择创建 "单元测试" 并将其命名为 "DinnerTest.cs"：</span><span class="sxs-lookup"><span data-stu-id="b67ec-134">We'll choose to create a "Unit Test" and name it "DinnerTest.cs":</span></span>

![](enable-automated-unit-testing/_static/image3.png)

<span data-ttu-id="b67ec-135">单击 "确定" 按钮时，Visual Studio 会将 DinnerTest.cs 文件添加（并打开）到项目中：</span><span class="sxs-lookup"><span data-stu-id="b67ec-135">When we click the "ok" button Visual Studio will add (and open) a DinnerTest.cs file to the project:</span></span>

![](enable-automated-unit-testing/_static/image4.png)

<span data-ttu-id="b67ec-136">默认的 Visual Studio 单元测试模板在其中有一组样板代码，我发现有点杂乱。</span><span class="sxs-lookup"><span data-stu-id="b67ec-136">The default Visual Studio unit test template has a bunch of boiler-plate code within it that I find a little messy.</span></span> <span data-ttu-id="b67ec-137">让我们将其清理，只包含以下代码：</span><span class="sxs-lookup"><span data-stu-id="b67ec-137">Let's clean it up to just contain the code below:</span></span>

[!code-csharp[Main](enable-automated-unit-testing/samples/sample1.cs)]

<span data-ttu-id="b67ec-138">上述 DinnerTest 类的 [TestClass] 属性将其标识为包含测试的类，以及可选的测试初始化和拆卸代码。</span><span class="sxs-lookup"><span data-stu-id="b67ec-138">The [TestClass] attribute on the DinnerTest class above identifies it as a class that will contain tests, as well as optional test initialization and teardown code.</span></span> <span data-ttu-id="b67ec-139">可以通过在其上添加具有 [TestMethod] 属性的公共方法，在其中定义测试。</span><span class="sxs-lookup"><span data-stu-id="b67ec-139">We can define tests within it by adding public methods that have a [TestMethod] attribute on them.</span></span>

<span data-ttu-id="b67ec-140">下面是我们要添加的两个测试中的第一个测试。</span><span class="sxs-lookup"><span data-stu-id="b67ec-140">Below are the first of two tests we'll add that exercise our Dinner class.</span></span> <span data-ttu-id="b67ec-141">第一次测试验证在创建新晚餐后，如果没有正确设置所有属性，则晚餐无效。</span><span class="sxs-lookup"><span data-stu-id="b67ec-141">The first test verifies that our Dinner is invalid if a new Dinner is created without all properties being set correctly.</span></span> <span data-ttu-id="b67ec-142">第二个测试验证晚餐是否有效，并且所有属性都设置了有效值：</span><span class="sxs-lookup"><span data-stu-id="b67ec-142">The second test verifies that our Dinner is valid when a Dinner has all properties set with valid values:</span></span>

[!code-csharp[Main](enable-automated-unit-testing/samples/sample2.cs)]

<span data-ttu-id="b67ec-143">你会注意到，我们的测试名称非常明确（并且稍有详细）。</span><span class="sxs-lookup"><span data-stu-id="b67ec-143">You'll notice above that our test names are very explicit (and somewhat verbose).</span></span> <span data-ttu-id="b67ec-144">我们这样做的原因是，我们可能最终会创建数百个或数千个小测试，因此，我们希望能够轻松快速地确定每个测试的意图和行为（特别是当我们要在测试运行程序中查找故障列表）。</span><span class="sxs-lookup"><span data-stu-id="b67ec-144">We are doing this because we might end up creating hundreds or thousands of small tests, and we want to make it easy to quickly determine the intent and behavior of each of them (especially when we are looking through a list of failures in a test runner).</span></span> <span data-ttu-id="b67ec-145">测试名称应在要测试的功能之后命名。</span><span class="sxs-lookup"><span data-stu-id="b67ec-145">The test names should be named after the functionality they are testing.</span></span> <span data-ttu-id="b67ec-146">以上我们使用的是 "名词\_应\_谓词" 命名模式。</span><span class="sxs-lookup"><span data-stu-id="b67ec-146">Above we are using a "Noun\_Should\_Verb" naming pattern.</span></span>

<span data-ttu-id="b67ec-147">我们使用 "AAA" 测试模式来构建测试，这种模式代表 "排列，Act，断言"：</span><span class="sxs-lookup"><span data-stu-id="b67ec-147">We are structuring the tests using the "AAA" testing pattern – which stands for "Arrange, Act, Assert":</span></span>

- <span data-ttu-id="b67ec-148">排列：设置要测试的单元</span><span class="sxs-lookup"><span data-stu-id="b67ec-148">Arrange: Setup the unit being tested</span></span>
- <span data-ttu-id="b67ec-149">Act：练习测试单元并捕获结果</span><span class="sxs-lookup"><span data-stu-id="b67ec-149">Act: Exercise the unit under test and capture results</span></span>
- <span data-ttu-id="b67ec-150">Assert：验证行为</span><span class="sxs-lookup"><span data-stu-id="b67ec-150">Assert: Verify the behavior</span></span>

<span data-ttu-id="b67ec-151">编写测试时，我们希望避免各个测试的操作过多。</span><span class="sxs-lookup"><span data-stu-id="b67ec-151">When we write tests we want to avoid having the individual tests do too much.</span></span> <span data-ttu-id="b67ec-152">相反，每个测试应该只验证单个概念（这会使查找失败的原因变得更加容易）。</span><span class="sxs-lookup"><span data-stu-id="b67ec-152">Instead each test should verify only a single concept (which will make it much easier to pinpoint the cause of failures).</span></span> <span data-ttu-id="b67ec-153">一种很好的指导原则是尝试每个测试只使用一个 assert 语句。</span><span class="sxs-lookup"><span data-stu-id="b67ec-153">A good guideline is to try and only have a single assert statement for each test.</span></span> <span data-ttu-id="b67ec-154">如果在测试方法中有多个 assert 语句，请确保它们都用于测试相同的概念。</span><span class="sxs-lookup"><span data-stu-id="b67ec-154">If you have more than one assert statement in a test method, make sure they are all being used to test the same concept.</span></span> <span data-ttu-id="b67ec-155">如果有疑问，请进行另一个测试。</span><span class="sxs-lookup"><span data-stu-id="b67ec-155">When in doubt, make another test.</span></span>

### <a name="running-tests"></a><span data-ttu-id="b67ec-156">正在运行测试</span><span class="sxs-lookup"><span data-stu-id="b67ec-156">Running Tests</span></span>

<span data-ttu-id="b67ec-157">Visual Studio 2008 Professional （及更高版本）包含一个内置的测试运行程序，可用于在 IDE 中运行 Visual Studio 单元测试项目。</span><span class="sxs-lookup"><span data-stu-id="b67ec-157">Visual Studio 2008 Professional (and higher editions) includes a built-in test runner that can be used to run Visual Studio Unit Test projects within the IDE.</span></span> <span data-ttu-id="b67ec-158">可以在 "解决方案" 菜单命令中选择 "**测试&gt;运行&gt;所有测试"** （或按 Ctrl R，A），以运行所有单元测试。</span><span class="sxs-lookup"><span data-stu-id="b67ec-158">We can select the **Test-&gt;Run-&gt;All Tests in Solution** menu command (or type Ctrl R, A) to run all of our unit tests.</span></span> <span data-ttu-id="b67ec-159">或者，也可以将游标定位在特定的测试类或测试方法中，并使用**测试&gt;在当前上下文菜单命令中运行&gt;测试**（或按 Ctrl R，t）来运行单元测试的子集。</span><span class="sxs-lookup"><span data-stu-id="b67ec-159">Or alternatively we can position our cursor within a specific test class or test method and use the **Test-&gt;Run-&gt;Tests in Current Context** menu command (or type Ctrl R, T) to run a subset of the unit tests.</span></span>

<span data-ttu-id="b67ec-160">让我们将光标置于 DinnerTest 类中，并键入 "Ctrl R，T" 以运行刚刚定义的两个测试。</span><span class="sxs-lookup"><span data-stu-id="b67ec-160">Let's position our cursor within the DinnerTest class and type "Ctrl R, T" to run the two tests we just defined.</span></span> <span data-ttu-id="b67ec-161">执行此操作时，将在 Visual Studio 中显示 "测试结果" 窗口，并在其中列出测试运行的结果：</span><span class="sxs-lookup"><span data-stu-id="b67ec-161">When we do this a "Test Results" window will appear within Visual Studio and we'll see the results of our test run listed within it:</span></span>

![](enable-automated-unit-testing/_static/image5.png)

<span data-ttu-id="b67ec-162">*注意：默认情况下，VS 测试结果窗口不显示 "类名" 列。可以通过在 "测试结果" 窗口中右键单击并使用 "添加/删除列" 菜单命令来添加此项。*</span><span class="sxs-lookup"><span data-stu-id="b67ec-162">*Note: The VS test results window does not show the Class Name column by default. You can add this by right-clicking within the Test Results window and using the Add/Remove Columns menu command.*</span></span>

<span data-ttu-id="b67ec-163">这两个测试只需运行一小部分，并且可以看到它们都通过。</span><span class="sxs-lookup"><span data-stu-id="b67ec-163">Our two tests took only a fraction of a second to run – and as you can see they both passed.</span></span> <span data-ttu-id="b67ec-164">现在，我们可以通过创建其他测试来验证具体规则验证，并涵盖添加到晚餐类的两个帮助器方法-IsUserHost （）和 IsUserRegistered （），来对这些方法进行补充。</span><span class="sxs-lookup"><span data-stu-id="b67ec-164">We can now go on and augment them by creating additional tests that verify specific rule validations, as well as cover the two helper methods - IsUserHost() and IsUserRegistered() – that we added to the Dinner class.</span></span> <span data-ttu-id="b67ec-165">为晚餐类准备好所有这些测试后，就可以更轻松、更安全地添加新的业务规则并在将来对其进行验证。</span><span class="sxs-lookup"><span data-stu-id="b67ec-165">Having all these tests in place for the Dinner class will make it much easier and safer to add new business rules and validations to it in the future.</span></span> <span data-ttu-id="b67ec-166">我们可以将新的规则逻辑添加到晚餐，然后在几秒钟内验证它是否未被任何以前的逻辑功能中断。</span><span class="sxs-lookup"><span data-stu-id="b67ec-166">We can add our new rule logic to Dinner, and then within seconds verify that it hasn't broken any of our previous logic functionality.</span></span>

<span data-ttu-id="b67ec-167">请注意，使用描述性测试名称可以轻松地快速了解每个测试要验证的内容。</span><span class="sxs-lookup"><span data-stu-id="b67ec-167">Notice how using a descriptive test name makes it easy to quickly understand what each test is verifying.</span></span> <span data-ttu-id="b67ec-168">我建议使用 "**工具-&gt;选项**" 菜单命令，打开 "测试工具-&gt;测试执行配置" 屏幕，并选中 "双击失败或无结论的单元测试结果将显示测试中的失败点" 复选框。</span><span class="sxs-lookup"><span data-stu-id="b67ec-168">I recommend using the **Tools-&gt;Options** menu command, opening the Test Tools-&gt;Test Execution configuration screen, and checking the "Double-clicking a failed or inconclusive unit test result displays the point of failure in the test" checkbox.</span></span> <span data-ttu-id="b67ec-169">这将允许您双击 "测试结果" 窗口中的故障并立即跳转到断言失败。</span><span class="sxs-lookup"><span data-stu-id="b67ec-169">This will allow you to double-click on a failure in the test results window and jump immediately to the assert failure.</span></span>

### <a name="creating-dinnerscontroller-unit-tests"></a><span data-ttu-id="b67ec-170">创建 DinnersController 单元测试</span><span class="sxs-lookup"><span data-stu-id="b67ec-170">Creating DinnersController Unit Tests</span></span>

<span data-ttu-id="b67ec-171">现在，让我们创建一些单元测试来验证我们的 DinnersController 功能。</span><span class="sxs-lookup"><span data-stu-id="b67ec-171">Let's now create some unit tests that verify our DinnersController functionality.</span></span> <span data-ttu-id="b67ec-172">首先，右键单击测试项目中的 "控制器" 文件夹，然后选择 "**添加-&gt;新测试**" 菜单命令。</span><span class="sxs-lookup"><span data-stu-id="b67ec-172">We'll start by right-clicking on the "Controllers" folder within our Test project and then choose the **Add-&gt;New Test** menu command.</span></span> <span data-ttu-id="b67ec-173">我们将创建 "单元测试" 并将其命名为 "DinnersControllerTest.cs"。</span><span class="sxs-lookup"><span data-stu-id="b67ec-173">We'll create a "Unit Test" and name it "DinnersControllerTest.cs".</span></span>

<span data-ttu-id="b67ec-174">我们将创建两个测试方法，用于验证 DinnersController 上的详细信息（）操作方法。</span><span class="sxs-lookup"><span data-stu-id="b67ec-174">We'll create two test methods that verify the Details() action method on the DinnersController.</span></span> <span data-ttu-id="b67ec-175">第一种验证是否在请求现有晚宴时返回视图。</span><span class="sxs-lookup"><span data-stu-id="b67ec-175">The first will verify that a View is returned when an existing Dinner is requested.</span></span> <span data-ttu-id="b67ec-176">第二个验证请求不存在的晚餐时返回 "NotFound" 视图：</span><span class="sxs-lookup"><span data-stu-id="b67ec-176">The second will verify that a "NotFound" view is returned when a non-existent Dinner is requested:</span></span>

[!code-csharp[Main](enable-automated-unit-testing/samples/sample3.cs)]

<span data-ttu-id="b67ec-177">上面的代码编译干净。</span><span class="sxs-lookup"><span data-stu-id="b67ec-177">The above code compiles clean.</span></span> <span data-ttu-id="b67ec-178">但在运行测试时，它们都将失败：</span><span class="sxs-lookup"><span data-stu-id="b67ec-178">When we run the tests, though, they both fail:</span></span>

![](enable-automated-unit-testing/_static/image6.png)

<span data-ttu-id="b67ec-179">如果查看错误消息，我们将看到测试失败的原因，因为我们的 DinnersRepository 类无法连接到数据库。</span><span class="sxs-lookup"><span data-stu-id="b67ec-179">If we look at the error messages, we'll see that the reason the tests failed was because our DinnersRepository class was unable to connect to a database.</span></span> <span data-ttu-id="b67ec-180">我们的 NerdDinner 应用程序使用连接字符串连接到本地 SQL Server Express 文件，该文件位于 NerdDinner 应用程序项目的 \App\_数据目录下。</span><span class="sxs-lookup"><span data-stu-id="b67ec-180">Our NerdDinner application is using a connection-string to a local SQL Server Express file which lives under the \App\_Data directory of the NerdDinner application project.</span></span> <span data-ttu-id="b67ec-181">由于我们的 NerdDinner 项目在不同的目录中进行编译和运行，因此，该应用程序项目的连接字符串的相对路径位置不正确。</span><span class="sxs-lookup"><span data-stu-id="b67ec-181">Because our NerdDinner.Tests project compiles and runs in a different directory then the application project, the relative path location of our connection-string is incorrect.</span></span>

<span data-ttu-id="b67ec-182">我们*可以*通过将 SQL Express 数据库文件复制到测试项目中来解决此问题，然后在测试项目的 app.config 中将相应的测试连接字符串添加到该文件中。</span><span class="sxs-lookup"><span data-stu-id="b67ec-182">We *could* fix this by copying the SQL Express database file to our test project, and then add an appropriate test connection-string to it in the App.config of our test project.</span></span> <span data-ttu-id="b67ec-183">这会使上面的测试解除阻止并运行。</span><span class="sxs-lookup"><span data-stu-id="b67ec-183">This would get the above tests unblocked and running.</span></span>

<span data-ttu-id="b67ec-184">然而，使用实际数据库的单元测试代码带来了许多挑战。</span><span class="sxs-lookup"><span data-stu-id="b67ec-184">Unit testing code using a real database, though, brings with it a number of challenges.</span></span> <span data-ttu-id="b67ec-185">尤其是在下列情况下：</span><span class="sxs-lookup"><span data-stu-id="b67ec-185">Specifically:</span></span>

- <span data-ttu-id="b67ec-186">它显著降低了单元测试的执行时间。</span><span class="sxs-lookup"><span data-stu-id="b67ec-186">It significantly slows down the execution time of unit tests.</span></span> <span data-ttu-id="b67ec-187">运行测试所花费的时间越长，频繁执行它们的可能性就越低。</span><span class="sxs-lookup"><span data-stu-id="b67ec-187">The longer it takes to run tests, the less likely you are to execute them frequently.</span></span> <span data-ttu-id="b67ec-188">理想情况下，你希望你的单元测试能够在数秒内运行，并将其作为编译项目的自然方式。</span><span class="sxs-lookup"><span data-stu-id="b67ec-188">Ideally you want your unit tests to be able to be run in seconds – and have it be something you do as naturally as compiling the project.</span></span>
- <span data-ttu-id="b67ec-189">它会使测试内的设置和清理逻辑复杂化。</span><span class="sxs-lookup"><span data-stu-id="b67ec-189">It complicates the setup and cleanup logic within tests.</span></span> <span data-ttu-id="b67ec-190">您希望每个单元测试都是独立的，并且不依赖于其他单元测试（无副作用或依赖项）。</span><span class="sxs-lookup"><span data-stu-id="b67ec-190">You want each unit test to be isolated and independent of others (with no side effects or dependencies).</span></span> <span data-ttu-id="b67ec-191">处理真实数据库时，必须注意状态，并在测试之间重置。</span><span class="sxs-lookup"><span data-stu-id="b67ec-191">When working against a real database you have to be mindful of state and reset it between tests.</span></span>

<span data-ttu-id="b67ec-192">让我们看一下称为 "依赖关系注入" 的设计模式，这可以帮助我们解决这些问题，并避免需要在测试中使用实际数据库。</span><span class="sxs-lookup"><span data-stu-id="b67ec-192">Let's look at a design pattern called "dependency injection" that can help us work around these issues and avoid the need to use a real database with our tests.</span></span>

### <a name="dependency-injection"></a><span data-ttu-id="b67ec-193">依赖关系注入</span><span class="sxs-lookup"><span data-stu-id="b67ec-193">Dependency Injection</span></span>

<span data-ttu-id="b67ec-194">现在，DinnersController 紧靠 DinnerRepository 类。</span><span class="sxs-lookup"><span data-stu-id="b67ec-194">Right now DinnersController is tightly "coupled" to the DinnerRepository class.</span></span> <span data-ttu-id="b67ec-195">"耦合" 指的是类显式依赖于另一类以便正常工作的情况：</span><span class="sxs-lookup"><span data-stu-id="b67ec-195">"Coupling" refers to a situation where a class explicitly relies on another class in order to work:</span></span>

[!code-csharp[Main](enable-automated-unit-testing/samples/sample4.cs)]

<span data-ttu-id="b67ec-196">由于 DinnerRepository 类需要对数据库的访问权限，DinnersController 类在 DinnerRepository 上具有紧密耦合的依赖项，因此，为了对 DinnersController 操作方法进行测试，要求我们具有一个数据库。</span><span class="sxs-lookup"><span data-stu-id="b67ec-196">Because the DinnerRepository class requires access to a database, the tightly coupled dependency the DinnersController class has on the DinnerRepository ends up requiring us to have a database in order for the DinnersController action methods to be tested.</span></span>

<span data-ttu-id="b67ec-197">我们可以通过使用名为 "依赖关系注入" 的设计模式来解决此问题，这种方法在使用它们的类中不再隐式创建依赖项（如提供数据访问的存储库类）。</span><span class="sxs-lookup"><span data-stu-id="b67ec-197">We can get around this by employing a design pattern called "dependency injection" – which is an approach where dependencies (like repository classes that provide data access) are no longer implicitly created within classes that use them.</span></span> <span data-ttu-id="b67ec-198">相反，可以将依赖项显式传递到使用构造函数参数的类。</span><span class="sxs-lookup"><span data-stu-id="b67ec-198">Instead, dependencies can be explicitly passed to the class that uses them using constructor arguments.</span></span> <span data-ttu-id="b67ec-199">如果使用接口定义依赖项，则我们可以灵活地为单元测试方案传递 "假" 依赖项实现。</span><span class="sxs-lookup"><span data-stu-id="b67ec-199">If the dependencies are defined using interfaces, we then have the flexibility to pass in "fake" dependency implementations for unit test scenarios.</span></span> <span data-ttu-id="b67ec-200">这样，我们便可以创建不需要访问数据库的特定于测试的依赖项实现。</span><span class="sxs-lookup"><span data-stu-id="b67ec-200">This enables us to create test-specific dependency implementations that do not actually require access to a database.</span></span>

<span data-ttu-id="b67ec-201">要了解这一点，让我们通过 DinnersController 实现依赖关系注入。</span><span class="sxs-lookup"><span data-stu-id="b67ec-201">To see this in action, let's implement dependency injection with our DinnersController.</span></span>

#### <a name="extracting-an-idinnerrepository-interface"></a><span data-ttu-id="b67ec-202">提取 IDinnerRepository 接口</span><span class="sxs-lookup"><span data-stu-id="b67ec-202">Extracting an IDinnerRepository interface</span></span>

<span data-ttu-id="b67ec-203">第一步是创建一个新的 IDinnerRepository 接口，用于封装控制器检索和更新就时所需的存储库协定。</span><span class="sxs-lookup"><span data-stu-id="b67ec-203">Our first step will be to create a new IDinnerRepository interface that encapsulates the repository contract our controllers require to retrieve and update Dinners.</span></span>

<span data-ttu-id="b67ec-204">可以通过右键单击 \Models 文件夹，然后选择 "**添加-&gt;新项**" 菜单命令并创建一个名为 IDinnerRepository.cs 的新接口，来手动定义此接口协定。</span><span class="sxs-lookup"><span data-stu-id="b67ec-204">We can define this interface contract manually by right-clicking on the \Models folder, and then choosing the **Add-&gt;New Item** menu command and creating a new interface named IDinnerRepository.cs.</span></span>

<span data-ttu-id="b67ec-205">此外，我们还可以使用内置 Visual Studio Professional （和更高版本）的重构工具为我们从现有的 DinnerRepository 类中自动提取和创建一个接口。</span><span class="sxs-lookup"><span data-stu-id="b67ec-205">Alternatively we can use the refactoring tools built-into Visual Studio Professional (and higher editions) to automatically extract and create an interface for us from our existing DinnerRepository class.</span></span> <span data-ttu-id="b67ec-206">若要使用 VS 提取此接口，只需将光标置于 DinnerRepository 类的文本编辑器中，然后右键单击并选择 "**重构-&gt;提取接口**" 菜单命令：</span><span class="sxs-lookup"><span data-stu-id="b67ec-206">To extract this interface using VS, simply position the cursor in the text editor on the DinnerRepository class, and then right-click and choose the **Refactor-&gt;Extract Interface** menu command:</span></span>

![](enable-automated-unit-testing/_static/image7.png)

<span data-ttu-id="b67ec-207">这将启动 "提取接口" 对话框，并提示我们输入要创建的接口的名称。</span><span class="sxs-lookup"><span data-stu-id="b67ec-207">This will launch the "Extract Interface" dialog and prompt us for the name of the interface to create.</span></span> <span data-ttu-id="b67ec-208">它将默认为 IDinnerRepository，并自动选择现有 DinnerRepository 类中的所有公共方法，以添加到接口：</span><span class="sxs-lookup"><span data-stu-id="b67ec-208">It will default to IDinnerRepository and automatically select all public methods on the existing DinnerRepository class to add to the interface:</span></span>

![](enable-automated-unit-testing/_static/image8.png)

<span data-ttu-id="b67ec-209">单击 "确定" 按钮时，Visual Studio 将向应用程序添加新的 IDinnerRepository 接口：</span><span class="sxs-lookup"><span data-stu-id="b67ec-209">When we click the "ok" button, Visual Studio will add a new IDinnerRepository interface to our application:</span></span>

[!code-csharp[Main](enable-automated-unit-testing/samples/sample5.cs)]

<span data-ttu-id="b67ec-210">将更新现有的 DinnerRepository 类，使其实现接口：</span><span class="sxs-lookup"><span data-stu-id="b67ec-210">And our existing DinnerRepository class will be updated so that it implements the interface:</span></span>

[!code-csharp[Main](enable-automated-unit-testing/samples/sample6.cs)]

#### <a name="updating-dinnerscontroller-to-support-constructor-injection"></a><span data-ttu-id="b67ec-211">更新 DinnersController 以支持构造函数注入</span><span class="sxs-lookup"><span data-stu-id="b67ec-211">Updating DinnersController to support constructor injection</span></span>

<span data-ttu-id="b67ec-212">现在，我们将更新 DinnersController 类以使用新的接口。</span><span class="sxs-lookup"><span data-stu-id="b67ec-212">We'll now update the DinnersController class to use the new interface.</span></span>

<span data-ttu-id="b67ec-213">当前 DinnersController 是硬编码的，因此其 "dinnerRepository" 字段始终是一个 DinnerRepository 类：</span><span class="sxs-lookup"><span data-stu-id="b67ec-213">Currently DinnersController is hard-coded such that its "dinnerRepository" field is always a DinnerRepository class:</span></span>

[!code-csharp[Main](enable-automated-unit-testing/samples/sample7.cs)]

<span data-ttu-id="b67ec-214">我们将对其进行更改，使 "dinnerRepository" 字段的类型为 IDinnerRepository 而不是 DinnerRepository。</span><span class="sxs-lookup"><span data-stu-id="b67ec-214">We'll change it so that the "dinnerRepository" field is of type IDinnerRepository instead of DinnerRepository.</span></span> <span data-ttu-id="b67ec-215">接下来，我们将添加两个公共 DinnersController 构造函数。</span><span class="sxs-lookup"><span data-stu-id="b67ec-215">We'll then add two public DinnersController constructors.</span></span> <span data-ttu-id="b67ec-216">其中一个构造函数允许将 IDinnerRepository 作为参数进行传递。</span><span class="sxs-lookup"><span data-stu-id="b67ec-216">One of the constructors allows an IDinnerRepository to be passed as an argument.</span></span> <span data-ttu-id="b67ec-217">另一个是使用现有 DinnerRepository 实现的默认构造函数：</span><span class="sxs-lookup"><span data-stu-id="b67ec-217">The other is a default constructor that uses our existing DinnerRepository implementation:</span></span>

[!code-csharp[Main](enable-automated-unit-testing/samples/sample8.cs)]

<span data-ttu-id="b67ec-218">由于 ASP.NET MVC 默认使用默认构造函数创建控制器类，因此，我们在运行时 DinnersController 将继续使用 DinnerRepository 类来执行数据访问。</span><span class="sxs-lookup"><span data-stu-id="b67ec-218">Because ASP.NET MVC by default creates controller classes using default constructors, our DinnersController at runtime will continue to use the DinnerRepository class to perform data access.</span></span>

<span data-ttu-id="b67ec-219">不过，现在我们可以更新单元测试，以使用参数构造函数传入 "虚假" 晚餐存储库实现。</span><span class="sxs-lookup"><span data-stu-id="b67ec-219">We can now update our unit tests, though, to pass in a "fake" dinner repository implementation using the parameter constructor.</span></span> <span data-ttu-id="b67ec-220">此 "虚假" 晚餐存储库不需要访问实际数据库，而是使用内存中示例数据。</span><span class="sxs-lookup"><span data-stu-id="b67ec-220">This "fake" dinner repository will not require access to a real database, and instead will use in-memory sample data.</span></span>

#### <a name="creating-the-fakedinnerrepository-class"></a><span data-ttu-id="b67ec-221">创建 FakeDinnerRepository 类</span><span class="sxs-lookup"><span data-stu-id="b67ec-221">Creating the FakeDinnerRepository class</span></span>

<span data-ttu-id="b67ec-222">让我们创建一个 FakeDinnerRepository 类。</span><span class="sxs-lookup"><span data-stu-id="b67ec-222">Let's create a FakeDinnerRepository class.</span></span>

<span data-ttu-id="b67ec-223">首先，我们将在 NerdDinner 项目中创建一个 "Fakes" 目录，然后向其添加新的 FakeDinnerRepository 类（右键单击该文件夹，然后选择 "**添加-&gt;新类**）"：</span><span class="sxs-lookup"><span data-stu-id="b67ec-223">We'll begin by creating a "Fakes" directory within our NerdDinner.Tests project and then add a new FakeDinnerRepository class to it (right-click on the folder and choose **Add-&gt;New Class**):</span></span>

![](enable-automated-unit-testing/_static/image9.png)

<span data-ttu-id="b67ec-224">我们将更新代码，使 FakeDinnerRepository 类实现 IDinnerRepository 接口。</span><span class="sxs-lookup"><span data-stu-id="b67ec-224">We'll update the code so that the FakeDinnerRepository class implements the IDinnerRepository interface.</span></span> <span data-ttu-id="b67ec-225">然后，可以右键单击它并选择 "实现接口 IDinnerRepository" 上下文菜单命令：</span><span class="sxs-lookup"><span data-stu-id="b67ec-225">We can then right-click on it and choose the "Implement interface IDinnerRepository" context menu command:</span></span>

![](enable-automated-unit-testing/_static/image10.png)

<span data-ttu-id="b67ec-226">这将导致 Visual Studio 将所有 IDinnerRepository 接口成员自动添加到 FakeDinnerRepository 类，其默认值为 "stub out" 实现：</span><span class="sxs-lookup"><span data-stu-id="b67ec-226">This will cause Visual Studio to automatically add all of the IDinnerRepository interface members to our FakeDinnerRepository class with default "stub out" implementations:</span></span>

[!code-csharp[Main](enable-automated-unit-testing/samples/sample9.cs)]

<span data-ttu-id="b67ec-227">然后，可以将 FakeDinnerRepository 实现更新为在内存中列表中工作，&lt;晚餐&gt; 集合作为构造函数参数传递给它：</span><span class="sxs-lookup"><span data-stu-id="b67ec-227">We can then update the FakeDinnerRepository implementation to work off of an in-memory List&lt;Dinner&gt; collection passed to it as a constructor argument:</span></span>

[!code-csharp[Main](enable-automated-unit-testing/samples/sample10.cs)]

<span data-ttu-id="b67ec-228">现在，我们有了一个不需要数据库的虚设 IDinnerRepository 实现，可以改为使用内存中的晚餐对象列表。</span><span class="sxs-lookup"><span data-stu-id="b67ec-228">We now have a fake IDinnerRepository implementation that does not require a database, and can instead work off an in-memory list of Dinner objects.</span></span>

#### <a name="using-the-fakedinnerrepository-with-unit-tests"></a><span data-ttu-id="b67ec-229">将 FakeDinnerRepository 用于单元测试</span><span class="sxs-lookup"><span data-stu-id="b67ec-229">Using the FakeDinnerRepository with Unit Tests</span></span>

<span data-ttu-id="b67ec-230">让我们返回到以前失败的 DinnersController 单元测试，因为数据库不可用。</span><span class="sxs-lookup"><span data-stu-id="b67ec-230">Let's return to the DinnersController unit tests that failed earlier because the database wasn't available.</span></span> <span data-ttu-id="b67ec-231">我们可以使用以下代码更新测试方法，以将使用内存中的内存导入数据的 FakeDinnerRepository 与 DinnersController 一起使用：</span><span class="sxs-lookup"><span data-stu-id="b67ec-231">We can update the test methods to use a FakeDinnerRepository populated with sample in-memory Dinner data to the DinnersController using the code below:</span></span>

[!code-csharp[Main](enable-automated-unit-testing/samples/sample11.cs)]

<span data-ttu-id="b67ec-232">现在，当我们运行这些测试时，它们都通过：</span><span class="sxs-lookup"><span data-stu-id="b67ec-232">And now when we run these tests they both pass:</span></span>

![](enable-automated-unit-testing/_static/image11.png)

<span data-ttu-id="b67ec-233">最重要的是，它们只需运行一小部分，无需任何复杂的设置/清理逻辑。</span><span class="sxs-lookup"><span data-stu-id="b67ec-233">Best of all, they take only a fraction of a second to run, and do not require any complicated setup/cleanup logic.</span></span> <span data-ttu-id="b67ec-234">现在，我们可以对所有 DinnersController 操作方法代码（包括列表、分页、详细信息、创建、更新和删除）进行单元测试，而无需连接到实际数据库。</span><span class="sxs-lookup"><span data-stu-id="b67ec-234">We can now unit test all of our DinnersController action method code (including listing, paging, details, create, update and delete) without ever needing to connect to a real database.</span></span>

| <span data-ttu-id="b67ec-235">**边主题：依赖关系注入框架**</span><span class="sxs-lookup"><span data-stu-id="b67ec-235">**Side Topic: Dependency Injection Frameworks**</span></span> |
| --- |
| <span data-ttu-id="b67ec-236">执行手动依赖关系注入（如我们的工作方式）运行正常，但随着应用程序中的依赖项和组件数量的增加，维护变得越来越困难。</span><span class="sxs-lookup"><span data-stu-id="b67ec-236">Performing manual dependency injection (like we are above) works fine, but does become harder to maintain as the number of dependencies and components in an application increases.</span></span> <span data-ttu-id="b67ec-237">.NET 存在多个依赖关系注入框架，可帮助提供更多依赖关系管理灵活性。</span><span class="sxs-lookup"><span data-stu-id="b67ec-237">Several dependency injection frameworks exist for .NET that can help provide even more dependency management flexibility.</span></span> <span data-ttu-id="b67ec-238">这些框架（有时也称为 "控制反转" （IoC）容器）提供了一些机制，允许在运行时指定对象的依赖项并将依赖项传递到对象（最常使用构造函数注入）).</span><span class="sxs-lookup"><span data-stu-id="b67ec-238">These frameworks, also sometimes called "Inversion of Control" (IoC) containers, provide mechanisms that enable an additional level of configuration support for specifying and passing dependencies to objects at runtime (most often using constructor injection).</span></span> <span data-ttu-id="b67ec-239">.NET 中的一些更常见的 OSS 依赖关系注入/IOC 框架包括： AutoFac、Ninject、Spring.NET、StructureMap 和 Windsor。</span><span class="sxs-lookup"><span data-stu-id="b67ec-239">Some of the more popular OSS Dependency Injection / IOC frameworks in .NET include: AutoFac, Ninject, Spring.NET, StructureMap, and Windsor.</span></span> <span data-ttu-id="b67ec-240">ASP.NET MVC 公开了可扩展性 Api，使开发人员能够参与控制器的解析和实例化，并使依赖关系注入/IoC 框架在此过程中完全集成。</span><span class="sxs-lookup"><span data-stu-id="b67ec-240">ASP.NET MVC exposes extensibility APIs that enable developers to participate in the resolution and instantiation of controllers, and which enables Dependency Injection / IoC frameworks to be cleanly integrated within this process.</span></span> <span data-ttu-id="b67ec-241">使用 DI/IOC 框架还可以从 DinnersController 中删除默认的构造函数，这将完全删除它与 DinnerRepository 之间的耦合。</span><span class="sxs-lookup"><span data-stu-id="b67ec-241">Using a DI/IOC framework would also enable us to remove the default constructor from our DinnersController – which would completely remove the coupling between it and the DinnerRepository.</span></span> <span data-ttu-id="b67ec-242">我们不会在 NerdDinner 应用程序中使用依赖关系注入/IOC 框架。</span><span class="sxs-lookup"><span data-stu-id="b67ec-242">We won't be using a dependency injection / IOC framework with our NerdDinner application.</span></span> <span data-ttu-id="b67ec-243">但如果 NerdDinner 的基本代码和功能增长，我们可能会考虑到这一点。</span><span class="sxs-lookup"><span data-stu-id="b67ec-243">But it is something we could consider for the future if the NerdDinner code-base and capabilities grew.</span></span> |

### <a name="creating-edit-action-unit-tests"></a><span data-ttu-id="b67ec-244">创建编辑操作单元测试</span><span class="sxs-lookup"><span data-stu-id="b67ec-244">Creating Edit Action Unit Tests</span></span>

<span data-ttu-id="b67ec-245">现在，让我们创建一些单元测试来验证 DinnersController 的编辑功能。</span><span class="sxs-lookup"><span data-stu-id="b67ec-245">Let's now create some unit tests that verify the Edit functionality of the DinnersController.</span></span> <span data-ttu-id="b67ec-246">首先，我们将测试编辑操作的 HTTP 获取版本：</span><span class="sxs-lookup"><span data-stu-id="b67ec-246">We'll start by testing the HTTP-GET version of our Edit action:</span></span>

[!code-csharp[Main](enable-automated-unit-testing/samples/sample12.cs)]

<span data-ttu-id="b67ec-247">接下来，我们将创建一个测试，用于验证请求某个 DinnerFormViewModel 对象所支持的视图时，该视图将呈现回来：</span><span class="sxs-lookup"><span data-stu-id="b67ec-247">We'll create a test that verifies that a View backed by a DinnerFormViewModel object is rendered back when a valid dinner is requested:</span></span>

[!code-csharp[Main](enable-automated-unit-testing/samples/sample13.cs)]

<span data-ttu-id="b67ec-248">但在运行测试时，我们会发现它失败，因为在编辑方法访问 User.Identity.Name 属性以执行 IsHostedBy （）检查时，会引发空引用异常。</span><span class="sxs-lookup"><span data-stu-id="b67ec-248">When we run the test, though, we'll find that it fails because a null reference exception is thrown when the Edit method accesses the User.Identity.Name property to perform the Dinner.IsHostedBy() check.</span></span>

<span data-ttu-id="b67ec-249">控制器基类上的 User 对象封装了有关已登录用户的详细信息，并在运行时创建控制器时由 ASP.NET MVC 填充。</span><span class="sxs-lookup"><span data-stu-id="b67ec-249">The User object on the Controller base class encapsulates details about the logged-in user, and is populated by ASP.NET MVC when it creates the controller at runtime.</span></span> <span data-ttu-id="b67ec-250">由于我们要在 web 服务器环境之外测试 DinnersController，因此不会设置 User 对象（因此为空引用异常）。</span><span class="sxs-lookup"><span data-stu-id="b67ec-250">Because we are testing the DinnersController outside of a web-server environment, the User object isn't set (hence the null reference exception).</span></span>

### <a name="mocking-the-useridentityname-property"></a><span data-ttu-id="b67ec-251">模拟 User.Identity.Name 属性</span><span class="sxs-lookup"><span data-stu-id="b67ec-251">Mocking the User.Identity.Name property</span></span>

<span data-ttu-id="b67ec-252">模拟框架通过使我们能够动态创建支持测试的各种依赖对象，使测试变得更加轻松。</span><span class="sxs-lookup"><span data-stu-id="b67ec-252">Mocking frameworks make testing easier by enabling us to dynamically create fake versions of dependent objects that support our tests.</span></span> <span data-ttu-id="b67ec-253">例如，我们可以在编辑操作测试中使用模拟框架来动态创建用户对象，DinnersController 可使用该对象查找模拟的用户名。</span><span class="sxs-lookup"><span data-stu-id="b67ec-253">For example, we can use a mocking framework in our Edit action test to dynamically create a User object that our DinnersController can use to lookup a simulated username.</span></span> <span data-ttu-id="b67ec-254">这将避免在我们运行测试时引发空引用。</span><span class="sxs-lookup"><span data-stu-id="b67ec-254">This will avoid a null reference from being thrown when we run our test.</span></span>

<span data-ttu-id="b67ec-255">可以将许多 .NET 模拟框架与 ASP.NET MVC 一起使用（可在此处查看这些框架的列表： [http://www.mockframeworks.com/](http://www.mockframeworks.com/)）。</span><span class="sxs-lookup"><span data-stu-id="b67ec-255">There are many .NET mocking frameworks that can be used with ASP.NET MVC (you can see a list of them here: [http://www.mockframeworks.com/](http://www.mockframeworks.com/)).</span></span> <span data-ttu-id="b67ec-256">若要测试我们的 NerdDinner 应用程序，我们将使用名为 "Moq" 的开源模拟 framework， [http://www.mockframeworks.com/moq](http://www.mockframeworks.com/moq)可以免费下载该框架。</span><span class="sxs-lookup"><span data-stu-id="b67ec-256">For testing our NerdDinner application we'll use an open source mocking framework called "Moq", which can be downloaded for free from [http://www.mockframeworks.com/moq](http://www.mockframeworks.com/moq).</span></span>

<span data-ttu-id="b67ec-257">下载完成后，我们会在 NerdDinner 项目中添加对 Moq 程序集的引用：</span><span class="sxs-lookup"><span data-stu-id="b67ec-257">Once downloaded, we'll add a reference in our NerdDinner.Tests project to the Moq.dll assembly:</span></span>

![](enable-automated-unit-testing/_static/image12.png)

<span data-ttu-id="b67ec-258">然后，将 "CreateDinnersControllerAs （用户名）" 帮助器方法添加到将用户名作为参数的测试类，然后 "模拟" DinnersController 实例上的 User.Identity.Name 属性：</span><span class="sxs-lookup"><span data-stu-id="b67ec-258">We'll then add a "CreateDinnersControllerAs(username)" helper method to our test class that takes a username as a parameter, and which then "mocks" the User.Identity.Name property on the DinnersController instance:</span></span>

[!code-csharp[Main](enable-automated-unit-testing/samples/sample14.cs)]

<span data-ttu-id="b67ec-259">以上我们使用 Moq 来创建 fakes ControllerContext 对象的 Mock 对象（这就是 ASP.NET MVC 传递到 Controller 类的对象，用于公开用户、请求、响应和会话等运行时对象）。</span><span class="sxs-lookup"><span data-stu-id="b67ec-259">Above we are using Moq to create a Mock object that fakes a ControllerContext object (which is what ASP.NET MVC passes to Controller classes to expose runtime objects like User, Request, Response, and Session).</span></span> <span data-ttu-id="b67ec-260">我们正在模拟模拟上的 "SetupGet" 方法，指示 ControllerContext 上的 HttpContext.User.Identity.Name 属性应返回传递给帮助器方法的用户名字符串。</span><span class="sxs-lookup"><span data-stu-id="b67ec-260">We are calling the "SetupGet" method on the Mock to indicate that the HttpContext.User.Identity.Name property on ControllerContext should return the username string we passed to the helper method.</span></span>

<span data-ttu-id="b67ec-261">可以模拟任意数量的 ControllerContext 属性和方法。</span><span class="sxs-lookup"><span data-stu-id="b67ec-261">We can mock any number of ControllerContext properties and methods.</span></span> <span data-ttu-id="b67ec-262">为了说明这一点，我还添加了 SetupGet （）调用，以用于 IsAuthenticated 属性（对于下面的测试，实际上不需要此属性），但这有助于阐释您如何模拟请求属性。</span><span class="sxs-lookup"><span data-stu-id="b67ec-262">To illustrate this I've also added a SetupGet() call for the Request.IsAuthenticated property (which isn't actually needed for the tests below – but which helps illustrate how you can mock Request properties).</span></span> <span data-ttu-id="b67ec-263">完成后，我们将 ControllerContext mock 的实例分配给 DinnersController 的帮助器方法返回的。</span><span class="sxs-lookup"><span data-stu-id="b67ec-263">When we are done we assign an instance of the ControllerContext mock to the DinnersController our helper method returns.</span></span>

<span data-ttu-id="b67ec-264">现在，我们可以编写使用此帮助器方法的单元测试来测试涉及不同用户的编辑方案：</span><span class="sxs-lookup"><span data-stu-id="b67ec-264">We can now write unit tests that use this helper method to test Edit scenarios involving different users:</span></span>

[!code-csharp[Main](enable-automated-unit-testing/samples/sample15.cs)]

<span data-ttu-id="b67ec-265">现在，当我们运行它们所通过的测试时：</span><span class="sxs-lookup"><span data-stu-id="b67ec-265">And now when we run the tests they pass:</span></span>

![](enable-automated-unit-testing/_static/image13.png)

### <a name="testing-updatemodel-scenarios"></a><span data-ttu-id="b67ec-266">测试 UpdateModel （）方案</span><span class="sxs-lookup"><span data-stu-id="b67ec-266">Testing UpdateModel() scenarios</span></span>

<span data-ttu-id="b67ec-267">我们已经创建了包含编辑操作的 HTTP GET 版本的测试。</span><span class="sxs-lookup"><span data-stu-id="b67ec-267">We've created tests that cover the HTTP-GET version of the Edit action.</span></span> <span data-ttu-id="b67ec-268">现在，让我们创建一些测试来验证 HTTP POST 版本的编辑操作：</span><span class="sxs-lookup"><span data-stu-id="b67ec-268">Let's now create some tests that verify the HTTP-POST version of the Edit action:</span></span>

[!code-csharp[Main](enable-automated-unit-testing/samples/sample16.cs)]

<span data-ttu-id="b67ec-269">我们使用此操作方法支持的有趣的新测试方案是在控制器基类上使用 UpdateModel （） helper 方法。</span><span class="sxs-lookup"><span data-stu-id="b67ec-269">The interesting new testing scenario for us to support with this action method is its usage of the UpdateModel() helper method on the Controller base class.</span></span> <span data-ttu-id="b67ec-270">我们使用此帮助器方法将窗体发布值绑定到晚餐对象实例。</span><span class="sxs-lookup"><span data-stu-id="b67ec-270">We are using this helper method to bind form-post values to our Dinner object instance.</span></span>

<span data-ttu-id="b67ec-271">下面是两个测试，演示了如何为要使用的 UpdateModel （）帮助程序方法提供窗体的已发布值。</span><span class="sxs-lookup"><span data-stu-id="b67ec-271">Below are two tests that demonstrates how we can supply form posted values for the UpdateModel() helper method to use.</span></span> <span data-ttu-id="b67ec-272">为此，我们将创建并填充 FormCollection 对象，然后将其分配给控制器上的 "ValueProvider" 属性。</span><span class="sxs-lookup"><span data-stu-id="b67ec-272">We'll do this by creating and populating a FormCollection object, and then assign it to the "ValueProvider" property on the Controller.</span></span>

<span data-ttu-id="b67ec-273">第一次测试验证是否在成功保存浏览器时，将浏览器重定向到详细信息操作。</span><span class="sxs-lookup"><span data-stu-id="b67ec-273">The first test verifies that on a successful save the browser is redirected to the details action.</span></span> <span data-ttu-id="b67ec-274">第二个测试验证在发布无效输入时，操作再次重新显示 "编辑" 视图并显示错误消息。</span><span class="sxs-lookup"><span data-stu-id="b67ec-274">The second test verifies that when invalid input is posted the action redisplays the edit view again with an error message.</span></span>

[!code-csharp[Main](enable-automated-unit-testing/samples/sample17.cs)]

### <a name="testing-wrap-up"></a><span data-ttu-id="b67ec-275">测试向上环绕</span><span class="sxs-lookup"><span data-stu-id="b67ec-275">Testing Wrap-Up</span></span>

<span data-ttu-id="b67ec-276">我们介绍了单元测试控制器类中涉及的核心概念。</span><span class="sxs-lookup"><span data-stu-id="b67ec-276">We've covered the core concepts involved in unit testing controller classes.</span></span> <span data-ttu-id="b67ec-277">我们可以使用这些技术轻松创建数百个验证应用程序行为的简单测试。</span><span class="sxs-lookup"><span data-stu-id="b67ec-277">We can use these techniques to easily create hundreds of simple tests that verify the behavior of our application.</span></span>

<span data-ttu-id="b67ec-278">由于控制器和模型测试不需要实际数据库，因此它们的运行速度极快且运行非常简单。</span><span class="sxs-lookup"><span data-stu-id="b67ec-278">Because our controller and model tests do not require a real database, they are extremely fast and easy to run.</span></span> <span data-ttu-id="b67ec-279">我们将能够在几秒内执行数百个自动测试，并立即获得反馈，以确定是否有更改中断了某些内容。</span><span class="sxs-lookup"><span data-stu-id="b67ec-279">We'll be able to execute hundreds of automated tests in seconds, and immediately get feedback as to whether a change we made broke something.</span></span> <span data-ttu-id="b67ec-280">这将有助于我们满怀信心地不断改进、重构和改进我们的应用程序。</span><span class="sxs-lookup"><span data-stu-id="b67ec-280">This will help provide us the confidence to continually improve, refactor, and refine our application.</span></span>

<span data-ttu-id="b67ec-281">我们已将测试作为本章中的最后一个主题进行，但不是因为在开发过程结束时应该执行测试！</span><span class="sxs-lookup"><span data-stu-id="b67ec-281">We covered testing as the last topic in this chapter – but not because testing is something you should do at the end of a development process!</span></span> <span data-ttu-id="b67ec-282">相反，应在开发过程中尽早编写自动测试。</span><span class="sxs-lookup"><span data-stu-id="b67ec-282">On the contrary, you should write automated tests as early as possible in your development process.</span></span> <span data-ttu-id="b67ec-283">这样做使您可以在开发时立即获得反馈，有助于您周全应用程序的用例方案，并指导您在设计应用程序时使用干净的分层和耦合。</span><span class="sxs-lookup"><span data-stu-id="b67ec-283">Doing so enables you to get immediate feedback as you develop, helps you think thoughtfully about your application's use case scenarios, and guides you to design your application with clean layering and coupling in mind.</span></span>

<span data-ttu-id="b67ec-284">本书后面的一章将讨论测试驱动开发（TDD），以及如何将其与 ASP.NET MVC 一起使用。</span><span class="sxs-lookup"><span data-stu-id="b67ec-284">A later chapter in the book will discuss Test Driven Development (TDD), and how to use it with ASP.NET MVC.</span></span> <span data-ttu-id="b67ec-285">TDD 是一种迭代编码实践，你首先编写生成的代码将满足的测试。</span><span class="sxs-lookup"><span data-stu-id="b67ec-285">TDD is an iterative coding practice where you first write the tests that your resulting code will satisfy.</span></span> <span data-ttu-id="b67ec-286">使用 TDD，通过创建用于验证要实现的功能的测试，开始每个功能。</span><span class="sxs-lookup"><span data-stu-id="b67ec-286">With TDD you begin each feature by creating a test that verifies the functionality you are about to implement.</span></span> <span data-ttu-id="b67ec-287">首先编写单元测试有助于确保你清楚地了解该功能及其工作原理。</span><span class="sxs-lookup"><span data-stu-id="b67ec-287">Writing the unit test first helps ensure that you clearly understand the feature and how it is supposed to work.</span></span> <span data-ttu-id="b67ec-288">只有在编写测试（并且已验证它失败）后，才可以实现测试所验证的实际功能。</span><span class="sxs-lookup"><span data-stu-id="b67ec-288">Only after the test is written (and you have verified that it fails) do you then implement the actual functionality the test verifies.</span></span> <span data-ttu-id="b67ec-289">因为您已经花了时间考虑该功能的工作原理，您将更好地理解这些要求以及实现它们的最佳方式。</span><span class="sxs-lookup"><span data-stu-id="b67ec-289">Because you've already spent time thinking about the use case of how the feature is supposed to work, you will have a better understanding of the requirements and how best to implement them.</span></span> <span data-ttu-id="b67ec-290">完成实现后，您可以重新运行测试，并获得有关该功能是否正常工作的即时反馈。</span><span class="sxs-lookup"><span data-stu-id="b67ec-290">When you are done with the implementation you can re-run the test – and get immediate feedback as to whether the feature works correctly.</span></span> <span data-ttu-id="b67ec-291">我们将在第10章中介绍 TDD。</span><span class="sxs-lookup"><span data-stu-id="b67ec-291">We'll cover TDD more in Chapter 10.</span></span>

### <a name="next-step"></a><span data-ttu-id="b67ec-292">下一步</span><span class="sxs-lookup"><span data-stu-id="b67ec-292">Next Step</span></span>

<span data-ttu-id="b67ec-293">某些最终的汇总注释。</span><span class="sxs-lookup"><span data-stu-id="b67ec-293">Some final wrap up comments.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="b67ec-294">[上一页](use-ajax-to-implement-mapping-scenarios.md)
> [下一页](nerddinner-wrap-up.md)</span><span class="sxs-lookup"><span data-stu-id="b67ec-294">[Previous](use-ajax-to-implement-mapping-scenarios.md)
[Next](nerddinner-wrap-up.md)</span></span>
