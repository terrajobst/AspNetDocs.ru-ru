---
uid: web-pages/overview/getting-started/aspnet-web-pages-razor-faq
title: Вопросы и ответы по веб-страницы ASP.NET (Razor) | Документация Майкрософт
author: Rick-Anderson
description: В этой статье перечислены часто задаваемые вопросы о веб-страницы ASP.NET (Razor) и WebMatrix. Версии программного обеспечения, используемые в руководстве веб-страницы ASP.NET (R...
ms.author: riande
ms.date: 02/07/2014
ms.assetid: b137bd04-25e1-47cb-9d96-ef2e179ecf1f
msc.legacyurl: /web-pages/overview/getting-started/aspnet-web-pages-razor-faq
msc.type: authoredcontent
ms.openlocfilehash: 6fa1b668e915af856a693e79eafb7180ed504dc2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78520656"
---
# <a name="aspnet-web-pages-razor-faq"></a>Вопросы и ответы по веб-страницам ASP.NET (Razor)

от [Tom фитзмаккен](https://github.com/tfitzmac)

> > [!NOTE] 
> > WebMatrix больше не рекомендуется использовать в качестве интегрированной среды разработки для веб-страницы ASP.NET. Используйте [Visual Studio](xref:aspnet/web-pages/overview/getting-started/program-asp-net-web-pages-in-visual-studio) или [Visual Studio Code](https://code.visualstudio.com/).
>
> В этой статье перечислены часто задаваемые вопросы о веб-страницы ASP.NET (Razor) и WebMatrix.
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>Версии программного обеспечения, используемые в этом руководстве
> 
> 
> - Веб-страницы ASP.NET (Razor) 3
> - Visual Studio 2013
> - WebMatrix 3
>   
> 
> Этот учебник также работает с веб-страницы ASP.NET 2, WebMatrix 2 и Visual Studio 2012.

- [В чем разница между веб-страницы ASP.NET, веб-формами ASP.NET и ASP.NET MVC?](#Whats_the_difference_between_ASP.NET_Web_Pages,_ASP.NET_Web_Forms,_and_ASP.NET_MVC)
- [Нужен ли WebMatrix для работы с веб-страницами?](#Do_I_need_WebMatrix_in_order_to_work_with_Web_Pages)
- [Можно ли использовать элементы управления веб-форм ASP.NET на странице веб-страниц?](#Can_I_use_ASP.NET_Web_Forms_controls_on_a_Web_Pages_page)
- [Можно ли развернуть веб-страницы ASP.NET сайт без использования WebMatrix?](#Can_I_deploy_an_ASP.NET_Web_Pages_site_without_using_WebMatrix)
- [Нужно ли использовать вспомогательный модуль безопасности для поддержки имен входа?](#Do_I_have_to_use_the_WebSecurity_helper_to_support_logins)
- [Поддерживает ли веб-страницы ASP.NET HTML5?](#Does_ASP.NET_Web_Pages_support_HTML5)
- [Можно ли использовать JavaScript и jQuery с веб-страницами?](#Can_I_use_JavaScript_and_jQuery_with_Web_Pages)
- [Дополнительные ресурсы](#AdditionalResources)

Вопросы об ошибках и других проблемах см. в разделе [руководство по устранению неполадок веб-страницы ASP.NET (Razor)](https://go.microsoft.com/fwlink/?LinkId=253001).

<a id="Whats_the_difference_between_ASP.NET_Web_Pages,_ASP.NET_Web_Forms,_and_ASP.NET_MVC"></a>
## <a name="whats-the-difference-between-aspnet-web-pages-aspnet-web-forms-and-aspnet-mvc"></a>В чем разница между веб-страницы ASP.NET, веб-формами ASP.NET и ASP.NET MVC?

Все три являются ASP.NET технологиями для создания динамических веб-приложений:

- Веб-страницы ASP.NET рассказывает о добавлении динамического кода (на стороне сервера) и доступе к базе данных к HTML-страницам и простых и упрощенных синтаксисов.
- Веб-формы ASP.NET основаны на объектной модели страницы и традиционных элементах управления окнами (кнопки, списки и т. д.). Веб-формы используют модель на основе событий, которая знакома тем, кто работал с разработкой на основе клиента (Windows Forms).
- ASP.NET MVC реализует шаблон модель-представление-контроллер для ASP.NET. Особое внимание уделяется «разделению проблем» (обработка, данные и уровни пользовательского интерфейса).

Все три платформы полностью поддерживаются и продолжают разрабатываться командой ASP.NET. Как правило, выбор используемой платформы зависит от фона и опыта работы с ASP.NET.

Веб-страницы ASP.NET в частности, была разработана, чтобы облегчить пользователям, которые уже знакомы с HTML, добавлять серверную обработку на страницы. Это хороший вариант для учащихся, любителей, людей в целом, которые не знакомы с программированием. Это также может быть хорошим выбором для разработчиков, имеющих опыт работы с веб-технологиями non-ASP.NET.

<a id="Do_I_need_WebMatrix_in_order_to_work_with_Web_Pages"></a>
## <a name="do-i-need-webmatrix-in-order-to-work-with-web-pages"></a>Нужен ли WebMatrix для работы с веб-страницами?

Нет. WebMatrix больше не рекомендуется использовать в качестве интегрированной среды разработки для веб-страницы ASP.NET. Используйте [Visual Studio](program-asp-net-web-pages-in-visual-studio.md) или [Visual Studio Code](https://code.visualstudio.com/).

Если вы не хотите использовать Visual Studio или Visual Studio Code, можно установить компоненты отдельных продуктов с помощью [установщик веб-платформы Майкрософт](https://www.microsoft.com/web/downloads/platform.aspx). Вам потребуются следующие продукты:

- Microsoft .NET Framework 4.5
- ASP.NET MVC 5 (который также устанавливает веб-страницы ASP.NET Framework)
- IIS Express (веб-сервер)
- Microsoft SQL Server Compact 4,0 (база данных)

Для редактирования страниц *. cshtml* (или *. vbhtml*) можно использовать текстовый редактор.

Управление базами данных SQL Server Compact (*SDF* -файлы) без инструмента немного сложнее. Средства Visual Studio контаиндс для управления базами данных *. sdf* . Вы также можете выполнять команды SQL в коде для выполнения многих задач управления SQL Server.

Для проверки страниц *. cshtml* без использования интегрированной среды разработки (IDE) их можно развернуть на активном сервере. (См [. раздел можно ли развернуть веб-страницы ASP.net сайт без использования WebMatrix?](#Can_I_deploy_an_ASP.NET_Web_Pages_site_without_using_WebMatrix))

### <a name="running-iis-express-without-using-an-ide"></a>Запуск IIS Express без использования интегрированной среды разработки

При установке IIS Express на компьютере в качестве веб-сервера его можно использовать для тестирования страниц. Можно запустить IIS Express из командной строки и связать ее с конкретным номером порта. Затем этот порт указывается при запросе *CSHTML* файлов в браузере.

В Windows откройте командную строку с правами администратора и измените значение на *C:\Program Files\IIS Express.* (Для 64-разрядных систем используйте папку *C:\Program Files (x86) \Иис Express.)* Затем введите следующую команду, используя фактический путь к сайту:

`iisexpress.exe /port:35896 /path:C:\BasicWebSite`

Можно использовать любой номер порта, который еще не зарезервирован другим процессом. (Обычно номера портов выше 1024.) Для значения `path` используйте путь к папке веб-сайта, в которой находятся файлы. *CSHTML* .

После выполнения этой команды для настройки IIS Express для обслуживания страниц можно открыть браузер и выбрать *CSHTML* -файл. Используйте URL-адрес, как в следующем примере:

`http://localhost:35896/default.cshtml`

Чтобы получить справку по IIS Express параметров командной строки, введите `iisexpress.exe /?` в командной строке.

<a id="Can_I_use_ASP.NET_Web_Forms_controls_on_a_Web_Pages_page"></a>
## <a name="can-i-use-aspnet-web-forms-controls-on-a-web-pages-page"></a>Можно ли использовать элементы управления веб-форм ASP.NET на странице веб-страниц?

Нет. Элементы управления веб-форм, такие как элемент управления [CheckBox](https://msdn.microsoft.com/library/system.web.ui.webcontrols.checkbox) , [элементы управления проверки](https://msdn.microsoft.com/library/bwd43d0x)и элемент управления [GridView](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview) , работают только на страницах Web Forms (*ASPX* -файлы). Для этих элементов управления требуется платформа страницы веб-форм.

<a id="Can_I_deploy_an_ASP.NET_Web_Pages_site_without_using_WebMatrix"></a>
## <a name="can-i-deploy-an-aspnet-web-pages-site-without-using-webmatrix"></a>Можно ли развернуть веб-страницы ASP.NET сайт без использования WebMatrix?

Да. Можно вручную скопировать файлы веб-сайта на сервер (обычно с помощью FTP). При выполнении ручного копирования также необходимо скопировать файлы, поддерживающие SQL Server Compact (база данных). Дополнительные сведения см. в записи блога [развертывание приложений веб-страниц без инструмента](http://mikepope.com/blog/DisplayBlog.aspx?permalink=2317).

<a id="Do_I_have_to_use_the_WebSecurity_helper_to_support_logins"></a>
## <a name="do-i-have-to-use-the-websecurity-helper-to-support-logins"></a>Нужно ли использовать вспомогательный модуль безопасности для поддержки имен входа?

Нет. Поставщик `SimpleMembership`, который является частью веб-страницы ASP.NET, является одним из вариантов. Также доступны поставщики безопасности, являющиеся частью ASP.NET (которые могут использоваться для работы с веб-формами). Например, можно использовать проверку подлинности с помощью форм в веб-страницы ASP.NET точно так же, как в веб-формах. Один из примеров использования проверки подлинности с помощью форм см. в служба поддержки Майкрософт статье [Реализация проверки подлинности на основе форм в приложении ASP.NET C#с использованием .NET](https://support.microsoft.com/kb/301240). Чтобы скачать простой пример, см. статью [ASP.NET версии &amp; Password](http://www.codeguru.com/csharp/.net/net_asp/scripting/article.php/c19295/ASPNET-version-of-Login--Password.htm).

Сведения об использовании проверки подлинности Windows см. в записи блога [использование проверки подлинности Windows в веб-страницы ASP.NET](http://mikepope.com/blog/DisplayBlog.aspx?permalink=2298).

<a id="Does_ASP.NET_Web_Pages_support_HTML5"></a>
## <a name="does-aspnet-web-pages-support-html5"></a>Поддерживает ли веб-страницы ASP.NET HTML5?

Да. Страницы, создаваемые с веб-страницы ASP.NET ( *. cshtml* или *. vbhtml* ), представляют собой HTML-страницы, которые также содержат код, выполняемый на сервере до подготовки страницы к просмотру. Пока браузер пользователя поддерживает HTML5, можно использовать элементы HTML5 на странице *. cshtml* или *. vbhtml* .

<a id="Can_I_use_JavaScript_and_jQuery_with_Web_Pages"></a>
## <a name="can-i-use-javascript-and-jquery-with-web-pages"></a>Можно ли использовать JavaScript и jQuery с веб-страницами?

Конечно. Страницы, создаваемые с веб-страницы ASP.NET ( *. cshtml* или *. vbhtml* ), представляют собой HTML-страницы с серверным кодом. Таким образом, все, что можно сделать на обычной HTML-странице с помощью JavaScript или jQuery, можно также сделать на странице *. cshtml* или *. vbhtml* .

Шаблон **начального сайта** в WebMatrix содержит несколько библиотек jQuery. При создании сайта с помощью этого шаблона папка *Scripts* содержит библиотеку ядра jQuery (*жкуери-1.6.2. js)* и библиотеки для проверки JQuery (*jQuery. Validate. js*и т. д.).

Ниже приведены некоторые записи в блоге, иллюстрирующие способы использования jQuery с веб-страницы ASP.NET.

- [Добавление "jQuery" в веб-страницы ASP.NET с помощью WebMatrix](http://rachelappel.com/jquery/adding-jquery-goodness-to-asp-net-web-pages-using-webmatrix/) с Рейчел Аппель (
- [5 мин: WebMatrix + пользовательский интерфейс jQuery + JSON + jQuery Templates](http://joeriks.com/2011/01/30/5-min-webmatrix-jquery-ui-json-jquery-templates/) by Йонас Ерикссон
- [Формы WebMatrix и jQuery](http://mikesdotnetting.com/Article/155/WebMatrix-And-jQuery-Forms) по Майк бринд

<a id="AdditionalResources"></a>
## <a name="additional-resources"></a>Дополнительные ресурсы

[Руководство по устранению неполадок веб-страниц ASP.NET (Razor)](https://go.microsoft.com/fwlink/?LinkId=253001)

[Форум WebMatrix и веб-страницы ASP.NET](https://forums.asp.net/1224.aspx/1?WebMatrix) на веб-сайте ASP.NET
