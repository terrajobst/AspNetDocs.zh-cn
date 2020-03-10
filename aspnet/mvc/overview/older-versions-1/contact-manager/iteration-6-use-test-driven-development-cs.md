---
uid: mvc/overview/older-versions-1/contact-manager/iteration-6-use-test-driven-development-cs
title: '迭代 #6 –使用测试驱动开发（C#） |Microsoft Docs'
author: microsoft
description: 在第六次迭代中，我们通过首先编写单元测试并针对单元测试编写代码，向应用程序添加新功能。 在此迭代中,。
ms.author: riande
ms.date: 02/20/2009
ms.assetid: 013c3c26-7dc3-41d1-8064-f233c86008b5
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-6-use-test-driven-development-cs
msc.type: authoredcontent
ms.openlocfilehash: aee0ff9d8d7f17e8a00dab12467bd3a3457fbe18
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78487124"
---
# <a name="iteration-6--use-test-driven-development-c"></a><span data-ttu-id="7886e-104">迭代 #6 –使用测试驱动开发（C#）</span><span class="sxs-lookup"><span data-stu-id="7886e-104">Iteration #6 – Use test-driven development (C#)</span></span>

<span data-ttu-id="7886e-105">由[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="7886e-105">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="7886e-106">下载代码</span><span class="sxs-lookup"><span data-stu-id="7886e-106">Download Code</span></span>](iteration-6-use-test-driven-development-cs/_static/contactmanager_6_cs1.zip)

> <span data-ttu-id="7886e-107">在第六次迭代中，我们通过首先编写单元测试并针对单元测试编写代码，向应用程序添加新功能。</span><span class="sxs-lookup"><span data-stu-id="7886e-107">In this sixth iteration, we add new functionality to our application by writing unit tests first and writing code against the unit tests.</span></span> <span data-ttu-id="7886e-108">在此迭代中，我们添加联系人组。</span><span class="sxs-lookup"><span data-stu-id="7886e-108">In this iteration, we add contact groups.</span></span>

## <a name="building-a-contact-management-aspnet-mvc-application-c"></a><span data-ttu-id="7886e-109">构建联系人管理 ASP.NET MVC 应用程序（C#）</span><span class="sxs-lookup"><span data-stu-id="7886e-109">Building a Contact Management ASP.NET MVC Application (C#)</span></span>

<span data-ttu-id="7886e-110">在本系列教程中，我们从一开始就生成一个完整的联系人管理应用程序。</span><span class="sxs-lookup"><span data-stu-id="7886e-110">In this series of tutorials, we build an entire Contact Management application from start to finish.</span></span> <span data-ttu-id="7886e-111">联系人管理器应用程序允许您存储联系人信息名称、电话号码和电子邮件地址，以获取人员列表。</span><span class="sxs-lookup"><span data-stu-id="7886e-111">The Contact Manager application enables you to store contact information - names, phone numbers and email addresses - for a list of people.</span></span>

<span data-ttu-id="7886e-112">我们通过多个迭代生成应用程序。</span><span class="sxs-lookup"><span data-stu-id="7886e-112">We build the application over multiple iterations.</span></span> <span data-ttu-id="7886e-113">随着每次迭代，我们将逐步改进应用程序。</span><span class="sxs-lookup"><span data-stu-id="7886e-113">With each iteration, we gradually improve the application.</span></span> <span data-ttu-id="7886e-114">此多个迭代方法的目标是使您能够了解每个更改的原因。</span><span class="sxs-lookup"><span data-stu-id="7886e-114">The goal of this multiple iteration approach is to enable you to understand the reason for each change.</span></span>

- <span data-ttu-id="7886e-115">迭代 #1-创建应用程序。</span><span class="sxs-lookup"><span data-stu-id="7886e-115">Iteration #1 - Create the application.</span></span> <span data-ttu-id="7886e-116">在第一次迭代中，我们以尽可能简单的方式创建联系人管理器。</span><span class="sxs-lookup"><span data-stu-id="7886e-116">In the first iteration, we create the Contact Manager in the simplest way possible.</span></span> <span data-ttu-id="7886e-117">添加对基本数据库操作的支持：创建、读取、更新和删除（CRUD）。</span><span class="sxs-lookup"><span data-stu-id="7886e-117">We add support for basic database operations: Create, Read, Update, and Delete (CRUD).</span></span>

- <span data-ttu-id="7886e-118">迭代 #2-使应用程序看起来不错。</span><span class="sxs-lookup"><span data-stu-id="7886e-118">Iteration #2 - Make the application look nice.</span></span> <span data-ttu-id="7886e-119">在此迭代中，我们通过修改默认的 ASP.NET MVC 视图母版页和级联样式表来改善应用程序的外观。</span><span class="sxs-lookup"><span data-stu-id="7886e-119">In this iteration, we improve the appearance of the application by modifying the default ASP.NET MVC view master page and cascading style sheet.</span></span>

- <span data-ttu-id="7886e-120">迭代 #3-添加窗体验证。</span><span class="sxs-lookup"><span data-stu-id="7886e-120">Iteration #3 - Add form validation.</span></span> <span data-ttu-id="7886e-121">在第三次迭代中，我们将添加基本的窗体验证。</span><span class="sxs-lookup"><span data-stu-id="7886e-121">In the third iteration, we add basic form validation.</span></span> <span data-ttu-id="7886e-122">我们阻止用户提交窗体，而无需填写所需的窗体字段。</span><span class="sxs-lookup"><span data-stu-id="7886e-122">We prevent people from submitting a form without completing required form fields.</span></span> <span data-ttu-id="7886e-123">我们还验证了电子邮件地址和电话号码。</span><span class="sxs-lookup"><span data-stu-id="7886e-123">We also validate email addresses and phone numbers.</span></span>

- <span data-ttu-id="7886e-124">迭代 #4-使应用程序松散耦合。</span><span class="sxs-lookup"><span data-stu-id="7886e-124">Iteration #4 - Make the application loosely coupled.</span></span> <span data-ttu-id="7886e-125">在第四次迭代中，我们将利用多种软件设计模式来更轻松地维护和修改联系人管理器应用程序。</span><span class="sxs-lookup"><span data-stu-id="7886e-125">In this fourth iteration, we take advantage of several software design patterns to make it easier to maintain and modify the Contact Manager application.</span></span> <span data-ttu-id="7886e-126">例如，我们重构应用程序以使用存储库模式和依赖关系注入模式。</span><span class="sxs-lookup"><span data-stu-id="7886e-126">For example, we refactor our application to use the Repository pattern and the Dependency Injection pattern.</span></span>

- <span data-ttu-id="7886e-127">迭代 #5-创建单元测试。</span><span class="sxs-lookup"><span data-stu-id="7886e-127">Iteration #5 - Create unit tests.</span></span> <span data-ttu-id="7886e-128">在第五次迭代中，通过添加单元测试使应用程序更易于维护和修改。</span><span class="sxs-lookup"><span data-stu-id="7886e-128">In the fifth iteration, we make our application easier to maintain and modify by adding unit tests.</span></span> <span data-ttu-id="7886e-129">我们模拟数据模型类，并为控制器和验证逻辑生成单元测试。</span><span class="sxs-lookup"><span data-stu-id="7886e-129">We mock our data model classes and build unit tests for our controllers and validation logic.</span></span>

- <span data-ttu-id="7886e-130">迭代 #6-使用测试驱动开发。</span><span class="sxs-lookup"><span data-stu-id="7886e-130">Iteration #6 - Use test-driven development.</span></span> <span data-ttu-id="7886e-131">在第六次迭代中，我们通过首先编写单元测试并针对单元测试编写代码，向应用程序添加新功能。</span><span class="sxs-lookup"><span data-stu-id="7886e-131">In this sixth iteration, we add new functionality to our application by writing unit tests first and writing code against the unit tests.</span></span> <span data-ttu-id="7886e-132">在此迭代中，我们添加联系人组。</span><span class="sxs-lookup"><span data-stu-id="7886e-132">In this iteration, we add contact groups.</span></span>

- <span data-ttu-id="7886e-133">迭代 #7-添加 Ajax 功能。</span><span class="sxs-lookup"><span data-stu-id="7886e-133">Iteration #7 - Add Ajax functionality.</span></span> <span data-ttu-id="7886e-134">在第七次迭代中，我们通过添加对 Ajax 的支持来提高应用程序的响应能力和性能。</span><span class="sxs-lookup"><span data-stu-id="7886e-134">In the seventh iteration, we improve the responsiveness and performance of our application by adding support for Ajax.</span></span>

## <a name="this-iteration"></a><span data-ttu-id="7886e-135">此迭代</span><span class="sxs-lookup"><span data-stu-id="7886e-135">This Iteration</span></span>

