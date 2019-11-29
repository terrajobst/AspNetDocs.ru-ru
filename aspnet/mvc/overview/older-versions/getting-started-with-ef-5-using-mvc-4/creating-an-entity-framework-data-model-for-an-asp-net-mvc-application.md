---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application
title: Создание Entity Framework модели данных для приложения ASP.NET MVC (1 из 10) | Документация Майкрософт
author: tdykstra
description: Более новая версия этой серии руководств доступна для Visual Studio 2013, Entity Framework 6 и MVC 5. Пример веб-приложения для университета Contoso — de...
ms.author: riande
ms.date: 07/30/2013
ms.assetid: 4ba029b6-ee7c-4e45-a0e7-b703c37e5d9a
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 8ee5aa22b6b2329b01d41437f30508e28a2288b2
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/28/2019
ms.locfileid: "74595971"
---
# <a name="creating-an-entity-framework-data-model-for-an-aspnet-mvc-application-1-of-10"></a>Создание Entity Framework модели данных для приложения ASP.NET MVC (1 из 10)

от [Tom Dykstra)](https://github.com/tdykstra)

[Скачать завершенный проект](https://code.msdn.microsoft.com/Getting-Started-with-dd0e2ed8)

> > [!NOTE] 
> > 
> > [Более новая версия этой серии руководств](../../getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md) доступна для Visual Studio 2013, Entity Framework 6 и MVC 5.
> 
> 
> Пример веб-приложения для университета Contoso демонстрирует создание приложений ASP.NET MVC 4 с помощью Entity Framework 5 и Visual Studio 2012. В этом примере приложения реализуется веб-сайт вымышленного университета Contoso. На нем предусмотрены различные функции, в том числе прием учащихся, создание курсов и назначение преподавателей. В этой серии руководств объясняется, как создать пример приложения университета Contoso. Вы можете [скачать готовое приложение](https://code.msdn.microsoft.com/Getting-Started-with-dd0e2ed8).
> 
> ## <a name="code-first"></a>Code First
> 
> Существует три способа работы с данными в Entity Framework: *Database First*, *Model First*и *Code First*. Это руководство предназначено для Code First. Сведения о различиях между этими рабочими процессами и рекомендации по выбору наиболее подходящего сценария см. в разделе [рабочие процессы разработки Entity Framework](https://msdn.microsoft.com/library/ms178359.aspx#dbfmfcf).
> 
> ## <a name="mvc"></a>MVC
> 
> Пример приложения основан на [ASP.NET MVC](../../../index.md). Если вы предпочитаете работать с моделью веб-форм ASP.NET, см. статью " [Привязка модели и веб-формы](../../../../web-forms/overview/presenting-and-managing-data/model-binding/retrieving-data.md) " серии руководств и [Схема содержимого ASP.NET Data Access](../../../../whitepapers/aspnet-data-access-content-map.md).
> 
> ## <a name="software-versions"></a>Версии программного обеспечения
> 
> | **Показано в руководстве** | **Также работает с** |
> | --- | --- |
> | Windows 8 | Windows 7 |
> | Visual Studio 2012 | Visual Studio 2012 Express для Web. Это автоматически устанавливается пакетом Windows Azure SDK, если у вас еще нет VS 2012 или VS 2012 Express для Web. Visual Studio 2013 должны работать, но учебник не тестировался с ним, и некоторые пункты меню и диалоговые окна отличаются. Для развертывания Windows Azure требуется [версия VS 2013 пакета SDK для Windows Azure](https://go.microsoft.com/fwlink/p/?linkid=323510) . |
> | .NET 4.5 | Большинство показанных функций будет работать в .NET 4, но некоторые не будут. Например, для поддержки перечисления в EF требуется .NET 4,5. |
> | Entity Framework 5 |  |
> | [Пакет Windows Azure SDK 2,1](https://go.microsoft.com/fwlink/p/?linkid=323511) | Если пропустить шаги развертывания Windows Azure, пакет SDK не требуется. При выпуске новой версии пакета SDK ссылка установит новую версию. В этом случае может потребоваться адаптировать некоторые инструкции к новому ИНТЕРФЕЙСу и функциям. |
> 
> ## <a name="questions"></a>Вопросы
> 
> Если у вас есть вопросы, которые не связаны непосредственно с этим руководством, вы можете опубликовать их на [форуме по ASP.NET Entity Framework](https://forums.asp.net/1227.aspx), на [форуме Entity Framework и LINQ to Entities](https://social.msdn.microsoft.com/forums/adodotnetentityframework/threads/)или [StackOverflow.com](http://stackoverflow.com/).
> 
> ## <a name="acknowledgments"></a>Благодарности
> 
> Для получения [подтверждений и замечаний о VB](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#acknowledgments)см. Последнее руководство в серии.
> 
> ## <a name="original-version-of-the-tutorial"></a>Исходная версия учебника
> 
> Исходная версия учебника доступна в [электронной книге EF 4,1/MVC 3](https://social.technet.microsoft.com/wiki/contents/articles/11608.e-book-gallery-for-microsoft-technologies.aspx#GettingStartedwiththeEntityFramework4.1usingASP.NETMVC).

## <a name="the-contoso-university-web-application"></a>Веб-приложение университета Contoso

В рамках этих учебников вы будете создавать приложение, которое представляет собой простой веб-сайт университета.

Пользователи приложения могут просматривать и обновлять сведения об учащихся, курсах и преподавателях. Будет создано несколько экранов.

![Students_Index_page](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image1.png)

![](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image2.png)

Стиль пользовательского интерфейса этого сайта практически полностью основан на встроенных шаблонах, поскольку это позволяет сосредоточиться на изучении и использовании возможностей платформы Entity Framework.

## <a name="prerequisites"></a>Необходимые компоненты

В руководстве и снимках экрана в этом учебнике предполагается, что вы используете [Visual studio 2012](https://www.microsoft.com/visualstudio/eng/downloads) или [Visual Studio 2012 Express для Web](https://go.microsoft.com/fwlink/?LinkID=275131), с последним обновлением и пакетом SDK Azure для .NET, установленным начиная с июля 2013. Все это можно получить по следующей ссылке:

[Пакет Azure SDK для .NET (Visual Studio 2012)](https://go.microsoft.com/fwlink/?LinkId=254364)

Если у вас установлена Visual Studio, на приведенной выше ссылке будут установлены все отсутствующие компоненты. Если у вас нет Visual Studio, ссылка установит Visual Studio 2012 Express для Web. Можно использовать Visual Studio 2013, но некоторые необходимые процедуры и экраны будут отличаться.

## <a name="create-an-mvc-web-application"></a>Создание веб-приложения MVC

Откройте Visual Studio и создайте новый C# проект с именем "ContosoUniversity" с помощью шаблона **веб-приложения ASP.NET MVC 4** . Убедитесь, что вы используете **.NET Framework 4,5** (вы будете использовать [Свойства`enum`](https://msdn.microsoft.com/data/hh859576.aspx), для которых требуется .NET 4,5).

![New_project_dialog_box](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image3.png)

В диалоговом окне **Новый проект ASP.NET MVC 4** выберите шаблон **Интернет приложение** .

Оставьте выбранным обработчик представлений **Razor** и оставьте флажок **создать проект модульного теста** снятым.

Нажмите кнопку **ОК**.

![Project_template_options](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image4.png)

## <a name="set-up-the-site-style"></a>Настройка стиля сайта

Выполните незначительную настройку меню, макета и домашней страницы сайта.

Откройте *Views\Shared\\_layout. cshtml*и замените содержимое файла следующим кодом. Изменения выделены.

[!code-cshtml[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample1.cshtml?highlight=5,15,25-28,43)]

Этот код вносит следующие изменения:

- Заменяет экземпляры шаблона "мое приложение ASP.NET MVC" и "ваш логотип здесь" на "университет Contoso".
- Добавляет ссылки на действия, которые будут использоваться далее в этом руководстве.

В *Views\Home\Index.cshtml*замените содержимое файла следующим кодом, чтобы исключить абзацы шаблона для ASP.NET и MVC:

[!code-cshtml[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample2.cshtml)]

В *Controllers\HomeController.CS*измените значение `ViewBag.Message` в методе действия `Index` на "Добро пожаловать в Contoso университета!", как показано в следующем примере:

[!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample3.cs?highlight=3)]

Нажмите клавиши CTRL + F5, чтобы запустить сайт. Домашняя страница отображается в главном меню.

![Contoso_University_home_page](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image5.png)

## <a name="create-the-data-model"></a>Создание модели данных

Теперь необходимо создать классы сущностей для приложения университета Contoso. Начнем с следующих трех сущностей:

![Class_diagram](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image6.png)

Между сущностями `Student` и `Enrollment`, а также между сущностями `Course` и `Enrollment` существует отношение "один ко многим". Другими словами, учащийся может быть зарегистрирован в любом количестве курсов, а в отдельном курсе может быть зарегистрировано любое количество учащихся.

В следующих разделах создаются классы для каждой из этих сущностей.

> [!NOTE]
> Если вы попытаетесь скомпилировать проект до завершения создания всех этих классов сущностей, вы получите ошибки компилятора.

### <a name="the-student-entity"></a>Сущность Student

![Student_entity](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image7.png)

В папке *Models* создайте *Student.CS* и замените имеющийся код следующим кодом:

[!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample4.cs)]

Свойство `StudentID` будет использоваться в качестве столбца первичного ключа в таблице базы данных, соответствующей этому классу. По умолчанию Entity Framework интерпретирует свойство с именем `ID` или *classname* `ID` в качестве первичного ключа.

Свойство `Enrollments` является *свойством навигации*. Свойства навигации содержат другие сущности, связанные с этой сущностью. В этом случае свойство `Enrollments` сущности `Student` будет содержать все `Enrollment` сущности, связанные с этой сущностью `Student`. Иными словами, если данная строка `Student` в базе данных содержит две связанные `Enrollment` строки (строки, которые содержат значение первичного ключа учащегося в их `StudentID` внешнем ключевом столбце), то `Student` `Enrollments`ной сущности будут содержать эти две `Enrollment` сущности.

Свойства навигации обычно определяются как `virtual`, чтобы они могли воспользоваться преимуществами определенных Entity Frameworkных функций, таких как *Отложенная загрузка*. (Отложенная загрузка будет объяснена позже, в руководстве по [чтению связанных данных](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md) далее в этой серии.

Если свойство навигации может содержать несколько сущностей (как в отношениях "многие ко многим" или "один ко многим"), оно должно иметь тип списка, допускающий добавление, удаление и обновление записей, такой как `ICollection`.

### <a name="the-enrollment-entity"></a>Сущность регистрации

![Enrollment_entity](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image8.png)

В папке *Models* создайте файл *Enrollment.cs* и замените существующий код следующим кодом:

[!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample5.cs)]

Свойство Grade является [перечислением](https://msdn.microsoft.com/data/hh859576.aspx). Знак вопроса после объявления типа `Grade` указывает, что свойство `Grade` [допускает значение NULL](https://msdn.microsoft.com/library/2cf62fcy.aspx). Оценка, имеющая значение null, отличается от нулевой — значение NULL означает, что категория не известна или еще не была назначена.

Свойство `StudentID` представляет собой внешний ключ. Ему соответствует свойство навигации `Student`. Сущность `Enrollment` связана с одной сущностью `Student`, поэтому это свойство может содержать одну сущность `Student` (в отличие от представленного ранее свойства навигации `Student.Enrollments`, которое может содержать несколько сущностей `Enrollment`).

Свойство `CourseID` представляет собой внешний ключ. Ему соответствует свойство навигации `Course`. Сущность `Enrollment` связана с одной сущностью `Course`.

### <a name="the-course-entity"></a>Сущность Course

![Course_entity](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image9.png)

В папке *Models* создайте *Course.CS*, заменив существующий код следующим кодом:

[!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample6.cs)]

Свойство `Enrollments` является свойством навигации. Сущность `Course` может быть связана с любым числом сущностей `Enrollment`.

Мы рассмотрим дополнительные сведения о [[датабасеженератед](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.databasegeneratedattribute(v=vs.110).aspx)([датабасеженератедоптион](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.databasegeneratedoption(v=vs.95).aspx). Нет)] в следующем руководстве. Фактически, этот атрибут позволяет ввести первичный ключ для курса, а не использовать базу данных, чтобы создать его.

## <a name="create-the-database-context"></a>Создание контекста базы данных

Класс main, который координирует Entity Framework функциональные возможности для конкретной модели данных, является классом *контекста базы данных* . Этот класс создается путем наследования от класса [System. Data. Entity. DbContext](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=VS.103).aspx) . В коде указываются сущности, которые включаются в модель данных. Также вы можете настроить реакцию платформы Entity Framework на некоторые события. В этом проекте соответствующий класс называется `SchoolContext`.

Создайте папку с именем *DAL* (для уровня доступа к данным). В этой папке создайте новый файл класса с именем *SchoolContext.CS*и замените существующий код следующим кодом:

[!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample7.cs)]

Этот код создает свойство [DbSet](https://msdn.microsoft.com/library/system.data.entity.dbset(v=VS.103).aspx) для каждого набора сущностей. В терминологии Entity Framework *набор сущностей* обычно соответствует таблице базы данных, а *сущность* соответствует строке в таблице.

Инструкция `modelBuilder.Conventions.Remove` в методе [OnModelCreating](https://msdn.microsoft.com/library/system.data.entity.dbcontext.onmodelcreating(v=vs.103).aspx) предотвращает множественное преобразование имен таблиц. Если этого не сделать, то созданные таблицы будут называться `Students`, `Courses`и `Enrollments`. Вместо этого имена таблиц будут `Student`, `Course`и `Enrollment`. В среде разработчиков нет единого мнения о том, следует ли использовать имена таблиц во множественном числе. В этом руководстве используется форма единственного числа, но важно отметить, что вы можете выбрать любую из этих форм, включив или опустив эту строку кода.

## <a name="sql-server-express-localdb"></a>SQL Server Express LocalDB

[LocalDB](https://blogs.msdn.com/b/sqlexpress/archive/2011/07/12/introducing-localdb-a-better-sql-express.aspx) — это упрощенная версия SQL Server Express ядро СУБД, которая запускается по запросу и запускается в пользовательском режиме. LocalDB выполняется в специальном режиме выполнения SQL Server Express, который позволяет работать с базами данных в виде *MDF* -файлов. Как правило, файлы базы данных LocalDB хранятся в папке *приложения\_данных* веб-проекта. Функция пользовательского экземпляра в SQL Server Express также позволяет работать с *MDF* -файлами, но функция пользовательского экземпляра является устаревшей. Поэтому для работы с *MDF* -файлами рекомендуется использовать LocalDB.

Обычно SQL Server Express не используется для рабочих веб-приложений. LocalDB в частности не рекомендуется для использования в рабочей среде с веб-приложением, поскольку оно не предназначено для работы с IIS.

В Visual Studio 2012 и более поздних версиях LocalDB устанавливается по умолчанию в Visual Studio. В Visual Studio 2010 и более ранних версиях SQL Server Express (без LocalDB) устанавливается по умолчанию в Visual Studio. его необходимо установить вручную, если вы используете Visual Studio 2010.

В этом учебнике вы будете работать с LocalDB, чтобы базу данных можно было хранить в папке *App\_Data* в файле *MDF* . Откройте корневой файл *Web. config* и добавьте новую строку подключения в коллекцию `connectionStrings`, как показано в следующем примере. (Убедитесь, что вы обновляете файл *Web. config* в корневой папке проекта. Кроме того, файл *Web. config* находится в вложенной папке *views* , которую не нужно обновлять.)

[!code-xml[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample8.xml)]

По умолчанию Entity Framework ищет строку подключения с именем, совпадающую с классом `DbContext` (`SchoolContext` для этого проекта). Добавленная строка подключения указывает базу данных LocalDB с именем *ContosoUniversity. mdf* , расположенную в папке *app\_Data* . Дополнительные сведения см. в разделе [SQL Server строки подключения для веб-приложений ASP.NET](https://msdn.microsoft.com/library/jj653752.aspx).

В действительности нет необходимости указывать строку подключения. Если строка подключения не указана, Entity Framework создаст ее. Однако база данных может отсутствовать в папке *приложения\_данных* приложения. Сведения о том, где будет создана база данных, см. в разделе [Code First к новой базе данных](https://msdn.microsoft.com/data/jj193542).

Коллекция `connectionStrings` также содержит строку подключения с именем `DefaultConnection`, которая используется для базы данных членства. Вы не будете использовать базу данных членства в этом руководстве. Единственное различие между двумя строками подключения — имя базы данных и значение атрибута Name.

## <a name="set-up-and-execute-a-code-first-migration"></a>Настройка и выполнение миграции Code First

При первом запуске разработки приложения модель данных изменяется часто, и каждый раз, когда модель изменяется, она получает несинхронизированную с базой данных. Можно настроить Entity Framework для автоматического удаления и повторного создания базы данных при каждом изменении модели данных. Это не проблема на раннем этапе разработки, так как тестовые данные легко создаются повторно, но после развертывания в рабочей среде обычно требуется обновить схему базы данных без удаления базы данных. Функция миграции позволяет Code First обновлять базу данных без удаления и повторного создания. На ранних этапах цикла разработки нового проекта можно использовать [дропкреатедатабасеифмоделчанжес](https://msdn.microsoft.com/library/gg679604(v=vs.103).aspx) для удаления, повторного создания и восстановления начального значения базы данных при каждом изменении модели. Вы готовы к развертыванию приложения, поэтому можете преобразовать его в подход к миграции. В этом учебнике будут использоваться только миграции. Дополнительные сведения см. в статье о [сериях презентаций](https://blogs.msdn.com/b/adonet/archive/2014/03/12/migrations-screencast-series.aspx)для [Code First migrations](https://msdn.microsoft.com/data/jj591621) и миграции.

### <a name="enable-code-first-migrations"></a>Включить Code First Migrations

1. В меню **Сервис** выберите **Диспетчер пакетов NuGet** , а затем **консоль диспетчера пакетов**.

    ![Selecting_Package_Manager_Console](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image10.png)
2. В командной строке `PM>` введите следующую команду:

    [!code-powershell[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample9.ps1)]

    ![Команда "включить-миграция"](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image11.png)

    Эта команда создает папку *migrations* в проекте ContosoUniversity и помещает в эту папку файл *Configuration.CS* , который можно изменить для настройки миграции.

    ![Папка "миграции"](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image12.png)

    Класс `Configuration` включает метод `Seed`, который вызывается при создании базы данных и каждый раз, когда она обновляется после изменения модели данных.

    [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample10.cs)]

    Этот метод `Seed` позволяет вставлять тестовые данные в базу данных после того, как Code First создает их или обновляет.

### <a name="set-up-the-seed-method"></a>Настройка метода начального значения

Метод [SEED](https://msdn.microsoft.com/library/hh829453(v=vs.103).aspx) запускается, когда Code First migrations создает базу данных и каждый раз, когда она обновляет базу данных до последней миграции. Цель метода начального значения заключается в том, чтобы можно было вставлять данные в таблицы, прежде чем приложение будет получать доступ к базе данных в первый раз.

В более ранних версиях Code First до выпуска миграций было распространено `Seed` методов вставки тестовых данных, так как при каждом изменении модели во время разработки база данных была полностью удалена и создана заново с нуля. При использовании Code First Migrations тестовые данные сохранены после изменения базы данных, поэтому, как правило, не требуется включать данные тестирования в метод [SEED](https://msdn.microsoft.com/library/hh829453(v=vs.103).aspx) . На самом деле вы не хотите, чтобы метод `Seed` вставил тестовые данные, если вы будете использовать миграции для развертывания базы данных в рабочей среде, так как метод `Seed` будет выполняться в рабочей среде. В этом случае необходимо, чтобы метод `Seed` вставил в базу данных только те данные, которые необходимо вставить в рабочую среду. Например, может потребоваться, чтобы база данных включала фактические имена отделов в таблицу `Department`, когда приложение станет доступным в рабочей среде.

В рамках этого руководства вы будете использовать миграции для развертывания, но метод `Seed` будет в любом случае вставлять тестовые данные, чтобы упростить просмотр работы функций приложения без необходимости вручную вставлять большой объем данных.

1. Замените содержимое файла *Configuration.CS* следующим кодом, который будет загружать тестовые данные в новую базу данных. 

    [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample11.cs)]

    Метод [SEED](https://msdn.microsoft.com/library/hh829453(v=vs.103).aspx) принимает объект контекста базы данных в качестве входного параметра, а код в методе использует этот объект для добавления новых сущностей в базу данных. Для каждого типа сущности код создает коллекцию новых сущностей, добавляет их в соответствующее свойство [DbSet](https://msdn.microsoft.com/library/system.data.entity.dbset(v=vs.103).aspx) , а затем сохраняет изменения в базе данных. Не нужно вызывать метод [SaveChanges](https://msdn.microsoft.com/library/system.data.entity.dbcontext.savechanges(v=VS.103).aspx) после каждой группы сущностей, как это сделано здесь, но это помогает узнать источник проблемы, если исключение возникает во время записи кода в базу данных.

    Некоторые инструкции, которые вставляют данные, используют метод [AddOrUpdate](https://msdn.microsoft.com/library/system.data.entity.migrations.idbsetextensions.addorupdate(v=vs.103).aspx) для выполнения операции "Upsert". Поскольку метод `Seed` выполняется при каждой миграции, невозможно просто вставить данные, так как добавляемые строки уже будут существовать после первой миграции, которая создает базу данных. Операция "Upsert" предотвращает ошибки, которые могут возникать при попытке вставить уже существующую строку, но ***переопределяет*** любые изменения данных, которые могли быть сделаны при тестировании приложения. При использовании тестовых данных в некоторых таблицах может быть нежелательно: в некоторых случаях при изменении данных во время тестирования необходимо сохранить изменения после обновления базы данных. В этом случае необходимо выполнить операцию условной вставки: вставить строку, если она еще не существует. Метод SEED использует оба подхода.

    Первый параметр, передаваемый методу [AddOrUpdate](https://msdn.microsoft.com/library/system.data.entity.migrations.idbsetextensions.addorupdate(v=vs.103).aspx) , указывает свойство, используемое для проверки, существует ли уже строка. Для данных тестового учащегося, которые вы предоставляете, для этой цели можно использовать свойство `LastName`, так как каждое Последнее имя в списке является уникальным:

    [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample12.cs)]

    В этом коде предполагается, что последние имена являются уникальными. Если вы вручную добавите учащийся с дубликатом фамилии, вы получите следующее исключение при следующем выполнении миграции.

    Последовательность содержит более одного элемента

    Дополнительные сведения о методе `AddOrUpdate` см. в разделе о [методе EF 4,3 AddOrUpdate](http://thedatafarm.com/blog/data-access/take-care-with-ef-4-3-addorupdate-method/) в блоге Юлия Лерман.

    Код, добавляющий `Enrollment` сущности, не использует метод `AddOrUpdate`. Он проверяет, существует ли сущность, и вставляет сущность, если она не существует. Этот подход позволит сохранить изменения, вносимые в регистрацию при выполнении миграции. Код выполняет цикл по каждому элементу [списка](https://msdn.microsoft.com/library/6sh2ey19.aspx) `Enrollment`и если регистрация не найдена в базе данных, она добавляет регистрацию в базу данных. При первом обновлении базы данных она будет пустой, поэтому она добавит каждую регистрацию.

    [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample13.cs)]

    Сведения об отладке метода `Seed` и обработке избыточных данных, таких как два учащихся с именем "Александр Carson", см. в разделе [Заполнение и отладка Entity Framework (EF) баз данных](https://blogs.msdn.com/b/rickandy/archive/2013/02/12/seeding-and-debugging-entity-framework-ef-dbs.aspx) в блоге Рик Андерсон (.
2. Постройте проект.

### <a name="create-and-execute-the-first-migration"></a>Создание и выполнение первой миграции

1. В окне консоли диспетчера пакетов введите следующие команды: 

    [!code-powershell[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample14.ps1)]

    ![](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image13.png)

    Команда `add-migration` добавляет в папку миграции файл *[датестамп]\_InitialCreate.CS* , содержащий код, который создает базу данных. Первый параметр (`InitialCreate)` используется для имени файла и может быть любым нужным; обычно вы выбираете слово или фразу, которая суммирует данные, выполняемые при миграции. Например, вы можете присвоить более поздней миграции имя &quot;AddDepartmentTable&quot;.

    ![Папка миграций с начальной миграцией](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image14.png)

    Метод `Up` класса `InitialCreate` создает таблицы базы данных, соответствующие наборам сущностей модели данных, а метод `Down` удаляет их. Функция миграций вызывает метод `Up`, чтобы реализовать изменения модели данных для миграции. При вводе команды для отката обновления функция миграций вызывает метод `Down`. В следующем коде показано содержимое файла `InitialCreate`:

    [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample15.cs)]

    Команда `update-database` запускает метод `Up` для создания базы данных, а затем запускает метод `Seed` для заполнения базы данных.

Для модели данных создана SQL Serverная база данных. Имя базы данных — *ContosoUniversity*, а *MDF* -файл — в папке *\_данных приложения* проекта, так как это будет указано в строке подключения.

Для просмотра базы данных в Visual Studio можно использовать либо **Обозреватель сервера** , либо **Обозреватель объектов SQL Server** (SSOX). В этом учебнике используется **Обозреватель сервера**. В Visual Studio Express 2012 для Web **Обозреватель сервера** называется **Обозреватель базы данных**.

1. В меню **вид** выберите пункт **Обозреватель сервера**.
2. Щелкните значок **Добавить подключение** .

    ![](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image15.png)
3. При появлении запроса в диалоговом окне **Выбор источника данных** выберите **Microsoft SQL Server**и нажмите кнопку **продолжить**.  
  
    ![](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image16.png)
4. В диалоговом окне **Добавление соединения** введите **(LocalDB) \V11.0** в поле **имя сервера**. В поле **выберите или введите имя базы данных**выберите **ContosoUniversity.**  
  
    ![](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image17.png)
5. Нажмите кнопку **ОК**.
6. Разверните **SchoolContext** , а затем — **таблицы**.  
  
    ![](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image18.png)
7. Щелкните правой кнопкой мыши таблицу **Student** и выберите команду **Показать данные таблицы** , чтобы просмотреть созданные столбцы и строки, вставленные в таблицу.

    ![Таблица учащихся](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image19.png)

## <a name="creating-a-student-controller-and-views"></a>Создание контроллера и представлений учащихся

Следующим шагом является создание контроллера MVC ASP.NET и представлений в приложении, которые могут работать с одной из этих таблиц.

1. Чтобы создать контроллер `Student`, щелкните правой кнопкой мыши папку **Controllers** в **Обозреватель решений**, выберите **добавить**, а затем щелкните **контроллер**. В диалоговом окне **Добавление контроллера** выберите следующие параметры и нажмите кнопку **Добавить**. 

   - Имя контроллера: **студентконтроллер**.
   - Шаблон: **контроллер MVC с действиями чтения и записи и представлениями с использованием Entity Framework**.
   - Класс модели: **Student (ContosoUniversity. Models)** . (Если этот параметр не отображается в раскрывающемся списке, выполните сборку проекта и повторите попытку.)
   - Класс контекста данных: **SchoolContext (ContosoUniversity. Models)** .
   - Представления: **Razor (CSHTML)** . (Значение по умолчанию.)

     ![Add_Controller_dialog_box_for_Student_controller](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image20.png)
2. Visual Studio откроет файл *контроллерс\студентконтроллер.КС* . Вы видите, что создана переменная класса, которая создает экземпляр объекта контекста базы данных:

     [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample16.cs)]

     Метод действия `Index` возвращает список учащихся из набора сущностей *Student* , считывая свойство `Students` экземпляра контекста базы данных:

     [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample17.cs)]

     В представлении *студент\индекс.кштмл* этот список отображается в таблице:

     [!code-cshtml[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample18.cshtml)]
3. Нажмите клавиши CTRL+F5, чтобы запустить проект.

     Щелкните вкладку **students (учащиеся** ), чтобы просмотреть тестовые данные, вставленные методом `Seed`.

     ![Страница индекса учащихся](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image21.png)

## <a name="conventions"></a>Обозначения

Объем кода, который вам пришлось писать, чтобы Entity Framework мог создать полную базу данных для вас, является минимальным из-за использования *соглашений*или допущений, которые делает Entity Framework. Некоторые из них уже были отмечены:

- В качестве имен таблиц используются множественные формы имен классов сущностей.
- В качестве имен столбцов используются имена свойств сущностей.
- Свойства сущности с именами `ID` или *classname* `ID` распознаются как свойства первичного ключа.

Вы видели, что соглашения могут быть переопределены (например, вы указали, что имена таблиц не должны быть преобразованы в множественный вид), и вы узнаете больше о соглашениях и о том, как их переопределить в руководстве [Создание более сложной модели данных](creating-a-more-complex-data-model-for-an-asp-net-mvc-application.md) далее в этой серии. Дополнительные сведения см. в разделе [соглашения Code First](https://msdn.microsoft.com/data/jj679962).

## <a name="summary"></a>Сводка

Теперь вы создали простое приложение, которое использует Entity Framework и SQL Server Express для хранения и вывода данных. В следующем учебнике вы узнаете, как выполнять базовые операции CRUD (создание, чтение, обновление, удаление). Вы можете оставить отзыв в нижней части этой страницы. Сообщите нам, как вам нравится эта часть руководства, и как ее улучшить.

Ссылки на другие ресурсы Entity Framework можно найти в [карте содержимого ASP.NET Data Access](../../../../whitepapers/aspnet-data-access-content-map.md).

> [!div class="step-by-step"]
> [Вперед](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application.md)
