---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part7
title: Добавление проверки в модель | Документация Майкрософт
author: shanselman
description: Это руководство для начинающих, в котором представлены основы ASP.NET MVC. Создание простого веб-приложения, считывающего и записывающего данные из базы данных.
ms.author: riande
ms.date: 08/14/2010
ms.assetid: aa7b3e8e-e23d-49f1-b160-f99a7f2982bd
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part7
msc.type: authoredcontent
ms.openlocfilehash: 9403be574324c34edf93bef1e0e4fd7ba68a3a9d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78437280"
---
# <a name="adding-validation-to-the-model"></a><span data-ttu-id="2a96f-104">Добавление проверки в модель</span><span class="sxs-lookup"><span data-stu-id="2a96f-104">Adding Validation to the Model</span></span>

<span data-ttu-id="2a96f-105">по [Скотт Hanselman](https://github.com/shanselman)</span><span class="sxs-lookup"><span data-stu-id="2a96f-105">by [Scott Hanselman](https://github.com/shanselman)</span></span>

> <span data-ttu-id="2a96f-106">Это руководство для начинающих, в котором представлены основы ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="2a96f-106">This is a beginner tutorial that introduces the basics of ASP.NET MVC.</span></span> <span data-ttu-id="2a96f-107">Вы создадите простое веб-приложение, считывающее и записывающее данные из базы данных.</span><span class="sxs-lookup"><span data-stu-id="2a96f-107">You'll create a simple web application that reads and writes from a database.</span></span> <span data-ttu-id="2a96f-108">Посетите [центр обучения ASP.NET MVC](../../../index.md) , чтобы найти другие руководства и примеры для ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="2a96f-108">Visit the [ASP.NET MVC learning center](../../../index.md) to find other ASP.NET MVC tutorials and samples.</span></span>

<span data-ttu-id="2a96f-109">В этом разделе мы будем реализовывать поддержку, необходимую для включения проверки входных данных в приложении.</span><span class="sxs-lookup"><span data-stu-id="2a96f-109">In this section we are going to implement the support necessary to enable input validation within our application.</span></span> <span data-ttu-id="2a96f-110">Мы гарантируем, что содержимое базы данных будет всегда правильным и предоставлять полезные сообщения об ошибках конечным пользователям при попытке ввести недопустимые данные фильмов.</span><span class="sxs-lookup"><span data-stu-id="2a96f-110">We'll ensure that our database content is always correct, and provide helpful error messages to end users when they try and enter Movie data which is not valid.</span></span> <span data-ttu-id="2a96f-111">Начнем с добавления немалой логики проверки к классу Movie.</span><span class="sxs-lookup"><span data-stu-id="2a96f-111">We'll begin by adding a little validation logic to the Movie class.</span></span>

<span data-ttu-id="2a96f-112">Щелкните правой кнопкой мыши папку Model и выберите пункт Добавить класс.</span><span class="sxs-lookup"><span data-stu-id="2a96f-112">Right click on the Model folder and select Add Class.</span></span> <span data-ttu-id="2a96f-113">Присвойте классу имя Movie.</span><span class="sxs-lookup"><span data-stu-id="2a96f-113">Name your class Movie.</span></span>

<span data-ttu-id="2a96f-114">Когда мы создали сущностную модель фильмов ранее, интегрированная среда разработки создала класс Movie.</span><span class="sxs-lookup"><span data-stu-id="2a96f-114">When we created the Movie Entity Model earlier, the IDE created a Movie class.</span></span> <span data-ttu-id="2a96f-115">Фактически часть класса Movie может находиться в одном файле, а часть — в другом.</span><span class="sxs-lookup"><span data-stu-id="2a96f-115">In fact, part of the Movie class can be in one file and part in another.</span></span> <span data-ttu-id="2a96f-116">Это называется частичным классом.</span><span class="sxs-lookup"><span data-stu-id="2a96f-116">This is called a Partial Class.</span></span> <span data-ttu-id="2a96f-117">Мы будем расширять класс Movie из другого файла.</span><span class="sxs-lookup"><span data-stu-id="2a96f-117">We're going to extend the Movie class from another file.</span></span>

<span data-ttu-id="2a96f-118">Мы создадим частичный класс Movie, который указывает на "дружественный класс" с некоторыми атрибутами, которые будут предоставлять системе указания по проверке.</span><span class="sxs-lookup"><span data-stu-id="2a96f-118">We'll create a partial movie class that points to a "buddy class" with some attributes that will give validation hints to the system.</span></span> <span data-ttu-id="2a96f-119">Мы помечаем заголовок и цену как обязательные, а также намерены, чтобы цена была в определенном диапазоне.</span><span class="sxs-lookup"><span data-stu-id="2a96f-119">We'll mark the Title and Price as Required, and also insist that the Price be within a certain range.</span></span> <span data-ttu-id="2a96f-120">Щелкните правой кнопкой мыши папку модели и выберите команду Добавить класс.</span><span class="sxs-lookup"><span data-stu-id="2a96f-120">Right click the Models folder and select Add Class.</span></span> <span data-ttu-id="2a96f-121">Присвойте классу имя Movie и нажмите кнопку ОК.</span><span class="sxs-lookup"><span data-stu-id="2a96f-121">Name your class Movie and Click the OK button.</span></span> <span data-ttu-id="2a96f-122">Вот как выглядит наш частичный класс Movie.</span><span class="sxs-lookup"><span data-stu-id="2a96f-122">Here's what our partial Movie class looks like.</span></span>

[!code-csharp[Main](getting-started-with-mvc-part7/samples/sample1.cs)]

<span data-ttu-id="2a96f-123">Повторно запустите приложение и попробуйте ввести фильм с ценой свыше 100.</span><span class="sxs-lookup"><span data-stu-id="2a96f-123">Re-Run your application and try to enter a movie with a price over 100.</span></span> <span data-ttu-id="2a96f-124">После отправки формы вы получите сообщение об ошибке.</span><span class="sxs-lookup"><span data-stu-id="2a96f-124">You'll get an error after you've submitted the form.</span></span> <span data-ttu-id="2a96f-125">Ошибка перехватывается на стороне сервера и возникает после отправки формы.</span><span class="sxs-lookup"><span data-stu-id="2a96f-125">The error is caught on the server side and occurs after the Form is POSTed.</span></span> <span data-ttu-id="2a96f-126">Обратите внимание, что встроенные вспомогательные методы HTML ASP.NET MVC были достаточно интеллектуальными для отображения сообщения об ошибке и сохранения значений для нас в элементах TextBox:</span><span class="sxs-lookup"><span data-stu-id="2a96f-126">Notice how ASP.NET MVC's built-in HTML helpers were smart enough to display the error message and maintain the values for us within the textbox elements:</span></span>

<span data-ttu-id="2a96f-127">[![Креатемовиевисвалидатион](getting-started-with-mvc-part7/_static/image2.png)](getting-started-with-mvc-part7/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="2a96f-127">[![CreateMovieWithValidation](getting-started-with-mvc-part7/_static/image2.png)](getting-started-with-mvc-part7/_static/image1.png)</span></span>

<span data-ttu-id="2a96f-128">Это прекрасно работает, но было бы неплохо, если бы мы могли сообщить пользователю на стороне клиента, прежде чем сервер будет вовлечен в работу.</span><span class="sxs-lookup"><span data-stu-id="2a96f-128">This works great, but it'd be nice if we could tell the user on the client-side, immediately, before the server gets involved.</span></span>

<span data-ttu-id="2a96f-129">Давайте разберем некоторую проверку на стороне клиента с помощью JavaScript.</span><span class="sxs-lookup"><span data-stu-id="2a96f-129">Let's enable some client-side validation with JavaScript.</span></span>

## <a name="adding-client-side-validation"></a><span data-ttu-id="2a96f-130">Добавление клиентской проверки</span><span class="sxs-lookup"><span data-stu-id="2a96f-130">Adding Client-Side Validation</span></span>

<span data-ttu-id="2a96f-131">Так как у нашего класса Movie уже есть некоторые атрибуты проверки, нам нужно просто добавить несколько файлов JavaScript в шаблон представления Create. aspx и добавить строку кода, чтобы включить проверку на стороне клиента.</span><span class="sxs-lookup"><span data-stu-id="2a96f-131">Since our Movie class already has some validation attributes, we'll just need to add a few JavaScript files to our Create.aspx View template and add a line of code to enable client-side validation to take place.</span></span>

<span data-ttu-id="2a96f-132">В VWD перейдите к нашей папке Views/Movie и откройте файл create. aspx.</span><span class="sxs-lookup"><span data-stu-id="2a96f-132">From within VWD go our Views/Movie folder and open up Create.aspx.</span></span>

<span data-ttu-id="2a96f-133">Откройте папку Scripts в обозреватель решений и перетащите следующие три скрипта в тег &lt;Head&gt;.</span><span class="sxs-lookup"><span data-stu-id="2a96f-133">Open up the Scripts folder in the Solution Explorer and drag the following three scripts to within the &lt;head&gt; tag.</span></span>

- <span data-ttu-id="2a96f-134">MicrosoftAjax. js</span><span class="sxs-lookup"><span data-stu-id="2a96f-134">MicrosoftAjax.js</span></span>
- <span data-ttu-id="2a96f-135">Микрософтмвквалидатион. js</span><span class="sxs-lookup"><span data-stu-id="2a96f-135">MicrosoftMvcValidation.js</span></span>

<span data-ttu-id="2a96f-136">Необходимо, чтобы эти файлы сценариев отображались в указанном порядке.</span><span class="sxs-lookup"><span data-stu-id="2a96f-136">You want these script files to appear in this order.</span></span>

[!code-html[Main](getting-started-with-mvc-part7/samples/sample2.html)]

<span data-ttu-id="2a96f-137">Кроме того, добавьте эту одну строку над HTML. Бегинформ:</span><span class="sxs-lookup"><span data-stu-id="2a96f-137">Also, add this single line above the Html.BeginForm:</span></span>

[!code-aspx[Main](getting-started-with-mvc-part7/samples/sample3.aspx)]

<span data-ttu-id="2a96f-138">Ниже приведен код, показанный в интегрированной среде разработки.</span><span class="sxs-lookup"><span data-stu-id="2a96f-138">Here's the code shown within the IDE.</span></span>

<span data-ttu-id="2a96f-139">[![фильмов — Microsoft Visual Web Developer 2010 Express (10)](getting-started-with-mvc-part7/_static/image4.png)](getting-started-with-mvc-part7/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="2a96f-139">[![Movies - Microsoft Visual Web Developer 2010 Express (10)](getting-started-with-mvc-part7/_static/image4.png)](getting-started-with-mvc-part7/_static/image3.png)</span></span>

<span data-ttu-id="2a96f-140">Запустите приложение и снова перейдите в/Мовиес/креате, а затем щелкните Создать без ввода каких бы то ни было данных.</span><span class="sxs-lookup"><span data-stu-id="2a96f-140">Run your application and visit /Movies/Create again, and click Create without entering any data.</span></span> <span data-ttu-id="2a96f-141">Сообщения об ошибках отображаются немедленно без страницы Flash, связанной с отправкой данных обратно на сервер.</span><span class="sxs-lookup"><span data-stu-id="2a96f-141">The error messages appear immediately without the page flash that we associate with sending data all the way back to the server.</span></span> <span data-ttu-id="2a96f-142">Это связано с тем, что ASP.NET MVC теперь проверяет входные данные как на стороне клиента (с помощью JavaScript), так и на сервере.</span><span class="sxs-lookup"><span data-stu-id="2a96f-142">This is because ASP.NET MVC is now validating the input on both the client (using JavaScript) and on the server.</span></span>

<span data-ttu-id="2a96f-143">[Создание ![Windows Internet Explorer](getting-started-with-mvc-part7/_static/image6.png)](getting-started-with-mvc-part7/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="2a96f-143">[![Create - Windows Internet Explorer](getting-started-with-mvc-part7/_static/image6.png)](getting-started-with-mvc-part7/_static/image5.png)</span></span>

<span data-ttu-id="2a96f-144">Это хорошо.</span><span class="sxs-lookup"><span data-stu-id="2a96f-144">This is looking good!</span></span> <span data-ttu-id="2a96f-145">Теперь добавим в базу данных один дополнительный столбец.</span><span class="sxs-lookup"><span data-stu-id="2a96f-145">Let's now add one additional column to the database.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="2a96f-146">[Назад](getting-started-with-mvc-part6.md)
> [Вперед](getting-started-with-mvc-part8.md)</span><span class="sxs-lookup"><span data-stu-id="2a96f-146">[Previous](getting-started-with-mvc-part6.md)
[Next](getting-started-with-mvc-part8.md)</span></span>
