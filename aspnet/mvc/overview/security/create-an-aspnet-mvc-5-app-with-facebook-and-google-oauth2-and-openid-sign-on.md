---
uid: mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on
title: Создание приложения MVC 5 с помощью Facebook, Twitter, LinkedIn и Google OAuth2 Sign-OnC#() | Документация Майкрософт
author: Rick-Anderson
description: В этом руководстве показано, как создать веб-приложение ASP.NET MVC 5, которое позволяет пользователям выполнять вход с использованием OAuth 2,0 с учетными данными из внешнего й...
ms.author: riande
ms.date: 04/03/2015
ms.assetid: 81ee500f-fc37-40d6-8722-f1b64720fbb6
msc.legacyurl: /mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on
msc.type: authoredcontent
ms.openlocfilehash: dd2e55d68ceb5a90134e394c00f3a3a231cb27d6
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457691"
---
# <a name="create-an-aspnet-mvc-5-app-with-facebook-twitter-linkedin-and-google-oauth2-sign-on-c"></a>Создание приложения ASP.NET MVC 5 с единым входом с помощью учетных данных Facebook, Twitter, LinkedIn и Google OAuth2 (C#)

по [Рик Андерсон (](https://twitter.com/RickAndMSFT)

> В этом руководстве показано, как создать веб-приложение ASP.NET MVC 5, которое позволяет пользователям входить в систему с помощью [OAuth 2,0](http://oauth.net/2/) с учетными данными от внешнего поставщика проверки подлинности, например Facebook, Twitter, LinkedIn, Microsoft или Google. Для простоты в этом учебнике рассматривается работа с учетными данными из Facebook и Google.
> 
> Включение этих учетных данных на веб-сайтах обеспечивает значительное преимущество, поскольку миллионы пользователей уже имеют учетные записи с этими внешними поставщиками. Эти пользователи могут быть более наклонными для регистрации на сайте, если им не нужно создавать и запоминать новый набор учетных данных.
> 
> См. также [приложение ASP.NET MVC 5 с использованием SMS и двухфакторной проверки подлинности по электронной почте](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication.md).
> 
> В этом учебнике также показано, как добавить данные профиля для пользователя и как использовать API членства для добавления ролей. Этот учебник написан на [Рик Андерсон (](https://blogs.msdn.com/rickAndy) (следуйте указаниям в Twitter: [@RickAndMSFT](https://twitter.com/RickAndMSFT) ).

<a id="start"></a>
## <a name="getting-started"></a>Начало работы

Начните с установки и запуска [Visual Studio Express 2013 для Web](https://go.microsoft.com/fwlink/?LinkId=299058) или [Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566). Установите Visual Studio [2013 с обновлением 3](https://go.microsoft.com/fwlink/?LinkId=390521) или более поздней версии. Дополнительные сведения о Dropbox, GitHub, LinkedIn, Instagram, buffer, Salesforce, STEAM, обмене стеками, Трипит, Твитч, Twitter, Yahoo! и др. см. в этом [образце проекта](https://github.com/matthewdunsdon/oauthforaspnet).

> [!NOTE]
> Необходимо установить Visual Studio [2013 с обновлением 3](https://go.microsoft.com/fwlink/?LinkId=390521) или более поздней версии, чтобы использовать Google OAuth 2 и локально выполнять отладку без предупреждений SSL.

Нажмите кнопку **создать проект** на **начальной** странице, либо можно воспользоваться меню, выбрать **файл**, а затем **создать проект**.

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image1.png)  

<a id="1st"></a>
## <a name="creating-your-first-application"></a>Создание первого приложения

Щелкните **создать проект**, выберите элемент **Visual C#**  слева, затем — **веб** , а затем выберите **веб-приложение ASP.NET**. Присвойте проекту имя "Мвкаус" и нажмите кнопку **ОК**.

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image2.png)

В диалоговом окне **Новый проект ASP.NET** щелкните **MVC**. Если проверка подлинности не является **отдельной учетной записью пользователя**, нажмите кнопку **изменить проверку подлинности** и выберите **отдельные учетные записи пользователей**. Проверив **размещение в облаке**, приложение будет легко размещаться в Azure.

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image3.png)

Если вы выбрали **узел в облаке**, заполните диалоговое окно настройки.

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image4.png)

### <a name="use-nuget-to-update-to-the-latest-owin-middleware"></a>Использование NuGet для обновления по промежуточного слоя OWIN

Используйте диспетчер пакетов NuGet для обновления по [промежуточного слоя OWIN](../../../aspnet/overview/owin-and-katana/getting-started-with-owin-and-katana.md). В меню слева выберите **обновления** . Можно нажать кнопку " **Обновить все** " или выполнить поиск только пакетов OWIN (показанных на следующем рисунке):

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image5.png)

На рисунке ниже показаны только пакеты OWIN:

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image6.png)

В консоли диспетчера пакетов (PMC) можно ввести команду `Update-Package`, которая будет обновлять все пакеты.

Нажмите клавишу **F5** или **CTRL + F5** , чтобы запустить приложение. На рисунке ниже показан номер порта 1234. При запуске приложения вы увидите другой номер порта.

В зависимости от размера окна браузера может потребоваться щелкнуть значок навигации, чтобы просмотреть ссылки **Домашняя страница**, **сведения о** **контакте**, **Регистрация** и **Вход** .

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image7.png)  
![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image8.png) 

