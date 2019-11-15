---
uid: identity/overview/features-api/two-factor-authentication-using-sms-and-email-with-aspnet-identity
title: Двухфакторная проверка подлинности с помощью SMS и электронной почты с ASP.NET Identity-ASP.NET 4. x
author: HaoK
description: В этом руководстве показано, как настроить двухфакторную проверку подлинности (2FA) с помощью SMS и электронной почты. Эта статья была написана на Рик Андерсон ((@RickAndMSFT), PR...
ms.author: riande
ms.date: 09/15/2015
ms.assetid: 053e23c4-13c9-40fa-87cb-3e9b0823b31e
ms.custom: seoapril2019
msc.legacyurl: /identity/overview/features-api/two-factor-authentication-using-sms-and-email-with-aspnet-identity
msc.type: authoredcontent
ms.openlocfilehash: 5f5218ca6c65ed3a2cd39d4e100349efa35d14cd
ms.sourcegitcommit: 6f0e10e4ca61a1e5534b09c655fd35cdc6886c8a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/15/2019
ms.locfileid: "74115098"
---
# <a name="two-factorauthentication-using-sms-and-email-with-aspnet-identity"></a><span data-ttu-id="309f6-104">Двухфакторная проверка подлинности с помощью SMS и электронной почты с ASP.NET Identity</span><span class="sxs-lookup"><span data-stu-id="309f6-104">Two-factor authentication using SMS and email with ASP.NET Identity</span></span>

<span data-ttu-id="309f6-105">[Хао кунг](https://github.com/HaoK), [получения запись блога](https://github.com/rustd), [Рик Андерсон (]((https://twitter.com/RickAndMSFT)), [Сухас Джоши](https://github.com/suhasj)</span><span class="sxs-lookup"><span data-stu-id="309f6-105">by [Hao Kung](https://github.com/HaoK), [Pranav Rastogi](https://github.com/rustd), [Rick Anderson]((https://twitter.com/RickAndMSFT)), [Suhas Joshi](https://github.com/suhasj)</span></span>

> <span data-ttu-id="309f6-106">В этом руководстве показано, как настроить двухфакторную проверку подлинности (2FA) с помощью SMS и электронной почты.</span><span class="sxs-lookup"><span data-stu-id="309f6-106">This tutorial will show you how to set up Two-factor authentication (2FA) using SMS and email.</span></span>
> 
> <span data-ttu-id="309f6-107">Эта статья была написана на Рик Андерсон (([@RickAndMSFT](https://twitter.com/#!/RickAndMSFT)), получения запись блога ([@rustd](https://twitter.com/rustd)), Хао Кунг и Сухас Джоши.</span><span class="sxs-lookup"><span data-stu-id="309f6-107">This article was written by Rick Anderson ([@RickAndMSFT](https://twitter.com/#!/RickAndMSFT)), Pranav Rastogi ([@rustd](https://twitter.com/rustd)), Hao Kung, and Suhas Joshi.</span></span> <span data-ttu-id="309f6-108">Пример NuGet написан в основном с помощью Хао кунг.</span><span class="sxs-lookup"><span data-stu-id="309f6-108">The NuGet sample was written primarily by Hao Kung.</span></span>

<span data-ttu-id="309f6-109">В этом разделе рассматриваются следующие вопросы:</span><span class="sxs-lookup"><span data-stu-id="309f6-109">This topic covers the following:</span></span>

- [<span data-ttu-id="309f6-110">Создание примера удостоверения</span><span class="sxs-lookup"><span data-stu-id="309f6-110">Building the Identity sample</span></span>](#build)
- [<span data-ttu-id="309f6-111">Настройка SMS для двухфакторной проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="309f6-111">Set up SMS for Two-factor authentication</span></span>](#SMS)
- [<span data-ttu-id="309f6-112">Включить двухфакторную проверку подлинности</span><span class="sxs-lookup"><span data-stu-id="309f6-112">Enable Two-factor authentication</span></span>](#enable2)
- [<span data-ttu-id="309f6-113">Регистрация поставщика двухфакторной проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="309f6-113">How to register a Two-factor authentication provider</span></span>](#reg)
- [<span data-ttu-id="309f6-114">Объединение социальных и местных учетных записей входа</span><span class="sxs-lookup"><span data-stu-id="309f6-114">Combine social and local login accounts</span></span>](#combine)
- [<span data-ttu-id="309f6-115">Блокировка учетной записи от атак методом подбора</span><span class="sxs-lookup"><span data-stu-id="309f6-115">Account lockout from brute force attacks</span></span>](#lock)

<a id="build"></a>

## <a name="building-the-identity-sample"></a><span data-ttu-id="309f6-116">Создание примера удостоверения</span><span class="sxs-lookup"><span data-stu-id="309f6-116">Building the Identity sample</span></span>

<span data-ttu-id="309f6-117">В этом разделе вы будете использовать NuGet для загрузки примера, с которым мы будем работать.</span><span class="sxs-lookup"><span data-stu-id="309f6-117">In this section, you'll use NuGet to download a sample we will work with.</span></span> <span data-ttu-id="309f6-118">Начните с установки и запуска [Visual Studio Express 2013 для Web](https://go.microsoft.com/fwlink/?LinkId=299058) или [Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566).</span><span class="sxs-lookup"><span data-stu-id="309f6-118">Start by installing and running [Visual Studio Express 2013 for Web](https://go.microsoft.com/fwlink/?LinkId=299058) or [Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566).</span></span> <span data-ttu-id="309f6-119">Установите Visual Studio [2013 с обновлением 2](https://go.microsoft.com/fwlink/?LinkId=390521) или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="309f6-119">Install Visual Studio [2013 Update 2](https://go.microsoft.com/fwlink/?LinkId=390521) or higher.</span></span>

> [!NOTE]
> <span data-ttu-id="309f6-120">Предупреждение. для работы с этим руководством необходимо установить Visual Studio [2013 с обновлением 2](https://go.microsoft.com/fwlink/?LinkId=390521) .</span><span class="sxs-lookup"><span data-stu-id="309f6-120">Warning: You must install Visual Studio [2013 Update 2](https://go.microsoft.com/fwlink/?LinkId=390521) to complete this tutorial.</span></span>

1. <span data-ttu-id="309f6-121">Создайте новый ***пустой*** веб-проект ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="309f6-121">Create a new ***empty*** ASP.NET Web project.</span></span>
2. <span data-ttu-id="309f6-122">В консоли диспетчера пакетов введите следующие команды:</span><span class="sxs-lookup"><span data-stu-id="309f6-122">In the Package Manager Console, enter the following the following commands:</span></span>  
  
    `Install-Package SendGrid`  
    `Install-Package -Prerelease Microsoft.AspNet.Identity.Samples`  
  
   <span data-ttu-id="309f6-123">В этом руководстве мы будем использовать [SendGrid](http://sendgrid.com/) для отправки электронной почты и [Twilio](https://www.twilio.com/) или [аспсмс](https://www.aspsms.com/asp.net/identity/testcredits/) для SMS.</span><span class="sxs-lookup"><span data-stu-id="309f6-123">In this tutorial, we'll use [SendGrid](http://sendgrid.com/) to send email and [Twilio](https://www.twilio.com/) or [ASPSMS](https://www.aspsms.com/asp.net/identity/testcredits/) for sms texting.</span></span> <span data-ttu-id="309f6-124">Пакет `Identity.Samples` устанавливает код, с которым будет работать.</span><span class="sxs-lookup"><span data-stu-id="309f6-124">The `Identity.Samples` package installs the code we will be working with.</span></span>
3. <span data-ttu-id="309f6-125">Настройте [проект для использования SSL](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="309f6-125">Set the [project to use SSL](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md).</span></span>
4. <span data-ttu-id="309f6-126">*Необязательно*. Следуйте инструкциям в [руководстве по подтверждению электронной почты](account-confirmation-and-password-recovery-with-aspnet-identity.md) , чтобы подключить SendGrid, а затем запустить приложение и зарегистрировать учетную запись электронной почты.</span><span class="sxs-lookup"><span data-stu-id="309f6-126">*Optional*: Follow the instructions in my [Email confirmation tutorial](account-confirmation-and-password-recovery-with-aspnet-identity.md) to hook up SendGrid and then run the app and register an email account.</span></span>
5. <span data-ttu-id="309f6-127">*Необязательно:* Удалите демонстрационный код подтверждения ссылки на электронную почту из примера (код `ViewBag.Link` в контроллере учетной записи.</span><span class="sxs-lookup"><span data-stu-id="309f6-127">*Optional:* Remove the demo email link confirmation code from the sample (The `ViewBag.Link` code in the account controller.</span></span> <span data-ttu-id="309f6-128">См. методы действий `DisplayEmail` и `ForgotPasswordConfirmation` и представления Razor).</span><span class="sxs-lookup"><span data-stu-id="309f6-128">See the `DisplayEmail` and `ForgotPasswordConfirmation` action methods and razor views ).</span></span>
6. <span data-ttu-id="309f6-129">*Необязательно:* Удалите код `ViewBag.Status` из контроллеров управления и учетных записей и из представлений Razor *виевс\аккаунт\верификоде.кштмл* и *виевс\манаже\верифифоненумбер.кштмл* .</span><span class="sxs-lookup"><span data-stu-id="309f6-129">*Optional:* Remove the `ViewBag.Status` code from the Manage and Account controllers and from the *Views\Account\VerifyCode.cshtml* and *Views\Manage\VerifyPhoneNumber.cshtml* razor views.</span></span> <span data-ttu-id="309f6-130">Кроме того, можно настроить отображение `ViewBag.Status`, чтобы проверить работу этого приложения локально, не прибегая к подключению и отправке сообщений электронной почты и SMS.</span><span class="sxs-lookup"><span data-stu-id="309f6-130">Alternatively, you can keep the `ViewBag.Status` display to test how this app works locally without having to hook up and send email and SMS messages.</span></span>

> [!NOTE]
> <span data-ttu-id="309f6-131">Предупреждение. при изменении каких-либо параметров безопасности в этом примере приложения производства должны будут подвергать аудиту безопасности, который явно вызывает внесенные изменения.</span><span class="sxs-lookup"><span data-stu-id="309f6-131">Warning: If you change any of the security settings in this sample, productions apps will need to undergo a security audit that explicitly calls out the changes made.</span></span>

<a id="SMS"></a>

## <a name="set-up-sms-for-two-factor-authentication"></a><span data-ttu-id="309f6-132">Настройка SMS для двухфакторной проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="309f6-132">Set up SMS for Two-factor authentication</span></span>

<span data-ttu-id="309f6-133">В этом учебнике приводятся инструкции по использованию Twilio или АСПСМС, но можно использовать любой другой поставщик SMS.</span><span class="sxs-lookup"><span data-stu-id="309f6-133">This tutorial provides instructions for using either Twilio or ASPSMS but you can use any other SMS provider.</span></span>

1. <span data-ttu-id="309f6-134">**Создание учетной записи пользователя с помощью поставщика SMS**</span><span class="sxs-lookup"><span data-stu-id="309f6-134">**Creating a User Account with an SMS provider**</span></span>  
  
   <span data-ttu-id="309f6-135">Создайте учетную запись [Twilio](https://www.twilio.com/try-twilio) или [аспсмс](https://www.aspsms.com/asp.net/identity/testcredits/) .</span><span class="sxs-lookup"><span data-stu-id="309f6-135">Create a [Twilio](https://www.twilio.com/try-twilio) or an [ASPSMS](https://www.aspsms.com/asp.net/identity/testcredits/) account.</span></span>
2. <span data-ttu-id="309f6-136">**Установка дополнительных пакетов или добавление ссылок на службы**</span><span class="sxs-lookup"><span data-stu-id="309f6-136">**Installing additional packages or adding service references**</span></span>  
  
   <span data-ttu-id="309f6-137">Twilio</span><span class="sxs-lookup"><span data-stu-id="309f6-137">Twilio:</span></span>  
   <span data-ttu-id="309f6-138">В консоли диспетчера пакетов введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="309f6-138">In the Package Manager Console, enter the following command:</span></span>  
    `Install-Package Twilio`  
  
   <span data-ttu-id="309f6-139">АСПСМС:</span><span class="sxs-lookup"><span data-stu-id="309f6-139">ASPSMS:</span></span>  
   <span data-ttu-id="309f6-140">Необходимо добавить следующую ссылку на службу:</span><span class="sxs-lookup"><span data-stu-id="309f6-140">The following service reference needs to be added:</span></span>  
  
    ![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image1.png)  
  
   <span data-ttu-id="309f6-141">Адрес:</span><span class="sxs-lookup"><span data-stu-id="309f6-141">Address:</span></span>  
    `https://webservice.aspsms.com/aspsmsx2.asmx?WSDL`  
  
   <span data-ttu-id="309f6-142">Пространство имен:</span><span class="sxs-lookup"><span data-stu-id="309f6-142">Namespace:</span></span>  
    `ASPSMSX2`
3. <span data-ttu-id="309f6-143">**Определение учетных данных пользователя поставщика SMS**</span><span class="sxs-lookup"><span data-stu-id="309f6-143">**Figuring out SMS Provider User credentials**</span></span>  
  
   <span data-ttu-id="309f6-144">Twilio</span><span class="sxs-lookup"><span data-stu-id="309f6-144">Twilio:</span></span>  
   <span data-ttu-id="309f6-145">На вкладке **панель мониторинга** учетной записи TWILIO скопируйте **SID учетной записи** и **токен проверки подлинности**.</span><span class="sxs-lookup"><span data-stu-id="309f6-145">From the **Dashboard** tab of your Twilio account, copy the **Account SID** and **Auth token**.</span></span>  
  
   <span data-ttu-id="309f6-146">АСПСМС:</span><span class="sxs-lookup"><span data-stu-id="309f6-146">ASPSMS:</span></span>  
   <span data-ttu-id="309f6-147">В параметрах учетной записи перейдите по адресу **Userkey** и скопируйте его вместе с автоматически определенным **паролем**.</span><span class="sxs-lookup"><span data-stu-id="309f6-147">From your account settings, navigate to **Userkey** and copy it together with your self-defined **Password**.</span></span>  
  
   <span data-ttu-id="309f6-148">Впоследствии эти значения будут храниться в переменных `SMSAccountIdentification` и `SMSAccountPassword`.</span><span class="sxs-lookup"><span data-stu-id="309f6-148">We will later store these values in the variables `SMSAccountIdentification` and `SMSAccountPassword` .</span></span>
4. <span data-ttu-id="309f6-149">**Указание SenderID или инициатора**</span><span class="sxs-lookup"><span data-stu-id="309f6-149">**Specifying SenderID / Originator**</span></span>  
  
   <span data-ttu-id="309f6-150">Twilio</span><span class="sxs-lookup"><span data-stu-id="309f6-150">Twilio:</span></span>  
   <span data-ttu-id="309f6-151">На вкладке **числа** скопируйте номер телефона Twilio.</span><span class="sxs-lookup"><span data-stu-id="309f6-151">From the **Numbers** tab, copy your Twilio phone number.</span></span>  
  
   <span data-ttu-id="309f6-152">АСПСМС:</span><span class="sxs-lookup"><span data-stu-id="309f6-152">ASPSMS:</span></span>  
   <span data-ttu-id="309f6-153">В меню **источник разблокировки** Разблокируйте один или несколько источник или выберите буквенно-цифровой инициатор (не поддерживается всеми сетями).</span><span class="sxs-lookup"><span data-stu-id="309f6-153">Within the **Unlock Originators** Menu, unlock one or more Originators or choose an alphanumeric Originator (Not supported by all networks).</span></span>  
  
   <span data-ttu-id="309f6-154">Позже это значение будет храниться в переменной `SMSAccountFrom`.</span><span class="sxs-lookup"><span data-stu-id="309f6-154">We will later store this value in the variable `SMSAccountFrom` .</span></span>
5. <span data-ttu-id="309f6-155">**Передача учетных данных поставщика SMS в приложение**</span><span class="sxs-lookup"><span data-stu-id="309f6-155">**Transferring SMS provider credentials into app**</span></span>  
  
   <span data-ttu-id="309f6-156">Сделайте учетные данные и номер телефона отправителя доступными для приложения:</span><span class="sxs-lookup"><span data-stu-id="309f6-156">Make the credentials and sender phone number available to the app:</span></span>

    [!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample1.cs)]

    > [!WARNING]
    > <span data-ttu-id="309f6-157">Безопасность — никогда не храните конфиденциальные данные в исходном коде.</span><span class="sxs-lookup"><span data-stu-id="309f6-157">Security - Never store sensitive data in your source code.</span></span> <span data-ttu-id="309f6-158">Учетная запись и учетные данные добавляются в приведенный выше код для упрощения примера.</span><span class="sxs-lookup"><span data-stu-id="309f6-158">The account and credentials are added to the code above to keep the sample simple.</span></span> <span data-ttu-id="309f6-159">См. раздел Ivan Аттен [ASP.NET MVC: Держитесь Private Settings из системы управления версиями](http://typecastexception.com/post/2014/04/06/ASPNET-MVC-Keep-Private-Settings-Out-of-Source-Control.aspx).</span><span class="sxs-lookup"><span data-stu-id="309f6-159">See Jon Atten's [ASP.NET MVC: Keep Private Settings Out of Source Control](http://typecastexception.com/post/2014/04/06/ASPNET-MVC-Keep-Private-Settings-Out-of-Source-Control.aspx).</span></span>
6. <span data-ttu-id="309f6-160">**Реализация обмена данными с поставщиком SMS**</span><span class="sxs-lookup"><span data-stu-id="309f6-160">**Implementation of data transfer to SMS provider**</span></span>  
  
   <span data-ttu-id="309f6-161">Настройте класс `SmsService` в файле *приложения\_старт\идентитиконфиг.КС* .</span><span class="sxs-lookup"><span data-stu-id="309f6-161">Configure the `SmsService`  class in the *App\_Start\IdentityConfig.cs* file.</span></span>  
  
   <span data-ttu-id="309f6-162">В зависимости от используемого поставщика SMS активируйте раздел **Twilio** или **аспсмс** :</span><span class="sxs-lookup"><span data-stu-id="309f6-162">Depending on the used SMS provider activate either the **Twilio** or the **ASPSMS** section:</span></span> 

    [!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample2.cs)]
7. <span data-ttu-id="309f6-163">Запустите приложение и войдите в систему с помощью ранее зарегистрированной учетной записи.</span><span class="sxs-lookup"><span data-stu-id="309f6-163">Run the app and log in with the account you previously registered.</span></span>
8. <span data-ttu-id="309f6-164">Щелкните идентификатор пользователя, который активирует метод действия `Index` в контроллере `Manage`.</span><span class="sxs-lookup"><span data-stu-id="309f6-164">Click on your User ID, which activates the `Index` action method in `Manage` controller.</span></span>  
  
    ![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image2.png)
9. <span data-ttu-id="309f6-165">Нажмите кнопку Добавить.</span><span class="sxs-lookup"><span data-stu-id="309f6-165">Click Add.</span></span>  
  
    ![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image3.png)
10. <span data-ttu-id="309f6-166">Через несколько секунд будет получено текстовое сообщение с кодом проверки.</span><span class="sxs-lookup"><span data-stu-id="309f6-166">In a few seconds you will get a text message with the verification code.</span></span> <span data-ttu-id="309f6-167">Введите его и нажмите кнопку **Отправить**.</span><span class="sxs-lookup"><span data-stu-id="309f6-167">Enter it and press **Submit**.</span></span>  
  
    ![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image4.png)
11. <span data-ttu-id="309f6-168">В представлении "Управление" отображается номер телефона.</span><span class="sxs-lookup"><span data-stu-id="309f6-168">The Manage view shows your phone number was added.</span></span>  
  
    ![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image5.png)

### <a name="examine-the-code"></a><span data-ttu-id="309f6-169">Изучение кода</span><span class="sxs-lookup"><span data-stu-id="309f6-169">Examine the code</span></span>

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample3.cs?highlight=2)]

<span data-ttu-id="309f6-170">Метод действия `Index` в контроллере `Manage` устанавливает сообщение о состоянии на основе предыдущего действия и предоставляет ссылки для изменения локального пароля или добавления локальной учетной записи.</span><span class="sxs-lookup"><span data-stu-id="309f6-170">The `Index` action method in `Manage` controller sets the status message based on your previous action and provides links to change your local password or add a local account.</span></span> <span data-ttu-id="309f6-171">Метод `Index` также отображает штат или номер телефона 2FA, внешние имена входа, 2FA включенные и запомните метод 2FA для этого браузера (см. Далее).</span><span class="sxs-lookup"><span data-stu-id="309f6-171">The `Index` method also displays the state or your 2FA phone number, external logins, 2FA enabled, and remember 2FA method for this browser(explained later).</span></span> <span data-ttu-id="309f6-172">Если щелкнуть свой идентификатор пользователя (адрес электронной почты) в заголовке окна, сообщение не передается.</span><span class="sxs-lookup"><span data-stu-id="309f6-172">Clicking on your user ID (email) in the title bar doesn't pass a message.</span></span> <span data-ttu-id="309f6-173">Щелкните **номер телефона: удалить** ссылка передает `Message=RemovePhoneSuccess` как строку запроса.</span><span class="sxs-lookup"><span data-stu-id="309f6-173">Clicking on the **Phone Number : remove** link passes `Message=RemovePhoneSuccess` as a query string.</span></span>  
  
`https://localhost:44300/Manage?Message=RemovePhoneSuccess`

<span data-ttu-id="309f6-174">[![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image6.png)]</span><span class="sxs-lookup"><span data-stu-id="309f6-174">[![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image6.png)]</span></span>

<span data-ttu-id="309f6-175">Метод действия `AddPhoneNumber` отображает диалоговое окно для ввода номера телефона, который может получить SMS-сообщения.</span><span class="sxs-lookup"><span data-stu-id="309f6-175">The `AddPhoneNumber` action method displays a dialog box to enter a phone number that can receive SMS messages.</span></span>

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample4.cs)]

![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image7.png)

<span data-ttu-id="309f6-176">При нажатии кнопки **отправить код проверки** отправляется номер телефона в метод действия HTTP POST `AddPhoneNumber`.</span><span class="sxs-lookup"><span data-stu-id="309f6-176">Clicking on the **Send verification code** button posts the phone number to the HTTP POST `AddPhoneNumber` action method.</span></span>

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample5.cs?highlight=12)]

<span data-ttu-id="309f6-177">Метод `GenerateChangePhoneNumberTokenAsync` создает маркер безопасности, который будет установлен в SMS Message.</span><span class="sxs-lookup"><span data-stu-id="309f6-177">The `GenerateChangePhoneNumberTokenAsync` method generates the security token which will be set in the SMS message.</span></span> <span data-ttu-id="309f6-178">Если служба SMS настроена, маркер отправляется в виде строки, &quot;код безопасности &lt;токен&gt;&quot;.</span><span class="sxs-lookup"><span data-stu-id="309f6-178">If the SMS service has been configured, the token is sent as the string &quot;Your security code is &lt;token&gt;&quot;.</span></span> <span data-ttu-id="309f6-179">`SmsService.SendAsync` метод вызывается асинхронно, приложение перенаправляется к методу действия `VerifyPhoneNumber` (который отображает следующее диалоговое окно), где можно ввести код проверки.</span><span class="sxs-lookup"><span data-stu-id="309f6-179">The `SmsService.SendAsync` method to is called asynchronously, then the app is redirected to the `VerifyPhoneNumber` action method (which displays the following dialog), where you can enter the verification code.</span></span>

![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image8.png)

<span data-ttu-id="309f6-180">После ввода кода и нажатия кнопки отправить код отправляется в метод действия HTTP POST `VerifyPhoneNumber`.</span><span class="sxs-lookup"><span data-stu-id="309f6-180">Once you enter the code and click submit, the code is posted to the HTTP POST `VerifyPhoneNumber` action method.</span></span>

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample6.cs)]

<span data-ttu-id="309f6-181">Метод `ChangePhoneNumberAsync` проверяет опубликованный код безопасности.</span><span class="sxs-lookup"><span data-stu-id="309f6-181">The `ChangePhoneNumberAsync` method checks the posted security code.</span></span> <span data-ttu-id="309f6-182">Если код правильный, то номер телефона добавляется в поле `PhoneNumber` таблицы `AspNetUsers`.</span><span class="sxs-lookup"><span data-stu-id="309f6-182">If the code is correct, the phone number is added to the `PhoneNumber` field of the `AspNetUsers` table.</span></span> <span data-ttu-id="309f6-183">При успешном вызове вызывается метод `SignInAsync`:</span><span class="sxs-lookup"><span data-stu-id="309f6-183">If that call is successful, the `SignInAsync` method is called:</span></span>

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample7.cs)]

<span data-ttu-id="309f6-184">Параметр `isPersistent` задает, сохраняется ли сеанс проверки подлинности в нескольких запросах.</span><span class="sxs-lookup"><span data-stu-id="309f6-184">The `isPersistent` parameter sets whether the authentication session is persisted across multiple requests.</span></span>

<span data-ttu-id="309f6-185">При изменении профиля безопасности создается новая метка безопасности, которая сохраняется в поле `SecurityStamp` таблицы *AspNetUsers* .</span><span class="sxs-lookup"><span data-stu-id="309f6-185">When you change your security profile, a new security stamp is generated and stored in the `SecurityStamp` field of the *AspNetUsers* table.</span></span> <span data-ttu-id="309f6-186">Обратите внимание, что поле `SecurityStamp` отличается от cookie безопасности.</span><span class="sxs-lookup"><span data-stu-id="309f6-186">Note, the `SecurityStamp` field is different from the security cookie.</span></span> <span data-ttu-id="309f6-187">Файл cookie безопасности не хранится в таблице `AspNetUsers` (или в другом месте в базе данных Identity).</span><span class="sxs-lookup"><span data-stu-id="309f6-187">The security cookie is not stored in the `AspNetUsers` table (or anywhere else in the Identity DB).</span></span> <span data-ttu-id="309f6-188">Маркер безопасности cookie является самозаверяющим с помощью [DPAPI](https://msdn.microsoft.com/library/system.security.cryptography.protecteddata.aspx) и создается с `UserId, SecurityStamp` и сроком действия.</span><span class="sxs-lookup"><span data-stu-id="309f6-188">The security cookie token is self-signed using [DPAPI](https://msdn.microsoft.com/library/system.security.cryptography.protecteddata.aspx) and is created with the `UserId, SecurityStamp` and expiration time information.</span></span>

<span data-ttu-id="309f6-189">По промежуточного слоя cookie проверяет файл cookie для каждого запроса.</span><span class="sxs-lookup"><span data-stu-id="309f6-189">The cookie middleware checks the cookie on each request.</span></span> <span data-ttu-id="309f6-190">Метод `SecurityStampValidator` в классе `Startup` порождает базу данных и периодически проверяет метку безопасности, как указано в `validateInterval`.</span><span class="sxs-lookup"><span data-stu-id="309f6-190">The `SecurityStampValidator` method in the `Startup` class hits the DB and checks security stamp periodically, as specified with the `validateInterval`.</span></span> <span data-ttu-id="309f6-191">Это происходит каждые 30 минут (в нашем примере), если только вы не измените профиль безопасности.</span><span class="sxs-lookup"><span data-stu-id="309f6-191">This only happens every 30 minutes (in our sample) unless you change your security profile.</span></span> <span data-ttu-id="309f6-192">Интервал в 30 минут был выбран для снижения количества обращений к базе данных.</span><span class="sxs-lookup"><span data-stu-id="309f6-192">The 30 minute interval was chosen to minimize trips to the database.</span></span>

<span data-ttu-id="309f6-193">При внесении каких-либо изменений в профиль безопасности необходимо вызвать метод `SignInAsync`.</span><span class="sxs-lookup"><span data-stu-id="309f6-193">The `SignInAsync` method needs to be called when any change is made to the security profile.</span></span> <span data-ttu-id="309f6-194">При изменении профиля безопасности база данных обновляет поле `SecurityStamp` и не вызывает метод `SignInAsync`, который остается в системе *только* до следующего момента, когда конвейер OWIN не достигнет базы данных (`validateInterval`).</span><span class="sxs-lookup"><span data-stu-id="309f6-194">When the security profile changes, the database is updates the `SecurityStamp` field, and without calling the `SignInAsync` method you would stay logged in *only* until the next time the OWIN pipeline hits the database (the `validateInterval`).</span></span> <span data-ttu-id="309f6-195">Это можно проверить, изменив метод `SignInAsync` для немедленного возврата и задав свойству cookie `validateInterval` значение от 30 минут до 5 секунд:</span><span class="sxs-lookup"><span data-stu-id="309f6-195">You can test this by changing the `SignInAsync` method to return immediately, and setting the cookie `validateInterval` property from 30 minutes to 5 seconds:</span></span>

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample8.cs?highlight=3)]

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample9.cs?highlight=20-21)]

<span data-ttu-id="309f6-196">С помощью приведенного выше кода можно изменить профиль безопасности (например, изменить состояние " **включен**"). при сбое метода `SecurityStampValidator.OnValidateIdentity` произойдет выход за 5 секунд.</span><span class="sxs-lookup"><span data-stu-id="309f6-196">With the above code changes, you can change your security profile (for example, by changing the state of **Two Factor Enabled**) and you will be logged out in 5 seconds when the `SecurityStampValidator.OnValidateIdentity` method fails.</span></span> <span data-ttu-id="309f6-197">Удалите строку возврата в методе `SignInAsync`, внесите еще одно изменение профиля безопасности, и вы не будете выходить из системы. Метод `SignInAsync` создает новый файл cookie безопасности.</span><span class="sxs-lookup"><span data-stu-id="309f6-197">Remove the return line in the `SignInAsync` method, make another security profile change and you will not be logged out. The `SignInAsync` method generates a new security cookie.</span></span>

<a id="enable2"></a>

## <a name="enable-two-factor-authentication"></a><span data-ttu-id="309f6-198">Включить двухфакторную проверку подлинности</span><span class="sxs-lookup"><span data-stu-id="309f6-198">Enable two-factor authentication</span></span>

<span data-ttu-id="309f6-199">В примере приложения необходимо использовать пользовательский интерфейс, чтобы включить двухфакторную проверку подлинности (2FA).</span><span class="sxs-lookup"><span data-stu-id="309f6-199">In the sample app, you need to use the UI to enable two-factor authentication (2FA).</span></span> <span data-ttu-id="309f6-200">Чтобы включить 2FA, щелкните свой идентификатор пользователя (псевдоним электронной почты) на панели навигации.![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="309f6-200">To enable 2FA, click on your user ID (email alias) in the navigation bar.![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image9.png)</span></span>  
<span data-ttu-id="309f6-201">Щелкните Включить 2FA.![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image10.png)</span><span class="sxs-lookup"><span data-stu-id="309f6-201">Click on enable 2FA.![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image10.png)</span></span> <span data-ttu-id="309f6-202">Выйдите из, а затем снова войдите в систему.</span><span class="sxs-lookup"><span data-stu-id="309f6-202">Log out, then log back in.</span></span> <span data-ttu-id="309f6-203">Если вы включили электронную почту (см. [предыдущий учебник](account-confirmation-and-password-recovery-with-aspnet-identity.md)), можно выбрать SMS или email для 2FA.![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="309f6-203">If you've enabled email (see my [previous tutorial](account-confirmation-and-password-recovery-with-aspnet-identity.md)), you can select the SMS or email for 2FA.![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image11.png)</span></span> <span data-ttu-id="309f6-204">Отобразится страница Проверка кода, где можно ввести код (с помощью SMS или электронной почты).![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image12.png)</span><span class="sxs-lookup"><span data-stu-id="309f6-204">The Verify Code page is displayed where you can enter the code (from SMS or email).![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image12.png)</span></span> <span data-ttu-id="309f6-205">Если установить флажок **Запомнить этот браузер** , вам не потребуется использовать 2FA для входа на этот компьютер и браузер.</span><span class="sxs-lookup"><span data-stu-id="309f6-205">Clicking on the **Remember this browser** check box will exempt you from needing to use 2FA to log on with that computer and browser.</span></span> <span data-ttu-id="309f6-206">При включении 2FA и нажатии кнопки " **Запомнить" Этот браузер** обеспечит надежную защиту 2FA от злоумышленников, пытающихся получить доступ к вашей учетной записи, если у них нет доступа к вашему компьютеру.</span><span class="sxs-lookup"><span data-stu-id="309f6-206">Enabling 2FA and clicking on the **Remember this browser** will provide you with strong 2FA protection from malicious users trying to access your account, as long as they don't have access to your computer.</span></span> <span data-ttu-id="309f6-207">Это можно сделать на любом частном компьютере, который вы регулярно используете.</span><span class="sxs-lookup"><span data-stu-id="309f6-207">You can do this on any private machine you regularly use.</span></span> <span data-ttu-id="309f6-208">Запоминаем **этот браузер**, вы получаете дополнительную безопасность 2FA на компьютерах, которые вы не используете регулярно, и вы получаете удобный способ, чтобы не выполнять 2FA на своих компьютерах.</span><span class="sxs-lookup"><span data-stu-id="309f6-208">By setting **Remember this browser**, you get the added security of 2FA from computers you don't regularly use, and you get the convenience on not having to go through 2FA on your own computers.</span></span> 

<a id="reg"></a>
## <a name="how-to-register-a-two-factor-authentication-provider"></a><span data-ttu-id="309f6-209">Регистрация поставщика двухфакторной проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="309f6-209">How to register a Two-factor authentication provider</span></span>

<span data-ttu-id="309f6-210">При создании нового проекта MVC файл *IdentityConfig.CS* содержит следующий код для регистрации поставщика двухфакторной проверки подлинности:</span><span class="sxs-lookup"><span data-stu-id="309f6-210">When you create a new MVC project, the *IdentityConfig.cs* file contains the following code to register a Two-factor authentication provider:</span></span>

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample10.cs?highlight=22-35)]

## <a name="add-a-phone-number-for-2fa"></a><span data-ttu-id="309f6-211">Добавление номера телефона для 2FA</span><span class="sxs-lookup"><span data-stu-id="309f6-211">Add a phone number for 2FA</span></span>

<span data-ttu-id="309f6-212">Метод действия `AddPhoneNumber` в контроллере `Manage` создает маркер безопасности и отправляет его на указанный номер телефона.</span><span class="sxs-lookup"><span data-stu-id="309f6-212">The `AddPhoneNumber` action method in the `Manage` controller generates a security token and sends it to the phone number you have provided.</span></span>

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample11.cs)]

