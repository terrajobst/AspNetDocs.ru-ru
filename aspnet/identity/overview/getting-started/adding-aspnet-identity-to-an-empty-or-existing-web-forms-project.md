---
uid: identity/overview/getting-started/adding-aspnet-identity-to-an-empty-or-existing-web-forms-project
title: Добавление ASP.NET Identity в пустой или существующий проект Web Forms — ASP.NET 4. x
author: raquelsa
description: В этом руководстве показано, как добавить ASP.NET Identity (систему членства для ASP.NET) в приложение ASP.NET. При создании новой веб-формы или MVC...
ms.author: riande
ms.date: 01/22/2019
ms.assetid: 1cbc0ed2-5bd6-4b62-8d34-4c193dcd8b25
ms.custom: seoapril2019
msc.legacyurl: /identity/overview/getting-started/adding-aspnet-identity-to-an-empty-or-existing-web-forms-project
msc.type: authoredcontent
ms.openlocfilehash: 8e82951d57f0b8052ee3f6530a7470be7d030206
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78471978"
---
# <a name="adding-aspnet-identity-to-an-empty-or-existing-web-forms-project"></a>Добавление ASP.NET Identity в пустой или существующий проект веб-форм

> В этом руководстве показано, как добавить [ASP.NET Identity](introduction-to-aspnet-identity.md) (новую систему членства для ASP.NET) в приложение ASP.NET.
> 
> При создании нового веб-формы или проекта MVC в Visual Studio 2017 RTM с отдельными учетными записями Visual Studio установит все необходимые пакеты и добавит все необходимые классы. В этом учебнике показано, как добавить поддержку ASP.NET Identity в существующий проект Web Forms или новый пустой проект. Я буду структурировать все пакеты NuGet, которые необходимо установить, и классы, которые необходимо добавить. Мы рассмотрим пример веб-форм для регистрации новых пользователей и входа в систему, выделяя все основные интерфейсы API точки входа для управления пользователями и проверки подлинности. В этом примере будет использоваться реализация ASP.NET Identity по умолчанию для хранилища данных SQL, созданная на основе Entity Framework. В этом руководстве мы будем использовать LocalDB для базы данных SQL.
> 

## <a name="get-started-with-aspnet-identity"></a>Начало работы с ASP.NET Identity

1. Начните с установки и запуска [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/).
2. Выберите **Новый проект** на начальной странице, либо используйте меню, выберите **файл**, а затем — **Новый проект**.
3. В левой области разверните узел **визуальный C#** элемент, затем выберите **веб**, а затем — веб **-приложение ASP.NET (.NET Framework)** . Присвойте проекту имя "Вебформсидентити" и нажмите кнопку **ОК**.
  
    ![](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/_static/image17.png)
4. В диалоговом окне **Новый проект ASP.NET** выберите **пустой** шаблон.
  
    ![](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/_static/image2.png)  
  
   Обратите внимание, что кнопка **изменить проверку подлинности** отключена, и в этом шаблоне поддержка проверки подлинности не предоставляется. Шаблоны веб-форм, MVC и веб-API позволяют выбрать способ проверки подлинности.

## <a name="add-identity-packages-to-your-app"></a>Добавление пакетов удостоверений в приложение

В обозреватель решений щелкните правой кнопкой мыши проект и выберите **Управление пакетами NuGet**. Найдите и установите пакет **Microsoft. AspNet. Identity. EntityFramework** . 
  
![](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/_static/image15.png)
  
Обратите внимание, что этот пакет будет устанавливать пакеты зависимостей: **EntityFramework** и **Microsoft ASP.NET Core Identity**.

## <a name="add-a-web-form-to-register-users"></a>Добавление веб-формы для регистрации пользователей

1. В **Обозреватель решений**щелкните правой кнопкой мыши проект и выберите **Добавить**, а затем — **веб-форма**.
  
    ![](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/_static/image4.png)
