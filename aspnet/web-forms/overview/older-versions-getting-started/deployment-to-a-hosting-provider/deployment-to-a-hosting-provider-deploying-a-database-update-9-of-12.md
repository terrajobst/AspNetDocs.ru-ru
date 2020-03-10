---
uid: web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12
title: 'Развертывание веб-приложения ASP.NET с SQL Server Compact с помощью Visual Studio или Visual Web Developer: развертывание обновления базы данных-9 из 12 | Документация Майкрософт'
author: tdykstra
description: В этой серии учебников показано, как развернуть (опубликовать) проект веб-приложения ASP.NET, включающий базу данных SQL Server Compact, с помощью Visual Stu...
ms.author: riande
ms.date: 11/17/2011
ms.assetid: a8d776af-4735-4612-87f6-9f326587f2d3
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12
msc.type: authoredcontent
ms.openlocfilehash: 3385e1019d9e7a9263fd9513c39b25eb85febbb5
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78455106"
---
# <a name="deploying-an-aspnet-web-application-with-sql-server-compact-using-visual-studio-or-visual-web-developer-deploying-a-database-update---9-of-12"></a>Развертывание веб-приложения ASP.NET с SQL Server Compact с помощью Visual Studio или Visual Web Developer: развертывание обновления базы данных-9 из 12

