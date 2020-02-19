---
uid: mvc/overview/views/dynamic-v-strongly-typed-views
title: Динамические и Строго типизированные представления | Документация Майкрософт
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 01/27/2011
ms.assetid: 0cbd88da-0da6-4605-b222-2835c6478304
msc.legacyurl: /mvc/overview/views/dynamic-v-strongly-typed-views
msc.type: authoredcontent
ms.openlocfilehash: 3e81c6381b1e280e3b74cb7eb6ea6e6c3224e655
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/19/2020
ms.locfileid: "77455681"
---
# <a name="dynamic-v-strongly-typed-views"></a>Динамические и строго типизированные представления

по [Рик Андерсон (](https://twitter.com/RickAndMSFT)

Существует три способа передачи информации из контроллера в представление в ASP.NET MVC 3:

1. Как объект модели со строгой типизацией.
2. Как динамический тип (с помощью @model Dynamic)
3. Использование ViewBag

Я написал простое приложение блогов MVC третьего уровня для сравнения динамических и строго типизированных представлений. Контроллер начинается с простого списка блогов:

[!code-csharp[Main](dynamic-v-strongly-typed-views/samples/sample1.cs)]

Щелкните правой кнопкой мыши метод Индекснотстонглитипед () и добавьте представление Razor.

[![8475. Нотстронглитипедвиев [1]](dynamic-v-strongly-typed-views/_static/image2.png)](dynamic-v-strongly-typed-views/_static/image1.png)

Убедитесь, что флажок **создать строго типизированное представление** не установлен. Результирующее представление не содержит много:

[!code-cshtml[Main](dynamic-v-strongly-typed-views/samples/sample2.cshtml)]

[!code-cshtml[Main](dynamic-v-strongly-typed-views/samples/sample3.cshtml)]

Так как мы используем динамическое, а не строго типизированное представление, IntelliSense не помогает нам. Завершенный код показан ниже:

[!code-cshtml[Main](dynamic-v-strongly-typed-views/samples/sample4.cshtml)]

[![6646. NotStronglyTypedView_5F00_IE [1]](dynamic-v-strongly-typed-views/_static/image4.png)](dynamic-v-strongly-typed-views/_static/image3.png)

Теперь мы добавим строго типизированное представление. Добавьте следующий код в контроллер:

[!code-csharp[Main](dynamic-v-strongly-typed-views/samples/sample5.cs)]

Обратите внимание, что это точно такое же возвращаемое представление (Топблогс); Вызовите метод как нестрого типизированное представление. Щелкните правой кнопкой мыши внутри *стонглитипединдекс ()* и выберите **Добавить представление**. На этот раз выберите класс модель **блога** и выберите **список** в качестве шаблона шаблонов.

[![5658. Стронгвиев [1]](dynamic-v-strongly-typed-views/_static/image6.png)](dynamic-v-strongly-typed-views/_static/image5.png)

В новом шаблоне представления мы получаем поддержку IntelliSense.

[![7002. IntelliSense [1]](dynamic-v-strongly-typed-views/_static/image8.png)](dynamic-v-strongly-typed-views/_static/image7.png)

Проект c# можно скачать [здесь](https://blogs.msdn.com/cfs-file.ashx/__key/CommunityServer-Blogs-Components-WeblogFiles/00-00-01-11-73-SSMS/1817.Mvc3ViewDemo.zip).
