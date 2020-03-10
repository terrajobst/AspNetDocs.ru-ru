---
uid: web-api/overview/advanced/sending-html-form-data-part-1
title: 'Отправка данных HTML-формы в веб-API ASP.NET: Form-UrlEncoded Data-ASP.NET 4. x'
author: MikeWasson
description: В этой статье показано, как отправить данные Form-UrlEncoded в контроллер веб-API с помощью ASP.NET 4. x.
ms.author: riande
ms.date: 06/15/2012
ms.custom: seoapril2019
ms.assetid: 585351c4-809a-4bf5-bcbe-35d624f565fe
msc.legacyurl: /web-api/overview/advanced/sending-html-form-data-part-1
msc.type: authoredcontent
ms.openlocfilehash: 7243069dbd8051b1374ed6e0112c273b8fe26f61
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78449244"
---
# <a name="sending-html-form-data-in-aspnet-web-api-form-urlencoded-data"></a>Отправка данных HTML-формы в веб-API ASP.NET: данные Form-UrlEncoded

по [Майк Уоссон](https://github.com/MikeWasson)

## <a name="part-1-form-urlencoded-data"></a>Часть 1. форма-UrlEncoded данных

В этой статье показано, как опубликовать данные формы-UrlEncoded в контроллере веб-API.

- [Общие сведения о HTML-формах](#overview_of_html_forms)
- [Отправка сложных типов](#sending_complex_types)
- [Отправка данных формы через AJAX](#sending_form_data_via_ajax)
- [Отправка простых типов](#sending_simple_types)

> [!NOTE]
> [Скачайте завершенный проект](https://code.msdn.microsoft.com/ASPNET-Web-API-Sending-a6f9d007).

<a id="overview_of_html_forms"></a>
## <a name="overview-of-html-forms"></a>Общие сведения о HTML-формах

Для отправки данных на сервер в HTML-формах используется либо GET, либо POST. Атрибут **method** элемента **Form** предоставляет метод HTTP:

[!code-html[Main](sending-html-form-data-part-1/samples/sample1.html)]

Метод по умолчанию — GET. Если форма использует GET, данные формы кодируются в универсальном коде ресурса (URI) в виде строки запроса. Если форма использует POST, данные формы помещаются в текст запроса. Для отправленных данных атрибут **енктипе** задает формат текста запроса:

| енктипе | Description |
| --- | --- |
| application/x-www-form-urlencoded | Данные формы кодируются как пары "имя-значение", аналогично строке запроса URI. Это формат по умолчанию для POST. |
| multipart/form-data | Данные формы кодируются как составное сообщение MIME. Используйте этот формат при отправке файла на сервер. |

В первой части этой статьи рассматривается формат x-www-Form-UrlEncoded. [Часть 2](sending-html-form-data-part-2.md) описывает составной MIME.

<a id="sending_complex_types"></a>
## <a name="sending-complex-types"></a>Отправка сложных типов

Как правило, будет отправлен сложный тип, состоящий из значений, взятых из нескольких элементов управления формы. Рассмотрим следующую модель, представляющую обновление состояния:

[!code-csharp[Main](sending-html-form-data-part-1/samples/sample2.cs)]

Ниже приведен контроллер веб-API, принимающий объект `Update` через POST.

[!code-csharp[Main](sending-html-form-data-part-1/samples/sample3.cs)]

> [!NOTE]
> Этот контроллер использует [маршрутизацию на основе действий](../web-api-routing-and-actions/routing-in-aspnet-web-api.md#routing_by_action_name), поэтому шаблон маршрута &quot;API/{Controller}/{Action}/{id}&quot;. Клиент будет отправлять данные в &quot;/АПИ/упдатес/комплекс&quot;.

Теперь напишем HTML-форму, чтобы пользователи могли отправить обновление состояния.

[!code-html[Main](sending-html-form-data-part-1/samples/sample4.html)]

Обратите внимание, что атрибут **Action** в форме является универсальным кодом ресурса (URI) действия контроллера. Ниже приведена форма с некоторыми значениями, введенными в:

![](sending-html-form-data-part-1/_static/image1.png)

Когда пользователь нажимает кнопку Отправить, браузер отправляет HTTP-запрос, аналогичный следующему:

[!code-console[Main](sending-html-form-data-part-1/samples/sample5.cmd)]

Обратите внимание, что текст запроса содержит данные формы, отформатированные как пары "имя-значение". Веб-API автоматически преобразует пары "имя-значение" в экземпляр класса `Update`.

<a id="sending_form_data_via_ajax"></a>
## <a name="sending-form-data-via-ajax"></a>Отправка данных формы через AJAX

Когда пользователь отправляет форму, браузер переходит от текущей страницы и отображает текст ответного сообщения. Это нормально, когда ответ является HTML-страницей. Однако в веб-API текст ответа обычно либо пуст, либо содержит структурированные данные, такие как JSON. В этом случае имеет смысл отправить данные формы с помощью запроса AJAX, чтобы страница могла обработать ответ.

В следующем коде показано, как отправлять данные формы с помощью jQuery.

[!code-html[Main](sending-html-form-data-part-1/samples/sample6.html)]

Функция **отправки** jQuery заменяет действие формы новой функцией. Это переопределяет поведение по умолчанию кнопки Отправить. Функция **Serialize** сериализует данные формы в пары "имя-значение". Чтобы отправить данные формы на сервер, вызовите `$.post()`.

По завершении запроса обработчик `.success()` или `.error()` отображает соответствующее сообщение пользователю.

![](sending-html-form-data-part-1/_static/image2.png)

<a id="sending_simple_types"></a>
## <a name="sending-simple-types"></a>Отправка простых типов

В предыдущих разделах мы отправили сложный тип, который веб-API десериализует в экземпляр класса Model. Можно также отправить простые типы, например строку.

> [!NOTE]
> Перед отправкой простого типа рекомендуется обернуть значение в сложный тип. Это дает преимущества проверки модели на стороне сервера и упрощает расширение модели при необходимости.

Основные шаги для отправки простого типа одинаковы, но есть два незначительных различия. Сначала в контроллере необходимо снабдить имя параметра атрибутом **FromBody** .

[!code-csharp[Main](sending-html-form-data-part-1/samples/sample7.cs?highlight=3)]

По умолчанию веб-API пытается получить простые типы из универсального кода ресурса (URI) запроса. Атрибут **FromBody** сообщает веб-API о необходимости считывания значения из текста запроса.

> [!NOTE]
> Веб-API считывает текст ответа не более одного раза, поэтому в тексте запроса может быть только один параметр действия. Если необходимо получить несколько значений из текста запроса, определите сложный тип.

Во вторых, клиенту необходимо отправить значение в следующем формате:

[!code-xml[Main](sending-html-form-data-part-1/samples/sample8.xml)]

В частности, часть имени пары «имя-значение» для простого типа должна быть пустой. Не все браузеры поддерживают это для HTML-форм, но этот формат создается в скрипте следующим образом:

[!code-javascript[Main](sending-html-form-data-part-1/samples/sample9.js)]

Ниже приведен пример формы.

[!code-html[Main](sending-html-form-data-part-1/samples/sample10.html)]

И вот сценарий для отправки значения формы. Единственное отличие от предыдущего скрипта — это аргумент, передаваемый в функцию **POST** .

[!code-javascript[Main](sending-html-form-data-part-1/samples/sample11.js?highlight=2)]

Один и тот же подход можно использовать для отправки массива простых типов:

[!code-javascript[Main](sending-html-form-data-part-1/samples/sample12.js)]

## <a name="additional-resources"></a>Дополнительные ресурсы

[Часть 2. Передача файлов и составной MIME](sending-html-form-data-part-2.md)
