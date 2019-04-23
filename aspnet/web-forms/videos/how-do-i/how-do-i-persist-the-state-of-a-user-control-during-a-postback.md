---
uid: web-forms/videos/how-do-i/how-do-i-persist-the-state-of-a-user-control-during-a-postback
title: '[How Do I]: Persist the State of a User Control During a Postback | Microsoft Docs'
author: rick-anderson
description: В этом видео Крис Пелз показан способ сохранения состояния одного или нескольких объектов в пользовательском элементе управления. Во-первых создается пользовательский элемент управления, представляющий слышали...
ms.author: riande
ms.date: 04/02/2009
ms.assetid: d1bca4c6-838c-40f7-87ec-80bb67e483e5
msc.legacyurl: /web-forms/videos/how-do-i/how-do-i-persist-the-state-of-a-user-control-during-a-postback
msc.type: video
ms.openlocfilehash: c87bd6c5c993a1bde8f8a84f6d53b431e54541d9
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/17/2019
ms.locfileid: "59414781"
---
# <a name="how-do-i-persist-the-state-of-a-user-control-during-a-postback"></a>[Инструкции]: Сохранение состояния пользовательского элемента управления во время обратной передачи
[How Do I]: Persist the State of a User Control During a Postback

<span data-ttu-id="5b0a4-104">по [Крис Пелз](https://twitter.com/chrispels)</span><span class="sxs-lookup"><span data-stu-id="5b0a4-104">by [Chris Pels](https://twitter.com/chrispels)</span></span>

<span data-ttu-id="5b0a4-105">В этом видео Крис Пелз показан способ сохранения состояния одного или нескольких объектов в пользовательском элементе управления.</span><span class="sxs-lookup"><span data-stu-id="5b0a4-105">In this video Chris Pels shows how to persist the state of one or more objects in a user control.</span></span> <span data-ttu-id="5b0a4-106">Во-первых создается пользовательский элемент управления, представляющий возможность пользователю указать критерии фильтра поиска.</span><span class="sxs-lookup"><span data-stu-id="5b0a4-106">First, a user control is created that represents the ability for a user to specify filter criteria for a search.</span></span> <span data-ttu-id="5b0a4-107">Кроме того вспомогательное класс фильтра создается для хранения сведений о фильтре.</span><span class="sxs-lookup"><span data-stu-id="5b0a4-107">In addition, a companion Filter class is created to store the filter information.</span></span> <span data-ttu-id="5b0a4-108">Несколько элементов пользовательского интерфейса добавляются в элемент управления фильтра, а также некоторые методы и свойства для хранения текущие данные фильтра в экземпляре класса фильтра.</span><span class="sxs-lookup"><span data-stu-id="5b0a4-108">Several user interface elements are added to the filter control along with some methods and properties to store the current filter information in the Filter class instance.</span></span> <span data-ttu-id="5b0a4-109">Далее сохраняемости пользователя элемента управления реализуется с помощью метода RegisterRequiresControlState и связанные методы сохранить или восстановить.</span><span class="sxs-lookup"><span data-stu-id="5b0a4-109">Next, the user control persistence is implemented using the RegisterRequiresControlState method and associated Save/Restore methods.</span></span> <span data-ttu-id="5b0a4-110">Эти методы хранения экземпляра класса фильтра и его данные во время обратной передачи страницы.</span><span class="sxs-lookup"><span data-stu-id="5b0a4-110">These methods store the instance of the filter class and its data during page postbacks.</span></span> <span data-ttu-id="5b0a4-111">Наконец есть о том, как хранить несколько объектов в реализации состояния элемента управления.</span><span class="sxs-lookup"><span data-stu-id="5b0a4-111">Finally, there is a discussion of how to store multiple objects in control state implementation.</span></span>

[<span data-ttu-id="5b0a4-112">&#9654;Просмотрите видео (23 минуты)</span><span class="sxs-lookup"><span data-stu-id="5b0a4-112">&#9654; Watch video (23 minutes)</span></span>](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-persist-the-state-of-a-user-control-during-a-postback)