<span data-ttu-id="309f6-213">После отправки маркера он перенаправляется к методу действия `VerifyPhoneNumber`, где можно ввести код для регистрации SMS для 2FA.</span><span class="sxs-lookup"><span data-stu-id="309f6-213">After sending the token, it redirects to the `VerifyPhoneNumber` action method, where you can enter the code to register SMS for 2FA.</span></span> <span data-ttu-id="309f6-214">SMS 2FA не используется, пока не будет проверен номер телефона.</span><span class="sxs-lookup"><span data-stu-id="309f6-214">SMS 2FA is not used until you have verified the phone number.</span></span>

## <a name="enabling-2fa"></a><span data-ttu-id="309f6-215">Включение 2FA</span><span class="sxs-lookup"><span data-stu-id="309f6-215">Enabling 2FA</span></span>

<span data-ttu-id="309f6-216">Метод действия `EnableTFA` включает 2FA:</span><span class="sxs-lookup"><span data-stu-id="309f6-216">The `EnableTFA` action method enables 2FA:</span></span>

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample12.cs)]

<span data-ttu-id="309f6-217">Обратите внимание, что необходимо вызвать `SignInAsync`, так как параметр Enable 2FA является изменением профиля безопасности.</span><span class="sxs-lookup"><span data-stu-id="309f6-217">Note the `SignInAsync` must be called because enable 2FA is a change to the security profile.</span></span> <span data-ttu-id="309f6-218">Когда 2FA включен, пользователю потребуется использовать 2FA для входа в систему с помощью описанных ими подходов 2FA (SMS и email в примере).</span><span class="sxs-lookup"><span data-stu-id="309f6-218">When 2FA is enabled, the user will need to use 2FA to log in, using the 2FA approaches they have registered (SMS and email in the sample).</span></span>