<span data-ttu-id="7886e-136">在联系人管理器应用程序的前一次迭代中，我们创建了单元测试，以便为代码提供安全网络。</span><span class="sxs-lookup"><span data-stu-id="7886e-136">In the previous iteration of the Contact Manager application, we created unit tests to provide a safety net for our code.</span></span> <span data-ttu-id="7886e-137">创建单元测试的动机是使代码更具弹性性以进行更改。</span><span class="sxs-lookup"><span data-stu-id="7886e-137">The motivation for creating the unit tests was to make our code more resilient to change.</span></span> <span data-ttu-id="7886e-138">使用单元测试后，我们可以对代码进行更改，并立即了解我们是否有损坏的现有功能。</span><span class="sxs-lookup"><span data-stu-id="7886e-138">With unit tests in place, we can happily make any change to our code and immediately know whether we have broken existing functionality.</span></span>

<span data-ttu-id="7886e-139">在此迭代中，我们使用单元测试来实现完全不同的目的。</span><span class="sxs-lookup"><span data-stu-id="7886e-139">In this iteration, we use unit tests for an entirely different purpose.</span></span> <span data-ttu-id="7886e-140">在此迭代中，我们将单元测试用作称为 "*测试驱动开发*" 的应用程序设计理念的一部分。</span><span class="sxs-lookup"><span data-stu-id="7886e-140">In this iteration, we use unit tests as part of an application design philosophy called *test-driven development*.</span></span> <span data-ttu-id="7886e-141">练习驱动开发时，先编写测试，然后针对测试编写代码。</span><span class="sxs-lookup"><span data-stu-id="7886e-141">When you practice test-driven development, you write tests first and then write code against the tests.</span></span>

<span data-ttu-id="7886e-142">更准确地说，在完成测试驱动开发时，创建代码时，需要完成三个步骤（红色/绿色/重构）：</span><span class="sxs-lookup"><span data-stu-id="7886e-142">More precisely, when practicing test-driven development, there are three steps that you complete when creating code (Red/ Green/Refactor):</span></span>

1. <span data-ttu-id="7886e-143">编写失败的单元测试（红色）</span><span class="sxs-lookup"><span data-stu-id="7886e-143">Write a unit test that fails (Red)</span></span>
2. <span data-ttu-id="7886e-144">编写通过单元测试的代码（绿色）</span><span class="sxs-lookup"><span data-stu-id="7886e-144">Write code that passes the unit test (Green)</span></span>
3. <span data-ttu-id="7886e-145">重构你的代码（重构）</span><span class="sxs-lookup"><span data-stu-id="7886e-145">Refactor your code (Refactor)</span></span>

<span data-ttu-id="7886e-146">首先，编写单元测试。</span><span class="sxs-lookup"><span data-stu-id="7886e-146">First, you write the unit test.</span></span> <span data-ttu-id="7886e-147">单元测试应表示你希望你的代码的行为方式。</span><span class="sxs-lookup"><span data-stu-id="7886e-147">The unit test should express your intention for how you expect your code to behave.</span></span> <span data-ttu-id="7886e-148">首次创建单元测试时，单元测试应失败。</span><span class="sxs-lookup"><span data-stu-id="7886e-148">When you first create the unit test, the unit test should fail.</span></span> <span data-ttu-id="7886e-149">测试应失败，因为尚未编写任何满足测试的应用程序代码。</span><span class="sxs-lookup"><span data-stu-id="7886e-149">The test should fail because you have not yet written any application code that satisfies the test.</span></span>

<span data-ttu-id="7886e-150">接下来，编写足够的代码，使单元测试通过。</span><span class="sxs-lookup"><span data-stu-id="7886e-150">Next, you write just enough code in order for the unit test to pass.</span></span> <span data-ttu-id="7886e-151">目标是以 laziest、sloppiest 和最快的方式编写代码。</span><span class="sxs-lookup"><span data-stu-id="7886e-151">The goal is to write the code in the laziest, sloppiest and fastest possible way.</span></span> <span data-ttu-id="7886e-152">您不应浪费时间思考您的应用程序的体系结构。</span><span class="sxs-lookup"><span data-stu-id="7886e-152">You should not waste time thinking about the architecture of your application.</span></span> <span data-ttu-id="7886e-153">相反，应重点编写满足单元测试所需目的所需的最少量代码。</span><span class="sxs-lookup"><span data-stu-id="7886e-153">Instead, you should focus on writing the minimal amount of code necessary to satisfy the intention expressed by the unit test.</span></span>

<span data-ttu-id="7886e-154">最后，在编写足够的代码后，你可以返回并考虑应用程序的总体体系结构。</span><span class="sxs-lookup"><span data-stu-id="7886e-154">Finally, after you have written enough code, you can step back and consider the overall architecture of your application.</span></span> <span data-ttu-id="7886e-155">在此步骤中，您将通过利用软件设计模式（例如存储库模式）重写（重构）您的代码，以便您的代码更易于维护。</span><span class="sxs-lookup"><span data-stu-id="7886e-155">In this step, you rewrite (refactor) your code by taking advantage of software design patterns -- such as the repository pattern -- so that your code is more maintainable.</span></span> <span data-ttu-id="7886e-156">你可以 fearlessly 在此步骤中重写代码，因为你的代码已被单元测试覆盖。</span><span class="sxs-lookup"><span data-stu-id="7886e-156">You can fearlessly rewrite your code in this step because your code is covered by unit tests.</span></span>

<span data-ttu-id="7886e-157">通过测试驱动开发，有很多好处。</span><span class="sxs-lookup"><span data-stu-id="7886e-157">There are many benefits that result from practicing test-driven development.</span></span> <span data-ttu-id="7886e-158">首先，由测试驱动的开发强制您关注实际需要编写的代码。</span><span class="sxs-lookup"><span data-stu-id="7886e-158">First, test-driven development forces you to focus on code that actually needs to be written.</span></span> <span data-ttu-id="7886e-159">由于你一直致力于编写足够的代码来传递特定测试，因此会阻止你 wandering 到黄龙，并编写大量不会使用的代码。</span><span class="sxs-lookup"><span data-stu-id="7886e-159">Because you are constantly focused on just writing enough code to pass a particular test, you are prevented from wandering into the weeds and writing massive amounts of code that you will never use.</span></span>

<span data-ttu-id="7886e-160">其次，"测试优先" 设计方法会强制您编写代码，从代码的使用角度来看。</span><span class="sxs-lookup"><span data-stu-id="7886e-160">Second, a "test first" design methodology forces you to write code from the perspective of how your code will be used.</span></span> <span data-ttu-id="7886e-161">换句话说，当练习驱动开发时，会不断地从用户角度编写测试。</span><span class="sxs-lookup"><span data-stu-id="7886e-161">In other words, when practicing test-driven development, you are constantly writing your tests from a user perspective.</span></span> <span data-ttu-id="7886e-162">因此，测试驱动的开发会导致更清晰且更易于理解的 Api。</span><span class="sxs-lookup"><span data-stu-id="7886e-162">Therefore, test-driven development can result in cleaner and more understandable APIs.</span></span>

<span data-ttu-id="7886e-163">最后，测试驱动的开发将强制你编写单元测试，作为编写应用程序的正常过程的一部分。</span><span class="sxs-lookup"><span data-stu-id="7886e-163">Finally, test-driven development forces you to write unit tests as part of the normal process of writing an application.</span></span> <span data-ttu-id="7886e-164">作为项目截止时间方法，测试通常是第一次进入窗口。</span><span class="sxs-lookup"><span data-stu-id="7886e-164">As a project deadline approaches, testing is typically the first thing that goes out the window.</span></span> <span data-ttu-id="7886e-165">另一方面，在进行测试驱动开发时，更有可能良性编写单元测试，因为测试驱动的开发会使单元测试成为构建应用程序的过程的核心。</span><span class="sxs-lookup"><span data-stu-id="7886e-165">When practicing test-driven development, on the other hand, you are more likely to be virtuous about writing unit tests because test-driven development makes unit tests central to the process of building an application.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="7886e-166">若要了解有关测试驱动开发的详细信息，建议阅读 Michael Feathers 书籍，**并有效地使用旧代码**。</span><span class="sxs-lookup"><span data-stu-id="7886e-166">To learn more about test-driven development, I recommend that you read Michael Feathers book **Working Effectively with Legacy Code**.</span></span>

<span data-ttu-id="7886e-167">在此迭代中，我们将向联系人管理器应用程序添加新功能。</span><span class="sxs-lookup"><span data-stu-id="7886e-167">In this iteration, we add a new feature to our Contact Manager application.</span></span> <span data-ttu-id="7886e-168">我们添加了对联系人组的支持。</span><span class="sxs-lookup"><span data-stu-id="7886e-168">We add support for Contact Groups.</span></span> <span data-ttu-id="7886e-169">您可以使用 "联系人组" 将您的联系人组织成不同的类别，例如业务和朋友组。</span><span class="sxs-lookup"><span data-stu-id="7886e-169">You can use Contact Groups to organize your contacts into categories such as Business and Friend groups.</span></span>

<span data-ttu-id="7886e-170">我们将按照测试驱动的开发过程将此新功能添加到我们的应用程序。</span><span class="sxs-lookup"><span data-stu-id="7886e-170">We'll add this new functionality to our application by following a process of test-driven development.</span></span> <span data-ttu-id="7886e-171">我们将首先编写单元测试，我们将针对这些测试编写所有代码。</span><span class="sxs-lookup"><span data-stu-id="7886e-171">We'll write our unit tests first and we'll write all of our code against these tests.</span></span>

