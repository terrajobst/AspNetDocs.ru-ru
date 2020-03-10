---
uid: webhooks/diagnostics/debugging
title: Отладка веб-перехватчиков ASP.NET | Документация Майкрософт
author: rick-anderson
description: Отладка веб-перехватчиков ASP.NET.
ms.author: riande
ms.date: 01/17/2012
ms.assetid: 467da78b-3c35-4c51-8b08-77a32379e4a8
ms.openlocfilehash: 517d282fc22703b5861b748aea51023fa0a12a26
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78520602"
---
# <a name="aspnet-webhooks-debugging"></a><span data-ttu-id="a1ce8-103">Отладка веб-перехватчиков ASP.NET</span><span class="sxs-lookup"><span data-stu-id="a1ce8-103">ASP.NET WebHooks debugging</span></span>  

## <a name="debugging-in-azure"></a><span data-ttu-id="a1ce8-104">Отладка в Azure</span><span class="sxs-lookup"><span data-stu-id="a1ce8-104">Debugging in Azure</span></span>

<span data-ttu-id="a1ce8-105">Чтобы выполнить отладку веб-приложения во время работы в Azure, см. Руководство по [устранению неполадок веб-приложения в службе приложений Azure с помощью Visual Studio](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/#webserverlogs).</span><span class="sxs-lookup"><span data-stu-id="a1ce8-105">To debug your Web Application while running in Azure, please see the tutorial [Troubleshoot a web app in Azure App Service using Visual Studio](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/#webserverlogs).</span></span>

## <a name="debugging-with-source-and-symbols"></a><span data-ttu-id="a1ce8-106">Отладка с использованием исходного кода и символов</span><span class="sxs-lookup"><span data-stu-id="a1ce8-106">Debugging with Source and Symbols</span></span>

<span data-ttu-id="a1ce8-107">В дополнение к отладке собственного кода можно выполнять отладку непосредственно в Microsoft ASP.NET веб-перехватчиках и на самом деле все .NET.</span><span class="sxs-lookup"><span data-stu-id="a1ce8-107">In addition to debugging your own code, it is possible to debug directly into Microsoft ASP.NET WebHooks, and in fact all of .NET.</span></span> <span data-ttu-id="a1ce8-108">Это работает независимо от того, выполняется ли отладка локально или удаленно.</span><span class="sxs-lookup"><span data-stu-id="a1ce8-108">This works regardless of whether you debug locally or remotely.</span></span> <span data-ttu-id="a1ce8-109">Сначала настройте Visual Studio, чтобы найти исходный код и символы, выбрав **Отладка** , а затем — **Параметры и параметры**.</span><span class="sxs-lookup"><span data-stu-id="a1ce8-109">First, configure Visual Studio to find the source and symbols by going to **Debug** and then **Options and Settings**.</span></span> <span data-ttu-id="a1ce8-110">Задайте такие параметры:</span><span class="sxs-lookup"><span data-stu-id="a1ce8-110">Set the options like this:</span></span>

![Параметры и настройки](_static/SourceSymbols.png)

<span data-ttu-id="a1ce8-112">Затем добавьте ссылку на [symbolsource.org](http://symbolsource.org) для скачивания исходного кода и символов.</span><span class="sxs-lookup"><span data-stu-id="a1ce8-112">Then add a link to [symbolsource.org](http://symbolsource.org) for downloading the source and symbols.</span></span> <span data-ttu-id="a1ce8-113">Перейдите на вкладку **символы** в меню выше и добавьте в качестве расположения символа следующее:</span><span class="sxs-lookup"><span data-stu-id="a1ce8-113">Go to the **Symbols** tab of the menu above and add the following as a symbol location:</span></span>

```
http://srv.symbolsource.org/pdb/Public
```

<span data-ttu-id="a1ce8-114">Кроме того, убедитесь, что каталог кэша имеет короткое имя. в противном случае имена файлов могут оказаться слишком длинными, что приведет к тому, что символы не будут загружены.</span><span class="sxs-lookup"><span data-stu-id="a1ce8-114">In addition, make sure that the cache directory has a short name; otherwise the file names can get too long which will cause the symbols to not load.</span></span> <span data-ttu-id="a1ce8-115">Пример пути:</span><span class="sxs-lookup"><span data-stu-id="a1ce8-115">A sample path is:</span></span>

```
C:\SymCache
```

<span data-ttu-id="a1ce8-116">Параметры должны выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="a1ce8-116">The settings should look similar to this:</span></span>

![Пример параметра расположение файла символов](_static/SymSource.png)
