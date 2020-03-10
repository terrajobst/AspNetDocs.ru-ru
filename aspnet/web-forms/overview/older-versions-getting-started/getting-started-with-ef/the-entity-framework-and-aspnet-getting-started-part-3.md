---
uid: web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-3
title: Начало работы с Entity Framework 4,0 Database First и веб-форм ASP.NET 4, часть 3 | Документация Майкрософт
author: tdykstra
description: Пример веб-приложения Contoso университета демонстрирует создание приложений ASP.NET Web Forms с помощью Entity Framework. Пример приложения:...
ms.author: riande
ms.date: 12/03/2010
ms.assetid: ccdc3f8c-2568-40a7-8f8b-3c23d2e05388
msc.legacyurl: /web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-3
msc.type: authoredcontent
ms.openlocfilehash: 88debb11a9157dce9ff000b1cb459b876dbceaf3
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78522642"
---
# <a name="getting-started-with-entity-framework-40-database-first-and-aspnet-4-web-forms---part-3"></a>Начало работы с Entity Framework 4,0 Database First и веб-форм ASP.NET 4. часть 3

от [Tom Dykstra)](https://github.com/tdykstra)

> Пример веб-приложения университета Contoso демонстрирует создание приложений ASP.NET Web Forms с помощью Entity Framework 4,0 и Visual Studio 2010. Сведения о серии руководств см. в [первом учебнике серии](the-entity-framework-and-aspnet-getting-started-part-1.md) .

## <a name="filtering-ordering-and-grouping-data"></a>Фильтрация, упорядочение и группирование данных

В предыдущем учебнике для просмотра и изменения данных использовался элемент управления `EntityDataSource`. В этом учебнике вы будете фильтровать, упорядочивать и группировать данные. При этом при установке свойств элемента управления `EntityDataSource` синтаксис отличается от других элементов управления источниками данных. Но вы увидите, что для сворачивания этих различий можно использовать элемент управления `QueryExtender`.

Вы измените страницу *students. aspx* , чтобы отфильтровать учащихся, сортировать по имени и искать по имени. Вы также измените страницу *Courses. aspx* , чтобы отобразить курсы для выбранного отдела и найти курсы по имени. Наконец, вы добавите статистику для учащихся на страницу *About. aspx* .

[![Image02](the-entity-framework-and-aspnet-getting-started-part-3/_static/image2.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image1.png)

[![Image11](the-entity-framework-and-aspnet-getting-started-part-3/_static/image4.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image3.png)

[![Image10](the-entity-framework-and-aspnet-getting-started-part-3/_static/image6.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image5.png)

[![Image14](the-entity-framework-and-aspnet-getting-started-part-3/_static/image8.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image7.png)

## <a name="using-the-entitydatasource-where-property-to-filter-data"></a>Использование свойства EntityDataSource "Where" для фильтрации данных

Откройте страницу *students. aspx* , созданную в предыдущем руководстве. Как уже настроено, элемент управления `GridView` на странице отображает все имена из `People` набора сущностей. Однако вы хотите показывать только учащихся, которые можно найти, выбрав `Person` сущности с датами регистрации, отличными от NULL.

Перейдите в режим **конструктора** и выберите элемент управления `EntityDataSource`. В окне **Свойства** присвойте свойству `Where` значение `it.EnrollmentDate is not null`.

[![image01](the-entity-framework-and-aspnet-getting-started-part-3/_static/image10.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image9.png)

Синтаксис, используемый в свойстве `Where` элемента управления `EntityDataSource`, Entity SQL. Entity SQL похож на Transact-SQL, но он настроен для использования с сущностями, а не с объектами базы данных. В `it.EnrollmentDate is not null`е выражения слово `it` представляет ссылку на сущность, возвращенную запросом. Таким образом, `it.EnrollmentDate` ссылается на свойство `EnrollmentDate` сущности `Person`, которую возвращает элемент управления `EntityDataSource`.

Запустите страницу. Список учащихся теперь содержит только учащихся. (Нет строк, которые отображаются там, где нет даты регистрации.)

[![Image02](the-entity-framework-and-aspnet-getting-started-part-3/_static/image12.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image11.png)

## <a name="using-the-entitydatasource-orderby-property-to-order-data"></a>Использование свойства EntityDataSource "OrderBy" для упорядочивания данных

Кроме того, при первом отображении список должен находиться в порядке имен. Если страница *students. aspx* по-прежнему открыта в режиме **конструктора** и элемент управления `EntityDataSource` по-прежнему выбран, в окне **Свойства** задайте для свойства **OrderBy** значение `it.LastName`.

[![Image05](the-entity-framework-and-aspnet-getting-started-part-3/_static/image14.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image13.png)

Запустите страницу. Список учащихся теперь находится в порядке фамилии.

[![Image04](the-entity-framework-and-aspnet-getting-started-part-3/_static/image16.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image15.png)

## <a name="using-a-control-parameter-to-set-the-where-property"></a>Использование параметра элемента управления для задания свойства "Where"

Как и в случае с другими элементами управления источниками данных, значения параметров можно передать свойству `Where`. На странице *Courses. aspx* , созданной в части 2 этого руководства, этот метод можно использовать для просмотра курсов, связанных с подразделением, которое пользователь выбирает из раскрывающегося списка.

Откройте *страницу Courses. aspx* и переключитесь в режим **конструктора** . Добавьте второй элемент управления `EntityDataSource` на страницу и присвойте ему имя `CoursesEntityDataSource`. Подключите его к модели `SchoolEntities` и выберите `Courses` в качестве значения **EntitySetName** .

В окне **Свойства** нажмите кнопку с многоточием в поле свойства **WHERE** . (Перед использованием окна **свойств** убедитесь, что элемент управления `CoursesEntityDataSource` выбран.)

[![Image06](the-entity-framework-and-aspnet-getting-started-part-3/_static/image18.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image17.png)

Откроется диалоговое окно **Редактор выражений** . В этом диалоговом окне выберите **автоматически создать выражение WHERE на основе указанных параметров**, а затем нажмите кнопку **Добавить параметр**. Присвойте параметру имя `DepartmentID`, выберите **элемент управления** в качестве значения **источника параметра** и выберите **департментсдропдовнлист** в качестве значения **ControlID** .

[![Image07](the-entity-framework-and-aspnet-getting-started-part-3/_static/image20.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image19.png)

Нажмите кнопку " **отобразить дополнительные свойства**" и в окне " **свойства** " диалогового окна **редактор выражений** измените значение свойства `Type` на `Int32`.

[![Image15](the-entity-framework-and-aspnet-getting-started-part-3/_static/image22.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image21.png)

Закончив, нажмите кнопку **OK**.

Ниже раскрывающегося списка добавьте элемент управления `GridView` на страницу и присвойте ему имя `CoursesGridView`. Подключите его к `CoursesEntityDataSource` элементу управления источниками данных, щелкните **Обновить схему**, щелкните **изменить столбцы**и удалите столбец `DepartmentID`. Разметка элемента управления `GridView` напоминает следующий пример.

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-3/samples/sample1.aspx)]

Когда пользователь изменяет выбранное подразделение в раскрывающемся списке, необходимо, чтобы список связанных курсов был изменен автоматически. Чтобы сделать это, выберите раскрывающийся список и в окне **Свойства** задайте для свойства `AutoPostBack` значение `True`.

[![Image08](the-entity-framework-and-aspnet-getting-started-part-3/_static/image24.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image23.png)

После завершения работы с конструктором переключитесь в представление **исходного кода** и замените свойства `ConnectionString` и `DefaultContainer` имени элемента управления `CoursesEntityDataSource` атрибутом `ContextTypeName="ContosoUniversity.DAL.SchoolEntities"`. По завершении разметка элемента управления будет выглядеть, как в следующем примере.

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-3/samples/sample2.aspx)]

Запустите страницу и используйте раскрывающийся список для выбора различных отделов. В элементе управления `GridView` отображаются только те курсы, которые предлагаются выбранным Отделом.

[![Image09](the-entity-framework-and-aspnet-getting-started-part-3/_static/image26.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image25.png)

## <a name="using-the-entitydatasource-groupby-property-to-group-data"></a>Использование свойства EntityDataSource "GroupBy" для группирования данных

Предположим, что университет Contoso хочет разместить на странице About некоторую статистику на основе текста учащихся. В частности, он хочет показать подразделение количества учащихся на дату их регистрации.

Откройте *About. aspx*и в представлении **исходного кода** замените существующее содержимое элемента управления `BodyContent` на "Статистика текста учащегося" между тегами `h2`:

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-3/samples/sample3.aspx)]

После заголовка добавьте элемент управления `EntityDataSource` и присвойте ему имя `StudentStatisticsEntityDataSource`. Подключите его к `SchoolEntities`, выберите `People` набор сущностей и оставьте поле **выбора** в мастере без изменений. Задайте следующие свойства в окне " **Свойства** ":

- Чтобы выполнить фильтрацию только для учащихся, задайте для свойства `Where` значение `it.EnrollmentDate is not null`.
- Чтобы сгруппировать результаты по дате регистрации, задайте для свойства `GroupBy` значение `it.EnrollmentDate`.
- Чтобы выбрать дату регистрации и число учащихся, задайте для свойства `Select` значение `it.EnrollmentDate, Count(it.EnrollmentDate) AS NumberOfStudents`.
- Чтобы упорядочить результаты по дате регистрации, задайте для свойства `OrderBy` значение `it.EnrollmentDate`.

В представлении **исходного кода** замените свойства `ConnectionString` и `DefaultContainer` именем свойством `ContextTypeName`. Разметка элемента управления `EntityDataSource` теперь напоминает следующий пример.

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-3/samples/sample4.aspx)]

Синтаксис свойств `Select`, `GroupBy`и `Where` похож на Transact-SQL, за исключением ключевого слова `it`, определяющего текущую сущность.

Добавьте следующую разметку, чтобы создать `GridView` элемент управления для вывода данных.

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-3/samples/sample5.aspx)]

Запустите страницу, чтобы просмотреть список, отображающий число учащихся по дате регистрации.

[![Image10](the-entity-framework-and-aspnet-getting-started-part-3/_static/image28.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image27.png)

## <a name="using-the-queryextender-control-for-filtering-and-ordering"></a>Использование элемента управления элемента для фильтрации и упорядочения

Элемент управления `QueryExtender` предоставляет способ задания фильтрации и сортировки в разметке. Синтаксис не зависит от используемой системы управления базами данных (СУБД). Обычно он не зависит от Entity Framework, за исключением того, что синтаксис, используемый для свойств навигации, уникален для Entity Framework.

В этой части учебника будет использоваться элемент управления `QueryExtender` для фильтрации и упорядочения данных, а одно из полей ORDER-BY — это свойство навигации.

(Если вы предпочитаете использовать код вместо разметки для расширения запросов, автоматически создаваемых элементом управления `EntityDataSource`, это можно сделать, обрабатывая событие `QueryCreated`. Именно так `QueryExtender` элемент управления расширяет запросы `EntityDataSource` Control.)

Откройте страницу *Courses. aspx* и под добавленной ранее разметкой вставьте следующую разметку, чтобы создать заголовок, текстовое поле для ввода строк поиска, кнопку поиска и элемент управления `EntityDataSource`, привязанный к `Courses`ному набору сущностей.

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-3/samples/sample6.aspx)]

Обратите внимание, что свойство `Include` `EntityDataSource` элемента управления имеет значение `Department`. В базе данных `Course` таблица не содержит название отдела; Он содержит `DepartmentID` столбец внешнего ключа. Если вы напрямую запрашиваете базу данных, чтобы получить имя отдела вместе с данными курса, необходимо объединить `Course` и `Department` таблицы. Установив для свойства `Include` значение `Department`, вы указываете, что Entity Framework должен выполнять работу по получению связанной `Department` сущности, когда она получает `Course` сущность. Затем сущность `Department` сохраняется в свойстве навигации `Department` сущности `Course`. (По умолчанию класс `SchoolEntities`, созданный конструктором моделей данных, извлекает связанные данные, когда это необходимо, и вы привязываете элемент управления источником данных к этому классу, поэтому установка свойства `Include` не требуется. Однако установка этого параметра повышает производительность страницы, так как в противном случае Entity Framework будет выполнять отдельные вызовы к базе данных для получения данных для `Course` сущностей и связанных сущностей `Department`.)

После только что созданного элемента управления `EntityDataSource` вставьте следующую разметку, чтобы создать элемент управления `QueryExtender`, привязанный к этому элементу управления `EntityDataSource`.

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-3/samples/sample7.aspx)]

Элемент `SearchExpression` указывает, что необходимо выбрать курсы, заголовки которых соответствуют значению, введенному в текстовом поле. Будет сравниваться только число символов, указанное в текстовом поле, так как свойство `SearchType` указывает `StartsWith`.

Элемент `OrderByExpression` указывает, что результирующий набор будет упорядочен по названию курса в названии отдела. Обратите внимание на то, как указано название отдела: `Department.Name`. Поскольку связь между сущностью `Course` и сущностью `Department` является "один к одному", свойство навигации `Department` содержит сущность `Department`. (Если это связь «один ко многим», свойство будет содержать коллекцию.) Чтобы получить имя отдела, необходимо указать свойство `Name` сущности `Department`.

Наконец, добавьте элемент управления `GridView` для просмотра списка курсов:

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-3/samples/sample8.aspx)]

