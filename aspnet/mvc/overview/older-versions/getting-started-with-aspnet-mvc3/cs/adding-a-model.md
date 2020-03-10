---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/adding-a-model
title: Добавление модели (C#) | Документация Майкрософт
author: Rick-Anderson
description: Примечание. Обновленная версия этого учебника доступна здесь, в которой используется ASP.NET MVC 5 и Visual Studio 2013. Он более безопасен, гораздо проще в исполнении и демонстрации...
ms.author: riande
ms.date: 01/12/2011
ms.assetid: 42355b95-5f1f-413e-8d16-14cdfaaefcd8
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/adding-a-model
msc.type: authoredcontent
ms.openlocfilehash: a5f494eaa05bcfcd9d49873db728d71c1fd332c8
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78434898"
---
# <a name="adding-a-model-c"></a>Добавление модели (C#)

по [Рик Андерсон (](https://twitter.com/RickAndMSFT)

> В этом учебнике вы узнаете об основах создания веб-приложения ASP.NET MVC с помощью Microsoft Visual Web Developer 2010 Express с пакетом обновления 1 (SP1), который является бесплатной версией Microsoft Visual Studio. Прежде чем начать, убедитесь, что установлены предварительные требования, перечисленные ниже. Чтобы установить все эти компоненты, щелкните следующую ссылку: [установщик веб-платформы](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack). Кроме того, вы можете отдельно установить необходимые компоненты, используя следующие ссылки:
> 
> - [Предварительные требования для Visual Studio Web Developer Express SP1](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [Обновление инструментов ASP.NET MVC 3](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - [SQL Server Compact 4,0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(поддержка времени выполнения и средств)
> 
> Если вы используете Visual Studio 2010 вместо Visual Web Developer 2010, установите необходимые компоненты, щелкнув следующую ссылку: [Предварительные требования для Visual studio 2010](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack).
> 
> Для этого раздела доступен проект Visual C# Web Developer с исходным кодом. [Скачайте C# версию](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098). Если вы предпочитаете Visual Basic, переключитесь на [Visual Basic версию](../vb/adding-a-model.md) этого учебника.

## <a name="adding-a-model"></a>Добавление модели

В этом разделе вы добавите некоторые классы для управления фильмами в базе данных. Эти классы будут частью "Model" приложения ASP.NET MVC.

Вы будете использовать .NET Frameworkную технологию доступа к данным, известную как Entity Framework, для определения и работы с этими классами модели. Entity Framework (часто называемый EF) поддерживает парадигму разработки, именуемую *Code First*. Code First позволяет создавать объекты модели, создавая простые классы. (Они также известны как классы POCO, от "обычных объектов CLR".) Затем базу данных можно создать в режиме реального времени из классов, что позволяет выполнять очень четкий и быстрый рабочий процесс разработки.

## <a name="adding-model-classes"></a>Добавление классов модели

В **Обозреватель решений**щелкните правой кнопкой мыши папку *модели* , выберите **добавить**, а затем выберите **класс**.

![](adding-a-model/_static/image1.png)

Присвойте *классу* имя Movie.

[![Креатемовиекласс](adding-a-model/_static/image3.png)](adding-a-model/_static/image2.png)

Добавьте в класс `Movie` следующие пять свойств:

[!code-csharp[Main](adding-a-model/samples/sample1.cs)]

Мы будем использовать класс `Movie` для представления фильмов в базе данных. Каждый экземпляр объекта `Movie` будет соответствовать строке в таблице базы данных, а каждое свойство класса `Movie` будет сопоставляться со столбцом в таблице.

В том же файле добавьте следующий класс `MovieDBContext`:

[!code-csharp[Main](adding-a-model/samples/sample2.cs)]

Класс `MovieDBContext` представляет контекст базы данных Entity Framework Movie, который обрабатывает выборку, хранение и обновление экземпляров класса `Movie` в базе данных. `MovieDBContext` является производным от базового класса `DbContext`, предоставляемого Entity Framework. Дополнительные сведения о `DbContext` и `DbSet`см. [в статье улучшения производительности для Entity Framework](https://blogs.msdn.com/b/efdesign/archive/2010/06/21/productivity-improvements-for-the-entity-framework.aspx?wa=wsignin1.0).

Чтобы иметь возможность ссылаться на `DbContext` и `DbSet`, необходимо добавить в начало файла следующую инструкцию `using`:

[!code-csharp[Main](adding-a-model/samples/sample3.cs)]

Полный файл *Movie.CS* показан ниже.

[!code-csharp[Main](adding-a-model/samples/sample4.cs)]

## <a name="creating-a-connection-string-and-working-with-sql-server-compact"></a>Создание строки подключения и работа с SQL Server Compact

Созданный класс `MovieDBContext` обрабатывает задачу подключения к базе данных и сопоставление объектов `Movie` с записями базы данных. Одним из вопросов, которые вы можете спросить, является указание того, к какой базе данных будет подключаться. Это можно сделать, добавив сведения о подключении в файл *Web. config* приложения.

Откройте корневой файл *Web. config* приложения. (Не файл *Web. config* в папке *views* .) На рисунке ниже показаны оба файла *Web. config* . Откройте файл *Web. config* , обозначенный красным цветом.

![](adding-a-model/_static/image4.png)

Добавьте следующую строку подключения в элемент `<connectionStrings>` в файле *Web. config* .

[!code-xml[Main](adding-a-model/samples/sample5.xml)]

В следующем примере показана часть файла *Web. config* с добавленной новой строкой подключения:

[!code-xml[Main](adding-a-model/samples/sample6.xml)]

Небольшой объем кода и XML — это все, что необходимо для написания, чтобы представить и сохранить данные фильмов в базе данных.

Далее предстоит создать новый класс `MoviesController`, который можно использовать для отображения данных фильмов и предоставления пользователям возможности создавать новые списки фильмов.

> [!div class="step-by-step"]
> [Назад](adding-a-view.md)
> [Вперед](accessing-your-models-data-from-a-controller.md)
