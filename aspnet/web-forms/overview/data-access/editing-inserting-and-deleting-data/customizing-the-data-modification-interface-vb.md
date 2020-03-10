---
uid: web-forms/overview/data-access/editing-inserting-and-deleting-data/customizing-the-data-modification-interface-vb
title: Настройка интерфейса изменения данных (VB) | Документация Майкрософт
author: rick-anderson
description: В этом учебнике мы рассмотрим, как настроить интерфейс редактируемого элемента управления GridView, заменив стандартные поля TextBox и CheckBox на алтернати...
ms.author: riande
ms.date: 07/17/2006
ms.assetid: 4830d984-bd2c-4a08-bfe5-2385599f1f7d
msc.legacyurl: /web-forms/overview/data-access/editing-inserting-and-deleting-data/customizing-the-data-modification-interface-vb
msc.type: authoredcontent
ms.openlocfilehash: 85ec7bdde6b2bffbbda066b0441bbd36b7072197
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78479256"
---
# <a name="customizing-the-data-modification-interface-vb"></a>Настройка интерфейса изменения данных (VB)

по [Скотт Митчелл](https://twitter.com/ScottOnWriting)

[Скачивание примера приложения](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_20_VB.exe) или [Загрузка PDF-файла](customizing-the-data-modification-interface-vb/_static/datatutorial20vb1.pdf)

> В этом учебнике мы рассмотрим, как настроить интерфейс редактируемого элемента управления GridView, заменив стандартные поля TextBox и CheckBox на альтернативные веб-элементы управления вводом.

## <a name="introduction"></a>Введение

BoundFields и Чеккбоксфиелдс, используемые элементами управления GridView и DetailsView, упрощают процесс изменения данных из-за возможности отображения интерфейсов, поддерживающих только чтение, редактируемых и вставляемых. Эти интерфейсы могут быть подготовлены к просмотру без необходимости добавлять дополнительную декларативную разметку или код. Однако у интерфейсов BoundField и CheckBoxField нет возможности настраивать, часто требуется в реальных сценариях. Чтобы настроить редактируемый или вставляемый интерфейс в GridView или DetailsView, необходимо вместо этого использовать TemplateField.

В [предыдущем учебном курсе](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb.md) мы увидели, как настраивать интерфейсы изменения данных, добавляя веб-элементы проверки. В этом учебнике мы рассмотрим, как настроить фактические веб-элементы управления сбором данных, заменив стандартные элементы управления TextBox и CheckBox BoundField и CheckBoxField на альтернативные веб-элементы управления вводом. В частности, мы создадим редактируемый элемент управления GridView, который позволяет обновлять название продукта, категорию, поставщика и состояние "снято с производства". При редактировании определенной строки поля категории и поставщика будут отображаться как элементов управления DropDownList, содержащие набор доступных категорий и поставщиков для выбора. Кроме того, будет заменен флажок CheckBoxField по умолчанию на элемент управления RadioButtonList, предлагающий два варианта: "Active" и "снят с работы".

[![интерфейс редактирования GridView включает элементов управления DropDownList и RadioButton.](customizing-the-data-modification-interface-vb/_static/image2.png)](customizing-the-data-modification-interface-vb/_static/image1.png)

**Рис. 1**. интерфейс редактирования GridView включает элементов управления DropDownList и RadioButton ([щелкните, чтобы просмотреть изображение с полным размером](customizing-the-data-modification-interface-vb/_static/image3.png)).

## <a name="step-1-creating-the-appropriateupdateproductoverload"></a>Шаг 1. создание соответствующей перегрузки`UpdateProduct`

В этом учебнике мы создадим редактируемый элемент управления GridView, который позволяет изменять название продукта, категорию, поставщика и состояние "снято с производства". Поэтому требуется перегрузка `UpdateProduct`, которая принимает пять входных параметров, состоящий из четырех значений продуктов и `ProductID`. Как и в предыдущих перегрузках, это будет следующим:

1. Получение сведений о продукте из базы данных для указанного `ProductID`
2. Обновите поля `ProductName`, `CategoryID`, `SupplierID`и `Discontinued`, а также
3. Отправьте запрос на обновление DAL с помощью метода `Update()` TableAdapter.

Для краткости, для этой конкретной перегрузки я пропустил проверку бизнес-правил, которая гарантирует, что продукт, помеченный как снятый, не является единственным продуктом, предоставляемым его поставщиком. Вы можете добавить его в, если предпочитаете, или, в идеале, выполнить рефакторинг логики для отдельного метода.

В следующем коде показана новая перегрузка `UpdateProduct` в классе `ProductsBLL`:

[!code-vb[Main](customizing-the-data-modification-interface-vb/samples/sample1.vb)]

## <a name="step-2-crafting-the-editable-gridview"></a>Шаг 2. Создание редактируемого элемента управления GridView

После добавления перегрузки `UpdateProduct` мы готовы к созданию редактируемого элемента управления GridView. Откройте страницу `CustomizedUI.aspx` в папке `EditInsertDelete` и добавьте в конструктор элемент управления GridView. Затем создайте новый элемент ObjectDataSource из смарт-тега GridView. Настройте ObjectDataSource для получения сведений о продукте с помощью метода `GetProducts()` класса `ProductBLL` и для обновления данных продукта с помощью только что созданной перегрузки `UpdateProduct`. На вкладках Вставка и удаление выберите (нет) в раскрывающихся списках.

[![настроить ObjectDataSource для использования только что созданной перегрузки UpdateProduct](customizing-the-data-modification-interface-vb/_static/image5.png)](customizing-the-data-modification-interface-vb/_static/image4.png)

**Рис. 2**. Настройка ObjectDataSource для использования только что созданной перегрузки `UpdateProduct` ([щелкните, чтобы просмотреть изображение с полным размером](customizing-the-data-modification-interface-vb/_static/image6.png))

Как мы видели в руководствах по изменению данных, декларативный синтаксис элемента ObjectDataSource, созданного Visual Studio, присваивает свойству `OldValuesParameterFormatString` значение `original_{0}`. Это, само собой, не будет работать с уровнем бизнес-логики, так как наши методы не предполагают, что исходное значение `ProductID` передается. Поэтому, как мы сделали в предыдущих учебных курсах, нужно удалить это назначение свойства из декларативного синтаксиса или, вместо этого, присвоить этому свойству значение `{0}`.

После этого изменения декларативная разметка ObjectDataSource должна выглядеть следующим образом:

[!code-aspx[Main](customizing-the-data-modification-interface-vb/samples/sample2.aspx)]

Обратите внимание, что свойство `OldValuesParameterFormatString` было удалено и в коллекции `UpdateParameters` есть `Parameter` для каждого входного параметра, ожидаемого нашей перегрузкой `UpdateProduct`.

Хотя элемент управления ObjectDataSource настроен для обновления только подмножества значений продукта, GridView в настоящее время отображает *все* поля продукта. Уделите немного времени, чтобы изменить GridView таким образом, чтобы:

- Он включает только `ProductName`, `SupplierName`, `CategoryName` BoundFields и `Discontinued` CheckBoxField
- Поля `CategoryName` и `SupplierName`, которые будут отображаться до (слева от) `Discontinued` CheckBoxField
- Свойство `HeaderText` `CategoryName` и `SupplierName` BoundFields имеет значение "Category" и "поставщик" соответственно
- Поддержка редактирования включена (установите флажок Включить редактирование в смарт-теге GridView).

После этих изменений конструктор будет выглядеть примерно так, как показано на рис. 3, с помощью декларативного синтаксиса GridView, показанного ниже.

[![удалить ненужные поля из GridView](customizing-the-data-modification-interface-vb/_static/image8.png)](customizing-the-data-modification-interface-vb/_static/image7.png)

**Рис. 3**. Удаление ненужных полей из GridView ([щелкните, чтобы просмотреть изображение с полным размером](customizing-the-data-modification-interface-vb/_static/image9.png))

[!code-aspx[Main](customizing-the-data-modification-interface-vb/samples/sample3.aspx)]

На этом этапе поведение GridView только для чтения завершено. При просмотре данных каждый продукт подготавливается к просмотру в виде строки в GridView с указанием названия продукта, категории, поставщика и состояния "снято с производства".

[![интерфейс только для чтения GridView завершен](customizing-the-data-modification-interface-vb/_static/image11.png)](customizing-the-data-modification-interface-vb/_static/image10.png)

**Рис. 4**. интерфейс только для чтения GridView завершен ([щелкните, чтобы просмотреть изображение с полным размером](customizing-the-data-modification-interface-vb/_static/image12.png))

> [!NOTE]
> Как обсуждалось в [обзоре руководства по вставке, обновлению и удалению данных](an-overview-of-inserting-updating-and-deleting-data-cs.md), крайне важно, чтобы состояние представления GridView s было включено (поведение по умолчанию). Если для свойства `EnableViewState` GridView s задано значение `false`, возникает риск непреднамеренного удаления или изменения записей одновременно выполняющимися пользователями. См. [Предупреждение: ошибка параллелизма с ASP.NET 2,0 gridviews/DetailsView/FormView, которые поддерживают редактирование и (или) удаление, а состояние представления — "отключено](http://scottonwriting.net/sowblog/posts/10054.aspx) " для получения дополнительных сведений.

## <a name="step-3-using-a-dropdownlist-for-the-category-and-supplier-editing-interfaces"></a>Шаг 3. Использование DropDownList для интерфейсов изменения категории и поставщика

Помните, что объект `ProductsRow` содержит свойства `CategoryID`, `CategoryName`, `SupplierID`и `SupplierName`, которые предоставляют фактические значения идентификатора внешнего ключа в таблице `Products` базы данных и соответствующие значения `Name` в таблицах `Categories` и `Suppliers`. `CategoryID` и `SupplierID` `ProductRow`могут быть считаны и записаны в, тогда как свойства `CategoryName` и `SupplierName` помечаются как доступные только для чтения.

Из-за состояния только для чтения свойств `CategoryName` и `SupplierName` для соответствующего BoundFields свойству `ReadOnly` задано значение `True`, что предотвращает изменение этих значений при редактировании строки. Хотя можно задать свойство `ReadOnly` для `False`, отрисовку `CategoryName` и `SupplierName` BoundFields как текстовых полей во время редактирования, такой подход приведет к возникновению исключения, когда пользователь пытается обновить продукт, поскольку не существует `UpdateProduct` перегрузок, использующих `CategoryName` и `SupplierName` входные данные. На самом деле мы не хотим создавать такую перегрузку по двум причинам:

- `Products` таблица не содержит `SupplierName` или `CategoryName` поля, но `SupplierID` и `CategoryID`. Поэтому мы хотим, чтобы наш метод передал эти значения ИДЕНТИФИКАТОРов, а не значения таблиц подстановки.
- Требование ввода имени поставщика или категории является менее идеальным, так как оно требует, чтобы пользователь знал о доступных категориях и поставщиках и их правильное написание.

Поля "поставщик" и "Категория" должны отображать имена категории и поставщиков в режиме только для чтения (как и сейчас) и раскрывающийся список соответствующих параметров при редактировании. Используя раскрывающийся список, конечный пользователь может быстро увидеть, какие категории и поставщики доступны для выбора, а также легко сделать выбор.

Чтобы обеспечить такое поведение, необходимо преобразовать `SupplierName` и `CategoryName` BoundFields в полей TemplateField, чьи `ItemTemplate` выдают значения `SupplierName` и `CategoryName`, а `EditItemTemplate` использует элемент управления DropDownList для перечисления доступных категорий и поставщиков.

## <a name="adding-thecategoriesandsuppliersdropdownlists"></a>Добавление`Categories`и`Suppliers`элементов управления DropDownList

Начните с преобразования `SupplierName` и `CategoryName` BoundFields в полей TemplateField By: щелкните ссылку Edit Columns (изменить столбцы) в смарт-теге GridView. Выбор BoundField из списка в левом нижнем углу; и щелкнув ссылку "преобразовать это поле в TemplateField". В процессе преобразования создается TemplateField с `ItemTemplate` и `EditItemTemplate`, как показано в следующем декларативном синтаксисе:

[!code-aspx[Main](customizing-the-data-modification-interface-vb/samples/sample4.aspx)]

Так как BoundField был помечен как доступный только для чтения, как `ItemTemplate`, так `EditItemTemplate` содержит элемент управления Label, свойство `Text` которого привязано к соответствующему полю данных (`CategoryName`, в приведенном выше синтаксисе). Необходимо изменить `EditItemTemplate`, заменив веб-элемент управления Label на элемент управления DropDownList.

Как мы видели в предыдущих учебных курсах, шаблон можно изменить с помощью конструктора или непосредственно из декларативного синтаксиса. Чтобы изменить его в конструкторе, щелкните ссылку Edit Templates (изменить шаблоны) в смарт-теге GridView и выберите вариант работы с `EditItemTemplate`поля категории. Удалите веб-элемент управления Label и замените его элементом управления DropDownList, установив для свойства идентификатора DropDownList значение `Categories`.

[![удалить почта и добавить DropDownList в EditItemTemplate](customizing-the-data-modification-interface-vb/_static/image14.png)](customizing-the-data-modification-interface-vb/_static/image13.png)

**Рис. 5**. Удаление почта и добавление DropDownList в `EditItemTemplate` ([щелкните, чтобы просмотреть изображение с полным размером](customizing-the-data-modification-interface-vb/_static/image15.png))

Далее необходимо заполнить DropDownList доступными категориями. Щелкните ссылку Выбор источника данных из смарт-тега DropDownList и выберите создать новый элемент ObjectDataSource с именем `CategoriesDataSource`.

[![создать новый элемент управления ObjectDataSource с именем CategoriesDataSource](customizing-the-data-modification-interface-vb/_static/image17.png)](customizing-the-data-modification-interface-vb/_static/image16.png)

**Рис. 6**. Создание нового элемента управления ObjectDataSource с именем `CategoriesDataSource` ([щелкните, чтобы просмотреть изображение с полным размером](customizing-the-data-modification-interface-vb/_static/image18.png))

Чтобы этот элемент управления ObjectDataSource возвращал все категории, привяжите его к методу `GetCategories()` класса `CategoriesBLL`.

[![привязать ObjectDataSource к методу CategoriesBLL Categories ()](customizing-the-data-modification-interface-vb/_static/image20.png)](customizing-the-data-modification-interface-vb/_static/image19.png)

**Рис. 7**. Привязка ObjectDataSource к методу `GetCategories()` `CategoriesBLL`([щелкните, чтобы просмотреть изображение с полным размером](customizing-the-data-modification-interface-vb/_static/image21.png))

Наконец, настройте параметры DropDownList таким образом, чтобы поле `CategoryName` отображалось в каждом `ListItem` DropDownList с полем `CategoryID`, используемым в качестве значения.

[![отображать поле CategoryName и значение CategoryID, используемое в качестве значения](customizing-the-data-modification-interface-vb/_static/image23.png)](customizing-the-data-modification-interface-vb/_static/image22.png)

**Рис. 8**. отображение поля `CategoryName` и `CategoryID`, используемого в качестве значения ([щелкните, чтобы просмотреть изображение с полным размером](customizing-the-data-modification-interface-vb/_static/image24.png))

После внесения этих изменений декларативная разметка для `EditItemTemplate` в `CategoryName` TemplateField будет включать DropDownList и элемент управления ObjectDataSource:

[!code-aspx[Main](customizing-the-data-modification-interface-vb/samples/sample5.aspx)]

> [!NOTE]
> Для элемента DropDownList в `EditItemTemplate` должно быть включено состояние просмотра. Вскоре мы добавим синтаксис DataBinding к декларативному синтаксису DropDownList и к командам привязки данных, таким как `Eval()` и `Bind()` могут появляться только в элементах управления, состояние представления которых — Enabled.

Повторите эти шаги, чтобы добавить элемент DropDownList с именем `Suppliers` в `EditItemTemplate``SupplierName` TemplateField. Это приведет к добавлению элемента управления DropDownList в `EditItemTemplate` и созданию другого элемента ObjectDataSource. Однако ObjectDataSource `Suppliers` DropDownList должен быть настроен на вызов метода `GetSuppliers()` класса `SuppliersBLL`. Кроме того, можно настроить `Suppliers` DropDownList для вывода поля `CompanyName` и использовать поле `SupplierID` в качестве значения для его `ListItem` s.

После добавления элементов управления DropDownList в два `EditItemTemplate`, загрузите страницу в браузере и нажмите кнопку Edit (изменить) для продукта Chef Anton's Cajun. Как показано на рис. 9, столбцы категории и поставщика продукта подготавливаются к просмотру в виде раскрывающихся списков, содержащих доступные категории и поставщики для выбора. Однако обратите внимание, что *первые* элементы в обоих раскрывающихся списках выбираются по умолчанию (напитки для категории и Exotic Liquids в качестве поставщика), хотя Chef anton's Cajun-кондимент, обеспечиваемой новыми Orleans Cajun.

[![первый элемент в раскрывающихся списках выбран по умолчанию](customizing-the-data-modification-interface-vb/_static/image26.png)](customizing-the-data-modification-interface-vb/_static/image25.png)

**Рис. 9**. первый элемент в раскрывающихся списках выбран по умолчанию (щелкните,[чтобы просмотреть изображение с полным размером](customizing-the-data-modification-interface-vb/_static/image27.png))

Кроме того, если нажать кнопку обновить, вы обнаружите, что значения `CategoryID` и `SupplierID` продукта заданы как `NULL`. Оба эти нежелательных поведения вызваны тем, что элементов управления DropDownList в `EditItemTemplate` s не привязаны к каким-либо полям данных из базовых данных продукта.

## <a name="binding-the-dropdownlists-to-thecategoryidandsupplieriddata-fields"></a>Привязка элементов управления DropDownList к полям данных`CategoryID`и`SupplierID`

Чтобы в раскрывающихся списках Категория и поставщик для отредактированного продукта были заданы соответствующие значения и эти значения отправляются обратно в метод `UpdateProduct` BLL после нажатия кнопки Обновить, необходимо привязать свойства элементов управления DropDownList ' `SelectedValue` к полям данных `CategoryID` и `SupplierID`, используя двустороннюю привязку данных. Чтобы сделать это с помощью `Categories` DropDownList, можно добавить `SelectedValue='<%# Bind("CategoryID") %>'` непосредственно в декларативный синтаксис.

Кроме того, можно задать привязки данных DropDownList, отредактировав шаблон в конструкторе и щелкнув ссылку изменить привязки данных в смарт-теге DropDownList. Затем укажите, что свойство `SelectedValue` должно быть привязано к полю `CategoryID` с помощью двухсторонней привязки данных (см. рис. 10). Повторите декларативный или конструкторный процесс, чтобы привязать `SupplierID` поле данных к `Suppliers` DropDownList.

[![привязать CategoryID к свойству SelectedValue DropDownList с помощью двухсторонней привязки данных](customizing-the-data-modification-interface-vb/_static/image29.png)](customizing-the-data-modification-interface-vb/_static/image28.png)

**Рис. 10**. Привязка `CategoryID` к свойству `SelectedValue` DropDownList с помощью двухсторонней привязки данных ([щелкните, чтобы просмотреть изображение с полным размером](customizing-the-data-modification-interface-vb/_static/image30.png))

После применения привязок к `SelectedValue` свойствам двух элементов управления DropDownList столбцы категории и поставщика отредактированного продукта будут по умолчанию использовать значения текущего продукта. После нажатия кнопки Обновить значения `CategoryID` и `SupplierID` выбранного элемента раскрывающегося списка будут переданы в метод `UpdateProduct`. На рис. 11 показано руководство после добавления инструкций DataBinding. Обратите внимание, что выбранные элементы раскрывающегося списка для Cajun Chef Anton's правильно Кондимент и новые Orleans Cajun-падения.

[![значения текущей категории и поставщика измененного продукта выбираются по умолчанию.](customizing-the-data-modification-interface-vb/_static/image32.png)](customizing-the-data-modification-interface-vb/_static/image31.png)

**Рис. 11**. значения текущей категории и поставщика измененного продукта выбираются по умолчанию ([щелкните, чтобы просмотреть изображение с полным размером](customizing-the-data-modification-interface-vb/_static/image33.png))

## <a name="handlingnullvalues"></a>Обработка значений`NULL`

Столбцы `CategoryID` и `SupplierID` в таблице `Products` могут быть `NULL`, но элементов управления DropDownList в `EditItemTemplate` s не содержат элемент списка для представления `NULL` значения. Это имеет два последствия.

- Пользователь не может использовать наш интерфейс для изменения категории или поставщика продукта со значения, отличного от`NULL`, на `NULL` один
- Если у продукта есть `NULL` `CategoryID` или `SupplierID`, то нажатие кнопки изменить приведет к возникновению исключения. Это связано с тем, что значение `NULL`, возвращаемое `CategoryID` (или `SupplierID`) в инструкции `Bind()`, не сопоставляется со значением в DropDownList (элемент DropDownList создает исключение, если его свойство `SelectedValue` имеет значение, *не* начисленное в коллекции элементов списка).

Чтобы обеспечить поддержку `NULL` `CategoryID` и `SupplierID` значений, необходимо добавить еще один `ListItem` в каждый элемент DropDownList, чтобы представить значение `NULL`. В области [фильтрации "основной/подробности" с помощью DropDownList](../masterdetail/master-detail-filtering-with-a-dropdownlist-cs.md) мы увидели, как добавить дополнительный `ListItem` к DropDownList с привязкой к данным, который включал установку свойства `AppendDataBoundItems` DropDownList в `True` и добавление дополнительных `ListItem`вручную. Однако в предыдущем руководстве мы добавили `ListItem` с `Value` `-1`. Тем не менее, логика привязки данных в ASP.NET автоматически преобразует пустую строку в `NULL` значение и наоборот. Таким образом, в этом руководстве мы хотим, чтобы `Value` `ListItem`быть пустой строкой.

Сначала установите для свойства элементов управления DropDownList `AppendDataBoundItems` значение `True`. Затем добавьте `NULL` `ListItem`, добавив следующий элемент `<asp:ListItem>` в каждый DropDownList, чтобы декларативная разметка была похожа на следующую:

[!code-aspx[Main](customizing-the-data-modification-interface-vb/samples/sample6.aspx)]

Я решил использовать "(нет)" в качестве текстового значения для этого `ListItem`, но при желании вы можете изменить его на пустую строку.

> [!NOTE]
> Как мы видели в *фильтрации "основной/подробности" с помощью DropDownList* , `ListItem` s можно добавить в элемент DropDownList в конструкторе, щелкнув свойство `Items` DropDownList в окно свойств (которое будет отображать редактор коллекции `ListItem`). Однако не забудьте добавить `NULL` `ListItem` для этого руководства с помощью декларативного синтаксиса. При использовании редактора коллекции `ListItem` созданный декларативный синтаксис будет полностью опускать параметр `Value` при присвоении пустой строки, создавая декларативную разметку, например: `<asp:ListItem>(None)</asp:ListItem>`. Хотя это может показаться небезопасным, значение Missing заставляет элемент DropDownList использовать значение свойства `Text`. Это означает, что если выбран этот `NULL` `ListItem`, будет предпринята попытка назначить значение "(нет)" `CategoryID`, что приведет к возникновению исключения. При явном задании `Value=""`значение `NULL` будет назначено `CategoryID` при выборе `NULL` `ListItem`.

Повторите эти действия для DropDownList поставщиков.

С помощью этого дополнительного `ListItem`интерфейс редактирования теперь может назначать значения `NULL` полям `CategoryID` и `SupplierID` продукта, как показано на рис. 12.

[![выбрать (нет), чтобы назначить значение NULL для категории или поставщика продукта](customizing-the-data-modification-interface-vb/_static/image35.png)](customizing-the-data-modification-interface-vb/_static/image34.png)

**Рис. 12**. Выберите (нет), чтобы назначить значение `NULL` для категории или поставщика продукта ([щелкните, чтобы просмотреть изображение с полным размером](customizing-the-data-modification-interface-vb/_static/image36.png))

## <a name="step-4-using-radiobuttons-for-the-discontinued-status"></a>Шаг 4. Использование переключателей для неподдерживаемого состояния

В настоящее время поле данных "`Discontinued` продуктов" выражается с помощью CheckBoxField, который отображает отключенный флажок для строк только для чтения и флажок Enabled для редактируемой строки. Хотя этот пользовательский интерфейс часто подходит, при необходимости его можно настроить с помощью TemplateField. В этом руководстве мы изменим CheckBoxField на TemplateField, который использует элемент управления RadioButtonList с двумя параметрами "Active" и "снят с производства", с которых пользователь может указать значение `Discontinued` продукта.

Начните с преобразования `Discontinued` CheckBoxField в TemplateField, который создаст TemplateField с `ItemTemplate` и `EditItemTemplate`. Оба шаблона включают флажок со свойством `Checked`, привязанным к полю данных `Discontinued`, единственное различие между ними заключается в том, что свойство `Enabled` `ItemTemplate`CheckBox имеет значение `False`.

Замените флажок в `ItemTemplate` и `EditItemTemplate` с помощью элемента управления RadioButtonList, установив для свойств "`ID` RadioButtonList" значение `DiscontinuedChoice`. Затем укажите, что RadioButtonList должны содержать два переключателя: один с меткой "активный" со значением "false" и один с меткой "снят с учета" со значением "true". Для этого можно либо ввести элементы `<asp:ListItem>` непосредственно через декларативный синтаксис, либо использовать редактор коллекции `ListItem` из конструктора. На рис. 13 показан редактор коллекции `ListItem` после указания двух параметров переключателя.

[![Добавление активных и неподдерживаемых параметров в RadioButtonList](customizing-the-data-modification-interface-vb/_static/image38.png)](customizing-the-data-modification-interface-vb/_static/image37.png)

**Рис. 13**. Добавление активных и неподдерживаемых параметров в RadioButtonList ([щелкните, чтобы просмотреть изображение с полным размером](customizing-the-data-modification-interface-vb/_static/image39.png))

Поскольку RadioButtonList в `ItemTemplate` не должен быть изменяемым, установите для свойства `Enabled` значение `False`, а для свойства `Enabled` — значение `True` (значение по умолчанию) для RadioButtonList в `EditItemTemplate`. При этом переключатели в нередактируемой строке будут доступны только для чтения, но пользователи смогут изменять значения RadioButton для редактируемой строки.

Нам по-прежнему нужно назначить свойства `SelectedValue` элементов управления RadioButtonList, чтобы в зависимости от поля данных этого `Discontinued` продукта был выбран соответствующий переключатель. Как и в элементов управления DropDownList, рассмотренном ранее в этом руководстве, этот синтаксис DataBinding можно добавить непосредственно в декларативную разметку или через ссылку изменить привязки данных в смарт-тегах RadioButtonList.

После добавления двух RadioButtonList и их настройки декларативная разметка `Discontinued` TemplateField должна выглядеть следующим образом:

[!code-aspx[Main](customizing-the-data-modification-interface-vb/samples/sample7.aspx)]

После внесения этих изменений столбец `Discontinued` был преобразован из списка флажков в список пар переключателей (см. рис. 14). При редактировании продукта выбирается соответствующий переключатель и состояние неподдерживаемого продукта можно обновить, выбрав другой переключатель и нажав кнопку Обновить.

[![неподдерживаемые флажки заменены парами переключателей](customizing-the-data-modification-interface-vb/_static/image41.png)](customizing-the-data-modification-interface-vb/_static/image40.png)

**Рис. 14**. снятые флажки заменены парами переключателей ([щелкните, чтобы просмотреть изображение с полным размером](customizing-the-data-modification-interface-vb/_static/image42.png))

> [!NOTE]
> Поскольку столбец `Discontinued` в базе данных `Products` не может иметь `NULL` значений, не нужно беспокоиться о записи `NULL` данных в интерфейсе. Однако, если `Discontinued` столбец может содержать `NULL` значения, нам нужно добавить третий переключатель в список, для его `Value` задана пустая строка (`Value=""`), как и в категории и элементов управления DropDownList поставщика.

## <a name="summary"></a>Сводка

Хотя BoundField и CheckBoxField автоматически визуализируют интерфейсы только для чтения, правки и вставки, у них отсутствует возможность настройки. Однако часто требуется настроить интерфейс редактирования или вставки, например, добавить элементы управления проверки (как мы видели в предыдущем руководстве) или настроить пользовательский интерфейс сбора данных (как мы видели в этом руководстве). Настройка интерфейса с помощью TemplateField может быть суммирована в следующих шагах:

1. Добавление TemplateField или преобразование существующего BoundField или CheckBoxField в TemplateField
2. Дополнение интерфейса при необходимости
3. Привязка соответствующих полей данных к вновь добавленным веб-элементам управления с помощью двухсторонней привязки данных

Помимо использования встроенных веб-элементов управления ASP.NET, можно также настроить шаблоны TemplateField с помощью пользовательских, скомпилированных серверных элементов управления и пользовательских элементов управления.

Поздравляем с программированием!

## <a name="about-the-author"></a>Об авторе

[Скотт Митчелл](http://www.4guysfromrolla.com/ScottMitchell.shtml), автор семи книг по ASP/ASP. NET и основатель [4GuysFromRolla.com](http://www.4guysfromrolla.com), работал с веб-технологиями Майкрософт с 1998. Скотт работает как независимый консультант, преподаватель и модуль записи. Его последняя книга — [*Sams обучать себя ASP.NET 2,0 за 24 часа*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco). Он доступен по адресу [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) или через его блог, который можно найти по адресу [http://ScottOnWriting.NET](http://ScottOnWriting.NET).

> [!div class="step-by-step"]
> [Назад](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb.md)
> [Вперед](implementing-optimistic-concurrency-vb.md)
