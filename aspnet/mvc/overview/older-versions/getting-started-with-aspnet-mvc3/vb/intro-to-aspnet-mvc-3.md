---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/intro-to-aspnet-mvc-3
title: Введение в ASP.NET MVC 3 (VB) | Документация Майкрософт
author: Rick-Anderson
description: В этом учебнике вы узнаете об основах создания веб-приложения ASP.NET MVC с помощью Microsoft Visual Web Developer 2010 Express с пакетом обновления 1 (SP1)...
ms.author: riande
ms.date: 01/12/2011
ms.assetid: a1b3d789-93b4-487f-b90d-80c9c9b4f8fa
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/intro-to-aspnet-mvc-3
msc.type: authoredcontent
ms.openlocfilehash: 24f7de303ef7f5a457bd509ecc6bd0e3be7e3d9d
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/19/2020
ms.locfileid: "77456345"
---
# <a name="intro-to-aspnet-mvc-3-vb"></a>Введение в ASP.NET MVC 3 (VB)

по [Рик Андерсон (](https://twitter.com/RickAndMSFT)

> В этом учебнике вы узнаете об основах создания веб-приложения ASP.NET MVC с помощью Microsoft Visual Web Developer 2010 Express с пакетом обновления 1 (SP1), который является бесплатной версией Microsoft Visual Studio. Прежде чем начать, убедитесь, что установлены предварительные требования, перечисленные ниже. Чтобы установить все эти компоненты, щелкните следующую ссылку: [установщик веб-платформы](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack). Кроме того, вы можете отдельно установить необходимые компоненты, используя следующие ссылки:
> 
> - [Предварительные требования для Visual Studio Web Developer Express SP1](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [Обновление инструментов ASP.NET MVC 3](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - [SQL Server Compact 4,0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(поддержка времени выполнения и средств)
> 
> Если вы используете Visual Studio 2010 вместо Visual Web Developer 2010, установите необходимые компоненты, щелкнув следующую ссылку: [Предварительные требования для Visual studio 2010](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack).
> 
> Для этого раздела доступен проект Visual Web Developer с исходным кодом VB.NET. [Скачайте версию VB.NET](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098). При желании C#переключитесь на [ C# версию](../cs/intro-to-aspnet-mvc-3.md) этого учебника.

В этом учебнике вы узнаете об основах создания веб-приложения ASP.NET MVC с помощью Microsoft Visual Web Developer 2010 Express с пакетом обновления 1 (SP1), который является бесплатной версией Microsoft Visual Studio. Прежде чем начать, убедитесь, что установлены предварительные требования, перечисленные ниже. Чтобы установить все эти компоненты, щелкните следующую ссылку: [установщик веб-платформы](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack). Кроме того, вы можете отдельно установить необходимые компоненты, используя следующие ссылки:

- [Предварительные требования для Visual Studio Web Developer Express SP1](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
- [Обновление инструментов ASP.NET MVC 3](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
- [SQL Server Compact 4,0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(поддержка времени выполнения и средств)

Если вы используете Visual Studio 2010 вместо Visual Web Developer 2010, установите необходимые компоненты, щелкнув следующую ссылку: [Предварительные требования для Visual studio 2010](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack).

Для этого раздела доступен проект Visual Web Developer с исходным кодом VB. [Скачайте версию VB здесь](https://code.msdn.microsoft.com/Project/Download/FileDownload.aspx?ProjectName=aspnetmvcsamples&amp;DownloadId=14824). Если вы предпочитаете CSharp, переключитесь на [CSharp версии](../cs/intro-to-aspnet-mvc-3.md) этого руководства.

## <a name="what-youll-build"></a>Что вы создадите

Вы реализуете простое приложение с перечнем фильмов, которое поддерживает создание, изменение и перечисление фильмов из базы данных. Ниже приведены два снимка экрана создаваемого приложения. Он содержит страницу, на которой отображается список фильмов из базы данных:

[![Мовиесвисвариауссм](intro-to-aspnet-mvc-3/_static/image2.png)](intro-to-aspnet-mvc-3/_static/image1.png)

Кроме того, приложение позволяет добавлять, изменять и удалять фильмы, а также просматривать сведения о них. Все сценарии ввода данных включают проверку, чтобы убедиться, что данные, хранящиеся в базе данных, верны.

[![Креатеформсо](intro-to-aspnet-mvc-3/_static/image4.png)](intro-to-aspnet-mvc-3/_static/image3.png)

## <a name="skills-youll-learn"></a>Чему вы научитесь

В этом учебнике вы узнаете:

- Создание нового проекта MVC ASP.NET
- Создание новой базы данных с помощью Entity Framework кода — First
- Создание контроллеров и представлений MVC ASP.NET
- Получение и отображение данных
- Как изменить данные и включить проверку данных

## <a name="getting-started"></a>Начало работы

Начните с запуска Visual Web Developer 2010 Express ("VWD" для краткого) и выберите **создать проект** на **начальной** странице.

Visual Web Developer — это интегрированная среда разработки (IDE). Как и при использовании Microsoft Word для написания документов, для создания приложений используется интегрированная среда разработки. В Visual Web Developer есть панель инструментов, в верхней части которой показаны различные доступные параметры. Также есть меню, предоставляющее еще один способ выполнения задач в интегрированной среде разработки. (Например, вместо выбора **нового проекта** на **начальной** странице можно использовать меню и выбрать **файл** &gt; **Новый проект**).

[![](intro-to-aspnet-mvc-3/_static/image6.png)](intro-to-aspnet-mvc-3/_static/image5.png)

## <a name="creating-your-first-application"></a>Создание первого приложения

Вы можете создавать приложения, используя либо Visual Basic, либо визуальный C# элемент в качестве языка программирования. В этом руководстве выберите Visual Basic слева, а затем выберите **ASP.NET MVC 3 веб-приложение**. Присвойте проекту имя "MvcMovie" и нажмите кнопку **ОК**.

![1NewMVCproj_sm](intro-to-aspnet-mvc-3/_static/image7.png)

В диалоговом окне **Новый проект ASP.NET MVC 3** выберите **Интернет приложение**. Оставьте **Razor** в качестве подсистемы представления по умолчанию.

![1InternetAppRazor_SM](intro-to-aspnet-mvc-3/_static/image8.png)

Нажмите кнопку **ОК**. Visual Web Developer использовал шаблон по умолчанию для только что созданного проекта MVC ASP.NET, так что у вас уже есть рабочее приложение, не делая ничего. Это простой "Hello World!" и это хорошее место для запуска приложения.

[![](intro-to-aspnet-mvc-3/_static/image10.png)](intro-to-aspnet-mvc-3/_static/image9.png)

В меню **Отладка** выберите пункт **Начать отладку**.

![](intro-to-aspnet-mvc-3/_static/image11.png)

Обратите внимание, что для начала отладки используется сочетание клавиш F5.

F5 заставляет Visual Web Developer запустить веб-сервер разработки и запустить веб-приложение. Затем VWD запускает браузер и открывает домашнюю страницу приложения. Обратите внимание, что в адресной строке браузера указано `localhost` и не что-то вроде `example.com`. Это связано с тем, что `localhost` всегда указывает на локальный компьютер, который в данном случае выполняет только что созданное приложение. Когда VWD запускает веб-проект, для проекта используется случайный порт. На приведенном ниже рисунке случайным номером порта является 43246. Возможно, ваш проект использует другой номер порта.

![](intro-to-aspnet-mvc-3/_static/image12.png)

Этот шаблон по умолчанию предоставляет две страницы для посещения и базовую страницу входа. Давайте изменим, как работает это приложение, и немного изучите ASP.NET MVC в процессе. Закройте браузер и измените код.

> [!div class="step-by-step"]
> [Дальше](adding-a-controller.md)
