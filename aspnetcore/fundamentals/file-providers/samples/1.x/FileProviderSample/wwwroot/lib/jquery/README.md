---
ms.openlocfilehash: 610b16b181422978dc143b95f28658bbdf177fdd
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57028281"
---
# <a name="jquery"></a><span data-ttu-id="a1f8c-101">jQuery</span><span class="sxs-lookup"><span data-stu-id="a1f8c-101">jQuery</span></span>

> <span data-ttu-id="a1f8c-102">jQuery — это быстрая, компактная и функционально богатая библиотека JavaScript.</span><span class="sxs-lookup"><span data-stu-id="a1f8c-102">jQuery is a fast, small, and feature-rich JavaScript library.</span></span>

<span data-ttu-id="a1f8c-103">Сведения о том, как начать работу с jQuery и как его правильно использовать, см. в [документации по jQuery](http://api.jquery.com/).</span><span class="sxs-lookup"><span data-stu-id="a1f8c-103">For information on how to get started and how to use jQuery, please see [jQuery's documentation](http://api.jquery.com/).</span></span>
<span data-ttu-id="a1f8c-104">Сведения об исходных файлах и проблемах см. на странице [репозитория jQuery](https://github.com/jquery/jquery).</span><span class="sxs-lookup"><span data-stu-id="a1f8c-104">For source files and issues, please visit the [jQuery repo](https://github.com/jquery/jquery).</span></span>

<span data-ttu-id="a1f8c-105">Перед обновлением ознакомьтесь с [записью блога о версии 3.3.1](https://blog.jquery.com/2017/03/20/jquery-3.3.1-now-available/).</span><span class="sxs-lookup"><span data-stu-id="a1f8c-105">If upgrading, please see the [blog post for 3.3.1](https://blog.jquery.com/2017/03/20/jquery-3.3.1-now-available/).</span></span> <span data-ttu-id="a1f8c-106">Здесь описаны важные отличия от предыдущей версии и представлена более удобочитаемая версия журнала изменений.</span><span class="sxs-lookup"><span data-stu-id="a1f8c-106">This includes notable differences from the previous version and a more readable changelog.</span></span>

## <a name="including-jquery"></a><span data-ttu-id="a1f8c-107">Включение jQuery</span><span class="sxs-lookup"><span data-stu-id="a1f8c-107">Including jQuery</span></span>

<span data-ttu-id="a1f8c-108">Ниже приведены несколько распространенных способов для включения jQuery.</span><span class="sxs-lookup"><span data-stu-id="a1f8c-108">Below are some of the most common ways to include jQuery.</span></span>

### <a name="browser"></a><span data-ttu-id="a1f8c-109">Браузер</span><span class="sxs-lookup"><span data-stu-id="a1f8c-109">Browser</span></span>

#### <a name="script-tag"></a><span data-ttu-id="a1f8c-110">Тэг Script</span><span class="sxs-lookup"><span data-stu-id="a1f8c-110">Script tag</span></span>

```html
<script src="https://code.jquery.com/jquery-3.3.1.min.js"></script>
```

#### <a name="babel"></a><span data-ttu-id="a1f8c-111">Babel</span><span class="sxs-lookup"><span data-stu-id="a1f8c-111">Babel</span></span>

<span data-ttu-id="a1f8c-112">[Babel](http://babeljs.io/) — это компилятор JavaScript нового поколения.</span><span class="sxs-lookup"><span data-stu-id="a1f8c-112">[Babel](http://babeljs.io/) is a next generation JavaScript compiler.</span></span> <span data-ttu-id="a1f8c-113">Среди прочего, он уже умеет использовать модули ES6 или ES2015, хотя собственный код браузеров еще не поддерживает эту функцию.</span><span class="sxs-lookup"><span data-stu-id="a1f8c-113">One of the features is the ability to use ES6/ES2015 modules now, even though browsers do not yet support this feature natively.</span></span>

```js
import $ from "jquery";
```

#### <a name="browserifywebpack"></a><span data-ttu-id="a1f8c-114">Browserify и Webpack</span><span class="sxs-lookup"><span data-stu-id="a1f8c-114">Browserify/Webpack</span></span>

<span data-ttu-id="a1f8c-115">Существует несколько способов использовать [Browserify](http://browserify.org/) и [Webpack](https://webpack.github.io/).</span><span class="sxs-lookup"><span data-stu-id="a1f8c-115">There are several ways to use [Browserify](http://browserify.org/) and [Webpack](https://webpack.github.io/).</span></span> <span data-ttu-id="a1f8c-116">Дополнительные сведения об использовании этих средств вы можете найти в документации по соответствующему проекту.</span><span class="sxs-lookup"><span data-stu-id="a1f8c-116">For more information on using these tools, please refer to the corresponding project's documention.</span></span> <span data-ttu-id="a1f8c-117">В скриптах, в том числе скриптах jQuery, это выглядит обычно так.</span><span class="sxs-lookup"><span data-stu-id="a1f8c-117">In the script, including jQuery will usually look like this...</span></span>

```js
var $ = require("jquery");
```

#### <a name="amd-asynchronous-module-definition"></a><span data-ttu-id="a1f8c-118">AMD (определение асинхронного модуля)</span><span class="sxs-lookup"><span data-stu-id="a1f8c-118">AMD (Asynchronous Module Definition)</span></span>

<span data-ttu-id="a1f8c-119">Формат модулей AMD специально разработан для браузеров.</span><span class="sxs-lookup"><span data-stu-id="a1f8c-119">AMD is a module format built for the browser.</span></span> <span data-ttu-id="a1f8c-120">Подробные сведения вы найдете в [документации по require.js](http://requirejs.org/docs/whyamd.html).</span><span class="sxs-lookup"><span data-stu-id="a1f8c-120">For more information, we recommend [require.js' documentation](http://requirejs.org/docs/whyamd.html).</span></span>

```js
define(["jquery"], function($) {

});
```

### <a name="node"></a><span data-ttu-id="a1f8c-121">Узел</span><span class="sxs-lookup"><span data-stu-id="a1f8c-121">Node</span></span>

<span data-ttu-id="a1f8c-122">Чтобы включить jQuery в [узел](nodejs.org), прежде всего следует выполнить установку с помощью npm.</span><span class="sxs-lookup"><span data-stu-id="a1f8c-122">To include jQuery in [Node](nodejs.org), first install with npm.</span></span>

```sh
npm install jquery
```

<span data-ttu-id="a1f8c-123">Чтобы использовать jQuery в узле, требуется окно с документом.</span><span class="sxs-lookup"><span data-stu-id="a1f8c-123">For jQuery to work in Node, a window with a document is required.</span></span> <span data-ttu-id="a1f8c-124">Так как это окно не поддерживается в собственном коде узла, его следует смоделировать внешними средствами, например [jsdom](https://github.com/tmpvar/jsdom).</span><span class="sxs-lookup"><span data-stu-id="a1f8c-124">Since no such window exists natively in Node, one can be mocked by tools such as [jsdom](https://github.com/tmpvar/jsdom).</span></span> <span data-ttu-id="a1f8c-125">Это будет полезно для тестирования.</span><span class="sxs-lookup"><span data-stu-id="a1f8c-125">This can be useful for testing purposes.</span></span>

```js
require("jsdom").env("", function(err, window) {
    if (err) {
        console.error(err);
        return;
    }

    var $ = require("jquery")(window);
});
```
