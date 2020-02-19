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
ms.openlocfilehash: 527b4392846e60dae0b216fdeabf21fd6618e4d7
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/19/2020
ms.locfileid: "77456742"
---
# <a name="two-factorauthentication-using-sms-and-email-with-aspnet-identity"></a>Двухфакторная проверка подлинности с помощью SMS и электронной почты с ASP.NET Identity

[Хао кунг](https://github.com/HaoK), [получения запись блога](https://github.com/rustd), [Рик Андерсон (](https://twitter.com/RickAndMSFT), [Сухас Джоши](https://github.com/suhasj)

> В этом руководстве показано, как настроить двухфакторную проверку подлинности (2FA) с помощью SMS и электронной почты.
> 
> Эта статья была написана на Рик Андерсон (([@RickAndMSFT](https://twitter.com/#!/RickAndMSFT)), получения запись блога ([@rustd](https://twitter.com/rustd)), Хао Кунг и Сухас Джоши. Пример NuGet написан в основном с помощью Хао кунг.

В этой статье рассматриваются следующие вопросы:

- [Создание примера удостоверения](#build)
- [Настройка SMS для двухфакторной проверки подлинности](#SMS)
- [Включить двухфакторную проверку подлинности](#enable2)
- [Регистрация поставщика двухфакторной проверки подлинности](#reg)
- [Объединение социальных и местных учетных записей входа](#combine)
- [Блокировка учетной записи от атак методом подбора](#lock)

<a id="build"></a>

## <a name="building-the-identity-sample"></a>Создание примера удостоверения

В этом разделе вы будете использовать NuGet для загрузки примера, с которым мы будем работать. Начните с установки и запуска [Visual Studio Express 2013 для Web](https://go.microsoft.com/fwlink/?LinkId=299058) или [Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566). Установите Visual Studio [2013 с обновлением 2](https://go.microsoft.com/fwlink/?LinkId=390521) или более поздней версии.

> [!NOTE]
> Предупреждение. для работы с этим руководством необходимо установить Visual Studio [2013 с обновлением 2](https://go.microsoft.com/fwlink/?LinkId=390521) .

1. Создайте новый ***пустой*** веб-проект ASP.NET.
2. В консоли диспетчера пакетов введите следующие команды:  
  
    `Install-Package SendGrid`  
    `Install-Package -Prerelease Microsoft.AspNet.Identity.Samples`  
  
   В этом руководстве мы будем использовать [SendGrid](http://sendgrid.com/) для отправки электронной почты и [Twilio](https://www.twilio.com/) или [аспсмс](https://www.aspsms.com/asp.net/identity/testcredits/) для SMS. Пакет `Identity.Samples` устанавливает код, с которым будет работать.
3. Настройте [проект для использования SSL](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md).
4. *Необязательно*. Следуйте инструкциям в [руководстве по подтверждению электронной почты](account-confirmation-and-password-recovery-with-aspnet-identity.md) , чтобы подключить SendGrid, а затем запустить приложение и зарегистрировать учетную запись электронной почты.
5. *Необязательно:* Удалите демонстрационный код подтверждения ссылки на электронную почту из примера (код `ViewBag.Link` в контроллере учетной записи. См. методы действий `DisplayEmail` и `ForgotPasswordConfirmation` и представления Razor).
6. *Необязательно:* Удалите код `ViewBag.Status` из контроллеров управления и учетных записей и из представлений Razor *виевс\аккаунт\верификоде.кштмл* и *виевс\манаже\верифифоненумбер.кштмл* . Кроме того, можно настроить отображение `ViewBag.Status`, чтобы проверить работу этого приложения локально, не прибегая к подключению и отправке сообщений электронной почты и SMS.

> [!NOTE]
> Предупреждение. при изменении каких-либо параметров безопасности в этом примере приложения производства должны будут подвергать аудиту безопасности, который явно вызывает внесенные изменения.

<a id="SMS"></a>

## <a name="set-up-sms-for-two-factor-authentication"></a>Настройка SMS для двухфакторной проверки подлинности

В этом учебнике приводятся инструкции по использованию Twilio или АСПСМС, но можно использовать любой другой поставщик SMS.

1. **Создание учетной записи пользователя с помощью поставщика SMS**  
  
   Создайте учетную запись [Twilio](https://www.twilio.com/try-twilio) или [аспсмс](https://www.aspsms.com/asp.net/identity/testcredits/) .
2. **Установка дополнительных пакетов или добавление ссылок на службы**  
  
   Twilio  
   В консоли диспетчера пакетов введите следующую команду.  
    `Install-Package Twilio`  
  
   АСПСМС:  
   Необходимо добавить следующую ссылку на службу:  
  
    ![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image1.png)  
  
   Адрес:  
    `https://webservice.aspsms.com/aspsmsx2.asmx?WSDL`  
  
   Пространство имен:  
    `ASPSMSX2`
3. **Определение учетных данных пользователя поставщика SMS**  
  
   Twilio  
   На вкладке **панель мониторинга** учетной записи TWILIO скопируйте **SID учетной записи** и **токен проверки подлинности**.  
  
   АСПСМС:  
   В параметрах учетной записи перейдите по адресу **Userkey** и скопируйте его вместе с автоматически определенным **паролем**.  
  
   Впоследствии эти значения будут храниться в переменных `SMSAccountIdentification` и `SMSAccountPassword`.
4. **Указание SenderID или инициатора**  
  
   Twilio  
   На вкладке **числа** скопируйте номер телефона Twilio.  
  
   АСПСМС:  
   В меню **источник разблокировки** Разблокируйте один или несколько источник или выберите буквенно-цифровой инициатор (не поддерживается всеми сетями).  
  
   Позже это значение будет храниться в переменной `SMSAccountFrom`.
5. **Передача учетных данных поставщика SMS в приложение**  
  
   Сделайте учетные данные и номер телефона отправителя доступными для приложения:

    [!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample1.cs)]

    > [!WARNING]
    > Безопасность — никогда не храните конфиденциальные данные в исходном коде. Учетная запись и учетные данные добавляются в приведенный выше код для упрощения примера. См. раздел Ivan Аттен [ASP.NET MVC: Держитесь Private Settings из системы управления версиями](http://typecastexception.com/post/2014/04/06/ASPNET-MVC-Keep-Private-Settings-Out-of-Source-Control.aspx).
6. **Реализация обмена данными с поставщиком SMS**  
  
   Настройте класс `SmsService` в файле *приложения\_старт\идентитиконфиг.КС* .  
  
   В зависимости от используемого поставщика SMS активируйте раздел **Twilio** или **аспсмс** : 

    [!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample2.cs)]
7. Запустите приложение и войдите в систему с помощью ранее зарегистрированной учетной записи.
8. Щелкните идентификатор пользователя, который активирует метод действия `Index` в контроллере `Manage`.  
  
    ![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image2.png)
9. Нажмите кнопку Добавить.  
  
    ![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image3.png)
10. Через несколько секунд будет получено текстовое сообщение с кодом проверки. Введите его и нажмите кнопку **Отправить**.  
  
    ![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image4.png)
11. В представлении "Управление" отображается номер телефона.  
  
    ![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image5.png)

### <a name="examine-the-code"></a>Анализ кода

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample3.cs?highlight=2)]

Метод действия `Index` в контроллере `Manage` устанавливает сообщение о состоянии на основе предыдущего действия и предоставляет ссылки для изменения локального пароля или добавления локальной учетной записи. Метод `Index` также отображает штат или номер телефона 2FA, внешние имена входа, 2FA включенные и запомните метод 2FA для этого браузера (см. Далее). Если щелкнуть свой идентификатор пользователя (адрес электронной почты) в заголовке окна, сообщение не передается. Щелкните **номер телефона: удалить** ссылка передает `Message=RemovePhoneSuccess` как строку запроса.  
  
`https://localhost:44300/Manage?Message=RemovePhoneSuccess`

[![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image6.png)]

Метод действия `AddPhoneNumber` отображает диалоговое окно для ввода номера телефона, который может получить SMS-сообщения.

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample4.cs)]

![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image7.png)

При нажатии кнопки **отправить код проверки** отправляется номер телефона в метод действия HTTP POST `AddPhoneNumber`.

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample5.cs?highlight=12)]

Метод `GenerateChangePhoneNumberTokenAsync` создает маркер безопасности, который будет установлен в SMS Message. Если служба SMS настроена, маркер отправляется в виде строки, &quot;код безопасности &lt;токен&gt;&quot;. `SmsService.SendAsync` метод вызывается асинхронно, приложение перенаправляется к методу действия `VerifyPhoneNumber` (который отображает следующее диалоговое окно), где можно ввести код проверки.

![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image8.png)

После ввода кода и нажатия кнопки отправить код отправляется в метод действия HTTP POST `VerifyPhoneNumber`.

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample6.cs)]

Метод `ChangePhoneNumberAsync` проверяет опубликованный код безопасности. Если код правильный, то номер телефона добавляется в поле `PhoneNumber` таблицы `AspNetUsers`. При успешном вызове вызывается метод `SignInAsync`:

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample7.cs)]

Параметр `isPersistent` задает, сохраняется ли сеанс проверки подлинности в нескольких запросах.

При изменении профиля безопасности создается новая метка безопасности, которая сохраняется в поле `SecurityStamp` таблицы *AspNetUsers* . Обратите внимание, что поле `SecurityStamp` отличается от cookie безопасности. Файл cookie безопасности не хранится в таблице `AspNetUsers` (или в другом месте в базе данных Identity). Маркер безопасности cookie является самозаверяющим с помощью [DPAPI](https://msdn.microsoft.com/library/system.security.cryptography.protecteddata.aspx) и создается с `UserId, SecurityStamp` и сроком действия.

По промежуточного слоя cookie проверяет файл cookie для каждого запроса. Метод `SecurityStampValidator` в классе `Startup` порождает базу данных и периодически проверяет метку безопасности, как указано в `validateInterval`. Это происходит каждые 30 минут (в нашем примере), если только вы не измените профиль безопасности. Интервал в 30 минут был выбран для снижения количества обращений к базе данных.

При внесении каких-либо изменений в профиль безопасности необходимо вызвать метод `SignInAsync`. При изменении профиля безопасности база данных обновляет поле `SecurityStamp` и не вызывает метод `SignInAsync`, который остается в системе *только* до следующего момента, когда конвейер OWIN не достигнет базы данных (`validateInterval`). Это можно проверить, изменив метод `SignInAsync` для немедленного возврата и задав свойству cookie `validateInterval` значение от 30 минут до 5 секунд:

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample8.cs?highlight=3)]

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample9.cs?highlight=20-21)]

