---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-an-action-cs
title: Создание действия (C#) | Документация Майкрософт
author: microsoft
description: Узнайте, как добавить новое действие в контроллер MVC ASP.NET. Сведения о требованиях к методу для действия.
ms.author: riande
ms.date: 03/02/2009
ms.assetid: cb33b28c-3025-4bd1-a1fa-eaa3af7bb56f
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-an-action-cs
msc.type: authoredcontent
ms.openlocfilehash: ebba935383819935ad85c95245666f4eaf6a0dca
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78470202"
---
# <a name="creating-an-action-c"></a><span data-ttu-id="096dc-104">Создание действия (C#)</span><span class="sxs-lookup"><span data-stu-id="096dc-104">Creating an Action (C#)</span></span>

<span data-ttu-id="096dc-105">по [Майкрософт](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="096dc-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="096dc-106">Узнайте, как добавить новое действие в контроллер MVC ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="096dc-106">Learn how to add a new action to an ASP.NET MVC controller.</span></span> <span data-ttu-id="096dc-107">Сведения о требованиях к методу для действия.</span><span class="sxs-lookup"><span data-stu-id="096dc-107">Learn about the requirements for a method to be an action.</span></span>

<span data-ttu-id="096dc-108">Цель этого учебника — объяснить, как можно создать новое действие контроллера.</span><span class="sxs-lookup"><span data-stu-id="096dc-108">The goal of this tutorial is to explain how you can create a new controller action.</span></span> <span data-ttu-id="096dc-109">Вы узнаете о требованиях к методу действия.</span><span class="sxs-lookup"><span data-stu-id="096dc-109">You learn about the requirements of an action method.</span></span> <span data-ttu-id="096dc-110">Вы также узнаете, как запретить доступ к методу в качестве действия.</span><span class="sxs-lookup"><span data-stu-id="096dc-110">You also learn how to prevent a method from being exposed as an action.</span></span>

## <a name="adding-an-action-to-a-controller"></a><span data-ttu-id="096dc-111">Добавление действия к контроллеру</span><span class="sxs-lookup"><span data-stu-id="096dc-111">Adding an Action to a Controller</span></span>

<span data-ttu-id="096dc-112">Новое действие добавляется к контроллеру путем добавления нового метода к контроллеру.</span><span class="sxs-lookup"><span data-stu-id="096dc-112">You add a new action to a controller by adding a new method to the controller.</span></span> <span data-ttu-id="096dc-113">Например, контроллер в листинге 1 содержит действие с именем index () и действие с именем SayHello ().</span><span class="sxs-lookup"><span data-stu-id="096dc-113">For example, the controller in Listing 1 contains an action named Index() and an action named SayHello().</span></span> <span data-ttu-id="096dc-114">Оба метода предоставляются как действия.</span><span class="sxs-lookup"><span data-stu-id="096dc-114">Both methods are exposed as actions.</span></span>

<span data-ttu-id="096dc-115">**Листинг 1. Controllers\HomeController.cs**</span><span class="sxs-lookup"><span data-stu-id="096dc-115">**Listing 1 - Controllers\HomeController.cs**</span></span>

[!code-csharp[Main](creating-an-action-cs/samples/sample1.cs)]

<span data-ttu-id="096dc-116">Чтобы обеспечить доступ к Вселенной в качестве действия, метод должен отвечать определенным требованиям:</span><span class="sxs-lookup"><span data-stu-id="096dc-116">In order to be exposed to the universe as an action, a method must meet certain requirements:</span></span>

- <span data-ttu-id="096dc-117">Метод должен быть открытым.</span><span class="sxs-lookup"><span data-stu-id="096dc-117">The method must be public.</span></span>
- <span data-ttu-id="096dc-118">Метод не может быть статическим методом.</span><span class="sxs-lookup"><span data-stu-id="096dc-118">The method cannot be a static method.</span></span>
- <span data-ttu-id="096dc-119">Метод не может быть методом расширения.</span><span class="sxs-lookup"><span data-stu-id="096dc-119">The method cannot be an extension method.</span></span>
- <span data-ttu-id="096dc-120">Метод не может быть конструктором, методом считывания или Setter.</span><span class="sxs-lookup"><span data-stu-id="096dc-120">The method cannot be a constructor, getter, or setter.</span></span>
- <span data-ttu-id="096dc-121">Метод не может иметь открытые универсальные типы.</span><span class="sxs-lookup"><span data-stu-id="096dc-121">The method cannot have open generic types.</span></span>
- <span data-ttu-id="096dc-122">Метод не является методом базового класса контроллера.</span><span class="sxs-lookup"><span data-stu-id="096dc-122">The method is not a method of the controller base class.</span></span>
- <span data-ttu-id="096dc-123">Метод не может содержать параметры **ref** или **out** .</span><span class="sxs-lookup"><span data-stu-id="096dc-123">The method cannot contain **ref** or **out** parameters.</span></span>

<span data-ttu-id="096dc-124">Обратите внимание, что нет ограничений на возвращаемый тип действия контроллера.</span><span class="sxs-lookup"><span data-stu-id="096dc-124">Notice that there are no restrictions on the return type of a controller action.</span></span> <span data-ttu-id="096dc-125">Действие контроллера может возвращать строку, значение типа DateTime, экземпляр класса Random или void.</span><span class="sxs-lookup"><span data-stu-id="096dc-125">A controller action can return a string, a DateTime, an instance of the Random class, or void.</span></span> <span data-ttu-id="096dc-126">Платформа ASP.NET MVC преобразует любой тип возвращаемого значения, который не является результатом действия, в строку и подготавливает строку к просмотру в браузере.</span><span class="sxs-lookup"><span data-stu-id="096dc-126">The ASP.NET MVC framework will convert any return type that is not an action result into a string and render the string to the browser.</span></span>

<span data-ttu-id="096dc-127">При добавлении любого метода, который не нарушает эти требования, метод предоставляется как действие контроллера.</span><span class="sxs-lookup"><span data-stu-id="096dc-127">When you add any method that does not violate these requirements to a controller, the method is exposed as a controller action.</span></span> <span data-ttu-id="096dc-128">Будьте внимательны.</span><span class="sxs-lookup"><span data-stu-id="096dc-128">Be careful here.</span></span> <span data-ttu-id="096dc-129">Действие контроллера может быть вызвано любым пользователем, подключенным к Интернету.</span><span class="sxs-lookup"><span data-stu-id="096dc-129">A controller action can be invoked by anyone connected to the Internet.</span></span> <span data-ttu-id="096dc-130">Не следует, например, создать действие контроллера Делетемивебсите ().</span><span class="sxs-lookup"><span data-stu-id="096dc-130">Do not, for example, create a DeleteMyWebsite() controller action.</span></span>

## <a name="preventing-a-public-method-from-being-invoked"></a><span data-ttu-id="096dc-131">Предотвращение вызова открытого метода</span><span class="sxs-lookup"><span data-stu-id="096dc-131">Preventing a Public Method from Being Invoked</span></span>

<span data-ttu-id="096dc-132">Если необходимо создать открытый метод в классе контроллера и вы не хотите предоставлять этот метод как действие контроллера, можно предотвратить вызов метода с помощью атрибута [unaction].</span><span class="sxs-lookup"><span data-stu-id="096dc-132">If you need to create a public method in a controller class and you don't want to expose the method as a controller action then you can prevent the method from being invoked by using the [NonAction] attribute.</span></span> <span data-ttu-id="096dc-133">Например, контроллер в листинге 2 содержит открытый метод с именем Компанисекретс (), дополненный атрибутом [unaction].</span><span class="sxs-lookup"><span data-stu-id="096dc-133">For example, the controller in Listing 2 contains a public method named CompanySecrets() that is decorated with the [NonAction] attribute.</span></span>

<span data-ttu-id="096dc-134">**Листинг 2. Контроллерс\воркконтроллер.КС**</span><span class="sxs-lookup"><span data-stu-id="096dc-134">**Listing 2 - Controllers\WorkController.cs**</span></span>

[!code-csharp[Main](creating-an-action-cs/samples/sample2.cs)]

<span data-ttu-id="096dc-135">Если вы попытаетесь вызвать действие контроллера Компанисекретс (), введя/Ворк/компанисекретс в адресной строке браузера, вы получите сообщение об ошибке на рис. 1.</span><span class="sxs-lookup"><span data-stu-id="096dc-135">If you attempt to invoke the CompanySecrets() controller action by typing /Work/CompanySecrets into the address bar of your browser then you'll get the error message in Figure 1.</span></span>

<span data-ttu-id="096dc-136">[![вызова метода, не вызывающего действия](creating-an-action-cs/_static/image1.jpg)](creating-an-action-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="096dc-136">[![Invoking a NonAction method](creating-an-action-cs/_static/image1.jpg)](creating-an-action-cs/_static/image1.png)</span></span>

<span data-ttu-id="096dc-137">**Рис. 01**. вызов метода, не[поддерживающего действия (щелкните, чтобы просмотреть изображение с полным размером](creating-an-action-cs/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="096dc-137">**Figure 01**: Invoking a NonAction method([Click to view full-size image](creating-an-action-cs/_static/image2.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="096dc-138">[Назад](creating-a-controller-cs.md)
> [Вперед](asp-net-mvc-routing-overview-vb.md)</span><span class="sxs-lookup"><span data-stu-id="096dc-138">[Previous](creating-a-controller-cs.md)
[Next](asp-net-mvc-routing-overview-vb.md)</span></span>