<a id="ssl"></a>
## <a name="setting-up-ssl-in-the-project"></a>Настройка SSL в проекте

Для подключения к поставщикам проверки подлинности, таким как Google и Facebook, необходимо настроить IIS-Express для использования SSL. Важно использовать SSL после входа в систему, а не отменять его на HTTP, файл cookie для входа является как секретным именем пользователя и паролем, и без использования SSL вы отправляете его в виде открытого текста по каналу передачи. Кроме того, вы уже предоставили время для выполнения подтверждения и обеспечения безопасности канала (который представляет собой основную часть того, что делает HTTPS медленнее, чем HTTP) до выполнения конвейера MVC, поэтому перенаправление обратно на HTTP после входа в систему не сделает текущий запрос или будущее. запросы выполняются гораздо быстрее.

1. В **Обозреватель решений**щелкните проект **мвкаус** .
2. Нажмите клавишу F4, чтобы отобразить свойства проекта. Кроме того, в меню **вид** можно выбрать **окно свойства**.
3. Измените значение по **протоколу SSL с Enabled** на true.  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image9.png)
4. Скопируйте URL-адрес SSL (который будет `https://localhost:44300/`, если не созданы другие проекты SSL).
5. В **Обозреватель решений**щелкните правой кнопкой мыши проект **мвкаус** и выберите пункт **Свойства**.
6. Перейдите на вкладку **веб** и вставьте URL-адрес SSL в поле **URL-адрес проекта** . Сохраните файл (CTL + S). Этот URL-адрес потребуется для настройки приложений проверки подлинности Facebook и Google.  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image10.png)
7. Добавьте атрибут [RequireHttps](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx) к контроллеру `Home`, чтобы все запросы должны использовать HTTPS. Более безопасный подход заключается в добавлении фильтра [RequireHttps](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx) в приложение. См. раздел &quot;Защита приложения с помощью SSL и атрибута авторизации&quot; в моем руководстве [Создание приложения ASP.NET MVC с проверкой подлинности и базой данных SQL и развертывание в службе приложений Azure](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data). Ниже показана часть контроллера Home.

    [!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample1.cs?highlight=1)]
8. Нажмите CTRL+F5, чтобы запустить приложение. Если вы установили сертификат ранее, можно пропустить оставшуюся часть этого раздела и перейти к [созданию приложения Google для OAuth 2 и подключению приложения к проекту](#goog). в противном случае следуйте инструкциям, чтобы доверять самозаверяющий сертификат, который IIS Express создан.  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image11.png)
9. Прочтите диалоговое окно **Security Warning (предупреждение системы безопасности** ) и нажмите кнопку **Да** , если хотите установить сертификат, представляющий localhost.  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image12.png)
10. В IE откроется *Главная* страница без предупреждений SSL.  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image13.png)
11. Google Chrome также принимает сертификат и будет отображать HTTPS-содержимое без предупреждения. Firefox использует собственное хранилище сертификатов, поэтому отобразится предупреждение. Для нашего приложения можно безопасно щелкнуть **я понимаю риски**.   
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image14.png)

<a id="goog"></a>
## <a name="creating-a-google-app-for-oauth-2-and-connecting-the-app-to-the-project"></a>Создание приложения Google для OAuth 2 и подключение приложения к проекту

> [!WARNING]
> Текущие инструкции Google OAuth см. [в разделе Настройка проверки подлинности Google в ASP.NET Core](/aspnet/core/security/authentication/social/google-logins).

