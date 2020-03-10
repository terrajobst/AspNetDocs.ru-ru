---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application
title: Реализация шаблонов репозитория и единиц работы в приложении ASP.NET MVC (9 из 10) | Документация Майкрософт
author: tdykstra
description: Пример веб-приложения Contoso университета демонстрирует создание приложений ASP.NET MVC 4 с помощью Entity Framework 5 Code First и Visual Studio...
ms.author: riande
ms.date: 07/30/2013
ms.assetid: 44761193-04ba-4990-9f90-145d3c10a716
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 18de9b125ee5d10795b9ce1a366918dadf4fc4e3
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78434382"
---
# <a name="implementing-the-repository-and-unit-of-work-patterns-in-an-aspnet-mvc-application-9-of-10"></a>Реализация шаблонов репозитория и единиц работы в приложении ASP.NET MVC (9 из 10)

от [Tom Dykstra)](https://github.com/tdykstra)

[Скачать завершенный проект](https://code.msdn.microsoft.com/Getting-Started-with-dd0e2ed8)

> Пример веб-приложения Contoso университета демонстрирует создание приложений ASP.NET MVC 4 с помощью Entity Framework 5 Code First и Visual Studio 2012. Сведения о серии руководств см. в [первом руководстве серии](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md). Вы можете начать серию руководств с начала или [скачать начальный проект для этой главы](building-the-ef5-mvc4-chapter-downloads.md) и начать отсюда.
> 
> > [!NOTE] 
> > 
> > Если проблема не устранена, [Скачайте готовую главу](building-the-ef5-mvc4-chapter-downloads.md) и попытайтесь воспроизвести проблему. Как правило, решение проблемы можно найти, сравнив код с завершенным кодом. Некоторые распространенные ошибки и способы их устранения см. в разделе [ошибки и обходные пути.](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)

В предыдущем учебном курсе было использовано наследование для сокращения избыточного кода в `Student` и `Instructor` классов сущностей. В этом учебнике вы увидите несколько способов использования шаблонов репозитория и единиц работы для операций CRUD. Как и в предыдущем учебнике, в этом случае вы измените способ работы кода с уже созданными страницами, а не создавайте новые страницы.

## <a name="the-repository-and-unit-of-work-patterns"></a>Шаблоны репозитория и единиц работы

Шаблоны репозитория и единиц работы предназначены для создания слоя абстракции между уровнем доступа к данным и уровнем бизнес-логики приложения. Реализация таких шаблонов позволяет изолировать приложение от изменений в хранилище данных и упрощает автоматическое модульное тестирование или разработку на основе тестирования.

В этом учебнике вы реализуете класс репозитория для каждого типа сущности. Для `Student` типа сущности вы создадите интерфейс репозитория и класс репозитория. При создании экземпляра репозитория в контроллере будет использоваться интерфейс, чтобы контроллер принял ссылку на любой объект, реализующий интерфейс репозитория. Когда контроллер запускается на веб-сервере, он получает репозиторий, который работает с Entity Framework. Когда контроллер запускается в классе модульного теста, он получает репозиторий, который работает с данными, сохраненными таким образом, что можно легко управлять для тестирования, например в коллекции в памяти.

Далее в этом руководстве вы будете использовать несколько репозиториев и класс единиц работы для `Course` и `Department` типов сущностей в контроллере `Course`. Класс единиц работы координирует работу нескольких репозиториев, создавая один класс контекста базы данных, общий для всех. Если вы хотите иметь возможность выполнять автоматическое модульное тестирование, вы создадите и используете интерфейсы для этих классов так же, как и для репозитория `Student`. Тем не менее, чтобы упростить учебник, вы создадите и используете эти классы без интерфейсов.

На следующем рисунке показан один из способов концептуализировать связей между классами контроллера и контекста по сравнению с тем, чтобы не использовать шаблон репозитория или единицы работы вообще.

![Repository_pattern_diagram](https://asp.net/media/2578149/Windows-Live-Writer_8c4963ba1fa3_CE3B_Repository_pattern_diagram_1df790d3-bdf2-4c11-9098-946ddd9cd884.png)

В этой серии руководств не создаются модульные тесты. Общие сведения о TDD с приложением MVC, которое использует шаблон репозитория, см. в разделе [Пошаговое руководство. Использование TDD с ASP.NET MVC](https://msdn.microsoft.com/library/ff847525.aspx). Дополнительные сведения о шаблоне репозитория см. в следующих ресурсах:

- [Шаблон репозитория](https://msdn.microsoft.com/library/ff649690.aspx) на сайте MSDN.
- [Использование шаблонов репозитория и единиц работы с Entity Framework 4,0](https://blogs.msdn.com/b/adonet/archive/2009/06/16/using-repository-and-unit-of-work-patterns-with-entity-framework-4-0.aspx) в блоге группы Entity Framework.
- В блоге Юлия Лерман, посвященном [хранилищу гибких публикаций Entity Framework 4](http://thedatafarm.com/blog/data-access/agile-entity-framework-4-repository-part-1-model-and-poco-classes/) .
- [Создание учетной записи с помощью приложения HTML5/jQuery](https://weblogs.asp.net/dwahlin/archive/2011/08/15/building-the-account-at-a-glance-html5-jquery-application.aspx) в блоге «вахлин».

> [!NOTE]
> Существует множество способов реализации шаблонов репозитория и единиц работы. Классы репозитория можно использовать с классом единиц работы или без него. Можно реализовать один репозиторий для всех типов сущностей или по одному для каждого типа. При реализации по одному для каждого типа можно использовать отдельные классы, универсальный базовый класс и производные классы, а также абстрактный базовый класс и производные классы. Вы можете включить бизнес-логику в репозиторий или ограничить ее логикой доступа к данным. Также можно создать слой абстракции в классе контекста базы данных, используя интерфейсы [идбсет](https://msdn.microsoft.com/library/gg679233(v=vs.103).aspx) вместо типов [DbSet](https://msdn.microsoft.com/library/system.data.entity.dbset(v=vs.103).aspx) для наборов сущностей. Подход к реализации слоя абстракции, приведенный в этом учебнике, является одним из вариантов, которые следует учитывать, а не рекомендациям для всех сценариев и сред.

## <a name="creating-the-student-repository-class"></a>Создание класса репозитория учащихся

В папке *DAL* создайте файл класса с именем *IStudentRepository.CS* и замените существующий код следующим кодом:

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample1.cs)]

Этот код объявляет типичный набор методов CRUD, включая два метода чтения — один, который возвращает все `Student` сущности и один `Student` сущность по ИДЕНТИФИКАТОРу.

В папке *DAL* создайте файл класса с именем *StudentRepository.CS* File. Замените существующий код следующим кодом, который реализует интерфейс `IStudentRepository`:

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample2.cs)]

Контекст базы данных определен в переменной класса, и конструктору требуется передать вызывающий объект в экземпляр контекста:

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample3.cs)]

Можно создать новый контекст в репозитории, но если вы использовали несколько репозиториев в одном контроллере, каждый из них будет иметь отдельный контекст. Позже вы будете использовать несколько репозиториев в контроллере `Course`, и вы увидите, как класс единиц работы может гарантировать, что все репозитории будут использовать один и тот же контекст.

Репозиторий реализует интерфейс [IDisposable](https://msdn.microsoft.com/library/system.idisposable.aspx) и удаляет контекст базы данных, как показано ранее в контроллере, и его методы CRUD выполняют вызовы к контексту базы данных так же, как вы видели ранее.

## <a name="change-the-student-controller-to-use-the-repository"></a>Изменение контроллера учащихся для использования репозитория

В *StudentController.CS*замените код, находящегося в классе, следующим кодом. Изменения выделены.

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample4.cs?highlight=13-18,44,75,77,102-103,120,137-138,159,172-174,186)]

Теперь контроллер объявляет переменную класса для объекта, реализующего интерфейс `IStudentRepository`, а не класс контекста:

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample5.cs)]

