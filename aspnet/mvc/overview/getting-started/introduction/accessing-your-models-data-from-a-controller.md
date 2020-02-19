---
uid: mvc/overview/getting-started/introduction/accessing-your-models-data-from-a-controller
title: Доступ к данным модели из контроллера | Документация Майкрософт
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 10/17/2013
ms.assetid: caa1ba4a-f9f0-4181-ba21-042e3997861d
msc.legacyurl: /mvc/overview/getting-started/introduction/accessing-your-models-data-from-a-controller
msc.type: authoredcontent
ms.openlocfilehash: 5d882d765133d32d3acdba9ffb5d43b69119a273
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457236"
---
# <a name="accessing-your-models-data-from-a-controller"></a>Доступ к данным модели из контроллера

по [Рик Андерсон (](https://twitter.com/RickAndMSFT)

[!INCLUDE [Tutorial Note](index.md)]

В этом разделе вы создадите новый класс `MoviesController` и запишете код, который извлекает данные фильмов и отображает их в браузере с помощью шаблона представления.

**Создайте приложение,** прежде чем переходить к следующему шагу. Если вы не создаете приложение, вы получите сообщение об ошибке при добавлении контроллера.

В обозреватель решений щелкните правой кнопкой мыши папку *Controllers* и выберите команду **Добавить**, а затем — **контроллер**.

![](accessing-your-models-data-from-a-controller/_static/image1.png)

В диалоговом окне **Добавление шаблона** выберите **контроллер MVC 5 с представлениями с помощью Entity Framework**и нажмите кнопку **добавить**.

![](accessing-your-models-data-from-a-controller/_static/image2.png)

- Выберите **фильм (MvcMovie. Models)** для класса Model.
- Выберите **мовиедбконтекст (MvcMovie. Models)** для класса контекста данных.
- В качестве имени контроллера введите **MoviesController**.

  На рисунке ниже показано диалоговое окно завершено.  
  
![](accessing-your-models-data-from-a-controller/_static/image3.png)   

Нажмите кнопку **Добавить**. (Если появляется сообщение об ошибке, то, возможно, приложение не было собрано до начала добавления контроллера.) Visual Studio создает следующие файлы и папки:

- Файл *MoviesController.CS* в папке *Controllers* .
- Папка *виевс\мовиес* .
- В новой папке *Виевс\мовиес* *создаются. cshtml, DELETE. cshtml, Details. cshtml, Edit. cshtml*и *index. cshtml* .

Visual Studio автоматически создавала методы и представления действия [CRUD](http://en.wikipedia.org/wiki/Create,_read,_update_and_delete) (создание, чтение, обновление и удаление) для вас (автоматическое создание методов и ПРЕДСТАВЛЕНИЙ действий CRUD называется формированием шаблонов). Теперь у вас есть полнофункциональное веб-приложение, которое позволяет создавать, перечислять, изменять и удалять записи фильмов.

Запустите приложение и щелкните ссылку на **ролик MVC** (или перейдите к контроллеру `Movies`, добавив */Movies* к URL-адресу в адресной строке браузера). Поскольку приложение полагается на маршрутизацию по умолчанию (определенную в файле *приложения\_старт\раутеконфиг.КС* ), запрос браузера `http://localhost:xxxxx/Movies` перенаправляется в метод действия `Index` по умолчанию контроллера `Movies`. Иными словами, `http://localhost:xxxxx/Movies` запроса браузера фактически аналогичен `http://localhost:xxxxx/Movies/Index`запроса браузера. Результатом является пустой список фильмов, так как вы еще не добавили их.

![](accessing-your-models-data-from-a-controller/_static/image4.png)

### <a name="creating-a-movie"></a>Создание фильма

Щелкните ссылку **Create New** (Создать). Введите некоторые сведения о фильме и нажмите кнопку **создать** .

![](accessing-your-models-data-from-a-controller/_static/image5.png)

> [!NOTE]
> Возможно, вы не сможете вводить десятичные или запятые в поле Price. для поддержки проверки jQuery для национальных стандартов, отличных от английского, которые используют запятую (&quot;,&quot;) для десятичной запятой и форматы даты, отличные от US-English, необходимо включить *глобализацию. js* и определенные *языки и региональные параметры/глобализации. js* (из [https://github.com/jquery/globalize](https://github.com/jquery/globalize) ) и JavaScript для использования `Globalize.parseFloat`. Я покажу, как это сделать в следующем руководстве. А пока вводите целые числа, такие как 10.

Нажатие кнопки **создать** приводит к тому, что форма будет отправлена на сервер, где сведения о фильме будут сохранены в базе данных. Затем вы перейдете на URL-адрес */Movies* , на котором можно увидеть созданный фильм в списке.

![](accessing-your-models-data-from-a-controller/_static/image6.png)

Создайте еще несколько записей фильмов. Попробуйте воспользоваться ссылками **Изменить**, **Сведения** и **Удалить** — все они работают.

## <a name="examining-the-generated-code"></a>Проверка созданного кода

Откройте файл *контроллерс\мовиесконтроллер.КС* и изучите созданный метод `Index`. Ниже показана часть контроллера фильмов с методом `Index`.

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample1.cs)]

Запрос к контроллеру `Movies` возвращает все записи в таблице `Movies`, а затем передает результаты в представление `Index`. Следующая строка из класса `MoviesController` создает экземпляр контекста базы данных Movie, как описано выше. Для запроса, изменения и удаления фильмов можно использовать контекст базы данных Movie.

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample2.cs)]

## <a name="strongly-typed-models-and-the-model-keyword"></a>Строго типизированные модели и ключевое слово @model

Ранее в этом руководстве вы узнали, как контроллер может передавать данные или объекты в шаблон представления с помощью объекта `ViewBag`. `ViewBag` — это динамический объект, предоставляющий удобный способ для передачи сведений в представление.

MVC также предоставляет возможность передачи *строго* типизированных объектов в шаблон представления. Такой строго типизированный подход обеспечивает лучшую проверку кода во время компиляции и более широкие возможности [IntelliSense](https://msdn.microsoft.com/library/hcw1s69b(v=vs.120).aspx) в редакторе Visual Studio. Механизм формирования шаблонов в Visual Studio использовал такой подход (то есть передает *строго* типизированную модель) с классом `MoviesController` и шаблонами представления при создании методов и представлений.

В файле *контроллерс\мовиесконтроллер.КС* изучите созданный метод `Details`. Ниже показан метод `Details`.

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample3.cs)]