Первый столбец — это поле шаблона, в котором отображается название отдела. Выражение DataBinding задает `Department.Name`, как показано в элементе управления `QueryExtender`.

Запустите страницу. В начальном отображении отображается список всех курсов, упорядоченных по отделам, а затем по названию курса.

[![Image11](the-entity-framework-and-aspnet-getting-started-part-3/_static/image30.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image29.png)

Введите "m" и нажмите кнопку " **Поиск** ", чтобы просмотреть все курсы, названия которых начинаются с "m" (при поиске не учитывается регистр).

[![Image12](the-entity-framework-and-aspnet-getting-started-part-3/_static/image32.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image31.png)

## <a name="using-the-like-operator-to-filter-data"></a>Использование оператора LIKE для фильтрации данных

С помощью оператора `Like` в свойстве `EntityDataSource` элемента управления `Where` можно добиться того же результата, что и для типов поиска `StartsWith`, `Contains`и `EndsWith` элемента управления `QueryExtender`. В этой части руководства вы узнаете, как использовать оператор `Like` для поиска учащихся по имени.

Откройте *students. aspx* в представлении **исходного кода** . После элемента управления `GridView` добавьте следующую разметку:

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-3/samples/sample9.aspx)]

Эта разметка похожа на ту, что вы видели ранее, за исключением значения свойства `Where`. Вторая часть выражения `Where` определяет Поиск подстроки (`LIKE %FirstMidName% or LIKE %LastName%`), которая выполняет поиск в первом и последнем именах, вводимых в текстовом поле.

Запустите страницу. Сначала вы увидите всех учащихся, так как значение по умолчанию для параметра `StudentName` — "%".

[![Image13](the-entity-framework-and-aspnet-getting-started-part-3/_static/image34.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image33.png)

Введите букву "g" в текстовом поле и нажмите кнопку " **Поиск**". Вы увидите список учащихся, имеющих "g" в имени или фамилии.

[![Image14](the-entity-framework-and-aspnet-getting-started-part-3/_static/image36.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image35.png)

Теперь вы отображаете, обновили, отфильтрованные, упорядоченные и сгруппированные данные из отдельных таблиц. В следующем учебнике вы начнете работать с связанными данными (сценарии "основной-подробности").

> [!div class="step-by-step"]
> [Назад](the-entity-framework-and-aspnet-getting-started-part-2.md)
> [Вперед](the-entity-framework-and-aspnet-getting-started-part-4.md)
