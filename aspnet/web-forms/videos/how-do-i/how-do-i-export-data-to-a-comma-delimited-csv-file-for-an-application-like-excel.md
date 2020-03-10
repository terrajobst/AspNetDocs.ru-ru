---
uid: web-forms/videos/how-do-i/how-do-i-export-data-to-a-comma-delimited-csv-file-for-an-application-like-excel
title: '[Инструкции:] Экспорт данных в файл с разделителями-запятыми (CSV) для приложения, например Excel | Документация Майкрософт'
author: rick-anderson
description: В этом видеоролике Крис пикселей показано, как взять данные из базы данных или другого источника и экспортировать их в файл с разделителями-запятыми, который можно использовать в приложении Li...
ms.author: riande
ms.date: 01/22/2009
ms.assetid: c9df86ad-aec2-43d5-bb8a-413ebb666673
msc.legacyurl: /web-forms/videos/how-do-i/how-do-i-export-data-to-a-comma-delimited-csv-file-for-an-application-like-excel
msc.type: video
ms.openlocfilehash: f27873eee345fe5347023b154de2b3833c9b6138
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78458070"
---
# <a name="how-do-i-export-data-to-a-comma-delimited-csv-file-for-an-application-like-excel"></a><span data-ttu-id="2be02-103">[Инструкции:] Экспорт данных в файл с разделителями-запятыми (CSV) для приложения, например Excel</span><span class="sxs-lookup"><span data-stu-id="2be02-103">[How Do I:] Export Data to a Comma Delimited (CSV) File for an Application Like Excel</span></span>

<span data-ttu-id="2be02-104">от [Крис пикселей](https://twitter.com/chrispels)</span><span class="sxs-lookup"><span data-stu-id="2be02-104">by [Chris Pels](https://twitter.com/chrispels)</span></span>

<span data-ttu-id="2be02-105">В этом видеоролике Крис пикселей показано, как взять данные из базы данных или другого источника и экспортировать их в файл с разделителями-запятыми, который можно использовать в приложении, например Excel.</span><span class="sxs-lookup"><span data-stu-id="2be02-105">In this video Chris Pels shows how to take data from a database or other source and export it to a comma delimited file that can be used in an application like Excel.</span></span> <span data-ttu-id="2be02-106">Во-первых, набор данных создается как объект DataTable.</span><span class="sxs-lookup"><span data-stu-id="2be02-106">First, a set of data is created as a DataTable object.</span></span> <span data-ttu-id="2be02-107">После этого ответ на текущий запрос веб-страницы удаляется, а заголовок и тип содержимого настраиваются как CSV-файл.</span><span class="sxs-lookup"><span data-stu-id="2be02-107">Next, the Response for the current web page request is cleared and the header and content type are configured to be a csv file.</span></span> <span data-ttu-id="2be02-108">Затем фактические данные добавляются в поток ответа путем первой записи заголовков столбцов для CSV-файла, за которым следуют значения данных.</span><span class="sxs-lookup"><span data-stu-id="2be02-108">Then the actual data is added to the response stream by first writing the column headers for the csv file followed by the data values.</span></span> <span data-ttu-id="2be02-109">Этот подход может быть полезен, если пользователям требуется экспортировать данные, чтобы их можно было использовать локально в таких программах, как Excel.</span><span class="sxs-lookup"><span data-stu-id="2be02-109">This approach can be useful when users require an export of data so it can be manipulated locally in a program like Excel.</span></span>

[<span data-ttu-id="2be02-110">&#9654;Смотреть видео (19 минут)</span><span class="sxs-lookup"><span data-stu-id="2be02-110">&#9654; Watch video (19 minutes)</span></span>](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-export-data-to-a-comma-delimited-csv-file-for-an-application-like-excel)
