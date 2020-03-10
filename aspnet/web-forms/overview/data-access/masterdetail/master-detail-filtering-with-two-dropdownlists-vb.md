---
uid: web-forms/overview/data-access/masterdetail/master-detail-filtering-with-two-dropdownlists-vb
title: Фильтрация "основной/подробности" с помощью двух элементов управления DropDownList (VB) | Документация Майкрософт
author: rick-anderson
description: Это руководство расширяет отношение "основной/подробности", добавляя третий слой, используя два элемента управления DropDownList для выбора нужного родителя и бабушке писи...
ms.author: riande
ms.date: 03/31/2010
ms.assetid: 11ae4f64-01ba-4823-95f4-a2fe1f84f7d7
msc.legacyurl: /web-forms/overview/data-access/masterdetail/master-detail-filtering-with-two-dropdownlists-vb
msc.type: authoredcontent
ms.openlocfilehash: 166d6a7664a326361dc2a3f115eddb988cd39d20
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78424296"
---
# <a name="masterdetail-filtering-with-two-dropdownlists-vb"></a>Фильтрация "Основной/подробности" с помощью двух элементов управления DropDownList (VB)

по [Скотт Митчелл](https://twitter.com/ScottOnWriting)

[Скачивание примера приложения](https://download.microsoft.com/download/5/d/7/5d7571fc-d0b7-4798-ad4a-c976c02363ce/ASPNET_Data_Tutorial_8_VB.exe) или [Загрузка PDF-файла](master-detail-filtering-with-two-dropdownlists-vb/_static/datatutorial08vb1.pdf)

> Это руководство расширяет отношение "основной/подробности", добавляя третий слой, используя два элемента управления DropDownList для выбора нужных записей родителей и бабушкх.

## <a name="introduction"></a>Введение

В [предыдущем учебном курсе](master-detail-filtering-with-a-dropdownlist-vb.md) мы рассмотрели, как отобразить простой отчет «основной/подробности» с помощью одного элемента управления DropDownList, заполненного категориями, и элементом управления GridView, отображающим продукты, принадлежащие выбранной категории. Этот шаблон отчета хорошо работает при отображении записей с отношением "один ко многим" и может быть легко расширено для работы в сценариях, включающих несколько связей "один ко многим". Например, система ввода заказов будет иметь таблицы, соответствующие клиентам, заказам и позициям строк заказа. У данного клиента может быть несколько заказов с каждым заказом, состоящим из нескольких элементов. Такие данные могут быть представлены пользователю с двумя элементов управления DropDownList и GridView. Первый DropDownList будет иметь элемент списка для каждого клиента в базе данных со вторым содержимым заказами, размещенными выбранным клиентом. Элемент управления GridView будет перечислять элементы строк из выбранного заказа.

Хотя база данных Northwind включает в себя каноническую информацию о клиенте/заказе или заказе в своих `Customers`, `Orders`и `Order Details` таблицах, эти таблицы не фиксируются в нашей архитектуре. Тем не менее, мы можем проиллюстрировать использование двух зависимых элементов управления DropDownList. В первом списке DropDownList будут перечислены категории и вторая продукция, относящаяся к выбранной категории. Затем DetailsView будет выводить сведения о выбранном продукте.

## <a name="step-1-creating-and-populating-the-categories-dropdownlist"></a>Шаг 1. Создание и заполнение элемента DropDownList в категориях

Первая цель — добавить DropDownList, в котором перечислены категории. Эти действия были подробно рассмотрены в предыдущем руководстве, но здесь приведены сводные сведения о полноте.

Откройте страницу `MasterDetailsDetails.aspx` в папке `Filtering`, добавьте DropDownList на страницу, задайте для свойства `ID` значение `Categories`, а затем щелкните ссылку Настроить источник данных в своем смарт-теге. В мастере настройки источника данных выберите Добавление нового источника данных.

[![добавить новый источник данных для DropDownList](master-detail-filtering-with-two-dropdownlists-vb/_static/image2.png)](master-detail-filtering-with-two-dropdownlists-vb/_static/image1.png)

**Рис. 1**. Добавление нового источника данных для DropDownList ([щелкните, чтобы просмотреть изображение с полным размером](master-detail-filtering-with-two-dropdownlists-vb/_static/image3.png))

Новый источник данных должен, естественно, быть ObjectDataSource. Назовите этот новый элемент ObjectDataSource `CategoriesDataSource` и вызовите метод `GetCategories()` объекта `CategoriesBLL`.

[![выбрать использование класса CategoriesBLL](master-detail-filtering-with-two-dropdownlists-vb/_static/image5.png)](master-detail-filtering-with-two-dropdownlists-vb/_static/image4.png)

**Рис. 2**. Выбор использования класса `CategoriesBLL` ([щелкните, чтобы просмотреть изображение с полным размером](master-detail-filtering-with-two-dropdownlists-vb/_static/image6.png))

[![настроить ObjectDataSource для использования метода-Categories ()](master-detail-filtering-with-two-dropdownlists-vb/_static/image8.png)](master-detail-filtering-with-two-dropdownlists-vb/_static/image7.png)

**Рис. 3**. Настройка ObjectDataSource для использования метода `GetCategories()` ([щелкните, чтобы просмотреть изображение с полным размером](master-detail-filtering-with-two-dropdownlists-vb/_static/image9.png))

После настройки ObjectDataSource необходимо указать, какое поле источника данных должно отображаться в элементе управления DropDownList `Categories` и какое значение должно быть настроено в качестве значения для элемента списка. Задайте поле `CategoryName` как отображаемое и `CategoryID` в качестве значения для каждого элемента списка.

[![отображать поле CategoryName и использовать CategoryID в качестве значения](master-detail-filtering-with-two-dropdownlists-vb/_static/image11.png)](master-detail-filtering-with-two-dropdownlists-vb/_static/image10.png)

**Рис. 4**. отображение поля `CategoryName` в DropDownList и использование `CategoryID` в качестве значения ([щелкните, чтобы просмотреть изображение с полным размером](master-detail-filtering-with-two-dropdownlists-vb/_static/image12.png))

На этом этапе у нас есть элемент управления DropDownList (`Categories`), который заполняется записями из `Categories` таблицы. Когда пользователь выбирает новую категорию из DropDownList, необходимо выполнить обратную передачу, чтобы обновить DropDownList продукта, который мы создадим на шаге 2. Поэтому установите флажок Включить автообратную передачу из смарт-тега `categories` DropDownList.

[![включить автообратную передачу для DropDownList категорий](master-detail-filtering-with-two-dropdownlists-vb/_static/image14.png)](master-detail-filtering-with-two-dropdownlists-vb/_static/image13.png)

**Рис. 5**. Включение автообратной передачи для `Categories` DropDownList ([щелкните, чтобы просмотреть изображение с полным размером](master-detail-filtering-with-two-dropdownlists-vb/_static/image15.png))

## <a name="step-2-displaying-the-selected-categorys-products-in-a-second-dropdownlist"></a>Шаг 2. Отображение продуктов выбранной категории во втором элементе DropDownList

После завершения работы с DropDownList `Categories` наш следующий шаг — отображение элемента DropDownList для продуктов, принадлежащих выбранной категории. Для этого добавьте в страницу другое окно DropDownList с именем `ProductsByCategory`. Как и в `Categories` DropDownList, создайте новый элемент ObjectDataSource для `ProductsByCategory` DropDownList с именем `ProductsByCategoryDataSource`.

[![добавить новый источник данных для DropDownList ProductsByCategory](master-detail-filtering-with-two-dropdownlists-vb/_static/image17.png)](master-detail-filtering-with-two-dropdownlists-vb/_static/image16.png)

**Рис. 6**. Добавление нового источника данных для элемента DropDownList `ProductsByCategory` ([щелкните, чтобы просмотреть изображение с полным размером](master-detail-filtering-with-two-dropdownlists-vb/_static/image18.png))

[![создать новый элемент управления ObjectDataSource с именем Продуктсбикатегоридатасаурце](master-detail-filtering-with-two-dropdownlists-vb/_static/image20.png)](master-detail-filtering-with-two-dropdownlists-vb/_static/image19.png)

**Рис. 7**. Создание нового элемента управления ObjectDataSource с именем `ProductsByCategoryDataSource` ([щелкните, чтобы просмотреть изображение с полным размером](master-detail-filtering-with-two-dropdownlists-vb/_static/image21.png))

Поскольку `ProductsByCategory` DropDownList должны отображать только те продукты, которые относятся к выбранной категории, элемент ObjectDataSource должен вызвать метод `GetProductsByCategoryID(categoryID)` из объекта `ProductsBLL`.

[![выбрать использование класса ProductsBLL](master-detail-filtering-with-two-dropdownlists-vb/_static/image23.png)](master-detail-filtering-with-two-dropdownlists-vb/_static/image22.png)

**Рис. 8**. Выбор использования класса `ProductsBLL` ([щелкните, чтобы просмотреть изображение с полным размером](master-detail-filtering-with-two-dropdownlists-vb/_static/image24.png))

[![настроить ObjectDataSource для использования метода GetProductsByCategoryID (categoryID)](master-detail-filtering-with-two-dropdownlists-vb/_static/image26.png)](master-detail-filtering-with-two-dropdownlists-vb/_static/image25.png)

**Рис. 9**. Настройка ObjectDataSource для использования метода `GetProductsByCategoryID(categoryID)` ([щелкните, чтобы просмотреть изображение с полным размером](master-detail-filtering-with-two-dropdownlists-vb/_static/image27.png))

На последнем шаге мастера необходимо указать значение параметра *`categoryID`* . Присвойте этот параметр выбранному элементу из `Categories` DropDownList.

[![извлечь значение параметра categoryID из DropDownList категорий](master-detail-filtering-with-two-dropdownlists-vb/_static/image29.png)](master-detail-filtering-with-two-dropdownlists-vb/_static/image28.png)

**Рис. 10**. извлечение значения *`categoryID`* параметра из `Categories` DropDownList ([щелкните, чтобы просмотреть изображение с полным размером](master-detail-filtering-with-two-dropdownlists-vb/_static/image30.png))

После настройки ObjectDataSource остается только указать поля источника данных, используемые для вывода и значения элементов DropDownList. Отобразите поле `ProductName` и используйте в качестве значения поле `ProductID`.

[![указать поля источника данных, используемые для свойств Text и Value элемента списка DropDownList](master-detail-filtering-with-two-dropdownlists-vb/_static/image32.png)](master-detail-filtering-with-two-dropdownlists-vb/_static/image31.png)

**Рис. 11**. Указание полей источника данных, используемых для свойств `ListItem` s "`Text` и `Value` элемента DropDownList ([щелкните, чтобы просмотреть изображение с полным размером](master-detail-filtering-with-two-dropdownlists-vb/_static/image33.png))

С помощью элемента управления DropDownList и `ProductsByCategory`, настроенного на нашей странице, будут отображены два элементов управления DropDownList: Первая выводит все категории, а вторая — список продуктов, принадлежащих выбранной категории. Когда пользователь выбирает новую категорию из первого элемента DropDownList, будет предприниматься обратная передача, а второй элемент DropDownList будет привязан повторно, отображая продукты, принадлежащие к только что выбранной категории. На рисунках 12 и 13 показаны `MasterDetailsDetails.aspx` в действии при просмотре в браузере.

[![при первом посещении страницы выбирается Категория «напитки»](master-detail-filtering-with-two-dropdownlists-vb/_static/image35.png)](master-detail-filtering-with-two-dropdownlists-vb/_static/image34.png)

**Рис. 12**. при первом посещении страницы выбирается Категория «напитки» ([щелкните, чтобы просмотреть изображение с полным размером](master-detail-filtering-with-two-dropdownlists-vb/_static/image36.png)).

[![выборе другой категории отображаются продукты новой категории.](master-detail-filtering-with-two-dropdownlists-vb/_static/image38.png)](master-detail-filtering-with-two-dropdownlists-vb/_static/image37.png)

**Рис. 13**. Выбор другой категории отображает продукты новой категории ([щелкните, чтобы просмотреть изображение с полным размером](master-detail-filtering-with-two-dropdownlists-vb/_static/image39.png))

В настоящее время `productsByCategory` DropDownList, при изменении, *не вызывает* обратную передачу. Однако мы хотим, чтобы обратная передача выполнялась после добавления элемента DetailsView для вывода сведений о выбранном продукте (шаг 3). Поэтому установите флажок Включить автообратную передачу из смарт-тега `productsByCategory` DropDownList.

[![включить функцию автообратной передачи для DropDownList productsByCategory](master-detail-filtering-with-two-dropdownlists-vb/_static/image41.png)](master-detail-filtering-with-two-dropdownlists-vb/_static/image40.png)

**Рис. 14**. Включение функции автообратной передачи для элемента DropDownList `productsByCategory` ([щелкните, чтобы просмотреть изображение с полным размером](master-detail-filtering-with-two-dropdownlists-vb/_static/image42.png))

## <a name="step-3-using-a-detailsview-to-display-details-for-the-selected-product"></a>Шаг 3. Отображение сведений о выбранном продукте с помощью элемента DetailsView

Последним шагом является отображение сведений о выбранном продукте в элементе DetailsView. Для этого добавьте DetailsView на страницу, задайте для свойства `ID` значение `ProductDetails`и создайте для него новый элемент управления ObjectDataSource. Настройте этот элемент ObjectDataSource, чтобы извлечь данные из метода `GetProductByProductID(productID)` класса `ProductsBLL`, используя выбранное значение `ProductsByCategory` DropDownList для значения параметра *`productID`* .

[![выбрать использование класса ProductsBLL](master-detail-filtering-with-two-dropdownlists-vb/_static/image44.png)](master-detail-filtering-with-two-dropdownlists-vb/_static/image43.png)

**Рис. 15**. Выбор использования класса `ProductsBLL` ([щелкните, чтобы просмотреть изображение с полным размером](master-detail-filtering-with-two-dropdownlists-vb/_static/image45.png))

[![настроить ObjectDataSource для использования метода Жетпродуктбипродуктид (productID)](master-detail-filtering-with-two-dropdownlists-vb/_static/image47.png)](master-detail-filtering-with-two-dropdownlists-vb/_static/image46.png)

**Рис. 16**. Настройка ObjectDataSource для использования метода `GetProductByProductID(productID)` ([щелкните, чтобы просмотреть изображение с полным размером](master-detail-filtering-with-two-dropdownlists-vb/_static/image48.png))

[![извлечь значение параметра productID из DropDownList ProductsByCategory](master-detail-filtering-with-two-dropdownlists-vb/_static/image50.png)](master-detail-filtering-with-two-dropdownlists-vb/_static/image49.png)

**Рис. 17**. извлечение значения *`productID`* параметра из `ProductsByCategory` DropDownList ([щелкните, чтобы просмотреть изображение с полным размером](master-detail-filtering-with-two-dropdownlists-vb/_static/image51.png))

Можно выбрать отображение любого из доступных полей в `ProductDetails` DetailsView. Я решил удалить поля `ProductID`, `SupplierID`и `CategoryID`, а также изменить порядок и отформатировать оставшиеся поля. Кроме того, я очистил свойства `Height` и `Width` DetailsView, позволяя элементу DetailsView расшириться до ширины, необходимой для наилучшего представления данных, а не ограничиваться заданным размером. Полная разметка показана ниже:

[!code-aspx[Main](master-detail-filtering-with-two-dropdownlists-vb/samples/sample1.aspx)]

Уделите немного времени, чтобы испытать страницу `MasterDetailsDetails.aspx` в браузере. На первый взгляд может показаться, что все работает надлежащим образом, но есть несложная проблема. При выборе новой категории `ProductsByCategory` DropDownList обновляется, чтобы включить эти продукты для выбранной категории, но `ProductDetails` DetailsView продолжает отображать предыдущую информацию о продукте. Элемент DetailsView обновляется при выборе другого продукта для выбранной категории. Более того, при тщательном тестировании вы обнаружите, что если постоянно выбрать новые категории (например, выбрать напитки из `Categories` DropDownList, затем «специи», а затем Конфектионс), то при каждом выборе категории DetailsView будет обновлено `ProductDetails`.

Чтобы помочь конкретизировать эту проблему, давайте взглянем на конкретный пример. При первом посещении страницы выбирается Категория «напитки», а связанные продукты загружаются в `ProductsByCategory` DropDownList. Chai — это выбранный продукт, и его сведения отображаются в `ProductDetails` DetailsView, как показано на рис. 18.

[![сведения о выбранном продукте отображаются в элементе DetailsView](master-detail-filtering-with-two-dropdownlists-vb/_static/image53.png)](master-detail-filtering-with-two-dropdownlists-vb/_static/image52.png)

**Рис. 18**. сведения о выбранном продукте отображаются в элементе DetailsView ([щелкните, чтобы просмотреть изображение с полным размером](master-detail-filtering-with-two-dropdownlists-vb/_static/image54.png))

Если вы изменяете выбор категории с "Напиткиs" на «специи», происходит обратная передача, и `ProductsByCategory` DropDownList обновляется соответствующим образом, но элемент DetailsView по-прежнему отображает сведения для Chai.

[![сведения о выбранном ранее продукте по-прежнему отображаются](master-detail-filtering-with-two-dropdownlists-vb/_static/image56.png)](master-detail-filtering-with-two-dropdownlists-vb/_static/image55.png)

**Рис. 19**. сведения о выбранном ранее продукте по-прежнему отображаются ([щелкните, чтобы просмотреть изображение с полным размером](master-detail-filtering-with-two-dropdownlists-vb/_static/image57.png))

При выборе нового продукта из списка элемент DetailsView обновляется, как и ожидалось. Если после изменения продукта выбрать новую категорию, то DetailsView снова не обновится. Однако если вместо выбора нового продукта выбрана новая категория, элемент DetailsView обновится. Что происходит в мире?

Проблема — это проблема времени в жизненном цикле страницы. Каждый раз, когда запрашивается страница, она проходит ряд шагов в качестве ее отрисовки. В одном из этих действий элементы управления ObjectDataSource проверяют, изменились ли какие либо их `SelectParameters` значения. Если да, то веб-элемент управления данными, привязанный к ObjectDataSource, знает, что ему нужно обновить его отображение. Например, если выбрана новая категория, `ProductsByCategoryDataSource` ObjectDataSource обнаруживает, что значения ее параметров изменились и `ProductsByCategory` DropDownList выполняет повторную привязку, получая продукты для выбранной категории.

Проблема, которая возникает в этой ситуации, заключается в том, что точка жизненного цикла страницы, которая проверяется на предмет измененных параметров, выполняется *перед* повторной привязкой связанных веб-элементов управления данными. Поэтому при выборе новой категории `ProductsByCategoryDataSource` ObjectDataSource обнаруживает изменение значения его параметра. Тем не менее, ObjectDataSource, используемый `ProductDetails` DetailsView, не запомните никаких изменений, так как `ProductsByCategory` DropDownList еще не был привязан. Позднее в жизненном цикле `ProductsByCategory` DropDownList повторно привязывается к элементу ObjectDataSource, заменяя продукты для вновь выбранной категории. Хотя значение DropDownList `ProductsByCategory` изменилось, элемент управления ObjectDataSource `ProductDetails` DetailsView уже выполнил проверку значения параметра; Таким образом, элемент DetailsView отображает свои предыдущие результаты. Это взаимодействие показано на рис. 20.

[![значение ProductsByCategory DropDownList изменяется после того, как ObjectDataSource Продуктдетаилс DetailsView проверяет наличие изменений](master-detail-filtering-with-two-dropdownlists-vb/_static/image59.png)](master-detail-filtering-with-two-dropdownlists-vb/_static/image58.png)

**Рис. 20**. значение `ProductsByCategory` DropDownList изменяется после того, как элемент управления ObjectDataSource `ProductDetails` DetailsView проверяет наличие изменений ([щелкните, чтобы просмотреть изображение с полным размером](master-detail-filtering-with-two-dropdownlists-vb/_static/image60.png))

Для устранения этой проблемы необходимо явно выполнить привязку `ProductDetails` DetailsView после привязки `ProductsByCategory` DropDownList. Это можно сделать, вызвав метод `DataBind()` `ProductDetails` DetailsView, когда срабатывает событие `DataBound` `ProductsByCategory` DropDownList. Добавьте следующий код обработчика событий в класс кода программной части `MasterDetailsDetails.aspx` страницы (см. "[программное задание значений параметров ObjectDataSource](../basic-reporting/programmatically-setting-the-objectdatasource-s-parameter-values-cs.md)" для обсуждения добавления обработчика событий):

[!code-vb[Main](master-detail-filtering-with-two-dropdownlists-vb/samples/sample2.vb)]

После того как был добавлен явный вызов метода `DataBind()` `ProductDetails` DetailsView, учебник работает правильно. На рис. 21 показано, как это изменение исправлено в нашей предыдущей проблеме.

[![Продуктдетаилс DetailsView явно обновляется при срабатывании события привязки к данным DropDownList ProductsByCategory](master-detail-filtering-with-two-dropdownlists-vb/_static/image62.png)](master-detail-filtering-with-two-dropdownlists-vb/_static/image61.png)

**Рисунок 21**. `ProductDetails` DetailsView явно обновляется при срабатывании события `DataBound` `ProductsByCategory` DropDownList ([щелкните, чтобы просмотреть изображение с полным размером](master-detail-filtering-with-two-dropdownlists-vb/_static/image63.png)).

## <a name="summary"></a>Сводка

Элемент DropDownList выступает в качестве идеального элемента пользовательского интерфейса для отчетов «основной/подробности», где существует связь «один ко многим» между главной и подробной записями. В предыдущем учебном курсе мы увидели, как использовать одно DropDownList для фильтрации продуктов, отображаемых выбранной категорией. В этом руководстве мы заменили элемент управления GridView для продуктов элементом управления DropDownList и используем DetailsView для просмотра сведений о выбранном продукте. Концепции, обсуждаемые в этом руководстве, можно легко расширить на модели данных, включающие в себя несколько связей «один ко многим», таких как клиенты, заказы и элементы заказов. В целом, всегда можно добавить элемент DropDownList для каждой из сущностей «один» в связях «один ко многим».

Поздравляем с программированием!

## <a name="about-the-author"></a>Об авторе

[Скотт Митчелл](http://www.4guysfromrolla.com/ScottMitchell.shtml), автор семи книг по ASP/ASP. NET и основатель [4GuysFromRolla.com](http://www.4guysfromrolla.com), работал с веб-технологиями Майкрософт с 1998. Скотт работает как независимый консультант, преподаватель и модуль записи. Его последняя книга — [*Sams обучать себя ASP.NET 2,0 за 24 часа*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco). Он доступен по адресу [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) или через его блог, который можно найти по адресу [http://ScottOnWriting.NET](http://ScottOnWriting.NET).

## <a name="special-thanks-to"></a>Специальная благодарность

Эта серия руководств была рассмотрена многими полезными рецензентами. Специалист по интересу для этого руководства был Хилтон Гизнау. Хотите ознакомиться с моими будущими статьями MSDN? Если это так, расположите строку в [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Назад](master-detail-filtering-with-a-dropdownlist-vb.md)
> [Вперед](master-detail-filtering-across-two-pages-vb.md)
