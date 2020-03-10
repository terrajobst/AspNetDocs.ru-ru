---
uid: web-pages/overview/ui-layouts-and-themes/twitter-helper
title: Вспомогательное приложение Twitter с веб-страницы ASP.NET | Документация Майкрософт
author: Rick-Anderson
description: В этом разделе и приложении показано, как добавить вспомогательную функцию Twitter в проект WebMatrix 3. Он содержит вспомогательный код Twitter и показывает, как вызвать вспомогательную функцию...
ms.author: riande
ms.date: 11/26/2018
ms.assetid: c1a1244e-b9c8-42e6-a00b-8456a4ec027c
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/twitter-helper
msc.type: authoredcontent
ms.openlocfilehash: 76e32b7c808467a9a87c70017dac02bdb895e1df
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78518622"
---
# <a name="twitter-helper-with-aspnet-web-pages"></a>Добавление вспомогательного приложения Twitter с помощью веб-страниц ASP.NET

от [Tom фитзмаккен](https://github.com/tfitzmac)

> [!IMPORTANT]
> Вспомогательные методы Twitter устарели. Сведения о новейших средствах взаимодействия Twitter для веб-сайтов см. в [обзоре Twitter для веб-сайтов](https://developer.twitter.com/en/docs/twitter-for-websites/overview).

> В этом разделе и приложении показано, как добавить вспомогательную функцию Twitter в проект WebMatrix 3. Он содержит вспомогательный код Twitter и показывает, как вызывать вспомогательные методы.
> 
> Этот код для файла Twitter. cshtml был разработан **Тиан Pan** Microsoft.
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>Версии программного обеспечения, используемые в этом руководстве
> 
> 
> - Веб-страницы ASP.NET (Razor) 3
>   
> 
> Этот учебник также работает с веб-страницы ASP.NET 2.

## <a name="introduction"></a>Введение

В этом разделе показано, как добавить в приложение вспомогательную функцию Twitter и использовать синтаксис Razor для вызова вспомогательных методов. Помощник Twitter упрощает включение в приложение кнопок и мини-приложений Twitter. Чтобы использовать мини-приложение Twitter, например временную шкалу пользователя или результаты поиска для хэш-тега, необходимо сначала создать мини-приложение [в Twitter](https://twitter.com/settings/widgets). После создания мини-приложения вы получите его идентификатор. Идентификатор мини-приложения передается в качестве параметра при вызове вспомогательных методов, которые отображают мини-приложение.

Этот раздел написан для версии 1,1 API Twitter. Непосредственно добавив в проект вспомогательный код Twitter, вы можете обновить вспомогательный код при изменении API Twitter.

Дополнительные сведения об установке WebMatrix см. в разделе [Введение в веб-страницы ASP.NET 2-Начало работы](../getting-started/introducing-aspnet-web-pages-2/getting-started.md).

## <a name="add-twitter-helper-to-your-project"></a>Добавление вспомогательного метода Twitter в проект

Чтобы добавить вспомогательный модуль Twitter, сначала добавьте папку с именем **App\_Code** в проект. Затем создайте файл с именем **Twitter. cshtml**.

![Папка App_Code](twitter-helper/_static/image1.png)

Замените код по умолчанию в Twitter. cshtml следующим кодом.

[!code-cshtml[Main](twitter-helper/samples/sample1.cshtml)]

## <a name="call-twitter-methods-from-your-web-pages"></a>Вызов методов Twitter с веб-страниц

В следующем примере показано, как использовать вспомогательные методы Twitter на странице в проекте. В проекте потребуется заменить значения параметров значениями, относящимися к вашим потребностям. Вы можете использовать предоставленные идентификаторы мини-приложений, чтобы узнать, как работают методы, но вам потребуется создать собственные мини-приложения для проекта.

Не все указанные ниже параметры являются обязательными. Необязательные параметры используются для настройки отображения кнопки или мини-приложения. Например, для кнопки "Далее" требуется только имя пользователя, но в примере показано, как включить число подписчиков и указать размер кнопки и языка.

[!code-html[Main](twitter-helper/samples/sample2.html)]

## <a name="see-the-results"></a>Просмотр результатов

Приведенный выше код создает следующие кнопки и мини-приложения. Эти кнопки и мини-приложения являются полнофункциональными, а не снимками экрана. Кнопка Далее отображается на испанском языке, так как для параметра Language задано значение **ES**.

### <a name="follow-button"></a>Кнопка "Далее"

[Следовать @aspnet)](https://twitter.com/aspnet)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + '://platform.twitter.com/widgets.js'; fjs.parentNode.insertBefore(js, fjs); } }(document, 'script', 'twitter-wjs');</script>`

### <a name="tweet-button"></a>Кнопка твита

[Твит](https://twitter.com/share)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + '://platform.twitter.com/widgets.js'; fjs.parentNode.insertBefore(js, fjs); } }(document, 'script', 'twitter-wjs');</script>`

### <a name="user-timeline-profile"></a>Временная шкала пользователя (профиль)

[Твиты по @aspnet](https://twitter.com/aspnet)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + "://platform.twitter.com/widgets.js"; fjs.parentNode.insertBefore(js, fjs); } }(document, "script", "twitter-wjs");</script>`

### <a name="favorites"></a>Избранное

[Избранные твиты по @Microsoft](https://twitter.com/Microsoft/favorites)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + "://platform.twitter.com/widgets.js"; fjs.parentNode.insertBefore(js, fjs); } }(document, "script", "twitter-wjs");</script>`

### <a name="list"></a>Список

[Твиты из @Microsoft/MS\_\_](https://twitter.com/microsoft/ms-consumer-brands/)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + "://platform.twitter.com/widgets.js"; fjs.parentNode.insertBefore(js, fjs); } }(document, "script", "twitter-wjs");</script>`

### <a name="search"></a>Поиск

[Твиты о &quot;#asp&quot;.net](https://twitter.com/search?q=%23asp.net)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + "://platform.twitter.com/widgets.js"; fjs.parentNode.insertBefore(js, fjs); } }(document, "script", "twitter-wjs");</script>`
