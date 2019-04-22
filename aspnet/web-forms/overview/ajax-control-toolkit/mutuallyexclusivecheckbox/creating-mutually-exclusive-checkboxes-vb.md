---
uid: web-forms/overview/ajax-control-toolkit/mutuallyexclusivecheckbox/creating-mutually-exclusive-checkboxes-vb
title: Создание взаимоисключающих флажков (VB) | Документация Майкрософт
author: wenz
description: 'Когда может быть выбран только один из набора параметров, обычно используются переключателей. Не существует недостаток, но: Один раз одной в группе переключателя...'
ms.author: riande
ms.date: 06/02/2008
ms.assetid: e9dd1d5a-a1db-4114-981d-6a91acb1d709
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/mutuallyexclusivecheckbox/creating-mutually-exclusive-checkboxes-vb
msc.type: authoredcontent
ms.openlocfilehash: 45ea3c3dbcf7816f67081a61230c4b055a90fcf5
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/17/2019
ms.locfileid: "59393630"
---
# <a name="creating-mutually-exclusive-checkboxes-vb"></a><span data-ttu-id="98fa0-104">Создание взаимоисключающих флажков (VB)</span><span class="sxs-lookup"><span data-stu-id="98fa0-104">Creating Mutually Exclusive Checkboxes (VB)</span></span>

