---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3
title: Введение в ASP.NET MVC 3 (C#) | Документация Майкрософт
author: Rick-Anderson
description: В этом учебнике вы узнаете об основах создания веб-приложения ASP.NET MVC с помощью Microsoft Visual Web Developer 2010 Express с пакетом обновления 1 (SP1)...
ms.author: riande
ms.date: 01/12/2011
ms.assetid: 86a80b35-88bd-4b7c-bd58-f6e7997197d4
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3
msc.type: authoredcontent
ms.openlocfilehash: e71275c93558c0b6ca087a145786e8c846b69721
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78434730"
---
# <a name="intro-to-aspnet-mvc-3-c"></a>Введение в ASP.NET MVC 3 (C#)

по [Рик Андерсон (](https://twitter.com/RickAndMSFT)

> > [!NOTE]
> > Обновленная версия этого учебника доступна [здесь](../../../getting-started/introduction/getting-started.md) , в которой используется ASP.NET MVC 5 и Visual Studio 2013. Он более безопасен, гораздо проще следовать и демонстрирует дополнительные функции.
> 
> 
> В этом учебнике вы узнаете об основах создания веб-приложения ASP.NET MVC с помощью Microsoft Visual Web Developer 2010 Express с пакетом обновления 1 (SP1), который является бесплатной версией Microsoft Visual Studio. Прежде чем начать, убедитесь, что установлены предварительные требования, перечисленные ниже. Чтобы установить все эти компоненты, щелкните следующую ссылку: [установщик веб-платформы](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack). Кроме того, вы можете отдельно установить необходимые компоненты, используя следующие ссылки:
> 
> - [Предварительные требования для Visual Studio Web Developer Express SP1](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [Обновление инструментов ASP.NET MVC 3](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - [SQL Server Compact 4,0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(поддержка времени выполнения и средств)
> 
> Если вы используете Visual Studio 2010 вместо Visual Web Developer 2010, установите необходимые компоненты, щелкнув следующую ссылку: [Предварительные требования для Visual studio 2010](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack).
> 
> Для этого раздела доступен проект Visual C# Web Developer с исходным кодом. [Скачайте C# версию](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098). Если вы предпочитаете Visual Basic, переключитесь на [Visual Basic версию](../vb/intro-to-aspnet-mvc-3.md) этого учебника.

## <a name="what-youll-build"></a>Что вы создадите

Вы реализуете простое приложение с перечнем фильмов, которое поддерживает создание, изменение и перечисление фильмов из базы данных. Ниже приведены два снимка экрана создаваемого приложения. Он содержит страницу, на которой отображается список фильмов из базы данных:

![мовиесвисвариауссм](intro-to-aspnet-mvc-3/_static/image1.png)

Кроме того, приложение позволяет добавлять, изменять и удалять фильмы, а также просматривать сведения о них. Все сценарии ввода данных включают проверку, чтобы убедиться, что данные, хранящиеся в базе данных, верны.

![](intro-to-aspnet-mvc-3/_static/image2.png)

## <a name="skills-youll-learn"></a>Чему вы научитесь

В этом учебнике вы узнаете:

- Создание нового проекта MVC ASP.NET.
- Создание контроллеров и представлений MVC ASP.NET.
- Создание новой базы данных с помощью Entity Framework парадигмы Code First.
- Получение и отображение данных.
- Как изменить данные и включить проверку данных.

## <a name="getting-started"></a>Приступая к работе

Начните с запуска Visual Web Developer 2010 Express («Visual Web Developer») и выберите пункт **создать проект** на **начальной** странице.

Visual Web Developer — это интегрированная среда разработки (IDE). Как и при использовании Microsoft Word для написания документов, для создания приложений используется интегрированная среда разработки. В Visual Web Developer есть панель инструментов, в верхней части которой показаны различные доступные параметры. Также есть меню, предоставляющее еще один способ выполнения задач в интегрированной среде разработки. (Например, вместо выбора **нового проекта** на **начальной** странице можно использовать меню и выбрать **файл** &gt; **Новый проект**).

[![](intro-to-aspnet-mvc-3/_static/image4.png)](intro-to-aspnet-mvc-3/_static/image3.png)

## <a name="creating-your-first-application"></a>Создание первого приложения

Приложения можно создавать с помощью Visual Basic или визуального C# элемента в качестве языка программирования. Выберите элемент C# Visual слева, а затем выберите **ASP.NET MVC 3 веб-приложение**. Присвойте проекту имя "MvcMovie" и нажмите кнопку **ОК**. (Если вы предпочитаете Visual Basic, переключитесь на [Visual Basic версию](../vb/intro-to-aspnet-mvc-3.md) этого учебника.)

![](intro-to-aspnet-mvc-3/_static/image5.png)

В диалоговом окне **Новый проект ASP.NET MVC 3** выберите **Интернет приложение**. Установите флажок **использовать разметку HTML5** и оставьте **Razor** в качестве ядра представления по умолчанию.

![](intro-to-aspnet-mvc-3/_static/image6.png)

Нажмите кнопку **ОК**. Visual Web Developer использовал шаблон по умолчанию для только что созданного проекта MVC ASP.NET, так что у вас уже есть рабочее приложение, не делая ничего. Это простой "Hello World!" и это хорошее место для запуска приложения.

[![](intro-to-aspnet-mvc-3/_static/image8.png)](intro-to-aspnet-mvc-3/_static/image7.png)

В меню **Отладка** выберите пункт **Начать отладку**.

![](intro-to-aspnet-mvc-3/_static/image9.png)

Обратите внимание, что для начала отладки используется сочетание клавиш F5.

F5 заставляет Visual Web Developer запустить веб-сервер разработки и запустить веб-приложение. Visual Web Developer запускает браузер и открывает домашнюю страницу приложения. Обратите внимание, что в адресной строке браузера указано `localhost` и не что-то вроде `example.com`. Это связано с тем, что `localhost` всегда указывает на локальный компьютер, который в данном случае выполняет только что созданное приложение. Когда Visual Web Developer запускает веб-проект, для веб-сервера используется случайный порт. На приведенном ниже рисунке случайным номером порта является 43246. При запуске приложения вы, вероятно, увидите другой номер порта.

![](intro-to-aspnet-mvc-3/_static/image10.png)

Сразу после этого шаблон по умолчанию предоставляет две страницы для посещения и базовую страницу входа. Следующим шагом является изменение того, как это приложение работает, и немного изучите ASP.NET MVC в процессе. Закройте браузер и измените код.

> [!div class="step-by-step"]
> [Дальше](adding-a-controller.md)
