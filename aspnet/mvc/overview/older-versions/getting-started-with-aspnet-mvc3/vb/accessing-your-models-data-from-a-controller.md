---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/accessing-your-models-data-from-a-controller
title: Доступ к данным модели из контроллера (VB) | Документация Майкрософт
author: Rick-Anderson
description: В этом учебнике вы узнаете об основах создания веб-приложения ASP.NET MVC с помощью Microsoft Visual Web Developer 2010 Express с пакетом обновления 1 (SP1)...
ms.author: riande
ms.date: 01/12/2011
ms.assetid: cad00de1-3c68-4ff4-a436-54236d449459
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/accessing-your-models-data-from-a-controller
msc.type: authoredcontent
ms.openlocfilehash: 37f45d8f12e3ab5c485718bcf2c59934ad272118
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78498660"
---
# <a name="accessing-your-models-data-from-a-controller-vb"></a>Доступ к данным модели из контроллера (VB)

по [Рик Андерсон (](https://twitter.com/RickAndMSFT)

> В этом учебнике вы узнаете об основах создания веб-приложения ASP.NET MVC с помощью Microsoft Visual Web Developer 2010 Express с пакетом обновления 1 (SP1), который является бесплатной версией Microsoft Visual Studio. Прежде чем начать, убедитесь, что установлены предварительные требования, перечисленные ниже. Чтобы установить все эти компоненты, щелкните следующую ссылку: [установщик веб-платформы](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack). Кроме того, вы можете отдельно установить необходимые компоненты, используя следующие ссылки:
> 
> - [Предварительные требования для Visual Studio Web Developer Express SP1](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [Обновление инструментов ASP.NET MVC 3](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - [SQL Server Compact 4,0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(поддержка времени выполнения и средств)
> 
> Если вы используете Visual Studio 2010 вместо Visual Web Developer 2010, установите необходимые компоненты, щелкнув следующую ссылку: [Предварительные требования для Visual studio 2010](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack).
> 
> Для этого раздела доступен проект Visual Web Developer с исходным кодом VB.NET. [Скачайте версию VB.NET](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098). При желании C#переключитесь на [ C# версию](../cs/accessing-your-models-data-from-a-controller.md) этого учебника.

В этом разделе вы создадите новый класс `MoviesController` и запишете код, который извлекает данные фильмов и отображает их в браузере с помощью шаблона представления. Перед продолжением обязательно создайте приложение.

Щелкните правой кнопкой мыши папку *Controllers* и создайте новый контроллер `MoviesController`. Выберите следующие параметры.

- Имя контроллера: **MoviesController**. (это установка по умолчанию).
- Шаблон: **контроллер с действиями чтения и записи и представлениями с использованием Entity Framework**.
- Класс модели: **Movie (MvcMovie. Models)** .
- Класс контекста данных: **мовиедбконтекст (MvcMovie. Models)** .
- Представления: **Razor (CSHTML)** . (Значение по умолчанию.)

[![5addMovieController](accessing-your-models-data-from-a-controller/_static/image2.png)](accessing-your-models-data-from-a-controller/_static/image1.png)

Нажмите кнопку **Добавить**. Visual Web Developer создает следующие файлы и папки:

- Файл *MoviesController. vb* в папке *Controllers* проекта.
- Папка *фильмов* в папке *views* проекта.
- *Создайте. vbhtml, DELETE. vbhtml, Details. vbhtml, Edit. vbhtml*и *index. vbhtml* в новой папке *виевс\мовиес*

[![5_ScaffoldMovie](accessing-your-models-data-from-a-controller/_static/image4.png)](accessing-your-models-data-from-a-controller/_static/image3.png)

Механизм формирования шаблонов ASP.NET MVC 3 автоматически создал для вас методы и представления действий CRUD (создание, чтение, обновление и удаление). Теперь у вас есть полнофункциональное веб-приложение, которое позволяет создавать, перечислять, изменять и удалять записи фильмов.

Запустите приложение и перейдите к контроллеру `Movies`, добавив */Movies* в URL-адрес в адресной строке браузера. Поскольку приложение полагается на маршрутизацию по умолчанию (определенную в файле *Global. asax* ), запрос браузера `http://localhost:xxxxx/Movies` направляется в метод действия `Index` по умолчанию контроллера `Movies`. Иными словами, `http://localhost:xxxxx/Movies` запроса браузера фактически аналогичен `http://localhost:xxxxx/Movies/Index`запроса браузера. Результатом является пустой список фильмов, так как вы еще не добавили их.

![](accessing-your-models-data-from-a-controller/_static/image5.png)

## <a name="creating-a-movie"></a>Создание фильма

Щелкните ссылку **Create New** (Создать). Введите некоторые сведения о фильме и нажмите кнопку **создать** .

![](accessing-your-models-data-from-a-controller/_static/image6.png)

Нажатие кнопки **создать** приводит к тому, что форма будет отправлена на сервер, где сведения о фильме будут сохранены в базе данных. Затем вы перейдете на URL-адрес */Movies* , на котором можно увидеть созданный фильм в списке.

[![Индексвхенхарримет](accessing-your-models-data-from-a-controller/_static/image8.png)](accessing-your-models-data-from-a-controller/_static/image7.png)

Создайте еще несколько записей фильмов. Попробуйте воспользоваться ссылками **Изменить**, **Сведения** и **Удалить** — все они работают.

## <a name="examining-the-generated-code"></a>Проверка созданного кода

Откройте файл *контроллерс\мовиесконтроллер.ВБ* и изучите созданный метод `Index`. Ниже показана часть контроллера фильмов с методом `Index`.

[!code-vb[Main](accessing-your-models-data-from-a-controller/samples/sample1.vb)]

Следующая строка из класса `MoviesController` создает экземпляр контекста базы данных Movie, как описано выше. Для запроса, изменения и удаления фильмов можно использовать контекст базы данных Movie.

[!code-vb[Main](accessing-your-models-data-from-a-controller/samples/sample2.vb)]

Запрос к контроллеру `Movies` возвращает все записи в таблице `Movies` базы данных фильмов, а затем передает результаты в представление `Index`.

## <a name="strongly-typed-models-and-the-model-keyword"></a>Строго типизированные модели и ключевое слово @model

Ранее в этом руководстве вы узнали, как контроллер может передавать данные или объекты в шаблон представления с помощью объекта `ViewBag`. `ViewBag` — это динамический объект, предоставляющий удобный способ для передачи сведений в представление.

ASP.NET MVC также предоставляет возможность передавать строго типизированные данные или объекты в шаблон представления. Такой строго типизированный подход обеспечивает лучшую проверку кода во время компиляции и более широкие возможности IntelliSense в редакторе Visual Web Developer. Мы используем этот подход с шаблоном представления *index. vbhtml* с классом `MoviesController`.

Обратите внимание, что код создает объект [`List`](https://msdn.microsoft.com/library/6sh2ey19.aspx) при вызове вспомогательного метода `View` в методе `Index` действия. Затем код передает этот список `Movies` из контроллера в представление:

[!code-vb[Main](accessing-your-models-data-from-a-controller/samples/sample3.vb)]

Включив инструкцию `@ModelType` в верхней части файла шаблона представления, можно указать тип объекта, который предполагается отобразить в представлении. При создании контроллера фильмов Visual Web Developer автоматически включил следующую инструкцию `@model` в начало файла *index. vbhtml* :

[!code-vbhtml[Main](accessing-your-models-data-from-a-controller/samples/sample4.vbhtml)]

Эта директива `@ModelType` позволяет получить доступ к списку фильмов, переданных контроллером в представление, используя строго типизированный объект `Model`. Например, в шаблоне *index. vbhtml* код проходит через фильмы, выполняя инструкцию `foreach` для строго типизированного объекта `Model`:

[!code-vbhtml[Main](accessing-your-models-data-from-a-controller/samples/sample5.vbhtml)]

Так как объект `Model` является строго типизированным (в виде объекта `IEnumerable<Movie>`), каждый объект `item` в цикле вводится как `Movie`. Помимо прочих преимуществ это означает, что во время компиляции кода и полной поддержки IntelliSense в редакторе кода вы получаете проверку.

[![5_Intellisense](accessing-your-models-data-from-a-controller/_static/image10.png)](accessing-your-models-data-from-a-controller/_static/image9.png)

## <a name="working-with-sql-server-compact"></a>Работа с SQL Server Compact

Entity Framework Code First обнаружила, что предоставленная строка подключения к базе данных указывала на базу данных `Movies`, которая еще не существовала, поэтому Code First автоматически создавала базу данных. Чтобы убедиться, что он создан, найдите в папке *приложение\_данные* . Если файл *movies. sdf* не отображается, нажмите кнопку " **Показать все файлы** " на панели инструментов **Обозреватель решений** , нажмите кнопку " **Обновить** ", а затем разверните папку " *приложение\_данные* ".

[![SDF_in_SolnExp](accessing-your-models-data-from-a-controller/_static/image12.png)](accessing-your-models-data-from-a-controller/_static/image11.png)

Дважды щелкните *movies. sdf* , чтобы открыть **Обозреватель сервера**. Затем разверните папку **таблицы** , чтобы просмотреть таблицы, созданные в базе данных.

> [!NOTE]
> Если при двойном щелчке на *movies. sdf*появляется сообщение об ошибке, убедитесь, что установлены **средства Visual Studio 2010 с пакетом обновления 1 (SP1) для SQL Server Compact 4,0**. (Ссылки на программное обеспечение см. в списке предварительных требований в первой части этой серии руководств.) Если установить выпуск сейчас, необходимо закрыть и снова открыть Visual Web Developer.

[![DB_explorer](accessing-your-models-data-from-a-controller/_static/image14.png)](accessing-your-models-data-from-a-controller/_static/image13.png)

Существует две таблицы, одна для `Movie` набора сущностей, а затем `EdmMetadata` таблицу. `EdmMetadata` таблица используется Entity Framework, чтобы определить, когда модель и база данных не синхронизированы.

Щелкните правой кнопкой мыши таблицу `Movies` и выберите **Показать данные таблицы** , чтобы просмотреть созданные данные.

[![Мовиестабле](accessing-your-models-data-from-a-controller/_static/image16.png)](accessing-your-models-data-from-a-controller/_static/image15.png)

Щелкните правой кнопкой мыши таблицу `Movies` и выберите **изменить схему таблицы**.

[![Едиттаблесчема](accessing-your-models-data-from-a-controller/_static/image18.png)](accessing-your-models-data-from-a-controller/_static/image17.png)

![таблесчемасм](accessing-your-models-data-from-a-controller/_static/image19.png)

Обратите внимание, что схема `Movies` таблицы сопоставляется с созданным ранее классом `Movie`. Entity Framework Code First автоматически создали эту схему на основе класса `Movie`.

По завершении закройте подключение. (Если вы не закроете подключение, при следующем запуске проекта может появиться сообщение об ошибке).

[![Клосеконнектион](accessing-your-models-data-from-a-controller/_static/image21.png)](accessing-your-models-data-from-a-controller/_static/image20.png)

Теперь у вас есть база данных и простая страница со списком для отображения содержимого из нее. В следующем руководстве мы рассмотрим оставшуюся часть кода с формированием шаблонов и добавим метод `SearchIndex` и представление `SearchIndex`, которое позволяет выполнять поиск фильмов в этой базе данных.

> [!div class="step-by-step"]
> [Назад](adding-a-model.md)
> [Вперед](examining-the-edit-methods-and-edit-view.md)
