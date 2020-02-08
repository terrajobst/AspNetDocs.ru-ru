---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application
title: Обработка параллелизма с помощью Entity Framework в приложении ASP.NET MVC (7 из 10) | Документация Майкрософт
author: tdykstra
description: Пример веб-приложения Contoso университета демонстрирует создание приложений ASP.NET MVC 4 с помощью Entity Framework 5 Code First и Visual Studio...
ms.author: riande
ms.date: 07/30/2013
ms.assetid: b83f47c4-8521-4d0a-8644-e8f77e39733e
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 9800a313879477f36a730e6a70c79bc06d403ae3
ms.sourcegitcommit: e365196c75ce93cd8967412b1cfdc27121816110
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/07/2020
ms.locfileid: "77074960"
---
# <a name="handling-concurrency-with-the-entity-framework-in-an-aspnet-mvc-application-7-of-10"></a>Обработка параллелизма с помощью Entity Framework в приложении ASP.NET MVC (7 из 10)

от [Tom Dykstra)](https://github.com/tdykstra)

[Скачать завершенный проект](https://code.msdn.microsoft.com/Getting-Started-with-dd0e2ed8)

> Пример веб-приложения Contoso университета демонстрирует создание приложений ASP.NET MVC 4 с помощью Entity Framework 5 Code First и Visual Studio 2012. Сведения о серии руководств см. в [первом руководстве серии](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md). Вы можете начать серию руководств с начала или [скачать начальный проект для этой главы](building-the-ef5-mvc4-chapter-downloads.md) и начать отсюда.
> 
> > [!NOTE] 
> > 
> > Если проблема не устранена, [Скачайте готовую главу](building-the-ef5-mvc4-chapter-downloads.md) и попытайтесь воспроизвести проблему. Как правило, решение проблемы можно найти, сравнив код с завершенным кодом. Некоторые распространенные ошибки и способы их устранения см. в разделе [ошибки и обходные пути.](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)

В предыдущих двух руководствах вы работали с взаимосвязанными данными. В этом руководстве показано, как управлять параллелизмом. Вы создадите веб-страницы, работающие с сущностью `Department`, а страницы, которые редактируют и удаляют `Department` сущности, будут справляться с ошибками параллелизма. На следующих иллюстрациях показаны страницы индексов и удаления, включая некоторые сообщения, отображаемые при возникновении конфликта параллелизма.

![Department_Index_page_before_edits](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)

![Department_Edit_page_2_after_clicking_Save](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image2.png)

## <a name="concurrency-conflicts"></a>Конфликты параллелизма

Конфликт параллелизма возникает, когда один пользователь отображает данные сущности, чтобы изменить их, а другой пользователь обновляет данные той же сущности до того, как изменение первого пользователя будет записано в базу данных. Если не включить обнаружение таких конфликтов, то пользователь, обновляющий базу данных последним, перезаписывает изменения другого пользователя. Во многих приложениях такой риск допустим: при небольшом числе пользователей или обновлений, а также в случае, если перезапись некоторых изменений не является критической, стоимость реализации параллелизма может перевесить его преимущества. В этом случае вам не нужно настраивать приложение для обработки конфликтов параллелизма.

### <a name="pessimistic-concurrency-locking"></a>Пессимистичный параллелизм (блокировка)

Если приложению нужно предотвратить случайную потерю данных в сценариях параллелизма, одним из способов сделать это являются блокировки базы данных. Это называется *пессимистичным параллелизмом*. Например, перед чтением строки из базы данных вы запрашиваете блокировку для доступа для обновления или только для чтения. Если заблокировать строку для обновления, другие пользователи не могут заблокировать ее для обновления или только для чтения, так как получат копию данных, которые находятся в процессе изменения. Если заблокировать строку только для чтения, другие пользователи также могут заблокировать ее только для чтения, но не для обновления.

Управление блокировками имеет недостатки. Оно может оказаться сложным с точки зрения программирования. Он требует значительных ресурсов управления базами данных и может вызвать проблемы с производительностью по мере увеличения числа пользователей приложения (то есть оно не масштабируется). Поэтому не все системы управления базами данных поддерживают пессимистичный параллелизм. Entity Framework не предоставляет встроенную поддержку для нее, и в этом руководстве не показано, как его реализовать.

### <a name="optimistic-concurrency"></a>Оптимистический параллелизм

Альтернативой пессимистичному параллелизму является *оптимистичный параллелизм*. Оптимистическая блокировка допускает появление конфликтов параллелизма, а затем обрабатывает их соответствующим образом. Например, Джон запускает страницу редактирования отделы, изменяет сумму **бюджета** для английского отдела с $350 000,00 на $0,00.

![Changing_English_dept_budget_to_100000](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image3.png)

Прежде чем Джон нажмет кнопку " **сохранить**", Мария выполняет ту же страницу и изменит поле " **Дата начала** " с 9/1/2007 на 8/8/2013.

![Changing_English_dept_start_date_to_1999](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image4.png)

Джон щелкает " **сохранить** " и видит свое изменение при возврате браузера на страницу индекса, затем Джейн щелкает **Save (сохранить**). Дальнейший ход событий определяется порядком обработки конфликтов параллелизма. Некоторые параметры перечислены ниже:

- Вы можете отслеживать, для какого свойства пользователь изменил и обновил только соответствующие столбцы в базе данных. В этом примере сценария данные не будут потеряны, так как эти два пользователя обновляли разные свойства. В следующий раз, когда кто-то просматривает англоязычный отдел, он увидит изменения в Джон и Мария — дату начала 8/8/2013 и бюджет на нуль долларов.

    Этот метод обновления помогает снизить число конфликтов, которые могут привести к потере данных, но не позволяет избежать такой потери, когда конкурирующие изменения вносятся в одно свойство сущности. То, работает ли Entity Framework в таком режиме, зависит от того, как вы реализуете код обновления. В веб-приложении это часто нецелесообразно, так как может потребоваться обрабатывать большой объем состояний, чтобы отслеживать все исходные значения свойств для сущности, а также новые значения. Поддержание большого количества состояний может повлиять на производительность приложения, так как требует наличия ресурсов сервера или должна быть включена в саму веб-страницу (например, в скрытых полях).
- Вы можете позволить Марии изменить перезапись изменений Джон. В следующий раз, когда кто-то просматривает английский язык, он увидит 8/8/2013 и восстановленное значение $350 000,00. Такой подход называется *победой клиента* или *сохранением последнего внесенного изменения*. (Значения клиента имеют приоритет над тем, что есть в хранилище данных.) Как отмечалось в разделе Введение в этот раздел, если вы не выполняете кодирование для обработки параллелизма, это происходит автоматически.
- Вы можете предотвратить обновление Марии в базе данных. Как правило, выводится сообщение об ошибке, отображается его текущее состояние и пользователь может повторно применить изменения, если он по-прежнему хочет сделать это. Это называется *победой хранилища*. (Значения в хранилище данных имеют приоритет над значениями, отправленными клиентом.) В этом руководстве вы реализуете сценарий Store WINS. Данный метод гарантирует, что никакие изменения не перезаписываются без оповещения пользователя о случившемся.

### <a name="detecting-concurrency-conflicts"></a>Обнаружение конфликтов параллелизма

Можно разрешить конфликты, обрабатывая исключения [оптимистикконкурренциексцептион](https://msdn.microsoft.com/library/system.data.optimisticconcurrencyexception.aspx) , которые создает Entity Framework. Чтобы определить, когда именно нужно выдавать исключения, платформа Entity Framework должна быть в состоянии обнаруживать конфликты. Поэтому нужно соответствующим образом настроить базу данных и модель данных. Ниже приведены некоторые варианты для реализации обнаружения конфликтов:

- Включите в таблицу базы данных столбец отслеживания, который позволяет определять, когда была изменена строка. Затем можно настроить Entity Framework, чтобы включить этот столбец в предложение `Where` команд SQL `Update` или `Delete`.

    Тип данных столбца отслеживания обычно равен [rowversion](https://msdn.microsoft.com/library/ms182776(v=sql.110).aspx). Значение [rowversion](https://msdn.microsoft.com/library/ms182776(v=sql.110).aspx) — это порядковый номер, увеличивающийся при каждом обновлении строки. В команде `Update` или `Delete` предложение `Where` включает исходное значение столбца отслеживания (версия исходной строки). Если обновляемая строка была изменена другим пользователем, значение в столбце `rowversion` отличается от исходного значения, поэтому инструкция `Update` или `Delete` не может найти обновляемую строку из-за предложения `Where`. Когда Entity Framework обнаружит, что ни одна из строк не была обновлена командой `Update` или `Delete` (т. е. Если число затронутых строк равно нулю), это интерпретируется как конфликт параллелизма.
- Настройте Entity Framework, чтобы включить исходные значения каждого столбца в таблице в предложении `Where` для команд `Update` и `Delete`.

    Как и в первом случае, если при первом чтении строки было изменено какое-либо значение в строке, предложение `Where` не вернет строку для обновления, которая Entity Framework интерпретируется как конфликт параллелизма. Для таблиц базы данных, имеющих много столбцов, этот подход может привести к созданию очень больших `Where` предложений и может потребовать, чтобы вы поддерживали большие объемы состояний. Как отмечалось ранее, поддержание большого количества состояний может повлиять на производительность приложения, так как оно требует наличия ресурсов сервера или должно быть указано на самой веб-странице. Поэтому этот подход обычно не рекомендуется, и он не является методом, используемым в этом руководстве.

    Если вы хотите реализовать этот подход к параллелизму, необходимо пометить все свойства, не являющиеся первичными ключами, в сущности, для которой необходимо отслеживание параллелизма, добавив к ним атрибут [ConcurrencyCheck](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.concurrencycheckattribute.aspx) . Это изменение позволяет Entity Framework включить все столбцы в предложение SQL `WHERE` инструкций `UPDATE`.

В оставшейся части этого учебника вы добавите свойство отслеживания [rowversion](https://msdn.microsoft.com/library/ms182776(v=sql.110).aspx) в сущность `Department`, создадите контроллер и представления и проверите, правильно ли работает все.

## <a name="add-an-optimistic-concurrency-property-to-the-department-entity"></a>Добавление свойства оптимистичного параллелизма в сущность Department

В *моделс\департмент.КС*добавьте свойство отслеживания с именем `RowVersion`.

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs?highlight=18-19)]

Атрибут [timestamp](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.timestampattribute.aspx) указывает, что этот столбец будет включаться в предложение `Where` `Update` и `Delete` команды, отправляемые в базу данных. Атрибут называется [меткой времени](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.timestampattribute.aspx) , так как предыдущие версии SQL Server использовали тип данных [timestamp](https://msdn.microsoft.com/library/ms182776(v=SQL.90).aspx) SQL до того, как он заменил значение [rowversion](https://msdn.microsoft.com/library/ms182776(v=sql.110).aspx) SQL. Тип .NET для `rowversion` является массивом байтов. Если вы предпочитаете использовать API Fluent, можно использовать метод [исконкурренцитокен](https://msdn.microsoft.com/library/gg679501(v=VS.103).aspx) для указания свойства отслеживания, как показано в следующем примере:

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]

См. статью о проблемах с GitHub [замените исконкурренцитокен на исровверсион](https://github.com/aspnet/AspNetDocs/issues/302).

Добавив свойство, вы изменили модель базы данных, поэтому нужно выполнить еще одну миграцию. Введите в консоли диспетчера пакетов (PMC) следующие команды:

[!code-console[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cmd)]

## <a name="create-a-department-controller"></a>Создание контроллера отдела

Создайте контроллер `Department` и представления так же, как и другие контроллеры, используя следующие параметры:

![Add_Controller_dialog_box_for_Department_controller](https://asp.net/media/2578041/Windows-Live-Writer_Handling-C.NET-MVC-Application-7-of-10h1_AFDC_Add_Controller_dialog_box_for_Department_controller_d1d9c788-f970-4d6a-9f5a-1eddc84330b7.png)

В *контроллерс\департментконтроллер.КС*добавьте инструкцию `using`:

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cs)]

Измените «LastName» на «FullName» везде в этом файле (четыре вхождения), чтобы раскрывающиеся списки администратора отдела содержали полное имя инструктора, а не только фамилию.

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cs?highlight=1)]

Замените существующий код для метода `HttpPost` `Edit` следующим кодом:

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.cs)]

