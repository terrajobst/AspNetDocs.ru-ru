---
uid: web-forms/overview/data-access/working-with-binary-files/displaying-binary-data-in-the-data-web-controls-vb
title: Отображение двоичных данных в веб-элементах управления данными (VB) | Документация Майкрософт
author: rick-anderson
description: В этом учебнике мы рассмотрим параметры для представления двоичных данных на веб-странице, включая отображение файла изображения и предоставление ссылки «download» f...
ms.author: riande
ms.date: 03/27/2007
ms.assetid: 9201656a-e1c2-4020-824b-18fb632d2925
msc.legacyurl: /web-forms/overview/data-access/working-with-binary-files/displaying-binary-data-in-the-data-web-controls-vb
msc.type: authoredcontent
ms.openlocfilehash: 27c901af092aa990f557750dc5d2c42ba2644c02
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78489102"
---
# <a name="displaying-binary-data-in-the-data-web-controls-vb"></a>Отображение двоичных данных в веб-элементах управления данными (VB)

по [Скотт Митчелл](https://twitter.com/ScottOnWriting)

[Скачивание примера приложения](https://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_55_VB.exe) или [Загрузка PDF-файла](displaying-binary-data-in-the-data-web-controls-vb/_static/datatutorial55vb1.pdf)

> В этом учебнике мы рассмотрим параметры для представления двоичных данных на веб-странице, включая отображение файла изображения и предоставление ссылки "Скачать" для PDF-файла.

## <a name="introduction"></a>Введение

В предыдущем учебном курсе мы изучили два метода связывания двоичных данных с базовой моделью данных приложения и использовали элемент управления FileUpload для передачи файлов из браузера в файловую систему веб-сервера. Мы еще не увидим, как связать отправленные двоичные данные с моделью данных. То есть после передачи и сохранения файла в файловой системе путь к файлу должен храниться в соответствующей записи базы данных. Если данные хранятся непосредственно в базе данных, передаваемые двоичные данные не должны сохраняться в файловой системе, но должны быть добавлены в базу данных.

Прежде чем мы рассмотрим связывание данных с моделью данных, давайте сначала посмотрим, как предоставить пользователю двоичные данные. Представление текстовых данных достаточно просто, но как следует представлять двоичные данные? Само собой, это зависит от типа двоичных данных. Для изображений, скорее всего, требуется отобразить изображение. для файлов PDF, документов Microsoft Word, ZIP-файлов и других типов двоичных данных предоставление ссылки для загрузки, скорее всего, является более подходящим.

В этом учебнике мы рассмотрим, как представлять двоичные данные наряду с соответствующими текстовыми данными с помощью веб-элементов управления данными, таких как GridView и DetailsView. В следующем учебном курсе мы соберем, как связать отправленный файл с базой данных.

## <a name="step-1-providingbrochurepathvalues"></a>Шаг 1. предоставление значений`BrochurePath`

Столбец `Picture` в таблице `Categories` уже содержит двоичные данные для различных изображений категорий. В частности, столбец `Picture` для каждой записи содержит двоичное содержимое многоцветного растрового изображения с низким качеством и 16-цветовым изображением. Каждое изображение категории имеет размер 172 пикселей в ширину и 120 пикселей в высоту и потребляет примерно 11 КБ. Что еще больше, двоичное содержимое в столбце `Picture` содержит 78-байтный заголовок [OLE](http://en.wikipedia.org/wiki/Object_Linking_and_Embedding) , который должен быть удален перед отображением изображения. Сведения о заголовке представлены в том случае, если база данных Northwind имеет корни в Microsoft Access. В Access двоичные данные хранятся с использованием типа данных OLE Object, который применяет этот заголовок. Сейчас мы увидим, как убрать заголовки из этих изображений низкого качества для отображения изображения. В следующем учебном курсе мы создадим интерфейс для обновления столбца `Picture` категорий и заменяем растровые изображения, использующие заголовки OLE, с эквивалентными изображениями JPG без лишних заголовков OLE.

В предыдущем учебном курсе мы увидели, как использовать элемент управления FileUpload. Таким образом, можно добавить файлы буклетов в файловую систему веб-сервера. Однако это не приведет к обновлению столбца `BrochurePath` в таблице `Categories`. В следующем учебном курсе мы посмотрим, как это сделать, но теперь нужно вручную указать значения для этого столбца.

В этом руководстве вы найдете семь файлов буклета PDF в папке `~/Brochures`, по одной для каждой категории, кроме Seafood. Я намеренно брошюру Seafood, чтобы продемонстрировать, как работать с сценариями, где не все записи имеют связанные двоичные данные. Чтобы обновить таблицу `Categories` с этими значениями, щелкните правой кнопкой мыши узел `Categories` в обозреватель сервера и выберите команду Отобразить данные таблицы. Затем введите виртуальные пути к файлам буклета для каждой категории, которая содержит буклет, как показано на рис. 1. Так как для категории Seafood нет буклета, оставьте значение столбца `BrochurePath` Columns `NULL`.

[![вручную ввести значения для столбца Categories таблицы Брочурепас](displaying-binary-data-in-the-data-web-controls-vb/_static/image1.gif)](displaying-binary-data-in-the-data-web-controls-vb/_static/image1.png)

**Рис. 1**. Ввод значений для столбца `Categories` `BrochurePath` таблицы вручную ([щелкните, чтобы просмотреть изображение с полным размером](displaying-binary-data-in-the-data-web-controls-vb/_static/image2.png))

## <a name="step-2-providing-a-download-link-for-the-brochures-in-a-gridview"></a>Шаг 2. предоставление ссылки для скачивания буклетов в GridView

Используя значения `BrochurePath`, предоставленные для таблицы `Categories`, мы готовы к созданию элемента управления GridView, содержащего каждую категорию вместе со ссылкой для скачивания буклета Category. На шаге 4 мы добавим этот элемент управления GridView, чтобы также отобразить изображение категории s.

Начните с перетаскивания элемента управления GridView с панели инструментов в конструктор страницы `DisplayOrDownloadData.aspx` в папке `BinaryData`. Задайте для `ID` GridView s `Categories` и через смарт-тег GridView s выберите привязку к новому источнику данных. В частности, привяжите его к элементу управления ObjectDataSource с именем `CategoriesDataSource`, который извлекает данные с помощью метода `CategoriesBLL` Objects `GetCategories()`.

[![создать новый элемент управления ObjectDataSource с именем CategoriesDataSource](displaying-binary-data-in-the-data-web-controls-vb/_static/image2.gif)](displaying-binary-data-in-the-data-web-controls-vb/_static/image3.png)

**Рис. 2**. Создание нового элемента управления ObjectDataSource с именем `CategoriesDataSource` ([щелкните, чтобы просмотреть изображение с полным размером](displaying-binary-data-in-the-data-web-controls-vb/_static/image4.png))

[![настроить ObjectDataSource для использования класса CategoriesBLL](displaying-binary-data-in-the-data-web-controls-vb/_static/image3.gif)](displaying-binary-data-in-the-data-web-controls-vb/_static/image5.png)

**Рис. 3**. Настройка ObjectDataSource для использования класса `CategoriesBLL` ([щелкните, чтобы просмотреть изображение с полным размером](displaying-binary-data-in-the-data-web-controls-vb/_static/image6.png))

[![получить список категорий с помощью метода-Categories ()](displaying-binary-data-in-the-data-web-controls-vb/_static/image4.gif)](displaying-binary-data-in-the-data-web-controls-vb/_static/image7.png)

**Рис. 4**. Получение списка категорий с помощью метода `GetCategories()` ([щелкните, чтобы просмотреть изображение с полным размером](displaying-binary-data-in-the-data-web-controls-vb/_static/image8.png))

После завершения работы мастера настройки источника данных Visual Studio автоматически добавит BoundField в `Categories` GridView для `CategoryID`, `CategoryName`, `Description`, `NumberOfProducts`и `BrochurePath` `DataColumn` s. Удалите `NumberOfProducts` BoundField, так как запрос `GetCategories()` метода s не извлекает эти сведения. Также удалите `CategoryID` BoundField и переименуйте свойства `CategoryName` и `BrochurePath` BoundFields `HeaderText` в категорию и буклет соответственно. После внесения этих изменений декларативная разметка GridView и ObjectDataSource должна выглядеть следующим образом:

[!code-aspx[Main](displaying-binary-data-in-the-data-web-controls-vb/samples/sample1.aspx)]

Просмотр этой страницы в браузере (см. рис. 5). Каждая из восьми категорий отображается в списке. Семь категорий с `BrochurePath`ными значениями имеют `BrochurePath` значение, отображаемое в соответствующем BoundField. Seafood, имеющий `NULL` значение для `BrochurePath`, отображает пустую ячейку.

[![указаны имя, описание и значение Брочурепас каждой категории](displaying-binary-data-in-the-data-web-controls-vb/_static/image5.gif)](displaying-binary-data-in-the-data-web-controls-vb/_static/image9.png)

**Рис. 5**. список имен, описание и `BrochurePath` значений категорий ([щелкните, чтобы просмотреть изображение с полным размером](displaying-binary-data-in-the-data-web-controls-vb/_static/image10.png))

Вместо отображения текста `BrochurePath` столбца необходимо создать ссылку на буклет. Чтобы сделать это, удалите `BrochurePath` BoundField и замените его на HyperLinkField. Задайте для свойства New HyperLinkField `HeaderText` значение буклет, его свойство `Text`, чтобы просмотреть буклет, а свойство `DataNavigateUrlFields` — `BrochurePath`.

![Добавление HyperLinkField для Брочурепас](displaying-binary-data-in-the-data-web-controls-vb/_static/image6.gif)

**Рис. 6**. Добавление HyperLinkField для `BrochurePath`

В результате будет добавлен столбец ссылок на GridView, как показано на рис. 7. При щелчке ссылки Просмотр буклета он либо отображается непосредственно в браузере, либо запрашивает у пользователя загрузку файла в зависимости от того, установлено ли средство чтения PDF и параметры браузера.

[![буклет категории можно просмотреть, щелкнув ссылку Просмотреть буклет.](displaying-binary-data-in-the-data-web-controls-vb/_static/image7.gif)](displaying-binary-data-in-the-data-web-controls-vb/_static/image11.png)

**Рис. 7**. буклет категории можно просмотреть, щелкнув ссылку Просмотреть буклет ([щелкните, чтобы просмотреть изображение с полным размером](displaying-binary-data-in-the-data-web-controls-vb/_static/image12.png)).

[![откроется PDF-файл брошюры Category](displaying-binary-data-in-the-data-web-controls-vb/_static/image8.gif)](displaying-binary-data-in-the-data-web-controls-vb/_static/image13.png)

**Рис. 8**. Отображение брошюры в формате PDF ([щелкните, чтобы просмотреть изображение с полным размером](displaying-binary-data-in-the-data-web-controls-vb/_static/image14.png))

## <a name="hiding-the-view-brochure-text-for-categories-without-a-brochure"></a>Скрытие представления текста буклета для категорий без буклета

Как показано на рис. 7, `BrochurePath` HyperLinkField отображает значение свойства `Text` (буклет для просмотра) для всех записей, независимо от того, есть ли для `BrochurePath`значение, отличное от`NULL`. Конечно, если `BrochurePath` `NULL`, ссылка отображается только как текст, как в случае с категорией Seafood (см. рис. 7). Вместо того, чтобы отображать буклет с представлением текста, может быть неплохо иметь эти категории без значения `BrochurePath` отобразить какой-либо альтернативный текст, например без доступных буклетов.

Чтобы обеспечить такое поведение, необходимо использовать TemplateField, содержимое которого создается посредством вызова метода страницы, который выдает соответствующие выходные данные на основе значения `BrochurePath`. Мы сперва изучили этот метод форматирования в [с помощью полей TemplateField в руководстве по элементу управления GridView](../custom-formatting/using-templatefields-in-the-gridview-control-vb.md) .

Превратите HyperLinkField в TemplateField, выбрав `BrochurePath` HyperLinkField и нажав кнопку преобразовать это поле в ссылку TemplateField в диалоговом окне Изменение столбцов.

![Преобразование HyperLinkField в TemplateField](displaying-binary-data-in-the-data-web-controls-vb/_static/image9.gif)

**Рис. 9**. Преобразование HyperLinkField в TemplateField

Это приведет к созданию TemplateField с `ItemTemplate`, содержащей веб-элемент управления HyperLink, свойство `NavigateUrl` которого привязано к значению `BrochurePath`. Замените эту разметку вызовом метода `GenerateBrochureLink`, передав значение `BrochurePath`:

[!code-aspx[Main](displaying-binary-data-in-the-data-web-controls-vb/samples/sample2.aspx)]

Затем создайте метод `Protected` в классе кода программной части ASP.NET Page s с именем `GenerateBrochureLink`, который возвращает `String` и принимает `Object` в качестве входного параметра.

[!code-vb[Main](displaying-binary-data-in-the-data-web-controls-vb/samples/sample3.vb)]

Этот метод определяет, является ли переданное `Object` значение `NULL` базы данных и, если это так, возвращает сообщение, указывающее, что в категории отсутствует буклет. В противном случае, если имеется `BrochurePath` значение, оно отображается в гиперссылке. Обратите внимание, что если `BrochurePath` значение, оно передается [методу`ResolveUrl(url)`](https://msdn.microsoft.com/library/system.web.ui.control.resolveurl.aspx). Этот метод разрешает переданный *URL-адрес*, заменяя `~`ный символ соответствующим виртуальным путем. Например, если приложение основано на `/Tutorial55`, `ResolveUrl("~/Brochures/Meats.pdf")` вернет `/Tutorial55/Brochures/Meat.pdf`.

На рис. 10 показана страница после применения этих изменений. Обратите внимание, что поле Seafood Category s (категория) `BrochurePath` теперь отображает текст нет буклета.

[![текст нет доступных буклетов отображается для этих категорий без буклета](displaying-binary-data-in-the-data-web-controls-vb/_static/image10.gif)](displaying-binary-data-in-the-data-web-controls-vb/_static/image15.png)

**Рис. 10**. текст без буклета отображается для этих категорий без буклета ([щелкните, чтобы просмотреть изображение с полным размером](displaying-binary-data-in-the-data-web-controls-vb/_static/image16.png))

## <a name="step-3-adding-a-web-page-to-display-a-category-s-picture"></a>Шаг 3. Добавление веб-страницы для просмотра рисунка категории

Когда пользователь посещает страницу ASP.NET, он получает HTML-код ASP.NET Page s. Полученный код HTML является просто текстом и не содержит двоичных данных. Любые дополнительные двоичные данные, такие как изображения, звуковые файлы, приложения Macromedia Flash, внедренные видео проигрывателя Windows Media и т. д., существуют как отдельные ресурсы на веб-сервере. HTML содержит ссылки на эти файлы, но не включает фактическое содержимое файлов.

Например, в HTML элемент `<img>` используется для ссылки на изображение с атрибутом `src`, указывающим на файл изображения следующим образом:

[!code-html[Main](displaying-binary-data-in-the-data-web-controls-vb/samples/sample4.html)]

Когда браузер получает этот код HTML, он выполняет другой запрос к веб-серверу, чтобы получить двоичное содержимое файла изображения, которое затем отображается в браузере. Одна и та же концепция применяется к любым двоичным данным. На шаге 2 Буклет не был отправлен в браузер в составе HTML-разметки страницы. Вместо этого отображаемые HTML-гиперссылки, которые при щелчке приводят к тому, что браузер запрашивает документ в формате PDF напрямую.

Чтобы показать или разрешить пользователям скачивать двоичные данные, размещенные в базе данных, необходимо создать отдельную веб-страницу, которая возвращает данные. Для нашего приложения существует только одно поле с двоичными данными, сохраненное непосредственно в базе данных. рисунок категории. Поэтому нам нужна страница, которая при вызове возвращает данные изображения для определенной категории.

Добавьте новую страницу ASP.NET в папку `BinaryData` с именем `DisplayCategoryPicture.aspx`. При этом не устанавливайте флажок Выбрать главную страницу. Эта страница принимает значение `CategoryID` в строке запроса и возвращает двоичные данные этой категории s `Picture` столбца. Поскольку эта страница возвращает двоичные данные и ничего другого, в разделе HTML не требуется разметки. Поэтому щелкните вкладку Источник в левом нижнем углу и удалите все разметку страницы, Кроме директивы `<%@ Page %>`. Это значит, что декларативная разметка `DisplayCategoryPicture.aspx` s должна состоять из одной строки:

[!code-aspx[Main](displaying-binary-data-in-the-data-web-controls-vb/samples/sample5.aspx)]

Если в директиве `<%@ Page %>` отображается атрибут `MasterPageFile`, удалите его.

В класс кода программной части Pages добавьте следующий код в обработчик событий `Page_Load`:

[!code-vb[Main](displaying-binary-data-in-the-data-web-controls-vb/samples/sample6.vb)]

Этот код начинается с считывания значения `CategoryID` строки запроса в переменную с именем `categoryID`. Затем данные изображения извлекаются с помощью вызова метода `GetCategoryWithBinaryDataByCategoryID(categoryID)` `CategoriesBLL` класса s. Эти данные возвращаются клиенту с помощью метода `Response.BinaryWrite(data)`, но перед этим вызывается заголовок OLE `Picture` значение столбца s. Это достигается путем создания массива `Byte` с именем `strippedImageData`, который будет содержать точно 78 символов, меньших, чем в столбце `Picture`. [Метод`Array.Copy`](https://msdn.microsoft.com/library/z50k9bft.aspx) используется для копирования данных из `category.Picture`, начиная с позиции 78, до `strippedImageData`.

Свойство `Response.ContentType` указывает [тип MIME](http://en.wikipedia.org/wiki/MIME) возвращаемого содержимого, чтобы браузер знал, как его визуализировать. Так как столбец `Categories` таблица s `Picture` является растровым изображением, здесь используется тип MIME Bitmap (Image/BMP). Если опустить тип MIME, большинство браузеров по-прежнему будет правильно отображать изображение, так как они могут вывести тип на основе содержимого двоичных данных файла изображения. Однако разумно по возможности включать тип MIME. Полный список [типов мультимедиа MIME](http://www.iana.org/assignments/media-types/)см. на [веб-сайте центра назначенных номеров Интернета](http://www.iana.org/) .

После создания этой страницы можно просмотреть определенную картинку категорий, посетив `DisplayCategoryPicture.aspx?CategoryID=categoryID`. На рис. 11 показана категория «напитки», которую можно просмотреть в `DisplayCategoryPicture.aspx?CategoryID=1`.

[![отображается изображение категории «напитки»](displaying-binary-data-in-the-data-web-controls-vb/_static/image11.gif)](displaying-binary-data-in-the-data-web-controls-vb/_static/image17.png)

**Рис. 11**. Отображение изображения категории «напитки» ([щелкните, чтобы просмотреть изображение с полным размером](displaying-binary-data-in-the-data-web-controls-vb/_static/image18.png))

Если при посещении `DisplayCategoryPicture.aspx?CategoryID=categoryID`возникает исключение, считывающее невозможность приведения объекта типа "System. DBNull" к типу "System. Byte []", возможны две вещи, которые могут привести к этому. Во первых, `Picture` столбца `Categories` Table s разрешает `NULL` значения. Однако на странице `DisplayCategoryPicture.aspx` предполагается наличие значения, отличного от`NULL`. Невозможно получить прямой доступ к свойству `Picture` `CategoriesDataTable`, если оно имеет значение `NULL`. Если вы хотите разрешить `NULL` значений для столбца `Picture`, d необходимо включить следующее условие:

[!code-vb[Main](displaying-binary-data-in-the-data-web-controls-vb/samples/sample7.vb)]

В приведенном выше коде предполагается, что существует файл изображения с именем `NoPictureAvailable.gif` в папке `Images`, которую нужно отобразить для этих категорий без рисунка.

Это исключение также может быть вызвано возвратом инструкции `CategoriesTableAdapter` s `GetCategoryWithBinaryDataByCategoryID` Method s `SELECT` в список столбцов основного запроса, что может произойти, если используются специальные инструкции SQL и сохранен повторный запуск мастера для основного запроса TableAdapter. Убедитесь, что `GetCategoryWithBinaryDataByCategoryID` Method s `SELECT` Инструкция по-прежнему содержит столбец `Picture`.

> [!NOTE]
> При каждом посещении `DisplayCategoryPicture.aspx` доступ к базе данных осуществляется, и возвращаются указанные данные изображения категории s. Но если изображение категории s не изменилось со времени последнего просмотра пользователем, это не потребует усилий. К счастью, HTTP допускает *условное получение*. С условным ПОЛУЧЕНИЕм клиент, выполняющий запрос HTTP, отправляет по HTTP- [заголовку`If-Modified-Since`](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html) , который предоставляет дату и время последнего получения этим ресурсом из веб-сервера. Если содержимое не изменилось с момента указанной даты, веб-сервер может ответить с [кодом состояния "не изменено" (304)](http://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html) и отказаться от отправить запрошенное содержимое ресурса. Вкратце, этот метод освобождает веб-сервер от необходимости отправки обратного содержимого для ресурса, если он не был изменен с момента последнего доступа к нему с клиента.

Однако для реализации этого поведения необходимо добавить `PictureLastModified` столбец в `Categories`ную таблицу для записи при последнем обновлении столбца `Picture`, а также код для проверки заголовка `If-Modified-Since`. Дополнительные сведения о заголовке `If-Modified-Since` и условном рабочем процессе получения см. в разделе [http Conditional-Get для хакеров RSS](http://fishbowl.pastiche.org/2002/10/21/http_conditional_get_for_rss_hackers) и более [подробный обзор выполнения HTTP-запросов на странице ASP.NET](http://aspnet.4guysfromrolla.com/articles/122204-1.aspx).

## <a name="step-4-displaying-the-category-pictures-in-a-gridview"></a>Шаг 4. отображение рисунков категорий в элементе управления GridView

Теперь, когда у нас есть веб-страница для показа определенной категории категорий, ее можно отобразить с помощью [веб-элемента управления Image](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/ctrlref/standard/image.aspx) или элемента `<img>` HTML, указывающего на `DisplayCategoryPicture.aspx?CategoryID=categoryID`. Изображения, URL-адреса которых определяются данными базы данных, могут отображаться в GridView или DetailsView с помощью Имажефиелд. Имажефиелд содержит свойства `DataImageUrlField` и `DataImageUrlFormatString`, которые работают, как свойства `DataNavigateUrlFields` и `DataNavigateUrlFormatString` HyperLinkField s.

Добавим `Categories` GridView в `DisplayOrDownloadData.aspx`, добавив Имажефиелд, чтобы отобразить изображение каждой категории. Просто добавьте Имажефиелд и задайте для его свойств `DataImageUrlField` и `DataImageUrlFormatString` значение `CategoryID` и `DisplayCategoryPicture.aspx?CategoryID={0}`соответственно. При этом будет создан столбец GridView, который визуализирует элемент `<img>`, к которому `src` ссылается атрибут `DisplayCategoryPicture.aspx?CategoryID={0}`, где {0} заменяется значением `CategoryID` строки GridView.

![Добавление Имажефиелд в GridView](displaying-binary-data-in-the-data-web-controls-vb/_static/image12.gif)

**Рис. 12**. Добавление элемента Имажефиелд в GridView

После добавления Имажефиелд декларативный синтаксис GridView s должен выглядеть так, как в Сусе следующем:

[!code-aspx[Main](displaying-binary-data-in-the-data-web-controls-vb/samples/sample8.aspx)]

Уделите несколько минут для просмотра этой страницы в браузере. Обратите внимание, что каждая запись теперь содержит изображение для категории.

[![изображение категорий отображается для каждой строки](displaying-binary-data-in-the-data-web-controls-vb/_static/image13.gif)](displaying-binary-data-in-the-data-web-controls-vb/_static/image19.png)

**Рис. 13**. изображение категории "Категория" отображается для каждой строки ([щелкните, чтобы просмотреть изображение с полным размером](displaying-binary-data-in-the-data-web-controls-vb/_static/image20.png))

## <a name="summary"></a>Сводка

В этом учебнике мы рассмотрели, как представлять двоичные данные. Способа представления данных зависит от типа данных. Для файлов брошюры PDF мы предложили пользователю ссылку на просмотр буклета, который при щелчке потратил пользователя непосредственно на PDF-файл. Для картинки категорий мы сначала создали страницу для извлечения и возврата двоичных данных из базы данных, а затем используем эту страницу для отображения каждой категории в элементе управления GridView.

Теперь, когда мы рассмотрели способ отображения двоичных данных, мы повторно готовы изучить, как выполнять операции вставки, обновления и удаления базы данных с двоичными данными. В следующем учебном курсе мы рассмотрим, как связать отправленный файл с соответствующей записью базы данных. В этом руководстве мы посмотрим, как обновлять существующие двоичные данные, а также как удалять двоичные данные при удалении связанной с ней записи.

Поздравляем с программированием!

## <a name="about-the-author"></a>Об авторе

[Скотт Митчелл](http://www.4guysfromrolla.com/ScottMitchell.shtml), автор семи книг по ASP/ASP. NET и основатель [4GuysFromRolla.com](http://www.4guysfromrolla.com), работал с веб-технологиями Майкрософт с 1998. Скотт работает как независимый консультант, преподаватель и модуль записи. Его последняя книга — [*Sams обучать себя ASP.NET 2,0 за 24 часа*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco). Он доступен по адресу [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) или через его блог, который можно найти по адресу [http://ScottOnWriting.NET](http://ScottOnWriting.NET).

## <a name="special-thanks-to"></a>Специальная благодарность

Эта серия руководств была рассмотрена многими полезными рецензентами. Потенциальные рецензенты для этого учебника были Терезой Мерфи и Дейв Гарднер. Хотите ознакомиться с моими будущими статьями MSDN? Если это так, расположите строку в [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Назад](uploading-files-vb.md)
> [Вперед](including-a-file-upload-option-when-adding-a-new-record-vb.md)
