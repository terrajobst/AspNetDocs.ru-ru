---
uid: aspnet/overview/owin-and-katana/owin-startup-class-detection
title: Обнаружение класса запуска OWIN | Документация Майкрософт
author: Praburaj
description: В этом руководстве показано, как настроить, какой класс запуска OWIN загружается. Дополнительные сведения о OWIN см. в обзоре проекта Katana. Этот учебник был...
ms.author: riande
ms.date: 01/28/2019
ms.assetid: 08257f55-36f4-4e39-9c88-2a5602838c79
msc.legacyurl: /aspnet/overview/owin-and-katana/owin-startup-class-detection
msc.type: authoredcontent
ms.openlocfilehash: e1670c32049ec33dd4d1941a091a429d3929c452
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78500184"
---
# <a name="owin-startup-class-detection"></a><span data-ttu-id="9919a-105">Определение класса запуска OWIN</span><span class="sxs-lookup"><span data-stu-id="9919a-105">OWIN Startup Class Detection</span></span>

> <span data-ttu-id="9919a-106">В этом руководстве показано, как настроить, какой класс запуска OWIN загружается.</span><span class="sxs-lookup"><span data-stu-id="9919a-106">This tutorial shows how to configure which OWIN startup class is loaded.</span></span> <span data-ttu-id="9919a-107">Дополнительные сведения о OWIN см. [в обзоре проекта Katana](an-overview-of-project-katana.md).</span><span class="sxs-lookup"><span data-stu-id="9919a-107">For more information on OWIN, see [An Overview of Project Katana](an-overview-of-project-katana.md).</span></span> <span data-ttu-id="9919a-108">Этот учебник написан на Рик Андерсон (( [@RickAndMSFT](https://twitter.com/#!/RickAndMSFT) ), прабураж Сиагаражан и Говард дайеркинг ( [@howard\_Дайеркинг](https://twitter.com/howard_dierking) ).</span><span class="sxs-lookup"><span data-stu-id="9919a-108">This tutorial was written by Rick Anderson ( [@RickAndMSFT](https://twitter.com/#!/RickAndMSFT) ), Praburaj Thiagarajan, and Howard Dierking ( [@howard\_dierking](https://twitter.com/howard_dierking) ).</span></span>
>
> ## <a name="prerequisites"></a><span data-ttu-id="9919a-109">предварительные требования</span><span class="sxs-lookup"><span data-stu-id="9919a-109">Prerequisites</span></span>
>
> [<span data-ttu-id="9919a-110">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="9919a-110">Visual Studio 2017</span></span>](https://visualstudio.microsoft.com/downloads/)

## <a name="owin-startup-class-detection"></a><span data-ttu-id="9919a-111">Определение класса запуска OWIN</span><span class="sxs-lookup"><span data-stu-id="9919a-111">OWIN Startup Class Detection</span></span>

 <span data-ttu-id="9919a-112">Каждое приложение OWIN имеет класс Startup, в котором указываются компоненты для конвейера приложения.</span><span class="sxs-lookup"><span data-stu-id="9919a-112">Every OWIN Application has a startup class where you specify components for the application pipeline.</span></span> <span data-ttu-id="9919a-113">Существует несколько способов подключения класса Startup к среде выполнения в зависимости от выбранной модели размещения (Овинхост, IIS и IIS-Express).</span><span class="sxs-lookup"><span data-stu-id="9919a-113">There are different ways you can connect your startup class with the runtime, depending on the hosting model you choose (OwinHost, IIS, and IIS-Express).</span></span> <span data-ttu-id="9919a-114">Класс Startup, показанный в этом учебнике, можно использовать во всех приложениях размещения.</span><span class="sxs-lookup"><span data-stu-id="9919a-114">The startup class shown in this tutorial can be used in every hosting application.</span></span> <span data-ttu-id="9919a-115">Вы подключаете класс Startup к среде выполнения размещения, используя один из следующих подходов:</span><span class="sxs-lookup"><span data-stu-id="9919a-115">You connect the startup class with the hosting runtime using one of the these approaches:</span></span>

1. <span data-ttu-id="9919a-116">**Соглашение об именовании**: Katana ищет класс с именем `Startup` в пространстве имен, соответствующем имени сборки или глобальному пространству имен.</span><span class="sxs-lookup"><span data-stu-id="9919a-116">**Naming Convention**: Katana looks for a class named `Startup` in namespace matching the assembly name or the global namespace.</span></span>
2. <span data-ttu-id="9919a-117">**Атрибут овинстартуп**: это подход, который большинство разработчиков будет использовать для указания класса Startup.</span><span class="sxs-lookup"><span data-stu-id="9919a-117">**OwinStartup Attribute**: This is the approach most developers will take to specify the startup class.</span></span> <span data-ttu-id="9919a-118">Следующий атрибут задает классу Startup классу `TestStartup` в пространстве имен `StartupDemo`.</span><span class="sxs-lookup"><span data-stu-id="9919a-118">The following attribute will set the startup class to the `TestStartup` class in the `StartupDemo` namespace.</span></span>

    [!code-csharp[Main](owin-startup-class-detection/samples/sample1.cs)]

   <span data-ttu-id="9919a-119">Атрибут `OwinStartup` переопределяет соглашение об именовании.</span><span class="sxs-lookup"><span data-stu-id="9919a-119">The `OwinStartup` attribute overrides the naming convention.</span></span> <span data-ttu-id="9919a-120">Можно также указать понятное имя с помощью этого атрибута, однако при использовании понятного имени необходимо также использовать элемент `appSetting` в файле конфигурации.</span><span class="sxs-lookup"><span data-stu-id="9919a-120">You can also specify a friendly name with this attribute, however, using a friendly name requires you to also use the `appSetting` element in the configuration file.</span></span>
3. <span data-ttu-id="9919a-121">**Элемент appSetting в файле конфигурации**: элемент `appSetting` переопределяет атрибут `OwinStartup` и соглашение об именовании.</span><span class="sxs-lookup"><span data-stu-id="9919a-121">**The appSetting element in the Configuration file**: The `appSetting` element overrides the `OwinStartup` attribute and naming convention.</span></span> <span data-ttu-id="9919a-122">Можно использовать несколько классов запуска (каждый с помощью атрибута `OwinStartup`) и указать, какой класс запуска будет загружаться в файл конфигурации, используя разметку, аналогичную следующей:</span><span class="sxs-lookup"><span data-stu-id="9919a-122">You can have multiple startup classes (each using an `OwinStartup` attribute) and configure which startup class will be loaded in a configuration file using markup similar to the following:</span></span>

    [!code-xml[Main](owin-startup-class-detection/samples/sample2.xml)]

   <span data-ttu-id="9919a-123">Следующий ключ, явно указывающий класс запуска и сборку, также можно использовать:</span><span class="sxs-lookup"><span data-stu-id="9919a-123">The following key, which explicitly specifies the startup class and assembly can also be used:</span></span>

    [!code-xml[Main](owin-startup-class-detection/samples/sample3.xml)]

   <span data-ttu-id="9919a-124">Следующий XML-код в файле конфигурации указывает понятное имя класса запуска `ProductionConfiguration`.</span><span class="sxs-lookup"><span data-stu-id="9919a-124">The following XML in the configuration file specifies a friendly startup class name of `ProductionConfiguration`.</span></span>

    [!code-xml[Main](owin-startup-class-detection/samples/sample4.xml)]

   <span data-ttu-id="9919a-125">Приведенная выше разметка должна использоваться со следующим атрибутом `OwinStartup`, который указывает понятное имя и приводит к запуску `ProductionStartup2` класса.</span><span class="sxs-lookup"><span data-stu-id="9919a-125">The above markup must be used with the following `OwinStartup` attribute which specifies a friendly name and causes the `ProductionStartup2` class to run.</span></span>

    [!code-csharp[Main](owin-startup-class-detection/samples/sample5.cs?highlight=1,16)]
4. <span data-ttu-id="9919a-126">Чтобы отключить обнаружение запуска OWIN, добавьте `appSetting owin:AutomaticAppStartup` со значением `"false"` в файле Web. config.</span><span class="sxs-lookup"><span data-stu-id="9919a-126">To disable OWIN startup discovery add the `appSetting owin:AutomaticAppStartup` with a value of `"false"` in the web.config file.</span></span>

    [!code-xml[Main](owin-startup-class-detection/samples/sample6.xml)]

## <a name="create-an-aspnet-web-app-using-owin-startup"></a><span data-ttu-id="9919a-127">Создание веб-приложения ASP.NET с помощью OWIN Startup</span><span class="sxs-lookup"><span data-stu-id="9919a-127">Create an ASP.NET Web App using OWIN Startup</span></span>

1. <span data-ttu-id="9919a-128">Создайте пустое веб-приложение Asp.Net и назовите его **стартупдемо**.</span><span class="sxs-lookup"><span data-stu-id="9919a-128">Create an empty Asp.Net web application and name it **StartupDemo**.</span></span> <span data-ttu-id="9919a-129">— Установите `Microsoft.Owin.Host.SystemWeb` с помощью диспетчера пакетов NuGet.</span><span class="sxs-lookup"><span data-stu-id="9919a-129">- Install `Microsoft.Owin.Host.SystemWeb` using the NuGet package manager.</span></span> <span data-ttu-id="9919a-130">В меню **Сервис** выберите **Диспетчер пакетов NuGet**, а затем — **консоль диспетчера пакетов**.</span><span class="sxs-lookup"><span data-stu-id="9919a-130">From the **Tools** menu, select **NuGet Package Manager**, and then **Package Manager Console**.</span></span> <span data-ttu-id="9919a-131">Введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="9919a-131">Enter the following command:</span></span>

    [!code-powershell[Main](owin-startup-class-detection/samples/sample7.ps1)]
2. <span data-ttu-id="9919a-132">Добавьте класс запуска OWIN.</span><span class="sxs-lookup"><span data-stu-id="9919a-132">Add an OWIN startup class.</span></span> <span data-ttu-id="9919a-133">В Visual Studio 2017 щелкните проект правой кнопкой мыши и выберите **Добавить класс**. — в диалоговом окне **Добавление нового элемента** введите *OWIN* в поле поиска и измените имя на Startup.cs, а затем нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="9919a-133">In Visual Studio 2017 right-click the project and select **Add Class**.- In the **Add New Item** dialog box, enter *OWIN* in the search field, and change the name to Startup.cs, and then select **Add**.</span></span>

     ![](owin-startup-class-detection/_static/image1.png)

   <span data-ttu-id="9919a-134">В следующий раз, когда нужно добавить *класс запуска Owin*, он будет доступен в меню **Добавить** .</span><span class="sxs-lookup"><span data-stu-id="9919a-134">The next time you want to add an *Owin Startup class*, it will be in available from the **Add** menu.</span></span>

     ![](owin-startup-class-detection/_static/image2.png)

   <span data-ttu-id="9919a-135">Кроме того, можно щелкнуть проект правой кнопкой мыши и выбрать **Добавить**, выбрать пункт **создать элемент**, а затем выбрать **класс запуска Owin**.</span><span class="sxs-lookup"><span data-stu-id="9919a-135">Alternatively, you can right-click the project and select **Add**, then select **New Item**, and then select the **Owin Startup class**.</span></span>

     ![](owin-startup-class-detection/_static/image3.png)

- <span data-ttu-id="9919a-136">Замените созданный код в файле *Startup.CS* следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="9919a-136">Replace the generated code in the *Startup.cs* file with the following:</span></span>

    [!code-csharp[Main](owin-startup-class-detection/samples/sample8.cs?highlight=5,7,15-28,31-34)]

  <span data-ttu-id="9919a-137">`app.Use` лямбда-выражение используется для регистрации указанного компонента по промежуточного слоя в конвейере OWIN.</span><span class="sxs-lookup"><span data-stu-id="9919a-137">The `app.Use` lambda expression is used to register the specified middleware component to the OWIN pipeline.</span></span> <span data-ttu-id="9919a-138">В этом случае мы настраиваете ведение журнала входящих запросов перед ответом на входящий запрос.</span><span class="sxs-lookup"><span data-stu-id="9919a-138">In this case we are setting up logging of incoming requests before responding to the incoming request.</span></span> <span data-ttu-id="9919a-139">Параметр `next` — это делегат ( [Func](https://msdn.microsoft.com/library/bb534960(v=vs.100).aspx) &lt; [Task](https://msdn.microsoft.com/library/dd321424(v=vs.100).aspx) &gt;) к следующему компоненту в конвейере.</span><span class="sxs-lookup"><span data-stu-id="9919a-139">The `next` parameter is the delegate ( [Func](https://msdn.microsoft.com/library/bb534960(v=vs.100).aspx) &lt; [Task](https://msdn.microsoft.com/library/dd321424(v=vs.100).aspx) &gt; ) to the next component in the pipeline.</span></span> <span data-ttu-id="9919a-140">`app.Run` лямбда-выражение подключает конвейер к входящим запросам и предоставляет механизм ответа.</span><span class="sxs-lookup"><span data-stu-id="9919a-140">The `app.Run` lambda expression hooks up the pipeline to incoming requests and provides the response mechanism.</span></span>
     > [!NOTE]
     > <span data-ttu-id="9919a-141">В приведенном выше коде мы добавили в комментарий атрибут `OwinStartup`, и мы используем соглашение о запуске класса с именем `Startup`. для запуска приложения нажмите клавишу ***F5*** .</span><span class="sxs-lookup"><span data-stu-id="9919a-141">In the code above we have commented out the `OwinStartup` attribute and we're relying on the convention of running the class named `Startup` .- Press ***F5*** to run the application.</span></span> <span data-ttu-id="9919a-142">Несколько раз нажмите кнопку "Обновить".</span><span class="sxs-lookup"><span data-stu-id="9919a-142">Hit refresh a few times.</span></span>

    <span data-ttu-id="9919a-143">![](owin-startup-class-detection/_static/image4.png) Примечание. число, показанное в изображениях этого учебника, не будет совпадать с отображаемым числом.</span><span class="sxs-lookup"><span data-stu-id="9919a-143">![](owin-startup-class-detection/_static/image4.png) Note: The number shown in the images in this tutorial will not match the number you see.</span></span> <span data-ttu-id="9919a-144">Строка миллисекунды используется для отображения нового ответа при обновлении страницы.</span><span class="sxs-lookup"><span data-stu-id="9919a-144">The millisecond string is used to show a new response when you refresh the page.</span></span>
  <span data-ttu-id="9919a-145">Данные трассировки можно просмотреть в окне **вывод** .</span><span class="sxs-lookup"><span data-stu-id="9919a-145">You can see the trace information in the **Output** window.</span></span>

    ![](owin-startup-class-detection/_static/image5.png)

## <a name="add-more-startup-classes"></a><span data-ttu-id="9919a-146">Добавление классов запуска</span><span class="sxs-lookup"><span data-stu-id="9919a-146">Add More Startup Classes</span></span>

<span data-ttu-id="9919a-147">В этом разделе мы добавим еще один класс Startup.</span><span class="sxs-lookup"><span data-stu-id="9919a-147">In this section we'll add another Startup class.</span></span> <span data-ttu-id="9919a-148">В приложение можно добавить несколько классов запуска OWIN.</span><span class="sxs-lookup"><span data-stu-id="9919a-148">You can add multiple OWIN startup class to your application.</span></span> <span data-ttu-id="9919a-149">Например, может потребоваться создать классы запуска для разработки, тестирования и производства.</span><span class="sxs-lookup"><span data-stu-id="9919a-149">For example, you might want to create startup classes for development, testing and production.</span></span>

1. <span data-ttu-id="9919a-150">Создайте новый класс запуска OWIN и назовите его `ProductionStartup`.</span><span class="sxs-lookup"><span data-stu-id="9919a-150">Create a new OWIN Startup class and name it `ProductionStartup`.</span></span>
2. <span data-ttu-id="9919a-151">Замените сгенерированный код следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="9919a-151">Replace the generated code with the following:</span></span>

    [!code-csharp[Main](owin-startup-class-detection/samples/sample9.cs?highlight=14-18)]
3. <span data-ttu-id="9919a-152">Нажмите клавишу Control F5, чтобы запустить приложение.</span><span class="sxs-lookup"><span data-stu-id="9919a-152">Press Control F5 to run the app.</span></span> <span data-ttu-id="9919a-153">Атрибут `OwinStartup` указывает, что запущен рабочий класс запуска.</span><span class="sxs-lookup"><span data-stu-id="9919a-153">The `OwinStartup` attribute specifies the production startup class is run.</span></span>

    ![](owin-startup-class-detection/_static/image6.png)
4. <span data-ttu-id="9919a-154">Создайте другой класс запуска OWIN и назовите его `TestStartup`.</span><span class="sxs-lookup"><span data-stu-id="9919a-154">Create another OWIN Startup class and name it `TestStartup`.</span></span>
5. <span data-ttu-id="9919a-155">Замените сгенерированный код следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="9919a-155">Replace the generated code with the following:</span></span>

    [!code-csharp[Main](owin-startup-class-detection/samples/sample10.cs?highlight=6,14-18)]

   <span data-ttu-id="9919a-156">Перегрузка атрибута `OwinStartup` выше указывает `TestingConfiguration` как *понятное* имя класса запуска.</span><span class="sxs-lookup"><span data-stu-id="9919a-156">The `OwinStartup` attribute overload above specifies `TestingConfiguration` as the *friendly* name of the Startup class.</span></span>
6. <span data-ttu-id="9919a-157">Откройте файл *Web. config* и добавьте ключ запуска приложения OWIN, который указывает понятное имя класса Startup:</span><span class="sxs-lookup"><span data-stu-id="9919a-157">Open the *web.config* file and add the OWIN App startup key which specifies the friendly name of the Startup class:</span></span>

    [!code-xml[Main](owin-startup-class-detection/samples/sample11.xml?highlight=3-5)]
7. <span data-ttu-id="9919a-158">Нажмите клавишу Control F5, чтобы запустить приложение.</span><span class="sxs-lookup"><span data-stu-id="9919a-158">Press Control F5 to run the app.</span></span> <span data-ttu-id="9919a-159">Элемент параметров приложения имеет приоритет и выполняется конфигурация теста.</span><span class="sxs-lookup"><span data-stu-id="9919a-159">The app settings element takes precedent, and the test configuration is run.</span></span>

    ![](owin-startup-class-detection/_static/image7.png)
8. <span data-ttu-id="9919a-160">Удалите *понятное* имя из атрибута `OwinStartup` в классе `TestStartup`.</span><span class="sxs-lookup"><span data-stu-id="9919a-160">Remove the *friendly* name from the `OwinStartup` attribute in the `TestStartup` class.</span></span>

    [!code-csharp[Main](owin-startup-class-detection/samples/sample12.cs)]
9. <span data-ttu-id="9919a-161">Замените ключ запуска приложения OWIN в файле *Web. config* следующим образом:</span><span class="sxs-lookup"><span data-stu-id="9919a-161">Replace the OWIN App startup key in the *web.config* file with the following:</span></span>

    [!code-xml[Main](owin-startup-class-detection/samples/sample13.xml)]
10. <span data-ttu-id="9919a-162">Верните атрибут `OwinStartup` в каждом классе в код атрибута по умолчанию, созданный Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="9919a-162">Revert the `OwinStartup` attribute in each class to the default attribute code generated by Visual Studio:</span></span>

    [!code-csharp[Main](owin-startup-class-detection/samples/sample14.cs)]

    <span data-ttu-id="9919a-163">Каждый из ключей запуска приложения OWIN, приведенных ниже, приведет к запуску рабочего класса.</span><span class="sxs-lookup"><span data-stu-id="9919a-163">Each of the OWIN App startup keys below will cause the production class to run.</span></span>

    [!code-xml[Main](owin-startup-class-detection/samples/sample15.xml)]

    <span data-ttu-id="9919a-164">Последний ключ запуска задает метод конфигурации запуска.</span><span class="sxs-lookup"><span data-stu-id="9919a-164">The last startup key specifies the startup configuration method.</span></span> <span data-ttu-id="9919a-165">Следующий ключ запуска приложения OWIN позволяет изменить имя класса конфигурации на `MyConfiguration`.</span><span class="sxs-lookup"><span data-stu-id="9919a-165">The following OWIN App startup key allows you to change the name of the configuration class to `MyConfiguration` .</span></span>

    [!code-xml[Main](owin-startup-class-detection/samples/sample16.xml)]

## <a name="using-owinhostexe"></a><span data-ttu-id="9919a-166">Использование Овинхост. exe</span><span class="sxs-lookup"><span data-stu-id="9919a-166">Using Owinhost.exe</span></span>

1. <span data-ttu-id="9919a-167">Замените файл Web. config следующей разметкой:</span><span class="sxs-lookup"><span data-stu-id="9919a-167">Replace the Web.config file with the following markup:</span></span>

    [!code-xml[Main](owin-startup-class-detection/samples/sample17.xml?highlight=3-6)]

   <span data-ttu-id="9919a-168">Последний ключ WINS, поэтому в данном случае `TestStartup` указан.</span><span class="sxs-lookup"><span data-stu-id="9919a-168">The last key wins, so in this case `TestStartup` is specified.</span></span>
2. <span data-ttu-id="9919a-169">Установите Овинхост из PMC:</span><span class="sxs-lookup"><span data-stu-id="9919a-169">Install Owinhost from the PMC:</span></span>

    [!code-console[Main](owin-startup-class-detection/samples/sample18.cmd)]
3. <span data-ttu-id="9919a-170">Перейдите в папку приложения (папку, содержащую файл *Web. config* ) и в командной строке введите:</span><span class="sxs-lookup"><span data-stu-id="9919a-170">Navigate to the application folder (the folder containing the *Web.config* file) and in a command prompt and type:</span></span>

    [!code-console[Main](owin-startup-class-detection/samples/sample19.cmd)]

   <span data-ttu-id="9919a-171">В командном окне отобразится следующее:</span><span class="sxs-lookup"><span data-stu-id="9919a-171">The command window will show:</span></span>

    [!code-console[Main](owin-startup-class-detection/samples/sample20.cmd)]
4. <span data-ttu-id="9919a-172">Запустите браузер с URL-адресом `http://localhost:5000/`.</span><span class="sxs-lookup"><span data-stu-id="9919a-172">Launch a browser with the URL `http://localhost:5000/`.</span></span>

    ![](owin-startup-class-detection/_static/image8.png)

   <span data-ttu-id="9919a-173">Овинхост учитывает приведенные выше соглашения о запуске.</span><span class="sxs-lookup"><span data-stu-id="9919a-173">OwinHost honored the startup conventions listed above.</span></span>
5. <span data-ttu-id="9919a-174">В окне командной строки нажмите клавишу ВВОД, чтобы выйти из Овинхост.</span><span class="sxs-lookup"><span data-stu-id="9919a-174">In the command window, press Enter to exit OwinHost.</span></span>
6. <span data-ttu-id="9919a-175">В классе `ProductionStartup` добавьте следующий атрибут Овинстартуп, указывающий понятное имя *продуктионконфигуратион*.</span><span class="sxs-lookup"><span data-stu-id="9919a-175">In the `ProductionStartup` class, add the following OwinStartup attribute which specifies a friendly name of *ProductionConfiguration*.</span></span>

    [!code-csharp[Main](owin-startup-class-detection/samples/sample21.cs)]
7. <span data-ttu-id="9919a-176">В командной строке введите:</span><span class="sxs-lookup"><span data-stu-id="9919a-176">In the command prompt and type:</span></span>

    [!code-console[Main](owin-startup-class-detection/samples/sample22.cmd)]

   <span data-ttu-id="9919a-177">Загружается класс рабочего запуска.</span><span class="sxs-lookup"><span data-stu-id="9919a-177">The Production startup class is loaded.</span></span>
    ![](owin-startup-class-detection/_static/image9.png)

   <span data-ttu-id="9919a-178">Наше приложение имеет несколько классов запуска, и в этом примере мы отложили, какой класс запуска будет загружаться до выполнения.</span><span class="sxs-lookup"><span data-stu-id="9919a-178">Our application has multiple startup classes, and in this example we have deferred which startup class to load until runtime.</span></span>
8. <span data-ttu-id="9919a-179">Проверьте следующие параметры запуска среды выполнения:</span><span class="sxs-lookup"><span data-stu-id="9919a-179">Test the following runtime startup options:</span></span>

    [!code-console[Main](owin-startup-class-detection/samples/sample23.cmd)]
