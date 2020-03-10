---
uid: mvc/overview/older-versions/working-with-the-dropdownlist-box-and-jquery/adding-a-new-category-to-the-dropdownlist-using-jquery-ui
title: Добавление новой категории в DropDownList с помощью пользовательского интерфейса jQuery | Документация Майкрософт
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 01/12/2012
ms.assetid: 44aa1ac4-6ea2-48a2-972d-52710c48eae5
msc.legacyurl: /mvc/overview/older-versions/working-with-the-dropdownlist-box-and-jquery/adding-a-new-category-to-the-dropdownlist-using-jquery-ui
msc.type: authoredcontent
ms.openlocfilehash: 3207079ee468232e5f75b081421241c232936baf
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78433158"
---
# <a name="adding-a-new-category-to-the-dropdownlist-using-jquery-ui"></a>Добавление новой категории в DropDownList с помощью пользовательского интерфейса jQuery

по [Рик Андерсон (](https://twitter.com/RickAndMSFT)

Тег HTML `Select` идеально подходит для представления списка фиксированных данных категорий, но часто приходится добавлять новые категории. Предположим, что нам нужно добавить жанр "Opera" к категориям в нашей базе данных? В этом разделе мы будем использовать пользовательский интерфейс jQuery, чтобы добавить диалоговое окно, которое можно использовать для добавления новой категории. На рисунке ниже показано, как пользовательский интерфейс будет отображаться в браузере.

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image1.png)

Когда пользователь выбирает ссылку " **Добавить новый жанр** ", всплывающее диалоговое окно предлагает пользователю ввести новое название жанра (и, при необходимости, описание). На рисунке ниже показано всплывающее диалоговое окно **Добавление жанра** .

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image2.png)

Если введено новое имя жанра и нажата кнопка **сохранить** , происходит следующее:

1. Вызов AJAX отправляет данные в метод Create в контроллере жанра, который сохраняет новый жанр в базе данных и возвращает новые сведения о жанре (название и идентификатор жанра) в формате JSON.
2. JavaScript добавляет новые данные о жанре в список выбора.
3. JavaScript делает новый жанр выбранным элементом.

   На приведенном ниже рисунке в базу данных был добавлен элемент **Opera** и выбран в раскрывающемся списке **Жанр** . 

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image3.png)

Откройте файл *виевс\стореманажер\креате.кштмл* и замените разметку жанра следующим кодом:

[!code-cshtml[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample1.cshtml)]

Частичное представление `_ChooseGenre` будет содержать всю логику для подключения JavaScript и jQuery, которые используются для реализации функции добавления нового жанра. После завершения кода это будет просто сделать с помощью пользовательского интерфейса исполнителя.

В обозреватель решений щелкните правой кнопкой мыши папку *виевс\стореманажер* и выберите **Добавить**, а затем **Просмотрите**. В поле **View Name input (имя представления** ) введите `_ChooseGenre` а затем нажмите кнопку **Добавить**. Замените разметку в файле *виевс\стореманажер\\_ChooseGenre. cshtml* следующим:

[!code-cshtml[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample2.cshtml)]

В первой строке объявляется, что в качестве модели передается `Album`, точно такую же инструкцию Model, которая находится в представлении Create. Следующие несколько строк являются разметкой вспомогательной функции **метки** . Следующая строка является вызовом модуля **DropDownList** , точно таким же, как в исходном представлении Create. В следующей строке добавляется ссылка с именем `Add New Genre`и стили наподобие кнопки. Строка, содержащая `ValidationMessageFor`, копируется непосредственно из представления создания. Следующие строки:

[!code-html[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample3.html)]

создает скрытый тег div с ИДЕНТИФИКАТОРом `genreDialog`. Для подключения к диалоговому окну **Добавление жанра** с идентификатором `genreDialog` в этом div будет использоваться jQuery. Последние два тега скрипта содержат ссылки на файлы JavaScript, которые будут использоваться для реализации функции добавления нового жанра. Файл */скриптс/чусеженре.ЖС* предоставляется в проекте, он будет рассмотрен позже в этом руководстве.

Запустите приложение и нажмите кнопку **Добавить новый жанр** . В диалоговом окне **Добавление жанра** введите **Opera** в поле **имя** ввода.

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image4.png)

Нажмите кнопку **Сохранить** . Вызов AJAX создает категорию Opera, а затем заполняет раскрывающийся список с помощью Opera и устанавливает Opera в качестве выбранного жанра.

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image5.png)

Введите имя исполнителя, название и Цена, а затем нажмите кнопку **создать** . Если ввести цену меньше $8,99, в верхней части представления индекса появится новый альбом. Убедитесь, что новая запись альбома сохранена в базе данных.

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image6.png)

Попробуйте создать новый жанр только с одной буквой. Следующий код в файле *моделс\женре.КС* задает минимальную и максимальную длину имени жанра.

[!code-csharp[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample4.cs)]

Отчеты о проверке на стороне клиента необходимо ввести строку от 2 до 20 символов.

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image7.png)

### <a name="examining-how-a-new-genre-is-added-to-the-database-and-the-select-list"></a>Проверка добавления нового жанра в базу данных и списка выбора.

