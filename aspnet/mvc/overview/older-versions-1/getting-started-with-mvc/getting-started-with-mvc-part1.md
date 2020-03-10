---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part1
title: Введение в ASP.NET MVC | Документация Майкрософт
author: shanselman
description: Это руководство для начинающих, в котором представлены основы ASP.NET MVC. Создание простого веб-приложения, считывающего и записывающего данные из базы данных.
ms.author: riande
ms.date: 08/14/2010
ms.assetid: bf4a1c19-0a94-4208-b268-a96ddcf26946
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part1
msc.type: authoredcontent
ms.openlocfilehash: f8f0014776ba1313119e8c39c63a216b0fc864e7
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78469800"
---
# <a name="intro-to-aspnet-mvc"></a>Введение в ASP.NET MVC

по [Скотт Hanselman](https://github.com/shanselman)

> > [!NOTE]
> > Обновленная версия, если этот учебник доступен [здесь](../../getting-started/introduction/getting-started.md) с помощью [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013). В новом руководстве используется ASP.NET MVC 5, который обеспечивает множество улучшений в рамках этого руководства.
>
>
> Это руководство для начинающих, в котором представлены основы ASP.NET MVC. Вы создадите простое веб-приложение, считывающее и записывающее данные из базы данных. Посетите [центр обучения ASP.NET MVC](../../../index.md) , чтобы найти другие руководства и примеры для ASP.NET MVC.

Давайте создадим наше первое веб-приложение ASP.NET MVC с помощью [Visual Web Developer 2010 Express](https://www.microsoft.com/express/Web/). Мы создадим небольшое приложение со списком фильмов, которое позволит нам создавать и перечислять фильмы.

## <a name="what-youll-build"></a>Что вы создадите

Ниже приведено два снимка экрана создаваемого приложения. Вы получите простую таблицу фильмов с различными столбцами.

[Список фильмов ![— Windows Internet Explorer (12)](getting-started-with-mvc-part1/_static/image2.png)](getting-started-with-mvc-part1/_static/image1.png)

И у вас будет форма создания, чтобы мы могли добавлять в список фильмы.

[![создания фильма — Windows Internet Explorer (2)](getting-started-with-mvc-part1/_static/image4.png)](getting-started-with-mvc-part1/_static/image3.png)

## <a name="skills-youll-learn"></a>Чему вы научитесь

В этом учебнике вы узнаете об основах создания веб-приложения ASP.NET MVC с помощью Visual Studio. Вы узнаете:

- Создание нового проекта MVC ASP.NET
- Создание новой базы данных с помощью SQL Server
- Создание контроллеров и представлений MVC ASP.NET
- Получение и отображение данных
- Как изменить данные и включить проверку данных
- Обновление схемы базы данных

## <a name="get-started"></a>Приступая к работе

Начните с запуска Visual Web Developer 2010 Express (теперь я называю его «VWD») и на начальном экране выберите пункт Создать проект.

Visual Web Developer — интегрированная среда разработки или интегрированная среда разработки. Как и при использовании Microsoft Word для написания документов, для создания приложений используется интегрированная среда разработки. В верхней части панели инструментов представлены различные доступные параметры, а также меню, которое можно было бы использовать для выбора файла | Новый проект.

[![Microsoft Visual Web Developer 2010 Express](getting-started-with-mvc-part1/_static/image6.png)](getting-started-with-mvc-part1/_static/image5.png)

## <a name="creating-your-first-application"></a>Создание первого приложения

Приложения можно создавать с помощью Visual Basic или Visual C#. Пока выберите элемент Visual C# слева, а затем — веб-приложение ASP.NET MVC 2. Присвойте проекту имя "фильмы" и нажмите кнопку ОК.

[![новый проект](getting-started-with-mvc-part1/_static/image8.png)](getting-started-with-mvc-part1/_static/image7.png)

В правой части обозреватель решений показаны все файлы и папки в приложении. В среднем окно находится в том месте, где вы редактируете код и тратите большую часть времени. Visual Studio использовала шаблон по умолчанию для только что созданного проекта MVC ASP.NET, поэтому у вас есть рабочее приложение, не делая ничего. Это простой "Hello World! и это хорошее место для начала работы с нашим приложением.

[![Microsoft Visual Web Developer 2010 Express](getting-started-with-mvc-part1/_static/image10.png)](getting-started-with-mvc-part1/_static/image9.png)

Нажмите кнопку "Воспроизведение" на панели инструментов.

![Начать отладку](getting-started-with-mvc-part1/_static/image11.png)

Это зеленая стрелка, указывающая вправо, которая будет компилировать программу и запускать приложение в веб-браузере.

*Примечание. Вы можете нажать клавишу F5 на клавиатуре или выбрать Отладка-&gt;начать отладку в меню "Отладка".*

Это приведет к тому, что Visual Web Developer запустит веб-сервер разработки и запустит наше веб-приложение (для этого не требуется настройка или действия, выполняемые вручную). Затем он запускает браузер и настраивает его для просмотра домашней страницы приложения. Обратите внимание, что в адресной строке браузера указано "localhost", а не что-то вроде example.com. Это связано с тем, что localhost всегда указывает на локальный компьютер, который в данном случае выполняет только что созданное приложение.

[Домашняя страница ![](getting-started-with-mvc-part1/_static/image13.png)](getting-started-with-mvc-part1/_static/image12.png)

Этот шаблон по умолчанию предоставляет две страницы для посещения и базовую страницу входа. Давайте изменим, как работает это приложение, и немного изучите ASP.NET MVC в процессе. Закройте браузер и измените код.

> [!div class="step-by-step"]
> [Дальше](getting-started-with-mvc-part2.md)
