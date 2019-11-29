---
uid: web-forms/overview/data-access/editing-inserting-and-deleting-data/examining-the-events-associated-with-inserting-updating-and-deleting-vb
title: Изучение событий, связанных с вставкой, обновлением и удалением (VB) | Документация Майкрософт
author: rick-anderson
description: В этом учебнике мы рассмотрим использование событий, происходящих до, во время и после операции вставки, обновления или удаления веб-элемента управления данными ASP.NET. W...
ms.author: riande
ms.date: 07/17/2006
ms.assetid: c9bd10a7-eff8-4d8c-bec9-963c2aef2d6e
msc.legacyurl: /web-forms/overview/data-access/editing-inserting-and-deleting-data/examining-the-events-associated-with-inserting-updating-and-deleting-vb
msc.type: authoredcontent
ms.openlocfilehash: 35edb3cefc6fe23bb56e667c02d10dc7798f730d
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/28/2019
ms.locfileid: "74633133"
---
# <a name="examining-the-events-associated-with-inserting-updating-and-deleting-vb"></a>Обзор событий, связанных со вставкой, обновлением и удалением (VB)

по [Скотт Митчелл](https://twitter.com/ScottOnWriting)

[Скачивание примера приложения](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_17_VB.exe) или [Загрузка PDF-файла](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/datatutorial17vb1.pdf)

> В этом учебнике мы рассмотрим использование событий, происходящих до, во время и после операции вставки, обновления или удаления веб-элемента управления данными ASP.NET. Также будет показано, как настроить интерфейс редактирования, чтобы обновить только подмножество полей продукта.

## <a name="introduction"></a>Введение

При использовании встроенных функций вставки, редактирования или удаления элементов управления GridView, DetailsView или FormView при завершении пользователем процесса добавления новой записи или обновления или удаления существующей записи происходит ряд действий. Как мы обсуждали в [предыдущем учебном курсе](an-overview-of-inserting-updating-and-deleting-data-vb.md), при редактировании строки в GridView кнопка "Изменить" заменяется кнопками "Обновить" и "Отмена", а BoundFields превращается в текстовые поля. После того как конечный пользователь обновит данные и нажмет кнопку обновить, на обратную передачу выполняются следующие действия.

1. GridView заполняет `UpdateParameters` ObjectDataSource уникальными идентифицирующими полями (с помощью свойства `DataKeyNames`) и значениями, указанными пользователем.
2. GridView вызывает метод `Update()` ObjectDataSource, который, в свою очередь, вызывает соответствующий метод в базовом объекте (`ProductsDAL.UpdateProduct`, в нашем предыдущем руководстве).
3. Базовые данные, которые теперь содержат обновленные изменения, повторно привязаны к GridView

В ходе этой последовательности действий вызывается ряд событий, что позволяет нам создавать обработчики событий для добавления настраиваемой логики там, где это необходимо. Например, перед шагом 1 срабатывает событие `RowUpdating` GridView. На этом этапе можно отменить запрос на обновление в случае возникновения ошибки проверки. При вызове метода `Update()` срабатывает событие `Updating` ObjectDataSource, предоставляя возможность добавлять или настраивать значения любого из `UpdateParameters`. После завершения выполнения метода базового объекта ObjectDataSource возникает событие `Updated` ObjectDataSource. Обработчик события `Updated` может проверить сведения об операции обновления, например количество затронутых строк и наличие исключения. Наконец, после шага 2 срабатывает событие `RowUpdated` GridView. обработчик событий для этого события может проверять дополнительные сведения о только что выполненной операции обновления.

На рис. 1 показана эта серия событий и действий при обновлении элемента управления GridView. Шаблон события на рис. 1 не является уникальным для обновления с помощью GridView. Вставка, обновление или удаление данных из GridView, DetailsView или FormView преЦипитатес одной и той же последовательности событий до и после уровня для веб-элемента управления данными и ObjectDataSource.

[При обновлении данных в GridView ![вызывается ряд событий, выполняемых до и после события](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image2.png)](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image1.png)

**Рис. 1**. запуск действий, выполняемых до и после событий, при обновлении данных в элементе управления GridView ([щелкните, чтобы просмотреть изображение с полным размером](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image3.png))

В этом учебнике мы рассмотрим использование этих событий для расширения встроенных возможностей вставки, обновления и удаления веб-элементов управления данными ASP.NET. Также будет показано, как настроить интерфейс редактирования, чтобы обновить только подмножество полей продукта.

## <a name="step-1-updating-a-productsproductnameandunitpricefields"></a>Шаг 1. Обновление полей`ProductName`и`UnitPrice`продукта

В интерфейсах редактирования из предыдущего учебника должны быть добавлены *все* поля продукта, которые не были доступны только для чтения. Если бы было необходимо удалить поле из GridView-скажите `QuantityPerUnit`-при обновлении данных веб-элемент управления не задаст значение `QuantityPerUnit` `UpdateParameters` ObjectDataSource. Затем ObjectDataSource передавал значение `Nothing` в метод `UpdateProduct` бизнес-логики (BLL), который изменит `QuantityPerUnit` столбец измененной записи базы данных на значение `NULL`. Аналогично, если обязательное поле, например `ProductName`, удаляется из интерфейса правки, обновление завершится ошибкой с исключением "*столбец" ProductName "не допускает значения NULL*". Причина этого поведения была вызвана тем, что ObjectDataSource был настроен на вызов метода `UpdateProduct` класса `ProductsBLL`, который ожидал входного параметра для каждого поля продукта. Таким образом, коллекция `UpdateParameters` ObjectDataSource содержала параметр для каждого входного параметра метода.

Если мы хотим предоставить веб-элемент управления данными, позволяющий конечному пользователю обновлять только подмножество полей, необходимо либо программно задать отсутствующие значения `UpdateParameters` в обработчике событий `Updating` ObjectDataSource, либо создать и вызвать метод BLL, который предполагает наличие только подмножества полей. Давайте рассмотрим этот второй подход.

В частности, создадим страницу, отображающую только поля `ProductName` и `UnitPrice` в редактируемом элементе управления GridView. Этот интерфейс редактирования GridView позволяет пользователю только обновлять два отображаемых поля: `ProductName` и `UnitPrice`. Поскольку этот интерфейс редактирования предоставляет только подмножество полей продукта, нам нужно создать элемент ObjectDataSource, использующий существующий метод `UpdateProduct` BLL и имеющий отсутствующие значения полей продукта, заданные программно в `Updating` обработчике событий, или необходимо создать новый метод BLL, который предполагает только подмножество полей, определенных в GridView. В этом руководстве мы будем использовать второй вариант и создаем перегрузку метода `UpdateProduct`, который принимает только три входных параметра: `productName`, `unitPrice`и `productID`:

[!code-vb[Main](examining-the-events-associated-with-inserting-updating-and-deleting-vb/samples/sample1.vb)]

Как и исходный метод `UpdateProduct`, эта перегрузка начинается с проверки наличия в базе данных продукта с указанным `ProductID`. В противном случае возвращается `False`, указывающий на сбой запроса на обновление сведений о продукте. В противном случае он обновляет существующие `ProductName` записи продукта и `UnitPrice` поля соответствующим образом и фиксирует обновление, вызывая метод `Update()` TableAdapter, передавая экземпляр `ProductsRow`.

Это дополнение к нашему `ProductsBLL` классу, мы готовы к созданию упрощенного интерфейса GridView. Откройте `DataModificationEvents.aspx` в папке `EditInsertDelete` и добавьте GridView на страницу. Создайте новый элемент ObjectDataSource и настройте его так, чтобы он использовал `ProductsBLL` класс с соответствующим `Select()` сопоставлением метода `GetProducts` и его `Update()` сопоставление с перегрузкой `UpdateProduct`, принимающей только входные параметры `productName`, `unitPrice`и `productID`. На рис. 2 показан мастер создания источника данных при сопоставлении метода `Update()` ObjectDataSource с новой перегрузкой метода `UpdateProduct` класса `ProductsBLL`.

[![сопоставьте метод Update () элемента ObjectDataSource с новой перегрузкой UpdateProduct](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image5.png)](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image4.png)

**Рис. 2**. сопоставьте метод `Update()` ObjectDataSource с новой перегрузкой `UpdateProduct` ([щелкните, чтобы просмотреть изображение с полным размером](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image6.png))

Поскольку в нашем примере изначально требуется возможность редактирования только данных, но не для вставки или удаления записей, потратьте немного времени, чтобы явно указать, что методы `Insert()` и `Delete()` ObjectDataSource не должны сопоставляться ни с одним из методов класса `ProductsBLL`, перейдя на вкладки вставки и удаления и выбрав (нет) в раскрывающемся списке.

[![выберите (нет) из раскрывающегося списка для вкладок Вставка и удаление.](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image8.png)](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image7.png)

**Рис. 3**. Выбор (нет) из раскрывающегося списка для вкладок вставки и удаления ([щелкните, чтобы просмотреть изображение с полным размером](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image9.png))

После завершения работы мастера установите флажок Включить редактирование в смарт-теге GridView.

После завершения работы мастера создания источника данных и привязки к GridView в Visual Studio был создан декларативный синтаксис для обоих элементов управления. Перейдите в представление исходного кода, чтобы проверить декларативную разметку ObjectDataSource, показанную ниже.

[!code-aspx[Main](examining-the-events-associated-with-inserting-updating-and-deleting-vb/samples/sample2.aspx)]

Поскольку нет сопоставлений для методов `Insert()` и `Delete()` ObjectDataSource, разделы `InsertParameters` или `DeleteParameters` отсутствуют. Более того, так как метод `Update()` сопоставлен с перегрузкой метода `UpdateProduct`, которая принимает только три входных параметра, раздел `UpdateParameters` содержит только три экземпляра `Parameter`.

Обратите внимание, что свойство `OldValuesParameterFormatString` ObjectDataSource имеет значение `original_{0}`. Это свойство задается автоматически с помощью Visual Studio при использовании мастера настройки источника данных. Однако, поскольку наши методы BLL не предполагают, что исходное значение `ProductID` передается, удалите это назначение свойства из декларативного синтаксиса ObjectDataSource.

> [!NOTE]
> Если вы просто удалите значение свойства `OldValuesParameterFormatString` из окно свойств в представление конструирования, это свойство по-прежнему будет существовать в декларативном синтаксисе, но будет установлено в виде пустой строки. Либо удалите свойство из декларативного синтаксиса, либо в окно свойств задайте значение по умолчанию `{0}`.

Хотя элемент ObjectDataSource содержит только `UpdateParameters` названия, цены и идентификатора продукта, Visual Studio добавил BoundField или CheckBoxField в GridView для каждого из полей продукта.

[![GridView содержит BoundField или CheckBoxField для каждого из полей продукта.](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image11.png)](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image10.png)

**Рисунок 4**. элемент GridView содержит BoundField или CheckBoxField для каждого из полей продукта ([щелкните, чтобы просмотреть изображение с полным размером](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image12.png)).

Когда пользователь редактирует продукт и нажимает кнопку "Обновить", GridView перечисляет поля, которые не были доступны только для чтения. Затем он устанавливает значение соответствующего параметра в коллекции `UpdateParameters` ObjectDataSource в значение, указанное пользователем. Если соответствующий параметр отсутствует, GridView добавляет его в коллекцию. Таким образом, если наш элемент GridView содержит BoundFields и Чеккбоксфиелдс для всех полей продукта, то ObjectDataSource будет вызывать перегрузку `UpdateProduct`, которая принимает все эти параметры, несмотря на тот факт, что декларативная разметка ObjectDataSource указывает только три входных параметра (см. рис. 5). Аналогично, если в GridView имеется некоторое сочетание полей продуктов, не предназначенных только для чтения, которые не соответствуют входным параметрам для перегрузки `UpdateProduct`, при попытке обновления будет вызвано исключение.

[![GridView добавит параметры в коллекцию UpdateParameters ObjectDataSource](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image14.png)](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image13.png)

**Рис. 5**. элемент управления GridView добавит параметры в коллекцию `UpdateParameters` ObjectDataSource ([щелкните, чтобы просмотреть изображение с полным размером](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image15.png))

Чтобы убедиться, что ObjectDataSource вызывает перегрузку `UpdateProduct`, которая принимает только имя продукта, цену и идентификатор, необходимо ограничить GridView, чтобы поля с возможностью редактирования были только для `ProductName` и `UnitPrice`. Это можно сделать, удалив другие BoundFields и Чеккбоксфиелдс, установив для этих полей `ReadOnly` свойство `True`или несколько комбинаций этих двух значений. В этом руководстве мы просто удалим все поля GridView, кроме `ProductName` и `UnitPrice` BoundFields, после чего декларативная разметка GridView будет выглядеть следующим образом:

[!code-aspx[Main](examining-the-events-associated-with-inserting-updating-and-deleting-vb/samples/sample3.aspx)]

Несмотря на то, что перегрузка `UpdateProduct` предполагает три входных параметра, в элементе GridView есть только два BoundFields. Это связано с тем, что входной параметр `productID` является значением первичного ключа и передается через значение свойства `DataKeyNames` для редактируемой строки.

Наш GridView вместе с перегрузкой `UpdateProduct` позволяет пользователю изменять только название и цену продукта, не теряя никаких других полей продукта.

[![интерфейс позволяет изменять только название и цену продукта](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image17.png)](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image16.png)

**Рис. 6**. интерфейс позволяет изменять только название и цену продукта ([щелкните, чтобы просмотреть изображение с полным размером](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image18.png)).

> [!NOTE]
> Как обсуждалось в предыдущем руководстве, крайне важно, чтобы состояние представления GridView s было включено (поведение по умолчанию). Если для свойства `EnableViewState` GridView s задано значение `false`, возникает риск непреднамеренного удаления или изменения записей одновременно выполняющимися пользователями. См. [Предупреждение: ошибка параллелизма с ASP.NET 2,0 gridviews/DetailsView/FormView, которые поддерживают редактирование и (или) удаление, а состояние представления — "отключено](http://scottonwriting.net/sowblog/posts/10054.aspx) " для получения дополнительных сведений.

## <a name="improving-theunitpriceformatting"></a>Улучшение форматирования`UnitPrice`

Хотя пример GridView, показанный на рис. 6, работает, поле `UnitPrice` не отформатировано, в результате отображается цена, в которой отсутствуют символы валют и есть четыре десятичных знака. Чтобы применить форматирование валюты для неизменяемых строк, просто задайте для свойства `DataFormatString` `UnitPrice` BoundField значение `{0:c}`, а для свойства `HtmlEncode` — значение `False`.

[![соответствующим образом задать свойства Датаформатстринг и HtmlEncode UnitPrice](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image20.png)](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image19.png)

**Рис. 7**. настройка свойств `DataFormatString` и `HtmlEncode` для `UnitPrice`соответственно ([щелкните, чтобы просмотреть изображение с полным размером](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image21.png))

После этого изменения Цена нередактируемых строк форматируется как валюта. Однако измененная строка по-прежнему отображает значение без символа валюты и с четырьмя десятичными разрядами.

[![неизменяемые строки теперь форматируются как денежные значения](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image23.png)](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image22.png)

**Рис. 8**. неизменяемые строки теперь форматируются как денежные значения ([щелкните, чтобы просмотреть изображение с полным размером](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image24.png))

Инструкции форматирования, указанные в свойстве `DataFormatString`, можно применить к интерфейсу редактирования, задав для свойства `ApplyFormatInEditMode` BoundField значение `True` (значение по умолчанию — `False`). Уделите время, чтобы задать для этого свойства значение `True`.

[![задать для свойства Апплиформатинедитмоде UnitPrice BoundField значение true](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image26.png)](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image25.png)

**Рис. 9**. установка свойства `ApplyFormatInEditMode` `UnitPrice` BoundField в значение `True` ([щелкните, чтобы просмотреть изображение с полным размером](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image27.png))

После этого изменения значение `UnitPrice`, отображаемое в измененной строке, также форматируется как денежная единица.

[![значение UnitPrice измененной строки теперь отформатировано как денежное](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image29.png)](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image28.png)

**Рис. 10**. значение `UnitPrice` измененной строки теперь отформатировано как денежная единица ([щелкните, чтобы просмотреть изображение с полным размером](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image30.png))

Однако обновление продукта с помощью символа валюты в текстовом поле, например $19,00, вызывает `FormatException`. Когда GridView пытается назначить предоставленные пользователем значения для коллекции `UpdateParameters` ObjectDataSource, не удается преобразовать `UnitPrice` строку "$19,00" в `Decimal`, необходимую для параметра (см. рис. 11). Чтобы устранить эту проблему, можно создать обработчик событий для события `RowUpdating` GridView и проанализировать предоставленные пользователем `UnitPrice` как `Decimal`в формате валюты.

Событие `RowUpdating` GridView принимает в качестве второго параметра объект типа [гридвиевупдативентаргс](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridviewupdateeventargs(VS.80).aspx), который включает словарь `NewValues` в качестве одного из свойств, которые содержат предоставленные пользователем значения, готовые для назначения коллекции `UpdateParameters` ObjectDataSource. Можно перезаписать существующее значение `UnitPrice` в коллекции `NewValues` десятичным значением, проанализированным с помощью формата валюты, со следующими строками кода в обработчике событий `RowUpdating`:

[!code-vb[Main](examining-the-events-associated-with-inserting-updating-and-deleting-vb/samples/sample4.vb)]

Если пользователь предоставил `UnitPrice` значение (например, "$19,00"), это значение перезаписывается десятичным значением, вычисленным [десятичным. Parse](https://msdn.microsoft.com/library/system.decimal.parse(VS.80).aspx), анализируя значение как денежную единицу. Это приведет к правильному анализу десятичного значения в случае любых символов валют, запятыми, десятичных разделителей и т. д., а также использует [Перечисление NumberStyles](https://msdn.microsoft.com/library/system.globalization.numberstyles(VS.80).aspx) в пространстве имен [System. Globalization](https://msdn.microsoft.com/library/abeh092z(VS.80).aspx) .

На рис. 11 показана и проблема, вызванная символами валют в предоставленных пользователем `UnitPrice`, а также способ использования обработчика событий `RowUpdating` GridView для правильного анализа таких входных данных.

[![значение UnitPrice измененной строки теперь отформатировано как денежное](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image32.png)](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image31.png)

**Рис. 11**. значение `UnitPrice` измененной строки теперь отформатировано как денежная единица ([щелкните, чтобы просмотреть изображение с полным размером](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image33.png))

## <a name="step-2-prohibitingnull-unitprices"></a>Шаг 2. запрет`NULL UnitPrices`

Хотя база данных настроена на разрешение `NULL` значений в столбце `UnitPrice` таблицы `Products`, может потребоваться запретить пользователям, посещающих эту конкретную страницу, указать значение `NULL` `UnitPrice`. Это значит, что если пользователю не удается ввести `UnitPrice` значение при редактировании строки продукта, вместо сохранения результатов в базе данных нужно отобразить сообщение, информирующее пользователя, что на этой странице для всех измененных продуктов должна быть указана цена.

`GridViewUpdateEventArgs` объект, переданный в обработчик событий `RowUpdating` GridView, содержит свойство `Cancel`, которое, если задано значение `True`, прерывает процесс обновления. Добавим обработчик событий `RowUpdating`, чтобы задать `e.Cancel` для `True` и вывести сообщение с объяснением причины, если значение `UnitPrice` в коллекции `NewValues` имеет значение `Nothing`.

Сначала добавьте веб-элемент управления Label на страницу с именем `MustProvideUnitPriceMessage`. Этот элемент управления Label будет отображаться, если пользователю не удастся указать `UnitPrice` значение при обновлении продукта. Задайте для свойства `Text` метки значение "необходимо указать цену на продукт". Я также создал новый класс CSS в `Styles.css` с именем `Warning` со следующим определением:

[!code-css[Main](examining-the-events-associated-with-inserting-updating-and-deleting-vb/samples/sample5.css)]

Наконец, задайте для свойства `CssClass` метки значение `Warning`. На этом этапе конструктор должен отображать предупреждающее сообщение красным, полужирным курсивом, очень большим размером шрифта над GridView, как показано на рис. 12.

[![Добавление метки над GridView](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image35.png)](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image34.png)

**Рис. 12**. над элементом управления GridView была добавлена метка ([щелкните, чтобы просмотреть изображение с полным размером](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image36.png))

По умолчанию эта метка должна быть скрыта, поэтому установите для свойства `Visible` значение `False` в обработчике событий `Page_Load`:

[!code-vb[Main](examining-the-events-associated-with-inserting-updating-and-deleting-vb/samples/sample6.vb)]

Если пользователь пытается обновить продукт без указания `UnitPrice`, необходимо отменить обновление и отобразить метку предупреждения. Дополните обработчик событий `RowUpdating` GridView следующим образом:

[!code-vb[Main](examining-the-events-associated-with-inserting-updating-and-deleting-vb/samples/sample7.vb)]

Если пользователь пытается сохранить продукт без указания цены, обновление отменяется и выводится полезное сообщение. Хотя база данных (и бизнес-логика) допускает `NULL` `UnitPrice` s, эта конкретная страница ASP.NET не имеет.

[![пользователь не может оставить поле UnitPrice пустым](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image38.png)](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image37.png)

**Рис. 13**. пользователь не может оставить `UnitPrice` пустым ([щелкните, чтобы просмотреть изображение с полным размером](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image39.png))

До сих пор мы увидели, как использовать событие `RowUpdating` GridView для программного изменения значений параметров, присвоенных `UpdateParameters` коллекции ObjectDataSource, а также как полностью отменить процесс обновления. Эти понятия переносятся на элементы управления DetailsView и FormView, а также применяются к вставке и удалению.

Эти задачи также можно выполнить на уровне ObjectDataSource с помощью обработчиков событий для его `Inserting`, `Updating`и `Deleting` событий. Эти события срабатывают перед вызовом связанного метода базового объекта и предоставляют последнюю возможность изменить коллекцию входных параметров или отменить операцию. Обработчики событий для этих трех событий передаются объекту типа [обжектдатасаурцемесодевентаргс](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasourcemethodeventargs(VS.80).aspx) , который имеет два важных свойства:

- [Отмена](https://msdn.microsoft.com/library/system.componentmodel.canceleventargs.cancel(VS.80).aspx), которая, если задано значение `True`, отменяет выполняемую операцию
- [InputParameters](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasourcemethodeventargs.inputparameters(VS.80).aspx)— коллекция `InsertParameters`, `UpdateParameters`или `DeleteParameters`в зависимости от того, предназначен ли обработчик для события `Inserting`, `Updating`или `Deleting`

Чтобы продемонстрировать работу со значениями параметров на уровне ObjectDataSource, включите на странице элемент управления DetailsView, позволяющий пользователям добавить новый продукт. Эта DetailsView будет использоваться для предоставления интерфейса для быстрого добавления нового продукта в базу данных. Чтобы обеспечить единообразный пользовательский интерфейс при добавлении нового продукта, можно позволить пользователю вводить только значения полей `ProductName` и `UnitPrice`. По умолчанию эти значения, которые не передаются в интерфейсе вставки DetailsView, будут установлены в значение `NULL` базы данных. Однако мы можем использовать событие `Inserting` ObjectDataSource для вставки различных значений по умолчанию, как мы увидим чуть позже.

## <a name="step-3-providing-an-interface-to-add-new-products"></a>Шаг 3. предоставление интерфейса для добавления новых продуктов

Перетащите элемент DetailsView с панели элементов в конструктор над элементом управления GridView, очистите его `Height` и `Width` свойства и привяжите его к ObjectDataSource, уже присутствующему на странице. Это приведет к добавлению BoundField или CheckBoxField для каждого из полей продукта. Так как мы хотим использовать эту DetailsView для добавления новых продуктов, необходимо установить флажок Включить вставку из смарт-тега. Однако такой вариант отсутствует, поскольку метод `Insert()` ObjectDataSource не сопоставлен с методом в классе `ProductsBLL` (Помните, что при настройке источника данных для этого сопоставления задано значение (нет).

Чтобы настроить ObjectDataSource, выберите ссылку Настроить источник данных из смарт-тега, запустив мастер. Первый экран позволяет изменить базовый объект, к которому привязан элемент управления ObjectDataSource; Оставьте значение `ProductsBLL`. На следующем экране перечисляются сопоставления методов ObjectDataSource с базовым объектом. Хотя мы явно указали, что методы `Insert()` и `Delete()` не должны сопоставляться ни с одним из методов, при переходе на вкладки вставки и удаления вы увидите, что сопоставление находится там. Это обусловлено тем, что методы `AddProduct` и `DeleteProduct` `ProductsBLL`используют атрибут `DataObjectMethodAttribute`, чтобы указать, что они являются методами по умолчанию для `Insert()` и `Delete()`соответственно. Таким образом, мастер ObjectDataSource выбирает их каждый раз при запуске мастера, если не указано другое значение.

Оставьте `Insert()` метод, указывающий на метод `AddProduct`, но снова установите в раскрывающемся списке вкладки удаление значение (нет).

[![установить в раскрывающемся списке вкладки вставки метод AddProduct](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image41.png)](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image40.png)

**Рис. 14**. выбор метода `AddProduct` в раскрывающемся списке вкладки вставки ([щелкните, чтобы просмотреть изображение с полным размером](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image42.png))

[![установить для раскрывающегося списка вкладки удаления значение (нет)](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image44.png)](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image43.png)

**Рис. 15**. Установка для раскрывающегося списка вкладки удаления значения (нет) ([щелкните, чтобы просмотреть изображение с полным размером](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image45.png))

После внесения этих изменений декларативный синтаксис ObjectDataSource будет расширен для включения коллекции `InsertParameters`, как показано ниже:

[!code-aspx[Main](examining-the-events-associated-with-inserting-updating-and-deleting-vb/samples/sample8.aspx)]

При повторном запуске мастера добавляется свойство `OldValuesParameterFormatString`. Уделите время очистить это свойство, присвоив ему значение по умолчанию (`{0}`) или полностью удалив его из декларативного синтаксиса.

Теперь, когда элемент управления ObjectDataSource предоставляет возможности вставки, в смарт-теге DetailsView будет включен флажок Включить вставку. Вернитесь в конструктор и установите этот флажок. Затем немного очистить элемент DetailsView, чтобы он получил только два BoundFields-`ProductName` и `UnitPrice`-и CommandField. На этом этапе декларативный синтаксис DetailsView должен выглядеть следующим образом:

[!code-aspx[Main](examining-the-events-associated-with-inserting-updating-and-deleting-vb/samples/sample9.aspx)]

На рис. 16 показана эта страница при просмотре в браузере на этом этапе. Как видите, в DetailsView отображается название и цена первого продукта (Chai). Однако мы хотим вставить интерфейс вставки, предоставляющий пользователю возможность быстро добавить новый продукт в базу данных.

[![элемент DetailsView в настоящее время отображается в режиме только для чтения](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image47.png)](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image46.png)

**Рис. 16**. сейчас DetailsView отображается в режиме только для чтения ([щелкните, чтобы просмотреть изображение с полным размером](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image48.png)).

Чтобы отобразить DetailsView в режиме вставки, необходимо задать для свойства `DefaultMode` значение `Inserting`. При первом посещении отображается элемент DetailsView в режиме вставки, после чего он сохраняется после вставки новой записи. Как показано на рис. 17, такой элемент DetailsView предоставляет быстрый интерфейс для добавления новой записи.

[![DetailsView предоставляет интерфейс для быстрого добавления нового продукта.](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image50.png)](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image49.png)

**Рис. 17**. элемент DetailsView предоставляет интерфейс для быстрого добавления нового продукта ([щелкните, чтобы просмотреть изображение с полным размером](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image51.png)).

Когда пользователь вводит название продукта и цену (например, "Acme вода" и 1,99, как показано на рис. 17) и нажимает кнопку "вставить", выполняется обратная передача и начинается процесс вставки, улучшалась в новую запись продукта, добавляемую в базу данных. Элемент управления DetailsView сохраняет свой интерфейс вставки, и GridView автоматически повторно привязывается к своему источнику данных, чтобы включить новый продукт, как показано на рис. 18.

![Продукт](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image52.png)

**Рис. 18**. в базу данных добавлен продукт «Acme».

Хотя элемент управления GridView на рис. 18 не отображает его, поля продукта, отсутствующие в интерфейсе DetailsView `CategoryID`, `SupplierID`, `QuantityPerUnit`и т. д., назначаются `NULL` значениям базы данных. Это можно увидеть, выполнив следующие действия.

1. Переход к обозреватель сервера в Visual Studio
2. Развертывание узла базы данных `NORTHWND.MDF`
3. Щелкните правой кнопкой мыши узел таблицы базы данных `Products`
4. Выбор представления данных таблицы

В результате будут перечислены все записи в таблице `Products`. Как показано на рис. 19, все наши новые столбцы продукта, кроме `ProductID`, `ProductName`и `UnitPrice`, имеют `NULL` значения.

[![полям продуктов, не предоставленным в DetailsView, присваиваются значения NULL](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image54.png)](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image53.png)

**Рис. 19**. полям продуктов, не предоставленным в DetailsView, присваиваются `NULL` значения ([щелкните, чтобы просмотреть изображение с полным размером](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image55.png))

Нам может потребоваться предоставить значение по умолчанию, отличное от `NULL` для одного или нескольких значений этих столбцов, так как `NULL` не является лучшим вариантом по умолчанию или если столбец базы данных не допускает `NULL` s. Для этого мы можем программно задавать значения параметров коллекции `InputParameters` DetailsView. Это назначение можно выполнить либо в обработчике событий для события `ItemInserting` DetailsView, либо в событии `Inserting` ObjectDataSource. Поскольку мы уже рассматривали использование событий предварительного и последующей обработки на уровне веб-элемента управления данными, давайте рассмотрим использование событий ObjectDataSource в этот раз.

## <a name="step-4-assigning-values-to-thecategoryidandsupplieridparameters"></a>Шаг 4. Присвоение значений параметрам`CategoryID`и`SupplierID`

В этом учебнике мы представим, что для нашего приложения при добавлении нового продукта через этот интерфейс ему следует назначить `CategoryID` и `SupplierID` значение 1. Как упоминалось ранее, ObjectDataSource имеет пару событий до и после уровня, которые срабатывают во время процесса изменения данных. Когда вызывается метод `Insert()`, ObjectDataSource сначала создает событие `Inserting`, затем вызывает метод, которому сопоставлен метод `Insert()`, и, наконец, вызывает событие `Inserted`. Обработчик событий `Inserting` предоставляет нам последнюю возможность настроить входные параметры или отменить операцию.

> [!NOTE]
> В реальных приложениях, скорее всего, потребуется либо предоставить пользователю указание категории и поставщика, либо выбрать для них это значение на основе определенных критериев или бизнес-логики (вместо того, чтобы явно выбрать идентификатор 1). В этом примере показано, как программно задать значение входного параметра из события предварительного уровня ObjectDataSource.

Уделите время созданию обработчика событий для события `Inserting` ObjectDataSource. Обратите внимание, что второй входной параметр обработчика событий — это объект типа `ObjectDataSourceMethodEventArgs`, имеющий свойство для доступа к коллекции параметров (`InputParameters`) и свойство для отмены операции (`Cancel`).

[!code-vb[Main](examining-the-events-associated-with-inserting-updating-and-deleting-vb/samples/sample10.vb)]

На этом этапе свойство `InputParameters` содержит коллекцию `InsertParameters` ObjectDataSource со значениями, назначенными из элемента DetailsView. Чтобы изменить значение одного из этих параметров, просто используйте: `e.InputParameters("paramName") = value`. Таким образом, чтобы задать `CategoryID` и `SupplierID` значения 1, настройте обработчик событий `Inserting` так, чтобы он выглядел следующим образом:

[!code-vb[Main](examining-the-events-associated-with-inserting-updating-and-deleting-vb/samples/sample11.vb)]

На этот раз при добавлении нового продукта (например, Acme Soda) для столбцов `CategoryID` и `SupplierID` нового продукта устанавливается значение 1 (см. рис. 20).

[![новые продукты теперь имеют значения CategoryID и КодПоставщика, равные 1](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image57.png)](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image56.png)

**Рис. 20**. новые продукты теперь имеют свои `CategoryID` и `SupplierID` значения 1 ([щелкните, чтобы просмотреть изображение с полным размером](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image58.png))

## <a name="summary"></a>Сводка

Во время процесса редактирования, вставки и удаления веб-элемент управления данными и ObjectDataSource просматривает ряд событий до и после предыдущего уровня. В этом учебнике мы рассмотрели события предварительного уровня и увидели, как их использовать для настройки входных параметров или отмены операции изменения данных в целом как из веб-элемента управления данными, так и из событий ObjectDataSource. В следующем учебном курсе мы рассмотрим создание и использование обработчиков событий для событий последующего уровня.

Поздравляем с программированием!

## <a name="about-the-author"></a>Об авторе

[Скотт Митчелл](http://www.4guysfromrolla.com/ScottMitchell.shtml), автор семи книг по ASP/ASP. NET и основатель [4GuysFromRolla.com](http://www.4guysfromrolla.com), работал с веб-технологиями Майкрософт с 1998. Скотт работает как независимый консультант, преподаватель и модуль записи. Его последняя книга — [*Sams обучать себя ASP.NET 2,0 за 24 часа*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco). Он доступен по адресу [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) или через его блог, который можно найти по адресу [http://ScottOnWriting.NET](http://ScottOnWriting.NET).

## <a name="special-thanks-to"></a>Специальная благодарность

Эта серия руководств была рассмотрена многими полезными рецензентами. Потенциальные рецензенты для этого учебника были основными редакторами и основными рецензентами. Хотите ознакомиться с моими будущими статьями MSDN? Если это так, расположите строку в [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Назад](an-overview-of-inserting-updating-and-deleting-data-vb.md)
> [Вперед](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb.md)
