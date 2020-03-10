---
uid: mvc/overview/getting-started/getting-started-with-ef-using-mvc/async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application
title: Учебник. Использование асинхронных и хранимых процедур с EF в приложении ASP.NET MVC
description: В этом учебнике показано, как реализовать асинхронную модель программирования и узнать, как использовать хранимые процедуры.
author: tdykstra
ms.author: riande
ms.date: 01/18/2019
ms.topic: tutorial
ms.assetid: 27d110fc-d1b7-4628-a763-26f1e6087549
msc.legacyurl: /mvc/overview/getting-started/getting-started-with-ef-using-mvc/async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 5612f2f25d06feb904a205505ed8f048d2263266
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78471390"
---
# <a name="tutorial-use-async-and-stored-procedures-with-ef-in-an-aspnet-mvc-app"></a><span data-ttu-id="8324b-103">Учебник. Использование асинхронных и хранимых процедур с EF в приложении ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="8324b-103">Tutorial: Use async and stored procedures with EF in an ASP.NET MVC App</span></span>

<span data-ttu-id="8324b-104">В предыдущих руководствах вы узнали, как считывать и обновлять данные с помощью синхронной модели программирования.</span><span class="sxs-lookup"><span data-stu-id="8324b-104">In earlier tutorials you learned how to read and update data using the synchronous programming model.</span></span> <span data-ttu-id="8324b-105">В этом учебнике показано, как реализовать асинхронную модель программирования.</span><span class="sxs-lookup"><span data-stu-id="8324b-105">In this tutorial you see how to implement the asynchronous programming model.</span></span> <span data-ttu-id="8324b-106">Асинхронный код может помочь приложению работать лучше, поскольку он обеспечивает более эффективное использование ресурсов сервера.</span><span class="sxs-lookup"><span data-stu-id="8324b-106">Asynchronous code can help an application perform better because it makes better use of server resources.</span></span>

<span data-ttu-id="8324b-107">В этом учебнике вы также узнаете, как использовать хранимые процедуры для операций вставки, обновления и удаления сущности.</span><span class="sxs-lookup"><span data-stu-id="8324b-107">In this tutorial you also see how to use stored procedures for insert, update, and delete operations on an entity.</span></span>

<span data-ttu-id="8324b-108">Наконец, вы повторно развертываете приложение в Azure, а также все изменения базы данных, реализованные с момента первого развертывания.</span><span class="sxs-lookup"><span data-stu-id="8324b-108">Finally, you redeploy the application to Azure, along with all of the database changes that you've implemented since the first time you deployed.</span></span>

<span data-ttu-id="8324b-109">На следующих рисунках изображены некоторые из страниц, с которыми вы будете работать.</span><span class="sxs-lookup"><span data-stu-id="8324b-109">The following illustrations show some of the pages that you'll work with.</span></span>

![Страница «отделы»](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)

![Создать отдел](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image2.png)

<span data-ttu-id="8324b-112">Изучив это руководство, вы:</span><span class="sxs-lookup"><span data-stu-id="8324b-112">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="8324b-113">Дополнительные сведения о асинхронном коде</span><span class="sxs-lookup"><span data-stu-id="8324b-113">Learn about asynchronous code</span></span>
> * <span data-ttu-id="8324b-114">Создание контроллера отдела</span><span class="sxs-lookup"><span data-stu-id="8324b-114">Create a Department controller</span></span>
> * <span data-ttu-id="8324b-115">Использование хранимых процедур</span><span class="sxs-lookup"><span data-stu-id="8324b-115">Use stored procedures</span></span>
> * <span data-ttu-id="8324b-116">Развертывание в Azure</span><span class="sxs-lookup"><span data-stu-id="8324b-116">Deploy to Azure</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8324b-117">предварительные требования</span><span class="sxs-lookup"><span data-stu-id="8324b-117">Prerequisites</span></span>

* [<span data-ttu-id="8324b-118">Обновление связанных данных</span><span class="sxs-lookup"><span data-stu-id="8324b-118">Updating Related Data</span></span>](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)

