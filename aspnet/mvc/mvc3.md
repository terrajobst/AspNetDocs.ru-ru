---
uid: mvc/mvc3
title: ASP.NET MVC 3 | Документация Майкрософт
author: rick-anderson
description: (включает в себя апреля 2011 г. средства обновления) ASP.NET MVC 3 — это платформа для создания масштабируемых, основанные на стандартах веб-приложений, с использованием шаблона проектирования, широко известных...
ms.author: riande
ms.date: 10/05/2010
ms.assetid: dddc8812-a0bc-49f9-aafb-caf2064c2b8c
msc.legacyurl: /mvc/mvc3
msc.type: content
ms.openlocfilehash: 82d18865815568c5df9768fd9dd403f11ebd1714
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57045431"
---
<a name="aspnet-mvc-3"></a>ASP.NET MVC 3
====================
> *(включает в себя апреля 2011 г. средства обновления)*
> 
> ASP.NET MVC 3 — это платформа для создания масштабируемых, основанные на стандартах веб-приложений, с помощью хорошо проверенных шаблонах проектирования и возможности ASP.NET и .NET Framework.
> 
> Он устанавливает side-by-side с ASP.NET MVC 2, чтобы начать использовать ее уже сегодня!
> 
> Скачайте [установщик здесь](https://go.microsoft.com/fwlink/?LinkID=208140)


## <a name="top-features"></a>Лучшие компоненты

- Интегрированная система формирования шаблонов, расширяемой с помощью NuGet
- Шаблоны HTML 5 поддержкой проектов
- Выразительный представления, включая новый обработчик представлений Razor
- Мощные обработчиков с помощью внедрения зависимостей и глобальные фильтры действий
- Поддержка Rich JavaScript ненавязчивый JavaScript, проверки jQuery и привязки JSON
- *Чтение списка все функции [ниже](#overview)*

## <a name="top-links"></a>Ссылок на ведущие

Новые возможности в ASP.NET MVC 3

- Фил Хаак: [ASP.NET MVC 3 выпуска](http://haacked.com/archive/2011/01/13/aspnetmvc3-released.aspx)
- Скотт Хансельман: [ASP.NET MVC3 WebMatrix, NuGet, IIS Express и Orchard выпущены - выпуска Web января корпорации Майкрософт в контексте](http://www.hanselman.com/blog/ASPNETMVC3WebMatrixNuGetIISExpressAndOrchardReleasedTheMicrosoftJanuaryWebReleaseInContext.aspx)
- Скотт Гатри: [Объявление о выпуске ASP.NET MVC 3, IIS Express, SQL CE 4, Web Farm Framework, Orchard, WebMatrix](https://weblogs.asp.net/scottgu/archive/2011/01/13/announcing-release-of-asp-net-mvc-3-iis-express-sql-ce-4-web-farm-framework-orchard-webmatrix.aspx)
- [Заметки о выпуске для ASP.NET MVC 3](../whitepapers/mvc3-release-notes.md)

Установка и справки

- Установка с помощью ASP.NET MVC 3 [установщика веб-платформы (рекомендуется)](https://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MVC3)
- Установка с помощью ASP.NET MVC 3 [исполняемого файла установщика](https://go.microsoft.com/fwlink/?LinkID=208140)
- Установка [ASP.NET MVC 3 для Visual Studio 11 Developer Preview](https://go.microsoft.com/fwlink/?LinkID=208140)
- Чтение [введение к руководству по ASP.NET MVC 3](overview/older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)
- Получение справки и обсудить ASP.NET MVC 3 в [форумы](https://forums.asp.net/1146.aspx)

<a id="overview"></a>
## <a name="aspnet-mvc-3-overview"></a>Общие сведения о ASP.NET MVC 3

ASP.NET MVC 3 лежит ASP.NET MVC 1 и 2, добавление полезных функций, как упростить код и разрешить глубже расширяемости. В этом разделе представлен обзор многих новых функций, включенных в этот выпуск, включает следующие разделы:

- [Расширяемая формирования шаблонов с интеграцией MvcScaffold](#BM_MvcScaffolding)
- [Шаблоны HTML 5 поддержкой проектов](#BM_HTML5)
- [Подсистема просмотра Razor](#BM_TheRazorViewEngine)
- [Поддержка нескольких обработчиков представлений](#BM_Support_for_Multiple_View_Engines)
- [Усовершенствования контроллера](#BM_Controller_Improvements)
- [JavaScript и Ajax](#BM_JavaScript_and_Ajax_Improvements)
- [Усовершенствования проверки модели](#BM_Model_Validation_Improvements)
- [Улучшения внедрения зависимостей](#BM_Dependency_Injection_Improvements)
- [Другие новые функции](#BM_Other_New_Features)

<a id="BM_MvcScaffolding"></a>

## <a name="extensible-scaffolding-with-mvcscaffold-integration"></a>Расширяемая формирования шаблонов с интеграцией MvcScaffold

Новая система формирования шаблонов упрощает взять и приступить к использованию продуктивно, если вы полностью знакомы с платформой, а также автоматизации основных задач разработки, если вы являетесь опытным и уже знаете, что он делает.

Это поддерживается новый NuGet *формирования шаблонов* пакета, который называется **MvcScaffolding**. Термин «Формирование шаблонов» используется много технологий программного обеспечения для обозначения «быстрого создания базовая схема программного обеспечения, вы можете отредактировать и настроить». Формирование шаблонов пакета, который мы создаем для ASP.NET MVC значительно целесообразно использовать в различных сценариях:

- **Если при изучении ASP.NET MVC в первый раз**, так как он предоставляет быстрый способ получить некоторые полезные, рабочего кода, который можно редактировать и адаптировать в соответствии с потребностями. Избавляет вас от trauma просмотрев пустая страница и необходимости не знает, с которого следует начать!
- **Если сообщайте ASP.NET MVC и теперь исследования новые технологии надстройка** например объектно реляционного сопоставления, обработчик представлений, библиотеку тестирования, и так далее, так как создатель этой технологии может также создать пакет формирования шаблонов для него.
- **Если результаты работы включает в себя несколько раз Создание схожие классов или файлы какого-либо рода**, так как можно создать настраиваемых средств формирования шаблонов, которые выводят средства тестирования, сценарии развертывания, или что-нибудь еще необходимо. Всем участникам рабочей группы можно также использовать настраиваемых средств формирования шаблонов.

Другие функции в MvcScaffolding:

- Поддержка для проектов C# и VB
- Поддержка Razor и ASPX просмотреть ядер
- Поддерживает формирование шаблонов в области ASP.NET MVC и использованию представления макеты и мастеров
- Вы можете легко настроить выходные данные, изменив шаблоны T4
- Вы можете добавить совершенно новых средств формирования шаблонов, с помощью пользовательской логики PowerShell и настраиваемых шаблонов T4. Эти (и любые настраиваемые параметры, которые вы предоставили их) автоматически отображается в списке завершения консоли.
- Вы можете получить пакеты NuGet, содержащие дополнительных средств формирования шаблонов для различных технологий (например,--экспериментальную один для LINQ to SQL теперь есть) и смешивать мороженое их друг с другом

Обновления средств ASP.NET MVC 3 включает в себя отличную поддержку Visual Studio для этого система формирования шаблонов, таких как:

- Добавление контроллера диалоговое окно теперь поддерживает полное автоматическое формирование шаблонов контроллера действия Create, Read, Update и Delete и представлениями. По умолчанию это формирует шаблоны кода доступа к данным с помощью EF Code First.
- Добавление контроллера диалоговое окно поддерживает *расширяемый элементов скаффолдинга* с помощью NuGet пакеты, такие как *MvcScaffolding*. Это дает возможность подключать формирует пользовательский шаблон в диалоговое окно, что позволит вам создать формирует шаблон для других технологий доступа к данным, например NHibernate или даже JET с технология ODBCDirect, если при желании!

Дополнительные сведения о формирования шаблонов в ASP.NET MVC 3 см. следующие ресурсы:

- Стив Сандерсон post серии, включает в себя: 

    1. [Общие сведения о: Сформировать шаблон проекта ASP.NET MVC 3 с пакетом mvcscaffolding](http://blog.stevensanderson.com/2011/01/13/scaffold-your-aspnet-mvc-3-project-with-the-mvcscaffolding-package/)
    2. [Стандартное использование: Типичными примерами использования и параметры](http://blog.stevensanderson.com/2011/01/13/mvcscaffolding-standard-usage/)
    3. [Один ко многим связей](http://blog.stevensanderson.com/2011/01/28/mvcscaffolding-one-to-many-relationships/)
    4. [Действия формирования шаблонов и модульные тесты](http://blog.stevensanderson.com/2011/03/28/scaffolding-actions-and-unit-tests-with-mvcscaffolding/)
    5. [Переопределение шаблоны T4](http://blog.stevensanderson.com/2011/04/06/mvcscaffolding-overriding-the-t4-templates/)
    6. [Это сообщение: Создание настраиваемых средств формирования шаблонов](http://blog.stevensanderson.com/2011/04/07/mvcscaffolding-creating-custom-scaffolders/)
- Блога Скотта Хансельмана от свой сеанс конференции PDC 2010 [построение блог с Microsoft «Без имени пакета из Web Love»](http://www.hanselman.com/blog/PDC10BuildingABlogWithMicrosoftUnnamedPackageOfWebLove.aspx)
- [Заметки о выпуске MVC 3](../whitepapers/mvc3-release-notes.md)

<a id="BM_HTML5"></a>

## <a name="html-5-project-templates"></a>Шаблоны HTML 5 проектов

Диалоговое окно Новый проект включает в себя версии флажок enable HTML 5 шаблонов проектов. Эти шаблоны использовать добавлена библиотека Modernizr 1.7 для предоставления поддержки совместимости для HTML 5 и CSS 3 в старых браузерах.

<a id="BM_TheRazorViewEngine"></a>

## <a name="the-razor-view-engine"></a>Подсистема просмотра Razor

ASP.NET MVC 3 поставляется с новый обработчик представлений с именем Razor, которая обеспечивает следующие преимущества:

- Синтаксис Razor — план в четком и краткими, требуя минимальное количество нажатий клавиш.
- Razor — прост в изучении, отчасти потому, что он основан на существующих языков, таких как C# и Visual Basic.
- Visual Studio включает выделение цветом IntelliSense и кода для синтаксиса Razor.
- Представления Razor можно подвергать модульному тестированию без запуска приложения и запустить веб-сервер.

Ниже приведены некоторые новые возможности Razor:

- `@model` синтаксис для указания типа, передаваемого в представление.
- `@* *@` синтаксис комментария.
- Возможность задавать значения по умолчанию (такие как `layoutpage`) один раз для всего узла.
- `Html.Raw` Метод для отображения текста без HTML-кодирование его.
- Поддержка совместного использования кода между несколькими представлениями (*\_viewstart.cshtml* или  *\_viewstart.vbhtml* файлов).

Razor также включает новые вспомогательные методы HTML, например следующие:

- `Chart`. Отображает диаграмму, предлагает те же функции, что элемент управления диаграммы в ASP.NET 4.
- `WebGrid`. Отображает сетку данных, дополненный функциональные возможности разбиения по страницам и сортировки.
- `Crypto`. Используется хэширование алгоритмов для создания правильно дополнительные salt-значения и хэшированные пароли.
- `WebImage`. Выводит изображение на экран.
- `WebMail`. Отправляет сообщение электронной почты.

Дополнительные сведения о Razor см. следующие ресурсы:

- [Введение в Razor блога Скотта Гатри](https://weblogs.asp.net/scottgu/archive/2010/07/02/introducing-razor.aspx)
- [Знакомство с post блог Скотта Гатри @model ключевое слово](https://weblogs.asp.net/scottgu/archive/2010/10/19/asp-net-mvc-3-new-model-directive-support-in-razor.aspx)
- [Знакомство с макеты Razor блога Скотта Гатри](https://weblogs.asp.net/scottgu/archive/2010/10/22/asp-net-mvc-3-layouts.aspx)
- [Razor краткий справочник по API](../web-pages/overview/api-reference/asp-net-web-pages-api-reference.md)
- [Заметки о выпуске MVC 3](../whitepapers/mvc3-release-notes.md)

<a id="BM_Support_for_Multiple_View_Engines"></a>

## <a name="support-for-multiple-view-engines"></a>Поддержка нескольких обработчиков представлений

**Добавление представления** диалогового окна в ASP.NET MVC 3 позволяет выбрать обработчик представлений, которые вы собираетесь работать, и **новый проект** диалоговое окно позволяет указать обработчик представлений по умолчанию для проекта. Вы можете подсистема просмотра веб-форм (ASPX), Razor или обработчик представлений с открытым исходным кодом например [Spark](http://sparkviewengine.com/), [NHaml](https://code.google.com/p/nhaml/), или [NDjango](http://ndjango.org/).

<a id="BM_Controller_Improvements"></a>

## <a name="controller-improvements"></a>Усовершенствования контроллера

### <a name="global-action-filters"></a>Глобальные фильтры действий

Иногда требуется выполнить логику до запуска метода действия или после запуска метода действия. Для этого в ASP.NET MVC 2 предоставляются фильтры действий. Фильтры действий представляют собой настраиваемые атрибуты, предоставляющие декларативные средства для добавления поведения перед действием и после действия к конкретному контроллеру методам действий. Однако в некоторых случаях может потребоваться указать поведение предварительного действия или после действия, которое применяется ко всем методам действий. MVC 3 позволяет указать глобальные фильтры, добавив их в `GlobalFilters` коллекции. Дополнительные сведения о глобальные фильтры действий см. следующие ресурсы:

- [Блог Скотта Гатри о предварительной версии MVC 3](https://weblogs.asp.net/scottgu/archive/2010/07/27/introducing-asp-net-mvc-3-preview-1.aspx)
- [Фильтрация в ASP.NET MVC](https://msdn.microsoft.com/library/gg416513(VS.98).aspx)

### <a name="new-viewbag-property"></a>Новое свойство «ViewBag»

Поддержка контроллеров MVC 2 `ViewData` свойство, которое дает возможность передачи данных в шаблон представления, с помощью API словаря с поздним связыванием. В MVC 3, можно также использовать довольно простой синтаксис с `ViewBag` свойство для выполнения той же цели. Например, вместо написания `ViewData["Message"]="text"`, можно написать `ViewBag.Message="text"`. Необходимо определить все строго типизированные классы для использования `ViewBag` свойство. Так как это динамическое свойство, можно вместо этого просто получить или набор свойств, а разрешит их динамически во время выполнения. На внутреннем уровне `ViewBag` свойства хранятся в виде пары имя/значение в `ViewData` словаря. (Примечание: в большинстве предварительных версий MVC 3, `ViewBag` свойство называлось `ViewModel` свойство.)

### <a name="new-actionresult-types"></a>Новые типы «ActionResult»

Следующие `ActionResult` типы и соответствующие вспомогательные методы являются новые или улучшенные в MVC 3:

- [HttpNotFoundResult](https://msdn.microsoft.com/library/system.web.mvc.httpnotfoundresult(v=vs.98).aspx). Возвращает код состояния HTTP 404 клиенту.
- [RedirectResult](https://msdn.microsoft.com/library/system.web.mvc.redirectresult(v=VS.98).aspx). Возвращает Временное перенаправление (код состояния HTTP 302) или постоянное перенаправление (код состояния HTTP 301), в зависимости от логического параметра. В сочетании с этим изменением [контроллера](https://msdn.microsoft.com/library/system.web.mvc.controller(v=VS.98).aspx) класс теперь имеет три метода для выполнения постоянной переадресации: `RedirectPermanent`, `RedirectToRoutePermanent`, и `RedirectToActionPermanent`. Эти методы возвращают экземпляр `RedirectResult` с `Permanent` свойство значение `true`.
- [HttpStatusCodeResult](https://msdn.microsoft.com/library/system.web.mvc.httpstatuscoderesult(v=VS.98).aspx). Возвращает определяемый пользователем код состояния HTTP.

<a id="BM_JavaScript_and_Ajax_Improvements"></a>

## <a name="javascript-and-ajax-improvements"></a>JavaScript и Ajax улучшения

По умолчанию вспомогательные функции Ajax и проверки в MVC 3 использовать подход, ненавязчивый JavaScript. Ненавязчивый JavaScript позволяет избежать внесения подставляемый код JavaScript в HTML. Это делает HTML меньшего размера и менее загроможденной и облегчает выгрузить или Настройка библиотеки JavaScript. Вспомогательные методы проверки в MVC 3 также используют `jQueryValidate` подключаемого модуля по умолчанию. Если требуется поведение MVC 2, вы можете отключить ненавязчивый JavaScript с использованием *web.config* файл параметров. Дополнительные сведения об улучшениях JavaScript и Ajax см. следующие ресурсы:

- [Основные сведения о ненавязчивый JavaScript на сайте Википедии](http://en.wikipedia.org/wiki/Unobtrusive_JavaScript)
- [Брэд Вилсон Ненавязчивый JavaScript Post](http://bradwilson.typepad.com/blog/2010/10/mvc3-unobtrusive-ajax.html)
- [Post проверки ненавязчивого JavaScript Брэда уилсона:](http://bradwilson.typepad.com/blog/2010/10/mvc3-unobtrusive-validation.html)
- [Создание приложения MVC 3 с помощью Razor и ненавязчивого JavaScript](overview/older-versions/creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript.md) (учебник на веб-сайте ASP.NET)
- [Заметки о выпуске MVC 3](../whitepapers/mvc3-release-notes.md)

### <a name="client-side-validation-enabled-by-default"></a>Проверка на стороне клиента включено по умолчанию

В более ранних версиях MVC, необходимо явно вызвать `Html.EnableClientValidation` метода из представления, чтобы включить проверку на стороне клиента. В MVC 3 это больше не требуется, так как проверка на стороне клиента включено по умолчанию. (Эту функцию можно отключить с помощью параметра в *web.config* файл.)

Для проверки на стороне клиента для работы, вы по-прежнему должны для ссылки на соответствующие jQuery и библиотеки jQuery проверки узла. Можно размещать их на собственном сервере или ссылаться на них из сети доставки содержимого (CDN), как CDN корпорации Microsoft или Google.

### <a name="remote-validator"></a>Удаленный проверяющий элемент управления

ASP.NET MVC 3 поддерживает новую [RemoteAttribute](https://msdn.microsoft.com/library/system.web.mvc.remoteattribute(v=VS.98).aspx) класс, который позволяет воспользоваться преимуществами проверки jQuery подключаемых в поддержку удаленный проверяющий элемент управления. Это позволяет библиотеке клиентской проверки для автоматически вызывает пользовательский метод, который определяется на сервере, чтобы выполнить логику проверки, которая может выполняться только на стороне сервера.

В следующем примере `Remote` атрибут указывает, что проверка клиента вызовет действие с именем `UserNameAvailable` на `UsersController` класса, чтобы проверить `UserName` поля.

[!code-csharp[Main](mvc3/samples/sample1.cs)]

В следующем примере соответствующим контроллером.

[!code-csharp[Main](mvc3/samples/sample2.cs)]

Дополнительные сведения об использовании `Remote` атрибут, см. в разделе [как: Реализация удаленной проверки в ASP.NET MVC](https://msdn.microsoft.com/library/gg508808(VS.98).aspx) в библиотеке MSDN.

### <a name="json-binding-support"></a>Поддержка привязки JSON

ASP.NET MVC 3 предусмотрена встроенная поддержка JSON привязки, которая позволяет методам действия для получения данных из JSON и привязку модели его с параметрами метода действия. Эта возможность полезна в сценариях, включающих клиентских шаблонов и привязки данных. (Клиент шаблоны позволяют форматирования и отображения отдельные элементы данных или набор элементов данных с помощью шаблонов, которые выполняются на клиентском компьютере.) MVC 3 позволяет легко подключать клиентских шаблонов с методами действий на сервере, отправки и получения данных JSON. Дополнительные сведения о поддержке привязки JSON см. в разделе **JavaScript и AJAX улучшения** раздел [записи блога Скотта Гатри MVC 3 Preview](https://weblogs.asp.net/scottgu/archive/2010/07/27/introducing-asp-net-mvc-3-preview-1.aspx).

<a id="BM_Model_Validation_Improvements"></a>

## <a name="model-validation-improvements"></a>Усовершенствования проверки модели

### <a name="dataannotations-metadata-attributes"></a>Атрибуты метаданных «DataAnnotations»

ASP.NET MVC 3 поддерживает `DataAnnotations` метаданных атрибуты, такие как `DisplayAttribute`.

### <a name="validationattribute-class"></a>Класс «ValidationAttribute»

`ValidationAttribute` Класса были внесены усовершенствования в .NET Framework 4 для поддержки нового `IsValid` перегрузку, которая предоставляет дополнительные сведения о текущем контексте проверки, например, какой объект проверяется в данный момент. Это обеспечивает более широкие сценарии, где можно проверить текущее значение на основе другого свойства модели. Например, новый `CompareAttribute` атрибут позволяет сравнить значения двух свойств модели. В следующем примере `ComparePassword` свойство должно соответствовать `Password` поля, чтобы быть допустимыми.

[!code-csharp[Main](mvc3/samples/sample3.cs)]

### <a name="validation-interfaces"></a>Интерфейсы проверки

[IValidatableObject](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.ivalidatableobject.aspx) интерфейс позволяет выполнять проверку на уровне модели, и это дает возможность предоставления проверки сообщения об ошибках, относящихся к состоянию общей модели, или между двумя свойствами внутри модели . MVC 3 теперь получает ошибки из `IValidatableObject` интерфейс привязки модели и автоматически флаги и основные особенности затронутых полей в представлении, с использованием встроенных вспомогательных методов формы HTML.

[IClientValidatable](https://msdn.microsoft.com/library/system.web.mvc.iclientvalidatable(v=VS.98).aspx) интерфейс позволяет ASP.NET MVC для обнаружения во время выполнения ли проверяющий элемент управления имеет поддержку для клиентской проверки. Этот интерфейс была разработана таким образом, чтобы его можно интегрировать с различными платформами проверки.

Дополнительные сведения об интерфейсах проверки, см. в разделе **усовершенствования проверки модели** раздел [записи блога Скотта Гатри MVC 3 Preview](https://weblogs.asp.net/scottgu/archive/2010/07/27/introducing-asp-net-mvc-3-preview-1.aspx). (Тем не менее, обратите внимание, что ссылка на «IValidateObject» в блоге должно быть «IValidatableObject».)

<a id="BM_Dependency_Injection_Improvements"></a>

## <a name="dependency-injection-improvements"></a>Улучшения внедрения зависимостей

ASP.NET MVC 3 реализована Улучшенная поддержка для применения внедрение зависимостей (DI), а также для интеграции с контейнерами внедрения зависимостей и инверсии управления (IOC). Добавлена поддержка внедрения Зависимостей в следующих областях:

- Контроллеры (Регистрация и включение фабрики контроллеров, добавления контроллеров).
- Представления (Регистрация и включение обработчиков представлений, внедрение зависимостей в представления страницы).
- Фильтры действий (поиск и добавление фильтров).
- Связыватели моделей ("Регистрация" и "Вставка").
- Поставщиков проверки модели ("Регистрация" и "Вставка").
- Поставщики метаданных модели ("Регистрация" и "Вставка").
- Поставщики значений ("Регистрация" и "Вставка").

MVC 3 поддерживает [локатор общей службы](https://github.com/unitycontainer/commonservicelocator) библиотеки и любой контейнер внедрения Зависимостей, поддерживающий эту библиотеку `IServiceLocator` интерфейс. Она также поддерживает новый `IDependencyResolver` интерфейс, который позволяет проще интегрировать DI-инфраструктур.

Дополнительные сведения о внедрении Зависимостей в MVC 3 см. следующие ресурсы:

- [Брэд Вилсон ряд записей блога на размещение службы](http://bradwilson.typepad.com/blog/2010/07/service-location-pt1-introduction.html)
- [Заметки о выпуске MVC 3](../whitepapers/mvc3-release-notes.md)

<a id="BM_Other_New_Features"></a>

## <a name="other-new-features"></a>Другие новые функции

### <a name="nuget-integration"></a>Интеграция NuGet

ASP.NET MVC 3 автоматически устанавливает и включает NuGet в процессе его установки. NuGet — это диспетчер бесплатный пакет с открытым кодом, который позволяет легко найти, установить и использовать в проектах библиотек .NET и инструменты. Он работает со всеми типами проектов Visual Studio (включая веб-форм ASP.NET и ASP.NET MVC).

NuGet позволяет разработчикам, занимающихся поддержкой проектов с открытым кодом (например, проекты как Moq, NHibernate, Ninject, StructureMap, NUnit, Windsor, RhinoMocks и Elmah) для упаковки их библиотеки и зарегистрировать их в веб-коллекции. Затем удобно для разработчиков .NET, которые хотят использовать одну из этих библиотек для поиска пакета и установите его в проектах, над которыми они работают.

С помощью обновления средств ASP.NET 3 шаблоны проектов включены JavaScript библиотеки предустановленных пакетов NuGet, так, чтобы они обновляемые с помощью NuGet. Entity Framework Code First также предварительно устанавливается как пакет NuGet.

Дополнительные сведения о NuGet см. в [документации по NuGet](https://docs.microsoft.com/nuget/).

### <a name="partial-page-output-caching"></a>Частичные кэширования выводимых данных

ASP.NET MVC поддерживается кэширования ответов полностраничном начиная с версии 1. MVC 3 также поддерживает частичную визуализацию страницы кэширование выходных данных, позволяющий легко области кэша или фрагменты ответа. Дополнительные сведения о кэшировании см. в разделе **частичное кэширование вывода страниц** раздел [записи блога Скотта Гатри MVC 3 версии-кандидата](https://weblogs.asp.net/scottgu/archive/2010/11/09/announcing-the-asp-net-mvc-3-release-candidate.aspx) и **дочерние действия кэширования вывода** раздел [заметки о выпуске MVC 3](../whitepapers/mvc3-release-notes.md).

### <a name="granular-control-over-request-validation"></a>Детальный контроль над проверка запросов

ASP.NET MVC имеет проверка встроенных запросов, который автоматически обеспечивает защиту от атак путем внедрения кода XSS и HTML. Тем не менее иногда требуется явно отключить проверку запроса, например, если нужно сообщить пользователи блога HTML содержимого (например, в записи блога и содержимого CMS). Теперь вы можете добавить [AllowHtml](https://msdn.microsoft.com/library/system.web.mvc.allowhtmlattribute(v=VS.98).aspx) атрибут модели или просмотра моделей, чтобы отключить проверку запроса на основе каждого свойства во время привязки модели. Дополнительные сведения о проверке запроса см. следующие ресурсы:

- **Ненавязчивый JavaScript и проверки** статьи [записи блога Скотта Гатри MVC 3 версии-кандидата](https://weblogs.asp.net/scottgu/archive/2010/11/09/announcing-the-asp-net-mvc-3-release-candidate.aspx).
- [Заметки о выпуске MVC 3](../whitepapers/mvc3-release-notes.md)

### <a name="extensible-new-project-dialog-box"></a>Расширяемая «новый проект» диалоговое окно

В ASP.NET MVC 3 вы можете добавить шаблоны проектов, обработчиков представлений и платформ проекта для модульных тестов **новый проект** диалоговое окно.

### <a name="template-scaffolding-improvements"></a>Усовершенствования шаблона формирования шаблонов

Определение свойств первичного ключа на моделях и обработка их соответствующим образом, чем в более ранних версиях MVC улучшенным формирования шаблонов ASP.NET MVC 3. (Например, формирования шаблонов теперь убедитесь, что первичный ключ не по шаблону редактируемую форму поля.)

По умолчанию формирует шаблон Create и Edit используют `Html.EditorFor` вспомогательный вместо `Html.TextBoxFor` вспомогательный. Это улучшает поддержку метаданные о модели в виде данных заметки атрибуты при **Добавление представления** диалоговом окне создается представление.

### <a name="new-overloads-for-htmllabelfor-and-htmllabelformodel"></a>Новые перегрузки для «Html.LabelFor» и «Html.LabelForModel»

Были добавлены новые перегрузки метода `LabelFor` и `LabelForModel` вспомогательные методы. Новые перегрузки позволяют указать или переопределить текст метки.

### <a name="sessionless-controller-support"></a>Поддержка sessionless контроллера

В ASP.NET MVC 3, можно указать, какому параметру требуется класс контроллера, использовании состояния сеанса и если да, ли состояние сеанса должно быть чтения и записи или только для чтения. Дополнительные сведения о поддержке sessionless контроллера см. в разделе [заметки о выпуске MVC 3](../whitepapers/mvc3-release-notes.md).

### <a name="new-additionalmetadataattribute-class"></a>Новый класс «AdditionalMetadataAttribute»

Можно использовать [AdditionalMetadata](https://msdn.microsoft.com/library/system.web.mvc.additionalmetadataattribute(v=VS.98).aspx) атрибут для заполнения `ModelMetadata.AdditionalValues` словарь для свойства модели. Например если модель представления имеет свойство, которое следует отображать только для администратора, можно снабдить это свойство, как показано в следующем примере:

[!code-csharp[Main](mvc3/samples/sample4.cs)]

Эти метаданные доступны в любой шаблон отображения или редактора при подготовке к просмотру представление модели продукта. Это можно интерпретировать сведения о метаданных.

### <a name="accountcontroller-improvements"></a>Усовершенствования AccountController

AccountController в шаблоне проекта по Интернету были значительно улучшены.

### <a name="new-intranet-project-template"></a>Новый шаблон проекта интрасети

Шаблон нового проекта интрасеть включено которого включает проверку подлинности Windows и удаляет AccountController.