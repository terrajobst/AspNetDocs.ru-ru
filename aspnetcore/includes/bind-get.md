---
ms.openlocfilehash: 545448e3673b02abc7e685bd987f2cf5f71375b4
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57051961"
---
> [!WARNING]
> В целях безопасности вам следует задать привязку данных запроса `GET` к свойствам страничной модели. Проверьте введенные данные пользователя, прежде чем сопоставлять их со свойствами. Привязка `GET` полезна при обращении к сценариям, использующим строку запроса или значения маршрутов.
>
> Чтобы привязать свойство к запросам `GET`, задайте в атрибуте [[BindProperty]](/dotnet/api/microsoft.aspnetcore.mvc.bindpropertyattribute) для свойства `SupportsGet` значение `true`: `[BindProperty(SupportsGet = true)]`.
