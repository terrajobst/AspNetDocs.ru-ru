---
uid: identity/overview/getting-started/aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider
title: ASP.NET Identity. Использование хранилища MySQL с поставщиком EntityFramework MySQL (C#)-ASP.NET 4. x
author: maumar
description: В этом руководстве показано, как заменить механизм хранения данных по умолчанию для ASP.NET Identity с EntityFramework (поставщиком клиента SQL) с помощью провид MySQL...
ms.author: riande
ms.date: 12/10/2013
ms.assetid: 15253312-a92c-43ba-908e-b5dacd3d08b8
ms.custom: seoapril2019
msc.legacyurl: /identity/overview/getting-started/aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider
msc.type: authoredcontent
ms.openlocfilehash: e89ed139657c5ce9ddcc56879946c62038919483
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78471876"
---
# <a name="aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider-c"></a>ASP.NET Identity. Использование хранилища MySQL с поставщиком EntityFramework MySQL (C#)

[Маурици Марковски](https://github.com/maumar), [Ракуел Соарес de Алмеида](https://github.com/raquelsa), [Роберт мкмуррай](https://github.com/rmcmurray)

> В этом руководстве показано, как заменить механизм хранения данных по умолчанию для [**ASP.NET Identity**](introduction-to-aspnet-identity.md) с помощью EntityFramework (поставщик клиента SQL) с поставщиком MySQL.

В этом учебнике будут рассмотрены следующие темы:

- Создание базы данных MySQL в Azure
- Создание приложения MVC с помощью шаблона Visual Studio 2013 MVC
- Настройка EntityFramework для работы с поставщиком базы данных MySQL
- Запуск приложения для проверки результатов

По завершении работы с этим руководством у вас будет приложение MVC с хранилищем ASP.NET Identity, которое использует базу данных MySQL, размещенную в Azure.

## <a name="creating-a-mysql-database-instance-on-azure"></a>Создание экземпляра базы данных MySQL в Azure

1. Войдите на [портал Azure](https://go.microsoft.com/fwlink/?linkid=529715&amp;clcid=0x409).
2. В нижней части страницы щелкните **создать** , а затем выберите **магазин**:

    [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image2.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image1.png)
3. В мастере **выбора и надстройки** выберите **ClearDB MySQL Database**, а затем щелкните стрелку " **Далее** " в нижней части рамки:

   [Щелкните следующее изображение, чтобы развернуть его. ] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image4.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image3.png)
4. Сохраните план " **бесплатный** " по умолчанию, измените **имя** на **идентитимисклдатабасе**, выберите ближайший к вам регион, а затем щелкните стрелку " **Далее** " в нижней части рамки:

   [Щелкните следующее изображение, чтобы развернуть его. ] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image6.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image5.png)
5. Щелкните флажок **приобрести** , чтобы завершить создание базы данных.

   [Щелкните следующее изображение, чтобы развернуть его. ] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image8.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image7.png)
6. После создания базой данных можно управлять на вкладке **НАДСТРОЙКИ** портала управления. Чтобы получить сведения о подключении для базы данных, щелкните **сведения о подключении** в нижней части страницы:

   [Щелкните следующее изображение, чтобы развернуть его. ] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image10.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image9.png)
7. Скопируйте строку подключения, нажав кнопку копирования в поле **CONNECTIONSTRING** и сохранив ее. Эти сведения будут использоваться далее в этом руководстве для приложения MVC.

   [Щелкните следующее изображение, чтобы развернуть его. ] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image12.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image11.png)

## <a name="creating-an-mvc-application-project"></a>Создание проекта приложения MVC

Чтобы выполнить действия, описанные в этом разделе руководства, сначала необходимо установить [Visual Studio Express 2013 для Web](https://go.microsoft.com/fwlink/?LinkId=299058) или [Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566). После установки Visual Studio выполните следующие действия, чтобы создать проект приложения MVC.

1. Откройте Visual Studio 2103.
2. На **начальной** странице нажмите кнопку **создать проект** или выберите в меню **файл** пункт **создать проект**:

   [Щелкните следующее изображение, чтобы развернуть его. ] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image2.jpg)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image1.jpg)
