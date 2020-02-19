---
uid: mvc/overview/getting-started/introduction/examining-the-edit-methods-and-edit-view
title: Проверка методов Edit и режима правки | Документация Майкрософт
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 01/06/2019
ms.assetid: 52a4d5fe-aa31-4471-b3cb-a064f82cb791
msc.legacyurl: /mvc/overview/getting-started/introduction/examining-the-edit-methods-and-edit-view
msc.type: authoredcontent
ms.openlocfilehash: 6cef963910b957e8b4ad7c7909385f6dbdff95c1
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/19/2020
ms.locfileid: "77456067"
---
# <a name="examining-the-edit-methods-and-edit-view"></a>Изучение методов Edit и представления Edit

по [Рик Андерсон (](https://twitter.com/RickAndMSFT)

[!INCLUDE [Tutorial Note](index.md)]

В этом разделе вы изучите созданные методы и представления действий `Edit` для контроллера фильмов. Но сначала мы будем использовать сокращенную версию, чтобы сделать дату выпуска более эффективной. Откройте файл *моделс\мовие.КС* и добавьте выделенные строки, показанные ниже:

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample1.cs?highlight=2,12-14)]

Кроме того, можно сделать так, чтобы культура даты была такой:

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample2.cs?highlight=3)]

Пространство имен [DataAnnotations](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx) будет рассмотрено в следующем учебнике. Атрибут [Display](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayattribute.aspx) определяет отображаемое имя поля (в этом случае "Release Date" вместо "ReleaseDate"). Атрибут [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx) указывает тип данных, в данном случае это дата, поэтому сведения о времени, хранящиеся в поле, не отображаются. Атрибут [DisplayFormat](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx) необходим для ошибки в браузере Chrome, которая неправильно отображает форматы даты.

Запустите приложение и перейдите к контроллеру `Movies`. Наведите указатель мыши на ссылку **Edit (изменить** ), чтобы просмотреть URL-адрес, на который он ссылается.

![EditLink_sm](examining-the-edit-methods-and-edit-view/_static/image1.png)

Ссылка для **редактирования** была создана методом `Html.ActionLink` в представлении *виевс\мовиес\индекс.кштмл* :

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample3.cshtml)]

![HTML. ActionLink](examining-the-edit-methods-and-edit-view/_static/image2.png)

Объект `Html` является вспомогательным объектом, который предоставляется с помощью свойства в базовом классе [System. Web. MVC. вебвиевпаже](https://msdn.microsoft.com/library/gg402107(VS.98).aspx) . Метод `ActionLink` вспомогательного метода позволяет легко динамически создавать гиперссылки HTML, которые связываются с методами действий на контроллерах. Первым аргументом метода `ActionLink` является отображаемый текст ссылки (например, `<a>Edit Me</a>`). Вторым аргументом является имя вызываемого метода действия (в данном случае `Edit` действие). Последний аргумент — это [Анонимный объект](https://weblogs.asp.net/scottgu/archive/2007/05/15/new-orcas-language-feature-anonymous-types.aspx) , создающий данные маршрута (в данном случае — идентификатор 4).

Созданная ссылка, показанная на предыдущем рисунке, `http://localhost:1234/Movies/Edit/4`. Маршрут по умолчанию (установленный в *App\_старт\раутеконфиг.КС*) принимает шаблон URL-адреса `{controller}/{action}/{id}`. Таким образом, ASP.NET преобразует `http://localhost:1234/Movies/Edit/4` в запрос метода действия `Edit` контроллера `Movies` с параметром `ID`, равным 4. Изучите следующий код из файла *App\_старт\раутеконфиг.КС* . Метод [файл MapRoute](../../older-versions-1/controllers-and-routing/asp-net-mvc-routing-overview-cs.md) используется для маршрутизации HTTP-запросов к правильному контроллеру и методу действия и указания необязательного параметра ID. Метод [файл MapRoute](../../older-versions-1/controllers-and-routing/asp-net-mvc-routing-overview-cs.md) также используется [хтмлхелперс](https://msdn.microsoft.com/library/system.web.mvc.htmlhelper(v=vs.108).aspx) , например `ActionLink` для создания URL-адресов с учетом контроллера, метода действия и всех данных маршрута.

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample4.cs?highlight=7)]

Можно также передать параметры метода действия с помощью строки запроса. Например, URL-адрес `http://localhost:1234/Movies/Edit?ID=3` также передает параметр `ID` из 3 в метод `Edit` действия контроллера `Movies`.

![едиткуеристринг](examining-the-edit-methods-and-edit-view/_static/image3.png)

Откройте контроллер `Movies`. Ниже показаны два метода действий `Edit`.

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample5.cs?highlight=19-21)]

