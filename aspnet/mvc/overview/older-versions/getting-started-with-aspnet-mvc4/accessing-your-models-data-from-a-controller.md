---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc4/accessing-your-models-data-from-a-controller
title: Доступ к данным модели из контроллера | Документация Майкрософт
author: Rick-Anderson
description: Примечание. Обновленная версия этого учебника доступна здесь, в которой используется ASP.NET MVC 5 и Visual Studio 2013. Он более безопасен, гораздо проще в исполнении и демонстрации...
ms.author: riande
ms.date: 08/28/2012
ms.assetid: 61e0206d-7f32-4018-992d-0a51b48b37dc
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc4/accessing-your-models-data-from-a-controller
msc.type: authoredcontent
ms.openlocfilehash: 7c4aa34567ac4fb31d1ed874cf65986c4e779e66
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/19/2020
ms.locfileid: "77456170"
---
# <a name="accessing-your-models-data-from-a-controller"></a>Доступ к данным модели из контроллера

по [Рик Андерсон (](https://twitter.com/RickAndMSFT)

> > [!NOTE]
> > Обновленная версия этого учебника доступна [здесь](../../getting-started/introduction/getting-started.md) , в которой используется ASP.NET MVC 5 и Visual Studio 2013. Он более безопасен, гораздо проще следовать и демонстрирует дополнительные функции.

В этом разделе вы создадите новый класс `MoviesController` и запишете код, который извлекает данные фильмов и отображает их в браузере с помощью шаблона представления.

**Создайте приложение,** прежде чем переходить к следующему шагу.

Щелкните правой кнопкой мыши папку *Controllers* и создайте новый контроллер `MoviesController`. Указанные ниже параметры не отображаются, пока не будет построено приложение. Выберите следующие параметры.

- Имя контроллера: **MoviesController**. (Это значение по умолчанию. )
- Шаблон: **контроллер MVC с действиями чтения и записи и представлениями с использованием Entity Framework**.
- Класс модели: **Movie (MvcMovie. Models)** .
- Класс контекста данных: **мовиедбконтекст (MvcMovie. Models)** .
- Представления: **Razor (CSHTML)** . (Значение по умолчанию.)

![аддскаффолдедмовиеконтроллер](accessing-your-models-data-from-a-controller/_static/image1.png)

Нажмите кнопку **Добавить**. Visual Studio Express создает следующие файлы и папки:

- Файл *MoviesController.CS* в папке *Controllers* проекта.
- Папка *фильмов* в папке *views* проекта.
- В новой папке *Виевс\мовиес* *создаются. cshtml, DELETE. cshtml, Details. cshtml, Edit. cshtml*и *index. cshtml* .

ASP.NET MVC 4 автоматически создал методы и представления действия CRUD (создание, чтение, обновление и удаление) для вас (автоматическое создание методов и представлений действий CRUD называется формированием шаблонов). Теперь у вас есть полнофункциональное веб-приложение, которое позволяет создавать, перечислять, изменять и удалять записи фильмов.

Запустите приложение и перейдите к контроллеру `Movies`, добавив */Movies* в URL-адрес в адресной строке браузера. Поскольку приложение полагается на маршрутизацию по умолчанию (определенную в файле *Global. asax* ), запрос браузера `http://localhost:xxxxx/Movies` направляется в метод действия `Index` по умолчанию контроллера `Movies`. Иными словами, `http://localhost:xxxxx/Movies` запроса браузера фактически аналогичен `http://localhost:xxxxx/Movies/Index`запроса браузера. Результатом является пустой список фильмов, так как вы еще не добавили их.

![](accessing-your-models-data-from-a-controller/_static/image2.png)

### <a name="creating-a-movie"></a>Создание фильма

Щелкните ссылку **Create New** (Создать). Введите некоторые сведения о фильме и нажмите кнопку **создать** .

![](accessing-your-models-data-from-a-controller/_static/image3.png)

Нажатие кнопки **создать** приводит к тому, что форма будет отправлена на сервер, где сведения о фильме будут сохранены в базе данных. Затем вы перейдете на URL-адрес */Movies* , на котором можно увидеть созданный фильм в списке.

![индексвхенхарримет](accessing-your-models-data-from-a-controller/_static/image4.png "индексвхенхарримет")

Создайте еще несколько записей фильмов. Попробуйте воспользоваться ссылками **Изменить**, **Сведения** и **Удалить** — все они работают.

## <a name="examining-the-generated-code"></a>Проверка созданного кода

Откройте файл *контроллерс\мовиесконтроллер.КС* и изучите созданный метод `Index`. Ниже показана часть контроллера фильмов с методом `Index`.

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample1.cs)]

