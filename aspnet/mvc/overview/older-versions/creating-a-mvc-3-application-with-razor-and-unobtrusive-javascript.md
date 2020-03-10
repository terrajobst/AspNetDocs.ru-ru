---
uid: mvc/overview/older-versions/creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript
title: Создание приложения MVC 3 с помощью Razor и ненавязчивого JavaScript | Документация Майкрософт
author: microsoft
description: Пример веб-приложения "список пользователей" демонстрирует, как просто создавать приложения ASP.NET MVC 3 с помощью подсистемы представлений Razor. Пример приложения s...
ms.author: riande
ms.date: 11/01/2010
ms.assetid: 658b149b-d770-46bf-8b4b-4e47cca242f3
msc.legacyurl: /mvc/overview/older-versions/creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript
msc.type: authoredcontent
ms.openlocfilehash: fb63493ff22c9261fc5746a998a32f2511141f87
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78435000"
---
# <a name="creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript"></a><span data-ttu-id="a60ed-104">Создание приложения на MVC 3 с помощью Razor и ненавязчивого JavaScript</span><span class="sxs-lookup"><span data-stu-id="a60ed-104">Creating a MVC 3 Application with Razor and Unobtrusive JavaScript</span></span>

<span data-ttu-id="a60ed-105">по [Майкрософт](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="a60ed-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="a60ed-106">Пример веб-приложения "список пользователей" демонстрирует, как просто создавать приложения ASP.NET MVC 3 с помощью подсистемы представлений Razor.</span><span class="sxs-lookup"><span data-stu-id="a60ed-106">The User List sample web application demonstrates how simple it is to create ASP.NET MVC 3 applications using the Razor view engine.</span></span> <span data-ttu-id="a60ed-107">В примере приложения показано, как использовать новый модуль представлений Razor с ASP.NET MVC версии 3 и Visual Studio 2010 для создания вымышленного веб-сайта списка пользователей, который включает такие функции, как создание, отображение, изменение и удаление пользователей.</span><span class="sxs-lookup"><span data-stu-id="a60ed-107">The sample application shows how to use the new Razor view engine with ASP.NET MVC version 3 and Visual Studio 2010 to create a fictional User List website that includes functionality such as creating, displaying, editing, and deleting users.</span></span>
> 
> <span data-ttu-id="a60ed-108">В этом учебнике описываются шаги, которые были выполнены для создания примера приложения ASP.NET MVC 3 в списке пользователей.</span><span class="sxs-lookup"><span data-stu-id="a60ed-108">This tutorial describes the steps that were taken in order to build the User List sample ASP.NET MVC 3 application.</span></span> <span data-ttu-id="a60ed-109">Проект Visual Studio с C# исходным кодом VB можно найти в этой статье: [download](https://code.msdn.microsoft.com/aspnetmvcsamples/Release/ProjectReleases.aspx?ReleaseId=5114).</span><span class="sxs-lookup"><span data-stu-id="a60ed-109">A Visual Studio project with C# and VB source code is available to accompany this topic: [Download](https://code.msdn.microsoft.com/aspnetmvcsamples/Release/ProjectReleases.aspx?ReleaseId=5114).</span></span> <span data-ttu-id="a60ed-110">Если у вас возникли вопросы по этому учебнику, опубликуйте их на [форуме MVC](https://forums.asp.net/1146.aspx).</span><span class="sxs-lookup"><span data-stu-id="a60ed-110">If you have questions about this tutorial, please post them to the [MVC forum](https://forums.asp.net/1146.aspx).</span></span>

## <a name="overview"></a><span data-ttu-id="a60ed-111">Обзор</span><span class="sxs-lookup"><span data-stu-id="a60ed-111">Overview</span></span>

<span data-ttu-id="a60ed-112">Создаваемое приложение — это простой веб-сайт списка пользователей.</span><span class="sxs-lookup"><span data-stu-id="a60ed-112">The application you'll be building is a simple user list website.</span></span> <span data-ttu-id="a60ed-113">Пользователи могут вводить, просматривать и обновлять сведения о пользователях.</span><span class="sxs-lookup"><span data-stu-id="a60ed-113">Users can enter, view, and update user information.</span></span>

![Образец сайта](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image1.png)

<span data-ttu-id="a60ed-115">Вы можете скачать VB и C# готовый проект [здесь](https://code.msdn.microsoft.com/Creating-a-MVC-3-28883c0f).</span><span class="sxs-lookup"><span data-stu-id="a60ed-115">You can download the VB and C# completed project [here](https://code.msdn.microsoft.com/Creating-a-MVC-3-28883c0f).</span></span>

## <a name="creating-the-web-application"></a><span data-ttu-id="a60ed-116">Создание веб-приложения</span><span class="sxs-lookup"><span data-stu-id="a60ed-116">Creating the Web Application</span></span>

<span data-ttu-id="a60ed-117">Чтобы начать работу с руководством, откройте Visual Studio 2010 и создайте новый проект с помощью шаблона *веб-приложения ASP.NET MVC 3* .</span><span class="sxs-lookup"><span data-stu-id="a60ed-117">To start the tutorial, open Visual Studio 2010 and create a new project using the *ASP.NET MVC 3 Web Application* template.</span></span> <span data-ttu-id="a60ed-118">Присвойте приложению имя &quot;Mvc3Razor&quot;.</span><span class="sxs-lookup"><span data-stu-id="a60ed-118">Name the application &quot;Mvc3Razor&quot;.</span></span>

<span data-ttu-id="a60ed-119">[![новый проект MVC 3](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image3.png)](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image2.png)</span><span class="sxs-lookup"><span data-stu-id="a60ed-119">[![New MVC 3 project](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image3.png)](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image2.png)</span></span>

<span data-ttu-id="a60ed-120">В диалоговом окне **Новый проект ASP.NET MVC 3** выберите **Интернет приложение**, выберите подсистему представлений Razor и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="a60ed-120">In the **New ASP.NET MVC 3 Project** dialog, select **Internet Application**, select the Razor view engine, and then click **OK**.</span></span>

![Диалоговое окно создания проекта ASP.NET MVC 3](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image4.png)

<span data-ttu-id="a60ed-122">В этом учебнике вы не будете использовать поставщик членства ASP.NET, поэтому вы можете удалить все файлы, связанные с входом и членством.</span><span class="sxs-lookup"><span data-stu-id="a60ed-122">In this tutorial you will not be using the ASP.NET membership provider, so you can delete all the files associated with logon and membership.</span></span> <span data-ttu-id="a60ed-123">В **Обозреватель решений**удалите следующие файлы и каталоги:</span><span class="sxs-lookup"><span data-stu-id="a60ed-123">In **Solution Explorer**, remove the following files and directories:</span></span>

- <span data-ttu-id="a60ed-124">*контроллерс\аккаунтконтроллер*</span><span class="sxs-lookup"><span data-stu-id="a60ed-124">*Controllers\AccountController*</span></span>
- <span data-ttu-id="a60ed-125">*моделс\аккаунтмоделс*</span><span class="sxs-lookup"><span data-stu-id="a60ed-125">*Models\AccountModels*</span></span>
- <span data-ttu-id="a60ed-126">*Views\Shared\\_LogOnPartial*</span><span class="sxs-lookup"><span data-stu-id="a60ed-126">*Views\Shared\\_LogOnPartial*</span></span>
- <span data-ttu-id="a60ed-127">*Виевс\аккаунт* (и все файлы в этом каталоге)</span><span class="sxs-lookup"><span data-stu-id="a60ed-127">*Views\Account* (and all the files in this directory)</span></span>

![Солн exp](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image5.png)

<span data-ttu-id="a60ed-129">Измените файл <em>\_Layout. cshtml</em> и замените разметку внутри элемента `<div>` с именем `logindisplay` на сообщение <em>&quot;</em>login Disabled&quot;.</span><span class="sxs-lookup"><span data-stu-id="a60ed-129">Edit the <em>\_Layout.cshtml</em> file and replace the markup inside the `<div>` element named `logindisplay` with the message <em>&quot;</em>Login Disabled&quot;.</span></span> <span data-ttu-id="a60ed-130">В следующем примере показана новая разметка:</span><span class="sxs-lookup"><span data-stu-id="a60ed-130">The following example shows the new markup:</span></span>

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample1.cshtml)]

