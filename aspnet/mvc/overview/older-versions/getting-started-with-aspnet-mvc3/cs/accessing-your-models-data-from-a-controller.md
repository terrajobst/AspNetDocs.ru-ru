---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/accessing-your-models-data-from-a-controller
title: Доступ к данным модели из контроллера (C#) | Документация Майкрософт
author: Rick-Anderson
description: В этом учебнике вы узнаете об основах создания веб-приложения ASP.NET MVC с помощью Microsoft Visual Web Developer 2010 Express с пакетом обновления 1 (SP1)...
ms.author: riande
ms.date: 01/12/2011
ms.assetid: 002ada5c-f114-47ab-a441-57dbdb728ea0
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/accessing-your-models-data-from-a-controller
msc.type: authoredcontent
ms.openlocfilehash: 2e9c7f24d426635760b613f570b85455ce71b3dc
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/19/2020
ms.locfileid: "77458172"
---
# <a name="accessing-your-models-data-from-a-controller-c"></a>Доступ к данным модели из контроллера (C#)

по [Рик Андерсон (](https://twitter.com/RickAndMSFT)

> > [!NOTE]
> > Обновленная версия этого учебника доступна [здесь](../../../getting-started/introduction/getting-started.md) , в которой используется ASP.NET MVC 5 и Visual Studio 2013. Он более безопасен, гораздо проще следовать и демонстрирует дополнительные функции.
> 
> 
> В этом учебнике вы узнаете об основах создания веб-приложения ASP.NET MVC с помощью Microsoft Visual Web Developer 2010 Express с пакетом обновления 1 (SP1), который является бесплатной версией Microsoft Visual Studio. Прежде чем начать, убедитесь, что установлены предварительные требования, перечисленные ниже. Чтобы установить все эти компоненты, щелкните следующую ссылку: [установщик веб-платформы](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack). Кроме того, вы можете отдельно установить необходимые компоненты, используя следующие ссылки:
> 
> - [Предварительные требования для Visual Studio Web Developer Express SP1](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [Обновление инструментов ASP.NET MVC 3](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - [SQL Server Compact 4,0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(поддержка времени выполнения и средств)
> 
> Если вы используете Visual Studio 2010 вместо Visual Web Developer 2010, установите необходимые компоненты, щелкнув следующую ссылку: [Предварительные требования для Visual studio 2010](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack).
> 
> Для этого раздела доступен проект Visual C# Web Developer с исходным кодом. [Скачайте C# версию](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098). Если вы предпочитаете Visual Basic, переключитесь на [Visual Basic версию](../vb/intro-to-aspnet-mvc-3.md) этого учебника.

В этом разделе вы создадите новый класс `MoviesController` и запишете код, который извлекает данные фильмов и отображает их в браузере с помощью шаблона представления. Перед продолжением обязательно создайте приложение.

Щелкните правой кнопкой мыши папку *Controllers* и создайте новый контроллер `MoviesController`. Выберите следующие параметры.

- Имя контроллера: **MoviesController**. (Это значение по умолчанию. )
- Шаблон: **контроллер с действиями чтения и записи и представлениями с использованием Entity Framework**.
- Класс модели: **Movie (MvcMovie. Models)** .
- Класс контекста данных: **мовиедбконтекст (MvcMovie. Models)** .
- Представления: **Razor (CSHTML)** . (Значение по умолчанию.)

[![аддскаффолдедмовиеконтроллер](accessing-your-models-data-from-a-controller/_static/image2.png "аддскаффолдедмовиеконтроллер")](accessing-your-models-data-from-a-controller/_static/image1.png)

Нажмите кнопку **Добавить**. Visual Web Developer создает следующие файлы и папки:

- Файл *MoviesController.CS* в папке *Controllers* проекта.
- Папка *фильмов* в папке *views* проекта.
- В новой папке *Виевс\мовиес* *создаются. cshtml, DELETE. cshtml, Details. cshtml, Edit. cshtml*и *index. cshtml* .

[![невмовиеконтроллерскриншот](accessing-your-models-data-from-a-controller/_static/image4.png "невмовиеконтроллерскриншот")](accessing-your-models-data-from-a-controller/_static/image3.png)

Механизм формирования шаблонов ASP.NET MVC 3 автоматически создал для вас методы и представления действий CRUD (создание, чтение, обновление и удаление). Теперь у вас есть полнофункциональное веб-приложение, которое позволяет создавать, перечислять, изменять и удалять записи фильмов.

Запустите приложение и перейдите к контроллеру `Movies`, добавив */Movies* в URL-адрес в адресной строке браузера. Поскольку приложение полагается на маршрутизацию по умолчанию (определенную в файле *Global. asax* ), запрос браузера `http://localhost:xxxxx/Movies` направляется в метод действия `Index` по умолчанию контроллера `Movies`. Иными словами, `http://localhost:xxxxx/Movies` запроса браузера фактически аналогичен `http://localhost:xxxxx/Movies/Index`запроса браузера. Результатом является пустой список фильмов, так как вы еще не добавили их.

![](accessing-your-models-data-from-a-controller/_static/image5.png)

### <a name="creating-a-movie"></a>Создание фильма

Щелкните ссылку **Create New** (Создать). Введите некоторые сведения о фильме и нажмите кнопку **создать** .

![](accessing-your-models-data-from-a-controller/_static/image6.png)

Нажатие кнопки **создать** приводит к тому, что форма будет отправлена на сервер, где сведения о фильме будут сохранены в базе данных. Затем вы перейдете на URL-адрес */Movies* , на котором можно увидеть созданный фильм в списке.

[![индексвхенхарримет](accessing-your-models-data-from-a-controller/_static/image8.png "индексвхенхарримет")](accessing-your-models-data-from-a-controller/_static/image7.png)

Создайте еще несколько записей фильмов. Попробуйте воспользоваться ссылками **Изменить**, **Сведения** и **Удалить** — все они работают.

## <a name="examining-the-generated-code"></a>Проверка созданного кода

Откройте файл *контроллерс\мовиесконтроллер.КС* и изучите созданный метод `Index`. Ниже показана часть контроллера фильмов с методом `Index`.

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample1.cs)]

Следующая строка из класса `MoviesController` создает экземпляр контекста базы данных Movie, как описано выше. Для запроса, изменения и удаления фильмов можно использовать контекст базы данных Movie.

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample2.cs)]

Запрос к контроллеру `Movies` возвращает все записи в таблице `Movies` базы данных фильмов, а затем передает результаты в представление `Index`.

## <a name="strongly-typed-models-and-the-model-keyword"></a>Строго типизированные модели и ключевое слово @model

Ранее в этом руководстве вы узнали, как контроллер может передавать данные или объекты в шаблон представления с помощью объекта `ViewBag`. `ViewBag` — это динамический объект, предоставляющий удобный способ для передачи сведений в представление.

ASP.NET MVC также предоставляет возможность передавать строго типизированные данные или объекты в шаблон представления. Такой строго типизированный подход обеспечивает лучшую проверку кода во время компиляции и более широкие возможности IntelliSense в редакторе Visual Web Developer. Мы используем этот подход с шаблоном представления *index. cshtml* с классом `MoviesController`.

Обратите внимание, что код создает объект [`List`](https://msdn.microsoft.com/library/6sh2ey19.aspx) при вызове вспомогательного метода `View` в методе `Index` действия. Затем код передает этот список `Movies` из контроллера в представление:

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample3.cs)]

Включив инструкцию `@model` в верхней части файла шаблона представления, можно указать тип объекта, который предполагается отобразить в представлении. При создании контроллера фильмов Visual Web Developer автоматически включил в начало файла *index. cshtml* следующую инструкцию `@model`:

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample4.cshtml)]