Параметр `id` обычно передается как данные маршрута, например `http://localhost:1234/movies/details/1` установит контроллер в качестве контроллера ролика, действие для `details`, а `id` — 1. Идентификатор можно также передать в строку запроса следующим образом:

`http://localhost:1234/movies/details?id=1`

При обнаружении `Movie` экземпляр модели `Movie` передается в представление `Details`.

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample4.cs)]

Изучите содержимое файла *виевс\мовиес\детаилс.кштмл* :

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample5.cshtml?highlight=1-2)]

Включив инструкцию `@model` в верхней части файла шаблона представления, можно указать тип объекта, который предполагается отобразить в представлении. При создании контроллера movie Visual Studio автоматически включает следующий оператор `@model` в начало файла *Details.cshtml*:

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample6.cshtml)]

Эта директива `@model` обеспечивает доступ к фильму, который контроллер передал в представление с использованием строго типизированного объекта `Model`. Например, в шаблоне *Details. cshtml* код передает каждое поле movie в `DisplayNameFor` и [DisplayFor](https://msdn.microsoft.com/library/system.web.mvc.html.displayextensions.displayfor(VS.98).aspx) вспомогательные методы HTML с помощью строго типизированного объекта `Model`. Методы `Create` и `Edit` и шаблоны представлений также передают объект модели фильма.

Изучите шаблон представления *index. cshtml* и метод `Index` в файле *MoviesController.CS* . Обратите внимание, что код создает объект [`List`](https://msdn.microsoft.com/library/6sh2ey19.aspx) при вызове вспомогательного метода `View` в методе `Index` действия. Затем код передает этот список `Movies` из метода действия `Index` в представление:

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample7.cs?highlight=3)]