## <a name="why-use-asynchronous-code"></a><span data-ttu-id="8324b-119">Зачем использовать асинхронный код</span><span class="sxs-lookup"><span data-stu-id="8324b-119">Why use asynchronous code</span></span>

<span data-ttu-id="8324b-120">Веб-сервер имеет ограниченное число потоков, поэтому при высокой загрузке могут использоваться все доступные потоки.</span><span class="sxs-lookup"><span data-stu-id="8324b-120">A web server has a limited number of threads available, and in high load situations all of the available threads might be in use.</span></span> <span data-ttu-id="8324b-121">В таких случаях сервер не может обрабатывать новые запросы до тех пор, пока не будут высвобождены потоки.</span><span class="sxs-lookup"><span data-stu-id="8324b-121">When that happens, the server can't process new requests until the threads are freed up.</span></span> <span data-ttu-id="8324b-122">В синхронном коде многие потоки могут быть заняты, не выполняя при этом какие-либо операции и ожидая завершения ввода-вывода.</span><span class="sxs-lookup"><span data-stu-id="8324b-122">With synchronous code, many threads may be tied up while they aren't actually doing any work because they're waiting for I/O to complete.</span></span> <span data-ttu-id="8324b-123">В асинхронном коде в то время, когда процесс ожидает завершения ввода-вывода, его поток высвобождается и может использоваться сервером для обработки других запросов.</span><span class="sxs-lookup"><span data-stu-id="8324b-123">With asynchronous code, when a process is waiting for I/O to complete, its thread is freed up for the server to use for processing other requests.</span></span> <span data-ttu-id="8324b-124">В результате асинхронный код позволяет более эффективно использовать ресурсы сервера, а сервер — обрабатывать больше трафика без задержек.</span><span class="sxs-lookup"><span data-stu-id="8324b-124">As a result, asynchronous code enables server resources to be use more efficiently, and the server is enabled to handle more traffic without delays.</span></span>

<span data-ttu-id="8324b-125">В более ранних версиях .NET написание и тестирование асинхронного кода было сложным, подвержено ошибкам и сложно отлаживать.</span><span class="sxs-lookup"><span data-stu-id="8324b-125">In earlier versions of .NET, writing and testing asynchronous code was complex, error prone, and hard to debug.</span></span> <span data-ttu-id="8324b-126">В .NET 4,5 написание, тестирование и отладка асинхронного кода настолько проще, что обычно следует писать асинхронный код, если нет причины отсутствия.</span><span class="sxs-lookup"><span data-stu-id="8324b-126">In .NET 4.5, writing, testing, and debugging asynchronous code is so much easier that you should generally write asynchronous code unless you have a reason not to.</span></span> <span data-ttu-id="8324b-127">Асинхронный код приводит к небольшому излишнему объему издержек, но в случае с низким трафиком снижается производительность, а в случае с большим трафиком потенциальное улучшение производительности является значительным.</span><span class="sxs-lookup"><span data-stu-id="8324b-127">Asynchronous code does introduce a small amount of overhead, but for low traffic situations the performance hit is negligible, while for high traffic situations, the potential performance improvement is substantial.</span></span>

