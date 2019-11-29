---
uid: web-forms/overview/ajax-control-toolkit/dropshadow/manipulating-dropshadow-properties-from-client-code-vb
title: Управление свойствами DropShadow из клиентского кода (VB) | Документация Майкрософт
author: wenz
description: Элемент управления DropShadow в наборе средств AJAX Control Toolkit расширяет панель с тенью. Свойства этого расширителя также можно изменить с помощью Жаваскрип клиента...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 11be4211-2fb9-4e15-b6d4-2aa623d81f3e
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/dropshadow/manipulating-dropshadow-properties-from-client-code-vb
msc.type: authoredcontent
ms.openlocfilehash: a39adb9c06819f6f828add7d762effad430b8570
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/28/2019
ms.locfileid: "74574043"
---
# <a name="manipulating-dropshadow-properties-from-client-code-vb"></a><span data-ttu-id="62192-104">Обработка свойств DropShadow из клиентского кода (VB)</span><span class="sxs-lookup"><span data-stu-id="62192-104">Manipulating DropShadow Properties from Client Code (VB)</span></span>

<span data-ttu-id="62192-105">по [Кристиан Венз](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="62192-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="62192-106">[Скачать код](https://download.microsoft.com/download/5/1/6/51652a81-500b-4f6b-88d3-617103e7941e/DropShadow2.vb.zip) или [скачать PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dropshadow2VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="62192-106">[Download Code](https://download.microsoft.com/download/5/1/6/51652a81-500b-4f6b-88d3-617103e7941e/DropShadow2.vb.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dropshadow2VB.pdf)</span></span>

> <span data-ttu-id="62192-107">Элемент управления DropShadow в наборе средств AJAX Control Toolkit расширяет панель с тенью.</span><span class="sxs-lookup"><span data-stu-id="62192-107">The DropShadow control in the AJAX Control Toolkit extends a panel with a drop shadow.</span></span> <span data-ttu-id="62192-108">Свойства этого расширителя также можно изменить с помощью клиентского кода JavaScript.</span><span class="sxs-lookup"><span data-stu-id="62192-108">Properties of this extender can also be changed using client JavaScript code.</span></span>

## <a name="overview"></a><span data-ttu-id="62192-109">Обзор</span><span class="sxs-lookup"><span data-stu-id="62192-109">Overview</span></span>

<span data-ttu-id="62192-110">Элемент управления DropShadow в наборе средств AJAX Control Toolkit расширяет панель с тенью.</span><span class="sxs-lookup"><span data-stu-id="62192-110">The DropShadow control in the AJAX Control Toolkit extends a panel with a drop shadow.</span></span> <span data-ttu-id="62192-111">Свойства этого расширителя также можно изменить с помощью клиентского кода JavaScript.</span><span class="sxs-lookup"><span data-stu-id="62192-111">Properties of this extender can also be changed using client JavaScript code.</span></span>

## <a name="steps"></a><span data-ttu-id="62192-112">Шаги</span><span class="sxs-lookup"><span data-stu-id="62192-112">Steps</span></span>

<span data-ttu-id="62192-113">Код начинается с панели, содержащей несколько строк текста:</span><span class="sxs-lookup"><span data-stu-id="62192-113">The code starts with a panel containing some lines of text:</span></span>

[!code-aspx[Main](manipulating-dropshadow-properties-from-client-code-vb/samples/sample1.aspx)]

<span data-ttu-id="62192-114">Связанный класс CSS предоставляет панели хороший цвет фона:</span><span class="sxs-lookup"><span data-stu-id="62192-114">The associated CSS class gives the panel a nice background color:</span></span>

[!code-css[Main](manipulating-dropshadow-properties-from-client-code-vb/samples/sample2.css)]

<span data-ttu-id="62192-115">`DropShadowExtender` добавляется для расширения панели с эффектом тени, для параметра Opacity устанавливается значение 50%:</span><span class="sxs-lookup"><span data-stu-id="62192-115">The `DropShadowExtender` is added to extend the panel with a drop shadow effect, opacity set to 50%:</span></span>

[!code-aspx[Main](manipulating-dropshadow-properties-from-client-code-vb/samples/sample3.aspx)]

<span data-ttu-id="62192-116">Затем элемент управления `ScriptManager` AJAX ASP.NET позволяет набору элементов управления работать:</span><span class="sxs-lookup"><span data-stu-id="62192-116">Then, the ASP.NET AJAX `ScriptManager` control enables the Control Toolkit to work:</span></span>

[!code-aspx[Main](manipulating-dropshadow-properties-from-client-code-vb/samples/sample4.aspx)]

<span data-ttu-id="62192-117">Другая панель содержит две ссылки JavaScript для настройки непрозрачности тени. ссылка «минус» уменьшает прозрачность тени, а ссылка «плюс» увеличивает ее.</span><span class="sxs-lookup"><span data-stu-id="62192-117">Another panel contains two JavaScript links for setting the opacity of the drop shadow: the minus link decreases the shadow's opacity, the plus link increases it.</span></span>

[!code-aspx[Main](manipulating-dropshadow-properties-from-client-code-vb/samples/sample5.aspx)]

<span data-ttu-id="62192-118">После этого функция JavaScript `changeOpacity()` должна сначала найти элемент управления `DropShadowExtender` на странице.</span><span class="sxs-lookup"><span data-stu-id="62192-118">The JavaScript function `changeOpacity()` must then first find the `DropShadowExtender` control on the page.</span></span> <span data-ttu-id="62192-119">ASP.NET AJAX определяет метод `$find()` для точности этой задачи.</span><span class="sxs-lookup"><span data-stu-id="62192-119">ASP.NET AJAX defines the `$find()` method for exactly that task.</span></span> <span data-ttu-id="62192-120">Затем метод `get_Opacity()` извлекает текущую непрозрачность, метод `set_Opacity()` задает его.</span><span class="sxs-lookup"><span data-stu-id="62192-120">Then, the `get_Opacity()` method retrieves the current opacity, the `set_Opacity()` method sets it.</span></span> <span data-ttu-id="62192-121">Затем код JavaScript помещает текущее значение непрозрачности в элемент `<label>`:</span><span class="sxs-lookup"><span data-stu-id="62192-121">The JavaScript code then puts the current opacity value in the `<label>` element:</span></span>

[!code-html[Main](manipulating-dropshadow-properties-from-client-code-vb/samples/sample6.html)]

<span data-ttu-id="62192-122">[![на стороне клиента изменяется непрозрачность](manipulating-dropshadow-properties-from-client-code-vb/_static/image2.png)](manipulating-dropshadow-properties-from-client-code-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="62192-122">[![The opacity is changed on the client side](manipulating-dropshadow-properties-from-client-code-vb/_static/image2.png)](manipulating-dropshadow-properties-from-client-code-vb/_static/image1.png)</span></span>

<span data-ttu-id="62192-123">Непрозрачность изменяется на стороне клиента ([щелкните, чтобы просмотреть изображение с полным размером](manipulating-dropshadow-properties-from-client-code-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="62192-123">The opacity is changed on the client side ([Click to view full-size image](manipulating-dropshadow-properties-from-client-code-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="62192-124">Назад</span><span class="sxs-lookup"><span data-stu-id="62192-124">Previous</span></span>](adjusting-the-z-index-of-a-dropshadow-vb.md)
