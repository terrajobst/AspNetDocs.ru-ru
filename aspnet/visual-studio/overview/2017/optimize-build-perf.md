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
# <a name="optimize-build-performance-for-solution"></a>Оптимизация производительности сборки для решения

Visual Studio 2017 15,8 или более поздней версии включает пункт меню: **сборка** > **компиляции ASP.NET** > **оптимизировать производительность сборки для решения**.

![Снимок экрана нового пункта меню](optimize-build-perf/_static/optimize-build-performance-for-solution.png)

ASP.NET компилирует свои представления во время выполнения, что означает, что проект ASP.NET несет с собой копию компилятора. Однако на компьютере разработчика, когда копия компилятора не совпадает с копией Visual Studio, производительность сборки будет затронута в 1-3 секунд на каждую инкрементную сборку. Эта функция обновляет копию компилятора проекта в соответствии с Visual Studio, что обычно ускоряет добавочные сборки.

**Это применимо только к проектам ASP.NET Framework 4.7.1 или более поздней версии, оно не применяется к ASP.NET Core.**