## <a name="what-gets-tested"></a><span data-ttu-id="7886e-172">测试的内容</span><span class="sxs-lookup"><span data-stu-id="7886e-172">What Gets Tested</span></span>

<span data-ttu-id="7886e-173">如前面的迭代中所述，通常不为数据访问逻辑或查看逻辑编写单元测试。</span><span class="sxs-lookup"><span data-stu-id="7886e-173">As we discussed in the previous iteration, you typically do not write unit tests for data access logic or view logic.</span></span> <span data-ttu-id="7886e-174">你不为数据访问逻辑编写单元测试，因为访问数据库是相对较慢的操作。</span><span class="sxs-lookup"><span data-stu-id="7886e-174">You don t write unit tests for data access logic because accessing a database is a relatively slow operation.</span></span> <span data-ttu-id="7886e-175">你没有为视图逻辑编写单元测试，因为访问视图需要旋转 web 服务器，这是一个相对较慢的操作。</span><span class="sxs-lookup"><span data-stu-id="7886e-175">You don t write unit tests for view logic because accessing a view requires spinning up a web server which is a relatively slow operation.</span></span> <span data-ttu-id="7886e-176">您不应编写单元测试，除非该测试可以在同一速度的情况上反复执行</span><span class="sxs-lookup"><span data-stu-id="7886e-176">You shouldn't write a unit test unless the test can be executed over and over again very fast</span></span>

<span data-ttu-id="7886e-177">由于测试驱动的开发由单元测试驱动，因此我们最初重点介绍如何编写控制器和业务逻辑。</span><span class="sxs-lookup"><span data-stu-id="7886e-177">Because test-driven development is driven by unit tests, we focus initially on writing controller and business logic.</span></span> <span data-ttu-id="7886e-178">我们避免对数据库或视图进行触摸。</span><span class="sxs-lookup"><span data-stu-id="7886e-178">We avoid touching the database or views.</span></span> <span data-ttu-id="7886e-179">在本教程的最后结束之前，我们不会修改数据库或创建视图。</span><span class="sxs-lookup"><span data-stu-id="7886e-179">We won't modify the database or create our views until the very end of this tutorial.</span></span> <span data-ttu-id="7886e-180">我们从可测试的内容开始。</span><span class="sxs-lookup"><span data-stu-id="7886e-180">We start with what can be tested.</span></span>

## <a name="creating-user-stories"></a><span data-ttu-id="7886e-181">创建用户情景</span><span class="sxs-lookup"><span data-stu-id="7886e-181">Creating User Stories</span></span>

<span data-ttu-id="7886e-182">在练习驱动开发时，您始终可以编写测试。</span><span class="sxs-lookup"><span data-stu-id="7886e-182">When practicing test-driven development, you always start by writing a test.</span></span> <span data-ttu-id="7886e-183">这会立即提出问题：如何确定要首先编写哪些测试？</span><span class="sxs-lookup"><span data-stu-id="7886e-183">This immediately raises the question: How do you decide what test to write first?</span></span> <span data-ttu-id="7886e-184">若要回答此问题，应编写一组[**用户情景**](http://en.wikipedia.org/wiki/User_stories)。</span><span class="sxs-lookup"><span data-stu-id="7886e-184">To answer this question, you should write a set of [**user stories**](http://en.wikipedia.org/wiki/User_stories).</span></span>

<span data-ttu-id="7886e-185">用户情景是软件要求的一种非常简短的（通常是一句）说明。</span><span class="sxs-lookup"><span data-stu-id="7886e-185">A user story is a very brief (usually one sentence) description of a software requirement.</span></span> <span data-ttu-id="7886e-186">它应该是从用户角度编写的要求的非技术说明。</span><span class="sxs-lookup"><span data-stu-id="7886e-186">It should be a non-technical description of a requirement written from a user perspective.</span></span>

<span data-ttu-id="7886e-187">下面是描述新联系人组功能所需功能的一组用户情景：</span><span class="sxs-lookup"><span data-stu-id="7886e-187">Here s the set of user stories that describe the features required by the new Contact Group functionality:</span></span>

1. <span data-ttu-id="7886e-188">用户可以查看联系人组的列表。</span><span class="sxs-lookup"><span data-stu-id="7886e-188">User can view a list of contact groups.</span></span>
2. <span data-ttu-id="7886e-189">用户可以创建新的联系人组。</span><span class="sxs-lookup"><span data-stu-id="7886e-189">User can create a new contact group.</span></span>
3. <span data-ttu-id="7886e-190">用户可以删除现有的联系人组。</span><span class="sxs-lookup"><span data-stu-id="7886e-190">User can delete an existing contact group.</span></span>
4. <span data-ttu-id="7886e-191">创建新联系人时，用户可以选择联系人组。</span><span class="sxs-lookup"><span data-stu-id="7886e-191">User can select a contact group when creating a new contact.</span></span>
5. <span data-ttu-id="7886e-192">编辑现有联系人时，用户可以选择联系人组。</span><span class="sxs-lookup"><span data-stu-id="7886e-192">User can select a contact group when editing an existing contact.</span></span>
6. <span data-ttu-id="7886e-193">联系人组的列表显示在 "索引" 视图中。</span><span class="sxs-lookup"><span data-stu-id="7886e-193">A list of contact groups is displayed in the Index view.</span></span>
7. <span data-ttu-id="7886e-194">当用户单击某个联系人组时，将显示匹配联系人的列表。</span><span class="sxs-lookup"><span data-stu-id="7886e-194">When a user clicks a contact group, a list of matching contacts is displayed.</span></span>

<span data-ttu-id="7886e-195">请注意，用户情景列表完全可由客户理解。</span><span class="sxs-lookup"><span data-stu-id="7886e-195">Notice that this list of user stories is completely understandable by a customer.</span></span> <span data-ttu-id="7886e-196">没有提到技术实现细节。</span><span class="sxs-lookup"><span data-stu-id="7886e-196">There is no mention of technical implementation details.</span></span>

<span data-ttu-id="7886e-197">在构建应用程序的过程中，用户情景集可能会变得更加完善。</span><span class="sxs-lookup"><span data-stu-id="7886e-197">While in the process of building your application, the set of user stories can become more refined.</span></span> <span data-ttu-id="7886e-198">您可以将用户情景划分为多个情景（要求）。</span><span class="sxs-lookup"><span data-stu-id="7886e-198">You might break a user story into multiple stories (requirements).</span></span> <span data-ttu-id="7886e-199">例如，你可能会决定创建新的联系人组应涉及验证。</span><span class="sxs-lookup"><span data-stu-id="7886e-199">For example, you might decide that creating a new contact group should involve validation.</span></span> <span data-ttu-id="7886e-200">提交不带名称的联系人组应返回验证错误。</span><span class="sxs-lookup"><span data-stu-id="7886e-200">Submitting a contact group without a name should return a validation error.</span></span>

<span data-ttu-id="7886e-201">创建用户情景列表后，就可以编写第一个单元测试了。</span><span class="sxs-lookup"><span data-stu-id="7886e-201">After you create a list of user stories, you are ready to write your first unit test.</span></span> <span data-ttu-id="7886e-202">首先，我们将创建一个单元测试，用于查看联系人组的列表。</span><span class="sxs-lookup"><span data-stu-id="7886e-202">We'll start by creating a unit test for viewing the list of contact groups.</span></span>

## <a name="listing-contact-groups"></a><span data-ttu-id="7886e-203">列出联系人组</span><span class="sxs-lookup"><span data-stu-id="7886e-203">Listing Contact Groups</span></span>

<span data-ttu-id="7886e-204">第一个用户情景是，用户应该能够查看联系人组的列表。</span><span class="sxs-lookup"><span data-stu-id="7886e-204">Our first user story is that a user should be able to view a list of contact groups.</span></span> <span data-ttu-id="7886e-205">我们需要通过测试来表达这一故事。</span><span class="sxs-lookup"><span data-stu-id="7886e-205">We need to express this story with a test.</span></span>

<span data-ttu-id="7886e-206">通过在 ContactManager 项目中右键单击 "控制器" 文件夹，选择 "**添加"、"新建测试**"，然后选择**单元测试**模板来创建新的单元测试（请参阅图1）。</span><span class="sxs-lookup"><span data-stu-id="7886e-206">Create a new unit test by right-clicking the Controllers folder in the ContactManager.Tests project, selecting **Add, New Test**, and selecting the **Unit Test** template (see Figure 1).</span></span> <span data-ttu-id="7886e-207">命名新的单元测试 GroupControllerTest.cs，并单击 **"确定"** 按钮。</span><span class="sxs-lookup"><span data-stu-id="7886e-207">Name the new unit test GroupControllerTest.cs and click the **OK** button.</span></span>

<span data-ttu-id="7886e-208">[添加 GroupControllerTest 单元测试 ![](iteration-6-use-test-driven-development-cs/_static/image1.jpg)](iteration-6-use-test-driven-development-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="7886e-208">[![Adding the GroupControllerTest unit test](iteration-6-use-test-driven-development-cs/_static/image1.jpg)](iteration-6-use-test-driven-development-cs/_static/image1.png)</span></span>

<span data-ttu-id="7886e-209">**图 01**：添加 GroupControllerTest 单元测试（[单击以查看完全大小的映像](iteration-6-use-test-driven-development-cs/_static/image2.png)）</span><span class="sxs-lookup"><span data-stu-id="7886e-209">**Figure 01**: Adding the GroupControllerTest unit test([Click to view full-size image](iteration-6-use-test-driven-development-cs/_static/image2.png))</span></span>

<span data-ttu-id="7886e-210">第一个单元测试包含在列表1中。</span><span class="sxs-lookup"><span data-stu-id="7886e-210">Our first unit test is contained in Listing 1.</span></span> <span data-ttu-id="7886e-211">此测试验证组控制器的 Index （）方法是否返回一组组。</span><span class="sxs-lookup"><span data-stu-id="7886e-211">This test verifies that the Index() method of the Group controller returns a set of Groups.</span></span> <span data-ttu-id="7886e-212">测试将验证是否在视图数据中返回了组的集合。</span><span class="sxs-lookup"><span data-stu-id="7886e-212">The test verifies that a collection of Groups is returned in view data.</span></span>

<span data-ttu-id="7886e-213">**列表 1-Controllers\GroupControllerTest.cs**</span><span class="sxs-lookup"><span data-stu-id="7886e-213">**Listing 1 - Controllers\GroupControllerTest.cs**</span></span>

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample1.cs)]