<span data-ttu-id="8324b-128">Дополнительные сведения об асинхронном программировании см. [в разделе Использование асинхронной поддержки .NET 4.5 во избежание блокирующих вызовов](../../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices.md#async).</span><span class="sxs-lookup"><span data-stu-id="8324b-128">For more information about asynchronous programming, see [Use .NET 4.5's async support to avoid blocking calls](../../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices.md#async).</span></span>

## <a name="create-department-controller"></a><span data-ttu-id="8324b-129">Создание контроллера отдела</span><span class="sxs-lookup"><span data-stu-id="8324b-129">Create Department controller</span></span>

<span data-ttu-id="8324b-130">Создайте контроллер отдела так же, как и для предыдущих контроллеров, за исключением этого времени, установите флажок **использовать асинхронные действия контроллера** .</span><span class="sxs-lookup"><span data-stu-id="8324b-130">Create a Department controller the same way you did the earlier controllers, except this time select the **Use async controller actions** check box.</span></span>

<span data-ttu-id="8324b-131">Следующие элементы показывают, что было добавлено в синхронный код для метода `Index`, чтобы сделать его асинхронным:</span><span class="sxs-lookup"><span data-stu-id="8324b-131">The following highlights show what was added to the synchronous code for the `Index` method to make it asynchronous:</span></span>

[!code-csharp[Main](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs?highlight=1,4)]

<span data-ttu-id="8324b-132">Для выполнения запроса Entity Frameworkной базы данных в асинхронном режиме были применены четыре изменения:</span><span class="sxs-lookup"><span data-stu-id="8324b-132">Four changes were applied to enable the Entity Framework database query to execute asynchronously:</span></span>

- <span data-ttu-id="8324b-133">Метод помечается ключевым словом `async`, которое указывает компилятору создавать обратные вызовы для частей тела метода и автоматически создавать возвращаемый объект `Task<ActionResult>`.</span><span class="sxs-lookup"><span data-stu-id="8324b-133">The method is marked with the `async` keyword, which tells the compiler to generate callbacks for parts of the method body and to automatically create the `Task<ActionResult>` object that is returned.</span></span>
- <span data-ttu-id="8324b-134">Тип возвращаемого значения изменен с `ActionResult` на `Task<ActionResult>`.</span><span class="sxs-lookup"><span data-stu-id="8324b-134">The return type was changed from `ActionResult` to `Task<ActionResult>`.</span></span> <span data-ttu-id="8324b-135">Тип `Task<T>` представляет текущую работу с результатом типа `T`.</span><span class="sxs-lookup"><span data-stu-id="8324b-135">The `Task<T>` type represents ongoing work with a result of type `T`.</span></span>
- <span data-ttu-id="8324b-136">Ключевое слово `await` было применено к вызову веб-службы.</span><span class="sxs-lookup"><span data-stu-id="8324b-136">The `await` keyword was applied to the web service call.</span></span> <span data-ttu-id="8324b-137">Когда компилятор видит это ключевое слово, в фоновом режиме он разделяет метод на две части.</span><span class="sxs-lookup"><span data-stu-id="8324b-137">When the compiler sees this keyword, behind the scenes it splits the method into two parts.</span></span> <span data-ttu-id="8324b-138">Первая часть завершается операцией, которая запускается асинхронно.</span><span class="sxs-lookup"><span data-stu-id="8324b-138">The first part ends with the operation that is started asynchronously.</span></span> <span data-ttu-id="8324b-139">Вторая часть помещается в метод обратного вызова, который вызывается по завершении операции.</span><span class="sxs-lookup"><span data-stu-id="8324b-139">The second part is put into a callback method that is called when the operation completes.</span></span>
- <span data-ttu-id="8324b-140">Вызвана асинхронная версия метода расширения `ToList`.</span><span class="sxs-lookup"><span data-stu-id="8324b-140">The asynchronous version of the `ToList` extension method was called.</span></span>

<span data-ttu-id="8324b-141">Почему `departments.ToList` оператор изменен, но не `departments = db.Departments`?</span><span class="sxs-lookup"><span data-stu-id="8324b-141">Why is the `departments.ToList` statement modified but not the `departments = db.Departments` statement?</span></span> <span data-ttu-id="8324b-142">Причина заключается в том, что только инструкции, вызывающие отправку запросов или команд в базу данных, выполняются асинхронно.</span><span class="sxs-lookup"><span data-stu-id="8324b-142">The reason is that only statements that cause queries or commands to be sent to the database are executed asynchronously.</span></span> <span data-ttu-id="8324b-143">Инструкция `departments = db.Departments` настраивает запрос, но запрос не выполняется, пока не будет вызван метод `ToList`.</span><span class="sxs-lookup"><span data-stu-id="8324b-143">The `departments = db.Departments` statement sets up a query but the query is not executed until the `ToList` method is called.</span></span> <span data-ttu-id="8324b-144">Поэтому асинхронно выполняется только метод `ToList`.</span><span class="sxs-lookup"><span data-stu-id="8324b-144">Therefore, only the `ToList` method is executed asynchronously.</span></span>

<span data-ttu-id="8324b-145">В методе `Details` и `HttpGet` `Edit` и `Delete` метод `Find` — это тот, который вызывает отправку запроса в базу данных, так что это метод, который выполняется асинхронно:</span><span class="sxs-lookup"><span data-stu-id="8324b-145">In the `Details` method and the `HttpGet` `Edit` and `Delete` methods, the `Find` method is the one that causes a query to be sent to the database, so that's the method that gets executed asynchronously:</span></span>

[!code-csharp[Main](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs?highlight=7)]

<span data-ttu-id="8324b-146">В методах `Create`, `HttpPost Edit`и `DeleteConfirmed` это вызов метода `SaveChanges`, который вызывает выполнение команды, а не инструкции, такие как `db.Departments.Add(department)`, которые вызывают изменение только сущностей в памяти.</span><span class="sxs-lookup"><span data-stu-id="8324b-146">In the `Create`, `HttpPost Edit`, and `DeleteConfirmed` methods, it is the `SaveChanges` method call that causes a command to be executed, not statements such as `db.Departments.Add(department)` which only cause entities in memory to be modified.</span></span>

[!code-csharp[Main](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cs?highlight=6)]

<span data-ttu-id="8324b-147">Откройте *виевс\департмент\индекс.кштмл*и замените код шаблона следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="8324b-147">Open *Views\Department\Index.cshtml*, and replace the template code with the following code:</span></span>

[!code-cshtml[Main](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cshtml?highlight=3,5,20-22,36-38)]

<span data-ttu-id="8324b-148">Этот код изменяет заголовок с index на Departments, перемещает имя администратора вправо и предоставляет полное имя администратора.</span><span class="sxs-lookup"><span data-stu-id="8324b-148">This code changes the title from Index to Departments, moves the Administrator name to the right, and provides the full name of the administrator.</span></span>

<span data-ttu-id="8324b-149">В представлениях создание, удаление, сведения и изменение измените заголовок поля `InstructorID` на "Администратор" так же, как и в поле "название отдела" в представлениях курсов.</span><span class="sxs-lookup"><span data-stu-id="8324b-149">In the Create, Delete, Details, and Edit views, change the caption for the `InstructorID` field to "Administrator" the same way you changed the department name field to "Department" in the Course views.</span></span>

<span data-ttu-id="8324b-150">В представлениях создание и изменение используйте следующий код:</span><span class="sxs-lookup"><span data-stu-id="8324b-150">In the Create and Edit views use the following code:</span></span>

[!code-cshtml[Main](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cshtml)]

<span data-ttu-id="8324b-151">В представлениях удаление и сведения используйте следующий код:</span><span class="sxs-lookup"><span data-stu-id="8324b-151">In the Delete and Details views use the following code:</span></span>

[!code-cshtml[Main](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.cshtml)]

<span data-ttu-id="8324b-152">Запустите приложение и перейдите на вкладку **Departments (подразделения** ).</span><span class="sxs-lookup"><span data-stu-id="8324b-152">Run the application, and click the **Departments** tab.</span></span>

<span data-ttu-id="8324b-153">Все работает так же, как и на других контроллерах, но в этом контроллере все запросы SQL выполняются асинхронно.</span><span class="sxs-lookup"><span data-stu-id="8324b-153">Everything works the same as in the other controllers, but in this controller all of the SQL queries are executing asynchronously.</span></span>

<span data-ttu-id="8324b-154">При использовании асинхронного программирования с Entity Framework необходимо учитывать некоторые моменты.</span><span class="sxs-lookup"><span data-stu-id="8324b-154">Some things to be aware of when you are using asynchronous programming with the Entity Framework:</span></span>

- <span data-ttu-id="8324b-155">Асинхронный код не является потокобезопасным.</span><span class="sxs-lookup"><span data-stu-id="8324b-155">The async code is not thread safe.</span></span> <span data-ttu-id="8324b-156">Иными словами, не пытайтесь выполнять несколько операций параллельно, используя один и тот же экземпляр контекста.</span><span class="sxs-lookup"><span data-stu-id="8324b-156">In other words, in other words, don't try to do multiple operations in parallel using the same context instance.</span></span>
- <span data-ttu-id="8324b-157">Если вы хотите использовать преимущества в производительности, которые обеспечивает асинхронный код, убедитесь, что все используемые пакеты библиотек (например, для разбиения на страницы) также используют асинхронный код при вызове любых методов Entity Framework, выполняющих запросы к базе данных.</span><span class="sxs-lookup"><span data-stu-id="8324b-157">If you want to take advantage of the performance benefits of async code, make sure that any library packages that you're using (such as for paging), also use async if they call any Entity Framework methods that cause queries to be sent to the database.</span></span>

## <a name="use-stored-procedures"></a><span data-ttu-id="8324b-158">Использование хранимых процедур</span><span class="sxs-lookup"><span data-stu-id="8324b-158">Use stored procedures</span></span>

<span data-ttu-id="8324b-159">Некоторые разработчики и администраторы баз данных предпочитают использовать хранимые процедуры для доступа к базам данным.</span><span class="sxs-lookup"><span data-stu-id="8324b-159">Some developers and DBAs prefer to use stored procedures for database access.</span></span> <span data-ttu-id="8324b-160">В более ранних версиях Entity Framework можно получить данные с помощью хранимой процедуры, [выполнив необработанный SQL-запрос](advanced-entity-framework-scenarios-for-an-mvc-web-application.md), но нельзя указать EF использовать хранимые процедуры для операций обновления.</span><span class="sxs-lookup"><span data-stu-id="8324b-160">In earlier versions of Entity Framework you can retrieve data using a stored procedure by [executing a raw SQL query](advanced-entity-framework-scenarios-for-an-mvc-web-application.md), but you can't instruct EF to use stored procedures for update operations.</span></span> <span data-ttu-id="8324b-161">В EF 6 можно легко настроить Code First для использования хранимых процедур.</span><span class="sxs-lookup"><span data-stu-id="8324b-161">In EF 6 it's easy to configure Code First to use stored procedures.</span></span>

1. <span data-ttu-id="8324b-162">В *дал\счулконтекст.КС*Добавьте выделенный код в метод `OnModelCreating`.</span><span class="sxs-lookup"><span data-stu-id="8324b-162">In *DAL\SchoolContext.cs*, add the highlighted code to the `OnModelCreating` method.</span></span>

    [!code-csharp[Main](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cs?highlight=9)]

    <span data-ttu-id="8324b-163">Этот код указывает Entity Framework использовать хранимые процедуры для операций вставки, обновления и удаления в сущности `Department`.</span><span class="sxs-lookup"><span data-stu-id="8324b-163">This code instructs Entity Framework to use stored procedures for insert, update, and delete operations on the `Department` entity.</span></span>
2. <span data-ttu-id="8324b-164">В консоли Управление пакетами введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="8324b-164">In Package Manage Console, enter the following command:</span></span>

    `add-migration DepartmentSP`

    <span data-ttu-id="8324b-165">Откройте *миграцию\\&lt;метку времени&gt;\_DepartmentSP.CS* , чтобы увидеть код в методе `Up`, который создает хранимые процедуры INSERT, Update и DELETE:</span><span class="sxs-lookup"><span data-stu-id="8324b-165">Open *Migrations\\&lt;timestamp&gt;\_DepartmentSP.cs* to see the code in the `Up` method that creates Insert, Update, and Delete stored procedures:</span></span>

    [!code-csharp[Main](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.cs?highlight=3-4,26-27,42-43)]
3. <span data-ttu-id="8324b-166">В консоли Управление пакетами введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="8324b-166">In Package Manage Console, enter the following command:</span></span>

     `update-database`
4. <span data-ttu-id="8324b-167">Запустите приложение в режиме отладки, перейдите на вкладку **подразделения** и нажмите кнопку **создать**.</span><span class="sxs-lookup"><span data-stu-id="8324b-167">Run the application in debug mode, click the **Departments** tab, and then click **Create New**.</span></span>
5. <span data-ttu-id="8324b-168">Введите данные для нового отдела и нажмите кнопку **создать**.</span><span class="sxs-lookup"><span data-stu-id="8324b-168">Enter data for a new department, and then click **Create**.</span></span>

6. <span data-ttu-id="8324b-169">В Visual Studio просмотрите журналы в окне **вывод** , чтобы увидеть, что для вставки новой строки отдела использовалась хранимая процедура.</span><span class="sxs-lookup"><span data-stu-id="8324b-169">In Visual Studio, look at the logs in the **Output** window to see that a stored procedure was used to insert the new Department row.</span></span>

     ![Пакет обновления для отдела вставки](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image6.png)

<span data-ttu-id="8324b-171">Code First создает имена хранимых процедур по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="8324b-171">Code First creates default stored procedure names.</span></span> <span data-ttu-id="8324b-172">При использовании существующей базы данных может потребоваться настроить имена хранимых процедур, чтобы использовать хранимые процедуры, уже определенные в базе данных.</span><span class="sxs-lookup"><span data-stu-id="8324b-172">If you are using an existing database, you might need to customize the stored procedure names in order to use stored procedures already defined in the database.</span></span> <span data-ttu-id="8324b-173">Сведения о том, как это сделать, см. в разделе [Entity Framework Code First вставки, обновления и удаления хранимых процедур](https://msdn.microsoft.com/data/dn468673).</span><span class="sxs-lookup"><span data-stu-id="8324b-173">For information about how to do that, see [Entity Framework Code First Insert/Update/Delete Stored Procedures](https://msdn.microsoft.com/data/dn468673).</span></span>

<span data-ttu-id="8324b-174">Если необходимо настроить создаваемые хранимые процедуры, можно изменить сформированный код для метода миграции `Up` метод, который создает хранимую процедуру.</span><span class="sxs-lookup"><span data-stu-id="8324b-174">If you want to customize what generated stored procedures do, you can edit the scaffolded code for the migrations `Up` method that creates the stored procedure.</span></span> <span data-ttu-id="8324b-175">Таким образом, изменения отражаются при выполнении миграции и будут применены к рабочей базе данных, когда миграция выполняется автоматически в рабочей среде после развертывания.</span><span class="sxs-lookup"><span data-stu-id="8324b-175">That way your changes are reflected whenever that migration is run and will be applied to your production database when migrations runs automatically in production after deployment.</span></span>

<span data-ttu-id="8324b-176">Если вы хотите изменить существующую хранимую процедуру, созданную при предыдущей миграции, можно использовать команду Add-Migration, чтобы создать пустую миграцию, а затем вручную написать код, который вызывает метод [алтерсторедпроцедуре](https://msdn.microsoft.com/library/system.data.entity.migrations.dbmigration.alterstoredprocedure.aspx) .</span><span class="sxs-lookup"><span data-stu-id="8324b-176">If you want to change an existing stored procedure that was created in a previous migration, you can use the Add-Migration command to generate a blank migration, and then manually write code that calls the [AlterStoredProcedure](https://msdn.microsoft.com/library/system.data.entity.migrations.dbmigration.alterstoredprocedure.aspx) method.</span></span>

## <a name="deploy-to-azure"></a><span data-ttu-id="8324b-177">Развертывание в Azure</span><span class="sxs-lookup"><span data-stu-id="8324b-177">Deploy to Azure</span></span>

<span data-ttu-id="8324b-178">Для работы с этим разделом необходимо завершить необязательное **развертывание приложения в Azure** в руководстве по [миграции и развертыванию](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application.md) этой серии.</span><span class="sxs-lookup"><span data-stu-id="8324b-178">This section requires you to have completed the optional **Deploying the app to Azure** section in the [Migrations and Deployment](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application.md) tutorial of this series.</span></span> <span data-ttu-id="8324b-179">Если возникли ошибки миграции, которые вы разрешили, удалив базу данных в локальном проекте, пропустите этот раздел.</span><span class="sxs-lookup"><span data-stu-id="8324b-179">If you had migrations errors that you resolved by deleting the database in your local project, skip this section.</span></span>

1. <span data-ttu-id="8324b-180">В Visual Studio щелкните правой кнопкой мыши проект в **обозревателе решений** и выберите **Опубликовать** в контекстном меню.</span><span class="sxs-lookup"><span data-stu-id="8324b-180">In Visual Studio, right-click the project in **Solution Explorer** and select **Publish** from the context menu.</span></span>
2. <span data-ttu-id="8324b-181">Щелкните **Опубликовать**.</span><span class="sxs-lookup"><span data-stu-id="8324b-181">Click **Publish**.</span></span>

    <span data-ttu-id="8324b-182">Visual Studio развертывает приложение в Azure, и приложение откроется в браузере по умолчанию, работающем в Azure.</span><span class="sxs-lookup"><span data-stu-id="8324b-182">Visual Studio deploys the application to Azure, and the application opens in your default browser, running in Azure.</span></span>
3. <span data-ttu-id="8324b-183">Протестируйте приложение, чтобы проверить его работоспособность.</span><span class="sxs-lookup"><span data-stu-id="8324b-183">Test the application to verify it's working.</span></span>

    <span data-ttu-id="8324b-184">При первом запуске страницы, обращающейся к базе данных, Entity Framework выполняет все миграции `Up` методы, необходимые для обновления базы данных до текущей модели данных.</span><span class="sxs-lookup"><span data-stu-id="8324b-184">The first time you run a page that accesses the database, the Entity Framework runs all of the migrations `Up` methods required to bring the database up to date with the current data model.</span></span> <span data-ttu-id="8324b-185">Теперь можно использовать все веб-страницы, добавленные со времени последнего развертывания, включая страницы Отдела, добавленные в этом руководстве.</span><span class="sxs-lookup"><span data-stu-id="8324b-185">You can now use all of the web pages that you added since the last time you deployed, including the Department pages that you added in this tutorial.</span></span>

## <a name="get-the-code"></a><span data-ttu-id="8324b-186">Получение кода</span><span class="sxs-lookup"><span data-stu-id="8324b-186">Get the code</span></span>

[<span data-ttu-id="8324b-187">Скачать завершенный проект</span><span class="sxs-lookup"><span data-stu-id="8324b-187">Download the Completed Project</span></span>](https://webpifeed.blob.core.windows.net/webpifeed/Partners/ASP.NET%20MVC%20Application%20Using%20Entity%20Framework%20Code%20First.zip)

## <a name="additional-resources"></a><span data-ttu-id="8324b-188">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="8324b-188">Additional resources</span></span>

<span data-ttu-id="8324b-189">Ссылки на другие ресурсы Entity Framework можно найти в [ресурсах, рекомендуемых для доступа к данным ASP.NET](../../../../whitepapers/aspnet-data-access-content-map.md).</span><span class="sxs-lookup"><span data-stu-id="8324b-189">Links to other Entity Framework resources can be found in the [ASP.NET Data Access - Recommended Resources](../../../../whitepapers/aspnet-data-access-content-map.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="8324b-190">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="8324b-190">Next steps</span></span>

<span data-ttu-id="8324b-191">Изучив это руководство, вы:</span><span class="sxs-lookup"><span data-stu-id="8324b-191">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="8324b-192">Общие сведения о асинхронном коде</span><span class="sxs-lookup"><span data-stu-id="8324b-192">Learned about asynchronous code</span></span>
> * <span data-ttu-id="8324b-193">Создан контроллер отдела</span><span class="sxs-lookup"><span data-stu-id="8324b-193">Created a Department controller</span></span>
> * <span data-ttu-id="8324b-194">Используемые хранимые процедуры</span><span class="sxs-lookup"><span data-stu-id="8324b-194">Used stored procedures</span></span>
> * <span data-ttu-id="8324b-195">Развернуто в Azure</span><span class="sxs-lookup"><span data-stu-id="8324b-195">Deployed to Azure</span></span>

<span data-ttu-id="8324b-196">Перейдите к следующей статье, чтобы узнать, как справляться с конфликтами, когда несколько пользователей одновременно обновляют одну и ту же сущность.</span><span class="sxs-lookup"><span data-stu-id="8324b-196">Advance to the next article to learn how to handle conflicts when multiple users update the same entity at the same time.</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="8324b-197">Обработка параллелизма</span><span class="sxs-lookup"><span data-stu-id="8324b-197">Handling concurrency</span></span>](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md)