## <a name="adding-the-model"></a><span data-ttu-id="a60ed-131">Добавление модели</span><span class="sxs-lookup"><span data-stu-id="a60ed-131">Adding the Model</span></span>

<span data-ttu-id="a60ed-132">В **Обозреватель решений**щелкните правой кнопкой мыши папку *модели* , выберите **добавить**, а затем выберите **класс**.</span><span class="sxs-lookup"><span data-stu-id="a60ed-132">In **Solution Explorer**, right-click the *Models* folder, select **Add**, and then click **Class**.</span></span>

![Новый класс пользовательского MDL](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image6.png)

<span data-ttu-id="a60ed-134">Назовите класс `UserModel`.</span><span class="sxs-lookup"><span data-stu-id="a60ed-134">Name the class `UserModel`.</span></span> <span data-ttu-id="a60ed-135">Замените содержимое файла *усермодел* следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="a60ed-135">Replace the contents of the *UserModel* file with the following code:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample2.cs)]

<span data-ttu-id="a60ed-136">Класс `UserModel` представляет пользователей.</span><span class="sxs-lookup"><span data-stu-id="a60ed-136">The `UserModel` class represents users.</span></span> <span data-ttu-id="a60ed-137">Каждый член класса снабжается атрибутом [Required](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx) из пространства имен [Annotations](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx) .</span><span class="sxs-lookup"><span data-stu-id="a60ed-137">Each member of the class is annotated with the [Required](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx) attribute from the [DataAnnotations](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx) namespace.</span></span> <span data-ttu-id="a60ed-138">Атрибуты в пространстве имен [Annotations](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx) обеспечивают автоматическую проверку на стороне клиента и сервера для веб-приложений.</span><span class="sxs-lookup"><span data-stu-id="a60ed-138">The attributes in the [DataAnnotations](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx) namespace provide automatic client- and server-side validation for web applications.</span></span>

