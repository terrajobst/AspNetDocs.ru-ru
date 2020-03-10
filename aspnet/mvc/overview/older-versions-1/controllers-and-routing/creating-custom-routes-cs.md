---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-custom-routes-cs
title: Создание настраиваемых маршрутовC#() | Документация Майкрософт
author: microsoft
description: Узнайте, как добавить пользовательские маршруты в приложение ASP.NET MVC. В этом руководстве вы узнаете, как изменить таблицу маршрутов по умолчанию в файле Global. asax.
ms.author: riande
ms.date: 02/16/2009
ms.assetid: 3cd08f02-8763-490a-b625-2ac96a24b73f
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-custom-routes-cs
msc.type: authoredcontent
ms.openlocfilehash: 58f72e390f0053d136ef00ddbda0b071ba225d98
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78486726"
---
# <a name="creating-custom-routes-c"></a><span data-ttu-id="6f240-104">Создание пользовательских маршрутов (C#)</span><span class="sxs-lookup"><span data-stu-id="6f240-104">Creating Custom Routes (C#)</span></span>

<span data-ttu-id="6f240-105">по [Майкрософт](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="6f240-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="6f240-106">Узнайте, как добавить пользовательские маршруты в приложение ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="6f240-106">Learn how to add custom routes to an ASP.NET MVC application.</span></span> <span data-ttu-id="6f240-107">В этом руководстве вы узнаете, как изменить таблицу маршрутов по умолчанию в файле Global. asax.</span><span class="sxs-lookup"><span data-stu-id="6f240-107">In this tutorial, you learn how to modify the default route table in the Global.asax file.</span></span>

<span data-ttu-id="6f240-108">В этом руководстве вы узнаете, как добавить настраиваемый маршрут в приложение ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="6f240-108">In this tutorial, you learn how to add a custom route to an ASP.NET MVC application.</span></span> <span data-ttu-id="6f240-109">Вы узнаете, как изменить таблицу маршрутов по умолчанию в файле Global. asax с помощью настраиваемого маршрута.</span><span class="sxs-lookup"><span data-stu-id="6f240-109">You learn how to modify the default route table in the Global.asax file with a custom route.</span></span>

<span data-ttu-id="6f240-110">Для многих простых ASP.NET приложений MVC Таблица маршрутов по умолчанию будет работать прекрасно.</span><span class="sxs-lookup"><span data-stu-id="6f240-110">For many simple ASP.NET MVC applications, the default route table will work just fine.</span></span> <span data-ttu-id="6f240-111">Однако вы можете обнаружить, что у вас есть специализированные потребности в маршрутизации.</span><span class="sxs-lookup"><span data-stu-id="6f240-111">However, you might discover that you have specialized routing needs.</span></span> <span data-ttu-id="6f240-112">В этом случае можно создать настраиваемый маршрут.</span><span class="sxs-lookup"><span data-stu-id="6f240-112">In that case, you can create a custom route.</span></span>

<span data-ttu-id="6f240-113">Представьте, например, что вы создаете приложение блога.</span><span class="sxs-lookup"><span data-stu-id="6f240-113">Imagine, for example, that you are building a blog application.</span></span> <span data-ttu-id="6f240-114">Может потребоваться обрабатывать входящие запросы, которые выглядят следующим образом:</span><span class="sxs-lookup"><span data-stu-id="6f240-114">You might want to handle incoming requests that look like this:</span></span>

<span data-ttu-id="6f240-115">/Archive/12-25-2009</span><span class="sxs-lookup"><span data-stu-id="6f240-115">/Archive/12-25-2009</span></span>

<span data-ttu-id="6f240-116">Когда пользователь вводит этот запрос, необходимо вернуть запись в блоге, соответствующую дате 12/25/2009.</span><span class="sxs-lookup"><span data-stu-id="6f240-116">When a user enters this request, you want to return the blog entry that corresponds to the date 12/25/2009.</span></span> <span data-ttu-id="6f240-117">Чтобы обрабатывался этот тип запроса, необходимо создать настраиваемый маршрут.</span><span class="sxs-lookup"><span data-stu-id="6f240-117">In order to handle this type of request, you need to create a custom route.</span></span>

<span data-ttu-id="6f240-118">Файл Global. asax в листинге 1 содержит новый настраиваемый маршрут с именем Blog, который обрабатывает запросы, которые выглядят как*Дата записи*/арчиве/.</span><span class="sxs-lookup"><span data-stu-id="6f240-118">The Global.asax file in Listing 1 contains a new custom route, named Blog, which handles requests that look like /Archive/*entry date*.</span></span>

<span data-ttu-id="6f240-119">**Листинг 1-Global. asax (с настраиваемым маршрутом)**</span><span class="sxs-lookup"><span data-stu-id="6f240-119">**Listing 1 - Global.asax (with custom route)**</span></span>

[!code-csharp[Main](creating-custom-routes-cs/samples/sample1.cs)]

<span data-ttu-id="6f240-120">Порядок маршрутов, добавляемых в таблицу маршрутов, важен.</span><span class="sxs-lookup"><span data-stu-id="6f240-120">The order of the routes that you add to the route table is important.</span></span> <span data-ttu-id="6f240-121">Новый пользовательский маршрут блога добавляется перед существующим маршрутом по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="6f240-121">Our new custom Blog route is added before the existing Default route.</span></span> <span data-ttu-id="6f240-122">Если вы меняете порядок, то маршрут по умолчанию всегда будет вызываться вместо настраиваемого маршрута.</span><span class="sxs-lookup"><span data-stu-id="6f240-122">If you reversed the order, then the Default route always will get called instead of the custom route.</span></span>

<span data-ttu-id="6f240-123">Пользовательский маршрут блога соответствует любому запросу, который начинается с/Арчиве/.</span><span class="sxs-lookup"><span data-stu-id="6f240-123">The custom Blog route matches any request that starts with /Archive/.</span></span> <span data-ttu-id="6f240-124">Таким образом, он будет соответствовать всем следующим URL-адресам:</span><span class="sxs-lookup"><span data-stu-id="6f240-124">So, it matches all of the following URLs:</span></span>

- <span data-ttu-id="6f240-125">/Archive/12-25-2009</span><span class="sxs-lookup"><span data-stu-id="6f240-125">/Archive/12-25-2009</span></span>

- <span data-ttu-id="6f240-126">/Archive/10-6-2004</span><span class="sxs-lookup"><span data-stu-id="6f240-126">/Archive/10-6-2004</span></span>

- <span data-ttu-id="6f240-127">/арчиве/аппле</span><span class="sxs-lookup"><span data-stu-id="6f240-127">/Archive/apple</span></span>

<span data-ttu-id="6f240-128">Пользовательский маршрут сопоставляет входящий запрос с контроллером с именем Archive и вызывает действие Entry ().</span><span class="sxs-lookup"><span data-stu-id="6f240-128">The custom route maps the incoming request to a controller named Archive and invokes the Entry() action.</span></span> <span data-ttu-id="6f240-129">При вызове метода Entry () Дата записи передается как параметр с именем Ентридате.</span><span class="sxs-lookup"><span data-stu-id="6f240-129">When the Entry() method is called, the entry date is passed as a parameter named entryDate.</span></span>

<span data-ttu-id="6f240-130">Вы можете использовать настраиваемый маршрут блога с контроллером в листинге 2.</span><span class="sxs-lookup"><span data-stu-id="6f240-130">You can use the Blog custom route with the controller in Listing 2.</span></span>

<span data-ttu-id="6f240-131">**Листинг 2. ArchiveController.cs**</span><span class="sxs-lookup"><span data-stu-id="6f240-131">**Listing 2 - ArchiveController.cs**</span></span>

[!code-csharp[Main](creating-custom-routes-cs/samples/sample2.cs)]

<span data-ttu-id="6f240-132">Обратите внимание, что метод Entry () в листинге 2 принимает параметр типа DateTime.</span><span class="sxs-lookup"><span data-stu-id="6f240-132">Notice that the Entry() method in Listing 2 accepts a parameter of type DateTime.</span></span> <span data-ttu-id="6f240-133">Платформа MVC достаточно интеллектуальна для того, чтобы автоматически преобразовать дату записи из URL-адреса в значение DateTime.</span><span class="sxs-lookup"><span data-stu-id="6f240-133">The MVC framework is smart enough to convert the entry date from the URL into a DateTime value automatically.</span></span> <span data-ttu-id="6f240-134">Если параметр даты записи из URL-адреса не может быть преобразован в тип DateTime, возникает ошибка (см. рис. 1).</span><span class="sxs-lookup"><span data-stu-id="6f240-134">If the entry date parameter from the URL cannot be converted to a DateTime, an error is raised (see Figure 1).</span></span>

<span data-ttu-id="6f240-135">**Рис. 1. Ошибка преобразования параметра**</span><span class="sxs-lookup"><span data-stu-id="6f240-135">**Figure 1 - Error from converting parameter**</span></span>

<span data-ttu-id="6f240-136">[![диалоговом окне «Создание проекта»](creating-custom-routes-cs/_static/image1.jpg)](creating-custom-routes-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="6f240-136">[![The New Project dialog box](creating-custom-routes-cs/_static/image1.jpg)](creating-custom-routes-cs/_static/image1.png)</span></span>

<span data-ttu-id="6f240-137">**Рис. 01**. Ошибка при преобразовании параметра ([щелкните, чтобы просмотреть изображение с полным размером](creating-custom-routes-cs/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="6f240-137">**Figure 01**: Error from converting parameter ([Click to view full-size image](creating-custom-routes-cs/_static/image2.png))</span></span>

## <a name="summary"></a><span data-ttu-id="6f240-138">Сводка</span><span class="sxs-lookup"><span data-stu-id="6f240-138">Summary</span></span>

<span data-ttu-id="6f240-139">Цель этого учебника — продемонстрировать, как можно создать настраиваемый маршрут.</span><span class="sxs-lookup"><span data-stu-id="6f240-139">The goal of this tutorial was to demonstrate how you can create a custom route.</span></span> <span data-ttu-id="6f240-140">Вы узнали, как добавить настраиваемый маршрут в таблицу маршрутов в файле Global. asax, который представляет записи блога.</span><span class="sxs-lookup"><span data-stu-id="6f240-140">You learned how to add a custom route to the route table in the Global.asax file that represents blog entries.</span></span> <span data-ttu-id="6f240-141">Мы обсуждали, как сопоставлять запросы для записей блога с контроллером с именем Арчивеконтроллер и действием контроллера с именем Entry ().</span><span class="sxs-lookup"><span data-stu-id="6f240-141">We discussed how to map requests for blog entries to a controller named ArchiveController and a controller action named Entry().</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="6f240-142">[Назад](aspnet-mvc-controllers-overview-cs.md)
> [Вперед](creating-a-route-constraint-cs.md)</span><span class="sxs-lookup"><span data-stu-id="6f240-142">[Previous](aspnet-mvc-controllers-overview-cs.md)
[Next](creating-a-route-constraint-cs.md)</span></span>
