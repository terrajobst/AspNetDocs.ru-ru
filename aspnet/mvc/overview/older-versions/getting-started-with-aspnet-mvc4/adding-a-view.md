---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-a-view
title: Добавление представления | Документация Майкрософт
author: Rick-Anderson
description: Примечание. Обновленную версию этого учебника доступен здесь, использующий ASP.NET MVC 5 и Visual Studio 2013. Это более безопасное и гораздо проще выполнить и демонстрационных версий...
ms.author: riande
ms.date: 08/28/2012
ms.assetid: dde851d7-882e-4d99-9b96-cf96daed81cc
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-a-view
msc.type: authoredcontent
ms.openlocfilehash: 7b55a55db6207b8ff18b2dd207e919cee45f6973
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57030381"
---
<a name="adding-a-view"></a>Добавление представления
====================
по [Рик Андерсон]((https://twitter.com/RickAndMSFT))

> > [!NOTE]
> > Обновленную версию этого учебника доступен [здесь](../../getting-started/introduction/getting-started.md) , использующий ASP.NET MVC 5 и Visual Studio 2013. Она более безопасные, гораздо проще следовать и показаны дополнительные возможности.


В этом разделе вы собираетесь изменить `HelloWorldController` класса для использования представления, файлы шаблонов для отчетливой инкапсуляции процесса создания HTML-ответов клиенту.

Вы создадите файл шаблона представления с помощью [представлений Razor](https://weblogs.asp.net/scottgu/archive/2010/07/02/introducing-razor.aspx) появилась в ASP.NET MVC 3. Шаблоны представления на основе Razor имеют *.cshtml* расширение файла, а также реализуют удобный способ для создания выходных данных с помощью C# HTML. Razor позволяет свести к минимуму число знаков и нажатий клавиш при написании шаблона представления, а также позволяет быстро, жидкостей, рабочие процессы кодирования.

На данный момент метод `Index` возвращает строку с сообщением, которое жестко задано в классе контроллера. Изменение `Index` метод для возврата `View` объекта, как показано в следующем коде:

[!code-csharp[Main](adding-a-view/samples/sample1.cs)]

`Index` Описанный выше метод использует шаблон представления для создания HTML-ответа в браузер. Методы контроллера (также известный как [методы действий](http://rachelappel.com/asp.net-mvc-actionresults-explained)), такие как `Index` метод выше, обычно возвращают [ActionResult](https://msdn.microsoft.com/library/system.web.mvc.actionresult.aspx) (или класс, производный от [ActionResult](https://msdn.microsoft.com/library/system.web.mvc.actionresult.aspx)), не примитивные типы, такие как строки.

В проекте, добавьте шаблон представления, можно использовать с `Index` метод. Чтобы сделать это, щелкните правой кнопкой мыши внутри `Index` метод и нажмите кнопку **Добавление представления**.

![](adding-a-view/_static/image1.png)

**Добавление представления** откроется диалоговое окно. Оставьте значения по умолчанию способ их и нажмите кнопку **добавить** кнопки:

![](adding-a-view/_static/image2.png)

*MvcMovie\Views\HelloWorld* папки и *MvcMovie\Views\HelloWorld\Index.cshtml* создаются файл. Вы можете увидеть их в **обозревателе решений**:

![](adding-a-view/_static/image3.png)

Ниже *Index.cshtml* файл, который был создан:

![HelloWorldIndex](adding-a-view/_static/image4.png)

Добавьте следующий код HTML в разделе `<h2>` тега.

[!code-html[Main](adding-a-view/samples/sample2.html)]

Полный *MvcMovie\Views\HelloWorld\Index.cshtml* файла приведен ниже.

[!code-cshtml[Main](adding-a-view/samples/sample3.cshtml?highlight=7-8)]

Если вы используете Visual Studio 2012, в обозревателе решений, щелкните правой кнопкой мыши *Index.cshtml* файл и выберите **просмотреть в инспекторе страниц**.

![PI](adding-a-view/_static/image5.png)

[Инспектор страниц руководства](../../views/using-page-inspector-in-aspnet-mvc.md) содержит дополнительные сведения об использовании этого нового инструмента.

Кроме того, запустите приложение и перейдите к `HelloWorld` контроллера (`http://localhost:xxxx/HelloWorld`). `Index` Метод в контроллере не делать много работы; он просто выполнил оператор `return View()`, которой указано, что метод должен использовать файл шаблона представления для отображения ответа в браузер. Так как имя файла шаблона представления для использования не был указан явным образом, ASP.NET MVC по умолчанию использует *Index.cshtml* просмотреть файл в *\Views\HelloWorld* папки. На рисунке ниже показана строка &quot;Hello from our View Template!&quot; жестко в представлении.

![](adding-a-view/_static/image6.png)

Выглядит довольно хорошо. Обратите внимание, что в строке заголовка браузера отображается &quot;индекса объект My ASP.NET&quot; и появляется надпись больших ссылку верхней части страницы &quot;ваша эмблема здесь.&quot; Ниже &quot;здесь ваш логотип.&quot; ссылку около, регистрации и журналов в ссылки и ниже, ссылающийся на домашнюю страницу и страницу контактов. Давайте изменим некоторые из них.

## <a name="changing-views-and-layout-pages"></a>Изменение представления и макета страницы

Во-первых, необходимо изменить &quot;здесь ваш логотип.&quot; заголовок в верхней части страницы. Этот текст является общим для каждой страницы. Фактически она реализуется только в одном месте в проекте, несмотря на то, что он отображается на каждой странице в приложении. Перейдите к */Views/Shared* папку в **обозревателе решений** и откройте  *\_Layout.cshtml* файла. Этот файл называется *страницы макета* и общей &quot;оболочки&quot; , использовать другие страницы.

![_LayoutCshtml](adding-a-view/_static/image7.png)

Шаблоны макета позволяют задать макет контейнера HTML для узла в одном месте, а затем применять их на разных страницах сайта. Найдите строку `@RenderBody()`. `RenderBody` — это заполнитель, в котором отображаются все создаваемые страницы для определенных представлений, &quot;упакованные&quot; на странице макета. Например, если щелкнуть ссылку About *Views\Home\About.cshtml* представление отображается внутри `RenderBody` метод.

Измените заголовок название узла в шаблоне макета с &quot;ваша эмблема здесь&quot; для &quot;MVC Movie&quot;.

[!code-cshtml[Main](adding-a-view/samples/sample4.cshtml)]

Замените содержимое элемента title следующую разметку:

[!code-cshtml[Main](adding-a-view/samples/sample5.cshtml)]

Запустите приложение и обратите внимание, что теперь отображается надпись &quot;MVC Movie &quot;. Нажмите кнопку **о** ссылку чтобы увидеть, каким образом эта страница показывает &quot;MVC Movie&quot;, слишком. Мы смогли сделать один раз в шаблон макета и быть всех страниц на сайте с учетом новый заголовок.

![](adding-a-view/_static/image8.png)

Теперь изменим заголовок в представление Index.

Откройте *MvcMovie\Views\HelloWorld\Index.cshtml*. Чтобы внести изменения в двух местах: во-первых, текст, расположенный в заголовке браузера, а затем в дополнительный заголовок ( `<h2>` элемент). Сделайте их немного разными, чтобы видеть, какой именно фрагмент кода изменяет соответствующую часть приложения.

[!code-cshtml[Main](adding-a-view/samples/sample6.cshtml)]

Для указания заголовка HTML для отображения, приведенном выше коде присваивает `Title` свойство `ViewBag` объекта (который находится в *Index.cshtml* Просмотр шаблона). Если взглянуть на исходный код в шаблон макета, можно заметить, что в шаблоне используется это значение в `<title>` элемент как часть `<head>` части HTML, мы изменили ранее. С помощью этого `ViewBag` подход, вы можете легко передавать другие параметры между представление шаблона, а файл макета.

Запустите приложение и перейдите к `http://localhost:xx/HelloWorld`. Обратите внимание, что основной и дополнительный заголовки браузера изменились. (Если изменения не отображаются, возможно, вы просматриваете кэшированное содержимое. В этом случае нажмите в браузере клавиши CTRL+F5 для принудительной загрузки ответа сервера.) Заголовок браузера создается с помощью `ViewBag.Title` задается *Index.cshtml* Просмотр шаблона и дополнительной &quot;-Movie App&quot; добавлен в файл макета.

Также Обратите внимание, каким образом содержимого в *Index.cshtml* Просмотр шаблона была объединена с  *\_Layout.cshtml* шаблон представления и один ответ HTML был отправлен в браузер. С помощью шаблонов макета можно легко вносить изменения, которые применяются ко всем страницам приложения.

![](adding-a-view/_static/image9.png)

Небольшой фрагмент &quot;данных&quot; (в данном случае &quot;Hello from our View Template!&quot; сообщения) задано жестко, однако. Приложение MVC предоставляет &quot;V&quot; (представление) и у вас есть &quot;C&quot; (контроллер), но не &quot;M&quot; (модель). еще. Чуть ниже мы рассмотрим создание базы данных и получать данные модели из нее.

## <a name="passing-data-from-the-controller-to-the-view"></a>Передача данных из контроллера в представление

Прежде чем мы перейдите к базе данных и поговорим о моделях, но давайте сперва поговорим о передачи данных из контроллера в представление. Классы контроллера вызываются в ответ на входящий запрос URL-адрес. Класс контроллера пишется код, который обрабатывает входящие браузер запрашивает, извлекает данные из базы данных и в конечном итоге определяет тип ответа для отправки обратно в браузер. Просмотр шаблонов может использоваться из контроллера для создания и форматирования ответа HTML в браузере.

Контроллеры — отвечает за предоставление независимо от используемых данных и объектов необходимых для шаблона представления для отображения ответа в браузер. Рекомендации: **Шаблон представления никогда не следует выполнять бизнес-логику или напрямую взаимодействовать с базой данных**. Вместо этого они должны работать только с данными, предоставляется к ней с помощью контроллера. Для обслуживания таких &quot;Разделение областей ответственности&quot; позволяет поддерживать код очистки, пригодного для тестирования и поддержки.

В настоящее время `Welcome` метода действия в `HelloWorldController` класса принимает `name` и `numTimes` параметр, после чего выводит значения непосредственно в браузере. Вместо отображения ответа в виде строки, настроим контроллер для использования шаблона представления. Шаблон представления создаст динамический ответ, для получения которого необходимо передать соответствующие фрагменты данных из контроллера в представление. Это можно сделать за счет этого контроллер может поместить динамические данные (параметры), которые требуются шаблону представления в `ViewBag` объект, который может получить доступ к шаблону представления.

Вернитесь к *HelloWorldController.cs* файлов и изменить `Welcome` метод, чтобы добавить `Message` и `NumTimes` значение `ViewBag` объекта. `ViewBag` является динамическим объектом, это означает, что угодно можно поместить в него данные; `ViewBag` объект не имеет определенных свойств до помещен внутри него. [Система привязки модели ASP.NET MVC](http://odetocode.com/Blogs/scott/archive/2009/04/27/6-tips-for-asp-net-mvc-model-binding.aspx) автоматически сопоставляет именованные параметры (`name` и `numTimes`) из строки запроса в адресной строке, чтобы параметрами метода. Полный файл *HelloWorldController.cs* выглядит следующим образом:

[!code-csharp[Main](adding-a-view/samples/sample7.cs)]

Теперь `ViewBag` объект содержит данные, которые будут переданы в представление автоматически.

Далее необходимо шаблон представления экрана приветствия! В **построения** меню, выберите **построения MvcMovie** чтобы убедиться, что проект скомпилирован.

Щелкните правой кнопкой мыши внутри `Welcome` метод и нажмите кнопку **Добавление представления**.

![](adding-a-view/_static/image10.png)

Вот что **Добавление представления** диалоговое окно выглядит как:

![](adding-a-view/_static/image11.png)

Нажмите кнопку **добавить**, а затем добавьте следующий код под `<h2>` элемент в новом *Welcome.cshtml* файла. Вы создадите цикл, который говорит &quot;Hello&quot; столько раз, сколько пользователь говорит должно. Полный *Welcome.cshtml* файла приведен ниже.

[!code-cshtml[Main](adding-a-view/samples/sample8.cshtml)]

Запустите приложение и перейдите к следующему URL-АДРЕСУ:

`http://localhost:xx/HelloWorld/Welcome?name=Scott&numtimes=4`

Теперь данные из URL-адрес и передаются в контроллер с помощью [связывателя модели](http://odetocode.com/Blogs/scott/archive/2009/04/27/6-tips-for-asp-net-mvc-model-binding.aspx). Контроллер упаковывает данные в `ViewBag` объект и передает этот объект в представление. Затем в представлении отображаются данные как HTML для пользователя.

![](adding-a-view/_static/image12.png)

В приведенном выше примере мы использовали `ViewBag` объект для передачи данных из контроллера в представление. Последнее в этом руководстве, мы будем использовать модель представления для передачи данных из контроллера в представление. Представление модели способ передачи данных является предпочтительным по подход контейнер представления. См. в записи блога [динамические V строго типизированные представления](https://blogs.msdn.com/b/rickandy/archive/2011/01/28/dynamic-v-strongly-typed-views.aspx) Дополнительные сведения.

Ну, подход из &quot;M&quot; для модели, а не тип базы данных. Итак, обобщим все полученные данные и попробуем создать базу данных фильмов.

> [!div class="step-by-step"]
> [Назад](adding-a-controller.md)
> [Вперед](adding-a-model.md)