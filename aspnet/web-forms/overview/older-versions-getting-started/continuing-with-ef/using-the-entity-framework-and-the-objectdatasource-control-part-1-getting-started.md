---
uid: web-forms/overview/older-versions-getting-started/continuing-with-ef/using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started
title: 'С помощью Entity Framework 4,0 и элемента управления ObjectDataSource, часть 1: начало работы | Документация Майкрософт'
author: tdykstra
description: Эта серия руководств основана на веб-приложении университета Contoso, которое создается начало работы с помощью Entity Framework серии руководств. Если yo...
ms.author: riande
ms.date: 01/26/2011
ms.assetid: 244278c1-fec8-4255-8a8a-13bde491c4f5
msc.legacyurl: /web-forms/overview/older-versions-getting-started/continuing-with-ef/using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started
msc.type: authoredcontent
ms.openlocfilehash: 2f14707eb058d438495dd2bc4c17b976c471fc97
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78440406"
---
# <a name="using-the-entity-framework-40-and-the-objectdatasource-control-part-1-getting-started"></a>С помощью Entity Framework 4,0 и элемента управления ObjectDataSource, часть 1: начало работы

от [Tom Dykstra)](https://github.com/tdykstra)

> Эта серия руководств основана на веб-приложении университета Contoso, которое создается [Начало работы с руководством по Entity Framework 4,0](../getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-1.md) . Если вы не выполнили предыдущие учебники, в качестве отправной точки для этого учебника вы можете скачать созданное [приложение](https://code.msdn.microsoft.com/ASPNET-Web-Forms-97f8ee9a) . Вы также можете [скачать приложение](https://code.msdn.microsoft.com/ASPNET-Web-Forms-6c7197aa) , созданное с помощью полной серии руководств.
> 
> Пример веб-приложения университета Contoso демонстрирует создание приложений ASP.NET Web Forms с помощью Entity Framework 4,0 и Visual Studio 2010. Пример приложения — это веб-сайт для вымышленного университета Contoso. На нем предусмотрены различные функции, в том числе прием учащихся, создание курсов и назначение преподавателей.
> 
> В учебнике показаны примеры C#в. [Загружаемый образец](https://code.msdn.microsoft.com/ASPNET-Web-Forms-6c7197aa) содержит код как в, C# так и в Visual Basic.
> 
> ## <a name="database-first"></a>База данных как основа
> 
> Существует три способа работы с данными в Entity Framework: *Database First*, *Model First*и *Code First*. Это руководство предназначено для Database First. Сведения о различиях между этими рабочими процессами и рекомендации по выбору наиболее подходящего сценария см. в разделе [рабочие процессы разработки Entity Framework](https://msdn.microsoft.com/library/ms178359.aspx#dbfmfcf).
> 
> ## <a name="web-forms"></a>Веб-формы
> 
> Как и в серии начало работы, в этой серии руководств используется модель веб-форм ASP.NET, и предполагается, что вы умеете работать с веб-формами ASP.NET в Visual Studio. Если это не так, см. статью [Начало работы с веб-формами ASP.NET 4,5](../../getting-started/getting-started-with-aspnet-45-web-forms/introduction-and-overview.md). Если вы предпочитаете работать с платформой MVC ASP.NET, см. статью [Начало работы с Entity Framework с помощью ASP.NET MVC](../../../../mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).
> 
> ## <a name="software-versions"></a>Версии программного обеспечения
> 
> | **Показано в руководстве** | **Также работает с** |
> | --- | --- |
> | Windows 7 | Windows 8 |
> | Visual Studio 2010 | Visual Studio 2010 Express для Web. Руководство не было протестировано в более поздних версиях Visual Studio. В выборе меню, диалоговых окнах и шаблонах существует много различий. |
> | .NET 4 | .NET 4,5 обратно совместима с .NET 4, но руководство не было протестировано с .NET 4,5. |
> | Entity Framework 4 | Руководство не было протестировано в более поздних версиях Entity Framework. Начиная с Entity Framework 5, EF использует по умолчанию `DbContext API`, который был представлен в EF 4,1. Элемент управления EntityDataSource предназначен для использования API `ObjectContext`. Сведения об использовании элемента управления EntityDataSource с API `DbContext` см. в [этой записи блога](https://blogs.msdn.com/b/webdev/archive/2012/09/13/how-to-use-the-entitydatasource-control-with-entity-framework-code-first.aspx). |
> 
> ## <a name="questions"></a>Вопросы
> 
> Если у вас есть вопросы, которые не связаны непосредственно с этим руководством, вы можете опубликовать их на [форуме по ASP.NET Entity Framework](https://forums.asp.net/1227.aspx), на [форуме Entity Framework и LINQ to Entities](https://social.msdn.microsoft.com/forums/adodotnetentityframework/threads/)или [StackOverflow.com](http://stackoverflow.com/).

Элемент управления `EntityDataSource` позволяет создавать приложения очень быстро, но для этого обычно требуется, чтобы на страницах *ASPX* было достаточно большого объема бизнес-логики и логики доступа к данным. Если вы предполагаете, что ваше приложение будет расти по сложности и требует постоянного обслуживания, можно приложить больше времени на разработку, чтобы создать структуру *n-уровневого* или *многоуровневой архитектуры* приложения, которая более удобна в обслуживании. Для реализации этой архитектуры необходимо отделить уровень представления от уровня бизнес-логики (BLL) и уровня доступа к данным (DAL). Одним из способов реализации этой структуры является использование элемента управления `ObjectDataSource` вместо элемента управления `EntityDataSource`. При использовании элемента управления `ObjectDataSource` вы реализуете собственный код доступа к данным, а затем вызываете его на *ASPX* -страницах с помощью элемента управления с множеством функций, аналогичных другим элементам управления источника данных. Это позволяет сочетать преимущества n-уровневого подхода с преимуществами использования элемента управления веб-форм для доступа к данным.

Элемент управления `ObjectDataSource` обеспечивает большую гибкость и другие способы. Поскольку вы пишете собственный код доступа к данным, проще всего выполнять не только чтение, вставку, обновление или удаление определенного типа сущности, а именно задачи, которые должен выполнить элемент управления `EntityDataSource`. Например, можно выполнять ведение журнала при каждом обновлении сущности, архивировать данные всякий раз при удалении сущности или автоматически проверять и обновлять связанные данные при вставке строки со значением внешнего ключа.

## <a name="business-logic-and-repository-classes"></a>Бизнес-логика и классы репозитория

Элемент управления `ObjectDataSource` работает путем вызова созданного класса. Класс включает методы, которые извлекают и обновляют данные, а также предоставляют имена этих методов элементу управления `ObjectDataSource` в разметке. Во время отрисовки или обработки обратной передачи `ObjectDataSource` вызывает указанные методы.

Помимо базовых операций CRUD, класс, который вы создаете для использования с элементом управления `ObjectDataSource`, может потребоваться выполнить бизнес-логику, когда `ObjectDataSource` считывает или обновляет данные. Например, при обновлении отдела может потребоваться проверить, что другие отделы не имеют одного и того же администратора, так как один пользователь не может быть администратором нескольких отделов.

В некоторых `ObjectDataSource` документации, например в [обзоре класса ObjectDataSource](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.aspx), элемент управления вызывает класс, называемый *бизнес-объектом* , который включает в себя как бизнес-логику, так и логику доступа к данным. В этом учебнике будут созданы отдельные классы для бизнес-логики и логики доступа к данным. Класс, инкапсулирующий логику доступа к данным, называется *репозиторием*. Класс бизнес-логики включает как методы логики, так и методы доступа к данным, но методы доступа к данным вызывают репозиторий для выполнения задач доступа к данным.

Также будет создан уровень абстракции между BLL и DAL, который упрощает автоматическое модульное тестирование слоя BLL. Этот уровень абстракции реализуется путем создания интерфейса и использования интерфейса при создании экземпляра репозитория в классе бизнес-логики. Это дает возможность предоставить класс бизнес-логики со ссылкой на любой объект, реализующий интерфейс репозитория. Для нормальной работы вы предоставляете объект репозитория, который работает с Entity Framework. Для тестирования вы предоставляете объект репозитория, который работает с данными, которые можно легко изменять, например переменные класса, определенные как коллекции.

На следующем рисунке показано различие между классом бизнес-логики, который включает в себя логику доступа к данным без репозитория и один из которых использует репозиторий.

[![Image05](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image2.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image1.png)

Начнем с создания веб-страниц, в которых элемент управления `ObjectDataSource` привязывается непосредственно к репозиторию, так как он выполняет только основные задачи доступа к данным. В следующем руководстве вы создадите класс бизнес-логики с логикой проверки и привязываете элемент управления `ObjectDataSource` к этому классу, а не к классу репозитория. Вы также создадите модульные тесты для логики проверки. В третьем учебнике этой серии вы добавите в приложение функции сортировки и фильтрации.

Страницы, создаваемые в этом руководстве, работают с `Departments` набором сущностей модели данных, созданной в [Начало работы серии руководств](../getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-1.md).

[![image01](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image4.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image3.png)

[![Image02](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image6.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image5.png)

## <a name="updating-the-database-and-the-data-model"></a>Обновление базы данных и модели данных

Вы начнете работу с этим руководством, внеся два изменения в базу данных, оба из которых потребовали соответствующих изменений модели данных, созданной в [Начало работы с учебниками по Entity Framework и веб-формам](../getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-1.md) . В одном из этих руководств вы внесли изменения в конструктор вручную для синхронизации модели данных с базой данных после изменения базы данных. В этом учебнике для автоматического обновления модели данных будет использоваться **модель обновления конструктора из базы данных** .

### <a name="adding-a-relationship-to-the-database"></a>Добавление связи с базой данных

В Visual Studio откройте веб-приложение университета Contoso, созданное в [Начало работы, с помощью серии руководств по Entity Framework и Web Forms](../getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-1.md) , а затем откройте диаграмму базы данных `SchoolDiagram`.

Если взглянуть на таблицу `Department` в диаграмме базы данных, вы увидите, что в ней есть `Administrator` столбец. Этот столбец является внешним ключом к `Person` таблице, но в базе данных не определено ни одной связи по внешнему ключу. Необходимо создать связь и обновить модель данных таким образом, чтобы Entity Framework мог автоматически справиться с этой связью.

В диаграмме базы данных щелкните правой кнопкой мыши таблицу `Department` и выберите пункт **связи**.

[![Image80](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image8.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image7.png)

В поле **связи по внешнему ключу** нажмите кнопку **Добавить**, а затем выберите **спецификацию таблиц и столбцов**.

[![Image81](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image10.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image9.png)

В диалоговом окне **таблицы и столбцы** задайте для поля и таблицы первичного ключа значение `Person` и `PersonID`и задайте для поля таблица и поле внешнего ключа значение `Department` и `Administrator`. (При этом имя связи изменится с `FK_Department_Department` на `FK_Department_Person`.)

[![Image82](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image12.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image11.png)

Нажмите кнопку **ОК** в поле **таблицы и столбцы** , нажмите кнопку **Закрыть** в поле **связи внешнего ключа** и сохраните изменения. Если появится запрос на сохранение `Person` и `Department` таблиц, нажмите кнопку **Да**.

> [!NOTE]
> Если вы удалили `Person` строки, соответствующие данным, которые уже находятся в `Administrator` столбце, сохранить это изменение будет невозможно. В этом случае используйте редактор таблиц в **Обозреватель сервера** , чтобы убедиться, что `Administrator` значение в каждой строке `Department` содержит идентификатор записи, которая фактически существует в таблице `Person`.
> 
> После сохранения изменений вы не сможете удалить строку из таблицы `Person`, если этот пользователь является администратором отдела. В рабочем приложении необходимо указать конкретное сообщение об ошибке, если ограничение базы данных не позволяет удалить или вы указали каскадное удаление. Пример указания каскадного удаления см. [в разделе Entity Framework и ASP.NET – начало работы часть 2](../getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-2.md).

### <a name="adding-a-view-to-the-database"></a>Добавление представления в базу данных

На создаваемой странице создать *Departments. aspx* необходимо предоставить раскрывающийся список инструкторов с именами в формате "фамилия, первый", чтобы пользователи могли выбрать администраторов отделов. Чтобы упростить это, вы создадите представление в базе данных. Представление будет содержать только данные, необходимые для раскрывающегося списка: полное имя (в правильном формате) и ключ записи.

В **Обозреватель сервера**разверните *School. mdf*, щелкните правой кнопкой мыши папку **представления** и выберите команду **Добавить новое представление**.

[![Image06](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image14.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image13.png)

Нажмите кнопку **Закрыть** при появлении диалогового окна **Добавление таблицы** и вставьте следующую инструкцию SQL на панель SQL:

[!code-sql[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample1.sql)]

Сохраните представление как `vInstructorName`.

### <a name="updating-the-data-model"></a>Обновление модели данных

В папке *DAL* откройте файл *счулмодел. EDMX* , щелкните правой кнопкой мыши область конструктора и выберите пункт **Обновить модель из базы данных**.

[![Image07](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image16.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image15.png)

В диалоговом окне **Выбор объектов базы данных** перейдите на вкладку **Добавить** и выберите только что созданное представление.

[![Image08](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image18.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image17.png)

Нажмите кнопку **Готово**.

В конструкторе вы увидите, что средство создало `vInstructorName` сущность и новую связь между сущностями `Department` и `Person`.

[![Image13](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image20.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image19.png)

> [!NOTE]
> В **выходных данных** и **Список ошибок** окнах может появиться предупреждающее сообщение о том, что средство автоматически создало первичный ключ для нового представления `vInstructorName`. Это ожидаемое поведение.

При ссылке на новую сущность `vInstructorName` в коде вы не хотите использовать соглашение об использовании базы данных с префиксом "v" в нижнем регистре. Таким образом, сущность и набор сущностей будут переименованы в модели.

Откройте **Обозреватель моделей**. Вы увидите, `vInstructorName` перечислены как тип сущности и представление.

[![Image14](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image22.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image21.png)

В разделе **счулмодел** (не **счулмодел. Store**) щелкните правой кнопкой мыши элемент **винструкторнаме** и выберите пункт **Свойства**. В окне **Свойства** измените свойство **Name** на "инструкторнаме" и измените значение свойства " **имя набора сущностей** " на "инструкторнамес".

[![Image15](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image24.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image23.png)

Сохраните и закройте модель данных, а затем перестройте проект.

## <a name="using-a-repository-class-and-an-objectdatasource-control"></a>Использование класса репозитория и элемента управления ObjectDataSource

Создайте новый файл класса в папке *DAL* , назовите его *SchoolRepository.CS*и замените существующий код следующим кодом:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample2.cs)]

Этот код предоставляет один метод `GetDepartments`, который возвращает все сущности в `Departments`ном наборе сущностей. Поскольку известно, что вы будете обращаться к свойству навигации `Person` для каждой возвращаемой строки, вы указываете безотлагательную загрузку для этого свойства с помощью метода `Include`. Класс также реализует интерфейс `IDisposable`, чтобы гарантировать освобождение подключения к базе данных при удалении объекта.

> [!NOTE]
> Распространенной практикой является создание класса репозитория для каждого типа сущности. В этом руководстве используется один класс репозитория для нескольких типов сущностей. Дополнительные сведения о шаблоне репозитория см. в записях [блога Entity Framework команды](https://blogs.msdn.com/b/adonet/archive/2009/06/16/using-repository-and-unit-of-work-patterns-with-entity-framework-4-0.aspx) и в блоге по [Юлия Лерман](http://thedatafarm.com/blog/data-access/agile-ef4-repository-part-3-fine-tuning-the-repository/).

Метод `GetDepartments` возвращает объект `IEnumerable`, а не объект `IQueryable`, чтобы гарантировать, что возвращаемая коллекция будет использоваться даже после удаления объекта репозитория. Объект `IQueryable` может вызвать доступ к базе данных при каждом доступе к нему, но объект репозитория может быть удален на время, когда элемент управления с привязкой к данным пытается обработать данные. Можно вернуть другой тип коллекции, например объект `IList`, а не объект `IEnumerable`. Однако возврат объекта `IEnumerable` гарантирует, что вы сможете выполнять стандартные задачи обработки списков только для чтения, такие как циклы `foreach` и запросы LINQ, но нельзя добавлять или удалять элементы в коллекции, что может предположить, что такие изменения будут сохранены в базе данных.

Создайте страницу *Departments. aspx* , использующую главную страницу *site. master* , и добавьте следующую разметку в элемент управления `Content` с именем `Content2`:

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample3.aspx)]

Эта разметка создает элемент управления `ObjectDataSource`, использующий только что созданный класс репозитория, и элемент управления `GridView` для вывода данных. Элемент управления `GridView` указывает команды **Edit** и **Delete** , но вы еще не добавили код для их поддержки.

В нескольких столбцах используются `DynamicField` элементы управления, что позволяет воспользоваться преимуществами автоматического форматирования данных и функций проверки. Чтобы они работали, необходимо вызвать метод `EnableDynamicData` в обработчике событий `Page_Init`. (`DynamicControl` элементы управления не используются в поле `Administrator`, так как они не работают со свойствами навигации.)

Атрибуты `Vertical-Align="Top"` будут важны позже при добавлении столбца с вложенным элементом управления `GridView` в сетку.

Откройте файл *Departments.aspx.CS* и добавьте следующую инструкцию `using`:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample4.cs)]

Затем добавьте следующий обработчик для события `Init` страницы:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample5.cs)]

В папке *DAL* создайте новый файл класса с именем *Department.CS* и замените существующий код следующим кодом:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample6.cs)]

Этот код добавляет метаданные в модель данных. Он указывает, что свойство `Budget` сущности `Department` фактически представляет валюту, хотя ее тип данных — `Decimal`и указывает, что значение должно находиться в диапазоне от 0 до $1 000 000,00. Он также указывает, что свойство `StartDate` должно быть отформатировано как дата в формате mm/дд/гггг.

Запустите страницу *departmentss. aspx* .

[![image01](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image26.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image25.png)

Обратите внимание, что хотя вы не указали строку формата в разметке страницы *Departments. aspx* для столбцов **бюджет** или **Дата начала** , к ним были применены элементы управления `DynamicField`, используемые по умолчанию, с использованием метаданных, указанных в файле *Department.CS* .

## <a name="adding-insert-and-delete-functionality"></a>Добавление функций вставки и удаления

Откройте *SchoolRepository.CS*, добавьте следующий код, чтобы создать метод `Insert` и метод `Delete`. Код также включает метод с именем `GenerateDepartmentID`, который вычисляет следующее доступное значение ключа записи для использования методом `Insert`. Это необходимо, поскольку база данных не настроена для автоматического вычисления для таблицы `Department`.

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample7.cs)]

### <a name="the-attach-method"></a>Метод Attach

Метод `DeleteDepartment` вызывает метод `Attach`, чтобы повторно установить ссылку, которая сохраняется в диспетчере состояний объектов контекста объекта между сущностью в памяти и строкой базы данных, которую она представляет. Это должно произойти до того, как метод вызовет метод `SaveChanges`.

Термин *контекст объекта* относится к классу Entity Framework, производному от класса `ObjectContext`, который используется для доступа к наборам сущностей и сущностям. В коде для этого проекта класс имеет имя `SchoolEntities`, а экземпляр с именем всегда имеет имя `context`. *Диспетчер состояния объектов* контекста объекта является классом, производным от класса `ObjectStateManager`. Контакт объекта использует диспетчер состояний объектов для хранения объектов сущностей и для отслеживания того, синхронизирован ли каждый из них с соответствующей строкой таблицы или строками в базе данных.

При чтении сущности контекст объекта сохраняет его в диспетчере состояний объектов и отслеживает, синхронизировано ли это представление объекта с базой данных. Например, если изменить значение свойства, устанавливается флаг, указывающий, что измененное свойство больше не синхронизировано с базой данных. Затем при вызове метода `SaveChanges` контекст объекта знает, что делать в базе данных, так как диспетчер состояний объектов точно знает, что отличается между текущим состоянием сущности и состоянием базы данных.

Однако этот процесс обычно не работает в веб-приложении, так как экземпляр контекста объекта, считывающий сущность вместе со всеми объектами в ее диспетчере состояния объектов, удаляется после отрисовки страницы. Экземпляр контекста объекта, который должен применить изменения, является новым, созданным для обработки обратной передачи. В случае с методом `DeleteDepartment` элемент управления `ObjectDataSource` повторно создает исходную версию сущности из значений в состоянии представления, но эта повторно созданная сущность `Department` не существует в диспетчере состояний объектов. Если вызвать метод `DeleteObject` для этой повторно созданной сущности, вызов завершится ошибкой, так как контекст объекта не знает, синхронизирована ли сущность с базой данных. Однако вызов метода `Attach` повторно устанавливает то же отслеживание между повторно созданной сущностью и значениями в базе данных, которые изначально выполнялись автоматически при считывании сущности в более раннем экземпляре контекста объекта.

Иногда не требуется, чтобы контекст объекта был отслеживанием сущностей в диспетчере состояний объектов, а также можно установить флаги, чтобы предотвратить это. Примеры приведены в последующих руководствах этой серии.

### <a name="the-savechanges-method"></a>Метод SaveChanges

Этот простой класс репозитория иллюстрирует основные принципы выполнения операций CRUD. В этом примере метод `SaveChanges` вызывается сразу после каждого обновления. В рабочем приложении может потребоваться вызвать метод `SaveChanges` из отдельного метода, чтобы обеспечить более полный контроль над обновлением базы данных. (В конце следующего руководства вы найдете ссылку на технический документ, в котором обсуждается шаблон единицы работы, который является одним из подходов к координации связанных обновлений.) Кроме того, обратите внимание, что в примере метод `DeleteDepartment` не включает код для обработки конфликтов параллелизма; код для этого будет добавлен в более позднем учебнике этой серии.

### <a name="retrieving-instructor-names-to-select-when-inserting"></a>Получение имен преподавателей для выбора при вставке

Пользователи должны иметь возможность выбрать администратора из списка инструкторов в раскрывающемся списке при создании новых подразделений. Поэтому добавьте следующий код в *SchoolRepository.CS* , чтобы создать метод для получения списка преподавателей с помощью представления, созданного ранее.

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample8.cs)]

### <a name="creating-a-page-for-inserting-departments"></a>Создание страницы для вставки отделов

Создайте страницу *департментсадд. aspx* , которая использует страницу *site. master* , и добавьте следующую разметку в элемент управления `Content` с именем `Content2`:

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample9.aspx)]

Эта разметка создает два элемента управления `ObjectDataSource`, один для вставки новых сущностей `Department` и один для получения имен преподавателей для элемента управления `DropDownList`, используемого для выбора администраторов отдела. Разметка создает `DetailsView` элемент управления для ввода новых отделов и задает обработчик для события `ItemInserting` элемента управления, чтобы можно было задать значение внешнего ключа `Administrator`. В конце находится элемент управления `ValidationSummary` для вывода сообщений об ошибках.

Откройте *DepartmentsAdd.aspx.CS* и добавьте следующую инструкцию `using`:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample10.cs)]

Добавьте следующие переменные и методы класса:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample11.cs)]

