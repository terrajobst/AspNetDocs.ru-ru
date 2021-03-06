---
uid: web-pages/overview/getting-started/introducing-aspnet-web-pages-2/form-basics
title: Общие сведения о веб-страницы ASP.NET HTML-форм | Документация Майкрософт
author: Rick-Anderson
description: В этом учебнике показаны основные сведения о создании формы ввода и обработке входных данных пользователя при использовании веб-страницы ASP.NET (Razor). И теперь...
ms.author: riande
ms.date: 05/28/2015
ms.assetid: 81ed82bf-b940-44f1-b94a-555d0cb7cc98
msc.legacyurl: /web-pages/overview/getting-started/introducing-aspnet-web-pages-2/form-basics
msc.type: authoredcontent
ms.openlocfilehash: f57661077ec3bb13f3d4ec41b130bda4d2fb9070
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78463542"
---
# <a name="introducing-aspnet-web-pages---html-form-basics"></a>Общие сведения о веб-страницы ASP.NET HTML-форм

от [Tom фитзмаккен](https://github.com/tfitzmac)

> В этом учебнике показаны основные сведения о создании формы ввода и обработке входных данных пользователя при использовании веб-страницы ASP.NET (Razor). Теперь, когда у вас есть база данных, вы будете использовать навыки работы с формой, чтобы пользователи могли находить определенные фильмы в базе данных. Предполагается, что вы выполнили ряд шагов по [вводу данных с помощью веб-страницы ASP.NET](/aspnet/web-pages/overview/getting-started/introducing-aspnet-web-pages-2/displaying-data).
> 
> Из этого руководства вы узнаете, как выполнять такие задачи:
> 
> - Создание формы с помощью стандартных элементов HTML.
> - Чтение входных данных пользователя в форме.
> - Создание SQL-запроса, который выборочно получает данные с помощью условия поиска, предоставленного пользователем.
> - Как иметь поля на странице «запомнить», что введено пользователем.
>   
> 
> Обсуждаемые функции и технологии:
> 
> - Объект `Request`.
> - Предложение SQL `Where`.

## <a name="what-youll-build"></a>Что вы создадите

В предыдущем руководстве вы создали базу данных, добавили в нее данные, а затем использовали `WebGrid` вспомогательное приложение для вывода данных. В этом учебнике вы добавите поле поиска, которое позволит находить фильмы определенного жанра или название которого содержит любое введенное слово. (Например, вы сможете найти все фильмы, жанр которых — "действие" или заголовок которых содержит "Гарри" или "Adventure.")

По завершении работы с этим руководством у вас будет страница следующего вида:

![Страница фильмов с поиском по жанрам и заголовкам](form-basics/_static/image1.png)

Часть страницы, приведенная в списке, совпадает с частью последнего руководства &mdash; сетке. Разница заключается в том, что в сетке будут показаны только те фильмы, которые вы искали.

## <a name="about-html-forms"></a>О HTML-формах

(Если у вас есть опыт создания HTML-форм и разница между `GET` и `POST`, этот раздел можно пропустить.)

Форма содержит элементы пользовательского ввода &mdash; текстовые поля, кнопки, переключатели, флажки, раскрывающиеся списки и т. д. Пользователи заполняют эти элементы управления или выполнят выбор, а затем отправляют форму, нажав кнопку.

В этом примере показан базовый синтаксис HTML формы:

[!code-html[Main](form-basics/samples/sample1.html)]

Когда эта разметка выполняется на странице, она создает простую форму, которая выглядит следующим образом:

![Базовая HTML-форма, отображаемая в браузере](form-basics/_static/image2.png)

Элемент `<form>` заключает в себя элементы HTML для отправки. (Простая ошибка заключается в добавлении элементов на страницу, но при этом не забудьте поместить их в элемент `<form>`. В этом случае ничего не отправляется.) Атрибут `method` указывает браузеру, как отправить ввод пользователя. Задайте значение `post`, если выполняется обновление на сервере, или `get`, если вы просто извлекаете данные с сервера.

<a id="GET,_POST,_and_HTTP_Verb_Safety"></a>

> [!TIP] 
> 
> **ПОЛУЧЕНИЕ, публикация и безопасность глагола HTTP**
> 
> Протокол HTTP, используемый обозревателями и серверами для обмена данными, в основных операциях является простым и незнакомым. Браузеры используют только несколько команд для выполнения запросов к серверам. При написании кода для Интернета полезно понимать эти глаголы и то, как их используют браузер и сервер. Далеко и нет наиболее часто используемых глаголов:
> 
> - `GET`. Браузер использует эту команду для выборки чего-либо с сервера. Например, при вводе URL-адреса в браузере браузер выполняет `GET` операцию, чтобы запросить нужную страницу. Если страница содержит графики, браузер выполняет дополнительные операции `GET` для получения изображений. Если `GET`ная операция должна передать сведения на сервер, сведения передаются как часть URL-адреса в строке запроса.
> - `POST`. Браузер отправляет запрос `POST` для отправки данных, добавляемых или изменяемых на сервере. Например, команда `POST` используется для создания записей в базе данных или для изменения существующих. В большинстве случаев при заполнении формы и нажатии кнопки "Отправить" браузер выполняет `POST` операцию. В `POST`ной операции данные, передаваемые на сервер, находятся в теле страницы.
> 
> Важное различие между этими глаголами заключается в том, что `GET`ная операция не может изменить что-либо на сервере — или поместив ее немного более абстрактным способом, операция `GET` не приводит к изменению состояния на сервере. Вы можете выполнять `GET`ную операцию с теми же ресурсами столько раз, сколько вы хотите, и эти ресурсы не меняются. (`GET`ная операция часто называется «надежной», или для использования технического термина — *идемпотентными*.) Конечно, в отличие от этого, `POST` запрос изменяет что-то на сервере каждый раз при выполнении операции.
> 
> Два примера помогут продемонстрировать это различие. При выполнении поиска с помощью такого механизма, как Bing или Google, вы заполняете форму, состоящую из одного текстового поля, и затем нажимайте кнопку Поиск. Браузер выполняет `GET` операцию со значением, введенным в поле, передаваемым как часть URL-адреса. Использовать операцию `GET` для этого типа формы неудобно, так как операция поиска не изменяет какие-либо ресурсы на сервере, она просто извлекает информацию.
> 
> Теперь рассмотрим процесс упорядочивания чего-то в сети. Заполните сведения о заказе и нажмите кнопку Submit (отправить). Эта операция будет `POST`ным запросом, так как операция приведет к изменениям на сервере, таким как новая запись заказа, изменение сведений об учетной записи и, возможно, много других изменений. В отличие от операции `GET`, нельзя повторять запрос `POST` — если вы сделали это, каждый раз, когда запрос был отправлен повторно, вы создадите новый порядок на сервере. (В таких случаях веб-сайты часто предупреждают вас от нажатия кнопки «отправить» несколько раз или отключают кнопку «Отправить», чтобы не переслать форму случайно.)
> 
> В рамках этого руководства для работы с HTML-формами используется как операция `GET`, так и `POST`ная операция. В каждом случае будет объяснено, почему используемая вами команда является соответствующей.
> 
> (Дополнительные сведения о HTTP-командах см. в статье [определения методов](http://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html) на сайте W3C.)

Большинство пользовательских элементов ввода являются HTML-элементами `<input>`. Они выглядят как `<input type="type" name="name">,`, где *тип* указывает на необходимый тип элемента управления вводом. Эти элементы являются общими.

- Текстовое поле: `<input type="text">`
- Флажок: `<input type="check">`
- Переключатель: `<input type="radio">`
- Кнопка: `<input type="button">`
- Кнопка "Отправить": `<input type="submit">`

Можно также использовать элемент `<textarea>`, чтобы создать многострочное текстовое поле и элемент `<select>` для создания раскрывающегося списка или прокручиваемого списка. (Дополнительные сведения об элементах HTML-форм см. в разделе [HTML Forms and Input](http://www.w3schools.com/html/html_forms.asp) на сайте W3Schools.)

Атрибут `name` очень важен, так как это значение будет получено позже, как вы увидите вскоре.

Интересной частью является то, что разработчик страницы выполняет с входными данными пользователя. Нет встроенных поведений, связанных с этими элементами. Вместо этого необходимо получить значения, введенные или выбранные пользователем, и выполнять с ними какие-либо действия. Это то, что вы узнаете в этом руководстве.

> [!TIP] 
> 
> **HTML5 и формы ввода**
> 
> Как вы, возможно, знакомы, HTML находится в переходе, а последняя версия (HTML5) включает поддержку более интуитивно понятных способов ввода информации пользователями. Например, в HTML5 вы (разработчик страницы) можете сообщить странице, что пользователь должен ввести дату. После этого браузер может автоматически отображать календарь, не требуя от пользователя вводить дату вручную. Однако HTML5 является новым и не поддерживается во всех браузерах.
> 
> Веб-страницы ASP.NET поддерживает ввод в HTML5 для экстента, который выполняет браузер пользователя. Представление новых атрибутов элемента `<input>` в HTML5 см. в разделе [HTML &lt;input&gt; Type Attribute](http://www.w3schools.com/html/html_form_input_types.asp) на сайте W3Schools.

## <a name="creating-the-form"></a>Создание формы

В WebMatrix в рабочей области **файлы** откройте страницу *movies. cshtml* .

После закрывающего тега `</h1>` и перед открывающим тегом `<div>` в вызове `grid.GetHtml` добавьте следующую разметку:

[!code-html[Main](form-basics/samples/sample2.html)]

Эта разметка создает форму, имеющую текстовое поле с именем `searchGenre` и кнопку Submit (отправить). Текстовое поле и кнопка отправки заключаются в элемент `<form>`, атрибут `method` которого имеет значение `get`. (Помните, что если не вставить текстовое поле и отправить кнопку в элемент `<form>`, то при нажатии кнопки ничего не будет отправлено.) Используйте команду `GET` здесь, так как вы создаете форму, которая не вносит никаких изменений на сервере — это просто приведет к поиску. (В предыдущем руководстве использовался метод `post`, способный отправлять изменения на сервер. Вы увидите, что в следующем руководстве снова.)

Запустите страницу. Хотя поведение для формы не определено, вы можете увидеть, как он выглядит:

![Страница фильмов с полем поиска для жанра](form-basics/_static/image3.png)

Введите значение в текстовое поле, например "комедия". Затем щелкните **Поиск жанра**.

Запишите URL-адрес страницы. Так как для атрибута `method` элемента `<form>` задано `get`, введенное значение теперь является частью строки запроса в URL-адресе следующим образом:

`http://localhost:45661/Movies.cshtml?searchGenre=Comedy`

## <a name="reading-form-values"></a>Считывание значений формы

Страница уже содержит код, который получает данные из базы данных и отображает результаты в сетке. Теперь необходимо добавить код, который считывает значение текстового поля, чтобы можно было выполнить SQL-запрос, включающий условие поиска.

Поскольку для метода формы задано `get`, можно прочитать значение, введенное в текстовое поле, с помощью следующего кода:

`var searchTerm = Request.QueryString["searchGenre"];`

Объект `Request.QueryString` (свойство `QueryString` объекта `Request`) включает значения элементов, которые были отправлены в ходе операции `GET`. Свойство `Request.QueryString` содержит *коллекцию* (список) значений, которые передаются в форме. Чтобы получить любое отдельное значение, необходимо указать имя нужного элемента. Поэтому необходимо иметь атрибут `name` в элементе `<input>` (`searchTerm`), который создает текстовое поле. (Дополнительные сведения об объекте `Request` см. в [боковой панели](#BKMK_TheRequestObject) ниже.)

Достаточно просто прочитать значение текстового поля. Но если пользователь ничего не введет в текстовое поле, но щелкнули **Поиск** , можно пропустить этот щелчок, так как поиск не выполняется.

В следующем примере кода показано, как реализовать эти условия. (Пока не нужно добавлять этот код. это можно сделать чуть позже.)

[!code-csharp[Main](form-basics/samples/sample3.cs)]

Тест разбивается таким образом:

- Получите значение `Request.QueryString["searchGenre"]`, а именно значение, которое было указано в элементе `<input>` с именем `searchGenre`.
- Выясните, не пуст ли он, с помощью метода `IsEmpty`. Этот метод является стандартным способом определения того, содержит ли какое-либо значение (например, элемент формы). Но на самом деле, вам нужно только, если он *не* пуст, поэтому...
- Добавьте оператор `!` перед тестом `IsEmpty`. (Оператор `!` означает логическое значение NOT).

В простом английском языке все `if` условие преобразуется в следующее: *Если элемент сеарчженре формы не пуст, то.* ..

Этот блок задает этап для создания запроса, использующего условие поиска. Это будет сделано в следующем разделе.

<a id="BKMK_TheRequestObject"></a>

> [!TIP] 
> 
> **Объект запроса**
> 
> Объект `Request` содержит все сведения, которые браузер отправляет в приложение при запросе или отправке страницы. Этот объект включает любые сведения, предоставляемые пользователем, например значения текстовых полей или файлы для отправки. Он также включает в себя все виды дополнительных сведений, таких как файлы cookie, значения в строке запроса URL-адреса (если они есть), путь к файлу на странице, тип браузера, который используется пользователем, список языков, заданных в браузере. и многое другое.
> 
> Объект `Request` — это *коллекция* (список) значений. Вы получаете отдельное значение из коллекции, указывая его имя:
> 
> `var someValue = Request["name"];`
> 
> Объект `Request` фактически предоставляет несколько подмножеств. Пример:
> 
> - `Request.Form` предоставляет значения из элементов в отправленном `<form>`ном элементе, если запрос является `POST` запросом.
> - `Request.QueryString` предоставляет только значения в строке запроса URL-адреса. (В URL-адресе, например `http://mysite/myapp/page?searchGenre=action&page=2`, раздел `?searchGenre=action&page=2` URL-адреса является строкой запроса.)
> - `Request.Cookies` коллекция предоставляет доступ к файлам cookie, отправленным браузером.
> 
> Чтобы получить значение, которое известно в отправленной форме, можно использовать `Request["name"]`. Кроме того, можно использовать более конкретные версии `Request.Form["name"]` (для запросов `POST`) или `Request.QueryString["name"]` (для запросов `GET`). Конечно, *Name* — это имя получаемого элемента.
> 
> Имя элемента, которое требуется получить, должно быть уникальным в используемой коллекции. Именно поэтому объект `Request` предоставляет подмножества, такие как `Request.Form` и `Request.QueryString`. Предположим, страница содержит элемент Form с именем `userName`, а *также* файл cookie с именем `userName`. Если вы получаете `Request["userName"]`, это неоднозначно, нужно ли использовать значение формы или файл cookie. Однако, если вы получаете `Request.Form["userName"]` или `Request.Cookie["userName"]`, вы явно отдаете значение, которое нужно получить.
> 
> Рекомендуется использовать конкретное подмножество `Request`, которое вам интересно, например `Request.Form` или `Request.QueryString`. Для простых страниц, создаваемых в этом учебнике, это, скорее всего, не имеет никакой разницы. Однако при создании более сложных страниц использование явной версии `Request.Form` или `Request.QueryString` может помочь избежать проблем, которые могут возникать, если страница содержит форму (или несколько форм), файлы cookie, значения строк запросов и т. д.

## <a name="creating-a-query-by-using-a-search-term"></a>Создание запроса с помощью условия поиска

Теперь, когда вы узнали, как получить введенное пользователем условие поиска, можно создать запрос, который его использует. Помните, что для получения всех элементов фильмов из базы данных вы используете SQL-запрос, который выглядит следующим образом:

`SELECT * FROM Movies`

Чтобы получить только определенные фильмы, необходимо использовать запрос, содержащий предложение `Where`. Это предложение позволяет задать условие, в котором строки возвращаются запросом. Ниже приведен пример:

`SELECT * FROM Movies WHERE Genre = 'Action'`

Базовый формат — `WHERE column = value`. Можно использовать разные операторы помимо `=`, например `>` (больше), `<` (меньше), `<>` (не равно), `<=` (меньше или равно) и т. д., в зависимости от того, что вы ищете.

Если вас интересует, инструкции SQL не учитывают регистр &mdash; `SELECT` совпадает с `Select` (или даже `select`). Тем не менее люди часто заменяют ключевые слова в инструкции SQL, например `SELECT` и `WHERE`, чтобы облегчить чтение.

### <a name="passing-the-search-term-as-a-parameter"></a>Передача условия поиска в качестве параметра

Поиск определенного жанра достаточно прост (`WHERE Genre = 'Action'`), но вы хотите иметь возможность искать любой жанр, вводимый пользователем. Для этого создайте запрос SQL, содержащий заполнитель для искомого значения. Эта команда будет выглядеть следующим образом:

`SELECT * FROM Movies WHERE Genre = @0`

Заполнитель — это `@`ный символ, за которым следует ноль. Как вы можете догадаться, запрос может содержать несколько заполнителей, и им будут присвоены имена `@0`, `@1`, `@2`и т. д.

Чтобы настроить запрос и фактически передать ему значение, используйте код, подобный приведенному ниже.

[!code-sql[Main](form-basics/samples/sample4.sql)]

Этот код аналогичен тому, что уже было сделано для вывода данных в сетке. Единственное отличие:

- Запрос содержит заполнитель (`WHERE Genre = @0"`).
- Запрос помещается в переменную (`selectCommand`); ранее запрос был передан непосредственно методу `db.Query`.
- При вызове метода `db.Query` вы передаете как запрос, так и значение, используемые для заполнителя. (Если запрос содержал несколько заполнителей, все они передаются в метод как отдельные значения.)

Если поместить все эти элементы вместе, вы получите следующий код:

[!code-csharp[Main](form-basics/samples/sample5.cs)]

> [!NOTE] 
> 
> **Важно!** Использование заполнителей (таких как `@0`) для передачи значений команде SQL *чрезвычайно важно* для обеспечения безопасности. Способ, который вы видите здесь с заполнителями для данных переменных, является единственным способом создания команд SQL.
> 
> Никогда не создавайте инструкцию SQL, объединяя (объединяя) литеральный текст и значения, получаемые от пользователя. Объединение вводимых пользователем данных в инструкцию SQL открывает сайт для *атаки путем внедрения кода SQL* , когда злоумышленник отправляет на страницу значения, которые применяют базу данных. (Дополнительные сведения см. в статье [внедрение кода SQL](https://msdn.microsoft.com/library/ms161953.aspx) на веб-сайт MSDN.)

## <a name="updating-the-movies-page-with-search-code"></a>Обновление страницы фильмов с помощью кода поиска

Теперь можно обновить код в файле *movies. cshtml* . Чтобы начать, замените код в блоке кода в верхней части страницы следующим кодом:

[!code-csharp[Main](form-basics/samples/sample6.cs)]

Разница заключается в том, что вы поместили запрос в переменную `selectCommand`, которую вы передадите в `db.Query` позже. Помещение инструкции SQL в переменную позволяет изменить инструкцию, которая будет выполнять поиск.

Вы также удалили эти две строки, которые появятся позже:

[!code-csharp[Main](form-basics/samples/sample7.cs)]

Еще не нужно выполнять запрос (то есть вызовите `db.Query`), и вы не хотите инициализировать вспомогательный модуль `WebGrid`. После выяснения того, какую инструкцию SQL необходимо выполнить, вы сможете выполнить эти действия.

После этого перезаписанного блока можно добавить новую логику для обработки поиска. Завершенный код будет выглядеть следующим образом. Обновите код на странице, чтобы он соответствовал этому примеру:

[!code-cshtml[Main](form-basics/samples/sample8.cshtml)]

Теперь страница работает следующим образом. При каждом запуске страницы код открывает базу данных, а `selectCommand` переменной присваивается инструкция SQL, которая получает все записи из таблицы `Movies`. Код также инициализирует переменную `searchTerm`.

Однако если текущий запрос содержит значение элемента `searchGenre`, то код задает `selectCommand` для другого запроса — а именно — `Where` для поиска жанра. Он также устанавливает `searchTerm` в любое значение, переданное в поле поиска (это может быть Nothing).

Независимо от того, какая инструкция SQL находится в `selectCommand`, код затем вызывает `db.Query`, чтобы выполнить запрос, передав его все, что находится в `searchTerm`. Если в `searchTerm`нет ничего, это не имеет значения, так как в этом случае нет параметра для передачи значения `selectCommand` в любом случае.

Наконец, код инициализирует вспомогательный объект `WebGrid`, используя результаты запроса, как и раньше.

Это можно увидеть, поместив инструкцию SQL и условие поиска в переменные, вы добавили гибкость в код. Как вы увидите далее в этом учебнике, вы можете использовать эту базовую платформу и добавлять логику для различных типов поиска.

## <a name="testing-the-search-by-genre-feature"></a>Тестирование функции поиска по жанру

В WebMatrix запустите страницу *movies. cshtml* . Отобразится страница с текстовым полем для жанра.

Введите жанр, введенный для одной из записей теста, а затем нажмите кнопку **Поиск**. На этот раз вы увидите только те фильмы, которые соответствуют этому жанру:

![Фильмы со списком страниц после поиска жанра "Комедиес"](form-basics/_static/image4.png)

Введите другой жанр и повторите поиск. Попробуйте ввести жанр, используя все строчные или прописные буквы, чтобы можно было увидеть, что при поиске не учитывается регистр.

## <a name="remembering-what-the-user-entered"></a>«Запоминание», что введено пользователем

Вы могли заметить, что после того, как вы указали жанр и щелкнули **Жанр для поиска**, вы видели список для этого жанра. Однако текстовое поле поиска было пустым &mdash; другими словами, оно не запомнило, что вы ввели.

Важно понимать, почему происходит это поведение. При отправке страницы браузер отправляет запрос на веб-сервер. Когда ASP.NET получает запрос, он создает новый экземпляр страницы, выполняет в нем код, а затем снова отображает страницу в браузере. На самом деле, страница не знает, что вы только что работали с предыдущей версией самой себя. Все знает, что он получил запрос, в котором есть данные формы.

Каждый раз, когда вы запрашиваете страницу &mdash; в первый раз или отправляя ее &mdash; вы получаете новую страницу. На веб-сервере отсутствует память вашего последнего запроса. Ни ASP.NET, ни не использует браузер. Единственное соединение между этими отдельными экземплярами страницы — это любые данные, передаваемые между ними. Например, при отправке страницы новый экземпляр страницы может получить данные формы, отправленные предыдущим экземпляром. (Другой способ передачи данных между страницами — использование файлов cookie.)

Формальный способ описать эту ситуацию — сказать, что веб-страницы не имеют *состояния*. Веб-серверы, сами страницы и элементы на странице не сохраняют никаких сведений о предыдущем состоянии страницы. Веб-узел был разработан таким образом, так как поддержание состояния отдельных запросов позволит быстро выгрузить ресурсы веб-серверов, которые часто обрабатывают тысячи, возможно, даже сотни тысяч запросов в секунду.

Поэтому текстовое поле было пустым. После отправки страницы ASP.NET создал новый экземпляр страницы и пропустил код и разметку. В этом коде нет ничего, что поASP.NET к постановке значения в текстовое поле. Итак, ASP.NET ничего не делало, и текстовое поле было подготовлено без значения.

Существует простой способ решения этой проблемы. Жанр, введенный в текстовое поле, доступен в коде &mdash; *он находится в* `Request.QueryString["searchGenre"]`.

Обновите разметку для текстового поля таким образом, чтобы атрибут `value` получит его значение из `searchTerm`, как показано в следующем примере:

[!code-html[Main](form-basics/samples/sample9.html?highlight=1)]

На этой странице можно также присвоить атрибуту `value` значение переменной `searchTerm`, так как эта переменная также содержит введенный жанр. Но использование объекта `Request` для установки атрибута `value`, как показано ниже, является стандартным способом выполнения этой задачи. (Если вы даже захотите это &mdash; в некоторых ситуациях, может потребоваться отобразить страницу *без* значений в полях. Все зависит от того, что происходит с вашим приложением.)

> [!NOTE]
> Вы не можете «запомнить» значение текстового поля, используемого для паролей. Это было бы нарушение безопасности, позволяющее пользователям заполнять поле пароля с помощью кода.

Снова запустите страницу, введите Жанр и щелкните **Поиск жанр**. На этот раз вы не увидите результаты поиска, но текстовое поле запоминает введенное в последний раз время:

![Страница, на которой показано, что в текстовом поле сохранена Предыдущая запись](form-basics/_static/image5.png)

## <a name="searching-for-any-word-in-the-title"></a>Поиск любого слова в заголовке

Теперь можно искать любой жанр, но может также потребоваться найти заголовок. Очень трудно получить заголовок в точном соответствии с поиском, поэтому вместо этого можно искать слово, которое появляется в любом месте заголовка. Для этого в SQL используйте оператор `LIKE` и синтаксис, как в следующем примере:

`SELECT * FROM Movies WHERE Title LIKE '%adventure%'`

Эта команда получает все фильмы, названия которых содержат "Adventure". При использовании оператора `LIKE` вы включаете символ-шаблон `%` как часть условия поиска. `LIKE 'adventure%'` поиска означает "начинается с" Adventure ". (Технически, это означает "строка" Adventure ", за которой следует что-нибудь.") Аналогичным образом условие поиска `LIKE '%adventure'` означает «все, за которым следует строка «Adventure», которая является еще одним способом: «заканчивается на «Adventure»».

Таким образом, условие поиска `LIKE '%adventure%'` означает «с помощью Adventure в любом месте в заголовке». (Технически, «все в названии, за которыми следует «Adventure», за которой следуют все»).

Внутри элемента `<form>` добавьте следующую разметку непосредственно под закрывающим тегом `</div>` для поиска жанра (непосредственно перед закрывающим элементом `</form>`):

[!code-html[Main](form-basics/samples/sample10.html)]

Код, обрабатывающий этот поиск, похож на код для поиска по жанру, за исключением того, что необходимо собрать `LIKE` Поиск. В блоке кода в верхней части страницы добавьте этот блок `if` сразу после блока `if` для поиска жанра:

[!code-csharp[Main](form-basics/samples/sample11.cs)]

Этот код использует ту же логику, которую вы видели ранее, за исключением того, что поиск использует оператор `LIKE` и код помещает "`%`" до и после условия поиска.

Обратите внимание на то, как было легко добавить еще один поиск на страницу. Все, что вам пришлось сделать:

- Создайте блок `if`, проверенный на предмет наличия значения в соответствующем поле поиска.
- Задайте для переменной `selectCommand` новую инструкцию SQL.
- Присвойте переменной `searchTerm` значение, которое будет передаваться в запрос.

Вот полный блок кода, который содержит новую логику поиска по названиям:

[!code-cshtml[Main](form-basics/samples/sample12.cshtml)]

Ниже приведено краткое описание того, что делает этот код.

- Переменные `searchTerm` и `selectCommand` инициализируются в верхней части. Вы собираетесь присвоить этим переменным соответствующее условие поиска (если таковое имеется) и соответствующую команду SQL в зависимости от того, что пользователь делает на странице. Поиск по умолчанию — это простой случай получения всех фильмов из базы данных.
- В тестах для `searchGenre` и `searchTitle`в коде задается `searchTerm` значение, которое необходимо найти. Эти блоки кода также устанавливают в `selectCommand` соответствующую команду SQL для этого поиска.
- Метод `db.Query` вызывается только один раз, используя любую команду SQL в `selectedCommand` и любое значение в `searchTerm`. Если условия поиска отсутствуют (без жанра и слова Title), значение `searchTerm` является пустой строкой. Однако это не имеет значения, поскольку в этом случае запрос не требует параметра.

## <a name="testing-the-title-search-feature"></a>Тестирование функции поиска по названию

Теперь можно протестировать завершенную страницу поиска. Запустите *movies. cshtml*.

Введите Жанр и щелкните **Поиск жанр**. В сетке отображаются фильмы этого жанра, например ранее.

Введите слово заголовка и щелкните **Поиск заголовок**. В сетке отображаются фильмы с таким словом в заголовке.

![Список фильмов, перечислений после поиска "The" в заголовке](form-basics/_static/image6.png)

Оставьте оба текстовых поля пустыми и нажмите любую кнопку. В сетке отображаются все фильмы.

## <a name="combining-the-queries"></a>Объединение запросов

Вы можете заметить, что доступные для выполнения операции поиска являются эксклюзивными. Нельзя одновременно выполнять поиск в заголовке и жанре, даже если в обоих полях поиска есть значения. Например, невозможно выполнить поиск всех фильмов действий, заголовок которых содержит "Adventure". (Как только страница будет помечена, если ввести значения как для жанра, так и для названия, поиск по названию получает приоритет.) Чтобы создать поиск, объединяющий условия, необходимо создать SQL-запрос со следующим синтаксисом:

`SELECT * FROM Movies WHERE Genre = @0 AND Title LIKE @1`

И вам нужно будет выполнить запрос, используя следующую инструкцию (примерно говоря):

`var selectedData = db.Query(selectCommand, searchGenre, searchTitle);`

Создание логики, позволяющей нескольким перестановкам критериев поиска, может попытаться подать немного усилий, как можно видеть. Поэтому мы будем останавливаться здесь.

## <a name="coming-up-next"></a>Далее

В следующем руководстве вы создадите страницу, которая использует форму, чтобы позволить пользователям добавлять в базу данных фильмы.

## <a name="complete-listing-for-movie-page-updated-with-search"></a>Полный список для страницы фильмов (обновлен с помощью поиска)

[!code-cshtml[Main](form-basics/samples/sample13.cshtml)]

## <a name="additional-resources"></a>Дополнительные ресурсы

- [Введение в веб-программирование ASP.NET с использованием синтаксиса Razor](https://go.microsoft.com/fwlink/?LinkID=202890)
- [Предложение SQL WHERE](http://www.w3schools.com/sql/sql_where.asp) на сайте W3Schools
- Статья об [определениях методов](http://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html) на сайте W3C

> [!div class="step-by-step"]
> [Назад](displaying-data.md)
> [Вперед](entering-data.md)
