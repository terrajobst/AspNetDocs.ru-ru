---
uid: web-forms/overview/older-versions-getting-started/continuing-with-ef/handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application
title: Обработка параллелизма с помощью Entity Framework 4,0 в веб-приложении ASP.NET 4 | Документация Майкрософт
author: tdykstra
description: Эта серия руководств основана на веб-приложении университета Contoso, которое создается начало работы с руководством по Entity Framework 4,0. Он...
ms.author: riande
ms.date: 01/26/2011
ms.assetid: a5aa22a6-fb7f-4f41-9c7f-addda151940b
msc.legacyurl: /web-forms/overview/older-versions-getting-started/continuing-with-ef/handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application
msc.type: authoredcontent
ms.openlocfilehash: 3df5f7d9c8fb22e1ea34fe16560bdb9a1309bb56
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78513504"
---
# <a name="handling-concurrency-with-the-entity-framework-40-in-an-aspnet-4-web-application"></a>Обработка параллелизма с помощью Entity Framework 4,0 в веб-приложении ASP.NET 4

от [Tom Dykstra)](https://github.com/tdykstra)

> Эта серия руководств основана на веб-приложении университета Contoso, которое создается [Начало работы с руководством по Entity Framework 4,0](https://asp.net/entity-framework/tutorials#Getting%20Started) . Если вы не выполнили предыдущие учебники, в качестве отправной точки для этого учебника вы можете скачать созданное [приложение](https://code.msdn.microsoft.com/ASPNET-Web-Forms-97f8ee9a) . Вы также можете [скачать приложение](https://code.msdn.microsoft.com/ASPNET-Web-Forms-6c7197aa) , созданное с помощью полной серии руководств. Если у вас есть вопросы о учебниках, их можно опубликовать на [форуме ASP.NET Entity Framework](https://forums.asp.net/1227.aspx).

В предыдущем учебнике вы узнали, как сортировать и фильтровать данные с помощью элемента управления `ObjectDataSource` и Entity Framework. В этом руководстве показаны параметры обработки параллелизма в веб-приложении ASP.NET, использующем Entity Framework. Вы создадите новую веб-страницу, предназначенную для обновления назначений для преподавателей в офисе. Вы будете справляться с проблемами параллелизма на этой странице и на странице отделов, созданной ранее.

[![Image06](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image2.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image1.png)

[![image01](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image4.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image3.png)

## <a name="concurrency-conflicts"></a>Конфликты параллелизма

Конфликт параллелизма возникает, когда один пользователь изменяет запись, а другой пользователь редактирует ту же запись до того, как первое изменение пользователя записывается в базу данных. Если вы не настраиваете Entity Framework для обнаружения таких конфликтов, кто угодно обновляет базу данных в последнюю очередь, перезапишу изменения другого пользователя. Во многих приложениях этот риск приемлем, и вам не нужно настраивать приложение для обработки возможных конфликтов параллелизма. (При наличии небольшого числа пользователей или небольшого числа обновлений или если не очень важно, если некоторые изменения перезаписываются, затраты на программирование параллелизма могут перестать иметь преимущество.) Если вам не нужно беспокоиться о конфликтах параллелизма, можно пропустить этот учебник. остальные два руководства в ряде не зависят от того, что вы создаете в этой серии.

### <a name="pessimistic-concurrency-locking"></a>Пессимистичный параллелизм (блокировка)

Если приложению нужно предотвратить случайную потерю данных в сценариях параллелизма, одним из способов сделать это являются блокировки базы данных. Это называется *пессимистичным параллелизмом*. Например, перед чтением строки из базы данных вы запрашиваете блокировку для доступа для обновления или только для чтения. Если заблокировать строку для обновления, другие пользователи не могут заблокировать ее для обновления или только для чтения, так как получат копию данных, которые находятся в процессе изменения. Если заблокировать строку только для чтения, другие пользователи также могут заблокировать ее только для чтения, но не для обновления.

Управление блокировками имеет некоторые недостатки. Оно может оказаться сложным с точки зрения программирования. Он требует значительных ресурсов управления базами данных и может вызвать проблемы с производительностью по мере увеличения числа пользователей приложения (то есть оно не масштабируется). Поэтому не все системы управления базами данных поддерживают пессимистичный параллелизм. Entity Framework не предоставляет встроенную поддержку для нее, и в этом руководстве не показано, как его реализовать.

### <a name="optimistic-concurrency"></a>Оптимистический параллелизм

Альтернативой пессимистичному параллелизму является *оптимистичный параллелизм*. Оптимистическая блокировка допускает появление конфликтов параллелизма, а затем обрабатывает их соответствующим образом. Например, Джон запускает страницу *Department. aspx* , щелкает ссылку Edit ( **изменить** ) для Отдела истории и сокращает сумму **бюджета** с $1 000 000,00 до $125 000,00. (Джон управляет конкурирующим Отделом и хочет освободить деньги для своего собственного отдела.)

[![Image07](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image6.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image5.png)

Прежде чем Джон нажмет кнопку " **Обновить**", Мария выполняет ту же страницу, щелкает ссылку " **изменить** " для отдела журнала, а затем изменяет поле " **Дата начала** " с 1/10/2011 на 1/1/1999. (Мария управляет Отделом истории и хочет предоставить ему более старший стаж.)

[![Image08](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image8.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image7.png)

Джон нажимает кнопку « **Обновить** », а затем Мария щелкает **Update**. Браузер Джейн теперь выводит сумму **бюджета** как $1 000 000,00, но это неверно, так как сумма была изменена с джон на $125 000,00.

Ниже перечислены некоторые действия, которые можно выполнить в этом сценарии.

- Вы можете отслеживать, для какого свойства пользователь изменил и обновил только соответствующие столбцы в базе данных. В этом примере сценария данные не будут потеряны, так как эти два пользователя обновляли разные свойства. В следующий раз, когда кто-то просматривает Отдел по истории, он увидит 1/1/1999 и $125 000,00. 

    Это поведение по умолчанию в Entity Framework и может значительно снизить количество конфликтов, которые могут привести к утрате данных. Однако такое поведение не позволяет избежать потери данных, если конкурирующие изменения вносятся в одно и то же свойство сущности. Кроме того, такое поведение не всегда возможно; При сопоставлении хранимых процедур с типом сущности все свойства сущности обновляются при внесении изменений в сущность в базе данных.
- Вы можете позволить Марии изменить перезапись изменений Джон. После того как Мария нажмет кнопку " **Обновить**", сумма **бюджета** возвращается к $1 000 000,00. Такой подход называется *победой клиента* или *сохранением последнего внесенного изменения*. (Значения клиента имеют приоритет над тем, что есть в хранилище данных.)
- Вы можете предотвратить обновление Марии в базе данных. Как правило, выводится сообщение об ошибке, отображается его текущее состояние и пользователь может повторно ввести изменения, если он все еще хочет сделать это. Можно дополнительно автоматизировать процесс, сохранив входные данные и предоставив ему возможность повторно применять его без необходимости вводить его заново. Это называется *победой хранилища*. (Значения в хранилище имеют приоритет над данными, передаваемыми клиентом.)

### <a name="detecting-concurrency-conflicts"></a>Обнаружение конфликтов параллелизма

В Entity Framework можно разрешить конфликты, обрабатывая исключения `OptimisticConcurrencyException`, которые создает Entity Framework. Чтобы определить, когда именно нужно выдавать исключения, платформа Entity Framework должна быть в состоянии обнаруживать конфликты. Поэтому нужно соответствующим образом настроить базу данных и модель данных. Ниже приведены некоторые варианты для реализации обнаружения конфликтов:

- В базе данных включите столбец таблицы, с помощью которого можно определить, когда строка была изменена. Затем можно настроить Entity Framework, чтобы включить этот столбец в предложение `Where` команд SQL `Update` или `Delete`.

    Это назначение столбца `Timestamp` в таблице `OfficeAssignment`.

    [![Image09](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image10.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image9.png)

    Тип данных `Timestamp` столбца также называется `Timestamp`. Однако столбец на самом деле не содержит значения даты или времени. Вместо этого значение представляет собой порядковый номер, увеличивающийся при каждом обновлении строки. В команде `Update` или `Delete` предложение `Where` включает исходное значение `Timestamp`. Если обновляемая строка была изменена другим пользователем, значение в `Timestamp` отличается от исходного значения, поэтому предложение `Where` не возвращает строку для обновления. Когда Entity Framework обнаружит, что ни одна из строк не обновлялась текущей `Update` или командой `Delete` (то есть если число затронутых строк равно нулю), это интерпретируется как конфликт параллелизма.
- Настройте Entity Framework, чтобы включить исходные значения каждого столбца в таблице в предложении `Where` для команд `Update` и `Delete`.

    Как и в первом случае, если при первом чтении строки было изменено какое-либо значение в строке, предложение `Where` не вернет строку для обновления, которая Entity Framework интерпретируется как конфликт параллелизма. Этот метод действует так же, как `Timestamp` поле, но может быть неэффективным. Для таблиц базы данных, имеющих много столбцов, это может привести к созданию очень больших `Where` предложений, а в веб-приложении это может потребовать сохранения большого количества состояний. Поддержание большого количества состояний может повлиять на производительность приложения, так как требует наличия ресурсов сервера (например, состояния сеанса) или должны быть добавлены в саму веб-страницу (например, состояние представления).

В этом учебнике будет добавлена обработка ошибок для конфликтов оптимистичного параллелизма для сущности, которая не имеет свойства отслеживания (сущность `Department`) и для сущности, у которой есть свойство отслеживания (сущность `OfficeAssignment`).

## <a name="handling-optimistic-concurrency-without-a-tracking-property"></a>Обработка оптимистичного параллелизма без свойства отслеживания

Чтобы реализовать оптимистичный параллелизм для `Department` сущности, которая не имеет свойства отслеживания (`Timestamp`), вам предстоит выполнить следующие задачи:

- Измените модель данных, чтобы включить отслеживание параллелизма для сущностей `Department`.
- В классе `SchoolRepository` Обрабатывайте исключения параллелизма в методе `SaveChanges`.
- На странице *Departments. aspx* обработка исключений параллелизма путем отображения сообщения пользователю с предупреждением о том, что попытки изменения не были успешными. Пользователь может просмотреть текущие значения и повторить изменения, если они все еще нужны.

### <a name="enabling-concurrency-tracking-in-the-data-model"></a>Включение отслеживания параллелизма в модели данных

В Visual Studio откройте веб-приложение Contoso университета, с которым вы работали в предыдущем учебнике этой серии.

Откройте *счулмодел. EDMX*и в конструкторе моделей данных щелкните правой кнопкой мыши свойство `Name` в сущности `Department` и выберите пункт **свойства**. В окне **Свойства** измените значение свойства `ConcurrencyMode` на `Fixed`.

[![Image16](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image12.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image11.png)

Сделайте то же самое для других скалярных свойств, не являющихся первичными ключами (`Budget`, `StartDate`и `Administrator`.) (Это невозможно сделать для свойств навигации.) Это указывает, что каждый раз, когда Entity Framework создает команду SQL `Update` или `Delete` для обновления сущности `Department` в базе данных, эти столбцы (с исходными значениями) должны включаться в предложение `Where`. Если при выполнении команды `Update` или `Delete` не найдено ни одной строки, Entity Framework вызовет исключение оптимистичного параллелизма.

Сохраните и закройте модель данных.

### <a name="handling-concurrency-exceptions-in-the-dal"></a>Обработка исключений параллелизма в DAL

Откройте *SchoolRepository.CS* и добавьте следующую инструкцию `using` для пространства имен `System.Data`:

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample1.cs)]

Добавьте следующий новый метод `SaveChanges`, обрабатывающий исключения оптимистичного параллелизма:

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample2.cs)]

Если при вызове этого метода возникает ошибка параллелизма, то значения свойств сущности в памяти заменяются значениями, находящиеся в базе данных. Исключение параллелизма вызывается повторно, чтобы веб-страница могла ее обменять.

В методах `DeleteDepartment` и `UpdateDepartment` замените существующий вызов на `context.SaveChanges()`, вызвав метод `SaveChanges()` для вызова нового метода.

### <a name="handling-concurrency-exceptions-in-the-presentation-layer"></a>Обработка исключений параллелизма на уровне представления

Откройте *отделы. aspx* и добавьте атрибут `OnDeleted="DepartmentsObjectDataSource_Deleted"` в элемент управления `DepartmentsObjectDataSource`. Открывающий тег для элемента управления теперь будет выглядеть следующим образом.

[!code-aspx[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample3.aspx)]

В элементе управления `DepartmentsGridView` укажите все столбцы таблицы в атрибуте `DataKeyNames`, как показано в следующем примере. Обратите внимание, что это приведет к созданию очень больших полей состояния представления, что является одной из причин того, что использование поля отслеживания обычно является предпочтительным способом отслеживания конфликтов параллелизма.

[!code-aspx[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample4.aspx)]

Откройте *Departments.aspx.CS* и добавьте следующую инструкцию `using` для пространства имен `System.Data`:

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample5.cs)]

Добавьте следующий новый метод, который будет вызываться из обработчиков событий `Updated` и `Deleted` для обработки исключений параллелизма:

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample6.cs)]