<span data-ttu-id="a60ed-139">Откройте класс `HomeController` и добавьте директиву `using`, чтобы получить доступ к классам `UserModel` и `Users`:</span><span class="sxs-lookup"><span data-stu-id="a60ed-139">Open the `HomeController` class and add a `using` directive so that you can access the `UserModel` and `Users` classes:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample3.cs)]

<span data-ttu-id="a60ed-140">Сразу после объявления `HomeController` добавьте следующий комментарий и ссылку на `Users` класс:</span><span class="sxs-lookup"><span data-stu-id="a60ed-140">Just after the `HomeController` declaration, add the following comment and the reference to a `Users` class:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample4.cs)]

<span data-ttu-id="a60ed-141">Класс `Users` — это упрощенное хранилище данных в памяти, которое будет использоваться в этом руководстве.</span><span class="sxs-lookup"><span data-stu-id="a60ed-141">The `Users` class is a simplified, in-memory data store that you'll use in this tutorial.</span></span> <span data-ttu-id="a60ed-142">В реальных приложениях для хранения сведений о пользователях используется база данных.</span><span class="sxs-lookup"><span data-stu-id="a60ed-142">In a real application you would use a database to store user information.</span></span> <span data-ttu-id="a60ed-143">Первые несколько строк файла `HomeController` показаны в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="a60ed-143">The first few lines of the `HomeController` file are shown in the following example:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample5.cs)]

<span data-ttu-id="a60ed-144">Создайте приложение, чтобы модель пользователя была доступна в мастере формирования шаблонов на следующем шаге.</span><span class="sxs-lookup"><span data-stu-id="a60ed-144">Build the application so that the user model will be available to the scaffolding wizard in the next step.</span></span>

## <a name="creating-the-default-view"></a><span data-ttu-id="a60ed-145">Создание представления по умолчанию</span><span class="sxs-lookup"><span data-stu-id="a60ed-145">Creating the Default View</span></span>

<span data-ttu-id="a60ed-146">Следующим шагом является Добавление метода действия и представления для отображения пользователей.</span><span class="sxs-lookup"><span data-stu-id="a60ed-146">The next step is to add an action method and view to display the users.</span></span>

<span data-ttu-id="a60ed-147">Удалите существующий файл *виевс\хоме\индекс* .</span><span class="sxs-lookup"><span data-stu-id="a60ed-147">Delete the existing *Views\Home\Index* file.</span></span> <span data-ttu-id="a60ed-148">Вы создадите новый файл *индекса* для просмотра пользователей.</span><span class="sxs-lookup"><span data-stu-id="a60ed-148">You will create a new *Index* file to display the users.</span></span>

<span data-ttu-id="a60ed-149">В классе `HomeController` замените содержимое метода `Index` следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="a60ed-149">In the `HomeController` class, replace the contents of the `Index` method with the following code:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample6.cs)]

<span data-ttu-id="a60ed-150">Щелкните правой кнопкой мыши внутри метода `Index` и выберите **Добавить представление**.</span><span class="sxs-lookup"><span data-stu-id="a60ed-150">Right-click inside the `Index` method and then click **Add View**.</span></span>

![Добавить представление](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image7.png)

