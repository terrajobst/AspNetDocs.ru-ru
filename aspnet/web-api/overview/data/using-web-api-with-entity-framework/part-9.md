---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-9
title: Добавить новый элемент в базу данных | Документация Майкрософт
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/16/2014
ms.assetid: 0967c29e-e124-4db0-a788-c45d0ff5aff2
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-9
msc.type: authoredcontent
ms.openlocfilehash: 692269a2c11e529af78f24feca74bba704b5b54b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78448974"
---
# <a name="add-a-new-item-to-the-database"></a>Добавление нового элемента в базу данных

по [Майк Уоссон](https://github.com/MikeWasson)

[Скачать завершенный проект](https://github.com/MikeWasson/BookService)

В этом разделе вы добавите возможность для пользователей создать новую книгу. В App. js добавьте следующий код в модель представления:

[!code-javascript[Main](part-9/samples/sample1.js)]

В index. cshtml Замените следующую разметку:

[!code-html[Main](part-9/samples/sample2.html)]

на:

[!code-html[Main](part-9/samples/sample3.html)]

Эта разметка создает форму для отправки нового автора. Значения для раскрывающегося списка Author привязаны к данным `authors` наблюдаемых в модели представления. Для других входных данных формы значения привязываются к данным свойства `newBook` модели представления.

Обработчик отправки в форме привязан к функции `addBook`:

[!code-html[Main](part-9/samples/sample4.html)]

Функция `addBook` считывает текущие значения входных данных формы, привязанные к данным, для создания объекта JSON. Затем он отправляет объект JSON в `/api/books`.

> [!div class="step-by-step"]
> [Назад](part-8.md)
> [Вперед](part-10.md)
