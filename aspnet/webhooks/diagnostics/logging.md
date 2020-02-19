---
uid: webhooks/diagnostics/logging
title: Ведение журнала веб-перехватчиков ASP.NET | Документация Майкрософт
author: rick-anderson
description: Как выполнять вход в веб-перехватчики ASP.NET.
ms.author: riande
ms.date: 01/17/2012
ms.assetid: f71bc442-5f80-481b-a32c-a0ec18dee9d6
ms.openlocfilehash: a05b32c4a8f9577bcf6170bd19a9e440b1aeb75b
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457587"
---
# <a name="aspnet-webhooks-logging"></a>Ведение журнала веб-перехватчиков ASP.NET

Microsoft ASP.NET веб-перехватчики используют ведение журнала в качестве способа создания отчетов о проблемах и проблемах. По умолчанию журналы записываются с помощью [System. Diagnostics. Trace](https://msdn.microsoft.com/library/system.diagnostics.trace) , где их можно отслеживать с помощью [прослушивателей трассировки](https://msdn.microsoft.com/library/system.diagnostics.tracelistener.aspx) , как и любого другого потока журнала.

При развертывании веб-приложения в качестве веб-приложения Azure журналы автоматически выбираются и могут управляться вместе с любым другим журналом событий [системы. Diagnostics. Trace](https://msdn.microsoft.com/library/system.diagnostics.trace) . Дополнительные сведения см. [в статье Включение ведения журнала диагностики для веб-приложений в службе приложений Azure](https://azure.microsoft.com/documentation/articles/web-sites-enable-diagnostic-log/) .

Кроме того, журналы можно получить непосредственно из Visual Studio, как описано в статье [Устранение неполадок веб-приложения в службе приложений Azure с помощью Visual Studio](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/#webserverlogs).

## <a name="redirecting-logs"></a>Перенаправление журналов

Вместо записи журналов в [System. Diagnostics. Trace](https://msdn.microsoft.com/library/system.diagnostics.trace)можно реализовать альтернативную реализацию ведения журнала, которая может входить непосредственно в Диспетчер журналов, например [log4net](http://logging.apache.org/log4net/) и [NLog](http://nlog-project.org/). Просто предоставьте реализацию [ILogger](https://github.com/aspnet/AspNetWebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Common/Diagnostics/ILogger.cs) и зарегистрируйте ее с помощью подсистемы внедрения зависимостей по своему усмотрению, и она будет забираться Microsoft ASP.NET веб-перехватчиками. Дополнительные сведения см. [в разделе Введение зависимостей в веб-API ASP.NET 2](https://www.asp.net/web-api/overview/advanced/dependency-injection) .
