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
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78449028"
---
# <a name="create-data-transfer-objects-dtos"></a><span data-ttu-id="62cd6-102">Создание объектов передачи данных (DTO)</span><span class="sxs-lookup"><span data-stu-id="62cd6-102">Create Data Transfer Objects (DTOs)</span></span>

<span data-ttu-id="62cd6-103">по [Майк Уоссон](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="62cd6-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="62cd6-104">Скачать завершенный проект</span><span class="sxs-lookup"><span data-stu-id="62cd6-104">Download Completed Project</span></span>](https://github.com/MikeWasson/BookService)

<span data-ttu-id="62cd6-105">Сейчас наш веб-API предоставляет клиенту сущности базы данных.</span><span class="sxs-lookup"><span data-stu-id="62cd6-105">Right now, our web API exposes the database entities to the client.</span></span> <span data-ttu-id="62cd6-106">Клиент получает данные, которые непосредственно сопоставляются с таблицами базы данных.</span><span class="sxs-lookup"><span data-stu-id="62cd6-106">The client receives data that maps directly to your database tables.</span></span> <span data-ttu-id="62cd6-107">Однако это не всегда хорошая идея.</span><span class="sxs-lookup"><span data-stu-id="62cd6-107">However, that's not always a good idea.</span></span> <span data-ttu-id="62cd6-108">Иногда требуется изменить форму данных, отправляемых клиенту.</span><span class="sxs-lookup"><span data-stu-id="62cd6-108">Sometimes you want to change the shape of the data that you send to client.</span></span> <span data-ttu-id="62cd6-109">Например, может понадобиться:</span><span class="sxs-lookup"><span data-stu-id="62cd6-109">For example, you might want to:</span></span>

- <span data-ttu-id="62cd6-110">Удалите циклические ссылки (см. предыдущий раздел).</span><span class="sxs-lookup"><span data-stu-id="62cd6-110">Remove circular references (see previous section).</span></span>
- <span data-ttu-id="62cd6-111">Скрыть определенные свойства, которые не должны просматривать клиенты.</span><span class="sxs-lookup"><span data-stu-id="62cd6-111">Hide particular properties that clients are not supposed to view.</span></span>
- <span data-ttu-id="62cd6-112">Чтобы уменьшить размер полезной нагрузки, пропустите некоторые свойства.</span><span class="sxs-lookup"><span data-stu-id="62cd6-112">Omit some properties in order to reduce payload size.</span></span>
- <span data-ttu-id="62cd6-113">Сведение графов объектов, содержащих вложенные объекты, чтобы сделать их более удобными для клиентов.</span><span class="sxs-lookup"><span data-stu-id="62cd6-113">Flatten object graphs that contain nested objects, to make them more convenient for clients.</span></span>
- <span data-ttu-id="62cd6-114">Избегайте перебора уязвимостей.</span><span class="sxs-lookup"><span data-stu-id="62cd6-114">Avoid "over-posting" vulnerabilities.</span></span> <span data-ttu-id="62cd6-115">(Дополнительные сведения см. в статье [Проверка модели](../../formats-and-model-binding/model-validation-in-aspnet-web-api.md) .)</span><span class="sxs-lookup"><span data-stu-id="62cd6-115">(See [Model Validation](../../formats-and-model-binding/model-validation-in-aspnet-web-api.md) for a discussion of over-posting.)</span></span>
- <span data-ttu-id="62cd6-116">Отделяйте слой служб от уровня базы данных.</span><span class="sxs-lookup"><span data-stu-id="62cd6-116">Decouple your service layer from your database layer.</span></span>

<span data-ttu-id="62cd6-117">Для этого можно определить *объект передачи данных* (DTO).</span><span class="sxs-lookup"><span data-stu-id="62cd6-117">To accomplish this, you can define a *data transfer object* (DTO).</span></span> <span data-ttu-id="62cd6-118">DTO — это объект, который определяет, как данные будут передаваться по сети.</span><span class="sxs-lookup"><span data-stu-id="62cd6-118">A DTO is an object that defines how the data will be sent over the network.</span></span> <span data-ttu-id="62cd6-119">Давайте посмотрим, как это работает с сущностью Book.</span><span class="sxs-lookup"><span data-stu-id="62cd6-119">Let's see how that works with the Book entity.</span></span> <span data-ttu-id="62cd6-120">В папке Models добавьте два класса DTO:</span><span class="sxs-lookup"><span data-stu-id="62cd6-120">In the Models folder, add two DTO classes:</span></span>

[!code-csharp[Main](part-5/samples/sample1.cs)]

<span data-ttu-id="62cd6-121">Класс `BookDetailDto` включает все свойства модели Book, за исключением того, что `AuthorName` является строкой, в которой будет содержаться имя автора.</span><span class="sxs-lookup"><span data-stu-id="62cd6-121">The `BookDetailDto` class includes all of the properties from the Book model, except that `AuthorName` is a string that will hold the author name.</span></span> <span data-ttu-id="62cd6-122">Класс `BookDto` содержит подмножество свойств из `BookDetailDto`.</span><span class="sxs-lookup"><span data-stu-id="62cd6-122">The `BookDto` class contains a subset of properties from `BookDetailDto`.</span></span>

<span data-ttu-id="62cd6-123">Затем замените два метода GET в классе `BooksController` на версии, возвращающие DTO.</span><span class="sxs-lookup"><span data-stu-id="62cd6-123">Next, replace the two GET methods in the `BooksController` class, with versions that return DTOs.</span></span> <span data-ttu-id="62cd6-124">Мы будем использовать инструкцию LINQ **SELECT** для преобразования сущностей Book в DTO.</span><span class="sxs-lookup"><span data-stu-id="62cd6-124">We'll use the LINQ **Select** statement to convert from Book entities into DTOs.</span></span>

[!code-csharp[Main](part-5/samples/sample2.cs)]

<span data-ttu-id="62cd6-125">Ниже приведен SQL, созданный с помощью нового метода `GetBooks`.</span><span class="sxs-lookup"><span data-stu-id="62cd6-125">Here is the SQL generated by the new `GetBooks` method.</span></span> <span data-ttu-id="62cd6-126">Видно, что EF преобразует LINQ **SELECT** в инструкцию SQL SELECT.</span><span class="sxs-lookup"><span data-stu-id="62cd6-126">You can see that EF translates the LINQ **Select** into a SQL SELECT statement.</span></span>

[!code-sql[Main](part-5/samples/sample3.sql)]

<span data-ttu-id="62cd6-127">Наконец, измените метод `PostBook`, чтобы он возвращал DTO.</span><span class="sxs-lookup"><span data-stu-id="62cd6-127">Finally, modify the `PostBook` method to return a DTO.</span></span>

[!code-csharp[Main](part-5/samples/sample4.cs)]

> [!NOTE]
> <span data-ttu-id="62cd6-128">В этом руководстве мы преобразуемся в DTO вручную в коде.</span><span class="sxs-lookup"><span data-stu-id="62cd6-128">In this tutorial, we're converting to DTOs manually in code.</span></span> <span data-ttu-id="62cd6-129">Другой вариант — использовать библиотеку, например [автосопоставитель](http://automapper.org/) , которая автоматически обрабатывает преобразование.</span><span class="sxs-lookup"><span data-stu-id="62cd6-129">Another option is to use a library like [AutoMapper](http://automapper.org/) that handles the conversion automatically.</span></span>
> 
> [!div class="step-by-step"]
> <span data-ttu-id="62cd6-130">[Назад](part-4.md)
> [Вперед](part-6.md)</span><span class="sxs-lookup"><span data-stu-id="62cd6-130">[Previous](part-4.md)
[Next](part-6.md)</span></span>
