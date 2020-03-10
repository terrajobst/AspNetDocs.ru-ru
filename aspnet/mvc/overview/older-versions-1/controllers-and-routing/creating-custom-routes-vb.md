---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-custom-routes-vb
title: Создание настраиваемых маршрутов (VB) | Документация Майкрософт
author: microsoft
description: Узнайте, как добавить пользовательские маршруты в приложение ASP.NET MVC. В этом руководстве вы узнаете, как изменить таблицу маршрутов по умолчанию в файле Global. asax.
ms.author: riande
ms.date: 02/16/2009
ms.assetid: 6ac5758b-6199-42af-adcb-21954b864951
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-custom-routes-vb
msc.type: authoredcontent
ms.openlocfilehash: 22b44e9e575c9d404881a23ee735bb0c8b7109e1
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78486696"
---
# <a name="creating-custom-routes-vb"></a><span data-ttu-id="94cbb-104">Создание пользовательских маршрутов (VB)</span><span class="sxs-lookup"><span data-stu-id="94cbb-104">Creating Custom Routes (VB)</span></span>

<span data-ttu-id="94cbb-105">по [Майкрософт](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="94cbb-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="94cbb-106">Узнайте, как добавить пользовательские маршруты в приложение ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="94cbb-106">Learn how to add custom routes to an ASP.NET MVC application.</span></span> <span data-ttu-id="94cbb-107">В этом руководстве вы узнаете, как изменить таблицу маршрутов по умолчанию в файле Global. asax.</span><span class="sxs-lookup"><span data-stu-id="94cbb-107">In this tutorial, you learn how to modify the default route table in the Global.asax file.</span></span>

<span data-ttu-id="94cbb-108">В этом руководстве вы узнаете, как добавить настраиваемый маршрут в приложение ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="94cbb-108">In this tutorial, you learn how to add a custom route to an ASP.NET MVC application.</span></span> <span data-ttu-id="94cbb-109">Вы узнаете, как изменить таблицу маршрутов по умолчанию в файле Global. asax с помощью настраиваемого маршрута.</span><span class="sxs-lookup"><span data-stu-id="94cbb-109">You learn how to modify the default route table in the Global.asax file with a custom route.</span></span>

<span data-ttu-id="94cbb-110">В приложениях ASP.NET MVC Таблица маршрутов по умолчанию будет работать прекрасно.</span><span class="sxs-lookup"><span data-stu-id="94cbb-110">In ASP.NET MVC applications, the default route table will work just fine.</span></span> <span data-ttu-id="94cbb-111">Однако вы можете обнаружить, что у вас есть специализированные потребности в маршрутизации.</span><span class="sxs-lookup"><span data-stu-id="94cbb-111">However, you might discover that you have specialized routing needs.</span></span> <span data-ttu-id="94cbb-112">В этом случае можно создать настраиваемый маршрут.</span><span class="sxs-lookup"><span data-stu-id="94cbb-112">In that case, you can create a custom route.</span></span>

<span data-ttu-id="94cbb-113">Представьте, например, что вы создаете приложение блога.</span><span class="sxs-lookup"><span data-stu-id="94cbb-113">Imagine, for example, that you are building a blog application.</span></span> <span data-ttu-id="94cbb-114">Может потребоваться обрабатывать входящие запросы, которые выглядят следующим образом:</span><span class="sxs-lookup"><span data-stu-id="94cbb-114">You might want to handle incoming requests that look like this:</span></span>

<span data-ttu-id="94cbb-115">/Archive/12-25-2009</span><span class="sxs-lookup"><span data-stu-id="94cbb-115">/Archive/12-25-2009</span></span>

<span data-ttu-id="94cbb-116">Когда пользователь вводит этот запрос, необходимо вернуть запись в блоге, соответствующую дате 12/25/2009.</span><span class="sxs-lookup"><span data-stu-id="94cbb-116">When a user enters this request, you want to return the blog entry that corresponds to the date 12/25/2009.</span></span> <span data-ttu-id="94cbb-117">Чтобы обрабатывался этот тип запроса, необходимо создать настраиваемый маршрут.</span><span class="sxs-lookup"><span data-stu-id="94cbb-117">In order to handle this type of request, you need to create a custom route.</span></span>

<span data-ttu-id="94cbb-118">Файл Global. asax в листинге 1 содержит новый настраиваемый маршрут с именем Blog, который обрабатывает запросы, которые выглядят как*Дата записи*/арчиве/.</span><span class="sxs-lookup"><span data-stu-id="94cbb-118">The Global.asax file in Listing 1 contains a new custom route, named Blog, which handles requests that look like /Archive/*entry date*.</span></span>

<span data-ttu-id="94cbb-119">**Листинг 1-Global. asax (с настраиваемым маршрутом)**</span><span class="sxs-lookup"><span data-stu-id="94cbb-119">**Listing 1 - Global.asax (with custom route)**</span></span>

[!code-vb[Main](creating-custom-routes-vb/samples/sample1.vb)]

<span data-ttu-id="94cbb-120">Порядок маршрутов, добавляемых в таблицу маршрутов, важен.</span><span class="sxs-lookup"><span data-stu-id="94cbb-120">The order of the routes that you add to the route table is important.</span></span> <span data-ttu-id="94cbb-121">Новый пользовательский маршрут блога добавляется перед существующим маршрутом по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="94cbb-121">Our new custom Blog route is added before the existing Default route.</span></span> <span data-ttu-id="94cbb-122">Если вы меняете порядок, то маршрут по умолчанию всегда будет вызываться вместо настраиваемого маршрута.</span><span class="sxs-lookup"><span data-stu-id="94cbb-122">If you reversed the order, then the Default route always will get called instead of the custom route.</span></span>

<span data-ttu-id="94cbb-123">Пользовательский маршрут блога соответствует любому запросу, который начинается с/Арчиве/.</span><span class="sxs-lookup"><span data-stu-id="94cbb-123">The custom Blog route matches any request that starts with /Archive/.</span></span> <span data-ttu-id="94cbb-124">Таким образом, он будет соответствовать всем следующим URL-адресам:</span><span class="sxs-lookup"><span data-stu-id="94cbb-124">So, it matches all of the following URLs:</span></span>

- <span data-ttu-id="94cbb-125">/Archive/12-25-2009</span><span class="sxs-lookup"><span data-stu-id="94cbb-125">/Archive/12-25-2009</span></span>

- <span data-ttu-id="94cbb-126">/Archive/10-6-2004</span><span class="sxs-lookup"><span data-stu-id="94cbb-126">/Archive/10-6-2004</span></span>

- <span data-ttu-id="94cbb-127">/арчиве/аппле</span><span class="sxs-lookup"><span data-stu-id="94cbb-127">/Archive/apple</span></span>

<span data-ttu-id="94cbb-128">Пользовательский маршрут сопоставляет входящий запрос с контроллером с именем Archive и вызывает действие Entry ().</span><span class="sxs-lookup"><span data-stu-id="94cbb-128">The custom route maps the incoming request to a controller named Archive and invokes the Entry() action.</span></span> <span data-ttu-id="94cbb-129">При вызове метода Entry () Дата записи передается как параметр с именем Ентридате.</span><span class="sxs-lookup"><span data-stu-id="94cbb-129">When the Entry() method is called, the entry date is passed as a parameter named entryDate.</span></span>

<span data-ttu-id="94cbb-130">Вы можете использовать настраиваемый маршрут блога с контроллером в листинге 2.</span><span class="sxs-lookup"><span data-stu-id="94cbb-130">You can use the Blog custom route with the controller in Listing 2.</span></span>

<span data-ttu-id="94cbb-131">**Листинг 2-Арчивеконтроллер. vb**</span><span class="sxs-lookup"><span data-stu-id="94cbb-131">**Listing 2 - ArchiveController.vb**</span></span>

[!code-vb[Main](creating-custom-routes-vb/samples/sample2.vb)]

<span data-ttu-id="94cbb-132">Обратите внимание, что метод Entry () в листинге 2 принимает параметр типа DateTime.</span><span class="sxs-lookup"><span data-stu-id="94cbb-132">Notice that the Entry() method in Listing 2 accepts a parameter of type DateTime.</span></span> <span data-ttu-id="94cbb-133">Платформа MVC достаточно интеллектуальна для того, чтобы автоматически преобразовать дату записи из URL-адреса в значение DateTime.</span><span class="sxs-lookup"><span data-stu-id="94cbb-133">The MVC framework is smart enough to convert the entry date from the URL into a DateTime value automatically.</span></span> <span data-ttu-id="94cbb-134">Если параметр даты записи из URL-адреса не может быть преобразован в тип DateTime, возникает ошибка (см. рис. 1).</span><span class="sxs-lookup"><span data-stu-id="94cbb-134">If the entry date parameter from the URL cannot be converted to a DateTime, an error is raised (see Figure 1).</span></span>

<span data-ttu-id="94cbb-135">**Рис. 1. Ошибка преобразования параметра**</span><span class="sxs-lookup"><span data-stu-id="94cbb-135">**Figure 1 - Error from converting parameter**</span></span>

<span data-ttu-id="94cbb-136">[![диалоговом окне «Создание проекта»](creating-custom-routes-vb/_static/image1.jpg)](creating-custom-routes-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="94cbb-136">[![The New Project dialog box](creating-custom-routes-vb/_static/image1.jpg)](creating-custom-routes-vb/_static/image1.png)</span></span>

<span data-ttu-id="94cbb-137">**Рис. 01**. Ошибка при преобразовании параметра ([щелкните, чтобы просмотреть изображение с полным размером](creating-custom-routes-vb/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="94cbb-137">**Figure 01**: Error from converting parameter ([Click to view full-size image](creating-custom-routes-vb/_static/image2.png))</span></span>

## <a name="summary"></a><span data-ttu-id="94cbb-138">Сводка</span><span class="sxs-lookup"><span data-stu-id="94cbb-138">Summary</span></span>

<span data-ttu-id="94cbb-139">Цель этого учебника — продемонстрировать, как можно создать настраиваемый маршрут.</span><span class="sxs-lookup"><span data-stu-id="94cbb-139">The goal of this tutorial was to demonstrate how you can create a custom route.</span></span> <span data-ttu-id="94cbb-140">Вы узнали, как добавить настраиваемый маршрут в таблицу маршрутов в файле Global. asax, который представляет записи блога.</span><span class="sxs-lookup"><span data-stu-id="94cbb-140">You learned how to add a custom route to the route table in the Global.asax file that represents blog entries.</span></span> <span data-ttu-id="94cbb-141">Мы обсуждали, как сопоставлять запросы для записей блога с контроллером с именем Арчивеконтроллер и действием контроллера с именем Entry ().</span><span class="sxs-lookup"><span data-stu-id="94cbb-141">We discussed how to map requests for blog entries to a controller named ArchiveController and a controller action named Entry().</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="94cbb-142">[Назад](asp-net-mvc-controller-overview-vb.md)
> [Вперед](creating-a-route-constraint-vb.md)</span><span class="sxs-lookup"><span data-stu-id="94cbb-142">[Previous](asp-net-mvc-controller-overview-vb.md)
[Next](creating-a-route-constraint-vb.md)</span></span>