3. Когда откроется диалоговое окно **Создание проекта** , разверните элемент  **C# визуальный** объект в списке шаблонов, затем щелкните **веб**и выберите **ASP.NET веб-приложение**. Присвойте проекту имя **идентитимисклдемо** и нажмите кнопку **ОК**:

   [Щелкните следующее изображение, чтобы развернуть его. ] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image14.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image13.png)
4. В диалоговом окне **Новый проект ASP.NET** выберите **MVC** темплатевис параметры по умолчанию. в этом случае **отдельные учетные записи пользователей** будут настроены как метод проверки подлинности. Нажмите кнопку **ОК**.

   [Щелкните следующее изображение, чтобы развернуть его. ] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image16.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image15.png)

## <a name="configure-entityframework-to-work-with-a-mysql-database"></a>Настройка EntityFramework для работы с базой данных MySQL

### <a name="update-the-entity-framework-assembly-for-your-project"></a>Обновление сборки Entity Framework для проекта

Приложение MVC, созданное на основе шаблона Visual Studio 2013, содержит ссылку на пакет [6.0.0 EntityFramework](http://www.nuget.org/packages/EntityFramework) , но обновления этой сборки были обновлены с момента выпуска, который содержит значительные улучшения производительности. Чтобы использовать последние обновления в приложении, выполните следующие действия.

1. Откройте проект MVC в Visual Studio.
2. В меню **Сервис**выберите пункт **Диспетчер пакетов NuGet**, а затем щелкните **консоль диспетчера пакетов**.

   [Щелкните следующее изображение, чтобы развернуть его. ] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image18.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image17.png)
3. В нижней части Visual Studio появится **консоль диспетчера пакетов** . Введите &quot;**Update — Package EntityFramework**&quot; и нажмите клавишу ВВОД:

   [Щелкните следующее изображение, чтобы развернуть его. ] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image20.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image19.png)

### <a name="install-the-mysql-provider-for-entityframework"></a>Установка поставщика MySQL для EntityFramework

Чтобы EntityFramework подключаться к базе данных MySQL, необходимо установить поставщик MySQL. Для этого откройте **консоль диспетчера пакетов** и введите &quot;**Install-Package MySQL. Data. Entity-** &quot;и нажмите клавишу ВВОД.

> [!NOTE]
> Это предварительная версия сборки, которая может содержать ошибки. Не следует использовать предварительную версию поставщика в рабочей среде.

[Щелкните следующее изображение, чтобы развернуть его.]