Конструктор по умолчанию (без параметров) создает новый экземпляр контекста, а необязательный конструктор позволяет вызывающему объекту передать экземпляр контекста.

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample6.cs)]

(Если бы вы использовали *внедрение зависимостей*или di, конструктор по умолчанию не нужен, поскольку программное обеспечение на языке di гарантирует, что всегда будет предоставляться правильный объект репозитория.)

В методах CRUD репозиторий теперь вызывается вместо контекста:

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample7.cs)]

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample8.cs)]

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample9.cs)]

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample10.cs)]

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample11.cs)]

После этого метод `Dispose` удаляет репозиторий вместо контекста:

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample12.cs)]

Запустите сайт и перейдите на вкладку **students (учащиеся** ).

![Students_Index_page](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/_static/image1.png)

Страница выглядит и работает так же, как и до изменения кода для использования репозитория, а другие страницы учащихся также работают. Однако существует важное различие в том, как метод `Index` контроллера выполняет фильтрацию и упорядочение. Исходная версия этого метода содержала следующий код:

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample13.cs?highlight=1)]

Обновленный метод `Index` содержит следующий код:

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample14.cs?highlight=1)]

Изменен только выделенный код.

В исходной версии кода `students` типизирован как объект `IQueryable`. Запрос не отправляется в базу данных, пока не будет преобразован в коллекцию с помощью метода, такого как `ToList`, который не происходит до тех пор, пока представление индекса не попытается получить доступ к модели учащихся. Метод `Where` в исходном коде выше становится предложением `WHERE` в SQL-запросе, который отправляется в базу данных. Это, в свою очередь, означает, что база данных возвращает только выбранные сущности. Однако в результате изменения `context.Students` в `studentRepository.GetStudents()`, переменная `students` после этой инструкции является коллекцией `IEnumerable`, включающей всех учащихся в базе данных. Конечный результат применения метода `Where` тот же, но теперь работа выполняется в памяти на веб-сервере, а не в базе данных. Для запросов, возвращающих большие объемы данных, это может оказаться неэффективным.

