---
uid: web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-2
title: Часть 2. Создание моделей предметной области | Документация Майкрософт
author: MikeWasson
description: ''
ms.author: riande
ms.date: 07/03/2012
ms.assetid: fe3ef85f-bdc6-4e10-9768-25aa565c01d0
msc.legacyurl: /web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-2
msc.type: authoredcontent
ms.openlocfilehash: 7c5ed1bdb4b390c94907b14e208231f16ad42d96
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/28/2019
ms.locfileid: "74600358"
---
# <a name="part-2-creating-the-domain-models"></a>Часть 2. Создание моделей предметной области

по [Майк Уоссон](https://github.com/MikeWasson)

[Скачать завершенный проект](https://code.msdn.microsoft.com/ASP-NET-Web-API-with-afa30545)

## <a name="add-models"></a>Добавление моделей

Существует три способа подхода Entity Framework.

- База данных. сначала вы начинаете с базы данных, а Entity Framework создаете код.
- Модель — сначала: начинается с визуальной модели, а Entity Framework создает и базу данных, и код.
- Код — сначала: начинается с кода, а Entity Framework создает базу данных.

Мы используем подход с использованием кода, поэтому начнем с определения наших объектов домена как POCO (обычные объекты CLR). При использовании подхода "код — первый" объекты предметной области не требуют дополнительного кода для поддержки уровня базы данных, например транзакций или сохраняемости. (В частности, им не нужно наследовать от класса [EntityObject](https://msdn.microsoft.com/library/system.data.objects.dataclasses.entityobject.aspx) .) Заметки к данным по-прежнему можно использовать для управления Entity Framework создания схемы базы данных.

Поскольку POCO не содержит дополнительных свойств, описывающих [состояние базы данных](https://msdn.microsoft.com/library/system.data.entitystate.aspx), их можно легко сериализовать в формат JSON или XML. Однако это не означает, что всегда следует предоставлять модели Entity Framework непосредственно клиентам, как будет показано далее в этом руководстве.

Мы создадим следующие POCO:

- Продукт
- Номер
- OrderDetail

Чтобы создать каждый класс, щелкните правой кнопкой мыши папку Models в обозреватель решений. В контекстном меню выберите **Добавить** , а затем выберите **класс.**

![](using-web-api-with-entity-framework-part-2/_static/image1.png)

Добавьте класс `Product` со следующей реализацией:

[!code-csharp[Main](using-web-api-with-entity-framework-part-2/samples/sample1.cs)]

По соглашению Entity Framework использует свойство `Id` в качестве первичного ключа и сопоставляет его со столбцом идентификаторов в таблице базы данных. При создании нового экземпляра `Product` не устанавливается значение для `Id`, так как база данных создает значение.

Атрибут **скаффолдколумн** указывает ASP.NET MVC пропустить свойство `Id` при создании формы редактора. Для проверки модели используется **обязательный** атрибут. Он указывает, что свойство `Name` должно быть непустой строкой.

Добавьте класс `Order`:

[!code-csharp[Main](using-web-api-with-entity-framework-part-2/samples/sample2.cs)]

Добавьте класс `OrderDetail`:

[!code-csharp[Main](using-web-api-with-entity-framework-part-2/samples/sample3.cs)]

## <a name="foreign-key-relations"></a>Связи по внешнему ключу

Заказ содержит много подробных сведений о заказах, и каждая информация о заказе относится к одному продукту. Для представления этих отношений класс `OrderDetail` определяет свойства с именами `OrderId` и `ProductId`. Entity Framework определит, что эти свойства представляют внешние ключи, и добавит ограничения внешнего ключа в базу данных.

![](using-web-api-with-entity-framework-part-2/_static/image2.png)

Классы `Order` и `OrderDetail` также включают свойства навигации, которые содержат ссылки на связанные объекты. При наличии заказа можно перейти к продуктам в порядке, следуя свойствам навигации.

Скомпилируйте проект прямо сейчас. Entity Framework использует отражение для обнаружения свойств моделей, поэтому для создания схемы базы данных требуется скомпилированная сборка.

## <a name="configure-the-media-type-formatters"></a>Настройка модулей форматирования типа мультимедиа

[Модуль форматирования типа мультимедиа](../../formats-and-model-binding/media-formatters.md) — это объект, который сериализует данные при записи веб-API в текст ответа HTTP. Встроенные модули форматирования поддерживают выходные данные JSON и XML. По умолчанию оба этих модуля форматирования сериализуются все объекты по значению.

Сериализация по значению создает проблему, если граф объекта содержит циклические ссылки. Именно в этом случае классы `Order` и `OrderDetail`, так как каждый из них содержит ссылку на другой. Модуль форматирования будет следовать ссылкам, записывать каждый объект по значению и идти по кругам. Поэтому необходимо изменить поведение по умолчанию.

В обозреватель решений разверните папку приложение\_запуск и откройте файл с именем WebApiConfig.cs. Добавьте следующий код в класс `WebApiConfig` :

[!code-csharp[Main](using-web-api-with-entity-framework-part-2/samples/sample4.cs?highlight=11)]

Этот код задает модуль форматирования JSON для сохранения ссылок на объекты и полностью удаляет модуль форматирования XML из конвейера. (Можно настроить модуль форматирования XML для сохранения ссылок на объекты, но это немного дополнительная работа, и для этого приложения требуется только JSON. Дополнительные сведения см. в разделе [Обработка циклических ссылок на объекты](../../formats-and-model-binding/json-and-xml-serialization.md#handling_circular_object_references).)

> [!div class="step-by-step"]
> [Назад](using-web-api-with-entity-framework-part-1.md)
> [Вперед](using-web-api-with-entity-framework-part-3.md)
