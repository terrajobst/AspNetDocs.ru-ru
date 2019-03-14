---
ms.openlocfilehash: 3be420696add54094f24424285a905e7e7963bad
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57028831"
---
# <a name="bootstraphttpgetbootstrapcom"></a>[<span data-ttu-id="37bf6-101">Начальная загрузка</span><span class="sxs-lookup"><span data-stu-id="37bf6-101">Bootstrap</span></span>](http://getbootstrap.com)

<span data-ttu-id="37bf6-102">[![Slack](https://bootstrap-slack.herokuapp.com/badge.svg)](https://bootstrap-slack.herokuapp.com)
![Версия Bower](https://img.shields.io/bower/v/bootstrap.svg)
[![Версия npm](https://img.shields.io/npm/v/bootstrap.svg)](https://www.npmjs.com/package/bootstrap)
[![Состояние сборки](https://img.shields.io/travis/twbs/bootstrap/master.svg)](https://travis-ci.org/twbs/bootstrap)
[![Состояние devDependency](https://img.shields.io/david/dev/twbs/bootstrap.svg)](https://david-dm.org/twbs/bootstrap#info=devDependencies)
[![NuGet](https://img.shields.io/nuget/v/bootstrap.svg)](https://www.nuget.org/packages/Bootstrap)
[![Состояние тестирования Selenium](https://saucelabs.com/browser-matrix/bootstrap.svg)](https://saucelabs.com/u/bootstrap)</span><span class="sxs-lookup"><span data-stu-id="37bf6-102">[![Slack](https://bootstrap-slack.herokuapp.com/badge.svg)](https://bootstrap-slack.herokuapp.com)
![Bower version](https://img.shields.io/bower/v/bootstrap.svg)
[![npm version](https://img.shields.io/npm/v/bootstrap.svg)](https://www.npmjs.com/package/bootstrap)
[![Build Status](https://img.shields.io/travis/twbs/bootstrap/master.svg)](https://travis-ci.org/twbs/bootstrap)
[![devDependency Status](https://img.shields.io/david/dev/twbs/bootstrap.svg)](https://david-dm.org/twbs/bootstrap#info=devDependencies)
[![NuGet](https://img.shields.io/nuget/v/bootstrap.svg)](https://www.nuget.org/packages/Bootstrap)
[![Selenium Test Status](https://saucelabs.com/browser-matrix/bootstrap.svg)](https://saucelabs.com/u/bootstrap)</span></span>

<span data-ttu-id="37bf6-103">"Начальная загрузка" — это эффективная, интуитивно понятная, мощная интерфейсная платформа, упрощающая и ускоряющая веб-разработку. Она создана [Марком Отто](https://twitter.com/mdo) (Mark Otto) и [Джейкобом Торнтоном](https://twitter.com/fat) (Jacob Thornton) и обслуживается [основной командой](https://github.com/orgs/twbs/people) с массовой поддержкой и участием сообщества.</span><span class="sxs-lookup"><span data-stu-id="37bf6-103">Bootstrap is a sleek, intuitive, and powerful front-end framework for faster and easier web development, created by [Mark Otto](https://twitter.com/mdo) and [Jacob Thornton](https://twitter.com/fat), and maintained by the [core team](https://github.com/orgs/twbs/people) with the massive support and involvement of the community.</span></span>

<span data-ttu-id="37bf6-104">Чтобы начать работу, посетите сайт <http://getbootstrap.com>!</span><span class="sxs-lookup"><span data-stu-id="37bf6-104">To get started, check out <http://getbootstrap.com>!</span></span>


## <a name="table-of-contents"></a><span data-ttu-id="37bf6-105">Содержание</span><span class="sxs-lookup"><span data-stu-id="37bf6-105">Table of contents</span></span>

* [<span data-ttu-id="37bf6-106">Быстрое начало работы</span><span class="sxs-lookup"><span data-stu-id="37bf6-106">Quick start</span></span>](#quick-start)
* [<span data-ttu-id="37bf6-107">Ошибки и запросы функций</span><span class="sxs-lookup"><span data-stu-id="37bf6-107">Bugs and feature requests</span></span>](#bugs-and-feature-requests)
* [<span data-ttu-id="37bf6-108">Документация</span><span class="sxs-lookup"><span data-stu-id="37bf6-108">Documentation</span></span>](#documentation)
* [<span data-ttu-id="37bf6-109">Добавление данных</span><span class="sxs-lookup"><span data-stu-id="37bf6-109">Contributing</span></span>](#contributing)
* [<span data-ttu-id="37bf6-110">Community</span><span class="sxs-lookup"><span data-stu-id="37bf6-110">Community</span></span>](#community)
* [<span data-ttu-id="37bf6-111">Управление версиями</span><span class="sxs-lookup"><span data-stu-id="37bf6-111">Versioning</span></span>](#versioning)
* [<span data-ttu-id="37bf6-112">Авторы</span><span class="sxs-lookup"><span data-stu-id="37bf6-112">Creators</span></span>](#creators)
* [<span data-ttu-id="37bf6-113">Авторские права и лицензия</span><span class="sxs-lookup"><span data-stu-id="37bf6-113">Copyright and license</span></span>](#copyright-and-license)


## <a name="quick-start"></a><span data-ttu-id="37bf6-114">Быстрое начало работы</span><span class="sxs-lookup"><span data-stu-id="37bf6-114">Quick start</span></span>

<span data-ttu-id="37bf6-115">Доступно несколько способов быстрого начала работы:</span><span class="sxs-lookup"><span data-stu-id="37bf6-115">Several quick start options are available:</span></span>

* <span data-ttu-id="37bf6-116">[скачать новейший выпуск](https://github.com/twbs/bootstrap/archive/v3.3.7.zip);</span><span class="sxs-lookup"><span data-stu-id="37bf6-116">[Download the latest release](https://github.com/twbs/bootstrap/archive/v3.3.7.zip).</span></span>
* <span data-ttu-id="37bf6-117">клонировать репозиторий: `git clone https://github.com/twbs/bootstrap.git`;</span><span class="sxs-lookup"><span data-stu-id="37bf6-117">Clone the repo: `git clone https://github.com/twbs/bootstrap.git`.</span></span>
* <span data-ttu-id="37bf6-118">установить с помощью [Bower](http://bower.io): `bower install bootstrap`;</span><span class="sxs-lookup"><span data-stu-id="37bf6-118">Install with [Bower](http://bower.io): `bower install bootstrap`.</span></span>
* <span data-ttu-id="37bf6-119">установить с помощью [npm](https://www.npmjs.com): `npm install bootstrap@3`;</span><span class="sxs-lookup"><span data-stu-id="37bf6-119">Install with [npm](https://www.npmjs.com): `npm install bootstrap@3`.</span></span>
* <span data-ttu-id="37bf6-120">установить с помощью [Meteor](https://www.meteor.com): `meteor add twbs:bootstrap`;</span><span class="sxs-lookup"><span data-stu-id="37bf6-120">Install with [Meteor](https://www.meteor.com): `meteor add twbs:bootstrap`.</span></span>
* <span data-ttu-id="37bf6-121">установить с помощью [Composer](https://getcomposer.org): `composer require twbs/bootstrap`.</span><span class="sxs-lookup"><span data-stu-id="37bf6-121">Install with [Composer](https://getcomposer.org): `composer require twbs/bootstrap`.</span></span>

<span data-ttu-id="37bf6-122">Дополнительные сведения о содержимом, шаблонах, примерах и т. д. платформы см. на странице о [начале работы](http://getbootstrap.com/getting-started/).</span><span class="sxs-lookup"><span data-stu-id="37bf6-122">Read the [Getting started page](http://getbootstrap.com/getting-started/) for information on the framework contents, templates and examples, and more.</span></span>

### <a name="whats-included"></a><span data-ttu-id="37bf6-123">Включенные ресурсы</span><span class="sxs-lookup"><span data-stu-id="37bf6-123">What's included</span></span>

<span data-ttu-id="37bf6-124">В скачанном каталоге вы увидите следующие каталоги и файлы с логически сгруппированными ресурсами, а также с компилированными и уменьшенными вариантами.</span><span class="sxs-lookup"><span data-stu-id="37bf6-124">Within the download you'll find the following directories and files, logically grouping common assets and providing both compiled and minified variations.</span></span> <span data-ttu-id="37bf6-125">Файл содержит примерно следующее:</span><span class="sxs-lookup"><span data-stu-id="37bf6-125">You'll see something like this:</span></span>

```
bootstrap/
├── css/
│   ├── bootstrap.css
│   ├── bootstrap.css.map
│   ├── bootstrap.min.css
│   ├── bootstrap.min.css.map
│   ├── bootstrap-theme.css
│   ├── bootstrap-theme.css.map
│   ├── bootstrap-theme.min.css
│   └── bootstrap-theme.min.css.map
├── js/
│   ├── bootstrap.js
│   └── bootstrap.min.js
└── fonts/
    ├── glyphicons-halflings-regular.eot
    ├── glyphicons-halflings-regular.svg
    ├── glyphicons-halflings-regular.ttf
    ├── glyphicons-halflings-regular.woff
    └── glyphicons-halflings-regular.woff2
```

<span data-ttu-id="37bf6-126">Мы предоставляем скомпилированные CSS и JS (`bootstrap.*`), а также скомпилированные и уменьшенные CSS и JS (`bootstrap.min.*`).</span><span class="sxs-lookup"><span data-stu-id="37bf6-126">We provide compiled CSS and JS (`bootstrap.*`), as well as compiled and minified CSS and JS (`bootstrap.min.*`).</span></span> <span data-ttu-id="37bf6-127">[Сопоставления источника](https://developer.chrome.com/devtools/docs/css-preprocessors) (`bootstrap.*.map`) CSS доступны для использования со средствами разработчика некоторых браузеров.</span><span class="sxs-lookup"><span data-stu-id="37bf6-127">CSS [source maps](https://developer.chrome.com/devtools/docs/css-preprocessors) (`bootstrap.*.map`) are available for use with certain browsers' developer tools.</span></span> <span data-ttu-id="37bf6-128">Шрифты Glyphicons включены, так как являются дополнительной темой программы начальной загрузки.</span><span class="sxs-lookup"><span data-stu-id="37bf6-128">Fonts from Glyphicons are included, as is the optional Bootstrap theme.</span></span>


## <a name="bugs-and-feature-requests"></a><span data-ttu-id="37bf6-129">Ошибки и запросы функций</span><span class="sxs-lookup"><span data-stu-id="37bf6-129">Bugs and feature requests</span></span>

<span data-ttu-id="37bf6-130">Обнаружили ошибку или хотите запросить добавление функции?</span><span class="sxs-lookup"><span data-stu-id="37bf6-130">Have a bug or a feature request?</span></span> <span data-ttu-id="37bf6-131">Сначала прочтите [руководство по устранению неполадок](https://github.com/twbs/bootstrap/blob/master/CONTRIBUTING.md#using-the-issue-tracker) и выполните поиск имеющихся и закрытых проблем.</span><span class="sxs-lookup"><span data-stu-id="37bf6-131">Please first read the [issue guidelines](https://github.com/twbs/bootstrap/blob/master/CONTRIBUTING.md#using-the-issue-tracker) and search for existing and closed issues.</span></span> <span data-ttu-id="37bf6-132">Если ваши проблема или предложение еще не рассматривались, [создайте запись](https://github.com/twbs/bootstrap/issues/new).</span><span class="sxs-lookup"><span data-stu-id="37bf6-132">If your problem or idea is not addressed yet, [please open a new issue](https://github.com/twbs/bootstrap/issues/new).</span></span>

<span data-ttu-id="37bf6-133">Обратите внимание, что **нужно запрашивать функции для [программы начальной загрузки версии 4](https://github.com/twbs/bootstrap/tree/v4-dev),** так как сейчас версия 3 находится в режиме обслуживания и в нее невозможно добавить новые функции.</span><span class="sxs-lookup"><span data-stu-id="37bf6-133">Note that **feature requests must target [Bootstrap v4](https://github.com/twbs/bootstrap/tree/v4-dev),** because Bootstrap v3 is now in maintenance mode and is closed off to new features.</span></span> <span data-ttu-id="37bf6-134">Это сделано, чтобы мы могли сосредоточить все усилия на улучшении программы начальной загрузки версии 4.</span><span class="sxs-lookup"><span data-stu-id="37bf6-134">This is so that we can focus our efforts on Bootstrap v4.</span></span>


## <a name="documentation"></a><span data-ttu-id="37bf6-135">Документация</span><span class="sxs-lookup"><span data-stu-id="37bf6-135">Documentation</span></span>

<span data-ttu-id="37bf6-136">Документация по программе начальной загрузки, включенная в этот репозиторий в корневом каталоге, создается с помощью [Jekyll](http://jekyllrb.com) и находится в общем доступе на страницах GitHub по адресу <http://getbootstrap.com>.</span><span class="sxs-lookup"><span data-stu-id="37bf6-136">Bootstrap's documentation, included in this repo in the root directory, is built with [Jekyll](http://jekyllrb.com) and publicly hosted on GitHub Pages at <http://getbootstrap.com>.</span></span> <span data-ttu-id="37bf6-137">Документацию также можно запускать локально.</span><span class="sxs-lookup"><span data-stu-id="37bf6-137">The docs may also be run locally.</span></span>

### <a name="running-documentation-locally"></a><span data-ttu-id="37bf6-138">Запуск документации локально</span><span class="sxs-lookup"><span data-stu-id="37bf6-138">Running documentation locally</span></span>

1. <span data-ttu-id="37bf6-139">При необходимости [установите Jekyll](http://jekyllrb.com/docs/installation) и другие зависимости Ruby с помощью `bundle install`.</span><span class="sxs-lookup"><span data-stu-id="37bf6-139">If necessary, [install Jekyll](http://jekyllrb.com/docs/installation) and other Ruby dependencies with `bundle install`.</span></span>
   <span data-ttu-id="37bf6-140">**Примечание для пользователей Windows.** Чтение [этого неофициального руководства](http://jekyll-windows.juthilo.com/) для получения Jekyll приступить к работе без проблем.</span><span class="sxs-lookup"><span data-stu-id="37bf6-140">**Note for Windows users:** Read [this unofficial guide](http://jekyll-windows.juthilo.com/) to get Jekyll up and running without problems.</span></span>
2. <span data-ttu-id="37bf6-141">Из корневого каталога `/bootstrap` запустите `bundle exec jekyll serve` в командной строке.</span><span class="sxs-lookup"><span data-stu-id="37bf6-141">From the root `/bootstrap` directory, run `bundle exec jekyll serve` in the command line.</span></span>
4. <span data-ttu-id="37bf6-142">Откройте `http://localhost:9001` в браузере.</span><span class="sxs-lookup"><span data-stu-id="37bf6-142">Open `http://localhost:9001` in your browser, and voilà.</span></span>

<span data-ttu-id="37bf6-143">Дополнительные сведения об использовании Jekyll см. в [этой](http://jekyllrb.com/docs/home/) документации.</span><span class="sxs-lookup"><span data-stu-id="37bf6-143">Learn more about using Jekyll by reading its [documentation](http://jekyllrb.com/docs/home/).</span></span>

### <a name="documentation-for-previous-releases"></a><span data-ttu-id="37bf6-144">Документация для предыдущих выпусков</span><span class="sxs-lookup"><span data-stu-id="37bf6-144">Documentation for previous releases</span></span>

<span data-ttu-id="37bf6-145">Сейчас документация по версии 2.3.2 доступна на странице <http://getbootstrap.com/2.3.2/> (на время перехода пользователей на программу начальной загрузки версии 3).</span><span class="sxs-lookup"><span data-stu-id="37bf6-145">Documentation for v2.3.2 has been made available for the time being at <http://getbootstrap.com/2.3.2/> while folks transition to Bootstrap 3.</span></span>

<span data-ttu-id="37bf6-146">Вы также можете скачать [предыдущие выпуски](https://github.com/twbs/bootstrap/releases) и документацию по ним.</span><span class="sxs-lookup"><span data-stu-id="37bf6-146">[Previous releases](https://github.com/twbs/bootstrap/releases) and their documentation are also available for download.</span></span>


## <a name="contributing"></a><span data-ttu-id="37bf6-147">Добавление данных</span><span class="sxs-lookup"><span data-stu-id="37bf6-147">Contributing</span></span>

<span data-ttu-id="37bf6-148">Прочитайте наши [рекомендации по добавлению данных](https://github.com/twbs/bootstrap/blob/master/CONTRIBUTING.md).</span><span class="sxs-lookup"><span data-stu-id="37bf6-148">Please read through our [contributing guidelines](https://github.com/twbs/bootstrap/blob/master/CONTRIBUTING.md).</span></span> <span data-ttu-id="37bf6-149">В них включены советы по добавлению записи о проблеме, стандарты программирования и примечания по разработке.</span><span class="sxs-lookup"><span data-stu-id="37bf6-149">Included are directions for opening issues, coding standards, and notes on development.</span></span>

<span data-ttu-id="37bf6-150">Кроме того, если запрос на вытягивание содержит исправления или функции JavaScript, необходимо включить [соответствующие модульные тесты](https://github.com/twbs/bootstrap/tree/master/js/tests).</span><span class="sxs-lookup"><span data-stu-id="37bf6-150">Moreover, if your pull request contains JavaScript patches or features, you must include [relevant unit tests](https://github.com/twbs/bootstrap/tree/master/js/tests).</span></span> <span data-ttu-id="37bf6-151">Все коды HTML и CSS должны соответствовать требованиям [руководства по написанию кода](https://github.com/mdo/code-guide), которое поддерживает [Марк Отто](https://github.com/mdo) (Mark Otto).</span><span class="sxs-lookup"><span data-stu-id="37bf6-151">All HTML and CSS should conform to the [Code Guide](https://github.com/mdo/code-guide), maintained by [Mark Otto](https://github.com/mdo).</span></span>

<span data-ttu-id="37bf6-152">**Сейчас добавление новых функций в программу начальной загрузки версии 3 невозможно.**</span><span class="sxs-lookup"><span data-stu-id="37bf6-152">**Bootstrap v3 is now closed off to new features.**</span></span> <span data-ttu-id="37bf6-153">Она перешла в режим обслуживания, что позволяет нам сосредоточиться на улучшении будущей платформы [начальной загрузки версии 4](https://github.com/twbs/bootstrap/tree/v4-dev).</span><span class="sxs-lookup"><span data-stu-id="37bf6-153">It has gone into maintenance mode so that we can focus our efforts on [Bootstrap v4](https://github.com/twbs/bootstrap/tree/v4-dev), the future of the framework.</span></span> <span data-ttu-id="37bf6-154">Запросы на вытягивание, которые добавляют новые функции (а не исправления ошибок), должны быть предназначены для [начальной загрузки версии 4 (ветвь git `v4-dev`)](https://github.com/twbs/bootstrap/tree/v4-dev).</span><span class="sxs-lookup"><span data-stu-id="37bf6-154">Pull requests which add new features (rather than fix bugs) should target [Bootstrap v4 (the `v4-dev` git branch)](https://github.com/twbs/bootstrap/tree/v4-dev) instead.</span></span>

<span data-ttu-id="37bf6-155">Параметры редактора, которые можно с легкостью использовать в стандартных текстовых редакторах, доступны в [конфигурации редактора](https://github.com/twbs/bootstrap/blob/master/.editorconfig).</span><span class="sxs-lookup"><span data-stu-id="37bf6-155">Editor preferences are available in the [editor config](https://github.com/twbs/bootstrap/blob/master/.editorconfig) for easy use in common text editors.</span></span> <span data-ttu-id="37bf6-156">Узнайте больше о подключаемых модулях и скачайте их на сайте <http://editorconfig.org>.</span><span class="sxs-lookup"><span data-stu-id="37bf6-156">Read more and download plugins at <http://editorconfig.org>.</span></span>


## <a name="community"></a><span data-ttu-id="37bf6-157">Сообщество</span><span class="sxs-lookup"><span data-stu-id="37bf6-157">Community</span></span>

<span data-ttu-id="37bf6-158">Получайте новости о разработке платформы начальной загрузки и общайтесь с разработчиками проекта и членами сообщества.</span><span class="sxs-lookup"><span data-stu-id="37bf6-158">Get updates on Bootstrap's development and chat with the project maintainers and community members.</span></span>

* <span data-ttu-id="37bf6-159">Подпишитесь на [@getbootstrap в Twitter](https://twitter.com/getbootstrap).</span><span class="sxs-lookup"><span data-stu-id="37bf6-159">Follow [@getbootstrap on Twitter](https://twitter.com/getbootstrap).</span></span>
* <span data-ttu-id="37bf6-160">Читайте [официальный блог платформы начальной загрузки](http://blog.getbootstrap.com) и оформите на него подписку.</span><span class="sxs-lookup"><span data-stu-id="37bf6-160">Read and subscribe to [The Official Bootstrap Blog](http://blog.getbootstrap.com).</span></span>
* <span data-ttu-id="37bf6-161">Присоединяйтесь к [официальной комнате Slack](https://bootstrap-slack.herokuapp.com).</span><span class="sxs-lookup"><span data-stu-id="37bf6-161">Join [the official Slack room](https://bootstrap-slack.herokuapp.com).</span></span>
* <span data-ttu-id="37bf6-162">Общайтесь со специалистами по начальной загрузке в IRC</span><span class="sxs-lookup"><span data-stu-id="37bf6-162">Chat with fellow Bootstrappers in IRC.</span></span> <span data-ttu-id="37bf6-163">на сервере `irc.freenode.net` канала `##bootstrap`.</span><span class="sxs-lookup"><span data-stu-id="37bf6-163">On the `irc.freenode.net` server, in the `##bootstrap` channel.</span></span>
* <span data-ttu-id="37bf6-164">Справку по реализации можно найти в Stack Overflow (с тегом [`twitter-bootstrap-3`](https://stackoverflow.com/questions/tagged/twitter-bootstrap-3)).</span><span class="sxs-lookup"><span data-stu-id="37bf6-164">Implementation help may be found at Stack Overflow (tagged [`twitter-bootstrap-3`](https://stackoverflow.com/questions/tagged/twitter-bootstrap-3)).</span></span>
* <span data-ttu-id="37bf6-165">Разработчикам следует использовать ключевое слово `bootstrap` в пакетах, которые изменяют или добавляют функции платформы начальной загрузки при распространении через [npm](https://www.npmjs.com/browse/keyword/bootstrap) или аналогичные механизмы доставки, чтобы обеспечить максимально эффективное обнаружение.</span><span class="sxs-lookup"><span data-stu-id="37bf6-165">Developers should use the keyword `bootstrap` on packages which modify or add to the functionality of Bootstrap when distributing through [npm](https://www.npmjs.com/browse/keyword/bootstrap) or similar delivery mechanisms for maximum discoverability.</span></span>


## <a name="versioning"></a><span data-ttu-id="37bf6-166">Управление версиями</span><span class="sxs-lookup"><span data-stu-id="37bf6-166">Versioning</span></span>

<span data-ttu-id="37bf6-167">Мы хотим обеспечить прозрачность цикла выпуска и стремимся поддерживать обратную совместимость, поэтому платформа начальной загрузки обслуживается в соответствии с требованиями [руководства по Семантическому версионированию](http://semver.org/).</span><span class="sxs-lookup"><span data-stu-id="37bf6-167">For transparency into our release cycle and in striving to maintain backward compatibility, Bootstrap is maintained under [the Semantic Versioning guidelines](http://semver.org/).</span></span> <span data-ttu-id="37bf6-168">Иногда это невозможно, но мы будем придерживаться этих правил, когда это возможно.</span><span class="sxs-lookup"><span data-stu-id="37bf6-168">Sometimes we screw up, but we'll adhere to those rules whenever possible.</span></span>

<span data-ttu-id="37bf6-169">Дополнительные сведения о журналах изменений для каждой версии выпуска программы начальной загрузки см. в [этой](https://github.com/twbs/bootstrap/releases) статье.</span><span class="sxs-lookup"><span data-stu-id="37bf6-169">See [the Releases section of our GitHub project](https://github.com/twbs/bootstrap/releases) for changelogs for each release version of Bootstrap.</span></span> <span data-ttu-id="37bf6-170">Записи об объявлениях о выходе в [официальном блоге по программе начальной загрузки](http://blog.getbootstrap.com) содержат сводки наиболее значимых изменений, внесенных в каждом выпуске.</span><span class="sxs-lookup"><span data-stu-id="37bf6-170">Release announcement posts on [the official Bootstrap blog](http://blog.getbootstrap.com) contain summaries of the most noteworthy changes made in each release.</span></span>


## <a name="creators"></a><span data-ttu-id="37bf6-171">Авторы</span><span class="sxs-lookup"><span data-stu-id="37bf6-171">Creators</span></span>

<span data-ttu-id="37bf6-172">**Марк Отто (Mark Otto)**</span><span class="sxs-lookup"><span data-stu-id="37bf6-172">**Mark Otto**</span></span>

* <https://twitter.com/mdo>
* <https://github.com/mdo>

<span data-ttu-id="37bf6-173">**Джейкоб Торнтон (Jacob Thornton)**</span><span class="sxs-lookup"><span data-stu-id="37bf6-173">**Jacob Thornton**</span></span>

* <https://twitter.com/fat>
* <https://github.com/fat>


## <a name="copyright-and-license"></a><span data-ttu-id="37bf6-174">Авторские права и лицензия</span><span class="sxs-lookup"><span data-stu-id="37bf6-174">Copyright and license</span></span>

<span data-ttu-id="37bf6-175">Код и авторские права на документацию 2011–2016 Twitter, Inc. Код выпущен с задействованием [лицензии MIT](https://github.com/twbs/bootstrap/blob/master/LICENSE).</span><span class="sxs-lookup"><span data-stu-id="37bf6-175">Code and documentation copyright 2011-2016 Twitter, Inc. Code released under [the MIT license](https://github.com/twbs/bootstrap/blob/master/LICENSE).</span></span> <span data-ttu-id="37bf6-176">Документы выпущены с задействованием [Creative Commons](https://github.com/twbs/bootstrap/blob/master/docs/LICENSE).</span><span class="sxs-lookup"><span data-stu-id="37bf6-176">Docs released under [Creative Commons](https://github.com/twbs/bootstrap/blob/master/docs/LICENSE).</span></span>