<span data-ttu-id="7886e-214">第一次在 Visual Studio 中的列表1中键入代码时，会收到大量红色波浪线。</span><span class="sxs-lookup"><span data-stu-id="7886e-214">When you first type the code in Listing 1 in Visual Studio, you'll get a lot of red squiggly lines.</span></span> <span data-ttu-id="7886e-215">尚未创建 GroupController 类或组类。</span><span class="sxs-lookup"><span data-stu-id="7886e-215">We have not created the GroupController or Group classes.</span></span>

<span data-ttu-id="7886e-216">此时，我们甚至无法生成应用程序，因此我们不能执行第一个单元测试。</span><span class="sxs-lookup"><span data-stu-id="7886e-216">At this point, we can t even build our application so we can t execute our first unit test.</span></span> <span data-ttu-id="7886e-217">这就好了。</span><span class="sxs-lookup"><span data-stu-id="7886e-217">That s good.</span></span> <span data-ttu-id="7886e-218">这会计为失败测试。</span><span class="sxs-lookup"><span data-stu-id="7886e-218">That counts as a failing test.</span></span> <span data-ttu-id="7886e-219">因此，我们现在有权开始编写应用程序代码。</span><span class="sxs-lookup"><span data-stu-id="7886e-219">Therefore, we now have permission to start writing application code.</span></span> <span data-ttu-id="7886e-220">我们需要编写足够的代码来执行测试。</span><span class="sxs-lookup"><span data-stu-id="7886e-220">We need to write enough code to execute our test.</span></span>

<span data-ttu-id="7886e-221">清单2中的组控制器类包含传递单元测试所需的最少代码。</span><span class="sxs-lookup"><span data-stu-id="7886e-221">The Group controller class in Listing 2 contains the bare minimum of code required to pass the unit test.</span></span> <span data-ttu-id="7886e-222">Index （）操作返回一个静态编码的组列表（组类在列表3中定义）。</span><span class="sxs-lookup"><span data-stu-id="7886e-222">The Index() action returns a statically coded list of Groups (the Group class is defined in Listing 3).</span></span>

<span data-ttu-id="7886e-223">**列表 2-Controllers\GroupController.cs**</span><span class="sxs-lookup"><span data-stu-id="7886e-223">**Listing 2 - Controllers\GroupController.cs**</span></span>

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample2.cs)]

<span data-ttu-id="7886e-224">**列表 3-Models\Group.cs**</span><span class="sxs-lookup"><span data-stu-id="7886e-224">**Listing 3 - Models\Group.cs**</span></span>

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample3.cs)]

<span data-ttu-id="7886e-225">将 GroupController 和 Group 类添加到项目中后，第一个单元测试成功完成（参见图2）。</span><span class="sxs-lookup"><span data-stu-id="7886e-225">After we add the GroupController and Group classes to our project, our first unit test completes successfully (see Figure 2).</span></span> <span data-ttu-id="7886e-226">我们已经完成了通过测试所需的最少工作量。</span><span class="sxs-lookup"><span data-stu-id="7886e-226">We have done the minimum work required to pass the test.</span></span> <span data-ttu-id="7886e-227">现在可以庆祝了。</span><span class="sxs-lookup"><span data-stu-id="7886e-227">It is time to celebrate.</span></span>

<span data-ttu-id="7886e-228">[![成功！](iteration-6-use-test-driven-development-cs/_static/image2.jpg)](iteration-6-use-test-driven-development-cs/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="7886e-228">[![Success!](iteration-6-use-test-driven-development-cs/_static/image2.jpg)](iteration-6-use-test-driven-development-cs/_static/image3.png)</span></span>

<span data-ttu-id="7886e-229">**图 02**： Success！（[单击以查看完全大小的映像](iteration-6-use-test-driven-development-cs/_static/image4.png)）</span><span class="sxs-lookup"><span data-stu-id="7886e-229">**Figure 02**: Success!([Click to view full-size image](iteration-6-use-test-driven-development-cs/_static/image4.png))</span></span>

## <a name="creating-contact-groups"></a><span data-ttu-id="7886e-230">创建联系人组</span><span class="sxs-lookup"><span data-stu-id="7886e-230">Creating Contact Groups</span></span>

<span data-ttu-id="7886e-231">现在，我们可以转到第二个用户案例。</span><span class="sxs-lookup"><span data-stu-id="7886e-231">Now we can move on to the second user story.</span></span> <span data-ttu-id="7886e-232">我们需要能够创建新的联系人组。</span><span class="sxs-lookup"><span data-stu-id="7886e-232">We need to be able to create new contact groups.</span></span> <span data-ttu-id="7886e-233">我们需要通过测试表达这一意图。</span><span class="sxs-lookup"><span data-stu-id="7886e-233">We need to express this intention with a test.</span></span>

<span data-ttu-id="7886e-234">列表4中的测试验证通过新组调用 Create （）方法将该组添加到 Index （）方法返回的组列表。</span><span class="sxs-lookup"><span data-stu-id="7886e-234">The test in Listing 4 verifies that calling the Create() method with a new Group adds the Group to the list of Groups returned by the Index() method.</span></span> <span data-ttu-id="7886e-235">换句话说，如果我创建一个新组，则应该能够从 Index （）方法返回的组列表返回新组。</span><span class="sxs-lookup"><span data-stu-id="7886e-235">In other words, if I create a new group then I should be able to get the new Group back from the list of Groups returned by the Index() method.</span></span>

<span data-ttu-id="7886e-236">**列表 4-Controllers\GroupControllerTest.cs**</span><span class="sxs-lookup"><span data-stu-id="7886e-236">**Listing 4 - Controllers\GroupControllerTest.cs**</span></span>

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample4.cs)]

<span data-ttu-id="7886e-237">列表4中的测试通过新的联系人组调用组控制器 Create （）方法。</span><span class="sxs-lookup"><span data-stu-id="7886e-237">The test in Listing 4 calls the Group controller Create() method with a new contact Group.</span></span> <span data-ttu-id="7886e-238">接下来，测试验证调用组控制器索引（）方法是否在视图数据中返回新组。</span><span class="sxs-lookup"><span data-stu-id="7886e-238">Next, the test verifies that calling the Group controller Index() method returns the new Group in view data.</span></span>

<span data-ttu-id="7886e-239">列表5中修改后的组控制器包含通过新测试所需的最小更改。</span><span class="sxs-lookup"><span data-stu-id="7886e-239">The modified Group controller in Listing 5 contains the bare minimum of changes required to pass the new test.</span></span>

<span data-ttu-id="7886e-240">**列表 5-Controllers\GroupController.cs**</span><span class="sxs-lookup"><span data-stu-id="7886e-240">**Listing 5 - Controllers\GroupController.cs**</span></span>

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample5.cs)]

## <a name="the-group-controller-in-listing-5-has-a-new-create-action-this-action-adds-a-group-to-a-collection-of-groups-notice-that-the-index-action-has-been-modified-to-return-the-contents-of-the-collection-of-groups"></a><span data-ttu-id="7886e-241">列表5中的组控制器具有新的 Create （）操作。</span><span class="sxs-lookup"><span data-stu-id="7886e-241">The Group controller in Listing 5 has a new Create() action.</span></span> <span data-ttu-id="7886e-242">此操作可将组添加到组的集合。</span><span class="sxs-lookup"><span data-stu-id="7886e-242">This action adds a Group to a collection of Groups.</span></span> <span data-ttu-id="7886e-243">请注意，已修改 Index （）操作以返回组集合的内容。</span><span class="sxs-lookup"><span data-stu-id="7886e-243">Notice that the Index() action has been modified to return the contents of the collection of Groups.</span></span>

