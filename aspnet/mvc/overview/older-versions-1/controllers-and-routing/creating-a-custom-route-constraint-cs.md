---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-a-custom-route-constraint-cs
title: Создание пользовательского ограничения маршрута (C#) | Документация Майкрософт
author: StephenWalther
description: Стивен Вальтер демонстрирует, как можно создать пользовательское ограничение маршрута. Мы реализуем простое пользовательское ограничение, которое не дает возможность сопоставлять маршрут w...
ms.author: riande
ms.date: 02/16/2009
ms.assetid: a4f4bf4e-abcc-4650-8f43-527e48b52fe6
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-a-custom-route-constraint-cs
msc.type: authoredcontent
ms.openlocfilehash: 98d5839e3d2623665770ccc5689c28f9eb29c8f6
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78486828"
---
# <a name="creating-a-custom-route-constraint-c"></a><span data-ttu-id="9dc6f-104">Создание пользовательского ограничения маршрута (C#)</span><span class="sxs-lookup"><span data-stu-id="9dc6f-104">Creating a Custom Route Constraint (C#)</span></span>

<span data-ttu-id="9dc6f-105">по [Стивен Вальтер](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="9dc6f-105">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

> <span data-ttu-id="9dc6f-106">Стивен Вальтер демонстрирует, как можно создать пользовательское ограничение маршрута.</span><span class="sxs-lookup"><span data-stu-id="9dc6f-106">Stephen Walther demonstrates how you can create a custom route constraint.</span></span> <span data-ttu-id="9dc6f-107">Мы реализуем простое настраиваемое ограничение, которое предотвращает сопоставление маршрута при выполнении запроса браузера с удаленного компьютера.</span><span class="sxs-lookup"><span data-stu-id="9dc6f-107">We implement a simple custom constraint that prevents a route from being matched when a browser request is made from a remote computer.</span></span>

<span data-ttu-id="9dc6f-108">Цель этого учебника — показать, как можно создать пользовательское ограничение маршрута.</span><span class="sxs-lookup"><span data-stu-id="9dc6f-108">The goal of this tutorial is to demonstrate how you can create a custom route constraint.</span></span> <span data-ttu-id="9dc6f-109">Настраиваемое ограничение маршрута позволяет запретить сопоставление маршрута, если не сопоставлено какое-либо пользовательское условие.</span><span class="sxs-lookup"><span data-stu-id="9dc6f-109">A custom route constraint enables you to prevent a route from being matched unless some custom condition is matched.</span></span>

<span data-ttu-id="9dc6f-110">В этом руководстве мы создадим ограничение на маршрут localhost.</span><span class="sxs-lookup"><span data-stu-id="9dc6f-110">In this tutorial, we create a Localhost route constraint.</span></span> <span data-ttu-id="9dc6f-111">Ограничение маршрута localhost соответствует только запросам, выполненным с локального компьютера.</span><span class="sxs-lookup"><span data-stu-id="9dc6f-111">The Localhost route constraint only matches requests made from the local computer.</span></span> <span data-ttu-id="9dc6f-112">Удаленные запросы из Интернета не сопоставляются.</span><span class="sxs-lookup"><span data-stu-id="9dc6f-112">Remote requests from across the Internet are not matched.</span></span>

<span data-ttu-id="9dc6f-113">Пользовательское ограничение маршрута реализуется путем реализации интерфейса Ираутеконстраинт.</span><span class="sxs-lookup"><span data-stu-id="9dc6f-113">You implement a custom route constraint by implementing the IRouteConstraint interface.</span></span> <span data-ttu-id="9dc6f-114">Это чрезвычайно простой интерфейс, описывающий один метод:</span><span class="sxs-lookup"><span data-stu-id="9dc6f-114">This is an extremely simple interface which describes a single method:</span></span>

[!code-csharp[Main](creating-a-custom-route-constraint-cs/samples/sample1.cs)]

<span data-ttu-id="9dc6f-115">Метод возвращает логическое значение.</span><span class="sxs-lookup"><span data-stu-id="9dc6f-115">The method returns a Boolean value.</span></span> <span data-ttu-id="9dc6f-116">Если возвращается значение false, маршрут, связанный с ограничением, не будет соответствовать запросу браузера.</span><span class="sxs-lookup"><span data-stu-id="9dc6f-116">If you return false, the route associated with the constraint won't match the browser request.</span></span>

<span data-ttu-id="9dc6f-117">Ограничение localhost содержится в листинге 1.</span><span class="sxs-lookup"><span data-stu-id="9dc6f-117">The Localhost constraint is contained in Listing 1.</span></span>

<span data-ttu-id="9dc6f-118">**Листинг 1. LocalhostConstraint.cs**</span><span class="sxs-lookup"><span data-stu-id="9dc6f-118">**Listing 1 - LocalhostConstraint.cs**</span></span>

[!code-csharp[Main](creating-a-custom-route-constraint-cs/samples/sample2.cs)]

<span data-ttu-id="9dc6f-119">Ограничение в листинге 1 использует преимущества свойства onlocal, предоставляемого классом HttpRequest.</span><span class="sxs-lookup"><span data-stu-id="9dc6f-119">The constraint in Listing 1 takes advantage of the IsLocal property exposed by the HttpRequest class.</span></span> <span data-ttu-id="9dc6f-120">Это свойство возвращает значение true, если IP-адрес запроса имеет значение 127.0.0.1 или если IP-адрес запроса совпадает с IP-адреса сервера.</span><span class="sxs-lookup"><span data-stu-id="9dc6f-120">This property returns true when the IP address of the request is either 127.0.0.1 or when the IP of the request is the same as the server's IP address.</span></span>

<span data-ttu-id="9dc6f-121">Пользовательское ограничение используется в маршруте, определенном в файле Global. asax.</span><span class="sxs-lookup"><span data-stu-id="9dc6f-121">You use a custom constraint within a route defined in the Global.asax file.</span></span> <span data-ttu-id="9dc6f-122">Файл Global. asax в листинге 2 использует ограничение localhost, чтобы запретить всем пользователям запрашивать страницу администрирования, если они не выполняют запрос с локального сервера.</span><span class="sxs-lookup"><span data-stu-id="9dc6f-122">The Global.asax file in Listing 2 uses the Localhost constraint to prevent anyone from requesting an Admin page unless they make the request from the local server.</span></span> <span data-ttu-id="9dc6f-123">Например, запрос на/админ/делетеалл завершится ошибкой с удаленного сервера.</span><span class="sxs-lookup"><span data-stu-id="9dc6f-123">For example, a request for /Admin/DeleteAll will fail when made from a remote server.</span></span>

<span data-ttu-id="9dc6f-124">**Листинг 2-Global. asax**</span><span class="sxs-lookup"><span data-stu-id="9dc6f-124">**Listing 2 - Global.asax**</span></span>

[!code-csharp[Main](creating-a-custom-route-constraint-cs/samples/sample3.cs)]

<span data-ttu-id="9dc6f-125">Ограничение localhost используется в определении маршрута администратора.</span><span class="sxs-lookup"><span data-stu-id="9dc6f-125">The Localhost constraint is used in the definition of the Admin route.</span></span> <span data-ttu-id="9dc6f-126">Этот маршрут не будет сопоставлен с запросом удаленного браузера.</span><span class="sxs-lookup"><span data-stu-id="9dc6f-126">This route won't be matched by a remote browser request.</span></span> <span data-ttu-id="9dc6f-127">Однако следует понимать, что другие маршруты, определенные в Global. asax, могут соответствовать одному и тому же запросу.</span><span class="sxs-lookup"><span data-stu-id="9dc6f-127">Realize, however, that other routes defined in Global.asax might match the same request.</span></span> <span data-ttu-id="9dc6f-128">Важно понимать, что ограничение не позволяет определенному маршруту сопоставлять запрос, а не все маршруты, определенные в файле Global. asax.</span><span class="sxs-lookup"><span data-stu-id="9dc6f-128">It is important to understand that a constraint prevents a particular route from matching a request and not all routes defined in the Global.asax file.</span></span>

<span data-ttu-id="9dc6f-129">Обратите внимание, что к маршруту по умолчанию был добавлен комментарий из файла Global. asax в листинге 2.</span><span class="sxs-lookup"><span data-stu-id="9dc6f-129">Notice that the Default route has been commented out from the Global.asax file in Listing 2.</span></span> <span data-ttu-id="9dc6f-130">Если вы включили маршрут по умолчанию, маршрут по умолчанию будет соответствовать запросам контроллера администратора.</span><span class="sxs-lookup"><span data-stu-id="9dc6f-130">If you include the Default route, then the Default route would match requests for the Admin controller.</span></span> <span data-ttu-id="9dc6f-131">В этом случае удаленные пользователи по-прежнему могут вызывать действия контроллера администратора, даже если их запросы не будут совпадать с маршрутом администратора.</span><span class="sxs-lookup"><span data-stu-id="9dc6f-131">In that case, remote users could still invoke actions of the Admin controller even though their requests wouldn't match the Admin route.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="9dc6f-132">[Назад](creating-a-route-constraint-cs.md)
> [Вперед](asp-net-mvc-controller-overview-vb.md)</span><span class="sxs-lookup"><span data-stu-id="9dc6f-132">[Previous](creating-a-route-constraint-cs.md)
[Next](asp-net-mvc-controller-overview-vb.md)</span></span>
