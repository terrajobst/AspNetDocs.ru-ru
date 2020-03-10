---
uid: web-pages/overview/mobile/rendering-aspnet-web-pages-sites-for-mobile-devices
title: Подготовка сайтов веб-страницы ASP.NET (Razor) для мобильных устройств | Документация Майкрософт
author: Rick-Anderson
description: 'В этой статье описывается создание страниц на веб-сайте веб-страницы ASP.NET (Razor), который будет правильно отображаться на мобильных устройствах. Что вы узнаете: как вы...'
ms.author: riande
ms.date: 02/17/2014
ms.assetid: f15ab392-c05e-4269-83bf-7c6d2b8c8ec8
msc.legacyurl: /web-pages/overview/mobile/rendering-aspnet-web-pages-sites-for-mobile-devices
msc.type: authoredcontent
ms.openlocfilehash: c012348d65e48a275cb0e4808fef2a7f31e5fb33
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78454356"
---
# <a name="rendering-aspnet-web-pages-razor-sites-for-mobile-devices"></a>Подготовка сайтов веб-страницы ASP.NET (Razor) для мобильных устройств

от [Tom фитзмаккен](https://github.com/tfitzmac)

> В этой статье описывается создание страниц на веб-сайте веб-страницы ASP.NET (Razor), который будет правильно отображаться на мобильных устройствах.
> 
> Из этого руководства вы узнаете, как выполнять такие задачи:
> 
> - Использование соглашения об именовании для указания того, что страница разработана специально для мобильных устройств.
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>Версии программного обеспечения, используемые в этом руководстве
> 
> 
> - Веб-страницы ASP.NET (Razor) 3
>   
> 
> Этот учебник также работает с веб-страницы ASP.NET 2.

Веб-страницы ASP.NET позволяет создавать пользовательские экраны для отображения содержимого на мобильных или других устройствах.

Самым простым способом создания страницы для конкретного устройства на веб-страницы ASP.NET сайте является использование такого шаблона именования файлов: *filename. Mobile. cshtml*. Можно создать две версии страницы (например, One с именем *MyFile. cshtml* и один с именем *MyFile. Mobile. cshtml*). Во время выполнения, когда мобильное устройство запрашивает *MyFile. cshtml*, ASP.NET визуализирует содержимое из *MyFile. Mobile. cshtml*. В противном случае отображается *MyFile. cshtml* .

В следующем примере показано, как включить отрисовку для мобильных устройств, добавив страницу содержимого на мобильных устройствах. Элемент «страница *. cshtml* » содержит содержимое и боковую панель навигации. Параметр "элемент *. Mobile. cshtml* " содержит то же содержимое, но не имеет боковой панели.

1. На веб-страницы ASP.NET сайте создайте файл с именем "код страницы *. cshtml* " и замените текущее содержимое следующей разметкой.

    [!code-html[Main](rendering-aspnet-web-pages-sites-for-mobile-devices/samples/sample1.html)]
2. Создайте файл с именем " *. Mobile. cshtml* " и замените имеющееся содержимое следующей разметкой. Обратите внимание, что мобильная версия страницы не охватывает раздел навигации для лучшей отрисовки на меньшем экране.

    [!code-html[Main](rendering-aspnet-web-pages-sites-for-mobile-devices/samples/sample2.html)]
3. Запустите браузер для настольных систем и перейдите по адресу "^ *. cshtml*". ![мобилеситес-1](rendering-aspnet-web-pages-sites-for-mobile-devices/_static/image1.png)
4. Запустите браузер для мобильных устройств (или эмулятор мобильного устройства) и перейдите по адресу "^ *. cshtml*". (Обратите внимание, что вы не включаете *. Mobile.* как часть URL-адреса.) Несмотря на то, что запрос имеет значение "No @ *. cshtml*", ASP.NET визуализирует. *Mobile. cshtml*.

    ![мобилеситес-2](rendering-aspnet-web-pages-sites-for-mobile-devices/_static/image2.png)

> [!NOTE]
> Для тестирования страниц мобильных устройств можно использовать симулятор мобильных устройств, работающий на настольном компьютере. Это средство позволяет тестировать веб-страницы так, как они будут выглядеть на мобильных устройствах (то есть обычно с значительно меньшей областью отображения). Одним из примеров симулятора является [надстройка агента пользователя](http://addons.mozilla.org/firefox/addon/user-agent-switcher/) для Mozilla Firefox, которая позволяет эмулировать различные мобильные браузеры из классической версии Firefox.

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a>Дополнительные ресурсы

[Эмулятор Windows Phone](https://msdn.microsoft.com/library/ff402563(v=VS.92).aspx)