С помощью приведенного выше кода можно изменить профиль безопасности (например, изменить состояние " **включен**"). при сбое метода `SecurityStampValidator.OnValidateIdentity` произойдет выход за 5 секунд. Удалите строку возврата в методе `SignInAsync`, внесите еще одно изменение профиля безопасности, и вы не будете выходить из системы. Метод `SignInAsync` создает новый файл cookie безопасности.

<a id="enable2"></a>

## <a name="enable-two-factor-authentication"></a>Включение двухфакторной проверки подлинности

В примере приложения необходимо использовать пользовательский интерфейс, чтобы включить двухфакторную проверку подлинности (2FA). Чтобы включить 2FA, щелкните свой идентификатор пользователя (псевдоним электронной почты) на панели навигации.![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image9.png)  
Щелкните Включить 2FA.![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image10.png) Выйдите из, а затем снова войдите в систему. Если вы включили электронную почту (см. [предыдущий учебник](account-confirmation-and-password-recovery-with-aspnet-identity.md)), можно выбрать SMS или email для 2FA.![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image11.png) Отобразится страница Проверка кода, где можно ввести код (с помощью SMS или электронной почты).![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image12.png) Если установить флажок **Запомнить этот браузер** , вам не потребуется использовать 2FA для входа на этот компьютер и браузер. При включении 2FA и нажатии кнопки " **Запомнить" Этот браузер** обеспечит надежную защиту 2FA от злоумышленников, пытающихся получить доступ к вашей учетной записи, если у них нет доступа к вашему компьютеру. Это можно сделать на любом частном компьютере, который вы регулярно используете. Запоминаем **этот браузер**, вы получаете дополнительную безопасность 2FA на компьютерах, которые вы не используете регулярно, и вы получаете удобный способ, чтобы не выполнять 2FA на своих компьютерах. 

