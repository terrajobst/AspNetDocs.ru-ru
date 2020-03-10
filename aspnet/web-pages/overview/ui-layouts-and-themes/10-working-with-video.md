---
uid: web-pages/overview/ui-layouts-and-themes/10-working-with-video
title: Отображение видео на сайте веб-страницы ASP.NET (Razor) | Документация Майкрософт
author: Rick-Anderson
description: В этой главе объясняется, как отобразить видео в веб-страницы ASP.NET со страницей синтаксис Razor.
ms.author: riande
ms.date: 02/20/2014
ms.assetid: 332fb3da-e2a5-460d-bb90-dd911e1e2c95
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/10-working-with-video
msc.type: authoredcontent
ms.openlocfilehash: 516d46f38ce8910209f4207c474b0404bf012950
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78510384"
---
# <a name="displaying-video-in-an-aspnet-web-pages-razor-site"></a><span data-ttu-id="c70c5-103">Отображение видео на сайте веб-страницы ASP.NET (Razor)</span><span class="sxs-lookup"><span data-stu-id="c70c5-103">Displaying Video in an ASP.NET Web Pages (Razor) Site</span></span>

<span data-ttu-id="c70c5-104">от [Tom фитзмаккен](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="c70c5-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="c70c5-105">В этой статье объясняется, как использовать проигрыватель видео (мультимедиа) на веб-сайте веб-страницы ASP.NET (Razor), чтобы пользователи могли просматривать видео, хранящиеся на сайте.</span><span class="sxs-lookup"><span data-stu-id="c70c5-105">This article explains how to use a video (media) player in an ASP.NET Web Pages (Razor) website to let users view videos that are stored on the site.</span></span> <span data-ttu-id="c70c5-106">Веб-страницы ASP.NET с синтаксис Razor позволяет воспроизводить видео Flash ( *. SWF*), Media Player ( *. wmv*) и Silverlight (*XAP*).</span><span class="sxs-lookup"><span data-stu-id="c70c5-106">ASP.NET Web Pages with Razor syntax lets you play Flash (*.swf*), Media Player (*.wmv*), and Silverlight (*.xap*) videos.</span></span>
> 
> <span data-ttu-id="c70c5-107">Из этого руководства вы узнаете, как выполнять такие задачи:</span><span class="sxs-lookup"><span data-stu-id="c70c5-107">What you'll learn:</span></span>
> 
> - <span data-ttu-id="c70c5-108">Как выбрать видеопроигрыватель.</span><span class="sxs-lookup"><span data-stu-id="c70c5-108">How to choose a video player.</span></span>
> - <span data-ttu-id="c70c5-109">Добавление видео на веб-страницу.</span><span class="sxs-lookup"><span data-stu-id="c70c5-109">How to add video to a web page.</span></span>
> - <span data-ttu-id="c70c5-110">Настройка атрибутов проигрывателя видео.</span><span class="sxs-lookup"><span data-stu-id="c70c5-110">How to set video player attributes.</span></span>
> 
> <span data-ttu-id="c70c5-111">Ниже приведены функции ASP.NET Razor Pages, представленные в статье:</span><span class="sxs-lookup"><span data-stu-id="c70c5-111">These are the ASP.NET Razor pages features introduced in the article:</span></span>
> 
> - <span data-ttu-id="c70c5-112">Вспомогательный метод `Video`.</span><span class="sxs-lookup"><span data-stu-id="c70c5-112">The `Video` helper.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="c70c5-113">Версии программного обеспечения, используемые в этом руководстве</span><span class="sxs-lookup"><span data-stu-id="c70c5-113">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="c70c5-114">Веб-страницы ASP.NET (Razor) 2</span><span class="sxs-lookup"><span data-stu-id="c70c5-114">ASP.NET Web Pages (Razor) 2</span></span>
> - <span data-ttu-id="c70c5-115">WebMatrix 2</span><span class="sxs-lookup"><span data-stu-id="c70c5-115">WebMatrix 2</span></span>
>   
> 
> <span data-ttu-id="c70c5-116">Этот учебник также работает с WebMatrix 3.</span><span class="sxs-lookup"><span data-stu-id="c70c5-116">This tutorial also works with WebMatrix 3.</span></span>

## <a name="introduction"></a><span data-ttu-id="c70c5-117">Введение</span><span class="sxs-lookup"><span data-stu-id="c70c5-117">Introduction</span></span>

<span data-ttu-id="c70c5-118">Может потребоваться отобразить видео на сайте.</span><span class="sxs-lookup"><span data-stu-id="c70c5-118">You might want to display a video on your site.</span></span> <span data-ttu-id="c70c5-119">Одним из способов сделать это является связывание с сайтом, на котором уже есть видео, например YouTube.</span><span class="sxs-lookup"><span data-stu-id="c70c5-119">One way to do that is to link to a site that already has the video, like YouTube.</span></span> <span data-ttu-id="c70c5-120">Если вы хотите внедрить видео с этих сайтов непосредственно на собственные страницы, обычно можно получить разметку HTML с сайта и скопировать их на страницу.</span><span class="sxs-lookup"><span data-stu-id="c70c5-120">If you want to embed a video from these sites directly in your own pages, you can usually get HTML markup from the site and then copy it into your page.</span></span> <span data-ttu-id="c70c5-121">Например, в следующем примере показано, как внедрить видео YouTube:</span><span class="sxs-lookup"><span data-stu-id="c70c5-121">For example, the following example shows how to embed a YouTube video:</span></span>

[!code-html[Main](10-working-with-video/samples/sample1.html?highlight=10-14)]

<span data-ttu-id="c70c5-122">Если вы хотите воспроизвести видео, которое находится на собственном веб-сайте (а не на общедоступном сайте для совместного использования видео), вы не можете напрямую привязать его, используя внедренную разметку, подобную этой.</span><span class="sxs-lookup"><span data-stu-id="c70c5-122">If you want to play a video that's on your own website (not on a public video-sharing site), you can't directly link to it using embedded markup like this.</span></span> <span data-ttu-id="c70c5-123">Однако можно воспроизводить видео с сайта с помощью вспомогательного метода `Video`, который отображает проигрыватель мультимедиа непосредственно на странице.</span><span class="sxs-lookup"><span data-stu-id="c70c5-123">However, you can play videos from your site by using the `Video` helper, which renders a media player directly in a page.</span></span>

<a id="Choosing_a_Video_Player"></a>
## <a name="choosing-a-video-player"></a><span data-ttu-id="c70c5-124">Выбор видеопроигрывателя</span><span class="sxs-lookup"><span data-stu-id="c70c5-124">Choosing a Video Player</span></span>

<span data-ttu-id="c70c5-125">Существует множество форматов для видеофайлов, и для каждого формата обычно требуется другой проигрыватель и другой способ настройки проигрывателя.</span><span class="sxs-lookup"><span data-stu-id="c70c5-125">There are lots of formats for video files, and each format typically requires a different player and a different way to configure the player.</span></span> <span data-ttu-id="c70c5-126">На страницах Razor ASP.NET можно воспроизвести видео на веб-странице с помощью вспомогательного метода `Video`.</span><span class="sxs-lookup"><span data-stu-id="c70c5-126">In ASP.NET Razor pages, you can play a video in a web page using the `Video` helper.</span></span> <span data-ttu-id="c70c5-127">Вспомогательный метод `Video` упрощает процесс встраивания видео на веб-страницу, так как автоматически создает `object` и `embed` HTML-элементы, которые обычно используются для добавления видео на страницу.</span><span class="sxs-lookup"><span data-stu-id="c70c5-127">The `Video` helper simplifies the process of embedding videos in a web page because it automatically generates the `object` and `embed` HTML elements that are normally used to add video to the page.</span></span>

<span data-ttu-id="c70c5-128">Вспомогательный модуль `Video` поддерживает следующие проигрыватели мультимедиа:</span><span class="sxs-lookup"><span data-stu-id="c70c5-128">The `Video` helper supports the following media players:</span></span>

- <span data-ttu-id="c70c5-129">Adobe Flash</span><span class="sxs-lookup"><span data-stu-id="c70c5-129">Adobe Flash</span></span>
- <span data-ttu-id="c70c5-130">Windows MediaPlayer</span><span class="sxs-lookup"><span data-stu-id="c70c5-130">Windows MediaPlayer</span></span>
- <span data-ttu-id="c70c5-131">Microsoft Silverlight</span><span class="sxs-lookup"><span data-stu-id="c70c5-131">Microsoft Silverlight</span></span>

### <a name="the-flash-player"></a><span data-ttu-id="c70c5-132">Проигрыватель Flash Player</span><span class="sxs-lookup"><span data-stu-id="c70c5-132">The Flash Player</span></span>

<span data-ttu-id="c70c5-133">Проигрыватель `Flash` вспомогательного приложения `Video` позволяет воспроизводить видео Flash (файлы *. SWF* ) на веб-странице.</span><span class="sxs-lookup"><span data-stu-id="c70c5-133">The `Flash` player of the `Video` helper let you play Flash videos (*.swf* files) in a web page.</span></span> <span data-ttu-id="c70c5-134">Как минимум необходимо указать путь к видеофайл.</span><span class="sxs-lookup"><span data-stu-id="c70c5-134">At a minimum, you have to provide a path to the video file.</span></span> <span data-ttu-id="c70c5-135">Если указать только путь, проигрыватель будет использовать значения по умолчанию, заданные текущей версией Flash.</span><span class="sxs-lookup"><span data-stu-id="c70c5-135">If you specify nothing but the path, the player uses default values that are set by the current version of Flash.</span></span> <span data-ttu-id="c70c5-136">Стандартные параметры по умолчанию:</span><span class="sxs-lookup"><span data-stu-id="c70c5-136">Typical default settings are:</span></span>

- <span data-ttu-id="c70c5-137">Видео отображается с использованием ширины и высоты по умолчанию и без цвета фона.</span><span class="sxs-lookup"><span data-stu-id="c70c5-137">The video is displayed using its default width and height and without a background color.</span></span>
- <span data-ttu-id="c70c5-138">Видео автоматически воспроизводится при загрузке страницы.</span><span class="sxs-lookup"><span data-stu-id="c70c5-138">The video plays automatically when the page loads.</span></span>
- <span data-ttu-id="c70c5-139">Видео циклически обрабатывается до тех пор, пока оно не будет явно остановлено.</span><span class="sxs-lookup"><span data-stu-id="c70c5-139">The video loops continuously until it's explicitly stopped.</span></span>
- <span data-ttu-id="c70c5-140">Видео масштабируется, чтобы отобразить все видео, а не обрезать видео в соответствии с конкретным размером.</span><span class="sxs-lookup"><span data-stu-id="c70c5-140">The video is scaled to show all of the video, rather than cropping the video to fit a specific size.</span></span>
- <span data-ttu-id="c70c5-141">Видео воспроизводится в окне.</span><span class="sxs-lookup"><span data-stu-id="c70c5-141">The video plays in a window.</span></span>

### <a name="the-mediaplayer-player"></a><span data-ttu-id="c70c5-142">Проигрыватель MediaPlayer</span><span class="sxs-lookup"><span data-stu-id="c70c5-142">The MediaPlayer Player</span></span>

<span data-ttu-id="c70c5-143">Проигрыватель `MediaPlayer` вспомогательного приложения `Video` позволяет воспроизводить видео Windows Media (*WMV* -файлы), Windows Media Audio (*WMA* -файлы) и MP3 (*MP3* -файлы) на странице.</span><span class="sxs-lookup"><span data-stu-id="c70c5-143">The `MediaPlayer` player of the `Video` helper lets you play Windows Media videos (*.wmv* files), Windows Media audio (*.wma* files), and MP3 (*.mp3* files) in a web page.</span></span> <span data-ttu-id="c70c5-144">Необходимо указать путь к файлу мультимедиа для воспроизведения. все остальные параметры являются необязательными.</span><span class="sxs-lookup"><span data-stu-id="c70c5-144">You must include path of the media file to play; all other parameters are optional.</span></span> <span data-ttu-id="c70c5-145">Если указать только путь, проигрыватель будет использовать параметры по умолчанию, заданные текущей версией MediaPlayer, например:</span><span class="sxs-lookup"><span data-stu-id="c70c5-145">If you specify only a path, the player uses default settings set by the current version of MediaPlayer, such as:</span></span>

- <span data-ttu-id="c70c5-146">Видео отображается с использованием ширины и высоты по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="c70c5-146">The video is displayed using its default width and height.</span></span>
- <span data-ttu-id="c70c5-147">Видео автоматически воспроизводится при загрузке страницы.</span><span class="sxs-lookup"><span data-stu-id="c70c5-147">The video plays automatically when the page loads.</span></span>
- <span data-ttu-id="c70c5-148">Видео воспроизводится один раз (он не находится в цикле).</span><span class="sxs-lookup"><span data-stu-id="c70c5-148">The video plays once (it doesn't loop).</span></span>
- <span data-ttu-id="c70c5-149">Проигрыватель отображает полный набор элементов управления в пользовательском интерфейсе.</span><span class="sxs-lookup"><span data-stu-id="c70c5-149">The player displays the full set of controls in the user interface.</span></span>
- <span data-ttu-id="c70c5-150">Видео воспроизводится в окне.</span><span class="sxs-lookup"><span data-stu-id="c70c5-150">The video plays in a window.</span></span>

### <a name="the-silverlight-player"></a><span data-ttu-id="c70c5-151">Проигрыватель Silverlight</span><span class="sxs-lookup"><span data-stu-id="c70c5-151">The Silverlight Player</span></span>

<span data-ttu-id="c70c5-152">Проигрыватель `Silverlight` вспомогательного приложения `Video` позволяет воспроизводить видео Windows Media (*WMV* -файлы), Windows Media Audio (*WMA* -файлы) и MP3 (*MP3* -файлы).</span><span class="sxs-lookup"><span data-stu-id="c70c5-152">The `Silverlight` player of the `Video` helper lets you play Windows Media Video (*.wmv* files), Windows Media Audio (*.wma* files), and MP3 (*.mp3* files).</span></span> <span data-ttu-id="c70c5-153">Необходимо задать параметр path, указывающий на пакет приложения на основе Silverlight (*XAP* -файл).</span><span class="sxs-lookup"><span data-stu-id="c70c5-153">You must set the path parameter to point to a Silverlight-based application package (*.xap* file).</span></span> <span data-ttu-id="c70c5-154">Также необходимо задать параметры Width и Height.</span><span class="sxs-lookup"><span data-stu-id="c70c5-154">You also must set the width and height parameters.</span></span> <span data-ttu-id="c70c5-155">Все остальные параметры являются необязательными.</span><span class="sxs-lookup"><span data-stu-id="c70c5-155">All other parameters are optional.</span></span> <span data-ttu-id="c70c5-156">При использовании проигрывателя Silverlight для видео, если заданы только необходимые параметры, проигрыватель Silverlight отображает видео без цвета фона.</span><span class="sxs-lookup"><span data-stu-id="c70c5-156">When you use the Silverlight player for video, if you set only the required parameters, the Silverlight player displays the video without a background color.</span></span>

> [!NOTE]
> <span data-ttu-id="c70c5-157">Если вы еще не знакомы с Silverlight: *XAP* -файл представляет собой сжатый файл, содержащий инструкции макета в *XAML* -файле, управляемый код в сборках и дополнительные ресурсы.</span><span class="sxs-lookup"><span data-stu-id="c70c5-157">In case you don't already know Silverlight: the *.xap* file is a compressed file that contains layout instructions in a *.xaml* file, managed code in assemblies, and optional resources.</span></span> <span data-ttu-id="c70c5-158">Вы можете создать *XAP* -файл в Visual Studio в качестве проекта приложения Silverlight.</span><span class="sxs-lookup"><span data-stu-id="c70c5-158">You can create a *.xap* file in Visual Studio as a Silverlight application project.</span></span>

<span data-ttu-id="c70c5-159">Проигрыватель `Silverlight` Video использует как параметры, указанные для проигрывателя, так и параметры, предоставленные в файле *. XAP* .</span><span class="sxs-lookup"><span data-stu-id="c70c5-159">The `Silverlight` video player uses both the settings that you provide for the player and the settings that are provided in the *.xap* file.</span></span>

> [!TIP] 
> 
> <a id="SB_MimeTypes"></a>
> ### <a name="mime-types"></a><span data-ttu-id="c70c5-160">Типы MIME</span><span class="sxs-lookup"><span data-stu-id="c70c5-160">MIME Types</span></span>
> 
> <span data-ttu-id="c70c5-161">Когда браузер загружает файл, браузер гарантирует, что тип файла соответствует типу MIME, указанному для отображаемого документа.</span><span class="sxs-lookup"><span data-stu-id="c70c5-161">When a browser downloads a file, the browser makes sure that the file type matches the MIME type that's specified for the document that's being rendered.</span></span> <span data-ttu-id="c70c5-162">Тип MIME — это тип содержимого или тип носителя файла.</span><span class="sxs-lookup"><span data-stu-id="c70c5-162">The MIME type is the content type or media type of a file.</span></span> <span data-ttu-id="c70c5-163">Модуль поддержки `Video` использует следующие типы MIME:</span><span class="sxs-lookup"><span data-stu-id="c70c5-163">The `Video` helper uses the following MIME types:</span></span>
> 
> - `application/x-shockwave-flash`
> - `application/x-mplayer2`
> - `application/x-silverlight-2`

<a id="Playing_Flash"></a>
## <a name="playing-flash-swf-videos"></a><span data-ttu-id="c70c5-164">Воспроизведение видео Flash (. SWF)</span><span class="sxs-lookup"><span data-stu-id="c70c5-164">Playing Flash (.swf) Videos</span></span>

<span data-ttu-id="c70c5-165">В этой процедуре показано, как воспроизвести видео с именем *Sample. SWF*в формате Flash.</span><span class="sxs-lookup"><span data-stu-id="c70c5-165">This procedure shows you how to play a Flash video named *sample.swf*.</span></span> <span data-ttu-id="c70c5-166">В процедуре предполагается, что у вас есть папка с именем *Media* на сайте, а *SWF* -файл находится в этой папке.</span><span class="sxs-lookup"><span data-stu-id="c70c5-166">The procedure assumes that you've got a folder named *Media* on your site and that the *.swf* file is in that folder.</span></span>

1. <span data-ttu-id="c70c5-167">Добавьте библиотеку вспомогательных веб-функций ASP.NET на веб-сайт, как описано в разделе [Установка вспомогательных функций на веб-страницы ASP.net сайте](https://go.microsoft.com/fwlink/?LinkId=252372), если вы еще не добавили его.</span><span class="sxs-lookup"><span data-stu-id="c70c5-167">Add the ASP.NET Web Helpers Library to your website as described in [Installing Helpers in an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=252372), if you haven't already added it.</span></span>
2. <span data-ttu-id="c70c5-168">На веб-сайте добавьте страницу и назовите ее *флашвидео. cshtml*.</span><span class="sxs-lookup"><span data-stu-id="c70c5-168">In the website, add a page and name it *FlashVideo.cshtml*.</span></span>
3. <span data-ttu-id="c70c5-169">Добавьте на страницу следующую разметку:</span><span class="sxs-lookup"><span data-stu-id="c70c5-169">Add the following markup to the page:</span></span> 

    [!code-cshtml[Main](10-working-with-video/samples/sample2.cshtml)]
4. <span data-ttu-id="c70c5-170">Запустите страницу в браузере.</span><span class="sxs-lookup"><span data-stu-id="c70c5-170">Run the page in a browser.</span></span> <span data-ttu-id="c70c5-171">(Перед выполнением страницы убедитесь, что она выбрана в рабочей области **файлы** .) Откроется страница, и видео будет воспроизводиться автоматически.</span><span class="sxs-lookup"><span data-stu-id="c70c5-171">(Make sure the page is selected in the **Files** workspace before you run it.) The page is displayed and the video plays automatically.</span></span> 

    <span data-ttu-id="c70c5-172">![Эскиз](10-working-with-video/_static/image1.jpg "ch08_video -1. jpg")</span><span class="sxs-lookup"><span data-stu-id="c70c5-172">![[image]](10-working-with-video/_static/image1.jpg "ch08_video-1.jpg")</span></span>

<span data-ttu-id="c70c5-173">Можно задать параметр `quality` для Flash-видео, чтобы `low`, `autolow`, `autohigh`, `medium`, `high`и `best`.</span><span class="sxs-lookup"><span data-stu-id="c70c5-173">You can set the `quality` parameter for a Flash video to `low`, `autolow`, `autohigh`, `medium`, `high`, and `best`:</span></span>

[!code-cshtml[Main](10-working-with-video/samples/sample3.cshtml)]

<span data-ttu-id="c70c5-174">Можно изменить видео Flash для воспроизведения с указанным размером с помощью параметра `scale`, который можно установить следующим образом:</span><span class="sxs-lookup"><span data-stu-id="c70c5-174">You can change the Flash video to play at a specific size using the `scale` parameter, which you can set to the following:</span></span>

- <span data-ttu-id="c70c5-175">`showall`.</span><span class="sxs-lookup"><span data-stu-id="c70c5-175">`showall`.</span></span> <span data-ttu-id="c70c5-176">Это делает весь видеоролик видимым при сохранении исходных пропорций.</span><span class="sxs-lookup"><span data-stu-id="c70c5-176">This makes the entire video visible while maintaining the original aspect ratio.</span></span> <span data-ttu-id="c70c5-177">Однако на каждой стороне могут пристоять границы.</span><span class="sxs-lookup"><span data-stu-id="c70c5-177">However, you might end up with borders on each side.</span></span>
- <span data-ttu-id="c70c5-178">`noorder`.</span><span class="sxs-lookup"><span data-stu-id="c70c5-178">`noorder`.</span></span> <span data-ttu-id="c70c5-179">Это позволяет масштабировать видео при сохранении исходных пропорций, но может быть обрезано.</span><span class="sxs-lookup"><span data-stu-id="c70c5-179">This scales the video while maintaining the original aspect ratio, but it might be cropped.</span></span>
- <span data-ttu-id="c70c5-180">`exactfit`.</span><span class="sxs-lookup"><span data-stu-id="c70c5-180">`exactfit`.</span></span> <span data-ttu-id="c70c5-181">Это делает видимым все видео без сохранения исходного пропорций, но может произойти искажение.</span><span class="sxs-lookup"><span data-stu-id="c70c5-181">This makes the entire video visible without preserving the original aspect ratio, but distortion may occur.</span></span>

<span data-ttu-id="c70c5-182">Если не указать параметр `scale`, будет отображаться все видео, а исходные пропорции будут сохранены без обрезки.</span><span class="sxs-lookup"><span data-stu-id="c70c5-182">If you don't specify a `scale` parameter, the entire video will be visible and the original aspect ratio will be maintained without any cropping.</span></span> <span data-ttu-id="c70c5-183">В следующем примере показано, как использовать параметр `scale`.</span><span class="sxs-lookup"><span data-stu-id="c70c5-183">The following example shows how to use the `scale` parameter:</span></span>

[!code-cshtml[Main](10-working-with-video/samples/sample4.cshtml)]

<span data-ttu-id="c70c5-184">Проигрыватель Flash Player поддерживает параметр режима видео с именем `windowMode`.</span><span class="sxs-lookup"><span data-stu-id="c70c5-184">The Flash player supports a video mode setting named `windowMode`.</span></span> <span data-ttu-id="c70c5-185">Это значение можно задать для `window`, `opaque`и `transparent`.</span><span class="sxs-lookup"><span data-stu-id="c70c5-185">You can set this to `window`, `opaque`, and `transparent`.</span></span> <span data-ttu-id="c70c5-186">По умолчанию `windowMode` имеет значение `window`, которое отображает видео в отдельном окне на веб-странице.</span><span class="sxs-lookup"><span data-stu-id="c70c5-186">By default, the `windowMode` is set to `window`, which displays the video in a separate window on the web page.</span></span> <span data-ttu-id="c70c5-187">Параметр `opaque` скрывает все содержимое экрана на веб-странице.</span><span class="sxs-lookup"><span data-stu-id="c70c5-187">The `opaque` setting hides everything behind the video on the web page.</span></span> <span data-ttu-id="c70c5-188">Параметр `transparent` позволяет отображать фон веб-страницы с помощью видео, при условии, что любая часть видео прозрачна.</span><span class="sxs-lookup"><span data-stu-id="c70c5-188">The `transparent` setting lets the background of the web page show through the video, assuming any part of the video is transparent.</span></span>

<a id="Playing_MediaPlayer"></a>
## <a name="playing-mediaplayer-wmv-videos"></a><span data-ttu-id="c70c5-189">Воспроизведение видеороликов MediaPlayer ( *. wmv*)</span><span class="sxs-lookup"><span data-stu-id="c70c5-189">Playing MediaPlayer (*.wmv*) Videos</span></span>

<span data-ttu-id="c70c5-190">В следующей процедуре показано, как воспроизвести окно Media Video с именем *Sample. wmv* , которое находится в папке *Media* .</span><span class="sxs-lookup"><span data-stu-id="c70c5-190">The following procedure shows you how to play a Window Media video named *sample.wmv* that's in the *Media* folder.</span></span>

1. <span data-ttu-id="c70c5-191">Добавьте библиотеку вспомогательных веб-функций ASP.NET на веб-сайт, как описано в разделе [Установка вспомогательных функций на веб-страницы ASP.net сайте](https://go.microsoft.com/fwlink/?LinkId=252372), если вы этого еще не сделали.</span><span class="sxs-lookup"><span data-stu-id="c70c5-191">Add the ASP.NET Web Helpers Library to your website as described in [Installing Helpers in an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=252372), if you haven't already.</span></span>
2. <span data-ttu-id="c70c5-192">Создайте новую страницу с именем *медиаплайервидео. cshtml*.</span><span class="sxs-lookup"><span data-stu-id="c70c5-192">Create a new page named *MediaPlayerVideo.cshtml*.</span></span>
3. <span data-ttu-id="c70c5-193">Добавьте на страницу следующую разметку:</span><span class="sxs-lookup"><span data-stu-id="c70c5-193">Add the following markup to the page:</span></span> 

    [!code-cshtml[Main](10-working-with-video/samples/sample5.cshtml)]
4. <span data-ttu-id="c70c5-194">Запустите страницу в браузере.</span><span class="sxs-lookup"><span data-stu-id="c70c5-194">Run the page in a browser.</span></span> <span data-ttu-id="c70c5-195">Видео загружается и воспроизводится автоматически.</span><span class="sxs-lookup"><span data-stu-id="c70c5-195">The video loads and plays automatically.</span></span> 

    <span data-ttu-id="c70c5-196">![Эскиз](10-working-with-video/_static/image2.jpg "ch08_video-2. jpg")</span><span class="sxs-lookup"><span data-stu-id="c70c5-196">![[image]](10-working-with-video/_static/image2.jpg "ch08_video-2.jpg")</span></span>

<span data-ttu-id="c70c5-197">Можно задать `playCount` целое число, которое показывает, сколько раз следует автоматически воспроизвести видео:</span><span class="sxs-lookup"><span data-stu-id="c70c5-197">You can set `playCount` to an integer that indicates how many times to play the video automatically:</span></span>

[!code-cshtml[Main](10-working-with-video/samples/sample6.cshtml)]

<span data-ttu-id="c70c5-198">Параметр `uiMode` позволяет указать, какие элементы управления отображаются в пользовательском интерфейсе.</span><span class="sxs-lookup"><span data-stu-id="c70c5-198">The `uiMode` parameter lets you specify which controls show up in the user interface.</span></span> <span data-ttu-id="c70c5-199">`uiMode` можно задать для `invisible`, `none`, `mini`или `full`.</span><span class="sxs-lookup"><span data-stu-id="c70c5-199">You can set `uiMode` to `invisible`, `none`, `mini`, or `full`.</span></span> <span data-ttu-id="c70c5-200">Если не указать параметр `uiMode`, видео будет отображаться в окне состояния, на панели поиска, на кнопках управления и в дополнение к видеоэкрану.</span><span class="sxs-lookup"><span data-stu-id="c70c5-200">If you don't specify a `uiMode` parameter, the video will be displayed with the status window, seek bar, control buttons, and volume controls in addition to the video window.</span></span> <span data-ttu-id="c70c5-201">Эти элементы управления также будут отображаться при использовании проигрывателя для воспроизведения звукового файла.</span><span class="sxs-lookup"><span data-stu-id="c70c5-201">These controls will also be displayed if you use the player to play an audio file.</span></span> <span data-ttu-id="c70c5-202">Ниже приведен пример использования параметра `uiMode`.</span><span class="sxs-lookup"><span data-stu-id="c70c5-202">Here's an example of how to use the `uiMode` parameter:</span></span>

[!code-cshtml[Main](10-working-with-video/samples/sample7.cshtml)]

<span data-ttu-id="c70c5-203">По умолчанию звук включен при воспроизведении видео.</span><span class="sxs-lookup"><span data-stu-id="c70c5-203">By default, audio is on when the video plays.</span></span> <span data-ttu-id="c70c5-204">Звук можно отключить, установив для параметра `mute` значение true:</span><span class="sxs-lookup"><span data-stu-id="c70c5-204">You can mute the audio by setting the `mute` parameter to true:</span></span>

[!code-cshtml[Main](10-working-with-video/samples/sample8.cshtml)]

<span data-ttu-id="c70c5-205">Вы можете управлять уровнем звука для видео MediaPlayer, присвоив параметру `volume` значение от 0 до 100.</span><span class="sxs-lookup"><span data-stu-id="c70c5-205">You can control the audio level of the MediaPlayer video by setting the `volume` parameter to a value between 0 and 100.</span></span> <span data-ttu-id="c70c5-206">Значение по умолчанию: 50.</span><span class="sxs-lookup"><span data-stu-id="c70c5-206">The default value is 50.</span></span> <span data-ttu-id="c70c5-207">Ниже приведен пример:</span><span class="sxs-lookup"><span data-stu-id="c70c5-207">Here's an example:</span></span>

[!code-cshtml[Main](10-working-with-video/samples/sample9.cshtml)]

<a id="Playing_Silverlight"></a>
## <a name="playing-silverlight-videos"></a><span data-ttu-id="c70c5-208">Воспроизведение видео Silverlight</span><span class="sxs-lookup"><span data-stu-id="c70c5-208">Playing Silverlight Videos</span></span>

<span data-ttu-id="c70c5-209">В этой процедуре показано, как воспроизвести видео, содержащееся на странице Silverlight *. XAP* , в папке с именем *Media*.</span><span class="sxs-lookup"><span data-stu-id="c70c5-209">This procedure shows you how to play video contained in a Silverlight *.xap* page that's in a folder named *Media*.</span></span>

1. <span data-ttu-id="c70c5-210">Добавьте библиотеку вспомогательных веб-функций ASP.NET на веб-сайт, как описано в разделе [Установка вспомогательных функций на веб-страницы ASP.net сайте](https://go.microsoft.com/fwlink/?LinkId=252372), если вы этого еще не сделали.</span><span class="sxs-lookup"><span data-stu-id="c70c5-210">Add the ASP.NET Web Helpers Library to your website as described in [Installing Helpers in an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=252372), if you haven't already .</span></span>
2. <span data-ttu-id="c70c5-211">Создайте новую страницу с именем *силверлигхтвидео. cshtml*.</span><span class="sxs-lookup"><span data-stu-id="c70c5-211">Create a new page named *SilverlightVideo.cshtml*.</span></span>
3. <span data-ttu-id="c70c5-212">Добавьте на страницу следующую разметку:</span><span class="sxs-lookup"><span data-stu-id="c70c5-212">Add the following markup to the page:</span></span> 

    [!code-cshtml[Main](10-working-with-video/samples/sample10.cshtml)]
4. <span data-ttu-id="c70c5-213">Запустите страницу в браузере.</span><span class="sxs-lookup"><span data-stu-id="c70c5-213">Run the page in a browser.</span></span> 

    <span data-ttu-id="c70c5-214">![Эскиз](10-working-with-video/_static/image3.jpg "ch08_video -3. jpg")</span><span class="sxs-lookup"><span data-stu-id="c70c5-214">![[image]](10-working-with-video/_static/image3.jpg "ch08_video-3.jpg")</span></span>

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a><span data-ttu-id="c70c5-215">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="c70c5-215">Additional Resources</span></span>

<span data-ttu-id="c70c5-216">[Обзор Silverlight](https://msdn.microsoft.com/library/bb404700(VS.95).aspx)</span><span class="sxs-lookup"><span data-stu-id="c70c5-216">[Silverlight Overview](https://msdn.microsoft.com/library/bb404700(VS.95).aspx)</span></span>

[<span data-ttu-id="c70c5-217">Атрибуты объекта Flash и тега EMBED</span><span class="sxs-lookup"><span data-stu-id="c70c5-217">Flash OBJECT and EMBED tag attributes</span></span>](http://kb2.adobe.com/cps/127/tn_12701.html)

<span data-ttu-id="c70c5-218">[Теги параметров пакета SDK для проигрывателя Windows Media 11](https://msdn.microsoft.com/library/aa392321(VS.85).aspx)</span><span class="sxs-lookup"><span data-stu-id="c70c5-218">[Windows Media Player 11 SDK PARAM Tags](https://msdn.microsoft.com/library/aa392321(VS.85).aspx)</span></span>