При создании контроллера фильмов Visual Studio автоматически включил в начало файла *index. cshtml* следующую инструкцию `@model`:

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample8.cshtml)]

Эта директива `@model` позволяет получить доступ к списку фильмов, переданных контроллером в представление, используя строго типизированный объект `Model`. Например, в шаблоне *index. cshtml* код проходит через фильмы, выполняя инструкцию `foreach` для строго типизированного объекта `Model`:

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample9.cshtml?highlight=1,4,7,10,13,16,19-21)]

Так как объект `Model` является строго типизированным (в виде объекта `IEnumerable<Movie>`), каждый объект `item` в цикле вводится как `Movie`. Помимо прочих преимуществ это означает, что во время компиляции кода и полной поддержки IntelliSense в редакторе кода вы получаете проверку.

![моделинтеллисенсе](accessing-your-models-data-from-a-controller/_static/image8.png)

## <a name="working-with-sql-server-localdb"></a>Работа с SQL Server LocalDB

Entity Framework Code First обнаружила, что предоставленная строка подключения к базе данных указывала на базу данных `Movies`, которая еще не существовала, поэтому Code First автоматически создавала базу данных. Чтобы убедиться, что он создан, найдите в папке *приложение\_данные* . Если файл *movies. mdf* не отображается, нажмите кнопку " **Показать все файлы** " на панели инструментов **Обозреватель решений** , нажмите кнопку " **Обновить** ", а затем разверните папку " *приложение\_данные* ".

![](accessing-your-models-data-from-a-controller/_static/image9.png)

Дважды щелкните *movies. mdf* , чтобы открыть **Обозреватель сервера**, а затем разверните папку **таблицы** , чтобы просмотреть таблицу фильмов. Обратите внимание на значок ключа рядом с ИДЕНТИФИКАТОРом. По умолчанию EF сделает свойство с именем ID первичным ключом. Дополнительные сведения о EF и MVC см. в разделе о отличном руководстве Tom Dykstra) по [MVC и EF](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).

![DB_explorer](accessing-your-models-data-from-a-controller/_static/image10.png "DB_explorer")

Щелкните правой кнопкой мыши таблицу `Movies` и выберите **Показать данные таблицы** , чтобы просмотреть созданные данные.

![](accessing-your-models-data-from-a-controller/_static/image11.png) 

![](accessing-your-models-data-from-a-controller/_static/image12.png)

Щелкните правой кнопкой мыши таблицу `Movies` и выберите **Open Table Definition (Открыть определение таблицы** ), чтобы увидеть структуру таблицы, которая Entity Framework Code First создана.

![](accessing-your-models-data-from-a-controller/_static/image13.png)

![](accessing-your-models-data-from-a-controller/_static/image14.png)

Обратите внимание, что схема `Movies` таблицы сопоставляется с созданным ранее классом `Movie`. Entity Framework Code First автоматически создали эту схему на основе класса `Movie`.

По завершении закройте подключение, щелкнув правой кнопкой мыши *мовиедбконтекст* и выбрав **закрыть подключение**. (Если вы не закроете подключение, при следующем запуске проекта может появиться сообщение об ошибке).

![](accessing-your-models-data-from-a-controller/_static/image15.png "CloseConnection")

Теперь у вас есть база данных и страницы для отображения, редактирования, обновления и удаления данных. В следующем руководстве мы рассмотрим оставшуюся часть кода с формированием шаблонов и добавим метод `SearchIndex` и представление `SearchIndex`, которое позволяет выполнять поиск фильмов в этой базе данных. Дополнительные сведения об использовании Entity Framework с MVC см. в разделе [Создание модели данных Entity Framework для приложения ASP.NET MVC](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).

> [!div class="step-by-step"]
> [Назад](creating-a-connection-string.md)
> [Вперед](examining-the-edit-methods-and-edit-view.md)