2. В диалоговом окне **Указание имени для элемента** введите имя нового **регистра**веб-формы и нажмите кнопку **ОК** .
3. Замените разметку в созданном файле *Register. aspx* приведенным ниже кодом. Изменения в коде выделены. 

    [!code-html[Main](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/samples/sample1.aspx?highlight=9,12-40)]

    > [!NOTE]
    > Это просто упрощенная версия файла *Register. aspx* , создаваемая при создании нового проекта веб-форм ASP.NET. Приведенная выше разметка добавляет поля формы и кнопку для регистрации нового пользователя.
4. Откройте файл *Register.aspx.CS* и замените содержимое файла следующим кодом:

    [!code-csharp[Main](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/samples/sample2.cs)]

    > [!NOTE] 
    > 
    > 1. Приведенный выше код является упрощенной версией файла *Register.aspx.CS* , который создается при создании нового проекта веб-форм ASP.NET.
    > 2. Класс *идентитюсер* является реализацией EntityFramework по умолчанию интерфейса *IUser* . Интерфейс *IUser* является минимальным интерфейсом для пользователя ASP.NET Identity Core.
    > 3. Класс *UserStore* является реализацией EntityFramework по умолчанию для хранилища пользователей. Этот класс реализует минимальные интерфейсы ASP.NET Identity Core: *IUserStore*, *иусерлогинсторе*, *IUserClaimStore* и *IUserRoleStore*.
    > 4. Класс *UserManager* предоставляет интерфейсы API, связанные с пользователем, которые автоматически сохраняют изменения в *UserStore*.
    > 5. Класс *идентитиресулт* представляет результат операции идентификации.
5. В **Обозреватель решений**щелкните правой кнопкой мыши проект и выберите **Добавить**, **Добавить папку ASP.NET** , а затем — **\_данные приложения**.
  
    ![](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/_static/image5.png)
6. Откройте файл *Web. config* и добавьте запись строки подключения для базы данных, которая будет использоваться для хранения сведений о пользователе. База данных будет создана во время выполнения EntityFramework для сущностей Identity. Строка подключения аналогична той, которая была создана при создании нового проекта веб-форм. Выделенный код показывает разметку, которую следует добавить:

    [!code-xml[Main](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/samples/sample3.xml?highlight=11-14)]
    
    > [!NOTE] 
    > В Visual Studio 2015 или более поздней версии замените `(localdb)\v11.0` `(localdb)\MSSQLLocalDB` в строке подключения.
    
7. Щелкните правой кнопкой мыши файл *Register. aspx* в проекте и выберите **задать в качестве начальной страницы**. Нажмите клавиши CTRL + F5, чтобы создать и запустить веб-приложение. Введите новое имя пользователя и пароль, а затем нажмите кнопку **зарегистрировать**.
  
    ![](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/_static/image6.png)  

    > [!NOTE]
    > ASP.NET Identity поддерживает проверку. в этом примере можно проверить поведение по умолчанию для проверяющих элементов управления для пользователей и паролей, которые поступают из пакета удостоверений Core. Проверяющий элемент управления по умолчанию для пользователя (`UserValidator`) имеет свойство `AllowOnlyAlphanumericUserNames` со значением по умолчанию, равным `true`. Проверяющий элемент управления по умолчанию для Password (`MinimumLengthValidator`) гарантирует, что пароль содержит не менее 6 символов. Эти проверяющие элементы управления являются свойствами на `UserManager`, которые могут быть переопределены, если требуется пользовательская проверка.

## <a name="verify-the-localdb-identity-database-and-tables-generated-by-entity-framework"></a>Проверьте базу данных удостоверений LocalDb и таблицы, созданные Entity Framework

1. В меню **вид** выберите **Обозреватель сервера**.
  
    ![](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/_static/image7.png)
2. Разверните узел **DefaultConnection (вебформсидентити)** , разверните узел **таблицы**, щелкните правой кнопкой мыши элемент **AspNetUsers** , а затем выберите команду **отобразить данные таблицы**.
  
    ![](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/_static/image8.png)  
    ![](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/_static/image9.png)

## <a name="configure-the-application-for-owin-authentication"></a>Настройка приложения для проверки подлинности OWIN

