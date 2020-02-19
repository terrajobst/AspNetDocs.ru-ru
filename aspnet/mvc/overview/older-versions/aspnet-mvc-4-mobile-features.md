---
uid: mvc/overview/older-versions/aspnet-mvc-4-mobile-features
title: Мобильные функции ASP.NET MVC 4 | Документация Майкрософт
author: Rick-Anderson
description: Теперь в этом руководстве используется версия MVC 5 с примерами кода при развертывании мобильного веб-приложения ASP.NET MVC 5 на веб-сайтах Azure.
ms.author: riande
ms.date: 08/15/2012
ms.assetid: 27dc4fc8-1b51-43b0-933f-fc1b52476523
msc.legacyurl: /mvc/overview/older-versions/aspnet-mvc-4-mobile-features
msc.type: authoredcontent
ms.openlocfilehash: 9716def069ca9f7115af32e16381f41bd4d13342
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457652"
---
# <a name="aspnet-mvc-4-mobile-features"></a>Мобильные функции ASP.NET MVC 4

по [Рик Андерсон (](https://twitter.com/RickAndMSFT)

> Теперь в этом руководстве используется версия MVC 5 с примерами кода при [развертывании мобильного веб-приложения ASP.NET MVC 5 на веб-сайтах Azure](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/).

В этом учебнике рассматриваются основы работы с мобильными функциями в веб-приложении ASP.NET MVC 4. Для работы с этим руководством можно использовать [Visual Studio Express 2012](https://www.microsoft.com/visualstudio/11/products/express) или Visual Web Developer 2010 Express с пакетом обновления 1 (&quot;Visual Web Developer или vWD&quot;). Если у вас уже есть профессиональная версия Visual Studio, ее можно использовать.

Прежде чем начать, убедитесь, что установлены предварительные требования, перечисленные ниже.

- [Visual Studio Express 2012](https://www.microsoft.com/visualstudio/11/products/express) (рекомендуется) или Visual Studio Web Developer Express SP1. Visual Studio 2012 содержит ASP.NET MVC 4. Если вы используете Visual Web Developer 2010, необходимо установить [ASP.NET MVC 4](https://go.microsoft.com/fwlink/?LinkId=243392).

Кроме того, понадобится эмулятор браузера для мобильного устройства. Можно использовать любое из следующих средств:

- [Эмулятор Windows 7 Phone](https://msdn.microsoft.com/library/ff402563(VS.92).aspx). (Это эмулятор, используемый в большинстве снимков экрана в этом учебнике.)
- Измените строку агента пользователя для эмуляции iPhone. См. [эту](http://www.howtogeek.com/113439/how-to-change-your-browsers-user-agent-without-installing-any-extensions/) запись блога.
- [Opera Mobile Emulator](http://www.opera.com/developer/tools/mobile/)
- [Apple Safari](http://www.apple.com/safari/download/) с агентом пользователя, имеющим значение iPhone. Инструкции по настройке агента пользователя в Safari на "iPhone" см. [в статье как разрешить Safari в браузере Internet Explorer](http://www.davidalison.com/2008/05/how-to-let-safari-pretend-its-ie.html) в блоге Дэвид Алисон.

К этой статье прилагаются следующие проекты Visual Studio с исходным кодом C#:

- [Начальная загрузка проекта](https://go.microsoft.com/fwlink/?linkid=228307&amp;clcid=0x409)
- [Завершено скачивание проекта](https://go.microsoft.com/fwlink/?linkid=228306&amp;clcid=0x409)

### <a name="what-youll-build"></a>Что вы создадите

В рамках этого руководства вы добавите функции мобильных устройств в простое приложение, посвященное конференции, которое предоставляется в [начальном проекте](https://go.microsoft.com/fwlink/?LinkId=228307). На следующем снимке экрана показана страница «Теги» завершенного приложения, как показано в [эмуляторе Windows 7 Phone](https://msdn.microsoft.com/library/ff402563(VS.92).aspx). Для упрощения ввода с клавиатуры см. раздел [Назначение клавиш для эмулятора Windows Phone](https://msdn.microsoft.com/library/ff754352(v=vs.92).aspx) .

[![p1_Tags_CompletedProj](aspnet-mvc-4-mobile-features/_static/image2.png)](aspnet-mvc-4-mobile-features/_static/image1.png)

Для разработки мобильного приложения можно использовать Internet Explorer версии 9 или 10, FireFox или Chrome, задав [строку агента пользователя](http://www.howtogeek.com/113439/how-to-change-your-browsers-user-agent-without-installing-any-extensions/). На следующем рисунке показано завершенное руководство по эмуляции iPhone с помощью Internet Explorer. Для отладки приложения можно использовать средства разработчика и [средство Fiddler](http://www.fiddler2.com/fiddler2/) для Internet Explorer F-12.

![](aspnet-mvc-4-mobile-features/_static/image3.png)

### <a name="skills-youll-learn"></a>Чему вы научитесь

В этом учебнике вы узнаете:

- Как шаблоны ASP.NET MVC 4 используют атрибут `viewport` HTML5 и адаптивную визуализацию для улучшения отображения на мобильных устройствах.
- Создание представлений для мобильных устройств.
- Создание переключателя представлений, который позволяет пользователям переключаться между мобильным представлением и представлением рабочего стола приложения.

### <a name="getting-started"></a>Начало работы

Скачайте приложение с перечнем конференций для начального проекта по следующей ссылке: [download](https://go.microsoft.com/fwlink/?LinkId=228307). Затем в проводнике Windows щелкните правой кнопкой мыши файл *мвкмобиле. zip* и выберите пункт **свойства**. В диалоговом окне **Свойства мвкмобиле. zip** нажмите кнопку **разблокировать** . Разблокировка устраняет предупреждение системы безопасности, выводимое при попытке использовать *ZIP-файл* , загруженный из Интернета.

![p1_unBlock](aspnet-mvc-4-mobile-features/_static/image4.png)

Щелкните правой кнопкой мыши файл *мвкмобиле. zip* и выберите **извлечь все** , чтобы распаковать файл. В Visual Studio откройте файл *мвкмобиле. sln* .

Нажмите клавиши CTRL + F5, чтобы запустить приложение, которое будет отображаться в браузере настольных систем. Запустите эмулятор браузера мобильного устройства, скопируйте URL-адрес приложения конференции в эмулятор и щелкните ссылку **Обзор по тегу** . Если вы используете эмулятор Windows Phone, щелкните строку URL-адреса и нажмите клавишу Pause, чтобы получить доступ с клавиатуры. На рисунке ниже показано представление *AllTags* (выберите пункт **Просмотр по тегу**).

[![p1_browseTag](aspnet-mvc-4-mobile-features/_static/image6.png)](aspnet-mvc-4-mobile-features/_static/image5.png)

Этот экран является очень удобным для чтения на мобильном устройстве. Щелкните ссылку ASP.NET.

[![p1_tagged_ASPNET](aspnet-mvc-4-mobile-features/_static/image8.png)](aspnet-mvc-4-mobile-features/_static/image7.png)

Представление тегов ASP.NET очень неудобно. Например, столбец **Date** очень труден для чтения. Далее в этом руководстве вы создадите версию представления *AllTags* , предназначенную специально для мобильных браузеров и которая сделает этот экран доступным для чтения.

Примечание. в настоящее время в модуле мобильного кэширования существует ошибка. Для рабочих приложений необходимо установить [исправленный пакет DisplayModes](http://nuget.org/packages/Microsoft.AspNet.Mvc.FixedDisplayModes) Nugget. Сведения об исправлении см. в статье [ASP.NET MVC 4 Mobile Caching](https://blogs.msdn.com/b/rickandy/archive/2012/09/17/asp-net-mvc-4-mobile-caching-bug-fixed.aspx) исправлена.

## <a name="css-media-queries"></a>Запросы мультимедиа CSS

[Запросы мультимедиа CSS](http://www.w3.org/TR/css3-mediaqueries/) — это расширение CSS для типов мультимедиа. Они позволяют создавать правила, переопределяющие правила CSS по умолчанию для определенных браузеров (агентов пользователя). Общее правило для CSS, предназначенное для мобильных браузеров, определяет максимальный размер экрана. Файл *контент\сите.КСС* , созданный при создании нового Интернет-проекта ASP.NET MVC 4, содержит следующий запрос носителя:

[!code-css[Main](aspnet-mvc-4-mobile-features/samples/sample1.css)]

Если окно браузера имеет размер 850 пикселей в ширину или менее, оно будет использовать правила CSS внутри этого блока мультимедиа. Вы можете использовать такие запросы CSS, чтобы обеспечить лучшее отображение HTML-содержимого в небольших браузерах (например, в мобильных браузерах), чем правила CSS по умолчанию, предназначенные для более широкого отображения браузеров настольных систем.

## <a name="the-viewport-meta-tag"></a>Тег meta окна просмотра

Большинство мобильных браузеров определяют ширину виртуального окна браузера (окно *просмотра*), размер которого гораздо больше, чем фактическая ширина мобильного устройства. Это позволяет мобильным браузерам вписать всю веб-страницу в виртуальную часть экрана. Затем пользователи могут увеличить интересующее вас содержимое. Однако если задать для ширины окна просмотра фактическую ширину устройства, то изменять масштаб не требуется, так как содержимое умещается в браузере для мобильных устройств.

В окне просмотра `<meta>` тег в файле макета ASP.NET MVC 4 для окна просмотра задается ширина устройства. В следующей строке показано окно просмотра `<meta>` тег в файле макета ASP.NET MVC 4.

[!code-html[Main](aspnet-mvc-4-mobile-features/samples/sample2.html)]

## <a name="examining-the-effect-of-css-media-queries-and-the-viewport-meta-tag"></a>Проверка влияния запросов мультимедиа CSS и мета тега окна просмотра

Откройте файл *Views\Shared\\_layout. cshtml* в редакторе и закомментируйте `<meta>` тег окна просмотра. В следующей разметке показана строка с комментарием.

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample3.cshtml)]

Откройте файл *мвкмобиле\контент\сите.КСС* в редакторе и измените максимальную ширину в запросе носителя на 0 пикселей. Это предотвратит использование правил CSS в мобильных браузерах. В следующей строке показан измененный запрос мультимедиа.

[!code-css[Main](aspnet-mvc-4-mobile-features/samples/sample4.css)]

Сохраните изменения и перейдите в приложение конференции в эмуляторе браузера для мобильных устройств. Маленький текст на следующем изображении является результатом удаления `<meta>` тега окна просмотра. Если не `<meta>` тег просмотра, браузер масштабируется до ширины окна просмотра по умолчанию (850 пикселей или больше для большинства мобильных браузеров).

[![p1_noViewPort](aspnet-mvc-4-mobile-features/_static/image10.png)](aspnet-mvc-4-mobile-features/_static/image9.png)

Отменить изменения — раскомментировать окно просмотра `<meta>` тег в файле макета и восстановить запрос носителя до 850 пикселей в файле *site. CSS* . Сохраните изменения и обновите браузер для мобильных устройств, чтобы убедиться, что экран с поддержкой мобильных устройств восстановлен.

Окно просмотра `<meta>` тег и запрос мультимедиа CSS не относятся к ASP.NET MVC 4, и вы можете воспользоваться преимуществами этих функций в любом веб-приложении. Но теперь они встроены в файлы, создаваемые при создании нового проекта ASP.NET MVC 4.

Дополнительные сведения о `<meta>` теге окна просмотра см. [в исчезнувшей двух окнах просмотра — второй части](http://www.quirksmode.org/mobile/viewports2.html).

В следующем разделе вы узнаете, как обеспечить представления для браузеров мобильных устройств.

## <a name="overriding-views-layouts-and-partial-views"></a>Переопределение представлений, макетов и частичных представлений

Значительная новая функция ASP.NET MVC 4 — это простой механизм, позволяющий переопределять любое представление (включая макеты и частичные представления) для мобильных браузеров в целом, для отдельного браузера для мобильных устройств или для любого конкретного браузера. Чтобы создать вид для мобильных устройств, можно скопировать файл представления и добавить расширение *.Mobile* к имени файла. Например, чтобы создать мобильное представление *индекса* , скопируйте *Views\Home\Index.cshtml* в *виевс\хоме\индекс.Мобиле.кштмл*.

В этом разделе для мобильных устройств будет создан специальный файл макета.

Чтобы начать, скопируйте *Views\Shared\\_layout. cshtml* в *Views\Shared\\_layout. Mobile. cshtml*. Откройте *\_Layout. Mobile. cshtml* и измените заголовок с **конференции MVC4** на **конференцию (Mobile)** .

В каждом вызове `Html.ActionLink` удалите "Просмотр по" в каждой ссылке *ActionLink*. Следующий код показывает завершенный раздел body файла макета для мобильных устройств.

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample5.cshtml)]

Скопируйте файл *виевс\хоме\аллтагс.кштмл* в *виевс\хоме\аллтагс.Мобиле.кштмл*. Откройте новый файл и измените элемент `<h2>` с "Tags" на "Tags (M)":

[!code-html[Main](aspnet-mvc-4-mobile-features/samples/sample6.html)]

Перейдите на страницу тегов, используя классический браузер и эмулятор браузера для мобильных устройств. В эмуляторе браузера для мобильных устройств показаны два внесенных изменения.

[![p2m_layoutTags. Mobile](aspnet-mvc-4-mobile-features/_static/image12.png)](aspnet-mvc-4-mobile-features/_static/image11.png)

В отличие от этого, экран рабочего стола не изменился.

[![p2_layoutTagsDesktop](aspnet-mvc-4-mobile-features/_static/image14.png)](aspnet-mvc-4-mobile-features/_static/image13.png)

## <a name="browser-specific-views"></a>Представления, относящиеся к браузеру

Кроме представлений для мобильных устройств и настольных компьютеров вы также можете создавать представления для отдельных браузеров. Например, можно создавать представления, специально предназначенные для браузера iPhone. В этом разделе вы узнаете, как создать макет для браузера iPhone и версию представления *AllTags* для iPhone.

Откройте файл *Global. asax* и добавьте следующий код в метод `Application_Start`.

[!code-csharp[Main](aspnet-mvc-4-mobile-features/samples/sample7.cs)]

Этот код определяет новый режим отображения с именем iPhone, который будет использоваться для каждого входящего запроса. Если входящий запрос удовлетворяет условию, которое вы задали (то есть, если агент пользователя содержит строку iPhone), ASP.NET MVC выполнит поиск представлений, которые содержат в своем имени суффикс iPhone.

В коде щелкните правой кнопкой мыши `DefaultDisplayMode`, выберите **Разрешить**, а затем выберите `using System.Web.WebPages;`. Это действие добавит ссылку на пространство имен `System.Web.WebPages`, в котором определяются типы `DisplayModes` и `DefaultDisplayMode`.

[![p2_resolve](aspnet-mvc-4-mobile-features/_static/image16.png)](aspnet-mvc-4-mobile-features/_static/image15.png)

Кроме того, вы можете вручную добавить следующую строку в раздел `using` файла.

[!code-csharp[Main](aspnet-mvc-4-mobile-features/samples/sample8.cs)]

Полное содержимое файла *Global. asax* приведено ниже.

[!code-csharp[Main](aspnet-mvc-4-mobile-features/samples/sample9.cs)]

Сохраните изменения. Скопируйте файл *мвкмобиле\виевс\шаред\\_layout. Mobile. cshtml* в *мвкмобиле\виевс\шаред\\_layout. iPhone. cshtml*. Откройте новый файл и измените заголовок `h1` с `Conference (Mobile)` на `Conference (iPhone)`.

Скопируйте файл *мвкмобиле\виевс\хоме\аллтагс.Мобиле.кштмл* в *мвкмобиле\виевс\хоме\аллтагс.ифоне.кштмл*. В новом файле измените значение элемента `<h2>` с "Tags (M)" на "Tags (iPhone)".

Запустите приложение. Запустите эмулятор браузера мобильного устройства. Убедитесь, что для его агента пользователя задано значение "iPhone", и перейдите к представлению *AllTags*. На следующем снимке экрана показано представление *AllTags* , отображаемое в браузере [Safari](http://www.apple.com/safari/download/) . Safari для Windows можно скачать [здесь](https://support.apple.com/kb/DL1531).

[![p2_iphoneView](aspnet-mvc-4-mobile-features/_static/image18.png)](aspnet-mvc-4-mobile-features/_static/image17.png)

В этом разделе мы рассмотрели, как создавать макеты и представления для мобильных устройств, а также как создавать макеты и представления для конкретных устройств, таких как iPhone. В следующем разделе вы узнаете, как использовать jQuery Mobile для более привлекательных мобильных представлений.

## <a name="using-jquery-mobile"></a>Использование jQuery Mobile

[Мобильная библиотека jQuery](http://jquerymobile.com/demos/1.0b3/#/demos/1.0b3/docs/about/intro.html) предоставляет платформу пользовательского интерфейса, которая работает со всеми основными мобильными браузерами. jQuery Mobile применяет *прогрессивное улучшение* к мобильным браузерам, поддерживающим CSS и JavaScript. Прогрессивное улучшение позволяет всем браузерам отображать базовое содержимое веб-страницы, одновременно позволяя более мощным браузерам и устройствам отображать более широкие возможности. Файлы JavaScript и CSS, которые включены в стиль мобильных устройств jQuery многие элементы, в соответствии с мобильными браузерами без внесения изменений в разметку.

В этом разделе вы установите пакет NuGet *jQuery. Mobile. MVC* , который устанавливает jQuery Mobile и мини-приложение для переключения представлений.

Чтобы начать, удалите созданные ранее файлы *shared\\_layout. Mobile. cshtml* и *shared\\_layout. iPhone. cshtml* .

Переименуйте файлы *виевс\хоме\аллтагс.Мобиле.кштмл* и *виевс\хоме\аллтагс.ифоне.кштмл* в *виевс\хоме\аллтагс.ифоне.кштмл.Хиде* и *Views\Home\AllTags.Mobile.cshtml.Hide*. Поскольку файлы больше не имеют расширения *. cshtml* , они не будут использоваться средой выполнения MVC ASP.NET для визуализации представления *AllTags* .

Установите пакет NuGet для *jQuery. Mobile. MVC* , выполнив следующие действия.

1. В меню **Сервис** выберите **Диспетчер пакетов NuGet**, а затем выберите **консоль диспетчера пакетов**.

    [![p3_packageMgr](aspnet-mvc-4-mobile-features/_static/image20.png)](aspnet-mvc-4-mobile-features/_static/image19.png)
2. В **консоли диспетчера пакетов**введите `Install-Package jQuery.Mobile.MVC -version 1.0.0`

На следующем рисунке показаны файлы, добавленные и измененные в проекте Мвкмобиле пакетом NuGet jQuery. Mobile. MVC. Добавляемые файлы имеют [Add] после имени файла. В образе не отображаются файлы GIF и PNG, добавленные в папку *контент\имажес* .

![](aspnet-mvc-4-mobile-features/_static/image21.png)

Пакет NuGet jQuery. Mobile. MVC устанавливает следующие компоненты:

- *Приложение\_файл старт\бундлемобилеконфиг.КС* , которое требуется для ссылки на добавленные файлы JavaScript и CSS. Следуйте приведенным ниже инструкциям и укажите ссылку на мобильный пакет, определенный в этом файле.
- Мобильные файлы CSS для jQuery.
- Мини-приложение контроллера `ViewSwitcher` (*контроллерс\виевсвитчерконтроллер.КС*).
- файлы JavaScript мобильных приложений jQuery.
- Файл макета jQuery в стиле мобильного устройства (*Views\Shared\\_layout. Mobile. cshtml*).
- Частичное представление *(мвкмобиле\виевс\шаред\\_ViewSwitcher. cshtml*), которое предоставляет ссылку в верхней части каждой страницы для переключения из представления рабочего стола в мобильное представление и наоборот.
- Несколько файлов изображений<em>PNG</em> и <em>GIF</em> в папке <em>контент\имажес</em>

Откройте файл *Global. asax* и добавьте следующий код в качестве последней строки метода `Application_Start`.

[!code-csharp[Main](aspnet-mvc-4-mobile-features/samples/sample10.cs)]

В следующем коде показан полный файл *Global. asax* .

[!code-csharp[Main](aspnet-mvc-4-mobile-features/samples/sample11.cs?highlight=26)]

> [!NOTE]
> Если вы используете Internet Explorer 9 и вы не видите строку `BundleMobileConfig` выше в желтом выделе, нажмите кнопку [Просмотр совместимости](https://windows.microsoft.com/windows7/How-to-use-Compatibility-View-in-Internet-Explorer-9)на кнопке![представления совместимости (отключено)](https://res2.windows.microsoft.com/resbox/en/Windows 7/main/f080e77f-9b66-4ac8-9af0-803c4f8a859c_15.jpg "Изображение кнопки представления "совместимость" (выкл.)") в IE, чтобы значок был изменен с помощью ![изображения кнопки представления совместимости (выключено)](https://res2.windows.microsoft.com/resbox/en/Windows 7/main/f080e77f-9b66-4ac8-9af0-803c4f8a859c_15.jpg "Изображение кнопки представления "совместимость" (выкл.)") на сплошной цветовой ![Рисунок кнопки представления совместимости (вкл.)](https://res1.windows.microsoft.com/resbox/en/Windows 7/main/156805ff-3130-481b-a12d-4d3a96470f36_14.jpg "Рисунок кнопки представления "совместимость" (вкл.)"). Кроме того, этот учебник можно просмотреть в браузере FireFox или Chrome.

Откройте файл *мвкмобиле\виевс\шаред\\_layout. Mobile. cshtml* и добавьте следующую разметку непосредственно после вызова `Html.Partial`:

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample12.cshtml)]

Полный файл *мвкмобиле\виевс\шаред\\_layout. Mobile. cshtml* показан ниже:

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample13.cshtml)]

Создайте приложение и в эмуляторе браузера мобильного устройства перейдите к представлению *AllTags* . Отображается следующее:

[![p3_afterNuGet](aspnet-mvc-4-mobile-features/_static/image23.png)](aspnet-mvc-4-mobile-features/_static/image22.png)

> [!NOTE]
> Можно выполнить отладку кода, относящегося к мобильным устройствам, [задав строку агента пользователя](http://www.howtogeek.com/113439/how-to-change-your-browsers-user-agent-without-installing-any-extensions/) для IE или Chrome на iPhone, а затем используя инструменты разработчика F-12. Если в браузере мобильного устройства не отображаются ссылки " **Домашняя страница**", " **докладчик**", " **тег**" и " **Дата** " в качестве кнопок, ссылки на мобильные сценарии jQuery и файлы CSS, вероятно, являются неправильными.

В дополнение к изменениям стиля отображается **мобильное представление** и ссылка, позволяющая переключиться из мобильного представления в режим рабочего стола. Выберите ссылку **представление рабочего стола** , и отобразится представление рабочего стола.

[![p3_desktopView](aspnet-mvc-4-mobile-features/_static/image25.png)](aspnet-mvc-4-mobile-features/_static/image24.png)

Представление "Рабочий стол" не позволяет напрямую вернуться к представлению для мобильных устройств. Это будет исправлено сейчас. Откройте файл *Views\Shared\\_layout. cshtml* . В элементе `body` страницы добавьте следующий код, который визуализирует мини-приложение для переключения представлений:

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample14.cshtml)]

Обновите представление *AllTags* в браузере для мобильных устройств. Теперь вы можете перемещаться между рабочими столами и мобильными представлениями.

[![p3_desktopViewWithMobileLink](aspnet-mvc-4-mobile-features/_static/image27.png)](aspnet-mvc-4-mobile-features/_static/image26.png)

> [!NOTE]
> Примечание к отладке. можно добавить следующий код в конец Views\Shared\\_ViewSwitcher. cshtml, чтобы упростить отладку представлений при использовании браузера. строка агента пользователя задается как мобильное устройство.
>
> [!code-csharp[Main](aspnet-mvc-4-mobile-features/samples/sample15.cs)]
>
> и добавьте следующий заголовок в файл *Views\Shared\\_layout. cshtml* .
>
> [!code-html[Main](aspnet-mvc-4-mobile-features/samples/sample16.html)]

Перейдите на страницу *AllTags* в браузере для настольных систем. Мини-приложение переключения представлений не отображается в браузере настольных систем, так как оно добавляется только на страницу макета для мобильных устройств. Далее в этом руководстве вы узнаете, как добавить мини-приложение "представление — переключатель" в представление рабочего стола.

[![p3_desktopBrowser](aspnet-mvc-4-mobile-features/_static/image29.png)](aspnet-mvc-4-mobile-features/_static/image28.png)

## <a name="improving-the-speakers-list"></a>Улучшение списка докладчиков

В браузере мобильного устройства выберите ссылку **Speakers** . Так как отсутствует мобильное представление (*AllSpeakers. Mobile. cshtml*), динамики по умолчанию (*AllSpeakers. cshtml*) отображаются с использованием представления мобильного макета ( *\_Layout. Mobile. cshtml*).

[![p3_speakersDeskTop](aspnet-mvc-4-mobile-features/_static/image31.png)](aspnet-mvc-4-mobile-features/_static/image30.png)

Вы можете глобально отключить представление по умолчанию (не мобильное) от подготовки к просмотру в мобильном макете, задав для параметра `RequireConsistentDisplayMode` значение `true` в файле *views\\_ViewStart. cshtml* , например:

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample17.cshtml)]

Если `RequireConsistentDisplayMode` имеет значение `true`, макет для мобильных устройств (<em>\_Layout. Mobile. cshtml</em>) используется только для мобильных представлений. (То есть файл представления имеет вид <em>* * ViewName</em><em>. Mobile. cshtml</em>.) вы можете задать `RequireConsistentDisplayMode` для `true`, если макет для мобильных устройств не работает с представлениями, не являющимися мобильными. На снимке экрана ниже показано, как отображается страница « <em>динамики</em> », когда `RequireConsistentDisplayMode` имеет значение `true`.

[![p3_speakersConsistent](aspnet-mvc-4-mobile-features/_static/image33.png)](aspnet-mvc-4-mobile-features/_static/image32.png)

Можно отключить режим отображения в представлении, установив для `RequireConsistentDisplayMode` значение `false` в файле представления. Следующая разметка в файле *виевс\хоме\аллспеакерс.кштмл* задает `RequireConsistentDisplayMode` для `false`:

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample18.cshtml)]

## <a name="creating-a-mobile-speakers-view"></a>Создание представления "Мобильные динамики"

Как вы только что увидели, представление *Speakers* удобно для чтения, но ссылки слишком малы, и касаться их на мобильном устройстве трудно. В этом разделе вы создадите представление *колонок* для мобильных устройств, которое похоже на современное мобильное приложение — оно отображает большие и простые ссылки и содержит поле поиска для быстрого поиска докладчиков.

Скопируйте *AllSpeakers. cshtml* в *AllSpeakers. Mobile. cshtml*. Откройте файл *AllSpeakers. Mobile. cshtml* и удалите элемент заголовка `<h2>`.

В теге `<ul>` добавьте атрибут `data-role` и задайте для него значение `listview`. Как и другие [атрибуты`data-*`](http://html5doctor.com/html5-custom-data-attributes/), `data-role="listview"` упрощает касание больших элементов списка. Вот как выглядит готовая разметка:

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample19.cshtml)]

Обновите браузер для мобильных устройств. Обновленное представление выглядит следующим образом:

[![p3_updatedSpeakerView1](aspnet-mvc-4-mobile-features/_static/image35.png)](aspnet-mvc-4-mobile-features/_static/image34.png)

Хотя представление для мобильных устройств Улучшено, переходить к длинному списку докладчиков очень сложно. Чтобы устранить эту проблему, добавьте в тег `<ul>` атрибут `data-filter` и задайте для него значение `true`. В приведенном ниже коде показана разметка `ul`.

[!code-html[Main](aspnet-mvc-4-mobile-features/samples/sample20.html)]

На следующем рисунке показано поле фильтра поиска в верхней части страницы, полученное из атрибута `data-filter`.

[![ps_Data_Filter](aspnet-mvc-4-mobile-features/_static/image37.png)](aspnet-mvc-4-mobile-features/_static/image36.png)

По мере ввода каждой буквы в поле поиска jQuery Mobile фильтрует отображаемый список, как показано на рисунке ниже.

[![ps_data_filter_SC](aspnet-mvc-4-mobile-features/_static/image39.png)](aspnet-mvc-4-mobile-features/_static/image38.png)

## <a name="improving-the-tags-list"></a>Улучшение списка тегов

Как и в представлении « *динамики* по умолчанию», представление « *теги* » доступно для чтения, но ссылки небольшие и трудно коснуться на мобильном устройстве. В этом разделе вы исправите представление *тегов* так же, как и в представлении « *динамики* ».

Удалите &quot;скрыть&quot; суффикса в файле *виевс\хоме\аллтагс.Мобиле.кштмл.Хиде* , чтобы его имя было *виевс\хоме\аллтагс.Мобиле.кштмл*. Откройте переименованный файл и удалите элемент `<h2>`.

Добавьте `data-role` и `data-filter` атрибуты в тег `<ul>`, как показано ниже:

[!code-html[Main](aspnet-mvc-4-mobile-features/samples/sample21.html)]

На рисунке ниже показана фильтрация страниц тегов по букве `J`.

[![p3_tags_J](aspnet-mvc-4-mobile-features/_static/image41.png)](aspnet-mvc-4-mobile-features/_static/image40.png)

## <a name="improving-the-dates-list"></a>Улучшение списка дат

Вы можете улучшить представление *дат* , например, улучшенные *динамики* и представления *тегов* , чтобы их было проще использовать на мобильном устройстве.

Скопируйте файл *виевс\хоме\аллдатес.кштмл* в *виевс\хоме\аллдатес.Мобиле.кштмл*. Откройте новый файл и удалите элемент `<h2>`.

Добавьте `data-role="listview"` в тег `<ul>` следующим образом:

[!code-html[Main](aspnet-mvc-4-mobile-features/samples/sample22.html)]

На рисунке ниже показано, как выглядит страница **даты** с `data-role`ным атрибутом.

[![p3_dates1](aspnet-mvc-4-mobile-features/_static/image43.png)](aspnet-mvc-4-mobile-features/_static/image42.png) Замените содержимое файла *виевс\хоме\аллдатес.Мобиле.кштмл* следующим кодом:

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample23.cshtml)]

Этот код группирует все сеансы по дням. Он создает разделитель списка для каждого нового дня и выводит список всех сеансов за каждый день под разделителем. Вот как это выглядит при выполнении этого кода:

[![p3_dates2](aspnet-mvc-4-mobile-features/_static/image45.png)](aspnet-mvc-4-mobile-features/_static/image44.png)

## <a name="improving-the-sessionstable-view"></a>Улучшение представления SessionsTable

В этом разделе вы создадите представление сеансов для мобильных устройств. Внесенные изменения будут более обширными, чем в других представлениях, которые мы создали.

В браузере мобильного устройства коснитесь кнопки **динамика** , а затем введите `Sc` в поле поиска.

[![ps_data_filter_SC](aspnet-mvc-4-mobile-features/_static/image47.png)](aspnet-mvc-4-mobile-features/_static/image46.png)

Коснитесь ссылки **Скотта Hanselman** .

[![p3_scottHa](aspnet-mvc-4-mobile-features/_static/image49.png)](aspnet-mvc-4-mobile-features/_static/image48.png)

Как видите, просмотр трудно читать в браузере для мобильных устройств. Столбец "Дата" трудно считать, а столбец "Теги" находится вне представления. Чтобы устранить эту проблему, скопируйте *виевс\хоме\сессионстабле.кштмл* в *виевс\хоме\сессионстабле.Мобиле.кштмл*, а затем замените содержимое файла следующим кодом:

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample24.cshtml)]

Код удаляет столбцы «комната» и «теги» и форматирует заголовок, докладчик и дату по вертикали, чтобы вся эта информация была доступна для чтения в браузере мобильного устройства. На рисунке ниже приведены изменения кода.

[![ps_SessionsByScottHa](aspnet-mvc-4-mobile-features/_static/image51.png)](aspnet-mvc-4-mobile-features/_static/image50.png)

## <a name="improving-the-sessionbycode-view"></a>Улучшение представления SessionByCode

Наконец, вы создадите представление *SessionByCode* для мобильных устройств. В браузере мобильного устройства коснитесь кнопки **динамика** , а затем введите `Sc` в поле поиска.

[![ps_data_filter_SC](aspnet-mvc-4-mobile-features/_static/image53.png)](aspnet-mvc-4-mobile-features/_static/image52.png)

Коснитесь ссылки **Скотта Hanselman** . Отобразятся сеансы Скотта Hanselman.

[![ps_SessionsByScottHa](aspnet-mvc-4-mobile-features/_static/image55.png)](aspnet-mvc-4-mobile-features/_static/image54.png)

Выберите **Обзор веб-канала MS Web** .

[![ps_love](aspnet-mvc-4-mobile-features/_static/image57.png)](aspnet-mvc-4-mobile-features/_static/image56.png)

Представление рабочего стола по умолчанию отлично, но его можно улучшить.

Скопируйте *виевс\хоме\сессионбикоде.кштмл* в *виевс\хоме\сессионбикоде.Мобиле.кштмл* и замените содержимое файла *виевс\хоме\сессионбикоде.Мобиле.кштмл* следующей разметкой:

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample25.cshtml)]

