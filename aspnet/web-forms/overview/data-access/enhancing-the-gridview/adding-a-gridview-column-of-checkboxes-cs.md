---
uid: web-forms/overview/data-access/enhancing-the-gridview/adding-a-gridview-column-of-checkboxes-cs
title: Добавление столбца GridView для флажков (C#) | Документация Майкрософт
author: rick-anderson
description: В этом учебнике рассматривается добавление столбца флажков к элементу управления GridView для предоставления пользователю интуитивно понятного способа выбора нескольких строк в G...
ms.author: riande
ms.date: 03/06/2007
ms.assetid: f63a9443-2db0-4f80-8246-840d3e86c2a3
msc.legacyurl: /web-forms/overview/data-access/enhancing-the-gridview/adding-a-gridview-column-of-checkboxes-cs
msc.type: authoredcontent
ms.openlocfilehash: b9d1ed50e8d88202c3286b4cd0e9ebf111dfbe21
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78478272"
---
# <a name="adding-a-gridview-column-of-checkboxes-c"></a>Добавление столбца GridView флажков (C#)

по [Скотт Митчелл](https://twitter.com/ScottOnWriting)

[Скачивание примера приложения](https://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_52_CS.exe) или [Загрузка PDF-файла](adding-a-gridview-column-of-checkboxes-cs/_static/datatutorial52cs1.pdf)

> В этом учебнике рассматривается добавление столбца флажков к элементу управления GridView для предоставления пользователю интуитивно понятного способа выбора нескольких строк GridView.

## <a name="introduction"></a>Введение

В предыдущем учебном курсе мы рассмотрели добавление столбца переключателей в GridView для выбора конкретной записи. Столбец переключателей является подходящим пользовательским интерфейсом, когда пользователь ограничивает выбор только одного элемента из сетки. Однако иногда может потребоваться разрешить пользователю выбирать произвольное количество элементов из сетки. Веб-клиенты электронной почты, например, обычно отображают список сообщений со столбцом флажков. Пользователь может выбрать произвольное число сообщений и выполнить некоторые действия, например переместить сообщения электронной почты в другую папку или удалить их.

В этом учебнике будет показано, как добавить столбец флажков и определить, какие флажки были проверены при обратной передаче. В частности, мы создадим пример, который точно имитирует пользовательский веб-интерфейс почтового клиента. В нашем примере будет содержаться страница GridView со списком продуктов в таблице базы данных `Products` с флажком в каждой строке (см. рис. 1). При нажатии кнопки Удалить выбранные продукты будут удалены выбранные продукты.

[![каждая строка продукта содержит флажок](adding-a-gridview-column-of-checkboxes-cs/_static/image1.gif)](adding-a-gridview-column-of-checkboxes-cs/_static/image1.png)

**Рис. 1**. Каждая строка продукта содержит флажок ([щелкните, чтобы просмотреть изображение с полным размером](adding-a-gridview-column-of-checkboxes-cs/_static/image2.png))

## <a name="step-1-adding-a-paged-gridview-that-lists-product-information"></a>Шаг 1. Добавление страничного GridView со списком сведений о продукте

Прежде чем беспокоиться о добавлении столбца флажков, давайте рассмотрим список продуктов в элементе управления GridView, который поддерживает разбиение на страницы. Для начала откройте страницу `CheckBoxField.aspx` в папке `EnhancedGridView` и перетащите элемент GridView с панели элементов в конструктор, установив для его `ID` значение `Products`. Затем выберите привязку GridView к новому элементу ObjectDataSource с именем `ProductsDataSource`. Настройте ObjectDataSource для использования класса `ProductsBLL`, вызвав метод `GetProducts()` для возврата данных. Поскольку этот элемент GridView будет доступен только для чтения, установите в раскрывающихся списках на вкладках обновление, вставка и удаление значение (нет).

[![создать новый элемент управления ObjectDataSource с именем Продуктсдатасаурце](adding-a-gridview-column-of-checkboxes-cs/_static/image2.gif)](adding-a-gridview-column-of-checkboxes-cs/_static/image3.png)

**Рис. 2**. Создание нового элемента управления ObjectDataSource с именем `ProductsDataSource` ([щелкните, чтобы просмотреть изображение с полным размером](adding-a-gridview-column-of-checkboxes-cs/_static/image4.png))

[![настроить ObjectDataSource для получения данных с помощью метода Products ()](adding-a-gridview-column-of-checkboxes-cs/_static/image3.gif)](adding-a-gridview-column-of-checkboxes-cs/_static/image5.png)

**Рис. 3**. Настройка ObjectDataSource для получения данных с помощью метода `GetProducts()` ([щелкните, чтобы просмотреть изображение с полным размером](adding-a-gridview-column-of-checkboxes-cs/_static/image6.png))

[![установить в раскрывающихся списках на вкладках обновления, вставки и удаления значение (нет)](adding-a-gridview-column-of-checkboxes-cs/_static/image4.gif)](adding-a-gridview-column-of-checkboxes-cs/_static/image7.png)

**Рис. 4**. Установка раскрывающихся списков на вкладках обновления, вставки и удаления в (нет) ([щелкните, чтобы просмотреть изображение с полным размером](adding-a-gridview-column-of-checkboxes-cs/_static/image8.png))

После завершения работы мастера настройки источника данных Visual Studio автоматически создаст Баундколумнс и Чеккбоксколумн для полей данных, связанных с продуктом. Как и в предыдущем руководстве, удалите все, кроме `ProductName`, `CategoryName`и `UnitPrice` BoundFields, а также измените свойства `HeaderText` на "продукт", "Категория" и "цена". Настройте `UnitPrice` BoundField, чтобы его значение было отформатировано как денежная единица. Также настройте GridView для поддержки разбиения на страницы, установив флажок Включить разбиение по страницам в смарт-теге.

Также добавим пользовательский интерфейс для удаления выбранных продуктов. Добавьте элемент управления "Кнопка" под элементом GridView, установив для его `ID` значение `DeleteSelectedProducts` и его свойство `Text`, чтобы удалить выбранные продукты. Вместо фактического удаления продуктов из базы данных в этом примере будет просто отображено сообщение с информацией о продуктах, которые были бы удалены. Для этого добавьте элемент управления Label под кнопкой. Задайте для его идентификатора значение `DeleteResults`, очистите свойство `Text` и задайте для его свойства `Visible` и `EnableViewState` значение `false`.

После внесения этих изменений декларативная разметка GridView, ObjectDataSource, Button и Label должна выглядеть следующим образом:

[!code-aspx[Main](adding-a-gridview-column-of-checkboxes-cs/samples/sample1.aspx)]

Уделите время просмотру страницы в браузере (см. рис. 5). На этом этапе вы увидите имя, категорию и цену первых десяти продуктов.

[![указаны имя, Категория и цена первых десяти продуктов](adding-a-gridview-column-of-checkboxes-cs/_static/image5.gif)](adding-a-gridview-column-of-checkboxes-cs/_static/image9.png)

**Рис. 5**. список названий, категорий и цен первых десяти продуктов ([щелкните, чтобы просмотреть изображение с полным размером](adding-a-gridview-column-of-checkboxes-cs/_static/image10.png))

## <a name="step-2-adding-a-column-of-checkboxes"></a>Шаг 2. Добавление столбца флажков

Поскольку ASP.NET 2,0 включает CheckBoxField, можно предположить, что он может использоваться для добавления столбца флажков в GridView. К сожалению, это не так, так как CheckBoxField предназначен для работы с логическими полями данных. То есть, чтобы использовать CheckBoxField, необходимо указать базовое поле данных, к значению которого обращается, чтобы определить, установлен ли флажок для визуализации. Мы не можем использовать CheckBoxField, чтобы просто включить столбец непроверенных флажков.

Вместо этого необходимо добавить TemplateField и добавить в его `ItemTemplate`веб-элемент управления CheckBox. Добавьте TemplateField в `Products` GridView и сделайте его первым (крайним левым) полем. Из смарт-тега GridView s щелкните ссылку Edit Templates (изменить шаблоны), а затем перетащите элемент управления CheckBox из панели элементов в `ItemTemplate`. Установите этот флажок s `ID` для свойства `ProductSelector`.

[![добавить веб-элемент управления CheckBox с именем Продуктселектор в TemplateField s ItemTemplate](adding-a-gridview-column-of-checkboxes-cs/_static/image6.gif)](adding-a-gridview-column-of-checkboxes-cs/_static/image11.png)

**Рис. 6**. Добавление веб-элемента управления CheckBox с именем `ProductSelector` в `ItemTemplate` TemplateField s ([щелкните, чтобы просмотреть изображение с полным размером](adding-a-gridview-column-of-checkboxes-cs/_static/image12.png))

После добавления TemplateField и веб-элемента управления CheckBox каждая строка включает флажок. На рис. 7 показана эта страница при просмотре в браузере после добавления TemplateField и CheckBox.

[![каждая строка продуктов теперь содержит флажок](adding-a-gridview-column-of-checkboxes-cs/_static/image7.gif)](adding-a-gridview-column-of-checkboxes-cs/_static/image13.png)

**Рис. 7**. Теперь каждая строка продукта содержит флажок ([щелкните, чтобы просмотреть изображение с полным размером](adding-a-gridview-column-of-checkboxes-cs/_static/image14.png)).

## <a name="step-3-determining-what-checkboxes-were-checked-on-postback"></a>Шаг 3. Определение флажков, которые были проверены при обратной передаче

На этом этапе у нас есть столбец флажков, но нет способа определить, какие флажки были проверены при обратной передаче. Однако при нажатии кнопки Удалить выбранные продукты необходимо знать, какие флажки были проверены, чтобы удалить эти продукты.

[Свойство`Rows`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.rows.aspx) GridView s предоставляет доступ к строкам данных в GridView. Можно выполнить итерацию по этим строкам, программно получить доступ к элементу управления CheckBox, а затем обратиться к свойству `Checked`, чтобы определить, выбран ли флажок.

Создайте обработчик событий для `Click` события `DeleteSelectedProducts` Web Control Button и добавьте следующий код:

[!code-csharp[Main](adding-a-gridview-column-of-checkboxes-cs/samples/sample2.cs)]

Свойство `Rows` Возвращает коллекцию экземпляров `GridViewRow`, описывающего строки данных GridView s. В этом цикле `foreach` перечисление этой коллекции. Для каждого `GridViewRow` объекта флажок Row s программным способом обращается с помощью `row.FindControl("controlID")`. Если флажок установлен, то строка s, соответствующая `ProductID` значение, извлекается из коллекции `DataKeys`. В этом упражнении мы просто отображаем информативное сообщение в метке `DeleteResults`, хотя в работающем приложении вместо этого выполняется вызов метода `ProductsBLL` класса s `DeleteProduct(productID)`.

После добавления этого обработчика событий после нажатия кнопки Удалить выбранные продукты отображается `ProductID` s выбранных продуктов.

[![при нажатии кнопки Удалить выбранные продукты отображаются продукты ProductID.](adding-a-gridview-column-of-checkboxes-cs/_static/image8.gif)](adding-a-gridview-column-of-checkboxes-cs/_static/image15.png)

**Рис. 8**. при нажатии кнопки Удалить выбранные продукты отображаются выбранные продукты `ProductID` s ([щелкните, чтобы просмотреть изображение с полным размером](adding-a-gridview-column-of-checkboxes-cs/_static/image16.png)).

## <a name="step-4-adding-check-all-and-uncheck-all-buttons"></a>Шаг 4. Добавление кнопок "проверить все" и "снять все"

Если пользователь хочет удалить все продукты на текущей странице, он должен проверить каждый из десяти флажков. Мы можем помочь ускорить этот процесс, добавив кнопку Проверить все, которая при нажатии устанавливает все флажки в сетке. Кнопка снять все будет так же полезной.

Добавьте на страницу два веб-элемента управления Button, поместив их над GridView. Установите первый `ID` s в `CheckAll` и его свойство `Text`, чтобы проверить все. Задайте для второго `ID` s значение `UncheckAll` и его свойство `Text`, чтобы снять все флажки.

[!code-aspx[Main](adding-a-gridview-column-of-checkboxes-cs/samples/sample3.aspx)]

Затем создайте метод в классе кода программной части с именем `ToggleCheckState(checkState)`, который при вызове перечисляет коллекцию `Products` GridView s `Rows` коллекции и устанавливает для каждого свойства CheckBox `Checked` значение переданного параметра *свойство CheckState* .

[!code-csharp[Main](adding-a-gridview-column-of-checkboxes-cs/samples/sample4.cs)]

Затем создайте `Click` обработчики событий для кнопок `CheckAll` и `UncheckAll`. В обработчике событий `CheckAll` s просто вызовите `ToggleCheckState(true)`. в `UncheckAll`вызовите `ToggleCheckState(false)`.

[!code-csharp[Main](adding-a-gridview-column-of-checkboxes-cs/samples/sample5.cs)]

С помощью этого кода нажатие кнопки Проверить все вызывает обратную передачу и проверяет все флажки в GridView. Аналогичным образом, установив флажок снять все флажки отменить все. На рис. 9 показан экран после проверки кнопки Проверить все.

[![нажатии кнопки "проверить все", выбирают все флажки](adding-a-gridview-column-of-checkboxes-cs/_static/image9.gif)](adding-a-gridview-column-of-checkboxes-cs/_static/image17.png)

**Рис. 9**. нажатие кнопки "проверить все" устанавливает все флажки ([щелкните, чтобы просмотреть изображение с полным размером](adding-a-gridview-column-of-checkboxes-cs/_static/image18.png))

> [!NOTE]
> При отображении столбца флажков одним из подходов к выбору или снятию флажков является наличие флажка в строке заголовка. Более того, для текущей реализации проверки все или снять все требуется обратная передача. Все флажки можно установить или снять, но полностью с помощью клиентского сценария, тем самым обеспечивая шустрее взаимодействие с пользователем. Чтобы узнать больше об использовании флажка строки заголовка для получения подробных сведений о всех возможностях и подробном рассмотрении использования методов на стороне клиента, изучите флажок Проверять [все флажки в GridView с помощью клиентского скрипта и флажка проверить все](http://aspnet.4guysfromrolla.com/articles/053106-1.aspx).

## <a name="summary"></a>Сводка

В случаях, когда необходимо разрешить пользователям выбирать произвольное число строк из элемента управления GridView перед продолжением, Добавление столбца флажков является одним из вариантов. Как мы видели в этом учебнике, включая столбец флажков в GridView, добавляет TemplateField с веб-элементом управления CheckBox. С помощью веб-элемента управления (по сравнению с внедрением разметки непосредственно в шаблон, как мы делали в предыдущем учебном курсе) ASP.NET автоматически запоминает, какие флажки были и не проверялись в обратной передаче. Можно также программно получить доступ к флажкам в коде, чтобы определить, установлен ли данный флажок, или изменить состояние проверки.

Это руководство и Последнее из них рассмотрели добавление столбца селектора строк в GridView. В следующем учебном курсе мы рассмотрим, как с небольшой работой мы можем добавить возможности вставки в GridView.

Поздравляем с программированием!

## <a name="about-the-author"></a>Об авторе

[Скотт Митчелл](http://www.4guysfromrolla.com/ScottMitchell.shtml), автор семи книг по ASP/ASP. NET и основатель [4GuysFromRolla.com](http://www.4guysfromrolla.com), работал с веб-технологиями Майкрософт с 1998. Скотт работает как независимый консультант, преподаватель и модуль записи. Его последняя книга — [*Sams обучать себя ASP.NET 2,0 за 24 часа*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco). Он доступен по адресу [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) или через его блог, который можно найти по адресу [http://ScottOnWriting.NET](http://ScottOnWriting.NET).

> [!div class="step-by-step"]
> [Назад](adding-a-gridview-column-of-radio-buttons-cs.md)
> [Вперед](inserting-a-new-record-from-the-gridview-s-footer-cs.md)