<a id="reg"></a>
## <a name="how-to-register-a-two-factor-authentication-provider"></a>Регистрация поставщика двухфакторной проверки подлинности

При создании нового проекта MVC файл *IdentityConfig.CS* содержит следующий код для регистрации поставщика двухфакторной проверки подлинности:

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample10.cs?highlight=22-35)]

## <a name="add-a-phone-number-for-2fa"></a>Добавление номера телефона для 2FA

Метод действия `AddPhoneNumber` в контроллере `Manage` создает маркер безопасности и отправляет его на указанный номер телефона.

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample11.cs)]

После отправки маркера он перенаправляется к методу действия `VerifyPhoneNumber`, где можно ввести код для регистрации SMS для 2FA. SMS 2FA не используется, пока не будет проверен номер телефона.

## <a name="enabling-2fa"></a>Включение 2FA

Метод действия `EnableTFA` включает 2FA:

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample12.cs)]

Обратите внимание, что необходимо вызвать `SignInAsync`, так как параметр Enable 2FA является изменением профиля безопасности. Когда 2FA включен, пользователю потребуется использовать 2FA для входа в систему с помощью описанных ими подходов 2FA (SMS и email в примере).

Вы можете добавить дополнительных поставщиков 2FA, таких как генераторы QR-кода, или написать собственную (см. статью [Использование Google Authenticator с ASP.NET Identity](https://www.jerriepelser.com//blog/using-google-authenticator-asp-net-identity/)).

> [!NOTE]
> Коды 2FA создаются с помощью [алгоритма одноразового пароля на основе времени](http://en.wikipedia.org/wiki/Time-based_One-time_Password_Algorithm) , а коды действительны в течение шести минут. Если для ввода кода требуется более шести минут, вы получите сообщение об ошибке недопустимого кода.

<a id="combine"></a>

## <a name="combine-social-and-local-login-accounts"></a>Объединение социальных и местных учетных записей входа

Вы можете объединить локальные и социальные учетные записи, щелкнув ссылку на электронную почту. В следующей последовательности &quot;RickAndMSFT@gmail.com&quot; сначала создается как локальное имя входа, но вы можете сначала создать учетную запись в качестве социальных сетей, а затем добавить локальное имя входа.

![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image13.png)

Щелкните ссылку **Управление** . Обратите внимание на 0 внешних (социальных) имен, связанных с этой учетной записью.

![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image14.png)

Щелкните ссылку на другой журнал службы и примите запросы приложения. Две учетные записи объединены, вы сможете войти в систему с любой учетной записью. Может потребоваться, чтобы пользователи могли добавлять локальные учетные записи в случае, если служба проверки подлинности в социальных сетях не работает, или более вероятно, что они потеряют доступ к учетной записи социальных сетей.

На следующем рисунке Tom является входом в социальной сети (который можно увидеть из **внешних имен входа: 1** на странице).

![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image15.png)

Если щелкнуть " **выбрать пароль** ", вы можете добавить локальный вход в систему, связанный с той же учетной записью.

![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image16.png)

<a id="lock"></a>

## <a name="account-lockout-from-brute-force-attacks"></a>Блокировка учетной записи от атак методом подбора

Вы можете защитить учетные записи приложения от словарных атак, включив блокировку пользователей. Следующий код в методе `ApplicationUserManager Create` настраивает блокировку:

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample13.cs)]

Приведенный выше код включает блокировку только для двухфакторной проверки подлинности. Хотя можно включить блокировку для имен входа, изменив `shouldLockout` на true в методе `Login` контроллера учетной записи, мы рекомендуем не включать блокировку для входа в систему, так как это делает учетную запись уязвимой для атак [DOS](http://en.wikipedia.org/wiki/Denial-of-service_attack) . В примере кода блокировка отключена для учетной записи администратора, созданной в методе `ApplicationDbInitializer Seed`:

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample14.cs?highlight=19)]