1. Перейдите к [Консоли разработчиков Google](https://console.developers.google.com/).
2. Если вы еще не создали проект, выберите **учетные данные** на вкладке слева и нажмите кнопку **создать**.
3. На вкладке слева щелкните **учетные данные**.
4. Щелкните **создать учетные данные** , а затем — **идентификатор клиента OAuth**. 

    1. В диалоговом окне **создать идентификатор клиента** следует использовать **веб-приложение** по умолчанию для типа приложения.
    2. Установите для **полномочных источников JavaScript** URL-адрес SSL, который вы использовали ранее (`https://localhost:44300/`, если не созданы другие проекты SSL).
    3. Задайте для подходящего **URI перенаправления** значение:  
         `https://localhost:44300/signin-google`
5. Щелкните элемент меню экрана согласия OAuth, а затем укажите адрес электронной почты и название продукта. Завершив заполнение формы, нажмите кнопку **сохранить**.
6. Щелкните пункт меню Библиотека, найдите **Google + API**, щелкните его и нажмите включить.
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image15.png)  
  
   На рисунке ниже показаны включенные интерфейсы API.  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image16.png)
7. В диспетчере API Google API посетите вкладку **учетные данные** , чтобы получить **идентификатор клиента**. Скачайте, чтобы сохранить JSON-файл с секретами приложения. Скопируйте и вставьте **ClientID** и **ClientSecret** в метод `UseGoogleAuthentication`, находящийся в файле *Startup.auth.CS* в папке *App_Start* . Значения **ClientID** и **ClientSecret** , показанные ниже, являются примерами и не работают.

    [!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample2.cs?highlight=37-39)]

    > [!WARNING]
    > Безопасность — никогда не храните конфиденциальные данные в исходном коде. Учетная запись и учетные данные добавляются в приведенный выше код для упрощения примера. См. рекомендации [по развертыванию паролей и других конфиденциальных данных в ASP.NET и службе приложений Azure](../../../identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure.md).
8. Нажмите **CTRL+F5** , чтобы построить и запустить приложение. Щелкните ссылку **Войти в систему** .  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image17.png)
9. В разделе **использовать другую службу для входа**щелкните **Google**.  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image18.png)

    > [!NOTE]
    > Если вы пропустили какие-либо из описанных выше действий, возникнет ошибка HTTP 401. Выполните приведенные выше действия. Если вы пропустили требуемый параметр (например, **Название продукта**), добавьте недостающий элемент и сохраните его. Проверка подлинности может занять несколько минут.
10. Вы будете перенаправлены на сайт Google, на который вы будете вводить свои учетные данные.   
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image19.png)
11. После ввода учетных данных появится запрос на получение разрешений для веб-приложения, которое было только что создано:
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image20.png)
12. Нажмите кнопку **Принимаю**. Теперь вы будете перенаправлены обратно на страницу **регистрации** приложения мвкаус, где можно зарегистрировать учетную запись Google. Вы можете изменить имя регистрации локального адреса электронной почты, используемое для учетной записи Gmail, но в общем случае необходимо использовать псевдоним электронной почты по умолчанию (то есть тот, который использовался для проверки подлинности). Нажмите кнопку **Зарегистрировать**.  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image21.png)

<a id="fb"></a>
## <a name="creating-the-app-in-facebook-and-connecting-the-app-to-the-project"></a>Создание приложения в Facebook и подключение приложения к проекту

> [!WARNING]
> Текущие инструкции по проверке подлинности Facebook OAuth2 см. в статье [Настройка проверки подлинности Facebook](/aspnet/core/security/authentication/social/facebook-logins) .

<a id="mdb"></a>
## <a name="examine-the-membership-data"></a>Проверка данных членства

В меню **вид** выберите пункт **Обозреватель сервера**.

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image32.png)

Разверните узел **DefaultConnection (мвкаус)** , разверните узел **таблицы**, щелкните правой кнопкой мыши элемент **AspNetUsers** и выберите команду **отобразить данные таблицы**.

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image33.png)

![данные таблицы aspnetusers](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image34.png)

<a id="ap"></a>
## <a name="adding-profile-data-to-the-user-class"></a>Добавление данных профиля в класс User

В этом разделе вы добавите дату рождения и домашний город в пользовательские данные во время регистрации, как показано на следующем рисунке.

![reg с помощью домашнего города и Бдай](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image35.png)

Откройте файл *моделс\идентитимоделс.КС* и добавьте свойства Дата рождения и домашний город:

[!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample4.cs?highlight=3-4)]

