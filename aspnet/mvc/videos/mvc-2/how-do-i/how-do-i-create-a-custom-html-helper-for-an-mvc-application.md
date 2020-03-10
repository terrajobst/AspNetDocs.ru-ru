---
uid: mvc/videos/mvc-2/how-do-i/how-do-i-create-a-custom-html-helper-for-an-mvc-application
title: Инструкции. Создание пользовательского вспомогательного метода HTML для приложения MVC | Документы Майкрософт
author: rick-anderson
description: В этом видео Крис пикселей показано, как создать пользовательский HtmlHelper, недоступный в стандартном наборе в приложении MVC. Во-первых, пример MVC прило...
ms.author: riande
ms.date: 12/11/2009
ms.assetid: 58b5eb15-4160-4ce2-ae70-6ba94262ea73
msc.legacyurl: /mvc/videos/mvc-2/how-do-i/how-do-i-create-a-custom-html-helper-for-an-mvc-application
msc.type: video
ms.openlocfilehash: 60953243d3038667e4f729b1394e68f0c9d7c178
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78450480"
---
# <a name="how-do-i-create-a-custom-html-helper-for-an-mvc-application"></a><span data-ttu-id="f82ec-105">Инструкции. Создание пользовательского вспомогательного метода HTML для приложения MVC</span><span class="sxs-lookup"><span data-stu-id="f82ec-105">How Do I: Create a Custom HTML Helper for an MVC Application?</span></span>

<span data-ttu-id="f82ec-106">от [Крис пикселей](https://twitter.com/chrispels)</span><span class="sxs-lookup"><span data-stu-id="f82ec-106">by [Chris Pels](https://twitter.com/chrispels)</span></span>

<span data-ttu-id="f82ec-107">В этом видео Крис пикселей показано, как создать пользовательский HtmlHelper, недоступный в стандартном наборе в приложении MVC.</span><span class="sxs-lookup"><span data-stu-id="f82ec-107">In this video Chris Pels shows how to create a custom HtmlHelper that is not available in the standard set in an MVC application.</span></span> <span data-ttu-id="f82ec-108">Во-первых, пример приложения MVC создается с демонстрационным контроллером и представлением для тестирования пользовательского HtmlHelper.</span><span class="sxs-lookup"><span data-stu-id="f82ec-108">First, a sample MVC application is created with a demo controller and view to test the custom HtmlHelper.</span></span> <span data-ttu-id="f82ec-109">Затем создается модуль с открытой функцией, которая является методом расширения, представляющим реализацию пользовательского HtmlHelper.</span><span class="sxs-lookup"><span data-stu-id="f82ec-109">Next, a module is created with a public function that is an extension method which represents the implementation of the custom HtmlHelper.</span></span> <span data-ttu-id="f82ec-110">Пользовательский вспомогательный метод предназначен для создания тегов `<img>` на странице и получения нескольких входящих параметров, включая идентификатор, URL-адрес и замещающий текст для тега Image.</span><span class="sxs-lookup"><span data-stu-id="f82ec-110">The custom helper is for creating `<img>` tags in a page and receives several inbound parameters including the id, url, and alt text for the image tag.</span></span> <span data-ttu-id="f82ec-111">Затем логика добавляется в функцию для возвращения завершенного тега `<img>` с указанными сведениями.</span><span class="sxs-lookup"><span data-stu-id="f82ec-111">The logic is then added to the function for returning the completed `<img>` tag with the specified information.</span></span> <span data-ttu-id="f82ec-112">Затем пользовательское HtmlHelper используется на демонстрационной странице для вывода изображения.</span><span class="sxs-lookup"><span data-stu-id="f82ec-112">Then the custom HtmlHelper is used on the demo page to display an image.</span></span> <span data-ttu-id="f82ec-113">Наконец, Пользовательский HtmlHelper расширяется для включения нескольких переопределений конструктора, которые обеспечивают гибкость для упрощения создания различных тегов `<img>`.</span><span class="sxs-lookup"><span data-stu-id="f82ec-113">Finally, the custom HtmlHelper is expanded to include multiple constructor overrides which provide flexibility for more easily creating different `<img>` tags.</span></span>

[<span data-ttu-id="f82ec-114">&#9654;Смотреть видео (18 минут)</span><span class="sxs-lookup"><span data-stu-id="f82ec-114">&#9654; Watch video (18 minutes)</span></span>](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-create-a-custom-html-helper-for-an-mvc-application)

> [!div class="step-by-step"]
> <span data-ttu-id="f82ec-115">[Назад](how-do-i-implement-view-models-to-manage-data-for-aspnet-mvc-views.md)
> [Вперед](how-do-i-work-with-model-binders-in-an-mvc-application.md)</span><span class="sxs-lookup"><span data-stu-id="f82ec-115">[Previous](how-do-i-implement-view-models-to-manage-data-for-aspnet-mvc-views.md)
[Next](how-do-i-work-with-model-binders-in-an-mvc-application.md)</span></span>
