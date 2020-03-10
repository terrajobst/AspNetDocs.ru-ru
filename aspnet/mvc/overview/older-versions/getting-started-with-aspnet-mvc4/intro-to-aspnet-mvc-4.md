---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc4/intro-to-aspnet-mvc-4
title: Введение в ASP.NET MVC 4 | Документация Майкрософт
author: Rick-Anderson
description: Обновленная версия, если этот учебник доступен здесь с помощью Visual Studio 2013. В новом руководстве используется ASP.NET MVC 5, который предоставляет множество улучшений по сравнению с t...
ms.author: riande
ms.date: 08/15/2012
ms.assetid: ed66530a-04d5-49eb-b76a-85be1f57c437
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc4/intro-to-aspnet-mvc-4
msc.type: authoredcontent
ms.openlocfilehash: 51709a9c6ddb39b8fcd1cd94cd08d530a595825a
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78485280"
---
# <a name="intro-to-aspnet-mvc-4"></a>Введение в ASP.NET MVC 4

по [Рик Андерсон (](https://twitter.com/RickAndMSFT)

> Обновленная версия, если этот учебник доступен [здесь](../../getting-started/introduction/getting-started.md) с помощью [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013). В новом руководстве используется ASP.NET MVC 5, который обеспечивает множество улучшений в рамках этого руководства.
>
> В этом учебнике вы узнаете об основах создания веб-приложения ASP.NET MVC 4 с помощью Microsoft [Visual Studio Express 2012](https://www.microsoft.com/visualstudio/11/products/express) или Visual Web Developer 2010 Express с пакетом обновления 1 (SP1). Visual Studio 2012 рекомендуется, для завершения работы с этим руководством не нужно устанавливать ничего. Если вы используете Visual Studio 2010, необходимо установить перечисленные ниже компоненты. Их можно установить, перейдя по следующим ссылкам:
>
> - [Предварительные требования для Visual Studio Web Developer Express SP1](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [Установщик ВПИ для ASP.NET MVC 4](https://go.microsoft.com/fwlink/?LinkId=243392)
> - [LocalDB](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLLocalDBOnly_11_0)
> - [SSDT](https://blogs.msdn.com/b/rickandy/archive/2012/08/02/installing-and-using-sql-server-data-tools-ssdt-on-visual-studio-2010-and-vwd.aspx)
>
> Если вы используете Visual Studio 2010 вместо Visual Web Developer 2010, установите [установщик ВПИ для ASP.NET MVC 4](https://go.microsoft.com/fwlink/?LinkId=243392) и: [Предварительные требования для Visual Studio 2010](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)
>
> Для этого раздела доступен проект Visual C# Web Developer с исходным кодом. [Скачайте C# версию](https://code.msdn.microsoft.com/Intro-to-ASPNET-MVC-4-61d0219d/file/114480/1/MvcMovie.zip).
>
> В этом руководстве вы запускаете приложение в Visual Studio. Можно также сделать приложение доступным через Интернет, развернув его на поставщик услуг размещения. Корпорация Майкрософт предлагает бесплатное веб-размещение для 10 веб-сайтов в [бесплатной пробной учетной записи Windows Azure](https://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A443DD604). Сведения о том, как развернуть веб-проект Visual Studio на веб-сайте Windows Azure, см. в статье [Создание и развертывание веб-сайта ASP.NET и базы данных SQL с помощью Visual Studio](https://docs.microsoft.com/dotnet/azure/). В этом учебнике также показано, как использовать Entity Framework Code First Migrations для развертывания базы данных SQL Server в базе данных SQL Windows Azure (ранее SQL Azure).
>
> Этот учебник написан на Рик Андерсон (( [@RickAndMSFT](https://twitter.com/#!/RickAndMSFT) ).

## <a name="what-youll-build"></a>Что вы создадите

> [!NOTE]
> Обновленная версия, если этот учебник доступен [здесь](../../getting-started/introduction/getting-started.md) с помощью [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013). В новом руководстве используется ASP.NET MVC 5, который обеспечивает множество улучшений в рамках этого руководства.

Вы реализуете простое приложение с перечнем фильмов, которое поддерживает создание, редактирование, Поиск и перечисление фильмов из базы данных. Ниже приведены два снимка экрана создаваемого приложения. Он содержит страницу, на которой отображается список фильмов из базы данных:

![](intro-to-aspnet-mvc-4/_static/image1.png)

Кроме того, приложение позволяет добавлять, изменять и удалять фильмы, а также просматривать сведения о них. Все сценарии ввода данных включают проверку, чтобы убедиться, что данные, хранящиеся в базе данных, верны.

![](intro-to-aspnet-mvc-4/_static/image2.png)

## <a name="getting-started"></a>Приступая к работе

Начните с запуска Visual Studio Express 2012 или Visual Web Developer 2010 Express. Большинство снимков экрана в этой серии используют Visual Studio Express 2012, но вы можете пройти это руководство с помощью Visual Studio 2010/с пакетом обновления 1 (SP1), Visual Studio 2012, Visual Studio Express 2012 или Visual Web Developer 2010 Express. На **начальной** странице выберите **Новый проект** .

Visual Studio — это интегрированная среда разработки (IDE). Как и при использовании Microsoft Word для написания документов, для создания приложений используется интегрированная среда разработки. В Visual Studio есть панель инструментов, в верхней части которой показаны различные доступные параметры. Также есть меню, предоставляющее еще один способ выполнения задач в интегрированной среде разработки. (Например, вместо выбора **нового проекта** на **начальной** странице можно использовать меню и выбрать **файл** &gt; **Новый проект**).

![](intro-to-aspnet-mvc-4/_static/image3.png)

## <a name="creating-your-first-application"></a>Создание первого приложения

Приложения можно создавать с помощью Visual Basic или визуального C# элемента в качестве языка программирования. Выберите элемент C# Visual слева, а затем выберите **ASP.NET MVC 4 веб-приложение**. Присвойте проекту имя &quot;MvcMovie&quot; и нажмите кнопку **ОК**.

![](intro-to-aspnet-mvc-4/_static/image4.png)

В диалоговом окне **Новый проект ASP.NET MVC 4** выберите **Интернет приложение**. Оставьте **Razor** в качестве подсистемы представления по умолчанию.

![](intro-to-aspnet-mvc-4/_static/image5.png)

Нажмите кнопку **ОК**. Visual Studio использовала шаблон по умолчанию для только что созданного проекта MVC ASP.NET, поэтому у вас есть рабочее приложение, не делая ничего. Это простой &quot;Hello World!&quot; проект, и это хорошее место для запуска приложения.

![](intro-to-aspnet-mvc-4/_static/image6.png)

В меню **Отладка** выберите пункт **Начать отладку**.

![](intro-to-aspnet-mvc-4/_static/image7.png)

Обратите внимание, что для начала отладки используется сочетание клавиш F5.

F5 заставляет Visual Studio запустить IIS Express и запускать веб-приложение. Затем Visual Studio запустит браузер и откроет домашнюю страницу приложения. Обратите внимание, что в адресной строке браузера указано `localhost` и не что-то вроде `example.com`. Это связано с тем, что `localhost` всегда указывает на локальный компьютер, который в данном случае выполняет только что созданное приложение. Когда Visual Studio выполняет веб-проект, для веб-сервера используется случайный порт. На рисунке ниже показан номер порта 41788. При запуске приложения вы, вероятно, увидите другой номер порта.

![](intro-to-aspnet-mvc-4/_static/image8.png)

По умолчанию в этом шаблоне содержится Домашняя страница, Контактная информация и сведения о них. Он также предоставляет поддержку для регистрации и входа в систему и ссылки на Facebook и Twitter. Следующим шагом является изменение способа работы этого приложения и немного подробнее о ASP.NET MVC. Закройте браузер и измените код.

> [!div class="step-by-step"]
> [Дальше](adding-a-controller.md)
