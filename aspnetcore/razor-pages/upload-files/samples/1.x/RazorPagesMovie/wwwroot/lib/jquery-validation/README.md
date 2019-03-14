---
ms.openlocfilehash: 1b563a8c0674d51f893415221ca8fab574b78265
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57046551"
---
<a name="--"></a>--
================================

<span data-ttu-id="ae154-101">[![Состояние сборки](https://secure.travis-ci.org/jzaefferer/jquery-validation.png)](http://travis-ci.org/jzaefferer/jquery-validation)
[![Состояние devDependency](https://david-dm.org/jzaefferer/jquery-validation/dev-status.png?theme=shields.io)](https://david-dm.org/jzaefferer/jquery-validation#info=devDependencies)</span><span class="sxs-lookup"><span data-stu-id="ae154-101">[![Build Status](https://secure.travis-ci.org/jzaefferer/jquery-validation.png)](http://travis-ci.org/jzaefferer/jquery-validation)
[![devDependency Status](https://david-dm.org/jzaefferer/jquery-validation/dev-status.png?theme=shields.io)](https://david-dm.org/jzaefferer/jquery-validation#info=devDependencies)</span></span>

<span data-ttu-id="ae154-102">Подключаемый модуль проверки jQuery предоставляет проверку доступности для имеющихся форм, делая всевозможные настройки в соответствии с вашим приложением.</span><span class="sxs-lookup"><span data-stu-id="ae154-102">The jQuery Validation Plugin provides drop-in validation for your existing forms, while making all kinds of customizations to fit your application really easy.</span></span>

## <a name="help-the-projecthttppledgiecomcampaigns18159"></a>[<span data-ttu-id="ae154-103">Помощь проекту</span><span class="sxs-lookup"><span data-stu-id="ae154-103">Help the project</span></span>](http://pledgie.com/campaigns/18159)

<span data-ttu-id="ae154-104">[![Помощь проекту](http://www.pledgie.com/campaigns/18159.png?skin_name=chrome)](http://pledgie.com/campaigns/18159)</span><span class="sxs-lookup"><span data-stu-id="ae154-104">[![Help the project](http://www.pledgie.com/campaigns/18159.png?skin_name=chrome)](http://pledgie.com/campaigns/18159)</span></span>

<span data-ttu-id="ae154-105">Этот проект нуждается в помощи.</span><span class="sxs-lookup"><span data-stu-id="ae154-105">This project is looking for help!</span></span> <span data-ttu-id="ae154-106">[Вы можете внести пожертвование в пользу проекта с помощью кампании Pledgie](http://pledgie.com/campaigns/18159) и сообщить об этом другим.</span><span class="sxs-lookup"><span data-stu-id="ae154-106">[You can donate to the ongoing pledgie campaign](http://pledgie.com/campaigns/18159) and help spread the word.</span></span> <span data-ttu-id="ae154-107">Если вы использовали подключаемый модуль или планируете его использовать, подумайте о пожертвовании (поможет любая сумма).</span><span class="sxs-lookup"><span data-stu-id="ae154-107">If you've used the plugin, or plan to use, consider a donation - any amount will help.</span></span>

<span data-ttu-id="ae154-108">Вы можете найти план по затратам на странице [Pledgie](http://pledgie.com/campaigns/18159).</span><span class="sxs-lookup"><span data-stu-id="ae154-108">You can find the plan for how to spend the money on the [pledgie page](http://pledgie.com/campaigns/18159).</span></span>

## <a name="get-started"></a><span data-ttu-id="ae154-109">Приступая к работе</span><span class="sxs-lookup"><span data-stu-id="ae154-109">Get Started</span></span>

### <a name="downloading-the-prebuilt-files"></a><span data-ttu-id="ae154-110">Скачивание предварительно созданных файлов</span><span class="sxs-lookup"><span data-stu-id="ae154-110">Downloading the prebuilt files</span></span>

<span data-ttu-id="ae154-111">Предварительно созданные файлы можно загрузить по адресу http://jqueryvalidation.org/</span><span class="sxs-lookup"><span data-stu-id="ae154-111">Prebuilt files can be downloaded from http://jqueryvalidation.org/</span></span>

### <a name="downloading-the-latest-changes"></a><span data-ttu-id="ae154-112">Скачивание последних изменений</span><span class="sxs-lookup"><span data-stu-id="ae154-112">Downloading the latest changes</span></span>

<span data-ttu-id="ae154-113">Невыпущенные файлы разработки можно получить следующим образом:</span><span class="sxs-lookup"><span data-stu-id="ae154-113">The unreleased development files can be obtained by:</span></span>

 1. <span data-ttu-id="ae154-114">[Скачав](https://github.com/jzaefferer/jquery-validation/archive/master.zip) или выполнив разветвление репозитория.</span><span class="sxs-lookup"><span data-stu-id="ae154-114">[Downloading](https://github.com/jzaefferer/jquery-validation/archive/master.zip) or Forking this repository</span></span>
 2. <span data-ttu-id="ae154-115">[Настроив сборку](CONTRIBUTING.md#build-setup).</span><span class="sxs-lookup"><span data-stu-id="ae154-115">[Setup the build](CONTRIBUTING.md#build-setup)</span></span>
 3. <span data-ttu-id="ae154-116">Запустив `grunt` для создания файлов в каталоге dist.</span><span class="sxs-lookup"><span data-stu-id="ae154-116">Run `grunt` to create the built files in the "dist" directory</span></span>

### <a name="including-it-on-your-page"></a><span data-ttu-id="ae154-117">Добавление на странице</span><span class="sxs-lookup"><span data-stu-id="ae154-117">Including it on your page</span></span>

<span data-ttu-id="ae154-118">Добавьте jQuery и подключаемый модуль на странице.</span><span class="sxs-lookup"><span data-stu-id="ae154-118">Include jQuery and the plugin on a page.</span></span> <span data-ttu-id="ae154-119">Выберите форму для проверки и вызовите метод `validate`.</span><span class="sxs-lookup"><span data-stu-id="ae154-119">Then select a form to validate and call the `validate` method.</span></span>

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

<span data-ttu-id="ae154-120">Вы также можете включить jQuery и подключаемый модуль с помощью модуля requirejs.</span><span class="sxs-lookup"><span data-stu-id="ae154-120">Alternatively include jQuery and the plugin via requirejs in your module.</span></span>

```js
define(["jquery", "jquery.validate"], function( $ ) {
    $("form").validate();
});
```

<span data-ttu-id="ae154-121">Дополнительные сведения о том, как установить правила и настройки, см. в [документации](http://jqueryvalidation.org/documentation/).</span><span class="sxs-lookup"><span data-stu-id="ae154-121">For more information on how to setup a rules and customizations, [check the documentation](http://jqueryvalidation.org/documentation/).</span></span>

## <a name="reporting-issues-and-contributing-code"></a><span data-ttu-id="ae154-122">Сообщение о возникших проблемах и добавление кода</span><span class="sxs-lookup"><span data-stu-id="ae154-122">Reporting issues and contributing code</span></span>

<span data-ttu-id="ae154-123">Дополнительные сведения см. в [рекомендациях по дополнению](CONTRIBUTING.md).</span><span class="sxs-lookup"><span data-stu-id="ae154-123">See the [Contributing Guidelines](CONTRIBUTING.md) for details.</span></span>

<span data-ttu-id="ae154-124">**ВАЖНОЕ ПРИМЕЧАНИЕ О ПРОВЕРКЕ ЭЛЕКТРОННОЙ ПОЧТЫ**.</span><span class="sxs-lookup"><span data-stu-id="ae154-124">**IMPORTANT NOTE ABOUT EMAIL VALIDATION**.</span></span> <span data-ttu-id="ae154-125">Начиная с версии 1.12.0, этот подключаемый модуль использует то же регулярное выражение, которое [предлагает использовать спецификация HTML5 для браузеров](https://html.spec.whatwg.org/multipage/forms.html#valid-e-mail-address).</span><span class="sxs-lookup"><span data-stu-id="ae154-125">As of version 1.12.0 this plugin is using the same regular expression that the [HTML5 specification suggests for browsers to use](https://html.spec.whatwg.org/multipage/forms.html#valid-e-mail-address).</span></span> <span data-ttu-id="ae154-126">Мы будем следовать этому примеру и используем ту же проверку.</span><span class="sxs-lookup"><span data-stu-id="ae154-126">We will follow their lead and use the same check.</span></span> <span data-ttu-id="ae154-127">Если вы считаете, что спецификация неправильная, обратитесь к специалистам и сообщите о проблеме.</span><span class="sxs-lookup"><span data-stu-id="ae154-127">If you think the specification is wrong, please report the issue to them.</span></span> <span data-ttu-id="ae154-128">Если у вас есть различные требования, рассмотрите [использование настраиваемого метода](http://jqueryvalidation.org/jQuery.validator.addMethod/).</span><span class="sxs-lookup"><span data-stu-id="ae154-128">If you have different requirements, consider [using a custom method](http://jqueryvalidation.org/jQuery.validator.addMethod/).</span></span>

## <a name="license"></a><span data-ttu-id="ae154-129">Лицензия</span><span class="sxs-lookup"><span data-stu-id="ae154-129">License</span></span>
<span data-ttu-id="ae154-130">Авторские права &copy; принадлежат Йорну Заффереру (Jörn Zaefferer)</span><span class="sxs-lookup"><span data-stu-id="ae154-130">Copyright &copy; Jörn Zaefferer</span></span><br>
<span data-ttu-id="ae154-131">Лицензировано с задействованием лицензии MIT.</span><span class="sxs-lookup"><span data-stu-id="ae154-131">Licensed under the MIT license.</span></span>
