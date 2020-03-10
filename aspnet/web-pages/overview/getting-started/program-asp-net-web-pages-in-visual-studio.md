---
uid: aspnet/web-pages/overview/getting-started/program-asp-net-web-pages-in-visual-studio
title: Программирование веб-страницы ASP.NET (Razor) с помощью Visual Studio | Документация Майкрософт
author: Rick-Anderson
description: В этом приложении объясняется, как можно использовать Visual Studio 2010 или Visual Web Developer 2010 Express для программирования веб-страницы ASP.NET с синтаксис Razor.
ms.author: riande
ms.date: 02/13/2014
ms.assetid: 0acfec5a-48f2-4766-a801-a0f426966f0a
msc.legacyurl: /web-pages/overview/getting-started/program-asp-net-web-pages-in-visual-studio
msc.type: authoredcontent
ms.openlocfilehash: 1a76098779d05912bf7bdf2de5fdce024770752c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78514296"
---
# <a name="programming-aspnet-web-pages-razor-using-visual-studio"></a>Программирование веб-страницы ASP.NET (Razor) с помощью Visual Studio

от [Tom фитзмаккен](https://github.com/tfitzmac)

> В этой статье объясняется, как можно использовать Visual Studio или Visual Web Developer Express для программирования веб-сайтов веб-страницы ASP.NET (Razor).
>
> Что вы узнаете
>
> - Что необходимо установить (если что-либо) для работы с веб-страницы ASP.NET в вашей версии Visual Studio.
> - Как добавить поддержку для веб-страницы ASP.NET в Visual Web Developer 2010 Express.
> - Использование функций в Visual Studio для работы с ASP.NET Razor Pages, включая IntelliSense и отладчик.
>
>
> ## <a name="software-versions-used-in-the-tutorial"></a>Версии программного обеспечения, используемые в этом руководстве
>
>
> - Веб-страницы ASP.NET (Razor) 3
> - Visual Studio 2013
> - WebMatrix 3
>
>
> Этот учебник также работает с веб-страницы ASP.NET 2, Visual Studio 2012, Visual Studio 2010 и WebMatrix 2.

ASP.NET веб-страницы можно программировать с помощью синтаксис Razor WebMatrix или многих других редакторов кода. Вы также можете использовать Microsoft Visual Studio, который является полнофункциональной интегрированной средой разработки (IDE), предоставляющей мощный набор средств для создания различных типов приложений (не только для веб-сайтов). Для работы с ASP.NET Razor Pages можно использовать [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017).

В Visual Studio есть две полезные функции для программирования с ASP.NET Razor Web Pages:

- *Технология IntelliSense*. Функция IntelliSense, встроенная в Visual Studio, является более всеобъемлющей, чем IntelliSense в WebMatrix.
- *Отладчик*. Отладчик позволяет устранять неполадки в коде путем остановки программы во время ее выполнения, проверки переменных и пошагового выполнения кода по строке.

## <a name="using-visual-studio-with-different-versions-of-aspnet-web-pages"></a>Использование Visual Studio с разными версиями веб-страницы ASP.NET

Для разработки веб-приложений ASP.NET в Visual Studio 2017 установите рабочую нагрузку **ASP.NET и веб-разработку** .

Visual Studio 2012 и Visual Studio 2013 включают поддержку веб-страницы ASP.NET. (Пакеты, необходимые для поддержки веб-страницы ASP.NET, устанавливаются при установке Visual Studio.)

Visual Studio 2010 не включает поддержку по умолчанию для веб-страницы ASP.NET. Чтобы использовать веб-страницы ASP.NET с Visual Studio 2010, необходимо установить пакет MVC ASP.NET. Чтобы получить веб-страницы ASP.NET 2, установите ASP.NET MVC 4.

В следующей таблице приведены сведения о поддержке веб-страницы ASP.NET в различных версиях Visual Studio.

|  | Visual Studio 2010 | Visual Studio 2012 | Visual Studio 2013 |
| --- | --- | --- | --- |
| **Веб-страницы ASP.NET 2** | Установка ASP.NET MVC 4 | Включает | Включает |
| **Веб-страницы ASP.NET 3** |  | Обновление до веб-страницы ASP.NET 3 через NuGet | Включает |

Сведения о работе с Visual Studio 2010 см. [в разделе Установка поддержки для веб-страницы ASP.NET в Visual studio 2010](#vs2010support).

## <a name="launching-visual-studio-from-webmatrix"></a>Запуск Visual Studio из WebMatrix

Если вы запустили проект в WebMatrix и хотите переключиться на Visual Studio, WebMatrix предоставляет кнопку для простого открытия проекта в Visual Studio. Чтобы эта кнопка была доступна, на компьютере должна быть установлена Visual Studio. На следующем рисунке показана кнопка в WebMatrix.

![Запуск Visual Studio](program-asp-net-web-pages-in-visual-studio/_static/image1.png)

При нажатии кнопки проект открывается в Visual Studio. Вы можете переключаться между WebMatrix и Visual Studio без каких бы то ни было проблем. Вы получите уведомления, если какие бы то ни было изменения в другой среде, и необходимо перезагрузить их для получения последних изменений.

## <a name="creating-aspnet-razor-site-in-visual-studio"></a>Создание сайта ASP.NET Razor в Visual Studio

Чтобы создать веб-сайт ASP.NET Razor в Visual Studio, выполните следующие действия.

1. Запустите Visual Studio.
2. В меню **файл** выберите пункт **создать веб-сайт**.

    ![создать новый веб-сайт](program-asp-net-web-pages-in-visual-studio/_static/image2.png)
3. В диалоговом окне **новый веб-сайт** выберите используемый язык (визуальный C# или Visual Basic).
4. Выберите шаблон **веб-сайт ASP.NET (Razor)** .

    ![сайт Razor](program-asp-net-web-pages-in-visual-studio/_static/image3.png)
5. Нажмите кнопку **ОК**.

Новый проект существует и заполняется веб-страницами по умолчанию, которые помогут приступить к работе.

### <a name="using-intellisense"></a>Using IntelliSense

Теперь, когда вы создали сайт, можно увидеть, как IntelliSense работает в Visual Studio.

1. На веб-сайте, который вы только что создали, откройте страницу *Default. cshtml* .
2. После тегов `<h3>` на странице введите `@ServerInfo.` (включая точку). Обратите внимание, как IntelliSense отображает доступные методы для модуля поддержки `ServerInfo` в раскрывающемся списке.

    ![IntelliSense](program-asp-net-web-pages-in-visual-studio/_static/image4.png)
3. Выберите метод `GetHtml` из списка и нажмите клавишу ВВОД. IntelliSense автоматически заполняет метод. (Как и в случае любого C#метода в, необходимо добавить `()` символов после метода.) Завершенный код для метода `GetHtml` выглядит, как в следующем примере:

    [!code-cshtml[Main](program-asp-net-web-pages-in-visual-studio/samples/sample1.cshtml)]
4. Нажмите клавиши CTRL + F5, чтобы запустить страницу. Вот как выглядит страница при отображении в браузере:

    ![страница по умолчанию в браузере](program-asp-net-web-pages-in-visual-studio/_static/image5.png)
5. Закройте браузер.

### <a name="using-the-debugger"></a>Использование отладчика

1. В верхней части страницы *Default. cshtml* после строки, начинающейся с `Page.Title`, добавьте следующую строку кода:

    [!code-csharp[Main](program-asp-net-web-pages-in-visual-studio/samples/sample2.cs)]
2. В сером поле редактора слева от кода нажмите кнопку Далее рядом с новой строкой, чтобы добавить *точку останова*. Точка останова — это маркер, указывающий отладчику на необходимость остановки выполнения программы на этом этапе, чтобы можно было увидеть, что происходит.

    ![Задать точку останова](program-asp-net-web-pages-in-visual-studio/_static/image6.png)
3. Удалите вызов метода `ServerInfo.GetHtml` и добавьте в его место вызов `@myTime` переменной. Этот вызов отображает текущее значение времени, возвращаемое новой строкой кода.
4. Нажмите клавишу F5, чтобы запустить страницу в отладчике. Страница останавливается в заданной точке останова. На следующем рисунке показано, как выглядит страница в редакторе с точкой останова (желтым цветом).

    ![Отладка точки останова](program-asp-net-web-pages-in-visual-studio/_static/image7.png)
5. На панели инструментов Отладка нажмите кнопку **Шаг с заходом** (или нажмите клавишу F11), чтобы выполнить следующую строку кода. Каждый раз при нажатии этой кнопки выполняется переход к следующей строке кода.

    ![Кнопка "шаг с заходом"](program-asp-net-web-pages-in-visual-studio/_static/image8.png)
6. Изучите значение переменной `myTime`, нажимая на нее указатель мыши или проверив значения, отображаемые в окнах " **локальные** " и " **Стек вызовов** ". В Visual Studio отобразится значение переменной.

    ![показывать значение времени](program-asp-net-web-pages-in-visual-studio/_static/image9.png)
7. После завершения проверки переменной и пошагового выполнения кода нажмите клавишу F5, чтобы продолжить выполнение страницы без остановки в каждой строке. После завершения шагов по выполнению кода в браузере отобразится страница.

Дополнительные сведения о отладчике и об отладке кода в Visual Studio см. в разделе [Пошаговое руководство. Отладка веб-страниц в Visual Web Developer](https://msdn.microsoft.com/library/z9e7w6cs.aspx).

## <a name="using-razor-in-aspnet-mvc-projects-with-visual-studio"></a>Использование Razor в проектах ASP.NET MVC с помощью Visual Studio

Синтаксис Razor также широко используется в проектах ASP.NET MVC. MVC — это мощный и основанный на шаблонах способ создания динамических веб-сайтов. Если веб-сайт веб-страницы ASP.NET трудно обслуживать, его можно преобразовать в приложение ASP.NET MVC. Пример создания приложения MVC см. в разделе [Начало работы with ASP.NET MVC 5](../../../mvc/overview/getting-started/introduction/getting-started.md).

<a id="vs2010support"></a>
## <a name="installing-support-for-aspnet-web-pages-in-visual-studio-2010"></a>Установка поддержки для веб-страницы ASP.NET в Visual Studio 2010

В этом разделе показано, как установить Visual Web Developer Express 2010 и инструменты веб-страницы ASP.NET для Visual Studio.

1. Если у вас еще нет установщика веб-платформы, скачайте его по следующему URL-адресу:

    [https://www.microsoft.com/web/downloads/platform.aspx](https://www.microsoft.com/web/downloads/platform.aspx)
2. Запустите установщик веб-платформы.
3. Перейдите на вкладку **продукты** .

    ![Вкладка "продукты установщика веб – платформы"](program-asp-net-web-pages-in-visual-studio/_static/image10.png)
4. Выполните поиск по запросу **ASP.NET MVC 4** (для веб-страницы ASP.NET 2) и нажмите кнопку **Добавить**. К этим продуктам относятся инструменты Visual Studio для создания веб-сайтов ASP.NET Razor.

    ![Параметры установки установщика платформы](program-asp-net-web-pages-in-visual-studio/_static/image11.png)
5. Нажмите кнопку **установить** , чтобы завершить установку.
