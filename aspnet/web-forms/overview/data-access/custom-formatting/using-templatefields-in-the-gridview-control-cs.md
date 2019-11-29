---
uid: web-forms/overview/data-access/custom-formatting/using-templatefields-in-the-gridview-control-cs
title: Использование полей TemplateField в элементе управления GridView (C#) | Документация Майкрософт
author: rick-anderson
description: Для обеспечения гибкости GridView предлагает TemplateField, который готовится к просмотру с помощью шаблона. Шаблон может включать сочетание статического кода HTML, веб-элементов управления и...
ms.author: riande
ms.date: 03/31/2010
ms.assetid: 11de31e8-a78a-4f96-bd75-66e994175902
msc.legacyurl: /web-forms/overview/data-access/custom-formatting/using-templatefields-in-the-gridview-control-cs
msc.type: authoredcontent
ms.openlocfilehash: ec17a16d7bb487d1c5cacf2d5971bbeffc1ba031
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/28/2019
ms.locfileid: "74628059"
---
# <a name="using-templatefields-in-the-gridview-control-c"></a>Использование TemplateField в элементе управления GridView (C#)

по [Скотт Митчелл](https://twitter.com/ScottOnWriting)

[Скачивание примера приложения](https://download.microsoft.com/download/9/6/9/969e5c94-dfb6-4e47-9570-d6d9e704c3c1/ASPNET_Data_Tutorial_12_CS.exe) или [Загрузка PDF-файла](using-templatefields-in-the-gridview-control-cs/_static/datatutorial12cs1.pdf)

> Для обеспечения гибкости GridView предлагает TemplateField, который готовится к просмотру с помощью шаблона. Шаблон может включать сочетание статического HTML, веб-элементов управления и синтаксиса привязки данных. В этом учебнике мы рассмотрим, как использовать TemplateField для достижения большей степени настройки с помощью элемента управления GridView.

## <a name="introduction"></a>Введение

GridView состоит из набора полей, указывающих, какие свойства из `DataSource` должны быть включены в отображаемые выходные данные вместе с тем, как будут отображаться данные. Простейшим типом поля является BoundField, который отображает значение данных в виде текста. Другие типы полей отображают данные с помощью альтернативных HTML-элементов. Например, CheckBoxField отображается в виде флажка, состояние которого зависит от значения указанного поля данных. Имажефиелд визуализирует изображение, источник изображения которого основан на указанном поле данных. Гиперссылки и кнопки, состояние которых зависит от значения базового поля данных, могут быть отображены с использованием типов полей HyperLinkField и Буттонфиелд.

Хотя типы полей CheckBoxField, Имажефиелд, HyperLinkField и Буттонфиелд допускают альтернативное представление данных, они по-прежнему имеют достаточно ограничений относительно форматирования. CheckBoxField может отображать только один флажок, в то время как Имажефиелд может отображать только одно изображение. Что делать, если конкретному полю требуется отобразить некоторый текст, флажок *и* изображение, основанные на разных значениях полей данных? Или что делать, если нам нужно отобразить данные с помощью веб-элемента управления, отличного от флажка, изображения, гиперссылки или кнопки? Кроме того, BoundField ограничивает его отображение одним полем данных. Что делать, если нужно отобразить два или более значений полей данных в одном столбце GridView?

Чтобы обеспечить такой уровень гибкости, GridView предлагает TemplateField, который готовится к просмотру с помощью *шаблона*. Шаблон может включать сочетание статического HTML, веб-элементов управления и синтаксиса привязки данных. Более того, TemplateField имеет множество шаблонов, которые можно использовать для настройки отрисовки в различных ситуациях. Например, `ItemTemplate` используется по умолчанию для отображения ячейки для каждой строки, но шаблон `EditItemTemplate` можно использовать для настройки интерфейса при редактировании данных.

В этом учебнике мы рассмотрим, как использовать TemplateField для достижения большей степени настройки с помощью элемента управления GridView. В [предыдущем учебном курсе](custom-formatting-based-upon-data-cs.md) было показано, как настроить форматирование на основе базовых данных с помощью обработчиков событий `DataBound` и `RowDataBound`. Другой способ настройки форматирования на основе базовых данных заключается в вызове методов форматирования из шаблона. Мы также рассмотрим этот метод в этом учебнике.

В этом учебнике мы будем использовать полей TemplateField для настройки внешнего вида списка сотрудников. В частности, мы будем перечислять всех сотрудников, но в них будут отображаться имена и фамилии сотрудника в одном столбце, дата их найма в элементе управления Calendar, а также столбец состояния, показывающий, сколько дней они были использованы в компании.

[для настройки экрана используются ![три полей TemplateField](using-templatefields-in-the-gridview-control-cs/_static/image2.png)](using-templatefields-in-the-gridview-control-cs/_static/image1.png)

**Рис. 1**. использование трех полей TemplateField для настройки отображения ([щелкните, чтобы просмотреть изображение в полном размере](using-templatefields-in-the-gridview-control-cs/_static/image3.png))

## <a name="step-1-binding-the-data-to-the-gridview"></a>Шаг 1. Привязка данных к GridView

В сценариях создания отчетов, где необходимо использовать полей TemplateField для настройки внешнего вида, проще всего начать с создания элемента управления GridView, который содержит только BoundFields, а затем добавить новый полей TemplateField или преобразовать существующий BoundFields в При необходимости полей TemplateField. Поэтому начнем с этого руководства, добавив GridView на страницу в конструкторе и привязывая его к элементу ObjectDataSource, который возвращает список сотрудников. В результате выполнения этих действий будет создан элемент управления GridView с BoundFields для каждого поля сотрудника.

Откройте страницу `GridViewTemplateField.aspx` и перетащите элемент GridView с панели инструментов в конструктор. В смарт-теге GridView выберите Добавление нового элемента управления ObjectDataSource, который вызывает метод `GetEmployees()` класса `EmployeesBLL`.

[![добавить новый элемент управления ObjectDataSource, вызывающий метод «сотрудники ()»](using-templatefields-in-the-gridview-control-cs/_static/image5.png)](using-templatefields-in-the-gridview-control-cs/_static/image4.png)

**Рис. 2**. Добавление нового элемента управления ObjectDataSource, который вызывает метод `GetEmployees()` ([щелкните, чтобы просмотреть изображение с полным размером](using-templatefields-in-the-gridview-control-cs/_static/image6.png))

Таким образом привязка GridView будет автоматически добавлять BoundField для каждого свойства сотрудника: `EmployeeID`, `LastName`, `FirstName`, `Title`, `HireDate`, `ReportsTo`и `Country`. Для этого отчета не стоит тратиться на отображение свойств `EmployeeID`, `ReportsTo`или `Country`. Чтобы удалить эти BoundFields, можно выполнить следующие действия.

- Используйте диалоговое окно поля. чтобы открыть это диалоговое окно, щелкните ссылку изменить столбцы в смарт-теге GridView. Затем выберите BoundFields из левого нижнего списка и нажмите красную кнопку X, чтобы удалить BoundField.
- Измените декларативный синтаксис GridView вручную из представления исходного кода, удалив элемент `<asp:BoundField>` для BoundField, который необходимо удалить.

После удаления `EmployeeID`, `ReportsTo`и `Country` BoundFields разметка GridView должна выглядеть следующим образом:

[!code-aspx[Main](using-templatefields-in-the-gridview-control-cs/samples/sample1.aspx)]

Уделите время для просмотра хода выполнения в браузере. На этом этапе вы увидите таблицу с записью для каждого сотрудника и четырьмя столбцами: один для фамилии сотрудника, один для своего имени, один для своего названия, а другой — для их даты найма.

[![поля LastName, FirstName, Title и HireDate отображаются для каждого сотрудника.](using-templatefields-in-the-gridview-control-cs/_static/image8.png)](using-templatefields-in-the-gridview-control-cs/_static/image7.png)

**Рис. 3**. поля `LastName`, `FirstName`, `Title`и `HireDate` отображаются для каждого сотрудника ([щелкните, чтобы просмотреть изображение с полным размером](using-templatefields-in-the-gridview-control-cs/_static/image9.png)).

## <a name="step-2-displaying-the-first-and-last-names-in-a-single-column"></a>Шаг 2. Отображение первого и последнего имен в одном столбце

В настоящее время имя и фамилия каждого сотрудника отображаются в отдельном столбце. Вместо этого может быть приятно объединить их в один столбец. Для этого необходимо использовать TemplateField. Мы можем добавить новый TemplateField, добавить к нему требуемую разметку и синтаксис привязки данных, а затем удалить `FirstName` и `LastName` BoundFields или преобразовать `FirstName` BoundField в TemplateField, изменить TemplateField, включив `LastName` значение, а затем удалить `LastName` BoundField.

Оба подхода имеют одинаковый результат, но лично я предпочитаю преобразовывать BoundFields в полей TemplateField, когда это возможно, так как преобразование автоматически добавляет `ItemTemplate` и `EditItemTemplate` с веб-элементами управления и синтаксис привязки данных для имитации внешнего вида и функциональности BoundField. Преимущество заключается в том, что нам потребуется меньше работы с TemplateField, так как в процессе преобразования будет выполнена часть работы для нас.

Чтобы преобразовать существующий BoundField в TemplateField, щелкните ссылку Edit Columns (изменить столбцы) в смарт-теге GridView и откройте диалоговое окно "поля". Выберите BoundField для преобразования из списка в левом нижнем углу и щелкните ссылку "преобразовать это поле в TemplateField" в правом нижнем углу.

[![преобразование BoundField в TemplateField из диалогового окна "поля"](using-templatefields-in-the-gridview-control-cs/_static/image11.png)](using-templatefields-in-the-gridview-control-cs/_static/image10.png)

**Рис. 4**. Преобразование BoundField в TemplateField из диалогового окна "поля" ([щелкните, чтобы просмотреть изображение с полным размером](using-templatefields-in-the-gridview-control-cs/_static/image12.png))

Преобразуйте `FirstName` BoundField в TemplateField. После этого изменения в конструкторе нет перцептиве разницы. Это обусловлено тем, что преобразование BoundField в TemplateField создает TemplateField, который поддерживает внешний вид и поведение BoundField. Несмотря на то, что на этом этапе конструктора нет визуальной разницы, этот процесс преобразования заменил декларативный синтаксис BoundField-`<asp:BoundField DataField="FirstName" HeaderText="FirstName" SortExpression="FirstName" />` на следующий синтаксис TemplateField:

[!code-aspx[Main](using-templatefields-in-the-gridview-control-cs/samples/sample2.aspx)]

Как видите, TemplateField состоит из двух шаблонов: `ItemTemplate` с меткой, `Text` свойству которой присвоено значение поля данных `FirstName`, а `EditItemTemplate` с элементом управления TextBox, свойство `Text` которого также установлено в поле данных `FirstName`. Синтаксис DataBinding — `<%# Bind("fieldName") %>` — указывает, что поле данных *`fieldName`* привязано к указанному свойству веб-элемента управления.

Чтобы добавить значение поля данных `LastName` в эту TemplateField, необходимо добавить еще один веб-элемент управления Label в `ItemTemplate` и привязать его свойство `Text` к `LastName`. Это можно сделать либо вручную, либо с помощью конструктора. Чтобы сделать это вручную, просто добавьте соответствующий декларативный синтаксис в `ItemTemplate`:

[!code-aspx[Main](using-templatefields-in-the-gridview-control-cs/samples/sample3.aspx)]

Чтобы добавить его через конструктор, щелкните ссылку Edit Templates (изменить шаблоны) в смарт-теге GridView. Будет отображен интерфейс редактирования шаблона GridView. В смарт-теге этого интерфейса есть список шаблонов в GridView. Так как у нас есть только одна TemplateField на этом этапе, единственными шаблонами, перечисленными в раскрывающемся списке, являются шаблоны для `FirstName` TemplateField, а также `EmptyDataTemplate` и `PagerTemplate`. Шаблон `EmptyDataTemplate`, если он указан, используется для отображения выходных данных GridView, если нет результатов, привязанных к GridView; `PagerTemplate`, если он указан, используется для отрисовки интерфейса разбиения по страницам для GridView, поддерживающего разбиение на страницы.

[![шаблоны GridView можно редактировать с помощью конструктора](using-templatefields-in-the-gridview-control-cs/_static/image14.png)](using-templatefields-in-the-gridview-control-cs/_static/image13.png)

**Рис. 5**. шаблоны GridView можно изменять с помощью конструктора ([щелкните, чтобы просмотреть изображение с полным размером](using-templatefields-in-the-gridview-control-cs/_static/image15.png))

Чтобы также отобразить `LastName` в `FirstName` TemplateField перетащите элемент управления Label с панели элементов в `ItemTemplate` `FirstName` TemplateField в интерфейсе редактирования шаблона GridView.

[![добавить веб-элемент управления Label к ItemTemplate элемента FirstName TemplateField](using-templatefields-in-the-gridview-control-cs/_static/image17.png)](using-templatefields-in-the-gridview-control-cs/_static/image16.png)

**Рис. 6**. Добавление элемента управления Label к элементу ItemTemplate `FirstName` TemplateField ([щелкните, чтобы просмотреть изображение с полным размером](using-templatefields-in-the-gridview-control-cs/_static/image18.png))

На этом этапе для веб-элемента управления Label, добавленного в TemplateField, свойство `Text` имеет значение "Label". Необходимо изменить это значение, чтобы это свойство было привязано к значению `LastName` поля данных. Чтобы сделать это, щелкните смарт-тег элемента управления Label и выберите параметр изменить привязки к данным.

[![выберите параметр изменить DataBindings в смарт-теге метки.](using-templatefields-in-the-gridview-control-cs/_static/image20.png)](using-templatefields-in-the-gridview-control-cs/_static/image19.png)

**Рис. 7**. Выбор параметра изменить DataBindings в смарт-теге метки ([щелкните, чтобы просмотреть изображение с полным размером](using-templatefields-in-the-gridview-control-cs/_static/image21.png))

Откроется диалоговое окно привязки к данным. Здесь можно выбрать свойство для участия в DataBinding из списка слева и выбрать поле для привязки данных из раскрывающегося списка справа. Выберите свойство `Text` слева и поле `LastName` справа и нажмите кнопку ОК.

[![привязать свойство Text к полю данных LastName](using-templatefields-in-the-gridview-control-cs/_static/image23.png)](using-templatefields-in-the-gridview-control-cs/_static/image22.png)

**Рис. 8**. привязка свойства `Text` к полю данных `LastName` ([щелкните, чтобы просмотреть изображение с полным размером](using-templatefields-in-the-gridview-control-cs/_static/image24.png))

> [!NOTE]
> Диалоговое окно DataBindings позволяет указать, следует ли выполнять двустороннюю привязку данных. Если оставить этот флажок снятым, вместо `<%# Bind("LastName")%>`будет использоваться синтаксис привязки данных `<%# Eval("LastName")%>`. Для работы с этим руководством подходит любой из этих подходов. Двусторонняя привязка при вставке и изменении данных играет важную роль. Однако для простого отображения данных любой из этих подходов будет работать одинаково хорошо. В следующих учебных курсах мы подробно рассмотрим двустороннюю привязку данных.

Уделите несколько минут для просмотра этой страницы в браузере. Как видите, GridView по-прежнему включает четыре столбца. Однако столбец `FirstName` *теперь содержит `FirstName`* и `LastName` значения полей данных.

[![оба значения FirstName и LastName показаны в одном столбце](using-templatefields-in-the-gridview-control-cs/_static/image26.png)](using-templatefields-in-the-gridview-control-cs/_static/image25.png)

**Рис. 9**. значения `FirstName` и `LastName` показаны в одном столбце ([щелкните, чтобы просмотреть изображение с полным размером](using-templatefields-in-the-gridview-control-cs/_static/image27.png)).

Чтобы выполнить первый шаг, удалите `LastName` BoundField и переименуйте свойство `FirstName` TemplateField `HeaderText` в "Name". После этих изменений декларативная разметка GridView должна выглядеть следующим образом:

[!code-aspx[Main](using-templatefields-in-the-gridview-control-cs/samples/sample4.aspx)]

[![имя и фамилии каждого сотрудника отображаются в одном столбце](using-templatefields-in-the-gridview-control-cs/_static/image29.png)](using-templatefields-in-the-gridview-control-cs/_static/image28.png)

**Рис. 10**. имя и фамилия каждого сотрудника отображаются в одном столбце ([щелкните, чтобы просмотреть изображение с полным размером](using-templatefields-in-the-gridview-control-cs/_static/image30.png))

## <a name="step-3-using-the-calendar-control-to-display-thehireddatefield"></a>Шаг 3. Использование элемента управления Calendar для вывода поля`HiredDate`

Отображение значения поля данных в виде текста в элементе управления GridView осуществляется так же просто, как использование BoundField. Однако в некоторых сценариях данные лучше всего выражаются с помощью определенного веб-элемента управления, а не только текста. Такая настройка представления данных возможна при использовании полей TemplateField. Например, вместо отображения даты найма сотрудника в виде текста можно отобразить календарь (с помощью [элемента управления Calendar](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar(VS.80).aspx)) с выделенной датой найма.

Чтобы добиться этого, начните с преобразования `HiredDate` BoundField в TemplateField. Просто перейдите к смарт-тегу GridView и щелкните ссылку изменить столбцы, чтобы открыть диалоговое окно поля. Выберите `HiredDate` BoundField и щелкните "преобразовать это поле в TemplateField".

[![преобразовать BoundField Хиреддате в TemplateField](using-templatefields-in-the-gridview-control-cs/_static/image32.png)](using-templatefields-in-the-gridview-control-cs/_static/image31.png)

**Рис. 11**. Преобразование `HiredDate` BoundField в TemplateField ([щелкните, чтобы просмотреть изображение с полным размером](using-templatefields-in-the-gridview-control-cs/_static/image33.png))

Как было показано на шаге 2, это приведет к замене BoundField на TemplateField, содержащий `ItemTemplate` и `EditItemTemplate` с меткой и TextBox, свойства `Text` которых привязаны к значению `HiredDate` с помощью синтаксиса DataBinding `<%# Bind("HiredDate")%>`.

Чтобы заменить текст элементом управления "Календарь", измените шаблон, удалив метку и добавив элемент управления "Календарь". В конструкторе выберите изменить шаблоны из смарт-тега GridView и выберите `ItemTemplate` `HireDate` TemplateField из раскрывающегося списка. Затем удалите элемент управления Label и перетащите элемент управления Calendar из панели элементов в интерфейс редактирования шаблона.

[![добавить элемент управления Calendar в столбец ItemTemplate TemplateField](using-templatefields-in-the-gridview-control-cs/_static/image35.png)](using-templatefields-in-the-gridview-control-cs/_static/image34.png)

**Рис. 12**. Добавление элемента управления Calendar в `ItemTemplate` `HireDate` TemplateField ([щелкните, чтобы просмотреть изображение с полным размером](using-templatefields-in-the-gridview-control-cs/_static/image36.png))

На этом этапе каждая строка в GridView будет содержать элемент управления Calendar в своем `HiredDate` TemplateField. Однако фактическое значение `HiredDate` сотрудника не задается в любом месте элемента управления Calendar, в результате чего каждый элемент управления Calendar по умолчанию отображает текущий месяц и дату. Чтобы устранить эту проблему, необходимо назначить `HiredDate` каждого сотрудника свойствам [SelectedDate](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.selecteddate(VS.80).aspx) и [Висибледате](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.visibledate(VS.80).aspx) элемента управления Calendar.

В смарт-теге элемента управления Calendar выберите Edit Databindingss. Затем привяжите свойства `SelectedDate` и `VisibleDate` к полю данных `HiredDate`.

[![привязать свойства SelectedDate и Висибледате к полю данных Хиреддате](using-templatefields-in-the-gridview-control-cs/_static/image38.png)](using-templatefields-in-the-gridview-control-cs/_static/image37.png)

**Рис. 13**. привязка свойств `SelectedDate` и `VisibleDate` к полю данных `HiredDate` ([щелкните, чтобы просмотреть изображение с полным размером](using-templatefields-in-the-gridview-control-cs/_static/image39.png))

> [!NOTE]
> Выбранную дату элемента управления календаря не обязательно должны быть видимыми. Например, в календаре может быть 1 августа 1999 в качестве выбранной<sup>даты, но</sup>отображается текущий месяц и год. Выбранная дата и видимая Дата задаются свойствами `SelectedDate` и `VisibleDate` элемента управления Calendar. Так как мы хотим выбрать `HiredDate` сотрудника и убедиться, что он показан, необходимо привязать оба свойства к полю данных `HireDate`.

При просмотре страницы в браузере календарь теперь показывает месяц срока найма сотрудника и выбирает эту конкретную дату.

[![Хиреддате сотрудника отображается в элементе управления Calendar](using-templatefields-in-the-gridview-control-cs/_static/image41.png)](using-templatefields-in-the-gridview-control-cs/_static/image40.png)

**Рис. 14**. `HiredDate` сотрудника отображается в элементе управления Calendar ([щелкните, чтобы просмотреть изображение с полным размером](using-templatefields-in-the-gridview-control-cs/_static/image42.png))

> [!NOTE]
> В отличие от всех примеров, которые мы видели до сих пор, в этом учебнике *не* было задано свойство `EnableViewState` для `false` для этого элемента управления GridView. Причина этого решения заключается в том, что щелчок дат элемента управления Calendar вызывает обратную передачу, устанавливая выбранную дату календаря в только что нажатую дату. Однако если состояние представления GridView отключено, при каждой обратной передаче данные GridView повторно привязаны к базовому источнику данных, что приводит к тому, что выбранная дата календаря *возвращается* в `HireDate`сотрудника, перезаписывая дату, выбранную пользователем.

В этом учебнике это затеи обсуждение, так как пользователь не может обновить `HireDate`сотрудника. Вероятно, лучше настроить элемент управления Calendar так, чтобы его даты не выглядели как выбираемые. Независимо от этого учебник показывает, что в некоторых обстоятельствах состояние представления должно быть включено, чтобы обеспечить определенные функциональные возможности.

## <a name="step-4-showing-the-number-of-days-the-employee-has-worked-for-the-company"></a>Шаг 4. Отображение количества дней, в течение которых сотрудник работал в компании

Пока мы видели два приложения полей TemplateField:

- Объединение двух или более значений полей данных в один столбец;
- Выражение значения поля данных с помощью веб-элемента управления, а не текста

Третье использование полей TemplateField — отображение метаданных о базовых данных GridView. В дополнение к отображению дат найма сотрудников, например, нам может потребоваться столбец, в котором отображается общее количество дней, в течение которых они были заданы.

Еще одно использование полей TemplateField возникает в сценариях, когда базовые данные должны отображаться иначе в отчете веб-страницы, чем в формате, хранящемся в базе данных. Предположим, что в `Employees` таблице имелось `Gender` поле, в котором хранится знак `M` или `F` для обозначения пол сотрудника. При отображении этих сведений на веб-странице может потребоваться отобразить пол или женщина, а не просто "M" или "F".

Оба этих сценария можно обработать, создав *метод форматирования* в классе кода программной части страницы ASP.NET (или в отдельной библиотеке классов, реализованном как метод `static`), который вызывается из шаблона. Такой метод форматирования вызывается из шаблона с использованием того же синтаксиса DataBinding, который рассматривался ранее. Метод форматирования может принимать любое количество параметров, но должен возвращать строку. Возвращаемая строка — это код HTML, который внедряется в шаблон.

Чтобы проиллюстрировать эту концепцию, давайте добавим наш учебник, чтобы показать столбец со списком общего количества дней, в течение которых сотрудник находится в задании. Этот метод форматирования будет принимать объект `Northwind.EmployeesRow` и возвращать количество дней, в течение которых сотрудник работал в виде строки. Этот метод может быть добавлен к классу кода программной части страницы ASP.NET, но *должен* быть помечен как `protected` или `public`, чтобы быть доступен из шаблона.

[!code-csharp[Main](using-templatefields-in-the-gridview-control-cs/samples/sample5.cs)]

Так как поле `HiredDate` может содержать `NULL` значения базы данных, перед продолжением вычисления необходимо убедиться, что это значение не `NULL`. Если `HiredDate` значение равно `NULL`, мы просто возвращаем строку "Unknown". Если это не `NULL`, мы вычислим разницу между текущим временем и значением `HiredDate` и возвращающим количество дней.

Чтобы использовать этот метод, необходимо вызвать его из TemplateField в GridView с помощью синтаксиса DataBinding. Начните с добавления нового TemplateField в GridView, щелкнув ссылку Edit Columns (изменить столбцы) в смарт-теге GridView и добавив новый TemplateField.

[![добавить новый TemplateField в GridView](using-templatefields-in-the-gridview-control-cs/_static/image44.png)](using-templatefields-in-the-gridview-control-cs/_static/image43.png)

**Рис. 15**. Добавление нового TemplateField в GridView ([щелкните, чтобы просмотреть изображение с полным размером](using-templatefields-in-the-gridview-control-cs/_static/image45.png))

Задайте для свойства `HeaderText` нового TemplateField значение "дни в задании", а для свойства `HorizontalAlign` его `ItemStyle`значение `Center`. Чтобы вызвать метод `DisplayDaysOnJob` из шаблона, добавьте `ItemTemplate` и используйте следующий синтаксис привязки данных:

[!code-aspx[Main](using-templatefields-in-the-gridview-control-cs/samples/sample6.aspx)]

`Container.DataItem` возвращает объект `DataRowView`, соответствующий записи `DataSource`, привязанной к `GridViewRow`. Свойство `Row` возвращает строго типизированный `Northwind.EmployeesRow`, который передается в метод `DisplayDaysOnJob`. Синтаксис DataBinding может отображаться непосредственно в `ItemTemplate` (как показано в декларативном синтаксисе ниже) или может быть назначен свойству `Text` веб-элемента управления Label.

> [!NOTE]
> Кроме того, вместо передачи экземпляра `EmployeesRow` можно просто передать значение `HireDate` с помощью `<%# DisplayDaysOnJob(Eval("HireDate")) %>`. Однако метод `Eval` возвращает `object`, поэтому нам пришлось бы изменить сигнатуру метода `DisplayDaysOnJob`, чтобы вместо нее принимался входной параметр типа `object`. Невозможно выполнить неявное приведение `Eval("HireDate")` вызова к `DateTime`, так как столбец `HireDate` в таблице `Employees` может содержать `NULL` значения. Поэтому нам нужно принять `object` в качестве входного параметра для метода `DisplayDaysOnJob`, проверить, имел ли он значение `NULL` базы данных (которое можно выполнить с помощью `Convert.IsDBNull(objectToCheck)`), и затем выполнить соответствующее выполнение.

Из-за этих тонкостей я решил передать весь экземпляр `EmployeesRow`. В следующем учебном курсе будет представлен более подходящий пример использования синтаксиса `Eval("columnName")` для передачи входного параметра в метод форматирования.

Ниже показан декларативный синтаксис для нашего GridView после добавления TemplateField и метод `DisplayDaysOnJob`, вызываемый из `ItemTemplate`:

[!code-aspx[Main](using-templatefields-in-the-gridview-control-cs/samples/sample7.aspx)]

На рис. 16 показан завершенный учебник при просмотре в браузере.

[![число дней, на которое отображается сотрудник в задании](using-templatefields-in-the-gridview-control-cs/_static/image47.png)](using-templatefields-in-the-gridview-control-cs/_static/image46.png)

**Рис. 16**. число дней, в течение которых сотрудник находится в задании ([щелкните, чтобы просмотреть изображение с полным размером](using-templatefields-in-the-gridview-control-cs/_static/image48.png))

## <a name="summary"></a>Сводка

TemplateField в элементе управления GridView обеспечивает большую степень гибкости при отображении данных, чем доступно в других элементах управления "поле". Полей TemplateField идеально подходят для ситуаций, в которых:

- Несколько полей данных должны отображаться в одном столбце GridView
- Данные лучше всего выражаются с помощью веб-элемента управления, а не обычного текста.
- Выходные данные зависят от базовых данных, таких как отображение метаданных или переформатирование данных.

Помимо настройки представления данных, полей TemplateField также используются для настройки пользовательских интерфейсов, используемых для редактирования и вставки данных, как мы увидим в следующих руководствах.

Следующие два руководства продолжают изучать шаблоны, начиная с рассмотрения использования полей TemplateField в DetailsView. После этого мы вернемся к элементу FormView, который использует шаблоны вместо полей для обеспечения большей гибкости макета и структуры данных.

Поздравляем с программированием!

## <a name="about-the-author"></a>Об авторе

[Скотт Митчелл](http://www.4guysfromrolla.com/ScottMitchell.shtml), автор семи книг по ASP/ASP. NET и основатель [4GuysFromRolla.com](http://www.4guysfromrolla.com), работал с веб-технологиями Майкрософт с 1998. Скотт работает как независимый консультант, преподаватель и модуль записи. Его последняя книга — [*Sams обучать себя ASP.NET 2,0 за 24 часа*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco). Он доступен по адресу [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) или через его блог, который можно найти по адресу [http://ScottOnWriting.NET](http://ScottOnWriting.NET).

## <a name="special-thanks-to"></a>Специальная благодарность

Эта серия руководств была рассмотрена многими полезными рецензентами. Специалист по интересу для этого руководства был «Jagers)». Хотите ознакомиться с моими будущими статьями MSDN? Если это так, расположите строку в [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Назад](custom-formatting-based-upon-data-cs.md)
> [Вперед](using-templatefields-in-the-detailsview-control-cs.md)
