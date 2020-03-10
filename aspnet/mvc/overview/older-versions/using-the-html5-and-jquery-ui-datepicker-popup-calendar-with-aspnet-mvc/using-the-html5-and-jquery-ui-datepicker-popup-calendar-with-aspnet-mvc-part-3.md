---
uid: mvc/overview/older-versions/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3
title: Использование HTML5 и всплывающего календаря DatePicker в элементе пользовательского интерфейса jQuery с ASP.NET MVC. часть 3 | Документация Майкрософт
author: Rick-Anderson
description: В этом учебнике вы узнаете, как работать с шаблонами редактора, шаблонами отображения и всплывающим календарем Datepicker пользовательского интерфейса jQuery в ASP.NET МВ...
ms.author: riande
ms.date: 08/29/2011
ms.assetid: 8f5f91ae-12d7-4cf3-ac09-4bb53d07ee60
msc.legacyurl: /mvc/overview/older-versions/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3
msc.type: authoredcontent
ms.openlocfilehash: b3249397e54e64538c4dc78e5fe8b94656e8962b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78433218"
---
# <a name="using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc---part-3"></a>Использование HTML5 и всплывающего календаря DatePicker в элементе пользовательского интерфейса jQuery с ASP.NET MVC. часть 3

по [Рик Андерсон (](https://twitter.com/RickAndMSFT)

> В этом учебнике вы узнаете, как работать с шаблонами редактора, шаблонами отображения и всплывающим календарем Datepicker пользовательского интерфейса jQuery в веб-приложении ASP.NET MVC.

## <a name="working-with-complex-types"></a>Работа со сложными типами

В этом разделе вы создадите класс Address и узнаете, как создать шаблон для его отображения.

В папке *Models* создайте новый файл класса с именем *Person.CS* , в котором будут размещены два типа: класс `Person` и класс `Address`. Класс `Person` будет содержать свойство, которое имеет тип `Address`. Тип `Address` является сложным типом, то есть не является одним из встроенных типов, таких как `int`, `string`или `double`. Вместо этого у него есть несколько свойств. Код для новых классов выглядит следующим образом:

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample1.cs)]

В контроллере `Movie` добавьте следующее действие `PersonDetail`, чтобы отобразить экземпляр Person:

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample2.cs)]

Затем добавьте следующий код в контроллер `Movie`, чтобы заполнить модель `Person` несколькими демонстрационными данными:

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample3.cs)]

Откройте файл *виевс\мовиес\персондетаил.кштмл* и добавьте следующую разметку для представления `PersonDetail`.

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample4.cshtml)]

Нажмите клавиши CTRL + F5, чтобы запустить приложение и выбрать *фильмы/персондетаил*.

Представление `PersonDetail` не содержит `Address` сложного типа, как видно на этом снимке экрана. (Адрес не отображается.)

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/_static/image1.png)

Данные модели `Address` не отображаются, так как это сложный тип. Чтобы отобразить сведения об адресе, снова откройте файл *виевс\мовиес\персондетаил.кштмл* и добавьте следующую разметку.

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample5.cshtml)]

Полная разметка для представления `PersonDetail` Now выглядит следующим образом:

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample6.cshtml)]

Запустите приложение еще раз и отобразите представление `PersonDetail`. Теперь отображаются сведения об адресе:

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/_static/image2.png)

### <a name="creating-a-template-for-a-complex-type"></a>Создание шаблона для сложного типа

В этом разделе вы создадите шаблон, который будет использоваться для визуализации `Address` сложного типа. При создании шаблона для типа `Address` ASP.NET MVC может автоматически использовать его для форматирования модели адресов в любом месте приложения. Это позволяет управлять визуализацией типа `Address` только из одного места в приложении.

В папке *views\shared\displaytemplates.* создайте строго типизированное частичное представление с именем **Address**:

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/_static/image3.png)

Нажмите кнопку **Добавить**, а затем откройте новый файл *виевс\шаред\дисплайтемплатес\аддресс.кштмл* . Новое представление содержит следующую созданную разметку:

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample7.cshtml)]

Запустите приложение и отобразите представление `PersonDetail`. На этот раз только что созданный шаблон `Address` используется для вывода `Address` сложного типа, поэтому отображение выглядит следующим образом:

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/_static/image4.png)

### <a name="summary-ways-to-specify-the-model-display-format-and-template"></a>Сводка. способы указания формата и шаблона представления модели

Вы видели, что можно указать формат или шаблон для свойства модели с помощью следующих подходов:

- Применение атрибута `DisplayFormat` к свойству в модели. Например, следующий код приводит к отображению даты без времени:

    [!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample8.cs)]
- Применение атрибута [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) к свойству в модели и указание типа данных. Например, следующий код приводит к отображению даты без времени.

    [!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample9.cs)]

    Если приложение содержит шаблон *Date. cshtml* в папке *Views\shared\displaytemplates.* или папке *виевс\мовиес\дисплайтемплатес* , то этот шаблон будет использоваться для визуализации свойства `DateTime`. В противном случае встроенная система создания шаблонов ASP.NET отображает свойство как дату.
- Создание шаблона вывода в папке *views\shared\displaytemplates.* или папке *виевс\мовиес\дисплайтемплатес* , имя которой соответствует типу данных, который необходимо отформатировать. Например, вы видели, что *виевс\шаред\дисплайтемплатес\датетиме.кштмл* использовался для отображения `DateTime` свойств в модели без добавления атрибута в модель и без добавления разметки в представления.
- Использование атрибута [UIHint](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.uihintattribute.uihint.aspx) в модели для указания шаблона для вывода свойства модели.
- Явное добавление имени шаблона отображения в вызов [HTML. DisplayFor](https://msdn.microsoft.com/library/ee407420.aspx) в представлении.

Используемый подход зависит от того, что необходимо сделать в приложении. Нередко приходится смешивать эти подходы, чтобы получить именно тот тип форматирования, который вам нужен.

В следующем разделе вы будете переключать шестеренки на несколько компонентов и переходить от настройки отображения данных для настройки способа их введения. Вы присоедините jQuery DatePicker к представлениям редактирования в приложении, чтобы предоставить изящен способ указания дат.

> [!div class="step-by-step"]
> [Назад](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2.md)
> [Вперед](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4.md)