Обратите внимание на второй метод действия `Edit`, которому предшествует атрибут `HttpPost`. Этот атрибут указывает, что перегрузка метода `Edit` может быть вызвана только для запросов POST. Можно применить атрибут `HttpGet` к первому методу Edit, но это необязательно, так как это значение по умолчанию. (Мы будем называть методы действий, которым неявно назначается атрибут `HttpGet` как методы `HttpGet`.) Атрибут [BIND](https://msdn.microsoft.com/library/system.web.mvc.bindattribute(v=vs.108).aspx) является еще одним важным механизмом безопасности, который позволяет злоумышленникам переключать данные в вашу модель. В атрибут BIND, который требуется изменить, должны быть включены только свойства. Вы можете ознакомиться с перезаписью и атрибутом BIND в [примечании безопасности при перезаписи](https://go.microsoft.com/fwlink/?LinkId=317598). В простой модели, используемой в этом учебнике, мы будем привязать все данные в модели. Атрибут [ValidateAntiForgeryToken](https://msdn.microsoft.com/library/system.web.mvc.validateantiforgerytokenattribute(v=vs.108).aspx) используется для предотвращения подделки запроса и связывания с `@Html.AntiForgeryToken()` в файле представления редактирования (*виевс\мовиес\едит.кштмл*), часть показана ниже.

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample6.cshtml?highlight=9)]

`@Html.AntiForgeryToken()` создает маркер скрытой подделки формы, который должен соответствовать методу `Edit` контроллера `Movies`. Дополнительные сведения о подделке межсайтовых запросов (также известном как XSRF или CSRF) см. в статье мой учебник [XSRF/CSRF предотвращение в MVC](../../security/xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages.md).

Метод `HttpGet` `Edit` принимает параметр идентификатора фильма, выполняет поиск фильма с помощью метода Entity Framework `Find` и возвращает выбранный фильм в представление редактирования. Если фильм не удается найти, возвращается [хттпнотфаунд](https://msdn.microsoft.com/library/gg453938(VS.98).aspx) . Если в представлении редактирования создана система формирования шаблонов, она проверяет класс `Movie` и создает код для отображения элементов `<label>` и `<input>` для каждого свойства класса. В следующем примере показано представление редактирования, созданное системой формирования шаблонов Visual Studio:

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample7.cshtml)]

Обратите внимание, что в шаблоне представления имеется оператор `@model MvcMovie.Models.Movie` в верхней части файла — это указывает, что представление ожидает, что модель шаблона представления будет иметь тип `Movie`.

Сформированный код использует несколько *вспомогательных методов* для упрощения разметки HTML. В вспомогательном модуле [`Html.LabelFor`](https://msdn.microsoft.com/library/gg401864(VS.98).aspx) отображается имя поля (&quot;заголовок&quot;, &quot;ReleaseDate&quot;, &quot;жанр&quot;или &quot;Price&quot;). Вспомогательный метод [`Html.EditorFor`](https://msdn.microsoft.com/library/system.web.mvc.html.editorextensions.editorfor(VS.98).aspx) визуализирует HTML-элемент `<input>`. В вспомогательном модуле [`Html.ValidationMessageFor`](https://msdn.microsoft.com/library/system.web.mvc.html.validationextensions.validationmessagefor(VS.98).aspx) отображаются все сообщения проверки, связанные с этим свойством.

Запустите приложение и перейдите по URL-адресу */Movies* . Щелкните ссылку **Edit** (Изменить). Просмотрите исходный код страницы в окне браузера. Ниже показан HTML-код для элемента Form.

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample8.cshtml?highlight=1-2)]

Элементы `<input>` находятся в HTML-элементе `<form>`, атрибут `action` которого имеет значение POST к URL-адресу */мовиес/едит* . Данные формы будут отправлены на сервер при нажатии кнопки **сохранить** . Во второй строке показан скрытый токен [XSRF](../../security/xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages.md) , созданный вызовом `@Html.AntiForgeryToken()`.

## <a name="processing-the-post-request"></a>Обработка запроса POST

В следующем листинге демонстрируется версия `HttpPost` метода действия `Edit`.

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample9.cs)]

