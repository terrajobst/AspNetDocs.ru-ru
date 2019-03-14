---
title: Учебник. Начало работы с EF Core в веб-приложении MVC ASP.NET
description: Это первый учебник из серии, в котором с самого начала описывается построение примера приложения для университета Contoso.
author: rick-anderson
ms.author: tdykstra
ms.custom: mvc
ms.date: 02/06/2019
ms.topic: tutorial
uid: data/ef-mvc/intro
ms.openlocfilehash: f7b557c8e560393ae886c46fad95c48ccbcc65b4
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57043471"
---
# <a name="tutorial-get-started-with-ef-core-in-an-aspnet-mvc-web-app"></a>Учебник. Начало работы с EF Core в веб-приложении MVC ASP.NET

[!INCLUDE [RP better than MVC](~/includes/RP-EF/rp-over-mvc.md)]

На примере веб-приложения Contoso University показано, как создавать веб-приложения MVC ASP.NET Core 2.2 с помощью Entity Framework (EF) Core 2.0 и Visual Studio 2017.

В этом примере приложения реализуется веб-сайт вымышленного университета Contoso. На нем предусмотрены различные функции, в том числе прием учащихся, создание курсов и назначение преподавателей. Это первый учебник из серии, в котором с самого начала описывается построение примера приложения для университета Contoso.

EF Core 2.0 — это последняя версия платформы EF, однако в ней реализованы еще не все возможности EF 6.x. Дополнительные сведения о выборе между платформами EF 6.x и EF Core см. в [этой статье](/ef/efcore-and-ef6/). Если вы используете платформу EF 6.x, ознакомьтесь с [предыдущей версией этой серии учебников](/aspnet/mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application).

