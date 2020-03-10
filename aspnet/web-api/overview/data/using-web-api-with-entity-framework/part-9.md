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
# <a name="add-a-new-item-to-the-database"></a><span data-ttu-id="d2bd5-102">Добавление нового элемента в базу данных</span><span class="sxs-lookup"><span data-stu-id="d2bd5-102">Add a New Item to the Database</span></span>

<span data-ttu-id="d2bd5-103">по [Майк Уоссон](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="d2bd5-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="d2bd5-104">Скачать завершенный проект</span><span class="sxs-lookup"><span data-stu-id="d2bd5-104">Download Completed Project</span></span>](https://github.com/MikeWasson/BookService)

<span data-ttu-id="d2bd5-105">В этом разделе вы добавите возможность для пользователей создать новую книгу.</span><span class="sxs-lookup"><span data-stu-id="d2bd5-105">In this section, you will add the ability for users to create a new book.</span></span> <span data-ttu-id="d2bd5-106">В App. js добавьте следующий код в модель представления:</span><span class="sxs-lookup"><span data-stu-id="d2bd5-106">In app.js, add the following code to the view model:</span></span>

[!code-javascript[Main](part-9/samples/sample1.js)]

<span data-ttu-id="d2bd5-107">В index. cshtml Замените следующую разметку:</span><span class="sxs-lookup"><span data-stu-id="d2bd5-107">In Index.cshtml, replace the following markup:</span></span>

[!code-html[Main](part-9/samples/sample2.html)]

<span data-ttu-id="d2bd5-108">на:</span><span class="sxs-lookup"><span data-stu-id="d2bd5-108">With:</span></span>

[!code-html[Main](part-9/samples/sample3.html)]

<span data-ttu-id="d2bd5-109">Эта разметка создает форму для отправки нового автора.</span><span class="sxs-lookup"><span data-stu-id="d2bd5-109">This markup creates a form for submitting a new author.</span></span> <span data-ttu-id="d2bd5-110">Значения для раскрывающегося списка Author привязаны к данным `authors` наблюдаемых в модели представления.</span><span class="sxs-lookup"><span data-stu-id="d2bd5-110">The values for the author drop-down list are data-bound to the `authors` observable in the view model.</span></span> <span data-ttu-id="d2bd5-111">Для других входных данных формы значения привязываются к данным свойства `newBook` модели представления.</span><span class="sxs-lookup"><span data-stu-id="d2bd5-111">For the other form inputs, the values are data-bound to the `newBook` property of the view model.</span></span>

<span data-ttu-id="d2bd5-112">Обработчик отправки в форме привязан к функции `addBook`:</span><span class="sxs-lookup"><span data-stu-id="d2bd5-112">The submit handler on the form is bound to the `addBook` function:</span></span>

[!code-html[Main](part-9/samples/sample4.html)]

<span data-ttu-id="d2bd5-113">Функция `addBook` считывает текущие значения входных данных формы, привязанные к данным, для создания объекта JSON.</span><span class="sxs-lookup"><span data-stu-id="d2bd5-113">The `addBook` function reads the current values of the data-bound form inputs to create a JSON object.</span></span> <span data-ttu-id="d2bd5-114">Затем он отправляет объект JSON в `/api/books`.</span><span class="sxs-lookup"><span data-stu-id="d2bd5-114">Then it POSTs the JSON object to `/api/books`.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="d2bd5-115">[Назад](part-8.md)
> [Вперед](part-10.md)</span><span class="sxs-lookup"><span data-stu-id="d2bd5-115">[Previous](part-8.md)
[Next](part-10.md)</span></span>
