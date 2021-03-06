---
uid: identity/overview/getting-started/developing-aspnet-apps-with-windows-azure-active-directory
title: Разработка приложений ASP.NET с помощью Azure Active Directory-ASP.NET 4. x
author: Rick-Anderson
description: Средства Microsoft ASP.NET для Azure Active Directory упрощают включение проверки подлинности для веб-приложений, размещенных в Azure. Вы можете использовать Azure й...
ms.author: riande
ms.date: 08/14/2014
ms.assetid: 457d7eaf-ee76-4ceb-9082-c7c1721435ad
ms.custom: seoapril2019
msc.legacyurl: /identity/overview/getting-started/developing-aspnet-apps-with-windows-azure-active-directory
msc.type: authoredcontent
ms.openlocfilehash: 28425ea8d1312dfc6e14df9677396f2cbcf6f16d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78471744"
---
# <a name="developing-aspnet-apps-with-azure-active-directory"></a>Разработка приложений ASP.NET с Azure Active Directory

по [Рик Андерсон (](https://twitter.com/RickAndMSFT)

Средства Microsoft ASP.NET для Azure Active Directory упрощают включение проверки подлинности для веб-приложений, размещенных в [Azure](https://www.windowsazure.com/home/features/web-sites/). Для проверки подлинности пользователей Office 365 в Организации можно использовать проверку подлинности Azure. корпоративные учетные записи синхронизируются с локальными Active Directory или пользователями, созданными в пользовательском домене Azure Active Directory. Включение проверки подлинности Windows Azure настраивает приложение для проверки подлинности пользователей с помощью одного клиента [Azure Active Directory](https://docs.microsoft.com/azure/active-directory/) .

В этом руководстве показано, как создать приложение ASP.NET, настроенное для входа с помощью [Azure Active Directory](https://msdn.microsoft.com/library/azure/mt168838.aspx) (Azure AD). Кроме того, вы узнаете, как вызвать API Graph, чтобы получить сведения о пользователе, выполнившего вход, и о том, как развернуть приложение в Azure.

## <a name="prerequisites"></a>предварительные требования

1. [Visual Studio Express 2013 для Web](https://my.visualstudio.com/Downloads?q=visual%20studio%202013#d-2013-express) или [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013).
2. Требуется [Обновление 4 для Visual Studio 2013](https://www.microsoft.com/download/details.aspx?id=44921) -обновление 3 или более поздняя версия.
3. Учетная запись Azure. [Щелкните здесь](https://azure.microsoft.com/pricing/free-trial/) , чтобы получить бесплатную пробную версию, если у вас еще нет учетной записи.

## <a name="add-a-global-administrator-to-your-active-directory"></a>Добавление глобального администратора в Active Directory

1. Выполните вход на [портал управления Azure](https://manage.windowsazure.com/).
2. Все учетные записи Azure содержат **Каталог по умолчанию** — щелкните его, а затем перейдите на вкладку **Пользователи** в верхней части страницы (см. изображение ниже).
3. Щелкните "Добавить пользователя".
    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image1.png)
4. Создайте нового пользователя с ролью **глобального администратора** . В верхнем меню щелкните **Пользователи** , а затем нажмите кнопку **Добавить пользователя** на панели команд.
5. В диалоговом окне **Добавление пользователя** введите имя нового пользователя и нажмите кнопку со стрелкой вправо.

    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image2.png)
6. Введите имя пользователя и задайте для роли значение **глобальный администратор**. Глобальным администраторам требуется альтернативный адрес электронной почты для восстановления пароля. После завершения нажмите кнопку со стрелкой вправо.

    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image3.png)
7. На следующей странице диалогового окна нажмите кнопку **создать**. Для нового пользователя будет создан временный пароль, отображаемый в диалоговом окне.

    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image4.png)

   Сохраните пароль, после первого входа в систему потребуется изменить пароль. На следующем рисунке показана новая учетная запись администратора. Для входа в приложение необходимо использовать Azure Active Directory, а не учетная запись Майкрософт, показанные на этой странице.

    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image5.png)

## <a name="create-an-aspnet-application"></a>Создание приложения ASP.NET

В следующих шагах используется [Visual Studio Express 2013 для Web](https://www.microsoft.com/download/details.aspx?id=40747)и требуется [Visual Studio 2013 обновление 3](https://www.microsoft.com/download/details.aspx?id=43721).

1. В Visual Studio щелкните **файл** , а затем — **Новый проект**. В диалоговом окне **Новый проект** выберите визуальный C# веб-проект в меню слева и нажмите кнопку **ОК**. Также можно снять флажок **добавить Application Insights в проект** , если вы не хотите использовать функциональные возможности приложения.
2. В диалоговом окне **Новый проект ASP.NET** выберите **MVC**и нажмите кнопку **изменить проверку подлинности**.

    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image6.png)
3. В диалоговом окне **Изменение проверки подлинности** выберите **учетные записи организации**. Эти параметры можно использовать для автоматической регистрации приложения в Azure AD, а также для автоматической настройки приложения для интеграции с Azure AD. Для регистрации и настройки приложения не нужно использовать диалоговое окно **изменение параметров проверки подлинности** , но оно значительно упрощает работу. Например, если вы используете Visual Studio 2012, вы по-прежнему можете вручную зарегистрировать приложение в портал управления Azure и обновить его конфигурацию для интеграции с Azure AD.
   В раскрывающихся меню выберите **облако — Единая Организация** и **единый вход, чтение данных каталога**. Введите домен для каталога Azure AD, например (на рисунке ниже) *aricka0yahoo.onmicrosoft.com*, а затем нажмите кнопку **ОК**. Доменное имя можно получить на вкладке "домены" для каталога по умолчанию на портале Azure (см. следующее изображение ниже).

    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image7.png)

   На следующем рисунке показано имя домена из портал Azure.

    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image8.png)

    > [!NOTE]
    > При необходимости можно настроить URI идентификатора приложения, который будет зарегистрирован в Azure AD, щелкнув **Дополнительные параметры**. URI идентификатора приложения — это уникальный идентификатор приложения, которое регистрируется в Azure AD и используется приложением для идентификации себя при взаимодействии с Azure AD. Дополнительные сведения об универсальном коде ресурса (URI) идентификатора приложения и других свойствах зарегистрированных приложений см. в [этом разделе](https://msdn.microsoft.com/library/azure/dn499820.aspx#BKMK_Registering). Установив флажок под полем URI идентификатора приложения, можно также переписать существующую регистрацию в Azure AD, которая использует тот же URI идентификатора приложения.
4. После нажатия кнопки **ОК**появится диалоговое окно входа, в котором потребуется выполнить вход с использованием учетной записи глобального администратора (а не учетная запись Майкрософт, связанной с вашей подпиской). Если вы ранее создали учетную запись администратора, вам потребуется изменить пароль, а затем снова войти, используя новый пароль.

    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image9.png)
5. После успешной проверки подлинности в диалоговом окне **Новый проект ASP.NET** отобразится выбранный вариант проверки подлинности (**Организация** ) и каталог, в котором будет зарегистрировано новое приложение (*aricka0yahoo.onmicrosoft.com* на рисунке ниже). Ниже этой информации установите флажок **узел в облаке**. Если этот флажок установлен, проект будет подготовлен в качестве веб-приложения Azure и будет включен для простой публикации позже. Нажмите кнопку **ОК**.

    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image10.png)