> [!NOTE]
> Версия этого учебника для ASP.NET Core 1.1 и VS 2017 с обновлением 2 в формате PDF доступна [здесь](https://webpifeed.blob.core.windows.net/webpifeed/Partners/efmvc1.1.pdf).

В этом учебнике рассмотрены следующие задачи.

> [!div class="checklist"]
> * Создание веб-приложения MVC ASP.NET Core
> * Настройка стиля сайта
> * Дополнительные сведения о пакетах NuGet EF Core
> * Создание модели данных
> * Создание контекста базы данных
> * Регистрация SchoolContext
> * Инициализация базы данных с тестовыми данными
> * Создание контроллера и представлений
> * Просмотр базы данных

## <a name="prerequisites"></a>Предварительные требования

[!INCLUDE [](~/includes/net-core-prereqs.md)]

## <a name="troubleshooting"></a>Устранение неполадок

Если вы столкнулись с проблемами, для их решения можно попробовать сравнить свой код с кодом [готового проекта](https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-mvc/intro/samples/cu-final). Список распространенных ошибок и способы их устранения см. в [разделе "Устранение неполадок" последнего руководства серии](advanced.md#common-errors). Если вам не удалось найти нужную информацию, вы можете задать вопрос на сайте StackOverflow.com в разделах, посвященных [ASP.NET Core](https://stackoverflow.com/questions/tagged/asp.net-core) или [EF Core](https://stackoverflow.com/questions/tagged/entity-framework-core).

> [!TIP]
> Эта серия включает в себя 10 учебников, содержание каждого из которых базируется на предыдущих учебниках. После успешного завершения каждого руководства рекомендуется сохранять копию проекта. Таким образом, при возникновении проблем вы сможете вернуться к предыдущему учебнику, а не к началу серии.

## <a name="contoso-university-web-app"></a>Веб-приложение Contoso University

В рамках этих учебников вы будете создавать приложение, которое представляет собой простой веб-сайт университета.

Пользователи приложения могут просматривать и обновлять сведения об учащихся, курсах и преподавателях. Будет создано несколько экранов.

![Страница указателя учащихся](intro/_static/students-index.png)

![Страница редактирования учащихся](intro/_static/student-edit.png)

Стиль пользовательского интерфейса этого сайта практически полностью основан на встроенных шаблонах, поскольку это позволяет сосредоточиться на изучении и использовании возможностей платформы Entity Framework.

## <a name="create-aspnet-core-mvc-web-app"></a>Создание веб-приложения MVC ASP.NET Core

Откройте Visual Studio и создайте новый веб-проект ASP.NET Core C# с именем "ContosoUniversity".

* В меню **Файл** выберите пункт **Создать > Проект**.

* В области слева выберите **Установленные > Visual C# > Интернет**.

* Выберите шаблон проекта **Веб-приложение ASP.NET Core**.

* Введите имя **ContosoUniversity** и нажмите кнопку **ОК**.

  ![Диалоговое окно создания нового проекта](intro/_static/new-project2.png)

* Дождитесь появления диалогового окна **Создание веб-приложения ASP.NET Core (.NET Core)**.

  ![Диалоговое окно "Создание проекта ASP.NET Core"](intro/_static/new-aspnet2.png)

* Выберите **ASP.NET Core 2.2** и шаблон **Веб-приложение (Модель — представление — контроллер)**.

  **Примечание.** В этом руководстве используются версии ASP.NET Core 2.2 и EF Core 2.0 или выше.

* Убедитесь, что для параметра **Проверка подлинности** задано значение **Без проверки подлинности**.

* Нажмите кнопку **ОК**.

## <a name="set-up-the-site-style"></a>Настройка стиля сайта

Выполните незначительную настройку меню, макета и домашней страницы сайта.

Откройте файл *Views/Shared/_Layout.cshtml* и внесите следующие изменения:

* Замените все вхождения "ContosoUniversity" на "Contoso University". Таких элементов будет три.

* Добавьте пункты меню **About** (Сведения), **Students** (Учащиеся), **Courses** (Курсы), **Instructors** (Преподаватели) и **Departments** (Кафедры). Удалите пункт меню **Privacy** (Конфиденциальность).

Изменения выделены.

[!code-cshtml[](intro/samples/cu/Views/Shared/_Layout.cshtml?highlight=6,32-36,51)]

Замените содержимое файла *Views/Home/Index.cshtml* следующим кодом, который заменяет текст о ASP.NET и MVC описанием этого приложения:

[!code-cshtml[](intro/samples/cu/Views/Home/Index.cshtml)]

Нажмите клавиши CTRL+F5, чтобы запустить проект, и выберите в меню **Отладка > Запуск без отладки**. Откроется домашняя страница, на которой будут представлены созданные в рамках этих учебников вкладки.

![Домашняя страница университета Contoso](intro/_static/home-page.png)

## <a name="about-ef-core-nuget-packages"></a>Сведения о пакетах NuGet EF Core

Чтобы реализовать поддержку EF Core в проекте, установите поставщик целевой базы данных. В этом учебнике используется SQL Server, для которого требуется пакет поставщика [Microsoft.EntityFrameworkCore.SqlServer](https://www.nuget.org/packages/Microsoft.EntityFrameworkCore.SqlServer/). Этот пакет входит в [метапакет Microsoft.AspNetCore.App](xref:fundamentals/metapackage-app), поэтому если приложение уже содержит ссылку на пакет `Microsoft.AspNetCore.App`, ссылаться на него не нужно.

Этот пакет и его зависимости (`Microsoft.EntityFrameworkCore` и `Microsoft.EntityFrameworkCore.Relational`) обеспечивают поддержку среды выполнения для платформы EF. Пакет средств будет добавлен позднее в рамках учебника [Миграции](migrations.md).

Дополнительные сведения о других поставщиках баз данных, которые доступны для платформы Entity Framework Core, см. в разделе [Поставщики баз данных](/ef/core/providers/).

## <a name="create-the-data-model"></a>Создание модели данных

Теперь необходимо создать классы сущностей для приложения университета Contoso. Для начала создаются следующие три сущности.

![Схема модели данных "курс-регистрация-учащийся"](intro/_static/data-model-diagram.png)

Между сущностями `Student` и `Enrollment`, а также между сущностями `Course` и `Enrollment` существует отношение "один ко многим". Другими словами, учащийся может быть зарегистрирован в любом количестве курсов, а в отдельном курсе может быть зарегистрировано любое количество учащихся.

В следующих разделах создаются классы для каждой из этих сущностей.

### <a name="the-student-entity"></a>Сущность Student

![Схема сущности Student](intro/_static/student-entity.png)

В папке *Models* создайте файл класса с именем *Student.cs* и замените код шаблона следующим кодом.

[!code-csharp[](intro/samples/cu/Models/Student.cs?name=snippet_Intro)]

Свойство `ID` будет использоваться в качестве столбца первичного ключа в таблице базы данных, соответствующей этому классу. По умолчанию платформа Entity Framework интерпретирует в качестве первичного ключа свойство `ID` или `classnameID`.

Свойство `Enrollments` является [свойством навигации](/ef/core/modeling/relationships). Свойства навигации содержат другие сущности, связанные с этой сущностью. В этом случае свойство `Enrollments` сущности `Student entity` содержит все сущности `Enrollment`, которые связаны с этой сущностью `Student`. Другими словами, если с указанной строкой Student в базе данных связаны две строки Enrollment (строки, в столбце внешнего ключа StudentID которых содержится первичный ключ этого учащегося), в этой сущности `Student` свойство навигации `Enrollments` будет содержать две этих сущности `Enrollment`.

Если свойство навигации может содержать несколько сущностей (как в отношениях "многие ко многим" или "один ко многим"), оно должно иметь тип списка, допускающий добавление, удаление и обновление записей, такой как `ICollection<T>`. Вы можете указать тип `ICollection<T>` либо, например, тип `List<T>` или `HashSet<T>`. Если указан тип `ICollection<T>`, платформа EF по умолчанию создает коллекцию `HashSet<T>`.

### <a name="the-enrollment-entity"></a>Сущность Enrollment

![Схема сущности Enrollment](intro/_static/enrollment-entity.png)

В папке *Models* создайте файл *Enrollment.cs* и замените существующий код следующим кодом:

[!code-csharp[](intro/samples/cu/Models/Enrollment.cs?name=snippet_Intro)]

Свойство `EnrollmentID` будет использоваться в качестве первичного ключа. В этой сущности используется шаблон `classnameID` вместо `ID`, как в сущности `Student`. Как правило, следует выбирать один шаблон, который будет использоваться в рамках всей модели данных. В этом случае демонстрируется возможность использования любого из шаблонов. В [одном из следующих учебников](inheritance.md) вы узнаете, за счет чего использование идентификатора без имени класса позволяет упростить реализацию наследования в модели данных.

Свойство `Grade` имеет тип `enum`. Знак вопроса после объявления типа `Grade` указывает, что свойство `Grade` допускает значение null. Оценка со значением null отличается от нулевой оценки тем, что при таком значении оценка еще не известна или не назначена.

Свойство `StudentID` представляет собой внешний ключ. Ему соответствует свойство навигации `Student`. Сущность `Enrollment` связана с одной сущностью `Student`, поэтому это свойство может содержать одну сущность `Student` (в отличие от представленного ранее свойства навигации `Student.Enrollments`, которое может содержать несколько сущностей `Enrollment`).

Свойство `CourseID` представляет собой внешний ключ. Ему соответствует свойство навигации `Course`. Сущность `Enrollment` связана с одной сущностью `Course`.

Платформа Entity Framework интерпретирует свойство как свойство внешнего ключа, если оно имеет имя `<navigation property name><primary key property name>` (например, `StudentID` для свойства навигации `Student`, поскольку сущность `Student` имеет первичный ключ `ID`). Свойства внешнего ключа также могут называться просто `<primary key property name>` (например, `CourseID` поскольку сущность `Course` имеет первичный ключ `CourseID`).

### <a name="the-course-entity"></a>Сущность Course

![Схема сущности Course](intro/_static/course-entity.png)

В папке *Models* создайте файл *Course.cs* и замените существующий код следующим кодом:

[!code-csharp[](intro/samples/cu/Models/Course.cs?name=snippet_Intro)]

Свойство `Enrollments` является свойством навигации. Сущность `Course` может быть связана с любым числом сущностей `Enrollment`.

Более подробное описание атрибута `DatabaseGenerated` будет приведено в [одном из следующих учебников](complex-data-model.md) этой серии. Фактически, этот атрибут позволяет ввести первичный ключ для курса, а не использовать базу данных, чтобы создать его.

## <a name="create-the-database-context"></a>Создание контекста базы данных

Контекст базы данных — это основной класс, который координирует функциональные возможности Entity Framework для заданной модели данных. Этот класс создается путем наследования от класса `Microsoft.EntityFrameworkCore.DbContext`. В коде указываются сущности, которые включаются в модель данных. Также вы можете настроить реакцию платформы Entity Framework на некоторые события. В этом проекте соответствующий класс называется `SchoolContext`.

В папке проекта создайте папку *Data*.

В папке *Data* создайте новый файл класса с именем *SchoolContext.cs* и замените код шаблона следующим кодом:

[!code-csharp[](intro/samples/cu/Data/SchoolContext.cs?name=snippet_Intro)]

Этот код создает свойство `DbSet` для каждого набора сущностей. В терминологии Entity Framework набор сущностей обычно соответствует таблице базы данных, а сущность — строке в этой таблице.

Вы можете опустить инструкции `DbSet<Enrollment>` и `DbSet<Course>`. Это не нарушит функциональность. Платформа Entity Framework включает эти инструкции неявно, поскольку сущность `Student` ссылается на сущность `Enrollment`, а `Enrollment` ссылается на сущность `Course`.

При создании базы данных платформа EF создает таблицы с именами, соответствующими именам свойств в `DbSet`. Имена свойств для коллекций, как правило, задаются во множественном числе (например, Students вместо Student), однако единого мнения по поводу присвоения имен во множественном числе таблицам среди разработчиков не существует. В этих учебниках вместо принятого по умолчанию способа таблицам в DbContext присваиваются имена в единственном числе. Чтобы сделать это, добавьте выделенный ниже код после последнего свойства DbSet.

[!code-csharp[](intro/samples/cu/Data/SchoolContext.cs?name=snippet_TableNames&highlight=16-21)]

## <a name="register-the-schoolcontext"></a>Регистрация SchoolContext

ASP.NET Core по умолчанию реализует технологию [внедрения зависимостей](../../fundamentals/dependency-injection.md). С помощью внедрения зависимостей службы (например, контекст базы данных EF) регистрируются во время запуска приложения. Затем компоненты, которые используют эти службы (например, контроллеры MVC), обращаются к ним через параметры конструктора. Код конструктора контроллера, который получает экземпляр контекста, будет приведен позднее в этом учебнике.

Чтобы зарегистрировать `SchoolContext` как службу, откройте файл *Startup.cs* и добавьте выделенные строки в метод `ConfigureServices`.

[!code-csharp[](intro/samples/cu/Startup.cs?name=snippet_SchoolContext&highlight=3-4)]

Имя строки подключения передается в контекст путем вызова метода для объекта `DbContextOptionsBuilder`. При локальной разработке [система конфигурации ASP.NET Core](xref:fundamentals/configuration/index) считывает строку подключения из файла *appsettings.json*.

Добавьте инструкции `using` для пространств имен `ContosoUniversity.Data` и `Microsoft.EntityFrameworkCore`, после чего выполните построение проекта.

[!code-csharp[](intro/samples/cu/Startup.cs?name=snippet_Usings)]

Откройте файл *appsettings.json* и добавьте строку подключения, как показано в следующем примере.

[!code-json[](./intro/samples/cu/appsettings1.json?highlight=2-4)]

### <a name="sql-server-express-localdb"></a>SQL Server Express LocalDB

Строка подключения указывает на базу данных SQL Server LocalDB. LocalDB — это упрощенная версия ядра СУБД SQL Server Express, предназначенная для разработки приложений и не ориентированная на использование в производственной среде. LocalDB запускается по запросу в пользовательском режиме, поэтому настройки не слишком сложны. По умолчанию база данных LocalDB создает файлы *.mdf* в каталоге `C:/Users/<user>`.

## <a name="initialize-db-with-test-data"></a>Инициализация базы данных с тестовыми данными

Платформа Entity Framework создает пустую базу данных. В этом разделе вы напишете метод, который вызывается после создания базы данных и заполняет ее тестовыми данными.

Здесь будет использоваться метод `EnsureCreated` для автоматического создания базы данных. В [одном из следующих учебников](migrations.md) вы узнаете, как обрабатывать изменения модели с использованием Code First Migrations, что позволяет изменять схему базы данных вместо того, чтобы удалять и повторно создавать ее.

В папке *Data* создайте новый файл класса с именем *DbInitializer.cs* и замените код шаблона следующим кодом, который обеспечивает создание базы данных и загрузку в нее тестовых данных.

[!code-csharp[](intro/samples/cu/Data/DbInitializer.cs?name=snippet_Intro)]

Этот код проверяет, добавлены ли в базу данных учащиеся. Если нет, база данных считается новой и заполняется тестовыми данными. Для повышения производительности тестовые данные загружаются массивами, а не коллекциями `List<T>`.

В файле *Program.cs* измените метод `Main`, чтобы реализовать следующее поведение при запуске приложения:

* Получение экземпляра контекста базы данных из контейнера внедрения зависимостей.
* Вызов метода инициализации с передачей ему контекста.
* Высвобождение контекста после завершения работы метода заполнения.

[!code-csharp[](intro/samples/cu/Program.cs?name=snippet_Seed&highlight=3-20)]

Добавьте инструкции `using`:

[!code-csharp[](intro/samples/cu/Program.cs?name=snippet_Usings)]

В предыдущих учебниках аналогичный код использовался в методе `Configure` в файле *Startup.cs*. Мы рекомендуем использовать метод `Configure` только для настройки конвейера запросов. Код запуска приложения принадлежит методу `Main`.

Теперь при первом запуске приложения будет создана и заполнена тестовыми данными необходимая для работы база данных. При любом изменении модели данных вы можете удалить базу, обновить метод заполнения и начать работу с новой базой данных аналогичным способом. В следующих учебниках вы узнаете, как изменить базу данных при изменении модели данных, не прибегая к ее удалению и повторному созданию.

## <a name="create-controller-and-views"></a>Создание контроллера и представлений

Далее вы будете использовать механизм шаблонов Visual Studio для добавления контроллера и представлений MVC, которые будут использовать платформу EF для запроса данных и их сохранения.

Автоматическое создание методов и представлений операций CRUD (создание, чтение, обновление и удаление) называется формированием шаблонов. Формирование шаблонов отличается от создания кода тем, что шаблонный код является отправной точкой и может изменяться в соответствии с потребностями, тогда как сформированный код обычно не изменяется. В тех случаях, когда требуется настроить созданный код в соответствии с внесенными изменениями, вы можете использовать разделяемые классы или повторно создать код.

* Щелкните правой кнопкой мыши папку **Контроллеры** в **обозревателе решений** и выберите **Добавить > Создать шаблонный элемент**.

Если открывается диалоговое окно **Добавление зависимостей MVC**:

* [Обновите Visual Studio до последней версии](https://www.visualstudio.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017). Это диалоговое окно отображает версии Visual Studio, предшествующие 15.5.
* Если обновить не удается, выберите **ДОБАВИТЬ** и снова выполните шаги по добавлению контроллера.

* В диалоговом окне **Добавление шаблона**:

  * Выберите **Контроллер MVC с представлениями, использующий Entity Framework**.

  * Нажмите кнопку **Добавить**. Откроется диалоговое окно **добавления контроллера MVC с представлениями с использованием Entity Framework**.

    ![Шаблон Student](intro/_static/scaffold-student2.png)

  * В разделе **Класс модели** выберите **Student**.

  * В разделе **Класс контекста данных** выберите **SchoolContext**.

  * Оставьте предлагаемое по умолчанию имя **StudentsController**.

  * Нажмите кнопку **Добавить**.

  При нажатии кнопки **Добавить** подсистема формирования шаблонов Visual Studio создает файл *StudentsController.cs* и набор представлений (файлы с расширением *.cshtml*), которые будут работать с контроллером.

(Подсистема формирования шаблонов также может создать контекст базы данных, если вы не создали его вручную, как было показано ранее в этом учебнике. Вы можете задать новый класс контекста в диалоговом окне **Добавление контроллера**, нажав на значок плюса справа от раздела **Класс контекста данных**.  В этом случае Visual Studio создаст класс `DbContext`, а также контроллеры и представления.)

Обратите внимание, что контроллер принимает `SchoolContext` в качестве параметра конструктора.

[!code-csharp[](intro/samples/cu/Controllers/StudentsController.cs?name=snippet_Context&highlight=5,7,9)]

Технология внедрения зависимостей ASP.NET Core обеспечивает передачу экземпляра `SchoolContext` в контроллер. Это поведение было настроено ранее в файле *Startup.cs*.

Контроллер содержит метод действия `Index`, который отображает всех учащихся в базе данных. Этот метод получает список учащихся из набора сущностей Students, считывая свойство `Students` экземпляра контекста базы данных:

[!code-csharp[](intro/samples/cu/Controllers/StudentsController.cs?name=snippet_ScaffoldedIndex&highlight=3)]

Позднее в этом учебнике будут описаны элементы асинхронного программирования в этом коде.

Представление *Views/Students/Index.cshtml* отображает этот список в таблице:

[!code-cshtml[](intro/samples/cu/Views/Students/Index1.cshtml)]

Нажмите клавиши CTRL+F5, чтобы запустить проект, и выберите в меню **Отладка > Запуск без отладки**.

Перейдите на вкладку Students (Учащиеся), чтобы просмотреть тестовые данные, добавленные методом `DbInitializer.Initialize`. В зависимости от размеров окна браузера ссылку на вкладку `Student` можно найти вверху страницы или щелкнув значок навигации в правом верхнем углу.

![Уменьшенное окно с домашней страницей университета Contoso](intro/_static/home-page-narrow.png)

![Страница указателя учащихся](intro/_static/students-index.png)

## <a name="view-the-database"></a>Просмотр базы данных

При запуске приложения метод `DbInitializer.Initialize` вызывает метод `EnsureCreated`. Платформа EF определяет, что база данных отсутствует, и создает ее, после чего код в оставшейся части метода `Initialize` заполняет базу данными. Для просмотра базы данных в Visual Studio можно использовать **обозреватель объектов SQL Server** (SSOX).

Закройте браузер.

Если окно SSOX не открылось, выберите его в меню **Вид** Visual Studio.

В окне SSOX щелкните **(localdb)\MSSQLLocalDB > Базы данных** и затем щелкните запись базы данных, имя которой указано в строке подключения в вашем файле *appsettings.json*.

Разверните узел **Таблицы**, чтобы просмотреть представленные в базе таблицы.

![Таблицы в SSOX](intro/_static/ssox-tables.png)

Щелкните правой кнопкой мыши таблицу **Student** и выберите пункт **Просмотр данных**, чтобы просмотреть созданные столбцы и строки, вставленные в базу данных.

![Таблица Student в SSOX](intro/_static/ssox-student-table.png)

Файлы базы данных с расширением <em>MDF</em> и <em>LDF</em> располагаются в папке <em>C:\Users\\<yourusername></em>.

Поскольку вы вызываете метод `EnsureCreated` в методе инициализатора, который выполняется при запуске приложения, теперь вы можете внести изменения в класс `Student`, удалить базу данных и снова запустить приложение. После этого база данных будет создана повторно в соответствии с внесенными изменениями. Например, при добавлении свойства `EmailAddress` в класс `Student` во вновь созданной таблице появится столбец `EmailAddress`.

## <a name="conventions"></a>Соглашения

Чтобы платформа Entity Framework автоматически создавала полную базу данных на основе принятых соглашений и допущений, потребуется написать минимальный объем кода.

* В качестве имен таблиц используются имена свойств `DbSet`. Для сущностей, на которые не ссылается свойство `DbSet`, в качестве имен таблиц используются имена классов сущностей.

* В качестве имен столбцов используются имена свойств сущностей.

* Свойства сущностей с именем ID или classnameID распознаются как свойства первичного ключа.

* Свойство интерпретируется как свойство внешнего ключа, если оно имеет имя *<navigation property name><primary key property name>* (например, `StudentID` для свойства навигации `Student`, так как сущность `Student` имеет первичный ключ `ID`). Свойства внешнего ключа также могут называться просто *<primary key property name>* (например `EnrollmentID`, поскольку сущность `Enrollment` имеет первичный ключ `EnrollmentID`).

Стандартное поведение можно переопределить. Например, можно явно задать имена таблиц, как было показано ранее в этом учебнике. Также можно указать имена столбцов и задать любое свойство в качестве первичного или внешнего ключа, как будет показано в [одном из следующих учебников](complex-data-model.md) этой серии.

## <a name="asynchronous-code"></a>Асинхронный код

Асинхронное программирование по умолчанию применяется в ASP.NET Core и EF Core.

Веб-сервер имеет ограниченное число потоков, поэтому при высокой загрузке могут использоваться все доступные потоки. В таких случаях сервер не может обрабатывать новые запросы до тех пор, пока не будут высвобождены потоки. В синхронном коде многие потоки могут быть заняты, не выполняя при этом какие-либо операции и ожидая завершения ввода-вывода. В асинхронном коде в то время, когда процесс ожидает завершения ввода-вывода, его поток высвобождается и может использоваться сервером для обработки других запросов. Таким образом, асинхронный код позволяет более эффективно использовать ресурсы сервера, который может обрабатывать больше трафика без задержек.

Во время выполнения асинхронный код использует немного больше служебных ресурсов, однако при низком объеме трафика этим можно пренебречь. Тем не менее в случае большого объема трафика это дает существенный выигрыш в производительности.

В следующем коде для асинхронного выполнения используются ключевое слово `async`, возвращаемое значение `Task<T>`, ключевое слово `await` и метод `ToListAsync`.

[!code-csharp[](intro/samples/cu/Controllers/StudentsController.cs?name=snippet_ScaffoldedIndex)]

* Ключевое слово `async` указывает компилятору создавать обратные вызовы для частей тела метода и автоматически создавать возвращаемый объект `Task<IActionResult>`.

* Тип возвращаемого значения `Task<IActionResult>` представляет текущую операцию с помощью результата типа `IActionResult`.

* Ключевое слово `await` предписывает компилятору разделить метод на две части. Первая часть завершается операцией, которая запускается в асинхронном режиме. Вторая часть помещается в метод обратного вызова, который вызывается при завершении операции.

* `ToListAsync` является асинхронной версией метода расширения `ToList`.

При написании асинхронного кода, который использует Entity Framework, необходимо учитывать некоторые моменты:

* Асинхронно выполняются только те инструкции, в результате которых в базу данных отправляются запросы или команды. К ним относятся, например, `ToListAsync`, `SingleOrDefaultAsync` и `SaveChangesAsync`. В их число не входят, например, инструкции, которые просто изменяют `IQueryable`, такие как `var students = context.Students.Where(s => s.LastName == "Davolio")`.

* Контекст EF не является потокобезопасным, поэтому не следует пытаться выполнять несколько операций параллельно. При вызове любого асинхронного метода EF всегда используйте ключевое слово `await`.

* Если вы хотите использовать преимущества в производительности, которые обеспечивает асинхронный код, убедитесь, что все используемые пакеты библиотек (например, для разбиения на страницы) также используют асинхронный код при вызове любых методов Entity Framework, выполняющих запросы к базе данных.

Дополнительные сведения об асинхронных методах программирования в .NET см. в разделе [Обзор асинхронной модели](/dotnet/articles/standard/async).

## <a name="get-the-code"></a>Получение кода

[Скачайте или ознакомьтесь с готовым приложением.](https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-mvc/intro/samples/cu-final)

## <a name="next-steps"></a>Следующие шаги

В этом учебнике рассмотрены следующие задачи.

> [!div class="checklist"]
> * Создание веб-приложения MVC ASP.NET Core
> * Настройка стиля сайта
> * Дополнительные сведения о пакетах NuGet EF Core
> * Создание модели данных
> * Создание контекста базы данных
> * Регистрация SchoolContext
> * Инициализация базы данных с тестовыми данными
> * Создание контроллера и представлений
> * Просмотр базы данных

В следующем учебнике вы узнаете, как выполнять основные операции CRUD (создание, чтение, обновление и удаление).

В следующем руководстве описано, как выполнять основные операции CRUD (создание, чтение, обновление и удаление).
> [!div class="nextstepaction"]
> [Реализация базовых функций CRUD](crud.md)