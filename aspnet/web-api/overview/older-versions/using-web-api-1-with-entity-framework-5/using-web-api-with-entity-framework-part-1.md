---
uid: web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-1
title: Часть 1. Обзор и создание проекта | Документация Майкрософт
author: MikeWasson
description: ''
ms.author: riande
ms.date: 07/03/2012
ms.assetid: 94421d86-68c4-4471-bf5f-82d654a17252
msc.legacyurl: /web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-1
msc.type: authoredcontent
ms.openlocfilehash: a76a18f2bd95969358452085ef342fdca8a386e2
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/28/2019
ms.locfileid: "74600330"
---
# <a name="part-1-overview-and-creating-the-project"></a>Часть 1. Обзор и создание проекта

по [Майк Уоссон](https://github.com/MikeWasson)

[Скачать завершенный проект](https://code.msdn.microsoft.com/ASP-NET-Web-API-with-afa30545)

Entity Framework — это платформа объектно-реляционного сопоставления. Он сопоставляет объекты домена в коде с сущностями в реляционной базе данных. В большинстве случаев вам не нужно беспокоиться о уровне базы данных, так как Entity Framework подбирается за вас. Код манипулирует объектами, и изменения сохраняются в базе данных.

## <a name="about-the-tutorial"></a>О учебнике

В этом руководстве вы создадите простое приложение Store. Приложение состоит из двух основных частей. Обычные пользователи могут просматривать продукты и создавать заказы:

![](using-web-api-with-entity-framework-part-1/_static/image1.png)

Администраторы могут создавать, удалять и изменять продукты:

![](using-web-api-with-entity-framework-part-1/_static/image2.png)

## <a name="skills-youll-learn"></a>Навыки, которые вы узнаете

Вот что вы узнаете:

- Использование Entity Framework с веб-API ASP.NET.
- Использование маскирования. js для создания динамического пользовательского интерфейса клиента.
- Использование проверки подлинности с помощью форм с веб-API для проверки подлинности пользователей.

Хотя это руководство является автономным, вы можете сначала ознакомиться со следующими учебниками:

- [Ваша первая веб-API ASP.NET](../../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md)
- [Создание веб-API, поддерживающего операции CRUD](../creating-a-web-api-that-supports-crud-operations.md)

Некоторые знания о [ASP.NET MVC](../../../../mvc/index.md) также полезны.

## <a name="overview"></a>Обзор

На высоком уровне ниже приведена архитектура приложения.

- ASP.NET MVC создает HTML-страницы для клиента.
- Веб-API ASP.NET предоставляет операции CRUD с данными (продукты и заказы).
- Entity Framework преобразует C# модели, используемые веб-API, в сущности базы данных.

![](using-web-api-with-entity-framework-part-1/_static/image3.png)

На следующей схеме показано, как объекты предметной области представлены на различных уровнях приложения: уровень базы данных, объектная модель и, наконец, формат подключения, который используется для передачи данных клиенту по протоколу HTTP.

![](using-web-api-with-entity-framework-part-1/_static/image4.png)

## <a name="create-the-visual-studio-project"></a>Создание проекта Visual Studio

Проект Tutorial можно создать с помощью Visual Web Developer Express или полной версии Visual Studio.

На **начальной** странице нажмите кнопку **создать проект**.

В области **шаблоны** выберите **Установленные шаблоны** и разверните узел  **C# визуального** элемента. В **разделе C#визуальный** элемент выберите **веб**. В списке шаблонов проектов выберите **ASP.NET MVC 4 веб-приложение**. Присвойте проекту имя "Продуктсторе" и нажмите кнопку **ОК**.

![](using-web-api-with-entity-framework-part-1/_static/image5.png)

В диалоговом окне **Новый проект ASP.NET MVC 4** выберите **Интернет приложение** и нажмите кнопку **ОК**.

![](using-web-api-with-entity-framework-part-1/_static/image6.png)

Шаблон "Интернет приложение" создает приложение ASP.NET MVC, которое поддерживает проверку подлинности с помощью форм. Если запустить приложение сейчас, у него уже есть некоторые функции:

- Новые пользователи могут зарегистрироваться, щелкнув ссылку "регистрация" в правом верхнем углу.
- Зарегистрированные пользователи могут войти, щелкнув ссылку "вход".

Сведения о членстве сохраняются в базе данных, которая создается автоматически. Дополнительные сведения о проверке подлинности в ASP.NET MVC см. в разделе [Пошаговое руководство. Использование проверки подлинности с помощью форм в ASP.NET MVC](https://msdn.microsoft.com/library/ff398049(VS.98).aspx).

## <a name="update-the-css-file"></a>Обновить CSS файл

Этот шаг является косметическим, но при этом страницы отображаются как предыдущие снимки экрана.

В обозреватель решений разверните папку содержимое и откройте файл с именем site. CSS. Добавьте следующие стили CSS:

[!code-css[Main](using-web-api-with-entity-framework-part-1/samples/sample1.css)]

> [!div class="step-by-step"]
> [Вперед](using-web-api-with-entity-framework-part-2.md)