<span data-ttu-id="a60ed-152">Выберите параметр **создать строго типизированное представление** .</span><span class="sxs-lookup"><span data-stu-id="a60ed-152">Select the **Create a strongly-typed view** option.</span></span> <span data-ttu-id="a60ed-153">В качестве **класса данных представления**выберите **Mvc3Razor. Models. усермодел**.</span><span class="sxs-lookup"><span data-stu-id="a60ed-153">For **View data class**, select **Mvc3Razor.Models.UserModel**.</span></span> <span data-ttu-id="a60ed-154">(Если в поле **класс представления** не отображается **Mvc3Razor. Models. усермодел** , необходимо выполнить сборку проекта.) Убедитесь, что для обработчика представлений задано значение **Razor**.</span><span class="sxs-lookup"><span data-stu-id="a60ed-154">(If you don't see **Mvc3Razor.Models.UserModel** in the **View data class** box, you need to build the project.) Make sure that the view engine is set to **Razor**.</span></span> <span data-ttu-id="a60ed-155">Задайте для параметра **Просмотреть содержимое** значение **список** и нажмите кнопку **добавить**.</span><span class="sxs-lookup"><span data-stu-id="a60ed-155">Set **View content** to **List** and then click **Add**.</span></span>

![Добавить представление индекса](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image8.png)

<span data-ttu-id="a60ed-157">Новое представление автоматически формирует формирование шаблонов пользовательских данных, которые передаются в представление `Index`.</span><span class="sxs-lookup"><span data-stu-id="a60ed-157">The new view automatically scaffolds the user data that's passed to the `Index` view.</span></span> <span data-ttu-id="a60ed-158">Изучите только что созданный файл *виевс\хоме\индекс* .</span><span class="sxs-lookup"><span data-stu-id="a60ed-158">Examine the newly generated *Views\Home\Index* file.</span></span> <span data-ttu-id="a60ed-159">Ссылки **создать**, **изменить**, **Подробности**и **Удалить** не работают, но остальная часть страницы функционирует.</span><span class="sxs-lookup"><span data-stu-id="a60ed-159">The **Create New**, **Edit**, **Details**, and **Delete** links don't work, but the rest of the page is functional.</span></span> <span data-ttu-id="a60ed-160">Запустите страницу.</span><span class="sxs-lookup"><span data-stu-id="a60ed-160">Run the page.</span></span> <span data-ttu-id="a60ed-161">Отобразится список пользователей.</span><span class="sxs-lookup"><span data-stu-id="a60ed-161">You see a list of users.</span></span>

![Страница индекса](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image9.png)

<span data-ttu-id="a60ed-163">Откройте файл *index. cshtml* и замените разметку `ActionLink` для **Edit**, **Details**и **Delete** следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="a60ed-163">Open the *Index.cshtml* file and replace the `ActionLink` markup for **Edit**, **Details**, and **Delete** with the following code:</span></span>

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample7.cshtml)]

<span data-ttu-id="a60ed-164">Имя пользователя используется в качестве идентификатора для поиска выбранной записи в ссылках **Edit**, **Details**и **Delete** .</span><span class="sxs-lookup"><span data-stu-id="a60ed-164">The user name is used as the ID to find the selected record in the **Edit**, **Details**, and **Delete** links.</span></span>

## <a name="creating-the-details-view"></a><span data-ttu-id="a60ed-165">Создание представления сведений</span><span class="sxs-lookup"><span data-stu-id="a60ed-165">Creating the Details View</span></span>

<span data-ttu-id="a60ed-166">Следующим шагом является Добавление метода действия `Details` и представления для отображения сведений о пользователе.</span><span class="sxs-lookup"><span data-stu-id="a60ed-166">The next step is to add a `Details` action method and view in order to display user details.</span></span>

![Сведения](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image10.png)

<span data-ttu-id="a60ed-168">Добавьте следующий метод `Details` к контроллеру Home:</span><span class="sxs-lookup"><span data-stu-id="a60ed-168">Add the following `Details` method to the home controller:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample8.cs)]

<span data-ttu-id="a60ed-169">Щелкните правой кнопкой мыши внутри метода `Details` и выберите <strong>Добавить представление</strong>.</span><span class="sxs-lookup"><span data-stu-id="a60ed-169">Right-click inside the `Details` method and then select <strong>Add View</strong>.</span></span> <span data-ttu-id="a60ed-170">Убедитесь, что поле <strong>класс данных представления</strong> содержит <strong>Mvc3Razor. Models. усермодел</strong><em>.</em></span><span class="sxs-lookup"><span data-stu-id="a60ed-170">Verify that the <strong>View data class</strong> box contains <strong>Mvc3Razor.Models.UserModel</strong><em>.</em></span></span> <span data-ttu-id="a60ed-171">Задайте <strong>сведения о</strong> <strong>содержимом представления</strong> и нажмите кнопку <strong>добавить</strong>.</span><span class="sxs-lookup"><span data-stu-id="a60ed-171">Set <strong>View content</strong> to <strong>Details</strong> and then click <strong>Add</strong>.</span></span>

![Добавить представление сведений](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image11.png)