Метод `Page_Init` включает функции платформа динамических данных. Обработчик события `Init` элемента управления `DropDownList` сохраняет ссылку на элемент управления, а обработчик для события `Inserting` элемента управления `DetailsView` использует эту ссылку для получения `PersonID` значения выбранного преподавателя и обновления свойства `Administrator` внешнего ключа сущности `Department`.

Запустите страницу, добавьте сведения о новом отделе, а затем щелкните ссылку **Вставить** .

[![Image04](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image28.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image27.png)

Введите значения для другого нового отдела. Введите число больше 1 000 000,00 в поле **бюджета** и перейдите к следующему полю. В поле появится звездочка, и если навести на нее указатель мыши, отобразится сообщение об ошибке, введенное в поле метаданные для этого поля.

[![Image03](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image30.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image29.png)

Нажмите кнопку **Вставить**, после чего отобразится сообщение об ошибке, отображаемое элементом управления `ValidationSummary` в нижней части страницы.

[![Image12](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image32.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image31.png)

Затем закройте браузер и откройте страницу *departmentss. aspx* . Добавьте возможность удаления на страницу *Departments. aspx* , добавив атрибут `DeleteMethod` в элемент управления `ObjectDataSource` и атрибут `DataKeyNames` к элементу управления `GridView`. Открывающие теги для этих элементов управления теперь будут выглядеть следующим образом:

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample12.aspx)]

Запустите страницу.

[![Image09](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image34.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image33.png)

Удалите подразделение, добавленное при выполнении страницы *департментсадд. aspx* .

## <a name="adding-update-functionality"></a>Добавление функции обновления

Откройте *SchoolRepository.CS* и добавьте следующий метод `Update`:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample13.cs)]

