---
ms.openlocfilehash: 939231583679d469d01724cc1a405bd45e46d2c5
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57175901"
---
```console
npm run release
```

Эта команда создает ресурсы на стороне клиента, которые будут обслуживаться при выполнении приложения. Эти ресурсы помещаются в папку *wwwroot*.

Веб-пакет выполнил следующие задачи:

* Очистка содержимого каталога *wwwroot*.
* Преобразование TypeScript в JavaScript (&mdash;этот процесс называется *транспилированием*).
* Корректировка созданного кода JavaScript в целях уменьшения размера файла (&mdash;этот процесс называется *минификацией*).
* Копирование обработанных файлов JavaScript, CSS и HTML из каталога *src* в *wwwroot*.
* Внедрение следующих элементов в файл *wwwroot/index.html*:
    * Тег `<link>`, ссылающийся на файл *wwwroot/main.\<hash\>.css*. Этот тег размещается непосредственно после закрывающего тега `</head>`.
    * Тег `<script>`, ссылающийся на минифицированный файл *wwwroot/main.\<hash\>.js*. Этот тег размещается непосредственно после закрывающего тега `</body>`.