Следующая строка из класса `MoviesController` создает экземпляр контекста базы данных Movie, как описано выше. Для запроса, изменения и удаления фильмов можно использовать контекст базы данных Movie.

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample2.cs)]

Запрос к контроллеру `Movies` возвращает все записи в таблице `Movies` базы данных фильмов, а затем передает результаты в представление `Index`.

## <a name="strongly-typed-models-and-the-model-keyword"></a>Строго типизированные модели и ключевое слово @model

Ранее в этом руководстве вы узнали, как контроллер может передавать данные или объекты в шаблон представления с помощью объекта `ViewBag`. `ViewBag` — это динамический объект, предоставляющий удобный способ для передачи сведений в представление.

ASP.NET MVC также предоставляет возможность передавать строго типизированные данные или объекты в шаблон представления. Такой строго типизированный подход обеспечивает лучшую проверку кода во время компиляции и более широкие возможности IntelliSense в редакторе Visual Studio. Механизм формирования шаблонов в Visual Studio использовал этот подход с классом `MoviesController` и шаблонами представления при создании методов и представлений.

В файле *контроллерс\мовиесконтроллер.КС* изучите созданный метод `Details`. Ниже показана часть контроллера фильмов с методом `Details`.

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample3.cs?highlight=3,8)]

Если `Movie` найден, экземпляр модели `Movie` передается в представление Details. Изучите содержимое файла *виевс\мовиес\детаилс.кштмл* .

Включив инструкцию `@model` в верхней части файла шаблона представления, можно указать тип объекта, который предполагается отобразить в представлении. При создании контроллера movie Visual Studio автоматически включает следующий оператор `@model` в начало файла *Details.cshtml*:

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample4.cshtml)]

Эта директива `@model` обеспечивает доступ к фильму, который контроллер передал в представление с использованием строго типизированного объекта `Model`. Например, в шаблоне *Details. cshtml* код передает каждое поле movie в `DisplayNameFor` и [DisplayFor](https://msdn.microsoft.com/library/system.web.mvc.html.displayextensions.displayfor(VS.98).aspx) вспомогательные методы HTML с помощью строго типизированного объекта `Model`. Методы Create и Edit и шаблоны представлений также передают объект модели фильма.

Изучите шаблон представления *index. cshtml* и метод `Index` в файле *MoviesController.CS* . Обратите внимание, что код создает объект [`List`](https://msdn.microsoft.com/library/6sh2ey19.aspx) при вызове вспомогательного метода `View` в методе `Index` действия. Затем код передает этот список `Movies` из контроллера в представление:

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample5.cs?highlight=3)]

При создании контроллера Movie Visual Studio Express автоматически включил следующую инструкцию `@model` в начало файла *index. cshtml* :

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample6.cshtml)]

Эта директива `@model` позволяет получить доступ к списку фильмов, переданных контроллером в представление, используя строго типизированный объект `Model`. Например, в шаблоне *index. cshtml* код проходит через фильмы, выполняя инструкцию `foreach` для строго типизированного объекта `Model`:

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample7.cshtml?highlight=1,4,7,10,13,16,19-21)]

