---
uid: mvc/overview/performance/profile-and-debug-your-aspnet-mvc-app-with-glimpse
title: Профилирование и отладка приложения ASP.NET MVC с помощью краткого описания | Документация Майкрософт
author: Rick-Anderson
description: Краткое описание — это расширяющееся и растущее семейство пакетов NuGet с открытым кодом, которое предоставляет подробные сведения о производительности, отладке и диагностике для ASP.NET a...
ms.author: riande
ms.date: 03/26/2015
ms.assetid: c205805f-efdd-4fa7-9616-f26eab180611
msc.legacyurl: /mvc/overview/performance/profile-and-debug-your-aspnet-mvc-app-with-glimpse
msc.type: authoredcontent
ms.openlocfilehash: d3689147a3bc3aa1f4180c377d2483a94bdd95a9
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78432900"
---
# <a name="profile-and-debug-your-aspnet-mvc-app-with-glimpse"></a>Профилирование и отладка приложения ASP.NET MVC с помощью Glimpse

по [Рик Андерсон (](https://twitter.com/RickAndMSFT)

> Краткое описание — это расширяющееся и растущее семейство пакетов NuGet с открытым кодом, которое предоставляет подробные сведения о производительности, отладке и диагностике для приложений ASP.NET. Это тривиальный способ установки, упрощения и быстрого ускорения, а также отображает ключевые метрики производительности в нижней части каждой страницы. Она позволяет детализировать приложение, если вам нужно узнать, что происходит на сервере. В кратком обзоре содержится очень важная информация, которую мы рекомендуем использовать на протяжении всего цикла разработки, включая тестовую среду Azure. Хотя [Fiddler](http://www.telerik.com/fiddler) и [средства разработки F-12](https://msdn.microsoft.com/library/ie/gg589512(v=vs.85).aspx) предоставляют представление на стороне клиента, в кратком обзоре представлено подробное представление о сервере. В этом учебнике основное внимание уделяется использованию пакетов ASP.NET MVC и EF, но доступны многие другие пакеты. Где это возможно, я буду ссылаться на соответствующие [документы с краткими](http://getglimpse.com/Docs/) сведениями, которые я могу поддерживать. «Краткий обзор» — это проект с открытым исходным кодом. Вы также можете участвовать в исходном коде и документах.

- [Установка краткого описания](#ig)
- [Включение краткого описания для localhost](#eg)
- [Вкладка временной шкалы](#Time)
- [Привязка модели](#mb)
- [Маршруты](#route)
- [Использование краткого описания в Azure](#da)
- [Дополнительные ресурсы](#addRes)

<a id="ig"></a>
## <a name="installing-glimpse"></a>Установка краткого описания

Вы можете установить его с помощью консоли диспетчера пакетов NuGet или консоли **Управление пакетами NuGet** . Для этой демонстрации я устанавливаю пакеты Mvc5 и EF6:

![Установка краткого описания из NuGet DLG](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image1.png)

Поиск *краткого описания. EF*

![Краткий обзор EF из NuGet Install DLG](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image2.png)

Выбрав **установленные пакеты**, можно увидеть установленные зависимые модули:

![Установленные краткие пакеты из диалогового окна](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image3.png)

Следующие команды устанавливают краткий обзор модулей MVC5 и EF6 из консоли диспетчера пакетов.

[!code-console[Main](profile-and-debug-your-aspnet-mvc-app-with-glimpse/samples/sample1.cmd)]

<a id="eg"></a>
## <a name="enable-glimpse-for-localhost"></a>Включение краткого описания для localhost

Перейдите в раздел http://localhost:&lt;p порт #&gt;/глимпсе.аксд и нажмите кнопку <strong>включить краткий</strong> обзор.

![Страница краткого axd](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image4.png)

Если панель "Избранное" отображается, можно перетащить кнопки краткого описания и добавить их в качестве закладок:

![Кнопки с краткими обзорами IE](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image5.png)

Теперь можно перемещаться по приложению, и в нижней части страницы отображается **заголовков** (HUD).

![Страница диспетчера контактов с HUD](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image6.png)

На [странице краткий обзор HUD](http://getglimpse.com/Docs/Heads-up-Display) содержатся сведения о времени, показанные выше. Ненавязчивые данные производительности, отображаемые HUD, могут немедленно уведомить вас о проблеме, прежде чем перейти к циклу тестирования. Если щелкнуть &quot;g&quot; в правом нижнем углу, откроется панель «Обзор»:

![Панель краткого описания](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image7.png)

На приведенном выше рисунке выбрана [вкладка выполнение](http://getglimpse.com/Docs/Execution-Tab) , в которой отображаются сведения о времени действий и фильтров в конвейере. На этапе 6 конвейера можно увидеть [таймер фильтра контрольных](http://www.nuget.org/packages/StopWatch/) данных. Хотя мой таймер неплотности может предоставить полезные данные о профиле и времени, он пропустил все время, затраченное на авторизацию и визуализацию представления. Вы можете прочитать сведения о своем таймере в [профиле и о том, как приложение ASP.NET MVC будет](https://blogs.msdn.com/b/webdev/archive/2014/07/29/profile-and-time-your-asp-net-mvc-app-all-the-way-to-azure.aspx)доступно в Azure. На странице [вкладок](http://getglimpse.com/Docs/Tabs) приводятся ссылки на подробные сведения о каждой вкладке.

<a id="Time"></a>
## <a name="the-timeline-tab"></a>Вкладка временной шкалы

Я изменил Dykstra)ный [учебник по EF 6/MVC 5](../getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md) с помощью следующего изменения кода в контроллере инструкторов:

[!code-csharp[Main](profile-and-debug-your-aspnet-mvc-app-with-glimpse/samples/sample2.cs?highlight=1,20-31)]

Приведенный выше код позволяет мне передать строку запроса (`eager`) для управления загрузкой данных. На приведенном ниже рисунке используется явная загрузка, и на странице времени отображаются все регистрации, загруженные в метод действия `Index`.

![явная загрузка](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image8.png)

В следующем коде указан параметр "безотлагательная", и каждая регистрация извлекается после вызова представления `Index`:

![указана безотлагательная](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image9.png)

Для получения подробных сведений о времени можно навести указатель мыши на отрезок времени:

![Наведите указатель мыши, чтобы просмотреть подробные сведения о времени](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image10.png)

<a id="mb"></a>
## <a name="model-binding"></a>Привязка модели

На [вкладке Привязка модели](http://getglimpse.com/Docs/Model-Binding-Tab) содержится множество сведений, которые помогут понять, как связаны переменные форм и почему некоторые из них не привязаны как можно скорее. На рисунке ниже показана **?** , который можно щелкнуть для открытия краткой страницы справки для этой функции.

![Представление привязки модели краткого представления](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image11.png)

<a id="route"></a>
## <a name="routes"></a>Маршруты

 Вкладка Общие маршруты поможет вам отлаживать и понимать маршрутизацию. На рисунке ниже выбран маршрут продукта (и он отображается зеленым цветом, в кратком соглашении). ![выбрано имя продукта](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image12.png) ограничения маршрута, также отображаются области и маркеры данных. Дополнительные сведения см. в разделе [краткие маршруты](http://getglimpse.com/Docs/Routes-Tab) и [Маршрутизация АТРИБУТОВ в ASP.NET MVC 5](https://blogs.msdn.com/b/webdev/archive/2013/10/17/attribute-routing-in-asp-net-mvc-5.aspx) . 

<a id="da"></a>
## <a name="using-glimpse-on-azure"></a>Использование краткого описания в Azure

В краткой политике безопасности по умолчанию только данные краткости отображаются только с локального узла. Вы можете изменить эту политику безопасности, чтобы просматривать эти данные на удаленном сервере (например, в веб-приложении Azure). Для тестовых сред в Azure добавьте выделенную метку в нижнюю часть файла *Web. config* , чтобы включить параметр «краткий обзор»:

[!code-xml[Main](profile-and-debug-your-aspnet-mvc-app-with-glimpse/samples/sample3.xml?highlight=2-6)]

С учетом этого изменения любой пользователь может видеть данные на удаленном сайте. Рассмотрите возможность добавления разметки выше в профиль публикации, чтобы она была развернута только при использовании этого профиля публикации (например, в тестовом профиле Azure). Чтобы ограничить данные краткого представления, мы добавим роль `canViewGlimpseData` и только пользователи этой роли могли просматривать данные о выпуске.

Удалите комментарии из файла *GlimpseSecurityPolicy.CS* и измените вызов [IsInRole](https://msdn.microsoft.com/library/system.security.principal.iprincipal.isinrole(v=vs.110).aspx) с `Administrator` на роль `canViewGlimpseData`:

[!code-csharp[Main](profile-and-debug-your-aspnet-mvc-app-with-glimpse/samples/sample4.cs?highlight=6)]

> [!WARNING]
> Безопасность. Расширенные данные, предоставляемые в кратком обзоре, могут предоставлять безопасность приложения. Корпорация Майкрософт не выполнила аудит безопасности "краткий обзор" для использования в приложениях производства.

Дополнительные сведения о добавлении ролей см. в руководстве [Развертывание веб-приложения Secure ASP.NET MVC 5 с помощью членства, OAuth и базы данных SQL в Azure](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/) .

<a id="addRes"></a>
## <a name="additional-resources"></a>Дополнительные ресурсы

- [Развертывание безопасного приложения ASP.NET MVC 5 с членством, OAuth и базой данных SQL в Azure](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/)
- [Краткий обзор конфигурации](http://getglimpse.com/Docs/Configuration) — страница документации по настройке вкладок, политика среды выполнения, ведение журнала и многое другое.
