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
# <a name="change-primary-key-for-users-in-aspnet-identity"></a>Изменение первичного ключа для пользователей в ASP.NET Identity

от [Tom фитзмаккен](https://github.com/tfitzmac)

> В Visual Studio 2013 веб-приложение по умолчанию использует строковое значение для ключа учетных записей пользователей. ASP.NET Identity позволяет изменить тип ключа в соответствии с требованиями к данным. Например, можно изменить тип ключа с строки на целое число.
> 
> В этом разделе показано, как начать работу с веб-приложением по умолчанию и изменить ключ учетной записи пользователя на целое число. Вы можете использовать те же изменения для реализации любого типа ключа в проекте. В нем показано, как внести эти изменения в веб-приложение по умолчанию, но можно применить аналогичные изменения к настроенному приложению. В нем отображаются изменения, необходимые при работе с MVC или веб-формами.
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>Версии программного обеспечения, используемые в этом руководстве
> 
> 
> - Visual Studio 2013 с обновлением 2 (или более поздней версии)
> - ASP.NET Identity 2,1 или более поздней версии

Для выполнения действий, описанных в этом руководстве, необходимо иметь Visual Studio 2013 обновление 2 (или более поздней версии) и веб-приложение, созданное из шаблона веб-приложения ASP.NET. Шаблон изменен в обновлении 3. В этом разделе показано, как изменить шаблон в обновлении 2 и обновлении 3.

Этот раздел состоит из следующих подразделов.

- [Изменение типа ключа в классе удостоверений пользователя](#userclass)
- [Добавление настраиваемых классов удостоверений, использующих тип ключа](#customclass)
- [Изменение класса контекста и диспетчера пользователей для использования типа ключа](#context)
- [Изменение конфигурации запуска для использования типа ключа](#startup)
- [Для MVC с обновлением 2 Измените AccountController, чтобы передать тип ключа.](#mvcupdate2)
- [Для MVC с обновлением 3 Измените AccountController и Манажеконтроллер, чтобы передать тип ключа.](#mvcupdate3)
- [Для веб-форм с обновлением 2 изменение страниц учетной записи для передачи типа ключа](#webformsupdate2)
- [Для веб-форм с обновлением 3 изменение страниц учетной записи для передачи типа ключа](#webformsupdate3)
- [Запустить приложение](#run)
- [Другие ресурсы](#other)

<a id="userclass"></a>
## <a name="change-the-type-of-the-key-in-the-identity-user-class"></a>Изменение типа ключа в классе удостоверений пользователя

В проекте, созданном из шаблона веб-приложения ASP.NET, укажите, что класс Аппликатионусер использует целое число для ключа учетных записей пользователей. В IdentityModels.cs измените класс Аппликатионусер, чтобы он наследовался от Идентитюсер, имеющего тип **int** для универсального параметра TKey. Вы также передаете имена трех настраиваемых классов, которые еще не реализованы.

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample1.cs?highlight=1-2)]

Вы изменили тип ключа, но по умолчанию остальная часть приложения по-прежнему предполагает, что ключ является строкой. Необходимо явно указать тип ключа в коде, который предполагает наличие строки.

В классе **аппликатионусер** измените метод **женератеусеридентитясинк** , чтобы включить int, как показано в выделенном ниже коде. Это изменение не требуется для проектов веб-форм с шаблоном обновления 3.

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample2.cs?highlight=2)]

<a id="customclass"></a>
## <a name="add-customized-identity-classes-that-use-the-key-type"></a>Добавление настраиваемых классов удостоверений, использующих тип ключа

Другие классы удостоверений, такие как Идентитюсерроле, Идентитюсерклаим, Идентитюсерлогин, Идентитироле, UserStore, Ролесторе, по-прежнему настраиваются на использование строкового ключа. Создайте новые версии этих классов, которые указывают целочисленное значение для ключа. Вам не нужно предоставлять много кода реализации в этих классах, поэтому в основном просто устанавливается int в качестве ключа.

Добавьте следующие классы в файл IdentityModels.cs.

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample3.cs)]

<a id="context"></a>
## <a name="change-the-context-class-and-user-manager-to-use-the-key-type"></a>Изменение класса контекста и диспетчера пользователей для использования типа ключа

В IdentityModels.cs измените определение класса **ApplicationDbContext** , чтобы использовать новые настраиваемые классы и **int** для ключа, как показано в выделенном коде.

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample4.cs?highlight=1-2)]

Параметр ThrowIfV1Schema больше не является допустимым в конструкторе. Измените конструктор, чтобы он не передавал значение ThrowIfV1Schema.

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample5.cs)]

Откройте IdentityConfig.cs и измените класс **аппликатионусерманжер** , чтобы использовать новый класс пользовательского хранилища для сохранения данных **и целое число для ключа** .

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample6.cs?highlight=1,3,12,14,32,37,48)]