<span data-ttu-id="a60ed-173">Запустите приложение и выберите ссылку сведения.</span><span class="sxs-lookup"><span data-stu-id="a60ed-173">Run the application and select a details link.</span></span> <span data-ttu-id="a60ed-174">При автоматическом формировании шаблонов отображается каждое свойство модели.</span><span class="sxs-lookup"><span data-stu-id="a60ed-174">The automatic scaffolding shows each property in the model.</span></span>

![Сведения](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image12.png)

## <a name="creating-the-edit-view"></a><span data-ttu-id="a60ed-176">Создание представления редактирования</span><span class="sxs-lookup"><span data-stu-id="a60ed-176">Creating the Edit View</span></span>

<span data-ttu-id="a60ed-177">Добавьте следующий метод `Edit` в контроллер Home.</span><span class="sxs-lookup"><span data-stu-id="a60ed-177">Add the following `Edit` method to the home controller.</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample9.cs)]

<span data-ttu-id="a60ed-178">Добавьте представление, как в предыдущих шагах, но задайте для параметра **Просмотр содержимого** значение **изменить**.</span><span class="sxs-lookup"><span data-stu-id="a60ed-178">Add a view as in the previous steps, but set **View content** to **Edit**.</span></span>

![Добавить представление редактирования](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image13.png)

<span data-ttu-id="a60ed-180">Запустите приложение и измените имя и фамилию одного из пользователей.</span><span class="sxs-lookup"><span data-stu-id="a60ed-180">Run the application and edit the first and last name of one of the users.</span></span> <span data-ttu-id="a60ed-181">При нарушении ограничений `DataAnnotation`, примененных к классу `UserModel`, при отправке формы будут отображаться ошибки проверки, вызванные кодом сервера.</span><span class="sxs-lookup"><span data-stu-id="a60ed-181">If you violate any `DataAnnotation` constraints that have been applied to the `UserModel` class, when you submit the form, you will see validation errors that are produced by server code.</span></span> <span data-ttu-id="a60ed-182">Например, если изменить имя &quot;Анна&quot; на &quot;&quot;, то при отправке формы в форме отобразится следующая ошибка:</span><span class="sxs-lookup"><span data-stu-id="a60ed-182">For example, if you change the first name &quot;Ann&quot; to &quot;A&quot;, when you submit the form, the following error is displayed on the form:</span></span>

`The field First Name must be a string with a minimum length of 3 and a maximum length of 8.`

<span data-ttu-id="a60ed-183">В этом руководстве вы имя пользователя в качестве первичного ключа.</span><span class="sxs-lookup"><span data-stu-id="a60ed-183">In this tutorial, you're treating the user name as the primary key.</span></span> <span data-ttu-id="a60ed-184">Поэтому свойство имени пользователя не может быть изменено.</span><span class="sxs-lookup"><span data-stu-id="a60ed-184">Therefore, the user name property cannot be changed.</span></span> <span data-ttu-id="a60ed-185">В файле *Edit. cshtml* сразу после инструкции `Html.BeginForm` задайте имя пользователя как скрытое поле.</span><span class="sxs-lookup"><span data-stu-id="a60ed-185">In the *Edit.cshtml* file, just after the `Html.BeginForm` statement, set the user name to be a hidden field.</span></span> <span data-ttu-id="a60ed-186">Это приводит к передаче свойства в модель.</span><span class="sxs-lookup"><span data-stu-id="a60ed-186">This causes the property to be passed in the model.</span></span> <span data-ttu-id="a60ed-187">В следующем фрагменте кода показано размещение оператора `Hidden`:</span><span class="sxs-lookup"><span data-stu-id="a60ed-187">The following code fragment shows the placement of the `Hidden` statement:</span></span>

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample10.cshtml)]

<span data-ttu-id="a60ed-188">Замените `TextBoxFor` и `ValidationMessageFor` разметку имени пользователя на вызов `DisplayFor`.</span><span class="sxs-lookup"><span data-stu-id="a60ed-188">Replace the `TextBoxFor` and `ValidationMessageFor` markup for the user name with a `DisplayFor` call.</span></span> <span data-ttu-id="a60ed-189">Метод `DisplayFor` отображает свойство как элемент только для чтения.</span><span class="sxs-lookup"><span data-stu-id="a60ed-189">The `DisplayFor` method displays the property as a read-only element.</span></span> <span data-ttu-id="a60ed-190">В следующем примере приведена полная разметка.</span><span class="sxs-lookup"><span data-stu-id="a60ed-190">The following example shows the completed markup.</span></span> <span data-ttu-id="a60ed-191">Первоначальные вызовы `TextBoxFor` и `ValidationMessageFor` заносятся в комментарий с помощью символов начала и конца комментария Razor (`@* *@`)</span><span class="sxs-lookup"><span data-stu-id="a60ed-191">The original `TextBoxFor` and `ValidationMessageFor` calls are commented out with the Razor begin-comment and end-comment characters (`@* *@`)</span></span>

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample11.cshtml)]

