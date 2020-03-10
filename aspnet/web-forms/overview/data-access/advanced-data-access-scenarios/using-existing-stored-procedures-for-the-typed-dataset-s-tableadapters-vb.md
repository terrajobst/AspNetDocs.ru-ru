---
uid: web-forms/overview/data-access/advanced-data-access-scenarios/using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb
title: Использование существующих хранимых процедур для адаптеров таблиц TableAdapter типизированного набора данных (VB) | Документация Майкрософт
author: rick-anderson
description: В предыдущем учебном курсе мы узнали, как использовать мастер TableAdapter для создания новых хранимых процедур. В этом учебнике мы рассмотрим, как один и тот же адаптер TableAdapter...
ms.author: riande
ms.date: 07/18/2007
ms.assetid: 2da25f6a-757e-4e7b-a812-1575288d8f7a
msc.legacyurl: /web-forms/overview/data-access/advanced-data-access-scenarios/using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb
msc.type: authoredcontent
ms.openlocfilehash: e35c3d6a98516a07f6119e6cb9dbeb99bc28fe33
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78427128"
---
# <a name="using-existing-stored-procedures-for-the-typed-datasets-tableadapters-vb"></a>Использование существующих хранимых процедур для адаптеров таблиц TableAdapter типизированного DataSet (VB)

