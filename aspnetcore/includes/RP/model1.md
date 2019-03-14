---
ms.openlocfilehash: 934db70fe49ba9a5330b25596dc694e0ac50c04e
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57037901"
---
Автор: [Рик Андерсон](https://twitter.com/RickAndMSFT) (Rick Anderson)

В этом разделе мы добавим классы для управления фильмами в базе данных. Эти классы используются в [Entity Framework Core](/ef/core) (EF Core) для работы с базой данных. EF Core —это платформа объектно реляционного сопоставления (ORM), которая позволяет упростить необходимый код доступа к данным.

Создаваемые вами классы моделей называются классами POCO (от "plain old CLR objects" — старые добрые объекты CLR), так как они не зависят от EF Core. Эти классы определяют свойства данных, которые хранятся в базе данных.

Работая с этим учебником, вы напишете классы моделей, а затем EF Core создаст базу данных. Другой вариант, который здесь не рассматривается: [создание классов моделей из существующей базы данных](/ef/core/get-started/aspnetcore/existing-db).

[Просмотрите или скачайте](https://github.com/aspnet/Docs/tree/master/aspnetcore/tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie) пример.
