---
uid: web-forms/overview/data-access/editing-inserting-and-deleting-data/adding-validation-controls-to-the-editing-and-inserting-interfaces-vb
title: Добавление элементов управления проверки в интерфейсы правки и вставки (VB) | Документация Майкрософт
author: rick-anderson
description: В этом учебнике мы посмотрим, как легко добавить элементы управления проверки в EditItemTemplate и InsertItemTemplate веб-элемента управления данными, чтобы предоставить дополнительные сведения...
ms.author: riande
ms.date: 07/17/2006
ms.assetid: e3d7028a-7a22-4a4f-babe-d53afc41c0e2
msc.legacyurl: /web-forms/overview/data-access/editing-inserting-and-deleting-data/adding-validation-controls-to-the-editing-and-inserting-interfaces-vb
msc.type: authoredcontent
ms.openlocfilehash: 5c5ad110ee0836f0a464b02a2b29254e2e06381e
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78479436"
---
# <a name="adding-validation-controls-to-the-editing-and-inserting-interfaces-vb"></a>Добавление элементов управления проверки в интерфейсы правки и вставки (VB)

по [Скотт Митчелл](https://twitter.com/ScottOnWriting)

[Скачивание примера приложения](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_19_VB.exe) или [Загрузка PDF-файла](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/datatutorial19vb1.pdf)

> В этом учебнике мы покажем, как легко добавить элементы управления проверки в EditItemTemplate и InsertItemTemplate веб-элемента управления данными, чтобы обеспечить пользовательский интерфейс с более надежными правами.

## <a name="introduction"></a>Введение

Элементы управления GridView и DetailsView в примерах, рассмотренных в прошлых трех учебниках, состоят из BoundFields и Чеккбоксфиелдс (типы полей, автоматически добавленные Visual Studio при привязке элемента управления GridView или DetailsView к источнику данных. Управление через смарт-тег). При редактировании строки в GridView или DetailsView те BoundFields, которые не предназначены только для чтения, преобразуются в текстовые поля, из которых конечный пользователь может изменять существующие данные. Аналогичным образом при вставке новой записи в элемент управления DetailsView эти BoundFields, свойство `InsertVisible` которых имеет значение `True` (по умолчанию), отображаются как пустые текстовые поля, в которых пользователь может предоставить значения полей новой записи. Аналогичным образом, Чеккбоксфиелдс, отключенные в стандартном интерфейсе только для чтения, преобразуются в флажки Enabled в интерфейсах правки и вставки.

Хотя интерфейсы редактирования и вставки по умолчанию для BoundField и CheckBoxField могут быть полезными, интерфейс не имеет какой либо проверки. Если пользователь делает ввод данных недопущенным, например пропускает `ProductName` поле или вводит недопустимое значение для `UnitsInStock` (например,-50), в глубине архитектуры приложения будет создано исключение. Хотя это исключение может быть корректно обработано, как показано в [предыдущем руководстве](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb.md), в идеале пользовательский интерфейс редактирования или вставки будет включать элементы управления проверки, чтобы предотвратить невозможность ввода таких недопустимых данных пользователем в первую очередь.

Чтобы предоставить настраиваемый интерфейс редактирования или вставки, необходимо заменить BoundField или CheckBoxField на TemplateField. Полей TemplateField, которая была темой обсуждения в разделе [Использование полей TemplateField в элементе управления GridView](../custom-formatting/using-templatefields-in-the-gridview-control-cs.md) и [Использование полей TemplateField в руководствах по элементу управления DetailsView](../custom-formatting/using-templatefields-in-the-detailsview-control-vb.md) , может состоять из нескольких шаблонов, определяющих отдельные интерфейсы для различных состояний строк. `ItemTemplate` TemplateField используется для отображения полей или строк, предназначенных только для чтения, в элементах управления DetailsView или GridView, в то время как `EditItemTemplate` и `InsertItemTemplate` указывают интерфейсы для использования в режимах редактирования и вставки соответственно.

В этом учебнике мы рассмотрим, как легко добавить элементы управления проверки в `EditItemTemplate` и `InsertItemTemplate` для предоставления более защищенного пользовательского интерфейса. В частности, в этом учебнике используется пример, созданный в статье [изучение событий, связанных с руководством по вставке, обновлению и удалению,](examining-the-events-associated-with-inserting-updating-and-deleting-vb.md) и дополнение интерфейсов правки и вставки для включения соответствующей проверки.

## <a name="step-1-replicating-the-example-fromexamining-the-events-associated-with-inserting-updating-and-deleting"></a>Шаг 1. репликация примера из[проверки событий, связанных с вставкой, обновлением и удалением](examining-the-events-associated-with-inserting-updating-and-deleting-vb.md)

В ходе [изучения событий, связанных с вставкой, обновлением и удалением](examining-the-events-associated-with-inserting-updating-and-deleting-vb.md) учебника, мы создали страницу, в которой указаны имена и цены продуктов в редактируемом элементе управления GridView. Кроме того, на странице содержится элемент DetailsView, для свойства `DefaultMode` которого было задано значение `Insert`, таким образом, всегда выполняется отрисовка в режиме вставки. С помощью этой DetailsView пользователь может ввести имя и цену для нового продукта, нажать кнопку Вставить и добавить в систему (см. рис. 1).

[![предыдущем примере позволяет пользователям добавлять новые продукты и изменять существующие.](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image2.png)](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image1.png)

**Рис. 1**. предыдущий пример позволяет пользователям добавлять новые продукты и изменять существующие ([щелкните, чтобы просмотреть изображение с полным размером](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image3.png)).

Наша цель этого руководства — расширение DetailsView и GridView для предоставления элементов управления проверки. В частности, наша логика проверки будет:

- Требовать, чтобы имя было указано при вставке или изменении продукта
- Требовать, чтобы цена была предоставлена при вставке записи; При редактировании записи будет по-прежнему требоваться Цена, но будет использоваться программная логика в обработчике событий `RowUpdating` GridView, уже присутствующей в предыдущем руководстве.
- Убедитесь, что значение, указанное для цены, является допустимым форматом валюты.

Прежде чем можно будет рассмотреть возможность расширения предыдущего примера, чтобы включить проверку, сначала необходимо выполнить репликацию примера со страницы `DataModificationEvents.aspx` на страницу этого руководства, `UIValidation.aspx`. Чтобы сделать это, необходимо скопировать декларативную разметку `DataModificationEvents.aspx` страницы и ее исходный код. Сначала скопируйте декларативную разметку, выполнив следующие действия.

1. Открытие страницы `DataModificationEvents.aspx` в Visual Studio
2. Переход к декларативной разметке страницы (нажмите кнопку "источник" в нижней части страницы)
3. Скопируйте текст в теги `<asp:Content>` и `</asp:Content>` (строки с 3 по 44), как показано на рис. 2.

[![скопировать текст в элемент управления &lt;ASP: Content&gt;](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image5.png)](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image4.png)

**Рис. 2**. копирование текста внутри элемента управления `<asp:Content>` ([щелкните, чтобы просмотреть изображение с полным размером](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image6.png))

1. Открытие страницы `UIValidation.aspx`
2. Переход к декларативной разметке страницы
3. Вставьте текст в элемент управления `<asp:Content>`.

Чтобы скопировать исходный код, откройте страницу `DataModificationEvents.aspx.vb` и скопируйте только текст *внутри* класса `EditInsertDelete_DataModificationEvents`. Скопируйте три обработчика событий (`Page_Load`, `GridView1_RowUpdating`и `ObjectDataSource1_Inserting`), но **не** копируйте объявление класса. Вставьте скопированный текст *в класс `EditInsertDelete_UIValidation` в `UIValidation.aspx.vb`* .

После перемещения содержимого и кода с `DataModificationEvents.aspx` на `UIValidation.aspx`, уделите несколько минут тестированию хода выполнения в браузере. Вы должны увидеть одни и те же функции в каждой из этих двух страниц (см. рис. 1 для снимка экрана `DataModificationEvents.aspx` в действии).

## <a name="step-2-converting-the-boundfields-into-templatefields"></a>Шаг 2. Преобразование BoundFields в полей TemplateField

Чтобы добавить элементы управления проверки в интерфейсы правки и вставки, BoundFields, используемый элементами управления DetailsView и GridView, необходимо преобразовать в полей TemplateField. Чтобы добиться этого, щелкните ссылку изменить столбцы и изменить поля в смарт-тегах GridView и DetailsView соответственно. Выберите все BoundFields и щелкните ссылку "преобразовать это поле в TemplateField".

[![преобразовать все BoundFields элемента DetailsView и GridView в полей TemplateField](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image8.png)](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image7.png)

**Рис. 3**. Преобразование всех BoundFields элементов DetailsView и GridView в полей TemplateField ([щелкните, чтобы просмотреть изображение с полным размером](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image9.png))

При преобразовании BoundField в TemplateField с помощью диалогового окна "поля" создается TemplateField, которая имеет те же интерфейсы только для чтения, правки и вставки, что и сам BoundField. В следующей разметке показан декларативный синтаксис поля `ProductName` в DetailsView после его преобразования в TemplateField:

[!code-aspx[Main](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/samples/sample1.aspx)]

Обратите внимание, что в этом TemplateField созданы три шаблона, которые автоматически создаются `ItemTemplate`, `EditItemTemplate`и `InsertItemTemplate`. `ItemTemplate` отображает одно значение поля данных (`ProductName`) с помощью веб-элемента управления Label, а `EditItemTemplate` и `InsertItemTemplate` представлять значение поля данных в веб-элементе управления TextBox, связывающем поле данных с свойством `Text` текстового поля, используя двустороннюю привязку данных. Так как мы используем только DetailsView на этой странице для вставки, вы можете удалить `ItemTemplate` и `EditItemTemplate` из двух полей TemplateField, несмотря на то, что они не имеют вреда.

Поскольку GridView не поддерживает встроенные функции вставки элемента управления DetailsView, преобразование поля `ProductName` GridView в TemplateField приводит только к `ItemTemplate` и `EditItemTemplate`:

[!code-aspx[Main](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/samples/sample2.aspx)]

Нажимая кнопку "преобразовать это поле в TemplateField", Visual Studio создаст TemplateField, шаблоны которого имитируют пользовательский интерфейс преобразованной BoundField. Это можно проверить, перейдя на эту страницу в браузере. Вы обнаружите, что внешний вид и поведение полей TemplateField идентичны опыту при использовании BoundFields.

> [!NOTE]
> Вы можете настроить интерфейсы редактирования в шаблонах по мере необходимости. Например, может потребоваться, чтобы текстовое поле в `UnitPrice` полей TemplateField отображалось как меньшее текстовое поле, чем `ProductName` текстовое поле. Для этого можно задать для свойства `Columns` текстового поля соответствующее значение или предоставить абсолютную ширину с помощью свойства `Width`. В следующем учебном курсе мы посмотрим, как полностью настроить интерфейс редактирования, заменив текстовое поле на альтернативный веб-элемент управления вводом данных.

## <a name="step-3-adding-the-validation-controls-to-the-gridviewsedititemtemplate-s"></a>Шаг 3. Добавление элементов управления проверки в`EditItemTemplate` s элемента GridView

При создании форм ввода данных важно, чтобы пользователи вводили все необходимые поля и все предоставленные входные данные были допустимыми, правильно отформатированными значениями. Чтобы обеспечить допустимость входных данных пользователя, ASP.NET предоставляет пять встроенных элементов управления проверки, предназначенных для проверки значения одного элемента управления вводом:

- [RequiredFieldValidator](https://msdn.microsoft.com/library/5hbw267h(VS.80).aspx) гарантирует, что указано значение
- Объект [CompareValidator](https://msdn.microsoft.com/library/db330ayw(VS.80).aspx) проверяет значение относительно другого значения веб-элемента управления или постоянного значения или обеспечивает допустимость формата значения для указанного типа данных.
- [RangeValidator](https://msdn.microsoft.com/library/f70d09xt.aspx) гарантирует, что значение находится в диапазоне значений
- [Регуларекспрессионвалидатор](https://msdn.microsoft.com/library/eahwtc9e.aspx) проверяет значение по [регулярному выражению](http://en.wikipedia.org/wiki/Regular_expression)
- [CustomValidator](https://msdn.microsoft.com/library/9eee01cx(VS.80).aspx) проверяет значение для пользовательского, определяемого пользователем метода

Дополнительные сведения об этих пяти элементах управления см. в [разделе "элементы проверки" статьи](https://quickstarts.asp.net/quickstartv20/aspnet/doc/ctrlref/validation/default.aspx) [краткие руководства по ASP.NET](https://asp.net/QuickStart/aspnet/).

В нашем учебном курсе необходимо использовать RequiredFieldValidator в элементах управления DetailsView и GridView `ProductName` полей TemplateField и RequiredFieldValidator в `UnitPrice` TemplateField DetailsView. Кроме того, необходимо добавить объект CompareValidator в элементы управления `UnitPrice` полей TemplateField, гарантирующие, что введенная цена имеет значение, большее или равное 0, и представлено в допустимом формате валюты.

> [!NOTE]
> Хотя в ASP.NET 1. x существовали те же пять элементов управления проверки, ASP.NET 2,0 добавил ряд усовершенствований, две основные возможности поддержки сценариев на стороне клиента для браузеров, отличных от Internet Explorer, и возможность секционировать элементы управления проверкой на странице в группы проверки. Дополнительные сведения о новых возможностях элементов управления проверки в 2,0 см. в статье [которая разбила The проверки элементов управления в ASP.NET 2,0](http://aspnet.4guysfromrolla.com/articles/112305-1.aspx).

Начнем с добавления необходимых элементов управления проверки в `EditItemTemplate` s в полей TemplateField GridView. Чтобы сделать это, щелкните ссылку изменить шаблоны в смарт-теге GridView, чтобы открыть интерфейс редактирования шаблонов. Здесь можно выбрать шаблон для редактирования из раскрывающегося списка. Так как мы хотим расширить интерфейс редактирования, нам нужно добавить элементы управления проверки в `ProductName` и `UnitPrice``EditItemTemplate` s.

[![нам нужно расширить Едититемтемплатес ProductName и UnitPrice](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image11.png)](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image10.png)

**Рис. 4**. необходимо расширить `ProductName` и `UnitPrice``EditItemTemplate` s ([щелкните, чтобы просмотреть изображение с полным размером](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image12.png))

В `ProductName` `EditItemTemplate`добавьте RequiredFieldValidator, перетащив его из панели элементов в интерфейс редактирования шаблона, поместив после текстового поля.

[![добавить RequiredFieldValidator в ProductName EditItemTemplate](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image14.png)](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image13.png)

**Рис. 5**. Добавление RequiredFieldValidator в `EditItemTemplate` `ProductName` ([щелкните, чтобы просмотреть изображение с полным размером](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image15.png))

Все элементы управления проверки работают путем проверки входных данных одного веб-элемента управления ASP.NET. Поэтому необходимо указать, что RequiredFieldValidator, который мы только что добавили, должен проверяться на соответствие текстовому полю в `EditItemTemplate`; Это достигается путем присвоения [свойству ControlToValidate](https://msdn.microsoft.com/library/system.web.ui.webcontrols.basevalidator.controltovalidate(VS.80).aspx) проверяющего элемента `ID` соответствующего веб-элемента управления. В настоящее время текстовое поле имеет довольно неопределенный `ID` `TextBox1`, но давайте изменим его на что-то более подходящее. Щелкните текстовое поле в шаблоне, а затем в окно свойств измените `ID` с `TextBox1` на `EditProductName`.

[![изменить идентификатор TextBox на Едитпродуктнаме](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image17.png)](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image16.png)

**Рис. 6**. изменение `ID` текстового поля на `EditProductName` ([щелкните, чтобы просмотреть изображение с полным размером](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image18.png))

Затем задайте для свойства `ControlToValidate` RequiredFieldValidator значение `EditProductName`. Наконец, задайте для [свойства ErrorMessage](https://msdn.microsoft.com/library/system.web.ui.webcontrols.basevalidator.errormessage(VS.80).aspx) значение "необходимо указать имя продукта", а [свойству Text](https://msdn.microsoft.com/library/system.web.ui.webcontrols.basevalidator.text(VS.80).aspx) — значение "\*". Значение свойства `Text`, если оно указано, является текстом, отображаемым элементом управления проверки, если проверка завершается неудачно. Значение свойства `ErrorMessage`, которое является обязательным, используется элементом управления ValidationSummary; Если значение свойства `Text` опущено, `ErrorMessage` значение свойства также является текстом, отображаемым элементом управления проверки на недопустимые входные данные.

После установки этих трех свойств RequiredFieldValidator экран должен выглядеть примерно так, как показано на рис. 7.

[![задать свойства ControlToValidate, ErrorMessage и Text для RequiredFieldValidator](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image20.png)](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image19.png)

**Рис. 7**. задание свойств `ControlToValidate`, `ErrorMessage`и `Text` для RequiredFieldValidator ([щелкните, чтобы просмотреть изображение с полным размером](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image21.png))

После добавления RequiredFieldValidator в `EditItemTemplate``ProductName` остается только добавить необходимую проверку в `UnitPrice` `EditItemTemplate`. Поскольку мы решили, что для этой страницы `UnitPrice` не является обязательным при редактировании записи, нам не нужно добавлять RequiredFieldValidator. Однако нам нужно добавить объект CompareValidator, чтобы `UnitPrice`, если он указан, правильно отформатирована как денежная единица и больше или равна 0.

Прежде чем добавить объект CompareValidator в `EditItemTemplate``UnitPrice`, сначала измените идентификатор веб-элемента управления TextBox с `TextBox2` на `EditUnitPrice`. После внесения этого изменения добавьте объект CompareValidator, установив для его свойства `ControlToValidate` значение `EditUnitPrice`, его свойство `ErrorMessage` значение "цена должна быть больше или равна нулю и не может включать символ валюты", а также его свойство `Text` в "\*".

Чтобы указать, что значение `UnitPrice` должно быть больше или равно 0, установите [свойство оператора](https://msdn.microsoft.com/library/system.web.ui.webcontrols.comparevalidator.operator(VS.80).aspx) CompareValidator в значение `GreaterThanEqual`, [свойство валуетокомпаре](https://msdn.microsoft.com/library/system.web.ui.webcontrols.comparevalidator.valuetocompare(VS.80).aspx) в значение 0, а [свойство Type](https://msdn.microsoft.com/library/system.web.ui.webcontrols.basecomparevalidator.type.aspx) — в значение `Currency`. Следующий декларативный синтаксис показывает `EditItemTemplate` `UnitPrice` TemplateField после внесения этих изменений:

[!code-aspx[Main](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/samples/sample3.aspx)]

После внесения этих изменений откройте страницу в браузере. Если вы попытаетесь опустить имя или ввести недопустимое значение цены при редактировании продукта, рядом с текстовым полем появится звездочка. Как показано на рис. 8, значение цены, включающее символ валюты, например $19,95, считается недопустимым. `Currency` объекта CompareValidator `Type` допускает разделители цифр (например, запятые или точки, в зависимости от настроек языка и региональных параметров) и начальный знак плюса или минуса, но *не* допускает символ валюты. Это поведение может озадачить пользователей, так как интерфейс правки в настоящее время визуализирует `UnitPrice`, используя формат валюты.

> [!NOTE]
> Вспомним, что в учебнике *события, связанные с вставкой, обновлением и удалением,* мы установили для свойства `DataFormatString` BoundField значение `{0:c}`, чтобы отформатировать его как денежную единицу. Кроме того, свойству `ApplyFormatInEditMode` присваивается значение true, в результате чего интерфейс редактирования GridView форматирует `UnitPrice` как денежную единицу. При преобразовании BoundField в TemplateField Visual Studio отметил эти параметры и отформатирует свойство `Text` текстового поля как денежную единицу с помощью синтаксиса DataBinding `<%# Bind("UnitPrice", "{0:c}") %>`.

[![звездочка отображается рядом с текстовыми полями с недопустимыми входными данными](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image23.png)](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image22.png)

**Рис. 8**. Звездочка рядом с текстовыми полями с недопустимым входом ([щелкните, чтобы просмотреть изображение с полным размером](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image24.png))

Хотя проверка работает как есть, пользователь должен вручную удалить символ валюты при редактировании записи, что неприемлемо. Для устранения этой проблемы у нас есть три варианта:

1. Настройте `EditItemTemplate` таким образом, чтобы значение `UnitPrice` не отформатировано как денежная единица.
2. Разрешить пользователю вводить символ валюты, удаляя объект CompareValidator и заменяя его Регуларекспрессионвалидатор, который правильно проверяет значение валюты в правильном формате. Проблема в том, что регулярное выражение для проверки значения валюты не вполне достаточно и потребует написания кода, если нам хотелось бы включить параметры языка и региональных параметров.
3. Полностью удалите элемент управления проверки и полагаются на логику проверки на стороне сервера в обработчике событий `RowUpdating` GridView.

Давайте перейдем к параметру #1 для этого упражнения. В настоящее время `UnitPrice` форматируется как валюта из-за выражения привязки данных для текстового поля в `EditItemTemplate`: `<%# Bind("UnitPrice", "{0:c}") %>`. Измените инструкцию Bind на `Bind("UnitPrice", "{0:n2}")`, которая форматирует результат как число с двумя цифрами точности. Это можно сделать напрямую с помощью декларативного синтаксиса или щелкнув ссылку Edit DataBindings (изменить ссылки на данные) в текстовом поле `EditUnitPrice` в `EditItemTemplate`е `UnitPrice` TemplateField (см. рис. 9 и 10).

[![щелкните ссылку изменить привязки к элементу TextBox.](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image26.png)](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image25.png)

**Рис. 9**. Щелкните ссылку Edit DataBindings (Правка) текстового поля ([щелкните, чтобы просмотреть изображение с полным размером](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image27.png))

[![указать описатель формата в инструкции BIND](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image29.png)](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image28.png)

**Рис. 10**. Указание описателя формата в операторе `Bind` ([щелкните, чтобы просмотреть изображение с полным размером](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image30.png))

При этом изменении отформатированная Цена в интерфейсе редактирования включает запятые в качестве разделителя групп и точку в качестве десятичного разделителя, но оставляет символ валюты.

> [!NOTE]
> `UnitPrice` `EditItemTemplate` не содержит RequiredFieldValidator, что позволяет выполнить обратную передачу и инициировать логику обновления. Однако обработчик событий `RowUpdating`, скопированный из руководства по *вставке, обновлению и удалению* , содержит программную проверку, которая гарантирует, что `UnitPrice` предоставляется. Вы можете удалить эту логику, оставить ее в виде "как есть" или добавить RequiredFieldValidator в `EditItemTemplate``UnitPrice`.

## <a name="step-4-summarizing-data-entry-problems"></a>Шаг 4. сводка проблем ввода данных

В дополнение к пяти проверочным элементам управления ASP.NET включает [элемент управления ValidationSummary](https://msdn.microsoft.com/library/f9h59855(VS.80).aspx), который отображает `ErrorMessage`ные элементы управления проверки, которые обнаружили недопустимые данные. Сводные данные могут отображаться в виде текста на веб-странице или с помощью модального окна MessageBox на стороне клиента. Попробуем улучшить этот учебник, чтобы включить в клиент MessageBox сводку по всем проблемам проверки.

Для этого перетащите элемент управления ValidationSummary с панели инструментов в конструктор. Расположение элемента управления проверки не имеет значения, так как мы настроим его для вывода сводки только в виде MessageBox. После добавления элемента управления задайте для его [Свойства шовсуммари](https://msdn.microsoft.com/library/system.web.ui.webcontrols.validationsummary.showsummary(VS.80).aspx) значение `False` а [свойству метода showmessagebox](https://msdn.microsoft.com/library/system.web.ui.webcontrols.validationsummary.showmessagebox(VS.80).aspx) — значение `True`. Благодаря этому добавлению все ошибки проверки обрабатываются в элементе MessageBox на стороне клиента.

[![ошибки проверки обобщены в окне MessageBox на стороне клиента](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image32.png)](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image31.png)

**Рис. 11**. ошибки проверки обобщены в окне MessageBox на стороне клиента ([щелкните, чтобы просмотреть изображение с полным размером](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image33.png))

## <a name="step-5-adding-the-validation-controls-to-the-detailsviewsinsertitemtemplate"></a>Шаг 5. Добавление элементов управления проверки в`InsertItemTemplate` элемента DetailsView

Все, что остается в этом руководстве, — добавить элементы управления проверки в интерфейс вставки DetailsView. Процесс добавления элементов управления проверки в шаблоны DetailsView идентичен тому, что был проверен в шаге 3. Поэтому мы удалим задачу на этом шаге. Как и в случае с `EditItemTemplate` GridView, я рекомендую переименовать `ID` s из текстовых полей из `TextBox1` неопределенный и `TextBox2` в `InsertProductName` и `InsertUnitPrice`.

Добавьте RequiredFieldValidator в `InsertItemTemplate``ProductName`. Присвойте `ControlToValidate` `ID` текстового поля в шаблоне, его свойству `Text` значение "\*" и свойству `ErrorMessage` значение "необходимо указать имя продукта".

Поскольку `UnitPrice` требуется для этой страницы при добавлении новой записи, добавьте RequiredFieldValidator в `UnitPrice` `InsertItemTemplate`, указав свойства `ControlToValidate`, `Text`и `ErrorMessage` соответствующим образом. Наконец, добавьте элемент управления CompareValidator в `InsertItemTemplate` `UnitPrice`, настроив его свойства `ControlToValidate`, `Text`, `ErrorMessage`, `Type`, `Operator`и `ValueToCompare` точно так же, как и в элементе управления CompareValidator `UnitPrice`в `EditItemTemplate`GridView.

После добавления этих элементов управления проверки новый продукт не может быть добавлен в систему, если его имя не указано или если его цена является отрицательным числом или недопустимым форматом.

[в интерфейс вставки DetailsView добавлена ![логика проверки](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image35.png)](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image34.png)

**Рис. 12**. логика проверки добавлена в интерфейс вставки DetailsView ([щелкните, чтобы просмотреть изображение с полным размером](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image36.png))

## <a name="step-6-partitioning-the-validation-controls-into-validation-groups"></a>Шаг 6. секционирование проверяющих элементов управления в группы проверки

Наша страница состоит из двух логически разнородных наборов элементов управления проверки: тех, которые соответствуют интерфейсу правки GridView, и тем, которые соответствуют интерфейсу вставки DetailsView. По умолчанию, когда выполняется обратная передача, проверяются *все* элементы управления проверки на странице. Однако при редактировании записи мы не хотим, чтобы элементы управления проверки интерфейса вставки элемента DetailsView были проверены. На рис. 13 показаны наши текущие дилеммой, когда пользователь редактирует продукт с помощью идеально допустимых значений. Если нажать кнопку обновить, это приведет к ошибке проверки, так как значения Name и Price в интерфейсе вставки пусты.

[![обновление продукта приводит к срабатыванию элементов управления проверки интерфейса вставки](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image38.png)](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image37.png)

**Рис. 13**. Обновление продукта вызывает срабатывание элементов управления проверки интерфейса вставки ([щелкните, чтобы просмотреть изображение с полным размером](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image39.png))

Элементы управления проверки в ASP.NET 2,0 могут быть разделены на группы проверки с помощью свойства `ValidationGroup`. Чтобы связать набор элементов управления проверки в группе, просто присвойте свойству `ValidationGroup` одно и то же значение. Для нашего руководства задайте для свойств `ValidationGroup` элементов управления проверки в элементе GridView полей TemplateField значение `EditValidationControls` и `ValidationGroup` свойства полей TemplateField DetailsView `InsertValidationControls`. Эти изменения можно выполнить непосредственно в декларативной разметке или с помощью окно свойств при использовании интерфейса редактирования шаблона конструктора.

Помимо элементов управления проверки, кнопки и элементы управления, связанные с кнопками в ASP.NET 2,0, также включают свойство `ValidationGroup`. Проверяющие элементы управления для группы проверки проверяются на допустимость только в том случае, если обратная передача вызывается кнопкой, имеющей тот же параметр `ValidationGroup` свойства. Например, чтобы кнопка вставки DetailsView активировала `InsertValidationControls` группу проверки, необходимо задать для свойства `ValidationGroup` CommandField значение `InsertValidationControls` (см. рис. 14). Кроме того, задайте для свойства Коммандфиелд'с `ValidationGroup` GridView значение `EditValidationControls`.

[![установить для свойства Валидатионграуп Коммандфиелд'с DetailsView значение Инсертвалидатионконтролс](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image41.png)](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image40.png)

**Рис. 14**. установка свойства `ValidationGroup` коммандфиелд'с DetailsView в значение `InsertValidationControls` ([щелкните, чтобы просмотреть изображение с полным размером](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image42.png))

После этих изменений полей TemplateField и Коммандфиелдс DetailsView и GridView должны выглядеть следующим образом:

Полей TemplateField и CommandField DetailsView

[!code-aspx[Main](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/samples/sample4.aspx)]

CommandField и полей TemplateField GridView

[!code-aspx[Main](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/samples/sample5.aspx)]

На этом этапе проверочные элементы управления, относящиеся к редактированию, срабатывают только при нажатии кнопки обновления GridView, а проверочные элементы управления, относящиеся к вставке, срабатывают только при нажатии кнопки вставки DetailsView, устраняя проблему, выделенную на рис. 13. Однако после этого изменения наш элемент управления ValidationSummary больше не отображается при вводе недопустимых данных. Элемент управления ValidationSummary также содержит свойство `ValidationGroup` и отображает сводные данные только для этих элементов управления проверки в своей группе проверки. Поэтому на этой странице должны быть два элемента управления проверки: одна для группы проверки `InsertValidationControls` и одна для `EditValidationControls`.

[!code-aspx[Main](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/samples/sample6.aspx)]

С этим добавлением наш учебник завершен.

## <a name="summary"></a>Сводка

Хотя BoundFields может предоставлять и интерфейс вставки, и правки, интерфейс нельзя настраивать. Как правило, нам нужно добавить элементы управления проверки в интерфейс правки и вставки, чтобы убедиться, что пользователь вводит необходимые входные данные в допустимый формат. Для этого необходимо преобразовать BoundFields в полей TemplateField и добавить элементы управления проверки к соответствующим шаблонам. В этом учебнике мы расширили пример из статьи *изучение событий, связанных с руководством по вставке, обновлению и удалению* , добавляя элементы управления проверки в интерфейс вставки DetailsView и интерфейс правки GridView. Более того, мы увидели, как отображать сводные данные проверки с помощью элемента управления ValidationSummary и как секционировать элементы управления проверки на странице в отдельные группы проверки.

Как мы видели в этом руководстве, полей TemplateField позволяют дополнять интерфейсы правки и вставки для включения элементов управления проверки. Полей TemplateField также можно расширить для включения дополнительных входных веб-элементов управления, что позволяет заменить текстовое поле более подходящим веб-элементом управления. В следующем учебном курсе мы покажем, как заменить элемент управления TextBox элементом управления DropDownList с привязкой к данным, который идеально подходит при редактировании внешнего ключа (такого как `CategoryID` или `SupplierID` в таблице `Products`).

Поздравляем с программированием!

## <a name="about-the-author"></a>Об авторе

[Скотт Митчелл](http://www.4guysfromrolla.com/ScottMitchell.shtml), автор семи книг по ASP/ASP. NET и основатель [4GuysFromRolla.com](http://www.4guysfromrolla.com), работал с веб-технологиями Майкрософт с 1998. Скотт работает как независимый консультант, преподаватель и модуль записи. Его последняя книга — [*Sams обучать себя ASP.NET 2,0 за 24 часа*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco). Он доступен по адресу [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) или через его блог, который можно найти по адресу [http://ScottOnWriting.NET](http://ScottOnWriting.NET).

## <a name="special-thanks-to"></a>Специальная благодарность

Эта серия руководств была рассмотрена многими полезными рецензентами. Потенциальным рецензентам для этого учебника были основными рецензентами и Зак Jones. Хотите ознакомиться с моими будущими статьями MSDN? Если это так, расположите строку в [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Назад](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb.md)
> [Вперед](customizing-the-data-modification-interface-vb.md)
