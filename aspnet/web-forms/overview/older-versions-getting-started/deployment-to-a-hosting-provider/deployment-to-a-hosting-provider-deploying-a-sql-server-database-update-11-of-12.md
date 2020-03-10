---
uid: web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12
title: 'Развертывание веб-приложения ASP.NET с SQL Server Compact с помощью Visual Studio или Visual Web Developer: развертывание обновления базы данных SQL Server-11 из 12 | Документация Майкрософт'
author: tdykstra
description: В этой серии учебников показано, как развернуть (опубликовать) проект веб-приложения ASP.NET, включающий базу данных SQL Server Compact, с помощью Visual Stu...
ms.author: riande
ms.date: 11/17/2011
ms.assetid: 5e2bb092-cb22-4511-ad0a-22ae12dd99b3
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12
msc.type: authoredcontent
ms.openlocfilehash: 0894c0ac24737e66b6960ef3d48aa17f78c6aa1d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78423978"
---
# <a name="deploying-an-aspnet-web-application-with-sql-server-compact-using-visual-studio-or-visual-web-developer-deploying-a-sql-server-database-update---11-of-12"></a>Развертывание веб-приложения ASP.NET с SQL Server Compact с помощью Visual Studio или Visual Web Developer: развертывание обновления базы данных SQL Server-11 из 12

