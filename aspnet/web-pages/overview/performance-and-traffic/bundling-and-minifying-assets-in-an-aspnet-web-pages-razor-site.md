---
uid: web-pages/overview/performance-and-traffic/bundling-and-minifying-assets-in-an-aspnet-web-pages-razor-site
title: Объединение и Минификация ресурсов на сайте веб-страницы ASP.NET (Razor) | Документация Майкрософт
author: microsoft
description: Объединение и минификации — это способы повышения производительности сайта. Объединение позволяет объединять несколько файлов JavaScript (JS) или нескольких каскадных таблиц стилей (...
ms.author: riande
ms.date: 06/21/2012
ms.assetid: 8906f1e9-4b66-4a03-8e8a-9e9debf8ed91
msc.legacyurl: /web-pages/overview/performance-and-traffic/bundling-and-minifying-assets-in-an-aspnet-web-pages-razor-site
msc.type: authoredcontent
ms.openlocfilehash: 5e42111ad71ec65581e56c73822e23ecd5fcbd58
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78516180"
---
# <a name="bundling-and-minifying-assets-in-an-aspnet-web-pages-razor-site"></a><span data-ttu-id="2556a-104">Объединение и минификация активов на сайте веб-страниц ASP.NET (Razor)</span><span class="sxs-lookup"><span data-stu-id="2556a-104">Bundling and Minifying Assets in an ASP.NET Web Pages (Razor) Site</span></span>

<span data-ttu-id="2556a-105">по [Майкрософт](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="2556a-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="2556a-106">Объединение и минификации — это способы повышения производительности сайта.</span><span class="sxs-lookup"><span data-stu-id="2556a-106">Bundling and minification are ways to make your site faster.</span></span> <span data-ttu-id="2556a-107">Объединение позволяет объединять несколько файлов JavaScript ( *. js*) или нескольких каскадных таблиц стилей (*CSS*), чтобы их можно было загружать как единое целое, а не по одному за раз.</span><span class="sxs-lookup"><span data-stu-id="2556a-107">Bundling lets you combine multiple JavaScript (*.js*) files or multiple cascading style sheet (*.css*) files so that they can be downloaded as a unit, rather than one at a time.</span></span> <span data-ttu-id="2556a-108">Минификации сжимает пробелы и выполняет другие виды сжатия, чтобы сделать Скачанные файлы максимально возможными.</span><span class="sxs-lookup"><span data-stu-id="2556a-108">Minification squeezes out whitespace and performs other types of compression to make the downloaded files as small a possible.</span></span>
> 
> > [!NOTE]
> > <span data-ttu-id="2556a-109">Версия-кандидат веб-страницы ASP.NET 2 не поддерживает объединение и минификации, так как пакет, содержащий необходимые элементы, еще не доступен в Microsoft WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="2556a-109">The RC release of ASP.NET Web Pages 2 does not support bundling and minification because the package that contains the required elements is not yet available in Microsoft WebMatrix.</span></span> <span data-ttu-id="2556a-110">Приносим извинения за неудобства.</span><span class="sxs-lookup"><span data-stu-id="2556a-110">We apologize for this inconvenience.</span></span> <span data-ttu-id="2556a-111">Ожидается, что пакет будет доступен в окончательном выпуске веб-страницы ASP.NET 2 и WebMatrix 2.</span><span class="sxs-lookup"><span data-stu-id="2556a-111">The package is expected to be available in the final release of ASP.NET Web Pages 2 and WebMatrix 2.</span></span>
