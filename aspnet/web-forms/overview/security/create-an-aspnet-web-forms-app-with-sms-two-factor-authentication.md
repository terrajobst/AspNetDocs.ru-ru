---
uid: web-forms/overview/security/create-an-aspnet-web-forms-app-with-sms-two-factor-authentication
title: Создание приложения ASP.NET Web Forms с помощью двусторонней проверки подлинности SMS (C#) | Документация Майкрософт
author: Erikre
description: В этом руководстве показано, как создать приложение веб-форм ASP.NET с двухфакторной проверкой подлинности. Этот учебник был разработан для дополнения учебника с названием CR...
ms.author: riande
ms.date: 10/09/2014
ms.assetid: 716264ae-ab72-45de-bfc5-53a6237089cf
msc.legacyurl: /web-forms/overview/security/create-an-aspnet-web-forms-app-with-sms-two-factor-authentication
msc.type: authoredcontent
ms.openlocfilehash: c9558aca8a655071c0c94ed66433cf721f26c011
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/19/2020
ms.locfileid: "77466419"
---
# <a name="create-an-aspnet-web-forms-app-with-sms-two-factor-authentication-c"></a>Создание приложения веб-форм ASP.NET с двухфакторной проверкой подлинности по SMS (C#)

по [Эрик Реитан](https://github.com/Erikre)

[Скачивание приложения веб-форм ASP.NET с помощью электронной почты и двухфакторной проверки подлинности SMS](https://code.msdn.microsoft.com/ASPNET-Web-Forms-App-with-5a0ff94e)

> В этом руководстве показано, как создать приложение веб-форм ASP.NET с двухфакторной проверкой подлинности. Этот учебник был разработан для дополнения учебника с названием [Создание безопасного приложения веб-форм ASP.NET с регистрацией пользователей, подтверждением электронной почты и сбросом пароля](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset.md). Кроме того, это руководство основано на [руководстве по MVC](../../../mvc/overview/security/aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication.md)Рик Андерсон (.

## <a name="introduction"></a>Введение

В этом учебнике рассматриваются шаги, необходимые для создания приложения ASP.NET Web Forms, поддерживающего двухфакторную проверку подлинности с помощью Visual Studio. Двухфакторная проверка подлинности — это дополнительный этап аутентификации пользователя. Этот дополнительный шаг создает уникальный персональный идентификационный номер (ПИН-код) во время входа. ПИН-код обычно отправляется пользователю как сообщение электронной почты или SMS. Пользователь приложения затем вводит ПИН-код в качестве дополнительной меры проверки подлинности при входе.

### <a name="tutorial-tasks-and-information"></a>Задачи и сведения в учебнике:

- [Создание приложения веб-форм ASP.NET](#createWebForms)
- [Настройка SMS и двухфакторной проверки подлинности](#SMS)
- [Включить двухфакторную проверку подлинности для зарегистрированного пользователя](#use2FA)
- [Дополнительные ресурсы](#addRes)

<a id="createWebForms"></a>
## <a name="create-an-aspnet-web-forms-app"></a>Создание приложения веб-форм ASP.NET

Начните с установки и запуска [Visual Studio Express 2013 для Web](https://go.microsoft.com/fwlink/?LinkId=299058) или [Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566). Установите [Visual Studio 2013 обновление 3](https://go.microsoft.com/fwlink/?LinkId=390465) или более поздней версии. Кроме того, необходимо создать учетную запись [Twilio](https://www.twilio.com/try-twilio) , как описано ниже.

> [!NOTE]
> Важно. для работы с этим руководством необходимо установить [Visual Studio 2013 обновление 3](https://go.microsoft.com/fwlink/?LinkId=390465) или более поздней версии.

1. Создайте новый проект (**файл** -&gt; **Новый проект**) и выберите шаблон **веб-приложение ASP.NET** вместе с .NET Framework версией 4.5.2 в диалоговом окне **Новый проект** .
2. В диалоговом окне **Новый проект ASP.NET** выберите шаблон **веб-формы** . Оставьте проверку подлинности по умолчанию как **учетные записи отдельных пользователей**. Затем нажмите кнопку **ОК** , чтобы создать новый проект.  
    ![Диалоговое окно "Новый проект ASP.NET"](create-an-aspnet-web-forms-app-with-sms-two-factor-authentication/_static/image1.png)
3. Включите SSL (SSL) для проекта. Выполните действия, описанные в разделе **Включение SSL для проекта** статьи [учебник начало работы with Web Forms](../getting-started/getting-started-with-aspnet-45-web-forms/checkout-and-payment-with-paypal.md#SSLWebForms).
4. В Visual Studio откройте **консоль диспетчера пакетов** (**средства** -&gt; диспетчер **пакетов NuGet** -&gt; **консоли диспетчера пакетов**) и введите следующую команду:  
    `Install-Package Twilio`

<a id="SMS"></a>
## <a name="setup-sms-and-two-factor-authentication"></a>Настройка SMS и двухфакторной проверки подлинности

В этом руководстве используется Twilio, но можно использовать любой поставщик SMS.

1. Создайте учетную запись [Twilio](https://www.twilio.com/try-twilio) .
2. На вкладке **панель мониторинга** учетной записи TWILIO скопируйте **SID учетной записи** и **токен проверки подлинности.** Они будут добавлены в приложение позже.
3. На вкладке **числа** скопируйте **номер телефона** Twilio.
4. Сделайте **идентификатор безопасности учетной записи**Twilio, **токен проверки подлинности** и **номер телефона** доступными для приложения. Чтобы не усложнять, эти значения будут храниться в файле *Web. config* . При развертывании в Azure значения можно безопасно хранить в разделе **appSettings** на вкладке веб-сайт Настройка. Кроме того, при добавлении номера телефона используются только цифры.   
   Обратите внимание, что можно также добавить учетные данные SendGrid. SendGrid — это служба уведомлений по электронной почте. Дополнительные сведения о том, как включить SendGrid, см. в разделе "подключить up SendGrid" учебника [Создание безопасного приложения веб-форм ASP.NET с регистрацией пользователей, подтверждением электронной почты и сбросом пароля.](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset.md)

    [!code-xml[Main](create-an-aspnet-web-forms-app-with-sms-two-factor-authentication/samples/sample1.xml?highlight=2,6-10)]

    > [!WARNING]
    > Безопасность — никогда не храните конфиденциальные данные в исходном коде. В этом примере учетная запись и учетные данные хранятся в разделе **appSettings** файла *Web. config* . В Azure эти значения можно безопасно сохранить на вкладке **[Настройка](https://blogs.msdn.com/b/webdev/archive/2014/06/04/queuebackgroundworkitem-to-reliably-schedule-and-run-long-background-process-in-asp-net.aspx)** в портал Azure. Дополнительные сведения см. в разделе Рик Андерсон (, озаглавленном рекомендации [по развертыванию паролей и других конфиденциальных данных в ASP.NET и Azure](/aspnet/identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure).
5. Настройте класс `SmsService` в файле *App\_старт\идентитиконфиг.КС* , сделав следующие изменения выделенными желтым цветом: 

    [!code-csharp[Main](create-an-aspnet-web-forms-app-with-sms-two-factor-authentication/samples/sample2.cs?highlight=5-17)]
6. Добавьте следующие `using` операторы в начало файла *IdentityConfig.CS* : 

    [!code-csharp[Main](create-an-aspnet-web-forms-app-with-sms-two-factor-authentication/samples/sample3.cs?highlight=1-4)]
7. Обновите файл *Account/Manage. aspx* , удалив строки, выделенные желтым цветом:  

    [!code-aspx[Main](create-an-aspnet-web-forms-app-with-sms-two-factor-authentication/samples/sample4.aspx?highlight=38,53,57-60,63,66,70,73)]
8. В обработчике `Page_Load` кода программной части *Manage.aspx.CS* раскомментируйте строку кода, выделенную желтым цветом, чтобы она появилась следующим образом: 

    [!code-csharp[Main](create-an-aspnet-web-forms-app-with-sms-two-factor-authentication/samples/sample5.cs?highlight=8)]
9. В раскодировании *Account*/*TwoFactorAuthenticationSignIn.aspx.CS*обновите обработчик `Page_Load`, добавив следующий код, выделенный желтым цветом: 

    [!code-csharp[Main](create-an-aspnet-web-forms-app-with-sms-two-factor-authentication/samples/sample6.cs?highlight=3-4,13)]

   Выполнив приведенный выше код, элемент "поставщики", содержащий параметры проверки подлинности, не будет сброшен к первому значению. Это позволит пользователю успешно выбрать все параметры, которые будут использоваться при проверке подлинности, а не только первый.
10. В **Обозреватель решений**щелкните правой кнопкой мыши *Default. aspx* и выберите **задать в качестве начальной страницы**.
11. Проверив приложение, сначала создайте приложение (**Ctrl**+**SHIFT**+**B**), а затем запустите приложение (**F5**) и либо выберите **Регистрация** , чтобы создать новую учетную запись пользователя, либо выберите **Вход** , если учетная запись пользователя уже зарегистрирована.
12. Войдя в систему (как пользователь), щелкните идентификатор пользователя (адрес электронной почты) на панели навигации, чтобы открыть страницу **Управление учетной записью** (Manage. aspx).  
    ![](create-an-aspnet-web-forms-app-with-sms-two-factor-authentication/_static/image2.png)
13. На странице **Управление учетной записью** нажмите кнопку **Добавить** рядом с **номером телефона** .  
    ![](create-an-aspnet-web-forms-app-with-sms-two-factor-authentication/_static/image3.png)
14. Добавьте номер телефона, по которому вы (как пользователь) хотите получить SMS-сообщения (текстовые сообщения), и нажмите кнопку **Submit (отправить** ).   
    ![](create-an-aspnet-web-forms-app-with-sms-two-factor-authentication/_static/image4.png)  
    На этом этапе приложение будет использовать учетные данные из *файла Web. config* для связи с Twilio. Сообщение SMS (текстовое сообщение) будет отправлено на телефон, связанный с учетной записью пользователя. Чтобы убедиться, что сообщение Twilio было отправлено, просмотрите панель мониторинга Twilio.
15. Через несколько секунд Телефон, связанный с учетной записью пользователя, получит текстовое сообщение, содержащее код проверки. Введите код проверки и нажмите кнопку **Отправить**.  
     ![](create-an-aspnet-web-forms-app-with-sms-two-factor-authentication/_static/image5.png)

<a id="use2FA"></a>
## <a name="enable-two-factor-authentication-for-a-registered-user"></a>Включение двухфакторной проверки подлинности для зарегистрированного пользователя

На этом этапе вы включили двухфакторную проверку подлинности для приложения. Чтобы пользователь мог использовать двухфакторную проверку подлинности, он может просто изменить их параметры с помощью пользовательского интерфейса. 

1. В качестве пользователя приложения можно включить двухфакторную проверку подлинности для конкретной учетной записи, щелкнув идентификатор пользователя (псевдоним электронной почты) на панели навигации, чтобы отобразить страницу **Управление учетной записью** . Затем щелкните ссылку **включить** , чтобы включить двухфакторную проверку подлинности для учетной записи.![](create-an-aspnet-web-forms-app-with-sms-two-factor-authentication/_static/image6.png)
2. Выйдите из системы, а затем снова войдите в систему. Если вы включили электронную почту, можно выбрать SMS или email для двухфакторной проверки подлинности. Если вы еще не включили электронную почту, см. Руководство по [созданию безопасного приложения веб-форм ASP.NET с регистрацией пользователей, подтверждением электронной почты и сбросом пароля](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset.md).![](create-an-aspnet-web-forms-app-with-sms-two-factor-authentication/_static/image7.png)
3. Отобразится страница двухфакторной проверки подлинности, на которой можно ввести код (с помощью SMS или электронной почты).![](create-an-aspnet-web-forms-app-with-sms-two-factor-authentication/_static/image8.png)  
 Если установить флажок **Запомнить этот браузер** , вам будет исключена необходимость использовать двухфакторную проверку подлинности для входа в систему при использовании браузера и устройства, на котором установлен флажок. Если пользователи-злоумышленники не смогут получить доступ к устройству, включите двухфакторную проверку подлинности и щелкните **Запомнить этот браузер** , чтобы предоставить вам удобный доступ к паролю, сохранив строгую двухфакторную проверку подлинности для всех попыток доступа с устройств, не являющихся доверенными. Это можно сделать на любом устройстве закрытого, которые регулярно использовать.

<a id="addRes"></a>
## <a name="additional-resources"></a>Дополнительные ресурсы

- [Двухфакторная проверка подлинности с помощью SMS и электронной почты в ASP.NET Identity](../../../identity/overview/features-api/two-factor-authentication-using-sms-and-email-with-aspnet-identity.md)
- [Ссылки на ASP.NET Identity Рекомендуемые ресурсы](../../../identity/overview/getting-started/aspnet-identity-recommended-resources.md)
- [Развертывание безопасного приложения веб-форм ASP.NET с членством, OAuth и базой данных SQL на веб-сайте Azure](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-webforms-app-membership-oauth-sql-database/)
- [Серия руководств по веб-формам ASP.NET. Добавление поставщика OAuth 2,0](../getting-started/getting-started-with-aspnet-45-web-forms/checkout-and-payment-with-paypal.md#OAuthWebForms)
- [Серия руководств по веб-формам ASP.NET. Включение SSL для проекта](../getting-started/getting-started-with-aspnet-45-web-forms/checkout-and-payment-with-paypal.md#SSLWebForms)
- [Подтверждение учетной записи и восстановление пароля с ASP.NET Identity](../../../identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md)
- [Создание приложения в Facebook и подключение приложения к проекту](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md#fb)
