---
uid: web-forms/overview/ajax-control-toolkit/dynamicpopulate/dynamically-populating-a-control-vb
title: Динамическое заполнение элемента управления (VB) | Документация Майкрософт
author: wenz
description: Элемент управления DynamicPopulate в наборе средств управления AJAX ASP.NET вызывает веб-службу (или метод страницы) и заполняет результирующее значение целевым элементом управления на t...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 27305347-7b5d-4519-97b7-197a357e7f6e
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/dynamicpopulate/dynamically-populating-a-control-vb
msc.type: authoredcontent
ms.openlocfilehash: d11320f1f89bb69afe5f62751574079716124da0
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78430458"
---
# <a name="dynamically-populating-a-control-vb"></a>Динамическое заполнение элемента управления (VB)

по [Кристиан Венз](https://github.com/wenz)

[Скачать код](https://download.microsoft.com/download/d/8/f/d8f2f6f9-1b7c-46ad-9252-e1fc81bdea3e/dynamicpopulate0.vb.zip) или [скачать PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dynamicpopulate0VB.pdf)

> Элемент управления DynamicPopulate в наборе средств управления AJAX ASP.NET вызывает веб-службу (или метод страницы) и заполняет полученное значение в целевом элементе управления на странице без обновления страницы.

## <a name="overview"></a>Обзор

Элемент управления `DynamicPopulate` в наборе средств управления AJAX ASP.NET вызывает веб-службу (или метод страницы) и заполняет полученное значение в целевом элементе управления на странице без обновления страницы. В этом руководстве показано, как это сделать.

## <a name="steps"></a>Шаги

Во-первых, вам понадобится ASP.NET Web Service, который реализует метод, вызываемый `DynamicPopulate`. Для класса веб-службы требуется атрибут `ScriptService`, определенный в `Microsoft.Web.Script.Services`; в противном случае ASP.NET AJAX не может создать клиентский прокси JavaScript для веб-службы, которая, в свою очередь, необходима для `DynamicPopulate`.

Веб-метод должен рассчитывать на один аргумент типа String, именуемый `contextKey`, поскольку элемент управления `DynamicPopulate` отправляет один фрагмент сведений о контексте при каждом вызове веб-службы. Следующая веб-служба возвращает текущую дату в формате, представленном аргументом `contextKey`:

[!code-aspx[Main](dynamically-populating-a-control-vb/samples/sample1.aspx)]

Затем веб-служба сохраняется как `DynamicPopulate.vb.asmx`. Кроме того, можно реализовать метод `getDate()` как метод страницы в реальной странице ASP.NET с помощью элемента управления `DynamicPopulate`.

На следующем шаге создайте новый файл ASP.NET. Как всегда, первым шагом является включение `ScriptManager` на текущую страницу для загрузки библиотеки ASP.NET AJAX и обеспечения работы набора средств управления:

[!code-aspx[Main](dynamically-populating-a-control-vb/samples/sample2.aspx)]

Затем добавьте элемент управления Label (например, с помощью элемента управления HTML с тем же именем или &lt;`asp:Label` /&gt; веб-элемент управления), который позже покажет результат вызова веб-службы.

[!code-aspx[Main](dynamically-populating-a-control-vb/samples/sample3.aspx)]

Кнопка HTML (как HTML-элемент управления, так как нам не требуется обратная передача на сервер) будет использоваться для активации динамического заполнения:

[!code-aspx[Main](dynamically-populating-a-control-vb/samples/sample4.aspx)]

Наконец, нам нужен элемент управления `DynamicPopulateExtender` для подключения к ним. Будут установлены следующие атрибуты (помимо очевидных, `ID` и `runat`=`"server"`):

- `TargetControlID`, куда помещается результат вызова веб-службы
- `ServicePath` путь к веб-службе (пропустите, если вы хотите использовать метод страницы)
- `ServiceMethod` имя веб-метода или метода страницы
- `ContextKey` сведения о контексте для отправки веб-службе
- элемент `PopulateTriggerControlID`, который активирует вызов веб-службы
- `ClearContentsDuringUpdate`, следует ли очищать целевой элемент во время вызова веб-службы

Как видите, элементу управления требуются некоторые сведения, но размещение всех данных в нем довольно прямолинейно. Ниже приведена разметка для элемента управления `DynamicPopulateExtender` в текущем сценарии.

[!code-aspx[Main](dynamically-populating-a-control-vb/samples/sample5.aspx)]

Запустите страницу ASP.NET в браузере и нажмите кнопку. Вы получите текущую дату в формате "месяц-день-год".

[![нажатии кнопки получает дату с сервера](dynamically-populating-a-control-vb/_static/image2.png)](dynamically-populating-a-control-vb/_static/image1.png)

При нажатии кнопки извлекается дата с сервера ([щелкните, чтобы просмотреть изображение с полным размером](dynamically-populating-a-control-vb/_static/image3.png)).

> [!div class="step-by-step"]
> [Назад](using-dynamicpopulate-with-a-user-control-and-javascript-cs.md)
> [Вперед](dynamically-populating-a-control-using-javascript-code-vb.md)
