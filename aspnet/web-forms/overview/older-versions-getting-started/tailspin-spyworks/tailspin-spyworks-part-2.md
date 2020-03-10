---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-2
title: Часть 2. уровень доступа к данным | Документация Майкрософт
author: JoeStagner
description: В этой серии руководств подробно описаны все шаги, предпринятые для создания примера приложения Tailspin Spyworks. В части 2 описывается добавление уровня доступа к данным.
ms.author: riande
ms.date: 07/21/2010
ms.assetid: 5a9d5429-d70b-411c-8474-f42cf7ef8a2b
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-2
msc.type: authoredcontent
ms.openlocfilehash: 342d2c54dfba5d052570e890f85dcf9739f9884f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78462654"
---
# <a name="part-2-data-access-layer"></a><span data-ttu-id="c7796-104">Часть 2. уровень доступа к данным</span><span class="sxs-lookup"><span data-stu-id="c7796-104">Part 2: Data Access Layer</span></span>

<span data-ttu-id="c7796-105">кем [Джо Stagner)](https://github.com/JoeStagner)</span><span class="sxs-lookup"><span data-stu-id="c7796-105">by [Joe Stagner](https://github.com/JoeStagner)</span></span>

> <span data-ttu-id="c7796-106">В Tailspin Spyworks. демонстрируется, как чрезвычайно прост в создании мощных масштабируемых приложений для платформы .NET.</span><span class="sxs-lookup"><span data-stu-id="c7796-106">Tailspin Spyworks demonstrates how extraordinarily simple it is to create powerful, scalable applications for the .NET platform.</span></span> <span data-ttu-id="c7796-107">Здесь показано, как использовать замечательные новые функции в ASP.NET 4 для создания Интернет-магазина, включая покупку, оформление и администрирование.</span><span class="sxs-lookup"><span data-stu-id="c7796-107">It shows off how to use the great new features in ASP.NET 4 to build an online store, including shopping, checkout, and administration.</span></span>
> 
> <span data-ttu-id="c7796-108">В этой серии руководств подробно описаны все шаги, предпринятые для создания примера приложения Tailspin Spyworks.</span><span class="sxs-lookup"><span data-stu-id="c7796-108">This tutorial series details all of the steps taken to build the Tailspin Spyworks sample application.</span></span> <span data-ttu-id="c7796-109">В части 2 описывается добавление уровня доступа к данным.</span><span class="sxs-lookup"><span data-stu-id="c7796-109">Part 2 covers adding the data access layer.</span></span>

## <a id="_Toc260221668"></a><span data-ttu-id="c7796-110">Добавление уровня доступа к данным</span><span class="sxs-lookup"><span data-stu-id="c7796-110">Adding the Data Access Layer</span></span>

<span data-ttu-id="c7796-111">Приложение электронной коммерции будет зависеть от двух баз данных.</span><span class="sxs-lookup"><span data-stu-id="c7796-111">Our ecommerce application will depend on two databases.</span></span>

<span data-ttu-id="c7796-112">Для получения сведений о клиенте мы будем использовать стандартную базу данных членства ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="c7796-112">For customer information we'll use the standard ASP.NET Membership database.</span></span> <span data-ttu-id="c7796-113">Для нашей покупательской корзины и каталога продуктов мы создадим базу данных SQL Express, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="c7796-113">For our shopping cart and product catalog we'll implement a SQL Express database as follows.</span></span>

![](tailspin-spyworks-part-2/_static/image1.jpg)

<span data-ttu-id="c7796-114">Создавайте базу данных (Commerce. mdf) в папке данных приложения\_. мы можем приступить к созданию нашего уровня доступа к данным с помощью Entity Framework .NET.</span><span class="sxs-lookup"><span data-stu-id="c7796-114">Having created the database (Commerce.mdf) in the application's App\_Data folder we can proceed to create our Data Access Layer using the .NET Entity Framework.</span></span>

<span data-ttu-id="c7796-115">Мы создадим папку с именем "доступ к данным\_доступом", и щелкните правой кнопкой мыши эту папку и выберите команду "добавить новый элемент".</span><span class="sxs-lookup"><span data-stu-id="c7796-115">We'll create a folder named "Data\_Access" and them right click on that folder and select "Add New Item".</span></span>

<span data-ttu-id="c7796-116">В элементе "установленные шаблоны" и выберите "ADO.NET EDM" введите EDM\_Commerce. EDMX в качестве имени и нажмите кнопку "Добавить".</span><span class="sxs-lookup"><span data-stu-id="c7796-116">In the "Installed Templates" item and then select "ADO.NET Entity Data Model" enter EDM\_Commerce.edmx as the name and click the "Add" button.</span></span>

![](tailspin-spyworks-part-2/_static/image2.jpg)

<span data-ttu-id="c7796-117">Выберите "создать из базы данных".</span><span class="sxs-lookup"><span data-stu-id="c7796-117">Choose "Generate from Database".</span></span>

![](tailspin-spyworks-part-2/_static/image1.png)

![](tailspin-spyworks-part-2/_static/image2.png)

![](tailspin-spyworks-part-2/_static/image3.png)

![](tailspin-spyworks-part-2/_static/image3.jpg)

<span data-ttu-id="c7796-118">Сохраните и создайте.</span><span class="sxs-lookup"><span data-stu-id="c7796-118">Save and build.</span></span>

<span data-ttu-id="c7796-119">Теперь мы готовы к добавлению нашей первой функции — меню категории продукта.</span><span class="sxs-lookup"><span data-stu-id="c7796-119">Now we are ready to add our first feature – a product category menu.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="c7796-120">[Назад](tailspin-spyworks-part-1.md)
> [Вперед](tailspin-spyworks-part-3.md)</span><span class="sxs-lookup"><span data-stu-id="c7796-120">[Previous](tailspin-spyworks-part-1.md)
[Next](tailspin-spyworks-part-3.md)</span></span>