## <a name="enabling-client-side-validation"></a><span data-ttu-id="a60ed-192">Включение проверки на стороне клиента</span><span class="sxs-lookup"><span data-stu-id="a60ed-192">Enabling Client-Side Validation</span></span>

<span data-ttu-id="a60ed-193">Чтобы включить проверку на стороне клиента в ASP.NET MVC 3, необходимо установить два флага и включить три файла JavaScript.</span><span class="sxs-lookup"><span data-stu-id="a60ed-193">To enable client-side validation in ASP.NET MVC 3, you must set two flags and you must include three JavaScript files.</span></span>

<span data-ttu-id="a60ed-194">Откройте файл *Web. config* приложения.</span><span class="sxs-lookup"><span data-stu-id="a60ed-194">Open the application's *Web.config* file.</span></span> <span data-ttu-id="a60ed-195">Убедитесь, что в параметрах приложения `that ClientValidationEnabled` и `UnobtrusiveJavaScriptEnabled` установлены в значение true.</span><span class="sxs-lookup"><span data-stu-id="a60ed-195">Verify `that ClientValidationEnabled` and `UnobtrusiveJavaScriptEnabled` are set to true in the application settings.</span></span> <span data-ttu-id="a60ed-196">В следующем фрагменте из корневого файла *Web. config* отображаются правильные параметры:</span><span class="sxs-lookup"><span data-stu-id="a60ed-196">The following fragment from the root *Web.config* file shows the correct settings:</span></span>

[!code-xml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample12.xml)]

<span data-ttu-id="a60ed-197">Установка значения "true" `UnobtrusiveJavaScriptEnabled` "включает ненавязчивую проверку AJAX и незаметное клиентская проверка.</span><span class="sxs-lookup"><span data-stu-id="a60ed-197">Setting `UnobtrusiveJavaScriptEnabled` to true enables unobtrusive Ajax and unobtrusive client validation.</span></span> <span data-ttu-id="a60ed-198">При использовании ненавязчивой проверки правила проверки преобразуются в атрибуты HTML5.</span><span class="sxs-lookup"><span data-stu-id="a60ed-198">When you use unobtrusive validation, the validation rules are turned into HTML5 attributes.</span></span> <span data-ttu-id="a60ed-199">Имена атрибутов HTML5 могут состоять только из строчных букв, цифр и дефисов.</span><span class="sxs-lookup"><span data-stu-id="a60ed-199">HTML5 attribute names can consist of only lowercase letters, numbers, and dashes.</span></span>

<span data-ttu-id="a60ed-200">Установка значения true для `ClientValidationEnabled` включает проверку на стороне клиента.</span><span class="sxs-lookup"><span data-stu-id="a60ed-200">Setting `ClientValidationEnabled` to true enables client-side validation.</span></span> <span data-ttu-id="a60ed-201">Настроив эти ключи в файле *Web. config* приложения, вы включите проверку клиента и ненавязчивый JavaScript для всего приложения.</span><span class="sxs-lookup"><span data-stu-id="a60ed-201">By setting these keys in the application *Web.config* file, you enable client validation and unobtrusive JavaScript for the entire application.</span></span> <span data-ttu-id="a60ed-202">Можно также включить или отключить эти параметры в отдельных представлениях или в методах контроллера, используя следующий код:</span><span class="sxs-lookup"><span data-stu-id="a60ed-202">You can also enable or disable these settings in individual views or in controller methods using the following code:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample13.cs)]

<span data-ttu-id="a60ed-203">Кроме того, в представление, подготовленное для просмотра, необходимо включить несколько файлов JavaScript.</span><span class="sxs-lookup"><span data-stu-id="a60ed-203">You also need to include several JavaScript files in the rendered view.</span></span> <span data-ttu-id="a60ed-204">Простой способ включить JavaScript во все представления — добавить их в файл *Views\Shared\\_layout. cshtml* .</span><span class="sxs-lookup"><span data-stu-id="a60ed-204">An easy way to include the JavaScript in all views is to add them to the *Views\Shared\\_Layout.cshtml* file.</span></span> <span data-ttu-id="a60ed-205">Замените\_элемент `<head>` файла *Layout. cshtml* следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="a60ed-205">Replace the `<head>` element of the *\_Layout.cshtml* file with the following code:</span></span>

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample14.cshtml)]