В шаблоне обновления 3 необходимо изменить класс Аппликатионсигнинманажер.

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample7.cs?highlight=1)]

<a id="startup"></a>
## <a name="change-start-up-configuration-to-use-the-key-type"></a>Изменение конфигурации запуска для использования типа ключа

В Startup.Auth.cs замените код Онвалидатеидентити, как показано ниже. Обратите внимание, что определение Жетусеридкаллбакк анализирует строковое значение в целое число.

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample8.cs?highlight=7-12)]

Если проект не распознает универсальную реализацию метода **UserID** , может потребоваться обновить пакет NuGet ASP.NET Identity до версии 2,1.

Вы внесли много изменений в классы инфраструктуры, используемые ASP.NET Identity. Если вы попытаетесь скомпилировать проект, вы увидите множество ошибок. К счастью, все остальные ошибки похожи. Класс Identity ожидает для ключа целое число, но контроллер (или веб-форма) передает строковое значение. В каждом случае необходимо преобразовать строку в тип и целое число, вызвав метод GetString **&lt;int&gt;** . Вы можете работать со списком ошибок из компиляции или следовать приведенным ниже изменениям.

Остальные изменения зависят от типа создаваемого проекта и обновления, установленного в Visual Studio. Вы можете перейти непосредственно к соответствующему разделу, перейдя по следующим ссылкам.

- [Для MVC с обновлением 2 Измените AccountController, чтобы передать тип ключа.](#mvcupdate2)
- [Для MVC с обновлением 3 Измените AccountController и Манажеконтроллер, чтобы передать тип ключа.](#mvcupdate3)
- [Для веб-форм с обновлением 2 изменение страниц учетной записи для передачи типа ключа](#webformsupdate2)
- [Для веб-форм с обновлением 3 изменение страниц учетной записи для передачи типа ключа](#webformsupdate3)

<a id="mvcupdate2"></a>
## <a name="for-mvc-with-update-2-change-the-accountcontroller-to-pass-the-key-type"></a>Для MVC с обновлением 2 Измените AccountController, чтобы передать тип ключа.

Откройте файл AccountController.cs. Необходимо изменить следующие методы.

Метод **конфирмемаил**

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample9.cs?highlight=1,3)]

Метод **отсвязи**

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample10.cs?highlight=5,9)]

Метод **управления (манажеусервиевмодел)**

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample11.cs?highlight=11,17,41)]

Метод **линклогинкаллбакк**

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample12.cs?highlight=10)]

Метод **ремовеаккаунтлист**

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample13.cs?highlight=3)]

Метод **хаспассворд**

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample14.cs?highlight=3)]

Теперь можно [запустить приложение](#run) и зарегистрировать нового пользователя.

<a id="mvcupdate3"></a>
## <a name="for-mvc-with-update-3-change-the-accountcontroller-and-managecontroller-to-pass-the-key-type"></a>Для MVC с обновлением 3 Измените AccountController и Манажеконтроллер, чтобы передать тип ключа.

Откройте файл AccountController.cs. Необходимо изменить следующий метод.

Метод **конфирмемаил**

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample15.cs?highlight=1,3)]

Метод **SendCode**

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample16.cs?highlight=4)]

Откройте файл ManageController.cs. Необходимо изменить следующие методы.

Метод **index**

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample17.cs?highlight=15-17)]

Методы **ремовелогин**

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample18.cs?highlight=3,13,17)]

Метод **аддфоненумбер**

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample19.cs?highlight=9)]

Метод **енаблетвофактораусентикатион**

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample20.cs?highlight=3-4)]

