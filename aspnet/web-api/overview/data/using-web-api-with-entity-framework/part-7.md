---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-7
title: Создание представления (пользовательский интерфейс) | Документация Майкрософт
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/16/2014
ms.assetid: b2445062-a1fe-4133-8994-f510280f6d9a
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-7
msc.type: authoredcontent
ms.openlocfilehash: 62c4523c2c6fb399cfbc3716309a1379996d601c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78448986"
---
# <a name="create-the-view-ui"></a><span data-ttu-id="e272b-102">Создание представления (пользовательский интерфейс)</span><span class="sxs-lookup"><span data-stu-id="e272b-102">Create the View (UI)</span></span>

<span data-ttu-id="e272b-103">по [Майк Уоссон](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="e272b-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="e272b-104">Скачать завершенный проект</span><span class="sxs-lookup"><span data-stu-id="e272b-104">Download Completed Project</span></span>](https://github.com/MikeWasson/BookService)

<span data-ttu-id="e272b-105">В этом разделе вы начнете определить HTML для приложения и добавить привязку данных между HTML и моделью представления.</span><span class="sxs-lookup"><span data-stu-id="e272b-105">In this section, you will start to define the HTML for the app, and add data binding between the HTML and the view model.</span></span>

<span data-ttu-id="e272b-106">Откройте файл Views/Home/Index. cshtml.</span><span class="sxs-lookup"><span data-stu-id="e272b-106">Open the file Views/Home/Index.cshtml.</span></span> <span data-ttu-id="e272b-107">Замените все содержимое этого файла следующим.</span><span class="sxs-lookup"><span data-stu-id="e272b-107">Replace the entire contents of that file with the following.</span></span>

[!code-cshtml[Main](part-7/samples/sample1.cshtml)]

<span data-ttu-id="e272b-108">Большая часть элементов `div` существует для стиля [начальной загрузки](http://getbootstrap.com/) .</span><span class="sxs-lookup"><span data-stu-id="e272b-108">Most of the `div` elements are there for [Bootstrap](http://getbootstrap.com/) styling.</span></span> <span data-ttu-id="e272b-109">Важные элементы — это объекты с атрибутами `data-bind`.</span><span class="sxs-lookup"><span data-stu-id="e272b-109">The important elements are the ones with `data-bind` attributes.</span></span> <span data-ttu-id="e272b-110">Этот атрибут связывает HTML с моделью представления.</span><span class="sxs-lookup"><span data-stu-id="e272b-110">This attribute links the HTML to the view model.</span></span>

<span data-ttu-id="e272b-111">Пример:</span><span class="sxs-lookup"><span data-stu-id="e272b-111">For example:</span></span>

[!code-html[Main](part-7/samples/sample2.html)]

<span data-ttu-id="e272b-112">В этом примере Привязка &quot;`text`&quot; приводит к тому, что элемент `<p>` отображает значение свойства `error` из модели представления.</span><span class="sxs-lookup"><span data-stu-id="e272b-112">In this example, the &quot;`text`&quot; binding causes the `<p>` element to show the value of the `error` property from the view model.</span></span> <span data-ttu-id="e272b-113">Помните, что `error` был объявлен как `ko.observable`:</span><span class="sxs-lookup"><span data-stu-id="e272b-113">Recall that `error` was declared as a `ko.observable`:</span></span>

[!code-javascript[Main](part-7/samples/sample3.js)]

<span data-ttu-id="e272b-114">Всякий раз, когда новому значению присваивается `error`, выколачивание обновляет текст в элементе `<p>`.</span><span class="sxs-lookup"><span data-stu-id="e272b-114">Whenever a new value is assigned to `error`, Knockout updates the text in the `<p>` element.</span></span>

<span data-ttu-id="e272b-115">Привязка `foreach` передается в цикл по содержимому массива `books`.</span><span class="sxs-lookup"><span data-stu-id="e272b-115">The `foreach` binding tells Knockout to loop through the contents of the `books` array.</span></span> <span data-ttu-id="e272b-116">Для каждого элемента в массиве выколачивание создает новый элемент &lt;Li&gt;.</span><span class="sxs-lookup"><span data-stu-id="e272b-116">For each item in the array, Knockout creates a new &lt;li&gt; element.</span></span> <span data-ttu-id="e272b-117">Привязки в контексте `foreach` ссылаются на свойства элемента массива.</span><span class="sxs-lookup"><span data-stu-id="e272b-117">Bindings inside the context of the `foreach` refer to properties on the array item.</span></span> <span data-ttu-id="e272b-118">Пример:</span><span class="sxs-lookup"><span data-stu-id="e272b-118">For example:</span></span>

[!code-html[Main](part-7/samples/sample4.html)]

<span data-ttu-id="e272b-119">Здесь привязка `text` считывает свойство Author каждой книги.</span><span class="sxs-lookup"><span data-stu-id="e272b-119">Here the `text` binding reads the Author property of each book.</span></span>

<span data-ttu-id="e272b-120">Если запустить приложение сейчас, оно должно выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="e272b-120">If you run the application now, it should look like this:</span></span>

![](part-7/_static/image1.png)

<span data-ttu-id="e272b-121">Список книг загружается асинхронно после загрузки страницы.</span><span class="sxs-lookup"><span data-stu-id="e272b-121">The list of books loads asynchronously, after the page loads.</span></span> <span data-ttu-id="e272b-122">Сейчас &quot;сведения&quot; ссылок не работают.</span><span class="sxs-lookup"><span data-stu-id="e272b-122">Right now, the &quot;Details&quot; links are not functional.</span></span> <span data-ttu-id="e272b-123">Мы добавим эту функцию в следующем разделе.</span><span class="sxs-lookup"><span data-stu-id="e272b-123">We'll add this functionality in the next section.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="e272b-124">[Назад](part-6.md)
> [Вперед](part-8.md)</span><span class="sxs-lookup"><span data-stu-id="e272b-124">[Previous](part-6.md)
[Next](part-8.md)</span></span>
