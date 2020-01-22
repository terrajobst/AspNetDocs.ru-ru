---
uid: identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity
title: Подтверждение учетной записи & восстановления пароля —C#ASP.NET Identity () — ASP.NET 4. x
author: HaoK
description: Перед выполнением этого учебника сначала необходимо создать безопасное веб-приложение ASP.NET MVC 5 с входом, подтверждением электронной почты и сбросом пароля. Этот учебник...
ms.author: riande
ms.date: 01/23/2019
ms.assetid: 8d54180d-f826-4df7-b503-7debf5ed9fb3
ms.custom: seoapril2019
msc.legacyurl: /identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity
msc.type: authoredcontent
ms.openlocfilehash: 4b2c88280df39aa81d60f9508910e8fe5d6db6b8
ms.sourcegitcommit: 88fc80e3f65aebdf61ec9414810ddbc31c543f04
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/22/2020
ms.locfileid: "76519119"
---
# <a name="account-confirmation-and-password-recovery-with-aspnet-identity-c"></a>Подтверждение учетной записи и восстановление пароля сC#помощью ASP.NET Identity ()

> Перед выполнением этого учебника сначала необходимо [создать безопасное веб-приложение ASP.NET MVC 5 с входом, подтверждением электронной почты и сбросом пароля](../../../mvc/overview/security/create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset.md). В этом учебнике содержатся дополнительные сведения, а также показано, как настроить адрес электронной почты для подтверждения локальной учетной записи и разрешить пользователям сбрасывать забытый пароль в ASP.NET Identity.

Учетная запись локального пользователя требует от пользователя создания пароля для учетной записи, а также сохранения (безопасного) пароля в веб-приложении. ASP.NET Identity также поддерживает учетные записи социальных сетей, не требующие от пользователя создания пароля для приложения. [Учетные записи социальных сетей](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md) используют третью сторону (например, Google, Twitter, Facebook или Microsoft) для проверки подлинности пользователей. В этой статье рассматриваются следующие вопросы:

