---
uid: mvc/overview/security/aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication
title: Приложение ASP.NET MVC 5 с использованием SMS и двухфакторной проверки подлинности по электронной почте | Документация Майкрософт
author: Rick-Anderson
description: В этом руководстве показано, как создать веб-приложение ASP.NET MVC 5 с двухфакторной проверкой подлинности. Необходимо завершить создание защищенного веб-приложения ASP.NET MVC 5 с помощью...
ms.author: riande
ms.date: 08/20/2015
ms.assetid: f50a5cdb-c06a-46ed-aa14-fc5b049dc8dc
msc.legacyurl: /mvc/overview/security/aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication
msc.type: authoredcontent
ms.openlocfilehash: c14149d802bfc0a227a839a2981dc3e8a3849c25
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78432822"
---
# <a name="aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication"></a><span data-ttu-id="1671e-104">Приложение ASP.NET MVC 5 с двухфакторной проверкой подлинности по SMS и электронной почте</span><span class="sxs-lookup"><span data-stu-id="1671e-104">ASP.NET MVC 5 app with SMS and email Two-Factor Authentication</span></span>

<span data-ttu-id="1671e-105">по [Рик Андерсон (](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="1671e-105">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

> <span data-ttu-id="1671e-106">В этом руководстве показано, как создать веб-приложение ASP.NET MVC 5 с двухфакторной проверкой подлинности.</span><span class="sxs-lookup"><span data-stu-id="1671e-106">This tutorial shows you how to build an ASP.NET MVC 5 web app with Two-Factor Authentication.</span></span> <span data-ttu-id="1671e-107">Прежде чем продолжить [, создайте безопасное веб-приложение ASP.NET MVC 5 с входом, подтверждением электронной почты и сбросом пароля](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset.md) .</span><span class="sxs-lookup"><span data-stu-id="1671e-107">You should complete [Create a secure ASP.NET MVC 5 web app with log in, email confirmation and password reset](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset.md) before proceeding.</span></span> <span data-ttu-id="1671e-108">Готовое приложение можно скачать [здесь](https://code.msdn.microsoft.com/MVC-5-with-2FA-email-8f26d952).</span><span class="sxs-lookup"><span data-stu-id="1671e-108">You can download the completed application [here](https://code.msdn.microsoft.com/MVC-5-with-2FA-email-8f26d952).</span></span> <span data-ttu-id="1671e-109">Загрузка содержит вспомогательные средства отладки, которые позволяют протестировать электронную почту и SMS без настройки электронной почты или поставщика SMS.</span><span class="sxs-lookup"><span data-stu-id="1671e-109">The download contains debugging helpers that let you test email confirmation and SMS without setting up an email or SMS provider.</span></span>
> 
> <span data-ttu-id="1671e-110">Этот учебник написан на [Рик Андерсон (](https://blogs.msdn.com/rickAndy) (Twitter: [@RickAndMSFT](https://twitter.com/RickAndMSFT) ).</span><span class="sxs-lookup"><span data-stu-id="1671e-110">This tutorial was written by [Rick Anderson](https://blogs.msdn.com/rickAndy) ( Twitter: [@RickAndMSFT](https://twitter.com/RickAndMSFT) ).</span></span>

- [<span data-ttu-id="1671e-111">Создание приложения ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="1671e-111">Create an ASP.NET MVC app</span></span>](#createMvc)
- [<span data-ttu-id="1671e-112">Настройка SMS для двухфакторной проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="1671e-112">Set up SMS for Two-factor authentication</span></span>](#SMS)
- [<span data-ttu-id="1671e-113">Включить двухфакторную проверку подлинности</span><span class="sxs-lookup"><span data-stu-id="1671e-113">Enable Two-factor authentication</span></span>](#enable2)
- [<span data-ttu-id="1671e-114">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="1671e-114">Additional Resources</span></span>](#addRes)

<a id="createMvc"></a>
## <a name="create-an-aspnet-mvc-app"></a><span data-ttu-id="1671e-115">Создание приложения ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="1671e-115">Create an ASP.NET MVC app</span></span>

<span data-ttu-id="1671e-116">Начните с установки и запуска [Visual Studio Express 2013 для Web](https://go.microsoft.com/fwlink/?LinkId=299058) или [Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566).</span><span class="sxs-lookup"><span data-stu-id="1671e-116">Start by installing and running [Visual Studio Express 2013 for Web](https://go.microsoft.com/fwlink/?LinkId=299058) or [Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566).</span></span> <span data-ttu-id="1671e-117">Установите [Visual Studio 2013 обновление 3](https://go.microsoft.com/fwlink/?LinkId=390465) или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="1671e-117">Install [Visual Studio 2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390465) or higher.</span></span>

> [!NOTE]
> <span data-ttu-id="1671e-118">Внимание! перед продолжением необходимо [создать безопасное веб-приложение ASP.NET MVC 5 с входом, подтверждением электронной почты и сбросом пароля](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset.md) .</span><span class="sxs-lookup"><span data-stu-id="1671e-118">Warning: You should complete [Create a secure ASP.NET MVC 5 web app with log in, email confirmation and password reset](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset.md) before proceeding.</span></span> <span data-ttu-id="1671e-119">Для работы с этим руководством необходимо установить [Visual Studio 2013 обновление 3](https://go.microsoft.com/fwlink/?LinkId=390465) или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="1671e-119">You must install [Visual Studio 2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390465) or higher to complete this tutorial.</span></span>

1. <span data-ttu-id="1671e-120">Создайте новый веб-проект ASP.NET и выберите шаблон MVC.</span><span class="sxs-lookup"><span data-stu-id="1671e-120">Create a new ASP.NET Web project and select the MVC template.</span></span> <span data-ttu-id="1671e-121">Веб-формы также поддерживают ASP.NET Identity, поэтому можно выполнять аналогичные действия в приложении Web Forms.</span><span class="sxs-lookup"><span data-stu-id="1671e-121">Web Forms also supports ASP.NET Identity, so you could follow similar steps in a web forms app.</span></span>  
    ![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image1.png)
2. <span data-ttu-id="1671e-122">Оставьте проверку подлинности по умолчанию как **учетные записи отдельных пользователей**.</span><span class="sxs-lookup"><span data-stu-id="1671e-122">Leave the default authentication as **Individual User Accounts**.</span></span> <span data-ttu-id="1671e-123">Если вы хотите разместить приложение в Azure, оставьте флажок установленным.</span><span class="sxs-lookup"><span data-stu-id="1671e-123">If you'd like to host the app in Azure, leave the check box checked.</span></span> <span data-ttu-id="1671e-124">Далее в этом руководстве мы будем выполнять развертывание в Azure.</span><span class="sxs-lookup"><span data-stu-id="1671e-124">Later in the tutorial we will deploy to Azure.</span></span> <span data-ttu-id="1671e-125">Вы можете [бесплатно открыть учетную запись Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="1671e-125">You can [open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span></span>
3. <span data-ttu-id="1671e-126">Настройте [проект для использования SSL](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="1671e-126">Set the [project to use SSL](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md).</span></span>

<a id="SMS"></a>
## <a name="set-up-sms-for-two-factor-authentication"></a><span data-ttu-id="1671e-127">Настройка SMS для двухфакторной проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="1671e-127">Set up SMS for Two-factor authentication</span></span>

<span data-ttu-id="1671e-128">В этом учебнике приводятся инструкции по использованию Twilio или АСПСМС, но можно использовать любой другой поставщик SMS.</span><span class="sxs-lookup"><span data-stu-id="1671e-128">This tutorial provides instructions for using either Twilio or ASPSMS but you can use any other SMS provider.</span></span>

1. <span data-ttu-id="1671e-129">**Создание учетной записи пользователя с помощью поставщика SMS**</span><span class="sxs-lookup"><span data-stu-id="1671e-129">**Creating a User Account with an SMS provider**</span></span>  
  
   <span data-ttu-id="1671e-130">Создайте учетную запись [Twilio](https://www.twilio.com/try-twilio) или [аспсмс](https://www.aspsms.com/asp.net/identity/testcredits/) .</span><span class="sxs-lookup"><span data-stu-id="1671e-130">Create a [Twilio](https://www.twilio.com/try-twilio) or an [ASPSMS](https://www.aspsms.com/asp.net/identity/testcredits/) account.</span></span>
2. <span data-ttu-id="1671e-131">**Установка дополнительных пакетов или добавление ссылок на службы**</span><span class="sxs-lookup"><span data-stu-id="1671e-131">**Installing additional packages or adding service references**</span></span>  
  
   <span data-ttu-id="1671e-132">Twilio</span><span class="sxs-lookup"><span data-stu-id="1671e-132">Twilio:</span></span>  
   <span data-ttu-id="1671e-133">В консоли диспетчера пакетов введите следующую команду.</span><span class="sxs-lookup"><span data-stu-id="1671e-133">In the Package Manager Console, enter the following command:</span></span>  
    `Install-Package Twilio`  
  
   <span data-ttu-id="1671e-134">АСПСМС:</span><span class="sxs-lookup"><span data-stu-id="1671e-134">ASPSMS:</span></span>  
   <span data-ttu-id="1671e-135">Необходимо добавить следующую ссылку на службу:</span><span class="sxs-lookup"><span data-stu-id="1671e-135">The following service reference needs to be added:</span></span>  
  
    ![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image2.png)  
  
   <span data-ttu-id="1671e-136">Адрес:</span><span class="sxs-lookup"><span data-stu-id="1671e-136">Address:</span></span>  
    `https://webservice.aspsms.com/aspsmsx2.asmx?WSDL`  
  
   <span data-ttu-id="1671e-137">Пространство имен:</span><span class="sxs-lookup"><span data-stu-id="1671e-137">Namespace:</span></span>  
    `ASPSMSX2`
3. <span data-ttu-id="1671e-138">**Определение учетных данных пользователя поставщика SMS**</span><span class="sxs-lookup"><span data-stu-id="1671e-138">**Figuring out SMS Provider User credentials**</span></span>  
  
   <span data-ttu-id="1671e-139">Twilio</span><span class="sxs-lookup"><span data-stu-id="1671e-139">Twilio:</span></span>  
   <span data-ttu-id="1671e-140">На вкладке **панель мониторинга** учетной записи TWILIO скопируйте **SID учетной записи** и **токен проверки подлинности**.</span><span class="sxs-lookup"><span data-stu-id="1671e-140">From the **Dashboard** tab of your Twilio account, copy the **Account SID** and **Auth token**.</span></span>  
  
   <span data-ttu-id="1671e-141">АСПСМС:</span><span class="sxs-lookup"><span data-stu-id="1671e-141">ASPSMS:</span></span>  
   <span data-ttu-id="1671e-142">В параметрах учетной записи перейдите по адресу **Userkey** и скопируйте его вместе с автоматически определенным **паролем**.</span><span class="sxs-lookup"><span data-stu-id="1671e-142">From your account settings, navigate to **Userkey** and copy it together with your self-defined **Password**.</span></span>  
  
   <span data-ttu-id="1671e-143">Позже эти значения будут храниться в файле *Web. config* в ключах `"SMSAccountIdentification"` и `"SMSAccountPassword"`.</span><span class="sxs-lookup"><span data-stu-id="1671e-143">We will later store these values in the *web.config* file within the keys `"SMSAccountIdentification"` and `"SMSAccountPassword"` .</span></span>
4. <span data-ttu-id="1671e-144">**Указание SenderID или инициатора**</span><span class="sxs-lookup"><span data-stu-id="1671e-144">**Specifying SenderID / Originator**</span></span>  
  
   <span data-ttu-id="1671e-145">Twilio</span><span class="sxs-lookup"><span data-stu-id="1671e-145">Twilio:</span></span>  
   <span data-ttu-id="1671e-146">На вкладке **числа** скопируйте номер телефона Twilio.</span><span class="sxs-lookup"><span data-stu-id="1671e-146">From the **Numbers** tab, copy your Twilio phone number.</span></span>  
  
   <span data-ttu-id="1671e-147">АСПСМС:</span><span class="sxs-lookup"><span data-stu-id="1671e-147">ASPSMS:</span></span>  
   <span data-ttu-id="1671e-148">В меню **источник разблокировки** Разблокируйте один или несколько источник или выберите буквенно-цифровой инициатор (не поддерживается всеми сетями).</span><span class="sxs-lookup"><span data-stu-id="1671e-148">Within the **Unlock Originators** Menu, unlock one or more Originators or choose an alphanumeric Originator (Not supported by all networks).</span></span>  
  
   <span data-ttu-id="1671e-149">Позже это значение будет храниться в файле *Web. config* в рамках ключевого `"SMSAccountFrom"`.</span><span class="sxs-lookup"><span data-stu-id="1671e-149">We will later store this value in the *web.config* file within the key `"SMSAccountFrom"` .</span></span>
5. <span data-ttu-id="1671e-150">**Передача учетных данных поставщика SMS в приложение**</span><span class="sxs-lookup"><span data-stu-id="1671e-150">**Transferring SMS provider credentials into app**</span></span>  
  
   <span data-ttu-id="1671e-151">Сделайте учетные данные и номер телефона отправителя доступными для приложения.</span><span class="sxs-lookup"><span data-stu-id="1671e-151">Make the credentials and sender phone number available to the app.</span></span> <span data-ttu-id="1671e-152">Для простоты мы будем хранить эти значения в файле *Web. config* .</span><span class="sxs-lookup"><span data-stu-id="1671e-152">To keep things simple we will store these values in the *web.config* file.</span></span> <span data-ttu-id="1671e-153">При развертывании в Azure значения можно хранить безопасно в разделе **Параметры приложения** на вкладке веб-сайт Настройка.</span><span class="sxs-lookup"><span data-stu-id="1671e-153">When we deploy to Azure, we can store the values securely in the **app settings** section on the web site configure tab.</span></span> 

    [!code-xml[Main](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/samples/sample1.xml?highlight=8-10)]

    > [!WARNING]
    > <span data-ttu-id="1671e-154">Безопасность — никогда не храните конфиденциальные данные в исходном коде.</span><span class="sxs-lookup"><span data-stu-id="1671e-154">Security - Never store sensitive data in your source code.</span></span> <span data-ttu-id="1671e-155">Учетная запись и учетные данные добавляются в приведенный выше код для упрощения примера.</span><span class="sxs-lookup"><span data-stu-id="1671e-155">The account and credentials are added to the code above to keep the sample simple.</span></span> <span data-ttu-id="1671e-156">См. рекомендации [по развертыванию паролей и других конфиденциальных данных в ASP.NET и Azure](../../../identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure.md).</span><span class="sxs-lookup"><span data-stu-id="1671e-156">See [Best practices for deploying passwords and other sensitive data to ASP.NET and Azure](../../../identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure.md).</span></span>
6. <span data-ttu-id="1671e-157">**Реализация обмена данными с поставщиком SMS**</span><span class="sxs-lookup"><span data-stu-id="1671e-157">**Implementation of data transfer to SMS provider**</span></span>  
  
   <span data-ttu-id="1671e-158">Настройте класс `SmsService` в файле *приложения\_старт\идентитиконфиг.КС* .</span><span class="sxs-lookup"><span data-stu-id="1671e-158">Configure the `SmsService`  class in the *App\_Start\IdentityConfig.cs* file.</span></span>  
  
   <span data-ttu-id="1671e-159">В зависимости от используемого поставщика SMS активируйте раздел **Twilio** или **аспсмс** :</span><span class="sxs-lookup"><span data-stu-id="1671e-159">Depending on the used SMS provider activate either the **Twilio** or the **ASPSMS** section:</span></span> 

    [!code-csharp[Main](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/samples/sample2.cs)]
7. <span data-ttu-id="1671e-160">Обновите представление Razor *виевс\манаже\индекс.кштмл* : (Примечание. не просто удаляйте комментарии в коде выхода, используйте приведенный ниже код.)</span><span class="sxs-lookup"><span data-stu-id="1671e-160">Update the *Views\Manage\Index.cshtml* Razor view: (note: don't just remove the comments in the exiting code, use the code below.)</span></span>  

    [!code-cshtml[Main](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/samples/sample3.cshtml?highlight=29-66)]
8. <span data-ttu-id="1671e-161">Убедитесь, что методы действия `EnableTwoFactorAuthentication` и `DisableTwoFactorAuthentication` в `ManageController` имеют атрибут[[ValidateAntiForgeryToken]](https://msdn.microsoft.com/library/system.web.mvc.validateantiforgerytokenattribute(v=vs.118).aspx) :</span><span class="sxs-lookup"><span data-stu-id="1671e-161">Verify the `EnableTwoFactorAuthentication` and `DisableTwoFactorAuthentication` action methods in the `ManageController` have the[[ValidateAntiForgeryToken]](https://msdn.microsoft.com/library/system.web.mvc.validateantiforgerytokenattribute(v=vs.118).aspx) attribute:</span></span>  

    [!code-csharp[Main](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/samples/sample4.cs?highlight=3,16)]
9. <span data-ttu-id="1671e-162">Запустите приложение и войдите в систему с помощью ранее зарегистрированной учетной записи.</span><span class="sxs-lookup"><span data-stu-id="1671e-162">Run the app and log in with the account you previously registered.</span></span>
10. <span data-ttu-id="1671e-163">Щелкните идентификатор пользователя, который активирует метод действия `Index` в контроллере `Manage`.</span><span class="sxs-lookup"><span data-stu-id="1671e-163">Click on your User ID, which activates the `Index` action method in `Manage` controller.</span></span>  
    ![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image3.png)
11. <span data-ttu-id="1671e-164">Нажмите кнопку «Добавить».</span><span class="sxs-lookup"><span data-stu-id="1671e-164">Click Add.</span></span>  
    ![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image4.png)
12. <span data-ttu-id="1671e-165">Метод действия `AddPhoneNumber` отображает диалоговое окно для ввода номера телефона, который может получить SMS-сообщения.</span><span class="sxs-lookup"><span data-stu-id="1671e-165">The `AddPhoneNumber` action method displays a dialog box to enter a phone number that can receive SMS messages.</span></span>

    [!code-csharp[Main](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/samples/sample5.cs)]

    ![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image5.png)
13. <span data-ttu-id="1671e-166">Через несколько секунд будет получено текстовое сообщение с кодом проверки.</span><span class="sxs-lookup"><span data-stu-id="1671e-166">In a few seconds you will get a text message with the verification code.</span></span> <span data-ttu-id="1671e-167">Введите его и нажмите кнопку **Отправить**.</span><span class="sxs-lookup"><span data-stu-id="1671e-167">Enter it and press **Submit**.</span></span>  
    ![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image6.png)
14. <span data-ttu-id="1671e-168">В представлении "Управление" отображается номер телефона.</span><span class="sxs-lookup"><span data-stu-id="1671e-168">The Manage view shows your phone number was added.</span></span>

<a id="enable2"></a>
## <a name="enable-two-factor-authentication"></a><span data-ttu-id="1671e-169">Включение двухфакторной проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="1671e-169">Enable two-factor authentication</span></span>

<span data-ttu-id="1671e-170">В приложении, созданном шаблоном, необходимо использовать пользовательский интерфейс, чтобы включить двухфакторную проверку подлинности (2FA).</span><span class="sxs-lookup"><span data-stu-id="1671e-170">In the template generated app, you need to use the UI to enable two-factor authentication (2FA).</span></span> <span data-ttu-id="1671e-171">Чтобы включить 2FA, щелкните свой идентификатор пользователя (псевдоним электронной почты) на панели навигации.</span><span class="sxs-lookup"><span data-stu-id="1671e-171">To enable 2FA, click on your user ID (email alias) in the navigation bar.</span></span>

![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image7.png)

<span data-ttu-id="1671e-172">Щелкните Включить 2FA.</span><span class="sxs-lookup"><span data-stu-id="1671e-172">Click on enable 2FA.</span></span>

![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image8.png)

<span data-ttu-id="1671e-173">Выполните выход, а затем снова войдите в систему.</span><span class="sxs-lookup"><span data-stu-id="1671e-173">Logout, then log back in.</span></span> <span data-ttu-id="1671e-174">Если вы включили электронную почту (см. [предыдущий учебник](../../../identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md)), можно выбрать SMS или email для 2FA.</span><span class="sxs-lookup"><span data-stu-id="1671e-174">If you've enabled email (see my [previous tutorial](../../../identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md)), you can select the SMS or email for 2FA.</span></span>

![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image9.png)

<span data-ttu-id="1671e-175">Отобразится страница Проверка кода, где можно ввести код (с помощью SMS или электронной почты).</span><span class="sxs-lookup"><span data-stu-id="1671e-175">The Verify Code page is displayed where you can enter the code (from SMS or email).</span></span>

![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image10.png)

<span data-ttu-id="1671e-176">Если установить флажок **Запомнить этот браузер** , вам не нужно будет использовать 2FA для входа в систему при использовании браузера и устройства, на котором вы проверяли флажок.</span><span class="sxs-lookup"><span data-stu-id="1671e-176">Clicking on the **Remember this browser** check box will exempt you from needing to use 2FA to log in when using the browser and device where you checked the box.</span></span> <span data-ttu-id="1671e-177">Пока пользователи-злоумышленники не смогут получить доступ к вашему устройству, что позволит 2FA и щелкнуть **Запомнить этот браузер** , вы сможете получить удобный доступ к паролю, сохранив при этом строгую защиту 2FA для доступа с устройств, не являющихся доверенными.</span><span class="sxs-lookup"><span data-stu-id="1671e-177">As long as malicious users can't gain access to your device, enabling 2FA and clicking on the **Remember this browser** will provide you with convenient one step password access, while still retaining strong 2FA protection for all access from non-trusted devices.</span></span> <span data-ttu-id="1671e-178">Это можно сделать на любом устройстве закрытого, которые регулярно использовать.</span><span class="sxs-lookup"><span data-stu-id="1671e-178">You can do this on any private device you regularly use.</span></span>

<span data-ttu-id="1671e-179">В этом учебнике содержатся краткие сведения о включении 2FA в новом приложении ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="1671e-179">This tutorial provides a quick introduction to enabling 2FA on a new ASP.NET MVC app.</span></span> <span data-ttu-id="1671e-180">Мой учебник, посвященный [двухфакторной проверке подлинности с помощью SMS и электронной почты с ASP.NET Identity](../../../identity/overview/features-api/two-factor-authentication-using-sms-and-email-with-aspnet-identity.md) , подробно расскажу о коде, выделенном в примере.</span><span class="sxs-lookup"><span data-stu-id="1671e-180">My tutorial [Two-factor authentication using SMS and email with ASP.NET Identity](../../../identity/overview/features-api/two-factor-authentication-using-sms-and-email-with-aspnet-identity.md) goes into detail on the code behind the sample.</span></span>

<a id="addRes"></a>
## <a name="additional-resources"></a><span data-ttu-id="1671e-181">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="1671e-181">Additional Resources</span></span>

- <span data-ttu-id="1671e-182">[Двухфакторная проверка подлинности с помощью SMS и электронной почты с ASP.NET Identity](../../../identity/overview/features-api/two-factor-authentication-using-sms-and-email-with-aspnet-identity.md) Подробное описание двухфакторной проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="1671e-182">[Two-factor authentication using SMS and email with ASP.NET Identity](../../../identity/overview/features-api/two-factor-authentication-using-sms-and-email-with-aspnet-identity.md) Goes into detail on Two-factor authentication</span></span>
- [<span data-ttu-id="1671e-183">Ссылки на ASP.NET Identity Рекомендуемые ресурсы</span><span class="sxs-lookup"><span data-stu-id="1671e-183">Links to ASP.NET Identity Recommended Resources</span></span>](../../../identity/overview/getting-started/aspnet-identity-recommended-resources.md)
- <span data-ttu-id="1671e-184">[Подтверждение учетной записи и восстановление пароля с ASP.NET Identity](../../../identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md) Дополнительные сведения о восстановлении пароля и подтверждении учетной записи.</span><span class="sxs-lookup"><span data-stu-id="1671e-184">[Account Confirmation and Password Recovery with ASP.NET Identity](../../../identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md) Goes into more detail on password recovery and account confirmation.</span></span>
- <span data-ttu-id="1671e-185">[Приложение MVC 5 с входом Facebook, Twitter, LinkedIn и Google OAuth2](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md) В этом руководстве показано, как написать приложение ASP.NET MVC 5 с проверкой подлинности Facebook и Google OAuth 2.</span><span class="sxs-lookup"><span data-stu-id="1671e-185">[MVC 5 App with Facebook, Twitter, LinkedIn and Google OAuth2 Sign-on](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md) This tutorial shows you how to write an ASP.NET MVC 5 app with Facebook and Google OAuth 2 authorization.</span></span> <span data-ttu-id="1671e-186">В нем также показано, как добавить дополнительные данные в базу данных удостоверений.</span><span class="sxs-lookup"><span data-stu-id="1671e-186">It also shows how to add additional data to the Identity database.</span></span>
- <span data-ttu-id="1671e-187">[Развертывание безопасного приложения MVC ASP.NET с членством, OAuth и базой данных SQL в Azure Web](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data).</span><span class="sxs-lookup"><span data-stu-id="1671e-187">[Deploy a Secure ASP.NET MVC app with Membership, OAuth, and SQL Database to Azure Web](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data).</span></span> <span data-ttu-id="1671e-188">В этом руководстве описывается добавление развертывания Azure, защита приложения с помощью ролей, использование API членства для добавления пользователей и ролей, а также дополнительные функции безопасности.</span><span class="sxs-lookup"><span data-stu-id="1671e-188">This tutorial adds Azure deployment, how to secure your app with roles, how to use the membership API to add users and roles, and additional security features.</span></span>
- [<span data-ttu-id="1671e-189">Создание приложения Google для OAuth 2 и подключение приложения к проекту</span><span class="sxs-lookup"><span data-stu-id="1671e-189">Creating a Google app for OAuth 2 and connecting the app to the project</span></span>](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md#goog)
- [<span data-ttu-id="1671e-190">Создание приложения в Facebook и подключение приложения к проекту</span><span class="sxs-lookup"><span data-stu-id="1671e-190">Creating the app in Facebook and connecting the app to the project</span></span>](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md#fb)
- [<span data-ttu-id="1671e-191">Настройка SSL в проекте</span><span class="sxs-lookup"><span data-stu-id="1671e-191">Setting up SSL in the Project</span></span>](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md#ssl)
- [<span data-ttu-id="1671e-192">Как настроить C# и ASP.NET среду разработки MVC</span><span class="sxs-lookup"><span data-stu-id="1671e-192">How to set up your C# and ASP.NET MVC development environment</span></span>](https://www.twilio.com/docs/usage/tutorials/how-to-set-up-your-csharp-and-asp-net-mvc-development-environment)
