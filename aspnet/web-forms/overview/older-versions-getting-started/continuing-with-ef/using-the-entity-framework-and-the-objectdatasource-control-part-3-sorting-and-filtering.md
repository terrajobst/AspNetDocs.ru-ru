---
uid: web-forms/overview/older-versions-getting-started/continuing-with-ef/using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering
title: Использование Entity Framework 4,0 и элемента управления ObjectDataSource, часть 3. Сортировка и фильтрация | Документация Майкрософт
author: tdykstra
description: Эта серия руководств основана на веб-приложении университета Contoso, которое создается начало работы с руководством по Entity Framework 4,0. Он...
ms.author: riande
ms.date: 01/26/2011
ms.assetid: 2990bd10-590d-43d5-9529-6b503ce5455d
msc.legacyurl: /web-forms/overview/older-versions-getting-started/continuing-with-ef/using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering
msc.type: authoredcontent
ms.openlocfilehash: 603120864528b9a5ff81214270eb9a7f1b68b347
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78512718"
---
# <a name="using-the-entity-framework-40-and-the-objectdatasource-control-part-3-sorting-and-filtering"></a>Использование Entity Framework 4,0 и элемента управления ObjectDataSource, часть 3. Сортировка и фильтрация

от [Tom Dykstra)](https://github.com/tdykstra)

> Эта серия руководств основана на веб-приложении университета Contoso, которое создается [Начало работы с руководством по Entity Framework 4,0](https://asp.net/entity-framework/tutorials#Getting%20Started) . Если вы не выполнили предыдущие учебники, в качестве отправной точки для этого учебника вы можете скачать созданное [приложение](https://code.msdn.microsoft.com/ASPNET-Web-Forms-97f8ee9a) . Вы также можете [скачать приложение](https://code.msdn.microsoft.com/ASPNET-Web-Forms-6c7197aa) , созданное с помощью полной серии руководств. Если у вас есть вопросы о учебниках, их можно опубликовать на [форуме ASP.NET Entity Framework](https://forums.asp.net/1227.aspx).

В предыдущем руководстве вы реализовали шаблон репозитория в многоуровневом веб-приложении, которое использует Entity Framework и элемент управления `ObjectDataSource`. В этом учебнике показано, как выполнять сортировку и фильтрацию и обработку сценариев "основной/подробности". Вы добавите следующие усовершенствования на страницу *Departments. aspx* :

- Текстовое поле, позволяющее пользователям выбирать отделы по имени.
- Список курсов для каждого отдела, показанного в сетке.
- Возможность сортировки путем щелчка заголовков столбцов.

[![image01](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image2.png)](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image1.png)

## <a name="adding-the-ability-to-sort-gridview-columns"></a>Добавление возможности сортировки столбцов GridView

Откройте страницу *departmentss. aspx* и добавьте атрибут `SortParameterName="sortExpression"` в элемент управления `ObjectDataSource` с именем `DepartmentsObjectDataSource`. (Позже вы создадите метод `GetDepartments`, который принимает параметр с именем `sortExpression`.) Разметка для открывающего тега элемента управления теперь напоминает следующий пример.

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample1.aspx)]

Добавьте атрибут `AllowSorting="true"` в открывающий тег элемента управления `GridView`. Разметка для открывающего тега элемента управления теперь напоминает следующий пример.

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample2.aspx)]

В *Departments.aspx.CS*задайте порядок сортировки по умолчанию, вызвав метод `Sort` `GridView` элемента управления из метода `Page_Load`:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample3.cs)]

Можно добавить код, который сортирует или фильтрует либо в классе бизнес-логики, либо в классе репозитория. Если сделать это в классе бизнес-логики, работа по сортировке или фильтрации будет выполнена после извлечения данных из базы данных, так как класс бизнес-логики работает с объектом `IEnumerable`, возвращенным репозиторием. Если добавить в класс репозитория код сортировки и фильтрации и сделать это до того, как выражение LINQ или запрос к объекту были преобразованы в `IEnumerable` объект, команды будут переданы в базу данных для обработки, что, как правило, более эффективно. В этом учебнике вы реализуете сортировку и фильтрацию таким образом, чтобы обработка была выполнена базой данных, т. е. в репозитории.

Чтобы добавить возможность сортировки, необходимо добавить новый метод в интерфейс репозитория и классы репозитория, а также в класс бизнес-логики. В файле *ISchoolRepository.CS* добавьте новый метод `GetDepartments`, который принимает `sortExpression` параметр, который будет использоваться для сортировки списка возвращаемых отделов:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample4.cs)]

В параметре `sortExpression` будет указан столбец для сортировки и направление сортировки.

Добавьте код для нового метода в файл *SchoolRepository.CS* :

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample5.cs)]

Измените существующий метод `GetDepartments` без параметров, чтобы вызвать новый метод:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample6.cs)]

