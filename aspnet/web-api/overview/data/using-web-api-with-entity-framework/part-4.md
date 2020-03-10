---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-4
title: Обработка связей сущностей | Документация Майкрософт
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/16/2014
ms.assetid: d2f5710c-23c7-40a5-9cd9-5d0516570cba
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-4
msc.type: authoredcontent
ms.openlocfilehash: be4948e5443a5eb4e1824c63dd0c445a7ee1928e
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78449124"
---
# <a name="handling-entity-relations"></a><span data-ttu-id="d75f9-102">Обработка отношений сущностей</span><span class="sxs-lookup"><span data-stu-id="d75f9-102">Handling Entity Relations</span></span>

<span data-ttu-id="d75f9-103">по [Майк Уоссон](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="d75f9-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="d75f9-104">Скачать завершенный проект</span><span class="sxs-lookup"><span data-stu-id="d75f9-104">Download Completed Project</span></span>](https://github.com/MikeWasson/BookService)

<span data-ttu-id="d75f9-105">В этом разделе описаны некоторые сведения о том, как EF загружает связанные сущности и как обрабатывались циклические свойства навигации в классах модели.</span><span class="sxs-lookup"><span data-stu-id="d75f9-105">This section describes some details of how EF loads related entities, and how to handle circular navigation properties in your model classes.</span></span> <span data-ttu-id="d75f9-106">(Этот раздел содержит фундаментальные сведения и не является обязательным для работы с этим руководством.</span><span class="sxs-lookup"><span data-stu-id="d75f9-106">(This section provides background knowledge, and is not required to complete the tutorial.</span></span> <span data-ttu-id="d75f9-107">Если вы предпочитаете, перейдите к [части 5.](part-5.md)..)</span><span class="sxs-lookup"><span data-stu-id="d75f9-107">If you prefer, skip to [Part 5.](part-5.md).)</span></span>

## <a name="eager-loading-versus-lazy-loading"></a><span data-ttu-id="d75f9-108">Упреждающая загрузка и отложенная загрузка</span><span class="sxs-lookup"><span data-stu-id="d75f9-108">Eager Loading versus Lazy Loading</span></span>

<span data-ttu-id="d75f9-109">При использовании EF с реляционной базой данных важно понимать, как EF загружает связанные данные.</span><span class="sxs-lookup"><span data-stu-id="d75f9-109">When using EF with a relational database, it's important to understand how EF loads related data.</span></span>

<span data-ttu-id="d75f9-110">Также полезно просмотреть запросы SQL, формируемые EF.</span><span class="sxs-lookup"><span data-stu-id="d75f9-110">It's also useful to see the SQL queries that EF generates.</span></span> <span data-ttu-id="d75f9-111">Чтобы выполнить трассировку SQL, добавьте следующую строку кода в конструктор `BookServiceContext`:</span><span class="sxs-lookup"><span data-stu-id="d75f9-111">To trace the SQL, add the following line of code to the `BookServiceContext` constructor:</span></span>

[!code-csharp[Main](part-4/samples/sample1.cs)]

<span data-ttu-id="d75f9-112">Если отправить запрос GET в/АПИ/Букс, он вернет JSON следующим образом:</span><span class="sxs-lookup"><span data-stu-id="d75f9-112">If you send a GET request to /api/books, it returns JSON like the following:</span></span>

[!code-console[Main](part-4/samples/sample2.cmd)]

<span data-ttu-id="d75f9-113">Можно увидеть, что свойство Author имеет значение null, даже если книга содержит допустимый Аусорид.</span><span class="sxs-lookup"><span data-stu-id="d75f9-113">You can see that the Author property is null, even though the book contains a valid AuthorId.</span></span> <span data-ttu-id="d75f9-114">Это обусловлено тем, что EF не загружает связанные сущности Author.</span><span class="sxs-lookup"><span data-stu-id="d75f9-114">That's because EF is not loading the related Author entities.</span></span> <span data-ttu-id="d75f9-115">Журнал трассировки запроса SQL подтверждает следующее:</span><span class="sxs-lookup"><span data-stu-id="d75f9-115">The trace log of the SQL query confirms this:</span></span>

[!code-console[Main](part-4/samples/sample3.sql)]

<span data-ttu-id="d75f9-116">Инструкция SELECT берется из таблицы Books и не ссылается на таблицу Author.</span><span class="sxs-lookup"><span data-stu-id="d75f9-116">The SELECT statement takes from the Books table, and does not reference the Author table.</span></span>

<span data-ttu-id="d75f9-117">Для справки ниже приведен метод класса `BooksController`, который возвращает список книг.</span><span class="sxs-lookup"><span data-stu-id="d75f9-117">For reference, here is the method in the `BooksController` class that returns the list of books.</span></span>

[!code-csharp[Main](part-4/samples/sample4.cs)]

<span data-ttu-id="d75f9-118">Давайте посмотрим, как можно вернуть автора в составе данных JSON.</span><span class="sxs-lookup"><span data-stu-id="d75f9-118">Let's see how we can return the Author as part of the JSON data.</span></span> <span data-ttu-id="d75f9-119">Существует три способа загрузки связанных данных в Entity Framework: Упреждающая загрузка, отложенная загрузка и явная загрузка.</span><span class="sxs-lookup"><span data-stu-id="d75f9-119">There are three ways to load related data in Entity Framework: eager loading, lazy loading, and explicit loading.</span></span> <span data-ttu-id="d75f9-120">С каждым приемом связаны компромиссы, поэтому важно понимать, как они работают.</span><span class="sxs-lookup"><span data-stu-id="d75f9-120">There are trade-offs with each technique, so it's important to understand how they work.</span></span>

### <a name="eager-loading"></a><span data-ttu-id="d75f9-121">Активная загрузка</span><span class="sxs-lookup"><span data-stu-id="d75f9-121">Eager Loading</span></span>

<span data-ttu-id="d75f9-122">При *безотлагательной загрузке*EF загружает связанные сущности в ходе первоначального запроса к базе данных.</span><span class="sxs-lookup"><span data-stu-id="d75f9-122">With *eager loading*, EF loads related entities as part of the initial database query.</span></span> <span data-ttu-id="d75f9-123">Для выполнения безотлагательной загрузки используйте метод расширения **System. Data. Entity. include** .</span><span class="sxs-lookup"><span data-stu-id="d75f9-123">To perform eager loading, use the **System.Data.Entity.Include** extension method.</span></span>

[!code-csharp[Main](part-4/samples/sample5.cs)]

<span data-ttu-id="d75f9-124">Это указывает EF включить в запрос данные автора.</span><span class="sxs-lookup"><span data-stu-id="d75f9-124">This tells EF to include the Author data in the query.</span></span> <span data-ttu-id="d75f9-125">Если внести это изменение и запустить приложение, данные JSON будут выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="d75f9-125">If you make this change and run the app, now the JSON data looks like this:</span></span>

[!code-console[Main](part-4/samples/sample6.cmd)]

<span data-ttu-id="d75f9-126">В журнале трассировки показано, что EF выполнил соединение с таблицами Book и Author.</span><span class="sxs-lookup"><span data-stu-id="d75f9-126">The trace log shows that EF performed a join on the Book and Author tables.</span></span>

[!code-console[Main](part-4/samples/sample7.cmd)]

### <a name="lazy-loading"></a><span data-ttu-id="d75f9-127">Отложенная загрузка</span><span class="sxs-lookup"><span data-stu-id="d75f9-127">Lazy Loading</span></span>

<span data-ttu-id="d75f9-128">При отложенной загрузке EF автоматически загружает связанную сущность при разыменовании свойства навигации для этой сущности.</span><span class="sxs-lookup"><span data-stu-id="d75f9-128">With lazy loading, EF automatically loads a related entity when the navigation property for that entity is dereferenced.</span></span> <span data-ttu-id="d75f9-129">Чтобы включить отложенную загрузку, сделайте свойство навигации виртуальным.</span><span class="sxs-lookup"><span data-stu-id="d75f9-129">To enable lazy loading, make the navigation property virtual.</span></span> <span data-ttu-id="d75f9-130">Например, в классе Book:</span><span class="sxs-lookup"><span data-stu-id="d75f9-130">For example, in the Book class:</span></span>

[!code-csharp[Main](part-4/samples/sample8.cs?highlight=6)]

<span data-ttu-id="d75f9-131">Теперь рассмотрим следующий код:</span><span class="sxs-lookup"><span data-stu-id="d75f9-131">Now consider the following code:</span></span>

[!code-csharp[Main](part-4/samples/sample9.cs)]

<span data-ttu-id="d75f9-132">Если отложенная загрузка включена, доступ к свойству `Author` в `books[0]` приводит к тому, что EF запрашивает у автора запрос к базе данных.</span><span class="sxs-lookup"><span data-stu-id="d75f9-132">When lazy loading is enabled, accessing the `Author` property on `books[0]` causes EF to query the database for the author.</span></span>

<span data-ttu-id="d75f9-133">Для отложенной загрузки требуется несколько обращений к базе данных, поскольку EF отправляет запрос каждый раз, когда он извлекает связанную сущность.</span><span class="sxs-lookup"><span data-stu-id="d75f9-133">Lazy loading requires multiple database trips, because EF sends a query each time it retrieves a related entity.</span></span> <span data-ttu-id="d75f9-134">Как правило, для сериализуемых объектов требуется неактивная загрузка.</span><span class="sxs-lookup"><span data-stu-id="d75f9-134">Generally, you want lazy loading disabled for objects that you serialize.</span></span> <span data-ttu-id="d75f9-135">Сериализатор должен считывать все свойства модели, что активирует загрузку связанных сущностей.</span><span class="sxs-lookup"><span data-stu-id="d75f9-135">The serializer has to read all of the properties on the model, which triggers loading the related entities.</span></span> <span data-ttu-id="d75f9-136">Например, ниже приведены запросы SQL, когда EF сериализует список книг с включенной отложенной загрузкой.</span><span class="sxs-lookup"><span data-stu-id="d75f9-136">For example, here are the SQL queries when EF serializes the list of books with lazy loading enabled.</span></span> <span data-ttu-id="d75f9-137">Видно, что EF делает три отдельных запроса для трех авторов.</span><span class="sxs-lookup"><span data-stu-id="d75f9-137">You can see that EF makes three separate queries for the three authors.</span></span>

[!code-console[Main](part-4/samples/sample10.sql)]

<span data-ttu-id="d75f9-138">В некоторых случаях может потребоваться использовать отложенную загрузку.</span><span class="sxs-lookup"><span data-stu-id="d75f9-138">There are still times when you might want to use lazy loading.</span></span> <span data-ttu-id="d75f9-139">Упреждающая загрузка может привести к тому, что EF создаст очень сложное соединение.</span><span class="sxs-lookup"><span data-stu-id="d75f9-139">Eager loading can cause EF to generate a very complex join.</span></span> <span data-ttu-id="d75f9-140">Или может потребоваться наличие связанных сущностей для небольшого подмножества данных, а отложенная загрузка будет более эффективной.</span><span class="sxs-lookup"><span data-stu-id="d75f9-140">Or you might need related entities for a small subset of the data, and lazy loading would be more efficient.</span></span>

<span data-ttu-id="d75f9-141">Одним из способов избежать проблем с сериализацией является сериализация объектов передаваемых данных (DTO), а не объектов сущностей.</span><span class="sxs-lookup"><span data-stu-id="d75f9-141">One way to avoid serialization problems is to serialize data transfer objects (DTOs) instead of entity objects.</span></span> <span data-ttu-id="d75f9-142">Этот подход будет показан далее в этой статье.</span><span class="sxs-lookup"><span data-stu-id="d75f9-142">I'll show this approach later in the article.</span></span>

### <a name="explicit-loading"></a><span data-ttu-id="d75f9-143">Явная загрузка</span><span class="sxs-lookup"><span data-stu-id="d75f9-143">Explicit Loading</span></span>

<span data-ttu-id="d75f9-144">Явная загрузка аналогична отложенной загрузке за исключением того, что вы явно получаете связанные данные в коде. Это не происходит автоматически при доступе к свойству навигации.</span><span class="sxs-lookup"><span data-stu-id="d75f9-144">Explicit loading is similar to lazy loading, except that you explicitly get the related data in code; it doesn't happen automatically when you access a navigation property.</span></span> <span data-ttu-id="d75f9-145">Явная загрузка обеспечивает более полное управление временем загрузки связанных данных, но требует дополнительного кода.</span><span class="sxs-lookup"><span data-stu-id="d75f9-145">Explicit loading gives you more control over when to load related data, but requires extra code.</span></span> <span data-ttu-id="d75f9-146">Дополнительные сведения о явной загрузке см. в разделе [Загрузка связанных сущностей](https://msdn.microsoft.com/data/jj574232#explicit).</span><span class="sxs-lookup"><span data-stu-id="d75f9-146">For more information about explicit loading, see [Loading Related Entities](https://msdn.microsoft.com/data/jj574232#explicit).</span></span>

## <a name="navigation-properties-and-circular-references"></a><span data-ttu-id="d75f9-147">Свойства навигации и циклические ссылки</span><span class="sxs-lookup"><span data-stu-id="d75f9-147">Navigation Properties and Circular References</span></span>

<span data-ttu-id="d75f9-148">Определив модели книги и автора, я определил свойство навигации в классе `Book` для связи «книга-автор», но я не определил свойство навигации в другом направлении.</span><span class="sxs-lookup"><span data-stu-id="d75f9-148">When I defined the Book and Author models, I defined a navigation property on the `Book` class for the Book-Author relationship, but I did not define a navigation property in the other direction.</span></span>

<span data-ttu-id="d75f9-149">Что произойдет, если добавить соответствующее свойство навигации в класс `Author`?</span><span class="sxs-lookup"><span data-stu-id="d75f9-149">What happens if you add the corresponding navigation property to the `Author` class?</span></span>

[!code-csharp[Main](part-4/samples/sample11.cs?highlight=7)]

<span data-ttu-id="d75f9-150">К сожалению, это создает проблему при сериализации моделей.</span><span class="sxs-lookup"><span data-stu-id="d75f9-150">Unfortunately, this creates a problem when you serialize the models.</span></span> <span data-ttu-id="d75f9-151">При загрузке связанных данных создается круглый граф объектов.</span><span class="sxs-lookup"><span data-stu-id="d75f9-151">If you load the related data, it creates a circular object graph.</span></span>

![](part-4/_static/image1.png)

<span data-ttu-id="d75f9-152">Когда модуль форматирования JSON или XML пытается сериализовать граф, возникает исключение.</span><span class="sxs-lookup"><span data-stu-id="d75f9-152">When the JSON or XML formatter tries to serialize the graph, it will throw an exception.</span></span> <span data-ttu-id="d75f9-153">Два модуля форматирования создают разные сообщения об исключениях.</span><span class="sxs-lookup"><span data-stu-id="d75f9-153">The two formatters throw different exception messages.</span></span> <span data-ttu-id="d75f9-154">Ниже приведен пример модуля форматирования JSON.</span><span class="sxs-lookup"><span data-stu-id="d75f9-154">Here is an example for the JSON formatter:</span></span>

[!code-console[Main](part-4/samples/sample12.cmd)]

<span data-ttu-id="d75f9-155">Вот модуль форматирования XML:</span><span class="sxs-lookup"><span data-stu-id="d75f9-155">Here is the XML formatter:</span></span>

[!code-xml[Main](part-4/samples/sample13.xml)]

<span data-ttu-id="d75f9-156">Одним из решений является использование DTO, который я опишу в следующем разделе.</span><span class="sxs-lookup"><span data-stu-id="d75f9-156">One solution is to use DTOs, which I describe in the next section.</span></span> <span data-ttu-id="d75f9-157">Кроме того, можно настроить модули форматирования JSON и XML для работы с циклами графов.</span><span class="sxs-lookup"><span data-stu-id="d75f9-157">Alternatively, you can configure the JSON and XML formatters to handle graph cycles.</span></span> <span data-ttu-id="d75f9-158">Дополнительные сведения см. в разделе [Обработка циклических ссылок на объекты](../../formats-and-model-binding/json-and-xml-serialization.md#handling_circular_object_references).</span><span class="sxs-lookup"><span data-stu-id="d75f9-158">For more information, see [Handling Circular Object References](../../formats-and-model-binding/json-and-xml-serialization.md#handling_circular_object_references).</span></span>

<span data-ttu-id="d75f9-159">В этом руководстве не требуется свойство навигации `Author.Book`, чтобы его можно было оставить.</span><span class="sxs-lookup"><span data-stu-id="d75f9-159">For this tutorial, you don't need the `Author.Book` navigation property, so you can leave it out.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="d75f9-160">[Назад](part-3.md)
> [Вперед](part-5.md)</span><span class="sxs-lookup"><span data-stu-id="d75f9-160">[Previous](part-3.md)
[Next](part-5.md)</span></span>