<span data-ttu-id="309f6-219">Вы можете добавить дополнительных поставщиков 2FA, таких как генераторы QR-кода, или написать собственную (см. статью [Использование Google Authenticator с ASP.NET Identity](https://www.jerriepelser.com//blog/using-google-authenticator-asp-net-identity/)).</span><span class="sxs-lookup"><span data-stu-id="309f6-219">You can add more 2FA providers such as QR code generators or you can write you own (See [Using Google Authenticator with ASP.NET Identity](https://www.jerriepelser.com//blog/using-google-authenticator-asp-net-identity/)).</span></span>

> [!NOTE]
> <span data-ttu-id="309f6-220">Коды 2FA создаются с помощью [алгоритма одноразового пароля на основе времени](http://en.wikipedia.org/wiki/Time-based_One-time_Password_Algorithm) , а коды действительны в течение шести минут.</span><span class="sxs-lookup"><span data-stu-id="309f6-220">The 2FA codes are generated using [Time-based One-time Password Algorithm](http://en.wikipedia.org/wiki/Time-based_One-time_Password_Algorithm) and codes are valid for six minutes.</span></span> <span data-ttu-id="309f6-221">Если для ввода кода требуется более шести минут, вы получите сообщение об ошибке недопустимого кода.</span><span class="sxs-lookup"><span data-stu-id="309f6-221">If you take more than six minutes to enter the code, you'll get an Invalid code error message.</span></span>

<a id="combine"></a>

## <a name="combine-social-and-local-login-accounts"></a><span data-ttu-id="309f6-222">Объединение социальных и местных учетных записей входа</span><span class="sxs-lookup"><span data-stu-id="309f6-222">Combine social and local login accounts</span></span>

<span data-ttu-id="309f6-223">Вы можете объединить локальные и социальные учетные записи, щелкнув ссылку на электронную почту.</span><span class="sxs-lookup"><span data-stu-id="309f6-223">You can combine local and social accounts by clicking on your email link.</span></span> <span data-ttu-id="309f6-224">В следующей последовательности &quot;RickAndMSFT@gmail.com&quot; сначала создается как локальное имя входа, но вы можете сначала создать учетную запись в качестве социальных сетей, а затем добавить локальное имя входа.</span><span class="sxs-lookup"><span data-stu-id="309f6-224">In the following sequence &quot;RickAndMSFT@gmail.com&quot; is first created as a local login, but you can create the account as a social log in first, then add a local login.</span></span>

![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image13.png)

<span data-ttu-id="309f6-225">Щелкните ссылку **Управление** .</span><span class="sxs-lookup"><span data-stu-id="309f6-225">Click on the **Manage** link.</span></span> <span data-ttu-id="309f6-226">Обратите внимание на 0 внешних (социальных) имен, связанных с этой учетной записью.</span><span class="sxs-lookup"><span data-stu-id="309f6-226">Note the 0 external (social logins) associated with this account.</span></span>

![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image14.png)

<span data-ttu-id="309f6-227">Щелкните ссылку на другой журнал службы и примите запросы приложения.</span><span class="sxs-lookup"><span data-stu-id="309f6-227">Click the link to another log in service and accept the app requests.</span></span> <span data-ttu-id="309f6-228">Две учетные записи объединены, вы сможете войти в систему с любой учетной записью.</span><span class="sxs-lookup"><span data-stu-id="309f6-228">The two accounts have been combined, you will be able to log on with either account.</span></span> <span data-ttu-id="309f6-229">Может потребоваться, чтобы пользователи могли добавлять локальные учетные записи в случае, если служба проверки подлинности в социальных сетях не работает, или более вероятно, что они потеряют доступ к учетной записи социальных сетей.</span><span class="sxs-lookup"><span data-stu-id="309f6-229">You might want your users to add local accounts in case their social log in authentication service is down, or more likely they have lost access to their social account.</span></span>

<span data-ttu-id="309f6-230">На следующем рисунке Tom является входом в социальной сети (который можно увидеть из **внешних имен входа: 1** на странице).</span><span class="sxs-lookup"><span data-stu-id="309f6-230">In the following image, Tom is a social log in (which you can see from the **External Logins: 1** shown on the page).</span></span>

![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image15.png)

<span data-ttu-id="309f6-231">Если щелкнуть " **выбрать пароль** ", вы можете добавить локальный вход в систему, связанный с той же учетной записью.</span><span class="sxs-lookup"><span data-stu-id="309f6-231">Clicking on **Pick a password** allows you to add a local log on associated with the same account.</span></span>

![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image16.png)

<a id="lock"></a>

## <a name="account-lockout-from-brute-force-attacks"></a><span data-ttu-id="309f6-232">Блокировка учетной записи от атак методом подбора</span><span class="sxs-lookup"><span data-stu-id="309f6-232">Account lockout from brute force attacks</span></span>

<span data-ttu-id="309f6-233">Вы можете защитить учетные записи приложения от словарных атак, включив блокировку пользователей.</span><span class="sxs-lookup"><span data-stu-id="309f6-233">You can protect the accounts on your app from dictionary attacks by enabling user lockout.</span></span> <span data-ttu-id="309f6-234">Следующий код в методе `ApplicationUserManager Create` настраивает блокировку:</span><span class="sxs-lookup"><span data-stu-id="309f6-234">The following code in the `ApplicationUserManager Create` method configures lock out:</span></span>

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample13.cs)]

<span data-ttu-id="309f6-235">Приведенный выше код включает блокировку только для двухфакторной проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="309f6-235">The code above enables lockout for two factor authentication only.</span></span> <span data-ttu-id="309f6-236">Хотя можно включить блокировку для имен входа, изменив `shouldLockout` на true в методе `Login` контроллера учетной записи, мы рекомендуем не включать блокировку для входа в систему, так как это делает учетную запись уязвимой для атак [DOS](http://en.wikipedia.org/wiki/Denial-of-service_attack) .</span><span class="sxs-lookup"><span data-stu-id="309f6-236">While you can enable lock out for logins by changing `shouldLockout` to true in the `Login` method of the account controller, we recommend you not enable lock out for logins because it makes the account susceptible to [DOS](http://en.wikipedia.org/wiki/Denial-of-service_attack) login attacks.</span></span> <span data-ttu-id="309f6-237">В примере кода блокировка отключена для учетной записи администратора, созданной в методе `ApplicationDbInitializer Seed`:</span><span class="sxs-lookup"><span data-stu-id="309f6-237">In the sample code, lockout is disabled for the admin account created in the `ApplicationDbInitializer Seed` method:</span></span>

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample14.cs?highlight=19)]

