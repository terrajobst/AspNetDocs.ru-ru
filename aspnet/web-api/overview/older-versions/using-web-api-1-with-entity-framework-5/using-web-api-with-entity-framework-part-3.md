---
uid: web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-3
title: Часть 3. Создание административного контроллера | Документация Майкрософт
author: MikeWasson
description: ''
ms.author: riande
ms.date: 07/04/2012
ms.assetid: 6b9ae3c4-0274-4170-a1bb-9df9c546b2a9
msc.legacyurl: /web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-3
msc.type: authoredcontent
ms.openlocfilehash: f39be7a84e85db93487d246e9f8cb59c401fe5ce
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/28/2019
ms.locfileid: "74600043"
---
# <a name="part-3-creating-an-admin-controller"></a>Часть 3. Создание административного контроллера

по [Майк Уоссон](https://github.com/MikeWasson)

[Скачать завершенный проект](https://code.msdn.microsoft.com/ASP-NET-Web-API-with-afa30545)

## <a name="add-an-admin-controller"></a>Добавление контроллера администратора

В этом разделе мы добавим контроллер веб-API, который поддерживает операции CRUD (создание, чтение, обновление и удаление) для продуктов. Контроллер будет использовать Entity Framework для взаимодействия с уровнем базы данных. Только администраторы смогут использовать этот контроллер. Клиенты будут получать доступ к продуктам через другой контроллер.

В обозреватель решений щелкните правой кнопкой мыши папку Controllers. Выберите **Добавить** , а затем — **контроллер**.

![](using-web-api-with-entity-framework-part-3/_static/image1.png)

В диалоговом окне **Добавление контроллера введите** имя контроллера `AdminController`. В разделе **шаблон**выберите &quot;контроллер API с действиями чтения и записи, используя Entity Framework&quot;. В разделе **класс модели**выберите "продукт (Продуктсторе. Models)". В разделе **контекст данных**выберите "&lt;новый контекст данных&gt;".

![](using-web-api-with-entity-framework-part-3/_static/image2.png)

> [!NOTE]
> Если в раскрывающемся списке **класс модели** не отображаются классы модели, убедитесь, что проект скомпилирован. Entity Framework использует отражение, поэтому ему требуется скомпилированная сборка.

Если выбрать команду "&lt;создать контекст данных&gt;", откроется диалоговое окно " **Создание контекста данных** ". Назовите `ProductStore.Models.OrdersContext`контекста данных.

![](using-web-api-with-entity-framework-part-3/_static/image3.png)

Нажмите кнопку **ОК** , чтобы закрыть диалоговое окно **новый контекст данных** . В диалоговом окне **Добавление контроллера** нажмите кнопку **Добавить**.

Вот что было добавлено в проект:

- Класс с именем `OrdersContext`, производный от **DbContext**. Этот класс обеспечивает привязывание между моделями POCO и базой данных.
- Контроллер веб-API с именем `AdminController`. Этот контроллер поддерживает операции CRUD на экземплярах `Product`. Для взаимодействия с Entity Frameworkом используется класс `OrdersContext`.
- Новая строка подключения к базе данных в файле Web. config.

![](using-web-api-with-entity-framework-part-3/_static/image4.png)

Откройте файл OrdersContext.cs. Обратите внимание, что конструктор задает имя строки подключения к базе данных. Это имя относится к строке подключения, которая была добавлена в файл Web. config.

[!code-csharp[Main](using-web-api-with-entity-framework-part-3/samples/sample1.cs)]

Добавьте в класс `OrdersContext` следующие свойства:

[!code-csharp[Main](using-web-api-with-entity-framework-part-3/samples/sample2.cs)]

**DbSet** представляет набор сущностей, которые можно запросить. Ниже приведен полный список для класса `OrdersContext`.

[!code-csharp[Main](using-web-api-with-entity-framework-part-3/samples/sample3.cs)]

Класс `AdminController` определяет пять методов, реализующих базовую функциональность CRUD. Каждый метод соответствует URI, который может быть вызван клиентом:

| Метод контроллера | Описание | URI | Метод HTTP |
| --- | --- | --- | --- |
| GetProducts | Возвращает все продукты. | API и продукты | GET |
| Продукт | Находит продукт по ИДЕНТИФИКАТОРу. | API/Products/*ID* | GET |
| путпродукт | Обновляет продукт. | API/Products/*ID* | PUT |
| Продукт | Создает новый продукт. | API и продукты | ПОМЕСТИТЬ |
| DeleteProduct | Удаляет продукт. | API/Products/*ID* | DELETE |

Каждый метод вызывает `OrdersContext` для запроса к базе данных. Методы, которые изменяют вызов метода Collection (размещение, публикация и удаление), `db.SaveChanges`, чтобы сохранить изменения в базе данных. Контроллеры создаются для каждого HTTP-запроса, а затем удаляются, поэтому необходимо сохранить изменения перед возвратом метода.

## <a name="add-a-database-initializer"></a>Добавление инициализатора базы данных

Entity Framework имеет удобную функцию, позволяющую заполнять базу данных при запуске, а также автоматически воссоздавать базу данных при каждом изменении моделей. Эта функция полезна во время разработки, поскольку у вас всегда есть тестовые данные даже при изменении моделей.

В обозреватель решений щелкните правой кнопкой мыши папку Models и создайте новый класс с именем `OrdersContextInitializer`. Вставьте следующую реализацию:

[!code-csharp[Main](using-web-api-with-entity-framework-part-3/samples/sample4.cs)]

Наследуя класс **дропкреатедатабасеифмоделчанжес** , мы сообщаем Entity Framework удалить базу данных при изменении классов модели. Когда Entity Framework создает (или повторно создает) базу данных, она вызывает метод **SEED** для заполнения таблиц. Мы используем метод **SEED** для добавления примеров продуктов, а также пример порядка.

Эта функция отлично подходит для тестирования, но не использует класс **дропкреатедатабасеифмоделчанжес** в рабочей среде, так как вы можете потерять данные, если кто-то изменил класс модели.

Затем откройте Global. asax и добавьте следующий код в метод **\_запуска приложения** :

[!code-csharp[Main](using-web-api-with-entity-framework-part-3/samples/sample5.cs)]

## <a name="send-a-request-to-the-controller"></a>Отправка запроса контроллеру

На этом этапе мы не написали код клиента, но веб-API можно вызвать с помощью веб-браузера или средства отладки HTTP, такого как [Fiddler](http://www.fiddler2.com/fiddler2/). В Visual Studio нажмите клавишу F5, чтобы начать отладку. Веб-браузер откроется в `http://localhost:*portnum*/`, где *портнум* — это номер порта.

Отправка HTTP-запроса в "`http://localhost:*portnum*/api/admin`. Первый запрос может быть слишком большим, так как Entity Framework необходимо создать и заполнить базу данных. Ответ должен выглядеть примерно следующим образом:

[!code-console[Main](using-web-api-with-entity-framework-part-3/samples/sample6.cmd)]

> [!div class="step-by-step"]
> [Назад](using-web-api-with-entity-framework-part-2.md)
> [Вперед](using-web-api-with-entity-framework-part-4.md)
