---
uid: web-api/overview/security/preventing-cross-site-request-forgery-csrf-attacks
title: Предупреждения атак с подделкой межсайтовых запросов в ASP.NET MVC
author: MikeWasson
description: Описание атаки подделкой межсайтовых запросов и как реализовать меры anti-CSRF в ASP.NET Web MVC.
ms.author: riande
ms.date: 12/12/2012
ms.assetid: 81d46f14-8f48-4d8c-830d-cc8d594dc11b
msc.legacyurl: /web-api/overview/security/preventing-cross-site-request-forgery-csrf-attacks
msc.type: authoredcontent
ms.openlocfilehash: c88975d1c205e9d0733bfb4c710b92bc8fdaaa7a
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57042371"
---
<a name="preventing-cross-site-request-forgery-csrf-attacks-in-aspnet-mvc-application"></a>Предупреждения атак с подделкой межсайтовых запросов в приложении ASP.NET MVC
====================
по [Майк Уоссон](https://github.com/MikeWasson)

Подделки межсайтовых запросов (CSRF) — это атака, при которой вредоносный сайт отправляет запрос на уязвимом сайте, где пользователь вошел в

Вот пример атаки CSRF:

1. Когда пользователь входит в `www.example.com` проверки подлинности с помощью форм.
2. Сервер проверяет подлинность пользователя. Ответ от сервера включает файл cookie проверки подлинности.
3. Не выходя из пользователь посещает вредоносных веб-сайта. Этот вредоносный сайт содержит следующий HTML-формы: 

    [!code-html[Main](preventing-cross-site-request-forgery-csrf-attacks/samples/sample1.html)]

    Обратите внимание, что отправляет уязвимом сайте, не на сайте вредоносных действий формы. Это часть CSRF «cross-site».
4. Пользователь нажимает кнопку «Отправить». Браузер включает в себя файл cookie проверки подлинности с запросом.
5. Этот запрос выполняется на сервере с контекстом проверки подлинности пользователя и могут выполнять любые операции, прошедший проверку пользователь может сделать.

Несмотря на то, что в этом примере требует от пользователя, нажмите кнопку «формы», страницу вредоносных может так же, как легко запускать сценарий, который автоматически отправляет форму. Кроме того с помощью протокола SSL не может помешать атаки CSRF, так как вредоносный сайт может отправить запрос « https://».

Как правило атак CSRF — для веб-сайтов, использующих файлы cookie для проверки подлинности, потому что браузеры отправляют все необходимые файлы cookie веб-узлу. Тем не менее атаки CSRF не ограничены использованием файлы cookie. Например Basic и дайджест-проверки подлинности также уязвимы. После входа пользователя в систему с помощью обычной или дайджест-проверки подлинности. браузер автоматически отправляет учетные данные до завершения сеанса.

## <a name="anti-forgery-tokens"></a>Маркеры защиты от подделки

Для предотвращения атак CSRF, ASP.NET MVC использует маркеры защиты от подделки, также называемый *запрашивать маркеры проверки*.

1. Клиент запрашивает страницу HTML, содержащий форму.
2. Сервер включает два маркера в ответе. Один маркер отправляется в виде файла cookie. Другой помещается в скрытом поле формы. Токены генерируются случайным образом, чтобы злоумышленник не может подобрать значения.
3. Когда клиент отправляет форму, оно должно отправлять маркеры на сервер. Клиент отправляет маркер cookie в виде файла cookie, и он отправляет маркер формы внутри формы данных. (Веб-клиент делает это автоматически при отправке формы пользователем.)
4. Если запрос не содержит маркеры, сервер запрещает запрос.

Ниже приведен пример HTML-форму с маркером скрытой форме:

[!code-html[Main](preventing-cross-site-request-forgery-csrf-attacks/samples/sample2.html)]

Маркеры защиты от подделки работать, поскольку вредоносной страницы не удается считать маркеры пользователя, из-за политики одного источника. ([Политики одного источника](http://www.w3.org/Security/wiki/Same_Origin_Policy) предотвратить документов, размещенные на двух разных сайтах, доступ к содержимому друг друга. Поэтому в предыдущем примере, вредоносной страницы может отправлять запросы на example.com, но его не удается прочитать ответ.)

Чтобы избежать атак CSRF, использование маркеров защиты от подделки с любой протокол проверки подлинности, где браузер автоматически отправляет учетные данные после входа пользователя. Это включает в себя протоколы проверки подлинности на основе файлов cookie, такие как проверка подлинности форм, а также протоколов, таких как Basic и дайджест-проверки подлинности.

Для любых nonsafe методов (POST, PUT, DELETE) должна требовать маркеров защиты от подделки. Кроме того убедитесь, что безопасные методы (GET, HEAD) не имеют никаких побочных эффектов. Кроме того при включении поддержки между доменами, такие как CORS и JSONP, затем даже безопасные методы, такие как GET являются потенциально уязвимым к CSRF-атакам, что позволяет злоумышленнику читать потенциально конфиденциальных данных.

## <a name="anti-forgery-tokens-in-aspnet-mvc"></a>Маркеры защиты от подделки в ASP.NET MVC

Чтобы добавить маркеры защиты от подделки на страницу Razor, используйте **HtmlHelper.AntiForgeryToken** вспомогательный метод:

[!code-cshtml[Main](preventing-cross-site-request-forgery-csrf-attacks/samples/sample3.cshtml)]

Этот метод добавляет скрытое поле формы, а также задает маркер cookie.

## <a name="anti-csrf-and-ajax"></a>Anti-CSRF и AJAX

Маркера формы может стать проблемой для запросов AJAX, так как запрос AJAX может отправлять данные JSON, не данные HTML-формы. Одно из решений — отправлять токены в HTTP-заголовка. Следующий код использует синтаксис Razor для создания маркеров и затем добавляет их AJAX-запросом. Токены созданные на сервере путем вызова **AntiForgery.GetTokens**.

[!code-html[Main](preventing-cross-site-request-forgery-csrf-attacks/samples/sample4.html)]

При обработке запроса Извлеките токены из заголовка запроса. Затем вызовите **AntiForgery.Validate** метод для проверки маркеров. **Validate** метод вызывает исключение, если токены не допускаются.

[!code-csharp[Main](preventing-cross-site-request-forgery-csrf-attacks/samples/sample5.cs)]