---
ms.openlocfilehash: 24c36493284988aa45b15c78e2577c0ef96aba56
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57029991"
---
<a name="jquery-validation-pluginhttpsjqueryvalidationorg---form-validation-made-easy"></a><span data-ttu-id="72caf-101">[Подключаемый модуль проверки jQuery](https://jqueryvalidation.org/) — упрощенная проверка форм</span><span class="sxs-lookup"><span data-stu-id="72caf-101">[jQuery Validation Plugin](https://jqueryvalidation.org/) - Form validation made easy</span></span>
================================

<span data-ttu-id="72caf-102">[![Состояние сборки](https://secure.travis-ci.org/jquery-validation/jquery-validation.svg)](https://travis-ci.org/jquery-validation/jquery-validation)
[![Состояние devDependency](https://david-dm.org/jquery-validation/jquery-validation/dev-status.svg?theme=shields.io)](https://david-dm.org/jquery-validation/jquery-validation#info=devDependencies)</span><span class="sxs-lookup"><span data-stu-id="72caf-102">[![Build Status](https://secure.travis-ci.org/jquery-validation/jquery-validation.svg)](https://travis-ci.org/jquery-validation/jquery-validation)
[![devDependency Status](https://david-dm.org/jquery-validation/jquery-validation/dev-status.svg?theme=shields.io)](https://david-dm.org/jquery-validation/jquery-validation#info=devDependencies)</span></span>

<span data-ttu-id="72caf-103">Подключаемый модуль проверки jQuery предоставляет проверку доступности для имеющихся форм, делая всевозможные настройки в соответствии с вашим приложением.</span><span class="sxs-lookup"><span data-stu-id="72caf-103">The jQuery Validation Plugin provides drop-in validation for your existing forms, while making all kinds of customizations to fit your application really easy.</span></span>

## <a name="getting-started"></a><span data-ttu-id="72caf-104">Начало работы</span><span class="sxs-lookup"><span data-stu-id="72caf-104">Getting Started</span></span>

### <a name="downloading-the-prebuilt-files"></a><span data-ttu-id="72caf-105">Скачивание предварительно созданных файлов</span><span class="sxs-lookup"><span data-stu-id="72caf-105">Downloading the prebuilt files</span></span>

<span data-ttu-id="72caf-106">Предварительно созданные файлы можно загрузить по адресу https://jqueryvalidation.org/</span><span class="sxs-lookup"><span data-stu-id="72caf-106">Prebuilt files can be downloaded from https://jqueryvalidation.org/</span></span>

### <a name="downloading-the-latest-changes"></a><span data-ttu-id="72caf-107">Скачивание последних изменений</span><span class="sxs-lookup"><span data-stu-id="72caf-107">Downloading the latest changes</span></span>

<span data-ttu-id="72caf-108">Невыпущенные файлы разработки можно получить следующим образом:</span><span class="sxs-lookup"><span data-stu-id="72caf-108">The unreleased development files can be obtained by:</span></span>

 1. <span data-ttu-id="72caf-109">[Скачав](https://github.com/jquery-validation/jquery-validation/archive/master.zip) или выполнив разветвление репозитория.</span><span class="sxs-lookup"><span data-stu-id="72caf-109">[Downloading](https://github.com/jquery-validation/jquery-validation/archive/master.zip) or Forking this repository</span></span>
 2. <span data-ttu-id="72caf-110">[Настроив сборку](CONTRIBUTING.md#build-setup).</span><span class="sxs-lookup"><span data-stu-id="72caf-110">[Setup the build](CONTRIBUTING.md#build-setup)</span></span>
 3. <span data-ttu-id="72caf-111">Запустив `grunt` для создания файлов в каталоге dist.</span><span class="sxs-lookup"><span data-stu-id="72caf-111">Run `grunt` to create the built files in the "dist" directory</span></span>

### <a name="including-it-on-your-page"></a><span data-ttu-id="72caf-112">Добавление на странице</span><span class="sxs-lookup"><span data-stu-id="72caf-112">Including it on your page</span></span>

<span data-ttu-id="72caf-113">Добавьте jQuery и подключаемый модуль на странице.</span><span class="sxs-lookup"><span data-stu-id="72caf-113">Include jQuery and the plugin on a page.</span></span> <span data-ttu-id="72caf-114">Выберите форму для проверки и вызовите метод `validate`.</span><span class="sxs-lookup"><span data-stu-id="72caf-114">Then select a form to validate and call the `validate` method.</span></span>

```html
<form>
    <input required>
</form>
<script src="jquery.js"></script>
<script src="jquery.validate.js"></script>
<script>
$("form").validate();
</script>
```

<span data-ttu-id="72caf-115">Вы также можете включить jQuery и подключаемый модуль с помощью модуля requirejs.</span><span class="sxs-lookup"><span data-stu-id="72caf-115">Alternatively include jQuery and the plugin via requirejs in your module.</span></span>

```js
define(["jquery", "jquery.validate"], function( $ ) {
    $("form").validate();
});
```

<span data-ttu-id="72caf-116">Дополнительные сведения о том, как установить правила и настройки, см. в [документации](https://jqueryvalidation.org/documentation/).</span><span class="sxs-lookup"><span data-stu-id="72caf-116">For more information on how to setup a rules and customizations, [check the documentation](https://jqueryvalidation.org/documentation/).</span></span>

## <a name="reporting-issues-and-contributing-code"></a><span data-ttu-id="72caf-117">Сообщение о возникших проблемах и добавление кода</span><span class="sxs-lookup"><span data-stu-id="72caf-117">Reporting issues and contributing code</span></span>

<span data-ttu-id="72caf-118">Дополнительные сведения см. в [рекомендациях по дополнению](CONTRIBUTING.md).</span><span class="sxs-lookup"><span data-stu-id="72caf-118">See the [Contributing Guidelines](CONTRIBUTING.md) for details.</span></span>

<span data-ttu-id="72caf-119">**ВАЖНОЕ ПРИМЕЧАНИЕ О ПРОВЕРКЕ ЭЛЕКТРОННОЙ ПОЧТЫ**.</span><span class="sxs-lookup"><span data-stu-id="72caf-119">**IMPORTANT NOTE ABOUT EMAIL VALIDATION**.</span></span> <span data-ttu-id="72caf-120">Начиная с версии 1.12.0, этот подключаемый модуль использует то же регулярное выражение, которое [предлагает использовать спецификация HTML5 для браузеров](https://html.spec.whatwg.org/multipage/forms.html#valid-e-mail-address).</span><span class="sxs-lookup"><span data-stu-id="72caf-120">As of version 1.12.0 this plugin is using the same regular expression that the [HTML5 specification suggests for browsers to use](https://html.spec.whatwg.org/multipage/forms.html#valid-e-mail-address).</span></span> <span data-ttu-id="72caf-121">Мы будем следовать этому примеру и используем ту же проверку.</span><span class="sxs-lookup"><span data-stu-id="72caf-121">We will follow their lead and use the same check.</span></span> <span data-ttu-id="72caf-122">Если вы считаете, что спецификация неправильная, обратитесь к специалистам и сообщите о проблеме.</span><span class="sxs-lookup"><span data-stu-id="72caf-122">If you think the specification is wrong, please report the issue to them.</span></span> <span data-ttu-id="72caf-123">Если у вас есть различные требования, рассмотрите [использование настраиваемого метода](https://jqueryvalidation.org/jQuery.validator.addMethod/).</span><span class="sxs-lookup"><span data-stu-id="72caf-123">If you have different requirements, consider [using a custom method](https://jqueryvalidation.org/jQuery.validator.addMethod/).</span></span>
<span data-ttu-id="72caf-124">Если вам нужно изменить встроенные шаблоны регулярных выражений для проверки, соблюдайте [инструкции, указанные в документации](https://jqueryvalidation.org/jQuery.validator.methods/).</span><span class="sxs-lookup"><span data-stu-id="72caf-124">In case you need to adjust the built-in validation regular expression patterns, please [follow the documentation](https://jqueryvalidation.org/jQuery.validator.methods/).</span></span>

<span data-ttu-id="72caf-125">**Важное примечание о методе REQUIRED**.</span><span class="sxs-lookup"><span data-stu-id="72caf-125">**IMPORTANT NOTE ABOUT REQUIRED METHOD**.</span></span> <span data-ttu-id="72caf-126">Начиная с версии 1.14.0, этот подключаемый модуль не удаляет концевые пробелы из значения вложенного элемента.</span><span class="sxs-lookup"><span data-stu-id="72caf-126">As of version 1.14.0 this plugin stops trimming white spaces from the value of the attached element.</span></span> <span data-ttu-id="72caf-127">Если вы хотите сохранить прежнее поведение, используйте [`normalizer`](https://jqueryvalidation.org/normalizer/) для преобразования значения элемента перед проверкой.</span><span class="sxs-lookup"><span data-stu-id="72caf-127">If you want to achieve the same result, you can use the [`normalizer`](https://jqueryvalidation.org/normalizer/) that can be used to transform the value of an element before validation.</span></span> <span data-ttu-id="72caf-128">Эта возможность доступна, начиная с версии `v1.15.0`.</span><span class="sxs-lookup"><span data-stu-id="72caf-128">This feature was available since `v1.15.0`.</span></span> <span data-ttu-id="72caf-129">Другими словами, вы можете применить что-то подобное:</span><span class="sxs-lookup"><span data-stu-id="72caf-129">In other words, you can do something like this:</span></span>
``` js
$("#myForm").validate({
    rules: {
        username: {
            required: true,
            // Using the normalizer to trim the value of the element
            // before validating it.
            //
            // The value of `this` inside the `normalizer` is the corresponding
            // DOMElement. In this example, `this` references the `username` element.
            normalizer: function(value) {
                return $.trim(value);
            }
        }
    }
});
```

## <a name="license"></a><span data-ttu-id="72caf-130">Лицензия</span><span class="sxs-lookup"><span data-stu-id="72caf-130">License</span></span>
<span data-ttu-id="72caf-131">Авторские права &copy; принадлежат Йорну Заффереру (Jörn Zaefferer)</span><span class="sxs-lookup"><span data-stu-id="72caf-131">Copyright &copy; Jörn Zaefferer</span></span><br>
<span data-ttu-id="72caf-132">Лицензировано с задействованием лицензии MIT.</span><span class="sxs-lookup"><span data-stu-id="72caf-132">Licensed under the MIT license.</span></span>