Представление будет хранить исходное значение `RowVersion` в скрытом поле. Когда связыватель модели создает `department` экземпляр, этот объект будет иметь исходное значение свойства `RowVersion` и новые значения для других свойств, введенные пользователем на странице редактирования. Затем, когда Entity Framework создает команду SQL `UPDATE`, эта команда будет включать предложение `WHERE`, которое ищет строку с исходным значением `RowVersion`.

Если команда `UPDATE` не затрагивает ни одной строки (ни одна из строк не имеет исходного значения `RowVersion`), Entity Framework создает исключение `DbUpdateConcurrencyException`, а код в блоке `catch` получает затронутую `Department` сущность из объекта исключения. Эта сущность имеет оба значения, считанные из базы данных, и новые значения, введенные пользователем:

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cs)]

Затем код добавляет пользовательское сообщение об ошибке для каждого столбца, в котором значения базы данных отличаются от значений, введенных пользователем на странице редактирования.

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.cs)]

В более длинном сообщении об ошибке объясняется, что произошло и что делать с ним:

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample9.cs)]

Наконец, код устанавливает `RowVersion` значение объекта `Department` в новое значение, полученное из базы данных. Это новое значение `RowVersion` будет сохранено в скрытом поле при повторном отображении страницы "Edit" (Редактирование). Когда пользователь в следующий раз нажимает кнопку **Save** (Сохранить), перехватываются только те ошибки параллелизма, которые возникли с момента повторного отображения страницы "Edit" (Редактирование).

