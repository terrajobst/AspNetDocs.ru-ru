---
uid: signalr/overview/testing-and-debugging/unit-testing-signalr-applications
title: Модульное тестирование приложений SignalR | Документация Майкрософт
author: bradygaster
description: В этой статье описывается, как использовать функции модульного тестирования SignalR 2,0.
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: d1983524-e0d5-4ee6-9d87-1f552f7cb964
msc.legacyurl: /signalr/overview/testing-and-debugging/unit-testing-signalr-applications
msc.type: authoredcontent
ms.openlocfilehash: 2cf2e88f141d89971439dc1fc4979849f8dded47
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78467304"
---
# <a name="unit-testing-signalr-applications"></a><span data-ttu-id="5846b-103">Модульное тестирование приложений SignalR</span><span class="sxs-lookup"><span data-stu-id="5846b-103">Unit Testing SignalR Applications</span></span>

<span data-ttu-id="5846b-104">по [Патрик Флетчера](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="5846b-104">by [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="5846b-105">В этой статье описывается использование функций модульного тестирования SignalR 2.</span><span class="sxs-lookup"><span data-stu-id="5846b-105">This article describes using the Unit Testing features of SignalR 2.</span></span>
>
> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="5846b-106">Версии программного обеспечения, используемые в этом разделе</span><span class="sxs-lookup"><span data-stu-id="5846b-106">Software versions used in this topic</span></span>
>
>
> - [<span data-ttu-id="5846b-107">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="5846b-107">Visual Studio 2013</span></span>](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - <span data-ttu-id="5846b-108">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="5846b-108">.NET 4.5</span></span>
> - <span data-ttu-id="5846b-109">SignalR версии 2</span><span class="sxs-lookup"><span data-stu-id="5846b-109">SignalR version 2</span></span>
>
>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="5846b-110">Вопросы и комментарии</span><span class="sxs-lookup"><span data-stu-id="5846b-110">Questions and comments</span></span>
>
> <span data-ttu-id="5846b-111">Оставьте отзыв о том, как вы понравится вам в этом учебнике, и что можно улучшить в комментариях в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="5846b-111">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="5846b-112">Если у вас есть вопросы, не связанные непосредственно с этим руководством, их можно опубликовать на [форуме ASP.NET SignalR](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) или [StackOverflow.com](http://stackoverflow.com/).</span><span class="sxs-lookup"><span data-stu-id="5846b-112">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>

<a id="unit"></a>
## <a name="unit-testing-signalr-applications"></a><span data-ttu-id="5846b-113">Модульное тестирование приложений SignalR</span><span class="sxs-lookup"><span data-stu-id="5846b-113">Unit testing SignalR applications</span></span>

<span data-ttu-id="5846b-114">Вы можете использовать функции модульных тестов в SignalR 2 для создания модульных тестов для приложения SignalR.</span><span class="sxs-lookup"><span data-stu-id="5846b-114">You can use the unit test features in SignalR 2 to create unit tests for your SignalR application.</span></span> <span data-ttu-id="5846b-115">SignalR 2 включает интерфейс [ихубкаллерконнектионконтекст](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.ihubcallerconnectioncontext(v=vs.118).aspx) , который можно использовать для создания макета объекта для имитации методов концентратора для тестирования.</span><span class="sxs-lookup"><span data-stu-id="5846b-115">SignalR 2 includes the [IHubCallerConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.ihubcallerconnectioncontext(v=vs.118).aspx) interface, which can be used to create a mock object to simulate your hub methods for testing.</span></span>

<span data-ttu-id="5846b-116">В этом разделе вы добавите модульные тесты для приложения, созданного в [Начало работы руководстве](../getting-started/tutorial-getting-started-with-signalr.md) , с помощью [xUnit.NET](https://github.com/xunit/xunit) и [MOQ](https://github.com/Moq/moq4).</span><span class="sxs-lookup"><span data-stu-id="5846b-116">In this section, you'll add unit tests for the application created in the [Getting Started tutorial](../getting-started/tutorial-getting-started-with-signalr.md) using [XUnit.net](https://github.com/xunit/xunit) and [Moq](https://github.com/Moq/moq4).</span></span>

<span data-ttu-id="5846b-117">XUnit.net будет использоваться для управления тестом; MOQ будет использоваться для создания [макета](http://en.wikipedia.org/wiki/Mock_object) объекта для тестирования.</span><span class="sxs-lookup"><span data-stu-id="5846b-117">XUnit.net will be used to control the test; Moq will be used to create a [mock](http://en.wikipedia.org/wiki/Mock_object) object for testing.</span></span> <span data-ttu-id="5846b-118">При необходимости можно использовать и другие платформы макетирования. [Нсубституте](http://nsubstitute.github.io/) также является хорошим выбором.</span><span class="sxs-lookup"><span data-stu-id="5846b-118">Other mocking frameworks can be used if desired; [NSubstitute](http://nsubstitute.github.io/) is also a good choice.</span></span> <span data-ttu-id="5846b-119">В этом руководстве показано, как настроить макет объекта двумя способами: во-первых, с помощью объекта `dynamic` (представленного в .NET Framework 4) и секунд с помощью интерфейса.</span><span class="sxs-lookup"><span data-stu-id="5846b-119">This tutorial demonstrates how to set up the mock object in two ways: First, using a `dynamic` object (introduced in .NET Framework 4), and second, using an interface.</span></span>

### <a name="contents"></a><span data-ttu-id="5846b-120">Содержимое</span><span class="sxs-lookup"><span data-stu-id="5846b-120">Contents</span></span>

<span data-ttu-id="5846b-121">Этот учебник содержит следующие разделы.</span><span class="sxs-lookup"><span data-stu-id="5846b-121">This tutorial contains the following sections.</span></span>

- [<span data-ttu-id="5846b-122">Модульное тестирование с динамическим</span><span class="sxs-lookup"><span data-stu-id="5846b-122">Unit testing with Dynamic</span></span>](#dynamic)
- [<span data-ttu-id="5846b-123">Модульное тестирование по типу</span><span class="sxs-lookup"><span data-stu-id="5846b-123">Unit testing by type</span></span>](#type)

<a id="dynamic"></a>
### <a name="unit-testing-with-dynamic"></a><span data-ttu-id="5846b-124">Модульное тестирование с динамическим</span><span class="sxs-lookup"><span data-stu-id="5846b-124">Unit testing with Dynamic</span></span>

<span data-ttu-id="5846b-125">В этом разделе вы добавите модульный тест для приложения, созданного в [Начало работы руководстве](../getting-started/tutorial-getting-started-with-signalr.md) , с помощью динамического объекта.</span><span class="sxs-lookup"><span data-stu-id="5846b-125">In this section, you'll add a unit test for the application created in the [Getting Started tutorial](../getting-started/tutorial-getting-started-with-signalr.md) using a dynamic object.</span></span>

1. <span data-ttu-id="5846b-126">Установите [расширение xUnit Runner](https://visualstudiogallery.msdn.microsoft.com/463c5987-f82b-46c8-a97e-b1cde42b9099) для Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="5846b-126">Install the [XUnit Runner extension](https://visualstudiogallery.msdn.microsoft.com/463c5987-f82b-46c8-a97e-b1cde42b9099) for Visual Studio 2013.</span></span>
2. <span data-ttu-id="5846b-127">Либо завершите работу с [руководством начало работы](../getting-started/tutorial-getting-started-with-signalr.md), либо Скачайте готовое приложение из [коллекции кода MSDN](https://code.msdn.microsoft.com/SignalR-Getting-Started-b9d18aa9).</span><span class="sxs-lookup"><span data-stu-id="5846b-127">Either complete the [Getting Started tutorial](../getting-started/tutorial-getting-started-with-signalr.md), or download the completed application from [MSDN Code Gallery](https://code.msdn.microsoft.com/SignalR-Getting-Started-b9d18aa9).</span></span>
3. <span data-ttu-id="5846b-128">Если вы используете скачанную версию приложения начало работы, откройте **консоль диспетчера пакетов** и нажмите кнопку **восстановить** , чтобы добавить в проект пакет SignalR.</span><span class="sxs-lookup"><span data-stu-id="5846b-128">If you are using the download version of the Getting Started application, open **Package Manager Console** and click **Restore** to add the SignalR package to the project.</span></span>

    ![Восстановление пакетов](unit-testing-signalr-applications/_static/image1.png)
4. <span data-ttu-id="5846b-130">Добавьте проект в решение для модульного теста.</span><span class="sxs-lookup"><span data-stu-id="5846b-130">Add a project to the solution for the unit test.</span></span> <span data-ttu-id="5846b-131">Щелкните решение правой кнопкой мыши в **Обозреватель решений** и выберите **Добавить**, **создать проект...** . В **C#** узле выберите узел **Windows** .</span><span class="sxs-lookup"><span data-stu-id="5846b-131">Right-click your solution in **Solution Explorer** and select **Add**, **New Project...**. Under the **C#** node, select the **Windows** node.</span></span> <span data-ttu-id="5846b-132">Выберите **Библиотека классов**.</span><span class="sxs-lookup"><span data-stu-id="5846b-132">Select **Class Library**.</span></span> <span data-ttu-id="5846b-133">Назовите новый проект **TestLibrary** и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="5846b-133">Name the new project **TestLibrary** and click **OK**.</span></span>

    ![Создание тестовой библиотеки](unit-testing-signalr-applications/_static/image2.png)
5. <span data-ttu-id="5846b-135">Добавьте ссылку в проект библиотеки тестов в проект Сигналрчат.</span><span class="sxs-lookup"><span data-stu-id="5846b-135">Add a reference in the test library project to the SignalRChat project.</span></span> <span data-ttu-id="5846b-136">Щелкните правой кнопкой мыши проект **TestLibrary** и выберите **Добавить**, **ссылка...** . Выберите узел **проекты** в узле **решение** и проверьте **сигналрчат**.</span><span class="sxs-lookup"><span data-stu-id="5846b-136">Right-click the **TestLibrary** project and select **Add**, **Reference...**. Select the **Projects** node under the **Solution** node, and check **SignalRChat**.</span></span> <span data-ttu-id="5846b-137">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="5846b-137">Click **OK**.</span></span>

    ![Добавить ссылку на проект](unit-testing-signalr-applications/_static/image3.png)
6. <span data-ttu-id="5846b-139">Добавьте пакеты SignalR, MOQ и XUnit в проект **TestLibrary** .</span><span class="sxs-lookup"><span data-stu-id="5846b-139">Add the SignalR, Moq, and XUnit packages to the **TestLibrary** project.</span></span> <span data-ttu-id="5846b-140">В **консоли диспетчера пакетов**задайте для раскрывающегося списка **проект по умолчанию** значение **TestLibrary**.</span><span class="sxs-lookup"><span data-stu-id="5846b-140">In the **Package Manager Console**, set the **Default Project** dropdown to **TestLibrary**.</span></span> <span data-ttu-id="5846b-141">В окне консоли выполните следующие команды:</span><span class="sxs-lookup"><span data-stu-id="5846b-141">Run the following commands in the console window:</span></span>

   - `Install-Package Microsoft.AspNet.SignalR`
   - `Install-Package Moq`
   - `Install-Package XUnit`

     ![Установка пакетов](unit-testing-signalr-applications/_static/image4.png)
7. <span data-ttu-id="5846b-143">Создайте файл теста.</span><span class="sxs-lookup"><span data-stu-id="5846b-143">Create the test file.</span></span> <span data-ttu-id="5846b-144">Щелкните правой кнопкой мыши проект **TestLibrary** и выберите пункт **Добавить...** , **класс**.</span><span class="sxs-lookup"><span data-stu-id="5846b-144">Right-click the **TestLibrary** project and click **Add...**, **Class**.</span></span> <span data-ttu-id="5846b-145">Назовите новый класс **Tests.CS**.</span><span class="sxs-lookup"><span data-stu-id="5846b-145">Name the new class **Tests.cs**.</span></span>
8. <span data-ttu-id="5846b-146">Замените содержимое Tests.cs следующим кодом.</span><span class="sxs-lookup"><span data-stu-id="5846b-146">Replace the contents of Tests.cs with the following code.</span></span>

    [!code-csharp[Main](unit-testing-signalr-applications/samples/sample1.cs)]

    <span data-ttu-id="5846b-147">В приведенном выше коде тестовый клиент создается с помощью объекта `Mock` из библиотеки [MOQ](https://github.com/Moq/moq4) типа [Ихубкаллерконнектионконтекст](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.ihubcallerconnectioncontext(v=vs.118).aspx) (в SignalR 2,1 назначьте `dynamic` для параметра типа.) Интерфейс `IHubCallerConnectionContext` — это прокси-объект, с помощью которого вызываются методы на клиенте.</span><span class="sxs-lookup"><span data-stu-id="5846b-147">In the code above, a test client is created using the `Mock` object from the [Moq](https://github.com/Moq/moq4) library, of type [IHubCallerConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.ihubcallerconnectioncontext(v=vs.118).aspx) (in SignalR 2.1, assign `dynamic` for the type parameter.) The `IHubCallerConnectionContext` interface is the proxy object with which you invoke methods on the client.</span></span> <span data-ttu-id="5846b-148">Затем функция `broadcastMessage` определяется для макета клиента, чтобы его можно было вызывать с помощью класса `ChatHub`.</span><span class="sxs-lookup"><span data-stu-id="5846b-148">The `broadcastMessage` function is then defined for the mock client so that it can be called by the `ChatHub` class.</span></span> <span data-ttu-id="5846b-149">Затем обработчик тестов вызывает метод `Send` класса `ChatHub`, который, в свою очередь, вызывает функцию макетирования `broadcastMessage`.</span><span class="sxs-lookup"><span data-stu-id="5846b-149">The test engine then calls the `Send` method of the `ChatHub` class, which in turn calls the mocked `broadcastMessage` function.</span></span>
9. <span data-ttu-id="5846b-150">Постройте решение, нажав клавишу **F6**.</span><span class="sxs-lookup"><span data-stu-id="5846b-150">Build the solution by pressing **F6**.</span></span>
10. <span data-ttu-id="5846b-151">Выполните модульный тест.</span><span class="sxs-lookup"><span data-stu-id="5846b-151">Run the unit test.</span></span> <span data-ttu-id="5846b-152">В Visual Studio выберите **тест**, **Windows**, **Обозреватель тестов**.</span><span class="sxs-lookup"><span data-stu-id="5846b-152">In Visual Studio, select **Test**, **Windows**, **Test Explorer**.</span></span> <span data-ttu-id="5846b-153">В окне обозревателя тестов щелкните правой кнопкой мыши **хубсаремоккаблевиадинамик** и выберите команду **Выполнить выбранные тесты**.</span><span class="sxs-lookup"><span data-stu-id="5846b-153">In the Test Explorer window, right-click **HubsAreMockableViaDynamic** and select **Run Selected Tests**.</span></span>

    ![Обозреватель тестов](unit-testing-signalr-applications/_static/image5.png)
11. <span data-ttu-id="5846b-155">Убедитесь, что тест пройден, проверив нижнюю панель в окне обозревателя тестов.</span><span class="sxs-lookup"><span data-stu-id="5846b-155">Verify that the test passed by checking the lower pane in the Test Explorer window.</span></span> <span data-ttu-id="5846b-156">В окне будет показано, что тест пройден.</span><span class="sxs-lookup"><span data-stu-id="5846b-156">The window will show that the test passed.</span></span>

    ![Тест пройден](unit-testing-signalr-applications/_static/image6.png)

<a id="type"></a>
### <a name="unit-testing-by-type"></a><span data-ttu-id="5846b-158">Модульное тестирование по типу</span><span class="sxs-lookup"><span data-stu-id="5846b-158">Unit testing by type</span></span>

<span data-ttu-id="5846b-159">В этом разделе вы добавите тест для приложения, созданного в [Начало работы руководстве](../getting-started/tutorial-getting-started-with-signalr.md) , используя интерфейс, содержащий тестируемый метод.</span><span class="sxs-lookup"><span data-stu-id="5846b-159">In this section, you'll add a test for the application created in the [Getting Started tutorial](../getting-started/tutorial-getting-started-with-signalr.md) using an interface that contains the method to be tested.</span></span>

1. <span data-ttu-id="5846b-160">Выполните шаги 1-7 в разделе [модульное тестирование с помощью динамического](#dynamic) учебника выше.</span><span class="sxs-lookup"><span data-stu-id="5846b-160">Complete steps 1-7 in the [Unit testing with Dynamic](#dynamic) tutorial above.</span></span>
2. <span data-ttu-id="5846b-161">Замените содержимое Tests.cs следующим кодом.</span><span class="sxs-lookup"><span data-stu-id="5846b-161">Replace the contents of Tests.cs with the following code.</span></span>

    [!code-csharp[Main](unit-testing-signalr-applications/samples/sample2.cs)]

    <span data-ttu-id="5846b-162">В приведенном выше коде создается интерфейс, определяющий сигнатуру метода `broadcastMessage`, для которого тестовый модуль будет создавать макет клиента.</span><span class="sxs-lookup"><span data-stu-id="5846b-162">In the code above, an interface is created defining the signature of the `broadcastMessage` method for which the test engine will create a mock client.</span></span> <span data-ttu-id="5846b-163">Затем макет клиента создается с помощью объекта `Mock` типа [ихубкаллерконнектионконтекст](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.ihubcallerconnectioncontext(v=vs.118).aspx) (в SignalR 2,1, назначьте `dynamic` для параметра типа.) Интерфейс `IHubCallerConnectionContext` — это прокси-объект, с помощью которого вызываются методы на клиенте.</span><span class="sxs-lookup"><span data-stu-id="5846b-163">A mock client is then created using the `Mock` object, of type [IHubCallerConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.ihubcallerconnectioncontext(v=vs.118).aspx) (in SignalR 2.1, assign `dynamic` for the type parameter.) The `IHubCallerConnectionContext` interface is the proxy object with which you invoke methods on the client.</span></span>

    <span data-ttu-id="5846b-164">Затем тест создает экземпляр `ChatHub`, а затем создает макет версии метода `broadcastMessage`, который, в свою очередь, вызывается путем вызова метода `Send` в концентраторе.</span><span class="sxs-lookup"><span data-stu-id="5846b-164">The test then creates an instance of `ChatHub`, and then creates a mock version of the `broadcastMessage` method, which in turn is invoked by calling the `Send` method on the hub.</span></span>
3. <span data-ttu-id="5846b-165">Постройте решение, нажав клавишу **F6**.</span><span class="sxs-lookup"><span data-stu-id="5846b-165">Build the solution by pressing **F6**.</span></span>
4. <span data-ttu-id="5846b-166">Выполните модульный тест.</span><span class="sxs-lookup"><span data-stu-id="5846b-166">Run the unit test.</span></span> <span data-ttu-id="5846b-167">В Visual Studio выберите **тест**, **Windows**, **Обозреватель тестов**.</span><span class="sxs-lookup"><span data-stu-id="5846b-167">In Visual Studio, select **Test**, **Windows**, **Test Explorer**.</span></span> <span data-ttu-id="5846b-168">В окне обозревателя тестов щелкните правой кнопкой мыши **хубсаремоккаблевиадинамик** и выберите команду **Выполнить выбранные тесты**.</span><span class="sxs-lookup"><span data-stu-id="5846b-168">In the Test Explorer window, right-click **HubsAreMockableViaDynamic** and select **Run Selected Tests**.</span></span>

    ![Обозреватель тестов](unit-testing-signalr-applications/_static/image7.png)
5. <span data-ttu-id="5846b-170">Убедитесь, что тест пройден, проверив нижнюю панель в окне обозревателя тестов.</span><span class="sxs-lookup"><span data-stu-id="5846b-170">Verify that the test passed by checking the lower pane in the Test Explorer window.</span></span> <span data-ttu-id="5846b-171">В окне будет показано, что тест пройден.</span><span class="sxs-lookup"><span data-stu-id="5846b-171">The window will show that the test passed.</span></span>

    ![Тест пройден](unit-testing-signalr-applications/_static/image8.png)
