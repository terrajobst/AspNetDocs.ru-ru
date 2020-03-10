---
uid: web-forms/overview/ajax-control-toolkit/mutuallyexclusivecheckbox/creating-mutually-exclusive-checkboxes-vb
title: Создание взаимоисключающих флажков (VB) | Документация Майкрософт
author: wenz
description: 'Если можно выбрать только один из наборов параметров, обычно используются переключатели. Однако существует недостаток: один переключатель в группе,...'
ms.author: riande
ms.date: 06/02/2008
ms.assetid: e9dd1d5a-a1db-4114-981d-6a91acb1d709
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/mutuallyexclusivecheckbox/creating-mutually-exclusive-checkboxes-vb
msc.type: authoredcontent
ms.openlocfilehash: f33936dd4d71f6bbf08f02966eefe44c8c152eba
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78446166"
---
# <a name="creating-mutually-exclusive-checkboxes-vb"></a><span data-ttu-id="f75cc-104">Создание взаимоисключающих флажков (VB)</span><span class="sxs-lookup"><span data-stu-id="f75cc-104">Creating Mutually Exclusive Checkboxes (VB)</span></span>

<span data-ttu-id="f75cc-105">по [Кристиан Венз](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="f75cc-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="f75cc-106">[Скачать код](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/MutuallyExclusiveCheckBox0.vb.zip) или [скачать PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/mutuallyexclusivecheckbox0VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="f75cc-106">[Download Code](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/MutuallyExclusiveCheckBox0.vb.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/mutuallyexclusivecheckbox0VB.pdf)</span></span>

> <span data-ttu-id="f75cc-107">Если можно выбрать только один из наборов параметров, обычно используются переключатели.</span><span class="sxs-lookup"><span data-stu-id="f75cc-107">When only one of a set of options may be selected, radio buttons are usually used.</span></span> <span data-ttu-id="f75cc-108">Несмотря на то, что один переключатель в группе выбран, снять флажок все переключатели невозможно.</span><span class="sxs-lookup"><span data-stu-id="f75cc-108">There is a drawback, though: Once one radio button in a group is selected, it is not possible to uncheck all radio buttons.</span></span> <span data-ttu-id="f75cc-109">Флажки в любое время можно снять, но они не являются взаимоисключающими.</span><span class="sxs-lookup"><span data-stu-id="f75cc-109">Check boxes can be unchecked at any time, however are not mutually exclusive.</span></span> <span data-ttu-id="f75cc-110">В этом учебнике лучше использовать оба подхода: флажки, которые являются взаимоисключающими.</span><span class="sxs-lookup"><span data-stu-id="f75cc-110">This tutorial provides the best of both approaches: check boxes that are mutually exclusive.</span></span>

## <a name="overview"></a><span data-ttu-id="f75cc-111">Обзор</span><span class="sxs-lookup"><span data-stu-id="f75cc-111">Overview</span></span>

<span data-ttu-id="f75cc-112">Если можно выбрать только один из наборов параметров, обычно используются переключатели.</span><span class="sxs-lookup"><span data-stu-id="f75cc-112">When only one of a set of options may be selected, radio buttons are usually used.</span></span> <span data-ttu-id="f75cc-113">Несмотря на то, что один переключатель в группе выбран, снять флажок все переключатели невозможно.</span><span class="sxs-lookup"><span data-stu-id="f75cc-113">There is a drawback, though: Once one radio button in a group is selected, it is not possible to uncheck all radio buttons.</span></span> <span data-ttu-id="f75cc-114">Флажки в любое время можно снять, но они не являются взаимоисключающими.</span><span class="sxs-lookup"><span data-stu-id="f75cc-114">Check boxes can be unchecked at any time, however are not mutually exclusive.</span></span> <span data-ttu-id="f75cc-115">В этом учебнике лучше использовать оба подхода: флажки, которые являются взаимоисключающими.</span><span class="sxs-lookup"><span data-stu-id="f75cc-115">This tutorial provides the best of both approaches: check boxes that are mutually exclusive.</span></span>

## <a name="steps"></a><span data-ttu-id="f75cc-116">Шаги</span><span class="sxs-lookup"><span data-stu-id="f75cc-116">Steps</span></span>

<span data-ttu-id="f75cc-117">Набор средств управления ASP.NET AJAX содержит расширитель Мутуаллексклусивечеккбокс.</span><span class="sxs-lookup"><span data-stu-id="f75cc-117">The ASP.NET AJAX Control Toolkit contains the MutuallyExclusiveCheckBox extender.</span></span> <span data-ttu-id="f75cc-118">Это позволяет программистам назначать любой флажок имени группы (`Key` атрибут).</span><span class="sxs-lookup"><span data-stu-id="f75cc-118">This enables programmers to assign any checkbox to a group name (`Key` attribute).</span></span> <span data-ttu-id="f75cc-119">Из всех флажков в одной группе можно выбрать только один из них.</span><span class="sxs-lookup"><span data-stu-id="f75cc-119">From all check boxes within the same group, only one may be selected at one time.</span></span>

<span data-ttu-id="f75cc-120">Начнем с установки двух флажков на новой странице ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="f75cc-120">Let's start with putting two check boxes on a new ASP.NET page.</span></span> <span data-ttu-id="f75cc-121">Для демонстрации принципа может быть больше, но два из них достаточно:</span><span class="sxs-lookup"><span data-stu-id="f75cc-121">There can be more, but two of them suffice to demonstrate the principle:</span></span>

[!code-aspx[Main](creating-mutually-exclusive-checkboxes-vb/samples/sample1.aspx)]

<span data-ttu-id="f75cc-122">Для обоих флажков на странице должен быть размещен элемент управления Мутуаллексклусивечеккбоксекстендер.</span><span class="sxs-lookup"><span data-stu-id="f75cc-122">For both checkboxes, a MutuallyExclusiveCheckBoxExtender control must be put on the page.</span></span> <span data-ttu-id="f75cc-123">Оба ключевых атрибута должны иметь одинаковое значение, так же как атрибуты значений элементов переключателя HTML должны быть идентичны, чтобы обозначить группу, к которой они принадлежат.</span><span class="sxs-lookup"><span data-stu-id="f75cc-123">Both Key attributes need to have the same value, just as the value attributes of HTML radio button elements must be identical to denote the group they belong to.</span></span> <span data-ttu-id="f75cc-124">Свойство TargetControlID расширителя указывает на идентификатор флажка.</span><span class="sxs-lookup"><span data-stu-id="f75cc-124">The TargetControlID property of the extender points to the ID of the check box.</span></span>

[!code-aspx[Main](creating-mutually-exclusive-checkboxes-vb/samples/sample2.aspx)]

<span data-ttu-id="f75cc-125">Наконец, включите ASP.NET AJAX `ScriptManager`, необходимый для всех элементов набора средств управления AJAX ASP.NET:</span><span class="sxs-lookup"><span data-stu-id="f75cc-125">Finally, include the ASP.NET AJAX `ScriptManager` which is required by all elements of the ASP.NET AJAX Control Toolkit:</span></span>

[!code-aspx[Main](creating-mutually-exclusive-checkboxes-vb/samples/sample3.aspx)]

<span data-ttu-id="f75cc-126">Сохраните и запустите страницу. Вы можете установить флажки и снять флажки, однако в этом случае оба флажка не будут установлены.</span><span class="sxs-lookup"><span data-stu-id="f75cc-126">Save and run the page: You can check and uncheck both check boxes, however at no time can both check boxes be checked.</span></span>

<span data-ttu-id="f75cc-127">[![только один флажок можно проверить за раз](creating-mutually-exclusive-checkboxes-vb/_static/image2.png)](creating-mutually-exclusive-checkboxes-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="f75cc-127">[![Only one checkbox can be checked at a time](creating-mutually-exclusive-checkboxes-vb/_static/image2.png)](creating-mutually-exclusive-checkboxes-vb/_static/image1.png)</span></span>

<span data-ttu-id="f75cc-128">Только один флажок может быть проверен за раз ([щелкните, чтобы просмотреть изображение с полным размером](creating-mutually-exclusive-checkboxes-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="f75cc-128">Only one checkbox can be checked at a time ([Click to view full-size image](creating-mutually-exclusive-checkboxes-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="f75cc-129">Назад</span><span class="sxs-lookup"><span data-stu-id="f75cc-129">Previous</span></span>](creating-mutually-exclusive-checkboxes-cs.md)
