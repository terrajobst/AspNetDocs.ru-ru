---
uid: whitepapers/aspnet-and-web-tools-20122-release-notes
title: Заметки о выпуске ASP.NET and Web Tools 2012,2 | Документация Майкрософт
author: rick-anderson
description: Заметки о выпуске для ASP.NET and Web Tools 2012,2.
ms.author: riande
ms.date: 02/14/2013
ms.assetid: bdb18d02-9f61-4676-836d-6fdea94f9282
msc.legacyurl: /whitepapers/aspnet-and-web-tools-20122-release-notes
msc.type: content
ms.openlocfilehash: a4ea1d7c146309e1d5e8be944d496e9fd87bca3e
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78420252"
---
# <a name="aspnet-and-web-tools-20122-release-notes"></a>ASP.NET и веб-инструменты 2012.2 — заметки о выпуске

> В этом документе описывается выпуск ASP.NET and Web Tools 2012,2. Это обновление веб-средств Visual Studio и ASP.NET.

- [Заметки об установке](#_Installation)
- [Документация](#_Documentation)
- [Поддержка](#_Support)
- [Требования к программному обеспечению](#_Software_Requirements)
- [Новые возможности в ASP.NET and Web Tools 2012,2](#_New_Features_in)

    - [инструментарий](#_Tooling);
    - [Веб-публикация](#_Web_Publishing)
    - [Шаблоны MVC ASP.NET](#_Templates)
    - [ASP.NET Web API](#_ASP.NET_Web_API)

    - [ASP.NET SignalR](#_ASP.NET_SignalR)
    - [ASP.NET понятные URL-адреса](#_ASP.NET_Friendly_URLs)
- [Известные проблемы и критические изменения](#_Known_Issues_and)

<a id="_Installation"></a>
## <a name="installation-notes"></a>Замечания по установке

ASP.NET and Web Tools 2012,2 для Visual Studio 2012 можно установить с помощью [установщика веб-платформы](https://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=ASPDOTNETandWebTools2012_2). Это обновление для Visual Studio 2012 или Visual Studio Express 2012 для Web, что является обязательным. Если Visual Studio не установлена, будет установлена Visual Studio Express 2012 для Web.

Можно также установить ASP.NET and Web Tools 2012,2 вручную. Необходимо установить Visual Studio 2012 или Visual Studio Express 2012 для Web. Затем выполните следующие действия. 

1. Скачайте установщик [ASP.NET и Web frameworks 2012,2](https://download.microsoft.com/download/6/5/6/6562AFBE-9503-4E64-970C-1427133FCD73/AspNetWebTools2012Setup.exe) из центра загрузки.
2. При появлении запроса нажмите кнопку выполнить. Кроме того, файл можно сохранить для последующего запуска.
3. Проверьте версию Visual Studio, которую вы будете обновлять. Это можно сделать, запустив Visual Studio, которую вы хотите обновить. Затем щелкните пункт меню "Справка".   
    ![](aspnet-and-web-tools-20122-release-notes/_static/image1.jpg)
4. Если вы видите пункт меню &quot;о Microsoft Visual Studio 2012 для Web&quot; Скачайте [веб-Средства для разработчиков 2012,2-Visual Studio Express 2012 для Web](https://go.microsoft.com/fwlink/?LinkID=282228). В противном случае Скачайте [веб-Средства для разработчиков 2012,2 — Visual Studio 2012](https://go.microsoft.com/fwlink/?LinkID=282228).
5. При появлении запроса нажмите кнопку выполнить. Кроме того, файл можно сохранить для последующего запуска.

> [!NOTE]
> Выпуск ASP.NET and Web Tools 2012,2 не включает SQL Server Data Tools. SQL Server и базы данных SQL Windows Azure предоставляют более широкий набор средств для работы с базами данных, включая автономную разработку проекта, сравнение схем и расширенные возможности развертывания баз данных. Для получения дополнительных сведений или установки SQL Server Data Tools посетите [https://go.microsoft.com/fwlink/?LinkID=237127](https://go.microsoft.com/fwlink/?LinkID=237127).

<a id="_Documentation"></a>
## <a name="documentation"></a>Документация

Руководства и другие сведения о ASP.NET and Web Tools 2012,2 доступны на веб-сайте ASP.NET (https://www.asp.net).

<a id="_Support"></a>
## <a name="support"></a>Поддержка

ASP.NET and Web Tools 2012,2 официально выпущена и поддерживается. Вы можете использовать стандартный канал поддержки. Вы также можете размещать вопросы на форумах ASP.NET ([https://forums.asp.net/](https://forums.asp.net/)), где участники сообщества ASP.NET часто могут предоставлять неофициальную поддержку.

<a id="_Software_Requirements"></a>
## <a name="software-requirements"></a>Требования к программному обеспечению

Для ASP.NET and Web Tools 2012,2 требуется Visual Studio 2012 или Visual Studio Express 2012 для Web.

<a id="_New_Features_in"></a>
## <a name="new-features-in-aspnet-and-web-tools-20122"></a>Новые возможности в ASP.NET and Web Tools 2012,2

В этом разделе описаны функции, которые появились в выпуске ASP.NET and Web Tools 2012,2.

<a id="_Tooling"></a>
### <a name="tooling"></a>Инструменты

- Инспектор страниц 

    - Поддерживает сопоставление выбора JavaScript, позволяя Инспектор страниц сопоставлять элементы, динамически добавленные на страницу, в соответствующий код JavaScript.
    - Возможность просмотра обновлений CSS в режиме реального времени.
    - Дополнительные сведения см. [в статье сопоставление CSS для автосинхронизации и выбора JavaScript в инспектор страниц](https://blogs.msdn.com/b/webdev/archive/2012/12/14/css-auto-sync-and-javascript-selection-mapping-in-page-inspector.aspx).
- Редактор 

    - Поддержка выделения синтаксиса для CoffeeScript, Мустаче, заголовки и Жсрендер.
    - Редактор HTML предоставляет IntelliSense для привязок маскирования.
    - Меньшее количество изменений и поддержка компилятора, позволяющих создавать динамические CSS с меньшим количеством.
    - Вставьте JSON как класс .NET. Используйте эту специальную команду вставки, чтобы вставить JSON C# в файл кода или VB.NET, и Visual Studio автоматически создаст классы .NET, выводимые из JSON.
- Поддержка эмулятора мобильных устройств добавляет обработчики расширения, чтобы сторонние эмуляторы можно было устанавливать в качестве VSIX. Установленные Эмуляторы будут отображаться в раскрывающемся списке F5, чтобы разработчики могли просматривать свои веб-сайты на различных мобильных устройствах. Дополнительные сведения об этой функции см. в записи блога Скотта Hanselman по [новой интеграции бровсерстакк с Visual Studio](http://www.hanselman.com/blog/CrossBrowserDebuggingIntegratedIntoVisualStudioWithBrowserStack.aspx).

<a id="_Web_Publishing"></a>
### <a name="web-publishing"></a>Веб-публикация

- Проекты веб-сайтов теперь имеют те же возможности публикации, что и проекты веб-приложений, включая публикацию на веб-сайтах Windows Azure.
- Выборочная &#8211; публикация для одного или нескольких файлов можно выполнить следующие действия (после публикации в веб-развертывание конечной точке): 

    - Опубликовать выбранные файлы.
    - Ознакомьтесь с разностью между локальным файлом и удаленным файлом.
    - Обновите локальный файл с помощью удаленного файла или обновите удаленный файл, используя локальный файл.

<a id="_Templates"></a>
### <a name="aspnet-mvc-templates"></a>Шаблоны MVC ASP.NET

- Новый шаблон приложения Facebook упрощает создание приложений Facebook Canvas. Всего за несколько простых шагов можно создать приложение Facebook, получающее данные от выполнившего вход пользователя и передающего их его друзьям. Шаблон содержит новую библиотеку, предназначенную для выполнения любых операций по проектированию приложений Facebook, включая проверку подлинности, разрешения, доступ к данным Facebook и многое другое. Дополнительные сведения об использовании шаблона приложения Facebook см. в разделе [https://go.microsoft.com/fwlink/?LinkID=269921](https://go.microsoft.com/fwlink/?LinkID=269921).
- С помощью нового шаблона одностраничного приложения MVC разработчики могут создавать интерактивные клиентские веб-приложения, применяя в веб-API ASP.NET код HTML 5 и CSS 3, а также используя популярные библиотеки Knockout и jQuery JavaScript. Шаблон включает приложение списка TODO, демонстрирующее общие рекомендации по созданию приложения HTML5 на JavaScript, которое использует API сервера RESTFUL. Дополнительные сведения можно прочитать на [https://www.asp.net/single-page-application](../single-page-application/index.md).
- Теперь можно создать VSIX, который добавляет новые шаблоны в диалоговое окно создания проекта ASP.NET MVC. Дополнительные сведения: [https://go.microsoft.com/fwlink/?LinkId=275019](https://go.microsoft.com/fwlink/?LinkId=275019)
- Шаблоны проектов &#8211; MVC пакета фикседдисплаймодес были обновлены для включения нового пакета NuGet "фикседдисплаймодес", который содержит обходной путь для ошибки в MVC 4. Дополнительные сведения об исправлении, содержащемуся в пакете, см. в этой записи блога ([https://blogs.msdn.com/b/rickandy/archive/2012/09/17/asp-net-mvc-4-mobile-caching-bug-fixed.aspx](https://blogs.msdn.com/b/rickandy/archive/2012/09/17/asp-net-mvc-4-mobile-caching-bug-fixed.aspx)) от команды MVC.

<a id="_ASP.NET_Web_API"></a>
### <a name="aspnet-web-api"></a>Веб-API ASP.NET

Веб-API ASP.NET улучшена с помощью нескольких новых функций:

- Веб-API ASP.NET OData
- Трассировка веб-API ASP.NET
- Страница справки веб-API ASP.NET

#### <a name="aspnet-web-api-odata"></a>Веб-API ASP.NET OData

Веб-API ASP.NET OData обеспечивает гибкость, необходимую для создания конечных точек OData с обширной бизнес-логикой по отношению к любому источнику данных. С веб-API ASP.NET OData вы управляете количеством семантики OData, которые необходимо предоставить. Веб-API ASP.NET OData входит в состав шаблонов проектов ASP.NET MVC 4 и также доступен в NuGet ([http://www.nuget.org/packages/microsoft.aspnet.webapi.odata](http://www.nuget.org/packages/microsoft.aspnet.webapi.odata)).

Веб-API ASP.NET OData в настоящее время поддерживает следующие функции:

- Включите семантику запроса OData, применив атрибут [Query].
- Простая проверка запросов OData и ограничение набора поддерживаемых параметров запроса, операторов и функций.
- Привязка параметра к Одатакуерйоптионс напрямую для получения абстрактного древовидного представления синтаксиса запроса, который затем может быть проверен и применен к интерфейсу IQueryable или IEnumerable.
- Включите разбиение на страницы на основе служб и создание ссылок на следующую страницу, указав ограничения результата для атрибута [с поддержкой запроса].
- Запросите общее число соответствующих ресурсов с помощью $inlinecount.
- Управление распространением значений NULL.
- Все операторы/ALL в $filter.
- Выведите модель EDM по соглашению или явно настройте модель таким же образом, как Entity Framework Code-First.
- Предоставление наборов сущностей путем наследования от Ентитисетконтроллер.
- Простые настраиваемые соглашения для предоставления свойств навигации, управления связями и реализации действий OData.
- Упрощенная маршрутизация с помощью метода расширения Маподатарауте.
- Поддержка управления версиями путем предоставления нескольких моделей EDM.
- Предоставьте сервисный документ и $metadata, чтобы можно было создавать клиенты (.NET, Windows Phone, Магазин Windows и т. д.) для веб-API.
- Поддержка подробных форматов OData ATOM, JSON и JSON.
- Создание, обновление, частичное обновление (исправление) и удаление сущностей.
- Запрос и обработка связей между сущностями.
- Создание связей связей, которые связываются с маршрутами.
- Сложные типы.
- Наследование типа сущности.
- Свойства коллекции.
- Перечисления.
- Действия OData.
- Основаны на той же фундаменте, что и WCF Data Services, а именно ODataLib ([http://www.nuget.org/packages/microsoft.data.odata](http://www.nuget.org/packages/microsoft.data.odata)).

Дополнительные сведения о веб-API ASP.NET OData см. в разделе [https://go.microsoft.com/fwlink/?LinkId=271141](https://go.microsoft.com/fwlink/?LinkId=271141).

#### <a name="aspnet-web-api-tracing"></a>Трассировка веб-API ASP.NET

Веб-API ASP.NETная трассировка интегрирует данные трассировки из веб-API с помощью трассировки .NET. Теперь он включен по умолчанию в шаблоне проекта веб-API. Данные трассировки для веб-API отправляются в окно вывода и становятся доступными через IntelliTrace. Веб-API ASP.NET трассировка позволяет отслеживать сведения о веб-API при размещении в Windows Azure с помощью интеграции с [windows система диагностики Azure](https://msdn.microsoft.com/library/windowsazure/hh411529.aspx). Можно также установить и включить трассировку веб-API ASP.NET в любом приложении, используя веб-API ASP.NET трассировки пакета NuGet ([http://www.nuget.org/packages/microsoft.aspnet.webapi.tracing](http://www.nuget.org/packages/microsoft.aspnet.webapi.tracing)).

Дополнительные сведения о настройке и использовании трассировки веб-API ASP.NET см. в разделе [https://go.microsoft.com/fwlink/?LinkID=269874](https://go.microsoft.com/fwlink/?LinkID=269874).

#### <a name="aspnet-web-api-help-page"></a>Страница справки веб-API ASP.NET

Страница справки веб-API ASP.NET теперь включена по умолчанию в шаблоне проекта веб-API. Страница справки веб-API ASP.NET автоматически создает документацию для веб-API, включая конечные точки HTTP, Поддерживаемые методы HTTP, параметры и примеры полезных данных сообщения запроса и ответа. Документация автоматически извлекается из комментариев в коде. Можно также добавить страницу справки веб-API ASP.NET в любое приложение, используя пакет NuGet страницы справки веб-API ASP.NET ([http://www.nuget.org/packages/microsoft.aspnet.webapi.helppage](http://www.nuget.org/packages/microsoft.aspnet.webapi.helppage)).

Дополнительные сведения о настройке и настройке страницы справки веб-API ASP.NET см. в разделе [https://go.microsoft.com/fwlink/?LinkId=271140](https://go.microsoft.com/fwlink/?LinkId=271140).

<a id="_ASP.NET_SignalR"></a>
### <a name="aspnet-signalr"></a>ASP.NET SignalR

ASP.NET SignalR упрощает добавление веб-возможностей в режиме реального времени в приложение ASP.NET, используя WebSockets, если они доступны, и автоматически применяет к другим методам, если это не так.

Дополнительные сведения об использовании SignalR ASP.NET см. в разделе [https://go.microsoft.com/fwlink/?LinkId=271271](https://go.microsoft.com/fwlink/?LinkId=271271).

<a id="_ASP.NET_Friendly_URLs"></a>
### <a name="aspnet-friendly-urls"></a>ASP.NET Friendly URLs

ASP.NET Фриендлюрлс позволяет разработчикам веб-форм легко создавать понятные URL-адреса (без расширения. aspx). Он не требует настройки и может использоваться с существующими приложениями ASP.NET v 4.0. Функция Фриендлюрлс также упрощает для разработчиков Добавление мобильных устройств в свои приложения благодаря поддержке переключения между настольными и мобильными представлениями.

Дополнительные сведения об установке и использовании удобных URL-адресов ASP.NET см. в разделе [http://www.hanselman.com/blog/IntroducingASPNETFriendlyUrlsCleanerURLsEasierRoutingAndMobileViewsForASPNETWebForms.aspx](http://www.hanselman.com/blog/IntroducingASPNETFriendlyUrlsCleanerURLsEasierRoutingAndMobileViewsForASPNETWebForms.aspx).

<a id="_Known_Issues_and"></a>
## <a name="known-issues-and-breaking-changes"></a>Известные проблемы и критические изменения

В этом разделе описаны известные проблемы и критические изменения в выпуске ASP.NET and Web Tools 2012,2.

### <a name="installation-issues"></a>Проблемы с установкой

#### <a name="out-of-order-installs-of-visual-studio-2012"></a>Неупорядоченные установки Visual Studio 2012

Для установки дополнительного SKU Visual Studio 2012 после установки ASP.NET and Web Tools 2012,2 потребуется операция восстановления. Рассмотрим следующую последовательность:

1. Установка Visual Studio 2012 Express для Web
2. Установка ASP.NET and Web Tools 2012,2
3. Установите Visual Studio 2012 Professional, Premium или Ultimate

Шаг 2 приведет к установке обновлений для Express для Web. Чтобы убедиться, что дополнительный SKU, установленный на шаге 3, содержит обновление, необходимо исправить ASP.NET and Web Tools 2012,2, чтобы установить обновления для последнего установленного SKU. Это также применимо, если номера SKU на шагах 1 и 3 реверсируются.

#### <a name="installing-microsoft-aspnet-and-web-tools-20122-when-visual-studio-is-open"></a>Установка Microsoft ASP.NET and Web Tools 2012,2 при открытии Visual Studio

Если VS открыт во время установки Microsoft ASP.NET and Web Tools 2012,2, Visual Studio может оказаться в неисправном состоянии. Пользователям рекомендуется закрыть все экземпляры Visual Studio, прежде чем продолжить установку.

#### <a name="canceling-aspnet-and-web-tools-20122-setup-in-the-middle-of-installation"></a>Отмена установки ASP.NET and Web Tools 2012,2 в процессе установки

Отмена установки ASP.NET and Web Tools 2012,2 в ходе установки приведет к неправильному состоянию Visual Studio. Чтобы решить эту проблему, выполните следующие действия. 

- Нажмите Установка и удаление программ
- Удалите Microsoft ASP.NET and Web Tools 2012,2, если они есть.
- Повторная установка Microsoft ASP.NET and Web Tools 2012,2

#### <a name="after-uninstalling-aspnet-and-web-tools-20122-the-aspnet-mvc-4-templates-and-razor-v2-web-site-templates-are-missing"></a>После удаления ASP.NET and Web Tools 2012,2 шаблоны ASP.NET MVC 4 и шаблоны веб-сайтов Razor v2 отсутствуют

При удалении ASP.NET and Web Tools 2012,2 также удаляются все шаблоны веб-сайтов ASP.NET MVC 4 и Razor v2 из Visual Studio 2012.

Чтобы устранить эту проблему, восстановите установку Visual Studio 2012, чтобы переустановить шаблоны веб-сайтов ASP.NET MVC 4 и Razor v2.

### <a name="tooling-issues"></a>Проблемы с инструментарием

#### <a name="nuget-error-reported-during-project-creation"></a>Ошибка NuGet при создании проекта

После установки ASP.NET and Web Tools 2012,2 может появиться следующая ошибка при создании проекта MVC 4

![](aspnet-and-web-tools-20122-release-notes/_static/image1.png)

ASP.NET and Web Tools 2012,2 поставляется с NuGet 2,1 и обновит расширение в Visual Studio 2012. В некоторых случаях установщик VSIX не сможет правильно обновить VSIX. Чтобы решить эту проблему, выполните следующие действия.

1. Запуск Visual Studio 2012 от имени администратора
2. Выберите Инструменты-&gt;расширения и обновления и удалите NuGet.
3. Закройте Visual Studio.
4. Перейдите в папку установки ASP.NET and Web Tools 2012,2:

    1. Для Visual Studio 2012: **Program FILES\MICROSOFT ASP. Нет\асп.нет Web Стакк\висуал Studio 2012**
    2. Для Visual Studio 2012 Express для Web: **Program FILES\MICROSOFT ASP. Нет\асп.нет Web Стакк\висуал Studio Express 2012 для Web**
5. Дважды щелкните NuGet. Tools. VSIX, чтобы переустановить NuGet.

### <a name="web-api-issues"></a>Проблемы веб-API

#### <a name="parsing-issues-in-filter-and-datetime-literals"></a>Анализ проблем в литералах $filter и DateTime

Средству синтаксического анализа URI OData не удается правильно проанализировать частичные литералы datetime. Например, $filter = Start EQ DateTime ' 2012-12-31T12:00 ' не удается правильно проанализировать. Обходной путь заключается в использовании полного литерала, $filter = Start EQ DateTime ' 2012-12-31T12:00:00 '.

#### <a name="odata-doesnt-support-case-insensitive-property-names"></a>OData не поддерживает имена свойств, не учитывающих регистр.

OData не поддерживает имена свойств без учета регистра в запросах OData и пути OData. См. рабочие элементы:

- [http://aspnetwebstack.codeplex.com/workitem/366](http://aspnetwebstack.codeplex.com/workitem/366)
- [http://aspnetwebstack.codeplex.com/workitem/704](http://aspnetwebstack.codeplex.com/workitem/704)

Если у пользователей разные регистры на стороне клиента JavaScript и на стороне сервера, они, скорее всего, будут столкнуться с этой проблемой. Эта проблема связана с разработкой протокола OData. Однако многие пользователи сообщают об этой ошибке. Чтобы обойти эту возможность, пользователям необходимо исправить свои случаи в URL-адресе.

#### <a name="default-odata-routing-conventions-doesnt-support-postput-on-navigation-property"></a>Соглашения о маршрутизации OData по умолчанию не поддерживают свойство навигации после или размещения.

Соглашения о маршрутизации OData по умолчанию не поддерживают свойство навигации после или размещения. См. [http://aspnetwebstack.codeplex.com/workitem/366](http://aspnetwebstack.codeplex.com/workitem/366)рабочего элемента. В соглашениях по умолчанию отсутствует это часто используемое соглашение.

Чтобы обойти эту возможность, пользователям необходимо расширить новое соглашение о маршрутизации для его поддержки.

### <a name="facebook-template-issues"></a>Проблемы с шаблонами Facebook

#### <a name="facebook-application-template-only-works-using-net-45"></a>Шаблон приложения Facebook работает только с .NET 4,5

Необходимо выбрать .NET 4,5 в раскрывающемся списке Платформа в диалоговом окне Новый проект, чтобы просмотреть шаблон приложения Facebook в ASP.NET MVC 4.

#### <a name="real-time-update-controller"></a>Контроллер обновления в режиме реального времени

Шаблон приложения Facebook позволяет пользователю легко создать контроллер веб-API для работы с обновлениями в режиме реального времени из Facebook. Если компьютер разработки находится за пределами NAT, контроллер может не работать без дальнейшей настройки сети. Дополнительные сведения см. в разделе [http://facebook.stackoverflow.com/questions/5259467/can-a-computer-behind-a-nat-router-receive-realtime-updates-from-facebook](http://facebook.stackoverflow.com/questions/5259467/can-a-computer-behind-a-nat-router-receive-realtime-updates-from-facebook)

#### <a name="query-string-values-conflict-with-facebook-oauth-parameters"></a>Значения строки запроса конфликтуют с параметрами OAuth Facebook

Следующие поля конфликтуют с URL-адресом обратного вызова диалогового окна Facebook OAuth. Не добавляйте собственные значения строки запроса со следующими именами: код, ошибка, ошибка\_описание, ошибка\_причина.

#### <a name="using-page-inspector-with-facebook-template"></a>Использование Инспектор страниц с шаблоном Facebook

Вы не можете использовать функцию Инспектор страниц в Visual Studio 2012 при отладке приложения Facebook. Инспектор страниц в настоящее время не поддерживает iframes.

### <a name="single-page-application-template-issues"></a>Проблемы с шаблоном одностраничного приложения

#### <a name="with-jquery-19knockout-221-update-when-running-default-mvc-spa-project-new-todo-item-edit-enter-focus-event-is-not-handled-properly"></a>При обновлении JQuery 1,9/выколачивание 2.2.1 при выполнении проекта по умолчанию для MVC SPA новый элемент TODO Edit ввод события фокуса не обрабатывается должным образом.

При обновлении JQuery 1,9/выколачивание 2.2.1 при выполнении проекта по умолчанию для MVC SPA при создании нового элемента TODO в списке ToDo новое поле "изменить элемент" не будет отображаться.

Чтобы решить эту проблему [http://knockoutjs.com/documentation/hasfocus-binding.html](http://knockoutjs.com/documentation/hasfocus-binding.html), выполните аналогичные исправления в следующем образце кода:

Файл TODO. Model. js  
 Функция ToDoList (Data), добавление следующих данных:  
 **Self. OnSelect = KO. наблюдаемый (false);**

Функция todoList. prototype. Аддтодо добавляет следующий черный текст:  
 **Self. IsTrue (true);**  
 Self. Невтодотитле (&quot;&quot;);

Файл index. cshtml, добавьте следующий черный текст:  
 &lt;форма data-bind =&quot;Submit: Аддтодо&quot;&gt;  
 &lt;input Class =&quot;Аддтодо&quot; Type =&quot;Text&quot; data-bind =&quot;значение: Невтодотитле, PlaceHolder: ' введите здесь, чтобы добавить ', Блуронентер: true, **хасфокус:** IsTrue, событие: {размытие: аддтодо}&quot; /&gt;  
 &gt; &lt;форм