Новая разметка использует атрибут `data-role` для улучшения макета представления.

Обновите браузер для мобильных устройств. Следующий рисунок отражает только что внесенные в код изменения:

[![p3_love2](aspnet-mvc-4-mobile-features/_static/image59.png)](aspnet-mvc-4-mobile-features/_static/image58.png)

## <a name="wrapup-and-review"></a>Врапуп и обзор

В этом учебнике появились новые мобильные функции в предварительной версии ASP.NET MVC 4 для разработчиков. К мобильным функциям относятся:

- Возможность определять макет, представления и частичные представления как глобально, так и для отдельного представления.
- Управление макетом и принудительным применением частичного переопределения с помощью свойства `RequireConsistentDisplayMode`.
- Мини-приложение переключателя представления для мобильных представлений, которое также может отображаться в представлениях рабочего стола.
- Поддержка поддержки конкретных браузеров, например браузера iPhone.

## <a name="see-also"></a>См. также:

- сайт [jQuery Mobile](http://jquerymobile.com) .
- [Общие сведения о jQuery Mobile](http://jquerymobile.com/demos/1.0b3/docs/about/intro.html)
- [Рекомендации от W3C по веб-приложениям для мобильных устройств](http://www.w3.org/TR/mwabp/)
- [Проектные рекомендации от W3C по запросам мультимедиа](http://www.w3.org/TR/css3-mediaqueries/)