В *виевс\департмент\едит.кштмл*Добавьте скрытое поле, чтобы сохранить значение свойства `RowVersion`, сразу после скрытого поля для свойства `DepartmentID`:

[!code-cshtml[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample10.cshtml?highlight=17)]

В *виевс\департмент\индекс.кштмл*замените существующий код следующим кодом, чтобы переместить ссылки на строки слева и изменить заголовок страницы и заголовки столбцов для показа `FullName` вместо `LastName` в столбце **администратора** :

[!code-cshtml[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample11.cshtml)]

## <a name="testing-optimistic-concurrency-handling"></a>Тестирование обработки оптимистичного параллелизма

Запустите сайт и щелкните **отделы**:

![Department_Index_page_before_edits](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image5.png)

Щелкните правой кнопкой мыши ссылку **изменить** гиперссылку для Kim аберкромбие и выберите **Открыть в новой вкладке,** а затем щелкните гиперссылку **изменить** для Kim аберкромбие. Эти два окна отображают одну и ту же информацию.

![Department_Edit_page_before_changes](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image6.png)

Измените поле в первом окне браузера и нажмите кнопку **сохранить**.

![Department_Edit_page_1_after_change](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image7.png)

В браузере отображается страница индекса с измененным значением.

![Departments_Index_page_after_first_budget_edit](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image8.png)

