---
uid: aspnet/web-pages/overview/getting-started/program-asp-net-web-pages-in-visual-studio
title: Программирование веб-страницы ASP.NET (Razor) с помощью Visual Studio | Документация Майкрософт
author: Rick-Anderson
description: В этом приложении объясняется, как можно использовать Visual Studio 2010 или Visual Web Developer 2010 Express для программирования веб-страницы ASP.NET с синтаксис Razor.
ms.author: riande
ms.date: 02/13/2014
ms.assetid: 0acfec5a-48f2-4766-a801-a0f426966f0a
msc.legacyurl: /web-pages/overview/getting-started/program-asp-net-web-pages-in-visual-studio
msc.type: authoredcontent
ms.openlocfilehash: 1a76098779d05912bf7bdf2de5fdce024770752c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78514296"
---
# <a name="programming-aspnet-web-pages-razor-using-visual-studio"></a><span data-ttu-id="175b9-103">Программирование веб-страницы ASP.NET (Razor) с помощью Visual Studio</span><span class="sxs-lookup"><span data-stu-id="175b9-103">Programming ASP.NET Web Pages (Razor) Using Visual Studio</span></span>

<span data-ttu-id="175b9-104">от [Tom фитзмаккен](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="175b9-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="175b9-105">В этой статье объясняется, как можно использовать Visual Studio или Visual Web Developer Express для программирования веб-сайтов веб-страницы ASP.NET (Razor).</span><span class="sxs-lookup"><span data-stu-id="175b9-105">This article explains how you can use Visual Studio or Visual Web Developer Express to program ASP.NET Web Pages (Razor) websites.</span></span>
>
> <span data-ttu-id="175b9-106">Что вы узнаете</span><span class="sxs-lookup"><span data-stu-id="175b9-106">What you'll learn</span></span>
>
> - <span data-ttu-id="175b9-107">Что необходимо установить (если что-либо) для работы с веб-страницы ASP.NET в вашей версии Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="175b9-107">What you need to install (if anything) to work with ASP.NET Web Pages in your version of Visual Studio.</span></span>
> - <span data-ttu-id="175b9-108">Как добавить поддержку для веб-страницы ASP.NET в Visual Web Developer 2010 Express.</span><span class="sxs-lookup"><span data-stu-id="175b9-108">How to add support for ASP.NET Web Pages to Visual Web Developer 2010 Express.</span></span>
> - <span data-ttu-id="175b9-109">Использование функций в Visual Studio для работы с ASP.NET Razor Pages, включая IntelliSense и отладчик.</span><span class="sxs-lookup"><span data-stu-id="175b9-109">How to use features in Visual Studio to work with ASP.NET Razor pages, including IntelliSense and the debugger.</span></span>
>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="175b9-110">Версии программного обеспечения, используемые в этом руководстве</span><span class="sxs-lookup"><span data-stu-id="175b9-110">Software versions used in the tutorial</span></span>
>
>
> - <span data-ttu-id="175b9-111">Веб-страницы ASP.NET (Razor) 3</span><span class="sxs-lookup"><span data-stu-id="175b9-111">ASP.NET Web Pages (Razor) 3</span></span>
> - <span data-ttu-id="175b9-112">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="175b9-112">Visual Studio 2013</span></span>
> - <span data-ttu-id="175b9-113">WebMatrix 3</span><span class="sxs-lookup"><span data-stu-id="175b9-113">WebMatrix 3</span></span>
>
>
> <span data-ttu-id="175b9-114">Этот учебник также работает с веб-страницы ASP.NET 2, Visual Studio 2012, Visual Studio 2010 и WebMatrix 2.</span><span class="sxs-lookup"><span data-stu-id="175b9-114">This tutorial also works with ASP.NET Web Pages 2, Visual Studio 2012, Visual Studio 2010, and WebMatrix 2.</span></span>

<span data-ttu-id="175b9-115">ASP.NET веб-страницы можно программировать с помощью синтаксис Razor WebMatrix или многих других редакторов кода.</span><span class="sxs-lookup"><span data-stu-id="175b9-115">You can program ASP.NET Web pages with Razor syntax using WebMatrix or many other code editors.</span></span> <span data-ttu-id="175b9-116">Вы также можете использовать Microsoft Visual Studio, который является полнофункциональной интегрированной средой разработки (IDE), предоставляющей мощный набор средств для создания различных типов приложений (не только для веб-сайтов).</span><span class="sxs-lookup"><span data-stu-id="175b9-116">You can also use Microsoft Visual Studio which is a full-featured integrated development environment (IDE) that provides a powerful set of tools for creating many types of applications (not just websites).</span></span> <span data-ttu-id="175b9-117">Для работы с ASP.NET Razor Pages можно использовать [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017).</span><span class="sxs-lookup"><span data-stu-id="175b9-117">To work with ASP.NET Razor pages, you can use [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017).</span></span>

<span data-ttu-id="175b9-118">В Visual Studio есть две полезные функции для программирования с ASP.NET Razor Web Pages:</span><span class="sxs-lookup"><span data-stu-id="175b9-118">Two particularly useful features that Visual Studio provides for programming with ASP.NET Razor web pages are:</span></span>

- <span data-ttu-id="175b9-119">*Технология IntelliSense*.</span><span class="sxs-lookup"><span data-stu-id="175b9-119">*IntelliSense*.</span></span> <span data-ttu-id="175b9-120">Функция IntelliSense, встроенная в Visual Studio, является более всеобъемлющей, чем IntelliSense в WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="175b9-120">The IntelliSense feature built into Visual Studio is more comprehensive than IntelliSense in WebMatrix.</span></span>
- <span data-ttu-id="175b9-121">*Отладчик*.</span><span class="sxs-lookup"><span data-stu-id="175b9-121">*Debugger*.</span></span> <span data-ttu-id="175b9-122">Отладчик позволяет устранять неполадки в коде путем остановки программы во время ее выполнения, проверки переменных и пошагового выполнения кода по строке.</span><span class="sxs-lookup"><span data-stu-id="175b9-122">The debugger lets you troubleshoot your code by stopping a program while it's running, examining variables, and stepping through the code line by line.</span></span>

## <a name="using-visual-studio-with-different-versions-of-aspnet-web-pages"></a><span data-ttu-id="175b9-123">Использование Visual Studio с разными версиями веб-страницы ASP.NET</span><span class="sxs-lookup"><span data-stu-id="175b9-123">Using Visual Studio with Different Versions of ASP.NET Web Pages</span></span>

<span data-ttu-id="175b9-124">Для разработки веб-приложений ASP.NET в Visual Studio 2017 установите рабочую нагрузку **ASP.NET и веб-разработку** .</span><span class="sxs-lookup"><span data-stu-id="175b9-124">To develop ASP.NET web apps in Visual Studio 2017, install the **ASP.NET and web development** workload.</span></span>

<span data-ttu-id="175b9-125">Visual Studio 2012 и Visual Studio 2013 включают поддержку веб-страницы ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="175b9-125">Visual Studio 2012 and Visual Studio 2013 include support for ASP.NET Web Pages.</span></span> <span data-ttu-id="175b9-126">(Пакеты, необходимые для поддержки веб-страницы ASP.NET, устанавливаются при установке Visual Studio.)</span><span class="sxs-lookup"><span data-stu-id="175b9-126">(The packages that are required in order to support ASP.NET Web Pages are installed when you install Visual Studio.)</span></span>

<span data-ttu-id="175b9-127">Visual Studio 2010 не включает поддержку по умолчанию для веб-страницы ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="175b9-127">Visual Studio 2010 does not include support by default for ASP.NET Web Pages.</span></span> <span data-ttu-id="175b9-128">Чтобы использовать веб-страницы ASP.NET с Visual Studio 2010, необходимо установить пакет MVC ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="175b9-128">To use ASP.NET Web Pages with Visual Studio 2010, you must install the ASP.NET MVC package.</span></span> <span data-ttu-id="175b9-129">Чтобы получить веб-страницы ASP.NET 2, установите ASP.NET MVC 4.</span><span class="sxs-lookup"><span data-stu-id="175b9-129">To get ASP.NET Web Pages 2, you install ASP.NET MVC 4.</span></span>

<span data-ttu-id="175b9-130">В следующей таблице приведены сведения о поддержке веб-страницы ASP.NET в различных версиях Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="175b9-130">The following table summarizes the support for ASP.NET Web Pages in different versions of Visual Studio.</span></span>

|  | <span data-ttu-id="175b9-131">Visual Studio 2010</span><span class="sxs-lookup"><span data-stu-id="175b9-131">Visual Studio 2010</span></span> | <span data-ttu-id="175b9-132">Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="175b9-132">Visual Studio 2012</span></span> | <span data-ttu-id="175b9-133">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="175b9-133">Visual Studio 2013</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="175b9-134">**Веб-страницы ASP.NET 2**</span><span class="sxs-lookup"><span data-stu-id="175b9-134">**ASP.NET Web Pages 2**</span></span> | <span data-ttu-id="175b9-135">Установка ASP.NET MVC 4</span><span class="sxs-lookup"><span data-stu-id="175b9-135">Install ASP.NET MVC 4</span></span> | <span data-ttu-id="175b9-136">Включает</span><span class="sxs-lookup"><span data-stu-id="175b9-136">(Included)</span></span> | <span data-ttu-id="175b9-137">Включает</span><span class="sxs-lookup"><span data-stu-id="175b9-137">(Included)</span></span> |
| <span data-ttu-id="175b9-138">**Веб-страницы ASP.NET 3**</span><span class="sxs-lookup"><span data-stu-id="175b9-138">**ASP.NET Web Pages 3**</span></span> |  | <span data-ttu-id="175b9-139">Обновление до веб-страницы ASP.NET 3 через NuGet</span><span class="sxs-lookup"><span data-stu-id="175b9-139">Update to ASP.NET Web Pages 3 through NuGet</span></span> | <span data-ttu-id="175b9-140">Включает</span><span class="sxs-lookup"><span data-stu-id="175b9-140">(Included)</span></span> |

<span data-ttu-id="175b9-141">Сведения о работе с Visual Studio 2010 см. [в разделе Установка поддержки для веб-страницы ASP.NET в Visual studio 2010](#vs2010support).</span><span class="sxs-lookup"><span data-stu-id="175b9-141">To work with Visual Studio 2010, see [Installing Support for ASP.NET Web Pages in Visual Studio 2010](#vs2010support).</span></span>

## <a name="launching-visual-studio-from-webmatrix"></a><span data-ttu-id="175b9-142">Запуск Visual Studio из WebMatrix</span><span class="sxs-lookup"><span data-stu-id="175b9-142">Launching Visual Studio from WebMatrix</span></span>

<span data-ttu-id="175b9-143">Если вы запустили проект в WebMatrix и хотите переключиться на Visual Studio, WebMatrix предоставляет кнопку для простого открытия проекта в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="175b9-143">If you have started a project in WebMatrix and want to switch to Visual Studio, WebMatrix provides a button to easily open the project in Visual Studio.</span></span> <span data-ttu-id="175b9-144">Чтобы эта кнопка была доступна, на компьютере должна быть установлена Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="175b9-144">You must have Visual Studio installed on your computer for this button to be enabled.</span></span> <span data-ttu-id="175b9-145">На следующем рисунке показана кнопка в WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="175b9-145">The following image shows the button in WebMatrix.</span></span>

![Запуск Visual Studio](program-asp-net-web-pages-in-visual-studio/_static/image1.png)

<span data-ttu-id="175b9-147">При нажатии кнопки проект открывается в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="175b9-147">When you click the button, the project is opened in Visual Studio.</span></span> <span data-ttu-id="175b9-148">Вы можете переключаться между WebMatrix и Visual Studio без каких бы то ни было проблем.</span><span class="sxs-lookup"><span data-stu-id="175b9-148">You can switch back and forth between WebMatrix and Visual Studio without any problems.</span></span> <span data-ttu-id="175b9-149">Вы получите уведомления, если какие бы то ни было изменения в другой среде, и необходимо перезагрузить их для получения последних изменений.</span><span class="sxs-lookup"><span data-stu-id="175b9-149">You will be notified if any files have changed in the other environment and need to be reloaded to get the latest changes.</span></span>

## <a name="creating-aspnet-razor-site-in-visual-studio"></a><span data-ttu-id="175b9-150">Создание сайта ASP.NET Razor в Visual Studio</span><span class="sxs-lookup"><span data-stu-id="175b9-150">Creating ASP.NET Razor Site in Visual Studio</span></span>

<span data-ttu-id="175b9-151">Чтобы создать веб-сайт ASP.NET Razor в Visual Studio, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="175b9-151">To create an ASP.NET Razor website in Visual Studio:</span></span>

1. <span data-ttu-id="175b9-152">Запустите Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="175b9-152">Open Visual Studio.</span></span>
2. <span data-ttu-id="175b9-153">В меню **файл** выберите пункт **создать веб-сайт**.</span><span class="sxs-lookup"><span data-stu-id="175b9-153">In the **File** menu, click **New Web Site**.</span></span>

    ![создать новый веб-сайт](program-asp-net-web-pages-in-visual-studio/_static/image2.png)
3. <span data-ttu-id="175b9-155">В диалоговом окне **новый веб-сайт** выберите используемый язык (визуальный C# или Visual Basic).</span><span class="sxs-lookup"><span data-stu-id="175b9-155">In the **New Web Site** dialog box, select the language to use (Visual C# or Visual Basic).</span></span>
4. <span data-ttu-id="175b9-156">Выберите шаблон **веб-сайт ASP.NET (Razor)** .</span><span class="sxs-lookup"><span data-stu-id="175b9-156">Select the **ASP.NET Web Site (Razor)** template.</span></span>

    ![сайт Razor](program-asp-net-web-pages-in-visual-studio/_static/image3.png)
5. <span data-ttu-id="175b9-158">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="175b9-158">Click **OK**.</span></span>

<span data-ttu-id="175b9-159">Новый проект существует и заполняется веб-страницами по умолчанию, которые помогут приступить к работе.</span><span class="sxs-lookup"><span data-stu-id="175b9-159">Your new project exists and is populated with some default web pages to help you get started.</span></span>

### <a name="using-intellisense"></a><span data-ttu-id="175b9-160">Using IntelliSense</span><span class="sxs-lookup"><span data-stu-id="175b9-160">Using IntelliSense</span></span>

<span data-ttu-id="175b9-161">Теперь, когда вы создали сайт, можно увидеть, как IntelliSense работает в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="175b9-161">Now that you've created a site, you can see how IntelliSense works in Visual Studio.</span></span>

1. <span data-ttu-id="175b9-162">На веб-сайте, который вы только что создали, откройте страницу *Default. cshtml* .</span><span class="sxs-lookup"><span data-stu-id="175b9-162">In the website you just created, open the *Default.cshtml* page.</span></span>
2. <span data-ttu-id="175b9-163">После тегов `<h3>` на странице введите `@ServerInfo.` (включая точку).</span><span class="sxs-lookup"><span data-stu-id="175b9-163">After the `<h3>` tags in the page, type `@ServerInfo.` (including the dot).</span></span> <span data-ttu-id="175b9-164">Обратите внимание, как IntelliSense отображает доступные методы для модуля поддержки `ServerInfo` в раскрывающемся списке.</span><span class="sxs-lookup"><span data-stu-id="175b9-164">Notice how IntelliSense displays the available methods for the `ServerInfo` helper in a drop-down list.</span></span>

    ![IntelliSense](program-asp-net-web-pages-in-visual-studio/_static/image4.png)
3. <span data-ttu-id="175b9-166">Выберите метод `GetHtml` из списка и нажмите клавишу ВВОД.</span><span class="sxs-lookup"><span data-stu-id="175b9-166">Select the `GetHtml` method from the list and then press Enter.</span></span> <span data-ttu-id="175b9-167">IntelliSense автоматически заполняет метод.</span><span class="sxs-lookup"><span data-stu-id="175b9-167">IntelliSense automatically fills in the method.</span></span> <span data-ttu-id="175b9-168">(Как и в случае любого C#метода в, необходимо добавить `()` символов после метода.) Завершенный код для метода `GetHtml` выглядит, как в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="175b9-168">(As with any method in C#, you must add `()` characters after the method.) The completed code for the `GetHtml` method looks like the following example:</span></span>

    [!code-cshtml[Main](program-asp-net-web-pages-in-visual-studio/samples/sample1.cshtml)]
4. <span data-ttu-id="175b9-169">Нажмите клавиши CTRL + F5, чтобы запустить страницу.</span><span class="sxs-lookup"><span data-stu-id="175b9-169">Press Ctrl+F5 to run the page.</span></span> <span data-ttu-id="175b9-170">Вот как выглядит страница при отображении в браузере:</span><span class="sxs-lookup"><span data-stu-id="175b9-170">This is what the page looks like when displayed in a browser:</span></span>

    ![страница по умолчанию в браузере](program-asp-net-web-pages-in-visual-studio/_static/image5.png)
5. <span data-ttu-id="175b9-172">Закройте браузер.</span><span class="sxs-lookup"><span data-stu-id="175b9-172">Close the browser.</span></span>

### <a name="using-the-debugger"></a><span data-ttu-id="175b9-173">Использование отладчика</span><span class="sxs-lookup"><span data-stu-id="175b9-173">Using the Debugger</span></span>

1. <span data-ttu-id="175b9-174">В верхней части страницы *Default. cshtml* после строки, начинающейся с `Page.Title`, добавьте следующую строку кода:</span><span class="sxs-lookup"><span data-stu-id="175b9-174">At the top of the *Default.cshtml* page, after the line that begins with `Page.Title`, add the following line of code:</span></span>

    [!code-csharp[Main](program-asp-net-web-pages-in-visual-studio/samples/sample2.cs)]
2. <span data-ttu-id="175b9-175">В сером поле редактора слева от кода нажмите кнопку Далее рядом с новой строкой, чтобы добавить *точку останова*.</span><span class="sxs-lookup"><span data-stu-id="175b9-175">In the gray margin of the editor to the left of the code, click next to this new line in order to add a *breakpoint*.</span></span> <span data-ttu-id="175b9-176">Точка останова — это маркер, указывающий отладчику на необходимость остановки выполнения программы на этом этапе, чтобы можно было увидеть, что происходит.</span><span class="sxs-lookup"><span data-stu-id="175b9-176">A breakpoint is a marker that tells the debugger to stop running the program at that point so you can see what's happening.</span></span>

    ![Задать точку останова](program-asp-net-web-pages-in-visual-studio/_static/image6.png)
3. <span data-ttu-id="175b9-178">Удалите вызов метода `ServerInfo.GetHtml` и добавьте в его место вызов `@myTime` переменной.</span><span class="sxs-lookup"><span data-stu-id="175b9-178">Remove the call to the `ServerInfo.GetHtml` method, and add a call to the `@myTime` variable in its place.</span></span> <span data-ttu-id="175b9-179">Этот вызов отображает текущее значение времени, возвращаемое новой строкой кода.</span><span class="sxs-lookup"><span data-stu-id="175b9-179">This call displays the current time value that's returned by the new line of code.</span></span>
4. <span data-ttu-id="175b9-180">Нажмите клавишу F5, чтобы запустить страницу в отладчике.</span><span class="sxs-lookup"><span data-stu-id="175b9-180">Press F5 to run the page in the debugger.</span></span> <span data-ttu-id="175b9-181">Страница останавливается в заданной точке останова.</span><span class="sxs-lookup"><span data-stu-id="175b9-181">The page stops on the breakpoint that you set.</span></span> <span data-ttu-id="175b9-182">На следующем рисунке показано, как выглядит страница в редакторе с точкой останова (желтым цветом).</span><span class="sxs-lookup"><span data-stu-id="175b9-182">The following image shows what the page looks like in the editor with the breakpoint (in yellow).</span></span>

    ![Отладка точки останова](program-asp-net-web-pages-in-visual-studio/_static/image7.png)
5. <span data-ttu-id="175b9-184">На панели инструментов Отладка нажмите кнопку **Шаг с заходом** (или нажмите клавишу F11), чтобы выполнить следующую строку кода.</span><span class="sxs-lookup"><span data-stu-id="175b9-184">In the Debug toolbar, click the **Step Into** button (or press F11) to run the next line of code.</span></span> <span data-ttu-id="175b9-185">Каждый раз при нажатии этой кнопки выполняется переход к следующей строке кода.</span><span class="sxs-lookup"><span data-stu-id="175b9-185">Each time you click this button, you advance the execution to the next line of code.</span></span>

    ![Кнопка "шаг с заходом"](program-asp-net-web-pages-in-visual-studio/_static/image8.png)
6. <span data-ttu-id="175b9-187">Изучите значение переменной `myTime`, нажимая на нее указатель мыши или проверив значения, отображаемые в окнах " **локальные** " и " **Стек вызовов** ".</span><span class="sxs-lookup"><span data-stu-id="175b9-187">Examine the value of the `myTime` variable by holding your mouse pointer over it or by inspecting the values displayed in the **Locals** and **Call Stack** windows.</span></span> <span data-ttu-id="175b9-188">В Visual Studio отобразится значение переменной.</span><span class="sxs-lookup"><span data-stu-id="175b9-188">Visual Studio display the value of the variable.</span></span>

    ![показывать значение времени](program-asp-net-web-pages-in-visual-studio/_static/image9.png)
7. <span data-ttu-id="175b9-190">После завершения проверки переменной и пошагового выполнения кода нажмите клавишу F5, чтобы продолжить выполнение страницы без остановки в каждой строке.</span><span class="sxs-lookup"><span data-stu-id="175b9-190">When you're done examining the variable and stepping through code, press F5 to continue running the page without stopping at each line.</span></span> <span data-ttu-id="175b9-191">После завершения шагов по выполнению кода в браузере отобразится страница.</span><span class="sxs-lookup"><span data-stu-id="175b9-191">When you've finished stepping through all the code, the browser displays the page.</span></span>

<span data-ttu-id="175b9-192">Дополнительные сведения о отладчике и об отладке кода в Visual Studio см. в разделе [Пошаговое руководство. Отладка веб-страниц в Visual Web Developer](https://msdn.microsoft.com/library/z9e7w6cs.aspx).</span><span class="sxs-lookup"><span data-stu-id="175b9-192">To learn more about the debugger and about how to debug code in Visual Studio, see [Walkthrough: Debugging Web Pages in Visual Web Developer](https://msdn.microsoft.com/library/z9e7w6cs.aspx).</span></span>

## <a name="using-razor-in-aspnet-mvc-projects-with-visual-studio"></a><span data-ttu-id="175b9-193">Использование Razor в проектах ASP.NET MVC с помощью Visual Studio</span><span class="sxs-lookup"><span data-stu-id="175b9-193">Using Razor in ASP.NET MVC projects with Visual Studio</span></span>

<span data-ttu-id="175b9-194">Синтаксис Razor также широко используется в проектах ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="175b9-194">The Razor syntax is also used extensively in ASP.NET MVC projects.</span></span> <span data-ttu-id="175b9-195">MVC — это мощный и основанный на шаблонах способ создания динамических веб-сайтов.</span><span class="sxs-lookup"><span data-stu-id="175b9-195">MVC is a powerful, patterns-based way to build dynamic websites.</span></span> <span data-ttu-id="175b9-196">Если веб-сайт веб-страницы ASP.NET трудно обслуживать, его можно преобразовать в приложение ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="175b9-196">If your ASP.NET Web Pages site becomes difficult to maintain, you might want to consider converting it to an ASP.NET MVC application.</span></span> <span data-ttu-id="175b9-197">Пример создания приложения MVC см. в разделе [Начало работы with ASP.NET MVC 5](../../../mvc/overview/getting-started/introduction/getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="175b9-197">For an example of creating an MVC application, see [Getting Started with ASP.NET MVC 5](../../../mvc/overview/getting-started/introduction/getting-started.md).</span></span>

<a id="vs2010support"></a>
## <a name="installing-support-for-aspnet-web-pages-in-visual-studio-2010"></a><span data-ttu-id="175b9-198">Установка поддержки для веб-страницы ASP.NET в Visual Studio 2010</span><span class="sxs-lookup"><span data-stu-id="175b9-198">Installing Support for ASP.NET Web Pages in Visual Studio 2010</span></span>

<span data-ttu-id="175b9-199">В этом разделе показано, как установить Visual Web Developer Express 2010 и инструменты веб-страницы ASP.NET для Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="175b9-199">This section shows how to install Visual Web Developer Express 2010 and the ASP.NET Web Pages Tools for Visual Studio.</span></span>

1. <span data-ttu-id="175b9-200">Если у вас еще нет установщика веб-платформы, скачайте его по следующему URL-адресу:</span><span class="sxs-lookup"><span data-stu-id="175b9-200">If you don't already have the Web Platform Installer, download it from the following URL:</span></span>

    [https://www.microsoft.com/web/downloads/platform.aspx](https://www.microsoft.com/web/downloads/platform.aspx)
2. <span data-ttu-id="175b9-201">Запустите установщик веб-платформы.</span><span class="sxs-lookup"><span data-stu-id="175b9-201">Run the Web Platform Installer.</span></span>
3. <span data-ttu-id="175b9-202">Перейдите на вкладку **продукты** .</span><span class="sxs-lookup"><span data-stu-id="175b9-202">Click the **Products** tab.</span></span>

    ![Вкладка "продукты установщика веб – платформы"](program-asp-net-web-pages-in-visual-studio/_static/image10.png)
4. <span data-ttu-id="175b9-204">Выполните поиск по запросу **ASP.NET MVC 4** (для веб-страницы ASP.NET 2) и нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="175b9-204">Search for **ASP.NET MVC 4** (for ASP.NET Web Pages 2) and then click **Add**.</span></span> <span data-ttu-id="175b9-205">К этим продуктам относятся инструменты Visual Studio для создания веб-сайтов ASP.NET Razor.</span><span class="sxs-lookup"><span data-stu-id="175b9-205">These products include Visual Studio tools for building ASP.NET Razor websites.</span></span>

    ![Параметры установки установщика платформы](program-asp-net-web-pages-in-visual-studio/_static/image11.png)
5. <span data-ttu-id="175b9-207">Нажмите кнопку **установить** , чтобы завершить установку.</span><span class="sxs-lookup"><span data-stu-id="175b9-207">Click **Install** to complete the installation.</span></span>