Этот код проверяет тип исключения и, если это исключение параллелизма, код динамически создает `CustomValidator` элемент управления, который, в свою очередь, отображает сообщение в элементе управления `ValidationSummary`.

Вызовите новый метод из обработчика `Updated` событий, добавленного ранее. Кроме того, создайте новый обработчик событий `Deleted`, который вызывает тот же метод (но не выполняет никаких других действий):

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample7.cs)]

### <a name="testing-optimistic-concurrency-in-the-departments-page"></a>Тестирование оптимистичного параллелизма на странице «отделы»

Запустите страницу *departmentss. aspx* .

[![Image17](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image14.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image13.png)

Нажмите кнопку **изменить** в строке и измените значение в столбце **бюджет** . (Помните, что вы можете изменять только те записи, которые были созданы для работы с этим руководством, так как существующие записи `School` базы данных содержат недопустимые данные. Запись для отдела экономики является надежной для экспериментов.)

[![Image18](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image16.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image15.png)

Откройте новое окно браузера и снова запустите страницу (скопируйте URL-адрес из первого поля адреса окна браузера во второе окно браузера).

[![Image17](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image18.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image17.png)

Щелкните **изменить** в той же строке, которую вы редактировали ранее, и измените значение **бюджета** на другое.

[![Image19](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image20.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image19.png)

Во втором окне браузера нажмите кнопку **Обновить**. Сумма **бюджета** успешно изменена на это новое значение.

[![Image20](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image22.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image21.png)

В первом окне браузера нажмите кнопку **Обновить**. Обновление завершается сбоем. Сумма **бюджета** отображается повторно с использованием значения, заданного во втором окне браузера, и появляется сообщение об ошибке.

[![Image21](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image24.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image23.png)

## <a name="handling-optimistic-concurrency-using-a-tracking-property"></a>Обработка оптимистичного параллелизма с помощью свойства отслеживания

Для обработки оптимистичного параллелизма сущности, имеющей свойство отслеживания, вам предстоит выполнить следующие задачи:

- Добавьте хранимые процедуры в модель данных для управления сущностями `OfficeAssignment`. (Свойства отслеживания и хранимые процедуры не должны использоваться вместе, они просто группируются здесь для иллюстрации.)
- Добавьте методы CRUD в DAL и BLL для `OfficeAssignment` сущностей, включая код для обработки исключений оптимистичного параллелизма в DAL.
- Создание веб-страницы назначений Office.
- Проверьте оптимистичный параллелизм на новой веб-странице.

### <a name="adding-officeassignment-stored-procedures-to-the-data-model"></a>Добавление хранимых процедур OfficeAssignment в модель данных

Откройте файл *счулмодел. EDMX* в конструкторе моделей, щелкните правой кнопкой мыши область конструктора и выберите пункт **Обновить модель из базы данных**. На вкладке **Добавить** в диалоговом окне **Выбор объектов базы данных** разверните узел **хранимые процедуры** и выберите три `OfficeAssignment` хранимые процедуры (см. следующий снимок экрана) и нажмите кнопку **Готово**. (Эти хранимые процедуры уже находятся в базе данных при их скачивании или создании с помощью скрипта.)

[![Image02](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image26.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image25.png)

Щелкните правой кнопкой мыши сущность `OfficeAssignment` и выберите **сопоставление хранимых процедур**.

[![Image03](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image28.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image27.png)

Задайте функции **вставки**, **обновления**и **удаления** , чтобы использовать их соответствующие хранимые процедуры. Для параметра `OrigTimestamp` функции `Update` задайте для **Свойства** значение `Timestamp` и выберите параметр **использовать исходное значение** .

[![Image04](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image30.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image29.png)

Когда Entity Framework вызывает хранимую процедуру `UpdateOfficeAssignment`, она передает исходное значение столбца `Timestamp` в параметре `OrigTimestamp`. Хранимая процедура использует этот параметр в своем предложении `Where`:

[!code-sql[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample8.sql)]

Хранимая процедура также выбирает новое значение `Timestamp` столбца после обновления, чтобы Entity Framework мог сохранить `OfficeAssignment` сущность, которая находится в синхронизированной памяти, с соответствующей строкой базы данных.

(Обратите внимание, что хранимая процедура для удаления назначения Office не имеет параметра `OrigTimestamp`. По этой причине Entity Framework не может проверить, не изменилась ли сущность перед ее удалением.)

Сохраните и закройте модель данных.

### <a name="adding-officeassignment-methods-to-the-dal"></a>Добавление методов OfficeAssignment в DAL

Откройте *ISchoolRepository.CS* и добавьте следующие методы CRUD для набора сущностей `OfficeAssignment`:

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample9.cs)]

Добавьте в *SchoolRepository.CS*следующие новые методы. В методе `UpdateOfficeAssignment` вместо `context.SaveChanges`вызывается метод локального `SaveChanges`.

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample10.cs)]

В тестовом проекте откройте *MockSchoolRepository.CS* и добавьте в нее следующие методы `OfficeAssignment` Collection и CRUD. (Макет репозитория должен реализовывать интерфейс репозитория, иначе решение не будет компилироваться.)

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample11.cs)]

### <a name="adding-officeassignment-methods-to-the-bll"></a>Добавление методов OfficeAssignment к BLL

В основном проекте откройте *SchoolBL.CS* и добавьте в него следующие методы CRUD для `OfficeAssignment` набора сущностей:

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample12.cs)]

## <a name="creating-an-officeassignments-web-page"></a>Создание веб-страницы Оффицеассигнментс

Создайте новую веб-страницу, использующую главную страницу *site. master* и назовите ее *оффицеассигнментс. aspx*. Добавьте следующую разметку в элемент управления `Content` с именем `Content2`:

[!code-aspx[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample13.aspx)]

Обратите внимание, что в атрибуте `DataKeyNames` разметка определяет свойство `Timestamp`, а также ключ записи (`InstructorID`). Указание свойств в атрибуте `DataKeyNames` приводит к тому, что элемент управления сохраняет их в состоянии элемента управления (похожем на состояние представления), чтобы исходные значения были доступны во время обработки обратной передачи.

Если вы не сохранили `Timestamp` значение, Entity Framework не будет иметь его в предложении `Where` команды SQL `Update`. Следовательно, для обновления ничего не найдено. В результате Entity Framework будет вызывать исключение оптимистичного параллелизма каждый раз при обновлении сущности `OfficeAssignment`.

Откройте *OfficeAssignments.aspx.CS* и добавьте следующую инструкцию `using` для уровня доступа к данным:

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample14.cs)]

