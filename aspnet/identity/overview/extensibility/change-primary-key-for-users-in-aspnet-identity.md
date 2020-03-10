---
uid: identity/overview/extensibility/change-primary-key-for-users-in-aspnet-identity
title: Изменение первичного ключа для пользователей в ASP.NET Identity-ASP.NET 4. x
author: Rick-Anderson
description: В Visual Studio 2013 веб-приложение по умолчанию использует строковое значение для ключа учетных записей пользователей. ASP.NET Identity позволяет изменить тип...
ms.author: riande
ms.date: 09/30/2014
ms.assetid: 44925849-5762-4504-a8cd-8f0cd06f6dc3
ms.custom: seoapril2019
msc.legacyurl: /identity/overview/extensibility/change-primary-key-for-users-in-aspnet-identity
msc.type: authoredcontent
ms.openlocfilehash: 0afea8eacfc646f1489b87629fdb2d437815d88c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78472266"
---
# <a name="change-primary-key-for-users-in-aspnet-identity"></a><span data-ttu-id="9d3cb-104">Изменение первичного ключа для пользователей в ASP.NET Identity</span><span class="sxs-lookup"><span data-stu-id="9d3cb-104">Change Primary Key for Users in ASP.NET Identity</span></span>

<span data-ttu-id="9d3cb-105">от [Tom фитзмаккен](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="9d3cb-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="9d3cb-106">В Visual Studio 2013 веб-приложение по умолчанию использует строковое значение для ключа учетных записей пользователей.</span><span class="sxs-lookup"><span data-stu-id="9d3cb-106">In Visual Studio 2013, the default web application uses a string value for the key for user accounts.</span></span> <span data-ttu-id="9d3cb-107">ASP.NET Identity позволяет изменить тип ключа в соответствии с требованиями к данным.</span><span class="sxs-lookup"><span data-stu-id="9d3cb-107">ASP.NET Identity enables you to change the type of the key to meet your data requirements.</span></span> <span data-ttu-id="9d3cb-108">Например, можно изменить тип ключа с строки на целое число.</span><span class="sxs-lookup"><span data-stu-id="9d3cb-108">For example, you can change the type of the key from a string to an integer.</span></span>
> 
> <span data-ttu-id="9d3cb-109">В этом разделе показано, как начать работу с веб-приложением по умолчанию и изменить ключ учетной записи пользователя на целое число.</span><span class="sxs-lookup"><span data-stu-id="9d3cb-109">This topic shows how to start with the default web application and change the user account key to an integer.</span></span> <span data-ttu-id="9d3cb-110">Вы можете использовать те же изменения для реализации любого типа ключа в проекте.</span><span class="sxs-lookup"><span data-stu-id="9d3cb-110">You can use the same modifications to implement any type of key in your project.</span></span> <span data-ttu-id="9d3cb-111">В нем показано, как внести эти изменения в веб-приложение по умолчанию, но можно применить аналогичные изменения к настроенному приложению.</span><span class="sxs-lookup"><span data-stu-id="9d3cb-111">It shows how to make these changes in the default web application, but you could apply similar modifications to a customized application.</span></span> <span data-ttu-id="9d3cb-112">В нем отображаются изменения, необходимые при работе с MVC или веб-формами.</span><span class="sxs-lookup"><span data-stu-id="9d3cb-112">It shows the changes needed when working with MVC or Web Forms.</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="9d3cb-113">Версии программного обеспечения, используемые в этом руководстве</span><span class="sxs-lookup"><span data-stu-id="9d3cb-113">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="9d3cb-114">Visual Studio 2013 с обновлением 2 (или более поздней версии)</span><span class="sxs-lookup"><span data-stu-id="9d3cb-114">Visual Studio 2013 with Update 2 (or later)</span></span>
> - <span data-ttu-id="9d3cb-115">ASP.NET Identity 2,1 или более поздней версии</span><span class="sxs-lookup"><span data-stu-id="9d3cb-115">ASP.NET Identity 2.1 or later</span></span>

<span data-ttu-id="9d3cb-116">Для выполнения действий, описанных в этом руководстве, необходимо иметь Visual Studio 2013 обновление 2 (или более поздней версии) и веб-приложение, созданное из шаблона веб-приложения ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="9d3cb-116">To perform the steps in this tutorial, you must have Visual Studio 2013 Update 2 (or later), and a web application created from the ASP.NET Web Application template.</span></span> <span data-ttu-id="9d3cb-117">Шаблон изменен в обновлении 3.</span><span class="sxs-lookup"><span data-stu-id="9d3cb-117">The template changed in Update 3.</span></span> <span data-ttu-id="9d3cb-118">В этом разделе показано, как изменить шаблон в обновлении 2 и обновлении 3.</span><span class="sxs-lookup"><span data-stu-id="9d3cb-118">This topic shows how to change the template in Update 2 and Update 3.</span></span>

<span data-ttu-id="9d3cb-119">Этот раздел состоит из следующих подразделов.</span><span class="sxs-lookup"><span data-stu-id="9d3cb-119">This topic contains the following sections:</span></span>

- [<span data-ttu-id="9d3cb-120">Изменение типа ключа в классе удостоверений пользователя</span><span class="sxs-lookup"><span data-stu-id="9d3cb-120">Change the type of the key in the Identity user class</span></span>](#userclass)
- [<span data-ttu-id="9d3cb-121">Добавление настраиваемых классов удостоверений, использующих тип ключа</span><span class="sxs-lookup"><span data-stu-id="9d3cb-121">Add customized Identity classes that use the key type</span></span>](#customclass)
- [<span data-ttu-id="9d3cb-122">Изменение класса контекста и диспетчера пользователей для использования типа ключа</span><span class="sxs-lookup"><span data-stu-id="9d3cb-122">Change the context class and user manager to use the key type</span></span>](#context)
- [<span data-ttu-id="9d3cb-123">Изменение конфигурации запуска для использования типа ключа</span><span class="sxs-lookup"><span data-stu-id="9d3cb-123">Change start-up configuration to use the key type</span></span>](#startup)
- [<span data-ttu-id="9d3cb-124">Для MVC с обновлением 2 Измените AccountController, чтобы передать тип ключа.</span><span class="sxs-lookup"><span data-stu-id="9d3cb-124">For MVC with Update 2, change the AccountController to pass the key type</span></span>](#mvcupdate2)
- [<span data-ttu-id="9d3cb-125">Для MVC с обновлением 3 Измените AccountController и Манажеконтроллер, чтобы передать тип ключа.</span><span class="sxs-lookup"><span data-stu-id="9d3cb-125">For MVC with Update 3, change the AccountController and ManageController to pass the key type</span></span>](#mvcupdate3)
- [<span data-ttu-id="9d3cb-126">Для веб-форм с обновлением 2 изменение страниц учетной записи для передачи типа ключа</span><span class="sxs-lookup"><span data-stu-id="9d3cb-126">For Web Forms with Update 2, change Account pages to pass the key type</span></span>](#webformsupdate2)
- [<span data-ttu-id="9d3cb-127">Для веб-форм с обновлением 3 изменение страниц учетной записи для передачи типа ключа</span><span class="sxs-lookup"><span data-stu-id="9d3cb-127">For Web Forms with Update 3, change Account pages to pass the key type</span></span>](#webformsupdate3)
- [<span data-ttu-id="9d3cb-128">Запустить приложение</span><span class="sxs-lookup"><span data-stu-id="9d3cb-128">Run application</span></span>](#run)
- [<span data-ttu-id="9d3cb-129">Другие ресурсы</span><span class="sxs-lookup"><span data-stu-id="9d3cb-129">Other resources</span></span>](#other)

<a id="userclass"></a>
## <a name="change-the-type-of-the-key-in-the-identity-user-class"></a><span data-ttu-id="9d3cb-130">Изменение типа ключа в классе удостоверений пользователя</span><span class="sxs-lookup"><span data-stu-id="9d3cb-130">Change the type of the key in the Identity user class</span></span>

<span data-ttu-id="9d3cb-131">В проекте, созданном из шаблона веб-приложения ASP.NET, укажите, что класс Аппликатионусер использует целое число для ключа учетных записей пользователей.</span><span class="sxs-lookup"><span data-stu-id="9d3cb-131">In your project created from the ASP.NET Web Application template, specify that the ApplicationUser class uses an integer for the key for user accounts.</span></span> <span data-ttu-id="9d3cb-132">В IdentityModels.cs измените класс Аппликатионусер, чтобы он наследовался от Идентитюсер, имеющего тип **int** для универсального параметра TKey.</span><span class="sxs-lookup"><span data-stu-id="9d3cb-132">In IdentityModels.cs, change the ApplicationUser class to inherit from IdentityUser that has a type of **int** for the TKey generic parameter.</span></span> <span data-ttu-id="9d3cb-133">Вы также передаете имена трех настраиваемых классов, которые еще не реализованы.</span><span class="sxs-lookup"><span data-stu-id="9d3cb-133">You also pass the names of three customized class which you have not implemented yet.</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample1.cs?highlight=1-2)]

<span data-ttu-id="9d3cb-134">Вы изменили тип ключа, но по умолчанию остальная часть приложения по-прежнему предполагает, что ключ является строкой.</span><span class="sxs-lookup"><span data-stu-id="9d3cb-134">You have changed the type of the key, but, by default, the rest of the application still assumes the key is a string.</span></span> <span data-ttu-id="9d3cb-135">Необходимо явно указать тип ключа в коде, который предполагает наличие строки.</span><span class="sxs-lookup"><span data-stu-id="9d3cb-135">You must explicitly indicate the type of the key in code that assumes a string.</span></span>

<span data-ttu-id="9d3cb-136">В классе **аппликатионусер** измените метод **женератеусеридентитясинк** , чтобы включить int, как показано в выделенном ниже коде.</span><span class="sxs-lookup"><span data-stu-id="9d3cb-136">In the **ApplicationUser** class, change the **GenerateUserIdentityAsync** method to include int, as shown in the highlighted code below.</span></span> <span data-ttu-id="9d3cb-137">Это изменение не требуется для проектов веб-форм с шаблоном обновления 3.</span><span class="sxs-lookup"><span data-stu-id="9d3cb-137">This change is not necessary for Web Forms projects with the Update 3 template.</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample2.cs?highlight=2)]

<a id="customclass"></a>
## <a name="add-customized-identity-classes-that-use-the-key-type"></a><span data-ttu-id="9d3cb-138">Добавление настраиваемых классов удостоверений, использующих тип ключа</span><span class="sxs-lookup"><span data-stu-id="9d3cb-138">Add customized Identity classes that use the key type</span></span>

<span data-ttu-id="9d3cb-139">Другие классы удостоверений, такие как Идентитюсерроле, Идентитюсерклаим, Идентитюсерлогин, Идентитироле, UserStore, Ролесторе, по-прежнему настраиваются на использование строкового ключа.</span><span class="sxs-lookup"><span data-stu-id="9d3cb-139">The other Identity classes, such as IdentityUserRole, IdentityUserClaim, IdentityUserLogin, IdentityRole, UserStore, RoleStore, are still set up to use a string key.</span></span> <span data-ttu-id="9d3cb-140">Создайте новые версии этих классов, которые указывают целочисленное значение для ключа.</span><span class="sxs-lookup"><span data-stu-id="9d3cb-140">Create new versions of these classes that specify an integer for the key.</span></span> <span data-ttu-id="9d3cb-141">Вам не нужно предоставлять много кода реализации в этих классах, поэтому в основном просто устанавливается int в качестве ключа.</span><span class="sxs-lookup"><span data-stu-id="9d3cb-141">You do not need to provide much implementation code in these classes, you are primarily just setting int as the key.</span></span>

<span data-ttu-id="9d3cb-142">Добавьте следующие классы в файл IdentityModels.cs.</span><span class="sxs-lookup"><span data-stu-id="9d3cb-142">Add the following classes to your IdentityModels.cs file.</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample3.cs)]

<a id="context"></a>
## <a name="change-the-context-class-and-user-manager-to-use-the-key-type"></a><span data-ttu-id="9d3cb-143">Изменение класса контекста и диспетчера пользователей для использования типа ключа</span><span class="sxs-lookup"><span data-stu-id="9d3cb-143">Change the context class and user manager to use the key type</span></span>

<span data-ttu-id="9d3cb-144">В IdentityModels.cs измените определение класса **ApplicationDbContext** , чтобы использовать новые настраиваемые классы и **int** для ключа, как показано в выделенном коде.</span><span class="sxs-lookup"><span data-stu-id="9d3cb-144">In IdentityModels.cs, change the definition of the **ApplicationDbContext** class to use your new customized classes and an **int** for the key, as shown in the highlighted code.</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample4.cs?highlight=1-2)]

<span data-ttu-id="9d3cb-145">Параметр ThrowIfV1Schema больше не является допустимым в конструкторе.</span><span class="sxs-lookup"><span data-stu-id="9d3cb-145">The ThrowIfV1Schema parameter is no longer valid in the constructor.</span></span> <span data-ttu-id="9d3cb-146">Измените конструктор, чтобы он не передавал значение ThrowIfV1Schema.</span><span class="sxs-lookup"><span data-stu-id="9d3cb-146">Change the constructor so it does not pass a ThrowIfV1Schema value.</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample5.cs)]

<span data-ttu-id="9d3cb-147">Откройте IdentityConfig.cs и измените класс **аппликатионусерманжер** , чтобы использовать новый класс пользовательского хранилища для сохранения данных **и целое число для ключа** .</span><span class="sxs-lookup"><span data-stu-id="9d3cb-147">Open IdentityConfig.cs, and change the **ApplicationUserManger** class to use your new user store class for persisting data and an **int** for the key.</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample6.cs?highlight=1,3,12,14,32,37,48)]

