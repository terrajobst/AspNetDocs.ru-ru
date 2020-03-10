---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-3
title: Часть 3. меню «Макет» и «Категория» | Документация Майкрософт
author: JoeStagner
description: В этой серии руководств подробно описаны все шаги, предпринятые для создания примера приложения Tailspin Spyworks. В части 3 описывается добавление макета и меню категорий.
ms.author: riande
ms.date: 07/21/2010
ms.assetid: 94ea1a70-a9bc-4241-8f36-08366d64bab9
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-3
msc.type: authoredcontent
ms.openlocfilehash: a223b97fd362ecf73ecde431e141021c1dcc6a6d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78519102"
---
# <a name="part-3-layout-and-category-menu"></a><span data-ttu-id="8e85e-104">Часть 3. меню «Макет» и «Категория»</span><span class="sxs-lookup"><span data-stu-id="8e85e-104">Part 3: Layout and Category Menu</span></span>

<span data-ttu-id="8e85e-105">кем [Джо Stagner)](https://github.com/JoeStagner)</span><span class="sxs-lookup"><span data-stu-id="8e85e-105">by [Joe Stagner](https://github.com/JoeStagner)</span></span>

> <span data-ttu-id="8e85e-106">В Tailspin Spyworks. демонстрируется, как чрезвычайно прост в создании мощных масштабируемых приложений для платформы .NET.</span><span class="sxs-lookup"><span data-stu-id="8e85e-106">Tailspin Spyworks demonstrates how extraordinarily simple it is to create powerful, scalable applications for the .NET platform.</span></span> <span data-ttu-id="8e85e-107">Здесь показано, как использовать замечательные новые функции в ASP.NET 4 для создания Интернет-магазина, включая покупку, оформление и администрирование.</span><span class="sxs-lookup"><span data-stu-id="8e85e-107">It shows off how to use the great new features in ASP.NET 4 to build an online store, including shopping, checkout, and administration.</span></span>
> 
> <span data-ttu-id="8e85e-108">В этой серии руководств подробно описаны все шаги, предпринятые для создания примера приложения Tailspin Spyworks.</span><span class="sxs-lookup"><span data-stu-id="8e85e-108">This tutorial series details all of the steps taken to build the Tailspin Spyworks sample application.</span></span> <span data-ttu-id="8e85e-109">В части 3 описывается добавление макета и меню категорий.</span><span class="sxs-lookup"><span data-stu-id="8e85e-109">Part 3 covers adding layout and a category menu.</span></span>

## <a id="_Toc260221669"></a><span data-ttu-id="8e85e-110">Добавление макета и меню категорий</span><span class="sxs-lookup"><span data-stu-id="8e85e-110">Adding Some Layout and a Category Menu</span></span>

<span data-ttu-id="8e85e-111">На главной странице сайта мы добавим div для столбца с левой стороны, который будет содержать меню нашей категории продуктов.</span><span class="sxs-lookup"><span data-stu-id="8e85e-111">In our site master page we'll add a div for the left side column that will contain our product category menu.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-3/samples/sample1.aspx)]

<span data-ttu-id="8e85e-112">Обратите внимание, что для класса CSS, который мы добавили в файл style. CSS, будет предоставлено нужное соответствие и другое форматирование.</span><span class="sxs-lookup"><span data-stu-id="8e85e-112">Note that the desired aligning and other formatting will be provided by the CSS class that we added to our Style.css file.</span></span>

[!code-css[Main](tailspin-spyworks-part-3/samples/sample2.css)]

<span data-ttu-id="8e85e-113">Меню категории продуктов будет динамически создано во время выполнения путем запроса к базе данных Commerce для существующих категорий продуктов и создания пунктов меню и соответствующих ссылок.</span><span class="sxs-lookup"><span data-stu-id="8e85e-113">The product category menu will be dynamically created at runtime by querying the Commerce database for existing product categories and creating the menu items and corresponding links.</span></span>

<span data-ttu-id="8e85e-114">Для этого мы будем использовать два ASP. Мощные элементы управления данными .NET.</span><span class="sxs-lookup"><span data-stu-id="8e85e-114">To accomplish this we will use two of ASP.NET's powerful data controls.</span></span> <span data-ttu-id="8e85e-115">Элемент управления "источник данных сущности" и элемент управления "ListView".</span><span class="sxs-lookup"><span data-stu-id="8e85e-115">The "Entity Data Source" control and the "ListView" control.</span></span>

![](tailspin-spyworks-part-3/_static/image1.jpg)

<span data-ttu-id="8e85e-116">Давайте перейдем к «представлению конструктора» и используем для настройки элементов управления вспомогательными командами.</span><span class="sxs-lookup"><span data-stu-id="8e85e-116">Let's switch to "Design View" and use the helpers to configure our controls.</span></span>

![](tailspin-spyworks-part-3/_static/image2.jpg)

<span data-ttu-id="8e85e-117">Давайте присвойте свойству идентификатора EntityDataSource значение EDS\_категории\_меню и щелкните "настроить источник данных".</span><span class="sxs-lookup"><span data-stu-id="8e85e-117">Let's set the EntityDataSource ID property to EDS\_Category\_Menu and click on "Configure Data Source".</span></span>

![](tailspin-spyworks-part-3/_static/image3.jpg)

<span data-ttu-id="8e85e-118">Выберите подключение Коммерцеентитиес, которое было создано для нас при создании модели источников данных сущностей для нашей базы данных Commerce, и нажмите кнопку "Далее".</span><span class="sxs-lookup"><span data-stu-id="8e85e-118">Select the CommerceEntities Connection that was created for us when we created the Entity Data Source Model for our Commerce Database and click "Next".</span></span>

![](tailspin-spyworks-part-3/_static/image4.jpg)

<span data-ttu-id="8e85e-119">Выберите имя набора сущностей "категории" и оставьте остальные параметры по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="8e85e-119">Select the "Categories" Entity set name and leave the rest of the options as default.</span></span> <span data-ttu-id="8e85e-120">Нажмите кнопку "Готово".</span><span class="sxs-lookup"><span data-stu-id="8e85e-120">Click "Finish".</span></span>

<span data-ttu-id="8e85e-121">Теперь давайте зададим свойство ID экземпляра элемента управления ListView, который мы поместили на странице в ListView\_Продуктсмену и активируйте его вспомогательную функцию.</span><span class="sxs-lookup"><span data-stu-id="8e85e-121">Now let's set the ID property of the ListView control instance that we placed on our page to ListView\_ProductsMenu and activate its helper.</span></span>

![](tailspin-spyworks-part-3/_static/image5.jpg)

<span data-ttu-id="8e85e-122">Несмотря на то, что можно использовать параметры управления для форматирования отображения и форматирования элементов данных, для создания нашего меню потребуется только простая разметка, поэтому мы будем вводить код в представлении исходного кода.</span><span class="sxs-lookup"><span data-stu-id="8e85e-122">Though we could use control options to format the data item display and formatting, our menu creation will only require simple markup so we will enter the code in the source view.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-3/samples/sample3.aspx)]