<span data-ttu-id="7886e-244">同样，我们已执行完传递单元测试所需的最少工作量。</span><span class="sxs-lookup"><span data-stu-id="7886e-244">Once again, we have performed the bare minimum amount of work required to pass the unit test.</span></span> <span data-ttu-id="7886e-245">对组控制器进行这些更改后，我们的所有单元测试都通过。</span><span class="sxs-lookup"><span data-stu-id="7886e-245">After we make these changes to the Group controller, all of our unit tests pass.</span></span>

## <a name="adding-validation"></a><span data-ttu-id="7886e-246">添加验证</span><span class="sxs-lookup"><span data-stu-id="7886e-246">Adding Validation</span></span>

<span data-ttu-id="7886e-247">用户情景中未明确说明此要求。</span><span class="sxs-lookup"><span data-stu-id="7886e-247">This requirement was not stated explicitly in the user story.</span></span> <span data-ttu-id="7886e-248">但是，要求组具有名称是合理的。</span><span class="sxs-lookup"><span data-stu-id="7886e-248">However, it is reasonable to require that a Group have a name.</span></span> <span data-ttu-id="7886e-249">否则，将联系人组织到组中将不会非常有用。</span><span class="sxs-lookup"><span data-stu-id="7886e-249">Otherwise, organizing contacts into Groups would not be very useful.</span></span>

<span data-ttu-id="7886e-250">清单6包含一个表示此目的的新测试。</span><span class="sxs-lookup"><span data-stu-id="7886e-250">Listing 6 contains a new test that expresses this intention.</span></span> <span data-ttu-id="7886e-251">此测试验证尝试在未提供名称的情况下创建组会导致在模型状态中出现验证错误消息。</span><span class="sxs-lookup"><span data-stu-id="7886e-251">This test verifies that attempting to create a Group without supplying a name results in a validation error message in model state.</span></span>

<span data-ttu-id="7886e-252">**列表 6-Controllers\GroupControllerTest.cs**</span><span class="sxs-lookup"><span data-stu-id="7886e-252">**Listing 6 - Controllers\GroupControllerTest.cs**</span></span>

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample6.cs)]

<span data-ttu-id="7886e-253">为了满足此测试要求，我们需要将 "名称" 属性添加到我们的组类（请参阅列表7）。</span><span class="sxs-lookup"><span data-stu-id="7886e-253">In order to satisfy this test, we need to add a Name property to our Group class (see Listing 7).</span></span> <span data-ttu-id="7886e-254">此外，我们还需要向组控制器 s Create （）操作添加一小段验证逻辑（请参阅列表8）。</span><span class="sxs-lookup"><span data-stu-id="7886e-254">Furthermore, we need to add a tiny bit of validation logic to our Group controller s Create() action (see Listing 8).</span></span>

<span data-ttu-id="7886e-255">**列表 7-Models\Group.cs**</span><span class="sxs-lookup"><span data-stu-id="7886e-255">**Listing 7 - Models\Group.cs**</span></span>

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample7.cs)]

<span data-ttu-id="7886e-256">**列表 8-Controllers\GroupController.cs**</span><span class="sxs-lookup"><span data-stu-id="7886e-256">**Listing 8 - Controllers\GroupController.cs**</span></span>

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample8.cs)]

<span data-ttu-id="7886e-257">请注意，组控制器 Create （）操作现在同时包含验证和数据库逻辑。</span><span class="sxs-lookup"><span data-stu-id="7886e-257">Notice that the Group controller Create() action now contains both validation and database logic.</span></span> <span data-ttu-id="7886e-258">目前，组控制器使用的数据库不只包含内存中集合。</span><span class="sxs-lookup"><span data-stu-id="7886e-258">Currently, the database used by the Group controller consists of nothing more than an in-memory collection.</span></span>

## <a name="time-to-refactor"></a><span data-ttu-id="7886e-259">重构时间</span><span class="sxs-lookup"><span data-stu-id="7886e-259">Time to Refactor</span></span>

<span data-ttu-id="7886e-260">红色/绿色/重构的第三步是重构部分。</span><span class="sxs-lookup"><span data-stu-id="7886e-260">The third step in Red/Green/Refactor is the Refactor part.</span></span> <span data-ttu-id="7886e-261">此时，我们需要从代码返回，并考虑如何重构应用程序以改善其设计。</span><span class="sxs-lookup"><span data-stu-id="7886e-261">At this point, we need to step back from our code and consider how we can refactor our application to improve its design.</span></span> <span data-ttu-id="7886e-262">"重构" 阶段是我们认为难以实现软件设计原则和模式的最佳方式。</span><span class="sxs-lookup"><span data-stu-id="7886e-262">The Refactor stage is the stage at which we think hard about the best way of implementing software design principles and patterns.</span></span>

<span data-ttu-id="7886e-263">我们可以按我们选择的任何方式修改代码，以改进代码设计。</span><span class="sxs-lookup"><span data-stu-id="7886e-263">We are free to modify our code in any way that we choose to improve the design of the code.</span></span> <span data-ttu-id="7886e-264">我们有一个安全的单元测试，阻止我们破坏现有功能。</span><span class="sxs-lookup"><span data-stu-id="7886e-264">We have a safety net of unit tests that prevent us from breaking existing functionality.</span></span>

<span data-ttu-id="7886e-265">目前，我们的组控制器从优秀的软件设计的角度来看是一种混乱。</span><span class="sxs-lookup"><span data-stu-id="7886e-265">Right now, our Group controller is a mess from the perspective of good software design.</span></span> <span data-ttu-id="7886e-266">组控制器包含验证和数据访问代码的混杂。</span><span class="sxs-lookup"><span data-stu-id="7886e-266">The Group controller contains a tangled mess of validation and data access code.</span></span> <span data-ttu-id="7886e-267">若要避免违反单一责任原则，需要将这些问题分隔到不同的类中。</span><span class="sxs-lookup"><span data-stu-id="7886e-267">To avoid violating the Single Responsibility Principle, we need to separate these concerns into different classes.</span></span>

<span data-ttu-id="7886e-268">重构的组控制器类包含在列表9中。</span><span class="sxs-lookup"><span data-stu-id="7886e-268">Our refactored Group controller class is contained in Listing 9.</span></span> <span data-ttu-id="7886e-269">已将控制器修改为使用 ContactManager 服务层。</span><span class="sxs-lookup"><span data-stu-id="7886e-269">The controller has been modified to use the ContactManager service layer.</span></span> <span data-ttu-id="7886e-270">这是与联系人控制器一起使用的服务层。</span><span class="sxs-lookup"><span data-stu-id="7886e-270">This is the same service layer that we use with the Contact controller.</span></span>

<span data-ttu-id="7886e-271">列表10包含添加到 ContactManager 服务层的新方法，以支持验证、列出和创建组。</span><span class="sxs-lookup"><span data-stu-id="7886e-271">Listing 10 contains the new methods added to the ContactManager service layer to support validating, listing, and creating groups.</span></span> <span data-ttu-id="7886e-272">更新了 IContactManagerService 接口，以包含新的方法。</span><span class="sxs-lookup"><span data-stu-id="7886e-272">The IContactManagerService interface was updated to include the new methods.</span></span>

<span data-ttu-id="7886e-273">列表11包含一个实现 IContactManagerRepository 接口的新 FakeContactManagerRepository 类。</span><span class="sxs-lookup"><span data-stu-id="7886e-273">Listing 11 contains a new FakeContactManagerRepository class that implements the IContactManagerRepository interface.</span></span> <span data-ttu-id="7886e-274">与也实现 IContactManagerRepository 接口的 EntityContactManagerRepository 类不同，我们的新 FakeContactManagerRepository 类不与数据库通信。</span><span class="sxs-lookup"><span data-stu-id="7886e-274">Unlike the EntityContactManagerRepository class that also implements the IContactManagerRepository interface, our new FakeContactManagerRepository class does not communicate with the database.</span></span> <span data-ttu-id="7886e-275">FakeContactManagerRepository 类使用内存中集合作为数据库的代理。</span><span class="sxs-lookup"><span data-stu-id="7886e-275">The FakeContactManagerRepository class uses an in-memory collection as a proxy for the database.</span></span> <span data-ttu-id="7886e-276">我们将在单元测试中使用此类作为假存储库层。</span><span class="sxs-lookup"><span data-stu-id="7886e-276">We'll use this class in our unit tests as a fake repository layer.</span></span>

<span data-ttu-id="7886e-277">**列表 9-Controllers\GroupController.cs**</span><span class="sxs-lookup"><span data-stu-id="7886e-277">**Listing 9 - Controllers\GroupController.cs**</span></span>

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample9.cs)]

<span data-ttu-id="7886e-278">**列表 10-Controllers\ContactManagerService.cs**</span><span class="sxs-lookup"><span data-stu-id="7886e-278">**Listing 10 - Controllers\ContactManagerService.cs**</span></span>

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample10.cs)]

<span data-ttu-id="7886e-279">**列表 11-Controllers\FakeContactManagerRepository.cs**</span><span class="sxs-lookup"><span data-stu-id="7886e-279">**Listing 11 - Controllers\FakeContactManagerRepository.cs**</span></span>

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample11.cs)]