<span data-ttu-id="a60ed-206">Первые два сценария jQuery размещаются в сети доставки содержимого (CDN) Microsoft AJAX.</span><span class="sxs-lookup"><span data-stu-id="a60ed-206">The first two jQuery scripts are hosted by the Microsoft Ajax Content Delivery Network (CDN).</span></span> <span data-ttu-id="a60ed-207">Используя преимущества сети доставки содержимого Microsoft AJAX, вы можете значительно повысить производительность ваших приложений при первом нажатии.</span><span class="sxs-lookup"><span data-stu-id="a60ed-207">By taking advantage of the Microsoft Ajax CDN, you can significantly improve the first-hit performance of your applications.</span></span>

<span data-ttu-id="a60ed-208">Запустите приложение и щелкните ссылку Edit (изменить).</span><span class="sxs-lookup"><span data-stu-id="a60ed-208">Run the application and click an edit link.</span></span> <span data-ttu-id="a60ed-209">Просмотрите исходный код страницы в браузере.</span><span class="sxs-lookup"><span data-stu-id="a60ed-209">View the page's source in the browser.</span></span> <span data-ttu-id="a60ed-210">В источнике обозревателя показано множество атрибутов формы `data-val` (для проверки данных).</span><span class="sxs-lookup"><span data-stu-id="a60ed-210">The browser source shows many attributes of the form `data-val` (for data validation).</span></span> <span data-ttu-id="a60ed-211">Если проверка клиента и ненавязчивый JavaScript включены, поля ввода с правилом проверки клиента содержат атрибут `data-val="true"`, чтобы активировать ненавязчивую проверку клиента.</span><span class="sxs-lookup"><span data-stu-id="a60ed-211">When client validation and unobtrusive JavaScript is enabled, input fields with a client-validation rule contain the `data-val="true"` attribute to trigger unobtrusive client validation.</span></span> <span data-ttu-id="a60ed-212">Например, поле `City` в модели было дополнено [требуемым](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx) атрибутом, результатом которого является код HTML, показанный в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="a60ed-212">For example, the `City` field in the model was decorated with the [Required](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx) attribute, which results in the HTML shown in the following example:</span></span>

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample15.cshtml)]

<span data-ttu-id="a60ed-213">Для каждого правила проверки клиента добавляется атрибут, имеющий форму `data-val-rulename="message"`.</span><span class="sxs-lookup"><span data-stu-id="a60ed-213">For each client-validation rule, an attribute is added that has the form `data-val-rulename="message"`.</span></span> <span data-ttu-id="a60ed-214">Используя приведенный ранее пример поля `City`, необходимое правило проверки клиента создает атрибут `data-val-required` и сообщение, &quot;поле City обязательно&quot;.</span><span class="sxs-lookup"><span data-stu-id="a60ed-214">Using the `City` field example shown earlier, the required client-validation rule generates the `data-val-required` attribute and the message &quot;The City field is required&quot;.</span></span> <span data-ttu-id="a60ed-215">Запустите приложение, измените одного из пользователей и очистите поле `City`.</span><span class="sxs-lookup"><span data-stu-id="a60ed-215">Run the application, edit one of the users, and clear the `City` field.</span></span> <span data-ttu-id="a60ed-216">При выходе из поля вы увидите сообщение об ошибке проверки на стороне клиента.</span><span class="sxs-lookup"><span data-stu-id="a60ed-216">When you tab out of the field, you see a client-side validation error message.</span></span>

![Требуется город](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image14.png)

<span data-ttu-id="a60ed-218">Аналогичным образом для каждого параметра в правиле проверки клиента добавляется атрибут, имеющий форму `data-val-rulename-paramname=paramvalue`.</span><span class="sxs-lookup"><span data-stu-id="a60ed-218">Similarly, for each parameter in the client-validation rule, an attribute is added that has the form `data-val-rulename-paramname=paramvalue`.</span></span> <span data-ttu-id="a60ed-219">Например, свойство `FirstName` записывается атрибутом [StringLength](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx) и задает минимальную длину, равную 3, и максимальную длину 8.</span><span class="sxs-lookup"><span data-stu-id="a60ed-219">For example, the `FirstName` property is annotated with the [StringLength](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx) attribute and specifies a minimum length of 3 and a maximum length of 8.</span></span> <span data-ttu-id="a60ed-220">Правило проверки данных с именем `length` имеет имя параметра `max` и значение параметра 8.</span><span class="sxs-lookup"><span data-stu-id="a60ed-220">The data validation rule named `length` has the parameter name `max` and the parameter value 8.</span></span> <span data-ttu-id="a60ed-221">Ниже показан код HTML, созданный для поля `FirstName` при изменении одного из пользователей.</span><span class="sxs-lookup"><span data-stu-id="a60ed-221">The following shows the HTML that is generated for the `FirstName` field when you edit one of the users:</span></span>

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample16.cshtml)]