Откройте файл *скриптс\чусеженре.ЖС* и изучите код.

[!code-javascript[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample5.js)]

Во второй строке используется идентификатор `genreDialog` для создания диалогового окна в теге DIV в файле *виевс\стореманажер\\_ChooseGenre. cshtml* . Большинство именованных параметров говорят сами за себя. Параметр `autoOpen` имеет значение false, при нажатии кнопки **создать жанр** диалоговое окно открывается явно (это описано в последнем случае). В диалоговом окне есть две кнопки: **сохранить** и **отменить**. Кнопка **Отмена** закрывает диалоговое окно. В следующем коде показана функция **Save** для кнопки.

[!code-javascript[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample6.js)]

`var createGenreForm` выбирается из идентификатора `createGenreForm`. Идентификатор `createGenreForm` был задан в следующем коде, обнаруженном в файле *виевс\женре\\_CreateGenre. cshtml* .

[!code-cshtml[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample7.cshtml)]

Вспомогательная перегрузка [HTML. бегинформ](https://msdn.microsoft.com/library/dd492714.aspx) , используемая в файле *виевс\женре\\_CreateGenre. cshtml* , создает HTML с атрибутом Action, содержащим URL-адрес для отправки формы. Это можно увидеть, отобразив страницу Создание альбома в браузере и выбрав пункт Показать исходный код в браузере. В следующей разметке показан созданный код HTML, содержащий тег form.

[!code-html[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample8.html)]

Строка jQuery `$.post` делает вызов AJAX атрибутом Action (`/StoreManager/Create`) и передает данные из диалогового окна **создание жанра** . Данные состоят из имени нового жанра и необязательного описания. При успешном вызове AJAX в разметку Select добавляется новое имя и значение жанра, а для нового жанра устанавливается выбранное значение. Так как это динамически создаваемая разметка, вы не можете увидеть новый параметр SELECT, просмотрев исходный код в браузере. Новый HTML-код можно увидеть с помощью средств разработчика F12 9 для разработчиков. Чтобы просмотреть новый параметр SELECT, в Internet Explorer 9 нажмите клавишу F12, чтобы запустить средства разработчика F12. Перейдите на страницу создания и добавьте новый жанр, чтобы выбрать новый жанр в списке жанр выбор. В средствах разработчика F12:

1. Перейдите на вкладку HTML.
2. Нажмите значок обновления.  
    ![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image8.png)
3. В поле поиска введите GenreID.
4. С помощью следующего значка   
    ![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image9.png)  
   Перейдите к следующему тегу SELECT:

    [!code-html[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample9.html)]
5. Разверните Последнее значение параметра.

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image10.png)

В следующем коде в файле *скриптс\чусеженре.ЖС* показано, как кнопка **Добавить новый жанра** будет подключена к событию Click и как будет создано диалоговое окно **Добавление нового жанра** .

[!code-javascript[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample10.js)]

В первой строке создается функция Click, присоединенная к кнопке **Добавить новый жанр** . Следующая разметка из файла Виевс\стореманажер\\_ChooseGenre. cshtml показывает, как создается кнопка **Добавить новый жанр** :

[!code-cshtml[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample11.cshtml)]

Метод Load создает и открывает диалоговое окно Добавление жанра и вызывает метод jQuery `parse`, чтобы клиентская проверка находилась на данных, вводимых в диалоговом окне.

В этом разделе вы узнали, как создать диалоговое окно, которое можно использовать для добавления новых данных категорий в список выбора. Вы можете выполнить ту же процедуру для создания пользовательского интерфейса, чтобы добавить нового исполнителя в список выбора исполнителя. В этом учебнике представлен обзор работы с **DropDownList**модуля поддержки HTML ASP.NET MVC. Дополнительные сведения о работе с **DropDownList**см. в разделе "Дополнительные ссылки" ниже. Свяжитесь с нами, если учебник полезен.

Rick.Anderson[at]Microsoft.com

### <a name="additional-references"></a>Дополнительные ссылки

- [ASP.NET MVC — руководство по каскадным раскрывающимся спискам](https://weblogs.asp.net/raduenuca/archive/2011/03/06/asp-net-mvc-cascading-dropdown-lists-tutorial-part-1-defining-the-problem-and-the-context.aspx) с помощью [Раду енука](https://weblogs.asp.net/raduenuca/default.aspx)
- [Выбрано](https://harvesthq.github.com/chosen/) Подключаемый модуль JavaScript, поддерживающий множественный выбор и фильтрацию.

### <a name="contributors"></a>участники;

- [Раду Енука](https://weblogs.asp.net/raduenuca/default.aspx)
- Жан-Сéбастиен Гаупил
- [Михаил Уилсон (](http://bradwilson.typepad.com/)

### <a name="reviewers"></a>Рецензенты

- Жан-Сéбастиен Гаупил
- [Михаил Уилсон (](http://bradwilson.typepad.com/)
- Майк Поуп
- Tom Dykstra)

> [!div class="step-by-step"]
> [Назад](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper.md)
