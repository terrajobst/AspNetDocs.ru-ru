---
uid: mvc/overview/older-versions-1/overview/understanding-models-views-and-controllers-cs
title: Основные сведения о моделях, представлениях иC#контроллерах () | Документация Майкрософт
author: StephenWalther
description: Не путать с моделями, представлениями и контроллерами? В этом руководстве Стивен Вальтер содержит сведения о различных частях приложения ASP.NET MVC.
ms.author: riande
ms.date: 08/19/2008
ms.assetid: 87313792-0a96-4caf-89fc-1457d54e5c1e
msc.legacyurl: /mvc/overview/older-versions-1/overview/understanding-models-views-and-controllers-cs
msc.type: authoredcontent
ms.openlocfilehash: 57dc82d02d38adc2514aa2c02c6f156ed0fb88a6
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78486090"
---
# <a name="understanding-models-views-and-controllers-c"></a>Общие сведения о моделях, представлениях и контроллерах (C#)

по [Стивен Вальтер](https://github.com/StephenWalther)

> Не путать с моделями, представлениями и контроллерами? В этом руководстве Стивен Вальтер содержит сведения о различных частях приложения ASP.NET MVC.

В этом учебнике представлен общий обзор моделей, представлений и контроллеров ASP.NET MVC. Иными словами, здесь объясняются M, V и C в ASP.NET MVC.

Прочитав этот учебник, вы должны понимать, как различные части приложения MVC ASP.NET работают вместе. Следует также понимать, как архитектура приложения ASP.NET MVC отличается от приложения ASP.NET Web Forms или приложения Active Server Pages.

## <a name="the-sample-aspnet-mvc-application"></a>Пример приложения ASP.NET MVC

Шаблон по умолчанию Visual Studio для создания веб-приложений ASP.NET MVC включает в себя очень простой пример приложения, который можно использовать для понимания различных частей приложения ASP.NET MVC. В этом руководстве мы используем это простое приложение.

Вы создадите новое приложение ASP.NET MVC с шаблоном MVC, запустив Visual Studio 2008 и выбрав файл параметров меню, новый проект (см. рис. 1). В диалоговом окне Новый проект выберите предпочитаемый язык программирования в разделе Типы проектов (Visual Basic C#или) и выберите **веб-приложение ASP.NET MVC** в разделе Шаблоны. Нажмите кнопку "ОК".

[Диалоговое окно ![нового проекта](understanding-models-views-and-controllers-cs/_static/image1.jpg)](understanding-models-views-and-controllers-cs/_static/image1.png)

**Рис. 01**. диалоговое окно создания проекта ([щелкните, чтобы просмотреть изображение с полным размером](understanding-models-views-and-controllers-cs/_static/image2.png))

При создании нового приложения ASP.NET MVC появляется диалоговое окно **Создание проекта модульного теста** (см. рис. 2). Это диалоговое окно позволяет создать отдельный проект в решении для тестирования приложения ASP.NET MVC. Выберите вариант **нет, не создавать проект модульного теста** и нажмите кнопку **ОК** .

[Диалоговое окно создания модульного теста ![](understanding-models-views-and-controllers-cs/_static/image2.jpg)](understanding-models-views-and-controllers-cs/_static/image3.png)

**Рис. 02**. диалоговое окно "Создание модульного теста[" (щелкните, чтобы просмотреть изображение с полным размером](understanding-models-views-and-controllers-cs/_static/image4.png))

После создания нового приложения MVC ASP.NET. В окне обозреватель решений вы увидите несколько папок и файлов. В частности, вы увидите три папки с именами Models, Views и Controllers. Как вы можете предположить из имен папок, эти папки содержат файлы для реализации моделей, представлений и контроллеров.

Если развернуть папку Controllers, появится файл с именем AccountController.cs и файл с именем HomeController.cs. Если развернуть папку Views, вы увидите три вложенных папки с именем Account, Home и Shared. Если развернуть корневую папку, вы увидите два дополнительных файла с именами About. aspx и index. aspx (см. рис. 3). Эти файлы составляют пример приложения, который входит в состав шаблона по умолчанию ASP.NET MVC.

[![обозреватель решений окно](understanding-models-views-and-controllers-cs/_static/image3.jpg)](understanding-models-views-and-controllers-cs/_static/image5.png)

**Рис. 03**. окно Обозреватель решений ([щелкните, чтобы просмотреть изображение с полным размером](understanding-models-views-and-controllers-cs/_static/image6.png))

Чтобы запустить пример приложения, выберите пункт меню **Отладка, начать отладку**. Кроме того, можно нажать клавишу F5.

При первом запуске приложения ASP.NET открывается диалоговое окно на рис. 4, в котором рекомендуется включить режим отладки. Нажмите кнопку ОК, и приложение будет запущено.

[диалоговое окно ![отладки не включено](understanding-models-views-and-controllers-cs/_static/image4.jpg)](understanding-models-views-and-controllers-cs/_static/image7.png)

**Рис. 04**. диалоговое окно "Отладка не включена" ([щелкните, чтобы просмотреть изображение с полным размером](understanding-models-views-and-controllers-cs/_static/image8.png))

При запуске приложения ASP.NET MVC Visual Studio запускает приложение в веб-браузере. Пример приложения состоит только из двух страниц: страницы индекса и страницы About. При первом запуске приложения отображается страница индекса (см. рис. 5). Можно переходить на страницу About, щелкнув ссылку меню в правом верхнем углу приложения.

[![страницы индекса](understanding-models-views-and-controllers-cs/_static/image10.png)](understanding-models-views-and-controllers-cs/_static/image9.png)

**Рис. 05**. страница индекса ([щелкните, чтобы просмотреть изображение с полным размером](understanding-models-views-and-controllers-cs/_static/image11.png))

Обратите внимание на URL-адреса в адресной строке браузера. Например, если щелкнуть ссылку меню About, URL-адрес в адресной строке браузера изменится на **/Хоме/абаут**.

Если закрыть окно браузера и вернуться в Visual Studio, вы не сможете найти файл с путем "Домашняя страница" или "о программе". Файлы не существуют. Как такое возможно?

## <a name="a-url-does-not-equal-a-page"></a>URL-адрес не равен странице

При создании традиционного приложения веб-форм ASP.NET или приложения Active Server Pages существует однозначное соответствие между URL-адресом и страницей. Если вы запрашиваете страницу с именем Сомепаже. aspx с сервера, то лучше быть страницей на диске с именем Сомепаже. aspx. Если файл Сомепаже. aspx не существует, возникает некрасивое сообщение об ошибке **404 — страница не найдена** .

При создании приложения ASP.NET MVC, напротив, отсутствует соответствие между URL-адресом, введенным в адресную строку браузера, и файлами, найденными в приложении. В приложении ASP.NET MVC URL-адрес соответствует действию контроллера, а не странице на диске.

В традиционном приложении ASP.NET или ASP запросы к браузеру сопоставлены со страницами. В приложении ASP.NET MVC, напротив, запросы браузера сопоставляются с действиями контроллера. Приложение веб-форм ASP.NET является ориентированным на содержимое. Приложение ASP.NET MVC, напротив, является ориентированным на логику приложения.

## <a name="understanding-aspnet-routing"></a>Основные сведения о маршрутизации ASP.NET

Запрос браузера сопоставляется с действием контроллера с помощью функции ASP.NET Framework, именуемой *маршрутизацией ASP.NET*. ASP.NET Маршрутизация используется платформой ASP.NET MVC для *маршрутизации* входящих запросов к действиям контроллера.

Маршрутизация ASP.NET использует таблицу маршрутов для обработки входящих запросов. Эта таблица маршрутов создается при первом запуске веб-приложения. Таблица маршрутов настроена в файле Global. asax. Файл Global. asax MVC по умолчанию содержится в листинге 1.

**Листинг 1-Global. asax**

[!code-csharp[Main](understanding-models-views-and-controllers-cs/samples/sample1.cs)]

При первом запуске приложения ASP.NET вызывается метод Application\_Start (). В листинге 1 Этот метод вызывает метод Регистерраутес (), а метод Регистерраутес () создает таблицу маршрутов по умолчанию.

Таблица маршрутов по умолчанию состоит из одного маршрута. Этот маршрут по умолчанию разбивает все входящие запросы на три сегмента (сегмент URL-адреса является любым символом обратной косой черты). Первый сегмент сопоставляется с именем контроллера, второй сегмент сопоставляется с именем действия, а последний сегмент сопоставляется с параметром, передаваемым в действие с именем ID.

Например, рассмотрим следующий URL-адрес:

/Product/Details/3

Этот URL-адрес разбивается на три параметра следующим образом:

Controller = продукт

Действие = сведения

ИД = 3

Маршрут по умолчанию, определенный в файле Global. asax, содержит значения по умолчанию для всех трех параметров. Контроллером по умолчанию является Home, действием по умолчанию является index, а идентификатором по умолчанию является пустая строка. Учитывая эти значения по умолчанию, рассмотрим синтаксический анализ следующего URL-адреса:

/Employee

Этот URL-адрес разбивается на три параметра следующим образом:

Контроллер = сотрудник

действие = индекс

Идентификатор =

Наконец, при открытии приложения ASP.NET MVC без указания URL-адреса (например, `http://localhost`) URL-адрес анализируется следующим образом:

контроллер = Главная

действие = индекс

Идентификатор =

Запрос направляется в действие index () в классе HomeController.

## <a name="understanding-controllers"></a>Основные сведения об контроллерах

Контроллер отвечает за управление способом взаимодействия пользователя с приложением MVC. Контроллер содержит логику управления потоком для приложения ASP.NET MVC. Контроллер определяет ответ, отправляемый пользователю, когда пользователь выполняет запрос к браузеру.

Контроллер — это просто класс (например, Visual Basic или C# класс). Пример приложения ASP.NET MVC включает в себя контроллер с именем HomeController.cs, расположенный в папке Controllers. Содержимое файла HomeController.cs воспроизводится в листинге 2.

**Листинг 2. HomeController.cs**

[!code-csharp[Main](understanding-models-views-and-controllers-cs/samples/sample2.cs)]

Обратите внимание, что у HomeController есть два метода с именами index () и About (). Эти два метода соответствуют двум действиям, предоставляемым контроллером. URL-адрес/Хоме/индекс вызывает метод HomeController. index (), а URL-адрес/Хоме/абаут вызывает метод HomeController. About ().

Любой открытый метод в контроллере предоставляется как действие контроллера. Необходимо соблюдать осторожность. Это означает, что любой открытый метод, содержащийся в контроллере, может быть вызван любым пользователем, у которого есть доступ к Интернету, путем ввода правильного URL-адреса в браузере.

## <a name="understanding-views"></a>Основные сведения о представлениях

Два действия контроллера, предоставляемые классом HomeController, index () и About (), возвращают представление. Представление содержит разметку HTML и содержимое, отправляемое в браузер. Представление является эквивалентом страницы при работе с ASP.NET приложением MVC.

Необходимо создать представления в правильном расположении. Действие HomeController. index () возвращает представление, расположенное по следующему пути:

\Views\Home\Index.aspx

Действие HomeController. About () возвращает представление, расположенное по следующему пути:

\Views\Home\About.aspx

В общем случае, если требуется возвратить представление для действия контроллера, необходимо создать вложенную папку в папке Views с тем же именем, что и у контроллера. Во вложенной папке необходимо создать файл. aspx с тем же именем, что и действие контроллера.

Файл в листинге 3 содержит представление About. aspx.

**Листинг 3 — About. aspx**

[!code-aspx[Main](understanding-models-views-and-controllers-cs/samples/sample3.aspx)]

Если пропустить первую строку в листинге 3, большая часть представления состоит из стандартного кода HTML. Вы можете изменить содержимое представления, введя нужный HTML-код.

Представление очень похоже на страницу Active Server страниц или веб-форм ASP.NET. Представление может содержать HTML-содержимое и скрипты. Скрипты можно писать на любом языке программирования .NET (например, C# или Visual Basic .NET). Скрипты используются для просмотра динамического содержимого, например данных базы данных.

## <a name="understanding-models"></a>Основные сведения о моделях

Мы обсуждали контроллеры, и мы обсуждали представления. Последний раздел, который нам нужно обсудить, — модели. Что такое модель MVC?

Модель MVC содержит всю логику приложения, которая не содержится в представлении или контроллере. Модель должна содержать всю бизнес-логику приложения, логику проверки и логику доступа к базе данных. Например, если для доступа к базе данных используется Microsoft Entity Framework, то в папке Models (модели) необходимо создать классы Entity Framework (файл EDMX).

Представление должно содержать только логику, связанную с созданием пользовательского интерфейса. Контроллер должен содержать только минимальную логику, необходимую для возврата правильного представления или перенаправить пользователя в другое действие (управление потоком). Все остальное должно содержаться в модели.

Как правило, необходимо стремиться к моделям FAT и фактам контроллерам. Методы контроллера должны содержать всего несколько строк кода. Если действие контроллера имеет слишком большой формат FAT, следует рассмотреть возможность перемещения логики в новый класс в папке Models.

## <a name="summary"></a>Сводка

В этом руководстве предоставлен общий обзор различных частей веб-приложения ASP.NET MVC. Вы узнали, как ASP.NET Routing сопоставляет входящие запросы браузера с определенными действиями контроллера. Вы узнали, как контроллеры позволяют управлять возвратом представлений в браузер. Наконец, вы узнали, как модели содержат бизнес-правила, проверку и логику доступа к базе данных.