6. Откроется диалоговое окно **Настройка веб-сайта Azure** с использованием автоматически созданного имени сайта и региона. Также обратите внимание на учетную запись, которую вы вошли в диалоговом окне. Вы хотите убедиться, что эта учетная запись является той, к которой подключена подписка Azure, обычно это учетная запись Майкрософт.

    > [!NOTE]
    > Для этого проекта требуется база данных. Необходимо выбрать одну из существующих баз данных или создать новую. База данных является обязательной, поскольку проект уже использует файл локальной базы данных для хранения небольшого объема данных конфигурации проверки подлинности. При развертывании приложения на веб-сайте Azure эта база данных не упаковывается в развертывание, поэтому необходимо выбрать доступную в облаке. Нажмите кнопку **ОК**.

    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image11.png)
7. Проект будет создан, и параметры проверки подлинности и веб-приложения будут автоматически настроены в проекте. После завершения этого процесса запустите проект локально, нажав клавишу **^ F5**. Вам потребуется выполнить вход с использованием учетной записи организации. Укажите имя пользователя и пароль для созданной ранее учетной записи и нажмите кнопку **войти**.

    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image12.png)
8. После успешного входа сайт ASP.NET покажет, что вы прошли проверку подлинности, отображая имя пользователя в правом верхнем углу страницы.

    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image13.png)

   Если возникает ошибка: значение не может быть равно null или пусто. Имя параметра: linkText ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image14.png)

   Ознакомьтесь с разделом [Отладка](#dbg) в конце этого руководства.

## <a name="basics-of-the-graph-api"></a>Основные сведения о API Graph

[API Graph](https://msdn.microsoft.com/library/azure/hh974476.aspx) — это программный интерфейс, используемый для выполнения CRUD и других операций с объектами в каталоге Azure AD. Если при создании нового проекта в Visual Studio 2013 выбран вариант учетной записи организации, то приложение уже будет настроено для вызова API Graph. В этом разделе кратко показано, как работает API Graph.

1. В работающем приложении щелкните имя пользователя, выполнившего вход, в правом верхнем углу страницы. Откроется страница профиля пользователя, которая является действием на контроллере home. Вы заметите, что в таблице содержатся сведения о пользователях учетной записи администратора, созданной ранее. Эта информация хранится в каталоге и вызывается API Graph для получения этих сведений при загрузке страницы.

    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image15.png)
2. Вернитесь в Visual Studio и разверните папку **Controllers** , а затем откройте файл **HomeController.CS** . Вы увидите действие **UserProfile ()** , содержащее код для получения маркера, а затем вызовите API Graph. Этот код повторяется ниже:

    [!code-csharp[Main](developing-aspnet-apps-with-windows-azure-active-directory/samples/sample1.cs?highlight=22)]

    Чтобы вызвать API Graph, сначала необходимо получить маркер. При извлечении маркера его строковое значение должно быть добавлено в заголовок авторизации для всех последующих запросов к API Graph. Большая часть приведенного выше кода обрабатывает сведения о проверке подлинности в Azure AD для получения маркера, использования маркера для выполнения вызова API Graph, а затем преобразования ответа, чтобы его можно было представить в представлении.

    Наиболее важной частью для обсуждения является следующая выделенная строка: `UserProfile profile = JsonConvert.DeserializeObject<UserProfile>(responseString);`. Эта строка представляет имя пользователя, которое было десериализовано из ответа JSON и представлено в представлении.

    Вы можете вызвать API Graph с помощью HttpClient и самостоятельно управлять необработанными данными, но проще всего использовать [клиентскую библиотеку графа, доступную через NuGet](http://www.nuget.org/packages/Microsoft.Azure.ActiveDirectory.GraphClient/). Клиентская библиотека обрабатывает необработанные HTTP-запросы и преобразование возвращаемых данных и значительно упрощает работу с API Graph в среде .NET. См. соответствующие примеры кода API Graph на сайте [GitHub.](https://github.com/AzureADSamples)

## <a name="deploy-the-application-to-azure"></a>Развертывание приложения в Azure

В следующих шагах показано, как развернуть приложение в Azure. На предыдущих шагах вы подключились к новому проекту с помощью веб-приложения в Azure, поэтому все готово к публикации всего за несколько шагов.

1. В Visual Studio щелкните проект правой кнопкой мыши и выберите **опубликовать**. Появится диалоговое окно **Публикация веб-сайта** , где каждый параметр уже настроен. Нажмите кнопку **Далее** , чтобы открыть страницу **Параметры** . Может появиться запрос на проверку подлинности; Убедитесь, что вы выполняете проверку подлинности с помощью учетной записи подписки Azure (обычно это учетная запись Майкрософт), а не учетной записи организации, созданной ранее.

    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image16.png)
2. Установите флажок " **включить проверку подлинности в Организации** ". В поле **домен** введите домен для каталога. В раскрывающемся списке **уровень доступа** выберите **единый вход и чтение данных каталога**. Вы заметите, что предыдущая используемая база данных уже заполнена в разделе **базы данных** . Щелкните **Опубликовать**.

    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image17.png)
