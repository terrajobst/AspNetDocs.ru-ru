---
uid: web-forms/overview/data-access/paging-and-sorting-with-the-datalist-and-repeater/sorting-data-in-a-datalist-or-repeater-control-cs
title: Сортировка данных в элементе управления DataList или Repeater (C#) | Документация Майкрософт
author: rick-anderson
description: В этом учебнике мы рассмотрим, как включить поддержку сортировки в DataList и Repeater, а также как создать элемент управления DataList или Repeater, данные которого могут...
ms.author: riande
ms.date: 11/13/2006
ms.assetid: f52c302a-1b7c-46fe-8a13-8412c95cbf6d
msc.legacyurl: /web-forms/overview/data-access/paging-and-sorting-with-the-datalist-and-repeater/sorting-data-in-a-datalist-or-repeater-control-cs
msc.type: authoredcontent
ms.openlocfilehash: 66a09c637d33c812b39e0ce85a552bd71665a2e1
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78502956"
---
# <a name="sorting-data-in-a-datalist-or-repeater-control-c"></a>Сортировка данных в элементе управления DataList или Repeater (C#)

по [Скотт Митчелл](https://twitter.com/ScottOnWriting)

[Скачивание примера приложения](https://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_45_CS.exe) или [Загрузка PDF-файла](sorting-data-in-a-datalist-or-repeater-control-cs/_static/datatutorial45cs1.pdf)

> В этом учебнике мы рассмотрим, как включить поддержку сортировки в DataList и Repeater, а также как создать элемент управления DataList или Repeater, данные которого могут быть страничными и отсортированными.

## <a name="introduction"></a>Введение

В [предыдущем учебном курсе](paging-report-data-in-a-datalist-or-repeater-control-cs.md) мы рассмотрели, как добавить поддержку разбиения по страницам в DataList. Мы создали новый метод в классе `ProductsBLL` (`GetProductsAsPagedDataSource`), который вернул объект `PagedDataSource`. При привязке к элементу управления DataList или Repeater в элементе управления DataList или Repeater отображается только запрошенная страница данных. Этот метод аналогичен тому, который используется внутренне элементами управления GridView, DetailsView и FormView для предоставления встроенных функций разбиения по страницам по умолчанию.

Помимо поддержки разбиения по страницам, GridView также включает поддержку сортировки Box. Ни DataList, ни Repeater не предоставляют встроенные функции сортировки. Однако функции сортировки можно добавлять с помощью ряда кода. В этом учебнике мы рассмотрим, как включить поддержку сортировки в DataList и Repeater, а также как создать элемент управления DataList или Repeater, данные которого могут быть страничными и отсортированными.

## <a name="a-review-of-sorting"></a>Проверка сортировки

Как мы видели в учебнике по [данным отчета о разбиении на страницы и сортировке](../paging-and-sorting/paging-and-sorting-report-data-cs.md) , элемент управления GridView обеспечивает поддержку сортировки в виде полей. Каждое поле GridView может иметь связанный `SortExpression`, который указывает поле данных, по которому сортируются данные. Если свойство `AllowSorting` GridView s имеет значение `true`, то каждое поле GridView со значением свойства `SortExpression` имеет заголовок, отображаемый в качестве элемента управления LinkButton. Когда пользователь щелкает определенный заголовок поля GridView, происходит обратная передача, а данные сортируются в соответствии с выбранными полями `SortExpression`.

Элемент управления GridView также имеет свойство `SortExpression`, в котором хранится `SortExpression` поля GridView, по которому сортируются данные. Кроме того, свойство `SortDirection` указывает, должны ли данные быть отсортированы по возрастанию или убыванию (если пользователь дважды щелкает определенную ссылку заголовка поля GridView, то порядок сортировки переключается).

Когда GridView привязан к своему элементу управления источниками данных, он передает `SortExpression` и `SortDirection` свойства элементу управления источником данных. Элемент управления источника данных получает данные, а затем сортирует их в соответствии с предоставленными свойствами `SortExpression` и `SortDirection`. После сортировки данных элемент управления источника данных возвращает его в GridView.

Чтобы реплицировать эту функцию с помощью элементов управления DataList или Repeater, необходимо:

- Создание интерфейса сортировки
- Запомните поле данных, по которому нужно выполнить сортировку, а также порядок сортировки по возрастанию или убыванию.
- Попросите ObjectDataSource отсортировать данные по определенному полю данных

Эти три задачи мы будем решать в шагах 3 и 4. Далее мы рассмотрим, как включить поддержку разбиения по страницам и сортировки в DataList или Repeater.

## <a name="step-2-displaying-the-products-in-a-repeater"></a>Шаг 2. Отображение продуктов в элементе Repeater

Прежде чем беспокоиться о реализации какой-либо функции сортировки, начнем с перечисления продуктов в элементе управления Repeater. Для начала откройте страницу `Sorting.aspx` в папке `PagingSortingDataListRepeater`. Добавьте на веб-страницу элемент управления Repeater, задав для его свойства `ID` значение `SortableProducts`. В смарт-теге Repeater s создайте новый объект ObjectDataSource с именем `ProductsDataSource` и настройте его для получения данных из `ProductsBLL` класса s `GetProducts()` метода. Выберите параметр (нет) в раскрывающихся списках на вкладках Вставка, обновление и удаление.

[![создать ObjectDataSource и настроить его для использования метода Жетпродуктсаспажеддатасаурце ()](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image2.png)](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image1.png)

**Рис. 1**. Создание ObjectDataSource и настройка его для использования метода `GetProductsAsPagedDataSource()` ([щелкните, чтобы просмотреть изображение с полным размером](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image3.png))

[![установить в раскрывающихся списках на вкладках обновления, вставки и удаления значение (нет)](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image5.png)](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image4.png)

**Рис. 2**. Настройка раскрывающихся списков на вкладках "Обновить", "вставить" и "Удалить" (нет) ([щелкните, чтобы просмотреть изображение с полным размером](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image6.png))

В отличие от DataList, Visual Studio не создает `ItemTemplate` для элемента управления Repeater автоматически, после того как привязывает его к источнику данных. Более того, мы должны добавить эту `ItemTemplate` декларативно, так как смарт-тег элемента управления Repeater не имеет параметра Edit Templates в DataList s. Разрешите использовать тот же `ItemTemplate` из предыдущего руководства, в котором отображалось имя, поставщик и Категория продукта.

После добавления `ItemTemplate`декларативная разметка Repeater и ObjectDataSource должна выглядеть следующим образом:

[!code-aspx[Main](sorting-data-in-a-datalist-or-repeater-control-cs/samples/sample1.aspx)]

На рис. 3 показана эта страница при просмотре в браузере.

[![отображается название, поставщик и Категория продукта.](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image8.png)](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image7.png)

**Рис. 3**. отображается название, поставщик и Категория каждого продукта ([щелкните, чтобы просмотреть изображение с полным размером](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image9.png)).

## <a name="step-3-instructing-the-objectdatasource-to-sort-the-data"></a>Шаг 3. указание элементу управления ObjectDataSource на сортировку данных

Чтобы отсортировать данные, отображаемые в элементе управления Repeater, необходимо сообщить элементу ObjectDataSource выражения сортировки, по которому должны быть отсортированы данные. Прежде чем ObjectDataSource получит свои данные, он сначала выдает [событие`Selecting`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.selecting.aspx), которое предоставляет возможность указать выражение сортировки. Обработчику `Selecting` событий передается объект типа [`ObjectDataSourceSelectingEventArgs`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasourceselectingeventargs.aspx), который имеет свойство с именем [`Arguments`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasourceselectingeventargs.arguments.aspx) типа [`DataSourceSelectArguments`](https://msdn.microsoft.com/library/system.web.ui.datasourceselectarguments.aspx). Класс `DataSourceSelectArguments` предназначен для передачи запросов, связанных с данными, от потребителя данных к элементу управления источника данных и включает [свойство`SortExpression`](https://msdn.microsoft.com/library/system.web.ui.datasourceselectarguments.sortexpression.aspx).

Чтобы передать сведения о сортировке со страницы ASP.NET в ObjectDataSource, создайте обработчик событий для события `Selecting` и используйте следующий код:

[!code-csharp[Main](sorting-data-in-a-datalist-or-repeater-control-cs/samples/sample2.cs)]

Значение *sortExpression* должно быть присвоено имени поля данных для сортировки данных (например, ProductName). Свойство, связанное с направлением сортировки, отсутствует, поэтому если нужно отсортировать данные в убывающем порядке, добавьте строку DESC к значению *sortExpression* (например, ProductName DESC).

Попробуйте выполнить некоторые другие жестко запрограммированные значения для *sortExpression* и проверьте результаты в браузере. Как показано на рис. 4, при использовании ProductName DESC в качестве *sortExpression*продукты сортируются по имени в противоположном алфавитном порядке.

[![продукты сортируются по имени в обратный алфавитный порядок](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image11.png)](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image10.png)

**Рис. 4**. продукты сортируются по именам в алфавитном порядке ([щелкните, чтобы просмотреть изображение с полным размером](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image12.png))

## <a name="step-4-creating-the-sorting-interface-and-remembering-the-sort-expression-and-direction"></a>Шаг 4. Создание интерфейса сортировки и запоминание выражения сортировки и направления

Включение поддержки сортировки в GridView преобразует каждый текст заголовка поля с возможностью сортировки в элемент управления LinkButton, который при щелчке сортирует данные соответствующим образом. Такой интерфейс сортировки имеет смысл для элемента управления GridView, где его данные четко располагаются в столбцах. Однако для элементов управления DataList и Repeater требуется другой интерфейс сортировки. Общий интерфейс сортировки для списка данных (в отличие от сетки данных) — это раскрывающийся список, предоставляющий поля, по которым можно сортировать данные. Давайте добавим такой интерфейс для этого руководства.

Добавьте веб-элемент управления DropDownList выше `SortableProducts` Repeater и задайте для его свойства `ID` значение `SortBy`. В окно свойств нажмите кнопку с многоточием в свойстве `Items`, чтобы открыть редактор коллекции ListItem. Добавьте `ListItem` s, чтобы отсортировать данные по полям `ProductName`, `CategoryName`и `SupplierName`. Кроме того, добавьте `ListItem`, чтобы сортировать продукты по именам в алфавитном порядке.

Для свойств `ListItem` `Text` можно задать любое значение (например, имя), но свойства `Value` должны быть заданы как имя поля данных (например, ProductName). Чтобы отсортировать результаты в убывающем порядке, добавьте строку DESC в имя поля данных, например ProductName.

![Добавление ListItem для каждого поля данных, допускающего сортировку](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image13.png)

**Рис. 5**. Добавление `ListItem` для каждого поля данных, допускающего сортировку

Наконец, добавьте веб-элемент управления Button справа от DropDownList. Задайте для его `ID` значение `RefreshRepeater` и его свойство `Text` для обновления.

После создания `ListItem` и добавления кнопки «Обновить» декларативный синтаксис элемента DropDownList и Button должен выглядеть следующим образом:

[!code-aspx[Main](sorting-data-in-a-datalist-or-repeater-control-cs/samples/sample3.aspx)]

После завершения работы DropDownList необходимо обновить обработчик событий ObjectDataSource `Selecting`, чтобы в нем использовалось выбранное свойство `SortBy``ListItem` s `Value`, а не жестко заданное выражение сортировки.

[!code-csharp[Main](sorting-data-in-a-datalist-or-repeater-control-cs/samples/sample4.cs)]

На этом этапе при первом посещении страницы товары изначально сортируются по полю `ProductName` данные, как `SortBy` `ListItem` выбрано по умолчанию (см. рис. 6). Выбор другого варианта сортировки, например Категория, и нажатие кнопки Обновить приведет к обратной передаче и повторной сортировке данных по имени категории, как показано на рис. 7.

[![продукты изначально сортируются по имени](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image15.png)](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image14.png)

**Рис. 6**. первоначально отсортированные продукты по имени ([щелкните, чтобы просмотреть изображение с полным размером](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image16.png))

[![продукты теперь сортируются по категориям](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image18.png)](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image17.png)

**Рис. 7**. Теперь продукты сортируются по категориям ([щелкните, чтобы просмотреть изображение с полным размером](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image19.png))

> [!NOTE]
> Нажатие кнопки «Обновить» приводит к автоматическому пересортировке данных, так как состояние представления Repeater s было отключено, что приводит к повторной привязке Repeater к своему источнику данных при каждой обратной передаче. Если оставить состояние представления Repeater s включенным, изменение раскрывающегося списка сортировка не повлияет на порядок сортировки. Чтобы устранить эту проблему, создайте обработчик событий для кнопки обновления `Click` событие и повторно привяжите Repeater к своему источнику данных (вызвав метод Repeater s `DataBind()`).

## <a name="remembering-the-sort-expression-and-direction"></a>Запоминание выражения и направления сортировки

При создании сортируемого элемента управления DataList или Repeater на странице, где могут возникать обратные передачи, не относящиеся к сортировке, крайне важно, чтобы выражение сортировки и направление были сохранены в обратных передачах. Например, предположим, что мы обновили Repeater в этом учебнике, чтобы включить кнопку «Удалить» для каждого продукта. Когда пользователь нажимает кнопку "Удалить", мы выполняем код, чтобы удалить выбранный продукт, а затем повторно привязать данные к элементу Repeater. Если сведения о сортировке не сохраняются в обратной передаче, то данные, отображаемые на экране, будут возвращаться к исходному порядку сортировки.

В этом руководстве DropDownList неявно сохраняет выражение сортировки и направление в своем состоянии просмотра для нас. Если бы мы использовали другой интерфейс сортировки, например LinkButton, который предоставил различные варианты сортировки, нам нужно помнить, что порядок сортировки для обратных передач должен быть важен. Это можно сделать, сохранив параметры сортировки в состоянии просмотра страницы, включив параметр Sort в строку запроса или используя другой метод сохранения состояния.

В будущих примерах этого учебника рассматривается сохранение сведений о сортировке в состоянии просмотра страницы.

## <a name="step-5-adding-sorting-support-to-a-datalist-that-uses-default-paging"></a>Шаг 5. Добавление поддержки сортировки в DataList, который использует разбиение по страницам по умолчанию

В [предыдущем учебном курсе](paging-report-data-in-a-datalist-or-repeater-control-cs.md) мы рассмотрели, как реализовать разбиение по страницам по умолчанию с помощью DataList. Добавим этот предыдущий пример, чтобы включить возможность сортировки данных, находящихся на странице. Для начала откройте `SortingWithDefaultPaging.aspx` и `Paging.aspx` страницы в папке `PagingSortingDataListRepeater`. На странице `Paging.aspx` нажмите кнопку Источник, чтобы просмотреть декларативную разметку страницы s. Скопируйте выделенный текст (см. рис. 8) и вставьте его в декларативную разметку `SortingWithDefaultPaging.aspx` между тегами `<asp:Content>`.

[![реплицировать декларативную разметку в теги &lt;ASP: Content&gt; тегами из файла paging. aspx в Сортингвисдефаултпагинг. aspx.](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image21.png)](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image20.png)

**Рис. 8**. репликация декларативной разметки в теги `<asp:Content>` из `Paging.aspx` в `SortingWithDefaultPaging.aspx` ([щелкните, чтобы просмотреть изображение с полным размером](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image22.png))

После копирования декларативной разметки скопируйте методы и свойства в класс кода программной части `Paging.aspx` Pages в класс кода программной части для `SortingWithDefaultPaging.aspx`. Затем просмотрите страницу `SortingWithDefaultPaging.aspx` в браузере. Она должна демонстрировать те же функциональные возможности и внешний вид, что и `Paging.aspx`.

## <a name="enhancing-productsbll-to-include-a-default-paging-and-sorting-method"></a>Улучшение ProductsBLL для включения метода разбиения по страницам и сортировки по умолчанию

В предыдущем учебном курсе мы создали метод `GetProductsAsPagedDataSource(pageIndex, pageSize)` в классе `ProductsBLL`, который вернул объект `PagedDataSource`. Этот объект `PagedDataSource` был заполнен *всеми* продуктами (с помощью метода `GetProducts()` BLL), но при привязке к DataList отображались только те записи, которые соответствуют указанным входным параметрам *pageIndex* и *pageSize* .

Ранее в этом руководстве мы добавили поддержку сортировки, указав выражение сортировки из обработчика событий ObjectDataSource `Selecting`. Это хорошо работает, когда ObjectDataSource возвращает объект, который можно сортировать, например `ProductsDataTable`, возвращаемый методом `GetProducts()`. Однако объект `PagedDataSource`, возвращаемый методом `GetProductsAsPagedDataSource`, не поддерживает сортировку внутреннего источника данных. Вместо этого необходимо отсортировать результаты, возвращенные методом `GetProducts()`, *перед* помещением их в `PagedDataSource`.

Чтобы сделать это, создайте новый метод в классе `ProductsBLL` `GetProductsSortedAsPagedDataSource(sortExpression, pageIndex, pageSize)`. Чтобы отсортировать `ProductsDataTable`, возвращаемый методом `GetProducts()`, укажите свойство `Sort` `DataTableView`по умолчанию:

[!code-csharp[Main](sorting-data-in-a-datalist-or-repeater-control-cs/samples/sample5.cs)]

Метод `GetProductsSortedAsPagedDataSource` немного отличается от метода `GetProductsAsPagedDataSource`, созданного в предыдущем руководстве. В частности, `GetProductsSortedAsPagedDataSource` принимает дополнительный входной параметр `sortExpression` и присваивает это значение свойству `Sort` `ProductDataTable` `DefaultView`. После нескольких строк кода источнику DataSource `PagedDataSource` Object s назначается `ProductDataTable` s `DefaultView`.

## <a name="calling-the-getproductssortedaspageddatasource-method-and-specifying-the-value-for-the-sortexpression-input-parameter"></a>Вызов метода Жетпродуктссортедаспажеддатасаурце и указание значения для входного параметра SortExpression

После завершения метода `GetProductsSortedAsPagedDataSource` необходимо предоставить значение для этого параметра. ObjectDataSource в `SortingWithDefaultPaging.aspx` в настоящее время настроен для вызова метода `GetProductsAsPagedDataSource` и передает два входных параметра через два `QueryStringParameters`, которые указаны в коллекции `SelectParameters`. Эти два `QueryStringParameters` указывают, что источник для параметров `GetProductsAsPagedDataSource` методов *pageIndex* и *pageSize* взят из полей QueryString `pageIndex` и `pageSize`.

Обновите свойство `SelectMethod` ObjectDataSource s таким образом, чтобы оно вызывало новый метод `GetProductsSortedAsPagedDataSource`. Затем добавьте новый `QueryStringParameter`, чтобы получить доступ к входному параметру *sortExpression* из поля QueryString `sortExpression`. Задайте для `QueryStringParameter` s `DefaultValue` значение ProductName.

После этих изменений декларативная разметка ObjectDataSource s должна выглядеть следующим образом:

[!code-aspx[Main](sorting-data-in-a-datalist-or-repeater-control-cs/samples/sample6.aspx)]

На этом этапе страница `SortingWithDefaultPaging.aspx` сортирует результаты в алфавитном порядке по названию продукта (см. рис. 9). Это связано с тем, что по умолчанию значение ProductName передается в качестве параметра `GetProductsSortedAsPagedDataSource` Method s *sortExpression* .

[![по умолчанию результаты сортируются по ProductName](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image24.png)](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image23.png)

**Рис. 9**. по умолчанию результаты сортируются по `ProductName` ([щелкните, чтобы просмотреть изображение с полным размером](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image25.png))

Если вручную добавить поле `sortExpression` QueryString, например `SortingWithDefaultPaging.aspx?sortExpression=CategoryName` результаты будут отсортированы по указанному `sortExpression`. Однако этот параметр `sortExpression` не включается в строку запроса при переходе на другую страницу данных. На самом деле, нажатие кнопок «Следующая» или «последняя страница» вернет нас к `Paging.aspx`! Кроме того, в настоящее время нет интерфейса сортировки. Единственный способ, которым пользователь может изменить порядок сортировки данных на странице, заключается в непосредственном управлении строкой запроса.

## <a name="creating-the-sorting-interface"></a>Создание интерфейса сортировки

Сначала необходимо обновить метод `RedirectUser`, чтобы отправить пользователю `SortingWithDefaultPaging.aspx` (а не `Paging.aspx`) и включить значение `sortExpression` в строку запроса. Также следует добавить свойство `SortExpression`, доступное только для чтения, с именем уровня страницы. Это свойство аналогично свойствам `PageIndex` и `PageSize`, созданным в предыдущем руководстве, возвращает значение поля `sortExpression` QueryString, если оно существует, и значение по умолчанию (ProductName) в противном случае.

В настоящее время метод `RedirectUser` принимает только один входной параметр, который является индексом отображаемой страницы. Однако иногда требуется перенаправить пользователя на определенную страницу данных с помощью выражения сортировки, отличного от того, что указано в строке запроса. Сейчас мы создадим интерфейс сортировки для этой страницы, который будет включать ряд веб-элементов управления "Кнопка" для сортировки данных по указанному столбцу. При нажатии одной из этих кнопок необходимо перенаправить пользователя, передав ему соответствующее значение выражения сортировки. Чтобы обеспечить эту функциональность, создайте две версии метода `RedirectUser`. Первый из них должен принимать только индекс страницы для вывода, а второй принимает индекс страницы и выражение сортировки.

[!code-csharp[Main](sorting-data-in-a-datalist-or-repeater-control-cs/samples/sample7.cs)]

В первом примере в этом руководстве мы создали интерфейс сортировки с помощью DropDownList. В этом примере мы будем использовать три веб-элемента управления "Кнопка", расположенные над элементом DataList, для сортировки по `ProductName`, один для `CategoryName`и один для `SupplierName`. Добавьте три веб-элемента управления "Кнопка", задав их `ID` и свойства `Text` соответствующим образом:

[!code-aspx[Main](sorting-data-in-a-datalist-or-repeater-control-cs/samples/sample8.aspx)]

Затем создайте обработчик событий `Click` для каждого из них. Обработчики событий должны вызывать метод `RedirectUser`, возвращая пользователя на первую страницу с помощью соответствующего выражения сортировки.

[!code-csharp[Main](sorting-data-in-a-datalist-or-repeater-control-cs/samples/sample9.cs)]

При первом посещении страницы данные сортируются по названию продукта в алфавитном порядке (см. рис. 9). Нажмите кнопку Далее, чтобы перейти на вторую страницу данных, а затем нажмите кнопку Сортировать по категории. Это возвращает нам первую страницу данных, отсортированную по имени категории (см. рис. 10). Аналогичным образом, при нажатии кнопки Сортировать по поставщику данные сортируются по поставщикам, начиная с первой страницы данных. Вариант сортировки запоминается по мере постраничного просмотра данных. На рис. 11 показана страница после сортировки по категории, а затем переводится на страницу тринадцатого данных.

[![продукты сортируются по категориям](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image27.png)](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image26.png)

**Рис. 10**. продукты сортируются по категориям ([щелкните, чтобы просмотреть изображение с полным размером](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image28.png))

[![выражение сортировки запоминается при разбиении по страницам данных](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image30.png)](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image29.png)

**Рис. 11**. выражение сортировки запоминается при разбиении по страницам данных ([щелкните, чтобы просмотреть изображение с полным размером](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image31.png))

## <a name="step-6-custom-paging-through-records-in-a-repeater"></a>Шаг 6. пользовательское разбиение по записям в элементе Repeater

Пример элемента управления DataList, проверенный на шаге 5, просматривает данные с помощью неэффективного метода разбиения по страницам по умолчанию. При разбиении на страницы достаточно большого объема данных необходимо использовать настраиваемое разбиение по страницам. Вернувшись к [эффективному разбиению на страницы больших объемов данных](../paging-and-sorting/efficiently-paging-through-large-amounts-of-data-cs.md) и [сортировку пользовательских](../paging-and-sorting/sorting-custom-paged-data-cs.md) учебных курсов по данным, мы рассматривали различия между стандартным и пользовательским разбиением по страницам и созданными методами в BLL для использования пользовательского разбиения на страницы и сортировки данных, настраиваемых на странице. В частности, в этих двух предыдущих учебных курсах мы добавили в класс `ProductsBLL` следующие три метода:

- `GetProductsPaged(startRowIndex, maximumRows)` возвращает определенное подмножество записей, начиная с *startRowIndex* и не превышающих *maximumRows*.
- `GetProductsPagedAndSorted(sortExpression, startRowIndex, maximumRows)` возвращает конкретное подмножество записей, отсортированных по указанному входному параметру *sortExpression* .
- `TotalNumberOfProducts()` предоставляет общее количество записей в таблице `Products` базы данных.

Эти методы можно использовать для эффективной страницы и сортировки данных с помощью элемента управления DataList или Repeater. Чтобы проиллюстрировать это, давайте начнем с создания элемента управления Repeater с поддержкой пользовательского разбиения по страницам. Затем мы добавим возможности сортировки.

Откройте страницу `SortingWithCustomPaging.aspx` в папке `PagingSortingDataListRepeater` и добавьте к странице элемент Repeater, установив для свойства `ID` значение `Products`. В смарт-теге Repeater s создайте новый элемент управления ObjectDataSource с именем `ProductsDataSource`. Настройте его для выбора данных из `GetProductsPaged` метода `ProductsBLL` классов.

[![настроить ObjectDataSource для использования метода GetProductsPaged класса ProductsBLL](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image33.png)](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image32.png)

**Рис. 12**. Настройка ObjectDataSource для использования метода `GetProductsPaged` `ProductsBLL` классов ([щелкните, чтобы просмотреть изображение с полным размером](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image34.png))

Задайте для раскрывающихся списков на вкладках обновление, вставить и удалить значение (нет), а затем нажмите кнопку Далее. Мастер настройки источников данных теперь запрашивает источники `GetProductsPaged` Method s *startRowIndex* и *maximumRows* input Parameters. В действительности эти входные параметры не учитываются. Вместо этого значения *startRowIndex* и *maximumRows* будут передаваться через свойство `Arguments` в обработчике событий ObjectDataSource `Selecting`, точно так же, как мы указали *sortExpression* в этом учебнике первой демонстрацией. Поэтому не задавайте в раскрывающихся списках источник параметров в мастере значение нет.

[![оставьте для источников параметров значение нет.](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image36.png)](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image35.png)

**Рис. 13**. Оставьте для источников параметров значение None ([щелкните, чтобы просмотреть изображение с полным размером](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image37.png)).

> [!NOTE]
> *Не* устанавливайте для свойства ObjectDataSource `EnablePaging` значение `true`. Это приведет к тому, что ObjectDataSource автоматически включит собственные параметры *startRowIndex* и *maximumRows* в список существующих параметров `SelectMethod` s. Свойство `EnablePaging` удобно использовать при привязке настраиваемых данных с страничными данными к элементу управления GridView, DetailsView или FormView, поскольку эти элементы управления предполагают определенное поведение от ObjectDataSource, которое доступно только при `true`свойства `EnablePaging`. Поскольку необходимо вручную добавить поддержку разбиения по страницам для элементов управления DataList и Repeater, оставьте для этого свойства значение `false` (по умолчанию), так как мы внедрить в необходимой функциональности непосредственно на странице ASP.NET.

Наконец, определите `ItemTemplate` Repeater s, чтобы отображались название, Категория и поставщик продукта. После этих изменений декларативный синтаксис Repeater и ObjectDataSource должен выглядеть следующим образом:

[!code-aspx[Main](sorting-data-in-a-datalist-or-repeater-control-cs/samples/sample10.aspx)]

Уделите время посетить страницу в браузере и обратите внимание, что записи не возвращаются. Это связано с тем, что мы еще не указали значения параметров *startRowIndex* и *maximumRows* . Таким образом, значения 0 передаются в обоих случаях. Чтобы указать эти значения, создайте обработчик событий для события `Selecting` ObjectDataSource и задайте значения этих параметров программным путем в жестко запрограммированные значения 0 и 5 соответственно:

[!code-csharp[Main](sorting-data-in-a-datalist-or-repeater-control-cs/samples/sample11.cs)]

При таком изменении на странице при просмотре в браузере отображаются первые пять продуктов.

[![отображаются первые пять записей](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image39.png)](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image38.png)

**Рис. 14**. Отображение первых пяти записей ([щелкните, чтобы просмотреть изображение с полным размером](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image40.png))

> [!NOTE]
> Продукты, перечисленные на рис. 14, сортируются по названию продукта, так как хранимая процедура `GetProductsPaged`, выполняющая эффективный пользовательский запрос разбиения на страницы, упорядочивает результаты по `ProductName`.

Чтобы позволить пользователю проходить по шагам страниц, необходимо отследить индексы начальной и максимальной строк и запоминать эти значения во всех обратных передачах. В примере с подкачкой по умолчанию мы использовали поля QueryString для сохранения этих значений. для этой демонстрации позвольте нам сохранить эти сведения в состоянии просмотра страницы. Создайте следующие два свойства:

[!code-csharp[Main](sorting-data-in-a-datalist-or-repeater-control-cs/samples/sample12.cs)]

Затем обновите код в обработчике событий выбора, чтобы он использовал свойства `StartRowIndex` и `MaximumRows`, а не жестко запрограммированные значения 0 и 5.

[!code-csharp[Main](sorting-data-in-a-datalist-or-repeater-control-cs/samples/sample13.cs)]

На этом этапе страница по-прежнему показывает только первые пять записей. Тем не менее, с этими свойствами мы повторно готовы к созданию интерфейса разбиения по страницам.

## <a name="adding-the-paging-interface"></a>Добавление интерфейса разбиения на страницы

Позвольте использовать тот же самый первый, предыдущий, последний интерфейс разбиения по страницам, используемый в примере по умолчанию, включая веб-элемент управления Label, отображающий просматриваемую страницу данных и общее количество страниц. Добавьте четыре веб-элемента управления "Кнопка" и метку под элементом Repeater.

[!code-aspx[Main](sorting-data-in-a-datalist-or-repeater-control-cs/samples/sample14.aspx)]

Затем создайте обработчики событий `Click` для четырех кнопок. При нажатии одной из этих кнопок необходимо обновить `StartRowIndex` и повторно привязать данные к элементу Repeater. Код для первой, предыдущей и следующей кнопок достаточно прост, но для последней кнопки как определить индекс начальной строки для последней страницы данных? Чтобы вычислить этот индекс, а также определить, должны ли быть включены кнопки «Следующая» и «последняя», необходимо знать, сколько записей в общем объеме страницы. Это можно определить, вызвав метод `ProductsBLL` класса s `TotalNumberOfProducts()`. Давайте создадим свойство уровня страницы, доступное только для чтения, с именем `TotalRowCount`, которое возвращает результаты метода `TotalNumberOfProducts()`:

[!code-csharp[Main](sorting-data-in-a-datalist-or-repeater-control-cs/samples/sample15.cs)]

С помощью этого свойства теперь можно определить индекс начальной строки последней страницы. В частности, это целочисленный результат `TotalRowCount` минус 1, разделенный на `MaximumRows`, умноженный на `MaximumRows`. Теперь можно написать обработчики событий `Click` для четырех кнопок интерфейса разбиения на страницы:

[!code-csharp[Main](sorting-data-in-a-datalist-or-repeater-control-cs/samples/sample16.cs)]

Наконец, необходимо отключить первую и предыдущую кнопки в интерфейсе разбиения по страницам при просмотре первой страницы данных и кнопок «Далее» и «последняя» при просмотре последней страницы. Для этого добавьте следующий код в обработчик событий ObjectDataSource `Selecting`:

[!code-csharp[Main](sorting-data-in-a-datalist-or-repeater-control-cs/samples/sample17.cs)]

После добавления этих `Click` обработчиков событий и кода для включения или отключения элементов интерфейса разбиения на страницы на основе текущего индекса начальной строки проверьте страницу в браузере. Как показано на рис. 15, при первом посещении страницы будут отключены первая и предыдущая кнопки. При нажатии кнопки Далее отображается вторая страница данных, а при нажатии кнопки последний отображается последняя страница (см. рис. 16 и 17). При просмотре последней страницы данных отключаются обе кнопки: Следующая и последняя.

[![кнопки "Предыдущая" и "Последняя" отключены при просмотре первой страницы продуктов](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image42.png)](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image41.png)

**Рис. 15**. кнопки "Предыдущий" и "последний" отключены при просмотре первой страницы продуктов ([щелкните, чтобы просмотреть изображение с полным размером](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image43.png))

[![отображается вторая страница продуктов](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image45.png)](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image44.png)

**Рис. 16**. Отображение второй страницы продуктов ([щелкните, чтобы просмотреть изображение с полным размером](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image46.png))

[![нажатии кнопки Last отображает последнюю страницу данных](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image48.png)](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image47.png)

**Рис. 17**. нажатие кнопки Last отображает последнюю страницу данных ([щелкните, чтобы просмотреть изображение с полным размером](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image49.png))

## <a name="step-7-including-sorting-support-with-the-custom-paged-repeater"></a>Шаг 7. Включение поддержки сортировки с помощью настраиваемого повторителя на страницы

Теперь, когда пользовательское разбиение по страницам реализовано, мы повторно готовы к включению поддержки сортировки. Метод `ProductsBLL` классов `GetProductsPagedAndSorted` имеет те же входные параметры *startRowIndex* и *maximumRows* , что и `GetProductsPaged`, но допускает дополнительный входной параметр *sortExpression* . Чтобы использовать метод `GetProductsPagedAndSorted` из `SortingWithCustomPaging.aspx`, необходимо выполнить следующие действия.

1. Измените свойство `SelectMethod` ObjectDataSource s с `GetProductsPaged` на `GetProductsPagedAndSorted`.
2. Добавьте объект `Parameter` *sortExpression* в коллекцию `SelectParameters` ObjectDataSource.
3. Создайте закрытое свойство `SortExpression` на уровне страницы, сохраняющее свое значение во всех обратных передачах через состояние просмотра страницы.
4. Обновите обработчик событий `Selecting` ObjectDataSource s, чтобы назначить параметру ObjectDataSource *sortExpression* значение свойства `SortExpression` уровня страницы.
5. Создайте интерфейс сортировки.

Начните с обновления свойства `SelectMethod` ObjectDataSource s и добавления `Parameter`*sortExpression* . Убедитесь, что свойство *sortExpression* `Parameter` s `Type` имеет значение `String`. После выполнения этих первых двух задач декларативная разметка ObjectDataSource s должна выглядеть следующим образом:

[!code-aspx[Main](sorting-data-in-a-datalist-or-repeater-control-cs/samples/sample18.aspx)]

Далее нам нужно свойство `SortExpression` уровня страницы, значение которого сериализуется в состояние представления. Если значение выражения сортировки не задано, используйте ProductName в качестве значения по умолчанию:

[!code-csharp[Main](sorting-data-in-a-datalist-or-repeater-control-cs/samples/sample19.cs)]

Прежде чем ObjectDataSource вызовет метод `GetProductsPagedAndSorted`, необходимо установить `Parameter` *sortExpression* в значение свойства `SortExpression`. В обработчике событий `Selecting` добавьте следующую строку кода:

[!code-csharp[Main](sorting-data-in-a-datalist-or-repeater-control-cs/samples/sample20.cs)]

Остается только реализовать интерфейс сортировки. Как и в последнем примере, пусть интерфейс сортировки реализован с помощью трех веб-элементов управления "Кнопка", которые позволяют пользователю сортировать результаты по названию продукта, категории или поставщику.

[!code-aspx[Main](sorting-data-in-a-datalist-or-repeater-control-cs/samples/sample21.aspx)]

Создайте `Click` обработчиков событий для этих трех элементов управления "Кнопка". В обработчике событий сбросьте `StartRowIndex` в значение 0, присвойте `SortExpression` подходящему значению и выполните повторную привязку данных к элементу Repeater:

[!code-csharp[Main](sorting-data-in-a-datalist-or-repeater-control-cs/samples/sample22.cs)]

Вот и все! Хотя существует ряд действий по реализации пользовательского разбиения по страницам и сортировки, шаги были очень похожи на те, что были необходимы для разбиения по страницам по умолчанию. На рис. 18 показаны продукты при просмотре последней страницы данных при сортировке по категории.

[![на последней странице данных, отсортированной по категории, отображается](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image51.png)](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image50.png)

**Рис. 18**. Отображение последней страницы данных, отсортированных по категориям ([щелкните, чтобы просмотреть изображение с полным размером](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image52.png))

> [!NOTE]
> В предыдущих примерах при сортировке по поставщику SupplierName был использован в качестве выражения сортировки. Однако для реализации пользовательского разбиения по страницам необходимо использовать CompanyName. Это происходит потому, что хранимая процедура, отвечающая за реализацию пользовательского разбиения `GetProductsPagedAndSorted` по страницам, передает выражение сортировки в ключевое слово `ROW_NUMBER()`, ключевому слову `ROW_NUMBER()` требуется фактическое имя столбца, а не псевдоним. Поэтому необходимо использовать `CompanyName` (имя столбца в `Suppliers` таблице) вместо псевдонима, используемого в запросе `SELECT` (`SupplierName`) для выражения сортировки.

## <a name="summary"></a>Сводка

Ни элемент управления DataList, ни Repeater не поддерживают встроенную поддержку сортировки, но с небольшой частью кода и пользовательского интерфейса сортировки, такие функциональные возможности можно добавить. При реализации сортировки, но без разбиения по страницам выражение сортировки можно указать с помощью объекта `DataSourceSelectArguments`, переданного в метод `Select` ObjectDataSource. Это свойство `DataSourceSelectArguments` `SortExpression` объекта можно назначить в обработчике событий ObjectDataSource `Selecting`.

Чтобы добавить возможности сортировки в элемент управления DataList или Repeater, который уже обеспечивает поддержку разбиения по страницам, самый простой подход заключается в настройке уровня бизнес-логики для включения метода, принимающего выражение сортировки. Эти сведения затем можно передать с помощью параметра в `SelectParameters`ObjectDataSource.

Этот учебник завершает изучение разбиения по страницам и сортировку с помощью элементов управления DataList и Repeater. В следующем и последнем учебнике рассматривается добавление веб-элементов управления "Кнопка" в шаблоны DataList и Repeater s для предоставления некоторых пользовательских функций, инициированных пользователем, для отдельных элементов.

Поздравляем с программированием!

## <a name="about-the-author"></a>Об авторе

[Скотт Митчелл](http://www.4guysfromrolla.com/ScottMitchell.shtml), автор семи книг по ASP/ASP. NET и основатель [4GuysFromRolla.com](http://www.4guysfromrolla.com), работал с веб-технологиями Майкрософт с 1998. Скотт работает как независимый консультант, преподаватель и модуль записи. Его последняя книга — [*Sams обучать себя ASP.NET 2,0 за 24 часа*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco). Он доступен по адресу [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) или через его блог, который можно найти по адресу [http://ScottOnWriting.NET](http://ScottOnWriting.NET).

## <a name="special-thanks-to"></a>Специальная благодарность

Эта серия руководств была рассмотрена многими полезными рецензентами. Специалистом по интересу для работы с этим руководством был Дэвид суру. Хотите ознакомиться с моими будущими статьями MSDN? Если это так, расположите строку в [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Назад](paging-report-data-in-a-datalist-or-repeater-control-cs.md)
> [Вперед](paging-report-data-in-a-datalist-or-repeater-control-vb.md)
