---
uid: mvc/overview/security/preventing-open-redirection-attacks
title: 阻止打开重定向攻击C#（） |Microsoft Docs
author: jongalloway
description: 本教程介绍如何在 ASP.NET MVC 应用程序中阻止开放重定向攻击。 本教程将讨论已进行的更改 。
ms.author: riande
ms.date: 02/27/2014
ms.assetid: 69fb02e0-f5b7-4c35-878c-fa87164fc785
msc.legacyurl: /mvc/overview/security/preventing-open-redirection-attacks
msc.type: authoredcontent
ms.openlocfilehash: cfa635d4fd14d031993c5b452325cbe334f82dc2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78432584"
---
# <a name="preventing-open-redirection-attacks-c"></a><span data-ttu-id="96229-104">阻止打开重定向攻击 (C#)</span><span class="sxs-lookup"><span data-stu-id="96229-104">Preventing Open Redirection Attacks (C#)</span></span>

<span data-ttu-id="96229-105">作者： [Jon Galloway](https://github.com/jongalloway)</span><span class="sxs-lookup"><span data-stu-id="96229-105">by [Jon Galloway](https://github.com/jongalloway)</span></span>

> <span data-ttu-id="96229-106">本教程介绍如何在 ASP.NET MVC 应用程序中阻止开放重定向攻击。</span><span class="sxs-lookup"><span data-stu-id="96229-106">This tutorial explains how you can prevent open redirection attacks in your ASP.NET MVC applications.</span></span> <span data-ttu-id="96229-107">本教程讨论了在 ASP.NET MVC 3 的 AccountController 中所做的更改，并演示了如何在现有的 ASP.NET MVC 1.0 和2应用程序中应用这些更改。</span><span class="sxs-lookup"><span data-stu-id="96229-107">This tutorial discusses the changes that have been made in the AccountController in ASP.NET MVC 3 and demonstrates how you can apply these changes in your existing ASP.NET MVC 1.0 and 2 applications.</span></span>

## <a name="what-is-an-open-redirection-attack"></a><span data-ttu-id="96229-108">什么是开放重定向攻击？</span><span class="sxs-lookup"><span data-stu-id="96229-108">What is an Open Redirection Attack?</span></span>

<span data-ttu-id="96229-109">重定向到通过请求（如 querystring 或窗体数据）指定的 URL 的任何 web 应用程序可能会被篡改，以将用户重定向到外部恶意 URL。</span><span class="sxs-lookup"><span data-stu-id="96229-109">Any web application that redirects to a URL that is specified via the request such as the querystring or form data can potentially be tampered with to redirect users to an external, malicious URL.</span></span> <span data-ttu-id="96229-110">这种篡改称为 "开放重定向攻击"。</span><span class="sxs-lookup"><span data-stu-id="96229-110">This tampering is called an open redirection attack.</span></span>

<span data-ttu-id="96229-111">每当应用程序逻辑重定向到指定的 URL 时，必须验证重定向 URL 是否未被篡改。</span><span class="sxs-lookup"><span data-stu-id="96229-111">Whenever your application logic redirects to a specified URL, you must verify that the redirection URL hasn't been tampered with.</span></span> <span data-ttu-id="96229-112">用于 ASP.NET MVC 1.0 和 ASP.NET MVC 2 的默认 AccountController 中使用的登录名容易受到开放重定向攻击。</span><span class="sxs-lookup"><span data-stu-id="96229-112">The login used in the default AccountController for both ASP.NET MVC 1.0 and ASP.NET MVC 2 is vulnerable to open redirection attacks.</span></span> <span data-ttu-id="96229-113">幸运的是，可以轻松地更新现有应用程序，以使用 ASP.NET MVC 3 预览版中的更正。</span><span class="sxs-lookup"><span data-stu-id="96229-113">Fortunately, it is easy to update your existing applications to use the corrections from the ASP.NET MVC 3 Preview.</span></span>

<span data-ttu-id="96229-114">若要了解该漏洞，请查看登录重定向在默认的 ASP.NET MVC 2 Web 应用程序项目中的工作原理。</span><span class="sxs-lookup"><span data-stu-id="96229-114">To understand the vulnerability, let's look at how the login redirection works in a default ASP.NET MVC 2 Web Application project.</span></span> <span data-ttu-id="96229-115">在此应用程序中，尝试访问具有 [授权] 属性的控制器操作会将未经授权的用户重定向到/Account/LogOn 视图。</span><span class="sxs-lookup"><span data-stu-id="96229-115">In this application, attempting to visit a controller action that has the [Authorize] attribute will redirect unauthorized users to the /Account/LogOn view.</span></span> <span data-ttu-id="96229-116">这种重定向到/Account/LogOn 的将包含一个 returnUrl 查询字符串参数，以便用户在成功登录后可以返回到最初请求的 URL。</span><span class="sxs-lookup"><span data-stu-id="96229-116">This redirect to /Account/LogOn will include a returnUrl querystring parameter so that the user can be returned to the originally requested URL after they have successfully logged in.</span></span>

<span data-ttu-id="96229-117">在下面的屏幕截图中，我们可以看到，如果未登录，尝试访问/Account/ChangePassword 视图会导致重定向到/Account/LogOn？ReturnUrl =% 2fAccount% 2fChangePassword% 2f。</span><span class="sxs-lookup"><span data-stu-id="96229-117">In the screenshot below, we can see that an attempt to access the /Account/ChangePassword view when not logged in results in a redirect to /Account/LogOn?ReturnUrl=%2fAccount%2fChangePassword%2f.</span></span>

[![](preventing-open-redirection-attacks/_static/image2.png)](preventing-open-redirection-attacks/_static/image1.png)

<span data-ttu-id="96229-118">**图 01**：具有打开的重定向的登录页</span><span class="sxs-lookup"><span data-stu-id="96229-118">**Figure 01**: Login page with an open redirection</span></span>

<span data-ttu-id="96229-119">由于未对 ReturnUrl querystring 参数进行验证，攻击者可以将其修改为将任何 URL 地址注入到参数中，以执行开放重定向攻击。</span><span class="sxs-lookup"><span data-stu-id="96229-119">Since the ReturnUrl querystring parameter is not validated, an attacker can modify it to inject any URL address into the parameter to conduct an open redirection attack.</span></span> <span data-ttu-id="96229-120">为了演示这一点，我们可以将 ReturnUrl 参数修改为[http://bing.com](http://bing.com)，因此生成的登录 URL 将为/Account/LogOn？ReturnUrl =<http://www.bing.com/>。</span><span class="sxs-lookup"><span data-stu-id="96229-120">To demonstrate this, we can modify the ReturnUrl parameter to [http://bing.com](http://bing.com), so the resulting login URL will be /Account/LogOn?ReturnUrl=<http://www.bing.com/>.</span></span> <span data-ttu-id="96229-121">成功登录到站点后，会重定向到[http://bing.com](http://bing.com)。</span><span class="sxs-lookup"><span data-stu-id="96229-121">Upon successfully logging in to the site, we are redirected to [http://bing.com](http://bing.com).</span></span> <span data-ttu-id="96229-122">由于此重定向未经过验证，因此它可能会指向尝试欺骗用户的恶意网站。</span><span class="sxs-lookup"><span data-stu-id="96229-122">Since this redirection is not validated, it could instead point to a malicious site that attempts to trick the user.</span></span>

### <a name="a-more-complex-open-redirection-attack"></a><span data-ttu-id="96229-123">更复杂的打开重定向攻击</span><span class="sxs-lookup"><span data-stu-id="96229-123">A more complex Open Redirection Attack</span></span>

<span data-ttu-id="96229-124">由于攻击者知道我们尝试登录到特定网站，从而使我们容易遭受[网络钓鱼攻击](https://www.microsoft.com/protect/fraud/phishing/symptoms.aspx)，因此打开重定向攻击尤其危险。</span><span class="sxs-lookup"><span data-stu-id="96229-124">Open redirection attacks are especially dangerous because an attacker knows that we're trying to log into a specific website, which makes us vulnerable to a [phishing attack](https://www.microsoft.com/protect/fraud/phishing/symptoms.aspx).</span></span> <span data-ttu-id="96229-125">例如，攻击者可能会向网站用户发送恶意电子邮件以尝试捕获其密码。</span><span class="sxs-lookup"><span data-stu-id="96229-125">For example, an attacker could send malicious emails to website users in an attempt to capture their passwords.</span></span> <span data-ttu-id="96229-126">让我们看一下如何在 NerdDinner 站点上工作。</span><span class="sxs-lookup"><span data-stu-id="96229-126">Let's look at how this would work on the NerdDinner site.</span></span> <span data-ttu-id="96229-127">（请注意，实时 NerdDinner 站点已更新，以防止开放重定向攻击。）</span><span class="sxs-lookup"><span data-stu-id="96229-127">(Note that the live NerdDinner site has been updated to protect against open redirection attacks.)</span></span>

<span data-ttu-id="96229-128">首先，攻击者向我们发送 NerdDinner 上的登录页面的链接，该链接包含重定向到其伪造的页面：</span><span class="sxs-lookup"><span data-stu-id="96229-128">First, an attacker sends us a link to the login page on NerdDinner that includes a redirect to their forged page:</span></span>

[http://nerddinner.com/Account/LogOn?returnUrl=http://nerddiner.com/Account/LogOn](http://nerddinner.com/Account/LogOn?returnUrl=http://nerddiner.com/Account/LogOn)

<span data-ttu-id="96229-129">请注意，返回 URL 指向 nerddiner.com，这在单词晚餐中缺少 "n"。</span><span class="sxs-lookup"><span data-stu-id="96229-129">Note that the return URL points to nerddiner.com, which is missing an "n" from the word dinner.</span></span> <span data-ttu-id="96229-130">在此示例中，这是攻击者控制的域。</span><span class="sxs-lookup"><span data-stu-id="96229-130">In this example, this is a domain that the attacker controls.</span></span> <span data-ttu-id="96229-131">访问上述链接时，将转到合法的 NerdDinner.com 登录页。</span><span class="sxs-lookup"><span data-stu-id="96229-131">When we access the above link, we're taken to the legitimate NerdDinner.com login page.</span></span>

[![](preventing-open-redirection-attacks/_static/image4.png)](preventing-open-redirection-attacks/_static/image3.png)

<span data-ttu-id="96229-132">**图 02**：包含打开的重定向的 NerdDinner 登录页</span><span class="sxs-lookup"><span data-stu-id="96229-132">**Figure 02**: NerdDinner login page with an open redirection</span></span>

<span data-ttu-id="96229-133">当我们正确登录后，ASP.NET MVC AccountController 的登录操作会将我们重定向到 returnUrl querystring 参数中指定的 URL。</span><span class="sxs-lookup"><span data-stu-id="96229-133">When we correctly log in, the ASP.NET MVC AccountController's LogOn action redirects us to the URL specified in the returnUrl querystring parameter.</span></span> <span data-ttu-id="96229-134">在这种情况下，它是攻击者输入的 URL， [http://nerddiner.com/Account/LogOn](http://nerddiner.com/Account/LogOn)。</span><span class="sxs-lookup"><span data-stu-id="96229-134">In this case, it's the URL that the attacker has entered, which is [http://nerddiner.com/Account/LogOn](http://nerddiner.com/Account/LogOn).</span></span> <span data-ttu-id="96229-135">除非我们非常密切，否则我们很可能不会注意到这一点，特别是因为攻击者小心确保其伪造的页面看起来与合法登录页面完全相同。</span><span class="sxs-lookup"><span data-stu-id="96229-135">Unless we're extremely watchful, it's very likely we won't notice this, especially because the attacker has been careful to make sure that their forged page looks exactly like the legitimate login page.</span></span> <span data-ttu-id="96229-136">此登录页面包含一个错误消息，该错误消息要求再次登录。</span><span class="sxs-lookup"><span data-stu-id="96229-136">This login page includes an error message requesting that we login again.</span></span> <span data-ttu-id="96229-137">笨拙我们，我们必须键入错误的密码。</span><span class="sxs-lookup"><span data-stu-id="96229-137">Clumsy us, we must have mistyped our password.</span></span>

[![](preventing-open-redirection-attacks/_static/image6.png)](preventing-open-redirection-attacks/_static/image5.png)

<span data-ttu-id="96229-138">**图 03**：伪造的 NerdDinner 登录屏幕</span><span class="sxs-lookup"><span data-stu-id="96229-138">**Figure 03**: Forged NerdDinner Login screen</span></span>

<span data-ttu-id="96229-139">重新键入用户名和密码时，伪造的登录页面会保存信息，并将信息发送回合法的 NerdDinner.com 站点。</span><span class="sxs-lookup"><span data-stu-id="96229-139">When we retype our user name and password, the forged login page saves the information and sends us back to the legitimate NerdDinner.com site.</span></span> <span data-ttu-id="96229-140">此时，NerdDinner.com 站点已经过身份验证，因此伪造的登录页面可以直接重定向到该页面。</span><span class="sxs-lookup"><span data-stu-id="96229-140">At this point, the NerdDinner.com site has already authenticated us, so the forged login page can redirect directly to that page.</span></span> <span data-ttu-id="96229-141">最终的结果是攻击者提供了用户名和密码，并且我们不知道我们已向其提供了用户名和密码。</span><span class="sxs-lookup"><span data-stu-id="96229-141">The end result is that the attacker has our user name and password, and we are unaware that we've provided it to them.</span></span>

## <a name="looking-at-the-vulnerable-code-in-the-accountcontroller-logon-action"></a><span data-ttu-id="96229-142">查看 AccountController LogOn 操作中有漏洞的代码</span><span class="sxs-lookup"><span data-stu-id="96229-142">Looking at the vulnerable code in the AccountController LogOn Action</span></span>

<span data-ttu-id="96229-143">ASP.NET MVC 2 应用程序中登录操作的代码如下所示。</span><span class="sxs-lookup"><span data-stu-id="96229-143">The code for the LogOn action in an ASP.NET MVC 2 application is shown below.</span></span> <span data-ttu-id="96229-144">请注意，在成功登录后，控制器返回重定向到 returnUrl。</span><span class="sxs-lookup"><span data-stu-id="96229-144">Note that upon a successful login, the controller returns a redirect to the returnUrl.</span></span> <span data-ttu-id="96229-145">你可以看到，不会对 returnUrl 参数执行任何验证。</span><span class="sxs-lookup"><span data-stu-id="96229-145">You can see that no validation is being performed against the returnUrl parameter.</span></span>

<span data-ttu-id="96229-146">**列表1– ASP.NET 中的 MVC 2 登录操作 `AccountController.cs`**</span><span class="sxs-lookup"><span data-stu-id="96229-146">**Listing 1 – ASP.NET MVC 2 LogOn action in `AccountController.cs`**</span></span>

[!code-csharp[Main](preventing-open-redirection-attacks/samples/sample1.cs)]

<span data-ttu-id="96229-147">现在，让我们看看 ASP.NET MVC 3 登录操作的更改。</span><span class="sxs-lookup"><span data-stu-id="96229-147">Now let's look at the changes to the ASP.NET MVC 3 LogOn action.</span></span> <span data-ttu-id="96229-148">已通过在名为 `IsLocalUrl()`的 System.web helper 类中调用新方法，将此代码更改为验证 returnUrl 参数。</span><span class="sxs-lookup"><span data-stu-id="96229-148">This code has been changed to validate the returnUrl parameter by calling a new method in the System.Web.Mvc.Url helper class named `IsLocalUrl()`.</span></span>

<span data-ttu-id="96229-149">**列表2– ASP.NET 中的 MVC 3 登录操作 `AccountController.cs`**</span><span class="sxs-lookup"><span data-stu-id="96229-149">**Listing 2 – ASP.NET MVC 3 LogOn action in `AccountController.cs`**</span></span>

[!code-csharp[Main](preventing-open-redirection-attacks/samples/sample2.cs)]

<span data-ttu-id="96229-150">这已更改为通过调用 System.web helper 类中的新方法来验证 return URL 参数，`IsLocalUrl()`。</span><span class="sxs-lookup"><span data-stu-id="96229-150">This has been changed to validate the return URL parameter by calling a new method in the System.Web.Mvc.Url helper class, `IsLocalUrl()`.</span></span>

## <a name="protecting-your-aspnet-mvc-10-and-mvc-2-applications"></a><span data-ttu-id="96229-151">保护 ASP.NET MVC 1.0 和 MVC 2 应用程序</span><span class="sxs-lookup"><span data-stu-id="96229-151">Protecting Your ASP.NET MVC 1.0 and MVC 2 Applications</span></span>

<span data-ttu-id="96229-152">通过添加 IsLocalUrl （） helper 方法并更新登录操作来验证 returnUrl 参数，我们可以利用现有 ASP.NET MVC 1.0 和2应用程序中的 ASP.NET MVC 3 更改。</span><span class="sxs-lookup"><span data-stu-id="96229-152">We can take advantage of the ASP.NET MVC 3 changes in our existing ASP.NET MVC 1.0 and 2 applications by adding the IsLocalUrl() helper method and updating the LogOn action to validate the returnUrl parameter.</span></span>

<span data-ttu-id="96229-153">UrlHelper IsLocalUrl （）方法实际上只是调用了 System.web 中的一个方法，因为 ASP.NET 网页应用程序也使用此验证。</span><span class="sxs-lookup"><span data-stu-id="96229-153">The UrlHelper IsLocalUrl() method actually just calling into a method in System.Web.WebPages, as this validation is also used by ASP.NET Web Pages applications.</span></span>

<span data-ttu-id="96229-154">**列表 3-ASP.NET MVC 3 UrlHelper 中的 IsLocalUrl （）方法 `class`**</span><span class="sxs-lookup"><span data-stu-id="96229-154">**Listing 3 – The IsLocalUrl() method from the ASP.NET MVC 3 UrlHelper `class`**</span></span>

[!code-csharp[Main](preventing-open-redirection-attacks/samples/sample3.cs)]

<span data-ttu-id="96229-155">IsUrlLocalToHost 方法包含实际的验证逻辑，如列表4中所示。</span><span class="sxs-lookup"><span data-stu-id="96229-155">The IsUrlLocalToHost method contains the actual validation logic, as shown in Listing 4.</span></span>

<span data-ttu-id="96229-156">**从 System.web RequestExtensions 类中列出4– IsUrlLocalToHost （）方法**</span><span class="sxs-lookup"><span data-stu-id="96229-156">**Listing 4 – IsUrlLocalToHost() method from the System.Web.WebPages RequestExtensions class**</span></span>

[!code-csharp[Main](preventing-open-redirection-attacks/samples/sample4.cs)]

<span data-ttu-id="96229-157">在我们的 ASP.NET MVC 1.0 或2应用程序中，我们会将 IsLocalUrl （）方法添加到 AccountController，但建议在可能的情况下将其添加到单独的帮助器类。</span><span class="sxs-lookup"><span data-stu-id="96229-157">In our ASP.NET MVC 1.0 or 2 application, we'll add a IsLocalUrl() method to the AccountController, but you're encouraged to add it to a separate helper class if possible.</span></span> <span data-ttu-id="96229-158">我们将对 IsLocalUrl （）的 ASP.NET MVC 3 版本进行两处小的更改，使其在 AccountController 内部工作。</span><span class="sxs-lookup"><span data-stu-id="96229-158">We will make two small changes to the ASP.NET MVC 3 version of IsLocalUrl() so that it will work inside the AccountController.</span></span> <span data-ttu-id="96229-159">首先，我们会将其从公共方法更改为私有方法，因为控制器中的公共方法可以作为控制器操作访问。</span><span class="sxs-lookup"><span data-stu-id="96229-159">First, we'll change it from a public method to a private method, since public methods in controllers can be accessed as controller actions.</span></span> <span data-ttu-id="96229-160">其次，我们将修改对应用程序主机检查 URL 主机的调用。</span><span class="sxs-lookup"><span data-stu-id="96229-160">Second, we'll modify the call that checks the URL host against the application host.</span></span> <span data-ttu-id="96229-161">该调用会使用 UrlHelper 类中的本地 RequestContext 字段。</span><span class="sxs-lookup"><span data-stu-id="96229-161">That call makes use of a local RequestContext field in the UrlHelper class.</span></span> <span data-ttu-id="96229-162">而不使用此。RequestContext，我们将使用这种情况。请求。</span><span class="sxs-lookup"><span data-stu-id="96229-162">Instead of using this.RequestContext.HttpContext.Request.Url.Host, we will use this.Request.Url.Host.</span></span> <span data-ttu-id="96229-163">下面的代码演示了修改后的 IsLocalUrl （）方法，以用于 ASP.NET MVC 1.0 和2应用程序中的控制器类。</span><span class="sxs-lookup"><span data-stu-id="96229-163">The following code shows the modified IsLocalUrl() method for use with a controller class in ASP.NET MVC 1.0 and 2 applications.</span></span>

<span data-ttu-id="96229-164">**列出5– IsLocalUrl （）方法，该方法经过修改后可用于 MVC 控制器类**</span><span class="sxs-lookup"><span data-stu-id="96229-164">**Listing 5 – IsLocalUrl() method, which is modified for use with an MVC Controller class**</span></span>

[!code-csharp[Main](preventing-open-redirection-attacks/samples/sample5.cs)]

<span data-ttu-id="96229-165">现在，IsLocalUrl （）方法已准备就绪，可以从登录操作调用它来验证 returnUrl 参数，如以下代码所示。</span><span class="sxs-lookup"><span data-stu-id="96229-165">Now that the IsLocalUrl() method is in place, we can call it from our LogOn action to validate the returnUrl parameter, as shown in the following code.</span></span>

<span data-ttu-id="96229-166">**列出6–验证 returnUrl 参数的已更新登录方法**</span><span class="sxs-lookup"><span data-stu-id="96229-166">**Listing 6 – Updated LogOn method which validates the returnUrl parameter**</span></span>

[!code-csharp[Main](preventing-open-redirection-attacks/samples/sample6.cs)]

<span data-ttu-id="96229-167">现在，我们可以尝试使用外部返回 URL 登录，来测试打开的重定向攻击。</span><span class="sxs-lookup"><span data-stu-id="96229-167">Now we can test an open redirection attack by attempting to log in using an external return URL.</span></span> <span data-ttu-id="96229-168">我们使用/Account/LogOn？ReturnUrl = 再次<http://www.bing.com/>。</span><span class="sxs-lookup"><span data-stu-id="96229-168">Let's use /Account/LogOn?ReturnUrl=<http://www.bing.com/> again.</span></span>

[![](preventing-open-redirection-attacks/_static/image8.png)](preventing-open-redirection-attacks/_static/image7.png)

<span data-ttu-id="96229-169">**图 04**：测试更新的登录操作</span><span class="sxs-lookup"><span data-stu-id="96229-169">**Figure 04**: Testing the updated LogOn Action</span></span>

<span data-ttu-id="96229-170">成功登录后，将重定向到 Home/Index 控制器操作，而不是外部 URL。</span><span class="sxs-lookup"><span data-stu-id="96229-170">After successfully logging in, we are redirected to the Home/Index Controller action rather than the external URL.</span></span>

[![](preventing-open-redirection-attacks/_static/image10.png)](preventing-open-redirection-attacks/_static/image9.png)

<span data-ttu-id="96229-171">**图 05**：打开重定向攻击失效</span><span class="sxs-lookup"><span data-stu-id="96229-171">**Figure 05**: Open Redirection attack defeated</span></span>

## <a name="summary"></a><span data-ttu-id="96229-172">摘要</span><span class="sxs-lookup"><span data-stu-id="96229-172">Summary</span></span>

<span data-ttu-id="96229-173">当在应用程序的 URL 中将重定向 Url 作为参数传递时，可能会出现 "打开重定向攻击"。</span><span class="sxs-lookup"><span data-stu-id="96229-173">Open redirection attacks can occur when redirection URLs are passed as parameters in the URL for an application.</span></span> <span data-ttu-id="96229-174">ASP.NET MVC 3 模板包含用于防范开放重定向攻击的代码。</span><span class="sxs-lookup"><span data-stu-id="96229-174">The ASP.NET MVC 3 template includes code to protect against open redirection attacks.</span></span> <span data-ttu-id="96229-175">可以将此代码添加到 ASP.NET MVC 1.0 和2应用程序的一些修改。</span><span class="sxs-lookup"><span data-stu-id="96229-175">You can add this code with some modification to ASP.NET MVC 1.0 and 2 applications.</span></span> <span data-ttu-id="96229-176">若要防止在登录 ASP.NET 1.0 和2应用程序时出现的重定向攻击，请添加 IsLocalUrl （）方法并验证登录操作中的 returnUrl 参数。</span><span class="sxs-lookup"><span data-stu-id="96229-176">To protect against open redirection attacks when logging into ASP.NET 1.0 and 2 applications, add a IsLocalUrl() method and validate the returnUrl parameter in the LogOn action.</span></span>
