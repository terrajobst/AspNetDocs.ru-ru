---
uid: web-forms/videos/how-do-i/how-do-i-persist-the-state-of-a-user-control-during-a-postback
title: '[How Do I]: Persist the State of a User Control During a Postback | Microsoft Docs'
author: rick-anderson
description: В этом видео Крис пикселей показано, как сохранить состояние одного или нескольких объектов в пользовательском элементе управления. Во-первых, создается пользовательский элемент управления, представляющий Абилит...
ms.author: riande
ms.date: 04/02/2009
ms.assetid: d1bca4c6-838c-40f7-87ec-80bb67e483e5
msc.legacyurl: /web-forms/videos/how-do-i/how-do-i-persist-the-state-of-a-user-control-during-a-postback
msc.type: video
ms.openlocfilehash: c87bd6c5c993a1bde8f8a84f6d53b431e54541d9
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78516276"
---
# <a name="how-do-i-persist-the-state-of-a-user-control-during-a-postback"></a><span data-ttu-id="ba082-103">[Инструкции]. Сохранение состояния пользовательского элемента управления во время обратной передачи</span><span class="sxs-lookup"><span data-stu-id="ba082-103">[How Do I]: Persist the State of a User Control During a Postback</span></span>

<span data-ttu-id="ba082-104">от [Крис пикселей](https://twitter.com/chrispels)</span><span class="sxs-lookup"><span data-stu-id="ba082-104">by [Chris Pels](https://twitter.com/chrispels)</span></span>

<span data-ttu-id="ba082-105">В этом видео Крис пикселей показано, как сохранить состояние одного или нескольких объектов в пользовательском элементе управления.</span><span class="sxs-lookup"><span data-stu-id="ba082-105">In this video Chris Pels shows how to persist the state of one or more objects in a user control.</span></span> <span data-ttu-id="ba082-106">Во-первых, создается пользовательский элемент управления, который представляет возможность для пользователя указывать условия фильтра для поиска.</span><span class="sxs-lookup"><span data-stu-id="ba082-106">First, a user control is created that represents the ability for a user to specify filter criteria for a search.</span></span> <span data-ttu-id="ba082-107">Кроме того, для хранения сведений о фильтрах создается сопутствующий класс фильтра.</span><span class="sxs-lookup"><span data-stu-id="ba082-107">In addition, a companion Filter class is created to store the filter information.</span></span> <span data-ttu-id="ba082-108">В элемент управления фильтра добавляются несколько элементов пользовательского интерфейса, а также некоторые методы и свойства для хранения сведений о текущем фильтре в экземпляре класса Filter.</span><span class="sxs-lookup"><span data-stu-id="ba082-108">Several user interface elements are added to the filter control along with some methods and properties to store the current filter information in the Filter class instance.</span></span> <span data-ttu-id="ba082-109">Затем сохраняемость пользовательского элемента управления реализуется с помощью метода Регистеррекуиресконтролстате и связанных методов Save/Restore.</span><span class="sxs-lookup"><span data-stu-id="ba082-109">Next, the user control persistence is implemented using the RegisterRequiresControlState method and associated Save/Restore methods.</span></span> <span data-ttu-id="ba082-110">Эти методы хранят экземпляр класса Filter и его данные во время обратных передач страницы.</span><span class="sxs-lookup"><span data-stu-id="ba082-110">These methods store the instance of the filter class and its data during page postbacks.</span></span> <span data-ttu-id="ba082-111">Наконец, существует обсуждение того, как хранить несколько объектов в реализации состояния элемента управления.</span><span class="sxs-lookup"><span data-stu-id="ba082-111">Finally, there is a discussion of how to store multiple objects in control state implementation.</span></span>

[<span data-ttu-id="ba082-112">&#9654;Смотреть видео (23 минуты)</span><span class="sxs-lookup"><span data-stu-id="ba082-112">&#9654; Watch video (23 minutes)</span></span>](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-persist-the-state-of-a-user-control-during-a-postback)
