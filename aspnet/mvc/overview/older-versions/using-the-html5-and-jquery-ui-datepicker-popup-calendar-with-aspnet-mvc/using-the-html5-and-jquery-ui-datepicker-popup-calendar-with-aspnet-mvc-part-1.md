---
uid: mvc/overview/older-versions/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-1
title: Использование HTML5 и всплывающего календаря DatePicker в элементе пользовательского интерфейса jQuery с ASP.NET MVC. часть 1 | Документация Майкрософт
author: Rick-Anderson
description: В этом учебнике вы узнаете, как работать с шаблонами редактора, шаблонами отображения и всплывающим календарем Datepicker пользовательского интерфейса jQuery в ASP.NET МВ...
ms.author: riande
ms.date: 08/29/2011
ms.assetid: c23d27f7-b0cf-44f2-8445-fb69e045c674
msc.legacyurl: /mvc/overview/older-versions/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-1
msc.type: authoredcontent
ms.openlocfilehash: c1c2380f24c72f6aabaaacaf975e95288a384ff1
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78433290"
---
# <a name="using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc---part-1"></a>Использование HTML5 и всплывающего календаря DatePicker в элементе пользовательского интерфейса jQuery с ASP.NET MVC. часть 1

по [Рик Андерсон (](https://twitter.com/RickAndMSFT)

> В этом учебнике вы узнаете, как работать с шаблонами редактора, шаблонами отображения и всплывающим календарем Datepicker пользовательского интерфейса jQuery в веб-приложении ASP.NET MVC.

В этом учебнике вы узнаете, как работать с шаблонами редактора, шаблонами отображения и [всплывающим календарем Datepicker пользовательского интерфейса](http://plugins.jquery.com/project/datepicker) jQuery в веб-приложении ASP.NET MVC. В этом руководстве можно использовать Microsoft Visual Web Developer 2010 Express с пакетом обновления 1 (&quot;Visual Web Developer&quot;), который является бесплатной версией Microsoft Visual Studio или можно использовать Visual Studio 2010 с пакетом обновления 1 (SP1), если у вас уже есть.

Прежде чем начать, убедитесь, что установлены предварительные требования, перечисленные ниже. Чтобы установить все эти компоненты, щелкните следующую ссылку: [установщик веб-платформы](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack). Кроме того, вы можете отдельно установить необходимое программное обеспечение, используя следующие ссылки:

- [Предварительные требования для Visual Studio Web Developer Express SP1](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
- [Обновление инструментов ASP.NET MVC 3](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
- [SQL Server Compact 4,0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(поддержка времени выполнения и средств)

Если вы используете Visual Studio 2010 вместо Visual Web Developer, установите необходимые компоненты, щелкнув следующую ссылку: [Предварительные требования для Visual studio 2010](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack).

В этом учебнике предполагается, что вы выполнили учебник [Начало работы в MVC 3](../getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) или вы знакомы с разработкой ASP.NET MVC. Это руководство начинается с готового проекта из учебника [Начало работы with MVC 3](../getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) .

В этом руководстве показан код C#в. Однако [начальный проект](https://archive.msdn.microsoft.com/Project/Download/FileDownload.aspx?ProjectName=aspnetmvcsamples&amp;DownloadId=15800) и завершенный проект также доступны в Visual Basic.

Проект Visual Studio с C# исходным кодом и Visual Basic доступен для этого раздела: [download](https://archive.msdn.microsoft.com/Project/Download/FileDownload.aspx?ProjectName=aspnetmvcsamples&amp;DownloadId=15800).

### <a name="what-youll-build"></a>Что вы создадите

Шаблоны (в частности, шаблоны редактирования и отображения) добавляются в простое приложение с перечнем фильмов, созданное в учебнике [Начало работы with MVC 3](../getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) . Вы также добавите всплывающий календарь [DatePicker элемента jQuery](http://jqueryui.com/demos/datepicker/) , чтобы упростить процесс ввода дат. На следующем снимке экрана показано измененное приложение с отображаемым всплывающим календарем Datepicker пользовательского интерфейса jQuery.

![Завершенная jQuery](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-1/_static/image1.png)

### <a name="skills-youll-learn"></a>Чему вы научитесь

В этом учебнике вы узнаете:

- Использование атрибутов из пространства имен [Annotations](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx) для управления форматом данных при их отображении и в режиме редактирования.
- Создание шаблонов (редактирование и отображение шаблонов) для управления форматированием данных.
- Добавление [DatePicker пользовательского интерфейса jQuery](http://jqueryui.com/demos/datepicker/) в качестве способа ввода полей даты.

### <a name="getting-started"></a>Приступая к работе

Если вы еще не получили приложение со списком фильмов из начального проекта, скачайте его: 

* [Скачайте](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098).
* В проводнике Windows щелкните правой кнопкой мыши файл *MvcMovie. zip* и выберите пункт **свойства**. 
* В диалоговом окне **Свойства MvcMovie. zip** выберите **разблокировать**. Разблокировка устраняет предупреждение системы безопасности, выводимое при попытке использовать *ZIP-файл* , загруженный из Интернета.

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-1/_static/image2.png)

Щелкните правой кнопкой мыши файл *MvcMovie. zip* и выберите **извлечь все** , чтобы распаковать файл. В Visual Web Developer или Visual Studio 2010 откройте файл *мвкмовиекс\_Tu. sln* .

В **Обозреватель решений**дважды щелкните *Views\Shared\\_layout. cshtml* , чтобы открыть его. Измените заголовок `H1` из **приложения роли MVC** на **Movie jQuery**. Нажмите клавиши CTRL + F5, чтобы запустить приложение, и перейдите на вкладку **Главная** , чтобы перейти к методу `Index` контроллера фильмов. Чтобы испытать приложение, щелкните ссылку Edit ( **изменить** ) и ссылка на **сведения** для одного из фильмов. Обратите внимание, что в представлениях "индекс", "Редактирование" и "подробности" Дата и цена выпуска отлично отформатированы:

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-1/_static/image3.png)

Форматирование даты и цены является результатом использования атрибута [DisplayFormat](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx) в свойствах класса `Movie`.

Откройте файл *Movie.CS* и закомментируйте атрибут `DisplayFormat` в свойствах `ReleaseDate` и `Price`. Итоговый класс `Movie` выглядит следующим образом:

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-1/samples/sample1.cs)]

Нажмите сочетание клавиш CTRL + F5 еще раз, чтобы запустить приложение, и перейдите на вкладку **Главная** , чтобы просмотреть список фильмов. На этот раз в дату выпуска отображается дата и время, а в поле Цена больше не отображается символ валюты. Изменения в классе `Movie` отменяют неприятное форматирование, которое вы видели ранее, но это можно исправить чуть позже.

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-1/_static/image4.png)

### <a name="using-the-dataannotations-datatype-attribute-to-specify-the-data-type"></a>Использование атрибута DataType в заметках для указания типа данных

Замените атрибут `DisplayFormat` с комментарием для `ReleaseDate` свойства атрибутом [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) с помощью перечисления `Date`. Замените атрибут `DisplayFormat` для свойства `Price` еще раз атрибутом [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) , в этот раз используя перечисление `Currency`. Вот как выглядит завершенный код:

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-1/samples/sample2.cs)]

Запустите приложение. Теперь Дата выпуска и свойства цены имеют правильный формат (то есть используются соответствующие форматы даты и валюты). Атрибут [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) предоставляет метаданные типа для встроенных шаблонов MVC ASP.NET, чтобы поля отображались в правильном формате. Использование атрибута `DataType` предпочтительнее использования атрибута `DisplayFormat`, изначально находился в коде, поскольку атрибут `DataType` делает эту модель более гибкой для целей, таких как интернационализации.

В следующем разделе вы узнаете, как создавать настраиваемые шаблоны для отображения полей дат.

> [!div class="step-by-step"]
> [Дальше](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2.md)
