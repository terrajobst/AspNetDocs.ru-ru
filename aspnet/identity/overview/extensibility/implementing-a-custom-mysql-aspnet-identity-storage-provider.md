---
uid: identity/overview/extensibility/implementing-a-custom-mysql-aspnet-identity-storage-provider
title: Реализация пользовательского поставщика хранилища ASP.NET Identity MySQL — ASP.NET 4. x
author: raquelsa
description: ASP.NET Identity — это расширяемая система, которая позволяет создать собственный поставщик хранилища и подключить его к приложению без повторной работы приложения...
ms.author: riande
ms.date: 05/22/2015
ms.assetid: 248f5fe7-39ba-40ea-ab1e-71a69b0bd649
ms.custom: seoapril2019
msc.legacyurl: /identity/overview/extensibility/implementing-a-custom-mysql-aspnet-identity-storage-provider
msc.type: authoredcontent
ms.openlocfilehash: 2f0b47d45bce82c71d1864536309f9e2ffed2d63
ms.sourcegitcommit: 88fc80e3f65aebdf61ec9414810ddbc31c543f04
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/22/2020
ms.locfileid: "76519132"
---
# <a name="implementing-a-custom-mysql-aspnet-identity-storage-provider"></a>Реализация пользовательского поставщика хранилища для поставщика хранилища MySQL в ASP.NET

[Ракуел Соарес de Алмеида](https://github.com/raquelsa), [Сухас Джоши](https://github.com/suhasj), [Tom фитзмаккен](https://github.com/tfitzmac)

> ASP.NET Identity — это расширяемая система, которая позволяет создать собственный поставщик хранилища и подключить его к приложению без повторной работы приложения. В этом разделе описывается создание поставщика хранилища MySQL для ASP.NET Identity. Общие сведения о создании пользовательских поставщиков хранилищ см. в статье [Обзор пользовательских поставщиков хранилища для ASP.NET Identity](overview-of-custom-storage-providers-for-aspnet-identity.md).
> 
> Для работы с этим руководством необходимо иметь Visual Studio 2013 с обновлением 2.
> 
> В этом руководстве рассматриваются следующие задачи:
> 
> - Покажите, как создать экземпляр базы данных MySQL в Azure.
> - В этой демонстрации показано, как использовать клиентское средство MySQL (MySQL Workbench) для создания таблиц и управления удаленной базой данных в Azure.
> - Покажите, как заменить реализацию хранилища ASP.NET Identity по умолчанию собственной реализацией в проекте приложения MVC.
> 
> Этот учебник изначально был написан Ракуел Соарес de Алмеида и Рик Андерсон (( [@RickAndMSFT](https://twitter.com/#!/RickAndMSFT) ). Пример проекта был обновлен для Identity 2,0 с помощью Сухас Джоши. Раздел был обновлен для удостоверения 2,0 на Tom Фитзмаккен.

## <a name="download-completed-project"></a>Скачать завершенный проект

По завершении работы с этим руководством у вас будет проект приложения MVC с ASP.NET Identity работать с базой данных MySQL, размещенной в Azure.

Вы можете скачать завершенный поставщик хранилища MySQL на сайте [AspNet. Identity. MySQL (GitHub)](https://github.com/aspnet/samples/tree/master/samples/aspnet/Identity/AspNet.Identity.MySQL).

## <a name="the-steps-you-will-perform"></a>Действия, которые вы будете выполнять

В этом руководстве вы:

1. Создание базы данных MySQL в Azure
2. Создание ASP.NET Identity таблиц в MySQL
3. Создание приложения MVC и его настройка для использования поставщика MySQL
4. Запуск приложения

В этом разделе не рассматривается архитектура ASP.NET Identity и решений, которые необходимо принять при реализации поставщика хранилища клиента. Дополнительные сведения см. в разделе [Обзор пользовательских поставщиков хранилища для ASP.NET Identity](overview-of-custom-storage-providers-for-aspnet-identity.md).

## <a name="review-mysql-storage-provider-classes"></a>Ознакомьтесь с классами поставщиков хранилища MySQL

Прежде чем начать процедуру создания поставщика хранилища MySQL, рассмотрим классы, составляющие поставщик хранилища. Вам понадобятся классы, управляющие операциями с базами данных и классами, которые вызываются из приложения для управления пользователями и ролями.

### <a name="storage-classes"></a>Классы хранения

- [Идентитюсер](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/IdentityUser.cs) — содержит свойства для пользователя.
- [UserStore](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/UserStore.cs) — содержит операции по добавлению, обновлению или извлечению пользователей.
- [Идентитироле](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/IdentityRole.cs) — содержит свойства для ролей.
- [Ролесторе](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/RoleStore.cs) — содержит операции по добавлению, удалению, обновлению и извлечению ролей.

### <a name="data-access-layer-classes"></a>Классы уровня доступа к данным

В этом примере классы уровня доступа к данным содержат инструкции SQL для работы с таблицами. Однако в коде может потребоваться использовать объектно-реляционное сопоставление (ORM), например Entity Framework или NHibernate. В частности, приложение может испытывать низкую производительность без использования ORM, включающего отложенную загрузку и кэширование объектов. Дополнительные сведения см. в разделе [ASP.NET Identity 2,0 без Entity Framework?](https://aspnetidentity.codeplex.com/discussions/561828)

- [Мисклдатабасе](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/MySQLDatabase.cs) — содержит подключение к базе данных MySQL и методы для выполнения операций с базой данных. Экземпляры UserStore и Ролесторе создаются с помощью экземпляра этого класса.
- [Ролетабле](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/RoleTable.cs) — содержит операции с базой данных для таблицы, в которой хранятся роли.
- [Усерклаимстабле](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/UserClaimsTable.cs) — содержит операции с базой данных для таблицы, в которой хранятся утверждения пользователей.
- [Усерлогинстабле](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/UserLoginsTable.cs) — содержит операции с базой данных для таблицы, в которой хранятся данные для входа пользователя.
- [Усерролетабле](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/UserRoleTable.cs) — содержит операции с базой данных для таблицы, в которой хранятся пользователи, которым назначены роли.
- [Усертабле](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/UserTable.cs) — содержит операции с базой данных для таблицы, в которой хранятся пользователи.

## <a name="create-a-mysql-database-instance-on-azure"></a>Создание экземпляра базы данных MySQL в Azure

1. Войдите на [портал Azure](https://manage.windowsazure.com/).
2. Щелкните **+ создать** в нижней части страницы, а затем выберите **магазин**.  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image1.png)
3. В мастере **выбора и надстройки** выберите **базу данных ClearDB MySQL** и щелкните стрелку "Далее" в нижней правой части диалогового окна.  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image2.png)
4. Используйте **бесплатный** план по умолчанию и измените **имя** на **идентитимисклдатабасе**. Выберите ближайший к вам регион, а затем щелкните стрелку "Далее".  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image3.png)
5. Установите флажок, чтобы завершить создание базы данных.  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image4.png)
6. После создания базой данных можно управлять на вкладке **НАДСТРОЙКИ** портала управления.   
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image5.png)
7. Чтобы получить сведения о подключении к базе данных, щелкните **сведения о подключении** в нижней части страницы.  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image6.png)
8. Скопируйте строку подключения, нажав кнопку "Копировать" и сохранив ее, чтобы впоследствии можно было использовать ее в приложении MVC.   
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image7.png)

