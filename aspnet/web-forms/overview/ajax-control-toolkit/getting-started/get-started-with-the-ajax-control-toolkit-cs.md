---
uid: web-forms/overview/ajax-control-toolkit/getting-started/get-started-with-the-ajax-control-toolkit-cs
title: Начало работы с набором средств AJAX ControlC#Toolkit () | Документация Майкрософт
author: microsoft
description: Изучите все, что нужно знать, чтобы приступить к работе с набором средств AJAX Control Toolkit.
ms.author: riande
ms.date: 05/12/2009
ms.assetid: 16dc5c11-65be-4eae-a818-9fad7f8259c6
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/getting-started/get-started-with-the-ajax-control-toolkit-cs
msc.type: authoredcontent
ms.openlocfilehash: 7478b090ec52778572d70065983de6be8bdb4e6b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78504090"
---
# <a name="get-started-with-the-ajax-control-toolkit-c"></a><span data-ttu-id="28db3-103">Начало работы с набором элементов управления AJAX (C#)</span><span class="sxs-lookup"><span data-stu-id="28db3-103">Get Started with the AJAX Control Toolkit (C#)</span></span>

<span data-ttu-id="28db3-104">по [Майкрософт](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="28db3-104">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="28db3-105">Изучите все, что нужно знать, чтобы приступить к работе с набором средств AJAX Control Toolkit.</span><span class="sxs-lookup"><span data-stu-id="28db3-105">Learn all you need to know to get started using the AJAX Control Toolkit.</span></span>

<span data-ttu-id="28db3-106">AJAX Control Toolkit содержит более 30 бесплатных элементов управления, которые можно использовать в приложениях ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="28db3-106">The AJAX Control Toolkit contains more than 30 free controls that you can use in your ASP.NET applications.</span></span> <span data-ttu-id="28db3-107">В этом руководстве вы узнаете, как загрузить набор средств AJAX Control Toolkit и добавить элементы управления набора средств в панель элементов Visual Studio или Visual Web Developer Express.</span><span class="sxs-lookup"><span data-stu-id="28db3-107">In this tutorial, you learn how to download the AJAX Control Toolkit and add the toolkit controls to your Visual Studio/Visual Web Developer Express toolbox.</span></span>

## <a name="downloading-the-ajax-control-toolkit"></a><span data-ttu-id="28db3-108">Загрузка набора средств AJAX Control Toolkit</span><span class="sxs-lookup"><span data-stu-id="28db3-108">Downloading the AJAX Control Toolkit</span></span>

<span data-ttu-id="28db3-109">[AJAX Control Toolkit](http://devexpress.com/act) — это проект с открытым исходным кодом, разработанный членами сообщества ASP.NET и группой ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="28db3-109">The [AJAX Control Toolkit](http://devexpress.com/act) is an open source project developed by the members of the ASP.NET community and the ASP.NET team.</span></span> 

<span data-ttu-id="28db3-110">[![Загрузка набора средств AJAX Control Toolkit](get-started-with-the-ajax-control-toolkit-cs/_static/image1.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="28db3-110">[![Downloading the AJAX Control Toolkit](get-started-with-the-ajax-control-toolkit-cs/_static/image1.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image1.png)</span></span>

<span data-ttu-id="28db3-111">**Рис. 01**. Загрузка набора средств AJAX Control Toolkit ([щелкните, чтобы просмотреть изображение с полным размером](get-started-with-the-ajax-control-toolkit-cs/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="28db3-111">**Figure 01**: Downloading the AJAX Control Toolkit([Click to view full-size image](get-started-with-the-ajax-control-toolkit-cs/_static/image2.png))</span></span>

<span data-ttu-id="28db3-112">После загрузки файла необходимо разблокировать файл.</span><span class="sxs-lookup"><span data-stu-id="28db3-112">After you download the file, you need to unblock the file.</span></span> <span data-ttu-id="28db3-113">Щелкните правой кнопкой мыши файл, выберите пункт Свойства и нажмите кнопку **разблокировать** (см. рис. 2).</span><span class="sxs-lookup"><span data-stu-id="28db3-113">Right-click the file, select Properties, and click the **Unblock** button (see Figure 2).</span></span>

<span data-ttu-id="28db3-114">[![разблокировки ZIP-файла набора средств AJAX Control Toolkit](get-started-with-the-ajax-control-toolkit-cs/_static/image2.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="28db3-114">[![Unblocking the AJAX Control Toolkit ZIP file](get-started-with-the-ajax-control-toolkit-cs/_static/image2.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image3.png)</span></span>

<span data-ttu-id="28db3-115">**Рис. 02**. Разблокирование ZIP-файла набора средств AJAX Control Toolkit ([щелкните, чтобы просмотреть изображение с полным размером](get-started-with-the-ajax-control-toolkit-cs/_static/image4.png))</span><span class="sxs-lookup"><span data-stu-id="28db3-115">**Figure 02**: Unblocking the AJAX Control Toolkit ZIP file([Click to view full-size image](get-started-with-the-ajax-control-toolkit-cs/_static/image4.png))</span></span>

<span data-ttu-id="28db3-116">После разблокировки файла можно распаковать его: щелкните файл правой кнопкой мыши и выберите пункт **извлечь все** .</span><span class="sxs-lookup"><span data-stu-id="28db3-116">After you unblock the file, you can unzip the file: Right-click the file and select the **Extract All** menu option.</span></span> <span data-ttu-id="28db3-117">Теперь мы готовы к добавлению набора средств в область элементов Visual Studio/Visual Web Developer.</span><span class="sxs-lookup"><span data-stu-id="28db3-117">Now, we are ready to add the toolkit to the Visual Studio/Visual Web Developer toolbox.</span></span>

## <a name="adding-the-ajax-control-toolkit-to-the-toolbox"></a><span data-ttu-id="28db3-118">Добавление набора средств AJAX Control Toolkit на панель элементов</span><span class="sxs-lookup"><span data-stu-id="28db3-118">Adding the AJAX Control Toolkit to the Toolbox</span></span>

<span data-ttu-id="28db3-119">Самый простой способ использовать AJAX Control Toolkit — добавить набор средств в панель элементов Visual Studio или Visual Web Developer (см. рис. 3).</span><span class="sxs-lookup"><span data-stu-id="28db3-119">The easiest way to use the AJAX Control Toolkit is to add the toolkit to your Visual Studio/Visual Web Developer toolbox (see Figure 3).</span></span> <span data-ttu-id="28db3-120">Таким образом, вы можете просто перетащить элемент управления набором средств на страницу, когда хотите его использовать.</span><span class="sxs-lookup"><span data-stu-id="28db3-120">That way, you can simply drag a toolkit control onto a page when you want to use it.</span></span>

<span data-ttu-id="28db3-121">[в панели элементов отображается ![AJAX Control Toolkit](get-started-with-the-ajax-control-toolkit-cs/_static/image3.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="28db3-121">[![AJAX Control Toolkit appears in toolbox](get-started-with-the-ajax-control-toolkit-cs/_static/image3.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image5.png)</span></span>

<span data-ttu-id="28db3-122">**Рис. 03**. набор средств управления AJAX отображается в области элементов ([щелкните, чтобы просмотреть изображение с полным размером](get-started-with-the-ajax-control-toolkit-cs/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="28db3-122">**Figure 03**: AJAX Control Toolkit appears in toolbox([Click to view full-size image](get-started-with-the-ajax-control-toolkit-cs/_static/image6.png))</span></span>

<span data-ttu-id="28db3-123">Сначала необходимо добавить вкладку AJAX Control Toolkit на панель элементов.</span><span class="sxs-lookup"><span data-stu-id="28db3-123">First, you need to add an AJAX Control Toolkit tab to the toolbox.</span></span> <span data-ttu-id="28db3-124">Выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="28db3-124">Follow these steps.</span></span>

1. <span data-ttu-id="28db3-125">Создайте веб-сайт ASP.NET, выбрав файл параметров меню, новый веб-сайт.</span><span class="sxs-lookup"><span data-stu-id="28db3-125">Create a new ASP.NET Website by selecting the menu option File, New Website.</span></span> <span data-ttu-id="28db3-126">Дважды щелкните Default. aspx в окне обозреватель решений, чтобы открыть файл в редакторе.</span><span class="sxs-lookup"><span data-stu-id="28db3-126">Double-click the Default.aspx in the Solution Explorer window to open the file in the editor.</span></span>
2. <span data-ttu-id="28db3-127">Щелкните правой кнопкой мыши панель элементов, расположенную под вкладкой Общие, и выберите пункт меню **Добавить вкладку** (см. рис. 4).</span><span class="sxs-lookup"><span data-stu-id="28db3-127">Right-click the Toolbox beneath the General Tab and select the menu option **Add Tab** (see Figure 4).</span></span>
3. <span data-ttu-id="28db3-128">Введите новую вкладку с именем набор средств управления AJAX.</span><span class="sxs-lookup"><span data-stu-id="28db3-128">Enter a new tab named AJAX Control Toolkit.</span></span>

<span data-ttu-id="28db3-129">[![Добавление новой вкладки](get-started-with-the-ajax-control-toolkit-cs/_static/image4.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="28db3-129">[![Adding a new tab](get-started-with-the-ajax-control-toolkit-cs/_static/image4.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image7.png)</span></span>

<span data-ttu-id="28db3-130">**Рис. 04**. Добавление новой вкладки ([щелкните, чтобы просмотреть изображение с полным размером](get-started-with-the-ajax-control-toolkit-cs/_static/image8.png))</span><span class="sxs-lookup"><span data-stu-id="28db3-130">**Figure 04**: Adding a new tab([Click to view full-size image](get-started-with-the-ajax-control-toolkit-cs/_static/image8.png))</span></span>

<span data-ttu-id="28db3-131">Далее необходимо добавить элементы управления AJAX Control Toolkit на новую вкладку. выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="28db3-131">Next, you need to add the AJAX Control Toolkit controls to the new tab. Follow these steps:</span></span>

- <span data-ttu-id="28db3-132">Щелкните правой кнопкой мыши под вкладкой AJAX Control Toolkit и выберите пункт меню **элементы (см. рис. 5)** .</span><span class="sxs-lookup"><span data-stu-id="28db3-132">Right-click beneath the AJAX Control Toolkit tab and select the menu option **Choose Items (see Figure 5)**.</span></span>
- <span data-ttu-id="28db3-133">Перейдите к расположению, в котором был распакован набор элементов управления AJAX, и выберите сборку Ажаксконтролтулкит. dll.</span><span class="sxs-lookup"><span data-stu-id="28db3-133">Browse to the location where you unzipped the AJAX Control Toolkit and select the AjaxControlToolkit.dll assembly.</span></span>

<span data-ttu-id="28db3-134">[![выбрать элементы для добавления в панель элементов](get-started-with-the-ajax-control-toolkit-cs/_static/image5.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="28db3-134">[![Choose items to add to the toolbox](get-started-with-the-ajax-control-toolkit-cs/_static/image5.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image9.png)</span></span>

<span data-ttu-id="28db3-135">**Рис. 05**. Выбор элементов для добавления на панель элементов ([щелкните, чтобы просмотреть изображение с полным размером](get-started-with-the-ajax-control-toolkit-cs/_static/image10.png))</span><span class="sxs-lookup"><span data-stu-id="28db3-135">**Figure 05**: Choose items to add to the toolbox([Click to view full-size image](get-started-with-the-ajax-control-toolkit-cs/_static/image10.png))</span></span>

<span data-ttu-id="28db3-136">После выполнения этих действий все элементы управления набора инструментов будут отображаться на панели элементов.</span><span class="sxs-lookup"><span data-stu-id="28db3-136">After you complete these steps, all of the toolkit controls will appear in your toolbox.</span></span>

## <a name="upgrading-to-a-new-version-of-the-toolkit"></a><span data-ttu-id="28db3-137">Обновление до новой версии набора средств</span><span class="sxs-lookup"><span data-stu-id="28db3-137">Upgrading to a New Version of the Toolkit</span></span>

<span data-ttu-id="28db3-138">Если вы использовали более старую версию набора средств и теперь вам нужно перейти к более поздней версии, рекомендуем выполнить следующие действия.</span><span class="sxs-lookup"><span data-stu-id="28db3-138">If you were using an older release of the Toolkit and now need to move to a later version here are the recommended steps:</span></span>

- <span data-ttu-id="28db3-139">Двоичные файлы. Удалите старую версию сборки Ажаксконтролтулкит. dll из папки Bin веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="28db3-139">Binaries - Delete the old version of the AjaxControlToolkit.dll assembly from your website Bin folder.</span></span>
- <span data-ttu-id="28db3-140">Элементы панели элементов — Удалите вкладку AJAX Control Toolkit и выполните описанные выше действия, чтобы повторно создать вкладку с новой версией сборки Ажаксконтролтулкит. dll.</span><span class="sxs-lookup"><span data-stu-id="28db3-140">Toolbox Items - Delete the AJAX Control Toolkit tab and follow the steps above to re-create the tab with the new version of the AjaxControlToolkit.dll assembly.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="28db3-141">Дальше</span><span class="sxs-lookup"><span data-stu-id="28db3-141">Next</span></span>](using-ajax-control-toolkit-controls-and-control-extenders-cs.md)