Измените любое поле во втором окне браузера и нажмите кнопку **сохранить**.

![Department_Edit_page_2_after_change](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image9.png)

В втором окне браузера нажмите кнопку **сохранить** . Отображается сообщение об ошибке:

![Department_Edit_page_2_after_clicking_Save](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image10.png)

Снова нажмите кнопку **Сохранить**. Значение, введенное во втором браузере, сохраняется вместе с исходным значением данных, измененных в первом браузере. Сохраненные значения отображаются при открытии страницы индекса.

![Department_Index_page_with_change_from_second_browser](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image11.png)

## <a name="updating-the-delete-page"></a>Обновление страницы удаления

Для страницы "Delete" (Удаление) платформа Entity Framework обнаруживает конфликты параллелизма, вызванные схожим изменением кафедры. Когда метод `HttpGet` `Delete` отображает представление подтверждения, представление включает исходное значение `RowVersion` в скрытое поле. Затем это значение доступно для метода `HttpPost` `Delete`, который вызывается, когда пользователь подтверждает удаление. Когда Entity Framework создает команду SQL `DELETE`, она включает предложение `WHERE` с исходным значением `RowVersion`. Если команда приводит к нулевой строке (то есть изменилась строка после отображения страницы подтверждения удаления), возникает исключение параллелизма, а метод `HttpGet Delete` вызывается с флагом ошибки `true`, чтобы отобразить страницу подтверждения с сообщением об ошибке. Также возможно, что было затронуто нулевое число строк, поскольку строка была удалена другим пользователем, поэтому в этом случае отображается другое сообщение об ошибке.