Так как объект `Model` является строго типизированным (в виде объекта `IEnumerable<Movie>`), каждый объект `item` в цикле вводится как `Movie`. Помимо прочих преимуществ это означает, что во время компиляции кода и полной поддержки IntelliSense в редакторе кода вы получаете проверку.

![моделинтеллисенсе](accessing-your-models-data-from-a-controller/_static/image5.png)

## <a name="working-with-sql-server-localdb"></a>Работа с SQL Server LocalDB

Entity Framework Code First обнаружила, что предоставленная строка подключения к базе данных указывала на базу данных `Movies`, которая еще не существовала, поэтому Code First автоматически создавала базу данных. Чтобы убедиться, что он создан, найдите в папке *приложение\_данные* . Если файл *movies. mdf* не отображается, нажмите кнопку " **Показать все файлы** " на панели инструментов **Обозреватель решений** , нажмите кнопку " **Обновить** ", а затем разверните папку " *приложение\_данные* ".

![](accessing-your-models-data-from-a-controller/_static/image6.png)

Дважды щелкните *movies. mdf* , чтобы открыть **Обозреватель баз данных**, а затем разверните папку **таблицы** , чтобы просмотреть таблицу фильмов.

![DB_explorer](accessing-your-models-data-from-a-controller/_static/image7.png "DB_explorer")

> [!NOTE]
> Если обозреватель баз данных не отображается, в меню **Сервис** выберите **подключиться к базе данных**, а затем отменяет диалоговое окно **Выбор источника данных** . Это приведет к принудительному открытию обозревателя баз данных.

> [!NOTE]
> Если вы используете VWD или Visual Studio 2010 и получаете ошибку, похожую на одну из следующих:
> 
> - База данных "C:\Webs\MVC4\MVCMOVIE\MVCMOVIE\APP\_ДАТА\МОВИЕС. Невозможно открыть MDF, так как он имеет версию 706. Этот сервер поддерживает версию 655 и более ранние. Переход на предыдущую версию не поддерживается.
> - &quot;исключение InvalidOperation не обработано пользовательским кодом&quot; в предоставленном объекте SqlConnection не указан исходный каталог.
> 
> Необходимо установить [SQL Server Data Tools](https://blogs.msdn.com/b/rickandy/archive/2012/08/02/installing-and-using-sql-server-data-tools-ssdt-on-visual-studio-2010-and-vwd.aspx) и [LocalDB](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLLocalDBOnly_11_0). Проверьте строку подключения `MovieDBContext`, указанную на предыдущей странице.

Щелкните правой кнопкой мыши таблицу `Movies` и выберите **Показать данные таблицы** , чтобы просмотреть созданные данные.

![](accessing-your-models-data-from-a-controller/_static/image8.png)

Щелкните правой кнопкой мыши таблицу `Movies` и выберите **Open Table Definition (Открыть определение таблицы** ), чтобы увидеть структуру таблицы, которая Entity Framework Code First создана.

![](accessing-your-models-data-from-a-controller/_static/image9.png "MoviesTable")

![](accessing-your-models-data-from-a-controller/_static/image10.png)

Обратите внимание, что схема `Movies` таблицы сопоставляется с созданным ранее классом `Movie`. Entity Framework Code First автоматически создали эту схему на основе класса `Movie`.

По завершении закройте подключение, щелкнув правой кнопкой мыши *мовиедбконтекст* и выбрав **закрыть подключение**. (Если вы не закроете подключение, при следующем запуске проекта может появиться сообщение об ошибке).

![](accessing-your-models-data-from-a-controller/_static/image11.png "CloseConnection")

Теперь у вас есть база данных и простая страница со списком для отображения содержимого из нее. В следующем руководстве мы рассмотрим оставшуюся часть кода с формированием шаблонов и добавим метод `SearchIndex` и представление `SearchIndex`, которое позволяет выполнять поиск фильмов в этой базе данных.

> [!div class="step-by-step"]
> [Назад](adding-a-model.md)
> [Вперед](examining-the-edit-methods-and-edit-view.md)