<span data-ttu-id="7886e-280">修改 IContactManagerRepository 接口需要使用来实现 EntityContactManagerRepository 类中的 CreateGroup （）和 ListGroups （）方法。</span><span class="sxs-lookup"><span data-stu-id="7886e-280">Modifying the IContactManagerRepository interface requires use to implement the CreateGroup() and ListGroups() methods in the EntityContactManagerRepository class.</span></span> <span data-ttu-id="7886e-281">实现此目的的 laziest 和最快方法是添加如下所示的存根方法：</span><span class="sxs-lookup"><span data-stu-id="7886e-281">The laziest and fastest way to do this is to add stub methods that look like this:</span></span>   

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample12.cs)]

<span data-ttu-id="7886e-282">最后，对应用程序设计所做的这些更改需要我们对单元测试进行一些修改。</span><span class="sxs-lookup"><span data-stu-id="7886e-282">Finally, these changes to the design of our application require us to make some modifications to our unit tests.</span></span> <span data-ttu-id="7886e-283">我们现在需要在执行单元测试时使用 FakeContactManagerRepository。</span><span class="sxs-lookup"><span data-stu-id="7886e-283">We now need to use the FakeContactManagerRepository when performing the unit tests.</span></span> <span data-ttu-id="7886e-284">已更新的 GroupControllerTest 类包含在列表12中。</span><span class="sxs-lookup"><span data-stu-id="7886e-284">The updated GroupControllerTest class is contained in Listing 12.</span></span>

<span data-ttu-id="7886e-285">**列表 12-Controllers\GroupControllerTest.cs**</span><span class="sxs-lookup"><span data-stu-id="7886e-285">**Listing 12 - Controllers\GroupControllerTest.cs**</span></span>

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample13.cs)]

<span data-ttu-id="7886e-286">完成所有这些更改后，我们会再次通过所有单元测试。</span><span class="sxs-lookup"><span data-stu-id="7886e-286">After we make all of these changes, once again, all of our unit tests pass.</span></span> <span data-ttu-id="7886e-287">我们已经完成了红色/绿色/重构的整个循环。</span><span class="sxs-lookup"><span data-stu-id="7886e-287">We have completed the entire cycle of Red/Green/Refactor.</span></span> <span data-ttu-id="7886e-288">我们已经实现了前两个用户情景。</span><span class="sxs-lookup"><span data-stu-id="7886e-288">We have implemented the first two user stories.</span></span> <span data-ttu-id="7886e-289">现在，我们已支持用户情景中表示的要求的单元测试。</span><span class="sxs-lookup"><span data-stu-id="7886e-289">We now have supporting unit tests for the requirements expressed in the user stories.</span></span> <span data-ttu-id="7886e-290">实现用户情景的其余部分涉及重复相同的红色/绿色/重构循环。</span><span class="sxs-lookup"><span data-stu-id="7886e-290">Implementing the remainder of the user stories involves repeating the same cycle of Red/Green/Refactor.</span></span>

## <a name="modifying-our-database"></a><span data-ttu-id="7886e-291">修改数据库</span><span class="sxs-lookup"><span data-stu-id="7886e-291">Modifying our Database</span></span>

<span data-ttu-id="7886e-292">遗憾的是，尽管我们已经满足单元测试所表示的所有需求，但我们的工作却不能完成。</span><span class="sxs-lookup"><span data-stu-id="7886e-292">Unfortunately, even though we have satisfied all of the requirements expressed by our unit tests, our work is not done.</span></span> <span data-ttu-id="7886e-293">我们仍需要修改数据库。</span><span class="sxs-lookup"><span data-stu-id="7886e-293">We still need to modify our database.</span></span>

<span data-ttu-id="7886e-294">我们需要创建一个新的组数据库表。</span><span class="sxs-lookup"><span data-stu-id="7886e-294">We need to create a new Group database table.</span></span> <span data-ttu-id="7886e-295">请执行这些步骤：</span><span class="sxs-lookup"><span data-stu-id="7886e-295">Follow these steps:</span></span>

1. <span data-ttu-id="7886e-296">在 "服务器资源管理器" 窗口中，右键单击 "表" 文件夹，然后选择 "**添加新表**" 菜单选项。</span><span class="sxs-lookup"><span data-stu-id="7886e-296">In the Server Explorer window, right-click the Tables folder and select the menu option **Add New Table**.</span></span>
2. <span data-ttu-id="7886e-297">在表设计器中输入下面所述的两个列。</span><span class="sxs-lookup"><span data-stu-id="7886e-297">Enter the two columns described below in the Table Designer.</span></span>
3. <span data-ttu-id="7886e-298">将 Id 列标记为主键和标识列。</span><span class="sxs-lookup"><span data-stu-id="7886e-298">Mark the Id column as a primary key and Identity column.</span></span>
4. <span data-ttu-id="7886e-299">通过单击软盘的图标，使用名称组保存新表。</span><span class="sxs-lookup"><span data-stu-id="7886e-299">Save the new table with the name Groups by clicking the icon of the floppy.</span></span>

<a id="0.11_table01"></a>

| <span data-ttu-id="7886e-300">**列名称**</span><span class="sxs-lookup"><span data-stu-id="7886e-300">**Column Name**</span></span> | <span data-ttu-id="7886e-301">**数据类型**</span><span class="sxs-lookup"><span data-stu-id="7886e-301">**Data Type**</span></span> | <span data-ttu-id="7886e-302">**允许 Null 值**</span><span class="sxs-lookup"><span data-stu-id="7886e-302">**Allow Nulls**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7886e-303">Id</span><span class="sxs-lookup"><span data-stu-id="7886e-303">Id</span></span> | <span data-ttu-id="7886e-304">int</span><span class="sxs-lookup"><span data-stu-id="7886e-304">int</span></span> | <span data-ttu-id="7886e-305">False</span><span class="sxs-lookup"><span data-stu-id="7886e-305">False</span></span> |
| <span data-ttu-id="7886e-306">“属性”</span><span class="sxs-lookup"><span data-stu-id="7886e-306">Name</span></span> | <span data-ttu-id="7886e-307">nvarchar(50)</span><span class="sxs-lookup"><span data-stu-id="7886e-307">nvarchar(50)</span></span> | <span data-ttu-id="7886e-308">False</span><span class="sxs-lookup"><span data-stu-id="7886e-308">False</span></span> |

