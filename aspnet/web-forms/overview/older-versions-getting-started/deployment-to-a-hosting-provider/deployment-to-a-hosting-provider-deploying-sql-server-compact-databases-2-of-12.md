---
uid: web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12
title: 'Развертывание веб-приложения ASP.NET с SQL Server Compact с помощью Visual Studio или Visual Web Developer: развертывание баз данных SQL Server Compact-2 из 12 | Документация Майкрософт'
author: tdykstra
description: В этой серии учебников показано, как развернуть (опубликовать) проект веб-приложения ASP.NET, включающий базу данных SQL Server Compact, с помощью Visual Stu...
ms.author: riande
ms.date: 11/17/2011
ms.assetid: c3c76516-4c48-4153-bd03-d70e3a3edbb0
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12
msc.type: authoredcontent
ms.openlocfilehash: 56ceabc79947967846d342354fd033510be5f05a
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78458256"
---
# <a name="deploying-an-aspnet-web-application-with-sql-server-compact-using-visual-studio-or-visual-web-developer-deploying-sql-server-compact-databases---2-of-12"></a>Развертывание веб-приложения ASP.NET с SQL Server Compact с помощью Visual Studio или Visual Web Developer: развертывание баз данных SQL Server Compact-2 из 12

от [Tom Dykstra)](https://github.com/tdykstra)

[Скачать начальный проект](https://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)

> В этой серии учебников показано, как развернуть (опубликовать) проект веб-приложения ASP.NET, включающий базу данных SQL Server Compact, с помощью Visual Studio 2012 RC или Visual Studio Express 2012 RC для Web. При установке обновления веб-публикации можно также использовать Visual Studio 2010. Введение в серию см. [в первом учебнике серии](deployment-to-a-hosting-provider-introduction-1-of-12.md).
> 
> Руководство, в котором показаны функции развертывания, появившиеся после выпуска версии-КАНДИДАТа Visual Studio 2012, демонстрирует развертывание SQL Server выпусков, отличных от SQL Server Compact, и демонстрация развертывания в веб-приложениях службы приложений Azure см. в разделе [ASP.NET Web Deploying using Visual Studio](../../deployment/visual-studio-web-deployment/introduction.md).

## <a name="overview"></a>Обзор

В этом руководстве показано, как настроить две базы данных SQL Server Compact и ядро СУБД для развертывания.

Для доступа к базе данных программе университета Contoso требуется следующее программное обеспечение, которое должно быть развернуто вместе с приложением, поскольку оно не включено в .NET Framework:

- [SQL Server Compact](https://www.microsoft.com/sqlserver/en/us/editions/compact.aspx) (ядро СУБД).
- [Универсальные поставщики ASP.NET](http://www.hanselman.com/blog/IntroducingSystemWebProvidersASPNETUniversalProvidersForSessionMembershipRolesAndUserProfileOnSQLCompactAndSQLAzure.aspx) (который позволяет системе членства в ASP.NET использовать SQL Server Compact)
- [Entity Framework 5,0](https://msdn.microsoft.com/library/gg696172(d=lightweight,v=vs.103).aspx)(Code First с миграцией).

Также необходимо развернуть структуру базы данных и некоторые (не все) данные в двух базах данных приложения. Как правило, при разработке приложения необходимо ввести тестовые данные в базу данных, которую не нужно развертывать на активном сайте. Однако вы также можете ввести некоторые рабочие данные, которые требуется развернуть. В этом учебнике вы настроите проект университета Contoso, чтобы при развертывании включалось необходимое программное обеспечение и правильные данные.

Напоминание. Если вы получаете сообщение об ошибке или что-то не работает при работе с этим руководством, обязательно ознакомьтесь со [страницей устранения неполадок](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md).

## <a name="sql-server-compact-versus-sql-server-express"></a>SQL Server Compact и SQL Server Express

В примере приложения используется SQL Server Compact 4,0. Это относительно новая возможность для веб-сайтов. более ранние версии SQL Server Compact не работают в среде веб-хостинга. SQL Server Compact предлагает несколько преимуществ по сравнению с более распространенным сценарием разработки с SQL Server Express и развертыванием в полной SQL Server. В зависимости от выбранного поставщика услуг размещения SQL Server Compact может быть дешевле для развертывания, так как некоторые поставщики могут взимать дополнительную плату для поддержки полной базы данных SQL Server. Дополнительная плата за SQL Server Compact не взимается, так как вы можете развернуть ядро СУБД как часть веб-приложения.

Однако следует также знать об ограничениях. SQL Server Compact не поддерживает хранимые процедуры, триггеры, представления или репликацию. (Полный список SQL Server функций, которые не поддерживаются SQL Server Compact, см. в разделе [различия между SQL Server Compact и SQL Server](https://msdn.microsoft.com/library/bb896140.aspx).) Кроме того, некоторые средства, которые можно использовать для управления схемами и данными в SQL Server Express и SQL Server базах данных, не работают с SQL Server Compact. Например, нельзя использовать SQL Server Management Studio или SQL Server Data Tools в Visual Studio с базами данных SQL Server Compact. У вас есть и другие варианты работы с SQL Server Compact базами данных:

- В Visual Studio можно использовать обозреватель сервера, который предлагает ограниченные функции обработки баз данных для SQL Server Compact.
- Можно использовать функцию обработки базы данных [WebMatrix](https://www.microsoft.com/web/webmatrix/), которая имеет больше функций, чем обозреватель сервера.
- Вы можете использовать относительно полнофункциональные инструменты сторонних разработчиков или средства с открытым исходным кодом, такие как [панель инструментов SQL Server Compact](https://github.com/ErikEJ/SqlCeToolbox) и [SQL Compact Data и программа скриптов схемы](https://github.com/ErikEJ/SqlCeToolbox).
- Вы можете создавать и запускать собственные скрипты DDL (язык описания данных) для работы со схемой базы данных.

Вы можете начать с SQL Server Compact, а затем выполнить обновление позже по мере развития потребностей. В последующих руководствах этой серии показано, как выполнить миграцию с SQL Server Compact на SQL Server Express и SQL Server. Однако если вы создаете новое приложение и предполагаете, что в ближайшем будущем требуется SQL Server, лучше всего начать с SQL Server или SQL Server Express.

## <a name="configuring-the-sql-server-compact-database-engine-for-deployment"></a>Настройка ядро СУБД SQL Server Compact для развертывания

Программное обеспечение, необходимое для доступа к данным в приложении университета Contoso, было добавлено путем установки следующих пакетов NuGet:

- [склсерверкомпакт](http://nuget.org/List/Packages/SqlServerCompact)
- [System. Web. Providers](http://nuget.org/List/Packages/System.Web.Providers) (универсальные поставщики ASP.NET)
- [EntityFramework](http://nuget.org/List/Packages/EntityFramework)
- [EntityFramework. Склсерверкомпакт](http://nuget.org/List/Packages/EntityFramework.sqlservercompact)

Ссылки указывают на текущие версии этих пакетов, которые могут быть более новыми, чем установленные в начальном проекте, скачанном для этого руководства. Для развертывания на поставщик услуг размещения убедитесь, что используется Entity Framework 5,0 или более поздней версии. В более ранних версиях Code First Migrations требуется полное доверие, и во многих поставщиках услуг размещения приложение будет работать со средним уровнем доверия. Дополнительные сведения о среднем уровне доверия см. в руководстве [развертывание в службах IIS в качестве тестовой среды](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12.md) .

Установка пакета NuGet обычно занимает все необходимое для развертывания этого программного обеспечения с помощью приложения. В некоторых случаях это включает в себя такие задачи, как изменение файла Web. config и добавление сценариев PowerShell, выполняемых при каждом построении решения. **Если вы хотите добавить поддержку любой из этих функций (например, SQL Server Compact и Entity Framework) без использования NuGet, убедитесь, что вы знаете, что делает Установка пакета NuGet, чтобы вы могли выполнить ту же работу вручную.**

Существует одно исключение, при котором NuGet не берет все, что нужно, чтобы обеспечить успешное развертывание. Пакет NuGet Склсерверкомпакт добавляет в проект скрипт, выполняемый после сборки, который копирует машинные сборки в вложенные папки *x86* и *AMD64* в папке Project *bin* , но скрипт не включает эти папки в проект. В результате веб-развертывание не будет копировать их на конечный веб-сайт, если они не включены в проект вручную. (Это происходит из-за конфигурации развертывания по умолчанию. другой вариант, который не используется в этих учебниках, заключается в изменении параметра, который управляет этим поведением. Параметр, который можно изменить, — это **только файлы, необходимые для запуска приложения** в разделе **элементы для развертывания** на вкладке **Пакет/Публикация веб-сайта** окна **Свойства проекта** . Изменять этот параметр обычно не рекомендуется, так как это может привести к развертыванию большего количества файлов в рабочей среде, чем требуется. Дополнительные сведения о альтернативных вариантах см. в руководстве по [настройке свойств проекта](deployment-to-a-hosting-provider-configuring-project-properties-4-of-12.md) .

Выполните сборку проекта, а затем в **Обозреватель решений** щелкните " **Показывать все файлы** ", если вы еще не сделали этого. Также может потребоваться нажать кнопку **Обновить**.

![Solution_Explorer_Show_All_Files](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image1.png)

Разверните папку **bin** , чтобы просмотреть папки **AMD64** и **x86** , а затем выберите эти папки, щелкните правой кнопкой мыши и выберите пункт **включить в проект**.

![amd64_and_x86_in_Solution_Explorer.png](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image2.png)

Значки папок изменяются, чтобы показывать, что папка включена в проект.

![Solution_Explorer_amd64_included. png](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image3.png)

## <a name="configuring-code-first-migrations-for-application-database-deployment"></a>Настройка Code First Migrations для развертывания базы данных приложения

При развертывании базы данных приложений обычно не требуется развертывать базу данных разработки со всеми данными в рабочей среде, так как большая часть данных в ней, вероятно, существует только в целях тестирования. Например, имена учащихся в тестовой базе данных являются вымышленными. С другой стороны, часто нельзя развертывать только структуру базы данных без каких бы то ни было данных. Некоторые данные в тестовой базе данных могут быть реальными и должны быть там, когда пользователи начинают использовать приложение. Например, база данных может иметь таблицу, содержащую допустимые значения категории или имена реальных отделов.

Для имитации этого распространенного сценария вы настроите метод начального значения Code First Migrations, который вставляет в базу данных только те данные, которые должны находиться в рабочей среде. Этот метод заполнения не вставляет проверочные данные, так как он будет выполняться в рабочей среде после того, как Code First создаст базу данных в рабочей среде.

В более ранних версиях Code First до выпуска миграций были распространены методы инициализации для вставки тестовых данных, так как при каждом изменении модели во время разработки база данных была полностью удалена и создана заново с нуля. При использовании Code First Migrations тестовые данные сохранены после изменения базы данных, поэтому не требуется включать тестовые данные в метод заполнения. Скачанный проект использует метод перед миграцией, включающий все данные в методе SEED класса инициализатора. В этом учебнике вы отключите класс инициализатора и включите миграцию. Затем вы обновите метод SEED в классе конфигурации миграции, чтобы вставить только те данные, которые необходимо вставить в рабочую среду.

На следующей схеме показана схема базы данных приложения.

[![School_database_diagram](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image5.png)](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image4.png)

В этих учебниках предполагается, что `Student` и `Enrollment` таблицы должны быть пустыми при первом развертывании сайта. Другие таблицы содержат данные, которые должны быть предварительно загружены, когда приложение становится активным.

Так как вы будете использовать Code First Migrations, больше не нужно использовать инициализатор Code First **дропкреатедатабасеифмоделчанжес** . Код для этого инициализатора находится в файле SchoolInitializer.cs в проекте ContosoUniversity. DAL. Параметр в элементе **appSettings** файла Web. config вызывает запуск этого инициализатора всякий раз, когда приложение пытается получить доступ к базе данных в первый раз:

[!code-xml[Main](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/samples/sample1.xml?highlight=3)]

Откройте файл Web. config приложения и удалите элемент, указывающий класс инициализатора Code First из элемента appSettings. Элемент appSettings теперь выглядит следующим образом:

[!code-xml[Main](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/samples/sample2.xml)]

> [!NOTE]
> Другой способ указания класса инициализатора — это сделать, вызвав `Database.SetInitializer` в методе `Application_Start` в файле *Global. asax* . Если вы включаете миграцию в проекте, который использует этот метод для указания инициализатора, удалите эту строку кода.

Затем включите Code First Migrations.

Первый шаг — убедиться, что проект ContosoUniversity задан как запускаемый проект. В **Обозреватель решений**щелкните правой кнопкой мыши проект ContosoUniversity и выберите **Назначить запускаемым проектом**. Code First Migrations будет искать в проекте запуска, чтобы найти строку подключения к базе данных.

В меню **Сервис** щелкните **Диспетчер пакетов NuGet**, а затем щелкните **Консоль диспетчера пакетов**.

![Selecting_Package_Manager_Console](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image6.png)

В верхней части окна **консоли диспетчера пакетов** выберите CONTOSOUNIVERSITY. DAL в качестве проекта по умолчанию, а затем в `PM>` строке введите "Enable-migrations".

![Enable-migrations_command](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image7.png)

Эта команда создает файл *Configuration.CS* в новой папке *миграций* в проекте ContosoUniversity. DAL.

![Migrations_folder_in_Solution_Explorer](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image8.png)

Вы выбрали проект DAL, так как команда "включить миграцию" должна выполняться в проекте, содержащем класс контекста Code First. Если этот класс находится в проекте библиотеки классов, Code First Migrations ищет строку подключения к базе данных в запускаемом проекте для решения. В решении ContosoUniversity веб-проект был задан как запускаемый проект. (Если вы не хотите назначать проект со строкой подключения в качестве запускаемого проекта в Visual Studio, можно указать запускаемый проект в команде PowerShell. Чтобы увидеть синтаксис команды для команды "включить миграцию", можно ввести команду "Get-Help Enable-migrations".)

Откройте файл Configuration.cs и замените комментарии в методе `Seed` следующим кодом:

[!code-csharp[Main](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/samples/sample3.cs)]

Ссылки на `List` имеют красные волнистые линии, так как у вас еще нет оператора `using` для ее пространства имен. Щелкните правой кнопкой мыши один из экземпляров `List` и выберите пункт **Разрешить**, а затем щелкните **использование System. Collections. Generic**.

![Разрешение с помощью инструкции using](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image9.png)

Этот фрагмент меню добавляет следующий код к операторам `using` в верхней части файла.

[!code-csharp[Main](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/samples/sample4.cs)]

> [!NOTE]
> Добавление кода в метод `Seed` является одним из множества способов вставки фиксированных данных в базу данных. Альтернативой является добавление кода в методы `Up` и `Down` каждого класса миграции. Методы `Up` и `Down` содержат код, который реализует изменения базы данных. Примеры можно увидеть в учебнике [развертывание обновления базы данных](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12.md) .
> 
> Кроме того, можно написать код, выполняющий инструкции SQL, с помощью метода `Sql`. Например, если вы добавили столбец бюджета в таблицу отдел и хотите инициализировать все бюджеты отдела до $1 000,00 в рамках миграции, можно добавить следующую строку кода в метод `Up` для этой миграции:
> 
> `Sql("UPDATE Department SET Budget = 1000");`
> 
> В этом примере, показанном в этом руководстве, используется метод `AddOrUpdate` в методе `Seed` класса Code First Migrations `Configuration`. Code First Migrations вызывает метод `Seed` после каждой миграции, и этот метод обновляет уже вставленные строки или вставляет их, если они еще не существуют. Метод `AddOrUpdate` может быть не лучшим выбором для вашего сценария. Дополнительные сведения см. в разделе о [методе EF 4,3 AddOrUpdate](http://thedatafarm.com/blog/data-access/take-care-with-ef-4-3-addorupdate-method/) в блоге Юлия Лерман.

Нажмите клавиши CTRL + SHIFT + B, чтобы выполнить сборку проекта.

Следующим шагом является создание класса `DbMigration` для первоначальной миграции. Необходимо, чтобы эта миграция могла создать новую базу данных, поэтому необходимо удалить уже существующую базу данных. SQL Server Compact базы данных содержатся в *SDF* файлы в папке *приложения\_данных* . В **Обозреватель решений**разверните *Данные приложения\_* в проекте ContosoUniversity, чтобы просмотреть две базы данных SQL Server Compact, которые представлены в *SDF* файлах.

Щелкните правой кнопкой мыши файл *School. sdf* и выберите команду **Удалить**.

![sdf_files_in_Solution_Explorer](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image10.png)

В окне **консоли диспетчера пакетов** введите команду "добавить начальную миграцию", чтобы создать начальную миграцию и присвойте ей имя "Initial".

![Добавление migration_command](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image11.png)

Code First Migrations создает другой файл класса в папке *migrations* , и этот класс содержит код, создающий схему базы данных.

В **консоли диспетчера пакетов**введите команду Update-Database, чтобы создать базу данных и запустить метод **SEED** .

![Обновление — database_command](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image12.png)

(Если возникает ошибка, указывающая, что таблица уже существует и не может быть создана, возможно, приложение было запущено после удаления базы данных и перед выполнением `update-database`. В этом случае удалите файл *School. sdf* еще раз и повторите команду `update-database`.)

Запустите приложение. Теперь страница учащихся пуста, но на странице инструкторов содержатся инструкторы. Это то, что вы получите в рабочей среде после развертывания приложения.

![Empty_Students_page](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image13.png)

![Instructors_page_after_initial_migration](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image14.png)

Теперь проект готов к развертыванию базы данных *School* .

## <a name="creating-a-membership-database-for-deployment"></a>Создание базы данных членства для развертывания

Приложение университета Contoso использует систему контроля членства ASP.NET и проверку подлинности с помощью форм для проверки подлинности и авторизации пользователей. Одна из ее страниц доступна только администраторам. Чтобы просмотреть эту страницу, запустите приложение и выберите пункт **Обновить кредиты** во всплывающем меню в разделе **курсы**. Приложение отображает страницу **входа** , так как только администраторы имеют право на использование страницы **Обновление кредитов** .

[![Log_in_page](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image16.png)](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image15.png)

Войдите в систему как "admin" с помощью пароля "PAS $ w0rd" (Обратите внимание на число нуля вместо буквы "o" в "w0rd"). После входа в систему отобразится страница **Обновление кредитов** .

[![Update_Credits_page](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image18.png)](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image17.png)

При первом развертывании сайта обычно исключаются большинство или все учетные записи пользователей, создаваемые для тестирования. В этом случае вы развернете учетную запись администратора и не сможете использовать учетные записи пользователей. Вместо того, чтобы удалять тестовые учетные записи вручную, вы создадите новую базу данных членства, имеющую только одну учетную запись администратора, необходимую в рабочей среде.

> [!NOTE]
> В базе данных членства хранится хэш паролей учетных записей. Чтобы развернуть учетные записи с одного компьютера на другой, необходимо убедиться, что подпрограммы хэширования не создают на целевом сервере разные хэши, чем на исходном компьютере. Они будут создавать одинаковые хэши при использовании универсальные поставщики ASP.NET, если не изменить алгоритм по умолчанию. Алгоритмом по умолчанию является HMACSHA256, который указывается в атрибуте **проверки** элемента **[machineKey](https://msdn.microsoft.com/library/w8h3skw9.aspx)** в файле Web. config.

База данных членства не обслуживается Code First Migrations, и не существует автоматического инициализатора, который заполняет базу данных тестовыми учетными записями (как и для базы данных School). Таким образом, чтобы обеспечить доступность тестовых данных, необходимо создать копию тестовой базы данных перед созданием новой.

В **Обозреватель решений**переименуйте файл *ASPNET. sdf* в папке *app\_Data* в файл *АСПнет-дев. sdf*. (Не создавайте копию, просто переименуйте ее — вы создадите новую базу данных чуть позже.)

В **Обозреватель решений**убедитесь, что выбран веб-проект (ContosoUniversity, а не CONTOSOUNIVERSITY. DAL). Затем в меню **проект** выберите **Конфигурация ASP.NET** , чтобы запустить **средство администрирования веб-сайта**(западноафриканскому).

Перейдите на вкладку **Безопасность** .

[![WAT_Security_tab](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image20.png)](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image19.png)

Щелкните **Создание ролей или управление ими** и добавьте роль **администратора** .

[![WAT_Create_New_Role](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image22.png)](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image21.png)

Вернитесь на вкладку **Безопасность** , щелкните **создать пользователя**и добавьте пользователя Admin в качестве администратора. Перед нажатием кнопки **создать пользователя** на странице **Создание пользователя** убедитесь, что установлен флажок **Администратор** . В этом руководстве используется пароль "PAS $ w0rd", и вы можете ввести любой адрес электронной почты.

[![WAT_Create_User](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image24.png)](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image23.png)

Закройте браузер. В **Обозреватель решений**нажмите кнопку "Обновить", чтобы увидеть новый файл *ASPNET. sdf* .

![New_aspnet.sdf_in_Solution_Explorer](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image25.png)

Щелкните правой кнопкой мыши **ASPNET. sdf** и выберите **включить в проект**.

## <a name="distinguishing-development-from-production-databases"></a>Отличия разработки от рабочих баз данных

В этом разделе вы переименуете базы данных, чтобы версии разработки Счул-дев. sdf и АСПнет-дев. sdf, а рабочие версии — Счул-прод. sdf и АСПнет-прод. sdf. Это не является обязательным, но это поможет вам предотвратить получение тестовых и рабочих версий баз данных.

В **Обозреватель решений**щелкните **Обновить** и разверните папку приложения\_данных, чтобы просмотреть созданную ранее базу данных School. щелкните его правой кнопкой мыши и выберите пункт **включить в проект**.

![Including_School.sdf_in_project](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image26.png)

Переименуйте *ASPNET. sdf* в *АСПнет-прод. sdf*.

Переименуйте *School. sdf* в *счул-дев. sdf*.

При запуске приложения в Visual Studio вы не хотите *использовать версии файлов базы данных, которые* вы хотите использовать для *разработки* . Таким образом, необходимо изменить строки подключения в файле Web. config, чтобы они указывали на версии баз данных, создаваемые для *разработчиков* . (Вы не создали файл Счул-прод. sdf, но это нормально, так как Code First создаст эту базу данных в рабочей среде при первом запуске приложения.)

Откройте файл Web. config приложения и перейдите к строкам подключения:

[!code-xml[Main](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/samples/sample5.xml)]

Измените "ASPNET. sdf" на "АСПнет-дев. sdf" и измените "School. sdf" на "Счул-дев. sdf":

[!code-xml[Main](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/samples/sample6.xml?highlight=4-5)]

Ядро СУБД SQL Server Compact и обе базы данных теперь готовы к развертыванию. В следующем руководстве описано, как настроить автоматическое преобразование файла *Web. config* для параметров, которые должны быть разными в средах разработки, тестирования и рабочей среде. (Между параметрами, которые необходимо изменить, являются строки подключения, но эти изменения будут внесены позже при создании профиля публикации.)

## <a name="more-information"></a>Дополнительные сведения

Дополнительные сведения о NuGet см. в статье [руководство по](http://docs.nuget.org/docs/start-here/overview) [управлению библиотеками проектов с помощью NuGet](https://msdn.microsoft.com/magazine/hh547106.aspx) и NuGet. Если вы не хотите использовать NuGet, вам потребуется изучить, как анализировать пакет NuGet, чтобы определить, что он делает при установке. (Например, это может быть Настройка преобразований *Web. config* , Настройка сценариев PowerShell для выполнения во время сборки и т. д.). Дополнительные сведения о том, как работает NuGet, см. в статье [Создание и Публикация пакета](http://docs.nuget.org/docs/creating-packages/creating-and-publishing-a-package) и [Преобразование файла конфигурации и исходного кода](http://docs.nuget.org/docs/creating-packages/configuration-file-and-source-code-transformations).

> [!div class="step-by-step"]
> [Назад](deployment-to-a-hosting-provider-introduction-1-of-12.md)
> [Вперед](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12.md)