от [Tom Dykstra)](https://github.com/tdykstra)

[Скачать начальный проект](https://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)

> В этой серии учебников показано, как развернуть (опубликовать) проект веб-приложения ASP.NET, включающий базу данных SQL Server Compact, с помощью Visual Studio 2012 RC или Visual Studio Express 2012 RC для Web. При установке обновления веб-публикации можно также использовать Visual Studio 2010. Введение в серию см. [в первом учебнике серии](deployment-to-a-hosting-provider-introduction-1-of-12.md).
> 
> Руководство, в котором показаны функции развертывания, появившиеся после выпуска версии-КАНДИДАТа Visual Studio 2012, демонстрирует развертывание SQL Server выпусков, отличных от SQL Server Compact, и демонстрация развертывания в веб-приложениях службы приложений Azure см. в разделе [ASP.NET Web Deploying using Visual Studio](../../deployment/visual-studio-web-deployment/introduction.md).

## <a name="overview"></a>Обзор

В этом руководстве вы вносите изменения в базу данных и связанную с ней изменения кода, тестируете изменения в Visual Studio, а затем развертываете обновление в тестовой и рабочей средах.

Напоминание. Если вы получаете сообщение об ошибке или что-то не работает при работе с этим руководством, обязательно ознакомьтесь со [страницей устранения неполадок](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md).

## <a name="adding-a-new-column-to-a-table"></a>Добавление нового столбца в таблицу

В этом разделе вы добавите столбец даты рождения в базовый класс `Person` для сущностей `Student` и `Instructor`. Затем вы обновите страницу, на которой отображаются данные о преподавателе, чтобы отобразить новый столбец.

В проекте *ContosoUniversity. DAL* откройте *Person.CS* и добавьте следующее свойство в конце класса `Person` (после него должны быть две закрывающие фигурные скобки):

[!code-csharp[Main](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/samples/sample1.cs)]

Затем обновите метод SEED, чтобы он выдает значение для нового столбца. Откройте *Migrations\Configuration.CS* и замените блок кода, который начинается `var instructors = new List<Instructor>`, на следующий блок кода, содержащий сведения о дате рождения:

[!code-csharp[Main](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/samples/sample2.cs)]

В проекте ContosoUniversity откройте *инструкторы. aspx* и добавьте новое поле шаблона, чтобы отобразить дату рождения. Добавьте его между ними для даты найма и назначения Office:

[!code-aspx[Main](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/samples/sample3.aspx)]

(Если отступы кода не синхронизированы, можно нажать сочетание клавиш CTRL-K и CTRL-D, чтобы автоматически переформатировать файл.)

Выполните сборку решения, а затем откройте окно **консоли диспетчера пакетов** . Убедитесь, что ContosoUniversity. DAL по-прежнему выбран в качестве **проекта по умолчанию**.

В окне **консоли диспетчера пакетов** выберите **ContosoUniversity. DAL** в качестве **проекта по умолчанию**, а затем введите следующую команду:

[!code-powershell[Main](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/samples/sample4.ps1)]

По завершении этой команды Visual Studio открывает файл класса, который определяет новый класс `DbMigration`, а в методе `Up` можно увидеть код, создающий новый столбец.

![AddBirthDate_migration_code](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image1.png)

Выполните сборку решения, а затем введите следующую команду в окне **консоли диспетчера пакетов** (убедитесь, что проект CONTOSOUNIVERSITY. DAL по-прежнему выбран):

[!code-powershell[Main](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/samples/sample5.ps1)]

По завершении выполнения команды запустите приложение и выберите страницу инструкторы. Когда страница загрузится, вы увидите, что в ней есть новое поле даты рождения.

[![Instructors_page_with_birth_date](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image3.png)](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image2.png)

## <a name="deploying-the-database-update-to-the-test-environment"></a>Развертывание обновления базы данных в тестовой среде

В **Обозреватель решений** выберите проект ContosoUniversity.

На панели инструментов **веб-публикация одним щелчком** выберите профиль **тестовой** публикации и щелкните **Опубликовать веб-сайт**. (Если панель инструментов отключена, выберите проект ContosoUniversity в **Обозреватель решений**.)

Visual Studio развертывает обновленное приложение, и браузер открывается на домашней странице. Запустите страницу инструкторы, чтобы убедиться, что обновление успешно развернуто. Когда приложение пытается получить доступ к базе данных для этой страницы, Code First обновляет схему базы данных и выполняет метод `Seed`. При отображении страницы отображается столбец ожидаемая **Дата рождения** с датами в нем.

[![Instructors_page_with_birth_date_Test](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image5.png)](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image4.png)

## <a name="deploying-the-database-update-to-the-production-environment"></a>Развертывание обновления базы данных в рабочей среде

Теперь можно выполнить развертывание в рабочей среде. Единственное отличие заключается в том, что вы будете использовать *приложение\_offline. htm* , чтобы запретить пользователям доступ к сайту и тем самым обновить базу данных при развертывании изменений. Для рабочего развертывания выполните следующие действия.

- Отправьте *приложение\_автономный htm* -файл на рабочий сайт.
- В Visual Studio выберите рабочий профиль на панели инструментов **веб-публикация одним щелчком** и щелкните **Опубликовать веб-сайт**.
- Удалите *приложение\_автономный htm* -файл с рабочего сайта.

> [!NOTE]
> Хотя приложение используется в рабочей среде, необходимо реализовать план резервного копирования. То есть следует периодически копировать файлы *счул-прод. sdf* и *АСПнет-прод. sdf* с рабочего сайта в безопасное место хранения, и вы должны поддерживать несколько поколений таких резервных копий. При обновлении базы данных необходимо создать резервную копию непосредственно перед изменением. Если вы сделаете ошибку и не обнаружите ее до тех пор, пока вы не развернете ее в рабочую среду, то сможете восстановить базу данных до состояния, в котором она находилась до повреждения.

Когда Visual Studio откроет URL-адрес домашней страницы в браузере, отобразится страница *приложение\_автономно. htm* . После удаления *приложения\_автономном htm* -файле можно снова перейти на домашнюю страницу, чтобы убедиться, что обновление успешно развернуто.

[![Instructors_page_with_birth_date_Prod](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image7.png)](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image6.png)

Теперь вы развернули обновление приложения, которое включало изменение базы данных в тестовую и рабочую среду. В следующем руководстве показано, как перенести базу данных из SQL Server Compact в SQL Server Express и SQL Server.

> [!div class="step-by-step"]
> [Назад](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12.md)
> [Вперед](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12.md)
