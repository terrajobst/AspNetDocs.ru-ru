---
ms.openlocfilehash: 3be420696add54094f24424285a905e7e7963bad
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57032891"
---
# <a name="bootstraphttpgetbootstrapcom"></a>[Начальная загрузка](http://getbootstrap.com)

[![Slack](https://bootstrap-slack.herokuapp.com/badge.svg)](https://bootstrap-slack.herokuapp.com)
![Версия Bower](https://img.shields.io/bower/v/bootstrap.svg)
[![Версия npm](https://img.shields.io/npm/v/bootstrap.svg)](https://www.npmjs.com/package/bootstrap)
[![Состояние сборки](https://img.shields.io/travis/twbs/bootstrap/master.svg)](https://travis-ci.org/twbs/bootstrap)
[![Состояние devDependency](https://img.shields.io/david/dev/twbs/bootstrap.svg)](https://david-dm.org/twbs/bootstrap#info=devDependencies)
[![NuGet](https://img.shields.io/nuget/v/bootstrap.svg)](https://www.nuget.org/packages/Bootstrap)
[![Состояние тестирования Selenium](https://saucelabs.com/browser-matrix/bootstrap.svg)](https://saucelabs.com/u/bootstrap)

"Начальная загрузка" — это эффективная, интуитивно понятная, мощная интерфейсная платформа, упрощающая и ускоряющая веб-разработку. Она создана [Марком Отто](https://twitter.com/mdo) (Mark Otto) и [Джейкобом Торнтоном](https://twitter.com/fat) (Jacob Thornton) и обслуживается [основной командой](https://github.com/orgs/twbs/people) с массовой поддержкой и участием сообщества.

Чтобы начать работу, посетите сайт <http://getbootstrap.com>!


## <a name="table-of-contents"></a>Содержание

* [Быстрое начало работы](#quick-start)
* [Ошибки и запросы функций](#bugs-and-feature-requests)
* [Документация](#documentation)
* [Добавление данных](#contributing)
* [Community](#community)
* [Управление версиями](#versioning)
* [Авторы](#creators)
* [Авторские права и лицензия](#copyright-and-license)


## <a name="quick-start"></a>Быстрое начало работы

Доступно несколько способов быстрого начала работы:

* [скачать новейший выпуск](https://github.com/twbs/bootstrap/archive/v3.3.7.zip);
* клонировать репозиторий: `git clone https://github.com/twbs/bootstrap.git`;
* установить с помощью [Bower](http://bower.io): `bower install bootstrap`;
* установить с помощью [npm](https://www.npmjs.com): `npm install bootstrap@3`;
* установить с помощью [Meteor](https://www.meteor.com): `meteor add twbs:bootstrap`;
* установить с помощью [Composer](https://getcomposer.org): `composer require twbs/bootstrap`.

Дополнительные сведения о содержимом, шаблонах, примерах и т. д. платформы см. на странице о [начале работы](http://getbootstrap.com/getting-started/).

### <a name="whats-included"></a>Включенные ресурсы

В скачанном каталоге вы увидите следующие каталоги и файлы с логически сгруппированными ресурсами, а также с компилированными и уменьшенными вариантами. Файл содержит примерно следующее:

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

Мы предоставляем скомпилированные CSS и JS (`bootstrap.*`), а также скомпилированные и уменьшенные CSS и JS (`bootstrap.min.*`). [Сопоставления источника](https://developer.chrome.com/devtools/docs/css-preprocessors) (`bootstrap.*.map`) CSS доступны для использования со средствами разработчика некоторых браузеров. Шрифты Glyphicons включены, так как являются дополнительной темой программы начальной загрузки.


## <a name="bugs-and-feature-requests"></a>Ошибки и запросы функций

Обнаружили ошибку или хотите запросить добавление функции? Сначала прочтите [руководство по устранению неполадок](https://github.com/twbs/bootstrap/blob/master/CONTRIBUTING.md#using-the-issue-tracker) и выполните поиск имеющихся и закрытых проблем. Если ваши проблема или предложение еще не рассматривались, [создайте запись](https://github.com/twbs/bootstrap/issues/new).

Обратите внимание, что **нужно запрашивать функции для [программы начальной загрузки версии 4](https://github.com/twbs/bootstrap/tree/v4-dev),** так как сейчас версия 3 находится в режиме обслуживания и в нее невозможно добавить новые функции. Это сделано, чтобы мы могли сосредоточить все усилия на улучшении программы начальной загрузки версии 4.


## <a name="documentation"></a>Документация

Документация по программе начальной загрузки, включенная в этот репозиторий в корневом каталоге, создается с помощью [Jekyll](http://jekyllrb.com) и находится в общем доступе на страницах GitHub по адресу <http://getbootstrap.com>. Документацию также можно запускать локально.

### <a name="running-documentation-locally"></a>Запуск документации локально

1. При необходимости [установите Jekyll](http://jekyllrb.com/docs/installation) и другие зависимости Ruby с помощью `bundle install`.
   **Примечание для пользователей Windows.** Чтение [этого неофициального руководства](http://jekyll-windows.juthilo.com/) для получения Jekyll приступить к работе без проблем.
2. Из корневого каталога `/bootstrap` запустите `bundle exec jekyll serve` в командной строке.
4. Откройте `http://localhost:9001` в браузере.

Дополнительные сведения об использовании Jekyll см. в [этой](http://jekyllrb.com/docs/home/) документации.

### <a name="documentation-for-previous-releases"></a>Документация для предыдущих выпусков

Сейчас документация по версии 2.3.2 доступна на странице <http://getbootstrap.com/2.3.2/> (на время перехода пользователей на программу начальной загрузки версии 3).

Вы также можете скачать [предыдущие выпуски](https://github.com/twbs/bootstrap/releases) и документацию по ним.


## <a name="contributing"></a>Добавление данных

Прочитайте наши [рекомендации по добавлению данных](https://github.com/twbs/bootstrap/blob/master/CONTRIBUTING.md). В них включены советы по добавлению записи о проблеме, стандарты программирования и примечания по разработке.

Кроме того, если запрос на вытягивание содержит исправления или функции JavaScript, необходимо включить [соответствующие модульные тесты](https://github.com/twbs/bootstrap/tree/master/js/tests). Все коды HTML и CSS должны соответствовать требованиям [руководства по написанию кода](https://github.com/mdo/code-guide), которое поддерживает [Марк Отто](https://github.com/mdo) (Mark Otto).

**Сейчас добавление новых функций в программу начальной загрузки версии 3 невозможно.** Она перешла в режим обслуживания, что позволяет нам сосредоточиться на улучшении будущей платформы [начальной загрузки версии 4](https://github.com/twbs/bootstrap/tree/v4-dev). Запросы на вытягивание, которые добавляют новые функции (а не исправления ошибок), должны быть предназначены для [начальной загрузки версии 4 (ветвь git `v4-dev`)](https://github.com/twbs/bootstrap/tree/v4-dev).

Параметры редактора, которые можно с легкостью использовать в стандартных текстовых редакторах, доступны в [конфигурации редактора](https://github.com/twbs/bootstrap/blob/master/.editorconfig). Узнайте больше о подключаемых модулях и скачайте их на сайте <http://editorconfig.org>.


## <a name="community"></a>Сообщество

Получайте новости о разработке платформы начальной загрузки и общайтесь с разработчиками проекта и членами сообщества.

* Подпишитесь на [@getbootstrap в Twitter](https://twitter.com/getbootstrap).
* Читайте [официальный блог платформы начальной загрузки](http://blog.getbootstrap.com) и оформите на него подписку.
* Присоединяйтесь к [официальной комнате Slack](https://bootstrap-slack.herokuapp.com).
* Общайтесь со специалистами по начальной загрузке в IRC на сервере `irc.freenode.net` канала `##bootstrap`.
* Справку по реализации можно найти в Stack Overflow (с тегом [`twitter-bootstrap-3`](https://stackoverflow.com/questions/tagged/twitter-bootstrap-3)).
* Разработчикам следует использовать ключевое слово `bootstrap` в пакетах, которые изменяют или добавляют функции платформы начальной загрузки при распространении через [npm](https://www.npmjs.com/browse/keyword/bootstrap) или аналогичные механизмы доставки, чтобы обеспечить максимально эффективное обнаружение.


## <a name="versioning"></a>Управление версиями

Мы хотим обеспечить прозрачность цикла выпуска и стремимся поддерживать обратную совместимость, поэтому платформа начальной загрузки обслуживается в соответствии с требованиями [руководства по Семантическому версионированию](http://semver.org/). Иногда это невозможно, но мы будем придерживаться этих правил, когда это возможно.

Дополнительные сведения о журналах изменений для каждой версии выпуска программы начальной загрузки см. в [этой](https://github.com/twbs/bootstrap/releases) статье. Записи об объявлениях о выходе в [официальном блоге по программе начальной загрузки](http://blog.getbootstrap.com) содержат сводки наиболее значимых изменений, внесенных в каждом выпуске.


## <a name="creators"></a>Авторы

**Марк Отто (Mark Otto)**

* <https://twitter.com/mdo>
* <https://github.com/mdo>

**Джейкоб Торнтон (Jacob Thornton)**

* <https://twitter.com/fat>
* <https://github.com/fat>


## <a name="copyright-and-license"></a>Авторские права и лицензия

Код и авторские права на документацию 2011–2016 Twitter, Inc. Код выпущен с задействованием [лицензии MIT](https://github.com/twbs/bootstrap/blob/master/LICENSE). Документы выпущены с задействованием [Creative Commons](https://github.com/twbs/bootstrap/blob/master/docs/LICENSE).
