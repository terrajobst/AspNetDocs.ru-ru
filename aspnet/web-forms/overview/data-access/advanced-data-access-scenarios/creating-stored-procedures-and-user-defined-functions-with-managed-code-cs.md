---
uid: web-forms/overview/data-access/advanced-data-access-scenarios/creating-stored-procedures-and-user-defined-functions-with-managed-code-cs
title: Создание хранимых процедур и определяемых пользователем функций с помощью управляемого кода (C#) | Документация Майкрософт
author: rick-anderson
description: Microsoft SQL Server 2005 интегрируется с общеязыковой средой выполнения .NET и позволяет разработчикам создавать объекты базы данных с помощью управляемого кода. Этот учебник...
ms.author: riande
ms.date: 08/03/2007
ms.assetid: 213eea41-1ab4-4371-8b24-1a1a66c515de
msc.legacyurl: /web-forms/overview/data-access/advanced-data-access-scenarios/creating-stored-procedures-and-user-defined-functions-with-managed-code-cs
msc.type: authoredcontent
ms.openlocfilehash: c6aec9ca70fe3ab568b3d17fea6bfd56671edc03
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/28/2019
ms.locfileid: "74605405"
---
# <a name="creating-stored-procedures-and-user-defined-functions-with-managed-code-c"></a>Создание хранимых процедур и определяемых пользователем функций с помощью управляемого кода (C#)

по [Скотт Митчелл](https://twitter.com/ScottOnWriting)

[Скачать код](https://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_75_CS.zip) или [скачать PDF](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/datatutorial75cs1.pdf)

> Microsoft SQL Server 2005 интегрируется с общеязыковой средой выполнения .NET и позволяет разработчикам создавать объекты базы данных с помощью управляемого кода. В этом руководстве показано, как создавать управляемые хранимые процедуры и управляемые определяемые пользователем функции с помощью C# Visual Basic или кода. Также показано, как эти выпуски Visual Studio позволяют отлаживать такие управляемые объекты базы данных.

## <a name="introduction"></a>Введение

Базы данных, например Microsoft s SQL Server 2005, используют [Transact-язык SQL (T-SQL)](http://en.wikipedia.org/wiki/Transact-SQL) для вставки, изменения и извлечения данных. Большинство систем баз данных включают конструкции для группирования ряда инструкций SQL, которые затем можно выполнять в виде одной многократно используемой единицы. Хранимые процедуры являются одним из примеров. Другой — *определяемые пользователем функции*(UDF) — конструкция, которая будет рассмотрена более подробно на шаге 9.

По сути, SQL предназначен для работы с наборами данных. Операторы `SELECT`, `UPDATE`и `DELETE` по сути применяются ко всем записям в соответствующей таблице и ограничиваются только их предложениями `WHERE`. Однако существует множество функций языка, предназначенных для работы с одной записью за раз и для манипулирования скалярными данными. [`CURSOR` s](http://www.sqlteam.com/item.asp?ItemID=553) позволяют циклически выполнять цикл по одному набору записей за раз. Функции обработки строк, такие как `LEFT`, `CHARINDEX`и `PATINDEX`, работают с скалярными данными. SQL также включает в себя инструкции потока управления, такие как `IF` и `WHILE`.

До Microsoft SQL Server 2005 хранимые процедуры и определяемые пользователем функции можно определить только как коллекцию инструкций T-SQL. Однако SQL Server 2005 была разработана для интеграции [со средой CLR, которая](https://msdn.microsoft.com/netframework/aa497266.aspx)является средой выполнения, используемой всеми сборками .NET. Следовательно, хранимые процедуры и UDF в базе данных SQL Server 2005 можно создать с помощью управляемого кода. То есть хранимую процедуру или определяемую пользователем функцию можно создать как метод в C# классе. Это позволяет этим хранимым процедурам и функциям UDF использовать функции в .NET Framework и из собственных пользовательских классов.

В этом учебнике мы рассмотрим, как создавать управляемые хранимые процедуры и определяемые пользователем функции и как интегрировать их в базу данных Northwind. Давайте приступим к работе!

> [!NOTE]
> Управляемые объекты базы данных имеют некоторые преимущества по сравнению с аналогами SQL. Основные преимущества языка и возможности повторного использования существующего кода и логики. Однако управляемые объекты базы данных, скорее всего, будут менее эффективными при работе с наборами данных, которые не требуют значительной процедурной логики. Более подробное обсуждение преимуществ использования управляемого кода и T-SQL см. в статье [преимущества использования управляемого кода для создания объектов базы данных](https://msdn.microsoft.com/library/k2e1fb36(VS.80).aspx).

## <a name="step-1-moving-the-northwind-database-out-ofapp_data"></a>Шаг 1. Перемещение базы данных Northwind из`App_Data`

Все наши учебники, таким образом, использовали файл базы данных Microsoft SQL Server 2005 Express Edition в папке `App_Data` веб-приложений. Размещение базы данных в `App_Data` упрощенное распространение и запуск этих учебников, так как все файлы были размещены в одном каталоге и не требуют дополнительных действий по настройке для тестирования учебника.

Однако в этом руководстве мы можем переместить базу данных Northwind из `App_Data` и явно зарегистрировать ее в экземпляре базы данных SQL Server 2005, экспресс-выпуск. Хотя мы можем выполнить действия, описанные в этом руководстве, с базой данных в папке `App_Data`, несколько шагов значительно упрощаются путем явной регистрации базы данных в экземпляре базы данных SQL Server 2005, экспресс-выпуск.

В загружаемом файле для этого учебника имеются два файла базы данных — `NORTHWND.MDF` и `NORTHWND_log.LDF` расположены в папке с именем `DataFiles`. Если вы используете собственную реализацию руководств, закройте Visual Studio и переместите `NORTHWND.MDF` и `NORTHWND_log.LDF` файлы из папки веб-сайта s `App_Data` в папку за пределами веб-сайта. После перемещения файлов базы данных в другую папку необходимо зарегистрировать базу данных Northwind в экземпляре базы данных SQL Server 2005, экспресс-выпуск. Это можно сделать в SQL Server Management Studio. Если на компьютере установлен выпуск, отличный от Express, SQL Server 2005, вероятно, у вас уже установлена Management Studio. Если на компьютере имеется только SQL Server 2005, экспресс-выпуск, загрузите и установите [Microsoft SQL Server Management Studio Express](https://www.microsoft.com/downloads/details.aspx?displaylang=en&amp;FamilyID=C243A5AE-4BD1-4E3D-94B8-5A0F62BF7796).

Запустите приложение SQL Server Management Studio. Как показано на рис. 1, Management Studio начинается с запроса сервера, к которому нужно подключиться. Введите Локалхост\склекспресс в поле имя сервера, выберите Проверка подлинности Windows в раскрывающемся списке Проверка подлинности и нажмите кнопку Подключить.

![Подключение к соответствующему экземпляру базы данных](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image1.png)

**Рис. 1**. подключение к соответствующему экземпляру базы данных

После подключения в окне обозревателя объектов будут перечислены сведения об экземпляре базы данных SQL Server 2005, экспресс-выпуск, включая его базы данных, сведения о безопасности, параметры управления и т. д.

Необходимо присоединить базу данных Northwind в папке `DataFiles` (или в любом месте, где она была перемещена) в экземпляр базы данных SQL Server 2005, экспресс-выпуск. Щелкните правой кнопкой мыши папку базы данных и выберите пункт Присоединить в контекстном меню. Откроется диалоговое окно Присоединение баз данных. Нажмите кнопку "Добавить", выполните детализацию до соответствующего файла `NORTHWND.MDF` и нажмите кнопку "ОК". На этом этапе экран должен выглядеть примерно так, как показано на рис. 2.

[![подключиться к соответствующему экземпляру базы данных](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image3.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image2.png)

**Рис. 2**. подключение к соответствующему экземпляру базы данных ([щелкните, чтобы просмотреть изображение с полным размером](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image4.png))

> [!NOTE]
> При подключении к экземпляру SQL Server 2005, экспресс-выпуск через Management Studio диалоговое окно Присоединение баз данных не позволяет выполнять детализацию в каталогах профилей пользователей, таких как мои документы. Поэтому не забудьте поместить файлы `NORTHWND.MDF` и `NORTHWND_log.LDF` в каталог профиля, не относящийся к пользователю.

Нажмите кнопку ОК, чтобы присоединить базу данных. Диалоговое окно Присоединение баз данных закроется, и в обозревателе объектов появится список только что подключенной базы данных. Вероятно, база данных Northwind имеет такое же имя, как `9FE54661B32FDD967F51D71D0D5145CC_LINE ARTICLES\DATATUTORIALS\VOLUME 3\CSHARP\73\ASPNET_DATA_TUTORIAL_75_CS\APP_DATA\NORTHWND.MDF`. Переименуйте базу данных в Northwind, щелкнув ее правой кнопкой мыши и выбрав пункт Переименовать.

![Переименование базы данных в Northwind](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image5.png)

**Рис. 3**. Переименование базы данных в Northwind

## <a name="step-2-creating-a-new-solution-and-sql-server-project-in-visual-studio"></a>Шаг 2. Создание нового решения и SQL Server проекта в Visual Studio

Для создания управляемых хранимых процедур или определяемых пользователем функций в SQL Server 2005 мы будем писать хранимую процедуру C# и логику UDF в виде кода в классе. После написания кода необходимо скомпилировать этот класс в сборку (файл `.dll`), зарегистрировать сборку в базе данных SQL Server, а затем создать хранимую процедуру или объект UDF в базе данных, которая указывает на соответствующий метод в сборке. Эти действия можно выполнить вручную. Мы можем создать код в любом текстовом редакторе, скомпилировать его из командной строки с помощью C# компилятора ([`csc.exe`](https://msdn.microsoft.com/library/ms379563(vs.80).aspx)), зарегистрировать его в базе данных с помощью команды [`CREATE ASSEMBLY`](https://msdn.microsoft.com/library/ms189524.aspx) или из Management Studio и добавить хранимую процедуру или объект UDF с помощью аналогичных средств. К счастью, в версии Professional и Team Systems Visual Studio входит SQL Server тип проекта, который автоматизирует эти задачи. В этом учебнике мы рассмотрим использование типа проекта SQL Server для создания управляемой хранимой процедуры и определяемой пользователем функции.

> [!NOTE]
> Если вы используете Visual Web Developer или стандартный выпуск Visual Studio, то вместо этого придется использовать ручной подход. На шаге 13 приведены подробные инструкции по выполнению этих шагов вручную. Я рекомендую прочесть шаги с 2 по 12, прежде чем считывать шаг 13, так как эти шаги содержат важные SQL Server инструкции по настройке, которые необходимо применить независимо от используемой версии Visual Studio.

Для начала откройте Visual Studio. В меню Файл выберите пункт Создать проект, чтобы открыть диалоговое окно Новый проект (см. рис. 4). Выполните детализацию до типа проекта базы данных, а затем в шаблонах, перечисленных справа, выберите Создание нового SQL Server проекта. Я решил назвать этот проект `ManagedDatabaseConstructs` и поместил его в решение с именем `Tutorial75`.

[![создать новый проект SQL Server](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image7.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image6.png)

**Рис. 4**. Создание нового проекта SQL Server ([щелкните, чтобы просмотреть изображение с полным размером](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image8.png))

Нажмите кнопку ОК в диалоговом окне Новый проект, чтобы создать решение и SQL Server проект.

Проект SQL Server привязан к определенной базе данных. Следовательно, после создания нового проекта SQL Server мы сразу же запросили указать эти сведения. На рис. 5 показано диалоговое окно Создание ссылки на базу данных, которое было заполнено, чтобы указать базу данных Northwind, зарегистрированную в SQL Server 2005, экспресс-выпуск экземпляре базы данных на шаге 1.

![Связывание проекта SQL Server с базой данных "Борей"](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image9.png)

**Рис. 5**. связывание SQL Server проекта с базой данных «Борей»

Чтобы выполнить отладку управляемых хранимых процедур и определяемых пользователем функций, которые будут созданы в рамках этого проекта, необходимо включить поддержку отладки SQL/CLR для подключения. При каждом связывании SQL Server проекта с новой базой данных (как мы делали на рис. 5) Visual Studio запрашивает у нас необходимость включить отладку SQL/CLR для подключения (см. рис. 6). Щелкните Да.

![Включить отладку SQL/CLR](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image10.png)

**Рис. 6**. Включение отладки SQL/CLR

На этом этапе в решение добавлен новый проект SQL Server. Он содержит папку с именем `Test Scripts` и файл с именем `Test.sql`, который используется для отладки управляемых объектов базы данных, созданных в проекте. Мы рассмотрим отладку на шаге 12.

Теперь мы можем добавить в этот проект новые управляемые хранимые процедуры и определяемые пользователем функции, но перед тем как мы добавим в решение существующее веб-приложение. В меню Файл выберите пункт Добавить и выберите существующий веб-сайт. Перейдите к соответствующей папке веб-сайта и нажмите кнопку ОК. Как показано на рис. 7, это приведет к обновлению решения для включения двух проектов: веб-сайта и `ManagedDatabaseConstructs` SQL Server проекта.

![обозреватель решений теперь содержит два проекта](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image11.png)

**Рис. 7**. Обозреватель решений теперь содержит два проекта

Значение `NORTHWNDConnectionString` в `Web.config` в данный момент ссылается на файл `NORTHWND.MDF` в папке `App_Data`. Так как мы удалили эту базу данных из `App_Data` и явно зарегистрировали ее в экземпляре SQL Server 2005, экспресс-выпуск базы данных, необходимо соответствующим образом обновить значение `NORTHWNDConnectionString`. Откройте файл `Web.config` на веб-сайте и измените значение `NORTHWNDConnectionString`, чтобы строка подключения была прочитана: `Data Source=localhost\SQLExpress;Initial Catalog=Northwind;Integrated Security=True`. После этого изменения `<connectionStrings>` раздел в `Web.config` должен выглядеть следующим образом:

[!code-xml[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample1.xml)]

> [!NOTE]
> Как обсуждалось в [предыдущем руководстве](debugging-stored-procedures-cs.md), при отладке SQL Server объекта из клиентского приложения, например веб-сайта ASP.NET, необходимо отключить пулы подключений. Приведенная выше строка подключения отключает пулы соединений (`Pooling=false`). Если вы не планируете выполнять отладку управляемых хранимых процедур и определяемых пользователем функций с веб-сайта ASP.NET, включите пулы подключений.

## <a name="step-3-creating-a-managed-stored-procedure"></a>Шаг 3. Создание управляемой хранимой процедуры

Чтобы добавить управляемую хранимую процедуру в базу данных Northwind, сначала необходимо создать хранимую процедуру как метод в проекте SQL Server. В обозреватель решений щелкните правой кнопкой мыши имя проекта `ManagedDatabaseConstructs` и выберите Добавить новый элемент. Откроется диалоговое окно Добавление нового элемента, в котором перечислены типы управляемых объектов базы данных, которые могут быть добавлены в проект. Как показано на рис. 8, сюда входят хранимые процедуры и определяемые пользователем функции, а также другие.

Начнем с добавления хранимой процедуры, которая просто возвращает все продукты, которые больше не поддерживаются. Присвойте новому файлу хранимой процедуры имя `GetDiscontinuedProducts.cs`.

[![добавить новую хранимую процедуру с именем GetDiscontinuedProducts.cs](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image13.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image12.png)

**Рис. 8**. Добавление новой хранимой процедуры с именем `GetDiscontinuedProducts.cs` ([щелкните, чтобы просмотреть изображение с полным размером](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image14.png))

Будет создан новый C# файл класса со следующим содержимым:

[!code-csharp[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample2.cs)]

Обратите внимание, что хранимая процедура реализована как метод `static` в `partial`ном файле класса с именем `StoredProcedures`. Более того, метод `GetDiscontinuedProducts` дополнен `SqlProcedure attribute`, который помечает метод как хранимую процедуру.

Следующий код создает объект `SqlCommand` и задает для его `CommandText` запрос `SELECT`, который возвращает все столбцы таблицы `Products` для продуктов, `Discontinued` поле которых равно 1. Затем он выполняет команду и отправляет результаты обратно клиентскому приложению. Добавьте этот код в метод `GetDiscontinuedProducts`.

[!code-csharp[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample3.cs)]

Все управляемые объекты базы данных имеют доступ к [`SqlContext` объекту](https://msdn.microsoft.com/library/ms131108.aspx) , представляющему контекст вызывающего объекта. `SqlContext` предоставляет доступ к [объекту`SqlPipe`](https://msdn.microsoft.com/library/microsoft.sqlserver.server.sqlpipe.aspx) через его [свойство`Pipe`](https://msdn.microsoft.com/library/microsoft.sqlserver.server.sqlcontext.pipe.aspx). Этот объект `SqlPipe` используется для паром информации между SQL Server базой данных и вызывающим приложением. Как следует из названия, [метод`ExecuteAndSend`](https://msdn.microsoft.com/library/microsoft.sqlserver.server.sqlpipe.executeandsend.aspx) выполняет переданный объект `SqlCommand` и отправляет результаты обратно клиентскому приложению.

> [!NOTE]
> Управляемые объекты базы данных лучше всего подходят для хранимых процедур и пользовательских функций, использующих процедурную логику, а не логику на основе наборов. Процедурная логика включает в себя работу с наборами данных на основе строк или работу с скалярными данными. Однако только что созданный метод `GetDiscontinuedProducts` не требует процедурной логики. Таким образом, в идеале он будет реализован как хранимая процедура T-SQL. Он реализуется как управляемая хранимая процедура для демонстрации действий, необходимых для создания и развертывания управляемых хранимых процедур.

## <a name="step-4-deploying-the-managed-stored-procedure"></a>Шаг 4. Развертывание управляемой хранимой процедуры

После выполнения этого кода мы готовы к развертыванию в базе данных Northwind. Развертывание SQL Server проекта компилирует код в сборку, регистрирует сборку в базе данных и создает соответствующие объекты в базе данных, связывая их с соответствующими методами в сборке. Точный набор задач, выполняемых при развертывании, более точно написан на шаге 13. Щелкните правой кнопкой мыши имя проекта `ManagedDatabaseConstructs` в обозреватель решений и выберите пункт Развернуть. Однако развертывание завершается сбоем со следующей ошибкой: неправильный синтаксис рядом с "EXTERNAL". Чтобы включить эту функцию, может потребоваться задать более высокое значение уровня совместимости текущей базы данных. См. справку по `sp_dbcmptlevel`у хранимой процедуры.

Это сообщение об ошибке возникает при попытке зарегистрировать сборку в базе данных Northwind. Чтобы зарегистрировать сборку в базе данных SQL Server 2005, уровень совместимости Database s должен быть равен 90. По умолчанию новые базы данных SQL Server 2005 имеют уровень совместимости 90. Однако базы данных, созданные с помощью Microsoft SQL Server 2000, имеют уровень совместимости по умолчанию 80. Так как база данных Northwind изначально была базой данных Microsoft SQL Server 2000, ее уровень совместимости в настоящее время равен 80, и поэтому его необходимо увеличить до 90, чтобы зарегистрировать управляемые объекты базы данных.

Чтобы обновить уровень совместимости базы данных, откройте новое окно запроса в Management Studio и введите:

[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample4.sql)]

Щелкните значок выполнить на панели инструментов, чтобы выполнить приведенный выше запрос.

[![обновить уровень совместимости базы данных "Борей"](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image16.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image15.png)

**Рис. 9**. обновление уровня совместимости базы данных Northwind ([щелкните, чтобы просмотреть изображение с полным размером](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image17.png))

После обновления уровня совместимости повторно разверните проект SQL Server. На этот раз развертывание должно завершиться без ошибок.

Вернитесь в SQL Server Management Studio, щелкните правой кнопкой мыши базу данных Northwind в обозревателе объектов и выберите команду Обновить. Далее перейдите в папку Программирование, а затем разверните папку сборки. Как показано на рис. 10, база данных Northwind теперь включает сборку, созданную `ManagedDatabaseConstructs` проектом.

![Сборка Манажеддатабасеконструктс теперь зарегистрирована в базе данных "Борей"](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image18.png)

**Рис. 10**. сборка `ManagedDatabaseConstructs` теперь зарегистрирована в базе данных Northwind

Также разверните папку Хранимые процедуры. Там вы увидите хранимую процедуру с именем `GetDiscontinuedProducts`. Эта хранимая процедура была создана процессом развертывания и указывает на метод `GetDiscontinuedProducts` в сборке `ManagedDatabaseConstructs`. При выполнении хранимой процедуры `GetDiscontinuedProducts` она, в свою очередь, выполняет метод `GetDiscontinuedProducts`. Поскольку это управляемая хранимая процедура, ее нельзя изменить с помощью Management Studio (следовательно, значок блокировки рядом с именем хранимой процедуры).

![Хранимая процедура Жетдисконтинуедпродуктс указана в папке хранимых процедур.](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image19.png)

**Рис. 11**. `GetDiscontinuedProducts` хранимая процедура указана в папке хранимых процедур

Прежде чем можно будет вызвать управляемую хранимую процедуру, необходимо преодолеть еще одно препятствие: база данных настроена для предотвращения выполнения управляемого кода. Проверьте это, открыв новое окно запроса и выполнив хранимую процедуру `GetDiscontinuedProducts`. Вы получите следующее сообщение об ошибке: выполнение пользовательского кода в .NET Framework отключено. Параметр конфигурации включения CLR Enabled.

Чтобы просмотреть сведения о конфигурации базы данных Northwind, введите и выполните команду `exec sp_configure` в окне запроса. Это показывает, что параметр clr enabled в настоящее время имеет значение 0.

[![параметр clr enabled в настоящее время имеет значение 0](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image21.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image20.png)

**Рис. 12**. в настоящее время параметр clr enabled имеет значение 0 ([щелкните, чтобы просмотреть изображение с полным размером](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image22.png))

Обратите внимание, что каждый параметр конфигурации на рис. 12 имеет следующие четыре значения: минимальное и максимальное значения, а также конфигурации и значения запуска. Чтобы обновить значение конфигурации для параметра Enabled CLR, выполните следующую команду:

[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample5.sql)]

При повторном запуске `exec sp_configure` вы увидите, что приведенная выше инструкция обновила параметр конфигурации s Enabled CLR в значение 1, но значение запуска по-прежнему равно 0. Чтобы это изменение конфигурации вступило в силу, необходимо выполнить [команду`RECONFIGURE`](https://msdn.microsoft.com/library/ms176069.aspx), которая установит значение параметра Run в текущее значение конфигурации. Просто введите `RECONFIGURE` в окне запроса и щелкните значок выполнить на панели инструментов. Если вы запустите `exec sp_configure` теперь вы увидите значение 1 для конфигурации s с включенной средой CLR и значений запуска.

После завершения настройки с включенной средой CLR мы готовы к запуску хранимой процедуры управляемого `GetDiscontinuedProducts`. В окне запроса введите и выполните команду `exec` `GetDiscontinuedProducts`. Вызов хранимой процедуры приводит к выполнению соответствующего управляемого кода в методе `GetDiscontinuedProducts`. Этот код выдает `SELECT` запрос, возвращающий все продукты, которые больше не поддерживаются, и возвращает эти данные вызывающему приложению, которое SQL Server Management Studio в этом экземпляре. Management Studio получает эти результаты и отображает их в окне результатов.

[![хранимая процедура Жетдисконтинуедпродуктс возвращает все неподдерживаемые продукты](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image24.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image23.png)

**Рис. 13**. `GetDiscontinuedProducts` хранимая процедура возвращает все неподдерживаемые продукты ([щелкните, чтобы просмотреть изображение с полным размером](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image25.png))

## <a name="step-5-creating-managed-stored-procedures-that-accept-input-parameters"></a>Шаг 5. Создание управляемых хранимых процедур, принимающих входные параметры

Многие из запросов и хранимых процедур, созданных в рамках этих учебников, используют *Параметры*. Например, в учебнике [Создание новых хранимых процедур для адаптеров TableAdapter типизированного набора данных](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs.md) мы создали хранимую процедуру с именем `GetProductsByCategoryID`, которая приняла входной параметр с именем `@CategoryID`. Затем хранимая процедура возвращает все продукты, `CategoryID` поле которых соответствует значению заданного параметра `@CategoryID`.

Чтобы создать управляемую хранимую процедуру, которая принимает входные параметры, просто укажите эти параметры в определении метода. Чтобы проиллюстрировать это, добавим еще одну управляемую хранимую процедуру в проект `ManagedDatabaseConstructs` с именем `GetProductsWithPriceLessThan`. Эта управляемая хранимая процедура принимает входной параметр, указывающий цену, и возвращает все продукты, чье `UnitPrice` поле меньше значения параметра s.

Чтобы добавить в проект новую хранимую процедуру, щелкните правой кнопкой мыши имя проекта `ManagedDatabaseConstructs` и выберите Добавить новую хранимую процедуру. Назовите файл `GetProductsWithPriceLessThan.cs`. Как было показано на шаге 3, в результате будет создан новый C# файл класса с методом с именем `GetProductsWithPriceLessThan` помещается в `StoredProcedures``partial` класса.

Обновите определение метода `GetProductsWithPriceLessThan`, чтобы оно принимало [`SqlMoney`](https://msdn.microsoft.com/library/system.data.sqltypes.sqlmoney.aspx) входной параметр с именем `price` и написал код для выполнения и возвращал результаты запроса:

[!code-csharp[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample6.cs)]

Определение и код `GetProductsWithPriceLessThan` метода во многом похожи на определение и код метода `GetDiscontinuedProducts`, созданного на шаге 3. Единственное отличие заключается в том, что метод `GetProductsWithPriceLessThan` принимает в качестве входного параметра (`price`), запрос `SqlCommand` s включает параметр (`@MaxPrice`), а параметр добавляется в коллекцию `SqlCommand` `Parameters`, и ему присваивается значение переменной `price`.

После добавления этого кода повторно разверните проект SQL Server. Затем вернитесь к SQL Server Management Studio и обновите папку хранимых процедур. Вы увидите новую запись, `GetProductsWithPriceLessThan`. В окне запроса введите и выполните команду `exec GetProductsWithPriceLessThan 25`, в которой будут перечислены все продукты, размер которых меньше $25, как показано на рис. 14.

[Отображаются ![продукты под управлением $25](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image27.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image26.png)

**Рис. 14**. отображаются продукты под $25 ([щелкните, чтобы просмотреть изображение с полным размером](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image28.png))

## <a name="step-6-calling-the-managed-stored-procedure-from-the-data-access-layer"></a>Шаг 6. вызов управляемой хранимой процедуры из уровня доступа к данным

На этом этапе мы добавили `GetDiscontinuedProducts` и `GetProductsWithPriceLessThan` управляемые хранимые процедуры в проект `ManagedDatabaseConstructs` и зарегистрировали их в базе данных SQL Server "Борей". Эти управляемые хранимые процедуры также вызывались из SQL Server Management Studio (см. рис. 13 и 14). Однако, чтобы приложение ASP.NET использовало эти управляемые хранимые процедуры, необходимо добавить их к уровням доступа к данным и бизнес-логики в архитектуре. На этом шаге мы добавим два новых метода в `ProductsTableAdapter` в `NorthwindWithSprocs` типизированном наборе данных, который изначально был создан в руководстве [Создание новых хранимых процедур для адаптеров TableAdapter типизированного набора данных](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs.md) . На шаге 7 в BLL будут добавлены соответствующие методы.

Откройте `NorthwindWithSprocs` типизированный набор данных в Visual Studio и начните с добавления нового метода в `ProductsTableAdapter` с именем `GetDiscontinuedProducts`. Чтобы добавить новый метод в TableAdapter, щелкните имя TableAdapter в конструкторе правой кнопкой мыши и выберите пункт Добавить запрос в контекстном меню.

> [!NOTE]
> Так как мы переместили базу данных Northwind из папки `App_Data` в экземпляр базы данных SQL Server 2005, экспресс-выпуск, необходимо обновить соответствующую строку подключения в файле Web. config, чтобы отразить это изменение. На шаге 2 мы обсуждали обновление значения `NORTHWNDConnectionString` в `Web.config`. Если вы забыли внести это обновление, появится сообщение об ошибке не удалось добавить запрос. Не удается найти `NORTHWNDConnectionString` соединений для объекта `Web.config` в диалоговом окне при попытке добавить новый метод в TableAdapter. Чтобы устранить эту ошибку, нажмите кнопку ОК, перейдите к `Web.config` и обновите значение `NORTHWNDConnectionString`, как описано в шаге 2. Затем попробуйте повторно добавить метод в TableAdapter. На этот раз она должна работать без ошибок.

При добавлении нового метода запускается мастер настройки запросов TableAdapter, который мы использовали много раз в прошлых учебных курсах. На первом шаге мы предложим указать, как TableAdapter должен обращаться к базе данных: через специальный оператор SQL или с помощью новой или существующей хранимой процедуры. Так как мы уже создали и зарегистрировали `GetDiscontinuedProducts` управляемую хранимую процедуру с базой данных, выберите параметр использовать существующую хранимую процедуру и нажмите кнопку Далее.

[![выберите параметр использовать существующую хранимую процедуру.](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image30.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image29.png)

**Рис. 15**. Выбор параметра использовать существующую хранимую процедуру ([щелкните, чтобы просмотреть изображение с полным размером](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image31.png))

На следующем экране запрашивается хранимая процедура, которую вызовет метод. Выберите из раскрывающегося списка `GetDiscontinuedProducts` управляемую хранимую процедуру и нажмите кнопку Далее.

[![Выбор управляемой хранимой процедуры Жетдисконтинуедпродуктс](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image33.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image32.png)

**Рис. 16**. Выбор управляемой хранимой процедуры `GetDiscontinuedProducts` ([щелкните, чтобы просмотреть изображение с полным размером](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image34.png))

Затем будет предложено указать, возвращает ли хранимая процедура строки, одно значение или ничего. Поскольку `GetDiscontinuedProducts` возвращает набор неподдерживаемых строк продуктов, выберите первый параметр (табличные данные) и нажмите кнопку Далее.

[![выберите параметр табличных данных](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image36.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image35.png)

**Рис. 17**. Выбор параметра табличных данных ([щелкните, чтобы просмотреть изображение с полным размером](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image37.png))

На последнем экране мастера можно указать используемые шаблоны доступа к данным и имена результирующих методов. Оставьте флажки установленными и назовите методы `FillByDiscontinued` и `GetDiscontinuedProducts`. Чтобы завершить работу мастера, нажмите кнопку Готово.

[![назовите методы Филлбидисконтинуед и Жетдисконтинуедпродуктс.](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image39.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image38.png)

**Рис. 18**. Именование методов `FillByDiscontinued` и `GetDiscontinuedProducts` ([щелкните, чтобы просмотреть изображение с полным размером](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image40.png))

Повторите эти шаги, чтобы создать методы с именами `FillByPriceLessThan` и `GetProductsWithPriceLessThan` в `ProductsTableAdapter` для `GetProductsWithPriceLessThan` управляемой хранимой процедуры.

На рис. 19 показан снимок экрана конструктора наборов данных после добавления методов в `ProductsTableAdapter` для `GetDiscontinuedProducts` и `GetProductsWithPriceLessThan` управляемых хранимых процедур.

[![Продуктстаблеадаптер включает новые методы, добавленные на этом шаге.](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image42.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image41.png)

**Рис. 19**. `ProductsTableAdapter` включает новые методы, добавленные на этом шаге ([щелкните, чтобы просмотреть изображение с полным размером](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image43.png)).

## <a name="step-7-adding-corresponding-methods-to-the-business-logic-layer"></a>Шаг 7. Добавление соответствующих методов на уровень бизнес-логики

Теперь, когда уровень доступа к данным обновлен, чтобы включить методы для вызова управляемых хранимых процедур, добавленных в шагах 4 и 5, необходимо добавить соответствующие методы к уровню бизнес-логики. Добавьте в класс `ProductsBLLWithSprocs` следующие два метода:

[!code-csharp[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample7.cs)]

Оба метода просто вызывают соответствующий метод DAL и возвращают экземпляр `ProductsDataTable`. Разметка `DataObjectMethodAttribute` над каждым методом приводит к тому, что эти методы включаются в раскрывающийся список на вкладке Выбор мастера настройки источника данных ObjectDataSource.

## <a name="step-8-invoking-the-managed-stored-procedures-from-the-presentation-layer"></a>Шаг 8. вызов управляемых хранимых процедур из уровня представления

Благодаря бизнес-логике и слоям доступа к данным, дополненным к включению поддержки вызова `GetDiscontinuedProducts` и `GetProductsWithPriceLessThan` управляемых хранимых процедур, можно отобразить результаты этих хранимых процедур на странице ASP.NET.

Откройте страницу `ManagedFunctionsAndSprocs.aspx` в папке `AdvancedDAL` и в области элементов перетащите элемент управления GridView на конструктор. Задайте для свойства `ID` GridView s значение `DiscontinuedProducts` и из его смарт-тега привяжите его к новому ObjectDataSource с именем `DiscontinuedProductsDataSource`. Настройте ObjectDataSource для извлечения данных из `GetDiscontinuedProducts` метода `ProductsBLLWithSprocs` классов.

[![настроить ObjectDataSource для использования класса Продуктсбллвисспрокс](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image45.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image44.png)

**Рис. 20**. Настройка ObjectDataSource для использования класса `ProductsBLLWithSprocs` ([щелкните, чтобы просмотреть изображение с полным размером](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image46.png))

[![выберите метод Жетдисконтинуедпродуктс из раскрывающегося списка на вкладке Выбор.](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image48.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image47.png)

**Рис. 21**. выбор метода `GetDiscontinuedProducts` из раскрывающегося списка на вкладке «Выбор» ([щелкните, чтобы просмотреть изображение с полным размером](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image49.png))

Поскольку эта сетка будет использоваться для просто вывода сведений о продукте, установите в раскрывающихся списках на вкладках обновления, вставки и удаления значение (нет), а затем нажмите кнопку Готово.

После завершения работы мастера Visual Studio автоматически добавит BoundField или CheckBoxField для каждого поля данных в `ProductsDataTable`. Удалите все эти поля, кроме `ProductName` и `Discontinued`, после чего декларативная разметка GridView и ObjectDataSource s должна выглядеть следующим образом:

[!code-aspx[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample8.aspx)]

Уделите несколько минут для просмотра этой страницы в браузере. При посещении страницы ObjectDataSource вызывает метод `ProductsBLLWithSprocs` класса s `GetDiscontinuedProducts`. Как было показано на шаге 7, этот метод вызывает метод DAL s `ProductsDataTable` класса s `GetDiscontinuedProducts`, который вызывает `GetDiscontinuedProducts` хранимую процедуру. Эта хранимая процедура является управляемой хранимой процедурой и выполняет код, созданный на шаге 3 и возвращающий Неподдерживаемые продукты.

Результаты, возвращаемые управляемой хранимой процедурой, упаковываются в `ProductsDataTable` DAL, а затем возвращаются в BLL, который затем возвращает их в слой представления, где они привязаны к GridView и отображаются. Как и ожидалось, в сетке перечислены продукты, которые больше не поддерживаются.

[![перечислены неподдерживаемые продукты](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image51.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image50.png)

**Рис. 22**. список неподдерживаемых продуктов ([щелкните, чтобы просмотреть изображение с полным размером](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image52.png))

Для получения дополнительных рекомендаций добавьте на страницу текстовое поле и другой элемент управления GridView. В этом элементе GridView отображаются продукты, меньшие, чем сумма, введенная в текстовое поле, путем вызова метода `ProductsBLLWithSprocs` класса s `GetProductsWithPriceLessThan`.

## <a name="step-9-creating-and-calling-t-sql-udfs"></a>Шаг 9. Создание и вызов пользовательских функций T-SQL

Определяемые пользователем функции (UDF) — это объекты базы данных, которые точно имитируют семантику функций в языках программирования. Как и функция в C#, UDF может включать переменное число входных параметров и возвращать значение определенного типа. Определяемая пользователем функция может возвращать скалярные данные — строку, целое число и так далее или табличные данные. Давайте посмотрим на оба типа UDF, начиная с определяемой пользователем функции, возвращающей скалярный тип данных.

Следующая определяемая пользователем функция вычисляет оценочное значение инвентаризации для конкретного продукта. Это достигается путем принятия трех входных параметров: `UnitPrice`, `UnitsInStock`и `Discontinued` значений для конкретного продукта, и возвращает значение типа `money`. Он вычисляет оценочное значение инвентаризации, умножая `UnitPrice` на `UnitsInStock`. Для неподдерживаемых элементов это значение является половиной.

[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample9.sql)]

После добавления этой определяемой пользователем функции в базу данных ее можно найти с помощью Management Studio, развернув папку Программирование, затем функции и затем функции скалярного значения. Его можно использовать в `SELECT` запросе следующим образом:

[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample10.sql)]

Я добавил `udf_ComputeInventoryValue` UDF в базу данных Northwind; На рис. 23 показаны выходные данные приведенного выше `SELECT` запроса при просмотре Management Studio. Также обратите внимание, что определяемая пользователем функция указана в папке функции скалярных значений в обозревателе объектов.

[![указаны значения запасов каждого продукта](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image54.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image53.png)

**Рис. 23**. список значений инвентаризации продуктов ([щелкните, чтобы просмотреть изображение с полным размером](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image55.png))

Пользовательские функции могут также возвращать табличные данные. Например, можно создать определяемую пользователем функцию, которая возвращает продукты, принадлежащие к определенной категории:

[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample11.sql)]

`udf_GetProductsByCategoryID` UDF принимает входной параметр `@CategoryID` и возвращает результаты указанного `SELECT` запроса. После создания на эту определяемую пользователем функцию можно ссылаться в предложении `FROM` (или `JOIN`) запроса `SELECT`. В следующем примере возвращаются значения `ProductID`, `ProductName`и `CategoryID` для каждого из напитков.

[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample12.sql)]

Я добавил `udf_GetProductsByCategoryID` UDF в базу данных Northwind; На рис. 24 показаны выходные данные приведенного выше `SELECT` запроса при просмотре Management Studio. Определяемые пользователем функции, возвращающие табличные данные, можно найти в папке функции "Таблица-значение" обозревателя объектов.

[![для каждого из напитков указаны ProductID, ProductName и CategoryID.](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image57.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image56.png)

**Рис. 24**. `ProductID`, `ProductName`и `CategoryID` указаны для каждого из напитков ([щелкните, чтобы просмотреть изображение с полным размером](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image58.png)).

> [!NOTE]
> Дополнительные сведения о создании и использовании [определяемых пользователем функций](http://www.sqlteam.com/item.asp?ItemID=1955)см. в этой записи. Также ознакомьтесь [с преимуществами и недостатками определяемых пользователем функций](http://www.samspublishing.com/articles/article.asp?p=31724&amp;rl=1).

## <a name="step-10-creating-a-managed-udf"></a>Шаг 10. Создание управляемой определяемой пользователем функции

Пользовательские функции `udf_ComputeInventoryValue` и `udf_GetProductsByCategoryID`, созданные в приведенных выше примерах, являются объектами базы данных T-SQL. SQL Server 2005 также поддерживает управляемые определяемые пользователем функции, которые можно добавить в проект `ManagedDatabaseConstructs` так же, как и управляемые хранимые процедуры из шагов 3 и 5. Для этого шага Давайте рассмотрим реализацию функции `udf_ComputeInventoryValue` UDF в управляемом коде.

Чтобы добавить управляемую определяемую пользователем функцию в проект `ManagedDatabaseConstructs`, щелкните правой кнопкой мыши имя проекта в обозреватель решений и выберите Добавить новый элемент. Выберите определяемый пользователем шаблон в диалоговом окне Добавление нового элемента и назовите новый файл UDF `udf_ComputeInventoryValue_Managed.cs`.

[![добавить новую управляемую определяемую пользователем функцию в проект Манажеддатабасеконструктс](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image60.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image59.png)

**Рис. 25**. Добавление новой УПРАВЛЯЕМой пользовательской функции в проект `ManagedDatabaseConstructs` ([щелкните, чтобы просмотреть изображение с полным размером](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image61.png))

Шаблон определяемой пользователем функции создает `partial` класс с именем `UserDefinedFunctions` с методом, имя которого совпадает с именем файла класса (`udf_ComputeInventoryValue_Managed`в данном экземпляре). Этот метод декорирован с помощью [атрибута`SqlFunction`](https://msdn.microsoft.com/library/microsoft.sqlserver.server.sqlfunctionattribute.aspx), который помечает метод как управляемую определяемую пользователем функцию.

[!code-csharp[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample13.cs)]

В настоящее время метод `udf_ComputeInventoryValue` возвращает [объект`SqlString`](https://msdn.microsoft.com/library/system.data.sqltypes.sqlstring.aspx) и не принимает входные параметры. Необходимо обновить определение метода таким образом, чтобы оно принимало три входных параметра: `UnitPrice`, `UnitsInStock`и `Discontinued`, и возвращает объект `SqlMoney`. Логика вычисления значения инвентаризации идентична функции, заданной в функции T-SQL `udf_ComputeInventoryValue` UDF.

[!code-csharp[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample14.cs)]

Обратите внимание, что входные параметры метода UDF имеют соответствующие типы SQL: `SqlMoney` для поля `UnitPrice`, [`SqlInt16`](https://msdn.microsoft.com/library/system.data.sqltypes.sqlint16.aspx) для `UnitsInStock`и [`SqlBoolean`](https://msdn.microsoft.com/library/system.data.sqltypes.sqlboolean.aspx) для `Discontinued`. Эти типы данных соответствуют типам, определенным в таблице `Products`: столбец `UnitPrice` имеет тип `money`, `UnitsInStock` столбец типа `smallint`и столбец `Discontinued` типа `bit`.

Код начинается с создания `SqlMoney` экземпляра с именем `inventoryValue`, которому присваивается значение 0. Таблица `Products` допускает значения `NULL` базы данных в столбцах `UnitsInPrice` и `UnitsInStock`. Поэтому сначала необходимо проверить, содержат ли эти значения `NULL` s, что мы делаем с помощью свойства `SqlMoney` Objects [`IsNull`](https://msdn.microsoft.com/library/system.data.sqltypes.sqlmoney.isnull.aspx). Если и `UnitPrice`, и `UnitsInStock` содержат значения, отличные от`NULL`, то `inventoryValue` будет вычисляться как произведение двух. Затем, если `Discontinued` имеет значение true, то значение будет вдвое меньше.

> [!NOTE]
> Объект `SqlMoney` допускает одновременное умножение двух экземпляров `SqlMoney`. Он не позволяет умножить экземпляр `SqlMoney` на литеральное число с плавающей запятой. Таким образом, чтобы сократить `inventoryValue` мы умножаем его на новый экземпляр `SqlMoney`, имеющий значение 0,5.

## <a name="step-11-deploying-the-managed-udf"></a>Шаг 11. Развертывание управляемой определяемой пользователем функции

Теперь, когда создана управляемая функция UDF, мы готовы к развертыванию ее в базе данных Northwind. Как было показано на шаге 4, управляемые объекты в проекте SQL Server развертываются, если щелкнуть правой кнопкой мыши имя проекта в обозреватель решений и выбрать пункт Развертывание в контекстном меню.

После развертывания проекта вернитесь в SQL Server Management Studio и обновите папку "функции с скалярными значениями". Теперь вы увидите две записи:

- `dbo.udf_ComputeInventoryValue` — ОПРЕДЕЛЯЕМая пользователем функция T-SQL, созданная на шаге 9, и
- `dbo.udf ComputeInventoryValue_Managed` — управляемая определяемая пользователем функция, созданная на шаге 10, которая была только что развернута.

Чтобы протестировать управляемую определяемую пользователем функцию, выполните следующий запрос в Management Studio:

[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample15.sql)]

Эта команда использует управляемую `udf ComputeInventoryValue_Managed` UDF вместо T-SQL `udf_ComputeInventoryValue` UDF, но выходные данные одинаковы. Чтобы увидеть снимок экрана с выходными данными UDF, вернитесь на рис. 23.

## <a name="step-12-debugging-the-managed-database-objects"></a>Шаг 12. Отладка объектов управляемой базы данных

В учебнике [Отладка хранимых процедур](debugging-stored-procedures-cs.md) мы обсуждали три варианта отладки SQL Server с помощью Visual Studio: Непосредственная отладка базы данных, отладка приложений и отладка из проекта SQL Server. Управляемые объекты базы данных не могут быть отлажены с помощью прямой отладки базы данных, но могут быть отлаживаться из клиентского приложения и непосредственно из проекта SQL Server. Чтобы отладка работала, однако база данных SQL Server 2005 должна разрешать отладку SQL/CLR. Вспомним, что при первоначальном создании проекта `ManagedDatabaseConstructs` в Visual Studio было предложено включить отладку SQL/CLR (см. рис. 6 на шаге 2). Этот параметр можно изменить, щелкнув правой кнопкой мыши базу данных в окне обозреватель сервера.

![Убедитесь, что база данных разрешает отладку SQL/CLR.](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image62.png)

**Рис. 26**. Проверка того, что база данных разрешает отладку SQL/CLR

Представьте, что нам нужно отладить `GetProductsWithPriceLessThan` управляемую хранимую процедуру. Начнем с установки точки останова в коде метода `GetProductsWithPriceLessThan`.

[![установить точку останова в методе Жетпродуктсвисприцелесссан](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image64.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image63.png)

**Рис. 27**. Задание точки останова в методе `GetProductsWithPriceLessThan` ([щелкните, чтобы просмотреть изображение с полным размером](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image65.png))

Давайте сначала рассмотрим отладку управляемых объектов базы данных из проекта SQL Server. Так как наше решение включает два проекта: `ManagedDatabaseConstructs` SQL Server проект вместе с нашим веб-сайтом для отладки из проекта SQL Server необходимо указать Visual Studio запустить проект `ManagedDatabaseConstructs` SQL Server при запуске отладки. Щелкните правой кнопкой мыши проект `ManagedDatabaseConstructs` в обозреватель решений и выберите в контекстном меню пункт Назначить запускаемым проектом.

При запуске проекта `ManagedDatabaseConstructs` из отладчика он выполняет инструкции SQL в файле `Test.sql`, который находится в папке `Test Scripts`. Например, чтобы протестировать `GetProductsWithPriceLessThan` управляемую хранимую процедуру, замените существующее содержимое файла `Test.sql` следующей инструкцией, которая вызывает `GetProductsWithPriceLessThan` управляемую хранимую процедуру, передав `@CategoryID` значение 14,95:

[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample16.sql)]

После того, как вы введете приведенный выше скрипт в `Test.sql`, начните отладку, перейдя в меню Отладка и выбрав начать отладку или нажав клавишу F5 или зеленым значком воспроизведения на панели инструментов. Это приведет к построению проектов в решении, развертыванию объектов управляемой базы данных в базе данных Northwind, а затем выполнению скрипта `Test.sql`. На этом этапе будет достигнута точка останова, и мы можем пошагово выполнить метод `GetProductsWithPriceLessThan`, проверить значения входных параметров и т. д.

[![была достигнута точка останова в методе Жетпродуктсвисприцелесссан](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image67.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image66.png)

**Рис. 28**. попадание в точку останова в методе `GetProductsWithPriceLessThan` ([щелкните, чтобы просмотреть изображение с полным размером](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image68.png))

Чтобы объект базы данных SQL можно было отлаживать через клиентское приложение, необходимо настроить для базы данных поддержку отладки приложений. Щелкните правой кнопкой мыши базу данных в обозреватель сервера и убедитесь, что установлен флажок Отладка приложения. Кроме того, необходимо настроить приложение ASP.NET для интеграции с отладчиком SQL и отключения пулов соединений. Эти действия подробно описаны на шаге 2 учебника по [хранимым процедурам отладки](debugging-stored-procedures-cs.md) .

После настройки приложения и базы данных ASP.NET установите в качестве запускаемого проекта веб-сайт ASP.NET и начните отладку. При посещении страницы, вызывающей один из управляемых объектов с точкой останова, приложение будет остановлено, а Управление будет включено в отладчик, где можно выполнить код по шагам, как показано на рис. 28.

## <a name="step-13-manually-compiling-and-deploying-managed-database-objects"></a>Шаг 13. Компиляция и развертывание управляемых объектов базы данных вручную

SQL Server проекты упрощают создание, компиляцию и развертывание управляемых объектов базы данных. К сожалению, SQL Server проекты доступны только в выпусках Visual Studio Professional и Team Systems. Если вы используете Visual Web Developer или стандартный выпуск Visual Studio и хотите использовать управляемые объекты базы данных, необходимо вручную создать и развернуть их. Это включает в себя четыре шага:

1. Создайте файл, содержащий исходный код для управляемого объекта базы данных.
2. Скомпилируйте объект в сборку,
3. Зарегистрируйте сборку в базе данных SQL Server 2005 и
4. Создайте объект базы данных в SQL Server, указывающий на соответствующий метод в сборке.

Чтобы продемонстрировать эти задачи, давайте создадим новую управляемую хранимую процедуру, которая возвращает те продукты, у которых `UnitPrice` больше указанного значения. Создайте новый файл на своем компьютере с именем `GetProductsWithPriceGreaterThan.cs` и введите в него следующий код (для этого можно использовать Visual Studio, Notepad или любой текстовый редактор):

[!code-csharp[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample17.cs)]

Этот код практически идентичен методу `GetProductsWithPriceLessThan` метода, созданному на шаге 5. Единственным отличием являются имена методов, предложение `WHERE` и имя параметра, используемого в запросе. Вернувшись в метод `GetProductsWithPriceLessThan`, `WHERE` предложение Read: `WHERE UnitPrice < @MaxPrice`. Здесь в `GetProductsWithPriceGreaterThan`используется: `WHERE UnitPrice > @MinPrice`.

Теперь необходимо скомпилировать этот класс в сборку. В командной строке перейдите в каталог, где сохранен файл `GetProductsWithPriceGreaterThan.cs`, и используйте C# компилятор (`csc.exe`) для компиляции файла класса в сборку:

[!code-console[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample18.cmd)]

Если папка, содержащая `csc.exe`, не находится в `PATH`системы, необходимо будет полностью ссылаться на путь, `%WINDOWS%\Microsoft.NET\Framework\version\`следующим образом:

[!code-console[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample19.cmd)]

[![компилировать GetProductsWithPriceGreaterThan.cs в сборку](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image70.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image69.png)

**Рис. 29**. Компиляция `GetProductsWithPriceGreaterThan.cs` в сборку ([щелкните, чтобы просмотреть изображение с полным размером](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image71.png))

Флаг `/t` указывает, что файл C# класса должен быть скомпилирован в библиотеку DLL (а не на исполняемый объект). Флаг `/out` задает имя результирующей сборки.

> [!NOTE]
> Вместо компиляции файла `GetProductsWithPriceGreaterThan.cs` класса из командной строки можно также использовать [ C# Visual Express Edition](https://msdn.microsoft.com/vstudio/express/visualcsharp/) или создать отдельный проект библиотеки классов в выпуске Visual Studio Standard Edition. S REN Джейкоб Лауритсен предоставляет такой проект Visual C# Express Edition с кодом для `GetProductsWithPriceGreaterThan` хранимой процедуры и двумя управляемыми хранимыми процедурами и UDF, созданными в шагах 3, 5 и 10. Проект REN s также включает команды T-SQL, необходимые для добавления соответствующих объектов базы данных.

В коде, скомпилированном в сборку, мы готовы зарегистрировать сборку в базе данных SQL Server 2005. Это можно выполнить с помощью T-SQL, используя командную `CREATE ASSEMBLY`или SQL Server Management Studio. Давайте рассмотрим использование Management Studio.

В Management Studio разверните папку Программирование в базе данных Northwind. Одна из его вложенных папок — сборки. Чтобы вручную добавить новую сборку в базу данных, щелкните правой кнопкой мыши папку сборки и выберите в контекстном меню пункт Создать сборку. Откроется диалоговое окно Новая сборка (см. рис. 30). Нажмите кнопку Обзор, выберите только что скомпилированную сборку `ManuallyCreatedDBObjects.dll` и нажмите кнопку ОК, чтобы добавить сборку в базу данных. Не следует видеть сборку `ManuallyCreatedDBObjects.dll` в обозревателе объектов.

[![добавить сборку Мануалликреатеддбобжектс. dll в базу данных](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image73.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image72.png)

**Рис. 30**. Добавление `ManuallyCreatedDBObjects.dll` сборки в базу данных ([щелкните, чтобы просмотреть изображение с полным размером](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image74.png))

![Мануалликреатеддбобжектс. dll отображается в обозревателе объектов.](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image75.png)

**Рис. 31**. `ManuallyCreatedDBObjects.dll` отображается в обозревателе объектов

Хотя мы добавили сборку в базу данных Northwind, нам еще не нужно связать хранимую процедуру с методом `GetProductsWithPriceGreaterThan` в сборке. Для этого откройте новое окно запроса и выполните следующий скрипт:

[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample20.sql)]

При этом создается новая хранимая процедура в базе данных Northwind с именем `GetProductsWithPriceGreaterThan` и связывается с управляемым методом `GetProductsWithPriceGreaterThan` (который находится в классе `StoredProcedures`, который находится в сборке `ManuallyCreatedDBObjects`).

После выполнения приведенного выше скрипта обновите папку хранимых процедур в обозревателе объектов. Вы должны увидеть новую запись хранимой процедуры-`GetProductsWithPriceGreaterThan`-с рядом значком замка. Чтобы протестировать эту хранимую процедуру, введите и выполните следующий скрипт в окне запроса:

[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample21.sql)]

Как показано на рисунке 32, приведенная выше команда отображает сведения о продуктах с `UnitPrice` более $24,95.

[![Мануалликреатеддбобжектс. dll отображается в обозревателе объектов.](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image77.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image76.png)

**Рис. 32**. `ManuallyCreatedDBObjects.dll` отображается в обозревателе объектов ([щелкните, чтобы просмотреть изображение с полным размером](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image78.png))

## <a name="summary"></a>Сводка

Microsoft SQL Server 2005 обеспечивает интеграцию со средой CLR, которая позволяет создавать объекты базы данных с помощью управляемого кода. Ранее эти объекты базы данных могли быть созданы только с помощью T-SQL, но теперь мы можем создавать эти объекты с помощью языков программирования C#.NET, таких как. В этом руководстве мы создали две управляемые хранимые процедуры и управляемую определяемую пользователем функцию.

Visual Studio s SQL Server тип проекта упрощает создание, компиляцию и развертывание управляемых объектов базы данных. Более того, он предлагает широкие возможности отладки. Однако SQL Server типы проектов доступны только в выпусках Visual Studio Professional и Team Systems. Для тех, кто использует Visual Web Developer или стандартный выпуск Visual Studio, шаги создания, компиляции и развертывания необходимо выполнять вручную, как было показано на шаге 13.

Поздравляем с программированием!

## <a name="further-reading"></a>Дополнительные сведения

Дополнительные сведения о разделах, обсуждаемых в этом руководстве, см. в следующих ресурсах:

- [Преимущества и недостатки определяемых пользователем функций](http://www.samspublishing.com/articles/article.asp?p=31724&amp;rl=1)
- [Создание объектов SQL Server 2005 в управляемом коде](https://channel9.msdn.com/Showpost.aspx?postid=142413)
- [Создание триггеров с помощью управляемого кода в SQL Server 2005](http://www.15seconds.com/issue/041006.htm)
- [Инструкции. Создание и запуск хранимой процедуры CLR SQL Server](https://msdn.microsoft.com/library/5czye81z(VS.80).aspx)
- [Как создать и запустить определяемую пользователем функцию CLR SQL Server](https://msdn.microsoft.com/library/w2kae45k(VS.80).aspx)
- [Инструкции. изменение скрипта `Test.sql` для запуска объектов SQL](https://msdn.microsoft.com/library/ms233682(VS.80).aspx)
- [Введение в определяемые пользователем функции](http://www.sqlteam.com/item.asp?ItemID=1955)
- [Управляемый код и SQL Server 2005 (видео)](https://channel9.msdn.com/Showpost.aspx?postid=142413)
- [Справочник по Transact-SQL](https://msdn.microsoft.com/library/aa299742(SQL.80).aspx)
- [Пошаговое руководство. Создание хранимой процедуры в управляемом коде](https://msdn.microsoft.com/library/zxsa8hkf(VS.80).aspx)

## <a name="about-the-author"></a>Об авторе

[Скотт Митчелл](http://www.4guysfromrolla.com/ScottMitchell.shtml), автор семи книг по ASP/ASP. NET и основатель [4GuysFromRolla.com](http://www.4guysfromrolla.com), работал с веб-технологиями Майкрософт с 1998. Скотт работает как независимый консультант, преподаватель и модуль записи. Его последняя книга — [*Sams обучать себя ASP.NET 2,0 за 24 часа*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco). Он доступен по адресу [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) или через его блог, который можно найти по адресу [http://ScottOnWriting.NET](http://ScottOnWriting.NET).

## <a name="special-thanks-to"></a>Специальная благодарность

Эта серия руководств была рассмотрена многими полезными рецензентами. Специалистом по интересу для этого учебника был режим REN Джейкоб Лауритсен. Помимо просмотра этой статьи, REN также создал проект Visual C# Express Edition, который входит в эту статью, чтобы вручную скомпилировать управляемые объекты базы данных. Хотите ознакомиться с моими будущими статьями MSDN? Если это так, расположите строку в [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Назад](debugging-stored-procedures-cs.md)
> [Вперед](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb.md)
