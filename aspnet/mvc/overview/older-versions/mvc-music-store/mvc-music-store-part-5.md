---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-5
title: Часть 5. Редактирование форм и шаблонов | Документация Майкрософт
author: jongalloway
description: В этой серии руководств подробно описаны все шаги, предпринятые для создания примера приложения музыкального хранилища ASP.NET MVC. В части 5 описывается редактирование форм и шаблонов.
ms.author: riande
ms.date: 04/21/2011
ms.assetid: 6b09413a-6d6a-425a-87c9-629f91b91b28
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-5
msc.type: authoredcontent
ms.openlocfilehash: 20b99cbe57b5dfa623205838a5929733a6c2d70d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78450912"
---
# <a name="part-5-edit-forms-and-templating"></a>Часть 5. изменение форм и шаблонов

[Джон Гэллоуэй](https://github.com/jongalloway)

> Музыкальное хранилище MVC — это учебное приложение, в котором представлены и объясняются пошаговые инструкции по использованию ASP.NET MVC и Visual Studio для разработки веб-приложений.  
>   
> Музыкальное хранилище MVC — это упрощенная реализация в магазине, которая продает музыкальные альбомы в сети и реализует базовое администрирование сайта, вход пользователя в систему и функции корзины покупок.
> 
> В этой серии руководств подробно описаны все шаги, предпринятые для создания примера приложения музыкального хранилища ASP.NET MVC. В части 5 описывается редактирование форм и шаблонов.

В прошлом разделе мы загрузили данные из нашей базы данных и выводили их на экран. В этой главе мы также разберем возможность редактирования данных.

## <a name="creating-the-storemanagercontroller"></a>Создание Стореманажерконтроллер

Начнем с создания нового контроллера с именем **стореманажерконтроллер**. Для этого контроллера мы будем использовать преимущества функций формирования шаблонов, доступных в обновлении инструментов ASP.NET MVC 3. Задайте параметры для диалогового окна Добавление контроллера, как показано ниже.

![](mvc-music-store-part-5/_static/image1.png)

При нажатии кнопки Добавить вы увидите, что механизм формирования шаблонов ASP.NET MVC 3 выполняет хороший объем работы за вас:

- Он создает новый Стореманажерконтроллер с локальной переменной Entity Framework
- Она добавляет папку Стореманажер в папку Views проекта.
- Он добавляет представление Create. cshtml, DELETE. cshtml, Details. cshtml, Edit. cshtml и index. cshtml, строго типизированное в класс альбома.

![](mvc-music-store-part-5/_static/image2.png)

Новый класс контроллера Стореманажер включает действия CRUD (создание, чтение, обновление, удаление), которые узнают, как работать с классом модели альбома и использовать наш контекст Entity Framework для доступа к базе данных.

## <a name="modifying-a-scaffolded-view"></a>Изменение шаблона представления

Важно помнить, что хотя этот код был создан для нас, он является стандартным кодом MVC ASP.NET, как мы написали в рамках этого руководства. Она призвана сэкономить время, затрачиваемое на написание стандартного кода контроллера и создание строго типизированных представлений вручную, но это не тот тип создаваемого кода, с которым вы могли бы ознакомиться с ужасные предупреждениями о том, как не должны изменить приведен. Это ваш код, и вы должны изменить его.

Итак, давайте начнем с быстрого редактирования в представление индекса Стореманажер (/Виевс/стореманажер/индекс.кштмл). В этом представлении отображается таблица со списком альбомов в магазине с ссылками Edit/Details/DELETE и включает общие свойства альбома. Мы удалим поле Албумартурл, так как оно не очень полезно в этом дисплее. В &lt;таблице&gt; в разделе кода представления удалите элементы &lt;TH&gt; и &lt;TD&gt;, окружающие ссылки на Албумартурл, как показано в выделенных ниже строках:

[!code-cshtml[Main](mvc-music-store-part-5/samples/sample1.cshtml)]

Измененный код представления будет выглядеть следующим образом:

[!code-cshtml[Main](mvc-music-store-part-5/samples/sample2.cshtml)]

## <a name="a-first-look-at-the-store-manager"></a>Первый взгляд на Store Manager

Теперь запустите приложение и перейдите к/Стореманажер/.. Отобразится только что измененный индекс Store Manager, в котором отображается список альбомов в магазине со ссылками на изменения, сведения и удаление.

![](mvc-music-store-part-5/_static/image3.png)

Если щелкнуть ссылку "Изменить", откроется форма редактирования с полями для альбома, включая раскрывающиеся списки для жанра и исполнителя.

![](mvc-music-store-part-5/_static/image4.png)

В нижней части щелкните ссылку "назад на список", а затем щелкните ссылку сведения для альбома. Отображаются подробные сведения об отдельном альбоме.

![](mvc-music-store-part-5/_static/image5.png)

Опять же, щелкните ссылку вернуться к списку, а затем щелкните ссылку удалить. Откроется диалоговое окно подтверждения, в котором отобразятся сведения об альбоме и будет предложено подтвердить удаление.

![](mvc-music-store-part-5/_static/image6.png)

Нажав кнопку Удалить внизу, вы удалите альбом и вернетесь на страницу индекса, на которой будет показан удаленный альбом.

Мы не работаем с менеджером магазина, но у нас есть рабочий контроллер и код представления для начала операций CRUD.

## <a name="looking-at-the-store-manager-controller-code"></a>Просмотр кода контроллера Store Manager

Контроллер Store Manager содержит хороший объем кода. Давайте вернемся сверху вниз. Контроллер включает в себя некоторые стандартные пространства имен для контроллера MVC, а также ссылку на пространство имен Models. Контроллер имеет частный экземпляр Мусиксторинтитиес, используемый каждым из действий контроллера для доступа к данным.

[!code-csharp[Main](mvc-music-store-part-5/samples/sample3.cs)]

### <a name="store-manager-index-and-details-actions"></a>Действия индекса и сведений диспетчера магазина

Представление индекса получает список альбомов, включая сведения о жанрах и исполнителях каждого альбома, как было показано ранее при работе с методом обзора магазина. Представление индекса следует за ссылками на связанные объекты, чтобы они могли отображать название жанра каждого альбома и имя исполнителя, поэтому контроллер является эффективным и запрашивает эти сведения в исходном запросе.

[!code-csharp[Main](mvc-music-store-part-5/samples/sample4.cs)]

Действие контроллера сведений контроллера Стореманажер работает точно так же, как и действие "сведения о контроллере хранилища", которое мы написали ранее — запрос для альбома по ИДЕНТИФИКАТОРу с помощью метода Find (), а затем возвращает его в представление.

[!code-csharp[Main](mvc-music-store-part-5/samples/sample5.cs)]

### <a name="the-create-action-methods"></a>Методы действия Create

Методы действия Create немного отличаются от тех, которые мы видели до сих пор, так как они обрабатывают входные данные формы. Когда пользователь впервые посещает/Стореманажер/креате/, отображается пустая форма. На этой HTML-странице будет содержаться &lt;форма&gt; элемент, содержащий элементы ввода раскрывающегося списка и текстового поля, где можно ввести сведения о альбоме.

После того как пользователь заполнит значения формы альбома, они смогут нажать кнопку "Сохранить", чтобы отправить эти изменения обратно в приложение, чтобы сохранить его в базе данных. Когда пользователь нажимает кнопку "Save" (сохранить), &lt;форма,&gt; выполняет HTTP-POST по адресу URL/Стореманажер/креате/и отправляет &lt;форму&gt; значений в составе HTTP-POST.

ASP.NET MVC позволяет легко разбивать логику этих двух сценариев вызова URL-адресов, позволяя реализовать два отдельных метода действия "создать" в нашем классе Стореманажерконтроллер — один для обработки начального HTTP-GET — для обзора URL-адреса/Стореманажер/креате/, а другой — для обработки HTTP-POST отправленных изменений.

### <a name="passing-information-to-a-view-using-viewbag"></a>Передача данных в представление с помощью ViewBag

Мы использовали ViewBag ранее в этом руководстве, но не говорили о нем. ViewBag позволяет передавать данные в представление без использования строго типизированного объекта модели. В этом случае наше действие изменить HTTP-GET Controller должно передать в форму список жанров и исполнителей, чтобы заполнить раскрывающиеся списки, а самый простой способ — вернуть их в виде ViewBag элементов.

ViewBag — это динамический объект, то есть вы можете ввести ViewBag. foo или ViewBag. Йоурнамехере без написания кода для определения этих свойств. В этом случае код контроллера использует ViewBag. GenreId и ViewBag. Артистид, чтобы значения раскрывающегося списка, переданные в форму, были GenreId и Артистид, которые являются свойствами альбома, которые будут заданы.

Эти раскрывающиеся значения возвращаются в форму с помощью объекта SelectList, который создается исключительно для этой цели. Это делается с помощью следующего кода:

[!code-csharp[Main](mvc-music-store-part-5/samples/sample6.cs)]

Как видно из кода метода действия, для создания этого объекта используются три параметра:

- Список элементов, которые будут отображены в раскрывающемся списке. Обратите внимание, что это не просто строка — мы передаем список жанров.
- Следующим параметром, передаваемым в SelectList, является выбранное значение. Таким способом SelectList знает, как предварительно выбрать элемент в списке. Это будет проще понять при рассмотрении формы редактирования, которая очень похожа на.
- Последний параметр — это отображаемое свойство. В этом случае это означает, что свойство Genre.Name будет отображаться для пользователя.

С учетом этого, действие HTTP-GET Create довольно простое — два Селектлистс добавляются в ViewBag, и объект модели не передается в форму (поскольку он еще не создан).

[!code-csharp[Main](mvc-music-store-part-5/samples/sample7.cs)]

### <a name="html-helpers-to-display-the-drop-downs-in-the-create-view"></a>Вспомогательные методы HTML для отображения раскрывающихся элементов в представлении создания

Поскольку мы говорили о том, как раскрывающиеся значения передаются в представление, давайте кратко рассмотрим представление, чтобы увидеть, как эти значения отображаются. В коде представления (/Виевс/стореманажер/креате.кштмл) вы увидите следующий вызов для отображения раскрывающегося списка жанра.

[!code-cshtml[Main](mvc-music-store-part-5/samples/sample8.cshtml)]

Это называется вспомогательным модулем HTML — служебным методом, который выполняет общую задачу представления. Вспомогательные методы HTML очень полезны для обеспечения краткости и удобочитаемости нашего кода представления. Вспомогательный элемент HTML. DropDownList предоставляется ASP.NET MVC, но, как мы увидим, можно создать собственные вспомогательные методы для просмотра кода, который мы будем использовать в нашем приложении.

Вызов HTML. DropDownList должен задаваться двумя объектами — где можно получить список и какое значение (если оно есть) должно быть заранее выбрано. Первый параметр, GenreId, указывает DropDownList найти значение с именем GenreId либо в модели, либо в ViewBag. Второй параметр используется для указания значения, которое будет отображаться как изначально выбранное в раскрывающемся списке. Так как эта форма является формой создания, нет значения для предвыбора и передается String. Empty.

### <a name="handling-the-posted-form-values"></a>Обработка отправленных значений формы

Как обсуждалось ранее, существует два метода действий, связанных с каждой формой. Первый обрабатывает запрос HTTP-GET и отображает форму. Второй обрабатывает запрос HTTP-POST, который содержит отправленные значения формы. Обратите внимание, что действие контроллера имеет атрибут [HttpPost], который сообщает ASP.NET MVC о том, что он должен отвечать только на запросы HTTP-POST.

[!code-csharp[Main](mvc-music-store-part-5/samples/sample9.cs)]

Это действие имеет четыре обязанности:

- 1. Чтение значений формы
- 2. Проверить, прошли ли значения формы правила проверки
- 3. Если отправка формы допустима, сохраните данные и отобразите обновленный список.
- 4. Если отправка формы является недопустимой, повторно отобразите форму с ошибками проверки.

#### <a name="reading-form-values-with-model-binding"></a>Считывание значений формы с помощью привязки модели

Действие контроллера обрабатывает отправку формы, которая включает значения для GenreId и Артистид (из раскрывающегося списка) и значения текстового поля для Title, Price и Албумартурл. Хотя доступ к значениям формы Возможен напрямую, лучшим подходом является использование возможностей привязки модели, встроенных в ASP.NET MVC. Когда действие контроллера принимает тип модели в качестве параметра, ASP.NET MVC попытается заполнить объект этого типа, используя входные данные формы (а также значения маршрута и строки запроса). Это достигается путем поиска значений, имена которых соответствуют свойствам объекта Model, например при задании значения GenreId нового объекта альбома выполняется поиск входных данных с именем GenreId. При создании представлений с помощью стандартных методов в ASP.NET MVC формы всегда отображаются с использованием имен свойств в качестве имен входных полей, поэтому имена полей будут просто соответствовать.

#### <a name="validating-the-model"></a>Проверка модели

Модель проверяется с помощью простого вызова ModelState. IsValid. Мы еще не добавили правила проверки в наш класс «альбом». это будет сделано немного, так что сейчас эта проверка не требует много усилий. Важно то, что эта проверка Моделстат. IsValid будет адаптирована к правилам проверки, которые мы поместили в нашей модели, поэтому будущие изменения правил проверки не потребует обновления кода действия контроллера.

#### <a name="saving-the-submitted-values"></a>Сохранение отправленных значений

Если отправка формы проходит проверку, пора сохранить значения в базе данных. При использовании Entity Framework необходимо только добавить модель в коллекцию альбомов и вызвать метод SaveChanges.

[!code-csharp[Main](mvc-music-store-part-5/samples/sample10.cs)]

Entity Framework создает соответствующие команды SQL для сохранения значения. После сохранения данных мы перенаправляем обратно в список альбомов, чтобы мы могли увидеть наше обновление. Это делается путем возвращения Редиректтоактион с именем действия контроллера, которое требуется отобразить. В данном случае это метод index.

#### <a name="displaying-invalid-form-submissions-with-validation-errors"></a>Отображение недопустимых отправок формы с ошибками проверки

В случае недопустимого ввода в форму раскрывающиеся значения добавляются в ViewBag (как в случае HTTP-GET), а привязанные значения модели передаются обратно в представление для отображения. Ошибки проверки автоматически отображаются с помощью вспомогательного метода HTML @Html.ValidationMessageFor.

#### <a name="testing-the-create-form"></a>Тестирование формы создания

Чтобы протестировать это, запустите приложение и перейдите к/Стореманажер/креате/. в нем отобразится пустая форма, возвращенная методом Стореконтроллер Create HTTP-GET.

Заполните некоторые значения и нажмите кнопку Создать, чтобы отправить форму.

![](mvc-music-store-part-5/_static/image7.png)

![](mvc-music-store-part-5/_static/image8.png)

### <a name="handling-edits"></a>Обработка изменений

Пара действий редактирования (HTTP-GET и HTTP-POST) очень похожа на методы действий создания, которые мы только что рассматривали. Так как сценарий редактирования предполагает работу с существующим альбомом, метод Edit HTTP-GET загружает альбом на основе параметра ID, переданного через маршрут. Этот код для получения альбома с помощью Албумид аналогичен тому, который ранее рассматривался в действии контроллера подробностей. Как и в случае с методом Create/HTTP-GET, раскрывающиеся значения возвращаются через ViewBag. Это позволяет нам вернуть альбом в качестве объекта модели в представление (которое строго типизировано в класс альбома) при передаче дополнительных данных (например, списка жанров) через ViewBag.

[!code-csharp[Main](mvc-music-store-part-5/samples/sample11.cs)]

Действие Edit HTTP-POST очень похоже на действие Create HTTP-POST. Единственное отличие заключается в том, что вместо добавления нового альбома в базу данных. Коллекция альбомов. мы находим текущий экземпляр альбома при помощи базы данных. Запись (альбом) и установка ее состояния в значение Modified. Это говорит Entity Framework, что мы изменяем существующий альбом, в отличие от создания нового.

[!code-csharp[Main](mvc-music-store-part-5/samples/sample12.cs)]

Мы можем протестировать это, запустив приложение и перейдя по адресу/Стореманжер/, а затем щелкнув ссылку Edit (изменить) для альбома.

![](mvc-music-store-part-5/_static/image9.png)

Отобразится форма редактирования, показанная в методе редактирования HTTP-GET. Заполните некоторые значения и нажмите кнопку Сохранить.

![](mvc-music-store-part-5/_static/image10.png)

При этом форма публикуется, сохраняет значения и возвращает нас в список альбомов, показывая, что значения были обновлены.

![](mvc-music-store-part-5/_static/image11.png)

### <a name="handling-deletion"></a>Обработка удаления

При удалении используется тот же шаблон, что и при редактировании и создании, при использовании одного действия контроллера для вывода формы подтверждения и еще одно действие контроллера, обрабатывающее отправку формы.

Действие "HTTP — получить удаление контроллера" точно аналогично предыдущему действию контроллера данных Store Manager.

[!code-csharp[Main](mvc-music-store-part-5/samples/sample13.cs)]

Мы отображаем форму, которая строго типизирована для типа альбома, с помощью шаблона удалить содержимое представления.

![](mvc-music-store-part-5/_static/image12.png)

В шаблоне удаления отображаются все поля модели, но мы можем упростить это немного. Измените код представления в/Виевс/стореманажер/делете.кштмл на следующий.

[!code-cshtml[Main](mvc-music-store-part-5/samples/sample14.cshtml)]

Отобразится упрощенное подтверждение удаления.

![](mvc-music-store-part-5/_static/image13.png)

Нажатие кнопки удалить приводит к обратной передаче формы на сервер, который выполняет действие Делетеконфирмед.

[!code-csharp[Main](mvc-music-store-part-5/samples/sample15.cs)]

Действие "HTTP-после удаления контроллера" выполняет следующие действия.

- 1. Загружает альбом по ИДЕНТИФИКАТОРу
- 2. Удаляет его из альбома и сохраняет изменения
- 3. Перенаправляет на индекс, показывая, что альбом был удален из списка

Чтобы проверить это, запустите приложение и перейдите по/Стореманажер. Выберите альбом из списка и щелкните ссылку удалить.

![](mvc-music-store-part-5/_static/image14.png)

Отобразится экран подтверждения удаления.

![](mvc-music-store-part-5/_static/image15.png)

Нажав кнопку Удалить, вы удаляете альбом и возвращает нам страницу индекса Store Manager, на которой показано, что альбом удален.

![](mvc-music-store-part-5/_static/image16.png)

### <a name="using-a-custom-html-helper-to-truncate-text"></a>Использование пользовательского вспомогательного метода HTML для усечения текста

У нас есть одна потенциальная ошибка на странице индекса Store Manager. Свойства названия и имени исполнителя могут быть достаточно длинными, чтобы они могли создать форматирование таблицы. Мы создадим пользовательский вспомогательный метод HTML, чтобы мы могли легко усекать эти и другие свойства в наших представлениях.

![](mvc-music-store-part-5/_static/image17.png)

Синтаксис @helper Razor значительно упрощает создание собственных вспомогательных функций для использования в представлениях. Откройте представление/Виевс/стореманажер/индекс.кштмл и добавьте следующий код сразу после строки @model.

[!code-cshtml[Main](mvc-music-store-part-5/samples/sample16.cshtml)]

Этот вспомогательный метод принимает строку и максимальную длину для разрешения. Если указанный текст короче указанной длины, вспомогательная функция выводит его как есть. Если он больше, то он усекает текст и визуализирует "..." для оставшейся части.

Теперь мы можем использовать наш вспомогательный метод Truncate, чтобы убедиться, что длина названия и свойства имени исполнителя не превышает 25 символов. Ниже представлен полный код представления, в котором используется наш новый вспомогательный модуль Truncate.

[!code-cshtml[Main](mvc-music-store-part-5/samples/sample17.cshtml)]

Теперь при просмотре URL-адреса/Стореманажер/альбомы и заголовки будут храниться ниже максимальной длины.

![](mvc-music-store-part-5/_static/image18.png)

Примечание. в этом примере показан простой случай создания и использования вспомогательного метода в одном представлении. Дополнительные сведения о создании вспомогательных функций, которые можно использовать на сайте, см. в записи блога: [http://bit.ly/mvc3-helper-options](http://bit.ly/mvc3-helper-options)

> [!div class="step-by-step"]
> [Назад](mvc-music-store-part-4.md)
> [Вперед](mvc-music-store-part-6.md)
