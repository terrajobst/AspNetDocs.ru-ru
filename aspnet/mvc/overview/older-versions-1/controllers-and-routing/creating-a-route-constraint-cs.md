---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-a-route-constraint-cs
title: Создание ограничения маршрута (C#) | Документация Майкрософт
author: StephenWalther
description: В этом руководстве Стивен Вальтер демонстрирует, как можно управлять тем, как запросы браузера сопоставляют маршруты, создавая ограничения маршрута с помощью регулярных выражений.
ms.author: riande
ms.date: 02/16/2009
ms.assetid: 0bfd06b1-12d3-4fbb-9779-a82e5eb7fe7d
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-a-route-constraint-cs
msc.type: authoredcontent
ms.openlocfilehash: 51ef859287b3424faf85f4a3606a220ab48a9466
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78470166"
---
# <a name="creating-a-route-constraint-c"></a><span data-ttu-id="7e7eb-103">Создание ограничения маршрута (C#)</span><span class="sxs-lookup"><span data-stu-id="7e7eb-103">Creating a Route Constraint (C#)</span></span>

<span data-ttu-id="7e7eb-104">по [Стивен Вальтер](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="7e7eb-104">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

> <span data-ttu-id="7e7eb-105">В этом руководстве Стивен Вальтер демонстрирует, как можно управлять тем, как запросы браузера сопоставляют маршруты, создавая ограничения маршрута с помощью регулярных выражений.</span><span class="sxs-lookup"><span data-stu-id="7e7eb-105">In this tutorial, Stephen Walther demonstrates how you can control how browser requests match routes by creating route constraints with regular expressions.</span></span>

<span data-ttu-id="7e7eb-106">Ограничения маршрута используются для ограничения запросов обозревателя, соответствующих определенному маршруту.</span><span class="sxs-lookup"><span data-stu-id="7e7eb-106">You use route constraints to restrict the browser requests that match a particular route.</span></span> <span data-ttu-id="7e7eb-107">Для указания ограничения маршрута можно использовать регулярное выражение.</span><span class="sxs-lookup"><span data-stu-id="7e7eb-107">You can use a regular expression to specify a route constraint.</span></span>

<span data-ttu-id="7e7eb-108">Например, предположим, что вы определили маршрут в листинге 1 в файле Global. asax.</span><span class="sxs-lookup"><span data-stu-id="7e7eb-108">For example, imagine that you have defined the route in Listing 1 in your Global.asax file.</span></span>

<span data-ttu-id="7e7eb-109">**Листинг 1. Global.asax.cs**</span><span class="sxs-lookup"><span data-stu-id="7e7eb-109">**Listing 1 - Global.asax.cs**</span></span>

[!code-csharp[Main](creating-a-route-constraint-cs/samples/sample1.cs)]

<span data-ttu-id="7e7eb-110">В листинге 1 содержится маршрут с именем Product.</span><span class="sxs-lookup"><span data-stu-id="7e7eb-110">Listing 1 contains a route named Product.</span></span> <span data-ttu-id="7e7eb-111">Вы можете использовать маршрут продукта, чтобы сопоставлять запросы браузера с Продуктконтроллер, содержащимся в листинге 2.</span><span class="sxs-lookup"><span data-stu-id="7e7eb-111">You can use the Product route to map browser requests to the ProductController contained in Listing 2.</span></span>

<span data-ttu-id="7e7eb-112">**Листинг 2. Контроллерс\продуктконтроллер.КС**</span><span class="sxs-lookup"><span data-stu-id="7e7eb-112">**Listing 2 - Controllers\ProductController.cs**</span></span>

[!code-csharp[Main](creating-a-route-constraint-cs/samples/sample2.cs)]

<span data-ttu-id="7e7eb-113">Обратите внимание, что действие Details (), предоставляемое контроллером продукта, принимает один параметр с именем productId.</span><span class="sxs-lookup"><span data-stu-id="7e7eb-113">Notice that the Details() action exposed by the Product controller accepts a single parameter named productId.</span></span> <span data-ttu-id="7e7eb-114">Этот параметр является целочисленным параметром.</span><span class="sxs-lookup"><span data-stu-id="7e7eb-114">This parameter is an integer parameter.</span></span>

<span data-ttu-id="7e7eb-115">Маршрут, определенный в листинге 1, будет соответствовать любому из следующих URL-адресов:</span><span class="sxs-lookup"><span data-stu-id="7e7eb-115">The route defined in Listing 1 will match any of the following URLs:</span></span>

- <span data-ttu-id="7e7eb-116">/Product/23</span><span class="sxs-lookup"><span data-stu-id="7e7eb-116">/Product/23</span></span>
- <span data-ttu-id="7e7eb-117">/Product/7</span><span class="sxs-lookup"><span data-stu-id="7e7eb-117">/Product/7</span></span>

<span data-ttu-id="7e7eb-118">К сожалению, маршрут также будет соответствовать следующим URL-адресам:</span><span class="sxs-lookup"><span data-stu-id="7e7eb-118">Unfortunately, the route will also match the following URLs:</span></span>

- <span data-ttu-id="7e7eb-119">/продукт/блах</span><span class="sxs-lookup"><span data-stu-id="7e7eb-119">/Product/blah</span></span>
- <span data-ttu-id="7e7eb-120">/продукт/аппле</span><span class="sxs-lookup"><span data-stu-id="7e7eb-120">/Product/apple</span></span>

<span data-ttu-id="7e7eb-121">Так как действие Details () принимает целочисленный параметр, запрос, содержащий нечто, отличное от целочисленного значения, вызовет ошибку.</span><span class="sxs-lookup"><span data-stu-id="7e7eb-121">Because the Details() action expects an integer parameter, making a request that contains something other than an integer value will cause an error.</span></span> <span data-ttu-id="7e7eb-122">Например, если ввести URL-адрес/продукт/Аппле в браузере, вы получите страницу ошибки на рис. 1.</span><span class="sxs-lookup"><span data-stu-id="7e7eb-122">For example, if you type the URL /Product/apple into your browser then you will get the error page in Figure 1.</span></span>

<span data-ttu-id="7e7eb-123">[![диалоговом окне «Создание проекта»](creating-a-route-constraint-cs/_static/image1.jpg)](creating-a-route-constraint-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="7e7eb-123">[![The New Project dialog box](creating-a-route-constraint-cs/_static/image1.jpg)](creating-a-route-constraint-cs/_static/image1.png)</span></span>

<span data-ttu-id="7e7eb-124">**Рис. 01**. Просмотр развернутой страницы ([щелкните, чтобы просмотреть изображение с полным размером](creating-a-route-constraint-cs/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="7e7eb-124">**Figure 01**: Seeing a page explode ([Click to view full-size image](creating-a-route-constraint-cs/_static/image2.png))</span></span>

<span data-ttu-id="7e7eb-125">Вы действительно хотите использовать только URL-адреса, содержащие правильный целочисленный productId.</span><span class="sxs-lookup"><span data-stu-id="7e7eb-125">What you really want to do is only match URLs that contain a proper integer productId.</span></span> <span data-ttu-id="7e7eb-126">Ограничение можно использовать при определении маршрута для ограничения URL-адресов, соответствующих маршруту.</span><span class="sxs-lookup"><span data-stu-id="7e7eb-126">You can use a constraint when defining a route to restrict the URLs that match the route.</span></span> <span data-ttu-id="7e7eb-127">Измененный маршрут продукта в листинге 3 содержит ограничение регулярного выражения, которое соответствует только целым числам.</span><span class="sxs-lookup"><span data-stu-id="7e7eb-127">The modified Product route in Listing 3 contains a regular expression constraint that only matches integers.</span></span>

<span data-ttu-id="7e7eb-128">**Листинг 3. Global.asax.cs**</span><span class="sxs-lookup"><span data-stu-id="7e7eb-128">**Listing 3 - Global.asax.cs**</span></span>

[!code-csharp[Main](creating-a-route-constraint-cs/samples/sample3.cs)]

<span data-ttu-id="7e7eb-129">Регулярное выражение \d + соответствует одному или нескольким целым числам.</span><span class="sxs-lookup"><span data-stu-id="7e7eb-129">The regular expression \d+ matches one or more integers.</span></span> <span data-ttu-id="7e7eb-130">Это ограничение приводит к тому, что маршрут продукта будет соответствовать следующим URL-адресам:</span><span class="sxs-lookup"><span data-stu-id="7e7eb-130">This constraint causes the Product route to match the following URLs:</span></span>

- <span data-ttu-id="7e7eb-131">/Product/3</span><span class="sxs-lookup"><span data-stu-id="7e7eb-131">/Product/3</span></span>
- <span data-ttu-id="7e7eb-132">/Product/8999</span><span class="sxs-lookup"><span data-stu-id="7e7eb-132">/Product/8999</span></span>

<span data-ttu-id="7e7eb-133">Но не следующие URL-адреса:</span><span class="sxs-lookup"><span data-stu-id="7e7eb-133">But not the following URLs:</span></span>

- <span data-ttu-id="7e7eb-134">/продукт/аппле</span><span class="sxs-lookup"><span data-stu-id="7e7eb-134">/Product/apple</span></span>
- <span data-ttu-id="7e7eb-135">/Product</span><span class="sxs-lookup"><span data-stu-id="7e7eb-135">/Product</span></span>

- <span data-ttu-id="7e7eb-136">Эти запросы браузера будут обрабатываться другим маршрутом или, если соответствующие маршруты отсутствуют, будет возвращено сообщение об ошибке *"ресурс не найден"* .</span><span class="sxs-lookup"><span data-stu-id="7e7eb-136">These browser requests will be handled by another route or, if there are no matching routes, a *The resource could not be found* error will be returned.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="7e7eb-137">[Назад](creating-custom-routes-cs.md)
> [Вперед](creating-a-custom-route-constraint-cs.md)</span><span class="sxs-lookup"><span data-stu-id="7e7eb-137">[Previous](creating-custom-routes-cs.md)
[Next](creating-a-custom-route-constraint-cs.md)</span></span>
