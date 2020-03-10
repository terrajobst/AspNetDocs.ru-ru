---
uid: web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-4
title: Часть 4. Добавление административного представления | Документация Майкрософт
author: MikeWasson
description: ''
ms.author: riande
ms.date: 07/04/2012
ms.assetid: 792f4513-a508-4d14-a0dd-1a2fe282c7bb
msc.legacyurl: /web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-4
msc.type: authoredcontent
ms.openlocfilehash: 664aeb33031e933322886a6d6bdd989277e9fda2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78447882"
---
# <a name="part-4-adding-an-admin-view"></a>Часть 4. Добавление административного представления

по [Майк Уоссон](https://github.com/MikeWasson)

[Скачать завершенный проект](https://code.msdn.microsoft.com/ASP-NET-Web-API-with-afa30545)

## <a name="add-an-admin-view"></a>Добавление представления администратора

Теперь мы вернемся к клиентской стороне и добавим страницу, которая может использовать данные из административного контроллера. Страница позволяет пользователям создавать, изменять и удалять продукты, отправляя запросы AJAX к контроллеру.

В обозреватель решений разверните папку Controllers и откройте файл с именем HomeController.cs. Этот файл содержит контроллер MVC. Добавьте метод с именем `Admin`:

[!code-csharp[Main](using-web-api-with-entity-framework-part-4/samples/sample1.cs)]

Метод **хттпраутеурл** создает универсальный код ресурса (URI) для веб-API и сохраняет его в контейнере представления для последующего использования.

Затем поместите текстовый курсор в метод действия `Admin`, щелкните его правой кнопкой мыши и выберите **Добавить представление**. Откроется диалоговое окно **Добавление представления** .

![](using-web-api-with-entity-framework-part-4/_static/image1.png)

В диалоговом окне **Добавление представления** назовите представление "admin". Установите флажок **создать строго типизированное представление**. В разделе **класс модели**выберите "продукт (Продуктсторе. Models)". Оставьте все остальные параметры в качестве значений по умолчанию.

![](using-web-api-with-entity-framework-part-4/_static/image2.png)

При нажатии кнопки **Добавить** добавляется файл admin. cshtml в области Views/Home. Откройте этот файл и добавьте следующий код HTML. Этот HTML определяет структуру страницы, но функции еще не привязаны.

[!code-cshtml[Main](using-web-api-with-entity-framework-part-4/samples/sample2.cshtml)]

## <a name="create-a-link-to-the-admin-page"></a>Создание ссылки на страницу администрирования

В обозреватель решений разверните папку представления, а затем — общую папку. Откройте файл с именем \_Layout. cshtml. Поиск элемента **UL** с ID = "Menu" и ссылки на действие для представления администрирования:

[!code-cshtml[Main](using-web-api-with-entity-framework-part-4/samples/sample3.cshtml)]

> [!NOTE]
> В примере проекта я сделал несколько других косметических изменений, например заменить строку "Ваша Эмблема здесь". Они не влияют на функциональность приложения. Вы можете скачать проект и сравнить файлы.

Запустите приложение и щелкните ссылку Admin (администратор), которая отображается в верхней части домашней страницы. Страница администрирования должна выглядеть следующим образом:

![](using-web-api-with-entity-framework-part-4/_static/image3.png)

Прямо сейчас страница не выполняет никаких действий. В следующем разделе мы будем использовать выколачивание. js для создания динамического пользовательского интерфейса.

## <a name="add-authorization"></a>Добавить авторизацию

Страница администрирования в настоящее время доступна для всех, кто посещает сайт. Изменим это значение, чтобы ограничить разрешения администраторам.

Для начала добавьте роль "Администратор" и пользователя с правами администратора. В обозреватель решений разверните папку фильтры и откройте файл с именем InitializeSimpleMembershipAttribute.cs. Нахождение конструктора `SimpleMembershipInitializer`. После вызова **инитиализедатабасеконнектион.** добавьте следующий код:

[!code-csharp[Main](using-web-api-with-entity-framework-part-4/samples/sample4.cs)]

Это быстрый и недействительный способ добавить роль "Администратор" и создать пользователя для роли.

В обозреватель решений разверните папку Controllers и откройте файл HomeController.cs. Добавьте атрибут **авторизовать** в метод `Admin`.

[!code-csharp[Main](using-web-api-with-entity-framework-part-4/samples/sample5.cs)]

Откройте файл AdminController.cs и добавьте атрибут **авторизовать** во весь класс `AdminController`.

[!code-csharp[Main](using-web-api-with-entity-framework-part-4/samples/sample6.cs)]

> [!NOTE]
> MVC и веб-API определяют атрибуты **авторизации** в разных пространствах имен. MVC использует **System. Web. MVC. AuthorizeAttribute**, а веб-API использует **System. Web. http. AuthorizeAttribute**.

Теперь только администраторы могут просматривать страницу Администратор. Кроме того, при отправке HTTP-запроса на административный контроллер запрос должен содержать файл cookie проверки подлинности. В противном случае сервер отправляет ответ HTTP 401 (несанкционированный). Это можно увидеть в Fiddler, отправив запрос GET в `http://localhost:*port*/api/admin`.

> [!div class="step-by-step"]
> [Назад](using-web-api-with-entity-framework-part-3.md)
> [Вперед](using-web-api-with-entity-framework-part-5.md)