## <a name="requiring-a-user-to-have-a-validated-email-account"></a><span data-ttu-id="309f6-238">Требуется, чтобы пользователь имел проверенную учетную запись электронной почты</span><span class="sxs-lookup"><span data-stu-id="309f6-238">Requiring a user to have a validated email account</span></span>

<span data-ttu-id="309f6-239">Следующий код требует, чтобы пользователь имел проверенную учетную запись электронной почты, прежде чем она сможет войти в систему:</span><span class="sxs-lookup"><span data-stu-id="309f6-239">The following code requires a user to have a validated email account before they can log in:</span></span>

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample15.cs?highlight=8-17)]

## <a name="how-signinmanager-checks-for-2fa-requirement"></a><span data-ttu-id="309f6-240">Как SignInManager проверяет требования 2FA</span><span class="sxs-lookup"><span data-stu-id="309f6-240">How SignInManager checks for 2FA requirement</span></span>

<span data-ttu-id="309f6-241">Как локальный вход, так и журнал в социальных сетях проверяют, включена ли 2FA.</span><span class="sxs-lookup"><span data-stu-id="309f6-241">Both the local log in and social log in check to see if 2FA is enabled.</span></span> <span data-ttu-id="309f6-242">Если 2FA включен, метод входа `SignInManager` возвращает `SignInStatus.RequiresVerification`, и пользователь будет перенаправлен к методу `SendCode` действия, где ему придется ввести код для завершения входа в систему.</span><span class="sxs-lookup"><span data-stu-id="309f6-242">If 2FA is enabled, the `SignInManager` logon method returns `SignInStatus.RequiresVerification`, and the user will be redirected to the `SendCode` action method, where they will have to enter the code to complete the log in sequence.</span></span> <span data-ttu-id="309f6-243">Если пользователь имеет RememberMe для локального файла cookie, `SignInManager` будет возвращать `SignInStatus.Success` и не должен проходить через 2FA.</span><span class="sxs-lookup"><span data-stu-id="309f6-243">If the user has RememberMe is set on the users local cookie, the `SignInManager` will return `SignInStatus.Success` and they will not have to go through 2FA.</span></span>

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample16.cs?highlight=20-22)]

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample17.cs?highlight=10-11,17-18)]

