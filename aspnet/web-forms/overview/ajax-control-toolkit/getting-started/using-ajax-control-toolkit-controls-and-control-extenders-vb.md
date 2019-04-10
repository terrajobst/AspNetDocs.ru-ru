---
uid: web-forms/overview/ajax-control-toolkit/getting-started/using-ajax-control-toolkit-controls-and-control-extenders-vb
title: С помощью элементов набора элементов управления AJAX и управляющих элементов-расширителей (VB) | Документация Майкрософт
author: microsoft
description: Сведения о добавлении элементов управления AJAX Control Toolkit и расширителей для страниц ASP.NET.
ms.author: riande
ms.date: 05/12/2009
ms.assetid: 763650a9-ffde-46a9-b779-7a9145dd5d88
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/getting-started/using-ajax-control-toolkit-controls-and-control-extenders-vb
msc.type: authoredcontent
ms.openlocfilehash: f3371165a30018c8096da8b6b9de567ed6fe6365
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2019
ms.locfileid: "59382632"
---
# <a name="using-ajax-control-toolkit-controls-and-control-extenders-vb"></a><span data-ttu-id="9740c-103">Использование элементов управления из набора элементов AJAX и управляющих элементов-расширителей (VB)</span><span class="sxs-lookup"><span data-stu-id="9740c-103">Using AJAX Control Toolkit Controls and Control Extenders (VB)</span></span>

