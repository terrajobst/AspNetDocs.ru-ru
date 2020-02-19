---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/adding-a-controller
title: Добавление контроллера (VB) | Документация Майкрософт
author: Rick-Anderson
description: В этом учебнике вы узнаете об основах создания веб-приложения ASP.NET MVC с помощью Microsoft Visual Web Developer 2010 Express с пакетом обновления 1 (SP1)...
ms.author: riande
ms.date: 01/12/2011
ms.assetid: 741259e1-54ac-4f71-b4e8-2bd5560bb950
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/adding-a-controller
msc.type: authoredcontent
ms.openlocfilehash: 2e77f62a9796211b0e59a99c71bc532659b7cb92
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457414"
---
# <a name="adding-a-controller-vb"></a>Добавление контроллера (VB)

по [Рик Андерсон (](https://twitter.com/RickAndMSFT)

> В этом учебнике вы узнаете об основах создания веб-приложения ASP.NET MVC с помощью Microsoft Visual Web Developer 2010 Express с пакетом обновления 1 (SP1), который является бесплатной версией Microsoft Visual Studio. Прежде чем начать, убедитесь, что установлены предварительные требования, перечисленные ниже. Чтобы установить все эти компоненты, щелкните следующую ссылку: [установщик веб-платформы](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack). Кроме того, вы можете отдельно установить необходимые компоненты, используя следующие ссылки:
> 
> - [Предварительные требования для Visual Studio Web Developer Express SP1](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [Обновление инструментов ASP.NET MVC 3](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - [SQL Server Compact 4,0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(поддержка времени выполнения и средств)
> 
> Если вы используете Visual Studio 2010 вместо Visual Web Developer 2010, установите необходимые компоненты, щелкнув следующую ссылку: [Предварительные требования для Visual studio 2010](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack).
> 
> Для этого раздела доступен проект Visual Web Developer с исходным кодом VB.NET. [Скачайте версию VB.NET](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098). При желании C#переключитесь на [ C# версию](../cs/adding-a-controller.md) этого учебника.

MVC означает *модель-представление-контроллер*. MVC — это шаблон для разработки приложений, в котором каждая часть имеет отдельную ответственность:

- Model: данные для приложения.
- Представления: файлы шаблонов, которые приложение будет использовать для динамического создания ответов HTML.
- Контроллеры: классы, которые обрабатывают входящие запросы URL-адресов к приложению, получают данные модели, а затем указывают шаблоны представления, которые отображают ответ клиенту.

Мы будем рассматривать все эти концепции в этом учебнике и покажу, как их использовать для создания приложения.

Создайте новый контроллер, щелкнув правой кнопкой мыши папку *Controllers* в **Обозреватель решений** и выбрав пункт **Добавить контроллер**.

[![аддконтроллер](adding-a-controller/_static/image2.png "аддконтроллер")](adding-a-controller/_static/image1.png)

Присвойте новому контроллеру имя &quot;HelloWorldController&quot; и нажмите кнопку **Добавить**.

[![2AddEmptyController](adding-a-controller/_static/image4.png "2AddEmptyController")](adding-a-controller/_static/image3.png)

Обратите внимание, что в **Обозреватель решений** справа, что был создан новый файл с именем *HelloWorldController.CS* и файл открыт в интегрированной среде разработки.

В новом блоке `public class HelloWorldController` создайте два новых метода, которые выглядят как следующий код. В качестве примера мы возвращаем строку HTML непосредственно из контроллера.

[!code-vb[Main](adding-a-controller/samples/sample1.vb)]

Контроллер имеет имя `HelloWorldController` а новый метод называется `Index`. Запустите приложение (нажмите клавишу F5 или CTRL + F5). После запуска браузера добавьте &quot;HelloWorld&quot; в путь в адресной строке. (На моем компьютере это `http://localhost:43246/HelloWorld`) Ваш браузер будет выглядеть, как показано на снимке экрана ниже. В приведенном выше методе код возвратил строку напрямую. Мы сказали, что система просто возвращала какой-либо код HTML, и это сделало!

![](adding-a-controller/_static/image5.png)

ASP.NET MVC вызывает различные классы контроллеров (и различные методы действий в них) в зависимости от входящего URL-адреса. Логика сопоставления по умолчанию, используемая ASP.NET MVC, использует следующий формат для управления тем, какой код вызывается:

`/[Controller]/[ActionName]/[Parameters]`

Первая часть URL-адреса определяет класс контроллера для выполнения. Поэтому */хелловорлд* сопоставляется с классом `HelloWorldController`. Вторая часть URL-адреса определяет метод действия для выполняемого класса. Поэтому */хелловорлд/индекс* приведет к выполнению метода `Index` класса `HelloWorldController`. Обратите внимание, что нам пришлось бы посетить */хелловорлд* выше, а метод `Index` использовался по умолчанию. Это вызвано тем, что метод, именуемый `Index`, является методом по умолчанию, который будет вызываться на контроллере, если он не указан явно.

Перейдите по адресу `http://localhost:xxxx/HelloWorld/Welcome`. Метод `Welcome` выполняет и возвращает строку, &quot;это метод действия приветствия...&quot;. Сопоставление MVC по умолчанию — `/[Controller]/[ActionName]/[Parameters]`. Для этого URL-адреса контроллер `HelloWorld`, а `Welcome` является методом. Мы еще не использовали `[Parameters]` часть URL-адреса.

![](adding-a-controller/_static/image6.png)

Давайте немного изменим пример, чтобы мы могли передать некоторые сведения о параметрах из URL-адреса в контроллер (например, */хелловорлд/велкоме? Name = скотт&amp;нумтимес = 4*). Измените метод `Welcome`, включив в него два параметра, как показано ниже. Обратите внимание, что мы использовали необязательный параметр VB, чтобы указать, что параметру `numTimes` по умолчанию будет присвоено значение 1, если для этого параметра не было передано никакого значения.

[!code-vb[Main](adding-a-controller/samples/sample2.vb)]

Запустите приложение и перейдите к `http://localhost:xxxx/HelloWorld/Welcome?name=Scott&numtimes=4` **.** Можно попробовать использовать разные значения для `name` и `numtimes`. Система автоматически сопоставляет именованные параметры из строки запроса в адресной строке с параметрами в методе.

![](adding-a-controller/_static/image7.png)

В этих примерах контроллер выполняет VC-часть MVC, то есть работу по просмотру и контроллеру. Контроллер возвращает HTML напрямую. Обычно мы не хотим, чтобы контроллеры возвращали HTML напрямую, так как это очень громоздкий для кода. Вместо этого мы обычно используем отдельный файл шаблона представления для создания ответа HTML. Давайте посмотрим, как это можно сделать.

> [!div class="step-by-step"]
> [Назад](intro-to-aspnet-mvc-3.md)
> [Вперед](adding-a-view.md)