<span data-ttu-id="309f6-244">В следующем коде показан метод действия `SendCode`.</span><span class="sxs-lookup"><span data-stu-id="309f6-244">The following code shows the `SendCode` action method.</span></span> <span data-ttu-id="309f6-245">Создается [селектлиститем](https://msdn.microsoft.com/library/system.web.mvc.selectlistitem.aspx) со всеми МЕТОДами 2FA, включенными для пользователя.</span><span class="sxs-lookup"><span data-stu-id="309f6-245">A [SelectListItem](https://msdn.microsoft.com/library/system.web.mvc.selectlistitem.aspx) is created with all the 2FA methods enabled for the user.</span></span> <span data-ttu-id="309f6-246">[Селектлиститем](https://msdn.microsoft.com/library/system.web.mvc.selectlistitem.aspx) передается в вспомогательный модуль [дропдовнлистфор](https://msdn.microsoft.com/library/system.web.ui.webcontrols.dropdownlist.aspx) , который позволяет пользователю выбрать подход 2FA (обычно это электронная почта и SMS).</span><span class="sxs-lookup"><span data-stu-id="309f6-246">The [SelectListItem](https://msdn.microsoft.com/library/system.web.mvc.selectlistitem.aspx) is passed to the [DropDownListFor](https://msdn.microsoft.com/library/system.web.ui.webcontrols.dropdownlist.aspx) helper, which allows the user to select the 2FA approach (typically email and SMS).</span></span>

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample18.cs)]