<span data-ttu-id="98fa0-105">по [Кристиан Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="98fa0-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="98fa0-106">[Скачать код](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/MutuallyExclusiveCheckBox0.vb.zip) или [скачать PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/mutuallyexclusivecheckbox0VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="98fa0-106">[Download Code](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/MutuallyExclusiveCheckBox0.vb.zip) or [Download PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/mutuallyexclusivecheckbox0VB.pdf)</span></span>

> <span data-ttu-id="98fa0-107">Когда может быть выбран только один из набора параметров, обычно используются переключателей.</span><span class="sxs-lookup"><span data-stu-id="98fa0-107">When only one of a set of options may be selected, radio buttons are usually used.</span></span> <span data-ttu-id="98fa0-108">Не существует недостаток, но: Выбрав один переключатель в группе, не поддерживается снимите флажки всех переключателей.</span><span class="sxs-lookup"><span data-stu-id="98fa0-108">There is a drawback, though: Once one radio button in a group is selected, it is not possible to uncheck all radio buttons.</span></span> <span data-ttu-id="98fa0-109">Флажки, можно снять в любой момент, но не являются взаимоисключающими.</span><span class="sxs-lookup"><span data-stu-id="98fa0-109">Check boxes can be unchecked at any time, however are not mutually exclusive.</span></span> <span data-ttu-id="98fa0-110">В этом руководстве приведены преимущества обоих подходов: флажки, которые являются взаимоисключающими.</span><span class="sxs-lookup"><span data-stu-id="98fa0-110">This tutorial provides the best of both approaches: check boxes that are mutually exclusive.</span></span>


## <a name="overview"></a><span data-ttu-id="98fa0-111">Обзор</span><span class="sxs-lookup"><span data-stu-id="98fa0-111">Overview</span></span>

<span data-ttu-id="98fa0-112">Когда может быть выбран только один из набора параметров, обычно используются переключателей.</span><span class="sxs-lookup"><span data-stu-id="98fa0-112">When only one of a set of options may be selected, radio buttons are usually used.</span></span> <span data-ttu-id="98fa0-113">Не существует недостаток, но: Выбрав один переключатель в группе, не поддерживается снимите флажки всех переключателей.</span><span class="sxs-lookup"><span data-stu-id="98fa0-113">There is a drawback, though: Once one radio button in a group is selected, it is not possible to uncheck all radio buttons.</span></span> <span data-ttu-id="98fa0-114">Флажки, можно снять в любой момент, но не являются взаимоисключающими.</span><span class="sxs-lookup"><span data-stu-id="98fa0-114">Check boxes can be unchecked at any time, however are not mutually exclusive.</span></span> <span data-ttu-id="98fa0-115">В этом руководстве приведены преимущества обоих подходов: флажки, которые являются взаимоисключающими.</span><span class="sxs-lookup"><span data-stu-id="98fa0-115">This tutorial provides the best of both approaches: check boxes that are mutually exclusive.</span></span>

## <a name="steps"></a><span data-ttu-id="98fa0-116">Шаги</span><span class="sxs-lookup"><span data-stu-id="98fa0-116">Steps</span></span>

<span data-ttu-id="98fa0-117">ASP.NET AJAX Control Toolkit содержит расширения MutuallyExclusiveCheckBox.</span><span class="sxs-lookup"><span data-stu-id="98fa0-117">The ASP.NET AJAX Control Toolkit contains the MutuallyExclusiveCheckBox extender.</span></span> <span data-ttu-id="98fa0-118">Это дает возможность программистам назначить любой checkbox с именем группы (`Key` атрибут).</span><span class="sxs-lookup"><span data-stu-id="98fa0-118">This enables programmers to assign any checkbox to a group name (`Key` attribute).</span></span> <span data-ttu-id="98fa0-119">Все флажки в той же группе может одновременно выбрать только один.</span><span class="sxs-lookup"><span data-stu-id="98fa0-119">From all check boxes within the same group, only one may be selected at one time.</span></span>

<span data-ttu-id="98fa0-120">Давайте начнем с размещением два флажка на новой странице ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="98fa0-120">Let's start with putting two check boxes on a new ASP.NET page.</span></span> <span data-ttu-id="98fa0-121">Может существовать несколько, но два из них достаточно для демонстрации принципа:</span><span class="sxs-lookup"><span data-stu-id="98fa0-121">There can be more, but two of them suffice to demonstrate the principle:</span></span>

[!code-aspx[Main](creating-mutually-exclusive-checkboxes-vb/samples/sample1.aspx)]

<span data-ttu-id="98fa0-122">Для оба флажка элемент управления MutuallyExclusiveCheckBoxExtender должны быть размещены на странице.</span><span class="sxs-lookup"><span data-stu-id="98fa0-122">For both checkboxes, a MutuallyExclusiveCheckBoxExtender control must be put on the page.</span></span> <span data-ttu-id="98fa0-123">Оба ключевые атрибуты должны иметь одинаковое значение, так же, как значение, которое атрибутов кнопку radio HTML-элементов должны совпадать для обозначения группы, которым они принадлежат.</span><span class="sxs-lookup"><span data-stu-id="98fa0-123">Both Key attributes need to have the same value, just as the value attributes of HTML radio button elements must be identical to denote the group they belong to.</span></span> <span data-ttu-id="98fa0-124">Свойство TargetControlID расширителя указывает на идентификатор поля с флажком.</span><span class="sxs-lookup"><span data-stu-id="98fa0-124">The TargetControlID property of the extender points to the ID of the check box.</span></span>

[!code-aspx[Main](creating-mutually-exclusive-checkboxes-vb/samples/sample2.aspx)]

<span data-ttu-id="98fa0-125">Наконец, включите ASP.NET AJAX `ScriptManager` которая необходима для всех элементов ASP.NET AJAX Control Toolkit:</span><span class="sxs-lookup"><span data-stu-id="98fa0-125">Finally, include the ASP.NET AJAX `ScriptManager` which is required by all elements of the ASP.NET AJAX Control Toolkit:</span></span>

[!code-aspx[Main](creating-mutually-exclusive-checkboxes-vb/samples/sample3.aspx)]

<span data-ttu-id="98fa0-126">Сохранить и запустить эту страницу: Можно проверить и снимите оба флажка, но никогда не установлены оба флажка нельзя.</span><span class="sxs-lookup"><span data-stu-id="98fa0-126">Save and run the page: You can check and uncheck both check boxes, however at no time can both check boxes be checked.</span></span>


<span data-ttu-id="98fa0-127">[![Одновременно можно проверить только один флажок](creating-mutually-exclusive-checkboxes-vb/_static/image2.png)](creating-mutually-exclusive-checkboxes-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="98fa0-127">[![Only one checkbox can be checked at a time](creating-mutually-exclusive-checkboxes-vb/_static/image2.png)](creating-mutually-exclusive-checkboxes-vb/_static/image1.png)</span></span>

<span data-ttu-id="98fa0-128">Одновременно можно проверить только один флажок ([Просмотр полноразмерного изображения](creating-mutually-exclusive-checkboxes-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="98fa0-128">Only one checkbox can be checked at a time ([Click to view full-size image](creating-mutually-exclusive-checkboxes-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="98fa0-129">Назад</span><span class="sxs-lookup"><span data-stu-id="98fa0-129">Previous</span></span>](creating-mutually-exclusive-checkboxes-cs.md)