Эта директива `@model` позволяет получить доступ к списку фильмов, переданных контроллером в представление, используя строго типизированный объект `Model`. Например, в шаблоне *index. cshtml* код проходит через фильмы, выполняя инструкцию `foreach` для строго типизированного объекта `Model`:

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample5.cshtml)]

Так как объект `Model` является строго типизированным (в виде объекта `IEnumerable<Movie>`), каждый объект `item` в цикле вводится как `Movie`. Помимо прочих преимуществ это означает, что во время компиляции кода и полной поддержки IntelliSense в редакторе кода вы получаете проверку.

[![моделинтеллисенсе](accessing-your-models-data-from-a-controller/_static/image10.png "моделинтеллисенсе")](accessing-your-models-data-from-a-controller/_static/image9.png)

## <a name="working-with-sql-server-compact"></a>Работа с SQL Server Compact

Entity Framework Code First обнаружила, что предоставленная строка подключения к базе данных указывала на базу данных `Movies`, которая еще не существовала, поэтому Code First автоматически создавала базу данных. Чтобы убедиться, что он создан, найдите в папке *приложение\_данные* . Если файл *movies. sdf* не отображается, нажмите кнопку " **Показать все файлы** " на панели инструментов **Обозреватель решений** , нажмите кнопку " **Обновить** ", а затем разверните папку " *приложение\_данные* ".