<span data-ttu-id="9d3cb-148">В шаблоне обновления 3 необходимо изменить класс Аппликатионсигнинманажер.</span><span class="sxs-lookup"><span data-stu-id="9d3cb-148">In the Update 3 template, you must change the ApplicationSignInManager class.</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample7.cs?highlight=1)]

<a id="startup"></a>
## <a name="change-start-up-configuration-to-use-the-key-type"></a><span data-ttu-id="9d3cb-149">Изменение конфигурации запуска для использования типа ключа</span><span class="sxs-lookup"><span data-stu-id="9d3cb-149">Change start-up configuration to use the key type</span></span>

<span data-ttu-id="9d3cb-150">В Startup.Auth.cs замените код Онвалидатеидентити, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="9d3cb-150">In Startup.Auth.cs, replace the OnValidateIdentity code, as highlighted below.</span></span> <span data-ttu-id="9d3cb-151">Обратите внимание, что определение Жетусеридкаллбакк анализирует строковое значение в целое число.</span><span class="sxs-lookup"><span data-stu-id="9d3cb-151">Notice that the getUserIdCallback definition, parses the string value into an integer.</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample8.cs?highlight=7-12)]

<span data-ttu-id="9d3cb-152">Если проект не распознает универсальную реализацию метода **UserID** , может потребоваться обновить пакет NuGet ASP.NET Identity до версии 2,1.</span><span class="sxs-lookup"><span data-stu-id="9d3cb-152">If your project does not recognize the generic implementation of the **GetUserId** method, you may need to update the ASP.NET Identity NuGet package to version 2.1</span></span>