> [!TIP]
> 
> **IQueryable и IEnumerable**
> 
> После реализации репозитория, как показано здесь, даже при вводе чего-либо в поле **поиска** запрос, отправленный SQL Server возвращает все строки учащихся, так как не включает условия поиска:
> 
> ![](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/_static/image2.png)
> 
> [!code-sql[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample15.sql)]
> 
> Этот запрос возвращает все данные учащегося, так как репозиторий выполнил запрос без знания условий поиска. Процесс сортировки, применения условий поиска и выбора подмножества данных для разбиения на страницы (в данном случае отображение всего 3 строк) выполняется в памяти позже, когда вызывается метод `ToPagedList` в коллекции `IEnumerable`.
> 
> В предыдущей версии кода (до реализации репозитория) запрос не отправляется в базу данных до тех пор, пока не будут применены условия поиска, когда `ToPagedList` вызывается для объекта `IQueryable`.
> 
> ![](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/_static/image3.png)
> 
> При вызове Топажедлист для объекта `IQueryable` запрос, отправленный в SQL Server, указывает строку поиска, и в результате возвращаются только строки, удовлетворяющие условию поиска, и в памяти не нужно выполнять фильтрацию.
> 
> [!code-sql[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample16.sql)]
> 
> (В следующем учебнике объясняется, как анализировать запросы, отправленные в SQL Server.)

В следующем разделе показано, как реализовать методы репозитория, позволяющие указать, что эта работа должна выполняться базой данных.

Теперь вы создали слой абстракции между контроллером и контекстом базы данных Entity Framework. Если вы собираетесь выполнять автоматическое модульное тестирование с помощью этого приложения, можно создать альтернативный класс репозитория в проекте модульного теста, который реализует `IStudentRepository` *.* Вместо того чтобы вызывать контекст для чтения и записи данных, этот макет класса репозитория может управлять коллекциями в памяти для тестирования функций контроллера.

