---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-a-controller-vb
title: Создание контроллера (VB) | Документация Майкрософт
author: StephenWalther
description: В этом руководстве Стивен Вальтер демонстрирует, как можно добавить контроллер в приложение ASP.NET MVC.
ms.author: riande
ms.date: 03/02/2009
ms.assetid: 204b7e86-f560-4611-8adb-785b33e777b9
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-a-controller-vb
msc.type: authoredcontent
ms.openlocfilehash: 60636b79ab5fc06ca904dee90ce74f256e046d12
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78486834"
---
# <a name="creating-a-controller-vb"></a><span data-ttu-id="5a5d9-103">Создание контроллера (VB)</span><span class="sxs-lookup"><span data-stu-id="5a5d9-103">Creating a Controller (VB)</span></span>

<span data-ttu-id="5a5d9-104">по [Стивен Вальтер](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="5a5d9-104">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

> <span data-ttu-id="5a5d9-105">В этом руководстве Стивен Вальтер демонстрирует, как можно добавить контроллер в приложение ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="5a5d9-105">In this tutorial, Stephen Walther demonstrates how you can add a controller to an ASP.NET MVC application.</span></span>

<span data-ttu-id="5a5d9-106">Цель этого учебника — объяснить, как можно создавать новые контроллеры MVC ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="5a5d9-106">The goal of this tutorial is to explain how you can create new ASP.NET MVC controllers.</span></span> <span data-ttu-id="5a5d9-107">Вы узнаете, как создавать контроллеры с помощью меню добавления контроллера в Visual Studio, а также путем создания файла класса вручную.</span><span class="sxs-lookup"><span data-stu-id="5a5d9-107">You learn how to create controllers both by using the Visual Studio Add Controller menu option and by creating a class file by hand.</span></span>

### <a name="using-the-add-controller-menu-option"></a><span data-ttu-id="5a5d9-108">Использование команды меню "добавить контроллер"</span><span class="sxs-lookup"><span data-stu-id="5a5d9-108">Using the Add Controller Menu Option</span></span>

<span data-ttu-id="5a5d9-109">Самый простой способ создать новый контроллер — щелкнуть правой кнопкой мыши папку Controllers в окне обозреватель решений Visual Studio и выбрать пункт меню **Добавить, контроллер** (см. рис. 1).</span><span class="sxs-lookup"><span data-stu-id="5a5d9-109">The easiest way to create a new controller is to right-click the Controllers folder in the Visual Studio Solution Explorer window and select the **Add, Controller** menu option (see Figure 1).</span></span> <span data-ttu-id="5a5d9-110">При выборе этого пункта меню открывается диалоговое окно **Добавление контроллера** (см. рис. 2).</span><span class="sxs-lookup"><span data-stu-id="5a5d9-110">Selecting this menu option opens the **Add Controller** dialog (see Figure 2).</span></span>

<span data-ttu-id="5a5d9-111">[![диалоговом окне «Создание проекта»](creating-a-controller-vb/_static/image1.jpg)](creating-a-controller-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="5a5d9-111">[![The New Project dialog box](creating-a-controller-vb/_static/image1.jpg)](creating-a-controller-vb/_static/image1.png)</span></span>

<span data-ttu-id="5a5d9-112">**Рис. 01**. Добавление нового контроллера ([щелкните, чтобы просмотреть изображение с полным размером](creating-a-controller-vb/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="5a5d9-112">**Figure 01**: Adding a new controller([Click to view full-size image](creating-a-controller-vb/_static/image2.png))</span></span>

<span data-ttu-id="5a5d9-113">[![диалоговом окне «Создание проекта»](creating-a-controller-vb/_static/image2.jpg)](creating-a-controller-vb/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="5a5d9-113">[![The New Project dialog box](creating-a-controller-vb/_static/image2.jpg)](creating-a-controller-vb/_static/image3.png)</span></span>

<span data-ttu-id="5a5d9-114">**Рис. 02**. диалоговое окно добавления контроллера ([щелкните, чтобы просмотреть изображение с полным размером](creating-a-controller-vb/_static/image4.png))</span><span class="sxs-lookup"><span data-stu-id="5a5d9-114">**Figure 02**: The Add Controller dialog ([Click to view full-size image](creating-a-controller-vb/_static/image4.png))</span></span>

<span data-ttu-id="5a5d9-115">Обратите внимание, что первая часть имени контроллера выделена в диалоговом окне **Добавление контроллера** .</span><span class="sxs-lookup"><span data-stu-id="5a5d9-115">Notice that the first part of the controller name is highlighted in the **Add Controller** dialog.</span></span> <span data-ttu-id="5a5d9-116">Имя каждого контроллера должно заканчиваться *контроллером*суффикса.</span><span class="sxs-lookup"><span data-stu-id="5a5d9-116">Every controller name must end with the suffix *Controller*.</span></span> <span data-ttu-id="5a5d9-117">Например, можно создать контроллер с именем *продуктконтроллер* , но не контроллер с именем *Product*.</span><span class="sxs-lookup"><span data-stu-id="5a5d9-117">For example, you can create a controller named *ProductController* but not a controller named *Product*.</span></span>

<span data-ttu-id="5a5d9-118">Если вы создаете контроллер, в котором отсутствует суффикс *контроллера* , вы не сможете вызвать контроллер.</span><span class="sxs-lookup"><span data-stu-id="5a5d9-118">If you create a controller that is missing the *Controller* suffix then you won't be able to invoke the controller.</span></span> <span data-ttu-id="5a5d9-119">Не делать этого — я не сталкивался с бесчисленным временем жизни моего жизненного цикла после выполнения этой ошибки.</span><span class="sxs-lookup"><span data-stu-id="5a5d9-119">Don't do this -- I've wasted countless hours of my life after making this mistake.</span></span>

<span data-ttu-id="5a5d9-120">**Листинг 1. Контроллерс\продуктконтроллер.ВБ**</span><span class="sxs-lookup"><span data-stu-id="5a5d9-120">**Listing 1 - Controllers\ProductController.vb**</span></span>

[!code-vb[Main](creating-a-controller-vb/samples/sample1.vb)]

<span data-ttu-id="5a5d9-121">Контроллеры всегда должны создаваться в папке Controllers.</span><span class="sxs-lookup"><span data-stu-id="5a5d9-121">You should always create controllers in the Controllers folder.</span></span> <span data-ttu-id="5a5d9-122">В противном случае вы будете нарушать соглашения ASP.NET MVC, и другие разработчики будут иметь более трудное понимание своего приложения.</span><span class="sxs-lookup"><span data-stu-id="5a5d9-122">Otherwise, you'll be violating the conventions of ASP.NET MVC and other developers will have a more difficult time understanding your application.</span></span>

### <a name="scaffolding-action-methods"></a><span data-ttu-id="5a5d9-123">Методы действий формирования шаблонов</span><span class="sxs-lookup"><span data-stu-id="5a5d9-123">Scaffolding Action Methods</span></span>

<span data-ttu-id="5a5d9-124">При создании контроллера у вас есть возможность автоматически создавать, обновлять и подробных методов действий (см. рис. 3).</span><span class="sxs-lookup"><span data-stu-id="5a5d9-124">When you create a controller, you have the option to generate Create, Update, and Details action methods automatically (see Figure 3).</span></span> <span data-ttu-id="5a5d9-125">При выборе этого параметра создается класс контроллера в листинге 2.</span><span class="sxs-lookup"><span data-stu-id="5a5d9-125">If you select this option then the controller class in Listing 2 is generated.</span></span>

<span data-ttu-id="5a5d9-126">[![автоматическое создание методов действий](creating-a-controller-vb/_static/image3.jpg)](creating-a-controller-vb/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="5a5d9-126">[![Creating action methods automatically](creating-a-controller-vb/_static/image3.jpg)](creating-a-controller-vb/_static/image5.png)</span></span>

<span data-ttu-id="5a5d9-127">**Рис. 03**. Автоматическое создание методов действий ([щелкните, чтобы просмотреть изображение с полным размером](creating-a-controller-vb/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="5a5d9-127">**Figure 03**: Creating action methods automatically ([Click to view full-size image](creating-a-controller-vb/_static/image6.png))</span></span>

<span data-ttu-id="5a5d9-128">**Листинг 2. Контроллерс\кустомерконтроллер.ВБ**</span><span class="sxs-lookup"><span data-stu-id="5a5d9-128">**Listing 2 - Controllers\CustomerController.vb**</span></span>

[!code-vb[Main](creating-a-controller-vb/samples/sample2.vb)]

<span data-ttu-id="5a5d9-129">Эти созданные методы являются методами-заглушками.</span><span class="sxs-lookup"><span data-stu-id="5a5d9-129">These generated methods are stub methods.</span></span> <span data-ttu-id="5a5d9-130">Необходимо добавить собственно логику для создания, обновления и отображения подробных сведений для клиента.</span><span class="sxs-lookup"><span data-stu-id="5a5d9-130">You must add the actual logic for creating, updating, and showing details for a customer yourself.</span></span> <span data-ttu-id="5a5d9-131">Но методы-заглушки предоставляют удобную отправную точку.</span><span class="sxs-lookup"><span data-stu-id="5a5d9-131">But, the stub methods provide you with a nice starting point.</span></span>

### <a name="creating-a-controller-class"></a><span data-ttu-id="5a5d9-132">Создание класса контроллера</span><span class="sxs-lookup"><span data-stu-id="5a5d9-132">Creating a Controller Class</span></span>

<span data-ttu-id="5a5d9-133">Контроллер MVC ASP.NET — это просто класс.</span><span class="sxs-lookup"><span data-stu-id="5a5d9-133">The ASP.NET MVC controller is just a class.</span></span> <span data-ttu-id="5a5d9-134">Если вы предпочитаете, вы можете проигнорировать удобный набор шаблонов контроллера Visual Studio и создать класс контроллера вручную.</span><span class="sxs-lookup"><span data-stu-id="5a5d9-134">If you prefer, you can ignore the convenient Visual Studio controller scaffolding and create a controller class by hand.</span></span> <span data-ttu-id="5a5d9-135">Выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="5a5d9-135">Follow these steps:</span></span>

1. <span data-ttu-id="5a5d9-136">Щелкните правой кнопкой мыши папку Controllers и выберите пункт меню **Добавить, новый элемент** и выберите шаблон **класса** (см. рис. 4).</span><span class="sxs-lookup"><span data-stu-id="5a5d9-136">Right-click the Controllers folder and select the menu option **Add, New Item** and select the **Class** template (see Figure 4).</span></span>
2. <span data-ttu-id="5a5d9-137">Назовите новый класс Персонконтроллер. vb и нажмите кнопку **Добавить** .</span><span class="sxs-lookup"><span data-stu-id="5a5d9-137">Name the new class PersonController.vb and click the **Add** button.</span></span>
3. <span data-ttu-id="5a5d9-138">Измените результирующий файл класса таким образом, чтобы класс наследовался от базового класса System. Web. MVC. Controller (см. листинг 3).</span><span class="sxs-lookup"><span data-stu-id="5a5d9-138">Modify the resulting class file so that the class inherits from the base System.Web.Mvc.Controller class (see Listing 3).</span></span>

<span data-ttu-id="5a5d9-139">[![создания нового класса](creating-a-controller-vb/_static/image4.jpg)](creating-a-controller-vb/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="5a5d9-139">[![Creating a new class](creating-a-controller-vb/_static/image4.jpg)](creating-a-controller-vb/_static/image7.png)</span></span>

<span data-ttu-id="5a5d9-140">**Рис. 04**. Создание нового класса ([щелкните, чтобы просмотреть изображение с полным размером](creating-a-controller-vb/_static/image8.png))</span><span class="sxs-lookup"><span data-stu-id="5a5d9-140">**Figure 04**: Creating a new class([Click to view full-size image](creating-a-controller-vb/_static/image8.png))</span></span>

<span data-ttu-id="5a5d9-141">**Листинг 3. Контроллерс\персонконтроллер.ВБ**</span><span class="sxs-lookup"><span data-stu-id="5a5d9-141">**Listing 3 - Controllers\PersonController.vb**</span></span>

[!code-vb[Main](creating-a-controller-vb/samples/sample3.vb)]

<span data-ttu-id="5a5d9-142">Контроллер в листинге 3 предоставляет одно действие с именем index (), которое возвращает строку "Hello World!".</span><span class="sxs-lookup"><span data-stu-id="5a5d9-142">The controller in Listing 3 exposes one action named Index() that returns the string "Hello World!".</span></span> <span data-ttu-id="5a5d9-143">Это действие контроллера можно вызвать, запустив приложение и запрашивая URL-адрес следующего вида:</span><span class="sxs-lookup"><span data-stu-id="5a5d9-143">You can invoke this controller action by running your application and requesting a URL like the following:</span></span>

`http://localhost:40071/Person`

> [!NOTE]
> 
> <span data-ttu-id="5a5d9-144">В ASP.NET Development Server используется случайный номер порта (например, 40071).</span><span class="sxs-lookup"><span data-stu-id="5a5d9-144">The ASP.NET Development Server uses a random port number (for example, 40071).</span></span> <span data-ttu-id="5a5d9-145">При вводе URL-адреса для вызова контроллера необходимо указать правильный номер порта.</span><span class="sxs-lookup"><span data-stu-id="5a5d9-145">When entering a URL to invoke a controller, you'll need to supply the right port number.</span></span> <span data-ttu-id="5a5d9-146">Номер порта можно определить, наведя указатель мыши на значок ASP.NET Development Server в области уведомлений Windows (в правом нижнем углу экрана).</span><span class="sxs-lookup"><span data-stu-id="5a5d9-146">You can determine the port number by hovering your mouse over the icon for the ASP.NET Development Server in the Windows Notification Area (bottom-right of your screen).</span></span>
> 
> [!div class="step-by-step"]
> <span data-ttu-id="5a5d9-147">[Назад](adding-dynamic-content-to-a-cached-page-vb.md)
> [Вперед](creating-an-action-vb.md)</span><span class="sxs-lookup"><span data-stu-id="5a5d9-147">[Previous](adding-dynamic-content-to-a-cached-page-vb.md)
[Next](creating-an-action-vb.md)</span></span>
