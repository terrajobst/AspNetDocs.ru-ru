---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/introduction-and-overview
title: Начало работы с веб-формами ASP.NET 4,7 и Visual Studio 2017 | Документация Майкрософт
author: Erikre
description: Эта серия пошаговых руководств поможет вам ознакомиться с основами создания приложения ASP.NET Web Forms с помощью ASP.NET 4,7 и Microsoft Visual Studio
ms.author: riande
ms.date: 01/09/2019
ms.assetid: 9b96eaa1-8ef0-4338-a2e8-e0f970bfaf68
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/introduction-and-overview
msc.type: authoredcontent
ms.openlocfilehash: 52d5eb7abe4520ebdf6667d299d055fc7619a635
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/28/2019
ms.locfileid: "74615453"
---
# <a name="getting-started-with-aspnet-45-web-forms-and-visual-studio-2017"></a><span data-ttu-id="99e71-103">Начало работы с веб-формами ASP.NET 4,5 и Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="99e71-103">Getting Started with ASP.NET 4.5 Web Forms and Visual Studio 2017</span></span>

<span data-ttu-id="99e71-104">[Скачайте образец проекта Wingtip Toys (C#)](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) или [Загрузите электронную книгу (PDF)](https://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)</span><span class="sxs-lookup"><span data-stu-id="99e71-104">[Download Wingtip Toys Sample Project (C#)](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) or [Download E-book (PDF)](https://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)</span></span>

<span data-ttu-id="99e71-105">В этой серии руководств показано, как создать приложение веб-форм ASP.NET с ASP.NET 4,5 и Microsoft Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="99e71-105">This tutorial series shows you how to build an ASP.NET Web Forms application with ASP.NET 4.5 and Microsoft Visual Studio 2017.</span></span> 

## <a name="introduction"></a><span data-ttu-id="99e71-106">Введение</span><span class="sxs-lookup"><span data-stu-id="99e71-106">Introduction</span></span>

<span data-ttu-id="99e71-107">В этой серии руководств описывается создание приложения ASP.NET Web Forms с помощью Visual Studio 2017 и ASP.NET 4,5.</span><span class="sxs-lookup"><span data-stu-id="99e71-107">This tutorial series guides you through creating an ASP.NET Web Forms application using Visual Studio 2017 and ASP.NET 4.5.</span></span> <span data-ttu-id="99e71-108">Вы создадите приложение с названием **Wingtip Toys** — упрощенный веб-сайт витрина, который продает товары по сети.</span><span class="sxs-lookup"><span data-stu-id="99e71-108">You'll create an application named **Wingtip Toys** - a simplified storefront web site selling items online.</span></span> <span data-ttu-id="99e71-109">Во время ряда выделяются новые компоненты ASP.NET 4,5.</span><span class="sxs-lookup"><span data-stu-id="99e71-109">During the series, new ASP.NET 4.5 features are highlighted.</span></span>

### <a name="target-audience"></a><span data-ttu-id="99e71-110">Целевая аудитория</span><span class="sxs-lookup"><span data-stu-id="99e71-110">Target audience</span></span>

<span data-ttu-id="99e71-111">Разработчики, впервые представленные в ASP.NET Web Forms, являются целевой аудиторией этой серии руководств.</span><span class="sxs-lookup"><span data-stu-id="99e71-111">Developers new to ASP.NET Web Forms are the target audience for this tutorial series.</span></span>

<span data-ttu-id="99e71-112">У вас должны быть знания в следующих областях:</span><span class="sxs-lookup"><span data-stu-id="99e71-112">You should have some knowledge in the following areas:</span></span>

- <span data-ttu-id="99e71-113">Объектно-ориентированное программирование (ООП) и языки</span><span class="sxs-lookup"><span data-stu-id="99e71-113">Object-oriented programming (OOP) and languages</span></span>
- <span data-ttu-id="99e71-114">Веб-разработка (HTML, CSS, JavaScript)</span><span class="sxs-lookup"><span data-stu-id="99e71-114">Web development (HTML, CSS, JavaScript)</span></span>
- <span data-ttu-id="99e71-115">Реляционные базы данных</span><span class="sxs-lookup"><span data-stu-id="99e71-115">Relational databases</span></span>
- <span data-ttu-id="99e71-116">N-уровневая архитектура</span><span class="sxs-lookup"><span data-stu-id="99e71-116">N-tier architecture</span></span>

<span data-ttu-id="99e71-117">Для просмотра этих областей рассмотрите следующее содержимое:</span><span class="sxs-lookup"><span data-stu-id="99e71-117">To review these areas, consider studying the following content:</span></span>

- [<span data-ttu-id="99e71-118">Начало работы с Visual C#</span><span class="sxs-lookup"><span data-stu-id="99e71-118">Getting Started with Visual C#</span></span>](https://msdn.microsoft.com/library/a72418yk.aspx)
- <span data-ttu-id="99e71-119">[Веб-разработка](https://msdn.microsoft.com/beginner/bb308760.aspx), [HTML, CSS, JavaScript, SQL, PHP, jQuery](http://w3schools.com/)</span><span class="sxs-lookup"><span data-stu-id="99e71-119">[Web Development](https://msdn.microsoft.com/beginner/bb308760.aspx), [HTML, CSS, JavaScript, SQL, PHP, JQuery](http://w3schools.com/)</span></span>
- [<span data-ttu-id="99e71-120">Реляционная база данных</span><span class="sxs-lookup"><span data-stu-id="99e71-120">Relational database</span></span>](http://en.wikipedia.org/wiki/Relational_database)
- [<span data-ttu-id="99e71-121">Многоуровневая архитектура</span><span class="sxs-lookup"><span data-stu-id="99e71-121">Multitier architecture</span></span>](http://en.wikipedia.org/wiki/Multitier_architecture)

### <a name="application-features"></a><span data-ttu-id="99e71-122">Функции приложения</span><span class="sxs-lookup"><span data-stu-id="99e71-122">Application features</span></span>

<span data-ttu-id="99e71-123">Функции веб-форм ASP.NET, представленные в этой серии, включают:</span><span class="sxs-lookup"><span data-stu-id="99e71-123">The ASP.NET Web Form features presented in this series include:</span></span>

- <span data-ttu-id="99e71-124">Проект веб-приложения (не проект веб-сайта)</span><span class="sxs-lookup"><span data-stu-id="99e71-124">The Web Application Project (not Web Site Project)</span></span>
- <span data-ttu-id="99e71-125">веб-формы</span><span class="sxs-lookup"><span data-stu-id="99e71-125">Web Forms</span></span>
- <span data-ttu-id="99e71-126">Главные страницы, Настройка</span><span class="sxs-lookup"><span data-stu-id="99e71-126">Master Pages, Configuration</span></span>
- <span data-ttu-id="99e71-127">Загрузке</span><span class="sxs-lookup"><span data-stu-id="99e71-127">Bootstrap</span></span>
- <span data-ttu-id="99e71-128">Code First Entity Framework, LocalDB</span><span class="sxs-lookup"><span data-stu-id="99e71-128">Entity Framework Code First, LocalDB</span></span>
- <span data-ttu-id="99e71-129">Проверка запроса</span><span class="sxs-lookup"><span data-stu-id="99e71-129">Request Validation</span></span>
- <span data-ttu-id="99e71-130">Строго типизированные элементы управления данными</span><span class="sxs-lookup"><span data-stu-id="99e71-130">Strongly-typed Data Controls</span></span>
- <span data-ttu-id="99e71-131">Привязка модели</span><span class="sxs-lookup"><span data-stu-id="99e71-131">Model Binding</span></span>
- <span data-ttu-id="99e71-132">Заметки к данным</span><span class="sxs-lookup"><span data-stu-id="99e71-132">Data Annotations</span></span>
- <span data-ttu-id="99e71-133">Поставщики значений</span><span class="sxs-lookup"><span data-stu-id="99e71-133">Value Providers</span></span>
- <span data-ttu-id="99e71-134">SSL и OAuth</span><span class="sxs-lookup"><span data-stu-id="99e71-134">SSL and OAuth</span></span>
- <span data-ttu-id="99e71-135">ASP.NET Identity, конфигурация и авторизация</span><span class="sxs-lookup"><span data-stu-id="99e71-135">ASP.NET Identity, Configuration, and Authorization</span></span>
- <span data-ttu-id="99e71-136">Ненавязчивая проверка</span><span class="sxs-lookup"><span data-stu-id="99e71-136">Unobtrusive Validation</span></span>
- <span data-ttu-id="99e71-137">Маршрутизация</span><span class="sxs-lookup"><span data-stu-id="99e71-137">Routing</span></span>
- <span data-ttu-id="99e71-138">Обработка ошибок ASP.NET</span><span class="sxs-lookup"><span data-stu-id="99e71-138">ASP.NET Error Handling</span></span>

### <a name="application-scenarios-and-tasks"></a><span data-ttu-id="99e71-139">Сценарии и задачи приложений</span><span class="sxs-lookup"><span data-stu-id="99e71-139">Application scenarios and tasks</span></span>

<span data-ttu-id="99e71-140">Задачи серии руководств включают:</span><span class="sxs-lookup"><span data-stu-id="99e71-140">Tutorial series tasks include:</span></span>

- <span data-ttu-id="99e71-141">Создание, просмотр и запуск нового проекта</span><span class="sxs-lookup"><span data-stu-id="99e71-141">Creating, reviewing, and running a new project</span></span>
- <span data-ttu-id="99e71-142">Создание структуры базы данных</span><span class="sxs-lookup"><span data-stu-id="99e71-142">Creating a database structure</span></span>
- <span data-ttu-id="99e71-143">Инициализация и заполнение базы данных</span><span class="sxs-lookup"><span data-stu-id="99e71-143">Initializing and seeding a database</span></span>
- <span data-ttu-id="99e71-144">Настройка пользовательского интерфейса со стилями, графикой и главной страницей</span><span class="sxs-lookup"><span data-stu-id="99e71-144">Customizing the UI with styles, graphics, and a master page</span></span>
- <span data-ttu-id="99e71-145">Добавление страниц и переходов</span><span class="sxs-lookup"><span data-stu-id="99e71-145">Adding pages and navigation</span></span>
- <span data-ttu-id="99e71-146">Отображение сведений о меню и данных о продуктах</span><span class="sxs-lookup"><span data-stu-id="99e71-146">Displaying menu details and product data</span></span>
- <span data-ttu-id="99e71-147">Создание корзины для покупок</span><span class="sxs-lookup"><span data-stu-id="99e71-147">Creating a shopping cart</span></span>
- <span data-ttu-id="99e71-148">Добавление поддержки SSL и OAuth</span><span class="sxs-lookup"><span data-stu-id="99e71-148">Adding SSL and OAuth support</span></span>
- <span data-ttu-id="99e71-149">Добавление метода оплаты</span><span class="sxs-lookup"><span data-stu-id="99e71-149">Adding a payment method</span></span>
- <span data-ttu-id="99e71-150">Включение роли администратора и пользователя в приложение</span><span class="sxs-lookup"><span data-stu-id="99e71-150">Including an administrator role and a user to the application</span></span>
- <span data-ttu-id="99e71-151">Ограниченный доступ к определенным страницам и папкам</span><span class="sxs-lookup"><span data-stu-id="99e71-151">Restricting access to specific pages and folder</span></span>
- <span data-ttu-id="99e71-152">Отправка файла в веб-приложение</span><span class="sxs-lookup"><span data-stu-id="99e71-152">Uploading a file to the web application</span></span>
- <span data-ttu-id="99e71-153">Реализация проверки входных данных</span><span class="sxs-lookup"><span data-stu-id="99e71-153">Implementing input validation</span></span>
- <span data-ttu-id="99e71-154">Регистрация маршрутов для веб-приложения</span><span class="sxs-lookup"><span data-stu-id="99e71-154">Registering routes for the web application</span></span>
- <span data-ttu-id="99e71-155">Реализация обработки ошибок и ведения журнала ошибок</span><span class="sxs-lookup"><span data-stu-id="99e71-155">Implementing error handling and error logging</span></span>

## <a name="overview"></a><span data-ttu-id="99e71-156">Обзор</span><span class="sxs-lookup"><span data-stu-id="99e71-156">Overview</span></span>

<span data-ttu-id="99e71-157">Эта серия руководств предназначена для пользователей, знакомых с концепциями программирования, но не в ASP.NET Web Forms.</span><span class="sxs-lookup"><span data-stu-id="99e71-157">This tutorial series is intended for someone familiar with programming concepts, but new to ASP.NET Web Forms.</span></span> <span data-ttu-id="99e71-158">Если вы уже знакомы с веб-формами ASP.NET, эта серия поможет вам узнать о новых функциях ASP.NET 4,5.</span><span class="sxs-lookup"><span data-stu-id="99e71-158">If you're already familiar with ASP.NET Web Forms, this series can still help you learn about new ASP.NET 4.5 features.</span></span> <span data-ttu-id="99e71-159">Для читателей, незнакомых с концепциями программирования и веб-формами ASP.NET, см. Дополнительные учебники по веб-формам, приведенные в разделе [Начало работы](../../../index.md) на веб-сайте ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="99e71-159">For readers unfamiliar with programming concepts and ASP.NET Web Forms, see the additional Web Forms tutorials provided in the [Getting Started](../../../index.md) section on the ASP.NET Web site.</span></span>

<span data-ttu-id="99e71-160">ASP.NET 4,5, предоставляемые в этой серии руководств, включают следующие функции:</span><span class="sxs-lookup"><span data-stu-id="99e71-160">The ASP.NET 4.5 provided in this tutorial series includes the following features:</span></span>

- <span data-ttu-id="99e71-161">Простой пользовательский интерфейс для создания проектов, обеспечивающих [поддержку многих платформ ASP.NET](../../../../visual-studio/overview/2013/creating-web-projects-in-visual-studio.md#add) (веб-форм, MVC и веб-API).</span><span class="sxs-lookup"><span data-stu-id="99e71-161">A simple UI for creating projects that offers [support for many ASP.NET frameworks](../../../../visual-studio/overview/2013/creating-web-projects-in-visual-studio.md#add) (Web Forms, MVC, and Web API).</span></span>
- <span data-ttu-id="99e71-162">[Начальная](../../../../visual-studio/overview/2013/creating-web-projects-in-visual-studio.md#bootstrap)Загрузка, макет, создание и реагирование инфраструктуры разработки.</span><span class="sxs-lookup"><span data-stu-id="99e71-162">[Bootstrap](../../../../visual-studio/overview/2013/creating-web-projects-in-visual-studio.md#bootstrap), a layout, theming, and responsive design framework.</span></span>
- <span data-ttu-id="99e71-163">[ASP.NET Identity](../../../../identity/index.md), Новая система членства ASP.NET, которая работает одинаково во всех платформах ASP.NET и работает с программным обеспечением, ОТЛИЧНЫМ от IIS.</span><span class="sxs-lookup"><span data-stu-id="99e71-163">[ASP.NET Identity](../../../../identity/index.md), a new ASP.NET membership system that works the same in all ASP.NET frameworks and works with web hosting software other than IIS.</span></span>
- [<span data-ttu-id="99e71-164">Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="99e71-164">Entity Framework 6</span></span>](https://msdn.microsoft.com/data/ef.aspx)

  <span data-ttu-id="99e71-165">Обновление Entity Framework позволяющее выполнять следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="99e71-165">An update to the Entity Framework enabling you to:</span></span>
  - <span data-ttu-id="99e71-166">Получение данных и работа с ними в виде строго типизированных объектов</span><span class="sxs-lookup"><span data-stu-id="99e71-166">Retrieve and manipulate data as strongly-typed objects</span></span>
  - <span data-ttu-id="99e71-167">Асинхронный доступ к данным</span><span class="sxs-lookup"><span data-stu-id="99e71-167">Access data asynchronously</span></span>
  - <span data-ttu-id="99e71-168">Обработку временных ошибок подключения</span><span class="sxs-lookup"><span data-stu-id="99e71-168">Handle transient connection faults</span></span>
  - <span data-ttu-id="99e71-169">Журналы инструкций SQL</span><span class="sxs-lookup"><span data-stu-id="99e71-169">Log SQL statements</span></span>

<span data-ttu-id="99e71-170">Полный список возможностей ASP.NET 4,5 см. в разделе [ASP.NET and Web Tools для Visual Studio 2013 заметок о выпуске](../../../../visual-studio/overview/2013/release-notes.md).</span><span class="sxs-lookup"><span data-stu-id="99e71-170">For a complete ASP.NET 4.5 feature list, see [ASP.NET and Web Tools for Visual Studio 2013 Release Notes](../../../../visual-studio/overview/2013/release-notes.md).</span></span>

### <a name="the-wingtip-toys-sample-application"></a><span data-ttu-id="99e71-171">Пример приложения Wingtip Toys</span><span class="sxs-lookup"><span data-stu-id="99e71-171">The Wingtip Toys sample application</span></span>

<span data-ttu-id="99e71-172">Следующие снимки экрана находятся в приложении веб-форм ASP.NET, которое создается в этой серии руководств.</span><span class="sxs-lookup"><span data-stu-id="99e71-172">The following screenshots are from the ASP.NET Web Forms application that you create in this tutorial series.</span></span> <span data-ttu-id="99e71-173">При запуске приложения в Visual Studio появляется следующая Домашняя страница.</span><span class="sxs-lookup"><span data-stu-id="99e71-173">When you run the application in Visual Studio, the following web Home page appears.</span></span>

![Wingtip Toys — страница по умолчанию](introduction-and-overview/_static/image1.png)

<span data-ttu-id="99e71-175">Вы можете зарегистрироваться как новый пользователь или войти как существующий пользователь.</span><span class="sxs-lookup"><span data-stu-id="99e71-175">You can register as a new user, or sign in as an existing user.</span></span> <span data-ttu-id="99e71-176">Верхняя навигация содержит ссылки на категории продуктов и их продукты из базы данных.</span><span class="sxs-lookup"><span data-stu-id="99e71-176">The top navigation has links to product categories and their products from the database.</span></span>

<span data-ttu-id="99e71-177">Если выбрано значение **продукты**, отображаются все доступные продукты.</span><span class="sxs-lookup"><span data-stu-id="99e71-177">If you select **Products**, all available products are displayed.</span></span> 

![Wingtip Toys — продукты](introduction-and-overview/_static/image2.png)

<span data-ttu-id="99e71-179">При выборе конкретного продукта отображаются сведения о продукте.</span><span class="sxs-lookup"><span data-stu-id="99e71-179">If you select a specific product, product details are displayed.</span></span>

![Wingtip Toys — сведения о продукте](introduction-and-overview/_static/image3.png)

<span data-ttu-id="99e71-181">Как пользователь, вы можете зарегистрироваться и войти в систему, используя функциональные возможности шаблона веб-форм по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="99e71-181">As a user, you can register and sign in with Web Forms template default functionality.</span></span> <span data-ttu-id="99e71-182">В этом учебнике также объясняется, как выполнить вход с использованием существующей учетной записи Gmail.</span><span class="sxs-lookup"><span data-stu-id="99e71-182">This tutorial also explains how to sign in using an existing Gmail account.</span></span> <span data-ttu-id="99e71-183">Кроме того, вы можете войти в систему от имени администратора, чтобы добавлять продукты в базу данных и удалять их из нее.</span><span class="sxs-lookup"><span data-stu-id="99e71-183">Additionally, you can sign in as the administrator to add and remove products from the database.</span></span>

![Wingtip Toys — вход](introduction-and-overview/_static/image4.png)

<span data-ttu-id="99e71-185">Войдя в систему как пользователь, вы можете добавить продукты в корзину для покупок и извлечь их с помощью PayPal.</span><span class="sxs-lookup"><span data-stu-id="99e71-185">Once you've signed in as a user, you can add products to the shopping cart and checkout with PayPal.</span></span> <span data-ttu-id="99e71-186">Пример приложения предназначен для работы в песочнице разработчика PayPal.</span><span class="sxs-lookup"><span data-stu-id="99e71-186">The sample application is designed to work in PayPal's developer sandbox.</span></span> <span data-ttu-id="99e71-187">Фактическая транзакция Money не выполняется.</span><span class="sxs-lookup"><span data-stu-id="99e71-187">No actual money transaction takes place.</span></span>

![Wingtip Toys — корзина для покупок](introduction-and-overview/_static/image5.png)

<span data-ttu-id="99e71-189">PayPal подтверждает сведения об учетной записи, заказе и платеже.</span><span class="sxs-lookup"><span data-stu-id="99e71-189">PayPal confirms your account, order, and payment information.</span></span>

![Wingtip Toys — PayPal](introduction-and-overview/_static/image6.png)

<span data-ttu-id="99e71-191">После возврата из PayPal можно проверить и выполнить заказ.</span><span class="sxs-lookup"><span data-stu-id="99e71-191">After returning from PayPal, you can review and complete your order.</span></span>

![Wingtip Toys — проверка заказа](introduction-and-overview/_static/image7.png)

## <a name="prerequisites"></a><span data-ttu-id="99e71-193">Необходимые компоненты</span><span class="sxs-lookup"><span data-stu-id="99e71-193">Prerequisites</span></span>

<span data-ttu-id="99e71-194">Прежде чем начать, убедитесь, что на компьютере установлено следующее программное обеспечение:</span><span class="sxs-lookup"><span data-stu-id="99e71-194">Before you start, make sure the following software is installed on your computer:</span></span>

- <span data-ttu-id="99e71-195">[Microsoft Visual Studio 2017 или Microsoft Visual Studio Community 2017](https://visualstudio.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="99e71-195">[Microsoft Visual Studio 2017 or Microsoft Visual Studio Community 2017](https://visualstudio.microsoft.com/downloads/).</span></span>

<span data-ttu-id="99e71-196">.NET Framework устанавливается автоматически.</span><span class="sxs-lookup"><span data-stu-id="99e71-196">The .NET Framework is installed automatically.</span></span>

<span data-ttu-id="99e71-197">В этой серии руководств используется Microsoft Visual Studio Community 2017.</span><span class="sxs-lookup"><span data-stu-id="99e71-197">This tutorial series uses Microsoft Visual Studio Community 2017.</span></span> <span data-ttu-id="99e71-198">Для выполнения этой серии руководств можно использовать либо Microsoft Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="99e71-198">You can use either that or Microsoft Visual Studio 2017 to complete this tutorial series.</span></span>

<span data-ttu-id="99e71-199">Обратите внимание на следующие сведения о Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="99e71-199">Note the following about Visual Studio:</span></span>

* <span data-ttu-id="99e71-200">Microsoft Visual Studio 2017 и Microsoft Visual Studio Community 2017 в рамках этой серии руководств называют *Visual Studio* .</span><span class="sxs-lookup"><span data-stu-id="99e71-200">Microsoft Visual Studio 2017 and Microsoft Visual Studio Community 2017 are referred to as *Visual Studio* throughout this tutorial series.</span></span>

* <span data-ttu-id="99e71-201">Visual Studio 2017 устанавливается рядом с уже установленными предыдущими версиями.</span><span class="sxs-lookup"><span data-stu-id="99e71-201">Visual Studio 2017 is installed next to any older versions already installed.</span></span> <span data-ttu-id="99e71-202">Сайты, созданные в более ранних версиях, можно открыть в Visual Studio 2017 и продолжить открытие в предыдущих версиях.</span><span class="sxs-lookup"><span data-stu-id="99e71-202">Sites created in earlier versions can be opened in Visual Studio 2017 and continue to open in previous versions.</span></span>

* <span data-ttu-id="99e71-203">При первом запуске Visual Studio предполагается, что выбраны параметры *веб-разработки* .</span><span class="sxs-lookup"><span data-stu-id="99e71-203">The first time you started Visual Studio, it is assumed you selected the *Web Development* settings.</span></span> <span data-ttu-id="99e71-204">Дополнительные сведения см. [в разделе как выбрать параметры среды веб-разработки](https://msdn.microsoft.com/library/ff521558.aspx).</span><span class="sxs-lookup"><span data-stu-id="99e71-204">For more information, see [How to: Select Web Development Environment Settings](https://msdn.microsoft.com/library/ff521558.aspx).</span></span>

<span data-ttu-id="99e71-205">После установки необходимых компонентов можно приступить к созданию веб-проекта, представленного в этой серии руководств.</span><span class="sxs-lookup"><span data-stu-id="99e71-205">After installing the prerequisites, you're ready to begin creating the Web project presented in this tutorial series.</span></span>

## <a name="download-the-sample-application"></a><span data-ttu-id="99e71-206">Загрузка примера приложения</span><span class="sxs-lookup"><span data-stu-id="99e71-206">Download the sample application</span></span>

 <span data-ttu-id="99e71-207">Готовый пример приложения можно загрузить в любое время с веб-сайта MSDN Samples:</span><span class="sxs-lookup"><span data-stu-id="99e71-207">You can download the completed sample application at anytime from the MSDN Samples site:</span></span>

<span data-ttu-id="99e71-208">[Начало работы с веб-формами ASP.NET 4,5 и Visual Studio 2013-Wingtip Toys](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) (C#)</span><span class="sxs-lookup"><span data-stu-id="99e71-208">[Getting Started with ASP.NET 4.5 Web Forms and Visual Studio 2013 - Wingtip Toys](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) (C#)</span></span> 

 <span data-ttu-id="99e71-209">Этот загружаемый файл содержит следующие элементы:</span><span class="sxs-lookup"><span data-stu-id="99e71-209">This download has the following items:</span></span>

- <span data-ttu-id="99e71-210">Пример приложения в папке *WingtipToys*</span><span class="sxs-lookup"><span data-stu-id="99e71-210">The sample application in the *WingtipToys* folder.</span></span>
- <span data-ttu-id="99e71-211">Ресурсы, используемые для создания примера приложения в папке *WingtipToys-Assets* в папке *WingtipToys* .</span><span class="sxs-lookup"><span data-stu-id="99e71-211">The resources used to create the sample application in the *WingtipToys-Assets* folder in the *WingtipToys* folder.</span></span>

<span data-ttu-id="99e71-212">Загружаемый файл является *ZIP* -файлом.</span><span class="sxs-lookup"><span data-stu-id="99e71-212">The download is a *.zip* file.</span></span> <span data-ttu-id="99e71-213">Чтобы просмотреть завершенный проект, созданный этой серией руководств, найдите и выберите *C#* папку в ZIP-файле.</span><span class="sxs-lookup"><span data-stu-id="99e71-213">To see the completed project that this tutorial series creates, find and select the *C#* folder in the .zip file.</span></span> <span data-ttu-id="99e71-214">Сохраните C# папку в папку, используемую для работы с проектами Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="99e71-214">Save the C# folder to the folder you use to work with Visual Studio projects.</span></span> <span data-ttu-id="99e71-215">По умолчанию папка проектов Visual Studio 2017 имеет следующие значения:</span><span class="sxs-lookup"><span data-stu-id="99e71-215">By default, the Visual Studio 2017 projects folder is:</span></span>

<span data-ttu-id="99e71-216"><strong>C:\Users&#92;</strong>  <strong><em>&lt;имя пользователя&gt;</em></strong> <strong>\саурце\репос</strong></span><span class="sxs-lookup"><span data-stu-id="99e71-216"><strong>C:\Users&#92;</strong><strong><em>&lt;username&gt;</em></strong><strong>\source\repos</strong></span></span>

<span data-ttu-id="99e71-217">Переименуйте ***C#*** папку в ***WingtipToys***.</span><span class="sxs-lookup"><span data-stu-id="99e71-217">Rename the ***C#*** folder to ***WingtipToys***.</span></span>

> [!NOTE]
> <span data-ttu-id="99e71-218">Если у вас уже есть папка с именем *WingtipToys* в папке Projects, временно переименуйте существующую папку, прежде чем *C#* переименовывать папку в *WingtipToys*.</span><span class="sxs-lookup"><span data-stu-id="99e71-218">If you already have a folder named *WingtipToys* in your Projects folder, temporarily rename that existing folder before renaming the *C#* folder to *WingtipToys*.</span></span>

<span data-ttu-id="99e71-219">Чтобы запустить завершенный проект, откройте папку *WingtipToys* и дважды щелкните файл *WingtipToys. sln* .</span><span class="sxs-lookup"><span data-stu-id="99e71-219">To run the completed project, open the *WingtipToys* folder and double-click the *WingtipToys.sln* file.</span></span> <span data-ttu-id="99e71-220">Visual Studio 2017 откроет проект.</span><span class="sxs-lookup"><span data-stu-id="99e71-220">Visual Studio 2017 opens the project.</span></span> <span data-ttu-id="99e71-221">Затем щелкните правой кнопкой мыши файл *Default. aspx* в **Обозреватель решений** и выберите **Просмотреть в браузере**.</span><span class="sxs-lookup"><span data-stu-id="99e71-221">Next, right-click the *Default.aspx* file in **Solution Explorer** and select **View In Browser**.</span></span>

## <a name="take-a-aspnet-web-forms-quiz-to-review-content"></a><span data-ttu-id="99e71-222">Пройдите викторину веб-форм ASP.NET для просмотра содержимого</span><span class="sxs-lookup"><span data-stu-id="99e71-222">Take a ASP.NET Web Forms quiz to review content</span></span>

<span data-ttu-id="99e71-223">После завершения серии руководств пройдите викторину, чтобы протестировать свои знания и получить основные понятия.</span><span class="sxs-lookup"><span data-stu-id="99e71-223">After completing the tutorial series, take a quiz to test your knowledge and reinforce key concepts.</span></span> <span data-ttu-id="99e71-224">Каждый вопрос содержит пояснения и ссылки на дополнительные рекомендации.</span><span class="sxs-lookup"><span data-stu-id="99e71-224">Each question provides an explanation and links to additional guidance.</span></span>

* [<span data-ttu-id="99e71-225">Викторина веб-форм ASP.NET</span><span class="sxs-lookup"><span data-stu-id="99e71-225">ASP.NET Web Forms Quiz</span></span>](https://blogs.msdn.microsoft.com/erikreitan/2016/01/08/asp-net-web-forms-quiz/) 

## <a name="tutorial-support-and-comments"></a><span data-ttu-id="99e71-226">Поддержка и комментарии в учебнике</span><span class="sxs-lookup"><span data-stu-id="99e71-226">Tutorial support and comments</span></span>

<span data-ttu-id="99e71-227">Для вопросов и комментариев Используйте раздел вопросов и ответов, включенный в [Начало работы с помощью веб-форм ASP.NET 4,5 и Visual Studio 2013-Wingtip Toys](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) (C#).</span><span class="sxs-lookup"><span data-stu-id="99e71-227">For questions and comments, use the Q and A section included on the [Getting Started with ASP.NET 4.5 Web Forms and Visual Studio 2013 - Wingtip Toys](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) (C#) sample page.</span></span>

<span data-ttu-id="99e71-228">Комментарии в этой серии руководств — это Добро пожаловать.</span><span class="sxs-lookup"><span data-stu-id="99e71-228">Comments on this tutorial series are welcome.</span></span> <span data-ttu-id="99e71-229">При обновлении этой серии руководств выполняются все усилия, касающиеся исправлений и предложений по улучшению.</span><span class="sxs-lookup"><span data-stu-id="99e71-229">When this tutorial series is updated, every effort is made to consider corrections or suggestions for improvements.</span></span>

<span data-ttu-id="99e71-230">При возникновении ошибки соответствующие сообщения об ошибках могут быть запутанными, без хорошего объяснения о том, как ее исправить.</span><span class="sxs-lookup"><span data-stu-id="99e71-230">If an error occurs, the corresponding error messages could be confusing, with no good explanation on how to fix it.</span></span> <span data-ttu-id="99e71-231">Справку можно просмотреть на [форумах ASP.NET](https://forums.asp.net/).</span><span class="sxs-lookup"><span data-stu-id="99e71-231">For help, you can check the [ASP.NET forums](https://forums.asp.net/).</span></span> <span data-ttu-id="99e71-232">Еще одним хорошим источником является раздел Q и A статьи [Начало работы with ASP.NET 4,5 Web Forms and Visual Studio 2013-Wingtip Toys](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) (C#).</span><span class="sxs-lookup"><span data-stu-id="99e71-232">Another good source is the Q and A section in the [Getting Started with ASP.NET 4.5 Web Forms and Visual Studio 2013 - Wingtip Toys](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) (C#) sample page.</span></span> 

> [!div class="step-by-step"]
> [<span data-ttu-id="99e71-233">Вперед</span><span class="sxs-lookup"><span data-stu-id="99e71-233">Next</span></span>](create-the-project.md)
