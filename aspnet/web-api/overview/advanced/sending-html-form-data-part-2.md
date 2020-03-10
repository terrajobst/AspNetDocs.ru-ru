---
uid: web-api/overview/advanced/sending-html-form-data-part-2
title: 'Отправка данных HTML-формы в веб-API ASP.NET: Отправка файлов и многокомпонентный MIME-ASP.NET 4. x'
author: MikeWasson
description: В этом руководстве показано, как отправлять файлы в веб-API. В нем также описывается обработка составных данных MIME.
ms.author: riande
ms.date: 06/21/2012
ms.custom: seoapril2019
ms.assetid: a7f3c1b5-69d9-4261-b082-19ffafa5f16a
msc.legacyurl: /web-api/overview/advanced/sending-html-form-data-part-2
msc.type: authoredcontent
ms.openlocfilehash: f5aaebb96f631dfb6b0da1fbca96cd93a6a7fe2d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78449214"
---
# <a name="sending-html-form-data-in-aspnet-web-api-file-upload-and-multipart-mime"></a><span data-ttu-id="95a85-104">Отправка данных HTML-формы в веб-API ASP.NET: Отправка файлов и многокомпонентный MIME</span><span class="sxs-lookup"><span data-stu-id="95a85-104">Sending HTML Form Data in ASP.NET Web API: File Upload and Multipart MIME</span></span>