<span data-ttu-id="7886e-309">接下来，需要删除 Contacts 表中的所有数据（否则，我们将无法在 "联系人" 和 "组" 表之间创建关系）。</span><span class="sxs-lookup"><span data-stu-id="7886e-309">Next, we need to delete all of the data from the Contacts table (otherwise, we won't be able to create a relationship between the Contacts and Groups tables).</span></span> <span data-ttu-id="7886e-310">请执行这些步骤：</span><span class="sxs-lookup"><span data-stu-id="7886e-310">Follow these steps:</span></span>

1. <span data-ttu-id="7886e-311">右键单击 "联系人" 表，然后选择菜单选项 "**显示表数据**"。</span><span class="sxs-lookup"><span data-stu-id="7886e-311">Right-click the Contacts table and select the menu option **Show Table Data**.</span></span>
2. <span data-ttu-id="7886e-312">删除所有行。</span><span class="sxs-lookup"><span data-stu-id="7886e-312">Delete all of the rows.</span></span>

<span data-ttu-id="7886e-313">接下来，需要定义组数据库表和现有联系人数据库表之间的关系。</span><span class="sxs-lookup"><span data-stu-id="7886e-313">Next, we need to define a relationship between the Groups database table and the existing Contacts database table.</span></span> <span data-ttu-id="7886e-314">请执行这些步骤：</span><span class="sxs-lookup"><span data-stu-id="7886e-314">Follow these steps:</span></span>

1. <span data-ttu-id="7886e-315">双击 "服务器资源管理器" 窗口中的 "联系人" 表，打开表设计器。</span><span class="sxs-lookup"><span data-stu-id="7886e-315">Double-click the Contacts table in the Server Explorer window to open the Table Designer.</span></span>
2. <span data-ttu-id="7886e-316">向名为 GroupId 的联系人表中添加一个新的整数列。</span><span class="sxs-lookup"><span data-stu-id="7886e-316">Add a new integer column to the Contacts table named GroupId.</span></span>
3. <span data-ttu-id="7886e-317">单击 "关系" 按钮以打开 "外键关系" 对话框（请参阅图3）。</span><span class="sxs-lookup"><span data-stu-id="7886e-317">Click the Relationship button to open the Foreign Key Relationships dialog (see Figure 3).</span></span>
4. <span data-ttu-id="7886e-318">单击“添加”按钮。</span><span class="sxs-lookup"><span data-stu-id="7886e-318">Click the Add button.</span></span>
5. <span data-ttu-id="7886e-319">单击出现在 "表和列规范" 按钮旁的省略号按钮。</span><span class="sxs-lookup"><span data-stu-id="7886e-319">Click the ellipsis button that appears next to the Table and Columns Specification button.</span></span>
6. <span data-ttu-id="7886e-320">在 "表和列" 对话框中，选择 "组" 作为主键表，Id 作为主键列。</span><span class="sxs-lookup"><span data-stu-id="7886e-320">In the Tables and Columns dialog, select Groups as the primary key table and Id as the primary key column.</span></span> <span data-ttu-id="7886e-321">选择 "联系人" 作为外键表，并选择 "GroupId" 作为外键列（参见图4）。</span><span class="sxs-lookup"><span data-stu-id="7886e-321">Select Contacts as the foreign key table and GroupId as the foreign key column (see Figure 4).</span></span> <span data-ttu-id="7886e-322">单击“确定”按钮。</span><span class="sxs-lookup"><span data-stu-id="7886e-322">Click the OK button.</span></span>
7. <span data-ttu-id="7886e-323">在 "**插入和更新规范**" 下，选择 "**删除规则**的值**级联**"。</span><span class="sxs-lookup"><span data-stu-id="7886e-323">Under **INSERT and UPDATE Specification**, select the value **Cascade** for **Delete Rule**.</span></span>
8. <span data-ttu-id="7886e-324">单击 "关闭" 按钮以关闭 "外键关系" 对话框。</span><span class="sxs-lookup"><span data-stu-id="7886e-324">Click the Close button to close the Foreign Key Relationships dialog.</span></span>
9. <span data-ttu-id="7886e-325">单击 "保存" 按钮以保存对 "联系人" 表所做的更改。</span><span class="sxs-lookup"><span data-stu-id="7886e-325">Click the Save button to save the changes to the Contacts table.</span></span>

<span data-ttu-id="7886e-326">[创建数据库表关系 ![](iteration-6-use-test-driven-development-cs/_static/image3.jpg)](iteration-6-use-test-driven-development-cs/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="7886e-326">[![Creating a database table relationship](iteration-6-use-test-driven-development-cs/_static/image3.jpg)](iteration-6-use-test-driven-development-cs/_static/image5.png)</span></span>

<span data-ttu-id="7886e-327">**图 03**：创建数据库表关系（[单击查看完全大小的图像](iteration-6-use-test-driven-development-cs/_static/image6.png)）</span><span class="sxs-lookup"><span data-stu-id="7886e-327">**Figure 03**: Creating a database table relationship ([Click to view full-size image](iteration-6-use-test-driven-development-cs/_static/image6.png))</span></span>

<span data-ttu-id="7886e-328">[指定表关系 ![](iteration-6-use-test-driven-development-cs/_static/image4.jpg)](iteration-6-use-test-driven-development-cs/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="7886e-328">[![Specifying table relationships](iteration-6-use-test-driven-development-cs/_static/image4.jpg)](iteration-6-use-test-driven-development-cs/_static/image7.png)</span></span>

<span data-ttu-id="7886e-329">**图 04**：指定表关系（[单击查看完全大小的图像](iteration-6-use-test-driven-development-cs/_static/image8.png)）</span><span class="sxs-lookup"><span data-stu-id="7886e-329">**Figure 04**: Specifying table relationships([Click to view full-size image](iteration-6-use-test-driven-development-cs/_static/image8.png))</span></span>

### <a name="updating-our-data-model"></a><span data-ttu-id="7886e-330">更新数据模型</span><span class="sxs-lookup"><span data-stu-id="7886e-330">Updating our Data Model</span></span>

<span data-ttu-id="7886e-331">接下来，我们需要更新数据模型以表示新的数据库表。</span><span class="sxs-lookup"><span data-stu-id="7886e-331">Next, we need to update our data model to represent the new database table.</span></span> <span data-ttu-id="7886e-332">请执行这些步骤：</span><span class="sxs-lookup"><span data-stu-id="7886e-332">Follow these steps:</span></span>

1. <span data-ttu-id="7886e-333">双击 "模型" 文件夹中的 ContactManagerModel 文件以打开 Entity Designer。</span><span class="sxs-lookup"><span data-stu-id="7886e-333">Double-click the ContactManagerModel.edmx file in the Models folder to open the Entity Designer.</span></span>
2. <span data-ttu-id="7886e-334">右键单击设计器图面，然后选择 "**从数据库更新模型**" 菜单选项。</span><span class="sxs-lookup"><span data-stu-id="7886e-334">Right-click the Designer surface and select the menu option **Update Model from Database**.</span></span>
3. <span data-ttu-id="7886e-335">在更新向导中，选择 "组" 表，然后单击 "完成" 按钮（见图5）。</span><span class="sxs-lookup"><span data-stu-id="7886e-335">In the Update Wizard, select the Groups table and click the Finish button (see Figure 5).</span></span>
4. <span data-ttu-id="7886e-336">右键单击 "组" 实体并选择 "**重命名**" 菜单选项。</span><span class="sxs-lookup"><span data-stu-id="7886e-336">Right-click the Groups entity and select the menu option **Rename**.</span></span> <span data-ttu-id="7886e-337">将 "*组*" 实体的名称更改为 "*分组*（单数）"。</span><span class="sxs-lookup"><span data-stu-id="7886e-337">Change the name of the *Groups* entity to *Group* (singular).</span></span>
5. <span data-ttu-id="7886e-338">右键单击显示在 Contact 实体底部的 "组" 导航属性。</span><span class="sxs-lookup"><span data-stu-id="7886e-338">Right-click the Groups navigation property that appears at the bottom of the Contact entity.</span></span> <span data-ttu-id="7886e-339">将*组*导航属性的名称更改为 "*分组*（单数）"。</span><span class="sxs-lookup"><span data-stu-id="7886e-339">Change the name of the *Groups* navigation property to *Group* (singular).</span></span>

<span data-ttu-id="7886e-340">[![从数据库更新实体框架模型](iteration-6-use-test-driven-development-cs/_static/image5.jpg)](iteration-6-use-test-driven-development-cs/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="7886e-340">[![Updating an Entity Framework model from the database](iteration-6-use-test-driven-development-cs/_static/image5.jpg)](iteration-6-use-test-driven-development-cs/_static/image9.png)</span></span>

<span data-ttu-id="7886e-341">**图 05**：从数据库更新实体框架模型（[单击以查看完全大小的映像](iteration-6-use-test-driven-development-cs/_static/image10.png)）</span><span class="sxs-lookup"><span data-stu-id="7886e-341">**Figure 05**: Updating an Entity Framework model from the database([Click to view full-size image](iteration-6-use-test-driven-development-cs/_static/image10.png))</span></span>

<span data-ttu-id="7886e-342">完成这些步骤后，你的数据模型将同时表示 "联系人" 和 "组" 表。</span><span class="sxs-lookup"><span data-stu-id="7886e-342">After you complete these steps, your data model will represent both the Contacts and Groups tables.</span></span> <span data-ttu-id="7886e-343">Entity Designer 应显示这两个实体（见图6）。</span><span class="sxs-lookup"><span data-stu-id="7886e-343">The Entity Designer should show both entities (see Figure 6).</span></span>

<span data-ttu-id="7886e-344">[显示组和联系人 Entity Designer ![](iteration-6-use-test-driven-development-cs/_static/image6.jpg)](iteration-6-use-test-driven-development-cs/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="7886e-344">[![Entity Designer displaying Group and Contact](iteration-6-use-test-driven-development-cs/_static/image6.jpg)](iteration-6-use-test-driven-development-cs/_static/image11.png)</span></span>

<span data-ttu-id="7886e-345">**图 06**：显示组和联系人的 Entity Designer （[单击查看完全大小的图像](iteration-6-use-test-driven-development-cs/_static/image12.png)）</span><span class="sxs-lookup"><span data-stu-id="7886e-345">**Figure 06**: Entity Designer displaying Group and Contact([Click to view full-size image](iteration-6-use-test-driven-development-cs/_static/image12.png))</span></span>

### <a name="creating-our-repository-classes"></a><span data-ttu-id="7886e-346">创建我们的存储库类</span><span class="sxs-lookup"><span data-stu-id="7886e-346">Creating our Repository Classes</span></span>

<span data-ttu-id="7886e-347">接下来，我们需要实现存储库类。</span><span class="sxs-lookup"><span data-stu-id="7886e-347">Next, we need to implement our repository class.</span></span> <span data-ttu-id="7886e-348">在此迭代过程中，我们在编写代码来满足单元测试的同时，在 IContactManagerRepository 接口中添加了几个新方法。</span><span class="sxs-lookup"><span data-stu-id="7886e-348">Over the course of this iteration, we added several new methods to the IContactManagerRepository interface while writing code to satisfy our unit tests.</span></span> <span data-ttu-id="7886e-349">IContactManagerRepository 接口的最终版本包含在列表14中。</span><span class="sxs-lookup"><span data-stu-id="7886e-349">The final version of the IContactManagerRepository interface is contained in Listing 14.</span></span>

<span data-ttu-id="7886e-350">**列表 14-Models\IContactManagerRepository.cs**</span><span class="sxs-lookup"><span data-stu-id="7886e-350">**Listing 14 - Models\IContactManagerRepository.cs**</span></span>

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample14.cs)]

<span data-ttu-id="7886e-351">我们实际上并未实现任何与使用联系人组相关的方法。</span><span class="sxs-lookup"><span data-stu-id="7886e-351">We haven't actually implemented any of the methods related to working with contact groups.</span></span> <span data-ttu-id="7886e-352">目前，EntityContactManagerRepository 类具有 IContactManagerRepository 接口中列出的每个联系人组方法的存根方法。</span><span class="sxs-lookup"><span data-stu-id="7886e-352">Currently, the EntityContactManagerRepository class has stub methods for each of the contact group methods listed in the IContactManagerRepository interface.</span></span> <span data-ttu-id="7886e-353">例如，ListGroups （）方法当前如下所示：</span><span class="sxs-lookup"><span data-stu-id="7886e-353">For example, the ListGroups() method currently looks like this:</span></span>

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample15.cs)]

<span data-ttu-id="7886e-354">存根方法使我们能够编译应用程序并传递单元测试。</span><span class="sxs-lookup"><span data-stu-id="7886e-354">The stub methods enabled us to compile our application and pass the unit tests.</span></span> <span data-ttu-id="7886e-355">不过，现在可以实际实现这些方法。</span><span class="sxs-lookup"><span data-stu-id="7886e-355">However, now it is time to actually implement these methods.</span></span> <span data-ttu-id="7886e-356">列表13中包含了 EntityContactManagerRepository 类的最终版本。</span><span class="sxs-lookup"><span data-stu-id="7886e-356">The final version of the EntityContactManagerRepository class is contained in Listing 13.</span></span>

<span data-ttu-id="7886e-357">**列表 13-Models\EntityContactManagerRepository.cs**</span><span class="sxs-lookup"><span data-stu-id="7886e-357">**Listing 13 - Models\EntityContactManagerRepository.cs**</span></span>

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample16.cs)]

