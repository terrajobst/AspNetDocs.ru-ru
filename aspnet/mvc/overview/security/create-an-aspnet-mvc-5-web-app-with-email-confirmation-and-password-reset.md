---
uid: mvc/overview/security/create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset
title: Создание безопасного веб-приложения ASP.NET MVC 5 с входом, подтверждением электронной почты и сбросом пароля (C#) | Документация Майкрософт
author: Rick-Anderson
description: В этом руководстве показано, как создать веб-приложение ASP.NET MVC 5 с подтверждением электронной почты и сбросом пароля с помощью системы членства ASP.NET Identity. Вы выca...
ms.author: riande
ms.date: 03/26/2015
ms.assetid: d4911cb3-1afb-4805-b860-10818c4b1280
msc.legacyurl: /mvc/overview/security/create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset
msc.type: authoredcontent
ms.openlocfilehash: 07f5b290b73f75000e6f29fe09e4dc25e144452f
ms.sourcegitcommit: 969e7db924ebad3cc0f0cb0d65d148e8b9221b9a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/06/2019
ms.locfileid: "74899697"
---
# <a name="create-a-secure-aspnet-mvc-5-web-app-with-log-in-email-confirmation-and-password-reset-c"></a><span data-ttu-id="f2ad6-104">Создание безопасного веб-приложения ASP.NET MVC 5 с входом, подтверждением электронной почты и сбросом пароля (C#)</span><span class="sxs-lookup"><span data-stu-id="f2ad6-104">Create a secure ASP.NET MVC 5 web app with log in, email confirmation and password reset (C#)</span></span>

<span data-ttu-id="f2ad6-105">по [Рик Андерсон (]((https://twitter.com/RickAndMSFT))</span><span class="sxs-lookup"><span data-stu-id="f2ad6-105">by [Rick Anderson]((https://twitter.com/RickAndMSFT))</span></span>

<span data-ttu-id="f2ad6-106">В этом руководстве показано, как создать веб-приложение ASP.NET MVC 5 с подтверждением электронной почты и сбросом пароля с помощью системы членства ASP.NET Identity.</span><span class="sxs-lookup"><span data-stu-id="f2ad6-106">This tutorial shows you how to build an ASP.NET MVC 5 web app with email confirmation and password reset using the ASP.NET Identity membership system.</span></span>

<span data-ttu-id="f2ad6-107">Обновленную версию этого учебника, в которой используется .NET Core, см. в разделе [Подтверждение учетной записи и восстановление пароля в ASP.NET Core [/АСПнет/коре/секурити/аусентикатион/аккконфирм).</span><span class="sxs-lookup"><span data-stu-id="f2ad6-107">For an updated version of this tutorial that uses .NET Core, see [Account confirmation and password recovery in ASP.NET Core[/aspnet/core/security/authentication/accconfirm).</span></span>

<a id="createMvc"></a>
## <a name="create-an-aspnet-mvc-app"></a><span data-ttu-id="f2ad6-108">Создание приложения ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="f2ad6-108">Create an ASP.NET MVC app</span></span>

<span data-ttu-id="f2ad6-109">Начните с установки и запуска [Visual Studio Express 2013 для Web](https://go.microsoft.com/fwlink/?LinkId=299058) или [Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566).</span><span class="sxs-lookup"><span data-stu-id="f2ad6-109">Start by installing and running [Visual Studio Express 2013 for Web](https://go.microsoft.com/fwlink/?LinkId=299058) or [Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566).</span></span> <span data-ttu-id="f2ad6-110">Установите [Visual Studio 2013 обновление 3](https://go.microsoft.com/fwlink/?LinkId=390465) или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="f2ad6-110">Install [Visual Studio 2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390465) or higher.</span></span>

> [!NOTE]
> <span data-ttu-id="f2ad6-111">Предупреждение. для работы с этим руководством необходимо установить [Visual Studio 2013 обновление 3](https://go.microsoft.com/fwlink/?LinkId=390465) или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="f2ad6-111">Warning: You must install [Visual Studio 2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390465) or higher to complete this tutorial.</span></span>

1. <span data-ttu-id="f2ad6-112">Создайте новый веб-проект ASP.NET и выберите шаблон MVC.</span><span class="sxs-lookup"><span data-stu-id="f2ad6-112">Create a new ASP.NET Web project and select the MVC template.</span></span> <span data-ttu-id="f2ad6-113">Веб-формы также поддерживают ASP.NET Identity, поэтому можно выполнять аналогичные действия в приложении Web Forms.</span><span class="sxs-lookup"><span data-stu-id="f2ad6-113">Web Forms also supports ASP.NET Identity, so you could follow similar steps in a web forms app.</span></span>  
    ![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image1.png)
2. <span data-ttu-id="f2ad6-114">Оставьте проверку подлинности по умолчанию как **учетные записи отдельных пользователей**.</span><span class="sxs-lookup"><span data-stu-id="f2ad6-114">Leave the default authentication as **Individual User Accounts**.</span></span> <span data-ttu-id="f2ad6-115">Если вы хотите разместить приложение в Azure, оставьте флажок установленным.</span><span class="sxs-lookup"><span data-stu-id="f2ad6-115">If you'd like to host the app in Azure, leave the check box checked.</span></span> <span data-ttu-id="f2ad6-116">Далее в этом руководстве мы будем выполнять развертывание в Azure.</span><span class="sxs-lookup"><span data-stu-id="f2ad6-116">Later in the tutorial we will deploy to Azure.</span></span> <span data-ttu-id="f2ad6-117">Вы можете [бесплатно открыть учетную запись Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="f2ad6-117">You can [open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span></span>
3. <span data-ttu-id="f2ad6-118">Настройте [проект для использования SSL](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="f2ad6-118">Set the [project to use SSL](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md).</span></span>
4. <span data-ttu-id="f2ad6-119">Запустите приложение, щелкните ссылку **Register** и зарегистрируйте пользователя.</span><span class="sxs-lookup"><span data-stu-id="f2ad6-119">Run the app, click the **Register** link and register a user.</span></span> <span data-ttu-id="f2ad6-120">На этом этапе единственной проверкой по электронной почте является атрибут [[EmailAddress]](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.emailaddressattribute(v=vs.110).aspx) .</span><span class="sxs-lookup"><span data-stu-id="f2ad6-120">At this point, the only validation on the email is with the [[EmailAddress]](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.emailaddressattribute(v=vs.110).aspx) attribute.</span></span>
5. <span data-ttu-id="f2ad6-121">В обозреватель сервера перейдите к **Коннектионс\дефаултконнектион\таблес\аспнетусерс данных**, щелкните правой кнопкой мыши и выберите **Открыть определение таблицы**.</span><span class="sxs-lookup"><span data-stu-id="f2ad6-121">In Server Explorer, navigate to **Data Connections\DefaultConnection\Tables\AspNetUsers**, right click and select **Open table definition**.</span></span>

    <span data-ttu-id="f2ad6-122">На следующем рисунке показана схема `AspNetUsers`:</span><span class="sxs-lookup"><span data-stu-id="f2ad6-122">The following image shows the `AspNetUsers` schema:</span></span>

    ![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image2.png)
6. <span data-ttu-id="f2ad6-123">Щелкните правой кнопкой мыши таблицу **AspNetUsers** и выберите команду " **отобразить данные таблицы**".</span><span class="sxs-lookup"><span data-stu-id="f2ad6-123">Right click on the **AspNetUsers** table and select **Show Table Data**.</span></span>  
    ![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image3.png)  
 <span data-ttu-id="f2ad6-124">На этом этапе электронная почта не подтверждена.</span><span class="sxs-lookup"><span data-stu-id="f2ad6-124">At this point the email has not been confirmed.</span></span>
7. <span data-ttu-id="f2ad6-125">Щелкните строку и выберите Удалить.</span><span class="sxs-lookup"><span data-stu-id="f2ad6-125">Click on the row and select delete.</span></span> <span data-ttu-id="f2ad6-126">Вы добавите это сообщение еще раз на следующем шаге и отправите сообщение электронной почты с подтверждением.</span><span class="sxs-lookup"><span data-stu-id="f2ad6-126">You'll add this email again in the next step, and send a confirmation email.</span></span>

## <a name="email-confirmation"></a><span data-ttu-id="f2ad6-127">Подтверждение по электронной почте</span><span class="sxs-lookup"><span data-stu-id="f2ad6-127">Email confirmation</span></span>

<span data-ttu-id="f2ad6-128">Рекомендуется подтвердить сообщение электронной почты о новой регистрации пользователя, чтобы убедиться, что они не олицетворяют кого-то другого (то есть они не зарегистрированы в электронной почте).</span><span class="sxs-lookup"><span data-stu-id="f2ad6-128">It's a best practice to confirm the email of a new user registration to verify they are not impersonating someone else (that is, they haven't registered with someone else's email).</span></span> <span data-ttu-id="f2ad6-129">Предположим, у вас есть дискуссионный форум, и вы хотели бы предотвратить регистрацию `"bob@example.com"` как `"joe@contoso.com"`.</span><span class="sxs-lookup"><span data-stu-id="f2ad6-129">Suppose you had a discussion forum, you would want to prevent `"bob@example.com"` from registering as `"joe@contoso.com"`.</span></span> <span data-ttu-id="f2ad6-130">Без подтверждения по электронной почте `"joe@contoso.com"` может получить от приложения нежелательную почту.</span><span class="sxs-lookup"><span data-stu-id="f2ad6-130">Without email confirmation, `"joe@contoso.com"` could get unwanted email from your app.</span></span> <span data-ttu-id="f2ad6-131">Предположим, что Боб случайно зарегистрировался как `"bib@example.com"` и не заметил его, он не сможет использовать восстановление пароля, так как у приложения нет нужной электронной почты.</span><span class="sxs-lookup"><span data-stu-id="f2ad6-131">Suppose Bob accidentally registered as `"bib@example.com"` and hadn't noticed it, he wouldn't be able to use password recover because the app doesn't have his correct email.</span></span> <span data-ttu-id="f2ad6-132">Подтверждение по электронной почте обеспечивает только ограниченную защиту от программы-роботы и не обеспечивает защиту от определенных отправителей, у них есть множество рабочих псевдонимов электронной почты, которые они могут использовать для регистрации.</span><span class="sxs-lookup"><span data-stu-id="f2ad6-132">Email confirmation provides only limited protection from bots and doesn't provide protection from determined spammers, they have many working email aliases they can use to register.</span></span>

<span data-ttu-id="f2ad6-133">Обычно требуется запретить новым пользователям отправлять данные на ваш веб-сайт, прежде чем они будут подтверждены электронной почтой, SMS-сообщением или другим механизмом.</span><span class="sxs-lookup"><span data-stu-id="f2ad6-133">You generally want to prevent new users from posting any data to your web site before they have been confirmed by email, a SMS text message or another mechanism.</span></span> <a id="build"></a><span data-ttu-id="f2ad6-134">В следующих разделах мы допустили подтверждение по электронной почте и изменим код, чтобы предотвратить вход новых зарегистрированных пользователей до подтверждения их электронной почты.</span><span class="sxs-lookup"><span data-stu-id="f2ad6-134">In the sections below, we will enable email confirmation and modify the code to prevent newly registered users from logging in until their email has been confirmed.</span></span>

<a id="SG"></a>
## <a name="hook-up-sendgrid"></a><span data-ttu-id="f2ad6-135">Подключение SendGrid</span><span class="sxs-lookup"><span data-stu-id="f2ad6-135">Hook up SendGrid</span></span>

<span data-ttu-id="f2ad6-136">Инструкции в этом разделе не являются текущими.</span><span class="sxs-lookup"><span data-stu-id="f2ad6-136">The instructions in this section are not current.</span></span> <span data-ttu-id="f2ad6-137">Обновленные инструкции см. в разделе [Configure SendGrid e-mail Provider](/aspnet/core/security/authentication/accconfirm#configure-email-provider) .</span><span class="sxs-lookup"><span data-stu-id="f2ad6-137">See [Configure SendGrid email provider](/aspnet/core/security/authentication/accconfirm#configure-email-provider) for updated instructions.</span></span>

<span data-ttu-id="f2ad6-138">Хотя в этом учебнике показано, как добавлять уведомления по электронной почте через [SendGrid](http://sendgrid.com/), можно отправлять электронную почту с помощью SMTP и других механизмов (см. [Дополнительные ресурсы](#addRes)).</span><span class="sxs-lookup"><span data-stu-id="f2ad6-138">Although this tutorial only shows how to add email notification through [SendGrid](http://sendgrid.com/), you can send email using SMTP and other mechanisms (see [additional resources](#addRes)).</span></span>

1. <span data-ttu-id="f2ad6-139">В консоли диспетчера пакетов введите следующую команду.</span><span class="sxs-lookup"><span data-stu-id="f2ad6-139">In the Package Manager Console, enter the following command:</span></span> 

    [!code-console[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample1.cmd)]
2. <span data-ttu-id="f2ad6-140">Перейдите на [страницу регистрации Azure SendGrid](https://go.microsoft.com/fwlink/?linkid=271033&clcid=0x409) и зарегистрируйтесь для бесплатной учетной записи SendGrid.</span><span class="sxs-lookup"><span data-stu-id="f2ad6-140">Go to the [Azure SendGrid sign up page](https://go.microsoft.com/fwlink/?linkid=271033&clcid=0x409) and register for a free SendGrid account.</span></span> <span data-ttu-id="f2ad6-141">Настройте SendGrid, добавив код, аналогичный приведенному ниже, в *App_Start/идентитиконфиг.КС*:</span><span class="sxs-lookup"><span data-stu-id="f2ad6-141">Configure SendGrid by adding code similar to the following in *App_Start/IdentityConfig.cs*:</span></span>

    [!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample2.cs?highlight=3,5)]

<span data-ttu-id="f2ad6-142">Необходимо добавить следующие ссылки:</span><span class="sxs-lookup"><span data-stu-id="f2ad6-142">You'll need to add the following includes:</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample3.cs)]

<span data-ttu-id="f2ad6-143">Чтобы не усложнять этот пример, мы будем хранить параметры приложения в файле *Web. config* :</span><span class="sxs-lookup"><span data-stu-id="f2ad6-143">To keep this sample simple, we'll store the app settings in the *web.config* file:</span></span>

[!code-xml[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample4.xml)]

> [!WARNING]
> <span data-ttu-id="f2ad6-144">Безопасность — никогда не храните конфиденциальные данные в исходном коде.</span><span class="sxs-lookup"><span data-stu-id="f2ad6-144">Security - Never store sensitive data in your source code.</span></span> <span data-ttu-id="f2ad6-145">Учетная запись и учетные данные хранятся в appSetting.</span><span class="sxs-lookup"><span data-stu-id="f2ad6-145">The account and credentials are stored in the appSetting.</span></span> <span data-ttu-id="f2ad6-146">В Azure эти значения можно безопасно сохранить на вкладке **[Настройка](https://blogs.msdn.com/b/webdev/archive/2014/06/04/queuebackgroundworkitem-to-reliably-schedule-and-run-long-background-process-in-asp-net.aspx)** в портал Azure.</span><span class="sxs-lookup"><span data-stu-id="f2ad6-146">On Azure, you can securely store these values on the **[Configure](https://blogs.msdn.com/b/webdev/archive/2014/06/04/queuebackgroundworkitem-to-reliably-schedule-and-run-long-background-process-in-asp-net.aspx)** tab in the Azure portal.</span></span> <span data-ttu-id="f2ad6-147">См. рекомендации [по развертыванию паролей и других конфиденциальных данных в ASP.NET и Azure](../../../identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure.md).</span><span class="sxs-lookup"><span data-stu-id="f2ad6-147">See [Best practices for deploying passwords and other sensitive data to ASP.NET and Azure](../../../identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure.md).</span></span>

### <a name="enable-email-confirmation-in-the-account-controller"></a><span data-ttu-id="f2ad6-148">Включить подтверждение электронной почты в контроллере учетной записи</span><span class="sxs-lookup"><span data-stu-id="f2ad6-148">Enable email confirmation in the Account controller</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample5.cs?highlight=16-21)]

<span data-ttu-id="f2ad6-149">Убедитесь, что в файле *виевс\аккаунт\конфирмемаил.кштмл* правильный синтаксис Razor.</span><span class="sxs-lookup"><span data-stu-id="f2ad6-149">Verify the *Views\Account\ConfirmEmail.cshtml* file has correct razor syntax.</span></span> <span data-ttu-id="f2ad6-150">(Возможно, отсутствует символ @ в первой строке.</span><span class="sxs-lookup"><span data-stu-id="f2ad6-150">( The @ character in the first line might be missing.</span></span> <span data-ttu-id="f2ad6-151">)</span><span class="sxs-lookup"><span data-stu-id="f2ad6-151">)</span></span>

[!code-cshtml[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample6.cshtml?highlight=1)]

<span data-ttu-id="f2ad6-152">Запустите приложение и щелкните ссылку Register (регистрация).</span><span class="sxs-lookup"><span data-stu-id="f2ad6-152">Run the app and click the Register link.</span></span> <span data-ttu-id="f2ad6-153">После отправки регистрационной формы вы войдете в систему.</span><span class="sxs-lookup"><span data-stu-id="f2ad6-153">Once you submit the registration form, you are logged in.</span></span>

![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image4.png)

<span data-ttu-id="f2ad6-154">Проверьте учетную запись электронной почты и щелкните ссылку, чтобы подтвердить свою электронную почту.</span><span class="sxs-lookup"><span data-stu-id="f2ad6-154">Check your email account and click on the link to confirm your email.</span></span>

<a id="require"></a>
## <a name="require-email-confirmation-before-log-in"></a><span data-ttu-id="f2ad6-155">Требовать подтверждение по электронной почте перед входом</span><span class="sxs-lookup"><span data-stu-id="f2ad6-155">Require email confirmation before log in</span></span>

<span data-ttu-id="f2ad6-156">В настоящее время, когда пользователь завершает регистрационную форму, он входит в систему.</span><span class="sxs-lookup"><span data-stu-id="f2ad6-156">Currently once a user completes the registration form, they are logged in.</span></span> <span data-ttu-id="f2ad6-157">Обычно необходимо подтвердить свою электронную почту перед записью в журнал.</span><span class="sxs-lookup"><span data-stu-id="f2ad6-157">You generally want to confirm their email before logging them in.</span></span> <span data-ttu-id="f2ad6-158">В разделе ниже мы изменим код, чтобы требовать от новых пользователей получения подтвержденного сообщения электронной почты до входа в систему (с проверкой подлинности).</span><span class="sxs-lookup"><span data-stu-id="f2ad6-158">In the section below, we will modify the code to require new users to have a confirmed email before they are logged in (authenticated).</span></span> <span data-ttu-id="f2ad6-159">Обновите метод `HttpPost Register` со следующими выделенными изменениями:</span><span class="sxs-lookup"><span data-stu-id="f2ad6-159">Update the `HttpPost Register` method with the following highlighted changes:</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample7.cs?highlight=14-15,23-30)]

<span data-ttu-id="f2ad6-160">Закомментируя метод `SignInAsync`, пользователь не будет выполнять вход с помощью регистрации.</span><span class="sxs-lookup"><span data-stu-id="f2ad6-160">By commenting out the `SignInAsync` method, the user will not be signed in by the registration.</span></span> <span data-ttu-id="f2ad6-161">Строку `TempData["ViewBagLink"] = callbackUrl;` можно использовать для [отладки приложения](#dbg) и проверки регистрации без отправки электронной почты.</span><span class="sxs-lookup"><span data-stu-id="f2ad6-161">The `TempData["ViewBagLink"] = callbackUrl;` line can be used to [debug the app](#dbg) and test registration without sending email.</span></span> <span data-ttu-id="f2ad6-162">`ViewBag.Message` используется для вывода инструкций Confirm.</span><span class="sxs-lookup"><span data-stu-id="f2ad6-162">`ViewBag.Message` is used to display the confirm instructions.</span></span> <span data-ttu-id="f2ad6-163">[Пример загрузки](https://code.msdn.microsoft.com/MVC-5-with-2FA-email-8f26d952) содержит код для проверки сообщения электронной почты без настройки электронной почты, а также может использоваться для отладки приложения.</span><span class="sxs-lookup"><span data-stu-id="f2ad6-163">The [download sample](https://code.msdn.microsoft.com/MVC-5-with-2FA-email-8f26d952) contains code to test email confirmation without setting up email, and can also be used to debug the application.</span></span>

<span data-ttu-id="f2ad6-164">Создайте файл `Views\Shared\Info.cshtml` и добавьте следующую разметку Razor:</span><span class="sxs-lookup"><span data-stu-id="f2ad6-164">Create a `Views\Shared\Info.cshtml` file and add the following razor markup:</span></span>

[!code-cshtml[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample8.cshtml)]

<span data-ttu-id="f2ad6-165">Добавьте [атрибут авторизовать](https://msdn.microsoft.com/library/system.web.mvc.authorizeattribute(v=vs.118).aspx) в метод действия `Contact` контроллера Home.</span><span class="sxs-lookup"><span data-stu-id="f2ad6-165">Add the [Authorize attribute](https://msdn.microsoft.com/library/system.web.mvc.authorizeattribute(v=vs.118).aspx) to the `Contact` action method of the Home controller.</span></span> <span data-ttu-id="f2ad6-166">Можно щелкнуть ссылку **контакт** , чтобы проверить, что анонимные пользователи не имеют доступа и пользователи, прошедшие проверку подлинности, имеют доступ.</span><span class="sxs-lookup"><span data-stu-id="f2ad6-166">You can click on the **Contact** link to verify anonymous users don't have access and authenticated users do have access.</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample9.cs?highlight=1)]

<span data-ttu-id="f2ad6-167">Необходимо также обновить метод действия `HttpPost Login`.</span><span class="sxs-lookup"><span data-stu-id="f2ad6-167">You must also update the `HttpPost Login` action method:</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample10.cs?highlight=13-22)]

<span data-ttu-id="f2ad6-168">Обновите представление *виевс\шаред\еррор.кштмл* , чтобы отобразить сообщение об ошибке:</span><span class="sxs-lookup"><span data-stu-id="f2ad6-168">Update the *Views\Shared\Error.cshtml* view to display the error message:</span></span>

[!code-cshtml[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample11.cshtml?highlight=8-17)]

<span data-ttu-id="f2ad6-169">Удалите все учетные записи в таблице **AspNetUsers** , содержащие псевдоним электронной почты, с которым вы хотите протестировать.</span><span class="sxs-lookup"><span data-stu-id="f2ad6-169">Delete any accounts in the **AspNetUsers** table that contain the email alias you wish to test with.</span></span> <span data-ttu-id="f2ad6-170">Запустите приложение и убедитесь, что вы не можете войти в систему, пока не подтвердите свой адрес электронной почты.</span><span class="sxs-lookup"><span data-stu-id="f2ad6-170">Run the app and verify you can't log in until you have confirmed your email address.</span></span> <span data-ttu-id="f2ad6-171">После подтверждения адреса электронной почты щелкните ссылку **контакт** .</span><span class="sxs-lookup"><span data-stu-id="f2ad6-171">Once you confirm your email address, click the **Contact** link.</span></span>

<a id="reset"></a>
## <a name="password-recoveryreset"></a><span data-ttu-id="f2ad6-172">Восстановление или сброс пароля</span><span class="sxs-lookup"><span data-stu-id="f2ad6-172">Password recovery/reset</span></span>

<span data-ttu-id="f2ad6-173">Удалите символы комментария из метода действия `HttpPost ForgotPassword` в контроллере учетной записи:</span><span class="sxs-lookup"><span data-stu-id="f2ad6-173">Remove the comment characters from the `HttpPost ForgotPassword` action method in the account controller:</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample12.cs?highlight=17-20)]

<span data-ttu-id="f2ad6-174">Удалите символы комментария из `ForgotPassword` [ActionLink](https://msdn.microsoft.com/library/system.web.mvc.html.linkextensions.actionlink(v=vs.118).aspx) в файле представления Razor *виевс\аккаунт\логин.кштмл* :</span><span class="sxs-lookup"><span data-stu-id="f2ad6-174">Remove the comment characters from the `ForgotPassword` [ActionLink](https://msdn.microsoft.com/library/system.web.mvc.html.linkextensions.actionlink(v=vs.118).aspx) in the *Views\Account\Login.cshtml* razor view file:</span></span>

[!code-cshtml[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample13.cshtml?highlight=47-50)]

<span data-ttu-id="f2ad6-175">На странице входа теперь отображается ссылка для сброса пароля.</span><span class="sxs-lookup"><span data-stu-id="f2ad6-175">The Log in page will now show a link to reset the password.</span></span>

<a id="rsend"></a>
## <a name="resend-email-confirmation-link"></a><span data-ttu-id="f2ad6-176">Ссылка для подтверждения повторной отправки по электронной почте</span><span class="sxs-lookup"><span data-stu-id="f2ad6-176">Resend email confirmation link</span></span>

<span data-ttu-id="f2ad6-177">После того как пользователь создает новую локальную учетную запись, он отправляет по электронной почте ссылку на подтверждение, которую необходимо использовать, прежде чем они смогут войти в систему.</span><span class="sxs-lookup"><span data-stu-id="f2ad6-177">Once a user creates a new local account, they are emailed a confirmation link they are required to use before they can log on.</span></span> <span data-ttu-id="f2ad6-178">Если пользователь случайно удалил сообщение электронной почты с подтверждением или сообщение не будет доставлено, ему потребуется снова отправить ссылку на подтверждение.</span><span class="sxs-lookup"><span data-stu-id="f2ad6-178">If the user accidentally deletes the confirmation email, or the email never arrives, they will need the confirmation link sent again.</span></span> <span data-ttu-id="f2ad6-179">В следующем примере кода показано, как это сделать.</span><span class="sxs-lookup"><span data-stu-id="f2ad6-179">The following code changes show how to enable this.</span></span>

<span data-ttu-id="f2ad6-180">Добавьте следующий вспомогательный метод в нижнюю часть файла *контроллерс\аккаунтконтроллер.КС* :</span><span class="sxs-lookup"><span data-stu-id="f2ad6-180">Add the following helper method to the bottom of the *Controllers\AccountController.cs* file:</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample14.cs)]

<span data-ttu-id="f2ad6-181">Обновите метод Register для использования нового модуля поддержки:</span><span class="sxs-lookup"><span data-stu-id="f2ad6-181">Update the Register method to use the new helper:</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample15.cs?highlight=17)]

<span data-ttu-id="f2ad6-182">Обновите метод входа, чтобы повторно отправить пароль, если учетная запись пользователя не подтверждена:</span><span class="sxs-lookup"><span data-stu-id="f2ad6-182">Update the Login method to resend the password if the user account has not been confirmed:</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample16.cs?highlight=20)]

<a id="combine"></a>
## <a name="combine-social-and-local-login-accounts"></a><span data-ttu-id="f2ad6-183">Объединение социальных и местных учетных записей входа</span><span class="sxs-lookup"><span data-stu-id="f2ad6-183">Combine social and local login accounts</span></span>

<span data-ttu-id="f2ad6-184">Вы можете объединить локальные и социальные учетные записи, щелкнув ссылку на электронную почту.</span><span class="sxs-lookup"><span data-stu-id="f2ad6-184">You can combine local and social accounts by clicking on your email link.</span></span> <span data-ttu-id="f2ad6-185">В следующей последовательности **RickAndMSFT@gmail.com** сначала создается как локальное имя входа, но вы можете сначала создать учетную запись в качестве входных социальных сетей, а затем добавить локальное имя входа.</span><span class="sxs-lookup"><span data-stu-id="f2ad6-185">In the following sequence **RickAndMSFT@gmail.com** is first created as a local login, but you can create the account as a social log in first, then add a local login.</span></span>

![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image5.png)

<span data-ttu-id="f2ad6-186">Щелкните ссылку **Управление** .</span><span class="sxs-lookup"><span data-stu-id="f2ad6-186">Click on the **Manage** link.</span></span> <span data-ttu-id="f2ad6-187">Обратите внимание на **внешние имена входа: 0** , связанные с этой учетной записью.</span><span class="sxs-lookup"><span data-stu-id="f2ad6-187">Note the **External Logins: 0** associated with this account.</span></span>

![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image6.png)

<span data-ttu-id="f2ad6-188">Щелкните ссылку на другой журнал службы и примите запросы приложения.</span><span class="sxs-lookup"><span data-stu-id="f2ad6-188">Click the link to another log in service and accept the app requests.</span></span> <span data-ttu-id="f2ad6-189">Две учетные записи объединены, вы сможете войти в систему с любой учетной записью.</span><span class="sxs-lookup"><span data-stu-id="f2ad6-189">The two accounts have been combined, you will be able to log on with either account.</span></span> <span data-ttu-id="f2ad6-190">Может потребоваться, чтобы пользователи могли добавлять локальные учетные записи в случае, если служба проверки подлинности в социальных сетях не работает, или более вероятно, что они потеряют доступ к учетной записи социальных сетей.</span><span class="sxs-lookup"><span data-stu-id="f2ad6-190">You might want your users to add local accounts in case their social log in authentication service is down, or more likely they have lost access to their social account.</span></span>

<span data-ttu-id="f2ad6-191">На следующем рисунке Tom является входом в социальной сети (который можно увидеть из **внешних имен входа: 1** на странице).</span><span class="sxs-lookup"><span data-stu-id="f2ad6-191">In the following image, Tom is a social log in (which you can see from the **External Logins: 1** shown on the page).</span></span>

![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image7.png)

<span data-ttu-id="f2ad6-192">Если щелкнуть " **выбрать пароль** ", вы можете добавить локальный вход в систему, связанный с той же учетной записью.</span><span class="sxs-lookup"><span data-stu-id="f2ad6-192">Clicking on **Pick a password** allows you to add a local log on associated with the same account.</span></span>

![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image8.png)

## <a name="email-confirmation-in-more-depth"></a><span data-ttu-id="f2ad6-193">Более подробное подтверждение по электронной почте</span><span class="sxs-lookup"><span data-stu-id="f2ad6-193">Email confirmation in more depth</span></span>

<span data-ttu-id="f2ad6-194">В этом разделе содержатся дополнительные сведения о [подтверждении учетной записи учебника и восстановлении пароля с ASP.NET Identity](../../../identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md) .</span><span class="sxs-lookup"><span data-stu-id="f2ad6-194">My tutorial [Account Confirmation and Password Recovery with ASP.NET Identity](../../../identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md) goes into this topic with more details.</span></span>

<a id="dbg"></a>
## <a name="debugging-the-app"></a><span data-ttu-id="f2ad6-195">Отладка приложения</span><span class="sxs-lookup"><span data-stu-id="f2ad6-195">Debugging the app</span></span>

<span data-ttu-id="f2ad6-196">Если вы не получаете электронное письмо со ссылкой:</span><span class="sxs-lookup"><span data-stu-id="f2ad6-196">If you don't get an email containing the link:</span></span>

- <span data-ttu-id="f2ad6-197">Проверьте папку нежелательной почты или спама.</span><span class="sxs-lookup"><span data-stu-id="f2ad6-197">Check your junk or spam folder.</span></span>
- <span data-ttu-id="f2ad6-198">Войдите в учетную запись SendGrid и щелкните [ссылку действие электронной почты](https://sendgrid.com/logs/index).</span><span class="sxs-lookup"><span data-stu-id="f2ad6-198">Log into your SendGrid account and click on the [Email Activity link](https://sendgrid.com/logs/index).</span></span>

<span data-ttu-id="f2ad6-199">Чтобы проверить ссылку проверки без сообщения электронной почты, скачайте [готовый пример](https://code.msdn.microsoft.com/MVC-5-with-2FA-email-8f26d952).</span><span class="sxs-lookup"><span data-stu-id="f2ad6-199">To test the verification link without email, download the [completed sample](https://code.msdn.microsoft.com/MVC-5-with-2FA-email-8f26d952).</span></span> <span data-ttu-id="f2ad6-200">На странице будут отображаться ссылки на подтверждение и коды подтверждения.</span><span class="sxs-lookup"><span data-stu-id="f2ad6-200">The confirmation link and confirmation codes will be displayed on the page.</span></span>

<a id="addRes"></a>
## <a name="additional-resources"></a><span data-ttu-id="f2ad6-201">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="f2ad6-201">Additional Resources</span></span>

- [<span data-ttu-id="f2ad6-202">Ссылки на ASP.NET Identity Рекомендуемые ресурсы</span><span class="sxs-lookup"><span data-stu-id="f2ad6-202">Links to ASP.NET Identity Recommended Resources</span></span>](../../../identity/overview/getting-started/aspnet-identity-recommended-resources.md)
- <span data-ttu-id="f2ad6-203">[Подтверждение учетной записи и восстановление пароля с ASP.NET Identity](../../../identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md) Дополнительные сведения о восстановлении пароля и подтверждении учетной записи.</span><span class="sxs-lookup"><span data-stu-id="f2ad6-203">[Account Confirmation and Password Recovery with ASP.NET Identity](../../../identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md) Goes into more detail on password recovery and account confirmation.</span></span>
- <span data-ttu-id="f2ad6-204">[Приложение MVC 5 с входом Facebook, Twitter, LinkedIn и Google OAuth2](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md) В этом руководстве показано, как написать приложение ASP.NET MVC 5 с проверкой подлинности Facebook и Google OAuth 2.</span><span class="sxs-lookup"><span data-stu-id="f2ad6-204">[MVC 5 App with Facebook, Twitter, LinkedIn and Google OAuth2 Sign-on](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md) This tutorial shows you how to write an ASP.NET MVC 5 app with Facebook and Google OAuth 2 authorization.</span></span> <span data-ttu-id="f2ad6-205">В нем также показано, как добавить дополнительные данные в базу данных удостоверений.</span><span class="sxs-lookup"><span data-stu-id="f2ad6-205">It also shows how to add additional data to the Identity database.</span></span>
- <span data-ttu-id="f2ad6-206">[Развертывание безопасного приложения MVC ASP.NET с членством, OAuth и базой данных SQL в Azure](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data).</span><span class="sxs-lookup"><span data-stu-id="f2ad6-206">[Deploy a Secure ASP.NET MVC app with Membership, OAuth, and SQL Database to Azure](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data).</span></span> <span data-ttu-id="f2ad6-207">В этом руководстве описывается добавление развертывания Azure, защита приложения с помощью ролей, использование API членства для добавления пользователей и ролей, а также дополнительные функции безопасности.</span><span class="sxs-lookup"><span data-stu-id="f2ad6-207">This tutorial adds Azure deployment, how to secure your app with roles, how to use the membership API to add users and roles, and additional security features.</span></span>
- [<span data-ttu-id="f2ad6-208">Создание приложения Google для OAuth 2 и подключение приложения к проекту</span><span class="sxs-lookup"><span data-stu-id="f2ad6-208">Creating a Google app for OAuth 2 and connecting the app to the project</span></span>](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md#goog)
- [<span data-ttu-id="f2ad6-209">Создание приложения в Facebook и подключение приложения к проекту</span><span class="sxs-lookup"><span data-stu-id="f2ad6-209">Creating the app in Facebook and connecting the app to the project</span></span>](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md#fb)
- [<span data-ttu-id="f2ad6-210">Настройка SSL в проекте</span><span class="sxs-lookup"><span data-stu-id="f2ad6-210">Setting up SSL in the Project</span></span>](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md#ssl)