На этом этапе мы добавили только поддержку для создания пользователей. Теперь мы покажем, как можно добавить проверку подлинности для входа пользователя. ASP.NET Identity использует по промежуточного слоя проверки подлинности Microsoft OWIN для проверки подлинности форм Проверка подлинности OWIN cookie — это файл cookie и механизм проверки подлинности на основе утверждений, который может использоваться любой платформой, размещенной в [OWIN](https://msdn.microsoft.com/magazine/dn451439.aspx) или IIS. В этой модели одни и те же пакеты проверки подлинности можно использовать в нескольких платформах, включая ASP.NET MVC и веб-формы. Дополнительные сведения о проекте Katana и о том, как выполнять по промежуточного слоя на узле, не зависят [от начало работы с проектом Katana](https://msdn.microsoft.com/magazine/dn451439.aspx).

## <a name="install-authentication-packages-to-your-application"></a>Установка пакетов проверки подлинности в приложение

1. В обозреватель решений щелкните правой кнопкой мыши проект и выберите **Управление пакетами NuGet**. Найдите и установите пакет ***Microsoft. AspNet. Identity. Owin*** . 
  
    ![](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/_static/image16.png)

2. Найдите и установите пакет ***Microsoft. Owin. host. SystemWeb*** .

    > [!NOTE]
    > Пакет **Microsoft. ASPNET. Identity. Owin** содержит набор классов расширений Owin для управления и настройки по промежуточного слоя проверки подлинности Owin, который будет использоваться ASP.NET Identity пакетах ядра.
    > Пакет **Microsoft. Owin. host. SystemWeb** содержит сервер Owin, который позволяет приложениям на основе Owin выполняться в IIS с помощью конвейера запросов ASP.NET. Дополнительные сведения см. [в разделе по промежуточного слоя OWIN в интегрированном конвейере IIS](../../../aspnet/overview/owin-and-katana/owin-middleware-in-the-iis-integrated-pipeline.md).

## <a name="add-owin-startup-and-authentication-configuration-classes"></a>Добавление классов конфигурации запуска и проверки подлинности OWIN

1. В **Обозреватель решений**щелкните правой кнопкой мыши проект, выберите **Добавить**, а затем **Добавить новый элемент**. В диалоговом окне Поиск текстового поля введите "*owin*". Назовите класс "*Startup*" и выберите **Добавить**. 
  
    ![](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/_static/image11.png)
2. В файле Startup.cs добавьте выделенный код, показанный ниже, чтобы настроить проверку подлинности файлов cookie OWIN.

    [!code-csharp[Main](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/samples/sample4.cs?highlight=1,3,15-19)]

    > [!NOTE]
    > Этот класс содержит атрибут `OwinStartup` для указания класса запуска OWIN. Каждое приложение OWIN имеет класс Startup, в котором указываются компоненты для конвейера приложения. Дополнительные сведения об этой модели см. в разделе [Обнаружение класса запуска OWIN](../../../aspnet/overview/owin-and-katana/owin-startup-class-detection.md) .

## <a name="add-web-forms-for-registering-and-signing-in-users"></a>Добавление веб-форм для регистрации пользователей и входа в систему

1. Откройте файл *Register.aspx.CS* и добавьте следующий код, который подписывает пользователя после того, как регистрация будет выполнена.

    [!code-csharp[Main](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/samples/sample5.cs)]

    > [!NOTE] 
    > 
    > - Так как проверка подлинности ASP.NET Identity и OWIN cookie — это система на основе утверждений, платформа требует от разработчика приложения создать [ClaimsIdentity](https://msdn.microsoft.com/library/microsoft.identitymodel.claims.claimsidentity.aspx) для пользователя. ClaimsIdentity содержит сведения обо всех утверждениях для пользователя, например о ролях, к которой принадлежит пользователь. На этом этапе можно также добавить дополнительные утверждения для пользователя.
    > - Вы можете войти в систему с помощью AuthenticationManager из OWIN и вызвать `SignIn` и передать в ClaimsIdentity, как показано выше. Этот код выполнит вход пользователя и создаст файл cookie. Этот вызов аналогичен [формаусентикатион. сетаускукие](https://msdn.microsoft.com/library/system.web.security.formsauthentication.setauthcookie.aspx) , используемому модулем [FormsAuthentication](https://msdn.microsoft.com/library/system.web.security.formsauthenticationmodule.aspx) .
2. В **Обозреватель решений**щелкните правой кнопкой мыши проект, выберите **Добавить**, а затем — **веб-форма**. Назовите имя **входа**веб-формы.
  
    ![](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/_static/image12.png)
3. Замените содержимое файла *Login. aspx* следующим кодом:

    [!code-aspx[Main](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/samples/sample6.aspx)]
4. Замените содержимое файла *Login.aspx.CS* следующим:

    [!code-csharp[Main](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/samples/sample7.cs)]

    > [!NOTE] 
    > 
    > - `Page_Load` теперь проверяет состояние текущего пользователя и выполняет действия в зависимости от состояния `Context.User.Identity.IsAuthenticated`.
    >   **Отображение имени пользователя, выполнившего вход** . платформа удостоверений Microsoft ASP.NET добавила методы расширения в [System. Security. Principal. IIdentity](https://msdn.microsoft.com/library/system.security.principal.iidentity.aspx) , что позволяет получить `UserName` и `UserId` для вошедшего в систему пользователя. Эти методы расширения определены в сборке `Microsoft.AspNet.Identity.Core`. Эти методы расширения являются заменой для [HttpContext.User.Identity.Name](https://msdn.microsoft.com/library/system.web.httpcontext.user.aspx) .
    > - Метод Signing: `This` метод заменяет предыдущий метод `CreateUser_Click` в этом примере и теперь после успешного создания пользователя выполняет вход в систему.   
    >   Платформа Microsoft OWIN Framework добавила методы расширения в `System.Web.HttpContext`, которые позволяют получить ссылку на `IOwinContext`. Эти методы расширения определены в `Microsoft.Owin.Host.SystemWeb` сборке. Класс `OwinContext` предоставляет свойство `IAuthenticationManager`, которое представляет функциональные возможности по промежуточного слоя для проверки подлинности, доступные в текущем запросе. Вы можете войти в систему с помощью `AuthenticationManager` из OWIN и вызова `SignIn` и передачи `ClaimsIdentity`, как показано выше. Так как проверка подлинности ASP.NET Identity и OWIN cookie — это система на основе утверждений, платформа требует, чтобы приложение создавало `ClaimsIdentity` для пользователя. `ClaimsIdentity` содержит сведения обо всех утверждениях для пользователя, например о ролях, к которым принадлежит пользователь. Можно также добавить дополнительные утверждения для пользователя на этом этапе. Этот код будет выполнять вход пользователя и создавать файл cookie. Этот вызов аналогичен [формаусентикатион. сетаускукие](https://msdn.microsoft.com/library/system.web.security.formsauthentication.setauthcookie.aspx) , используемому модулем [FormsAuthentication](https://msdn.microsoft.com/library/system.web.security.formsauthenticationmodule.aspx) .
    > - метод `SignOut`: получает ссылку на `AuthenticationManager` из OWIN и вызывает `SignOut`. Это аналогично методу [FormsAuthentication. Signing](https://msdn.microsoft.com/library/system.web.security.formsauthentication.signout.aspx) , используемому модулем [FormsAuthentication](https://msdn.microsoft.com/library/system.web.security.formsauthenticationmodule.aspx) .
5. Нажмите клавиши **CTRL + F5** , чтобы создать и запустить веб-приложение. Введите новое имя пользователя и пароль, а затем нажмите кнопку **зарегистрировать**.
  
    ![](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/_static/image13.png)  
   Примечание. на этом этапе новый пользователь создается и входит в систему.
6. Нажмите кнопку **выход** . Вы будете перенаправлены на форму входа.
7. Введите недопустимое имя пользователя или пароль и нажмите кнопку **Вход** . 
   Метод `UserManager.Find` вернет значение null, и появится сообщение об ошибке: " *недопустимое имя пользователя или пароль* ".
  
    ![](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/_static/image14.png)
