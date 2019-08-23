---
uid: overview
title: Обзор ASP.NET | Документация Майкрософт
author: rick-anderson
description: Общие сведения о ASP.NET, бесплатной платформе для создания веб-сайтов, приложений и веб-API.
ms.assetid: 3a309468-f1ca-4e51-b9c3-536af79d7a8b
ms.author: riande
ms.date: 08/10/2019
msc.legacyurl: ''
msc.type: content
ms.openlocfilehash: 9a6d08849f09c9d7a779df64f70e8770d2af3c87
ms.sourcegitcommit: b67ffd5b2c5cff01ec4c8eb12a21f693f2e11887
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/23/2019
ms.locfileid: "69995287"
---
# <a name="aspnet-overview"></a>Обзор ASP.NET

ASP.NET — бесплатная интернет-платформа для создания замечательных веб-сайтов и веб-приложений с помощью HTML, CSS и JavaScript. Также можно создавать веб-API и использовать технологии реального времени, такие как веб-сокеты.

[ASP.NET Core](https://docs.microsoft.com/aspnet/core/) является альтернативой ASP.NET.  Смотрите [рекомендации по выбору между ASP.NET и ASP.NET Core](https://docs.microsoft.com/aspnet/core/choose-aspnet-framework).

## <a name="get-started"></a>Начало работы

Установите [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) Community Edition — бесплатную интегрированную среду разработки для ASP.NET в Windows.

## <a name="websites-and-web-applications"></a>Сайты и веб-приложения

 ASP.NET предлагает три платформы для создания веб-приложений: Веб-формы, ASP.NET MVC и веб-страницы ASP.NET. Все три платформы стабильны и полноценны: замечательные веб-приложения можно создать с помощью любой из них. Независимо от того, какую платформу выберете, вы везде получите все преимущества и возможности ASP.NET.

Каждая платформа предназначена для определенного стиля разработки. Ваш выбор зависит от сочетания навыков программирования (знаний, опыта разработки), типа создаваемого приложения и удобного вам подхода к разработке.

Ниже приведен обзор каждой из платформ и некоторые идеи о выборе между ними. Если предпочитаете видео с введением, смотрите [Making Websites with ASP.NET (Создание веб-сайтов с ASP.NET)](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/Making-Websites-with-ASPNET) и [What is Web Tools? (Возможности веб-инструментов)](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/what-is-web-tools)

|   | Если у вас есть опыт работы в | Стиль разработки | Требуем |
|-----------|----------------------|-----------------------------------------------------|----------------|
| Веб-формы | Win Forms, WPF, .NET | Быстрая разработка с помощью широких возможностей библиотеки элементов управления, которые инкапсулируют разметку HTML | RAD среднего уровня, продвинутый уровень |
| MVC       | Ruby on Rails, .NET  | Полный контроль над разметкой HTML, код и разметка разделены, упрощенное написание тестов. Лучший выбор для мобильных устройств и одностраничных приложений (SPA). | Средний и продвинутый уровень |
| Веб-страницы  | Классический ASP, PHP     | Разметка HTML и код вместе в одном файле | Новый, средний уровень |

### <a name="web-forms"></a>Веб-формы

С веб-формами ASP.NET можно создавать динамические веб-сайты, используя знакомую модель перетаскивания, управляемую событиями. Область конструирования и сотни элементов управления и компонентов позволяют быстро создавать комплексные сайты с эффективным пользовательским интерфейсом и доступом к данным.

[Дополнительные сведения о веб-формах](web-forms/index.md)

### <a name="mvc"></a>MVC

ASP.NET MVC предлагает эффективный, основанный на шаблонах способ создания динамических веб-сайтов, который позволяет четко разделять проблемы и дает полный контроль над разметкой для увлекательных и гибких разработок. ASP.NET MVC содержит множество функций, позволяющих вести быструю TDD-совместимую разработку для создания сложных приложений, использующих новейшие веб-стандарты.

[Дополнительные сведения о MVC](mvc/index.md)

### <a name="aspnet-web-pages"></a>Веб-страницы ASP.NET

Веб-страницы ASP.NET и синтаксис Razor обеспечивают быстрый, понятный и простой способ объединения серверного кода с HTML для создания динамического веб-содержимого. Подключайтесь к базам данных, добавляйте видео, ссылки на сайты социальных сетей и множество других дополнительных функций, чтобы создавать прекрасные сайты, которые соответствуют новейшим веб-стандартам.

[Дополнительные сведения о веб-страницах](web-pages/index.md)

### <a name="notes-about-web-forms-mvc-and-web-pages"></a>Примечания о веб-формах, MVC и веб-страницах

Все три платформы ASP.NET основаны на платформе .NET Framework и используют основные функциональные возможности .NET и ASP.NET. Например, все три платформы предоставляют модель безопасности аутентификации, основанную на членстве, а также все три располагают одинаковыми возможностями для управления запросами, обработки сеансов и всех других основных функций ASP.NET.

Кроме того, эти три платформы не полностью независимы друг от друга и выбор одной из них не препятствует использованию другой. Так как платформы могут сосуществовать в одном и том же веб-приложении, некоторые компоненты приложений, написанные с помощью разных платформ, встречаются нечасто. Например, клиентские части приложения могут быть разработаны в MVC для оптимизации разметки, тогда как доступ к данным и административные части разрабатываются в веб-формах для использования преимуществ элементов управления данными и простого доступа к данным.

## <a name="web-apis"></a>Веб-API

Веб-API ASP.NET — это платформа, которая позволяет легко создавать HTTP-службы для широкого диапазона клиентов, включая браузеры и мобильные устройства. ASP.NET Web API - это идеальная платформа для сборки REST-приложений на базе .NET Framework.

[Дополнительные сведения о веб-API](web-api/index.md)

<!-- Put first under Web API TOC:  Watch video (9 minutes) https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/services-and-aspnet -->

## <a name="real-time-technologies"></a>Технологии в реальном времени

ASP.NET SignalR — это новая библиотека для разработчиков ASP.NET, которая упрощает разработку веб-функций в режиме реального времени. SignalR обеспечивает двунаправленную связь между сервером и клиентом. Серверы могут мгновенно отправлять содержимое подключенным клиентам по мере доступности. SignalR поддерживает веб-сокеты и обращается к другим совместимым методам для старых браузеров. SignalR включает API для управления подключениями (например, события подключения и отключения), группирования соединений и авторизации.

[Дополнительные сведения о SignalR](signalr/index.md)

<!-- Put first under SignalR TOC:  Watch video (6 minutes) https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/signalr-and-the-real-time-web -->

## <a name="mobile-apps-and-sites"></a>Мобильные приложения и сайты

ASP.NET может работать с собственными мобильными приложениями с помощью серверной части веб-API, а также мобильных веб-сайтов, использующих такие платформы разработки, как начальная загрузка Twitter. При создании собственного мобильного приложения можно легко создать веб-API на основе JSON для управления доступом к данным, проверкой подлинности и Push-уведомлениями для приложения. Если вы создаете реагирующий мобильный сайт, вы можете использовать любую платформу CSS или открытую систему сетки или выбрать мощную мобильную систему, например jQuery Mobile или Sencha, а также замечательные мобильные приложения с PhoneGap.

[Дополнительные сведения о разработке мобильных приложений и сайтов](mobile/index.md)

<!-- Put first under mobile TOC:  Watch video (11 minutes) https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/aspnet-and-mobile -->

## <a name="single-page-applications"></a>Одностраничные приложения

Одностраничные приложения ASP.NET (SPA) позволяют создавать приложения, включающие значительное взаимодействие на стороне клиента, с использованием HTML 5, CSS 3 и JavaScript. Visual Studio включает шаблон для создания одностраничных приложений с помощью knockout.js и веб-API ASP.NET. Помимо встроенного шаблона SPA-шаблоны, созданные сообществом разработчиков, также доступны для загрузки.

[Дополнительные сведения о разработке одностраничных приложений](single-page-application/index.md)

## <a name="webhooks"></a>WebHooks

Веб-перехватчик — это упрощенный HTTP-шаблон, обеспечивающий простую модель подписки для связи друг с другом веб-API и SaaS-служб. Когда в службе происходит событие, зарегистрированным подписчикам отправляется уведомление в форме POST HTTP-запроса. Запрос POST содержит сведения о событии, благодаря чему получатель может выполнить соответствующие действия.

Веб-перехватчики используются в большом количестве служб, включая Dropbox, GitHub, Instagram, MailChimp, PayPal, Slack, Trello и многих других. Например, веб-перехватчик может указывать, что файл был изменен в Dropbox, изменение кода зафиксировано в GitHub, платеж был инициализирован в PayPal или была создана карточка в Trello.

[Дополнительные сведения о веб-перехватчиках](webhooks/index.md)

<!--
Create Deployment TOC based on https://www.asp.net/aspnet/overview/deployment
Copy deployment content map to MVC, WebForms, Web Pages, Web API sections.
Copy Web Deployment in Enterprise from WebForms to MVC
Move under ASP.NET Best practices
    What not to do in ASP.NET, and what to do instead https://review.docs.microsoft.cus/aspnet/aspnet/overview/web-development-best-practices/what-not-to-do-in-aspnet-and-what-to-do-instead
    Async and await https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/async-and-await
    Building Real World Cloud Apps with Azure https://review.docs.microsoft.com/aspnet/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/introduction
    Hands on Lab: Maintainable Azure Websites: Managing Change and Scale https://review.docs.microsoft.com/aspnet/aspnet/overview/developing-apps-with-windows-azure/maintainable-azure-websites-managing-change-and-scale

-->
