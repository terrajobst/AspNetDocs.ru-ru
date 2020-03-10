---
uid: mvc/overview/older-versions-1/models-data/validating-with-a-service-layer-vb
title: Проверка с помощью слоя служб (VB) | Документация Майкрософт
author: StephenWalther
description: Узнайте, как переместить логику проверки из действий контроллера в отдельный слой служб. В этом руководстве Стивен Вальтер объясняет, как это делать...
ms.author: riande
ms.date: 03/02/2009
ms.assetid: 344bb38e-4965-4c47-bda1-f6d29ae5b83a
msc.legacyurl: /mvc/overview/older-versions-1/models-data/validating-with-a-service-layer-vb
msc.type: authoredcontent
ms.openlocfilehash: 704657ffe6f50eaf3eb0d91d0d334567003ab7f4
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78436578"
---
# <a name="validating-with-a-service-layer-vb"></a><span data-ttu-id="03b1d-104">Проверка с помощью уровня службы (VB)</span><span class="sxs-lookup"><span data-stu-id="03b1d-104">Validating with a Service Layer (VB)</span></span>

<span data-ttu-id="03b1d-105">по [Стивен Вальтер](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="03b1d-105">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

> <span data-ttu-id="03b1d-106">Узнайте, как переместить логику проверки из действий контроллера в отдельный слой служб.</span><span class="sxs-lookup"><span data-stu-id="03b1d-106">Learn how to move your validation logic out of your controller actions and into a separate service layer.</span></span> <span data-ttu-id="03b1d-107">В этом руководстве Стивен Вальтер содержит сведения о том, как можно обеспечить четкое разделение проблем, изолируя уровень службы на уровне контроллера.</span><span class="sxs-lookup"><span data-stu-id="03b1d-107">In this tutorial, Stephen Walther explains how you can maintain a sharp separation of concerns by isolating your service layer from your controller layer.</span></span>

<span data-ttu-id="03b1d-108">Цель этого руководства — описать один метод выполнения проверки в приложении MVC ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="03b1d-108">The goal of this tutorial is to describe one method of performing validation in an ASP.NET MVC application.</span></span> <span data-ttu-id="03b1d-109">В этом руководстве вы узнаете, как переместить логику проверки из контроллеров в отдельный слой служб.</span><span class="sxs-lookup"><span data-stu-id="03b1d-109">In this tutorial, you learn how to move your validation logic out of your controllers and into a separate service layer.</span></span>

## <a name="separating-concerns"></a><span data-ttu-id="03b1d-110">Отделение проблем</span><span class="sxs-lookup"><span data-stu-id="03b1d-110">Separating Concerns</span></span>

<span data-ttu-id="03b1d-111">При создании приложения ASP.NET MVC не следует размещать логику базы данных в действиях контроллера.</span><span class="sxs-lookup"><span data-stu-id="03b1d-111">When you build an ASP.NET MVC application, you should not place your database logic inside your controller actions.</span></span> <span data-ttu-id="03b1d-112">Смешивание базы данных и логики контроллера делает приложение более сложным для обслуживания с течением времени.</span><span class="sxs-lookup"><span data-stu-id="03b1d-112">Mixing your database and controller logic makes your application more difficult to maintain over time.</span></span> <span data-ttu-id="03b1d-113">Рекомендуется размещать всю логику базы данных в отдельном слое репозитория.</span><span class="sxs-lookup"><span data-stu-id="03b1d-113">The recommendation is that you place all of your database logic in a separate repository layer.</span></span>

<span data-ttu-id="03b1d-114">Например, листинг 1 содержит простой репозиторий с именем Продуктрепоситори.</span><span class="sxs-lookup"><span data-stu-id="03b1d-114">For example, Listing 1 contains a simple repository named the ProductRepository.</span></span> <span data-ttu-id="03b1d-115">Репозиторий продукта содержит весь код доступа к данным для приложения.</span><span class="sxs-lookup"><span data-stu-id="03b1d-115">The product repository contains all of the data access code for the application.</span></span> <span data-ttu-id="03b1d-116">В список также входит интерфейс Ипродуктрепоситори, реализованный в репозитории продуктов.</span><span class="sxs-lookup"><span data-stu-id="03b1d-116">The listing also includes the IProductRepository interface that the product repository implements.</span></span>

<span data-ttu-id="03b1d-117">**Листинг 1. Моделс\продуктрепоситори.ВБ**</span><span class="sxs-lookup"><span data-stu-id="03b1d-117">**Listing 1 - Models\ProductRepository.vb**</span></span>

[!code-vb[Main](validating-with-a-service-layer-vb/samples/sample1.vb)]

<span data-ttu-id="03b1d-118">Контроллер в листинге 2 использует слой репозитория в действиях index () и Create ().</span><span class="sxs-lookup"><span data-stu-id="03b1d-118">The controller in Listing 2 uses the repository layer in both its Index() and Create() actions.</span></span> <span data-ttu-id="03b1d-119">Обратите внимание, что этот контроллер не содержит логику базы данных.</span><span class="sxs-lookup"><span data-stu-id="03b1d-119">Notice that this controller does not contain any database logic.</span></span> <span data-ttu-id="03b1d-120">Создание слоя репозитория позволяет поддерживать четкое разделение проблем.</span><span class="sxs-lookup"><span data-stu-id="03b1d-120">Creating a repository layer enables you to maintain a clean separation of concerns.</span></span> <span data-ttu-id="03b1d-121">Контроллеры отвечают за логику управления потоком приложений, и репозиторий отвечает за логику доступа к данным.</span><span class="sxs-lookup"><span data-stu-id="03b1d-121">Controllers are responsible for application flow control logic and the repository is responsible for data access logic.</span></span>

<span data-ttu-id="03b1d-122">**Листинг 2. Контроллерс\продуктконтроллер.ВБ**</span><span class="sxs-lookup"><span data-stu-id="03b1d-122">**Listing 2 - Controllers\ProductController.vb**</span></span>

[!code-vb[Main](validating-with-a-service-layer-vb/samples/sample2.vb)]

## <a name="creating-a-service-layer"></a><span data-ttu-id="03b1d-123">Создание слоя служб</span><span class="sxs-lookup"><span data-stu-id="03b1d-123">Creating a Service Layer</span></span>

<span data-ttu-id="03b1d-124">Таким образом, логика управления потоком приложения принадлежит контроллеру, а логика доступа к данным — в репозитории.</span><span class="sxs-lookup"><span data-stu-id="03b1d-124">So, application flow control logic belongs in a controller and data access logic belongs in a repository.</span></span> <span data-ttu-id="03b1d-125">В этом случае, где вы помещаете логику проверки?</span><span class="sxs-lookup"><span data-stu-id="03b1d-125">In that case, where do you put your validation logic?</span></span> <span data-ttu-id="03b1d-126">Одним из вариантов является размещение логики проверки на *уровне служб*.</span><span class="sxs-lookup"><span data-stu-id="03b1d-126">One option is to place your validation logic in a *service layer*.</span></span>

<span data-ttu-id="03b1d-127">Слой служб — это дополнительный уровень в приложении ASP.NET MVC, исправляет связь между контроллером и слоем репозитория.</span><span class="sxs-lookup"><span data-stu-id="03b1d-127">A service layer is an additional layer in an ASP.NET MVC application that mediates communication between a controller and repository layer.</span></span> <span data-ttu-id="03b1d-128">Слой служб содержит бизнес-логику.</span><span class="sxs-lookup"><span data-stu-id="03b1d-128">The service layer contains business logic.</span></span> <span data-ttu-id="03b1d-129">В частности, он содержит логику проверки.</span><span class="sxs-lookup"><span data-stu-id="03b1d-129">In particular, it contains validation logic.</span></span>

<span data-ttu-id="03b1d-130">Например, уровень службы продукта в листинге 3 имеет метод Креатепродукт ().</span><span class="sxs-lookup"><span data-stu-id="03b1d-130">For example, the product service layer in Listing 3 has a CreateProduct() method.</span></span> <span data-ttu-id="03b1d-131">Метод Креатепродукт () вызывает метод Валидатепродукт () для проверки нового продукта перед передачей продукта в репозиторий продукта.</span><span class="sxs-lookup"><span data-stu-id="03b1d-131">The CreateProduct() method calls the ValidateProduct() method to validate a new product before passing the product to the product repository.</span></span>

<span data-ttu-id="03b1d-132">**Листинг 3. Моделс\продуктсервице.ВБ**</span><span class="sxs-lookup"><span data-stu-id="03b1d-132">**Listing 3 - Models\ProductService.vb**</span></span>

[!code-vb[Main](validating-with-a-service-layer-vb/samples/sample3.vb)]

<span data-ttu-id="03b1d-133">Контроллер продукта был обновлен в листинге 4 для использования слоя служб вместо слоя репозитория.</span><span class="sxs-lookup"><span data-stu-id="03b1d-133">The Product controller has been updated in Listing 4 to use the service layer instead of the repository layer.</span></span> <span data-ttu-id="03b1d-134">Уровень контроллера взаимодействует со слоем служб.</span><span class="sxs-lookup"><span data-stu-id="03b1d-134">The controller layer talks to the service layer.</span></span> <span data-ttu-id="03b1d-135">Слой служб обращается к слою репозитория.</span><span class="sxs-lookup"><span data-stu-id="03b1d-135">The service layer talks to the repository layer.</span></span> <span data-ttu-id="03b1d-136">Каждый уровень имеет отдельную ответственность.</span><span class="sxs-lookup"><span data-stu-id="03b1d-136">Each layer has a separate responsibility.</span></span>

<span data-ttu-id="03b1d-137">**Листинг 4. Контроллерс\продуктконтроллер.ВБ**</span><span class="sxs-lookup"><span data-stu-id="03b1d-137">**Listing 4 - Controllers\ProductController.vb**</span></span>

[!code-vb[Main](validating-with-a-service-layer-vb/samples/sample4.vb)]

<span data-ttu-id="03b1d-138">Обратите внимание, что служба продукта создается в конструкторе контроллера продукта.</span><span class="sxs-lookup"><span data-stu-id="03b1d-138">Notice that the product service is created in the product controller constructor.</span></span> <span data-ttu-id="03b1d-139">При создании службы продукта словарь состояния модели передается в службу.</span><span class="sxs-lookup"><span data-stu-id="03b1d-139">When the product service is created, the model state dictionary is passed to the service.</span></span> <span data-ttu-id="03b1d-140">Служба продукта использует состояние модели для передачи сообщений об ошибках проверки обратно в контроллер.</span><span class="sxs-lookup"><span data-stu-id="03b1d-140">The product service uses model state to pass validation error messages back to the controller.</span></span>

## <a name="decoupling-the-service-layer"></a><span data-ttu-id="03b1d-141">Отделение слоя служб</span><span class="sxs-lookup"><span data-stu-id="03b1d-141">Decoupling the Service Layer</span></span>

<span data-ttu-id="03b1d-142">Не удалось изолировать уровни контроллера и службы в одном отношении.</span><span class="sxs-lookup"><span data-stu-id="03b1d-142">We have failed to isolate the controller and service layers in one respect.</span></span> <span data-ttu-id="03b1d-143">Уровни контроллера и службы взаимодействуют через состояние модели.</span><span class="sxs-lookup"><span data-stu-id="03b1d-143">The controller and service layers communicate through model state.</span></span> <span data-ttu-id="03b1d-144">Иными словами, уровень служб зависит от конкретной функции платформы MVC ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="03b1d-144">In other words, the service layer has a dependency on a particular feature of the ASP.NET MVC framework.</span></span>

<span data-ttu-id="03b1d-145">Мы хотим, чтобы уровень служб был как можно более изолирован от уровня контроллера.</span><span class="sxs-lookup"><span data-stu-id="03b1d-145">We want to isolate the service layer from our controller layer as much as possible.</span></span> <span data-ttu-id="03b1d-146">Теоретически, мы должны иметь возможность использовать слой служб с приложением любого типа, а не только ASP.NET приложение MVC.</span><span class="sxs-lookup"><span data-stu-id="03b1d-146">In theory, we should be able to use the service layer with any type of application and not only an ASP.NET MVC application.</span></span> <span data-ttu-id="03b1d-147">Например, в будущем может потребоваться построить внешний интерфейс WPF для нашего приложения.</span><span class="sxs-lookup"><span data-stu-id="03b1d-147">For example, in the future, we might want to build a WPF front-end for our application.</span></span> <span data-ttu-id="03b1d-148">Мы должны найти способ удаления зависимости от состояния модели MVC ASP.NET из уровня служб.</span><span class="sxs-lookup"><span data-stu-id="03b1d-148">We should find a way to remove the dependency on ASP.NET MVC model state from our service layer.</span></span>

<span data-ttu-id="03b1d-149">В листинге 5 слой служб был обновлен так, чтобы он больше не использовал состояние модели.</span><span class="sxs-lookup"><span data-stu-id="03b1d-149">In Listing 5, the service layer has been updated so that it no longer uses model state.</span></span> <span data-ttu-id="03b1d-150">Вместо этого используется любой класс, реализующий интерфейс Ивалидатиондиктионари.</span><span class="sxs-lookup"><span data-stu-id="03b1d-150">Instead, it uses any class that implements the IValidationDictionary interface.</span></span>

<span data-ttu-id="03b1d-151">**Листинг 5 — Моделс\продуктсервице.ВБ (отделено)**</span><span class="sxs-lookup"><span data-stu-id="03b1d-151">**Listing 5 - Models\ProductService.vb (decoupled)**</span></span>

[!code-vb[Main](validating-with-a-service-layer-vb/samples/sample5.vb)]

<span data-ttu-id="03b1d-152">Интерфейс Ивалидатиондиктионари определен в листинге 6.</span><span class="sxs-lookup"><span data-stu-id="03b1d-152">The IValidationDictionary interface is defined in Listing 6.</span></span> <span data-ttu-id="03b1d-153">Этот простой интерфейс имеет один метод и одно свойство.</span><span class="sxs-lookup"><span data-stu-id="03b1d-153">This simple interface has a single method and a single property.</span></span>

<span data-ttu-id="03b1d-154">**Листинг 6. Моделс\ивалидатиондиктионари.КС**</span><span class="sxs-lookup"><span data-stu-id="03b1d-154">**Listing 6 - Models\IValidationDictionary.cs**</span></span>

[!code-vb[Main](validating-with-a-service-layer-vb/samples/sample6.vb)]

<span data-ttu-id="03b1d-155">Класс в листинге 7 с именем класса Моделстатевраппер реализует интерфейс Ивалидатиондиктионари.</span><span class="sxs-lookup"><span data-stu-id="03b1d-155">The class in Listing 7, named the ModelStateWrapper class, implements the IValidationDictionary interface.</span></span> <span data-ttu-id="03b1d-156">Можно создать экземпляр класса Моделстатевраппер, передав в конструктор словарь состояния модели.</span><span class="sxs-lookup"><span data-stu-id="03b1d-156">You can instantiate the ModelStateWrapper class by passing a model state dictionary to the constructor.</span></span>

<span data-ttu-id="03b1d-157">**Листинг 7 — Моделс\моделстатевраппер.ВБ**</span><span class="sxs-lookup"><span data-stu-id="03b1d-157">**Listing 7 - Models\ModelStateWrapper.vb**</span></span>

[!code-vb[Main](validating-with-a-service-layer-vb/samples/sample7.vb)]

<span data-ttu-id="03b1d-158">Наконец, обновленный контроллер в листинге 8 использует Моделстатевраппер при создании слоя служб в конструкторе.</span><span class="sxs-lookup"><span data-stu-id="03b1d-158">Finally, the updated controller in Listing 8 uses the ModelStateWrapper when creating the service layer in its constructor.</span></span>

<span data-ttu-id="03b1d-159">**Листинг 8. Контроллерс\продуктконтроллер.ВБ**</span><span class="sxs-lookup"><span data-stu-id="03b1d-159">**Listing 8 - Controllers\ProductController.vb**</span></span>

[!code-vb[Main](validating-with-a-service-layer-vb/samples/sample8.vb)]

<span data-ttu-id="03b1d-160">Использование интерфейса Ивалидатиондиктионари и класса Моделстатевраппер позволяет полностью изолировать наш уровень служб от нашего уровня контроллера.</span><span class="sxs-lookup"><span data-stu-id="03b1d-160">Using the IValidationDictionary interface and the ModelStateWrapper class enables us to completely isolate our service layer from our controller layer.</span></span> <span data-ttu-id="03b1d-161">Уровень службы больше не зависит от состояния модели.</span><span class="sxs-lookup"><span data-stu-id="03b1d-161">The service layer is no longer dependent on model state.</span></span> <span data-ttu-id="03b1d-162">Можно передать любой класс, реализующий интерфейс Ивалидатиондиктионари, в слой службы.</span><span class="sxs-lookup"><span data-stu-id="03b1d-162">You can pass any class that implements the IValidationDictionary interface to the service layer.</span></span> <span data-ttu-id="03b1d-163">Например, приложение WPF может реализовать интерфейс Ивалидатиондиктионари с помощью простого класса коллекции.</span><span class="sxs-lookup"><span data-stu-id="03b1d-163">For example, a WPF application might implement the IValidationDictionary interface with a simple collection class.</span></span>

## <a name="summary"></a><span data-ttu-id="03b1d-164">Сводка</span><span class="sxs-lookup"><span data-stu-id="03b1d-164">Summary</span></span>

<span data-ttu-id="03b1d-165">Цель этого учебника — обсудить один из подходов к выполнению проверки в приложении ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="03b1d-165">The goal of this tutorial was to discuss one approach to performing validation in an ASP.NET MVC application.</span></span> <span data-ttu-id="03b1d-166">В этом руководстве вы узнали, как переместить всю логику проверки из контроллеров в отдельный слой служб.</span><span class="sxs-lookup"><span data-stu-id="03b1d-166">In this tutorial, you learned how to move all of your validation logic out of your controllers and into a separate service layer.</span></span> <span data-ttu-id="03b1d-167">Вы также узнали, как изолировать слой служб от своего уровня контроллера, создав класс Моделстатевраппер.</span><span class="sxs-lookup"><span data-stu-id="03b1d-167">You also learned how to isolate your service layer from your controller layer by creating a ModelStateWrapper class.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="03b1d-168">[Назад](validating-with-the-idataerrorinfo-interface-vb.md)
> [Вперед](validation-with-the-data-annotation-validators-vb.md)</span><span class="sxs-lookup"><span data-stu-id="03b1d-168">[Previous](validating-with-the-idataerrorinfo-interface-vb.md)
[Next](validation-with-the-data-annotation-validators-vb.md)</span></span>
