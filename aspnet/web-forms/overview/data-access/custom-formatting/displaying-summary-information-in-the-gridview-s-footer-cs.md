---
uid: web-forms/overview/data-access/custom-formatting/displaying-summary-information-in-the-gridview-s-footer-cs
title: Отображение сводных данных в нижнем колонтитуле GridView (C#) | Документация Майкрософт
author: rick-anderson
description: Сводные данные часто отображаются в нижней части отчета в строке сводки. Элемент управления GridView может содержать строку нижнего колонтитула, ячейки которой мы можем использовать...
ms.author: riande
ms.date: 03/31/2010
ms.assetid: d50edc31-9286-4c6a-8635-be09e72752a4
msc.legacyurl: /web-forms/overview/data-access/custom-formatting/displaying-summary-information-in-the-gridview-s-footer-cs
msc.type: authoredcontent
ms.openlocfilehash: b258a2bdeaea8da4e9c5c5d8043b167d94e1e817
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78441780"
---
# <a name="displaying-summary-information-in-the-gridviews-footer-c"></a>Отображение сводной информации в нижнем колонтитуле элемента управления GridView (C#)

по [Скотт Митчелл](https://twitter.com/ScottOnWriting)

[Скачивание примера приложения](https://download.microsoft.com/download/9/6/9/969e5c94-dfb6-4e47-9570-d6d9e704c3c1/ASPNET_Data_Tutorial_15_CS.exe) или [Загрузка PDF-файла](displaying-summary-information-in-the-gridview-s-footer-cs/_static/datatutorial15cs1.pdf)

> Сводные данные часто отображаются в нижней части отчета в строке сводки. Элемент управления GridView может включать строку нижнего колонтитула, в которой можно программно внедрять статистические данные. В этом учебнике мы посмотрим, как отображать статистические данные в этой строке нижнего колонтитула.

## <a name="introduction"></a>Введение

В дополнение к просмотру каждой цены продуктов, единиц на складе, единиц по заказу и переупорядочения, пользователь может также заинтересовать статистические сведения, такие как средняя цена, общее количество единиц на складе и т. д. Такие сводные сведения часто отображаются в нижней части отчета в строке сводки. Элемент управления GridView может включать строку нижнего колонтитула, в которой можно программно внедрять статистические данные.

Эта задача предоставляет нам три проблемы:

1. Настройка GridView для вывода строки нижнего колонтитула
2. Определение сводных данных; то есть как вычислить среднюю цену или сумму единиц в запасах?
3. Внедрение сводных данных в соответствующие ячейки строки нижнего колонтитула

В этом учебнике мы посмотрим, как преодолеть эти трудности. В частности, мы создадим страницу со списком категорий в раскрывающемся списке с продуктами выбранной категории, отображаемыми в GridView. GridView будет содержать строку нижнего колонтитула, которая показывает среднюю цену и общее количество единиц в запасе и по заказу для продуктов в этой категории.

[![сводные сведения отображаются в строке нижнего колонтитула GridView.](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image2.png)](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image1.png)

**Рис. 1**. Сводные данные отображаются в строке нижнего колонтитула GridView ([щелкните, чтобы просмотреть изображение с полным размером](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image3.png))

В этом учебнике со сведениями о категориях и интерфейсах "основной" и "подробности" реализованы концепции, описанные в предыдущей [фильтрации "основной/подробности" с помощью DropDownList](../masterdetail/master-detail-filtering-with-a-dropdownlist-cs.md) . Если вы еще не работали с предыдущим руководством, сделайте это, прежде чем продолжить.

## <a name="step-1-adding-the-categories-dropdownlist-and-products-gridview"></a>Шаг 1. Добавление элемента управления DropDownList и Products в элемент управления "категории"

Прежде чем добавлять сводные данные к нижнему колонтитулу GridView, давайте сначала создадим отчет «основной/подробности». После завершения первого шага мы рассмотрим, как включать сводные данные.

Для начала откройте страницу `SummaryDataInFooter.aspx` в папке `CustomFormatting`. Добавьте элемент управления DropDownList и задайте для его `ID` значение `Categories`. Затем щелкните ссылку Выбор источника данных из смарт-тега DropDownList и выберите Добавить новый элемент ObjectDataSource с именем `CategoriesDataSource`, который вызывает метод `GetCategories()` класса `CategoriesBLL`.

[![добавить новый элемент управления ObjectDataSource с именем CategoriesDataSource](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image5.png)](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image4.png)

**Рис. 2**. Добавление нового элемента управления ObjectDataSource с именем `CategoriesDataSource` ([щелкните, чтобы просмотреть изображение с полным размером](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image6.png))

[![, что ObjectDataSource вызывает метод CategoriesBLL класса](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image8.png)](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image7.png)

**Рис. 3**. элемент ObjectDataSource вызывает метод `GetCategories()` класса `CategoriesBLL` ([щелкните, чтобы просмотреть изображение с полным размером](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image9.png))

После настройки элемента управления ObjectDataSource мастер возвращает нас в мастер настройки источника данных DropDownList, из которого необходимо указать, какое значение поля данных должно быть отображено, и какое должно соответствовать значению элемента управления DropDownList `ListItem` s. Отобразите поле `CategoryName` и используйте в качестве значения `CategoryID`.

[![использовать поля CategoryName и CategoryID в качестве текста и значения для ListItem соответственно](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image11.png)](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image10.png)

**Рис. 4**. использование полей `CategoryName` и `CategoryID` в качестве `Text` и `Value` для `ListItem` s соответственно (щелкните,[чтобы просмотреть изображение с полным размером](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image12.png))

На этом этапе у нас есть элемент DropDownList (`Categories`), в котором перечислены категории в системе. Теперь необходимо добавить GridView, в котором перечислены продукты, принадлежащие к выбранной категории. Тем не менее, прежде чем делать это, установите флажок Включить автообратную передачу в смарт-теге DropDownList. Как обсуждалось в разделе *Фильтрация "основной/подробности" с помощью DropDownList* , присвоив свойству `AutoPostBack` dropdownlist значение `true` страница будет отправлена обратно при каждом изменении значения DropDownList. Это приведет к обновлению GridView, отображая продукты для вновь выбранной категории. Если свойство `AutoPostBack` имеет значение `false` (по умолчанию), то изменение категории не приведет к обратной передаче и, следовательно, не обновит список продуктов.

[![установите флажок Включить автообратную передачу в смарт-теге DropDownList.](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image14.png)](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image13.png)

**Рис. 5**. Установите флажок Включить автообратную передачу в смарт-теге DropDownList ([щелкните, чтобы просмотреть изображение с полным размером](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image15.png)).

Добавьте на страницу элемент управления GridView, чтобы отобразить продукты для выбранной категории. Задайте для `ID` GridView значение `ProductsInCategory` и привяжите его к новому ObjectDataSource с именем `ProductsInCategoryDataSource`.

[![добавить новый элемент управления ObjectDataSource с именем Продуктсинкатегоридатасаурце](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image17.png)](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image16.png)

**Рис. 6**. Добавление нового элемента управления ObjectDataSource с именем `ProductsInCategoryDataSource` ([щелкните, чтобы просмотреть изображение с полным размером](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image18.png))

Настройте ObjectDataSource таким образом, чтобы он вызывал метод `GetProductsByCategoryID(categoryID)` класса `ProductsBLL`.

[![, что ObjectDataSource вызывает метод GetProductsByCategoryID (categoryID)](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image20.png)](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image19.png)

**Рис. 7**. вызов метода `GetProductsByCategoryID(categoryID)` ObjectDataSource ([щелкните, чтобы просмотреть изображение с полным размером](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image21.png))

Так как метод `GetProductsByCategoryID(categoryID)` принимает входной параметр, на последнем шаге мастера можно указать источник значения параметра. Чтобы отобразить эти продукты из выбранной категории, необходимо, чтобы параметр был извлечен из `Categories` DropDownList.

[![получить значение параметра categoryID из элемента DropDownList выбранных категорий](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image23.png)](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image22.png)

**Рис. 8**. получение значения параметра *`categoryID`* из DropDownList выбранных категорий ([щелкните, чтобы просмотреть изображение с полным размером](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image24.png))

После завершения работы мастера GridView будет иметь BoundField для каждого свойства продукта. Сделаем эти BoundFields, чтобы отображались только `ProductName`, `UnitPrice`, `UnitsInStock`и `UnitsOnOrder` BoundFields. Вы можете добавлять любые параметры уровня поля в остальные BoundFields (например, форматировать `UnitPrice` как валюту). После внесения этих изменений декларативная разметка GridView должна выглядеть следующим образом:

[!code-aspx[Main](displaying-summary-information-in-the-gridview-s-footer-cs/samples/sample1.aspx)]

На этом этапе у нас есть полностью работающий отчет «основной/подробности», в котором отображается имя, Цена за единицу, единицы складского учета и единицы измерения по заказу для продуктов, принадлежащих выбранной категории.

[![получить значение параметра categoryID из элемента DropDownList выбранных категорий](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image26.png)](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image25.png)

**Рис. 9**. получение значения параметра *`categoryID`* из DropDownList выбранных категорий ([щелкните, чтобы просмотреть изображение с полным размером](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image27.png))

## <a name="step-2-displaying-a-footer-in-the-gridview"></a>Шаг 2. Отображение нижнего колонтитула в GridView

Элемент управления GridView может отображать как строку верхнего, так и нижнего колонтитула. Эти строки отображаются в зависимости от значений свойств `ShowHeader` и `ShowFooter` соответственно, с `ShowHeader` по умолчанию `true` и `ShowFooter` в `false`. Чтобы включить нижний колонтитул в GridView, просто установите для свойства `ShowFooter` значение `true`.

[![присвоить свойству Шовфутер элемента GridView значение true](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image29.png)](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image28.png)

**Рис. 10**. задание для свойства `ShowFooter` GridView значения `true` ([щелкните, чтобы просмотреть изображение с полным размером](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image30.png))

Строка нижнего колонтитула содержит ячейку для каждого поля, определенного в GridView; Однако по умолчанию эти ячейки пусты. Уделите время для просмотра хода выполнения в браузере. Если свойство `ShowFooter` теперь имеет значение `true`, GridView содержит пустую строку нижнего колонтитула.

[![GridView теперь содержит строку нижнего колонтитула](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image32.png)](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image31.png)

**Рис. 11**. Теперь GridView содержит строку нижнего колонтитула ([щелкните, чтобы просмотреть изображение с полным размером](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image33.png))

Строка нижнего колонтитула на рис. 11 не выделена, так как она имеет белый фон. Давайте создадим `FooterStyle` класс CSS в `Styles.css`, который указывает темно-красный фон, а затем настроит файл обложки `GridView.skin` в теме `DataWebControls`, чтобы назначить этот класс CSS свойству `FooterStyle``CssClass` элемента управления GridView. Если вам нужно зарезервировать обложки и темы, см. статью о [просмотре данных с помощью элемента управления ObjectDataSource](../basic-reporting/displaying-data-with-the-objectdatasource-cs.md) .

Для начала добавьте следующий класс CSS в `Styles.css`:

[!code-css[Main](displaying-summary-information-in-the-gridview-s-footer-cs/samples/sample2.css)]

Класс `FooterStyle` CSS аналогичен стилю для класса `HeaderStyle`, хотя цвет фона `HeaderStyle`является более темным, а его текст отображается полужирным шрифтом. Более того, текст в нижнем колонтитуле выравнивается по правому краю, в то время как текст заголовка выравнивается по центру.

Затем, чтобы связать этот класс CSS с нижним колонтитулом GridView, откройте файл `GridView.skin` в теме `DataWebControls` и задайте свойство `CssClass` `FooterStyle`. После этого добавления разметка файла должна выглядеть следующим образом:

[!code-aspx[Main](displaying-summary-information-in-the-gridview-s-footer-cs/samples/sample3.aspx)]

Как видно на снимке экрана, это изменение делает нижний колонтитул более четким.

[![строка нижнего колонтитула GridView теперь имеет цвет фона Реддиш](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image35.png)](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image34.png)

**Рис. 12**. Теперь строка нижнего колонтитула GridView имеет цвет фона Реддиш ([щелкните, чтобы просмотреть изображение с полным размером](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image36.png))

## <a name="step-3-computing-the-summary-data"></a>Шаг 3. Вычисление сводных данных

При отображении нижнего колонтитула GridView мы рассмотрим, как вычислять сводные данные. Существует два способа вычисления этой статистической информации:

1. С помощью SQL-запроса можно выдать дополнительный запрос к базе данных, чтобы вычислить сводные данные для определенной категории. SQL содержит ряд агрегатных функций вместе с предложением `GROUP BY` для указания данных, по которым должны суммироваться данные. Следующий запрос SQL вернет необходимые сведения:  

    [!code-sql[Main](displaying-summary-information-in-the-gridview-s-footer-cs/samples/sample4.sql)]

    Конечно, вам не нужно выдавать этот запрос непосредственно с `SummaryDataInFooter.aspx` страницы, а путем создания метода в `ProductsTableAdapter` и `ProductsBLL`.
2. Вычислите эту информацию по мере добавления в GridView, как описано в разделе [пользовательское форматирование на основе данных](custom-formatting-based-upon-data-cs.md) , обработчик событий `RowDataBound` GridView срабатывает один раз для каждой строки, добавляемой в GridView после привязкой к данным. Создав обработчик событий для этого события, можно удержать общую сумму значений, которые мы хотим агрегировать. После привязки последней строки данных к GridView мы получаем итоги и сведения, необходимые для вычисления среднего значения.

Я обычно использую второй подход, так как он сохраняет поездку в базу данных и усилия, необходимые для реализации сводных функций уровня доступа к данным и уровня бизнес-логики, но любой из этих подходов будет достаточно. В этом учебнике мы будем использовать второй вариант и отслеживаю промежуточный итог с помощью обработчика событий `RowDataBound`.

Создайте обработчик событий `RowDataBound` для GridView, выбрав элемент GridView в конструкторе, щелкнув значок с молнией из окно свойств и дважды щелкнув событие `RowDataBound`. Будет создан новый обработчик событий с именем `ProductsInCategory_RowDataBound` в классе кода программной части `SummaryDataInFooter.aspx` страницы.

[!code-csharp[Main](displaying-summary-information-in-the-gridview-s-footer-cs/samples/sample5.cs)]

Чтобы обеспечить выполнение итоговой суммы, необходимо определить переменные вне области обработчика событий. Создайте следующие четыре переменные уровня страницы:

- `_totalUnitPrice`, типа `decimal`
- `_totalNonNullUnitPriceCount`, типа `int`
- `_totalUnitsInStock`, типа `int`
- `_totalUnitsOnOrder`, типа `int`

Затем напишите код для увеличения этих трех переменных для каждой строки данных, обнаруженной в обработчике событий `RowDataBound`.

[!code-csharp[Main](displaying-summary-information-in-the-gridview-s-footer-cs/samples/sample6.cs)]

Обработчик событий `RowDataBound` начинает с того, что мы работаем с DataRow. После установки `Northwind.ProductsRow` экземпляр, который был только что связан с `GridViewRow`ным объектом в `e.Row`, сохраняется в переменной `product`. Затем выполнение итоговых переменных увеличивается на соответствующие значения текущего продукта (предполагая, что они не содержат значение `NULL` базы данных). Мы отслеживаем общее `UnitPrice` и количество записей, не относящихся к `UnitPrice``NULL`, поскольку средняя цена является частями этих двух чисел.

## <a name="step-4-displaying-the-summary-data-in-the-footer"></a>Шаг 4. Отображение сводных данных в нижнем колонтитуле

При суммировании сводных данных последним шагом является отображение их в строке нижнего колонтитула GridView. Эта задача также может быть выполнена программно с помощью обработчика событий `RowDataBound`. Помните, что обработчик событий `RowDataBound` срабатывает для *каждой* строки, привязанной к GridView, включая строку нижнего колонтитула. Поэтому мы можем расширить наш обработчик событий, чтобы отобразить данные в строке нижнего колонтитула, используя следующий код:

[!code-csharp[Main](displaying-summary-information-in-the-gridview-s-footer-cs/samples/sample7.cs)]

Так как строка нижнего колонтитула добавляется в GridView после добавления всех строк данных, мы можем быть уверены, что по мере готовности к отображению сводных данных в нижнем колонтитуле все выполненные итоговые вычисления будут завершены. Последним шагом является задание этих значений в ячейках нижнего колонтитула.

Чтобы отобразить текст в определенной ячейке нижнего колонтитула, используйте `e.Row.Cells[index].Text = value`, где `Cells` индексирование начинается с 0. Следующий код вычисляет среднюю цену (общую цену, деленную на количество продуктов) и отображает ее вместе с общим количеством единиц в запасах и единицах по порядку в соответствующих ячейках нижнего колонтитула GridView.

[!code-csharp[Main](displaying-summary-information-in-the-gridview-s-footer-cs/samples/sample8.cs)]

На рис. 13 показан отчет после добавления этого кода. Обратите внимание, что `ToString("c")` приводит к форматированию средней сводной информации о ценах как денежной.

[![строка нижнего колонтитула GridView теперь имеет цвет фона Реддиш](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image38.png)](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image37.png)

**Рис. 13**. Теперь строка нижнего колонтитула GridView имеет цвет фона Реддиш ([щелкните, чтобы просмотреть изображение с полным размером](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image39.png))

## <a name="summary"></a>Сводка

Отображение сводных данных является общим требованием к отчету, а элемент управления GridView упрощает включение таких сведений в строку нижнего колонтитула. Строка нижнего колонтитула отображается, когда свойству `ShowFooter` GridView присвоено значение `true` и текст в ячейках может быть задан программно с помощью обработчика событий `RowDataBound`. Вычисление сводных данных может выполняться путем повторного запроса к базе данных или с помощью кода в классе кода программной части страницы ASP.NET для программного вычисления сводных данных.

Это руководство завершает изучение пользовательского форматирования с помощью элементов управления GridView, DetailsView и FormView. В нашем следующем учебнике мы начнем с того, чтобы исследовать вставку, обновление и удаление данных с помощью этих же элементов управления.

Поздравляем с программированием!

## <a name="about-the-author"></a>Об авторе

[Скотт Митчелл](http://www.4guysfromrolla.com/ScottMitchell.shtml), автор семи книг по ASP/ASP. NET и основатель [4GuysFromRolla.com](http://www.4guysfromrolla.com), работал с веб-технологиями Майкрософт с 1998. Скотт работает как независимый консультант, преподаватель и модуль записи. Его последняя книга — [*Sams обучать себя ASP.NET 2,0 за 24 часа*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco). Он доступен по адресу [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) или через его блог, который можно найти по адресу [http://ScottOnWriting.NET](http://ScottOnWriting.NET).

> [!div class="step-by-step"]
> [Назад](using-the-formview-s-templates-cs.md)
> [Вперед](custom-formatting-based-upon-data-vb.md)