<span data-ttu-id="a60ed-222">Дополнительные сведения о ненавязчивой проверке клиента см. в блоге Михаил Уилсон (, посвященном записи [ненавязчивой проверки клиента в ASP.NET MVC 3](http://bradwilson.typepad.com/blog/2010/10/mvc3-unobtrusive-validation.html) .</span><span class="sxs-lookup"><span data-stu-id="a60ed-222">For more information about unobtrusive client validation, see the entry [Unobtrusive Client Validation in ASP.NET MVC 3](http://bradwilson.typepad.com/blog/2010/10/mvc3-unobtrusive-validation.html) in Brad Wilson's blog.</span></span>

> [!NOTE]
> <span data-ttu-id="a60ed-223">В бета-версии ASP.NET MVC 3 иногда необходимо отправить форму, чтобы начать проверку на стороне клиента.</span><span class="sxs-lookup"><span data-stu-id="a60ed-223">In ASP.NET MVC 3 Beta, you sometimes need to submit the form in order to start client-side validation.</span></span> <span data-ttu-id="a60ed-224">Это может быть изменено для окончательного выпуска.</span><span class="sxs-lookup"><span data-stu-id="a60ed-224">This might be changed for the final release.</span></span>

## <a name="creating-the-create-view"></a><span data-ttu-id="a60ed-225">Создание представления создания</span><span class="sxs-lookup"><span data-stu-id="a60ed-225">Creating the Create View</span></span>

<span data-ttu-id="a60ed-226">Следующим шагом является Добавление метода действия `Create` и представления, чтобы позволить пользователю создать нового пользователя.</span><span class="sxs-lookup"><span data-stu-id="a60ed-226">The next step is to add a `Create` action method and view in order to enable the user to create a new user.</span></span> <span data-ttu-id="a60ed-227">Добавьте следующий метод `Create` к контроллеру Home:</span><span class="sxs-lookup"><span data-stu-id="a60ed-227">Add the following `Create` method to the home controller:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample17.cs)]

<span data-ttu-id="a60ed-228">Добавьте представление, как в предыдущих шагах, но задайте для параметра **представление содержимое** значение **создать**.</span><span class="sxs-lookup"><span data-stu-id="a60ed-228">Add a view as in the previous steps, but set **View content** to **Create**.</span></span>

![Создание представления](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image15.png)

<span data-ttu-id="a60ed-230">Запустите приложение, выберите ссылку **создать** и добавьте нового пользователя.</span><span class="sxs-lookup"><span data-stu-id="a60ed-230">Run the application, select the **Create** link, and add a new user.</span></span> <span data-ttu-id="a60ed-231">Метод `Create` автоматически использует преимущества проверки на стороне клиента и на стороне сервера.</span><span class="sxs-lookup"><span data-stu-id="a60ed-231">The `Create` method automatically takes advantage of client-side and server-side validation.</span></span> <span data-ttu-id="a60ed-232">Попробуйте ввести имя пользователя, содержащее пробелы, например &quot;Бен X&quot;.</span><span class="sxs-lookup"><span data-stu-id="a60ed-232">Try to enter a user name that contains white space, such as &quot;Ben X&quot;.</span></span> <span data-ttu-id="a60ed-233">При выходе из поля "имя пользователя" отображается ошибка проверки на стороне клиента (`White space is not allowed`).</span><span class="sxs-lookup"><span data-stu-id="a60ed-233">When you tab out of the user name field, a client-side validation error (`White space is not allowed`) is displayed.</span></span>

## <a name="add-the-delete-method"></a><span data-ttu-id="a60ed-234">Добавление метода Delete</span><span class="sxs-lookup"><span data-stu-id="a60ed-234">Add the Delete method</span></span>

<span data-ttu-id="a60ed-235">Чтобы завершить работу с этим руководством, добавьте следующий метод `Delete` к контроллеру Home:</span><span class="sxs-lookup"><span data-stu-id="a60ed-235">To complete the tutorial, add the following `Delete` method to the home controller:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample18.cs)]

<span data-ttu-id="a60ed-236">Добавьте `Delete` представление, как в предыдущих шагах, указав **содержимое представления** для **удаления**.</span><span class="sxs-lookup"><span data-stu-id="a60ed-236">Add a `Delete` view as in the previous steps, setting **View content** to **Delete**.</span></span>

![Удалить представление](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image16.png)

<span data-ttu-id="a60ed-238">Теперь у вас есть простое, но полностью функциональное приложение ASP.NET MVC 3 с проверкой.</span><span class="sxs-lookup"><span data-stu-id="a60ed-238">You now have a simple but fully functional ASP.NET MVC 3 application with validation.</span></span>
