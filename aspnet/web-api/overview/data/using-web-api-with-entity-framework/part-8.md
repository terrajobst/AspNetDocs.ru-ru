---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-8
title: Отобразить сведения об элементе | Документация Майкрософт
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/16/2014
ms.assetid: 75ef94b1-bbec-4681-9210-452dba816144
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-8
msc.type: authoredcontent
ms.openlocfilehash: 3f48c5ad73ceb9a4873fbbb621b518553a498966
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78449004"
---
# <a name="display-item-details"></a>Отображение сведений об элементе

по [Майк Уоссон](https://github.com/MikeWasson)

[Скачать завершенный проект](https://github.com/MikeWasson/BookService)

В этом разделе вы добавите возможность просмотра сведений для каждой книги. В App. js добавьте в модель представления следующий код:

[!code-javascript[Main](part-8/samples/sample1.js)]

В Views/Home/Index. cshtml добавьте элемент привязки данных к ссылке Details:

[!code-html[Main](part-8/samples/sample2.html?highlight=5)]

Это привязывает обработчик щелчка для &lt;элемента&gt; к функции `getBookDetail` в модели представления.

В том же файле замените следующую отметку:

[!code-html[Main](part-8/samples/sample3.html)]

следующим кодом:

[!code-html[Main](part-8/samples/sample4.html)]

Эта разметка создает таблицу, привязанную к данным в свойствах `detail` наблюдаемых в модели представления.

Синтаксис&lt;!--Ko--&gt;&quot; позволяет включить привязку маскирования за пределы элемента DOM. В этом случае привязка `if` вызывает отображение этого раздела разметки только в том случае, если `details` не имеет значение null.

[!code-html[Main](part-8/samples/sample5.html)]

Теперь, если запустить приложение и щелкнуть одну из &quot;сведений&quot; ссылок, приложение отобразит сведения о книге.

[![](part-8/_static/image2.png)](part-8/_static/image1.png)

> [!div class="step-by-step"]
> [Назад](part-7.md)
> [Вперед](part-9.md)