Откройте файл *моделс\аккаунтвиевмоделс.КС* и задайте свойства Дата рождения и домашний город в `ExternalLoginConfirmationViewModel`.

[!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample5.cs?highlight=8-9)]

Откройте файл *контроллерс\аккаунтконтроллер.КС* и добавьте код для даты рождения и домашнего города в метод действия `ExternalLoginConfirmation`, как показано ниже.

[!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample6.cs?highlight=21-23)]

Добавьте дату рождения и домашний город в файл *виевс\аккаунт\екстерналлогинконфирматион.кштмл* :

[!code-cshtml[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample7.cshtml?highlight=27-40)]

Удалите базу данных членства, чтобы снова зарегистрировать свою учетную запись Facebook в приложении, и убедитесь, что вы можете добавить новую дату рождения и сведения личного профиля города.

В **Обозреватель решений**щелкните значок **Показывать все файлы** , щелкните правой кнопкой мыши *добавить\_дата\аспнет-мвкаус-&lt;датестамп&gt;. mdf* и нажмите кнопку **Удалить**.

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image36.png)

В меню **Сервис** выберите **Диспетчер пакетов NuGet**, а затем щелкните **консоль диспетчера пакетов** (PMC). Введите следующие команды в PMC.

1. Включение и миграция
2. Инициализация добавления и миграции
3. Обновление базы данных

Запустите приложение и используйте FaceBook и Google для входа и регистрации некоторых пользователей.

## <a name="examine-the-membership-data"></a>Проверка данных членства

В меню **вид** выберите пункт **Обозреватель сервера**.

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image37.png)

Щелкните правой кнопкой мыши **AspNetUsers** и выберите команду " **отобразить данные таблицы**".

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image38.png)

Ниже показаны поля `HomeTown` и `BirthDate`.

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image39.png)

<a id="off"></a>
## <a name="logging-off-your-app-and-logging-in-with-another-account"></a>Выход из приложения и вход с другой учетной записью

Если вы входите в приложение с помощью Facebook, а затем выйдете из сети и попытаетесь войти еще раз с другой учетной записью Facebook (используя тот же браузер), вы сразу же войдете в предыдущую учетную запись Facebook, которую вы использовали. Чтобы использовать другую учетную запись, перейдите в Facebook и выйдите из Facebook. То же правило применяется к любому другому поставщику проверки подлинности стороннего производителя. Кроме того, можно войти в систему с другой учетной записью, используя другой браузер.

## <a name="next-steps"></a>Следующие шаги

См. статью [Знакомство с поставщиками безопасности Yahoo и LinkedIn OAuth для OWIN](http://www.jerriepelser.com/blog/introducing-the-yahoo-linkedin-oauth-security-providers-for-owin/) с помощью Джерри Пелсер для Yahoo и LinkedIn. Чтобы включить кнопки входа в социальных сетях, см. Джерри кнопки входа в систему ASP.NET MVC 5.

Следуйте указаниям [в моем руководстве создание приложения ASP.NET MVC с проверкой подлинности и базой данных SQL и развертывание в службе приложений Azure](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data), которое продолжится в этом руководстве и демонстрирует следующее:

1. Развертывание приложения в Azure.
2. Как защитить приложение с помощью ролей.
3. Как защитить приложение с помощью фильтров [RequireHttps](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute(v=vs.108).aspx) и [авторизации](https://msdn.microsoft.com/library/system.web.mvc.authorizeattribute(v=vs.100).aspx) .
4. Как использовать API членства для добавления пользователей и ролей.

Оставьте отзыв о том, как вы понравится вам в этом учебнике, и что мы можем улучшить. Вы также можете запросить новые темы [, как показано в разделе как с кодом](http://aspnet.uservoice.com/forums/228522-show-me-how-with-code). Вы можете даже попросить и проголосовать за новые функции, которые будут добавлены в ASP.NET. Например, можно проголосовать за средство для [создания пользователей и ролей и управления ими.](http://aspnet.uservoice.com/forums/41199-general-asp-net/suggestions/5646857-asp-net-identity-membership-db-tool-to-mangage-use)

Хорошее описание работы служб внешней аутентификации ASP.NET см. в статье о [внешних службах аутентификации](https://asp.net/web-api/overview/security/external-authentication-services)Роберт мкмуррай. Статья Роберт также подробно рассказывает о включении проверки подлинности Майкрософт и Twitter. Отличное [руководство по EF/MVC](../getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md) Tom Dykstra) демонстрирует работу с Entity Framework.
