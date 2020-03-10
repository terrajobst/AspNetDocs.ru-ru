---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-6
title: Создание клиента JavaScript | Документация Майкрософт
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/16/2014
ms.assetid: 20360326-b123-4b1e-abae-1d350edf4ce4
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-6
msc.type: authoredcontent
ms.openlocfilehash: 74f2cc4e5e401d690042b05b028dfc0c46ae282a
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78504726"
---
# <a name="create-the-javascript-client"></a><span data-ttu-id="5bdda-102">Создание клиента JavaScript</span><span class="sxs-lookup"><span data-stu-id="5bdda-102">Create the JavaScript Client</span></span>

<span data-ttu-id="5bdda-103">по [Майк Уоссон](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="5bdda-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="5bdda-104">Скачать завершенный проект</span><span class="sxs-lookup"><span data-stu-id="5bdda-104">Download Completed Project</span></span>](https://github.com/MikeWasson/BookService)

<span data-ttu-id="5bdda-105">В этом разделе вы создадите клиент для приложения, используя HTML, JavaScript и библиотеку [маскирования. js](http://knockoutjs.com/) .</span><span class="sxs-lookup"><span data-stu-id="5bdda-105">In this section, you will create the client for the application, using HTML, JavaScript, and the [Knockout.js](http://knockoutjs.com/) library.</span></span> <span data-ttu-id="5bdda-106">Клиентское приложение будет построено поэтапно:</span><span class="sxs-lookup"><span data-stu-id="5bdda-106">We'll build the client app in stages:</span></span>

- <span data-ttu-id="5bdda-107">Отображение списка книг.</span><span class="sxs-lookup"><span data-stu-id="5bdda-107">Showing a list of books.</span></span>
- <span data-ttu-id="5bdda-108">Отображение сведений о книге.</span><span class="sxs-lookup"><span data-stu-id="5bdda-108">Showing a book detail.</span></span>
- <span data-ttu-id="5bdda-109">Добавление новой книги.</span><span class="sxs-lookup"><span data-stu-id="5bdda-109">Adding a new book.</span></span>

<span data-ttu-id="5bdda-110">Библиотека маскирования использует шаблон Model-View-ViewModel (MVVM):</span><span class="sxs-lookup"><span data-stu-id="5bdda-110">The Knockout library uses the Model-View-ViewModel (MVVM) pattern:</span></span>

- <span data-ttu-id="5bdda-111">**Модель** — это серверное представление данных в бизнес-домене (в нашем случае это книги и авторы).</span><span class="sxs-lookup"><span data-stu-id="5bdda-111">The **model** is the server-side representation of the data in the business domain (in our case, books and authors).</span></span>
- <span data-ttu-id="5bdda-112">**Представление** — это уровень представления (HTML).</span><span class="sxs-lookup"><span data-stu-id="5bdda-112">The **view** is the presentation layer (HTML).</span></span>
- <span data-ttu-id="5bdda-113">**Модель представления** — это объект JavaScript, содержащий модели.</span><span class="sxs-lookup"><span data-stu-id="5bdda-113">The **view model** is a JavaScript object that holds the models.</span></span> <span data-ttu-id="5bdda-114">Модель представления является абстракцией кода пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="5bdda-114">The view model is a code abstraction of the UI.</span></span> <span data-ttu-id="5bdda-115">Он не имеет сведений о представлении HTML.</span><span class="sxs-lookup"><span data-stu-id="5bdda-115">It has no knowledge of the HTML representation.</span></span> <span data-ttu-id="5bdda-116">Вместо этого он представляет абстрактные функции представления, например &quot;список книг&quot;.</span><span class="sxs-lookup"><span data-stu-id="5bdda-116">Instead, it represents abstract features of the view, such as &quot;a list of books&quot;.</span></span>

<span data-ttu-id="5bdda-117">Представление привязано к модели представления.</span><span class="sxs-lookup"><span data-stu-id="5bdda-117">The view is data-bound to the view model.</span></span> <span data-ttu-id="5bdda-118">Обновления модели представления автоматически отражаются в представлении.</span><span class="sxs-lookup"><span data-stu-id="5bdda-118">Updates to the view model are automatically reflected in the view.</span></span> <span data-ttu-id="5bdda-119">Модель представления также получает события из представления, например нажатия кнопок.</span><span class="sxs-lookup"><span data-stu-id="5bdda-119">The view model also gets events from the view, such as button clicks.</span></span>

![](part-6/_static/image1.png)

<span data-ttu-id="5bdda-120">Такой подход упрощает изменение макета и пользовательского интерфейса приложения, так как вы можете изменить привязки, не переписывая код.</span><span class="sxs-lookup"><span data-stu-id="5bdda-120">This approach makes it easy to change the layout and UI of your app, because you can change the bindings, without rewriting any code.</span></span> <span data-ttu-id="5bdda-121">Например, можно отобразить список элементов в виде `<ul>`, а затем изменить его позже на таблицу.</span><span class="sxs-lookup"><span data-stu-id="5bdda-121">For example, you might show a list of items as a `<ul>`, then change it later to a table.</span></span>

## <a name="add-the-knockout-library"></a><span data-ttu-id="5bdda-122">Добавление библиотеки маскирования</span><span class="sxs-lookup"><span data-stu-id="5bdda-122">Add the Knockout Library</span></span>

<span data-ttu-id="5bdda-123">В Visual Studio в меню **Сервис** выберите **Диспетчер пакетов NuGet**.</span><span class="sxs-lookup"><span data-stu-id="5bdda-123">In Visual Studio, from the **Tools** menu, select **NuGet Package Manager**.</span></span> <span data-ttu-id="5bdda-124">Затем щелкните **Консоль диспетчера пакетов**.</span><span class="sxs-lookup"><span data-stu-id="5bdda-124">Then select **Package Manager Console**.</span></span> <span data-ttu-id="5bdda-125">В окне "Консоль диспетчера пакетов" введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="5bdda-125">In the Package Manager Console window, enter the following command:</span></span>

[!code-console[Main](part-6/samples/sample1.cmd)]

<span data-ttu-id="5bdda-126">Эта команда добавляет файлы маскирования в папку Scripts.</span><span class="sxs-lookup"><span data-stu-id="5bdda-126">This command adds the Knockout files to the Scripts folder.</span></span>

## <a name="create-the-view-model"></a><span data-ttu-id="5bdda-127">Создание модели представления</span><span class="sxs-lookup"><span data-stu-id="5bdda-127">Create the View Model</span></span>

<span data-ttu-id="5bdda-128">Добавьте в папку Scripts файл JavaScript с именем App. js.</span><span class="sxs-lookup"><span data-stu-id="5bdda-128">Add a JavaScript file named app.js to the Scripts folder.</span></span> <span data-ttu-id="5bdda-129">(В обозреватель решений щелкните правой кнопкой мыши папку скрипты, выберите **Добавить**, а затем выберите пункт **файл JavaScript**.) Вставьте следующий код:</span><span class="sxs-lookup"><span data-stu-id="5bdda-129">(In Solution Explorer, right-click the Scripts folder, select **Add**, then select **JavaScript File**.) Paste in the following code:</span></span>

[!code-javascript[Main](part-6/samples/sample2.js)]

<span data-ttu-id="5bdda-130">В маскировании класс `observable` обеспечивает привязку данных.</span><span class="sxs-lookup"><span data-stu-id="5bdda-130">In Knockout, the `observable` class enables data-binding.</span></span> <span data-ttu-id="5bdda-131">Когда содержимое наблюдаемого изменения, наблюдаемое изменение уведомляет все элементы управления, привязанные к данным, поэтому они могут обновлять себя.</span><span class="sxs-lookup"><span data-stu-id="5bdda-131">When the contents of an observable change, the observable notifies all of the data-bound controls, so they can update themselves.</span></span> <span data-ttu-id="5bdda-132">(Класс `observableArray` — это версия *наблюдаемого*объекта.) Для начала наша модель представления имеет два observable:</span><span class="sxs-lookup"><span data-stu-id="5bdda-132">(The `observableArray` class is the array version of *observable*.) To start with, our view model has two observables:</span></span>

- <span data-ttu-id="5bdda-133">`books` содержит список книг.</span><span class="sxs-lookup"><span data-stu-id="5bdda-133">`books` holds the list of books.</span></span>
- <span data-ttu-id="5bdda-134">`error` содержит сообщение об ошибке при сбое вызова AJAX.</span><span class="sxs-lookup"><span data-stu-id="5bdda-134">`error` contains an error message if an AJAX call fails.</span></span>

<span data-ttu-id="5bdda-135">Метод `getAllBooks` делает вызов AJAX для получения списка книг.</span><span class="sxs-lookup"><span data-stu-id="5bdda-135">The `getAllBooks` method makes an AJAX call to get the list of books.</span></span> <span data-ttu-id="5bdda-136">Затем он помещает результат в массив `books`.</span><span class="sxs-lookup"><span data-stu-id="5bdda-136">Then it pushes the result onto the `books` array.</span></span>

<span data-ttu-id="5bdda-137">Метод `ko.applyBindings` является частью библиотеки маскирования.</span><span class="sxs-lookup"><span data-stu-id="5bdda-137">The `ko.applyBindings` method is part of the Knockout library.</span></span> <span data-ttu-id="5bdda-138">Он принимает модель представления в качестве параметра и настраивает привязку данных.</span><span class="sxs-lookup"><span data-stu-id="5bdda-138">It takes the view model as a parameter and sets up the data binding.</span></span>

## <a name="add-a-script-bundle"></a><span data-ttu-id="5bdda-139">Добавление пакета сценариев</span><span class="sxs-lookup"><span data-stu-id="5bdda-139">Add a Script Bundle</span></span>

<span data-ttu-id="5bdda-140">Объединение — это функция в ASP.NET 4,5, которая упрощает объединение нескольких файлов в один файл.</span><span class="sxs-lookup"><span data-stu-id="5bdda-140">Bundling is a feature in ASP.NET 4.5 that makes it easy to combine or bundle multiple files into a single file.</span></span> <span data-ttu-id="5bdda-141">Объединение сокращает количество запросов к серверу, что может повысить время загрузки страницы.</span><span class="sxs-lookup"><span data-stu-id="5bdda-141">Bundling reduces the number of requests to the server, which can improve page load time.</span></span>

<span data-ttu-id="5bdda-142">Откройте файл App\_Start/Бундлеконфиг. cs.</span><span class="sxs-lookup"><span data-stu-id="5bdda-142">Open the file App\_Start/BundleConfig.cs.</span></span> <span data-ttu-id="5bdda-143">Добавьте следующий код в метод Регистербундлес.</span><span class="sxs-lookup"><span data-stu-id="5bdda-143">Add the following code to the RegisterBundles method.</span></span>

[!code-csharp[Main](part-6/samples/sample3.cs)]

> [!div class="step-by-step"]
> <span data-ttu-id="5bdda-144">[Назад](part-5.md)
> [Вперед](part-7.md)</span><span class="sxs-lookup"><span data-stu-id="5bdda-144">[Previous](part-5.md)
[Next](part-7.md)</span></span>
