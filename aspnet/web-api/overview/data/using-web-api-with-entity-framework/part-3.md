---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-3
title: Использовать Code First Migrations для заполнения базы данных | Документация Майкрософт
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/16/2014
ms.assetid: 76e2013a-65b7-488c-834d-9448ecea378e
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-3
msc.type: authoredcontent
ms.openlocfilehash: 257bd06848adb949330856cc71eeb3d685e9d036
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78449118"
---
# <a name="use-code-first-migrations-to-seed-the-database"></a>Использование Code First Migrations для заполнения базы данных

по [Майк Уоссон](https://github.com/MikeWasson)

[Скачать завершенный проект](https://github.com/MikeWasson/BookService)

В этом разделе вы будете использовать [Code First migrations](https://msdn.microsoft.com/data/jj591621) в EF для заполнения базы данных тестовыми данными.

В меню **Сервис** выберите **Диспетчер пакетов NuGet**, а затем выберите **консоль диспетчера пакетов**. В окне "Консоль диспетчера пакетов" введите следующую команду:

[!code-console[Main](part-3/samples/sample1.cmd)]

Эта команда добавляет папку с именем миграции в проект и файл кода с именем Configuration.cs в папке migrations.

![](part-3/_static/image1.png)

Откройте файл Configuration.cs. Добавьте следующую инструкцию **using** .

[!code-csharp[Main](part-3/samples/sample2.cs)]

Затем добавьте следующий код в метод **Configuration. SEED** :

[!code-csharp[Main](part-3/samples/sample3.cs)]

В окне консоли диспетчера пакетов введите следующие команды:

[!code-console[Main](part-3/samples/sample4.cmd)]

Первая команда создает код, создающий базу данных, а вторая команда выполняет этот код. База данных создается локально с помощью [LocalDB](https://msdn.microsoft.com/library/hh510202.aspx).

![](part-3/_static/image2.png)

## <a name="explore-the-api-optional"></a>Изучение API (необязательно)

Нажмите F5, чтобы выполнить приложение в режиме отладки. Visual Studio запускает IIS Express и запускает веб-приложение. Затем Visual Studio запустит браузер и откроет домашнюю страницу приложения.

Когда Visual Studio выполняет веб-проект, он назначает номер порта. На рисунке ниже показан номер порта 50524. При запуске приложения вы увидите другой номер порта.

![](part-3/_static/image3.png)

Домашняя страница реализуется с помощью ASP.NET MVC. В верхней части страницы есть ссылка с текстом "API". Эта ссылка позволяет получить автоматически созданную страницу справки для веб-API. (Дополнительные сведения о создании этой страницы справки и о том, как добавить собственную документацию на страницу, см. в разделе [Создание страниц справки для веб-API ASP.NET](../../getting-started-with-aspnet-web-api/creating-api-help-pages.md).) Можно щелкнуть ссылку на страницу справки, чтобы просмотреть сведения об API, включая формат запроса и ответа.

![](part-3/_static/image4.png)

API включает операции CRUD в базе данных. Ниже приведена сводка по API.

| Авторы |  |
| --- | -- |
| GET api/authors | Получение всех авторов. |
| GET api/authors/{id} | Получить автора по ИДЕНТИФИКАТОРу. |
| POST /api/authors | Создайте нового автора. |
| PUT /api/authors/{id} | Обновление существующего автора. |
| DELETE /api/authors/{id} | Удаление автора. |

| Книги |  |
| --- | -- |
| GET /api/books | Получить все книги. |
| GET /api/books/{id} | Получение книги по ИДЕНТИФИКАТОРу. |
| POST /api/books | Создайте новую книгу. |
| PUT /api/books/{id} | Обновление существующей книги. |
| DELETE /api/books/{id} | Удаление книги. |

## <a name="view-the-database-optional"></a>Просмотр базы данных (необязательно)

При выполнении команды Update-Database EF создал базу данных и вызвала метод `Seed`. При локальном запуске приложения EF использует [LocalDB](https://blogs.msdn.com/b/sqlexpress/archive/2011/07/12/introducing-localdb-a-better-sql-express.aspx). Вы можете просмотреть базу данных в Visual Studio. В меню **Представление** выберите **Обозреватель объектов SQL Server**.

![](part-3/_static/image5.png)

В диалоговом окне **соединение с сервером** в поле ввода **имя сервера** введите "(LocalDB) \v11.0". Оставьте параметр **проверки подлинности** "Проверка подлинности Windows". Нажмите кнопку **Соединить**.

![](part-3/_static/image6.png)

Visual Studio подключается к LocalDB и отображает существующие базы данных в окне обозреватель объектов SQL Server. Можно развернуть узлы, чтобы просмотреть таблицы, созданные EF.

![](part-3/_static/image7.png)

Чтобы просмотреть данные, щелкните правой кнопкой мыши таблицу и выберите **Просмотреть данные**.

![](part-3/_static/image8.png)

На следующем снимке экрана показаны результаты для таблицы Books. Обратите внимание, что EF заполняет базу данных начальными данными, а таблица содержит внешний ключ для таблицы authors.

![](part-3/_static/image9.png)

> [!div class="step-by-step"]
> [Назад](part-2.md)
> [Вперед](part-4.md)
