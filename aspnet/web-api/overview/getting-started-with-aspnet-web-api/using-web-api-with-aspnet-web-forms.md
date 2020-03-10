---
uid: web-api/overview/getting-started-with-aspnet-web-api/using-web-api-with-aspnet-web-forms
title: Использование веб-API с ASP.NET Web Forms-ASP.NET 4. x
author: MikeWasson
description: Руководство с кодом пошаговым руководством по добавлению веб-API в приложение ASP.NET Forms для ASP.NET 4. x
ms.author: riande
ms.date: 04/03/2012
ms.custom: seoapril2019
ms.assetid: 25da8c3f-4e90-4946-9765-4f160985e1e4
msc.legacyurl: /web-api/overview/getting-started-with-aspnet-web-api/using-web-api-with-aspnet-web-forms
msc.type: authoredcontent
ms.openlocfilehash: ae553b62998fefd128e12711cbde958ea42d8c63
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78448536"
---
# <a name="using-web-api-with-aspnet-web-forms"></a>Использование веб-API с помощью веб-форм ASP.NET

по [Майк Уоссон](https://github.com/MikeWasson)

В этом руководстве описано, как добавить веб-API в традиционное приложение ASP.NET Web Forms в ASP.NET 4. x. 

## <a name="overview"></a>Обзор

Хотя веб-API ASP.NET упаковывается с помощью ASP.NET MVC, можно легко добавить веб-API в традиционное приложение ASP.NET Web Forms.

Для использования веб-API в приложении Web Forms необходимо выполнить два основных действия.

- Добавьте контроллер веб-API, производный от класса **ApiController** .
- Добавьте таблицу маршрутов в метод **\_запуска приложения** .

## <a name="create-a-web-forms-project"></a>Создание проекта веб-форм

Запустите Visual Studio и выберите **создать проект** на **начальной** странице. Либо в меню **файл** выберите **создать** , а затем — **проект**.

В области **шаблоны** выберите **Установленные шаблоны** и разверните узел  **C# визуального** элемента. В **разделе C#визуальный** элемент выберите **веб**. В списке шаблонов проектов выберите **ASP.NET Web Forms Application**. Введите имя проекта и нажмите кнопку **ОК**.

![](using-web-api-with-aspnet-web-forms/_static/image1.png)

## <a name="create-the-model-and-controller"></a>Создание модели и контроллера

В этом руководстве используются те же классы модели и контроллера, что и в [Начало работы](tutorial-your-first-web-api.md) руководстве.

Сначала добавьте класс Model. В **Обозреватель решений**щелкните правой кнопкой мыши проект и выберите команду **Добавить класс**. Назовите класс Product и добавьте следующую реализацию:

[!code-csharp[Main](using-web-api-with-aspnet-web-forms/samples/sample1.cs)]

Затем добавьте в проект контроллер веб-API. *контроллер* — это объект, который обрабатывает HTTP-запросы к веб API.

В **обозревателе решений** щелкните проект правой кнопкой мыши. Выберите **Добавить новый элемент**.

![](using-web-api-with-aspnet-web-forms/_static/image2.png)

В разделе **Установленные шаблоны**разверните **узел C# визуальный** элемент и выберите **веб**. Затем в списке шаблонов выберите **класс контроллера веб-API**. Присвойте контроллеру имя "Продуктсконтроллер" и нажмите кнопку **Добавить**.

![](using-web-api-with-aspnet-web-forms/_static/image3.png)

Мастер **добавления нового элемента** создаст файл с именем ProductsController.cs. Удалите методы, добавленные мастером, и добавьте следующие методы.

[!code-csharp[Main](using-web-api-with-aspnet-web-forms/samples/sample2.cs)]

Дополнительные сведения о коде в этом контроллере см. в руководстве по [Начало работы](tutorial-your-first-web-api.md) .

## <a name="add-routing-information"></a>Добавление сведений о маршрутизации

Далее мы добавим маршрут URI, чтобы в контроллере были направляться URI формы &quot;/АПИ/Продуктс/&quot;.

В **Обозреватель решений**дважды щелкните Global. asax, чтобы открыть файл кода программной части Global.asax.cs. Добавьте следующую инструкцию **using** .

[!code-csharp[Main](using-web-api-with-aspnet-web-forms/samples/sample3.cs)]

Затем добавьте следующий код в метод **\_запуска приложения** :

[!code-csharp[Main](using-web-api-with-aspnet-web-forms/samples/sample4.cs)]

Дополнительные сведения о таблицах маршрутизации см. [в разделе Маршрутизация в веб-API ASP.NET](../web-api-routing-and-actions/routing-in-aspnet-web-api.md).

## <a name="add-client-side-ajax"></a>Добавление AJAX на стороне клиента

Это все, что необходимо для создания веб-API, к которому могут обращаться клиенты. Теперь добавим HTML-страницу, которая использует jQuery для вызова API.

Убедитесь, что эталонная страница (например, *site. master*) содержит `ContentPlaceHolder` с `ID="HeadContent"`:

[!code-html[Main](using-web-api-with-aspnet-web-forms/samples/sample8.html)]

Откройте файл Default. aspx. Замените стандартный текст в разделе основное содержимое, как показано ниже.

[!code-aspx[Main](using-web-api-with-aspnet-web-forms/samples/sample5.aspx)]

Затем добавьте ссылку на исходный файл jQuery в раздел `HeaderContent`:

[!code-aspx[Main](using-web-api-with-aspnet-web-forms/samples/sample6.aspx?highlight=2)]

Примечание. можно легко добавить ссылку на скрипт, перетащив файл из **Обозреватель решений** в окно редактора кода.

![](using-web-api-with-aspnet-web-forms/_static/image4.png)

Под тегом скрипта jQuery добавьте следующий блок скрипта:

[!code-html[Main](using-web-api-with-aspnet-web-forms/samples/sample7.html)]

Когда документ загружается, этот скрипт делает запрос AJAX для &quot;API и продуктов&quot;. Запрос возвращает список продуктов в формате JSON. Сценарий добавляет сведения о продукте в таблицу HTML.

При запуске приложения оно должно выглядеть следующим образом:

![](using-web-api-with-aspnet-web-forms/_static/image5.png)
