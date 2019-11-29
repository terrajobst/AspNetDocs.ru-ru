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
ms.openlocfilehash: 0e720b3e4c5d3b8f779afe3a6e2b47baa86eec4c
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/28/2019
ms.locfileid: "74592709"
---
# <a name="building-the-chapter-downloads-for-the-ef-5-mvc-4-tutorials"></a><span data-ttu-id="0dd5b-103">Создание загружаемых материалов для разделов руководства по EF 5 MVC 4</span><span class="sxs-lookup"><span data-stu-id="0dd5b-103">Building the Chapter Downloads for the EF 5 MVC 4 Tutorials</span></span>

<span data-ttu-id="0dd5b-104">по [Рик Андерсон (]((https://twitter.com/RickAndMSFT))</span><span class="sxs-lookup"><span data-stu-id="0dd5b-104">by [Rick Anderson]((https://twitter.com/RickAndMSFT))</span></span>

[<span data-ttu-id="0dd5b-105">Скачать завершенный проект</span><span class="sxs-lookup"><span data-stu-id="0dd5b-105">Download Completed Project</span></span>](https://code.msdn.microsoft.com/Getting-Started-with-dd0e2ed8)

> <span data-ttu-id="0dd5b-106">Пример веб-приложения Contoso университета демонстрирует создание приложений ASP.NET MVC 4 с помощью Entity Framework 5 Code First и Visual Studio 2012.</span><span class="sxs-lookup"><span data-stu-id="0dd5b-106">The Contoso University sample web application demonstrates how to create ASP.NET MVC 4 applications using the Entity Framework 5 Code First and Visual Studio 2012.</span></span> <span data-ttu-id="0dd5b-107">Сведения о серии руководств см. в [первом руководстве серии](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span><span class="sxs-lookup"><span data-stu-id="0dd5b-107">For information about the tutorial series, see [the first tutorial in the series](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span></span>

## <a name="building-the-chapter-downloads"></a><span data-ttu-id="0dd5b-108">Создание загрузок для глав</span><span class="sxs-lookup"><span data-stu-id="0dd5b-108">Building the Chapter Downloads</span></span>

1. <span data-ttu-id="0dd5b-109">Скачайте и распакуйте пример ZIP-файла проекта.</span><span class="sxs-lookup"><span data-stu-id="0dd5b-109">Download and unzip the  project sample zip file.</span></span> <span data-ttu-id="0dd5b-110">В распакованном пакете загрузки вы найдете дополнительные ZIP-файлы, по одной для завершения каждой главы.</span><span class="sxs-lookup"><span data-stu-id="0dd5b-110">In the unzipped download package, you will find additional zip files, one for the completion of each chapter.</span></span>
2. <span data-ttu-id="0dd5b-111">Щелкните правой кнопкой мыши нужный ZIP-файл, выберите пункт **Свойства**и нажмите кнопку **разблокировать** .</span><span class="sxs-lookup"><span data-stu-id="0dd5b-111">Right click on the desired zip file, click **Properties**, and click the **Unblock** button.</span></span>  
  
    ![](building-the-ef5-mvc4-chapter-downloads/_static/image1.png)
3. <span data-ttu-id="0dd5b-112">Распакуйте файл.</span><span class="sxs-lookup"><span data-stu-id="0dd5b-112">Unzip the file.</span></span>
4. <span data-ttu-id="0dd5b-113">Дважды щелкните файл *Кукс. sln* , чтобы запустить Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0dd5b-113">Double-click the *CUx.sln* file to launch Visual Studio.</span></span>
5. <span data-ttu-id="0dd5b-114">В меню **Сервис** выберите **Диспетчер пакетов NuGet**, а затем — **консоль диспетчера пакетов**.</span><span class="sxs-lookup"><span data-stu-id="0dd5b-114">From the **Tools** menu, click **NuGet Package Manager**, then **Package Manager Console**.</span></span>  
  
    ![](building-the-ef5-mvc4-chapter-downloads/_static/image2.png)
6. <span data-ttu-id="0dd5b-115">В консоли диспетчера пакетов (PMC) нажмите кнопку **восстановить**.</span><span class="sxs-lookup"><span data-stu-id="0dd5b-115">In the Package Manager Console (PMC), click **Restore**.</span></span>  
  
    ![](building-the-ef5-mvc4-chapter-downloads/_static/image3.png)
7. <span data-ttu-id="0dd5b-116">Закройте Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0dd5b-116">Exit Visual Studio.</span></span>
8. <span data-ttu-id="0dd5b-117">Перезапустите Visual Studio, открыв файл решения, который вы закрыли на предыдущем шаге.</span><span class="sxs-lookup"><span data-stu-id="0dd5b-117">Restart Visual Studio, opening the solution file you closed in the step above.</span></span>
9. <span data-ttu-id="0dd5b-118">В консоли диспетчера пакетов (PMC) введите команду `Update-Database`:</span><span class="sxs-lookup"><span data-stu-id="0dd5b-118">In the Package Manager Console (PMC), enter the `Update-Database` command:</span></span>  
  
    ![](building-the-ef5-mvc4-chapter-downloads/_static/image4.png)  

    > [!NOTE]
    > <span data-ttu-id="0dd5b-119">При возникновении следующей ошибки:</span><span class="sxs-lookup"><span data-stu-id="0dd5b-119">If you get the following error:</span></span>  
    >   
    >  <span data-ttu-id="0dd5b-120">*Термин "обновление базы данных" не распознается как имя командлета, функции, файла сценария или исполняемой программы. Проверьте правильность написания имени или, если путь включен, проверьте правильность пути и повторите попытку.*</span><span class="sxs-lookup"><span data-stu-id="0dd5b-120">*The term 'Update-Database' is not recognized as the name of a cmdlet, function, script file, or operable program. Check the spelling of the name, or if a path was included, verify that the path is correct and try again.*</span></span>  
    > <span data-ttu-id="0dd5b-121">Закройте и перезапустите Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0dd5b-121">Exit and restart Visual Studio.</span></span>

    <span data-ttu-id="0dd5b-122">При каждом выполнении миграции будет запущен метод SEED.</span><span class="sxs-lookup"><span data-stu-id="0dd5b-122">Each migration will run, then the seed method will run.</span></span> <span data-ttu-id="0dd5b-123">Теперь можно запустить приложение.</span><span class="sxs-lookup"><span data-stu-id="0dd5b-123">You can now run the app.</span></span>

    ![](building-the-ef5-mvc4-chapter-downloads/_static/image5.png)

> [!div class="step-by-step"]
> [<span data-ttu-id="0dd5b-124">Назад</span><span class="sxs-lookup"><span data-stu-id="0dd5b-124">Previous</span></span>](advanced-entity-framework-scenarios-for-an-mvc-web-application.md)
