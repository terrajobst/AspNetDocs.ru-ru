---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-2
title: Добавление моделей и контроллеров | Документация Майкрософт
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/16/2014
ms.assetid: 88908ff8-51a9-40eb-931c-a8139128b680
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-2
msc.type: authoredcontent
ms.openlocfilehash: 57dacda421968f341284d89c9a3ad80040c16e25
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78449190"
---
# <a name="add-models-and-controllers"></a><span data-ttu-id="c1ba3-102">Добавление моделей и контроллеров</span><span class="sxs-lookup"><span data-stu-id="c1ba3-102">Add Models and Controllers</span></span>

<span data-ttu-id="c1ba3-103">по [Майк Уоссон](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="c1ba3-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="c1ba3-104">Скачать завершенный проект</span><span class="sxs-lookup"><span data-stu-id="c1ba3-104">Download Completed Project</span></span>](https://github.com/MikeWasson/BookService)

<span data-ttu-id="c1ba3-105">В этом разделе вы добавите классы модели, определяющие сущности базы данных.</span><span class="sxs-lookup"><span data-stu-id="c1ba3-105">In this section, you will add model classes that define the database entities.</span></span> <span data-ttu-id="c1ba3-106">Затем вы добавите контроллеры веб-API, выполняющие операции CRUD с этими сущностями.</span><span class="sxs-lookup"><span data-stu-id="c1ba3-106">Then you will add Web API controllers that perform CRUD operations on those entities.</span></span>

## <a name="add-model-classes"></a><span data-ttu-id="c1ba3-107">Добавление классов модели</span><span class="sxs-lookup"><span data-stu-id="c1ba3-107">Add Model Classes</span></span>

<span data-ttu-id="c1ba3-108">В этом учебнике мы создадим базу данных с помощью подхода "Code First" к Entity Framework (EF).</span><span class="sxs-lookup"><span data-stu-id="c1ba3-108">In this tutorial, we'll create the database by using the "Code First" approach to Entity Framework (EF).</span></span> <span data-ttu-id="c1ba3-109">С помощью Code First вы пишете C# классы, соответствующие таблицам базы данных, и EF создает базу данных.</span><span class="sxs-lookup"><span data-stu-id="c1ba3-109">With Code First, you write C# classes that correspond to database tables, and EF creates the database.</span></span> <span data-ttu-id="c1ba3-110">(Дополнительные сведения см. в разделе [Entity Framework подходов к разработке](https://msdn.microsoft.com/library/ms178359%28v=vs.110%29.aspx#dbfmfcf).)</span><span class="sxs-lookup"><span data-stu-id="c1ba3-110">(For more information, see [Entity Framework Development Approaches](https://msdn.microsoft.com/library/ms178359%28v=vs.110%29.aspx#dbfmfcf).)</span></span>

<span data-ttu-id="c1ba3-111">Начнем с определения наших объектов домена как POCO (обычные объекты CLR).</span><span class="sxs-lookup"><span data-stu-id="c1ba3-111">We start by defining our domain objects as POCOs (plain-old CLR objects).</span></span> <span data-ttu-id="c1ba3-112">Мы создадим следующие POCO:</span><span class="sxs-lookup"><span data-stu-id="c1ba3-112">We will create the following POCOs:</span></span>

- <span data-ttu-id="c1ba3-113">Автор</span><span class="sxs-lookup"><span data-stu-id="c1ba3-113">Author</span></span>
- <span data-ttu-id="c1ba3-114">Book</span><span class="sxs-lookup"><span data-stu-id="c1ba3-114">Book</span></span>

<span data-ttu-id="c1ba3-115">В обозреватель решений щелкните правой кнопкой мыши папку модели.</span><span class="sxs-lookup"><span data-stu-id="c1ba3-115">In Solution Explorer, right click the Models folder.</span></span> <span data-ttu-id="c1ba3-116">Нажмите кнопку **Добавить**, а затем выберите **класс**.</span><span class="sxs-lookup"><span data-stu-id="c1ba3-116">Select **Add**, then select **Class**.</span></span> <span data-ttu-id="c1ba3-117">Назовите класс `Author`.</span><span class="sxs-lookup"><span data-stu-id="c1ba3-117">Name the class `Author`.</span></span>

![](part-2/_static/image1.png)

<span data-ttu-id="c1ba3-118">Замените весь стандартный код в Author.cs следующим кодом.</span><span class="sxs-lookup"><span data-stu-id="c1ba3-118">Replace all of the boilerplate code in Author.cs with the following code.</span></span>

[!code-csharp[Main](part-2/samples/sample1.cs)]

<span data-ttu-id="c1ba3-119">Добавьте еще один класс с именем `Book`и приведенный ниже код.</span><span class="sxs-lookup"><span data-stu-id="c1ba3-119">Add another class named `Book`, with the following code.</span></span>

[!code-csharp[Main](part-2/samples/sample2.cs)]

<span data-ttu-id="c1ba3-120">Entity Framework будут использовать эти модели для создания таблиц базы данных.</span><span class="sxs-lookup"><span data-stu-id="c1ba3-120">Entity Framework will use these models to create database tables.</span></span> <span data-ttu-id="c1ba3-121">Для каждой модели свойство `Id` станет первичным ключевым столбцом таблицы базы данных.</span><span class="sxs-lookup"><span data-stu-id="c1ba3-121">For each model, the `Id` property will become the primary key column of the database table.</span></span>

<span data-ttu-id="c1ba3-122">В классе Book `AuthorId` определяет внешний ключ в `Author` таблице.</span><span class="sxs-lookup"><span data-stu-id="c1ba3-122">In the Book class, the `AuthorId` defines a foreign key into the `Author` table.</span></span> <span data-ttu-id="c1ba3-123">(Для простоты я полагаю, что каждая книга имеет один автор.) Класс Book также содержит свойство навигации для связанного `Author`.</span><span class="sxs-lookup"><span data-stu-id="c1ba3-123">(For simplicity, I'm assuming that each book has a single author.) The book class also contains a navigation property to the related `Author`.</span></span> <span data-ttu-id="c1ba3-124">Для доступа к связанным `Author` в коде можно использовать свойство навигации.</span><span class="sxs-lookup"><span data-stu-id="c1ba3-124">You can use the navigation property to access the related `Author` in code.</span></span> <span data-ttu-id="c1ba3-125">Я говорю Подробнее о свойствах навигации в части 4, [обрабатывая связи сущностей](part-4.md).</span><span class="sxs-lookup"><span data-stu-id="c1ba3-125">I say more about navigation properties in part 4, [Handling Entity Relations](part-4.md).</span></span>

## <a name="add-web-api-controllers"></a><span data-ttu-id="c1ba3-126">Добавление контроллеров веб-API</span><span class="sxs-lookup"><span data-stu-id="c1ba3-126">Add Web API Controllers</span></span>

<span data-ttu-id="c1ba3-127">В этом разделе мы добавим контроллеры веб-API, поддерживающие операции CRUD (создание, чтение, обновление и удаление).</span><span class="sxs-lookup"><span data-stu-id="c1ba3-127">In this section, we'll add Web API controllers that support CRUD operations (create, read, update, and delete).</span></span> <span data-ttu-id="c1ba3-128">Контроллеры будут использовать Entity Framework для взаимодействия с уровнем базы данных.</span><span class="sxs-lookup"><span data-stu-id="c1ba3-128">The controllers will use Entity Framework to communicate with the database layer.</span></span>

<span data-ttu-id="c1ba3-129">Во-первых, можно удалить файловые контроллеры/объекта valuescontroller. cs.</span><span class="sxs-lookup"><span data-stu-id="c1ba3-129">First, you can delete the file Controllers/ValuesController.cs.</span></span> <span data-ttu-id="c1ba3-130">Этот файл содержит пример контроллера веб-API, но он не требуется для работы с этим руководством.</span><span class="sxs-lookup"><span data-stu-id="c1ba3-130">This file contains an example Web API controller, but you don't need it for this tutorial.</span></span>

![](part-2/_static/image2.png)

<span data-ttu-id="c1ba3-131">Затем постройте проект.</span><span class="sxs-lookup"><span data-stu-id="c1ba3-131">Next, build the project.</span></span> <span data-ttu-id="c1ba3-132">Формирование шаблонов веб-API использует отражение для поиска классов модели, поэтому ему требуется скомпилированная сборка.</span><span class="sxs-lookup"><span data-stu-id="c1ba3-132">The Web API scaffolding uses reflection to find the model classes, so it needs the compiled assembly.</span></span>

<span data-ttu-id="c1ba3-133">В обозреватель решений щелкните правой кнопкой мыши папку Controllers.</span><span class="sxs-lookup"><span data-stu-id="c1ba3-133">In Solution Explorer, right-click the Controllers folder.</span></span> <span data-ttu-id="c1ba3-134">Нажмите кнопку **Добавить**, а затем выберите **контроллер**.</span><span class="sxs-lookup"><span data-stu-id="c1ba3-134">Select **Add**, then select **Controller**.</span></span>

![](part-2/_static/image3.png)

<span data-ttu-id="c1ba3-135">В диалоговом окне **Добавление шаблона** выберите "контроллер веб-API 2 с действиями с помощью Entity Framework".</span><span class="sxs-lookup"><span data-stu-id="c1ba3-135">In the **Add Scaffold** dialog, select "Web API 2 Controller with actions, using Entity Framework".</span></span> <span data-ttu-id="c1ba3-136">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="c1ba3-136">Click **Add**.</span></span>

![](part-2/_static/image4.png)

<span data-ttu-id="c1ba3-137">В диалоговом окне **Добавление контроллера** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="c1ba3-137">In the **Add Controller** dialog, do the following:</span></span>

1. <span data-ttu-id="c1ba3-138">В раскрывающемся списке **класс модели** выберите класс `Author`.</span><span class="sxs-lookup"><span data-stu-id="c1ba3-138">In the **Model class** dropdown, select the `Author` class.</span></span> <span data-ttu-id="c1ba3-139">(Если вы не видите его в раскрывающемся списке, убедитесь, что вы создали проект.)</span><span class="sxs-lookup"><span data-stu-id="c1ba3-139">(If you don't see it listed in the dropdown, make sure that you built the project.)</span></span>
2. <span data-ttu-id="c1ba3-140">Установите флажок "использовать действия асинхронного контроллера".</span><span class="sxs-lookup"><span data-stu-id="c1ba3-140">Check "Use async controller actions".</span></span>
3. <span data-ttu-id="c1ba3-141">Оставьте имя контроллера &quot;Аусорсконтроллер&quot;.</span><span class="sxs-lookup"><span data-stu-id="c1ba3-141">Leave the controller name as &quot;AuthorsController&quot;.</span></span>
4. <span data-ttu-id="c1ba3-142">Нажмите кнопку со знаком «плюс» (+) рядом с **классом контекста данных**.</span><span class="sxs-lookup"><span data-stu-id="c1ba3-142">Click plus (+) button next to **Data Context Class**.</span></span>

![](part-2/_static/image5.png)

<span data-ttu-id="c1ba3-143">В диалоговом окне **новый контекст данных** оставьте имя по умолчанию и нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="c1ba3-143">In the **New Data Context** dialog, leave the default name and click **Add**.</span></span>

![](part-2/_static/image6.png)

<span data-ttu-id="c1ba3-144">Нажмите кнопку **Добавить** , чтобы завершить диалоговое окно **Добавление контроллера** .</span><span class="sxs-lookup"><span data-stu-id="c1ba3-144">Click **Add** to complete the **Add Controller** dialog.</span></span> <span data-ttu-id="c1ba3-145">В этом диалоговом окне в проект добавляются два класса:</span><span class="sxs-lookup"><span data-stu-id="c1ba3-145">The dialog adds two classes to your project:</span></span>

- <span data-ttu-id="c1ba3-146">`AuthorsController` определяет контроллер веб-API.</span><span class="sxs-lookup"><span data-stu-id="c1ba3-146">`AuthorsController` defines a Web API controller.</span></span> <span data-ttu-id="c1ba3-147">Контроллер реализует REST API, которые клиенты используют для выполнения операций CRUD в списке авторов.</span><span class="sxs-lookup"><span data-stu-id="c1ba3-147">The controller implements the REST API that clients use to perform CRUD operations on the list of authors.</span></span>
- <span data-ttu-id="c1ba3-148">`BookServiceContext` управляет объектами сущностей во время выполнения, включая заполнение объектов данными из базы данных, отслеживание изменений и сохранение данных в базе данных.</span><span class="sxs-lookup"><span data-stu-id="c1ba3-148">`BookServiceContext` manages entity objects during run time, which includes populating objects with data from a database, change tracking, and persisting data to the database.</span></span> <span data-ttu-id="c1ba3-149">Он наследует от `DbContext`.</span><span class="sxs-lookup"><span data-stu-id="c1ba3-149">It inherits from `DbContext`.</span></span>

![](part-2/_static/image7.png)

<span data-ttu-id="c1ba3-150">На этом этапе повторите сборку проекта.</span><span class="sxs-lookup"><span data-stu-id="c1ba3-150">At this point, build the project again.</span></span> <span data-ttu-id="c1ba3-151">Теперь выполните те же действия, чтобы добавить контроллер API для сущностей `Book`.</span><span class="sxs-lookup"><span data-stu-id="c1ba3-151">Now go through the same steps to add an API controller for `Book` entities.</span></span> <span data-ttu-id="c1ba3-152">На этот раз выберите `Book` для класса Model и выберите существующий класс `BookServiceContext` для класса контекста данных.</span><span class="sxs-lookup"><span data-stu-id="c1ba3-152">This time, select `Book` for the model class, and select the existing `BookServiceContext` class for the data context class.</span></span> <span data-ttu-id="c1ba3-153">(Не создавайте новый контекст данных.) Нажмите кнопку **Добавить** , чтобы добавить контроллер.</span><span class="sxs-lookup"><span data-stu-id="c1ba3-153">(Don't create a new data context.) Click **Add** to add the controller.</span></span>

![](part-2/_static/image8.png)

> [!div class="step-by-step"]
> <span data-ttu-id="c1ba3-154">[Назад](part-1.md)
> [Вперед](part-3.md)</span><span class="sxs-lookup"><span data-stu-id="c1ba3-154">[Previous](part-1.md)
[Next](part-3.md)</span></span>
