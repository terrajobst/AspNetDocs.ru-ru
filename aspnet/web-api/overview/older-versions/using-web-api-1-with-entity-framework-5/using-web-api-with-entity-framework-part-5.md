---
uid: web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-5
title: Часть 5. Создание динамического пользовательского интерфейса с помощью маскирования. js | Документация Майкрософт
author: MikeWasson
description: ''
ms.author: riande
ms.date: 07/04/2012
ms.assetid: 9d9cb3b0-f4a7-434e-a508-9fc0ad0eb813
msc.legacyurl: /web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-5
msc.type: authoredcontent
ms.openlocfilehash: bbdeba756de7986cfeb92aa10a57f4f101382f99
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/28/2019
ms.locfileid: "74599997"
---
# <a name="part-5-creating-a-dynamic-ui-with-knockoutjs"></a><span data-ttu-id="05457-102">Часть 5. Создание динамического пользовательского интерфейса с помощью маскирования. js</span><span class="sxs-lookup"><span data-stu-id="05457-102">Part 5: Creating a Dynamic UI with Knockout.js</span></span>

<span data-ttu-id="05457-103">по [Майк Уоссон](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="05457-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="05457-104">Скачать завершенный проект</span><span class="sxs-lookup"><span data-stu-id="05457-104">Download Completed Project</span></span>](https://code.msdn.microsoft.com/ASP-NET-Web-API-with-afa30545)

## <a name="creating-a-dynamic-ui-with-knockoutjs"></a><span data-ttu-id="05457-105">Создание динамического пользовательского интерфейса с помощью Knockout.js</span><span class="sxs-lookup"><span data-stu-id="05457-105">Creating a Dynamic UI with Knockout.js</span></span>

<span data-ttu-id="05457-106">В этом разделе мы будем использовать маскирование. js для добавления функциональных возможностей в административное представление.</span><span class="sxs-lookup"><span data-stu-id="05457-106">In this section, we'll use Knockout.js to add functionality to the Admin view.</span></span>

<span data-ttu-id="05457-107">[Выколачивание. js](http://knockoutjs.com/) — это библиотека JavaScript, которая позволяет легко привязывать элементы управления HTML к данным.</span><span class="sxs-lookup"><span data-stu-id="05457-107">[Knockout.js](http://knockoutjs.com/) is a Javascript library that makes it easy to bind HTML controls to data.</span></span> <span data-ttu-id="05457-108">В маскировании. js используется шаблон Model-View-ViewModel (MVVM).</span><span class="sxs-lookup"><span data-stu-id="05457-108">Knockout.js uses the Model-View-ViewModel (MVVM) pattern.</span></span>

- <span data-ttu-id="05457-109">*Модель* — это серверное представление данных в бизнес-домене (в нашем случае это продукты и заказы).</span><span class="sxs-lookup"><span data-stu-id="05457-109">The *model* is the server-side representation of the data in the business domain (in our case, products and orders).</span></span>
- <span data-ttu-id="05457-110">*Представление* — это уровень представления (HTML).</span><span class="sxs-lookup"><span data-stu-id="05457-110">The *view* is the presentation layer (HTML).</span></span>
- <span data-ttu-id="05457-111">*Модель представления* — это объект JavaScript, который содержит данные модели.</span><span class="sxs-lookup"><span data-stu-id="05457-111">The *view-model* is a Javascript object that holds the model data.</span></span> <span data-ttu-id="05457-112">Модель представления — это абстракция кода пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="05457-112">The view-model is a code abstraction of the UI.</span></span> <span data-ttu-id="05457-113">Он не имеет сведений о представлении HTML.</span><span class="sxs-lookup"><span data-stu-id="05457-113">It has no knowledge of the HTML representation.</span></span> <span data-ttu-id="05457-114">Вместо этого он представляет абстрактные функции представления, например "список элементов".</span><span class="sxs-lookup"><span data-stu-id="05457-114">Instead, it represents abstract features of the view, such as "a list of items".</span></span>

<span data-ttu-id="05457-115">Представление привязано к данным в модели представления.</span><span class="sxs-lookup"><span data-stu-id="05457-115">The view is data-bound to the view-model.</span></span> <span data-ttu-id="05457-116">Обновления модели представления автоматически отражаются в представлении.</span><span class="sxs-lookup"><span data-stu-id="05457-116">Updates to the view-model are automatically reflected in the view.</span></span> <span data-ttu-id="05457-117">Модель представления также получает события из представления, такие как нажатия кнопки, и выполняет операции с моделью, например создание заказа.</span><span class="sxs-lookup"><span data-stu-id="05457-117">The view-model also gets events from the view, such as button clicks, and performs operations on the model, such as creating an order.</span></span>

![](using-web-api-with-entity-framework-part-5/_static/image1.png)

<span data-ttu-id="05457-118">Сначала мы определим модель представления.</span><span class="sxs-lookup"><span data-stu-id="05457-118">First we'll define the view-model.</span></span> <span data-ttu-id="05457-119">После этого мы будем привязывать разметку HTML к модели представления.</span><span class="sxs-lookup"><span data-stu-id="05457-119">After that, we will bind the HTML markup to the view-model.</span></span>

<span data-ttu-id="05457-120">Добавьте следующий раздел Razor в Admin. cshtml:</span><span class="sxs-lookup"><span data-stu-id="05457-120">Add the following Razor section to Admin.cshtml:</span></span>

[!code-cshtml[Main](using-web-api-with-entity-framework-part-5/samples/sample1.cshtml)]

<span data-ttu-id="05457-121">Этот раздел можно добавить в любое место в файле.</span><span class="sxs-lookup"><span data-stu-id="05457-121">You can add this section anywhere in the file.</span></span> <span data-ttu-id="05457-122">Когда представление отображается, раздел появляется в нижней части страницы HTML, прямо перед закрывающим тегом &lt;/боди&gt;.</span><span class="sxs-lookup"><span data-stu-id="05457-122">When the view is rendered, the section appears at the bottom of the HTML page, right before the closing &lt;/body&gt; tag.</span></span>

<span data-ttu-id="05457-123">Весь скрипт для этой страницы будет находиться внутри тега script, указанного комментарием:</span><span class="sxs-lookup"><span data-stu-id="05457-123">All of the script for this page will go inside the script tag indicated by the comment:</span></span>

[!code-html[Main](using-web-api-with-entity-framework-part-5/samples/sample2.html)]

<span data-ttu-id="05457-124">Сначала определите класс представление-модель:</span><span class="sxs-lookup"><span data-stu-id="05457-124">First, define a view-model class:</span></span>

[!code-javascript[Main](using-web-api-with-entity-framework-part-5/samples/sample3.js)]

<span data-ttu-id="05457-125">**KO. обсерваблеаррай** — это особый тип объекта в маскировании, который называется *наблюдаемым*.</span><span class="sxs-lookup"><span data-stu-id="05457-125">**ko.observableArray** is a special kind of object in Knockout, called an *observable*.</span></span> <span data-ttu-id="05457-126">Из [документации по выколачивание. js](http://knockoutjs.com/documentation/observables.html)можно наблюдать за объектом JavaScript, который может уведомлять подписчиков об изменениях.</span><span class="sxs-lookup"><span data-stu-id="05457-126">From the [Knockout.js documentation](http://knockoutjs.com/documentation/observables.html): An observable is a "JavaScript object that can notify subscribers about changes."</span></span> <span data-ttu-id="05457-127">При изменении содержимого наблюдаемого изменения представление автоматически обновляется для соответствия.</span><span class="sxs-lookup"><span data-stu-id="05457-127">When the contents of an observable change, the view is automatically updated to match.</span></span>

<span data-ttu-id="05457-128">Чтобы заполнить массив `products`, выполните запрос AJAX к веб-API.</span><span class="sxs-lookup"><span data-stu-id="05457-128">To populate the `products` array, make an AJAX request to the web API.</span></span> <span data-ttu-id="05457-129">Помните, что мы сохранили базовый URI для API в контейнере представлений (см. [часть 4](using-web-api-with-entity-framework-part-4.md) учебника).</span><span class="sxs-lookup"><span data-stu-id="05457-129">Recall that we stored the base URI for the API in the view bag (see [Part 4](using-web-api-with-entity-framework-part-4.md) of the tutorial).</span></span>

[!code-javascript[Main](using-web-api-with-entity-framework-part-5/samples/sample4.js?highlight=5)]

<span data-ttu-id="05457-130">Затем добавьте функции в модель представления для создания, обновления и удаления продуктов.</span><span class="sxs-lookup"><span data-stu-id="05457-130">Next, add functions to the view-model to create, update, and delete products.</span></span> <span data-ttu-id="05457-131">Эти функции отправляют вызовы AJAX в веб-API и используют результаты для обновления модели представления.</span><span class="sxs-lookup"><span data-stu-id="05457-131">These functions submit AJAX calls to the web API and use the results to update the view-model.</span></span>

[!code-javascript[Main](using-web-api-with-entity-framework-part-5/samples/sample5.js?highlight=7)]

<span data-ttu-id="05457-132">Теперь самая важная часть: когда модель DOM полностью загружена, вызовите функцию **KO. апплибиндингс** и передайте новый экземпляр `ProductsViewModel`:</span><span class="sxs-lookup"><span data-stu-id="05457-132">Now the most important part: When the DOM is fulled loaded, call the **ko.applyBindings** function and pass in a new instance of the `ProductsViewModel`:</span></span>

[!code-javascript[Main](using-web-api-with-entity-framework-part-5/samples/sample6.js)]

<span data-ttu-id="05457-133">Метод **KO. апплибиндингс** активирует маскирование и подсоединяет модель представления к представлению.</span><span class="sxs-lookup"><span data-stu-id="05457-133">The **ko.applyBindings** method activates Knockout and wires up the view-model to the view.</span></span>

<span data-ttu-id="05457-134">Теперь, когда у нас есть модель представления, можно создать привязки.</span><span class="sxs-lookup"><span data-stu-id="05457-134">Now that we have a view-model, we can create the bindings.</span></span> <span data-ttu-id="05457-135">В выколачивание. js это можно сделать, добавив атрибуты `data-bind` в элементы HTML.</span><span class="sxs-lookup"><span data-stu-id="05457-135">In Knockout.js, you do this by adding `data-bind` attributes to HTML elements.</span></span> <span data-ttu-id="05457-136">Например, чтобы привязать список HTML к массиву, используйте привязку `foreach`:</span><span class="sxs-lookup"><span data-stu-id="05457-136">For example, to bind an HTML list to an array, use the `foreach` binding:</span></span>

[!code-html[Main](using-web-api-with-entity-framework-part-5/samples/sample7.html?highlight=1)]

<span data-ttu-id="05457-137">Привязка `foreach` выполняет итерацию по массиву и создает дочерние элементы для каждого объекта в массиве.</span><span class="sxs-lookup"><span data-stu-id="05457-137">The `foreach` binding iterates through the array and creates child elements for each object in the array.</span></span> <span data-ttu-id="05457-138">Привязки к дочерним элементам могут ссылаться на свойства объектов Array.</span><span class="sxs-lookup"><span data-stu-id="05457-138">Bindings on the child elements can refer to properties on the array objects.</span></span>

<span data-ttu-id="05457-139">Добавьте следующие привязки в список "обновить продукты":</span><span class="sxs-lookup"><span data-stu-id="05457-139">Add the following bindings to the "update-products" list:</span></span>

[!code-html[Main](using-web-api-with-entity-framework-part-5/samples/sample8.html)]

<span data-ttu-id="05457-140">Элемент `<li>` находится в области привязки **foreach** .</span><span class="sxs-lookup"><span data-stu-id="05457-140">The `<li>` element occurs within the scope of the **foreach** binding.</span></span> <span data-ttu-id="05457-141">Это означает, что выколачивание будет визуализировать элемент один раз для каждого продукта в массиве `products`.</span><span class="sxs-lookup"><span data-stu-id="05457-141">That means Knockout will render the element once for each product in the `products` array.</span></span> <span data-ttu-id="05457-142">Все привязки в элементе `<li>` ссылаются на этот экземпляр продукта.</span><span class="sxs-lookup"><span data-stu-id="05457-142">All of the bindings within the `<li>` element refer to that product instance.</span></span> <span data-ttu-id="05457-143">Например, `$data.Name` ссылается на свойство `Name` в продукте.</span><span class="sxs-lookup"><span data-stu-id="05457-143">For example, `$data.Name` refers to the `Name` property on the product.</span></span>

<span data-ttu-id="05457-144">Чтобы задать значения для текстовых входов, используйте привязку `value`.</span><span class="sxs-lookup"><span data-stu-id="05457-144">To set the values of the text inputs, use the `value` binding.</span></span> <span data-ttu-id="05457-145">Кнопки привязаны к функциям в представлении "модель" с помощью привязки `click`.</span><span class="sxs-lookup"><span data-stu-id="05457-145">The buttons are bound to functions on the model-view, using the `click` binding.</span></span> <span data-ttu-id="05457-146">Экземпляр продукта передается в качестве параметра каждой функции.</span><span class="sxs-lookup"><span data-stu-id="05457-146">The product instance is passed as a parameter to each function.</span></span> <span data-ttu-id="05457-147">Дополнительные сведения см. в [документации по выколачивание. js](http://knockoutjs.com/documentation/observables.html) с хорошим описанием различных привязок.</span><span class="sxs-lookup"><span data-stu-id="05457-147">For more information, the [Knockout.js documentation](http://knockoutjs.com/documentation/observables.html) has good descriptions of the various bindings.</span></span>

<span data-ttu-id="05457-148">Затем добавьте привязку для события **Submit** в форму Добавление продукта:</span><span class="sxs-lookup"><span data-stu-id="05457-148">Next, add a binding for the **submit** event on the Add Product form:</span></span>

[!code-html[Main](using-web-api-with-entity-framework-part-5/samples/sample9.html)]

<span data-ttu-id="05457-149">Эта привязка вызывает функцию `create` в модели представления для создания нового продукта.</span><span class="sxs-lookup"><span data-stu-id="05457-149">This binding calls the `create` function on the view-model to create a new product.</span></span>

<span data-ttu-id="05457-150">Ниже приведен полный код представления администрирования.</span><span class="sxs-lookup"><span data-stu-id="05457-150">Here is the complete code for the Admin view:</span></span>

[!code-cshtml[Main](using-web-api-with-entity-framework-part-5/samples/sample10.cshtml)]

<span data-ttu-id="05457-151">Запустите приложение, войдите в систему с помощью учетной записи администратора и щелкните ссылку Admin (администратор).</span><span class="sxs-lookup"><span data-stu-id="05457-151">Run the application, log in with the Administrator account, and click the "Admin" link.</span></span> <span data-ttu-id="05457-152">Вы должны увидеть список продуктов и иметь возможность создавать, обновлять или удалять продукты.</span><span class="sxs-lookup"><span data-stu-id="05457-152">You should see the list of products, and be able to create, update, or delete products.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="05457-153">[Назад](using-web-api-with-entity-framework-part-4.md)
> [Вперед](using-web-api-with-entity-framework-part-6.md)</span><span class="sxs-lookup"><span data-stu-id="05457-153">[Previous](using-web-api-with-entity-framework-part-4.md)
[Next](using-web-api-with-entity-framework-part-6.md)</span></span>