Метод **дисаблетвофактораусентикатион**

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample21.cs?highlight=3-4)]

Методы **верифифоненумбер**

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample22.cs?highlight=4,18,21)]

Метод **ремовефоненумбер**

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample23.cs?highlight=3,8)]

Метод **ChangePassword**

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample24.cs?highlight=10,13)]

Метод **SetPassword**

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample25.cs?highlight=5,8)]

Метод **манажелогинс**

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample26.cs?highlight=7,12)]

Метод **линклогинкаллбакк**

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample27.cs?highlight=8)]

Метод **хаспассворд**

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample28.cs?highlight=3)]

Метод **хасфоненумбер**

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample29.cs?highlight=3)]

Теперь можно [запустить приложение](#run) и зарегистрировать нового пользователя.

<a id="webformsupdate2"></a>
## <a name="for-web-forms-with-update-2-change-account-pages-to-pass-the-key-type"></a>Для веб-форм с обновлением 2 изменение страниц учетной записи для передачи типа ключа

Для веб-форм с обновлением 2 необходимо изменить следующие страницы.

**Confirm.aspx.cx**

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample30.cs?highlight=8)]

**RegisterExternalLogin.aspx.cs**

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample31.cs?highlight=36)]

**Manage.aspx.cs**

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample32.cs?highlight=3,22,47,52,69,85,93,98)]

Теперь можно [запустить приложение](#run) и зарегистрировать нового пользователя.

<a id="webformsupdate3"></a>
## <a name="for-web-forms-with-update-3-change-account-pages-to-pass-the-key-type"></a>Для веб-форм с обновлением 3 изменение страниц учетной записи для передачи типа ключа

Для веб-форм с обновлением 3 необходимо изменить следующие страницы.

**Confirm.aspx.cx**

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample33.cs?highlight=8)]

**RegisterExternalLogin.aspx.cs**

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample34.cs?highlight=36)]

**Manage.aspx.cs**

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample35.cs?highlight=11,27,32,34,82,87,99,108)]

**VerifyPhoneNumber.aspx.cs**

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample36.cs?highlight=8,23,27)]

**AddPhoneNumber.aspx.cs**

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample37.cs?highlight=7)]

**ManagePassword.aspx.cs**

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample38.cs?highlight=11,47,50,68)]

**ManageLogins.aspx.cs**

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample39.cs?highlight=16,23,32,41,45)]

**TwoFactorAuthenticationSignIn.aspx.cs**

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample40.cs?highlight=14-15,29,53)]

<a id="run"></a>
## <a name="run-application"></a>Запуск приложения

Все необходимые изменения в шаблоне веб-приложения по умолчанию завершены. Запустите приложение и зарегистрируйте нового пользователя. После регистрации пользователя вы заметите, что таблица AspNetUsers содержит столбец идентификаторов, который является целым числом.

![новый первичный ключ](change-primary-key-for-users-in-aspnet-identity/_static/image1.png)

Если вы ранее создали ASP.NET Identity таблицы с другим первичным ключом, необходимо внести некоторые дополнительные изменения. Если возможно, просто удалите существующую базу данных. База данных будет создана заново с правильной структурой при запуске веб-приложения и добавлении нового пользователя. Если удаление невозможно, то для изменения таблиц выполните код с первой миграцией. Однако новый целочисленный первичный ключ не будет настроен как свойство IDENTITY SQL в базе данных. Необходимо вручную задать столбец идентификатора в качестве удостоверения.

<a id="other"></a>
## <a name="other-resources"></a>Другие ресурсы

- [Обзор пользовательских поставщиков хранилищ для ASP.NET Identity](overview-of-custom-storage-providers-for-aspnet-identity.md)
- [Миграция существующего веб-сайта из членства SQL в ASP.NET Identity](../migrations/migrating-an-existing-website-from-sql-membership-to-aspnet-identity.md)
- [Перенос данных универсального поставщика для членства и профилей пользователей в ASP.NET Identity](../migrations/migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity.md)
- [Пример приложения](https://github.com/aspnet/samples/tree/master/samples/aspnet/Identity/ChangePK) с измененным первичным ключом
