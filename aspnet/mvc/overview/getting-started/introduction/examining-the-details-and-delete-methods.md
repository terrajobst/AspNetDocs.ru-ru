---
uid: mvc/overview/getting-started/introduction/examining-the-details-and-delete-methods
title: Изучение методов Details и Delete | Документация Майкрософт
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 03/26/2015
ms.assetid: f1d2a916-626c-4a54-8df4-77e6b9fff355
msc.legacyurl: /mvc/overview/getting-started/introduction/examining-the-details-and-delete-methods
msc.type: authoredcontent
ms.openlocfilehash: c68d7a022f14bdcf2a08696691d2b6ef888a8d54
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57064941"
---
<a name="examining-the-details-and-delete-methods"></a><span data-ttu-id="9f516-102">Изучение методов Details и Delete</span><span class="sxs-lookup"><span data-stu-id="9f516-102">Examining the Details and Delete Methods</span></span>
====================
<span data-ttu-id="9f516-103">по [Рик Андерсон]((https://twitter.com/RickAndMSFT))</span><span class="sxs-lookup"><span data-stu-id="9f516-103">by [Rick Anderson]((https://twitter.com/RickAndMSFT))</span></span>

[!INCLUDE [Tutorial Note](sample/code-location.md)]

<span data-ttu-id="9f516-104">В этой части руководства вы рассмотрите автоматически созданный `Details` и `Delete` методы.</span><span class="sxs-lookup"><span data-stu-id="9f516-104">In this part of the tutorial, you'll examine the automatically generated `Details` and `Delete` methods.</span></span>

## <a name="examining-the-details-and-delete-methods"></a><span data-ttu-id="9f516-105">Изучение методов Details и Delete</span><span class="sxs-lookup"><span data-stu-id="9f516-105">Examining the Details and Delete Methods</span></span>

<span data-ttu-id="9f516-106">Откройте `Movie` контроллера и изучите `Details` метод.</span><span class="sxs-lookup"><span data-stu-id="9f516-106">Open the `Movie` controller and examine the `Details` method.</span></span>

![](examining-the-details-and-delete-methods/_static/image1.png)

[!code-csharp[Main](examining-the-details-and-delete-methods/samples/sample1.cs)]

<span data-ttu-id="9f516-107">Подсистема формирования шаблонов MVC, созданная этим методом действия добавляет комментарий, показывающий HTTP-запроса, который вызывает метод.</span><span class="sxs-lookup"><span data-stu-id="9f516-107">The MVC scaffolding engine that created this action method adds a comment showing a HTTP request that invokes the method.</span></span> <span data-ttu-id="9f516-108">В данном случае это `GET` запроса, состоящая из трех сегментов URL-адрес, `Movies` контроллера, `Details` метод и `ID` значение.</span><span class="sxs-lookup"><span data-stu-id="9f516-108">In this case it's a `GET` request with three URL segments, the `Movies` controller, the `Details` method and a `ID` value.</span></span>

<span data-ttu-id="9f516-109">Код сначала облегчает поиск данных с помощью `Find` метод.</span><span class="sxs-lookup"><span data-stu-id="9f516-109">Code First makes it easy to search for data using the `Find` method.</span></span> <span data-ttu-id="9f516-110">Это функция важный элемент обеспечения безопасности, встроенной в метод является то, что код проверяет, `Find` метод обнаружил фильм, прежде чем код пытается выполнить любые действия с его.</span><span class="sxs-lookup"><span data-stu-id="9f516-110">An important security feature built into the method is that the code verifies that the `Find` method has found a movie before the code tries to do anything with it.</span></span> <span data-ttu-id="9f516-111">Например, злоумышленник может внести ошибки на сайт путем изменения созданного ссылками из URL-адрес `http://localhost:xxxx/Movies/Details/1` в нечто подобное `http://localhost:xxxx/Movies/Details/12345` (или любое другое значение, которое не представляет фактический фильм).</span><span class="sxs-lookup"><span data-stu-id="9f516-111">For example, a hacker could introduce errors into the site by changing the URL created by the links from `http://localhost:xxxx/Movies/Details/1` to something like `http://localhost:xxxx/Movies/Details/12345` (or some other value that doesn't represent an actual movie).</span></span> <span data-ttu-id="9f516-112">Если вы не проверили наличие фильма со значением null, фильма со значением null приведет к ошибке базы данных.</span><span class="sxs-lookup"><span data-stu-id="9f516-112">If you did not check for a null movie, a null movie would result in a database error.</span></span>

<span data-ttu-id="9f516-113">Просмотрите методы `Delete` и `DeleteConfirmed`.</span><span class="sxs-lookup"><span data-stu-id="9f516-113">Examine the `Delete` and `DeleteConfirmed` methods.</span></span>

[!code-csharp[Main](examining-the-details-and-delete-methods/samples/sample2.cs?highlight=17)]

<span data-ttu-id="9f516-114">Обратите внимание, что HTTP GET `Delete` метод не удаляет указанный фильм, он возвращает представление фильма, где вы сможете отправить (`HttpPost`) удаление.</span><span class="sxs-lookup"><span data-stu-id="9f516-114">Note that the HTTP GET `Delete` method doesn't delete the specified movie, it returns a view of the movie where you can submit (`HttpPost`) the deletion.</span></span> <span data-ttu-id="9f516-115">Выполнение операции удаления в ответ на запрос GET (или выполнение операции редактирования, создания или любой другой операции, изменяющей данные) открывает брешь в системе безопасности.</span><span class="sxs-lookup"><span data-stu-id="9f516-115">Performing a delete operation in response to a GET request (or for that matter, performing an edit operation, create operation, or any other operation that changes data) opens up a security hole.</span></span> <span data-ttu-id="9f516-116">Дополнительные сведения об этом см. запись в блоге Стивен Вальтер [46 совет # ASP.NET MVC — не использовать ссылки, удалить, так как они создают бреши в системе безопасности](http://stephenwalther.com/blog/archive/2009/01/21/asp.net-mvc-tip-46-ndash-donrsquot-use-delete-links-because.aspx).</span><span class="sxs-lookup"><span data-stu-id="9f516-116">For more information about this, see Stephen Walther's blog entry [ASP.NET MVC Tip #46 — Don't use Delete Links because they create Security Holes](http://stephenwalther.com/blog/archive/2009/01/21/asp.net-mvc-tip-46-ndash-donrsquot-use-delete-links-because.aspx).</span></span>

<span data-ttu-id="9f516-117">Метод `HttpPost`, который удаляет данные, называется `DeleteConfirmed`, поэтому метод HTTP POST обладает уникальной сигнатурой или именем.</span><span class="sxs-lookup"><span data-stu-id="9f516-117">The `HttpPost` method that deletes the data is named `DeleteConfirmed` to give the HTTP POST method a unique signature or name.</span></span> <span data-ttu-id="9f516-118">Ниже приведены сигнатуры двух методов:</span><span class="sxs-lookup"><span data-stu-id="9f516-118">The two method signatures are shown below:</span></span>

[!code-csharp[Main](examining-the-details-and-delete-methods/samples/sample3.cs)]

<span data-ttu-id="9f516-119">Требуется, чтобы в среде CLR перегруженные методы имели уникальную сигнатуру параметров (то же имя метода, но другой список параметров).</span><span class="sxs-lookup"><span data-stu-id="9f516-119">The common language runtime (CLR) requires overloaded methods to have a unique parameter signature (same method name but different list of parameters).</span></span> <span data-ttu-id="9f516-120">Однако здесь необходимы два метода Delete — один для GET--и один для POST, имеют такой же сигнатурой параметров.</span><span class="sxs-lookup"><span data-stu-id="9f516-120">However, here you need two Delete methods -- one for GET and one for POST -- that both have the same parameter signature.</span></span> <span data-ttu-id="9f516-121">(Они оба должны принимать целочисленное значение в качестве параметра.)</span><span class="sxs-lookup"><span data-stu-id="9f516-121">(They both need to accept a single integer as a parameter.)</span></span>

<span data-ttu-id="9f516-122">Чтобы отсортировать этот выходной, можно сделать несколько вещей.</span><span class="sxs-lookup"><span data-stu-id="9f516-122">To sort this out, you can do a couple of things.</span></span> <span data-ttu-id="9f516-123">Одна — предоставить методы разные имена.</span><span class="sxs-lookup"><span data-stu-id="9f516-123">One is to give the methods different names.</span></span> <span data-ttu-id="9f516-124">Именно это было представлено в предыдущем примере механизма формирования шаблонов.</span><span class="sxs-lookup"><span data-stu-id="9f516-124">That's what the scaffolding mechanism did in the preceding example.</span></span> <span data-ttu-id="9f516-125">Но в этом случае возникает небольшая проблема: ASP.NET сопоставляет сегменты URL-адреса с методами действий по имени, а при переименовании метода, как правило, маршрутизация не сможет найти этот метод.</span><span class="sxs-lookup"><span data-stu-id="9f516-125">However, this introduces a small problem: ASP.NET maps segments of a URL to action methods by name, and if you rename a method, routing normally wouldn't be able to find that method.</span></span> <span data-ttu-id="9f516-126">Решение показано в примере, а именно: в метод `DeleteConfirmed` следует добавить атрибут `ActionName("Delete")`.</span><span class="sxs-lookup"><span data-stu-id="9f516-126">The solution is what you see in the example, which is to add the `ActionName("Delete")` attribute to the `DeleteConfirmed` method.</span></span> <span data-ttu-id="9f516-127">Это фактически выполняет сопоставление для системы маршрутизации, таким образом, чтобы URL-адрес, который включает в себя */Delete/* для отправки запроса будет найти `DeleteConfirmed` метод.</span><span class="sxs-lookup"><span data-stu-id="9f516-127">This effectively performs mapping for the routing system so that a URL that includes */Delete/* for a POST request will find the `DeleteConfirmed` method.</span></span>

<span data-ttu-id="9f516-128">Другой распространенный способ избежать с помощью методов с одинаковыми именами и сигнатурами является искусственное изменение сигнатуры метода POST для включения неиспользуемый параметр.</span><span class="sxs-lookup"><span data-stu-id="9f516-128">Another common way to avoid a problem with methods that have identical names and signatures is to artificially change the signature of the POST method to include an unused parameter.</span></span> <span data-ttu-id="9f516-129">Например, некоторые разработчики добавить тип параметра `FormCollection` , передаваемый в метод POST и затем просто не использовать параметр:</span><span class="sxs-lookup"><span data-stu-id="9f516-129">For example, some developers add a parameter type `FormCollection` that is passed to the POST method, and then simply don't use the parameter:</span></span>

[!code-csharp[Main](examining-the-details-and-delete-methods/samples/sample4.cs)]

## <a name="summary"></a><span data-ttu-id="9f516-130">Сводка</span><span class="sxs-lookup"><span data-stu-id="9f516-130">Summary</span></span>

<span data-ttu-id="9f516-131">Теперь у вас есть полное приложение ASP.NET MVC, которое хранит данные в локальную базу данных DB.</span><span class="sxs-lookup"><span data-stu-id="9f516-131">You now have a complete ASP.NET MVC application that stores data in a local DB database.</span></span> <span data-ttu-id="9f516-132">Можно создать, чтение, обновление, удаление и поиск фильмов.</span><span class="sxs-lookup"><span data-stu-id="9f516-132">You can create, read, update, delete, and search for movies.</span></span>

![](examining-the-details-and-delete-methods/_static/image2.png)

## <a name="next-steps"></a><span data-ttu-id="9f516-133">Следующие шаги</span><span class="sxs-lookup"><span data-stu-id="9f516-133">Next Steps</span></span>

<span data-ttu-id="9f516-134">После создания и тестирования веб-приложения, пора сделать его доступным для других пользователей через Интернет.</span><span class="sxs-lookup"><span data-stu-id="9f516-134">After you have built and tested a web application, the next step is to make it available to other people to use over the Internet.</span></span> <span data-ttu-id="9f516-135">Чтобы сделать это, необходимо развернуть его на веб-поставщик услуг размещения.</span><span class="sxs-lookup"><span data-stu-id="9f516-135">To do that, you have to deploy it to a web hosting provider.</span></span> <span data-ttu-id="9f516-136">Корпорация Майкрософт предлагает бесплатные услуг хостинга до 10 веб-сайтов в [бесплатную пробную учетную запись Azure](https://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A443DD604).</span><span class="sxs-lookup"><span data-stu-id="9f516-136">Microsoft offers free web hosting for up to 10 web sites in a [free Azure trial account](https://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A443DD604).</span></span> <span data-ttu-id="9f516-137">Я предлагаю вы затем учебник моей [развертывание приложения Secure ASP.NET MVC с членством, OAuth и базой данных SQL в Azure](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data).</span><span class="sxs-lookup"><span data-stu-id="9f516-137">I suggest you next follow my tutorial [Deploy a Secure ASP.NET MVC app with Membership, OAuth, and SQL Database to Azure](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data).</span></span> <span data-ttu-id="9f516-138">Отличная руководство представляет собой том Дайкстра любителей [Создание модели данных Entity Framework для приложения ASP.NET MVC](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span><span class="sxs-lookup"><span data-stu-id="9f516-138">An excellent tutorial is Tom Dykstra's intermediate-level [Creating an Entity Framework Data Model for an ASP.NET MVC Application](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span></span> <span data-ttu-id="9f516-139">[StackOverflow](http://stackoverflow.com/help) и [форумах ASP.NET MVC](https://forums.asp.net/1146.aspx) являются отличной помещает задавать вопросы.</span><span class="sxs-lookup"><span data-stu-id="9f516-139">[Stackoverflow](http://stackoverflow.com/help) and the [ASP.NET MVC forums](https://forums.asp.net/1146.aspx) are a great places to ask questions.</span></span> <span data-ttu-id="9f516-140">Выполните [мне](https://twitter.com/RickAndMSFT) в twitter, поэтому вы можете получать обновления на моем новейшие учебники.</span><span class="sxs-lookup"><span data-stu-id="9f516-140">Follow [me](https://twitter.com/RickAndMSFT) on twitter so you can get updates on my latest tutorials.</span></span>

<span data-ttu-id="9f516-141">Вы откликнитесь.</span><span class="sxs-lookup"><span data-stu-id="9f516-141">Feedback is welcome.</span></span>

<span data-ttu-id="9f516-142">— [Рик Андерсон](https://blogs.msdn.com/rickAndy) twitter: [@RickAndMSFT](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="9f516-142">— [Rick Anderson](https://blogs.msdn.com/rickAndy) twitter: [@RickAndMSFT](https://twitter.com/RickAndMSFT)</span></span>  
<span data-ttu-id="9f516-143">— [(Scott hanselman)](http://www.hanselman.com/blog/) twitter: [@shanselman](https://twitter.com/shanselman)</span><span class="sxs-lookup"><span data-stu-id="9f516-143">— [Scott Hanselman](http://www.hanselman.com/blog/) twitter: [@shanselman](https://twitter.com/shanselman)</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="9f516-144">Назад</span><span class="sxs-lookup"><span data-stu-id="9f516-144">Previous</span></span>](adding-validation.md)