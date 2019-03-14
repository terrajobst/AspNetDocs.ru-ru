---
uid: web-forms/overview/data-access/paging-and-sorting-with-the-datalist-and-repeater/paging-report-data-in-a-datalist-or-repeater-control-cs
title: Разбиение по страницам данных отчета в элементе управления DataList или Repeater (C#) | Документация Майкрософт
author: rick-anderson
description: При ни DataList, ни элемент управления Repeater предложение автоматическое разбиение по страницам или сортировки поддержки этом руководстве показано, как для добавления поддержки разбиения по страницам для элементов управления DataList или Repeater...
ms.author: riande
ms.date: 11/13/2006
ms.assetid: e8e0809b-25c4-4c3b-8d12-9a17048148ae
msc.legacyurl: /web-forms/overview/data-access/paging-and-sorting-with-the-datalist-and-repeater/paging-report-data-in-a-datalist-or-repeater-control-cs
msc.type: authoredcontent
ms.openlocfilehash: 4212b7bff41d76eaef18d638cf28441b50061159
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57024631"
---
<a name="paging-report-data-in-a-datalist-or-repeater-control-c"></a>Разбиение по страницам данных отчета в элементе управления DataList или Repeater (C#)
====================
по [Скотт Митчелл](https://twitter.com/ScottOnWriting)

[Скачайте пример приложения](http://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_44_CS.exe) или [скачать PDF](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/datatutorial44cs1.pdf)

> Хотя ни DataList, ни элемент управления Repeater предложения, автоматическое разбиение по страницам или сортировки поддержки в этом руководстве показано, как добавление поддержки разбиения по страницам элемента управления DataList или Repeater, что гораздо более гибкие разбиение по страницам и данных отображения интерфейсов.


## <a name="introduction"></a>Вступление

Разбиение по страницам и сортировка – две часто встречающиеся функции отображения данных в интерактивном приложении. Например при поиске книг по ASP.NET в Интернет-магазине, могут существовать сотни книг, но отчет с результатами поиска только десять совпадениями на одной странице. Кроме того результаты можно отсортировать по title, цена, количество страниц, имя автора и т. д. Как уже говорилось в [разбиение по страницам и сортировка данных отчета](../paging-and-sorting/paging-and-sorting-report-data-cs.md) учебник, элементы управления GridView, DetailsView и FormView, имеют встроенную поддержку разбиения по страницам, можно включить на уровне такта флажок. GridView также обеспечения поддержки сортировки.

К сожалению ни элемент управления DataList, ни элемент управления Repeater предлагают автоматическое разбиение по страницам или сортировки поддержки. В этом руководстве мы рассмотрим, как добавить поддержку разбиения по страницам для элементов управления DataList или Repeater. Мы вручную необходимо создать интерфейс разбиения по страницам, на соответствующую страницу записей и помните, посещение которого выполняется во время обратной передачи страницы. Хотя это требует больше времени и кода по сравнению с GridView, DetailsView и FormView, DataList и Repeater позволяют гораздо более гибкие разбиение по страницам и данных отображения интерфейсов.

> [!NOTE]
> Это руководство посвящено исключительно разбиения на страницы. В следующем учебном курсе мы обратим наше внимание на возможности сортировки.


## <a name="step-1-adding-the-paging-and-sorting-tutorial-web-pages"></a>Шаг 1. Добавление разбиения по страницам и сортировка учебника веб-страниц

Прежде чем приступать к этом руководстве, позволяют s сначала Отвлекитесь и добавим страницы ASP.NET, которые потребуются для этого учебника и еще один. Начнем с создания новой папки в проект с именем `PagingSortingDataListRepeater`. Добавьте следующие пять страниц ASP.NET в этой папке, в которых настроено использование главной страницы `Site.master`:

- `Default.aspx`
- `Paging.aspx`
- `Sorting.aspx`
- `SortingWithDefaultPaging.aspx`
- `SortingWithCustomPaging.aspx`


![Создайте папку PagingSortingDataListRepeater и добавление страниц учебника по ASP.NET](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image1.png)

**Рис. 1**: Создание `PagingSortingDataListRepeater` папки и добавление страниц учебника по ASP.NET


Затем откройте `Default.aspx` страницы и перетащите `SectionLevelTutorialListing.ascx` пользовательского элемента управления с `UserControls` папку в область конструктора. Данный пользовательский элемент управления, созданный в учебном курсе [главные страницы и структуру переходов узла](../introduction/master-pages-and-site-navigation-cs.md) , просматривает карту узла и отображает руководства, имеющиеся в данном разделе, в виде маркированного списка.


[![Добавление элемента управления Sectionleveltutoriallisting.ascx к странице Default.aspx](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image3.png)](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image2.png)

**Рис. 2**: Добавить `SectionLevelTutorialListing.ascx` для пользовательского элемента управления `Default.aspx` ([Просмотр полноразмерного изображения](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image4.png))


Чтобы в маркированном списке отображались учебные курсы, которые будут созданы и разбиению на страницы, необходимо добавить их в карту узла. Откройте `Web.sitemap` файл и добавьте следующую разметку после изменение и удаление с помощью разметки узла карты веб DataList:


[!code-xml[Main](paging-report-data-in-a-datalist-or-repeater-control-cs/samples/sample1.xml)]


![Обновление карты узла для добавления новых страниц ASP.NET](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image5.png)

**Рис. 3**: Обновление карты узла для добавления новых страниц ASP.NET


## <a name="a-review-of-paging"></a>Обзор разбиения на страницы

В предыдущих учебных курсах мы узнали, как просматривать данные в элементах управления GridView, DetailsView и FormView. Эти три элемента управления предоставляют простую форму разбиения на страницы вызывается *разбиение по страницам по умолчанию* , можно реализовать, просто проверив параметр Включить разбиение по страницам в смарт-теге элемента управления s. С разбиением на страницы по умолчанию, при каждом запросе страницы данных, либо на первой странице посетите или когда пользователь переходит на другую страницу данных GridView, DetailsView, или элемента управления FormView повторно запрашивает *все* данных из Элемент управления ObjectDataSource. Он затем фрагменты определенного набора записей, отображаемых Запрошенный индекс страницы и количество записей, отображаемых на одной странице. Мы рассмотрели разбиение по страницам по умолчанию, подробно [разбиение по страницам и сортировка данных отчета](../paging-and-sorting/paging-and-sorting-report-data-cs.md) руководства.

Так как по страницам по умолчанию повторно запрашивает все записи для каждой страницы, нецелесообразно при работе с большими объемами данных. Например представьте разбиение по страницам 50 000 записей с размером страницы из 10. Каждый раз, когда пользователь переходит на новую страницу, все 50 000 записей должны извлекаться из базы данных, несмотря на то, что отображаются только десять из них.

*Пользовательское разбиение по страницам* решает устранить проблемы с производительностью разбиения на страницы по умолчанию, взяв только точные подмножества записей, отображаемых на запрашиваемой странице. При реализации пользовательского разбиения по страницам, мы должны написать SQL-запрос, возвращающий эффективно правильного набора записей. Мы рассмотрели создание такого запроса с помощью SQL Server 2005 s новый [ `ROW_NUMBER()` ключевое слово](http://www.4guysfromrolla.com/webtech/010406-1.shtml) обратно в [эффективного разбиения на страницы через больших объемов данных](../paging-and-sorting/efficiently-paging-through-large-amounts-of-data-cs.md) руководства.

Реализовать разбиение по страницам по умолчанию в элементах управления DataList или Repeater, мы используем [ `PagedDataSource` класс](https://msdn.microsoft.com/library/system.web.ui.webcontrols.pageddatasource.aspx) как оболочка `ProductsDataTable` страниц, содержимое. `PagedDataSource` Класс имеет `DataSource` свойство, которое можно назначить любой перечисляемый объект и [ `PageSize` ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.pageddatasource.pagesize.aspx) и [ `CurrentPageIndex` ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.pageddatasource.currentpageindex.aspx) свойств, которые указывают, сколько записей следует Показать на одной странице и индекс текущей страницы. После настройки этих свойств `PagedDataSource` можно использовать в качестве источника данных каких-либо данных веб-элемента управления. `PagedDataSource`, При перечислении, будет возвращать только соответствующее подмножество записей из его внутреннее `DataSource` на основе `PageSize` и `CurrentPageIndex` свойства. Рис. 4 показаны функциональные возможности `PagedDataSource` класса.


![PagedDataSource упаковывает перечисляемый объект с возможностью разбивки на страницы интерфейсом](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image6.png)

**Рис. 4**: `PagedDataSource` Упаковывает перечисляемый объект с возможностью разбивки на страницы интерфейсом


`PagedDataSource` Объект может быть создан и настроен непосредственно из уровня бизнес-логики и привязан к элементе управления DataList или Repeater через элемент управления ObjectDataSource, или можно создать и настроить непосредственно в класс фонового кода страницы s ASP.NET. Если используется второй подход, мы отказ от использования ObjectDataSource и вместо этого программной привязки разбитых на страницы данных в DataList или Repeater.

`PagedDataSource` Объект также имеет свойства для поддержки пользовательского разбиения по страницам. Тем не менее, мы можно обойти с помощью `PagedDataSource` для пользовательского разбиения по страницам, так как у нас уже есть методы BLL `ProductsBLL` классов, предназначенных для пользовательского разбиения по страницам, которые возвращают точные записи для отображения.

В этом руководстве мы рассмотрим реализация разбиения по страницам по умолчанию в элементе управления DataList, добавив новый метод для `ProductsBLL` класс, который возвращает соответствующим образом настроенная `PagedDataSource` объекта. В следующем учебном курсе будет показано, как пользовательское разбиение по страницам.

## <a name="step-2-adding-a-default-paging-method-in-the-business-logic-layer"></a>Шаг 2. Добавление метода разбиения по страницам по умолчанию на уровне бизнес-логики

`ProductsBLL` Класс в настоящее время имеет метод для возврата всей информации о продукте `GetProducts()` и один для возвращения определенного подмножества продуктов в начальный индекс `GetProductsPaged(startRowIndex, maximumRows)`. С разбиением на страницы по умолчанию, GridView, DetailsView и FormView элементы управления используют все `GetProducts()` метод для получения всех продуктов, но при использовании `PagedDataSource` внутренне, чтобы отобразить только нужное подмножество записей. Выполнить репликацию этой функциональности с помощью элементов управления DataList и Repeater, можно создать новый метод в BLL, которая имитирует такое поведение.

Добавление метода для `ProductsBLL` класс с именем `GetProductsAsPagedDataSource` , принимает два целочисленных параметра:

- `pageIndex` индекс страницы для отображения, индексируются с нуля, и
- `pageSize` число записей, отображаемых на одной странице.

`GetProductsAsPagedDataSource` начинается с получения *все* записи из `GetProducts()`. Затем он создает `PagedDataSource` объекта, присвоив его `CurrentPageIndex` и `PageSize` свойства к значениям переданного `pageIndex` и `pageSize` параметров. Метод завершается, возвращая соответствующую настройку `PagedDataSource`:


[!code-csharp[Main](paging-report-data-in-a-datalist-or-repeater-control-cs/samples/sample2.cs)]

## <a name="step-3-displaying-product-information-in-a-datalist-using-default-paging"></a>Шаг 3. Отображение информации о продукте в элементе управления DataList, с разбиением на страницы по умолчанию

С помощью `GetProductsAsPagedDataSource` метода, добавленного к `ProductsBLL` класса, теперь можно создать элемент управления DataList или Repeater, обеспечивающая разбиение по страницам по умолчанию. Сначала откройте `Paging.aspx` странице в `PagingSortingDataListRepeater` папки и перетащите элемент управления DataList из инструментария в конструктор, установив DataList s `ID` свойства `ProductsDefaultPaging`. В смарт-теге элемента управления DataList s, создайте новый ObjectDataSource, именуемый `ProductsDefaultPagingDataSource` и настройте его таким образом, чтобы он извлекает данные с помощью `GetProductsAsPagedDataSource` метод.


[![Создание нового ObjectDataSource и настроить его для использования () GetProductsAsPagedDataSource метод](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image8.png)](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image7.png)

**Рис. 5**: Создание нового ObjectDataSource и настройте его для использования `GetProductsAsPagedDataSource` `()` метод ([Просмотр полноразмерного изображения](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image9.png))


Установите раскрывающиеся списки в UPDATE, INSERT и удаление вкладок (нет).


[![Установите раскрывающиеся списки в UPDATE, INSERT и удаление вкладок (нет)](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image11.png)](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image10.png)

**Рис. 6**: Установите раскрывающиеся списки в UPDATE, INSERT и удаление вкладок (нет) ([Просмотр полноразмерного изображения](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image12.png))


Так как `GetProductsAsPagedDataSource` метод ожидает, что два входных параметра, предлагает указать источник этих значений параметров.

Индекс страницы и значения размера страниц должны сохраняться во время обратной передачи. Они могут храниться в состоянии представления, сохраняются в строку запроса, хранящихся в переменных сеанса или сохраненных с помощью некоторые другие методики. В этом руководстве мы будем использовать строку запроса, который имеет преимущество, позволяя определенной страницы данных в закладки.

В частности, используйте pageIndex поля строки запроса и pageSize для `pageIndex` и `pageSize` параметров, соответственно (см. рис. 7). Отвлекитесь и задать значения по умолчанию для этих параметров, как значения строки запроса, выиграл t присутствовать при первом посещении этой странице. Для `pageIndex`, значение по умолчанию равно 0 (откроется первая страница данных) и `pageSize` s значение по умолчанию для 4.


[![Использовать строку запроса в качестве источника для параметров pageIndex и pageSize](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image14.png)](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image13.png)

**Рис. 7**: Использовать строку запроса в качестве источника для `pageIndex` и `pageSize` параметров ([Просмотр полноразмерного изображения](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image15.png))


После настройки ObjectDataSource, Visual Studio автоматически создает `ItemTemplate` элемента управления DataList. Настройка `ItemTemplate` , чтобы были показаны только название продукта s, категорию и поставщика. Также задайте DataList s `RepeatColumns` значение 2, его `Width` 100% и его `ItemStyle` s `Width` 50%. Эти параметры ширины предоставит равные интервалы для двух столбцов.

После внесения этих изменений разметка s элементов управления DataList и ObjectDataSource должна выглядеть следующим образом:


[!code-aspx[Main](paging-report-data-in-a-datalist-or-repeater-control-cs/samples/sample3.aspx)]

> [!NOTE]
> Так как мы не выполняете любое обновление или удалить функциональные возможности в этом руководстве, можно отключить состояние представления элемента управления DataList s для уменьшения размера отображаемой страницы.


При первоначальном просмотре страницы через браузер, ни `pageIndex` , ни `pageSize` предоставляются параметры строки запроса. Таким образом используются значения по умолчанию 0 и 4. Как показано на рис. 8, в результате элемент управления DataList, отображаются первые четыре продукты.


[![Перечислены четыре первых продуктов](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image17.png)](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image16.png)

**Рис. 8**: Перечислены четыре первых продуктов ([Просмотр полноразмерного изображения](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image18.png))


Без интерфейс разбиения по страницам, там s в настоящее время не просто означает, что пользователь может перейти на вторую страницу данных. Мы создадим интерфейс разбиения по страницам на шаге 4. Сейчас, разбиение на страницы только можно, задав критерии разбиения на страницы в строке запроса. Например, чтобы просмотреть на второй странице, измените URL-адрес в адресной строке браузера s из `Paging.aspx` для `Paging.aspx?pageIndex=2` и нажмите клавишу ВВОД. В результате второй странице отображения данных (см. рис. 9).


[![Откроется вторая страница данных](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image20.png)](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image19.png)

**Рис. 9**: Откроется вторая страница данных ([Просмотр полноразмерного изображения](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image21.png))


## <a name="step-4-creating-the-paging-interface"></a>Шаг 4. Создание интерфейса разбиения по страницам

Существует множество различных интерфейсов разбиение по страницам, которые могут быть реализованы. Эти элементы управления GridView, DetailsView и FormView обеспечивают четыре разных интерфейсов для выбора одного из:

- **Следующий, предыдущий** пользователи могут перемещать одну страницу за раз, к следующему или предыдущему сообщению.
- **Далее, назад, первой, последней** помимо кнопки "Далее" и "Назад", этот интерфейс включает первая и последняя кнопки для перехода к самой первой или последней странице.
- **Числовые** перечислены номера страниц в интерфейсе разбиения по страницам, что позволяет пользователю быстро перейти к определенной странице.
- **Числовые, во-первых, последний** помимо номера страниц, включает кнопки для перехода к самой первой или последней странице.

Для элементов управления DataList и Repeater мы отвечаем принятии решения относительно интерфейса разбиения по страницам и ее реализацию. Это включает в себя создание необходимых веб-элементов управления на странице и отображение запрошенной страницы при нажатии определенной кнопки интерфейс разбиения по страницам. Кроме того некоторые элементы управления интерфейса разбиения на страницы может потребоваться отключить. Например при просмотре первой страницы данных с помощью следующего, назад, во-первых, последнего интерфейса, кнопки "первый" и "Назад будет отключен.

Для этого руководства используйте let s следующего, назад, во-первых, последнего интерфейса. Добавьте четыре кнопки веб-элементов управления на страницу и задайте их `ID` s, чтобы `FirstPage`, `PrevPage`, `NextPage`, и `LastPage`. Задайте `Text` свойства &lt; &lt; во-первых, &lt; Prev, Далее &gt;и последний &gt; &gt; .


[!code-aspx[Main](paging-report-data-in-a-datalist-or-repeater-control-cs/samples/sample4.aspx)]

Создайте `Click` обработчик событий для каждого из этих кнопок. Чуть позже мы добавим код, необходимый для отображения на запрошенную страницу.

## <a name="remembering-the-total-number-of-records-being-paged-through"></a>Запоминание общее число записей, разбиваемых по страницам

Независимо от выбранного интерфейса разбиения по страницам нам нужно вычисления и помните, общее число записей, разбиваемых по страницам. Общее число строк (в сочетании с размером страницы) определяет, сколько всего страниц данных разбиваемых по страницам, которое определяет, какие элементы управления интерфейса разбиения на страницы добавляются или включены. Далее, назад, первый последний интерфейс, который мы создаем, количество страниц используется двумя способами:

- Чтобы определить, что мы просматриваете последней страницы, в этом случае кнопки следующего и последнего будут отключены.
- Если пользователь нажимает кнопку последней, нам нужно whisk их до последней страницы, индекс которого является одним меньше, чем страницы учитываются.

Количество страниц, вычисляется как общее число строк, выделенных деленное на размер страницы. Например, если мы разбиение по страницам 79 записей с помощью четырех записей на одну страницу, затем количество страниц — 20 (округление в большую сторону 79 / 4). При использовании числовых интерфейс разбиения по страницам, эта информация окно сообщает о том, сколько кнопок с номерами страниц для отображения; Если наш интерфейс разбиения по страницам включает кнопки следующего или последним, количество страниц позволяет определить, когда нужно отключить кнопки следующего или последнего.

Если интерфейс разбиения по страницам включает последнюю кнопку, крайне важно, что общее число записей, разбиваемых по страницам запомнить во время обратной передачи, чтобы при нажатии кнопки последней мы могли определить индекс последней страницы. Чтобы решить данную проблему, создайте `TotalRowCount` свойства в класс фонового кода страницы s ASP.NET, который сохраняет его значение состояния представления:


[!code-csharp[Main](paging-report-data-in-a-datalist-or-repeater-control-cs/samples/sample5.cs)]

В дополнение к `TotalRowCount`, Уделите время их создания страницам свойств только для чтения для удобного доступа индекс страницы, размер страницы и количества страниц:


[!code-csharp[Main](paging-report-data-in-a-datalist-or-repeater-control-cs/samples/sample6.cs)]

## <a name="determining-the-total-number-of-records-being-paged-through"></a>Определение общее число записей, разбиваемых по страницам

`PagedDataSource` Объект, возвращенный ObjectDataSource s `Select()` метод имеет в ней *все* товарных записей, даже если только их подмножество, отображаются в элементе управления DataList. `PagedDataSource` s [ `Count` свойство](https://msdn.microsoft.com/library/system.web.ui.webcontrols.pageddatasource.count.aspx) возвращает количество элементов, отображаемых в элементе управления DataList; [ `DataSourceCount` свойство](https://msdn.microsoft.com/library/system.web.ui.webcontrols.pageddatasource.datasourcecount.aspx) возвращает общее количество элементов в `PagedDataSource`. Таким образом, нам нужно назначить ASP.NET страницы s `TotalRowCount` свойство value объекта `PagedDataSource` s `DataSourceCount` свойство.

Для этого необходимо создать обработчик событий для ObjectDataSource s `Selected` событий. В `Selected` обработчик событий, у нас есть доступ к возвращаемому значению ObjectDataSource s `Select()` метод в данном случае `PagedDataSource`.


[!code-csharp[Main](paging-report-data-in-a-datalist-or-repeater-control-cs/samples/sample7.cs)]

## <a name="displaying-the-requested-page-of-data"></a>Отображение запрошенной страницы данных

Когда пользователь нажимает одну из кнопок в интерфейсе разбиения по страницам, нам нужно открыть запрошенную страницу данных. Так как параметры разбиения по страницам задаются с помощью строки запроса, для отображения запрошенной страницы данных используют `Response.Redirect(url)` требуется браузер пользователя s повторно запросить `Paging.aspx` страницы с соответствующими параметрами разбиения на страницы. Например, для отображения второй страницы данных, будет перенаправлять пользователя для `Paging.aspx?pageIndex=1`.

Чтобы решить данную проблему, создайте `RedirectUser(sendUserToPageIndex)` метод, который перенаправляет пользователя для `Paging.aspx?pageIndex=sendUserToPageIndex`. Затем вызовите этот метод из четыре кнопки `Click` обработчики событий. В `FirstPage` `Click` обработчик событий, вызовите `RedirectUser(0)`, отправить их на первую страницу; в `PrevPage` `Click` обработчик событий, используйте `PageIndex - 1` как индекс страницы; и т. д.


[!code-csharp[Main](paging-report-data-in-a-datalist-or-repeater-control-cs/samples/sample8.cs)]

С помощью `Click` завершения обработчики событий, DataList s записи можно просматривать постранично, нажимая кнопки. Отвлекитесь и попробуйте!

## <a name="disabling-paging-interface-controls"></a>Отключение постраничного просмотра элементы управления интерфейса

В настоящее время включены все четыре кнопки, независимо от того, просматриваемой странице. Тем не менее мы хотим отключить кнопки первый» и «назад, когда отображение первой страницы данных, и Далее» и «последняя кнопок, при отображении на последней странице. `PagedDataSource` Объект, возвращенный ObjectDataSource s `Select()` метод имеет свойства [ `IsFirstPage` ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.pageddatasource.isfirstpage.aspx) и [ `IsLastPage` ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.pageddatasource.islastpage.aspx) , можно проверить для определения того, если просматривается на первой или последней странице данных.

Добавьте следующий код в элемент управления ObjectDataSource s `Selected` обработчик событий:


[!code-csharp[Main](paging-report-data-in-a-datalist-or-repeater-control-cs/samples/sample9.cs)]

В результате этого добавления кнопок первый» и «Назад будет отключена при просмотре первой страницы, хотя кнопки следующего и последний будет отключена при просмотре на последней странице.

Let s выполните интерфейс разбиения по страницам, информируя пользователя об что странице их повторно в настоящее время Просмотр и существует общее количество страниц. Добавьте на страницу элемент управления Label Web и задайте его `ID` свойства `CurrentPageNumber`. Задайте его `Text` свойство в ObjectDataSource s выбранные обработчик событий такой, что он включает текущую просматриваемую страницу (`PageIndex + 1`) и общее число страниц (`PageCount`).


[!code-csharp[Main](paging-report-data-in-a-datalist-or-repeater-control-cs/samples/sample10.cs)]

Рис. 10 показана `Paging.aspx` при первом посещении. Так как строку запроса пуст, DataList по умолчанию отображается первые четыре продуктов; Первый» и «назад кнопок будут отключены. Нажав кнопку Далее отображаются следующие четыре записи (см. рис. 11); Теперь доступны кнопки первый и назад.


[![Отображается первая страница данных](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image23.png)](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image22.png)

**Рис. 10**: Отображается первая страница данных ([Просмотр полноразмерного изображения](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image24.png))


[![Откроется вторая страница данных](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image26.png)](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image25.png)

**Рис. 11**: Откроется вторая страница данных ([Просмотр полноразмерного изображения](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image27.png))


> [!NOTE]
> Интерфейс разбиения по страницам можно улучшить, позволяя пользователю указать, сколько страниц для просмотра на одной странице. Например элемента управления DropDownList удалось добавить варианты размера страницы Листинг 5, 10, 25, 50 и все. После выбора размера страницы, пользователи должны будут выполнять перенаправление обратно к `Paging.aspx?pageIndex=0&pageSize=selectedPageSize`. Я оставлю реализации это улучшение в качестве упражнения для чтения.


## <a name="using-custom-paging"></a>С помощью пользовательского разбиения по страницам

На страницах DataList через его данных, используя метод разбиения на страницы неэффективно по умолчанию. При работе с большими объемами данных, крайне важно, что можно использовать пользовательское разбиение по страницам. Несмотря на то, что сведения о реализации немного отличаться, принципы, лежащие в основе реализации пользовательского разбиения по страницам в элементе управления DataList совпадают с разбиением на страницы по умолчанию. С помощью пользовательского разбиения по страницам, использовать `ProductBLL` класс s `GetProductsPaged` метод (а не `GetProductsAsPagedDataSource`). Как уже говорилось в [эффективного разбиения на страницы через больших объемов данных](../paging-and-sorting/efficiently-paging-through-large-amounts-of-data-cs.md) руководстве `GetProductsPaged` должен быть передан начала строки индекса и максимальное количество возвращаемых строк. Эти параметры можно поддерживать через так же как и строки запроса `pageIndex` и `pageSize` параметры, используемые по умолчанию разбиение по страницам.

Так как здесь s не `PagedDataSource` при пользовательском разбиении альтернативных методик должен использоваться для определения общее число записей, разбиваемых по с помощью и был ли мы повторно отображение к первой или последней странице данных. `TotalNumberOfProducts()` Метод в `ProductsBLL` класс возвращает общее число продуктов, разбиваемых по страницам. Чтобы определить, если просматривается первая страница данных, проверьте индекс начальной строки, если оно равно нулю, то просматривается первая страница. Последняя страница просматривается, если индекс начальной строки, а также максимальное число строк для возврата больше или равно общему числу записей, разбиваемых по страницам.

Мы рассмотрим реализации пользовательского разбиения по страницам более подробно в следующем учебном курсе.

## <a name="summary"></a>Сводка

Ни DataList, ни элемент управления Repeater обеспечивает готовую поддержку разбиения по страницам см. в случае с GridView, DetailsView и управляет FormView, подобные функции, которые могут добавляться с минимальными усилиями. Самый простой способ реализовать разбиение по страницам по умолчанию является весь набор продуктов в рамках программы-оболочки `PagedDataSource` , а затем привязывают `PagedDataSource` DataList или Repeater. В этом руководстве мы добавили `GetProductsAsPagedDataSource` метод `ProductsBLL` класса для возвращения `PagedDataSource`. `ProductsBLL` Класс уже содержит методы, необходимые для пользовательского разбиения по страницам `GetProductsPaged` и `TotalNumberOfProducts`.

А также извлечение точного набора записей, отображаемых для пользовательского разбиения по страницам либо все записи в `PagedDataSource` по умолчанию, необходимо также вручную добавить интерфейс разбиения по страницам. В этом руководстве мы создали следующий, предыдущий, во-первых, последнего интерфейс четыре кнопки веб-элементами управления. Кроме того был добавлен элемент управления Label, отображая номер текущей страницы и общее число страниц.

В следующем учебном курсе будет показано, как добавить поддержку сортировки для элементов управления DataList и Repeater. Мы также будет показано, как создать элемент управления DataList, могут быть, разбитых на страницы и сортировки (с примерами, используя значение по умолчанию и пользовательское разбиение по страницам).

Счастливого вам программирования!

## <a name="about-the-author"></a>Об авторе

[Скотт Митчелл](http://www.4guysfromrolla.com/ScottMitchell.shtml), автор семи книг по ASP/ASP.NET и основатель веб- [4GuysFromRolla.com](http://www.4guysfromrolla.com), работает с веб-технологиями Microsoft с 1998 года. Скотт — независимый консультант, преподаватель и автор. Его последняя книга — [ *Sams Teach ASP.NET 2.0 in 24 часа*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco). Ним можно связаться по адресу [ mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) или через его блог, который можно найти в [ http://ScottOnWriting.NET ](http://ScottOnWriting.NET).

## <a name="special-thanks-to"></a>Особая благодарность

В этой серии руководств пособий рецензировалась многими компетентными редакторами. (Liz Shulok), Алексей Pespisa и Leigh Екатерина, стали Лиз Шалок в этом руководстве. Хотите поработать с моих последующих статей для MSDN? Если Да, напишите мне [ mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Вперед](sorting-data-in-a-datalist-or-repeater-control-cs.md)