Атрибут [ValidateAntiForgeryToken](https://msdn.microsoft.com/library/system.web.mvc.validateantiforgerytokenattribute(v=vs.108).aspx) проверяет токен [XSRF](../../security/xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages.md) , созданный `@Html.AntiForgeryToken()`ным вызовом в представлении.

[Связыватель модели MVC ASP.NET](https://msdn.microsoft.com/library/dd410405.aspx) принимает значения отправленной формы и создает объект `Movie`, который передается как параметр `movie`. `ModelState.IsValid` проверяет, что данные, отправленные в форме, можно использовать для изменения (изменения или обновления) объекта `Movie`. Если данные являются допустимыми, данные фильмов сохраняются в `Movies` коллекции `db`(`MovieDBContext` экземпляр). Новые данные фильмов сохраняются в базе данных путем вызова метода `SaveChanges` `MovieDBContext`. После сохранения данных код перенаправляет пользователя в метод действия `Index` класса `MoviesController`, который отображает коллекцию фильмов с учетом только что внесенных изменений.

Как только проверка на стороне клиента определит, что значение поля недопустимо, выводится сообщение об ошибке. Если JavaScript отключен, проверка на стороне клиента отключена. Однако сервер обнаруживает, что отправленные значения недопустимы, а значения формы повторно отображаются с сообщениями об ошибках.

Проверка рассматривается более подробно далее в этом руководстве.

Вспомогательные методы `Html.ValidationMessageFor` в шаблоне представления *Edit. cshtml* отвечают за отображение соответствующих сообщений об ошибках.

![абкнотвалид](examining-the-edit-methods-and-edit-view/_static/image4.png)

Все методы `HttpGet` соответствуют аналогичному шаблону. Они получают объект Movie (или список объектов, в случае `Index`) и передают модель в представление. Метод `Create` передает пустой объект Movie в представление Create. Все методы, которые создают, редактируют, удаляют или иным образом изменяют данные, делают это в перегрузке метода `HttpPost`. Изменение данных в методе HTTP GET является угрозой безопасности, как описано в записи блога [совет ASP.NET #46 — не использовать ссылки DELETE, так как они создают бреши в системе безопасности](http://stephenwalther.com/blog/archive/2009/01/21/asp.net-mvc-tip-46-ndash-donrsquot-use-delete-links-because.aspx). Изменение данных в методе GET также нарушает рекомендации по протоколу HTTP и шаблон архитектуры [RESTful](http://en.wikipedia.org/wiki/Representational_State_Transfer) , указывающий, что запросы GET не должны изменять состояние приложения. Другими словами, операция GET должна выполняться безопасным способом, то есть не иметь побочных эффектов и не изменять существующие данные.

## <a name="jquery-validation-for-non-english-locales"></a>проверка jQuery для национальных стандартов, отличных от английского

Если используется компьютер с английским языком США, можно пропустить этот раздел и перейти к следующему руководству. Версию этого учебника для глобализации можно скачать [здесь](https://archive.msdn.microsoft.com/Project/Download/FileDownload.aspx?ProjectName=aspnetmvcsamples&amp;DownloadId=16475). Отличные два этапа учебника по интернационализации см. в разделе [надим ASP.NET MVC 5 International интернационализации](http://afana.me/post/aspnet-mvc-internationalization.aspx).

> [!NOTE]
> для поддержки проверки jQuery для национальных стандартов, отличных от английского, которые используют запятую (&quot;,&quot;) для десятичной запятой и форматы даты, отличные от US-English, необходимо включить *глобализацию. js* и определенные *языки и региональные параметры/глобализации. js* (из [https://github.com/jquery/globalize](https://github.com/jquery/globalize) ) и JavaScript для использования `Globalize.parseFloat`. Вы можете получить неанглоязычные проверки jQuery в NuGet. (Не устанавливайте глобализацию, если используется английский язык).

1. В меню **Сервис** выберите **Диспетчер пакетов NuGet**, а затем щелкните **Управление пакетами NuGet для решения**.

    ![](examining-the-edit-methods-and-edit-view/_static/image5.png)
2. На левой панели нажмите кнопку <strong>Обзор *.</strong>*  (См. изображение ниже.)
3. В поле ввода введите * глобализация * *.

    ![](examining-the-edit-methods-and-edit-view/_static/image6.png) выберите `jQuery.Validation.Globalize`, выберите `MvcMovie` и нажмите кнопку **установить**. Файл *скриптс\жкуери.глобализе\глобализе.ЖС* будет добавлен в проект. Папка * Скриптс\жкуери.глобализе\културес\* будет содержать множество файлов JavaScript языка и региональных параметров. Обратите внимание, что установка этого пакета может занять пять минут.

   В следующем коде показаны изменения в файле Виевс\мовиес\едит.кштмл:

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample10.cshtml)]

Чтобы избежать повторения этого кода в каждом представлении редактирования, его можно переместить в файл макета. Сведения о том, как оптимизировать загрузку скрипта, см. в разделе мой учебник [объединение и минификации](../../performance/bundling-and-minification.md).

Дополнительные сведения см. в статье [ASP.NET MVC 3 International](http://afana.me/post/aspnet-mvc-internationalization.aspx) и [ASP.NET MVC 3 internationaling-Part 2 (NerdDinner)](http://afana.me/post/aspnet-mvc-internationalization-part-2.aspx).

Как временное исправление, если вы не можете выполнить проверку в Вашем языковом стандарте, можно принудительно настроить компьютер на использование английского языка (США) или отключить JavaScript в браузере. Чтобы заставить компьютер использовать английский язык (США), можно добавить элемент Globalization в корневой файл *Web. config* проекта. В следующем коде показан элемент globalization с культурой, заданной США английским.

[!code-xml[Main](examining-the-edit-methods-and-edit-view/samples/sample11.xml)]

<a id="gettingstarted"></a><a id="jQueryAjaxJSON"></a>В следующем руководстве мы реализуем функции поиска.

> [!div class="step-by-step"]
> [Назад](accessing-your-models-data-from-a-controller.md)
> [Вперед](adding-search.md)
