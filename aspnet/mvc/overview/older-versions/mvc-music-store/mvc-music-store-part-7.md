---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-7
title: Часть 7. членство и авторизация | Документация Майкрософт
author: jongalloway
description: В этой серии руководств подробно описаны все шаги, предпринятые для создания примера приложения музыкального хранилища ASP.NET MVC. В части 7 рассматривается членство и авторизация.
ms.author: riande
ms.date: 10/13/2010
ms.assetid: c8511ebe-68bc-4240-87c3-d5ced84a3f37
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-7
msc.type: authoredcontent
ms.openlocfilehash: a6a1a936e0ea29ea36721ba78f35845401f74c01
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78433470"
---
# <a name="part-7-membership-and-authorization"></a><span data-ttu-id="6157f-104">Часть 7. членство и авторизация</span><span class="sxs-lookup"><span data-stu-id="6157f-104">Part 7: Membership and Authorization</span></span>

<span data-ttu-id="6157f-105">[Джон Гэллоуэй](https://github.com/jongalloway)</span><span class="sxs-lookup"><span data-stu-id="6157f-105">by [Jon Galloway](https://github.com/jongalloway)</span></span>

> <span data-ttu-id="6157f-106">Музыкальное хранилище MVC — это учебное приложение, в котором представлены и объясняются пошаговые инструкции по использованию ASP.NET MVC и Visual Studio для разработки веб-приложений.</span><span class="sxs-lookup"><span data-stu-id="6157f-106">The MVC Music Store is a tutorial application that introduces and explains step-by-step how to use ASP.NET MVC and Visual Studio for web development.</span></span>  
>   
> <span data-ttu-id="6157f-107">Музыкальное хранилище MVC — это упрощенная реализация в магазине, которая продает музыкальные альбомы в сети и реализует базовое администрирование сайта, вход пользователя в систему и функции корзины покупок.</span><span class="sxs-lookup"><span data-stu-id="6157f-107">The MVC Music Store is a lightweight sample store implementation which sells music albums online, and implements basic site administration, user sign-in, and shopping cart functionality.</span></span>  
>   
> <span data-ttu-id="6157f-108">В этой серии руководств подробно описаны все шаги, предпринятые для создания примера приложения музыкального хранилища ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="6157f-108">This tutorial series details all of the steps taken to build the ASP.NET MVC Music Store sample application.</span></span> <span data-ttu-id="6157f-109">В части 7 рассматривается членство и авторизация.</span><span class="sxs-lookup"><span data-stu-id="6157f-109">Part 7 covers Membership and Authorization.</span></span>

<span data-ttu-id="6157f-110">Наш контроллер Store Manager в настоящее время доступен всем, кто посещает наш сайт.</span><span class="sxs-lookup"><span data-stu-id="6157f-110">Our Store Manager controller is currently accessible to anyone visiting our site.</span></span> <span data-ttu-id="6157f-111">Изменим это значение, чтобы ограничить разрешения администраторам сайта.</span><span class="sxs-lookup"><span data-stu-id="6157f-111">Let's change this to restrict permission to site administrators.</span></span>

## <a name="adding-the-accountcontroller-and-views"></a><span data-ttu-id="6157f-112">Добавление AccountController и представлений</span><span class="sxs-lookup"><span data-stu-id="6157f-112">Adding the AccountController and Views</span></span>

<span data-ttu-id="6157f-113">Единственное различие между шаблоном веб-приложения Full ASP.NET MVC 3 и шаблоном веб-приложения ASP.NET MVC 3 заключается в том, что пустой шаблон не включает контроллер учетной записи.</span><span class="sxs-lookup"><span data-stu-id="6157f-113">One difference between the full ASP.NET MVC 3 Web Application template and the ASP.NET MVC 3 Empty Web Application template is that the empty template doesn't include an Account Controller.</span></span> <span data-ttu-id="6157f-114">Мы добавим контроллер учетной записи, скопировав несколько файлов из нового приложения MVC ASP.NET, созданного из шаблона веб-приложения ASP.NET MVC 3.</span><span class="sxs-lookup"><span data-stu-id="6157f-114">We'll add an Account Controller by copying a few files from a new ASP.NET MVC application created from the full ASP.NET MVC 3 Web Application template.</span></span>

<span data-ttu-id="6157f-115">Создайте новое приложение ASP.NET MVC с помощью шаблона веб-приложения Full ASP.NET MVC 3 и скопируйте следующие файлы в те же каталоги в нашем проекте:</span><span class="sxs-lookup"><span data-stu-id="6157f-115">Create a new ASP.NET MVC application using the full ASP.NET MVC 3 Web Application template and copy the following files into the same directories in our project:</span></span>

1. <span data-ttu-id="6157f-116">Копирование AccountController.cs в каталоге Controllers</span><span class="sxs-lookup"><span data-stu-id="6157f-116">Copy AccountController.cs in the Controllers directory</span></span>
2. <span data-ttu-id="6157f-117">Копирование Аккаунтмоделс в каталоге Models</span><span class="sxs-lookup"><span data-stu-id="6157f-117">Copy AccountModels in the Models directory</span></span>
3. <span data-ttu-id="6157f-118">Создайте каталог учетных записей внутри каталога views и скопируйте все четыре представления в</span><span class="sxs-lookup"><span data-stu-id="6157f-118">Create an Account directory inside the Views directory and copy all four views in</span></span>

<span data-ttu-id="6157f-119">Измените пространство имен для классов контроллера и модели, чтобы они начинались с Мвкмусиксторе.</span><span class="sxs-lookup"><span data-stu-id="6157f-119">Change the namespace for the Controller and Model classes so they begin with MvcMusicStore.</span></span> <span data-ttu-id="6157f-120">Класс AccountController должен использовать пространство имен Мвкмусиксторе. Controllers, а класс Аккаунтмоделс должен использовать пространство имен Мвкмусиксторе. Models.</span><span class="sxs-lookup"><span data-stu-id="6157f-120">The AccountController class should use the MvcMusicStore.Controllers namespace, and the AccountModels class should use the MvcMusicStore.Models namespace.</span></span>

<span data-ttu-id="6157f-121">*Примечание. Эти файлы также доступны в загружаемом файле Мвкмусиксторе-Ассетс. zip, из которого мы скопировали файлы проекта сайта в начале этого руководства. Файлы членства находятся в каталоге Code.*</span><span class="sxs-lookup"><span data-stu-id="6157f-121">*Note: These files are also available in the MvcMusicStore-Assets.zip download from which we copied our site design files at the beginning of the tutorial. The Membership files are located in the Code directory.*</span></span>

<span data-ttu-id="6157f-122">Обновленное решение должно выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="6157f-122">The updated solution should look like the following:</span></span>

![](mvc-music-store-part-7/_static/image1.png)

## <a name="adding-an-administrative-user-with-the-aspnet-configuration-site"></a><span data-ttu-id="6157f-123">Добавление пользователя с правами администратора с сайтом конфигурации ASP.NET</span><span class="sxs-lookup"><span data-stu-id="6157f-123">Adding an Administrative User with the ASP.NET Configuration site</span></span>

<span data-ttu-id="6157f-124">Прежде чем требовать авторизацию на нашем веб-сайте, необходимо создать пользователя с доступом.</span><span class="sxs-lookup"><span data-stu-id="6157f-124">Before we require Authorization in our website, we'll need to create a user with access.</span></span> <span data-ttu-id="6157f-125">Самый простой способ создать пользователя — использовать встроенный веб-сайт конфигурации ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="6157f-125">The easiest way to create a user is to use the built-in ASP.NET Configuration website.</span></span>

<span data-ttu-id="6157f-126">Запустите веб-сайт конфигурации ASP.NET, щелкнув значок в обозреватель решений.</span><span class="sxs-lookup"><span data-stu-id="6157f-126">Launch the ASP.NET Configuration website by clicking following the icon in the Solution Explorer.</span></span>

![](mvc-music-store-part-7/_static/image2.png)

<span data-ttu-id="6157f-127">Запустится веб-сайт конфигурации.</span><span class="sxs-lookup"><span data-stu-id="6157f-127">This launches a configuration website.</span></span> <span data-ttu-id="6157f-128">Щелкните вкладку Безопасность на начальном экране, а затем щелкните ссылку "включить роли" в центре экрана.</span><span class="sxs-lookup"><span data-stu-id="6157f-128">Click on the Security tab on the home screen, then click the "Enable roles" link in the center of the screen.</span></span>

![](mvc-music-store-part-7/_static/image3.png)

<span data-ttu-id="6157f-129">Щелкните ссылку "создать роли" или "Управление ролями".</span><span class="sxs-lookup"><span data-stu-id="6157f-129">Click the "Create or Manage roles" link.</span></span>

![](mvc-music-store-part-7/_static/image4.png)

<span data-ttu-id="6157f-130">В качестве имени роли введите "Administrator" и нажмите кнопку Добавить роль.</span><span class="sxs-lookup"><span data-stu-id="6157f-130">Enter "Administrator" as the role name and press the Add Role button.</span></span>

![](mvc-music-store-part-7/_static/image5.png)

<span data-ttu-id="6157f-131">Нажмите кнопку "назад", а затем щелкните ссылку Создать пользователя в левой части.</span><span class="sxs-lookup"><span data-stu-id="6157f-131">Click the Back button, then click on the Create user link on the left side.</span></span>

![](mvc-music-store-part-7/_static/image6.png)

<span data-ttu-id="6157f-132">Заполните поля сведений о пользователе слева, используя следующие сведения:</span><span class="sxs-lookup"><span data-stu-id="6157f-132">Fill in the user information fields on the left using the following information:</span></span>

| <span data-ttu-id="6157f-133">**Поле**</span><span class="sxs-lookup"><span data-stu-id="6157f-133">**Field**</span></span> | <span data-ttu-id="6157f-134">**Value**</span><span class="sxs-lookup"><span data-stu-id="6157f-134">**Value**</span></span> |
| --- | --- |
| <span data-ttu-id="6157f-135">**Имя пользователя**</span><span class="sxs-lookup"><span data-stu-id="6157f-135">**User Name**</span></span> | <span data-ttu-id="6157f-136">Администратор</span><span class="sxs-lookup"><span data-stu-id="6157f-136">Administrator</span></span> |
| <span data-ttu-id="6157f-137">**Пароль**</span><span class="sxs-lookup"><span data-stu-id="6157f-137">**Password**</span></span> | <span data-ttu-id="6157f-138">password123!</span><span class="sxs-lookup"><span data-stu-id="6157f-138">password123!</span></span> |
| <span data-ttu-id="6157f-139">**Подтвердите пароль**</span><span class="sxs-lookup"><span data-stu-id="6157f-139">**Confirm Password**</span></span> | <span data-ttu-id="6157f-140">password123!</span><span class="sxs-lookup"><span data-stu-id="6157f-140">password123!</span></span> |
| <span data-ttu-id="6157f-141">**Электронная почта**</span><span class="sxs-lookup"><span data-stu-id="6157f-141">**E-mail**</span></span> | <span data-ttu-id="6157f-142">(любой адрес электронной почты будет работать)</span><span class="sxs-lookup"><span data-stu-id="6157f-142">(any email address will work)</span></span> |
| <span data-ttu-id="6157f-143">**Контрольный вопрос**</span><span class="sxs-lookup"><span data-stu-id="6157f-143">**Security Question**</span></span> | <span data-ttu-id="6157f-144">(что вам нравится)</span><span class="sxs-lookup"><span data-stu-id="6157f-144">(whatever you like)</span></span> |
| <span data-ttu-id="6157f-145">**Ответ на контрольный вопрос**</span><span class="sxs-lookup"><span data-stu-id="6157f-145">**Security Answer**</span></span> | <span data-ttu-id="6157f-146">(что вам нравится)</span><span class="sxs-lookup"><span data-stu-id="6157f-146">(whatever you like)</span></span> |

<span data-ttu-id="6157f-147">*Примечание. Вы можете использовать любой пароль, который вы хотите. Параметры безопасности пароля по умолчанию должны иметь пароль длиной 7 символов и содержать один символ, отличный от буквенно-цифрового.*</span><span class="sxs-lookup"><span data-stu-id="6157f-147">*Note: You can of course use any password you'd like. The default password security settings require a password that is 7 characters long and contains one non-alphanumeric character.*</span></span>

<span data-ttu-id="6157f-148">Выберите роль администратора для этого пользователя и нажмите кнопку Создать пользователя.</span><span class="sxs-lookup"><span data-stu-id="6157f-148">Select the Administrator role for this user, and click the Create User button.</span></span>

![](mvc-music-store-part-7/_static/image7.png)

<span data-ttu-id="6157f-149">На этом этапе должно отобразиться сообщение о том, что пользователь успешно создан.</span><span class="sxs-lookup"><span data-stu-id="6157f-149">At this point, you should see a message indicating that the user was created successfully.</span></span>

![](mvc-music-store-part-7/_static/image8.png)

<span data-ttu-id="6157f-150">Теперь окно браузера можно закрыть.</span><span class="sxs-lookup"><span data-stu-id="6157f-150">You can now close the browser window.</span></span>

## <a name="role-based-authorization"></a><span data-ttu-id="6157f-151">Авторизация на основе ролей</span><span class="sxs-lookup"><span data-stu-id="6157f-151">Role-based Authorization</span></span>

<span data-ttu-id="6157f-152">Теперь можно ограничить доступ к Стореманажерконтроллер с помощью атрибута [авторизовать], указав, что пользователь должен быть в роли администратора для доступа к любому действию контроллера в классе.</span><span class="sxs-lookup"><span data-stu-id="6157f-152">Now we can restrict access to the StoreManagerController using the [Authorize] attribute, specifying that the user must be in the Administrator role to access any controller action in the class.</span></span>

[!code-csharp[Main](mvc-music-store-part-7/samples/sample1.cs)]

<span data-ttu-id="6157f-153">*Примечание. атрибут [авторизовать] может быть размещен в конкретных методах действия, а также на уровне класса контроллера.*</span><span class="sxs-lookup"><span data-stu-id="6157f-153">*Note: The [Authorize] attribute can be placed on specific action methods as well as at the Controller class level.*</span></span>

<span data-ttu-id="6157f-154">Теперь при просмотре/Стореманажер открывается диалоговое окно входа в систему:</span><span class="sxs-lookup"><span data-stu-id="6157f-154">Now browsing to /StoreManager brings up a Log On dialog:</span></span>

![](mvc-music-store-part-7/_static/image9.png)

<span data-ttu-id="6157f-155">После входа в систему с помощью нашей новой учетной записи администратора мы можем переходить к экрану редактирования альбома, как и раньше.</span><span class="sxs-lookup"><span data-stu-id="6157f-155">After logging on with our new Administrator account, we're able to go to the Album Edit screen as before.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="6157f-156">[Назад](mvc-music-store-part-6.md)
> [Вперед](mvc-music-store-part-8.md)</span><span class="sxs-lookup"><span data-stu-id="6157f-156">[Previous](mvc-music-store-part-6.md)
[Next](mvc-music-store-part-8.md)</span></span>