от [Tom Dykstra)](https://github.com/tdykstra)

[Скачать начальный проект](https://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)

> В этой серии учебников показано, как развернуть (опубликовать) проект веб-приложения ASP.NET, включающий базу данных SQL Server Compact, с помощью Visual Studio 2012 RC или Visual Studio Express 2012 RC для Web. При установке обновления веб-публикации можно также использовать Visual Studio 2010. Введение в серию см. [в первом учебнике серии](deployment-to-a-hosting-provider-introduction-1-of-12.md).
> 
> Руководство, в котором показаны функции развертывания, появившиеся после выпуска версии-КАНДИДАТа Visual Studio 2012, демонстрирует развертывание SQL Server выпусков, отличных от SQL Server Compact, и демонстрация развертывания на веб-сайтах Windows Azure см. в разделе [ASP.NET Web Deploying using Visual Studio](../../deployment/visual-studio-web-deployment/introduction.md).

## <a name="overview"></a>Обзор

В этом руководстве показано, как развернуть обновление базы данных в полной SQL Server базе данных. Поскольку Code First Migrations выполняет всю работу по обновлению базы данных, процесс практически идентичен тому, что вы делали для SQL Server Compact в учебнике [развертывание обновления базы данных](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12.md) .

Напоминание. Если вы получаете сообщение об ошибке или что-то не работает при работе с этим руководством, обязательно ознакомьтесь со [страницей устранения неполадок](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md).

## <a name="adding-a-new-column-to-a-table"></a>Добавление нового столбца в таблицу

В этом разделе учебника вы измените базу данных и внесите соответствующие изменения в код, а затем протестируйте их в Visual Studio, чтобы подготовиться к развертыванию в тестовой и рабочей средах. Это изменение включает добавление `OfficeHours` столбца в сущность `Instructor` и отображение новых сведений на веб-странице **инструкторов** .

В проекте ContosoUniversity. DAL откройте *Instructor.CS* и добавьте следующее свойство между свойствами `HireDate` и `Courses`:

[!code-csharp[Main](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/samples/sample1.cs)]

Обновите класс инициализатора таким образом, чтобы он выполнив новый столбец с тестовыми данными. Откройте *Migrations\Configuration.CS* и замените блок кода, который начинается `var instructors = new List<Instructor>`, на следующий блок кода, включающий новый столбец:

[!code-csharp[Main](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/samples/sample2.cs)]

В проекте ContosoUniversity откройте *инструкторы. aspx* и добавьте новое поле шаблона для Office Hours непосредственно перед закрывающим тегом `</Columns>` в первом элементе управления `GridView`:

[!code-aspx[Main](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/samples/sample3.aspx)]

Создайте решение.

Откройте окно **консоли диспетчера пакетов** и выберите в качестве **проекта по умолчанию**ContosoUniversity. DAL.

Введите следующие команды:

[!code-powershell[Main](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/samples/sample4.ps1)]

Запустите приложение и выберите страницу **инструкторы** . Загрузка страницы занимает немного больше времени, чем обычно, поскольку Entity Framework повторно создает базу данных и заполняет ее тестовыми данными.

[![Instructors_page_with_office_hours](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image2.png)](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image1.png)

## <a name="deploying-the-database-update-to-the-test-environment"></a>Развертывание обновления базы данных в тестовой среде

При использовании Code First Migrations метод развертывания изменения базы данных на SQL Server аналогичен для SQL Server Compact. Однако необходимо изменить профиль публикации теста, так как он все еще настроен для миграции с SQL Server Compact на SQL Server.

Первым шагом является удаление преобразований строки подключения, созданных в предыдущем руководстве. Они больше не нужны, так как вы задаете преобразования строки подключения в профиле публикации, как это делалось перед настройкой вкладки **Пакет/Публикация SQL** для миграции на SQL Server.

Откройте файл *Web. Test. config* и удалите элемент `connectionStrings`. Единственным оставшимся преобразование в файле *Web. Test. config* является `Environment` значение в элементе `appSettings`.

Теперь можно обновить профиль публикации и опубликовать его в тестовой среде.

Откройте мастер **публикации веб-сайта** и перейдите на вкладку **профиль** .

Выберите профиль **тестовой** публикации.

Перейдите на вкладку **Параметры**.

Щелкните **включить новые улучшения публикации базы данных**.

В поле Строка подключения для **SchoolContext**введите то же значение, которое использовалось в файле преобразования *Web. Test. config* в предыдущем руководстве:

[!code-console[Main](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/samples/sample5.cmd)]

Выберите **выполнить Code First migrations (выполняется при запуске приложения)** . (В вашей версии Visual Studio этот флажок может быть помечен как **применить Code First migrations**.)

В поле Строка подключения для **DefaultConnection**введите то же значение, которое использовалось в файле преобразования *Web. Test. config* в предыдущем руководстве:

[!code-console[Main](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/samples/sample6.cmd)]

Не снимайте флажок **обновлять базу данных** .

Щелкните **Опубликовать**.

Visual Studio развертывает изменения кода в тестовой среде и открывает браузер на домашней странице университета Contoso.

Выберите страницу инструкторы.

Когда приложение запускает эту страницу, оно пытается получить доступ к базе данных. Code First Migrations проверяет, является ли база данных текущей, и обнаруживает, что последняя миграция еще не применена. Code First Migrations применяет последнюю миграцию, запускает метод `Seed`, а затем страница выполняется в обычном режиме. Вы увидите новый столбец Office Hours с заполненными данными.

[![Instructors_page_with_OfficeHours_Test](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image4.png)](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image3.png)

## <a name="deploying-the-database-update-to-the-production-environment"></a>Развертывание обновления базы данных в рабочей среде

Также необходимо изменить профиль публикации для рабочей среды. В этом случае вы удалите существующий профиль и создадите новый, импортировав обновленный файл. publishsettings. Обновленный файл будет содержать строку подключения для SQL Server базы данных по адресу Цитаниум.

Как было показано при развертывании в тестовой среде, в файле преобразования *Web. Production. config* больше не требуются преобразования строки соединения. Откройте этот файл и удалите элемент `connectionStrings`. Остальные преобразования предназначены для `Environment` значения в элементе `appSettings` и элемента `location`, который предоставляет доступ к отчетам об ошибках ELMAH.

Перед созданием нового профиля публикации для рабочей среды Скачайте обновленный файл publishsettings так же, как и ранее в учебнике [развертывание в рабочей среде](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md) . (На панели управления Цитаниум щелкните **веб-сайты**, а затем щелкните веб-сайт **contosouniversity.com** . Выберите вкладку **веб-публикация** и нажмите кнопку **скачать профиль публикации для этого веб-сайта**.) Причина заключается в том, чтобы получить строку подключения к базе данных в publishsettings-файле. Строка подключения была недоступна при первой загрузке файла, так как вы все еще используете SQL Server Compact и еще не создали базу данных SQL Server в Цитаниум.

Теперь можно обновить профиль публикации и опубликовать его в рабочей среде.

Откройте мастер **публикации веб-сайта** и перейдите на вкладку **профиль** .

Щелкните **Управление профилями**, а затем удалите рабочий профиль.

Закройте мастер **публикации веб-сайта** , чтобы сохранить это изменение.

Снова откройте мастер **публикации веб-сайта** и нажмите кнопку **Импорт**.

На вкладке **Подключение** измените **URL-адрес назначения** на соответствующее значение, если используется временный URL-адрес.

Щелкните **Далее**.

На вкладке **Параметры** щелкните **включить новые улучшения публикации базы данных**.

В раскрывающемся списке Строка подключения для **SchoolContext**выберите строку подключения цитаниум.

![Selecting_Cytanium_connection_string](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image5.png)

Выберите **выполнить миграцию Code First (выполняется при запуске приложения)** .

В раскрывающемся списке Строка подключения для **DefaultConnection**выберите строку подключения цитаниум.

Перейдите на вкладку **профиль** , щелкните **Управление профилями**и переименуйте профиль с "contosouniversity.com-веб-развертывание" на "Production".

Закройте профиль публикации, чтобы сохранить изменения, а затем откройте его снова.

Щелкните **Опубликовать**. (Для реального рабочего веб-сайта можно скопировать *приложение\_offline. htm* в рабочую среду и разместить его в папке проекта перед публикацией, а затем удалить его после завершения развертывания.)

Visual Studio развертывает изменения кода в тестовой среде и открывает браузер на домашней странице университета Contoso.

Выберите страницу инструкторы.

Code First Migrations обновляет базу данных так же, как в тестовой среде. Вы увидите новый столбец Office Hours с заполненными данными.

![Instructors_page_with_OfficeHours_Prod](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image6.png)

Обновление приложения, которое включало изменение базы данных, успешно развернуто с помощью SQL Server базы данных.

## <a name="more-information"></a>Дополнительные сведения

Эта серия руководств по развертыванию веб-приложения ASP.NET для сторонних поставщиков услуг размещения завершается. Дополнительные сведения о любом из разделов, рассмотренных в этих учебниках, см. на странице [ASP.NET Deployment (схема содержимого развертывания](https://msdn.microsoft.com/library/bb386521(v=vs.110).aspx) ) на веб-сайте MSDN.

## <a name="acknowledgements"></a>Благодарности

Я хотел бы поблагодарить следующих людей, которые внесли значительные вклады в содержание этой серии руководств:

- [Альберто ПоблаЦион, MVP &amp; MCT, Испания](https://mvp.support.microsoft.com/profile/Alberto)
- Жарод Фергюсон, MVP по разработке платформы данных США
- Харша Миттал, Microsoft
- [Кристина Олсон, Microsoft](https://blogs.iis.net/krolson/default.aspx)
- [Майк Поуп, Майкрософт](http://www.mikepope.com/blog/DisplayBlog.aspx)
- Мохит Сривастава, Microsoft
- [Раффаеле Риалди, Италия](http://www.iamraf.net/)
- [Рик Андерсон (, Microsoft](https://blogs.msdn.com/b/rickandy/)
- [Саид Хашими, Microsoft](http://sedodream.com/default.aspx)(twitter: [@sayedihashimi](http://twitter.com/sayedihashimi))
- [Скотт Hanselman](http://www.hanselman.com/blog/) (twitter: [@shanselman](http://twitter.com/shanselman))
- [Скотт Хантер, Microsoft](https://blogs.msdn.com/b/scothu/) (twitter: [@coolcsh](http://twitter.com/coolcsh))
- [Срđан Боžовиć, Сербия](http://msforge.net/blogs/zmajcek/)
- [Вишал Джоши, Microsoft](http://vishaljoshi.blogspot.com/) (twitter: [@vishalrjoshi](http://twitter.com/vishalrjoshi))

> [!div class="step-by-step"]
> [Назад](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12.md)
> [Вперед](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md)
