---
title: Меньше, Sass и Font Awesome в ASP.NET Core
author: ardalis
description: Узнайте, как использовать меньше, Sass и Font Awesome в приложениях ASP.NET Core.
ms.author: tdykstra
ms.date: 10/14/2016
uid: client-side/less-sass-fa
ms.openlocfilehash: 2229c4e3b0238ff17c15e78f657b9acb10495c72
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57065561"
---
# <a name="less-sass-and-font-awesome-in-aspnet-core"></a><span data-ttu-id="5d24c-103">Меньше, Sass и Font Awesome в ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="5d24c-103">Less, Sass, and Font Awesome in ASP.NET Core</span></span>

<span data-ttu-id="5d24c-104">Автор: [Стив Смит](https://ardalis.com/) (Steve Smith)</span><span class="sxs-lookup"><span data-stu-id="5d24c-104">By [Steve Smith](https://ardalis.com/)</span></span>

<span data-ttu-id="5d24c-105">Пользователи веб-приложений имеют более высокий уровень ожиданий, когда дело доходит до применения стиля и в целом столкнуться.</span><span class="sxs-lookup"><span data-stu-id="5d24c-105">Users of web applications have increasingly high expectations when it comes to style and overall experience.</span></span> <span data-ttu-id="5d24c-106">Современные веб-приложения часто используют большой набор средств и платформ для определения и управления их внешний вид согласованным способом.</span><span class="sxs-lookup"><span data-stu-id="5d24c-106">Modern web applications frequently leverage rich tools and frameworks for defining and managing their look and feel in a consistent manner.</span></span> <span data-ttu-id="5d24c-107">Платформы, такие как [Bootstrap](http://getbootstrap.com/) может сыграть относительно определения общего набора стили и параметры макета для веб-сайтов.</span><span class="sxs-lookup"><span data-stu-id="5d24c-107">Frameworks like [Bootstrap](http://getbootstrap.com/) can go a long way toward defining a common set of styles and layout options for web sites.</span></span> <span data-ttu-id="5d24c-108">Однако большинство сайтов нетривиальные также преимущества возможность эффективно определять и поддерживать стили и каскадные таблицы стилей (CSS), а также простой доступ к не изображения значков, которые сделают более интуитивно понятный интерфейс веб-узла.</span><span class="sxs-lookup"><span data-stu-id="5d24c-108">However, most non-trivial sites also benefit from being able to effectively define and maintain styles and cascading style sheet (CSS) files, as well as having easy access to non-image icons that help make the site's interface more intuitive.</span></span> <span data-ttu-id="5d24c-109">Именно здесь языки и инструменты, которые поддерживают [меньше](http://lesscss.org/) и [Sass](http://sass-lang.com/), и библиотеки, например [Font Awesome](http://fontawesome.io/), бывают.</span><span class="sxs-lookup"><span data-stu-id="5d24c-109">That's where languages and tools that support [Less](http://lesscss.org/) and [Sass](http://sass-lang.com/), and libraries like [Font Awesome](http://fontawesome.io/), come in.</span></span>

## <a name="css-preprocessor-languages"></a><span data-ttu-id="5d24c-110">Языки препроцессора CSS</span><span class="sxs-lookup"><span data-stu-id="5d24c-110">CSS preprocessor languages</span></span>

<span data-ttu-id="5d24c-111">Языки, которые компилируются в других языках, чтобы улучшить возможности работы с базовый язык, называются препроцессорами.</span><span class="sxs-lookup"><span data-stu-id="5d24c-111">Languages that are compiled into other languages, in order to improve the experience of working with the underlying language, are referred to as preprocessors.</span></span> <span data-ttu-id="5d24c-112">Существует два популярных препроцессорами для CSS: Менее и Sass.</span><span class="sxs-lookup"><span data-stu-id="5d24c-112">There are two popular preprocessors for CSS: Less and Sass.</span></span>  <span data-ttu-id="5d24c-113">Эти препроцессорами Добавление компонентов к CSS, например поддержка переменных и вложенные правила, которые для более удобного обслуживания больших и сложных таблиц стилей.</span><span class="sxs-lookup"><span data-stu-id="5d24c-113">These preprocessors add features to CSS, such as support for variables and nested rules, which improve the maintainability of large, complex stylesheets.</span></span> <span data-ttu-id="5d24c-114">CSS, как язык является очень простым, отсутствует поддержка даже такой простой, как переменные, и как правило, это сделать файлы CSS, повторяющихся и перегруженными.</span><span class="sxs-lookup"><span data-stu-id="5d24c-114">CSS as a language is very basic, lacking support even for something as simple as variables, and this tends to make CSS files repetitive and bloated.</span></span> <span data-ttu-id="5d24c-115">Добавление реальных языковых функций через препроцессорами может помочь сократить дублирование и обеспечить улучшенную организацию правил стилей.</span><span class="sxs-lookup"><span data-stu-id="5d24c-115">Adding real programming language features via preprocessors can help reduce duplication and provide better organization of styling rules.</span></span> <span data-ttu-id="5d24c-116">Visual Studio предоставляет встроенную поддержку обоих Less и Sass, а также расширения, которые можно улучшить процесс разработки, при работе с этими языками.</span><span class="sxs-lookup"><span data-stu-id="5d24c-116">Visual Studio provides built-in support for both Less and Sass, as well as extensions that can further improve the development experience when working with these languages.</span></span>

<span data-ttu-id="5d24c-117">Рассмотрим краткий пример как препроцессорами повышает удобочитаемость и обслуживаемость информации о стилях CSS:</span><span class="sxs-lookup"><span data-stu-id="5d24c-117">As a quick example of how preprocessors can improve readability and maintainability of style information, consider this CSS:</span></span>

```css
.header {
    color: black;
    font-weight: bold;
    font-size: 18px;
    font-family: Helvetica, Arial, sans-serif;
}

.small-header {
    color: black;
    font-weight: bold;
    font-size: 14px;
    font-family: Helvetica, Arial, sans-serif;
}
```

<span data-ttu-id="5d24c-118">С помощью меньше, это можно переписать, чтобы избавиться от дублирования, с помощью *примеси* (с разделителями «mix» позволяет свойства из одного класса или набор правил в другой):</span><span class="sxs-lookup"><span data-stu-id="5d24c-118">Using Less, this can be rewritten to eliminate all of the duplication, using a *mixin* (so named because it allows you to "mix in" properties from one class or rule-set into another):</span></span>

```less
.header {
    color: black;
    font-weight: bold;
    font-size: 18px;
    font-family: Helvetica, Arial, sans-serif;
}

.small-header {
    .header;
    font-size: 14px;
}
```

## <a name="less"></a><span data-ttu-id="5d24c-119">меньше</span><span class="sxs-lookup"><span data-stu-id="5d24c-119">Less</span></span>

<span data-ttu-id="5d24c-120">CSS менее препроцессора выполняется с помощью Node.js.</span><span class="sxs-lookup"><span data-stu-id="5d24c-120">The Less CSS preprocessor runs using Node.js.</span></span> <span data-ttu-id="5d24c-121">Чтобы установить, меньше, используйте диспетчер пакетов Node (npm) из командной строки (-g означает «глобальные»):</span><span class="sxs-lookup"><span data-stu-id="5d24c-121">To install Less, use Node Package Manager (npm) from a command prompt (-g means "global"):</span></span>

```console
npm install -g less
```

<span data-ttu-id="5d24c-122">Если вы используете Visual Studio, вы можете начать работу с меньшими усилиями, добавив один или несколько меньше файлов в проект, а затем настроив Gulp или Grunt для обрабатывать их во время компиляции.</span><span class="sxs-lookup"><span data-stu-id="5d24c-122">If you're using Visual Studio, you can get started with Less by adding one or more Less files to your project, and then configuring Gulp (or Grunt) to process them at compile-time.</span></span> <span data-ttu-id="5d24c-123">Добавить *стили* папки в проект, а затем добавьте новый файл с именем Less *main.less* в эту папку.</span><span class="sxs-lookup"><span data-stu-id="5d24c-123">Add a *Styles* folder to your project, and then add a new Less file named *main.less* to this folder.</span></span>

![Добавьте файл less](less-sass-fa/_static/add-less-file.png)

<span data-ttu-id="5d24c-125">После добавления структуры папок должна выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="5d24c-125">Once added, your folder structure should look something like this:</span></span>

![Структура папок](less-sass-fa/_static/folder-structure.png)

<span data-ttu-id="5d24c-127">Теперь можно добавить некоторые основные стили в файл, который будет скомпилирован в CSS и развернут в папку wwwroot, Gulp.</span><span class="sxs-lookup"><span data-stu-id="5d24c-127">Now you can add some basic styling to the file, which will be compiled into CSS and deployed to the wwwroot folder by Gulp.</span></span>

<span data-ttu-id="5d24c-128">Изменить *main.less* для включения следующим содержимым, который создает простой цветовой палитрой из одного основного цвета.</span><span class="sxs-lookup"><span data-stu-id="5d24c-128">Modify *main.less* to include the following content, which creates a simple color palette from a single base color.</span></span>

```less
@base: #663333;
@background: spin(@base, 180);
@lighter: lighten(spin(@base, 5), 10%);
@lighter2: lighten(spin(@base, 10), 20%);
@darker: darken(spin(@base, -5), 10%);
@darker2: darken(spin(@base, -10), 20%);

body {
    background-color:@background;
}
.baseColor  {color:@base}
.bgLight    {color:@lighter}
.bgLight2   {color:@lighter2}
.bgDark     {color:@darker}
.bgDark2    {color:@darker2}
```

<span data-ttu-id="5d24c-129">`@base` а другой @-prefixed элементы являются переменными.</span><span class="sxs-lookup"><span data-stu-id="5d24c-129">`@base` and the other @-prefixed items are variables.</span></span> <span data-ttu-id="5d24c-130">Каждый из них представляет цвет.</span><span class="sxs-lookup"><span data-stu-id="5d24c-130">Each of them represents a color.</span></span> <span data-ttu-id="5d24c-131">За исключением `@base`, их можно установить с помощью функции цвета: Осветление, который затемняется и запустить.</span><span class="sxs-lookup"><span data-stu-id="5d24c-131">Except for `@base`, they're set using color functions: lighten, darken, and spin.</span></span> <span data-ttu-id="5d24c-132">Осветление и который затемняется делать практически что вы ожидаете; Счетчик корректирует цветового тона цвета на число градусов (около цветовой круг).</span><span class="sxs-lookup"><span data-stu-id="5d24c-132">Lighten and darken do pretty much what you would expect; spin adjusts the hue of a color by a number of degrees (around the color wheel).</span></span> <span data-ttu-id="5d24c-133">Меньше процессор может игнорировать переменные, которые не используются, чтобы продемонстрировать, как работают эти переменные, нам нужно где-нибудь их использовать.</span><span class="sxs-lookup"><span data-stu-id="5d24c-133">The Less processor is smart enough to ignore variables that aren't used, so to demonstrate how these variables work, we need to use them somewhere.</span></span> <span data-ttu-id="5d24c-134">Классы `.baseColor`, и т.д. мы рассмотрим вычисляемые значения всех переменных в CSS-файл, который создается.</span><span class="sxs-lookup"><span data-stu-id="5d24c-134">The classes `.baseColor`, etc. will demonstrate the calculated values of each of the variables in the CSS file that's produced.</span></span>

### <a name="get-started"></a><span data-ttu-id="5d24c-135">Начало работы</span><span class="sxs-lookup"><span data-stu-id="5d24c-135">Get started</span></span>

<span data-ttu-id="5d24c-136">Создание **файл конфигурации npm** (*package.json*) в папке проекта и изменить его, чтобы ссылаться на `gulp` и `gulp-less`:</span><span class="sxs-lookup"><span data-stu-id="5d24c-136">Create an **npm Configuration File** (*package.json*) in your project folder and edit it to reference `gulp` and `gulp-less`:</span></span>

```json
{
  "version": "1.0.0",
  "name": "asp.net",
  "private": true,
  "devDependencies": {
    "gulp": "3.9.1",
    "gulp-less": "3.3.0"
  }
}
```

<span data-ttu-id="5d24c-137">Установка зависимостей, либо в командной строке в папке проекта или в Visual Studio **обозревателе решений** (**зависимости > npm > восстановление пакетов**).</span><span class="sxs-lookup"><span data-stu-id="5d24c-137">Install the dependencies either at a command prompt in your project folder, or in Visual Studio **Solution Explorer** (**Dependencies > npm > Restore packages**).</span></span>

```console
npm install
```

![VS восстановление пакетов](less-sass-fa/_static/restore-packages.png)

<span data-ttu-id="5d24c-139">В папке проекта создайте **файл конфигурации Gulp** (*gulpfile.js*) для определения автоматизированного процесса.</span><span class="sxs-lookup"><span data-stu-id="5d24c-139">In the project folder, create a **Gulp Configuration File** (*gulpfile.js*) to define the automated process.</span></span>  <span data-ttu-id="5d24c-140">Добавьте переменную в верхней части файла для представления меньше и меньше выполнение задачи:</span><span class="sxs-lookup"><span data-stu-id="5d24c-140">Add a variable at the top of the file to represent Less, and a task to run Less:</span></span>

```javascript
var gulp = require("gulp"),
  fs = require("fs"),
  less = require("gulp-less");

gulp.task("less", function () {
  return gulp.src('Styles/main.less')
    .pipe(less())
    .pipe(gulp.dest('wwwroot/css'));
});
```

<span data-ttu-id="5d24c-141">Откройте **Task Runner Explorer** (**представление > другие Windows > Task Runner Explorer**).</span><span class="sxs-lookup"><span data-stu-id="5d24c-141">Open the **Task Runner Explorer** (**View > Other Windows > Task Runner Explorer**).</span></span> <span data-ttu-id="5d24c-142">Используемые задачами, вы должны увидеть новую задачу с именем `less`.</span><span class="sxs-lookup"><span data-stu-id="5d24c-142">Among the tasks, you should see a new task named `less`.</span></span> <span data-ttu-id="5d24c-143">Может потребоваться обновить окно.</span><span class="sxs-lookup"><span data-stu-id="5d24c-143">You might have to refresh the window.</span></span>

<span data-ttu-id="5d24c-144">Запустите `less` задач и вы увидите результат, аналогичный, как показано здесь:</span><span class="sxs-lookup"><span data-stu-id="5d24c-144">Run the `less` task, and you see output similar to what is shown here:</span></span>

![меньше запускатель задач](less-sass-fa/_static/less-task-runner.png)

<span data-ttu-id="5d24c-146">*Wwwroot/css* папка теперь содержит новый файл, *main.css*:</span><span class="sxs-lookup"><span data-stu-id="5d24c-146">The *wwwroot/css* folder now contains a new file, *main.css*:</span></span>

![основной css создан](less-sass-fa/_static/main-css-created.png)

<span data-ttu-id="5d24c-148">Откройте *main.css* и вы увидите примерно следующее:</span><span class="sxs-lookup"><span data-stu-id="5d24c-148">Open *main.css* and you see something like the following:</span></span>

```css
body {
    background-color: #336666;
}
.baseColor {
    color: #663333;
}
.bgLight {
    color: #884a44;
}
.bgLight2 {
    color: #aa6355;
}
.bgDark {
    color: #442225;
}
.bgDark2 {
    color: #221114;
}
```

<span data-ttu-id="5d24c-149">Простую HTML-страницу, чтобы добавить *wwwroot* папки и ссылку *main.css* для просмотра цветовую палитру в действии.</span><span class="sxs-lookup"><span data-stu-id="5d24c-149">Add a simple HTML page to the *wwwroot* folder, and reference *main.css* to see the color palette in action.</span></span>

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8" />
    <link href="css/main.css" rel="stylesheet" />
    <title></title>
</head>
<body>
    <div>
        <div class="baseColor">BaseColor</div>
        <div class="bgLight">Light</div>
        <div class="bgLight2">Light2</div>
        <div class="bgDark">Dark</div>
        <div class="bgDark2">Dark2</div>
    </div>
</body>
</html>
```

<span data-ttu-id="5d24c-150">Вы увидите что 180 градусов вращаться во `@base` , использовавшихся для создания `@background` привело к цветовой круг противоположных цвет `@base`:</span><span class="sxs-lookup"><span data-stu-id="5d24c-150">You can see that the 180 degree spin on `@base` used to produce `@background` resulted in the color wheel opposing color of `@base`:</span></span>

![Пример менее тестирования](less-sass-fa/_static/less-test-screenshot.png)

<span data-ttu-id="5d24c-152">Меньше также поддерживает вложенные правила, а также вложенные медиа-запросами.</span><span class="sxs-lookup"><span data-stu-id="5d24c-152">Less also provides support for nested rules, as well as nested media queries.</span></span> <span data-ttu-id="5d24c-153">Например определение вложенные иерархии как меню может привести к подробных правил CSS, такие как следующие:</span><span class="sxs-lookup"><span data-stu-id="5d24c-153">For example, defining nested hierarchies like menus can result in verbose CSS rules like these:</span></span>

```css
nav {
    height: 40px;
    width: 100%;
}
nav li {
    height: 38px;
    width: 100px;
}
nav li a:link {
    color: #000;
    text-decoration: none;
}
nav li a:visited {
    text-decoration: none;
    color: #CC3333;
}
nav li a:hover {
    text-decoration: underline;
    font-weight: bold;
}
nav li a:active {
    text-decoration: underline;
}
```

<span data-ttu-id="5d24c-154">В идеале все правила стиля, связанных с будут располагаться друг с другом в CSS-файл, но на практике нет ничего применение этого правила, за исключением соглашение о вызовах и возможно комментариев блоке.</span><span class="sxs-lookup"><span data-stu-id="5d24c-154">Ideally all of the related style rules will be placed together within the CSS file, but in practice there's nothing enforcing this rule except convention and perhaps block comments.</span></span>

<span data-ttu-id="5d24c-155">Определив эти же правила, используя меньше выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="5d24c-155">Defining these same rules using Less looks like this:</span></span>

```less
nav {
    height: 40px;
    width: 100%;
    li {
        height: 38px;
        width: 100px;
        a {
            color: #000;
            &:link { text-decoration:none}
            &:visited { color: #CC3333; text-decoration:none}
            &:hover { text-decoration:underline; font-weight:bold}
            &:active {text-decoration:underline}
        }
    }
}
```

<span data-ttu-id="5d24c-156">Обратите внимание, что в этом случае все подчиненные элементы `nav` содержатся внутри своей области.</span><span class="sxs-lookup"><span data-stu-id="5d24c-156">Note that in this case, all of the subordinate elements of `nav` are contained within its scope.</span></span> <span data-ttu-id="5d24c-157">Больше не все повторения родительских элементов (`nav`, `li`, `a`), и число строк, общее также (хотя некоторые из, является результатом размещения значений на те же строки во втором примере).</span><span class="sxs-lookup"><span data-stu-id="5d24c-157">There's no longer any repetition of parent elements (`nav`, `li`, `a`), and the total line count has dropped as well (though some of that's a result of putting values on the same lines in the second example).</span></span> <span data-ttu-id="5d24c-158">Он может быть очень удобно, организационно, чтобы увидеть все правила для данного элемента пользовательского интерфейса в явно связанной области, в этом случае от остальной части файла, заключенные фигурные скобки.</span><span class="sxs-lookup"><span data-stu-id="5d24c-158">It can be very helpful, organizationally, to see all of the rules for a given UI element within an explicitly bounded scope, in this case set off from the rest of the file by curly braces.</span></span>

<span data-ttu-id="5d24c-159">`&` Синтаксис является компонентом селектор меньше с & представляющий родительский объект текущего выделения.</span><span class="sxs-lookup"><span data-stu-id="5d24c-159">The `&` syntax is a Less selector feature, with & representing the current selector parent.</span></span> <span data-ttu-id="5d24c-160">В этом случае в пределах {...}</span><span class="sxs-lookup"><span data-stu-id="5d24c-160">So, within the a {...}</span></span> <span data-ttu-id="5d24c-161">блок, `&` представляет `a` тег и, следовательно, `&:link` эквивалентен `a:link`.</span><span class="sxs-lookup"><span data-stu-id="5d24c-161">block, `&` represents an `a` tag, and thus `&:link` is equivalent to `a:link`.</span></span>

<span data-ttu-id="5d24c-162">Медиа-запросами, очень полезна при создании отвечает архитектуре, могут также активно участвовать в работе повторения и сложности в CSS.</span><span class="sxs-lookup"><span data-stu-id="5d24c-162">Media queries, extremely useful in creating responsive designs, can also contribute heavily to repetition and complexity in CSS.</span></span> <span data-ttu-id="5d24c-163">Меньше позволяет запросам мультимедиа вкладываются в классы, таким образом, чтобы все определение класса не должно повторяться в пределах разных верхнего уровня `@media` элементов.</span><span class="sxs-lookup"><span data-stu-id="5d24c-163">Less allows media queries to be nested within classes, so that the entire class definition doesn't need to be repeated within different top-level `@media` elements.</span></span> <span data-ttu-id="5d24c-164">Например вот CSS быстрые меню:</span><span class="sxs-lookup"><span data-stu-id="5d24c-164">For example, here is CSS for a responsive menu:</span></span>

```css
.navigation {
    margin-top: 30%;
    width: 100%;
}
@media screen and (min-width: 40em) {
    .navigation {
        margin: 0;
    }
}
@media screen and (min-width: 62em) {
    .navigation {
        width: 960px;
        margin: 0;
    }
}
```

<span data-ttu-id="5d24c-165">Это может быть лучше, определены в меньше как:</span><span class="sxs-lookup"><span data-stu-id="5d24c-165">This can be better defined in Less as:</span></span>

```less
.navigation {
    margin-top: 30%;
    width: 100%;
    @media screen and (min-width: 40em) {
        margin: 0;
    }
    @media screen and (min-width: 62em) {
        width: 960px;
        margin: 0;
    }
}
```

<span data-ttu-id="5d24c-166">Другой особенностью меньше, мы уже видели является поддержка математических операций, позволяя атрибуты стиля были сконструированы из предварительно определенные переменные.</span><span class="sxs-lookup"><span data-stu-id="5d24c-166">Another feature of Less that we have already seen is its support for mathematical operations, allowing style attributes to be constructed from pre-defined variables.</span></span> <span data-ttu-id="5d24c-167">В результате обновление связанных стили гораздо проще, так как базовый переменной может быть изменено, и все зависимые значения изменяются автоматически.</span><span class="sxs-lookup"><span data-stu-id="5d24c-167">This makes updating related styles much easier, since the base variable can be modified and all dependent values change automatically.</span></span>

<span data-ttu-id="5d24c-168">Файлы CSS, особенно для больших веб-узлов (и особенно в том случае, если используются медиа-запросами), привлекать довольно большим временем, что делает работу с ними громоздким.</span><span class="sxs-lookup"><span data-stu-id="5d24c-168">CSS files, especially for large sites (and especially if media queries are being used), tend to get quite large over time, making working with them unwieldy.</span></span> <span data-ttu-id="5d24c-169">Less-файлы можно задать отдельно, затем извлечь их с помощью `@import` директивы.</span><span class="sxs-lookup"><span data-stu-id="5d24c-169">Less files can be defined separately, then pulled together using `@import` directives.</span></span> <span data-ttu-id="5d24c-170">Меньше может также использоваться для импорта отдельных файлов CSS, а также при необходимости.</span><span class="sxs-lookup"><span data-stu-id="5d24c-170">Less can also be used to import individual CSS files, as well, if desired.</span></span>

<span data-ttu-id="5d24c-171">*Примеси* могут принимать параметры, а меньше поддерживает условную логику в виде из mixin условия, которые предоставляют декларативный способ определения, когда определенные примеси вступают в силу.</span><span class="sxs-lookup"><span data-stu-id="5d24c-171">*Mixins* can accept parameters, and Less supports conditional logic in the form of mixin guards, which provide a declarative way to define when certain mixins take effect.</span></span> <span data-ttu-id="5d24c-172">Обычно для примеси условия используется для настройки цветов на основе света или является темный цвет источника.</span><span class="sxs-lookup"><span data-stu-id="5d24c-172">A common use for mixin guards is to adjust colors based on how light or dark the source color is.</span></span> <span data-ttu-id="5d24c-173">Учитывая примеси, который принимает параметр для цвета, примеси условие можно использовать для изменения примеси, на основе этого цвета:</span><span class="sxs-lookup"><span data-stu-id="5d24c-173">Given a mixin that accepts a parameter for color, a mixin guard can be used to modify the mixin based on that color:</span></span>

```less
.box (@color) when (lightness(@color) >= 50%) {
    background-color: #000;
}
.box (@color) when (lightness(@color) < 50%) {
    background-color: #FFF;
}
.box (@color) {
    color: @color;
}

.feature {
    .box (@base);
}
```

<span data-ttu-id="5d24c-174">Учитывая текущие `@base` значение `#663333`, меньше он создаст следующий код CSS:</span><span class="sxs-lookup"><span data-stu-id="5d24c-174">Given our current `@base` value of `#663333`, this Less script will produce the following CSS:</span></span>

```css
.feature {
    background-color: #FFF;
    color: #663333;
}
```

<span data-ttu-id="5d24c-175">Меньше предоставляет ряд дополнительных функций, но она должна выдать некоторое представление о степени предварительной обработки языка.</span><span class="sxs-lookup"><span data-stu-id="5d24c-175">Less provides a number of additional features, but this should give you some idea of the power of this preprocessing language.</span></span>

## <a name="sass"></a><span data-ttu-id="5d24c-176">Sass</span><span class="sxs-lookup"><span data-stu-id="5d24c-176">Sass</span></span>

<span data-ttu-id="5d24c-177">Sass аналогична меньше, предоставляя поддержку многих те же функции, но с немного другой синтаксис.</span><span class="sxs-lookup"><span data-stu-id="5d24c-177">Sass is similar to Less, providing support for many of the same features, but with slightly different syntax.</span></span> <span data-ttu-id="5d24c-178">Он создается с помощью Ruby, а не JavaScript и может разные параметры настройки.</span><span class="sxs-lookup"><span data-stu-id="5d24c-178">It's built using Ruby, rather than JavaScript, and so has different setup requirements.</span></span> <span data-ttu-id="5d24c-179">На исходном языке Sass не использовать фигурные скобки или точкой с запятой, но вместо определенные области с помощью пробелов и отступов.</span><span class="sxs-lookup"><span data-stu-id="5d24c-179">The original Sass language didn't use curly braces or semicolons, but instead defined scope using white space and indentation.</span></span> <span data-ttu-id="5d24c-180">В версии 3 Sass, был представлен новый синтаксис, **SCSS** («Sassy CSS»).</span><span class="sxs-lookup"><span data-stu-id="5d24c-180">In version 3 of Sass, a new syntax was introduced, **SCSS** ("Sassy CSS").</span></span> <span data-ttu-id="5d24c-181">SCSS аналогична CSS уровней отступа и пробелы не учитываются, и вместо этого используется точка с запятой и фигурные скобки.</span><span class="sxs-lookup"><span data-stu-id="5d24c-181">SCSS is similar to CSS in that it ignores indentation levels and whitespace, and instead uses semicolons and curly braces.</span></span>

<span data-ttu-id="5d24c-182">Чтобы установить Sass, обычно вы бы сначала установить Ruby (предварительно установлен в macOS) и выполните:</span><span class="sxs-lookup"><span data-stu-id="5d24c-182">To install Sass, typically you would first install Ruby (pre-installed on macOS), and then run:</span></span>

```console
gem install sass
```

<span data-ttu-id="5d24c-183">Тем не менее если вы используете Visual Studio, вы можете получить работу с Sass во многом так же как это делается с меньшими усилиями.</span><span class="sxs-lookup"><span data-stu-id="5d24c-183">However, if you're running Visual Studio, you can get started with Sass in much the same way as you would with Less.</span></span> <span data-ttu-id="5d24c-184">Откройте *package.json* и добавить пакет «gulp sass» `devDependencies`:</span><span class="sxs-lookup"><span data-stu-id="5d24c-184">Open *package.json* and add the "gulp-sass" package to `devDependencies`:</span></span>

```json
"devDependencies": {
  "gulp": "3.9.1",
  "gulp-less": "3.3.0",
  "gulp-sass": "3.1.0"
}
```

<span data-ttu-id="5d24c-185">Затем измените *gulpfile.js* Добавление переменной sass и задачи для компиляции файлов Sass и помещает результаты в папке wwwroot:</span><span class="sxs-lookup"><span data-stu-id="5d24c-185">Next, modify *gulpfile.js* to add a sass variable and a task to compile your Sass files and place the results in the wwwroot folder:</span></span>

```javascript
var gulp = require("gulp"),
  fs = require("fs"),
  less = require("gulp-less"),
  sass = require("gulp-sass");

// other content removed

gulp.task("sass", function () {
  return gulp.src('Styles/main2.scss')
    .pipe(sass())
    .pipe(gulp.dest('wwwroot/css'));
});
```

<span data-ttu-id="5d24c-186">Теперь можно добавить файл Sass *main2.scss* для *стили* папку в корневой папке проекта:</span><span class="sxs-lookup"><span data-stu-id="5d24c-186">Now you can add the Sass file *main2.scss* to the *Styles* folder in the root of the project:</span></span>

![Добавьте файл scss](less-sass-fa/_static/add-scss-file.png)

<span data-ttu-id="5d24c-188">Откройте *main2.scss* и добавьте следующий код:</span><span class="sxs-lookup"><span data-stu-id="5d24c-188">Open *main2.scss* and add the following:</span></span>

```sass
$base: #CC0000;
body {
    background-color: $base;
}
```

<span data-ttu-id="5d24c-189">Сохраните все файлы.</span><span class="sxs-lookup"><span data-stu-id="5d24c-189">Save all of your files.</span></span> <span data-ttu-id="5d24c-190">Теперь при обновлении **Task Runner Explorer**, вы увидите `sass` задачи.</span><span class="sxs-lookup"><span data-stu-id="5d24c-190">Now when you refresh **Task Runner Explorer**, you see a `sass` task.</span></span> <span data-ttu-id="5d24c-191">Запустите его, а в */wwwroot/css* папки.</span><span class="sxs-lookup"><span data-stu-id="5d24c-191">Run it, and look in the */wwwroot/css* folder.</span></span> <span data-ttu-id="5d24c-192">Теперь есть *main2.css* файл с таким содержимым:</span><span class="sxs-lookup"><span data-stu-id="5d24c-192">There's now a *main2.css* file, with these contents:</span></span>

```css
body {
    background-color: #CC0000;
}
```

<span data-ttu-id="5d24c-193">Sass поддерживает вложение точно так же было меньше обозревателем, предоставляя аналогичные преимущества в отношении.</span><span class="sxs-lookup"><span data-stu-id="5d24c-193">Sass supports nesting in much the same was that Less does, providing similar benefits.</span></span> <span data-ttu-id="5d24c-194">Файлы можно разделить по функциям и включенных с использованием `@import` директивы:</span><span class="sxs-lookup"><span data-stu-id="5d24c-194">Files can be split up by function and included using the `@import` directive:</span></span>

```sass
@import 'anotherfile';
```

<span data-ttu-id="5d24c-195">Sass поддерживает примеси, с помощью `@mixin` ключевое слово их определения и `@include` Чтобы включить их, как в следующем примере из [sass lang.com](http://sass-lang.com):</span><span class="sxs-lookup"><span data-stu-id="5d24c-195">Sass supports mixins as well, using the `@mixin` keyword to define them and `@include` to include them, as in this example from [sass-lang.com](http://sass-lang.com):</span></span>

```sass
@mixin border-radius($radius) {
    -webkit-border-radius: $radius;
    -moz-border-radius: $radius;
    -ms-border-radius: $radius;
    border-radius: $radius;
}

.box { @include border-radius(10px); }
```

<span data-ttu-id="5d24c-196">В дополнение к примеси Sass также поддерживает концепцию наследования, позволяя один класс для другого расширения.</span><span class="sxs-lookup"><span data-stu-id="5d24c-196">In addition to mixins, Sass also supports the concept of inheritance, allowing one class to extend another.</span></span> <span data-ttu-id="5d24c-197">Он аналогичен примеси, но приводит к меньшим объемом кода CSS.</span><span class="sxs-lookup"><span data-stu-id="5d24c-197">It's conceptually similar to a mixin, but results in less CSS code.</span></span> <span data-ttu-id="5d24c-198">Он выполняется с помощью `@extend` ключевое слово.</span><span class="sxs-lookup"><span data-stu-id="5d24c-198">It's accomplished using the `@extend` keyword.</span></span> <span data-ttu-id="5d24c-199">Чтобы опробовать примеси, добавьте следующий код в ваш *main2.scss* файла:</span><span class="sxs-lookup"><span data-stu-id="5d24c-199">To try out mixins, add the following to your *main2.scss* file:</span></span>

```sass
@mixin alert {
    border: 1px solid black;
    padding: 5px;
    color: #333333;
}

.success {
    @include alert;
    border-color: green;
}

.error {
    @include alert;
    color: red;
    border-color: red;
    font-weight:bold;
}
```

<span data-ttu-id="5d24c-200">Изучите выходные данные в *main2.css* после выполнения команды `sass` задачи в **Task Runner Explorer**:</span><span class="sxs-lookup"><span data-stu-id="5d24c-200">Examine the output in *main2.css* after running the `sass` task in **Task Runner Explorer**:</span></span>

```css
.success {
    border: 1px solid black;
    padding: 5px;
    color: #333333;
    border-color: green;
 }

.error {
    border: 1px solid black;
    padding: 5px;
    color: #333333;
    color: red;
    border-color: red;
    font-weight: bold;
}
```

<span data-ttu-id="5d24c-201">Обратите внимание на то, что все общие свойства из mixin оповещения повторяются в каждом классе.</span><span class="sxs-lookup"><span data-stu-id="5d24c-201">Notice that all of the common properties of the alert mixin are repeated in each class.</span></span> <span data-ttu-id="5d24c-202">Mixin аналогичную хорошие помогает исключить дублирование во время разработки, но он по-прежнему создает CSS с большим дублируются, размер которых превышает необходимые файлы CSS - потенциальные проблемы производительности в результате чего.</span><span class="sxs-lookup"><span data-stu-id="5d24c-202">The mixin did a good job of helping eliminate duplication at development time, but it's still creating CSS with a lot of duplication in it, resulting in larger than necessary CSS files - a potential performance issue.</span></span>

<span data-ttu-id="5d24c-203">Теперь замените предупреждения примеси с `.alert` класса и измените `@include` для `@extend` (запоминание расширить `.alert`, а не `alert`):</span><span class="sxs-lookup"><span data-stu-id="5d24c-203">Now replace the alert mixin with a `.alert` class, and change `@include` to `@extend` (remembering to extend `.alert`, not `alert`):</span></span>

```sass
.alert {
    border: 1px solid black;
    padding: 5px;
    color: #333333;
}

.success {
    @extend .alert;
    border-color: green;
}

.error {
    @extend .alert;
    color: red;
    border-color: red;
    font-weight:bold;
}
```

<span data-ttu-id="5d24c-204">Еще раз выполните Sass и проверьте итоговый CSS:</span><span class="sxs-lookup"><span data-stu-id="5d24c-204">Run Sass once more, and examine the resulting CSS:</span></span>

```css
.alert, .success, .error {
    border: 1px solid black;
    padding: 5px;
    color: #333333;
}

.success {
    border-color: green;
}

.error {
    color: red;
    border-color: red;
    font-weight: bold;
}
```

<span data-ttu-id="5d24c-205">Теперь свойства определяются только как необходимое число раз, и лучше создается CSS.</span><span class="sxs-lookup"><span data-stu-id="5d24c-205">Now the properties are defined only as many times as needed, and better CSS is generated.</span></span>

<span data-ttu-id="5d24c-206">Sass также включает функции и операции условную логику, аналогичную меньше.</span><span class="sxs-lookup"><span data-stu-id="5d24c-206">Sass also includes functions and conditional logic operations, similar to Less.</span></span> <span data-ttu-id="5d24c-207">На самом деле возможности два языка очень похожи.</span><span class="sxs-lookup"><span data-stu-id="5d24c-207">In fact, the two languages' capabilities are very similar.</span></span>

## <a name="less-or-sass"></a><span data-ttu-id="5d24c-208">Менее или Sass?</span><span class="sxs-lookup"><span data-stu-id="5d24c-208">Less or Sass?</span></span>

<span data-ttu-id="5d24c-209">По-прежнему не консенсус относительно будь то обычно лучше использовать меньше или Sass (или даже нужно ли предпочитать исходного Sass или новых правил синтаксиса SCSS в Sass).</span><span class="sxs-lookup"><span data-stu-id="5d24c-209">There's still no consensus as to whether it's generally better to use Less or Sass (or even whether to prefer the original Sass or the newer SCSS syntax within Sass).</span></span> <span data-ttu-id="5d24c-210">Наверное, наиболее важное решение — **используйте один из этих средств**, а не просто вручную кодировать файлов CSS.</span><span class="sxs-lookup"><span data-stu-id="5d24c-210">Probably the most important decision is to **use one of these tools**, as opposed to just hand-coding your CSS files.</span></span> <span data-ttu-id="5d24c-211">После внесения, принятия решений, оба Less и Sass хорошими вариантами являются.</span><span class="sxs-lookup"><span data-stu-id="5d24c-211">Once you've made that decision, both Less and Sass are good choices.</span></span>

## <a name="font-awesome"></a><span data-ttu-id="5d24c-212">Font Awesome</span><span class="sxs-lookup"><span data-stu-id="5d24c-212">Font Awesome</span></span>

<span data-ttu-id="5d24c-213">Помимо препроцессорами CSS еще один интересный ресурс для современных веб-приложений стиля замечательно шрифта.</span><span class="sxs-lookup"><span data-stu-id="5d24c-213">In addition to CSS preprocessors, another great resource for styling modern web applications is Font Awesome.</span></span> <span data-ttu-id="5d24c-214">Font Awesome — это набор средств, который предоставляет более чем 500 масштабируемого векторного значки, которые могут свободно использоваться в веб-приложениях.</span><span class="sxs-lookup"><span data-stu-id="5d24c-214">Font Awesome is a toolkit that provides over 500 scalable vector icons that can be freely used in your web applications.</span></span> <span data-ttu-id="5d24c-215">Он был изначально разработаны для работы с помощью Bootstrap, но имеет не зависят от этой платформы или на любой библиотеки JavaScript.</span><span class="sxs-lookup"><span data-stu-id="5d24c-215">It was originally designed to work with Bootstrap, but it has no dependency on that framework or on any JavaScript libraries.</span></span>

<span data-ttu-id="5d24c-216">Чтобы приступить к работе с Font Awesome проще всего добавить ссылку на него, с помощью своего расположения в общедоступных доставки содержимого сети (CDN):</span><span class="sxs-lookup"><span data-stu-id="5d24c-216">The easiest way to get started with Font Awesome is to add a reference to it, using its public content delivery network (CDN) location:</span></span>

```html
<link rel="stylesheet" href="//maxcdn.bootstrapcdn.com/font-awesome/4.3.0/css/font-awesome.min.css">
```

<span data-ttu-id="5d24c-217">Его можно также добавить в проект Visual Studio, добавьте его в «зависимости» в *bower.json*:</span><span class="sxs-lookup"><span data-stu-id="5d24c-217">You can also add it to your Visual Studio project by adding it to the "dependencies" in *bower.json*:</span></span>

```json
{
  "name": "ASP.NET",
  "private": true,
  "dependencies": {
    "bootstrap": "3.0.0",
    "jquery": "1.10.2",
    "jquery-validation": "1.11.1",
    "jquery-validation-unobtrusive": "3.2.2",
    "hammer.js": "2.0.4",
    "bootstrap-touch-carousel": "0.8.0",
    "Font-Awesome": "4.3.0"
  }
}
```

<span data-ttu-id="5d24c-218">Получив ссылку на Font Awesome на странице, добавление значков для приложения, применяя классы Font Awesome, обычно начинаются с «fa-», чтобы элементов встроенного HTML (такие как `<span>` или `<i>`).</span><span class="sxs-lookup"><span data-stu-id="5d24c-218">Once you have a reference to Font Awesome on a page, you can add icons to your application by applying Font Awesome classes, typically prefixed with "fa-", to your inline HTML elements (such as `<span>` or `<i>`).</span></span>  <span data-ttu-id="5d24c-219">Например можно добавить значки для простых списков и меню, используя следующий код:</span><span class="sxs-lookup"><span data-stu-id="5d24c-219">For example, you can add icons to simple lists and menus using code like this:</span></span>

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8" />
    <title></title>
    <link href="lib/font-awesome/css/font-awesome.css" rel="stylesheet" />
</head>
<body>
    <ul class="fa-ul">
        <li><i class="fa fa-li fa-home"></i> Home</li>
        <li><i class="fa fa-li fa-cog"></i> Settings</li>
    </ul>
</body>
</html>
```

<span data-ttu-id="5d24c-220">В результате получается следующий код в браузере, — обратите внимание на значок рядом с каждого элемента:</span><span class="sxs-lookup"><span data-stu-id="5d24c-220">This produces the following in the browser - note the icon beside each item:</span></span>

![значки списка перечислены](less-sass-fa/_static/list-icons-screenshot.png)

<span data-ttu-id="5d24c-222">Можно просмотреть полный список доступных значков здесь:</span><span class="sxs-lookup"><span data-stu-id="5d24c-222">You can view a complete list of the available icons here:</span></span>

http://fontawesome.io/icons/

## <a name="summary"></a><span data-ttu-id="5d24c-223">Сводка</span><span class="sxs-lookup"><span data-stu-id="5d24c-223">Summary</span></span>

<span data-ttu-id="5d24c-224">Современных веб-приложений требуют все более быстро реагирующих гибких моделей, которые являются чистой, интуитивно понятный и простой в использовании из широкого спектра устройств.</span><span class="sxs-lookup"><span data-stu-id="5d24c-224">Modern web applications increasingly demand responsive, fluid designs that are clean, intuitive, and easy to use from a variety of devices.</span></span> <span data-ttu-id="5d24c-225">Управления, таблиц стилей CSS, необходимые для достижения этих целей лучше всего, менее с помощью препроцессора like или Sass.</span><span class="sxs-lookup"><span data-stu-id="5d24c-225">Managing the complexity of the CSS stylesheets required to achieve these goals is best done using a preprocessor like Less or Sass.</span></span> <span data-ttu-id="5d24c-226">Кроме того наборы средств, таких как Font Awesome быстро предоставлять хорошо известных значков в меню навигации текстовое и кнопок, повышение общей пользователь работы приложения.</span><span class="sxs-lookup"><span data-stu-id="5d24c-226">In addition, toolkits like Font Awesome quickly provide well-known icons to textual navigation menus and buttons, improving the overall user experience of your application.</span></span>
