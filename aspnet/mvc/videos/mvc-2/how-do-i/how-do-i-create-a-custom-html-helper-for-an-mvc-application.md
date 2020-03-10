---
uid: mvc/videos/mvc-2/how-do-i/how-do-i-create-a-custom-html-helper-for-an-mvc-application
title: Инструкции. Создание пользовательского вспомогательного метода HTML для приложения MVC | Документы Майкрософт
author: rick-anderson
description: В этом видео Крис пикселей показано, как создать пользовательский HtmlHelper, недоступный в стандартном наборе в приложении MVC. Во-первых, пример MVC прило...
ms.author: riande
ms.date: 12/11/2009
ms.assetid: 58b5eb15-4160-4ce2-ae70-6ba94262ea73
msc.legacyurl: /mvc/videos/mvc-2/how-do-i/how-do-i-create-a-custom-html-helper-for-an-mvc-application
msc.type: video
ms.openlocfilehash: 60953243d3038667e4f729b1394e68f0c9d7c178
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78450480"
---
# <a name="how-do-i-create-a-custom-html-helper-for-an-mvc-application"></a>Инструкции. Создание пользовательского вспомогательного метода HTML для приложения MVC

от [Крис пикселей](https://twitter.com/chrispels)

В этом видео Крис пикселей показано, как создать пользовательский HtmlHelper, недоступный в стандартном наборе в приложении MVC. Во-первых, пример приложения MVC создается с демонстрационным контроллером и представлением для тестирования пользовательского HtmlHelper. Затем создается модуль с открытой функцией, которая является методом расширения, представляющим реализацию пользовательского HtmlHelper. Пользовательский вспомогательный метод предназначен для создания тегов `<img>` на странице и получения нескольких входящих параметров, включая идентификатор, URL-адрес и замещающий текст для тега Image. Затем логика добавляется в функцию для возвращения завершенного тега `<img>` с указанными сведениями. Затем пользовательское HtmlHelper используется на демонстрационной странице для вывода изображения. Наконец, Пользовательский HtmlHelper расширяется для включения нескольких переопределений конструктора, которые обеспечивают гибкость для упрощения создания различных тегов `<img>`.

[&#9654;Смотреть видео (18 минут)](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-create-a-custom-html-helper-for-an-mvc-application)

> [!div class="step-by-step"]
> [Назад](how-do-i-implement-view-models-to-manage-data-for-aspnet-mvc-views.md)
> [Вперед](how-do-i-work-with-model-binders-in-an-mvc-application.md)