<span data-ttu-id="95a85-105">по [Майк Уоссон](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="95a85-105">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

## <a name="part-2-file-upload-and-multipart-mime"></a><span data-ttu-id="95a85-106">Часть 2. Передача файлов и составной MIME</span><span class="sxs-lookup"><span data-stu-id="95a85-106">Part 2: File Upload and Multipart MIME</span></span>

<span data-ttu-id="95a85-107">В этом руководстве показано, как отправлять файлы в веб-API.</span><span class="sxs-lookup"><span data-stu-id="95a85-107">This tutorial shows how to upload files to a web API.</span></span> <span data-ttu-id="95a85-108">В нем также описывается обработка составных данных MIME.</span><span class="sxs-lookup"><span data-stu-id="95a85-108">It also describes how to process multipart MIME data.</span></span>

> [!NOTE]
> <span data-ttu-id="95a85-109">[Скачайте завершенный проект](https://code.msdn.microsoft.com/ASPNET-Web-API-File-Upload-a8c0fb0d).</span><span class="sxs-lookup"><span data-stu-id="95a85-109">[Download the completed project](https://code.msdn.microsoft.com/ASPNET-Web-API-File-Upload-a8c0fb0d).</span></span>

<span data-ttu-id="95a85-110">Ниже приведен пример HTML-формы для отправки файла.</span><span class="sxs-lookup"><span data-stu-id="95a85-110">Here is an example of an HTML form for uploading a file:</span></span>

[!code-html[Main](sending-html-form-data-part-2/samples/sample1.html)]

![](sending-html-form-data-part-2/_static/image1.png)

<span data-ttu-id="95a85-111">Эта форма содержит элемент управления вводом текста и элемент управления вводом файла.</span><span class="sxs-lookup"><span data-stu-id="95a85-111">This form contains a text input control and a file input control.</span></span> <span data-ttu-id="95a85-112">Если форма содержит элемент управления вводом файла, атрибут **енктипе** всегда должен быть &quot;составной&quot;многоэлементных данных/форм, который указывает, что форма будет отправлена как многокомпонентное сообщение MIME.</span><span class="sxs-lookup"><span data-stu-id="95a85-112">When a form contains a file input control, the **enctype** attribute should always be &quot;multipart/form-data&quot;, which specifies that the form will be sent as a multipart MIME message.</span></span>

<span data-ttu-id="95a85-113">Формат многокомпонентного сообщения MIME проще понять, взглянув на пример запроса:</span><span class="sxs-lookup"><span data-stu-id="95a85-113">The format of a multipart MIME message is easiest to understand by looking at an example request:</span></span>

[!code-console[Main](sending-html-form-data-part-2/samples/sample2.cmd)]

<span data-ttu-id="95a85-114">Это сообщение разделено на две *части*— по одному для каждого элемента управления формы.</span><span class="sxs-lookup"><span data-stu-id="95a85-114">This message is divided into two *parts*, one for each form control.</span></span> <span data-ttu-id="95a85-115">Границы части обозначаются линиями, начинающимися с тире.</span><span class="sxs-lookup"><span data-stu-id="95a85-115">Part boundaries are indicated by the lines that start with dashes.</span></span>

> [!NOTE]
> <span data-ttu-id="95a85-116">Граница части включает в себя случайный компонент (&quot;41184676334&quot;), чтобы предотвратить случайное отображение строки границы внутри части сообщения.</span><span class="sxs-lookup"><span data-stu-id="95a85-116">The part boundary includes a random component (&quot;41184676334&quot;) to ensure that the boundary string does not accidentally appear inside a message part.</span></span>

<span data-ttu-id="95a85-117">Каждая часть сообщения содержит один или несколько заголовков, за которыми следует содержимое части.</span><span class="sxs-lookup"><span data-stu-id="95a85-117">Each message part contains one or more headers, followed by the part contents.</span></span>

- <span data-ttu-id="95a85-118">Заголовок Content-Disposition содержит имя элемента управления.</span><span class="sxs-lookup"><span data-stu-id="95a85-118">The Content-Disposition header includes the name of the control.</span></span> <span data-ttu-id="95a85-119">Для файлов также содержит имя файла.</span><span class="sxs-lookup"><span data-stu-id="95a85-119">For files, it also contains the file name.</span></span>
- <span data-ttu-id="95a85-120">Заголовок Content-Type описывает данные в части.</span><span class="sxs-lookup"><span data-stu-id="95a85-120">The Content-Type header describes the data in the part.</span></span> <span data-ttu-id="95a85-121">Если этот заголовок опущен, по умолчанию используется text/plain.</span><span class="sxs-lookup"><span data-stu-id="95a85-121">If this header is omitted, the default is text/plain.</span></span>

<span data-ttu-id="95a85-122">В предыдущем примере пользователь передал файл с именем Грандканйон. jpg с типом содержимого image/jpeg; а значение текстового ввода было &quot;лето&quot;.</span><span class="sxs-lookup"><span data-stu-id="95a85-122">In the previous example, the user uploaded a file named GrandCanyon.jpg, with content type image/jpeg; and the value of the text input was &quot;Summer Vacation&quot;.</span></span>

## <a name="file-upload"></a><span data-ttu-id="95a85-123">Передача файла</span><span class="sxs-lookup"><span data-stu-id="95a85-123">File Upload</span></span>

<span data-ttu-id="95a85-124">Теперь давайте взглянем на контроллер веб-API, который считывает файлы из составного сообщения MIME.</span><span class="sxs-lookup"><span data-stu-id="95a85-124">Now let's look at a Web API controller that reads files from a multipart MIME message.</span></span> <span data-ttu-id="95a85-125">Контроллер будет считывать файлы в асинхронном режиме.</span><span class="sxs-lookup"><span data-stu-id="95a85-125">The controller will read the files asynchronously.</span></span> <span data-ttu-id="95a85-126">Веб-API поддерживает асинхронные действия с помощью [модели программирования на основе задач](https://msdn.microsoft.com/library/dd460693.aspx).</span><span class="sxs-lookup"><span data-stu-id="95a85-126">Web API supports asynchronous actions using the [task-based programming model](https://msdn.microsoft.com/library/dd460693.aspx).</span></span> <span data-ttu-id="95a85-127">Во-первых, вот код, если вы нацелены на .NET Framework 4,5, поддерживающие ключевые слова **Async** и **await** .</span><span class="sxs-lookup"><span data-stu-id="95a85-127">First, here is the code if you are targeting .NET Framework 4.5, which supports the **async** and **await** keywords.</span></span>

[!code-csharp[Main](sending-html-form-data-part-2/samples/sample3.cs)]

<span data-ttu-id="95a85-128">Обратите внимание, что действие контроллера не принимает никаких параметров.</span><span class="sxs-lookup"><span data-stu-id="95a85-128">Notice that the controller action does not take any parameters.</span></span> <span data-ttu-id="95a85-129">Это связано с тем, что мы обрабатываем текст запроса внутри действия без вызова модуля форматирования типа мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="95a85-129">That's because we process the request body inside the action, without invoking a media-type formatter.</span></span>

<span data-ttu-id="95a85-130">Метод **исмултипартконтент** проверяет, содержит ли запрос составной MIME-сообщение.</span><span class="sxs-lookup"><span data-stu-id="95a85-130">The **IsMultipartContent** method checks whether the request contains a multipart MIME message.</span></span> <span data-ttu-id="95a85-131">В противном случае контроллер возвращает код состояния HTTP 415 (неподдерживаемый тип носителя).</span><span class="sxs-lookup"><span data-stu-id="95a85-131">If not, the controller returns HTTP status code 415 (Unsupported Media Type).</span></span>

<span data-ttu-id="95a85-132">Класс **мултипартформдатастреампровидер** — это вспомогательный объект, который выделяет потоковые файлы для отправленных файлов.</span><span class="sxs-lookup"><span data-stu-id="95a85-132">The **MultipartFormDataStreamProvider** class is a helper object that allocates file streams for uploaded files.</span></span> <span data-ttu-id="95a85-133">Для чтения составного сообщения MIME вызовите метод **реадасмултипартасинк** .</span><span class="sxs-lookup"><span data-stu-id="95a85-133">To read the multipart MIME message, call the **ReadAsMultipartAsync** method.</span></span> <span data-ttu-id="95a85-134">Этот метод извлекает все части сообщения и записывает их в потоки, предоставляемые **мултипартформдатастреампровидер**.</span><span class="sxs-lookup"><span data-stu-id="95a85-134">This method extracts all of the message parts and writes them into the streams provided by the **MultipartFormDataStreamProvider**.</span></span>

<span data-ttu-id="95a85-135">По завершении выполнения метода можно получить сведения о файлах из свойства **филедата** , которое представляет собой коллекцию объектов **мултипартфиледата** .</span><span class="sxs-lookup"><span data-stu-id="95a85-135">When the method completes, you can get information about the files from the **FileData** property, which is a collection of **MultipartFileData** objects.</span></span>

- <span data-ttu-id="95a85-136">**Мултипартфиледата. filename** — это локальное имя файла на сервере, где был сохранен файл.</span><span class="sxs-lookup"><span data-stu-id="95a85-136">**MultipartFileData.FileName** is the local file name on the server, where the file was saved.</span></span>
- <span data-ttu-id="95a85-137">**Мултипартфиледата. Headers** содержит заголовок части (а*не* заголовок запроса).</span><span class="sxs-lookup"><span data-stu-id="95a85-137">**MultipartFileData.Headers** contains the part header (*not* the request header).</span></span> <span data-ttu-id="95a85-138">Его можно использовать для доступа к содержимому\_расположения и заголовкам Content-Type.</span><span class="sxs-lookup"><span data-stu-id="95a85-138">You can use this to access the Content\_Disposition and Content-Type headers.</span></span>

<span data-ttu-id="95a85-139">Как видно из названия, **реадасмултипартасинк** является асинхронным методом.</span><span class="sxs-lookup"><span data-stu-id="95a85-139">As the name suggests, **ReadAsMultipartAsync** is an asynchronous method.</span></span> <span data-ttu-id="95a85-140">Чтобы выполнить работу после завершения метода, используйте [задачу продолжения](https://msdn.microsoft.com/library/ee372288.aspx) (.NET 4,0) или ключевое слово **await** (.NET 4,5).</span><span class="sxs-lookup"><span data-stu-id="95a85-140">To perform work after the method completes, use a [continuation task](https://msdn.microsoft.com/library/ee372288.aspx) (.NET 4.0) or the **await** keyword (.NET 4.5).</span></span>

<span data-ttu-id="95a85-141">Ниже приведена версия .NET Framework 4,0 с предыдущим кодом:</span><span class="sxs-lookup"><span data-stu-id="95a85-141">Here is the .NET Framework 4.0 version of the previous code:</span></span>

[!code-csharp[Main](sending-html-form-data-part-2/samples/sample4.cs)]

## <a name="reading-form-control-data"></a><span data-ttu-id="95a85-142">Чтение данных элемента управления формы</span><span class="sxs-lookup"><span data-stu-id="95a85-142">Reading Form Control Data</span></span>

<span data-ttu-id="95a85-143">HTML-форма, которую я показал ранее, имел элемент управления Text input.</span><span class="sxs-lookup"><span data-stu-id="95a85-143">The HTML form that I showed earlier had a text input control.</span></span>

[!code-html[Main](sending-html-form-data-part-2/samples/sample5.html)]

<span data-ttu-id="95a85-144">Значение элемента управления можно получить из свойства **формдата** объекта **мултипартформдатастреампровидер**.</span><span class="sxs-lookup"><span data-stu-id="95a85-144">You can get the value of the control from the **FormData** property of the **MultipartFormDataStreamProvider**.</span></span>

[!code-csharp[Main](sending-html-form-data-part-2/samples/sample6.cs?highlight=15)]

<span data-ttu-id="95a85-145">**Формдата** — это **NameValueCollection** , содержащий пары "имя-значение" для элементов управления формы.</span><span class="sxs-lookup"><span data-stu-id="95a85-145">**FormData** is a **NameValueCollection** that contains name/value pairs for the form controls.</span></span> <span data-ttu-id="95a85-146">Коллекция может содержать дублирующиеся ключи.</span><span class="sxs-lookup"><span data-stu-id="95a85-146">The collection can contain duplicate keys.</span></span> <span data-ttu-id="95a85-147">Рассмотрим следующую форму:</span><span class="sxs-lookup"><span data-stu-id="95a85-147">Consider this form:</span></span>

[!code-html[Main](sending-html-form-data-part-2/samples/sample7.html)]

![](sending-html-form-data-part-2/_static/image2.png)

<span data-ttu-id="95a85-148">Текст запроса может выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="95a85-148">The request body might look like this:</span></span>

[!code-console[Main](sending-html-form-data-part-2/samples/sample8.cmd)]

<span data-ttu-id="95a85-149">В этом случае коллекция **формдата** будет содержать следующие пары "ключ-значение":</span><span class="sxs-lookup"><span data-stu-id="95a85-149">In that case, the **FormData** collection would contain the following key/value pairs:</span></span>

- <span data-ttu-id="95a85-150">Поездка: круговой путь</span><span class="sxs-lookup"><span data-stu-id="95a85-150">trip: round-trip</span></span>
- <span data-ttu-id="95a85-151">параметры: не останавливаться</span><span class="sxs-lookup"><span data-stu-id="95a85-151">options: nonstop</span></span>
- <span data-ttu-id="95a85-152">параметры: даты</span><span class="sxs-lookup"><span data-stu-id="95a85-152">options: dates</span></span>
- <span data-ttu-id="95a85-153">рабочее место: окно</span><span class="sxs-lookup"><span data-stu-id="95a85-153">seat: window</span></span>