по [Скотт Митчелл](https://twitter.com/ScottOnWriting)

[Скачать код](https://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_68_VB.zip) или [скачать PDF](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/datatutorial68vb1.pdf)

> В предыдущем учебном курсе мы узнали, как использовать мастер TableAdapter для создания новых хранимых процедур. В этом учебнике мы рассмотрим, как мастер TableAdapter может работать с существующими хранимыми процедурами. Мы также научитесь вручную добавлять новые хранимые процедуры в нашу базу данных.

## <a name="introduction"></a>Введение

В [предыдущем учебном курсе](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb.md) мы увидели, как адаптеры таблиц типизированного набора данных могут быть настроены для использования хранимых процедур для доступа к данным, а не к специальным инструкциям SQL. В частности, мы рассмотрели, как мастер TableAdapter автоматически создает эти хранимые процедуры. При переносе устаревшего приложения на ASP.NET 2,0 или при создании веб-сайта ASP.NET 2,0 на основе существующей модели данных, вероятно, что база данных уже содержит нужные вам хранимые процедуры. Кроме того, можно создать хранимые процедуры вручную или с помощью какого-либо средства, отличного от мастера TableAdapter, который создает хранимые процедуры.

В этом учебнике мы рассмотрим, как настроить TableAdapter для использования существующих хранимых процедур. Поскольку база данных Northwind содержит только небольшой набор встроенных хранимых процедур, мы также рассмотрим шаги, необходимые для ручного добавления новых хранимых процедур в базу данных в среде Visual Studio. Давайте приступим к работе!

> [!NOTE]
> В процессе [переноса изменений базы данных в рамках руководства по транзакциям](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb.md) мы добавили методы в TableAdapter для поддержки транзакций (`BeginTransaction`, `CommitTransaction`и т. д.). Кроме того, транзакции могут полностью управляться внутри хранимой процедуры, что не требует внесения изменений в код уровня доступа к данным. В этом учебнике мы рассмотрим команды T-SQL, используемые для выполнения инструкций хранимых процедур в области действия транзакции.

## <a name="step-1-adding-stored-procedures-to-the-northwind-database"></a>Шаг 1. Добавление хранимых процедур в базу данных Northwind

Visual Studio упрощает добавление новых хранимых процедур в базу данных. Добавим новую хранимую процедуру в базу данных Northwind, которая возвращает все столбцы из таблицы `Products` для тех, которые имеют определенное значение `CategoryID`. В окне обозреватель сервера разверните базу данных Northwind, чтобы отображались ее папки — диаграммы базы данных, таблицы, представления и т. д. Как было показано в предыдущем руководстве, папка хранимые процедуры содержит существующие хранимые процедуры базы данных. Чтобы добавить новую хранимую процедуру, просто щелкните правой кнопкой мыши папку Хранимые процедуры и выберите в контекстном меню пункт Добавить новую хранимую процедуру.

[![щелкните правой кнопкой мыши папку Хранимые процедуры и добавьте новую хранимую процедуру.](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image2.png)](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image1.png)

**Рис. 1**. Щелкните правой кнопкой мыши папку Хранимые процедуры и добавьте новую хранимую процедуру ([щелкните, чтобы просмотреть изображение с полным размером](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image3.png)).

Как показано на рис. 1, при выборе параметра Добавить новую хранимую процедуру в Visual Studio открывается окно скрипта с описанием скрипта SQL, необходимого для создания хранимой процедуры. Мы обработаем этот сценарий и выполняем его, после чего хранимая процедура будет добавлена в базу данных.

Введите следующий скрипт:

[!code-sql[Main](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/samples/sample1.sql)]

При выполнении этот сценарий добавляет новую хранимую процедуру в базу данных Northwind с именем `Products_SelectByCategoryID`. Эта хранимая процедура принимает один входной параметр (`@CategoryID`, типа `int`) и возвращает все поля для этих продуктов с соответствующим значением `CategoryID`.

Чтобы выполнить этот `CREATE PROCEDURE` сценарий и добавить хранимую процедуру в базу данных, щелкните значок сохранить на панели инструментов или нажмите клавиши CTRL + S. После этого папка хранимых процедур обновится, отображая созданную хранимую процедуру. Кроме того, скрипт в окне изменит тонкость с `CREATE PROCEDURE dbo.Products_SelectProductByCategoryID` на `ALTER PROCEDURE` `dbo.Products_SelectProductByCategoryID`. `CREATE PROCEDURE` добавляет в базу данных новую хранимую процедуру, а `ALTER PROCEDURE` обновляет существующую. Так как начало скрипта изменилось на `ALTER PROCEDURE`, изменение входных параметров хранимых процедур или инструкций SQL и нажатие значка Сохранить приведет к обновлению хранимой процедуры этими изменениями.

На рис. 2 показана Visual Studio после сохранения `Products_SelectByCategoryID` хранимой процедуры.

[![Products_SelectByCategoryID в базу данных добавлена хранимая процедура](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image5.png)](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image4.png)

**Рис. 2**. хранимая процедура `Products_SelectByCategoryID` добавлена в базу данных ([щелкните, чтобы просмотреть изображение с полным размером](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image6.png))

## <a name="step-2-configuring-the-tableadapter-to-use-an-existing-stored-procedure"></a>Шаг 2. Настройка адаптера таблицы для использования существующей хранимой процедуры

Теперь, когда в базу данных была добавлена `Products_SelectByCategoryID` хранимая процедура, мы можем настроить уровень доступа к данным, чтобы использовать эту хранимую процедуру при вызове одного из ее методов. В частности, мы добавим метод `GetProductsByCategoryID(<_i22_>categoryID)<!--_i22_-->` в `ProductsTableAdapter` в `NorthwindWithSprocs` типизированном наборе данных, который вызывает только что созданную хранимую процедуру `Products_SelectByCategoryID`.

Для начала откройте набор данных `NorthwindWithSprocs`. Щелкните правой кнопкой мыши `ProductsTableAdapter` и выберите команду Добавить запрос, чтобы запустить мастер настройки запроса адаптера таблицы. В [предыдущем учебном курсе](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb.md) мы решили, что TableAdapter создает новую хранимую процедуру для нас. Однако в этом руководстве мы хотим связать новый метод TableAdapter с существующей `Products_SelectByCategoryID` хранимой процедурой. Поэтому выберите параметр использовать существующую хранимую процедуру на первом шаге мастера, а затем нажмите кнопку Далее.

[![выберите параметр использовать существующую хранимую процедуру.](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image8.png)](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image7.png)

**Рис. 3**. Выбор параметра "использовать существующую хранимую процедуру" ([щелкните, чтобы просмотреть изображение с полным размером](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image9.png))

На следующем экране представлен раскрывающийся список, заполненный хранимыми процедурами базы данных. При выборе хранимой процедуры выводится список входных параметров слева и поля данных, которые были возвращены (если имеются) справа. Выберите `Products_SelectByCategoryID` хранимую процедуру из списка и нажмите кнопку Далее.

[![выбрать Products_SelectByCategoryID хранимую процедуру](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image11.png)](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image10.png)

**Рис. 4**. Выбор хранимой процедуры `Products_SelectByCategoryID` ([щелкните, чтобы просмотреть изображение с полным размером](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image12.png))

На следующем экране запрашивается, какие данные возвращаются хранимой процедурой, и наш ответ определяет тип, возвращаемый методом TableAdapter s. Например, если указать, что табличные данные возвращаются, метод возвратит `ProductsDataTable` экземпляр, заполненный записями, возвращаемыми хранимой процедурой. Напротив, если бы мы указывали, что эта хранимая процедура возвращает единственное значение, TableAdapter возвратит `Object`, которому присваивается значение в первом столбце первой записи, возвращенной хранимой процедурой.

Так как хранимая процедура `Products_SelectByCategoryID` возвращает все продукты, относящиеся к определенной категории, выберите первый ответ — табличные данные, а затем нажмите кнопку Далее.

[![указать, что хранимая процедура возвращает табличные данные](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image14.png)](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image13.png)

**Рис. 5**. Указание того, что хранимая процедура возвращает табличные данные ([щелкните, чтобы просмотреть изображение с полным размером](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image15.png))

Остается только указать, какие шаблоны методов следует использовать, за которыми следуют имена этих методов. Оставьте как заполненную таблицу данных, так и возвращаемые параметры DataTable, но переименуйте методы в `FillByCategoryID` и `GetProductsByCategoryID`. Затем нажмите кнопку Далее, чтобы ознакомиться с краткими сведениями о задачах, которые будут выполнены мастером. Если все выглядит правильно, нажмите кнопку Готово.

[![назовите методы Филлбикатегорид и GetProductsByCategoryID.](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image17.png)](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image16.png)

**Рис. 6**. Именование методов `FillByCategoryID` и `GetProductsByCategoryID` ([щелкните, чтобы просмотреть изображение с полным размером](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image18.png))

> [!NOTE]
> Методы TableAdapter, которые мы только что создали, `FillByCategoryID` и `GetProductsByCategoryID`, должны иметь входной параметр типа `Integer`. Это значение входного параметра передается в хранимую процедуру через его параметр `@CategoryID`. При изменении параметров `Products_SelectByCategory` хранимых процедур s необходимо также обновить параметры для этих методов TableAdapter. Как обсуждалось в [предыдущем руководстве](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb.md), это можно сделать одним из двух способов: путем добавления или удаления параметров из коллекции Parameters вручную или путем повторного запуска мастера TableAdapter.

## <a name="step-3-adding-agetproductsbycategoryidcategoryidmethod-to-the-bll"></a>Шаг 3. добавление к BLL метода`GetProductsByCategoryID(categoryID)`

После завершения `GetProductsByCategoryID` метода DAL необходимо предоставить доступ к этому методу на уровне бизнес-логики. Откройте файл класса `ProductsBLLWithSprocs` и добавьте следующий метод:

[!code-vb[Main](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/samples/sample2.vb)]

Этот метод BLL просто возвращает `ProductsDataTable`, возвращенный методом `ProductsTableAdapter` s `GetProductsByCategoryID`. Атрибут `DataObjectMethodAttribute` предоставляет метаданные, используемые мастером настройки источников данных ObjectDataSource. В частности, этот метод будет отображаться в раскрывающемся списке SELECT Tab s (выбор вкладок).

## <a name="step-4-displaying-products-by-category"></a>Шаг 4. Отображение продуктов по категориям

Чтобы протестировать вновь добавленную `Products_SelectByCategoryID` хранимую процедуру и соответствующие методы DAL и BLL, давайте создадим страницу ASP.NET, содержащую DropDownList и GridView. В элементе управления DropDownList будут перечислены все категории в базе данных, а в элементе управления GridView будут отображаться продукты, принадлежащие выбранной категории.

> [!NOTE]
> Мы создали интерфейсы "основной/подробности" с помощью элементов управления DropDownList в предыдущих руководствах. Более подробные сведения о реализации такого отчета «основной/подробности» см. в разделе [Фильтрация "основной/подробности" с помощью DropDownList](../masterdetail/master-detail-filtering-with-a-dropdownlist-vb.md) .

Откройте страницу `ExistingSprocs.aspx` в папке `AdvancedDAL` и перетащите DropDownList из области элементов в конструктор. Установите для свойства DropDownList `ID` значение `Categories`, а для свойства `AutoPostBack` значение `True`. Затем из своего смарт-тега привяжите DropDownList к новому ObjectDataSource с именем `CategoriesDataSource`. Настройте ObjectDataSource таким образом, чтобы он получал свои данные из метода `CategoriesBLL` класса s `GetCategories`. Установите в раскрывающихся списках на вкладках обновления, вставки и удаления значение (нет).

[![получить данные из метода CategoriesBLL класса s](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image20.png)](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image19.png)

**Рис. 7**. Извлечение данных из метода `GetCategories` `CategoriesBLL` классов ([щелкните, чтобы просмотреть изображение с полным размером](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image21.png))

[![установить в раскрывающихся списках на вкладках обновления, вставки и удаления значение (нет)](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image23.png)](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image22.png)

**Рис. 8**. Установка в раскрывающихся списках на вкладках «обновление», «вставка» и «удаление» (нет) ([щелкните, чтобы просмотреть изображение с полным размером](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image24.png))

После завершения работы мастера ObjectDataSource настройте в DropDownList отображение поля данных `CategoryName` и используйте поле `CategoryID` в качестве `Value` для каждого `ListItem`.

На этом этапе декларативная разметка DropDownList и ObjectDataSource должна выглядеть следующим образом:

[!code-aspx[Main](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/samples/sample3.aspx)]

Затем перетащите элемент управления GridView на конструктор, поместив его под элементом управления DropDownList. Установите `ID` GridView s `ProductsByCategory` и, из своего смарт-тега, привяжите его к новому ObjectDataSource с именем `ProductsByCategoryDataSource`. Настройте `ProductsByCategoryDataSource` ObjectDataSource для использования класса `ProductsBLLWithSprocs`, получая данные с помощью метода `GetProductsByCategoryID(categoryID)`. Поскольку этот элемент GridView будет использоваться только для вывода данных, задайте для раскрывающихся списков на вкладках обновление, вставка и удаление значение (нет) и нажмите кнопку Далее.

[![настроить ObjectDataSource для использования класса Продуктсбллвисспрокс](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image26.png)](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image25.png)

**Рис. 9**. Настройка ObjectDataSource для использования класса `ProductsBLLWithSprocs` ([щелкните, чтобы просмотреть изображение с полным размером](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image27.png))

[![получить данные из метода GetProductsByCategoryID (КодТипа)](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image29.png)](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image28.png)

**Рис. 10**. получение данных из метода `GetProductsByCategoryID(categoryID)` ([щелкните, чтобы просмотреть изображение с полным размером](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image30.png))

Метод, выбранный на вкладке SELECT, ожидает параметр, поэтому последний шаг мастера запрашивает у нас источник параметра s. Задайте в раскрывающемся списке Источник параметра значение Управление и выберите элемент управления `Categories` из раскрывающегося списка ControlID. Нажмите кнопку Готово, чтобы завершить работу с мастером.

[![использовать DropDownList категории в качестве источника параметра categoryID](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image32.png)](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image31.png)

**Рис. 11**. использование DropDownList `Categories` в качестве источника параметра `categoryID` ([щелкните, чтобы просмотреть изображение с полным размером](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image33.png))

После завершения работы мастера ObjectDataSource Visual Studio добавит BoundFields и CheckBoxField для каждого поля данных продукта. Вы можете настроить эти поля по своему усмотрению.

Откройте страницу в браузере. При посещении страницы выбирается Категория «напитки» и соответствующие продукты, перечисленные в сетке. Изменение раскрывающегося списка на альтернативную категорию, как показано на рис. 12, вызывает обратную передачу и перегружает сетку с продуктами новой выбранной категории.

[![отображаются продукты в категории создать.](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image35.png)](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image34.png)

**Рис. 12**. отображаются продукты в категории создать ([щелкните, чтобы просмотреть изображение с полным размером](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image36.png))

## <a name="step-5-wrapping-a-stored-procedure-s-statements-within-the-scope-of-a-transaction"></a>Шаг 5. заключение в оболочку хранимых процедур инструкций в области действия транзакции

В процессе [переноса изменений базы данных в рамках руководства по транзакциям](../working-with-batched-data/wrapping-database-modifications-within-a-transaction-vb.md) мы обсуждали методы выполнения ряда инструкций изменения базы данных в области транзакции. Помните, что изменения, выполненные под символом-отработкой транзакции, либо все успешно, либо все завершаются сбоем, что гарантирует атомарность. Ниже приведены методы использования транзакций.

- Использование классов в пространстве имен `System.Transactions`
- Уровень доступа к данным использует ADO.NET классы, такие как `SqlTransaction`, и
- Добавление команд транзакций T-SQL непосредственно в хранимую процедуру

В руководстве по *обработке изменений базы данных в рамках транзакции* используются классы ADO.NET в DAL. В оставшейся части этого руководства рассматривается управление транзакцией с помощью команд T-SQL в хранимой процедуре.

Три основные команды SQL для запуска, фиксации и отката транзакции вручную `BEGIN TRANSACTION`, `COMMIT TRANSACTION`и `ROLLBACK TRANSACTION`соответственно. Как и в случае с подходом ADO.NET, при использовании транзакций из хранимой процедуры необходимо применить следующий шаблон:

1. Указывает на начало транзакции.
2. Выполните инструкции SQL, составляющие транзакцию.
3. При возникновении ошибки в одной из инструкций, приведенных на шаге 2, необходимо выполнить откат транзакции.
4. Если все инструкции, выполненные на шаге 2, завершаются без ошибок, зафиксируйте транзакцию.

Этот шаблон можно реализовать в синтаксисе T-SQL, используя следующий шаблон:

[!code-sql[Main](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/samples/sample4.sql)]

Шаблон начинается с определения блока `TRY...CATCH`, новой — для SQL Server 2005. Как и в случае с блоками `Try...Catch` в Visual Basic, блок SQL `TRY...CATCH` выполняет инструкции в блоке `TRY`. Если какая-либо инструкция вызывает ошибку, управление немедленно передается в блок `CATCH`.

При отсутствии ошибок выполнения инструкций SQL, описывающего транзакцию, инструкция `COMMIT TRANSACTION` фиксирует изменения и завершает транзакцию. Однако если одна из инструкций приводит к ошибке, то `ROLLBACK TRANSACTION` в блоке `CATCH` возвращает базу данных в состояние до начала транзакции. Хранимая процедура также вызывает ошибку с помощью [команды RAISERROR](https://msdn.microsoft.com/library/ms178592.aspx), которая приводит к возникновению `SqlException` в приложении.

> [!NOTE]
> Так как блок `TRY...CATCH` является новым для SQL Server 2005, указанный выше шаблон не будет работать при использовании более ранних версий Microsoft SQL Server. Если вы не используете SQL Server 2005, обратитесь к [разделу Управление транзакциями в SQL Server хранимых процедурах](http://www.4guysfromrolla.com/webtech/080305-1.shtml) для шаблона, который будет работать с другими версиями SQL Server.

Давайте посмотрим на конкретный пример. Существует ограничение внешнего ключа между таблицами `Categories` и `Products`, то есть каждое поле `CategoryID` в таблице `Products` должно сопоставляться со значением `CategoryID` в таблице `Categories`. Любое действие, нарушающее это ограничение, например попытку удалить категорию с соответствующими продуктами, приводит к нарушению ограничения внешнего ключа. Чтобы проверить это, вернитесь к примеру "обновление и удаление существующих двоичных данных" в разделе "работа с двоичными данными" (`~/BinaryData/UpdatingAndDeleting.aspx`). На этой странице перечислены все категории в системе, а также кнопки "Изменить" и "Удалить" (см. рис. 13), но при попытке удалить категорию с соответствующими продуктами (например, напитки) происходит сбой удаления из-за нарушения ограничения внешнего ключа (см. рис. 14).

[![каждая категория отображается в элементе управления GridView с кнопками "Изменить" и "Удалить"](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image38.png)](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image37.png)

**Рис. 13**. Каждая категория отображается в элементе управления GridView с кнопками "Изменить" и "Удалить" ([щелкните, чтобы просмотреть изображение с полным размером](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image39.png))

[![удалить категорию, имеющую существующие продукты, нельзя.](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image41.png)](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image40.png)

**Рис. 14**. невозможно удалить категорию, имеющую существующие продукты ([щелкните, чтобы просмотреть изображение с полным размером](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image42.png))

Но представьте, что мы хотим разрешить удаление категорий независимо от наличия связанных с ними продуктов. Если категория с продуктами должна быть удалена, представьте, что необходимо также удалить существующие продукты (хотя другой вариант — просто задать для его продуктов `CategoryID` значения `NULL`). Эту функцию можно реализовать с помощью правил Cascade в ограничении внешнего ключа. Кроме того, можно создать хранимую процедуру, которая принимает входной параметр `@CategoryID` и при вызове явно удаляет все связанные продукты, а затем указанную категорию.

Первая попыток в такой хранимой процедуре может выглядеть следующим образом:

[!code-sql[Main](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/samples/sample5.sql)]

Хотя это определенно удаляет связанные продукты и категории, оно не выполняется в рамках транзакции. Представьте себе, что существует еще какое-то ограничение внешнего ключа на `Categories`, которое запрещает удаление определенного значения `@CategoryID`. Проблема заключается в том, что в этом случае все продукты будут удалены перед попыткой удалить категорию. В итоге, для такой категории эта хранимая процедура удалит все свои продукты, пока Категория осталась, так как она все еще содержит связанные записи в какой-либо другой таблице.

Однако если хранимая процедура была заключена в область транзакции, то при удалении на `Categories`удаления из `Products`ной таблицы будет произведен откат. Следующий скрипт хранимой процедуры использует транзакцию для обеспечения атомарности между двумя операторами `DELETE`:

[!code-sql[Main](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/samples/sample6.sql)]

Потратьте время на добавление `Categories_Delete` хранимой процедуры в базу данных Northwind. Инструкции по добавлению хранимых процедур в базу данных см. на шаге 1.

## <a name="step-6-updating-thecategoriestableadapter"></a>Шаг 6. обновление`CategoriesTableAdapter`

Хотя мы добавили в базу данных хранимую процедуру `Categories_Delete`, DAL в настоящее время настроен на использование специальных инструкций SQL для выполнения удаления. Необходимо обновить `CategoriesTableAdapter` и указать, что вместо этого будет использоваться хранимая процедура `Categories_Delete`.

> [!NOTE]
> Ранее в этом учебнике мы работали с набором данных `NorthwindWithSprocs`. Однако этот набор данных содержит только одну сущность, `ProductsDataTable`, и нам нужно работать с категориями. Таким образом, в оставшейся части этого руководства, когда я расскажу о слое доступа к данным I m, ссылающемся на набор данных `Northwind`, тот, который был создан в учебнике [Создание уровня доступа к данным](../introduction/creating-a-data-access-layer-vb.md) .

Откройте набор данных Northwind, выберите `CategoriesTableAdapter`и перейдите к окно свойств. В окно свойств перечислены `InsertCommand`, `UpdateCommand`, `DeleteCommand`и `SelectCommand`, используемые TableAdapter, а также его имя и сведения о соединении. Разверните свойство `DeleteCommand`, чтобы просмотреть сведения о нем. Как показано на рис. 15, свойству `DeleteCommand` s `CommandType` присвоено значение Text, которое указывает, что он отправляет текст в свойстве `CommandText` в виде специального SQL-запроса.

![Выберите Категориестаблеадаптер в конструкторе, чтобы просмотреть его свойства в окне "Свойства".](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image43.png)

**Рис. 15**. Выбор `CategoriesTableAdapter` в конструкторе для просмотра его свойств в окне "Свойства"

Чтобы изменить эти параметры, выберите текст (DeleteCommand) в окно свойств и выберите (создать) в раскрывающемся списке. Это приведет к очистке параметров свойств `CommandText`, `CommandType`и `Parameters`. Затем задайте для свойства `CommandType` значение `StoredProcedure`, а затем введите имя хранимой процедуры для `CommandText` (`dbo.Categories_Delete`). Если вы обязательно вводите свойства в этом порядке, сначала `CommandType`, а затем `CommandText` — Visual Studio автоматически заполнит коллекцию Parameters. Если эти свойства не вводятся в указанном порядке, необходимо вручную добавить параметры с помощью редактора коллекции параметров. В любом случае лучше щелкнуть многоточие в свойстве Parameters, чтобы открыть редактор коллекции параметров, чтобы убедиться в том, что были внесены правильные настройки параметров (см. рис. 16). Если в диалоговом окне Параметры не отображаются, добавьте параметр `@CategoryID` вручную (не нужно добавлять `@RETURN_VALUE` параметр).

![Проверьте правильность настроек параметров](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image44.png)

**Рис. 16**. Проверка правильности параметров

После обновления DAL удаление категории автоматически удалит все связанные с ней продукты и сделает это в рамках транзакции. Чтобы проверить это, вернитесь на страницу "обновление и удаление существующих двоичных данных" и нажмите кнопку "Удалить" для одной из категорий. При одном щелчке мыши Категория и все связанные с ней продукты будут удалены.

> [!NOTE]
> Перед тестированием хранимой процедуры `Categories_Delete`, которая удалит ряд продуктов вместе с выбранной категорией, возможно, будет целесообразно создать резервную копию базы данных. Если вы используете базу данных `NORTHWND.MDF` в `App_Data`, просто закройте Visual Studio и скопируйте файлы MDF и LDF в `App_Data` в другую папку. После тестирования функциональности базу данных можно восстановить, закрыв Visual Studio и заменив текущие файлы MDF и LDF в `App_Data` с резервными копиями.

## <a name="summary"></a>Сводка

В то время как мастер TableAdapter автоматически создает хранимые процедуры для нас, бывают случаи, когда эти хранимые процедуры уже созданы или вы хотите создать их вручную или с помощью других средств. Для поддержки таких сценариев TableAdapter также можно настроить так, чтобы он указывал на существующую хранимую процедуру. В этом учебнике мы рассмотрели, как вручную добавить хранимые процедуры в базу данных в среде Visual Studio и как связать методы TableAdapter s с этими хранимыми процедурами. Мы также рассмотрели команды T-SQL и шаблон сценария, используемые для запуска, фиксации и отката транзакций в хранимой процедуре.

Поздравляем с программированием!

## <a name="about-the-author"></a>Об авторе

[Скотт Митчелл](http://www.4guysfromrolla.com/ScottMitchell.shtml), автор семи книг по ASP/ASP. NET и основатель [4GuysFromRolla.com](http://www.4guysfromrolla.com), работал с веб-технологиями Майкрософт с 1998. Скотт работает как независимый консультант, преподаватель и модуль записи. Его последняя книга — [*Sams обучать себя ASP.NET 2,0 за 24 часа*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco). Он доступен по адресу [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) или через его блог, который можно найти по адресу [http://ScottOnWriting.NET](http://ScottOnWriting.NET).

## <a name="special-thanks-to"></a>Специальная благодарность

Эта серия руководств была рассмотрена многими полезными рецензентами. Потенциальные рецензенты для этого руководства были Хилтон Жеисенов, S REN Джейкоб Лауритсен и Терезой Мерфи. Хотите ознакомиться с моими будущими статьями MSDN? Если это так, расположите строку в [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Назад](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb.md)
> [Вперед](updating-the-tableadapter-to-use-joins-vb.md)