<span data-ttu-id="9d3cb-153">Вы внесли много изменений в классы инфраструктуры, используемые ASP.NET Identity.</span><span class="sxs-lookup"><span data-stu-id="9d3cb-153">You have made a lot of changes to the infrastructure classes used by ASP.NET Identity.</span></span> <span data-ttu-id="9d3cb-154">Если вы попытаетесь скомпилировать проект, вы увидите множество ошибок.</span><span class="sxs-lookup"><span data-stu-id="9d3cb-154">If you try compiling the project, you will notice a lot of errors.</span></span> <span data-ttu-id="9d3cb-155">К счастью, все остальные ошибки похожи.</span><span class="sxs-lookup"><span data-stu-id="9d3cb-155">Fortunately, the remaining errors are all similar.</span></span> <span data-ttu-id="9d3cb-156">Класс Identity ожидает для ключа целое число, но контроллер (или веб-форма) передает строковое значение.</span><span class="sxs-lookup"><span data-stu-id="9d3cb-156">The Identity class expects an integer for the key, but the controller (or Web Form) is passing a string value.</span></span> <span data-ttu-id="9d3cb-157">В каждом случае необходимо преобразовать строку в тип и целое число, вызвав метод GetString **&lt;int&gt;** .</span><span class="sxs-lookup"><span data-stu-id="9d3cb-157">In each case, you need to convert from a string to and integer by calling **GetUserId&lt;int&gt;**.</span></span> <span data-ttu-id="9d3cb-158">Вы можете работать со списком ошибок из компиляции или следовать приведенным ниже изменениям.</span><span class="sxs-lookup"><span data-stu-id="9d3cb-158">You can either work through the error list from compilation or follow the changes below.</span></span>