3. Visual Studio начнет развертывание веб-сайта, после чего появится новое окно браузера. Возможно, вам будет предложено снова пройти проверку подлинности в каталоге. После проверки подлинности вы будете перенаправлены на новый опубликованный веб-сайт в Azure.

    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image18.png)

<a id="dbg"></a>
## <a name="debugging-the-app"></a>Отладка приложения

Если возникнет следующая ошибка: значение не может быть null или пустым. Имя параметра: linkText

![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image19.png)

Замените код в файле *Views\Shared\\_LoginPartial. cshtml* следующим кодом:

[!code-cshtml[Main](developing-aspnet-apps-with-windows-azure-active-directory/samples/sample2.cshtml?highlight=1-8,15-16)]

После запуска приложения, если вошедший в систему пользователь отображает "null User", выйдите из системы и снова войдите с помощью учетной записи Active Directory, созданной ранее.

Отличная рекомендация, которую следует выполнить, — это Раинэй [веб-сайты Azure и аутентификация Организации с помощью Azure AD](http://rickrainey.com/2014/08/19/deep-dive-azure-websites-and-organizational-authentication-using-azure-ad/).

## <a name="more-information"></a>Дополнительные сведения

- [Подробный обзор: веб-сайты Azure и аутентификация в Организации с помощью Azure AD](http://rickrainey.com/2014/08/19/deep-dive-azure-websites-and-organizational-authentication-using-azure-ad/)
- [Обзор API Graph Azure AD](https://msdn.microsoft.com/library/azure/hh974476.aspx)
- [Сценарии проверки подлинности в Azure AD](https://msdn.microsoft.com/library/azure/dn499820.aspx)
- [Примеры кода Azure AD на сайте GitHub](https://github.com/AzureADSamples)
