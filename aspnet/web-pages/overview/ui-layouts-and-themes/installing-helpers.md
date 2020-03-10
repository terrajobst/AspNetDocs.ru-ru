---
uid: web-pages/overview/ui-layouts-and-themes/installing-helpers
title: Установка вспомогательного приложения на сайте веб-страницы ASP.NET (Razor) | Документация Майкрософт
author: Rick-Anderson
description: В этой статье описывается, как установить вспомогательную функцию на веб-сайте веб-страницы ASP.NET (Razor). Вспомогательный объект — это многократно используемый компонент, который включает в себя код и разметку для...
ms.author: riande
ms.date: 02/18/2014
ms.assetid: 5e968ead-906a-45ea-ac2a-c70e57e1a9b1
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/installing-helpers
msc.type: authoredcontent
ms.openlocfilehash: 41e33c04a53a6ad257c3937cdadcec767e9217c8
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78518646"
---
# <a name="installing-a-helper-in-an-aspnet-web-pages-razor-site"></a><span data-ttu-id="81339-104">Установка вспомогательного приложения на сайте веб-страницы ASP.NET (Razor)</span><span class="sxs-lookup"><span data-stu-id="81339-104">Installing a Helper in an ASP.NET Web Pages (Razor) Site</span></span>

<span data-ttu-id="81339-105">от [Tom фитзмаккен](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="81339-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="81339-106">В этой статье описывается, как установить вспомогательную функцию на веб-сайте веб-страницы ASP.NET (Razor).</span><span class="sxs-lookup"><span data-stu-id="81339-106">This article describes how to install a helper in an ASP.NET Web Pages (Razor) website.</span></span> <span data-ttu-id="81339-107">*Вспомогательное приложение* — это многократно используемый компонент, который содержит код и разметку для выполнения задачи, которая может быть утомительной или сложной.</span><span class="sxs-lookup"><span data-stu-id="81339-107">A *helper* is a reusable component that includes code and markup to perform a task that might be tedious or complex.</span></span>
> 
> <span data-ttu-id="81339-108">Из этого руководства вы узнаете, как выполнять такие задачи:</span><span class="sxs-lookup"><span data-stu-id="81339-108">What you'll learn:</span></span>
> 
> - <span data-ttu-id="81339-109">Как установить вспомогательную функцию на веб-сайте, созданном с помощью WebMatrix 3.</span><span class="sxs-lookup"><span data-stu-id="81339-109">How to install a helper in a website created using WebMatrix 3.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="81339-110">Версии программного обеспечения, используемые в этом руководстве</span><span class="sxs-lookup"><span data-stu-id="81339-110">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="81339-111">WebMatrix 3</span><span class="sxs-lookup"><span data-stu-id="81339-111">WebMatrix 3</span></span>

## <a name="overview-of-helpers"></a><span data-ttu-id="81339-112">Обзор вспомогательных функций</span><span class="sxs-lookup"><span data-stu-id="81339-112">Overview of Helpers</span></span>

<span data-ttu-id="81339-113">Некоторые задачи, которые часто требуется выполнить на веб-страницах, потребовали много кода или требуются дополнительные знания.</span><span class="sxs-lookup"><span data-stu-id="81339-113">Some tasks that people often want to do on web pages require a lot of code or require extra knowledge.</span></span> <span data-ttu-id="81339-114">Примеры включают отображение диаграммы для данных; Добавление кнопки "Далее" в Twitter на странице; Отправка электронной почты с веб-сайта; Обрезка изображений или изменение их размера; использование PayPal для сайта.</span><span class="sxs-lookup"><span data-stu-id="81339-114">Examples include displaying a chart for data; putting a Twitter "Follow" button on a page; sending email from your website; cropping or resizing images; using PayPal for your site.</span></span> <span data-ttu-id="81339-115">Чтобы упростить эти виды действий, веб-страницы ASP.NET позволяет использовать *вспомогательные методы*.</span><span class="sxs-lookup"><span data-stu-id="81339-115">To make it easy to do these kinds of things, ASP.NET Web Pages lets you use *helpers*.</span></span> <span data-ttu-id="81339-116">Вспомогательные методы — это компоненты, которые устанавливаются для сайта и позволяют выполнять типичные задачи с помощью всего строки или двух кода Razor.</span><span class="sxs-lookup"><span data-stu-id="81339-116">Helpers are components that you install for a site and that let you perform typical tasks by using just a line or two of Razor code.</span></span>

<span data-ttu-id="81339-117">Веб-страницы ASP.NET имеет несколько встроенных вспомогательных функций.</span><span class="sxs-lookup"><span data-stu-id="81339-117">ASP.NET Web Pages has a few helpers built in.</span></span> <span data-ttu-id="81339-118">Однако многие вспомогательные методы доступны в пакетах (надстройках), которые предоставляются с помощью диспетчера пакетов NuGet.</span><span class="sxs-lookup"><span data-stu-id="81339-118">However, many helpers are available in packages (add-ins) that are provided using the NuGet package manager.</span></span> <span data-ttu-id="81339-119">NuGet позволяет выбрать пакет для установки, после чего он позаботится о всех деталях установки.</span><span class="sxs-lookup"><span data-stu-id="81339-119">NuGet lets you select a package to install and then it takes care of all the details of the installation.</span></span>

## <a name="installing-a-helper-in-webmatrix-3"></a><span data-ttu-id="81339-120">Установка вспомогательного модуля в WebMatrix 3</span><span class="sxs-lookup"><span data-stu-id="81339-120">Installing a Helper in WebMatrix 3</span></span>

1. <span data-ttu-id="81339-121">В WebMatrix 3 нажмите кнопку **NuGet** .</span><span class="sxs-lookup"><span data-stu-id="81339-121">In WebMatrix 3, click the **NuGet** button.</span></span>

    ![Диалоговое окно "коллекция NuGet" в WebMatrix](installing-helpers/_static/image1.png)
2. <span data-ttu-id="81339-123">Запустится диспетчер пакетов NuGet и отобразятся доступные пакеты.</span><span class="sxs-lookup"><span data-stu-id="81339-123">This launches the NuGet package manager and displays available packages.</span></span> <span data-ttu-id="81339-124">В поле поиска введите ключевое слово для вспомогательного приложения, которое требуется установить.</span><span class="sxs-lookup"><span data-stu-id="81339-124">In the search box, enter a keyword for the helper you want to install.</span></span>

    ![Диалоговое окно "коллекция NuGet" в WebMatrix](installing-helpers/_static/image2.png)
3. <span data-ttu-id="81339-126">Выберите пакет и нажмите кнопку **установить**.</span><span class="sxs-lookup"><span data-stu-id="81339-126">Select the package and then click **Install**.</span></span> <span data-ttu-id="81339-127">Нажмите кнопку **Да** при появлении запроса на установку пакета и укажите, что вы принимаете условия.</span><span class="sxs-lookup"><span data-stu-id="81339-127">Click **Yes** when asked if you want to install the package and indicate that you accept the terms.</span></span>

     <span data-ttu-id="81339-128">Если вы устанавливаете вспомогательный модуль в первый раз, NuGet создает папки на веб-сайте для кода, составляющего вспомогательное приложение.</span><span class="sxs-lookup"><span data-stu-id="81339-128">If this is the first time you've installed a helper, NuGet creates folders in your website for the code that makes up the helper.</span></span>
4. <span data-ttu-id="81339-129">Чтобы удалить вспомогательное приложение, нажмите кнопку **коллекция** , перейдите на вкладку **установленные** и выберите пакет, который нужно удалить.</span><span class="sxs-lookup"><span data-stu-id="81339-129">To uninstall a helper, click the **Gallery** button, click the **Installed** tab, and pick the package you want to uninstall.</span></span>

## <a name="installing-the-twitter-helper"></a><span data-ttu-id="81339-130">Установка вспомогательного приложения Twitter</span><span class="sxs-lookup"><span data-stu-id="81339-130">Installing the Twitter helper</span></span>

<span data-ttu-id="81339-131">Последняя версия API Twitter несовместима с вспомогательным приложением Twitter, которое устанавливается с помощью NuGet.</span><span class="sxs-lookup"><span data-stu-id="81339-131">The latest version of the Twitter API is not compatible with the Twitter helper you install through NuGet.</span></span> <span data-ttu-id="81339-132">Дополнительные сведения о настройке модуля поддержки Twitter в проекте см. в разделе [вспомогательное приложение Twitter в WebMatrix](twitter-helper.md) .</span><span class="sxs-lookup"><span data-stu-id="81339-132">Instead, see the [Twitter Helper with WebMatrix](twitter-helper.md) topic for information about how to set up the Twitter helper in your project.</span></span>

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a><span data-ttu-id="81339-133">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="81339-133">Additional Resources</span></span>

[<span data-ttu-id="81339-134">Основы программирования веб-страницы ASP.NET 2</span><span class="sxs-lookup"><span data-stu-id="81339-134">Introducing ASP.NET Web Pages 2 - Programming Basics</span></span>](../getting-started/introducing-razor-syntax-c.md)

[<span data-ttu-id="81339-135">Вспомогательное приложение Twitter с WebMatrix</span><span class="sxs-lookup"><span data-stu-id="81339-135">Twitter Helper with WebMatrix</span></span>](twitter-helper.md)