Добавьте следующий метод `Page_Init`, который включает функции платформа динамических данных. Также добавьте следующий обработчик для события `Updated` элемента управления `ObjectDataSource`, чтобы проверить наличие ошибок параллелизма:

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample15.cs)]

### <a name="testing-optimistic-concurrency-in-the-officeassignments-page"></a>Тестирование оптимистичного параллелизма на странице Оффицеассигнментс

Запустите страницу *оффицеассигнментс. aspx* .

[![Image10](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image32.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image31.png)

Нажмите кнопку **изменить** в строке и измените значение в столбце **Расположение** .

[![Image11](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image34.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image33.png)

Откройте новое окно браузера и снова запустите страницу (скопируйте URL-адрес из первого окна браузера во второе окно браузера).

[![Image10](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image36.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image35.png)

Нажмите кнопку **изменить** в той же строке, которая была изменена ранее, и измените значение **расположения** на другое.

[![Image12](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image38.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image37.png)

Во втором окне браузера нажмите кнопку **Обновить**.

[![Image13](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image40.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image39.png)

Перейдите в первое окно браузера и нажмите кнопку **Обновить**.

[![Image15](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image42.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image41.png)

Вы увидите сообщение об ошибке, и значение **расположения** было изменено, чтобы отобразить значение, которое вы изменили, во втором окне браузера.

## <a name="handling-concurrency-with-the-entitydatasource-control"></a>Обработка параллелизма с помощью элемента управления EntityDataSource

Элемент управления `EntityDataSource` включает встроенную логику, которая распознает параметры параллелизма в модели данных и соответствующим образом обрабатывает операции обновления и удаления. Однако, как и в случае с любыми исключениями, необходимо вручную Обрабатывайте исключения `OptimisticConcurrencyException`, чтобы предоставить понятное пользователю сообщение об ошибке.

Далее предстоит настроить страницу *Courses. aspx* (которая использует элемент управления `EntityDataSource`), чтобы разрешить операции обновления и удаления, а также отобразить сообщение об ошибке при возникновении конфликта параллелизма. Сущность `Course` не имеет столбца отслеживания параллелизма, поэтому вы будете использовать тот же метод, что и для сущности `Department`: отслеживайте значения всех неключевых свойств.

Откройте файл *счулмодел. EDMX* . Для свойств, не являющихся ключевыми `Course` сущности (`Title`, `Credits`и `DepartmentID`), задайте для свойства **режим параллелизма** значение `Fixed`. Затем сохраните и закройте модель данных.

Откройте страницу *Courses. aspx* и внесите следующие изменения:

- В элементе управления `CoursesEntityDataSource` добавьте атрибуты `EnableUpdate="true"` и `EnableDelete="true"`. Открывающий тег для этого элемента управления теперь напоминает следующий пример:

    [!code-aspx[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample16.aspx)]
- В элементе управления `CoursesGridView` измените значение атрибута `DataKeyNames` на `"CourseID,Title,Credits,DepartmentID"`. Затем добавьте элемент `CommandField` в элемент `Columns`, в котором отображаются кнопки " **изменить** " и " **удалить** " (`<asp:CommandField ShowEditButton="True" ShowDeleteButton="True" />`). Элемент управления `GridView` теперь напоминает следующий пример:

    [!code-aspx[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample17.aspx)]

Запустите страницу и создайте ситуацию конфликта, как раньше, на странице отделы. Запустите страницу в двух окнах браузера, щелкните **изменить** в той же строке в каждом окне и внесите различные изменения в каждом из них. Щелкните **Обновить** в одном окне, а затем нажмите кнопку **Обновить** в другом окне. При нажатии кнопки **Обновить** во второй раз отображается страница ошибки, которая возникает из-за необработанного исключения параллелизма.

[![Image22](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image44.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image43.png)

Эту ошибку можно обработать так же, как она была обработана для элемента управления `ObjectDataSource`. Откройте страницу *Courses. aspx* и в элементе управления `CoursesEntityDataSource` укажите обработчики событий `Deleted` и `Updated`. Открывающий тег элемента управления теперь напоминает следующий пример:

[!code-aspx[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample18.aspx)]

Перед элементом управления `CoursesGridView` добавьте следующий элемент управления `ValidationSummary`:

[!code-aspx[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample19.aspx)]

В *Courses.aspx.CS*добавьте оператор `using` для пространства имен `System.Data`, добавьте метод, проверяющий исключения параллелизма, и добавьте обработчики для обработчиков `Updated` и `Deleted` элемента управления `EntityDataSource`. Код будет выглядеть следующим образом:

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample20.cs)]

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample21.cs)]

Единственное различие между этим кодом и тем, что было сделано для элемента управления `ObjectDataSource`, заключается в том, что в данном случае исключение параллелизма находится в свойстве `Exception` объекта аргументов события, а не в свойстве `InnerException` этого исключения.

Запустите страницу и снова создайте конфликт параллелизма. На этот раз отображается сообщение об ошибке:

[![Image23](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image46.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image45.png)

На этом заканчивается введение в обработку конфликтов параллелизма. В следующем руководстве приведены рекомендации по повышению производительности веб-приложения, использующего Entity Framework.

> [!div class="step-by-step"]
> [Назад](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering.md)
> [Вперед](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application.md)
