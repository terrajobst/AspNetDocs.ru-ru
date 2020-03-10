---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-4
title: Часть 4. список продуктов | Документация Майкрософт
author: JoeStagner
description: В этой серии руководств подробно описаны все шаги, предпринятые для создания примера приложения Tailspin Spyworks. В части 4 описывается список продуктов с помощью элемента управления "отдача"...
ms.author: riande
ms.date: 07/21/2010
ms.assetid: 4fab47d5-a6ec-4fdc-91f0-651a093a24b9
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-4
msc.type: authoredcontent
ms.openlocfilehash: 7af1b8afa2ecc8df9846f2edd2091b26b93a811c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78457284"
---
# <a name="part-4-listing-products"></a><span data-ttu-id="9a9e9-104">Часть 4. список продуктов</span><span class="sxs-lookup"><span data-stu-id="9a9e9-104">Part 4: Listing Products</span></span>

<span data-ttu-id="9a9e9-105">кем [Джо Stagner)](https://github.com/JoeStagner)</span><span class="sxs-lookup"><span data-stu-id="9a9e9-105">by [Joe Stagner](https://github.com/JoeStagner)</span></span>

> <span data-ttu-id="9a9e9-106">В Tailspin Spyworks. демонстрируется, как чрезвычайно прост в создании мощных масштабируемых приложений для платформы .NET.</span><span class="sxs-lookup"><span data-stu-id="9a9e9-106">Tailspin Spyworks demonstrates how extraordinarily simple it is to create powerful, scalable applications for the .NET platform.</span></span> <span data-ttu-id="9a9e9-107">Здесь показано, как использовать замечательные новые функции в ASP.NET 4 для создания Интернет-магазина, включая покупку, оформление и администрирование.</span><span class="sxs-lookup"><span data-stu-id="9a9e9-107">It shows off how to use the great new features in ASP.NET 4 to build an online store, including shopping, checkout, and administration.</span></span>
> 
> <span data-ttu-id="9a9e9-108">В этой серии руководств подробно описаны все шаги, предпринятые для создания примера приложения Tailspin Spyworks.</span><span class="sxs-lookup"><span data-stu-id="9a9e9-108">This tutorial series details all of the steps taken to build the Tailspin Spyworks sample application.</span></span> <span data-ttu-id="9a9e9-109">В части 4 описывается список продуктов с помощью элемента управления GridView.</span><span class="sxs-lookup"><span data-stu-id="9a9e9-109">Part 4 covers listing products with the GridView control.</span></span>

## <a id="_Toc260221670"></a><span data-ttu-id="9a9e9-110">Список продуктов с помощью элемента управления GridView</span><span class="sxs-lookup"><span data-stu-id="9a9e9-110">Listing Products with the GridView Control</span></span>

<span data-ttu-id="9a9e9-111">Давайте начнем реализацию страницы Продуктслист. aspx, щелкнув правой кнопкой мыши в нашем решении и выбрав "Добавить" и "новый элемент".</span><span class="sxs-lookup"><span data-stu-id="9a9e9-111">Let's begin implementing our ProductsList.aspx page by "Right Clicking" on our solution and selecting "Add" and "New Item".</span></span>

![](tailspin-spyworks-part-4/_static/image1.jpg)

<span data-ttu-id="9a9e9-112">Выберите "веб-форма с использованием главной страницы" и введите имя страницы Продуктслист. aspx.</span><span class="sxs-lookup"><span data-stu-id="9a9e9-112">Choose "Web Form Using Master Page" and enter a page name of ProductsList.aspx".</span></span>

<span data-ttu-id="9a9e9-113">Нажмите кнопку "Добавить".</span><span class="sxs-lookup"><span data-stu-id="9a9e9-113">Click "Add".</span></span>

![](tailspin-spyworks-part-4/_static/image2.jpg)

<span data-ttu-id="9a9e9-114">Затем выберите папку Styles (стили), в которую помещена страница Site. master, и выберите ее в окне "содержимое папки".</span><span class="sxs-lookup"><span data-stu-id="9a9e9-114">Next choose the "Styles" folder where we placed the Site.Master page and select it from the "Contents of folder" window.</span></span>

![](tailspin-spyworks-part-4/_static/image3.jpg)

<span data-ttu-id="9a9e9-115">Нажмите кнопку "ОК", чтобы создать страницу.</span><span class="sxs-lookup"><span data-stu-id="9a9e9-115">Click "Ok" to create the page.</span></span>

<span data-ttu-id="9a9e9-116">База данных заполняется данными о продуктах, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="9a9e9-116">Our database is populated with product data as seen below.</span></span>

![](tailspin-spyworks-part-4/_static/image4.jpg)

<span data-ttu-id="9a9e9-117">После создания страницы мы снова будем использовать источник данных сущности для доступа к данным этого продукта, но в этом экземпляре нужно выбрать сущности «продукт», чтобы ограничить возвращаемые элементы только теми, которые относятся к выбранной категории.</span><span class="sxs-lookup"><span data-stu-id="9a9e9-117">After our page is created we'll again use an Entity Data Source to access that product data, but in this instance we need to select the Product Entities and we need to restrict the items that are returned to only those for the selected Category.</span></span>

<span data-ttu-id="9a9e9-118">Для этого мы будем сообщать EntityDataSource автоматически создавать предложение WHERE, и мы будем указывать Вхерепараметер.</span><span class="sxs-lookup"><span data-stu-id="9a9e9-118">To accomplish this we'll tell the EntityDataSource to Auto Generate the WHERE clause and we'll specify the WhereParameter.</span></span>

<span data-ttu-id="9a9e9-119">Вы помните, что при создании пунктов меню в меню "Категория продукта" Мы динамически создали ссылку, добавив CategoryID в строку запроса для каждой ссылки.</span><span class="sxs-lookup"><span data-stu-id="9a9e9-119">You'll recall that when we created the Menu Items in our "Product Category Menu" we dynamically built the link by adding the CategoryID to the QueryString for each link.</span></span> <span data-ttu-id="9a9e9-120">Мы будем сообщать источнику данных сущности о необходимости получения параметра WHERE из этого параметра QueryString.</span><span class="sxs-lookup"><span data-stu-id="9a9e9-120">We will tell the Entity Data Source to derive the WHERE parameter from that QueryString parameter.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-4/samples/sample1.aspx)]

<span data-ttu-id="9a9e9-121">Далее мы настроим элемент управления ListView для вывода списка продуктов.</span><span class="sxs-lookup"><span data-stu-id="9a9e9-121">Next, we'll configure the ListView control to display a list of products.</span></span> <span data-ttu-id="9a9e9-122">Чтобы создать оптимальные возможности для покупок, мы будем сжимать несколько кратких функций в каждом отдельном продукте, который отображается в нашей Листвев.</span><span class="sxs-lookup"><span data-stu-id="9a9e9-122">To create an optimal shopping experience we'll compact several concise features into each individual product displayed in our ListVew.</span></span>

- <span data-ttu-id="9a9e9-123">Название продукта будет ссылкой на подробное представление продукта.</span><span class="sxs-lookup"><span data-stu-id="9a9e9-123">The product name will be a link to the product's detail view.</span></span>
- <span data-ttu-id="9a9e9-124">Отобразится цена продукта.</span><span class="sxs-lookup"><span data-stu-id="9a9e9-124">The product's price will be displayed.</span></span>
- <span data-ttu-id="9a9e9-125">Будет отображен образ продукта, и мы динамически выбираем образ из каталога образов каталога в нашем приложении.</span><span class="sxs-lookup"><span data-stu-id="9a9e9-125">An image of the product will be displayed and we'll dynamically select the image from a catalog images directory in our application.</span></span>
- <span data-ttu-id="9a9e9-126">Мы будем включать ссылку для незамедлительного добавления конкретного продукта в корзину для покупок.</span><span class="sxs-lookup"><span data-stu-id="9a9e9-126">We will include a link to immediately add the specific product to the shopping cart.</span></span>

<span data-ttu-id="9a9e9-127">Ниже приведена разметка для нашего экземпляра элемента управления ListView.</span><span class="sxs-lookup"><span data-stu-id="9a9e9-127">Here is the markup for our ListView control instance.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-4/samples/sample2.aspx)]

