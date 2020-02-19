---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/adding-a-controller
title: Добавление контроллера (C#) | Документация Майкрософт
author: Rick-Anderson
description: В этом учебнике вы узнаете об основах создания веб-приложения ASP.NET MVC с помощью Microsoft Visual Web Developer 2010 Express с пакетом обновления 1 (SP1), который...
ms.author: riande
ms.date: 01/12/2011
ms.assetid: 0b8c56b5-fdf3-42dd-a866-98fbe0ab78a0
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/adding-a-controller
msc.type: authoredcontent
ms.openlocfilehash: 959116ff773f4ef466cda6b172e8321590b50e5b
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457843"
---
# <a name="adding-a-controller-c"></a>Добавление контроллера (C#)

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

MVC означает *модель-представление-контроллер*. MVC — это шаблон для разработки приложений, которые хорошо спроектированы и просты в обслуживании. Приложения на основе MVC содержат:

- Controllers: классы, которые обрабатывали входящие запросы к приложению, получают данные модели, а затем указывают шаблоны представлений, возвращающие ответ клиенту.
- Модели: классы, представляющие данные приложения и использующие логику проверки для применения бизнес-правил для этих данных.
- Представления: файлы шаблонов, используемые приложением для динамического создания ответов HTML.

Мы покажем все эти концепции в этой серии руководств и покажем, как их использовать для создания приложения.

Начнем с создания класса Controller. В **Обозреватель решений**щелкните правой кнопкой мыши папку *Controllers* и выберите пункт **Добавить контроллер**.

[![](adding-a-controller/_static/image2.png)](adding-a-controller/_static/image1.png)

Присвойте новому контроллеру имя "HelloWorldController". Оставьте шаблон по умолчанию **пустым контроллером** и нажмите кнопку **Добавить**.

[![Аддхелловорлдконтроллер](adding-a-controller/_static/image4.png)](adding-a-controller/_static/image3.png)

Обратите внимание, что в **Обозреватель решений** создан новый файл с именем *HelloWorldController.CS*. Файл открыт в интегрированной среде разработки.

![](adding-a-controller/_static/image5.png)

В блоке `public class HelloWorldController` создайте два метода, которые выглядят как следующий код. В качестве примера контроллер вернет строку HTML.

[!code-csharp[Main](adding-a-controller/samples/sample1.cs)]

Контроллеру присваивается имя `HelloWorldController`, а первым приведенному выше методу присваивается имя `Index`. Давайте выберем его из браузера. Запустите приложение (нажмите клавишу F5 или CTRL + F5). В браузере добавьте "HelloWorld" к пути в адресной строке. (Например, на рисунке ниже `http://localhost:43246/HelloWorld.`) Страница в браузере будет выглядеть, как на следующем снимке экрана. В приведенном выше методе код возвратил строку напрямую. Вы сообщили системе, что просто возвращали какой-либо код HTML.

![](adding-a-controller/_static/image6.png)

ASP.NET MVC вызывает различные классы контроллеров (и различные методы действий в них) в зависимости от входящего URL-адреса. Логика сопоставления по умолчанию, используемая ASP.NET MVC, использует следующий формат для определения вызываемого кода:

`/[Controller]/[ActionName]/[Parameters]`

Первая часть URL-адреса определяет класс контроллера для выполнения. Поэтому */хелловорлд* сопоставляется с классом `HelloWorldController`. Вторая часть URL-адреса определяет метод действия для выполняемого класса. Поэтому */хелловорлд/индекс* приведет к выполнению метода `Index` класса `HelloWorldController`. Обратите внимание, что нам пришлось бы перейти к */хелловорлд* , а метод `Index` использовался по умолчанию. Это вызвано тем, что метод, именуемый `Index`, является методом по умолчанию, который будет вызываться на контроллере, если он не указан явно.

Перейдите по адресу `http://localhost:xxxx/HelloWorld/Welcome`. Выполняется метод `Welcome`, который возвращает строку "This is the Welcome action method..." (Это метод действия Welcome...). Сопоставление MVC по умолчанию — `/[Controller]/[ActionName]/[Parameters]`. Для этого URL-адреса заданы контроллер `HelloWorld` и метод действия `Welcome`. Часть URL-адреса `[Parameters]` на данный момент еще не использовалась.

![](adding-a-controller/_static/image7.png)

Давайте немного изменим пример, чтобы вы могли передать некоторые сведения о параметрах с URL-адреса на контроллер (например, */хелловорлд/велкоме? Name = скотт&amp;нумтимес = 4*). Измените метод `Welcome`, включив в него два параметра, как показано ниже. Обратите внимание, что в C# коде используется функция необязательного параметра, указывающая, что параметр `numTimes` по умолчанию должен иметь значение 1, если для этого параметра не было передано никакого значения.

[!code-csharp[Main](adding-a-controller/samples/sample2.cs)]

Запустите приложение и перейдите по URL-адресу примера (`http://localhost:xxxx/HelloWorld/Welcome?name=Scott&numtimes=4)`. Вы можете попробовать различные значения `name` и `numtimes` в URL-адресе. Система автоматически сопоставляет именованные параметры из строки запроса в адресной строке с параметрами в методе.

![](adding-a-controller/_static/image8.png)

В этих примерах контроллер выполняет "VC" части MVC, т. е. представление и контроллер работают. Контроллер возвращает HTML напрямую. Обычно вы не хотите, чтобы контроллеры возвращали HTML напрямую, так как это очень громоздкий для кода. Вместо этого мы обычно используем отдельный файл шаблона представления для создания ответа HTML. Давайте посмотрим, как это можно сделать.

> [!div class="step-by-step"]
> [Назад](intro-to-aspnet-mvc-3.md)
> [Вперед](adding-a-view.md)
