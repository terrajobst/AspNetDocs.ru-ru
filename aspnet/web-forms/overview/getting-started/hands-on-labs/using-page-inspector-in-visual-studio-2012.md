---
uid: web-forms/overview/getting-started/hands-on-labs/using-page-inspector-in-visual-studio-2012
title: Использование инспектора страниц в Visual Studio 2012 | Документация Майкрософт
author: rick-anderson
description: В этой лаборатории вы поймете, новое средство для поиска и устранения проблем веб-страницы в Visual Studio — инспектор страниц. Инспектор страниц-это новое средство b...
ms.author: riande
ms.date: 02/18/2013
ms.assetid: 73232292-a5fe-4720-82a1-8f6553effd1f
msc.legacyurl: /web-forms/overview/getting-started/hands-on-labs/using-page-inspector-in-visual-studio-2012
msc.type: authoredcontent
ms.openlocfilehash: ce654eb5abd54613987f2375cc973febc9dc2ad5
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57041961"
---
<a name="using-page-inspector-in-visual-studio-2012"></a>Использование инспектора страниц в Visual Studio 2012
====================
по [Web Слышатся Team](https://twitter.com/webcamps)

> В этой лаборатории вы поймете, новое средство для поиска и устранения проблем веб-страницы в Visual Studio — инспектор страниц.
> 
> Инспектор страниц — это новое средство, которое переносит средства диагностики браузера в Visual Studio и предоставляет расширенные возможности интеграции между браузером, ASP.NET и исходный код. Он отображает веб-страницы (HTML, Web Forms, ASP.NET MVC или веб-страницы) непосредственно в интегрированной среде разработки Visual Studio и позволяет изучить исходный код и конечного результата. Инспектор страниц позволяет легко разложить веб-сайт, быстро создавать страницы с нуля и быстро диагностировать проблемы.
> 
> В настоящее время у нас есть ряд веб-платформ, которые создают гибкой и масштабируемой веб-сайтов своевременно, такие как ASP.NET MVC и веб-форм. С другой стороны он получает становится все сложнее найти проблемы на страницах, поскольку интегрированная среда разработки не поддерживает представления конструктора в страниц на основе шаблона и динамического содержимого. Таким образом эти веб-сайты нужно открывать в браузере, чтобы увидеть, как они отображаются пользователю.
> 
> Веб-разработчиков, использования внешних инструментов обнаруживать проблемы, которые регулярно запускать в браузере. Затем они вернитесь в интегрированную среду разработки и приступить к устранению. Это и обратно действия между интегрированной среды разработки, браузера и средств профилирования может оказаться неэффективным и иногда требуется новое развертывание и каждый раз, вы хотите воспроизвести проблемную ситуацию очистки кэша.
> 
> Инспектор страниц ликвидирует пробел в веб-разработках между клиентом (средства браузера) и сервером (ASP.NET и исходный код), объединяя лучшее из обеих сторон с использованием комбинированного набора функций.
> 
> Использование инспектора страниц, можно увидеть, какие элементы в исходные файлы (включая код на стороне сервера) создана HTML-разметка для отображения в браузере. Инспектор страниц также позволяет изменять свойства CSS и атрибуты элементов DOM, чтобы увидеть изменения немедленно отражаются в обозревателе.
> 
> Это Практическое занятие будет пошагово функции инспектор страниц и покажем, как их использовать для устранения проблем в веб-приложениях. **Это лабораторное занятие содержит двух упражнениях используется как потоки, но предназначенных для различных технологий. Если вы являетесь разработчиком ASP.NET MVC, выполните упражнение. Если вы являетесь упражнения выполните разработчика веб-форм, два**.
> 
> Это лабораторное занятие поможет усовершенствования и новые возможности, описанные ранее, применяя незначительные изменения в образец веб-приложение, в папке с исходным кодом.
> 
> Все примеры кода и фрагменты кода включены в Web лагеря комплект обучающих материалов, доступных в [ https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409 ](https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409).


<a id="Objectives"></a>

<a id="Objectives"></a>
### <a name="objectives"></a>Цели

В этой практической работу вы узнаете, как:

- Разложить веб-сайта с помощью инспектора страниц
- Проверять и предварительный просмотр изменений стилей CSS в инспекторе страниц
- Обнаружение и устранение неполадок на веб-страницах, использование инспектора страниц

<a id="Prerequisites"></a>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a>Предварительные требования

Необходимо иметь следующие элементы во укомплектовать данную лабораторию:

- [Microsoft Visual Studio Express 2012 для Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) или руководителя (чтение [приложение А](#AppendixA) инструкции по его установке).
- Internet Explorer 9 или более поздней версии

* * *

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a>Упражнения

Это Практическое занятие включает в себя следующие упражнения:

1. [Упражнение 1. Использование инспектора страниц в проекты ASP.NET MVC](#Exercise1)
2. [Упражнение 2. Использование инспектора страниц в проекты веб-форм](#Exercise2)

> [!NOTE]
> Каждого упражнения сопровождается начальный решения, расположенный в папке "Begin" упражнения, чему вы сможете каждого упражнения, независимо от других. В исходном коде для упражнения вы найдете также окончания папку, содержащую решение Visual Studio с кодом, полученный в результате выполнения действий, описанных в соответствующий упражнении. Эти решения можно использовать в качестве руководства, если вам нужна дополнительная помощь, отвечая на это Практическое занятие.


Предполагаемое время для выполнения этого лабораторного: **30 минут**.

<a id="Exercise1"></a>

<a id="Exercise_1_Using_Page_Inspector_in_ASPNET_MVC_Projects"></a>
### <a name="exercise-1-using-page-inspector-in-aspnet-mvc-projects"></a>Упражнение 1. Использование инспектора страниц в проекты ASP.NET MVC

В этом упражнении вы узнаете, как для предварительного просмотра и отладки **ASP.NET MVC 4** решения с помощью **инспектор страниц**. Во-первых выполнит краткое краткая информация о средстве изучить возможности, упрощающие процесс отладки Интернета. После этого будет работать на веб-странице, содержащий ошибки стилей. Вы узнаете, как использовать инспектор страниц для поиска исходного кода, который создает проблему и устранить ее.

<a id="Ex1Task1"></a>

<a id="Task_1_-_Exploring_Page_Inspector"></a>
#### <a name="task-1---exploring-page-inspector"></a>Задача 1 - изучение инспектор страниц

В этой задаче вы узнаете, как использовать инспектор страниц в контексте проекта ASP.NET MVC 4, показывающий Коллекция фотографий.

1. Откройте **начать** решений, расположенный **источника/сервера Ex1-MVC4/начало/** папки.

   1. Необходимо будет загрузить некоторые отсутствующие пакеты NuGet прежде чем продолжить. Чтобы сделать это, нажмите кнопку **проекта** меню и выберите **управление пакетами NuGet**.
   2. В **управление пакетами NuGet** диалоговое окно, нажмите кнопку **восстановить** чтобы скачивать отсутствующие пакеты.
   3. Наконец, постройте решение, нажав кнопку **построения** | **построить решение**.

      > [!NOTE]
      > Одним из преимуществ использования NuGet является отсутствие поставлять все библиотеки в проекте, уменьшив размер проекта. С помощью NuGet Power Tools путем указания версий пакета в файле Packages.config можно для скачивания всех необходимых библиотек при первом запуске проекта. Вот почему необходимо выполните описанные выше действия, после открытия существующего решения из этой лаборатории.
2. В обозревателе решений найдите **Index.cshtml** представления **/Views/Home** папку проекта, щелкните его правой кнопкой мыши и выберите **просмотреть в инспекторе страниц**.

    ![Выбор файла для предварительного просмотра в инспекторе страниц](using-page-inspector-in-visual-studio-2012/_static/image1.png "выбора файла для предварительного просмотра в инспекторе страниц")

    *Выбор файла для предварительного просмотра в инспекторе страниц*
3. Окно инспектора страниц будет отображаться */Home/Index* URL-адрес сопоставлен с источником представления, которые вы выбрали.

    ![ThefirstcontactwithPageInspector](using-page-inspector-in-visual-studio-2012/_static/image2.png)

    *Первого контакта в инспекторе страниц*

    Инспектор страниц средство встроено в среде Visual Studio. Инспектор содержит внедренные браузера, вместе с профилировщику мощный HTML. Обратите внимание, что у вас нет для запуска решения для просмотра страниц.

    > [!NOTE]
    > Если ширина браузера инспектора страниц меньше, чем ширина Открывающаяся страница, не появится страница должным образом. Если это произойдет, настройте ширину нижнего инспектор страниц.
4. Нажмите кнопку **файлы** вкладку в инспекторе страниц.

    Вы увидите все исходные файлы, которые являются составляющими на страницу индекса. Эта функция помогает определить все элементы с первого взгляда, особенно в том случае, если вы работаете с частичными представлениями и шаблонами. Обратите внимание на то, что также можно открыть каждый файл при нажатии кнопки ссылки.

    ![Вкладка файлов](using-page-inspector-in-visual-studio-2012/_static/image3.png)

    *Вкладка "файлы"*
5. Нажмите кнопку **переключиться в режим проверки** кнопки, расположенной в левой части вкладки.

    Это средство позволит вам выбрать какой-либо элемент страницы и увидеть его код HTML и Razor.

    ![Проверки режим кнопки переключателя](using-page-inspector-in-visual-studio-2012/_static/image4.png)

    *Режим инспектирования выключателя.*
6. В браузере инспектора страниц наведите указатель мыши на элементы страницы. Хотя навести указатель мыши на любую часть отображенной странице отображается тип элемента, и соответствующие исходная разметка или код будет выделен в редакторе Visual Studio.

    ![Inspectionmodeinaction](using-page-inspector-in-visual-studio-2012/_static/image5.png)

    *Режим инспектирования в действии*

    > [!NOTE]
    > Нельзя развернуть окно инспектора страниц или вы не сможете см. на вкладке предварительного просмотра, исходным кодом. Если щелкнуть элемент в инспекторе страниц, когда она развернута, исходный код выделения будет отображаться, но он будет скрывать окно инспектора страниц.

    Если вы Обратите внимание на **Index.cshtml** файл, вы заметите, что выделена часть исходного кода, который создает выбранного элемента. Эта функция упрощает редактирование long исходные файлы, предоставляя прямой и быстрый способ доступа к коду.

    ![Inspectingelements](using-page-inspector-in-visual-studio-2012/_static/image6.png)

    *Просмотр элементов*
7. Нажмите кнопку **переключиться в режим проверки** кнопки (![перейдите на вкладку HTML для отображения в браузере инспектора страниц кода HTML.](using-page-inspector-in-visual-studio-2012/_static/image7.png "Перейдите на вкладку HTML для отображения в браузере инспектора страниц кода HTML.") ) для отключения курсор.
8. Выберите **HTML** вкладка для отображения в браузере инспектора страниц HTML-код.
9. В HTML-разметка найдите элемент списка с Koala ссылку и выберите его.

    Обратите внимание на то, что при выборе кода, соответствующие выходные данные автоматически выделяются в обозревателе. Эта функция полезна увидеть, каким образом блок HTML отображается на странице.

    ![Выбор элемента HTML на странице](using-page-inspector-in-visual-studio-2012/_static/image8.png "выбора HTML-элемент на странице")

    *Выбор элемента HTML на странице*
10. Нажмите кнопку **переключиться в режим проверки** кнопку, чтобы включить *режим инспектирования* и нажмите кнопку на панели навигации. В правой части HTML-код, в панели «Стили» вы увидите список со стилями CSS, применен к выбранному элементу.

    > [!NOTE]
    > Поскольку заголовок является частью макета веб-узла, инспектор страниц приведет к открытию \_файла Layout.cshtml и выделения, затронутых сегмент кода.

    ![Discoveringstyles](using-page-inspector-in-visual-studio-2012/_static/image9.png)

    *Обнаружение стили и исходные файлы для выбранного элемента*
11. Наведите указатель мыши синей полосы избранные указатель проверки переключатель включен и выберите команду полукруг.

    ![Выбор элемента](using-page-inspector-in-visual-studio-2012/_static/image10.png "Выбор элемента")

    *Выбор элемента*
12. В панели «Стили» найдите **фоновое изображение** раздел **.main-content** группы. **Снимите флажок** **фоновое изображение** и посмотрите, что получится. Можно заметить, что браузер будет отражать изменения немедленно, и скрыт элемент управления circle.

    > [!NOTE]
    > Изменения, которые применяются на вкладке Стили инспектор страницы не влияют на исходные таблицы стилей. Можно снять флажок стили или изменить их значения столько раз, сколько требуется, но они будут восстановлены после обновления страницы.

    ![Включение и отключение стили CSS](using-page-inspector-in-visual-studio-2012/_static/image11.png "Включение и отключение стилей CSS")

    *Включение и отключение стилей CSS*
13. Теперь щелкните "**ваша эмблема здесь**" текст в заголовке, с помощью режима проверки.
14. В **стили** вкладке, найдите **размер шрифта** CSS атрибут в разделе **.site title** группы. Дважды щелкните значение атрибута и замените значение 2,3 em с **3 em**, а затем нажмите клавишу **ввод**. Обратите внимание на то, что заголовок ищет больше.

    ![Изменение значения CSS в инспекторе страниц](using-page-inspector-in-visual-studio-2012/_static/image12.png "значения изменение CSS в инспекторе страниц")

    *Изменение значений CSS в инспекторе страниц*
15. Нажмите кнопку **Trace Styles** вкладки, расположенной в правой области окна инспектора страниц. Это альтернативный способ увидеть все стили, которые были применены к выделению, упорядоченные по имени атрибута.

    ![CSSstylestracing](using-page-inspector-in-visual-studio-2012/_static/image13.png)

    *Трассировка стилей CSS выбранного элемента*
16. Другой особенностью инспектор страниц — панель макета. Используя режим инспектирования, выберите на панели навигации и нажмите кнопку **макета** вкладку на правой панели. Вы увидите точный размер выбранного элемента, а также размер его смещение, поля, заполнения и границы. Обратите внимание на то, что можно также изменить значения из этого представления.

    ![Макет элемента в инспекторе страниц](using-page-inspector-in-visual-studio-2012/_static/image14.png "макет элемента в инспекторе страниц")

    *Макет элемента в инспекторе страниц*

<a id="Ex1Task2"></a>

<a id="Task_2_-_Finding_and_Fixing_Style_Issues_in_the_Photo_Gallery"></a>
#### <a name="task-2---finding-and-fixing-style-issues-in-the-photo-gallery"></a>Задача 2 - поиск и устранение проблем в галерею изображений

Как диагностировать проблемы веб-страниц с предыдущими версиями Visual Studio? Вы, вероятно, знакомы с веб-средств, выполняемых вне Visual Studio IDE, такие как средства разработчика Internet Explorer или Firebug для отладки. Браузеры только понимать HTML, сценарии и стили, а основная структура создают HTML-код, который будет отрисовываться. По этой причине часто требуется развернуть весь сайт, чтобы посмотреть как веб-страниц.

Возможно, выполнили такие шаги, если требуется обнаруживать и исправлять проблемы в веб-сайт:

1. Запустите решение из Visual Studio или развернуть страницу на веб-сервере.
2. В браузере откройте средства разработчика использовать, или просто открыть исходный код и стили и пытаться найти совпадения для проблемы. Чтобы найти связанные файлы, то нужно использовать &quot;поиска&quot; или &quot;поиска в файлах&quot; функции с именем стилей классов.
3. После обнаружения ошибки, остановите веб-браузер и сервером.
4. Очистите кэш браузера.
5. Вернитесь в Visual Studio, чтобы применить исправление. Повторите все шаги для проверки.

Как в ASP.NET MVC 4 не реальные WYSIWYG, большинство проблем стиля обнаруживаются на более позднем этапе после запуска или развертывание веб-приложения. Теперь с помощью инспектора страниц, можно просматривать любые страницы без запуска решения.

В этой задаче будет использоваться инспектор страниц и исправить приложение Photo Gallery некоторые проблемы.

1. Использование инспектора страниц, найдите **зарегистрировать** и **вход** ссылки в левой части заголовка.

    Обратите внимание на то, что ссылки не отображаются в ожидаемом месте справа, и они отображаются как маркированный список. Теперь будет выровнять ссылки справа и изменение стиля их соответствующим образом.

    ![Поиск регистра и журналов в ссылки](using-page-inspector-in-visual-studio-2012/_static/image15.png "поиск регистра и журналов в ссылки")

    *Поиск регистра и журналов в ссылки*
2. С выбранным режимом проверки переключателя щелкните ближе к, но не на Register ссылку, чтобы открыть ее код.

    Обратите внимание, что исходный код из ссылок находится в  **\_LoginPartial.cshtml** файл, не Index.cshtml ни \_Layout.cshtml, который местах, можно найти в первую очередь. Вы были размещены непосредственно в файле правильного источника.
3. В **стили** найдите и щелкните **<section> #login</section>** элемента, который является контейнером HTML для этих ссылок.

    Обратите внимание, что **#login** стиль автоматически размещается в **Site.css** после нажатия кнопки. Кроме того код теперь выделено.

    ![Выбрав стили CSS](using-page-inspector-in-visual-studio-2012/_static/image16.png "выбора стилей CSS")

    *Выбрав стили CSS*
4. Раскомментируйте **text-align** атрибут в выделенном коде, удалив открывающих и закрывающих символов и сохраните **Site.css** файл.

    Инспектор страниц известно о любых файлов, составляющих текущую страницу, и он может определить при изменении любого из этих файлов. Он оповещает пользователя каждый раз, когда текущей страницы в браузере не синхронизирована с исходными файлами.
5. В браузере инспектора страниц щелкните полосу, расположенные в адресной строке, чтобы перезагрузить страницу.

    ![Перезагрузить страницу](using-page-inspector-in-visual-studio-2012/_static/image17.png)

    *Перезагрузить страницу*

    Ссылки, теперь находятся в правом, но они все еще выглядят как маркированный список. Теперь будет удалить маркеры и выровнять по ссылкам горизонтально.

    ![Обновленная страница](using-page-inspector-in-visual-studio-2012/_static/image18.png)

    *Обновленная страница*
6. Используя режим проверки, выберите любой из **&lt;li&gt;** элементы, содержащие &quot;зарегистрировать&quot; и &quot;вход&quot; ссылки. Щелкните  **&lt;разделе&gt; #login** элемент для доступа к **Styles.css** кода.

    ![Поиск стиля](using-page-inspector-in-visual-studio-2012/_static/image19.png "поиск стиля")

    *Поиск стиля*
7. В **Style.css**, раскомментируйте код для **#login li** элементов. Стиль, который вы добавляете будет скрыть маркера и отображать элементы по горизонтали.

    ![Изменение стиля ссылки входа](using-page-inspector-in-visual-studio-2012/_static/image20.png "изменение стиля ссылки входа")

    *Изменение стиля ссылки входа*
8. Сохранить **Style.css** файл и щелкните один раз на панели, расположенной ниже адреса, чтобы перезагрузить страницу. Обратите внимание на то, что ссылки отображаются правильно.

    ![Ссылки, выровненный по правой стороне](using-page-inspector-in-visual-studio-2012/_static/image21.png "ссылки, выровненный по правой стороне")

    *Ссылки, выровненный по правой стороне*
9. Наконец мы изменим заголовок. Режим проверки щелкните **ваша эмблема здесь** текста и get в исходный код, который создает его.
10. Теперь вы находитесь в  **\_Layout.cshtml**, замените "**ваша эмблема здесь**'текст с'**Photo Gallery**". Сохранить и обновить браузера инспектора страниц.

    ![Назначение новый заголовок](using-page-inspector-in-visual-studio-2012/_static/image22.png "назначение новый заголовок")

    *Назначение новый заголовок*

    ![PhotoGallerypage](using-page-inspector-in-visual-studio-2012/_static/image23.png)

    *Обновить страницу Photo Gallery*
11. Наконец, все **PhotoGallery** проекта и нажмите клавишу **F5** для запуска приложения. Извлечь все, что изменения работают должным образом.

* * *

<a id="Exercise2"></a>

<a id="Exercise_2_Using_Page_Inspector_in_WebForms_Projects"></a>
### <a name="exercise-2-using-page-inspector-in-webforms-projects"></a>Упражнение 2. Использование инспектора страниц в проекты веб-форм

В этом упражнении вы узнаете, как для предварительного просмотра и отладки решения веб-форм, использование инспектора страниц. Сначала будет выполнять краткое краткая информация о средстве изучить возможности инспектор страниц, которые облегчают процесс отладки Интернета. После этого будет работать на веб-странице, содержащий ошибки стилей. Вы узнаете, как использовать инспектор страниц для поиска исходного кода, который создает проблему и устранить ее.

<a id="Ex2Task1"></a>

<a id="Task_1_-_Exploring_Page_Inspector"></a>
#### <a name="task-1---exploring-page-inspector"></a>Задача 1 - изучение инспектор страниц

В этой задаче вы узнаете, как использовать функции инспектора страниц в контексте проекта веб-форм, который показывает коллекцию фотографий.

1. Откройте **начать** решений, расположенный **источника/Ex2-веб-форм иначало/** папки.

   1. Необходимо будет загрузить некоторые отсутствующие пакеты NuGet прежде чем продолжить. Чтобы сделать это, нажмите кнопку **проекта** меню и выберите **управление пакетами NuGet**.
   2. В **управление пакетами NuGet** диалоговое окно, нажмите кнопку **восстановить** чтобы скачивать отсутствующие пакеты.
   3. Наконец, постройте решение, нажав кнопку **построения** | **построить решение**.

      > [!NOTE]
      > Одним из преимуществ использования NuGet является отсутствие поставлять все библиотеки в проекте, уменьшив размер проекта. С помощью NuGet Power Tools путем указания версий пакета в файле Packages.config можно для скачивания всех необходимых библиотек при первом запуске проекта. Вот почему необходимо выполните описанные выше действия, после открытия существующего решения из этой лаборатории.
2. В обозревателе решений найдите **Default.aspx** странице, щелкните его правой кнопкой мыши и выберите **просмотреть в инспекторе страниц**.

    ![Default.aspx открывается в инспекторе страниц](using-page-inspector-in-visual-studio-2012/_static/image24.png "Default.aspx открывается в инспекторе страниц")

    *Открытие Default.aspx в инспекторе страниц*
3. Окно инспектора страниц будет показана страница Default.aspx.

    ![Просмотр в инспекторе страниц Default.aspx](using-page-inspector-in-visual-studio-2012/_static/image25.png "Просмотр Default.aspx в инспекторе страниц")

    *Просмотр Default.aspx в инспекторе страниц*

    Инспектор страниц средство встроено в среде Visual Studio. Инспектор содержит внедренные браузера, а также мощные профилировщик HTML, отображающий выбранный код. Обратите внимание, что у вас нет для запуска решения для просмотра страниц.

    > [!NOTE]
    > Если ширина браузера инспектора страниц меньше, чем ширина Открывающаяся страница, не появится страница должным образом. Если это произойдет, настройте ширину нижнего инспектор страниц.
4. Нажмите кнопку **файлы** вкладку в инспекторе страниц.

    Вы увидите все исходные файлы, которые являются составляющими отображаемой страницы по умолчанию. Это полезная функция для определения всех элементов, вы можете быстро, особенно в том случае, если вы работаете с пользовательские элементы управления и главные страницы. Обратите внимание, что можно также перейти к каждому из файлов.

    ![Вкладка "файлы"](using-page-inspector-in-visual-studio-2012/_static/image26.png "вкладка \"файлы\"")

    *Вкладка "файлы"*
5. Нажмите кнопку **переключиться в режим проверки** кнопки, расположенной в левой части вкладки.

    Это средство позволит вам выбрать любой элемент страницы и ознакомьтесь с его исходного кода и .aspx HTML.

    ![Режим инспектирования выключатель](using-page-inspector-in-visual-studio-2012/_static/image27.png "кнопку переключиться в режим проверки")

    *Режим инспектирования выключателя.*
6. В браузере инспектора страниц наведите указатель мыши элементы страницы. Хотя навести указатель мыши на любую часть отображенной странице отображается тип элемента, и соответствующие исходная разметка или код будет выделен в редакторе Visual Studio.

    ![Режим инспектирования в действии](using-page-inspector-in-visual-studio-2012/_static/image28.png "режим инспектирования в действии")

    *Режим инспектирования в действии*

    > [!NOTE]
    > Нельзя развернуть окно инспектора страниц или вы не сможете см. на вкладке предварительного просмотра, исходным кодом. Если щелкнуть элемент в инспекторе страниц, когда она развернута, исходный код выделения будет отображаться, но он будет скрывать окно инспектора страниц.

    Если вы Обратите внимание на **Default.aspx** файл, вы заметите, что выделена часть исходного кода, который создает выбранного элемента. Эта функция облегчает выпуск long исходные файлы, предоставляя прямой и быстрый способ доступа к коду.

    ![Просмотр элементов](using-page-inspector-in-visual-studio-2012/_static/image29.png "проверки элементов")

    *Просмотр элементов*
7. Нажмите кнопку **переключиться в режим проверки** кнопки (![Select-the-HTML-tab-to-display-the-HTML-code-rendered-in-the-Page-Inspector-browser.](using-page-inspector-in-visual-studio-2012/_static/image30.png "Select-the-HTML-tab-to-display-the-HTML-code-rendered-in-the-Page-Inspector-browser.") ), расположенный в инспектор страниц вкладок, чтобы отключить курсор.
8. Выберите **HTML** вкладка для отображения в браузере инспектора страниц HTML-код.
9. В коде HTML найдите элемент списка с Koala ссылку и выберите его.

    Обратите внимание, что при выборе кода, соответствующие выходные данные автоматически выделенный браузера. Эта функция полезна увидеть, каким образом блок HTML отображается на странице.

    ![Выбор элемента HTML на странице](using-page-inspector-in-visual-studio-2012/_static/image31.png "Выбор элемента HTML на странице")

    *Выбор элемента HTML на странице*
10. Нажмите кнопку **переключиться в режим проверки** кнопку, чтобы включить *режим инспектирования* и нажмите кнопку на панели навигации. В правой части HTML-код, в панели «Стили» вы увидите список со стилями CSS, применен к выбранному элементу.

    > [!NOTE]
    > Поскольку заголовок является частью макета веб-узла, инспектор страниц также откройте файл Site.Master и выделять фрагмент кода, которые затронуты.

    ![DiscoveringstylesWebForms](using-page-inspector-in-visual-studio-2012/_static/image32.png "обнаружения стили и исходные файлы для выбранного элемента")

    *Обнаружение стили и исходные файлы для выбранного элемента*
11. Переключить проверки указатель включена наведите указатель мыши под строкой меню и выберите команду пустое полукруг.

    ![Выбор элемента](using-page-inspector-in-visual-studio-2012/_static/image33.png "Выбор элемента")

    *Выбор элемента*
12. В панели «Стили» найдите **фоновое изображение** раздел **.main-content** группы. **Снимите флажок** **фоновое изображение** и посмотрите, что получится. Можно заметить, что браузер будет отражать изменения немедленно, и скрыт элемент управления circle.

    > [!NOTE]
    > Изменения, которые применяются на вкладке Стили инспектор страницы не влияют на исходные таблицы стилей. Можно снять флажок стили или изменить их значения столько раз, сколько требуется, но они будут восстановлены после обновления страницы.

    ![Включение и отключение CSS styles2](using-page-inspector-in-visual-studio-2012/_static/image34.png "Включение и отключение стилей CSS")

    *Включение и отключение стилей CSS*
13. Теперь щелкните "**вашей** **эмблема здесь"** текст в заголовке, с помощью режима проверки.
14. В **стили** вкладке, найдите **размер шрифта** CSS атрибут в разделе **.site title** группы. Дважды щелкните атрибут один раз, чтобы изменить его значение. Замените 2.3em значение с **3em**, и нажмите клавишу ВВОД. Обратите внимание на то, что заголовок ищет больше.

    ![Изменение значения CSS в странице Inspector2](using-page-inspector-in-visual-studio-2012/_static/image35.png "значения изменение CSS в инспекторе страниц")

    *Изменение значений CSS в инспекторе страниц*
15. Нажмите кнопку **Trace Styles** вкладки, расположенной в правой области окна инспектора страниц. Это альтернативный способ увидеть все стили, которые были применены к выделению, упорядоченные по имени атрибута.

    ![Трассировка стилей CSS выбранного элемента](using-page-inspector-in-visual-studio-2012/_static/image36.png "трассировка стилей CSS выбранного элемента")

    *Трассировка стилей CSS выбранного элемента*
16. Другой особенностью инспектор страниц — панель макета. Используя режим инспектирования, выберите на панели навигации и нажмите кнопку **макета** вкладку на правой панели. Вы увидите точный размер выбранного элемента, а также размер его смещение, поля, заполнения и границы. Обратите внимание на то, что можно также изменить значения из этого представления.

    ![Макет элемента в инспекторе страниц](using-page-inspector-in-visual-studio-2012/_static/image37.png "макет элемента в инспекторе страниц")

    *Макет элемента в инспекторе страниц*

<a id="Ex2Task2"></a>

<a id="Task_2_-_Finding_and_Fixing_Style_Issues_in_the_Photo_Gallery"></a>
#### <a name="task-2---finding-and-fixing-style-issues-in-the-photo-gallery"></a>Задача 2 - поиск и устранение проблем в галерею изображений

Как диагностировать проблемы веб-страниц с предыдущими версиями Visual Studio? Вы, вероятно, знакомы с веб-средств, выполняемых вне Visual Studio IDE, такие как средства разработчика Internet Explorer или Firebug для отладки. Браузеры только понимать HTML, сценарии и стили, а основная структура создают HTML-код, который будет отрисовываться. По этой причине часто требуется развернуть весь сайт, чтобы посмотреть как веб-страниц.

Возможно, выполнили такие шаги, если требуется обнаруживать и исправлять проблемы в веб-сайт:

1. Запустите решение из Visual Studio или развернуть страницу на веб-сервере.
2. В браузере откройте средства разработчика использовать, или просто открыть исходный код и стили и пытаться найти совпадения для проблемы. Чтобы найти связанные файлы, то нужно использовать &quot;поиска&quot; или &quot;поиска в файлах&quot; функции с именем стилей классов.
3. После обнаружения ошибки, остановите веб-браузер и сервером.
4. Очистите кэш браузера.
5. Вернитесь в Visual Studio, чтобы применить исправление. Повторите все шаги для проверки.

Так как не реальные WYSIWYG, в веб-форм ASP.NET, некоторые проблемы стиля обнаруживаются на более позднем этапе после запуска или развертывания. Теперь с помощью инспектора страниц, можно просматривать любые страницы без запуска решения.

В этой задаче будет использоваться для устранения некоторых проблем приложение фотоальбома для инспектора страниц. В следующих шагах вы обнаружит и быстро устранить некоторые проблемы простых стилей в заголовке.

1. С помощью проверки страницы найдите **зарегистрировать** и **вход** ссылки в левой части заголовка.

    Обратите внимание на то, что ссылка не отображается в ожидаемом месте в правой части. Теперь будет выровнять ссылку справа и изменение стиля соответствующим образом.

    ![Войдите в ссылке, расположенный в левой части](using-page-inspector-in-visual-studio-2012/_static/image38.png "войдите в ссылке, расположенный в левой части")

    *Ссылка вход в систему, расположенный в левой части*
2. С выбранным режимом проверки переключателя выберите ссылку вход в систему, чтобы открыть ее код.

    Обратите внимание, что ссылка исходный код находится в **Site.Master** файл, не на странице Default.aspx, который является местом, может выглядеть в первую очередь; вы были размещены непосредственно в файле правильного источника.
3. В **стили** найдите и щелкните  **&lt;разделе&gt; #login** элемента, который является контейнером HTML для этих ссылок.

    Обратите внимание, что **#login** стиль автоматически размещается в **Site.css** после нажатия кнопки. Кроме того код теперь выделено.

    ![Выбрав стили CSS](using-page-inspector-in-visual-studio-2012/_static/image39.png "выбора стилей CSS")

    *Выбрав стили CSS*
4. Раскомментируйте **text-align** атрибут в выделенном коде, удалив открывающих и закрывающих символов и сохраните **Site.css** файл.

    Инспектор страниц известно о любых файлов, составляющих текущую страницу, и он может определить при изменении любого из этих файлов. Он оповещает пользователя каждый раз, когда текущей страницы в браузере не синхронизирована с исходными файлами.
5. В браузере инспектора страниц щелкните полосу, расположенные в адресной строке, чтобы сохранить изменения и обновите страницу.

    ![Reloadingthepage](using-page-inspector-in-visual-studio-2012/_static/image40.png)

    *Перезагрузить страницу*

    Ссылки, теперь находятся в правом, но они все еще выглядят как маркированный список. Теперь будет удалить маркеры и выровнять по ссылкам горизонтально.

    ![Обновленная страница](using-page-inspector-in-visual-studio-2012/_static/image41.png)

    *Обновленная страница*
6. Используя режим проверки, выберите любой из **&lt;li&gt;** элементы, содержащие &quot;зарегистрировать&quot; и &quot;вход&quot; ссылки. Щелкните  **&lt;разделе&gt; #login** элемент для доступа к **Styles.css** кода.

    ![Поиск стиля](using-page-inspector-in-visual-studio-2012/_static/image42.png "поиск стиля")

    *Поиск стиля*
7. В **Style.css**, раскомментируйте код для **#login li** элементов. Стиль, который вы добавляете будет скрыть маркера и отображать элементы по горизонтали.

    ![Изменение стиля ссылки входа](using-page-inspector-in-visual-studio-2012/_static/image43.png "изменение стиля ссылки входа")

    *Изменение стиля ссылки входа*
8. Сохранить **Style.css** файл и щелкните один раз на панели, расположенной ниже адреса, чтобы перезагрузить страницу. Обратите внимание на то, что ссылки отображаются правильно.

    ![Ссылки, выровненный по правой стороне](using-page-inspector-in-visual-studio-2012/_static/image44.png "ссылки, выровненный по правой стороне")

    *Ссылки, выровненный по правой стороне*
9. Наконец мы изменим заголовок. Вместо поиска для "**ваша эмблема здесь"** текста во всех файлах, используйте режим инспектирования щелкните текст и получить исходный код, который создает его.

    ![Поиск название узла](using-page-inspector-in-visual-studio-2012/_static/image45.png "поиск заголовок сайта")

    *Поиск заголовок сайта*
10. Теперь вы находитесь в **Site.Master**, замените "**ваша эмблема здесь**'текст с'**Photo Gallery**". Сохранить и обновить браузера инспектора страниц.

    ![Обновить страницу Photo Gallery](using-page-inspector-in-visual-studio-2012/_static/image46.png "странице Photo Gallery")

    *Обновить страницу Photo Gallery*
11. Наконец, щелкните **F5** для запуска приложения извлечения все изменения работают должным образом.

* * *

<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a>Сводка

Выполнив этот практический семинар, выученных, как использовать инспектор страниц для предварительного просмотра веб-приложения без необходимости заново собрать и запустить веб-сайт в браузере. Кроме того как быстро находить и исправлять ошибки, обратившись к непосредственно из выводимые данные к исходному коду выученных.

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a>Приложение а. Установка Visual Studio Express 2012 для Web

Вы можете установить **Microsoft Visual Studio Express 2012 для Web** или другой &quot;Express&quot; версию с помощью **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)**. Приведенные ниже инструкции описывают действия, необходимые для установки *Visual studio Express 2012 для Web* с помощью *Microsoft Web Platform Installer*.

1. Перейдите к [ [ https://go.microsoft.com/?linkid=9810169 ](https://go.microsoft.com/?linkid=9810169) ](https://go.microsoft.com/?linkid=9810169). Кроме того, если вы уже установили установщика веб-платформы, можно открыть его и выполните поиск продукта &quot; <em>Visual Studio Express 2012 для Web с пакетом Windows Azure SDK</em>&quot;.
2. Щелкните **установить сейчас**. Если у вас нет **установщика веб-платформы** вы будете перенаправлены к сначала загрузить и установить его.
3. Один раз **установщика веб-платформы** открыт, нажмите кнопку **установить** для запуска программы установки.

    ![Установка Visual Studio Express](using-page-inspector-in-visual-studio-2012/_static/image47.png "установка Visual Studio Express")

    *Установка Visual Studio Express*
4. Прочтите лицензии и условия все продукты и нажмите кнопку **я принимаю** для продолжения.

    ![Принятие условий лицензии](using-page-inspector-in-visual-studio-2012/_static/image48.png)

    *Принятие условий лицензии*
5. Подождите, пока не завершится процесс загрузки и установки.

    ![Ход установки](using-page-inspector-in-visual-studio-2012/_static/image49.png)

    *Ход выполнения установки*
6. После завершения установки нажмите кнопку **Готово**.

    ![Установка завершена](using-page-inspector-in-visual-studio-2012/_static/image50.png)

    *Установка завершена*
7. Нажмите кнопку **выхода** закрыть установщик веб-платформы.
8. Чтобы открыть Visual Studio Express для Web, перейдите к **запустить** экрана и Займитесь написанием &quot; **VS Express**&quot;, нажмите кнопку на **VS Express для Web** Плитка.

    ![VS Express для Web плитки](using-page-inspector-in-visual-studio-2012/_static/image51.png)

    *VS Express для Web плитки*