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
ms.openlocfilehash: 6169c972ad0f4ee2079d3638c54a5accc4b8b3de
ms.sourcegitcommit: 88fc80e3f65aebdf61ec9414810ddbc31c543f04
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/22/2020
ms.locfileid: "76519353"
---
# <a name="create-a-secure-aspnet-mvc-5-web-app-with-log-in-email-confirmation-and-password-reset-c"></a>Создание безопасного веб-приложения ASP.NET MVC 5 с входом, подтверждением электронной почты и сбросом пароля (C#)

по [Рик Андерсон (](https://twitter.com/RickAndMSFT)

В этом руководстве показано, как создать веб-приложение ASP.NET MVC 5 с подтверждением электронной почты и сбросом пароля с помощью системы членства ASP.NET Identity.

Обновленную версию этого руководства, в которой используется .NET Core, см. [в разделе Подтверждение учетной записи и восстановление пароля в ASP.NET Core](/aspnet/core/security/authentication/accconfirm).

<a id="createMvc"></a>
## <a name="create-an-aspnet-mvc-app"></a>Создание приложения ASP.NET MVC

Начните с установки и запуска [Visual Studio Express 2013 для Web](https://go.microsoft.com/fwlink/?LinkId=299058) или [Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566). Установите [Visual Studio 2013 обновление 3](https://go.microsoft.com/fwlink/?LinkId=390465) или более поздней версии.

> [!NOTE]
> Предупреждение. для работы с этим руководством необходимо установить [Visual Studio 2013 обновление 3](https://go.microsoft.com/fwlink/?LinkId=390465) или более поздней версии.

1. Создайте новый веб-проект ASP.NET и выберите шаблон MVC. Веб-формы также поддерживают ASP.NET Identity, поэтому можно выполнять аналогичные действия в приложении Web Forms.  
    ![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image1.png)
2. Оставьте проверку подлинности по умолчанию как **учетные записи отдельных пользователей**. Если вы хотите разместить приложение в Azure, оставьте флажок установленным. Далее в этом руководстве мы будем выполнять развертывание в Azure. Вы можете [бесплатно открыть учетную запись Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).
3. Настройте [проект для использования SSL](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md).
4. Запустите приложение, щелкните ссылку **Register** и зарегистрируйте пользователя. На этом этапе единственной проверкой по электронной почте является атрибут [[EmailAddress]](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.emailaddressattribute(v=vs.110).aspx) .
5. В обозреватель сервера перейдите к **Коннектионс\дефаултконнектион\таблес\аспнетусерс данных**, щелкните правой кнопкой мыши и выберите **Открыть определение таблицы**.

    На следующем рисунке показана схема `AspNetUsers`:

    ![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image2.png)
6. Щелкните правой кнопкой мыши таблицу **AspNetUsers** и выберите команду " **отобразить данные таблицы**".  
    ![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image3.png)  
 На этом этапе электронная почта не подтверждена.
7. Щелкните строку и выберите Удалить. Вы добавите это сообщение еще раз на следующем шаге и отправите сообщение электронной почты с подтверждением.

## <a name="email-confirmation"></a>Подтверждение по электронной почте

Рекомендуется подтвердить сообщение электронной почты о новой регистрации пользователя, чтобы убедиться, что они не олицетворяют кого-то другого (то есть они не зарегистрированы в электронной почте). Предположим, у вас есть дискуссионный форум, и вы хотели бы предотвратить регистрацию `"bob@example.com"` как `"joe@contoso.com"`. Без подтверждения по электронной почте `"joe@contoso.com"` может получить от приложения нежелательную почту. Предположим, что Боб случайно зарегистрировался как `"bib@example.com"` и не заметил его, он не сможет использовать восстановление пароля, так как у приложения нет нужной электронной почты. Подтверждение по электронной почте обеспечивает только ограниченную защиту от программы-роботы и не обеспечивает защиту от определенных отправителей, у них есть множество рабочих псевдонимов электронной почты, которые они могут использовать для регистрации.

Обычно требуется запретить новым пользователям отправлять данные на ваш веб-сайт, прежде чем они будут подтверждены электронной почтой, SMS-сообщением или другим механизмом. <a id="build"></a>В следующих разделах мы допустили подтверждение по электронной почте и изменим код, чтобы предотвратить вход новых зарегистрированных пользователей до подтверждения их электронной почты.

<a id="SG"></a>
## <a name="hook-up-sendgrid"></a>Подключение SendGrid

Инструкции в этом разделе не являются текущими. Обновленные инструкции см. в разделе [Configure SendGrid e-mail Provider](/aspnet/core/security/authentication/accconfirm#configure-email-provider) .

Хотя в этом учебнике показано, как добавлять уведомления по электронной почте через [SendGrid](http://sendgrid.com/), можно отправлять электронную почту с помощью SMTP и других механизмов (см. [Дополнительные ресурсы](#addRes)).

1. В консоли диспетчера пакетов введите следующую команду. 

    [!code-console[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample1.cmd)]
2. Перейдите на [страницу регистрации Azure SendGrid](https://go.microsoft.com/fwlink/?linkid=271033&clcid=0x409) и зарегистрируйтесь для бесплатной учетной записи SendGrid. Настройте SendGrid, добавив код, аналогичный приведенному ниже, в *App_Start/идентитиконфиг.КС*:

    [!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample2.cs?highlight=3,5)]

Необходимо добавить следующие ссылки:

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample3.cs)]

Чтобы не усложнять этот пример, мы будем хранить параметры приложения в файле *Web. config* :

[!code-xml[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample4.xml)]

> [!WARNING]
> Безопасность — никогда не храните конфиденциальные данные в исходном коде. Учетная запись и учетные данные хранятся в appSetting. В Azure эти значения можно безопасно сохранить на вкладке **[Настройка](https://blogs.msdn.com/b/webdev/archive/2014/06/04/queuebackgroundworkitem-to-reliably-schedule-and-run-long-background-process-in-asp-net.aspx)** в портал Azure. См. рекомендации [по развертыванию паролей и других конфиденциальных данных в ASP.NET и Azure](../../../identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure.md).

### <a name="enable-email-confirmation-in-the-account-controller"></a>Включить подтверждение электронной почты в контроллере учетной записи

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample5.cs?highlight=16-21)]

Убедитесь, что в файле *виевс\аккаунт\конфирмемаил.кштмл* правильный синтаксис Razor. (Возможно, отсутствует символ @ в первой строке. )

[!code-cshtml[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample6.cshtml?highlight=1)]

Запустите приложение и щелкните ссылку Register (регистрация). После отправки регистрационной формы вы войдете в систему.

![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image4.png)

Проверьте учетную запись электронной почты и щелкните ссылку, чтобы подтвердить свою электронную почту.

<a id="require"></a>
## <a name="require-email-confirmation-before-log-in"></a>Требовать подтверждение по электронной почте перед входом

В настоящее время, когда пользователь завершает регистрационную форму, он входит в систему. Обычно необходимо подтвердить свою электронную почту перед записью в журнал. В разделе ниже мы изменим код, чтобы требовать от новых пользователей получения подтвержденного сообщения электронной почты до входа в систему (с проверкой подлинности). Обновите метод `HttpPost Register` со следующими выделенными изменениями:

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample7.cs?highlight=14-15,23-30)]

Закомментируя метод `SignInAsync`, пользователь не будет выполнять вход с помощью регистрации. Строку `TempData["ViewBagLink"] = callbackUrl;` можно использовать для [отладки приложения](#dbg) и проверки регистрации без отправки электронной почты. `ViewBag.Message` используется для вывода инструкций Confirm. [Пример загрузки](https://code.msdn.microsoft.com/MVC-5-with-2FA-email-8f26d952) содержит код для проверки сообщения электронной почты без настройки электронной почты, а также может использоваться для отладки приложения.

Создайте файл `Views\Shared\Info.cshtml` и добавьте следующую разметку Razor:

[!code-cshtml[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample8.cshtml)]

Добавьте [атрибут авторизовать](https://msdn.microsoft.com/library/system.web.mvc.authorizeattribute(v=vs.118).aspx) в метод действия `Contact` контроллера Home. Можно щелкнуть ссылку **контакт** , чтобы проверить, что анонимные пользователи не имеют доступа и пользователи, прошедшие проверку подлинности, имеют доступ.

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample9.cs?highlight=1)]

Необходимо также обновить метод действия `HttpPost Login`.

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample10.cs?highlight=13-22)]

