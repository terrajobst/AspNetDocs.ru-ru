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
# <a name="aspnet-webhooks-debugging"></a>Отладка веб-перехватчиков ASP.NET  

## <a name="debugging-in-azure"></a>Отладка в Azure

Чтобы выполнить отладку веб-приложения во время работы в Azure, см. Руководство по [устранению неполадок веб-приложения в службе приложений Azure с помощью Visual Studio](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/#webserverlogs).

## <a name="debugging-with-source-and-symbols"></a>Отладка с использованием исходного кода и символов

В дополнение к отладке собственного кода можно выполнять отладку непосредственно в Microsoft ASP.NET веб-перехватчиках и на самом деле все .NET. Это работает независимо от того, выполняется ли отладка локально или удаленно. Сначала настройте Visual Studio, чтобы найти исходный код и символы, выбрав **Отладка** , а затем — **Параметры и параметры**. Задайте такие параметры:

![Параметры и настройки](_static/SourceSymbols.png)

Затем добавьте ссылку на [symbolsource.org](http://symbolsource.org) для скачивания исходного кода и символов. Перейдите на вкладку **символы** в меню выше и добавьте в качестве расположения символа следующее:

```
http://srv.symbolsource.org/pdb/Public
```

Кроме того, убедитесь, что каталог кэша имеет короткое имя. в противном случае имена файлов могут оказаться слишком длинными, что приведет к тому, что символы не будут загружены. Пример пути:

```
C:\SymCache
```

Параметры должны выглядеть следующим образом:

![Пример параметра расположение файла символов](_static/SymSource.png)
