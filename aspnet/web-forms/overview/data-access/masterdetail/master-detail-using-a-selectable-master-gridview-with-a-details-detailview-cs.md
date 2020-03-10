---
uid: web-forms/overview/data-access/masterdetail/master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs
title: "\"Основной/подробности\" с помощью выбираемого элемента управления GridView с подробными сведениями DetailView (C#) | Документация Майкрософт"
author: rick-anderson
description: В этом учебнике есть элемент управления GridView, чьи строки содержат имя и цену каждого продукта вместе с кнопкой выбора. Нажмите кнопку выбрать для партику...
ms.author: riande
ms.date: 03/31/2010
ms.assetid: 0f982827-f8f9-420d-b36b-57b23f5aa519
msc.legacyurl: /web-forms/overview/data-access/masterdetail/master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs
msc.type: authoredcontent
ms.openlocfilehash: 04c427341f063729bd23b416a96f5acb20702792
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78503628"
---
# <a name="masterdetail-using-a-selectable-master-gridview-with-a-details-detailview-c"></a>Отчет "Основной/подробности" с помощью элемента управления GridView с возможностью выбора для основной информации и элемента управления DetailView для подробных сведений (C#)

по [Скотт Митчелл](https://twitter.com/ScottOnWriting)

[Скачивание примера приложения](https://download.microsoft.com/download/4/6/3/463cf87c-4724-4cbc-b7b5-3f866f43ba50/ASPNET_Data_Tutorial_10_CS.exe) или [Загрузка PDF-файла](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/datatutorial10cs1.pdf)

> В этом учебнике есть элемент управления GridView, чьи строки содержат имя и цену каждого продукта вместе с кнопкой выбора. Нажатие кнопки выбрать для конкретного продукта приведет к тому, что все его полные сведения будут отображаться в элементе управления DetailsView на той же странице.

## <a name="introduction"></a>Введение

В [предыдущем учебном курсе](master-detail-filtering-across-two-pages-cs.md) было показано, как создать отчет «основной/подробности» с помощью двух веб-страниц: «главной» веб-страницы, из которой был отображен список поставщиков. и веб-страницу "сведения", в которой перечислены продукты, предоставляемые выбранным поставщиком. Этот формат отчета с двумя страницами можно сжать на одну страницу. В этом учебнике есть элемент управления GridView, чьи строки содержат имя и цену каждого продукта вместе с кнопкой выбора. Нажатие кнопки выбрать для конкретного продукта приведет к тому, что все его полные сведения будут отображаться в элементе управления DetailsView на той же странице.

[![нажатии кнопки выбрать отображает сведения о продукте.](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image2.png)](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image1.png)

**Рис. 1**. нажатие кнопки "выбрать" отображает сведения о продукте ([щелкните, чтобы просмотреть изображение с полным размером](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image3.png))

## <a name="step-1-creating-a-selectable-gridview"></a>Шаг 1. Создание выбираемого элемента управления GridView

Вспомним, что в двух-страничном отчете «основной/подробности» каждая Главная запись включала гиперссылку, которая при щелчке отправляет пользователю на страницу сведений, передавая `SupplierID` значение нажатой строки в строке запроса. Такая гиперссылка была добавлена в каждую строку GridView с помощью HyperLinkField. Для одностраничного отчета «основной/подробности» требуется кнопка для каждой строки GridView, при нажатии которой отображаются подробные сведения. Элемент управления GridView можно настроить для включения кнопки выбора для каждой строки, которая вызывает обратную передачу, и помечает эту строку как [Селектедров](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.selectedrow.aspx)GridView.

Для начала добавьте элемент управления GridView на страницу `DetailsBySelecting.aspx` в папке `Filtering`, установив для свойства `ID` значение `ProductsGrid`. Затем добавьте новый элемент управления ObjectDataSource с именем `AllProductsDataSource`, который вызывает метод `GetProducts()` класса `ProductsBLL`.

[![создать элемент управления ObjectDataSource с именем Аллпродуктсдатасаурце](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image5.png)](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image4.png)

**Рис. 2**. Создание элемента управления ObjectDataSource с именем `AllProductsDataSource` ([щелкните, чтобы просмотреть изображение с полным размером](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image6.png))

[![использования класса ProductsBLL](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image8.png)](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image7.png)

**Рис. 3**. использование класса `ProductsBLL` ([щелкните, чтобы просмотреть изображение с полным размером](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image9.png))

[![настроить ObjectDataSource для вызова метода Products ()](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image11.png)](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image10.png)

**Рис. 4**. Настройка ObjectDataSource для вызова метода `GetProducts()` ([щелкните, чтобы просмотреть изображение с полным размером](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image12.png))

Измените поля GridView, удалив все, кроме `ProductName` и `UnitPrice` BoundFields. Кроме того, вы можете настроить эти BoundFields по мере необходимости, например форматирование `UnitPrice` BoundField в виде валюты и изменение свойств `HeaderText` BoundFields. Эти действия можно выполнить графически, щелкнув ссылку Edit Columns (изменить столбцы) в смарт-теге GridView или настроив декларативный синтаксис вручную.

[![удалить все BoundFields, кроме ProductName и UnitPrice](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image14.png)](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image13.png)

**Рис. 5**. удаление всех `ProductName` и `UnitPrice` BoundFields ([щелкните, чтобы просмотреть изображение с полным размером](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image15.png))

Последняя разметка для GridView:

[!code-aspx[Main](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/samples/sample1.aspx)]

Далее необходимо пометить GridView как выбираемое, что приведет к добавлению кнопки выбрать в каждую строку. Чтобы сделать это, просто установите флажок Включить выбор в смарт-теге GridView.

[![сделать строки GridView выбираемыми](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image17.png)](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image16.png)

**Рис. 6**. обеспечение выбора строк GridView ([щелкните, чтобы просмотреть изображение с полным размером](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image18.png))

При проверке параметра "Включение выбора" в `ProductsGrid` GridView добавляется элемент CommandField со свойством `ShowSelectButton`, установленным в значение true. Это приводит к нажатию кнопки SELECT для каждой строки GridView, как показано на рис. 6. По умолчанию кнопки выбора отображаются как LinkButton, но вместо этого можно использовать кнопки или Имажебуттонс в свойстве `ButtonType` CommandField.

[!code-aspx[Main](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/samples/sample2.aspx)]

При нажатии кнопки выбора строки GridView происходит обратная передача, и свойство `SelectedRow` GridView обновляется. В дополнение к свойству `SelectedRow` GridView предоставляет свойства [SelectedIndex](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.selectedindex%28VS.80%29.aspx), [SelectedValue](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.selectedvalue%28VS.80%29.aspx)и [селектеддатакэй](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.selecteddatakey%28VS.80%29.aspx) . Свойство `SelectedIndex` возвращает индекс выбранной строки, тогда как свойства `SelectedValue` и `SelectedDataKey` возвращают значения, основанные на [свойстве DataKeyNames](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.datakeynames%28VS.80%29.aspx)элемента GridView.

Свойство `DataKeyNames` используется для связывания одного или нескольких значений полей данных с каждой строкой и обычно используется для уникальной идентификации сведений из базовых данных в каждой строке GridView. Свойство `SelectedValue` возвращает значение первого `DataKeyNames` поля данных для выбранной строки, где, как свойство `SelectedDataKey` возвращает объект `DataKey` выбранной строки, который содержит все значения для указанных полей ключа данных для этой строки.

При привязке источника данных к GridView, DetailsView или FormView в конструкторе свойству `DataKeyNames` автоматически присваивается однозначно идентифицирующее поле данных. Хотя это свойство было задано автоматически в предыдущих учебных курсах, примеры работали бы без указанного свойства `DataKeyNames`. Однако для элемента управления GridView в этом учебнике, а также для будущих руководств, в которых мы будем изучать вставку, обновление и удаление, необходимо правильно задать свойство `DataKeyNames`. Подождите, что свойство `DataKeyNames` GridView имеет значение `ProductID`.

Давайте проверим наш ход работы через браузер. Обратите внимание, что в элементе управления GridView указаны имя и цена для всех продуктов, а также выбрана LinkButton. Нажатие кнопки выбрать приводит к выполнению обратной передачи. На этапе 2 мы посмотрим, как элемент DetailsView будет отвечать на эту обратную передачу, отображая сведения о выбранном продукте.

[![каждая строка продукта содержит SELECT LinkButton](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image20.png)](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image19.png)

**Рис. 7**. Каждая строка продукта содержит команду LinkButton ([щелкните, чтобы просмотреть изображение с полным размером](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image21.png)).

### <a name="highlighting-the-selected-row"></a>Выделение выбранной строки

`ProductsGrid` GridView имеет свойство `SelectedRowStyle`, которое можно использовать для диктовки визуального стиля для выбранной строки. Это может повысить эффективность работы пользователя. Это позволяет более точно показать, какая строка GridView выбрана в данный момент. В этом руководстве мы добавим выделенную строку желтым фоном.

Как и в предыдущих учебных курсах, мы стремимся к тому, чтобы параметры, связанные с Aesthetic, определялись как классы CSS. Поэтому создайте новый класс CSS в `Styles.css` с именем `SelectedRowStyle`.

[!code-css[Main](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/samples/sample3.css)]

Чтобы применить этот класс CSS к свойству `SelectedRowStyle` *всех* элементов управления GridView в серии руководств, измените обложку `GridView.skin` в теме `DataWebControls`, чтобы включить параметры `SelectedRowStyle`, как показано ниже.

[!code-aspx[Main](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/samples/sample4.aspx)]

С этим добавлением выбранная строка GridView теперь выделяется желтым цветом фона.

[![настроить внешний вид выбранной строки с помощью свойства Селектедровстиле GridView](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image23.png)](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image22.png)

**Рис. 8**. Настройка внешнего вида выбранной строки с помощью свойства `SelectedRowStyle` GridView ([щелкните, чтобы просмотреть изображение с полным размером](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image24.png))

## <a name="step-2-displaying-the-selected-products-details-in-a-detailsview"></a>Шаг 2. Отображение сведений о выбранном продукте в элементе DetailsView

По завершении `ProductsGrid` GridView остается только добавить DetailsView, отображающий сведения о конкретном выбранном продукте. Добавьте элемент управления DetailsView над элементом GridView и создайте новый объект ObjectDataSource с именем `ProductDetailsDataSource`. Так как мы хотим, чтобы эта DetailsView отображала определенную информацию о выбранном продукте, настройте `ProductDetailsDataSource` для использования метода `GetProductByProductID(productID)` класса `ProductsBLL`.

[![вызвать метод Жетпродуктбипродуктид (productID) класса ProductsBLL](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image26.png)](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image25.png)

**Рис. 9**. вызов метода `GetProductByProductID(productID)` класса `ProductsBLL` ([щелкните, чтобы просмотреть изображение с полным размером](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image27.png))

Получите значение *`productID`* параметра, полученное из свойства `SelectedValue` элемента управления GridView. Как мы обсуждали ранее, свойство `SelectedValue` GridView возвращает первое значение ключа данных для выбранной строки. Поэтому крайне важно, чтобы свойство `DataKeyNames` GridView было установлено в значение `ProductID`, чтобы возвращаемое значение `ProductID` строки возвращалось `SelectedValue`.

[![задать параметр productID для свойства SelectedValue GridView](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image29.png)](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image28.png)

**Рис. 10**. установка параметра *`productID`* для свойства `SelectedValue` GridView ([щелкните, чтобы просмотреть изображение с полным размером](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image30.png))

После того как `productDetailsDataSource` ObjectDataSource правильно настроен и привязан к элементу DetailsView, этот учебник завершен. При первом посещении страницы не выбрана ни одна строка, поэтому свойство `SelectedValue` GridView возвращает `null`. Поскольку нет продуктов со значением `NULL` `ProductID`, метод `GetProductByProductID(productID)` не возвращает никаких записей, что означает, что элемент DetailsView не отображается (см. рис. 11). При нажатии кнопки выбора строки GridView происходит обратная передача и обновляется элемент DetailsView. В этот раз `SelectedValue` свойство GridView возвращает `ProductID` выбранной строки, метод `GetProductByProductID(productID)` возвращает `ProductsDataTable` со сведениями об этом конкретном продукте, а DetailsView показывает эти сведения (см. рис. 12).

[![при первом посещении отображается только GridView](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image32.png)](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image31.png)

**Рис. 11**. при первом посещении отображается только GridView ([щелкните, чтобы просмотреть изображение с полным размером](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image33.png))

[![после выбора строки отображаются сведения о продукте](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image35.png)](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image34.png)

**Рис. 12**. при выборе строки отображаются сведения о продукте ([щелкните, чтобы просмотреть изображение с полным размером](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image36.png)).

## <a name="summary"></a>Сводка

В этом и предыдущих трех руководствах мы видели ряд методов отображения отчетов «основной/подробности». В этом учебнике мы рассмотрели использование выбранного элемента управления GridView для размещения основных записей и DetailsView, чтобы отобразить сведения о выбранной главной записи на той же странице. В предыдущих руководствах мы рассмотрели, как отображать отчеты "основной/подробности" с помощью элементов управления DropDownList и отображать главные записи на одной веб-странице и в подробных записях на другом.

Этот учебник завершает изучение отчетов «основной/подробности». Начиная с следующего учебника мы начнем исследование настраиваемого форматирования с помощью GridView, DetailsView и FormView. Мы посмотрим, как настроить внешний вид этих элементов управления на основе привязанных к ним данных, как суммировать данные в нижнем колонтитуле GridView и как использовать шаблоны для получения более высокого уровня контроля над макетом.

Поздравляем с программированием!

## <a name="about-the-author"></a>Об авторе

[Скотт Митчелл](http://www.4guysfromrolla.com/ScottMitchell.shtml), автор семи книг по ASP/ASP. NET и основатель [4GuysFromRolla.com](http://www.4guysfromrolla.com), работал с веб-технологиями Майкрософт с 1998. Скотт работает как независимый консультант, преподаватель и модуль записи. Его последняя книга — [*Sams обучать себя ASP.NET 2,0 за 24 часа*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco). Он доступен по адресу [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) или через его блог, который можно найти по адресу [http://ScottOnWriting.NET](http://ScottOnWriting.NET).

## <a name="special-thanks-to"></a>Специальная благодарность

Эта серия руководств была рассмотрена многими полезными рецензентами. Специалист по интересу для этого руководства был Хилтон Гизнау. Хотите ознакомиться с моими будущими статьями MSDN? Если это так, расположите строку в [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Назад](master-detail-filtering-across-two-pages-cs.md)
> [Вперед](master-detail-filtering-with-a-dropdownlist-vb.md)