<span data-ttu-id="9740c-104">по [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="9740c-104">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="9740c-105">Сведения о добавлении элементов управления AJAX Control Toolkit и расширителей для страниц ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="9740c-105">Learn how to add AJAX Control Toolkit controls and extenders to your ASP.NET pages.</span></span>


<span data-ttu-id="9740c-106">AJAX Control Toolkit содержит набор элементов управления и управляющих элементов-расширителей.</span><span class="sxs-lookup"><span data-stu-id="9740c-106">The AJAX Control Toolkit contains a set of controls and control extenders.</span></span> <span data-ttu-id="9740c-107">Из этого краткого руководства вы узнаете, как добавить элементы управления и управляющих элементов-расширителей для страницы ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="9740c-107">In this brief tutorial, you learn how to add both controls and control extenders to an ASP.NET page.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="9740c-108">Инструкции по установке AJAX Control Toolkit и добавление AJAX Control Toolkit на панель элементов Visual Studio или Visual Web Developer, см. в этом руководстве [приступить к работе с AJAX Control Toolkit](get-started-with-the-ajax-control-toolkit-vb.md).</span><span class="sxs-lookup"><span data-stu-id="9740c-108">For instructions on installing the AJAX Control Toolkit and adding the AJAX Control Toolkit to the Visual Studio/Visual Web Developer toolbox, see the tutorial [Get Started with the AJAX Control Toolkit](get-started-with-the-ajax-control-toolkit-vb.md).</span></span>


## <a name="using-ajax-control-toolkit-controls"></a><span data-ttu-id="9740c-109">С помощью элементов набора элементов управления AJAX</span><span class="sxs-lookup"><span data-stu-id="9740c-109">Using AJAX Control Toolkit Controls</span></span>

<span data-ttu-id="9740c-110">Элемент управления AJAX Control Toolkit работает так же, как обычный элемент управления ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="9740c-110">An AJAX Control Toolkit control works just like a normal ASP.NET control.</span></span> <span data-ttu-id="9740c-111">Можно перетащить элемент управления из панели элементов на странице ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="9740c-111">You can drag the control from the toolbox onto an ASP.NET page.</span></span> <span data-ttu-id="9740c-112">Элемент управления можно добавить на страницу в режиме конструктора или представление источника.</span><span class="sxs-lookup"><span data-stu-id="9740c-112">You can add the control to the page in either Design view or Source view.</span></span>

<span data-ttu-id="9740c-113">Нет одного особые требования при использовании элементов управления AJAX Control Toolkit.</span><span class="sxs-lookup"><span data-stu-id="9740c-113">There is one special requirement when using the controls from the AJAX Control Toolkit.</span></span> <span data-ttu-id="9740c-114">Страница должна содержать элемент управления ScriptManager.</span><span class="sxs-lookup"><span data-stu-id="9740c-114">The page must contain a ScriptManager control.</span></span> <span data-ttu-id="9740c-115">Элемент управления ScriptManager отвечает за включение все необходимые JavaScript, необходимую элементам управления AJAX Control Toolkit.</span><span class="sxs-lookup"><span data-stu-id="9740c-115">The ScriptManager control is responsible for including all of the necessary JavaScript required by the AJAX Control Toolkit controls.</span></span>

<span data-ttu-id="9740c-116">Например на вкладке AJAX Control Toolkit включает элемент управления с именем редактирующего элемента управления.</span><span class="sxs-lookup"><span data-stu-id="9740c-116">For example, the AJAX Control Toolkit tab includes a control named the Editor control.</span></span> <span data-ttu-id="9740c-117">Этот элемент управления отображает мощный HTML редактор.</span><span class="sxs-lookup"><span data-stu-id="9740c-117">This control displays a rich HTML editor.</span></span> <span data-ttu-id="9740c-118">Выполните следующие действия, чтобы добавить на страницу элемент управления редактора.</span><span class="sxs-lookup"><span data-stu-id="9740c-118">Follow these steps to add the Editor control to a page:</span></span>

1. <span data-ttu-id="9740c-119">Создать новую страницу ASP.NET с именем ShowEditor.aspx</span><span class="sxs-lookup"><span data-stu-id="9740c-119">Create a new ASP.NET page named ShowEditor.aspx</span></span>
2. <span data-ttu-id="9740c-120">Выберите элемент управления ScriptManager from beneath вкладки AJAX-расширения в области элементов и перетащите элемент управления на страницу.</span><span class="sxs-lookup"><span data-stu-id="9740c-120">Select the ScriptManager control from beneath the AJAX Extensions tab in the toolbox and drag the control onto the page.</span></span>
3. <span data-ttu-id="9740c-121">Выберите элемент управления редактора from beneath вкладке AJAX Control Toolkit на панели элементов и перетащите элемент управления на страницу (см. рис. 1).</span><span class="sxs-lookup"><span data-stu-id="9740c-121">Select the Editor control from beneath the AJAX Control Toolkit tab in the toolbox and drag the control onto the page (see Figure 1).</span></span> <span data-ttu-id="9740c-122">Конструктор должен выглядеть как на рис. 2.</span><span class="sxs-lookup"><span data-stu-id="9740c-122">The Designer should look like Figure 2.</span></span>
4. <span data-ttu-id="9740c-123">Запустите веб-сайт, выбрав вариант меню **отладка, начать отладку** или нажмите клавишу F5.</span><span class="sxs-lookup"><span data-stu-id="9740c-123">Run the web site by selecting the menu option **Debug, Start Debugging** or hitting the F5 key.</span></span>
5. <span data-ttu-id="9740c-124">Вы увидите страницу, на рис. 3.</span><span class="sxs-lookup"><span data-stu-id="9740c-124">You should see the page in Figure 3.</span></span>


[![S<span data-ttu-id="9740c-125">Отказ от элемент управления редактора HTML]</span><span class="sxs-lookup"><span data-stu-id="9740c-125">electing the HTML Editor control]</span></span>(using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image1.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image1.png)

<span data-ttu-id="9740c-126">**Рис 01**: Выбрав элемент управления редактора HTML ([Просмотр полноразмерного изображения](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="9740c-126">**Figure 01**: Selecting the HTML Editor control([Click to view full-size image](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image2.png))</span></span>


[![V<span data-ttu-id="9740c-127">isual Studio конструктора с элементом управления ScriptManager и редактирования]</span><span class="sxs-lookup"><span data-stu-id="9740c-127">isual Studio Designer with ScriptManager and Edit control]</span></span>(using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image2.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image3.png)

<span data-ttu-id="9740c-128">**Рис. 02**: Конструктор Visual Studio с помощью элемента управления ScriptManager и редактирования ([Просмотр полноразмерного изображения](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image4.png))</span><span class="sxs-lookup"><span data-stu-id="9740c-128">**Figure 02**: Visual Studio Designer with ScriptManager and Edit control([Click to view full-size image](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image4.png))</span></span>


[![T<span data-ttu-id="9740c-129">страница DisplayEditor.aspx HE]</span><span class="sxs-lookup"><span data-stu-id="9740c-129">he DisplayEditor.aspx page]</span></span>(using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image3.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image5.png)

<span data-ttu-id="9740c-130">**Рис 03**: На странице DisplayEditor.aspx ([Просмотр полноразмерного изображения](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="9740c-130">**Figure 03**: The DisplayEditor.aspx page([Click to view full-size image](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image6.png))</span></span>


## <a name="using-ajax-control-toolkit-control-extenders"></a><span data-ttu-id="9740c-131">С помощью набора средств управляющих элементов-расширителей элементов управления AJAX</span><span class="sxs-lookup"><span data-stu-id="9740c-131">Using AJAX Control Toolkit Control Extenders</span></span>

<span data-ttu-id="9740c-132">AJAX Control Toolkit также содержит управляющих элементов-расширителей.</span><span class="sxs-lookup"><span data-stu-id="9740c-132">The AJAX Control Toolkit also contains control extenders.</span></span> <span data-ttu-id="9740c-133">Как предполагает имя, управляющего элемента-расширителя расширяет функциональность существующего элемента управления.</span><span class="sxs-lookup"><span data-stu-id="9740c-133">As its name suggests, a control extender extends the functionality of an existing control.</span></span> <span data-ttu-id="9740c-134">Например элемент управления средства расширения ConfirmButton расширяет стандартный элемент управления ASP.NET Button.</span><span class="sxs-lookup"><span data-stu-id="9740c-134">For example, the ConfirmButton control extender extends the standard ASP.NET Button control.</span></span> <span data-ttu-id="9740c-135">Расширитель изменяет поведение кнопки элемента управления s, чтобы кнопка отображает диалоговое окно подтверждения, если щелкнуть его.</span><span class="sxs-lookup"><span data-stu-id="9740c-135">The extender changes the Button control�s behavior so that the Button displays a confirmation dialog when you click it.</span></span>

<span data-ttu-id="9740c-136">Расширитель элемента управления, так же, как элемент управления AJAX Control Toolkit, необходим элемент управления ScriptManager.</span><span class="sxs-lookup"><span data-stu-id="9740c-136">A control extender, just like an AJAX Control Toolkit control, requires a ScriptManager control.</span></span> <span data-ttu-id="9740c-137">Перед началом использования расширителей элементов управления на странице, необходимо добавить элемент управления ScriptManager к странице.</span><span class="sxs-lookup"><span data-stu-id="9740c-137">You must add a ScriptManager control to a page before you start using control extenders in the page.</span></span>

<span data-ttu-id="9740c-138">Выполните следующие действия для использования средства расширения ConfirmButton элемента управления.</span><span class="sxs-lookup"><span data-stu-id="9740c-138">Follow these steps to use the ConfirmButton control extender:</span></span>

1. <span data-ttu-id="9740c-139">Создать новую страницу ASP.NET с именем ShowConfirmButton.aspx</span><span class="sxs-lookup"><span data-stu-id="9740c-139">Create a new ASP.NET page named ShowConfirmButton.aspx</span></span>
2. <span data-ttu-id="9740c-140">Добавьте элемент управления ScriptManager к странице, перетащив элемент управления на странице from beneath вкладки AJAX-расширения.</span><span class="sxs-lookup"><span data-stu-id="9740c-140">Add a ScriptManager control to the page by dragging the control onto the page from beneath the AJAX Extensions tab.</span></span>
3. <span data-ttu-id="9740c-141">Добавление стандартного элемента управления кнопки на страницу, перетащив кнопку from beneath вкладке «Стандартные» на панели элементов в область конструктора.</span><span class="sxs-lookup"><span data-stu-id="9740c-141">Add a standard Button control to the page by dragging the Button from beneath the Standard tab in the toolbox onto the Designer surface.</span></span>
4. <span data-ttu-id="9740c-142">Нажмите кнопку **Добавить расширитель** параметр задачи (см. рис. 4).</span><span class="sxs-lookup"><span data-stu-id="9740c-142">Click the **Add Extender** task option (see Figure 4).</span></span>
5. <span data-ttu-id="9740c-143">В диалоговом окне выберите расширитель выберите ConfirmButtonExtender (см. рис. 5) и нажмите кнопку "ОК".</span><span class="sxs-lookup"><span data-stu-id="9740c-143">In the Choose Extender dialog, select ConfirmButtonExtender (see Figure 5) and click the OK button.</span></span>
6. <span data-ttu-id="9740c-144">Выберите элемент управления в конструкторе и разверните средств расширения, Button1\_ConfirmButtonExtender узла в окне «Свойства» (см. рис. 6).</span><span class="sxs-lookup"><span data-stu-id="9740c-144">Select the Button control in the Designer and expand the Extenders, Button1\_ConfirmButtonExtender node in the Properties window (see Figure 6).</span></span> <span data-ttu-id="9740c-145">Назначьте *действительно?* ConfirmText свойству.</span><span class="sxs-lookup"><span data-stu-id="9740c-145">Assign the value *�Really?�* to the ConfirmText property.</span></span>
7. <span data-ttu-id="9740c-146">Откройте страницу, выбрав параметр меню **отладка, начать отладку** или нажмите клавишу F5.</span><span class="sxs-lookup"><span data-stu-id="9740c-146">Run the page by selecting the menu option **Debug, Start Debugging** or hit the F5 key.</span></span>


[![T<span data-ttu-id="9740c-147">он параметр задачи Добавить расширитель]</span><span class="sxs-lookup"><span data-stu-id="9740c-147">he Add Extender task option]</span></span>(using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image4.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image7.png)

<span data-ttu-id="9740c-148">**Рис. 04**: Параметр задачи Добавить расширитель ([Просмотр полноразмерного изображения](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image8.png))</span><span class="sxs-lookup"><span data-stu-id="9740c-148">**Figure 04**: The Add Extender task option([Click to view full-size image](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image8.png))</span></span>


[![S<span data-ttu-id="9740c-149">Отказ от средства расширения ConfirmButton управления]</span><span class="sxs-lookup"><span data-stu-id="9740c-149">electing the ConfirmButton control extender]</span></span>(using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image5.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image9.png)

<span data-ttu-id="9740c-150">**05 рис**: Выбрав элемент управления средства расширения ConfirmButton ([Просмотр полноразмерного изображения](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image10.png))</span><span class="sxs-lookup"><span data-stu-id="9740c-150">**Figure 05**: Selecting the ConfirmButton control extender([Click to view full-size image](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image10.png))</span></span>


[![S<span data-ttu-id="9740c-151">выполнение свойство ConfirmButton]</span><span class="sxs-lookup"><span data-stu-id="9740c-151">etting a ConfirmButton property]</span></span>(using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image6.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image11.png)

<span data-ttu-id="9740c-152">**Рис 06**: Задание свойства ConfirmButton ([Просмотр полноразмерного изображения](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image12.png))</span><span class="sxs-lookup"><span data-stu-id="9740c-152">**Figure 06**: Setting a ConfirmButton property([Click to view full-size image](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image12.png))</span></span>


<span data-ttu-id="9740c-153">При открытии страницы вы увидите кнопку.</span><span class="sxs-lookup"><span data-stu-id="9740c-153">When the page opens, you should see a button.</span></span> <span data-ttu-id="9740c-154">При нажатии кнопки появляется диалоговое окно подтверждения на рис. 7.</span><span class="sxs-lookup"><span data-stu-id="9740c-154">When you click the button, you get the confirmation dialog in Figure 7.</span></span>


[![D<span data-ttu-id="9740c-155">isplaying диалоговое окно подтверждения]</span><span class="sxs-lookup"><span data-stu-id="9740c-155">isplaying the confirmation dialog]</span></span>(using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image7.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image13.png)

<span data-ttu-id="9740c-156">**07 рис**: Отображение диалоговое окно подтверждения ([Просмотр полноразмерного изображения](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image14.png))</span><span class="sxs-lookup"><span data-stu-id="9740c-156">**Figure 07**: Displaying the confirmation dialog([Click to view full-size image](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image14.png))</span></span>


<span data-ttu-id="9740c-157">Обратите внимание на то, что обычно не перетащить расширитель элемента управления на страницу.</span><span class="sxs-lookup"><span data-stu-id="9740c-157">Notice that you normally do not drag a control extender onto a page.</span></span> <span data-ttu-id="9740c-158">Вместо этого использовать **Добавить расширитель** задач параметр, чтобы добавить расширение к элементу управления, уже добавленных на страницу.</span><span class="sxs-lookup"><span data-stu-id="9740c-158">Instead, you use the **Add Extender** task option to add an extender to a control that you have already added to a page.</span></span> <span data-ttu-id="9740c-159">Обратите внимание на то, кроме того, настройте элемент управления свойства расширителя, открыв окно свойств для расширяемого элемента управления.</span><span class="sxs-lookup"><span data-stu-id="9740c-159">Notice, furthermore, that you set control extender properties by opening the property sheet for the control being extended.</span></span>

<span data-ttu-id="9740c-160">Один элемент управления ASP.NET может быть расширена путем нескольких управляющих элементов-расширителей.</span><span class="sxs-lookup"><span data-stu-id="9740c-160">A single ASP.NET control can be extended by multiple control extenders.</span></span> <span data-ttu-id="9740c-161">Окно свойств для расширяемого элемента управления будут перечислены все расширителей элементов управления, связанные с элементом управления.</span><span class="sxs-lookup"><span data-stu-id="9740c-161">The property sheet for the control being extended will list all of the control extenders associated with the control.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="9740c-162">[Назад](get-started-with-the-ajax-control-toolkit-vb.md)
> [Вперед](creating-a-custom-ajax-control-toolkit-control-extender-vb.md)</span><span class="sxs-lookup"><span data-stu-id="9740c-162">[Previous](get-started-with-the-ajax-control-toolkit-vb.md)
[Next](creating-a-custom-ajax-control-toolkit-control-extender-vb.md)</span></span>
