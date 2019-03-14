---
ms.openlocfilehash: b6f39dd0dedb38961eb021cde355f7ec83283195
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57024871"
---
# <a name="aspnet-core-web-api-controller-sample"></a><span data-ttu-id="8b0f2-101">Пример контроллера веб-API ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="8b0f2-101">ASP.NET Core Web API Controller Sample</span></span>

<span data-ttu-id="8b0f2-102">Этот пример приложения состоит из следующих проектов:</span><span class="sxs-lookup"><span data-stu-id="8b0f2-102">This sample app consists of the following projects:</span></span>

- <span data-ttu-id="8b0f2-103">\**WebApiSample.Api.22*: Проект ASP.NET Core 2.2, предназначенных для .NET Core 2.2.</span><span class="sxs-lookup"><span data-stu-id="8b0f2-103">\**WebApiSample.Api.22*: An ASP.NET Core 2.2 project targeting .NET Core 2.2.</span></span>
- <span data-ttu-id="8b0f2-104">**WebApiSample.Api.21**: Проект ASP.NET Core 2.1, предназначенных для .NET Core 2.1.</span><span class="sxs-lookup"><span data-stu-id="8b0f2-104">**WebApiSample.Api.21**: An ASP.NET Core 2.1 project targeting .NET Core 2.1.</span></span>
- <span data-ttu-id="8b0f2-105">**WebApiSample.Api.Pre21**: Проект ASP.NET Core 2.0, предназначенном для .NET Core 2.0.</span><span class="sxs-lookup"><span data-stu-id="8b0f2-105">**WebApiSample.Api.Pre21**: An ASP.NET Core 2.0 project targeting .NET Core 2.0.</span></span>
- <span data-ttu-id="8b0f2-106">**WebApiSample.DataAccess**: Библиотека классов .NET Standard 2.0, выступая в качестве уровня доступа данных для проектов веб-API 2.</span><span class="sxs-lookup"><span data-stu-id="8b0f2-106">**WebApiSample.DataAccess**: A .NET Standard 2.0 class library serving as a data access tier for the 2 Web API projects.</span></span>

<span data-ttu-id="8b0f2-107">В этом примере показаны различные способы создания контроллера веб-API:</span><span class="sxs-lookup"><span data-stu-id="8b0f2-107">This sample illustrates variations of Web API controller creation:</span></span>

- [<span data-ttu-id="8b0f2-108">Создание класса, производного от ControllerBase</span><span class="sxs-lookup"><span data-stu-id="8b0f2-108">Derive class from ControllerBase</span></span>](https://docs.microsoft.com/aspnet/core/web-api#derive-class-from-controllerbase)
- [<span data-ttu-id="8b0f2-109">Аннотирование класса атрибутом ApiControllerAttribute</span><span class="sxs-lookup"><span data-stu-id="8b0f2-109">Annotate class with ApiControllerAttribute</span></span>](https://docs.microsoft.com/aspnet/core/web-api#annotate-class-with-apicontrollerattribute)
