---
uid: web-forms/overview/data-access/masterdetail/master-detail-filtering-with-a-dropdownlist-cs
title: Фильтрация "основной/подробности" с помощьюC#DropDownList () | Документация Майкрософт
author: rick-anderson
description: В этом учебнике мы рассмотрим, как отобразить основные записи в элементе управления DropDownList и сведения о выбранном элементе списка в GridView.
ms.author: riande
ms.date: 03/31/2010
ms.assetid: 53e659cc-eefb-40c1-a1dc-559481c99443
msc.legacyurl: /web-forms/overview/data-access/masterdetail/master-detail-filtering-with-a-dropdownlist-cs
msc.type: authoredcontent
ms.openlocfilehash: 3ec549f9da7a2b3a021e77827f0039e6ae60b5c5
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78424572"
---
# <a name="masterdetail-filtering-with-a-dropdownlist-c"></a>Фильтрация "Основной/подробности" с помощью элемента управления DropDownList (C#)

по [Скотт Митчелл](https://twitter.com/ScottOnWriting)

[Скачивание примера приложения](https://download.microsoft.com/download/4/6/3/463cf87c-4724-4cbc-b7b5-3f866f43ba50/ASPNET_Data_Tutorial_7_CS.exe) или [Загрузка PDF-файла](master-detail-filtering-with-a-dropdownlist-cs/_static/datatutorial07cs1.pdf)

> В этом учебнике мы рассмотрим, как отобразить основные записи в элементе управления DropDownList и сведения о выбранном элементе списка в GridView.

## <a name="introduction"></a>Введение

Общий тип отчета — это отчет « *основной/подробности*», в котором начинается отчет, в котором показан набор «основных» записей. Затем пользователь может выполнить детализацию до одной из основных записей, тем самым просмотрев сведения о главной записи. Отчеты «основной/подробности» являются идеальным выбором для визуализации связей «один ко многим», например для отчета, отображающего все категории, и предоставления пользователю возможности выбора определенной категории и отображения связанных с ней продуктов. Кроме того, отчеты «основной/подробности» полезны для отображения подробных сведений из особенно «широких» таблиц (с большим количеством столбцов). Например, уровень «основной» отчета «основной/подробности» может показывать только название продукта и цену за единицу в базе данных, а детализация конкретного продукта покажет дополнительные поля продуктов (категория, поставщик, количество на единицу и т. д.).

Существует множество способов реализации отчета «основной/подробности». В этом и следующих трех учебных курсах мы рассмотрим разнообразные отчеты «основной/подробности». В этом учебнике мы рассмотрим, как отобразить основные записи в [элементе управления DropDownList](https://msdn.microsoft.com/library/dtx91y0z.aspx) и сведения о выбранном элементе списка в GridView. В частности, в отчете «основной/подробности» этого учебника будут перечислены сведения о категории и продукте.

## <a name="step-1-displaying-the-categories-in-a-dropdownlist"></a>Шаг 1. Отображение категорий в элементе DropDownList

В нашем отчете «основной/подробности» будут перечислены категории в DropDownList, а продукты выбранного элемента списка отображаются на странице в элементе управления GridView. Первая задача, предшествующая нам, заключается в том, чтобы отобразить категории в DropDownList. Откройте страницу `FilterByDropDownList.aspx` в папке `Filtering`, перетащите DropDownList с панели элементов на конструктор страницы и задайте для свойства `ID` значение `Categories`. Затем щелкните ссылку Выбор источника данных из смарт-тега DropDownList. Отобразится мастер настройки источника данных.

[![указать источник данных DropDownList](master-detail-filtering-with-a-dropdownlist-cs/_static/image2.png)](master-detail-filtering-with-a-dropdownlist-cs/_static/image1.png)

**Рис. 1**. Указание источника данных DropDownList ([щелкните, чтобы просмотреть изображение с полным размером](master-detail-filtering-with-a-dropdownlist-cs/_static/image3.png))

Выберите, чтобы добавить новый элемент ObjectDataSource с именем `CategoriesDataSource`, который вызывает метод `GetCategories()` класса `CategoriesBLL`.

[![добавить новый элемент управления ObjectDataSource с именем CategoriesDataSource](master-detail-filtering-with-a-dropdownlist-cs/_static/image5.png)](master-detail-filtering-with-a-dropdownlist-cs/_static/image4.png)

**Рис. 2**. Добавление нового элемента управления ObjectDataSource с именем `CategoriesDataSource` ([щелкните, чтобы просмотреть изображение с полным размером](master-detail-filtering-with-a-dropdownlist-cs/_static/image6.png))

[![выбрать использование класса CategoriesBLL](master-detail-filtering-with-a-dropdownlist-cs/_static/image8.png)](master-detail-filtering-with-a-dropdownlist-cs/_static/image7.png)

**Рис. 3**. Выбор использования класса `CategoriesBLL` ([щелкните, чтобы просмотреть изображение с полным размером](master-detail-filtering-with-a-dropdownlist-cs/_static/image9.png))

[![настроить ObjectDataSource для использования метода-Categories ()](master-detail-filtering-with-a-dropdownlist-cs/_static/image11.png)](master-detail-filtering-with-a-dropdownlist-cs/_static/image10.png)

**Рис. 4**. Настройка ObjectDataSource для использования метода `GetCategories()` ([щелкните, чтобы просмотреть изображение с полным размером](master-detail-filtering-with-a-dropdownlist-cs/_static/image12.png))

После настройки ObjectDataSource необходимо указать поле источника данных, которое должно быть отображено в элементе управления DropDownList, и какое из значений должно быть связано со значением элемента списка. По`CategoryName` поле в качестве отображаемого и `CategoryID` в качестве значения для каждого элемента списка.

[![отображать поле CategoryName и использовать CategoryID в качестве значения](master-detail-filtering-with-a-dropdownlist-cs/_static/image14.png)](master-detail-filtering-with-a-dropdownlist-cs/_static/image13.png)

**Рис. 5**. отображение поля `CategoryName` в DropDownList и использование `CategoryID` в качестве значения ([щелкните, чтобы просмотреть изображение с полным размером](master-detail-filtering-with-a-dropdownlist-cs/_static/image15.png))

На этом этапе у нас есть элемент управления DropDownList, который заполняется записями из таблицы `Categories` (все это выполняется около шести секунд). На рис. 6 показан ход работы в браузере.

[![раскрывающийся список с текущими категориями](master-detail-filtering-with-a-dropdownlist-cs/_static/image17.png)](master-detail-filtering-with-a-dropdownlist-cs/_static/image16.png)

**Рис. 6**. раскрывающийся список с текущими категориями ([щелкните, чтобы просмотреть изображение с полным размером](master-detail-filtering-with-a-dropdownlist-cs/_static/image18.png))

## <a name="step-2-adding-the-products-gridview"></a>Шаг 2. Добавление элемента управления GridView для продуктов

Последним шагом в нашем отчете «основной/подробности» является отображение списка продуктов, связанных с выбранной категорией. Для этого добавьте элемент управления GridView на страницу и создайте новый элемент ObjectDataSource с именем `productsDataSource`. Элементы управления `productsDataSource` изменяют свои данные из метода `GetProductsByCategoryID(categoryID)` класса `ProductsBLL`.

[![выбрать метод GetProductsByCategoryID (КодТипа)](master-detail-filtering-with-a-dropdownlist-cs/_static/image20.png)](master-detail-filtering-with-a-dropdownlist-cs/_static/image19.png)

**Рис. 7**. выбор метода `GetProductsByCategoryID(categoryID)` ([щелкните, чтобы просмотреть изображение с полным размером](master-detail-filtering-with-a-dropdownlist-cs/_static/image21.png))

После выбора этого метода мастер ObjectDataSource запрашивает значение параметра *`categoryID`* метода. Чтобы использовать значение выбранного элемента DropDownList `categories`, установите источник параметра в значение Control, а для ControlID — значение `Categories`.

[![задать для параметра categoryID значение элемента DropDownList категорий](master-detail-filtering-with-a-dropdownlist-cs/_static/image23.png)](master-detail-filtering-with-a-dropdownlist-cs/_static/image22.png)

**Рис. 8**. Установка для параметра *`categoryID`* значения `Categories` DropDownList ([щелкните, чтобы просмотреть изображение с полным размером](master-detail-filtering-with-a-dropdownlist-cs/_static/image24.png))

Уделите немного времени для проверки хода выполнения в браузере. При первом посещении страницы отображаются эти продукты, относящиеся к выбранной категории (напитки) (как показано на рис. 9), но изменение DropDownList не приводит к обновлению данных. Это связано с тем, что для обновления элемента управления GridView должна быть выполнена обратная передача. Для этого у нас есть два варианта (ни один из них не требует написания кода):

- **Задайте**для[Свойства автообратный вызов](https://msdn.microsoft.com/library/system.web.ui.webcontrols.listcontrol.autopostback%28VS.80%29.aspx)категорий**значение true.** (Это можно сделать, установив флажок Включить автообратную передачу в смарт-теге DropDownList.) Это приведет к запуску обратной передачи при изменении пользователем выбранного элемента DropDownList. Таким образом, когда пользователь выбирает новую категорию из DropDownList, произойдет обратная передача, и GridView будет обновлен с использованием продуктов для вновь выбранной категории. (Это подход, который я использовал в этом учебнике.)
- **Добавьте веб-элемент управления "Кнопка" рядом с DropDownList.** Задайте для свойства `Text` значение обновить или что-то подобное. При таком подходе пользователю нужно будет выбрать новую категорию и нажать кнопку. Нажатие кнопки приведет к обратной передаче и обновлению GridView для вывода списка продуктов выбранной категории.

На рисунках 9 и 10 показан отчет «основной/подробности» в действии.

[![при первом посещении страницы отображаются продукты напитков](master-detail-filtering-with-a-dropdownlist-cs/_static/image26.png)](master-detail-filtering-with-a-dropdownlist-cs/_static/image25.png)

**Рис. 9**. при первом посещении страницы отображаются продукты напитков ([щелкните, чтобы просмотреть изображение с полным размером](master-detail-filtering-with-a-dropdownlist-cs/_static/image27.png)).

[![выборе нового продукта (фрукты) автоматически вызывает обратную передачу, обновляя элемент GridView](master-detail-filtering-with-a-dropdownlist-cs/_static/image29.png)](master-detail-filtering-with-a-dropdownlist-cs/_static/image28.png)

**Рис. 10**. Выбор нового продукта (фрукты) автоматически вызывает обратную передачу, обновляя элемент управления GridView ([щелкните, чтобы просмотреть изображение с полным размером](master-detail-filtering-with-a-dropdownlist-cs/_static/image30.png))

## <a name="adding-a----choose-a-category----list-item"></a>Добавление элемента списка "--выберите категорию--"

При первом посещении страницы `FilterByDropDownList.aspx` по умолчанию выбирается первый элемент списка в элементе управления DropDownList, отображая продукты категории «напитки» в GridView. Вместо того чтобы показывать продукты первой категории, нам может потребоваться выбрать элемент DropDownList, который выглядит примерно так: "--выберите категорию--".

Чтобы добавить новый элемент списка в DropDownList, перейдите к окно свойств и щелкните многоточие в свойстве `Items`. Добавьте новый элемент списка с `Text` "--выберите категорию--" и `-1``Value`.

[![Добавить--выберите категорию--элемент списка](master-detail-filtering-with-a-dropdownlist-cs/_static/image32.png)](master-detail-filtering-with-a-dropdownlist-cs/_static/image31.png)

**Рис. 11**. Добавление a--Выбор категории--элемент списка ([щелкните, чтобы просмотреть изображение с полным размером](master-detail-filtering-with-a-dropdownlist-cs/_static/image33.png))

Кроме того, можно добавить элемент списка, добавив в DropDownList следующую разметку:

[!code-aspx[Main](master-detail-filtering-with-a-dropdownlist-cs/samples/sample1.aspx)]

Кроме того, необходимо присвоить `AppendDataBoundItems`у элемента управления DropDownList значение true, так как при привязке категорий к DropDownList из ObjectDataSource они будут перезаписывать все добавленные вручную элементы списка, если `AppendDataBoundItems` не имеет значения true.

![Присвойте свойству Аппенддатабаундитемс значение true.](master-detail-filtering-with-a-dropdownlist-cs/_static/image34.png)

**Рис. 12**. установка свойства `AppendDataBoundItems` в значение true

После внесения этих изменений при первом посещении страницы выбирается параметр "--выбрать категорию--", и продукты не отображаются.

[![при начальной загрузке страницы продукты не отображаются](master-detail-filtering-with-a-dropdownlist-cs/_static/image36.png)](master-detail-filtering-with-a-dropdownlist-cs/_static/image35.png)

**Рис. 13**. при начальной загрузке страницы продукты не отображаются ([щелкните, чтобы просмотреть изображение с полным размером](master-detail-filtering-with-a-dropdownlist-cs/_static/image37.png))

Причина, по которой продукты не отображаются, не отображается, поскольку выбран элемент списка "--выберите категорию--", так как его значение `-1`, а в базе данных нет продуктов с `CategoryID` `-1`. Если это желаемое поведение, то на этом этапе вы закончите! Если же вы хотите отобразить *все* категории при выборе элемента списка "--выберите категорию--", вернитесь к классу `ProductsBLL` и настройте метод `GetProductsByCategoryID(categoryID)`, чтобы он вызывал метод `GetProducts()`, если переданный в *`categoryID`* параметр меньше нуля:

[!code-csharp[Main](master-detail-filtering-with-a-dropdownlist-cs/samples/sample2.cs)]

Используемая методика аналогична подходу, который мы использовали для отображения всех поставщиков в учебнике по [декларативным параметрам](../basic-reporting/declarative-parameters-cs.md) , хотя в этом примере используется значение `-1`, указывающее, что необходимо извлечь все записи, а не `null`. Это обусловлено тем, что параметр *`categoryID`* метода `GetProductsByCategoryID(categoryID)` предполагает, что передано целочисленное значение, в то время как в учебнике по декларативным параметрам мы передали входной параметр String.

На рис. 14 показан снимок экрана `FilterByDropDownList.aspx` при выборе параметра «--выберите категорию--». Здесь все продукты отображаются по умолчанию, и пользователь может уменьшить отображаемые данные, выбрав определенную категорию.

[![все продукты теперь перечислены по умолчанию](master-detail-filtering-with-a-dropdownlist-cs/_static/image39.png)](master-detail-filtering-with-a-dropdownlist-cs/_static/image38.png)

**Рис. 14**. Теперь все продукты перечислены по умолчанию ([щелкните, чтобы просмотреть изображение с полным размером](master-detail-filtering-with-a-dropdownlist-cs/_static/image40.png))

## <a name="summary"></a>Сводка

При отображении иерархически связанных данных часто бывает удобно представлять данные с помощью отчетов «основной/подробности», из которых пользователь может начать изучение данных из верхней части иерархии и детализировать подробные сведения. В этом учебнике мы рассмотрели создание простого отчета «основной/подробности», в котором отображаются продукты выбранной категории. Это было выполнено с помощью DropDownList для списка категорий и GridView для продуктов, принадлежащих выбранной категории.

В [следующем учебном курсе](master-detail-filtering-with-two-dropdownlists-cs.md) мы рассмотрим интерфейс DropDownList на один шаг дальше, используя два элементов управления DropDownList.

Поздравляем с программированием!

## <a name="about-the-author"></a>Об авторе

[Скотт Митчелл](http://www.4guysfromrolla.com/ScottMitchell.shtml), автор семи книг по ASP/ASP. NET и основатель [4GuysFromRolla.com](http://www.4guysfromrolla.com), работал с веб-технологиями Майкрософт с 1998. Скотт работает как независимый консультант, преподаватель и модуль записи. Его последняя книга — [*Sams обучать себя ASP.NET 2,0 за 24 часа*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco). Он доступен по адресу [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) или через его блог, который можно найти по адресу [http://ScottOnWriting.NET](http://ScottOnWriting.NET).

> [!div class="step-by-step"]
> [Дальше](master-detail-filtering-with-two-dropdownlists-cs.md)