<span data-ttu-id="9a9e9-128">Мы динамически создаем несколько ссылок для каждого отображаемого продукта.</span><span class="sxs-lookup"><span data-stu-id="9a9e9-128">We are dynamically building several links for each displayed product.</span></span>

<span data-ttu-id="9a9e9-129">Кроме того, перед тестированием новой страницы необходимо создать структуру каталогов для образов каталога продуктов следующим образом.</span><span class="sxs-lookup"><span data-stu-id="9a9e9-129">Also, before we test own new page we need to create the directory structure for the product catalog images as follows.</span></span>

![](tailspin-spyworks-part-4/_static/image1.png)

<span data-ttu-id="9a9e9-130">После получения доступа к нашим образам продукта можно протестировать страницу списка продуктов.</span><span class="sxs-lookup"><span data-stu-id="9a9e9-130">Once our product images are accessible we can test our product list page.</span></span>

![](tailspin-spyworks-part-4/_static/image5.jpg)

<span data-ttu-id="9a9e9-131">На домашней странице сайта щелкните одну из ссылок списка категорий.</span><span class="sxs-lookup"><span data-stu-id="9a9e9-131">From the site's home page, click on one of the Category List Links.</span></span>

![](tailspin-spyworks-part-4/_static/image6.jpg)

<span data-ttu-id="9a9e9-132">Теперь необходимо реализовать страницу Продуктдетаилс. aspx и функцию Аддтокарт.</span><span class="sxs-lookup"><span data-stu-id="9a9e9-132">Now we need to implement the ProductDetails.aspx page and the AddToCart functionality.</span></span>

