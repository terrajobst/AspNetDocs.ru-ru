---
uid: web-forms/overview/data-access/advanced-data-access-scenarios/adding-additional-datatable-columns-vb
title: Добавление дополнительных столбцов таблицы данных (VB) | Документация Майкрософт
author: rick-anderson
description: При использовании мастера TableAdapter для создания типизированного набора данных соответствующая таблица DataTable содержит столбцы, возвращаемые основным запросом к базе данных. Но там...
ms.author: riande
ms.date: 07/18/2007
ms.assetid: 1e8e65f9-fe3e-4250-810b-c90227786bed
msc.legacyurl: /web-forms/overview/data-access/advanced-data-access-scenarios/adding-additional-datatable-columns-vb
msc.type: authoredcontent
ms.openlocfilehash: 3a55f8bc4d3508387927ca81674073a001867de7
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/28/2019
ms.locfileid: "74608295"
---
# <a name="adding-additional-datatable-columns-vb"></a>Добавление дополнительных столбцов DataTable (VB)

по [Скотт Митчелл](https://twitter.com/ScottOnWriting)

[Скачать код](https://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_70_VB.zip) или [скачать PDF](adding-additional-datatable-columns-vb/_static/datatutorial70vb1.pdf)

> При использовании мастера TableAdapter для создания типизированного набора данных соответствующая таблица DataTable содержит столбцы, возвращаемые основным запросом к базе данных. Но бывают случаи, когда таблица данных должна включать дополнительные столбцы. В этом учебнике мы рассмотрим, почему рекомендуется использовать хранимые процедуры, если нам нужны дополнительные столбцы DataTable.

## <a name="introduction"></a>Введение

При добавлении TableAdapter к типизированному набору данных соответствующая схема DataTable s определяется основным запросом TableAdapter s. Например, если основной запрос возвращает поля данных *a*, *b*и *c*, то объект DataTable будет иметь три соответствующих столбца с именами *A*, *b*и *c*. В дополнение к основному запросу TableAdapter может включать дополнительные запросы, возвращающие, возможно, подмножество данных на основе какого-либо параметра. Например, в дополнение к основному запросу `ProductsTableAdapter` s, который возвращает сведения обо всех продуктах, он также содержит методы, такие как `GetProductsByCategoryID(categoryID)` и `GetProductByProductID(productID)`, возвращающие определенные сведения о продукте на основе указанного параметра.

Модель, отражающая схему DataTable s, отражает основной запрос TableAdapter s, хорошо работает, если все методы TableAdapter возвращают то же или меньше полей данных, чем указано в основном запросе. Если методу TableAdapter требуется возвращать дополнительные поля данных, необходимо соответствующим образом расширить схему DataTable s. В « [основной/подробности» с помощью маркированного списка основных записей с](../filtering-scenarios-with-the-datalist-and-repeater/master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb.md) руководством по DataList мы добавили метод в `CategoriesTableAdapter`, которые возвращали поля данных `CategoryID`, `CategoryName`и `Description`, определенные в основном запросе и `NumberOfProducts`, дополнительное поле данных, которое сообщило о количестве продуктов, связанных с каждой категорией. Мы вручную добавили новый столбец в `CategoriesDataTable` для записи значения поля данных `NumberOfProducts` из этого нового метода.

Как обсуждалось в руководстве по [отправке файлов](../working-with-binary-files/uploading-files-vb.md) , необходимо соблюдать осторожность при использовании адаптеров таблиц, использующих специальные инструкции SQL и имеющих методы, поля данных которых не точно соответствуют основному запросу. Если мастер настройки TableAdapter запускается повторно, он обновляет все методы TableAdapter, чтобы список полей данных соответствовал основному запросу. Таким образом, любые методы с настроенными списками столбцов будут возвращаться к списку столбцов основного запроса, не возвращая ожидаемые данные. Эта проблема не возникает при использовании хранимых процедур.

В этом учебнике мы рассмотрим, как расширить схему DataTable s для включения дополнительных столбцов. Из-за хрупкостии TableAdapter при использовании специальных инструкций SQL в этом учебнике мы будем использовать хранимые процедуры. Дополнительные сведения о настройке TableAdapter для использования хранимых процедур см. в разделе [Создание новых хранимых процедур для адаптеров таблиц](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb.md) с типизированным набором данных и [использование существующих хранимых процедур](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb.md) .

## <a name="step-1-adding-apricequartilecolumn-to-theproductsdatatable"></a>Шаг 1. Добавление`PriceQuartile`столбца в`ProductsDataTable`

В руководстве *Создание новых хранимых процедур для адаптеров таблиц типизированного набора данных* мы создали типизированный набор данных с именем `NorthwindWithSprocs`. В настоящее время этот набор данных содержит два объекта DataTable: `ProductsDataTable` и `EmployeesDataTable`. `ProductsTableAdapter` имеет следующие три метода:

- `GetProducts` — основной запрос, который возвращает все записи из таблицы `Products`
- `GetProductsByCategoryID(categoryID)` — возвращает все продукты с указанным *CategoryID*.
- `GetProductByProductID(productID)` — Возвращает определенный продукт с указанным *ProductID*.

Основной запрос и два дополнительных метода возвращают один и тот же набор полей данных, а именно все столбцы из таблицы `Products`. Нет коррелированных вложенных запросов или `JOIN` s извлекать связанные данные из `Categories` или `Suppliers` таблиц. Таким образом, `ProductsDataTable` имеет соответствующий столбец для каждого поля в `Products` таблице.

В этом руководстве мы добавим метод в `ProductsTableAdapter` с именем `GetProductsWithPriceQuartile`, который возвращает все продукты. В дополнение к стандартным полям данных продукта `GetProductsWithPriceQuartile` также включает в себя `PriceQuartile` поле данных, которое указывает, в какой квартиль приходится цена продукта. Например, продукты, цены которых находятся в наиболее дорогих 25%, будут иметь `PriceQuartile` значение 1, а цены, которые попадают на 25%, будут иметь значение 4. Прежде чем беспокоиться о создании хранимой процедуры для возврата этих сведений, сначала необходимо обновить `ProductsDataTable`, чтобы включить столбец для хранения результатов `PriceQuartile` при использовании метода `GetProductsWithPriceQuartile`.

Откройте `NorthwindWithSprocs` набор данных и щелкните правой кнопкой мыши `ProductsDataTable`. Выберите Добавить в контекстном меню, а затем выберите столбец.

[![добавить новый столбец в Продуктсдататабле](adding-additional-datatable-columns-vb/_static/image2.png)](adding-additional-datatable-columns-vb/_static/image1.png)

**Рис. 1**. Добавление нового столбца в `ProductsDataTable` ([щелкните, чтобы просмотреть изображение с полным размером](adding-additional-datatable-columns-vb/_static/image3.png))

Будет добавлен новый столбец в таблицу DataTable с именем Column1 типа `System.String`. Необходимо изменить имя этого столбца на Прицекуартиле и его тип на `System.Int32`, так как он будет использоваться для хранения числа от 1 до 4. Выберите только что добавленный столбец в `ProductsDataTable` и в окно свойств задайте для свойства `Name` значение Прицекуартиле, а для свойства `DataType` — `System.Int32`.

[![задать имя нового столбца и свойства DataType](adding-additional-datatable-columns-vb/_static/image5.png)](adding-additional-datatable-columns-vb/_static/image4.png)

**Рис. 2**. Установка новых столбцов `Name` и `DataType` свойств ([щелкните, чтобы просмотреть изображение с полным размером](adding-additional-datatable-columns-vb/_static/image6.png))

Как показано на рис. 2, существуют дополнительные свойства, которые могут быть заданы, например, должны ли значения в столбце быть уникальными, если столбец является автоматически увеличивающимся, независимо от того, разрешены ли значения `NULL` базы данных и т. д. Оставьте для этих свойств значения по умолчанию.

## <a name="step-2-creating-thegetproductswithpricequartilemethod"></a>Шаг 2. Создание метода`GetProductsWithPriceQuartile`

Теперь, когда `ProductsDataTable` был обновлен для включения столбца `PriceQuartile`, мы готовы создать метод `GetProductsWithPriceQuartile`. Для начала щелкните правой кнопкой мыши TableAdapter и выберите команду Добавить запрос в контекстном меню. Откроется мастер настройки запросов адаптера таблицы TableAdapter, который сначала запрашивает у нас необходимость использовать специальные инструкции SQL или новую или существующую хранимую процедуру. Так как у нас еще нет хранимой процедуры, возвращающей данные о ценах квартиль, давайте разрешите TableAdapter создать эту хранимую процедуру для нас. Выберите параметр создать новую хранимую процедуру и нажмите кнопку Далее.

[![заставить мастер TableAdapter создать хранимую процедуру для нас](adding-additional-datatable-columns-vb/_static/image8.png)](adding-additional-datatable-columns-vb/_static/image7.png)

**Рис. 3**. мастеру TableAdapter создать хранимую процедуру для нас ([щелкните, чтобы просмотреть изображение с полным размером](adding-additional-datatable-columns-vb/_static/image9.png))

На следующем экране, показанном на рис. 4, мастер запрашивает тип добавляемого запроса. Так как метод `GetProductsWithPriceQuartile` возвратит все столбцы и записи из таблицы `Products`, выберите параметр выбрать, возвращающий строки и нажмите кнопку Далее.

[![наш запрос будет инструкцией SELECT, возвращающей несколько строк.](adding-additional-datatable-columns-vb/_static/image11.png)](adding-additional-datatable-columns-vb/_static/image10.png)

**Рис. 4**. наш запрос будет `SELECT` инструкцией, возвращающей несколько строк ([щелкните, чтобы просмотреть изображение с полным размером](adding-additional-datatable-columns-vb/_static/image12.png)).

Далее будет предложено ввести запрос `SELECT`. В мастере введите следующий запрос:

[!code-sql[Main](adding-additional-datatable-columns-vb/samples/sample1.sql)]

В приведенном выше запросе используется новая [функция`NTILE`](https://msdn.microsoft.com/library/ms175126.aspx) SQL Server 2005 s, чтобы разделить результаты на четыре группы, в которых группы определяются `UnitPrice` значениями, отсортированными в порядке убывания.

К сожалению, конструктор запросов не знает, как проанализировать ключевое слово `OVER` и отобразит сообщение об ошибке при синтаксическом анализе запроса. Поэтому введите приведенный выше запрос непосредственно в текстовое поле в мастере без использования конструктор запросов.

> [!NOTE]
> Дополнительные сведения о NTILE и SQL Server 2005 s других функциях ранжирования см. в разделе [Получение ранжированных результатов с помощью Microsoft SQL Server 2005](http://www.4guysfromrolla.com/webtech/010406-1.shtml) и [функции ранжирования](https://msdn.microsoft.com/library/ms189798.aspx) из [электронной документации по SQL Server 2005](https://msdn.microsoft.com/library/ms189798.aspx).

После ввода `SELECT` запроса и нажатия кнопки Далее мастер предложит указать имя создаваемой хранимой процедуры. Присвойте новой хранимой процедуре имя `Products_SelectWithPriceQuartile` и нажмите кнопку Далее.

[![имя хранимой процедуры Products_SelectWithPriceQuartile](adding-additional-datatable-columns-vb/_static/image14.png)](adding-additional-datatable-columns-vb/_static/image13.png)

**Рис. 5**. присвойте хранимой процедуре имя `Products_SelectWithPriceQuartile` ([щелкните, чтобы просмотреть изображение с полным размером](adding-additional-datatable-columns-vb/_static/image15.png))

Наконец, мы предлагаем вам указать имя методов TableAdapter. Оставьте установленными флажки заполнить таблицу данных и вернуть таблицу DataTable, а затем присвойте методам `FillWithPriceQuartile` и `GetProductsWithPriceQuartile`.

[![назовите методы TableAdapter s и нажмите кнопку Готово.](adding-additional-datatable-columns-vb/_static/image17.png)](adding-additional-datatable-columns-vb/_static/image16.png)

**Рис. 6**. Назовите методы TableAdapter и нажмите кнопку Готово ([щелкните, чтобы просмотреть изображение с полным размером](adding-additional-datatable-columns-vb/_static/image18.png)).

Используя указанный запрос `SELECT` и хранимую процедуру и методы TableAdapter, нажмите кнопку Готово, чтобы завершить работу мастера. На этом этапе в мастере может появиться предупреждение или два сообщения о том, что конструкция или инструкция SQL `OVER` не поддерживается. Эти предупреждения можно игнорировать.

После завершения работы мастера TableAdapter должен включать методы `FillWithPriceQuartile` и `GetProductsWithPriceQuartile`, а база данных должна содержать хранимую процедуру с именем `Products_SelectWithPriceQuartile`. Уделите время, чтобы убедиться, что TableAdapter действительно содержит этот новый метод и что хранимая процедура правильно добавлена в базу данных. Если при проверке базы данных хранимая процедура не отображается, попробуйте щелкнуть правой кнопкой мыши папку Хранимые процедуры и выбрать команду Обновить.

![Проверка добавления нового метода в TableAdapter](adding-additional-datatable-columns-vb/_static/image19.png)

**Рис. 7**. Проверка добавления нового метода в TableAdapter

[![убедиться, что база данных содержит хранимую процедуру Products_SelectWithPriceQuartile](adding-additional-datatable-columns-vb/_static/image21.png)](adding-additional-datatable-columns-vb/_static/image20.png)

**Рис. 8**. Убедитесь, что база данных содержит `Products_SelectWithPriceQuartile` хранимую процедуру ([щелкните, чтобы просмотреть изображение с полным размером](adding-additional-datatable-columns-vb/_static/image22.png))

> [!NOTE]
> Одним из преимуществ использования хранимых процедур вместо специальных инструкций SQL является то, что повторное выполнение мастера настройки TableAdapter не приведет к изменению списков столбцов хранимых процедур. Проверьте это, щелкнув правой кнопкой мыши TableAdapter, выбрав параметр "Настройка" в контекстном меню, чтобы запустить мастер, и нажмите кнопку "Готово", чтобы завершить работу мастера. Затем перейдите к базе данных и просмотрите `Products_SelectWithPriceQuartile` хранимую процедуру. Обратите внимание, что список столбцов не был изменен. Если мы использовали специальные инструкции SQL, повторный запуск мастера настройки адаптера таблицы приведет к возврату этого списка столбцов запроса в соответствие с основным списком столбцов запроса, тем самым удаляя инструкцию NTILE из запроса, используемого методом `GetProductsWithPriceQuartile`.

Когда вызывается метод `GetProductsWithPriceQuartile` уровня доступа к данным, TableAdapter выполняет хранимую процедуру `Products_SelectWithPriceQuartile` и добавляет строку в `ProductsDataTable` для каждой возвращенной записи. Поля данных, возвращаемые хранимой процедурой, сопоставляются со столбцами `ProductsDataTable` s. Поскольку в хранимой процедуре возвращается `PriceQuartile` поле данных, его значение присваивается столбцу `ProductsDataTable` s `PriceQuartile`.

Для тех методов TableAdapter, запросы которых не возвращают `PriceQuartile` поле данных, `PriceQuartile` столбец s имеет значение, заданное свойством `DefaultValue`. Как показано на рис. 2, это значение устанавливается равным `DBNull`, по умолчанию. Если вы предпочитаете другое значение по умолчанию, просто задайте соответствующее свойство `DefaultValue`. Просто убедитесь, что значение `DefaultValue` допустимо для столбцов `DataType` (т. е. `System.Int32` для столбца `PriceQuartile`).

На этом этапе мы выполнили необходимые действия по добавлению дополнительного столбца в таблицу DataTable. Чтобы убедиться, что этот дополнительный столбец работает должным образом, давайте создадим страницу ASP.NET, на которой отображаются названия продуктов, цены и цены квартиль. Тем не менее, прежде всего необходимо обновить уровень бизнес-логики, включив в него метод, который вызывает метод DAL s `GetProductsWithPriceQuartile`. На шаге 3 мы будем обновлять BLL, а затем создаем страницу ASP.NET на шаге 4.

## <a name="step-3-augmenting-the-business-logic-layer"></a>Шаг 3. дополнение уровня бизнес-логики

Прежде чем использовать новый метод `GetProductsWithPriceQuartile` на уровне представления, необходимо сначала добавить соответствующий метод в BLL. Откройте файл класса `ProductsBLLWithSprocs` и добавьте следующий код:

[!code-vb[Main](adding-additional-datatable-columns-vb/samples/sample2.vb)]

Как и другие методы получения данных в `ProductsBLLWithSprocs`, метод `GetProductsWithPriceQuartile` просто вызывает DAL, соответствующий методу `GetProductsWithPriceQuartile` и возвращает результаты.

## <a name="step-4-displaying-the-price-quartile-information-in-an-aspnet-web-page"></a>Шаг 4. Отображение сведений о стоимости квартиль на веб-странице ASP.NET

После добавления BLL мы повторно готовы к созданию страницы ASP.NET, на которой показана Цена квартиль для каждого продукта. Откройте страницу `AddingColumns.aspx` в папке `AdvancedDAL` и перетащите элемент управления GridView с панели инструментов в конструктор, установив для свойства `ID` значение `Products`. В смарт-теге GridView s привяжите его к новому ObjectDataSource с именем `ProductsDataSource`. Настройте ObjectDataSource для использования метода `GetProductsWithPriceQuartile` `ProductsBLLWithSprocs` классов. Так как это будет сетка только для чтения, установите в раскрывающихся списках на вкладках обновление, вставка и удаление значение (нет).

[![настроить ObjectDataSource для использования класса Продуктсбллвисспрокс](adding-additional-datatable-columns-vb/_static/image24.png)](adding-additional-datatable-columns-vb/_static/image23.png)

**Рис. 9**. Настройка ObjectDataSource для использования класса `ProductsBLLWithSprocs` ([щелкните, чтобы просмотреть изображение с полным размером](adding-additional-datatable-columns-vb/_static/image25.png))

[![получить сведения о продукте из метода Жетпродуктсвисприцекуартиле](adding-additional-datatable-columns-vb/_static/image27.png)](adding-additional-datatable-columns-vb/_static/image26.png)

**Рис. 10**. Получение сведений о продукте из метода `GetProductsWithPriceQuartile` ([щелкните, чтобы просмотреть изображение с полным размером](adding-additional-datatable-columns-vb/_static/image28.png))

После завершения работы мастера настройки источника данных Visual Studio автоматически добавит BoundField или CheckBoxField в GridView для каждого из полей данных, возвращаемых методом. Одно из этих полей данных — `PriceQuartile`, то есть столбец, добавленный в `ProductsDataTable` на шаге 1.

Измените поля GridView s, удалив все, кроме `ProductName`, `UnitPrice`и `PriceQuartile` BoundFields. Настройте `UnitPrice` BoundField, чтобы отформатировать свое значение как денежную, а `UnitPrice` и `PriceQuartile` BoundFields, соответственно, выравнивание по центру. Наконец, измените оставшиеся свойства BoundFields `HeaderText` на Product, Price и Price квартиль соответственно. Кроме того, установите флажок Включить сортировку в смарт-теге GridView s.

После этих изменений декларативная разметка GridView и ObjectDataSource должна выглядеть следующим образом:

[!code-aspx[Main](adding-additional-datatable-columns-vb/samples/sample3.aspx)]

На рис. 11 показана эта страница при посещении через браузер. Обратите внимание, что изначально продукты упорядочиваются по цене в порядке убывания, при этом каждому продукту назначается соответствующее значение `PriceQuartile`. Разумеется, эти данные можно отсортировать по другим критериям со значением столбца price квартиль, по-прежнему отражающему ранжирование продукта по отношению к цене (см. рис. 12).

[![продукты упорядочиваются по ценам](adding-additional-datatable-columns-vb/_static/image30.png)](adding-additional-datatable-columns-vb/_static/image29.png)

**Рис. 11**. продукты упорядочены по ценам ([щелкните, чтобы просмотреть изображение с полным размером](adding-additional-datatable-columns-vb/_static/image31.png))

[![продукты упорядочиваются по именам](adding-additional-datatable-columns-vb/_static/image33.png)](adding-additional-datatable-columns-vb/_static/image32.png)

**Рис. 12**. продукты упорядочены по именам ([щелкните, чтобы просмотреть изображение с полным размером](adding-additional-datatable-columns-vb/_static/image34.png))

> [!NOTE]
> С помощью нескольких строк кода можно дополнить GridView таким образом, чтобы строки продукта закрашены на основе их `PriceQuartile` значения. Мы можем открасить эти продукты в первый квартиль светло-зеленый, а второй квартиль — желтой и т. д. Я рекомендую добавить эту функцию в некоторое время. Если требуется обновить форматирование элемента управления GridView, ознакомьтесь с учебником [пользовательское форматирование на основе данных](../custom-formatting/custom-formatting-based-upon-data-vb.md) .

## <a name="an-alternative-approach---creating-another-tableadapter"></a>Альтернативный подход — создание другого адаптера TableAdapter

Как было показано в этом руководстве, при добавлении метода в TableAdapter, который возвращает поля данных, отличные от тех, которые были введены основным запросом, можно добавить соответствующие столбцы в таблицу данных. Однако такой подход хорошо работает, только если в TableAdapter имеется небольшое количество методов, возвращающих различные поля данных, и если эти альтернативные поля данных не отличаются от основного запроса.

Вместо того чтобы добавлять столбцы в таблицу данных, можно добавить еще один адаптер таблицы к набору, который содержит методы из первого адаптера таблицы, возвращающие различные поля данных. В этом руководстве вместо того, чтобы добавлять столбец `PriceQuartile` в `ProductsDataTable` (где он используется только методом `GetProductsWithPriceQuartile`), можно было добавить дополнительный адаптер TableAdapter к набору данных с именем `ProductsWithPriceQuartileTableAdapter`, в котором в качестве основного запроса использовалась хранимая процедура `Products_SelectWithPriceQuartile`. ASP.NET страницы, необходимые для получения сведений о продукте с помощью произведения "цена", будут использовать `ProductsWithPriceQuartileTableAdapter`, а те, которые не могли бы продолжать использовать `ProductsTableAdapter`.

При добавлении нового адаптера таблицы DataTables остаются унтарнишед, а их столбцы точно отражают поля данных, возвращаемые их методами TableAdapter. Однако дополнительные адаптеры таблиц могут добавлять повторяющиеся задачи и функциональные возможности. Например, если ASP.NET страницы, на которых отображается `PriceQuartile` столбец, также требовались для поддержки вставки, обновления и удаления, `ProductsWithPriceQuartileTableAdapter` потребуется правильно настроить свойства `InsertCommand`, `UpdateCommand`и `DeleteCommand`. Хотя эти свойства будут зеркально отражены `ProductsTableAdapter` s, в этой конфигурации вводится дополнительный шаг. Более того, теперь существует два способа обновления, удаления или добавления продукта в базу данных — с помощью классов `ProductsTableAdapter` и `ProductsWithPriceQuartileTableAdapter`.

Загружаемый файл для этого учебника содержит класс `ProductsWithPriceQuartileTableAdapter` в наборе данных `NorthwindWithSprocs`, который иллюстрирует этот альтернативный подход.

## <a name="summary"></a>Сводка

В большинстве случаев все методы TableAdapter возвращают один и тот же набор полей данных, но бывают случаи, когда определенному методу или двум может потребоваться возврат дополнительного поля. Например, в « [основной/подробности» с помощью маркированного списка основных записей с учебником «сведения о DataList](../filtering-scenarios-with-the-datalist-and-repeater/master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb.md) » мы добавили метод в `CategoriesTableAdapter`, в дополнение к полям данных «основные запросы», возвращали поле `NumberOfProducts`, которое сообщило о количестве продуктов, связанных с каждой категорией. В этом учебнике мы рассмотрели Добавление метода в `ProductsTableAdapter`, который возвращал `PriceQuartile` поле в дополнение к полям данных основных запросов. Чтобы записать дополнительные поля данных, возвращаемые методами TableAdapter s, необходимо добавить соответствующие столбцы в таблицу данных.

Если вы планируете добавлять столбцы в таблицу данных вручную, рекомендуется использовать хранимые процедуры адаптера таблицы. Если TableAdapter использует специальные инструкции SQL, каждый раз при выполнении мастера настройки TableAdapter все списки полей данных методов возвращаются к полям данных, возвращаемым основным запросом. Эта проблема не распространяется на хранимые процедуры, поэтому они рекомендуются и использовались в этом руководстве.

Поздравляем с программированием!

## <a name="about-the-author"></a>Об авторе

[Скотт Митчелл](http://www.4guysfromrolla.com/ScottMitchell.shtml), автор семи книг по ASP/ASP. NET и основатель [4GuysFromRolla.com](http://www.4guysfromrolla.com), работал с веб-технологиями Майкрософт с 1998. Скотт работает как независимый консультант, преподаватель и модуль записи. Его последняя книга — [*Sams обучать себя ASP.NET 2,0 за 24 часа*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco). Он доступен по адресу [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) или через его блог, который можно найти по адресу [http://ScottOnWriting.NET](http://ScottOnWriting.NET).

## <a name="special-thanks-to"></a>Специальная благодарность

Эта серия руководств была рассмотрена многими полезными рецензентами. Потенциальные рецензенты для этого руководства: Рэнди Шмидт, Джеки редакторами, Бернадетте Леигх и Хилтон Гизнау. Хотите ознакомиться с моими будущими статьями MSDN? Если это так, расположите строку в [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Назад](updating-the-tableadapter-to-use-joins-vb.md)
> [Вперед](working-with-computed-columns-vb.md)
