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
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457600"
---
# <a name="aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication"></a>Приложение ASP.NET MVC 5 с двухфакторной проверкой подлинности по SMS и электронной почте

по [Рик Андерсон (](https://twitter.com/RickAndMSFT)

> В этом руководстве показано, как создать веб-приложение ASP.NET MVC 5 с двухфакторной проверкой подлинности. Прежде чем продолжить [, создайте безопасное веб-приложение ASP.NET MVC 5 с входом, подтверждением электронной почты и сбросом пароля](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset.md) . Готовое приложение можно скачать [здесь](https://code.msdn.microsoft.com/MVC-5-with-2FA-email-8f26d952). Загрузка содержит вспомогательные средства отладки, которые позволяют протестировать электронную почту и SMS без настройки электронной почты или поставщика SMS.
> 
> Этот учебник написан на [Рик Андерсон (](https://blogs.msdn.com/rickAndy) (Twitter: [@RickAndMSFT](https://twitter.com/RickAndMSFT) ).

- [Создание приложения ASP.NET MVC](#createMvc)
- [Настройка SMS для двухфакторной проверки подлинности](#SMS)
- [Включить двухфакторную проверку подлинности](#enable2)
- [Дополнительные ресурсы](#addRes)

<a id="createMvc"></a>
## <a name="create-an-aspnet-mvc-app"></a>Создание приложения ASP.NET MVC

Начните с установки и запуска [Visual Studio Express 2013 для Web](https://go.microsoft.com/fwlink/?LinkId=299058) или [Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566). Установите [Visual Studio 2013 обновление 3](https://go.microsoft.com/fwlink/?LinkId=390465) или более поздней версии.

> [!NOTE]
> Внимание! перед продолжением необходимо [создать безопасное веб-приложение ASP.NET MVC 5 с входом, подтверждением электронной почты и сбросом пароля](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset.md) . Для работы с этим руководством необходимо установить [Visual Studio 2013 обновление 3](https://go.microsoft.com/fwlink/?LinkId=390465) или более поздней версии.

1. Создайте новый веб-проект ASP.NET и выберите шаблон MVC. Веб-формы также поддерживают ASP.NET Identity, поэтому можно выполнять аналогичные действия в приложении Web Forms.  
    ![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image1.png)
2. Оставьте проверку подлинности по умолчанию как **учетные записи отдельных пользователей**. Если вы хотите разместить приложение в Azure, оставьте флажок установленным. Далее в этом руководстве мы будем выполнять развертывание в Azure. Вы можете [бесплатно открыть учетную запись Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).
3. Настройте [проект для использования SSL](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md).

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
  
    ![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image2.png)  
  
   Адрес:  
    `https://webservice.aspsms.com/aspsmsx2.asmx?WSDL`  
  
   Пространство имен:  
    `ASPSMSX2`
3. **Определение учетных данных пользователя поставщика SMS**  
  
   Twilio  
   На вкладке **панель мониторинга** учетной записи TWILIO скопируйте **SID учетной записи** и **токен проверки подлинности**.  
  
   АСПСМС:  
   В параметрах учетной записи перейдите по адресу **Userkey** и скопируйте его вместе с автоматически определенным **паролем**.  
  
   Позже эти значения будут храниться в файле *Web. config* в ключах `"SMSAccountIdentification"` и `"SMSAccountPassword"`.
4. **Указание SenderID или инициатора**  
  
   Twilio  
   На вкладке **числа** скопируйте номер телефона Twilio.  
  
   АСПСМС:  
   В меню **источник разблокировки** Разблокируйте один или несколько источник или выберите буквенно-цифровой инициатор (не поддерживается всеми сетями).  
  
   Позже это значение будет храниться в файле *Web. config* в рамках ключевого `"SMSAccountFrom"`.
5. **Передача учетных данных поставщика SMS в приложение**  
  
   Сделайте учетные данные и номер телефона отправителя доступными для приложения. Для простоты мы будем хранить эти значения в файле *Web. config* . При развертывании в Azure значения можно хранить безопасно в разделе **Параметры приложения** на вкладке веб-сайт Настройка. 

    [!code-xml[Main](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/samples/sample1.xml?highlight=8-10)]

    > [!WARNING]
    > Безопасность — никогда не храните конфиденциальные данные в исходном коде. Учетная запись и учетные данные добавляются в приведенный выше код для упрощения примера. См. рекомендации [по развертыванию паролей и других конфиденциальных данных в ASP.NET и Azure](../../../identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure.md).
6. **Реализация обмена данными с поставщиком SMS**  
  
   Настройте класс `SmsService` в файле *приложения\_старт\идентитиконфиг.КС* .  
  
   В зависимости от используемого поставщика SMS активируйте раздел **Twilio** или **аспсмс** : 

    [!code-csharp[Main](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/samples/sample2.cs)]
7. Обновите представление Razor *виевс\манаже\индекс.кштмл* : (Примечание. не просто удаляйте комментарии в коде выхода, используйте приведенный ниже код.)  

    [!code-cshtml[Main](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/samples/sample3.cshtml?highlight=29-66)]
8. Убедитесь, что методы действия `EnableTwoFactorAuthentication` и `DisableTwoFactorAuthentication` в `ManageController` имеют атрибут[[ValidateAntiForgeryToken]](https://msdn.microsoft.com/library/system.web.mvc.validateantiforgerytokenattribute(v=vs.118).aspx) :  

    [!code-csharp[Main](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/samples/sample4.cs?highlight=3,16)]
9. Запустите приложение и войдите в систему с помощью ранее зарегистрированной учетной записи.
10. Щелкните идентификатор пользователя, который активирует метод действия `Index` в контроллере `Manage`.  
    ![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image3.png)
11. Нажмите кнопку Добавить.  
    ![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image4.png)
12. Метод действия `AddPhoneNumber` отображает диалоговое окно для ввода номера телефона, который может получить SMS-сообщения.

    [!code-csharp[Main](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/samples/sample5.cs)]

    ![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image5.png)
13. Через несколько секунд будет получено текстовое сообщение с кодом проверки. Введите его и нажмите кнопку **Отправить**.  
    ![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image6.png)
14. В представлении "Управление" отображается номер телефона.

<a id="enable2"></a>
## <a name="enable-two-factor-authentication"></a>Включение двухфакторной проверки подлинности

В приложении, созданном шаблоном, необходимо использовать пользовательский интерфейс, чтобы включить двухфакторную проверку подлинности (2FA). Чтобы включить 2FA, щелкните свой идентификатор пользователя (псевдоним электронной почты) на панели навигации.

![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image7.png)

Щелкните Включить 2FA.

![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image8.png)

Выполните выход, а затем снова войдите в систему. Если вы включили электронную почту (см. [предыдущий учебник](../../../identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md)), можно выбрать SMS или email для 2FA.

![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image9.png)

Отобразится страница Проверка кода, где можно ввести код (с помощью SMS или электронной почты).

![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image10.png)

Если установить флажок **Запомнить этот браузер** , вам не нужно будет использовать 2FA для входа в систему при использовании браузера и устройства, на котором вы проверяли флажок. Пока пользователи-злоумышленники не смогут получить доступ к вашему устройству, что позволит 2FA и щелкнуть **Запомнить этот браузер** , вы сможете получить удобный доступ к паролю, сохранив при этом строгую защиту 2FA для доступа с устройств, не являющихся доверенными. Это можно сделать на любом устройстве закрытого, которые регулярно использовать.

В этом учебнике содержатся краткие сведения о включении 2FA в новом приложении ASP.NET MVC. Мой учебник, посвященный [двухфакторной проверке подлинности с помощью SMS и электронной почты с ASP.NET Identity](../../../identity/overview/features-api/two-factor-authentication-using-sms-and-email-with-aspnet-identity.md) , подробно расскажу о коде, выделенном в примере.

<a id="addRes"></a>
## <a name="additional-resources"></a>Дополнительные ресурсы

- [Двухфакторная проверка подлинности с помощью SMS и электронной почты с ASP.NET Identity](../../../identity/overview/features-api/two-factor-authentication-using-sms-and-email-with-aspnet-identity.md) Подробное описание двухфакторной проверки подлинности
- [Ссылки на ASP.NET Identity Рекомендуемые ресурсы](../../../identity/overview/getting-started/aspnet-identity-recommended-resources.md)
- [Подтверждение учетной записи и восстановление пароля с ASP.NET Identity](../../../identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md) Дополнительные сведения о восстановлении пароля и подтверждении учетной записи.
- [Приложение MVC 5 с входом Facebook, Twitter, LinkedIn и Google OAuth2](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md) В этом руководстве показано, как написать приложение ASP.NET MVC 5 с проверкой подлинности Facebook и Google OAuth 2. В нем также показано, как добавить дополнительные данные в базу данных удостоверений.
- [Развертывание безопасного приложения MVC ASP.NET с членством, OAuth и базой данных SQL в Azure Web](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data). В этом руководстве описывается добавление развертывания Azure, защита приложения с помощью ролей, использование API членства для добавления пользователей и ролей, а также дополнительные функции безопасности.
- [Создание приложения Google для OAuth 2 и подключение приложения к проекту](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md#goog)
- [Создание приложения в Facebook и подключение приложения к проекту](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md#fb)
- [Настройка SSL в проекте](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md#ssl)
- [Как настроить C# и ASP.NET среду разработки MVC](https://www.twilio.com/docs/usage/tutorials/how-to-set-up-your-csharp-and-asp-net-mvc-development-environment)