## <a name="requiring-a-user-to-have-a-validated-email-account"></a>Требуется, чтобы пользователь имел проверенную учетную запись электронной почты

Следующий код требует, чтобы пользователь имел проверенную учетную запись электронной почты, прежде чем она сможет войти в систему:

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample15.cs?highlight=8-17)]

## <a name="how-signinmanager-checks-for-2fa-requirement"></a>Как SignInManager проверяет требования 2FA

Как локальный вход, так и журнал в социальных сетях проверяют, включена ли 2FA. Если 2FA включен, метод входа `SignInManager` возвращает `SignInStatus.RequiresVerification`, и пользователь будет перенаправлен к методу `SendCode` действия, где ему придется ввести код для завершения входа в систему. Если пользователь имеет RememberMe для локального файла cookie, `SignInManager` будет возвращать `SignInStatus.Success` и не должен проходить через 2FA.

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample16.cs?highlight=20-22)]

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample17.cs?highlight=10-11,17-18)]

В следующем коде показан метод действия `SendCode`. Создается [селектлиститем](https://msdn.microsoft.com/library/system.web.mvc.selectlistitem.aspx) со всеми МЕТОДами 2FA, включенными для пользователя. [Селектлиститем](https://msdn.microsoft.com/library/system.web.mvc.selectlistitem.aspx) передается в вспомогательный модуль [дропдовнлистфор](https://msdn.microsoft.com/library/system.web.ui.webcontrols.dropdownlist.aspx) , который позволяет пользователю выбрать подход 2FA (обычно это электронная почта и SMS).

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample18.cs)]