## <a name="implement-a-generic-repository-and-a-unit-of-work-class"></a>Реализация универсального репозитория и класса единиц работы

Создание класса репозитория для каждого типа сущности может привести к созданию большого объема избыточного кода, что может привести к частичному обновлению. Например, предположим, что необходимо обновить два разных типа сущностей в рамках одной транзакции. Если каждый из них использует отдельный экземпляр контекста базы данных, один может завершиться успешно, а другой может произойти сбой. Одним из способов сворачивания избыточного кода является использование универсального репозитория и один из способов убедиться, что все репозитории используют один и тот же контекст базы данных (и, таким образом, согласовывая все обновления), — использовать класс единиц работы.

В этом разделе руководства вы создадите класс `GenericRepository` и класс `UnitOfWork` и будете использовать их в контроллере `Course` для доступа к наборам сущностей `Department` и `Course`. Как было сказано ранее, для упрощения этой части учебника не создаются интерфейсы для этих классов. Но если вы собираетесь использовать их для упрощения TDD, обычно их можно реализовать с помощью интерфейсов так же, как и в репозитории `Student`.

### <a name="create-a-generic-repository"></a>Создание универсального репозитория

В папке *DAL* создайте *GenericRepository.CS* и замените существующий код следующим кодом:

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample17.cs)]

Переменные класса объявляются для контекста базы данных и для набора сущностей, для которого создается экземпляр репозитория.

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample18.cs)]

Конструктор принимает экземпляр контекста базы данных и инициализирует переменную набора сущностей:

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample19.cs)]

В методе `Get` используются лямбда-выражения, позволяющие вызывающему коду задавать условие фильтра и столбец для упорядочивания результатов по, а параметр строки позволяет вызывающему объекту предоставить список свойств навигации с разделителями-запятыми для безотлагательной загрузки:

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample20.cs)]

Код `Expression<Func<TEntity, bool>> filter` означает, что вызывающий объект предоставит лямбда-выражение на основе типа `TEntity`, и это выражение возвратит логическое значение. Например, если создается экземпляр репозитория для `Student` типа сущности, код в вызывающем методе может указать `student => student.LastName == "Smith`&quot; для параметра `filter`.

Код `Func<IQueryable<TEntity>, IOrderedQueryable<TEntity>> orderBy` также означает, что вызывающий объект предоставит лямбда-выражение. Но в этом случае входными данными для выражения является объект `IQueryable` для `TEntity` типа. Выражение возвратит упорядоченную версию этого `IQueryable` объекта. Например, если создается экземпляр репозитория для `Student` типа сущности, код в вызывающем методе может указать `q => q.OrderBy(s => s.LastName)` для параметра `orderBy`.

Код в методе `Get` создает объект `IQueryable`, а затем применяет критерий фильтра, если таковой имеется:

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample21.cs)]

Далее он применяет выражения с упреждающим загрузкой после синтаксического анализа списка с разделителями-запятыми:

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample22.cs)]

Наконец, он применяет выражение `orderBy`, если оно имеется, и возвращает результаты. в противном случае он возвращает результаты неупорядоченного запроса:

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample23.cs)]

При вызове метода `Get` можно выполнять фильтрацию и сортировку коллекции `IEnumerable`, возвращаемой методом, а не предоставлять параметры для этих функций. Но после этого работа по сортировке и фильтрации будет осуществляться в памяти на веб-сервере. Используя эти параметры, вы гарантируете, что работа будет выполняться базой данных, а не веб-сервером. Альтернативой является создание производных классов для конкретных типов сущностей и добавление специализированных методов `Get`, таких как `GetStudentsInNameOrder` или `GetStudentsByName`. Однако в сложном приложении это может привести к созданию большого количества таких производных классов и специализированных методов, которые могут оказаться более сложными для обслуживания.

Код в методах `GetByID`, `Insert`и `Update` похож на тот, который вы видели в неуниверсальном репозитории. (Вы не предоставляете параметр безотлагательной загрузки в сигнатуре `GetByID`, так как не удается выполнить неудачную загрузку с помощью метода `Find`.)