Обновите представление *виевс\шаред\еррор.кштмл* , чтобы отобразить сообщение об ошибке:

[!code-cshtml[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample11.cshtml?highlight=8-17)]

Удалите все учетные записи в таблице **AspNetUsers** , содержащие псевдоним электронной почты, с которым вы хотите протестировать. Запустите приложение и убедитесь, что вы не можете войти в систему, пока не подтвердите свой адрес электронной почты. После подтверждения адреса электронной почты щелкните ссылку **контакт** .

<a id="reset"></a>
## <a name="password-recoveryreset"></a>Восстановление или сброс пароля

Удалите символы комментария из метода действия `HttpPost ForgotPassword` в контроллере учетной записи:

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample12.cs?highlight=17-20)]

Удалите символы комментария из `ForgotPassword` [ActionLink](https://msdn.microsoft.com/library/system.web.mvc.html.linkextensions.actionlink(v=vs.118).aspx) в файле представления Razor *виевс\аккаунт\логин.кштмл* :

[!code-cshtml[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample13.cshtml?highlight=47-50)]

На странице входа теперь отображается ссылка для сброса пароля.

<a id="rsend"></a>
## <a name="resend-email-confirmation-link"></a>Ссылка для подтверждения повторной отправки по электронной почте

После того как пользователь создает новую локальную учетную запись, он отправляет по электронной почте ссылку на подтверждение, которую необходимо использовать, прежде чем они смогут войти в систему. Если пользователь случайно удалил сообщение электронной почты с подтверждением или сообщение не будет доставлено, ему потребуется снова отправить ссылку на подтверждение. В следующем примере кода показано, как это сделать.

Добавьте следующий вспомогательный метод в нижнюю часть файла *контроллерс\аккаунтконтроллер.КС* :

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample14.cs)]