После того как пользователь отправляет 2FA подход, вызывается метод действия `HTTP POST SendCode`, `SignInManager` отправляется код 2FA, а пользователь перенаправляется к методу `VerifyCode` действия, где можно ввести код для завершения входа.

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample19.cs?highlight=3,13-14,18)]

## <a name="2fa-lockout"></a>Блокировка 2FA

Несмотря на то, что вы можете задать блокировку учетных записей при попытке входа в систему с использованием пароля, этот подход сделает ваше имя входа уязвимым для блокировки [DOS](http://en.wikipedia.org/wiki/Denial-of-service_attack) . Рекомендуется использовать блокировку учетных записей только с 2FA. При создании `ApplicationUserManager` в примере кода задается 2FA блокировка, а `MaxFailedAccessAttemptsBeforeLockout` — пять. Когда пользователь входит в систему (через локальную учетную запись или учетную запись социальных сетей), каждая попытка неудачной попытки на 2FA сохраняется, и при достижении максимального количества попыток пользователь блокируется в течение пяти минут (можно установить время блокировки с `DefaultAccountLockoutTimeSpan`).

<a id="addRes"></a>

## <a name="additional-resources"></a>Дополнительные ресурсы

- [ASP.NET Identity Рекомендуемые ресурсы](../getting-started/aspnet-identity-recommended-resources.md) Полный список блогов по удостоверениям, видеороликов, руководств и полезных ссылок.
- В [приложении MVC 5 с помощью входа Facebook, Twitter, LinkedIn и Google OAuth2](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md) также показано, как добавить сведения о профиле в таблицу Users.
- [ASP.NET MVC и Identity 2,0: основные сведения](http://typecastexception.com/post/2014/04/20/ASPNET-MVC-and-Identity-20-Understanding-the-Basics.aspx) по Джон аттен.
- [Подтверждение учетной записи и восстановление пароля с ASP.NET Identity](account-confirmation-and-password-recovery-with-aspnet-identity.md)
- [Введение в ASP.NET Identity](../getting-started/introduction-to-aspnet-identity.md)
- [Объявление о ВЫпуске RTM ASP.NET Identity 2.0.0](https://blogs.msdn.com/b/webdev/archive/2014/03/20/test-announcing-rtm-of-asp-net-identity-2-0-0.aspx) by получения запись блога.
- [ASP.NET Identity 2,0: Настройка проверки учетной записи и двухфакторной авторизации](http://typecastexception.com/post/2014/04/20/ASPNET-Identity-20-Setting-Up-Account-Validation-and-Two-Factor-Authorization.aspx) с помощью Джон аттен.
