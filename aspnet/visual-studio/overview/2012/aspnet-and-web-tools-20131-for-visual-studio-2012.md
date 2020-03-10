---
uid: visual-studio/overview/2012/aspnet-and-web-tools-20131-for-visual-studio-2012
title: Заметки о выпуске для ASP.NET and Web Tools 2013,1 для Visual Studio 2012 | Документация Майкрософт
author: microsoft
description: В этом документе описывается выпуск ASP.NET and Web Tools 2013,1 для Visual Studio 2012.
ms.author: riande
ms.date: 11/13/2013
ms.assetid: ca26e5bb-630e-41d2-8512-2a9386c431cb
msc.legacyurl: /visual-studio/overview/2012/aspnet-and-web-tools-20131-for-visual-studio-2012
msc.type: authoredcontent
ms.openlocfilehash: 260af1018064d60d80cbb1002001f28c4daffffd
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78467106"
---
# <a name="release-notes-for-aspnet-and-web-tools-20131-for-visual-studio-2012"></a>Заметки о выпуске ASP.NET and Web Tools 2013.1 для Visual Studio 2012

по [Майкрософт](https://github.com/microsoft)

> В этом документе описывается выпуск ASP.NET and Web Tools 2013,1 для Visual Studio 2012.

## <a name="contents"></a>Содержимое

- [Заметки об установке](#install)
- [Требования к программному обеспечению](#requirements)
- Новые функции в ASP.NET and Web Tools 2013,1 для Visual Studio 2012

    - [Начальная загрузка](#bootstrap)
    - [Шаблоны](#templates)

        - [Шаблон ASP.NET MVC 5](#mvc5template)
        - [Шаблон веб-API ASP.NET 2](#apitemplate)
        - [Шаблоны элементов](#itemtemplate)
    - [Entity Framework 6](#ef6)
    - [Формирование шаблонов ASP.NET](#scaffold)
    - [Редактор Razor](#razor)
    - [NuGet 2.7](#nuget)
- Известные проблемы и критические изменения

    - [Формирование шаблонов ASP.NET](#issuescaffolding)

        - [Формирование шаблонов MVC и веб-API — HTTP 404, ошибка "не найдено"](#404issue)
        - [Visual Studio Express 2012 для веб-сайта прекращает работу после добавления шаблона элемента](#expressissue)
    - [ASP.NET Razor 3](#issuerazor)

        - [Просмотр файла CSHTML с помощью кнопки "Обзор" или нажатия клавиши F5 приводит к ошибке сервера](#browseissue)
        - [Перезапись URL-адреса и тильда (~)](#rewriteissue)
    - [Шаблоны](#templateissue)

<a id="install"></a>
## <a name="installation-notes"></a>Замечания по установке

[Установка](https://www.microsoft.com/web/handlers/webpi.ashx/getinstaller/WebNode11Pack.appids) ASP.NET and Web Tools 2013,1 для Visual Studio 2012.

<a id="requirements"></a>
## <a name="software-requirements"></a>Требования к программному обеспечению

Необходимо иметь Visual Studio 2012 или Visual Studio Express 2012 для Web.

## <a name="new-features-in-aspnet-and-web-tools-20131-for-visual-studio-2012"></a>Новые функции в ASP.NET and Web Tools 2013,1 для Visual Studio 2012

<a id="bootstrap"></a>
### <a name="bootstrap"></a>Загрузке

При формировании шаблонов MVC 5 и представлений в разметке для представлений используется [Начальная](http://getbootstrap.com/)загрузка.

<a id="templates"></a>
### <a name="templates"></a>Шаблоны

<a id="mvc5template"></a>
#### <a name="aspnet-mvc-5-template"></a>Шаблон ASP.NET MVC 5

Мы добавили новый шаблон MVC 5. Он ссылается на последние версии пакетов NuGet для MVC 5, и для добавления контроллеров и представлений можно использовать формирование шаблонов.

<a id="apitemplate"></a>
#### <a name="aspnet-web-api-2-template"></a>Шаблон веб-API ASP.NET 2

Мы добавили новый шаблон веб-API 2. Он ссылается на последние версии пакетов NuGet для Web API 2, и вы можете использовать формирование шаблонов для добавления контроллеров и представлений.

<a id="itemtemplate"></a>
#### <a name="item-templates"></a>Шаблоны элементов

Мы добавили новые шаблоны элементов для представлений MVC 5, Web Pages (Razor 3) и Web API 2 Controllers. Они устанавливают связанные пакеты NuGet в проект при добавлении новых элементов.

<a id="ef6"></a>
### <a name="entity-framework-6"></a>Entity Framework 6

При формировании шаблона контроллера MVC или веб-API с помощью Entity Framework используется платформа 6. Дополнительные сведения о Entity Framework см. в [журнале версий Entity Framework](https://msdn.com/data/jj574253).

Вы также можете скачать и установить инструменты Entity Framework 6 для Visual Studio 2012. См. раздел [Get Entity Framework](https://msdn.com/data/ee712906#tooling).

<a id="scaffold"></a>
### <a name="aspnet-scaffolding"></a>Формирование шаблонов ASP.NET

Формирование шаблонов ASP.NET — это платформа создания кода для веб-приложений ASP.NET. Это упрощает добавление в проект стандартного кода, взаимодействующего с моделью данных.

В предыдущих версиях Visual Studio формирование шаблонов было ограничено ASP.NET проектами MVC. В этом обновлении теперь можно использовать формирование шаблонов для любого проекта ASP.NET, включая веб-формы. Это обновление не поддерживает создание страниц для проекта веб-форм, но вы по-прежнему можете использовать формирование шаблонов с веб-формами, добавив зависимости MVC в проект. Поддержка создания страниц для веб-форм будет добавлена в будущем обновлении.

При использовании формирования шаблонов убедитесь, что в проекте установлены все необходимые зависимости. Например, если начать с проекта веб-форм ASP.NET, а затем использовать формирование шаблонов для добавления контроллера веб-API, необходимые пакеты NuGet и ссылки добавляются в проект автоматически.

Чтобы добавить формирование шаблонов MVC в проект веб-форм, добавьте новый шаблонный **элемент** и выберите **зависимости MVC 5** в диалоговом окне. Существует два варианта формирования шаблонов MVC. Минимальный и полный. Если выбрать минимум, в проект будут добавлены только пакеты NuGet и ссылки для ASP.NET MVC. Если выбран параметр Full, добавляются минимальные зависимости, а также необходимые файлы содержимого для проекта MVC.

Поддержка формирования шаблонов асинхронных контроллеров использует новые асинхронные функции из Entity Framework 6.

Дополнительные сведения и учебники см. в разделе [Общие сведения о формировании шаблонов ASP.NET](../2013/aspnet-scaffolding-overview.md). В этих руководствах показано формирование шаблонов с помощью Visual Studio 2013, но они также применимы к ASP.NET and Web Tools 2013,1 для Visual Studio 2012.

<a id="razor"></a>
### <a name="razor-editor"></a>Редактор Razor

В этом обновлении Visual Studio 2012 теперь поддерживает инструментарий и редактирование Razor 3.

<a id="nuget"></a>
### <a name="nuget-27"></a>NuGet 2.7

NuGet 2,7 включает широкий набор новых функций, которые подробно описаны в [заметках о выпуске NuGet 2,7](http://docs.nuget.org/docs/release-notes/nuget-2.7).

Эта версия NuGet устраняет необходимость явно разрешить NuGet восстанавливать недостающие пакеты. При установке NuGet 2,7 пользователям неявно предоставляется согласие на автоматическое восстановление отсутствующих пакетов. Пользователи могут явно отказаться от восстановления пакетов с помощью параметров NuGet в Visual Studio. Это изменение упрощает восстановление пакетов.

## <a name="known-issues-and-breaking-changes"></a>Известные проблемы и критические изменения

<a id="issuescaffolding"></a>
### <a name="aspnet-scaffolding"></a>Формирование шаблонов ASP.NET

<a id="404issue"></a>
#### <a name="mvc-and-web-api-scaffolding---http-404-not-found-error"></a>Формирование шаблонов MVC и веб-API — HTTP 404, ошибка "не найдено"

Если при добавлении шаблона элемента в проект возникла ошибка, возможно, проект будет оставаться в нестабильном состоянии. Откат некоторых изменений, внесенных в формирование шаблонов, будет выполнен, однако откат других изменений, таких как установленные пакеты NuGet, не будет отменен. При откате изменений конфигурации маршрутизации пользователи получат ошибку HTTP 404 при переходе к шаблонным элементам.

Чтобы устранить эту ошибку для MVC, добавьте новый шаблонный элемент и выберите зависимости MVC 5 (минимальное или полное). Этот процесс добавит все необходимые изменения в проект.

Чтобы устранить эту ошибку для веб-API, выполните следующие действия.

1. Добавьте в проект следующий класс WebApiConfig.

    [!code-csharp[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample1.cs)]

    [!code-vb[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample2.vb)]
2. Настройте WebApiConfig. Register в методе запуска приложения\_в Global. asax следующим образом:

    [!code-csharp[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample3.cs)]

    [!code-vb[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample4.vb)]

<a id="expressissue"></a>
#### <a name="visual-studio-express-2012-for-web-stops-working-after-adding-a-scaffolded-item"></a>Visual Studio Express 2012 для веб-сайта прекращает работу после добавления шаблона элемента

Если Visual Studio Express 2012 для веб-сайта прекращает работу после добавления шаблона элемента с Entity Framework (например, контроллер веб-API 2 с действиями с помощью Entity Framework), возможно, Visual Studio Express не удалось загрузить машинный образ сборки. зависит от System. Web. Extensions.

Чтобы устранить эту проблему, настройте Visual Studio Express для работы с изображением MSIL для System. Web. Extensions:

1. Откройте командную строку в режиме администратора.
2. Перейдите в%ProgramFiles%\Microsoft Visual Studio 11.0 \ Common7\IDE или% ProgramFiles (x86)% \ Microsoft Visual Studio 11.0 \ Common7\IDE (для 64 разрядов Windows).
3. Откройте файл Ввдекспресс. exe. config в текстовом редакторе.
4. Добавьте следующую строку в элемент конфигурации &lt;&gt;/&lt;среды выполнения&gt;:  

    [!code-xml[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample5.xml)]
5. Перезапустите Visual Studio Express 2012 для Web.

<a id="issuerazor"></a>
### <a name="aspnet-razor-3"></a>ASP.NET Razor 3

<a id="browseissue"></a>
#### <a name="viewing-cshtml-file-with-browse-with-or-f5-causes-a-server-error"></a>Просмотр файла CSHTML с помощью кнопки "Обзор" или нажатия клавиши F5 приводит к ошибке сервера

При создании проекта MVC 5 в Visual Studio 2012 (или открытом в Visual Studio 2012 проект MVC 5, созданный в Visual Studio 2013) и попытке просмотра файла CSHTML с помощью команды "Обзор" или "F5" вы получите сообщение об ошибке **"ошибка сервера" в приложении "/"** . Сервер пытается переходить к `http://localhost:XXXX/Views/../XXXX.cshtml`

Чтобы устранить эту проблему, измените значение параметра **действие при запуске** в проекте на **определенную страницу**. Вам не нужно указывать значение для страницы.

![](aspnet-and-web-tools-20131-for-visual-studio-2012/_static/image1.png)

После внесения этого изменения при нажатии клавиши F5 выполняется переход к корню приложения (`http://localhost:XXXX`). Это поведение отличается от поведения проектов MVC 5 в Visual Studio 2013, где **Текущая страница** запускает открытую страницу.

<a id="rewriteissue"></a>
#### <a name="url-rewrite-and-tilde"></a>Перезапись URL-адреса и тильда (~)

После обновления до ASP.NET Razor 3 или ASP.NET MVC 5, тильда (~) может перестать работать правильно, если используется переписывание URL-адресов. Переписывание URL-адресов влияет на нотацию тильды (~) в HTML-элементах, таких как &lt;A/&gt;, &lt;SCRIPT/&gt;, &lt;LINK/&gt;, и в результате тильда больше не сопоставляется с корневым каталогом.

Например, при перезаписи запросов для **ASP.NET/Content** в **ASP.NET**атрибут href в &lt;A href = "~/контент/"/&gt; разрешается в **/контент/контент/** вместо **/** . Чтобы отключить это изменение, можно задать для контекста **IIS\_васурлревриттен** значение false на каждой веб-странице или в **приложении\_BeginRequest** в Global. asax.

<a id="templateissue"></a>
### <a name="templates"></a>Шаблоны

При создании проектов ASP.NET MVC с помощью Visual Studio 2012 на Windows 8.1 или Windows Server 2012 R2 в Visual Studio отображается сообщение об ошибке "Настройка веб-узла [URL] для ASP.NET 4,5".

![Ошибка конфигурации](aspnet-and-web-tools-20131-for-visual-studio-2012/_static/image2.png)

Вы видите эту ошибку, так как Visual Studio 2012 не включает компонент ASP.NET 4,5 при установке в этих выпусках Windows. Чтобы включить ASP.NET 4,5, выполните действия, описанные в разделе [Включение или отключение компонентов Windows](https://windows.microsoft.com/windows-8/turn-windows-features-on-off).

![Включение или отключение функций Windows](aspnet-and-web-tools-20131-for-visual-studio-2012/_static/image3.png)

Кроме того, можно включить ASP.NET 4,5 с помощью командной строки.

1. Откройте командную строку в режиме администратора.
2. Выполните следующую команду, чтобы включить ASP.NET 4,5.  
    `dism /Online /Enable-Feature /FeatureName:NetFx4Extended-ASPNET45 /Quiet /NoRestart`