<span data-ttu-id="9d3cb-159">Остальные изменения зависят от типа создаваемого проекта и обновления, установленного в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9d3cb-159">The remaining changes depend on the type of project you are creating and which update you have installed in Visual Studio.</span></span> <span data-ttu-id="9d3cb-160">Вы можете перейти непосредственно к соответствующему разделу, перейдя по следующим ссылкам.</span><span class="sxs-lookup"><span data-stu-id="9d3cb-160">You can go directly to the relevant section through the following links</span></span>

- [<span data-ttu-id="9d3cb-161">Для MVC с обновлением 2 Измените AccountController, чтобы передать тип ключа.</span><span class="sxs-lookup"><span data-stu-id="9d3cb-161">For MVC with Update 2, change the AccountController to pass the key type</span></span>](#mvcupdate2)
- [<span data-ttu-id="9d3cb-162">Для MVC с обновлением 3 Измените AccountController и Манажеконтроллер, чтобы передать тип ключа.</span><span class="sxs-lookup"><span data-stu-id="9d3cb-162">For MVC with Update 3, change the AccountController and ManageController to pass the key type</span></span>](#mvcupdate3)
- [<span data-ttu-id="9d3cb-163">Для веб-форм с обновлением 2 изменение страниц учетной записи для передачи типа ключа</span><span class="sxs-lookup"><span data-stu-id="9d3cb-163">For Web Forms with Update 2, change Account pages to pass the key type</span></span>](#webformsupdate2)
- [<span data-ttu-id="9d3cb-164">Для веб-форм с обновлением 3 изменение страниц учетной записи для передачи типа ключа</span><span class="sxs-lookup"><span data-stu-id="9d3cb-164">For Web Forms with Update 3, change Account pages to pass the key type</span></span>](#webformsupdate3)

<a id="mvcupdate2"></a>
## <a name="for-mvc-with-update-2-change-the-accountcontroller-to-pass-the-key-type"></a><span data-ttu-id="9d3cb-165">Для MVC с обновлением 2 Измените AccountController, чтобы передать тип ключа.</span><span class="sxs-lookup"><span data-stu-id="9d3cb-165">For MVC with Update 2, change the AccountController to pass the key type</span></span>

<span data-ttu-id="9d3cb-166">Откройте файл AccountController.cs.</span><span class="sxs-lookup"><span data-stu-id="9d3cb-166">Open the AccountController.cs file.</span></span> <span data-ttu-id="9d3cb-167">Необходимо изменить следующие методы.</span><span class="sxs-lookup"><span data-stu-id="9d3cb-167">You need to change the following methods.</span></span>

<span data-ttu-id="9d3cb-168">Метод **конфирмемаил**</span><span class="sxs-lookup"><span data-stu-id="9d3cb-168">**ConfirmEmail** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample9.cs?highlight=1,3)]

<span data-ttu-id="9d3cb-169">Метод **отсвязи**</span><span class="sxs-lookup"><span data-stu-id="9d3cb-169">**Disassociate** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample10.cs?highlight=5,9)]

