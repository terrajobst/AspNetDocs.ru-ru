---
uid: web-forms/overview/data-access/enhancing-the-gridview/inserting-a-new-record-from-the-gridview-s-footer-vb
title: Вставка новой записи из нижнего колонтитула GridView (VB) | Документация Майкрософт
author: rick-anderson
description: Элемент управления GridView предлагает встроенную поддержку для вставки новой записи данных, этого руководстве показано, как для расширения GridView для включения...
ms.author: riande
ms.date: 03/06/2007
ms.assetid: 528acc48-f20c-4b4e-aa16-4cc02f068ebb
msc.legacyurl: /web-forms/overview/data-access/enhancing-the-gridview/inserting-a-new-record-from-the-gridview-s-footer-vb
msc.type: authoredcontent
ms.openlocfilehash: 0c661190125e818d3abaf54f50a0067d0944a956
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57059391"
---
<a name="inserting-a-new-record-from-the-gridviews-footer-vb"></a>Вставка новой записи из нижнего колонтитула GridView (VB)
====================
по [Скотт Митчелл](https://twitter.com/ScottOnWriting)

[Скачайте пример приложения](http://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_53_VB.exe) или [скачать PDF](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/datatutorial53vb1.pdf)

> Элемент управления GridView предлагает встроенную поддержку для вставки новой записи данных, в этом руководстве показано как повысить эффективность GridView, чтобы включить интерфейс для вставки.


## <a name="introduction"></a>Вступление

Как уже говорилось в [Обзор Вставка, обновление и удаление данных](../editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-vb.md) учебника, элементы GridView, DetailsView и FormView Web управления включают встроенные возможности изменения. При использовании с декларативной источников данных, эти три веб-элементы управления можно быстро и легко настроить для изменения данных — и в сценариях без необходимости писать ни одной строки кода. К сожалению только эти элементы управления DetailsView и FormView обеспечивают встроенные Вставка, редактирование и удаление возможностей. GridView предоставляет только поддержки правки и удаления. Однако с небольшой паста изгибом, мы можем расширить GridView, чтобы включить интерфейс для вставки.

При добавлении возможности вставки к GridView, мы отвечаем решить, каким образом новые записи будут добавлены, создание интерфейса вставки и написание кода для вставки новой записи. В этом учебном курсе мы рассмотрим добавление интерфейса вставки в нижнем колонтитуле GridView s строки (см. рис. 1). Ячейкой нижним колонтитулом для каждого столбца включает в себя соответствующие данные коллекции элемент пользовательского интерфейса (текстовое поле для имени продукта s, элемента управления DropDownList для поставщика и т. д.). Мы также требуется столбец для добавления кнопка, при щелчке, вызывает обратную передачу и вставить новую запись в `Products` таблицу с помощью значения, заданные в строке нижнего колонтитула.


[![Строки нижнего колонтитула предоставляет интерфейс для добавления новых продуктов](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image1.gif)](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image1.png)

**Рис. 1**: Строки нижнего колонтитула предоставляет интерфейс для добавления новых продуктов ([Просмотр полноразмерного изображения](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image2.png))


## <a name="step-1-displaying-product-information-in-a-gridview"></a>Шаг 1. Отображение информации о продукте в элементе управления GridView

Прежде чем заняться Создание интерфейса вставки в нижнем колонтитуле GridView s, позвольте s сначала остановиться на добавление элемента GridView на страницу, которая перечисляет продукты в базе данных. Сначала откройте `InsertThroughFooter.aspx` странице в `EnhancedGridView` папки и перетащите элемент управления GridView с панели элементов в конструктор, установив GridView s `ID` свойства `Products`. Затем используйте смарт-тега GridView s, чтобы привязать его к элементу управления ObjectDataSource с именем `ProductsDataSource`.


[![Создайте новый ObjectDataSource, именуемый ProductsDataSource](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image2.gif)](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image3.png)

**Рис. 2**: Создайте новый ObjectDataSource с именем `ProductsDataSource` ([Просмотр полноразмерного изображения](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image4.png))


Настройка ObjectDataSource на использование `ProductsBLL` класс s `GetProducts()` метод для получения сведений о продуктах. В этом учебнике let s планируют освоение строго возможности вставки и не беспокоиться об изменении и удалении. Таким образом, убедитесь, что раскрывающемся списке на вкладке "Вставка" присвоено `AddProduct()` и раскрывающиеся списки на вкладках UPDATE и DELETE установлены (нет).


[![Сопоставить метод AddProduct методом Insert() s ObjectDataSource](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image3.gif)](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image5.png)

**Рис. 3**: Карта `AddProduct` метод ObjectDataSource s `Insert()` метод ([Просмотр полноразмерного изображения](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image6.png))


[![Установить обновление и удаление вкладки раскрывающихся списков (нет)](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image4.gif)](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image7.png)

**Рис. 4**: Установить обновление и удаление вкладок раскрывающиеся списки (нет) ([Просмотр полноразмерного изображения](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image8.png))


После завершения работы мастера настройки источника данных s ObjectDataSource Visual Studio автоматически добавит поля GridView для каждого из соответствующих полей данных. Пока оставьте все поля, добавленные в Visual Studio. Далее в этом руководстве мы вернемся и удалить некоторые поля, значения которых кое t необходимо указать при добавлении новой записи.

Так как можно ближе к 80 продуктов в базе данных, пользователю придется прокрутить вплоть до нижней части веб-страницы, чтобы добавить новую запись. Таким образом позволяют включить разбиение на страницы сделать интерфейс вставки более видимым и доступным s. Чтобы включить разбиение по страницам, просто установите флажок Включить разбиение по страницам в смарт-теге GridView s.

На этом этапе GridView и ObjectDataSource s декларативная разметка должна выглядеть следующим:


[!code-aspx[Main](inserting-a-new-record-from-the-gridview-s-footer-vb/samples/sample1.aspx)]


[![В элементе управления GridView, разбитых на страницы отображаются все поля данных продукта](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image5.gif)](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image9.png)

**Рис. 5**: В элементе управления GridView, разбитых на страницы отображаются все поля данных продукта ([Просмотр полноразмерного изображения](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image10.png))


## <a name="step-2-adding-a-footer-row"></a>Шаг 2. Добавление строки нижнего колонтитула

Вместе с заголовка, так и строк данных GridView включает строку нижнего колонтитула. В зависимости от значения GridView s отображаются строки верхнего и нижнего колонтитулов [ `ShowHeader` ](https://msdn.microsoft.com/en-gb/library/system.web.ui.webcontrols.gridview.showheader.aspx) и [ `ShowFooter` ](https://msdn.microsoft.com/en-gb/library/system.web.ui.webcontrols.gridview.showfooter.aspx) свойства. Чтобы отобразить строки нижнего колонтитула, просто задайте `ShowFooter` свойства `True`. Как показано на рис. 6, параметр `ShowFooter` свойства `True` добавляет строку нижнего колонтитула в сетку.


[![Чтобы отобразить строки нижнего колонтитула, установите значение True для ShowFooter](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image6.gif)](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image11.png)

**Рис. 6**: Для отображения строки нижнего колонтитула, задайте `ShowFooter` для `True` ([Просмотр полноразмерного изображения](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image12.png))


Обратите внимание, что строки нижнего колонтитула цвет Темно-красный фон. Это происходит из-за тему DataWebControls, мы создали и применяются ко всем страницам в [отображение данных с ObjectDataSource](../basic-reporting/displaying-data-with-the-objectdatasource-vb.md) руководства. В частности `GridView.skin` файл настраивает `FooterStyle` свойство таких что он использует `FooterStyle` класс CSS. `FooterStyle` Класс определен в `Styles.css` следующим образом:


[!code-css[Main](inserting-a-new-record-from-the-gridview-s-footer-vb/samples/sample2.css)]

> [!NOTE]
> Мы ve использовать с помощью строки нижнего колонтитула GridView s в предыдущих учебных курсах. При необходимости обращаться к [отображение сведения о в нижнем колонтитуле элемента GridView](../custom-formatting/displaying-summary-information-in-the-gridview-s-footer-vb.md) учебника в памяти.


После задания `ShowFooter` свойства `True`, Отвлекитесь и просмотреть выходные данные в браузере. В настоящее время t строки нижнего колонтитула содержит текст или веб-элементов управления. На шаге 3 мы изменим нижний колонтитул для каждого поля GridView, теперь она содержит соответствующий интерфейс вставки.


[![Пустая строка является отображается над разбиение по страницам элементы управления интерфейса](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image7.gif)](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image13.png)

**Рис. 7**: Пустая строка является отображается над разбиение по страницам элементы управления интерфейса ([Просмотр полноразмерного изображения](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image14.png))


## <a name="step-3-customizing-the-footer-row"></a>Шаг 3. Настройка строки нижнего колонтитула

Вернитесь в [использование полей TemplateField в элементе управления GridView](../custom-formatting/using-templatefields-in-the-gridview-control-vb.md) руководства мы узнали, как значительно настраивать отображение определенного столбца GridView использование полей TemplateField (в отличие от полей BoundField или CheckBoxFields), в списке [ Настройка интерфейса изменения данных](../editing-inserting-and-deleting-data/customizing-the-data-modification-interface-vb.md) мы рассмотрели использование полей TemplateField для настройки интерфейса правки в элементе управления GridView. Вспомним, что поле TemplateField представляет собой ряд шаблонов, определяющий набор разметки, веб-элементы управления и синтаксис привязки данных использовался с определенными типами строк. `ItemTemplate`, К примеру, указывает шаблон, используемый для строк только для чтения, пока `EditItemTemplate` определяет шаблон для редактируемой строки.

Вместе с `ItemTemplate` и `EditItemTemplate`, также включает TemplateField `FooterTemplate` , указывает содержимое строки нижнего колонтитула. Таким образом, можно добавить веб-элементы управления, необходимые для каждого поля s, интерфейс в `FooterTemplate`. Чтобы начать, преобразуйте все поля в GridView в поля TemplateField. Это можно сделать, щелкнув ссылку Правка столбцов в GridView s смарт-тег, выделяя каждое поле в левом нижнем углу и выбрав Convert это поле в TemplateField ссылку.


![Преобразовать каждое поле в TemplateField](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image8.gif)

**Рис. 8**: Преобразовать каждое поле в TemplateField


Это поле в TemplateField, щелкнув Convert включает текущий тип поля в эквивалентные TemplateField. Например, каждый BoundField заменяется TemplateField с `ItemTemplate` , содержащий метку для отображения соответствующего поля данных и `EditItemTemplate` , отображающий поле данных в текстовое поле. `ProductName` BoundField преобразования в TemplateField следующую разметку:


[!code-aspx[Main](inserting-a-new-record-from-the-gridview-s-footer-vb/samples/sample3.aspx)]

Аналогичным образом `Discontinued` CheckBoxField будет преобразована в поле TemplateField, `ItemTemplate` и `EditItemTemplate` содержать флажок веб-элемент управления (с `ItemTemplate` s флажок отключен). Только для чтения `ProductID` преобразования BoundField в поле TemplateField в элемент управления Label в обоих `ItemTemplate` и `EditItemTemplate`. Короче говоря поле в TemplateField преобразование существующих GridView — быстрый и простой способ переключиться расширенными возможностями настройки TemplateField без потери каких-либо существующие функциональные возможности поле s.

С момента GridView мы повторно работа с t поддержки редактирования, вы можете удалить `EditItemTemplate` из каждого TemplateField, оставляя только `ItemTemplate`. После этого декларативная разметка s GridView должен выглядеть следующим образом:


[!code-aspx[Main](inserting-a-new-record-from-the-gridview-s-footer-vb/samples/sample4.aspx)]

Теперь, когда в поле TemplateField преобразования каждого поля GridView, мы можем ввести соответствующий интерфейс вставки в каждом поле s `FooterTemplate`. Некоторые поля не будет иметь интерфейс для вставки (`ProductID`, к примеру); другие зависит от веб-элементов управления, используемую для сбора информацию о новых продуктах s.

Чтобы создать интерфейс редактирования, выберите ссылку Изменить шаблоны в смарт-теге GridView s. Затем выберите в раскрывающемся списке выберите соответствующее поле s `FooterTemplate` и перетащите соответствующий элемент управления из области элементов в конструктор.


[![Добавить соответствующий интерфейс вставки FooterTemplate s каждого поля](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image9.gif)](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image15.png)

**Рис. 9**: Добавьте соответствующий интерфейс вставки для каждого поля s `FooterTemplate` ([Просмотр полноразмерного изображения](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image16.png))


Следующем маркированном списке перечисляет поля GridView, с указанием интерфейса вставки для добавления:

- `ProductID` нет.
- `ProductName` Добавление текстового поля и задайте его `ID` для `NewProductName`. Добавьте элемент управления RequiredFieldValidator, чтобы убедиться, что пользователь вводит значение для нового названия продукта s.
- `SupplierID` нет.
- `CategoryID` нет.
- `QuantityPerUnit` Добавление текстового поля, установка его `ID` для `NewQuantityPerUnit`.
- `UnitPrice` Добавление текстового поля с именем `NewUnitPrice` и CompareValidator, которое гарантирует, что введенное значение является значение валюты, больше или равно нулю.
- `UnitsInStock` использовать текстовое поле, `ID` присваивается `NewUnitsInStock`. Включить элемент управления CompareValidator, гарантирует, что введенное значение: целочисленное значение больше или равно нулю.
- `UnitsOnOrder` использовать текстовое поле, `ID` присваивается `NewUnitsOnOrder`. Включить элемент управления CompareValidator, гарантирует, что введенное значение: целочисленное значение больше или равно нулю.
- `ReorderLevel` использовать текстовое поле, `ID` присваивается `NewReorderLevel`. Включить элемент управления CompareValidator, гарантирует, что введенное значение: целочисленное значение больше или равно нулю.
- `Discontinued` Добавление флага, установка его `ID` для `NewDiscontinued`.
- `CategoryName` Добавление элемента управления DropDownList и задание его `ID` для `NewCategoryID`. Привяжите его к элементу управления ObjectDataSource с именем `CategoriesDataSource` и настройте его для использования `CategoriesBLL` класс s `GetCategories()` метод. У элемента управления DropDownList s `ListItem` отображения s `CategoryName` данных поле, с помощью `CategoryID` поля данных, как их значения.
- `SupplierName` Добавление элемента управления DropDownList и задание его `ID` для `NewSupplierID`. Привяжите его к элементу управления ObjectDataSource с именем `SuppliersDataSource` и настройте его для использования `SuppliersBLL` класс s `GetSuppliers()` метод. У элемента управления DropDownList s `ListItem` отображения s `CompanyName` данных поле, с помощью `SupplierID` поля данных, как их значения.

Для каждого из элементов управления проверки, очистите `ForeColor` свойство, чтобы `FooterStyle` CSS класс s белый цвет будет использоваться вместо используемого по умолчанию красным. Также используйте `ErrorMessage` свойство подробное описание, но значение `Text` свойство звездочку. Чтобы не вызывал текст элемента управления s проверки интерфейса вставки программы-оболочки на две строки, задайте `FooterStyle` s `Wrap` значение false для каждого из `FooterTemplate` , которые используют проверяющим элементом управления. Наконец, добавьте элемент управления ValidationSummary под GridView и задайте его `ShowMessageBox` свойства `True` и его `ShowSummary` свойства `False`.

При добавлении нового продукта, то необходимо предоставить `CategoryID` и `SupplierID`. Эта информация захватывается посредством элементов управления DropDownList в ячейках нижний колонтитул для `CategoryName` и `SupplierName` поля. Я решил использовать эти поля, в отличие от `CategoryID` и `SupplierID` полей TemplateField так, как пользователь в сетке s столбцы данных, скорее всего более интересуют имена категорию и поставщика, а не значениями Идентификаторов. Так как `CategoryID` и `SupplierID` значения теперь записываются в `CategoryName` и `SupplierName` вставки интерфейсы s поля, мы можем удалить `CategoryID` и `SupplierID` полей TemplateField из GridView.

Аналогичным образом `ProductID` не используется при добавлении нового продукта, поэтому `ProductID` TemplateField можно также удалить. Тем не менее, позволить оставить s `ProductID` в сетке. В дополнение к текстовых полей, элементов управления DropDownList, флажки и элементы управления проверки, составляющие интерфейс вставки, нам также потребуется добавить кнопка, при щелчке, выполняет действия, чтобы добавить новый продукт в базу данных. На шаге 4 мы включаем кнопку «Add» в интерфейсе правки в `ProductID` TemplateField s `FooterTemplate`.

Вы можете улучшить внешний вид различных полей GridView. Например, может потребоваться отформатировать `UnitPrice` значения как денежной единицы, — по правому краю `UnitsInStock`, `UnitsOnOrder`, и `ReorderLevel` поля и обновление `HeaderText` значения для полей TemplateField.

После создания масса Вставка интерфейсов в `FooterTemplate` s, удаление `SupplierID`, и `CategoryID` поля TemplateField и повышая внешнее представление сетки через форматирование и выравнивание полей TemplateField, ваш декларативной s GridView Разметка должна выглядеть следующим образом:


[!code-aspx[Main](inserting-a-new-record-from-the-gridview-s-footer-vb/samples/sample5.aspx)]

При просмотре в обозревателе, строке нижнего колонтитула GridView s теперь включает в себя завершенные Вставка интерфейса (см. рис. 10). На этом этапе вставки t интерфейса включают средства для пользователя указать, она s введенные данные о новом продукте и хочет, чтобы вставить новую запись в базу данных. Кроме того, мы ve еще, чтобы решить, каким образом данные, вводимые в нижнем колонтитуле будет преобразовано в новую запись в `Products` базы данных. На шаге 4, мы рассмотрим способы включить кнопку "Добавить", чтобы интерфейс вставки и для выполнения кода на обратную передачу при его щелчке s. Шаг 5 показано, как вставить новую запись с использованием данных из нижнего колонтитула.


[![Нижнего колонтитула GridView предоставляет интерфейс для добавления новой записи](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image10.gif)](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image17.png)

**Рис. 10**: Нижнего колонтитула GridView предоставляет интерфейс для добавления новой записи ([Просмотр полноразмерного изображения](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image18.png))


## <a name="step-4-including-an-add-button-in-the-inserting-interface"></a>Шаг 4. Включая кнопку «Add» в интерфейсе правки

Нам нужно включить кнопку добавления где-нибудь в интерфейсе вставки, так как s строки нижнего колонтитула, интерфейсам, в настоящее время отсутствуют средства для пользователя указать, что они завершили ввод информацию о новых продуктах s. Это могут быть размещены в одном из существующих `FooterTemplate` s или мы может добавить новый столбец в сетке для этой цели. Для этого руководства позволяют s поместить кнопку Add в `ProductID` TemplateField s `FooterTemplate`.

В режиме конструктора щелкните ссылку Изменить шаблоны в смарт-теге GridView s и выберите `ProductID` поле s `FooterTemplate` из раскрывающегося списка. Добавить кнопку веб-элемент управления (LinkButton или ImageButton, если вы предпочитаете) в шаблон, указав его идентификатор `AddProduct`, ее `CommandName` операциями вставки и его `Text` свойство добавить, как показано на рис. 11.


[![Поместите «добавить» в FooterTemplate s ProductID TemplateField](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image11.gif)](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image19.png)

**Рис. 11**: Поместите кнопку "Добавить" в `ProductID` TemplateField s `FooterTemplate` ([Просмотр полноразмерного изображения](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image20.png))


Как только вы ve включены «добавить», проверьте страницу в браузере. Обратите внимание, что при нажатии кнопки «Добавить» с недопустимыми данными в интерфейсе правки, обратную передачу коротких circuited и управления ValidationSummary указывает недопустимые данные (см. рис. 12). С помощью соответствующие данные, введенные нажав кнопку «Добавить» вызывает обратную передачу. Отсутствует запись добавляется в базу данных, тем не менее. Нам потребуется написать небольшой фрагмент кода для фактического выполнения инструкции insert.


[![S добавить кнопку обратная передача находится в короткое Circuited при недопустимых данных в интерфейсе вставки](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image12.gif)](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image21.png)

**Рис. 12**: Добавление кнопки с обратной передачи — это короткие Circuited при недопустимых данных в интерфейсе вставки ([Просмотр полноразмерного изображения](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image22.png))


> [!NOTE]
> Проверяющие элементы управления в интерфейсе правки не были назначены в группу проверки. Это работает отлично до тех пор, пока интерфейс вставки — это единственный набор элементов управления проверки на странице. Если, однако существуют и другие элементы управления проверки на странице (например, элементов управления проверки в существующем интерфейсе правки сетки s), элементов управления проверки в Вставка интерфейса и добавьте кнопку s `ValidationGroup` свойства должны назначаться и то же значение so как для Свяжите эти элементы управления с группой определенной проверки. См. в разделе [разбор элементов управления проверки в ASP.NET 2.0](http://aspnet.4guysfromrolla.com/articles/112305-1.aspx) Дополнительные сведения о секционировании проверяющие элементы управления и кнопки на странице на группы проверки.


## <a name="step-5-inserting-a-new-record-into-theproductstable"></a>Шаг 5. Вставка новой записи в`Products`таблицы

При использовании встроенных функций редактирования элемента управления GridView, GridView автоматически обрабатывает все действия, необходимые для выполнения обновления. В частности, при нажатии кнопки "Обновить", он копирует значений, введенных из интерфейса правки с параметрами ObjectDataSource s `UpdateParameters` коллекции и запущена off обновления путем вызова ObjectDataSource s `Update()` метод. Так как GridView не поддерживает такие встроенные функции для вставки, нужно реализовать код, который вызывает ObjectDataSource s `Insert()` метод и копирует значения из вставку интерфейс ObjectDataSource s `InsertParameters` коллекции .

Эта логика вставки должен быть выполнен после нажатия кнопки Добавить. Как уже говорилось в [Добавление и реагирование на кнопки в элементе управления GridView](../custom-button-actions/adding-and-responding-to-buttons-to-a-gridview-vb.md) учебник, каждый раз, когда нажата кнопка, LinkButton или ImageButton в элементе управления GridView, GridView s `RowCommand` вызывает событие при обратной передаче. Это событие возникает, кнопки, LinkButton или ImageButton был ли добавлен явным образом такие как «добавить» в строке нижнего колонтитула или если она автоматически добавляется GridView (например, элементов управления LinkButton в верхней части каждого столбца, если установлен флажок Включить сортировку, или Элементов управления LinkButton в интерфейсе разбиения по страницам при выборе Включить разбиение по страницам).

Таким образом, чтобы реагировать на пользователя, нажав кнопку «Добавить», необходимо создать обработчик событий для GridView s `RowCommand` событий. Так как это событие возникает каждый раз, когда *любой* нажатии кнопки LinkButton и ImageButton в GridView его s жизненно важных, что мы только продолжить вставку логики Если `CommandName` свойство, переданное в схемы обработчик событий для `CommandName` значение «добавить» (Insert). Кроме того мы также продолжать следует только при допустимые данные отчета, проверяющие элементы управления. Чтобы решить эту проблему, создайте обработчик событий для `RowCommand` событий следующим кодом:


[!code-vb[Main](inserting-a-new-record-from-the-gridview-s-footer-vb/samples/sample6.vb)]

> [!NOTE]
> Может возникнуть вопрос, почему обработчик событий остановились проверка `Page.IsValid` свойство. В конце концов Если недопустимые данные в интерфейсе правки подавить реализованных t обратную передачу? Это предположение относится правильно, пока пользователь не отключил JavaScript или принимает меры для обхода логику проверки на стороне клиента. Иными словами один не следует полагаться исключительно на клиентской проверки; всегда следует выполнять проверку на стороне сервера на допустимость перед началом работы с данными.


На этапе 1 мы создали `ProductsDataSource` ObjectDataSource таким образом, чтобы его `Insert()` относящимся `ProductsBLL` класс s `AddProduct` метод. Для вставки новой записи в `Products` таблицы, мы можете просто вызвать ObjectDataSource s `Insert()` метод:


[!code-vb[Main](inserting-a-new-record-from-the-gridview-s-footer-vb/samples/sample7.vb)]

Теперь, когда `Insert()` метод был вызван, остается лишь для копирования значений из интерфейса вставки с параметрами, передаваемое в `ProductsBLL` класс s `AddProduct` метод. Как мы видели в [Проверка события, связанные с вставки, обновления и удаления](../editing-inserting-and-deleting-data/examining-the-events-associated-with-inserting-updating-and-deleting-vb.md) учебника, это можно сделать через ObjectDataSource s `Inserting` событий. В `Inserting` событий, нам нужно программно сослаться на элементы управления из `Products` нижнего колонтитула GridView s строк и назначить их значения для `e.InputParameters` коллекции. Когда пользователь опускает значение, например оставляя `ReorderLevel` пустое текстовое поле, нам нужно указать, что значение, вставляемое в базе данных должны быть `NULL`. Так как `AddProducts` метод принимает обнуляемые типы для полей, допускающие значения NULL базы данных, просто использовать тип, допускающий значение NULL и присвойте ему значение `Nothing` в случае, когда опускается ввод данных пользователем.


[!code-vb[Main](inserting-a-new-record-from-the-gridview-s-footer-vb/samples/sample8.vb)]

С помощью `Inserting` доделан, новые записи добавляются в `Products` таблицы базы данных с помощью строки нижнего колонтитула GridView s. Продолжим и попробуйте добавить несколько новых продуктов.

## <a name="enhancing-and-customizing-the-add-operation"></a>Улучшение и настройка добавить операцию

В настоящее время кнопку Add добавляет новую запись в таблицу базы данных, но не предоставляет каких-либо визуальной обратной связи, что запись успешно добавлена. В идеальном случае Label Web элемента управления или клиентского окна предупреждения будет информировать пользователя, что их insert была выполнена успешно. Оставить этот в качестве упражнения для чтения.

GridView, используемый в этом руководстве не применяется выполняет сортировку для перечисленных продуктов и не позволяет пользователю сортировать данные. Следовательно записи упорядочены, как в базе данных путем их поле первичного ключа. Так как каждая новая запись имеет `ProductID` значение большее, чем последний, каждый раз при добавлении нового продукта приписываются в конец сетки. Таким образом можно автоматически отправлять пользователю на последнюю страницу элемент GridView после добавления новой записи. Это можно сделать, добавив следующую строку кода после вызова `ProductsDataSource.Insert()` в `RowCommand` обработчик событий, чтобы указать, что пользователь должен отправляться к последней странице после привязки данных к GridView:


[!code-vb[Main](inserting-a-new-record-from-the-gridview-s-footer-vb/samples/sample9.vb)]

`SendUserToLastPage` Логическая переменная уровня страницы, изначально назначается значение `False`. В GridView s `DataBound` обработчик событий, если `SendUserToLastPage` имеет значение false, `PageIndex` обновляется свойство будет перенаправлен на последнюю страницу.


[!code-vb[Main](inserting-a-new-record-from-the-gridview-s-footer-vb/samples/sample10.vb)]

Причина `PageIndex` свойство задается в `DataBound` обработчик событий (в отличие от `RowCommand` обработчик событий) так как при `RowCommand` обработчик событий запускает мы ve еще, чтобы добавить новую запись для `Products` таблицы базы данных. Таким образом, в `RowCommand` обработчик событий индекс последней страницы (`PageCount - 1`) представляет индекс последней страницы *перед* был добавлен новый продукт. Для большинства продуктов добавляемого последний индекс страницы аналогичен после добавления нового продукта. Но когда добавленный продукт приводит новый последний индекс страницы, если мы изменим неправильно `PageIndex` в `RowCommand` обработчик событий, то мы будете перенаправлены на второй — на последней странице (последний индекс страницы перед добавлением нового продукта) в отличие от новых последней странице i индекса. Так как `DataBound` обработчик событий вызывается после добавления нового продукта и данные повторно привязываются к сетке, задав `PageIndex` существует свойство мы знаем, нам удалось извлечь нужный индекс последней страницы.

Наконец GridView, используемый в этом руководстве широким из-за количества полей, которые должны собираться для добавления нового продукта. Из-за этого ширины DetailsView s вертикальный макет может быть предпочтительнее. GridView s общая ширина могла быть уменьшена путем сбора меньшее количество входных данных. Возможно, мы кое t необходимость сбора `UnitsOnOrder`, `UnitsInStock`, и `ReorderLevel` полей при добавлении нового продукта, в таком случае эти поля может быть удален из элемента GridView.

Чтобы настроить данные, собранные, можно использовать один из двух подходов:

- Продолжать использовать `AddProduct` метод, который ожидает, что значения для `UnitsOnOrder`, `UnitsInStock`, и `ReorderLevel` поля. В `Inserting` обработчик событий, предоставляют жестко, по умолчанию значения для этих входных данных, которые были удалены из интерфейса вставки.
- Создание новой перегрузкой `AddProduct` метод в `ProductsBLL` класс, который не принимает входные данные для `UnitsOnOrder`, `UnitsInStock`, и `ReorderLevel` поля. Затем на странице ASP.NET, настройте ObjectDataSource на использование этой новой перегрузке.

Оба варианта также будет работать одинаково. В предыдущих руководствах мы использовали последний вариант создания нескольких перегрузок для `ProductsBLL` класс s `UpdateProduct` метод.

## <a name="summary"></a>Сводка

GridView не имеет встроенные возможности вставки, найденных в DetailsView и FormView, но немного усилий интерфейс для вставки могут добавляться к строке нижнего колонтитула. Для отображения строки нижнего колонтитула в элементе управления GridView, просто задайте его `ShowFooter` свойства `True`. Содержимое строки нижнего колонтитула можно настроить для каждого поля путем преобразования поле в TemplateField и добавление вставку интерфейс `FooterTemplate`. Как мы видели в этом руководстве `FooterTemplate` может содержать кнопки, текстовые поля, элементов управления DropDownList, флажки, элементов управления источниками данных для заполнения управляемых данными веб-элементов управления (например, элементов управления DropDownList) и элементов управления проверки. Вместе с элементами управления для сбора входных данных пользователя s требуется добавить кнопку LinkButton и ImageButton.

При нажатии кнопки Добавить элемент управления ObjectDataSource s `Insert()` метод вызывается для запуска операций по вставке. ObjectDataSource затем вызывает метод вставки настроенного ( `ProductsBLL` класс s `AddProduct` метод, в этом руководстве). Нам необходимо скопировать значения из s GridView, интерфейсам, чтобы элемент управления ObjectDataSource s `InsertParameters` коллекции перед вызываемого метода insert. Это можно сделать с программного обращения вставки интерфейса веб-элементы управления ObjectDataSource s `Inserting` обработчик событий.

Этот учебник завершает наш Рассмотрение методов улучшения внешнего s GridView. Следующий набор учебных курсов будет проверять, как работать с двоичными данными, таких как изображения, PDF-файлы, документы Word и т. д и данные веб-элементов управления.

Счастливого вам программирования!

## <a name="about-the-author"></a>Об авторе

[Скотт Митчелл](http://www.4guysfromrolla.com/ScottMitchell.shtml), автор семи книг по ASP/ASP.NET и основатель веб- [4GuysFromRolla.com](http://www.4guysfromrolla.com), работает с веб-технологиями Microsoft с 1998 года. Скотт — независимый консультант, преподаватель и автор. Его последняя книга — [ *Sams Teach ASP.NET 2.0 in 24 часа*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco). Ним можно связаться по адресу [ mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) или через его блог, который можно найти в [ http://ScottOnWriting.NET ](http://ScottOnWriting.NET).

## <a name="special-thanks-to"></a>Особая благодарность

В этой серии руководств пособий рецензировалась многими компетентными редакторами. Основной рецензент этого учебного был Екатерина Leigh. Хотите поработать с моих последующих статей для MSDN? Если Да, напишите мне [ mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Назад](adding-a-gridview-column-of-checkboxes-vb.md)