В *DepartmentController.CS*замените метод `HttpGet` `Delete` следующим кодом:

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample12.cs)]

Этот метод принимает необязательный параметр, который указывает, отображается ли страница повторно после ошибки параллелизма. Если этот флаг имеет значение `true`, в представление отправляется сообщение об ошибке с помощью свойства `ViewBag`.

Замените код в методе `HttpPost` `Delete` (с именем `DeleteConfirmed`) следующим кодом:

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample13.cs)]

В шаблонном коде, который вы только что заменили, этот метод принимал только идентификатор записи:

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample14.cs)]

Вы изменили этот параметр на `Department` экземпляр сущности, созданный связывателем модели. Это предоставляет доступ к значению свойства `RowVersion` в дополнение к ключу записи.

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample15.cs)]

Вы также изменили имя метода действия с `DeleteConfirmed` на `Delete`. Шаблонный код с именем `HttpPost` метод `Delete` `DeleteConfirmed`, чтобы присвоить методу `HttpPost` уникальную сигнатуру. (Среда CLR требует, чтобы перегруженные методы имели различные параметры метода.) Теперь, когда сигнатуры уникальны, можно придерживаться соглашения MVC и использовать одно и то же имя для методов `HttpPost` и `HttpGet` DELETE.

При перехвате ошибки параллелизма код повторно отображает страницу подтверждения удаления и предоставляет флаг, указывающий, что нужно отобразить сообщение об ошибке параллелизма.

В *виевс\департмент\делете.кштмл*замените сформированный код следующим кодом, который вносит некоторые изменения в форматирование и добавляет поле сообщения об ошибке. Изменения выделены.

[!code-cshtml[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample16.cshtml?highlight=9,37,40,45-46)]

Этот код добавляет сообщение об ошибке между заголовками `h2` и `h3`:

[!code-cshtml[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample17.cshtml)]

Он заменяет `LastName` `FullName` в поле `Administrator`:

[!code-cshtml[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample18.cshtml)]

Наконец, он добавляет скрытые поля для свойств `DepartmentID` и `RowVersion` после инструкции `Html.BeginForm`:

[!code-cshtml[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample19.cshtml)]

Запустите страницу индекса отделов. Щелкните правой кнопкой мыши гиперссылку **Удалить** для английского Отдела и выберите пункт **Открыть в новом окне,** а затем в первом окне щелкните гиперссылку **изменить** для английского Отдела.

В первом окне измените одно из значений и нажмите кнопку **Save (сохранить** ):

![Department_Edit_page_after_change_before_delete](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image12.png)

Изменение будет подтверждено на странице индекса.

![Departments_Index_page_after_budget_edit_before_delete](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image13.png)

Во втором окне нажмите кнопку **Удалить**.

![Department_Delete_confirmation_page_before_concurrency_error](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image14.png)

Вы видите сообщение об ошибке параллелизма, а значения кафедры обновляются с использованием актуальных сведений из базы данных.

![Department_Delete_confirmation_page_with_concurrency_error](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image15.png)

Если нажать кнопку **Delete** (Удалить) еще раз, вы будете перенаправлены на страницу индекса, которая показывает, что кафедра была удалена.

## <a name="summary"></a>Сводка

На этом заканчивается введение в обработку конфликтов параллелизма. Дополнительные сведения о других способах обработки различных сценариев параллелизма см. в статье [шаблоны оптимистического параллелизма](https://blogs.msdn.com/b/adonet/archive/2011/02/03/using-dbcontext-in-ef-feature-ctp5-part-9-optimistic-concurrency-patterns.aspx) и [Работа со значениями свойств](https://blogs.msdn.com/b/adonet/archive/2011/01/30/using-dbcontext-in-ef-feature-ctp5-part-5-working-with-property-values.aspx) в блоге Entity Framework Team. В следующем учебнике показано, как реализовать наследование "один таблица на иерархию" для сущностей `Instructor` и `Student`.

Ссылки на другие ресурсы Entity Framework можно найти в [карте содержимого ASP.NET Data Access](../../../../whitepapers/aspnet-data-access-content-map.md).

> [!div class="step-by-step"]
> [Назад](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)
> [Вперед](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application.md)