<span data-ttu-id="9d3cb-170">Метод **управления (манажеусервиевмодел)**</span><span class="sxs-lookup"><span data-stu-id="9d3cb-170">**Manage(ManageUserViewModel)** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample11.cs?highlight=11,17,41)]

<span data-ttu-id="9d3cb-171">Метод **линклогинкаллбакк**</span><span class="sxs-lookup"><span data-stu-id="9d3cb-171">**LinkLoginCallback** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample12.cs?highlight=10)]

<span data-ttu-id="9d3cb-172">Метод **ремовеаккаунтлист**</span><span class="sxs-lookup"><span data-stu-id="9d3cb-172">**RemoveAccountList** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample13.cs?highlight=3)]

<span data-ttu-id="9d3cb-173">Метод **хаспассворд**</span><span class="sxs-lookup"><span data-stu-id="9d3cb-173">**HasPassword** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample14.cs?highlight=3)]

<span data-ttu-id="9d3cb-174">Теперь можно [запустить приложение](#run) и зарегистрировать нового пользователя.</span><span class="sxs-lookup"><span data-stu-id="9d3cb-174">You can now [run the application](#run) and register a new user.</span></span>

<a id="mvcupdate3"></a>
## <a name="for-mvc-with-update-3-change-the-accountcontroller-and-managecontroller-to-pass-the-key-type"></a><span data-ttu-id="9d3cb-175">Для MVC с обновлением 3 Измените AccountController и Манажеконтроллер, чтобы передать тип ключа.</span><span class="sxs-lookup"><span data-stu-id="9d3cb-175">For MVC with Update 3, change the AccountController and ManageController to pass the key type</span></span>

<span data-ttu-id="9d3cb-176">Откройте файл AccountController.cs.</span><span class="sxs-lookup"><span data-stu-id="9d3cb-176">Open the AccountController.cs file.</span></span> <span data-ttu-id="9d3cb-177">Необходимо изменить следующий метод.</span><span class="sxs-lookup"><span data-stu-id="9d3cb-177">You need to change the following method.</span></span>

<span data-ttu-id="9d3cb-178">Метод **конфирмемаил**</span><span class="sxs-lookup"><span data-stu-id="9d3cb-178">**ConfirmEmail** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample15.cs?highlight=1,3)]

