---
ms.openlocfilehash: e5565381f44480e2531925717ee7815da92d1ff5
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57030041"
---
# <a name="update-the-generated-pages"></a>Изменение созданных страниц

Автор: [Рик Андерсон](https://twitter.com/RickAndMSFT) (Rick Anderson)

Все готово для приложения по работе с фильмами, но презентация далеко не идеальна. Мы не хотим видеть время (12:00:00 AM на рисунке ниже), а заголовок **ReleaseDate** (ДатаВыпуска) должен состоять из двух слов: **Release Date**.

![Приложение Movie с данными по фильмам, открытое в Chrome](../../tutorials/razor-pages/sql/_static/m55.png)

## <a name="update-the-generated-code"></a>Обновление созданного кода

Откройте файл *Models/Movie.cs* и добавьте указанные ниже выделенные строки кода:

[!code-csharp[](code/Models/Movie.cs?highlight=2,11-12)]
