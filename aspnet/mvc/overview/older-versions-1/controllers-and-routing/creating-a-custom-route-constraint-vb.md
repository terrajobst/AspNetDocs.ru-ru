---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-a-custom-route-constraint-vb
title: Создание пользовательского ограничения маршрута (VB) | Документация Майкрософт
author: StephenWalther
description: Стивен Вальтер демонстрирует, как можно создать пользовательское ограничение маршрута. Мы реализуем простое пользовательское ограничение, которое не дает возможность сопоставлять маршрут w...
ms.author: riande
ms.date: 02/16/2009
ms.assetid: 892edb27-1cc2-4eaf-8314-dbc2efc6228a
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-a-custom-route-constraint-vb
msc.type: authoredcontent
ms.openlocfilehash: 2330708cf4a28180ce8a05f4696bf7a7a32092d6
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78486792"
---
# <a name="creating-a-custom-route-constraint-vb"></a><span data-ttu-id="1cd48-104">Создание пользовательского ограничения маршрута (VB)</span><span class="sxs-lookup"><span data-stu-id="1cd48-104">Creating a Custom Route Constraint (VB)</span></span>

<span data-ttu-id="1cd48-105">по [Стивен Вальтер](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="1cd48-105">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

> <span data-ttu-id="1cd48-106">Стивен Вальтер демонстрирует, как можно создать пользовательское ограничение маршрута.</span><span class="sxs-lookup"><span data-stu-id="1cd48-106">Stephen Walther demonstrates how you can create a custom route constraint.</span></span> <span data-ttu-id="1cd48-107">Мы реализуем простое настраиваемое ограничение, которое предотвращает сопоставление маршрута при выполнении запроса браузера с удаленного компьютера.</span><span class="sxs-lookup"><span data-stu-id="1cd48-107">We implement a simple custom constraint that prevents a route from being matched when a browser request is made from a remote computer.</span></span>

<span data-ttu-id="1cd48-108">Цель этого учебника — показать, как можно создать пользовательское ограничение маршрута.</span><span class="sxs-lookup"><span data-stu-id="1cd48-108">The goal of this tutorial is to demonstrate how you can create a custom route constraint.</span></span> <span data-ttu-id="1cd48-109">Настраиваемое ограничение маршрута позволяет запретить сопоставление маршрута, если не сопоставлено какое-либо пользовательское условие.</span><span class="sxs-lookup"><span data-stu-id="1cd48-109">A custom route constraint enables you to prevent a route from being matched unless some custom condition is matched.</span></span>

<span data-ttu-id="1cd48-110">В этом руководстве мы создадим ограничение на маршрут localhost.</span><span class="sxs-lookup"><span data-stu-id="1cd48-110">In this tutorial, we create a Localhost route constraint.</span></span> <span data-ttu-id="1cd48-111">Ограничение маршрута localhost соответствует только запросам, выполненным с локального компьютера.</span><span class="sxs-lookup"><span data-stu-id="1cd48-111">The Localhost route constraint only matches requests made from the local computer.</span></span> <span data-ttu-id="1cd48-112">Удаленные запросы из Интернета не сопоставляются.</span><span class="sxs-lookup"><span data-stu-id="1cd48-112">Remote requests from across the Internet are not matched.</span></span>

<span data-ttu-id="1cd48-113">Пользовательское ограничение маршрута реализуется путем реализации интерфейса Ираутеконстраинт.</span><span class="sxs-lookup"><span data-stu-id="1cd48-113">You implement a custom route constraint by implementing the IRouteConstraint interface.</span></span> <span data-ttu-id="1cd48-114">Это чрезвычайно простой интерфейс, описывающий один метод:</span><span class="sxs-lookup"><span data-stu-id="1cd48-114">This is an extremely simple interface which describes a single method:</span></span>

[!code-vb[Main](creating-a-custom-route-constraint-vb/samples/sample1.vb)]

<span data-ttu-id="1cd48-115">Метод возвращает логическое значение.</span><span class="sxs-lookup"><span data-stu-id="1cd48-115">The method returns a Boolean value.</span></span> <span data-ttu-id="1cd48-116">Если возвращается значение false, маршрут, связанный с ограничением, не будет соответствовать запросу браузера.</span><span class="sxs-lookup"><span data-stu-id="1cd48-116">If you return False, the route associated with the constraint won't match the browser request.</span></span>

<span data-ttu-id="1cd48-117">Ограничение localhost содержится в листинге 1.</span><span class="sxs-lookup"><span data-stu-id="1cd48-117">The Localhost constraint is contained in Listing 1.</span></span>

<span data-ttu-id="1cd48-118">**Листинг 1-Локалхостконстраинт. vb**</span><span class="sxs-lookup"><span data-stu-id="1cd48-118">**Listing 1 - LocalhostConstraint.vb**</span></span>

[!code-vb[Main](creating-a-custom-route-constraint-vb/samples/sample2.vb)]

<span data-ttu-id="1cd48-119">Ограничение в листинге 1 использует преимущества свойства onlocal, предоставляемого классом HttpRequest.</span><span class="sxs-lookup"><span data-stu-id="1cd48-119">The constraint in Listing 1 takes advantage of the IsLocal property exposed by the HttpRequest class.</span></span> <span data-ttu-id="1cd48-120">Это свойство возвращает значение true, если IP-адрес запроса имеет значение 127.0.0.1 или если IP-адрес запроса совпадает с IP-адреса сервера.</span><span class="sxs-lookup"><span data-stu-id="1cd48-120">This property returns true when the IP address of the request is either 127.0.0.1 or when the IP of the request is the same as the server's IP address.</span></span>

<span data-ttu-id="1cd48-121">Пользовательское ограничение используется в маршруте, определенном в файле Global. asax.</span><span class="sxs-lookup"><span data-stu-id="1cd48-121">You use a custom constraint within a route defined in the Global.asax file.</span></span> <span data-ttu-id="1cd48-122">Файл Global. asax в листинге 2 использует ограничение localhost, чтобы запретить всем пользователям запрашивать страницу администрирования, если они не выполняют запрос с локального сервера.</span><span class="sxs-lookup"><span data-stu-id="1cd48-122">The Global.asax file in Listing 2 uses the Localhost constraint to prevent anyone from requesting an Admin page unless they make the request from the local server.</span></span> <span data-ttu-id="1cd48-123">Например, запрос на/админ/делетеалл завершится ошибкой с удаленного сервера.</span><span class="sxs-lookup"><span data-stu-id="1cd48-123">For example, a request for /Admin/DeleteAll will fail when made from a remote server.</span></span>

<span data-ttu-id="1cd48-124">**Листинг 2-Global. asax**</span><span class="sxs-lookup"><span data-stu-id="1cd48-124">**Listing 2 - Global.asax**</span></span>

[!code-vb[Main](creating-a-custom-route-constraint-vb/samples/sample3.vb)]

<span data-ttu-id="1cd48-125">Ограничение localhost используется в определении маршрута администратора.</span><span class="sxs-lookup"><span data-stu-id="1cd48-125">The Localhost constraint is used in the definition of the Admin route.</span></span> <span data-ttu-id="1cd48-126">Этот маршрут не будет сопоставлен с запросом удаленного браузера.</span><span class="sxs-lookup"><span data-stu-id="1cd48-126">This route won't be matched by a remote browser request.</span></span> <span data-ttu-id="1cd48-127">Однако следует понимать, что другие маршруты, определенные в Global. asax, могут соответствовать одному и тому же запросу.</span><span class="sxs-lookup"><span data-stu-id="1cd48-127">Realize, however, that other routes defined in Global.asax might match the same request.</span></span> <span data-ttu-id="1cd48-128">Важно понимать, что ограничение не позволяет определенному маршруту сопоставлять запрос, а не все маршруты, определенные в файле Global. asax.</span><span class="sxs-lookup"><span data-stu-id="1cd48-128">It is important to understand that a constraint prevents a particular route from matching a request and not all routes defined in the Global.asax file.</span></span>

<span data-ttu-id="1cd48-129">Обратите внимание, что к маршруту по умолчанию был добавлен комментарий из файла Global. asax в листинге 2.</span><span class="sxs-lookup"><span data-stu-id="1cd48-129">Notice that the Default route has been commented out from the Global.asax file in Listing 2.</span></span> <span data-ttu-id="1cd48-130">Если вы включили маршрут по умолчанию, маршрут по умолчанию будет соответствовать запросам контроллера администратора.</span><span class="sxs-lookup"><span data-stu-id="1cd48-130">If you include the Default route, then the Default route would match requests for the Admin controller.</span></span> <span data-ttu-id="1cd48-131">В этом случае удаленные пользователи по-прежнему могут вызывать действия контроллера администратора, даже если их запросы не будут совпадать с маршрутом администратора.</span><span class="sxs-lookup"><span data-stu-id="1cd48-131">In that case, remote users could still invoke actions of the Admin controller even though their requests wouldn't match the Admin route.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="1cd48-132">Назад</span><span class="sxs-lookup"><span data-stu-id="1cd48-132">Previous</span></span>](creating-a-route-constraint-vb.md)