<span data-ttu-id="9d3cb-179">Метод **SendCode**</span><span class="sxs-lookup"><span data-stu-id="9d3cb-179">**SendCode** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample16.cs?highlight=4)]

<span data-ttu-id="9d3cb-180">Откройте файл ManageController.cs.</span><span class="sxs-lookup"><span data-stu-id="9d3cb-180">Open the ManageController.cs file.</span></span> <span data-ttu-id="9d3cb-181">Необходимо изменить следующие методы.</span><span class="sxs-lookup"><span data-stu-id="9d3cb-181">You need to change the following methods.</span></span>

<span data-ttu-id="9d3cb-182">Метод **index**</span><span class="sxs-lookup"><span data-stu-id="9d3cb-182">**Index** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample17.cs?highlight=15-17)]

<span data-ttu-id="9d3cb-183">Методы **ремовелогин**</span><span class="sxs-lookup"><span data-stu-id="9d3cb-183">**RemoveLogin** methods</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample18.cs?highlight=3,13,17)]

<span data-ttu-id="9d3cb-184">Метод **аддфоненумбер**</span><span class="sxs-lookup"><span data-stu-id="9d3cb-184">**AddPhoneNumber** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample19.cs?highlight=9)]

<span data-ttu-id="9d3cb-185">Метод **енаблетвофактораусентикатион**</span><span class="sxs-lookup"><span data-stu-id="9d3cb-185">**EnableTwoFactorAuthentication** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample20.cs?highlight=3-4)]

<span data-ttu-id="9d3cb-186">Метод **дисаблетвофактораусентикатион**</span><span class="sxs-lookup"><span data-stu-id="9d3cb-186">**DisableTwoFactorAuthentication** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample21.cs?highlight=3-4)]

<span data-ttu-id="9d3cb-187">Методы **верифифоненумбер**</span><span class="sxs-lookup"><span data-stu-id="9d3cb-187">**VerifyPhoneNumber** methods</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample22.cs?highlight=4,18,21)]

<span data-ttu-id="9d3cb-188">Метод **ремовефоненумбер**</span><span class="sxs-lookup"><span data-stu-id="9d3cb-188">**RemovePhoneNumber** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample23.cs?highlight=3,8)]

<span data-ttu-id="9d3cb-189">Метод **ChangePassword**</span><span class="sxs-lookup"><span data-stu-id="9d3cb-189">**ChangePassword** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample24.cs?highlight=10,13)]

<span data-ttu-id="9d3cb-190">Метод **SetPassword**</span><span class="sxs-lookup"><span data-stu-id="9d3cb-190">**SetPassword** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample25.cs?highlight=5,8)]

<span data-ttu-id="9d3cb-191">Метод **манажелогинс**</span><span class="sxs-lookup"><span data-stu-id="9d3cb-191">**ManageLogins** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample26.cs?highlight=7,12)]

<span data-ttu-id="9d3cb-192">Метод **линклогинкаллбакк**</span><span class="sxs-lookup"><span data-stu-id="9d3cb-192">**LinkLoginCallback** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample27.cs?highlight=8)]

<span data-ttu-id="9d3cb-193">Метод **хаспассворд**</span><span class="sxs-lookup"><span data-stu-id="9d3cb-193">**HasPassword** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample28.cs?highlight=3)]

<span data-ttu-id="9d3cb-194">Метод **хасфоненумбер**</span><span class="sxs-lookup"><span data-stu-id="9d3cb-194">**HasPhoneNumber** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample29.cs?highlight=3)]

