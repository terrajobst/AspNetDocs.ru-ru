---
uid: web-forms/overview/ajax-control-toolkit/cascadingdropdown/using-cascadingdropdown-with-a-database-cs
title: Использование CascadingDropDown с базой данных (C#) | Документация Майкрософт
author: wenz
description: Элемент управления CascadingDropDown в наборе средств AJAX Control Toolkit расширяет элемент управления DropDownList таким образом, что изменения в одном элементе DropDownList загружают связанные значения в АНОС...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 684f0c28-a490-4e5b-b5e5-5dfb77464b49
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/cascadingdropdown/using-cascadingdropdown-with-a-database-cs
msc.type: authoredcontent
ms.openlocfilehash: bcf453170d17807b4e3b2d2a8b545cba43139f89
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78483750"
---
# <a name="using-cascadingdropdown-with-a-database-c"></a>Использование CascadingDropDown с базой данных (C#)

по [Кристиан Венз](https://github.com/wenz)

[Скачать код](https://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown1.cs.zip) или [скачать PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/cascadingdropdown1CS.pdf)

> Элемент управления CascadingDropDown в наборе средств AJAX Control Toolkit расширяет элемент управления DropDownList таким образом, что изменения в одном элементе DropDownList загружают связанные значения из другого DropDownList. Чтобы это работало, необходимо создать специальную веб-службу.

## <a name="overview"></a>Обзор

Элемент управления CascadingDropDown в наборе средств AJAX Control Toolkit расширяет элемент управления DropDownList таким образом, что изменения в одном элементе DropDownList загружают связанные значения из другого DropDownList. (Например, один список содержит список штатов США, а следующий список заполняется основными городами в этом состоянии.) Чтобы это работало, необходимо создать специальную веб-службу.

## <a name="steps"></a>Шаги

Во-первых, требуется источник данных. В этом примере используется база данных AdventureWorks и Microsoft SQL Server 2005 Express Edition. База данных является необязательной частью установки Visual Studio (включая экспресс-выпуск) и доступна как отдельная загрузка в разделе [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064). База данных AdventureWorks входит в состав примеров SQL Server 2005 и образцов баз данных (скачать в [https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;D исплайланг = EN](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)). Самый простой способ настроить базу данных — использовать Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;D исплайланг = EN](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)) и присоединить файл базы данных `AdventureWorks.mdf`.

В этом примере предполагается, что экземпляр SQL Server 2005, экспресс-выпуск называется `SQLEXPRESS` и находится на том же компьютере, что и веб-сервер. Это также настройка по умолчанию. Если настройка отличается, необходимо адаптировать сведения о соединении для базы данных.

Чтобы активировать функциональные возможности ASP.NET AJAX и набора элементов управления, элемент управления `ScriptManager` должен быть размещен в любом месте страницы (но внутри &lt;`form`&gt;):

[!code-aspx[Main](using-cascadingdropdown-with-a-database-cs/samples/sample1.aspx)]

На следующем шаге требуются два элемента управления DropDownList. В этом примере мы используем сведения о поставщике и контактной информации из AdventureWorks, поэтому создадим один список для доступных поставщиков и один для доступных контактов:

[!code-aspx[Main](using-cascadingdropdown-with-a-database-cs/samples/sample2.aspx)]

Затем на страницу должны быть добавлены два расширителя CascadingDropDown. Один из них заполняет первый список (поставщики), а другой — второй список (Contacts). Необходимо задать следующие атрибуты:

- `ServicePath`: URL веб-службы, которая доставляет записи списка
- `ServiceMethod`: веб-метод, поставляющий записи списка
- `TargetControlID`: Идентификатор раскрывающегося списка
- `Category`: сведения о категории, которые передаются в веб-метод при вызове
- `PromptText`: текст, отображаемый при асинхронной загрузке данных списка с сервера
- `ParentControlID`: (необязательно) родительский раскрывающийся список, который запускает загрузку текущего списка

В зависимости от используемого языка программирования имя веб-службы в вопросе изменяется, но все остальные значения атрибутов одинаковы. Вот элемент CascadingDropDown для первого раскрывающегося списка:

[!code-aspx[Main](using-cascadingdropdown-with-a-database-cs/samples/sample3.aspx)]

Расширителям элемента управления для второго списка необходимо задать атрибут `ParentControlID`, чтобы при выборе записи в списке поставщиков триггер загрузил связанные элементы в список контактов.

[!code-aspx[Main](using-cascadingdropdown-with-a-database-cs/samples/sample4.aspx)]

Фактически работа выполняется в веб-службе, которая настроена следующим образом. Обратите внимание, что используется атрибут `[ScriptService]`, в противном случае ASP.NET AJAX не может создать прокси JavaScript для доступа к веб-методам из клиентского кода скрипта.

[!code-aspx[Main](using-cascadingdropdown-with-a-database-cs/samples/sample5.aspx)]

Сигнатура веб-методов, вызываемых CascadingDropDown, выглядит следующим образом:

[!code-csharp[Main](using-cascadingdropdown-with-a-database-cs/samples/sample6.cs)]

Поэтому возвращаемое значение должно быть массивом типа `CascadingDropDownNameValue` который определяется набором элементов управления. Метод `GetVendors()` довольно прост в реализации: код подключается к базе данных AdventureWorks и запрашивает первые 25 поставщиков. Первый параметр в конструкторе `CascadingDropDownNameValue` — это заголовок записи списка, второй — его значение (атрибут value в элементе HTML &lt;`option`&gt;). Ниже приведен код:

[!code-csharp[Main](using-cascadingdropdown-with-a-database-cs/samples/sample7.cs)]

Получение связанных контактов для поставщика (имя метода: `GetContactsForVendor()`) немного сложнее. Сначала необходимо определить поставщика, выбранного в первом раскрывающемся списке. Набор элементов управления определяет вспомогательный метод для этой задачи: метод `ParseKnownCategoryValuesString()` Возвращает элемент `StringDictionary` с данными раскрывающегося списка:

[!code-csharp[Main](using-cascadingdropdown-with-a-database-cs/samples/sample8.cs)]

По соображениям безопасности эти данные должны быть проверены первыми. Поэтому при наличии записи поставщика (поскольку свойство `Category` первого элемента CascadingDropDown имеет значение `"Vendor"`), можно получить идентификатор выбранного поставщика:

[!code-csharp[Main](using-cascadingdropdown-with-a-database-cs/samples/sample9.cs)]

Остальная часть метода довольно проста в прямом направлении. Идентификатор поставщика используется в качестве параметра для SQL-запроса, который получает все связанные контакты для этого поставщика. Опять же, метод возвращает массив типа `CascadingDropDownNameValue`.

[!code-csharp[Main](using-cascadingdropdown-with-a-database-cs/samples/sample10.cs)]

Загрузите страницу ASP.NET и спустя некоторое время, когда список поставщиков заполняется 25 записями. Выберите одну запись и обратите внимание на то, как второй раскрывающийся список заполняется данными.

[![первый список заполняется автоматически](using-cascadingdropdown-with-a-database-cs/_static/image2.png)](using-cascadingdropdown-with-a-database-cs/_static/image1.png)

Первый список заполняется автоматически ([щелкните, чтобы просмотреть изображение с полным размером](using-cascadingdropdown-with-a-database-cs/_static/image3.png))

[![второй список заполняется в соответствии с выбором в первом списке.](using-cascadingdropdown-with-a-database-cs/_static/image5.png)](using-cascadingdropdown-with-a-database-cs/_static/image4.png)

Второй список заполняется в соответствии с выбором в первом списке ([щелкните, чтобы просмотреть изображение с полным размером](using-cascadingdropdown-with-a-database-cs/_static/image6.png)).

> [!div class="step-by-step"]
> [Назад](filling-a-list-using-cascadingdropdown-cs.md)
> [Вперед](presetting-list-entries-with-cascadingdropdown-cs.md)
