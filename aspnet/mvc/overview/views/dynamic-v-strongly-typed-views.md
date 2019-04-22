---
uid: mvc/overview/views/dynamic-v-strongly-typed-views
title: Динамические и Строго типизированные представления | Документация Майкрософт
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 01/27/2011
ms.assetid: 0cbd88da-0da6-4605-b222-2835c6478304
msc.legacyurl: /mvc/overview/views/dynamic-v-strongly-typed-views
msc.type: authoredcontent
ms.openlocfilehash: 3235fc58fbf93cb87946f8ebd4a478eff7ce80e3
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/17/2019
ms.locfileid: "59386142"
---
# <a name="dynamic-v-strongly-typed-views"></a><span data-ttu-id="5173a-103">Динамические и</span><span class="sxs-lookup"><span data-stu-id="5173a-103">Dynamic v.</span></span> <span data-ttu-id="5173a-104">строго типизированные представления</span><span class="sxs-lookup"><span data-stu-id="5173a-104">Strongly Typed Views</span></span>

<span data-ttu-id="5173a-105">по [Рик Андерсон]((https://twitter.com/RickAndMSFT))</span><span class="sxs-lookup"><span data-stu-id="5173a-105">by [Rick Anderson]((https://twitter.com/RickAndMSFT))</span></span>

<span data-ttu-id="5173a-106">Существует три способа для передачи данных из контроллера в представление в ASP.NET MVC 3:</span><span class="sxs-lookup"><span data-stu-id="5173a-106">There are three ways to pass information from a controller to a view in ASP.NET MVC 3:</span></span>

1. <span data-ttu-id="5173a-107">В виде строго типизированной модели объекта.</span><span class="sxs-lookup"><span data-stu-id="5173a-107">As a strongly typed model object.</span></span>
2. <span data-ttu-id="5173a-108">Как динамический тип (с помощью @model динамические)</span><span class="sxs-lookup"><span data-stu-id="5173a-108">As a dynamic type (using @model dynamic)</span></span>
3. <span data-ttu-id="5173a-109">Использование ViewBag</span><span class="sxs-lookup"><span data-stu-id="5173a-109">Using the ViewBag</span></span>

<span data-ttu-id="5173a-110">Я написал простое приложение MVC 3 верхней блога для сравнения и сравните динамические и строго типизированные представления.</span><span class="sxs-lookup"><span data-stu-id="5173a-110">I've written a simple MVC 3 Top Blog application to compare and contrast dynamic and strongly typed views.</span></span> <span data-ttu-id="5173a-111">Контроллер начинается с простой список блогов:</span><span class="sxs-lookup"><span data-stu-id="5173a-111">The controller starts out with a simple list of blogs:</span></span>

[!code-csharp[Main](dynamic-v-strongly-typed-views/samples/sample1.cs)]

<span data-ttu-id="5173a-112">Щелкните правой кнопкой мыши в методе IndexNotStonglyTyped() и добавить представление Razor.</span><span class="sxs-lookup"><span data-stu-id="5173a-112">Right click in the IndexNotStonglyTyped() method and add a Razor view.</span></span>

<span data-ttu-id="5173a-113">[![8475.NotStronglyTypedView[1]](dynamic-v-strongly-typed-views/_static/image2.png)](dynamic-v-strongly-typed-views/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="5173a-113">[![8475.NotStronglyTypedView[1]](dynamic-v-strongly-typed-views/_static/image2.png)](dynamic-v-strongly-typed-views/_static/image1.png)</span></span>

<span data-ttu-id="5173a-114">Убедитесь, что **создать строго типизированное представление** флажок не установлен.</span><span class="sxs-lookup"><span data-stu-id="5173a-114">Make sure the **Create a strongly-typed view** box is not checked.</span></span> <span data-ttu-id="5173a-115">Результирующее представление не содержат множество:</span><span class="sxs-lookup"><span data-stu-id="5173a-115">The resulting view doesn't contain much:</span></span>

[!code-cshtml[Main](dynamic-v-strongly-typed-views/samples/sample2.cshtml)]

[!code-cshtml[Main](dynamic-v-strongly-typed-views/samples/sample3.cshtml)]

<span data-ttu-id="5173a-116">Поскольку мы используем динамический и не строго типизированного представления, intellisense не помогают.</span><span class="sxs-lookup"><span data-stu-id="5173a-116">Because we're using a dynamic and not a strongly typed view, intellisense doesn't help us.</span></span> <span data-ttu-id="5173a-117">Ниже приведен полный код:</span><span class="sxs-lookup"><span data-stu-id="5173a-117">The completed code is shown below:</span></span>

[!code-cshtml[Main](dynamic-v-strongly-typed-views/samples/sample4.cshtml)]

<span data-ttu-id="5173a-118">[![6646.NotStronglyTypedView_5F00_IE[1]](dynamic-v-strongly-typed-views/_static/image4.png)](dynamic-v-strongly-typed-views/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="5173a-118">[![6646.NotStronglyTypedView_5F00_IE[1]](dynamic-v-strongly-typed-views/_static/image4.png)](dynamic-v-strongly-typed-views/_static/image3.png)</span></span>

<span data-ttu-id="5173a-119">Теперь мы добавим строго типизированного представления.</span><span class="sxs-lookup"><span data-stu-id="5173a-119">Now we'll add a strongly typed view.</span></span> <span data-ttu-id="5173a-120">Добавьте следующий код в контроллер:</span><span class="sxs-lookup"><span data-stu-id="5173a-120">Add the following code to the controller:</span></span>

[!code-csharp[Main](dynamic-v-strongly-typed-views/samples/sample5.cs)]


<span data-ttu-id="5173a-121">Обратите внимание, что это точно тем же возвращаемое View(topBlogs); вызывать как не строго типизированного представления.</span><span class="sxs-lookup"><span data-stu-id="5173a-121">Notice it's exactly the same return View(topBlogs); call as the non-strongly typed view.</span></span> <span data-ttu-id="5173a-122">Щелкните правой кнопкой мыши внутри элемента *StonglyTypedIndex()* и выберите **Добавление представления**.</span><span class="sxs-lookup"><span data-stu-id="5173a-122">Right click inside of *StonglyTypedIndex()* and select **Add View**.</span></span> <span data-ttu-id="5173a-123">На этот раз выберите **блог** класс модели и выберите **списка** как шаблон каркаса.</span><span class="sxs-lookup"><span data-stu-id="5173a-123">This time select the **Blog** Model class and select **List** as the Scaffold template.</span></span>

<span data-ttu-id="5173a-124">[![5658.StrongView [1]](dynamic-v-strongly-typed-views/_static/image6.png)](dynamic-v-strongly-typed-views/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="5173a-124">[![5658.StrongView[1]](dynamic-v-strongly-typed-views/_static/image6.png)](dynamic-v-strongly-typed-views/_static/image5.png)</span></span>

<span data-ttu-id="5173a-125">В новый шаблон представления мы обеспечить поддержку intellisense.</span><span class="sxs-lookup"><span data-stu-id="5173a-125">Inside the new view template we get intellisense support.</span></span>

<span data-ttu-id="5173a-126">[![7002.IntelliSense[1]](dynamic-v-strongly-typed-views/_static/image8.png)](dynamic-v-strongly-typed-views/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="5173a-126">[![7002.IntelliSense[1]](dynamic-v-strongly-typed-views/_static/image8.png)](dynamic-v-strongly-typed-views/_static/image7.png)</span></span>

<span data-ttu-id="5173a-127">Можно загрузить проект c# [здесь](https://blogs.msdn.com/cfs-file.ashx/__key/CommunityServer-Blogs-Components-WeblogFiles/00-00-01-11-73-SSMS/1817.Mvc3ViewDemo.zip).</span><span class="sxs-lookup"><span data-stu-id="5173a-127">The c# project can be downloaded [here](https://blogs.msdn.com/cfs-file.ashx/__key/CommunityServer-Blogs-Components-WeblogFiles/00-00-01-11-73-SSMS/1817.Mvc3ViewDemo.zip).</span></span>