Обновите метод Register для использования нового модуля поддержки:

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample15.cs?highlight=17)]

Обновите метод входа, чтобы повторно отправить пароль, если учетная запись пользователя не подтверждена:

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample16.cs?highlight=20)]

<a id="combine"></a>
## <a name="combine-social-and-local-login-accounts"></a>Объединение социальных и местных учетных записей входа

Вы можете объединить локальные и социальные учетные записи, щелкнув ссылку на электронную почту. В следующей последовательности **RickAndMSFT@gmail.com** сначала создается как локальное имя входа, но вы можете сначала создать учетную запись в качестве входных социальных сетей, а затем добавить локальное имя входа.

![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image5.png)

Щелкните ссылку **Управление** . Обратите внимание на **внешние имена входа: 0** , связанные с этой учетной записью.

![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image6.png)

Щелкните ссылку на другой журнал службы и примите запросы приложения. Две учетные записи объединены, вы сможете войти в систему с любой учетной записью. Может потребоваться, чтобы пользователи могли добавлять локальные учетные записи в случае, если служба проверки подлинности в социальных сетях не работает, или более вероятно, что они потеряют доступ к учетной записи социальных сетей.

На следующем рисунке Tom является входом в социальной сети (который можно увидеть из **внешних имен входа: 1** на странице).

![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image7.png)

Если щелкнуть " **выбрать пароль** ", вы можете добавить локальный вход в систему, связанный с той же учетной записью.

![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image8.png)

## <a name="email-confirmation-in-more-depth"></a>Более подробное подтверждение по электронной почте

В этом разделе содержатся дополнительные сведения о [подтверждении учетной записи учебника и восстановлении пароля с ASP.NET Identity](../../../identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md) .

<a id="dbg"></a>
## <a name="debugging-the-app"></a>Отладка приложения

Если вы не получаете электронное письмо со ссылкой:

- Проверьте папку нежелательной почты или спама.
- Войдите в учетную запись SendGrid и щелкните [ссылку действие электронной почты](https://sendgrid.com/logs/index).

Чтобы проверить ссылку проверки без сообщения электронной почты, скачайте [готовый пример](https://code.msdn.microsoft.com/MVC-5-with-2FA-email-8f26d952). На странице будут отображаться ссылки на подтверждение и коды подтверждения.

<a id="addRes"></a>
## <a name="additional-resources"></a>Дополнительные ресурсы

- [Ссылки на ASP.NET Identity Рекомендуемые ресурсы](../../../identity/overview/getting-started/aspnet-identity-recommended-resources.md)
- [Подтверждение учетной записи и восстановление пароля с ASP.NET Identity](../../../identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md) Дополнительные сведения о восстановлении пароля и подтверждении учетной записи.
- [Приложение MVC 5 с входом Facebook, Twitter, LinkedIn и Google OAuth2](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md) В этом руководстве показано, как написать приложение ASP.NET MVC 5 с проверкой подлинности Facebook и Google OAuth 2. В нем также показано, как добавить дополнительные данные в базу данных удостоверений.
- [Развертывание безопасного приложения MVC ASP.NET с членством, OAuth и базой данных SQL в Azure](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data). В этом руководстве описывается добавление развертывания Azure, защита приложения с помощью ролей, использование API членства для добавления пользователей и ролей, а также дополнительные функции безопасности.
- [Создание приложения Google для OAuth 2 и подключение приложения к проекту](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md#goog)
- [Создание приложения в Facebook и подключение приложения к проекту](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md#fb)
- [Настройка SSL в проекте](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md#ssl)