### <a name="creating-the-views"></a><span data-ttu-id="7886e-358">创建视图</span><span class="sxs-lookup"><span data-stu-id="7886e-358">Creating the Views</span></span>

<span data-ttu-id="7886e-359">当你使用默认的 ASP.NET 视图引擎时，ASP.NET MVC 应用程序。</span><span class="sxs-lookup"><span data-stu-id="7886e-359">ASP.NET MVC application when you use the default ASP.NET view engine.</span></span> <span data-ttu-id="7886e-360">因此，你不会创建用于响应特定单元测试的视图。</span><span class="sxs-lookup"><span data-stu-id="7886e-360">So, you don t create views in response to a particular unit test.</span></span> <span data-ttu-id="7886e-361">但是，因为在没有视图的情况下，应用程序不能使用，因此，我们无法在不创建和修改 Contact Manager 应用程序中包含的视图的情况下完成此迭代。</span><span class="sxs-lookup"><span data-stu-id="7886e-361">However, because an application would be useless without views, we can t complete this iteration without creating and modifying the views contained in the Contact Manager application.</span></span>

<span data-ttu-id="7886e-362">我们需要创建以下新视图来管理联系人组（请参阅图7）：</span><span class="sxs-lookup"><span data-stu-id="7886e-362">We need to create the following new views for managing contact groups (see Figure 7):</span></span>

- <span data-ttu-id="7886e-363">Views\Group\Index.aspx-显示联系人组列表</span><span class="sxs-lookup"><span data-stu-id="7886e-363">Views\Group\Index.aspx - Displays list of contact groups</span></span>
- <span data-ttu-id="7886e-364">Views\Group\Delete.aspx-显示用于删除联系人组的确认表单</span><span class="sxs-lookup"><span data-stu-id="7886e-364">Views\Group\Delete.aspx - Displays confirmation form for deleting a contact group</span></span>

<span data-ttu-id="7886e-365">[![组索引视图](iteration-6-use-test-driven-development-cs/_static/image7.jpg)](iteration-6-use-test-driven-development-cs/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="7886e-365">[![The Group Index view](iteration-6-use-test-driven-development-cs/_static/image7.jpg)](iteration-6-use-test-driven-development-cs/_static/image13.png)</span></span>

<span data-ttu-id="7886e-366">**图 07**：组索引视图（[单击以查看完全大小的图像](iteration-6-use-test-driven-development-cs/_static/image14.png)）</span><span class="sxs-lookup"><span data-stu-id="7886e-366">**Figure 07**: The Group Index view([Click to view full-size image](iteration-6-use-test-driven-development-cs/_static/image14.png))</span></span>

<span data-ttu-id="7886e-367">我们需要修改以下现有视图，使其包括联系人组：</span><span class="sxs-lookup"><span data-stu-id="7886e-367">We need to modify the following existing views so that they include contact groups:</span></span>

- <span data-ttu-id="7886e-368">Views\Home\Create.aspx</span><span class="sxs-lookup"><span data-stu-id="7886e-368">Views\Home\Create.aspx</span></span>
- <span data-ttu-id="7886e-369">Views\Home\Edit.aspx</span><span class="sxs-lookup"><span data-stu-id="7886e-369">Views\Home\Edit.aspx</span></span>
- <span data-ttu-id="7886e-370">Views\Home\Index.aspx</span><span class="sxs-lookup"><span data-stu-id="7886e-370">Views\Home\Index.aspx</span></span>

<span data-ttu-id="7886e-371">通过查看本教程附带的 Visual Studio 应用程序，可以看到修改后的视图。</span><span class="sxs-lookup"><span data-stu-id="7886e-371">You can see the modified views by looking at the Visual Studio application that accompanies this tutorial.</span></span> <span data-ttu-id="7886e-372">例如，图8说明了联系人索引视图。</span><span class="sxs-lookup"><span data-stu-id="7886e-372">For example, Figure 8 illustrates the Contact Index view.</span></span>

<span data-ttu-id="7886e-373">[![联系人索引视图](iteration-6-use-test-driven-development-cs/_static/image8.jpg)](iteration-6-use-test-driven-development-cs/_static/image15.png)</span><span class="sxs-lookup"><span data-stu-id="7886e-373">[![The Contact Index view](iteration-6-use-test-driven-development-cs/_static/image8.jpg)](iteration-6-use-test-driven-development-cs/_static/image15.png)</span></span>

<span data-ttu-id="7886e-374">**图 08**：联系人索引视图（[单击查看完全大小的图像](iteration-6-use-test-driven-development-cs/_static/image16.png)）</span><span class="sxs-lookup"><span data-stu-id="7886e-374">**Figure 08**: The Contact Index view([Click to view full-size image](iteration-6-use-test-driven-development-cs/_static/image16.png))</span></span>

## <a name="summary"></a><span data-ttu-id="7886e-375">摘要</span><span class="sxs-lookup"><span data-stu-id="7886e-375">Summary</span></span>

<span data-ttu-id="7886e-376">在此迭代中，我们将按照测试驱动的开发应用程序设计方法，向联系人管理器应用程序添加新功能。</span><span class="sxs-lookup"><span data-stu-id="7886e-376">In this iteration, we added new functionality to our Contact Manager application by following a test-driven development application design methodology.</span></span> <span data-ttu-id="7886e-377">我们首先创建一组用户情景。</span><span class="sxs-lookup"><span data-stu-id="7886e-377">We started by creating a set of user stories.</span></span> <span data-ttu-id="7886e-378">我们创建了一组与用户情景表示的要求相对应的单元测试。</span><span class="sxs-lookup"><span data-stu-id="7886e-378">We created a set of unit tests that corresponds to the requirements expressed by the user stories.</span></span> <span data-ttu-id="7886e-379">最后，我们编写了足够的代码来满足单元测试所表示的需求。</span><span class="sxs-lookup"><span data-stu-id="7886e-379">Finally, we wrote just enough code to satisfy the requirements expressed by the unit tests.</span></span>

<span data-ttu-id="7886e-380">编写完足够的代码来满足单元测试所表示的要求后，我们更新了数据库和视图。</span><span class="sxs-lookup"><span data-stu-id="7886e-380">After we finished writing enough code to satisfy the requirements expressed by the unit tests, we updated our database and views.</span></span> <span data-ttu-id="7886e-381">我们向数据库中添加了一个新的 "组" 表，并更新了实体框架数据模型。</span><span class="sxs-lookup"><span data-stu-id="7886e-381">We added a new Groups table to our database and updated our Entity Framework Data Model.</span></span> <span data-ttu-id="7886e-382">我们还创建和修改了一组视图。</span><span class="sxs-lookup"><span data-stu-id="7886e-382">We also created and modified a set of views.</span></span>

<span data-ttu-id="7886e-383">在下一次迭代中，最后一次迭代-我们会重写应用程序以利用 Ajax。</span><span class="sxs-lookup"><span data-stu-id="7886e-383">In the next iteration -- the final iteration -- we rewrite our application to take advantage of Ajax.</span></span> <span data-ttu-id="7886e-384">利用 Ajax，我们将提高联系人管理器应用程序的响应能力和性能。</span><span class="sxs-lookup"><span data-stu-id="7886e-384">By taking advantage of Ajax, we'll improve the responsiveness and performance of the Contact Manager application.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="7886e-385">[上一页](iteration-5-create-unit-tests-cs.md)
> [下一页](iteration-7-add-ajax-functionality-cs.md)</span><span class="sxs-lookup"><span data-stu-id="7886e-385">[Previous](iteration-5-create-unit-tests-cs.md)
[Next](iteration-7-add-ajax-functionality-cs.md)</span></span>