<span data-ttu-id="9d3cb-195">Теперь можно [запустить приложение](#run) и зарегистрировать нового пользователя.</span><span class="sxs-lookup"><span data-stu-id="9d3cb-195">You can now [run the application](#run) and register a new user.</span></span>

<a id="webformsupdate2"></a>
## <a name="for-web-forms-with-update-2-change-account-pages-to-pass-the-key-type"></a><span data-ttu-id="9d3cb-196">Для веб-форм с обновлением 2 изменение страниц учетной записи для передачи типа ключа</span><span class="sxs-lookup"><span data-stu-id="9d3cb-196">For Web Forms with Update 2, change Account pages to pass the key type</span></span>

<span data-ttu-id="9d3cb-197">Для веб-форм с обновлением 2 необходимо изменить следующие страницы.</span><span class="sxs-lookup"><span data-stu-id="9d3cb-197">For Web Forms with Update 2, you need to change the following pages.</span></span>

<span data-ttu-id="9d3cb-198">**Confirm.aspx.cx**</span><span class="sxs-lookup"><span data-stu-id="9d3cb-198">**Confirm.aspx.cx**</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample30.cs?highlight=8)]

<span data-ttu-id="9d3cb-199">**RegisterExternalLogin.aspx.cs**</span><span class="sxs-lookup"><span data-stu-id="9d3cb-199">**RegisterExternalLogin.aspx.cs**</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample31.cs?highlight=36)]

<span data-ttu-id="9d3cb-200">**Manage.aspx.cs**</span><span class="sxs-lookup"><span data-stu-id="9d3cb-200">**Manage.aspx.cs**</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample32.cs?highlight=3,22,47,52,69,85,93,98)]

<span data-ttu-id="9d3cb-201">Теперь можно [запустить приложение](#run) и зарегистрировать нового пользователя.</span><span class="sxs-lookup"><span data-stu-id="9d3cb-201">You can now [run the application](#run) and register a new user.</span></span>

<a id="webformsupdate3"></a>
## <a name="for-web-forms-with-update-3-change-account-pages-to-pass-the-key-type"></a><span data-ttu-id="9d3cb-202">Для веб-форм с обновлением 3 изменение страниц учетной записи для передачи типа ключа</span><span class="sxs-lookup"><span data-stu-id="9d3cb-202">For Web Forms with Update 3, change Account pages to pass the key type</span></span>

<span data-ttu-id="9d3cb-203">Для веб-форм с обновлением 3 необходимо изменить следующие страницы.</span><span class="sxs-lookup"><span data-stu-id="9d3cb-203">For Web Forms with Update 3, you need to change the following pages.</span></span>

<span data-ttu-id="9d3cb-204">**Confirm.aspx.cx**</span><span class="sxs-lookup"><span data-stu-id="9d3cb-204">**Confirm.aspx.cx**</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample33.cs?highlight=8)]

<span data-ttu-id="9d3cb-205">**RegisterExternalLogin.aspx.cs**</span><span class="sxs-lookup"><span data-stu-id="9d3cb-205">**RegisterExternalLogin.aspx.cs**</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample34.cs?highlight=36)]

<span data-ttu-id="9d3cb-206">**Manage.aspx.cs**</span><span class="sxs-lookup"><span data-stu-id="9d3cb-206">**Manage.aspx.cs**</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample35.cs?highlight=11,27,32,34,82,87,99,108)]

<span data-ttu-id="9d3cb-207">**VerifyPhoneNumber.aspx.cs**</span><span class="sxs-lookup"><span data-stu-id="9d3cb-207">**VerifyPhoneNumber.aspx.cs**</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample36.cs?highlight=8,23,27)]

<span data-ttu-id="9d3cb-208">**AddPhoneNumber.aspx.cs**</span><span class="sxs-lookup"><span data-stu-id="9d3cb-208">**AddPhoneNumber.aspx.cs**</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample37.cs?highlight=7)]

<span data-ttu-id="9d3cb-209">**ManagePassword.aspx.cs**</span><span class="sxs-lookup"><span data-stu-id="9d3cb-209">**ManagePassword.aspx.cs**</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample38.cs?highlight=11,47,50,68)]

<span data-ttu-id="9d3cb-210">**ManageLogins.aspx.cs**</span><span class="sxs-lookup"><span data-stu-id="9d3cb-210">**ManageLogins.aspx.cs**</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample39.cs?highlight=16,23,32,41,45)]

<span data-ttu-id="9d3cb-211">**TwoFactorAuthenticationSignIn.aspx.cs**</span><span class="sxs-lookup"><span data-stu-id="9d3cb-211">**TwoFactorAuthenticationSignIn.aspx.cs**</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample40.cs?highlight=14-15,29,53)]