В тестовом проекте добавьте следующий новый метод в *MockSchoolRepository.CS*:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample7.cs)]

Если вы собираетесь создавать модульные тесты, зависящие от этого метода, возвращающего отсортированный список, необходимо отсортировать список перед его возвратом. Вы не создадите такие тесты, как в этом руководстве, поэтому метод может просто возвратить Несортированный список отделов.

В файле *SchoolBL.CS* добавьте следующий новый метод в класс бизнес-логики:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample8.cs)]

Этот код передает параметр Sort методу репозитория.

Запустите страницу *departmentss. aspx* .

[![Image02](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image4.png)](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image3.png)

Теперь можно щелкнуть заголовок любого столбца, чтобы выполнить сортировку по этому столбцу. Если столбец уже отсортирован, щелчок заголовка меняет направление сортировки на противоположное.

## <a name="adding-a-search-box"></a>Добавление поля поиска

В этом разделе вы добавите текстовое поле поиска, свяжете его с элементом управления `ObjectDataSource`, используя параметр элемента управления, и добавите метод в класс бизнес-логики для поддержки фильтрации.

Откройте страницу *departmentss. aspx* и добавьте следующую разметку между заголовком и первым элементом управления `ObjectDataSource`:

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample9.aspx)]

В элементе управления `ObjectDataSource` с именем `DepartmentsObjectDataSource`выполните следующие действия.

- Добавьте элемент `SelectParameters` для параметра с именем `nameSearchString`, который получает значение, указанное в элементе управления `SearchTextBox`.
- Измените значение атрибута `SelectMethod` на `GetDepartmentsByName`. (Этот метод будет создан позже.)

Разметка для элемента управления `ObjectDataSource` теперь напоминает следующий пример:

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample10.aspx)]

В *ISchoolRepository.CS*добавьте метод `GetDepartmentsByName`, который принимает `sortExpression` и `nameSearchString` параметры:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample11.cs)]

В *SchoolRepository.CS*добавьте следующий новый метод:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample12.cs)]

Этот код использует метод `Where` для выбора элементов, содержащих строку поиска. Если строка поиска пуста, будут выбраны все записи. Обратите внимание, что при указании вызовов методов вместе в одном операторе (`Include`, затем `OrderBy`, а затем `Where`) метод `Where` должен всегда быть последним.

Измените существующий метод `GetDepartments`, который принимает параметр `sortExpression` для вызова нового метода:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample13.cs)]

В *MockSchoolRepository.CS* в тестовом проекте добавьте следующий новый метод:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample14.cs)]

В *SchoolBL.CS*добавьте следующий новый метод:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample15.cs)]

Запустите страницу *departmentss. aspx* и введите строку поиска, чтобы убедиться, что логика выбора работает. Оставьте текстовое поле пустым и попробуйте выполнить поиск, чтобы убедиться, что все записи возвращены.

[![Image03](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image6.png)](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image5.png)

## <a name="adding-a-details-column-for-each-grid-row"></a>Добавление столбца сведений для каждой строки сетки

Далее нужно просмотреть все курсы по каждому отделу, отображаемому в правой ячейке сетки. Для этого используется вложенный элемент управления `GridView` и привязка его к данным из свойства навигации `Courses` сущности `Department`.

Откройте *отделы. aspx* и в разметке для элемента управления `GridView` укажите обработчик для события `RowDataBound`. Разметка для открывающего тега элемента управления теперь напоминает следующий пример.

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample16.aspx)]

Добавьте новый элемент `TemplateField` после поля шаблона `Administrator`:

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample17.aspx)]

Эта разметка создает вложенный элемент управления `GridView`, который показывает номер курса и заголовок списка курсов. Он не указывает источник данных, так как он будет привязку к нему в коде обработчика `RowDataBound`.

Откройте *Departments.aspx.CS* и добавьте следующий обработчик для события `RowDataBound`:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample18.cs)]

Этот код получает `Department` сущность из аргументов события, преобразует `Courses` свойство навигации в коллекцию `List` и привязывает вложенные `GridView` к коллекции.

Откройте файл *SchoolRepository.CS* и укажите безотлагательную загрузку для свойства навигации `Courses`, вызвав метод `Include` в запросе объекта, созданном в методе `GetDepartmentsByName`. Оператор `return` в методе `GetDepartmentsByName` теперь напоминает следующий пример.

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample19.cs)]

Запустите страницу. Помимо возможностей сортировки и фильтрации, добавленных ранее, в элементе управления GridView теперь отображаются вложенные сведения о курсе для каждого отдела.

[![image01](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image8.png)](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image7.png)

В результате вы закончите вводные сведения о сценариях сортировки, фильтрации и "основной/подробности". В следующем руководстве вы узнаете, как работать с параллелизмом.

> [!div class="step-by-step"]
> [Назад](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests.md)
> [Вперед](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application.md)