<span data-ttu-id="9a9e9-133">Используйте файл-&gt;New, чтобы создать имя страницы Продуктдетаилс. aspx с помощью главной страницы сайта, как это было сделано ранее.</span><span class="sxs-lookup"><span data-stu-id="9a9e9-133">Use File-&gt;New to create a page name ProductDetails.aspx using the site Master Page as we did previously.</span></span>

<span data-ttu-id="9a9e9-134">Мы снова будем использовать элемент управления EntityDataSource для доступа к конкретной записи продукта в базе данных, и мы будем использовать элемент управления FormView ASP.NET для вывода данных о продукте следующим образом.</span><span class="sxs-lookup"><span data-stu-id="9a9e9-134">We will again use an EntityDataSource control to access the specific product record in the database and we will use an ASP.NET FormView control to display the product data as follows.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-4/samples/sample3.aspx)]

<span data-ttu-id="9a9e9-135">Не беспокойтесь, если форматирование выглядит немного весело.</span><span class="sxs-lookup"><span data-stu-id="9a9e9-135">Don't worry if the formatting looks a bit funny to you.</span></span> <span data-ttu-id="9a9e9-136">Приведенная выше разметка оставляет место в макете для нескольких функций, которые мы будем реализовывать позже.</span><span class="sxs-lookup"><span data-stu-id="9a9e9-136">The markup above leaves room in the display layout for a couple of features we'll implement later on.</span></span>

<span data-ttu-id="9a9e9-137">Корзина для покупок будет представлять более сложную логику в нашем приложении.</span><span class="sxs-lookup"><span data-stu-id="9a9e9-137">The Shopping Cart will represent the more complex logic in our application.</span></span> <span data-ttu-id="9a9e9-138">Чтобы приступить к работе, используйте файл-&gt;New, чтобы создать страницу с именем Мишоппингкарт. aspx.</span><span class="sxs-lookup"><span data-stu-id="9a9e9-138">To get started, use File-&gt;New to create a page called MyShoppingCart.aspx.</span></span>

<span data-ttu-id="9a9e9-139">Обратите внимание, что мы не выбираем имя ShoppingCart. aspx.</span><span class="sxs-lookup"><span data-stu-id="9a9e9-139">Note that we are not choosing the name ShoppingCart.aspx.</span></span>

<span data-ttu-id="9a9e9-140">Наша база данных содержит таблицу с именем «ShoppingCart».</span><span class="sxs-lookup"><span data-stu-id="9a9e9-140">Our database contains a table named "ShoppingCart".</span></span> <span data-ttu-id="9a9e9-141">Когда мы создали EDM класс был создан для каждой таблицы в базе данных.</span><span class="sxs-lookup"><span data-stu-id="9a9e9-141">When we generated an Entity Data Model a class was created for each table in the database.</span></span> <span data-ttu-id="9a9e9-142">Таким образом, EDM создал класс сущностей с именем «ShoppingCart».</span><span class="sxs-lookup"><span data-stu-id="9a9e9-142">Therefore, the Entity Data Model generated an Entity Class named "ShoppingCart".</span></span> <span data-ttu-id="9a9e9-143">Мы можем изменить модель, чтобы мы могли использовать это имя для реализации нашей корзины покупок или расширить его для наших нужд, но вместо этого мы будем выбирать имя, которое позволит избежать конфликта.</span><span class="sxs-lookup"><span data-stu-id="9a9e9-143">We could edit the model so that we could use that name for our shopping cart implementation or extend it for our needs, but we will opt instead to simply select a name that will avoid the conflict.</span></span>

<span data-ttu-id="9a9e9-144">Также стоит отметить, что мы будем создавать простую корзину для покупок и внедрять логику покупательской корзины с отображением корзины.</span><span class="sxs-lookup"><span data-stu-id="9a9e9-144">It's also worth noting that we will be creating a simple shopping cart and embedding the shopping cart logic with the shopping cart display.</span></span> <span data-ttu-id="9a9e9-145">Мы также можем реализовать нашу корзину для покупок на совершенно отдельном бизнес-уровне.</span><span class="sxs-lookup"><span data-stu-id="9a9e9-145">We might also choose to implement our shopping cart in a completely separate Business Layer.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="9a9e9-146">[Назад](tailspin-spyworks-part-3.md)
> [Вперед](tailspin-spyworks-part-5.md)</span><span class="sxs-lookup"><span data-stu-id="9a9e9-146">[Previous](tailspin-spyworks-part-3.md)
[Next](tailspin-spyworks-part-5.md)</span></span>
