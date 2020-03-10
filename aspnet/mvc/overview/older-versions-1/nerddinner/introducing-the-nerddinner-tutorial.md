---
uid: mvc/overview/older-versions-1/nerddinner/introducing-the-nerddinner-tutorial
title: Знакомство с руководством по NerdDinner | Документация Майкрософт
author: shanselman
description: Лучшим способом изучения новой платформы является создание чего-то с ней. В этом руководстве описано, как создать небольшое, но полное приложение, использующее ASP.NE...
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 397522d5-0402-4b94-b810-a2fb564f869d
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/introducing-the-nerddinner-tutorial
msc.type: authoredcontent
ms.openlocfilehash: 154cfe6694cf723c0a1f8e33bfdb42c97594518f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78468936"
---
# <a name="introducing-the-nerddinner-tutorial"></a>Общие сведения об учебнике по NerdDinner

по [Скотт Hanselman](https://github.com/shanselman)

[Скачать в формате PDF](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> Лучшим способом изучения новой платформы является создание чего-то с ней. В этом руководстве описано, как создать небольшое, но полное приложение, использующее ASP.NET MVC 1, и некоторые основные понятия, лежащие в основе ИТ.
> 
> Если вы используете ASP.NET MVC 3, мы рекомендуем следовать руководствам по [Начало работы в MVC 3 или в приложении для](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) [музыкального магазина MVC](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) .

## <a name="nerddinner-tutorial"></a>Руководство по NerdDinner

Лучшим способом изучения новой платформы является создание чего-то с ней. В этом руководстве описано, как создать небольшое, но полное приложение, использующее ASP.NET MVC, и некоторые основные понятия, лежащие в основе ИТ.

Приложение, которое мы собираемся создавать, называется "NerdDinner". NerdDinner предоставляет пользователям простой способ поиска и организации диннерс в Интернете:

![](introducing-the-nerddinner-tutorial/_static/image1.png)

NerdDinner позволяет зарегистрированным пользователям создавать, изменять и удалять диннерс. Он обеспечивает согласованный набор проверок и бизнес-правил для приложения:

![](introducing-the-nerddinner-tutorial/_static/image2.png)

Посетители могут использовать карту на основе AJAX для поиска предстоящих диннерс рядом:

![](introducing-the-nerddinner-tutorial/_static/image3.png)

Щелкнув обед, вы перейдете на страницу сведений, где они могут получить дополнительные сведения о них:

![](introducing-the-nerddinner-tutorial/_static/image4.png)

Если вы заинтересованы в посещении компании Dinner, то можете войти на сайт или зарегистрироваться на нем:

![](introducing-the-nerddinner-tutorial/_static/image5.png)

Затем они могут щелкнуть ссылку RSVP на основе AJAX, чтобы посетить событие:

![](introducing-the-nerddinner-tutorial/_static/image6.png)

![](introducing-the-nerddinner-tutorial/_static/image7.png)

### <a name="implementing-nerddinner"></a>Реализация NerdDinner

Мы начнем наше приложение NerdDinner, используя команду "файл-&gt;новый проект" в Visual Studio, чтобы создать новый проект ASP.NET MVC. Затем мы постепенно добавим функции и функции. Как мы будем охватывать:

1. [Создание нового проекта MVC ASP.NET](create-a-new-aspnet-mvc-project.md)
2. [Создание базы данных](create-a-database.md)
3. [Создание модели с проверками бизнес-правил](build-a-model-with-business-rule-validations.md)
4. [Использование контроллеров и представлений для реализации пользовательского интерфейса листинга и подробностей](use-controllers-and-views-to-implement-a-listingdetails-ui.md)
5. [Как обеспечить поддержку записи формы для CRUD (создание, чтение, обновление, удаление) данных](provide-crud-create-read-update-delete-data-form-entry-support.md)
6. [Использование ViewData и реализация классов ViewModel](use-viewdata-and-implement-viewmodel-classes.md)
7. [Повторное использование пользовательского интерфейса с помощью главных страниц и частичных элементов](re-use-ui-using-master-pages-and-partials.md)
8. [Реализация эффективного разбиения данных на страницы](implement-efficient-data-paging.md)
9. [Защита приложений с помощью проверки подлинности и авторизации](secure-applications-using-authentication-and-authorization.md)
10. [Использование AJAX для доставки динамических обновлений](use-ajax-to-deliver-dynamic-updates.md)
11. [Использование AJAX для реализации сценариев сопоставления](use-ajax-to-implement-mapping-scenarios.md)
12. [Включение автоматического модульного тестирования](enable-automated-unit-testing.md)

Вы можете создать собственную копию NerdDinner с нуля, выполнив каждый шаг, который мы пошаговым руководством в этой главе. Вы также можете скачать готовую версию исходного кода здесь: [NerdDinner на GitHub](https://github.com/AspNetMVPSamples/NerdDinner). Кроме того, можно также [загрузить бесплатную версию этого учебника в формате PDF](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf) , если вы хотите прочитать учебник в автономном режиме.

Для создания приложения можно использовать Visual Studio 2008 или бесплатный выпуск Visual Web Developer 2008 Express. Для базы данных можно использовать либо SQL Server, либо бесплатную SQL Server Express.

Вы можете установить ASP.NET MVC, Visual Web Developer 2008 Express и SQL Server Express (все бесплатное) с помощью версии 2 [установщик веб-платформы Майкрософт](https://www.microsoft.com/web/downloads/platform.aspx)

### <a name="now-lets-get-started"></a>Теперь приступим к работе...

Теперь, когда мы узнали, что такое NerdDinner, давайте создадим закатайте рукава и напишем некоторый код.

Начнем с использования файла-&gt;нового проекта в Visual Studio, чтобы создать приложение NerdDinner.

> [!div class="step-by-step"]
> [Дальше](create-a-new-aspnet-mvc-project.md)
