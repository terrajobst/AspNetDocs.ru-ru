---
uid: web-forms/overview/data-access/advanced-data-access-scenarios/updating-the-tableadapter-to-use-joins-cs
title: Обновление TableAdapter для использования соединений (C#) | Документация Майкрософт
author: rick-anderson
description: При работе с базой данных часто запрашиваются данные, распределенные по нескольким таблицам. Чтобы получить данные из двух разных таблиц, можно использовать любой из них...
ms.author: riande
ms.date: 07/18/2007
ms.assetid: 675531a7-cb54-4dd6-89ac-2636e4c285a5
msc.legacyurl: /web-forms/overview/data-access/advanced-data-access-scenarios/updating-the-tableadapter-to-use-joins-cs
msc.type: authoredcontent
ms.openlocfilehash: 24ff3645783dabfcdef5ac313a2d4833e4998efc
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78427776"
---
# <a name="updating-the-tableadapter-to-use-joins-c"></a>Обновление адаптера таблицы TableAdapter для использования JOIN (C#)

по [Скотт Митчелл](https://twitter.com/ScottOnWriting)

[Скачать код](https://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_69_CS.zip) или [скачать PDF](updating-the-tableadapter-to-use-joins-cs/_static/datatutorial69cs1.pdf)

> При работе с базой данных часто запрашиваются данные, распределенные по нескольким таблицам. Для получения данных из двух разных таблиц можно использовать Коррелированный вложенный запрос или операцию JOIN. В этом учебнике мы сравниваем коррелированные вложенные запросы и синтаксис JOIN перед тем, как создать TableAdapter, включающий соединение в основном запросе.

## <a name="introduction"></a>Введение

В реляционных базах данных, с которыми мы заинтересованы в работе, часто распределяются по нескольким таблицам. Например, при отображении сведений о продукте, скорее всего, потребуется перечислить все продукты, соответствующие категории и имена поставщиков. Таблица `Products` имеет `CategoryID` и `SupplierID` значений, но фактические имена категорий и поставщиков находятся в таблицах `Categories` и `Suppliers` соответственно.

Чтобы получить сведения из другой связанной таблицы, можно использовать *коррелированные вложенные запросы* или `JOIN`*s*. Коррелированный вложенный запрос — это связанный `SELECT` запрос, который ссылается на столбцы внешнего запроса. Например, в учебнике [Создание уровня доступа к данным](../introduction/creating-a-data-access-layer-cs.md) мы использовали два коррелированных вложенных запроса в главном запросе `ProductsTableAdapter` s, чтобы получить имена категорий и поставщиков для каждого продукта. `JOIN` — это конструкция SQL, которая объединяет связанные строки из двух разных таблиц. Мы использовали `JOIN` в [запросах данных с помощью учебника по элементу управления SqlDataSource](../accessing-the-database-directly-from-an-aspnet-page/querying-data-with-the-sqldatasource-control-cs.md) , чтобы отобразить сведения о категории вместе с каждым продуктом.

Причина, по которой мы абстаинед из использования `JOIN` s с адаптерами таблиц TableAdapter, заключается в наличии ограничений в мастере адаптеров таблиц для автоматического создания соответствующих `INSERT`, `UPDATE`и `DELETE` инструкций. В частности, если основной запрос TableAdapter s содержит `JOIN` s, TableAdapter не может создать специальные инструкции SQL или хранимые процедуры для свойств `InsertCommand`, `UpdateCommand`и `DeleteCommand`.

В этом учебнике мы кратко сравниваем коррелированные вложенные запросы и `JOIN` s перед изучением того, как создать TableAdapter, включающий `JOIN` s в основной запрос.

## <a name="comparing-and-contrasting-correlated-subqueries-andjoin-s"></a>Сравнение и отличие коррелированных вложенных запросов и`JOIN` s

Помните, что `ProductsTableAdapter`, созданные в первом руководстве в наборе данных `Northwind`, используют коррелированные вложенные запросы для возврата каждой категории и имени поставщика в соответствии с соответствующими продуктами. Ниже приведен основной запрос `ProductsTableAdapter` s.

[!code-sql[Main](updating-the-tableadapter-to-use-joins-cs/samples/sample1.sql)]

Два коррелированных вложенных запроса — `(SELECT CategoryName FROM Categories WHERE Categories.CategoryID = Products.CategoryID)` и `(SELECT CompanyName FROM Suppliers WHERE Suppliers.SupplierID = Products.SupplierID)` — `SELECT` запросы, возвращающие одно значение для каждого продукта в виде дополнительного столбца в списке столбцов внешнего `SELECT` оператора.

Кроме того, можно использовать `JOIN` для возврата имени поставщика и категории каждого продукта. Следующий запрос возвращает те же выходные данные, что и предыдущий, но использует `JOIN` s вместо вложенных запросов:

[!code-sql[Main](updating-the-tableadapter-to-use-joins-cs/samples/sample2.sql)]

`JOIN` объединяет записи из одной таблицы с записями из другой таблицы на основе некоторых критериев. Например, в приведенном выше запросе `LEFT JOIN Categories ON Categories.CategoryID = Products.CategoryID` предписывает SQL Server объединить каждую запись продукта с записью категории, `CategoryID` значение которой соответствует значению `CategoryID` продукта. Объединенный результат позволяет нам работать с соответствующими полями категорий для каждого продукта (например, `CategoryName`).

> [!NOTE]
> `JOIN` s обычно используются при запросе данных из реляционных баз данных. Если вы не знакомы с синтаксисом `JOIN` или вам нужно немного захотят его использование, я рекомендую [учебник SQL JOIN](http://www.w3schools.com/sql/sql_join.asp) в [W3-школах](http://www.w3schools.com/). Также стоит ознакомиться с [`JOIN` фундаментальными](https://msdn.microsoft.com/library/ms191517.aspx) сведениями и [основными принципами вложенных запросов](https://msdn.microsoft.com/library/ms189575.aspx) [электронной документации по SQL](https://msdn.microsoft.com/library/ms130214.aspx).

Так как `JOIN` s и коррелированные вложенные запросы можно использовать для получения связанных данных из других таблиц, многие разработчики размещают свои заголовки и заинтересовали, какой подход использовать. Все эксперты по SQL, которые я написал, говорят примерно на то же самое, что это не имеет смысла в плане производительности, так как SQL Server выдает примерно одинаковые планы выполнения. Затем их советим, чтобы использовать методику, с которой вы и ваша команда знакомы. Это означает, что после устранения этого Совета эксперты сразу же выражают свои предпочтения `JOIN` s через коррелированные вложенные запросы.

При построении уровня доступа к данным с помощью типизированных наборов данных средства лучше работают при использовании вложенных запросов. В частности, мастер TableAdapter не будет автоматически формировать соответствующие инструкции `INSERT`, `UPDATE`и `DELETE`, если основной запрос содержит какие-либо `JOIN`, но автоматически создаст эти инструкции при использовании коррелированных вложенных запросов.

Чтобы исследовать этот недостаток, создайте временный типизированный набор данных в папке `~/App_Code/DAL`. В мастере настройки адаптера таблицы выберите использование специальных инструкций SQL и введите следующий `SELECT` запрос (см. рис. 1):

[!code-sql[Main](updating-the-tableadapter-to-use-joins-cs/samples/sample3.sql)]

[![введите основной запрос, содержащий объединения](updating-the-tableadapter-to-use-joins-cs/_static/image2.png)](updating-the-tableadapter-to-use-joins-cs/_static/image1.png)

**Рис. 1**. ввод основного запроса, содержащего `JOIN` s ([щелкните, чтобы просмотреть изображение с полным размером](updating-the-tableadapter-to-use-joins-cs/_static/image3.png))

По умолчанию TableAdapter автоматически создает инструкции `INSERT`, `UPDATE`и `DELETE` на основе основного запроса. Если нажать кнопку "Дополнительно", можно увидеть, что эта функция включена. Несмотря на этот параметр, TableAdapter не сможет создать `INSERT`, `UPDATE`и инструкции `DELETE`, так как главный запрос содержит `JOIN`.

![Введите основной запрос, содержащий объединения](updating-the-tableadapter-to-use-joins-cs/_static/image4.png)

**Рис. 2**. ввод основного запроса, содержащего `JOIN` s

Нажмите кнопку Готово, чтобы завершить работу с мастером. На этом этапе конструктор наборов данных будет включать один TableAdapter с таблицей DataTable со столбцами для каждого из полей, возвращаемых в списке столбцов `SELECT` запроса. К ним относятся `CategoryName` и `SupplierName`, как показано на рис. 3.

![Таблица данных содержит столбец для каждого поля, возвращенного в списке столбцов.](updating-the-tableadapter-to-use-joins-cs/_static/image5.png)

**Рис. 3**. Таблица данных содержит столбец для каждого поля, возвращенного в списке столбцов.

Хотя таблица данных содержит соответствующие столбцы, в TableAdapter отсутствуют значения свойств `InsertCommand`, `UpdateCommand`и `DeleteCommand`. Чтобы подтвердить это, щелкните TableAdapter в конструкторе и перейдите к окно свойств. Вы увидите, что свойства `InsertCommand`, `UpdateCommand`и `DeleteCommand` установлены в значение (нет).

[![свойствах InsertCommand, UpdateCommand и DeleteCommand установлены в значение (нет)](updating-the-tableadapter-to-use-joins-cs/_static/image7.png)](updating-the-tableadapter-to-use-joins-cs/_static/image6.png)

**Рис. 4**. свойства `InsertCommand`, `UpdateCommand`и `DeleteCommand` имеют значение (нет) ([щелкните, чтобы просмотреть изображение с полным размером](updating-the-tableadapter-to-use-joins-cs/_static/image8.png))

Чтобы обойти этот недостаток, можно вручную предоставить инструкции и параметры SQL для свойств `InsertCommand`, `UpdateCommand`и `DeleteCommand` через окно свойств. Кроме того, можно начать с настройки основного запроса TableAdapter s, чтобы он *не* включал никаких `JOIN`. Это позволит автоматически создавать инструкции `INSERT`, `UPDATE`и `DELETE` для нас. После завершения работы мастера можно вручную обновить `SelectCommand` TableAdapter с окно свойств, чтобы он включал синтаксис `JOIN`.

Хотя этот подход работает, очень нестабильным при использовании нерегламентированных запросов SQL, так как каждый раз, когда основной запрос TableAdapter s перестраивается с помощью мастера, автоматически создаваемые инструкции `INSERT`, `UPDATE`и `DELETE` создаются повторно. Это означает, что все настройки, которые будут внесены позже, будут потеряны, если щелкнуть правой кнопкой мыши TableAdapter, выбрать пункт настроить в контекстном меню и снова завершить работу мастера.

Хрупкости автоматически создаваемых инструкций `INSERT`, `UPDATE`и `DELETE` TableAdapter, к счастью, ограничены непрямыми инструкциями SQL. Если TableAdapter использует хранимые процедуры, можно настроить `SelectCommand`, `InsertCommand`, `UpdateCommand`или `DeleteCommand` хранимых процедур, а также повторно запустить мастер настройки TableAdapter, не опасаясь, что хранимые процедуры будут изменены.

В следующих нескольких шагах мы создадим TableAdapter, который, изначально, использует основной запрос, исключающий `JOIN` s, чтобы соответствующие хранимые процедуры INSERT, Update и DELETE были созданы автоматически. Затем мы будем обновлять `SelectCommand` так, чтобы использовать `JOIN`, возвращающий дополнительные столбцы из связанных таблиц. Наконец, мы создадим соответствующий класс уровня бизнес-логики и продемонстрируем использование адаптера таблицы на веб-странице ASP.NET.

## <a name="step-1-creating-the-tableadapter-using-a-simplified-main-query"></a>Шаг 1. Создание адаптера таблицы с помощью упрощенного основного запроса

В этом учебнике мы добавим TableAdapter и строго типизированную таблицу DataTable для таблицы `Employees` в `NorthwindWithSprocs`ном наборе данных. Таблица `Employees` содержит поле `ReportsTo`, в котором указано `EmployeeID` менеджера Employee Manager. Например, сотрудник Anne Белов имеет значение `ReportTo` 5, которое является `EmployeeID` Стивен Батурин. Следовательно, Anne сообщает Стивен и его начальнику. Вместе с отчетами `ReportsTo` значения каждого сотрудника также может потребоваться получить имя своего руководителя. Это можно сделать с помощью `JOIN`. Но использование `JOIN` при первоначальном создании TableAdapter исключает возможность автоматического создания соответствующих возможностей вставки, обновления и удаления с помощью мастера. Поэтому начнем с создания адаптера таблицы TableAdapter, основной запрос которого не содержит `JOIN` s. Затем на шаге 2 мы будем обновлять основную хранимую процедуру запроса для получения имени руководителя с помощью `JOIN`.

Сначала откройте набор данных `NorthwindWithSprocs` в папке `~/App_Code/DAL`. Щелкните правой кнопкой мыши конструктор, выберите пункт Добавить в контекстном меню и выберите пункт меню TableAdapter. Запустится мастер настройки адаптера таблицы. Как показано на рис. 5, мастер создает новые хранимые процедуры и нажимайте кнопку Далее. Сведения о создании новых хранимых процедур с помощью мастера адаптеров таблиц см. в руководстве по [созданию новых хранимых процедур для объектов TableAdapter с типизированным набором данных](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs.md) .

[![выберите параметр создать новые хранимые процедуры.](updating-the-tableadapter-to-use-joins-cs/_static/image10.png)](updating-the-tableadapter-to-use-joins-cs/_static/image9.png)

**Рис. 5**. Выбор параметра "создать новые хранимые процедуры" ([щелкните, чтобы просмотреть изображение с полным размером](updating-the-tableadapter-to-use-joins-cs/_static/image11.png))

Используйте следующую инструкцию `SELECT` для основного запроса TableAdapter s:

[!code-sql[Main](updating-the-tableadapter-to-use-joins-cs/samples/sample4.sql)]

Поскольку этот запрос не включает `JOIN` s, мастер TableAdapter автоматически создает хранимые процедуры с соответствующими инструкциями `INSERT`, `UPDATE`и `DELETE`, а также хранимую процедуру для выполнения основного запроса.

На следующем шаге мы наименовать хранимые процедуры TableAdapter s. Используйте имена `Employees_Select`, `Employees_Insert`, `Employees_Update`и `Employees_Delete`, как показано на рис. 6.

[![имя хранимых процедур TableAdapter s](updating-the-tableadapter-to-use-joins-cs/_static/image13.png)](updating-the-tableadapter-to-use-joins-cs/_static/image12.png)

**Рис. 6**. Именование хранимых процедур TableAdapter ([щелкните, чтобы просмотреть изображение с полным размером](updating-the-tableadapter-to-use-joins-cs/_static/image14.png))

На последнем шаге мы предложим указать имя для методов TableAdapter s. Используйте `Fill` и `GetEmployees` в качестве имен методов. Также убедитесь, что установлен флажок создать методы для отправки обновлений непосредственно в базу данных (GenerateDBDirectMethods).

[![имя методы адаптера таблицы TableAdapter Fill и Employees](updating-the-tableadapter-to-use-joins-cs/_static/image16.png)](updating-the-tableadapter-to-use-joins-cs/_static/image15.png)

**Рис. 7**. Именование методов TableAdapter `Fill` и `GetEmployees` ([щелкните, чтобы просмотреть изображение с полным размером](updating-the-tableadapter-to-use-joins-cs/_static/image17.png))

После завершения работы мастера ознакомьтесь с хранимыми процедурами в базе данных. Вы должны увидеть четыре новых: `Employees_Select`, `Employees_Insert`, `Employees_Update`и `Employees_Delete`. Затем проверьте только что созданный `EmployeesDataTable` и `EmployeesTableAdapter`. Объект DataTable содержит столбец для каждого поля, возвращенного основным запросом. Щелкните TableAdapter и перейдите к окно свойств. Вы увидите, что свойства `InsertCommand`, `UpdateCommand`и `DeleteCommand` правильно настроены для вызова соответствующих хранимых процедур.

[![TableAdapter включает возможности вставки, обновления и удаления](updating-the-tableadapter-to-use-joins-cs/_static/image19.png)](updating-the-tableadapter-to-use-joins-cs/_static/image18.png)

**Рис. 8**. Таблица TableAdapter включает возможности вставки, обновления и удаления ([щелкните, чтобы просмотреть изображение с полным размером](updating-the-tableadapter-to-use-joins-cs/_static/image20.png))

После того как автоматически созданы хранимые процедуры INSERT, Update и DELETE, а также правильно настроены свойства `InsertCommand`, `UpdateCommand`и `DeleteCommand`, мы готовы к настройке хранимой процедуры `SelectCommand` s для получения дополнительных сведений о каждом менеджере Employee s. В частности, необходимо обновить хранимую процедуру `Employees_Select`, чтобы она использовала `JOIN` и возвращала диспетчер s `FirstName` и `LastName` значения. После обновления хранимой процедуры необходимо будет обновить таблицу данных, чтобы она включала эти дополнительные столбцы. Мы рассмотрим эти две задачи в шагах 2 и 3.

## <a name="step-2-customizing-the-stored-procedure-to-include-ajoin"></a>Шаг 2. Настройка хранимой процедуры для включения`JOIN`

Начните с перехода к обозреватель сервера, перейдите в папку Хранимые процедуры базы данных Northwind и откройте хранимую процедуру `Employees_Select`. Если эта хранимая процедура не отображается, щелкните правой кнопкой мыши папку Хранимые процедуры и выберите команду Обновить. Обновите хранимую процедуру таким образом, чтобы она использовала `LEFT JOIN` для возвращения имени и фамилии руководителя:

[!code-sql[Main](updating-the-tableadapter-to-use-joins-cs/samples/sample5.sql)]

После обновления инструкции `SELECT` сохраните изменения, выбрав в меню Файл пункт Сохранить `Employees_Select`. Кроме того, можно щелкнуть значок сохранить на панели инструментов или нажать клавиши CTRL + S. После сохранения изменений щелкните правой кнопкой мыши хранимую процедуру `Employees_Select` в обозреватель сервера и выберите команду выполнить. Это приведет к запуску хранимой процедуры и отображению ее результатов в окне вывода (см. рис. 9).

[![результаты хранимых процедур отображаются в окно вывода](updating-the-tableadapter-to-use-joins-cs/_static/image22.png)](updating-the-tableadapter-to-use-joins-cs/_static/image21.png)

**Рис. 9**. Результаты хранимых процедур отображаются в окно вывода ([щелкните, чтобы просмотреть изображение с полным размером](updating-the-tableadapter-to-use-joins-cs/_static/image23.png))

## <a name="step-3-updating-the-datatable-s-columns"></a>Шаг 3. Обновление столбцов DataTable s

На этом этапе хранимая процедура `Employees_Select` возвращает значения `ManagerFirstName` и `ManagerLastName`, но в `EmployeesDataTable` отсутствуют эти столбцы. Эти отсутствующие столбцы можно добавить в таблицу данных одним из двух способов:

- **Вручную** щелкните правой кнопкой мыши таблицу данных в конструкторе DataSet и в меню "Добавить" выберите столбец. Затем можно присвоить имя столбцу и задать его свойства соответствующим образом.
- **Автоматически** . Мастер настройки адаптера таблицы обновит столбцы DataTable s, чтобы отразить поля, возвращаемые хранимой процедурой `SelectCommand`. При использовании специальных инструкций SQL мастер также удалит свойства `InsertCommand`, `UpdateCommand`и `DeleteCommand`, так как `SelectCommand` теперь содержит `JOIN`. Но при использовании хранимых процедур эти свойства команды остаются без изменений.

Мы подробно изучили Добавление столбцов таблицы данных в предыдущие руководства, включая [«основной/подробности», используя маркированный список основных записей с элементом управления DataList](../filtering-scenarios-with-the-datalist-and-repeater/master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs.md) и [отправкой файлов](../working-with-binary-files/uploading-files-cs.md), и мы подробно рассмотрим этот процесс в следующем учебном курсе. Однако в этом руководстве мы будем использовать автоматический подход с помощью мастера настройки TableAdapter.

Для начала щелкните правой кнопкой мыши `EmployeesTableAdapter` и выберите в контекстном меню пункт Настроить. Откроется мастер настройки TableAdapter, в котором перечислены хранимые процедуры, используемые для выбора, вставки, обновления и удаления, а также возвращаемые значения и параметры (если они есть). Этот мастер показан на рис. 10. Здесь можно увидеть, что `Employees_Select` хранимая процедура теперь возвращает поля `ManagerFirstName` и `ManagerLastName`.

[![мастер отображает список обновленных столбцов для хранимой процедуры Employees_Select](updating-the-tableadapter-to-use-joins-cs/_static/image25.png)](updating-the-tableadapter-to-use-joins-cs/_static/image24.png)

**Рис. 10**. в мастере отображается список обновленных столбцов для `Employees_Select` хранимой процедуры ([щелкните, чтобы просмотреть изображение с полным размером](updating-the-tableadapter-to-use-joins-cs/_static/image26.png))

Завершите работу мастера, нажав кнопку Готово. При возврате к конструктору наборов данных `EmployeesDataTable` включает два дополнительных столбца: `ManagerFirstName` и `ManagerLastName`.

[![Емплойисдататабле содержит два новых столбца](updating-the-tableadapter-to-use-joins-cs/_static/image28.png)](updating-the-tableadapter-to-use-joins-cs/_static/image27.png)

**Рис. 11**. `EmployeesDataTable` содержит два новых столбца ([щелкните, чтобы просмотреть изображение с полным размером](updating-the-tableadapter-to-use-joins-cs/_static/image29.png))

Чтобы продемонстрировать, что обновленная хранимая процедура `Employees_Select` действует и возможности вставки, обновления и удаления TableAdapter по-прежнему работают, давайте создадим веб-страницу, позволяющую пользователям просматривать и удалять сотрудников. Однако перед созданием такой страницы необходимо сначала создать новый класс на уровне бизнес-логики для работы с сотрудниками из набора данных `NorthwindWithSprocs`. На шаге 4 мы создадим класс `EmployeesBLLWithSprocs`. На шаге 5 этот класс будет использоваться на странице ASP.NET.

## <a name="step-4-implementing-the-business-logic-layer"></a>Шаг 4. реализация уровня бизнес-логики

Создайте новый файл класса в папке `~/App_Code/BLL` с именем `EmployeesBLLWithSprocs.cs`. Этот класс имитирует семантику существующего класса `EmployeesBLL`, только этот новый класс предоставляет меньше методов и использует `NorthwindWithSprocs`ный набор данных (вместо набора данных `Northwind`). Добавьте в класс `EmployeesBLLWithSprocs` приведенный далее код.

[!code-csharp[Main](updating-the-tableadapter-to-use-joins-cs/samples/sample6.cs)]

Свойство `Adapter` `EmployeesBLLWithSprocs` классов возвращает экземпляр `NorthwindWithSprocs` набора данных `EmployeesTableAdapter`. Этот метод используется классами `GetEmployees` и `DeleteEmployee`. Метод `GetEmployees` вызывает метод `EmployeesTableAdapter` s, соответствующий `GetEmployees`, который вызывает хранимую процедуру `Employees_Select` и заполняет ее результаты в `EmployeeDataTable`. Метод `DeleteEmployee` аналогичным образом вызывает метод `EmployeesTableAdapter` s `Delete`, который вызывает хранимую процедуру `Employees_Delete`.

## <a name="step-5-working-with-the-data-in-the-presentation-layer"></a>Шаг 5. Работа с данными на уровне представления данных

После завершения работы с классом `EmployeesBLLWithSprocs` мы уже готовы к работе с данными о сотрудниках через страницу ASP.NET. Откройте страницу `JOINs.aspx` в папке `AdvancedDAL` и перетащите элемент управления GridView с панели инструментов в конструктор, установив для свойства `ID` значение `Employees`. Затем в смарт-теге GridView s свяжите сетку с новым элементом управления ObjectDataSource с именем `EmployeesDataSource`.

Настройте ObjectDataSource для использования класса `EmployeesBLLWithSprocs` и на вкладках выбор и удаление убедитесь, что в раскрывающихся списках выбраны методы `GetEmployees` и `DeleteEmployee`. Нажмите кнопку Готово, чтобы завершить настройку ObjectDataSource s.

[![настроить ObjectDataSource для использования класса Емплойисбллвисспрокс](updating-the-tableadapter-to-use-joins-cs/_static/image31.png)](updating-the-tableadapter-to-use-joins-cs/_static/image30.png)

**Рис. 12**. Настройка ObjectDataSource для использования класса `EmployeesBLLWithSprocs` ([щелкните, чтобы просмотреть изображение с полным размером](updating-the-tableadapter-to-use-joins-cs/_static/image32.png))

[![, что ObjectDataSource использует методы «Делетимплойи» и «сотрудники»](updating-the-tableadapter-to-use-joins-cs/_static/image34.png)](updating-the-tableadapter-to-use-joins-cs/_static/image33.png)

**Рис. 13**. элемент ObjectDataSource должен использовать методы `GetEmployees` и `DeleteEmployee` ([щелкните, чтобы просмотреть изображение с полным размером](updating-the-tableadapter-to-use-joins-cs/_static/image35.png))

Visual Studio добавит BoundField в GridView для каждого столбца `EmployeesDataTable` s. Удалите все эти BoundFields, за исключением `Title`, `LastName`, `FirstName`, `ManagerFirstName`и `ManagerLastName` и переименуйте свойства `HeaderText` для последних четырех BoundFields по фамилии, имени, имени руководителя и фамилии Manager s соответственно.

Чтобы разрешить пользователям удалять сотрудников с этой страницы, необходимо выполнить два действия. Во-первых, попросите GridView предоставить возможности удаления, установив флажок Разрешить удаление из своего интеллектуального тега. Во-вторых, измените свойство `OldValuesParameterFormatString` ObjectDataSource из значения, установленного мастером ObjectDataSource (`original_{0}`), на значение по умолчанию (`{0}`). После внесения этих изменений декларативная разметка GridView и ObjectDataSource должна выглядеть следующим образом:

[!code-aspx[Main](updating-the-tableadapter-to-use-joins-cs/samples/sample7.aspx)]

Протестируйте страницу, посетив ее через браузер. Как показано на рис. 14, на странице будет отображаться название каждого сотрудника и его имя руководителя (при условии, что у них есть одно из них).

[![соединение в хранимой процедуре Employees_Select возвращает имя руководителя](updating-the-tableadapter-to-use-joins-cs/_static/image37.png)](updating-the-tableadapter-to-use-joins-cs/_static/image36.png)

**Рис. 14**. `JOIN` в хранимой процедуре `Employees_Select` возвращает имя менеджера ([щелкните, чтобы просмотреть изображение с полным размером](updating-the-tableadapter-to-use-joins-cs/_static/image38.png)).

При нажатии кнопки удалить запускается рабочий процесс удаления, итогом при `Employees_Delete` выполнении хранимой процедуры. Однако попытка выполнить инструкцию `DELETE` в хранимой процедуре завершается неудачей из-за нарушения ограничения внешнего ключа (см. рис. 15). В частности, каждый сотрудник имеет одну или несколько записей в `Orders` таблице, что приводит к сбою удаления.

[![Удаление сотрудника, имеющего соответствующие заказы, приводит к нарушению ограничения внешнего ключа.](updating-the-tableadapter-to-use-joins-cs/_static/image40.png)](updating-the-tableadapter-to-use-joins-cs/_static/image39.png)

**Рис. 15**. Удаление сотрудника, имеющего соответствующие заказы, приводит к нарушению ограничения внешнего ключа ([щелкните, чтобы просмотреть изображение с полным размером](updating-the-tableadapter-to-use-joins-cs/_static/image41.png))

Чтобы разрешить удаление сотрудника, можно:

- Обновите ограничение внешнего ключа для каскадных удалений,
- Вручную удалите записи из таблицы `Orders` для сотрудников, которые требуется удалить, или
- Обновите `Employees_Delete` хранимую процедуру, чтобы сначала удалить связанные записи из `Orders` таблицы перед удалением записи `Employees`. Мы обсуждали этот прием в учебнике [использование существующих хранимых процедур для адаптеров таблиц типизированного набора данных s](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs.md) .

Я оставлю это в качестве упражнения для читателя.

## <a name="summary"></a>Сводка

При работе с реляционными базами данных часто запросы извлекают свои данные из нескольких связанных таблиц. Коррелированные вложенные запросы и `JOIN` s предоставляют два различных метода доступа к данным из связанных таблиц в запросе. В предыдущих учебных курсах мы чаще всего использовали коррелированные вложенные запросы, так как TableAdapter не может автоматически создавать `INSERT`, `UPDATE`и операторы `DELETE` для запросов, включающих `JOIN` s. Хотя эти значения могут быть предоставлены вручную, при использовании специальных инструкций SQL любые настройки будут перезаписаны после завершения работы мастера настройки TableAdapter.

К счастью, адаптеры таблиц, созданные с помощью хранимых процедур, не пострадает от тех же хрупкости, которые были созданы с помощью специальных инструкций SQL. Таким образом, можно создать TableAdapter, основной запрос которого использует `JOIN` при использовании хранимых процедур. В этом учебнике мы увидели, как создать такой адаптер таблицы. Мы начали с помощью запроса к основному адаптеру TableAdapter s `JOIN``SELECT`, чтобы соответствующие хранимые процедуры вставки, обновления и удаления создавались бы в автоматическом виде. После завершения начальной настройки адаптера таблицы TableAdapter мы дополнены хранимой процедурой `SelectCommand` для использования `JOIN` и повторного запуска мастера настройки TableAdapter для обновления столбцов `EmployeesDataTable` s.

Повторное выполнение мастера настройки TableAdapter автоматически обновил `EmployeesDataTable` столбцы, чтобы они отражали поля данных, возвращаемые хранимой процедурой `Employees_Select`. Кроме того, можно вручную добавить эти столбцы в таблицу DataTable. В следующем руководстве мы рассмотрим добавление столбцов в таблицу данных вручную.

Поздравляем с программированием!

## <a name="about-the-author"></a>Об авторе

[Скотт Митчелл](http://www.4guysfromrolla.com/ScottMitchell.shtml), автор семи книг по ASP/ASP. NET и основатель [4GuysFromRolla.com](http://www.4guysfromrolla.com), работал с веб-технологиями Майкрософт с 1998. Скотт работает как независимый консультант, преподаватель и модуль записи. Его последняя книга — [*Sams обучать себя ASP.NET 2,0 за 24 часа*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco). Он доступен по адресу [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) или через его блог, который можно найти по адресу [http://ScottOnWriting.NET](http://ScottOnWriting.NET).

## <a name="special-thanks-to"></a>Специальная благодарность

Эта серия руководств была рассмотрена многими полезными рецензентами. Потенциальные рецензенты для этого учебника были Хилтон Жеисенов, Дэвид суру и Терезой Мерфи. Хотите ознакомиться с моими будущими статьями MSDN? Если это так, расположите строку в [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Назад](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs.md)
> [Вперед](adding-additional-datatable-columns-cs.md)