[![SDF_in_SolnExp](accessing-your-models-data-from-a-controller/_static/image12.png "SDF_in_SolnExp")](accessing-your-models-data-from-a-controller/_static/image11.png)

Дважды щелкните *movies. sdf* , чтобы открыть **Обозреватель сервера**. Затем разверните папку **таблицы** , чтобы просмотреть таблицы, созданные в базе данных.

> [!NOTE]
> Если при двойном щелчке на *movies. sdf*появляется сообщение об ошибке, убедитесь, что установлен [SQL Server Compact 4,0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(поддержка времени выполнения и средств). (Ссылки на программное обеспечение см. в списке предварительных требований в первой части этой серии руководств.) Если установить выпуск сейчас, необходимо закрыть и снова открыть Visual Web Developer.

[![DB_explorer](accessing-your-models-data-from-a-controller/_static/image14.png "DB_explorer")](accessing-your-models-data-from-a-controller/_static/image13.png)

Существует две таблицы, одна для `Movie` набора сущностей, а затем `EdmMetadata` таблицу. `EdmMetadata` таблица используется Entity Framework, чтобы определить, когда модель и база данных не синхронизированы.

Щелкните правой кнопкой мыши таблицу `Movies` и выберите **Показать данные таблицы** , чтобы просмотреть созданные данные.

[![мовиестабле](accessing-your-models-data-from-a-controller/_static/image16.png "мовиестабле")](accessing-your-models-data-from-a-controller/_static/image15.png)

Щелкните правой кнопкой мыши таблицу `Movies` и выберите **изменить схему таблицы**.

[![едиттаблесчема](accessing-your-models-data-from-a-controller/_static/image18.png "едиттаблесчема")](accessing-your-models-data-from-a-controller/_static/image17.png)

[![таблесчемасм](accessing-your-models-data-from-a-controller/_static/image20.png "таблесчемасм")](accessing-your-models-data-from-a-controller/_static/image19.png)

Обратите внимание, что схема `Movies` таблицы сопоставляется с созданным ранее классом `Movie`. Entity Framework Code First автоматически создали эту схему на основе класса `Movie`.

По завершении закройте подключение. (Если вы не закроете подключение, при следующем запуске проекта может появиться сообщение об ошибке).

[![клосеконнектион](accessing-your-models-data-from-a-controller/_static/image22.png "клосеконнектион")](accessing-your-models-data-from-a-controller/_static/image21.png)

Теперь у вас есть база данных и простая страница со списком для отображения содержимого из нее. В следующем руководстве мы рассмотрим оставшуюся часть кода с формированием шаблонов и добавим метод `SearchIndex` и представление `SearchIndex`, которое позволяет выполнять поиск фильмов в этой базе данных.

> [!div class="step-by-step"]
> [Назад](adding-a-model.md)
> [Вперед](examining-the-edit-methods-and-edit-view.md)