[![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image22.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image21.png)

### <a name="making-project-configuration-changes-to-the-webconfig-file-for-your-application"></a>Внесение изменений в конфигурацию проекта в файл Web. config для приложения

В этом разделе вы настроите Entity Framework, чтобы использовать только что установленный поставщик MySQL, Зарегистрируйте фабрику поставщика MySQL и добавьте строку подключения из Azure.

> [!NOTE]
> В следующих примерах содержится конкретная версия сборки для MySql. Data. dll. Если версия сборки изменяется, необходимо изменить соответствующие параметры конфигурации, указав правильную версию.

1. Откройте файл Web. config для проекта в Visual Studio 2013.
2. Определите следующие параметры конфигурации, определяющие поставщика и фабрику базы данных по умолчанию для Entity Framework:

    [!code-xml[Main](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/samples/sample1.xml)]
3. Замените эти параметры конфигурации следующим, который настраивает Entity Framework для использования поставщика MySQL:

    [!code-xml[Main](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/samples/sample2.xml)]
4. Найдите раздел &lt;connectionStrings&gt; и замените его следующим кодом, который определит строку подключения для базы данных MySQL, размещенной в Azure (Обратите внимание, что значение providerName также изменилось с исходного):

    [!code-xml[Main](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/samples/sample3.xml?highlight=3-4)]

### <a name="adding-custom-migrationhistory-context"></a>Добавление пользовательского контекста Мигратионхистори

Entity Framework Code First использует таблицу **мигратионхистори** , чтобы следить за изменениями модели и обеспечить согласованность между схемой базы данных и концептуальной схемой. Однако по умолчанию эта таблица не работает для MySQL, так как первичный ключ слишком большой. Чтобы устранить эту ситуацию, необходимо уменьшить размер ключа для этой таблицы. Для этого выполните следующие действия.

1. Сведения о схеме для этой таблицы захватываются в **хисториконтекст**, который может быть изменен как любой другой **DbContext**. Для этого добавьте в проект новый файл класса с именем **MySqlHistoryContext.CS** и замените его содержимое следующим кодом:

    [!code-csharp[Main](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/samples/sample4.cs)]
2. Затем необходимо настроить Entity Framework для использования измененного **хисториконтекст**, а не по умолчанию. Это можно сделать, используя функции настройки на основе кода. Для этого добавьте в проект новый файл класса с именем **MySqlConfiguration.CS** и замените его содержимое на:

    [!code-csharp[Main](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/samples/sample5.cs)]

### <a name="creating-a-custom-entityframework-initializer-for-applicationdbcontext"></a>Создание пользовательского инициализатора EntityFramework для ApplicationDbContext

Поставщик MySQL, представленный в этом руководстве, в настоящее время не поддерживает Entity Framework миграций, поэтому для подключения к базе данных необходимо использовать инициализаторы модели. Поскольку в этом руководстве используется экземпляр MySQL в Azure, необходимо создать пользовательский инициализатор Entity Framework.

> [!NOTE]
> Этот шаг не требуется при подключении к SQL Server экземпляру в Azure или при использовании базы данных, размещенной в локальной среде.

Чтобы создать пользовательский инициализатор Entity Framework для MySQL, выполните следующие действия.

1. Добавьте в проект новый файл класса с именем **MySqlInitializer.CS** и замените его содержимое следующим кодом:

    [!code-csharp[Main](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/samples/sample6.cs?highlight=23)]
2. Откройте файл **IdentityModels.CS** для проекта, который находится в каталоге **Models** , и замените его содержимое следующим:

    [!code-csharp[Main](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/samples/sample7.cs)]

## <a name="running-the-application-and-verifying-the-database"></a>Запуск приложения и проверка базы данных

После выполнения шагов, описанных в предыдущих разделах, необходимо протестировать базу данных. Для этого выполните следующие действия.

1. Нажмите клавиши **CTRL + F5** , чтобы создать и запустить веб-приложение.
2. Перейдите на вкладку **Register (регистрация** ) в верхней части страницы:

   [Щелкните следующее изображение, чтобы развернуть его. ] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image4.jpg)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image3.jpg)
3. Введите новое имя пользователя и пароль, а затем нажмите кнопку **зарегистрировать**:

   [Щелкните следующее изображение, чтобы развернуть его. ] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image24.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image23.png)
4. На этом этапе в базе данных MySQL создаются ASP.NET Identity таблицы, и пользователь регистрируется и регистрируется в приложении:

   [Щелкните следующее изображение, чтобы развернуть его. ] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image6.jpg)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image5.jpg)

### <a name="installing-mysql-workbench-tool-to-verify-the-data"></a>Установка средства MySQL Workbench для проверки данных

1. Установка средства **MySQL Workbench** на [странице загрузок MySQL](http://dev.mysql.com/downloads/windows/installer/)
2. В мастере установки: вкладка **Выбор компонентов** выберите **MySQL Workbench** в разделе **приложения** .
3. Запустите приложение и добавьте новое подключение, используя данные строки подключения из базы данных Azure MySQL, созданной на беггинг из этого руководства.
4. После установления соединения проверьте **ASP.NET Identity** таблицы, созданные в **идентитимисклдатабасе.**
5. Вы увидите, что все ASP.NET Identity необходимые таблицы созданы, как показано на рисунке ниже:

   [Щелкните следующее изображение, чтобы развернуть его. ] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image8.jpg)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image7.jpg)
6. Просмотрите таблицу **aspnetusers** для экземпляра, чтобы проверить наличие записей при регистрации новых пользователей.

   [Щелкните следующее изображение, чтобы развернуть его. ] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image26.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image25.png)
