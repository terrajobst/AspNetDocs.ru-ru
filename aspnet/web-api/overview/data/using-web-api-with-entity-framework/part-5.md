---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-5
title: Создание объектов Передача данных (DTO) | Документация Майкрософт
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/16/2014
ms.assetid: 0fd07176-b74b-48f0-9fac-0f02e3ffa213
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-5
msc.type: authoredcontent
ms.openlocfilehash: fc0463420207eba764014b8ec7123c5150e38247
ms.sourcegitcommit: 84b1681d4e6253e30468c8df8a09fe03beea9309
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/02/2019
ms.locfileid: "73445762"
---
# <a name="create-data-transfer-objects-dtos"></a>Создание объектов передачи данных (DTO)

по [Майк Уоссон](https://github.com/MikeWasson)

[Скачать завершенный проект](https://github.com/MikeWasson/BookService)

Сейчас наш веб-API предоставляет клиенту сущности базы данных. Клиент получает данные, которые непосредственно сопоставляются с таблицами базы данных. Однако это не всегда хорошая идея. Иногда требуется изменить форму данных, отправляемых клиенту. Например, можно сделать следующее:

- Удалите циклические ссылки (см. предыдущий раздел).
- Скрыть определенные свойства, которые не должны просматривать клиенты.
- Чтобы уменьшить размер полезной нагрузки, пропустите некоторые свойства.
- Сведение графов объектов, содержащих вложенные объекты, чтобы сделать их более удобными для клиентов.
- Избегайте перебора уязвимостей. (Дополнительные сведения см. в статье [Проверка модели](../../formats-and-model-binding/model-validation-in-aspnet-web-api.md) .)
- Отделяйте слой служб от уровня базы данных.

Для этого можно определить *объект передачи данных* (DTO). DTO — это объект, который определяет, как данные будут передаваться по сети. Давайте посмотрим, как это работает с сущностью Book. В папке Models добавьте два класса DTO:

[!code-csharp[Main](part-5/samples/sample1.cs)]

Класс `BookDetailDto` включает все свойства модели Book, за исключением того, что `AuthorName` является строкой, в которой будет содержаться имя автора. Класс `BookDto` содержит подмножество свойств из `BookDetailDto`.

Затем замените два метода GET в классе `BooksController` на версии, возвращающие DTO. Мы будем использовать инструкцию LINQ **SELECT** для преобразования сущностей Book в DTO.

[!code-csharp[Main](part-5/samples/sample2.cs)]

Ниже приведен SQL, созданный с помощью нового метода `GetBooks`. Видно, что EF преобразует LINQ **SELECT** в инструкцию SQL SELECT.

[!code-sql[Main](part-5/samples/sample3.sql)]

Наконец, измените метод `PostBook`, чтобы он возвращал DTO.

[!code-csharp[Main](part-5/samples/sample4.cs)]

> [!NOTE]
> В этом руководстве мы преобразуемся в DTO вручную в коде. Другой вариант — использовать библиотеку, например [автосопоставитель](http://automapper.org/) , которая автоматически обрабатывает преобразование.
> 
> [!div class="step-by-step"]
> [Назад](part-4.md)
> [Вперед](part-6.md)