При нажатии кнопки **Обновить** на странице *Departments. aspx* элемент управления `ObjectDataSource` создает две `Department` сущности для передачи методу `UpdateDepartment`. Одна из них содержит исходные значения, сохраненные в состоянии представления, а другая содержит новые значения, введенные в элементе управления `GridView`. Код в методе `UpdateDepartment` передает сущность `Department`, которая имеет исходные значения, в метод `Attach`, чтобы установить отслеживание между сущностью и базой данных. Затем код передает `Department` сущность, которая имеет новые значения для метода `ApplyCurrentValues`. Контекст объекта сравнивает старое и новое значения. Если новое значение отличается от старого, контекст объекта изменяет значение свойства. Затем метод `SaveChanges` обновляет только измененные столбцы в базе данных. (Однако если функция обновления для этой сущности сопоставлена с хранимой процедурой, вся строка будет обновлена независимо от того, какие столбцы были изменены.)

Откройте файл *departmentss. aspx* и добавьте в элемент управления `DepartmentsObjectDataSource` следующие атрибуты:

- `UpdateMethod="UpdateDepartment"`
- `ConflictDetection="CompareAllValues"`   
 В результате старые значения сохраняются в состоянии представления, чтобы их можно было сравнивать с новыми значениями в методе `Update`.