<span data-ttu-id="8e85e-123">Обратите внимание на инструкцию eval: &lt;% # eval ("CategoryName")%&gt;</span><span class="sxs-lookup"><span data-stu-id="8e85e-123">Please note the "Eval" statement : &lt;%# Eval("CategoryName") %&gt;</span></span>

<span data-ttu-id="8e85e-124">Синтаксис ASP.NET &lt;% #%&gt; является сокращенным соглашением, которое указывает среде выполнения выполнить все, что содержится в, и выводит результаты "в строке".</span><span class="sxs-lookup"><span data-stu-id="8e85e-124">The ASP.NET syntax &lt;%# %&gt; is a shorthand convention that instructs the runtime to execute whatever is contained within and output the results "in Line".</span></span>

<span data-ttu-id="8e85e-125">Инструкция eval ("CategoryName") указывает, что для текущей записи в привязанной коллекции элементов данных необходимо получить значение имен элементов модели сущности "CategoryName".</span><span class="sxs-lookup"><span data-stu-id="8e85e-125">The statement Eval("CategoryName") instructs that, for the current entry in the bound collection of data items, fetch the value of the Entity Model item names "CategoryName".</span></span> <span data-ttu-id="8e85e-126">Это краткий синтаксис для очень мощной функции.</span><span class="sxs-lookup"><span data-stu-id="8e85e-126">This is concise syntax for a very powerful feature.</span></span>

<span data-ttu-id="8e85e-127">Теперь можно запустить приложение.</span><span class="sxs-lookup"><span data-stu-id="8e85e-127">Lets run the application now.</span></span>

![](tailspin-spyworks-part-3/_static/image6.jpg)

<span data-ttu-id="8e85e-128">Обратите внимание, что теперь меню «Категория продукта» отображается, а при наведении указателя мыши на один из пунктов меню «Категория» ссылка на пункт меню будет указывать на страницу, которой мы еще не реализовали с именем Продуктслист. aspx и что мы создали динамический аргумент строки запроса, содержащий  Идентификатор категории.</span><span class="sxs-lookup"><span data-stu-id="8e85e-128">Note that our product category menu is now displayed and when we hover over one of the category menu items we can see the menu item link points to a page we have yet to implement named ProductsList.aspx and that we have built a dynamic query string argument that contains the category id.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="8e85e-129">[Назад](tailspin-spyworks-part-2.md)
> [Вперед](tailspin-spyworks-part-4.md)</span><span class="sxs-lookup"><span data-stu-id="8e85e-129">[Previous](tailspin-spyworks-part-2.md)
[Next](tailspin-spyworks-part-4.md)</span></span>
