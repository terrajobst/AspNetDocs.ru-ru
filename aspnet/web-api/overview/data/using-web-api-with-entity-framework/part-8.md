---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-8
title: Отобразить сведения об элементе | Документация Майкрософт
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/16/2014
ms.assetid: 75ef94b1-bbec-4681-9210-452dba816144
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-8
msc.type: authoredcontent
ms.openlocfilehash: 3f48c5ad73ceb9a4873fbbb621b518553a498966
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78449004"
---
# <a name="display-item-details"></a><span data-ttu-id="91385-102">Отображение сведений об элементе</span><span class="sxs-lookup"><span data-stu-id="91385-102">Display Item Details</span></span>

<span data-ttu-id="91385-103">по [Майк Уоссон](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="91385-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="91385-104">Скачать завершенный проект</span><span class="sxs-lookup"><span data-stu-id="91385-104">Download Completed Project</span></span>](https://github.com/MikeWasson/BookService)

<span data-ttu-id="91385-105">В этом разделе вы добавите возможность просмотра сведений для каждой книги.</span><span class="sxs-lookup"><span data-stu-id="91385-105">In this section, you will add the ability to view details for each book.</span></span> <span data-ttu-id="91385-106">В App. js добавьте в модель представления следующий код:</span><span class="sxs-lookup"><span data-stu-id="91385-106">In app.js, add to the following code to the view model:</span></span>

[!code-javascript[Main](part-8/samples/sample1.js)]

<span data-ttu-id="91385-107">В Views/Home/Index. cshtml добавьте элемент привязки данных к ссылке Details:</span><span class="sxs-lookup"><span data-stu-id="91385-107">In Views/Home/Index.cshtml, add a data-bind element to the Details link:</span></span>

[!code-html[Main](part-8/samples/sample2.html?highlight=5)]

<span data-ttu-id="91385-108">Это привязывает обработчик щелчка для &lt;элемента&gt; к функции `getBookDetail` в модели представления.</span><span class="sxs-lookup"><span data-stu-id="91385-108">This binds the click handler for the &lt;a&gt; element to the `getBookDetail` function on the view model.</span></span>

<span data-ttu-id="91385-109">В том же файле замените следующую отметку:</span><span class="sxs-lookup"><span data-stu-id="91385-109">In the same file, replace the following mark-up:</span></span>

[!code-html[Main](part-8/samples/sample3.html)]

<span data-ttu-id="91385-110">следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="91385-110">with this:</span></span>

[!code-html[Main](part-8/samples/sample4.html)]

<span data-ttu-id="91385-111">Эта разметка создает таблицу, привязанную к данным в свойствах `detail` наблюдаемых в модели представления.</span><span class="sxs-lookup"><span data-stu-id="91385-111">This markup creates a table that is data-bound to the properties of the `detail` observable in the view model.</span></span>

<span data-ttu-id="91385-112">Синтаксис&lt;!--Ko--&gt;&quot; позволяет включить привязку маскирования за пределы элемента DOM.</span><span class="sxs-lookup"><span data-stu-id="91385-112">The "&lt;!-- ko --&gt;&quot; syntax lets you include a Knockout binding outside of a DOM element.</span></span> <span data-ttu-id="91385-113">В этом случае привязка `if` вызывает отображение этого раздела разметки только в том случае, если `details` не имеет значение null.</span><span class="sxs-lookup"><span data-stu-id="91385-113">In this case, the `if` binding causes this section of markup to be displayed only when `details` is non-null.</span></span>

[!code-html[Main](part-8/samples/sample5.html)]

<span data-ttu-id="91385-114">Теперь, если запустить приложение и щелкнуть одну из &quot;сведений&quot; ссылок, приложение отобразит сведения о книге.</span><span class="sxs-lookup"><span data-stu-id="91385-114">Now if you run the app and click one of the &quot;Detail&quot; links, the app will display the book details.</span></span>

[![](part-8/_static/image2.png)](part-8/_static/image1.png)

> [!div class="step-by-step"]
> <span data-ttu-id="91385-115">[Назад](part-7.md)
> [Вперед](part-9.md)</span><span class="sxs-lookup"><span data-stu-id="91385-115">[Previous](part-7.md)
[Next](part-9.md)</span></span>