- `OldValuesParameterFormatString="orig{0}"`   
 Это информирует элемент управления о том, что имя параметра исходных значений `origDepartment`.

Разметка для открывающего тега элемента управления `ObjectDataSource` теперь напоминает следующий пример:

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample14.aspx)]

Добавьте атрибут `OnRowUpdating="DepartmentsGridView_RowUpdating"` в элемент управления `GridView`. Он используется для задания значения свойства `Administrator` на основе строки, выбираемой пользователем в раскрывающемся списке. Открывающий тег `GridView` теперь напоминает следующий пример:

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample15.aspx)]

Добавьте элемент управления `EditItemTemplate` для столбца `Administrator` в элемент управления `GridView` сразу после элемента управления `ItemTemplate` для этого столбца:

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample16.aspx)]

Этот `EditItemTemplate` элемент управления аналогичен элементу управления `InsertItemTemplate` на странице *департментсадд. aspx* . Разница заключается в том, что начальное значение элемента управления задается с помощью атрибута `SelectedValue`.

Перед элементом управления `GridView` добавьте элемент управления `ValidationSummary`, как показано на странице *департментсадд. aspx* .

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample17.aspx)]

Откройте *Departments.aspx.CS* и сразу после объявления разделяемого класса добавьте следующий код, чтобы создать частное поле для ссылки на элемент управления `DropDownList`:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample18.cs)]

