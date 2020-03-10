---
uid: web-forms/overview/ajax-control-toolkit/dropshadow/manipulating-dropshadow-properties-from-client-code-cs
title: Управление свойствами DropShadow из клиентского кода (C#) | Документация Майкрософт
author: wenz
description: Настройка интерфейса правки элемента управления DataList
ms.author: riande
ms.date: 06/02/2008
ms.assetid: c83ca3e6-c0bf-4158-a166-40c1ab0f33da
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/dropshadow/manipulating-dropshadow-properties-from-client-code-cs
msc.type: authoredcontent
ms.openlocfilehash: 790f0d881e43518600968d6c175d4eaa53d0e5f9
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78497430"
---
# <a name="manipulating-dropshadow-properties-from-client-code-c"></a><span data-ttu-id="93d3d-103">Обработка свойств DropShadow из клиентского кода (C#)</span><span class="sxs-lookup"><span data-stu-id="93d3d-103">Manipulating DropShadow Properties from Client Code (C#)</span></span>

<span data-ttu-id="93d3d-104">по [Кристиан Венз](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="93d3d-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="93d3d-105">[Скачать код](https://download.microsoft.com/download/5/1/6/51652a81-500b-4f6b-88d3-617103e7941e/DropShadow2.cs.zip) или [скачать PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dropshadow2CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="93d3d-105">[Download Code](https://download.microsoft.com/download/5/1/6/51652a81-500b-4f6b-88d3-617103e7941e/DropShadow2.cs.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dropshadow2CS.pdf)</span></span>

> <span data-ttu-id="93d3d-106">Элемент управления DropShadow в наборе средств AJAX Control Toolkit расширяет панель с тенью.</span><span class="sxs-lookup"><span data-stu-id="93d3d-106">The DropShadow control in the AJAX Control Toolkit extends a panel with a drop shadow.</span></span> <span data-ttu-id="93d3d-107">Свойства этого расширителя также можно изменить с помощью клиентского кода JavaScript.</span><span class="sxs-lookup"><span data-stu-id="93d3d-107">Properties of this extender can also be changed using client JavaScript code.</span></span>

## <a name="overview"></a><span data-ttu-id="93d3d-108">Обзор</span><span class="sxs-lookup"><span data-stu-id="93d3d-108">Overview</span></span>

<span data-ttu-id="93d3d-109">Элемент управления DropShadow в наборе средств AJAX Control Toolkit расширяет панель с тенью.</span><span class="sxs-lookup"><span data-stu-id="93d3d-109">The DropShadow control in the AJAX Control Toolkit extends a panel with a drop shadow.</span></span> <span data-ttu-id="93d3d-110">Свойства этого расширителя также можно изменить с помощью клиентского кода JavaScript.</span><span class="sxs-lookup"><span data-stu-id="93d3d-110">Properties of this extender can also be changed using client JavaScript code.</span></span>

## <a name="steps"></a><span data-ttu-id="93d3d-111">Шаги</span><span class="sxs-lookup"><span data-stu-id="93d3d-111">Steps</span></span>

<span data-ttu-id="93d3d-112">Код начинается с панели, содержащей несколько строк текста:</span><span class="sxs-lookup"><span data-stu-id="93d3d-112">The code starts with a panel containing some lines of text:</span></span>

[!code-aspx[Main](manipulating-dropshadow-properties-from-client-code-cs/samples/sample1.aspx)]

<span data-ttu-id="93d3d-113">Связанный класс CSS предоставляет панели хороший цвет фона:</span><span class="sxs-lookup"><span data-stu-id="93d3d-113">The associated CSS class gives the panel a nice background color:</span></span>

[!code-css[Main](manipulating-dropshadow-properties-from-client-code-cs/samples/sample2.css)]

<span data-ttu-id="93d3d-114">`DropShadowExtender` добавляется для расширения панели с эффектом тени, для параметра Opacity устанавливается значение 50%:</span><span class="sxs-lookup"><span data-stu-id="93d3d-114">The `DropShadowExtender` is added to extend the panel with a drop shadow effect, opacity set to 50%:</span></span>

[!code-aspx[Main](manipulating-dropshadow-properties-from-client-code-cs/samples/sample3.aspx)]

<span data-ttu-id="93d3d-115">Затем элемент управления `ScriptManager` AJAX ASP.NET позволяет набору элементов управления работать:</span><span class="sxs-lookup"><span data-stu-id="93d3d-115">Then, the ASP.NET AJAX `ScriptManager` control enables the Control Toolkit to work:</span></span>

[!code-aspx[Main](manipulating-dropshadow-properties-from-client-code-cs/samples/sample4.aspx)]

<span data-ttu-id="93d3d-116">Другая панель содержит две ссылки JavaScript для настройки непрозрачности тени. ссылка «минус» уменьшает прозрачность тени, а ссылка «плюс» увеличивает ее.</span><span class="sxs-lookup"><span data-stu-id="93d3d-116">Another panel contains two JavaScript links for setting the opacity of the drop shadow: the minus link decreases the shadow's opacity, the plus link increases it.</span></span>

[!code-aspx[Main](manipulating-dropshadow-properties-from-client-code-cs/samples/sample5.aspx)]

<span data-ttu-id="93d3d-117">После этого функция JavaScript `changeOpacity()` должна сначала найти элемент управления `DropShadowExtender` на странице.</span><span class="sxs-lookup"><span data-stu-id="93d3d-117">The JavaScript function `changeOpacity()` must then first find the `DropShadowExtender` control on the page.</span></span> <span data-ttu-id="93d3d-118">ASP.NET AJAX определяет метод `$find()` для точности этой задачи.</span><span class="sxs-lookup"><span data-stu-id="93d3d-118">ASP.NET AJAX defines the `$find()` method for exactly that task.</span></span> <span data-ttu-id="93d3d-119">Затем метод `get_Opacity()` извлекает текущую непрозрачность, метод `set_Opacity()` задает его.</span><span class="sxs-lookup"><span data-stu-id="93d3d-119">Then, the `get_Opacity()` method retrieves the current opacity, the `set_Opacity()` method sets it.</span></span> <span data-ttu-id="93d3d-120">Затем код JavaScript помещает текущее значение непрозрачности в элемент `<label>`:</span><span class="sxs-lookup"><span data-stu-id="93d3d-120">The JavaScript code then puts the current opacity value in the `<label>` element:</span></span>

[!code-html[Main](manipulating-dropshadow-properties-from-client-code-cs/samples/sample6.html)]

<span data-ttu-id="93d3d-121">[![на стороне клиента изменяется непрозрачность](manipulating-dropshadow-properties-from-client-code-cs/_static/image2.png)](manipulating-dropshadow-properties-from-client-code-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="93d3d-121">[![The opacity is changed on the client side](manipulating-dropshadow-properties-from-client-code-cs/_static/image2.png)](manipulating-dropshadow-properties-from-client-code-cs/_static/image1.png)</span></span>

<span data-ttu-id="93d3d-122">Непрозрачность изменяется на стороне клиента ([щелкните, чтобы просмотреть изображение с полным размером](manipulating-dropshadow-properties-from-client-code-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="93d3d-122">The opacity is changed on the client side ([Click to view full-size image](manipulating-dropshadow-properties-from-client-code-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="93d3d-123">[Назад](adjusting-the-z-index-of-a-dropshadow-cs.md)
> [Вперед](adjusting-the-z-index-of-a-dropshadow-vb.md)</span><span class="sxs-lookup"><span data-stu-id="93d3d-123">[Previous](adjusting-the-z-index-of-a-dropshadow-cs.md)
[Next](adjusting-the-z-index-of-a-dropshadow-vb.md)</span></span>
