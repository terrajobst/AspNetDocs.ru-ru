---
ms.openlocfilehash: 545448e3673b02abc7e685bd987f2cf5f71375b4
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57051961"
---
> [!WARNING]
> <span data-ttu-id="09fdf-101">В целях безопасности вам следует задать привязку данных запроса `GET` к свойствам страничной модели.</span><span class="sxs-lookup"><span data-stu-id="09fdf-101">For security reasons, you must opt in to binding `GET` request data to page model properties.</span></span> <span data-ttu-id="09fdf-102">Проверьте введенные данные пользователя, прежде чем сопоставлять их со свойствами.</span><span class="sxs-lookup"><span data-stu-id="09fdf-102">Verify user input before mapping it to properties.</span></span> <span data-ttu-id="09fdf-103">Привязка `GET` полезна при обращении к сценариям, использующим строку запроса или значения маршрутов.</span><span class="sxs-lookup"><span data-stu-id="09fdf-103">Opting in to `GET` binding is useful when addressing scenarios which rely on query string or route values.</span></span>
>
> <span data-ttu-id="09fdf-104">Чтобы привязать свойство к запросам `GET`, задайте в атрибуте [[BindProperty]](/dotnet/api/microsoft.aspnetcore.mvc.bindpropertyattribute) для свойства `SupportsGet` значение `true`: `[BindProperty(SupportsGet = true)]`.</span><span class="sxs-lookup"><span data-stu-id="09fdf-104">To bind a property on `GET` requests, set the [[BindProperty]](/dotnet/api/microsoft.aspnetcore.mvc.bindpropertyattribute) attribute's `SupportsGet` property to `true`: `[BindProperty(SupportsGet = true)]`</span></span>