Затем добавьте обработчики для `Init` события элемента управления `DropDownList` и события `RowUpdating` элемента управления `GridView`:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample19.cs)]

Обработчик события `Init` сохраняет ссылку на элемент управления `DropDownList` в поле класс. Обработчик события `RowUpdating` использует ссылку для получения значения, которое пользователь указал, и применения его к свойству `Administrator` сущности `Department`.

Используйте страницу *департментсадд. aspx* для добавления нового отдела, затем запустите страницу *departmentss. aspx* и нажмите кнопку **изменить** в добавленной строке.

> [!NOTE]
> Вы не сможете изменять строки, которые не были добавлены (то есть уже в базе данных) из-за недопустимых данных в базе данных. Администраторы для строк, созданных с помощью базы данных, являются студентами. При попытке изменить один из них вы получите страницу ошибки, которая сообщает об ошибке, например `'InstructorsDropDownList' has a SelectedValue which is invalid because it does not exist in the list of items.`

[![Image10](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image36.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image35.png)

Если ввести недопустимую сумму **бюджета** и нажать кнопку **Обновить**, появится та же звездочка и сообщение об ошибке, которое вы видели на странице *Departments. aspx* .

Измените значение поля или выберите другого администратора и нажмите кнопку **Обновить**. Будет отображено изменение.

[![Image09](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image38.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image37.png)

Это завершает вводные сведения об использовании элемента управления `ObjectDataSource` для базовых операций CRUD (создание, чтение, обновление, удаление) с Entity Framework. Вы создали простое n-уровневое приложение, но уровень бизнес-логики по-прежнему тесно связан с уровнем доступа к данным, что усложняет автоматическое модульное тестирование. В следующем учебнике вы узнаете, как реализовать шаблон репозитория для упрощения модульного тестирования.

> [!div class="step-by-step"]
> [Дальше](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests.md)
