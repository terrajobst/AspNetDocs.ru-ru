---
uid: mvc/overview/older-versions-1/controllers-and-routing/adding-dynamic-content-to-a-cached-page-cs
title: Добавление динамического содержимого в кэшированную страницу (C#) | Документация Майкрософт
author: microsoft
description: Узнайте, как смешивать динамическое и кэшированное содержимое на одной странице. Подстановка после кэширования позволяет отображать динамическое содержимое, например заголовки объявлений o...
ms.author: riande
ms.date: 01/27/2009
ms.assetid: 2ddd4407-d143-4a94-877c-21771bfb97a6
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/adding-dynamic-content-to-a-cached-page-cs
msc.type: authoredcontent
ms.openlocfilehash: be43712d3dd5235117558e991d9dd71aa30ec470
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78486942"
---
# <a name="adding-dynamic-content-to-a-cached-page-c"></a>Добавление динамического содержимого на кэшированные страницы (C#)

по [Майкрософт](https://github.com/microsoft)

> Узнайте, как смешивать динамическое и кэшированное содержимое на одной странице. Подстановка после кэширования позволяет отображать динамическое содержимое, например баннеры или Новости, на странице, для которой кэшированы выходные данные.

Используя преимущества кэширования выходных данных, можно значительно повысить производительность ASP.NET приложения MVC. Вместо повторного создания страницы каждый раз, когда запрашивается страница, эту страницу можно создать один раз и кэшировать в памяти для нескольких пользователей.

Но существует проблема. Что делать, если требуется отображать динамическое содержимое на странице? Например, представьте, что вы хотите отобразить баннер на странице. Вы не хотите, чтобы объявление баннера было кэшировано, чтобы каждый пользователь видел одно и то же объявление. Это не так.

К счастью, существует простое решение. Можно воспользоваться возможностями платформы ASP.NET, именуемой *подстановкой после кэширования*. Подстановка после кэширования позволяет заменять динамическое содержимое на странице, которая была кэширована в памяти.

Обычно при выходе из кэша страницы с помощью атрибута [OutputCache] страница кэшируется как на сервере, так и на клиенте (веб-браузер). При использовании подстановки после кэширования страница кэшируется только на сервере.

#### <a name="using-post-cache-substitution"></a>Использование подстановки после кэширования

Использование подстановки после кэширования требует выполнения двух шагов. Во-первых, необходимо определить метод, который возвращает строку, представляющую динамическое содержимое, которое необходимо отобразить на кэшированной странице. Затем вызовите метод HttpResponse. Вритесубститутион (), чтобы внедрить динамическое содержимое на страницу.

Представьте, например, что требуется случайное отображение различных элементов новостей в кэшированной странице. Класс в листинге 1 предоставляет один метод с именем Рендерневс (), который случайным образом возвращает один элемент новостей из списка из трех элементов новостей.

**Листинг 1 — Моделс\невс.КС**

[!code-csharp[Main](adding-dynamic-content-to-a-cached-page-cs/samples/sample1.cs)]

Чтобы воспользоваться преимуществами подстановки после кэширования, вызовите метод HttpResponse. Вритесубститутион (). Метод Вритесубститутион () настраивает код для замены области кэшированной страницы динамическим содержимым. Метод Вритесубститутион () используется для отображения элемента случайных новостей в представлении в листинге 2.

**Листинг 2 — Виевс\хоме\индекс.аспкс**

[!code-aspx[Main](adding-dynamic-content-to-a-cached-page-cs/samples/sample2.aspx)]

Метод Рендерневс передается методу Вритесубститутион (). Обратите внимание, что метод Рендерневс не вызывается (скобки отсутствуют). Вместо этого ссылка на метод передается в Вритесубститутион ().

Представление индекса кэшируется. Представление возвращается контроллером в листинге 3. Обратите внимание, что действие index () дополнено атрибутом [OutputCache], который приводит к кэшированию представления индекса в течение 60 секунд.

**Листинг 3 — Controllers\HomeController.cs**

[!code-csharp[Main](adding-dynamic-content-to-a-cached-page-cs/samples/sample3.cs)]

Несмотря на то, что представление индекса кэшируется, при запросе страницы индекса отображаются различные элементы случайных новостей. При запросе страницы индекса время, отображаемое на странице, не изменяется в течение 60 секунд (см. рис. 1). Тот факт, что время не меняется, подтверждает, что страница кэшируется. Однако содержимое, введенное методом Вритесубститутион () — Случайная новость — изменяется с каждым запросом.

**Рис. 1. внедрение элементов динамических новостей в кэшированную страницу**

![clip_image002](adding-dynamic-content-to-a-cached-page-cs/_static/image1.jpg)

#### <a name="using-post-cache-substitution-in-helper-methods"></a>Использование подстановки после кэширования в вспомогательных методах

Более простым способом использования подстановки после кэширования является инкапсуляция вызова метода Вритесубститутион () в пользовательском вспомогательном методе. Этот подход проиллюстрирован вспомогательным методом в листинге 4.

**Листинг 4 — AdHelper.cs**

[!code-csharp[Main](adding-dynamic-content-to-a-cached-page-cs/samples/sample4.cs)]

В листинге 4 содержится статический класс, предоставляющий два метода: Рендербаннер () и Рендербаннеринтернал (). Метод Рендербаннер () представляет фактический вспомогательный метод. Этот метод расширяет стандартный класс ASP.NET MVC HtmlHelper, чтобы можно было вызывать HTML. Рендербаннер () в представлении точно так же, как любой другой вспомогательный метод.

Метод Рендербаннер () вызывает метод HttpResponse. Вритесубститутион (), передающий метод Рендербаннеринтернал () методу Вритесубститутион ().

Метод Рендербаннеринтернал () является закрытым методом. Этот метод не будет представлен как вспомогательный метод. Метод Рендербаннеринтернал () случайным образом возвращает одно изображение баннерного объявления из списка трех изображений баннеров.

Измененное представление индекса в листинге 5 показывает, как можно использовать вспомогательный метод Рендербаннер (). Обратите внимание, что в верхней части представления включена дополнительная директива &lt;% @ Import%&gt; для импорта пространства имен MvcApplication1. Вспомогательныеs. Если не импортировать это пространство имен, метод Рендербаннер () не будет отображаться как метод в свойстве HTML.

**Листинг 5 – Виевс\хоме\индекс.аспкс (с методом Рендербаннер ())**

[!code-aspx[Main](adding-dynamic-content-to-a-cached-page-cs/samples/sample5.aspx)]

Когда вы запрашиваете страницу, отображенную представлением в листинге 5, при каждом запросе отображается другое баннерное объявление (см. рис. 2). Страница кэшируется, но объявление баннера динамически вставляется вспомогательным методом Рендербаннер ().

**Рис. 2. представление индекса, отображающее случайное объявление баннера**

![clip_image004](adding-dynamic-content-to-a-cached-page-cs/_static/image2.jpg)

#### <a name="summary"></a>Сводка

В этом руководстве объясняется, как можно динамически обновлять содержимое в кэшированной странице. Вы узнали, как использовать метод HttpResponse. Вритесубститутион (), чтобы включить динамическое содержимое для вставки в кэшированную страницу. Вы также узнали, как инкапсулировать вызов метода Вритесубститутион () в вспомогательном методе HTML.

Воспользуйтесь преимуществами кэширования, когда это возможно. это может оказать значительное влияние на производительность веб-приложений. Как описано в этом руководстве, можно воспользоваться преимуществами кэширования, даже если требуется отобразить на страницах динамическое содержимое.

> [!div class="step-by-step"]
> [Назад](improving-performance-with-output-caching-cs.md)
> [Вперед](creating-a-controller-cs.md)