Для метода `Delete` предоставляются две перегрузки:

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample24.cs)]

Один из них позволяет передать только идентификатор удаляемой сущности, а другой — экземпляр сущности. Как было показано в учебнике [Обработка параллелизма](../../getting-started/getting-started-with-ef-using-mvc/handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md) , для обработки параллелизма необходим метод `Delete`, принимающий экземпляр сущности, включающий исходное значение свойства отслеживания.

Этот универсальный репозиторий будет выполнять стандартные требования CRUD. Если определенный тип сущности имеет особые требования, например более сложную фильтрацию или упорядочение, можно создать производный класс, содержащий дополнительные методы для этого типа.

## <a name="creating-the-unit-of-work-class"></a>Создание класса единиц работы

Класс единиц работы играет одну цель: чтобы убедиться, что при использовании нескольких репозиториев они совместно используют один контекст базы данных. Таким образом, при завершении единицы работы можно вызвать метод `SaveChanges` для этого экземпляра контекста и гарантировать, что все связанные изменения будут согласовываться. Все, что требуется классу, — это `Save` метод и свойство для каждого репозитория. Каждое свойство репозитория возвращает экземпляр репозитория, экземпляр которого был создан с использованием того же экземпляра контекста базы данных, что и другие экземпляры репозитория.

В папке *DAL* создайте файл класса с именем *UnitOfWork.CS* и замените код шаблона следующим кодом:

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample25.cs)]

Код создает переменные класса для контекста базы данных и каждого репозитория. Для переменной `context` создается экземпляр нового контекста:

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample26.cs)]

Каждое свойство репозитория проверяет, существует ли уже репозиторий. В противном случае он создает экземпляр репозитория, передавая ему экземпляр контекста. В результате все репозитории совместно используют один и тот же экземпляр контекста.

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample27.cs)]

Метод `Save` вызывает `SaveChanges` в контексте базы данных.

Как и любой класс, создающий экземпляр контекста базы данных в переменной класса, `UnitOfWork` класс реализует `IDisposable` и удаляет контекст.

### <a name="changing-the-course-controller-to-use-the-unitofwork-class-and-repositories"></a>Изменение контроллера курса для использования класса и репозиториев Унитофворк

Замените код, который в данный момент находится в *CourseController.CS* , на следующий код:

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample28.cs?highlight=15,20,22,31,54-55,70,85-86,101-102,122-124,130)]

Этот код добавляет переменную класса для класса `UnitOfWork`. (Если бы вы использовали здесь интерфейсы, вы не будете инициализировать переменную здесь; вместо этого нужно реализовать шаблон двух конструкторов так же, как и для репозитория `Student`.)

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample29.cs)]

В остальной части класса все ссылки на контекст базы данных заменяются ссылками на соответствующий репозиторий с использованием `UnitOfWork` свойств для доступа к репозиторию. Метод `Dispose` уничтожает экземпляр `UnitOfWork`.

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample30.cs)]

Запустите сайт и перейдите на вкладку **курсы** .

![Courses_Index_page](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/_static/image4.png)

Страница выглядит и работает так же, как и до внесения изменений, а другие страницы курса также работают одинаково.

## <a name="summary"></a>Сводка

Теперь вы реализовали шаблоны репозитория и единицы работы. Вы использовали лямбда-выражения в качестве параметров метода в универсальном репозитории. Дополнительные сведения об использовании этих выражений с объектом `IQueryable` см. в разделе [интерфейс IQueryable (t) (System. LINQ)](https://msdn.microsoft.com/library/bb351562.aspx) в библиотеке MSDN. В следующем учебном курсе вы узнаете, как работать с некоторыми расширенными сценариями.

Ссылки на другие ресурсы Entity Framework можно найти в [карте содержимого ASP.NET Data Access](../../../../whitepapers/aspnet-data-access-content-map.md).

> [!div class="step-by-step"]
> [Назад](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application.md)
> [Вперед](advanced-entity-framework-scenarios-for-an-mvc-web-application.md)