<a id="run"></a>
## <a name="run-application"></a><span data-ttu-id="9d3cb-212">Запуск приложения</span><span class="sxs-lookup"><span data-stu-id="9d3cb-212">Run application</span></span>

<span data-ttu-id="9d3cb-213">Все необходимые изменения в шаблоне веб-приложения по умолчанию завершены.</span><span class="sxs-lookup"><span data-stu-id="9d3cb-213">You have finished all of the required changes to the default Web Application template.</span></span> <span data-ttu-id="9d3cb-214">Запустите приложение и зарегистрируйте нового пользователя.</span><span class="sxs-lookup"><span data-stu-id="9d3cb-214">Run the application and register a new user.</span></span> <span data-ttu-id="9d3cb-215">После регистрации пользователя вы заметите, что таблица AspNetUsers содержит столбец идентификаторов, который является целым числом.</span><span class="sxs-lookup"><span data-stu-id="9d3cb-215">After registering the user, you will notice that the AspNetUsers table has an Id column that is an integer.</span></span>

![новый первичный ключ](change-primary-key-for-users-in-aspnet-identity/_static/image1.png)

<span data-ttu-id="9d3cb-217">Если вы ранее создали ASP.NET Identity таблицы с другим первичным ключом, необходимо внести некоторые дополнительные изменения.</span><span class="sxs-lookup"><span data-stu-id="9d3cb-217">If you have previously created the ASP.NET Identity tables with a different primary key, you need to make some additional changes.</span></span> <span data-ttu-id="9d3cb-218">Если возможно, просто удалите существующую базу данных.</span><span class="sxs-lookup"><span data-stu-id="9d3cb-218">If possible, just delete the existing database.</span></span> <span data-ttu-id="9d3cb-219">База данных будет создана заново с правильной структурой при запуске веб-приложения и добавлении нового пользователя.</span><span class="sxs-lookup"><span data-stu-id="9d3cb-219">The database will be re-created with the correct design when you run the web application and add a new user.</span></span> <span data-ttu-id="9d3cb-220">Если удаление невозможно, то для изменения таблиц выполните код с первой миграцией.</span><span class="sxs-lookup"><span data-stu-id="9d3cb-220">If deletion is not possible, run code first migrations to change the tables.</span></span> <span data-ttu-id="9d3cb-221">Однако новый целочисленный первичный ключ не будет настроен как свойство IDENTITY SQL в базе данных.</span><span class="sxs-lookup"><span data-stu-id="9d3cb-221">However, the new integer primary key will not be set up as a SQL IDENTITY property in the database.</span></span> <span data-ttu-id="9d3cb-222">Необходимо вручную задать столбец идентификатора в качестве удостоверения.</span><span class="sxs-lookup"><span data-stu-id="9d3cb-222">You must manually set the Id column as an IDENTITY.</span></span>

<a id="other"></a>
## <a name="other-resources"></a><span data-ttu-id="9d3cb-223">Другие ресурсы</span><span class="sxs-lookup"><span data-stu-id="9d3cb-223">Other resources</span></span>

- [<span data-ttu-id="9d3cb-224">Обзор пользовательских поставщиков хранилищ для ASP.NET Identity</span><span class="sxs-lookup"><span data-stu-id="9d3cb-224">Overview of Custom Storage Providers for ASP.NET Identity</span></span>](overview-of-custom-storage-providers-for-aspnet-identity.md)
- [<span data-ttu-id="9d3cb-225">Миграция существующего веб-сайта из членства SQL в ASP.NET Identity</span><span class="sxs-lookup"><span data-stu-id="9d3cb-225">Migrating an Existing Website from SQL Membership to ASP.NET Identity</span></span>](../migrations/migrating-an-existing-website-from-sql-membership-to-aspnet-identity.md)
- [<span data-ttu-id="9d3cb-226">Перенос данных универсального поставщика для членства и профилей пользователей в ASP.NET Identity</span><span class="sxs-lookup"><span data-stu-id="9d3cb-226">Migrating Universal Provider Data for Membership and User Profiles to ASP.NET Identity</span></span>](../migrations/migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity.md)
- <span data-ttu-id="9d3cb-227">[Пример приложения](https://github.com/aspnet/samples/tree/master/samples/aspnet/Identity/ChangePK) с измененным первичным ключом</span><span class="sxs-lookup"><span data-stu-id="9d3cb-227">[Sample application](https://github.com/aspnet/samples/tree/master/samples/aspnet/Identity/ChangePK) with changed primary key</span></span>
