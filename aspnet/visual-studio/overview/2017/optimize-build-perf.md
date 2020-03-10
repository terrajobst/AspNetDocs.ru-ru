---
uid: visual-studio/overview/2017/optimize-build-perf
title: Оптимизация производительности сборки для решения
author: AngelosP
description: Оптимизация производительности сборки для решения
ms.author: riande
ms.date: 08/29/2018
msc.type: authoredcontent
ms.openlocfilehash: c1a5cf5e59374b4c0dd7150c5dd62fbde42af555
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78504978"
---
# <a name="optimize-build-performance-for-solution"></a><span data-ttu-id="f1d34-103">Оптимизация производительности сборки для решения</span><span class="sxs-lookup"><span data-stu-id="f1d34-103">Optimize build performance for solution</span></span>

<span data-ttu-id="f1d34-104">Visual Studio 2017 15,8 или более поздней версии включает пункт меню: **сборка** > **компиляции ASP.NET** > **оптимизировать производительность сборки для решения**.</span><span class="sxs-lookup"><span data-stu-id="f1d34-104">Visual Studio 2017 15.8 or later include a menu item: **Build** > **ASP.NET Compilation** > **Optimize Build Performance for Solution**.</span></span>

![Снимок экрана нового пункта меню](optimize-build-perf/_static/optimize-build-performance-for-solution.png)

<span data-ttu-id="f1d34-106">ASP.NET компилирует свои представления во время выполнения, что означает, что проект ASP.NET несет с собой копию компилятора.</span><span class="sxs-lookup"><span data-stu-id="f1d34-106">ASP.NET compiles its views at runtime, which means that an ASP.NET project carries with it a copy of the compiler.</span></span> <span data-ttu-id="f1d34-107">Однако на компьютере разработчика, когда копия компилятора не совпадает с копией Visual Studio, производительность сборки будет затронута в 1-3 секунд на каждую инкрементную сборку.</span><span class="sxs-lookup"><span data-stu-id="f1d34-107">However on a developer machine when the copy of the compiler doesn't match Visual Studio's copy, build performance is impacted on the order of 1-3 seconds per incremental build.</span></span> <span data-ttu-id="f1d34-108">Эта функция обновляет копию компилятора проекта в соответствии с Visual Studio, что обычно ускоряет добавочные сборки.</span><span class="sxs-lookup"><span data-stu-id="f1d34-108">This feature updates your project's copy of the compiler to match Visual Studio's, which usually speeds up incremental builds.</span></span>

<span data-ttu-id="f1d34-109">**Это применимо только к проектам ASP.NET Framework 4.7.1 или более поздней версии, оно не применяется к ASP.NET Core.**</span><span class="sxs-lookup"><span data-stu-id="f1d34-109">**This is applicable to ASP.NET Framework 4.7.1 or later projects only, it does not apply to ASP.NET Core.**</span></span>