<span data-ttu-id="309f6-247">После того как пользователь отправляет 2FA подход, вызывается метод действия `HTTP POST SendCode`, `SignInManager` отправляется код 2FA, а пользователь перенаправляется к методу `VerifyCode` действия, где можно ввести код для завершения входа.</span><span class="sxs-lookup"><span data-stu-id="309f6-247">Once the user posts the 2FA approach, the `HTTP POST SendCode` action method is called, the `SignInManager` sends the 2FA code, and the user is redirected to the `VerifyCode` action method where they can enter the code to complete the log in.</span></span>

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample19.cs?highlight=3,13-14,18)]

## <a name="2fa-lockout"></a><span data-ttu-id="309f6-248">Блокировка 2FA</span><span class="sxs-lookup"><span data-stu-id="309f6-248">2FA Lockout</span></span>

<span data-ttu-id="309f6-249">Несмотря на то, что вы можете задать блокировку учетных записей при попытке входа в систему с использованием пароля, этот подход сделает ваше имя входа уязвимым для блокировки [DOS](http://en.wikipedia.org/wiki/Denial-of-service_attack) .</span><span class="sxs-lookup"><span data-stu-id="309f6-249">Although you can set account lockout on login password attempt failures, that approach makes your login susceptible to [DOS](http://en.wikipedia.org/wiki/Denial-of-service_attack) lockouts.</span></span> <span data-ttu-id="309f6-250">Рекомендуется использовать блокировку учетных записей только с 2FA.</span><span class="sxs-lookup"><span data-stu-id="309f6-250">We recommend you use account lockout only with 2FA.</span></span> <span data-ttu-id="309f6-251">При создании `ApplicationUserManager` в примере кода задается 2FA блокировка, а `MaxFailedAccessAttemptsBeforeLockout` — пять.</span><span class="sxs-lookup"><span data-stu-id="309f6-251">When the `ApplicationUserManager` is created, the sample code sets 2FA lockout and `MaxFailedAccessAttemptsBeforeLockout` to five.</span></span> <span data-ttu-id="309f6-252">Когда пользователь входит в систему (через локальную учетную запись или учетную запись социальных сетей), каждая попытка неудачной попытки на 2FA сохраняется, и при достижении максимального количества попыток пользователь блокируется в течение пяти минут (можно установить время блокировки с `DefaultAccountLockoutTimeSpan`).</span><span class="sxs-lookup"><span data-stu-id="309f6-252">Once a user logs in (through local account or social account), each failed attempt at 2FA is stored, and if the maximum attempts is reached, the user is locked out for five minutes (you can set the lock out time with `DefaultAccountLockoutTimeSpan`).</span></span>

<a id="addRes"></a>

## <a name="additional-resources"></a><span data-ttu-id="309f6-253">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="309f6-253">Additional Resources</span></span>

- <span data-ttu-id="309f6-254">[ASP.NET Identity Рекомендуемые ресурсы](../getting-started/aspnet-identity-recommended-resources.md) Полный список блогов по удостоверениям, видеороликов, руководств и полезных ссылок.</span><span class="sxs-lookup"><span data-stu-id="309f6-254">[ASP.NET Identity Recommended Resources](../getting-started/aspnet-identity-recommended-resources.md) Complete list of Identity blogs, videos, tutorials and great SO links.</span></span>
- <span data-ttu-id="309f6-255">В [приложении MVC 5 с помощью входа Facebook, Twitter, LinkedIn и Google OAuth2](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md) также показано, как добавить сведения о профиле в таблицу Users.</span><span class="sxs-lookup"><span data-stu-id="309f6-255">[MVC 5 App with Facebook, Twitter, LinkedIn and Google OAuth2 Sign-on](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md) also shows how to add profile information to the users table.</span></span>
- <span data-ttu-id="309f6-256">[ASP.NET MVC и Identity 2,0: основные сведения](http://typecastexception.com/post/2014/04/20/ASPNET-MVC-and-Identity-20-Understanding-the-Basics.aspx) по Джон аттен.</span><span class="sxs-lookup"><span data-stu-id="309f6-256">[ASP.NET MVC and Identity 2.0: Understanding the Basics](http://typecastexception.com/post/2014/04/20/ASPNET-MVC-and-Identity-20-Understanding-the-Basics.aspx) by John Atten.</span></span>
- [<span data-ttu-id="309f6-257">Подтверждение учетной записи и восстановление пароля с ASP.NET Identity</span><span class="sxs-lookup"><span data-stu-id="309f6-257">Account Confirmation and Password Recovery with ASP.NET Identity</span></span>](account-confirmation-and-password-recovery-with-aspnet-identity.md)
- [<span data-ttu-id="309f6-258">Введение в ASP.NET Identity</span><span class="sxs-lookup"><span data-stu-id="309f6-258">Introduction to ASP.NET Identity</span></span>](../getting-started/introduction-to-aspnet-identity.md)
- <span data-ttu-id="309f6-259">[Объявление о ВЫпуске RTM ASP.NET Identity 2.0.0](https://blogs.msdn.com/b/webdev/archive/2014/03/20/test-announcing-rtm-of-asp-net-identity-2-0-0.aspx) by получения запись блога.</span><span class="sxs-lookup"><span data-stu-id="309f6-259">[Announcing RTM of ASP.NET Identity 2.0.0](https://blogs.msdn.com/b/webdev/archive/2014/03/20/test-announcing-rtm-of-asp-net-identity-2-0-0.aspx) by Pranav Rastogi.</span></span>
- <span data-ttu-id="309f6-260">[ASP.NET Identity 2,0: Настройка проверки учетной записи и двухфакторной авторизации](http://typecastexception.com/post/2014/04/20/ASPNET-Identity-20-Setting-Up-Account-Validation-and-Two-Factor-Authorization.aspx) с помощью Джон аттен.</span><span class="sxs-lookup"><span data-stu-id="309f6-260">[ASP.NET Identity 2.0: Setting Up Account Validation and Two-Factor Authorization](http://typecastexception.com/post/2014/04/20/ASPNET-Identity-20-Setting-Up-Account-Validation-and-Two-Factor-Authorization.aspx) by John Atten.</span></span>
