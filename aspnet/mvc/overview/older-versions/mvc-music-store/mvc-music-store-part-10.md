---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-10
title: Часть 10. окончательные обновления структуры навигации и сайта, заключение | Документация Майкрософт
author: jongalloway
description: В этой серии руководств подробно описаны все шаги, предпринятые для создания примера приложения музыкального хранилища ASP.NET MVC. Часть 10 охватывает Финальные обновления для навигации и S...
ms.author: riande
ms.date: 04/21/2011
ms.assetid: 0c6e4c2f-fcdb-4978-9656-1990c6f15727
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-10
msc.type: authoredcontent
ms.openlocfilehash: f701d1fbabc3e1a97c3750d00e96bf8dba1105cd
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78433614"
---
# <a name="part-10-final-updates-to-navigation-and-site-design-conclusion"></a>Часть 10. окончательные обновления навигации и дизайна сайта, заключение

[Джон Гэллоуэй](https://github.com/jongalloway)

> Музыкальное хранилище MVC — это учебное приложение, в котором представлены и объясняются пошаговые инструкции по использованию ASP.NET MVC и Visual Studio для разработки веб-приложений.  
>   
> Музыкальное хранилище MVC — это упрощенная реализация в магазине, которая продает музыкальные альбомы в сети и реализует базовое администрирование сайта, вход пользователя в систему и функции корзины покупок.  
>   
> В этой серии руководств подробно описаны все шаги, предпринятые для создания примера приложения музыкального хранилища ASP.NET MVC. В части 10 описаны Финальные обновления навигации и дизайна узла, заключение.

Мы выполнили все основные функции нашего сайта, но у нас по-прежнему есть некоторые функции для добавления в навигацию по сайту, домашнюю страницу и страницу обзора магазина.

## <a name="creating-the-shopping-cart-summary-partial-view"></a>Создание частичного представления сводки корзины для покупок

Мы хотим предоставить количество элементов в корзине для покупок пользователя на всем сайте.

![](mvc-music-store-part-10/_static/image1.png)

Это можно легко реализовать, создав частичное представление, которое добавляется к нашему сайту site. master.

Как показано выше, контроллер ShoppingCart включает метод действия Картсуммари, который возвращает частичное представление:

[!code-csharp[Main](mvc-music-store-part-10/samples/sample1.cs)]

Чтобы создать частичное представление Картсуммари, щелкните правой кнопкой мыши папку Views/ShoppingCart и выберите Добавить представление. Назовите представление Картсуммари и установите флажок "создать частичное представление", как показано ниже.

![](mvc-music-store-part-10/_static/image2.png)

Частичное представление Картсуммари — это просто ссылка на представление индекса ShoppingCart, показывающее количество элементов в корзине. Полный код для Картсуммари. cshtml выглядит следующим образом:

[!code-cshtml[Main](mvc-music-store-part-10/samples/sample2.cshtml)]

Можно включить частичное представление на любую страницу сайта, включая главный узел, с помощью метода HTML. RenderAction. RenderAction требует указать имя действия ("Картсуммари") и имя контроллера ("ShoppingCart"), как показано ниже.

[!code-cshtml[Main](mvc-music-store-part-10/samples/sample3.cshtml)]

Перед добавлением этого элемента в макет сайта мы также создадим меню жанр, чтобы мы могли сделать все наши веб-узлы. master Updates в один момент времени.

## <a name="creating-the-genre-menu-partial-view"></a>Создание частичного представления меню жанра

Мы можем сделать так, чтобы наши пользователи могли перемещаться по магазину, добавляя меню жанра, в котором перечислены все жанры, доступные в нашем магазине.

![](mvc-music-store-part-10/_static/image3.png)

Мы выполняйте те же действия, а также создадите частичное представление Женремену, после чего мы можем добавить их в главную страницу. Сначала добавьте следующее действие контроллера Женремену в Стореконтроллер:

[!code-csharp[Main](mvc-music-store-part-10/samples/sample4.cs)]

Это действие возвращает список жанров, которые будут отображаться в частичном представлении, которое будет создано далее.

*Примечание. Мы добавили атрибут [Чилдактиононли] к этому действию контроллера, что означает, что мы хотим, чтобы это действие было использовано только из частичного представления. Этот атрибут предотвратит выполнение действия контроллера, перейдя к/Сторе/женремену. Это не требуется для частичных представлений, но рекомендуется, поскольку мы хотим убедиться, что наши действия контроллера используются, как мы планируем. Мы также возвращаем Партиалвиев, а не View, что позволяет обработчику представлений не использовать макет для этого представления, так как он включается в другие представления.*

Щелкните действие контроллера Женремену правой кнопкой мыши и создайте частичное представление с именем Женремену, которое строго типизировано с помощью класса данных для представления жанра, как показано ниже.

![](mvc-music-store-part-10/_static/image4.png)

Обновите код представления для частичного представления Женремену, чтобы отобразить элементы с помощью неупорядоченного списка, как показано ниже.

[!code-cshtml[Main](mvc-music-store-part-10/samples/sample5.cshtml)]

## <a name="updating-site-layout-to-display-our-partial-views"></a>Обновление макета сайта для отображения наших частичных представлений

Мы можем добавить наши частичные представления в макет узла (/Виевс/Шаред/\_Layout. cshtml), вызвав HTML. RenderAction (). Мы добавим их как в, так и в дополнительной разметке для отображения их, как показано ниже:

[!code-cshtml[Main](mvc-music-store-part-10/samples/sample6.cshtml)]

Теперь, когда мы запускаем приложение, мы увидим жанр в левой области навигации и сводку по корзине вверху.

## <a name="update-to-the-store-browse-page"></a>Обновление страницы обзора магазина

Страница обзора хранилища является функциональной, но она не выглядит очень хорошо. Мы можем обновить страницу, чтобы отобразить альбомы в более качественном макете, обновив код представления (в/Виевс/Сторе/бровсе.кштмл) следующим образом:

[!code-cshtml[Main](mvc-music-store-part-10/samples/sample7.cshtml)]

Здесь мы используем URL-адрес. Action, а не HTML. ActionLink, чтобы мы могли применить к ссылке специальное форматирование, включающее иллюстрацию альбома.

*Примечание. для этих альбомов выводится универсальная Обложка альбома. Эти сведения хранятся в базе данных и редактируются с помощью диспетчера магазинов. Вы можете добавить собственную иллюстрацию.*

Теперь, когда мы перейдем по жанру, мы увидим альбомы, показанные в сетке с иллюстрациями альбома.

![](mvc-music-store-part-10/_static/image5.png)

## <a name="updating-the-home-page-to-show-top-selling-albums"></a>Обновление домашней страницы для отображения лучших продаваемых альбомов

Мы хотим приподняться к нашим лучшим альбомам на домашней странице, чтобы увеличить объем продаж. Мы сделаем некоторые обновления для нашего HomeController, чтобы справиться с этим, а также добавили дополнительные графические изображения.

Во-первых, мы добавим свойство навигации в наш класс «альбом», чтобы EntityFramework знать, что они связаны. Последние несколько строк нашего класса **альбома** теперь должны выглядеть следующим образом:

[!code-csharp[Main](mvc-music-store-part-10/samples/sample8.cs)]

*Примечание. для этого потребуется добавить оператор using для переноса в пространство имен System. Collections. Generic.*

Сначала мы добавим поля Сторедб и Мвкмусиксторе. Models с помощью инструкций, как в других контроллерах. Далее мы добавим следующий метод в HomeController, который запрашивает нашу базу данных для поиска лучших в продаже альбомов в соответствии с OrderDetails.

[!code-csharp[Main](mvc-music-store-part-10/samples/sample9.cs)]

Это частный метод, так как мы не хотим сделать его доступным в качестве действия контроллера. Мы используем его в HomeController для простоты, но при необходимости рекомендуется переместить бизнес-логику в отдельные классы служб.

Теперь мы можем обновить действие контроллера индекса, чтобы запросить пять лучших альбомов и вернуть их в представление.

[!code-csharp[Main](mvc-music-store-part-10/samples/sample10.cs)]

Полный код для обновленного HomeController показан ниже.

[!code-csharp[Main](mvc-music-store-part-10/samples/sample11.cs)]

Наконец, необходимо обновить представление домашнего индекса таким образом, чтобы он мог отобразить список альбомов, обновив тип модели и добавив список альбомов в нижнюю часть. Эта возможность также будет использоваться для добавления заголовка и раздела продвижения на страницу.

[!code-cshtml[Main](mvc-music-store-part-10/samples/sample12.cshtml)]

Теперь, когда мы запустим приложение, мы увидим обновленную домашнюю страницу с помощью самых популярных альбомов и нашего рекламного сообщения.

![](mvc-music-store-part-10/_static/image1.jpg)

## <a name="conclusion"></a>Заключение

Мы увидели, что ASP.NET MVC упрощает создание сложного веб-сайта с доступом к базе данных, членством, AJAX и т. д. очень быстро. Надеюсь, в этом учебнике были предоставлены средства, необходимые для начала создания собственных приложений ASP.NET MVC.

> [!div class="step-by-step"]
> [Назад](mvc-music-store-part-9.md)