## <a name="create-the-aspnet-identity-tables-in-a-mysql-database"></a>Создание ASP.NET Identity таблиц в базе данных MySQL

### <a name="install-mysql-workbench-tool-to-connect-and-manage-mysql-database"></a>Установка средства MySQL Workbench для подключения к базе данных MySQL и управления ею

1. Установка средства **MySQL Workbench** на [странице загрузок MySQL](http://dev.mysql.com/downloads/windows/installer/)
2. Запустите приложение и добавьте нажатие кнопки **мисклконнектионс +** , чтобы добавить новое подключение. Используйте данные строки подключения, скопированные из базы данных Azure MySQL, созданной ранее в этом руководстве.
3. После установления соединения откройте новую вкладку **запроса** . Вставьте команды из [мисклидентити. SQL](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/MySQLIdentity.sql) в запрос и выполните его, чтобы создать таблицы базы данных.
4. Теперь у вас есть все ASP.NET Identity необходимые таблицы, созданные в базе данных MySQL, размещенной в Azure, как показано ниже.  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image1.jpg)

## <a name="create-an-mvc-application-project-from-template-and-configure-it-to-use-mysql-provider"></a>Создание проекта приложения MVC на основе шаблона и настройка его для использования поставщика MySQL

При необходимости установите либо [Visual Studio Express 2013 для Web](https://go.microsoft.com/fwlink/?LinkId=299058) , либо [Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566) с обновлением 2.

### <a name="download-the-aspnetidentitymysql-project-from-github"></a>Скачайте проект ASP. NET. Identity. MySQL из GitHub.

1. Перейдите по URL-адресу репозитория в [AspNet. Identity. MySQL (GitHub)](https://github.com/aspnet/samples/tree/master/samples/aspnet/Identity/AspNet.Identity.MySQL/).
2. Скачайте исходный код.
3. Извлеките ZIP-файл в локальную папку.
4. Откройте решение AspNet. Identity. MySQL и создайте его.

### <a name="create-a-new-mvc-application-project-from-template"></a>Создание нового проекта приложения MVC на основе шаблона

1. Щелкните правой кнопкой мыши решение **AspNet. Identity. MySQL** и **добавьте** **Новый проект** .
2. В диалоговом окне **Добавление нового проекта** выберите в левой части элемент **Visual C#**  , а затем — **веб** - **приложение ASP.NET**. Назовите проект **идентитимисклдемо**; и нажмите кнопку ОК.  
  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image2.jpg)
3. В диалоговом окне **Новый проект ASP.NET** выберите шаблон MVC с параметрами по умолчанию (включая **учетные записи отдельных пользователей** в качестве метода проверки подлинности) и нажмите кнопку **ОК**.![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image3.jpg)
4. В обозреватель решений щелкните правой кнопкой мыши проект Идентитимисклдемо и выберите пункт **Управление пакетами NuGet**. В диалоговом окне Поиск текстового поля введите **Identity. EntityFramework**. Выберите этот пакет в списке результатов и нажмите кнопку **Удалить**. Вам будет предложено удалить пакет зависимостей EntityFramework. Нажмите кнопку Да, так как этот пакет больше не будет находиться в этом приложении.
5. Щелкните правой кнопкой мыши проект Идентитимисклдемо, выберите **Добавить**, **ссылка, решение, проекты,** выберите проект AspNet. Identity. MySQL и нажмите кнопку **ОК**.
6. В проекте Идентитимисклдемо замените все ссылки на  
    `using Microsoft.AspNet.Identity.EntityFramework;`  
   С  
     `using AspNet.Identity.MySQL;`
7. В IdentityModels.cs задайте **ApplicationDbContext** как производный от **мисклдатабасе** и включите конструктор, принимающий один параметр с именем соединения.  

    [!code-csharp[Main](implementing-a-custom-mysql-aspnet-identity-storage-provider/samples/sample1.cs)]
8. Откройте файл IdentityConfig.cs. В методе **аппликатионусерманажер. Create** замените экземпляр UserManager следующим кодом:  

    [!code-csharp[Main](implementing-a-custom-mysql-aspnet-identity-storage-provider/samples/sample2.cs)]
9. Откройте файл Web. config и замените строку DefaultConnection этой записью, заменив выделенные значения строкой подключения к базе данных MySQL, созданной на предыдущих шагах.  

    [!code-xml[Main](implementing-a-custom-mysql-aspnet-identity-storage-provider/samples/sample3.xml?highlight=2)]

## <a name="run-the-app-and-connect-to-the-mysql-db"></a>Запуск приложения и подключение к базе данных MySQL

1. Щелкните правой кнопкой мыши проект **идентитимисклдемо** и выберите **Назначить запускаемым проектом** .
2. Нажмите клавиши **CTRL + F5** , чтобы создать и запустить приложение.
3. Щелкните вкладку **Register (регистрация** ) в верхней части страницы.
4. Введите новое имя пользователя и пароль, а затем щелкните **Регистрация**.  
  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image8.png)
5. Теперь новый пользователь зарегистрирован и вошел в систему.  
  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image9.png)
6. Вернитесь к средству MySQL Workbench и изучите содержимое таблицы **идентитимисклдатабасе** . Проверьте таблицу "Пользователи" на наличие записей при регистрации новых пользователей.  
  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image10.png)

## <a name="next-steps"></a>Дальнейшие действия

Дополнительные сведения о том, как включить другие методы проверки подлинности в этом приложении, см. в статье [Создание приложения ASP.NET MVC 5 с помощью Facebook и Google OAuth2 и OpenID Connect входа](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md).

Сведения о том, как интегрировать базу данных с OAuth и настроить роли для ограничения доступа пользователей к вашему приложению, см. в статье [развертывание защищенного приложения ASP.NET MVC 5 с членством, OAuth и базой данных SQL в Azure](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data).
