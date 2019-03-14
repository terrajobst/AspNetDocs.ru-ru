---
uid: web-forms/overview/data-access/paging-and-sorting/paging-and-sorting-report-data-vb
title: Разбиение по страницам и сортировка данных (Visual Basic) | Документация Майкрософт
author: rick-anderson
description: Разбиение по страницам и сортировка – две часто встречающиеся функции отображения данных в интерактивном приложении. В этом руководстве мы рассмотрим первый взгляд на добавление сортировки и...
ms.author: riande
ms.date: 08/15/2006
ms.assetid: b895e37e-0e69-45cc-a7e4-17ddd2e1b38d
msc.legacyurl: /web-forms/overview/data-access/paging-and-sorting/paging-and-sorting-report-data-vb
msc.type: authoredcontent
ms.openlocfilehash: 2e1cc844122b0fdebbc0be09f88baa11a461ab8e
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57038621"
---
<a name="paging-and-sorting-report-data-vb"></a>Разбиение по страницам и упорядочение данных отчета (VB)
====================
по [Скотт Митчелл](https://twitter.com/ScottOnWriting)

[Скачайте пример приложения](http://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_24_VB.exe) или [скачать PDF](paging-and-sorting-report-data-vb/_static/datatutorial24vb1.pdf)

> Разбиение по страницам и сортировка – две часто встречающиеся функции отображения данных в интерактивном приложении. В этом руководстве мы рассмотрим первый взгляд на добавление сортировки и упорядочения к отчетам, которые мы будут надстраиваться в будущих учебных курсах.


## <a name="introduction"></a>Вступление

Разбиение по страницам и сортировка – две часто встречающиеся функции отображения данных в интерактивном приложении. Например при поиске книг по ASP.NET в Интернет-магазине, могут существовать сотни книг, но отчет с результатами поиска только десять совпадениями на одной странице. Кроме того результаты можно отсортировать по title, цена, количество страниц, имя автора и т. д. Хотя в предыдущих 23 учебных курсах рассматривалось Создание различных отчетов, включая интерфейсы, позволяющие добавления, изменения и удаления данных, мы продуктом, не рассматривались как сортировать данные и единственным разбиение по страницам примеры мы видели ve проработали DetailsView и FormView элементы управления.

В этом руководстве будет показано, как добавить сортировки и упорядочения к отчетам, что может быть выполнено простой установкой нескольких флажков. К сожалению такая упрощенная реализация имеет свои недостатки, которые интерфейс упорядочения содержит почти все необходимое, а процедуры разбиения на страницы не предназначены для эффективного просмотра больших результирующих наборов. Как преодолеть ограничения out-of--box разбиение по страницам и сортировка решения будут посвящены следующие учебники.

## <a name="step-1-adding-the-paging-and-sorting-tutorial-web-pages"></a>Шаг 1. Добавление разбиения по страницам и сортировка учебника веб-страниц

Прежде чем приступать к этом руководстве, позволяют сначала Отвлекитесь и добавим страницы ASP.NET, которые потребуются для этого учебника и трех последующих s. Начнем с создания новой папки в проект с именем `PagingAndSorting`. Добавьте следующие пять страниц ASP.NET в этой папке, в которых настроено использование главной страницы `Site.master`:

- `Default.aspx`
- `SimplePagingSorting.aspx`
- `EfficientPaging.aspx`
- `SortParameter.aspx`
- `CustomSortingUI.aspx`


![Создание папки PagingAndSorting и добавление страниц учебника по ASP.NET](paging-and-sorting-report-data-vb/_static/image1.png)

**Рис. 1**: Создание папки PagingAndSorting и добавление страниц учебника по ASP.NET


Затем откройте `Default.aspx` страницы и перетащите `SectionLevelTutorialListing.ascx` пользовательского элемента управления с `UserControls` папку в область конструктора. Данный пользовательский элемент управления, созданный в учебном курсе [главные страницы и структуру переходов узла](../introduction/master-pages-and-site-navigation-vb.md) , просматривает карту узла и отображает руководства, имеющиеся в данном разделе, в виде маркированного списка.


![Добавление элемента управления Sectionleveltutoriallisting.ascx к странице Default.aspx](paging-and-sorting-report-data-vb/_static/image2.png)

**Рис. 2**: Добавление элемента управления Sectionleveltutoriallisting.ascx к странице Default.aspx


Чтобы в маркированном списке отображались учебные курсы, которые будут созданы и разбиению на страницы, необходимо добавить их в карту узла. Откройте `Web.sitemap` файл и добавьте следующую разметку после редактирования, вставки и удаления сайта разметки узла карты:


[!code-xml[Main](paging-and-sorting-report-data-vb/samples/sample1.xml)]


![Обновление карты узла для добавления новых страниц ASP.NET](paging-and-sorting-report-data-vb/_static/image3.png)

**Рис. 3**: Обновление карты узла для добавления новых страниц ASP.NET


## <a name="step-2-displaying-product-information-in-a-gridview"></a>Шаг 2. Отображение информации о продукте в элементе управления GridView

Мы фактически реализации возможностей упорядочения и разбиения по страницам, позвольте s сначала создать стандартный не srotable, элемент управления GridView со списком информации о продукте. Это задача мы хранить много раз выполняли данной серии учебных курсов таким образом, эти действия должны быть знакомы. Сначала откройте `SimplePagingSorting.aspx` страницы и перетащите элемент управления GridView с панели элементов в конструктор, установив его `ID` свойства `Products`. Создайте новый ObjectDataSource, который использует класса ProductsBLL s `GetProducts()` для возврата всей информации о продукте.


![Получение информации обо всех продуктах с помощью метода GetProducts()](paging-and-sorting-report-data-vb/_static/image4.png)

**Рис. 4**: Получение информации обо всех продуктах с помощью метода GetProducts()


Так как этот отчет является не только для чтения отчет, здесь s необходимо сопоставлять ObjectDataSource s `Insert()`, `Update()`, или `Delete()` соответствующим методам `ProductsBLL` методов; таким образом, выберите значение (None) из раскрывающегося списка для обновления, вставки, и удаление вкладок.


![Выберите (нет) параметра в раскрывающемся списке в UPDATE, INSERT и удаление вкладок](paging-and-sorting-report-data-vb/_static/image5.png)

**Рис. 5**: Выберите (нет) параметра в раскрывающемся списке в UPDATE, INSERT и удаление вкладок


Далее позволяют настраивать поля GridView s, чтобы отображались только названия продуктов, поставщики, категории, цены и состояний неподдерживаемые s. Кроме того, изменения можно вносить любые форматирования уровня полей, такие как настройка `HeaderText` или форматирование цены как денежной единицы. После внесения этих изменений декларативная разметка s GridView должен выглядеть следующим образом:


[!code-aspx[Main](paging-and-sorting-report-data-vb/samples/sample2.aspx)]

Рис. 6 показаны до сих при просмотре через браузер. Обратите внимание, что страница со списком продуктов в одном экране с отображением каждого s название продукта, категории, поставщика, цены и более не поддерживается состояние.


[![Каждым из продуктов, перечислены](paging-and-sorting-report-data-vb/_static/image7.png)](paging-and-sorting-report-data-vb/_static/image6.png)

**Рис. 6**: Каждым из продуктов, перечислены ([Просмотр полноразмерного изображения](paging-and-sorting-report-data-vb/_static/image8.png))


## <a name="step-3-adding-paging-support"></a>Шаг 3. Добавление поддержки разбиения по страницам

Листинг *все* продуктов на одном экране может привести к информационной перегрузке пользователей, изучающих данные. Чтобы сделать результаты более управляемыми, мы можно разбить данные на страницы меньшего размера данных и разрешить пользователям перемещаться по одной странице данных за раз. Для выполнения этого просто установите флажок Enable Paging в смарт-теге GridView s (этот параметр задает GridView s [ `AllowPaging` свойство](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.allowpaging.aspx) для `true`).


[![Установите флажок Включить разбиение на страницы для добавления поддержки разбиения по страницам](paging-and-sorting-report-data-vb/_static/image10.png)](paging-and-sorting-report-data-vb/_static/image9.png)

**Рис. 7**: Установите флажок "Включить разбиение по страницам" для добавления поддержки разбиения по страницам ([Просмотр полноразмерного изображения](paging-and-sorting-report-data-vb/_static/image11.png))


Включение разбиения на страницы ограничивает количество записей, отображаемых на одной странице и добавляет *интерфейс разбиения по страницам* к GridView. Интерфейс разбиения по страницам по умолчанию, показано на рис. 7, — это последовательность номеров страниц, позволяя пользователю быстро переходить от одной страницы данных в другой. Этот интерфейс разбиения по страницам должен быть вам знаком, как мы ve рассматривался при добавлении поддержки разбиения по страницам к элементам управления DetailsView и FormView в предыдущих учебных курсах.

Элементы управления DetailsView и FormView отображает только одну запись на одной странице. GridView, обращается к его [ `PageSize` свойство](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.pagesize.aspx) для определения количества записей, отображаемых на странице (данное свойство принимает значение 10).

Этот интерфейс разбиения по страницам s GridView, DetailsView и FormView можно настроить, используя следующие свойства:

- `PagerStyle` Указывает сведения о стиле для интерфейса разбиения по страницам; можно указать параметры, например `BackColor`, `ForeColor`, `CssClass`, `HorizontalAlign`, и т. д.
- `PagerSettings` содержит множество свойств, которые можно настраивать функциональность интерфейса разбиения по страницам; `PageButtonCount` указывает максимальное число цифровых номеров страниц отображается в интерфейсе разбиения по страницам (по умолчанию — 10); [ `Mode` свойство](https://msdn.microsoft.com/library/system.web.ui.webcontrols.pagersettings.mode.aspx) указывает, как работает и может быть присвоено интерфейс разбиения по страницам: 

    - `NextPrevious` показаны далее» и «Previous кнопки, позволяя пользователям перемещаться вперед и назад одной странице за раз
    - `NextPreviousFirstLast` Помимо кнопки "Далее" и "Назад" Первая и последняя кнопки также будут включены, позволяя пользователю быстро перейти к первой или последней странице данных
    - `Numeric` Отображение ряда номеров страниц, позволяющее пользователю немедленно переходить на любую страницу
    - `NumericFirstLast` Помимо номеров страниц включает кнопки первая и последняя, позволяя пользователю быстро перейти к первой или последней странице данных. Первой/последней кнопки отображаются, только если все номера страниц не может поместиться

Кроме того GridView, DetailsView и FormView, предлагают `PageIndex` и `PageCount` , обозначающие текущую просматриваемую страницу и общее число страниц данных, соответственно. `PageIndex` Свойство индексируется начиная с 0, означающее, что при просмотре первой страницы данных `PageIndex` будет равно 0. `PageCount`, с другой стороны, начинает учитываться с 1, означающее, что `PageIndex` ограничено значениями от 0 и `PageCount - 1`.

Позвольте s нужно потратить немного улучшим стандартный вид интерфейса разбиения по страницам s наших GridView. В частности позвольте s имеют интерфейс разбиения по страницам, правому краю и светло-серый фон. Вместо того чтобы задавать эти свойства напрямую через GridView s `PagerStyle` свойства, let s создайте класс CSS в `Styles.css` с именем `PagerRowStyle` и назначьте `PagerStyle` s `CssClass` помощью нашей темы. Сначала откройте `Styles.css` и добавить следующий код CSS определение класса:


[!code-css[Main](paging-and-sorting-report-data-vb/samples/sample3.css)]

Затем откройте `GridView.skin` файл `DataWebControls` папку внутри `App_Themes` папки. Как уже говорилось в *главные страницы и структуру переходов узла* , файлы обложки могут использоваться для указания значения свойств по умолчанию для веб-элемент управления. Поэтому необходимо расширить существующие параметры для включения параметра `PagerStyle` s `CssClass` свойства `PagerRowStyle`. Кроме того, s позволяют настроить интерфейс разбиения по страницам, чтобы отображалось не более кнопок пять номерами страниц, с помощью `NumericFirstLast` интерфейс разбиения по страницам.


[!code-aspx[Main](paging-and-sorting-report-data-vb/samples/sample4.aspx)]

## <a name="the-paging-user-experience"></a>Взаимодействие с пользователем разбиения на страницы

Рис. 8 показана открытая в браузере после проверки флажок Enable Paging s GridView веб-страницы и `PagerStyle` и `PagerSettings` конфигурации были внесены через `GridView.skin` файл. Обратите внимание только десяти записей отображаются, а интерфейс разбиения по страницам указывает, что просматривается первая страница данных.


[![С поддержкой разбиения по страницам отображаются только подмножество записей за раз](paging-and-sorting-report-data-vb/_static/image13.png)](paging-and-sorting-report-data-vb/_static/image12.png)

**Рис. 8**: С поддержкой разбиения по страницам, отображаются только подмножество записей за раз ([Просмотр полноразмерного изображения](paging-and-sorting-report-data-vb/_static/image14.png))


Когда пользователь щелкает один из номеров страниц в интерфейсе разбиения по страницам, обратная передача и страница повторно загружается показывает, что запрошенный страницы s записей. Рис. 9 показаны результаты после перехода к последней странице данных. Обратите внимание на то, что последняя страница имеет только одну запись; Это обусловлено существует 81 в целом, приводит к 8 страниц по 10 записей и одна страница с записью одиночному.


[![Щелкнув номер страницы вызывает обратную передачу и показано соответствующее подмножество записей](paging-and-sorting-report-data-vb/_static/image16.png)](paging-and-sorting-report-data-vb/_static/image15.png)

**Рис. 9**: Щелкнув номер страницы вызывает обратную передачу и показаны соответствующие записи из подмножества ([Просмотр полноразмерного изображения](paging-and-sorting-report-data-vb/_static/image17.png))


## <a name="paging-s-server-side-workflow"></a>Разбиение по страницам s серверный рабочий процесс

Когда пользователь щелкает кнопку в интерфейсе разбиения по страницам, обратная передача и начинается следующий серверный рабочий процесс:

1. GridView-s (или DetailsView или FormView) `PageIndexChanging` вызывает событие
2. Элемент управления ObjectDataSource повторно запрашивает *все* данные из BLL; GridView s `PageIndex` и `PageSize` значения свойств используются для определения записей, возвращенных из BLL должны отображаться в GridView
3. GridView s `PageIndexChanged` вызывает событие

На шаге 2 элемент управления ObjectDataSource повторно запрашивает все данные из источника данных. Этот стиль разбиения по страницам обычно называется *разбиение по страницам по умолчанию*, так как он s разбиение по страницам по умолчанию используется при задании `AllowPaging` свойства `true`. Имеет значения по умолчанию наивно разбиение по страницам данных веб-элемент управления получает все записи для каждой страницы данных, несмотря на то, что только подмножество записей преобразуется HTML, s, отправляемых в браузер. Если к базе данных кэшируется в BLL или элемент управления ObjectDataSource, разбиение по страницам по умолчанию неработоспособно для достаточно больших наборах результатов или для веб-приложений с большим числом одновременных пользователей.

В следующем учебном курсе мы рассмотрим, как реализовать *пользовательское разбиение по страницам*. С помощью пользовательского разбиения по страницам можно специально указать ObjectDataSource для извлечения только точного набора записей, необходимых для запрошенной страницы данных. Как вы можете представить, пользовательское разбиение по страницам значительно повышает эффективность разбиение по страницам больших результирующих наборов.

> [!NOTE]
> Хотя разбиение по страницам по умолчанию не подходит, при разбиении на страницы через достаточно больших наборах результатов или для узлов со множеством одновременно работающих пользователей, осознать, что требует множества изменений и усилий для реализации пользовательского разбиения по страницам и не простая установка флажка (как по умолчанию разбиение по страницам). Таким образом, разбиение по страницам по умолчанию может быть идеальным выбором для небольших, низким трафиком веб-сайтов или когда задает разбиение по страницам относительно небольшой результирующий, так как он s гораздо проще и быстрее реализовать.


Например если мы знаем, что мы никогда не будет более чем 100 продуктов в базе данных, минимальное увеличение производительности на пользовательское разбиение по страницам, навряд ли компенсируется усилия, необходимые для его реализации. Если, однако мы один день возможно, тысяч или десятков тысяч продуктов, *не* реализации пользовательского разбиения по страницам будет значительно препятствовать масштабируемости приложения.

## <a name="step-4-customizing-the-paging-experience"></a>Шаг 4. Настройка интерфейса разбиения по страницам

Веб-элементы управления данными предоставляют ряд свойств, которые можно использовать для улучшения обслуживания пользователя s разбиения на страницы. `PageCount` Свойство, например, определяет, сколько всего страниц, хотя `PageIndex` указывает текущую просматриваемую страницу и можно задать для быстрого перехода пользователя к определенной странице. Чтобы продемонстрировать способы использования этих свойств, чтобы улучшить взаимодействие с пользователем s разбиения на страницы, давайте s добавьте метку веб-элемента управления на страницу, сообщающее, какой странице их повторно в настоящее время посещения, а также элемент управления DropDownList, что дает возможность быстрого перехода к определенной странице .

Во-первых, добавьте элемент управления Label Web на страницу, задайте его `ID` свойства `PagingInformation`и очистите его `Text` свойство. Создайте обработчик событий для GridView s `DataBound` событий и добавьте следующий код:


[!code-vb[Main](paging-and-sorting-report-data-vb/samples/sample5.vb)]

Этот обработчик события присваивает `PagingInformation` метка s `Text` сообщение, информирующее пользователя страницы, просматриваемой в данный момент свойство `Products.PageIndex + 1` из общего числа страниц `Products.PageCount` (мы добавим 1, чтобы `Products.PageIndex` свойство поскольку `PageIndex` индексируется начиная с 0). Я выбрал присваивание эту метку s `Text` свойство в `DataBound` обработчик событий, в отличие от `PageIndexChanged` обработчик событий из-за `DataBound` происходит каждый раз данные будут привязаны к GridView, тогда как `PageIndexChanged` только обработчик событий вызывается при изменении индекса страницы. Посетите при GridView инициализируется данными, привязанными на первой странице, `PageIndexChanging` fire t событий (в то время как `DataBound` при событии).

В результате этого добавления пользователя отображается сообщение о том, какие просматриваемой страницы и сколько всего страниц данных существует.


[![Отображаются номер текущей страницы и общее число страниц](paging-and-sorting-report-data-vb/_static/image19.png)](paging-and-sorting-report-data-vb/_static/image18.png)

**Рис. 10**: Отображаются номер текущей страницы и общее число страниц ([Просмотр полноразмерного изображения](paging-and-sorting-report-data-vb/_static/image20.png))


Помимо элемента управления Label позвольте s также добавить элемент управления DropDownList, перечислены номера страниц в GridView с выбранной текущей просматриваемой страницей. Смысл в том, что пользователь может быстро перейти с текущей страницы в другую, просто выбрав новый индекс страницы в элементе управления DropDownList. Начните с добавления элемента управления DropDownList конструктор, установив его `ID` свойства `PageList` и установить флажок Включить AutoPostBack смарт-теге.

Затем вернитесь к `DataBound` обработчик событий и добавьте следующий код:


[!code-vb[Main](paging-and-sorting-report-data-vb/samples/sample6.vb)]

Этот код начинается с очистки элементов в `PageList` DropDownList. Это может показаться излишним, поскольку один t было ожидать, что число страниц, чтобы изменить, но другие пользователи могут параллельно использовать систему, добавление или удаление записей из `Products` таблицы. Такие вставки или удаления могут привести к изменению количества страниц данных.

Далее, нам нужно снова создать номера страниц и один из них, который сопоставляется текущего GridView `PageIndex` выбран по умолчанию. Это осуществляется с помощью цикла от 0 до `PageCount - 1`, добавления нового `ListItem` в каждой итерации и установив его `Selected` свойство значение true, если индекс текущей итерации равно GridView s `PageIndex` свойство.

Наконец, нам необходимо создать обработчик событий для элемента управления DropDownList s `SelectedIndexChanged` ObjectDataSource, который запускается каждый раз, когда пользователь выбрать другой элемент в списке. Чтобы создать этот обработчик событий, просто дважды щелкните в конструкторе элемента управления DropDownList, а затем добавьте следующий код:


[!code-vb[Main](paging-and-sorting-report-data-vb/samples/sample7.vb)]

Как показано на рис. 11, просто изменив GridView s `PageIndex` свойство вызывает запись данных привязывается к GridView. В GridView s `DataBound` обработчик событий, соответствующих DropDownList `ListItem` выбран.


[![Он автоматически откроется шестой странице при выборе элемент страницы 6 стрелку раскрывающегося списка](paging-and-sorting-report-data-vb/_static/image22.png)](paging-and-sorting-report-data-vb/_static/image21.png)

**Рис. 11**: Он автоматически откроется шестой странице при выборе элемент страницы 6 стрелку раскрывающегося списка ([Просмотр полноразмерного изображения](paging-and-sorting-report-data-vb/_static/image23.png))


## <a name="step-5-adding-bi-directional-sorting-support"></a>Шаг 5. Добавление поддержки двунаправленного сортировки

Добавление поддержки сортировки с двунаправленным письмом является простым добавлением поддержки разбиения по страницам просто установите флажок Включить сортировку в смарт-теге GridView s (присваивающего GridView s [ `AllowSorting` свойство](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.allowsorting.aspx) для `true`). Результате этого заголовки полей GridView s как LinkButton, при щелчке, вызывает обратную передачу и возвращать данные, отсортированные по выбранному столбцу в порядке возрастания. Еще раз щелкнув один и тот же заголовок LinkButton выполняется переупорядочивание данных в порядке убывания.

> [!NOTE]
> При использовании пользовательского уровня доступа к данным вместо типизированного набора DataSet, не имеется параметр Включить сортировку в смарт-теге GridView s. Только элементов управления GridView привязать к источникам данных со встроенной поддержкой упорядочения иметь этот флажок доступен. Типизированный набор DataSet предоставляет поддержку сортировки out of box, поскольку ADO.NET DataTable предоставляет `Sort` метод, при вызове сортирует s DataTable с помощью критериев, заданных объектов DataRow.


Если DAL не возвращает объекты, которые изначально поддерживают сортировку, необходимо будет настроить элемент управления ObjectDataSource для передачи сведений о сортировке уровня бизнес-логики, который можно сортировать данные или данные отсортированы по DAL. Мы рассмотрим порядок сортировки данных в бизнес-логики и уровни доступа к данным в следующем учебном курсе.

Сортировки элементов управления LinkButton, преобразуются в гиперссылки HTML, текущие цвета которых (синий для непосещенных ссылок и Темно-красный для посещенных ссылок) пересекаться с цветом фона строки заголовка. Вместо этого let s у всех ссылок строки заголовка установим белый цвет независимо от того, следует ли они ve был посещен или нет. Это можно сделать, добавив следующую команду, чтобы `Styles.css` класса:


[!code-css[Main](paging-and-sorting-report-data-vb/samples/sample8.css)]

Этот синтаксис указывает на использование белого цвета при отображении этих гиперссылок в элементе, используется класс HeaderStyle.

После этого добавления к CSS при посещении страницы через обозреватель экран должен выглядеть как на рис. 12. В частности на рис. 12 показаны результаты после нажатия ссылку заголовка s цены.


[![Результаты упорядочены по UnitPrice в возрастающем порядке](paging-and-sorting-report-data-vb/_static/image25.png)](paging-and-sorting-report-data-vb/_static/image24.png)

**Рис. 12**: Результаты упорядочены по UnitPrice в возрастающем порядке ([Просмотр полноразмерного изображения](paging-and-sorting-report-data-vb/_static/image26.png))


## <a name="examining-the-sorting-workflow"></a>Изучение рабочего потока упорядочения

GridView все поля BoundField, CheckBoxField, TemplateField и т. д. у `SortExpression` свойство, указывающее выражение, которое следует использовать для сортировки данных, при щелчке ссылки заголовка сортировки s поля. У GridView есть также `SortExpression` свойство. При нажатии элемента управления LinkButton нажатии, GridView назначает s поле `SortExpression` значение его `SortExpression` свойство. Затем данные повторно извлекается из элемента управления ObjectDataSource и отсортированы в соответствии с GridView s `SortExpression` свойство. Ниже приведена последовательность действий, процесс, если пользователь сортирует данные в элементе управления GridView:

1. GridView s [событие сортировки](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.sorting(VS.80).aspx) активируется
2. GridView s [ `SortExpression` свойство](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.sortexpression.aspx) присваивается `SortExpression` поля, элемент управления LinkButton была нажата
3. Элемент управления ObjectDataSource повторно получает данные из BLL, а затем упорядочивает их с использованием GridView s `SortExpression`
4. GridView s `PageIndex` свойство сбрасывается на 0, означающее, что при упорядлочении пользователь возвращается к первой странице данных (при условии, что реализована поддержка разбиения по страницам)
5. GridView s [ `Sorted` событий](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.sorted(VS.80).aspx) активируется

Как и с разбиением на страницы по умолчанию, упорядочение по умолчанию снова получает *все* записи из BLL. При использовании упорядочения без разбиения на страницы или с по умолчанию разбиение на страницы, там s не способ обхода этой производительность (хватает кэширования данных базы данных). Тем не менее, как мы увидим в дальнейших учебных курсах, он s, возможно эффективное упорядочение данных при использовании пользовательского разбиения по страницам.

При привязке элемента ObjectDataSource к GridView через стрелку раскрывающегося списка в смарт-теге GridView s, каждое поле GridView автоматически имеет его `SortExpression` присваивается имя поля данных в `ProductsRow` класса. Например `ProductName` BoundField s `SortExpression` присваивается `ProductName`, как показано в следующей декларативной разметке:


[!code-aspx[Main](paging-and-sorting-report-data-vb/samples/sample9.aspx)]

Поля можно настроить таким образом, чтобы его не поддерживает сортировку по очистке s его `SortExpression` (присвоение ему пустой строкой). Чтобы проиллюстрировать это, представим, что мы требуется разрешить клиентам упорядочения по цене. `UnitPrice` BoundField s `SortExpression` может быть удалено из декларативной разметке либо через поля-диалоговое окно (которое можно открыть, щелкнув ссылку Изменить столбцы в смарт-теге GridView s).


![Результаты упорядочены по UnitPrice в возрастающем порядке](paging-and-sorting-report-data-vb/_static/image27.png)

**Рис. 13**: Результаты упорядочены по UnitPrice в возрастающем порядке


Один раз `SortExpression` свойство было снято для `UnitPrice` BoundField, заголовок отображается как текст, а не как ссылки, таким образом запрещая пользователям выполнять упорядочение данных по цене.


[![При удалении свойства SortExpression приводит к, пользователи больше не возможности упорядочения продуктов по цене](paging-and-sorting-report-data-vb/_static/image29.png)](paging-and-sorting-report-data-vb/_static/image28.png)

**Рис. 14**: При удалении свойства SortExpression приводит к, пользователи могут больше не сортировать продукты, цена ([Просмотр полноразмерного изображения](paging-and-sorting-report-data-vb/_static/image30.png))


## <a name="programmatically-sorting-the-gridview"></a>Программное упорядочение элемента управления GridView

Можно также отсортировать содержимое элемента управления GridView программным способом с помощью GridView s [ `Sort` метод](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.sort.aspx). Просто передайте `SortExpression` значение сортировки вместе с [ `SortDirection` ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.sortdirection.aspx) (`Ascending` или `Descending`), и GridView s данные будут переупорядочены.

Представьте, что причина, мы отключили сортировку по `UnitPrice` было, поскольку мы опасались, что наши клиенты просто бы покупать только самые дешевые продукты. Тем не менее мы хотим поощрить ее к купить самые дорогие продукты, поэтому мы d, такие как их, чтобы иметь возможность упорядочения по цене, но только из самых дорогих цены до наименее.

Для выполнения добавьте кнопку веб-элемент управления на страницу, задайте его `ID` свойства `SortPriceDescending`и его `Text` свойства для сортировки по цене. Создайте обработчик событий для кнопки s `Click` событий, дважды щелкнув элемент управления в конструкторе. Добавьте следующий код в этот обработчик событий:


[!code-vb[Main](paging-and-sorting-report-data-vb/samples/sample10.vb)]

После нажатия этой кнопки пользователь возвращается к первой странице с продуктами, упорядоченными по цене начиная с самой высокой (см рис. 15).


[![Нажатии кнопки выполняется упорядочение продуктов начиная с самых дорогих с самой](paging-and-sorting-report-data-vb/_static/image32.png)](paging-and-sorting-report-data-vb/_static/image31.png)

**Рис. 15**: Нажатии кнопки выполняется упорядочение продуктов из самых дорогих с самой ([Просмотр полноразмерного изображения](paging-and-sorting-report-data-vb/_static/image33.png))


## <a name="summary"></a>Сводка

В этом руководстве мы узнали, как для реализации по умолчанию, разбиение по страницам и сортировка возможности которые включаются простой установкой флажка! При выполнении пользователем упорядочения или данных по страницам, сходный рабочий процесс развертывания:

1. Обратная
2. Данные веб-элемента управления s предварительно уровня вызывает событие (`PageIndexChanging` или `Sorting`)
3. Повторно все данные извлекаются с ObjectDataSource
4. Данные веб-элемента управления s после уровня вызывает событие (`PageIndexChanged` или `Sorted`)

Хотя реализация разбиения по страницам и сортировка выполняется очень просто, больше усилий должен быть применен для использования более эффективного пользовательского разбиения по страницам и улучшения интерфейса разбиения или упорядочения. Эти вопросы будут рассмотрены в последующих учебных курсах.

Счастливого вам программирования!

## <a name="about-the-author"></a>Об авторе

[Скотт Митчелл](http://www.4guysfromrolla.com/ScottMitchell.shtml), автор семи книг по ASP/ASP.NET и основатель веб- [4GuysFromRolla.com](http://www.4guysfromrolla.com), работает с веб-технологиями Microsoft с 1998 года. Скотт — независимый консультант, преподаватель и автор. Его последняя книга — [ *Sams Teach ASP.NET 2.0 in 24 часа*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco). Ним можно связаться по адресу [ mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) или через его блог, который можно найти в [ http://ScottOnWriting.NET ](http://ScottOnWriting.NET).

> [!div class="step-by-step"]
> [Назад](creating-a-customized-sorting-user-interface-cs.md)
> [Вперед](efficiently-paging-through-large-amounts-of-data-vb.md)