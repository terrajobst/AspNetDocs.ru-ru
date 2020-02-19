---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/building-the-ef5-mvc4-chapter-downloads
title: Создание загружаемых материалов для учебников по EF 5 для MVC 4 | Документация Майкрософт
author: Rick-Anderson
description: Пример веб-приложения Contoso университета демонстрирует создание приложений ASP.NET MVC 4 с помощью Entity Framework 5 Code First и Visual Studio...
ms.author: riande
ms.date: 07/30/2013
ms.assetid: d0a89089-eed8-4f61-a478-c5ffa30186f5
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/building-the-ef5-mvc4-chapter-downloads
msc.type: authoredcontent
ms.openlocfilehash: 10237af40e3914b65e5181f17555697e86adea4b
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457860"
---
# <a name="building-the-chapter-downloads-for-the-ef-5-mvc-4-tutorials"></a><span data-ttu-id="378c3-103">Создание загружаемых материалов для разделов руководства по EF 5 MVC 4</span><span class="sxs-lookup"><span data-stu-id="378c3-103">Building the Chapter Downloads for the EF 5 MVC 4 Tutorials</span></span>

<span data-ttu-id="378c3-104">по [Рик Андерсон (](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="378c3-104">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

[<span data-ttu-id="378c3-105">Скачать завершенный проект</span><span class="sxs-lookup"><span data-stu-id="378c3-105">Download Completed Project</span></span>](https://code.msdn.microsoft.com/Getting-Started-with-dd0e2ed8)

> <span data-ttu-id="378c3-106">Пример веб-приложения Contoso университета демонстрирует создание приложений ASP.NET MVC 4 с помощью Entity Framework 5 Code First и Visual Studio 2012.</span><span class="sxs-lookup"><span data-stu-id="378c3-106">The Contoso University sample web application demonstrates how to create ASP.NET MVC 4 applications using the Entity Framework 5 Code First and Visual Studio 2012.</span></span> <span data-ttu-id="378c3-107">Сведения о серии руководств см. в [первом руководстве серии](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span><span class="sxs-lookup"><span data-stu-id="378c3-107">For information about the tutorial series, see [the first tutorial in the series](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span></span>

## <a name="building-the-chapter-downloads"></a><span data-ttu-id="378c3-108">Создание загрузок для глав</span><span class="sxs-lookup"><span data-stu-id="378c3-108">Building the Chapter Downloads</span></span>

1. <span data-ttu-id="378c3-109">Скачайте и распакуйте пример ZIP-файла проекта.</span><span class="sxs-lookup"><span data-stu-id="378c3-109">Download and unzip the  project sample zip file.</span></span> <span data-ttu-id="378c3-110">В распакованном пакете загрузки вы найдете дополнительные ZIP-файлы, по одной для завершения каждой главы.</span><span class="sxs-lookup"><span data-stu-id="378c3-110">In the unzipped download package, you will find additional zip files, one for the completion of each chapter.</span></span>
2. <span data-ttu-id="378c3-111">Щелкните правой кнопкой мыши нужный ZIP-файл, выберите пункт **Свойства**и нажмите кнопку **разблокировать** .</span><span class="sxs-lookup"><span data-stu-id="378c3-111">Right click on the desired zip file, click **Properties**, and click the **Unblock** button.</span></span>  
  
    ![](building-the-ef5-mvc4-chapter-downloads/_static/image1.png)
3. <span data-ttu-id="378c3-112">Распакуйте файл.</span><span class="sxs-lookup"><span data-stu-id="378c3-112">Unzip the file.</span></span>
4. <span data-ttu-id="378c3-113">Дважды щелкните файл *Кукс. sln* , чтобы запустить Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="378c3-113">Double-click the *CUx.sln* file to launch Visual Studio.</span></span>
5. <span data-ttu-id="378c3-114">В меню **Сервис** выберите **Диспетчер пакетов NuGet**, а затем — **консоль диспетчера пакетов**.</span><span class="sxs-lookup"><span data-stu-id="378c3-114">From the **Tools** menu, click **NuGet Package Manager**, then **Package Manager Console**.</span></span>  
  
    ![](building-the-ef5-mvc4-chapter-downloads/_static/image2.png)
6. <span data-ttu-id="378c3-115">В консоли диспетчера пакетов (PMC) нажмите кнопку **восстановить**.</span><span class="sxs-lookup"><span data-stu-id="378c3-115">In the Package Manager Console (PMC), click **Restore**.</span></span>  
  
    ![](building-the-ef5-mvc4-chapter-downloads/_static/image3.png)
7. <span data-ttu-id="378c3-116">Закройте Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="378c3-116">Exit Visual Studio.</span></span>
8. <span data-ttu-id="378c3-117">Перезапустите Visual Studio, открыв файл решения, который вы закрыли на предыдущем шаге.</span><span class="sxs-lookup"><span data-stu-id="378c3-117">Restart Visual Studio, opening the solution file you closed in the step above.</span></span>
9. <span data-ttu-id="378c3-118">В консоли диспетчера пакетов (PMC) введите команду `Update-Database`:</span><span class="sxs-lookup"><span data-stu-id="378c3-118">In the Package Manager Console (PMC), enter the `Update-Database` command:</span></span>  
  
    ![](building-the-ef5-mvc4-chapter-downloads/_static/image4.png)  

    > [!NOTE]
    > <span data-ttu-id="378c3-119">Если возникает следующее сообщение об ошибке:</span><span class="sxs-lookup"><span data-stu-id="378c3-119">If you get the following error:</span></span>  
    >   
    >  <span data-ttu-id="378c3-120">*Термин "обновление базы данных" не распознается как имя командлета, функции, файла сценария или исполняемой программы. Проверьте правильность написания имени или, если путь включен, проверьте правильность пути и повторите попытку.*</span><span class="sxs-lookup"><span data-stu-id="378c3-120">*The term 'Update-Database' is not recognized as the name of a cmdlet, function, script file, or operable program. Check the spelling of the name, or if a path was included, verify that the path is correct and try again.*</span></span>  
    > <span data-ttu-id="378c3-121">Закройте и перезапустите Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="378c3-121">Exit and restart Visual Studio.</span></span>

    <span data-ttu-id="378c3-122">При каждом выполнении миграции будет запущен метод SEED.</span><span class="sxs-lookup"><span data-stu-id="378c3-122">Each migration will run, then the seed method will run.</span></span> <span data-ttu-id="378c3-123">Теперь можно запустить приложение.</span><span class="sxs-lookup"><span data-stu-id="378c3-123">You can now run the app.</span></span>

    ![](building-the-ef5-mvc4-chapter-downloads/_static/image5.png)

> [!div class="step-by-step"]
> [<span data-ttu-id="378c3-124">Назад</span><span class="sxs-lookup"><span data-stu-id="378c3-124">Previous</span></span>](advanced-entity-framework-scenarios-for-an-mvc-web-application.md)