- [Создание приложения ASP.NET MVC](#createMvc) и изучение ASP.NET Identity функций.
- [Создание примера удостоверения](#build)
- [Настройка подтверждения по электронной почте](#email)

Новые пользователи регистрируют свой псевдоним электронной почты, который создает локальную учетную запись.

![](account-confirmation-and-password-recovery-with-aspnet-identity/_static/image1.png)

При нажатии кнопки зарегистрировать в адрес электронной почты будет отправлено сообщение с подтверждением, содержащее маркер проверки.

![](account-confirmation-and-password-recovery-with-aspnet-identity/_static/image2.png)

Пользователь отправил сообщение с маркером подтверждения для своей учетной записи.

![](account-confirmation-and-password-recovery-with-aspnet-identity/_static/image3.png)

Выбор ссылки подтверждает учетную запись.

![](account-confirmation-and-password-recovery-with-aspnet-identity/_static/image4.png)

<a id="passwordReset"></a>

## <a name="password-recoveryreset"></a>Восстановление или сброс пароля

Локальные пользователи, которые забыли свой пароль, могут иметь маркер безопасности, отправленный в свою учетную запись электронной почты, что позволит им сбросить пароль.  
  
![](account-confirmation-and-password-recovery-with-aspnet-identity/_static/image5.png)  
  
Вскоре пользователь получит сообщение электронной почты со ссылкой, позволяющим сбросить пароль.  
  
![](account-confirmation-and-password-recovery-with-aspnet-identity/_static/image6.png)  
При выборе ссылки они перемещаются на страницу сброса.  
  
![](account-confirmation-and-password-recovery-with-aspnet-identity/_static/image7.png)  
  
При нажатии кнопки **Reset (Сброс** ) будет подтверждено, что пароль был сброшен.  
  
![](account-confirmation-and-password-recovery-with-aspnet-identity/_static/image8.png)

<a id="createMvc"></a>

## <a name="create-an-aspnet-web-app"></a>Создание веб-приложения ASP.NET

Начните с установки и запуска [Visual Studio 2017](https://visualstudio.microsoft.com/).

1. Создайте новый веб-проект ASP.NET и выберите шаблон MVC. Веб-формы также поддерживают ASP.NET Identity, поэтому можно выполнять аналогичные действия в приложении Web Forms.
2. Измените проверку подлинности для **отдельных учетных записей пользователей**.
3. Запустите приложение, выберите ссылку **Register** и зарегистрируйте пользователя. На этом этапе единственной проверкой по электронной почте является атрибут [[EmailAddress]](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.emailaddressattribute(v=vs.110).aspx) .
4. В обозреватель сервера перейдите к **Коннектионс\дефаултконнектион\таблес\аспнетусерс данных**, щелкните правой кнопкой мыши и выберите **Открыть определение таблицы**.

    На следующем рисунке показана схема `AspNetUsers`:

    ![](account-confirmation-and-password-recovery-with-aspnet-identity/_static/image9.png)
5. Щелкните правой кнопкой мыши таблицу **AspNetUsers** и выберите команду " **отобразить данные таблицы**".  
  
    ![](account-confirmation-and-password-recovery-with-aspnet-identity/_static/image10.png)  
  
   На этом этапе электронная почта не подтверждена.

Хранилище данных по умолчанию для ASP.NET Identity Entity Framework, но его можно настроить для использования других хранилищ данных и добавления дополнительных полей. См. раздел [Дополнительные ресурсы](#addRes) в конце этого руководства.

[Класс запуска OWIN](../../../aspnet/overview/owin-and-katana/owin-startup-class-detection.md) ( *Startup.CS* ) вызывается при запуске приложения и вызывает метод `ConfigureAuth` в *приложении\_старт\стартуп.АУС.КС*, который настраивает конвейер OWIN и инициализирует ASP.NET Identity. Проверьте метод `ConfigureAuth`. Каждый вызов `CreatePerOwinContext` регистрирует обратный вызов (сохраненный в `OwinContext`), который будет вызываться один раз для каждого запроса, чтобы создать экземпляр указанного типа. Можно задать точку останова в конструкторе и `Create` метод каждого типа (`ApplicationDbContext, ApplicationUserManager`) и убедиться, что они вызываются при каждом запросе. Экземпляр `ApplicationDbContext` и `ApplicationUserManager` хранится в контексте OWIN, к которому можно получить доступ в рамках всего приложения. ASP.NET Identity подключается к конвейеру OWIN через по промежуточного слоя cookie. Дополнительные сведения см. [в разделе Управление жизненным циклом запроса для класса UserManager в ASP.NET Identity](https://blogs.msdn.com/b/webdev/archive/2014/02/12/per-request-lifetime-management-for-usermanager-class-in-asp-net-identity.aspx).

При изменении профиля безопасности создается новая метка безопасности, которая сохраняется в поле `SecurityStamp` таблицы *AspNetUsers* . Обратите внимание, что поле `SecurityStamp` отличается от cookie безопасности. Файл cookie безопасности не хранится в таблице `AspNetUsers` (или в другом месте в базе данных Identity). Маркер безопасности cookie является самозаверяющим с помощью [DPAPI](https://msdn.microsoft.com/library/system.security.cryptography.protecteddata.aspx) и создается с `UserId, SecurityStamp` и сроком действия.

По промежуточного слоя cookie проверяет файл cookie для каждого запроса. Метод `SecurityStampValidator` в классе `Startup` порождает базу данных и периодически проверяет метку безопасности, как указано в `validateInterval`. Это происходит каждые 30 минут (в нашем примере), если только вы не измените профиль безопасности. Интервал в 30 минут был выбран для снижения количества обращений к базе данных. Дополнительные сведения см. в [руководстве по двухфакторной проверке подлинности](index.md) .

В соответствии с комментариями в коде метод `UseCookieAuthentication` поддерживает проверку подлинности файлов cookie. Поле `SecurityStamp` и связанный код предоставляют дополнительный уровень безопасности для приложения. при смене пароля вы будете выходить из браузера, выполнившего вход. Метод `SecurityStampValidator.OnValidateIdentity` позволяет приложению проверять маркер безопасности при входе пользователя в систему, который используется при смене пароля или использовании внешнего имени входа. Это необходимо для того, чтобы все токены (файлы cookie), созданные с помощью старого пароля, стали недействительными. Если в примере проекта изменить пароль пользователя, то все предыдущие токены станут недействительными и `SecurityStamp` обновится.

Система удостоверений позволяет настроить приложение, чтобы при изменении профиля безопасности пользователей (например, при изменении пользователем пароля или изменении связанного имени входа (например, из Facebook, Google, учетная запись Майкрософт и т. д.) пользователь вышел из системы. экземпляры браузера. Например, на рисунке ниже показан пример приложения [единого выхода](https://github.com/aspnet/samples/tree/master/samples/aspnet/Identity/SingleSignOutSample) , который позволяет пользователю выйти из всех экземпляров браузера (в данном случае это Internet Explorer, Firefox и Chrome), нажав одну из кнопок. Кроме того, образец позволяет выйти только из определенного экземпляра браузера.

![](account-confirmation-and-password-recovery-with-aspnet-identity/_static/image11.png)

В [примере приложения единого выхода](https://github.com/aspnet/samples/tree/master/samples/aspnet/Identity/SingleSignOutSample) показано, как ASP.NET Identity позволяет повторно создать маркер безопасности. Это необходимо для того, чтобы все токены (файлы cookie), созданные с помощью старого пароля, стали недействительными. Эта функция обеспечивает дополнительный уровень безопасности для приложения. При изменении пароля будет выполнен выход из этого приложения.

Файл *\_Старт\идентитиконфиг.КС приложения* содержит классы `ApplicationUserManager`, `EmailService` и `SmsService`. Классы `EmailService` и `SmsService` реализуют интерфейс `IIdentityMessageService`, поэтому в каждом классе есть общие методы для настройки электронной почты и SMS. Хотя в этом учебнике показано, как добавлять уведомления по электронной почте через [SendGrid](http://sendgrid.com/), можно отправлять электронную почту с помощью SMTP и других механизмов.

Класс `Startup` также содержит форму стереотипного для добавления социальных сетей (Facebook, Twitter и т. д.), см. раздел мое [приложение MVC 5 с входом Facebook, Twitter, LinkedIn и Google OAuth2](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md) для получения дополнительных сведений.

Изучите класс `ApplicationUserManager`, который содержит сведения об удостоверениях пользователей, и настраивает следующие компоненты.

- Требования к надежности пароля.
- Блокировка пользователя (число попыток и время).
- Двухфакторная проверка подлинности (2FA). Я расскажу о 2FA и SMS в другом учебнике.
- Подключение электронной почты и служб SMS. (Я расскажу о SMS в другом руководстве).

Класс `ApplicationUserManager` является производным от класса универсального `UserManager<ApplicationUser>`. `ApplicationUser` является производным от [идентитюсер](https://msdn.microsoft.com/library/microsoft.aspnet.identity.entityframework.identityuser.aspx). `IdentityUser` является производным от класса универсального `IdentityUser`:

[!code-csharp[Main](account-confirmation-and-password-recovery-with-aspnet-identity/samples/sample1.cs)]

Указанные выше свойства совпадают со свойствами в таблице `AspNetUsers`, показанной выше.

Универсальные аргументы в `IUser` позволяют создавать производный класс, используя различные типы для первичного ключа. См. пример [чанжепк](https://github.com/aspnet/samples/tree/master/samples/aspnet/Identity/ChangePK) , в котором показано, как изменить первичный ключ с String на int или GUID.

### <a name="applicationuser"></a>ApplicationUser

`ApplicationUser` (`public class ApplicationUserManager : UserManager<ApplicationUser>`) определяется в *моделс\идентитимоделс.КС* как:

[!code-csharp[Main](account-confirmation-and-password-recovery-with-aspnet-identity/samples/sample2.cs?highlight=8-9)]

Выделенный выше код создает [ClaimsIdentity](https://msdn.microsoft.com/library/system.security.claims.claimsidentity.aspx). Проверка подлинности ASP.NET Identity и OWIN cookie основана на заявках, поэтому платформа требует, чтобы приложение создавало `ClaimsIdentity` для пользователя. `ClaimsIdentity` содержит сведения обо всех утверждениях для пользователя, например имя пользователя, возраст и роли, к которым он принадлежит. На этом этапе можно также добавить дополнительные утверждения для пользователя.

Метод `AuthenticationManager.SignIn` OWIN передает `ClaimsIdentity` и выполняет вход в систему пользователя:

[!code-csharp[Main](account-confirmation-and-password-recovery-with-aspnet-identity/samples/sample3.cs?highlight=4-6)]

[Приложение MVC 5 с входом Facebook, Twitter, LinkedIn и Google OAuth2](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md) . здесь показано, как можно добавить дополнительные свойства в класс `ApplicationUser`.

## <a name="email-confirmation"></a>Подтверждение по электронной почте

Рекомендуется подтвердить, что сообщение электронной почты зарегистрировано новым пользователем, чтобы убедиться, что он не олицетворяет другого пользователя (то есть не зарегистрировался в сообщении электронной почты). Предположим, у вас есть дискуссионный форум, и вы хотели бы предотвратить регистрацию `"bob@example.com"` как `"joe@contoso.com"`. Без подтверждения по электронной почте `"joe@contoso.com"` может получить от приложения нежелательную почту. Предположим, что Боб случайно зарегистрировался как `"bib@example.com"` и не заметил его, он не сможет использовать восстановление пароля, так как у приложения нет нужной электронной почты. Подтверждение по электронной почте обеспечивает только ограниченную защиту от программы-роботы и не обеспечивает защиту от определенных отправителей, у них есть множество рабочих псевдонимов электронной почты, которые они могут использовать для регистрации. В приведенном ниже примере пользователь не сможет изменить пароль, пока учетная запись не будет подтверждена (они выбирают ссылку подтверждения, полученную на учетной записи электронной почты, которая зарегистрирована в). Этот рабочий процесс можно применить к другим сценариям, например отправить ссылку на подтверждение и сбросить пароль для новых учетных записей, созданных администратором, отправив пользователю сообщение электронной почты, когда они изменили свой профиль и т. д. Обычно требуется запретить новым пользователям отправлять данные на ваш веб-сайт, прежде чем они будут подтверждены электронной почтой, SMS-сообщением или другим механизмом. <a id="build"></a>

## <a name="build-a-more-complete-sample"></a>Создание более полного примера

В этом разделе вы будете использовать NuGet для загрузки более полного примера, с которым мы будем работать.

1. Создайте новый ***пустой*** веб-проект ASP.NET.
2. В консоли диспетчера пакетов введите следующие команды: 

    [!code-console[Main](account-confirmation-and-password-recovery-with-aspnet-identity/samples/sample4.cmd)]

   В этом руководстве мы будем использовать [SendGrid](http://sendgrid.com/) для отправки электронной почты. Пакет `Identity.Samples` устанавливает код, с которым будет работать.
3. Настройте [проект для использования SSL](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md).
4. Протестируйте создание локальной учетной записи, запустив приложение, щелкнув ссылку **Register (регистрация** ) и отправляя форму регистрации.
5. Щелкните ссылку демонстрационная электронная почта, которая имитирует подтверждение по электронной почте.
6. Удалите демонстрационный код подтверждения ссылки на электронную почту из примера (код `ViewBag.Link` в контроллере учетной записи. См. методы действий `DisplayEmail` и `ForgotPasswordConfirmation` и представления Razor).

> [!WARNING]
> Если вы измените какие-либо параметры безопасности в этом примере, приложения производства должны будут подвергать аудиту безопасности, который явно вызывает внесенные изменения.

## <a name="examine-the-code-in-app_startidentityconfigcs"></a>Изучите код в приложении\_Старт\идентитиконфиг.КС

В этом примере показано, как создать учетную запись и добавить ее к роли *администратора* . Необходимо заменить электронное письмо в примере на адрес электронной почты, который будет использоваться для учетной записи администратора. Самый простой способ создать учетную запись администратора — программно в методе `Seed`. Мы надеемся, что в будущем есть средство, которое позволит создавать и администрировать пользователей и роли. Пример кода позволяет создавать пользователей и роли и управлять ими, но сначала необходимо иметь учетную запись администратора для запуска ролей и страниц администрирования пользователей. В этом примере учетная запись администратора создается при заполнении базы данных.

Измените пароль и измените имя на учетную запись, в которой можно получать уведомления по электронной почте.

> [!WARNING]
> Безопасность — никогда не храните конфиденциальные данные в исходном коде.

Как упоминалось ранее, `app.CreatePerOwinContext` вызов в классе Startup добавляет обратные вызовы в метод `Create` в классах содержимого базы данных приложения, диспетчера пользователей и диспетчеров ролей. Конвейер OWIN вызывает метод `Create` для этих классов для каждого запроса и сохраняет контекст для каждого класса. Контроллер учетной записи предоставляет диспетчер пользователей из контекста HTTP (который содержит контекст OWIN):

[!code-csharp[Main](account-confirmation-and-password-recovery-with-aspnet-identity/samples/sample5.cs)]

Когда пользователь регистрирует локальную учетную запись, вызывается метод `HTTP Post Register`:

[!code-csharp[Main](account-confirmation-and-password-recovery-with-aspnet-identity/samples/sample6.cs)]

Приведенный выше код использует данные модели для создания новой учетной записи пользователя с помощью введенного адреса электронной почты и пароля. Если псевдоним электронной почты находится в хранилище данных, создание учетной записи завершается сбоем, и форма снова отображается. Метод `GenerateEmailConfirmationTokenAsync` создает токен безопасного подтверждения и сохраняет его в хранилище данных ASP.NET Identity. Метод [URL. Action](https://msdn.microsoft.com/library/dd505232(v=vs.118).aspx) создает ссылку, содержащую `UserId` и токен подтверждения. Затем эта ссылка отправляется пользователю по электронной почте. пользователь может выбрать ссылку в своем приложении для подтверждения своей учетной записи.

<a id="email"></a>

## <a name="set-up-email-confirmation"></a>Настройка подтверждения по электронной почте

Перейдите на [страницу регистрации Azure SendGrid](https://azure.microsoft.com/gallery/store/sendgrid/sendgrid-azure/) и зарегистрируйтесь для бесплатной учетной записи. Добавьте код, аналогичный приведенному ниже, чтобы настроить SendGrid:

[!code-csharp[Main](account-confirmation-and-password-recovery-with-aspnet-identity/samples/sample7.cs?highlight=5)]

> [!NOTE]
> Почтовые клиенты часто принимают только текстовые сообщения (без HTML). Сообщение должно быть предоставлено в виде текста и HTML. В приведенном выше примере SendGrid это выполняется с помощью приведенного выше кода `myMessage.Text` и `myMessage.Html`.

В следующем коде показано, как отправить сообщение электронной почты с помощью класса [MailMessage](https://msdn.microsoft.com/library/system.net.mail.mailmessage.aspx) , где `message.Body` возвращает только ссылку.

[!code-csharp[Main](account-confirmation-and-password-recovery-with-aspnet-identity/samples/sample8.cs)]

> [!WARNING]
> Безопасность — никогда не храните конфиденциальные данные в исходном коде. Учетная запись и учетные данные хранятся в appSetting. В Azure эти значения можно безопасно сохранить на вкладке **[Настройка](https://blogs.msdn.com/b/webdev/archive/2014/06/04/queuebackgroundworkitem-to-reliably-schedule-and-run-long-background-process-in-asp-net.aspx)** в портал Azure. См. рекомендации [по развертыванию паролей и других конфиденциальных данных в ASP.NET и Azure](best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure.md).

Введите учетные данные SendGrid, запустите приложение, зарегистрируйтесь с помощью псевдонима электронной почты, чтобы выбрать ссылку подтвердить в сообщении электронной почты. Чтобы узнать, как это сделать с помощью учетной записи электронной почты [Outlook.com](http://outlook.com) , ознакомьтесь с разделом [ C# Настройка SMTP в Джон аттен для узла Outlook.com SMTP](http://typecastexception.com/post/2013/12/20/C-SMTP-Configuration-for-OutlookCom-SMTP-Host.aspx) и его[ASP.NET Identity 2,0: Настройка проверки учетной записи и записей двухфакторной авторизации](http://typecastexception.com/post/2014/04/20/ASPNET-Identity-20-Setting-Up-Account-Validation-and-Two-Factor-Authorization.aspx) .

После того как пользователь нажмет кнопку **Register (зарегистрировать** ), на свой адрес электронной почты отправляется сообщение с подтверждением, содержащее маркер проверки.

![](account-confirmation-and-password-recovery-with-aspnet-identity/_static/image12.png)

Пользователь отправил сообщение с маркером подтверждения для своей учетной записи.

![](account-confirmation-and-password-recovery-with-aspnet-identity/_static/image13.png)

## <a name="examine-the-code"></a>Изучение кода

В следующем примере кода показан метод `POST ForgotPassword`.

[!code-csharp[Main](account-confirmation-and-password-recovery-with-aspnet-identity/samples/sample9.cs)]

Метод завершается со сбоем автоматически, если адрес электронной почты пользователя не подтвержден. Если для недействительного адреса электронной почты была отправлена ошибка, пользователи-злоумышленники могут использовать эти сведения для поиска действительного идентификатора пользователя (псевдонимов электронной почты) для атаки.

В следующем коде показан метод `ConfirmEmail` в контроллере учетной записи, который вызывается, когда пользователь выбирает ссылку подтверждения в отправленном сообщении электронной почты:

[!code-csharp[Main](account-confirmation-and-password-recovery-with-aspnet-identity/samples/sample10.cs)]

После использования маркера забытого пароля он стал недействительным. Следующий код изменяется в методе `Create` (в файле *приложения\_старт\идентитиконфиг.КС* ) задает срок действия токенов в 3 часа.

[!code-csharp[Main](account-confirmation-and-password-recovery-with-aspnet-identity/samples/sample11.cs?highlight=6-8)]

В приведенном выше коде срок действия забытого пароля и маркеров подтверждения по электронной почте истечет через 3 часа. `TokenLifespan` по умолчанию — один день.

В следующем коде показан метод подтверждения по электронной почте:

[!code-csharp[Main](account-confirmation-and-password-recovery-with-aspnet-identity/samples/sample12.cs)]

 Чтобы сделать приложение более безопасным, ASP.NET Identity поддерживает двухфакторную проверку подлинности (2FA). См. [ASP.NET Identity 2,0: Настройка проверки учетной записи и Двухфакторная авторизация](http://typecastexception.com/post/2014/04/20/ASPNET-Identity-20-Setting-Up-Account-Validation-and-Two-Factor-Authorization.aspx) с помощью Джон аттен. Несмотря на то, что вы можете задать блокировку учетных записей при попытке входа в систему с использованием пароля, этот подход сделает ваше имя входа уязвимым для блокировки [DOS](http://en.wikipedia.org/wiki/Denial-of-service_attack) . Рекомендуется использовать блокировку учетных записей только с 2FA.  
<a id="addRes"></a>

## <a name="additional-resources"></a>Дополнительные ресурсы

- [Обзор пользовательских поставщиков хранилищ для ASP.NET Identity](../extensibility/overview-of-custom-storage-providers-for-aspnet-identity.md)
- В [приложении MVC 5 с помощью входа Facebook, Twitter, LinkedIn и Google OAuth2](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md) также показано, как добавить сведения о профиле в таблицу Users.
- [ASP.NET MVC и Identity 2,0: основные сведения](http://typecastexception.com/post/2014/04/20/ASPNET-MVC-and-Identity-20-Understanding-the-Basics.aspx) по Джон аттен.
- [Введение в ASP.NET Identity](../getting-started/introduction-to-aspnet-identity.md)
- [Объявление о ВЫпуске RTM ASP.NET Identity 2.0.0](https://blogs.msdn.com/b/webdev/archive/2014/03/20/test-announcing-rtm-of-asp-net-identity-2-0-0.aspx) by получения запись блога.
