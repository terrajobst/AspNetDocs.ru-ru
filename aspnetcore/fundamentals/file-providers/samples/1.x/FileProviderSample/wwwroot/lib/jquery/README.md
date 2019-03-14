---
ms.openlocfilehash: 610b16b181422978dc143b95f28658bbdf177fdd
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57028281"
---
# <a name="jquery"></a>jQuery

> jQuery — это быстрая, компактная и функционально богатая библиотека JavaScript.

Сведения о том, как начать работу с jQuery и как его правильно использовать, см. в [документации по jQuery](http://api.jquery.com/).
Сведения об исходных файлах и проблемах см. на странице [репозитория jQuery](https://github.com/jquery/jquery).

Перед обновлением ознакомьтесь с [записью блога о версии 3.3.1](https://blog.jquery.com/2017/03/20/jquery-3.3.1-now-available/). Здесь описаны важные отличия от предыдущей версии и представлена более удобочитаемая версия журнала изменений.

## <a name="including-jquery"></a>Включение jQuery

Ниже приведены несколько распространенных способов для включения jQuery.

### <a name="browser"></a>Браузер

#### <a name="script-tag"></a>Тэг Script

```html
<script src="https://code.jquery.com/jquery-3.3.1.min.js"></script>
```

#### <a name="babel"></a>Babel

[Babel](http://babeljs.io/) — это компилятор JavaScript нового поколения. Среди прочего, он уже умеет использовать модули ES6 или ES2015, хотя собственный код браузеров еще не поддерживает эту функцию.

```js
import $ from "jquery";
```

#### <a name="browserifywebpack"></a>Browserify и Webpack

Существует несколько способов использовать [Browserify](http://browserify.org/) и [Webpack](https://webpack.github.io/). Дополнительные сведения об использовании этих средств вы можете найти в документации по соответствующему проекту. В скриптах, в том числе скриптах jQuery, это выглядит обычно так.

```js
var $ = require("jquery");
```

#### <a name="amd-asynchronous-module-definition"></a>AMD (определение асинхронного модуля)

Формат модулей AMD специально разработан для браузеров. Подробные сведения вы найдете в [документации по require.js](http://requirejs.org/docs/whyamd.html).

```js
define(["jquery"], function($) {

});
```

### <a name="node"></a>Узел

Чтобы включить jQuery в [узел](nodejs.org), прежде всего следует выполнить установку с помощью npm.

```sh
npm install jquery
```

Чтобы использовать jQuery в узле, требуется окно с документом. Так как это окно не поддерживается в собственном коде узла, его следует смоделировать внешними средствами, например [jsdom](https://github.com/tmpvar/jsdom). Это будет полезно для тестирования.

```js
require("jsdom").env("", function(err, window) {
    if (err) {
        console.error(err);
        return;
    }

    var $ = require("jquery")(window);
});
```
